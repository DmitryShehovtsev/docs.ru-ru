---
title: "Изменение деревьев XML (LINQ to XML) (C#)"
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
ms.assetid: 8ec47e6d-2363-4694-be46-8d5ca4d15fc9
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 0cb4ff851dbea97f254d5290ce021d560849e3d9
ms.contentlocale: ru-ru
ms.lasthandoff: 07/28/2017

---
# <a name="modifying-xml-trees-linq-to-xml-c"></a><span data-ttu-id="ef51d-102">Изменение деревьев XML (LINQ to XML) (C#)</span><span class="sxs-lookup"><span data-stu-id="ef51d-102">Modifying XML Trees (LINQ to XML) (C#)</span></span>
[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]<span data-ttu-id="ef51d-103"> служит для хранения XML-дерева в памяти.</span><span class="sxs-lookup"><span data-stu-id="ef51d-103"> is an in-memory store for an XML tree.</span></span> <span data-ttu-id="ef51d-104">После загрузки или синтаксического анализа XML-дерева из источника [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] позволяет изменить это дерево, после чего его можно сериализовать, сохранив, например, в файл или отправив на удаленный сервер.</span><span class="sxs-lookup"><span data-stu-id="ef51d-104">After you load or parse an XML tree from a source, [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] lets you modify that tree in place, and then serialize the tree, perhaps saving it to a file or sending it to a remote server.</span></span>  
  
 <span data-ttu-id="ef51d-105">При изменении дерева на месте используются такие методы, как <xref:System.Xml.Linq.XContainer.Add%2A>.</span><span class="sxs-lookup"><span data-stu-id="ef51d-105">When you modify a tree in place, you use certain methods, such as <xref:System.Xml.Linq.XContainer.Add%2A>.</span></span>  
  
 <span data-ttu-id="ef51d-106">Однако существует другой подход, который заключается в использовании функционального построения для создания нового дерева другой формы.</span><span class="sxs-lookup"><span data-stu-id="ef51d-106">However, there is another approach, which is to use functional construction to generate a new tree with a different shape.</span></span> <span data-ttu-id="ef51d-107">В зависимости от типов изменений, которые необходимо внести в XML-дерево, а также в зависимости от размера самого дерева, этот подход может быть более надежным и простым для разработки.</span><span class="sxs-lookup"><span data-stu-id="ef51d-107">Depending on the types of changes that you need to make to your XML tree, and depending on the size of the tree, this approach can be more robust and easier to develop.</span></span> <span data-ttu-id="ef51d-108">В первом разделе этой части приведено сравнение обоих подходов.</span><span class="sxs-lookup"><span data-stu-id="ef51d-108">The first topic in this section compares these two approaches.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="ef51d-109">Содержание</span><span class="sxs-lookup"><span data-stu-id="ef51d-109">In This Section</span></span>  
  
|<span data-ttu-id="ef51d-110">Раздел</span><span class="sxs-lookup"><span data-stu-id="ef51d-110">Topic</span></span>|<span data-ttu-id="ef51d-111">Описание</span><span class="sxs-lookup"><span data-stu-id="ef51d-111">Description</span></span>|  
|-----------|-----------------|  
|[<span data-ttu-id="ef51d-112">Сравнение изменения дерева XML в памяти с функциональной сборкой (LINQ to XML) (C#)</span><span class="sxs-lookup"><span data-stu-id="ef51d-112">In-Memory XML Tree Modification vs. Functional Construction (LINQ to XML) (C#)</span></span>](../../../../csharp/programming-guide/concepts/linq/in-memory-xml-tree-modification-vs-functional-construction-linq-to-xml.md)|<span data-ttu-id="ef51d-113">Сравниваются изменение XML-дерева в памяти и функциональное построение.</span><span class="sxs-lookup"><span data-stu-id="ef51d-113">Compares modifying an XML tree in memory to functional construction.</span></span>|  
|[<span data-ttu-id="ef51d-114">Добавление элементов, атрибутов и узлов в дерево XML (C#)</span><span class="sxs-lookup"><span data-stu-id="ef51d-114">Adding Elements, Attributes, and Nodes to an XML Tree (C#)</span></span>](../../../../csharp/programming-guide/concepts/linq/adding-elements-attributes-and-nodes-to-an-xml-tree.md)|<span data-ttu-id="ef51d-115">Приводятся сведения о добавлении элементов, атрибутов или узлов к XML-дереву.</span><span class="sxs-lookup"><span data-stu-id="ef51d-115">Provides information about adding elements, attributes, or nodes to an XML tree.</span></span>|  
|[<span data-ttu-id="ef51d-116">Изменение элементов, атрибутов и узлов в дереве XML</span><span class="sxs-lookup"><span data-stu-id="ef51d-116">Modifying Elements, Attributes, and Nodes in an XML Tree</span></span>](../../../../csharp/programming-guide/concepts/linq/modifying-elements-attributes-and-nodes-in-an-xml-tree.md)|<span data-ttu-id="ef51d-117">Приводятся сведения о добавлении существующих элементов, атрибутов или узлов.</span><span class="sxs-lookup"><span data-stu-id="ef51d-117">Provides information about modifying existing elements, attributes, or nodes.</span></span>|  
|[<span data-ttu-id="ef51d-118">Удаление элементов, атрибутов и узлов из дерева XML (C#)</span><span class="sxs-lookup"><span data-stu-id="ef51d-118">Removing Elements, Attributes, and Nodes from an XML Tree (C#)</span></span>](../../../../csharp/programming-guide/concepts/linq/removing-elements-attributes-and-nodes-from-an-xml-tree.md)|<span data-ttu-id="ef51d-119">Приводятся сведения об удалении элементов, атрибутов или узлов из XML-дерева.</span><span class="sxs-lookup"><span data-stu-id="ef51d-119">Provides information about removing elements, attributes, or nodes from the XML tree.</span></span>|  
|[<span data-ttu-id="ef51d-120">Обслуживание пар "имя-значение" (C#)</span><span class="sxs-lookup"><span data-stu-id="ef51d-120">Maintaining Name/Value Pairs (C#)</span></span>](../../../../csharp/programming-guide/concepts/linq/maintaining-name-value-pairs.md)|<span data-ttu-id="ef51d-121">Приводится описание того, как следует поддерживать сведения о приложении, которые лучше всего хранятся в парах «имя-значение», например сведения о настройках или глобальные настройки.</span><span class="sxs-lookup"><span data-stu-id="ef51d-121">Describes how to maintain application information that is best kept as name/value pairs, such as configuration information or global settings.</span></span>|  
|[<span data-ttu-id="ef51d-122">Практическое руководство. Изменение пространства имен для всего дерева XML (C#)</span><span class="sxs-lookup"><span data-stu-id="ef51d-122">How to: Change the Namespace for an Entire XML Tree (C#)</span></span>](../../../../csharp/programming-guide/concepts/linq/how-to-change-the-namespace-for-an-entire-xml-tree.md)|<span data-ttu-id="ef51d-123">Показывается, как переместить XML-дерево из одного пространства имен в другое.</span><span class="sxs-lookup"><span data-stu-id="ef51d-123">Shows how to move an XML tree from one namespace into another.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="ef51d-124">См. также</span><span class="sxs-lookup"><span data-stu-id="ef51d-124">See Also</span></span>  
 [<span data-ttu-id="ef51d-125">Руководство по программированию (LINQ to XML) (C#)</span><span class="sxs-lookup"><span data-stu-id="ef51d-125">Programming Guide (LINQ to XML) (C#)</span></span>](../../../../csharp/programming-guide/concepts/linq/programming-guide-linq-to-xml.md)
