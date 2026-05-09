# Operating Systems
## Complete Topic Explanations — Exam Preparation Guide

---

# CHAPTER 1: Introduction to Operating Systems

## What an Operating System Actually Does

An operating system is the most fundamental piece of software on a computer. Every other program — whether it is a web browser, a game, or a word processor — runs on top of the operating system and depends on it entirely. Without an operating system, application software would have to directly manage every hardware component on the machine: the processor, memory chips, storage disks, network cards, keyboards, and displays. That would make writing any application enormously complex and completely non-portable — software written for one machine would not run on any other.

The operating system solves this by acting as an intermediary layer between hardware and software. It hides the messy, low-level details of hardware from application programs, presenting instead a clean, consistent set of services that any program can use. This is why you can write a Python program that reads a file without knowing whether the hard drive is a spinning magnetic disk or a solid-state drive — the OS handles the difference.

Beyond abstraction, the OS is also a resource manager. At any moment, dozens of programs may want to use the CPU, read from memory, write to disk, and send data over the network. The OS allocates these resources, enforces boundaries between programs so they cannot accidentally or maliciously interfere with each other, and ensures that no single program monopolizes resources at the expense of others.

## Goals of an Operating System

Two goals sometimes pull in opposite directions. The first goal is convenience — making the computer easy to use. A well-designed OS shields users and programmers from hardware complexity. The second goal is efficiency — making the best possible use of hardware resources. Sometimes maximizing efficiency requires allowing complexity that reduces convenience. A well-designed OS balances these goals depending on its intended environment: a phone OS prioritizes battery efficiency and touch-friendly interaction; a server OS prioritizes throughput and stability.

## Types of Operating Systems

Operating systems are designed for specific environments, and the design reflects those environments completely.

**Batch Operating Systems** were the earliest type. Users submitted jobs — programs and their data — and the OS ran them one after another without user interaction. Throughput was the only metric that mattered. There was no interactive response because humans were not sitting at the machine while it ran.

**Time-Sharing Operating Systems** allowed multiple users to interact with the computer simultaneously. The OS rapidly switches between users, giving each the illusion of having the machine to themselves. Response time matters here — users expect quick feedback when they type a command.

**Real-Time Operating Systems (RTOS)** are designed for environments where missing a deadline is not just inconvenient but potentially catastrophic. An airbag control system must respond within milliseconds. A nuclear reactor control system must process sensor data within strict time windows. RTOS designs prioritize guaranteed response times over throughput or fairness.

**Distributed Operating Systems** manage a collection of independent computers, presenting them to users as a single coherent system. The individual machines may be in the same room or on different continents. Resource sharing, fault tolerance, and communication are the central design challenges.

**Mobile Operating Systems** — iOS, Android — are designed for battery-powered devices with touch interfaces, limited memory, and intermittent network connectivity. They manage power consumption aggressively and prioritize responsiveness.

**Embedded Operating Systems** run inside devices that are not general-purpose computers: smart TVs, washing machines, medical monitors. They are typically small, efficient, and highly specialized.

---

# CHAPTER 2: Operating System Structure

## Kernel and User Space

The most important architectural division in any operating system is between the kernel and user space. The kernel is the core of the OS — the part that runs with full hardware privileges and has direct access to all resources. User space is where application programs run — they have restricted privileges and must request services from the kernel through a defined interface called the system call interface.

This separation is not just organizational — it is enforced by hardware. Modern processors run in at least two modes: kernel mode (also called supervisor or privileged mode) and user mode. In kernel mode, any instruction is allowed, including those that directly control hardware. In user mode, certain instructions are forbidden. If a user-mode program tries to execute a privileged instruction, the hardware generates an exception and the OS terminates the offending program. This is how one misbehaving program cannot crash the entire system — it simply cannot issue instructions that would harm other programs or the kernel.

## System Calls

A system call is the mechanism through which a user-space program requests a service from the kernel. When your program calls `fopen()` to open a file, eventually that call translates into a system call that crosses the kernel/user-space boundary. The processor switches from user mode to kernel mode, the kernel performs the requested operation, and then control returns to the user program in user mode.

System calls are grouped by what they do:

- **Process management** — creating processes (`fork`), executing programs (`exec`), terminating processes (`exit`), waiting for a child process to finish (`wait`)
- **File management** — opening, reading, writing, closing, deleting files
- **Device management** — requesting and releasing device access, reading and writing devices
- **Memory management** — allocating and freeing memory
- **Communication** — creating pipes, sending messages between processes
- **Information** — getting system time, getting process attributes

## Monolithic, Microkernel, and Layered Designs

Different OS architectures reflect different trade-offs between performance and modularity.

In a **monolithic kernel**, all OS services — memory management, file systems, device drivers, networking, scheduling — run together in a single large program in kernel space. Linux and traditional Unix are monolithic. The advantage is performance: components communicate by calling functions directly, which is fast. The disadvantage is fragility — a bug in any driver can crash the entire kernel.

In a **microkernel**, only the most fundamental services run in kernel space: basic IPC (inter-process communication), minimal memory management, and basic scheduling. Everything else — file systems, device drivers, networking — runs as user-space processes called servers. If a driver crashes, only that server process dies; the kernel and other programs continue. The Mach microkernel and QNX follow this design. The disadvantage is performance overhead: what would be a direct function call in a monolithic kernel becomes a message exchange between processes.

