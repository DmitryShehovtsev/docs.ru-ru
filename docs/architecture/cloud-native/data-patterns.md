---
title: Шаблоны данных, ориентированные на облако
description: Создание архитектуры облачных приложений .NET для Azure | Собственные шаблоны данных в облаке
ms.date: 06/30/2019
ms.openlocfilehash: 0d251f3046fcd3f3a2f5d856a123a35d3f7ecff2
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2019
ms.locfileid: "73841825"
---
# <a name="cloud-native-data-patterns"></a>Шаблоны данных, ориентированные на облако

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

Хотя децентрализованные данные могут привести к повышению производительности, масштабируемости и экономии затрат, она также предоставляет множество проблем. Запросы данных между микрослужбами являются сложными. Транзакция, охватывающая микрослужбы, должна управляться программно, так как распределенные транзакции не поддерживаются в облачных приложениях. Вы перейдете из мира *немедленной согласованности* в *окончательную согласованность*.

Сейчас мы обсудим эти проблемы.

## <a name="cross-service-queries"></a>Запросы между службами

Как приложение запрашивает данные, распределенные по нескольким независимым микрослужбам?

Этот сценарий показан на рис. 5-4.

![Запросы между микрослужбами](./media/cross-service-query.png)

**Рис. 5-4**. Запросы между микрослужбами

Обратите внимание, как на предыдущем рисунке показана микрослужба корзины покупок, которая добавляет элемент в корзину пользователя. Хотя хранилище данных покупательской корзины содержит таблицу корзины и lineItem, она не содержит данных о продуктах или ценах, так как эти товары находятся в микрослужбах продукта и цены. Чтобы добавить элемент, микрослужбе корзины покупок требуются данные и цены на продукты. Что такое параметры для получения данных о продуктах и ценах?

На рис. 5-5 показано, как микрослужба корзины покупок выполняет прямой вызов по протоколу HTTP как к каталогу продуктов, так и к микрослужбам ценообразования.

![Прямой обмен данными по протоколу HTTP](./media/direct-http-communication.png)

**Рис. 5-5**. Прямой обмен данными по протоколу HTTP

В главе 4 мы обсуждали, как прямые вызовы HTTP между микрослужбами приводят к использованию системы и не считаются хорошей практикой.

Можно реализовать микрослужбу агрегатора, показанную на рисунке 5-6.

![Микрослужба агрегатора](./media/aggregator-microservice.png)

**Рис. 5-6**. Микрослужба агрегатора

Хотя этот подход инкапсулирует рабочий процесс бизнес-операций в отдельной микрослужбе, он добавляет сложность и по-прежнему приводит к прямым вызовам HTTP.

