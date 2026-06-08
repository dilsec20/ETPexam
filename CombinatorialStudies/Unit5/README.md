# Unit 5: Data Structures

---

## 5.1 Arrays

### 1D Array Address Calculation:
```
Address of A[i] = Base Address + i × Size
```
Example: Base = 1000, Size = 4 bytes, A[5] = 1000 + 5×4 = **1020**

### 2D Array Address Calculation:

**Row-Major Order** (C, C++, Java — row by row):
```
Address of A[i][j] = Base + (i × C + j) × Size
```
Where C = number of columns

**Column-Major Order** (Fortran — column by column):
```
Address of A[i][j] = Base + (j × R + i) × Size
```
Where R = number of rows

**Example:** A[10][20], Base = 2000, Size = 4 bytes. Find A[3][5] in Row-Major:
```
= 2000 + (3 × 20 + 5) × 4 = 2000 + 65 × 4 = 2000 + 260 = 2260
```

### Disadvantages of Arrays:
- **Fixed size** — cannot grow dynamically
- **Insertion/Deletion is O(n)** — requires shifting
- **Memory wastage** if elements inserted are fewer than allocated size
- Elements are sequentially accessed in linked form

> **PYQ: Disadvantage of array? → There are chances of wastage of memory space if elements inserted are lesser than allocated size** ✅

---

## 5.2 Linked Lists

| Type | Description |
|---|---|
| **Singly** | data + next pointer |
| **Doubly** | data + next + prev pointer |
| **Circular** | Last node → first node |

### Array vs Linked List:
| Feature | Array | Linked List |
|---|---|---|
| Size | Fixed | Dynamic |
| Access | O(1) random | O(n) sequential |
| Insert/Delete | O(n) | O(1) at head |
| Memory | Contiguous | Non-contiguous + pointer overhead |

---

## 5.3 Stacks — LIFO (Last In, First Out)

**Operations:** push O(1), pop O(1), peek O(1)

### Applications of Stack:
- ✅ Function call stack (recursion)
- ✅ Undo/redo operations
- ✅ Expression evaluation (postfix/prefix)
- ✅ **Infix to Postfix conversion**
- ✅ **Balanced parentheses check**
- ✅ Backtracking
- ✅ Browser back button
- ✅ **Reversing a word/string**
- ✅ Compiler syntax analysis
- ✅ **Tracking local variables at runtime**
- ❌ NOT for: Data transfer between two asynchronous processes (that's a Queue/Buffer)

> **PYQ: Which is NOT application of stack? → a) Data transfer between two asynchronous processes** ✅  
> **PYQ: Data structure for reversing a word? → d) Stack** ✅  
> **PYQ: Data structure for parentheses matching? → d) Stack** ✅  
> **PYQ: Data structure for implementing recursion? → a) Stack** ✅

---

## 5.4 Infix, Prefix, Postfix Expressions

### Definitions:
| Type | Operator Position | Example |
|---|---|---|
| **Infix** | Between operands | A + B |
| **Prefix** (Polish) | Before operands | + A B |
| **Postfix** (Reverse Polish) | After operands | A B + |

### Infix to Postfix Conversion — uses **Stack**:

> **PYQ: Which data structure converts infix to postfix? → c) Stack** ✅

### Infix to Prefix Conversion:
**Steps:** Reverse infix → Convert to postfix → Reverse result

**PYQ: Prefix form of A-B/(C*D^E):**
```
Step 1: Precedence: ^ > * > / > -
Step 2: A - B/(C*D^E)
       = A - B/(C*(^DE))        → ^ first
       = A - B/(*C^DE)          → * next
       = A - (/B*C^DE)          → / next
       = -A/B*C^DE              → - last
Prefix = - A / B * C ^ D E
```
> **PYQ Answer: → b) -A/B*C^DE** (written as -A/BC*DE in compact form) ✅

### Postfix Expression Evaluation — uses **Stack**:

**PYQ: Value of postfix expression `6 3 2 4 + - *` ?**
```
Read 6 → push 6.          Stack: [6]
Read 3 → push 3.          Stack: [6, 3]
Read 2 → push 2.          Stack: [6, 3, 2]
Read 4 → push 4.          Stack: [6, 3, 2, 4]
Read + → pop 4, 2 → 2+4=6 → push 6.   Stack: [6, 3, 6]
Read - → pop 6, 3 → 3-6=-3 → push -3. Stack: [6, -3]
Read * → pop -3, 6 → 6×(-3)=-18.       Stack: [-18]
Answer = -18
```
> **PYQ Answer: b) -18** ✅

