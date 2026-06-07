# Unit 6: Algorithms

---

## 6.1 Understanding Algorithms

**Algorithm:** A step-by-step, well-defined procedure for solving a problem in a finite number of steps.

### Properties of an Algorithm:
1. **Input** — Zero or more inputs
2. **Output** — At least one output
3. **Definiteness** — Each step is clear and unambiguous
4. **Finiteness** — Must terminate after a finite number of steps
5. **Effectiveness** — Each step is basic enough to be carried out

---

## 6.2 Running Time Analysis & Rate of Growth

### Common Time Complexities (Fastest → Slowest):

| Notation | Name | Example |
|---|---|---|
| O(1) | Constant | Array access, hash table lookup |
| O(log n) | Logarithmic | Binary search |
| O(n) | Linear | Linear search, traversal |
| O(n log n) | Linearithmic | Merge sort, Quick sort (avg) |
| O(n²) | Quadratic | Bubble sort, Selection sort, Insertion sort |
| O(n³) | Cubic | Floyd-Warshall, naive matrix multiply |
| O(2ⁿ) | Exponential | Recursive Fibonacci (naive), subsets |
| O(n!) | Factorial | Permutations, brute-force TSP |

### Growth Rate Order:
```
O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(n³) < O(2ⁿ) < O(n!)
```

---

## 6.3 Asymptotic Notation

| Notation | Meaning | Represents |
|---|---|---|
| **Big-O (O)** | Upper bound | Worst case (at most) |
| **Omega (Ω)** | Lower bound | Best case (at least) |
| **Theta (Θ)** | Tight bound | Average / exact growth rate |
| **Little-o (o)** | Strict upper bound | Grows strictly slower |
| **Little-omega (ω)** | Strict lower bound | Grows strictly faster |

**Big-O:** f(n) = O(g(n)) means f(n) ≤ c·g(n) for all n ≥ n₀

### Rules for Big-O:
1. **Drop constants:** O(5n) = O(n)
2. **Drop lower-order terms:** O(n² + n) = O(n²)
3. **Loops:** Single loop = O(n), nested loops = O(n²)
4. **Sequential:** O(A) + O(B) = O(max(A, B))
5. **Nested:** O(A) × O(B) = O(A × B)

---

## 6.4 Sorting Algorithms

| Algorithm | Best | Average | Worst | Space | Stable | Method |
|---|---|---|---|---|---|---|
| **Bubble Sort** | O(n) | O(n²) | O(n²) | O(1) | Yes | Comparison |
| **Selection Sort** | O(n²) | O(n²) | O(n²) | O(1) | No | Comparison |
| **Insertion Sort** | O(n) | O(n²) | O(n²) | O(1) | Yes | Comparison |
| **Merge Sort** | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes | Divide & Conquer |
| **Quick Sort** | O(n log n) | O(n log n) | O(n²) | O(log n) | No | Divide & Conquer |
| **Heap Sort** | O(n log n) | O(n log n) | O(n log n) | O(1) | No | Comparison |
| **Counting Sort** | O(n+k) | O(n+k) | O(n+k) | O(k) | Yes | Non-comparison |
| **Radix Sort** | O(nk) | O(nk) | O(nk) | O(n+k) | Yes | Non-comparison |

**Stable sort:** Preserves relative order of equal elements.  
**In-place sort:** Uses O(1) extra space (Bubble, Selection, Insertion, Heap, Quick).

---

## 6.5 Searching Algorithms

| Algorithm | Time (Avg) | Requirement |
|---|---|---|
| **Linear Search** | O(n) | None (unsorted OK) |
| **Binary Search** | O(log n) | Array must be **sorted** |

**Binary Search:** Repeatedly divide search space in half.
```
Compare target with middle element:
- If equal → found
- If target < middle → search left half
- If target > middle → search right half
```

---

## 6.6 Recursion and Backtracking

### Recursion:
A function that **calls itself** to solve smaller subproblems until reaching a **base case**.

```
factorial(n):
    if n == 0: return 1        ← Base case
    return n * factorial(n-1)  ← Recursive case
```

### Key Concepts:
- **Base case:** Condition that stops recursion (without it → infinite recursion → stack overflow)
- **Recursive case:** The function calls itself with a smaller input
- **Call stack:** Each recursive call adds a frame to the stack

### Common Recursive Problems:
- Factorial, Fibonacci, Tower of Hanoi, Binary search, Tree traversals, Merge sort

### Backtracking:
An algorithmic technique that explores all possibilities by **trying a choice**, and if it doesn't work, **undoing it (backtracking)** and trying the next option.

