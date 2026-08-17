# Data Structures & Algorithms (DSA) — Master Learning Handbook

> **Purpose:** A single beginner-friendly master reference for learning, revising, interviewing, and applying Data Structures & Algorithms.
>
> **Example language:** Python for readability. The concepts are language-independent and apply to Java, JavaScript, C++, C#, PHP, and other languages.
>
> **Recommended method:** Understand → Visualize → Dry-run → Implement → Analyze → Practice → Revisit.

---

# Table of Contents

1. [How to Use This Handbook](#1-how-to-use-this-handbook)
2. [What Is DSA?](#2-what-is-dsa)
3. [Problem-Solving Mindset](#3-problem-solving-mindset)
4. [Time and Space Complexity](#4-time-and-space-complexity)
5. [Asymptotic Notation](#5-asymptotic-notation)
6. [Math Fundamentals for DSA](#6-math-fundamentals-for-dsa)
7. [Bit Manipulation](#7-bit-manipulation)
8. [Arrays](#8-arrays)
9. [Strings](#9-strings)
10. [Linked Lists](#10-linked-lists)
11. [Stacks](#11-stacks)
12. [Queues and Deques](#12-queues-and-deques)
13. [Hash Maps and Sets](#13-hash-maps-and-sets)
14. [Sorting Algorithms](#14-sorting-algorithms)
15. [Searching and Binary Search](#15-searching-and-binary-search)
16. [Two Pointers](#16-two-pointers)
17. [Sliding Window](#17-sliding-window)
18. [Prefix Sum and Difference Arrays](#18-prefix-sum-and-difference-arrays)
19. [Recursion](#19-recursion)
20. [Backtracking](#20-backtracking)
21. [Trees](#21-trees)
22. [Binary Search Trees](#22-binary-search-trees)
23. [Heaps and Priority Queues](#23-heaps-and-priority-queues)
24. [Tries](#24-tries)
25. [Graphs](#25-graphs)
26. [BFS](#26-bfs)
27. [DFS](#27-dfs)
28. [Topological Sorting](#28-topological-sorting)
29. [Shortest Path Algorithms](#29-shortest-path-algorithms)
30. [Minimum Spanning Tree](#30-minimum-spanning-tree)
31. [Disjoint Set Union](#31-disjoint-set-union)
32. [Strongly Connected Components](#32-strongly-connected-components)
33. [Greedy Algorithms](#33-greedy-algorithms)
34. [Dynamic Programming](#34-dynamic-programming)
35. [Important DP Patterns](#35-important-dp-patterns)
36. [String-Matching Algorithms](#36-string-matching-algorithms)
37. [Monotonic Stack and Queue](#37-monotonic-stack-and-queue)
38. [Intervals and Sweep Line](#38-intervals-and-sweep-line)
39. [Segment Trees](#39-segment-trees)
40. [Fenwick Trees](#40-fenwick-trees)
41. [Quickselect and Selection](#41-quickselect-and-selection)
42. [Core Problem-Solving Patterns](#42-core-problem-solving-patterns)
43. [Real-World Use Cases](#43-real-world-use-cases)
44. [Interview Problem-Solving Framework](#44-interview-problem-solving-framework)
45. [Common Mistakes and Debugging](#45-common-mistakes-and-debugging)
46. [Complexity Cheat Sheet](#46-complexity-cheat-sheet)
47. [DSA Learning Roadmap](#47-dsa-learning-roadmap)
48. [Practice Problem Ladder](#48-practice-problem-ladder)
49. [30-Day Revision Plan](#49-30-day-revision-plan)
50. [Glossary](#50-glossary)
51. [Advanced Topics](#51-advanced-topics)
52. [Final Recognition Cheat Sheet](#52-final-recognition-cheat-sheet)

---

# 1. How to Use This Handbook

Do not try to memorize every algorithm or code snippet. For each topic, learn these six things:

1. **What problem does it solve?**
2. **How does it work?**
3. **What is the time complexity?**
4. **What is the space complexity?**
5. **What clues in a problem suggest it?**
6. **When should it not be used?**

A productive learning loop:

```text
Understand
   ↓
Visualize
   ↓
Dry Run
   ↓
Implement
   ↓
Analyze Complexity
   ↓
Solve Variations
   ↓
Review Mistakes
```

For every solved problem, keep notes like:

```text
Problem:
Pattern:
Brute-force solution:
Optimized solution:
Why it works:
Time complexity:
Space complexity:
Mistake I made:
Recognition clue:
```

The goal is **pattern recognition**, not memorizing hundreds of answers.

---

# 2. What Is DSA?

Data Structures and Algorithms (DSA) is the study of how to organize data and how to process it efficiently and correctly. The practical skill is choosing operations and representations that fit the constraints, then proving correctness and understanding the time/memory trade-off.

## Data Structure

A data structure is the organization chosen for data because that organization makes some operations cheaper than others. When selecting one, ask which operations must be fast—indexing, insertion, deletion, lookup, ordering, minimum/maximum retrieval, or relationship traversal—and what memory trade-off is acceptable.

A data structure defines **how data is stored and organized**.

Examples:

- Array
- Linked List
- Stack
- Queue
- Hash Table
- Tree
- Heap
- Graph
- Trie

## Algorithm

An algorithm is a finite, unambiguous procedure that converts an input into the required output. A useful explanation of an algorithm should state its preconditions, the main invariant or idea that keeps it correct, when it stops, and its time and space complexity.

An algorithm defines **how data is processed to solve a problem**.

Examples:

- Searching
- Sorting
- Traversal
- Shortest path
- Greedy selection
- Dynamic programming
- Backtracking

## Simple real-world example

Imagine an application stores 1,000,000 employee IDs.

If the IDs are stored only in an unsorted list, searching may require:

```text
O(n)
```

If you maintain a hash map by employee ID, average lookup becomes approximately:

```text
O(1)
```

The choice of data structure often decides the efficiency of the application.

---

# 3. Problem-Solving Mindset

Good DSA work starts before coding. Translate the prompt into inputs, outputs, constraints, edge cases, and required complexity; derive a correct baseline; then optimize the repeated work while preserving a clear invariant that explains correctness.

A strong DSA learner does not immediately begin coding.

## Step 1 — Understand the problem

Identify:

- Input
- Output
- Constraints
- Duplicate handling
- Whether ordering matters
- Whether negative values exist
- Whether the input can be modified
- Whether one or many answers are possible

Example:

> Return indices of two values whose sum equals a target.

Clarify:

```text
Can I use one element twice?
Can duplicate numbers exist?
Is one valid answer guaranteed?
Should I return values or indices?
```

## Step 2 — Build a brute-force solution

This step is part of turning a problem statement into a defensible solution. Do it explicitly before moving on: the result of this step should give you concrete information you can use to choose, verify, or explain the algorithm.

```python
def two_sum_bruteforce(nums, target):
    for i in range(len(nums)):
        for j in range(i + 1, len(nums)):
            if nums[i] + nums[j] == target:
                return [i, j]
```

Complexity:

```text
Time:  O(n²)
Space: O(1)
```

Brute force gives a correctness baseline.

## Step 3 — Identify repeated work

This step is part of turning a problem statement into a defensible solution. Do it explicitly before moving on: the result of this step should give you concrete information you can use to choose, verify, or explain the algorithm.

For each number `x`, you need to know whether:

```text
target - x
```

has already appeared.

Use a hash map:

```python
def two_sum(nums, target):
    seen = {}

    for i, value in enumerate(nums):
        required = target - value

        if required in seen:
            return [seen[required], i]

        seen[value] = i
```

Complexity:

```text
Time:  O(n)
Space: O(n)
```

## Step 4 — Ask pattern questions

This step is part of turning a problem statement into a defensible solution. Do it explicitly before moving on: the result of this step should give you concrete information you can use to choose, verify, or explain the algorithm.

```text
Is the input sorted?
Do I need fast membership lookup?
Is the problem about a contiguous range?
Is there a monotonic True/False answer space?
Is this a graph disguised as relationships?
Do subproblems repeat?
Do I repeatedly need smallest/largest values?
Am I generating every possible choice?
```

These questions often reveal the correct approach.

---

# 4. Time and Space Complexity

Complexity analysis estimates how an algorithm's resource usage grows as input size increases. Focus on the dominant growth rate rather than machine-specific timing, and analyze both execution work and extra memory so you can compare approaches before benchmarking.

Complexity describes how resource use grows as input size grows.

## O(1) — Constant

`O(1)` means the amount of work does not grow with the number of input elements. It does **not** mean the operation takes exactly one CPU instruction; it means the step count is bounded by a constant with respect to input size. Examples include reading a known array index or checking a stored variable.

```python
value = nums[5]
```

Typical examples:

- Array index access
- Stack push/pop
- Average hash lookup

## O(log n) — Logarithmic

`O(log n)` appears when each step reduces the remaining problem by a constant factor, often by half. Binary search is the classic example. The logarithm base is ignored in Big-O because changing the base only multiplies the count by a constant factor.

Typical example:

```text
Binary Search
```

Each step reduces the search space by a constant factor.

For one billion elements:

```text
log2(1,000,000,000) ≈ 30
```

That is why binary search is extremely efficient.

## O(n) — Linear

`O(n)` means the running time grows proportionally with the input size. A single complete pass over an array is the standard example. Several separate linear passes are still `O(n)` because constant multipliers are omitted in asymptotic analysis.

```python
for value in nums:
    process(value)
```

One pass over the input.

## O(n log n)

`O(n log n)` commonly appears when an algorithm performs logarithmic levels of work and processes `O(n)` data across each level. Efficient comparison sorts such as merge sort and heap sort have this bound; divide-and-conquer algorithms often produce it as well.

Typical efficient comparison sorting:

- Merge Sort
- Heap Sort
- Average-case Quick Sort

## O(n²) — Quadratic

`O(n²)` usually appears when the algorithm examines many pairs of input elements, such as two nested loops over the same `n` items. Doubling `n` can make the dominant work roughly four times larger, so quadratic approaches become expensive quickly on large inputs.

Common when checking all pairs:

```python
for i in range(n):
    for j in range(n):
        ...
```

For very large `n`, this is usually too slow.

## O(2^n) — Exponential

The code below is a concrete example of **O(2^n) — Exponential**. Read it by identifying the input/state first, then trace each mutation or decision until the produced value/output. When reusing the pattern, preserve its required preconditions and include the cost of nested library operations in the complexity analysis.

Common when every element has two choices:

```text
include
exclude
```

Typical subset/backtracking problems.

## O(n!) — Factorial

Factorial is defined for non-negative integers by `n! = n × (n-1) × ... × 1`, with `0! = 1`. A recursive implementation mirrors that definition, but an iterative version avoids recursive call-stack growth. Factorial values grow extremely quickly, so ordinary fixed-width integer types overflow at relatively small `n` values.

Common when generating every ordering.

Examples:

- Permutations
- Brute-force Traveling Salesman

## Space Complexity

Space complexity measures how much additional memory grows with input size. Distinguish the input itself from **auxiliary space** used by the algorithm, and remember to include recursion depth, temporary arrays, hash tables, queues, and stacks. An in-place algorithm usually means `O(1)` or very small auxiliary storage, not that the input occupies no memory.

A fast algorithm can still use too much memory.

Example:

```python
seen = set(nums)
```

may improve speed but use:

```text
O(n)
```

extra memory.

Always analyze both:

```text
Time
Space
```

---

# 5. Asymptotic Notation

Asymptotic notation describes growth rates while ignoring constant factors and small-input details. Big-O is commonly used for an upper growth bound, Big-Omega for a lower bound, and Big-Theta when upper and lower bounds match asymptotically.

## Big-O

Big-O is an asymptotic upper bound on growth. In everyday algorithm analysis it is often used to describe dominant upper-order behavior, but the formal notation does not itself mean 'worst case'—case analysis and asymptotic bound are separate ideas.

Asymptotic upper bound. This is the notation used most often in interviews.

## Big-Omega

Big-Omega (`Ω`) gives an asymptotic lower bound: beyond some input size, the function grows at least as fast as the stated bound up to a constant factor.

Asymptotic lower bound.

## Big-Theta

Big-Theta (`Θ`) is a tight asymptotic bound: the function is bounded both above and below by the same growth rate up to constant factors.

Tight asymptotic bound.

## Ignore constants

Constant factors do not change asymptotic growth, so `3n + 20` is `O(n)`. Do not confuse this with real performance: constants still affect actual runtime and can matter greatly for realistic input sizes.

```text
O(2n)   → O(n)
O(100n) → O(n)
O(5000) → O(1)
```

## Ignore lower-order terms

For large `n`, the fastest-growing term dominates. Thus `n² + 100n + 5` is `O(n²)`. Lower-order terms can affect small inputs but do not change the asymptotic class.

```text
O(n² + n + 20) → O(n²)
```

---

# 6. Math Fundamentals for DSA

A small set of mathematical tools appears repeatedly in DSA: modular arithmetic, divisibility, GCD/LCM, primes, logarithms, combinatorics, and exponentiation. The purpose is practical—these tools simplify constraints, prevent overflow, or reduce repeated computation in algorithms.

## Greatest Common Divisor — Euclidean Algorithm

The Euclidean algorithm finds the greatest common divisor (GCD) by repeatedly replacing `(a, b)` with `(b, a mod b)` until the second value becomes zero. The remaining non-zero value is the GCD. It runs in logarithmic time with respect to the numeric values and is a standard building block for fractions, modular arithmetic, and LCM calculation.

```python
def gcd(a, b):
    while b:
        a, b = b, a % b
    return a
```

Complexity:

```text
O(log(min(a, b)))
```

## Least Common Multiple

The least common multiple (LCM) of two non-zero integers can be derived from the GCD: `lcm(a, b) = |a / gcd(a, b) × b|`. Dividing before multiplying reduces overflow risk in fixed-width languages. Define how your implementation should behave when either input is zero; a common convention returns zero.

```python
def lcm(a, b):
    return abs(a * b) // gcd(a, b)
```

## Prime Check

```python
def is_prime(n):
    if n < 2:
        return False

    divisor = 2

    while divisor * divisor <= n:
        if n % divisor == 0:
            return False
        divisor += 1

    return True
```

Why stop at `sqrt(n)`? If `n = a × b`, at least one factor must be `<= sqrt(n)`.

## Sieve of Eratosthenes

The Sieve of Eratosthenes finds all primes up to a limit by marking multiples of each discovered prime as composite. Starting the marking at `p × p` is enough because smaller multiples already have a smaller prime factor. The standard implementation runs in `O(n log log n)` time and uses `O(n)` marking space.

Find every prime up to `n`.

```python
def sieve(n):
    if n < 2:
        return []

    prime = [True] * (n + 1)
    prime[0] = prime[1] = False

    p = 2
    while p * p <= n:
        if prime[p]:
            for multiple in range(p * p, n + 1, p):
                prime[multiple] = False
        p += 1

    return [i for i, value in enumerate(prime) if value]
```

Typical complexity:

```text
O(n log log n)
```

## Fast Exponentiation

Fast exponentiation computes `base^exp` by repeatedly squaring the base and using the binary representation of the exponent. Each step halves the remaining exponent, reducing multiplication count from `O(exp)` to `O(log exp)`. A modular variant applies `% mod` after multiplications to keep values bounded.

```python
def power(base, exponent):
    result = 1

    while exponent > 0:
        if exponent % 2 == 1:
            result *= base

        base *= base
        exponent //= 2

    return result
```

Complexity:

```text
O(log exponent)
```

## Modular Arithmetic

Modular arithmetic keeps values within a fixed remainder range and is common in counting problems or large exponentiation. Addition and multiplication can usually be reduced after each operation, but division requires a modular inverse and is not equivalent to ordinary integer division.

Useful when results become extremely large.

```text
(a + b) mod m = ((a mod m) + (b mod m)) mod m
(a × b) mod m = ((a mod m) × (b mod m)) mod m
```

A common contest modulus is:

```python
MOD = 1_000_000_007
```

---

# 7. Bit Manipulation

Bit manipulation treats an integer as a sequence of binary bits. Operations such as AND (`&`), OR (`|`), XOR (`^`), complement (`~`), and shifts can test or modify individual bits efficiently. Use explicit parentheses around shift expressions when precedence could be unclear, and remember that signed integer width and overflow behavior are language-specific.

Important operators:

| Operator | Meaning |
|---|---|
| `a & b` | AND |
| `a \| b` | OR |
| `a ^ b` | XOR |
| `~a` | NOT |
| `a << k` | Left shift |
| `a >> k` | Right shift |

## Odd or even

The least significant binary bit tells parity: it is `1` for odd integers and `0` for even integers. Testing `n & 1` is a constant-time alternative to `n % 2`, although `% 2` is often clearer when bit operations are not otherwise relevant.

```python
if n & 1:
    print("odd")
```

## Check kth bit

`bit_is_set(n, k)` tests whether the zero-based bit at position `k` in integer `n` is `1`. `1 << k` creates a mask containing only that bit, and bitwise AND keeps it only if it is present in `n`. The function returns a Boolean and runs in `O(1)` time for fixed-width machine integers.

```python
def bit_is_set(n, k):
    return (n & (1 << k)) != 0
```

## Set kth bit

To set the zero-based bit `k`, OR the number with the mask `1 << k`. The mask has a `1` only at position `k`, so every other bit is preserved while bit `k` becomes `1`. This is a constant-time bit operation on fixed-width integers.

```python
n |= 1 << k
```

## Clear kth bit

To clear the zero-based bit `k`, build the mask `1 << k`, invert it, and AND it with the number. The inverted mask has a `0` at position `k`, which forces that bit off while preserving the remaining bits.

```python
n &= ~(1 << k)
```

## Toggle kth bit

To toggle the zero-based bit `k`, XOR the number with `1 << k`. XOR with `1` flips a bit (`0 ↔ 1`), while XOR with `0` leaves the other positions unchanged.

```python
n ^= 1 << k
```

## Remove lowest set bit

`n & (n - 1)` clears the lowest set bit of a positive/nonzero integer. Repeating this operation counts set bits in time proportional to the number of `1` bits rather than the full integer width (Brian Kernighan's technique).

```python
n &= n - 1
```

Used in efficient bit counting:

```python
def count_set_bits(n):
    count = 0

    while n:
        n &= n - 1
        count += 1

    return count
```

## XOR trick

When every value except one appears exactly twice, XOR is useful because `x ^ x = 0` and `x ^ 0 = x`. XORing the full array cancels each duplicate pair, leaving the unique value in `O(n)` time and `O(1)` extra space. This exact trick does not directly solve cases where duplicates appear three times.

Properties:

```text
x ^ x = 0
x ^ 0 = x
```

Problem:

> Every number appears twice except one.

```python
def single_number(nums):
    answer = 0

    for value in nums:
        answer ^= value

    return answer
```

```text
Time:  O(n)
Space: O(1)
```

---

# 8. Arrays

An array-like structure stores elements in an indexed sequence. Its main advantage is direct access by position; the main trade-off is that inserting or deleting near the front or middle usually requires shifting elements. In DSA problems, arrays are also the base structure behind two pointers, sliding windows, prefix sums, binary search, heaps, and many dynamic-programming tables.

Arrays store elements sequentially.

Python lists behave like dynamic arrays.

```python
nums = [10, 20, 30, 40]
```

```text
Index:  0   1   2   3
Value: 10  20  30  40
```

## Typical Complexity

| Operation | Complexity |
|---|---:|
| Access by index | O(1) |
| Update by index | O(1) |
| Search unsorted | O(n) |
| Append | Amortized O(1) |
| Insert at beginning | O(n) |
| Delete in middle | O(n) |

## Reverse an array in place

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

## Kadane's Algorithm

An algorithm is a finite, unambiguous procedure that converts an input into the required output. A useful explanation of an algorithm should state its preconditions, the main invariant or idea that keeps it correct, when it stops, and its time and space complexity.

Problem:

> Find maximum sum of a contiguous subarray.

Input:

```text
[-2, 1, -3, 4, -1, 2, 1, -5, 4]
```

Best subarray:

```text
[4, -1, 2, 1]
```

Answer:

```text
6
```

```python
def max_subarray(nums):
    current = nums[0]
    best = nums[0]

    for value in nums[1:]:
        current = max(value, current + value)
        best = max(best, current)

    return best
```

```text
Time:  O(n)
Space: O(1)
```

Recognition clue:

```text
maximum/minimum sum over a contiguous subarray
```

---

# 9. Strings

A string is a sequence of characters, but its exact behavior depends on the language's string model and character encoding. DSA string problems commonly need indexing/traversal, frequency counting, substring handling, comparison, prefix/suffix reasoning, or pattern matching. Always check whether the task assumes simple ASCII-like characters or full Unicode text.

Strings are sequences of characters.

Many string problems reduce to:

- Arrays
- Hash maps
- Two pointers
- Sliding windows
- Tries
- Dynamic programming

## Palindrome

A palindrome reads the same forward and backward under the problem's comparison rules. The standard two-pointer check compares the leftmost and rightmost relevant characters and moves inward, stopping on the first mismatch. Time is `O(n)` and extra space can be `O(1)` when normalization is not stored separately.

```python
def is_palindrome(s):
    left = 0
    right = len(s) - 1

    while left < right:
        if s[left] != s[right]:
            return False

        left += 1
        right -= 1

    return True
```

## Character frequency

A frequency table records how many times each value occurs. Python's `Counter` constructs this mapping directly from an iterable and is useful when counts—not just membership—are needed.

```python
from collections import Counter

frequency = Counter("banana")
```

Result:

```text
b: 1
a: 3
n: 2
```

## Anagram

Two strings are anagrams when they contain the same symbols with the same frequencies, subject to the problem's normalization rules. A frequency map gives `O(n)` expected time and avoids sorting; sorting both strings is simpler in some cases but typically costs `O(n log n)`. Decide explicitly whether case, spaces, punctuation, and Unicode normalization matter.

```python
from collections import Counter

def are_anagrams(a, b):
    return Counter(a) == Counter(b)
```

Example:

```text
listen
silent
```

## Substring vs Subsequence

**Substring** = contiguous.

```text
"bcd"
```

is a substring of:

```text
"abcdef"
```

**Subsequence** = order is preserved but positions may be skipped.

```text
"ace"
```

is a subsequence of:

```text
"abcde"
```

This difference frequently determines the correct algorithm.

---

# 10. Linked Lists

A linked list stores values in nodes connected by references rather than by contiguous indexed positions. This makes pointer rewiring cheap once the relevant node is known, but random access is slow because traversal normally starts from the head. Linked-list problems therefore focus heavily on pointer movement, insertion/removal, reversal, cycle detection, and fast/slow-pointer techniques.

A linked list stores nodes connected by references.

```text
10 → 20 → 30 → None
```

```python
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None
```

## Advantages

These are the practical benefits of **Linked Lists**, not automatic guarantees. They matter most when the pattern is solving the problem it was designed for; otherwise the extra abstraction may cost more than it saves.

- Dynamic size
- Fast insertion/deletion when location is already known

## Disadvantages

These are the main trade-offs introduced by **Linked Lists**. Treat them as design costs to evaluate against the expected benefit, especially for small systems where additional layers, indirection, or infrastructure can reduce clarity.

- No `O(1)` random access
- Pointer/reference memory overhead
- Usually poorer CPU-cache locality than arrays

## Traverse

Linked-list traversal starts at `head` and repeatedly follows each node's `next` reference until it becomes `None`. `current` is only a moving reference; it does not change the links. The example prints each node value, visits `n` nodes in `O(n)` time, and uses `O(1)` extra iterative space.

```python
def traverse(head):
    current = head

    while current:
        print(current.value)
        current = current.next
```

## Reverse linked list

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

## Middle node — Fast/Slow pointers

Advance `slow` by one node and `fast` by two. When `fast` reaches the end, `slow` is at the middle. For even-length lists, the loop condition determines whether the first or second middle is returned, so match it to the problem's required convention.

```python
def middle_node(head):
    slow = head
    fast = head

    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next

    return slow
```

## Detect cycle — Floyd's Algorithm

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

```text
Time:  O(n)
Space: O(1)
```

Recognition clues:

```text
linked list + cycle
linked list + middle
linked list + kth relation
```

---

# 11. Stacks

A stack follows:

```text
LIFO = Last In, First Out
```

Python:

```python
stack = []
stack.append(10)
stack.append(20)

value = stack[-1]
removed = stack.pop()
```

## Use Cases

Use **Stacks** when the problem characteristics below are genuinely present. The list is a recognition aid, not a rule that every listed situation must use this approach.

- Undo/redo
- Browser navigation
- Function calls
- Expression parsing
- DFS
- Balanced brackets
- Monotonic-stack problems

## Valid Parentheses

Balanced-bracket checking uses a stack of opening brackets. Each closing bracket must match the most recent unmatched opening bracket, so a mismatch or an empty stack fails immediately; after the scan, the stack must also be empty. The algorithm is `O(n)` time and `O(n)` worst-case space.

```python
def valid_parentheses(s):
    pairs = {
        ')': '(',
        ']': '[',
        '}': '{'
    }

    stack = []

    for ch in s:
        if ch in "([{":
            stack.append(ch)
        else:
            if not stack or stack[-1] != pairs.get(ch):
                return False
            stack.pop()

    return not stack
```

---

# 12. Queues and Deques

A queue follows:

```text
FIFO = First In, First Out
```

Use `deque` in Python:

```python
from collections import deque

queue = deque()
queue.append("A")
queue.append("B")

first = queue.popleft()
```

## Common Uses

Use **Queues and Deques** when the problem characteristics below are genuinely present. The list is a recognition aid, not a rule that every listed situation must use this approach.

- BFS
- Customer/service queues
- Job processing
- Producer/consumer concepts

## Deque

A deque (double-ended queue) supports insertion and removal at both the front and back. It can behave as either a stack or a queue and is especially useful for sliding-window algorithms and 0-1 BFS. Prefer an implementation whose front and back operations are constant-time rather than an array operation that shifts many elements.

A deque supports insertion/removal from both ends.

```python
from collections import deque

dq = deque()

dq.append(10)
dq.appendleft(5)
dq.pop()
dq.popleft()
```

Important uses:

- Sliding-window maximum
- BFS
- Monotonic queue

---

# 13. Hash Maps and Sets

Hash tables give very fast average lookup.

Python:

```python
mapping = {}
unique = set()
```

Typical average complexity:

| Operation | Average |
|---|---:|
| Insert | O(1) |
| Search | O(1) |
| Delete | O(1) |

Worst-case behavior may be worse because of collisions, but normal implementations perform very well.

## Frequency map

A frequency map stores `value → count`. Scan the input once, incrementing the count for each value; later frequency queries are average `O(1)` with a hash map. This pattern is useful for duplicates, anagrams, counting categories, majority/frequency problems, and many sliding-window algorithms.

```python
def frequencies(nums):
    freq = {}

    for value in nums:
        freq[value] = freq.get(value, 0) + 1

    return freq
```

## Duplicate detection

Duplicate detection can use a set of values seen so far. If the current value is already present, a duplicate exists; otherwise add it and continue. This is `O(n)` expected time with `O(n)` extra space, compared with `O(n²)` pair checking or `O(n log n)` sorting.

```python
def contains_duplicate(nums):
    seen = set()

    for value in nums:
        if value in seen:
            return True

        seen.add(value)

    return False
```

Recognition clues:

```text
duplicate
count
frequency
seen before
membership
matching complement
```

---

# 14. Sorting Algorithms

Sorting rearranges values according to an ordering rule so later operations can exploit structure. Learn not only the code but also stability, in-place behavior, best/average/worst complexity, comparator requirements, and when a language's built-in sort is preferable to a manual algorithm.

Sorting often unlocks other techniques:

- Binary search
- Two pointers
- Greedy algorithms
- Interval merging

## Bubble Sort

Bubble sort repeatedly compares adjacent elements and swaps pairs that are out of order. After each full pass, one extreme value has moved to its final end position. It is easy to learn but `O(n²)` in average/worst cases; with an early-exit flag it can be `O(n)` on already sorted input.

Repeatedly swap adjacent out-of-order values.

```python
def bubble_sort(arr):
    n = len(arr)

    for i in range(n):
        swapped = False

        for j in range(n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True

        if not swapped:
            break

    return arr
```

Worst:

```text
O(n²)
```

Mostly educational.

## Selection Sort

Selection sort repeatedly chooses the smallest (or largest) remaining element and places it into the next final position. It performs `O(n²)` comparisons regardless of initial order and only `O(n)` swaps, so it is mostly educational or useful when writes are unusually expensive. The usual in-place form is not stable.

Find the smallest remaining value and place it next.

```text
Time: O(n²)
```

Good for learning but rarely preferred for large real data.

## Insertion Sort

Insertion sort grows a sorted prefix one element at a time. For each new value, it shifts larger prefix elements to the right until the correct insertion position opens. It is stable with the usual comparison, in-place, `O(n²)` in the average/worst case, and `O(n)` on already or nearly sorted data.

Insert each value into an already-sorted prefix.

```python
def insertion_sort(arr):
    for i in range(1, len(arr)):
        current = arr[i]
        j = i - 1

        while j >= 0 and arr[j] > current:
            arr[j + 1] = arr[j]
            j -= 1

        arr[j + 1] = current

    return arr
```

Good for:

- Small arrays
- Nearly sorted arrays

## Merge Sort

Merge sort divides the sequence into halves, recursively sorts each half, and merges two sorted halves in linear time. Its recurrence leads to `O(n log n)` time in all standard cases; array implementations typically need `O(n)` auxiliary merge storage. Merge sort is stable when equal elements are taken from the left half first.

Divide into halves, recursively sort them, then merge.

```python
def merge_sort(arr):
    if len(arr) <= 1:
        return arr

    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])

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

```text
Time:  O(n log n)
Space: O(n)
```

## Quick Sort

Quick sort partitions elements around a pivot so smaller and larger values move to opposite sides, then recursively sorts the partitions. Average time is `O(n log n)` but poor pivot choices can produce `O(n²)`. Partition scheme, duplicate handling, and recursion depth are important implementation details.

Partition around a pivot.

Typical complexity:

```text
Average: O(n log n)
Worst:   O(n²)
```

## Heap Sort

A heap is a partially ordered tree structure commonly used to implement a priority queue. A min-heap exposes the smallest item; a max-heap exposes the largest. Insert and removal of the root are typically `O(log n)`, while reading the root is `O(1)`, making heaps ideal for top-k, scheduling, streaming minima/maxima, and graph algorithms such as Dijkstra or Prim.

Uses a heap.

```text
Build heap: O(n)
Overall:    O(n log n)
```

## Counting Sort

Useful when integer values lie in a small range.

```text
Time: O(n + k)
```

`k` = size of value range.

Avoid it when the range is huge.

## Radix Sort

Radix sort orders keys by processing digits/positions using a stable sub-sort such as counting sort. For fixed-width non-negative integers, complexity is roughly `O(d(n + k))` where `d` is digit count and `k` the radix. Handling negatives, strings, or variable lengths requires an explicit representation strategy.

Processes digits/positions.

Typical:

```text
O(d(n + k))
```

where `d` is number of digits/positions.

## Stable Sorting

Sorting all values is often the simplest selection baseline. It is appropriate when ordered output is useful elsewhere or input size is moderate; it does unnecessary work when only one rank is needed and no other sorted-order benefit exists.

A stable sort preserves the original order of equal keys.

This is useful when sorting records by multiple fields.

## Sorting Summary

| Algorithm | Best | Average | Worst | Stable? |
|---|---:|---:|---:|---|
| Bubble | O(n) optimized | O(n²) | O(n²) | Yes |
| Selection | O(n²) | O(n²) | O(n²) | Usually No |
| Insertion | O(n) | O(n²) | O(n²) | Yes |
| Merge | O(n log n) | O(n log n) | O(n log n) | Yes |
| Quick | O(n log n) | O(n log n) | O(n²) | Usually No |
| Heap | O(n log n) | O(n log n) | O(n log n) | No |

---

# 15. Searching and Binary Search

Searching asks whether, where, or under what condition a target can be found. Start with linear search as the no-precondition baseline, then use binary search when ordering or monotonicity lets you safely discard large parts of the search space.

## Linear Search

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

```python
def linear_search(nums, target):
    for i, value in enumerate(nums):
        if value == target:
            return i

    return -1
```

```text
Time: O(n)
```

## Binary Search

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

Requires sorted data or another monotonic search condition.

```python
def binary_search(nums, target):
    left = 0
    right = len(nums) - 1

    while left <= right:
        mid = left + (right - left) // 2

        if nums[mid] == target:
            return mid

        if nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return -1
```

```text
Time: O(log n)
```

## Lower Bound

A lower bound returns the first position whose value is **not less than** the target (equivalently, the insertion position before existing equal values). The binary-search invariant must preserve all possible answers, including the position immediately after the final element when every value is smaller.

First position where:

```text
value >= target
```

## Upper Bound

An upper bound returns the first position whose value is **greater than** the target, which is the insertion position after all existing equal values. It differs from lower bound only in the comparison that decides which half can still contain the answer.

First position where:

```text
value > target
```

## Binary Search on Answer

Binary search can search an **answer range**, not only an array.

Example:

> Find the minimum machine speed that finishes all jobs within a deadline.

Feasibility might look like:

```text
False False False True True True
```

The first `True` can be found using binary search.

Typical problems:

- Minimum capacity
- Maximum minimum distance
- Minimum speed
- Shipping capacity
- Book/job allocation
- Production rate

Recognition clues:

```text
minimum possible X
maximum possible X
can it be done with X?
monotonic feasibility
```

---

# 16. Two Pointers

Two pointers maintain two indexes or references whose movement eliminates unnecessary repeated work. Common forms are opposite-end pointers on sorted data and same-direction read/write pointers for in-place filtering. The technique is most valuable when pointer movement can be justified by an invariant, such as sorted order or a maintained valid region.

Two indices move through the data and often replace nested loops.

## Pair Sum in Sorted Array

With sorted input, place one pointer at each end. If the sum is too small, moving the left pointer right is the only move that can increase it; if the sum is too large, move the right pointer left. This invariant gives `O(n)` time and `O(1)` extra space after sorting is already available.

```python
def pair_sum(nums, target):
    left = 0
    right = len(nums) - 1

    while left < right:
        total = nums[left] + nums[right]

        if total == target:
            return [left, right]

        if total < target:
            left += 1
        else:
            right -= 1

    return None
```

```text
Time: O(n)
```

## Remove Duplicates from Sorted Array

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

Recognition clues:

```text
sorted array
pair
palindrome
merge
remove duplicates
partition
```

---

# 17. Sliding Window

A sliding window tracks a contiguous range while updating only the information that changes when the range expands or shrinks. Fixed-size windows are used when the length is known; variable-size windows adjust a boundary until a validity condition is restored. The usual goal is to replace repeated recomputation of every subarray or substring with a single linear pass.

Sliding window is powerful for **contiguous** portions of arrays or strings.

Two major types:

1. Fixed-size window
2. Variable-size window

## Fixed Window — Maximum sum of K consecutive values

This is a fixed-size sliding-window problem. Build the first `k`-element sum once, then each shift subtracts the outgoing value and adds the incoming value, producing `O(n)` total time instead of `O(nk)` repeated summation.

```python
def max_sum_k(nums, k):
    if k > len(nums):
        return None

    window_sum = sum(nums[:k])
    best = window_sum

    for right in range(k, len(nums)):
        window_sum += nums[right]
        window_sum -= nums[right - k]
        best = max(best, window_sum)

    return best
```

```text
Time: O(n)
```

## Variable Window — Longest substring without duplicates

A variable-size sliding window expands one boundary and shrinks the other whenever the validity constraint is violated. This is linear when each boundary moves forward at most `n` times and window state can be updated incrementally.

```python
def longest_unique_substring(s):
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

Recognition clues:

```text
substring
subarray
contiguous
longest
shortest
at most K
window of size K
without repeating
```

Important warning: sliding-window sum logic may fail when negative values destroy the monotonic behavior needed to move boundaries safely.

---

# 18. Prefix Sum and Difference Arrays

Prefix sums and difference arrays are complementary preprocessing techniques. Prefix sums make repeated range queries cheap; difference arrays make many range updates cheap before one final reconstruction. Their correctness depends on a clear indexing convention and careful boundary handling.

## Prefix Sum

A prefix sum precomputes cumulative totals so that later range sums can be answered by subtraction. With the common convention `prefix[i] = sum of elements before i`, the sum of the half-open range `[left, right)` is `prefix[right] - prefix[left]`. Building the prefix array costs `O(n)` time and each range query then costs `O(1)`.

Input:

```text
[2, 4, 1, 5, 3]
```

Prefix array:

```text
[0, 2, 6, 7, 12, 15]
```

```python
def build_prefix(nums):
    prefix = [0]

    for value in nums:
        prefix.append(prefix[-1] + value)

    return prefix
```

Range sum from `l` to `r`:

```python
prefix[r + 1] - prefix[l]
```

After preprocessing:

```text
Range query: O(1)
```

## Prefix Sum + Hash Map

A prefix sum precomputes cumulative totals so that later range sums can be answered by subtraction. With the common convention `prefix[i] = sum of elements before i`, the sum of the half-open range `[left, right)` is `prefix[right] - prefix[left]`. Building the prefix array costs `O(n)` time and each range query then costs `O(1)`.

Very important problem:

> Count subarrays with sum equal to `k`.

```python
def subarray_sum(nums, k):
    count = 0
    current_sum = 0
    frequency = {0: 1}

    for value in nums:
        current_sum += value
        count += frequency.get(current_sum - k, 0)
        frequency[current_sum] = frequency.get(current_sum, 0) + 1

    return count
```

```text
Time: O(n)
```

This works with negative numbers too.

## Difference Array

Efficient repeated range updates.

To add `x` to `[l, r]`:

```python
diff[l] += x

if r + 1 < n:
    diff[r + 1] -= x
```

Then prefix-sum the difference array to recover final values.

Applications:

- Booking ranges
- Capacity changes
- Calendar load
- Range increment operations

---

# 19. Recursion

Recursion solves a problem by calling the same routine on a smaller or simpler state. Every recursive solution needs a **base case** that stops further calls and a **progress rule** that moves toward that base case. Also account for call-stack space: even an algorithm with little explicit memory usage may use `O(depth)` stack space.

A recursive function calls itself.

Every recursive solution requires:

1. Base case
2. Recursive case

```python
def factorial(n):
    if n <= 1:
        return 1

    return n * factorial(n - 1)
```

Call stack:

```text
factorial(4)
└── factorial(3)
    └── factorial(2)
        └── factorial(1)
```

## Good uses

These are situations where the surrounding technique matches the data shape and operations well. Confirm the stated preconditions first; a pattern can become incorrect or slower when those assumptions do not hold.

- Trees
- Divide and conquer
- Backtracking

## Risks

- Stack overflow
- Repeated computation
- Difficult debugging
- Extra recursive overhead

Use iteration when recursion provides no meaningful benefit.

---

# 20. Backtracking

Backtracking explores a decision tree by making a choice, recursively exploring what follows, and then undoing that choice before trying the next option. It is appropriate when the task asks for all valid combinations, permutations, placements, paths, or constraint-satisfying configurations. Pruning impossible branches early is often the difference between a practical and an impractical solution.

Backtracking explores choices and undoes them.

General pattern:

```python
def backtrack(state):
    if complete(state):
        save(state)
        return

    for choice in choices(state):
        make(choice)
        backtrack(state)
        undo(choice)
```

Mental model:

```text
Choose
Explore
Undo
```

## Generate Subsets

Generating all subsets explores two choices for each element: include it or exclude it. That creates `2^n` possible subsets, so exponential output size is unavoidable. Backtracking should add a **copy** of the current path to the result because the same mutable path is modified during later recursive calls.

```python
def subsets(nums):
    result = []
    current = []

    def backtrack(index):
        if index == len(nums):
            result.append(current.copy())
            return

        backtrack(index + 1)

        current.append(nums[index])
        backtrack(index + 1)
        current.pop()

    backtrack(0)
    return result
```

There are:

```text
2^n
```

subsets.

## Generate Permutations

Generating permutations chooses one unused item for each next position, recursively explores the remainder, and then undoes the choice. There are `n!` outputs for distinct items, so factorial work is inherent. With duplicate input values, add a duplicate-skipping rule if unique permutations are required.

```python
def permutations(nums):
    result = []

    def backtrack(start):
        if start == len(nums):
            result.append(nums.copy())
            return

        for i in range(start, len(nums)):
            nums[start], nums[i] = nums[i], nums[start]
            backtrack(start + 1)
            nums[start], nums[i] = nums[i], nums[start]

    backtrack(0)
    return result
```

Classic backtracking problems:

- N-Queens
- Sudoku
- Word Search
- Combination Sum
- Generate Parentheses
- Permutations
- Subsets
- Maze paths

Recognition clues:

```text
generate all possibilities
all combinations
all permutations
try every valid arrangement
```

---

# 21. Trees

A tree is a connected acyclic hierarchical structure with nodes linked by parent/child relationships. Tree algorithms are easiest to understand recursively: define what one subtree call returns, choose a traversal order, and account for tree height because recursion/operation cost can degrade on skewed trees.

A tree represents hierarchy.

```text
        A
       / \
      B   C
     / \
    D   E
```

Important terms:

- Root
- Parent
- Child
- Sibling
- Leaf
- Edge
- Depth
- Height
- Subtree
- Ancestor
- Descendant

## Binary Tree

A binary tree node has at most two children, conventionally `left` and `right`. Unlike a BST, a general binary tree has no ordering rule unless the problem states one; searches therefore usually require traversal rather than directional comparison.

Each node has at most two children.

```python
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None
```

## Preorder

Preorder traversal visits **node → left subtree → right subtree**. It is useful when the parent must be processed before its children, such as copying a tree, serializing certain tree formats, or producing prefix-style expression order. A complete traversal visits every node once, so time is `O(n)`.

```text
Root → Left → Right
```

```python
def preorder(root):
    if not root:
        return

    print(root.value)
    preorder(root.left)
    preorder(root.right)
```

## Inorder

Inorder traversal visits **left subtree → node → right subtree**. On a Binary Search Tree with a consistent ordering rule, this produces keys in sorted order. A complete traversal is `O(n)` time and uses `O(h)` call-stack/explicit-stack space for tree height `h`.

```text
Left → Root → Right
```

```python
def inorder(root):
    if not root:
        return

    inorder(root.left)
    print(root.value)
    inorder(root.right)
```

Important property:

> Inorder traversal of a valid BST returns values in sorted order.

## Postorder

Postorder traversal visits **left subtree → right subtree → node**. Because children are processed before their parent, it is useful for deleting trees, computing subtree aggregates, and many tree-DP problems. A complete traversal is `O(n)` time and uses `O(h)` traversal stack space.

```text
Left → Right → Root
```

Useful when child results are needed before the parent.

Examples:

- Tree deletion
- Subtree size
- Directory-size calculation
- Tree DP

## Level Order

Level-order traversal is BFS on a tree. Use a queue to process nodes in increasing depth; if the output is grouped by levels, capture the queue size at the start of each level so newly enqueued children belong to the next group.

Uses BFS:

```python
from collections import deque

def level_order(root):
    if not root:
        return []

    queue = deque([root])
    result = []

    while queue:
        node = queue.popleft()
        result.append(node.value)

        if node.left:
            queue.append(node.left)
        if node.right:
            queue.append(node.right)

    return result
```

## Height

A node's **height** is the length of the longest downward path from that node to a leaf, under the chosen edge/node convention. Tree operation complexity is often expressed in terms of overall tree height `h`.

```python
def height(root):
    if root is None:
        return 0

    return 1 + max(height(root.left), height(root.right))
```

Common tree interview problems:

- Maximum depth
- Minimum depth
- Diameter
- Balanced tree
- Invert tree
- Lowest common ancestor
- Path sum
- Serialize/deserialize
- Construct tree from traversals

---

# 22. Binary Search Trees

A Binary Search Tree (BST) maintains an ordering invariant: values in one subtree compare before the node and values in the other compare after it, according to the chosen duplicate policy. Operations depend on tree height, so an unbalanced BST can degrade from `O(log n)` expected/balanced behavior to `O(n)`.

BST rule:

```text
left values  < node
right values > node
```

If duplicates are allowed, a consistent policy must be defined.

Example:

```text
        8
       / \
      3   10
     / \    \
    1   6    14
```

## Search

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

```python
def search_bst(root, target):
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

Balanced tree:

```text
O(log n)
```

Worst unbalanced tree:

```text
O(n)
```

## Balanced BSTs

A balanced BST keeps height `O(log n)` by enforcing a balancing rule during updates. This prevents ordinary search/insert/delete from degrading to linear time on adversarial insertion order. AVL and Red-Black trees use different balance guarantees and update trade-offs.

Examples:

- AVL Tree
- Red-Black Tree

Related database/indexing structures:

- B-tree
- B+ tree

---

# 23. Heaps and Priority Queues

A heap efficiently exposes the current minimum or maximum.

Python provides a min-heap:

```python
import heapq

heap = []
heapq.heappush(heap, 20)
heapq.heappush(heap, 5)
heapq.heappush(heap, 10)

print(heapq.heappop(heap))
```

Output:

```text
5
```

## Complexity

| Operation | Complexity |
|---|---:|
| Peek min | O(1) |
| Insert | O(log n) |
| Remove min | O(log n) |
| Build heap | O(n) |

## Top K Largest Values

A min-heap of size `k` can maintain the `k` largest values seen so far. Push candidates and remove the smallest whenever the heap exceeds `k`; at the end, the heap contains the desired top `k`. This uses `O(n log k)` time and `O(k)` extra space, often better than sorting all `n` items.

```python
import heapq

def top_k_largest(nums, k):
    heap = []

    for value in nums:
        heapq.heappush(heap, value)

        if len(heap) > k:
            heapq.heappop(heap)

    return sorted(heap, reverse=True)
```

```text
Time: O(n log k)
```

Useful when `k << n`.

Recognition clues:

```text
top K
kth largest
kth smallest
priority
closest K
repeated smallest/largest
```

Real uses:

- Schedulers
- Dijkstra
- Top-K rankings
- Merge K sorted streams
- Streaming median

---

# 24. Tries

A Trie stores strings by prefix.

Words:

```text
cat
car
care
dog
```

Conceptually:

```text
root
├─ c
│  └─ a
│     ├─ t
│     └─ r
│        └─ e
└─ d
   └─ o
      └─ g
```

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_word = False
```

```python
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

For a word of length `L`:

```text
Insert/Search/Prefix: O(L)
```

Use cases:

- Autocomplete
- Dictionaries
- Prefix search
- Spell checking
- Word games

---

# 25. Graphs

A graph contains:

```text
Vertices + Edges
```

Graphs may be:

- Directed
- Undirected
- Weighted
- Unweighted
- Cyclic
- Acyclic
- Connected
- Disconnected

Real-world graph examples:

- Social network
- Road network
- Flight network
- Computer network
- Package dependency graph
- Workflow graph

## Adjacency List

An adjacency list stores, for each vertex, the vertices (and optionally edge weights) directly connected to it. It uses `O(V + E)` space and is usually preferred for sparse graphs because traversing a vertex touches only its actual outgoing/incident edges. For undirected graphs, each edge is normally stored in both endpoint lists.

```python
graph = {
    "A": ["B", "C"],
    "B": ["A", "D"],
    "C": ["A", "D"],
    "D": ["B", "C"]
}
```

Space:

```text
O(V + E)
```

Usually best for sparse graphs.

## Adjacency Matrix

An adjacency matrix uses a `V × V` table where one cell records whether or with what weight an edge connects two vertices. Edge existence is `O(1)` to check, but memory is `O(V²)` even for sparse graphs. It is useful for dense graphs or algorithms that naturally work with all vertex pairs.

```text
    A B C D
A   0 1 1 0
B   1 0 0 1
C   1 0 0 1
D   0 1 1 0
```

Space:

```text
O(V²)
```

Useful for dense graphs or constant-time edge-existence checks.

---

# 26. BFS

Breadth-first search explores a graph or tree level by level using a queue. In an unweighted graph, the first time BFS reaches a vertex is through a path with the minimum number of edges from the start. With adjacency-list representation, a complete traversal is `O(V + E)` when each vertex is processed once.

Breadth-First Search explores level by level.

Uses a queue.

```python
from collections import deque

def bfs(graph, start):
    visited = {start}
    queue = deque([start])

    while queue:
        node = queue.popleft()
        print(node)

        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
```

Complexity:

```text
O(V + E)
```

## Use BFS for

- Shortest path in unweighted graphs
- Minimum number of moves
- Level-order tree traversal
- Grid shortest paths
- Degrees of separation
- Multi-source nearest-distance problems

Important practice: mark nodes visited when they are **enqueued**, not after they are later removed, to avoid duplicate queue entries.

---

# 27. DFS

Depth-first search explores one branch as far as possible before returning to try another branch. It can be implemented recursively or with an explicit stack and is widely used for connected components, cycle detection, tree processing, path exploration, topological reasoning, and many backtracking-style searches. Track visited state in cyclic graphs to avoid endless revisits.

Depth-First Search explores deeply before backtracking.

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

## Common DFS Uses

Depth-first search explores one branch as far as possible before returning to try another branch. It can be implemented recursively or with an explicit stack and is widely used for connected components, cycle detection, tree processing, path exploration, topological reasoning, and many backtracking-style searches. Track visited state in cyclic graphs to avoid endless revisits.

- Connected components
- Cycle detection
- Tree traversal
- Island counting
- Graph exploration
- Topological-sort variants

## Number of Islands

Treat each land cell as a graph vertex connected to neighboring land cells. Scan the grid; each unvisited land cell starts one BFS/DFS that marks its entire island. Every cell is processed a constant number of times, so runtime is `O(rows × cols)`.

```python
def num_islands(grid):
    if not grid:
        return 0

    rows = len(grid)
    cols = len(grid[0])
    count = 0

    def visit(r, c):
        if (
            r < 0 or r >= rows
            or c < 0 or c >= cols
            or grid[r][c] != "1"
        ):
            return

        grid[r][c] = "0"
        visit(r + 1, c)
        visit(r - 1, c)
        visit(r, c + 1)
        visit(r, c - 1)

    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == "1":
                count += 1
                visit(r, c)

    return count
```

This demonstrates that a matrix can be an implicit graph.

---

# 28. Topological Sorting

Sorting rearranges values according to an ordering rule so later operations can exploit structure. Learn not only the code but also stability, in-place behavior, best/average/worst complexity, comparator requirements, and when a language's built-in sort is preferable to a manual algorithm.

Topological ordering applies to a:

```text
DAG = Directed Acyclic Graph
```

If:

```text
A → B
```

then `A` must appear before `B`.

Applications:

- Course prerequisites
- Package/build dependencies
- Workflow ordering
- Job scheduling
- Spreadsheet dependency evaluation

## Kahn's Algorithm

An algorithm is a finite, unambiguous procedure that converts an input into the required output. A useful explanation of an algorithm should state its preconditions, the main invariant or idea that keeps it correct, when it stops, and its time and space complexity.

```python
from collections import deque

def topological_sort(graph):
    indegree = {node: 0 for node in graph}

    for node in graph:
        for neighbor in graph[node]:
            indegree[neighbor] += 1

    queue = deque(
        node for node in graph
        if indegree[node] == 0
    )

    order = []

    while queue:
        node = queue.popleft()
        order.append(node)

        for neighbor in graph[node]:
            indegree[neighbor] -= 1

            if indegree[neighbor] == 0:
                queue.append(neighbor)

    if len(order) != len(graph):
        raise ValueError("Cycle detected")

    return order
```

```text
Time: O(V + E)
```

Recognition clues:

```text
prerequisite
dependency
must happen before
course schedule
build order
```

---

# 29. Shortest Path Algorithms

Choose the algorithm based on the graph.

## BFS

Breadth-first search explores a graph or tree level by level using a queue. In an unweighted graph, the first time BFS reaches a vertex is through a path with the minimum number of edges from the start. With adjacency-list representation, a complete traversal is `O(V + E)` when each vertex is processed once.

Use when every edge has equal cost, typically `1`.

```text
O(V + E)
```

## Dijkstra's Algorithm

Dijkstra's algorithm computes single-source shortest paths when edge weights are non-negative. Maintain tentative distances and repeatedly process the smallest-distance candidate from a min-priority queue; ignore stale queue entries whose distance no longer matches the best known value. Typical adjacency-list complexity is `O((V+E) log V)`.

Use for non-negative weighted edges.

```python
import heapq

def dijkstra(graph, start):
    distance = {
        node: float("inf")
        for node in graph
    }

    distance[start] = 0
    heap = [(0, start)]

    while heap:
        dist, node = heapq.heappop(heap)

        if dist != distance[node]:
            continue

        for neighbor, weight in graph[node]:
            candidate = dist + weight

            if candidate < distance[neighbor]:
                distance[neighbor] = candidate
                heapq.heappush(heap, (candidate, neighbor))

    return distance
```

Typical heap complexity:

```text
O((V + E) log V)
```

Do **not** use ordinary Dijkstra with negative edge weights.

## Bellman-Ford

Bellman-Ford finds single-source shortest paths even when some edges are negative. Relax every edge up to `V-1` times because a simple shortest path uses at most `V-1` edges; one additional successful relaxation indicates a reachable negative cycle. Complexity is `O(VE)`.

Handles negative edges and detects reachable negative cycles.

```text
Time: O(VE)
```

## Floyd-Warshall

Floyd-Warshall computes all-pairs shortest paths by progressively allowing each vertex as an intermediate point. Its core transition is `dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])`. It uses `O(V³)` time and `O(V²)` distance storage and can handle negative edges, but not negative cycles when meaningful finite shortest paths are required.

All-pairs shortest paths.

```text
Time:  O(V³)
Space: O(V²)
```

Useful when the number of vertices is relatively small and many source/destination queries are needed.

## DAG Shortest Path

For a weighted DAG:

1. Topologically sort vertices.
2. Relax edges in topological order.

Can run in:

```text
O(V + E)
```

## Shortest-Path Choice Table

| Situation | Algorithm |
|---|---|
| Unweighted | BFS |
| Weighted, non-negative | Dijkstra |
| Negative edges | Bellman-Ford |
| All-pairs, small V | Floyd-Warshall |
| DAG | Topological relaxation |

---

# 30. Minimum Spanning Tree

For a connected weighted **undirected** graph, an MST:

- Connects all vertices
- Uses `V - 1` edges
- Contains no cycle
- Has minimum total weight

Applications:

- Cheapest network cabling
- Road planning
- Power distribution
- Site connectivity

## Kruskal's Algorithm

An algorithm is a finite, unambiguous procedure that converts an input into the required output. A useful explanation of an algorithm should state its preconditions, the main invariant or idea that keeps it correct, when it stops, and its time and space complexity.

1. Sort edges by weight.
2. Add the cheapest edge that does not create a cycle.
3. Use DSU to track components.

```text
Time: O(E log E)
```

## Prim's Algorithm

Prim's algorithm builds a minimum spanning tree by repeatedly adding the cheapest edge that connects the current tree to a new vertex. A min-priority queue efficiently selects the next candidate edge. With an adjacency list and binary heap, the common complexity is `O(E log V)`; the graph should be treated as weighted and undirected for the standard MST problem.

Grow the tree from one start node using a priority queue.

Typical:

```text
O(E log V)
```

---

# 31. Disjoint Set Union

Also called:

```text
Union-Find
```

Operations:

```text
find(x)
union(a, b)
```

```python
class DSU:
    def __init__(self, n):
        self.parent = list(range(n))
        self.rank = [0] * n

    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])

        return self.parent[x]

    def union(self, a, b):
        root_a = self.find(a)
        root_b = self.find(b)

        if root_a == root_b:
            return False

        if self.rank[root_a] < self.rank[root_b]:
            root_a, root_b = root_b, root_a

        self.parent[root_b] = root_a

        if self.rank[root_a] == self.rank[root_b]:
            self.rank[root_a] += 1

        return True
```

With path compression and union by rank/size:

```text
Amortized almost O(1)
```

More precisely:

```text
O(α(n))
```

Use cases:

- Kruskal MST
- Dynamic connectivity
- Friend groups
- Network components
- Cycle detection in undirected graphs

---

# 32. Strongly Connected Components

In a directed graph, an SCC is a maximal group where every node can reach every other node.

Algorithms:

- Kosaraju
- Tarjan

Applications:

- Dependency analysis
- Compiler graphs
- Deadlock-style reasoning
- Condensing a directed graph into a DAG

Kosaraju high-level process:

```text
1. DFS and record finishing order.
2. Reverse all edges.
3. Process vertices in reverse finishing order.
4. Each DFS tree is one SCC.
```

Complexity:

```text
O(V + E)
```

---

# 33. Greedy Algorithms

A greedy algorithm commits to a locally best-looking choice without revisiting earlier decisions. That can be very efficient, but it is correct only when the problem has a property that makes local choices compatible with a global optimum. A convincing greedy solution should include a justification such as an exchange argument, cut property, or invariant—not merely an intuition that the choice looks best.

A greedy algorithm chooses the locally best option at each step.

But greedy is only correct when that local choice can be **proven safe**.

## Activity Selection

For the classic maximum-number-of-non-overlapping-intervals problem, sorting by finishing time and repeatedly choosing the earliest finishing compatible interval is optimal. The greedy choice leaves as much room as possible for future intervals; sorting dominates at `O(n log n)`.

Problem:

> Attend the maximum number of non-overlapping meetings.

Correct greedy strategy:

```text
Always choose the meeting that finishes earliest.
```

```python
def max_meetings(intervals):
    intervals.sort(key=lambda item: item[1])

    count = 0
    previous_end = float("-inf")

    for start, end in intervals:
        if start >= previous_end:
            count += 1
            previous_end = end

    return count
```

## Common Greedy Problems

A greedy algorithm commits to a locally best-looking choice without revisiting earlier decisions. That can be very efficient, but it is correct only when the problem has a property that makes local choices compatible with a global optimum. A convincing greedy solution should include a justification such as an exchange argument, cut property, or invariant—not merely an intuition that the choice looks best.

- Activity selection
- Fractional knapsack
- Huffman coding
- Some scheduling problems
- Some jump problems
- Minimum spanning tree

## Greedy vs DP

A greedy algorithm commits to a locally best-looking choice without revisiting earlier decisions. That can be very efficient, but it is correct only when the problem has a property that makes local choices compatible with a global optimum. A convincing greedy solution should include a justification such as an exchange argument, cut property, or invariant—not merely an intuition that the choice looks best.

Greedy:

```text
Make one safe local choice and never revisit it.
```

DP:

```text
Compare multiple interacting alternatives because subproblems overlap.
```

Never use greedy only because it "looks obvious". Look for a correctness argument.

---

# 34. Dynamic Programming

Dynamic programming is useful when many candidate solutions reuse the same subproblems and the answer can be composed from smaller states. The core design work is to define the **state**, derive the **transition**, set correct **base cases**, and choose an evaluation order. Memoization computes states on demand; tabulation computes them in an explicit order.

Dynamic Programming is useful when a problem has:

1. Overlapping subproblems
2. Optimal substructure

Mental model:

```text
Solve each useful subproblem once.
Store the answer.
Reuse it.
```

## Naive Fibonacci

Naive recursive Fibonacci branches into two recursive calls and recomputes the same smaller values many times, causing exponential work. It is useful only to demonstrate overlapping subproblems; memoization or iteration reduces the number of distinct states to `O(n)`.

```python
def fib(n):
    if n <= 1:
        return n

    return fib(n - 1) + fib(n - 2)
```

This repeats the same work many times.

## Memoization — Top Down

Top-down DP starts from the requested state and recursively computes only states that are reached, caching each result. The memo key must fully identify a state, and recursion depth counts toward space usage.

```python
def fib(n, memo=None):
    if memo is None:
        memo = {}

    if n <= 1:
        return n

    if n not in memo:
        memo[n] = fib(n - 1, memo) + fib(n - 2, memo)

    return memo[n]
```

## Tabulation — Bottom Up

Bottom-up DP orders states so every dependency is already computed before a state is filled. It avoids recursion overhead and makes iteration order explicit, but may compute states that top-down memoization would never visit.

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

## Space Optimization

Space optimization removes DP states that are no longer needed. If `dp[i]` depends only on a fixed number of earlier rows/values, replace the full table with rolling variables or a small rolling array. Do this only after the full state transition is correct, because update order can accidentally overwrite a dependency.

```python
def fib(n):
    if n <= 1:
        return n

    previous2 = 0
    previous1 = 1

    for _ in range(2, n + 1):
        current = previous1 + previous2
        previous2 = previous1
        previous1 = current

    return previous1
```

```text
Space: O(1)
```

## DP Design Checklist

For every DP problem answer:

```text
1. What does dp[state] mean?
2. What choices exist?
3. What is the transition?
4. What are the base cases?
5. In what order are states evaluated?
6. Which state contains the answer?
7. Can memory be optimized?
```

If you cannot describe the state precisely, the DP is not yet clearly designed.

---

# 35. Important DP Patterns

DP patterns differ mainly in how the **state** is shaped: index, two indexes, capacity, interval, subset mask, grid cell, tree node, or digit position. For each pattern, write the state meaning as a sentence before the recurrence; this prevents many dimension and transition errors.

## Climbing Stairs

Climbing Stairs is a simple DP model: if the final move can be one or two steps, the number of ways to reach step `i` is the sum of the ways to reach `i-1` and `i-2`. Define base cases carefully; conventions for `n = 0` depend on whether 'do nothing' counts as one valid way.

If you may climb 1 or 2 steps:

```text
ways[n] = ways[n-1] + ways[n-2]
```

## 0/1 Knapsack

In 0/1 Knapsack each item can be selected at most once. A typical state combines item/index and remaining capacity; in 1D optimization, iterate capacities **downward** so the current item is not reused within the same iteration.

Each item can be used at most once.

A common state:

```text
dp[item_index][remaining_capacity]
```

Choices:

```text
Take item
Skip item
```

## Unbounded Knapsack

Unbounded knapsack allows an item to be selected more than once. In one-dimensional tabulation, the loop direction is important: iterating capacities upward allows the current item to contribute repeatedly to later states. This differs from 0/1 knapsack, where downward capacity iteration prevents reusing the same item in one iteration.

Items can be reused.

Examples:

- Coin Change
- Rod Cutting

## Coin Change — Minimum Coins

The minimum-coin problem asks for the fewest coins needed to form each amount. A common DP state stores the best answer for amount `x`; each coin proposes `1 + dp[x - coin]` when that smaller amount is reachable. Use a sentinel larger than any possible answer and distinguish 'unreachable' from a valid zero-coin base case.

```python
def coin_change(coins, amount):
    dp = [float("inf")] * (amount + 1)
    dp[0] = 0

    for current in range(1, amount + 1):
        for coin in coins:
            if coin <= current:
                dp[current] = min(
                    dp[current],
                    1 + dp[current - coin]
                )

    return -1 if dp[amount] == float("inf") else dp[amount]
```

## Longest Increasing Subsequence

The Longest Increasing Subsequence (LIS) keeps elements in original order but not necessarily contiguously. A simple DP is `O(n²)`; a tails/binary-search method maintains the smallest possible tail for each subsequence length and runs in `O(n log n)`. The tails array is not necessarily the actual LIS unless predecessor information is also stored.

Basic DP:

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

```text
Time: O(n²)
```

An optimized binary-search technique can achieve:

```text
O(n log n)
```

## Longest Common Subsequence

The Longest Common Subsequence (LCS) asks for the longest sequence that appears in two inputs in the same relative order, without requiring contiguity. A classic DP state `dp[i][j]` describes prefixes of the two sequences: matching symbols extend the answer; otherwise the transition skips one side. The standard table takes `O(mn)` time.

For:

```text
abcde
ace
```

the LCS is:

```text
ace
```

A common DP definition:

```text
dp[i][j] = LCS length using first i chars of A and first j chars of B
```

## Grid DP

Grid DP stores the best/count answer for each cell based on previously solved neighboring cells. The allowed movement determines the transition and valid evaluation order. When movement is only right/down, row-major or column-major tabulation is usually straightforward; if arbitrary cycles are allowed, the problem may be a graph problem rather than simple DP.

A typical transition for counting paths:

```text
dp[r][c] = dp[r-1][c] + dp[r][c-1]
```

## Edit Distance

Edit Distance measures the minimum inserts, deletes, and replacements needed to transform one string into another. A DP state over prefixes considers matching equal characters or taking one operation plus the best neighboring subproblem. Standard complexity is `O(mn)` time and `O(mn)` space before row optimization.

Operations:

- Insert
- Delete
- Replace

Uses:

- Spell correction concepts
- Diff tools
- Sequence similarity

## Interval DP

Interval DP defines a state over a contiguous range, commonly `dp[left][right]`, and combines answers from smaller subintervals. It appears in problems such as matrix-chain multiplication, optimal parenthesization, or bursting balloons. The challenge is choosing the interval length/order so every dependency has already been computed.

State describes a range:

```text
dp[left][right]
```

Examples:

- Matrix Chain Multiplication
- Burst Balloons
- Palindrome partitioning
- Interval games

## Tree DP

Tree DP computes a state for each node from states of its children (or from a rerooted parent/child relationship). A DFS usually establishes the processing order. Clearly define what each state means—for example, 'best answer in this subtree if the node is chosen'—because correctness depends on combining child states consistently.

State belongs to a tree node.

Examples:

- Tree diameter
- Maximum path sum
- Subtree values
- Rerooting problems

## Bitmask DP

Bits represent a subset of items.

Often useful when:

```text
n is small, roughly 15–22 depending on complexity
```

Examples:

- Traveling Salesman DP
- Assignment problems
- Visit-subset states

---

# 36. String-Matching Algorithms

String-matching algorithms search for one or more patterns inside text. Compare them by preprocessing cost, search complexity, memory, collision behavior, alphabet assumptions, and whether the same pattern or same text will be queried repeatedly.

## Naive Matching

Naive pattern matching tries the pattern at every possible text start and compares characters until mismatch. Worst-case time is `O(nm)`, but it is simple and often adequate for small inputs; KMP/Z avoid repeated comparisons when larger guarantees are needed.

Try the pattern at every possible starting position.

Worst-case:

```text
O(nm)
```

## KMP

Knuth-Morris-Pratt (KMP) searches for a pattern without rechecking characters that are already known to match. It preprocesses the pattern into a prefix/failure table, then uses that table to decide how far the pattern can shift after a mismatch. Preprocessing plus search runs in `O(m + n)` for pattern length `m` and text length `n`.

Knuth-Morris-Pratt avoids rechecking characters.

Uses:

```text
LPS = Longest Proper Prefix that is also a Suffix
```

Complexity:

```text
O(n + m)
```

## Rabin-Karp

Rabin-Karp compares rolling hash values for the pattern and each same-length text window. Updating the rolling hash can be constant-time per shift, making the average scan efficient and especially useful when searching many patterns or repeated windows. Because different strings can share a hash, a hash match should be verified when correctness cannot tolerate collisions.

Uses rolling hash.

Applications:

- Pattern matching
- Multiple substring comparisons
- Duplicate-string detection concepts

Hash collisions must be handled.

## Z Algorithm

The Z algorithm computes, for each position, the length of the longest substring starting there that matches the prefix of the whole string. By reusing a previously matched interval, it runs in linear time. A common pattern-search trick concatenates `pattern + separator + text` and looks for Z-values equal to the pattern length.

`Z[i]` stores the length of the longest prefix match beginning at index `i`.

```text
Time: O(n)
```

Useful for prefix-based pattern matching.

## Rolling Hash

After preprocessing, substring hashes can be compared efficiently.

Applications:

- Duplicate substring search
- String comparisons
- Pattern matching

Because hashes can collide, verification or multiple hashes may be used when correctness requires it.

---

# 37. Monotonic Stack and Queue

Monotonic stacks and queues maintain candidates in sorted order while processing a sequence. They turn many 'nearest greater/smaller' and sliding-window extrema problems into linear time because each element is inserted and removed only a constant number of times.

A monotonic structure maintains values in increasing or decreasing order while scanning.

## Next Greater Element

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

```text
Time: O(n)
```

Although a `while` appears inside a `for`, each index is pushed and popped at most once.

Common problems:

- Next Greater Element
- Next Smaller Element
- Daily Temperatures
- Stock Span
- Largest Rectangle in Histogram
- Trapping Rain Water variants

## Monotonic Queue

A monotonic queue, usually implemented with a deque, maintains candidates in sorted-by-value order while also expiring elements that leave a sliding range. It gives `O(n)` total processing for sliding-window maximum/minimum because each index enters and leaves the deque at most once.

Useful for sliding-window maximum/minimum.

Can reduce:

```text
O(nk)
```

to:

```text
O(n)
```

---

# 38. Intervals and Sweep Line

Interval problems represent ranges such as time spans, coordinates, or reservations. Before coding, define whether endpoints are inclusive or exclusive and whether touching intervals overlap; that decision controls sorting, merge conditions, sweep-line events, and off-by-one behavior.

Intervals occur in:

- Meetings
- Bookings
- Reservations
- Employee shifts
- CPU jobs
- Capacity planning

## Merge Intervals

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

```text
Time: O(n log n)
```

because sorting dominates.

## Sweep Line

Convert interval boundaries into events:

```text
start → +1
end   → -1
```

Sort events and sweep across time.

Applications:

- Maximum overlapping meetings
- Minimum number of rooms
- Peak active users
- Resource utilization
- Skyline problems

Important: whether start and end at the same coordinate overlap depends on problem semantics, so event ordering matters.

---

# 39. Segment Trees

A tree is a connected acyclic hierarchical structure with nodes linked by parent/child relationships. Tree algorithms are easiest to understand recursively: define what one subtree call returns, choose a traversal order, and account for tree height because recursion/operation cost can degrade on skewed trees.

Segment Trees support efficient dynamic range operations.

Typical complexity:

```text
Build:        O(n)
Point update: O(log n)
Range query:  O(log n)
Space:        O(n)
```

Typical operations:

- Range sum
- Range minimum
- Range maximum
- GCD

## Why not always use prefix sum?

A prefix sum precomputes cumulative totals so that later range sums can be answered by subtraction. With the common convention `prefix[i] = sum of elements before i`, the sum of the half-open range `[left, right)` is `prefix[right] - prefix[left]`. Building the prefix array costs `O(n)` time and each range query then costs `O(1)`.

Prefix sum:

```text
Query:  O(1)
Update: O(n)
```

Segment Tree:

```text
Query:  O(log n)
Update: O(log n)
```

If data changes often and queries are frequent, a Segment Tree becomes useful.

## Lazy Propagation

Used for range updates.

Example:

```text
Add 5 to every value from L to R.
```

Lazy propagation stores deferred work instead of visiting every leaf immediately.

---

# 40. Fenwick Trees

Also called:

```text
Binary Indexed Tree (BIT)
```

Useful for dynamic prefix aggregates.

Typical:

```text
Point update: O(log n)
Prefix sum:   O(log n)
Range sum:    O(log n)
Space:        O(n)
```

Common uses:

- Dynamic prefix sums
- Inversion counting
- Frequency tables
- Online cumulative counts

Prefer a Fenwick Tree over a Segment Tree when its simpler operation set is sufficient.

---

# 41. Quickselect and Selection

Suppose you need only the kth smallest or kth largest value.

Full sorting:

```text
O(n log n)
```

Quickselect uses partitioning similar to Quick Sort.

Typical complexity:

```text
Average: O(n)
Worst:   O(n²)
```

## Choosing a kth-element strategy

The best kth-element method depends on whether you need one rank or repeated ranks, whether mutation is allowed, and whether worst-case guarantees matter. Full sort is simplest (`O(n log n)`), a heap is `O(n log k)`, and Quickselect is `O(n)` average but `O(n²)` worst case without stronger pivot selection.

### Sorting

Sorting all values is often the simplest selection baseline. It is appropriate when ordered output is useful elsewhere or input size is moderate; it does unnecessary work when only one rank is needed and no other sorted-order benefit exists.

```text
O(n log n)
```

Simple and good for moderate input.

### Heap

A heap is a partially ordered tree structure commonly used to implement a priority queue. A min-heap exposes the smallest item; a max-heap exposes the largest. Insert and removal of the root are typically `O(log n)`, while reading the root is `O(1)`, making heaps ideal for top-k, scheduling, streaming minima/maxima, and graph algorithms such as Dijkstra or Prim.

```text
O(n log k)
```

Great when `k` is small or data arrives as a stream.

### Quickselect

Quickselect partitions around a pivot like Quicksort but continues only into the side containing the desired rank. Expected time is `O(n)` with randomized/good pivots, worst-case `O(n²)`, and it normally mutates the input unless implemented on a copy.

```text
Average O(n)
```

Excellent when only one order statistic is needed.

---

# 42. Core Problem-Solving Patterns

Problem-solving patterns are reusable ways to remove repeated work. Treat each pattern as a clue-to-invariant mapping: identify the input structure, state what must remain true while the algorithm runs, and only then choose pointer movements, data structures, or transitions.

This section is more important than memorizing isolated problems.

## Pattern 1 — Frequency Map

A frequency map stores `value → count`. Scan the input once, incrementing the count for each value; later frequency queries are average `O(1)` with a hash map. This pattern is useful for duplicates, anagrams, counting categories, majority/frequency problems, and many sliding-window algorithms.

Clues:

```text
count
duplicate
anagram
frequency
most common
```

Use:

```text
Hash Map / Counter
```

## Pattern 2 — Two Pointers

Two pointers maintain two indexes or references whose movement eliminates unnecessary repeated work. Common forms are opposite-end pointers on sorted data and same-direction read/write pointers for in-place filtering. The technique is most valuable when pointer movement can be justified by an invariant, such as sorted order or a maintained valid region.

Clues:

```text
sorted
pair
palindrome
merge
remove duplicates
```

## Pattern 3 — Sliding Window

A sliding window tracks a contiguous range while updating only the information that changes when the range expands or shrinks. Fixed-size windows are used when the length is known; variable-size windows adjust a boundary until a validity condition is restored. The usual goal is to replace repeated recomputation of every subarray or substring with a single linear pass.

Clues:

```text
contiguous
substring
subarray
longest/shortest range
at most K
```

## Pattern 4 — Fast/Slow Pointers

Think of **fast/slow pointers** as a recognition pattern rather than a memorized solution. The clues below suggest that the technique may remove repeated work; confirm its preconditions and maintain an invariant that explains why pointer/state updates are safe.

Clues:

```text
cycle
middle
linked list
repeated state
```

## Pattern 5 — Prefix Sum

A prefix sum precomputes cumulative totals so that later range sums can be answered by subtraction. With the common convention `prefix[i] = sum of elements before i`, the sum of the half-open range `[left, right)` is `prefix[right] - prefix[left]`. Building the prefix array costs `O(n)` time and each range query then costs `O(1)`.

Clues:

```text
range sum
many range queries
subarray sum
cumulative
```

## Pattern 6 — Binary Search

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

Clues:

```text
sorted
monotonic
minimum feasible
maximum feasible
```

## Pattern 7 — Heap

A heap is a partially ordered tree structure commonly used to implement a priority queue. A min-heap exposes the smallest item; a max-heap exposes the largest. Insert and removal of the root are typically `O(log n)`, while reading the root is `O(1)`, making heaps ideal for top-k, scheduling, streaming minima/maxima, and graph algorithms such as Dijkstra or Prim.

Clues:

```text
top K
priority
kth
closest
repeated minimum/maximum
```

## Pattern 8 — BFS

Breadth-first search explores a graph or tree level by level using a queue. In an unweighted graph, the first time BFS reaches a vertex is through a path with the minimum number of edges from the start. With adjacency-list representation, a complete traversal is `O(V + E)` when each vertex is processed once.

Clues:

```text
minimum moves
unweighted shortest path
level
nearest
```

## Pattern 9 — DFS

Depth-first search explores one branch as far as possible before returning to try another branch. It can be implemented recursively or with an explicit stack and is widely used for connected components, cycle detection, tree processing, path exploration, topological reasoning, and many backtracking-style searches. Track visited state in cyclic graphs to avoid endless revisits.

Clues:

```text
connected components
explore region
islands
tree recursion
```

## Pattern 10 — Backtracking

Backtracking explores a decision tree by making a choice, recursively exploring what follows, and then undoing that choice before trying the next option. It is appropriate when the task asks for all valid combinations, permutations, placements, paths, or constraint-satisfying configurations. Pruning impossible branches early is often the difference between a practical and an impractical solution.

Clues:

```text
generate all
combinations
permutations
valid arrangements
```

## Pattern 11 — Dynamic Programming

Dynamic programming is useful when many candidate solutions reuse the same subproblems and the answer can be composed from smaller states. The core design work is to define the **state**, derive the **transition**, set correct **base cases**, and choose an evaluation order. Memoization computes states on demand; tabulation computes them in an explicit order.

Clues:

```text
number of ways
minimum cost
maximum value
repeated choices
overlapping subproblems
```

## Pattern 12 — Greedy

A greedy algorithm commits to a locally best-looking choice without revisiting earlier decisions. That can be very efficient, but it is correct only when the problem has a property that makes local choices compatible with a global optimum. A convincing greedy solution should include a justification such as an exchange argument, cut property, or invariant—not merely an intuition that the choice looks best.

Clues:

```text
schedule
earliest finish
minimum resources
provably safe local choice
```

## Pattern 13 — Monotonic Stack

A monotonic stack keeps its elements in increasing or decreasing order by removing values that can no longer be useful. Each element is pushed and popped at most once, so many nearest-greater/nearest-smaller problems become `O(n)`. The crucial design decision is whether the stack stores values or indexes and which comparison preserves the needed candidate boundary.

Clues:

```text
next greater
next smaller
nearest greater
histogram
temperature
```

## Pattern 14 — DSU

Think of **dsu** as a recognition pattern rather than a memorized solution. The clues below suggest that the technique may remove repeated work; confirm its preconditions and maintain an invariant that explains why pointer/state updates are safe.

Clues:

```text
groups
same component
dynamic connectivity
undirected cycle
```

## Pattern 15 — Topological Sort

A topological ordering places every prerequisite before the items that depend on it. It exists only for a **directed acyclic graph (DAG)**. Common implementations use Kahn's algorithm with indegrees and a queue, or DFS with postorder; if all vertices cannot be ordered, the dependency graph contains a cycle.

Clues:

```text
prerequisites
dependencies
before/after constraints
```

## Pattern 16 — Trie

A trie stores keys by shared prefixes. Each step consumes one symbol, so lookup time depends mainly on key length rather than on the number of stored keys. Tries are useful for autocomplete, prefix counting, dictionary search, and word-grid problems, but they can use substantially more memory than a hash-based set or map.

Clues:

```text
prefix
dictionary
autocomplete
many words
```

## Pattern 17 — Segment/Fenwick Tree

Think of **segment/fenwick tree** as a recognition pattern rather than a memorized solution. The clues below suggest that the technique may remove repeated work; confirm its preconditions and maintain an invariant that explains why pointer/state updates are safe.

Clues:

```text
many range queries
frequent updates
online dynamic data
```

---

# 43. Real-World Use Cases

Real systems use DSA through the operations they need: fast lookup, ordering, scheduling, routing, deduplication, top-k retrieval, dependency resolution, or range aggregation. The useful habit is to translate the business requirement into required operations and then choose the structure that makes those operations efficient.

DSA is not only for interviews.

## Search Autocomplete

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

Possible structures:

```text
Trie
Frequency Map
Heap
```

1. Trie finds prefix candidates.
2. Frequency data scores popularity.
3. Heap selects top suggestions.

## GPS Navigation

Road networks are weighted graphs: intersections are vertices and roads are edges with distance/time costs. Dijkstra works for non-negative costs; A* can accelerate point-to-point search with an admissible heuristic. Real routing also needs turn restrictions and dynamic weights.

Model:

```text
Intersection = Vertex
Road         = Edge
Travel time  = Weight
```

Algorithms:

- Dijkstra
- A* in many practical pathfinding systems

## Social Network

A social network is naturally a graph where people are vertices and relationships are edges. BFS/DFS support reachability and degrees of separation, while sets/maps support neighbor membership; large-scale recommendations often require more specialized ranking/indexing beyond basic traversal.

```text
User       = Vertex
Friendship = Edge
```

Tasks:

- Mutual friends → Sets
- Connection distance → BFS
- Connected communities → DFS/DSU
- Recommendations → Graph algorithms

## Browser Back Button

Back navigation is naturally LIFO: the most recently visited prior page should be returned first. A stack models this directly; real browser forward navigation typically needs a second stack or indexed history state.

```text
Stack
```

## Print/Job Queue

A queue follows **First In, First Out (FIFO)** order: the earliest enqueued item is processed first. The key operations are enqueue, dequeue, front/peek, and emptiness checking. Queues are a natural fit for breadth-first search, scheduling, buffering, and any workflow that must preserve arrival order.

```text
Queue
```

## Priority Scheduler

A priority queue returns the next highest/lowest-priority job efficiently. Insert and remove-best are typically `O(log n)`, making it appropriate when priorities change the processing order rather than simple FIFO arrival.

```text
Heap / Priority Queue
```

## File System

A file system namespace is hierarchical and is commonly modeled as a tree: directories contain child files/directories. Tree traversal supports recursive listing, size aggregation, and search; links/mounts can introduce graph-like behavior in real systems.

```text
Tree
```

## Database Indexing

Balanced search trees/B-trees are common indexing structures because they keep search paths shallow and support ordered/range access. Hash indexes favor equality lookup. The DSA lesson is to match the index structure to the query operations, not to assume one index type is universally best.

Common related structures:

```text
B-tree
B+ tree
Hash index
```

## Dependency Management

Dependencies form a directed graph from a prerequisite to a dependent item (or the reverse by convention). A topological ordering gives a valid execution/build order when the graph is acyclic; a cycle means the prerequisites cannot all be satisfied in a linear order.

```text
Directed Graph
Topological Sort
Cycle Detection
```

## Calendar Scheduling

Bookings are intervals on a time axis. Sorting, overlap checks, sweep lines, heaps, or interval trees can answer different questions such as merge bookings, detect conflicts, count simultaneous rooms, or support dynamic inserts.

```text
Intervals
Sorting
Sweep Line
Heap
```

## Cheapest Network Connection

The code below is a concrete example of **Cheapest Network Connection**. Read it by identifying the input/state first, then trace each mutation or decision until the produced value/output. When reusing the pattern, preserve its required preconditions and include the cost of nested library operations in the complexity analysis.

```text
MST
Kruskal
Prim
```

---

# 44. Interview Problem-Solving Framework

An interview framework makes your reasoning visible: clarify inputs and constraints, establish a brute-force baseline, identify repeated work, choose a pattern, justify correctness, analyze complexity, implement clearly, and test edge cases. The explanation is part of the solution, not an extra step after coding.

Use this sequence during interviews.

## 1. Restate the problem

Restate the task in your own words, naming the input, required output, and success condition. This catches misunderstandings before implementation starts.

Explain what must be returned in your own words.

## 2. Clarify assumptions

Clarify assumptions that can change correctness or complexity: empty input, duplicates, negative values, input size, whether mutation is allowed, and whether multiple valid answers may exist.

Ask about:

```text
empty input
duplicates
negative values
input size
mutation
multiple answers
```

## 3. Describe brute force

State a simple correct approach first. Its purpose is to establish a baseline and reveal which repeated operation is making the solution slow.

A correct slow solution shows that you understand the problem.

## 4. Identify the bottleneck

Name the exact repeated work responsible for the brute-force cost—for example repeated membership search, repeated range summation, or exploring the same state many times.

Example:

```text
We repeatedly scan for the complement.
```

## 5. Optimize

Replace the bottleneck with a data structure, precomputation, ordering, or algorithmic pattern. Explain the invariant that makes the optimized step valid rather than naming a pattern alone.

Example:

```text
Store seen values in a hash map.
```

## 6. State complexity before coding

State the expected time and auxiliary-space complexity before implementation. This creates a target you can verify against the final code, including library operations used inside loops.

Example:

```text
Time:  O(n)
Space: O(n)
```

## 7. Write clear code

Implement with descriptive state names and a structure that mirrors the explanation. Avoid compressing steps when that hides the algorithm's invariant or edge-case handling.

Prefer descriptive names:

```python
left
right
current_sum
frequency
distance
```

## 8. Dry run

Trace the code on a small concrete input, recording how the important pointers, queue/stack contents, DP state, or graph-visited state changes after each step.

Trace a normal example.

## 9. Test edge cases

Before finishing, test the smallest valid input, boundaries, duplicates, absent targets, extreme values, and structure-specific cases such as disconnected graphs or skewed trees when relevant.

Typical cases:

```text
empty input
one element
all equal
all distinct
duplicates
already sorted
reverse sorted
negative values
answer at boundary
```

---

# 45. Common Mistakes and Debugging

DSA bugs are often caused by incorrect boundaries, stale state, missing visited checks, wrong base cases, or an invariant that was never made explicit. Debug by reducing the input, tracing state changes line by line, and checking the first point where the program diverges from the expected invariant.

## Off-by-one errors

Off-by-one bugs happen when an endpoint is included/excluded incorrectly. Write the interval convention explicitly—such as `[left, right]` or `[left, right)`—and test empty, one-element, and boundary-position cases before trusting the loop.

Bad:

```python
for i in range(len(nums) + 1):
    print(nums[i])
```

Correct:

```python
for i in range(len(nums)):
    print(nums[i])
```

## Empty-input assumptions

Algorithms that immediately read the first element or root need an explicit empty-input contract. Either handle the empty case early or document that the caller guarantees non-empty input; otherwise initialization can fail before the core algorithm begins.

This fails on an empty array:

```python
maximum = nums[0]
```

Handle empty input if allowed.

## Binary search boundaries never move

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

Classic inclusive-boundary binary search must make progress:

```python
left = mid + 1
```

or:

```python
right = mid - 1
```

## Marking BFS nodes visited too late

Breadth-first search explores a graph or tree level by level using a queue. In an unweighted graph, the first time BFS reaches a vertex is through a path with the minimum number of edges from the start. With adjacency-list representation, a complete traversal is `O(V + E)` when each vertex is processed once.

Usually mark when **enqueuing** to prevent duplicates.

## Forgetting backtracking undo

Backtracking explores a decision tree by making a choice, recursively exploring what follows, and then undoing that choice before trying the next option. It is appropriate when the task asks for all valid combinations, permutations, placements, paths, or constraint-satisfying configurations. Pruning impossible branches early is often the difference between a practical and an impractical solution.

```python
current.append(choice)
backtrack(...)
current.pop()
```

The undo step is essential.

## Vague DP state

A DP state must be a sentence precise enough to determine its dimensions and transitions, for example: “`dp[i]` is the minimum cost to finish the first `i` items.” If you cannot state exactly what a cell means, recurrence and base-case bugs are likely.

You should be able to say:

```text
dp[i] means ...
```

in one exact sentence.

## Dijkstra with negative edges

Dijkstra relies on non-negative edge weights; a later negative edge can invalidate a distance that was treated as final. Use Bellman-Ford for general negative edges (and cycle detection), or exploit DAG order when the graph is acyclic.

Ordinary Dijkstra assumes non-negative weights.

## Sliding window with negative values

A sliding window tracks a contiguous range while updating only the information that changes when the range expands or shrinks. Fixed-size windows are used when the length is known; variable-size windows adjust a boundary until a validity condition is restored. The usual goal is to replace repeated recomputation of every subarray or substring with a single linear pass.

Some sum-based sliding-window approaches require monotonic behavior that negative values destroy.

## Integer overflow

Fixed-width integer arithmetic can wrap when a sum, difference, or product exceeds the type's range. Promote operands **before** the risky operation (for example to `long`) and check problem constraints rather than casting only after overflow has already occurred.

In fixed-width languages such as Java/C++, use an appropriate integer type for large sums and products.

## Accidental input mutation

A graph/grid solution may change input:

```python
grid[r][c] = "0"
```

If callers require the original data, use a separate visited structure.

## Debugging Checklist

1. Test the smallest possible input.
2. Test empty input.
3. Test one item.
4. Test duplicates.
5. Trace pointers/indices.
6. Check loop invariants.
7. Check base cases.
8. Inspect state after mutation.
9. Dry-run manually.
10. Only optimize after correctness is established.

---

# 46. Complexity Cheat Sheet

Use a complexity cheat sheet to recall typical costs, then verify the exact implementation being used. 'Hash lookup is `O(1)`' means average/expected behavior under normal hashing assumptions; a tree or language-specific container may have different guarantees.

## Data Structures

| Data Structure | Access | Search | Insert | Delete |
|---|---:|---:|---:|---:|
| Array | O(1) | O(n) | O(n) middle | O(n) middle |
| Dynamic array append | — | — | Amortized O(1) | — |
| Linked List | O(n) | O(n) | O(1)* | O(1)* |
| Hash Table | — | Avg O(1) | Avg O(1) | Avg O(1) |
| Balanced BST | O(log n) | O(log n) | O(log n) | O(log n) |
| Heap | — | O(n) general | O(log n) | O(log n) top |
| Trie | — | O(L) | O(L) | O(L) |

`*` when the correct node/reference is already known.

## Algorithms

| Algorithm | Complexity |
|---|---:|
| Linear Search | O(n) |
| Binary Search | O(log n) |
| Bubble Sort | O(n²) |
| Selection Sort | O(n²) |
| Insertion Sort | O(n²) worst |
| Merge Sort | O(n log n) |
| Heap Sort | O(n log n) |
| Quick Sort | O(n log n) average |
| BFS | O(V + E) |
| DFS | O(V + E) |
| Topological Sort | O(V + E) |
| Dijkstra + heap | O((V + E) log V) |
| Bellman-Ford | O(VE) |
| Floyd-Warshall | O(V³) |
| Kruskal | O(E log E) |
| KMP | O(n + m) |
| Sieve | O(n log log n) |
| Fenwick update/query | O(log n) |
| Segment Tree update/query | O(log n) |

## Input-Size Intuition

Approximate only:

```text
n <= 10
    factorial approaches may sometimes work

n <= 20–25
    O(2^n) may sometimes work

n <= 1,000
    O(n²) may be acceptable depending on environment

n <= 100,000
    usually aim for O(n log n) or O(n)

n >= 1,000,000
    usually need near-linear work
```

Actual limits depend on:

- Language
- Hardware
- Constant factors
- Number of test cases
- Memory limits

---

# 47. DSA Learning Roadmap

A learning roadmap should progress from basic containers and complexity to reusable patterns, trees/graphs, and advanced techniques. Advance when you can derive and explain a solution without copying, not merely when you have completed a fixed number of exercises.

## Stage 1 — Foundation

Learn:

- Arrays
- Strings
- Complexity
- Basic math
- Bit basics

Practice:

- Maximum/minimum
- Reverse array/string
- Palindrome
- Frequency counting
- Missing number

## Stage 2 — Core Structures

Learn:

- Linked List
- Stack
- Queue
- Hash Map
- Set

Practice:

- Two Sum
- Valid Parentheses
- Reverse Linked List
- Middle Node
- Cycle Detection
- Duplicate Detection

## Stage 3 — Core Patterns

Learn:

- Two Pointers
- Sliding Window
- Prefix Sum
- Binary Search

Practice:

- Pair Sum
- 3Sum
- Longest Unique Substring
- Range Sum
- Search Rotated Array
- Binary Search on Answer

## Stage 4 — Recursion and Backtracking

Backtracking explores a decision tree by making a choice, recursively exploring what follows, and then undoing that choice before trying the next option. It is appropriate when the task asks for all valid combinations, permutations, placements, paths, or constraint-satisfying configurations. Pruning impossible branches early is often the difference between a practical and an impractical solution.

Learn:

- Recursion tree
- Base cases
- Choice/explore/undo
- Divide and conquer

Practice:

- Subsets
- Permutations
- Combination Sum
- Generate Parentheses
- N-Queens

## Stage 5 — Trees and Heaps

Learn:

- Tree traversals
- BST
- Height/diameter
- Heap
- Trie

Practice:

- Tree depth
- Validate BST
- Lowest common ancestor
- Top K
- Prefix autocomplete

## Stage 6 — Graphs

A graph models entities as vertices and relationships as edges. Before choosing an algorithm, determine whether the graph is directed or undirected, weighted or unweighted, cyclic or acyclic, and connected or disconnected. Those properties decide whether BFS, DFS, topological sorting, shortest-path algorithms, minimum-spanning-tree algorithms, or connectivity structures are appropriate.

Learn:

- Representations
- BFS
- DFS
- Components
- Cycle detection
- Topological sort
- Dijkstra
- DSU
- MST

Practice:

- Number of Islands
- Course Schedule
- Network Delay
- Connected Components
- Redundant Connection

## Stage 7 — Greedy and DP

A greedy algorithm commits to a locally best-looking choice without revisiting earlier decisions. That can be very efficient, but it is correct only when the problem has a property that makes local choices compatible with a global optimum. A convincing greedy solution should include a justification such as an exchange argument, cut property, or invariant—not merely an intuition that the choice looks best.

Learn:

- Greedy proof intuition
- Memoization
- Tabulation
- Knapsack
- LIS
- LCS
- Grid DP
- Interval DP

Practice:

- Climbing Stairs
- House Robber
- Coin Change
- LCS
- Partition problems
- Activity scheduling

## Stage 8 — Advanced

These items combine or extend core patterns. Add them only after the prerequisite structure is comfortable; for each one, learn the invariant and complexity rather than memorizing a finished template.

Learn when needed:

- Monotonic stack/queue
- Segment Tree
- Fenwick Tree
- SCC
- Advanced string algorithms
- Sweep Line
- Bitmask DP
- Tree DP

---

# 48. Practice Problem Ladder

A problem ladder increases difficulty by changing one dimension at a time—larger constraints, less obvious patterns, combined techniques, or stricter space requirements. Move upward only after you can explain and re-implement the previous level without relying on memorized code.

## Beginner

Solve problems such as:

- Find maximum
- Find second largest
- Reverse array
- Reverse string
- Palindrome
- Frequency counting
- Missing number
- Move zeroes
- Merge sorted arrays
- Binary search

Target:

```text
20–30 problems
```

## Easy Pattern Problems

- Two Sum
- Valid Anagram
- Contains Duplicate
- Best Time to Buy/Sell Stock
- Maximum Subarray
- Valid Parentheses
- Linked List Cycle
- Middle of Linked List
- Merge Two Sorted Lists
- Flood Fill

Target total:

```text
40–60 problems
```

## Medium

- Longest Substring Without Repeating
- 3Sum
- Product of Array Except Self
- Search in Rotated Sorted Array
- Group Anagrams
- Top K Frequent Elements
- Kth Largest
- Number of Islands
- Course Schedule
- Combination Sum
- Generate Parentheses
- Coin Change
- House Robber
- Longest Increasing Subsequence
- Longest Common Subsequence
- Merge Intervals

Target total:

```text
80–120 quality problems
```

## Advanced Interview

- Trapping Rain Water
- Largest Rectangle in Histogram
- LRU Cache
- Merge K Sorted Lists
- Serialize/Deserialize Binary Tree
- Word Ladder
- Alien Dictionary
- Network Delay Time
- Edit Distance
- Word Break
- Minimum Window Substring
- Median of Two Sorted Arrays
- Advanced binary-search-on-answer problems

Target total:

```text
150–200 carefully reviewed problems
```

Do not chase count blindly. After every problem, record:

```text
Pattern
Brute force
Optimization
Time
Space
Mistake
Recognition clue
```

---

# 49. 30-Day Revision Plan

This revision plan is a pacing framework, not a guarantee of mastery in thirty days. Use spaced repetition: re-derive old techniques, retry failed problems without notes, and mix topics so recognition comes from the problem rather than from the day's label.

## Days 1–3

Use this schedule as a pacing guide rather than a strict quota. If a topic still feels mechanical, spend additional time tracing examples and re-solving mistakes before increasing difficulty.

```text
Complexity
Arrays
Strings
Hashing
```

## Days 4–6

Use this schedule as a pacing guide rather than a strict quota. If a topic still feels mechanical, spend additional time tracing examples and re-solving mistakes before increasing difficulty.

```text
Linked Lists
Stacks
Queues
```

## Days 7–10

Use this schedule as a pacing guide rather than a strict quota. If a topic still feels mechanical, spend additional time tracing examples and re-solving mistakes before increasing difficulty.

```text
Two Pointers
Sliding Window
Prefix Sum
Binary Search
```

## Days 11–13

Use this schedule as a pacing guide rather than a strict quota. If a topic still feels mechanical, spend additional time tracing examples and re-solving mistakes before increasing difficulty.

```text
Recursion
Backtracking
```

## Days 14–17

Use this schedule as a pacing guide rather than a strict quota. If a topic still feels mechanical, spend additional time tracing examples and re-solving mistakes before increasing difficulty.

```text
Trees
BST
Heap
Trie
```

## Days 18–21

Use this schedule as a pacing guide rather than a strict quota. If a topic still feels mechanical, spend additional time tracing examples and re-solving mistakes before increasing difficulty.

```text
Graphs
BFS
DFS
Topological Sort
```

## Days 22–24

Use this schedule as a pacing guide rather than a strict quota. If a topic still feels mechanical, spend additional time tracing examples and re-solving mistakes before increasing difficulty.

```text
Dijkstra
DSU
MST
```

## Days 25–27

Use this schedule as a pacing guide rather than a strict quota. If a topic still feels mechanical, spend additional time tracing examples and re-solving mistakes before increasing difficulty.

```text
Greedy
Dynamic Programming
```

## Days 28–29

Use this schedule as a pacing guide rather than a strict quota. If a topic still feels mechanical, spend additional time tracing examples and re-solving mistakes before increasing difficulty.

```text
Monotonic Stack
Intervals
Advanced Range Structures
```

## Day 30

Treat this block as focused revision. Re-derive at least one implementation from memory, solve a fresh problem, and retry one earlier mistake so the topic is reinforced through recall rather than rereading.

Simulate an interview:

```text
1 array/string problem
1 tree/graph problem
1 DP/greedy problem
```

For each answer explain:

```text
Brute force
Optimization
Correctness idea
Time
Space
Edge cases
```

---

# 50. Glossary

The glossary defines terms in compact form for revision. When a term affects algorithm choice—such as stable sort, DAG, subarray, subsequence, or amortized complexity—connect the definition to the property it guarantees, not just the vocabulary.

## Algorithm

An algorithm is a finite, unambiguous procedure that converts an input into the required output. A useful explanation of an algorithm should state its preconditions, the main invariant or idea that keeps it correct, when it stops, and its time and space complexity.
A finite procedure for solving a problem.

## Data Structure

A data structure is the organization chosen for data because that organization makes some operations cheaper than others. When selecting one, ask which operations must be fast—indexing, insertion, deletion, lookup, ordering, minimum/maximum retrieval, or relationship traversal—and what memory trade-off is acceptable.
A method for organizing and storing data.

## Node

A custom node class groups the value stored at one position with references to neighboring nodes. The exact fields depend on the structure—for example, `next` for a singly linked list and `left`/`right` for a binary tree. Algorithms usually pass or return node references rather than copying whole structures.
An individual element in a linked structure such as a linked list, tree, or graph.

## Edge

An **edge** represents a relationship between vertices. It may be directed or undirected and can carry data such as weight, capacity, label, or cost; those properties determine which graph algorithms are valid.
A connection between graph vertices.

## Vertex

A **vertex** (node) is an entity in a graph. Vertices are usually identified by an index/key and connected through edges; algorithm complexity often uses `V` for the number of vertices.
A graph node.

## Root

The **root** is the distinguished top node of a rooted tree. It has no parent, and traversal/depth relationships are commonly defined relative to it.
Topmost node of a tree.

## Leaf

A **leaf** is a tree node with no children. Leaf handling often forms a natural base case for recursion, subtree aggregation, or path problems.
A tree node with no children.

## Depth

A node's **depth** is its distance from the root under the chosen convention, commonly measured in edges (root depth `0`). Some educational texts count nodes instead, so define the convention when it matters.
Distance from the root to a node.

## Height

A node's **height** is the length of the longest downward path from that node to a leaf, under the chosen edge/node convention. Tree operation complexity is often expressed in terms of overall tree height `h`.
Longest downward path from a node to a leaf.

## Cycle

A **cycle** is a path that returns to a previously visited vertex according to the graph's direction rules. Cycle detection differs between directed and undirected graphs because the immediate parent edge is expected in an undirected traversal.
A path that returns to a previously visited node under the relevant graph interpretation.

## DAG

A **DAG (Directed Acyclic Graph)** is a directed graph with no directed cycle. Because no dependency can lead back to itself, DAGs are central to prerequisite scheduling, build pipelines, dependency resolution, and dynamic programming over topological order.
Directed Acyclic Graph.

## Connected Component

A **connected component** is a maximal group of vertices in an undirected graph where every pair is connected by some path. A full BFS/DFS from each still-unvisited vertex can label or count components in `O(V + E)` time.
A maximal group of connected vertices in an undirected graph.

## Subarray

A **subarray** is a contiguous slice of an array. For example, `[2, 3]` is a subarray of `[1, 2, 3, 4]`, while `[1, 3]` is not because it skips an element.
A contiguous part of an array.

## Substring

A **substring** is a contiguous portion of a string. For example, `"cat"` is a substring of `"educate"` only if those characters appear consecutively in that order.
A contiguous part of a string.

## Subsequence

A **subsequence** keeps the original relative order but may skip elements. For example, `[1, 3, 5]` is a subsequence of `[1, 2, 3, 4, 5]` even though it is not contiguous.
A selection preserving relative order but allowing skipped positions.

## Subset

A **subset** is any selection of elements from a set; unlike a subsequence, order and original positions are not the defining property. A set of `n` distinct elements has `2^n` subsets, including the empty set.
A selection of elements without a contiguous/order requirement inherent to the mathematical set.

## Stable Sort

A **stable sort** preserves the original relative order of records whose sort keys compare equal. This matters when data is sorted by multiple fields in stages, because a later stable sort does not destroy earlier ordering among ties.
A sort that preserves the relative order of equal keys.

## In-place

An **in-place** algorithm performs its main transformation in the original data structure while using only a small amount of extra storage, commonly `O(1)` auxiliary space. This does not mean the algorithm uses literally zero memory.
Uses only a small amount of additional storage compared with the input.

## Amortized Complexity

Amortized analysis spreads the cost of occasional expensive operations over a long sequence of operations. For example, a dynamic array resize may cost `O(n)`, but because resizing is infrequent, repeated append operations can still have `O(1)` amortized cost. Amortized complexity is a sequence-level guarantee; it does not mean every individual operation is constant-time.
Average operation cost over a sequence of operations.

## Memoization

Memoization caches a function's result by state so repeated calls return immediately. In Python, a dictionary or `functools.cache/lru_cache` can be used when arguments are hashable. Include all state-changing parameters in the cache key.
Top-down caching of subproblem results.

## Tabulation

Tabulation computes DP states iteratively from base cases toward the target. The table shape and iteration order must ensure every referenced dependency is already computed; this often avoids recursion-depth limits.
Bottom-up dynamic programming.

## Relaxation

**Relaxation** is the shortest-path operation that asks whether reaching `v` through `u` gives a better known distance. If `dist[u] + weight(u, v)` is smaller than `dist[v]`, the algorithm updates `dist[v]`; repeated relaxations are the core of Dijkstra and Bellman–Ford.
Trying to improve a graph distance:

```text
dist[v] = min(dist[v], dist[u] + weight(u, v))
```

## Invariant
A condition that remains true while an algorithm runs.

Examples:

- Binary search keeps the answer inside the active search interval.
- Insertion sort keeps the processed prefix sorted.
- Sliding window maintains the chosen validity rule for the current window.

---

# 51. Advanced Topics

Advanced topics are most useful after core patterns are comfortable because they combine multiple invariants and trade-offs. Study them when your target problems actually require stronger range queries, string indexing, graph decomposition, probabilistic reasoning, or specialized data structures.

After the core handbook is comfortable, continue with these topics as needed.

## Advanced Trees

These items combine or extend core patterns. Add them only after the prerequisite structure is comfortable; for each one, learn the invariant and complexity rather than memorizing a finished template.

- AVL Tree
- Red-Black Tree
- B-tree / B+ Tree
- Sparse Table
- Binary Lifting
- Lowest Common Ancestor
- Heavy-Light Decomposition

## Advanced Graphs

These items combine or extend core patterns. Add them only after the prerequisite structure is comfortable; for each one, learn the invariant and complexity rather than memorizing a finished template.

- Tarjan SCC
- Bridges
- Articulation Points
- A* Search
- Max Flow
- Min Cut
- Bipartite Matching
- Eulerian Paths
- Hamiltonian concepts

## Advanced Dynamic Programming

These items combine or extend core patterns. Add them only after the prerequisite structure is comfortable; for each one, learn the invariant and complexity rather than memorizing a finished template.

- Bitmask DP
- Digit DP
- Tree DP
- Rerooting DP
- DP on DAG
- Divide-and-conquer DP optimization
- Knuth optimization concepts

## Advanced Strings

These items combine or extend core patterns. Add them only after the prerequisite structure is comfortable; for each one, learn the invariant and complexity rather than memorizing a finished template.

- Suffix Array
- Suffix Tree
- Suffix Automaton
- Rolling Hash
- Manacher's Algorithm
- Aho-Corasick

## Computational Geometry

**Computational geometry** applies algorithms to points, lines, polygons, and spatial relationships. Common DSA topics include orientation/cross-product tests, line-segment intersection, convex hulls, sweep-line methods, and closest-pair problems.

- Orientation
- Segment intersection
- Convex Hull
- Sweep-line geometry
- Closest Pair

## Other Important Topics

- Meet in the Middle
- Randomized Algorithms
- Reservoir Sampling
- Bloom Filters
- Skip Lists
- LRU/LFU Cache Design
- Consistent Hashing concepts
- Game Theory
- Probability for Algorithms

Not all of these are required for ordinary software-development interviews, but they become useful in competitive programming, system internals, research, or specialized algorithmic roles.

---

# 52. Final Recognition Cheat Sheet

Recognition clues help narrow candidate techniques, but they are not proofs. Use each clue to form a hypothesis, then verify the input properties and state an invariant or recurrence that explains why the candidate algorithm is correct.

When you see:

```text
"pair in sorted array"
→ Two Pointers
```

```text
"substring/subarray + contiguous"
→ Sliding Window / Prefix Sum / Kadane / DP
```

```text
"top K / kth / priority"
→ Heap
```

```text
"duplicate / frequency / seen before"
→ Hash Map / Set
```

```text
"minimum possible maximum"
→ Binary Search on Answer
```

```text
"prerequisites / dependencies"
→ Directed Graph + Topological Sort
```

```text
"shortest path, all edges equal"
→ BFS
```

```text
"shortest weighted path, no negative weights"
→ Dijkstra
```

```text
"negative edge weights"
→ Bellman-Ford or another suitable negative-weight method
```

```text
"connect everything at minimum total cost"
→ MST
```

```text
"dynamic groups / connectivity"
→ DSU
```

```text
"generate every valid combination"
→ Backtracking
```

```text
"number of ways / minimum cost / maximum value + repeated subproblems"
→ Dynamic Programming
```

```text
"next greater / next smaller"
→ Monotonic Stack
```

```text
"prefix lookup / autocomplete"
→ Trie
```

```text
"many range queries + many updates"
→ Fenwick Tree / Segment Tree
```

---

# Bonus — How to Know You Truly Learned a Topic

You understand an algorithm when you can do all of these without copying:

- Explain it in simple language.
- Draw a small example.
- Implement a basic version.
- State its time complexity.
- State its space complexity.
- Explain why it is correct.
- Recognize when it is useful.
- Recognize when it is not useful.
- Solve a variation of the original problem.

Do not only memorize:

```text
Longest Substring Without Repeating Characters
```

Learn the reusable idea:

```text
Maintain a valid window.
Expand the right boundary.
When the rule breaks, move the left boundary.
Store only the information needed to validate the current window.
```

That reasoning transfers to many future problems.

---

# Bonus — Mini Projects for Learning DSA

Mini projects connect abstract structures to persistent state and user-visible behavior. For each project, identify the dominant operations first, choose the data structure based on those operations, and document what would become slower or harder if a different structure were used.

## 1. Autocomplete Engine

An autocomplete engine combines a **trie** for fast prefix navigation, optional hash maps for metadata, and often a heap or ranking structure for the best suggestions. A useful implementation should define how words are inserted, how prefixes are searched, and how ties or popularity scores affect the returned suggestions.

Use:

```text
Trie
Hash Map
Heap
```

Features:

- Add words
- Search prefixes
- Rank suggestions

## 2. Route Finder

A route finder models locations as graph vertices and roads/connections as edges. Use BFS when every edge has equal cost; use Dijkstra when edge weights such as distance or travel time are non-negative. The program should return the reachable path or distance and handle unreachable destinations explicitly.

Use:

```text
Graph
BFS
Dijkstra
```

Features:

- Add locations
- Add roads
- Find shortest route

## 3. Task Scheduler

A scheduler often needs efficient priority selection plus state for queued/completed work. A priority queue handles the next highest/lowest-priority task, while maps can support task lookup/cancellation. Define tie-breaking and deadline semantics so scheduling is deterministic.

Use:

```text
Heap
Queue
Hash Map
```

Features:

- Priorities
- Deadlines
- Execution order

## 4. Social Network Analyzer

A social network is naturally a graph where people are vertices and relationships are edges. BFS/DFS support reachability and degrees of separation, while sets/maps support neighbor membership; large-scale recommendations often require more specialized ranking/indexing beyond basic traversal.

Use:

```text
Graph
BFS
DFS
Sets
```

Features:

- Add friendships
- Mutual friends
- Connection distance
- Connected groups

## 5. Calendar Conflict Detector

A calendar conflict detector treats meetings as intervals. Sort by start time, then compare each interval with the end of the previous accepted interval; an overlap exists when the next start is before the relevant previous end. Sorting costs `O(n log n)` and the subsequent scan costs `O(n)`.

Use:

```text
Intervals
Sorting
Sweep Line
Heap
```

Features:

- Detect meeting conflicts
- Find free time
- Calculate required rooms/resources

---

# Final Principle

Do not aim to memorize 500 solutions.

Aim to recognize a relatively small set of reusable patterns.

For every new problem ask:

```text
1. What is the brute-force approach?
2. What work is repeated?
3. Can a data structure make that operation faster?
4. Is the data sorted or monotonic?
5. Is this about a contiguous range?
6. Is this really a graph problem?
7. Do subproblems repeat?
8. Do I need every possibility or only the best one?
9. Can a greedy choice be proven safe?
10. What are the time and space complexities?
```

Once these questions become automatic, DSA becomes structured problem solving rather than a collection of tricks.

---

**End of DSA Master Handbook**
