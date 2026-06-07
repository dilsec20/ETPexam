# Unit 5: Data Structures

---

## 5.1 Introduction
**Data Structure:** A way of organizing, storing, and managing data for efficient access and modification.

### Types:
| Type | Examples |
|---|---|
| **Linear** | Array, Linked List, Stack, Queue |
| **Non-Linear** | Tree, Graph |

### Array:
- Fixed-size, contiguous memory, O(1) random access by index
- Insertion/Deletion: O(n) (shifting required)

---

## 5.2 Linked Lists

| Type | Description |
|---|---|
| **Singly Linked List** | Each node has data + pointer to next node |
| **Doubly Linked List** | Each node has data + pointer to next + pointer to previous |
| **Circular Linked List** | Last node points back to the first node |

### Array vs Linked List:
| Feature | Array | Linked List |
|---|---|---|
| Size | Fixed | Dynamic |
| Access | O(1) random | O(n) sequential |
| Insertion/Deletion | O(n) | O(1) at head |
| Memory | Contiguous | Non-contiguous |
| Extra memory | None | Pointer overhead |

---

## 5.3 Stacks

**Stack:** LIFO (Last In, First Out). Like a stack of plates.

**Operations:**
| Operation | Description | Time |
|---|---|---|
| push(x) | Add element to top | O(1) |
| pop() | Remove top element | O(1) |
| peek()/top() | View top element | O(1) |
| isEmpty() | Check if empty | O(1) |

**Applications:** Function call stack, undo/redo, expression evaluation, backtracking, browser history, balanced parentheses check.

**Infix to Postfix:** Use stack to convert (e.g., A+B → AB+)
- **Infix:** A + B (operator between operands)
- **Prefix:** +AB (operator before operands)
- **Postfix:** AB+ (operator after operands)

---

## 5.4 Queues

**Queue:** FIFO (First In, First Out). Like a line at a shop.

**Operations:**
| Operation | Description | Time |
|---|---|---|
| enqueue(x) | Add element at rear | O(1) |
| dequeue() | Remove element from front | O(1) |
| front()/peek() | View front element | O(1) |

**Types:**
| Type | Description |
|---|---|
| **Simple Queue** | FIFO; insert at rear, delete from front |
| **Circular Queue** | Last position connects back to first; solves wasted space problem |
| **Priority Queue** | Elements dequeued based on priority, not arrival order |
| **Deque (Double-ended)** | Insert/delete from both front and rear |

**Applications:** CPU scheduling, BFS traversal, printer queue, buffering.

---

## 5.5 Trees

**Tree:** Non-linear hierarchical data structure with nodes connected by edges.

| Term | Definition |
|---|---|
| **Root** | Topmost node (no parent) |
| **Leaf** | Node with no children |
| **Height** | Longest path from root to leaf |
| **Depth** | Path from root to a node |
| **Degree** | Number of children of a node |
| **Parent/Child** | Direct ancestor/descendant |
| **Sibling** | Nodes with same parent |

### Binary Tree:
- Each node has at most **2 children** (left, right)
- **Full Binary Tree:** Every node has 0 or 2 children
- **Complete Binary Tree:** All levels filled except possibly the last (filled left to right)
- **Perfect Binary Tree:** All internal nodes have 2 children and all leaves at same level
- **Degenerate/Skewed:** Each node has only 1 child (like a linked list)

### Binary Search Tree (BST):
- Left child < Parent < Right child
- Search, Insert, Delete: O(log n) average, O(n) worst (skewed)
- **Inorder traversal of BST gives sorted output**

### Tree Traversals:
| Traversal | Order | Use |
|---|---|---|
| **Inorder** | Left → Root → Right | Sorted order (BST) |
| **Preorder** | Root → Left → Right | Copy tree |
| **Postorder** | Left → Right → Root | Delete tree |
| **Level Order** | Level by level (BFS) | BFS traversal |

### Balanced Trees:
| Tree | Property |
|---|---|
| **AVL Tree** | Height difference between left and right subtree ≤ 1 (balance factor) |
| **Red-Black Tree** | Self-balancing with color properties; used in Java TreeMap, C++ map |
| **B-Tree** | Multi-way search tree; used in databases and file systems |

