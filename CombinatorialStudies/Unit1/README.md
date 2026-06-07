# Unit 1: Operating System Basics

---

## 1.1 Foundations of Operating Systems

**Operating System (OS):** System software that manages hardware and software resources and acts as an intermediary between the user and hardware.

### Functions:
- Process Management, Memory Management, File System Management, I/O Management, Security, Networking

### Components:
| Component | Role |
|---|---|
| **Kernel** | Core of OS; manages hardware, memory, processes in privileged mode |
| **Shell** | User interface — CLI (bash, cmd) or GUI |
| **System Calls** | API for programs to request kernel services (`fork()`, `exec()`, `open()`, `read()`, `write()`) |

### Kernel Types:
| Type | Description | Example |
|---|---|---|
| **Monolithic** | All services in kernel space; fast but less modular | Linux, Unix |
| **Microkernel** | Minimal kernel; most services in user space | Minix, QNX |
| **Hybrid** | Combines both | Windows NT, macOS |

---

## 1.2 Types of Operating Systems

| Type | Description | Example |
|---|---|---|
| **Batch OS** | Jobs collected and executed without user interaction | Early IBM |
| **Time-Sharing** | CPU time shared using time slices | Unix |
| **Real-Time (RTOS)** | Strict time deadlines | VxWorks |
| **Distributed** | Multiple machines act as one system | LOCUS |
| **Multiprogramming** | Multiple programs in memory; CPU switches on I/O wait | Mainframes |
| **Multiprocessing** | Multiple CPUs execute processes in parallel | Modern Linux |

**Hard Real-Time** — Missing deadline = total failure (pacemaker)  
**Soft Real-Time** — Missing deadline = degraded performance (video streaming)

---

## 1.3 Memory Management

### Memory Hierarchy: Registers → Cache → RAM → SSD/HDD

### Placement Algorithms:
| Algorithm | Description |
|---|---|
| **First Fit** | First hole big enough |
| **Best Fit** | Smallest hole big enough |
| **Worst Fit** | Largest hole |

### Paging:
- Physical memory → **Frames**, Logical memory → **Pages** (same fixed size)
- **Page Table** maps pages to frames
- Eliminates external fragmentation, may cause internal fragmentation

### Segmentation:
- Variable-size segments (code, data, stack)
- Can cause external fragmentation

### Virtual Memory & Page Replacement:
| Algorithm | Description |
|---|---|
| **FIFO** | Replace oldest page |
| **LRU** | Replace least recently used page |
| **Optimal** | Replace page not needed for longest time (theoretical) |

**Thrashing** — More time paging than executing  
**Belady's Anomaly** — FIFO: more frames can mean more page faults  
**Internal Fragmentation** — Waste inside allocated block (paging)  
**External Fragmentation** — Waste between blocks (segmentation)

---

## 1.4 CPU Scheduling

### Formulas:
```
Turnaround Time = Completion Time - Arrival Time
Waiting Time = Turnaround Time - Burst Time
```

| Algorithm | Type | Key Feature |
|---|---|---|
| **FCFS** | Non-Preemptive | Convoy Effect |
| **SJF** | Non-Preemptive | Minimum avg waiting time; can cause starvation |
| **SRTF** | Preemptive | Preemptive SJF |
| **Round Robin** | Preemptive | Time quantum; best for time-sharing |
| **Priority** | Both | Starvation solved by Aging |
| **Multilevel Feedback Queue** | Preemptive | Most flexible |

---

## 1.5 Process Synchronization & IPC

### Process States: New → Ready → Running → Waiting → Terminated

### Process vs Thread:
| Feature | Process | Thread |
|---|---|---|
| Memory | Separate | Shared |
| Overhead | High | Low |
| Crash | Independent | Affects whole process |

### Critical Section Requirements: Mutual Exclusion, Progress, Bounded Waiting

### Synchronization: Mutex (binary lock), Semaphore (counting), Monitor

### Deadlock Conditions (all 4 needed):
1. Mutual Exclusion  2. Hold and Wait  3. No Preemption  4. Circular Wait

**Banker's Algorithm** — Deadlock avoidance (check safe state)  
**Aging** — Solves starvation  

### IPC Methods: Pipes, Named Pipes, Message Queues, Shared Memory (fastest), Sockets, Signals

---

## MCQ Practice Questions (50+)

---

**Q1.** Which component of the OS directly interacts with hardware?
A. Shell  B. System Call  **C. Kernel ✅**  D. User Interface

---

**Q2.** Which scheduling algorithm causes Convoy Effect?
**A. FCFS ✅**  B. SJF  C. Round Robin  D. Priority

---

**Q3.** Belady's Anomaly occurs in which page replacement algorithm?
**A. FIFO ✅**  B. LRU  C. Optimal  D. LFU

---

**Q4.** Which algorithm gives minimum average waiting time?
A. FCFS  **B. SJF ✅**  C. Round Robin  D. Priority

---

**Q5.** Which is NOT a necessary condition for deadlock?
A. Mutual Exclusion  B. Hold and Wait  C. Circular Wait  **D. Preemption ✅**

