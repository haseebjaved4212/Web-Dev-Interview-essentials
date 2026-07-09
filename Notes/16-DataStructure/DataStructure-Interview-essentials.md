<div align="center">

# Data Structures Essentials

![DataStructures](https://img.shields.io/badge/Data%20Structures-DSA-orange?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Level](https://img.shields.io/badge/Level-Beginner%20to%20Intermediate-brightgreen?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Interview%20Ready-blue?style=for-the-badge)

**A simple, beginner-friendly guide to understand data structures and answer interview questions with confidence**

</div>

---

## Table of Contents

1. [What is a Data Structure](#what-is-a-data-structure)
2. [Why Data Structures Matter](#why-data-structures-matter)
3. [Arrays](#arrays)
4. [Linked Lists](#linked-lists)
5. [Stacks](#stacks)
6. [Queues](#queues)
7. [Hash Tables](#hash-tables)
8. [Trees](#trees)
9. [Binary Search Trees](#binary-search-trees)
10. [Heaps](#heaps)
11. [Graphs](#graphs)
12. [Tries](#tries)
13. [Choosing the Right Data Structure](#choosing-the-right-data-structure)
14. [Time Complexity Comparison](#time-complexity-comparison)
15. [Common Interview Questions](#common-interview-questions-spoken-style-answers)
16. [Quick Cheat Sheet](#quick-cheat-sheet)

---

## What is a Data Structure

A data structure is a way of organizing and storing data so it can be accessed and modified efficiently. The same data can be stored in different ways, and the structure I choose directly affects how fast operations like searching, inserting, or deleting will be.

**Spoken answer:** I would describe a data structure as the container I choose for my data, and that choice has real consequences. Picking the right one can turn a slow, clunky solution into something fast and clean, so understanding the trade-offs between them is one of the most useful things I can know as a developer.

---

## Why Data Structures Matter

**Spoken answer:** Every data structure makes trade-offs between speed of access, speed of insertion or deletion, and memory usage. An array gives me fast access by index but slow insertion in the middle. A linked list gives me fast insertion but slow access. Knowing these trade-offs helps me pick the right tool instead of forcing one structure to handle every situation.

---

## Arrays

```python
arr = [10, 20, 30, 40]
arr[1] = 25          # update by index, O(1)
arr.append(50)       # add to end, O(1) amortized
arr.insert(0, 5)     # insert at start, O(n)
arr.pop(0)           # remove from start, O(n)
```

| Operation | Time Complexity |
|---|---|
| Access by index | O(1) |
| Search | O(n) |
| Insert or delete at end | O(1) |
| Insert or delete at start or middle | O(n) |

**Spoken answer:** An array stores elements in contiguous memory, which is why accessing any element by its index is instant. The downside is that inserting or removing an element from the beginning or middle requires shifting every element after it, which makes those operations slower as the array grows.

---

## Linked Lists

```python
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def append(self, value):
        new_node = Node(value)
        if not self.head:
            self.head = new_node
            return
        current = self.head
        while current.next:
            current = current.next
        current.next = new_node
```

| Operation | Time Complexity |
|---|---|
| Access by index | O(n) |
| Insert or delete at head | O(1) |
| Insert or delete at tail | O(n), or O(1) if tail is tracked |
| Search | O(n) |

**Spoken answer:** A linked list stores elements as separate nodes, where each node points to the next one, rather than sitting in one continuous block of memory. This makes inserting or removing from the front very fast, since I just change a pointer, but finding a specific element means walking through the list one node at a time, since there is no direct indexing like an array.

---

## Stacks

```python
stack = []
stack.append(1)   # push
stack.append(2)
stack.pop()        # pop, removes 2
```

**Spoken answer:** A stack follows a last in, first out order, meaning the most recently added item is the first one to come out. I think of it like a stack of plates, I can only add or remove from the top. Stacks are used for things like undo functionality, expression evaluation, and tracking function calls during recursion.

---

## Queues

```python
from collections import deque

queue = deque()
queue.append(1)     # enqueue
queue.append(2)
queue.popleft()      # dequeue, removes 1
```

**Spoken answer:** A queue follows a first in, first out order, meaning the first item added is the first one removed, just like a line of people waiting. Queues are commonly used for task scheduling, handling requests in order, and in algorithms like breadth first search.

---

## Hash Tables

```python
prices = {"apple": 50, "banana": 20}
prices["orange"] = 30
print(prices["apple"])   # O(1) average lookup
del prices["banana"]
```

| Operation | Average Case | Worst Case |
|---|---|---|
| Insert | O(1) | O(n) |
| Search | O(1) | O(n) |
| Delete | O(1) | O(n) |

**Spoken answer:** A hash table stores data as key-value pairs and uses a hash function to convert a key into an index, which is why lookups are close to instant on average. Python's dictionary is a hash table under the hood. The worst case degrades to O(n) if many keys hash to the same spot, which is called a collision, but a good hash function makes that rare in practice.

---

## Trees

```python
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.children = []
```

**Spoken answer:** A tree is a hierarchical structure made of nodes, where each node can have child nodes, starting from a single root node at the top. Unlike a linked list, which is linear, a tree branches out, which makes it useful for representing things like file systems, organizational charts, or a website's navigation structure.

---

## Binary Search Trees

```python
class Node:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

def insert(root, value):
    if root is None:
        return Node(value)
    if value < root.value:
        root.left = insert(root.left, value)
    else:
        root.right = insert(root.right, value)
    return root
```

| Operation | Average Case | Worst Case |
|---|---|---|
| Search | O(log n) | O(n) |
| Insert | O(log n) | O(n) |
| Delete | O(log n) | O(n) |

**Spoken answer:** A binary search tree keeps every value in the left subtree smaller than the current node, and every value in the right subtree larger, which makes searching very efficient since I can eliminate half the remaining nodes at each step. The worst case happens when the tree becomes unbalanced, like a straight line of nodes, which is why balanced variants such as AVL trees or Red-Black trees exist.

---

## Heaps

```python
import heapq

nums = [5, 1, 8, 3]
heapq.heapify(nums)      # turns list into a min heap
heapq.heappush(nums, 2)
smallest = heapq.heappop(nums)   # always removes the smallest
```

**Spoken answer:** A heap is a tree-based structure where the smallest value, in a min heap, or the largest value, in a max heap, always sits at the root, making it fast to repeatedly access the minimum or maximum. Heaps are the backbone of priority queues and are used in algorithms like Dijkstra's shortest path and heap sort.

---

## Graphs

```python
graph = {
    "A": ["B", "C"],
    "B": ["D"],
    "C": ["D"],
    "D": []
}
```

| Representation | Description |
|---|---|
| Adjacency List | Each node stores a list of connected nodes, memory efficient |
| Adjacency Matrix | A grid showing connections between every pair of nodes, faster lookups but more memory |

**Spoken answer:** A graph is a set of nodes connected by edges, and unlike a tree, it does not have to follow a strict hierarchy, connections can go in any direction and even form cycles. I usually represent a graph as an adjacency list when it is sparse, since it saves memory, and consider an adjacency matrix when I need fast lookups on whether two specific nodes are connected.

---

## Tries

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end_of_word = False

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end_of_word = True
```

**Spoken answer:** A trie is a tree structure specialized for storing strings, where each path from the root to a node represents a prefix. It is commonly used for autocomplete and spell checking, since it lets me quickly find all words that share a given prefix without scanning through an entire list of words.

---

## Choosing the Right Data Structure

| Need | Good Choice |
|---|---|
| Fast access by index | Array |
| Frequent insertion or deletion at the start | Linked List |
| Undo functionality, matching brackets | Stack |
| Processing tasks in order, level order traversal | Queue |
| Fast lookups by key | Hash Table |
| Hierarchical data | Tree |
| Sorted data with fast search | Binary Search Tree |
| Repeatedly finding minimum or maximum | Heap |
| Modeling connections or relationships | Graph |
| Prefix based string search | Trie |

**Spoken answer:** When I am deciding which data structure to use, I think about what operation happens most often. If I need constant time lookups, a hash table usually wins. If I need to maintain order and process things sequentially, a queue or stack fits better. There is rarely a single correct answer, it depends on the specific pattern of operations the problem needs.

---

## Time Complexity Comparison

| Structure | Access | Search | Insert | Delete |
|---|---|---|---|---|
| Array | O(1) | O(n) | O(n) | O(n) |
| Linked List | O(n) | O(n) | O(1) | O(1) |
| Stack | O(n) | O(n) | O(1) | O(1) |
| Queue | O(n) | O(n) | O(1) | O(1) |
| Hash Table | O(1) avg | O(1) avg | O(1) avg | O(1) avg |
| Binary Search Tree | O(log n) avg | O(log n) avg | O(log n) avg | O(log n) avg |
| Heap | O(1) for min or max | O(n) | O(log n) | O(log n) |

---

## Common Interview Questions (Spoken-Style Answers)

**Q: What is the difference between an array and a linked list?**
An array stores elements in contiguous memory, giving instant access by index but slow insertion in the middle. A linked list stores elements as separate nodes connected by pointers, giving fast insertion and deletion but slower access since I have to walk through nodes one at a time.

**Q: When would you use a stack over a queue?**
I use a stack when the most recently added item needs to be processed first, like tracking function calls or implementing undo. I use a queue when items need to be processed in the exact order they arrived, like handling requests or tasks in a scheduler.

**Q: How does a hash table achieve close to constant time lookups?**
It uses a hash function to convert a key into an index in an underlying array, so instead of searching through every element, it can jump almost directly to where the value should be. Collisions, where two keys hash to the same index, are handled with techniques like chaining or open addressing.

**Q: What is the difference between a tree and a graph?**
A tree is a specific type of graph that has no cycles and exactly one path between any two nodes, usually with a clear parent-child hierarchy. A graph is more general and can have cycles, multiple connections between nodes, and no strict hierarchy at all.

**Q: What is a balanced binary search tree and why does it matter?**
It's a binary search tree that keeps its height roughly logarithmic relative to the number of nodes, instead of becoming a long unbalanced chain. This matters because it guarantees search, insert, and delete all stay around O(log n) instead of degrading to O(n) in the worst case.

**Q: What is the difference between a min heap and a max heap?**
In a min heap, the smallest value is always at the root, making it fast to repeatedly retrieve the minimum. In a max heap, the largest value is always at the root instead. Both are commonly used to implement priority queues.

**Q: When would you choose a trie over a hash table for storing strings?**
A trie is better when I need prefix based operations, like autocomplete or checking if any word starts with a certain prefix, since it organizes strings character by character. A hash table is better for simple exact-match lookups, since it does not naturally support prefix searches.

---

## Quick Cheat Sheet

| Structure | Best For |
|---|---|
| Array | Fast indexed access, fixed or predictable size |
| Linked List | Frequent insertions or deletions at the ends |
| Stack | Last in first out order, undo, recursion tracking |
| Queue | First in first out order, task scheduling |
| Hash Table | Fast key based lookups |
| Tree | Hierarchical data |
| Binary Search Tree | Sorted data with efficient search |
| Heap | Repeatedly finding min or max, priority queues |
| Graph | Modeling networks and relationships |
| Trie | Prefix based string search, autocomplete |

---

<div align="center">

**Made for interview prep by Haseeb Javed**
Good luck with your data structures interviews.

</div>