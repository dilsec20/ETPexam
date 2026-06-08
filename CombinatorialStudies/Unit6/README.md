# Unit 6: Algorithms

---

## 6.1 Understanding Algorithms

**Algorithm:** Step-by-step procedure for solving a problem in finite steps.

### Properties: Input, Output, Definiteness, Finiteness, Effectiveness

---

## 6.2 Running Time Analysis & Asymptotic Notation

### Growth Rate (Fastest → Slowest):
```
O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(n³) < O(2ⁿ) < O(n!)
```

### Asymptotic Notations:
| Notation | Meaning | Represents |
|---|---|---|
| **Big-O (O)** | Upper bound | Worst case |
| **Omega (Ω)** | Lower bound | Best case |
| **Theta (Θ)** | Tight bound | Average/exact |

### Rules:
- Drop constants: O(5n) = O(n)
- Drop lower terms: O(n² + n) = O(n²)
- Single loop = O(n), nested = O(n²), triple nested = O(n³)

---

## 6.3 Sorting Algorithms

| Algorithm | Best | Average | Worst | Stable | In-Place |
|---|---|---|---|---|---|
| **Bubble Sort** | O(n) | O(n²) | **O(n²)** | ✅ Yes | ✅ Yes |
| **Selection Sort** | O(n²) | O(n²) | O(n²) | ❌ No | ✅ Yes |
| **Insertion Sort** | **O(n)** | O(n²) | O(n²) | ✅ Yes | ✅ Yes |
| **Merge Sort** | O(n log n) | O(n log n) | O(n log n) | ✅ Yes | ❌ O(n) |
| **Quick Sort** | O(n log n) | O(n log n) | **O(n²)** | ❌ No | ✅ Yes |
| **Heap Sort** | O(n log n) | O(n log n) | O(n log n) | ❌ No | ✅ Yes |

> **PYQ: Bubble sort complexity? → O(n²)** ✅

### Insertion Sort:
- Starts with the **2nd element** (index 1), compares with previous elements
- Best for **nearly sorted data** — O(n) best case

> **PYQ: Insertion sort begins with the _____ element → b) Second** ✅

### Selection Sort Pass-by-Pass:
**PYQ: Third pass of selection sort for list 3, 5, 4, 1, 2:**
```
Original: 3, 5, 4, 1, 2
Pass 1: Find min(3,5,4,1,2)=1, swap with pos 0 → 1, 5, 4, 3, 2
Pass 2: Find min(5,4,3,2)=2, swap with pos 1   → 1, 2, 4, 3, 5
Pass 3: Find min(4,3,5)=3, swap with pos 2      → 1, 2, 3, 4, 5
```
> **PYQ Answer: b) 1, 2, 3, 4, 5** ✅

---

## 6.4 Searching

| Algorithm | Time | Requirement |
|---|---|---|
| **Linear Search** | O(n) | None |
| **Binary Search** | **O(log n)** | **Sorted array** |

---

## 6.5 Recursion and Backtracking

### Recursion:
- Function calls itself
- **Base case** prevents infinite recursion → stack overflow
- Uses **Stack** data structure

### Common: Factorial, Fibonacci, Tower of Hanoi, Tree traversals

### Backtracking:
Try a choice → if it fails → **undo and try next** (N-Queens, Sudoku, Maze)

---

## 6.6 Dynamic Programming (DP)

**DP:** Break into **overlapping subproblems**, store solutions to avoid recomputation.

### Requirements:
1. **Optimal Substructure** — optimal solution from optimal sub-solutions
2. **Overlapping Subproblems** — same subproblems solved repeatedly

### Approaches:
| Approach | Description |
|---|---|
| **Top-Down (Memoization)** | Recursion + cache |
| **Bottom-Up (Tabulation)** | Iterative, fill table |

> **PYQ: Algorithm that uses past results to find new results → c) Dynamic Programming** ✅

### Classic DP: Fibonacci, LCS, Knapsack 0/1, Coin Change, Edit Distance

### Divide & Conquer vs DP:
| Feature | D&C | DP |
|---|---|---|
| Subproblems | Non-overlapping | Overlapping |
| Example | Merge Sort, Quick Sort | Fibonacci, Knapsack |

> **PYQ: Combining optimal solutions to non-overlapping subproblems → c) Divide and Conquer** ✅

---

## 6.7 Greedy Algorithms

**Greedy:** Make **locally optimal choice** at each step. Does NOT always give optimal solution.

### Classic Greedy:
- Activity Selection (earliest finish time)
- **Fractional Knapsack** (value/weight ratio)
- Huffman Coding
- Dijkstra's shortest path
- Prim's/Kruskal's MST
- **Coin Change (greedy)** — pick largest coin first

### Greedy Coin Change — When It FAILS:
**PYQ: Coins = {1, 3, 4}. Greedy picks largest first. For which sum does it NOT give optimal?**