Распространенный подход к выполнению запросов между службами использует [шаблон материализованных представлений](https://docs.microsoft.com/azure/architecture/patterns/materialized-view), показанный на рис. 5-7.

![Шаблон материализованных представлений](./media/materialized-view-pattern.png)

**Figure5-7**. Шаблон материализованных представлений

С помощью этого шаблона вы напрямую размещаете локальную таблицу (которая называется *моделью чтения*) в службе корзины покупок, которая содержит денормализованную копию данных, необходимых для микрослужб продукта и ценообразования. Помещение этих данных в микрослужбу корзины покупок устраняет необходимость в вызове дорогостоящих вызовов между службами. Данные, локальные для службы, позволяют повысить время отклика и надежность.

Перехватить этот подход, теперь у вас есть дублирующиеся данные в системе. В собственных системах в облаке дублированные данные не считаются [антишаблоном](https://en.wikipedia.org/wiki/Anti-pattern) и обычно реализуются в собственных системах в облаке. Однако только одна система может быть владельцем любого набора данных, и необходимо реализовать механизм синхронизации для системы записи, чтобы обновить все связанные модели чтения, при каждом изменении базовых данных.

## <a name="transactional-support"></a>Поддержка транзакций

Хотя запросы между микрослужбами являются сложной задачей, реализация транзакции между микрослужбами может быть сложной. Встроенная задача поддержания согласованности данных между источниками данных, которые находятся в разных микрослужбах, не может быть неполной. На рис. 5-8 показана проблема.

![Транзакция в шаблоне Saga](./media/saga-transaction-operation.png)

**Рис. 5-8**. Реализация транзакции по микрослужбам

Обратите внимание на то, как на предыдущем рисунке пять независимых микрослужб участвуют в распределенной транзакции *создания заказа* . Однако транзакция для каждой из пяти отдельных микрослужб должна завершиться с ошибкой, или все они должны прерываться и выполнять откат операции. Хотя встроенная поддержка транзакций доступна внутри каждой микрослужбы, распределенная транзакция не поддерживается во всех пяти службах.

Так как поддержка транзакций необходима для того, чтобы эта операция поддерживала согласованность данных в каждой микрослужбе, необходимо программно создать распределенную транзакцию.

Популярным шаблоном программного добавления поддержки транзакций является [шаблон Saga](https://blog.couchbase.com/saga-pattern-implement-business-transactions-using-microservices-part/). Он реализуется путем группирования локальных транзакций вместе и последовательного вызова каждого из них. Если локальная транзакция завершается ошибкой, Saga прерывает операцию и вызывает набор [компенсирующих транзакций](https://docs.microsoft.com/azure/architecture/patterns/compensating-transaction) для отмены изменений, внесенных предыдущими локальными транзакциями. На рис. 5-9 показана неудачная транзакция с шаблоном Saga.

![Откат в шаблоне Saga](./media/saga-rollback-operation.png)

**Рис. 5-9**. Откат транзакции

Обратите внимание на то, как на предыдущем рисунке операция *женератеконтент* завершилась сбоем в микрослужбе музыки. Saga вызывает компенсирующие транзакции (красным цветом) для удаления содержимого, отмены платежа и отмены заказа, возвращая данные для каждой микрослужбы обратно в противоречивое состояние.

Шаблоны Saga обычно организуются как ряд связанных событий или организованы в виде набора связанных команд.

## <a name="cqrs-pattern"></a>Шаблон CQRS

CQRS или [Разделение команд и запросов](https://docs.microsoft.com/azure/architecture/patterns/cqrs)— шаблон архитектуры, который разделяет операции, считывающие данные из тех, которые записывают данные. Этот шаблон помогает повысить производительность, масштабируемость и безопасность.

В обычных сценариях доступа к данным реализуется одна модель (объект сущности и репозитория), которая *выполняет операции* чтения и записи данных.

Однако более продвинутый сценарий доступа к данным может выиграть от отдельных моделей и таблиц данных для операций чтения и записи. Чтобы повысить производительность, операция считывания, известная как *запрос*, может выполнить запрос к строго денормализованному представлению данных, чтобы избежать дорогостоящих повторяющихся соединений таблиц. В то время как операция *записи* , называемая *командой*, может обновляться по полностью нормализованному представлению данных. Затем необходимо реализовать механизм, обеспечивающий синхронизацию обоих представлений. Как правило, при изменении таблицы записи возникает событие, которое реплицирует изменение данных в таблицу чтения.

На рис. 5-10 показана реализация шаблона CQRS.

![Реализация CQRS](./media/cqrs-implementation.png)

**Рис. 5-10**. Реализация CQRS

Обратите внимание на то, как на предыдущем рисунке реализована отдельная модель команд и запросов. Более того, каждая операция записи данных сохраняется в хранилище записи и затем передается в хранилище для чтения. Обратите особое внимание на то, как процесс распространения работает с принципом [окончательной согласованности](https://www.cloudcomputingpatterns.org/eventual_consistency/), в то время как модель чтения в конечном итоге синхронизируется с моделью записи, но в процессе может возникнуть некоторое запаздывание.

Реализуя разделение, вы можете масштабировать операции чтения и записи отдельно. Кроме того, при операциях записи может быть обеспечена более строгая безопасность, чем в отношении операций чтения.

Как правило, шаблоны CQRS применяются к ограниченным разделам системы в зависимости от конкретных потребностей.

## <a name="relational-vs-nosql"></a>Реляционная VS NoSQL

Влияние технологий [NoSQL](https://www.geeksforgeeks.org/introduction-to-nosql/) не может быть слишком строгим, особенно для распределенных облачных систем. Распространение новых технологий для работы с данными в этом пространстве приводит к нарушению работы решений, которые в монопольном режиме пополагались на реляционные базы данных.

С одной стороны, реляционные базы данных были распространенной технологией для десятилетий. Они являются зрелыми, проверенными и широко реализованными. Конкурирующие продукты баз данных, опыт и инструментарий абаундс. Реляционные базы данных предоставляют хранилище связанных таблиц данных. Эти таблицы имеют фиксированную схему, используют SQL (язык SQL) для управления данными и имеют гарантии [ACID](https://www.geeksforgeeks.org/acid-properties-in-dbms/) (также известной как атомарность, согласованность, изоляция и устойчивость).

Базы данных No-SQL, на другой стороне, относятся к высокопроизводительным, нереляционным хранилищам данных. Эти приложения Excel позволяют легко использовать, масштабируемость, устойчивость и характеристики доступности. Вместо объединения таблиц нормализованных данных NoSQL хранит Самоописывающие (без схемы) данные обычно в документах JSON. Они не предлагают гарантий [ACID](https://www.geeksforgeeks.org/acid-properties-in-dbms/) .

Способ понять различия между этими типами баз данных можно найти в [теоремае Cap](https://towardsdatascience.com/cap-theorem-and-distributed-database-management-systems-5c2be977950e), наборе принципов, которые можно применить к распределенным системам, в которых хранится состояние. На рис. 5-11 показаны три свойства теоремаа CAP.

![Теорема CAP](./media/cap-theorem.png)

**Рис. 5-11**. Теорема CAP

Теорема утверждает, что любая распределенная система данных будет предоставлять компромисс между согласованностью, доступностью и отклонениям секций, и что любая база данных может гарантировать только два из трех свойств:

- *Согласованность*. Каждый узел в кластере будет отвечать последним данным, даже если он требует блокировки запроса, пока все реплики не будут правильно обновлены.

- *Доступность*. Каждый узел будет возвращать ответ в разумное время, даже если этот ответ не является самыми последними данными.

- *Допуск секции*: гарантирует, что система продолжит работу в случае сбоя узла или потери связи с другим.

Реляционные базы данных представляют согласованность и доступность, но не допускают отклонения секций. Секционирование реляционной базы данных, например сегментирование, является сложной задачей и может повлиять на производительность.

С другой стороны, базы данных NoSQL обычно демонстрируют допустимость разбиения на разделы, которая называется горизонтальной масштабируемостью и высокой доступностью. Как теорема ограничения указывает, вы можете иметь только два из трех принципов, и вы потеряли свойство согласованности.

Базы данных NoSQL распределяются и обычно масштабируются на серверах. Это может обеспечить высокую доступность как внутри, так и между географическими регионами с меньшими затратами. Данные можно секционировать и реплицировать на этих компьютерах или узлах, обеспечивая избыточность и отказоустойчивость. Недостатком является согласованность. Изменение данных на одном узле NoSQL может занять некоторое время для распространения на другие узлы. Как правило, узел базы данных NoSQL предоставит немедленный ответ на запрос, даже если данные, которые он представляет, устарели и еще не обновлены.

Это известная [Окончательная согласованность](https://www.cloudcomputingpatterns.org/eventual_consistency/), характеристика распределенных систем данных, в которой транзакции ACID не поддерживаются. Это небольшая задержка между обновлением элемента данных и временем, которое требуется для распространения этого обновления на каждый из узлов реплик. Если обновить элемент продукта в базе данных NoSQL в США, но в то же время запросите тот же элемент данных из узла реплики в Европе, вы можете получить сведения о продукте более ранней версии до тех пор, пока не будет обновлен Европейский узел с изменением продукта. Компромисс заключается в том, что благодаря [надежной согласованности](https://en.wikipedia.org/wiki/Strong_consistency), ожидающей обновления всех узлов реплики перед возвратом результата запроса, можно поддерживать огромные масштабы и объем трафика, но с возможностью представления более старых данных.

Базы данных NoSQL можно классифицировать по следующим четырем моделям:

- *Хранилище документов* (MongoDB, CouchDB, Couchbase): данные (и соответствующие метаданные) хранятся нереляционно в денормализованных документах на основе JSON внутри базы данных.

- *Хранилище "ключ — значение* " (Redis, Риак, memcached): данные хранятся в виде простых пар "ключ-значение" с системными операциями, выполняемыми по уникальному ключу доступа, сопоставленному со значением данных пользователя.

- *Хранилище в широких столбцах* (HBase, Cassandra). связанные данные хранятся в формате столбцов в виде набора пар «вложенные ключ-значение» в одном столбце, при этом данные обычно извлекаются в виде одной единицы без объединения нескольких таблиц.

- *Хранилища графов* (neo4j, Titan): данные хранятся в виде графического представления внутри узла вместе с краями, задающих связь между узлами.

Базы данных NoSQL можно оптимизировать для работы с крупномасштабными данными, особенно если данные относительно просты. Рассмотрим базу данных NoSQL, когда:

- Для рабочей нагрузки требуется крупномасштабная и высокая степень параллелизма.
- У вас большое число пользователей.
- Данные могут быть выражены просто без связей.
- Необходимо географически распределить данные.
- Вам не нужны гарантии ACID.
- Будет развернут на оборудование для товара.

Затем рассмотрим реляционную базу данных в следующих случаях:

- Для рабочих нагрузок требуется средний или большой масштаб.
- Параллелизм не является серьезной проблемой.
- Необходимы гарантии ACID.
- Данные лучше выразить реляционно.
- Приложение будет развернуто на большом и высоком оборудовании.

Далее мы рассмотрим хранилище данных в облаке Azure.

>[!div class="step-by-step"]
>[Назад](distributed-data.md)
>[Вперед](azure-data-storage.md)