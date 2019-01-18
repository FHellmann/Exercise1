# Reasons for concurrency and parallelism


To complete this exercise you will have to use git. Create one or several commits that adds answers to the following questions and push it to your groups repository to complete the task.

When answering the questions, remember to use all the resources at your disposal. Asking the internet isn't a form of "cheating", it's a way of learning.

 ### What is concurrency? What is parallelism? What's the difference?
 > Concurrency and parallelism are distinct concepts. Concurrency is concerned with managing access to shared state from different threads, whereas parallelism is concerned with utilizing multiple processors/cores to improve the performance of a computation.
 
 ### Why have machines become increasingly multicore in the past decade?
 > The trend towards multiple cores is an engineering approach that helps the CPU designers avoid the power consumption problem that came with ever increasing frequency scaling. As CPU speeds rose into the 3-4 Ghz range the amount of electrical power required to go faster started to become prohibitive. The technical reasons for this are complex but factors like heat losses and leakage current (power that simply passes through the circuitry without doing anything useful) both increase faster as frequencies rise. While it's certainly possible to build a 6 GHz general purpose x86 CPU, it's not proven economical to do so efficiently. That's why the move to multi-core started and it is why we will see that trend continue at least until the parallelization issues become insurmountable. At the moment the trend towards virtualization has helped in the server arena as that allows us to parallelize aggregate workloads efficiently, for the moment at any rate.
 
 ### What kinds of problems motivates the need for concurrent execution?
 (Or phrased differently: What problems do concurrency help in solving?)
 > Concurrency refers to the ability of different parts or units of a program, algorithm, or problem to be executed out-of-order or in partial order, without affecting the final outcome. This allows for parallel execution of the concurrent units, which can significantly improve overall speed of the execution in multi-processor and multi-core systems. In more technical terms, concurrency refers to the decomposability property of a program, algorithm, or problem into order-independent or partially-ordered components or units.
 
 ### Does creating concurrent programs make the programmer's life easier? Harder? Maybe both?
 (Come back to this after you have worked on part 4 of this exercise)
 > Creating concurrent programs makes the programmer's life easier in the program structuring and in the aspect of the "don't repeat yourself" (DRY) principle. On the other hand it also makes the programmer's life harder because the behaviour especially when it comes to testing is really hard to reproduce because the behaviour is not deterministic anymore.
 
 ### What are the differences between processes, threads, green threads, and coroutines?
 > - Process: OS-managed (possibly) truly concurrent, at least in the presence of suitable hardware support. Exist within their own address space.
 > - Thread: OS-managed, within the same address space as the parent and all its other threads. Possibly truly concurrent, and multi-tasking is pre-emptive.
 > - Green Thread: These are user-space projections of the same concept as threads, but are not OS-managed. Probably not truly concurrent, except in the sense that there may be multiple worker threads or processes giving them CPU time concurrently, so probably best to consider this as interleaved or multiplexed.
 > - Coroutines: Exactly fibers, except not OS-managed.
 
 ### Which one of these do `pthread_create()` (C/POSIX), `threading.Thread()` (Python), `go` (Go) create?
 > - `pthread_create()` (C/POSIX) = thread
 > - `threading.Thread()` (Python) = green thread
 > - `go` (Go) = Something very fancy
 
 ### How does pythons Global Interpreter Lock (GIL) influence the way a python Thread behaves?
 > GIL effectively restricts bytecode execution to a single core, thus rendering pure Python threads an ineffective tool for distributing CPU bound work across multiple cores.
 
 ### With this in mind: What is the workaround for the GIL (Hint: it's another module)?
 > The main alternative provided in the standard library for CPU bound applications is the multiprocessing module, which works well for workloads that consist of relatively small numbers of long running computational tasks, but results in excessive message passing overhead if the duration of individual operations is short.
 
 ### What does `func GOMAXPROCS(n int) int` change? 
 > The GOMAXPROCS variable limits the number of operating system threads that can execute user-level Go code simultaneously. There is no limit to the number of threads that can be blocked in system calls on behalf of Go code; those do not count against the GOMAXPROCS limit. This package's GOMAXPROCS function queries and changes the limit.
