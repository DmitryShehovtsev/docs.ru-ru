---
title: Установка .NET Core в openSUSE (.NET Core)
description: Здесь приводятся различные способы установки пакета SDK для .NET Core и среды выполнения .NET Core в openSUSE.
author: adegeo
ms.author: adegeo
ms.date: 06/04/2020
ms.openlocfilehash: 24f0a5b5278d038c2f941b0984efcacd91dcbe31
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ru-RU
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619472"
---
# <a name="install-net-core-sdk-or-net-core-runtime-on-opensuse"></a><span data-ttu-id="d378f-103">Установка пакета SDK для .NET Core или среды выполнения .NET Core в openSUSE</span><span class="sxs-lookup"><span data-stu-id="d378f-103">Install .NET Core SDK or .NET Core Runtime on openSUSE</span></span>

<span data-ttu-id="d378f-104">.NET Core поддерживается в openSUSE.</span><span class="sxs-lookup"><span data-stu-id="d378f-104">.NET Core is supported on openSUSE.</span></span> <span data-ttu-id="d378f-105">В этой статье описано, как установить .NET Core в openSUSE.</span><span class="sxs-lookup"><span data-stu-id="d378f-105">This article describes how to install .NET Core on openSUSE.</span></span>

[!INCLUDE [linux-intro-sdk-vs-runtime](includes/linux-intro-sdk-vs-runtime.md)]

[!INCLUDE [linux-install-package-manager-x64-vs-arm](includes/linux-install-package-manager-x64-vs-arm.md)]

## <a name="supported-distributions"></a><span data-ttu-id="d378f-106">Поддерживаемые дистрибутивы</span><span class="sxs-lookup"><span data-stu-id="d378f-106">Supported distributions</span></span>

<span data-ttu-id="d378f-107">В следующей таблице приведен список выпусков .NET Core, которые сейчас поддерживаются в openSUSE 15.</span><span class="sxs-lookup"><span data-stu-id="d378f-107">The following table is a list of currently supported .NET Core releases on openSUSE 15.</span></span> <span data-ttu-id="d378f-108">Эти версии поддерживаются до тех пор, пока для версии [.NET Core](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) или версии openSUSE не будет прекращена поддержка.</span><span class="sxs-lookup"><span data-stu-id="d378f-108">These versions remain supported until either the version of [.NET Core reaches end-of-support](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) or the version of openSUSE is no longer supported.</span></span>

- <span data-ttu-id="d378f-109">Значок ✔️ означает, что версия openSUSE или .NET Core поддерживается.</span><span class="sxs-lookup"><span data-stu-id="d378f-109">A ✔️ indicates that the version of openSUSE or .NET Core is still supported.</span></span>
- <span data-ttu-id="d378f-110">Значок ❌ означает, что версия openSUSE или версия .NET Core в таком выпуске openSUSE не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="d378f-110">A ❌ indicates that the version of openSUSE or .NET Core isn't supported on that openSUSE release.</span></span>
- <span data-ttu-id="d378f-111">Если значок ✔️ стоит как напротив версии openSUSE, так и напротив версии .NET Core, это значит, что такое сочетание ОС и .NET поддерживается.</span><span class="sxs-lookup"><span data-stu-id="d378f-111">When both a version of openSUSE and a version of .NET Core have ✔️, that OS and .NET combination are supported.</span></span>

