---
title: "Сравнение XPath и LINQ to XML1 | Документы Microsoft"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: c3fd07c1-6761-4e4b-8eb1-ddd780ed8d44
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 0cd533442604a8fff23e5573f907aa157a723f11
ms.contentlocale: ru-ru
ms.lasthandoff: 04/12/2017


---
# <a name="comparison-of-xpath-and-linq-to-xml"></a><span data-ttu-id="7b80f-102">Сравнительные характеристики XPath и LINQ to XML</span><span class="sxs-lookup"><span data-stu-id="7b80f-102">Comparison of XPath and LINQ to XML</span></span>
<span data-ttu-id="7b80f-103">XPath и [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] имеют некоторые сходные функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="7b80f-103">XPath and [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] offer some similar functionality.</span></span> <span data-ttu-id="7b80f-104">И то и другое можно использовать, чтобы запрашивать XML-дерево для возвращения таких результатов, как коллекция элементов, коллекция атрибутов, коллекция узлов или значение элемента или атрибута.</span><span class="sxs-lookup"><span data-stu-id="7b80f-104">Both can be used to query an XML tree, returning such results as a collection of elements, a collection of attributes, a collection of nodes, or the value of an element or attribute.</span></span> <span data-ttu-id="7b80f-105">Однако между ними также есть некоторые различия.</span><span class="sxs-lookup"><span data-stu-id="7b80f-105">However, there are also some differences.</span></span>  
  
## <a name="differences-between-xpath-and-linq-to-xml"></a><span data-ttu-id="7b80f-106">Различия между XPath и LINQ to XML</span><span class="sxs-lookup"><span data-stu-id="7b80f-106">Differences Between XPath and LINQ to XML</span></span>  
 <span data-ttu-id="7b80f-107">XPath не поддерживает проекции новых типов.</span><span class="sxs-lookup"><span data-stu-id="7b80f-107">XPath does not allow projection of new types.</span></span> <span data-ttu-id="7b80f-108">Может возвращать только коллекции узлов из дерева, тогда как [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] может выполнить запрос, проецировав граф объектов или XML-дерево в новой форме.</span><span class="sxs-lookup"><span data-stu-id="7b80f-108">It can only return collections of nodes from the tree, whereas [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] can execute a query and project an object graph or an XML tree in a new shape.</span></span> <span data-ttu-id="7b80f-109">Запросы [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] гораздо более эффективны и обладают большими возможностями, чем выражения XPath.</span><span class="sxs-lookup"><span data-stu-id="7b80f-109">[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] queries encompass much more functionality and are much more powerful than XPath expressions.</span></span>  
  
 <span data-ttu-id="7b80f-110">Выражение XPath представлено в изолированном виде, внутри строки.</span><span class="sxs-lookup"><span data-stu-id="7b80f-110">XPath expressions exist in isolation within a string.</span></span> <span data-ttu-id="7b80f-111">Компилятор Visual Basic не удается выполнить синтаксический анализ выражения XPath во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="7b80f-111">The Visual Basic compiler cannot help parse the XPath expression at compile time.</span></span> <span data-ttu-id="7b80f-112">Напротив [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] запросы анализируются и компилируются компилятором основных участников.</span><span class="sxs-lookup"><span data-stu-id="7b80f-112">By contrast, [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] queries are parsed and compiled by theVisual Basic compiler.</span></span> <span data-ttu-id="7b80f-113">Компилятор способен обнаруживать многие ошибки запроса.</span><span class="sxs-lookup"><span data-stu-id="7b80f-113">The compiler is able to catch many query errors.</span></span>  
  
 <span data-ttu-id="7b80f-114">Результаты XPath не являются строго типизированными.</span><span class="sxs-lookup"><span data-stu-id="7b80f-114">XPath results are not strongly typed.</span></span> <span data-ttu-id="7b80f-115">В некоторых ситуациях результатом вычисления выражения XPath является объект, а задача определения соответствующего типа и приведения результата в соответствии с необходимостью возлагается на разработчика.</span><span class="sxs-lookup"><span data-stu-id="7b80f-115">In a number of circumstances, the result of evaluating an XPath expression is an object, and it is up to the developer to determine the proper type and cast the result as necessary.</span></span> <span data-ttu-id="7b80f-116">В отличие от этого, проекции на основе запроса [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] являются строго типизированными.</span><span class="sxs-lookup"><span data-stu-id="7b80f-116">By contrast, the projections from a [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] query are strongly typed.</span></span>  
  
