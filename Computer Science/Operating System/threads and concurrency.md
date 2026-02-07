## Threads
|Threads||
|--|--|
|visual **metaphor**|**worker** at a shop <br> - active entity: executing unit of a process <br> - works simultaneously with others threads  <br> - requires coordination - sharing of I/O devices, CPUs, memory
----


## Process vs. Thread
|Aspects |Process | Threads|
|--|---|--|
Defination|A single-thread process is represented by <br> - its [**address space**](process%20management.md#process-address-space-and-memory-management) (virtual - physical memory mapping) and <br> - its **execation context** (stack pointer, register, program counter etc). |Threads represent multiple **independent** execution contexts. <br> - **shared info**: They are within the **same virtual address space**, which means they share the virtual to physical address mapping, and the code/data/files.<br> - **Per-thread info** (in a seperate data structure): Threads will potentially execute **different** **instructions** and accessing different portions of the **address space**, operate on different portions of the **input** etc. This means that each thread will have to have its own different **program counter, stack stack, pointer, thread-specific registers**.|
|PCB|<br> OS represents  all the information in a [process control block (PCB)](process%20management.md#process-control-block). | More complex PCB: <br> - shared virtual address mapping, code,data <br> - per-thread executaion context.|
|virtual addresss| seperate| shared|
|execution context|✅| ✅ |
|context switch| longer | shorter|
|communication mechanisms| inter process communication (IPC) (expensive)| shared variable (cheap)|
|cache| cold| hot|
----

Figure: Multi-Threads
![Multi-Threads](figures/os-multi-threads.png)

Figure: Single thread Process vs. **Multi Thread** Process
![Process vs. Thread](figures/os-process-vs-thread.png)







### Benefits of Multithreading
|cases| reasons|
|--|---|
|in multi-core/multi processor system| - Each thread executes same code but for different subset of **input** (e.g., a matrix)in **parallel** **concurrently** on a different processor to **speed up** <br> - Each thread executes different portions of program for special **tasks** to set **prioirty** differently and get **performance gain** by **hot cache** |
|why **multithreading** instead of **multiprocess**?| - **lower memory requirement**: A **multiprocess** application requires **more memory** => more swaps from disk (we have to allocate each process a address space, and a executation context) while <br>  a **multi-threaded** application requires **less memory** (sharing address space). <br> - **lower communication overhead**: communicating, passing, synchronizing data among processes (requires **inter process communication IPC**) is more **costly** than **inter thread communication**(**shared variables** in the same process address space)|
|even on **Single CPU** or generally when **number of threads > the number of CPUs**| - **Hide latency** associated with I/O operations: If thread has to wait on some event for some time **(t_idle)> two context switche (2*t_ctx_switch)**, then it makes sense to switch to another **thread** to perform other operation and switch back. <br> - **No memory overhead**: Threads **shared address space**|
|User applications and **OS kernel**| support **multiple execution contexts** to operate concurrently <br> - OS threads could work on behalf of apps <br> - run OS level services like aemons and device drivers. |
---

Figure: Multi-process requires more **memory (address space)** while multi-threads does not!
![Multi-Process](figures/os-multi-process.png)

Figure: Multi-threading is benificial even on **Single CPU**
![Multi-Process](figures/os-multi-thread-single-CPU.png)

## Basic Thread Mechanisms
### overview
|What we need to support threads|Function| Meaning|
|---|---|--|
|thread data structure| identify threads, keep track resource usage| represent each thread
|Synchronization Mechanisms| - create and manage threads <br> - allow threads safely coordinate among each other running concurrently in the same address space| - don't overwrite each other's inputs or results <br> - allow one thread to wait on results that should be produced by other threads| 
---






### Synchronization Mechanisms
#### Why we need synchronization mechanisms? issues of concurrent execution 

Figure: Data Race problem on threads because threads share memory address space
![data race](figures/os-data-race.png)

|process| threads|
|---|---|
|Each process operate within their own address space. The operating system ensures that no valid mapping and access for any address in address space of a process (e.g., P2) to physcial memory (X) which is already mapped to another process (P1)| Threads share the same virtual address space and virtual to physical address mappings, which introduces data race problems: one thread can try to read the data while another modifies it, leading to inconsistencies|
---
#### Synchronization Mechanisms
To avoid the issues of concurrent execution
|Mechanisms| Basic Idea| Details |
|---|---|--|
|**Mutual  Exclusion** <br> - **mutex** <br> (like a lock)| **Whenever** accessing **shared** data/state among threads: **only one** thread at a time is allowed to access shared data **exclusively** by acquiring a mutex. The other threads (**blocked** threads) will be suspended on the lock operation until the mutex owner **releases** the mutex.| - the mutex should have at least the following information: <br> lock status (lock?), <br> owner, <br> blocked threads (list). <br> - The portion of the code protected by the mutex is called the **critical section**. <br> - Common thread API: <br> **lock(m)** <br> // critical section <br> **unlock(m)** |
|**Condition Variable**| a thread is waiting on other threads with specific condition before processding|
----





### Thread Creation
#### 
|data structure and mechanisms| name | details|
|--|--|--|
|thread data structure|thread type|all the info to **represent** a thread, including:  <br> Thread ID, Program counter, Stack pointer, Register values, Stack, Other thread specific attributes (e.g., for thread management)|
|**create** a thread|parent thread call **Fork(proc, args)**| two arguments: <br> - proc: the procedure that created thread will start executing <br> - args: arguments for the procedure proc. Note that: It is not the UNIX fork. <br> <br> When one thread (parent thread $T_0$) calls fork, a new thread (child thread $T_1$) is created with a new thread data structure (its fields are initialized such that its program counter pointing to the first instructure of the procedure proc and the arguments will be avilable on the stack of the thread). When the thread finishes, store the results of computation in the shared address space and use mechanisms to notify the parent or other threads. |
|**terminate** a thread|parent thread call **Join (child thread ID)**| The parent thread will be **blocked** until the child completes. Join will return to the parent the result of the child's computation. At that point,child thread exits the system and all the resources allocated for child will be freed.
---


Figure: Thread creation and termination
![thread creation](figures/os-thread-creation.png)


Figure: Thread creation example: insert element to a shared link list
![thread creation](figures/os-thread-creation-example.png)
Note: data race: because we do not know which thread will run at which time, we cannot be certain of the ordering of the elements in the shared list. Perhaps the child thread inserts its element before the parent thread, or perhaps the parent thread inserts first. 

Figure: data race example: insert element to a shared link list -> overwriting
![thread creation](figures/os-thread-data-race-example.png)
If multiple threads running concurrently, the operations are randomly interleaved. Only one element will be ultimately successfully linked to the list; the other one will be lost.