**Template:**
```
solve(state):
    if is_solution(state): return state
    for each choice:
        make_choice()
        if solve(next_state): return true
        undo_choice()   ← backtrack
    return false
```

**Classic Problems:** N-Queens, Sudoku solver, Maze solving, Subset sum, Permutations.

---

## 6.7 Dynamic Programming (DP)

**Dynamic Programming:** Solving complex problems by breaking them into **overlapping subproblems** and storing solutions to avoid redundant computation.

### Key Properties:
1. **Optimal Substructure** — Optimal solution contains optimal solutions of subproblems
2. **Overlapping Subproblems** — Same subproblems solved multiple times

### Approaches:
| Approach | Description |
|---|---|
| **Top-Down (Memoization)** | Recursion + cache results in array/map |
| **Bottom-Up (Tabulation)** | Iterative, fill table from smallest subproblem up |

### Fibonacci — DP vs Recursion:
```
// Naive recursion: O(2ⁿ) — exponential!
fib(n) = fib(n-1) + fib(n-2)

// DP (Bottom-Up): O(n)
dp[0] = 0, dp[1] = 1
for i = 2 to n: dp[i] = dp[i-1] + dp[i-2]
```

### Classic DP Problems:
- Fibonacci, Longest Common Subsequence (LCS), Longest Increasing Subsequence (LIS), 0/1 Knapsack, Coin Change, Matrix Chain Multiplication, Edit Distance

### Divide & Conquer vs Dynamic Programming:
| Feature | D&C | DP |
|---|---|---|
| Subproblems | Non-overlapping | Overlapping |
| Approach | Recursive | Recursive + memoize or iterative |
| Example | Merge Sort, Quick Sort | Fibonacci, Knapsack |

---

## 6.8 Greedy Algorithms

**Greedy Algorithm:** Makes the **locally optimal choice** at each step, hoping to find the **global optimum**. Does NOT always give the optimal solution.

### Properties:
1. **Greedy Choice Property** — Local optimal choice leads to global optimal
2. **Optimal Substructure** — Optimal solution contains optimal solutions of subproblems

### Classic Greedy Problems:
| Problem | Greedy Strategy |
|---|---|
| **Activity Selection** | Select activity with earliest finish time |
| **Fractional Knapsack** | Select items with highest value/weight ratio |
| **Huffman Coding** | Build tree with lowest frequency nodes first |
| **Dijkstra's** | Always pick unvisited vertex with smallest distance |
| **Prim's / Kruskal's MST** | Pick minimum weight edge |
| **Job Scheduling** | Select jobs with maximum profit/deadline |
| **Coin Change (greedy)** | Pick largest coin first (works for standard denominations) |

### Greedy vs DP:
| Feature | Greedy | DP |
|---|---|---|
| Makes choice | Before solving subproblem | After solving subproblems |
| Optimal always? | Not always | Yes (if applicable) |
| Speed | Usually faster | Can be slower |
| Example | Fractional Knapsack | 0/1 Knapsack |

---

## MCQ Practice Questions (50+)

---

**Q1.** Big-O notation represents:
A. Best case  **B. Upper bound / Worst case ✅**  C. Average case  D. Exact case

---

**Q2.** Binary search time complexity:
A. O(n)  **B. O(log n) ✅**  C. O(n²)  D. O(1)

---

**Q3.** Binary search requires:
A. Unsorted array  **B. Sorted array ✅**  C. Linked list  D. Hash table

---

**Q4.** Which sorting algorithm has worst case O(n²)?
A. Merge Sort  **B. Quick Sort ✅**  C. Heap Sort  D. Counting Sort

---

**Q5.** Merge sort time complexity (all cases):
**A. O(n log n) ✅**  B. O(n²)  C. O(n)  D. O(log n)

---

**Q6.** Which sort is NOT stable?
A. Merge Sort  B. Bubble Sort  **C. Quick Sort ✅**  D. Insertion Sort

---

**Q7.** Greedy algorithm always gives optimal solution:
A. True  **B. False — not always ✅**

---

**Q8.** Dynamic Programming requires:
A. Non-overlapping subproblems  **B. Overlapping subproblems + optimal substructure ✅**  C. No subproblems  D. Random choice

---

**Q9.** Naive recursive Fibonacci has complexity:
A. O(n)  **B. O(2ⁿ) ✅**  C. O(n²)  D. O(log n)

---

**Q10.** DP Fibonacci (bottom-up) has complexity:
**A. O(n) ✅**  B. O(2ⁿ)  C. O(n²)  D. O(n log n)