## <a name="result-ordering"></a><span data-ttu-id="7b80f-117">Упорядочение результатов</span><span class="sxs-lookup"><span data-stu-id="7b80f-117">Result Ordering</span></span>  
 <span data-ttu-id="7b80f-118">В документе XPath 1.0 Recommendation указано, что коллекция, которая является результатом вычисления выражения XPath, не упорядочена.</span><span class="sxs-lookup"><span data-stu-id="7b80f-118">The XPath 1.0 Recommendation states that a collection that is the result of evaluating an XPath expression is unordered.</span></span>  
  
 <span data-ttu-id="7b80f-119">Однако при просмотре коллекции, возвращенной методом оси [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] XPath, можно отметить, что узлы в коллекции возвращены в том же порядке, что и в документе.</span><span class="sxs-lookup"><span data-stu-id="7b80f-119">However, when iterating through a collection returned by a [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] XPath axis method, the nodes in the collection are returned in document order.</span></span> <span data-ttu-id="7b80f-120">И они располагаются так даже при доступе к осям XPath, где предикаты выражены в обратном порядке по отношению к документу, например `preceding` и `preceding-sibling`.</span><span class="sxs-lookup"><span data-stu-id="7b80f-120">This is the case even when accessing the XPath axes where predicates are expressed in terms of reverse document order, such as `preceding` and `preceding-sibling`.</span></span>  
  
 <span data-ttu-id="7b80f-121">Напротив, большинство [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] осей возвращают коллекции в порядке документа, однако две из них, <xref:System.Xml.Linq.XNode.Ancestors%2A>и <xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A>, возвращают коллекции в обратном порядке документа.</xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A> </xref:System.Xml.Linq.XNode.Ancestors%2A></span><span class="sxs-lookup"><span data-stu-id="7b80f-121">By contrast, most of the [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] axes return collections in document order, but two of them, <xref:System.Xml.Linq.XNode.Ancestors%2A> and <xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A>, return collections in reverse document order.</span></span> <span data-ttu-id="7b80f-122">В следующей таблице перечисляются эти оси и указывается порядок коллекций для каждой из них.</span><span class="sxs-lookup"><span data-stu-id="7b80f-122">The following table enumerates the axes, and indicates collection order for each:</span></span>  
  
