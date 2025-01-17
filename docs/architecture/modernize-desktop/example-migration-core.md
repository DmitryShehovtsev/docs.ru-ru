---
title: Пример миграции на .NET Core 3.1
description: Показано, как перенести примеры приложений, предназначенных для .NET Framework в .NET Core 3,1.
ms.date: 05/12/2020
ms.openlocfilehash: 6a0311e9aaeb25ac39f3394d3a62e17046fe03d8
ms.sourcegitcommit: c4a15c6c4ecbb8a46ad4e67d9b3ab9b8b031d849
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/20/2020
ms.locfileid: "97866779"
---
# <a name="example-of-migrating-to-net-core-31"></a>Пример миграции на .NET Core 3.1

В этой главе представлены практические рекомендации, которые помогут выполнить миграцию существующего приложения из .NET Framework в .NET Core.

Мы представим хорошо структурированный процесс, который вы можете отслеживать, а также наиболее важные моменты, которые следует учитывать на каждом шаге.

Затем мы задокументировани пошаговый процесс миграции для примера классического приложения как из версий WinForms, так и для WPF.

## <a name="migration-process-overview"></a>Общие сведения о процессе миграции

Процесс миграции состоит из четырех последовательных шагов:

1. **Подготовка**. Изучите зависимости, которые проект должен иметь представление о дальнейших действиях. На этом шаге вы переведите текущий проект в состояние, которое упрощает точку запуска для миграции.

2. **Миграция файла проекта.** в проектах .NET Core используется новый формат проекта в стиле SDK. Создайте новый файл проекта с этим форматом или обновите его, чтобы использовать стиль пакета SDK.

3. **Исправление кода и сборки:** Создание кода в .NET Core различие между .NET Framework и .NET Core различается на уровне API. При необходимости обновите сторонние пакеты до тех, которые поддерживают .NET Core.

4. **Запуск и тестирование:** Могут возникнуть различия, которые не отображаются до времени выполнения. Поэтому не забудьте запустить приложение и проверить, что все работает правильно.

### <a name="preparation"></a>Подготовка

#### <a name="migrate-packagesconfig-file"></a>Миграция файла packages.config

