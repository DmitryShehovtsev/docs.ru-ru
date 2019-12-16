---
title: "Параметры и возвращаемые значения для многопоточных процедур (Visual Basic) | Документы Microsoft"
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
ms.assetid: cbdce172-7ff6-41a9-bb21-53a7c6f538a5
caps.latest.revision: 4
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 6d1eb53454b6e0d964be15df2e320ce189e7d875
ms.contentlocale: ru-ru
ms.lasthandoff: 04/12/2017

---
# <a name="parameters-and-return-values-for-multithreaded-procedures-visual-basic"></a><span data-ttu-id="a3265-102">Параметры и возвращаемые значения для многопоточных процедур (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="a3265-102">Parameters and Return Values for Multithreaded Procedures (Visual Basic)</span></span>
<span data-ttu-id="a3265-103">Предоставление и возврат значений в многопоточных приложениях является сложной, так как конструктор для класса поток должен быть передан ссылку на процедуру, которая не принимает аргументов и не возвращает значений.</span><span class="sxs-lookup"><span data-stu-id="a3265-103">Supplying and returning values in a multithreaded application is complicated because the constructor for the thread class must be passed a reference to a procedure that takes no arguments and returns no value.</span></span> <span data-ttu-id="a3265-104">В следующих разделах показаны некоторые простые способы передачи параметров и возвращаемых значений из процедур в отдельных потоках.</span><span class="sxs-lookup"><span data-stu-id="a3265-104">The following sections show some simple ways to supply parameters and return values from procedures on separate threads.</span></span>  
  
## <a name="supplying-parameters-for-multithreaded-procedures"></a><span data-ttu-id="a3265-105">Предоставление параметров для многопоточных процедур</span><span class="sxs-lookup"><span data-stu-id="a3265-105">Supplying Parameters for Multithreaded Procedures</span></span>  
 <span data-ttu-id="a3265-106">Лучший способ передачи параметров при вызове многопотокового метода является заключение нужного метода в класс и определение полей для этого класса, который будет использоваться в качестве параметров для нового потока.</span><span class="sxs-lookup"><span data-stu-id="a3265-106">The best way to supply parameters for a multithreaded method call is to wrap the target method in a class and define fields for that class that will serve as parameters for the new thread.</span></span> <span data-ttu-id="a3265-107">Преимуществом этого подхода является то, что новый экземпляр класса, позволяет создавать со своими параметрами нужно запустить новый поток каждый раз.</span><span class="sxs-lookup"><span data-stu-id="a3265-107">The advantage of this approach is that you can create a new instance of the class, with its own parameters, every time you want to start a new thread.</span></span> <span data-ttu-id="a3265-108">Например рассмотрим функцию, вычисляющую площадь треугольника, как показано в следующем коде:</span><span class="sxs-lookup"><span data-stu-id="a3265-108">For example, suppose you have a function that calculates the area of a triangle, as in the following code:</span></span>  
  
```vb  
Function CalcArea(ByVal Base As Double, ByVal Height As Double) As Double  
    CalcArea = 0.5 * Base * Height  
End Function  
```  
  
 <span data-ttu-id="a3265-109">Можно написать класс-оболочку `CalcArea` и имеет поля для хранения входных параметров, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="a3265-109">You can write a class that wraps the `CalcArea` function and creates fields to store input parameters, as follows:</span></span>  
  
```vb  
Class AreaClass  
    Public Base As Double  
    Public Height As Double  
    Public Area As Double  
    Sub CalcArea()  
        Area = 0.5 * Base * Height  
        MessageBox.Show("The area is: " & Area.ToString)  
    End Sub  
End Class  
```  
  
 <span data-ttu-id="a3265-110">Для использования `AreaClass`, можно создать `AreaClass` и установить `Base` и `Height` свойства, как показано в следующем коде:</span><span class="sxs-lookup"><span data-stu-id="a3265-110">To use the `AreaClass`, you can create an `AreaClass` object, and set the `Base` and `Height` properties as shown in the following code:</span></span>  
  