---

## 5.5 Queues — FIFO (First In, First Out)

**Operations:** enqueue O(1), dequeue O(1)

### Types:
| Type | Description |
|---|---|
| **Simple Queue** | FIFO |
| **Circular Queue** | Last → first; solves wasted space |
| **Priority Queue** | Dequeue by priority |
| **Deque** | Insert/delete from **BOTH front and rear** |

> **PYQ: What is a deque? → c) A queue with insert/delete defined for both front and rear ends** ✅  
> **PYQ: Insert/delete from both ends but not middle? → b) Deque** ✅

**Applications:** CPU scheduling (Round Robin), BFS traversal, printer queue, buffering

---

## 5.6 Trees

### Binary Search Tree (BST):
- Left < Root < Right
- **Inorder traversal → sorted output**
- Average: O(log n), Worst (skewed): O(n)

### Traversals:
| Traversal | Order |
|---|---|
| **Inorder** | Left → Root → Right |
| **Preorder** | Root → Left → Right |
| **Postorder** | Left → Right → Root |
| **Level Order** | BFS using **Queue** |

### Balanced vs Unbalanced Trees:
| Tree | Balanced? |
|---|---|
| **AVL Tree** | ✅ Yes (balance factor ≤ 1) |
| **Red-Black Tree** | ✅ Yes |
| **B-Tree** | ✅ Yes (used in **databases, external memory**) |
| **Splay Tree** | ❌ **NOT balanced** (self-adjusting but not strictly balanced) |

> **PYQ: Which is NOT a balanced binary tree? → a) Splay tree** ✅  
> **PYQ: Most widely used external memory data structure? → a) B-tree** ✅  
> **PYQ: LIFO principle data structure? → c) Stack** ✅

---

## 5.7 Graphs

### Representation:
| Method | Space | Edge Check |
|---|---|---|
| **Adjacency Matrix** | O(V²) | O(1) |
| **Adjacency List** | O(V+E) | O(V) |

### BFS and DFS:
| Algorithm | Uses | Complexity |
|---|---|---|
| **BFS** | **Queue** | **O(V + E)** |
| **DFS** | **Stack/Recursion** | O(V + E) |

> **PYQ: BFS data structure? → d) Queue** ✅  
> **PYQ: BFS time complexity? → a) O(V + E)** ✅  
> **PYQ: BFS traversal of graph results in? → Tree** ✅ (BFS tree / spanning tree)

### Graph Formulas:

**Vertex Coloring:**
If a graph G has degree at most **d**, then it can have a vertex coloring of at most **d + 1** colors.
> **PYQ: Degree at most 23 → vertex coloring of d+1 = 24** ✅

**Forest Edges Formula:**
A forest with **V vertices** and **K connected components** has:
```
Edges = V - K
```
> **PYQ: 54 vertices, 17 components → Edges = 54 - 17 = 37** ✅

**Regular Graph Edges:**
A regular graph where every vertex has degree **d** and has **n** vertices:
```
Edges = (n × d) / 2
```
> **PYQ: Degree 46, 8 vertices → Edges = (8 × 46)/2 = 184** ✅

### Key Algorithms:
| Algorithm | Purpose |
|---|---|
| **Dijkstra's** | Shortest path (NO negative edges) |
| **Bellman-Ford** | Shortest path (handles negatives) |
| **Floyd-Warshall** | All-pairs shortest path |
| **Kruskal's** | MST (sort edges) |
| **Prim's** | MST (vertex-based) |

> **PYQ: Dijkstra's cannot be applied on → b) Graphs having negative weight function** ✅  
> **PYQ: When k=0 in Floyd-Warshall → b) 0 intermediate vertices** ✅  
> **PYQ: Max decrease-key operations in Dijkstra's = Number of vertices - 1** ✅

---

## 5.8 Hashing

**Hash Function:** Maps key to index: `h(key) = key % table_size`

**Collision Resolution:** Chaining (linked lists), Linear Probing, Quadratic Probing, Double Hashing

**Load Factor:** α = n/m (items/table_size)

> **PYQ: If n keys hashed into table of size m where n < m, expected collisions for a key x is → a) Less than 1** ✅  
> (When load factor < 1, expected collisions per key < 1)

---

## 5.9 Heaps

| Type | Root |
|---|---|
| **Max Heap** | Maximum element |
| **Min Heap** | Minimum element |

