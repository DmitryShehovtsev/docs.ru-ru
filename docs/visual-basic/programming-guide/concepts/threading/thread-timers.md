---
title: "Таймеры (Visual Basic) потоков | Документы Microsoft"
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
ms.assetid: 809cba93-cc93-4e21-afda-f299f9a39818
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: af184f6f061cfd95b767a95a6b34f18bd6ba4f2b
ms.contentlocale: ru-ru
ms.lasthandoff: 04/12/2017

---
# <a name="thread-timers-visual-basic"></a><span data-ttu-id="b3552-102">Таймеры потоков (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="b3552-102">Thread Timers (Visual Basic)</span></span>
<span data-ttu-id="b3552-103"><xref:System.Threading.Timer?displayProperty=fullName>Класс полезен для периодического запуска задач в отдельном потоке.</xref:System.Threading.Timer?displayProperty=fullName></span><span class="sxs-lookup"><span data-stu-id="b3552-103">The <xref:System.Threading.Timer?displayProperty=fullName> class is useful for periodically running a task on a separate thread.</span></span> <span data-ttu-id="b3552-104">Например можно использовать таймер потока для проверки состояния и целостности базы данных или резервное копирование важных файлов.</span><span class="sxs-lookup"><span data-stu-id="b3552-104">For example, you could use a thread timer to check the status and integrity of a database or to back up critical files.</span></span>  
  
## <a name="thread-timer-example"></a><span data-ttu-id="b3552-105">Пример таймера потока</span><span class="sxs-lookup"><span data-stu-id="b3552-105">Thread Timer Example</span></span>  
 <span data-ttu-id="b3552-106">В следующем примере задача запускается каждые две секунды и использует флаг для инициирования <xref:System.IDisposable.Dispose%2A>метод, который останавливает таймер.</xref:System.IDisposable.Dispose%2A></span><span class="sxs-lookup"><span data-stu-id="b3552-106">The following example starts a task every two seconds and uses a flag to initiate the <xref:System.IDisposable.Dispose%2A> method that stops the timer.</span></span> <span data-ttu-id="b3552-107">В этом примере состояние отображается в окне вывода.</span><span class="sxs-lookup"><span data-stu-id="b3552-107">This example posts status to the output window.</span></span>  
  
```vb  
Private Class StateObjClass  
    ' Used to hold parameters for calls to TimerTask.  
    Public SomeValue As Integer  
    Public TimerReference As System.Threading.Timer  
    Public TimerCanceled As Boolean  
End Class  
  
Public Sub RunTimer()  
    Dim StateObj As New StateObjClass  
    StateObj.TimerCanceled = False  
    StateObj.SomeValue = 1  
    Dim TimerDelegate As New System.Threading.TimerCallback(AddressOf TimerTask)  
    ' Create a timer that calls a procedure every 2 seconds.  
    ' Note: There is no Start method; the timer starts running as soon as   
    ' the instance is created.  
    Dim TimerItem As New System.Threading.Timer(TimerDelegate, StateObj,  
                                                2000, 2000)  
    ' Save a reference for Dispose.  
    StateObj.TimerReference = TimerItem  
  
    ' Run for ten loops.  
    While StateObj.SomeValue < 10  
        ' Wait one second.  
        System.Threading.Thread.Sleep(1000)  
    End While  
  
    ' Request Dispose of the timer object.  
    StateObj.TimerCanceled = True  
End Sub  
  
Private Sub TimerTask(ByVal StateObj As Object)  
    Dim State As StateObjClass = CType(StateObj, StateObjClass)  
    ' Use the interlocked class to increment the counter variable.  
    System.Threading.Interlocked.Increment(State.SomeValue)  
    System.Diagnostics.Debug.WriteLine("Launched new thread  " & Now.ToString)  
    If State.TimerCanceled Then  
        ' Dispose Requested.  
        State.TimerReference.Dispose()  
        System.Diagnostics.Debug.WriteLine("Done  " & Now)  
    End If  
End Sub  
```  
  
 <span data-ttu-id="b3552-108">Таймеры потоков особенно полезны при <xref:System.Windows.Forms.Timer?displayProperty=fullName>объект недоступен, например при разработке консольных приложений.</xref:System.Windows.Forms.Timer?displayProperty=fullName></span><span class="sxs-lookup"><span data-stu-id="b3552-108">Thread timers are particularly useful when the <xref:System.Windows.Forms.Timer?displayProperty=fullName> object is unavailable, such as when you are developing console applications.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b3552-109">См. также</span><span class="sxs-lookup"><span data-stu-id="b3552-109">See Also</span></span>  
 <span data-ttu-id="b3552-110"><xref:System.Threading></xref:System.Threading></span><span class="sxs-lookup"><span data-stu-id="b3552-110"><xref:System.Threading></span></span>   
<span data-ttu-id="b3552-111"> [Многопоточные приложения (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/multithreaded-applications.md)</span><span class="sxs-lookup"><span data-stu-id="b3552-111"> [Multithreaded Applications (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/multithreaded-applications.md)</span></span>