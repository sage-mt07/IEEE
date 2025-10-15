---
conversation_id: "dc3d6ed4-1ba5-47dd-8122-4da8e03e806a"
title: "IO Thread Env Variables"
create_time: 1716944994.222939
update_time: 1716945041.823456
language_guess: "en"
num_messages: 17
part_index: 1
part_count: 1
---

### system — 2024-05-29T01:09:54.222939+00:00

_(empty)_

### user — 2024-05-29T01:09:54.293535+00:00

NET 6には、I/Oスレッドに関連する環境変数

### assistant — 2024-05-29T01:10:03.749068+00:00

_(empty)_

### assistant — 2024-05-29T01:10:03.749281+00:00

.NET 6には、I/Oスレッドに関連する環境変数がいくつかあります。これらの環境変数を使用することで、アプリケーションのI/Oスレッドプールの動作を調整することができます。以下はその例です：

1. **DOTNET_THREADPOOL_IO_COMPLETION_PORT_MIN_THREADS**: 最小のI/Oコンプリーションポートスレッドの数を指定します。この変数を設定することで、I/Oスレッドプールの初期スレッド数を調整できます。

2. **DOTNET_THREADPOOL_IO_COMPLETION_PORT_MAX_THREADS**: 最大のI/Oコンプリーションポートスレッドの数を指定します。この変数を設定することで、I/Oスレッドプールが使用できる最大スレッド数を制限できます。

3. **DOTNET_THREADPOOL_MAX_THREADS**: スレッドプールが作成できる最大スレッド数を指定します。これには、通常の作業スレッドとI/Oコンプリーションポートスレッドの両方が含まれます。

これらの環境変数は、アプリケーションのパフォーマンスやリソース使用率を最適化するために重要です。適切に設定することで、I/O操作の効率を向上させることができます。

具体的な使用例や詳細な設定については、.NETの公式ドキュメントを参照することをお勧めします。

### user — 2024-05-29T01:10:31.560627+00:00

公式ドキュメントのuri

### assistant — 2024-05-29T01:10:41.558110+00:00

search(".NET 6 I/O threads environment variables site:docs.microsoft.com")

### tool — 2024-05-29T01:10:41.562738+00:00

_(empty)_

### assistant — 2024-05-29T01:10:41.566414+00:00

mclick([0, 1, 2])

### tool — 2024-05-29T01:10:41.572713+00:00

Error when executing command `mclick([0, 1, 2])`

3 failed clicks:
recorded='click(0)' temporary=None permanent='click failed' new_state=None final=None success=False feedback='Tried to click on an invalid id `0`. Available ids: dict_keys([])' metadata={}
recorded='click(1)' temporary=None permanent='click failed' new_state=None final=None success=False feedback='Tried to click on an invalid id `1`. Available ids: dict_keys([])' metadata={}
recorded='click(2)' temporary=None permanent='click failed' new_state=None final=None success=False feedback='Tried to click on an invalid id `2`. Available ids: dict_keys([])' metadata={}

### assistant — 2024-05-29T01:10:41.572927+00:00

search(".NET 6 I/O threads environment variables")

### tool — 2024-05-29T01:10:41.579666+00:00

_(empty)_

### assistant — 2024-05-29T01:10:41.585193+00:00

mclick([0, 2, 10])

### tool — 2024-05-29T01:10:41.592182+00:00

* This setting is enabled by default on Windows 11 and later versions, and disabled by default on Windows 10 and earlier versions. For this setting to take effect when enabled, the GC must also be configured to use all CPU groups; for more information, see 【6†GC CPU groups】.

Setting name Values  
runtimeconfig.json N/A N/A  
Environment variable `COMPlus_Thread_UseAllCpuGroups` or `DOTNET_Thread_UseAllCpuGroups` `0` - disabled   
`1` - enabled  

## Assign threads to CPU groups on Windows

  * On machines that have multiple CPU groups and 【7†all CPU groups are being used】, this setting configures whether threads are automatically distributed across CPU groups.
  * When this setting is enabled, new threads are assigned to a CPU group in a way that tries to fully populate a CPU group that is already in use before utilizing a new CPU group.
  * This setting is enabled by default.