> The condition is "No Preemption", not "Preemption."

---

**Q6.** What is thrashing?
A. Running too many programs  B. A disk scheduling algorithm  **C. Process spends more time paging than executing ✅**  D. Memory leak

---

**Q7.** In Round Robin, when time quantum expires, the process:
A. Terminates  B. Goes to waiting  **C. Moves to back of ready queue ✅**  D. Gets higher priority

---

**Q8.** Which fragmentation occurs in paging?
A. External  **B. Internal ✅**  C. Both  D. Neither

---

**Q9.** Fastest IPC mechanism?
A. Pipes  B. Message Queues  **C. Shared Memory ✅**  D. Sockets

---

**Q10.** A semaphore initialized to 1 is equivalent to:
**A. Mutex ✅**  B. Counting Semaphore  C. Monitor  D. Spinlock

---

**Q11.** Banker's Algorithm is used for deadlock:
A. Detection  **B. Avoidance ✅**  C. Prevention  D. Recovery

---

**Q12.** Paging divides physical memory into:
A. Segments  **B. Frames ✅**  C. Blocks  D. Sectors

---

**Q13.** Starvation in priority scheduling is solved by:
A. Increasing quantum  **B. Aging ✅**  C. Using FCFS  D. More CPUs

---

**Q14.** Which is a preemptive scheduling algorithm?
A. FCFS  B. SJF  **C. SRTF ✅**  D. None

---

**Q15.** A page fault occurs when:
A. Hardware error  B. Page table error  **C. Referenced page not in main memory ✅**  D. Config error

---

**Q16.** All OS services run in kernel space in:
**A. Monolithic Kernel ✅**  B. Microkernel  C. Hybrid  D. Exokernel

---

**Q17.** Critical section problem requires all EXCEPT:
A. Mutual Exclusion  B. Progress  C. Bounded Waiting  **D. Starvation ✅**

---

**Q18.** Best Fit allocates:
A. First hole big enough  **B. Smallest hole big enough ✅**  C. Largest hole  D. Random hole

---

**Q19.** Turnaround Time = ?
A. Burst - Arrival  **B. Completion Time - Arrival Time ✅**  C. Waiting + Arrival  D. Completion - Burst

---

**Q20.** Producer-Consumer uses:
A. Mutex only  **B. Semaphores (mutex + empty + full) ✅**  C. Signals  D. Pipes

---

**Q21.** Which OS type guarantees response within strict time deadlines?
A. Batch OS  B. Time-sharing  **C. Real-Time OS ✅**  D. Network OS

---

**Q22.** `fork()` system call creates a:
A. Thread  **B. Child process ✅**  C. File  D. Semaphore

---

**Q23.** In which state is a process waiting for I/O?
A. Ready  B. Running  **C. Waiting/Blocked ✅**  D. Terminated

---

**Q24.** Which scheduling is best for time-sharing systems?
A. FCFS  B. SJF  **C. Round Robin ✅**  D. Priority

---

**Q25.** Context switching involves saving and restoring:
A. Files  **B. Process state (PCB) ✅**  C. Disk data  D. Network connections

---

**Q26.** The PCB (Process Control Block) contains:
A. Only process ID  B. Only program counter  **C. Process ID, state, program counter, registers, memory info ✅**  D. Only memory info

---

**Q27.** Which page replacement is theoretically the best but not implementable?
A. FIFO  B. LRU  **C. Optimal (OPT) ✅**  D. LFU

---

**Q28.** In a multiprogramming system, when one process waits for I/O, the CPU:
A. Waits idle  **B. Switches to another process ✅**  C. Shuts down  D. Restarts

---

**Q29.** Mutual Exclusion means:
**A. Only one process in critical section at a time ✅**  B. All processes execute together  C. No process can enter  D. Processes share memory freely

---

**Q30.** Semaphore `wait(S)` operation is also called:
A. V(S)  B. signal(S)  **C. P(S) ✅**  D. release(S)

---

**Q31.** Which deadlock handling strategy ignores the problem entirely?
A. Prevention  B. Avoidance  C. Detection  **D. Ostrich Algorithm ✅**

---

**Q32.** Worst Fit algorithm allocates:
A. Smallest hole  **B. Largest hole ✅**  C. First hole  D. Last hole

---

**Q33.** A process that has finished execution is in the:
A. Ready state  B. Blocked state  **C. Terminated state ✅**  D. New state

---

**Q34.** Which classic synchronization problem involves 5 philosophers and 5 forks?
A. Producer-Consumer  B. Reader-Writer  **C. Dining Philosophers ✅**  D. Sleeping Barber

---

**Q35.** Logical memory is divided into pages; physical memory is divided into:
A. Segments  **B. Frames ✅**  C. Clusters  D. Tracks

---

**Q36.** Which system call is used to execute a new program in Unix?
A. fork()  **B. exec() ✅**  C. wait()  D. exit()

---

**Q37.** In a time-sharing OS, the CPU switches between processes using:
A. Interrupts only  **B. Time quantum/time slice ✅**  C. Priority only  D. Random selection

