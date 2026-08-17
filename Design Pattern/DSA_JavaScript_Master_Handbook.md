# DSA with JavaScript — Master Learning Handbook

> **Goal:** Build a complete, practical understanding of Data Structures and Algorithms (DSA) using JavaScript—from first principles to advanced interview and real-world problem-solving patterns.
>
> This handbook is designed to work as:
> - a beginner-friendly learning path,
> - a revision guide,
> - an interview-preparation reference,
> - a collection of reusable JavaScript templates,
> - and a single long-term DSA knowledge base.

---

# Table of Contents

1. [How to Use This Handbook](#1-how-to-use-this-handbook)
2. [What Are Data Structures and Algorithms?](#2-what-are-data-structures-and-algorithms)
3. [JavaScript Foundations for DSA](#3-javascript-foundations-for-dsa)
4. [Time and Space Complexity](#4-time-and-space-complexity)
5. [Problem-Solving Framework](#5-problem-solving-framework)
6. [Arrays](#6-arrays)
7. [Strings](#7-strings)
8. [Hash Maps and Sets](#8-hash-maps-and-sets)
9. [Linked Lists](#9-linked-lists)
10. [Stacks](#10-stacks)
11. [Queues and Deques](#11-queues-and-deques)
12. [Recursion](#12-recursion)
13. [Searching Algorithms](#13-searching-algorithms)
14. [Sorting Algorithms](#14-sorting-algorithms)
15. [Two Pointers](#15-two-pointers)
16. [Sliding Window](#16-sliding-window)
17. [Prefix Sum and Difference Arrays](#17-prefix-sum-and-difference-arrays)
18. [Matrices and Grids](#18-matrices-and-grids)
19. [Backtracking](#19-backtracking)
20. [Trees](#20-trees)
21. [Binary Search Trees](#21-binary-search-trees)
22. [Heaps and Priority Queues](#22-heaps-and-priority-queues)
23. [Tries](#23-tries)
24. [Graphs](#24-graphs)
25. [Union-Find / Disjoint Set Union](#25-union-find--disjoint-set-union)
26. [Greedy Algorithms](#26-greedy-algorithms)
27. [Dynamic Programming](#27-dynamic-programming)
28. [Bit Manipulation](#28-bit-manipulation)
29. [Mathematics for DSA](#29-mathematics-for-dsa)
30. [Monotonic Stack and Queue](#30-monotonic-stack-and-queue)
31. [String-Matching Algorithms](#31-string-matching-algorithms)
32. [Segment Trees](#32-segment-trees)
33. [Fenwick Tree / Binary Indexed Tree](#33-fenwick-tree--binary-indexed-tree)
34. [Advanced Graph Algorithms](#34-advanced-graph-algorithms)
35. [Advanced Dynamic Programming](#35-advanced-dynamic-programming)
36. [Common Interview Patterns](#36-common-interview-patterns)
37. [JavaScript-Specific DSA Pitfalls](#37-javascript-specific-dsa-pitfalls)
38. [Reusable JavaScript Templates](#38-reusable-javascript-templates)
39. [DSA Learning Roadmap](#39-dsa-learning-roadmap)
40. [Practice Strategy](#40-practice-strategy)
41. [Complexity Cheat Sheet](#41-complexity-cheat-sheet)
42. [Pattern Recognition Cheat Sheet](#42-pattern-recognition-cheat-sheet)
43. [Interview Preparation Checklist](#43-interview-preparation-checklist)
44. [Mini Projects for DSA Practice](#44-mini-projects-for-dsa-practice)
45. [Final Revision Notes](#45-final-revision-notes)
46. [Additional Linked List Types](#appendix-s--additional-linked-list-types)
47. [Additional Sorting and Selection Algorithms](#appendix-t--additional-sorting-and-selection-algorithms)
48. [Tree Types You Should Know](#appendix-u--tree-types-you-should-know)
49. [Graph Representation and Cycle Detection](#appendix-v--graph-representation-and-cycle-detection)
50. [Full Shortest-Path Reference](#appendix-w--full-shortest-path-reference)
51. [Divide and Conquer](#appendix-x--divide-and-conquer)
52. [Amortized Analysis in Practice](#appendix-y--amortized-analysis-in-practice)
53. [Final DSA Decision Tree](#appendix-z--final-dsa-decision-tree)

---

# 1. How to Use This Handbook

Do not try to memorize every algorithm immediately.

A better cycle is:

1. **Understand the problem.**
2. **Write a brute-force solution.**
3. **Identify the bottleneck.**
4. **Choose a data structure or pattern that removes the bottleneck.**
5. **Implement it yourself.**
6. **Analyze time and space complexity.**
7. **Solve 3–10 related problems.**
8. **Revisit the topic later without looking at notes.**

For each topic, ask:

- What problem does this solve?
- Why is this data structure useful?
- What operations are fast?
- What operations are slow?
- What are the common patterns?
- When should I not use it?
- Can I implement it from scratch?
- Can I explain it to another person?

---

# 2. What Are Data Structures and Algorithms?

Data Structures and Algorithms (DSA) is the study of how to organize data and how to process it efficiently and correctly. The practical skill is choosing operations and representations that fit the constraints, then proving correctness and understanding the time/memory trade-off.

## 2.1 Data Structure

A **data structure** is a method for organizing data so that certain operations become efficient.

Examples:

- Array → ordered values and fast indexed access
- Hash Map → fast key-based lookup
- Stack → last-in-first-out processing
- Queue → first-in-first-out processing
- Heap → quickly retrieve minimum/maximum priority
- Tree → hierarchical data
- Graph → relationships and networks

### Real-world analogy

Suppose a company stores employee information.

If employees are stored in a plain array:

```js
const employees = [
  { id: 101, name: "Aisha" },
  { id: 102, name: "Ravi" },
  { id: 103, name: "Meera" }
];
```

To find employee `103`, we may scan the array.

But if we use a Map:

```js
const employeeById = new Map();

employeeById.set(101, { name: "Aisha" });
employeeById.set(102, { name: "Ravi" });
employeeById.set(103, { name: "Meera" });

console.log(employeeById.get(103));
```

Lookup becomes conceptually much faster for large datasets.

---

## 2.2 Algorithm

An **algorithm** is a finite sequence of steps used to solve a problem.

Example: Find the largest number.

```js
function findMax(nums) {
  let max = nums[0];

  for (let i = 1; i < nums.length; i++) {
    if (nums[i] > max) {
      max = nums[i];
    }
  }

  return max;
}
```

The data structure is the array.  
The algorithm is the procedure used to find the maximum.

---

## 2.3 Why DSA Matters

DSA improves your ability to:

- solve problems systematically,
- write scalable software,
- understand performance,
- design efficient APIs and services,
- optimize database or in-memory processing,
- prepare for technical interviews,
- understand how libraries work internally.

---

# 3. JavaScript Foundations for DSA

You do not need all of JavaScript before learning DSA, but you must be comfortable with the following.

## 3.1 Variables

Variables give names to values and state used by an algorithm. In DSA code, use descriptive names for indexes, boundaries, counters, and accumulated results because unclear state is a common source of off-by-one and update-order bugs.

```js
let count = 0;
const limit = 10;
```

Prefer `const` unless reassignment is required.

---

## 3.2 Arrays

An array-like structure stores elements in an indexed sequence. Its main advantage is direct access by position; the main trade-off is that inserting or deleting near the front or middle usually requires shifting elements. In DSA problems, arrays are also the base structure behind two pointers, sliding windows, prefix sums, binary search, heaps, and many dynamic-programming tables.

```js
const nums = [10, 20, 30];

nums.push(40);
nums.pop();

console.log(nums[0]);
console.log(nums.length);
```

Important methods:

```js
arr.push(value);      // add to end
arr.pop();            // remove from end
arr.shift();          // remove from beginning
arr.unshift(value);   // add to beginning
arr.slice(start, end);
arr.splice(start, deleteCount);
arr.includes(value);
arr.indexOf(value);
arr.reverse();
arr.sort();
```

### Important warning

This warning highlights a language behavior that can silently change the algorithm's result or complexity. Treat default library semantics—especially sorting, numeric precision, and mutating array methods—as part of the algorithm contract rather than assuming behavior from another language.

JavaScript's default `sort()` compares elements as strings unless you provide a comparator. That can produce an order that is wrong for numeric DSA problems. `sort()` also **mutates the array**.

```js
const values = [1, 30, 4, 21, 100000];

console.log([...values].sort());
// [1, 100000, 21, 30, 4]  <- string/lexicographic order

console.log([...values].sort((a, b) => a - b));
// [1, 4, 21, 30, 100000]  <- numeric ascending order
```

The comparator receives two elements, `a` and `b`. Returning a negative value places `a` before `b`; returning a positive value places `b` before `a`; returning `0` leaves them equal for ordering purposes.

Use:

```js
nums.sort((a, b) => a - b); // numeric ascending; mutates nums
nums.sort((a, b) => b - a); // numeric descending; mutates nums
```

The spread expression `[...values]` above creates a shallow copy so the demonstration does not modify the original `values` array.

---

## 3.3 Objects

Plain JavaScript objects can store key/value pairs, but property keys are strings or symbols and objects inherit object-oriented behavior/prototype semantics. For arbitrary dynamic DSA keys, especially non-string keys, `Map` often communicates intent more clearly and provides a dedicated key-value API.

```js
const frequencies = {};

frequencies["apple"] = 2;
frequencies["banana"] = 5;
```

For DSA, `Map` is often clearer when keys are dynamic.

---

## 3.4 Map

JavaScript `Map` stores key/value pairs and accepts keys of any value type. Core operations are `set`, `get`, `has`, and `delete`; iteration preserves insertion order. It is commonly used for frequency maps, index lookup, graph tables, and memoization.

```js
const map = new Map();

map.set("a", 10);
map.set("b", 20);

console.log(map.get("a"));
console.log(map.has("b"));

map.delete("a");
```

Iteration:

```js
for (const [key, value] of map) {
  console.log(key, value);
}
```

---

## 3.5 Set

A set stores unique values and is designed for membership testing. In DSA it is useful for duplicate detection, visited states, and window membership. It does not provide positional indexing; use a sequence when index-based order is the main operation.

```js
const seen = new Set();

seen.add(10);
seen.add(20);

console.log(seen.has(10));

seen.delete(20);
```

Useful for:

- duplicate detection,
- visited nodes,
- unique elements,
- membership testing.

---

## 3.6 Loops

Loops express repeated state updates. In DSA, choose the loop form that makes boundaries and mutation obvious: index-based loops for positions and direct iteration for values. Boundary clarity matters more than syntax brevity.

```js
for (let i = 0; i < nums.length; i++) {
  console.log(nums[i]);
}
```

```js
for (const value of nums) {
  console.log(value);
}
```

Avoid `for...in` for array values because it iterates property keys.

---

## 3.7 Functions

A function/method packages a reusable piece of algorithmic work behind inputs and a return value. For DSA helpers, make the contract explicit: what each parameter represents, whether the input is mutated, what is returned, and what happens for empty or invalid input.

```js
function add(a, b) {
  return a + b;
}
```

Arrow function:

```js
const add = (a, b) => a + b;
```

---

## 3.8 Classes

Classes are useful in DSA for nodes, heaps, tries, graphs, or reusable structures that own state plus operations. Keep fields tied to one invariant and expose methods that preserve it; a class is unnecessary when a small pure function solves the problem more clearly.

Useful when implementing linked lists, trees, heaps, graphs, etc.

```js
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}
```

---

## 3.9 Destructuring

Destructuring extracts values from arrays or properties from objects into local variables. It can make DSA code clearer when unpacking pairs, coordinates, queue entries, or map entries, but overly nested destructuring can make state changes harder to follow.

```js
const [a, b] = [10, 20];

const user = { name: "Ali", age: 25 };
const { name, age } = user;
```

---

## 3.10 Swap Trick

Swapping exchanges two values without changing the rest of the data. It is common in sorting, partitioning, reversal, and heap operations. Ensure both positions are valid before swapping; in-place algorithms rely on this operation preserving all values rather than losing one through overwrite.

```js
[a, b] = [b, a];
```

Useful in sorting and two-pointer problems.

---

## 3.11 Number Limitations

JavaScript `Number` uses IEEE-754 double precision.

Safe integer range:

```js
Number.MIN_SAFE_INTEGER
Number.MAX_SAFE_INTEGER
```

For very large integers:

```js
const huge = 12345678901234567890n;
```

Use `BigInt` when the problem requires integer precision beyond safe `Number` limits.

Do not directly mix `BigInt` and `Number`:

```js
// 10n + 5 // TypeError
10n + 5n;
```

---

## 3.12 Node.js Competitive Programming Input Template

This template reads standard input once and tokenizes/parses it for fast contest-style access. Keep parsing logic separate from the algorithm, and be explicit about numeric conversion because input tokens arrive as strings. For very large inputs, avoid repeated expensive string operations inside the main solving loop.

```js
const fs = require("fs");

const input = fs.readFileSync(0, "utf8").trim();
const tokens = input.split(/\s+/);

let index = 0;

const n = Number(tokens[index++]);

const nums = [];
for (let i = 0; i < n; i++) {
  nums.push(Number(tokens[index++]));
}

console.log(nums);
```

---

# 4. Time and Space Complexity

Complexity analysis estimates how an algorithm's resource usage grows as input size increases. Focus on the dominant growth rate rather than machine-specific timing, and analyze both execution work and extra memory so you can compare approaches before benchmarking.

Complexity measures how resource usage grows with input size.

Let `n` represent input size.

---

## 4.1 Big O

Big O commonly describes an upper bound on growth.

Typical complexities:

| Complexity | Name | Example |
|---|---|---|
| O(1) | Constant | Array index access |
| O(log n) | Logarithmic | Binary search |
| O(n) | Linear | Scan array |
| O(n log n) | Linearithmic | Merge sort |
| O(n²) | Quadratic | Nested loops |
| O(n³) | Cubic | Triple nested loops |
| O(2ⁿ) | Exponential | Some subset recursion |
| O(n!) | Factorial | Permutations |

---

## 4.2 O(1)

`O(1)` means the amount of work does not grow with the number of input elements. It does **not** mean the operation takes exactly one CPU instruction; it means the step count is bounded by a constant with respect to input size. Examples include reading a known array index or checking a stored variable.

```js
function first(arr) {
  return arr[0];
}
```

Input size does not affect the number of steps significantly.

---

## 4.3 O(n)

`O(n)` means the running time grows proportionally with the input size. A single complete pass over an array is the standard example. Several separate linear passes are still `O(n)` because constant multipliers are omitted in asymptotic analysis.

```js
function sum(arr) {
  let total = 0;

  for (const num of arr) {
    total += num;
  }

  return total;
}
```

---

## 4.4 O(n²)

`O(n²)` usually appears when the algorithm examines many pairs of input elements, such as two nested loops over the same `n` items. Doubling `n` can make the dominant work roughly four times larger, so quadratic approaches become expensive quickly on large inputs.

```js
for (let i = 0; i < n; i++) {
  for (let j = 0; j < n; j++) {
    // work
  }
}
```

---

## 4.5 O(log n)

`O(log n)` appears when each step reduces the remaining problem by a constant factor, often by half. Binary search is the classic example. The logarithm base is ignored in Big-O because changing the base only multiplies the count by a constant factor.

Repeatedly cutting the search space in half creates logarithmic complexity.

Example: binary search.

---

## 4.6 O(n log n)

`O(n log n)` commonly appears when an algorithm performs logarithmic levels of work and processes `O(n)` data across each level. Efficient comparison sorts such as merge sort and heap sort have this bound; divide-and-conquer algorithms often produce it as well.

Efficient comparison-based sorting algorithms often achieve O(n log n).

Examples:

- merge sort,
- heap sort,
- average-case quicksort.

---

## 4.7 Space Complexity

Space complexity measures how much additional memory grows with input size. Distinguish the input itself from **auxiliary space** used by the algorithm, and remember to include recursion depth, temporary arrays, hash tables, queues, and stacks. An in-place algorithm usually means `O(1)` or very small auxiliary storage, not that the input occupies no memory.

Space complexity measures additional memory.

Example:

```js
function doubled(arr) {
  const result = [];

  for (const num of arr) {
    result.push(num * 2);
  }

  return result;
}
```

Extra array → O(n) auxiliary space.

---

## 4.8 Drop Constants

Big-O ignores constant multipliers because they do not change asymptotic growth. `O(3n)` is written as `O(n)`. Constants can still matter in real benchmarking, so asymptotic simplification is for growth-rate comparison, not a claim that implementations with the same Big-O run equally fast.

O(2n) becomes O(n).

O(100) becomes O(1).

---

## 4.9 Keep Dominant Term

When several growth terms are added, the fastest-growing term dominates for large `n`. For example, `O(n² + n + 10)` simplifies to `O(n²)`. This simplification is valid for asymptotic analysis even though lower-order work can matter for small inputs.

O(n² + n + 10) becomes O(n²).

---

## 4.10 Amortized Complexity

Some operations are occasionally expensive but cheap on average.

Dynamic array `push()` is usually considered amortized O(1), even though resizing the internal storage can occasionally cost O(n).

---

## 4.11 Input Size Heuristic

These are rough interview/competitive-programming heuristics:

| n | Often Acceptable |
|---:|---|
| 10 | O(n!) may sometimes work |
| 20 | O(2ⁿ) may work |
| 100 | O(n³) may work |
| 1,000 | O(n²) may work |
| 100,000 | O(n log n) / O(n) |
| 1,000,000 | Usually O(n) or O(n log n) carefully |

Actual limits depend on language, environment, constants, and time limit.

---

# 5. Problem-Solving Framework

A problem-solving framework turns an unfamiliar prompt into a sequence of verifiable decisions. Clarify the contract, build a correct baseline, locate repeated work, choose a structure/pattern that removes it, state why the optimization is valid, and test the boundaries.

Use this framework consistently.

## Step 1: Understand the problem

This step is part of turning a problem statement into a defensible solution. Do it explicitly before moving on: the result of this step should give you concrete information you can use to choose, verify, or explain the algorithm.

Identify:

- input,
- output,
- constraints,
- edge cases,
- whether ordering matters,
- whether duplicates matter,
- whether negative values exist,
- whether the input is sorted.

---

## Step 2: Work through examples

This step is part of turning a problem statement into a defensible solution. Do it explicitly before moving on: the result of this step should give you concrete information you can use to choose, verify, or explain the algorithm.

Example problem:

> Find two numbers whose sum equals a target.

Input:

```txt
[2, 7, 11, 15], target = 9
```

Output:

```txt
[0, 1]
```

---

## Step 3: Start with brute force

This step is part of turning a problem statement into a defensible solution. Do it explicitly before moving on: the result of this step should give you concrete information you can use to choose, verify, or explain the algorithm.

```js
function twoSum(nums, target) {
  for (let i = 0; i < nums.length; i++) {
    for (let j = i + 1; j < nums.length; j++) {
      if (nums[i] + nums[j] === target) {
        return [i, j];
      }
    }
  }

  return [];
}
```

Complexity:

- Time: O(n²)
- Space: O(1)

---

## Step 4: Identify repeated work

This step is part of turning a problem statement into a defensible solution. Do it explicitly before moving on: the result of this step should give you concrete information you can use to choose, verify, or explain the algorithm.

For each number, brute force repeatedly searches for its complement.

Complement:

```txt
target - currentNumber
```

Use a Hash Map.

```js
function twoSum(nums, target) {
  const seen = new Map();

  for (let i = 0; i < nums.length; i++) {
    const needed = target - nums[i];

    if (seen.has(needed)) {
      return [seen.get(needed), i];
    }

    seen.set(nums[i], i);
  }

  return [];
}
```

Complexity:

- Time: O(n) average
- Space: O(n)

---

## Step 5: Test edge cases

This step is part of turning a problem statement into a defensible solution. Do it explicitly before moving on: the result of this step should give you concrete information you can use to choose, verify, or explain the algorithm.

Test:

- empty input,
- one element,
- duplicates,
- negatives,
- answer at beginning,
- answer at end,
- no answer.

---

# 6. Arrays

An array-like structure stores elements in an indexed sequence. Its main advantage is direct access by position; the main trade-off is that inserting or deleting near the front or middle usually requires shifting elements. In DSA problems, arrays are also the base structure behind two pointers, sliding windows, prefix sums, binary search, heaps, and many dynamic-programming tables.

An array stores elements in order.

```js
const arr = [10, 20, 30];
```

## 6.1 Common Operations

| Operation | Typical Complexity |
|---|---:|
| Access by index | O(1) |
| Search unsorted | O(n) |
| Push | Amortized O(1) |
| Pop | O(1) |
| Shift | O(n) |
| Unshift | O(n) |
| Insert/delete middle | O(n) |

---

## 6.2 Traversal

Traversal means visiting each relevant element/node in a defined order. The important state is the current position and the rule for advancing to the next one. A full traversal is usually `O(n)` for a linear structure, while trees/graphs additionally require a stack/queue or recursion and, for cyclic graphs, visited tracking.

```js
for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]);
}
```

---

## 6.3 Find Maximum

Finding a maximum requires a baseline that is valid for the input domain. Initialize from the first element (after handling empty input) rather than from `0`, which fails when every value is negative. Then scan once and replace the current maximum whenever a larger value appears: `O(n)` time, `O(1)` extra space.

```js
function maxValue(nums) {
  if (nums.length === 0) return undefined;

  let max = nums[0];

  for (let i = 1; i < nums.length; i++) {
    if (nums[i] > max) {
      max = nums[i];
    }
  }

  return max;
}
```

---

## 6.4 Reverse In Place

In-place reversal swaps symmetric elements from the two ends and moves inward until the pointers meet. Each element is touched a constant number of times, giving `O(n)` time and `O(1)` auxiliary space. The input array is mutated, so callers that need the original order must copy it first.

```js
function reverseArray(nums) {
  let left = 0;
  let right = nums.length - 1;

  while (left < right) {
    [nums[left], nums[right]] = [nums[right], nums[left]];
    left++;
    right--;
  }

  return nums;
}
```

---

## 6.5 Remove Duplicates from Sorted Array

Because the array is sorted, equal values appear next to one another. A read pointer scans every element while a write pointer marks where the next distinct value belongs. The algorithm runs in `O(n)` time and can overwrite the input in place using `O(1)` extra space; the returned length/count tells the caller which prefix contains the unique values.

```js
function removeDuplicates(nums) {
  if (nums.length === 0) return 0;

  let write = 1;

  for (let read = 1; read < nums.length; read++) {
    if (nums[read] !== nums[read - 1]) {
      nums[write] = nums[read];
      write++;
    }
  }

  return write;
}
```

Pattern: **read pointer + write pointer**.

---

## 6.6 Rotate Array

Array rotation shifts positions cyclically. Normalize the shift with modulo so values larger than the array length do not cause repeated work. Common approaches are a new array (`O(n)` extra space) or the three-reversal method (`O(1)` extra space for mutable arrays).

Rotate right by `k`.

```js
function reverse(nums, left, right) {
  while (left < right) {
    [nums[left], nums[right]] = [nums[right], nums[left]];
    left++;
    right--;
  }
}

function rotate(nums, k) {
  const n = nums.length;
  if (n === 0) return nums;

  k %= n;

  reverse(nums, 0, n - 1);
  reverse(nums, 0, k - 1);
  reverse(nums, k, n - 1);

  return nums;
}
```

Time: O(n)  
Space: O(1)

---

## 6.7 Maximum Subarray — Kadane's Algorithm

Problem:

> Find the contiguous subarray with the largest sum.

```js
function maxSubArray(nums) {
  let current = nums[0];
  let best = nums[0];

  for (let i = 1; i < nums.length; i++) {
    current = Math.max(nums[i], current + nums[i]);
    best = Math.max(best, current);
  }

  return best;
}
```

Core idea:

At each position, decide:

- start a new subarray here, or
- extend the previous subarray.

Time: O(n)  
Space: O(1)

---

# 7. Strings

A string is a sequence of characters, but its exact behavior depends on the language's string model and character encoding. DSA string problems commonly need indexing/traversal, frequency counting, substring handling, comparison, prefix/suffix reasoning, or pattern matching. Always check whether the task assumes simple ASCII-like characters or full Unicode text.

JavaScript strings are immutable.

```js
let text = "hello";
```

You cannot directly modify one character:

```js
// text[0] = "H"; // does not change the string
```

Convert when needed:

```js
const chars = text.split("");
chars[0] = "H";
text = chars.join("");
```

---

## 7.1 Character Frequency

A frequency table records how many times each value occurs. Python's `Counter` constructs this mapping directly from an iterable and is useful when counts—not just membership—are needed.

```js
function frequencyMap(str) {
  const freq = new Map();

  for (const ch of str) {
    freq.set(ch, (freq.get(ch) ?? 0) + 1);
  }

  return freq;
}
```

---

## 7.2 Palindrome

A palindrome reads the same forward and backward under the problem's comparison rules. The standard two-pointer check compares the leftmost and rightmost relevant characters and moves inward, stopping on the first mismatch. Time is `O(n)` and extra space can be `O(1)` when normalization is not stored separately.

```js
function isPalindrome(str) {
  let left = 0;
  let right = str.length - 1;

  while (left < right) {
    if (str[left] !== str[right]) {
      return false;
    }

    left++;
    right--;
  }

  return true;
}
```

---

## 7.3 Valid Anagram

Two strings are anagrams when they contain the same symbols with the same frequencies, subject to the problem's normalization rules. A frequency map gives `O(n)` expected time and avoids sorting; sorting both strings is simpler in some cases but typically costs `O(n log n)`. Decide explicitly whether case, spaces, punctuation, and Unicode normalization matter.

```js
function isAnagram(a, b) {
  if (a.length !== b.length) return false;

  const freq = new Map();

  for (const ch of a) {
    freq.set(ch, (freq.get(ch) ?? 0) + 1);
  }

  for (const ch of b) {
    if (!freq.has(ch)) return false;

    freq.set(ch, freq.get(ch) - 1);

    if (freq.get(ch) === 0) {
      freq.delete(ch);
    }
  }

  return freq.size === 0;
}
```

---

## 7.4 Longest Common Prefix

The longest common prefix is the longest starting substring shared by every string in the collection. A practical approach uses one string as the candidate prefix and shortens/compares it against the others. Handle an empty collection explicitly; the answer is an empty string when no first character is shared.

```js
function longestCommonPrefix(words) {
  if (words.length === 0) return "";

  let prefix = words[0];

  for (let i = 1; i < words.length; i++) {
    while (!words[i].startsWith(prefix)) {
      prefix = prefix.slice(0, -1);

      if (prefix === "") return "";
    }
  }

  return prefix;
}
```

---

## 7.5 String Problems Commonly Use

- frequency maps,
- two pointers,
- sliding window,
- stack,
- trie,
- dynamic programming,
- KMP/Z/Rabin-Karp for advanced matching.

---

# 8. Hash Maps and Sets

Hash-based structures trade extra memory for fast average-case membership, lookup, insertion, and deletion. They are especially useful for frequency tables, duplicate detection, complement lookup, caching, and visited-state tracking. Their ordering guarantees and worst-case behavior depend on the language and implementation, so do not assume sorted iteration unless the API explicitly provides it.

Hashing is one of the most important DSA techniques.

JavaScript provides:

```js
Map
Set
```

---

## 8.1 Why Hashing?

Suppose we repeatedly ask:

> Have I seen this value before?

Array search:

```js
arr.includes(value);
```

Worst-case O(n).

Set:

```js
seen.has(value);
```

Average expected lookup is commonly treated as O(1).

---

## 8.2 Duplicate Detection

Duplicate detection can use a set of values seen so far. If the current value is already present, a duplicate exists; otherwise add it and continue. This is `O(n)` expected time with `O(n)` extra space, compared with `O(n²)` pair checking or `O(n log n)` sorting.

```js
function containsDuplicate(nums) {
  const seen = new Set();

  for (const num of nums) {
    if (seen.has(num)) return true;
    seen.add(num);
  }

  return false;
}
```

---

## 8.3 Frequency Counting

Frequency counting scans the input and stores how many times each value occurs. A hash map gives expected `O(n)` build time; a fixed-size array can be faster and more memory-efficient when the key range is small and known. The resulting counts support duplicates, grouping, anagrams, and many window problems.

```js
function countWords(words) {
  const freq = new Map();

  for (const word of words) {
    freq.set(word, (freq.get(word) ?? 0) + 1);
  }

  return freq;
}
```

---

## 8.4 First Non-Repeating Character

Count each character first, then scan the original string again and return the first character whose frequency is one. The second pass is important because a hash map alone does not necessarily express the required original-position rule. Overall time is `O(n)`.

```js
function firstUniqueChar(s) {
  const freq = new Map();

  for (const ch of s) {
    freq.set(ch, (freq.get(ch) ?? 0) + 1);
  }

  for (let i = 0; i < s.length; i++) {
    if (freq.get(s[i]) === 1) {
      return i;
    }
  }

  return -1;
}
```

---

## 8.5 When to Think "Hash Map"

Hash-based structures trade extra memory for fast average-case membership, lookup, insertion, and deletion. They are especially useful for frequency tables, duplicate detection, complement lookup, caching, and visited-state tracking. Their ordering guarantees and worst-case behavior depend on the language and implementation, so do not assume sorted iteration unless the API explicitly provides it.

Use a map when you see:

- count,
- frequency,
- lookup by key,
- complement,
- group similar values,
- seen before,
- memoization,
- cache,
- index tracking.

---

# 9. Linked Lists

A linked list stores values in nodes connected by references rather than by contiguous indexed positions. This makes pointer rewiring cheap once the relevant node is known, but random access is slow because traversal normally starts from the head. Linked-list problems therefore focus heavily on pointer movement, insertion/removal, reversal, cycle detection, and fast/slow-pointer techniques.

A linked list consists of nodes.

Each node stores:

- value,
- pointer/reference to the next node.

---

## 9.1 Node

A custom node class groups the value stored at one position with references to neighboring nodes. The exact fields depend on the structure—for example, `next` for a singly linked list and `left`/`right` for a binary tree. Algorithms usually pass or return node references rather than copying whole structures.

```js
class ListNode {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}
```

---

## 9.2 Singly Linked List

A singly linked list node stores a value plus one `next` reference. Access to the `i`th element requires traversal from the head, but insertion/removal near a known node only changes a small number of links. Keep ownership of the head (and optional tail) explicit.

```js
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }

  append(value) {
    const node = new ListNode(value);

    if (!this.head) {
      this.head = node;
      this.tail = node;
    } else {
      this.tail.next = node;
      this.tail = node;
    }

    this.length++;
  }

  prepend(value) {
    const node = new ListNode(value);

    node.next = this.head;
    this.head = node;

    if (!this.tail) {
      this.tail = node;
    }

    this.length++;
  }
}
```

---

## 9.3 Complexity

| Operation | Singly Linked List |
|---|---:|
| Access by index | O(n) |
| Search | O(n) |
| Insert at head | O(1) |
| Delete head | O(1) |
| Insert at tail with tail pointer | O(1) |

---

## 9.4 Reverse Linked List

Reversing a singly linked list rewires each node's `next` reference. Keep three pieces of state: the previous node, the current node, and the original next node so the remainder of the list is not lost before reassignment. The iterative algorithm runs in `O(n)` time and `O(1)` extra space.

```js
function reverseList(head) {
  let previous = null;
  let current = head;

  while (current) {
    const nextNode = current.next;

    current.next = previous;
    previous = current;
    current = nextNode;
  }

  return previous;
}
```

Important interview pattern.

---

## 9.5 Find Middle — Fast and Slow Pointer

Move one pointer one node at a time and another two nodes at a time. When the fast pointer reaches the end, the slow pointer is at the middle. Define which middle should be returned for even-length lists; the common loop condition determines whether you get the first or second middle.

```js
function middleNode(head) {
  let slow = head;
  let fast = head;

  while (fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;
  }

  return slow;
}
```

---

## 9.6 Detect Cycle — Floyd's Algorithm

An algorithm is a finite, unambiguous procedure that converts an input into the required output. A useful explanation of an algorithm should state its preconditions, the main invariant or idea that keeps it correct, when it stops, and its time and space complexity.

```js
function hasCycle(head) {
  let slow = head;
  let fast = head;

  while (fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;

    if (slow === fast) {
      return true;
    }
  }

  return false;
}
```

Time: O(n)  
Space: O(1)

---

## 9.7 Merge Two Sorted Lists

Merging two sorted linked lists repeatedly chooses the smaller current head and appends that node to the result chain. A dummy/sentinel head can simplify the first-insertion case; return the node after the dummy. Every input node is linked once, so time is `O(n + m)`.

```js
function mergeTwoLists(a, b) {
  const dummy = new ListNode(0);
  let current = dummy;

  while (a && b) {
    if (a.value <= b.value) {
      current.next = a;
      a = a.next;
    } else {
      current.next = b;
      b = b.next;
    }

    current = current.next;
  }

  current.next = a ?? b;

  return dummy.next;
}
```

---

# 10. Stacks

A stack follows:

> **Last In, First Out (LIFO)**

Examples:

- browser back history,
- undo functionality,
- function call stack,
- expression parsing,
- DFS,
- bracket validation.

JavaScript arrays can implement stacks efficiently at the end:

```js
const stack = [];

stack.push(10);
stack.push(20);

console.log(stack.pop());
```

---

## 10.1 Valid Parentheses

Balanced-bracket checking uses a stack of opening brackets. Each closing bracket must match the most recent unmatched opening bracket, so a mismatch or an empty stack fails immediately; after the scan, the stack must also be empty. The algorithm is `O(n)` time and `O(n)` worst-case space.

```js
function isValidParentheses(s) {
  const stack = [];

  const pairs = new Map([
    [")", "("],
    ["]", "["],
    ["}", "{"]
  ]);

  for (const ch of s) {
    if (pairs.has(ch)) {
      if (stack.pop() !== pairs.get(ch)) {
        return false;
      }
    } else {
      stack.push(ch);
    }
  }

  return stack.length === 0;
}
```

---

## 10.2 Min Stack

A stack follows **Last In, First Out (LIFO)** order: the most recently pushed item is the first one removed. The core operations are push, pop, peek/top, and an emptiness check. Stacks are useful when later work depends on the most recent unfinished item, such as expression evaluation, undo, DFS, bracket matching, monotonic-stack problems, and simulated recursion.

Support retrieving minimum in O(1).

```js
class MinStack {
  constructor() {
    this.stack = [];
    this.minStack = [];
  }

  push(value) {
    this.stack.push(value);

    const currentMin =
      this.minStack.length === 0
        ? value
        : Math.min(value, this.minStack[this.minStack.length - 1]);

    this.minStack.push(currentMin);
  }

  pop() {
    this.minStack.pop();
    return this.stack.pop();
  }

  top() {
    return this.stack[this.stack.length - 1];
  }

  getMin() {
    return this.minStack[this.minStack.length - 1];
  }
}
```

---

# 11. Queues and Deques

A queue follows:

> **First In, First Out (FIFO)**

Examples:

- print jobs,
- support tickets,
- BFS,
- task scheduling,
- message processing.

---

## 11.1 Avoid Repeated `shift()` for Large Queues

The code below is a concrete example of **11.1 Avoid Repeated `shift()` for Large Queues**. Read it by identifying the input/state first, then trace each mutation or decision until the produced value/output. When reusing the pattern, preserve its required preconditions and include the cost of nested library operations in the complexity analysis.

Although convenient:

```js
queue.shift();
```

removing the first element may require reindexing.

A better pattern:

```js
const queue = [];
let head = 0;

queue.push("A");
queue.push("B");

const item = queue[head++];
```

---

## 11.2 Queue Class

A queue follows **First In, First Out (FIFO)** order: the earliest enqueued item is processed first. The key operations are enqueue, dequeue, front/peek, and emptiness checking. Queues are a natural fit for breadth-first search, scheduling, buffering, and any workflow that must preserve arrival order.

```js
class Queue {
  constructor() {
    this.items = [];
    this.head = 0;
  }

  enqueue(value) {
    this.items.push(value);
  }

  dequeue() {
    if (this.isEmpty()) return undefined;

    const value = this.items[this.head];
    this.head++;

    return value;
  }

  front() {
    return this.items[this.head];
  }

  isEmpty() {
    return this.head >= this.items.length;
  }

  size() {
    return this.items.length - this.head;
  }
}
```

---

## 11.3 Deque

A **deque** supports insertion/removal at both ends.

Useful in:

- sliding-window maximum,
- 0-1 BFS,
- monotonic queue,
- palindrome-like processing.

For performance-sensitive JavaScript, consider implementing a deque using an indexed object or circular buffer instead of frequent `shift()` / `unshift()`.

---

# 12. Recursion

Recursion solves a problem by calling the same routine on a smaller or simpler state. Every recursive solution needs a **base case** that stops further calls and a **progress rule** that moves toward that base case. Also account for call-stack space: even an algorithm with little explicit memory usage may use `O(depth)` stack space.

Recursion occurs when a function calls itself.

Every recursive solution needs:

1. a base case,
2. progress toward that base case.

---

## 12.1 Factorial

Factorial is defined for non-negative integers by `n! = n × (n-1) × ... × 1`, with `0! = 1`. A recursive implementation mirrors that definition, but an iterative version avoids recursive call-stack growth. Factorial values grow extremely quickly, so ordinary fixed-width integer types overflow at relatively small `n` values.

```js
function factorial(n) {
  if (n <= 1) return 1;

  return n * factorial(n - 1);
}
```

---

## 12.2 Recursive Sum

A recursive sum processes one element and delegates the remainder to a smaller state until a base case such as an empty suffix/index is reached. It is `O(n)` time but also uses `O(n)` call-stack space, so an iterative loop is usually preferable when recursion adds no structural clarity.

```js
function sum(nums, index = 0) {
  if (index === nums.length) {
    return 0;
  }

  return nums[index] + sum(nums, index + 1);
}
```

---

## 12.3 Recursion Tree

Recursion solves a problem by calling the same routine on a smaller or simpler state. Every recursive solution needs a **base case** that stops further calls and a **progress rule** that moves toward that base case. Also account for call-stack space: even an algorithm with little explicit memory usage may use `O(depth)` stack space.

Naive Fibonacci:

```js
function fib(n) {
  if (n <= 1) return n;

  return fib(n - 1) + fib(n - 2);
}
```

This repeats subproblems.

Complexity is exponential.

Memoization fixes it:

```js
function fib(n, memo = new Map()) {
  if (n <= 1) return n;

  if (memo.has(n)) {
    return memo.get(n);
  }

  const result = fib(n - 1, memo) + fib(n - 2, memo);
  memo.set(n, result);

  return result;
}
```

---

## 12.4 Recursion vs Iteration

Use recursion naturally for:

- trees,
- DFS,
- backtracking,
- divide-and-conquer,
- memoized DP.

Use iteration when:

- stack depth may become very large,
- recursion overhead matters,
- the iterative solution is clearer.

JavaScript environments may throw a stack overflow for deep recursion.

---

# 13. Searching Algorithms

Searching asks whether, where, or under what condition a target can be found. Start with linear search as the no-precondition baseline, then use binary search when ordering or monotonicity lets you safely discard large parts of the search space.

## 13.1 Linear Search

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

```js
function linearSearch(nums, target) {
  for (let i = 0; i < nums.length; i++) {
    if (nums[i] === target) {
      return i;
    }
  }

  return -1;
}
```

Time: O(n)

---

## 13.2 Binary Search

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

Requirement:

> Search space must have monotonic/sorted structure.

```js
function binarySearch(nums, target) {
  let left = 0;
  let right = nums.length - 1;

  while (left <= right) {
    const mid = left + Math.floor((right - left) / 2);

    if (nums[mid] === target) {
      return mid;
    }

    if (nums[mid] < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }

  return -1;
}
```

Time: O(log n)

---

## 13.3 Lower Bound

A lower bound returns the first position whose value is **not less than** the target (equivalently, the insertion position before existing equal values). The binary-search invariant must preserve all possible answers, including the position immediately after the final element when every value is smaller.

Find the first index where:

```txt
nums[index] >= target
```

```js
function lowerBound(nums, target) {
  let left = 0;
  let right = nums.length;

  while (left < right) {
    const mid = left + Math.floor((right - left) / 2);

    if (nums[mid] < target) {
      left = mid + 1;
    } else {
      right = mid;
    }
  }

  return left;
}
```

---

## 13.4 Upper Bound

An upper bound returns the first position whose value is **greater than** the target, which is the insertion position after all existing equal values. It differs from lower bound only in the comparison that decides which half can still contain the answer.

First index where:

```txt
nums[index] > target
```

```js
function upperBound(nums, target) {
  let left = 0;
  let right = nums.length;

  while (left < right) {
    const mid = left + Math.floor((right - left) / 2);

    if (nums[mid] <= target) {
      left = mid + 1;
    } else {
      right = mid;
    }
  }

  return left;
}
```

---

## 13.5 Binary Search on Answer

Sometimes you are not searching an array.

You are searching the smallest/largest answer satisfying a condition.

Pattern:

```js
function binarySearchAnswer(low, high, canDo) {
  let answer = high;

  while (low <= high) {
    const mid = low + Math.floor((high - low) / 2);

    if (canDo(mid)) {
      answer = mid;
      high = mid - 1;
    } else {
      low = mid + 1;
    }
  }

  return answer;
}
```

Typical problems:

- minimum capacity,
- minimum speed,
- maximum feasible distance,
- minimum days,
- smallest threshold.

---

# 14. Sorting Algorithms

Sorting rearranges values according to an ordering rule so later operations can exploit structure. Learn not only the code but also stability, in-place behavior, best/average/worst complexity, comparator requirements, and when a language's built-in sort is preferable to a manual algorithm.

Sorting often simplifies a difficult problem.

It can enable:

- binary search,
- two pointers,
- greedy choices,
- duplicate handling,
- interval merging.

---

## 14.1 Bubble Sort

Bubble sort repeatedly compares adjacent elements and swaps pairs that are out of order. After each full pass, one extreme value has moved to its final end position. It is easy to learn but `O(n²)` in average/worst cases; with an early-exit flag it can be `O(n)` on already sorted input.

Repeatedly swap adjacent inverted pairs.

```js
function bubbleSort(nums) {
  const arr = [...nums];

  for (let end = arr.length - 1; end > 0; end--) {
    let swapped = false;

    for (let i = 0; i < end; i++) {
      if (arr[i] > arr[i + 1]) {
        [arr[i], arr[i + 1]] = [arr[i + 1], arr[i]];
        swapped = true;
      }
    }

    if (!swapped) break;
  }

  return arr;
}
```

Worst: O(n²)

Mainly useful for learning.

---

## 14.2 Selection Sort

Selection sort repeatedly chooses the smallest (or largest) remaining element and places it into the next final position. It performs `O(n²)` comparisons regardless of initial order and only `O(n)` swaps, so it is mostly educational or useful when writes are unusually expensive. The usual in-place form is not stable.

Select the minimum and place it next.

```js
function selectionSort(nums) {
  const arr = [...nums];

  for (let i = 0; i < arr.length; i++) {
    let minIndex = i;

    for (let j = i + 1; j < arr.length; j++) {
      if (arr[j] < arr[minIndex]) {
        minIndex = j;
      }
    }

    [arr[i], arr[minIndex]] = [arr[minIndex], arr[i]];
  }

  return arr;
}
```

Time: O(n²)

---

## 14.3 Insertion Sort

Insertion sort grows a sorted prefix one element at a time. For each new value, it shifts larger prefix elements to the right until the correct insertion position opens. It is stable with the usual comparison, in-place, `O(n²)` in the average/worst case, and `O(n)` on already or nearly sorted data.

Good conceptual fit for nearly sorted data.

```js
function insertionSort(nums) {
  const arr = [...nums];

  for (let i = 1; i < arr.length; i++) {
    const value = arr[i];
    let j = i - 1;

    while (j >= 0 && arr[j] > value) {
      arr[j + 1] = arr[j];
      j--;
    }

    arr[j + 1] = value;
  }

  return arr;
}
```

Worst: O(n²)

---

## 14.4 Merge Sort

Merge sort divides the sequence into halves, recursively sorts each half, and merges two sorted halves in linear time. Its recurrence leads to `O(n log n)` time in all standard cases; array implementations typically need `O(n)` auxiliary merge storage. Merge sort is stable when equal elements are taken from the left half first.

Divide array in half, recursively sort, merge.

```js
function merge(left, right) {
  const result = [];

  let i = 0;
  let j = 0;

  while (i < left.length && j < right.length) {
    if (left[i] <= right[j]) {
      result.push(left[i++]);
    } else {
      result.push(right[j++]);
    }
  }

  while (i < left.length) result.push(left[i++]);
  while (j < right.length) result.push(right[j++]);

  return result;
}

function mergeSort(nums) {
  if (nums.length <= 1) return nums;

  const mid = Math.floor(nums.length / 2);

  const left = mergeSort(nums.slice(0, mid));
  const right = mergeSort(nums.slice(mid));

  return merge(left, right);
}
```

Time: O(n log n)  
Extra space: O(n)

---

## 14.5 Quick Sort

Quick sort partitions elements around a pivot so smaller and larger values move to opposite sides, then recursively sorts the partitions. Average time is `O(n log n)` but poor pivot choices can produce `O(n²)`. Partition scheme, duplicate handling, and recursion depth are important implementation details.

Choose a pivot and partition values around it.

```js
function quickSort(nums) {
  const arr = [...nums];

  function sort(left, right) {
    if (left >= right) return;

    const pivot = arr[right];
    let p = left;

    for (let i = left; i < right; i++) {
      if (arr[i] <= pivot) {
        [arr[i], arr[p]] = [arr[p], arr[i]];
        p++;
      }
    }

    [arr[p], arr[right]] = [arr[right], arr[p]];

    sort(left, p - 1);
    sort(p + 1, right);
  }

  sort(0, arr.length - 1);

  return arr;
}
```

Average: O(n log n)  
Worst: O(n²)

Randomized pivoting helps reduce bad cases.

---

## 14.6 Counting Sort

Useful when values are integers in a manageable range.

```js
function countingSort(nums) {
  if (nums.length === 0) return [];

  const min = Math.min(...nums);
  const max = Math.max(...nums);

  const count = new Array(max - min + 1).fill(0);

  for (const num of nums) {
    count[num - min]++;
  }

  const result = [];

  for (let i = 0; i < count.length; i++) {
    while (count[i] > 0) {
      result.push(i + min);
      count[i]--;
    }
  }

  return result;
}
```

Time: O(n + k), where `k` is value range.

Do not use when the numeric range is enormous.

---

## 14.7 Sorting Comparison

| Algorithm | Best | Average | Worst | Extra Space |
|---|---:|---:|---:|---:|
| Bubble | O(n) optimized | O(n²) | O(n²) | O(1) |
| Selection | O(n²) | O(n²) | O(n²) | O(1) |
| Insertion | O(n) | O(n²) | O(n²) | O(1) |
| Merge | O(n log n) | O(n log n) | O(n log n) | O(n) |
| Quick | O(n log n) | O(n log n) | O(n²) | recursion |
| Counting | O(n+k) | O(n+k) | O(n+k) | O(k) |

---

# 15. Two Pointers

Two pointers maintain two indexes or references whose movement eliminates unnecessary repeated work. Common forms are opposite-end pointers on sorted data and same-direction read/write pointers for in-place filtering. The technique is most valuable when pointer movement can be justified by an invariant, such as sorted order or a maintained valid region.

Two pointers use two indices that move according to a rule.

Common situations:

- sorted arrays,
- palindrome checking,
- partitioning,
- pair sum,
- removing duplicates,
- linked lists.

---

## 15.1 Pair Sum in Sorted Array

With sorted input, place one pointer at each end. If the sum is too small, moving the left pointer right is the only move that can increase it; if the sum is too large, move the right pointer left. This invariant gives `O(n)` time and `O(1)` extra space after sorting is already available.

```js
function hasPairSum(nums, target) {
  let left = 0;
  let right = nums.length - 1;

  while (left < right) {
    const sum = nums[left] + nums[right];

    if (sum === target) {
      return true;
    }

    if (sum < target) {
      left++;
    } else {
      right--;
    }
  }

  return false;
}
```

Time: O(n)

---

## 15.2 Move Zeroes

Use a write pointer for the next non-zero position while a read pointer scans the array. Copy/swap non-zero values forward in original order, then fill or leave zeros in the remaining suffix depending on the implementation. This yields `O(n)` time and `O(1)` extra space.

```js
function moveZeroes(nums) {
  let insert = 0;

  for (let i = 0; i < nums.length; i++) {
    if (nums[i] !== 0) {
      [nums[insert], nums[i]] = [nums[i], nums[insert]];
      insert++;
    }
  }

  return nums;
}
```

---

## 15.3 Three Sum

Typical strategy:

1. sort,
2. fix one number,
3. use two pointers for the remaining pair.

```js
function threeSum(nums) {
  nums.sort((a, b) => a - b);

  const result = [];

  for (let i = 0; i < nums.length - 2; i++) {
    if (i > 0 && nums[i] === nums[i - 1]) continue;

    let left = i + 1;
    let right = nums.length - 1;

    while (left < right) {
      const sum = nums[i] + nums[left] + nums[right];

      if (sum === 0) {
        result.push([nums[i], nums[left], nums[right]]);

        while (left < right && nums[left] === nums[left + 1]) left++;
        while (left < right && nums[right] === nums[right - 1]) right--;

        left++;
        right--;
      } else if (sum < 0) {
        left++;
      } else {
        right--;
      }
    }
  }

  return result;
}
```

Time: O(n²)

---

# 16. Sliding Window

A sliding window tracks a contiguous range while updating only the information that changes when the range expands or shrinks. Fixed-size windows are used when the length is known; variable-size windows adjust a boundary until a validity condition is restored. The usual goal is to replace repeated recomputation of every subarray or substring with a single linear pass.

Sliding window is used for contiguous ranges.

Clues:

- subarray,
- substring,
- consecutive,
- longest/shortest range,
- at most / at least constraints.

---

## 16.1 Fixed-Size Window

A fixed-size sliding window maintains an aggregate for exactly `k` consecutive elements. Build the first window, then for each shift subtract/remove the outgoing contribution and add the incoming one. This turns many `O(nk)` repeated-window calculations into `O(n)`.

Maximum sum of `k` consecutive values.

```js
function maxWindowSum(nums, k) {
  if (k > nums.length) return null;

  let windowSum = 0;

  for (let i = 0; i < k; i++) {
    windowSum += nums[i];
  }

  let best = windowSum;

  for (let right = k; right < nums.length; right++) {
    windowSum += nums[right];
    windowSum -= nums[right - k];

    best = Math.max(best, windowSum);
  }

  return best;
}
```

Time: O(n)

---

## 16.2 Variable-Size Window

A variable-size sliding window expands one boundary and shrinks the other whenever the validity constraint is violated. This is linear when each boundary moves forward at most `n` times and when window state can be updated incrementally. The validity condition must be monotonic enough that shrinking can restore it.

Longest substring without repeating characters:

```js
function lengthOfLongestSubstring(s) {
  const lastSeen = new Map();

  let left = 0;
  let best = 0;

  for (let right = 0; right < s.length; right++) {
    const ch = s[right];

    if (lastSeen.has(ch) && lastSeen.get(ch) >= left) {
      left = lastSeen.get(ch) + 1;
    }

    lastSeen.set(ch, right);

    best = Math.max(best, right - left + 1);
  }

  return best;
}
```

---

## 16.3 Minimum Length Subarray with Sum ≥ Target

Assuming positive numbers:

```js
function minSubArrayLen(target, nums) {
  let left = 0;
  let sum = 0;
  let best = Infinity;

  for (let right = 0; right < nums.length; right++) {
    sum += nums[right];

    while (sum >= target) {
      best = Math.min(best, right - left + 1);
      sum -= nums[left++];
    }
  }

  return best === Infinity ? 0 : best;
}
```

Sliding window works here because all values are positive, making the sum behave monotonically as the window expands/shrinks.

---

# 17. Prefix Sum and Difference Arrays

Prefix sums and difference arrays are complementary preprocessing techniques. Prefix sums make repeated range queries cheap; difference arrays make many range updates cheap before one final reconstruction. Their correctness depends on a clear indexing convention and careful boundary handling.

## 17.1 Prefix Sum

A prefix sum precomputes cumulative totals so that later range sums can be answered by subtraction. With the common convention `prefix[i] = sum of elements before i`, the sum of the half-open range `[left, right)` is `prefix[right] - prefix[left]`. Building the prefix array costs `O(n)` time and each range query then costs `O(1)`.

Given:

```txt
[2, 4, 1, 5]
```

Prefix sums:

```txt
[0, 2, 6, 7, 12]
```

Define:

```txt
prefix[i + 1] = prefix[i] + nums[i]
```

Then range sum `[left, right]` is:

```txt
prefix[right + 1] - prefix[left]
```

Implementation:

```js
function buildPrefix(nums) {
  const prefix = new Array(nums.length + 1).fill(0);

  for (let i = 0; i < nums.length; i++) {
    prefix[i + 1] = prefix[i] + nums[i];
  }

  return prefix;
}

function rangeSum(prefix, left, right) {
  return prefix[right + 1] - prefix[left];
}
```

Build: O(n)  
Each query: O(1)

---

## 17.2 Prefix Sum + Hash Map

A prefix sum precomputes cumulative totals so that later range sums can be answered by subtraction. With the common convention `prefix[i] = sum of elements before i`, the sum of the half-open range `[left, right)` is `prefix[right] - prefix[left]`. Building the prefix array costs `O(n)` time and each range query then costs `O(1)`.

Count subarrays with sum `k`.

```js
function subarraySum(nums, k) {
  const count = new Map();
  count.set(0, 1);

  let prefix = 0;
  let answer = 0;

  for (const num of nums) {
    prefix += num;

    answer += count.get(prefix - k) ?? 0;

    count.set(prefix, (count.get(prefix) ?? 0) + 1);
  }

  return answer;
}
```

Important pattern.

---

## 17.3 Difference Array

A difference array represents the *changes* between positions so that many range updates can be recorded cheaply. A range addition marks where an effect starts and where it stops; one final prefix accumulation reconstructs the resulting values. It is useful when updates are numerous but point-by-point results are only needed after all updates are known.

Efficiently apply many range increments.

To add `value` to every position `[left, right]`:

```txt
diff[left] += value
diff[right + 1] -= value
```

Then reconstruct using prefix sum.

```js
function applyRangeUpdates(n, updates) {
  const diff = new Array(n + 1).fill(0);

  for (const [left, right, value] of updates) {
    diff[left] += value;

    if (right + 1 < n) {
      diff[right + 1] -= value;
    }
  }

  const result = new Array(n).fill(0);
  let running = 0;

  for (let i = 0; i < n; i++) {
    running += diff[i];
    result[i] = running;
  }

  return result;
}
```

---

# 18. Matrices and Grids

Matrices and grids are indexed 2D structures, but many grid problems are graphs in disguise: each cell is a vertex and allowed moves define edges. Start by clarifying row/column bounds and movement rules, then choose direct iteration, prefix techniques, BFS/DFS, or DP based on the required operation.

A matrix is commonly represented as:

```js
const grid = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];
```

---

## 18.1 Traversal

Traversal means visiting each relevant element/node in a defined order. The important state is the current position and the rule for advancing to the next one. A full traversal is usually `O(n)` for a linear structure, while trees/graphs additionally require a stack/queue or recursion and, for cyclic graphs, visited tracking.

```js
for (let r = 0; r < grid.length; r++) {
  for (let c = 0; c < grid[0].length; c++) {
    console.log(grid[r][c]);
  }
}
```

---

## 18.2 Direction Arrays

An array-like structure stores elements in an indexed sequence. Its main advantage is direct access by position; the main trade-off is that inserting or deleting near the front or middle usually requires shifting elements. In DSA problems, arrays are also the base structure behind two pointers, sliding windows, prefix sums, binary search, heaps, and many dynamic-programming tables.

Very useful:

```js
const directions = [
  [1, 0],
  [-1, 0],
  [0, 1],
  [0, -1]
];
```

Then:

```js
for (const [dr, dc] of directions) {
  const nr = r + dr;
  const nc = c + dc;
}
```

---

## 18.3 Flood Fill

Flood fill explores all grid cells connected to a start cell under a movement rule and matching condition. BFS or DFS both work; mark a cell visited (or recolor it) when it is discovered to prevent repeated work. Runtime is `O(rows × cols)` in the worst case.

```js
function floodFill(image, sr, sc, color) {
  const original = image[sr][sc];

  if (original === color) return image;

  const rows = image.length;
  const cols = image[0].length;

  function dfs(r, c) {
    if (
      r < 0 ||
      r >= rows ||
      c < 0 ||
      c >= cols ||
      image[r][c] !== original
    ) {
      return;
    }

    image[r][c] = color;

    dfs(r + 1, c);
    dfs(r - 1, c);
    dfs(r, c + 1);
    dfs(r, c - 1);
  }

  dfs(sr, sc);

  return image;
}
```

---

## 18.4 Island Problems

Grid-island problems are graph problems in disguise.

Common actions:

- BFS/DFS connected cells,
- mark visited,
- count components,
- calculate area/perimeter,
- detect boundaries.

---

# 19. Backtracking

Backtracking explores a decision tree by making a choice, recursively exploring what follows, and then undoing that choice before trying the next option. It is appropriate when the task asks for all valid combinations, permutations, placements, paths, or constraint-satisfying configurations. Pruning impossible branches early is often the difference between a practical and an impractical solution.

Backtracking explores possibilities and undoes choices.

General pattern:

```js
function backtrack(state, choices) {
  if (isSolution(state)) {
    saveSolution(state);
    return;
  }

  for (const choice of choices) {
    if (!isValid(choice, state)) continue;

    makeChoice(choice, state);
    backtrack(state, choices);
    undoChoice(choice, state);
  }
}
```

---

## 19.1 Generate Subsets

Generating all subsets explores two choices for each element: include it or exclude it. That creates `2^n` possible subsets, so exponential output size is unavoidable. Backtracking should add a **copy** of the current path to the result because the same mutable path is modified during later recursive calls.

```js
function subsets(nums) {
  const result = [];
  const current = [];

  function dfs(index) {
    if (index === nums.length) {
      result.push([...current]);
      return;
    }

    // exclude
    dfs(index + 1);

    // include
    current.push(nums[index]);
    dfs(index + 1);
    current.pop();
  }

  dfs(0);

  return result;
}
```

Time: O(2ⁿ × n) if copying each subset.

---

## 19.2 Permutations

Generating permutations chooses one unused item for each next position, recursively explores the remainder, and then undoes the choice. There are `n!` outputs for distinct items, so factorial work is inherent. With duplicate input values, add a duplicate-skipping rule if unique permutations are required.

```js
function permutations(nums) {
  const result = [];
  const current = [];
  const used = new Array(nums.length).fill(false);

  function dfs() {
    if (current.length === nums.length) {
      result.push([...current]);
      return;
    }

    for (let i = 0; i < nums.length; i++) {
      if (used[i]) continue;

      used[i] = true;
      current.push(nums[i]);

      dfs();

      current.pop();
      used[i] = false;
    }
  }

  dfs();

  return result;
}
```

---

## 19.3 Combination Sum Style

Combination-sum backtracking builds a candidate combination and recurses on the remaining target. Whether the recursive call reuses the current index or advances to the next index determines whether an item may be chosen multiple times. Prune when the remaining target becomes impossible under the problem's assumptions.

```js
function combinationSum(candidates, target) {
  const result = [];
  const current = [];

  function dfs(start, remaining) {
    if (remaining === 0) {
      result.push([...current]);
      return;
    }

    if (remaining < 0) return;

    for (let i = start; i < candidates.length; i++) {
      current.push(candidates[i]);

      dfs(i, remaining - candidates[i]);

      current.pop();
    }
  }

  dfs(0, target);

  return result;
}
```

---

## 19.4 Backtracking Clues

Backtracking explores a decision tree by making a choice, recursively exploring what follows, and then undoing that choice before trying the next option. It is appropriate when the task asks for all valid combinations, permutations, placements, paths, or constraint-satisfying configurations. Pruning impossible branches early is often the difference between a practical and an impractical solution.

Think backtracking for:

- "generate all",
- combinations,
- permutations,
- subsets,
- N-Queens,
- Sudoku,
- word search,
- path enumeration,
- constraint satisfaction.

---

# 20. Trees

A tree is a connected acyclic hierarchical structure with nodes linked by parent/child relationships. Tree algorithms are easiest to understand recursively: define what one subtree call returns, choose a traversal order, and account for tree height because recursion/operation cost can degrade on skewed trees.

A tree is a hierarchical structure.

Important vocabulary:

- root,
- node,
- edge,
- parent,
- child,
- sibling,
- leaf,
- depth,
- height,
- subtree.

---

## 20.1 Binary Tree Node

A binary tree node has at most two children, conventionally `left` and `right`. Unlike a BST, a general binary tree has no ordering rule unless the problem states one; searches therefore usually require traversal rather than directional comparison.

```js
class TreeNode {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
  }
}
```

---

## 20.2 DFS Traversals

Depth-first search explores one branch as far as possible before returning to try another branch. It can be implemented recursively or with an explicit stack and is widely used for connected components, cycle detection, tree processing, path exploration, topological reasoning, and many backtracking-style searches. Track visited state in cyclic graphs to avoid endless revisits.

### Preorder

Preorder traversal visits **node → left subtree → right subtree**. It is useful when the parent must be processed before its children, such as copying a tree, serializing certain tree formats, or producing prefix-style expression order. A complete traversal visits every node once, so time is `O(n)`.

```txt
root -> left -> right
```

```js
function preorder(root, result = []) {
  if (!root) return result;

  result.push(root.value);
  preorder(root.left, result);
  preorder(root.right, result);

  return result;
}
```

### Inorder

Inorder traversal visits **left subtree → node → right subtree**. On a Binary Search Tree with a consistent ordering rule, this produces keys in sorted order. A complete traversal is `O(n)` time and uses `O(h)` call-stack/explicit-stack space for tree height `h`.

```txt
left -> root -> right
```

```js
function inorder(root, result = []) {
  if (!root) return result;

  inorder(root.left, result);
  result.push(root.value);
  inorder(root.right, result);

  return result;
}
```

### Postorder

Postorder traversal visits **left subtree → right subtree → node**. Because children are processed before their parent, it is useful for deleting trees, computing subtree aggregates, and many tree-DP problems. A complete traversal is `O(n)` time and uses `O(h)` traversal stack space.

```txt
left -> right -> root
```

```js
function postorder(root, result = []) {
  if (!root) return result;

  postorder(root.left, result);
  postorder(root.right, result);
  result.push(root.value);

  return result;
}
```

---

## 20.3 Level Order Traversal — BFS

Level-order traversal is BFS on a tree. Use a queue to process nodes in increasing depth; if the output is grouped by levels, capture the queue size at the start of each level so newly enqueued children belong to the next group.

```js
function levelOrder(root) {
  if (!root) return [];

  const result = [];
  const queue = [root];
  let head = 0;

  while (head < queue.length) {
    const levelSize = queue.length - head;
    const level = [];

    for (let i = 0; i < levelSize; i++) {
      const node = queue[head++];

      level.push(node.value);

      if (node.left) queue.push(node.left);
      if (node.right) queue.push(node.right);
    }

    result.push(level);
  }

  return result;
}
```

---

## 20.4 Maximum Depth

Maximum tree depth is the number of nodes (or edges, depending on the chosen convention) on the longest root-to-leaf path. A recursive solution returns `1 + max(leftDepth, rightDepth)` for a non-null node. It visits each node once: `O(n)` time and `O(h)` stack space.

```js
function maxDepth(root) {
  if (!root) return 0;

  return 1 + Math.max(
    maxDepth(root.left),
    maxDepth(root.right)
  );
}
```

---

## 20.5 Invert Binary Tree

Inverting a binary tree swaps the left and right child of every node. DFS or BFS both work and visit each node once: `O(n)` time. Recursive DFS uses `O(h)` stack space; iterative BFS/DFS uses an explicit queue/stack proportional to the frontier.

```js
function invertTree(root) {
  if (!root) return null;

  [root.left, root.right] = [
    invertTree(root.right),
    invertTree(root.left)
  ];

  return root;
}
```

---

## 20.6 Diameter of Binary Tree

A binary tree node has at most two children, conventionally `left` and `right`. Unlike a BST, a general binary tree has no ordering rule unless the problem states one; searches therefore usually require traversal rather than directional comparison.

Diameter is the longest path between any two nodes, measured in edges.

```js
function diameterOfBinaryTree(root) {
  let best = 0;

  function height(node) {
    if (!node) return 0;

    const left = height(node.left);
    const right = height(node.right);

    best = Math.max(best, left + right);

    return 1 + Math.max(left, right);
  }

  height(root);

  return best;
}
```

Important tree-DP idea:

> Return one value upward while updating a global answer.

---

## 20.7 Lowest Common Ancestor in Binary Tree

The lowest common ancestor (LCA) is the deepest node whose subtree contains both targets. A recursive binary-tree solution returns a target when found; if left and right recursive results are both non-null, the current node is the LCA. Clarify whether both target nodes are guaranteed to exist.

```js
function lowestCommonAncestor(root, p, q) {
  if (!root || root === p || root === q) {
    return root;
  }

  const left = lowestCommonAncestor(root.left, p, q);
  const right = lowestCommonAncestor(root.right, p, q);

  if (left && right) {
    return root;
  }

  return left ?? right;
}
```

---

# 21. Binary Search Trees

A Binary Search Tree (BST) maintains an ordering invariant: values in one subtree compare before the node and values in the other compare after it, according to the chosen duplicate policy. Operations depend on tree height, so an unbalanced BST can degrade from `O(log n)` expected/balanced behavior to `O(n)`.

BST property:

For each node:

```txt
left values < node value < right values
```

assuming distinct values.

---

## 21.1 Search

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

```js
function searchBST(root, target) {
  let current = root;

  while (current) {
    if (current.value === target) {
      return current;
    }

    current =
      target < current.value
        ? current.left
        : current.right;
  }

  return null;
}
```

Average when balanced: O(log n)  
Worst when skewed: O(n)

---

## 21.2 Insert

Insertion must preserve the data structure's invariant. For an ordered tree, compare the new key at each node and descend to the appropriate child until an empty position is found; for duplicate keys, follow the policy defined by the problem. Runtime is proportional to the structure's height.

```js
function insertBST(root, value) {
  if (!root) {
    return new TreeNode(value);
  }

  if (value < root.value) {
    root.left = insertBST(root.left, value);
  } else {
    root.right = insertBST(root.right, value);
  }

  return root;
}
```

---

## 21.3 Validate BST

Validating a BST requires checking the **entire allowed range** for each node, not only comparing a node with its immediate children. Pass lower/upper bounds (or use inorder ordering) so descendants cannot violate an ancestor's constraint. Decide how duplicates are handled before choosing strict or non-strict comparisons.

Do not only compare a node with its immediate children.

Use allowed ranges:

```js
function isValidBST(root) {
  function validate(node, min, max) {
    if (!node) return true;

    if (node.value <= min || node.value >= max) {
      return false;
    }

    return (
      validate(node.left, min, node.value) &&
      validate(node.right, node.value, max)
    );
  }

  return validate(root, -Infinity, Infinity);
}
```

---

## 21.4 Inorder Property

Inorder traversal visits **left subtree → node → right subtree**. On a Binary Search Tree with a consistent ordering rule, this produces keys in sorted order. A complete traversal is `O(n)` time and uses `O(h)` call-stack/explicit-stack space for tree height `h`.

Inorder traversal of a valid BST produces sorted values.

This fact powers many BST problems.

---

# 22. Heaps and Priority Queues

A heap is a tree-based structure used to quickly access the smallest or largest element.

### Min Heap

A heap is a partially ordered tree structure commonly used to implement a priority queue. A min-heap exposes the smallest item; a max-heap exposes the largest. Insert and removal of the root are typically `O(log n)`, while reading the root is `O(1)`, making heaps ideal for top-k, scheduling, streaming minima/maxima, and graph algorithms such as Dijkstra or Prim.

Parent ≤ children.

### Max Heap

Parent ≥ children.

Common use cases:

- top K elements,
- scheduling,
- Dijkstra,
- running median,
- merge K sorted lists,
- task prioritization.

JavaScript historically has not had a universally available built-in priority queue across coding platforms, so it is valuable to know how to implement one.

---

## 22.1 Min Heap Implementation

This implementation turns the surrounding concept into concrete state and operations. Identify what each field stores, which method mutates that state, and what invariant must remain true after every operation; those details matter more than memorizing the exact syntax.

```js
class MinHeap {
  constructor(compare = (a, b) => a - b) {
    this.heap = [];
    this.compare = compare;
  }

  size() {
    return this.heap.length;
  }

  peek() {
    return this.heap[0];
  }

  push(value) {
    this.heap.push(value);
    this.#bubbleUp(this.heap.length - 1);
  }

  pop() {
    if (this.heap.length === 0) return undefined;
    if (this.heap.length === 1) return this.heap.pop();

    const top = this.heap[0];
    this.heap[0] = this.heap.pop();

    this.#bubbleDown(0);

    return top;
  }

  #bubbleUp(index) {
    while (index > 0) {
      const parent = Math.floor((index - 1) / 2);

      if (this.compare(this.heap[index], this.heap[parent]) >= 0) {
        break;
      }

      [this.heap[index], this.heap[parent]] =
        [this.heap[parent], this.heap[index]];

      index = parent;
    }
  }

  #bubbleDown(index) {
    const n = this.heap.length;

    while (true) {
      let best = index;
      const left = 2 * index + 1;
      const right = 2 * index + 2;

      if (
        left < n &&
        this.compare(this.heap[left], this.heap[best]) < 0
      ) {
        best = left;
      }

      if (
        right < n &&
        this.compare(this.heap[right], this.heap[best]) < 0
      ) {
        best = right;
      }

      if (best === index) break;

      [this.heap[index], this.heap[best]] =
        [this.heap[best], this.heap[index]];

      index = best;
    }
  }
}
```

---

## 22.2 Heap Complexity

A heap is a partially ordered tree structure commonly used to implement a priority queue. A min-heap exposes the smallest item; a max-heap exposes the largest. Insert and removal of the root are typically `O(log n)`, while reading the root is `O(1)`, making heaps ideal for top-k, scheduling, streaming minima/maxima, and graph algorithms such as Dijkstra or Prim.

| Operation | Complexity |
|---|---:|
| Peek min/max | O(1) |
| Insert | O(log n) |
| Remove min/max | O(log n) |
| Build heap | O(n) with bottom-up heapify |

---

## 22.3 K Largest Elements

A min-heap of size `k` can maintain the `k` largest values seen so far. Push candidates and remove the smallest whenever the heap exceeds `k`; at the end, the heap contains the desired top `k`. This uses `O(n log k)` time and `O(k)` extra space.

Keep a min heap of size `k`.

```js
function kLargest(nums, k) {
  const heap = new MinHeap();

  for (const num of nums) {
    heap.push(num);

    if (heap.size() > k) {
      heap.pop();
    }
  }

  const result = [];

  while (heap.size() > 0) {
    result.push(heap.pop());
  }

  return result.reverse();
}
```

Time: O(n log k)

---

# 23. Tries

A Trie stores strings by character prefixes.

Useful for:

- autocomplete,
- prefix search,
- dictionary lookup,
- spell-check-like systems,
- word search.

---

## 23.1 Trie Node

A trie stores keys by shared prefixes. Each step consumes one symbol, so lookup time depends mainly on key length rather than on the number of stored keys. Tries are useful for autocomplete, prefix counting, dictionary search, and word-grid problems, but they can use substantially more memory than a hash-based set or map.

```js
class TrieNode {
  constructor() {
    this.children = new Map();
    this.isEnd = false;
  }
}
```

---

## 23.2 Trie

A trie stores keys by shared prefixes. Each step consumes one symbol, so lookup time depends mainly on key length rather than on the number of stored keys. Tries are useful for autocomplete, prefix counting, dictionary search, and word-grid problems, but they can use substantially more memory than a hash-based set or map.

```js
class Trie {
  constructor() {
    this.root = new TrieNode();
  }

  insert(word) {
    let node = this.root;

    for (const ch of word) {
      if (!node.children.has(ch)) {
        node.children.set(ch, new TrieNode());
      }

      node = node.children.get(ch);
    }

    node.isEnd = true;
  }

  search(word) {
    const node = this.#findNode(word);
    return node !== null && node.isEnd;
  }

  startsWith(prefix) {
    return this.#findNode(prefix) !== null;
  }

  #findNode(text) {
    let node = this.root;

    for (const ch of text) {
      if (!node.children.has(ch)) {
        return null;
      }

      node = node.children.get(ch);
    }

    return node;
  }
}
```

Time for word length `L`: O(L)

---

# 24. Graphs

A graph contains:

- vertices/nodes,
- edges/connections.

Types:

- directed,
- undirected,
- weighted,
- unweighted,
- cyclic,
- acyclic,
- connected,
- disconnected.

Real-world examples:

- social networks,
- roads,
- flight routes,
- dependencies,
- computer networks,
- recommendation relationships.

---

## 24.1 Adjacency List

An adjacency list stores, for each vertex, the vertices (and optionally edge weights) directly connected to it. It uses `O(V + E)` space and is usually preferred for sparse graphs because traversing a vertex touches only its actual outgoing/incident edges. For undirected graphs, each edge is normally stored in both endpoint lists.

```js
const graph = new Map();

function addEdge(a, b) {
  if (!graph.has(a)) graph.set(a, []);
  if (!graph.has(b)) graph.set(b, []);

  graph.get(a).push(b);
  graph.get(b).push(a);
}
```

For sparse graphs, adjacency lists are usually preferred.

---

## 24.2 BFS

Breadth-first search explores a graph or tree level by level using a queue. In an unweighted graph, the first time BFS reaches a vertex is through a path with the minimum number of edges from the start. With adjacency-list representation, a complete traversal is `O(V + E)` when each vertex is processed once.

```js
function bfs(graph, start) {
  const visited = new Set([start]);
  const queue = [start];
  let head = 0;

  const order = [];

  while (head < queue.length) {
    const node = queue[head++];
    order.push(node);

    for (const neighbor of graph.get(node) ?? []) {
      if (!visited.has(neighbor)) {
        visited.add(neighbor);
        queue.push(neighbor);
      }
    }
  }

  return order;
}
```

Use BFS for:

- shortest path in unweighted graph,
- levels,
- minimum number of moves,
- nearest target.

---

## 24.3 DFS

Depth-first search explores one branch as far as possible before returning to try another branch. It can be implemented recursively or with an explicit stack and is widely used for connected components, cycle detection, tree processing, path exploration, topological reasoning, and many backtracking-style searches. Track visited state in cyclic graphs to avoid endless revisits.

Recursive:

```js
function dfs(graph, start, visited = new Set(), order = []) {
  visited.add(start);
  order.push(start);

  for (const neighbor of graph.get(start) ?? []) {
    if (!visited.has(neighbor)) {
      dfs(graph, neighbor, visited, order);
    }
  }

  return order;
}
```

Iterative:

```js
function dfsIterative(graph, start) {
  const visited = new Set();
  const stack = [start];
  const order = [];

  while (stack.length > 0) {
    const node = stack.pop();

    if (visited.has(node)) continue;

    visited.add(node);
    order.push(node);

    for (const neighbor of graph.get(node) ?? []) {
      if (!visited.has(neighbor)) {
        stack.push(neighbor);
      }
    }
  }

  return order;
}
```

---

## 24.4 Connected Components

A connected component is a maximal group of vertices reachable from one another (for the relevant directed/undirected definition). Scan all vertices; whenever an unvisited vertex is found, run BFS/DFS to mark one new component. Across the entire graph, adjacency-list traversal is `O(V + E)`.

```js
function countComponents(n, edges) {
  const graph = Array.from({ length: n }, () => []);

  for (const [a, b] of edges) {
    graph[a].push(b);
    graph[b].push(a);
  }

  const visited = new Array(n).fill(false);
  let components = 0;

  function dfs(node) {
    visited[node] = true;

    for (const next of graph[node]) {
      if (!visited[next]) {
        dfs(next);
      }
    }
  }

  for (let node = 0; node < n; node++) {
    if (!visited[node]) {
      components++;
      dfs(node);
    }
  }

  return components;
}
```

---

## 24.5 Topological Sort

A topological ordering places every prerequisite before the items that depend on it. It exists only for a **directed acyclic graph (DAG)**. Common implementations use Kahn's algorithm with indegrees and a queue, or DFS with postorder; if all vertices cannot be ordered, the dependency graph contains a cycle.

Used for directed acyclic graphs (DAGs).

Examples:

- course prerequisites,
- build dependencies,
- task scheduling.

### Kahn's Algorithm

An algorithm is a finite, unambiguous procedure that converts an input into the required output. A useful explanation of an algorithm should state its preconditions, the main invariant or idea that keeps it correct, when it stops, and its time and space complexity.

```js
function topologicalSort(n, edges) {
  const graph = Array.from({ length: n }, () => []);
  const indegree = new Array(n).fill(0);

  for (const [from, to] of edges) {
    graph[from].push(to);
    indegree[to]++;
  }

  const queue = [];
  let head = 0;

  for (let i = 0; i < n; i++) {
    if (indegree[i] === 0) {
      queue.push(i);
    }
  }

  const order = [];

  while (head < queue.length) {
    const node = queue[head++];
    order.push(node);

    for (const next of graph[node]) {
      indegree[next]--;

      if (indegree[next] === 0) {
        queue.push(next);
      }
    }
  }

  return order.length === n ? order : [];
}
```

If not all nodes are processed, a directed cycle exists.

---

## 24.6 Dijkstra's Algorithm

Dijkstra's algorithm computes single-source shortest paths when edge weights are non-negative. Maintain tentative distances and repeatedly process the smallest-distance candidate from a min-priority queue; ignore stale queue entries whose distance no longer matches the best known value. Typical adjacency-list complexity is `O((V+E) log V)`.

Find shortest paths from a source when edge weights are non-negative.

```js
function dijkstra(n, graph, source) {
  const dist = new Array(n).fill(Infinity);
  dist[source] = 0;

  const pq = new MinHeap((a, b) => a[0] - b[0]);
  pq.push([0, source]);

  while (pq.size() > 0) {
    const [currentDist, node] = pq.pop();

    if (currentDist !== dist[node]) continue;

    for (const [next, weight] of graph[node]) {
      const candidate = currentDist + weight;

      if (candidate < dist[next]) {
        dist[next] = candidate;
        pq.push([candidate, next]);
      }
    }
  }

  return dist;
}
```

Typical complexity with a heap:

```txt
O((V + E) log V)
```

Dijkstra is not valid with negative-weight edges.

---

# 25. Union-Find / Disjoint Set Union

Union-Find, also called Disjoint Set Union (DSU), maintains a collection of non-overlapping groups under two main operations: `find` identifies a representative and `union` merges groups. Path compression plus union by rank/size makes a long sequence of operations effectively near-constant time in practice. It is useful for dynamic connectivity, cycle detection in undirected graphs, Kruskal's MST, and component grouping.

DSU tracks connected groups.

Operations:

- `find(x)` → representative of x's component
- `union(a, b)` → merge components

Useful for:

- connectivity,
- cycle detection,
- Kruskal MST,
- grouping,
- dynamic components.

---

## 25.1 Implementation

This implementation turns the surrounding concept into concrete state and operations. Identify what each field stores, which method mutates that state, and what invariant must remain true after every operation; those details matter more than memorizing the exact syntax.

```js
class DSU {
  constructor(n) {
    this.parent = Array.from({ length: n }, (_, i) => i);
    this.rank = new Array(n).fill(0);
    this.components = n;
  }

  find(x) {
    if (this.parent[x] !== x) {
      this.parent[x] = this.find(this.parent[x]);
    }

    return this.parent[x];
  }

  union(a, b) {
    let rootA = this.find(a);
    let rootB = this.find(b);

    if (rootA === rootB) {
      return false;
    }

    if (this.rank[rootA] < this.rank[rootB]) {
      [rootA, rootB] = [rootB, rootA];
    }

    this.parent[rootB] = rootA;

    if (this.rank[rootA] === this.rank[rootB]) {
      this.rank[rootA]++;
    }

    this.components--;

    return true;
  }
}
```

Path compression + union by rank makes operations extremely close to O(1) amortized.

---

# 26. Greedy Algorithms

A greedy algorithm makes the best local choice at each step.

The hard part is proving that local choices lead to a global optimum.

Common greedy clues:

- choose earliest finishing interval,
- choose largest/smallest feasible item,
- optimize by sorting,
- repeatedly take best available choice.

---

## 26.1 Interval Scheduling

For the classic maximum-number-of-non-overlapping-intervals problem, sorting by finishing time and repeatedly choosing the earliest finishing compatible interval is optimal. The greedy choice leaves as much room as possible for future intervals; sorting dominates at `O(n log n)`.

Select maximum number of non-overlapping intervals.

Strategy:

> Sort by finishing time.

```js
function maxNonOverlapping(intervals) {
  intervals.sort((a, b) => a[1] - b[1]);

  let count = 0;
  let lastEnd = -Infinity;

  for (const [start, end] of intervals) {
    if (start >= lastEnd) {
      count++;
      lastEnd = end;
    }
  }

  return count;
}
```

---

## 26.2 Jump Game

The greedy Jump Game invariant stores the farthest index reachable from any position processed so far. If the scan reaches an index beyond that frontier, the path is impossible; otherwise update the frontier with `i + nums[i]`. The scan is `O(n)` time and `O(1)` extra space.

```js
function canJump(nums) {
  let farthest = 0;

  for (let i = 0; i < nums.length; i++) {
    if (i > farthest) {
      return false;
    }

    farthest = Math.max(farthest, i + nums[i]);
  }

  return true;
}
```

Track the furthest reachable position.

---

## 26.3 Greedy vs DP

Ask:

> Once I make this local choice, can it ever prevent the global optimum?

If yes, greedy may fail.

When choices depend on previous state in complex ways, dynamic programming may be necessary.

---

# 27. Dynamic Programming

Dynamic programming is useful when many candidate solutions reuse the same subproblems and the answer can be composed from smaller states. The core design work is to define the **state**, derive the **transition**, set correct **base cases**, and choose an evaluation order. Memoization computes states on demand; tabulation computes them in an explicit order.

Dynamic Programming (DP) solves problems with:

1. **overlapping subproblems**
2. **optimal substructure**

Two main forms:

- memoization → top-down
- tabulation → bottom-up

---

## 27.1 DP Thinking Framework

For every DP problem, identify:

1. **State** — what does `dp[...]` mean?
2. **Transition** — how do previous states produce current state?
3. **Base case**
4. **Answer location**
5. **Computation order**
6. **Can space be optimized?**

---

## 27.2 Fibonacci — Memoization

Memoized Fibonacci stores the result for each `n` the first time it is computed. Later calls return the cached value instead of expanding the same recursive subtree again, reducing exponential recursion to `O(n)` distinct states and `O(n)` memo/stack space.

```js
function fib(n, memo = new Map()) {
  if (n <= 1) return n;

  if (memo.has(n)) {
    return memo.get(n);
  }

  const value = fib(n - 1, memo) + fib(n - 2, memo);
  memo.set(n, value);

  return value;
}
```

---

## 27.3 Fibonacci — Tabulation

Tabulated Fibonacci builds answers from the base cases upward. Each state uses the previous two values, so a full table costs `O(n)` space but can be reduced to two rolling variables when earlier states are no longer needed. Runtime is `O(n)`.

```js
function fib(n) {
  if (n <= 1) return n;

  const dp = new Array(n + 1).fill(0);

  dp[1] = 1;

  for (let i = 2; i <= n; i++) {
    dp[i] = dp[i - 1] + dp[i - 2];
  }

  return dp[n];
}
```

---

## 27.4 Space Optimization

Space optimization removes DP states that are no longer needed. If `dp[i]` depends only on a fixed number of earlier rows/values, replace the full table with rolling variables or a small rolling array. Do this only after the full state transition is correct, because update order can accidentally overwrite a dependency.

```js
function fib(n) {
  if (n <= 1) return n;

  let prev2 = 0;
  let prev1 = 1;

  for (let i = 2; i <= n; i++) {
    const current = prev1 + prev2;
    prev2 = prev1;
    prev1 = current;
  }

  return prev1;
}
```

---

## 27.5 Climbing Stairs

Climbing Stairs is a simple DP model: if the final move can be one or two steps, the number of ways to reach step `i` is the sum of the ways to reach `i-1` and `i-2`. Define base cases carefully; conventions for `n = 0` depend on whether 'do nothing' counts as one valid way.

State:

```txt
dp[i] = number of ways to reach step i
```

Transition:

```txt
dp[i] = dp[i - 1] + dp[i - 2]
```

---

## 27.6 House Robber

House Robber is a take/skip DP. For each house, compare skipping it (keep the previous best) with taking it (add its value to the best solution that excludes the adjacent previous house). Only the previous two DP values are needed, so the common optimized solution is `O(n)` time and `O(1)` extra space.

At each house:

- rob it + best before previous,
- skip it + previous best.

```js
function rob(nums) {
  let prev2 = 0;
  let prev1 = 0;

  for (const money of nums) {
    const current = Math.max(
      prev1,
      prev2 + money
    );

    prev2 = prev1;
    prev1 = current;
  }

  return prev1;
}
```

---

## 27.7 0/1 Knapsack

Each item can be used at most once.

State idea:

```txt
dp[i][capacity]
```

or optimized:

```txt
dp[capacity]
```

```js
function knapsack(weights, values, capacity) {
  const dp = new Array(capacity + 1).fill(0);

  for (let i = 0; i < weights.length; i++) {
    for (let c = capacity; c >= weights[i]; c--) {
      dp[c] = Math.max(
        dp[c],
        dp[c - weights[i]] + values[i]
      );
    }
  }

  return dp[capacity];
}
```

Important:

> Iterate capacity backward for 0/1 knapsack.

---

## 27.8 Unbounded Knapsack

Unbounded knapsack allows an item to be selected more than once. In one-dimensional tabulation, the loop direction is important: iterating capacities upward allows the current item to contribute repeatedly to later states. This differs from 0/1 knapsack, where downward capacity iteration prevents reusing the same item in one iteration.

Items can be reused.

Typically iterate capacity forward.

This difference is fundamental.

---

## 27.9 Coin Change — Minimum Coins

The minimum-coin problem asks for the fewest coins needed to form each amount. A common DP state stores the best answer for amount `x`; each coin proposes `1 + dp[x - coin]` when that smaller amount is reachable. Use a sentinel larger than any possible answer and distinguish 'unreachable' from a valid zero-coin base case.

```js
function coinChange(coins, amount) {
  const dp = new Array(amount + 1).fill(Infinity);
  dp[0] = 0;

  for (let current = 1; current <= amount; current++) {
    for (const coin of coins) {
      if (coin <= current) {
        dp[current] = Math.min(
          dp[current],
          dp[current - coin] + 1
        );
      }
    }
  }

  return dp[amount] === Infinity ? -1 : dp[amount];
}
```

---

## 27.10 Longest Increasing Subsequence — O(n²)

The Longest Increasing Subsequence (LIS) keeps elements in original order but not necessarily contiguously. A simple DP is `O(n²)`; a tails/binary-search method maintains the smallest possible tail for each subsequence length and runs in `O(n log n)`. The tails array is not necessarily the actual LIS unless predecessor information is also stored.

```js
function lengthOfLIS(nums) {
  const n = nums.length;
  const dp = new Array(n).fill(1);

  let best = 0;

  for (let i = 0; i < n; i++) {
    for (let j = 0; j < i; j++) {
      if (nums[j] < nums[i]) {
        dp[i] = Math.max(dp[i], dp[j] + 1);
      }
    }

    best = Math.max(best, dp[i]);
  }

  return best;
}
```

Advanced LIS can be solved in O(n log n) using binary search.

---

## 27.11 Longest Common Subsequence

The Longest Common Subsequence (LCS) asks for the longest sequence that appears in two inputs in the same relative order, without requiring contiguity. A classic DP state `dp[i][j]` describes prefixes of the two sequences: matching symbols extend the answer; otherwise the transition skips one side. The standard table takes `O(mn)` time.

```js
function longestCommonSubsequence(a, b) {
  const rows = a.length + 1;
  const cols = b.length + 1;

  const dp = Array.from(
    { length: rows },
    () => new Array(cols).fill(0)
  );

  for (let i = 1; i < rows; i++) {
    for (let j = 1; j < cols; j++) {
      if (a[i - 1] === b[j - 1]) {
        dp[i][j] = dp[i - 1][j - 1] + 1;
      } else {
        dp[i][j] = Math.max(
          dp[i - 1][j],
          dp[i][j - 1]
        );
      }
    }
  }

  return dp[a.length][b.length];
}
```

---

## 27.12 Grid DP

Grid DP stores the best/count answer for each cell based on previously solved neighboring cells. The allowed movement determines the transition and valid evaluation order. When movement is only right/down, row-major or column-major tabulation is usually straightforward; if arbitrary cycles are allowed, the problem may be a graph problem rather than simple DP.

Number of unique paths:

```js
function uniquePaths(rows, cols) {
  const dp = new Array(cols).fill(1);

  for (let r = 1; r < rows; r++) {
    for (let c = 1; c < cols; c++) {
      dp[c] += dp[c - 1];
    }
  }

  return dp[cols - 1];
}
```

---

## 27.13 DP Categories

Learn these categories separately:

- 1D DP
- 2D DP
- grid DP
- knapsack
- subsequence DP
- string DP
- interval DP
- tree DP
- digit DP
- bitmask DP
- DAG DP.

---

# 28. Bit Manipulation

Bit manipulation treats an integer as a sequence of binary bits. Operations such as AND (`&`), OR (`|`), XOR (`^`), complement (`~`), and shifts can test or modify individual bits efficiently. Use explicit parentheses around shift expressions when precedence could be unclear, and remember that signed integer width and overflow behavior are language-specific.

JavaScript bitwise operators work on 32-bit signed integers.

Operators:

```txt
&   AND
|   OR
^   XOR
~   NOT
<<  left shift
>>  signed right shift
>>> unsigned right shift
```

---

## 28.1 Check a Bit

To test bit `k`, create a mask `1 << k` and AND it with the number. A non-zero result means that bit is set. State whether bit positions are zero-based and ensure `k` is within the integer width used by the language.

```js
function isBitSet(num, bit) {
  return (num & (1 << bit)) !== 0;
}
```

---

## 28.2 Set a Bit

To set bit `k`, OR the number with the mask `1 << k`. OR leaves all existing `1` bits unchanged and forces the selected bit to `1`. The operation modifies the numeric value but does not affect other bit positions.

```js
num |= 1 << bit;
```

---

## 28.3 Clear a Bit

To clear bit `k`, invert the one-bit mask and AND it with the number. The inverted mask has `0` at bit `k` and `1` elsewhere, so only the selected bit is forced to zero. Signed-width/complement behavior follows the language's integer representation.

```js
num &= ~(1 << bit);
```

---

## 28.4 Toggle a Bit

To toggle bit `k`, XOR the number with `1 << k`. XOR with `1` flips a bit and XOR with `0` preserves it, so all other bit positions remain unchanged.

```js
num ^= 1 << bit;
```

---

## 28.5 Odd or Even

The least significant binary bit tells parity: it is `1` for odd integers and `0` for even integers. Testing `n & 1` is a constant-time alternative to `n % 2`, although `% 2` is often clearer when bit operations are not otherwise relevant.

```js
function isOdd(n) {
  return (n & 1) === 1;
}
```

---

## 28.6 XOR Properties

XOR has three useful algebraic properties for DSA: `x ^ x = 0`, `x ^ 0 = x`, and order/grouping can be rearranged because XOR is associative and commutative. These properties enable cancellation tricks, parity/state toggling, and some prefix-XOR problems.

```txt
a ^ a = 0
a ^ 0 = a
XOR is associative and commutative
```

Find single number where every other value appears twice:

```js
function singleNumber(nums) {
  let result = 0;

  for (const num of nums) {
    result ^= num;
  }

  return result;
}
```

---

## 28.7 Subset Bitmask

For `n` small enough, every subset can be represented by a bitmask.

```js
function allSubsets(nums) {
  const result = [];
  const total = 1 << nums.length;

  for (let mask = 0; mask < total; mask++) {
    const subset = [];

    for (let i = 0; i < nums.length; i++) {
      if (mask & (1 << i)) {
        subset.push(nums[i]);
      }
    }

    result.push(subset);
  }

  return result;
}
```

Because JavaScript bitwise operators are 32-bit, this style is limited for large `n`; use `BigInt`-based bit operations or a different representation when necessary.

---

# 29. Mathematics for DSA

A small set of mathematical tools appears repeatedly in DSA: modular arithmetic, divisibility, GCD/LCM, primes, logarithms, combinatorics, and exponentiation. The purpose is practical—these tools simplify constraints, prevent overflow, or reduce repeated computation in algorithms.

## 29.1 GCD — Euclidean Algorithm

An algorithm is a finite, unambiguous procedure that converts an input into the required output. A useful explanation of an algorithm should state its preconditions, the main invariant or idea that keeps it correct, when it stops, and its time and space complexity.

```js
function gcd(a, b) {
  while (b !== 0) {
    [a, b] = [b, a % b];
  }

  return Math.abs(a);
}
```

---

## 29.2 LCM

The least common multiple (LCM) of two non-zero integers can be derived from the GCD: `lcm(a, b) = |a / gcd(a, b) × b|`. Dividing before multiplying reduces overflow risk in fixed-width languages. Define how your implementation should behave when either input is zero; a common convention returns zero.

```js
function lcm(a, b) {
  return Math.abs((a / gcd(a, b)) * b);
}
```

Divide before multiply when possible to reduce overflow risk.

---

## 29.3 Prime Check

The example implements **29.3 Prime Check** with `isPrime(...)`. Its parameters are `n`. Trace how those inputs change or are read, then inspect the `return` statement (or observable mutation/output) to identify the result. Also account for the cost of any loop, recursion, container operation, or nested call when deriving complexity.

```js
function isPrime(n) {
  if (n < 2) return false;

  for (let d = 2; d * d <= n; d++) {
    if (n % d === 0) {
      return false;
    }
  }

  return true;
}
```

Time: O(√n)

---

## 29.4 Sieve of Eratosthenes

The Sieve of Eratosthenes finds all primes up to a limit by marking multiples of each discovered prime as composite. Starting the marking at `p × p` is enough because smaller multiples already have a smaller prime factor. The standard implementation runs in `O(n log log n)` time and uses `O(n)` marking space.

Find primes up to `n`.

```js
function sieve(n) {
  const isPrime = new Array(n + 1).fill(true);

  isPrime[0] = false;
  if (n >= 1) isPrime[1] = false;

  for (let p = 2; p * p <= n; p++) {
    if (!isPrime[p]) continue;

    for (let multiple = p * p; multiple <= n; multiple += p) {
      isPrime[multiple] = false;
    }
  }

  const primes = [];

  for (let i = 2; i <= n; i++) {
    if (isPrime[i]) primes.push(i);
  }

  return primes;
}
```

---

## 29.5 Fast Exponentiation

Fast exponentiation computes `base^exp` by repeatedly squaring the base and using the binary representation of the exponent. Each step halves the remaining exponent, reducing multiplication count from `O(exp)` to `O(log exp)`. A modular variant applies `% mod` after multiplications to keep values bounded.

Compute `base^exp` efficiently.

```js
function fastPow(base, exp) {
  let result = 1;

  while (exp > 0) {
    if (exp % 2 === 1) {
      result *= base;
    }

    base *= base;
    exp = Math.floor(exp / 2);
  }

  return result;
}
```

Time: O(log exp)

---

## 29.6 Modular Exponentiation with BigInt

Modular exponentiation combines exponentiation by squaring with a modulus and `BigInt` arithmetic so intermediate values remain exact even beyond `Number`'s safe integer range. Keep all operands as `BigInt` (for example `1n`), because JavaScript does not allow mixing `Number` and `BigInt` in arithmetic.

```js
function modPow(base, exp, mod) {
  base = BigInt(base);
  exp = BigInt(exp);
  mod = BigInt(mod);

  let result = 1n;

  while (exp > 0n) {
    if (exp & 1n) {
      result = (result * base) % mod;
    }

    base = (base * base) % mod;
    exp >>= 1n;
  }

  return result;
}
```

---

# 30. Monotonic Stack and Queue

Monotonic stacks and queues maintain candidates in sorted order while processing a sequence. They turn many 'nearest greater/smaller' and sliding-window extrema problems into linear time because each element is inserted and removed only a constant number of times.

A monotonic structure keeps values in increasing or decreasing order.

These patterns often reduce O(n²) "find next greater/smaller" problems to O(n).

---

## 30.1 Next Greater Element

Next-greater-element problems ask for the first later value that exceeds the current value. A decreasing monotonic stack stores unresolved indexes/values; when a larger value arrives, it resolves stack entries until monotonic order is restored. Each item is pushed and popped at most once, so the scan is `O(n)`.

```js
function nextGreater(nums) {
  const result = new Array(nums.length).fill(-1);
  const stack = [];

  for (let i = 0; i < nums.length; i++) {
    while (
      stack.length > 0 &&
      nums[i] > nums[stack[stack.length - 1]]
    ) {
      const index = stack.pop();
      result[index] = nums[i];
    }

    stack.push(i);
  }

  return result;
}
```

Each index enters and leaves the stack at most once.

Time: O(n)

---

## 30.2 Daily Temperatures Pattern

Daily Temperatures is a next-greater-element problem. A decreasing stack of unresolved indexes waits until a warmer temperature appears; then the index difference gives the waiting days. Store indexes rather than only temperatures because the output needs distance.

Same principle:

> Pop all previous positions whose answer has just been found.

---

## 30.3 Sliding Window Maximum

A sliding window tracks a contiguous range while updating only the information that changes when the range expands or shrinks. Fixed-size windows are used when the length is known; variable-size windows adjust a boundary until a validity condition is restored. The usual goal is to replace repeated recomputation of every subarray or substring with a single linear pass.

Use a deque that stores useful indices in decreasing value order.

```js
function maxSlidingWindow(nums, k) {
  const deque = [];
  let head = 0;
  const result = [];

  for (let i = 0; i < nums.length; i++) {
    while (
      head < deque.length &&
      deque[head] <= i - k
    ) {
      head++;
    }

    while (
      deque.length > head &&
      nums[deque[deque.length - 1]] <= nums[i]
    ) {
      deque.pop();
    }

    deque.push(i);

    if (i >= k - 1) {
      result.push(nums[deque[head]]);
    }
  }

  return result;
}
```

Time: O(n)

---

# 31. String-Matching Algorithms

String-matching algorithms search for one or more patterns inside text. Compare them by preprocessing cost, search complexity, memory, collision behavior, alphabet assumptions, and whether the same pattern or same text will be queried repeatedly.

## 31.1 Naive Matching

Naive pattern matching tries the pattern at every possible text start and compares characters until mismatch. Worst-case time is `O(nm)`, but it is simple and often adequate for small inputs; KMP/Z avoid repeated comparisons when larger guarantees are needed.

Try the pattern at every starting position.

Worst case:

```txt
O(n × m)
```

where:

- `n` = text length,
- `m` = pattern length.

---

## 31.2 KMP

Knuth-Morris-Pratt (KMP) searches for a pattern without rechecking characters that are already known to match. It preprocesses the pattern into a prefix/failure table, then uses that table to decide how far the pattern can shift after a mismatch. Preprocessing plus search runs in `O(m + n)` for pattern length `m` and text length `n`.

KMP avoids rechecking characters by preprocessing the pattern.

It builds an LPS array:

> Longest Proper Prefix which is also Suffix.

### Build LPS

The KMP LPS (longest proper prefix that is also a suffix) table records how much of the pattern can still be reused after a mismatch. While building it, a mismatch falls back to a shorter previously computed border instead of restarting from zero, which keeps preprocessing linear.

```js
function buildLPS(pattern) {
  const lps = new Array(pattern.length).fill(0);

  let len = 0;
  let i = 1;

  while (i < pattern.length) {
    if (pattern[i] === pattern[len]) {
      len++;
      lps[i] = len;
      i++;
    } else if (len > 0) {
      len = lps[len - 1];
    } else {
      lps[i] = 0;
      i++;
    }
  }

  return lps;
}
```

### Search

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

```js
function kmpSearch(text, pattern) {
  if (pattern.length === 0) return 0;

  const lps = buildLPS(pattern);

  let i = 0;
  let j = 0;

  while (i < text.length) {
    if (text[i] === pattern[j]) {
      i++;
      j++;

      if (j === pattern.length) {
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

Time: O(n + m)

---

## 31.3 Rabin-Karp

Rabin-Karp compares rolling hash values for the pattern and each same-length text window. Updating the rolling hash can be constant-time per shift, making the average scan efficient and especially useful when searching many patterns or repeated windows. Because different strings can share a hash, a hash match should be verified when correctness cannot tolerate collisions.

Rabin-Karp compares rolling hashes.

Useful when:

- searching many patterns,
- substring hashing,
- plagiarism-like matching,
- repeated substring techniques.

Be aware of hash collisions.

---

## 31.4 Z Algorithm

The Z array stores:

> length of the longest substring starting at `i` that matches the prefix.

Useful for:

- pattern matching,
- repeated prefixes,
- string periodicity.

KMP and Z are both worth learning after mastering basic string patterns.

---

# 32. Segment Trees

A segment tree supports efficient range queries and point/range updates.

Common queries:

- range sum,
- range minimum,
- range maximum,
- GCD,
- custom associative aggregation.

Typical complexity:

| Operation | Complexity |
|---|---:|
| Build | O(n) |
| Query | O(log n) |
| Point update | O(log n) |

---

## 32.1 Range Sum Segment Tree

A segment tree recursively stores an aggregate for intervals of the array. For range sums, each node stores the sum of its segment; a query skips disjoint segments, returns fully covered segments, and splits partial overlaps. Point updates and range queries are typically `O(log n)` after `O(n)` construction.

```js
class SegmentTree {
  constructor(nums) {
    this.n = nums.length;
    this.tree = new Array(2 * this.n).fill(0);

    for (let i = 0; i < this.n; i++) {
      this.tree[this.n + i] = nums[i];
    }

    for (let i = this.n - 1; i > 0; i--) {
      this.tree[i] =
        this.tree[i * 2] +
        this.tree[i * 2 + 1];
    }
  }

  update(index, value) {
    let pos = index + this.n;
    this.tree[pos] = value;

    while (pos > 1) {
      pos = Math.floor(pos / 2);

      this.tree[pos] =
        this.tree[pos * 2] +
        this.tree[pos * 2 + 1];
    }
  }

  query(left, right) {
    // [left, right)
    let l = left + this.n;
    let r = right + this.n;

    let sum = 0;

    while (l < r) {
      if (l % 2 === 1) {
        sum += this.tree[l++];
      }

      if (r % 2 === 1) {
        sum += this.tree[--r];
      }

      l = Math.floor(l / 2);
      r = Math.floor(r / 2);
    }

    return sum;
  }
}
```

---

## 32.2 Lazy Propagation

If a problem requires many range updates and range queries, a simple segment tree may not be enough.

**Lazy propagation** postpones updates until they are actually needed.

Learn lazy propagation after mastering:

- recursion,
- segment tree build/query/update,
- range semantics.

---

# 33. Fenwick Tree / Binary Indexed Tree

Fenwick Tree efficiently supports prefix sums with updates.

Typical complexity:

- update: O(log n)
- prefix sum: O(log n)
- range sum: O(log n)

It is simpler than a segment tree for prefix-sum-style operations.

---

## 33.1 Implementation

This implementation turns the surrounding concept into concrete state and operations. Identify what each field stores, which method mutates that state, and what invariant must remain true after every operation; those details matter more than memorizing the exact syntax.

```js
class FenwickTree {
  constructor(n) {
    this.n = n;
    this.bit = new Array(n + 1).fill(0);
  }

  add(index, delta) {
    // external index: 0-based
    for (let i = index + 1; i <= this.n; i += i & -i) {
      this.bit[i] += delta;
    }
  }

  prefixSum(index) {
    let sum = 0;

    for (let i = index + 1; i > 0; i -= i & -i) {
      sum += this.bit[i];
    }

    return sum;
  }

  rangeSum(left, right) {
    return (
      this.prefixSum(right) -
      (left > 0 ? this.prefixSum(left - 1) : 0)
    );
  }
}
```

---

# 34. Advanced Graph Algorithms

Advanced graph problems are defined less by their story and more by graph properties: edge weights, direction, cycles, connectivity, negative edges, or repeated connectivity changes. Verify those properties first because they determine whether shortest path, MST, SCC, bridge/articulation, flow, or specialized traversal algorithms are valid.

## 34.1 Bellman-Ford

Bellman-Ford finds single-source shortest paths even when some edges are negative. Relax every edge up to `V-1` times because a simple shortest path uses at most `V-1` edges; one additional successful relaxation indicates a reachable negative cycle. Complexity is `O(VE)`.

Use when negative edge weights may exist.

Properties:

- single-source shortest path,
- can detect reachable negative-weight cycles.

Complexity:

```txt
O(VE)
```

---

## 34.2 Floyd-Warshall

Floyd-Warshall computes all-pairs shortest paths by progressively allowing each vertex as an intermediate point. Its core transition is `dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])`. It uses `O(V³)` time and `O(V²)` distance storage and can handle negative edges, but not negative cycles when meaningful finite shortest paths are required.

All-pairs shortest paths.

DP relation:

```txt
dist[i][j] =
min(
  dist[i][j],
  dist[i][k] + dist[k][j]
)
```

Complexity:

```txt
O(V³)
```

Good for smaller graphs.

---

## 34.3 Minimum Spanning Tree

A minimum spanning tree (MST) connects all vertices of a connected, weighted, undirected graph with minimum total edge weight and no cycles. Kruskal's algorithm grows the MST by globally smallest safe edges; Prim's grows outward from the current tree. If the graph is disconnected, the corresponding result is a minimum spanning forest rather than one spanning tree.

Goal:

Connect all vertices with minimum total edge cost.

### Kruskal

1. Sort edges by weight.
2. Add smallest edge that does not create a cycle.
3. Use DSU.

```js
function kruskal(n, edges) {
  edges.sort((a, b) => a[2] - b[2]);

  const dsu = new DSU(n);

  let total = 0;
  let used = 0;

  for (const [u, v, weight] of edges) {
    if (dsu.union(u, v)) {
      total += weight;
      used++;

      if (used === n - 1) break;
    }
  }

  return used === n - 1 ? total : null;
}
```

---

## 34.4 Prim

Prim's algorithm builds a minimum spanning tree by repeatedly adding the cheapest edge that connects the current tree to a new vertex. A min-priority queue efficiently selects the next candidate edge. With an adjacency list and binary heap, the common complexity is `O(E log V)`; the graph should be treated as weighted and undirected for the standard MST problem.

Grow an MST from a starting node by repeatedly choosing the cheapest edge connecting the tree to an unvisited node.

Usually implemented with a min heap.

---

## 34.5 Strongly Connected Components

In a directed graph, an SCC is a maximal group where every node can reach every other node.

Common algorithms:

- Kosaraju,
- Tarjan.

Use cases:

- dependency cycles,
- condensation DAG,
- graph structure analysis.

---

## 34.6 Bridges and Articulation Points

Bridges and articulation points identify single edges/vertices whose removal increases connectivity components. A DFS uses discovery times and low-link values to determine whether a subtree has an alternate route back to an ancestor. The algorithm is `O(V + E)` with an adjacency list.

### Bridge

A **bridge** is an edge whose removal increases the number of connected components in an undirected graph. In DFS low-link analysis, a tree edge `(u,v)` is a bridge when `low[v] > disc[u]`, meaning the child's subtree has no back edge reaching `u` or an ancestor.

An edge whose removal increases connected components.

### Articulation point

A vertex whose removal disconnects part of the graph.

These use DFS discovery times and low-link values.

Learn after mastering:

- DFS,
- graph timestamps,
- recursion tree,
- undirected graph parent handling.

---

# 35. Advanced Dynamic Programming

Advanced DP expands the same fundamentals—state, transition, base cases, evaluation order—into multidimensional, interval, tree, bitmask, digit, or optimization-heavy states. The first task is always to prove what one state represents and why transitions cover all valid choices exactly as intended.

## 35.1 Interval DP

Interval DP defines a state over a contiguous range, commonly `dp[left][right]`, and combines answers from smaller subintervals. It appears in problems such as matrix-chain multiplication, optimal parenthesization, or bursting balloons. The challenge is choosing the interval length/order so every dependency has already been computed.

State represents a range:

```txt
dp[left][right]
```

Typical problems:

- matrix chain multiplication,
- burst balloons,
- palindrome partitioning,
- merging ranges.

---

## 35.2 Tree DP

Tree DP computes a state for each node from states of its children (or from a rerooted parent/child relationship). A DFS usually establishes the processing order. Clearly define what each state means—for example, 'best answer in this subtree if the node is chosen'—because correctness depends on combining child states consistently.

State is calculated from child subtrees.

Typical pattern:

```js
function dfs(node, parent) {
  let value = base;

  for (const child of graph[node]) {
    if (child === parent) continue;

    const childValue = dfs(child, node);
    value = combine(value, childValue);
  }

  return value;
}
```

---

## 35.3 Bitmask DP

Used when `n` is small, often `n <= 20` approximately.

State:

```txt
dp[mask]
```

or:

```txt
dp[mask][last]
```

Common for:

- traveling salesperson,
- assignment,
- subset selection,
- visiting sets of nodes.

---

## 35.4 Digit DP

Counts numbers satisfying digit-based conditions without enumerating all values.

Typical state may include:

```txt
position
tight
started
additional properties
```

Examples:

- count numbers ≤ N with digit sum K,
- count numbers without repeated digits,
- count numbers containing a pattern.

This is an advanced topic.

---

## 35.5 DP Optimization Mindset

After solving a DP problem:

1. Can one dimension be removed?
2. Are only previous rows needed?
3. Can transitions be optimized with prefix sums?
4. Can monotonic queue optimization apply?
5. Can binary search reduce a transition?
6. Is there a greedy reformulation?

---

# 36. Common Interview Patterns

Interview patterns are recognition shortcuts, not substitutes for reasoning. For each clue, confirm the necessary preconditions, state the invariant or state definition, and explain why the optimized approach eliminates the brute-force bottleneck.

Learning patterns is more useful than memorizing isolated solutions.

---

## 36.1 Frequency Counter

A frequency-counter pattern summarizes input as value → count and then compares or queries those counts instead of repeatedly scanning the original data. It trades `O(n)` extra storage in the worst case for expected constant-time frequency lookup.

Clues:

- duplicate,
- anagram,
- counts,
- matching frequency.

Use:

```js
Map
Set
```

---

## 36.2 Two Pointers

Two pointers maintain two indexes or references whose movement eliminates unnecessary repeated work. Common forms are opposite-end pointers on sorted data and same-direction read/write pointers for in-place filtering. The technique is most valuable when pointer movement can be justified by an invariant, such as sorted order or a maintained valid region.

Clues:

- sorted array,
- pair target,
- palindrome,
- remove duplicates,
- opposite ends.

---

## 36.3 Sliding Window

A sliding window tracks a contiguous range while updating only the information that changes when the range expands or shrinks. Fixed-size windows are used when the length is known; variable-size windows adjust a boundary until a validity condition is restored. The usual goal is to replace repeated recomputation of every subarray or substring with a single linear pass.

Clues:

- contiguous,
- substring,
- subarray,
- longest/shortest,
- fixed-size window.

---

## 36.4 Fast and Slow Pointer

Fast/slow pointers move through the same structure at different rates. The technique works when relative speed reveals structure—for example, the middle of a linked list or a cycle. State the loop condition carefully because it controls where the slow pointer ends on even-length inputs.

Clues:

- linked-list cycle,
- middle node,
- repeated-state sequence.

---

## 36.5 Binary Search

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

Clues:

- sorted input,
- monotonic condition,
- minimum feasible answer,
- maximum possible answer.

---

## 36.6 DFS/BFS

Breadth-first search explores a graph or tree level by level using a queue. In an unweighted graph, the first time BFS reaches a vertex is through a path with the minimum number of edges from the start. With adjacency-list representation, a complete traversal is `O(V + E)` when each vertex is processed once.

Clues:

- connected components,
- tree traversal,
- grid islands,
- path existence,
- shortest unweighted path.

---

## 36.7 Backtracking

Backtracking explores a decision tree by making a choice, recursively exploring what follows, and then undoing that choice before trying the next option. It is appropriate when the task asks for all valid combinations, permutations, placements, paths, or constraint-satisfying configurations. Pruning impossible branches early is often the difference between a practical and an impractical solution.

Clues:

- all combinations,
- all permutations,
- choices with undo,
- constraint search.

---

## 36.8 Heap / Top K

A heap is a partially ordered tree structure commonly used to implement a priority queue. A min-heap exposes the smallest item; a max-heap exposes the largest. Insert and removal of the root are typically `O(log n)`, while reading the root is `O(1)`, making heaps ideal for top-k, scheduling, streaming minima/maxima, and graph algorithms such as Dijkstra or Prim.

Clues:

- K largest,
- K smallest,
- continuously retrieve min/max,
- streaming,
- priority scheduling.

---

## 36.9 Monotonic Stack

A monotonic stack keeps its elements in increasing or decreasing order by removing values that can no longer be useful. Each element is pushed and popped at most once, so many nearest-greater/nearest-smaller problems become `O(n)`. The crucial design decision is whether the stack stores values or indexes and which comparison preserves the needed candidate boundary.

Clues:

- next greater,
- next smaller,
- nearest greater/smaller,
- histogram,
- temperature wait time.

---

## 36.10 Prefix Sum

A prefix sum precomputes cumulative totals so that later range sums can be answered by subtraction. With the common convention `prefix[i] = sum of elements before i`, the sum of the half-open range `[left, right)` is `prefix[right] - prefix[left]`. Building the prefix array costs `O(n)` time and each range query then costs `O(1)`.

Clues:

- many range sum queries,
- subarray sum,
- cumulative balance,
- count ranges.

---

## 36.11 Union-Find

Union-Find, also called Disjoint Set Union (DSU), maintains a collection of non-overlapping groups under two main operations: `find` identifies a representative and `union` merges groups. Path compression plus union by rank/size makes a long sequence of operations effectively near-constant time in practice. It is useful for dynamic connectivity, cycle detection in undirected graphs, Kruskal's MST, and component grouping.

Clues:

- dynamically connect groups,
- cycle in undirected graph,
- number of components,
- redundant connection.

---

## 36.12 Dynamic Programming

Dynamic programming is useful when many candidate solutions reuse the same subproblems and the answer can be composed from smaller states. The core design work is to define the **state**, derive the **transition**, set correct **base cases**, and choose an evaluation order. Memoization computes states on demand; tabulation computes them in an explicit order.

Clues:

- count number of ways,
- min/max result over choices,
- repeated subproblems,
- subsequence,
- optimal partition.

---

# 37. JavaScript-Specific DSA Pitfalls

JavaScript has several behaviors that matter directly in DSA: numeric values use IEEE-754 `Number`, default array sorting is string-based, front-of-array operations can shift elements, object keys differ from `Map` keys, and deep recursion may exceed the call stack. Choose APIs with those semantics in mind.

## 37.1 Numeric Sort

JavaScript's `Array.prototype.sort()` compares string forms by default. Supply a comparator for numeric order: `(a, b) => a - b` ascending or `b - a` descending. `sort()` mutates the array, so copy first if the original order must be preserved.

Wrong:

```js
nums.sort();
```

Correct:

```js
nums.sort((a, b) => a - b);
```

---

## 37.2 `shift()` Performance

`shift()` removes the first array element, which may require reindexing/moving the remaining elements and is therefore linear in array length in typical engines. Repeated `shift()` calls can turn a queue algorithm quadratic; use a head index or a dedicated deque/queue structure instead.

Repeated queue operations with `shift()` can be inefficient.

Prefer head index.

---

## 37.3 Deep Recursion

Recursion solves a problem by calling the same routine on a smaller or simpler state. Every recursive solution needs a **base case** that stops further calls and a **progress rule** that moves toward that base case. Also account for call-stack space: even an algorithm with little explicit memory usage may use `O(depth)` stack space.

JavaScript may throw:

```txt
RangeError: Maximum call stack size exceeded
```

For deep DFS:

- use an iterative stack,
- or ensure input depth is safe.

---

## 37.4 `Number` Precision

JavaScript `Number` exactly represents integers only up to `Number.MAX_SAFE_INTEGER` (`2^53 - 1`). Sums/products beyond the safe range may silently lose integer precision. Use `BigInt` when exact large-integer arithmetic is required, while remembering it cannot be mixed directly with `Number`.

Large integers may lose precision.

Use:

```js
BigInt
```

when required.

---

## 37.5 Bitwise 32-Bit Conversion

Bitwise operations convert numeric operands to 32-bit integers.

Do not assume JavaScript bitwise operations safely handle all `Number` integer magnitudes.

---

## 37.6 Object vs Map

Objects have prototype behavior and string/symbol property keys.

For DSA frequency/lookup logic, `Map` can be clearer:

```js
const map = new Map();
```

Use objects when appropriate, but understand the difference.

---

## 37.7 Copying Arrays

An array-like structure stores elements in an indexed sequence. Its main advantage is direct access by position; the main trade-off is that inserting or deleting near the front or middle usually requires shifting elements. In DSA problems, arrays are also the base structure behind two pointers, sliding windows, prefix sums, binary search, heaps, and many dynamic-programming tables.

Shallow copy:

```js
const copy = [...arr];
```

For a matrix:

```js
const matrixCopy = matrix.map(row => [...row]);
```

This is still only a shallow copy at the nested-element level.

---

## 37.8 Matrix Initialization Bug

Using `Array(rows).fill(sameArray)` repeats the **same inner-array reference**, so changing one row changes every row. Create each row independently, for example with `Array.from({length: rows}, () => Array(cols).fill(0))`.

Wrong:

```js
const matrix = new Array(3).fill(new Array(3).fill(0));
```

All rows refer to the same array.

Correct:

```js
const matrix = Array.from(
  { length: 3 },
  () => new Array(3).fill(0)
);
```

---

## 37.9 String Immutability

An immutable string cannot be modified in place after creation. Operations that appear to change it actually create a new string, which matters in loops because repeated concatenation can allocate many temporary objects. For many edits, collect pieces in a mutable buffer/list and build the final string once.

Repeated string concatenation may be less suitable for some heavy construction scenarios.

Collect pieces and `join("")` when appropriate.

---

## 37.10 `Math.max(...largeArray)`

Spreading a very large array into `Math.max` passes every element as a function argument and can exceed engine argument limits or allocate heavily. For large data, scan with a loop/reducer instead; the asymptotic time remains `O(n)` without the huge argument list.

Spreading a huge array can exceed argument limits.

Safer:

```js
let max = -Infinity;

for (const value of nums) {
  if (value > max) max = value;
}
```

---

# 38. Reusable JavaScript Templates

Templates reduce boilerplate for patterns you already understand, but they should not be memorized as unexplained code. For each template, know the invariant, parameter meaning, return value, mutation behavior, and the exact condition that changes its boundaries or state.

## 38.1 Frequency Map

A frequency map stores `value → count`. Scan the input once, incrementing the count for each value; later frequency queries are average `O(1)` with a hash map. This pattern is useful for duplicates, anagrams, counting categories, majority/frequency problems, and many sliding-window algorithms.

```js
function frequencyMap(values) {
  const freq = new Map();

  for (const value of values) {
    freq.set(value, (freq.get(value) ?? 0) + 1);
  }

  return freq;
}
```

---

## 38.2 Binary Search

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

```js
function binarySearch(nums, target) {
  let left = 0;
  let right = nums.length - 1;

  while (left <= right) {
    const mid = left + Math.floor((right - left) / 2);

    if (nums[mid] === target) return mid;

    if (nums[mid] < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }

  return -1;
}
```

---

## 38.3 Sliding Window

A sliding window tracks a contiguous range while updating only the information that changes when the range expands or shrinks. Fixed-size windows are used when the length is known; variable-size windows adjust a boundary until a validity condition is restored. The usual goal is to replace repeated recomputation of every subarray or substring with a single linear pass.

```js
function slidingWindow(nums) {
  let left = 0;

  for (let right = 0; right < nums.length; right++) {
    // add nums[right] to state

    while (/* window invalid */) {
      // remove nums[left] from state
      left++;
    }

    // update answer
  }
}
```

---

## 38.4 DFS Tree

Depth-first search explores one branch as far as possible before returning to try another branch. It can be implemented recursively or with an explicit stack and is widely used for connected components, cycle detection, tree processing, path exploration, topological reasoning, and many backtracking-style searches. Track visited state in cyclic graphs to avoid endless revisits.

```js
function dfs(node) {
  if (!node) return;

  dfs(node.left);
  dfs(node.right);
}
```

---

## 38.5 DFS Graph

Depth-first search explores one branch as far as possible before returning to try another branch. It can be implemented recursively or with an explicit stack and is widely used for connected components, cycle detection, tree processing, path exploration, topological reasoning, and many backtracking-style searches. Track visited state in cyclic graphs to avoid endless revisits.

```js
function dfs(graph, start) {
  const visited = new Set();

  function visit(node) {
    if (visited.has(node)) return;

    visited.add(node);

    for (const next of graph.get(node) ?? []) {
      visit(next);
    }
  }

  visit(start);

  return visited;
}
```

---

## 38.6 BFS

Breadth-first search explores a graph or tree level by level using a queue. In an unweighted graph, the first time BFS reaches a vertex is through a path with the minimum number of edges from the start. With adjacency-list representation, a complete traversal is `O(V + E)` when each vertex is processed once.

```js
function bfs(graph, start) {
  const visited = new Set([start]);
  const queue = [start];

  let head = 0;

  while (head < queue.length) {
    const node = queue[head++];

    for (const next of graph.get(node) ?? []) {
      if (!visited.has(next)) {
        visited.add(next);
        queue.push(next);
      }
    }
  }

  return visited;
}
```

---

## 38.7 Backtracking

Backtracking explores a decision tree by making a choice, recursively exploring what follows, and then undoing that choice before trying the next option. It is appropriate when the task asks for all valid combinations, permutations, placements, paths, or constraint-satisfying configurations. Pruning impossible branches early is often the difference between a practical and an impractical solution.

```js
function backtrack(path, choices) {
  if (/* complete */) {
    // record a copy
    return;
  }

  for (const choice of choices) {
    if (/* invalid */) continue;

    path.push(choice);

    backtrack(path, choices);

    path.pop();
  }
}
```

---

## 38.8 Memoization

Memoization caches a function's result by state so repeated calls return immediately. In Python, a dictionary or `functools.cache/lru_cache` can be used when arguments are hashable. Include all state-changing parameters in the cache key.

```js
function solve(state, memo = new Map()) {
  const key = JSON.stringify(state);

  if (memo.has(key)) {
    return memo.get(key);
  }

  const result = /* recurrence */;

  memo.set(key, result);

  return result;
}
```

For performance-critical problems, avoid expensive `JSON.stringify()` when a compact numeric/string key can be constructed.

---

## 38.9 Topological Sort

A topological ordering places every prerequisite before the items that depend on it. It exists only for a **directed acyclic graph (DAG)**. Common implementations use Kahn's algorithm with indegrees and a queue, or DFS with postorder; if all vertices cannot be ordered, the dependency graph contains a cycle.

```js
function topo(n, edges) {
  const graph = Array.from({ length: n }, () => []);
  const indegree = new Array(n).fill(0);

  for (const [u, v] of edges) {
    graph[u].push(v);
    indegree[v]++;
  }

  const queue = [];
  let head = 0;

  for (let i = 0; i < n; i++) {
    if (indegree[i] === 0) queue.push(i);
  }

  const order = [];

  while (head < queue.length) {
    const node = queue[head++];
    order.push(node);

    for (const next of graph[node]) {
      if (--indegree[next] === 0) {
        queue.push(next);
      }
    }
  }

  return order.length === n ? order : null;
}
```

---

# 39. DSA Learning Roadmap

A learning roadmap should progress from basic containers and complexity to reusable patterns, trees/graphs, and advanced techniques. Advance when you can derive and explain a solution without copying, not merely when you have completed a fixed number of exercises.

A good sequence matters.

## Phase 1 — Fundamentals

Learn:

- JavaScript basics,
- arrays,
- strings,
- objects,
- Map,
- Set,
- loops,
- functions,
- Big O.

Goal:

> Be able to analyze O(1), O(n), O(n²), O(log n), O(n log n).

---

## Phase 2 — Core Patterns

This phase groups skills that reinforce one another. Do not judge progress only by the number of topics completed; the target is being able to recognize the pattern, implement it without copying, analyze complexity, and explain edge cases.

Learn:

- frequency counting,
- two pointers,
- sliding window,
- prefix sum,
- binary search.

These patterns solve a very large number of interview questions.

---

## Phase 3 — Linear Data Structures

This phase groups skills that reinforce one another. Do not judge progress only by the number of topics completed; the target is being able to recognize the pattern, implement it without copying, analyze complexity, and explain edge cases.

Learn:

- linked list,
- stack,
- queue,
- deque.

Solve:

- reverse list,
- cycle detection,
- valid parentheses,
- min stack,
- queue-based BFS.

---

## Phase 4 — Recursion and Backtracking

Backtracking explores a decision tree by making a choice, recursively exploring what follows, and then undoing that choice before trying the next option. It is appropriate when the task asks for all valid combinations, permutations, placements, paths, or constraint-satisfying configurations. Pruning impossible branches early is often the difference between a practical and an impractical solution.

Learn:

- recursion tree,
- base cases,
- subsets,
- permutations,
- combinations,
- N-Queens,
- grid search.

---

## Phase 5 — Trees

This phase groups skills that reinforce one another. Do not judge progress only by the number of topics completed; the target is being able to recognize the pattern, implement it without copying, analyze complexity, and explain edge cases.

Learn:

- binary trees,
- DFS traversals,
- BFS,
- BST,
- depth,
- diameter,
- LCA,
- balanced-tree concepts.

---

## Phase 6 — Heap and Trie

A heap is a partially ordered tree structure commonly used to implement a priority queue. A min-heap exposes the smallest item; a max-heap exposes the largest. Insert and removal of the root are typically `O(log n)`, while reading the root is `O(1)`, making heaps ideal for top-k, scheduling, streaming minima/maxima, and graph algorithms such as Dijkstra or Prim.

Learn:

- min/max heap,
- priority queue,
- top K,
- trie insert/search/prefix.

---

## Phase 7 — Graphs

A graph models entities as vertices and relationships as edges. Before choosing an algorithm, determine whether the graph is directed or undirected, weighted or unweighted, cyclic or acyclic, and connected or disconnected. Those properties decide whether BFS, DFS, topological sorting, shortest-path algorithms, minimum-spanning-tree algorithms, or connectivity structures are appropriate.

Learn:

- adjacency list,
- BFS,
- DFS,
- components,
- cycle detection,
- topological sort,
- Dijkstra,
- DSU,
- MST.

---

## Phase 8 — Dynamic Programming

Learn in this order:

1. Fibonacci-style 1D DP
2. Climbing stairs
3. House robber
4. Grid DP
5. Knapsack
6. Coin change
7. LIS
8. LCS
9. String DP
10. Interval DP
11. Tree DP
12. Bitmask DP

---

## Phase 9 — Advanced Topics

These items combine or extend core patterns. Add them only after the prerequisite structure is comfortable; for each one, learn the invariant and complexity rather than memorizing a finished template.

Learn:

- monotonic stack,
- monotonic queue,
- KMP/Z,
- segment tree,
- Fenwick tree,
- advanced graphs,
- bitmasking,
- advanced DP.

---

# 40. Practice Strategy

Effective practice alternates focused topic work with mixed problems. Focused sets build a pattern; mixed sets test whether you can recognize that pattern without a chapter label. Re-solve mistakes after a delay so recall and reasoning—not short-term memory—drive the solution.

## 40.1 Use Difficulty Progression

Difficulty should rise after the underlying pattern is stable. Start with one-variable versions, then add constraints, combined structures, or tighter space bounds; jumping to hard mixed problems too early can turn practice into solution memorization rather than skill building.

For every topic:

```txt
Easy -> Easy -> Medium -> Medium -> Medium -> Hard
```

Do not jump directly into the hardest problems.

---

## 40.2 Solve by Pattern

Instead of random problems, group them.

Example sliding-window session:

1. fixed-size maximum sum,
2. longest unique substring,
3. smallest window satisfying a sum,
4. frequency-constrained substring,
5. window maximum.

This builds pattern recognition.

---

## 40.3 The 30-Minute Rule

When stuck:

1. spend meaningful time understanding the problem,
2. write examples,
3. attempt brute force,
4. identify constraints,
5. only then inspect a hint or explanation.

After reading a solution:

> Close it and reimplement from memory.

---

## 40.4 Maintain a Mistake Log

Record the mistaken assumption, the first failing example, the corrected invariant, and a trigger that should remind you next time. Reviewing this log is more valuable than only recording solved problem names because it targets repeatable reasoning errors.

For every failed problem, record:

```txt
Problem:
Pattern:
What I tried:
Why it failed:
Correct idea:
Complexity:
What clue I missed:
```

This is one of the highest-value learning habits.

---

## 40.5 Repetition Schedule

Re-solve difficult problems after:

- 1 day,
- 3 days,
- 7 days,
- 14 days,
- 30 days.

Do not only reread solutions.

---

## 40.6 Explain Out Loud

After solving:

> "I use a sliding window because the problem asks for the longest contiguous substring and the validity condition can be restored by moving the left pointer."

If you can explain the solution clearly, you likely understand it.

---

# 41. Complexity Cheat Sheet

Use a complexity cheat sheet to recall typical costs, then verify the exact implementation being used. 'Hash lookup is `O(1)`' means average/expected behavior under normal hashing assumptions; a tree or language-specific container may have different guarantees.

## Arrays

An array-like structure stores elements in an indexed sequence. Its main advantage is direct access by position; the main trade-off is that inserting or deleting near the front or middle usually requires shifting elements. In DSA problems, arrays are also the base structure behind two pointers, sliding windows, prefix sums, binary search, heaps, and many dynamic-programming tables.

| Operation | Complexity |
|---|---:|
| Access | O(1) |
| Search | O(n) |
| Push | amortized O(1) |
| Pop | O(1) |
| Shift | O(n) |
| Unshift | O(n) |
| Insert/delete middle | O(n) |

---

## Hash Map / Set

Hash-based structures trade extra memory for fast average-case membership, lookup, insertion, and deletion. They are especially useful for frequency tables, duplicate detection, complement lookup, caching, and visited-state tracking. Their ordering guarantees and worst-case behavior depend on the language and implementation, so do not assume sorted iteration unless the API explicitly provides it.

Typical expected behavior:

| Operation | Average |
|---|---:|
| Insert | O(1) |
| Lookup | O(1) |
| Delete | O(1) |

---

## Linked List

| Operation | Complexity |
|---|---:|
| Access by index | O(n) |
| Search | O(n) |
| Insert head | O(1) |
| Delete head | O(1) |

---

## Stack

A stack follows **Last In, First Out (LIFO)** order: the most recently pushed item is the first one removed. The core operations are push, pop, peek/top, and an emptiness check. Stacks are useful when later work depends on the most recent unfinished item, such as expression evaluation, undo, DFS, bracket matching, monotonic-stack problems, and simulated recursion.

| Operation | Complexity |
|---|---:|
| Push | O(1) amortized |
| Pop | O(1) |
| Peek | O(1) |

---

## Queue

A queue follows **First In, First Out (FIFO)** order: the earliest enqueued item is processed first. The key operations are enqueue, dequeue, front/peek, and emptiness checking. Queues are a natural fit for breadth-first search, scheduling, buffering, and any workflow that must preserve arrival order.

With a proper head-index/circular-buffer implementation:

| Operation | Complexity |
|---|---:|
| Enqueue | O(1) amortized |
| Dequeue | O(1) |
| Front | O(1) |

---

## Heap

A heap is a partially ordered tree structure commonly used to implement a priority queue. A min-heap exposes the smallest item; a max-heap exposes the largest. Insert and removal of the root are typically `O(log n)`, while reading the root is `O(1)`, making heaps ideal for top-k, scheduling, streaming minima/maxima, and graph algorithms such as Dijkstra or Prim.

| Operation | Complexity |
|---|---:|
| Peek | O(1) |
| Push | O(log n) |
| Pop | O(log n) |

---

## BST

BST operation cost is `O(h)` for tree height `h`. Balanced height gives `O(log n)`, while a skewed tree can make search/insert/delete `O(n)`. Inorder traversal remains `O(n)` and yields sorted keys.

Balanced:

| Operation | Complexity |
|---|---:|
| Search | O(log n) |
| Insert | O(log n) |
| Delete | O(log n) |

Worst-case skewed:

```txt
O(n)
```

---

## Graph

Adjacency list:

| Algorithm | Complexity |
|---|---:|
| BFS | O(V + E) |
| DFS | O(V + E) |
| Topological Sort | O(V + E) |
| Dijkstra + heap | O((V+E) log V) |
| Bellman-Ford | O(VE) |
| Floyd-Warshall | O(V³) |

---

## Sorting

Sorting all values is often the simplest selection baseline. It is appropriate when ordered output is useful elsewhere or input size is moderate; it does unnecessary work when only one rank is needed and no other sorted-order benefit exists.

| Algorithm | Complexity |
|---|---:|
| Bubble | O(n²) |
| Selection | O(n²) |
| Insertion | O(n²) worst |
| Merge | O(n log n) |
| Quick | O(n log n) average |
| Counting | O(n + k) |

---

# 42. Pattern Recognition Cheat Sheet

Use this quick mapping during practice.

| Problem Clue | Think About |
|---|---|
| Pair in sorted array | Two pointers |
| Find value in sorted array | Binary search |
| Minimum feasible value | Binary search on answer |
| Duplicate / frequency | Map / Set |
| Contiguous subarray/substring | Sliding window |
| Many range sums | Prefix sum |
| Many range updates | Difference array |
| Reverse/middle/cycle in linked list | Pointer manipulation |
| Matching brackets | Stack |
| Next greater/smaller | Monotonic stack |
| Repeatedly get min/max | Heap |
| Top K | Heap |
| Prefix words | Trie |
| Hierarchy | Tree |
| Unweighted shortest path | BFS |
| Connected components | DFS/BFS/DSU |
| Dependencies | Topological sort |
| Weighted shortest path, no negatives | Dijkstra |
| Negative weights | Bellman-Ford |
| Connect all nodes cheaply | MST |
| All subsets/permutations | Backtracking |
| Count ways / min-max choices | DP |
| Repeated recursion states | Memoization |
| Small n with subset state | Bitmask DP |
| Dynamic range query | Segment/Fenwick tree |
| Pattern search in long text | KMP/Z/Rabin-Karp |

---

# 43. Interview Preparation Checklist

Before interviews, you should be able to implement without notes:

- Array traversal
- Hash map frequency counting
- Two Sum
- Two pointers
- Sliding window
- Prefix sum
- Binary search
- Lower/upper bound
- Linked-list reversal
- Fast/slow pointer
- Stack
- Queue
- BFS
- DFS
- Binary-tree traversals
- BST search/validation
- Heap
- Top K
- Backtracking subsets/permutations
- Topological sort
- DSU
- Dijkstra
- Basic greedy
- 1D DP
- 2D DP
- Knapsack
- LCS/LIS concepts
- Monotonic stack

You should also be able to explain:

- time complexity,
- space complexity,
- trade-offs,
- edge cases,
- why your chosen pattern works.

---

# 44. Mini Projects for DSA Practice

Mini projects connect abstract structures to persistent state and user-visible behavior. For each project, identify the dominant operations first, choose the data structure based on those operations, and document what would become slower or harder if a different structure were used.

Projects make DSA feel practical.

## 44.1 Autocomplete Search

Autocomplete is naturally modeled as prefix lookup. A trie can retrieve the node representing a prefix in `O(prefix length)`, after which suggestions can be enumerated or ranked; a sorted-list + binary-search approach can be simpler for mostly static data.

Use:

- Trie,
- DFS,
- ranking.

Features:

- insert words,
- prefix lookup,
- return top suggestions.

---

## 44.2 Route Finder

Use:

- graph,
- BFS,
- Dijkstra.

Features:

- cities as nodes,
- roads as edges,
- shortest route,
- cheapest route.

---

## 44.3 Task Scheduler

A scheduler often needs efficient priority selection plus state for queued/completed work. A priority queue handles the next highest/lowest-priority task, while maps can support task lookup/cancellation. Define tie-breaking and deadline semantics so scheduling is deterministic.

Use:

- priority queue,
- heap,
- queue.

Features:

- priority,
- deadline,
- execution order.

---

## 44.4 Browser History Simulator

Browser history is a stack-like navigation problem, often modeled with separate back and forward stacks. Visiting a new page clears forward history; Back moves the current page to the forward stack, and Forward reverses that transfer. Each navigation can be constant-time.

Use:

- stack,
- doubly linked list.

Features:

- visit,
- back,
- forward.

---

## 44.5 Social Network Suggestions

Friend relationships form a graph. Suggestions can come from two-hop neighborhoods, mutual-friend counts, or graph-ranking algorithms; use a set to exclude the user and existing friends and to deduplicate candidates. The exact algorithm depends on scale and recommendation quality requirements.

Use:

- graph,
- BFS,
- sets.

Features:

- mutual friends,
- distance between users,
- connected groups.

---

## 44.6 Cache

A basic cache maps keys to previously computed/fetched values so repeated requests can avoid expensive work. Define capacity, eviction, freshness/TTL, and invalidation; without those policies a cache can consume unbounded memory or return stale data.

Implement:

- LRU Cache.

Use:

- Hash Map,
- doubly linked list.

Target complexity:

```txt
get()  -> O(1)
put()  -> O(1)
```

---

## 44.7 Search Engine Word Index

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

Use:

- Map,
- Set,
- Trie,
- inverted index ideas.

Features:

- document indexing,
- word lookup,
- prefix lookup,
- occurrence counts.

---

# 45. Final Revision Notes

Final revision should prioritize recall and discrimination between similar patterns. Re-derive key invariants, compare alternatives, write templates from memory, and revisit mistakes—especially problems where your first approach had the wrong complexity or hidden precondition.

## 45.1 Core Principle

The core principle is to choose a technique because of the **required operations and constraints**, not because its name appeared in a similar-looking problem. State the invariant or recurrence in your own words before using the template.

DSA is not about memorizing 500 solutions.

It is about recognizing:

```txt
problem structure
      ↓
correct pattern
      ↓
correct data structure
      ↓
efficient implementation
```

---

## 45.2 The Most Important Topics

If you must prioritize, master these first:

1. Big O
2. Arrays
3. Strings
4. Hash Maps / Sets
5. Two Pointers
6. Sliding Window
7. Binary Search
8. Stack / Queue
9. Linked Lists
10. Recursion
11. Trees
12. BFS / DFS
13. Heap
14. Graphs
15. Greedy
16. Dynamic Programming

Then add advanced topics.

---

# Appendix A — Detailed Scenario Guide

Use this section to practice translating problem wording into required operations and constraints. The mapping is a starting hypothesis: confirm the technique's preconditions and explain the invariant before committing to it.

This section connects real scenarios with the appropriate DSA idea.

## Scenario 1: Detect duplicate transaction IDs

Requirement:

> A payment system receives transaction IDs. Detect whether an ID has already appeared.

Use:

```txt
Set
```

Why:

Membership lookup is the core operation.

---

## Scenario 2: Count API calls per client

This scenario is a recognition exercise. Translate the story into required operations—lookup, ordering, range processing, connectivity, priority, or dependency handling—then justify why the suggested structure makes those operations efficient.

Requirement:

> Calculate how many requests each client ID made.

Use:

```txt
Map<ClientId, Count>
```

---

## Scenario 3: Last 100 application logs

This scenario is a recognition exercise. Translate the story into required operations—lookup, ordering, range processing, connectivity, priority, or dependency handling—then justify why the suggested structure makes those operations efficient.

Requirement:

> Keep only the newest 100 logs.

Use:

```txt
Queue / circular buffer
```

---

## Scenario 4: Undo editor actions

This scenario is a recognition exercise. Translate the story into required operations—lookup, ordering, range processing, connectivity, priority, or dependency handling—then justify why the suggested structure makes those operations efficient.

Requirement:

> Undo most recent action first.

Use:

```txt
Stack
```

---

## Scenario 5: Customer support tickets

This scenario is a recognition exercise. Translate the story into required operations—lookup, ordering, range processing, connectivity, priority, or dependency handling—then justify why the suggested structure makes those operations efficient.

Requirement:

> Process tickets in arrival order.

Use:

```txt
Queue
```

If priority matters:

```txt
Priority Queue
```

---

## Scenario 6: Employee reporting hierarchy

This scenario is a recognition exercise. Translate the story into required operations—lookup, ordering, range processing, connectivity, priority, or dependency handling—then justify why the suggested structure makes those operations efficient.

Requirement:

> Find all employees under a manager.

Use:

```txt
Tree
```

---

## Scenario 7: Road navigation

This scenario is a recognition exercise. Translate the story into required operations—lookup, ordering, range processing, connectivity, priority, or dependency handling—then justify why the suggested structure makes those operations efficient.

Requirement:

> Find shortest travel route.

Use:

```txt
Weighted Graph + Dijkstra
```

---

## Scenario 8: Course prerequisites

This scenario is a recognition exercise. Translate the story into required operations—lookup, ordering, range processing, connectivity, priority, or dependency handling—then justify why the suggested structure makes those operations efficient.

Requirement:

> Find an order in which courses can be completed.

Use:

```txt
Directed Graph + Topological Sort
```

---

## Scenario 9: Search autocomplete

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

Requirement:

> Return words beginning with a typed prefix.

Use:

```txt
Trie
```

---

## Scenario 10: Top 10 most active users

This scenario is a recognition exercise. Translate the story into required operations—lookup, ordering, range processing, connectivity, priority, or dependency handling—then justify why the suggested structure makes those operations efficient.

Use:

```txt
Hash Map for counts
+
Heap for Top K
```

---

## Scenario 11: Maximum activity during any 5-minute window

This scenario is a recognition exercise. Translate the story into required operations—lookup, ordering, range processing, connectivity, priority, or dependency handling—then justify why the suggested structure makes those operations efficient.

Use:

```txt
Sliding Window
```

---

## Scenario 12: Thousands of range sum queries

This scenario is a recognition exercise. Translate the story into required operations—lookup, ordering, range processing, connectivity, priority, or dependency handling—then justify why the suggested structure makes those operations efficient.

Use:

```txt
Prefix Sum
```

If values also change dynamically:

```txt
Fenwick Tree / Segment Tree
```

---

## Scenario 13: Merge overlapping bookings

This scenario is a recognition exercise. Translate the story into required operations—lookup, ordering, range processing, connectivity, priority, or dependency handling—then justify why the suggested structure makes those operations efficient.

Sort intervals then merge.

```js
function mergeIntervals(intervals) {
  if (intervals.length === 0) return [];

  intervals.sort((a, b) => a[0] - b[0]);

  const merged = [intervals[0]];

  for (let i = 1; i < intervals.length; i++) {
    const current = intervals[i];
    const last = merged[merged.length - 1];

    if (current[0] <= last[1]) {
      last[1] = Math.max(last[1], current[1]);
    } else {
      merged.push(current);
    }
  }

  return merged;
}
```

Pattern:

```txt
Sort + Greedy / Interval Processing
```

---

## Scenario 14: Shortest number of moves in a game

This scenario is a recognition exercise. Translate the story into required operations—lookup, ordering, range processing, connectivity, priority, or dependency handling—then justify why the suggested structure makes those operations efficient.

If each move has equal cost:

```txt
BFS
```

If move costs differ and are non-negative:

```txt
Dijkstra
```

---

## Scenario 15: Find clusters of users

This scenario is a recognition exercise. Translate the story into required operations—lookup, ordering, range processing, connectivity, priority, or dependency handling—then justify why the suggested structure makes those operations efficient.

If users are connected by relationships:

```txt
DFS / BFS / DSU
```

---

# Appendix B — Classic Problems by Topic

Classic problems are useful because each isolates a reusable idea. Study them by recording the brute-force bottleneck, the optimized invariant, the required data structure, and the small change in constraints that would make a different approach necessary.

Use this as a practice checklist.

## Arrays

An array-like structure stores elements in an indexed sequence. Its main advantage is direct access by position; the main trade-off is that inserting or deleting near the front or middle usually requires shifting elements. In DSA problems, arrays are also the base structure behind two pointers, sliding windows, prefix sums, binary search, heaps, and many dynamic-programming tables.

- Two Sum
- Best Time to Buy and Sell Stock
- Maximum Subarray
- Product of Array Except Self
- Rotate Array
- Merge Sorted Array
- Missing Number

## Strings

A string is a sequence of characters, but its exact behavior depends on the language's string model and character encoding. DSA string problems commonly need indexing/traversal, frequency counting, substring handling, comparison, prefix/suffix reasoning, or pattern matching. Always check whether the task assumes simple ASCII-like characters or full Unicode text.

- Valid Anagram
- Valid Palindrome
- Longest Common Prefix
- Group Anagrams
- Longest Substring Without Repeating Characters
- Minimum Window Substring

## Linked Lists

A linked list stores values in nodes connected by references rather than by contiguous indexed positions. This makes pointer rewiring cheap once the relevant node is known, but random access is slow because traversal normally starts from the head. Linked-list problems therefore focus heavily on pointer movement, insertion/removal, reversal, cycle detection, and fast/slow-pointer techniques.

- Reverse Linked List
- Middle of Linked List
- Linked List Cycle
- Merge Two Sorted Lists
- Remove Nth Node From End
- Reorder List
- LRU Cache

## Stack

A stack follows **Last In, First Out (LIFO)** order: the most recently pushed item is the first one removed. The core operations are push, pop, peek/top, and an emptiness check. Stacks are useful when later work depends on the most recent unfinished item, such as expression evaluation, undo, DFS, bracket matching, monotonic-stack problems, and simulated recursion.

- Valid Parentheses
- Min Stack
- Daily Temperatures
- Next Greater Element
- Largest Rectangle in Histogram
- Evaluate Reverse Polish Notation

## Queue / BFS

A queue follows **First In, First Out (FIFO)** order: the earliest enqueued item is processed first. The key operations are enqueue, dequeue, front/peek, and emptiness checking. Queues are a natural fit for breadth-first search, scheduling, buffering, and any workflow that must preserve arrival order.

- Number of Islands
- Rotting Oranges
- Shortest Path in Binary Matrix
- Binary Tree Level Order Traversal

## Binary Search

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

- Binary Search
- Search Insert Position
- First/Last Position
- Search Rotated Sorted Array
- Find Minimum in Rotated Sorted Array
- Koko Eating Bananas style problems

## Trees

- Maximum Depth
- Invert Binary Tree
- Same Tree
- Balanced Binary Tree
- Diameter
- LCA
- Validate BST
- Kth Smallest in BST
- Serialize/Deserialize Binary Tree

## Heap

A heap is a partially ordered tree structure commonly used to implement a priority queue. A min-heap exposes the smallest item; a max-heap exposes the largest. Insert and removal of the root are typically `O(log n)`, while reading the root is `O(1)`, making heaps ideal for top-k, scheduling, streaming minima/maxima, and graph algorithms such as Dijkstra or Prim.

- Kth Largest
- Top K Frequent Elements
- Merge K Sorted Lists
- Find Median from Data Stream
- Task Scheduler

## Graphs

A graph models entities as vertices and relationships as edges. Before choosing an algorithm, determine whether the graph is directed or undirected, weighted or unweighted, cyclic or acyclic, and connected or disconnected. Those properties decide whether BFS, DFS, topological sorting, shortest-path algorithms, minimum-spanning-tree algorithms, or connectivity structures are appropriate.

- Number of Islands
- Clone Graph
- Course Schedule
- Number of Connected Components
- Network Delay Time
- Cheapest Flights
- Redundant Connection
- Minimum Spanning Tree

## Backtracking

Backtracking explores a decision tree by making a choice, recursively exploring what follows, and then undoing that choice before trying the next option. It is appropriate when the task asks for all valid combinations, permutations, placements, paths, or constraint-satisfying configurations. Pruning impossible branches early is often the difference between a practical and an impractical solution.

- Subsets
- Permutations
- Combination Sum
- Letter Combinations
- Word Search
- Palindrome Partitioning
- N-Queens
- Sudoku Solver

## Dynamic Programming

Dynamic programming is useful when many candidate solutions reuse the same subproblems and the answer can be composed from smaller states. The core design work is to define the **state**, derive the **transition**, set correct **base cases**, and choose an evaluation order. Memoization computes states on demand; tabulation computes them in an explicit order.

- Climbing Stairs
- House Robber
- Coin Change
- Partition Equal Subset Sum
- Longest Increasing Subsequence
- Longest Common Subsequence
- Edit Distance
- Unique Paths
- Word Break
- Decode Ways
- Burst Balloons

---

# Appendix C — LRU Cache from Scratch

An LRU cache combines:

```txt
Hash Map + Doubly Linked List
```

Why?

Map gives O(1) key lookup.

Doubly linked list gives O(1) removal and movement when the node is already known.

```js
class DoublyNode {
  constructor(key = 0, value = 0) {
    this.key = key;
    this.value = value;

    this.prev = null;
    this.next = null;
  }
}

class LRUCache {
  constructor(capacity) {
    this.capacity = capacity;
    this.map = new Map();

    this.left = new DoublyNode();
    this.right = new DoublyNode();

    this.left.next = this.right;
    this.right.prev = this.left;
  }

  #remove(node) {
    node.prev.next = node.next;
    node.next.prev = node.prev;
  }

  #insertAtRight(node) {
    const previous = this.right.prev;

    previous.next = node;
    node.prev = previous;

    node.next = this.right;
    this.right.prev = node;
  }

  get(key) {
    if (!this.map.has(key)) {
      return -1;
    }

    const node = this.map.get(key);

    this.#remove(node);
    this.#insertAtRight(node);

    return node.value;
  }

  put(key, value) {
    if (this.map.has(key)) {
      this.#remove(this.map.get(key));
    }

    const node = new DoublyNode(key, value);

    this.map.set(key, node);
    this.#insertAtRight(node);

    if (this.map.size > this.capacity) {
      const lru = this.left.next;

      this.#remove(lru);
      this.map.delete(lru.key);
    }
  }
}
```

This is an excellent example of combining multiple data structures.

---

# Appendix D — Advanced Binary Search Examples

Binary search applies when a search space is ordered or when a yes/no feasibility condition changes monotonically. Each iteration discards roughly half of the remaining candidates, giving `O(log n)` iterations. Correct boundary handling is the main difficulty: define exactly what `left`, `right`, and `mid` mean and decide whether the interval is closed or half-open.

## Search Rotated Sorted Array

A rotated sorted array still has at least one sorted half around each midpoint. Compare the midpoint with one boundary to identify that sorted half, then decide whether the target lies inside its value range. With distinct values this gives `O(log n)`; many duplicates can make the decision ambiguous and degrade performance.

```js
function searchRotated(nums, target) {
  let left = 0;
  let right = nums.length - 1;

  while (left <= right) {
    const mid = left + Math.floor((right - left) / 2);

    if (nums[mid] === target) {
      return mid;
    }

    if (nums[left] <= nums[mid]) {
      // left side sorted
      if (nums[left] <= target && target < nums[mid]) {
        right = mid - 1;
      } else {
        left = mid + 1;
      }
    } else {
      // right side sorted
      if (nums[mid] < target && target <= nums[right]) {
        left = mid + 1;
      } else {
        right = mid - 1;
      }
    }
  }

  return -1;
}
```

Key insight:

At least one half is sorted.

---

# Appendix E — Advanced Interval Patterns

These topics extend the core toolkit for problems with stronger performance, query, or modeling requirements. Study them after the foundational data structures and patterns are comfortable so the additional invariants and implementation complexity remain understandable.

## Merge Intervals

To merge overlapping intervals, first sort by start coordinate. Keep the last merged interval; if the next interval overlaps under the chosen endpoint convention, extend the end, otherwise start a new merged interval. Sorting dominates at `O(n log n)`; the scan itself is `O(n)`.

Covered earlier.

## Insert Interval

Insertion must preserve the data structure's invariant. For an ordered tree, compare the new key at each node and descend to the appropriate child until an empty position is found; for duplicate keys, follow the policy defined by the problem. Runtime is proportional to the structure's height.

Strategy:

1. append all intervals completely before new interval,
2. merge overlapping intervals,
3. append remaining intervals.

## Meeting Rooms

Sort starts and ends or use a min heap.

Clue:

> How many simultaneous intervals exist?

Think:

- sweep line,
- heap,
- sorted events.

---

# Appendix F — Sweep Line

A sweep-line algorithm converts intervals/events into ordered points.

Example:

For each interval `[start, end]`:

```txt
(start, +1)
(end, -1)
```

Sort events, accumulate active count.

Use cases:

- maximum overlapping meetings,
- room allocation,
- concurrent sessions,
- timeline utilization.

Be careful about tie-breaking when one interval ends exactly when another starts.

---

# Appendix G — Coordinate Compression

Sometimes values are huge:

```txt
[1000000000, 50, 900000000]
```

but only relative order matters.

Compress:

```txt
50 -> 0
900000000 -> 1
1000000000 -> 2
```

Implementation:

```js
function coordinateCompress(values) {
  const sorted = [...new Set(values)].sort((a, b) => a - b);

  const rank = new Map();

  sorted.forEach((value, index) => {
    rank.set(value, index);
  });

  return values.map(value => rank.get(value));
}
```

Useful with:

- Fenwick trees,
- segment trees,
- inversion counting,
- offline queries.

---

# Appendix H — Inversion Count

An inversion is a pair:

```txt
i < j and nums[i] > nums[j]
```

Brute force:

```txt
O(n²)
```

Can be counted in:

```txt
O(n log n)
```

using merge sort.

This is a powerful example of using the merge step to count relationships.

---

# Appendix I — Meet-in-the-Middle

For some subset problems where `n ≈ 40`, `2^n` is too large but `2^(n/2)` may work.

Strategy:

1. split input in half,
2. enumerate subset values for each half,
3. sort/search/combine results.

Typical complexity:

```txt
O(2^(n/2))
```

Useful for:

- subset sum,
- closest subset target,
- constrained combinatorial search.

---

# Appendix J — Sparse Table

A sparse table is useful for **static** range queries where data does not change.

Common example:

```txt
Range Minimum Query
```

Typical:

- Build: O(n log n)
- Query: O(1) for idempotent operations such as min/max

Choose:

- Prefix sum → static sums
- Fenwick → dynamic prefix sums
- Segment tree → flexible dynamic range queries
- Sparse table → static min/max-like queries

---

# Appendix K — Shortest Path Decision Table

| Graph Type | Algorithm |
|---|---|
| Unweighted | BFS |
| All edges same cost | BFS |
| Weights 0 or 1 | 0-1 BFS |
| Non-negative weights | Dijkstra |
| Negative weights | Bellman-Ford |
| All-pairs, smaller V | Floyd-Warshall |
| DAG | Topological-order relaxation |

---

# Appendix L — 0-1 BFS Concept

If every edge weight is only `0` or `1`:

- weight 0 → push to front,
- weight 1 → push to back.

This gives:

```txt
O(V + E)
```

and can outperform Dijkstra.

Requires a proper deque.

---

# Appendix M — Common Mistakes by Topic

DSA bugs are often caused by incorrect boundaries, stale state, missing visited checks, wrong base cases, or an invariant that was never made explicit. Debug by reducing the input, tracing state changes line by line, and checking the first point where the program diverges from the expected invariant.

## Arrays

An array-like structure stores elements in an indexed sequence. Its main advantage is direct access by position; the main trade-off is that inserting or deleting near the front or middle usually requires shifting elements. In DSA problems, arrays are also the base structure behind two pointers, sliding windows, prefix sums, binary search, heaps, and many dynamic-programming tables.

- forgetting empty input,
- off-by-one indexing,
- modifying the input unintentionally.

## Binary Search

Searching a search-ordered structure relies on its ordering invariant to discard one side after each comparison. State the target and the current node/index explicitly, and define what happens when the target is absent. The runtime depends on the structure's height or search-space reduction.

- infinite loop,
- incorrect boundaries,
- wrong inequality,
- not defining what left/right represent.

## Sliding Window

A sliding window tracks a contiguous range while updating only the information that changes when the range expands or shrinks. Fixed-size windows are used when the length is known; variable-size windows adjust a boundary until a validity condition is restored. The usual goal is to replace repeated recomputation of every subarray or substring with a single linear pass.

- using it when negative values break monotonic behavior,
- forgetting to remove outgoing state,
- moving left incorrectly.

## Trees

- missing null base case,
- confusing height in nodes vs edges,
- using a global variable without resetting it.

## Graphs

A graph models entities as vertices and relationships as edges. Before choosing an algorithm, determine whether the graph is directed or undirected, weighted or unweighted, cyclic or acyclic, and connected or disconnected. Those properties decide whether BFS, DFS, topological sorting, shortest-path algorithms, minimum-spanning-tree algorithms, or connectivity structures are appropriate.

- forgetting visited tracking,
- treating directed edges as undirected,
- not processing disconnected components.

## Dijkstra

Dijkstra's algorithm computes single-source shortest paths when edge weights are non-negative. Maintain tentative distances and repeatedly process the smallest-distance candidate from a min-priority queue; ignore stale queue entries whose distance no longer matches the best known value. Typical adjacency-list complexity is `O((V+E) log V)`.

- using it with negative edges,
- not skipping stale heap entries.

## DP

- state not clearly defined,
- incorrect base case,
- wrong iteration order,
- accidentally reusing an item in 0/1 knapsack.

## Backtracking

Backtracking explores a decision tree by making a choice, recursively exploring what follows, and then undoing that choice before trying the next option. It is appropriate when the task asks for all valid combinations, permutations, placements, paths, or constraint-satisfying configurations. Pruning impossible branches early is often the difference between a practical and an impractical solution.

- forgetting to undo a choice,
- storing `current` without copying it,
- failing to skip duplicates when required.

---

# Appendix N — How to Derive an Optimized Solution

Optimization should follow a reproducible path: build a correct baseline, identify the repeated expensive operation, decide what information could be reused/precomputed, choose a structure that makes that operation cheaper, and prove the new state update preserves correctness.

Suppose brute force is O(n²).

Ask:

### Question 1

Before checking an answer, write the expected complexity/pattern and one sentence explaining why. The purpose of the question is to test reasoning from operations and constraints, not recognition of a memorized code shape.

Am I repeatedly searching for an item?

Use:

```txt
Set / Map
```

### Question 2

Before checking an answer, write the expected complexity/pattern and one sentence explaining why. The purpose of the question is to test reasoning from operations and constraints, not recognition of a memorized code shape.

Is the input sorted or can I sort it?

Use:

```txt
Two pointers / Binary search
```

### Question 3

Before checking an answer, write the expected complexity/pattern and one sentence explaining why. The purpose of the question is to test reasoning from operations and constraints, not recognition of a memorized code shape.

Am I recalculating a range sum?

Use:

```txt
Prefix sum
```

### Question 4

Before checking an answer, write the expected complexity/pattern and one sentence explaining why. The purpose of the question is to test reasoning from operations and constraints, not recognition of a memorized code shape.

Am I evaluating overlapping contiguous ranges?

Use:

```txt
Sliding window
```

### Question 5

Before checking an answer, write the expected complexity/pattern and one sentence explaining why. The purpose of the question is to test reasoning from operations and constraints, not recognition of a memorized code shape.

Am I repeatedly finding next greater/smaller?

Use:

```txt
Monotonic stack
```

### Question 6

Before checking an answer, write the expected complexity/pattern and one sentence explaining why. The purpose of the question is to test reasoning from operations and constraints, not recognition of a memorized code shape.

Am I recursively solving the same state?

Use:

```txt
Memoization / DP
```

### Question 7

Am I repeatedly finding the minimum/maximum among active candidates?

Use:

```txt
Heap
```

This "bottleneck-first" thinking is one of the best ways to improve.

---

# Appendix O — Communication During Interviews

A strong technical answer is not only code.

Use a structure like:

```txt
1. Clarify requirements.
2. Give brute-force approach.
3. State its complexity.
4. Identify the bottleneck.
5. Propose optimized approach.
6. Explain why it works.
7. Implement.
8. Test.
9. State final complexity.
```

Example:

> "A brute-force approach checks every pair, which is O(n²). Since for each number I need to know whether its complement has already appeared, I can store previous values in a Map. That reduces average lookup to constant time, making the whole pass O(n) with O(n) extra space."

This demonstrates understanding instead of memorization.

---

# Appendix P — 12-Week Suggested Study Plan

Use this plan as a sequence of skill dependencies rather than a rigid calendar. Spend extra time where you cannot yet explain the invariant, implement without copying, or analyze complexity; mastery is more important than keeping pace with a date label.

## Week 1

Treat this block as focused revision. Re-derive at least one implementation from memory, solve a fresh problem, and retry one earlier mistake so the topic is reinforced through recall rather than rereading.

- JavaScript DSA syntax
- Big O
- Arrays
- Strings

## Week 2

Treat this block as focused revision. Re-derive at least one implementation from memory, solve a fresh problem, and retry one earlier mistake so the topic is reinforced through recall rather than rereading.

- Hash Map
- Set
- Two Pointers

## Week 3

Treat this block as focused revision. Re-derive at least one implementation from memory, solve a fresh problem, and retry one earlier mistake so the topic is reinforced through recall rather than rereading.

- Sliding Window
- Prefix Sum
- Binary Search

## Week 4

Treat this block as focused revision. Re-derive at least one implementation from memory, solve a fresh problem, and retry one earlier mistake so the topic is reinforced through recall rather than rereading.

- Linked Lists
- Stack
- Queue

## Week 5

Treat this block as focused revision. Re-derive at least one implementation from memory, solve a fresh problem, and retry one earlier mistake so the topic is reinforced through recall rather than rereading.

- Recursion
- Backtracking

## Week 6

Treat this block as focused revision. Re-derive at least one implementation from memory, solve a fresh problem, and retry one earlier mistake so the topic is reinforced through recall rather than rereading.

- Trees
- BST
- BFS/DFS on trees

## Week 7

Treat this block as focused revision. Re-derive at least one implementation from memory, solve a fresh problem, and retry one earlier mistake so the topic is reinforced through recall rather than rereading.

- Heap
- Trie
- Intervals

## Week 8

Treat this block as focused revision. Re-derive at least one implementation from memory, solve a fresh problem, and retry one earlier mistake so the topic is reinforced through recall rather than rereading.

- Graph BFS/DFS
- Components
- Topological Sort

## Week 9

Treat this block as focused revision. Re-derive at least one implementation from memory, solve a fresh problem, and retry one earlier mistake so the topic is reinforced through recall rather than rereading.

- DSU
- Dijkstra
- MST
- Greedy

## Week 10

Treat this block as focused revision. Re-derive at least one implementation from memory, solve a fresh problem, and retry one earlier mistake so the topic is reinforced through recall rather than rereading.

- 1D DP
- Grid DP
- Knapsack

## Week 11

Treat this block as focused revision. Re-derive at least one implementation from memory, solve a fresh problem, and retry one earlier mistake so the topic is reinforced through recall rather than rereading.

- LCS
- LIS
- String DP
- Advanced DP patterns

## Week 12

- Monotonic Stack
- Fenwick Tree
- Segment Tree
- String algorithms
- Mixed interview sets

Repeat difficult topics after the initial 12 weeks.

---

# Appendix Q — Mastery Levels

Treat this section as an evidence-based self-check. Mark an item complete only when you can explain it in simple language, implement or apply it without copying, analyze its trade-offs, and recognize cases where it should not be used.

## Level 1 — Beginner

You can:

- write loops,
- use arrays/maps/sets,
- solve linear-search problems,
- understand Big O basics.

## Level 2 — Foundation

This mastery level groups skills that should be demonstrated through explanation and implementation, not just recognized by name. Use the bullets below as exit criteria: move on when you can solve representative problems and justify the complexity without relying on notes.

You can:

- use two pointers,
- sliding window,
- binary search,
- stack,
- queue,
- linked list.

## Level 3 — Intermediate

This mastery level groups skills that should be demonstrated through explanation and implementation, not just recognized by name. Use the bullets below as exit criteria: move on when you can solve representative problems and justify the complexity without relying on notes.

You can:

- solve tree DFS/BFS,
- backtracking,
- heaps,
- graph traversal,
- basic greedy.

## Level 4 — Strong

This mastery level groups skills that should be demonstrated through explanation and implementation, not just recognized by name. Use the bullets below as exit criteria: move on when you can solve representative problems and justify the complexity without relying on notes.

You can:

- solve topological sort,
- DSU,
- Dijkstra,
- common DP patterns,
- monotonic stack.

## Level 5 — Advanced

These items combine or extend core patterns. Add them only after the prerequisite structure is comfortable; for each one, learn the invariant and complexity rather than memorizing a finished template.

You can:

- derive DP states,
- solve advanced graph problems,
- use segment/Fenwick trees,
- understand KMP/Z,
- apply bitmask/interval/tree DP.

## Level 6 — Interview Ready

You can:

- identify patterns quickly,
- explain trade-offs,
- write correct code under time pressure,
- test edge cases,
- optimize from brute force,
- discuss complexity confidently.

---

# Appendix R — Final Master Checklist

Treat this section as an evidence-based self-check. Mark an item complete only when you can explain it in simple language, implement or apply it without copying, analyze its trade-offs, and recognize cases where it should not be used.

Mark a topic complete only when you can:

- explain it,
- implement it,
- analyze it,
- recognize when to use it,
- solve multiple related problems.

## Fundamentals

Use this checklist group as a self-test. For every item, be able to explain the core invariant or idea, implement the essential operation, state its complexity, and recognize at least one appropriate use case.

- [ ] JavaScript syntax for DSA
- [ ] Big O
- [ ] Space complexity
- [ ] Arrays
- [ ] Strings
- [ ] Map / Set

## Core Patterns

- [ ] Frequency counting
- [ ] Two pointers
- [ ] Sliding window
- [ ] Prefix sum
- [ ] Difference array
- [ ] Binary search
- [ ] Binary search on answer

## Linear Structures

Use this checklist group as a self-test. For every item, be able to explain the core invariant or idea, implement the essential operation, state its complexity, and recognize at least one appropriate use case.

- [ ] Linked list
- [ ] Fast/slow pointers
- [ ] Stack
- [ ] Queue
- [ ] Deque
- [ ] Monotonic stack
- [ ] Monotonic queue

## Recursion

Recursion solves a problem by calling the same routine on a smaller or simpler state. Every recursive solution needs a **base case** that stops further calls and a **progress rule** that moves toward that base case. Also account for call-stack space: even an algorithm with little explicit memory usage may use `O(depth)` stack space.

- [ ] Recursion basics
- [ ] Backtracking
- [ ] Subsets
- [ ] Permutations
- [ ] Combinations

## Trees

For tree revision, make sure you can explain recursive and iterative traversal, BFS level order, BST ordering, height/depth, balanced versus skewed shapes, and how recursion depth affects space. Practice both returning computed values and mutating/building tree structures.

- [ ] Binary tree
- [ ] DFS traversals
- [ ] BFS
- [ ] BST
- [ ] Height/depth
- [ ] Diameter
- [ ] LCA

## Specialized Structures

Use this checklist group as a self-test. For every item, be able to explain the core invariant or idea, implement the essential operation, state its complexity, and recognize at least one appropriate use case.

- [ ] Heap
- [ ] Priority queue
- [ ] Trie
- [ ] DSU
- [ ] Fenwick tree
- [ ] Segment tree

## Graphs

A graph models entities as vertices and relationships as edges. Before choosing an algorithm, determine whether the graph is directed or undirected, weighted or unweighted, cyclic or acyclic, and connected or disconnected. Those properties decide whether BFS, DFS, topological sorting, shortest-path algorithms, minimum-spanning-tree algorithms, or connectivity structures are appropriate.

- [ ] Graph representation
- [ ] BFS
- [ ] DFS
- [ ] Components
- [ ] Cycle detection
- [ ] Topological sort
- [ ] Dijkstra
- [ ] Bellman-Ford
- [ ] Floyd-Warshall
- [ ] Kruskal
- [ ] Prim
- [ ] SCC concepts
- [ ] Bridges/articulation concepts

## Dynamic Programming

Dynamic programming is useful when many candidate solutions reuse the same subproblems and the answer can be composed from smaller states. The core design work is to define the **state**, derive the **transition**, set correct **base cases**, and choose an evaluation order. Memoization computes states on demand; tabulation computes them in an explicit order.

- [ ] Memoization
- [ ] Tabulation
- [ ] 1D DP
- [ ] 2D DP
- [ ] Grid DP
- [ ] Knapsack
- [ ] Coin change
- [ ] LIS
- [ ] LCS
- [ ] String DP
- [ ] Interval DP
- [ ] Tree DP
- [ ] Bitmask DP
- [ ] Digit DP concepts

## Strings

A string is a sequence of characters, but its exact behavior depends on the language's string model and character encoding. DSA string problems commonly need indexing/traversal, frequency counting, substring handling, comparison, prefix/suffix reasoning, or pattern matching. Always check whether the task assumes simple ASCII-like characters or full Unicode text.

- [ ] Frequency patterns
- [ ] Sliding window strings
- [ ] Trie
- [ ] KMP
- [ ] Z algorithm concept
- [ ] Rabin-Karp concept

## Mathematics / Bits

Use this checklist group as a self-test. For every item, be able to explain the core invariant or idea, implement the essential operation, state its complexity, and recognize at least one appropriate use case.

- [ ] GCD
- [ ] LCM
- [ ] Prime checking
- [ ] Sieve
- [ ] Fast exponentiation
- [ ] Modular arithmetic basics
- [ ] Bit manipulation
- [ ] Subset masks

---

# Closing Principle

When facing a new DSA problem, do not immediately ask:

> "Which solution did I memorize?"

Ask:

> "What is the structure of this problem?"

Then reason:

```txt
What operations are repeated?
What information must I remember?
Does order matter?
Is the input sorted?
Is the answer a contiguous range?
Is this a connectivity problem?
Are there repeated subproblems?
Do I need the min/max candidate repeatedly?
Can I model this as a graph?
Can I define a DP state?
```

That is the point where DSA changes from memorization into engineering problem solving.

---

**End of Handbook**


# Appendix S — Additional Linked List Types

Linked-list variants change the available links and therefore the cost or convenience of operations. Singly, doubly, circular, and sentinel-based lists should be compared by pointer structure, traversal direction, boundary handling, memory overhead, and the operations they simplify.

## Doubly Linked List

Each node stores:

```txt
previous <- node -> next
```

This makes removal of a **known node** O(1), because both neighbors are directly accessible.

```js
class DoublyLinkedNode {
  constructor(value) {
    this.value = value;
    this.prev = null;
    this.next = null;
  }
}

class DoublyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }

  push(value) {
    const node = new DoublyLinkedNode(value);

    if (!this.tail) {
      this.head = node;
      this.tail = node;
    } else {
      node.prev = this.tail;
      this.tail.next = node;
      this.tail = node;
    }

    this.length++;
    return node;
  }

  remove(node) {
    if (!node) return;

    if (node.prev) {
      node.prev.next = node.next;
    } else {
      this.head = node.next;
    }

    if (node.next) {
      node.next.prev = node.prev;
    } else {
      this.tail = node.prev;
    }

    node.prev = null;
    node.next = null;
    this.length--;
  }
}
```

Common use cases:

- LRU cache,
- browser history,
- playlists,
- navigation in both directions.

---

## Circular Linked List

In a circular list, the final node points back to the first node.

```txt
A -> B -> C
^         |
|_________|
```

Use cases:

- round-robin scheduling,
- cyclic playlists,
- turn-based games,
- repeated rotations.

Always be careful with termination conditions because `next` may never become `null`.

---

# Appendix T — Additional Sorting and Selection Algorithms

Sorting rearranges values according to an ordering rule so later operations can exploit structure. Learn not only the code but also stability, in-place behavior, best/average/worst complexity, comparator requirements, and when a language's built-in sort is preferable to a manual algorithm.

## Heap Sort

Heap sort:

1. Build a max heap.
2. Move maximum to the end.
3. Restore heap property.
4. Repeat.

Properties:

- Time: O(n log n)
- Extra array space: O(1) for an in-place implementation
- Not stable in the usual form

```js
function heapSort(nums) {
  const arr = [...nums];
  const n = arr.length;

  function heapify(size, root) {
    while (true) {
      let largest = root;
      const left = 2 * root + 1;
      const right = 2 * root + 2;

      if (left < size && arr[left] > arr[largest]) {
        largest = left;
      }

      if (right < size && arr[right] > arr[largest]) {
        largest = right;
      }

      if (largest === root) break;

      [arr[root], arr[largest]] = [arr[largest], arr[root]];
      root = largest;
    }
  }

  for (let i = Math.floor(n / 2) - 1; i >= 0; i--) {
    heapify(n, i);
  }

  for (let end = n - 1; end > 0; end--) {
    [arr[0], arr[end]] = [arr[end], arr[0]];
    heapify(end, 0);
  }

  return arr;
}
```

---

## Radix Sort

Radix sort processes integer digits rather than directly comparing full values.

For non-negative base-10 integers, a common version repeatedly performs stable counting by each digit.

Typical complexity:

```txt
O(d × (n + base))
```

where `d` is the number of digits.

It can be useful when:

- keys are bounded integers,
- digit count is manageable,
- comparison sorting is unnecessary.

---

## Bucket Sort

Bucket sort distributes values among buckets, sorts within buckets, then concatenates them.

It can perform very well when values are approximately uniformly distributed.

Its performance depends strongly on input distribution and bucket design.

---

## Quickselect

Quickselect finds the kth smallest/largest element without fully sorting.

Average time:

```txt
O(n)
```

Worst case:

```txt
O(n²)
```

Concept:

- partition like quicksort,
- only recurse/iterate into the side containing the target index.

```js
function kthSmallest(nums, k) {
  const arr = [...nums];
  const target = k - 1;

  let left = 0;
  let right = arr.length - 1;

  while (left <= right) {
    const pivotIndex = left + Math.floor(Math.random() * (right - left + 1));

    [arr[pivotIndex], arr[right]] = [arr[right], arr[pivotIndex]];
    const pivot = arr[right];

    let p = left;

    for (let i = left; i < right; i++) {
      if (arr[i] <= pivot) {
        [arr[i], arr[p]] = [arr[p], arr[i]];
        p++;
      }
    }

    [arr[p], arr[right]] = [arr[right], arr[p]];

    if (p === target) {
      return arr[p];
    }

    if (p < target) {
      left = p + 1;
    } else {
      right = p - 1;
    }
  }

  return undefined;
}
```

Use heap instead when:

- data is streaming,
- you repeatedly need top K,
- maintaining incremental state matters.

---

# Appendix U — Tree Types You Should Know

Tree names encode structural guarantees—binary, search-ordered, balanced, heap-ordered, prefix-oriented, multiway, and so on. Learn each tree by its invariant first, because that invariant determines operation complexity and which algorithms are valid.

## Full Binary Tree

A binary tree node has at most two children, conventionally `left` and `right`. Unlike a BST, a general binary tree has no ordering rule unless the problem states one; searches therefore usually require traversal rather than directional comparison.

Every node has either:

- 0 children, or
- 2 children.

## Complete Binary Tree

A binary tree node has at most two children, conventionally `left` and `right`. Unlike a BST, a general binary tree has no ordering rule unless the problem states one; searches therefore usually require traversal rather than directional comparison.

All levels are full except possibly the last, and the last is filled from left to right.

Binary heaps use this shape.

## Perfect Binary Tree

A binary tree node has at most two children, conventionally `left` and `right`. Unlike a BST, a general binary tree has no ordering rule unless the problem states one; searches therefore usually require traversal rather than directional comparison.

Every internal node has two children and all leaves are at the same depth.

## Balanced Binary Tree

A binary tree node has at most two children, conventionally `left` and `right`. Unlike a BST, a general binary tree has no ordering rule unless the problem states one; searches therefore usually require traversal rather than directional comparison.

Height remains approximately logarithmic rather than degenerating into a chain.

## Skewed Tree

Each node has only one child.

A BST can degrade from O(log n) search to O(n) when badly skewed.

---

## AVL Tree

A self-balancing BST.

For every node, the height difference between left and right subtrees is tightly bounded.

Uses rotations to restore balance after updates.

Typical search/insert/delete:

```txt
O(log n)
```

---

## Red-Black Tree

Another self-balancing BST using coloring rules.

It allows slightly looser balance than AVL trees but still guarantees logarithmic height.

Red-black trees are common in standard-library ordered maps/sets in several languages.

For JavaScript interview work, you usually need to understand the concept rather than implement the full structure unless specifically asked.

---

## B-Tree and B+ Tree

Multiway balanced search trees optimized for storage systems where reading a block/page is expensive.

Common applications:

- databases,
- file systems,
- indexes.

A B+ tree typically stores actual records or record pointers in leaves and links leaves for efficient range scans.

These are important system-design-adjacent data structures even though they are less common in standard coding interviews.

---

# Appendix V — Graph Representation and Cycle Detection

Graph representation affects both memory and traversal cost, while cycle detection depends on graph direction. Use adjacency lists for most sparse graphs, matrices for dense/all-pairs access, and choose the cycle algorithm only after deciding whether edges are directed or undirected.

## Adjacency Matrix

An adjacency matrix uses a `V × V` table where one cell records whether or with what weight an edge connects two vertices. Edge existence is `O(1)` to check, but memory is `O(V²)` even for sparse graphs. It is useful for dense graphs or algorithms that naturally work with all vertex pairs.

```js
const matrix = Array.from(
  { length: n },
  () => new Array(n).fill(false)
);

matrix[u][v] = true;
matrix[v][u] = true;
```

Space:

```txt
O(V²)
```

Useful when:

- graph is dense,
- constant-time edge-existence checks are important,
- vertex count is small enough.

---

## Edge List

An **edge list** stores a graph as a list of edges rather than grouping edges by vertex. In `[from, to, weight]`, the first two values identify the endpoints and the third is the edge weight. It is compact and convenient when an algorithm mainly processes edges—such as Kruskal or Bellman–Ford—but it is inefficient when you frequently need all neighbors of one vertex.

```js
const edges = [
  [0, 1, 5],
  [1, 2, 8]
];
```

Useful for:

- Kruskal,
- Bellman-Ford,
- input representation.

---

## Undirected Graph Cycle Detection with DFS

Depth-first search explores one branch as far as possible before returning to try another branch. It can be implemented recursively or with an explicit stack and is widely used for connected components, cycle detection, tree processing, path exploration, topological reasoning, and many backtracking-style searches. Track visited state in cyclic graphs to avoid endless revisits.

```js
function hasUndirectedCycle(graph) {
  const n = graph.length;
  const visited = new Array(n).fill(false);

  function dfs(node, parent) {
    visited[node] = true;

    for (const next of graph[node]) {
      if (!visited[next]) {
        if (dfs(next, node)) return true;
      } else if (next !== parent) {
        return true;
      }
    }

    return false;
  }

  for (let node = 0; node < n; node++) {
    if (!visited[node] && dfs(node, -1)) {
      return true;
    }
  }

  return false;
}
```

---

## Directed Graph Cycle Detection

A directed cycle exists when DFS reaches a vertex that is already on the **current recursion path**. The three-state array distinguishes an unvisited vertex (`0`), a vertex currently being explored (`1`), and a fully processed vertex (`2`). `hasDirectedCycle(graph)` receives an adjacency-list graph and returns `true` as soon as a back-edge to state `1` is found; otherwise it returns `false`. The traversal is `O(V + E)` time and `O(V)` auxiliary space for the state array plus the DFS call stack.

Use three states:

```txt
0 = unvisited
1 = currently in DFS path
2 = completely processed
```

```js
function hasDirectedCycle(graph) {
  const n = graph.length;
  const state = new Array(n).fill(0);

  function dfs(node) {
    state[node] = 1;

    for (const next of graph[node]) {
      if (state[next] === 1) {
        return true;
      }

      if (state[next] === 0 && dfs(next)) {
        return true;
      }
    }

    state[node] = 2;
    return false;
  }

  for (let node = 0; node < n; node++) {
    if (state[node] === 0 && dfs(node)) {
      return true;
    }
  }

  return false;
}
```

---

## Bipartite Graph Check

A graph is bipartite if vertices can be colored with two colors so every edge joins different colors.

```js
function isBipartite(graph) {
  const n = graph.length;
  const color = new Array(n).fill(-1);

  for (let start = 0; start < n; start++) {
    if (color[start] !== -1) continue;

    const queue = [start];
    let head = 0;

    color[start] = 0;

    while (head < queue.length) {
      const node = queue[head++];

      for (const next of graph[node]) {
        if (color[next] === -1) {
          color[next] = color[node] ^ 1;
          queue.push(next);
        } else if (color[next] === color[node]) {
          return false;
        }
      }
    }
  }

  return true;
}
```

Useful in:

- two-group constraints,
- odd-cycle detection,
- matching foundations.

---

# Appendix W — Full Shortest-Path Reference

Shortest-path algorithms are not interchangeable. Choose based on edge weights and graph structure: BFS for unweighted/equal-weight edges, Dijkstra for non-negative weights, Bellman-Ford when negative edges matter, DAG relaxation for acyclic directed graphs, and Floyd-Warshall for all-pairs problems at smaller `V`.

## Bellman-Ford Implementation

This implementation turns the surrounding concept into concrete state and operations. Identify what each field stores, which method mutates that state, and what invariant must remain true after every operation; those details matter more than memorizing the exact syntax.

```js
function bellmanFord(n, edges, source) {
  const dist = new Array(n).fill(Infinity);
  dist[source] = 0;

  for (let i = 0; i < n - 1; i++) {
    let changed = false;

    for (const [u, v, weight] of edges) {
      if (dist[u] === Infinity) continue;

      if (dist[u] + weight < dist[v]) {
        dist[v] = dist[u] + weight;
        changed = true;
      }
    }

    if (!changed) break;
  }

  for (const [u, v, weight] of edges) {
    if (
      dist[u] !== Infinity &&
      dist[u] + weight < dist[v]
    ) {
      return {
        distances: dist,
        hasReachableNegativeCycle: true
      };
    }
  }

  return {
    distances: dist,
    hasReachableNegativeCycle: false
  };
}
```

---

## Floyd-Warshall Implementation

Floyd-Warshall computes all-pairs shortest paths by progressively allowing each vertex as an intermediate point. Its core transition is `dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])`. It uses `O(V³)` time and `O(V²)` distance storage and can handle negative edges, but not negative cycles when meaningful finite shortest paths are required.

```js
function floydWarshall(matrix) {
  const n = matrix.length;
  const dist = matrix.map(row => [...row]);

  for (let k = 0; k < n; k++) {
    for (let i = 0; i < n; i++) {
      for (let j = 0; j < n; j++) {
        dist[i][j] = Math.min(
          dist[i][j],
          dist[i][k] + dist[k][j]
        );
      }
    }
  }

  return dist;
}
```

Represent unreachable paths using `Infinity`.

---

## DAG Shortest Path

For a weighted DAG:

1. topologically sort vertices,
2. relax outgoing edges in topological order.

This can handle negative edge weights as long as there is no directed cycle.

Complexity:

```txt
O(V + E)
```

---

# Appendix X — Divide and Conquer

Divide and conquer splits a problem into smaller independent subproblems, solves them recursively, and combines their results. Merge sort is a classic example: divide the array, sort each half, then merge the sorted halves. It differs from dynamic programming because divide-and-conquer subproblems usually do not overlap heavily.

Divide and conquer:

1. divide a problem into smaller independent subproblems,
2. solve them,
3. combine results.

Examples:

- merge sort,
- quicksort,
- binary search,
- closest-pair algorithms,
- divide-and-conquer geometry.

---

## Divide and Conquer vs Dynamic Programming

Dynamic programming is useful when many candidate solutions reuse the same subproblems and the answer can be composed from smaller states. The core design work is to define the **state**, derive the **transition**, set correct **base cases**, and choose an evaluation order. Memoization computes states on demand; tabulation computes them in an explicit order.

### Divide and Conquer

Divide and conquer splits a problem into smaller independent subproblems, solves them recursively, and combines their results. Merge sort is a classic example: divide the array, sort each half, then merge the sorted halves. It differs from dynamic programming because divide-and-conquer subproblems usually do not overlap heavily.

Subproblems are usually mostly independent.

### Dynamic Programming

Dynamic programming is useful when many candidate solutions reuse the same subproblems and the answer can be composed from smaller states. The core design work is to define the **state**, derive the **transition**, set correct **base cases**, and choose an evaluation order. Memoization computes states on demand; tabulation computes them in an explicit order.

Subproblems overlap, so solved results are cached/reused.

---

## Recurrence Example

A **recurrence** expresses the running time of a recursive algorithm in terms of smaller inputs. For merge sort, `2T(n/2)` represents sorting two halves and `O(n)` represents merging them. There are about `log₂ n` levels and `O(n)` work per level, so the total running time is `O(n log n)`.

Merge sort:

```txt
T(n) = 2T(n/2) + O(n)
```

which gives:

```txt
O(n log n)
```

Understanding recurrences helps explain recursive algorithm complexity.

---

# Appendix Y — Amortized Analysis in Practice

Amortized analysis spreads the cost of occasional expensive operations over a long sequence of operations. For example, a dynamic array resize may cost `O(n)`, but because resizing is infrequent, repeated append operations can still have `O(1)` amortized cost. Amortized complexity is a sequence-level guarantee; it does not mean every individual operation is constant-time.

Sometimes one operation looks expensive but the cost is spread across many operations.

## Dynamic Array Growth

Imagine an array capacity doubles:

```txt
1 -> 2 -> 4 -> 8 -> 16 -> ...
```

A resize may copy many elements, but resizing does not happen on every push.

Across a long sequence of pushes, average push cost remains amortized O(1).

Other places amortized thinking appears:

- dynamic arrays,
- monotonic stacks,
- union-find,
- some hash-table operations.

---

# Appendix Z — Final DSA Decision Tree

A decision tree narrows the search for an algorithm by asking about structure: sortedness, contiguity, graph relationships, repeated states, priority, prefix/range operations, or monotonic feasibility. Treat the result as a candidate and verify its preconditions before coding.

When you see a new problem, walk through this checklist.

## 1. Is it a lookup/counting problem?

Answer this question from the concrete design/problem pressure first. The suggested pattern is a candidate, not an automatic choice; compare it with the simplest alternative and check whether the expected variation is real.

Think:

```txt
Map / Set
```

## 2. Is the input sorted?

Answer this question from the concrete design/problem pressure first. The suggested pattern is a candidate, not an automatic choice; compare it with the simplest alternative and check whether the expected variation is real.

Think:

```txt
Two pointers
Binary search
```

## 3. Is the answer about a contiguous subarray or substring?

Answer this question from the concrete design/problem pressure first. The suggested pattern is a candidate, not an automatic choice; compare it with the simplest alternative and check whether the expected variation is real.

Think:

```txt
Sliding window
Prefix sum
Kadane
```

## 4. Is it asking for next/previous greater or smaller?

Answer this question from the concrete design/problem pressure first. The suggested pattern is a candidate, not an automatic choice; compare it with the simplest alternative and check whether the expected variation is real.

Think:

```txt
Monotonic stack
```

## 5. Is it asking for top K or repeated min/max?

Answer this question from the concrete design/problem pressure first. The suggested pattern is a candidate, not an automatic choice; compare it with the simplest alternative and check whether the expected variation is real.

Think:

```txt
Heap
```

## 6. Is it hierarchy?

Answer this question from the concrete design/problem pressure first. The suggested pattern is a candidate, not an automatic choice; compare it with the simplest alternative and check whether the expected variation is real.

Think:

```txt
Tree DFS/BFS
```

## 7. Is it relationships, routes, dependencies, connectivity?

Answer this question from the concrete design/problem pressure first. The suggested pattern is a candidate, not an automatic choice; compare it with the simplest alternative and check whether the expected variation is real.

Think:

```txt
Graph
BFS / DFS
DSU
Topological sort
Dijkstra
MST
```

## 8. Does it ask for every possible configuration?

Answer this question from the concrete design/problem pressure first. The suggested pattern is a candidate, not an automatic choice; compare it with the simplest alternative and check whether the expected variation is real.

Think:

```txt
Backtracking
```

## 9. Does brute-force recursion repeat states?

Recursion solves a problem by calling the same routine on a smaller or simpler state. Every recursive solution needs a **base case** that stops further calls and a **progress rule** that moves toward that base case. Also account for call-stack space: even an algorithm with little explicit memory usage may use `O(depth)` stack space.

Think:

```txt
Memoization / DP
```

## 10. Are there many static range queries?

Answer this question from the concrete design/problem pressure first. The suggested pattern is a candidate, not an automatic choice; compare it with the simplest alternative and check whether the expected variation is real.

Think:

```txt
Prefix sum
Sparse table
```

## 11. Are there updates plus range queries?

Answer this question from the concrete design/problem pressure first. The suggested pattern is a candidate, not an automatic choice; compare it with the simplest alternative and check whether the expected variation is real.

Think:

```txt
Fenwick tree
Segment tree
```

## 12. Is the input tiny but choices are exponential?

Answer this question from the concrete design/problem pressure first. The suggested pattern is a candidate, not an automatic choice; compare it with the simplest alternative and check whether the expected variation is real.

Think:

```txt
Bitmasking
Meet-in-the-middle
Bitmask DP
```

---

# Final Advice for Mastery

Treat this section as an evidence-based self-check. Mark an item complete only when you can explain it in simple language, implement or apply it without copying, analyze its trade-offs, and recognize cases where it should not be used.

A learner should progress from:

```txt
syntax
→ brute force
→ complexity
→ basic data structures
→ reusable patterns
→ trees/graphs
→ greedy/DP
→ advanced structures
→ mixed problem solving
```

For every new algorithm, build four layers of understanding:

### Layer 1 — Intuition

This layer describes one dimension of mastery. Do not treat it as a vocabulary list: connect the idea to a manual dry run, a clean implementation, and an explanation of why the algorithm is correct.

Explain it without code.

### Layer 2 — Mechanics

This layer describes one dimension of mastery. Do not treat it as a vocabulary list: connect the idea to a manual dry run, a clean implementation, and an explanation of why the algorithm is correct.

Trace it manually on a small example.

### Layer 3 — Implementation

This implementation turns the surrounding concept into concrete state and operations. Identify what each field stores, which method mutates that state, and what invariant must remain true after every operation; those details matter more than memorizing the exact syntax.

Write it from memory in JavaScript.

### Layer 4 — Recognition

Know what clues in a new problem suggest that algorithm.

That fourth layer is what turns DSA knowledge into practical problem-solving skill.

---

**End of DSA with JavaScript Master Handbook**