```vb  
Protected Sub TestArea()  
    Dim AreaObject As New AreaClass  
    Dim Thread As New System.Threading.Thread(  
                        AddressOf AreaObject.CalcArea)  
    AreaObject.Base = 30  
    AreaObject.Height = 40  
    Thread.Start()  
End Sub  
```  
  
 <span data-ttu-id="a3265-111">Обратите внимание, что `TestArea` не проверяет значение `Area` после вызова `CalcArea` метод.</span><span class="sxs-lookup"><span data-stu-id="a3265-111">Notice that the `TestArea` procedure does not check the value of the `Area` field after calling the `CalcArea` method.</span></span> <span data-ttu-id="a3265-112">Поскольку `CalcArea` выполняется в отдельном потоке, `Area` поле не обязательно быть задано, если проверить его сразу после вызова `Thread.Start`.</span><span class="sxs-lookup"><span data-stu-id="a3265-112">Because `CalcArea` runs on a separate thread, the `Area` field is not guaranteed to be set if you check it immediately after calling `Thread.Start`.</span></span> <span data-ttu-id="a3265-113">В следующем разделе описываются более эффективный способ возвращения значений из многопоточных процедур.</span><span class="sxs-lookup"><span data-stu-id="a3265-113">The next section discusses a better way to return values from multithreaded procedures.</span></span>  
  
## <a name="returning-values-from-multithreaded-procedures"></a><span data-ttu-id="a3265-114">Получение возвращаемых значений от многопоточных процедур</span><span class="sxs-lookup"><span data-stu-id="a3265-114">Returning Values from Multithreaded Procedures</span></span>  
 <span data-ttu-id="a3265-115">Получение возвращаемых значений от процедур, выполняемых в отдельных потоках, осложняется тем, что процедуры не могут быть функциями и нельзя использовать `ByRef` аргументы.</span><span class="sxs-lookup"><span data-stu-id="a3265-115">Returning values from procedures that run on separate threads is complicated by the fact that the procedures cannot be functions and cannot use `ByRef` arguments.</span></span> <span data-ttu-id="a3265-116">Самый простой способ возвращения значений является использование <xref:System.ComponentModel.BackgroundWorker>компонент для управления потоками и вызова события при завершении задачи и обработки результатов с помощью обработчика событий.</xref:System.ComponentModel.BackgroundWorker></span><span class="sxs-lookup"><span data-stu-id="a3265-116">The easiest way to return values is to use the <xref:System.ComponentModel.BackgroundWorker> component to manage your threads and raise an event when the task is done, and process the results with an event handler.</span></span>  
  
 <span data-ttu-id="a3265-117">В следующем примере возвращается значение, при возникновении события от процедуры, выполняющейся в отдельном потоке:</span><span class="sxs-lookup"><span data-stu-id="a3265-117">The following example returns a value by raising an event from a procedure running on a separate thread:</span></span>  
  