**Heap Sort:** O(n log n), Space O(1)  
**Priority Queue** is implemented using a **Heap**

---

## MCQ Practice Questions (50+ PYQ Style)

---

**Q1.** What are the disadvantages of arrays?

a) Index value can be negative  
b) Elements are sequentially accessed  
c) Data structures like queue/stack cannot be implemented  
**d) Wastage of memory if fewer elements than allocated size ✅**

---

**Q2.** Which data structure is used for implementing recursion?

**a) Stack ✅**  
b) Queue  
c) List  
d) Array

---

**Q3.** Which is NOT the application of stack?

**a) Data transfer between two asynchronous processes ✅**  
b) Compiler Syntax Analyzer  
c) Tracking local variables at runtime  
d) Parenthesis balancing program

---

**Q4.** Which data structure converts infix to postfix?

a) Tree  
b) Branch  
**c) Stack ✅**  
d) Queue

---

**Q5.** Value of postfix expression `6 3 2 4 + - *` ?

a) 74  
**b) -18 ✅**  
c) 22  
d) 40

---

**Q6.** BFS data structure?

a) Array  
b) Stack  
c) Tree  
**d) Queue ✅**

---

**Q7.** Prefix form of A-B/(C*D^E)?

a) -A/B*C^DE  
**b) -A/BC*DE ✅**  
c) -ABCD*DE  
d) -/*ACBDE

---

**Q8.** LIFO principle data structure?

a) Tree  
b) Branch  
**c) Stack ✅**  
d) Queue

---

**Q9.** Which is NOT a balanced binary tree?

**a) Splay tree ✅**  
b) B-tree  
c) AVL tree  
d) Red-black tree

---

**Q10.** Parentheses matching uses?

a) Priority queue  
b) Queue  
c) n-ary tree  
**d) Stack ✅**

---

**Q11.** Most widely used external memory data structure?

**a) B-tree ✅**  
b) Red-black tree  
c) AVL tree  
d) Both AVL and Red-black

---

**Q12.** Most appropriate for reversing a word?

a) Queue  
b) Stack  
c) Graph  
**d) Stack ✅**

---

**Q13.** What is a deque?

a) Queue with singly and doubly linked lists  
b) Queue with insert/delete for front only  
**c) Queue with insert/delete defined for both front and rear ends ✅**  
d) Queue with doubly linked list

---

**Q14.** Insert/delete from both ends but not middle?

a) Priority queue  
**b) Deque ✅**  
c) Circular queue  
d) Queue

---

**Q15.** Binary search complexity?

a) O(n)  
**b) O(log n) ✅**  
c) O(n²)  
d) O(n log n)

---

**Q16.** If G has degree at most 23, vertex coloring needed?

a) 23  
**b) 24 ✅**  
c) 176  
d) 64

---

**Q17.** Forest with 54 vertices and 17 connected components has total edges:

a) 38  
**b) 37 ✅**  
c) 54  
d) 63

---

**Q18.** Regular graph: degree 46, 8 vertices → number of edges?

a) 347  
b) 230  
**c) 184 ✅**  
d) 186

---

**Q19.** Dijkstra's CANNOT be applied on:

a) Directed and weighted  
**b) Graphs having negative weight ✅**  
c) Unweighted  
d) Undirected

---

**Q20.** When k=0 in Floyd-Warshall:

a) 1 intermediate vertex  
**b) 0 intermediate vertices ✅**  
c) N intermediate  
d) N-1 intermediate

---

**Q21.** Max decrease-key operations in Dijkstra's = ?

a) Total vertices  
b) Total edges  
**c) Number of vertices - 1 ✅**  
d) Number of edges - 1

---

**Q22.** BFS traversal of a graph results in:

a) Linked list  
**b) Tree ✅**  
c) Graph with back edges  
d) Arrays

---

**Q23.** BFS time complexity:

**a) O(V + E) ✅**  
b) O(V)  
c) O(E)  
d) O(V*E)

---

**Q24.** If n keys hashed into table of size m (n < m), expected collisions per key x:

**a) Less than 1 ✅**  
b) Less than n  
c) Less than m  
d) Less than n/2

---

**Q25.** Stack follows:

**a) LIFO ✅**  
b) FIFO  
c) Random  
d) Priority

---

**Q26.** Queue follows:

**a) FIFO ✅**  
b) LIFO  
c) Random  
d) FILO

---

**Q27.** Inorder traversal of BST gives:

**a) Sorted output ✅**  
b) Reverse sorted  
c) Random  
d) Level order

---

**Q28.** Array access by index:

**a) O(1) ✅**  
b) O(n)  
c) O(log n)  
d) O(n²)

---

**Q29.** Linked list search:

a) O(1)  
**b) O(n) ✅**  
c) O(log n)  
d) O(n²)

---

**Q30.** Hash table average search:

**a) O(1) ✅**  
b) O(n)  
c) O(log n)  
d) O(n²)

---

**Q31.** Max heap root contains:

**a) Maximum element ✅**  
b) Minimum  
c) Median  
d) Random

---

**Q32.** Dijkstra's finds:

**a) Shortest path in weighted graph ✅**  
b) MST  
c) Topological order  
d) Longest path

---

**Q33.** Kruskal's and Prim's find:

**a) Minimum Spanning Tree ✅**  
b) Shortest path  
c) Topological sort  
d) All paths

---

**Q34.** Inorder traversal order:

**a) Left → Root → Right ✅**  
b) Root → Left → Right  
c) Left → Right → Root  
d) Right → Root → Left

---

**Q35.** Preorder: **Root → Left → Right ✅**

---

**Q36.** Postorder: **Left → Right → Root ✅**

---

**Q37.** AVL tree balance factor ≤ :

**a) 1 ✅**  
b) 2  
c) 0  
d) 3

---

**Q38.** Collision in hashing:

**a) Two keys map to same index ✅**  
b) Hash function error  
c) Overflow  
d) Key not found

---

**Q39.** Heap sort complexity:

**a) O(n log n) ✅**  
b) O(n)  
c) O(n²)  
d) O(log n)

---

**Q40.** Adjacency matrix space:

**a) O(V²) ✅**  
b) O(V+E)  
c) O(V)  
d) O(E)

---

**Q41.** Adjacency list best for:

**a) Sparse graphs ✅**  
b) Dense  
c) Complete  
d) All

---

**Q42.** Level order traversal uses:

**a) Queue ✅**  
b) Stack  
c) Heap  
d) Hash

---

**Q43.** Priority queue implemented using:

**a) Heap ✅**  
b) Array  
c) Linked list  
d) Stack

---

**Q44.** BST worst case search (skewed):

**a) O(n) ✅**  
b) O(log n)  
c) O(1)  
d) O(n²)

---

**Q45.** Inserting at head of singly linked list:

**a) O(1) ✅**  
b) O(n)  
c) O(log n)  
d) O(n²)

---

**Q46.** Topological sort works on:

**a) DAG (Directed Acyclic Graph) ✅**  
b) Undirected  
c) Trees  
d) Any

---

**Q47.** Bellman-Ford handles which Dijkstra cannot?

**a) Negative edge weights ✅**  
b) Weighted edges  
c) Undirected  
d) Dense

---

**Q48.** 2D Array A[5][10], Base = 1000, Size = 2. Find A[3][4] in Row-Major:

a) 1048  
b) 1064  
**c) 1068 ✅**  
d) 1072

> = 1000 + (3×10 + 4)×2 = 1000 + 34×2 = 1000 + 68 = 1068

---

**Q49.** Circular queue solves:

**a) Wasted space problem of simple queue ✅**  
b) Stack overflow  
c) Hash collision  
d) Tree imbalance

---

**Q50.** Graph with no cycles:

**a) Acyclic ✅**  
b) Cyclic  
c) Complete  
d) Dense

---

## Scenario / One-Line Answers

**S1.** Postfix evaluation: Scan left to right. Push operands. On operator, pop two, compute, push result.  
**S2.** 2D array Row-Major: Base + (i×Cols + j) × Size. Column-Major: Base + (j×Rows + i) × Size.  
**S3.** Stack is used for: recursion, parentheses matching, infix→postfix, reversing, undo. NOT for async data transfer (that's queue).  
**S4.** Splay tree is NOT balanced — it's self-adjusting (recently accessed element moved to root).  
**S5.** B-tree is the standard external memory (disk-based) data structure used in databases.  
**S6.** Deque = double-ended queue — insert/delete from BOTH front and rear.  
**S7.** Forest edges = V - K (vertices minus connected components).  
**S8.** Regular graph edges = (n × degree) / 2.  
**S9.** Vertex coloring = degree + 1 colors (Brook's theorem upper bound).  
**S10.** Floyd-Warshall: k=0 means no intermediate vertices, only direct edges considered.

---