В .NET Framework приложении все ссылки на внешние пакеты объявляются в файле *packages.config* . В .NET Core больше не нужно использовать файл *packages.config* . Вместо этого используйте свойство [PackageReference](../../core/project-sdk/msbuild-props.md#packagereference) в файле проекта, чтобы указать пакеты NuGet для приложения.

Поэтому необходимо перейти от одного формата к другому. Обновление можно выполнить вручную, используя зависимости, содержащиеся в файле *packages.config* , и перенести их в файл проекта в `PackageReference` формате. Вы также можете позволить Visual Studio выполнить свою работу: щелкните правой кнопкой мыши файл *packages.config* и выберите пункт **перенести packages.config в PackageReference** .

#### <a name="verify-every-dependency-compatibility-in-net-core"></a>Проверка каждой совместимости зависимостей в .NET Core

После переноса ссылок на пакеты необходимо проверить каждую ссылку на совместимость. Вы можете исследовать зависимости каждого пакета NuGet, используемого приложением в [NuGet.org](https://www.nuget.org/). Если пакет имеет .NET Standard зависимости, он будет работать в .NET Core, так как .NET Core 3,1 [поддерживает](../../standard/net-standard.md#net-implementation-support) все версии .NET Standard. На следующем рисунке показаны зависимости для `Castle.Windsor` пакета.

![Снимок экрана зависимостей NuGet для пакета Castle. Windsor](./media/example-migration-core/nuget-dependencies.png)

Чтобы проверить совместимость пакета, можно использовать средство <https://fuget.org> , предлагающее более подробные сведения о версиях и зависимостях.

Возможно, проект ссылается на старые версии пакетов, не поддерживающие .NET Core, но вы можете найти более новые версии, поддерживающие ее. Поэтому обновление пакетов до более новых версий обычно является хорошей рекомендацией. Однако следует учитывать, что обновление версии пакета может привести к внесению некоторых критических изменений, которые приведут к необходимости обновления кода.

Что произойдет, если вы не нашли совместимую версию? Что делать, если не нужно обновлять версию пакета из-за этих критических изменений? Не беспокойтесь, так как можно зависеть от пакетов .NET Framework из приложения .NET Core. Не забудьте серьезно протестировать ее, так как она может вызвать ошибки времени выполнения, если внешний пакет вызывает API, недоступный в .NET Core. Это очень удобно, если вы используете старый пакет, который не будет обновляться, и вы можете просто перенацелить работу на .NET Core.

#### <a name="check-for-api-compatibility"></a>Проверка совместимости API

Поскольку поверхность API в .NET Framework и .NET Core аналогична, но не идентична, необходимо проверить, какие интерфейсы API доступны в .NET Core, а какие нет. Средство анализатора переносимости .NET можно использовать для использования интерфейсов API, которые отсутствуют в .NET Core. Он рассматривает двоичный уровень приложения, извлекает все вызываемые API, а затем перечисляет, какие интерфейсы API недоступны в вашей целевой платформе (в данном случае это .NET Core 3,1).

Дополнительные сведения об этом средстве можно найти по адресу:

<https://docs.microsoft.com/dotnet/standard/analyzers/portability-analyzer>

Интересным аспектом этого средства является то, что он охватывает только отличия от собственного кода, а не код из внешних пакетов, которые нельзя изменить. Помните, что большинство этих пакетов следует обновить, чтобы они работали с .NET Core.

### <a name="migrate-project-file"></a>Перенос файла проекта

#### <a name="create-the-new-net-core-project"></a>Создание нового проекта .NET Core

В большинстве случаев необходимо обновить существующий проект до нового формата .NET Core. Однако можно также создать новый проект, сохранив старый. Основным недостатком обновления старого проекта является то, что вы потеряли поддержку конструктора, что может быть важным для вас. Если вы хотите продолжить работу с конструктором, необходимо создать новый проект .NET Core параллельно с прежним и общим ресурсам. Если необходимо изменить элементы пользовательского интерфейса в конструкторе, можно переключиться на старый проект, чтобы сделать это. А так как ресурсы связаны, они также будут обновлены в проекте .NET Core.

[Проект в стиле пакета SDK](../../core/project-sdk/msbuild-props.md) для .NET Core гораздо проще, чем формат проекта .NET Framework. За исключением упомянутых ранее `PackageReference` записей, вам больше не потребуется делать это. Новый формат проекта включает определенные расширения файлов по [умолчанию](../../core/tools/csproj.md#default-compilation-includes-in-net-core-projects), например `.cs` файлы и `.xaml` , без необходимости явно включать их в файл проекта.

#### <a name="assemblyinfo-considerations"></a>Рекомендации по Assembly.info

Атрибуты формируются автоматически в проектах .NET Core. Если проект содержит файл *AssemblyInfo.CS* , то определения будут дублироваться, что приведет к конфликтам компиляции. Вы можете удалить старый файл *AssemblyInfo.CS* или отключить автоматическое создание, добавив следующую запись в файл проекта .NET Core:

```xml
<Project Sdk="Microsoft.NET.Sdk.WindowsDesktop">
  <PropertyGroup>
    <GenerateAssemblyInfo>false</GenerateAssemblyInfo>
  </PropertyGroup>
</Project>
```

#### <a name="resources"></a>Ресурсы

Внедренные ресурсы включаются автоматически, но ресурсы — нет, поэтому необходимо перенести ресурсы в новый файл проекта.

#### <a name="package-references"></a>Ссылки на пакеты

С помощью параметра **Migrate packages.config to PackageReference** можно легко переместить ссылки на внешние пакеты в новый формат, как упоминалось ранее.

#### <a name="update-package-references"></a>Обновление ссылок на пакеты

Обновите версии пакетов, которые были бы совместимыми, как показано в предыдущем разделе.

### <a name="fix-the-code-and-build"></a>Исправление кода и сборка

#### <a name="microsoftwindowscompatibility"></a>Microsoft. Windows. Compatibility

Если приложение зависит от интерфейсов API, которые недоступны в .NET Core, таких как реестр, списки ACL или WCF, необходимо включить ссылку на `Microsoft.Windows.Compatibility` пакет, чтобы добавить эти API для Windows. Они работают с .NET Core, но не включены, так как они не являются кросс-платформенными.

Это средство, именуемое анализатором API ( <https://docs.microsoft.com/dotnet/standard/analyzers/api-analyzer> ), помогающее определить интерфейсы API, которые не совместимы с кодом.

#### <a name="use-if-directives"></a>Использовать \# директивы if

Если требуются разные пути выполнения при нацеливании на .NET Framework и .NET Core, следует использовать константы компиляции. Добавьте в \# код несколько директив if, чтобы иметь одинаковую базу кода для обеих целей.

#### <a name="technologies-not-available-on-net-core"></a>Технологии, недоступные в .NET Core

Некоторые технологии недоступны в .NET Core, например:

* Домены приложений
* Удаленное взаимодействие
* Управление доступом для кода
* Сервер WCF
* Рабочий процесс Windows

Именно поэтому необходимо найти замену этих технологий, если вы используете их в своем приложении. Дополнительные сведения см. в статье [.NET Framework технологии, недоступные в .NET Core](../../core/porting/net-framework-tech-unavailable.md) .

#### <a name="regenerate-autogenerated-clients"></a>Повторное создание автоматически сформированных клиентов

Если приложение использует автоматически сформированный код, например клиент WCF, может потребоваться повторно создать этот код для .NET Core. Иногда можно найти некоторые отсутствующие ссылки, так как они могут не быть включены в набор сборок .NET Core по умолчанию. С помощью такого средства <https://apisof.net/> , как, можно легко найти сборку, в которой находится отсутствующая ссылка, и добавить ее из NuGet.

#### <a name="rolling-back-package-versions"></a>Откат версий пакета

Как правило, мы уже упоминали, что вы лучше обновляете каждую версию одного пакета, чтобы обеспечить совместимость с .NET Core. Однако вы можете найти, что для обновленной и совместимой версий сборки просто не взимается. Если стоимость изменения не является приемлемой, можно рассмотреть возможность отката версий пакета, сохраняя те, которые используются в .NET Framework. Несмотря на то, что они не предназначены для .NET Core, они должны работать правильно, если они не вызывают некоторые неподдерживаемые API.

### <a name="run-and-test"></a>Запуск и тестирование

После создания приложения без ошибок можно запустить последний шаг миграции, проверив все функциональные возможности.

На этом заключительном этапе можно найти несколько различных проблем в зависимости от сложности приложения и используемых зависимостей и интерфейсов API.

Например, при использовании файлов конфигурации (*app.config*) могут возникнуть ошибки во время выполнения, такие как разделы конфигурации, которые отсутствуют. Использование `Microsoft.Extensions.Configuration` пакета NuGet должно исправить эту ошибку.

Другой причиной ошибок является использование `BeginInvoke` методов и, `EndInvoke` поскольку они не поддерживаются в .NET Core. Они не поддерживаются в .NET Core, так как они имеют зависимость от удаленного взаимодействия, которое не существует в .NET Core. Чтобы решить эту проблему, попробуйте использовать `await` ключевое слово (если доступно) или <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=nameWithType> метод.

Анализаторы совместимости можно использовать для выявления интерфейсов API и шаблонов кода в коде, которые могут вызывать проблемы во время выполнения с помощью .NET Core. Перейдите на страницу <https://github.com/dotnet/platform-compat> и используйте анализатор .NET API для своего проекта.

## <a name="migrating-a-windows-forms-application"></a>Перенос приложения Windows Forms

Чтобы продемонстрировать полный процесс миграции Windows Forms приложения, мы решили перенести пример приложения Ешоп, доступного по адресу <https://github.com/dotnet-architecture/eShopModernizing/tree/master/eShopLegacyNTier/src/eShopWinForms> . Полный результат миграции можно найти по адресу <https://github.com/dotnet-architecture/eShopModernizing/tree/master/eShopModernizedNTier/src/eShopWinForms> .

Это приложение показывает Каталог продуктов и позволяет пользователю перемещаться по продуктам, фильтровать их и выполнять поиск. С точки зрения архитектуры, приложение использует внешнюю службу WCF, которая служит фасадной для серверной базы данных.

Основное окно приложения можно увидеть на следующем рисунке:

![Главное окно приложения](./media/example-migration-core/main-application-window.png)

Если открыть *CSPROJ* -файл проекта, можно увидеть примерно следующее:

![Снимок экрана с содержимым файла CSPROJ](./media/example-migration-core/csproj-file.png)

Как упоминалось ранее, проект .NET Core имеет более компактный стиль, поэтому необходимо перенести структуру проекта в новый стиль пакет SDK для .NET Core.

В Обозреватель решений щелкните правой кнопкой мыши проект Windows Forms и выберите команду **Выгрузить проект**  >  **изменить**.

Теперь можно обновить CSPROJ файл. Вы удалите все содержимое и замените его следующим кодом:

```xml
<Project Sdk="Microsoft.NET.Sdk.WindowsDesktop">
    <PropertyGroup>
        <OutputType>WinExe</OutputType>
        <TargetFramework>netcoreapp3.1</TargetFramework>
        <UseWindowsForms>true</UseWindowsForms>
        <GenerateAssemblyInfo>false</GenerateAssemblyInfo>
    </PropertyGroup>
</Project>
```

Сохраните и перезагрузите проект. Теперь обновление файла проекта завершено, и проект предназначен для .NET Core.

Если скомпилировать проект на этом этапе, вы найдете некоторые ошибки, связанные со ссылкой на клиент WCF. Так как этот код создается автоматически, необходимо создать его повторно, чтобы он нацелиться на .NET Core.

![Снимок экрана с ошибками компиляции в Visual Studio](./media/example-migration-core/winforms-compilation-errors.png)

Удалите файл *Reference.CS* и создайте новый клиент службы.

Щелкните правой кнопкой мыши **подключенные службы** и выберите пункт **Добавить подключенную службу** .

![Снимок экрана: меню "Подключенные службы" с выбранным параметром "добавить подключенную службу"](./media/example-migration-core/add-connected-service.png)

Откроется окно Подключенные службы. Выберите параметр **веб-служба Microsoft WCF** .

![Снимок экрана окна Подключенные службы](./media/example-migration-core/connected-services-window.png)

Если у вас есть служба WCF в том же решении, что и в этом примере, вместо указания URL-адреса службы можно выбрать параметр **Discover** .

![Снимок экрана: окно "Настройка ссылки на веб-службу WCF"](./media/example-migration-core/configure-wcf-reference.png)

После обнаружения службы средство отражает контракт API, реализованный службой. Измените имя пространства имен, `eShopServiceReference` как показано на следующем рисунке:

![Снимок экрана: контракт API и пространство имен изменены](./media/example-migration-core/api-contract-namespace.png)

Нажмите кнопку **Готово** . Через некоторое время вы увидите созданный код.

Вы должны увидеть три автоматически создаваемых файла:

1. *Начало работы*: ссылка на GitHub, чтобы предоставить некоторую информацию о WCF.
2. *ConnectedService.json*: параметры конфигурации для подключения к службе.
3. *Reference.CS*: фактический код клиента WCF.

![Снимок экрана обозреватель решений окна с тремя автоматически созданными файлами](./media/example-migration-core/autogenerated-files.png)

При повторной компиляции вы увидите много ошибок, поступающих из файлов *CS* в папку *Helper* . Эта папка присутствовала в .NET Framework версии, но не включена в Old *. csproj*. Но при использовании нового проекта в стиле SDK каждый файл кода, который находится под расположением файла проекта, включается по умолчанию. То есть новый проект .NET Core пытается скомпилировать файлы в папке *Helper* . Так как эта папка не требуется, ее можно безопасно удалить.

Если скомпилировать проект еще раз и выполнить его, вы не увидите образы продукта. Проблема заключается в том, что теперь путь к файлам немного изменился. Чтобы устранить эту проблему, необходимо добавить в путь другой уровень глубины, обновив в файле `CatalogView.cs` строку:

```csharp
string image_name = Environment.CurrentDirectory + "\\..\\..\\Assets\\Images\\Catalog\\" + catalogItems.Picturefilename;
```

в

```csharp
string image_name = Environment.CurrentDirectory + "\\..\\..\\..\\Assets\\Images\\Catalog\\" + catalogItems.Picturefilename;
```

После этого изменения можно убедиться, что приложение запускается и работает должным образом в .NET Core.

## <a name="migrating-a-wpf-application"></a>Миграция приложения WPF

Мы будем использовать `Shop.ClassicWPF` пример приложения для выполнения миграции. На следующем рисунке показан снимок экрана приложения перед миграцией:

![Пример приложения перед миграцией](./media/example-migration-core/app-before-migration.png)

Это приложение использует локальную базу данных SQL Server Express для хранения сведений о каталоге продуктов. Доступ к этой базе данных осуществляется непосредственно из приложения WPF.

Сначала необходимо обновить файл *CSPROJ* до нового стиля SDK, используемого приложениями .NET Core. Вы выполните те же действия, которые описаны в Windows Forms миграции: вы выгружаете проект, открываете файл *. csproj* , обновляете его содержимое и перезагружаете проект.

В этом случае удалите все содержимое файла *CSPROJ* и замените его следующим кодом:

```xml
<Project Sdk="Microsoft.NET.Sdk.WindowsDesktop">
    <PropertyGroup>
        <OutputType>WinExe</OutputType>
        <TargetFramework>netcoreapp3.1</TargetFramework>
        <UseWpf>true</UseWpf>
        <GenerateAssemblyInfo>false</GenerateAssemblyInfo>
    </PropertyGroup>
</Project>
```

Если перезагрузить проект и скомпилировать его, вы получите следующую ошибку:

![Снимок экрана с ошибками компиляции в Visual Studio](./media/example-migration-core/wpf-compilation-error.png)

Так как вы удалили все содержимое *CSPROJ* , вы потеряли спецификацию ссылок проекта, присутствующую в старом проекте. Необходимо просто добавить эту строку в *CSPROJ* файл, чтобы включить ссылку на проект.

```xml
<ItemGroup>
    <ProjectReference Include="..\\eShop.SqlProvider\\eShop.SqlProvider.csproj" />
<ItemGroup>
```

Можно также разрешить Visual Studio, щелкнув правой кнопкой мыши узел **зависимости** и выбрав пункт **Добавить ссылку на проект**. Выберите проект из решения и нажмите кнопку " **ОК**":

![Снимок экрана: диалоговое окно диспетчера ссылок с выбранным проектом Ешоп. дескриптора SqlProvider](./media/example-migration-core/reference-manager.png)

После добавления ссылки на отсутствующий проект приложение компилируется и выполняется должным образом в .NET Core.

>[!div class="step-by-step"]
>[Назад](windows-migration.md)
>[Вперед](deploy-modern-applications.md)