|<span data-ttu-id="7b80f-123">Ось LINQ to XML</span><span class="sxs-lookup"><span data-stu-id="7b80f-123">LINQ to XML axis</span></span>|<span data-ttu-id="7b80f-124">Упорядочение</span><span class="sxs-lookup"><span data-stu-id="7b80f-124">Ordering</span></span>|  
|----------------------|--------------|  
|<span data-ttu-id="7b80f-125">XContainer.DescendantNodes</span><span class="sxs-lookup"><span data-stu-id="7b80f-125">XContainer.DescendantNodes</span></span>|<span data-ttu-id="7b80f-126">Порядок документа</span><span class="sxs-lookup"><span data-stu-id="7b80f-126">Document order</span></span>|  
|<span data-ttu-id="7b80f-127">XContainer.Descendants</span><span class="sxs-lookup"><span data-stu-id="7b80f-127">XContainer.Descendants</span></span>|<span data-ttu-id="7b80f-128">Порядок документа</span><span class="sxs-lookup"><span data-stu-id="7b80f-128">Document order</span></span>|  
|<span data-ttu-id="7b80f-129">XContainer.Elements</span><span class="sxs-lookup"><span data-stu-id="7b80f-129">XContainer.Elements</span></span>|<span data-ttu-id="7b80f-130">Порядок документа</span><span class="sxs-lookup"><span data-stu-id="7b80f-130">Document order</span></span>|  
|<span data-ttu-id="7b80f-131">XContainer.Nodes</span><span class="sxs-lookup"><span data-stu-id="7b80f-131">XContainer.Nodes</span></span>|<span data-ttu-id="7b80f-132">Порядок документа</span><span class="sxs-lookup"><span data-stu-id="7b80f-132">Document order</span></span>|  
|<span data-ttu-id="7b80f-133">XContainer.NodesAfterSelf</span><span class="sxs-lookup"><span data-stu-id="7b80f-133">XContainer.NodesAfterSelf</span></span>|<span data-ttu-id="7b80f-134">Порядок документа</span><span class="sxs-lookup"><span data-stu-id="7b80f-134">Document order</span></span>|  
|<span data-ttu-id="7b80f-135">XContainer.NodesBeforeSelf</span><span class="sxs-lookup"><span data-stu-id="7b80f-135">XContainer.NodesBeforeSelf</span></span>|<span data-ttu-id="7b80f-136">Порядок документа</span><span class="sxs-lookup"><span data-stu-id="7b80f-136">Document order</span></span>|  
|<span data-ttu-id="7b80f-137">XElement.AncestorsAndSelf</span><span class="sxs-lookup"><span data-stu-id="7b80f-137">XElement.AncestorsAndSelf</span></span>|<span data-ttu-id="7b80f-138">Обратный порядок документа</span><span class="sxs-lookup"><span data-stu-id="7b80f-138">Reverse document order</span></span>|  
|<span data-ttu-id="7b80f-139">XElement.Attributes</span><span class="sxs-lookup"><span data-stu-id="7b80f-139">XElement.Attributes</span></span>|<span data-ttu-id="7b80f-140">Порядок документа</span><span class="sxs-lookup"><span data-stu-id="7b80f-140">Document order</span></span>|  
|<span data-ttu-id="7b80f-141">XElement.DescendantNodesAndSelf</span><span class="sxs-lookup"><span data-stu-id="7b80f-141">XElement.DescendantNodesAndSelf</span></span>|<span data-ttu-id="7b80f-142">Порядок документа</span><span class="sxs-lookup"><span data-stu-id="7b80f-142">Document order</span></span>|  
|<span data-ttu-id="7b80f-143">XElement.DescendantsAndSelf</span><span class="sxs-lookup"><span data-stu-id="7b80f-143">XElement.DescendantsAndSelf</span></span>|<span data-ttu-id="7b80f-144">Порядок документа</span><span class="sxs-lookup"><span data-stu-id="7b80f-144">Document order</span></span>|  
|<span data-ttu-id="7b80f-145">XNode.Ancestors</span><span class="sxs-lookup"><span data-stu-id="7b80f-145">XNode.Ancestors</span></span>|<span data-ttu-id="7b80f-146">Обратный порядок документа</span><span class="sxs-lookup"><span data-stu-id="7b80f-146">Reverse document order</span></span>|  
|<span data-ttu-id="7b80f-147">XNode.ElementsAfterSelf</span><span class="sxs-lookup"><span data-stu-id="7b80f-147">XNode.ElementsAfterSelf</span></span>|<span data-ttu-id="7b80f-148">Порядок документа</span><span class="sxs-lookup"><span data-stu-id="7b80f-148">Document order</span></span>|  
|<span data-ttu-id="7b80f-149">XNode.ElementsBeforeSelf</span><span class="sxs-lookup"><span data-stu-id="7b80f-149">XNode.ElementsBeforeSelf</span></span>|<span data-ttu-id="7b80f-150">Порядок документа</span><span class="sxs-lookup"><span data-stu-id="7b80f-150">Document order</span></span>|  
|<span data-ttu-id="7b80f-151">XNode.NodesAfterSelf</span><span class="sxs-lookup"><span data-stu-id="7b80f-151">XNode.NodesAfterSelf</span></span>|<span data-ttu-id="7b80f-152">Порядок документа</span><span class="sxs-lookup"><span data-stu-id="7b80f-152">Document order</span></span>|  
|<span data-ttu-id="7b80f-153">XNode.NodesBeforeSelf</span><span class="sxs-lookup"><span data-stu-id="7b80f-153">XNode.NodesBeforeSelf</span></span>|<span data-ttu-id="7b80f-154">Порядок документа</span><span class="sxs-lookup"><span data-stu-id="7b80f-154">Document order</span></span>|  
  
