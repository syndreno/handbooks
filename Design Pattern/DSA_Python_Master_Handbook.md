# DSA with Python — Master Learning Handbook

> **Data Structures and Algorithms (DSA) in Python — Beginner to Advanced**
>
> A single-reference handbook for learning, revision, interviews, competitive programming, and practical software engineering.

---

## Table of Contents

1. [How to Use This Handbook](#1-how-to-use-this-handbook)
2. [What Is DSA?](#2-what-is-dsa)
3. [Python for DSA](#3-python-for-dsa)
4. [Complexity Analysis](#4-complexity-analysis)
5. [Mathematical Foundations](#5-mathematical-foundations)
6. [Recursion](#6-recursion)
7. [Arrays and Python Lists](#7-arrays-and-python-lists)
8. [Strings](#8-strings)
9. [Linked Lists](#9-linked-lists)
10. [Stacks](#10-stacks)
11. [Queues and Deques](#11-queues-and-deques)
12. [Hash Tables, Dictionaries, and Sets](#12-hash-tables-dictionaries-and-sets)
13. [Searching Algorithms](#13-searching-algorithms)
14. [Sorting Algorithms](#14-sorting-algorithms)
15. [Two Pointers](#15-two-pointers)
16. [Sliding Window](#16-sliding-window)
17. [Prefix Sum, Suffix Sum, and Difference Arrays](#17-prefix-sum-suffix-sum-and-difference-arrays)
18. [Intervals](#18-intervals)
19. [Binary Search Patterns](#19-binary-search-patterns)
20. [Trees](#20-trees)
21. [Binary Search Trees](#21-binary-search-trees)
22. [Heaps and Priority Queues](#22-heaps-and-priority-queues)
23. [Tries](#23-tries)
24. [Graphs](#24-graphs)
25. [Union-Find / Disjoint Set Union](#25-union-find--disjoint-set-union)
26. [Greedy Algorithms](#26-greedy-algorithms)
27. [Backtracking](#27-backtracking)
28. [Dynamic Programming](#28-dynamic-programming)
29. [Bit Manipulation](#29-bit-manipulation)
30. [Monotonic Stack and Monotonic Queue](#30-monotonic-stack-and-monotonic-queue)
31. [Advanced String Algorithms](#31-advanced-string-algorithms)
32. [Range Query Data Structures](#32-range-query-data-structures)
33. [Advanced Graph Algorithms](#33-advanced-graph-algorithms)
34. [Advanced Tree Concepts](#34-advanced-tree-concepts)
35. [Algorithm Design Paradigms](#35-algorithm-design-paradigms)
36. [Common Problem-Solving Patterns](#36-common-problem-solving-patterns)
37. [Python-Specific DSA Optimizations](#37-python-specific-dsa-optimizations)
38. [Testing and Debugging DSA Solutions](#38-testing-and-debugging-dsa-solutions)
39. [Interview Problem-Solving Framework](#39-interview-problem-solving-framework)
40. [Competitive Programming Template](#40-competitive-programming-template)
41. [Common Mistakes and Anti-Patterns](#41-common-mistakes-and-anti-patterns)
42. [DSA Roadmap](#42-dsa-roadmap)
43. [Practice Problem Checklist](#43-practice-problem-checklist)
44. [Cheat Sheets](#44-cheat-sheets)
45. [Mini Projects Using DSA](#45-mini-projects-using-dsa)
46. [Final Revision Strategy](#46-final-revision-strategy)

---

# 1. How to Use This Handbook

This handbook is designed for several types of learners:

- A complete beginner learning DSA for the first time.
- A Python developer who wants stronger problem-solving skills.
- A student preparing for coding interviews.
- A competitive programmer.
- An experienced developer revising algorithms.
- Someone who wants one master reference instead of many scattered notes.

A good learning cycle is:

```text
Learn concept
    ↓
Understand operations
    ↓
Understand time/space complexity
    ↓
Implement from scratch
    ↓
Use Python's built-in equivalent
    ↓
Solve easy problems
    ↓
Solve pattern-based medium problems
    ↓
Study edge cases
    ↓
Revise
```

Do not memorize every implementation blindly. The real objective is to recognize:

1. What structure fits the problem?
2. What operations need to be fast?
3. What trade-offs are acceptable?
4. What pattern is hidden in the problem?
5. What complexity is required by the input size?

---

# 2. What Is DSA?

Data Structures and Algorithms (DSA) is the study of how to organize data and how to process it efficiently and correctly. The practical skill is choosing operations and representations that fit the constraints, then proving correctness and understanding the time/memory trade-off.

## 2.1 Data Structure

A **data structure** is a way of organizing data so that particular operations can be performed efficiently.

Examples:

| Data Structure | Typical Strength |
|---|---|
| Array/List | Fast indexing |
| Linked List | Cheap insertion/removal when node is known |
| Stack | Last-In-First-Out processing |
| Queue | First-In-First-Out processing |
| Hash Table | Fast average lookup |
| Heap | Fast access to minimum/maximum priority |
| Tree | Hierarchical data |
| Graph | Relationships/networks |
| Trie | Prefix search |
| Union-Find | Connectivity tracking |

## 2.2 Algorithm

An algorithm is a finite, unambiguous procedure that converts an input into the required output. A useful explanation of an algorithm should state its preconditions, the main invariant or idea that keeps it correct, when it stops, and its time and space complexity.

An **algorithm** is a finite sequence of steps used to solve a problem.

Examples:

- Binary search
- Merge sort
- Breadth-first search
- Depth-first search
- Dijkstra's shortest path
- Dynamic programming

## 2.3 Why DSA Matters

Imagine an application with 10 records. Almost any solution works.

Now imagine:

```text
10 records
1,000 records
1,000,000 records
1,000,000,000 records
```

A poor algorithm can become unusable as data grows.

For example:

```python
# O(n)
for value in values:
    if value == target:
        return True
```

If the list is sorted, binary search can reduce this to approximately:

```text
O(log n)
```

For one billion values:

```text
Linear search: potentially ~1,000,000,000 checks
Binary search: roughly ~30 checks
```

That difference is why algorithms matter.

---

# 3. Python for DSA

Python is popular for DSA because its syntax lets us focus on the algorithm rather than boilerplate.

## 3.1 Core Python Containers

Python's main DSA containers have different strengths: `list` for indexed dynamic sequences, `tuple` for immutable fixed records, `set` for unique membership, and `dict` for key/value lookup. Operation cost depends on the container, so choose based on required access rather than syntax convenience.

```python
numbers = [10, 20, 30]          # list
point = (4, 7)                  # tuple
unique = {1, 2, 3}              # set
user = {"id": 10, "name": "A"}  # dict
```

## 3.2 Essential Imports

These standard-library modules provide DSA-ready implementations: `deque` for queues, `Counter/defaultdict` for counting/grouping, `heapq` for min-heaps, `bisect` for binary-search insertion points, and `functools` helpers for memoization. Import only what the solution uses so dependencies stay obvious.

```python
from collections import deque, defaultdict, Counter
from functools import lru_cache
from heapq import heappush, heappop, heapify
from bisect import bisect_left, bisect_right
from math import gcd, inf
```

## 3.3 Python List Comprehensions

A list comprehension builds a new list by iterating and optionally filtering an iterable. It is concise for simple transformations but allocates the full result; use a generator expression when lazy iteration is sufficient, and prefer a normal loop when the expression becomes hard to read.

```python
squares = [x * x for x in range(10)]
evens = [x for x in range(20) if x % 2 == 0]
```

Avoid complicated comprehensions when they reduce readability.

## 3.4 `enumerate`

`enumerate(iterable)` yields `(index, value)` pairs, avoiding a separate manual counter. It is ideal when both the element and its position are needed; the optional `start` argument changes the first reported index without changing the underlying iterable.

Instead of:

```python
for i in range(len(nums)):
    print(i, nums[i])
```

Prefer:

```python
for i, value in enumerate(nums):
    print(i, value)
```

## 3.5 `zip`

`zip(a, b, ...)` iterates corresponding elements together and stops at the shortest input by default. It is useful for parallel arrays, coordinates, and pairwise data; if unequal lengths should be an error or preserved, use an explicit check or `itertools.zip_longest` as appropriate.

```python
names = ["A", "B", "C"]
scores = [80, 92, 76]

for name, score in zip(names, scores):
    print(name, score)
```

## 3.6 Multiple Assignment

Swapping exchanges two values without changing the rest of the data. It is common in sorting, partitioning, reversal, and heap operations. Ensure both positions are valid before swapping; in-place algorithms rely on this operation preserving all values rather than losing one through overwrite.

```python
a, b = b, a
```

Useful for swapping values.

## 3.7 Negative Indexing

Negative indexing addresses elements relative to the end of a sequence; `-1` means the last element. It is convenient, but algorithms translated from languages without negative indexing can accidentally hide an out-of-bounds bug if a negative index is accepted as valid.

```python
arr = [10, 20, 30]

arr[-1]  # 30
arr[-2]  # 20
```

## 3.8 Slicing

```python
arr[start:end:step]
```

Example:

```python
arr = [1, 2, 3, 4, 5]

arr[1:4]   # [2, 3, 4]
arr[::-1]  # reversed copy
```

Important:

> Slicing generally creates a new sequence and therefore costs time and memory proportional to the slice size.

## 3.9 Python Mutable vs Immutable Objects

Mutable objects can change after creation; immutable objects cannot. This affects aliasing, function side effects, hashability, default arguments, and dictionary/set keys. A tuple is only hashable when all of its contained values are hashable.

Common mutable objects:

```text
list
dict
set
custom class objects
```

Common immutable objects:

```text
int
float
bool
str
tuple
frozenset
```

This matters when using objects as dictionary keys.

---

# 4. Complexity Analysis

Complexity analysis estimates how an algorithm's resource usage grows as input size increases. Focus on the dominant growth rate rather than machine-specific timing, and analyze both execution work and extra memory so you can compare approaches before benchmarking.

Complexity analysis estimates how algorithm resource usage grows as input size grows.

The two main measurements are:

- **Time Complexity**
- **Space Complexity**

---

## 4.1 Big-O Notation

Big-O describes an asymptotic upper growth rate.

Common complexities:

| Complexity | Name | Typical Example |
|---|---|---|
| O(1) | Constant | Dictionary lookup average case |
| O(log n) | Logarithmic | Binary search |
| O(n) | Linear | Scan array |
| O(n log n) | Linearithmic | Efficient comparison sorting |
| O(n²) | Quadratic | Nested pair loops |
| O(n³) | Cubic | Some matrix/DP algorithms |
| O(2^n) | Exponential | Subset recursion |
| O(n!) | Factorial | Permutations |

---

## 4.2 O(1)

`O(1)` means the amount of work does not grow with the number of input elements. It does **not** mean the operation takes exactly one CPU instruction; it means the step count is bounded by a constant with respect to input size. Examples include reading a known array index or checking a stored variable.

```python
def first(arr):
    return arr[0]
```

The work does not meaningfully grow with `n`.

---

## 4.3 O(n)

`O(n)` means the running time grows proportionally with the input size. A single complete pass over an array is the standard example. Several separate linear passes are still `O(n)` because constant multipliers are omitted in asymptotic analysis.

```python
def contains(arr, target):
    for item in arr:
        if item == target:
            return True
    return False
```

Worst case examines every element.

---

## 4.4 O(n²)

`O(n²)` usually appears when the algorithm examines many pairs of input elements, such as two nested loops over the same `n` items. Doubling `n` can make the dominant work roughly four times larger, so quadratic approaches become expensive quickly on large inputs.

```python
for i in range(n):
    for j in range(n):
        print(i, j)
```

Approximately `n × n` operations.

---

## 4.5 O(log n)

`O(log n)` appears when each step reduces the remaining problem by a constant factor, often by half. Binary search is the classic example. The logarithm base is ignored in Big-O because changing the base only multiplies the count by a constant factor.

Repeatedly reducing a problem by a constant factor often creates logarithmic complexity.

```python
while n > 1:
    n //= 2
```

---

## 4.6 O(n log n)

`O(n log n)` commonly appears when an algorithm performs logarithmic levels of work and processes `O(n)` data across each level. Efficient comparison sorts such as merge sort and heap sort have this bound; divide-and-conquer algorithms often produce it as well.

Common in divide-and-conquer sorting.

Example:

```text
Merge sort
Heap sort
Average efficient comparison sorts
```

---

## 4.7 Best, Average, and Worst Case

An algorithm can have different complexity for different input arrangements. State which case you are analyzing and what input distribution/condition produces it; for example, Quick Sort can be `O(n log n)` average but `O(n²)` worst case with poor pivots.

Linear search:

```python
def search(arr, target):
    for item in arr:
        if item == target:
            return True
    return False
```

Best case:

```text
Target is first element → O(1)
```

Worst case:

```text
Target is last or absent → O(n)
```

Average case:

```text
O(n)
```

---

## 4.8 Amortized Complexity

Amortized analysis spreads the cost of occasional expensive operations over a long sequence of operations. For example, a dynamic array resize may cost `O(n)`, but because resizing is infrequent, repeated append operations can still have `O(1)` amortized cost. Amortized complexity is a sequence-level guarantee; it does not mean every individual operation is constant-time.

Python list append is normally considered:

```text
O(1) amortized
```

Occasionally the internal array must resize, which costs `O(n)`, but resizing does not occur for every append.

---

## 4.9 Space Complexity

Space complexity measures how much additional memory grows with input size. Distinguish the input itself from **auxiliary space** used by the algorithm, and remember to include recursion depth, temporary arrays, hash tables, queues, and stacks. An in-place algorithm usually means `O(1)` or very small auxiliary storage, not that the input occupies no memory.

Example:

```python
def doubled(nums):
    result = []

    for x in nums:
        result.append(x * 2)

    return result
```

Additional storage grows with `n`:

```text
O(n)
```

An in-place operation may use:

```text
O(1) auxiliary space
```

---

## 4.10 Practical Input-Size Heuristic

This is approximate, not a strict rule:

| Input Size | Usually Consider |
|---|---|
| n ≤ 10 | factorial/exponential may be possible |
| n ≤ 20 | O(2^n) sometimes possible |
| n ≤ 100 | O(n³) sometimes possible |
| n ≤ 1,000 | O(n²) often possible |
| n ≤ 100,000 | O(n log n) usually desirable |
| n ≤ 1,000,000 | O(n) or O(n log n) |
| Extremely large | O(log n), O(1), streaming, special math |

Always consider language, constants, memory, and environment.

---

# 5. Mathematical Foundations

A small set of mathematical tools appears repeatedly in DSA: modular arithmetic, divisibility, GCD/LCM, primes, logarithms, combinatorics, and exponentiation. The purpose is practical—these tools simplify constraints, prevent overflow, or reduce repeated computation in algorithms.

DSA frequently uses simple mathematical ideas.

## 5.1 Modulo

The modulo operator returns a remainder and appears in cyclic indexing, parity, hashing, and modular arithmetic. Be careful with negative operands because remainder sign rules differ across languages; if a non-negative mathematical modulus is required, normalize the result according to the language's semantics.

```python
17 % 5
# 2
```

Useful for:

- Cyclic arrays
- Hashing
- Even/odd tests
- Modular arithmetic
- Large-number problems

Circular index:

```python
next_index = (index + 1) % n
```

---

## 5.2 Greatest Common Divisor

The Euclidean algorithm finds the greatest common divisor (GCD) by repeatedly replacing `(a, b)` with `(b, a mod b)` until the second value becomes zero. The remaining non-zero value is the GCD. It runs in logarithmic time with respect to the numeric values and is a standard building block for fractions, modular arithmetic, and LCM calculation.

```python
from math import gcd

gcd(18, 24)
# 6
```

Euclidean algorithm:

```python
def gcd_custom(a, b):
    while b:
        a, b = b, a % b
    return a
```

Complexity:

```text
O(log(min(a, b)))
```

---

## 5.3 Least Common Multiple

The least common multiple (LCM) of two non-zero integers can be derived from the GCD: `lcm(a, b) = |a / gcd(a, b) × b|`. Dividing before multiplying reduces overflow risk in fixed-width languages. Define how your implementation should behave when either input is zero; a common convention returns zero.

```python
def lcm(a, b):
    return abs(a * b) // gcd(a, b)
```

---

## 5.4 Prime Check

```python
def is_prime(n):
    if n < 2:
        return False

    d = 2

    while d * d <= n:
        if n % d == 0:
            return False
        d += 1

    return True
```

Why stop at `sqrt(n)`?

If `n = a × b`, at least one factor must be `≤ sqrt(n)`.

---

## 5.5 Sieve of Eratosthenes

The Sieve of Eratosthenes finds all primes up to a limit by marking multiples of each discovered prime as composite. Starting the marking at `p × p` is enough because smaller multiples already have a smaller prime factor. The standard implementation runs in `O(n log log n)` time and uses `O(n)` marking space.

Find all primes up to `n`.

```python
def sieve(n):
    prime = [True] * (n + 1)

    if n >= 0:
        prime[0] = False
    if n >= 1:
        prime[1] = False

    p = 2

    while p * p <= n:
        if prime[p]:
            for multiple in range(p * p, n + 1, p):
                prime[multiple] = False
        p += 1

    return [i for i, is_p in enumerate(prime) if is_p]
```

Complexity:

```text
Time: O(n log log n)
Space: O(n)
```

---

# 6. Recursion

Recursion solves a problem by calling the same routine on a smaller or simpler state. Every recursive solution needs a **base case** that stops further calls and a **progress rule** that moves toward that base case. Also account for call-stack space: even an algorithm with little explicit memory usage may use `O(depth)` stack space.

Recursion occurs when a function calls itself.

## 6.1 Basic Example

Use the example to identify the recursive state, base case, and progress step. Trace a small input manually and write the call sequence/returns; this makes stack growth and termination concrete instead of treating recursion as magic.

```python
def countdown(n):
    if n == 0:
        return

    print(n)
    countdown(n - 1)
```

Every recursive algorithm needs:

1. A **base case**
2. Progress toward the base case

---

## 6.2 Factorial

Factorial is defined for non-negative integers by `n! = n × (n-1) × ... × 1`, with `0! = 1`. A recursive implementation mirrors that definition, but an iterative version avoids recursive call-stack growth. Factorial values grow extremely quickly, so ordinary fixed-width integer types overflow at relatively small `n` values.

```python
def factorial(n):
    if n <= 1:
        return 1

    return n * factorial(n - 1)
```

---

## 6.3 Recursion Stack

Recursion solves a problem by calling the same routine on a smaller or simpler state. Every recursive solution needs a **base case** that stops further calls and a **progress rule** that moves toward that base case. Also account for call-stack space: even an algorithm with little explicit memory usage may use `O(depth)` stack space.

Calling:

```python
factorial(4)
```

conceptually produces:

```text
factorial(4)
    factorial(3)
        factorial(2)
            factorial(1)
```

Each call consumes stack space.

Complexity:

```text
Time: O(n)
Stack space: O(n)
```

---

## 6.4 Python Recursion Limitation

Recursion solves a problem by calling the same routine on a smaller or simpler state. Every recursive solution needs a **base case** that stops further calls and a **progress rule** that moves toward that base case. Also account for call-stack space: even an algorithm with little explicit memory usage may use `O(depth)` stack space.

Python is not optimized for deep recursive calls.

For deeply nested problems, iterative methods may be safer.

Graph DFS can often be implemented iteratively:

```python
def dfs_iterative(graph, start):
    stack = [start]
    visited = set()

    while stack:
        node = stack.pop()

        if node in visited:
            continue

        visited.add(node)

        for neighbor in graph[node]:
            if neighbor not in visited:
                stack.append(neighbor)

    return visited
```

---

# 7. Arrays and Python Lists

An array-like structure stores elements in an indexed sequence. Its main advantage is direct access by position; the main trade-off is that inserting or deleting near the front or middle usually requires shifting elements. In DSA problems, arrays are also the base structure behind two pointers, sliding windows, prefix sums, binary search, heaps, and many dynamic-programming tables.

Python's built-in `list` is a dynamic array.

```python
arr = [10, 20, 30, 40]
```

## 7.1 Common Operations

| Operation | Typical Complexity |
|---|---|
| `arr[i]` | O(1) |
| `arr.append(x)` | O(1) amortized |
| `arr.pop()` | O(1) |
| `arr.insert(0, x)` | O(n) |
| `arr.pop(0)` | O(n) |
| Search | O(n) |
| Delete middle | O(n) |
| Sort | O(n log n) |

---

## 7.2 Why Indexing Is Fast

Python lists are dynamic arrays of object references, so an index can be translated directly to a slot offset. That gives `O(1)` indexed access; it does not make searching by value constant-time, which still requires scanning unless another index/map is maintained.

A dynamic array stores references in contiguous indexed slots, allowing direct indexed access.

---

## 7.3 Maximum Element

Finding a maximum requires a baseline that is valid for the input domain. Initialize from the first element (after handling empty input) rather than from `0`, which fails when every value is negative. Then scan once and replace the current maximum whenever a larger value appears: `O(n)` time, `O(1)` extra space.

```python
def find_max(nums):
    if not nums:
        raise ValueError("empty sequence")

    best = nums[0]

    for value in nums[1:]:
        if value > best:
            best = value

    return best
```

Better for production Python:

```python
best = max(nums)
```

Implement manually when learning the algorithm.

---

## 7.4 Reverse an Array In Place

In-place reversal swaps symmetric elements from the two ends and moves inward until the pointers meet. Each element is touched a constant number of times, giving `O(n)` time and `O(1)` auxiliary space. The input array is mutated, so callers that need the original order must copy it first.

```python
def reverse_array(nums):
    left = 0
    right = len(nums) - 1

    while left < right:
        nums[left], nums[right] = nums[right], nums[left]
        left += 1
        right -= 1
```

Complexity:

```text
Time: O(n)
Extra space: O(1)
```

---

## 7.5 Rotate Array Right by k

Normalize `k` with `k %= n` after handling an empty list. A slicing solution is concise but allocates new lists; an in-place three-reversal method uses constant auxiliary storage but mutates the original list.

Example:

```text
[1,2,3,4,5,6,7], k=3

→ [5,6,7,1,2,3,4]
```

Using slicing:

```python
def rotate(nums, k):
    if not nums:
        return nums

    k %= len(nums)
    return nums[-k:] + nums[:-k]
```

Time:

```text
O(n)
```

Extra space:

```text
O(n)
```

---

## 7.6 Kadane's Algorithm — Maximum Subarray Sum

An algorithm is a finite, unambiguous procedure that converts an input into the required output. A useful explanation of an algorithm should state its preconditions, the main invariant or idea that keeps it correct, when it stops, and its time and space complexity.

Problem:

Find the contiguous subarray with maximum sum.

```python
def max_subarray(nums):
    current = nums[0]
    best = nums[0]

    for x in nums[1:]:
        current = max(x, current + x)
        best = max(best, current)

    return best
```

Example:

```text
[-2,1,-3,4,-1,2,1,-5,4]

Best subarray:
[4,-1,2,1]

Sum = 6
```

Complexity:

```text
Time: O(n)
Space: O(1)
```

---

# 8. Strings

A string is a sequence of characters, but its exact behavior depends on the language's string model and character encoding. DSA string problems commonly need indexing/traversal, frequency counting, substring handling, comparison, prefix/suffix reasoning, or pattern matching. Always check whether the task assumes simple ASCII-like characters or full Unicode text.

Python strings are immutable sequences.

```python
text = "algorithm"
```

## 8.1 Character Access

Character access means reading a symbol at a particular position in a string. Before using an index-based approach, know what one index represents in the language: a byte, UTF-16 code unit, Unicode code point, or grapheme cluster. For basic ASCII-style DSA exercises, direct indexing is usually sufficient; production international text may require Unicode-aware iteration.

```python
text[0]
text[-1]
```

## 8.2 String Immutability

An immutable string cannot be modified in place after creation. Operations that appear to change it actually create a new string, which matters in loops because repeated concatenation can allocate many temporary objects. For many edits, collect pieces in a mutable buffer/list and build the final string once.

This is invalid:

```python
text[0] = "A"
```

Create a new string instead.

---

## 8.3 String Concatenation in Loops

When a loop repeatedly appends text, prefer a builder or a collection of pieces followed by one join/concatenation step. This avoids repeatedly copying an ever-growing immutable string and makes the intended construction process explicit.

Avoid repeated concatenation for large workloads:

```python
result = ""

for word in words:
    result += word
```

Prefer:

```python
result = "".join(words)
```

---

## 8.4 Palindrome

A palindrome reads the same forward and backward under the problem's comparison rules. The standard two-pointer check compares the leftmost and rightmost relevant characters and moves inward, stopping on the first mismatch. Time is `O(n)` and extra space can be `O(1)` when normalization is not stored separately.

```python
def is_palindrome(text):
    left = 0
    right = len(text) - 1

    while left < right:
        if text[left] != text[right]:
            return False

        left += 1
        right -= 1

    return True
```

---

## 8.5 Character Frequency

A frequency table records how many times each value occurs. Python's `Counter` constructs this mapping directly from an iterable and is useful when counts—not just membership—are needed.

```python
from collections import Counter

counts = Counter("banana")
```

Produces conceptually:

```python
{
    "b": 1,
    "a": 3,
    "n": 2
}
```

Manual version:

```python
def frequency(text):
    counts = {}

    for ch in text:
        counts[ch] = counts.get(ch, 0) + 1

    return counts
```

---

## 8.6 Anagram Check

Two strings are anagrams when they contain the same symbols with the same frequencies, subject to the problem's normalization rules. A frequency map gives `O(n)` expected time and avoids sorting; sorting both strings is simpler in some cases but typically costs `O(n log n)`. Decide explicitly whether case, spaces, punctuation, and Unicode normalization matter.

```python
from collections import Counter

def is_anagram(a, b):
    return Counter(a) == Counter(b)
```

Example:

```text
listen
silent
```

---

## 8.7 Longest Common Prefix

The longest common prefix is the longest starting substring shared by every string in the collection. A practical approach uses one string as the candidate prefix and shortens/compares it against the others. Handle an empty collection explicitly; the answer is an empty string when no first character is shared.

```python
def longest_common_prefix(words):
    if not words:
        return ""

    prefix = words[0]

    for word in words[1:]:
        while not word.startswith(prefix):
            prefix = prefix[:-1]

            if not prefix:
                return ""

    return prefix
```

---

# 9. Linked Lists

A linked list stores values in nodes connected by references rather than by contiguous indexed positions. This makes pointer rewiring cheap once the relevant node is known, but random access is slow because traversal normally starts from the head. Linked-list problems therefore focus heavily on pointer movement, insertion/removal, reversal, cycle detection, and fast/slow-pointer techniques.

A linked list stores values in nodes connected through references.

## 9.1 Singly Linked List Node

A singly linked list node stores a value plus one `next` reference. Access to the `i`th element requires traversal from the head, but insertion/removal near a known node only changes a small number of links. Keep ownership of the head (and optional tail) explicit.

```python
class ListNode:
    def __init__(self, value=0, next_node=None):
        self.value = value
        self.next = next_node
```

Example:

```text
10 → 20 → 30 → None
```

---

## 9.2 Array vs Linked List

| Operation | Array/List | Linked List |
|---|---:|---:|
| Access by index | O(1) | O(n) |
| Search | O(n) | O(n) |
| Insert at front | O(n) | O(1) |
| Delete front | O(n) | O(1) |
| Append | O(1) amortized | O(1) with tail |
| Memory locality | Better | Worse |

---

## 9.3 Traverse a Linked List

Start from `head`, process the current node, then advance to `current.next` until the reference becomes `None`. This visits each node exactly once (`O(n)` time) and requires `O(1)` extra space for the traversal pointer.

```python
def print_list(head):
    current = head

    while current:
        print(current.value)
        current = current.next
```

---

## 9.4 Reverse Linked List

Reversing a singly linked list rewires each node's `next` reference. Keep three pieces of state: the previous node, the current node, and the original next node so the remainder of the list is not lost before reassignment. The iterative algorithm runs in `O(n)` time and `O(1)` extra space.

```python
def reverse_list(head):
    previous = None
    current = head

    while current:
        next_node = current.next
        current.next = previous
        previous = current
        current = next_node

    return previous
```

Conceptually:

```text
Before:
1 → 2 → 3 → None

After:
3 → 2 → 1 → None
```

Complexity:

```text
Time: O(n)
Space: O(1)
```

---

## 9.5 Find Middle Node

Use two references: `slow` advances one node at a time and `fast` advances two. When `fast` reaches the end, `slow` points to the middle (for even-length lists, define which of the two middle nodes the implementation returns). The method runs in `O(n)` time and `O(1)` extra space without a preliminary length pass.

Use slow and fast pointers.

```python
def middle_node(head):
    slow = head
    fast = head

    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next

    return slow
```

---

## 9.6 Detect Cycle — Floyd's Algorithm

An algorithm is a finite, unambiguous procedure that converts an input into the required output. A useful explanation of an algorithm should state its preconditions, the main invariant or idea that keeps it correct, when it stops, and its time and space complexity.

```python
def has_cycle(head):
    slow = head
    fast = head

    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next

        if slow is fast:
            return True

    return False
```

Complexity:

```text
Time: O(n)
Space: O(1)
```

---

## 9.7 Doubly Linked List

A doubly linked list stores both `next` and `prev` links. This enables traversal in both directions and makes deletion of a known node easier because its predecessor is directly available, at the cost of extra memory and more pointer updates that must remain consistent.

A doubly linked node contains:

```text
previous ← node → next
```

Useful for:

- LRU cache
- Browser forward/back history
- Undo/redo structures
- Ordered collections requiring fast node removal

---

# 10. Stacks

A stack follows:

```text
LIFO
Last In, First Out
```

Example:

```text
Push A
Push B
Push C

Pop → C
```

Use Python list:

```python
stack = []

stack.append(10)
stack.append(20)

value = stack.pop()
```

Operations:

```text
push: O(1) amortized
pop: O(1)
top: O(1)
```

---

## 10.1 Balanced Parentheses

Balanced-bracket checking uses a stack of opening brackets. Each closing bracket must match the most recent unmatched opening bracket, so a mismatch or an empty stack fails immediately; after the scan, the stack must also be empty. The algorithm is `O(n)` time and `O(n)` worst-case space.

```python
def is_valid_parentheses(s):
    pairs = {
        ")": "(",
        "]": "[",
        "}": "{",
    }

    stack = []

    for ch in s:
        if ch in "([{":
            stack.append(ch)

        elif ch in pairs:
            if not stack or stack.pop() != pairs[ch]:
                return False

    return not stack
```

Use cases:

- Expression parsing
- Compiler syntax
- Nested structures
- HTML/XML-like validation

---

## 10.2 Evaluate Reverse Polish Notation

Reverse Polish Notation places operators after operands. Scan tokens left to right: push numbers; when an operator appears, pop the required operands in the correct order, compute, and push the result. A stack is ideal because the most recent operands are consumed first.

```python
def eval_rpn(tokens):
    stack = []

    for token in tokens:
        if token not in {"+", "-", "*", "/"}:
            stack.append(int(token))
            continue

        b = stack.pop()
        a = stack.pop()

        if token == "+":
            stack.append(a + b)
        elif token == "-":
            stack.append(a - b)
        elif token == "*":
            stack.append(a * b)
        else:
            stack.append(int(a / b))

    return stack[-1]
```

---

# 11. Queues and Deques

A queue follows:

```text
FIFO
First In, First Out
```

Do not normally use:

```python
queue = []
queue.pop(0)
```

because removing from the front of a list costs:

```text
O(n)
```

Use `deque`.

```python
from collections import deque

queue = deque()

queue.append("A")
queue.append("B")

queue.popleft()
```

Typical complexity:

```text
append: O(1)
appendleft: O(1)
pop: O(1)
popleft: O(1)
```

---

## 11.1 Queue Use Cases

A queue follows **First In, First Out (FIFO)** order: the earliest enqueued item is processed first. The key operations are enqueue, dequeue, front/peek, and emptiness checking. Queues are a natural fit for breadth-first search, scheduling, buffering, and any workflow that must preserve arrival order.

- BFS
- Job processing
- Message buffering
- Print queue
- Request scheduling

---

## 11.2 Deque Use Cases

A deque (double-ended queue) supports insertion and removal at both the front and back. It can behave as either a stack or a queue and is especially useful for sliding-window algorithms and 0-1 BFS. Prefer an implementation whose front and back operations are constant-time rather than an array operation that shifts many elements.

A deque supports efficient operations at both ends.

```python
dq = deque()

dq.append(10)
dq.appendleft(5)
dq.pop()
dq.popleft()
```

Useful for:

- Sliding-window maximum
- BFS
- Double-ended scheduling
- Recent-event tracking

---

# 12. Hash Tables, Dictionaries, and Sets

Hash-based structures trade extra memory for fast average-case membership, lookup, insertion, and deletion. They are especially useful for frequency tables, duplicate detection, complement lookup, caching, and visited-state tracking. Their ordering guarantees and worst-case behavior depend on the language and implementation, so do not assume sorted iteration unless the API explicitly provides it.

Python:

```text
dict → hash map
set  → hash set
```

## 12.1 Dictionary

```python
student = {
    "name": "Alex",
    "score": 95,
}
```

Common average complexities:

| Operation | Average |
|---|---:|
| Lookup | O(1) |
| Insert | O(1) |
| Delete | O(1) |

Worst-case theoretical behavior can degrade, but average-case hash-table performance is the practical model used in most DSA problems.

---

## 12.2 Set

A set stores unique values and is designed for membership testing. In DSA it is useful for duplicate detection, visited states, and window membership. It does not provide positional indexing; use a sequence when index-based order is the main operation.

```python
seen = set()

seen.add(10)
10 in seen
```

Use a set when you care about membership, uniqueness, or duplicates.

---

## 12.3 Two Sum

The optimized Two Sum pattern trades memory for speed. While scanning, compute the complement `target - current`; if that complement was seen earlier, return the matching indexes/values, otherwise store the current item. With a hash map this is `O(n)` expected time and `O(n)` extra space.

Problem:

Find two indices whose values sum to target.

```python
def two_sum(nums, target):
    seen = {}

    for i, value in enumerate(nums):
        needed = target - value

        if needed in seen:
            return [seen[needed], i]

        seen[value] = i

    return []
```

Complexity:

```text
Time: O(n) average
Space: O(n)
```

Naive double loop:

```text
O(n²)
```

---

## 12.4 First Non-Repeating Character

Count each character first, then scan the original string again and return the first character whose frequency is one. The second pass is important because a hash map alone does not necessarily express the required original-position rule. Overall time is `O(n)`.

```python
from collections import Counter

def first_unique_char(s):
    counts = Counter(s)

    for i, ch in enumerate(s):
        if counts[ch] == 1:
            return i

    return -1
```

---

## 12.5 `defaultdict`

`defaultdict(factory)` creates a missing value automatically using the supplied factory. It simplifies grouping/counting such as `defaultdict(list)` or `defaultdict(int)`, but accessing a missing key **inserts** it, which differs from `dict.get()` and can matter when merely checking presence.

```python
from collections import defaultdict

graph = defaultdict(list)

graph["A"].append("B")
```

Useful when values have a natural default.

---

## 12.6 `Counter`

`Counter` is a dictionary subclass specialized for frequency counting. Construct it from an iterable to obtain element counts, then use normal mapping access or helpers such as `most_common`. It is clearer than a manual loop when frequency counting is the whole operation.

```python
from collections import Counter

Counter([1, 1, 1, 2, 2, 3])
```

Very useful for:

- Frequency counting
- Anagrams
- Majority/frequency problems
- Multiset-like logic

---

# 13. Searching Algorithms

Searching asks whether, where, or under what condition a target can be found. Start with linear search as the no-precondition baseline, then use binary search when ordering or monotonicity lets you safely discard large parts of the search space.

## 13.1 Linear Search

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

```python
def linear_search(arr, target):
    for i, value in enumerate(arr):
        if value == target:
            return i

    return -1
```

Complexity:

```text
Time: O(n)
Space: O(1)
```

Use when:

- Data is unsorted
- Input is small
- Search happens once

---

## 13.2 Binary Search

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

Requirement:

> The search space must be sorted or satisfy a monotonic condition.

```python
def binary_search(arr, target):
    left = 0
    right = len(arr) - 1

    while left <= right:
        mid = left + (right - left) // 2

        if arr[mid] == target:
            return mid

        if arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return -1
```

Complexity:

```text
Time: O(log n)
Space: O(1)
```

---

## 13.3 Python `bisect`

`bisect_left(sorted_list, x)` returns the first insertion index before equal values; `bisect_right` returns the insertion index after equal values. The search for the index is `O(log n)`, but inserting into a Python list at that index is still `O(n)` because elements shift.

```python
from bisect import bisect_left

arr = [1, 3, 3, 5, 8]

index = bisect_left(arr, 3)
# 1
```

`bisect_left` returns the leftmost insertion position.

`bisect_right` returns the position after existing equal values.

---

# 14. Sorting Algorithms

Sorting rearranges values according to an ordering rule so later operations can exploit structure. Learn not only the code but also stability, in-place behavior, best/average/worst complexity, comparator requirements, and when a language's built-in sort is preferable to a manual algorithm.

Sorting is one of the most important algorithm families.

## 14.1 Sorting Summary

| Algorithm | Best | Average | Worst | Extra Space | Stable? |
|---|---:|---:|---:|---:|---|
| Bubble | O(n)* | O(n²) | O(n²) | O(1) | Yes |
| Selection | O(n²) | O(n²) | O(n²) | O(1) | Usually No |
| Insertion | O(n) | O(n²) | O(n²) | O(1) | Yes |
| Merge | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes |
| Quick | O(n log n) | O(n log n) | O(n²) | stack dependent | Usually No |
| Heap | O(n log n) | O(n log n) | O(n log n) | O(1)** | No |
| Counting | O(n+k) | O(n+k) | O(n+k) | O(k) | Can be |
| Radix | digit-dependent | digit-dependent | digit-dependent | extra | Usually |

\* optimized bubble sort  
\** for an in-place heap implementation

Python's built-in sorting uses **Timsort**, which is stable and highly optimized.

---

## 14.2 Bubble Sort

Bubble sort repeatedly compares adjacent elements and swaps pairs that are out of order. After each full pass, one extreme value has moved to its final end position. It is easy to learn but `O(n²)` in average/worst cases; with an early-exit flag it can be `O(n)` on already sorted input.

```python
def bubble_sort(arr):
    arr = arr[:]
    n = len(arr)

    for end in range(n - 1, 0, -1):
        swapped = False

        for i in range(end):
            if arr[i] > arr[i + 1]:
                arr[i], arr[i + 1] = arr[i + 1], arr[i]
                swapped = True

        if not swapped:
            break

    return arr
```

Good for:

- Learning
- Tiny or nearly sorted data in educational contexts

Not typically used for production sorting.

---

## 14.3 Selection Sort

Selection sort repeatedly chooses the smallest (or largest) remaining element and places it into the next final position. It performs `O(n²)` comparisons regardless of initial order and only `O(n)` swaps, so it is mostly educational or useful when writes are unusually expensive. The usual in-place form is not stable.

```python
def selection_sort(arr):
    arr = arr[:]

    for i in range(len(arr)):
        minimum = i

        for j in range(i + 1, len(arr)):
            if arr[j] < arr[minimum]:
                minimum = j

        arr[i], arr[minimum] = arr[minimum], arr[i]

    return arr
```

---

## 14.4 Insertion Sort

Insertion sort grows a sorted prefix one element at a time. For each new value, it shifts larger prefix elements to the right until the correct insertion position opens. It is stable with the usual comparison, in-place, `O(n²)` in the average/worst case, and `O(n)` on already or nearly sorted data.

```python
def insertion_sort(arr):
    arr = arr[:]

    for i in range(1, len(arr)):
        current = arr[i]
        j = i - 1

        while j >= 0 and arr[j] > current:
            arr[j + 1] = arr[j]
            j -= 1

        arr[j + 1] = current

    return arr
```

Useful when:

- Data is small
- Data is almost sorted

---

## 14.5 Merge Sort

Merge sort divides the sequence into halves, recursively sorts each half, and merges two sorted halves in linear time. Its recurrence leads to `O(n log n)` time in all standard cases; array implementations typically need `O(n)` auxiliary merge storage. Merge sort is stable when equal elements are taken from the left half first.

Divide:

```text
[8,3,5,4]

→ [8,3] [5,4]
→ [8] [3] [5] [4]
```

Merge:

```text
[3,8] [4,5]
→ [3,4,5,8]
```

Implementation:

```python
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
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1

    result.extend(left[i:])
    result.extend(right[j:])

    return result
```

Complexity:

```text
Time: O(n log n)
Space: O(n)
```

---

## 14.6 Quick Sort

Quick sort partitions elements around a pivot so smaller and larger values move to opposite sides, then recursively sorts the partitions. Average time is `O(n log n)` but poor pivot choices can produce `O(n²)`. Partition scheme, duplicate handling, and recursion depth are important implementation details.

```python
def quick_sort(arr):
    if len(arr) <= 1:
        return arr

    pivot = arr[len(arr) // 2]

    lower = [x for x in arr if x < pivot]
    equal = [x for x in arr if x == pivot]
    higher = [x for x in arr if x > pivot]

    return quick_sort(lower) + equal + quick_sort(higher)
```

This is easy to understand but allocates extra lists.

Classic in-place quicksort uses partitioning.

Average:

```text
O(n log n)
```

Worst:

```text
O(n²)
```

---

## 14.7 Python Sorting

`sorted(iterable)` returns a new list, while `list.sort()` mutates an existing list and returns `None`. Both use stable Timsort and accept `key=` for derived ordering; prefer `key` over custom comparison emulation because Python's sorting API is key-oriented.

```python
numbers.sort()
```

modifies the original list.

```python
sorted_numbers = sorted(numbers)
```

returns a new list.

Custom sorting:

```python
employees = [
    ("A", 30),
    ("B", 25),
    ("C", 40),
]

employees.sort(key=lambda item: item[1])
```

Multi-key sorting:

```python
records.sort(key=lambda x: (x[0], -x[1]))
```

---

# 15. Two Pointers

Two pointers maintain two indexes or references whose movement eliminates unnecessary repeated work. Common forms are opposite-end pointers on sorted data and same-direction read/write pointers for in-place filtering. The technique is most valuable when pointer movement can be justified by an invariant, such as sorted order or a maintained valid region.

Two pointers use two indices that move according to a condition.

Common situations:

- Sorted arrays
- Pair problems
- Palindromes
- Removing duplicates
- Partitioning
- Linked-list slow/fast pointer problems

---

## 15.1 Pair Sum in Sorted Array

With sorted input, place one pointer at each end. If the sum is too small, moving the left pointer right is the only move that can increase it; if the sum is too large, move the right pointer left. This invariant gives `O(n)` time and `O(1)` extra space after sorting is already available.

```python
def pair_sum_sorted(nums, target):
    left = 0
    right = len(nums) - 1

    while left < right:
        total = nums[left] + nums[right]

        if total == target:
            return left, right

        if total < target:
            left += 1
        else:
            right -= 1

    return None
```

Complexity:

```text
O(n)
```

instead of:

```text
O(n²)
```

---

## 15.2 Remove Duplicates from Sorted Array

Because the array is sorted, equal values appear next to one another. A read pointer scans every element while a write pointer marks where the next distinct value belongs. The algorithm runs in `O(n)` time and can overwrite the input in place using `O(1)` extra space; the returned length/count tells the caller which prefix contains the unique values.

```python
def remove_duplicates(nums):
    if not nums:
        return 0

    write = 1

    for read in range(1, len(nums)):
        if nums[read] != nums[read - 1]:
            nums[write] = nums[read]
            write += 1

    return write
```

---

# 16. Sliding Window

A sliding window tracks a contiguous range while updating only the information that changes when the range expands or shrinks. Fixed-size windows are used when the length is known; variable-size windows adjust a boundary until a validity condition is restored. The usual goal is to replace repeated recomputation of every subarray or substring with a single linear pass.

Sliding window is used for contiguous subarray or substring problems.

Typical clues:

```text
longest substring
shortest subarray
maximum sum of k elements
at most k
minimum window
continuous segment
```

---

## 16.1 Fixed-Size Window

A fixed-size sliding window maintains an aggregate for exactly `k` consecutive elements. Build the first window, then for each shift subtract/remove the outgoing contribution and add the incoming one. This turns many `O(nk)` repeated-window calculations into `O(n)`.

Maximum sum of any subarray of size `k`.

```python
def max_sum_k(nums, k):
    if k <= 0 or k > len(nums):
        raise ValueError("invalid k")

    window_sum = sum(nums[:k])
    best = window_sum

    for right in range(k, len(nums)):
        window_sum += nums[right]
        window_sum -= nums[right - k]
        best = max(best, window_sum)

    return best
```

Complexity:

```text
O(n)
```

Instead of recalculating every window:

```text
O(nk)
```

---

## 16.2 Variable-Size Window

A variable-size sliding window expands one boundary and shrinks the other whenever the validity constraint is violated. This is linear when each boundary moves forward at most `n` times and when window state can be updated incrementally. The validity condition must be monotonic enough that shrinking can restore it.

Longest substring without repeated characters:

```python
def length_of_longest_substring(s):
    last_seen = {}
    left = 0
    best = 0

    for right, ch in enumerate(s):
        if ch in last_seen and last_seen[ch] >= left:
            left = last_seen[ch] + 1

        last_seen[ch] = right
        best = max(best, right - left + 1)

    return best
```

---

# 17. Prefix Sum, Suffix Sum, and Difference Arrays

Prefix and suffix accumulations summarize data from opposite directions, while difference arrays summarize changes across ranges. These techniques trade `O(n)` preprocessing for much cheaper repeated queries or batched updates and are especially sensitive to indexing conventions.

## 17.1 Prefix Sum

A prefix sum precomputes cumulative totals so that later range sums can be answered by subtraction. With the common convention `prefix[i] = sum of elements before i`, the sum of the half-open range `[left, right)` is `prefix[right] - prefix[left]`. Building the prefix array costs `O(n)` time and each range query then costs `O(1)`.

For:

```text
nums = [2, 4, 1, 7]
```

prefix sum:

```text
[0, 2, 6, 7, 14]
```

Implementation:

```python
def prefix_sum(nums):
    prefix = [0]

    for x in nums:
        prefix.append(prefix[-1] + x)

    return prefix
```

Range sum `[left, right]`:

```python
range_sum = prefix[right + 1] - prefix[left]
```

After preprocessing:

```text
Range query: O(1)
```

---

## 17.2 Prefix Frequency

A frequency table records how many times each value occurs. Python's `Counter` constructs this mapping directly from an iterable and is useful when counts—not just membership—are needed.

For strings or bounded values, prefix counts can answer repeated range-frequency queries.

---

## 17.3 Suffix Sum

A suffix sum stores cumulative totals from the right. With a clear convention such as `suffix[i] = sum(arr[i:])`, a suffix query is direct and left/right aggregate comparisons become easy. Building all suffix sums is `O(n)` time and space.

```python
def suffix_sum(nums):
    suffix = [0] * (len(nums) + 1)

    for i in range(len(nums) - 1, -1, -1):
        suffix[i] = nums[i] + suffix[i + 1]

    return suffix
```

Useful when the future/right-side aggregate is repeatedly needed.

---

## 17.4 Difference Array

A difference array represents the *changes* between positions so that many range updates can be recorded cheaply. A range addition marks where an effect starts and where it stops; one final prefix accumulation reconstructs the resulting values. It is useful when updates are numerous but point-by-point results are only needed after all updates are known.

Difference arrays efficiently apply many range increments.

Suppose we repeatedly do:

```text
add value x to every position from l to r
```

Instead of updating every element:

```python
diff[l] += x
diff[r + 1] -= x
```

Then reconstruct using prefix sums.

```python
def range_additions(n, updates):
    diff = [0] * (n + 1)

    for left, right, value in updates:
        diff[left] += value

        if right + 1 < n:
            diff[right + 1] -= value

    result = [0] * n
    running = 0

    for i in range(n):
        running += diff[i]
        result[i] = running

    return result
```

---

# 18. Intervals

Interval problems represent ranges such as time spans, coordinates, or reservations. Before coding, define whether endpoints are inclusive or exclusive and whether touching intervals overlap; that decision controls sorting, merge conditions, sweep-line events, and off-by-one behavior.

Intervals often appear as:

```text
[start, end]
```

Common tasks:

- Merge overlapping intervals
- Insert interval
- Detect conflicts
- Meeting-room scheduling
- Count simultaneous events

---

## 18.1 Merge Intervals

To merge overlapping intervals, first sort by start coordinate. Keep the last merged interval; if the next interval overlaps under the chosen endpoint convention, extend the end, otherwise start a new merged interval. Sorting dominates at `O(n log n)`; the scan itself is `O(n)`.

```python
def merge_intervals(intervals):
    if not intervals:
        return []

    intervals.sort(key=lambda x: x[0])

    merged = [intervals[0]]

    for start, end in intervals[1:]:
        last_end = merged[-1][1]

        if start <= last_end:
            merged[-1][1] = max(last_end, end)
        else:
            merged.append([start, end])

    return merged
```

Example:

```text
[[1,3], [2,6], [8,10], [9,12]]

→ [[1,6], [8,12]]
```

Complexity:

```text
Sorting: O(n log n)
Merge scan: O(n)
Overall: O(n log n)
```

---

# 19. Binary Search Patterns

Binary search applies when a search space is ordered or when a yes/no feasibility condition changes monotonically. Each iteration discards roughly half of the remaining candidates, giving `O(log n)` iterations. Correct boundary handling is the main difficulty: define exactly what `left`, `right`, and `mid` mean and decide whether the interval is closed or half-open.

Binary search is more than finding a number.

It can search any **monotonic search space**.

---

## 19.1 First Occurrence

To find the first occurrence in sorted data, binary search does not stop immediately on equality. Record the matching index, then continue searching the left half because an earlier equal value may exist. This remains `O(log n)` time.

```python
def first_occurrence(arr, target):
    left = 0
    right = len(arr) - 1
    answer = -1

    while left <= right:
        mid = (left + right) // 2

        if arr[mid] >= target:
            if arr[mid] == target:
                answer = mid
            right = mid - 1
        else:
            left = mid + 1

    return answer
```

---

## 19.2 Binary Search on Answer

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

Suppose the question asks:

```text
What is the minimum capacity needed?
What is the smallest maximum workload?
What is the minimum speed that completes the task?
```

If a candidate value can be checked as:

```text
possible / impossible
```

and feasibility is monotonic, binary search may apply.

General template:

```python
def binary_search_answer(low, high, feasible):
    answer = high

    while low <= high:
        mid = (low + high) // 2

        if feasible(mid):
            answer = mid
            high = mid - 1
        else:
            low = mid + 1

    return answer
```

---

# 20. Trees

A tree is a connected acyclic hierarchical structure with nodes linked by parent/child relationships. Tree algorithms are easiest to understand recursively: define what one subtree call returns, choose a traversal order, and account for tree height because recursion/operation cost can degrade on skewed trees.

A tree is a hierarchical structure with nodes and edges.

Terminology:

```text
Root
Parent
Child
Sibling
Leaf
Depth
Height
Subtree
Ancestor
Descendant
```

---

## 20.1 Binary Tree Node

A binary tree node has at most two children, conventionally `left` and `right`. Unlike a BST, a general binary tree has no ordering rule unless the problem states one; searches therefore usually require traversal rather than directional comparison.

```python
class TreeNode:
    def __init__(self, value=0, left=None, right=None):
        self.value = value
        self.left = left
        self.right = right
```

---

## 20.2 DFS Traversals

Depth-first search explores one branch as far as possible before returning to try another branch. It can be implemented recursively or with an explicit stack and is widely used for connected components, cycle detection, tree processing, path exploration, topological reasoning, and many backtracking-style searches. Track visited state in cyclic graphs to avoid endless revisits.

### Preorder

Preorder traversal visits **node → left subtree → right subtree**. It is useful when the parent must be processed before its children, such as copying a tree, serializing certain tree formats, or producing prefix-style expression order. A complete traversal visits every node once, so time is `O(n)`.

```text
Root → Left → Right
```

```python
def preorder(root):
    if not root:
        return []

    return [root.value] + preorder(root.left) + preorder(root.right)
```

### Inorder

Inorder traversal visits **left subtree → node → right subtree**. On a Binary Search Tree with a consistent ordering rule, this produces keys in sorted order. A complete traversal is `O(n)` time and uses `O(h)` call-stack/explicit-stack space for tree height `h`.

```text
Left → Root → Right
```

```python
def inorder(root):
    if not root:
        return []

    return inorder(root.left) + [root.value] + inorder(root.right)
```

### Postorder

Postorder traversal visits **left subtree → right subtree → node**. Because children are processed before their parent, it is useful for deleting trees, computing subtree aggregates, and many tree-DP problems. A complete traversal is `O(n)` time and uses `O(h)` traversal stack space.

```text
Left → Right → Root
```

```python
def postorder(root):
    if not root:
        return []

    return postorder(root.left) + postorder(root.right) + [root.value]
```

---

## 20.3 Iterative DFS

Depth-first search explores one branch as far as possible before returning to try another branch. It can be implemented recursively or with an explicit stack and is widely used for connected components, cycle detection, tree processing, path exploration, topological reasoning, and many backtracking-style searches. Track visited state in cyclic graphs to avoid endless revisits.

```python
def preorder_iterative(root):
    if not root:
        return []

    stack = [root]
    result = []

    while stack:
        node = stack.pop()
        result.append(node.value)

        if node.right:
            stack.append(node.right)

        if node.left:
            stack.append(node.left)

    return result
```

---

## 20.4 BFS / Level Order

Level-order traversal is BFS on a tree. Use a queue to process nodes in increasing depth; if the output is grouped by levels, capture the queue size at the start of each level so newly enqueued children belong to the next group.

```python
from collections import deque

def level_order(root):
    if not root:
        return []

    queue = deque([root])
    result = []

    while queue:
        level = []

        for _ in range(len(queue)):
            node = queue.popleft()
            level.append(node.value)

            if node.left:
                queue.append(node.left)

            if node.right:
                queue.append(node.right)

        result.append(level)

    return result
```

---

## 20.5 Maximum Depth

Maximum tree depth is the number of nodes (or edges, depending on the chosen convention) on the longest root-to-leaf path. A recursive solution returns `1 + max(leftDepth, rightDepth)` for a non-null node. It visits each node once: `O(n)` time and `O(h)` stack space.

```python
def max_depth(root):
    if not root:
        return 0

    return 1 + max(
        max_depth(root.left),
        max_depth(root.right),
    )
```

---

## 20.6 Tree Diameter

Diameter = longest path between any two nodes.

```python
def diameter_of_tree(root):
    best = 0

    def depth(node):
        nonlocal best

        if not node:
            return 0

        left = depth(node.left)
        right = depth(node.right)

        best = max(best, left + right)

        return 1 + max(left, right)

    depth(root)
    return best
```

This is a common **postorder tree DP** pattern.

---

# 21. Binary Search Trees

A Binary Search Tree (BST) maintains an ordering invariant: values in one subtree compare before the node and values in the other compare after it, according to the chosen duplicate policy. Operations depend on tree height, so an unbalanced BST can degrade from `O(log n)` expected/balanced behavior to `O(n)`.

A Binary Search Tree (BST) normally satisfies:

```text
left values < node value
right values > node value
```

Policies for duplicates vary.

---

## 21.1 Search

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

```python
def bst_search(root, target):
    current = root

    while current:
        if current.value == target:
            return current

        if target < current.value:
            current = current.left
        else:
            current = current.right

    return None
```

Average in a balanced BST:

```text
O(log n)
```

Worst in a skewed BST:

```text
O(n)
```

---

## 21.2 Insert

Insertion must preserve the data structure's invariant. For an ordered tree, compare the new key at each node and descend to the appropriate child until an empty position is found; for duplicate keys, follow the policy defined by the problem. Runtime is proportional to the structure's height.

```python
def bst_insert(root, value):
    if root is None:
        return TreeNode(value)

    if value < root.value:
        root.left = bst_insert(root.left, value)
    else:
        root.right = bst_insert(root.right, value)

    return root
```

---

## 21.3 Inorder Traversal of BST

Traversal means visiting each relevant element/node in a defined order. The important state is the current position and the rule for advancing to the next one. A full traversal is usually `O(n)` for a linear structure, while trees/graphs additionally require a stack/queue or recursion and, for cyclic graphs, visited tracking.

Inorder traversal produces sorted values.

---

## 21.4 Validate BST

Validating a BST requires checking the **entire allowed range** for each node, not only comparing a node with its immediate children. Pass lower/upper bounds (or use inorder ordering) so descendants cannot violate an ancestor's constraint. Decide how duplicates are handled before choosing strict or non-strict comparisons.

```python
def is_valid_bst(root):
    def validate(node, low, high):
        if not node:
            return True

        if not (low < node.value < high):
            return False

        return (
            validate(node.left, low, node.value)
            and validate(node.right, node.value, high)
        )

    return validate(root, float("-inf"), float("inf"))
```

---

# 22. Heaps and Priority Queues

A heap is a tree-based structure used to efficiently access the minimum or maximum element.

Python's `heapq` implements a **min-heap**.

```python
import heapq

heap = []

heapq.heappush(heap, 10)
heapq.heappush(heap, 3)
heapq.heappush(heap, 8)

smallest = heapq.heappop(heap)
# 3
```

Typical complexity:

```text
peek min: O(1)
push: O(log n)
pop min: O(log n)
heapify n items: O(n)
```

---

## 22.1 Max Heap in Python

A heap is a partially ordered tree structure commonly used to implement a priority queue. A min-heap exposes the smallest item; a max-heap exposes the largest. Insert and removal of the root are typically `O(log n)`, while reading the root is `O(1)`, making heaps ideal for top-k, scheduling, streaming minima/maxima, and graph algorithms such as Dijkstra or Prim.

Use negative values:

```python
heapq.heappush(heap, -value)
largest = -heapq.heappop(heap)
```

Modern Python environments may also provide max-heap helper APIs, but the negation pattern is universally familiar in interview code.

---

## 22.2 Top K Largest

A min-heap of size `k` can maintain the `k` largest values seen so far. Push candidates and remove the smallest whenever the heap exceeds `k`; at the end, the heap contains the desired top `k`. This uses `O(n log k)` time and `O(k)` extra space, often better than sorting all `n` items.

```python
import heapq

def top_k_largest(nums, k):
    return heapq.nlargest(k, nums)
```

For streaming scenarios, maintain a min-heap of size `k`.

```python
def top_k_stream(nums, k):
    heap = []

    for value in nums:
        if len(heap) < k:
            heapq.heappush(heap, value)
        elif value > heap[0]:
            heapq.heapreplace(heap, value)

    return heap
```

Complexity:

```text
O(n log k)
```

---

## 22.3 Priority Queue Use Cases

A queue follows **First In, First Out (FIFO)** order: the earliest enqueued item is processed first. The key operations are enqueue, dequeue, front/peek, and emptiness checking. Queues are a natural fit for breadth-first search, scheduling, buffering, and any workflow that must preserve arrival order.

- Task scheduling
- Dijkstra's algorithm
- Top-K problems
- Merge K sorted lists
- Event simulation
- CPU/job prioritization

---

# 23. Tries

A trie is a tree specialized for strings and prefixes.

Use cases:

- Autocomplete
- Dictionary search
- Prefix queries
- Spell checking
- Routing prefixes

---

## 23.1 Trie Implementation

This implementation turns the surrounding concept into concrete state and operations. Identify what each field stores, which method mutates that state, and what invariant must remain true after every operation; those details matter more than memorizing the exact syntax.

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_word = False


class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word):
        node = self.root

        for ch in word:
            node = node.children.setdefault(ch, TrieNode())

        node.is_word = True

    def search(self, word):
        node = self.root

        for ch in word:
            if ch not in node.children:
                return False
            node = node.children[ch]

        return node.is_word

    def starts_with(self, prefix):
        node = self.root

        for ch in prefix:
            if ch not in node.children:
                return False
            node = node.children[ch]

        return True
```

If word length is `L`, common operation time is:

```text
O(L)
```

---

# 24. Graphs

A graph models entities as vertices and relationships as edges. Before choosing an algorithm, determine whether the graph is directed or undirected, weighted or unweighted, cyclic or acyclic, and connected or disconnected. Those properties decide whether BFS, DFS, topological sorting, shortest-path algorithms, minimum-spanning-tree algorithms, or connectivity structures are appropriate.

A graph contains:

```text
Vertices / Nodes
Edges
```

Graphs can be:

- Directed
- Undirected
- Weighted
- Unweighted
- Cyclic
- Acyclic
- Connected
- Disconnected

---

## 24.1 Real-World Graph Examples

| Scenario | Node | Edge |
|---|---|---|
| Social network | Person | Friendship/follow |
| Maps | City/intersection | Road |
| Internet | Router | Connection |
| Dependencies | Package/task | Depends-on relation |
| Website | Page | Link |

---

## 24.2 Adjacency List

An adjacency list stores, for each vertex, the vertices (and optionally edge weights) directly connected to it. It uses `O(V + E)` space and is usually preferred for sparse graphs because traversing a vertex touches only its actual outgoing/incident edges. For undirected graphs, each edge is normally stored in both endpoint lists.

```python
graph = {
    "A": ["B", "C"],
    "B": ["A", "D"],
    "C": ["A"],
    "D": ["B"],
}
```

Typically efficient for sparse graphs.

---

## 24.3 BFS

Breadth-first search explores a graph or tree level by level using a queue. In an unweighted graph, the first time BFS reaches a vertex is through a path with the minimum number of edges from the start. With adjacency-list representation, a complete traversal is `O(V + E)` when each vertex is processed once.

```python
from collections import deque

def bfs(graph, start):
    queue = deque([start])
    visited = {start}
    order = []

    while queue:
        node = queue.popleft()
        order.append(node)

        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)

    return order
```

Complexity:

```text
O(V + E)
```

Typical use cases:

- Shortest path in unweighted graph
- Level traversal
- Minimum number of moves
- Nearest target search

---

## 24.4 DFS

Depth-first search explores one branch as far as possible before returning to try another branch. It can be implemented recursively or with an explicit stack and is widely used for connected components, cycle detection, tree processing, path exploration, topological reasoning, and many backtracking-style searches. Track visited state in cyclic graphs to avoid endless revisits.

Recursive:

```python
def dfs(graph, node, visited=None):
    if visited is None:
        visited = set()

    visited.add(node)

    for neighbor in graph[node]:
        if neighbor not in visited:
            dfs(graph, neighbor, visited)

    return visited
```

Complexity:

```text
O(V + E)
```

Use cases:

- Connectivity
- Cycle detection
- Components
- Backtracking-style exploration
- Topological algorithms
- Tree/graph structure analysis

---

## 24.5 Connected Components

A connected component is a maximal group of vertices reachable from one another (for the relevant directed/undirected definition). Scan all vertices; whenever an unvisited vertex is found, run BFS/DFS to mark one new component. Across the entire graph, adjacency-list traversal is `O(V + E)`.

```python
def count_components(graph):
    visited = set()
    components = 0

    for node in graph:
        if node in visited:
            continue

        components += 1
        stack = [node]

        while stack:
            current = stack.pop()

            if current in visited:
                continue

            visited.add(current)

            for neighbor in graph[current]:
                if neighbor not in visited:
                    stack.append(neighbor)

    return components
```

---

## 24.6 Cycle Detection in Undirected Graph

In an undirected graph, DFS/BFS can detect a cycle by seeing an already visited neighbor that is **not** the edge back to the current vertex's parent. Union-Find is another option when edges are processed incrementally: an edge joining two vertices already in the same set closes a cycle.

```python
def has_cycle_undirected(graph):
    visited = set()

    def dfs(node, parent):
        visited.add(node)

        for neighbor in graph[node]:
            if neighbor not in visited:
                if dfs(neighbor, node):
                    return True

            elif neighbor != parent:
                return True

        return False

    for node in graph:
        if node not in visited and dfs(node, None):
            return True

    return False
```

---

## 24.7 Topological Sort — Kahn's Algorithm

A topological ordering places every prerequisite before the items that depend on it. It exists only for a **directed acyclic graph (DAG)**. Common implementations use Kahn's algorithm with indegrees and a queue, or DFS with postorder; if all vertices cannot be ordered, the dependency graph contains a cycle.

Applicable to a **Directed Acyclic Graph (DAG)**.

```python
from collections import deque

def topological_sort(graph):
    indegree = {node: 0 for node in graph}

    for node in graph:
        for neighbor in graph[node]:
            indegree[neighbor] = indegree.get(neighbor, 0) + 1

    queue = deque(
        node for node, degree in indegree.items()
        if degree == 0
    )

    order = []

    while queue:
        node = queue.popleft()
        order.append(node)

        for neighbor in graph.get(node, []):
            indegree[neighbor] -= 1

            if indegree[neighbor] == 0:
                queue.append(neighbor)

    if len(order) != len(indegree):
        return None  # cycle exists

    return order
```

Use cases:

- Course prerequisites
- Build systems
- Job dependencies
- Deployment ordering

---

## 24.8 Dijkstra's Algorithm

Dijkstra's algorithm computes single-source shortest paths when edge weights are non-negative. Maintain tentative distances and repeatedly process the smallest-distance candidate from a min-priority queue; ignore stale queue entries whose distance no longer matches the best known value. Typical adjacency-list complexity is `O((V+E) log V)`.

Find shortest paths from one source in a graph with **non-negative edge weights**.

```python
import heapq

def dijkstra(graph, source):
    distances = {node: float("inf") for node in graph}
    distances[source] = 0

    heap = [(0, source)]

    while heap:
        distance, node = heapq.heappop(heap)

        if distance != distances[node]:
            continue

        for neighbor, weight in graph[node]:
            new_distance = distance + weight

            if new_distance < distances[neighbor]:
                distances[neighbor] = new_distance
                heapq.heappush(
                    heap,
                    (new_distance, neighbor),
                )

    return distances
```

Typical complexity with adjacency list + binary heap:

```text
O((V + E) log V)
```

Often simplified to:

```text
O(E log V)
```

---

# 25. Union-Find / Disjoint Set Union

Union-Find, also called Disjoint Set Union (DSU), maintains a collection of non-overlapping groups under two main operations: `find` identifies a representative and `union` merges groups. Path compression plus union by rank/size makes a long sequence of operations effectively near-constant time in practice. It is useful for dynamic connectivity, cycle detection in undirected graphs, Kruskal's MST, and component grouping.

Union-Find tracks which items belong to the same connected component.

Operations:

```text
find(x)
union(a, b)
```

Optimizations:

- Path compression
- Union by rank/size

---

## 25.1 Implementation

This implementation turns the surrounding concept into concrete state and operations. Identify what each field stores, which method mutates that state, and what invariant must remain true after every operation; those details matter more than memorizing the exact syntax.

```python
class DSU:
    def __init__(self, n):
        self.parent = list(range(n))
        self.size = [1] * n

    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])

        return self.parent[x]

    def union(self, a, b):
        root_a = self.find(a)
        root_b = self.find(b)

        if root_a == root_b:
            return False

        if self.size[root_a] < self.size[root_b]:
            root_a, root_b = root_b, root_a

        self.parent[root_b] = root_a
        self.size[root_a] += self.size[root_b]

        return True
```

Amortized complexity is extremely close to constant:

```text
O(α(n))
```

where `α` is the inverse Ackermann function.

---

## 25.2 Use Cases

Use **Union-Find / Disjoint Set Union** when the problem characteristics below are genuinely present. The list is a recognition aid, not a rule that every listed situation must use this approach.

- Connectivity queries
- Detect cycles
- Kruskal's MST
- Network grouping
- Account merging
- Dynamic component tracking

---

# 26. Greedy Algorithms

A greedy algorithm chooses the locally best decision at each step.

Greedy does **not** always work.

You need a reason or proof that local optimal choices lead to a global optimum.

---

## 26.1 Activity Selection

For the classic maximum-number-of-non-overlapping-intervals problem, sorting by finishing time and repeatedly choosing the earliest finishing compatible interval is optimal. The greedy choice leaves as much room as possible for future intervals; sorting dominates at `O(n log n)`.

Choose the maximum number of non-overlapping activities.

Greedy idea:

> Always choose the activity that finishes earliest.

```python
def max_activities(intervals):
    intervals.sort(key=lambda x: x[1])

    count = 0
    last_end = float("-inf")

    for start, end in intervals:
        if start >= last_end:
            count += 1
            last_end = end

    return count
```

---

## 26.2 Greedy Clues

A greedy algorithm commits to a locally best-looking choice without revisiting earlier decisions. That can be very efficient, but it is correct only when the problem has a property that makes local choices compatible with a global optimum. A convincing greedy solution should include a justification such as an exchange argument, cut property, or invariant—not merely an intuition that the choice looks best.

Problems involving:

- Earliest finish
- Smallest/largest available choice
- Minimizing waiting
- Maximizing count
- Scheduling
- Interval selection
- Huffman coding
- Minimum spanning tree

may involve greedy reasoning.

---

## 26.3 How to Validate Greedy Logic

Ask:

1. Can I exchange an optimal solution's first choice with my greedy choice without making it worse?
2. Does the remaining problem have the same structure?
3. Can local decisions harm a later requirement?
4. Is there a known counterexample?

---

# 27. Backtracking

Backtracking explores a decision tree by making a choice, recursively exploring what follows, and then undoing that choice before trying the next option. It is appropriate when the task asks for all valid combinations, permutations, placements, paths, or constraint-satisfying configurations. Pruning impossible branches early is often the difference between a practical and an impractical solution.

Backtracking explores possibilities and undoes decisions.

Template:

```python
def backtrack(state):
    if goal_reached(state):
        save_solution(state)
        return

    for choice in choices(state):
        make_choice(choice)
        backtrack(state)
        undo_choice(choice)
```

---

## 27.1 Generate Subsets

Generating all subsets explores two choices for each element: include it or exclude it. That creates `2^n` possible subsets, so exponential output size is unavoidable. Backtracking should add a **copy** of the current path to the result because the same mutable path is modified during later recursive calls.

```python
def subsets(nums):
    result = []
    path = []

    def backtrack(index):
        if index == len(nums):
            result.append(path.copy())
            return

        # Exclude
        backtrack(index + 1)

        # Include
        path.append(nums[index])
        backtrack(index + 1)
        path.pop()

    backtrack(0)
    return result
```

Complexity:

```text
O(2^n)
```

because there are `2^n` subsets.

---

## 27.2 Generate Permutations

Generating permutations chooses one unused item for each next position, recursively explores the remainder, and then undoes the choice. There are `n!` outputs for distinct items, so factorial work is inherent. With duplicate input values, add a duplicate-skipping rule if unique permutations are required.

```python
def permutations(nums):
    result = []
    path = []
    used = [False] * len(nums)

    def backtrack():
        if len(path) == len(nums):
            result.append(path.copy())
            return

        for i in range(len(nums)):
            if used[i]:
                continue

            used[i] = True
            path.append(nums[i])

            backtrack()

            path.pop()
            used[i] = False

    backtrack()
    return result
```

---

## 27.3 Combination Sum Style

Combination-sum backtracking builds a candidate combination and recurses on the remaining target. Whether the recursive call reuses the current index or advances to the next index determines whether an item may be chosen multiple times. Prune when the remaining target becomes impossible under the problem's assumptions.

```python
def combination_sum(candidates, target):
    result = []
    path = []

    def backtrack(start, remaining):
        if remaining == 0:
            result.append(path.copy())
            return

        if remaining < 0:
            return

        for i in range(start, len(candidates)):
            value = candidates[i]

            path.append(value)
            backtrack(i, remaining - value)
            path.pop()

    backtrack(0, target)
    return result
```

---

## 27.4 Backtracking Use Cases

Backtracking explores a decision tree by making a choice, recursively exploring what follows, and then undoing that choice before trying the next option. It is appropriate when the task asks for all valid combinations, permutations, placements, paths, or constraint-satisfying configurations. Pruning impossible branches early is often the difference between a practical and an impractical solution.

- Sudoku
- N-Queens
- Word search
- Permutations
- Combinations
- Subsets
- Constraint satisfaction
- Maze/path enumeration

---

# 28. Dynamic Programming

Dynamic programming is useful when many candidate solutions reuse the same subproblems and the answer can be composed from smaller states. The core design work is to define the **state**, derive the **transition**, set correct **base cases**, and choose an evaluation order. Memoization computes states on demand; tabulation computes them in an explicit order.

Dynamic Programming (DP) solves problems with overlapping subproblems and optimal substructure.

Two major styles:

```text
Top-down → recursion + memoization
Bottom-up → iterative tabulation
```

---

## 28.1 How to Recognize DP

DP is a candidate when a brute-force recursion revisits the same state and the final answer can be composed from smaller-state answers. Do not use DP solely because the prompt asks for a minimum/maximum—first identify repeated subproblems and a precise state.

Common clues:

```text
maximum / minimum
number of ways
can we reach?
best possible
choose / skip
subsequence
partition
paths
state depends on previous state
```

DP often appears when brute-force recursion repeats the same states.

---

## 28.2 Fibonacci — Bad Recursive Version

Naive recursive Fibonacci repeats subproblems exponentially; it is a teaching example of why memoization is needed, not a scalable implementation.

```python
def fib(n):
    if n <= 1:
        return n

    return fib(n - 1) + fib(n - 2)
```

Complexity is exponential.

---

## 28.3 Memoization

Memoization caches a function's result by state so repeated calls return immediately. In Python, a dictionary or `functools.cache/lru_cache` can be used when arguments are hashable. Include all state-changing parameters in the cache key.

```python
from functools import lru_cache

@lru_cache(maxsize=None)
def fib(n):
    if n <= 1:
        return n

    return fib(n - 1) + fib(n - 2)
```

Complexity:

```text
Time: O(n)
Space: O(n)
```

---

## 28.4 Tabulation

Tabulation computes DP states iteratively from base cases toward the target. The table shape and iteration order must ensure every referenced dependency is already computed; this often avoids recursion-depth limits.

```python
def fib(n):
    if n <= 1:
        return n

    dp = [0] * (n + 1)
    dp[1] = 1

    for i in range(2, n + 1):
        dp[i] = dp[i - 1] + dp[i - 2]

    return dp[n]
```

---

## 28.5 Space Optimization

Space optimization removes DP states that are no longer needed. If `dp[i]` depends only on a fixed number of earlier rows/values, replace the full table with rolling variables or a small rolling array. Do this only after the full state transition is correct, because update order can accidentally overwrite a dependency.

```python
def fib(n):
    if n <= 1:
        return n

    prev2 = 0
    prev1 = 1

    for _ in range(2, n + 1):
        current = prev1 + prev2
        prev2 = prev1
        prev1 = current

    return prev1
```

Space:

```text
O(1)
```

---

## 28.6 House Robber

House Robber is a take/skip DP. For each house, compare skipping it (keep the previous best) with taking it (add its value to the best solution that excludes the adjacent previous house). Only the previous two DP values are needed, so the common optimized solution is `O(n)` time and `O(1)` extra space.

You cannot take adjacent houses.

```python
def rob(nums):
    prev2 = 0
    prev1 = 0

    for money in nums:
        current = max(
            prev1,
            prev2 + money,
        )

        prev2 = prev1
        prev1 = current

    return prev1
```

State meaning:

```text
best answer up to current position
```

Transition:

```text
max(
    skip current,
    take current + best before previous
)
```

---

## 28.7 0/1 Knapsack

Each item can be chosen at most once.

State:

```text
dp[i][capacity]
```

Possible meaning:

```text
Maximum value using first i items within capacity
```

Transition:

```text
skip item
or
take item if it fits
```

Space-optimized implementation:

```python
def knapsack(weights, values, capacity):
    dp = [0] * (capacity + 1)

    for weight, value in zip(weights, values):
        for c in range(capacity, weight - 1, -1):
            dp[c] = max(
                dp[c],
                dp[c - weight] + value,
            )

    return dp[capacity]
```

Why iterate capacity backwards?

To prevent the same item from being reused multiple times.

---

## 28.8 Coin Change — Minimum Coins

The minimum-coin problem asks for the fewest coins needed to form each amount. A common DP state stores the best answer for amount `x`; each coin proposes `1 + dp[x - coin]` when that smaller amount is reachable. Use a sentinel larger than any possible answer and distinguish 'unreachable' from a valid zero-coin base case.

```python
def coin_change(coins, amount):
    dp = [float("inf")] * (amount + 1)
    dp[0] = 0

    for value in range(1, amount + 1):
        for coin in coins:
            if coin <= value:
                dp[value] = min(
                    dp[value],
                    dp[value - coin] + 1,
                )

    return -1 if dp[amount] == float("inf") else dp[amount]
```

---

## 28.9 Longest Common Subsequence

The Longest Common Subsequence (LCS) asks for the longest sequence that appears in two inputs in the same relative order, without requiring contiguity. A classic DP state `dp[i][j]` describes prefixes of the two sequences: matching symbols extend the answer; otherwise the transition skips one side. The standard table takes `O(mn)` time.

For strings `a` and `b`:

```python
def lcs(a, b):
    rows = len(a) + 1
    cols = len(b) + 1

    dp = [[0] * cols for _ in range(rows)]

    for i in range(1, rows):
        for j in range(1, cols):
            if a[i - 1] == b[j - 1]:
                dp[i][j] = 1 + dp[i - 1][j - 1]
            else:
                dp[i][j] = max(
                    dp[i - 1][j],
                    dp[i][j - 1],
                )

    return dp[-1][-1]
```

---

## 28.10 Longest Increasing Subsequence

The Longest Increasing Subsequence (LIS) keeps elements in original order but not necessarily contiguously. A simple DP is `O(n²)`; a tails/binary-search method maintains the smallest possible tail for each subsequence length and runs in `O(n log n)`. The tails array is not necessarily the actual LIS unless predecessor information is also stored.

Simple DP:

```python
def lis_length(nums):
    if not nums:
        return 0

    dp = [1] * len(nums)

    for i in range(len(nums)):
        for j in range(i):
            if nums[j] < nums[i]:
                dp[i] = max(dp[i], dp[j] + 1)

    return max(dp)
```

Complexity:

```text
O(n²)
```

There is also an `O(n log n)` solution using binary search.

---

## 28.11 Grid DP

Grid DP stores the best/count answer for each cell based on previously solved neighboring cells. The allowed movement determines the transition and valid evaluation order. When movement is only right/down, row-major or column-major tabulation is usually straightforward; if arbitrary cycles are allowed, the problem may be a graph problem rather than simple DP.

Count paths from top-left to bottom-right while moving right/down:

```python
def unique_paths(rows, cols):
    dp = [1] * cols

    for _ in range(1, rows):
        for c in range(1, cols):
            dp[c] += dp[c - 1]

    return dp[-1]
```

---

## 28.12 DP Design Framework

For each DP problem, define:

1. **State** — what does `dp[...]` mean?
2. **Transition** — how do previous states produce this state?
3. **Base case**
4. **Evaluation order**
5. **Answer location**
6. **Possible memory optimization**

Never code DP before clearly defining the state.

---

# 29. Bit Manipulation

Bit manipulation treats an integer as a sequence of binary bits. Operations such as AND (`&`), OR (`|`), XOR (`^`), complement (`~`), and shifts can test or modify individual bits efficiently. Use explicit parentheses around shift expressions when precedence could be unclear, and remember that signed integer width and overflow behavior are language-specific.

Computers represent integers using bits.

Useful operators:

```python
a & b   # AND
a | b   # OR
a ^ b   # XOR
~a      # NOT
a << k  # shift left
a >> k  # shift right
```

---

## 29.1 Check Odd or Even

The least significant binary bit tells parity: it is `1` for odd integers and `0` for even integers. Testing `n & 1` is a constant-time alternative to `n % 2`, although `% 2` is often clearer when bit operations are not otherwise relevant.

```python
if n & 1:
    print("odd")
else:
    print("even")
```

---

## 29.2 Check k-th Bit

To test bit `k`, create a mask `1 << k` and AND it with the number. A non-zero result means that bit is set. State whether bit positions are zero-based and ensure `k` is within the integer width used by the language.

```python
def is_bit_set(n, k):
    return bool(n & (1 << k))
```

---

## 29.3 Set k-th Bit

To set bit `k`, OR the number with the mask `1 << k`. OR leaves all existing `1` bits unchanged and forces the selected bit to `1`. The operation modifies the numeric value but does not affect other bit positions.

```python
n |= 1 << k
```

---

## 29.4 Clear k-th Bit

To clear bit `k`, invert the one-bit mask and AND it with the number. The inverted mask has `0` at bit `k` and `1` elsewhere, so only the selected bit is forced to zero. Signed-width/complement behavior follows the language's integer representation.

```python
n &= ~(1 << k)
```

---

## 29.5 Toggle k-th Bit

To toggle bit `k`, XOR the number with `1 << k`. XOR with `1` flips a bit and XOR with `0` preserves it, so all other bit positions remain unchanged.

```python
n ^= 1 << k
```

---

## 29.6 Single Number Using XOR

When every value except one appears exactly twice, XOR is useful because `x ^ x = 0` and `x ^ 0 = x`. XORing the full array cancels each duplicate pair, leaving the unique value in `O(n)` time and `O(1)` extra space. This exact trick does not directly solve cases where duplicates appear three times.

Every value appears twice except one.

```python
def single_number(nums):
    result = 0

    for value in nums:
        result ^= value

    return result
```

Why?

```text
x ^ x = 0
x ^ 0 = x
```

---

## 29.7 Count Set Bits

Count set bits either by examining each bit or by repeatedly clearing the lowest set bit with `n &= n - 1`. The latter loops once per `1` bit. Python also provides `int.bit_count()` when the goal is production code rather than implementing the technique.

Python:

```python
n.bit_count()
```

Manual Brian Kernighan method:

```python
def count_bits(n):
    count = 0

    while n:
        n &= n - 1
        count += 1

    return count
```

Each iteration removes the lowest set bit.

---

# 30. Monotonic Stack and Monotonic Queue

A monotonic stack keeps its elements in increasing or decreasing order by removing values that can no longer be useful. Each element is pushed and popped at most once, so many nearest-greater/nearest-smaller problems become `O(n)`. The crucial design decision is whether the stack stores values or indexes and which comparison preserves the needed candidate boundary.

These structures preserve increasing or decreasing order.

They are extremely useful when the problem asks about:

```text
next greater
next smaller
previous greater
previous smaller
largest rectangle
daily temperatures
sliding-window max/min
```

---

## 30.1 Next Greater Element

Next-greater-element problems ask for the first later value that exceeds the current value. A decreasing monotonic stack stores unresolved indexes/values; when a larger value arrives, it resolves stack entries until monotonic order is restored. Each item is pushed and popped at most once, so the scan is `O(n)`.

```python
def next_greater(nums):
    result = [-1] * len(nums)
    stack = []

    for i, value in enumerate(nums):
        while stack and nums[stack[-1]] < value:
            index = stack.pop()
            result[index] = value

        stack.append(i)

    return result
```

Each index enters and leaves the stack once.

Complexity:

```text
O(n)
```

---

## 30.2 Sliding Window Maximum

A sliding window tracks a contiguous range while updating only the information that changes when the range expands or shrinks. Fixed-size windows are used when the length is known; variable-size windows adjust a boundary until a validity condition is restored. The usual goal is to replace repeated recomputation of every subarray or substring with a single linear pass.

```python
from collections import deque

def max_sliding_window(nums, k):
    dq = deque()
    result = []

    for right, value in enumerate(nums):
        while dq and dq[0] <= right - k:
            dq.popleft()

        while dq and nums[dq[-1]] <= value:
            dq.pop()

        dq.append(right)

        if right >= k - 1:
            result.append(nums[dq[0]])

    return result
```

Complexity:

```text
O(n)
```

---

# 31. Advanced String Algorithms

Advanced string algorithms avoid repeatedly rechecking the same characters. Techniques such as KMP, Z, rolling hash, tries, suffix structures, and prefix functions are chosen based on whether the task needs exact pattern search, many prefix queries, repeated substring comparison, or indexing of a large text collection.

For normal interview work, hashes, two pointers, and sliding windows cover many string problems. Advanced algorithms become useful for specialized search workloads.

---

## 31.1 KMP — Knuth-Morris-Pratt

Knuth-Morris-Pratt (KMP) searches for a pattern without rechecking characters that are already known to match. It preprocesses the pattern into a prefix/failure table, then uses that table to decide how far the pattern can shift after a mismatch. Preprocessing plus search runs in `O(m + n)` for pattern length `m` and text length `n`.

KMP finds a pattern inside text in:

```text
O(n + m)
```

where:

```text
n = text length
m = pattern length
```

The key idea is an **LPS array**:

```text
Longest Proper Prefix which is also a Suffix
```

```python
def build_lps(pattern):
    lps = [0] * len(pattern)
    length = 0
    i = 1

    while i < len(pattern):
        if pattern[i] == pattern[length]:
            length += 1
            lps[i] = length
            i += 1

        elif length:
            length = lps[length - 1]

        else:
            lps[i] = 0
            i += 1

    return lps


def kmp_search(text, pattern):
    if pattern == "":
        return 0

    lps = build_lps(pattern)

    i = 0
    j = 0

    while i < len(text):
        if text[i] == pattern[j]:
            i += 1
            j += 1

            if j == len(pattern):
                return i - j

        elif j:
            j = lps[j - 1]

        else:
            i += 1

    return -1
```

---

## 31.2 Rabin-Karp

Rabin-Karp compares rolling hash values for the pattern and each same-length text window. Updating the rolling hash can be constant-time per shift, making the average scan efficient and especially useful when searching many patterns or repeated windows. Because different strings can share a hash, a hash match should be verified when correctness cannot tolerate collisions.

Uses rolling hash to search patterns.

Conceptual steps:

```text
1. Hash pattern.
2. Hash first text window.
3. Slide window.
4. Update hash efficiently.
5. Compare actual strings when hashes match.
```

Useful for:

- Multiple pattern matching variants
- Rolling-hash problems
- Duplicate substring ideas

Beware of hash collisions.

---

## 31.3 Z Algorithm

The Z algorithm computes, for each position, the length of the longest substring starting there that matches the prefix of the whole string. By reusing a previously matched interval, it runs in linear time. A common pattern-search trick concatenates `pattern + separator + text` and looks for Z-values equal to the pattern length.

Computes for each position how many characters match the prefix.

Useful for:

- Pattern matching
- Prefix occurrence problems
- String periodicity

---

## 31.4 Manacher's Algorithm

An algorithm is a finite, unambiguous procedure that converts an input into the required output. A useful explanation of an algorithm should state its preconditions, the main invariant or idea that keeps it correct, when it stops, and its time and space complexity.

Finds longest palindromic substring in linear time:

```text
O(n)
```

It is advanced and usually unnecessary unless constraints demand it.

---

# 32. Range Query Data Structures

Range-query structures are useful when an array changes and you still need repeated queries such as sums, minima, maxima, or other associative aggregates. Fenwick trees are compact and excellent for prefix-style operations; segment trees are more general and can support complex queries and lazy range updates.

Prefix sums work well for static sums. If values change, more powerful structures may be needed.

---

## 32.1 Fenwick Tree / Binary Indexed Tree

A Fenwick Tree stores partial prefix aggregates in a compact array indexed by the least-significant set bit. Point updates and prefix-sum queries both take `O(log n)`, and a range sum is the difference of two prefix sums. Most implementations use 1-based internal indexing even when the input array is 0-based.

Supports:

```text
Point update: O(log n)
Prefix sum: O(log n)
Range sum: O(log n)
```

```python
class FenwickTree:
    def __init__(self, n):
        self.n = n
        self.tree = [0] * (n + 1)

    def add(self, index, delta):
        index += 1

        while index <= self.n:
            self.tree[index] += delta
            index += index & -index

    def prefix_sum(self, index):
        result = 0
        index += 1

        while index > 0:
            result += self.tree[index]
            index -= index & -index

        return result

    def range_sum(self, left, right):
        if left == 0:
            return self.prefix_sum(right)

        return (
            self.prefix_sum(right)
            - self.prefix_sum(left - 1)
        )
```

---

## 32.2 Segment Tree

A segment tree can support range queries and updates.

Typical:

```text
Build: O(n)
Query: O(log n)
Point update: O(log n)
```

Example range-sum segment tree:

```python
class SegmentTree:
    def __init__(self, nums):
        n = 1

        while n < len(nums):
            n *= 2

        self.n = n
        self.tree = [0] * (2 * n)

        for i, value in enumerate(nums):
            self.tree[n + i] = value

        for i in range(n - 1, 0, -1):
            self.tree[i] = (
                self.tree[2 * i]
                + self.tree[2 * i + 1]
            )

    def update(self, index, value):
        pos = self.n + index
        self.tree[pos] = value
        pos //= 2

        while pos:
            self.tree[pos] = (
                self.tree[2 * pos]
                + self.tree[2 * pos + 1]
            )
            pos //= 2

    def query(self, left, right):
        # inclusive [left, right]
        left += self.n
        right += self.n

        result = 0

        while left <= right:
            if left % 2 == 1:
                result += self.tree[left]
                left += 1

            if right % 2 == 0:
                result += self.tree[right]
                right -= 1

            left //= 2
            right //= 2

        return result
```

Segment trees can also support:

- Minimum
- Maximum
- GCD
- Frequency
- Lazy range updates

---

## 32.3 Sparse Table

A Sparse Table preprocesses an immutable array for idempotent range queries such as minimum/maximum. It uses `O(n log n)` preprocessing/storage and answers RMQ in `O(1)` using two overlapping power-of-two blocks; updates are not efficient, so use it for static data.

Useful for **static idempotent range queries**, such as range minimum.

Typical:

```text
Build: O(n log n)
Query: O(1) for RMQ
Updates: not efficient
```

---

# 33. Advanced Graph Algorithms

Advanced graph problems are defined less by their story and more by graph properties: edge weights, direction, cycles, connectivity, negative edges, or repeated connectivity changes. Verify those properties first because they determine whether shortest path, MST, SCC, bridge/articulation, flow, or specialized traversal algorithms are valid.

## 33.1 Bellman-Ford

Bellman-Ford finds single-source shortest paths even when some edges are negative. Relax every edge up to `V-1` times because a simple shortest path uses at most `V-1` edges; one additional successful relaxation indicates a reachable negative cycle. Complexity is `O(VE)`.

Can handle negative-weight edges.

It can also detect a reachable negative cycle.

Complexity:

```text
O(VE)
```

```python
def bellman_ford(n, edges, source):
    dist = [float("inf")] * n
    dist[source] = 0

    for _ in range(n - 1):
        changed = False

        for u, v, weight in edges:
            if dist[u] != float("inf") and dist[u] + weight < dist[v]:
                dist[v] = dist[u] + weight
                changed = True

        if not changed:
            break

    for u, v, weight in edges:
        if dist[u] != float("inf") and dist[u] + weight < dist[v]:
            raise ValueError("negative cycle detected")

    return dist
```

---

## 33.2 Floyd-Warshall

Floyd-Warshall computes all-pairs shortest paths by progressively allowing each vertex as an intermediate point. Its core transition is `dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])`. It uses `O(V³)` time and `O(V²)` distance storage and can handle negative edges, but not negative cycles when meaningful finite shortest paths are required.

All-pairs shortest paths.

```python
def floyd_warshall(matrix):
    n = len(matrix)
    dist = [row[:] for row in matrix]

    for k in range(n):
        for i in range(n):
            for j in range(n):
                dist[i][j] = min(
                    dist[i][j],
                    dist[i][k] + dist[k][j],
                )

    return dist
```

Complexity:

```text
Time: O(V³)
Space: O(V²)
```

---

## 33.3 Minimum Spanning Tree

A minimum spanning tree (MST) connects all vertices of a connected, weighted, undirected graph with minimum total edge weight and no cycles. Kruskal's algorithm grows the MST by globally smallest safe edges; Prim's grows outward from the current tree. If the graph is disconnected, the corresponding result is a minimum spanning forest rather than one spanning tree.

A Minimum Spanning Tree connects all vertices of a connected weighted undirected graph with minimum total edge weight and no cycles.

Important algorithms:

```text
Kruskal
Prim
```

---

## 33.4 Kruskal's Algorithm

An algorithm is a finite, unambiguous procedure that converts an input into the required output. A useful explanation of an algorithm should state its preconditions, the main invariant or idea that keeps it correct, when it stops, and its time and space complexity.

1. Sort edges by weight.
2. Add smallest edge that does not create a cycle.
3. Use Union-Find.

```python
def kruskal(n, edges):
    dsu = DSU(n)
    total = 0
    chosen = []

    for weight, u, v in sorted(edges):
        if dsu.union(u, v):
            total += weight
            chosen.append((u, v, weight))

    if len(chosen) != n - 1:
        return None

    return total, chosen
```

Complexity is dominated by edge sorting:

```text
O(E log E)
```

---

## 33.5 Prim's Algorithm

Prim's algorithm builds a minimum spanning tree by repeatedly adding the cheapest edge that connects the current tree to a new vertex. A min-priority queue efficiently selects the next candidate edge. With an adjacency list and binary heap, the common complexity is `O(E log V)`; the graph should be treated as weighted and undirected for the standard MST problem.

Uses a priority queue to grow one connected tree.

Useful when adjacency-list representation is natural.

---

## 33.6 Strongly Connected Components

In a directed graph, an SCC is a maximal group where every node can reach every other node.

Algorithms:

- Kosaraju
- Tarjan

Applications:

- Dependency analysis
- Deadlock/cycle groups
- Condensation DAG
- Program/module relationships

---

# 34. Advanced Tree Concepts

Advanced tree techniques build on traversal, subtree state, ancestor relationships, balancing, and range/order information. Define the tree type and invariant first—binary, search-ordered, rooted, weighted, balanced—because the valid algorithms depend on those properties.

## 34.1 Balanced Trees

A normal BST can become:

```text
1
 \
  2
   \
    3
     \
      4
```

Then operations degrade to:

```text
O(n)
```

Balanced search trees attempt to maintain height around:

```text
O(log n)
```

Examples:

- AVL Tree
- Red-Black Tree

Python does not include a built-in general-purpose balanced BST.

---

## 34.2 AVL Tree

An AVL tree is a self-balancing BST that keeps each node's left/right subtree heights within one. Rotations restore balance after updates, maintaining `O(log n)` height and search/insert/delete. It uses stricter balancing than a Red-Black tree and may perform more rotations on updates.

An AVL tree maintains strict balance:

```text
balance factor = height(left) - height(right)
```

Allowed values are generally:

```text
-1, 0, +1
```

Rotations restore balance.

---

## 34.3 Red-Black Tree

A Red-Black Tree maintains balance through color and structural invariants.

It is less strictly balanced than AVL but provides:

```text
Search: O(log n)
Insert: O(log n)
Delete: O(log n)
```

---

## 34.4 B-Tree and B+ Tree

Designed for storage systems where accessing disk/page blocks is expensive.

Common use:

- Databases
- File systems
- Indexes

B+ trees are especially common for database indexes because internal nodes guide search while leaf nodes store/search ordered entries efficiently.

---

## 34.5 Lowest Common Ancestor

The lowest common ancestor (LCA) is the deepest node whose subtree contains both targets. A recursive binary-tree solution returns a target when found; if left and right recursive results are both non-null, the current node is the LCA. Clarify whether both target nodes are guaranteed to exist.

For a general binary tree:

```python
def lowest_common_ancestor(root, p, q):
    if not root or root is p or root is q:
        return root

    left = lowest_common_ancestor(root.left, p, q)
    right = lowest_common_ancestor(root.right, p, q)

    if left and right:
        return root

    return left or right
```

---

# 35. Algorithm Design Paradigms

An algorithm is a finite, unambiguous procedure that converts an input into the required output. A useful explanation of an algorithm should state its preconditions, the main invariant or idea that keeps it correct, when it stops, and its time and space complexity.

Algorithms are easier to understand when grouped by design style.

---

## 35.1 Brute Force

Try all possibilities.

Advantages:

- Easy to derive
- Useful for validation
- Good starting point

Disadvantages:

- Often too slow

Example:

```text
Two Sum with nested loops → O(n²)
```

---

## 35.2 Divide and Conquer

Divide and conquer splits a problem into smaller independent subproblems, solves them recursively, and combines their results. Merge sort is a classic example: divide the array, sort each half, then merge the sorted halves. It differs from dynamic programming because divide-and-conquer subproblems usually do not overlap heavily.

Steps:

```text
Divide problem
Solve smaller pieces
Combine results
```

Examples:

- Merge sort
- Quick sort
- Binary search
- Closest-pair style algorithms

---

## 35.3 Greedy

A greedy algorithm commits to a locally best-looking choice without revisiting earlier decisions. That can be very efficient, but it is correct only when the problem has a property that makes local choices compatible with a global optimum. A convincing greedy solution should include a justification such as an exchange argument, cut property, or invariant—not merely an intuition that the choice looks best.

Choose the best immediate option.

Examples:

- Interval scheduling
- Kruskal
- Prim
- Huffman coding

---

## 35.4 Dynamic Programming

Dynamic programming is useful when many candidate solutions reuse the same subproblems and the answer can be composed from smaller states. The core design work is to define the **state**, derive the **transition**, set correct **base cases**, and choose an evaluation order. Memoization computes states on demand; tabulation computes them in an explicit order.

Reuse overlapping subproblems.

Examples:

- Knapsack
- LCS
- Coin change
- Grid path
- LIS

---

## 35.5 Backtracking

Backtracking explores a decision tree by making a choice, recursively exploring what follows, and then undoing that choice before trying the next option. It is appropriate when the task asks for all valid combinations, permutations, placements, paths, or constraint-satisfying configurations. Pruning impossible branches early is often the difference between a practical and an impractical solution.

Explore decision tree and undo choices.

Examples:

- N-Queens
- Sudoku
- Permutations

---

## 35.6 Branch and Bound

Explore candidates while using bounds to eliminate branches that cannot beat the current best solution.

Used in optimization problems.

---

## 35.7 Randomized Algorithms

Randomness can improve expected performance or simplify logic.

Examples:

- Randomized quicksort pivot
- Reservoir sampling
- Randomized hashing ideas

---

# 36. Common Problem-Solving Patterns

Problem-solving patterns are reusable ways to remove repeated work. Treat each pattern as a clue-to-invariant mapping: identify the input structure, state what must remain true while the algorithm runs, and only then choose pointer movements, data structures, or transitions.

Learning patterns is one of the fastest ways to improve.

## Pattern 1 — Hash Map for Complement

Hash-based structures trade extra memory for fast average-case membership, lookup, insertion, and deletion. They are especially useful for frequency tables, duplicate detection, complement lookup, caching, and visited-state tracking. Their ordering guarantees and worst-case behavior depend on the language and implementation, so do not assume sorted iteration unless the API explicitly provides it.

Clue:

```text
pair values
target sum
lookup previous value
```

Example:

```text
Two Sum
```

---

## Pattern 2 — Two Pointers

Two pointers maintain two indexes or references whose movement eliminates unnecessary repeated work. Common forms are opposite-end pointers on sorted data and same-direction read/write pointers for in-place filtering. The technique is most valuable when pointer movement can be justified by an invariant, such as sorted order or a maintained valid region.

Clue:

```text
sorted array
pair
palindrome
opposite ends
remove duplicates
```

---

## Pattern 3 — Sliding Window

A sliding window tracks a contiguous range while updating only the information that changes when the range expands or shrinks. Fixed-size windows are used when the length is known; variable-size windows adjust a boundary until a validity condition is restored. The usual goal is to replace repeated recomputation of every subarray or substring with a single linear pass.

Clue:

```text
contiguous
substring
subarray
longest/shortest
at most k
exactly k
```

---

## Pattern 4 — Prefix Sum

A prefix sum precomputes cumulative totals so that later range sums can be answered by subtraction. With the common convention `prefix[i] = sum of elements before i`, the sum of the half-open range `[left, right)` is `prefix[right] - prefix[left]`. Building the prefix array costs `O(n)` time and each range query then costs `O(1)`.

Clue:

```text
many range-sum queries
subarray sum
cumulative values
```

---

## Pattern 5 — Fast/Slow Pointer

Think of **fast/slow pointer** as a recognition pattern rather than a memorized solution. The clues below suggest that the technique may remove repeated work; confirm its preconditions and maintain an invariant that explains why pointer/state updates are safe.

Clue:

```text
linked list cycle
middle node
cycle entrance
```

---

## Pattern 6 — Binary Search

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

Clue:

```text
sorted
monotonic
minimum possible answer
maximum feasible answer
```

---

## Pattern 7 — Monotonic Stack

A monotonic stack keeps its elements in increasing or decreasing order by removing values that can no longer be useful. Each element is pushed and popped at most once, so many nearest-greater/nearest-smaller problems become `O(n)`. The crucial design decision is whether the stack stores values or indexes and which comparison preserves the needed candidate boundary.

Clue:

```text
next greater
next smaller
nearest greater
histogram
temperatures
```

---

## Pattern 8 — Heap / Top-K

A heap is a partially ordered tree structure commonly used to implement a priority queue. A min-heap exposes the smallest item; a max-heap exposes the largest. Insert and removal of the root are typically `O(log n)`, while reading the root is `O(1)`, making heaps ideal for top-k, scheduling, streaming minima/maxima, and graph algorithms such as Dijkstra or Prim.

Clue:

```text
largest k
smallest k
continuously changing minimum/maximum
priority
merge sorted streams
```

---

## Pattern 9 — BFS

Breadth-first search explores a graph or tree level by level using a queue. In an unweighted graph, the first time BFS reaches a vertex is through a path with the minimum number of edges from the start. With adjacency-list representation, a complete traversal is `O(V + E)` when each vertex is processed once.

Clue:

```text
minimum number of steps
unweighted shortest path
level traversal
nearest
```

---

## Pattern 10 — DFS

Depth-first search explores one branch as far as possible before returning to try another branch. It can be implemented recursively or with an explicit stack and is widely used for connected components, cycle detection, tree processing, path exploration, topological reasoning, and many backtracking-style searches. Track visited state in cyclic graphs to avoid endless revisits.

Clue:

```text
components
all paths
tree recursion
exploration
cycle/connectivity
```

---

## Pattern 11 — Union-Find

Union-Find, also called Disjoint Set Union (DSU), maintains a collection of non-overlapping groups under two main operations: `find` identifies a representative and `union` merges groups. Path compression plus union by rank/size makes a long sequence of operations effectively near-constant time in practice. It is useful for dynamic connectivity, cycle detection in undirected graphs, Kruskal's MST, and component grouping.

Clue:

```text
dynamic connectivity
merge groups
number of components
redundant connection
```

---

## Pattern 12 — Backtracking

Backtracking explores a decision tree by making a choice, recursively exploring what follows, and then undoing that choice before trying the next option. It is appropriate when the task asks for all valid combinations, permutations, placements, paths, or constraint-satisfying configurations. Pruning impossible branches early is often the difference between a practical and an impractical solution.

Clue:

```text
generate all
combinations
permutations
valid configurations
constraint search
```

---

## Pattern 13 — Dynamic Programming

Dynamic programming is useful when many candidate solutions reuse the same subproblems and the answer can be composed from smaller states. The core design work is to define the **state**, derive the **transition**, set correct **base cases**, and choose an evaluation order. Memoization computes states on demand; tabulation computes them in an explicit order.

Clue:

```text
optimal answer
number of ways
repeated states
choose/skip
subsequence
```

---

## Pattern 14 — Greedy

A greedy algorithm commits to a locally best-looking choice without revisiting earlier decisions. That can be very efficient, but it is correct only when the problem has a property that makes local choices compatible with a global optimum. A convincing greedy solution should include a justification such as an exchange argument, cut property, or invariant—not merely an intuition that the choice looks best.

Clue:

```text
schedule
interval
local best
minimum resources
maximum number selected
```

---

## Pattern 15 — Topological Sort

A topological ordering places every prerequisite before the items that depend on it. It exists only for a **directed acyclic graph (DAG)**. Common implementations use Kahn's algorithm with indegrees and a queue, or DFS with postorder; if all vertices cannot be ordered, the dependency graph contains a cycle.

Clue:

```text
dependencies
prerequisites
before/after ordering
DAG
```

---

## Pattern 16 — Trie

A trie stores keys by shared prefixes. Each step consumes one symbol, so lookup time depends mainly on key length rather than on the number of stored keys. Tries are useful for autocomplete, prefix counting, dictionary search, and word-grid problems, but they can use substantially more memory than a hash-based set or map.

Clue:

```text
prefix
dictionary
autocomplete
word search
```

---

## Pattern 17 — Matrix Traversal

Traversal means visiting each relevant element/node in a defined order. The important state is the current position and the rule for advancing to the next one. A full traversal is usually `O(n)` for a linear structure, while trees/graphs additionally require a stack/queue or recursion and, for cyclic graphs, visited tracking.

Typical directions:

```python
DIRECTIONS = [
    (1, 0),
    (-1, 0),
    (0, 1),
    (0, -1),
]
```

Boundary check:

```python
0 <= r < rows and 0 <= c < cols
```

Common tasks:

- Number of islands
- Flood fill
- Maze
- Shortest path
- Word search

---

# 37. Python-Specific DSA Optimizations

Python's high-level containers make DSA concise, but operation choice still matters. Use `deque` for efficient queue operations, sets/dicts for membership, `heapq` for priority queues, built-in sorting for production-quality sorting, and avoid accidental copying or quadratic string/list operations inside loops.

## 37.1 Use `deque` for Queue

A queue follows **First In, First Out (FIFO)** order: the earliest enqueued item is processed first. The key operations are enqueue, dequeue, front/peek, and emptiness checking. Queues are a natural fit for breadth-first search, scheduling, buffering, and any workflow that must preserve arrival order.

Bad:

```python
queue.pop(0)
```

Better:

```python
queue.popleft()
```

with `collections.deque`.

---

## 37.2 Use Sets for Membership

Membership in a Python set is expected `O(1)`, compared with `O(n)` scanning a list. Convert to a set when you perform many membership checks and do not need duplicate counts or positional order; the conversion itself costs `O(n)` and extra memory.

Bad for repeated membership checks:

```python
if value in large_list:
```

Often better:

```python
lookup = set(large_list)

if value in lookup:
```

Trade-off:

```text
Extra memory for faster average membership
```

---

## 37.3 Avoid Unnecessary Copies

Slicing, `list(...)`, `sorted(...)`, and some transformations allocate new containers. In hot loops or recursion, repeated copies can change both time and space complexity; pass indexes/views or mutate/backtrack carefully when copying is not required for correctness.

This creates a copy:

```python
arr[:]
```

So does:

```python
list(arr)
```

And string/list slicing generally copies data.

---

## 37.4 String Construction

When a loop repeatedly appends text, prefer a builder or a collection of pieces followed by one join/concatenation step. This avoids repeatedly copying an ever-growing immutable string and makes the intended construction process explicit.

Prefer:

```python
pieces = []
pieces.append("A")
pieces.append("B")

result = "".join(pieces)
```

---

## 37.5 Use Built-ins

Built-ins are usually implemented efficiently.

Prefer:

```python
sum(nums)
min(nums)
max(nums)
sorted(nums)
```

when the purpose is not to demonstrate the underlying algorithm.

---

## 37.6 Use Tuple Keys

Tuples make convenient immutable composite dictionary/set keys, such as `(row, col)` or `(index, remaining)`. Every tuple element must be hashable. They are especially useful for memoization and visited states with multiple dimensions.

Coordinates:

```python
visited = set()

visited.add((row, col))
```

Tuples containing hashable objects can be dictionary/set keys.

---

## 37.7 Memoization

Memoization caches a function's result by state so repeated calls return immediately. In Python, a dictionary or `functools.cache/lru_cache` can be used when arguments are hashable. Include all state-changing parameters in the cache key.

```python
from functools import lru_cache

@lru_cache(maxsize=None)
def solve(state):
    ...
```

Remember:

> All arguments used as cache keys must be hashable.

A list cannot be directly used as an `lru_cache` key; convert to a tuple when appropriate.

---

## 37.8 Heap Tuple Ordering

A heap is a partially ordered tree structure commonly used to implement a priority queue. A min-heap exposes the smallest item; a max-heap exposes the largest. Insert and removal of the root are typically `O(log n)`, while reading the root is `O(1)`, making heaps ideal for top-k, scheduling, streaming minima/maxima, and graph algorithms such as Dijkstra or Prim.

```python
heapq.heappush(heap, (priority, item))
```

Python compares tuple elements from left to right.

If two priorities are equal and `item` objects cannot be compared, include a numeric tie-breaker:

```python
(priority, sequence_number, item)
```

---

## 37.9 Beware of Mutable 2D Initialization

`[[0] * cols] * rows` repeats the same inner-list reference. Updating one row changes corresponding cells in every row. Build independent rows with `[[0] * cols for _ in range(rows)]`.

Wrong:

```python
grid = [[0] * cols] * rows
```

Rows reference the same inner list.

Correct:

```python
grid = [[0] * cols for _ in range(rows)]
```

---

## 37.10 Python Integer Behavior

Python integers have arbitrary precision, so ordinary integer overflow is not a concern like it is in fixed-width integer languages.

However:

- Large integer arithmetic costs more.
- Bit-manipulation assumptions involving fixed-width signed integers may require care.

---

# 38. Testing and Debugging DSA Solutions

Testing DSA code means exercising both algorithmic correctness and boundary behavior. Include empty/minimal inputs, duplicates, already-ordered and reverse-ordered inputs, extreme numeric values, disconnected structures, and cases that force every branch of the algorithm.

Do not test only the happy path.

## 38.1 Essential Edge Cases

Test minimal and boundary inputs that challenge assumptions: empty/singleton collections, duplicates, all-equal values, negative/extreme values, disconnected graphs, one-node trees, and limits that exercise overflow/recursion depth. Add cases specific to the algorithm's invariant.

For arrays:

```text
[]
[1]
[1, 1]
already sorted
reverse sorted
all equal
negative values
duplicates
very large values
```

For strings:

```text
""
"a"
"aaaa"
special characters
case differences
spaces
```

For trees:

```text
empty tree
single node
only-left chain
only-right chain
balanced tree
duplicates if allowed
```

For graphs:

```text
one node
disconnected graph
cycle
self-loop
parallel edges
unreachable target
```

---

## 38.2 Brute-Force Oracle

A powerful testing method:

1. Write a slow but obviously correct solution.
2. Write optimized solution.
3. Generate many small random inputs.
4. Compare results.

Example:

```python
import random

def brute(nums):
    # slow but simple
    ...

def optimized(nums):
    ...

for _ in range(1000):
    nums = [random.randint(-5, 5) for _ in range(8)]

    assert brute(nums) == optimized(nums)
```

This is especially useful for:

- DP
- Greedy
- Sliding window
- Graph problems
- Complex indexing

---

## 38.3 Invariants

An invariant is something that remains true throughout an algorithm.

Examples:

Binary search:

```text
If target exists, it is inside the current search range.
```

Monotonic stack:

```text
Stack remains increasing/decreasing by chosen rule.
```

Sliding window:

```text
Current window always satisfies the maintained condition.
```

Writing the invariant often reveals bugs.

---

# 39. Interview Problem-Solving Framework

An interview framework makes your reasoning visible: clarify inputs and constraints, establish a brute-force baseline, identify repeated work, choose a pattern, justify correctness, analyze complexity, implement clearly, and test edge cases. The explanation is part of the solution, not an extra step after coding.

When given a DSA problem, avoid immediately typing code.

Use this sequence.

## Step 1 — Restate the Problem

This step is part of turning a problem statement into a defensible solution. Do it explicitly before moving on: the result of this step should give you concrete information you can use to choose, verify, or explain the algorithm.

Explain it in your own words.

---

## Step 2 — Clarify Inputs

This step is part of turning a problem statement into a defensible solution. Do it explicitly before moving on: the result of this step should give you concrete information you can use to choose, verify, or explain the algorithm.

Ask or infer:

```text
Can input be empty?
Are duplicates allowed?
Is it sorted?
Can numbers be negative?
How large can n be?
Can I modify the input?
What should happen if no answer exists?
```

---

## Step 3 — Work Through an Example

This step is part of turning a problem statement into a defensible solution. Do it explicitly before moving on: the result of this step should give you concrete information you can use to choose, verify, or explain the algorithm.

Use a small input manually.

---

## Step 4 — Describe Brute Force

This step is part of turning a problem statement into a defensible solution. Do it explicitly before moving on: the result of this step should give you concrete information you can use to choose, verify, or explain the algorithm.

Example:

```text
Try every pair: O(n²)
```

This shows understanding.

---

## Step 5 — Identify the Bottleneck

This step is part of turning a problem statement into a defensible solution. Do it explicitly before moving on: the result of this step should give you concrete information you can use to choose, verify, or explain the algorithm.

Ask:

```text
What repeated work makes brute force slow?
```

---

## Step 6 — Select a Pattern

This step is part of turning a problem statement into a defensible solution. Do it explicitly before moving on: the result of this step should give you concrete information you can use to choose, verify, or explain the algorithm.

Possible structures:

```text
Hash map
Two pointers
Sliding window
Heap
Binary search
BFS/DFS
DP
Greedy
```

---

## Step 7 — State Complexity Before Coding

This step is part of turning a problem statement into a defensible solution. Do it explicitly before moving on: the result of this step should give you concrete information you can use to choose, verify, or explain the algorithm.

Example:

```text
I'll use a hash map to reduce lookup from O(n) to O(1) average,
making the full solution O(n) time and O(n) space.
```

---

## Step 8 — Code Clearly

This step is part of turning a problem statement into a defensible solution. Do it explicitly before moving on: the result of this step should give you concrete information you can use to choose, verify, or explain the algorithm.

Prefer:

```python
left
right
current_sum
visited
distance
```

instead of:

```python
a
b
x
tmp2
```

unless the variable is truly conventional and local.

---

## Step 9 — Test Edge Cases

This step is part of turning a problem statement into a defensible solution. Do it explicitly before moving on: the result of this step should give you concrete information you can use to choose, verify, or explain the algorithm.

Walk through:

```text
small input
empty input
duplicate case
boundary case
```

---

## Step 10 — Reconfirm Complexity

This step is part of turning a problem statement into a defensible solution. Do it explicitly before moving on: the result of this step should give you concrete information you can use to choose, verify, or explain the algorithm.

State final:

```text
Time: ...
Space: ...
```

---

# 40. Competitive Programming Template

A competitive-programming template should contain only stable utilities that reduce input/output and setup overhead. Keep problem-specific algorithms out until needed; oversized templates slow debugging and can hide assumptions about indexing, numeric range, or mutable global state.

A simple Python template:

```python
import sys
from collections import defaultdict, deque, Counter
from heapq import heappush, heappop
from bisect import bisect_left, bisect_right

input = sys.stdin.readline


def solve():
    n = int(input())
    nums = list(map(int, input().split()))

    # solution here


if __name__ == "__main__":
    solve()
```

For multiple test cases:

```python
def solve():
    t = int(input())

    for _ in range(t):
        n = int(input())
        nums = list(map(int, input().split()))

        # process
```

---

## 40.1 Recursion in Competitive Programming

Some deep recursive graph/tree traversals can hit Python's recursion limit.

You may see:

```python
import sys
sys.setrecursionlimit(1_000_000)
```

Use this carefully.

Increasing the recursion limit does not eliminate stack-memory risk.

Iterative traversal is often safer.

---

# 41. Common Mistakes and Anti-Patterns

DSA bugs are often caused by incorrect boundaries, stale state, missing visited checks, wrong base cases, or an invariant that was never made explicit. Debug by reducing the input, tracing state changes line by line, and checking the first point where the program diverges from the expected invariant.

## Mistake 1 — Using `pop(0)` as Queue

A queue follows **First In, First Out (FIFO)** order: the earliest enqueued item is processed first. The key operations are enqueue, dequeue, front/peek, and emptiness checking. Queues are a natural fit for breadth-first search, scheduling, buffering, and any workflow that must preserve arrival order.

```python
queue.pop(0)
```

is O(n).

Use:

```python
deque.popleft()
```

---

## Mistake 2 — Forgetting Visited Set

This mistake is common because the code can look plausible on normal inputs. Use a minimal counterexample, state the violated invariant/assumption, and fix the reasoning before optimizing or memorizing a corrected snippet.

Graph traversal without visited tracking can revisit nodes indefinitely in cyclic graphs.

---

## Mistake 3 — Incorrect Binary Search Boundaries

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

Common bugs:

```text
left < right vs left <= right
mid update
right = mid vs right = mid - 1
```

Choose a binary-search template and understand its invariant.

---

## Mistake 4 — Returning Too Early in Recursion

Recursion solves a problem by calling the same routine on a smaller or simpler state. Every recursive solution needs a **base case** that stops further calls and a **progress rule** that moves toward that base case. Also account for call-stack space: even an algorithm with little explicit memory usage may use `O(depth)` stack space.

Incorrect placement of `return` can prevent exploration of alternative branches.

---

## Mistake 5 — Shared 2D Lists

Creating a 2D list by multiplying one inner list shares references between rows. Mutating one row then mutates every alias. Use a comprehension that constructs a fresh inner list for each row.

Wrong:

```python
matrix = [[0] * 3] * 3
```

Correct:

```python
matrix = [[0] * 3 for _ in range(3)]
```

---

## Mistake 6 — Modifying Collection While Iterating

This can skip data or cause logical errors.

Prefer iterating over a copy or constructing a new result.

---

## Mistake 7 — Missing Copy in Backtracking

Backtracking explores a decision tree by making a choice, recursively exploring what follows, and then undoing that choice before trying the next option. It is appropriate when the task asks for all valid combinations, permutations, placements, paths, or constraint-satisfying configurations. Pruning impossible branches early is often the difference between a practical and an impractical solution.

Wrong:

```python
result.append(path)
```

when `path` continues changing.

Correct:

```python
result.append(path.copy())
```

---

## Mistake 8 — Using Dijkstra with Negative Edges

Dijkstra relies on non-negative edge weights; a later negative edge can invalidate a distance that was treated as final. Use Bellman-Ford for general negative edges (and cycle detection), or exploit DAG order when the graph is acyclic.

Dijkstra assumes non-negative weights.

Use another algorithm such as Bellman-Ford when negative edges matter.

---

## Mistake 9 — Calling a Greedy Choice "Obviously Optimal"

A greedy algorithm commits to a locally best-looking choice without revisiting earlier decisions. That can be very efficient, but it is correct only when the problem has a property that makes local choices compatible with a global optimum. A convincing greedy solution should include a justification such as an exchange argument, cut property, or invariant—not merely an intuition that the choice looks best.

A greedy algorithm needs justification.

---

## Mistake 10 — Optimizing Before Understanding

This mistake is common because the code can look plausible on normal inputs. Use a minimal counterexample, state the violated invariant/assumption, and fix the reasoning before optimizing or memorizing a corrected snippet.

First derive correctness. Then optimize bottlenecks.

---

# 42. DSA Roadmap

A learning roadmap should progress from basic containers and complexity to reusable patterns, trees/graphs, and advanced techniques. Advance when you can derive and explain a solution without copying, not merely when you have completed a fixed number of exercises.

A structured progression:

## Phase 1 — Foundations

This phase groups skills that reinforce one another. Do not judge progress only by the number of topics completed; the target is being able to recognize the pattern, implement it without copying, analyze complexity, and explain edge cases.

Learn:

- Python basics
- Big-O
- Arrays
- Strings
- Hash maps
- Sets

Target:

```text
Understand complexity and basic iteration.
```

---

## Phase 2 — Linear Data Structures

This phase groups skills that reinforce one another. Do not judge progress only by the number of topics completed; the target is being able to recognize the pattern, implement it without copying, analyze complexity, and explain edge cases.

Learn:

- Linked lists
- Stack
- Queue
- Deque

Target:

```text
Recognize LIFO/FIFO and pointer-based problems.
```

---

## Phase 3 — Core Patterns

This phase groups skills that reinforce one another. Do not judge progress only by the number of topics completed; the target is being able to recognize the pattern, implement it without copying, analyze complexity, and explain edge cases.

Learn:

- Two pointers
- Sliding window
- Prefix sum
- Binary search
- Intervals

Target:

```text
Solve medium array/string problems efficiently.
```

---

## Phase 4 — Recursion and Trees

Recursion solves a problem by calling the same routine on a smaller or simpler state. Every recursive solution needs a **base case** that stops further calls and a **progress rule** that moves toward that base case. Also account for call-stack space: even an algorithm with little explicit memory usage may use `O(depth)` stack space.

Learn:

- Recursion
- Binary trees
- DFS
- BFS
- BST

Target:

```text
Become comfortable with recursive state.
```

---

## Phase 5 — Heaps and Graphs

A graph models entities as vertices and relationships as edges. Before choosing an algorithm, determine whether the graph is directed or undirected, weighted or unweighted, cyclic or acyclic, and connected or disconnected. Those properties decide whether BFS, DFS, topological sorting, shortest-path algorithms, minimum-spanning-tree algorithms, or connectivity structures are appropriate.

Learn:

- Heap
- Graph representation
- BFS/DFS
- Topological sort
- Dijkstra
- DSU

Target:

```text
Solve dependency, shortest-path, and connectivity problems.
```

---

## Phase 6 — Backtracking and Greedy

Backtracking explores a decision tree by making a choice, recursively exploring what follows, and then undoing that choice before trying the next option. It is appropriate when the task asks for all valid combinations, permutations, placements, paths, or constraint-satisfying configurations. Pruning impossible branches early is often the difference between a practical and an impractical solution.

Learn:

- Subsets
- Permutations
- Combinations
- Constraint solving
- Greedy reasoning

---

## Phase 7 — Dynamic Programming

Dynamic programming is useful when many candidate solutions reuse the same subproblems and the answer can be composed from smaller states. The core design work is to define the **state**, derive the **transition**, set correct **base cases**, and choose an evaluation order. Memoization computes states on demand; tabulation computes them in an explicit order.

Progress in this order:

```text
1D DP
Grid DP
Knapsack
Subsequence DP
String DP
Interval/state DP
Tree DP
Bitmask DP
```

---

## Phase 8 — Advanced

These items combine or extend core patterns. Add them only after the prerequisite structure is comfortable; for each one, learn the invariant and complexity rather than memorizing a finished template.

Learn as needed:

- Monotonic stack/queue
- Trie
- KMP
- Fenwick tree
- Segment tree
- MST
- Bellman-Ford
- SCC
- Advanced DP
- Bitmasking

---

# 43. Practice Problem Checklist

Treat this section as an evidence-based self-check. Mark an item complete only when you can explain it in simple language, implement or apply it without copying, analyze its trade-offs, and recognize cases where it should not be used.

Use this as a study tracker.

## Arrays

An array-like structure stores elements in an indexed sequence. Its main advantage is direct access by position; the main trade-off is that inserting or deleting near the front or middle usually requires shifting elements. In DSA problems, arrays are also the base structure behind two pointers, sliding windows, prefix sums, binary search, heaps, and many dynamic-programming tables.

- [ ] Find maximum/minimum
- [ ] Reverse array
- [ ] Rotate array
- [ ] Move zeroes
- [ ] Remove duplicates
- [ ] Majority element
- [ ] Maximum subarray
- [ ] Product except self
- [ ] Merge sorted arrays
- [ ] Missing number

## Strings

A string is a sequence of characters, but its exact behavior depends on the language's string model and character encoding. DSA string problems commonly need indexing/traversal, frequency counting, substring handling, comparison, prefix/suffix reasoning, or pattern matching. Always check whether the task assumes simple ASCII-like characters or full Unicode text.

- [ ] Palindrome
- [ ] Valid anagram
- [ ] Character frequency
- [ ] Longest common prefix
- [ ] Longest unique substring
- [ ] Group anagrams
- [ ] String compression
- [ ] Minimum window substring

## Hashing

- [ ] Two Sum
- [ ] Duplicate detection
- [ ] Frequency map
- [ ] First unique element
- [ ] Longest consecutive sequence
- [ ] Subarray sum equals k

## Linked Lists

A linked list stores values in nodes connected by references rather than by contiguous indexed positions. This makes pointer rewiring cheap once the relevant node is known, but random access is slow because traversal normally starts from the head. Linked-list problems therefore focus heavily on pointer movement, insertion/removal, reversal, cycle detection, and fast/slow-pointer techniques.

- [ ] Reverse linked list
- [ ] Find middle
- [ ] Detect cycle
- [ ] Find cycle start
- [ ] Merge sorted lists
- [ ] Remove nth from end
- [ ] Add two numbers
- [ ] Copy random-pointer list

## Stack / Queue

A stack follows **Last In, First Out (LIFO)** order: the most recently pushed item is the first one removed. The core operations are push, pop, peek/top, and an emptiness check. Stacks are useful when later work depends on the most recent unfinished item, such as expression evaluation, undo, DFS, bracket matching, monotonic-stack problems, and simulated recursion.

- [ ] Valid parentheses
- [ ] Min stack
- [ ] Evaluate RPN
- [ ] Implement queue with stacks
- [ ] Implement stack with queues
- [ ] Daily temperatures
- [ ] Largest rectangle
- [ ] Sliding-window maximum

## Binary Search

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

- [ ] Standard search
- [ ] First occurrence
- [ ] Last occurrence
- [ ] Search insert position
- [ ] Rotated sorted array
- [ ] Find minimum rotated
- [ ] Peak element
- [ ] Binary search on answer

## Trees

- [ ] Preorder
- [ ] Inorder
- [ ] Postorder
- [ ] Level order
- [ ] Maximum depth
- [ ] Same tree
- [ ] Invert tree
- [ ] Diameter
- [ ] Balanced tree
- [ ] Lowest common ancestor
- [ ] Validate BST
- [ ] Kth smallest BST
- [ ] Serialize/deserialize tree

## Heaps

- [ ] Kth largest
- [ ] Top K frequent
- [ ] Merge K sorted lists
- [ ] Find median from data stream
- [ ] Task scheduling

## Graphs

A graph models entities as vertices and relationships as edges. Before choosing an algorithm, determine whether the graph is directed or undirected, weighted or unweighted, cyclic or acyclic, and connected or disconnected. Those properties decide whether BFS, DFS, topological sorting, shortest-path algorithms, minimum-spanning-tree algorithms, or connectivity structures are appropriate.

- [ ] BFS
- [ ] DFS
- [ ] Number of islands
- [ ] Clone graph
- [ ] Connected components
- [ ] Course schedule
- [ ] Topological sort
- [ ] Shortest unweighted path
- [ ] Dijkstra
- [ ] Network delay
- [ ] DSU connectivity
- [ ] Minimum spanning tree

## Backtracking

Backtracking explores a decision tree by making a choice, recursively exploring what follows, and then undoing that choice before trying the next option. It is appropriate when the task asks for all valid combinations, permutations, placements, paths, or constraint-satisfying configurations. Pruning impossible branches early is often the difference between a practical and an impractical solution.

- [ ] Subsets
- [ ] Permutations
- [ ] Combination sum
- [ ] Generate parentheses
- [ ] Word search
- [ ] N-Queens
- [ ] Sudoku solver

## Dynamic Programming

- [ ] Fibonacci
- [ ] Climbing stairs
- [ ] House robber
- [ ] Coin change
- [ ] 0/1 knapsack
- [ ] Partition equal subset sum
- [ ] Unique paths
- [ ] Minimum path sum
- [ ] Longest increasing subsequence
- [ ] Longest common subsequence
- [ ] Edit distance
- [ ] Decode ways
- [ ] Word break

## Advanced

These items combine or extend core patterns. Add them only after the prerequisite structure is comfortable; for each one, learn the invariant and complexity rather than memorizing a finished template.

- [ ] Trie
- [ ] KMP
- [ ] Fenwick tree
- [ ] Segment tree
- [ ] Kruskal
- [ ] Prim
- [ ] Bellman-Ford
- [ ] SCC
- [ ] Bitmask DP

---

# 44. Cheat Sheets

Cheat sheets are for rapid recall, not first-time learning. Use each item as a prompt to reconstruct the invariant, preconditions, operation costs, and common edge cases; if you cannot explain those details, revisit the full concept before relying on the shortcut.

## 44.1 Complexity Cheat Sheet

Use this cheat sheet to estimate whether an approach is plausible for the input size. The entries describe common growth rates, not guarantees for every implementation; always include the cost of nested operations and Python container methods used inside loops.

### Python List

Python list indexing and append are `O(1)` amortized; inserting/removing near the front or middle is `O(n)` because elements shift. Membership search is also `O(n)` unless a separate set/dict index is maintained.

```text
Index                O(1)
Append               O(1) amortized
Pop end              O(1)
Insert/delete front  O(n)
Search               O(n)
Sort                 O(n log n)
```

### Dictionary / Set

Python dictionary/set lookup, insertion, and deletion are `O(1)` average/expected under normal hashing assumptions. They use extra memory and require hashable keys/elements; iteration order guarantees differ between `dict` and `set`.

```text
Lookup   O(1) average
Insert   O(1) average
Delete   O(1) average
```

### Heap

A heap is a partially ordered tree structure commonly used to implement a priority queue. A min-heap exposes the smallest item; a max-heap exposes the largest. Insert and removal of the root are typically `O(log n)`, while reading the root is `O(1)`, making heaps ideal for top-k, scheduling, streaming minima/maxima, and graph algorithms such as Dijkstra or Prim.

```text
Peek min   O(1)
Push       O(log n)
Pop        O(log n)
Heapify    O(n)
```

### BST

BST operation cost is `O(h)` for tree height `h`. Balanced height gives `O(log n)`, while a skewed tree can make search/insert/delete `O(n)`. Inorder traversal remains `O(n)` and yields sorted keys.

Balanced:

```text
Search  O(log n)
Insert  O(log n)
Delete  O(log n)
```

Worst skewed:

```text
O(n)
```

### Graph

With adjacency lists, BFS and DFS visit each vertex and edge a constant number of times: `O(V + E)`. Additional memory includes visited state and the traversal queue/stack.

```text
BFS  O(V + E)
DFS  O(V + E)
```

---

## 44.2 Pattern Selection Cheat Sheet

These clues are **recognition prompts**, not automatic answers. For example, a contiguous-range problem suggests sliding window only when the window can be adjusted while preserving the needed invariant; negative values can invalidate some common sum-window strategies. Confirm the preconditions before applying a pattern.

If the question says...

```text
"pair in sorted array"
→ Two pointers

"substring/subarray, longest/shortest"
→ Sliding window

"many range sum queries"
→ Prefix sum

"minimum steps in unweighted graph"
→ BFS

"all possibilities"
→ Backtracking

"dependencies/order"
→ Topological sort

"shortest weighted path, non-negative"
→ Dijkstra

"connectivity after merging"
→ Union-Find

"top k"
→ Heap

"next greater/smaller"
→ Monotonic stack

"prefix search"
→ Trie

"number of ways / min / max with repeated states"
→ Dynamic programming

"minimum feasible / maximum feasible"
→ Binary search on answer
```

---

## 44.3 Useful Python Snippets

These snippets are small building blocks commonly used in Python DSA solutions. Before copying one, understand whether it mutates data, allocates a new container, or relies on average-case hash behavior, because those details affect correctness and complexity.

### Frequency

A frequency table records how many times each value occurs. Python's `Counter` constructs this mapping directly from an iterable and is useful when counts—not just membership—are needed.

```python
from collections import Counter

freq = Counter(nums)
```

### Group Values

Grouping maps a key/category to a collection of matching values. `defaultdict(list)` is convenient because each unseen key automatically receives an empty list before appending.

```python
from collections import defaultdict

groups = defaultdict(list)

for key, value in records:
    groups[key].append(value)
```

### Queue

A queue follows **First In, First Out (FIFO)** order: the earliest enqueued item is processed first. The key operations are enqueue, dequeue, front/peek, and emptiness checking. Queues are a natural fit for breadth-first search, scheduling, buffering, and any workflow that must preserve arrival order.

```python
from collections import deque

q = deque([start])

while q:
    node = q.popleft()
```

### Min Heap

A heap is a partially ordered tree structure commonly used to implement a priority queue. A min-heap exposes the smallest item; a max-heap exposes the largest. Insert and removal of the root are typically `O(log n)`, while reading the root is `O(1)`, making heaps ideal for top-k, scheduling, streaming minima/maxima, and graph algorithms such as Dijkstra or Prim.

```python
import heapq

heap = []
heapq.heappush(heap, value)
value = heapq.heappop(heap)
```

### Binary Search

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

```python
left = 0
right = len(nums) - 1

while left <= right:
    mid = (left + right) // 2
```

### Four-Direction Grid

Represent four-neighbor movement with `(dr, dc)` offsets. For each cell, compute `nr = r + dr`, `nc = c + dc`, check bounds first, then apply visited/value conditions before enqueuing or recursing.

```python
for dr, dc in ((1, 0), (-1, 0), (0, 1), (0, -1)):
    nr = r + dr
    nc = c + dc
```

---

# 45. Mini Projects Using DSA

Mini projects connect abstract structures to persistent state and user-visible behavior. For each project, identify the dominant operations first, choose the data structure based on those operations, and document what would become slower or harder if a different structure were used.

Learning becomes stronger when DSA is used outside textbook problems.

## Project 1 — Autocomplete Engine

This project turns the data structures or patterns listed below into a small system with observable behavior. Build the simplest working version first, then add tests and measure whether the chosen structure actually improves the target operation.

Use:

```text
Trie
Priority ranking
Hash map
```

Features:

- Insert words
- Prefix search
- Top suggestions
- Usage frequency

---

## Project 2 — Route Finder

This project turns the data structures or patterns listed below into a small system with observable behavior. Build the simplest working version first, then add tests and measure whether the chosen structure actually improves the target operation.

Use:

```text
Graph
Dijkstra
BFS
Heap
```

Model:

```text
City/intersection → node
Road → edge
Distance/time → weight
```

---

## Project 3 — LRU Cache

This project turns the data structures or patterns listed below into a small system with observable behavior. Build the simplest working version first, then add tests and measure whether the chosen structure actually improves the target operation.

Use:

```text
Hash map
Doubly linked list
```

Goal:

```text
get(): O(1)
put(): O(1)
```

Conceptual structure:

```text
Dictionary:
key → linked-list node

Doubly linked list:
least recent ← ... → most recent
```

---

## Project 4 — Task Scheduler

A scheduler often needs efficient priority selection plus state for queued/completed work. A priority queue handles the next highest/lowest-priority task, while maps can support task lookup/cancellation. Define tie-breaking and deadline semantics so scheduling is deterministic.

Use:

```text
Priority queue
Queue
Hash map
```

Features:

- Priority
- Deadline
- Waiting jobs
- Completed jobs

---

## Project 5 — Dependency Resolver

This project turns the data structures or patterns listed below into a small system with observable behavior. Build the simplest working version first, then add tests and measure whether the chosen structure actually improves the target operation.

Use:

```text
Directed graph
Topological sort
Cycle detection
```

Example:

```text
Package A depends on B
B depends on C

Install order:
C → B → A
```

---

## Project 6 — Social Network Analyzer

A social network is naturally a graph where people are vertices and relationships are edges. BFS/DFS support reachability and degrees of separation, while sets/maps support neighbor membership; large-scale recommendations often require more specialized ranking/indexing beyond basic traversal.

Use:

```text
Graph
BFS
DFS
Union-Find
```

Features:

- Friend suggestions
- Connected communities
- Degrees of separation
- Reachability

---

## Project 7 — Search Suggestion Service

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

Use:

```text
Trie
Heap
Frequency map
```

Return top suggestions for a prefix.

---

## Project 8 — Mini Spreadsheet Formula Dependency Engine

This project turns the data structures or patterns listed below into a small system with observable behavior. Build the simplest working version first, then add tests and measure whether the chosen structure actually improves the target operation.

Use:

```text
Graph
Topological sort
Cycle detection
```

If:

```text
C1 = A1 + B1
D1 = C1 * 2
```

dependency graph determines calculation order.

---

# 46. Final Revision Strategy

A strong DSA learner should be able to answer four questions for every important topic:

```text
1. What problem does this solve?
2. How does it work?
3. What is its time/space complexity?
4. When should I choose it instead of another technique?
```

A recommended weekly revision cycle:

```text
Day 1: Arrays + hashing
Day 2: Two pointers + sliding window
Day 3: Stack + queue + linked list
Day 4: Binary search + intervals + heap
Day 5: Trees + graphs
Day 6: Greedy + backtracking + DP
Day 7: Mixed timed practice + revision
```

---

# Appendix A — Full DSA Decision Guide

Use this section to practice translating problem wording into required operations and constraints. The mapping is a starting hypothesis: confirm the technique's preconditions and explain the invariant before committing to it.

When reading a new problem, ask these questions in order.

## A. Is the input tiny?

Answer this question from the concrete design/problem pressure first. The suggested pattern is a candidate, not an automatic choice; compare it with the simplest alternative and check whether the expected variation is real.

If yes, brute force/backtracking may be acceptable.

---

## B. Does order matter?

Answer this question from the concrete design/problem pressure first. The suggested pattern is a candidate, not an automatic choice; compare it with the simplest alternative and check whether the expected variation is real.

If no, consider:

```text
set
dictionary
Counter
sorting
```

---

## C. Is the data sorted?

Answer this question from the concrete design/problem pressure first. The suggested pattern is a candidate, not an automatic choice; compare it with the simplest alternative and check whether the expected variation is real.

Consider:

```text
binary search
two pointers
bisect
```

---

## D. Is the answer based on contiguous elements?

Answer this question from the concrete design/problem pressure first. The suggested pattern is a candidate, not an automatic choice; compare it with the simplest alternative and check whether the expected variation is real.

Consider:

```text
sliding window
prefix sum
Kadane
monotonic deque
```

---

## E. Do we repeatedly need minimum/maximum?

Answer this question from the concrete design/problem pressure first. The suggested pattern is a candidate, not an automatic choice; compare it with the simplest alternative and check whether the expected variation is real.

Consider:

```text
heap
monotonic stack
monotonic queue
```

---

## F. Is there hierarchy?

Answer this question from the concrete design/problem pressure first. The suggested pattern is a candidate, not an automatic choice; compare it with the simplest alternative and check whether the expected variation is real.

Consider:

```text
tree
DFS
BFS
```

---

## G. Are there relationships or routes?

Answer this question from the concrete design/problem pressure first. The suggested pattern is a candidate, not an automatic choice; compare it with the simplest alternative and check whether the expected variation is real.

Consider:

```text
graph
BFS
DFS
Dijkstra
Union-Find
```

---

## H. Are there prerequisites?

Answer this question from the concrete design/problem pressure first. The suggested pattern is a candidate, not an automatic choice; compare it with the simplest alternative and check whether the expected variation is real.

Consider:

```text
topological sort
```

---

## I. Must we generate every valid possibility?

Answer this question from the concrete design/problem pressure first. The suggested pattern is a candidate, not an automatic choice; compare it with the simplest alternative and check whether the expected variation is real.

Consider:

```text
backtracking
```

---

## J. Does brute-force recursion repeat states?

Recursion solves a problem by calling the same routine on a smaller or simpler state. Every recursive solution needs a **base case** that stops further calls and a **progress rule** that moves toward that base case. Also account for call-stack space: even an algorithm with little explicit memory usage may use `O(depth)` stack space.

Consider:

```text
memoization
dynamic programming
```

---

## K. Is feasibility monotonic?

Answer this question from the concrete design/problem pressure first. The suggested pattern is a candidate, not an automatic choice; compare it with the simplest alternative and check whether the expected variation is real.

Consider:

```text
binary search on answer
```

---

# Appendix B — Deeper Scenario Examples

Use this section to practice translating problem wording into required operations and constraints. The mapping is a starting hypothesis: confirm the technique's preconditions and explain the invariant before committing to it.

## Scenario 1 — Fraud Detection Duplicate Transaction IDs

This scenario is a recognition exercise. Translate the story into required operations—lookup, ordering, range processing, connectivity, priority, or dependency handling—then justify why the suggested structure makes those operations efficient.

You receive millions of transaction IDs and need to detect duplicates.

Naive approach:

```text
Compare each transaction with every other transaction
O(n²)
```

Better:

```python
def has_duplicate(ids):
    seen = set()

    for transaction_id in ids:
        if transaction_id in seen:
            return True

        seen.add(transaction_id)

    return False
```

Average:

```text
O(n) time
O(n) space
```

Data structure:

```text
Hash set
```

---

## Scenario 2 — Browser History

This scenario is a recognition exercise. Translate the story into required operations—lookup, ordering, range processing, connectivity, priority, or dependency handling—then justify why the suggested structure makes those operations efficient.

Requirements:

```text
Visit page
Go back
Go forward
```

Possible design:

```text
Two stacks
```

or:

```text
Doubly linked list with current pointer
```

This demonstrates that the same product behavior can be modeled with different structures.

---

## Scenario 3 — Customer Support Ticket Priority

This scenario is a recognition exercise. Translate the story into required operations—lookup, ordering, range processing, connectivity, priority, or dependency handling—then justify why the suggested structure makes those operations efficient.

Requirement:

```text
Process highest-priority ticket first.
```

Use:

```text
Priority queue / heap
```

If priorities change dynamically, more advanced queue/indexing design may be needed.

---

## Scenario 4 — Employee Reporting Hierarchy

This scenario is a recognition exercise. Translate the story into required operations—lookup, ordering, range processing, connectivity, priority, or dependency handling—then justify why the suggested structure makes those operations efficient.

Requirement:

```text
CEO
 ├─ Director A
 │   ├─ Manager
 │   └─ Manager
 └─ Director B
```

Use:

```text
Tree
```

Operations:

- Find descendants → DFS/BFS
- Find reporting depth → tree depth
- Aggregate team metrics → postorder traversal

---

## Scenario 5 — Flight Route Network

This scenario is a recognition exercise. Translate the story into required operations—lookup, ordering, range processing, connectivity, priority, or dependency handling—then justify why the suggested structure makes those operations efficient.

Airports:

```text
Vertices
```

Flights:

```text
Edges
```

If all flights count equally:

```text
BFS can find minimum number of hops.
```

If flight costs differ:

```text
Dijkstra can find cheapest route when weights are non-negative.
```

---

## Scenario 6 — Build Pipeline Dependencies

This scenario is a recognition exercise. Translate the story into required operations—lookup, ordering, range processing, connectivity, priority, or dependency handling—then justify why the suggested structure makes those operations efficient.

Example:

```text
Compile backend
    ↓
Run backend tests
    ↓
Build package
    ↓
Deploy
```

Use:

```text
Directed Acyclic Graph
Topological sorting
```

A cycle means an impossible dependency chain.

---

## Scenario 7 — Product Search Autocomplete

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

Search prefix:

```text
"lap"
```

Suggestions:

```text
laptop
laptop stand
laptop bag
```

Use:

```text
Trie
```

Add frequency ranking with:

```text
Hash map + heap
```

---

## Scenario 8 — Stock Price Next Greater Value

This scenario is a recognition exercise. Translate the story into required operations—lookup, ordering, range processing, connectivity, priority, or dependency handling—then justify why the suggested structure makes those operations efficient.

Question:

```text
For each day's price, when is the next day with a higher price?
```

Use:

```text
Monotonic stack
```

Instead of comparing each day against all later days.

---

## Scenario 9 — Server Log Requests in Last 5 Minutes

This scenario is a recognition exercise. Translate the story into required operations—lookup, ordering, range processing, connectivity, priority, or dependency handling—then justify why the suggested structure makes those operations efficient.

Need to continuously maintain recent requests.

Use:

```text
Queue/deque
```

As current time advances:

```text
append new request
remove requests older than 5 minutes from left
```

---

## Scenario 10 — Cheapest Network Cable Layout

Computers are nodes and possible cables are weighted edges.

Need all computers connected with minimum total cable cost.

Use:

```text
Minimum Spanning Tree
Kruskal or Prim
```

---

# Appendix C — Complexity Reasoning Examples

These examples practice deriving complexity from code structure rather than guessing from the topic name. Count how many times each statement can execute, include recursive depth and auxiliary structures, and simplify only after forming the correct expression.

## Example 1

This loop visits each integer from `0` through `n - 1` exactly once. Because the body performs constant work per iteration, the running time grows linearly: `O(n)`. The loop itself uses `O(1)` auxiliary space.

```python
for i in range(n):
    print(i)
```

Complexity:

```text
O(n)
```

---

## Example 2

This example demonstrates nested work. To derive the complexity, count how many times the inner operation executes across all iterations rather than only counting the number of loop statements.

```python
for i in range(n):
    for j in range(n):
        print(i, j)
```

Complexity:

```text
O(n²)
```

---

## Example 3

Here `i` doubles after every iteration. After `k` iterations, `i` is approximately `2^k`; reaching `n` therefore requires `k ≈ log₂ n` iterations. The loop runs in `O(log n)` time and uses `O(1)` auxiliary space.

```python
i = 1

while i < n:
    i *= 2
```

Values:

```text
1
2
4
8
16
...
```

Number of iterations:

```text
log₂(n)
```

Complexity:

```text
O(log n)
```

---

## Example 4

This example combines loops with different growth rates. Analyze each block separately, then combine sequential costs by addition and keep the dominant term after simplifying.

```python
for i in range(n):
    j = 1

    while j < n:
        j *= 2
```

Outer:

```text
n
```

Inner:

```text
log n
```

Total:

```text
O(n log n)
```

---

## Example 5 — Consecutive Loops

Consecutive loops do not multiply their complexities unless one is nested inside the other. If one loop costs `O(n)` and the next also costs `O(n)`, the total is `O(n + n) = O(n)` after dropping constant factors.

```python
for i in range(n):
    ...

for j in range(n):
    ...
```

Total:

```text
O(n + n)
= O(2n)
= O(n)
```

Big-O ignores constant factors.

---

# Appendix D — When Not to Use a Data Structure

Good DSA is also about avoiding unnecessary complexity.

Do not use:

```text
Trie
```

if a small `set` solves the problem.

Do not use:

```text
Segment tree
```

if one prefix-sum pass solves all queries.

Do not use:

```text
Dijkstra
```

if every edge has equal weight and BFS is sufficient.

Do not use:

```text
Linked list
```

when you need frequent random indexing.

Do not use:

```text
Dynamic programming
```

just because a problem contains "maximum" or "minimum."

Choose the simplest structure that satisfies the complexity requirement.

---

# Appendix E — Recommended Mastery Levels

Treat this section as an evidence-based self-check. Mark an item complete only when you can explain it in simple language, implement or apply it without copying, analyze its trade-offs, and recognize cases where it should not be used.

## Beginner

You should confidently understand:

- Big-O
- Arrays
- Strings
- Dictionaries
- Sets
- Stack
- Queue
- Basic recursion
- Linear search
- Binary search
- Basic sorting

---

## Intermediate

You should confidently solve:

- Two pointers
- Sliding window
- Prefix sums
- Linked lists
- Trees
- Heaps
- BFS/DFS
- Basic graphs
- Backtracking
- Greedy
- Intro DP

---

## Advanced

These items combine or extend core patterns. Add them only after the prerequisite structure is comfortable; for each one, learn the invariant and complexity rather than memorizing a finished template.

You should understand:

- Complex DP
- Monotonic structures
- Tries
- Union-Find
- Dijkstra
- MST
- SCC
- Fenwick tree
- Segment tree
- Advanced string algorithms
- Binary search on answer
- Bitmask techniques

---

# Appendix F — Glossary

**Adjacent**  
Two items directly connected or next to each other.

**Ancestor**  
A node above another node in a tree.

**Backtracking**  
Exploring choices while undoing decisions when returning.

**BFS**  
Breadth-First Search; explores level by level.

**BST**  
Binary Search Tree.

**Connected Component**  
A maximal group of mutually reachable nodes in an undirected graph.

**DFS**  
Depth-First Search; explores deeply before backtracking.

**DAG**  
Directed Acyclic Graph.

**Edge**  
A connection between graph vertices.

**Graph**  
A collection of vertices connected by edges.

**Heap**  
Priority-based tree structure with fast min/max access.

**Memoization**  
Caching results of repeated function states.

**Node**  
Element in a linked structure, tree, or graph.

**Prefix**  
Beginning portion of a sequence.

**Queue**  
FIFO structure.

**Recursion**  
Function solving a problem using smaller calls to itself.

**Stable Sort**  
Equal-key elements preserve their original relative order.

**Stack**  
LIFO structure.

**Subarray**  
Contiguous portion of an array.

**Subsequence**  
Elements kept in order but not necessarily contiguous.

**Substring**  
Contiguous portion of a string.

**Tree**  
Hierarchical acyclic connected structure.

**Trie**  
Prefix-oriented tree for strings.

**Vertex**  
Graph node.

---

# Appendix G — DSA Mindset

The most valuable skill is not memorizing hundreds of solutions.

It is being able to transform:

```text
Problem statement
```

into:

```text
Constraints
    ↓
Required complexity
    ↓
Data structure
    ↓
Algorithmic pattern
    ↓
Invariant/state
    ↓
Correct implementation
    ↓
Edge-case validation
```

When stuck, ask:

```text
Can I sort the input?

Can I trade memory for speed?

Can a hash table eliminate repeated lookup?

Is the data contiguous?

Is the search space monotonic?

Can I model this as a graph?

Does BFS give the minimum number of steps?

Do I repeatedly solve the same state?

Can a heap maintain only the best k values?

Can I process information from left to right?

Can I precompute something?

What is the brute-force solution?

What exact repeated work makes brute force slow?
```

These questions are often more useful than memorizing another problem answer.

---

# Final Summary

Use this summary to check whether the handbook has become a connected mental model rather than a collection of isolated algorithms. You should be able to move from constraints → required operations → data structure/pattern → invariant/state → implementation → complexity → edge-case validation.

A strong Python DSA foundation consists of four layers.

## Layer 1 — Structures

This layer is about choosing how data is organized. For each listed structure, know its core invariant, common operations, typical time/space costs, and at least one problem where its strengths matter.

```text
Array/List
String
Linked List
Stack
Queue/Deque
Hash Map/Set
Tree/BST
Heap
Trie
Graph
Union-Find
Fenwick/Segment Tree
```

## Layer 2 — Core Algorithms

The code below is a concrete example of **Layer 2 — Core Algorithms**. Read it by identifying the input/state first, then trace each mutation or decision until the produced value/output. When reusing the pattern, preserve its required preconditions and include the cost of nested library operations in the complexity analysis.

```text
Searching
Sorting
Tree traversal
BFS
DFS
Shortest path
Minimum spanning tree
Topological sort
String matching
```

## Layer 3 — Problem-Solving Patterns

These patterns are reusable ways to reorganize brute-force work. Mastery means recognizing the clue, stating the invariant/state, explaining why the optimization is valid, and deriving its complexity—not merely memorizing a template.

```text
Two pointers
Sliding window
Prefix sum
Intervals
Binary search on answer
Monotonic stack/queue
Greedy
Backtracking
Dynamic programming
Bit manipulation
```

## Layer 4 — Engineering Skill

```text
Complexity analysis
Choosing trade-offs
Clear Python implementation
Testing
Edge cases
Debugging
Explaining correctness
Recognizing patterns
```

If you can explain **why** each structure and algorithm works, derive its complexity, implement it cleanly, and recognize when it applies, you are no longer merely memorizing DSA—you are developing algorithmic problem-solving skill.

---

# Suggested Next Steps

After completing this handbook:

1. Implement every major structure at least once from scratch.
2. Solve 10–20 focused problems per core pattern.
3. Re-solve important problems without looking at previous code.
4. Keep a mistake journal.
5. Practice explaining solutions verbally.
6. Mix topics so you learn pattern recognition rather than chapter recognition.
7. Build at least two small DSA-based projects.
8. Revise complexity and pattern-selection cheat sheets regularly.
9. Move from correctness → optimization → clarity.
10. Teach the concept to someone else; teaching exposes gaps quickly.

---

**End of DSA with Python — Master Learning Handbook**
