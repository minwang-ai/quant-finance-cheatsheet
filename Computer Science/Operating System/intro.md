## Operating Systems 

### What is an Operating System?

| Item | Definition |
|---|---|
| higher level Applications | - laptop/desktop/phone: browser, editor, messaging, music apps etc <br> - datacenter: web server, database, simulation|
| Operating System (OS) | Software layer **between apps and hardware** to **abstract** complex hardware and **manage** hardware resources (**arbitration**). <br> Elements:  file system, device driver, CPU scheduler etc <br> Visual **metaphor**: **shop manager** (allocates resources, schedules work, enforces rules). |
| Hardware | - Central Processing Units (CPUs) <br> - Physical Memory <br> - Network Interconnects (Ethernet port/Wifi Card) <br> - Graphic Processing Units (GPU) <br> - Storage Devices (hard Disk, SSDs, Flash drives [USB]) |

![OS sits between apps and hardware](figures/os-what-is-os.png)

---


#### Main functions of OS

| Function | What it means | Quick example |
|---|---|---|
| **Hide hardware complexity** | **Directly** has privileged **access** to the underlying hardware and provide simpler abstractions than raw devices to apps | - Support different types of devices <br> - File abstraction instead of a block of disk storage: `read`/`write` <br> - Internet Socket abstraction instead of bits and packets: `send/receive` |
| **Allocate, Manage resources** | Manages hardware on behalf of applications according to some predefined **policies**. Decide how many and which resources will the app use, e.g., CPU, memory, IO | - allocates memory for applications <br> - schedules apps for execution on the CPU <br> -controls access to various devices and so on |
| **Isolation & protection** | Ensures that **applications** are isolated and prevent concurrent apps from harming each other | - Allocate each apps different parts of underlying phycial memory <br> - Make sure one application can’t read/write another’s memory |

#### Examples of OS
| Category| Examples |
|---|---|
| Desktop | - Microsoft Windows <br> - Unix-based : Mac OS X (extend BCD),   Linux|
| Embedded | Android, iOS, Symbian |
| Server||




### OS elements: abstraction vs mechanism vs policy

| Term | Meaning | Examples |
|---|---|---|
| Abstraction | “What” interface you program against | - For applications: Process/thread; <br> - For hardware: file (storage), socket (network card), memory page (phycial memory)|
| Mechanism | “How” the OS performs operations on abstractions | - Create/schedule process/thread to run on CPU; <br> - open/read/write/allocate hardware resources |
| Policy | "How"he mechanisms will be used to manage the underlying hardware | - The max number of sockets an application can access <br> - Which data can be removed from memory: <br> - Page replacement: Least-recently used (LRU) / earliest deadline first (EDF)  |

Memory example (compact):

| Component | In memory management |
|---|---|
| Abstraction | Memory page (fixed-size addressable region) of memory|
| Mechanisms | - Allocate page in DRAM <br> - map the memory page into a process addres to allow the process access the actual physical memory  <br>- move pages from DRAM to disk accorrding to polices (**swapping**). |
| Policy | The **Least recently used** (LRU)  (unimportant, likely not useful in future) memory page will be copied in disk <br> The frequently/currently used are more important (we might contineu to use them) so we metain them in memory since it is faster to access memory than disk.|

![OS sits between apps and hardware](figures/os-memory-manage.png)




### Design principles

| Principle | Why it matters |
|---|---|
| Separate mechanism from policy | Keep mechanisms flexible so different policies can be swapped (LRU vs LFU vs random) |
| Optimize for the common case | Pick policies that match expected workloads and usage patterns |

### Protection boundary: user vs kernel

| Concept | Key point |
|---|---|
| User mode (unprivileged) | Normal applications run here; cannot directly access hardware |
| Kernel mode (privileged) | OS runs here; can execute privileged instructions and access devices |
| System calls | Controlled entry points from user → kernel (requested services) |
| Traps | CPU-enforced transfer to OS on illegal/privileged action in user mode (OS decides: allow/deny/terminate) |
| Signals/notifications | OS-to-process notifications (asynchronous events) |

Common system call examples:

| Area | Example calls |
|---|---|
| Files | `open`, `read`, `write` |
| Networking | `send`, `recv` |
| Memory | `mmap` |

System call flow (one-liner): process calls into kernel → OS does privileged work → returns to the same process (user → kernel → user); this transition has overhead.

### OS services (what the OS “provides”)

| Service | Typical responsibility | Related hardware |
|---|---|---|
| Process management | Create/terminate processes; schedule CPU | CPU |
| Memory management | Allocate/translate/protect memory | DRAM/MMU |
| File management | Naming, permissions, persistence, buffering | Storage devices |
| Device management | Drivers; device access control | Peripherals |
| Storage management | Block I/O, caching, scheduling | Disk/flash |
| Security | Auth, access control, isolation | Cross-cutting |
| Filesystem (as a service) | Higher-level abstraction built on storage | Not a single device |

### OS organization (kernel designs)

| Design | What it looks like | Pros | Cons |
|---|---|---|---|
| Monolithic | Most services/drivers inside kernel | Fast calls; inlining/optimizations | Large, less customizable; harder to port/manage; bigger memory footprint |
| Modular | Core kernel + loadable modules | Maintainable; smaller base footprint; add features dynamically | Indirection can reduce optimization opportunities; module compatibility/maintenance issues |
| Microkernel | Minimal kernel; many services in user space using IPC | Small; verifiable (common in embedded) | IPC + frequent user/kernel crossings can be expensive; often hardware-specific |

### Example architectures (very high-level)

| System | Layering (rough) | Notes |
|---|---|---|
| Linux | Hardware → Linux kernel → standard libraries (syscall interface) → utilities (shell/toolchain) → user apps | Kernel has components like virtual file system, memory management, process management; often supports modular replacement |
| macOS (OS X) | Hardware → (Mach + BSD + I/O frameworks) → user space | Includes I/O Kit + kernel extension support; Mach provides primitives (e.g., threads/scheduling/IPC), BSD provides POSIX + networking |