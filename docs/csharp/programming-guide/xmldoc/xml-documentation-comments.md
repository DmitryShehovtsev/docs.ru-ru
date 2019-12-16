---
title: "Комментарии к XML-документации (Руководство по программированию на C#)"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- cs.xml
dev_langs:
- CSharp
helpviewer_keywords:
- XML [C#], code comments
- comments [C#], XML
- documentation comments [C#]
- C# source code files
- C# language, XML code comments
- XML documentation comments [C#]
ms.assetid: 803b7f7b-7428-4725-b5db-9a6cff273199
caps.latest.revision: 26
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 408b2de29b15158499067da05dbb2f89eb1ba22f
ms.contentlocale: ru-ru
ms.lasthandoff: 07/28/2017

---
# <a name="xml-documentation-comments-c-programming-guide"></a><span data-ttu-id="a8be5-102">Комментарии к XML-документации (Руководство по программированию на C#)</span><span class="sxs-lookup"><span data-stu-id="a8be5-102">XML Documentation Comments (C# Programming Guide)</span></span>
<span data-ttu-id="a8be5-103">В Visual C# можно создавать документацию для кода путем включения XML-элементов в специальные поля комментариев (начинающиеся с трех символов косой черты) в исходном коде непосредственно перед блоком кода, к которому относятся комментарии. Например:</span><span class="sxs-lookup"><span data-stu-id="a8be5-103">In Visual C# you can create documentation for your code by including XML elements in special comment fields (indicated by triple slashes) in the source code directly before the code block to which the comments refer, for example:</span></span>  
  
```  
/// <summary>  
///  This class performs an important function.  
/// </summary>  
public class MyClass{}  
```  
  
 <span data-ttu-id="a8be5-104">При выполнении компиляции с параметром [/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) компилятор осуществляет поиск всех тегов XML в исходном коде и создает XML-файл документации.</span><span class="sxs-lookup"><span data-stu-id="a8be5-104">When you compile with the [/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) option, the compiler will search for all XML tags in the source code and create an XML documentation file.</span></span> <span data-ttu-id="a8be5-105">Для получения окончательной документации на основе созданного компилятором файла можно создать пользовательский инструмент или использовать инструмент [Sandcastle](https://github.com/EWSoftware/SHFB).</span><span class="sxs-lookup"><span data-stu-id="a8be5-105">To create the final documentation based on the compiler-generated file, you can create a custom tool or use a tool such as [Sandcastle](https://github.com/EWSoftware/SHFB).</span></span>  
  
 <span data-ttu-id="a8be5-106">Для ссылки на XML-элементы (например, если функция обрабатывает определенные XML-элементы, которые требуется включить в комментарии XML-документации) можно использовать стандартный механизм заключения в скобки (`<` и `>`).</span><span class="sxs-lookup"><span data-stu-id="a8be5-106">To refer to XML elements (for example, your function processes specific XML elements that you want to describe in an XML documentation comment), you can use the standard quoting mechanism (`<` and `>`).</span></span>  <span data-ttu-id="a8be5-107">Для ссылки на универсальные идентификаторы в элементах ссылок кода (`cref`) можно использовать escape-символы (например, `cref="List<T>"`) или фигурные скобки (`cref="List{T}"`).</span><span class="sxs-lookup"><span data-stu-id="a8be5-107">To refer to generic identifiers in code reference (`cref`) elements, you can use either the escape characters (for example, `cref="List<T>"`) or braces (`cref="List{T}"`).</span></span>  <span data-ttu-id="a8be5-108">В особом случае компилятор анализирует фигурные скобки, как угловые, чтобы при ссылке на универсальные идентификаторы сделать комментарий документации менее громоздким.</span><span class="sxs-lookup"><span data-stu-id="a8be5-108">As a special case, the compiler parses the braces as angle brackets to make the documentation comment less cumbersome to author when referring to generic identifiers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="a8be5-109">Комментарии XML-документации не являются метаданными. Они не включаются в скомпилированную сборку, и поэтому не доступны посредством отражения.</span><span class="sxs-lookup"><span data-stu-id="a8be5-109">The XML documentation comments are not metadata; they are not included in the compiled assembly and therefore they are not accessible through reflection.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="a8be5-110">Содержание</span><span class="sxs-lookup"><span data-stu-id="a8be5-110">In This Section</span></span>  
  
-   [<span data-ttu-id="a8be5-111">Рекомендуемые теги для комментариев документации</span><span class="sxs-lookup"><span data-stu-id="a8be5-111">Recommended Tags for Documentation Comments</span></span>](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)  
  
-   [<span data-ttu-id="a8be5-112">Обработка XML-файла</span><span class="sxs-lookup"><span data-stu-id="a8be5-112">Processing the XML File</span></span>](../../../csharp/programming-guide/xmldoc/processing-the-xml-file.md)  
  
-   [<span data-ttu-id="a8be5-113">Разделители для тегов документации</span><span class="sxs-lookup"><span data-stu-id="a8be5-113">Delimiters for Documentation Tags</span></span>](../../../csharp/programming-guide/xmldoc/delimiters-for-documentation-tags.md)  
  
-   [<span data-ttu-id="a8be5-114">Практическое руководство. Использование XML-документации</span><span class="sxs-lookup"><span data-stu-id="a8be5-114">How to: Use the XML Documentation Features</span></span>](../../../csharp/programming-guide/xmldoc/how-to-use-the-xml-documentation-features.md)  
  
## <a name="related-sections"></a><span data-ttu-id="a8be5-115">Связанные разделы</span><span class="sxs-lookup"><span data-stu-id="a8be5-115">Related Sections</span></span>  
 <span data-ttu-id="a8be5-116">Дополнительные сведения:</span><span class="sxs-lookup"><span data-stu-id="a8be5-116">For more information, see:</span></span>  
  
-   [<span data-ttu-id="a8be5-117">/doc (обработка комментариев документации)</span><span class="sxs-lookup"><span data-stu-id="a8be5-117">/doc (Process Documentation Comments)</span></span>](../../../csharp/language-reference/compiler-options/doc-compiler-option.md)  
  
## <a name="c-language-specification"></a><span data-ttu-id="a8be5-118">Спецификация языка C#</span><span class="sxs-lookup"><span data-stu-id="a8be5-118">C# Language Specification</span></span>  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a><span data-ttu-id="a8be5-119">См. также</span><span class="sxs-lookup"><span data-stu-id="a8be5-119">See Also</span></span>  
 [<span data-ttu-id="a8be5-120">Руководство по программированию на C#</span><span class="sxs-lookup"><span data-stu-id="a8be5-120">C# Programming Guide</span></span>](../../../csharp/programming-guide/index.md)