```vb  
Private Class AreaClass2  
    Public Base As Double  
    Public Height As Double  
    Function CalcArea() As Double  
        ' Calculate the area of a triangle.  
        Return 0.5 * Base * Height  
    End Function  
End Class  
  
Private WithEvents BackgroundWorker1 As New System.ComponentModel.BackgroundWorker  
  
Private Sub TestArea2()  
    Dim AreaObject2 As New AreaClass2  
    AreaObject2.Base = 30  
    AreaObject2.Height = 40  
  
    ' Start the asynchronous operation.  
    BackgroundWorker1.RunWorkerAsync(AreaObject2)  
End Sub  
  
' This method runs on the background thread when it starts.  
Private Sub BackgroundWorker1_DoWork(  
    ByVal sender As Object,   
    ByVal e As System.ComponentModel.DoWorkEventArgs  
    ) Handles BackgroundWorker1.DoWork  
  
    Dim AreaObject2 As AreaClass2 = CType(e.Argument, AreaClass2)  
    ' Return the value through the Result property.  
    e.Result = AreaObject2.CalcArea()  
End Sub  
  
' This method runs on the main thread when the background thread finishes.  
Private Sub BackgroundWorker1_RunWorkerCompleted(  
    ByVal sender As Object,  
    ByVal e As System.ComponentModel.RunWorkerCompletedEventArgs  
    ) Handles BackgroundWorker1.RunWorkerCompleted  
  
    ' Access the result through the Result property.  
    Dim Area As Double = CDbl(e.Result)  
    MessageBox.Show("The area is: " & Area.ToString)  
End Sub  
```  
  
 <span data-ttu-id="a3265-118">Можно указать параметры и возвращаемые значения для потоков из пула потоков с помощью необязательного `ByVal` объект состояния переменной <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A>метод.</xref:System.Threading.ThreadPool.QueueUserWorkItem%2A></span><span class="sxs-lookup"><span data-stu-id="a3265-118">You can provide parameters and return values to thread-pool threads by using the optional `ByVal` state-object variable of the <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A> method.</span></span> <span data-ttu-id="a3265-119">Таймер потока потоков также поддерживает объект состояния для этой цели.</span><span class="sxs-lookup"><span data-stu-id="a3265-119">Thread-timer threads also support a state object for this purpose.</span></span> <span data-ttu-id="a3265-120">Сведения о группировке потоков и таймеры потоков в разделе [пул потоков (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/thread-pooling.md)[пул потоков](http://msdn.microsoft.com/library/4b8bb2c8-8ca4-457c-9afd-d11bc9a05701) и [таймеры потоков (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/thread-timers.md).</span><span class="sxs-lookup"><span data-stu-id="a3265-120">For information on thread pooling and thread timers, see [Thread Pooling (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/thread-pooling.md)[Thread Pooling](http://msdn.microsoft.com/library/4b8bb2c8-8ca4-457c-9afd-d11bc9a05701) and [Thread Timers (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/thread-timers.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a3265-121">См. также</span><span class="sxs-lookup"><span data-stu-id="a3265-121">See Also</span></span>  
 <span data-ttu-id="a3265-122">[Пошаговое руководство: Многопоточность с помощью компонента BackgroundWorker (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/walkthrough-multithreading-with-the-backgroundworker-component.md) </span><span class="sxs-lookup"><span data-stu-id="a3265-122">[Walkthrough: Multithreading with the BackgroundWorker Component (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/walkthrough-multithreading-with-the-backgroundworker-component.md) </span></span>  
<span data-ttu-id="a3265-123"> [Группировка потоков в пул (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/thread-pooling.md) </span><span class="sxs-lookup"><span data-stu-id="a3265-123"> [Thread Pooling (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/thread-pooling.md) </span></span>  
<span data-ttu-id="a3265-124"> [Синхронизация потоков (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/thread-synchronization.md) </span><span class="sxs-lookup"><span data-stu-id="a3265-124"> [Thread Synchronization (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/thread-synchronization.md) </span></span>  
<span data-ttu-id="a3265-125"> [События](../../../../visual-basic/programming-guide/language-features/events/index.md) </span><span class="sxs-lookup"><span data-stu-id="a3265-125"> [Events](../../../../visual-basic/programming-guide/language-features/events/index.md) </span></span>  
<span data-ttu-id="a3265-126"> [Многопоточные приложения (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/multithreaded-applications.md) </span><span class="sxs-lookup"><span data-stu-id="a3265-126"> [Multithreaded Applications (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/multithreaded-applications.md) </span></span>  
<span data-ttu-id="a3265-127"> [Делегаты](../../../../visual-basic/programming-guide/language-features/delegates/index.md) </span><span class="sxs-lookup"><span data-stu-id="a3265-127"> [Delegates](../../../../visual-basic/programming-guide/language-features/delegates/index.md) </span></span>  
<span data-ttu-id="a3265-128"> [Многопоточность в компонентах](http://msdn.microsoft.com/library/2fc31e68-fb71-4544-b654-0ce720478779)</span><span class="sxs-lookup"><span data-stu-id="a3265-128"> [Multithreading in Components](http://msdn.microsoft.com/library/2fc31e68-fb71-4544-b654-0ce720478779)</span></span>