A **layered OS** organizes the system into hierarchical layers, each built on the layer below it. Layer 0 is hardware; the top layer is the user interface. Each layer only communicates with the layer directly below it. This produces clean design but is rarely used in practice because many OS functions do not fit neatly into a strict hierarchy.

## Operating System Services

An OS provides services that fall into two categories: those that benefit the user directly, and those that ensure the system operates correctly.

Services directly helpful to users include program execution (loading, running, and terminating programs), I/O operations (accessing files and devices), file system manipulation (creating, deleting, reading, writing files and directories), communications (between processes and between computers), and error detection (reporting hardware and software errors).

Services that maintain system integrity include resource allocation (distributing CPU time, memory, and I/O among competing processes), accounting (tracking who uses what resources), and protection and security (ensuring processes cannot interfere with each other and unauthorized users cannot access the system).

---

# CHAPTER 3: Processes

## What a Process Is

A program and a process are not the same thing, and understanding the difference is fundamental. A program is a passive entity — a file of instructions stored on disk. A process is a program in execution — it is active, it has a current instruction being executed, registers holding working values, a stack holding function call information, and heap memory holding dynamically allocated data. Two simultaneous executions of the same program are two separate processes, each with their own state.

Every process has an address space — the range of memory addresses it can use. Modern operating systems give each process the illusion that it owns the entire memory of the machine, through a technique called virtual memory. In reality, its memory may be scattered across physical RAM and may include parts that are currently stored on disk.

## Process States

A process moves through states during its lifetime. Understanding these states is essential to understanding how the OS manages the CPU.

**New** — the process is being created. Its data structures are being set up.

**Ready** — the process is loaded into memory and waiting for the CPU. It is fully prepared to execute; it just needs to be given the processor.

**Running** — the process is currently executing instructions on the CPU. On a single-core system, only one process can be in this state at a time.

**Waiting (Blocked)** — the process is waiting for something to happen before it can continue. It might be waiting for a file to finish reading, a network packet to arrive, or a timer to expire. While waiting, it makes no use of the CPU and should not take it from processes that are ready to run.

**Terminated** — the process has finished executing and is being cleaned up.

The OS manages these state transitions. The **scheduler** decides which ready process gets the CPU next. A process moves from running to waiting when it requests an I/O operation. It moves from waiting to ready when the I/O completes. It moves from running to ready when its time slice expires.

## Process Control Block (PCB)

The OS maintains a data structure for every process called the Process Control Block (PCB). This is everything the OS needs to know about a process:

- **Process ID (PID)** — a unique number identifying the process
- **Process state** — current state (new, ready, running, waiting, terminated)
- **Program counter** — the address of the next instruction to execute
- **CPU registers** — the contents of all processor registers at last save
- **CPU scheduling information** — priority, scheduling queue pointers
- **Memory management information** — base and limit registers, page tables
- **I/O status information** — list of open files, pending I/O requests
- **Accounting information** — CPU time used, time limits, process number

When the OS switches the CPU from one process to another — a context switch — it saves the running process's PCB and loads the new process's PCB. The CPU registers are restored to the values saved in the new process's PCB, and execution resumes exactly where that process left off.

## Context Switching

A context switch is the mechanism that creates the illusion of simultaneous execution. When the OS decides to stop running process A and start running process B, it must save everything about process A (into A's PCB) and restore everything about process B (from B's PCB). This save-and-restore operation takes time — typically a few microseconds on modern hardware. During a context switch, no useful work is done; it is pure overhead. This is why excessive context switching is a performance problem.

## Process Creation and Termination

In Unix-based systems, processes are created using the `fork()` system call. `fork()` creates a new process — the child — that is an exact copy of the calling process — the parent. Both processes continue executing from the same point in the code after `fork()`, but they can tell each other apart by `fork()`'s return value: it returns 0 in the child and the child's PID in the parent. Typically the child immediately calls `exec()` to replace itself with a different program. This `fork-exec` pattern is how every process on a Unix system is created.

A process terminates by calling `exit()`, or when it receives a signal it cannot handle. When a process terminates, the OS reclaims its resources — memory, open files, and other allocated objects. However, the process's entry in the process table remains until the parent process calls `wait()` to retrieve its exit status. A terminated process whose parent has not yet called `wait()` is called a zombie — it consumes a process table slot but no real resources.

## Inter-Process Communication (IPC)

Processes are isolated by design — one process cannot directly read another's memory. But processes often need to cooperate: a web server needs to pass a request to a worker process; a producer process needs to pass data to a consumer process. Two fundamental IPC mechanisms exist.

**Shared memory** sets up a region of memory that two or more processes can both access. Data written by one process can be read by the other. Shared memory is fast because it involves no kernel intervention after setup — processes communicate at memory speed. The challenge is synchronization: if two processes try to update shared data simultaneously, the result can be corrupted.

**Message passing** has processes send and receive messages through the OS kernel. One process calls `send(message)` and another calls `receive(&message)`. Message passing is simpler to reason about because each message is a complete, discrete communication. The kernel provides the ordering and reliability guarantees. The cost is performance — every message goes through the kernel, adding overhead.

---

# CHAPTER 4: Threads

## Processes vs Threads

A thread is a unit of execution within a process. A traditional process has a single thread of execution — one program counter, one stack, executing one sequence of instructions at a time. A multithreaded process has multiple threads, each with its own program counter and stack, but all sharing the same address space, open files, and other process resources.

The difference matters enormously for performance. Creating a new process is expensive — the OS must set up a completely new address space. Creating a new thread within an existing process is cheap — only a new stack and register set are needed; everything else is shared. Switching between threads of the same process is faster than switching between processes for the same reason.