## <a name="positional-predicates"></a><span data-ttu-id="7b80f-155">Позиционные предикаты</span><span class="sxs-lookup"><span data-stu-id="7b80f-155">Positional Predicates</span></span>  
 <span data-ttu-id="7b80f-156">В выражении XPath позиционные предикаты представляются с учетом порядка расположения в документе для многих осей, однако они располагаются в порядке, обратном по отношению к документу, для обратных осей, а именно `preceding`, `preceding-sibling`, `ancestor` и `ancestor-or-self`.</span><span class="sxs-lookup"><span data-stu-id="7b80f-156">Within an XPath expression, positional predicates are expressed in terms of document order for many axes, but are expressed in reverse document order for reverse axes, which are `preceding`, `preceding-sibling`, `ancestor`, and `ancestor-or-self`.</span></span> <span data-ttu-id="7b80f-157">Например, выражение XPath `preceding-sibling::*[1]` возвращает ближайший предшествующий одноуровневый элемент.</span><span class="sxs-lookup"><span data-stu-id="7b80f-157">For example, the XPath expression `preceding-sibling::*[1]` returns the immediately preceding sibling.</span></span> <span data-ttu-id="7b80f-158">Так происходит даже несмотря на то, что итоговый результирующий набор представляется в порядке документа.</span><span class="sxs-lookup"><span data-stu-id="7b80f-158">This is the case even though the final result set is presented in document order.</span></span>  
  
 <span data-ttu-id="7b80f-159">В отличие от этого все позиционные предикаты в LINQ to XML всегда выражаются в порядке оси.</span><span class="sxs-lookup"><span data-stu-id="7b80f-159">By contrast, all positional predicates in LINQ to XML are always expressed in terms of the order of the axis.</span></span> <span data-ttu-id="7b80f-160">Например, `anElement.ElementsBeforeSelf().ToList()[0]` возвращает первый дочерний элемент родителя запрашиваемого элемента, а не ближайший предшествующий одноуровневый элемент.</span><span class="sxs-lookup"><span data-stu-id="7b80f-160">For example, `anElement.ElementsBeforeSelf().ToList()[0]` returns the first child element of the parent of the queried element, not the immediate preceding sibling.</span></span> <span data-ttu-id="7b80f-161">Другой пример: `anElement.Ancestors().ToList()[0]` возвращает родительский элемент.</span><span class="sxs-lookup"><span data-stu-id="7b80f-161">Another example: `anElement.Ancestors().ToList()[0]` returns the parent element.</span></span>  
  
 <span data-ttu-id="7b80f-162">Отметим, что при описанном выше подходе материализуется вся коллекция.</span><span class="sxs-lookup"><span data-stu-id="7b80f-162">Note that the above approach materializes the entire collection.</span></span> <span data-ttu-id="7b80f-163">Это не самый эффективный способ написания такого запроса.</span><span class="sxs-lookup"><span data-stu-id="7b80f-163">This is not the most efficient way to write that query.</span></span> <span data-ttu-id="7b80f-164">Запрос был написан так в целях демонстрации поведения позиционных предикатов.</span><span class="sxs-lookup"><span data-stu-id="7b80f-164">It was written in that way to demonstrate the behavior of positional predicates.</span></span> <span data-ttu-id="7b80f-165">Более подходящим способом написания этого же запроса является использование <xref:System.Linq.Enumerable.First%2A>метод следующим образом: `anElement.ElementsBeforeSelf().First()`.</xref:System.Linq.Enumerable.First%2A></span><span class="sxs-lookup"><span data-stu-id="7b80f-165">A more appropriate way to write the same query is to use the <xref:System.Linq.Enumerable.First%2A> method, as follows: `anElement.ElementsBeforeSelf().First()`.</span></span>  
  
 <span data-ttu-id="7b80f-166">Если бы потребовалось найти ближайший предшествующий элемент в [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)], то было бы написано следующее выражение:</span><span class="sxs-lookup"><span data-stu-id="7b80f-166">If you wanted to find the immediately preceding element in [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)], you would write the following expression:</span></span>  
  
 `ElementsBeforeSelf().Last()`  
  
