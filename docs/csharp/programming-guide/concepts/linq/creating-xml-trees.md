---
title: "Создание деревьев XML (C#)"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: bccc3e0a-c08c-468e-9d30-e075670fdace
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 99b197b86096b803b9732ab2546b23ff59e3e2fe
ms.contentlocale: ru-ru
ms.lasthandoff: 07/28/2017

---
# <a name="creating-xml-trees-c"></a><span data-ttu-id="9e732-102">Создание деревьев XML (C#)</span><span class="sxs-lookup"><span data-stu-id="9e732-102">Creating XML Trees (C#)</span></span>
<span data-ttu-id="9e732-103">Одна из самых распространенных задач при работе с XML состоит в построении XML-дерева.</span><span class="sxs-lookup"><span data-stu-id="9e732-103">One of the most common XML tasks is constructing an XML tree.</span></span> <span data-ttu-id="9e732-104">В этом разделе описывается несколько способов создания таких деревьев.</span><span class="sxs-lookup"><span data-stu-id="9e732-104">This section describes several ways to create them.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="9e732-105">Содержание</span><span class="sxs-lookup"><span data-stu-id="9e732-105">In This Section</span></span>  
  
|<span data-ttu-id="9e732-106">Раздел</span><span class="sxs-lookup"><span data-stu-id="9e732-106">Topic</span></span>|<span data-ttu-id="9e732-107">Описание</span><span class="sxs-lookup"><span data-stu-id="9e732-107">Description</span></span>|  
|-----------|-----------------|  
|[<span data-ttu-id="9e732-108">Функциональное построение (LINQ to XML) (C#)</span><span class="sxs-lookup"><span data-stu-id="9e732-108">Functional Construction (LINQ to XML) (C#)</span></span>](../../../../csharp/programming-guide/concepts/linq/functional-construction-linq-to-xml.md)|<span data-ttu-id="9e732-109">Содержит общие сведения о функциональном построении в [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)].</span><span class="sxs-lookup"><span data-stu-id="9e732-109">Provides an overview of functional construction in [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)].</span></span> <span data-ttu-id="9e732-110">Функциональное построение позволяет создавать все XML-дерево или его часть с помощью одной инструкции.</span><span class="sxs-lookup"><span data-stu-id="9e732-110">Functional construction enables you to create all or part of your XML tree in a single statement.</span></span> <span data-ttu-id="9e732-111">В этом разделе также показано, как внедрять запросы при построении XML-дерева.</span><span class="sxs-lookup"><span data-stu-id="9e732-111">This topic also shows how to embed queries when constructing an XML tree.</span></span>|  
|[<span data-ttu-id="9e732-112">Создание деревьев XML на языке C# (LINQ to XML)</span><span class="sxs-lookup"><span data-stu-id="9e732-112">Creating XML Trees in C# (LINQ to XML)</span></span>](../../../../csharp/programming-guide/concepts/linq/creating-xml-trees-linq-to-xml-2.md)|<span data-ttu-id="9e732-113">Показывает, как строить деревья на языке C#.</span><span class="sxs-lookup"><span data-stu-id="9e732-113">Shows how to create trees in C#.</span></span>|  
|[<span data-ttu-id="9e732-114">Сравнение клонирования и Присоединение (C#)</span><span class="sxs-lookup"><span data-stu-id="9e732-114">Cloning vs. Attaching (C#)</span></span>](../../../../csharp/programming-guide/concepts/linq/cloning-vs-attaching.md)|<span data-ttu-id="9e732-115">Иллюстрирует различие между добавлением узлов из существующего XML-дерева (узлы клонируются и затем добавляются) и добавлением узлов, не имеющих родителя (такие узлы просто присоединяются).</span><span class="sxs-lookup"><span data-stu-id="9e732-115">Demonstrates the difference between adding nodes from an existing XML tree (nodes are cloned and then added) and adding nodes with no parent (they are simply attached).</span></span>|  
|[<span data-ttu-id="9e732-116">Анализ XML (C#)</span><span class="sxs-lookup"><span data-stu-id="9e732-116">Parsing XML (C#)</span></span>](../../../../csharp/programming-guide/concepts/linq/parsing-xml.md)|<span data-ttu-id="9e732-117">Показывает, как выполнить синтаксический анализ XML из множества источников.</span><span class="sxs-lookup"><span data-stu-id="9e732-117">Shows how to parse XML from a variety of sources.</span></span> [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]<span data-ttu-id="9e732-118"> работает уровнем выше <xref:System.Xml.XmlReader>, который используется для анализа кода XML.</span><span class="sxs-lookup"><span data-stu-id="9e732-118"> is layered on top of <xref:System.Xml.XmlReader>, which is used to parse the XML.</span></span>|  
|[<span data-ttu-id="9e732-119">Практическое руководство. Заполнение дерева XML с помощью XmlWriter (LINQ to XML) (C#)</span><span class="sxs-lookup"><span data-stu-id="9e732-119">How to: Populate an XML Tree with an XmlWriter (LINQ to XML) (C#)</span></span>](../../../../csharp/programming-guide/concepts/linq/how-to-populate-an-xml-tree-with-an-xmlwriter-linq-to-xml.md)|<span data-ttu-id="9e732-120">Показывает, как заполнять XML-дерево с помощью <xref:System.Xml.XmlWriter>.</span><span class="sxs-lookup"><span data-stu-id="9e732-120">Shows how to populate an XML tree by using an <xref:System.Xml.XmlWriter>.</span></span>|  
|[<span data-ttu-id="9e732-121">Практическое руководство. Проверка с использованием XSD (LINQ to XML) (C#)</span><span class="sxs-lookup"><span data-stu-id="9e732-121">How to: Validate Using XSD (LINQ to XML) (C#)</span></span>](../../../../csharp/programming-guide/concepts/linq/how-to-validate-using-xsd-linq-to-xml.md)|<span data-ttu-id="9e732-122">Показывает, как проверять XML-дерево с помощью XSD.</span><span class="sxs-lookup"><span data-stu-id="9e732-122">Shows how to validate an XML tree using XSD.</span></span>|  
|[<span data-ttu-id="9e732-123">Допустимое содержимое объектов XElement и XDocument</span><span class="sxs-lookup"><span data-stu-id="9e732-123">Valid Content of XElement and XDocument Objects</span></span>](../../../../csharp/programming-guide/concepts/linq/valid-content-of-xelement-and-xdocument-objects3.md)|<span data-ttu-id="9e732-124">Описывает допустимые аргументы, которые можно передавать конструкторам, а также методы, которые можно использовать для добавления содержимого в элементы и документы.</span><span class="sxs-lookup"><span data-stu-id="9e732-124">Describes the valid arguments that can be passed to the constructors and methods that are used to add content to elements and documents.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="9e732-125">См. также</span><span class="sxs-lookup"><span data-stu-id="9e732-125">See Also</span></span>  
 [<span data-ttu-id="9e732-126">Руководство по программированию (LINQ to XML) (C#)</span><span class="sxs-lookup"><span data-stu-id="9e732-126">Programming Guide (LINQ to XML) (C#)</span></span>](../../../../csharp/programming-guide/concepts/linq/programming-guide-linq-to-xml.md)