---

## 5.6 Graphs

**Graph:** Non-linear structure with vertices (nodes) and edges (connections).

### Types:
| Type | Description |
|---|---|
| **Directed (Digraph)** | Edges have direction (A → B) |
| **Undirected** | Edges have no direction (A — B) |
| **Weighted** | Edges have weights/costs |
| **Unweighted** | All edges equal |
| **Cyclic** | Contains a cycle |
| **Acyclic** | No cycles (DAG = Directed Acyclic Graph) |

### Representation:
| Method | Space | Edge check | Best for |
|---|---|---|---|
| **Adjacency Matrix** | O(V²) | O(1) | Dense graphs |
| **Adjacency List** | O(V+E) | O(V) | Sparse graphs |

### Graph Algorithms:
| Algorithm | Purpose | Type |
|---|---|---|
| **BFS** | Shortest path (unweighted), level-order | Uses Queue |
| **DFS** | Cycle detection, topological sort | Uses Stack/Recursion |
| **Dijkstra's** | Shortest path (weighted, no negative edges) | Greedy |
| **Bellman-Ford** | Shortest path (handles negative edges) | DP |
| **Floyd-Warshall** | All-pairs shortest path | DP |
| **Kruskal's** | Minimum Spanning Tree (MST) | Greedy, uses edges |
| **Prim's** | Minimum Spanning Tree (MST) | Greedy, uses vertices |
| **Topological Sort** | Linear ordering of DAG vertices | DFS-based |

**BFS:** Uses **Queue** → Breadth-first, level by level  
**DFS:** Uses **Stack/Recursion** → Depth-first, goes as deep as possible

---

## 5.7 Hashing

**Hashing:** Technique to map data to a fixed-size value (hash) for O(1) average access.

| Term | Definition |
|---|---|
| **Hash Function** | Maps key to index: `h(key) = key % table_size` |
| **Hash Table** | Array-based structure using hash function for indexing |
| **Collision** | Two different keys map to the same index |

### Collision Resolution:
| Method | Description |
|---|---|
| **Chaining** | Each index stores a linked list of elements |
| **Open Addressing (Linear Probing)** | If collision, check next slot: `(h(k) + i) % size` |
| **Quadratic Probing** | `(h(k) + i²) % size` |
| **Double Hashing** | Use second hash function: `(h1(k) + i * h2(k)) % size` |

**Load Factor:** α = n/m (items/table size). Higher α = more collisions.

**Applications:** Dictionaries, caches, databases, password storage, symbol tables.

---

## 5.8 Heaps

**Heap:** Complete binary tree with heap property.

| Type | Property |
|---|---|
| **Max Heap** | Parent ≥ Children (root is maximum) |
| **Min Heap** | Parent ≤ Children (root is minimum) |

**Operations:**
| Operation | Time |
|---|---|
| Insert | O(log n) |
| Delete (root) | O(log n) |
| Get min/max | O(1) |
| Build heap | O(n) |

**Heap Sort:** Build max heap, repeatedly extract max → O(n log n)  
**Priority Queue** is commonly implemented using a heap.

---

## MCQ Practice Questions (50+)

---

**Q1.** Stack follows which principle?
A. FIFO  **B. LIFO ✅**  C. Random  D. Priority

---

**Q2.** Queue follows which principle?
**A. FIFO ✅**  B. LIFO  C. Random  D. FILO

---

**Q3.** Which traversal of BST gives sorted output?
**A. Inorder ✅**  B. Preorder  C. Postorder  D. Level order

---

**Q4.** BFS uses which data structure?
A. Stack  **B. Queue ✅**  C. Tree  D. Heap

---

**Q5.** DFS uses which data structure?
**A. Stack ✅**  B. Queue  C. Heap  D. Hash table

---

**Q6.** Array access by index is:
**A. O(1) ✅**  B. O(n)  C. O(log n)  D. O(n²)

---

**Q7.** Linked list search is:
A. O(1)  **B. O(n) ✅**  C. O(log n)  D. O(n²)