For sum = 6:
- Greedy: 4+1+1 = 3 coins
- Optimal: 3+3 = 2 coins → **Greedy FAILS for 6** ✅

For sum = 10: Greedy: 4+4+1+1=4 coins, Optimal: 4+3+3=3 coins → also fails  
For sum = 14: Greedy: 4+4+4+1+1=5, Optimal: 4+4+3+3=4 → fails  

> **PYQ Answer: c) 6** ✅ (simplest failing case)

### Greedy vs DP:
| Feature | Greedy | DP |
|---|---|---|
| Optimal always? | Not always | Yes |
| Speed | Faster | Can be slower |
| Example | Fractional Knapsack | 0/1 Knapsack |

---

## MCQ Practice Questions (50+ PYQ Style)

---

**Q1.** An algorithm which uses past results to find new results is:

a) Brute Force  
b) Divide and Conquer  
**c) Dynamic Programming ✅**  
d) None

---

**Q2.** Insertion sort starts with the _____ element:

a) First  
**b) Second ✅**  
c) Third  
d) Fourth

---

**Q3.** Third pass of selection sort for list 3, 5, 4, 1, 2:

a) 1, 2, 4, 3, 5  
**b) 1, 2, 3, 4, 5 ✅**  
c) 1, 5, 4, 3, 2  
d) 3, 5, 4, 1, 2

---

**Q4.** Bubble sort complexity:

a) O(log n)  
b) O(n)  
**c) O(n²) ✅**  
d) O(n log n)

---

**Q5.** Combining optimal solutions to non-overlapping subproblems:

a) Dynamic Programming  
b) Greedy  
**c) Divide and Conquer ✅**  
d) Recursion

---

**Q6.** Coins {1, 3, 4}, greedy (largest first). Which sum does NOT give optimal?

a) 100  
b) 10  
**c) 6 ✅**  
d) 14

---

**Q7.** Big-O represents:

**a) Upper bound / Worst case ✅**  
b) Best case  
c) Average  
d) Exact

---

**Q8.** Binary search complexity:

**a) O(log n) ✅**  
b) O(n)  
c) O(n²)  
d) O(1)

---

**Q9.** Binary search requires:

**a) Sorted array ✅**  
b) Unsorted  
c) Linked list  
d) Hash table

---

**Q10.** Quick sort worst case:

a) O(n log n)  
**b) O(n²) ✅**  
c) O(n)  
d) O(log n)

---

**Q11.** Merge sort (all cases):

**a) O(n log n) ✅**  
b) O(n²)  
c) O(n)  
d) O(log n)

---

**Q12.** Which sort is NOT stable?

a) Merge Sort  
b) Bubble Sort  
**c) Quick Sort ✅**  
d) Insertion Sort

---

**Q13.** Greedy always gives optimal?

**a) No, not always ✅**  
b) Yes always

---

**Q14.** DP requires:

**a) Overlapping subproblems + optimal substructure ✅**  
b) Non-overlapping  
c) No subproblems  
d) Random choice

---

**Q15.** Naive recursive Fibonacci:

**a) O(2ⁿ) ✅**  
b) O(n)  
c) O(n²)  
d) O(log n)

---

**Q16.** DP Fibonacci (bottom-up):

**a) O(n) ✅**  
b) O(2ⁿ)  
c) O(n²)  
d) O(n log n)

---

**Q17.** Base case prevents:

**a) Infinite recursion / stack overflow ✅**  
b) Compilation error  
c) Memory leak  
d) Syntax error

---

**Q18.** Merge sort uses:

**a) Divide and Conquer ✅**  
b) Greedy  
c) DP  
d) Backtracking

---

**Q19.** Insertion sort best case:

**a) O(n) ✅**  
b) O(n²)  
c) O(n log n)  
d) O(1)

---

**Q20.** Selection sort is:

**a) Not stable ✅**  
b) Stable  
c) Both  
d) Neither

---

**Q21.** O(1) means:

**a) Constant time ✅**  
b) Linear  
c) Logarithmic  
d) Quadratic

---

**Q22.** Space complexity of merge sort:

**a) O(n) ✅**  
b) O(1)  
c) O(log n)  
d) O(n²)

---

**Q23.** Omega (Ω) represents:

**a) Lower bound ✅**  
b) Upper bound  
c) Tight bound  
d) Exact

---

**Q24.** Theta (Θ) represents:

**a) Tight bound ✅**  
b) Upper  
c) Lower  
d) None

---

**Q25.** O(5n + 3) = ?

**a) O(n) ✅**  
b) O(5n)  
c) O(3)  
d) O(5n+3)

---

**Q26.** O(n² + n + 1) = ?

**a) O(n²) ✅**  
b) O(n)  
c) O(1)  
d) O(n²+n)

---

**Q27.** Two nested loops of n:

**a) O(n²) ✅**  
b) O(n)  
c) O(2n)  
d) O(n log n)

