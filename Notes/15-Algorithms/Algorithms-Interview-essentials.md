<div align="center">

# 🧠 Algorithms Essentials

![Algorithms](https://img.shields.io/badge/Algorithms-DSA-orange?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Level](https://img.shields.io/badge/Level-Beginner%20to%20Intermediate-brightgreen?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Interview%20Ready-blue?style=for-the-badge)

**A simple, beginner-friendly guide to understand algorithms and answer interview questions with confidence**

</div>

---

## 📖 Table of Contents

1. [What is an Algorithm](#-what-is-an-algorithm)
2. [Big O Notation](#-big-o-notation)
3. [Time vs Space Complexity](#-time-vs-space-complexity)
4. [Searching Algorithms](#-searching-algorithms)
5. [Sorting Algorithms](#-sorting-algorithms)
6. [Recursion](#-recursion)
7. [Two Pointers](#-two-pointers)
8. [Sliding Window](#-sliding-window)
9. [Divide and Conquer](#-divide-and-conquer)
10. [Greedy Algorithms](#-greedy-algorithms)
11. [Dynamic Programming](#-dynamic-programming)
12. [Backtracking](#-backtracking)
13. [Graph Algorithms](#-graph-algorithms)
14. [Tree Traversal](#-tree-traversal)
15. [Hashing](#-hashing)
16. [Common Problem Patterns](#-common-problem-patterns)
17. [How to Approach a Problem in an Interview](#-how-to-approach-a-problem-in-an-interview)
18. [Common Interview Questions](#-common-interview-questions-spoken-style-answers)
19. [Quick Cheat Sheet](#-quick-cheat-sheet)

---

## 🧩 What is an Algorithm

An algorithm is just a clear set of steps to solve a problem or complete a task. In programming, we care about writing algorithms that are correct, but also efficient, meaning they use time and memory wisely as the input grows larger.

**Spoken answer:** I think of an algorithm as a step by step recipe for solving a problem. Two algorithms can both give the correct answer, but one might be much faster or use less memory than the other, and that difference matters a lot once the input gets big.

---

## 📈 Big O Notation

| Notation | Name | Example |
|---|---|---|
| O(1) | Constant | Accessing an array by index |
| O(log n) | Logarithmic | Binary search |
| O(n) | Linear | Looping through a list once |
| O(n log n) | Linearithmic | Merge sort, quick sort |
| O(n²) | Quadratic | Nested loops, bubble sort |
| O(2^n) | Exponential | Naive recursive Fibonacci |

**Spoken answer:** Big O notation describes how the running time or memory usage of an algorithm grows as the input size grows, ignoring constant factors. It's not about exact seconds, it's about the pattern of growth, so I can compare algorithms fairly regardless of the machine they run on.

---

## ⚖️ Time vs Space Complexity

**Spoken answer:** Time complexity tells me how the runtime grows with input size, while space complexity tells me how much extra memory the algorithm needs. Sometimes there's a trade-off, like using a hash map to speed up lookups, which costs extra memory but saves a lot of time.

---

## 🔍 Searching Algorithms

```python
# Linear Search - O(n)
def linear_search(arr, target):
    for i, val in enumerate(arr):
        if val == target:
            return i
    return -1

# Binary Search - O(log n), array must be sorted
def binary_search(arr, target):
    low, high = 0, len(arr) - 1
    while low <= high:
        mid = (low + high) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    return -1
```

**Spoken answer:** Linear search checks every element one by one, so it works on any list but takes longer as the list grows. Binary search is much faster because it repeatedly cuts the search space in half, but it only works if the array is already sorted.

---

## 🔃 Sorting Algorithms

```python
# Bubble Sort - O(n²)
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr

# Merge Sort - O(n log n)
def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    return merge(left, right)

def merge(left, right):
    result = []
    i = j = 0
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i]); i += 1
        else:
            result.append(right[j]); j += 1
    result.extend(left[i:])
    result.extend(right[j:])
    return result
```

| Algorithm | Best Case | Average Case | Worst Case | Stable |
|---|---|---|---|---|
| Bubble Sort | O(n) | O(n²) | O(n²) | Yes |
| Insertion Sort | O(n) | O(n²) | O(n²) | Yes |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) | Yes |
| Quick Sort | O(n log n) | O(n log n) | O(n²) | No |

**Spoken answer:** Bubble sort and insertion sort are simple but slow, mainly useful for teaching or very small datasets. Merge sort splits the array into halves, sorts each half, then merges them back together, guaranteeing O(n log n) every time. Quick sort is usually faster in practice but can hit O(n²) in the worst case if the pivot choices are bad.

---

## 🔁 Recursion

```python
def factorial(n):
    if n == 0:            # base case
        return 1
    return n * factorial(n - 1)   # recursive case
```

**Spoken answer:** Recursion is when a function calls itself to solve a smaller version of the same problem. Every recursive function needs a base case, which stops the recursion, and a recursive case that moves toward that base case. Without a proper base case, it would keep calling itself forever and crash with a stack overflow.

---

## 👉👈 Two Pointers

```python
def is_palindrome(s):
    left, right = 0, len(s) - 1
    while left < right:
        if s[left] != s[right]:
            return False
        left += 1
        right -= 1
    return True
```

**Spoken answer:** The two pointer technique uses two variables to track positions in a list or string, usually moving toward each other or in the same direction. It's great for problems like checking palindromes or finding pairs that sum to a target, because it avoids nested loops and keeps the solution at O(n).

---

## 🪟 Sliding Window

```python
def max_sum_subarray(arr, k):
    window_sum = sum(arr[:k])
    max_sum = window_sum
    for i in range(k, len(arr)):
        window_sum += arr[i] - arr[i - k]
        max_sum = max(max_sum, window_sum)
    return max_sum
```

**Spoken answer:** Sliding window is useful when I need to look at a contiguous chunk of a list, like a subarray of fixed size. Instead of recalculating the sum from scratch every time, I slide the window forward by adding the new element and removing the old one, which turns an O(n*k) solution into O(n).

---

## ➗ Divide and Conquer

**Spoken answer:** Divide and conquer means breaking a big problem into smaller subproblems of the same type, solving each one recursively, and then combining the results. Merge sort is a classic example, it splits the array in half repeatedly until pieces are tiny, then merges sorted pieces back together.

---

## 🎯 Greedy Algorithms

**Spoken answer:** A greedy algorithm makes the best possible choice at each step, hoping that these local choices lead to a globally optimal solution. It works well for problems like coin change with standard denominations or activity scheduling, but it does not always give the correct answer for every problem, so I have to verify it actually applies before trusting it.

---

## 🧮 Dynamic Programming

```python
# Fibonacci with memoization
def fib(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fib(n - 1, memo) + fib(n - 2, memo)
    return memo[n]
```

**Spoken answer:** Dynamic programming solves problems by breaking them into overlapping subproblems and storing the results so I don't recalculate the same thing multiple times. Without memoization, calculating Fibonacci recursively takes exponential time, but with it, the same calculation becomes linear, since each value is only computed once.

---

## 🔙 Backtracking

```python
def find_subsets(nums):
    result = []
    def backtrack(start, path):
        result.append(path[:])
        for i in range(start, len(nums)):
            path.append(nums[i])
            backtrack(i + 1, path)
            path.pop()
    backtrack(0, [])
    return result
```

**Spoken answer:** Backtracking explores all possible options step by step, and whenever a choice leads to a dead end or an invalid state, it undoes that choice and tries a different path. It's commonly used for problems like generating permutations, subsets, or solving puzzles like Sudoku.

---

## 🌐 Graph Algorithms

```python
# BFS
from collections import deque

def bfs(graph, start):
    visited = set([start])
    queue = deque([start])
    while queue:
        node = queue.popleft()
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)

# DFS
def dfs(graph, node, visited=None):
    if visited is None:
        visited = set()
    visited.add(node)
    for neighbor in graph[node]:
        if neighbor not in visited:
            dfs(graph, neighbor, visited)
```

**Spoken answer:** BFS explores a graph level by level using a queue, which makes it great for finding the shortest path in an unweighted graph. DFS goes as deep as possible down one path before backtracking, usually implemented with recursion or a stack, and is useful for things like detecting cycles or exploring all connected components.

---

## 🌳 Tree Traversal

```python
# In-order traversal
def inorder(node):
    if node:
        inorder(node.left)
        print(node.value)
        inorder(node.right)
```

| Traversal | Order |
|---|---|
| In-order | Left, Root, Right |
| Pre-order | Root, Left, Right |
| Post-order | Left, Right, Root |
| Level-order | Level by level, using a queue |

**Spoken answer:** In-order traversal on a binary search tree gives values in sorted order, which is a very common interview fact. Pre-order is useful for copying a tree's structure, and post-order is often used when I need to process children before the parent, like when deleting a tree.

---

## 🔑 Hashing

```python
def has_pair_with_sum(arr, target):
    seen = set()
    for num in arr:
        if target - num in seen:
            return True
        seen.add(num)
    return False
```

**Spoken answer:** Hashing lets me store and look up values in close to constant time using a hash map or set. A lot of brute force O(n²) problems, like finding pairs that sum to a target, can be reduced to O(n) just by trading a bit of extra memory for a hash-based lookup.

---

## 🧩 Common Problem Patterns

| Pattern | Used For |
|---|---|
| Two Pointers | Sorted arrays, palindrome checks |
| Sliding Window | Subarrays or substrings with a condition |
| Fast and Slow Pointers | Cycle detection in linked lists |
| Binary Search | Sorted data or search space reduction |
| BFS / DFS | Graphs, trees, connected components |
| Dynamic Programming | Overlapping subproblems, optimization |
| Backtracking | Generating combinations, permutations |
| Merge Intervals | Overlapping ranges or scheduling |

**Spoken answer:** Once I recognize which pattern a problem fits into, solving it becomes much easier, because most interview problems are variations of a small set of well known patterns rather than something completely new every time.

---

## 🧭 How to Approach a Problem in an Interview

1. Restate the problem in my own words to confirm understanding
2. Ask about edge cases, like empty input or duplicates
3. Start with a brute force solution, even if it's slow
4. Identify the time and space complexity of that brute force approach
5. Look for a pattern to optimize it
6. Code it step by step, thinking out loud
7. Test with a simple example and then an edge case

**Spoken answer:** I always start by making sure I understand the problem correctly before writing any code, since a lot of mistakes come from solving the wrong problem. Then I think of the simplest brute force solution first, and only after that do I look for ways to optimize it, rather than jumping straight to a complex solution.

---

## 💬 Common Interview Questions (Spoken-Style Answers)

**Q: What is the difference between time complexity and space complexity?**
Time complexity measures how the running time grows as input size increases, while space complexity measures how much extra memory the algorithm needs. Both are usually expressed using Big O notation.

**Q: Why is binary search faster than linear search?**
Binary search cuts the search space in half with every step, giving it O(log n) time, while linear search checks each element one at a time, giving it O(n). The trade-off is that binary search only works on sorted data.

**Q: What is the difference between BFS and DFS?**
BFS explores level by level using a queue and is good for finding the shortest path in unweighted graphs. DFS goes deep down one branch before backtracking, usually using recursion or a stack, and is good for exploring all possible paths or detecting cycles.

**Q: What is memoization?**
Memoization is a technique where I store the results of expensive function calls and return the cached result when the same inputs occur again, which avoids repeating the same calculation and speeds up recursive algorithms significantly.

**Q: What is the difference between a greedy algorithm and dynamic programming?**
A greedy algorithm makes the locally best choice at each step without looking back, which is fast but not always correct for every problem. Dynamic programming considers overlapping subproblems and builds up to the optimal solution by storing intermediate results, which is more reliable but usually needs more memory.

**Q: What is a stack overflow in recursion?**
It happens when a recursive function calls itself too many times without reaching a base case, using up all the memory allocated for the call stack, which then crashes the program.

**Q: How would you find duplicates in an array efficiently?**
I would use a hash set to track numbers I've already seen while looping through the array once. If I encounter a number that's already in the set, it's a duplicate, which gives me an O(n) solution instead of comparing every pair.

---

## ⚡ Quick Cheat Sheet

| Concept | Time Complexity |
|---|---|
| Array access by index | O(1) |
| Linear search | O(n) |
| Binary search | O(log n) |
| Bubble / Insertion sort | O(n²) |
| Merge / Quick sort (average) | O(n log n) |
| Hash map lookup | O(1) average |
| BFS / DFS on graph | O(V + E) |
| Recursive Fibonacci (no memo) | O(2^n) |
| Fibonacci with memoization | O(n) |

| Pattern | Typical Use |
|---|---|
| Two Pointers | Sorted array pair problems |
| Sliding Window | Subarray or substring problems |
| Binary Search | Search space reduction |
| BFS | Shortest path, level order |
| DFS | Path exploration, cycle detection |
| Dynamic Programming | Optimization with overlapping subproblems |
| Backtracking | Permutations, combinations, puzzles |

---

<div align="center">

**Made for interview prep by Haseeb Javed**
Good luck with your algorithms and data structures interviews! 🚀

</div>