---

**Q8.** Hash table average search is:
**A. O(1) ✅**  B. O(n)  C. O(log n)  D. O(n²)

---

**Q9.** In a max heap, the root contains:
A. Minimum element  **B. Maximum element ✅**  C. Median  D. Random element

---

**Q10.** Dijkstra's algorithm finds:
**A. Shortest path in weighted graph ✅**  B. Minimum spanning tree  C. Topological order  D. Longest path

---

**Q11.** Kruskal's and Prim's algorithms find:
A. Shortest path  **B. Minimum Spanning Tree (MST) ✅**  C. Topological sort  D. All paths

---

**Q12.** Which linked list has a pointer to both next and previous?
A. Singly  **B. Doubly ✅**  C. Circular  D. Array

---

**Q13.** Inorder traversal order?
**A. Left → Root → Right ✅**  B. Root → Left → Right  C. Left → Right → Root  D. Right → Root → Left

---

**Q14.** Preorder traversal order?
A. Left → Root → Right  **B. Root → Left → Right ✅**  C. Left → Right → Root  D. Root → Right → Left

---

**Q15.** Postorder traversal order?
A. Root → Left → Right  B. Left → Root → Right  **C. Left → Right → Root ✅**  D. Right → Left → Root

---

**Q16.** AVL tree ensures balance factor ≤:
**A. 1 ✅**  B. 2  C. 0  D. 3

---

**Q17.** Collision in hashing means:
A. Hash function error  **B. Two keys map to the same index ✅**  C. Table overflow  D. Key not found

---

**Q18.** Chaining resolves collision using:
A. Open addressing  **B. Linked list at each index ✅**  C. Binary tree  D. Heap

---

**Q19.** Heap sort time complexity:
A. O(n)  **B. O(n log n) ✅**  C. O(n²)  D. O(log n)

---

**Q20.** Adjacency matrix space complexity:
A. O(V+E)  **B. O(V²) ✅**  C. O(V)  D. O(E)

---

**Q21.** Adjacency list is better for:
A. Dense graphs  **B. Sparse graphs ✅**  C. Complete graphs  D. All graphs

---

**Q22.** Stack application does NOT include:
A. Function calls  B. Undo operation  **C. BFS traversal ✅**  D. Balanced parentheses

---

**Q23.** Queue application:
A. DFS  B. Recursion  **C. CPU scheduling / BFS ✅**  D. Undo

---

**Q24.** Priority queue is implemented using:
A. Array  **B. Heap ✅**  C. Linked list  D. Stack

---

**Q25.** Full binary tree — every node has:
**A. 0 or 2 children ✅**  B. Exactly 2  C. At most 1  D. Any number

---

**Q26.** BST: Left child value is _____ than parent:
**A. Less ✅**  B. Greater  C. Equal  D. Random

---

**Q27.** Topological sort works on:
A. Undirected graphs  **B. DAG (Directed Acyclic Graph) ✅**  C. Trees  D. Any graph

---

**Q28.** Bellman-Ford handles _____ which Dijkstra's cannot:
A. Weighted edges  **B. Negative edge weights ✅**  C. Undirected graphs  D. Dense graphs

---

**Q29.** Floyd-Warshall finds:
A. Single source shortest path  **B. All-pairs shortest path ✅**  C. MST  D. Topological sort

---

**Q30.** Load factor in hashing = ?
A. table_size / items  **B. items / table_size ✅**  C. items × table_size  D. items + table_size

---

**Q31.** Linear probing formula:
A. h(k) + i²  **B. (h(k) + i) % size ✅**  C. h(k) * i  D. h(k) - i

---

**Q32.** Deque allows:
A. Insert at rear only  B. Delete from front only  **C. Insert/delete from both ends ✅**  D. Random access

---

**Q33.** Circular queue solves:
**A. Wasted space problem of simple queue ✅**  B. Stack overflow  C. Hash collision  D. Tree imbalance

---

**Q34.** Worst case BST search (skewed tree):
A. O(1)  B. O(log n)  **C. O(n) ✅**  D. O(n²)

---