---

**Q28.** Fractional Knapsack uses:

**a) Greedy ✅**  
b) DP  
c) Backtracking  
d) Brute force

---

**Q29.** 0/1 Knapsack uses:

**a) Dynamic Programming ✅**  
b) Greedy  
c) Backtracking  
d) Linear search

---

**Q30.** Tower of Hanoi moves for n disks:

**a) 2ⁿ - 1 ✅**  
b) n  
c) n²  
d) n!

---

**Q31.** Memoization is:

**a) Top-down DP ✅**  
b) Bottom-up  
c) Greedy  
d) Brute force

---

**Q32.** Tabulation is:

**a) Bottom-up DP ✅**  
b) Top-down  
c) Greedy  
d) Recursive

---

**Q33.** Dijkstra cannot handle:

**a) Negative edge weights ✅**  
b) Weighted edges  
c) Undirected  
d) Dense

---

**Q34.** Best sort for nearly sorted data:

**a) Insertion Sort ✅**  
b) Quick Sort  
c) Merge Sort  
d) Selection Sort

---

**Q35.** Counting sort is:

**a) Non-comparison sort ✅**  
b) Comparison sort  
c) In-place  
d) Unstable

---

**Q36.** In-place sorting means:

**a) O(1) extra space ✅**  
b) O(n) space  
c) Not stable  
d) Uses recursion

---

**Q37.** Linear search worst case:

**a) O(n) ✅**  
b) O(log n)  
c) O(1)  
d) O(n²)

---

**Q38.** Recurrence T(n) = 2T(n/2) + n →

**a) O(n log n) — Merge Sort ✅**  
b) O(log n)  
c) O(n)  
d) O(n²)

---

**Q39.** Recurrence T(n) = T(n/2) + O(1) →

**a) O(log n) — Binary Search ✅**  
b) O(n)  
c) O(n log n)  
d) O(n²)

---

**Q40.** Activity Selection uses:

**a) Greedy (earliest finish time) ✅**  
b) DP  
c) Backtracking  
d) Brute force

---

**Q41.** N-Queens solved by:

**a) Backtracking ✅**  
b) Greedy  
c) DP  
d) Sorting

---

**Q42.** LCS (Longest Common Subsequence) uses:

**a) Dynamic Programming ✅**  
b) Greedy  
c) Backtracking  
d) Sorting

---

**Q43.** Which is faster: O(n) or O(n log n)?

**a) O(n) ✅**  
b) O(n log n)  
c) Same  
d) Depends

---

**Q44.** Heap sort space:

**a) O(1) ✅**  
b) O(n)  
c) O(log n)  
d) O(n²)

---

**Q45.** Quick sort worst case occurs when:

**a) Array is already sorted (bad pivot) ✅**  
b) Array random  
c) Array unique  
d) Small array

---

**Q46.** Stable sort means:

**a) Equal elements maintain original relative order ✅**  
b) Never crashes  
c) Less memory  
d) Always O(n log n)

---

**Q47.** Brute force:

**a) Tries all possible solutions ✅**  
b) Greedy choice  
c) DP table  
d) Recursion only

---

**Q48.** Correct growth order:

a) O(n²) < O(n) < O(log n)  
b) O(n!) < O(2ⁿ) < O(n²)  
**c) O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(2ⁿ) < O(n!) ✅**  
d) O(log n) < O(1) < O(n)

---

**Q49.** Quick sort average:

**a) O(n log n) ✅**  
b) O(n²)  
c) O(n)  
d) O(2ⁿ)

---

**Q50.** O(n log n) is the lower bound for:

**a) Comparison-based sorting ✅**  
b) All sorting  
c) Searching  
d) Hashing

---

## Scenario / One-Line Answers

**S1.** Insertion sort starts with 2nd element, compares with elements before it, shifts them right to insert correctly.  
**S2.** Selection sort: In each pass, find minimum in unsorted portion, swap with first unsorted position.  
**S3.** Greedy coin {1,3,4} for sum 6: Greedy gives 4+1+1=3 coins; Optimal is 3+3=2 coins → greedy fails.  
**S4.** DP uses past results; D&C splits into independent non-overlapping subproblems.  
**S5.** Bubble sort: Compare adjacent, swap if wrong order. O(n²). Best O(n) with flag optimization.  
**S6.** Quick sort worst case: already sorted array with poor pivot (first/last element) → O(n²).  
**S7.** Binary search requires sorted array; halves search space each step → O(log n).  
**S8.** Stable sort: if two elements have equal keys, their relative order is preserved. Merge, Bubble, Insertion are stable.  
**S9.** Tower of Hanoi: n disks → 2ⁿ - 1 moves. For 3 disks = 7 moves.  
**S10.** Dijkstra = Greedy. Floyd-Warshall = DP. Bellman-Ford = DP. Kruskal/Prim = Greedy.

---