Setting name Values  
runtimeconfig.json N/A N/A  
Environment variable `COMPlus_Thread_AssignCpuGroups` or `DOTNET_Thread_AssignCpuGroups` `0` - disabled   
`1` - enabled  

## Minimum threads

  * Specifies the minimum number of threads for the worker thread pool.
  * Corresponds to the 【8†ThreadPool.SetMinThreads】 method.

Setting name Values  
runtimeconfig.json `System.Threading.ThreadPool.MinThreads` An integer that represents the minimum number of threads  
MSBuild property `ThreadPoolMinThreads` An integer that represents the minimum number of threads  
Environment variable N/A N/A  

### Examples

runtimeconfig.json file:

    {
       "runtimeOptions": {
          "configProperties": {
             "System.Threading.ThreadPool.MinThreads": 4
          }
       }
    }

runtimeconfig.template.json file:

    {
       "configProperties": {
          "System.Threading.ThreadPool.MinThreads": 4
       }
    }

Project file:

    <Project Sdk="Microsoft.NET.Sdk">

      <PropertyGroup>
        <ThreadPoolMinThreads>4</ThreadPoolMinThreads>
      </PropertyGroup>

    </Project>

## Maximum threads

  * Specifies the maximum number of threads for the worker thread pool.
  * Corresponds to the 【9†ThreadPool.SetMaxThreads】 method.

Setting name Values  
runtimeconfig.json `System.Threading.ThreadPool.MaxThreads` An integer that represents the maximum number of threads  
MSBuild property `ThreadPoolMaxThreads` An integer that represents the maximum number of threads  
Environment variable N/A N/A  

### Examples

runtimeconfig.json file:

    {
       "runtimeOptions": {
          "configProperties": {
             "System.Threading.ThreadPool.MaxThreads": 20
          }
       }
    }

runtimeconfig.template.json file:

    {
       "configProperties": {
          "System.Threading.ThreadPool.MaxThreads": 20
       }
    }

Project file:

    <Project Sdk="Microsoft.NET.Sdk">

      <PropertyGroup>
        <ThreadPoolMaxThreads>20</ThreadPoolMaxThreads>
      </PropertyGroup>

    </Project>

## Windows thread pool

  * For projects on Windows, configures whether thread pool thread management is delegated to the Windows thread pool.
  * If you omit this setting or the platform is not Windows, the .NET thread pool is used instead.
  * Only applications published with Native AOT on Windows use the Windows thread pool by default, for which you can opt to use the .NET thread pool instead by disabling the config setting.
  * The Windows thread pool may perform better in some cases, such as in cases where the minimum number of threads is configured to a high value, or when the Windows thread pool is already being heavily used by the app. There may also be cases where the .NET thread pool performs better, such as in heavy I/O handling on larger machines. It's advisable to check performance metrics when changing this config setting.
  * Some APIs are not supported when using the Windows thread pool, such as 【8†ThreadPool.SetMinThreads】, 【9†ThreadPool.SetMaxThreads】, and 【10†ThreadPool.BindHandle(SafeHandle)】. Thread pool config settings for minimum and maximum threads are also not effective. An alternative to 【10†ThreadPool.BindHandle(SafeHandle)】 is the 【11†ThreadPoolBoundHandle】 class.

Setting name Values Version introduced  
runtimeconfig.json `System.Threading.ThreadPool.UseWindowsThreadPool` `true` - enabled   
`false` - disabled .NET 8  
MSBuild property `UseWindowsThreadPool` `true` - enabled   
`false` - disabled .NET 8  
Environment variable `DOTNET_ThreadPool_UseWindowsThreadPool` `1` - enabled   
`0` - disabled .NET 8  

### Examples

runtimeconfig.json file:

    {
       "runtimeOptions": {
          "configProperties": {
             "System.Threading.ThreadPool.UseWindowsThreadPool": true
          }
       }
    }

runtimeconfig.template.json file:

    {
       "configProperties": {
          "System.Threading.ThreadPool.UseWindowsThreadPool": true
       }
    }

Project file:

    <Project Sdk="Microsoft.NET.Sdk">

      <PropertyGroup>
        <UseWindowsThreadPool>true</UseWindowsThreadPool>
      </PropertyGroup>

    </Project>

## Thread injection in response to blocking work items

