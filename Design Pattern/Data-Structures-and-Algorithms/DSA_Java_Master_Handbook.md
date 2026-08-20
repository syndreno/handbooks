# DSA with Java — Master Learning Handbook

> A beginner-friendly, in-depth, single-file handbook for learning Data Structures and Algorithms (DSA) using Java.
>
> **Goal:** Help a new learner move from “What is an array?” to confidently solving interview, competitive-programming, and real-world algorithmic problems in Java.

---

## How to Use This Handbook

This handbook is designed in layers:

1. **Foundation** — Java syntax and complexity you need for DSA.
2. **Core Data Structures** — arrays, strings, linked lists, stacks, queues, hashing, trees, heaps, graphs.
3. **Core Algorithms** — searching, sorting, recursion, backtracking, greedy, dynamic programming, graph algorithms.
4. **Problem-Solving Patterns** — two pointers, sliding window, prefix sums, monotonic stack, binary search on answer, intervals, etc.
5. **Advanced Structures and Algorithms** — trie, union-find, Fenwick tree, segment tree, KMP, MST, SCC, and more.
6. **Java-Specific DSA Toolkit** — Collections Framework, comparators, fast I/O, overflow, immutable/mutable choices.
7. **Interview System** — how to recognize patterns, explain solutions, test edge cases, and optimize.
8. **Practice Roadmap** — a structured path from beginner to advanced.

### Recommended learning loop

For every topic:

- Understand the **problem the concept solves**.
- Learn the **mental model**.
- Trace one example manually.
- Implement it yourself without copying.
- Study the time and space complexity.
- Solve at least 3–5 variations.
- Revisit the topic after a few days.

---

# Table of Contents

