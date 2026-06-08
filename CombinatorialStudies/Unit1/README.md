# Unit 1: Operating System Basics

---

## 1.1 Foundations of Operating Systems

**Operating System (OS):** System software that acts as an intermediary between the user and hardware, managing resources.

### Components:
| Component | Role |
|---|---|
| **Kernel** | Core; manages hardware, memory, processes in privileged mode |
| **Shell** | User interface — CLI (bash) or GUI |
| **System Calls** | API for programs to request kernel services (`fork()`, `exec()`, `open()`, `read()`, `write()`, `wait()`, `exit()`) |

### Kernel Types:
| Type | Description | Example |
|---|---|---|
| **Monolithic** | All services in kernel space; fast | Linux, Unix |
| **Microkernel** | Minimal kernel; most services in user space | Minix, QNX |
| **Hybrid** | Combines both | Windows NT, macOS |

---

## 1.2 Types of Operating Systems

| Type | Key Feature | Example |
|---|---|---|
| **Batch OS** | Jobs in batches, no interaction | Early IBM |
| **Time-Sharing** | CPU shared using time slices | Unix |
| **Real-Time (RTOS)** | Strict time deadlines | VxWorks |
| **Distributed** | Multiple machines as one system | LOCUS |
| **Multiprogramming** | Multiple programs in memory | Mainframes |
| **Multiprocessing** | Multiple CPUs | Modern Linux |

**Hard Real-Time** — Missing deadline = failure (pacemaker)  
**Soft Real-Time** — Missing deadline = degraded performance (video streaming)

---

## 1.3 Memory Management

### Memory Hierarchy: Registers → Cache (L1→L2→L3) → RAM → SSD/HDD

### Placement Algorithms:
| Algorithm | Description |
|---|---|
| **First Fit** | First hole big enough |
| **Best Fit** | Smallest hole big enough |
| **Worst Fit** | Largest hole |

### Paging:
- Physical memory → **Frames**, Logical memory → **Pages** (same fixed size)
- **Page Table** maps pages to frames
- Eliminates external fragmentation; may cause internal fragmentation
- Logical Address = Page Number + Page Offset

### Virtual Memory & Page Replacement:
| Algorithm | Description |
|---|---|
| **FIFO** | Replace oldest page (suffers **Belady's Anomaly**) |
| **LRU** | Replace least recently used page |
| **Optimal** | Replace page not needed for longest time (theoretical, not implementable) |

### Key Concepts:
- **Thrashing** — Process spends more time paging than executing
- **Belady's Anomaly** — In FIFO only: more frames → more page faults (paradox)
- **Internal Fragmentation** — Waste INSIDE allocated block (paging)
- **External Fragmentation** — Waste BETWEEN allocated blocks (segmentation)
- **Increasing RAM improves performance because fewer page faults occur**

### Context Switch:
- Saves/restores process state (PCB): program counter, registers, memory maps
- **General purpose registers** need to be saved during context switch
- **Translation look-aside buffer (TLB)** does NOT need to be saved (it's flushed)

---

## 1.4 CPU Scheduling

### Formulas:
```
Turnaround Time (TAT) = Completion Time - Arrival Time
Waiting Time (WT) = Turnaround Time - Burst Time
Response Time = First CPU Time - Arrival Time
```

| Algorithm | Type | Key Point |
|---|---|---|
| **FCFS** | Non-Preemptive | Simple; causes **Convoy Effect** |
| **SJF** | Non-Preemptive | Min avg waiting time; causes **starvation** |
| **SRTF** | Preemptive | Preemptive SJF; also causes starvation |
| **Round Robin** | Preemptive | Time quantum; best for time-sharing; no starvation |
| **Priority** | Both | Starvation solved by **Aging** |
| **Multilevel Feedback Queue** | Preemptive | Most flexible algorithm |

> **SJF / Shortest Job Next can lead to starvation** of longer processes.

---

## 1.5 Process Synchronization & IPC

### Process States: New → Ready → Running → Waiting → Terminated

### Deadlock — 4 Necessary Conditions (ALL must hold):
1. **Mutual Exclusion** — Resources cannot be shared (claims **exclusive control**)
2. **Hold and Wait** — Process holds resources while waiting for others
3. **No Preemption** — Resources cannot be forcibly taken
4. **Circular Wait** — Circular chain of waiting processes

**Banker's Algorithm** — Deadlock avoidance (checks safe state)

### Synchronization:
- **Mutex** — Binary lock (only one thread at a time)
- **Semaphore** — Integer counter for signaling (Binary = mutex, Counting = N resources)
- **Monitor** — High-level construct with automatic mutual exclusion

### IPC Methods: Pipes, Named Pipes, Message Queues, **Shared Memory (fastest)**, Sockets, Signals

---

## MCQ Practice Questions (50+ PYQ Style)

---

**Q1.** Which page replacement algorithm suffers from Belady's anomaly?

a) FIFO ← **✅**  
b) LRU  
c) Optimal Page Replacement  
d) Both LRU and FIFO