---

**Q11.** Backtracking is used for:
A. Sorting  **B. N-Queens, Sudoku, maze solving ✅**  C. Searching  D. Hashing

---

**Q12.** Base case in recursion prevents:
A. Compilation error  **B. Infinite recursion / stack overflow ✅**  C. Memory leak  D. Syntax error

---

**Q13.** Which sort uses divide and conquer?
A. Bubble Sort  **B. Merge Sort ✅**  C. Selection Sort  D. Insertion Sort

---

**Q14.** Insertion sort best case is:
**A. O(n) ✅**  B. O(n²)  C. O(n log n)  D. O(1)

---

**Q15.** Selection sort is:
A. Stable  **B. Not stable ✅**  C. In-place and stable  D. Not in-place

---

**Q16.** O(1) means:
**A. Constant time ✅**  B. Linear time  C. Logarithmic  D. Quadratic

---

**Q17.** O(n log n) is faster than:
A. O(log n)  B. O(n)  **C. O(n²) ✅**  D. O(1)

---

**Q18.** Space complexity of merge sort:
A. O(1)  **B. O(n) ✅**  C. O(log n)  D. O(n²)

---

**Q19.** Quick sort average case:
**A. O(n log n) ✅**  B. O(n²)  C. O(n)  D. O(2ⁿ)

---

**Q20.** Omega (Ω) notation represents:
A. Upper bound  **B. Lower bound ✅**  C. Tight bound  D. Exact value

---

**Q21.** Theta (Θ) notation represents:
A. Upper bound  B. Lower bound  **C. Tight bound ✅**  D. None

---

**Q22.** Drop constants rule: O(5n + 3) = ?
A. O(5n)  **B. O(n) ✅**  C. O(3)  D. O(5n+3)

---

**Q23.** Drop lower terms: O(n² + n + 1) = ?
**A. O(n²) ✅**  B. O(n)  C. O(1)  D. O(n²+n)

---

**Q24.** Two nested loops of n each: complexity?
A. O(n)  **B. O(n²) ✅**  C. O(2n)  D. O(n log n)

---

**Q25.** Fractional Knapsack uses:
**A. Greedy ✅**  B. DP  C. Backtracking  D. Brute force

---

**Q26.** 0/1 Knapsack uses:
A. Greedy  **B. Dynamic Programming ✅**  C. Backtracking  D. Linear search

---

**Q27.** Dijkstra's algorithm is:
**A. Greedy ✅**  B. DP  C. Backtracking  D. Divide and conquer

---

**Q28.** Huffman coding is:
**A. Greedy ✅**  B. DP  C. Brute force  D. Backtracking

---

**Q29.** Tower of Hanoi with n disks requires how many moves?
A. n  B. n²  **C. 2ⁿ - 1 ✅**  D. n!

---

**Q30.** Memoization is a _____ approach:
**A. Top-down DP ✅**  B. Bottom-up DP  C. Greedy  D. Brute force

---

**Q31.** Tabulation is a _____ approach:
A. Top-down  **B. Bottom-up DP ✅**  C. Greedy  D. Recursive

---

**Q32.** Which algorithm cannot handle negative edge weights?
**A. Dijkstra's ✅**  B. Bellman-Ford  C. Floyd-Warshall  D. BFS

---

**Q33.** Bubble sort makes how many passes in worst case for n elements?
A. 1  **B. n-1 ✅**  C. n  D. n²

---

**Q34.** Best case of bubble sort (optimized):
**A. O(n) ✅**  B. O(n²)  C. O(n log n)  D. O(1)

---

**Q35.** Which sorting is best for nearly sorted data?
A. Quick Sort  B. Merge Sort  **C. Insertion Sort ✅**  D. Selection Sort

---

**Q36.** Counting sort is _____ comparison sort:
A. A  **B. Not a (non-comparison) ✅**  C. Stable  D. In-place

---

**Q37.** In-place sorting means:
**A. Uses O(1) extra space ✅**  B. Uses O(n) space  C. Not stable  D. Uses recursion

---

**Q38.** Linear search worst case:
**A. O(n) ✅**  B. O(log n)  C. O(1)  D. O(n²)

---

**Q39.** Recurrence T(n) = 2T(n/2) + n represents:
**A. Merge Sort — O(n log n) ✅**  B. Binary Search  C. Fibonacci  D. Bubble Sort

---

**Q40.** Recurrence T(n) = T(n/2) + O(1) represents:
A. Merge Sort  **B. Binary Search — O(log n) ✅**  C. Linear Search  D. Fibonacci