| <span data-ttu-id="d378f-112">openSUSE</span><span class="sxs-lookup"><span data-stu-id="d378f-112">openSUSE</span></span>                   | <span data-ttu-id="d378f-113">.NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="d378f-113">.NET Core 2.1</span></span> | <span data-ttu-id="d378f-114">.NET Core 3.1</span><span class="sxs-lookup"><span data-stu-id="d378f-114">.NET Core 3.1</span></span> | <span data-ttu-id="d378f-115">Предварительная версия .NET 5 (только установка вручную)</span><span class="sxs-lookup"><span data-stu-id="d378f-115">.NET 5 Preview (manual install only)</span></span> |
|----------------------------|---------------|---------------|----------------|
| <span data-ttu-id="d378f-116">✔️ [15](#opensuse-15-)</span><span class="sxs-lookup"><span data-stu-id="d378f-116">✔️ [15](#opensuse-15-)</span></span>     | <span data-ttu-id="d378f-117">✔️ 2.1</span><span class="sxs-lookup"><span data-stu-id="d378f-117">✔️ 2.1</span></span>        | <span data-ttu-id="d378f-118">✔️ 3.1</span><span class="sxs-lookup"><span data-stu-id="d378f-118">✔️ 3.1</span></span>        | <span data-ttu-id="d378f-119">✔️ 5.0 (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="d378f-119">✔️ 5.0 Preview</span></span> |

<span data-ttu-id="d378f-120">Следующие версии .NET Core больше не поддерживаются</span><span class="sxs-lookup"><span data-stu-id="d378f-120">The following versions of .NET Core are no longer supported.</span></span> <span data-ttu-id="d378f-121">(но остаются доступными для скачивания):</span><span class="sxs-lookup"><span data-stu-id="d378f-121">The downloads for these still remain published:</span></span>

- <span data-ttu-id="d378f-122">3.0</span><span class="sxs-lookup"><span data-stu-id="d378f-122">3.0</span></span>
- <span data-ttu-id="d378f-123">2.2</span><span class="sxs-lookup"><span data-stu-id="d378f-123">2.2</span></span>
- <span data-ttu-id="d378f-124">2.0</span><span class="sxs-lookup"><span data-stu-id="d378f-124">2.0</span></span>

## <a name="how-to-install-other-versions"></a><span data-ttu-id="d378f-125">Установка других версий</span><span class="sxs-lookup"><span data-stu-id="d378f-125">How to install other versions</span></span>

[!INCLUDE [package-manager-switcher](./includes/package-manager-heading-hack-pkgname.md)]

## <a name="opensuse-15-"></a><span data-ttu-id="d378f-126">openSUSE 15 ✔️</span><span class="sxs-lookup"><span data-stu-id="d378f-126">openSUSE 15 ✔️</span></span>

[!INCLUDE [linux-prep-intro-generic](includes/linux-prep-intro-generic.md)]

```bash
sudo zypper install libicu
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
wget https://packages.microsoft.com/config/opensuse/15/prod.repo
sudo mv prod.repo /etc/zypp/repos.d/microsoft-prod.repo
sudo chown root:root /etc/zypp/repos.d/microsoft-prod.repo
```

[!INCLUDE [linux-zyp-install-31](includes/linux-install-31-zyp.md)]

## <a name="troubleshoot-the-package-manager"></a><span data-ttu-id="d378f-127">Устранение неполадок диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="d378f-127">Troubleshoot the package manager</span></span>

<span data-ttu-id="d378f-128">В этом разделе описаны распространенные ошибки, которые могут возникнуть при использовании диспетчера пакетов для установки .NET Core.</span><span class="sxs-lookup"><span data-stu-id="d378f-128">This section provides information on common errors you may get while using the package manager to install .NET Core.</span></span>

### <a name="failed-to-fetch"></a><span data-ttu-id="d378f-129">Ошибка получения</span><span class="sxs-lookup"><span data-stu-id="d378f-129">Failed to fetch</span></span>

[!INCLUDE [package-manager-failed-to-fetch-rpm](includes/package-manager-failed-to-fetch-rpm.md)]

## <a name="snap"></a><span data-ttu-id="d378f-130">Snap-пакеты</span><span class="sxs-lookup"><span data-stu-id="d378f-130">Snap</span></span>

[!INCLUDE [linux-install-snap](includes/linux-install-snap.md)]

## <a name="dependencies"></a><span data-ttu-id="d378f-131">Зависимости</span><span class="sxs-lookup"><span data-stu-id="d378f-131">Dependencies</span></span>

<span data-ttu-id="d378f-132">Если для установки используется диспетчер пакетов, эти библиотеки устанавливаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="d378f-132">When you install with a package manager, these libraries are installed for you.</span></span> <span data-ttu-id="d378f-133">Но если вы устанавливаете .NET Core вручную или публикуете автономное приложение, вам потребуется установить эти библиотеки:</span><span class="sxs-lookup"><span data-stu-id="d378f-133">But, if you manually install .NET Core or you publish a self-contained app, you'll need to make sure these libraries are installed:</span></span>

- <span data-ttu-id="d378f-134">krb5</span><span class="sxs-lookup"><span data-stu-id="d378f-134">krb5</span></span>
- <span data-ttu-id="d378f-135">libicu</span><span class="sxs-lookup"><span data-stu-id="d378f-135">libicu</span></span>
- <span data-ttu-id="d378f-136">libopenssl1_0_0</span><span class="sxs-lookup"><span data-stu-id="d378f-136">libopenssl1_0_0</span></span>

<span data-ttu-id="d378f-137">Если в целевой среде выполнения установлена версия OpenSSL 1.1 или более поздняя, необходимо установить **compat-openssl10**.</span><span class="sxs-lookup"><span data-stu-id="d378f-137">If the target runtime environment's OpenSSL version is 1.1 or newer, you'll need to install **compat-openssl10**.</span></span>

<span data-ttu-id="d378f-138">Дополнительные сведения о зависимостях см. в статье об [автономных приложениях Linux](https://github.com/dotnet/core/blob/master/Documentation/self-contained-linux-apps.md).</span><span class="sxs-lookup"><span data-stu-id="d378f-138">For more information about the dependencies, see [Self-contained Linux apps](https://github.com/dotnet/core/blob/master/Documentation/self-contained-linux-apps.md).</span></span>

<span data-ttu-id="d378f-139">Для приложений .NET Core, использующих сборку *System.Drawing.Common*, необходима также следующая зависимость:</span><span class="sxs-lookup"><span data-stu-id="d378f-139">For .NET Core apps that use the *System.Drawing.Common* assembly, you'll also need the following dependency:</span></span>

- [<span data-ttu-id="d378f-140">libgdiplus (версии 6.0.1 или выше)</span><span class="sxs-lookup"><span data-stu-id="d378f-140">libgdiplus (version 6.0.1 or later)</span></span>](https://www.mono-project.com/docs/gui/libgdiplus/)

  > [!WARNING]
  > <span data-ttu-id="d378f-141">Вы можете установить последнюю версию *libgdiplus*, добавив в систему репозиторий Mono.</span><span class="sxs-lookup"><span data-stu-id="d378f-141">You can install a recent version of *libgdiplus* by adding the Mono repository to your system.</span></span> <span data-ttu-id="d378f-142">Для получения дополнительной информации см. <https://www.mono-project.com/download/stable/>.</span><span class="sxs-lookup"><span data-stu-id="d378f-142">For more information, see <https://www.mono-project.com/download/stable/>.</span></span>

## <a name="scripted-install"></a><span data-ttu-id="d378f-143">Установка с помощью скрипта</span><span class="sxs-lookup"><span data-stu-id="d378f-143">Scripted install</span></span>

[!INCLUDE [linux-install-scripted](includes/linux-install-scripted.md)]

## <a name="manual-install"></a><span data-ttu-id="d378f-144">Установка вручную</span><span class="sxs-lookup"><span data-stu-id="d378f-144">Manual install</span></span>

[!INCLUDE [linux-install-manual](includes/linux-install-manual.md)]

## <a name="next-steps"></a><span data-ttu-id="d378f-145">Следующие шаги</span><span class="sxs-lookup"><span data-stu-id="d378f-145">Next steps</span></span>

- [<span data-ttu-id="d378f-146">Учебник. Создание консольного приложения с помощью пакета SDK для .NET Core в Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="d378f-146">Tutorial: Create a console application with .NET Core SDK using Visual Studio Code</span></span>](../tutorials/with-visual-studio-code.md)