---

**Q2.** Increasing the RAM of a computer typically improves performance because:

a) Virtual memory increases  
b) Larger RAMs are faster  
**c) Fewer page faults occur ✅**  
d) Fewer segmentation faults occur

---

**Q3.** Which process scheduling algorithm may lead to starvation?

a) FIFO  
b) Round Robin  
**c) Shortest Job Next ✅**  
d) None of the above

---

**Q4.** In which of the four deadlock conditions do processes claim exclusive control of resources?

a) No pre-emption  
**b) Mutual exclusion ✅**  
c) Circular wait  
d) Hold and wait

---

**Q5.** Which need NOT necessarily be saved during a context switch?

a) General purpose registers  
**b) Translation look-aside buffer ✅**  
c) Program counter  
d) All of the above

---

**Q6.** Which scheduling algorithm causes the Convoy Effect?

**a) FCFS ✅**  
b) SJF  
c) Round Robin  
d) Priority

---

**Q7.** Which scheduling algorithm gives minimum average waiting time?

a) FCFS  
**b) SJF ✅**  
c) Round Robin  
d) FCFS

---

**Q8.** In Round Robin, when time quantum expires, the process:

a) Terminates  
b) Goes to waiting  
**c) Moves to back of ready queue ✅**  
d) Gets higher priority

---

**Q9.** Which fragmentation occurs in paging?

a) External  
**b) Internal ✅**  
c) Both  
d) Neither

---

**Q10.** Fastest IPC mechanism?

a) Pipes  
b) Message Queues  
**c) Shared Memory ✅**  
d) Sockets

---

**Q11.** A semaphore initialized to 1 is equivalent to:

**a) Mutex ✅**  
b) Counting Semaphore  
c) Monitor  
d) Spinlock

---

**Q12.** Banker's Algorithm is used for deadlock:

a) Detection  
**b) Avoidance ✅**  
c) Prevention  
d) Recovery

---

**Q13.** Paging divides physical memory into:

a) Segments  
**b) Frames ✅**  
c) Blocks  
d) Sectors

---

**Q14.** Starvation in priority scheduling is solved by:

a) Increasing quantum  
**b) Aging ✅**  
c) Using FCFS  
d) More CPUs

---

**Q15.** A page fault occurs when:

a) Hardware error  
b) Page table error  
**c) Referenced page not in main memory ✅**  
d) Configuration error

---

**Q16.** All OS services in kernel space → which kernel?

**a) Monolithic ✅**  
b) Microkernel  
c) Hybrid  
d) Exokernel

---

**Q17.** Critical section problem requires all EXCEPT:

a) Mutual Exclusion  
b) Progress  
c) Bounded Waiting  
**d) Starvation ✅**

---

**Q18.** Best Fit allocates:

a) First hole  
**b) Smallest hole big enough ✅**  
c) Largest hole  
d) Random

---

**Q19.** Turnaround Time = ?

a) Burst - Arrival  
**b) Completion Time - Arrival Time ✅**  
c) Waiting + Arrival  
d) Completion - Burst

---

**Q20.** Which OS guarantees strict time deadlines?

a) Batch OS  
b) Time-sharing  
**c) Real-Time OS ✅**  
d) Network OS

---

**Q21.** `fork()` creates a:

a) Thread  
**b) Child process ✅**  
c) File  
d) Semaphore

---

**Q22.** Process waiting for I/O is in which state?

a) Ready  
b) Running  
**c) Waiting/Blocked ✅**  
d) Terminated

---

**Q23.** Which page replacement is theoretically best but not implementable?

a) FIFO  
b) LRU  
**c) Optimal ✅**  
d) LFU

---

**Q24.** In a multiprogramming system, when one process waits for I/O:

a) CPU waits  
**b) CPU switches to another process ✅**  
c) System shuts down  
d) CPU restarts

---

**Q25.** Semaphore wait(S) operation is also called:

a) V(S)  
b) signal(S)  
**c) P(S) ✅**  
d) release(S)

---

**Q26.** Which deadlock handling ignores the problem?

a) Prevention  
b) Avoidance  
c) Detection  
**d) Ostrich Algorithm ✅**