## Why Use Threads?

Threads are the natural model for programs that need to do multiple things simultaneously. A web server must handle many client requests at once — if it serves requests one at a time, clients queue up and response time degrades. With threads, each request gets its own thread, so hundreds of requests can be in progress simultaneously without any one waiting for others. A word processor uses threads so spell-checking can happen in the background while you continue typing in the foreground. A web browser uses threads so the UI remains responsive while page content is downloading.

Threads also make better use of multicore processors. A single-threaded program uses only one core no matter how many the machine has. A multithreaded program can run different threads on different cores simultaneously, achieving true parallelism and completing work faster.

## User-Level vs Kernel-Level Threads

Threads can be managed either by a library in user space or by the OS kernel.

**User-level threads** are managed entirely by a thread library without kernel involvement. Thread creation, switching, and synchronization are all handled in user space. The kernel sees only a single process and is unaware that multiple threads exist. This makes thread operations very fast — no system calls needed. The critical weakness is that if any thread makes a blocking system call, the kernel blocks the entire process (since it sees only one entity). No other thread in that process can run until the blocking call returns.

**Kernel-level threads** are managed by the OS. The kernel is aware of each thread and can schedule them independently. If one thread blocks, the kernel can schedule another thread from the same process on the same or a different CPU. This provides true parallelism on multicore systems. The cost is that thread operations require system calls, making them slower than user-level operations.

Most modern systems use a hybrid model that maps user-level threads onto kernel-level threads to get the benefits of both.

---

# CHAPTER 5: CPU Scheduling

## The Purpose of Scheduling

On a multiprocessing system with many ready processes, the CPU scheduler must decide which process runs next every time the CPU becomes free. This decision, made hundreds or thousands of times per second, has enormous impact on overall system performance and user experience.

The CPU scheduler deals with short-term scheduling — deciding which of the ready processes gets the CPU now. This is distinct from medium-term scheduling (deciding which processes should be swapped in or out of memory) and long-term scheduling (deciding which new processes should be admitted to the system).

## Scheduling Criteria

No single scheduling algorithm is best for all situations. Different criteria matter for different environments:

- **CPU utilization** — keep the CPU busy as much as possible. In practice, systems target 40–90% utilization.
- **Throughput** — number of processes completed per unit time. Maximize completed work.
- **Turnaround time** — total time from process submission to completion. Minimize time from submission to result.
- **Waiting time** — total time a process spends in the ready queue. Scheduling algorithms directly affect this.
- **Response time** — time from request submission to first response. Critical for interactive systems where users expect immediate feedback.

For batch systems, throughput and turnaround time matter most. For interactive systems, response time and waiting time dominate.

## First-Come, First-Served (FCFS)

FCFS is the simplest scheduling algorithm: processes are served in the order they arrive. It is non-preemptive — once a process starts running, it runs until it either completes or blocks for I/O. The implementation uses a simple queue.

FCFS is fair in the sense that no process waits forever, but it produces poor average waiting times when a long process arrives before several short ones. This is the convoy effect: a long process holds the CPU while short processes — which could have finished quickly — wait behind it. If a 10-second job arrives before three 1-second jobs, the average waiting time is much higher than if the short jobs had gone first.

## Shortest Job First (SJF)

SJF selects the process with the shortest next CPU burst — the period of time the process will run before either completing or blocking. By running short jobs first, SJF minimizes average waiting time. It is provably optimal in this sense — no other algorithm produces a lower average waiting time for a given set of jobs with known burst lengths.

The practical problem with SJF is that the OS cannot know in advance how long each process's next CPU burst will be. The common solution is to predict burst length based on past behavior using exponential averaging — a weighted average of the process's recent burst lengths. Processes that have historically had short bursts are predicted to have short bursts again.

SJF can be non-preemptive or preemptive. The preemptive version — called Shortest Remaining Time First (SRTF) — preempts the running process whenever a new process arrives with a shorter remaining burst. SRTF gives even lower average waiting times but can cause starvation: a long process may never run if a steady stream of short processes keeps arriving.

## Priority Scheduling

Each process is assigned a priority, and the scheduler always runs the highest-priority ready process. Priority can be assigned based on process type (system processes over user processes), payment, age, or any other criterion.

Priority scheduling suffers from **starvation** — low-priority processes may wait indefinitely if high-priority processes keep arriving. The solution is **aging**: gradually increase the priority of a waiting process over time. A process that has waited long enough eventually becomes high-priority and gets scheduled.

## Round Robin (RR)

Round Robin is designed specifically for time-sharing systems where every user expects reasonably prompt responses. Each process is assigned a time quantum — a fixed slice of CPU time, typically 10–100 milliseconds. The scheduler maintains a circular queue of ready processes. Each process runs for one quantum, and then the next process in the queue gets the CPU. If a process's burst is shorter than the quantum, it voluntarily releases the CPU when done. If it still has work remaining when its quantum expires, it is preempted and placed at the back of the queue.

The key trade-off is the size of the quantum. A very large quantum degenerates into FCFS. A very small quantum produces excellent response time but excessive context switches dominate — the overhead of saving and restoring registers thousands of times per second wastes CPU time that could be doing useful work. In practice, context switch time is around 10 microseconds, so a quantum of 10–100 milliseconds keeps the overhead at an acceptable 1–10%.

## Multilevel Queue Scheduling

