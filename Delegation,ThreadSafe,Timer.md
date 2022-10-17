-------------------------------------------------------
# Deleigation #
> 委派: 我們可以發現--再相似的流程中把不同的邏輯抽出來就是委派的精隨。
> > Delegate的發展由函數指標(funtion pointer)而來，可以說Delegate是函數指標中的語法糖(Syntactic sugar)也不為過
> 
> 事件: 可以把一堆可變的動作/行為封裝出去，交給第三方指定
>
> 泛型: Action<>與Func<T,TRESULT>
> 
> 現成委派類 - Func與Action:
> > 在.NET Framework 3.5類別庫(與C#3.0一同推出)已經透過泛型定義好委派類別讓我們直接使用，減少我們額外的宣告委派的動作。
> > 而這些定義好的泛型delegate類別就是今天要講的 Func 與 Action。

[C#知識點講解之C#delegate、event、Action、EventHandler的使用和區別](https://www.twblogs.net/a/5eaf373086ec4d604917cf06)



### IT鐵人賽 - 我要轉職成 C# / .NET 工程師 - 委派 
> [委派 C#1.0](https://ithelp.ithome.com.tw/articles/10227783)
> 
> [委派 C# 2.0 與 匿名函式](https://ithelp.ithome.com.tw/articles/10227971)
> 
> [C# 3.0 Lambda 表示式](https://ithelp.ithome.com.tw/articles/10228322)
>
> [現成委派類 - Func <T> 與 Action <T>](https://ithelp.ithome.com.tw/articles/10228657)
> 現成委派類 - Func與Action
> > * Action - 接受沒有回傳值的void方法
> >
> > * Func - 接受有回傳值的方法


### 利用事件傳遞數據 
> [C# 事件(下) – 加上event關鍵字](https://ithelp.ithome.com.tw/articles/10228906)
> 但是委派要能讓外部客戶訂閱，就要能被外部使用，所以委派也有可能被外部執行而送出意料之外的通知。
> 而這個問題並不是private、protected這類存取修飾字可以解決的，所以在C#中，提供了event關鍵字來解決這個問題，讓委派能被外部加入方法，又能禁止被外部執行。
> 
> 用法很簡單，只要在之前的程式碼上，在使用我們自定義的委派型別前加上event就可以了. **加上event後，C#編譯器就會禁止外部來執行這個委派。**

### 程式人生
> [C# 委託(delegate)和事件(event)詳解](https://www.796t.com/content/1548166147.html)
> 
> [快速理解C#中的委託與事件](https://www.796t.com/content/1549107564.html)
> 

### William
>[何謂委派](https://medium.com/@WilliamWhetstone/c-%E4%BD%95%E8%AC%82%E5%A7%94%E6%B4%BE-delegate-e7eec68da4e2)
>
>[Design Pattern:Observer Pattern 觀察者模式](https://medium.com/@WilliamWhetstone/design-pattern-observer-pattern-%E8%A7%80%E5%AF%9F%E8%80%85%E6%A8%A1%E5%BC%8F-9c24298b4660)

### hackmd
> [[C#]使用委派(Delegate)與事件(Event)](https://hackmd.io/@BKLiang/csharp_delegate_event)
> 
> [玩轉C#之【委派和事件】- 委派的宣告、實體化和使用](https://hackmd.io/@IsHlp74-TK6Gg5UC4REAEw/ry3zuJi6L)

### 今天要介紹的是C#的委派 Delegate
> [本篇開始會依序從C#的發展順序介紹委派 Delegate、Anonymous Function、Lambda Expression、Func<>、Action<>](http://death0400.blogspot.com/2018/01/c-delegate.html)


-------------------------------------------------------
# 對控制項進行安全線程呼叫
### 原理
> [舊文重發：Windows 表單與多執行緒](https://www.huanlintalk.com/2009/01/windows.html)
> 在撰寫多執行緒的 Windows 表單應用程式時，有一項必須特別注意的規則，就是不可以在工作執行緒（worker thread）當中修改表單或控制項的屬性與方法。本文說明這項規則的由來，以及違反此規則將造成的後果，同時示範錯誤的以及正確的程式撰寫方式。

### Invoke & BeginInvoke
> [淺談Invoke 和 BegionInvoke的用法](https://iter01.com/427335.html)
> 
> [【分析】浅谈C#中Control的Invoke与BeginInvoke在主副线程中的执行顺序和区别（SamWang）](https://www.cnblogs.com/wangshenhe/archive/2012/05/25/2516842.html)
> > * Control.Invoke 方法 (Delegate) :在拥有此控件的基础窗口句柄的线程上执行指定的委托。
> > * Control.BeginInvoke 方法 (Delegate) :在创建控件的基础句柄所在线程上异步执行指定委托。
> > * Control的Invoke和BeginInvoke的委托方法是在主线程，即UI线程上执行。（也就是说如果你的委托方法用来取花费时间长的数据，然后更新界面什么的，千万别在主线程上调用Control.Invoke和Control.BeginInvoke，因为这些是依然阻塞UI线程的，造成界面的假死）
> > * Invoke会阻塞主支线程，BeginInvoke只会阻塞主线程，不会阻塞支线程！因此BeginInvoke的异步执行是指相对于支线程异步，而不是相对于主线程异步。（从最后一个例子就能看出，程序运行点击button1）

### 對控制項進行安全線程呼叫
> [如何 Windows Forms .net) 對控制項進行安全線程呼叫](https://learn.microsoft.com/zh-tw/dotnet/desktop/winforms/controls/how-to-make-thread-safe-calls?view=netdesktop-6.0&source=recommendations)
> 
> [跨執行緒存取UI](https://www.ez2o.com/Blog/Post/csharp-Cross-Thread-Call-Object)

-------------------------------------------------------
# Multi-thread / Timer
> [談談C#中各種執行緒的使用及注意項~](https://codingnote.cc/zh-tw/p/118004/)
> * 封裝一個執行緒類進行函數和參數的傳遞
> * C#中timer類的用法

> [C# Timer(3種)](https://ithelp.ithome.com.tw/articles/10195452?sc=rss.qu)

> [[C#.NET][Thread] 執行緒定時器](https://www.dotblogs.com.tw/yc421206/2011/01/30/21141)
> * System.Timers.Timer
> * System.Threading.Timer
> * System.Windows.Forms.Timer

> [[讀書筆記] Threading in C# - PART 3: USING THREADS](https://ithelp.ithome.com.tw/articles/10254641)

 ### Backgroundworker與Thread的區別
> [台部落-線程封裝組件(BackgroundWorker)和線程(Thread)](https://www.twblogs.net/a/5f0211f8d33e2533b014f8e5)
> 兩種方式的coding比對
> * BackgroundWorker是微軟的在.net Framwork中添加的一個組件，主要對線程的訪問提供了一種安全的方式。簡單的說就是對Thread的一次封裝。
> > 微軟官方的解釋爲：Executes an operation on a separate thread.就是說，開始一個新的線程執行操作。
> > BackgroundWorker是在內部使用了線程池的技術；同時，在Winform或WPF編碼中，它還給工作線程和UI線程提供了交互的能力。
>
> * Thread的使用就比較麻煩了，對於尤其是對異步提醒來說，需要寫委託，代碼量是很多
> * *總結* 當你執行的任務較簡單,不需要複雜控制時使用BackgroundWorker,較為方便;當你要執行的任務需要複雜控制(如執行緒同步)時,要自己 建立執行緒。畢竟，如果我們要實用多個執行緒，還需要往表單中加好幾個BackgroundWorker控制元件。

> [C#中Backgroundworker與Thread的區別](https://www.it145.com/9/183227.html)
  
  