---

**Q27.** A process that finished but parent hasn't called wait() is:

a) Orphan  
**b) Zombie ✅**  
c) Daemon  
d) Blocked

---

**Q28.** A process whose parent terminated is:

**a) Orphan ✅**  
b) Zombie  
c) Daemon  
d) Init

---

**Q29.** Thread is also called a:

**a) Lightweight process ✅**  
b) Heavy process  
c) Kernel module  
d) Daemon

---

**Q30.** If Round Robin quantum = ∞, it behaves like:

**a) FCFS ✅**  
b) SJF  
c) Priority  
d) SRTF

---

**Q31.** If Round Robin quantum is very small:

a) Throughput increases  
**b) Too many context switches, overhead increases ✅**  
c) Performance improves  
d) No effect

---

**Q32.** Dining Philosophers problem involves:

a) 3 philosophers  
**b) 5 philosophers and 5 forks ✅**  
c) 10 philosophers  
d) 2 philosophers

---

**Q33.** Which classic problem has a bounded buffer?

**a) Producer-Consumer ✅**  
b) Reader-Writer  
c) Dining Philosophers  
d) Sleeping Barber

---

**Q34.** External fragmentation is solved by:

a) Paging only  
b) Compaction only  
**c) Both Paging and Compaction ✅**  
d) Neither

---

**Q35.** Demand paging loads a page into memory:

a) At program start  
**b) Only when it is needed (on page fault) ✅**  
c) At boot time  
d) Randomly

---

**Q36.** User-level threads are managed by:

a) Kernel  
**b) User-level library ✅**  
c) Hardware  
d) Shell

---

**Q37.** PCB (Process Control Block) contains:

a) Only PID  
b) Only program counter  
**c) PID, state, program counter, registers, memory info ✅**  
d) Only memory

---

**Q38.** The Multilevel Feedback Queue is the most _____ scheduling algorithm:

a) Simple  
**b) Flexible ✅**  
c) Fast  
d) Outdated

---

**Q39.** SRTF stands for:

a) Shortest Run Time First  
**b) Shortest Remaining Time First ✅**  
c) Shortest Response Time First  
d) Simple Round Time First

---

**Q40.** Which of the following is NOT a process state?

a) Ready  
b) Running  
c) Waiting  
**d) Executing ✅**

---

**Q41.** In Reader-Writer problem, multiple readers can read simultaneously:

**a) True ✅**  
b) False

---

**Q42.** `wait()` system call is used by a parent to:

a) Create a child  
**b) Wait for child process to finish ✅**  
c) Kill a child  
d) Send data

---

**Q43.** Virtual memory allows execution of processes:

a) Only smaller than RAM  
**b) Larger than physical memory ✅**  
c) Equal to RAM  
d) Only on SSD

---

**Q44.** What does thrashing cause?

a) High CPU utilization  
**b) Low CPU utilization and excessive paging ✅**  
c) Faster execution  
d) More free memory

---

**Q45.** Which of the following uses circular queue internally?

a) Stack  
b) Tree  
**c) CPU scheduling (Round Robin) ✅**  
d) Graph

---

**Q46.** What is the main difference between process and thread?

a) Threads are slower  
**b) Threads share memory space; processes have separate memory ✅**  
c) Processes are lighter  
d) No difference

---

**Q47.** Cache memory is placed between:

**a) CPU and RAM ✅**  
b) RAM and Disk  
c) CPU and Disk  
d) I/O and RAM

---

**Q48.** Logical address is generated by:

**a) CPU ✅**  
b) MMU  
c) Hard disk  
d) RAM

---

**Q49.** Physical address is generated by:

a) CPU  
**b) MMU (Memory Management Unit) ✅**  
c) Compiler  
d) Linker

---

**Q50.** Which is NOT a deadlock condition?

a) Mutual Exclusion  
b) Hold and Wait  
c) No Preemption  
**d) Preemption ✅**

---

## Scenario / One-Line Answers

**S1.** Increasing RAM → fewer page faults → better performance.  
**S2.** Belady's Anomaly occurs ONLY in FIFO, not in LRU or Optimal.  
**S3.** SJF causes starvation; solved by aging.  
**S4.** Mutual exclusion = process claims exclusive control of resources.  
**S5.** TLB does NOT need saving during context switch (it's hardware cache, gets flushed).  
**S6.** Fork() returns 0 to child, child's PID to parent.  
**S7.** Zombie = finished but parent hasn't collected exit status. Orphan = parent died.  
**S8.** Thrashing = too many processes, not enough frames → CPU utilization drops.

---