Real systems typically have different types of processes with fundamentally different requirements. Foreground (interactive) processes need fast response; background (batch) processes need throughput. A multilevel queue divides the ready queue into separate queues for different process categories, with each queue having its own scheduling algorithm. A strict priority exists between queues — foreground queue processes are always served before background queue processes — but starvation of lower-priority queues is a concern.

**Multilevel Feedback Queue** scheduling addresses this by allowing processes to move between queues. A new process starts in a high-priority queue with a short quantum. If it uses its full quantum without finishing, it moves to the next lower-priority queue with a longer quantum. Processes that use the CPU briefly and voluntarily (interactive programs) remain in high-priority queues. Long-running CPU-bound processes naturally migrate to lower-priority queues where they get longer but less frequent time slices. This self-adjusting behavior requires choosing the number of queues, the scheduling algorithm for each, and the criteria for promotion and demotion — which is why it is the most complex but also the most flexible and practical algorithm.

---

# CHAPTER 6: Process Synchronization

## The Critical Section Problem

When multiple processes or threads share data and execute concurrently, a fundamental problem emerges. Suppose two processes both try to increment a shared counter. The operation "increment counter" looks atomic — one step — but at the machine level it involves three steps: read the value into a register, add one to the register, write the result back. If both processes read the value before either writes back, both write the same incremented value and one increment is lost.

The section of code that accesses shared data is called the **critical section**. If two processes can be in their critical sections simultaneously, data corruption can result. This is called a race condition — the outcome depends on the precise timing of execution, which is unpredictable.

A correct solution to the critical section problem must satisfy three requirements:

- **Mutual exclusion** — only one process at a time may be in its critical section
- **Progress** — if no process is in its critical section, the selection of which waiting process enters next cannot be postponed indefinitely
- **Bounded waiting** — there must be a limit on how many times other processes can enter the critical section before a waiting process is granted entry

## Mutex Locks and Semaphores

A **mutex lock** (mutual exclusion lock) is the simplest synchronization tool. Before entering a critical section, a process acquires the lock. After leaving, it releases the lock. If another process tries to acquire an already-held lock, it is blocked until the lock is released. The semantics are simple: the lock is either held by exactly one process, or it is free.

A **semaphore** is a generalization. It is an integer variable accessed only through two atomic operations: `wait()` (also written P) and `signal()` (also written V). `wait()` decrements the semaphore; if the result is negative, the calling process is blocked. `signal()` increments the semaphore; if there are blocked processes, one is awakened.

A binary semaphore (value 0 or 1) behaves like a mutex. A counting semaphore with an initial value of n allows up to n processes to be in their critical sections simultaneously — useful for managing a pool of n identical resources.

## Classic Synchronization Problems

Three classic problems appear in every OS course because they illuminate the challenges of synchronization.

**The Producer-Consumer Problem** (also called Bounded Buffer) involves a producer that generates data and places it in a shared buffer, and a consumer that removes and processes data from the buffer. The buffer holds at most n items. The producer must wait if the buffer is full; the consumer must wait if the buffer is empty. Three semaphores manage this: `mutex` for mutual exclusion on buffer access, `empty` (initialized to n) counting empty slots, and `full` (initialized to 0) counting filled slots.

**The Readers-Writers Problem** involves a shared data structure accessed by readers (who only read) and writers (who modify). Multiple readers can safely access simultaneously, but a writer needs exclusive access. The challenge is allowing as much concurrent reading as possible while ensuring writers can eventually access the data. Naïve solutions either favor readers (writers can starve) or favor writers (readers can starve).

**The Dining Philosophers Problem** involves five philosophers sitting at a round table, each needing two forks (one on each side) to eat, but only five forks total. This models the problem of allocating multiple resources among multiple processes without deadlock. If all philosophers simultaneously pick up the fork on their left, none can pick up the fork on their right, and all wait forever — a deadlock.

## Deadlock

A deadlock is a situation where a set of processes are all waiting for resources held by other processes in the same set — so none can ever proceed. Four conditions must all hold simultaneously for a deadlock to occur:

- **Mutual exclusion** — at least one resource is held in a non-shareable mode
- **Hold and wait** — a process holds at least one resource while waiting for more
- **No preemption** — resources cannot be forcibly taken from a process
- **Circular wait** — a circular chain of processes exists, each waiting for a resource held by the next

These four conditions, known as the Coffman conditions, are important because deadlock prevention strategies work by ensuring at least one condition cannot hold.

Deadlock handling strategies take different approaches. **Prevention** designs the system so one Coffman condition can never hold. **Avoidance** dynamically examines resource allocation requests and grants them only when the system is guaranteed to stay in a safe state — the Banker's Algorithm is the classic avoidance algorithm. **Detection and recovery** allows deadlocks to occur, detects them using a resource allocation graph or wait-for graph, then recovers by terminating processes or preempting resources. **Ignorance** (the ostrich algorithm) simply ignores the problem — if deadlocks are rare enough, the cost of prevention or detection may exceed the cost of occasional reboots. Surprisingly, this is what most general-purpose operating systems actually do.

---

# CHAPTER 7: Memory Management

## Why Memory Management is Necessary

Every process needs memory to run — for its code, data, and stack. Memory is finite. If 20 processes are running and together they need more memory than physically exists, the OS must decide what to do. Memory management is the part of the OS that decides how memory is allocated among competing processes, ensures processes cannot access each other's memory (protection), and provides the abstraction of a large, private address space to each process (virtual memory).

## Contiguous Memory Allocation