## <a name="performance-differences"></a><span data-ttu-id="7b80f-167">Различия в производительности</span><span class="sxs-lookup"><span data-stu-id="7b80f-167">Performance Differences</span></span>  
 <span data-ttu-id="7b80f-168">Запросы XPath, которые используют функциональность XPath в [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] будет работать так же как [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] запросов.</span><span class="sxs-lookup"><span data-stu-id="7b80f-168">XPath queries that use the XPath functionality in [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] will not perform as well as [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] queries.</span></span>  
  
## <a name="comparison-of-composition"></a><span data-ttu-id="7b80f-169">Сравнение композиций</span><span class="sxs-lookup"><span data-stu-id="7b80f-169">Comparison of Composition</span></span>  
 <span data-ttu-id="7b80f-170">Композиция запроса [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] немного напоминает композицию выражения XPath, хотя по синтаксису они совершенно различны.</span><span class="sxs-lookup"><span data-stu-id="7b80f-170">Composition of a [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] query is somewhat parallel to composition of an XPath expression, although very different in syntax.</span></span>  
  
 <span data-ttu-id="7b80f-171">Например, если в переменной с именем `customers` имеется элемент и требуется найти внучатый элемент с именем `CompanyName` во всех дочерних элементах с именем `Customer`, то нужно написать следующее выражение XPath:</span><span class="sxs-lookup"><span data-stu-id="7b80f-171">For example, if you have an element in a variable named `customers`, and you want to find a grandchild element named `CompanyName` under all child elements named `Customer`, you would write an XPath expression as follows:</span></span>  
  
```vb  
customers.XPathSelectElements("./Customer/CompanyName")  
```  
  
 <span data-ttu-id="7b80f-172">Эквивалентное выражение [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] таково:</span><span class="sxs-lookup"><span data-stu-id="7b80f-172">The equivalent [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] query is:</span></span>  
  
```vb  
customers.Element("Customer").Elements("CompanyName")  
```  
  
 <span data-ttu-id="7b80f-173">Существуют похожие аналоги для каждой оси XPath.</span><span class="sxs-lookup"><span data-stu-id="7b80f-173">There are similar parallels for each of the XPath axes.</span></span>  
  
