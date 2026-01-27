## Threads
|Threads||
|--|--|
|visual **metaphor**|**worker** at a shop <br> - active entity: executing unit of a process <br> - works simultaneously with others threads  <br> - requires coordination - sharing of I/O devices, CPUs, memory
|**Benefits** of **Multithreading** <br> (in multi-core/multi processor system)| - Each thread executes same code but for different subset of **input** (e.g., a matrix)in **parallel** **concurrently** on a different processor to **speed up** <br> - Each thread executes different portions of program for special **tasks** to set **prioirty** differently and get **performance gain** by **hot cache** |
|why **multithreading** instead of **multiprocess**?| - **lower memory requirement**: A **multiprocess** application requires **more memory** => more swaps from disk (we have to allocate each process a address space, and a executation context) while <br>  a **multi-threaded** application requires **less memory** (sharing address space). <br> - **lower communication overhead**: communicating, passing, synchronizing data among processes (requires **inter process communication IPC**) is more **costly** than **inter thread communication**(**shared variables** in the same process address space)|
----
Figure: Multi-Process requires more memory!
![Multi-Process](figures/os-multi-process.png)

## Process vs. Thread
|Single thread Process | Multi Thread Process|
|--|---|
A single-thread process is represented by <br> - its [**address space**](process%20management.md#process-address-space-and-memory-management) (virtual - physical memory mapping) and <br> - its **execation context** (stack pointer, register, program counter etc). |Threads represent multiple **independent** execution contexts. <br> - **shared info**: They are within the **same virtual address space**, which means they share the virtual to physical address mapping, and the code/data/files.<br> - **Per-thread info** (in a seperate data structure): Threads will potentially execute **different** **instructions** and accessing different portions of the **address space**, operate on different portions of the **input** etc. This means that each thread will have to have its own different **program counter, stack stack, pointer, thread-specific registers**.|
<br> OS represents  all the information in a [process control block (PCB)](process%20management.md#process-control-block). | More complex PCB: <br> - shared virtual address mapping, code,data <br> - per-thread executaion context.|
----

Figure: Multi-Threads
![Multi-Threads](figures/os-multi-threads.png)

Figure: Single thread Process vs. Multi Thread Process
![Process vs. Thread](figures/os-process-vs-thread.png)

