In the simplest approach, each process is allocated a single contiguous block of physical memory. This requires two fundamental protections: a base register holding the starting address of the process's memory region, and a limit register holding the size of the region. Every memory access by the process is checked by hardware: the address must be greater than or equal to the base and less than base plus limit. Violations cause a hardware exception.

When processes terminate, they leave gaps — holes — in physical memory. Over time, memory becomes fragmented: there may be plenty of total free memory, but no single contiguous block large enough for a new process. This is **external fragmentation**. Three strategies exist for allocating a process to a hole: first-fit (allocate the first hole that is big enough), best-fit (allocate the smallest hole that is big enough), and worst-fit (allocate the largest hole). First-fit and best-fit both outperform worst-fit in practice, but all three suffer from fragmentation.

**Compaction** — moving all processes to one end of memory to consolidate free space — solves fragmentation but is expensive: it requires stopping every process while memory is shuffled around.

## Segmentation

Segmentation provides the programmer's view of memory: a program consists of logical segments — code, data, stack, heap. Each segment is a variable-length unit that can be of different sizes. The logical address consists of a segment number and an offset within that segment. A segment table maps each segment to its physical base address and length.

Segmentation allows each segment to grow and shrink independently. The stack grows down as function calls nest; the heap grows up as memory is dynamically allocated. But segments are still contiguous in physical memory, so external fragmentation remains.

## Paging

Paging eliminates external fragmentation by abandoning the requirement for contiguous physical memory. Physical memory is divided into fixed-size blocks called **frames**. A process's logical address space is divided into same-size blocks called **pages**. Any page can be placed in any free frame — they do not need to be adjacent.

Every process has a **page table** mapping its logical page numbers to physical frame numbers. A logical address consists of two parts: a page number (used as an index into the page table to find the frame number) and a page offset (added to the frame number to get the physical address).

Paging introduces **internal fragmentation**: a process's last page may not fill its frame completely, wasting the remaining space. But this waste — at most one frame per process — is far less damaging than external fragmentation.

The major overhead of paging is that every memory access requires two physical memory accesses: one to the page table (to look up the frame number) and one to the actual data. This would halve performance. The solution is a **Translation Lookaside Buffer (TLB)** — a small, fast cache of recent page-to-frame mappings in hardware. If the desired mapping is in the TLB (a hit), no page table lookup is needed. TLB hit rates of 99% and higher are typical, making the overhead negligible.

## Virtual Memory

Virtual memory takes paging further by allowing a process's address space to be larger than physical memory. Not all pages need to be in physical memory simultaneously — only the pages currently being used need to be resident. Pages that are not in memory are stored on disk (in a swap space or page file).

When a process accesses a page that is not in memory, the hardware generates a **page fault**. The OS handles the page fault by:

1. Finding the required page on disk
2. Finding a free frame in physical memory (or freeing one using a page replacement algorithm)
3. Loading the page from disk into the frame
4. Updating the page table
5. Restarting the instruction that caused the fault

Page faults are expensive — disk access takes millions of times longer than memory access. The goal is to minimize page fault rates.

## Page Replacement Algorithms

When a page fault occurs and no free frame is available, the OS must choose a victim frame to evict to disk. The choice matters enormously for performance.

**FIFO (First-In, First-Out)** evicts the oldest page — the one that has been in memory longest. It is simple to implement but performs poorly: an old page might be heavily used, and evicting it causes an immediate page fault.

**Optimal (OPT)** replaces the page that will not be used for the longest time in the future. This produces the minimum possible page fault rate — it is the theoretical ideal. It cannot be implemented in practice because the OS cannot know the future, but it serves as a benchmark for evaluating real algorithms.

**Least Recently Used (LRU)** replaces the page that has not been used for the longest time. Based on the principle of temporal locality — pages used recently are likely to be used again soon — LRU approximates OPT closely and is widely used. Exact LRU requires hardware support to timestamp every memory access, which is expensive. Approximations using reference bits are used in practice.

## Thrashing

Thrashing occurs when a process spends more time handling page faults than executing instructions. If a process does not have enough frames to hold its working set — the set of pages it actively uses — it generates page faults nearly every instruction. Bringing in a page requires evicting another page, which is then needed immediately, causing another fault. The process makes no progress.

At the system level, thrashing creates a vicious cycle. The CPU utilization drops (processes are all waiting for pages), the scheduler adds more processes to improve CPU utilization, but more processes means fewer frames per process, causing more thrashing, causing CPU utilization to drop further. The solution is working set model management — ensuring each process has enough frames to hold its working set — and load control: reducing the degree of multiprogramming when thrashing is detected.

---

# CHAPTER 8: File Systems

## What a File System Provides

A file system provides a structured, named, persistent storage abstraction on top of raw storage devices. Without a file system, programs would have to work with raw disk blocks — block 0, block 1, block 2 — with no organization, naming, or protection. The file system provides:

- Named files and hierarchical directories
- Access control — determining who can read, write, or execute each file
- Space management — tracking which disk blocks are free and which are occupied
- Persistence — ensuring data survives power failures

## File Concepts and Attributes

A file is a named collection of related information recorded on secondary storage. Files have both data content and attributes — metadata the OS maintains about the file:

- **Name** — human-readable identifier
- **Identifier** — unique number used internally by the file system (inode number in Unix)
- **Type** — text, binary, executable, directory
- **Location** — pointer to the file's data on disk
- **Size** — current size in bytes
- **Protection** — access control information
- **Timestamps** — creation time, last modified time, last accessed time
- **Owner** — user ID of the file's owner