---

**Q38.** What does SRTF stand for?
A. Shortest Run Time First  **B. Shortest Remaining Time First ✅**  C. Shortest Response Time First  D. Simple Round Time First

---

**Q39.** External fragmentation can be solved by:
A. Paging  B. Compaction  C. Both  **D. Both Paging and Compaction ✅**

---

**Q40.** Which IPC method allows communication between processes on different machines?
A. Pipes  B. Shared Memory  C. Signals  **D. Sockets ✅**

---

**Q41.** Demand paging loads a page into memory:
A. At program start  B. At boot time  **C. Only when it is needed (on page fault) ✅**  D. Randomly

---

**Q42.** Multilevel Feedback Queue is the most _____ scheduling algorithm:
A. Simple  B. Fast  **C. Flexible ✅**  D. Outdated

---

**Q43.** A thread is also called a:
**A. Lightweight process ✅**  B. Heavy process  C. Kernel module  D. Device driver

---

**Q44.** User-level threads are managed by:
A. Kernel  **B. User-level library ✅**  C. Hardware  D. Shell

---

**Q45.** Which of the following is NOT a process state?
A. Ready  B. Running  C. Waiting  **D. Executing ✅**

> Standard states: New, Ready, Running, Waiting, Terminated. "Executing" is not a standard term.

---

**Q46.** If a large time quantum is used in Round Robin, it behaves like:
**A. FCFS ✅**  B. SJF  C. Priority  D. SRTF

---

**Q47.** If a very small time quantum is used in Round Robin:
A. Throughput increases  B. Performance improves  **C. Too many context switches, overhead increases ✅**  D. No effect

---

**Q48.** In the Reader-Writer problem, multiple readers can read simultaneously:
**A. True ✅**  B. False

> Readers can access shared data concurrently. Writers need exclusive access.

---

**Q49.** `wait()` system call is used by a parent process to:
A. Create a child  **B. Wait for a child process to finish ✅**  C. Kill a child  D. Send data to child

---

**Q50.** Which memory technique allows a process larger than physical memory to execute?
A. Paging  B. Segmentation  **C. Virtual Memory ✅**  D. Caching

---

## Scenario & One-Line Answer Questions

---

**S1.** A process with burst time 50ms is waiting behind a process with burst time 500ms in FCFS. What problem is this?
> **Convoy Effect** — Short processes wait behind a long process in FCFS scheduling.

**S2.** A system has 5 processes and all are rapidly swapping pages in and out. What is happening?
> **Thrashing** — The system is spending more time on page swapping than actual process execution due to insufficient frames.

**S3.** You increase the number of frames allocated to a process using FIFO replacement, but page faults increase. What anomaly is this?
> **Belady's Anomaly** — In FIFO page replacement, more frames can paradoxically lead to more page faults.

**S4.** Process A holds Resource 1 and waits for Resource 2. Process B holds Resource 2 and waits for Resource 1. What is this?
> **Deadlock** — Both processes are waiting for resources held by the other, creating a circular wait.

**S5.** A low-priority process never gets CPU time because higher-priority processes keep arriving. What is this?
> **Starvation** — The process indefinitely waits. Solved by **Aging** (gradually increasing priority over time).

**S6.** What happens when fork() is called?
> A new **child process** is created that is a copy of the parent. `fork()` returns 0 to the child and the child's PID to the parent.

**S7.** A process needs a page that is not in RAM. What happens?
> A **Page Fault** occurs. The OS loads the required page from disk into a free frame in RAM.

**S8.** What is the difference between preemptive and non-preemptive scheduling?
> **Preemptive** — OS can interrupt a running process (Round Robin, SRTF). **Non-preemptive** — process runs until it finishes or blocks (FCFS, SJF).

**S9.** Why is Optimal page replacement not practically implementable?
> Because it requires **future knowledge** — knowing which pages will be needed next, which is impossible in real systems.

**S10.** In a paging system, a process is 10,000 bytes and page size is 4096 bytes. How many pages?
> 3 pages (4096 + 4096 + 1808). The last page has **internal fragmentation** of 4096 - 1808 = **2288 bytes** wasted.

**S11.** What is the difference between a process and a thread?
> A **process** has its own memory space and resources. A **thread** shares the process's memory and resources but has its own stack and program counter. Threads are lightweight; context switching between threads is faster.

**S12.** What is a zombie process?
> A process that has completed execution but still has an entry in the process table because its parent hasn't called `wait()` to collect its exit status.

**S13.** What is an orphan process?
> A process whose parent has terminated. In Unix, orphan processes are adopted by the `init` process (PID 1).

**S14.** What is the difference between a mutex and a semaphore?
> **Mutex** — Binary lock (0 or 1), owned by a thread, only the owner can unlock. **Semaphore** — Integer counter, can be used for signaling between processes, any process can signal.

**S15.** If Round Robin time quantum = ∞, which algorithm does it become?
> **FCFS (First Come First Serve)** — With infinite quantum, no preemption occurs, and processes run to completion in arrival order.

---