|<span data-ttu-id="7b80f-174">Ось XPath</span><span class="sxs-lookup"><span data-stu-id="7b80f-174">XPath axis</span></span>|<span data-ttu-id="7b80f-175">Ось LINQ to XML</span><span class="sxs-lookup"><span data-stu-id="7b80f-175">LINQ to XML axis</span></span>|  
|----------------|----------------------|  
|<span data-ttu-id="7b80f-176">дочерняя (ось по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="7b80f-176">child (the default axis)</span></span>|<span data-ttu-id="7b80f-177"><xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=fullName></xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=fullName></span><span class="sxs-lookup"><span data-stu-id="7b80f-177"><xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=fullName></span></span>|  
|<span data-ttu-id="7b80f-178">родительская (...)</span><span class="sxs-lookup"><span data-stu-id="7b80f-178">Parent (..)</span></span>|<span data-ttu-id="7b80f-179"><xref:System.Xml.Linq.XObject.Parent%2A?displayProperty=fullName></xref:System.Xml.Linq.XObject.Parent%2A?displayProperty=fullName></span><span class="sxs-lookup"><span data-stu-id="7b80f-179"><xref:System.Xml.Linq.XObject.Parent%2A?displayProperty=fullName></span></span>|  
|<span data-ttu-id="7b80f-180">ось атрибутов (@)</span><span class="sxs-lookup"><span data-stu-id="7b80f-180">attribute axis (@)</span></span>|<span data-ttu-id="7b80f-181"><xref:System.Xml.Linq.XElement.Attribute%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.Attribute%2A?displayProperty=fullName></span><span class="sxs-lookup"><span data-stu-id="7b80f-181"><xref:System.Xml.Linq.XElement.Attribute%2A?displayProperty=fullName></span></span><br /><br /> <span data-ttu-id="7b80f-182">или</span><span class="sxs-lookup"><span data-stu-id="7b80f-182">or</span></span><br /><br /> <span data-ttu-id="7b80f-183"><xref:System.Xml.Linq.XElement.Attributes%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.Attributes%2A?displayProperty=fullName></span><span class="sxs-lookup"><span data-stu-id="7b80f-183"><xref:System.Xml.Linq.XElement.Attributes%2A?displayProperty=fullName></span></span>|  
|<span data-ttu-id="7b80f-184">ось ancestor</span><span class="sxs-lookup"><span data-stu-id="7b80f-184">ancestor axis</span></span>|<span data-ttu-id="7b80f-185"><xref:System.Xml.Linq.XNode.Ancestors%2A?displayProperty=fullName></xref:System.Xml.Linq.XNode.Ancestors%2A?displayProperty=fullName></span><span class="sxs-lookup"><span data-stu-id="7b80f-185"><xref:System.Xml.Linq.XNode.Ancestors%2A?displayProperty=fullName></span></span>|  
|<span data-ttu-id="7b80f-186">ось ancestor-or-self</span><span class="sxs-lookup"><span data-stu-id="7b80f-186">ancestor-or-self axis</span></span>|<span data-ttu-id="7b80f-187"><xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A?displayProperty=fullName></span><span class="sxs-lookup"><span data-stu-id="7b80f-187"><xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A?displayProperty=fullName></span></span>|  
|<span data-ttu-id="7b80f-188">дочерняя ось (//)</span><span class="sxs-lookup"><span data-stu-id="7b80f-188">descendant axis (//)</span></span>|<span data-ttu-id="7b80f-189"><xref:System.Xml.Linq.XContainer.Descendants%2A?displayProperty=fullName></xref:System.Xml.Linq.XContainer.Descendants%2A?displayProperty=fullName></span><span class="sxs-lookup"><span data-stu-id="7b80f-189"><xref:System.Xml.Linq.XContainer.Descendants%2A?displayProperty=fullName></span></span><br /><br /> <span data-ttu-id="7b80f-190">или</span><span class="sxs-lookup"><span data-stu-id="7b80f-190">or</span></span><br /><br /> <span data-ttu-id="7b80f-191"><xref:System.Xml.Linq.XContainer.DescendantNodes%2A?displayProperty=fullName></xref:System.Xml.Linq.XContainer.DescendantNodes%2A?displayProperty=fullName></span><span class="sxs-lookup"><span data-stu-id="7b80f-191"><xref:System.Xml.Linq.XContainer.DescendantNodes%2A?displayProperty=fullName></span></span>|  
|<span data-ttu-id="7b80f-192">descendant-or-self</span><span class="sxs-lookup"><span data-stu-id="7b80f-192">descendant-or-self</span></span>|<span data-ttu-id="7b80f-193"><xref:System.Xml.Linq.XElement.DescendantsAndSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.DescendantsAndSelf%2A?displayProperty=fullName></span><span class="sxs-lookup"><span data-stu-id="7b80f-193"><xref:System.Xml.Linq.XElement.DescendantsAndSelf%2A?displayProperty=fullName></span></span><br /><br /> <span data-ttu-id="7b80f-194">или</span><span class="sxs-lookup"><span data-stu-id="7b80f-194">or</span></span><br /><br /> <span data-ttu-id="7b80f-195"><xref:System.Xml.Linq.XElement.DescendantNodesAndSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.DescendantNodesAndSelf%2A?displayProperty=fullName></span><span class="sxs-lookup"><span data-stu-id="7b80f-195"><xref:System.Xml.Linq.XElement.DescendantNodesAndSelf%2A?displayProperty=fullName></span></span>|  
|<span data-ttu-id="7b80f-196">following-sibling</span><span class="sxs-lookup"><span data-stu-id="7b80f-196">following-sibling</span></span>|<span data-ttu-id="7b80f-197"><xref:System.Xml.Linq.XNode.ElementsAfterSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XNode.ElementsAfterSelf%2A?displayProperty=fullName></span><span class="sxs-lookup"><span data-stu-id="7b80f-197"><xref:System.Xml.Linq.XNode.ElementsAfterSelf%2A?displayProperty=fullName></span></span><br /><br /> <span data-ttu-id="7b80f-198">или</span><span class="sxs-lookup"><span data-stu-id="7b80f-198">or</span></span><br /><br /> <span data-ttu-id="7b80f-199"><xref:System.Xml.Linq.XNode.NodesAfterSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XNode.NodesAfterSelf%2A?displayProperty=fullName></span><span class="sxs-lookup"><span data-stu-id="7b80f-199"><xref:System.Xml.Linq.XNode.NodesAfterSelf%2A?displayProperty=fullName></span></span>|  
|<span data-ttu-id="7b80f-200">preceding-sibling</span><span class="sxs-lookup"><span data-stu-id="7b80f-200">preceding-sibling</span></span>|<span data-ttu-id="7b80f-201"><xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=fullName></span><span class="sxs-lookup"><span data-stu-id="7b80f-201"><xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=fullName></span></span><br /><br /> <span data-ttu-id="7b80f-202">или</span><span class="sxs-lookup"><span data-stu-id="7b80f-202">or</span></span><br /><br /> <span data-ttu-id="7b80f-203"><xref:System.Xml.Linq.XNode.NodesBeforeSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XNode.NodesBeforeSelf%2A?displayProperty=fullName></span><span class="sxs-lookup"><span data-stu-id="7b80f-203"><xref:System.Xml.Linq.XNode.NodesBeforeSelf%2A?displayProperty=fullName></span></span>|  
|<span data-ttu-id="7b80f-204">following</span><span class="sxs-lookup"><span data-stu-id="7b80f-204">following</span></span>|<span data-ttu-id="7b80f-205">Непосредственного эквивалента нет.</span><span class="sxs-lookup"><span data-stu-id="7b80f-205">No direct equivalent.</span></span>|  
|<span data-ttu-id="7b80f-206">preceding</span><span class="sxs-lookup"><span data-stu-id="7b80f-206">preceding</span></span>|<span data-ttu-id="7b80f-207">Непосредственного эквивалента нет.</span><span class="sxs-lookup"><span data-stu-id="7b80f-207">No direct equivalent.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="7b80f-208">См. также</span><span class="sxs-lookup"><span data-stu-id="7b80f-208">See Also</span></span>  
 [<span data-ttu-id="7b80f-209">LINQ to XML для пользователей XPath (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="7b80f-209">LINQ to XML for XPath Users (Visual Basic)</span></span>](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-for-xpath-users.md)