1. [DSA Fundamentals](#1-dsa-fundamentals)
2. [Java Essentials for DSA](#2-java-essentials-for-dsa)
3. [Time and Space Complexity](#3-time-and-space-complexity)
4. [Arrays](#4-arrays)
5. [Strings](#5-strings)
6. [Matrices and 2D Arrays](#6-matrices-and-2d-arrays)
7. [Linked Lists](#7-linked-lists)
8. [Stacks](#8-stacks)
9. [Queues and Deques](#9-queues-and-deques)
10. [Hashing](#10-hashing)
11. [Recursion](#11-recursion)
12. [Backtracking](#12-backtracking)
13. [Searching](#13-searching)
14. [Sorting](#14-sorting)
15. [Two Pointers](#15-two-pointers)
16. [Sliding Window](#16-sliding-window)
17. [Prefix Sum and Difference Arrays](#17-prefix-sum-and-difference-arrays)
18. [Intervals](#18-intervals)
19. [Binary Search on Answer](#19-binary-search-on-answer)
20. [Bit Manipulation](#20-bit-manipulation)
21. [Mathematics for DSA](#21-mathematics-for-dsa)
22. [Trees](#22-trees)
23. [Binary Search Trees](#23-binary-search-trees)
24. [Heaps and Priority Queues](#24-heaps-and-priority-queues)
25. [Trie](#25-trie)
26. [Graphs](#26-graphs)
27. [Disjoint Set Union](#27-disjoint-set-union)
28. [Greedy Algorithms](#28-greedy-algorithms)
29. [Dynamic Programming](#29-dynamic-programming)
30. [Monotonic Stack and Queue](#30-monotonic-stack-and-queue)
31. [Advanced Range Data Structures](#31-advanced-range-data-structures)
32. [Advanced String Algorithms](#32-advanced-string-algorithms)
33. [Advanced Graph Algorithms](#33-advanced-graph-algorithms)
34. [Common Problem-Solving Patterns](#34-common-problem-solving-patterns)
35. [Java Collections Framework for DSA](#35-java-collections-framework-for-dsa)
36. [Java Performance and Common Pitfalls](#36-java-performance-and-common-pitfalls)
37. [Reusable Java Templates](#37-reusable-java-templates)
38. [Interview Problem-Solving Framework](#38-interview-problem-solving-framework)
39. [Edge Cases Checklist](#39-edge-cases-checklist)
40. [Practice Roadmap](#40-practice-roadmap)
41. [Pattern Recognition Cheat Sheet](#41-pattern-recognition-cheat-sheet)
42. [Complexity Cheat Sheet](#42-complexity-cheat-sheet)
43. [Final Mastery Checklist](#43-final-mastery-checklist)

### Advanced Appendices

- [Appendix A — Additional Sorting and Selection Algorithms](#appendix-a--additional-sorting-and-selection-algorithms)
- [Appendix B — Queue Variants and Design Patterns](#appendix-b--queue-variants-and-design-patterns)
- [Appendix C — Hashing Internals](#appendix-c--hashing-internals)
- [Appendix D — Balanced and Multiway Trees](#appendix-d--balanced-and-multiway-trees)
- [Appendix E — Advanced Tree Algorithms](#appendix-e--advanced-tree-algorithms)
- [Appendix F — More Graph Patterns](#appendix-f--more-graph-patterns)
- [Appendix G — Advanced Dynamic Programming Patterns](#appendix-g--advanced-dynamic-programming-patterns)
- [Appendix H — Advanced String Structures](#appendix-h--advanced-string-structures)
- [Appendix I — Randomization and Probabilistic Thinking](#appendix-i--randomization-and-probabilistic-thinking)
- [Appendix J — Amortized Analysis](#appendix-j--amortized-analysis)
- [Appendix K — Invariants](#appendix-k--invariants-the-hidden-skill-behind-correct-algorithms)
- [Appendix L — Data Structure Selection Guide](#appendix-l--data-structure-selection-guide)
- [Appendix M — Problem Difficulty Progression](#appendix-m--problem-difficulty-progression)
- [Appendix N — Building Your Personal DSA Library](#appendix-n--building-your-personal-dsa-library)
- [Appendix O — What Should I Learn Next?](#appendix-o--final-what-should-i-learn-next-decision-tree)

---

# 1. DSA Fundamentals

DSA begins with two linked ideas: **how data is organized** and **how operations transform that data**. The goal is not to memorize names, but to learn how representation choices affect correctness, runtime, memory use, and code clarity.

## 1.1 What are Data Structures?

A **data structure** is a way of organizing data so that operations on it can be performed efficiently.

Examples:

- Array — fast indexed access.
- Linked List — flexible insertion/deletion when a node position is known.
- Stack — last-in, first-out processing.
- Queue — first-in, first-out processing.
- HashMap — fast key-based lookup on average.
- Heap — efficient retrieval of minimum or maximum element.
- Tree — hierarchical information.
- Graph — relationships between arbitrary entities.

### Real-world analogy

Imagine a warehouse:

- Unsorted pile → hard to find anything.
- Numbered shelves → array-like indexed access.
- Priority dispatch area → heap.
- Customer waiting line → queue.
- Undo history → stack.
- Employee ID directory → hash map.

Choosing the right data structure is often more important than writing clever code.

## 1.2 What is an Algorithm?

An **algorithm** is a finite sequence of steps that transforms an input into a desired output.

Example problem:

> Find whether `37` exists in a sorted array.

Possible algorithms:

- Linear search — inspect every value.
- Binary search — repeatedly discard half the search space.

The second algorithm is dramatically faster for large sorted arrays.

## 1.3 Data Structure vs Algorithm

| Concept | Meaning | Example |
|---|---|---|
| Data Structure | How data is organized | Array, HashMap, Tree |
| Algorithm | How a problem is solved | Binary Search, Merge Sort |

They work together. For example, Dijkstra's shortest path algorithm typically combines a graph with a priority queue.

## 1.4 Abstract Data Type (ADT)

An ADT defines **what operations are supported**, not necessarily how they are implemented.

A stack ADT supports:

- `push`
- `pop`
- `peek`
- `isEmpty`

It can be implemented using:

- array
- dynamic array
- linked list

## 1.5 Correctness, Efficiency, Readability

A strong DSA solution should ideally satisfy three goals:

1. **Correctness** — works for all valid inputs.
2. **Efficiency** — uses acceptable time and memory.
3. **Clarity** — another developer can understand and maintain it.

---

# 2. Java Essentials for DSA

You do not need every Java feature before starting DSA, but the following features are essential.

## 2.1 Basic Program Structure

This is the minimum executable shell around the examples. The entry point starts the program, while helper methods and data-structure classes can be added as separate methods or nested/top-level classes. For interview-style code, keep this scaffolding small so the algorithm remains the focus.

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, DSA!");
    }
}
```

## 2.2 Primitive Types

Primitive numeric and boolean types matter in DSA because they determine value range, arithmetic behavior, memory representation, and comparison semantics. Choose the smallest type that safely represents the required values, but promote calculations when a sum or product can exceed that range.

| Type | Common DSA Usage |
|---|---|
| `int` | indexes, most values |
| `long` | large sums/products |
| `double` | floating-point calculations |
| `char` | character algorithms |
| `boolean` | visited flags, conditions |

### Overflow warning

Overflow happens when an arithmetic result does not fit in the numeric type used for the operation. Promote operands **before** multiplication/addition when necessary; converting the already-overflowed result afterward is too late. Always compare the problem's maximum input values with the type's range.

```java
int a = 1_000_000_000;
int b = 1_000_000_000;
int product = a * b; // overflow
```

Use `long`:

```java
long product = 1L * a * b;
```

The `1L` forces multiplication to happen using `long` arithmetic.

## 2.3 Arrays

An array-like structure stores elements in an indexed sequence. Its main advantage is direct access by position; the main trade-off is that inserting or deleting near the front or middle usually requires shifting elements. In DSA problems, arrays are also the base structure behind two pointers, sliding windows, prefix sums, binary search, heaps, and many dynamic-programming tables.

```java
int[] nums = {10, 20, 30};
System.out.println(nums[1]); // 20
```

## 2.4 Enhanced For Loop

An enhanced `for` loop iterates directly over each element and is ideal when the algorithm only needs values. It does not expose the current index and should not be used when you must replace elements by position or structurally modify the same collection during iteration.

```java
for (int value : nums) {
    System.out.println(value);
}
```

Use an index loop when you need the position:

```java
for (int i = 0; i < nums.length; i++) {
    System.out.println(i + " -> " + nums[i]);
}
```

## 2.5 Methods

A function/method packages a reusable piece of algorithmic work behind inputs and a return value. For DSA helpers, make the contract explicit: what each parameter represents, whether the input is mutated, what is returned, and what happens for empty or invalid input.

```java
static int max(int a, int b) {
    return a > b ? a : b;
}
```

## 2.6 Classes for Custom Nodes

Classes are useful in DSA for nodes, heaps, tries, graphs, or reusable structures that own state plus operations. Keep fields tied to one invariant and expose methods that preserve it; a class is unnecessary when a small pure function solves the problem more clearly.

```java
class ListNode {
    int val;
    ListNode next;

    ListNode(int val) {
        this.val = val;
    }
}
```

## 2.7 Generics

Generics let one data-structure implementation work with multiple element types while preserving compile-time type safety. A generic node or container should express the minimum operations it actually needs rather than forcing callers to cast from a broad type.

```java
List<Integer> numbers = new ArrayList<>();
Map<String, Integer> frequency = new HashMap<>();
```

Java collections require wrapper types such as `Integer`, not primitive `int`.

## 2.8 Useful Java Utilities

Java's standard library provides reliable building blocks such as `Arrays`, `Collections`, `Math`, `Comparator`, and collection implementations. Use these when the task is about solving a problem rather than reimplementing library behavior, but know the mutation and complexity of each operation you call.

```java
import java.util.*;
```

Common classes:

- `Arrays`
- `Collections`
- `ArrayList`
- `LinkedList`
- `ArrayDeque`
- `HashMap`
- `HashSet`
- `TreeMap`
- `TreeSet`
- `PriorityQueue`

---

# 3. Time and Space Complexity

Complexity analysis estimates how an algorithm's resource usage grows as input size increases. Focus on the dominant growth rate rather than machine-specific timing, and analyze both execution work and extra memory so you can compare approaches before benchmarking.

Complexity describes how resource usage grows as input size grows.

## 3.1 Big-O Notation

Big-O describes how an upper growth bound changes as input size grows. In interview usage it is commonly used to communicate the dominant running-time or memory growth of an implementation. Derive it from executed work and data-structure operations rather than assigning it from the algorithm's name alone.

Big-O usually describes an upper-bound growth rate.

Common complexities from fastest to slowest:

```text
O(1)
O(log n)
O(n)
O(n log n)
O(n^2)
O(n^3)
O(2^n)
O(n!)
```

## 3.2 O(1) — Constant Time

`O(1)` means the amount of work does not grow with the number of input elements. It does **not** mean the operation takes exactly one CPU instruction; it means the step count is bounded by a constant with respect to input size. Examples include reading a known array index or checking a stored variable.

```java
int first = nums[0];
```

Array indexing does not depend on the array length.

## 3.3 O(n) — Linear Time

`O(n)` means the running time grows proportionally with the input size. A single complete pass over an array is the standard example. Several separate linear passes are still `O(n)` because constant multipliers are omitted in asymptotic analysis.

```java
int sum = 0;
for (int x : nums) {
    sum += x;
}
```

If the array doubles in size, work roughly doubles.

## 3.4 O(n²) — Quadratic Time

`O(n²)` usually appears when the algorithm examines many pairs of input elements, such as two nested loops over the same `n` items. Doubling `n` can make the dominant work roughly four times larger, so quadratic approaches become expensive quickly on large inputs.

```java
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        // work
    }
}
```

Typical for checking all pairs.

## 3.5 O(log n)

`O(log n)` appears when each step reduces the remaining problem by a constant factor, often by half. Binary search is the classic example. The logarithm base is ignored in Big-O because changing the base only multiplies the count by a constant factor.

Binary search repeatedly halves the problem size:

```text
n -> n/2 -> n/4 -> n/8 -> ... -> 1
```

## 3.6 O(n log n)

`O(n log n)` commonly appears when an algorithm performs logarithmic levels of work and processes `O(n)` data across each level. Efficient comparison sorts such as merge sort and heap sort have this bound; divide-and-conquer algorithms often produce it as well.

Efficient comparison sorting algorithms such as merge sort typically run in `O(n log n)`.

## 3.7 Recursive Complexity

For recursive code, analyze both **how many calls/states exist** and **how much work each call performs**. Also include maximum recursion depth in space complexity. A recursion tree, recurrence relation, or count of unique memoized states can make the growth explicit.

Example:

```java
static int factorial(int n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}
```

Time: `O(n)`

Call-stack space: `O(n)`

## 3.8 Amortized Complexity

Amortized analysis spreads the cost of occasional expensive operations over a long sequence of operations. For example, a dynamic array resize may cost `O(n)`, but because resizing is infrequent, repeated append operations can still have `O(1)` amortized cost. Amortized complexity is a sequence-level guarantee; it does not mean every individual operation is constant-time.

`ArrayList.add()` is usually `O(1)`, but occasionally resizing costs `O(n)`.

Across many insertions, the average cost is still **amortized O(1)**.

## 3.9 Space Complexity

Space complexity measures how much additional memory grows with input size. Distinguish the input itself from **auxiliary space** used by the algorithm, and remember to include recursion depth, temporary arrays, hash tables, queues, and stacks. An in-place algorithm usually means `O(1)` or very small auxiliary storage, not that the input occupies no memory.

Consider both:

- Auxiliary data structures.
- Recursion call stack.

Example:

```java
int[] copy = nums.clone();
```

Extra space: `O(n)`.

## 3.10 Input Size Rule of Thumb

These are rough—not guarantees:

| Input size | Typical feasible complexity |
|---:|---|
| `n <= 20` | `O(2^n)` may be possible |
| `n <= 100` | `O(n^3)` may be possible |
| `n <= 1,000` | `O(n^2)` often possible |
| `n <= 100,000` | usually target `O(n log n)` or `O(n)` |
| `n >= 1,000,000` | often near `O(n)` |

---

# 4. Arrays

An array-like structure stores elements in an indexed sequence. Its main advantage is direct access by position; the main trade-off is that inserting or deleting near the front or middle usually requires shifting elements. In DSA problems, arrays are also the base structure behind two pointers, sliding windows, prefix sums, binary search, heaps, and many dynamic-programming tables.

An array stores elements in contiguous logical positions and provides constant-time indexed access.

## 4.1 Basic Operations

```java
int[] arr = new int[5];
arr[0] = 10;
arr[1] = 20;
```

| Operation | Complexity |
|---|---:|
| Access by index | `O(1)` |
| Update by index | `O(1)` |
| Search unsorted | `O(n)` |
| Insert in middle | `O(n)` |
| Delete from middle | `O(n)` |

## 4.2 Find Maximum

Finding a maximum requires a baseline that is valid for the input domain. Initialize from the first element (after handling empty input) rather than from `0`, which fails when every value is negative. Then scan once and replace the current maximum whenever a larger value appears: `O(n)` time, `O(1)` extra space.

```java
static int findMax(int[] arr) {
    int max = arr[0];

    for (int x : arr) {
        max = Math.max(max, x);
    }

    return max;
}
```

**Scenario:** Find the highest daily sales value.

Time: `O(n)`

Space: `O(1)`

## 4.3 Reverse an Array In Place

In-place reversal swaps symmetric elements from the two ends and moves inward until the pointers meet. Each element is touched a constant number of times, giving `O(n)` time and `O(1)` auxiliary space. The input array is mutated, so callers that need the original order must copy it first.

```java
static void reverse(int[] arr) {
    int left = 0;
    int right = arr.length - 1;

    while (left < right) {
        int temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;
        left++;
        right--;
    }
}
```

## 4.4 Second Largest Distinct Element

Track the largest and second-largest **distinct** values while scanning once. Updating order matters: when a new maximum arrives, the old maximum becomes the second-largest candidate; equal values should not replace the distinct second candidate. Define what to return when fewer than two distinct values exist.

```java
static Integer secondLargest(int[] arr) {
    Integer largest = null;
    Integer second = null;

    for (int x : arr) {
        if (largest == null || x > largest) {
            if (largest == null || x != largest) {
                second = largest;
            }
            largest = x;
        } else if (x != largest && (second == null || x > second)) {
            second = x;
        }
    }

    return second;
}
```

## 4.5 Remove Duplicates from Sorted Array

Because the array is sorted, equal values appear next to one another. A read pointer scans every element while a write pointer marks where the next distinct value belongs. The algorithm runs in `O(n)` time and can overwrite the input in place using `O(1)` extra space; the returned length/count tells the caller which prefix contains the unique values.

```java
static int removeDuplicates(int[] nums) {
    if (nums.length == 0) return 0;

    int write = 1;

    for (int read = 1; read < nums.length; read++) {
        if (nums[read] != nums[read - 1]) {
            nums[write++] = nums[read];
        }
    }

    return write;
}
```

This demonstrates the **read/write pointer** technique.

## 4.6 Rotate Array Right by k

Normalize `k` with `k %= n` after handling an empty list. A slicing solution is concise but allocates new lists; an in-place three-reversal method uses constant auxiliary storage but mutates the original list.

Idea:

1. Reverse entire array.
2. Reverse first `k` elements.
3. Reverse remaining elements.

```java
static void rotateRight(int[] nums, int k) {
    int n = nums.length;
    if (n == 0) return;

    k %= n;
    reverseRange(nums, 0, n - 1);
    reverseRange(nums, 0, k - 1);
    reverseRange(nums, k, n - 1);
}

static void reverseRange(int[] nums, int left, int right) {
    while (left < right) {
        int temp = nums[left];
        nums[left++] = nums[right];
        nums[right--] = temp;
    }
}
```

Time: `O(n)`

Space: `O(1)`

## 4.7 Kadane's Algorithm — Maximum Subarray Sum

An algorithm is a finite, unambiguous procedure that converts an input into the required output. A useful explanation of an algorithm should state its preconditions, the main invariant or idea that keeps it correct, when it stops, and its time and space complexity.

Problem:

```text
[-2, 1, -3, 4, -1, 2, 1, -5, 4]
```

Best contiguous subarray:

```text
[4, -1, 2, 1]
```

Sum = `6`.

```java
static int maxSubarraySum(int[] nums) {
    int current = nums[0];
    int best = nums[0];

    for (int i = 1; i < nums.length; i++) {
        current = Math.max(nums[i], current + nums[i]);
        best = Math.max(best, current);
    }

    return best;
}
```

Mental model:

> At each index, either continue the current subarray or start fresh here.

---

# 5. Strings

A string is a sequence of characters, but its exact behavior depends on the language's string model and character encoding. DSA string problems commonly need indexing/traversal, frequency counting, substring handling, comparison, prefix/suffix reasoning, or pattern matching. Always check whether the task assumes simple ASCII-like characters or full Unicode text.

Java `String` objects are immutable.

```java
String s = "java";
s = s + " dsa";
```

The original string is not modified; a new string is created.

For repeated modifications, use `StringBuilder`.

## 5.1 Character Access

Character access means reading a symbol at a particular position in a string. Before using an index-based approach, know what one index represents in the language: a byte, UTF-16 code unit, Unicode code point, or grapheme cluster. For basic ASCII-style DSA exercises, direct indexing is usually sufficient; production international text may require Unicode-aware iteration.

```java
char c = s.charAt(0);
int n = s.length();
```

## 5.2 Reverse a String

Reversing a string creates the characters in opposite order. Because strings are often immutable, implementations typically use a mutable character buffer/array or a builder rather than assigning directly into the original string. State whether Unicode code units/code points matter for the problem.

```java
static String reverseString(String s) {
    return new StringBuilder(s).reverse().toString();
}
```

Manual form:

```java
static String reverseManual(String s) {
    char[] chars = s.toCharArray();
    int left = 0, right = chars.length - 1;

    while (left < right) {
        char temp = chars[left];
        chars[left] = chars[right];
        chars[right] = temp;
        left++;
        right--;
    }

    return new String(chars);
}
```

## 5.3 Palindrome Check

A palindrome reads the same forward and backward under the problem's comparison rules. The standard two-pointer check compares the leftmost and rightmost relevant characters and moves inward, stopping on the first mismatch. Time is `O(n)` and extra space can be `O(1)` when normalization is not stored separately.

```java
static boolean isPalindrome(String s) {
    int left = 0;
    int right = s.length() - 1;

    while (left < right) {
        if (s.charAt(left) != s.charAt(right)) {
            return false;
        }
        left++;
        right--;
    }

    return true;
}
```

## 5.4 Character Frequency

A frequency table records how many times each value occurs. Python's `Counter` constructs this mapping directly from an iterable and is useful when counts—not just membership—are needed.

For lowercase English letters:

```java
static int[] frequency(String s) {
    int[] freq = new int[26];

    for (char c : s.toCharArray()) {
        freq[c - 'a']++;
    }

    return freq;
}
```

## 5.5 Anagram Check

Two strings are anagrams when they contain the same symbols with the same frequencies, subject to the problem's normalization rules. A frequency map gives `O(n)` expected time and avoids sorting; sorting both strings is simpler in some cases but typically costs `O(n log n)`. Decide explicitly whether case, spaces, punctuation, and Unicode normalization matter.

```java
static boolean isAnagram(String a, String b) {
    if (a.length() != b.length()) return false;

    int[] freq = new int[26];

    for (char c : a.toCharArray()) freq[c - 'a']++;
    for (char c : b.toCharArray()) freq[c - 'a']--;

    for (int count : freq) {
        if (count != 0) return false;
    }

    return true;
}
```

## 5.6 StringBuilder

Repeated string concatenation can create many temporary immutable string objects. A builder accumulates pieces in a mutable buffer and produces the final string once, which is usually better when constructing output inside loops. Use it when the number of appended pieces is non-trivial; plain concatenation is still fine for a few small fixed expressions.

```java
StringBuilder sb = new StringBuilder();
sb.append("Java");
sb.append(' ');
sb.append("DSA");
System.out.println(sb.toString());
```

Use `StringBuilder` when constructing a result inside loops.

## 5.7 Longest Common Prefix

The longest common prefix is the longest starting substring shared by every string in the collection. A practical approach uses one string as the candidate prefix and shortens/compares it against the others. Handle an empty collection explicitly; the answer is an empty string when no first character is shared.

```java
static String longestCommonPrefix(String[] words) {
    if (words.length == 0) return "";

    String prefix = words[0];

    for (int i = 1; i < words.length; i++) {
        while (!words[i].startsWith(prefix)) {
            prefix = prefix.substring(0, prefix.length() - 1);
            if (prefix.isEmpty()) return "";
        }
    }

    return prefix;
}
```

---

# 6. Matrices and 2D Arrays

An array-like structure stores elements in an indexed sequence. Its main advantage is direct access by position; the main trade-off is that inserting or deleting near the front or middle usually requires shifting elements. In DSA problems, arrays are also the base structure behind two pointers, sliding windows, prefix sums, binary search, heaps, and many dynamic-programming tables.

```java
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
```

## 6.1 Traverse a Matrix

Matrix traversal usually uses one loop for rows and another for columns. Keep the dimensions explicit—`rows` and `cols` can differ—and access `matrix[row][col]` only after verifying bounds. A full rectangular traversal visits each cell once: `O(rows × cols)`.

```java
for (int row = 0; row < matrix.length; row++) {
    for (int col = 0; col < matrix[row].length; col++) {
        System.out.print(matrix[row][col] + " ");
    }
}
```

## 6.2 Transpose a Square Matrix

A transpose swaps rows and columns: element `(r, c)` moves to `(c, r)`. For a square matrix, it can be done in place by swapping only one side of the diagonal; visiting both sides would swap elements twice and undo the work. Rectangular matrices require a new shape unless the representation supports resizing.

```java
static void transpose(int[][] matrix) {
    int n = matrix.length;

    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            int temp = matrix[i][j];
            matrix[i][j] = matrix[j][i];
            matrix[j][i] = temp;
        }
    }
}
```

## 6.3 Rotate Matrix 90° Clockwise

For a square matrix, a common in-place clockwise rotation is **transpose, then reverse each row**. The transpose moves `(r,c)` to `(c,r)` and row reversal completes the geometric rotation. The algorithm is `O(n²)` time with `O(1)` extra array space.

Approach:

1. Transpose.
2. Reverse each row.

```java
static void rotate90Clockwise(int[][] matrix) {
    transpose(matrix);

    for (int[] row : matrix) {
        int left = 0, right = row.length - 1;
        while (left < right) {
            int temp = row[left];
            row[left++] = row[right];
            row[right--] = temp;
        }
    }
}
```

## 6.4 Spiral Traversal

Traversal means visiting each relevant element/node in a defined order. The important state is the current position and the rule for advancing to the next one. A full traversal is usually `O(n)` for a linear structure, while trees/graphs additionally require a stack/queue or recursion and, for cyclic graphs, visited tracking.

```java
static List<Integer> spiralOrder(int[][] matrix) {
    List<Integer> result = new ArrayList<>();

    int top = 0;
    int bottom = matrix.length - 1;
    int left = 0;
    int right = matrix[0].length - 1;

    while (top <= bottom && left <= right) {
        for (int col = left; col <= right; col++) {
            result.add(matrix[top][col]);
        }
        top++;

        for (int row = top; row <= bottom; row++) {
            result.add(matrix[row][right]);
        }
        right--;

        if (top <= bottom) {
            for (int col = right; col >= left; col--) {
                result.add(matrix[bottom][col]);
            }
            bottom--;
        }

        if (left <= right) {
            for (int row = bottom; row >= top; row--) {
                result.add(matrix[row][left]);
            }
            left++;
        }
    }

    return result;
}
```

---

# 7. Linked Lists

A linked list stores values in nodes connected by references rather than by contiguous indexed positions. This makes pointer rewiring cheap once the relevant node is known, but random access is slow because traversal normally starts from the head. Linked-list problems therefore focus heavily on pointer movement, insertion/removal, reversal, cycle detection, and fast/slow-pointer techniques.

A linked list stores nodes connected using references.

```java
class ListNode {
    int val;
    ListNode next;

    ListNode(int val) {
        this.val = val;
    }
}
```

## 7.1 Why Use a Linked List?

Advantages:

- Dynamic size.
- Efficient insertion/deletion when the relevant node is known.

Disadvantages:

- No direct indexed access.
- Extra memory for references.
- Poorer cache locality than arrays.

## 7.2 Traversal

Traversal means visiting each relevant element/node in a defined order. The important state is the current position and the rule for advancing to the next one. A full traversal is usually `O(n)` for a linear structure, while trees/graphs additionally require a stack/queue or recursion and, for cyclic graphs, visited tracking.

```java
static void printList(ListNode head) {
    ListNode current = head;

    while (current != null) {
        System.out.print(current.val + " ");
        current = current.next;
    }
}
```

## 7.3 Insert at Beginning

Inserting at the beginning is cheap for a linked structure when only the head reference changes, but expensive for a dynamic array because existing elements may need to shift. This difference is a useful example of choosing a data structure based on the operations that must be fast.

```java
static ListNode insertFront(ListNode head, int value) {
    ListNode node = new ListNode(value);
    node.next = head;
    return node;
}
```

## 7.4 Reverse a Linked List

Reversing a singly linked list rewires each node's `next` reference. Keep three pieces of state: the previous node, the current node, and the original next node so the remainder of the list is not lost before reassignment. The iterative algorithm runs in `O(n)` time and `O(1)` extra space.

```java
static ListNode reverseList(ListNode head) {
    ListNode previous = null;
    ListNode current = head;

    while (current != null) {
        ListNode nextNode = current.next;
        current.next = previous;
        previous = current;
        current = nextNode;
    }

    return previous;
}
```

Three pointers:

```text
previous <- current -> next
```

## 7.5 Find Middle Node

Use two references: `slow` advances one node at a time and `fast` advances two. When `fast` reaches the end, `slow` points to the middle (for even-length lists, define which of the two middle nodes the implementation returns). The method runs in `O(n)` time and `O(1)` extra space without a preliminary length pass.

Use slow and fast pointers.

```java
static ListNode middleNode(ListNode head) {
    ListNode slow = head;
    ListNode fast = head;

    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }

    return slow;
}
```

## 7.6 Detect Cycle — Floyd's Algorithm

An algorithm is a finite, unambiguous procedure that converts an input into the required output. A useful explanation of an algorithm should state its preconditions, the main invariant or idea that keeps it correct, when it stops, and its time and space complexity.

```java
static boolean hasCycle(ListNode head) {
    ListNode slow = head;
    ListNode fast = head;

    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;

        if (slow == fast) return true;
    }

    return false;
}
```

## 7.7 Merge Two Sorted Linked Lists

A linked list stores values in nodes connected by references rather than by contiguous indexed positions. This makes pointer rewiring cheap once the relevant node is known, but random access is slow because traversal normally starts from the head. Linked-list problems therefore focus heavily on pointer movement, insertion/removal, reversal, cycle detection, and fast/slow-pointer techniques.

```java
static ListNode mergeSorted(ListNode a, ListNode b) {
    ListNode dummy = new ListNode(0);
    ListNode tail = dummy;

    while (a != null && b != null) {
        if (a.val <= b.val) {
            tail.next = a;
            a = a.next;
        } else {
            tail.next = b;
            b = b.next;
        }
        tail = tail.next;
    }

    tail.next = (a != null) ? a : b;
    return dummy.next;
}
```

## 7.8 Doubly Linked List

A doubly linked list stores both `next` and `prev` links. This enables traversal in both directions and makes deletion of a known node easier because its predecessor is directly available, at the cost of extra memory and more pointer updates that must remain consistent.

```java
class DoublyNode {
    int val;
    DoublyNode prev;
    DoublyNode next;

    DoublyNode(int val) {
        this.val = val;
    }
}
```

Useful for:

- browser history
- LRU cache
- bidirectional traversal

---

# 8. Stacks

A stack follows **LIFO** — Last In, First Out.

Use cases:

- undo/redo
- function calls
- expression evaluation
- bracket matching
- monotonic stack problems
- DFS

## 8.1 Recommended Java Stack Implementation

This implementation turns the surrounding concept into concrete state and operations. Identify what each field stores, which method mutates that state, and what invariant must remain true after every operation; those details matter more than memorizing the exact syntax.

Prefer `ArrayDeque` over the legacy `Stack` class.

```java
Deque<Integer> stack = new ArrayDeque<>();

stack.push(10);
stack.push(20);

System.out.println(stack.peek()); // 20
System.out.println(stack.pop());  // 20
```

## 8.2 Valid Parentheses

Balanced-bracket checking uses a stack of opening brackets. Each closing bracket must match the most recent unmatched opening bracket, so a mismatch or an empty stack fails immediately; after the scan, the stack must also be empty. The algorithm is `O(n)` time and `O(n)` worst-case space.

```java
static boolean isValidParentheses(String s) {
    Deque<Character> stack = new ArrayDeque<>();

    for (char c : s.toCharArray()) {
        if (c == '(' || c == '[' || c == '{') {
            stack.push(c);
        } else {
            if (stack.isEmpty()) return false;

            char open = stack.pop();

            if ((c == ')' && open != '(') ||
                (c == ']' && open != '[') ||
                (c == '}' && open != '{')) {
                return false;
            }
        }
    }

    return stack.isEmpty();
}
```

## 8.3 Min Stack Concept

A stack follows **Last In, First Out (LIFO)** order: the most recently pushed item is the first one removed. The core operations are push, pop, peek/top, and an emptiness check. Stacks are useful when later work depends on the most recent unfinished item, such as expression evaluation, undo, DFS, bracket matching, monotonic-stack problems, and simulated recursion.

Goal: support `push`, `pop`, and minimum retrieval in `O(1)`.

```java
class MinStack {
    private final Deque<Integer> values = new ArrayDeque<>();
    private final Deque<Integer> minimums = new ArrayDeque<>();

    void push(int x) {
        values.push(x);
        if (minimums.isEmpty() || x <= minimums.peek()) {
            minimums.push(x);
        }
    }

    int pop() {
        int value = values.pop();
        if (value == minimums.peek()) {
            minimums.pop();
        }
        return value;
    }

    int min() {
        return minimums.peek();
    }
}
```

---

# 9. Queues and Deques

A queue follows **FIFO** — First In, First Out.

Use cases:

- task scheduling
- BFS
- request processing
- buffering

## 9.1 Queue in Java

A queue follows **First In, First Out (FIFO)** order: the earliest enqueued item is processed first. The key operations are enqueue, dequeue, front/peek, and emptiness checking. Queues are a natural fit for breadth-first search, scheduling, buffering, and any workflow that must preserve arrival order.

```java
Queue<Integer> queue = new ArrayDeque<>();

queue.offer(10);
queue.offer(20);

System.out.println(queue.peek()); // 10
System.out.println(queue.poll()); // 10
```

Prefer:

- `offer()` instead of `add()`
- `poll()` instead of `remove()`
- `peek()` instead of `element()`

because the first group handles empty/full conditions more gracefully.

## 9.2 Deque

A deque (double-ended queue) supports insertion and removal at both the front and back. It can behave as either a stack or a queue and is especially useful for sliding-window algorithms and 0-1 BFS. Prefer an implementation whose front and back operations are constant-time rather than an array operation that shifts many elements.

A deque supports insertion/removal from both ends.

```java
Deque<Integer> deque = new ArrayDeque<>();

deque.offerFirst(10);
deque.offerLast(20);
deque.pollFirst();
deque.pollLast();
```

Common uses:

- sliding window maximum
- monotonic queue
- palindrome logic
- implementing stacks and queues

---

# 10. Hashing

Hashing maps keys to values using a hash function.

Java tools:

- `HashMap<K, V>`
- `HashSet<E>`

Average insert/search/delete is generally `O(1)`.

## 10.1 Frequency Map

A frequency map stores `value → count`. Scan the input once, incrementing the count for each value; later frequency queries are average `O(1)` with a hash map. This pattern is useful for duplicates, anagrams, counting categories, majority/frequency problems, and many sliding-window algorithms.

```java
static Map<Integer, Integer> buildFrequency(int[] nums) {
    Map<Integer, Integer> freq = new HashMap<>();

    for (int x : nums) {
        freq.put(x, freq.getOrDefault(x, 0) + 1);
    }

    return freq;
}
```

## 10.2 Two Sum

The optimized Two Sum pattern trades memory for speed. While scanning, compute the complement `target - current`; if that complement was seen earlier, return the matching indexes/values, otherwise store the current item. With a hash map this is `O(n)` expected time and `O(n)` extra space.

```java
static int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> indexByValue = new HashMap<>();

    for (int i = 0; i < nums.length; i++) {
        int needed = target - nums[i];

        if (indexByValue.containsKey(needed)) {
            return new int[]{indexByValue.get(needed), i};
        }

        indexByValue.put(nums[i], i);
    }

    return new int[]{-1, -1};
}
```

Mental pattern:

> Instead of repeatedly searching the past, remember it.

## 10.3 Detect Duplicates

Duplicate detection can use a set of values seen so far. If the current value is already present, a duplicate exists; otherwise add it and continue. This is `O(n)` expected time with `O(n)` extra space, compared with `O(n²)` pair checking or `O(n log n)` sorting.

```java
static boolean containsDuplicate(int[] nums) {
    Set<Integer> seen = new HashSet<>();

    for (int x : nums) {
        if (!seen.add(x)) return true;
    }

    return false;
}
```

## 10.4 Group Anagrams

The example implements **10.4 Group Anagrams** with `groupAnagrams(...)`. Its parameters are `String[] words`. Trace how those inputs change or are read, then inspect the `return` statement (or observable mutation/output) to identify the result. Also account for the cost of any loop, recursion, container operation, or nested call when deriving complexity.

```java
static List<List<String>> groupAnagrams(String[] words) {
    Map<String, List<String>> groups = new HashMap<>();

    for (String word : words) {
        char[] chars = word.toCharArray();
        Arrays.sort(chars);
        String key = new String(chars);

        groups.computeIfAbsent(key, k -> new ArrayList<>()).add(word);
    }

    return new ArrayList<>(groups.values());
}
```

---

# 11. Recursion

Recursion occurs when a function calls itself on a smaller version of the same problem.

Every recursive solution needs:

1. Base case.
2. Recursive case.
3. Progress toward the base case.

## 11.1 Factorial

Factorial is defined for non-negative integers by `n! = n × (n-1) × ... × 1`, with `0! = 1`. A recursive implementation mirrors that definition, but an iterative version avoids recursive call-stack growth. Factorial values grow extremely quickly, so ordinary fixed-width integer types overflow at relatively small `n` values.

```java
static long factorial(int n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}
```

## 11.2 Sum of Array Recursively

A recursive sum processes one element and delegates the remainder to a smaller state until a base case such as an empty suffix/index is reached. It is `O(n)` time but also uses `O(n)` call-stack space, so an iterative loop is usually preferable when recursion adds no structural clarity.

```java
static int sum(int[] arr, int index) {
    if (index == arr.length) return 0;
    return arr[index] + sum(arr, index + 1);
}
```

## 11.3 Recursion Tree

Recursion solves a problem by calling the same routine on a smaller or simpler state. Every recursive solution needs a **base case** that stops further calls and a **progress rule** that moves toward that base case. Also account for call-stack space: even an algorithm with little explicit memory usage may use `O(depth)` stack space.

Naive Fibonacci:

```java
static int fib(int n) {
    if (n <= 1) return n;
    return fib(n - 1) + fib(n - 2);
}
```

The same subproblems are recomputed repeatedly. This leads naturally to **dynamic programming**.

## 11.4 Stack Overflow Risk

A stack follows **Last In, First Out (LIFO)** order: the most recently pushed item is the first one removed. The core operations are push, pop, peek/top, and an emptiness check. Stacks are useful when later work depends on the most recent unfinished item, such as expression evaluation, undo, DFS, bracket matching, monotonic-stack problems, and simulated recursion.

Java recursion depth is limited by the thread stack. Very deep recursion can cause `StackOverflowError`.

For a long linked list or graph, iterative logic may be safer.

---

# 12. Backtracking

Backtracking explores a decision tree by making a choice, recursively exploring what follows, and then undoing that choice before trying the next option. It is appropriate when the task asks for all valid combinations, permutations, placements, paths, or constraint-satisfying configurations. Pruning impossible branches early is often the difference between a practical and an impractical solution.

Backtracking explores choices, abandons invalid paths, and tries alternatives.

Template:

```java
void backtrack(State state) {
    if (isSolution(state)) {
        save(state);
        return;
    }

    for (Choice choice : choices(state)) {
        make(choice);
        backtrack(state);
        undo(choice);
    }
}
```

## 12.1 Generate All Subsets

Generating all subsets explores two choices for each element: include it or exclude it. That creates `2^n` possible subsets, so exponential output size is unavoidable. Backtracking should add a **copy** of the current path to the result because the same mutable path is modified during later recursive calls.

```java
static List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    buildSubsets(nums, 0, new ArrayList<>(), result);
    return result;
}

static void buildSubsets(
        int[] nums,
        int index,
        List<Integer> current,
        List<List<Integer>> result) {

    if (index == nums.length) {
        result.add(new ArrayList<>(current));
        return;
    }

    // Exclude nums[index]
    buildSubsets(nums, index + 1, current, result);

    // Include nums[index]
    current.add(nums[index]);
    buildSubsets(nums, index + 1, current, result);
    current.remove(current.size() - 1);
}
```

## 12.2 Permutations

Generating permutations chooses one unused item for each next position, recursively explores the remainder, and then undoes the choice. There are `n!` outputs for distinct items, so factorial work is inherent. With duplicate input values, add a duplicate-skipping rule if unique permutations are required.

```java
static List<List<Integer>> permutations(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    boolean[] used = new boolean[nums.length];
    generatePermutations(nums, used, new ArrayList<>(), result);
    return result;
}

static void generatePermutations(
        int[] nums,
        boolean[] used,
        List<Integer> current,
        List<List<Integer>> result) {

    if (current.size() == nums.length) {
        result.add(new ArrayList<>(current));
        return;
    }

    for (int i = 0; i < nums.length; i++) {
        if (used[i]) continue;

        used[i] = true;
        current.add(nums[i]);

        generatePermutations(nums, used, current, result);

        current.remove(current.size() - 1);
        used[i] = false;
    }
}
```

## 12.3 Combination Sum Pattern

The key decision is whether the same candidate can be reused and where the next loop should begin.

```java
static void combinationSum(
        int[] candidates,
        int start,
        int remaining,
        List<Integer> current,
        List<List<Integer>> result) {

    if (remaining == 0) {
        result.add(new ArrayList<>(current));
        return;
    }

    for (int i = start; i < candidates.length; i++) {
        if (candidates[i] > remaining) continue;

        current.add(candidates[i]);
        combinationSum(candidates, i, remaining - candidates[i], current, result);
        current.remove(current.size() - 1);
    }
}
```

## 12.4 N-Queens Mental Model

Place one queen row by row while tracking:

- used columns
- used main diagonals (`row - col`)
- used anti-diagonals (`row + col`)

Backtrack whenever a queen would attack an existing queen.

---

# 13. Searching

Searching asks whether, where, or under what condition a target can be found. Start with linear search as the no-precondition baseline, then use binary search when ordering or monotonicity lets you safely discard large parts of the search space.

## 13.1 Linear Search

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

```java
static int linearSearch(int[] arr, int target) {
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == target) return i;
    }
    return -1;
}
```

Time: `O(n)`.

## 13.2 Binary Search

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

Requires sorted data.

```java
static int binarySearch(int[] arr, int target) {
    int left = 0;
    int right = arr.length - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (arr[mid] == target) return mid;

        if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }

    return -1;
}
```

Time: `O(log n)`.

### Why this midpoint expression?

Using `left + (right - left) / 2` computes the same midpoint as `(left + right) / 2` while avoiding the potentially overflowing addition of two large positive indexes in fixed-width integer languages. The exact integer-division rounding still determines which middle is chosen.

Prefer:

```java
int mid = left + (right - left) / 2;
```

over:

```java
int mid = (left + right) / 2;
```

because `left + right` may overflow for very large indices.

## 13.3 Lower Bound

A lower bound returns the first position whose value is **not less than** the target (equivalently, the insertion position before existing equal values). The binary-search invariant must preserve all possible answers, including the position immediately after the final element when every value is smaller.

Find first index with value `>= target`.

```java
static int lowerBound(int[] arr, int target) {
    int left = 0;
    int right = arr.length;

    while (left < right) {
        int mid = left + (right - left) / 2;

        if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid;
        }
    }

    return left;
}
```

## 13.4 Upper Bound

An upper bound returns the first position whose value is **greater than** the target, which is the insertion position after all existing equal values. It differs from lower bound only in the comparison that decides which half can still contain the answer.

Find first index with value `> target`.

```java
static int upperBound(int[] arr, int target) {
    int left = 0;
    int right = arr.length;

    while (left < right) {
        int mid = left + (right - left) / 2;

        if (arr[mid] <= target) {
            left = mid + 1;
        } else {
            right = mid;
        }
    }

    return left;
}
```

---

# 14. Sorting

Sorting rearranges values according to an ordering rule so later operations can exploit structure. Learn not only the code but also stability, in-place behavior, best/average/worst complexity, comparator requirements, and when a language's built-in sort is preferable to a manual algorithm.

Sorting makes many problems easier by imposing order.

## 14.1 Bubble Sort

Bubble sort repeatedly compares adjacent elements and swaps pairs that are out of order. After each full pass, one extreme value has moved to its final end position. It is easy to learn but `O(n²)` in average/worst cases; with an early-exit flag it can be `O(n)` on already sorted input.

```java
static void bubbleSort(int[] arr) {
    for (int end = arr.length - 1; end > 0; end--) {
        boolean swapped = false;

        for (int i = 0; i < end; i++) {
            if (arr[i] > arr[i + 1]) {
                int temp = arr[i];
                arr[i] = arr[i + 1];
                arr[i + 1] = temp;
                swapped = true;
            }
        }

        if (!swapped) break;
    }
}
```

Time: worst `O(n²)`.

Main value: learning, not production use.

## 14.2 Selection Sort

Selection sort repeatedly chooses the smallest (or largest) remaining element and places it into the next final position. It performs `O(n²)` comparisons regardless of initial order and only `O(n)` swaps, so it is mostly educational or useful when writes are unusually expensive. The usual in-place form is not stable.

```java
static void selectionSort(int[] arr) {
    for (int i = 0; i < arr.length - 1; i++) {
        int minIndex = i;

        for (int j = i + 1; j < arr.length; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }

        int temp = arr[i];
        arr[i] = arr[minIndex];
        arr[minIndex] = temp;
    }
}
```

## 14.3 Insertion Sort

Insertion sort grows a sorted prefix one element at a time. For each new value, it shifts larger prefix elements to the right until the correct insertion position opens. It is stable with the usual comparison, in-place, `O(n²)` in the average/worst case, and `O(n)` on already or nearly sorted data.

Very useful conceptually and efficient for small/nearly sorted data.

```java
static void insertionSort(int[] arr) {
    for (int i = 1; i < arr.length; i++) {
        int current = arr[i];
        int j = i - 1;

        while (j >= 0 && arr[j] > current) {
            arr[j + 1] = arr[j];
            j--;
        }

        arr[j + 1] = current;
    }
}
```

## 14.4 Merge Sort

Merge sort divides the sequence into halves, recursively sorts each half, and merges two sorted halves in linear time. Its recurrence leads to `O(n log n)` time in all standard cases; array implementations typically need `O(n)` auxiliary merge storage. Merge sort is stable when equal elements are taken from the left half first.

Divide array in half, sort both halves, merge them.

```java
static void mergeSort(int[] arr) {
    int[] temp = new int[arr.length];
    mergeSort(arr, temp, 0, arr.length - 1);
}

static void mergeSort(int[] arr, int[] temp, int left, int right) {
    if (left >= right) return;

    int mid = left + (right - left) / 2;
    mergeSort(arr, temp, left, mid);
    mergeSort(arr, temp, mid + 1, right);
    merge(arr, temp, left, mid, right);
}

static void merge(int[] arr, int[] temp, int left, int mid, int right) {
    int i = left;
    int j = mid + 1;
    int k = left;

    while (i <= mid && j <= right) {
        if (arr[i] <= arr[j]) {
            temp[k++] = arr[i++];
        } else {
            temp[k++] = arr[j++];
        }
    }

    while (i <= mid) temp[k++] = arr[i++];
    while (j <= right) temp[k++] = arr[j++];

    for (int p = left; p <= right; p++) {
        arr[p] = temp[p];
    }
}
```

Time: `O(n log n)`.

Space: `O(n)`.

## 14.5 Quick Sort

Quick sort partitions elements around a pivot so smaller and larger values move to opposite sides, then recursively sorts the partitions. Average time is `O(n log n)` but poor pivot choices can produce `O(n²)`. Partition scheme, duplicate handling, and recursion depth are important implementation details.

```java
static void quickSort(int[] arr, int low, int high) {
    if (low >= high) return;

    int pivotIndex = partition(arr, low, high);
    quickSort(arr, low, pivotIndex - 1);
    quickSort(arr, pivotIndex + 1, high);
}

static int partition(int[] arr, int low, int high) {
    int pivot = arr[high];
    int i = low;

    for (int j = low; j < high; j++) {
        if (arr[j] <= pivot) {
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
            i++;
        }
    }

    int temp = arr[i];
    arr[i] = arr[high];
    arr[high] = temp;

    return i;
}
```

Average: `O(n log n)`.

Worst: `O(n²)` if partitioning becomes extremely unbalanced.

## 14.6 Counting Sort Idea

Counting sort is useful when keys are integers from a reasonably small known range. Count each key, then reconstruct output from those counts (or use prefix counts for a stable form). Its complexity is `O(n + k)` for `n` items and key range size `k`, so it is poor when `k` is huge compared with `n`.

Useful when values lie in a small known integer range.

```java
static int[] countingSort(int[] arr, int maxValue) {
    int[] count = new int[maxValue + 1];

    for (int x : arr) {
        count[x]++;
    }

    int[] result = new int[arr.length];
    int index = 0;

    for (int value = 0; value < count.length; value++) {
        while (count[value]-- > 0) {
            result[index++] = value;
        }
    }

    return result;
}
```

## 14.7 Java Built-In Sorting

Sorting all values is often the simplest selection baseline. It is appropriate when ordered output is useful elsewhere or input size is moderate; it does unnecessary work when only one rank is needed and no other sorted-order benefit exists.

```java
Arrays.sort(arr);
```

For object lists:

```java
list.sort(Comparator.naturalOrder());
```

For interviews, know how sorting algorithms work even when production code should usually use standard library sorting.

---

# 15. Two Pointers

Two pointers maintain two indexes or references whose movement eliminates unnecessary repeated work. Common forms are opposite-end pointers on sorted data and same-direction read/write pointers for in-place filtering. The technique is most valuable when pointer movement can be justified by an invariant, such as sorted order or a maintained valid region.

Two pointers use two indexes moving through a sequence.

Common forms:

- opposite directions
- same direction
- slow/fast pointers
- read/write pointers

## 15.1 Pair Sum in Sorted Array

With sorted input, place one pointer at each end. If the sum is too small, moving the left pointer right is the only move that can increase it; if the sum is too large, move the right pointer left. This invariant gives `O(n)` time and `O(1)` extra space after sorting is already available.

```java
static boolean hasPairWithSum(int[] arr, int target) {
    int left = 0;
    int right = arr.length - 1;

    while (left < right) {
        int sum = arr[left] + arr[right];

        if (sum == target) return true;

        if (sum < target) {
            left++;
        } else {
            right--;
        }
    }

    return false;
}
```

Why it works:

- If sum is too small, increase the smaller value.
- If sum is too large, decrease the larger value.

## 15.2 Move Zeros to End

Use a write pointer for the next non-zero position while a read pointer scans the array. Copy/swap non-zero values forward in original order, then fill or leave zeros in the remaining suffix depending on the implementation. This yields `O(n)` time and `O(1)` extra space.

```java
static void moveZeros(int[] nums) {
    int write = 0;

    for (int read = 0; read < nums.length; read++) {
        if (nums[read] != 0) {
            int temp = nums[write];
            nums[write] = nums[read];
            nums[read] = temp;
            write++;
        }
    }
}
```

## 15.3 Container With Most Water Pattern

Key insight:

> Move the pointer at the shorter wall, because moving the taller one cannot improve the limiting height.

---

# 16. Sliding Window

A sliding window tracks a contiguous range while updating only the information that changes when the range expands or shrinks. Fixed-size windows are used when the length is known; variable-size windows adjust a boundary until a validity condition is restored. The usual goal is to replace repeated recomputation of every subarray or substring with a single linear pass.

Sliding window is ideal for contiguous subarray/substring problems.

Two types:

1. Fixed-size window.
2. Variable-size window.

## 16.1 Maximum Sum of k Consecutive Elements

This fixed-window problem demonstrates why sliding windows are useful. Compute the sum of the first `k` values, then each shift subtracts the element leaving the window and adds the new entering element. The result is `O(n)` time instead of recomputing each `k`-element sum in `O(k)`.

```java
static int maxWindowSum(int[] nums, int k) {
    if (k > nums.length) throw new IllegalArgumentException();

    int windowSum = 0;

    for (int i = 0; i < k; i++) {
        windowSum += nums[i];
    }

    int best = windowSum;

    for (int right = k; right < nums.length; right++) {
        windowSum += nums[right];
        windowSum -= nums[right - k];
        best = Math.max(best, windowSum);
    }

    return best;
}
```

Naive approach: `O(nk)`.

Sliding window: `O(n)`.

## 16.2 Longest Substring Without Repeating Characters

Use a variable sliding window that contains no duplicate characters. When a repeated character invalidates the window, advance the left boundary past its previous occurrence (or shrink while updating counts). Each boundary moves forward at most `n` times, giving `O(n)` expected time with a map/set.

```java
static int longestUniqueSubstring(String s) {
    Map<Character, Integer> lastSeen = new HashMap<>();
    int left = 0;
    int best = 0;

    for (int right = 0; right < s.length(); right++) {
        char c = s.charAt(right);

        if (lastSeen.containsKey(c)) {
            left = Math.max(left, lastSeen.get(c) + 1);
        }

        lastSeen.put(c, right);
        best = Math.max(best, right - left + 1);
    }

    return best;
}
```

## 16.3 Smallest Window Meeting a Condition

Generic variable-window template:

```java
int left = 0;

for (int right = 0; right < n; right++) {
    add(arr[right]);

    while (windowIsValid()) {
        updateAnswer();
        remove(arr[left]);
        left++;
    }
}
```

Use this for:

- minimum subarray length
- smallest substring covering a requirement
- at-most-K distinct elements

---

# 17. Prefix Sum and Difference Arrays

Prefix sums and difference arrays are complementary preprocessing techniques. Prefix sums make repeated range queries cheap; difference arrays make many range updates cheap before one final reconstruction. Their correctness depends on a clear indexing convention and careful boundary handling.

## 17.1 Prefix Sum

For:

```text
[2, 4, 1, 7]
```

prefix can be:

```text
[0, 2, 6, 7, 14]
```

where `prefix[i]` stores sum of the first `i` elements.

```java
static long[] prefixSum(int[] nums) {
    long[] prefix = new long[nums.length + 1];

    for (int i = 0; i < nums.length; i++) {
        prefix[i + 1] = prefix[i] + nums[i];
    }

    return prefix;
}
```

Range sum `[left, right]`:

```java
long sum = prefix[right + 1] - prefix[left];
```

After `O(n)` preprocessing, each range query is `O(1)`.

## 17.2 Prefix Sum + HashMap

A prefix sum precomputes cumulative totals so that later range sums can be answered by subtraction. With the common convention `prefix[i] = sum of elements before i`, the sum of the half-open range `[left, right)` is `prefix[right] - prefix[left]`. Building the prefix array costs `O(n)` time and each range query then costs `O(1)`.

Count subarrays whose sum equals `k`:

```java
static int countSubarraysSumK(int[] nums, int k) {
    Map<Long, Integer> count = new HashMap<>();
    count.put(0L, 1);

    long prefix = 0;
    int answer = 0;

    for (int x : nums) {
        prefix += x;
        answer += count.getOrDefault(prefix - k, 0);
        count.put(prefix, count.getOrDefault(prefix, 0) + 1);
    }

    return answer;
}
```

Reason:

```text
prefix[j] - prefix[i] = k
=> prefix[i] = prefix[j] - k
```

## 17.3 Difference Array

A difference array represents the *changes* between positions so that many range updates can be recorded cheaply. A range addition marks where an effect starts and where it stops; one final prefix accumulation reconstructs the resulting values. It is useful when updates are numerous but point-by-point results are only needed after all updates are known.

Useful when performing many range updates.

To add `value` to `[left, right]`:

```java
diff[left] += value;
if (right + 1 < diff.length) {
    diff[right + 1] -= value;
}
```

Recover final values using a prefix sum.

---

# 18. Intervals

Interval problems represent ranges such as time spans, coordinates, or reservations. Before coding, define whether endpoints are inclusive or exclusive and whether touching intervals overlap; that decision controls sorting, merge conditions, sweep-line events, and off-by-one behavior.

Interval problems often become easy after sorting.

## 18.1 Merge Overlapping Intervals

To merge overlapping intervals, first sort by start coordinate. Keep the last merged interval; if the next interval overlaps under the chosen endpoint convention, extend the end, otherwise start a new merged interval. Sorting dominates at `O(n log n)`; the scan itself is `O(n)`.

```java
static int[][] mergeIntervals(int[][] intervals) {
    Arrays.sort(intervals, Comparator.comparingInt(a -> a[0]));

    List<int[]> merged = new ArrayList<>();

    for (int[] current : intervals) {
        if (merged.isEmpty() ||
            merged.get(merged.size() - 1)[1] < current[0]) {
            merged.add(current.clone());
        } else {
            int[] last = merged.get(merged.size() - 1);
            last[1] = Math.max(last[1], current[1]);
        }
    }

    return merged.toArray(new int[merged.size()][]);
}
```

Common scenarios:

- meeting scheduling
- booking overlap
- employee shift ranges
- network time windows

## 18.2 Meeting Rooms Concept

If intervals are sorted by start time, compare each meeting with the previous ending time.

For minimum number of rooms, use a min-heap of end times.

---

# 19. Binary Search on Answer

Sometimes you are not searching an array. You are searching the **answer space**.

Typical form:

> Find the smallest/largest value `x` for which a monotonic condition becomes true.

Template:

```java
long left = minimumPossible;
long right = maximumPossible;

while (left < right) {
    long mid = left + (right - left) / 2;

    if (canAchieve(mid)) {
        right = mid;
    } else {
        left = mid + 1;
    }
}

return left;
```

## 19.1 Example: Minimum Capacity to Ship Packages

Question:

> Given package weights and `days`, what is the minimum ship capacity needed?

Search range:

- lower bound = maximum single package weight
- upper bound = total weight

`canShip(capacity)` is monotonic:

- if capacity works, any larger capacity also works.

This monotonic property makes binary search possible.

---

# 20. Bit Manipulation

Bit manipulation treats an integer as a sequence of binary bits. Operations such as AND (`&`), OR (`|`), XOR (`^`), complement (`~`), and shifts can test or modify individual bits efficiently. Use explicit parentheses around shift expressions when precedence could be unclear, and remember that signed integer width and overflow behavior are language-specific.

Bits are useful for flags, subsets, parity, XOR tricks, and low-level optimizations.

## 20.1 Operators

The main bitwise operators are AND (`&`), OR (`|`), XOR (`^`), NOT (`~`), left shift (`<<`), and right shift (`>>`/language variants). They operate on the binary representation of integers; distinguish them from logical operators such as `&&`/`||` and parenthesize expressions when precedence may be unclear.

| Operator | Meaning |
|---|---|
| `&` | AND |
| `|` | OR |
| `^` | XOR |
| `~` | NOT |
| `<<` | left shift |
| `>>` | signed right shift |
| `>>>` | unsigned right shift |

## 20.2 Check Odd/Even

The least significant binary bit tells parity: it is `1` for odd integers and `0` for even integers. Testing `n & 1` is a constant-time alternative to `n % 2`, although `% 2` is often clearer when bit operations are not otherwise relevant.

```java
boolean isOdd = (n & 1) == 1;
```

## 20.3 Check k-th Bit

To test bit `k`, create a mask `1 << k` and AND it with the number. A non-zero result means that bit is set. State whether bit positions are zero-based and ensure `k` is within the integer width used by the language.

```java
boolean set = (n & (1 << k)) != 0;
```

## 20.4 Set k-th Bit

To set bit `k`, OR the number with the mask `1 << k`. OR leaves all existing `1` bits unchanged and forces the selected bit to `1`. The operation modifies the numeric value but does not affect other bit positions.

```java
n |= (1 << k);
```

## 20.5 Clear k-th Bit

To clear bit `k`, invert the one-bit mask and AND it with the number. The inverted mask has `0` at bit `k` and `1` elsewhere, so only the selected bit is forced to zero. Signed-width/complement behavior follows the language's integer representation.

```java
n &= ~(1 << k);
```

## 20.6 Toggle k-th Bit

To toggle bit `k`, XOR the number with `1 << k`. XOR with `1` flips a bit and XOR with `0` preserves it, so all other bit positions remain unchanged.

```java
n ^= (1 << k);
```

## 20.7 Power of Two

For a positive integer that is a power of two, exactly one bit is set. Therefore `n > 0 && (n & (n - 1)) == 0` detects powers of two because subtracting one flips that single set bit and all lower bits. The positivity check is essential.

For positive `n`:

```java
static boolean isPowerOfTwo(int n) {
    return n > 0 && (n & (n - 1)) == 0;
}
```

## 20.8 Single Number Using XOR

When every value except one appears exactly twice, XOR is useful because `x ^ x = 0` and `x ^ 0 = x`. XORing the full array cancels each duplicate pair, leaving the unique value in `O(n)` time and `O(1)` extra space. This exact trick does not directly solve cases where duplicates appear three times.

If every number appears twice except one:

```java
static int singleNumber(int[] nums) {
    int result = 0;

    for (int x : nums) {
        result ^= x;
    }

    return result;
}
```

Because:

```text
x ^ x = 0
x ^ 0 = x
```

## 20.9 Enumerating Subsets with Bitmasks

An `n`-element set has `2^n` subset masks. For each mask from `0` to `2^n - 1`, bit `i` indicates whether element `i` is included. This is a compact iterative alternative to recursive subset generation, with the same unavoidable `O(n·2^n)` work if every subset is materialized.

```java
static void printSubsets(int[] nums) {
    int n = nums.length;

    for (int mask = 0; mask < (1 << n); mask++) {
        System.out.print("[");

        for (int i = 0; i < n; i++) {
            if ((mask & (1 << i)) != 0) {
                System.out.print(nums[i] + " ");
            }
        }

        System.out.println("]");
    }
}
```

---

# 21. Mathematics for DSA

A small set of mathematical tools appears repeatedly in DSA: modular arithmetic, divisibility, GCD/LCM, primes, logarithms, combinatorics, and exponentiation. The purpose is practical—these tools simplify constraints, prevent overflow, or reduce repeated computation in algorithms.

## 21.1 GCD — Euclidean Algorithm

An algorithm is a finite, unambiguous procedure that converts an input into the required output. A useful explanation of an algorithm should state its preconditions, the main invariant or idea that keeps it correct, when it stops, and its time and space complexity.

```java
static long gcd(long a, long b) {
    while (b != 0) {
        long temp = a % b;
        a = b;
        b = temp;
    }
    return Math.abs(a);
}
```

## 21.2 LCM

The least common multiple (LCM) of two non-zero integers can be derived from the GCD: `lcm(a, b) = |a / gcd(a, b) × b|`. Dividing before multiplying reduces overflow risk in fixed-width languages. Define how your implementation should behave when either input is zero; a common convention returns zero.

```java
static long lcm(long a, long b) {
    return Math.abs(a / gcd(a, b) * b);
}
```

Dividing before multiplying can reduce overflow risk.

## 21.3 Prime Check

The example implements **21.3 Prime Check** with `isPrime(...)`. Its parameters are `int n`. Trace how those inputs change or are read, then inspect the `return` statement (or observable mutation/output) to identify the result. Also account for the cost of any loop, recursion, container operation, or nested call when deriving complexity.

```java
static boolean isPrime(int n) {
    if (n < 2) return false;

    for (int d = 2; 1L * d * d <= n; d++) {
        if (n % d == 0) return false;
    }

    return true;
}
```

Time: `O(sqrt(n))`.

## 21.4 Sieve of Eratosthenes

The Sieve of Eratosthenes finds all primes up to a limit by marking multiples of each discovered prime as composite. Starting the marking at `p × p` is enough because smaller multiples already have a smaller prime factor. The standard implementation runs in `O(n log log n)` time and uses `O(n)` marking space.

Find all primes up to `n`.

```java
static boolean[] sieve(int n) {
    boolean[] prime = new boolean[n + 1];
    Arrays.fill(prime, true);

    if (n >= 0) prime[0] = false;
    if (n >= 1) prime[1] = false;

    for (int p = 2; 1L * p * p <= n; p++) {
        if (!prime[p]) continue;

        for (int multiple = p * p; multiple <= n; multiple += p) {
            prime[multiple] = false;
        }
    }

    return prime;
}
```

## 21.5 Fast Exponentiation

Fast exponentiation computes `base^exp` by repeatedly squaring the base and using the binary representation of the exponent. Each step halves the remaining exponent, reducing multiplication count from `O(exp)` to `O(log exp)`. A modular variant applies `% mod` after multiplications to keep values bounded.

Compute `base^exponent` in `O(log exponent)`.

```java
static long power(long base, long exponent) {
    long result = 1;

    while (exponent > 0) {
        if ((exponent & 1) == 1) {
            result *= base;
        }

        base *= base;
        exponent >>= 1;
    }

    return result;
}
```

## 21.6 Modular Arithmetic

Modular arithmetic keeps values within a fixed remainder range and is common in counting problems or large exponentiation. Addition and multiplication can usually be reduced after each operation, but division requires a modular inverse and is not equivalent to ordinary integer division.

Common competitive-programming modulus:

```java
static final long MOD = 1_000_000_007L;
```

Rules:

```text
(a + b) mod m = ((a mod m) + (b mod m)) mod m
(a * b) mod m = ((a mod m) * (b mod m)) mod m
```

---

# 22. Trees

A tree is a connected acyclic hierarchical structure with nodes linked by parent/child relationships. Tree algorithms are easiest to understand recursively: define what one subtree call returns, choose a traversal order, and account for tree height because recursion/operation cost can degrade on skewed trees.

A tree is a connected acyclic structure.

A binary tree node:

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;

    TreeNode(int val) {
        this.val = val;
    }
}
```

## 22.1 Tree Terminology

- Root — top node.
- Parent — node directly above another.
- Child — node directly below another.
- Leaf — node with no children.
- Depth — edges from root to node.
- Height — longest path downward to a leaf.
- Subtree — node plus all descendants.

## 22.2 DFS Traversals

Depth-first search explores one branch as far as possible before returning to try another branch. It can be implemented recursively or with an explicit stack and is widely used for connected components, cycle detection, tree processing, path exploration, topological reasoning, and many backtracking-style searches. Track visited state in cyclic graphs to avoid endless revisits.

### Preorder

Preorder traversal visits **node → left subtree → right subtree**. It is useful when the parent must be processed before its children, such as copying a tree, serializing certain tree formats, or producing prefix-style expression order. A complete traversal visits every node once, so time is `O(n)`.

```text
Root -> Left -> Right
```

```java
static void preorder(TreeNode root) {
    if (root == null) return;

    System.out.print(root.val + " ");
    preorder(root.left);
    preorder(root.right);
}
```

### Inorder

Inorder traversal visits **left subtree → node → right subtree**. On a Binary Search Tree with a consistent ordering rule, this produces keys in sorted order. A complete traversal is `O(n)` time and uses `O(h)` call-stack/explicit-stack space for tree height `h`.

```text
Left -> Root -> Right
```

```java
static void inorder(TreeNode root) {
    if (root == null) return;

    inorder(root.left);
    System.out.print(root.val + " ");
    inorder(root.right);
}
```

### Postorder

Postorder traversal visits **left subtree → right subtree → node**. Because children are processed before their parent, it is useful for deleting trees, computing subtree aggregates, and many tree-DP problems. A complete traversal is `O(n)` time and uses `O(h)` traversal stack space.

```text
Left -> Right -> Root
```

```java
static void postorder(TreeNode root) {
    if (root == null) return;

    postorder(root.left);
    postorder(root.right);
    System.out.print(root.val + " ");
}
```

## 22.3 Level-Order Traversal — BFS

Traversal means visiting each relevant element/node in a defined order. The important state is the current position and the rule for advancing to the next one. A full traversal is usually `O(n)` for a linear structure, while trees/graphs additionally require a stack/queue or recursion and, for cyclic graphs, visited tracking.

```java
static List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> result = new ArrayList<>();
    if (root == null) return result;

    Queue<TreeNode> queue = new ArrayDeque<>();
    queue.offer(root);

    while (!queue.isEmpty()) {
        int levelSize = queue.size();
        List<Integer> level = new ArrayList<>();

        for (int i = 0; i < levelSize; i++) {
            TreeNode node = queue.poll();
            level.add(node.val);

            if (node.left != null) queue.offer(node.left);
            if (node.right != null) queue.offer(node.right);
        }

        result.add(level);
    }

    return result;
}
```

## 22.4 Maximum Depth

Maximum tree depth is the number of nodes (or edges, depending on the chosen convention) on the longest root-to-leaf path. A recursive solution returns `1 + max(leftDepth, rightDepth)` for a non-null node. It visits each node once: `O(n)` time and `O(h)` stack space.

```java
static int maxDepth(TreeNode root) {
    if (root == null) return 0;

    return 1 + Math.max(
        maxDepth(root.left),
        maxDepth(root.right)
    );
}
```

## 22.5 Count Nodes

Counting tree nodes is a postorder-style recursion: the count for a non-null node is `1 + count(left) + count(right)`, while an empty subtree contributes zero. Every node is visited once, giving `O(n)` time and `O(h)` recursion stack space.

```java
static int countNodes(TreeNode root) {
    if (root == null) return 0;
    return 1 + countNodes(root.left) + countNodes(root.right);
}
```

## 22.6 Diameter of a Binary Tree

The **diameter** is the length of the longest path between two tree nodes under the problem's chosen unit (usually edges, sometimes nodes). A postorder DFS can return each subtree's height while updating the best `leftHeight + rightHeight` path seen at each node. Every node is processed once, so the usual solution is `O(n)` time with `O(h)` recursion-stack space for tree height `h`.

Diameter is often measured as the maximum number of edges on any path between two nodes.

```java
static int diameter(TreeNode root) {
    int[] best = new int[1];
    heightForDiameter(root, best);
    return best[0];
}

static int heightForDiameter(TreeNode node, int[] best) {
    if (node == null) return 0;

    int leftHeight = heightForDiameter(node.left, best);
    int rightHeight = heightForDiameter(node.right, best);

    best[0] = Math.max(best[0], leftHeight + rightHeight);

    return 1 + Math.max(leftHeight, rightHeight);
}
```

## 22.7 Lowest Common Ancestor in a Binary Tree

The lowest common ancestor (LCA) is the deepest node whose subtree contains both targets. A recursive binary-tree solution returns a target when found; if left and right recursive results are both non-null, the current node is the LCA. Clarify whether both target nodes are guaranteed to exist.

```java
static TreeNode lowestCommonAncestor(
        TreeNode root,
        TreeNode p,
        TreeNode q) {

    if (root == null || root == p || root == q) {
        return root;
    }

    TreeNode left = lowestCommonAncestor(root.left, p, q);
    TreeNode right = lowestCommonAncestor(root.right, p, q);

    if (left != null && right != null) return root;
    return left != null ? left : right;
}
```

---

# 23. Binary Search Trees

A Binary Search Tree (BST) maintains an ordering invariant: values in one subtree compare before the node and values in the other compare after it, according to the chosen duplicate policy. Operations depend on tree height, so an unbalanced BST can degrade from `O(log n)` expected/balanced behavior to `O(n)`.

A BST maintains an ordering property.

Common convention:

```text
left subtree < node < right subtree
```

## 23.1 Search

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

```java
static TreeNode searchBST(TreeNode root, int target) {
    while (root != null) {
        if (root.val == target) return root;

        if (target < root.val) {
            root = root.left;
        } else {
            root = root.right;
        }
    }

    return null;
}
```

Average in a balanced tree: `O(log n)`.

Worst in a skewed tree: `O(n)`.

## 23.2 Insert

Insertion must preserve the data structure's invariant. For an ordered tree, compare the new key at each node and descend to the appropriate child until an empty position is found; for duplicate keys, follow the policy defined by the problem. Runtime is proportional to the structure's height.

```java
static TreeNode insertBST(TreeNode root, int value) {
    if (root == null) return new TreeNode(value);

    if (value < root.val) {
        root.left = insertBST(root.left, value);
    } else if (value > root.val) {
        root.right = insertBST(root.right, value);
    }

    return root;
}
```

## 23.3 Validate BST

Validating a BST requires checking the **entire allowed range** for each node, not only comparing a node with its immediate children. Pass lower/upper bounds (or use inorder ordering) so descendants cannot violate an ancestor's constraint. Decide how duplicates are handled before choosing strict or non-strict comparisons.

Use bounds rather than only comparing a node with its immediate children.

```java
static boolean isValidBST(TreeNode root) {
    return validate(root, Long.MIN_VALUE, Long.MAX_VALUE);
}

static boolean validate(TreeNode node, long low, long high) {
    if (node == null) return true;

    if (node.val <= low || node.val >= high) return false;

    return validate(node.left, low, node.val) &&
           validate(node.right, node.val, high);
}
```

## 23.4 Inorder of a BST

Inorder traversal visits **left subtree → node → right subtree**. On a Binary Search Tree with a consistent ordering rule, this produces keys in sorted order. A complete traversal is `O(n)` time and uses `O(h)` call-stack/explicit-stack space for tree height `h`.

Inorder traversal yields values in sorted order.

This observation is extremely useful in BST interview problems.

---

# 24. Heaps and Priority Queues

A heap efficiently keeps track of the smallest or largest priority element.

Java's `PriorityQueue` is a **min-heap** by default.

```java
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
```

Max-heap:

```java
PriorityQueue<Integer> maxHeap =
    new PriorityQueue<>(Comparator.reverseOrder());
```

## 24.1 Complexity

| Operation | Complexity |
|---|---:|
| Peek min/max | `O(1)` |
| Insert | `O(log n)` |
| Remove top | `O(log n)` |
| Build heap from collection | typically `O(n)` |

## 24.2 Kth Largest Element

A min-heap of size `k` is a common way to find the kth largest value: after processing all elements, the heap root is the kth largest. Complexity is `O(n log k)` time and `O(k)` space. Quickselect can achieve `O(n)` average time when mutation and worst-case trade-offs are acceptable.

Maintain a min-heap of size `k`.

```java
static int kthLargest(int[] nums, int k) {
    PriorityQueue<Integer> heap = new PriorityQueue<>();

    for (int x : nums) {
        heap.offer(x);

        if (heap.size() > k) {
            heap.poll();
        }
    }

    return heap.peek();
}
```

Time: `O(n log k)`.

## 24.3 Top K Frequent Elements

Count frequencies first, then keep or select the `k` highest-frequency keys. A heap gives `O(u log k)` after counting `u` unique values; bucket-by-frequency can be linear in `n` with more memory. Decide how ties should be handled if the problem requires deterministic ordering.

A typical strategy:

1. Count frequencies with `HashMap`.
2. Maintain heap based on frequency.

## 24.4 Merge K Sorted Lists

A min-heap can always expose the smallest current head among the `k` lists.

This reduces the repeated global search from `O(k)` per extraction to `O(log k)`.

---

# 25. Trie

A trie stores keys by shared prefixes. Each step consumes one symbol, so lookup time depends mainly on key length rather than on the number of stored keys. Tries are useful for autocomplete, prefix counting, dictionary search, and word-grid problems, but they can use substantially more memory than a hash-based set or map.

A trie is a prefix tree for strings.

Useful for:

- autocomplete
- dictionary lookup
- prefix search
- word games
- routing by string prefix

## 25.1 Trie Implementation

This implementation turns the surrounding concept into concrete state and operations. Identify what each field stores, which method mutates that state, and what invariant must remain true after every operation; those details matter more than memorizing the exact syntax.

```java
class Trie {
    private static class Node {
        Node[] children = new Node[26];
        boolean endOfWord;
    }

    private final Node root = new Node();

    void insert(String word) {
        Node current = root;

        for (char c : word.toCharArray()) {
            int index = c - 'a';

            if (current.children[index] == null) {
                current.children[index] = new Node();
            }

            current = current.children[index];
        }

        current.endOfWord = true;
    }

    boolean search(String word) {
        Node node = findNode(word);
        return node != null && node.endOfWord;
    }

    boolean startsWith(String prefix) {
        return findNode(prefix) != null;
    }

    private Node findNode(String text) {
        Node current = root;

        for (char c : text.toCharArray()) {
            int index = c - 'a';
            current = current.children[index];
            if (current == null) return null;
        }

        return current;
    }
}
```

For Unicode or broad character sets, a `Map<Character, Node>` may be more appropriate than a fixed array.

---

# 26. Graphs

A graph models entities as vertices and relationships as edges. Before choosing an algorithm, determine whether the graph is directed or undirected, weighted or unweighted, cyclic or acyclic, and connected or disconnected. Those properties decide whether BFS, DFS, topological sorting, shortest-path algorithms, minimum-spanning-tree algorithms, or connectivity structures are appropriate.

A graph consists of:

- vertices/nodes
- edges

Graphs may be:

- directed or undirected
- weighted or unweighted
- connected or disconnected
- cyclic or acyclic

## 26.1 Graph Representation

A graph representation determines the cost of storage and neighbor access. Adjacency lists use `O(V + E)` space and are usually best for sparse graphs; adjacency matrices use `O(V²)` space but make edge-existence checks constant-time. Include edge weights with each neighbor when the graph is weighted.

### Adjacency List

An adjacency list stores, for each vertex, the vertices (and optionally edge weights) directly connected to it. It uses `O(V + E)` space and is usually preferred for sparse graphs because traversing a vertex touches only its actual outgoing/incident edges. For undirected graphs, each edge is normally stored in both endpoint lists.

```java
List<List<Integer>> graph = new ArrayList<>();

for (int i = 0; i < n; i++) {
    graph.add(new ArrayList<>());
}

graph.get(u).add(v);
graph.get(v).add(u); // only for undirected graph
```

This is usually preferred for sparse graphs.

### Adjacency Matrix

An adjacency matrix uses a `V × V` table where one cell records whether or with what weight an edge connects two vertices. Edge existence is `O(1)` to check, but memory is `O(V²)` even for sparse graphs. It is useful for dense graphs or algorithms that naturally work with all vertex pairs.

```java
int[][] graph = new int[n][n];
```

Useful when:

- graph is dense
- constant-time edge existence checks are important

Memory: `O(V²)`.

## 26.2 Breadth-First Search

Breadth-first search explores a graph or tree level by level using a queue. In an unweighted graph, the first time BFS reaches a vertex is through a path with the minimum number of edges from the start. With adjacency-list representation, a complete traversal is `O(V + E)` when each vertex is processed once.

BFS explores by distance layers.

```java
static void bfs(List<List<Integer>> graph, int start) {
    boolean[] visited = new boolean[graph.size()];
    Queue<Integer> queue = new ArrayDeque<>();

    visited[start] = true;
    queue.offer(start);

    while (!queue.isEmpty()) {
        int node = queue.poll();
        System.out.print(node + " ");

        for (int neighbor : graph.get(node)) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                queue.offer(neighbor);
            }
        }
    }
}
```

Use BFS for shortest path in an **unweighted** graph.

## 26.3 Depth-First Search

Depth-first search explores one branch as far as possible before returning to try another branch. It can be implemented recursively or with an explicit stack and is widely used for connected components, cycle detection, tree processing, path exploration, topological reasoning, and many backtracking-style searches. Track visited state in cyclic graphs to avoid endless revisits.

```java
static void dfs(
        List<List<Integer>> graph,
        int node,
        boolean[] visited) {

    visited[node] = true;
    System.out.print(node + " ");

    for (int neighbor : graph.get(node)) {
        if (!visited[neighbor]) {
            dfs(graph, neighbor, visited);
        }
    }
}
```

## 26.4 Connected Components

A connected component is a maximal group of vertices reachable from one another (for the relevant directed/undirected definition). Scan all vertices; whenever an unvisited vertex is found, run BFS/DFS to mark one new component. Across the entire graph, adjacency-list traversal is `O(V + E)`.

```java
static int countComponents(List<List<Integer>> graph) {
    boolean[] visited = new boolean[graph.size()];
    int components = 0;

    for (int node = 0; node < graph.size(); node++) {
        if (!visited[node]) {
            components++;
            dfs(graph, node, visited);
        }
    }

    return components;
}
```

## 26.5 Cycle Detection in Undirected Graph

In an undirected graph, DFS/BFS can detect a cycle by seeing an already visited neighbor that is **not** the edge back to the current vertex's parent. Union-Find is another option when edges are processed incrementally: an edge joining two vertices already in the same set closes a cycle.

DFS must remember the parent.

```java
static boolean hasUndirectedCycle(
        List<List<Integer>> graph,
        int node,
        int parent,
        boolean[] visited) {

    visited[node] = true;

    for (int neighbor : graph.get(node)) {
        if (!visited[neighbor]) {
            if (hasUndirectedCycle(graph, neighbor, node, visited)) {
                return true;
            }
        } else if (neighbor != parent) {
            return true;
        }
    }

    return false;
}
```

## 26.6 Cycle Detection in Directed Graph

In a directed graph, a DFS detects a cycle when it reaches a vertex currently on the active recursion path (often tracked with a color or `inStack` flag). A previously visited vertex that is no longer active is not by itself a cycle. Kahn's topological algorithm can also detect a cycle when fewer than `V` vertices are processed.

Use states:

- `0` = unvisited
- `1` = currently in recursion path
- `2` = fully processed

```java
static boolean hasDirectedCycle(
        List<List<Integer>> graph,
        int node,
        int[] state) {

    state[node] = 1;

    for (int neighbor : graph.get(node)) {
        if (state[neighbor] == 1) return true;

        if (state[neighbor] == 0 &&
            hasDirectedCycle(graph, neighbor, state)) {
            return true;
        }
    }

    state[node] = 2;
    return false;
}
```

## 26.7 Topological Sort — Kahn's Algorithm

A topological ordering places every prerequisite before the items that depend on it. It exists only for a **directed acyclic graph (DAG)**. Common implementations use Kahn's algorithm with indegrees and a queue, or DFS with postorder; if all vertices cannot be ordered, the dependency graph contains a cycle.

Only defined for DAGs.

```java
static List<Integer> topologicalSort(List<List<Integer>> graph) {
    int n = graph.size();
    int[] indegree = new int[n];

    for (int u = 0; u < n; u++) {
        for (int v : graph.get(u)) {
            indegree[v]++;
        }
    }

    Queue<Integer> queue = new ArrayDeque<>();

    for (int i = 0; i < n; i++) {
        if (indegree[i] == 0) queue.offer(i);
    }

    List<Integer> order = new ArrayList<>();

    while (!queue.isEmpty()) {
        int u = queue.poll();
        order.add(u);

        for (int v : graph.get(u)) {
            if (--indegree[v] == 0) {
                queue.offer(v);
            }
        }
    }

    if (order.size() != n) {
        return Collections.emptyList(); // cycle exists
    }

    return order;
}
```

Scenario:

- course prerequisites
- build dependencies
- workflow dependencies

## 26.8 Grid as a Graph

A matrix can be treated as a graph where each cell is a node.

Directions:

```java
int[][] dirs = {
    {1, 0},
    {-1, 0},
    {0, 1},
    {0, -1}
};
```

Typical problems:

- number of islands
- flood fill
- shortest path in a maze
- connected regions

---

# 27. Disjoint Set Union

Also called:

- Union-Find
- DSU

It efficiently tracks connected components as edges are added.

Two key optimizations:

1. Path compression.
2. Union by size/rank.

```java
class DSU {
    private final int[] parent;
    private final int[] size;

    DSU(int n) {
        parent = new int[n];
        size = new int[n];

        for (int i = 0; i < n; i++) {
            parent[i] = i;
            size[i] = 1;
        }
    }

    int find(int x) {
        if (parent[x] != x) {
            parent[x] = find(parent[x]);
        }
        return parent[x];
    }

    boolean union(int a, int b) {
        int rootA = find(a);
        int rootB = find(b);

        if (rootA == rootB) return false;

        if (size[rootA] < size[rootB]) {
            int temp = rootA;
            rootA = rootB;
            rootB = temp;
        }

        parent[rootB] = rootA;
        size[rootA] += size[rootB];
        return true;
    }
}
```

Uses:

- cycle detection
- connected components
- Kruskal's MST
- account merging
- dynamic connectivity

With optimizations, operations are effectively near-constant amortized time.

---

# 28. Greedy Algorithms

A greedy algorithm commits to a locally best-looking choice without revisiting earlier decisions. That can be very efficient, but it is correct only when the problem has a property that makes local choices compatible with a global optimum. A convincing greedy solution should include a justification such as an exchange argument, cut property, or invariant—not merely an intuition that the choice looks best.

A greedy algorithm makes the locally best choice at each step.

Important warning:

> A greedy choice must be justified. “It feels optimal” is not a proof.

## 28.1 Activity Selection

For the classic maximum-number-of-non-overlapping-intervals problem, sorting by finishing time and repeatedly choosing the earliest finishing compatible interval is optimal. The greedy choice leaves as much room as possible for future intervals; sorting dominates at `O(n log n)`.

Goal: attend maximum number of non-overlapping meetings.

Greedy strategy:

> Always choose the compatible meeting that finishes earliest.

Why?

It leaves the greatest remaining time for future meetings.

## 28.2 Fractional Knapsack

For divisible items, sort by value/weight ratio descending.

This greedy method is optimal for fractional knapsack.

It is **not** generally correct for 0/1 knapsack.

## 28.3 Jump Game

The greedy Jump Game invariant stores the farthest index reachable from any position processed so far. If the scan reaches an index beyond that frontier, the path is impossible; otherwise update the frontier with `i + nums[i]`. The scan is `O(n)` time and `O(1)` extra space.

Track the farthest reachable index.

```java
static boolean canJump(int[] nums) {
    int farthest = 0;

    for (int i = 0; i < nums.length; i++) {
        if (i > farthest) return false;

        farthest = Math.max(farthest, i + nums[i]);
    }

    return true;
}
```

## 28.4 Greedy Recognition Clues

Consider greedy when:

- sorting reveals an obvious local choice
- objective involves earliest finish/latest start
- each choice permanently simplifies the remainder
- an exchange argument can show another optimal solution can adopt the greedy choice

---

# 29. Dynamic Programming

Dynamic programming is useful when many candidate solutions reuse the same subproblems and the answer can be composed from smaller states. The core design work is to define the **state**, derive the **transition**, set correct **base cases**, and choose an evaluation order. Memoization computes states on demand; tabulation computes them in an explicit order.

Dynamic Programming (DP) is used when:

1. Problems have overlapping subproblems.
2. Optimal solutions can be built from smaller optimal solutions.

Two styles:

- Top-down memoization.
- Bottom-up tabulation.

## 29.1 Fibonacci with Memoization

Memoized Fibonacci stores the result for each `n` the first time it is computed. Later calls return the cached value instead of expanding the same recursive subtree again, reducing exponential recursion to `O(n)` distinct states and `O(n)` memo/stack space.

```java
static long fibMemo(int n, long[] memo) {
    if (n <= 1) return n;

    if (memo[n] != -1) return memo[n];

    memo[n] = fibMemo(n - 1, memo) + fibMemo(n - 2, memo);
    return memo[n];
}
```

Usage:

```java
long[] memo = new long[n + 1];
Arrays.fill(memo, -1);
long answer = fibMemo(n, memo);
```

## 29.2 Fibonacci Tabulation

Tabulated Fibonacci builds answers from the base cases upward. Each state uses the previous two values, so a full table costs `O(n)` space but can be reduced to two rolling variables when earlier states are no longer needed. Runtime is `O(n)`.

```java
static long fibTab(int n) {
    if (n <= 1) return n;

    long[] dp = new long[n + 1];
    dp[1] = 1;

    for (int i = 2; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }

    return dp[n];
}
```

## 29.3 Space Optimization

Space optimization removes DP states that are no longer needed. If `dp[i]` depends only on a fixed number of earlier rows/values, replace the full table with rolling variables or a small rolling array. Do this only after the full state transition is correct, because update order can accidentally overwrite a dependency.

```java
static long fibOptimized(int n) {
    if (n <= 1) return n;

    long prev2 = 0;
    long prev1 = 1;

    for (int i = 2; i <= n; i++) {
        long current = prev1 + prev2;
        prev2 = prev1;
        prev1 = current;
    }

    return prev1;
}
```

## 29.4 Climbing Stairs

Climbing Stairs is a simple DP model: if the final move can be one or two steps, the number of ways to reach step `i` is the sum of the ways to reach `i-1` and `i-2`. Define base cases carefully; conventions for `n = 0` depend on whether 'do nothing' counts as one valid way.

If you may climb 1 or 2 steps:

```text
dp[i] = dp[i - 1] + dp[i - 2]
```

The important skill is deriving the recurrence from the final decision.

## 29.5 House Robber

House Robber is a take/skip DP. For each house, compare skipping it (keep the previous best) with taking it (add its value to the best solution that excludes the adjacent previous house). Only the previous two DP values are needed, so the common optimized solution is `O(n)` time and `O(1)` extra space.

At each house:

- skip it
- rob it and combine with best result two houses earlier

```java
static int rob(int[] nums) {
    int prev2 = 0;
    int prev1 = 0;

    for (int money : nums) {
        int current = Math.max(prev1, prev2 + money);
        prev2 = prev1;
        prev1 = current;
    }

    return prev1;
}
```

## 29.6 0/1 Knapsack

Each item can be taken at most once.

State:

```text
dp[i][capacity]
```

Meaning:

> Best value using the first `i` items with given capacity.

Transition:

```text
skip item
or
use item + best remaining capacity
```

Space-optimized Java:

```java
static int knapsack(int[] weight, int[] value, int capacity) {
    int[] dp = new int[capacity + 1];

    for (int i = 0; i < weight.length; i++) {
        for (int c = capacity; c >= weight[i]; c--) {
            dp[c] = Math.max(dp[c], value[i] + dp[c - weight[i]]);
        }
    }

    return dp[capacity];
}
```

Why iterate capacity backward?

To prevent using the same item multiple times in the same iteration.

## 29.7 Unbounded Knapsack

Unbounded knapsack allows an item to be selected more than once. In one-dimensional tabulation, the loop direction is important: iterating capacities upward allows the current item to contribute repeatedly to later states. This differs from 0/1 knapsack, where downward capacity iteration prevents reusing the same item in one iteration.

If each item can be reused, iterate capacity forward.

This direction difference is a major DP pattern.

## 29.8 Coin Change — Minimum Coins

The minimum-coin problem asks for the fewest coins needed to form each amount. A common DP state stores the best answer for amount `x`; each coin proposes `1 + dp[x - coin]` when that smaller amount is reachable. Use a sentinel larger than any possible answer and distinguish 'unreachable' from a valid zero-coin base case.

```java
static int minCoins(int[] coins, int amount) {
    int impossible = amount + 1;
    int[] dp = new int[amount + 1];
    Arrays.fill(dp, impossible);
    dp[0] = 0;

    for (int current = 1; current <= amount; current++) {
        for (int coin : coins) {
            if (coin <= current) {
                dp[current] = Math.min(
                    dp[current],
                    1 + dp[current - coin]
                );
            }
        }
    }

    return dp[amount] == impossible ? -1 : dp[amount];
}
```

## 29.9 Longest Common Subsequence

The Longest Common Subsequence (LCS) asks for the longest sequence that appears in two inputs in the same relative order, without requiring contiguity. A classic DP state `dp[i][j]` describes prefixes of the two sequences: matching symbols extend the answer; otherwise the transition skips one side. The standard table takes `O(mn)` time.

State:

```text
dp[i][j] = LCS length of prefixes a[0..i-1], b[0..j-1]
```

Transition:

```java
if (a.charAt(i - 1) == b.charAt(j - 1)) {
    dp[i][j] = 1 + dp[i - 1][j - 1];
} else {
    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
}
```

## 29.10 Longest Increasing Subsequence

The Longest Increasing Subsequence (LIS) keeps elements in original order but not necessarily contiguously. A simple DP is `O(n²)`; a tails/binary-search method maintains the smallest possible tail for each subsequence length and runs in `O(n log n)`. The tails array is not necessarily the actual LIS unless predecessor information is also stored.

Classic `O(n²)` DP:

```java
static int lisQuadratic(int[] nums) {
    int n = nums.length;
    int[] dp = new int[n];
    Arrays.fill(dp, 1);

    int best = 0;

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < i; j++) {
            if (nums[j] < nums[i]) {
                dp[i] = Math.max(dp[i], dp[j] + 1);
            }
        }
        best = Math.max(best, dp[i]);
    }

    return best;
}
```

Advanced version uses binary search in `O(n log n)`.

## 29.11 Grid DP

Grid DP stores the best/count answer for each cell based on previously solved neighboring cells. The allowed movement determines the transition and valid evaluation order. When movement is only right/down, row-major or column-major tabulation is usually straightforward; if arbitrary cycles are allowed, the problem may be a graph problem rather than simple DP.

Typical state:

```text
dp[row][col]
```

Examples:

- number of paths
- minimum path sum
- maximum collected value
- obstacle navigation

## 29.12 DP Design Checklist

When designing DP, answer:

1. What does one state mean?
2. What parameters uniquely describe a subproblem?
3. What are the choices?
4. What is the recurrence?
5. What are the base cases?
6. In what order can states be computed?
7. Can memory be reduced?

---

# 30. Monotonic Stack and Queue

Monotonic stacks and queues maintain candidates in sorted order while processing a sequence. They turn many 'nearest greater/smaller' and sliding-window extrema problems into linear time because each element is inserted and removed only a constant number of times.

A monotonic structure maintains values in increasing or decreasing order.

## 30.1 Next Greater Element

Next-greater-element problems ask for the first later value that exceeds the current value. A decreasing monotonic stack stores unresolved indexes/values; when a larger value arrives, it resolves stack entries until monotonic order is restored. Each item is pushed and popped at most once, so the scan is `O(n)`.

```java
static int[] nextGreater(int[] nums) {
    int n = nums.length;
    int[] answer = new int[n];
    Arrays.fill(answer, -1);

    Deque<Integer> stack = new ArrayDeque<>();

    for (int i = 0; i < n; i++) {
        while (!stack.isEmpty() && nums[stack.peek()] < nums[i]) {
            answer[stack.pop()] = nums[i];
        }

        stack.push(i);
    }

    return answer;
}
```

The stack stores indexes whose answer has not yet been found.

## 30.2 Largest Rectangle in Histogram

This classic problem uses a monotonic increasing stack to find how far each bar can extend before meeting a smaller bar.

## 30.3 Sliding Window Maximum

A sliding window tracks a contiguous range while updating only the information that changes when the range expands or shrinks. Fixed-size windows are used when the length is known; variable-size windows adjust a boundary until a validity condition is restored. The usual goal is to replace repeated recomputation of every subarray or substring with a single linear pass.

Use a deque of indexes whose values are decreasing.

```java
static int[] maxSlidingWindow(int[] nums, int k) {
    int n = nums.length;
    int[] result = new int[n - k + 1];
    Deque<Integer> deque = new ArrayDeque<>();
    int out = 0;

    for (int right = 0; right < n; right++) {
        while (!deque.isEmpty() && deque.peekFirst() <= right - k) {
            deque.pollFirst();
        }

        while (!deque.isEmpty() && nums[deque.peekLast()] <= nums[right]) {
            deque.pollLast();
        }

        deque.offerLast(right);

        if (right >= k - 1) {
            result[out++] = nums[deque.peekFirst()];
        }
    }

    return result;
}
```

Time: `O(n)` because each index enters and leaves the deque at most once.

---

# 31. Advanced Range Data Structures

Range-query structures are useful when an array changes and you still need repeated queries such as sums, minima, maxima, or other associative aggregates. Fenwick trees are compact and excellent for prefix-style operations; segment trees are more general and can support complex queries and lazy range updates.

## 31.1 Fenwick Tree / Binary Indexed Tree

A Fenwick Tree stores partial prefix aggregates in a compact array indexed by the least-significant set bit. Point updates and prefix-sum queries both take `O(log n)`, and a range sum is the difference of two prefix sums. Most implementations use 1-based internal indexing even when the input array is 0-based.

Supports:

- point update
- prefix sum query

both in `O(log n)`.

```java
class FenwickTree {
    private final long[] bit;

    FenwickTree(int n) {
        bit = new long[n + 1];
    }

    void add(int index, long delta) {
        for (int i = index + 1; i < bit.length; i += i & -i) {
            bit[i] += delta;
        }
    }

    long prefixSum(int index) {
        long sum = 0;

        for (int i = index + 1; i > 0; i -= i & -i) {
            sum += bit[i];
        }

        return sum;
    }

    long rangeSum(int left, int right) {
        return prefixSum(right) - (left == 0 ? 0 : prefixSum(left - 1));
    }
}
```

Use when data changes and many prefix/range sums are requested.

## 31.2 Segment Tree

A segment tree supports flexible range queries and updates.

Common operations:

- sum
- minimum
- maximum
- gcd

Typical complexities:

- Build: `O(n)`
- Point update: `O(log n)`
- Range query: `O(log n)`

```java
class SegmentTree {
    private final long[] tree;
    private final int n;

    SegmentTree(int[] nums) {
        n = nums.length;
        tree = new long[4 * Math.max(1, n)];
        if (n > 0) build(nums, 1, 0, n - 1);
    }

    private void build(int[] nums, int node, int left, int right) {
        if (left == right) {
            tree[node] = nums[left];
            return;
        }

        int mid = left + (right - left) / 2;
        build(nums, node * 2, left, mid);
        build(nums, node * 2 + 1, mid + 1, right);
        tree[node] = tree[node * 2] + tree[node * 2 + 1];
    }

    long query(int ql, int qr) {
        return query(1, 0, n - 1, ql, qr);
    }

    private long query(int node, int left, int right, int ql, int qr) {
        if (qr < left || right < ql) return 0;
        if (ql <= left && right <= qr) return tree[node];

        int mid = left + (right - left) / 2;
        return query(node * 2, left, mid, ql, qr)
             + query(node * 2 + 1, mid + 1, right, ql, qr);
    }
}
```

## 31.3 Lazy Propagation

When updates affect an entire range, a regular segment tree may repeatedly visit many nodes.

Lazy propagation delays pushing updates to children until necessary.

Typical operations:

- range add
- range assign
- range sum/min/max query

Learn it only after mastering normal segment trees.

## 31.4 Sparse Table

Useful for static arrays where:

- there are many queries
- there are no updates
- operation is idempotent, such as `min`, `max`, or `gcd`

Can answer Range Minimum Query in `O(1)` after `O(n log n)` preprocessing.

---

# 32. Advanced String Algorithms

Advanced string algorithms avoid repeatedly rechecking the same characters. Techniques such as KMP, Z, rolling hash, tries, suffix structures, and prefix functions are chosen based on whether the task needs exact pattern search, many prefix queries, repeated substring comparison, or indexing of a large text collection.

## 32.1 Naive Pattern Matching

For text length `n` and pattern length `m`, checking every alignment can take `O(nm)`.

## 32.2 KMP — Knuth-Morris-Pratt

KMP avoids re-checking text characters by using information about the pattern itself.

It builds an LPS array:

> `lps[i]` = length of the longest proper prefix of `pattern[0..i]` that is also a suffix.

```java
static int[] buildLps(String pattern) {
    int[] lps = new int[pattern.length()];
    int length = 0;

    for (int i = 1; i < pattern.length();) {
        if (pattern.charAt(i) == pattern.charAt(length)) {
            lps[i++] = ++length;
        } else if (length > 0) {
            length = lps[length - 1];
        } else {
            lps[i++] = 0;
        }
    }

    return lps;
}

static int kmpSearch(String text, String pattern) {
    if (pattern.isEmpty()) return 0;

    int[] lps = buildLps(pattern);
    int i = 0;
    int j = 0;

    while (i < text.length()) {
        if (text.charAt(i) == pattern.charAt(j)) {
            i++;
            j++;

            if (j == pattern.length()) {
                return i - j;
            }
        } else if (j > 0) {
            j = lps[j - 1];
        } else {
            i++;
        }
    }

    return -1;
}
```

Time: `O(n + m)`.

## 32.3 Rabin-Karp

Rabin-Karp compares rolling hash values for the pattern and each same-length text window. Updating the rolling hash can be constant-time per shift, making the average scan efficient and especially useful when searching many patterns or repeated windows. Because different strings can share a hash, a hash match should be verified when correctness cannot tolerate collisions.

Uses rolling hashes to compare substring fingerprints efficiently.

Useful when:

- searching many equal-length windows
- matching multiple patterns
- duplicate substring problems

Hash collisions must be handled carefully.

## 32.4 Z Algorithm

The Z algorithm computes, for each position, the length of the longest substring starting there that matches the prefix of the whole string. By reusing a previously matched interval, it runs in linear time. A common pattern-search trick concatenates `pattern + separator + text` and looks for Z-values equal to the pattern length.

For each index `i`, the Z-array stores how many characters from `s[i...]` match the prefix of `s`.

Applications:

- pattern matching
- prefix occurrence analysis
- string periodicity

## 32.5 Longest Palindromic Substring

A longest-palindromic-substring algorithm must preserve contiguity, unlike subsequence problems. Expanding around every possible center is a simple `O(n²)` time, `O(1)` extra-space approach; DP also takes `O(n²)` space/time, while Manacher's algorithm reaches linear time but is more complex.

A useful `O(n²)` technique is expand-around-center.

```java
static String longestPalindrome(String s) {
    if (s.isEmpty()) return "";

    int bestStart = 0;
    int bestLength = 1;

    for (int center = 0; center < s.length(); center++) {
        int len1 = expand(s, center, center);
        int len2 = expand(s, center, center + 1);
        int len = Math.max(len1, len2);

        if (len > bestLength) {
            bestLength = len;
            bestStart = center - (len - 1) / 2;
        }
    }

    return s.substring(bestStart, bestStart + bestLength);
}

static int expand(String s, int left, int right) {
    while (left >= 0 && right < s.length() &&
           s.charAt(left) == s.charAt(right)) {
        left--;
        right++;
    }

    return right - left - 1;
}
```

---

# 33. Advanced Graph Algorithms

Advanced graph problems are defined less by their story and more by graph properties: edge weights, direction, cycles, connectivity, negative edges, or repeated connectivity changes. Verify those properties first because they determine whether shortest path, MST, SCC, bridge/articulation, flow, or specialized traversal algorithms are valid.

## 33.1 Dijkstra's Algorithm

Finds shortest paths from one source when all edge weights are non-negative.

Weighted edge model:

```java
static class Edge {
    int to;
    int weight;

    Edge(int to, int weight) {
        this.to = to;
        this.weight = weight;
    }
}

static class State {
    int node;
    long distance;

    State(int node, long distance) {
        this.node = node;
        this.distance = distance;
    }
}
```

Implementation:

```java
static long[] dijkstra(List<List<Edge>> graph, int source) {
    int n = graph.size();
    long[] dist = new long[n];
    Arrays.fill(dist, Long.MAX_VALUE);

    PriorityQueue<State> pq = new PriorityQueue<>(
        Comparator.comparingLong(state -> state.distance)
    );

    dist[source] = 0;
    pq.offer(new State(source, 0));

    while (!pq.isEmpty()) {
        State current = pq.poll();
        int u = current.node;
        long d = current.distance;

        if (d != dist[u]) continue;

        for (Edge edge : graph.get(u)) {
            long newDistance = d + edge.weight;

            if (newDistance < dist[edge.to]) {
                dist[edge.to] = newDistance;
                pq.offer(new State(edge.to, newDistance));
            }
        }
    }

    return dist;
}
```

Time with adjacency list + heap:

```text
O((V + E) log V)
```

Do not use standard Dijkstra with negative-weight edges.

## 33.2 Bellman-Ford

Handles negative edge weights and can detect a reachable negative cycle.

Core idea:

Relax every edge `V - 1` times.

A further successful relaxation indicates a reachable negative cycle.

Typical complexity:

```text
O(VE)
```

## 33.3 Floyd-Warshall

Floyd-Warshall computes all-pairs shortest paths by progressively allowing each vertex as an intermediate point. Its core transition is `dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])`. It uses `O(V³)` time and `O(V²)` distance storage and can handle negative edges, but not negative cycles when meaningful finite shortest paths are required.

All-pairs shortest paths.

State:

```text
dist[i][j]
```

Transition:

```text
dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])
```

Complexity:

```text
O(V^3)
```

Good for relatively small dense graphs.

## 33.4 Minimum Spanning Tree

A minimum spanning tree (MST) connects all vertices of a connected, weighted, undirected graph with minimum total edge weight and no cycles. Kruskal's algorithm grows the MST by globally smallest safe edges; Prim's grows outward from the current tree. If the graph is disconnected, the corresponding result is a minimum spanning forest rather than one spanning tree.

A Minimum Spanning Tree connects every vertex with minimum total edge weight and no cycles.

Applications:

- network cabling
- road planning
- clustering
- infrastructure cost minimization

### Kruskal's Algorithm

An algorithm is a finite, unambiguous procedure that converts an input into the required output. A useful explanation of an algorithm should state its preconditions, the main invariant or idea that keeps it correct, when it stops, and its time and space complexity.

1. Sort edges by weight.
2. Add the lightest edge that does not create a cycle.
3. Use DSU to check connectivity.

```java
static class WeightedEdge {
    int u;
    int v;
    int weight;

    WeightedEdge(int u, int v, int weight) {
        this.u = u;
        this.v = v;
        this.weight = weight;
    }
}

static long kruskal(int n, List<WeightedEdge> edges) {
    edges.sort(Comparator.comparingInt(edge -> edge.weight));

    DSU dsu = new DSU(n);
    long total = 0;
    int used = 0;

    for (WeightedEdge edge : edges) {
        if (dsu.union(edge.u, edge.v)) {
            total += edge.weight;
            used++;

            if (used == n - 1) break;
        }
    }

    if (used != n - 1) {
        throw new IllegalStateException("Graph is disconnected");
    }

    return total;
}
```

### Prim's Algorithm

Prim's algorithm builds a minimum spanning tree by repeatedly adding the cheapest edge that connects the current tree to a new vertex. A min-priority queue efficiently selects the next candidate edge. With an adjacency list and binary heap, the common complexity is `O(E log V)`; the graph should be treated as weighted and undirected for the standard MST problem.

Grows the MST outward from a chosen starting vertex using a min-priority queue.

## 33.5 Strongly Connected Components

In a directed graph, an SCC is a maximal set of nodes where each node is reachable from every other node in the same set.

Major algorithms:

- Kosaraju
- Tarjan

Uses:

- dependency analysis
- circuit analysis
- condensation DAGs

## 33.6 Bridges and Articulation Points

A **bridge** is an edge whose removal increases the number of connected components.

An **articulation point** is a vertex whose removal increases the number of connected components.

Tarjan-style DFS uses:

- discovery time
- low-link values

These concepts are important in network resilience problems.

## 33.7 0-1 BFS

When edge weights are only `0` or `1`, use a deque:

- weight 0 → push to front
- weight 1 → push to back

It can outperform Dijkstra for this special case.

---

# 34. Common Problem-Solving Patterns

Problem-solving patterns are reusable ways to remove repeated work. Treat each pattern as a clue-to-invariant mapping: identify the input structure, state what must remain true while the algorithm runs, and only then choose pointer movements, data structures, or transitions.

This section is one of the most important in the handbook.

## 34.1 Frequency Counting

Frequency counting scans the input and stores how many times each value occurs. A hash map gives expected `O(n)` build time; a fixed-size array can be faster and more memory-efficient when the key range is small and known. The resulting counts support duplicates, grouping, anagrams, and many window problems.

Use when the problem says:

- occurrences
- duplicates
- counts
- majority
- matching inventory

Tools:

- array frequency table
- `HashMap`

## 34.2 Sorting + Scan

Sorting all values is often the simplest selection baseline. It is appropriate when ordered output is useful elsewhere or input size is moderate; it does unnecessary work when only one rank is needed and no other sorted-order benefit exists.

Use when order can expose structure.

Examples:

- overlapping intervals
- closest pair candidates
- duplicate detection
- greedy scheduling

## 34.3 Two Pointers

Two pointers maintain two indexes or references whose movement eliminates unnecessary repeated work. Common forms are opposite-end pointers on sorted data and same-direction read/write pointers for in-place filtering. The technique is most valuable when pointer movement can be justified by an invariant, such as sorted order or a maintained valid region.

Clues:

- sorted array
- pair/triplet
- palindrome
- remove duplicates in place
- partitioning

## 34.4 Sliding Window

A sliding window tracks a contiguous range while updating only the information that changes when the range expands or shrinks. Fixed-size windows are used when the length is known; variable-size windows adjust a boundary until a validity condition is restored. The usual goal is to replace repeated recomputation of every subarray or substring with a single linear pass.

Clues:

- contiguous subarray/substring
- longest/shortest window
- at most / at least K condition
- fixed-size segment

## 34.5 Prefix Sum

A prefix sum precomputes cumulative totals so that later range sums can be answered by subtraction. With the common convention `prefix[i] = sum of elements before i`, the sum of the half-open range `[left, right)` is `prefix[right] - prefix[left]`. Building the prefix array costs `O(n)` time and each range query then costs `O(1)`.

Clues:

- many range-sum queries
- subarray sums
- balance before/after index
- cumulative counts

## 34.6 Fast and Slow Pointer

Fast/slow pointers move through the same structure at different rates. The technique works when relative speed reveals structure—for example, the middle of a linked list or a cycle. State the loop condition carefully because it controls where the slow pointer ends on even-length inputs.

Clues:

- linked-list cycle
- middle node
- repeated functional mapping

## 34.7 Monotonic Stack

A monotonic stack keeps its elements in increasing or decreasing order by removing values that can no longer be useful. Each element is pushed and popped at most once, so many nearest-greater/nearest-smaller problems become `O(n)`. The crucial design decision is whether the stack stores values or indexes and which comparison preserves the needed candidate boundary.

Clues:

- next greater/smaller
- previous greater/smaller
- histogram
- daily temperatures
- nearest boundary

## 34.8 Heap / Top-K

A heap is a partially ordered tree structure commonly used to implement a priority queue. A min-heap exposes the smallest item; a max-heap exposes the largest. Insert and removal of the root are typically `O(log n)`, while reading the root is `O(1)`, making heaps ideal for top-k, scheduling, streaming minima/maxima, and graph algorithms such as Dijkstra or Prim.

Clues:

- top `k`
- kth largest/smallest
- continuously retrieve smallest/largest
- merge sorted streams

## 34.9 BFS

Breadth-first search explores a graph or tree level by level using a queue. In an unweighted graph, the first time BFS reaches a vertex is through a path with the minimum number of edges from the start. With adjacency-list representation, a complete traversal is `O(V + E)` when each vertex is processed once.

Clues:

- shortest path with equal edge cost
- minimum steps
- level-by-level traversal
- nearest target in grid

## 34.10 DFS / Backtracking

Backtracking explores a decision tree by making a choice, recursively exploring what follows, and then undoing that choice before trying the next option. It is appropriate when the task asks for all valid combinations, permutations, placements, paths, or constraint-satisfying configurations. Pruning impossible branches early is often the difference between a practical and an impractical solution.

Clues:

- explore all paths
- components
- generate combinations
- choose/unchoose
- tree recursion

## 34.11 Topological Sort

A topological ordering places every prerequisite before the items that depend on it. It exists only for a **directed acyclic graph (DAG)**. Common implementations use Kahn's algorithm with indegrees and a queue, or DFS with postorder; if all vertices cannot be ordered, the dependency graph contains a cycle.

Clues:

- prerequisites
- dependency ordering
- jobs that must occur before other jobs

## 34.12 Union-Find

Union-Find, also called Disjoint Set Union (DSU), maintains a collection of non-overlapping groups under two main operations: `find` identifies a representative and `union` merges groups. Path compression plus union by rank/size makes a long sequence of operations effectively near-constant time in practice. It is useful for dynamic connectivity, cycle detection in undirected graphs, Kruskal's MST, and component grouping.

Clues:

- repeated connectivity queries
- joining groups
- detect redundant edge
- Kruskal MST

## 34.13 Dynamic Programming

Dynamic programming is useful when many candidate solutions reuse the same subproblems and the answer can be composed from smaller states. The core design work is to define the **state**, derive the **transition**, set correct **base cases**, and choose an evaluation order. Memoization computes states on demand; tabulation computes them in an explicit order.

Clues:

- count ways
- minimum/maximum cost
- repeated subproblems
- “best answer up to index i”
- decisions such as take/skip

## 34.14 Binary Search on Answer

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

Clues:

- minimum possible maximum
- maximum possible minimum
- “can we do it with X?”
- monotonic feasibility

## 34.15 Sweep Line

Useful when processing events across a coordinate/time axis.

Typical technique:

```text
(start, +1)
(end, -1)
```

Sort events and maintain active count.

Use for:

- simultaneous meetings
- peak users
- overlapping bookings
- interval coverage

## 34.16 Meet in the Middle

When `n` is around 30–45 and `2^n` is too large:

1. Split into two halves.
2. Enumerate subset results in each half.
3. Combine efficiently using sorting/binary search/hash lookup.

## 34.17 Coordinate Compression

When values are huge but only relative order matters:

```text
[1000, 10, 500000]
```

can map to:

```text
[1, 0, 2]
```

Useful with Fenwick trees, segment trees, and sweep-line algorithms.

---

# 35. Java Collections Framework for DSA

Java's Collections Framework provides production-ready dynamic arrays, maps, sets, queues, deques, and priority queues. DSA work requires knowing both the interface and the implementation trade-off—for example, `ArrayList` vs `LinkedList`, `HashMap` vs `TreeMap`, and `ArrayDeque` vs legacy `Stack`.

## 35.1 ArrayList

```java
List<Integer> list = new ArrayList<>();
list.add(10);
list.get(0);
list.set(0, 20);
```

Typical complexities:

| Operation | Complexity |
|---|---:|
| `get(i)` | `O(1)` |
| append | amortized `O(1)` |
| insert/delete middle | `O(n)` |

## 35.2 LinkedList

Java's `LinkedList` implements both `List` and `Deque`, but it is often not the fastest practical choice due to node allocation and cache behavior.

For stack/queue operations, `ArrayDeque` is generally the preferred default.

## 35.3 HashMap

The code below is a concrete example of **35.3 HashMap**. Read it by identifying the input/state first, then trace each mutation or decision until the produced value/output. When reusing the pattern, preserve its required preconditions and include the cost of nested library operations in the complexity analysis.

```java
Map<String, Integer> map = new HashMap<>();
map.put("java", 1);
map.get("java");
map.containsKey("java");
```

Useful methods:

```java
map.getOrDefault(key, 0);
map.putIfAbsent(key, value);
map.computeIfAbsent(key, k -> new ArrayList<>());
map.merge(key, 1, Integer::sum);
```

## 35.4 HashSet

The code below is a concrete example of **35.4 HashSet**. Read it by identifying the input/state first, then trace each mutation or decision until the produced value/output. When reusing the pattern, preserve its required preconditions and include the cost of nested library operations in the complexity analysis.

```java
Set<Integer> set = new HashSet<>();
set.add(10);
set.contains(10);
set.remove(10);
```

## 35.5 TreeMap and TreeSet

`TreeMap` and `TreeSet` maintain keys/elements in sorted order using a balanced tree. Core search/insert/delete operations are `O(log n)`, unlike expected `O(1)` hash-based structures. Use them when ordered iteration, floor/ceiling, or range navigation is required—not just for membership.

Maintain sorted order.

Operations are usually `O(log n)`.

Useful methods:

```java
TreeSet<Integer> set = new TreeSet<>();
set.floor(10);
set.ceiling(10);
set.lower(10);
set.higher(10);
```

## 35.6 PriorityQueue

The code below is a concrete example of **35.6 PriorityQueue**. Read it by identifying the input/state first, then trace each mutation or decision until the produced value/output. When reusing the pattern, preserve its required preconditions and include the cost of nested library operations in the complexity analysis.

```java
PriorityQueue<Integer> pq = new PriorityQueue<>();
pq.offer(5);
pq.offer(2);
pq.offer(9);
System.out.println(pq.poll()); // 2
```

## 35.7 ArrayDeque

The code below is a concrete example of **35.7 ArrayDeque**. Read it by identifying the input/state first, then trace each mutation or decision until the produced value/output. When reusing the pattern, preserve its required preconditions and include the cost of nested library operations in the complexity analysis.

Excellent default for:

- stack
- queue
- deque

```java
Deque<Integer> dq = new ArrayDeque<>();
```

Note: `ArrayDeque` does not permit `null` elements.

## 35.8 Comparator

A comparator defines the ordering used by sorting or ordered/priority structures. It must be consistent enough for the algorithm/container: returning negative, zero, or positive indicates before/equal/after. Avoid subtraction-based comparisons on large integers because arithmetic overflow can reverse the intended ordering.

```java
class Person {
    String name;
    int age;

    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

List<Person> people = new ArrayList<>();
people.sort(Comparator.comparingInt(person -> person.age));
```

Descending:

```java
people.sort(Comparator.comparingInt((Person person) -> person.age).reversed());
```

Tie breaker:

```java
people.sort(
    Comparator.comparingInt((Person person) -> person.age)
              .thenComparing(person -> person.name)
);
```

### Avoid comparator overflow

Do not implement integer comparison as `a - b` when values can approach numeric limits; the subtraction itself may overflow. Use the language's safe comparison helper or explicit relational comparisons so ordering remains correct.

Bad:

```java
(a, b) -> a - b
```

Safer:

```java
Integer.compare(a, b)
```

---

# 36. Java Performance and Common Pitfalls

Correct algorithms can still fail in Java because of numeric overflow, boxing, comparator mistakes, recursion depth, accidental quadratic string construction, or using a collection with the wrong operation cost. Treat language-level behavior as part of complexity analysis, not as an afterthought.

## 36.1 `==` vs `.equals()`

For Java reference types, `==` checks whether two references point to the same object, while `.equals()` checks logical equality according to the class implementation. DSA code that compares boxed numbers, strings, list elements, or custom keys usually needs logical equality unless identity is explicitly intended.

For objects, `==` compares references.

```java
String a = new String("java");
String b = new String("java");

System.out.println(a == b);      // false
System.out.println(a.equals(b)); // true
```

## 36.2 Integer Overflow

Fixed-width integer arithmetic can wrap when a sum, difference, or product exceeds the type's range. Promote operands **before** the risky operation (for example to `long`) and check problem constraints rather than casting only after overflow has already occurred.

If constraints allow values near `10^9`, sums and products may need `long`.

```java
long sum = 0;
for (int x : nums) {
    sum += x;
}
```

## 36.3 String Concatenation in Loops

When a loop repeatedly appends text, prefer a builder or a collection of pieces followed by one join/concatenation step. This avoids repeatedly copying an ever-growing immutable string and makes the intended construction process explicit.

Avoid repeated immutable string creation:

```java
String result = "";
for (...) {
    result += value;
}
```

Prefer:

```java
StringBuilder sb = new StringBuilder();
for (...) {
    sb.append(value);
}
```

## 36.4 Modifying a Collection During Enhanced Iteration

Changing a collection's structure while an enhanced `for` loop is traversing it can invalidate the iterator and commonly triggers `ConcurrentModificationException` in Java's fail-fast collections. Use the iterator's own removal operation, collect changes for later, or choose a safe concurrent structure when appropriate.

This may cause `ConcurrentModificationException`.

Use an iterator when removing while iterating:

```java
Iterator<Integer> it = list.iterator();

while (it.hasNext()) {
    if (it.next() < 0) {
        it.remove();
    }
}
```

## 36.5 Recursion Depth

Recursion solves a problem by calling the same routine on a smaller or simpler state. Every recursive solution needs a **base case** that stops further calls and a **progress rule** that moves toward that base case. Also account for call-stack space: even an algorithm with little explicit memory usage may use `O(depth)` stack space.

Deep DFS on a huge graph may overflow the Java call stack.

Use iterative DFS when needed:

```java
Deque<Integer> stack = new ArrayDeque<>();
stack.push(start);
```

## 36.6 Primitive Arrays vs Boxed Collections

An array-like structure stores elements in an indexed sequence. Its main advantage is direct access by position; the main trade-off is that inserting or deleting near the front or middle usually requires shifting elements. In DSA problems, arrays are also the base structure behind two pointers, sliding windows, prefix sums, binary search, heaps, and many dynamic-programming tables.

`int[]` is much more memory-efficient than `List<Integer>`.

Use primitive arrays when:

- size is known
- performance matters
- rich list operations are unnecessary

## 36.7 `Arrays.asList()` with Primitive Arrays

An array-like structure stores elements in an indexed sequence. Its main advantage is direct access by position; the main trade-off is that inserting or deleting near the front or middle usually requires shifting elements. In DSA problems, arrays are also the base structure behind two pointers, sliding windows, prefix sums, binary search, heaps, and many dynamic-programming tables.

This is a common trap:

```java
int[] arr = {1, 2, 3};
System.out.println(Arrays.asList(arr).size()); // 1
```

The entire `int[]` becomes one element.

For objects:

```java
Integer[] arr = {1, 2, 3};
List<Integer> list = Arrays.asList(arr);
```

## 36.8 Mutable Keys in HashMap

Do not mutate fields involved in `equals()`/`hashCode()` after using an object as a hash key.

Otherwise the map may no longer be able to find the key correctly.

## 36.9 PriorityQueue Iteration Is Not Sorted

The code below is a concrete example of **36.9 PriorityQueue Iteration Is Not Sorted**. Read it by identifying the input/state first, then trace each mutation or decision until the produced value/output. When reusing the pattern, preserve its required preconditions and include the cost of nested library operations in the complexity analysis.

This:

```java
for (int x : pq) {
    System.out.println(x);
}
```

does **not** guarantee sorted iteration order.

To retrieve sorted-by-priority order, repeatedly `poll()`.

## 36.10 Defensive Edge-Case Handling

Defensive DSA code handles invalid or minimal inputs at the boundary so the core loop/recursion can rely on clear assumptions. Examples include empty arrays, null roots, `k` outside valid ranges, disconnected graphs, and arithmetic ranges that require wider numeric types.

Before indexing:

```java
if (arr.length == 0) {
    // handle empty input
}
```

Never assume a problem excludes empty input unless the constraints say so.

---

# 37. Reusable Java Templates

Templates reduce boilerplate for patterns you already understand, but they should not be memorized as unexplained code. For each template, know the invariant, parameter meaning, return value, mutation behavior, and the exact condition that changes its boundaries or state.

## 37.1 Basic Interview Template

This template is scaffolding for a solution, not an algorithm by itself. Keep input parsing and output separate from the solving method, give the solver a clear parameter/return contract, and place only the data structures required by the chosen approach inside it.

```java
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        // local test
    }

    static int solve(int[] nums) {
        return 0;
    }
}
```

## 37.2 Fast Input with BufferedReader

`BufferedReader` reduces I/O overhead by reading larger character buffers instead of many tiny operations. Parsed tokens are still strings, so convert them deliberately to numeric types and handle whitespace/line boundaries according to the input format.

```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int n = Integer.parseInt(br.readLine().trim());
        StringTokenizer st = new StringTokenizer(br.readLine());

        int[] arr = new int[n];

        for (int i = 0; i < n; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }
    }
}
```

## 37.3 Custom Fast Scanner

A custom scanner reads raw bytes/chars and parses tokens with minimal allocation, which can help on very large competitive-programming input. It adds code and bug surface, so use it only when ordinary buffered input is a measured bottleneck and test end-of-file, signs, and whitespace carefully.

```java
import java.io.*;

class FastScanner {
    private final InputStream in = System.in;
    private final byte[] buffer = new byte[1 << 16];
    private int ptr = 0;
    private int len = 0;

    private int read() throws IOException {
        if (ptr >= len) {
            len = in.read(buffer);
            ptr = 0;
            if (len <= 0) return -1;
        }
        return buffer[ptr++];
    }

    int nextInt() throws IOException {
        int c;
        do {
            c = read();
        } while (c <= ' ');

        int sign = 1;
        if (c == '-') {
            sign = -1;
            c = read();
        }

        int value = 0;
        while (c > ' ') {
            value = value * 10 + (c - '0');
            c = read();
        }

        return value * sign;
    }
}
```

Use this only when input performance genuinely matters.

## 37.4 Fast Output

Buffer output and write it in larger chunks instead of calling a print routine thousands of times. A `StringBuilder`, `BufferedWriter`, or `PrintWriter` can reduce I/O overhead; remember that constructing a very large output buffer also consumes memory proportional to the produced text.

```java
StringBuilder out = new StringBuilder();

for (int x : result) {
    out.append(x).append('\n');
}

System.out.print(out);
```

## 37.5 BFS Grid Template

Breadth-first search explores a graph or tree level by level using a queue. In an unweighted graph, the first time BFS reaches a vertex is through a path with the minimum number of edges from the start. With adjacency-list representation, a complete traversal is `O(V + E)` when each vertex is processed once.

```java
static int bfsGrid(int[][] grid, int sr, int sc) {
    int rows = grid.length;
    int cols = grid[0].length;

    int[][] dirs = {
        {1, 0}, {-1, 0}, {0, 1}, {0, -1}
    };

    boolean[][] visited = new boolean[rows][cols];
    Queue<int[]> queue = new ArrayDeque<>();

    queue.offer(new int[]{sr, sc});
    visited[sr][sc] = true;

    int distance = 0;

    while (!queue.isEmpty()) {
        int size = queue.size();

        for (int i = 0; i < size; i++) {
            int[] cell = queue.poll();
            int r = cell[0];
            int c = cell[1];

            for (int[] d : dirs) {
                int nr = r + d[0];
                int nc = c + d[1];

                if (nr < 0 || nr >= rows || nc < 0 || nc >= cols) {
                    continue;
                }

                if (visited[nr][nc]) continue;

                visited[nr][nc] = true;
                queue.offer(new int[]{nr, nc});
            }
        }

        distance++;
    }

    return distance;
}
```

## 37.6 Iterative DFS Template

Depth-first search explores one branch as far as possible before returning to try another branch. It can be implemented recursively or with an explicit stack and is widely used for connected components, cycle detection, tree processing, path exploration, topological reasoning, and many backtracking-style searches. Track visited state in cyclic graphs to avoid endless revisits.

```java
static void iterativeDfs(List<List<Integer>> graph, int start) {
    boolean[] visited = new boolean[graph.size()];
    Deque<Integer> stack = new ArrayDeque<>();

    stack.push(start);

    while (!stack.isEmpty()) {
        int node = stack.pop();

        if (visited[node]) continue;
        visited[node] = true;

        for (int neighbor : graph.get(node)) {
            if (!visited[neighbor]) {
                stack.push(neighbor);
            }
        }
    }
}
```

## 37.7 Binary Search First True Template

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

```java
static int firstTrue(int left, int right) {
    while (left < right) {
        int mid = left + (right - left) / 2;

        if (condition(mid)) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }

    return left;
}
```

## 37.8 Backtracking Template

Backtracking explores a decision tree by making a choice, recursively exploring what follows, and then undoing that choice before trying the next option. It is appropriate when the task asks for all valid combinations, permutations, placements, paths, or constraint-satisfying configurations. Pruning impossible branches early is often the difference between a practical and an impractical solution.

```java
static void backtrack(
        int index,
        List<Integer> current,
        List<List<Integer>> result) {

    if (/* base case */) {
        result.add(new ArrayList<>(current));
        return;
    }

    for (/* every available choice */) {
        // choose

        backtrack(index + 1, current, result);

        // undo
    }
}
```

## 37.9 Memoization Template

A memoization template caches the answer for a state before that state is recomputed. The state key must contain every variable that affects the returned result; otherwise distinct subproblems may incorrectly share one cache entry. Use a sentinel or presence check that cannot be confused with a valid computed answer.

```java
static int solve(int state, int[] memo) {
    if (/* base case */) return /* answer */;

    if (memo[state] != -1) {
        return memo[state];
    }

    int answer = /* transition */;
    memo[state] = answer;
    return answer;
}
```

---

# 38. Interview Problem-Solving Framework

An interview framework makes your reasoning visible: clarify inputs and constraints, establish a brute-force baseline, identify repeated work, choose a pattern, justify correctness, analyze complexity, implement clearly, and test edge cases. The explanation is part of the solution, not an extra step after coding.

When given a DSA problem, do not immediately code.

Use this process.

## Step 1: Clarify the Problem

Ask or determine:

- What are the input types?
- What is the output?
- Are duplicates possible?
- Can values be negative?
- Is the input sorted?
- Can input be empty?
- What are the constraints?
- Do we need indexes or values?
- Is mutation allowed?

## Step 2: Work a Small Example

This step is part of turning a problem statement into a defensible solution. Do it explicitly before moving on: the result of this step should give you concrete information you can use to choose, verify, or explain the algorithm.

Example:

```text
nums = [2, 7, 11, 15]
target = 9
```

Manually identify the expected answer before designing the algorithm.

## Step 3: State the Brute Force

This step is part of turning a problem statement into a defensible solution. Do it explicitly before moving on: the result of this step should give you concrete information you can use to choose, verify, or explain the algorithm.

For Two Sum:

```text
Check every pair -> O(n^2)
```

This proves you understand the problem before optimization.

## Step 4: Find the Bottleneck

This step is part of turning a problem statement into a defensible solution. Do it explicitly before moving on: the result of this step should give you concrete information you can use to choose, verify, or explain the algorithm.

What is repeatedly expensive?

For Two Sum:

> Repeatedly searching whether the complement appeared earlier.

Replace repeated searching with a hash map.

## Step 5: Choose a Pattern

Ask:

- Sorted? → binary search / two pointers.
- Contiguous? → sliding window / prefix sum.
- Top K? → heap.
- Dependency order? → topological sort.
- Minimum steps? → BFS.
- Repeated optimal subproblems? → DP.
- All combinations? → backtracking.

## Step 6: Explain Correctness

Do not only say “it works.” Explain why.

Example for two pointers:

> Because the array is sorted, if the current sum is too small, decreasing the right pointer cannot help; only moving left forward can increase the sum.

## Step 7: Analyze Complexity

This step is part of turning a problem statement into a defensible solution. Do it explicitly before moving on: the result of this step should give you concrete information you can use to choose, verify, or explain the algorithm.

State both:

```text
Time: O(n)
Space: O(n)
```

## Step 8: Code Clearly

This step is part of turning a problem statement into a defensible solution. Do it explicitly before moving on: the result of this step should give you concrete information you can use to choose, verify, or explain the algorithm.

Prefer descriptive names:

```java
int left = 0;
int right = nums.length - 1;
```

instead of:

```java
int a = 0, b = n - 1;
```

## Step 9: Dry Run

This step is part of turning a problem statement into a defensible solution. Do it explicitly before moving on: the result of this step should give you concrete information you can use to choose, verify, or explain the algorithm.

Trace at least one normal example.

## Step 10: Test Edge Cases

This step is part of turning a problem statement into a defensible solution. Do it explicitly before moving on: the result of this step should give you concrete information you can use to choose, verify, or explain the algorithm.

Before finalizing the solution, test cases that challenge the algorithm's assumptions and boundaries. At minimum, consider empty or smallest-valid input, duplicates, boundary indexes, all-negative or zero values, very large values that may overflow `int`, and structure-specific cases such as disconnected/cyclic graphs, one-node or skewed trees, and empty strings when relevant. The purpose is to exercise every important branch and verify that the algorithm's invariant still holds.

---

# 39. Edge Cases Checklist

Before declaring a solution complete, consider:

- Empty input.
- Single element.
- Two elements.
- All values equal.
- Already sorted.
- Reverse sorted.
- All negative values.
- Zero values.
- Duplicate values.
- Target absent.
- Target at first/last position.
- Maximum integer values.
- Large sums requiring `long`.
- Disconnected graph.
- Graph with cycle.
- Tree with one node.
- Highly skewed tree.
- String with spaces/punctuation.
- Empty string.
- Unicode requirements.

Example bug:

```java
int max = 0;
```

This is wrong for an array such as:

```text
[-10, -5, -20]
```

Correct initialization:

```java
int max = arr[0];
```

---

# 40. Practice Roadmap

A practice roadmap should progress from understanding operations to recognizing patterns under mixed conditions. Advance when you can derive and explain a solution without copying, not merely when you have completed a fixed number of exercises.

## Phase 1 — Java + Complexity

Master:

- loops
- methods
- arrays
- strings
- classes
- collections
- Big-O

Suggested exercises:

1. Sum of array.
2. Maximum/minimum.
3. Reverse array.
4. Count frequency.
5. Palindrome string.
6. Prime check.

## Phase 2 — Core Array Patterns

Master:

- sorting
- binary search
- hashing
- two pointers
- sliding window
- prefix sum

Suggested problem types:

1. Two Sum.
2. Three Sum.
3. Move Zeros.
4. Remove Duplicates.
5. Maximum Subarray.
6. Longest Unique Substring.
7. Subarray Sum Equals K.
8. Merge Intervals.

## Phase 3 — Linked Structures

Master:

- linked list
- stack
- queue
- deque

Suggested problems:

1. Reverse List.
2. Detect Cycle.
3. Merge Sorted Lists.
4. Valid Parentheses.
5. Min Stack.
6. Next Greater Element.

## Phase 4 — Trees and Heaps

Master:

- DFS traversals
- BFS/level order
- recursion on trees
- BST
- priority queue

Suggested problems:

1. Maximum Depth.
2. Same Tree.
3. Invert Tree.
4. Level Order Traversal.
5. Validate BST.
6. Lowest Common Ancestor.
7. Kth Largest.
8. Top K Frequent.

## Phase 5 — Graphs

Master:

- adjacency list
- BFS
- DFS
- connected components
- cycle detection
- topological sort
- DSU

Suggested problems:

1. Number of Islands.
2. Clone Graph.
3. Course Schedule.
4. Connected Components.
5. Redundant Connection.
6. Shortest Path in Binary Matrix.

## Phase 6 — Recursion and Backtracking

Backtracking explores a decision tree by making a choice, recursively exploring what follows, and then undoing that choice before trying the next option. It is appropriate when the task asks for all valid combinations, permutations, placements, paths, or constraint-satisfying configurations. Pruning impossible branches early is often the difference between a practical and an impractical solution.

Master:

- recursion tree
- choose/explore/unchoose
- pruning

Problems:

1. Subsets.
2. Permutations.
3. Combination Sum.
4. Word Search.
5. N-Queens.
6. Sudoku Solver.

## Phase 7 — Dynamic Programming

Recommended order:

1. Fibonacci pattern.
2. Climbing Stairs.
3. House Robber.
4. Coin Change.
5. 0/1 Knapsack.
6. Grid DP.
7. LCS.
8. LIS.
9. Partition DP.
10. Interval DP.
11. Tree DP.

## Phase 8 — Advanced

These items combine or extend core patterns. Add them only after the prerequisite structure is comfortable; for each one, learn the invariant and complexity rather than memorizing a finished template.

Master:

- trie
- monotonic stack/queue
- Dijkstra
- Bellman-Ford
- Floyd-Warshall
- MST
- SCC
- bridges/articulation points
- Fenwick tree
- segment tree
- KMP
- bitmasking
- advanced DP

---

# 41. Pattern Recognition Cheat Sheet

| Problem wording / clue | Think about |
|---|---|
| “sorted array” | binary search, two pointers |
| “pair with target” | hash map, two pointers |
| “contiguous subarray” | sliding window, prefix sum, Kadane |
| “substring” | sliding window, hashing, KMP |
| “range sum” | prefix sum, Fenwick, segment tree |
| “many range updates” | difference array, lazy segment tree |
| “top K” | heap |
| “kth largest/smallest” | heap, quickselect, binary search |
| “next greater/smaller” | monotonic stack |
| “minimum steps” | BFS |
| “weighted shortest path” | Dijkstra / Bellman-Ford |
| “prerequisites” | graph + topological sort |
| “connected groups” | DFS/BFS/DSU |
| “all combinations” | backtracking |
| “count ways” | DP |
| “min/max cost over decisions” | DP or greedy |
| “minimum feasible X” | binary search on answer |
| “prefix words” | trie |
| “overlapping schedules” | intervals, sorting, heap |
| “dynamic connectivity” | DSU |
| “static range min” | sparse table |
| “dynamic range query” | Fenwick/segment tree |

---

# 42. Complexity Cheat Sheet

Use a complexity cheat sheet to recall typical costs, then verify the exact implementation being used. 'Hash lookup is `O(1)`' means average/expected behavior under normal hashing assumptions; a tree or language-specific container may have different guarantees.

## Arrays and Collections

| Structure/Operation | Typical Complexity |
|---|---:|
| Array access | `O(1)` |
| Array search | `O(n)` |
| ArrayList access | `O(1)` |
| ArrayList append | amortized `O(1)` |
| ArrayList middle insert/delete | `O(n)` |
| HashMap get/put | average `O(1)` |
| HashSet contains/add | average `O(1)` |
| TreeMap/TreeSet operations | `O(log n)` |
| PriorityQueue offer/poll | `O(log n)` |
| PriorityQueue peek | `O(1)` |

## Sorting

| Algorithm | Best | Average | Worst | Extra Space |
|---|---:|---:|---:|---:|
| Bubble | `O(n)` optimized | `O(n²)` | `O(n²)` | `O(1)` |
| Selection | `O(n²)` | `O(n²)` | `O(n²)` | `O(1)` |
| Insertion | `O(n)` | `O(n²)` | `O(n²)` | `O(1)` |
| Merge Sort | `O(n log n)` | `O(n log n)` | `O(n log n)` | `O(n)` |
| Quick Sort | `O(n log n)` | `O(n log n)` | `O(n²)` | recursion-dependent |
| Counting Sort | `O(n + k)` | `O(n + k)` | `O(n + k)` | `O(k)` |

## Graph Algorithms

| Algorithm | Complexity |
|---|---:|
| BFS | `O(V + E)` |
| DFS | `O(V + E)` |
| Topological Sort | `O(V + E)` |
| Dijkstra with heap | `O((V + E) log V)` |
| Bellman-Ford | `O(VE)` |
| Floyd-Warshall | `O(V³)` |
| Kruskal | dominated by edge sort, typically `O(E log E)` |
| DSU operations | near `O(1)` amortized |

## Trees

| Operation | Balanced BST | Worst skewed BST |
|---|---:|---:|
| Search | `O(log n)` | `O(n)` |
| Insert | `O(log n)` | `O(n)` |
| Delete | `O(log n)` | `O(n)` |
| Full traversal | `O(n)` | `O(n)` |

---

# 43. Final Mastery Checklist

Treat this section as an evidence-based self-check. Mark an item complete only when you can explain it in simple language, implement or apply it without copying, analyze its trade-offs, and recognize cases where it should not be used.

Use this as your final self-assessment.

## Foundation

- [ ] I understand Big-O notation.
- [ ] I can estimate time and space complexity.
- [ ] I know when `int` may overflow and when to use `long`.
- [ ] I can use arrays, strings, methods, classes, and Java collections comfortably.

## Arrays and Strings

- [ ] I can reverse, rotate, scan, and partition arrays.
- [ ] I understand Kadane's algorithm.
- [ ] I can solve two-pointer problems.
- [ ] I can solve fixed and variable sliding-window problems.
- [ ] I can use prefix sums and hash maps together.
- [ ] I can solve interval problems after sorting.

## Linked Structures

- [ ] I can reverse a linked list.
- [ ] I understand slow/fast pointers.
- [ ] I can detect a cycle.
- [ ] I can use stacks and queues with `ArrayDeque`.

## Trees

- [ ] I know preorder, inorder, postorder, and level order.
- [ ] I can solve recursive tree problems.
- [ ] I understand BST ordering.
- [ ] I can validate a BST.
- [ ] I understand LCA and tree diameter.

## Heap and Hashing

A heap is a partially ordered tree structure commonly used to implement a priority queue. A min-heap exposes the smallest item; a max-heap exposes the largest. Insert and removal of the root are typically `O(log n)`, while reading the root is `O(1)`, making heaps ideal for top-k, scheduling, streaming minima/maxima, and graph algorithms such as Dijkstra or Prim.

- [ ] I can solve Top-K problems.
- [ ] I can configure min-heaps and max-heaps.
- [ ] I understand frequency maps and sets.

## Graphs

- [ ] I can build adjacency lists.
- [ ] I know BFS and DFS.
- [ ] I can count components.
- [ ] I can detect cycles.
- [ ] I understand topological sorting.
- [ ] I know when to use Dijkstra, Bellman-Ford, and Floyd-Warshall.
- [ ] I understand MST and DSU.

## Recursion / Backtracking

Backtracking explores a decision tree by making a choice, recursively exploring what follows, and then undoing that choice before trying the next option. It is appropriate when the task asks for all valid combinations, permutations, placements, paths, or constraint-satisfying configurations. Pruning impossible branches early is often the difference between a practical and an impractical solution.

- [ ] I can define a base case correctly.
- [ ] I understand choose → recurse → undo.
- [ ] I can generate subsets and permutations.
- [ ] I understand pruning.

## Dynamic Programming

- [ ] I can recognize overlapping subproblems.
- [ ] I can define a DP state in plain English.
- [ ] I can derive transitions.
- [ ] I can write memoization and tabulation.
- [ ] I understand 0/1 vs unbounded knapsack.
- [ ] I understand LCS and LIS patterns.
- [ ] I can optimize DP memory when only previous states are needed.

## Advanced

- [ ] I understand monotonic stacks/queues.
- [ ] I can use a trie.
- [ ] I understand Fenwick trees.
- [ ] I understand segment trees.
- [ ] I know KMP conceptually and can implement it.
- [ ] I understand SCC, bridges, and articulation points conceptually.
- [ ] I can recognize binary-search-on-answer problems.

---

# Bonus: How to Think Like a Strong DSA Solver

A strong solver does not memorize hundreds of unrelated solutions. They build a library of **ideas**.

When you see a new problem, ask:

```text
What information am I repeatedly recomputing?
Can I store it?

Is the input ordered?
Can sorting create useful structure?

Is the question about a contiguous region?
Would a window or prefix sum help?

Do I only need the best K values?
Would a heap help?

Is this naturally a graph?
What are the nodes and edges?

Do choices lead to repeated states?
Could this be dynamic programming?

Do I need every valid configuration?
Could this be backtracking?

Is there a monotonic yes/no condition?
Could I binary-search the answer?
```

This way of thinking is more valuable than memorizing code.

---

# Bonus: Scenario-to-DSA Mapping

Use this section to practice translating problem wording into required operations and constraints. The mapping is a starting hypothesis: confirm the technique's preconditions and explain the invariant before committing to it.

## Scenario 1 — E-commerce Search Suggestions

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

Possible tools:

- Trie for prefixes.
- HashMap for product metadata.
- Heap for top-ranked suggestions.

## Scenario 2 — Delivery Route Planning

This scenario is a recognition exercise. Translate the story into required operations—lookup, ordering, range processing, connectivity, priority, or dependency handling—then justify why the suggested structure makes those operations efficient.

Possible tools:

- Graph representation.
- Dijkstra for non-negative travel costs.
- BFS if every road has equal cost.

## Scenario 3 — Employee Meeting Scheduler

This scenario is a recognition exercise. Translate the story into required operations—lookup, ordering, range processing, connectivity, priority, or dependency handling—then justify why the suggested structure makes those operations efficient.

Possible tools:

- interval sorting
- merging intervals
- min-heap for room allocation
- sweep line for peak overlap count

## Scenario 4 — Stock Price Analytics

Possible tools:

- prefix sums for range totals
- sliding windows for moving metrics
- monotonic stack for next greater price
- segment tree for dynamic range queries

## Scenario 5 — Social Network Friend Groups

A social network is naturally a graph where people are vertices and relationships are edges. BFS/DFS support reachability and degrees of separation, while sets/maps support neighbor membership; large-scale recommendations often require more specialized ranking/indexing beyond basic traversal.

Possible tools:

- graph DFS/BFS
- DSU for dynamic group merging
- shortest path for degrees of separation

## Scenario 6 — Autocomplete Dictionary

This scenario is a recognition exercise. Translate the story into required operations—lookup, ordering, range processing, connectivity, priority, or dependency handling—then justify why the suggested structure makes those operations efficient.

Possible tools:

- Trie
- frequency map
- priority queue for ranking completions

## Scenario 7 — Task Dependency Engine

This scenario is a recognition exercise. Translate the story into required operations—lookup, ordering, range processing, connectivity, priority, or dependency handling—then justify why the suggested structure makes those operations efficient.

Possible tools:

- directed graph
- cycle detection
- topological sort

## Scenario 8 — Cache Design

An LRU cache commonly combines:

- HashMap for `O(1)` lookup.
- Doubly linked list for `O(1)` recency updates.

The key lesson is that advanced systems often combine multiple basic data structures.

---

# Bonus: Common Mistakes by Beginners

DSA bugs are often caused by incorrect boundaries, stale state, missing visited checks, wrong base cases, or an invariant that was never made explicit. Debug by reducing the input, tracing state changes line by line, and checking the first point where the program diverges from the expected invariant.

## Mistake 1 — Coding Before Understanding Constraints

An `O(n²)` solution may be fine for `n = 1,000` but disastrous for `n = 1,000,000`.

## Mistake 2 — Memorizing Without Deriving

This mistake is common because the code can look plausible on normal inputs. Use a minimal counterexample, state the violated invariant/assumption, and fix the reasoning before optimizing or memorizing a corrected snippet.

Instead of memorizing:

```text
dp[i] = max(dp[i-1], nums[i] + dp[i-2])
```

understand the decision:

```text
Skip current item OR take current item.
```

## Mistake 3 — Ignoring Overflow

This mistake is common because the code can look plausible on normal inputs. Use a minimal counterexample, state the violated invariant/assumption, and fix the reasoning before optimizing or memorizing a corrected snippet.

Always inspect maximum input size before using `int` for sums or products.

## Mistake 4 — Overusing HashMap

This mistake is common because the code can look plausible on normal inputs. Use a minimal counterexample, state the violated invariant/assumption, and fix the reasoning before optimizing or memorizing a corrected snippet.

If values are lowercase letters only, an `int[26]` is simpler and faster.

## Mistake 5 — Using Recursion Everywhere

Recursion solves a problem by calling the same routine on a smaller or simpler state. Every recursive solution needs a **base case** that stops further calls and a **progress rule** that moves toward that base case. Also account for call-stack space: even an algorithm with little explicit memory usage may use `O(depth)` stack space.

Recursion is elegant, but deep recursion may overflow Java's stack.

## Mistake 6 — Forgetting to Mark BFS Nodes Visited When Enqueuing

Breadth-first search explores a graph or tree level by level using a queue. In an unweighted graph, the first time BFS reaches a vertex is through a path with the minimum number of edges from the start. With adjacency-list representation, a complete traversal is `O(V + E)` when each vertex is processed once.

Bad:

```text
mark visited when dequeued
```

This can enqueue the same node repeatedly.

Better:

```text
mark visited when enqueued
```

## Mistake 7 — Mixing Node Value with Node Identity

Two tree nodes can hold the same value but still be different nodes.

Use node references when identity matters.

## Mistake 8 — Off-by-One Errors in Binary Search

Off-by-one bugs happen when an endpoint is included/excluded incorrectly. Write the interval convention explicitly—such as `[left, right]` or `[left, right)`—and test empty, one-element, and boundary-position cases before trusting the loop.

Choose one invariant and maintain it consistently.

Examples:

```text
closed interval [left, right]
```

or:

```text
half-open interval [left, right)
```

Do not mix both styles midway.

---

# Bonus: How to Review a Solved Problem

After solving a problem, record:

```text
Problem:
Pattern:
Brute force:
Optimized idea:
Why it works:
Time complexity:
Space complexity:
Mistake I made:
Key trigger words:
Similar problems:
```

Example:

```text
Problem: Longest Substring Without Repeating Characters
Pattern: Variable sliding window
Brute force: Check all substrings
Optimized idea: Track latest character index
Why it works: Move left beyond the previous duplicate
Time: O(n)
Space: O(k), where k is character-set size
Trigger words: longest + substring + no duplicates
```

This review habit builds pattern recognition much faster than solving many problems once.

---

# Bonus: 12-Week Suggested Study Plan

Use this plan as a sequence of skill dependencies rather than a rigid calendar. Spend extra time where you cannot yet explain the invariant, implement without copying, or analyze complexity; mastery is more important than keeping pace with a date label.

## Weeks 1–2

Use this schedule as a pacing guide rather than a strict quota. If a topic still feels mechanical, spend additional time tracing examples and re-solving mistakes before increasing difficulty.

- Java DSA syntax
- complexity
- arrays
- strings
- hashing
- sorting
- binary search

## Weeks 3–4

Use this schedule as a pacing guide rather than a strict quota. If a topic still feels mechanical, spend additional time tracing examples and re-solving mistakes before increasing difficulty.

- two pointers
- sliding window
- prefix sums
- linked lists
- stacks
- queues

## Weeks 5–6

Use this schedule as a pacing guide rather than a strict quota. If a topic still feels mechanical, spend additional time tracing examples and re-solving mistakes before increasing difficulty.

- recursion
- backtracking
- binary trees
- BST
- heaps

## Weeks 7–8

Use this schedule as a pacing guide rather than a strict quota. If a topic still feels mechanical, spend additional time tracing examples and re-solving mistakes before increasing difficulty.

- graphs
- BFS/DFS
- topological sort
- DSU
- shortest paths

## Weeks 9–10

Use this schedule as a pacing guide rather than a strict quota. If a topic still feels mechanical, spend additional time tracing examples and re-solving mistakes before increasing difficulty.

- greedy
- DP fundamentals
- knapsack
- LCS/LIS
- grid DP

## Weeks 11–12

Use this schedule as a pacing guide rather than a strict quota. If a topic still feels mechanical, spend additional time tracing examples and re-solving mistakes before increasing difficulty.

- monotonic structures
- tries
- Fenwick tree
- segment tree
- advanced graphs
- string matching
- timed mock interviews

### Daily practice pattern

The code below is a concrete example of **Daily practice pattern**. Read it by identifying the input/state first, then trace each mutation or decision until the produced value/output. When reusing the pattern, preserve its required preconditions and include the cost of nested library operations in the complexity analysis.

A practical daily session:

```text
20 min  -> revise concept
20 min  -> trace examples manually
45 min  -> solve 1 new problem
30 min  -> solve/retry an older problem
15 min  -> write learning notes
```

Quality of review matters more than raw problem count.

---

# Final Advice

To master DSA in Java:

1. Learn the concept, not just the syntax.
2. Understand the brute-force solution first.
3. Identify what causes the brute force to be slow.
4. Map the bottleneck to a known pattern.
5. Explain why the optimized approach is correct.
6. Analyze time and space complexity every time.
7. Implement from memory.
8. Practice variations, not only identical questions.
9. Revisit failed problems.
10. Learn to combine data structures and algorithms.

The final goal is not:

> “I have seen this problem before.”

The final goal is:

> “I understand the structure of this problem, I can identify the right pattern, derive a correct solution, implement it cleanly in Java, and explain its complexity.”

---

## End of Handbook

Use this file as a living reference. Add your own solved-problem notes, mistakes, reusable templates, and pattern observations as you progress.

---

# Appendix A — Additional Sorting and Selection Algorithms

Sorting rearranges values according to an ordering rule so later operations can exploit structure. Learn not only the code but also stability, in-place behavior, best/average/worst complexity, comparator requirements, and when a language's built-in sort is preferable to a manual algorithm.

The main sorting chapter covers the algorithms most learners should study first. This appendix completes the picture with several important specialized techniques.

## A.1 Heap Sort

Heap sort repeatedly moves the maximum element to the end of the array.

Properties:

- Time: `O(n log n)` in best, average, and worst cases.
- Extra array space: `O(1)` for the in-place version.
- Not stable in its usual form.

```java
static void heapSort(int[] arr) {
    int n = arr.length;

    // Build max heap.
    for (int i = n / 2 - 1; i >= 0; i--) {
        heapify(arr, n, i);
    }

    // Repeatedly move maximum to the end.
    for (int end = n - 1; end > 0; end--) {
        int temp = arr[0];
        arr[0] = arr[end];
        arr[end] = temp;

        heapify(arr, end, 0);
    }
}

static void heapify(int[] arr, int heapSize, int root) {
    int largest = root;
    int left = 2 * root + 1;
    int right = 2 * root + 2;

    if (left < heapSize && arr[left] > arr[largest]) {
        largest = left;
    }

    if (right < heapSize && arr[right] > arr[largest]) {
        largest = right;
    }

    if (largest != root) {
        int temp = arr[root];
        arr[root] = arr[largest];
        arr[largest] = temp;

        heapify(arr, heapSize, largest);
    }
}
```

## A.2 Quickselect

Quickselect finds the kth smallest/largest element without fully sorting the array.

Average time:

```text
O(n)
```

Worst time:

```text
O(n^2)
```

Randomized pivot selection makes pathological behavior much less likely.

Concept:

1. Partition around a pivot.
2. Determine which side contains the target rank.
3. Recurse/iterate only into that side.

This is often preferable to sorting the entire array when only one rank is needed.

## A.3 Radix Sort

Radix sort processes digits/characters one position at a time.

For fixed-width non-negative integers with base `b` and `d` digits:

```text
O(d * (n + b))
```

It is not comparison-based, so it can beat the `O(n log n)` comparison-sorting barrier under suitable constraints.

## A.4 Bucket Sort

Bucket sort distributes values into buckets, sorts within buckets, and concatenates them.

It works well when input is distributed reasonably uniformly over a known range.

Worst-case behavior can still degrade significantly if many values fall into one bucket.

## A.5 Stable vs Unstable Sorting

A sort is **stable** when equal keys preserve their original relative order.

Example input:

```text
(Alice, 20)
(Bob, 20)
(Carol, 18)
```

After a stable age sort:

```text
(Carol, 18)
(Alice, 20)
(Bob, 20)
```

Alice remains before Bob because their keys are equal.

Stability matters when sorting by multiple attributes in stages.

---

# Appendix B — Queue Variants and Design Patterns

A queue follows **First In, First Out (FIFO)** order: the earliest enqueued item is processed first. The key operations are enqueue, dequeue, front/peek, and emptiness checking. Queues are a natural fit for breadth-first search, scheduling, buffering, and any workflow that must preserve arrival order.

## B.1 Circular Queue

A circular queue reuses freed positions in a fixed-size array.

Core state:

```text
head
size
capacity
```

Logical position `i` can map to physical index:

```text
(head + i) % capacity
```

Use cases:

- fixed-size buffers
- streaming systems
- producer/consumer queues
- round-robin scheduling

## B.2 Queue Using Two Stacks

Maintain:

- `inStack` for new elements
- `outStack` for removals

When `outStack` is empty, transfer everything from `inStack` to `outStack`.

Although one transfer can cost `O(n)`, each element moves only a constant number of times, giving amortized `O(1)` operations.

## B.3 Stack Using Queues

This is mainly an educational exercise showing how one ADT can be implemented using another.

Possible strategy:

1. Push a new element into a queue.
2. Rotate previous elements behind it.
3. Queue front now behaves like stack top.

---

# Appendix C — Hashing Internals

Understanding internals helps explain when hashing performs well and when it does not.

## C.1 Hash Function

A hash function converts a key into an integer-like hash value.

The table then maps the hash to a bucket.

A good hash function should spread typical keys reasonably evenly.

## C.2 Collision

A collision occurs when different keys map to the same bucket.

Hash tables must resolve collisions using strategies such as:

- separate chaining
- open addressing

Java's `HashMap` handles collisions internally.

## C.3 Load Factor

Load factor roughly measures:

```text
number of stored entries / number of buckets
```

As a table becomes crowded, lookup can become slower, so implementations resize when necessary.

## C.4 Why `equals()` and `hashCode()` Matter

For custom objects used as hash keys:

- equal objects must produce the same hash code
- `equals()` must follow its mathematical contract

A broken equality/hash implementation can make `HashMap` and `HashSet` behave unexpectedly.

---

# Appendix D — Balanced and Multiway Trees

A tree is a connected acyclic hierarchical structure with nodes linked by parent/child relationships. Tree algorithms are easiest to understand recursively: define what one subtree call returns, choose a traversal order, and account for tree height because recursion/operation cost can degrade on skewed trees.

## D.1 Why Ordinary BSTs Can Become Slow

Insert values:

```text
1, 2, 3, 4, 5
```

into a plain BST and it may become a chain:

```text
1
 \
  2
   \
    3
     \
      4
       \
        5
```

Search becomes `O(n)`.

Balanced trees keep height near `O(log n)`.

## D.2 AVL Tree

An AVL tree is a self-balancing BST where each node's balance factor is typically limited to:

```text
-1, 0, +1
```

Rebalancing uses rotations:

- left rotation
- right rotation
- left-right rotation
- right-left rotation

AVL trees are excellent for learning tree rotations and strict balancing.

## D.3 Red-Black Tree

A red-black tree maintains looser balance using node colors and structural rules.

This guarantees `O(log n)` search, insertion, and deletion.

Java's ordered map/set implementations are based on balanced-tree concepts; as a DSA learner, understand the guarantees and rotation/recoloring ideas even if you do not frequently implement one from scratch.

## D.4 B-Tree and B+ Tree

Binary trees are not always ideal for storage systems because disk/page access is expensive.

B-Trees use many children per node, reducing tree height.

B+ Trees store records primarily in leaves and commonly link leaves for efficient range scans.

Typical applications:

- database indexes
- file systems
- storage engines

---

# Appendix E — Advanced Tree Algorithms

These topics extend the core toolkit for problems with stronger performance, query, or modeling requirements. Study them after the foundational data structures and patterns are comfortable so the additional invariants and implementation complexity remain understandable.

## E.1 Tree Diameter Using Two BFS/DFS Passes

For an unweighted tree:

1. Start from any node `x`.
2. Find a farthest node `a`.
3. Start from `a`.
4. Find a farthest node `b`.
5. Distance `a -> b` is the tree diameter.

This technique is simple and powerful.

## E.2 Euler Tour / Flattening a Tree

A DFS can assign each node an entry time and exit time.

A subtree can then correspond to a contiguous interval in DFS order.

This converts some tree problems into array range-query problems.

Common combination:

```text
Euler tour + Fenwick tree
Euler tour + segment tree
```

Use cases:

- subtree sum
- subtree update
- query all descendants

## E.3 Binary Lifting for Ancestor Queries

Precompute:

```text
up[node][j] = 2^j-th ancestor of node
```

Then kth ancestor or Lowest Common Ancestor queries can often be answered in `O(log n)`.

Preprocessing is usually `O(n log n)`.

## E.4 Tree DP

DP is not limited to arrays.

A tree DP state may represent:

```text
best answer for the subtree rooted at node
```

Examples:

- maximum independent set on a tree
- choose/not choose node
- subtree path values
- rerooting problems

## E.5 Rerooting DP

Sometimes you need an answer assuming **every node** is the root.

A common strategy:

1. First DFS computes subtree information.
2. Second DFS transfers parent/outside information to children.

This can reduce an otherwise `O(n²)` approach to `O(n)` or `O(n log n)`.

---

# Appendix F — More Graph Patterns

Graph patterns often appear under non-graph wording such as dependencies, routes, friendships, transformations, or grouping. This appendix focuses on recognizing structural properties—direction, weights, components, cycles, ordering, and connectivity changes—before choosing a traversal or specialized algorithm.

## F.1 Bipartite Graph

A graph is bipartite if vertices can be divided into two groups such that every edge goes between groups.

Equivalent view:

> Can the graph be colored with two colors so adjacent nodes have different colors?

BFS implementation:

```java
static boolean isBipartite(List<List<Integer>> graph) {
    int n = graph.size();
    int[] color = new int[n];
    Arrays.fill(color, -1);

    for (int start = 0; start < n; start++) {
        if (color[start] != -1) continue;

        Queue<Integer> queue = new ArrayDeque<>();
        queue.offer(start);
        color[start] = 0;

        while (!queue.isEmpty()) {
            int u = queue.poll();

            for (int v : graph.get(u)) {
                if (color[v] == -1) {
                    color[v] = color[u] ^ 1;
                    queue.offer(v);
                } else if (color[v] == color[u]) {
                    return false;
                }
            }
        }
    }

    return true;
}
```

Use cases:

- two-team assignment
- conflict grouping
- matching problems

## F.2 Multi-Source BFS

Instead of one source, enqueue all sources at distance 0.

Examples:

- distance to nearest hospital
- spreading fire
- rotten oranges
- nearest zero in matrix

This often avoids running BFS separately from every source.

## F.3 A* Search — Concept

A* extends shortest-path search with a heuristic estimate:

```text
priority = distanceSoFar + estimatedDistanceToGoal
```

If the heuristic is admissible and well-behaved, A* can search dramatically fewer states than uninformed shortest-path methods.

Common application:

- pathfinding in maps and games

## F.4 Maximum Flow

A flow network has:

- source
- sink
- directed capacities

Goal:

> Send as much flow as possible from source to sink without exceeding capacities.

Key concepts:

- residual graph
- augmenting path
- max-flow/min-cut theorem

Important algorithms:

- Ford-Fulkerson
- Edmonds-Karp
- Dinic's algorithm

Applications:

- network routing
- assignment
- scheduling
- bipartite matching

## F.5 Bipartite Matching

Goal:

> Match left-side entities to right-side entities without reusing a vertex.

Examples:

- workers to jobs
- students to projects
- drivers to requests

It can be solved with augmenting paths or reduced to max flow.

---

# Appendix G — Advanced Dynamic Programming Patterns

Advanced DP expands the same fundamentals—state, transition, base cases, evaluation order—into multidimensional, interval, tree, bitmask, digit, or optimization-heavy states. The first task is always to prove what one state represents and why transitions cover all valid choices exactly as intended.

## G.1 State Compression / Bitmask DP

Use a bitmask when a state depends on a small set of selected items.

Example state:

```text
dp[mask]
```

where bit `i` indicates whether item `i` has been used.

Common problems:

- traveling salesperson for small `n`
- assignment problems
- visit-all-nodes variants

Complexity often looks like:

```text
O(n * 2^n)
```

## G.2 Digit DP

Digit DP counts numbers in a range that satisfy digit-related constraints.

Typical state contains:

```text
position
restricted/tight flag
started flag
other problem-specific information
```

Useful for questions like:

> How many numbers from 1 to N have no repeated digits?

## G.3 Interval DP

Interval DP defines a state over a contiguous range, commonly `dp[left][right]`, and combines answers from smaller subintervals. It appears in problems such as matrix-chain multiplication, optimal parenthesization, or bursting balloons. The challenge is choosing the interval length/order so every dependency has already been computed.

State describes an interval:

```text
dp[left][right]
```

Examples:

- matrix chain multiplication
- burst balloons
- optimal game strategies

A common transition tries a split point `k` inside the interval.

## G.4 Partition DP

Split a sequence into groups and optimize the total score/cost.

Typical form:

```text
dp[i] = best answer for first i elements
```

Try where the last partition begins.

## G.5 DP on DAG

A DAG has no cycles, so topological order naturally gives a valid DP computation order.

Examples:

- longest path in DAG
- number of paths
- dependency-based optimization

## G.6 Tree DP

Tree DP computes a state for each node from states of its children (or from a rerooted parent/child relationship). A DFS usually establishes the processing order. Clearly define what each state means—for example, 'best answer in this subtree if the node is chosen'—because correctness depends on combining child states consistently.

As described earlier, tree structure provides natural subproblems rooted at nodes.

Often state tracks whether a node is selected or some information about parent choice.

## G.7 Memoization State Design Mistake

A frequent error is forgetting a variable that affects future decisions.

Suppose answer depends on:

```text
index AND remaining capacity
```

Then memoizing only by `index` is incorrect because two calls at the same index with different capacity are different subproblems.

---

# Appendix H — Advanced String Structures

These topics extend the core toolkit for problems with stronger performance, query, or modeling requirements. Study them after the foundational data structures and patterns are comfortable so the additional invariants and implementation complexity remain understandable.

## H.1 Rolling Hash

A rolling hash allows a substring hash to be updated or retrieved efficiently after preprocessing.

Typical uses:

- duplicate substring detection
- substring equality checks
- Rabin-Karp

Because collisions are possible, correctness-critical solutions may use:

- double hashing
- explicit verification after hash match

## H.2 Suffix Array — Concept

A suffix array stores starting indexes of all suffixes in lexicographically sorted order.

For:

```text
banana
```

suffixes include:

```text
banana
anana
nana
ana
na
a
```

Once suffixes are ordered, many substring problems become structured searches.

Applications:

- pattern search
- repeated substring problems
- lexicographic suffix queries

## H.3 LCP Array

LCP means Longest Common Prefix between neighboring suffixes in suffix-array order.

Combining suffix array + LCP helps solve:

- longest repeated substring
- common substring analysis

## H.4 Manacher's Algorithm — Concept

Manacher's algorithm finds palindromic radii for all centers in linear time.

You do not need it for most interviews, but it is a useful advanced string technique after mastering expand-around-center and DP approaches.

---

# Appendix I — Randomization and Probabilistic Thinking

Randomization is useful when deterministic choices can trigger bad cases.

Examples:

- randomized quicksort pivot
- randomized quickselect
- hashing defenses
- randomized test generation

Randomized algorithms are analyzed using expected behavior rather than only a fixed execution path.

---

# Appendix J — Amortized Analysis

Amortized analysis studies the average cost of operations over a sequence, even when occasional individual operations are expensive.

Classic example: dynamic arrays.

Suppose capacity doubles:

```text
1 -> 2 -> 4 -> 8 -> 16 -> ...
```

A resize copies many elements, but resizes happen infrequently.

Across `n` appends, the total copying work is still `O(n)`, making append amortized `O(1)`.

Other areas where amortized thinking appears:

- monotonic stacks
- two-stack queues
- union-find
- some caching structures

---

# Appendix K — Invariants: The Hidden Skill Behind Correct Algorithms

An **invariant** is a statement that remains true throughout an algorithm.

Examples:

## Binary search invariant

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

```text
If target exists, it remains inside the current search interval.
```

## Sliding window invariant

A sliding window tracks a contiguous range while updating only the information that changes when the range expands or shrinks. Fixed-size windows are used when the length is known; variable-size windows adjust a boundary until a validity condition is restored. The usual goal is to replace repeated recomputation of every subarray or substring with a single linear pass.

```text
The current window satisfies the maintained frequency/count rules.
```

## Dijkstra invariant

With non-negative edge weights, once Dijkstra removes the currently smallest-distance **unprocessed** vertex from the priority queue, that distance is final. Any alternative path reaching it later would have to add a non-negative edge to a path that was already at least as large.

```text
When a valid minimum-distance state is finalized from the priority queue, no shorter non-negative path can later appear.
```

## Monotonic stack invariant

A monotonic stack keeps its elements in increasing or decreasing order by removing values that can no longer be useful. Each element is pushed and popped at most once, so many nearest-greater/nearest-smaller problems become `O(n)`. The crucial design decision is whether the stack stores values or indexes and which comparison preserves the needed candidate boundary.

```text
Indexes in the stack correspond to values maintained in a chosen monotonic order.
```

Thinking in invariants is one of the best ways to move from “code that seems right” to algorithms you can actually prove correct.

---

# Appendix L — Data Structure Selection Guide

Choose based on the operations you need most often.

| Need | Strong default |
|---|---|
| indexed access | array / ArrayList |
| append sequence | ArrayList |
| LIFO | ArrayDeque as stack |
| FIFO | ArrayDeque as queue |
| both ends | ArrayDeque |
| key -> value | HashMap |
| uniqueness | HashSet |
| sorted keys | TreeMap |
| sorted unique values | TreeSet |
| repeatedly smallest/largest | PriorityQueue |
| prefix strings | Trie |
| dynamic connectivity | DSU |
| dynamic prefix sums | Fenwick Tree |
| flexible range query/update | Segment Tree |
| hierarchical ordered search | balanced BST |
| arbitrary relationships | Graph |

---

# Appendix M — Problem Difficulty Progression

When learning a pattern, do not jump directly from the definition to the hardest problem.

Use this progression:

```text
Level 1: direct implementation
Level 2: one pattern with obvious trigger
Level 3: same pattern with a hidden trigger
Level 4: combine two patterns
Level 5: optimize memory/time
Level 6: prove correctness under tricky constraints
```

Example for sliding window:

```text
1. Maximum sum of fixed k
2. Longest substring without duplicates
3. Minimum window satisfying counts
4. Sliding window + frequency map
5. Sliding window + deque
6. Multiple constraints / transformed windows
```

---

# Appendix N — Building Your Personal DSA Library

Create a personal directory such as:

```text
dsa-java/
├── arrays/
├── strings/
├── linked-list/
├── stack-queue/
├── trees/
├── graphs/
├── dynamic-programming/
├── advanced/
├── templates/
└── notes/
```

For each solved problem, keep:

```text
README.md          -> explanation
Solution.java      -> clean final implementation
BruteForce.java    -> optional first approach
notes.md           -> mistakes and variations
```

Do not build a library of copied answers. Build a library of ideas you can reproduce.

---

# Appendix O — Final “What Should I Learn Next?” Decision Tree

Use this decision tree to choose the next topic based on demonstrated gaps rather than novelty. Prioritize the prerequisite that blocks your current problems: basic operation costs before patterns, traversal before advanced graph/tree algorithms, and state definition before advanced dynamic programming.

Use this after finishing the basics.

```text
Can I solve basic array/string problems?
    No -> arrays, hashing, sorting, binary search
    Yes
      |
      v
Can I recognize common patterns?
    No -> two pointers, sliding window, prefix sum, heap
    Yes
      |
      v
Am I comfortable with recursion?
    No -> recursion + linked lists + trees
    Yes
      |
      v
Can I solve tree/graph traversal problems?
    No -> DFS, BFS, BST, topological sort, DSU
    Yes
      |
      v
Can I derive DP states and transitions?
    No -> 1D DP -> knapsack -> grid -> strings
    Yes
      |
      v
Need stronger interview skills?
    -> mixed pattern practice + timed mocks

Need competitive programming depth?
    -> Fenwick, segment tree, advanced graphs,
       bitmask DP, string algorithms, number theory
```

---

# Handbook Maintenance Notes

DSA fundamentals are largely language-agnostic, while Java APIs evolve over time. The examples in this handbook intentionally use broadly available Java language and collection features so they remain useful across common modern Java environments.

When maintaining your copy:

- Add constraints beside each practice problem.
- Record whether a solution is iterative or recursive.
- Note overflow risks.
- Add your own test cases.
- Add alternative implementations only when they teach a different idea.
- Revisit complexity claims whenever you change the data structure.

---

# True Mastery Standard

You can consider yourself strong in DSA when you can repeatedly do the following on unfamiliar problems:

1. Translate the story into a precise computational problem.
2. Identify constraints that rule out slow approaches.
3. Produce a correct brute-force baseline.
4. Detect the bottleneck.
5. Recognize one or more useful patterns.
6. Select the right data structure.
7. Explain an invariant or correctness argument.
8. Implement the solution cleanly in Java.
9. Analyze worst-case time and auxiliary space.
10. Test edge cases systematically.
11. Improve the solution if constraints demand it.
12. Explain tradeoffs rather than claiming one technique is always “best.”

That is the point where DSA becomes problem-solving skill rather than memorized code.