**Q35.** Red-Black tree is used in:
**A. Java TreeMap, C++ map ✅**  B. Databases  C. Operating systems  D. Compilers

---

**Q36.** B-Tree is used in:
A. Games  **B. Databases and file systems ✅**  C. Networking  D. Graphics

---

**Q37.** Graph with no cycles is called:
A. Cyclic  **B. Acyclic ✅**  C. Complete  D. Dense

---

**Q38.** DAG stands for:
**A. Directed Acyclic Graph ✅**  B. Dynamic Array Graph  C. Data Allocation Graph  D. Directed Allocation Group

---

**Q39.** Inserting at the head of a singly linked list is:
**A. O(1) ✅**  B. O(n)  C. O(log n)  D. O(n²)

---

**Q40.** Stack overflow occurs when:
A. Stack is empty  **B. Stack is full (or infinite recursion) ✅**  C. Pop from empty  D. Push is slow

---

**Q41.** Stack underflow occurs when:
**A. Pop from an empty stack ✅**  B. Stack is full  C. Push fails  D. Peek fails

---

**Q42.** Level order traversal uses:
A. Stack  **B. Queue ✅**  C. Heap  D. Hash

---

**Q43.** Expression "AB+CD-*" is in:
A. Infix  B. Prefix  **C. Postfix ✅**  D. Invalid

---

**Q44.** The height of a balanced BST with n nodes is approximately:
A. n  **B. log₂(n) ✅**  C. n²  D. √n

---

**Q45.** Minimum element in a min heap is at:
**A. Root ✅**  B. Last leaf  C. Any position  D. Leftmost leaf

---

**Q46.** Prim's algorithm uses:
A. Edges sorted by weight  **B. Vertex-based greedy approach ✅**  C. DFS  D. BFS

---

**Q47.** Kruskal's algorithm uses:
**A. Edges sorted by weight ✅**  B. Vertex-based approach  C. DFS  D. Queue

---

**Q48.** Hash function h(k) = k % 10. h(25) = ?
A. 2  **B. 5 ✅**  C. 25  D. 10

---

**Q49.** Which graph representation checks edge existence in O(1)?
**A. Adjacency Matrix ✅**  B. Adjacency List  C. Edge List  D. Incidence Matrix

---

**Q50.** Complete binary tree with n nodes has height:
A. n  **B. ⌊log₂(n)⌋ ✅**  C. n/2  D. 2n

---

## Scenario & One-Line Answer Questions

---

**S1.** You need to check if parentheses are balanced: `{[()]}`. Which data structure?
> **Stack** — push opening brackets, pop on closing bracket, check match.

**S2.** You need to find the shortest path in an unweighted graph. Which algorithm?
> **BFS** (Breadth-First Search) — gives shortest path in unweighted graphs.

**S3.** You have a dictionary where you need O(1) average lookup. Which data structure?
> **Hash Table** — provides O(1) average-case search, insert, and delete.

**S4.** What is the difference between a stack and a queue?
> **Stack** is LIFO (last in, first out). **Queue** is FIFO (first in, first out).

**S5.** Inorder traversal of a BST with values [5, 3, 7, 1, 4] gives?
> **1, 3, 4, 5, 7** — Inorder traversal of BST always gives sorted order.

**S6.** What is the difference between BFS and DFS?
> **BFS** explores neighbors first (uses queue, level by level). **DFS** explores as deep as possible (uses stack/recursion, branch by branch).

**S7.** Why is hash table search O(1) but can degrade to O(n)?
> Average case is O(1) due to direct indexing. Worst case is O(n) when all keys collide into the same index (all in one chain).

**S8.** When would you use a linked list over an array?
> When you need **frequent insertions/deletions** and don't need random access. Linked list has O(1) insertion at head; array requires O(n) shifting.

**S9.** What is the difference between a min heap and max heap?
> **Min heap**: root = minimum, parent ≤ children. **Max heap**: root = maximum, parent ≥ children.

**S10.** What is the time complexity of inserting into a BST?
> **O(log n)** average case (balanced), **O(n)** worst case (skewed/degenerate tree).

---