## File Operations

The OS provides a set of system calls for file operations. The most important sequence is:

1. `open()` — locate the file on disk, verify access permissions, and create an entry in the OS's open file table. Returns a file descriptor — a small integer used for subsequent operations.
2. `read()` — transfer data from the file into a buffer in memory
3. `write()` — transfer data from a memory buffer to the file
4. `seek()` (or `lseek()`) — move the file position pointer to a different location for random access
5. `close()` — remove the entry from the open file table and flush any buffered writes to disk

The open file table is a kernel data structure with one entry per open file per process, storing the file's current position, access mode, and a reference count.

## Directory Structure

Directories are special files that map file names to their attributes (or to inode numbers that lead to attributes). Directory structures have evolved from simple flat designs to hierarchical trees.

A **single-level directory** puts all files in one directory. Simple but impractical — file names must all be unique across all users, and finding files in a large collection is difficult.

A **two-level directory** gives each user their own directory. Solves the naming conflict between users but limits organization within each user's space.

A **tree-structured directory** (hierarchical) allows arbitrary depth — directories containing files and other directories. This is the model used by all modern operating systems: Unix, Windows, macOS. The root directory (`/` in Unix, `C:\` in Windows) is at the top; any path from root to a file uniquely identifies it.

An **acyclic graph directory** allows files and directories to have multiple parent directories — a file or directory can appear in multiple places. Unix hard links and Windows shortcuts implement this concept. Care must be taken to avoid dangling references when files are deleted.

## File Allocation Methods

How the OS stores file data on disk is a critical design decision affecting performance and space utilization.

**Contiguous allocation** stores each file in a contiguous run of disk blocks. This enables excellent sequential read performance — a single disk seek positions the head at the start of the file, and the rest is read without seeking. It also supports efficient direct access: to read block n of a file, seek directly to the file's start plus n. The fatal weakness is external fragmentation — over time, free space becomes fragmented into small non-contiguous pieces, making it impossible to allocate large contiguous regions for new files.

**Linked allocation** stores each file as a linked list of disk blocks that can be scattered anywhere on disk. Each block contains a pointer to the next block. This eliminates external fragmentation — any free block can be used. But sequential access requires following the chain, which can involve many seeks. Direct access is terrible — to read block n, you must follow n pointers from the start. The FAT (File Allocation Table) file system used in Windows and USB drives stores all the next-pointers in a table in memory rather than in the blocks themselves, which improves performance significantly.

**Indexed allocation** gives each file an index block containing an array of pointers to its data blocks. The index block is itself stored on disk. This supports both sequential and direct access efficiently — to read block n, index into the index block at position n to find the data block's address. The challenge is that the index block has fixed size, limiting the maximum file size. Multi-level indexing (index blocks pointing to other index blocks) extends the maximum file size dramatically. Unix i-nodes use a combination of direct pointers, single indirect, double indirect, and triple indirect blocks to support files ranging from tiny to enormous.

## Free Space Management

The file system must track which disk blocks are free for allocation. Two common approaches:

A **free-space bitmap** (or bit vector) has one bit per disk block: 0 means free, 1 means occupied (or vice versa). Finding a contiguous free region is efficient with bit manipulation. The bitmap for a large disk can be cached entirely in memory.

A **free list** links all free blocks into a linked list. Traversing the list is the only way to find free blocks, which is slow. But if blocks are allocated and freed one at a time, only the head of the list is ever accessed, making it fast in practice.

---

# CHAPTER 9: I/O Systems

## The I/O Challenge

I/O devices are extraordinarily diverse — keyboards, mice, monitors, disks, USB drives, network cards, printers, cameras — and each communicates with the CPU in fundamentally different ways. The OS must provide a unified abstraction over this diversity while managing the enormous difference in speed between CPU operations (nanoseconds) and I/O operations (milliseconds for disk, even longer for human input).

## I/O Hardware Concepts

Every I/O device connects to the CPU through a **device controller** — hardware that manages the device and presents a simplified interface to software. The CPU communicates with controllers through **I/O ports** (addresses in a special I/O address space) or **memory-mapped I/O** (device registers mapped to regular memory addresses, accessed with normal load and store instructions).

A controller has registers that the CPU reads and writes to command the device and check its status:

- **Status register** — indicates whether the device is idle, busy, or has completed an operation
- **Command register** — written by the CPU to start operations
- **Data register** — holds data being transferred to or from the device

## Polling, Interrupts, and DMA

Three mechanisms exist for managing when and how the CPU interacts with I/O operations.

**Polling** (busy waiting) has the CPU continuously check the device's status register in a loop until the operation completes. It is simple and has very low latency for fast devices, but wastes enormous CPU time for slow operations — the CPU is spinning in a loop doing no useful work.

**Interrupt-driven I/O** frees the CPU during the operation. The CPU starts the I/O operation, then continues executing other processes. When the device finishes, it sends an electrical signal — an interrupt — to the CPU. The CPU pauses its current work, executes an interrupt service routine (ISR) that handles the completion, then resumes what it was doing. Interrupts are efficient for slow devices because the CPU is freed to do useful work during the wait.

**Direct Memory Access (DMA)** takes interrupt-driven I/O further by removing the CPU from the data transfer entirely. Instead of reading data word by word from the device and writing it to memory, the CPU programs a DMA controller with the source (device), destination (memory address), and size of the transfer. The DMA controller manages the entire transfer, communicating directly with the device and writing directly to memory. When finished, it interrupts the CPU. DMA is essential for high-speed devices like disk controllers and network cards where transferring data word-by-word through the CPU would saturate it.

## Device Drivers and the I/O Subsystem

A device driver is a software module — typically part of the kernel — that knows how to communicate with a specific device controller. When the OS needs to read data from a disk, it calls the disk driver, which translates the abstract "read block n" request into the exact sequence of commands, status checks, and data transfers that the specific controller understands.

Drivers present a uniform interface upward (to the rest of the OS) and a device-specific interface downward (to the hardware). This is what allows the OS to treat all keyboards the same, all disks the same, and all network cards the same at the application level — the driver layer handles the differences.

The I/O subsystem handles several higher-level concerns:

**Buffering** stores data temporarily while it is being transferred. A buffer between a fast device and a slow one prevents the fast device from overrunning the slow one. Double buffering — using two buffers alternately — allows one buffer to be transferred to its destination while the other is being filled, hiding latency.

**Caching** keeps copies of frequently used data in faster storage. The buffer cache in an OS holds recently accessed disk blocks in memory — if the same block is read again, the memory copy is returned instead of going to disk again. Disk caching can improve I/O performance by orders of magnitude for workloads with good locality.

**Spooling** is a buffer for devices that cannot interleave data from multiple processes. A printer cannot switch between two print jobs in the middle — it must finish one before starting another. The spooler accepts print jobs from all processes into a queue on disk, then sends them to the printer one at a time.

## Disk Scheduling

Disk access time has three components: seek time (moving the read/write head to the right track), rotational latency (waiting for the right sector to rotate under the head), and transfer time (actually transferring the data). Seek time dominates — it can be many milliseconds, while transfer time for a few kilobytes is microseconds. Disk scheduling algorithms minimize total seek time across a queue of pending requests.

**FCFS** serves disk requests in arrival order — simple but can produce wild head movements if requests are scattered across the disk.

**SSTF (Shortest Seek Time First)** always serves the request closest to the current head position. This minimizes total head movement but can cause starvation of requests at the far edges of the disk if middle requests keep arriving.

**SCAN (Elevator algorithm)** moves the head from one end of the disk to the other, servicing all requests encountered along the way, then reverses direction. Like an elevator — it goes up servicing floors, reaches the top, then goes down. All requests are eventually served.

**C-SCAN (Circular SCAN)** improves on SCAN by only servicing requests in one direction. When the head reaches one end, it immediately returns to the beginning without servicing requests on the return trip. This provides more uniform wait times because requests at the far end are not effectively twice as far as requests near the starting end.

---

# CHAPTER 10: Security and Protection

## Protection vs Security

These two terms are related but distinct. **Protection** refers to mechanisms that control which processes and users can access which resources within the system. It is about internal access control — enforcing the rules the system defines. **Security** refers to protecting the system from external threats — unauthorized users, malicious programs, and attacks from the network.

Both are essential. Protection without security means you have careful internal access control but the system can be broken into from outside. Security without protection means the system might resist external attacks but once inside, any process can do anything.

## Goals of Protection

A protection system exists to serve several goals. It prevents processes from interfering with each other's data. It prevents processes from accessing hardware directly (that is the OS's job). It ensures that a process can only access resources it has been explicitly authorized to use. It provides the mechanisms through which administrators can define and enforce access policies.

Protection is a mechanism, not a policy. The OS provides the tools — access control lists, permissions, privilege levels — but the system administrator or application defines the actual rules. This separation of mechanism from policy is a fundamental OS design principle: the OS should enforce whatever policy is defined without imposing any particular policy itself.

## Access Control

An **access matrix** is the conceptual model for access control. Rows represent subjects (users or processes), columns represent objects (files, devices, memory regions), and each cell lists the operations the subject is allowed to perform on the object. In practice, the full matrix is never stored because it is enormous and mostly empty.

Two compressed representations are used:

An **Access Control List (ACL)** stores the access matrix column by column. Each object has a list of (subject, permissions) pairs. When someone tries to access an object, the system checks the object's ACL to see if that subject has the required permission. ACLs make it easy to enumerate who can access a specific object and to revoke access for a specific user.

A **Capability list** stores the access matrix row by row. Each subject has a list of (object, permissions) pairs called capabilities. Possessing a capability grants access to the object. Capabilities make it easy to enumerate what a specific user can access and to delegate access by transferring capabilities.

## Types of Security Threats

**Malware** is software designed to damage or gain unauthorized access to systems:

- **Viruses** attach themselves to legitimate programs and spread when those programs are executed. They require human action to propagate (running an infected program).
- **Worms** are self-replicating programs that spread autonomously across networks, exploiting vulnerabilities in network services.
- **Trojans** disguise themselves as legitimate software to trick users into running them, then perform malicious actions in the background.
- **Ransomware** encrypts a victim's files and demands payment for the decryption key.
- **Rootkits** modify the OS itself to hide their presence, making them extremely difficult to detect.

**Network attacks** exploit the connectivity that makes systems useful:

- **Denial of Service (DoS)** overwhelms a system with traffic so that it cannot respond to legitimate requests.
- **Phishing** tricks users into revealing credentials through deceptive communications.
- **Man-in-the-middle attacks** intercept communication between two parties to eavesdrop or modify data.
- **Buffer overflow attacks** exploit poorly written code to write data beyond a buffer's bounds, overwriting adjacent memory — including return addresses — to execute arbitrary code.

## Security Mechanisms

**Authentication** verifies identity — are you who you claim to be? Authentication factors fall into three categories:

- Something you know — passwords, PINs
- Something you have — a physical token, a smart card, a phone (for SMS codes)
- Something you are — biometrics: fingerprint, face, iris

Multi-factor authentication requires two or more of these categories, making it dramatically harder to compromise.

**Encryption** transforms data into an unreadable form without the decryption key, protecting confidentiality during storage and transmission. Symmetric encryption uses the same key for encryption and decryption (fast, but key distribution is a challenge). Asymmetric encryption uses a public key for encryption and a private key for decryption (solves key distribution but is slower).

**Firewalls** inspect network traffic and block connections that violate defined rules, reducing the attack surface exposed to the internet.

---

# CHAPTER 11: Deadlocks (Deep Dive)

## Understanding Deadlock Thoroughly

Deadlock was introduced in the context of synchronization, but it deserves deeper treatment because it is one of the most challenging problems in OS design. A deadlock is not a bug in the traditional sense — individual processes and the OS may all be functioning perfectly, yet the system has reached a state from which it cannot escape.

Consider four processes: P1 holds resource A and needs B. P2 holds B and needs C. P3 holds C and needs D. P4 holds D and needs A. Each is waiting for a resource held by the next — a circular chain of dependency. None can proceed. This is the essence of deadlock.

## Resource Allocation Graphs

A resource allocation graph provides a formal way to represent and detect deadlock. The graph has two types of nodes: process nodes (circles) and resource nodes (rectangles). An arrow from a resource to a process (assignment edge) means the process holds that resource. An arrow from a process to a resource (request edge) means the process is waiting for that resource.

If the graph contains no cycle, no deadlock exists. If the graph contains a cycle, deadlock may exist. For single-instance resources, a cycle means deadlock with certainty. For multi-instance resources, a cycle is necessary but not sufficient for deadlock.

## The Banker's Algorithm

The Banker's Algorithm is the classic deadlock avoidance algorithm, named by Dijkstra after the strategy a banker uses to avoid going bankrupt. The OS acts as a banker with a finite amount of resources (cash). Processes declare their maximum resource needs in advance. When a process requests resources, the banker checks whether granting the request would leave the system in a **safe state** — a state from which every process can eventually obtain all the resources it needs and complete.

A state is safe if a **safe sequence** exists — an ordering of all processes such that each process can be allocated the maximum resources it might need using currently available resources plus resources held by processes that appear earlier in the sequence.

The algorithm checks every request before granting it. If granting would produce an unsafe state, the process waits. This guarantees deadlock can never occur, but it is conservative — it may deny requests that would not actually lead to deadlock. It also requires knowing maximum resource needs in advance, which is often impractical. For these reasons, the Banker's Algorithm is more important as a concept than as a practical implementation.

## Recovery from Deadlock

When a system detects deadlock (through periodic resource allocation graph analysis), it must recover. Two approaches exist.

**Process termination** breaks the deadlock by killing one or more deadlocked processes, releasing their resources. Killing all deadlocked processes at once is guaranteed to break the deadlock but wastes all their completed work. Killing one process at a time and re-running detection is more careful. The OS must choose which process to kill — typically the one with the lowest cost in terms of priority, amount of work completed, and resources held.

**Resource preemption** takes a resource from a process and gives it to another. This must be combined with rolling the preempted process back to a state before it acquired the resource (requiring checkpointing mechanisms). The challenge is preventing starvation — if the same process is always selected as the victim, it will never complete.

---

# CHAPTER 12: Virtualization

## What Virtualization Is

Virtualization allows multiple operating systems to run simultaneously on a single physical machine. Each OS sees a complete virtual computer — virtual CPU, virtual memory, virtual devices — and behaves as if it were the only OS running on dedicated hardware. The software layer that creates and manages these virtual machines is called a **hypervisor** or **Virtual Machine Monitor (VMM)**.

The physical machine runs the hypervisor, which runs multiple guest operating systems. A server that used to run one OS and serve one purpose can now run many virtual machines, each with its own OS, serving different purposes — all on the same physical hardware. This revolutionized data center economics.

## Type 1 and Type 2 Hypervisors

**Type 1 hypervisors** (bare-metal) run directly on the hardware without a host OS between them. They are the lowest software layer and have direct access to all hardware. VMware ESXi, Microsoft Hyper-V, and Xen are Type 1 hypervisors. They provide excellent performance because there is no host OS overhead.

**Type 2 hypervisors** (hosted) run on top of a conventional OS, like any other application. VirtualBox and VMware Workstation are Type 2. They are easier to install and use — you run them on your existing operating system — but they have more overhead because hardware access goes through two software layers.

## Benefits and Challenges

Virtualization provides isolation — a failure or compromise in one VM does not affect others on the same physical machine. It provides encapsulation — an entire running system can be saved to a file, copied, moved, and restored. It provides consolidation — running many VMs on one server instead of many physical servers reduces hardware costs, energy consumption, and physical space.

The challenge is performance — the hypervisor must intercept and translate privileged hardware operations from the guest OS, adding overhead. Memory virtualization adds another layer of address translation. Modern hardware includes virtualization extensions (Intel VT-x, AMD-V) that make many of these operations efficient by providing hardware support for guest mode execution.

---

*End of Operating Systems Course Guide*

*Recommended Textbook: Abraham Silberschatz, Peter Baer Galvin, Greg Gagne — "Operating System Concepts" (Dinosaur Book)*
*Reference: Andrew S. Tanenbaum — "Modern Operating Systems"*