In some cases, the thread pool detects work items that block its threads. To compensate, it injects more threads. In .NET 6+, you can use the following 【12†runtime configuration†github.com】 settings to configure thread injection in response to blocking work items. Currently, these settings take effect only for work items that wait for another task to complete, such as in typical 【13†sync-over-async†devblogs.microsoft.com】 cases.

runtimeconfig.json setting name Description Version introduced  
`System.Threading.ThreadPool.Blocking.ThreadsToAddWithoutDelay_ProcCountFactor` After the thread count based on `MinThreads` is reached, this value (after it is multiplied by the processor count) specifies how many additional threads may be created without a delay. .NET 6  
`System.Threading.ThreadPool.Blocking.ThreadsPerDelayStep_ProcCountFactor` After the thread count based on `ThreadsToAddWithoutDelay` is reached, this value (after it is multiplied by the processor count) specifies after how many threads an additional `DelayStepMs` would be added to the delay before each new thread is created. .NET 6  
`System.Threading.ThreadPool.Blocking.DelayStepMs` After the thread count based on `ThreadsToAddWithoutDelay` is reached, this value specifies how much additional delay to add per `ThreadsPerDelayStep` threads, which would be applied before each new thread is created. .NET 6  
`System.Threading.ThreadPool.Blocking.MaxDelayMs` After the thread count based on `ThreadsToAddWithoutDelay` is reached, this value specifies the max delay to use before each new thread is created. .NET 6  
`System.Threading.ThreadPool.Blocking.IgnoreMemoryUsage` By default, the rate of thread injection in response to blocking is limited by heuristics that determine whether there is sufficient physical memory available. In some situations, it may be preferable to inject threads more quickly even in low-memory situations. You can disable the memory usage heuristics by turning off this switch. .NET 7  

### How the configuration settings take effect

  * After the thread count based on `MinThreads` is reached, up to `ThreadsToAddWithoutDelay` additional threads may be created without a delay.
  * After that, before each additional thread is created, a delay is induced, starting with `DelayStepMs`.
  * For every `ThreadsPerDelayStep` threads that are added with a delay, an additional `DelayStepMs` is added to the delay.
  * The delay may not exceed `MaxDelayMs`.
  * Delays are only induced before creating threads. If threads are already available, they would be released without delay to compensate for blocking work items.
  * Physical memory usage and limits are also used and, beyond a threshold, the system switches to slower thread injection.

### Examples

runtimeconfig.json file:

    {
       "runtimeOptions": {
          "configProperties": {
             "System.Threading.ThreadPool.Blocking.ThreadsToAddWithoutDelay_ProcCountFactor": 5
          }
       }
    }

runtimeconfig.template.json file:

    {
       "configProperties": {
          "System.Threading.ThreadPool.Blocking.ThreadsToAddWithoutDelay_ProcCountFactor": 5
       }
    }

## `AutoreleasePool` for managed threads

This option configures whether each managed thread receives an implicit 【14†NSAutoreleasePool†developer.apple.com】 when running on a supported macOS platform.

Setting name Values Version introduced  
runtimeconfig.json `System.Threading.Thread.EnableAutoreleasePool` `true` or `false` .NET 6  
MSBuild property `AutoreleasePoolSupport` `true` or `false` .NET 6  
Environment variable N/A N/A N/A  

### Examples

runtimeconfig.json file:

    {
       "runtimeOptions": {
          "configProperties": {
             "System.Threading.Thread.EnableAutoreleasePool": true
          }
       }
    }

runtimeconfig.template.json file:

    {
       "configProperties": {
          "System.Threading.Thread.EnableAutoreleasePool": true
       }
    }

Project file:

    <Project Sdk="Microsoft.NET.Sdk">

      <PropertyGroup>
        <AutoreleasePoolSupport>true</AutoreleasePoolSupport>
      </PropertyGroup>

    </Project>

Collaborate with us on GitHub 

The source for this content can be found on GitHub, where you can also create and review issues and pull requests. For more information, see 【15†our contributor guide】. 

[Image 0] [Image 1] 

.NET

Open a documentation issue 【1

### tool — 2024-05-29T01:10:41.592439+00:00