---

**Q41.** Activity Selection Problem is solved by:
**A. Greedy (earliest finish time) ✅**  B. DP  C. Backtracking  D. Brute force

---

**Q42.** N-Queens problem is solved by:
A. Greedy  B. DP  **C. Backtracking ✅**  D. Sorting

---

**Q43.** Longest Common Subsequence (LCS) uses:
A. Greedy  **B. Dynamic Programming ✅**  C. Backtracking  D. Sorting

---

**Q44.** Which is faster: O(n) or O(n log n)?
**A. O(n) ✅**  B. O(n log n)  C. Same  D. Depends

---

**Q45.** Heap sort space complexity:
**A. O(1) ✅**  B. O(n)  C. O(log n)  D. O(n²)

---

**Q46.** Quick sort worst case occurs when:
A. Array is random  **B. Array is already sorted (bad pivot) ✅**  C. Array has unique elements  D. Array is small

---

**Q47.** Master Theorem is used to solve:
A. Any equation  **B. Divide and conquer recurrences ✅**  C. DP problems  D. Greedy problems

---

**Q48.** What does "stable sort" mean?
**A. Equal elements maintain their original relative order ✅**  B. Algorithm never crashes  C. Uses less memory  D. Always O(n log n)

---

**Q49.** Brute force approach:
**A. Tries all possible solutions ✅**  B. Makes greedy choice  C. Uses DP table  D. Uses recursion only

---

**Q50.** Which is the correct growth order?
A. O(n²) < O(n) < O(log n)  
B. O(n!) < O(2ⁿ) < O(n²)  
**C. O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(2ⁿ) < O(n!) ✅**  
D. O(log n) < O(1) < O(n)

---

## Scenario & One-Line Answer Questions

---

**S1.** You need to sort 1 million integers. Which algorithm would you choose and why?
> **Merge Sort** or **Quick Sort** — both are O(n log n). Merge Sort is stable and consistent; Quick Sort is faster in practice with good pivot selection.

**S2.** You are given a sorted array and need to find if a number exists. Which algorithm?
> **Binary Search** — O(log n), requires sorted array. Much faster than linear search O(n).

**S3.** What is the difference between recursion and iteration?
> **Recursion** solves a problem by calling itself (uses call stack, can cause stack overflow). **Iteration** uses loops (while/for). Iteration is generally more space-efficient.

**S4.** When does Dynamic Programming outperform Greedy?
> When the greedy choice does NOT lead to the optimal solution. Example: 0/1 Knapsack — greedy fails but DP gives the optimal answer.

**S5.** What is memoization?
> Storing the results of expensive function calls and returning the cached result when the same inputs occur again. It's the **top-down approach** to DP.

**S6.** Why is Quick Sort preferred over Merge Sort in practice?
> Quick Sort has better **cache performance** (in-place, sequential access) and lower constant factors, despite having O(n²) worst case (rare with good pivot).

**S7.** What is the difference between Divide and Conquer and Dynamic Programming?
> **D&C** divides into **independent, non-overlapping** subproblems (Merge Sort). **DP** has **overlapping** subproblems and stores solutions to avoid recomputation (Fibonacci).

**S8.** Explain backtracking in one line.
> Backtracking is a systematic search that tries choices, and **undoes them (backtracks)** when they lead to dead ends.

**S9.** What is the time complexity of accessing the i-th element in an array vs linked list?
> **Array: O(1)** (direct index access). **Linked List: O(n)** (must traverse from head).

**S10.** Big-O of three nested loops each running n times?
> **O(n³)** — each loop contributes a factor of n.

**S11.** What is the significance of O(n log n) in sorting?
> O(n log n) is the **theoretical lower bound** for comparison-based sorting algorithms. No comparison sort can do better than O(n log n) in the worst case.

**S12.** What is tail recursion?
> A recursive call that is the **last operation** in the function. It can be optimized by the compiler into iteration (tail call optimization), saving stack space.

**S13.** Explain greedy vs DP for Knapsack problem.
> **Fractional Knapsack** (items can be divided): Greedy works — pick highest value/weight ratio. **0/1 Knapsack** (items are whole): Greedy fails — must use DP to consider all combinations.

**S14.** How many subsets does a set of n elements have?
> **2ⁿ** subsets (including empty set and the set itself).

**S15.** What is the time complexity of the Tower of Hanoi?
> **O(2ⁿ)** — requires 2ⁿ - 1 moves for n disks. It grows exponentially.

---