Many methods of the managed threading classes provide time-outs to help you detect deadlocks. For example, the following code attempts to acquire a lock on an object named `lockObject`. If the lock is not obtained in 300 milliseconds, 【5†Monitor.TryEnter】 returns `false`.

    If Monitor.TryEnter(lockObject, 300) Then  
        Try  
            ' Place code protected by the Monitor here.  
        Finally  
            Monitor.Exit(lockObject)  
        End Try  
    Else  
        ' Code to execute if the attempt times out.  
    End If  

    if (Monitor.TryEnter(lockObject, 300)) {  
        try {  
            // Place code protected by the Monitor here.  
        }  
        finally {  
            Monitor.Exit(lockObject);  
        }  
    }  
    else {  
        // Code to execute if the attempt times out.  
    }  

### Race conditions

A race condition is a bug that occurs when the outcome of a program depends on which of two or more threads reaches a particular block of code first. Running the program many times produces different results, and the result of any given run cannot be predicted.

A simple example of a race condition is incrementing a field. Suppose a class has a private static field (Shared in Visual Basic) that is incremented every time an instance of the class is created, using code such as `objCt++;` (C#) or `objCt += 1` (Visual Basic). This operation requires loading the value from `objCt` into a register, incrementing the value, and storing it in `objCt`.

In a multithreaded application, a thread that has loaded and incremented the value might be preempted by another thread which performs all three steps; when the first thread resumes execution and stores its value, it overwrites `objCt` without taking into account the fact that the value has changed in the interim.

This particular race condition is easily avoided by using methods of the 【6†Interlocked】 class, such as 【7†Interlocked.Increment】. To read about other techniques for synchronizing data among multiple threads, see 【8†Synchronizing Data for Multithreading】.

Race conditions can also occur when you synchronize the activities of multiple threads. Whenever you write a line of code, you must consider what might happen if a thread were preempted before executing the line (or before any of the individual machine instructions that make up the line), and another thread overtook it.

## Static members and static constructors

A class is not initialized until its class constructor (`static` constructor in C#, `Shared Sub New` in Visual Basic) has finished running. To prevent the execution of code on a type that is not initialized, the common language runtime blocks all calls from other threads to `static` members of the class (`Shared` members in Visual Basic) until the class constructor has finished running.

For example, if a class constructor starts a new thread, and the thread procedure calls a `static` member of the class, the new thread blocks until the class constructor completes.

This applies to any type that can have a `static` constructor.

## Number of processors

Whether there are multiple processors or only one processor available on a system can influence multithreaded architecture. For more information, see 【9†Number of Processors】.

Use the 【10†Environment.ProcessorCount】 property to determine the number of processors available at run time.

## General recommendations

Consider the following guidelines when using multiple threads:

  * Don't use 【11†Thread.Abort】 to terminate other threads. Calling `Abort` on another thread is akin to throwing an exception on that thread, without knowing what point that thread has reached in its processing.

  * Don't use 【12†Thread.Suspend】 and 【13†Thread.Resume】 to synchronize the activities of multiple threads. Do use 【14†Mutex】, 【15†ManualResetEvent】, 【16†AutoResetEvent】, and 【17†Monitor】.

  * Don't control the execution of worker threads from your main program (using events, for example). Instead, design your program so that worker threads are responsible for waiting until work is available, executing it, and notifying other parts of your program when finished. If your worker threads do not block, consider using thread pool threads. 【18†Monitor.PulseAll】 is useful in situations where worker threads block.

  * Don't use types as lock objects. That is, avoid code such as `lock(typeof(X))` in C# or `SyncLock(GetType(X))` in Visual Basic, or the use of 【19†Monitor.Enter】 with 【20†Type】 objects. For a given type, there is only one instance of 【20†System.Type】 per application domain. If the type you take a lock on is public, code other than your own can take locks on it, leading to deadlocks. For additional issues, see 【21†Reliability Best Practices】.

  * Use caution when locking on instances, for example `lock(this)` in C# or `SyncLock(Me)` in Visual Basic. If other code in your application, external to the type, takes a lock on the object, deadlocks could occur.

  * Do ensure that a thread that has entered a monitor always leaves that monitor, even if an exception occurs while the thread is in the monitor. The C# 【22†lock】 statement and the Visual Basic 【23†SyncLock】 statement provide this behavior automatically, employing a finally block to ensure that 【24†Monitor.Exit】 is called. If you cannot ensure that Exit will be called, consider changing your design to use Mutex. A mutex is automatically released when the thread that currently owns it terminates.

  * Do use multiple threads for tasks that require different resources, and avoid assigning multiple threads to a single resource. For example, any task involving I/O benefits from having its own thread, because that thread will block during I/O operations and thus allow other threads to execute. User input is another resource that benefits from a dedicated thread. On a single-processor computer, a task that involves intensive computation coexists with user input and with tasks that involve I/O, but multiple computation-intensive tasks contend with each other.

  * Consider using methods of the 【6†Interlocked】 class for simple state changes, instead of using the `lock` statement (`SyncLock` in Visual Basic). The `lock` statement is a good general-purpose tool, but the 【6†Interlocked】 class provides better performance for updates that must be atomic. Internally, it executes a single lock prefix if there is no contention. In code reviews, watch for code like that shown in the following examples. In the first example, a state variable is incremented:

        SyncLock lockObject  
        myField += 1  
    End SyncLock  

        lock(lockObject)
    {  
        myField++;  
    }  

You can improve performance by using the 【7†Increment】 method instead of the `lock` statement, as follows:

        System.Threading.Interlocked.Increment(myField)  

        System.Threading.Interlocked.Increment(myField);  

Note

Use the 【25†Add】 method for atomic increments larger than 1.

In the second example, a reference type variable is updated only if it is a null reference (`Nothing` in Visual Basic).

        If x Is Nothing Then  
        SyncLock lockObject  
            If x Is Nothing Then  
                x = y  
            End If  
        End SyncLock  
    End If  

        if (x == null)  
    {  
        lock (lockObject)  
        {  
            x ??= y;
        }  
    }  

Performance can be improved by using the 【26†CompareExchange】 method instead, as follows:

        System.Threading.Interlocked.CompareExchange(x, y, Nothing)  

        System.Threading.Interlocked.CompareExchange(ref x, y, null);  

Note

The 【27†CompareExchange<T>(T, T, T)】 method overload provides a type-safe alternative for reference types.

## Recommendations for class libraries

Consider the following guidelines when designing class libraries for multithreading:

  * Avoid the need for synchronization, if possible. This is especially true for heavily used code. For example, an algorithm might be adjusted to tolerate a race condition rather than eliminate it. Unnecessary synchronization decreases performance and creates the possibility of deadlocks and race conditions.

  * Make static data (`Shared` in Visual Basic) thread safe by default.

  * Do not make instance data thread safe by default. Adding locks to create thread-safe code decreases performance, increases lock contention, and creates the possibility for deadlocks to occur. In common application models, only one thread at a time executes user code, which minimizes the need for thread safety. For this reason, the .NET class libraries are not thread safe by default.

  * Avoid providing static methods that alter static state. In common server scenarios, static state is shared across requests, which means multiple threads can execute that code at the same time. This opens up the possibility of threading bugs. Consider using a design pattern that encapsulates data into instances that are not shared across requests. Furthermore, if static data are synchronized, calls between static methods that alter state can result in deadlocks or redundant synchronization, adversely affecting performance.

## See also

  * 【28†Threading】
  * 【29†Threads and Threading】

Collaborate with us on GitHub 

The source for this content can be found on GitHub, where you can also create and review issues and pull requests. For more information, see 【30†our contributor guide】. 

[Image 0] [Image 1] 

.NET

Open a documentation issue 【31† Provide product feedback †aka.ms】 

## Feedback

  Com

### tool — 2024-05-29T01:10:41.592674+00:00

* 【5†About】
  * 【6†Archives】

# I/O Threads Explained

December 13, 2014

Microsoft has released async/await feature in .Net 4.5. It’s a really great stuff as it significantly simplifies one of the most painful areas - asynchronous programming. Before that, Task Parallel Library (TPL) and Parallel LINQ (PLINQ) were released in .Net 4.0. They address problems with parallel programming - another painful area in .Net.

I often see programmers struggling with a question when to use each of these features. Let’s step back and recall what does it actually mean to be asynchronous or parallel.

## The difference between asynchronous programming and parallel programming

So, is there any difference between these two notions? Yes, there is. You can think of parallel programming as a subset of asynchronous programming: every parallel execution is asynchronous, but not every asynchronous execution is parallel.

Let’s take an example.

  * When someone calls you, you usually pick up your phone and answer immediately, leaving your current tasks. It is a synchronous communication.

  * When someone sends you an email, you can postpone the answer, say, to evening, and continue working on your current tasks. It is an asynchronous communication.

  * When someone calls you, you can answer while working on your current tasks at the same time. It’s a parallel communication.

Returning to programming, the difference between synchronous and asynchronous execution is that in case of synchronous execution, the thread leaves its current task and starts working on a new task immediately. On the other hand, with asynchronous execution the thread continues working on its current task.

The difference between asynchronous and parallel execution is that with asynchronous execution you don’t always need another thread to execute a new task. The new task can be executed after the thread is done with its current task. Until that moment, this new task waits in a queue.

## What are I/O threads?

To use asynchronous and parallel features of the .NET properly, you should also understand the concept of I/O threads.

Not everything in a program consumes CPU time. When a thread tries to read data from a file on disk or sends a TCP/IP packet through network, the only thing it does is delegate the actual work to a device - disk or network adapter - and wait for results.

It’s very expensive to spend threads' time on waiting. Even through threads sleep and don’t consume CPU time while waiting for the results, it doesn’t really pay off because it’s a waste of system resources. Every thread holds about 2Mb of memory for stack variables, local storage and so on. Also, the more threads you have, the more time it takes to switch among them.

It’s much more efficient for threads to send a command to device and ask to ping them back after the work is done. Threads shouldn’t spend their time on sleeping.

Think about the analogy. Let’s say there’s a cook making a dinner for a lot of people. He or she certainly has a gas-stove or a toaster or a human assistant. The cook’s time costs more than toaster’s, stove’s or even assistant’s time, so it would be better if the cook doesn’t waste their time on sitting and waiting for a toast to be made. Or for the assistant to return from a store. It’d be more efficient for them to put the cake in the oven and return back after the bell, cooking other stuff meanwhile. A single cook can be very productive in such a way.

I/O thread is an abstraction intended to hide work with devices behind a simple and familiar concept. The main point here is that you don’t have to work with those devices in a different way, you can think of the pipeline inside them just like it’s a usual CPU consuming thread. At the same time, I/O threads are extremely cheap in comparison with CPU-bound threads, because, in fact, they are merely requests to devices.

So, let’s summarize. When a program reads data from a file, we say it starts a new I/O thread, meaning that it actually sends a command to a hard drive. When the drive finishes reading, we say I/O thread is completed, meaning that the drive sends the data back to the program.

Let’s look at the code:

    public void ReadData(string filePath, int byteCount)
    {
        byte[] buffer = new byte[byteCount];
        using (FileStream fs = new FileStream(filePath, FileMode.Open))
        {
            fs.Read(buffer, 0, byteCount); // 1
        }
    }

I/O thread is started at the line marked as "1". The main thread falls to sleep and waits for the I/O thread to complete. After it’s done, it sends the data back to the main thread. Then the main thread wakes up and continues working.

Why mimic CPU-bound threads behavior?

Why would I/O threads mimic CPU-bound threads? Because they are really about the same. Both I/O thread and CPU-bound thread proceed some work. The only difference is that I/O thread uses resources other than CPU.

Look at this code:

    public void Compute()
    {
        Thread thread = new Thread(() => PerformComputation());
        thread.Start(); // 1
        thread.Join(); // 2
    }

CPU bound thread is started at the line "1". At the line "2" the calling thread falls to sleep, waiting for the inner thread to complete. After it’s done, the main thread continues working. It’s really similar to what we had in the previous code example, isn’t it?

The 【7†Task class†msdn.microsoft.com】 introduced in .NET 4 allows to hide the difference between these two types of threads:

    public Task ReadDataAsync(string filePath, int byteCount)
    {
        byte[] buffer = new byte[byteCount];
        FileStream fs = new FileStream(filePath, FileMode.Open);
        return fs.ReadAsync(buffer, 0, byteCount);
    }

    public Task ComputeAsync()
    {
        return Task.Run(() => PerformComputation());
    }

Now you can get the Task instance and track its state in spite of what type of work is actually being performed. In other words, Task class allows to abstract CPU-bound threads and I/O threads in a 【8†future†en.wikipedia.org】 construct.

## Further reading

  * 【9†CLR via C#†www.amazon.com】, Chapter 28: I/O-Bound Asynchronous Operations

  * 【10†I/O Completion Ports†msdn.microsoft.com】: an MSDN article in describing I/O completion ports in detail

  * 【11†← Separation of Concerns in ORM】 
  * 【12†Async/await in C#: pitfalls →】 

## Subscribe

* * *

I don't post everything on my blog. Don't miss smaller tips and updates. Sign up to my mailing list below.

## Comments

* * *

Please enable JavaScript to view the 【13†comments powered by Disqus.†disqus.com】 【14†comments powered by Disqus†disqus.com】 

Top

[Image 1: Vladimir Khorikov]

###### Vladimir Khorikov

【15† †twitter.com】 【16† 】 【17† †www.linkedin.com】

###### My book

【18† 】

Click here to get a 40% discount

###### Pluralsight courses

【19† 】 ‒ 【20†Pragmatic Unit Testing】  
‒ 【21†Domain-Driven Design in Practice】  
‒ 【22†Applying Functional Principles in C#】  
‒ 【23†Database Delivery Best Practices】  
‒ 【24†Specification Pattern in C#】  
‒ 【25†Refactoring from Anemic Domain Model】  
‒ 【26†Domain-Driven Design: Working with Legacy Projects】  
‒ 【27†CQRS in Practice】  
‒ 【28†DDD and EF Core: Preserving Encapsulation】  
‒ 【29†Validation and DDD】  
‒ 【30†Encapsulating EF Core Usage】  
‒ 【31†Prepare for coding interviews with CodeStandard†codestandard.net】

###### Most Popular Articles

‒ 【32†EF Core 2.1 vs NHibernate 5.1: DDD perspective】  
‒ 【33†C# and F# approaches to illegal states】  
‒ 【34†Optimistic locking and automatic retry】  
‒ 【35†Entity vs Value Object: the ultimate list of differences】  
‒ 【36†DTO vs Value Object vs POCO】  
‒ 【37†3 misuses of ?. operator in C# 6】  
‒ 【38†Specification pattern: C# implementation】  
‒ 【39†Database versioning best practices】  
‒ 【40†Unit testing private methods】  
‒ 【41†Functional C#: Handling failures, input errors】  
‒ 【42†REST API response codes: 400 vs 500】

【43† †mvp.microsoft.com】

###### Recent Articles

‒ 【44†Storing information in its highest form】  
‒ 【45†Which collection interface to use?】  
‒ 【46†Generic types are for arguments, specific types are for return values】  
‒ 【47†Modeling Relationships in a DDD Way】  
‒ 【48†Encapsulating EF Core Usage: New Pluralsight course】  
‒ 【49†Collections and Primitive Obsession】  
‒ 【50†How to Assert Database State?】  
‒ 【51†Should you Abstract the Database?】  
‒ 【52†Database and Always-Valid Domain Model】  
‒ 【53†Specification Pattern vs Always-Valid Domain Model】  

【6†» All arti

### assistant — 2024-05-29T01:10:41.592952+00:00

.NET 6 provides several environment variables for configuring I/O threads, which can be particularly useful for optimizing the performance of applications involving asynchronous and parallel operations.

Key environment variables include:

1. **`DOTNET_THREADPOOL_IO_COMPLETION_PORT_MIN_THREADS`**: This sets the minimum number of I/O completion port threads.
2. **`DOTNET_THREADPOOL_IO_COMPLETION_PORT_MAX_THREADS`**: This sets the maximum number of I/O completion port threads.
3. **`DOTNET_THREADPOOL_MAX_THREADS`**: This defines the maximum number of threads for the thread pool, including both worker and I/O threads.

These configurations help control how the .NET runtime handles I/O-bound operations, ensuring efficient resource use and potentially improving application responsiveness. Detailed settings and examples can be found in the .NET documentation:

- [Threading config settings](https://learn.microsoft.com/en-us/dotnet/core/runtime-config/threading)
- [Managed Threading Best Practices](https://learn.microsoft.com/en-us/dotnet/standard/threading/managed-threading-best-practices)

For an in-depth explanation of I/O threads and their management, you might also find the article on Enterprise Craftsmanship helpful: [I/O Threads Explained](https://enterprisecraftsmanship.com/posts/io-threads-explained).
