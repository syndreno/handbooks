# Python Debugging Master Handbook

> A beginner-friendly, practical, and in-depth guide to finding, understanding, fixing, and preventing bugs in Python applications.

---

## Table of Contents

1. [What Is Debugging?](#1-what-is-debugging)
2. [The Debugging Mindset](#2-the-debugging-mindset)
3. [Types of Bugs](#3-types-of-bugs)
4. [A Repeatable Debugging Workflow](#4-a-repeatable-debugging-workflow)
5. [Reading Python Error Messages and Tracebacks](#5-reading-python-error-messages-and-tracebacks)
6. [Syntax Errors](#6-syntax-errors)
7. [Runtime Exceptions](#7-runtime-exceptions)
8. [Logical Bugs](#8-logical-bugs)
9. [Debugging with `print()`](#9-debugging-with-print)
10. [Better Temporary Debug Output](#10-better-temporary-debug-output)
11. [Python Logging](#11-python-logging)
12. [Assertions](#12-assertions)
13. [The Built-in `breakpoint()` Function](#13-the-built-in-breakpoint-function)
14. [The `pdb` Debugger](#14-the-pdb-debugger)
15. [Post-Mortem Debugging](#15-post-mortem-debugging)
16. [Debugging in VS Code](#16-debugging-in-vs-code)
17. [Debugging in PyCharm](#17-debugging-in-pycharm)
18. [Debugging Functions](#18-debugging-functions)
19. [Debugging Variables and Scope](#19-debugging-variables-and-scope)
20. [Debugging Collections](#20-debugging-collections)
21. [Debugging Strings](#21-debugging-strings)
22. [Debugging Numeric Code](#22-debugging-numeric-code)
23. [Debugging Conditions](#23-debugging-conditions)
24. [Debugging Loops](#24-debugging-loops)
25. [Debugging Comprehensions](#25-debugging-comprehensions)
26. [Debugging File Handling](#26-debugging-file-handling)
27. [Debugging Paths](#27-debugging-paths)
28. [Debugging JSON](#28-debugging-json)
29. [Debugging CSV Data](#29-debugging-csv-data)
30. [Debugging Dates and Time](#30-debugging-dates-and-time)
31. [Debugging Exceptions Properly](#31-debugging-exceptions-properly)
32. [Custom Exceptions](#32-custom-exceptions)
33. [Debugging Object-Oriented Python](#33-debugging-object-oriented-python)
34. [Debugging Imports](#34-debugging-imports)
35. [Debugging Virtual Environments](#35-debugging-virtual-environments)
36. [Debugging Package and Dependency Problems](#36-debugging-package-and-dependency-problems)
37. [Debugging Environment Variables](#37-debugging-environment-variables)
38. [Debugging HTTP Requests and APIs](#38-debugging-http-requests-and-apis)
39. [Debugging Web Applications](#39-debugging-web-applications)
40. [Debugging Database Code](#40-debugging-database-code)
41. [Debugging Tests](#41-debugging-tests)
42. [Debugging with `pytest`](#42-debugging-with-pytest)
43. [Debugging Mocking Problems](#43-debugging-mocking-problems)
44. [Debugging Type Problems](#44-debugging-type-problems)
45. [Debugging Dataclasses](#45-debugging-dataclasses)
46. [Debugging Decorators](#46-debugging-decorators)
47. [Debugging Generators and Iterators](#47-debugging-generators-and-iterators)
48. [Debugging Context Managers](#48-debugging-context-managers)
49. [Debugging Recursion](#49-debugging-recursion)
50. [Debugging Async Python](#50-debugging-async-python)
51. [Debugging Threads](#51-debugging-threads)
52. [Debugging Multiprocessing](#52-debugging-multiprocessing)
53. [Debugging Race Conditions](#53-debugging-race-conditions)
54. [Debugging Performance Problems](#54-debugging-performance-problems)
55. [Profiling CPU Usage](#55-profiling-cpu-usage)
56. [Debugging Memory Problems](#56-debugging-memory-problems)
57. [Debugging Memory Leaks](#57-debugging-memory-leaks)
58. [Debugging Subprocesses](#58-debugging-subprocesses)
59. [Debugging Unicode and Encoding](#59-debugging-unicode-and-encoding)
60. [Debugging Regular Expressions](#60-debugging-regular-expressions)
61. [Debugging Configuration Problems](#61-debugging-configuration-problems)
62. [Debugging CLI Programs](#62-debugging-cli-programs)
63. [Debugging Dockerized Python](#63-debugging-dockerized-python)
64. [Debugging CI/CD Failures](#64-debugging-cicd-failures)
65. [Remote Debugging](#65-remote-debugging)
66. [Production Debugging](#66-production-debugging)
67. [Security-Safe Debugging](#67-security-safe-debugging)
68. [Reproducing Intermittent Bugs](#68-reproducing-intermittent-bugs)
69. [Reducing a Bug to a Minimal Reproduction](#69-reducing-a-bug-to-a-minimal-reproduction)
70. [Binary Search Debugging](#70-binary-search-debugging)
71. [Git Bisect for Regression Bugs](#71-git-bisect-for-regression-bugs)
72. [Rubber Duck Debugging](#72-rubber-duck-debugging)
73. [Debugging Real-World Scenarios](#73-debugging-real-world-scenarios)
74. [Common Debugging Mistakes](#74-common-debugging-mistakes)
75. [Debugging Best Practices](#75-debugging-best-practices)
76. [Bug Report Template](#76-bug-report-template)
77. [Debugging Checklist](#77-debugging-checklist)
78. [Python Debugging Toolkit Reference](#78-python-debugging-toolkit-reference)
79. [Learning Exercises](#79-learning-exercises)
80. [Final Debugging Strategy](#80-final-debugging-strategy)
81. [Appendix E: Recommended Python Debugging Tools and Configuration](#appendix-e-recommended-python-debugging-tools-and-configuration)

---

# 1. What Is Debugging?

**Debugging** is the process of finding out why a program behaves differently from what you intended, locating the actual cause, fixing it, and verifying that the fix does not create new problems.

A beginner often thinks debugging means:

> "Find the bad line and change it."

In real applications, debugging is usually more like:

1. Observe a symptom.
2. Reproduce it.
3. Gather evidence.
4. Form a hypothesis.
5. Test the hypothesis.
6. Locate the root cause.
7. Fix the root cause.
8. Add a test so the bug does not return.

Example:

```python
def calculate_total(price, quantity):
    return price + quantity

print(calculate_total(100, 3))
```

Output:

```text
103
```

But the expected total is `300`.

The program does not crash. It simply uses the wrong operator.

Correct version:

```python
def calculate_total(price, quantity):
    return price * quantity

print(calculate_total(100, 3))
```

Output:

```text
300
```

This is a **logical bug**.

---

# 2. The Debugging Mindset

Good debugging is less about guessing and more about investigation.

## 2.1 Ask useful questions

When something fails, ask:

- What exactly happened?
- What did I expect instead?
- Can I reproduce it?
- Does it happen every time?
- What input triggers it?
- What changed recently?
- Which part of the system definitely works?
- Which part is still uncertain?
- What evidence do I have?

## 2.2 Separate facts from assumptions

Bad debugging:

> "The database is probably broken."

Better debugging:

> "The API returned HTTP 500. The traceback shows a `KeyError` before any database query is executed."

## 2.3 Change one thing at a time

If you modify five things and the bug disappears, you do not know which change fixed it.

Prefer:

```text
change -> test -> observe -> continue
```

## 2.4 Reproduce before fixing

If possible, create a reliable reproduction first.

A bug you cannot reproduce is much harder to verify.

---

# 3. Types of Bugs

Python bugs generally fall into several categories.

| Bug type | Example | Typical symptom |
|---|---|---|
| Syntax error | Missing `:` | Program does not start |
| Runtime exception | `10 / 0` | Program crashes |
| Logical bug | `+` instead of `*` | Wrong result |
| Data bug | Unexpected `None` | Wrong or missing data |
| Integration bug | API contract changed | External call fails |
| Concurrency bug | Shared data race | Intermittent result |
| Performance bug | O(n²) loop | Program is too slow |
| Memory bug | Unbounded cache | Memory keeps growing |
| Environment bug | Wrong Python executable | Works on one machine only |
| Dependency bug | Incompatible package versions | Import/runtime failure |
| Configuration bug | Missing environment variable | Wrong startup behavior |

---

# 4. A Repeatable Debugging Workflow

Use this workflow whenever possible.

## Step 1: Define the expected behavior

Write down:

```text
Input:  price=100, quantity=3
Expected: 300
Actual:   103
```

## Step 2: Reproduce the bug

Make the failure happen consistently.

## Step 3: Reduce the problem

Remove unrelated code.

Instead of debugging a 2,000-line application, try to create a 10-line example.

## Step 4: Read the error completely

Do not read only:

```text
KeyError: 'email'
```

Read the complete traceback and identify where **your code** first failed.

## Step 5: Inspect program state

Check:

- variable values
- variable types
- function arguments
- return values
- object attributes
- database responses
- API responses
- file paths
- environment variables

## Step 6: Form a hypothesis

Example:

> "`user_data` sometimes does not contain the `email` key."

## Step 7: Prove or disprove it

```python
print(user_data)
print(user_data.keys())
```

or use a debugger.

## Step 8: Fix the root cause

Do not merely hide the symptom.

## Step 9: Add a regression test

```python
def test_user_without_email():
    ...
```

## Step 10: Remove temporary debug code

Remove noisy `print()` statements, temporary files, debug flags, and secrets.

---

# 5. Reading Python Error Messages and Tracebacks

Consider:

```python
def get_discount(price):
    return price * 0.10

def checkout(product):
    return get_discount(product["price"])

product = {"name": "Keyboard"}

print(checkout(product))
```

Python reports something similar to:

```text
Traceback (most recent call last):
  File "app.py", line 9, in <module>
    print(checkout(product))
  File "app.py", line 6, in checkout
    return get_discount(product["price"])
KeyError: 'price'
```

## How to read it

Start from the bottom:

```text
KeyError: 'price'
```

This is the exception.

Then look at the frame above it:

```python
return get_discount(product["price"])
```

That expression tried to access a missing dictionary key.

## Key traceback concepts

A traceback shows a **call stack**.

Example:

```text
main()
  -> checkout()
      -> calculate()
          -> failure
```

The lowest application frame often contains the most immediate cause.

However, the **root cause** may still be earlier.

For example, a missing key could mean:

- input validation was skipped,
- an API response changed,
- a database column was renamed,
- a test fixture is incomplete.

---

# 6. Syntax Errors

Syntax errors happen before Python can execute the program.

Example:

```python
if age >= 18
    print("Adult")
```

Error:

```text
SyntaxError: expected ':'
```

Correct:

```python
if age >= 18:
    print("Adult")
```

## Common causes

- missing colon
- unmatched parentheses
- bad indentation
- unclosed string
- invalid assignment
- malformed f-string
- incorrect keyword placement

Example:

```python
print("Hello"
```

Possible error:

```text
SyntaxError: '(' was never closed
```

### Debugging tip

When Python points to a line, also inspect the **previous line**. Some syntax problems are detected one line after the actual mistake.

---

# 7. Runtime Exceptions

Runtime exceptions occur after Python starts executing.

Example:

```python
result = 10 / 0
```

Output:

```text
ZeroDivisionError: division by zero
```

Common runtime exceptions:

| Exception | Meaning |
|---|---|
| `NameError` | Name does not exist |
| `TypeError` | Wrong type or operation |
| `ValueError` | Right type, invalid value |
| `KeyError` | Missing dictionary key |
| `IndexError` | Invalid sequence index |
| `AttributeError` | Missing object attribute |
| `FileNotFoundError` | File does not exist |
| `PermissionError` | Permission denied |
| `ImportError` | Import failed |
| `ModuleNotFoundError` | Module unavailable |
| `ZeroDivisionError` | Division by zero |
| `TimeoutError` | Operation timed out |

---

# 8. Logical Bugs

Logical bugs are dangerous because the program may appear to work.

Example:

```python
def is_adult(age):
    return age > 18
```

For many systems, age `18` should count as adult.

Correct:

```python
def is_adult(age):
    return age >= 18
```

## How to debug logical bugs

Inspect:

- boundary values
- comparisons
- boolean expressions
- loop ranges
- indexes
- formulas
- units
- rounding
- timezone assumptions
- sorting direction
- default values

Boundary test:

```python
for age in [17, 18, 19]:
    print(age, is_adult(age))
```

---

# 9. Debugging with `print()`

`print()` is the simplest debugging tool.

Example:

```python
def calculate_discount(price, percentage):
    discount = price * percentage
    print("price:", price)
    print("percentage:", percentage)
    print("discount:", discount)
    return price - discount
```

This can quickly reveal incorrect state.

## Add context

Weak:

```python
print(value)
```

Better:

```python
print("value:", value)
```

Even better:

```python
print(f"DEBUG calculate_discount: price={price!r}, percentage={percentage!r}")
```

`!r` uses `repr()`, which makes values such as spaces and escape characters easier to notice.

Example:

```python
name = "Alice "
print(name)
print(repr(name))
```

Output:

```text
Alice
'Alice '
```

The second output reveals the trailing space.

## When `print()` is useful

- tiny scripts
- quick local debugging
- checking control flow
- checking values

## When not to rely on it

- production systems
- multithreaded applications
- large services
- applications requiring log levels
- systems needing timestamps and request IDs

Use `logging` instead.

---

# 10. Better Temporary Debug Output

## `repr()`

```python
value = "\n"
print(value)
print(repr(value))
```

`repr()` exposes hidden characters.

## `type()`

```python
value = "123"
print(type(value))
```

Output:

```text
<class 'str'>
```

## `id()`

Useful for object identity investigations:

```python
a = []
b = a

print(id(a))
print(id(b))
```

## `vars()`

Inspect an object's writable attributes:

```python
class User:
    def __init__(self):
        self.name = "Alice"
        self.age = 30

user = User()

print(vars(user))
```

Output:

```text
{'name': 'Alice', 'age': 30}
```

## `dir()`

Inspect available names:

```python
print(dir(user))
```

Useful when investigating an `AttributeError`.

## Pretty printing

```python
from pprint import pprint

data = {
    "user": {
        "name": "Alice",
        "roles": ["admin", "editor"]
    }
}

pprint(data)
```

---

# 11. Python Logging

Logging is a structured way to record what a program is doing.

```python
import logging

logging.basicConfig(level=logging.INFO)

logging.debug("Detailed debugging data")
logging.info("Application started")
logging.warning("Disk space is low")
logging.error("Operation failed")
logging.critical("System cannot continue")
```

## Log levels

| Level | Typical use |
|---|---|
| `DEBUG` | Detailed developer information |
| `INFO` | Normal important events |
| `WARNING` | Unexpected but recoverable situation |
| `ERROR` | Operation failed |
| `CRITICAL` | Serious system-wide failure |

## Recommended logger pattern

```python
import logging

logger = logging.getLogger(__name__)

def process_order(order_id):
    logger.info("Processing order %s", order_id)
```

Prefer logger formatting placeholders:

```python
logger.debug("User id=%s status=%s", user_id, status)
```

rather than eagerly building debug strings.

## Log exceptions with traceback

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    logger.exception("Calculation failed")
```

`logger.exception()` should normally be called inside an exception handler.

## Do not log secrets

Never log:

- passwords
- API keys
- access tokens
- session cookies
- private keys
- full payment card numbers
- sensitive personal data unless explicitly safe and necessary

Bad:

```python
logger.debug("Login payload: %s", payload)
```

if `payload` includes a password.

Better:

```python
logger.debug("Login attempt for username=%s", username)
```

---

# 12. Assertions

Assertions document conditions that should always be true during correct execution.

```python
def calculate_average(total, count):
    assert count > 0, "count must be positive"
    return total / count
```

If:

```python
calculate_average(100, 0)
```

you get:

```text
AssertionError: count must be positive
```

## Assertions are not input validation

Do not use:

```python
assert user_has_permission(user)
```

for security-sensitive validation.

Python assertions can be disabled with optimization options.

Use explicit validation:

```python
if not user_has_permission(user):
    raise PermissionError("Access denied")
```

Use assertions mainly for:

- internal invariants
- developer assumptions
- impossible states
- debugging internal logic

---

# 13. The Built-in `breakpoint()` Function

`breakpoint()` is Python's standard, source-level way to pause a running program and hand control to the configured debugger.

## 13.1 What it does

The simplest use is:

```python
breakpoint()
```

With Python's default configuration, execution pauses and you enter `pdb`.

Example:

```python
def calculate_total(items):
    total = 0

    for item in items:
        breakpoint()
        total += item["price"] * item["quantity"]

    return total
```

When execution reaches the breakpoint, you can inspect the current stack frame:

```text
(Pdb) item
(Pdb) total
(Pdb) type(item)
(Pdb) where
```

The program is paused at its real runtime state, so this is often more useful than adding many temporary `print()` calls.

## 13.2 How it works

Conceptually, `breakpoint()` delegates to Python's breakpoint hook. The default hook starts the built-in debugger.

This gives tools and environments a standard integration point instead of requiring every project to hard-code:

```python
import pdb
pdb.set_trace()
```

## 13.3 Inputs and return behavior

Most application code calls it with no arguments:

```python
breakpoint()
```

Arguments, when supplied, are forwarded to the configured breakpoint hook. Do not design normal application logic around a value returned from `breakpoint()`; its purpose is debugging control, not business computation.

## 13.4 `PYTHONBREAKPOINT`

The `PYTHONBREAKPOINT` environment variable can change breakpoint behavior.

A particularly useful setting is:

```bash
PYTHONBREAKPOINT=0
```

This disables `breakpoint()` calls for that process.

That can be useful when temporary breakpoints accidentally remain in code, but it is still better to remove development-only breakpoints before committing or deploying.

## 13.5 When to use it

Use `breakpoint()` when:

- you know approximately where state becomes wrong,
- the bug depends on runtime values,
- stepping through control flow is easier than printing many values,
- you need to inspect locals, the call stack, or object state.

Avoid depending on interactive breakpoints in unattended production processes, background workers, or services where pausing execution could block real traffic.

## 13.6 Common mistake

Do not stop only on the line that crashes and immediately patch the value.

Ask:

```text
Why did this value become wrong?
Where was it last correct?
Which caller supplied it?
```

The breakpoint helps you collect evidence; it does not replace root-cause analysis.

---
# 14. The `pdb` Debugger

`pdb` is Python's built-in debugger.

## Starting a program under `pdb`

```bash
python -m pdb app.py
```

## Important commands

| Command | Meaning |
|---|---|
| `l` / `list` | Show nearby source code |
| `n` / `next` | Execute next line in current function |
| `s` / `step` | Step into a function |
| `c` / `continue` | Continue execution |
| `p expr` | Print expression |
| `pp expr` | Pretty-print expression |
| `w` / `where` | Show call stack |
| `u` / `up` | Move up stack |
| `d` / `down` | Move down stack |
| `b` | Show/set breakpoint |
| `cl` | Clear breakpoint |
| `r` / `return` | Run until function returns |
| `q` / `quit` | Exit debugger |
| `h` / `help` | Show help |

## Example

```python
def divide(a, b):
    result = a / b
    return result

x = 10
y = 2

breakpoint()
print(divide(x, y))
```

At the debugger:

```text
(Pdb) p x
10

(Pdb) p y
2

(Pdb) s
```

## Step vs next

Suppose:

```python
result = calculate_total(items)
```

`next` executes the function call without entering its internal lines.

`step` enters `calculate_total()`.

Use `step` when you suspect the called function.

Use `next` when you trust it and want to stay in the current function.

---

# 15. Post-Mortem Debugging

**Post-mortem debugging** means inspecting the program after an exception has already occurred, while the traceback and failing stack frames are still available.

This is different from starting a program under a debugger from the beginning.

## 15.1 Basic pattern

```python
import pdb

try:
    run_application()
except Exception:
    pdb.post_mortem()
```

When `run_application()` raises an exception, `pdb.post_mortem()` opens an interactive debugger at the traceback so you can inspect the failure.

Useful commands include:

```text
where
up
down
p variable_name
pp complex_object
```

## 15.2 Why post-mortem debugging is useful

Suppose a function fails only for one unusual record. Instead of guessing what happened, post-mortem debugging lets you inspect:

- the exact local variables at failure,
- the call stack,
- function arguments,
- objects referenced by the failing frame,
- caller frames that may reveal where the bad value originated.

## 15.3 pytest post-mortem debugging

For test failures:

```bash
pytest --pdb
```

pytest runs the tests normally and opens a debugger when a test fails.

To start tracing at the beginning of each test instead:

```bash
pytest --trace
```

These solve different problems:

| Command | Behavior |
|---|---|
| `pytest --pdb` | Enter debugger on failure |
| `pytest --trace` | Enter debugger at the start of test execution |

## 15.4 Starting under `pdb` is not post-mortem

This command:

```bash
python -m pdb app.py
```

starts `app.py` under the debugger. It is useful, but it is **interactive debugging from program start**, not post-mortem debugging.

## 15.5 When not to use it

Do not rely on interactive post-mortem debugging as your only production strategy. Production processes may restart, run without a terminal, or contain sensitive data.

For production failures, prefer safely collected:

- exception logs,
- request/correlation IDs,
- sanitized context,
- metrics and traces,
- crash diagnostics,
- a reproduction in a controlled environment.

---
# 16. Debugging in VS Code

VS Code supports breakpoints, variable inspection, stack inspection, conditional breakpoints, watch expressions, and debug consoles.

Typical workflow:

1. Open the Python file.
2. Click beside a line number to add a breakpoint.
3. Open **Run and Debug**.
4. Start the Python debugger.
5. Trigger the code path.
6. Inspect:
   - Variables
   - Watch
   - Call Stack
   - Breakpoints
7. Step through execution.

## Conditional breakpoint

Instead of breaking for every loop iteration, break only when:

```text
user_id == 500
```

This is useful for data-dependent bugs.

## Logpoints

A logpoint prints information without changing application source code.

Conceptually:

```text
user_id={user_id}, total={total}
```

Use this when repeatedly stopping would be inconvenient.

## Debug configuration concept

Projects may use a `.vscode/launch.json` configuration.

Example:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Debug current Python file",
      "type": "debugpy",
      "request": "launch",
      "program": "${file}",
      "console": "integratedTerminal"
    }
  ]
}
```

Exact available options depend on the installed Python debugger extension and project setup.

---

# 17. Debugging in PyCharm

PyCharm has an integrated Python debugger, so you can pause execution without adding debug statements to the source.

## 17.1 Basic workflow

1. Open the Python file or test.
2. Click in the gutter to set a breakpoint.
3. Start the target with **Debug** rather than **Run**.
4. Reproduce the code path.
5. When execution pauses, inspect variables and the call stack.
6. Step through the smallest suspicious area.
7. Evaluate expressions when you need to test a hypothesis.
8. Resume execution and verify the result.

## 17.2 Controls you should learn

| Control | Purpose |
|---|---|
| Resume | Continue until the next breakpoint or program end |
| Step Over | Execute the current line without entering called functions |
| Step Into | Enter a function called on the current line |
| Step Out | Finish the current function and return to its caller |
| Run to Cursor | Continue directly to a selected source line |
| Evaluate Expression | Evaluate an expression in the paused context |

## 17.3 Watches and inline values

A **watch** is useful when the same expression matters across several steps.

For example:

```python
order.total - order.discount
```

Instead of repeatedly typing the expression, add it as a watch and observe how it changes.

Inline debugger values are convenient, but always confirm that you are looking at the correct stack frame when several functions contain similarly named variables.

## 17.4 Exception breakpoints

An exception breakpoint can pause execution when a chosen exception is raised.

This is valuable when:

- an exception is caught later and normally hidden,
- the traceback is transformed by a framework,
- you want to stop at the original raise point.

For a broad exception such as `Exception`, expect many pauses. Narrow the exception type when possible.

## 17.5 Debugging tests

Run a specific failing test under the debugger before debugging the entire suite.

Typical strategy:

```text
reproduce failing test
→ debug only that test
→ inspect first incorrect state
→ fix root cause
→ run related tests
→ run full suite
```

## 17.6 Remote and alternate interpreters

PyCharm can also debug code that uses non-local interpreters in supported configurations. The important debugging rule is to verify that the interpreter and source files being debugged are the same ones you think are running.

Common mismatches include:

- local source but remote runtime,
- wrong virtual environment,
- stale container image,
- different dependency versions,
- source path mapping problems.

---
# 18. Debugging Functions

A function bug often involves:

- wrong arguments
- incorrect defaults
- wrong return value
- accidental mutation
- hidden global dependency
- early return
- missing return

Example:

```python
def get_discount(price):
    discount = price * 0.10
```

Then:

```python
result = get_discount(100)
print(result)
```

Output:

```text
None
```

Why?

Because a Python function without an explicit return statement returns `None`.

Correct:

```python
def get_discount(price):
    discount = price * 0.10
    return discount
```

---

# 19. Debugging Variables and Scope

Python uses scope rules commonly summarized as LEGB:

- Local
- Enclosing
- Global
- Built-in

Example:

```python
count = 10

def show():
    count = 5
    print(count)

show()
print(count)
```

Output:

```text
5
10
```

The local `count` is different from the global `count`.

## `UnboundLocalError`

```python
count = 10

def increase():
    count += 1
    return count
```

Python sees an assignment to `count`, so it treats `count` as local.

Correct, if global mutation is truly intended:

```python
count = 10

def increase():
    global count
    count += 1
    return count
```

But a cleaner design is often:

```python
def increase(count):
    return count + 1

count = increase(count)
```

---

# 20. Debugging Collections

## List index problems

```python
values = [10, 20, 30]
print(values[3])
```

Output:

```text
IndexError: list index out of range
```

Valid indexes are `0`, `1`, and `2`.

## Dictionary key problems

```python
user = {"name": "Alice"}
print(user["email"])
```

Output:

```text
KeyError: 'email'
```

Possible fix when missing email is acceptable:

```python
email = user.get("email")
```

Possible fix when email is required:

```python
if "email" not in user:
    raise ValueError("User email is required")
```

Do not blindly use `.get()` everywhere. It may hide invalid data.

---

# 21. Debugging Strings

Common string bugs include:

- leading/trailing spaces
- unexpected newline characters
- case differences
- Unicode differences
- wrong encoding
- invisible characters

Example:

```python
username = "admin "
print(username == "admin")
```

Output:

```text
False
```

Inspect with:

```python
print(repr(username))
```

Output:

```text
'admin '
```

Normalize only when appropriate:

```python
username = username.strip()
```

Do not strip data where spaces are meaningful.

---

# 22. Debugging Numeric Code

## Integer vs floating-point behavior

```python
print(0.1 + 0.2)
```

Often outputs:

```text
0.30000000000000004
```

This is normal binary floating-point behavior.

For money, consider decimal arithmetic:

```python
from decimal import Decimal

total = Decimal("0.1") + Decimal("0.2")
print(total)
```

Output:

```text
0.3
```

## Integer division

```python
print(7 / 2)
print(7 // 2)
```

Output:

```text
3.5
3
```

## Debug unit mismatches

Example:

```python
timeout_ms = 5000
time.sleep(timeout_ms)
```

This sleeps for 5,000 **seconds**, not milliseconds.

Correct:

```python
time.sleep(timeout_ms / 1000)
```

Always include units in variable names when ambiguity exists.

---

# 23. Debugging Conditions

Common bugs:

```python
if age > 18:
```

instead of:

```python
if age >= 18:
```

## Wrong boolean logic

Bug:

```python
if role != "admin" or role != "manager":
    print("Denied")
```

This condition is always true.

Correct:

```python
if role != "admin" and role != "manager":
    print("Denied")
```

Cleaner:

```python
if role not in {"admin", "manager"}:
    print("Denied")
```

## Truthiness surprises

These values are falsy:

```python
False
None
0
0.0
""
[]
{}
set()
```

Do not confuse:

```python
if not value:
```

with:

```python
if value is None:
```

If `0` is valid data, `if not value` may be wrong.

---

# 24. Debugging Loops

## Off-by-one errors

```python
for i in range(1, 5):
    print(i)
```

Output:

```text
1
2
3
4
```

`range()` excludes the stop value.

## Accidental infinite loop

```python
x = 1

while x < 10:
    print(x)
```

`x` never changes.

Correct:

```python
while x < 10:
    print(x)
    x += 1
```

## Use `enumerate()`

Instead of:

```python
for i in range(len(items)):
    print(i, items[i])
```

prefer:

```python
for i, item in enumerate(items):
    print(i, item)
```

This reduces index-related bugs.

---

# 25. Debugging Comprehensions

Dense comprehensions are harder to debug.

Example:

```python
result = [x * 2 for x in values if x > 10]
```

When debugging, temporarily expand it:

```python
result = []

for x in values:
    print("x:", x)

    if x > 10:
        doubled = x * 2
        print("doubled:", doubled)
        result.append(doubled)
```

Once correct, you can return to the comprehension.

Readable code is easier to debug.

---

# 26. Debugging File Handling

Example:

```python
with open("config.json") as f:
    data = f.read()
```

Possible errors:

- wrong current directory
- wrong filename
- missing permission
- wrong encoding
- file locked by another process
- malformed contents

Inspect:

```python
from pathlib import Path

path = Path("config.json")

print("cwd:", Path.cwd())
print("path:", path.resolve())
print("exists:", path.exists())
print("is_file:", path.is_file())
```

Use explicit encoding for text files:

```python
with open("config.json", encoding="utf-8") as f:
    data = f.read()
```

---

# 27. Debugging Paths

Relative path bugs are extremely common.

```python
Path("data/input.csv")
```

is relative to the **current working directory**, not automatically the script directory.

Inspect:

```python
from pathlib import Path

print("Current working directory:", Path.cwd())
print("Script directory:", Path(__file__).resolve().parent)
```

Robust project-relative example:

```python
BASE_DIR = Path(__file__).resolve().parent
CONFIG_PATH = BASE_DIR / "config" / "settings.json"
```

---

# 28. Debugging JSON

Example:

```python
import json

text = '{"name": "Alice",}'
data = json.loads(text)
```

The trailing comma makes the JSON invalid.

Catch decoding errors during investigation:

```python
try:
    data = json.loads(text)
except json.JSONDecodeError as exc:
    print("message:", exc.msg)
    print("line:", exc.lineno)
    print("column:", exc.colno)
```

## JSON type surprises

JSON:

```json
{
  "active": true,
  "count": null
}
```

becomes:

```python
{
    "active": True,
    "count": None
}
```

Always inspect external data rather than assuming its shape.

---

# 29. Debugging CSV Data

CSV files may contain:

- different delimiters
- quoted commas
- empty fields
- duplicate headers
- BOM characters
- mixed encodings
- inconsistent row lengths

Prefer the `csv` module over manual `split(",")`.

```python
import csv

with open("users.csv", newline="", encoding="utf-8") as f:
    reader = csv.DictReader(f)

    for row_number, row in enumerate(reader, start=2):
        print(row_number, row)
```

The row number helps locate bad source data.

---

# 30. Debugging Dates and Time

Date/time bugs commonly involve:

- timezone confusion
- naive vs aware datetimes
- daylight-saving transitions
- formatting
- locale assumptions
- milliseconds vs seconds

Example:

```python
from datetime import datetime

date_text = "2026-08-17"

value = datetime.strptime(date_text, "%Y-%m-%d")
print(value)
```

When parsing fails, compare the input exactly with the format.

Use:

```python
print(repr(date_text))
```

to catch hidden spaces.

## Timezone awareness

For systems spanning regions, prefer timezone-aware datetimes.

```python
from datetime import datetime, timezone

now = datetime.now(timezone.utc)
```

---

# 31. Debugging Exceptions Properly

Bad:

```python
try:
    process()
except:
    pass
```

This hides bugs.

Also problematic:

```python
try:
    process()
except Exception:
    print("Something went wrong")
```

because the traceback may be lost.

Better:

```python
try:
    process()
except ValueError as exc:
    logger.exception("Invalid input: %s", exc)
    raise
```

## Catch the narrowest useful exception

Prefer:

```python
except FileNotFoundError:
```

over:

```python
except Exception:
```

when you only expect a missing file.

## Preserve exception chains

```python
try:
    load_config()
except OSError as exc:
    raise RuntimeError("Unable to load application configuration") from exc
```

This preserves the original cause.

---

# 32. Custom Exceptions

Custom exceptions make domain failures clearer.

```python
class InsufficientBalanceError(Exception):
    pass
```

Use:

```python
def withdraw(balance, amount):
    if amount > balance:
        raise InsufficientBalanceError(
            f"Cannot withdraw {amount}; balance is {balance}"
        )

    return balance - amount
```

This is clearer than raising a generic `Exception`.

---

# 33. Debugging Object-Oriented Python

Common OOP bugs include:

- wrong `self`
- mutable class attributes
- missing superclass initialization
- method override problems
- property side effects
- incorrect `__eq__`
- inheritance confusion

## Mutable class attribute bug

```python
class Cart:
    items = []

    def add(self, item):
        self.items.append(item)
```

All instances share the same list.

```python
a = Cart()
b = Cart()

a.add("Book")

print(b.items)
```

Output:

```text
['Book']
```

Correct:

```python
class Cart:
    def __init__(self):
        self.items = []

    def add(self, item):
        self.items.append(item)
```

---

# 34. Debugging Imports

Common errors:

```text
ModuleNotFoundError
ImportError
circular import
```

## Confirm the interpreter

```bash
python -c "import sys; print(sys.executable)"
```

## Confirm import path

```python
import sys
print(sys.path)
```

## Confirm where a package came from

```python
import requests
print(requests.__file__)
```

## Watch for filename shadowing

If your file is named:

```text
requests.py
```

then:

```python
import requests
```

may import your local file instead of the real package.

Similarly avoid names such as:

```text
json.py
random.py
typing.py
logging.py
email.py
```

when they unintentionally shadow standard-library modules.

---

# 35. Debugging Virtual Environments

A common problem:

> "I installed the package, but Python says it is missing."

Often `pip` and `python` point to different environments.

Check:

```bash
python -c "import sys; print(sys.executable)"
python -m pip --version
python -m pip list
```

Prefer:

```bash
python -m pip install package_name
```

because it uses the `pip` associated with that Python interpreter.

## Check virtual environment

```python
import sys

print(sys.prefix)
print(sys.base_prefix)
```

If they differ, you are usually running inside a virtual environment.

---

# 36. Debugging Package and Dependency Problems

Dependency failures are often environment failures disguised as code failures.

Typical symptoms include:

```text
ModuleNotFoundError
ImportError
AttributeError after an upgrade
unexpected keyword argument
version conflict warnings
works on one machine but not another
```

## 36.1 Verify which Python and pip you are using

```bash
python --version
python -c "import sys; print(sys.executable)"
python -m pip --version
```

Prefer:

```bash
python -m pip ...
```

over a bare `pip ...` when you need to be certain that pip belongs to the same interpreter.

## 36.2 Inspect installed packages

```bash
python -m pip list
python -m pip show requests
python -m pip check
```

`pip check` reports incompatible or missing requirements in the currently installed environment.

For a suspicious package, also inspect where Python imported it from:

```python
import requests

print(requests.__file__)
print(getattr(requests, "__version__", "version attribute unavailable"))
```

This can reveal that Python loaded a different installation than expected.

## 36.3 Reproduce in a clean virtual environment

A clean environment separates application problems from accumulated local state.

Example:

```bash
python -m venv .venv
```

Activate it, install only the project's declared dependencies, then rerun the failing case.

If the clean environment works, compare:

- package versions,
- Python version,
- platform/architecture,
- environment variables,
- optional extras,
- lock or requirements files.

## 36.4 Bugs after an upgrade

When a failure begins immediately after a dependency change:

1. Record the previously working and currently failing versions.
2. Read the exact exception and failing API call.
3. Check the dependency's official migration/release documentation.
4. Reproduce with a minimal example.
5. Decide whether to update your code, pin temporarily, or roll back.
6. Add a test for the affected integration.

Do not permanently freeze an old dependency only to avoid understanding the incompatibility.

## 36.5 Common mistake: editing the environment blindly

Repeatedly reinstalling random packages can destroy useful evidence.

Before changing packages, capture:

```bash
python --version
python -m pip list
python -m pip check
```

For reproducible projects, keep dependency declarations and lock/constraint files under version control.

---
# 37. Debugging Environment Variables

Example:

```python
import os

api_url = os.getenv("API_URL")
print(api_url)
```

If output is:

```text
None
```

the variable is missing from the current process environment.

For required variables:

```python
api_url = os.environ["API_URL"]
```

This raises a `KeyError` immediately if missing.

A clearer approach:

```python
api_url = os.getenv("API_URL")

if not api_url:
    raise RuntimeError("API_URL environment variable is required")
```

Never print secrets while debugging production.

---

# 38. Debugging HTTP Requests and APIs

When an API call fails, inspect:

- URL
- HTTP method
- query parameters
- headers
- request body
- authentication
- status code
- response headers
- response body
- timeout
- redirects

Example with `requests`:

```python
import requests

response = requests.get(
    "https://example.com/api/users",
    timeout=10,
)

print("status:", response.status_code)
print("headers:", response.headers)
print("body:", response.text[:500])
```

Then:

```python
response.raise_for_status()
```

## JSON debugging

Do not assume every response is JSON.

Bad:

```python
data = response.json()
```

without considering that a proxy or server may return HTML.

During debugging:

```python
print(response.headers.get("content-type"))
print(response.text[:500])
```

## Always use timeouts

Avoid:

```python
requests.get(url)
```

Prefer a reasonable timeout for your application.

---

# 39. Debugging Web Applications

For frameworks such as Flask, Django, FastAPI, or similar systems, trace one request from beginning to end:

```text
client
  -> web server
  -> routing
  -> middleware
  -> authentication
  -> handler/view
  -> service layer
  -> database/API
  -> response serialization
  -> client
```

Record useful context:

- request ID
- endpoint
- method
- user or account identifier, if safe
- status code
- duration
- important dependency failures

## Do not expose development debug pages publicly

Interactive development debuggers can expose sensitive code and application state.

Use them only in trusted development environments.

---

# 40. Debugging Database Code

When a query behaves incorrectly, inspect:

- SQL text
- parameters
- transaction state
- affected row count
- result shape
- database connection target
- isolation level
- commit/rollback behavior

Bad:

```python
query = f"SELECT * FROM users WHERE id = {user_id}"
```

Prefer parameterization:

```python
cursor.execute(
    "SELECT * FROM users WHERE id = %s",
    (user_id,),
)
```

Placeholder style depends on the database driver.

## Transaction bug example

```python
cursor.execute("UPDATE accounts SET balance = 0")
```

If the connection requires explicit commit and you forget:

```python
connection.commit()
```

the change may appear missing.

During debugging, verify:

```text
Which database?
Which schema?
Which transaction?
Was it committed?
```

---

# 41. Debugging Tests

A failing test is evidence.

Do not immediately change the assertion.

Ask:

- Is the implementation wrong?
- Is the test wrong?
- Is the fixture wrong?
- Is shared state leaking?
- Is the test order-dependent?
- Is time involved?
- Is randomness involved?
- Is an external service involved?

Example:

```python
def add(a, b):
    return a - b

def test_add():
    assert add(2, 3) == 5
```

The test correctly exposes the implementation bug.

---

# 42. Debugging with `pytest`

Useful patterns:

```bash
pytest
```

Verbose:

```bash
pytest -v
```

Run one file:

```bash
pytest tests/test_orders.py
```

Run one test:

```bash
pytest tests/test_orders.py::test_create_order
```

Stop after first failure:

```bash
pytest -x
```

Show local variables in tracebacks:

```bash
pytest -l
```

Enter debugger on failure:

```bash
pytest --pdb
```

Show captured output:

```bash
pytest -s
```

Be careful: disabling output capture can make large test suites noisy.

---

# 43. Debugging Mocking Problems

Mocks replace real collaborators during tests. A test can fail because production code is wrong, but it can also fail because the mock itself does not match reality.

## 43.1 Patch where the name is looked up

Suppose:

```python
# service.py
from payments import charge

def buy():
    return charge()
```

`service.py` now has its own reference named `charge`.

A test commonly patches:

```python
from unittest.mock import patch

with patch("service.charge"):
    ...
```

rather than blindly patching:

```python
patch("payments.charge")
```

The general rule is:

> Patch the name used by the code under test, not merely the module where the object was originally defined.

## 43.2 Verify the mock contract

Common mock-related bugs include:

- wrong return type,
- wrong exception type,
- missing attributes,
- async function mocked as a normal synchronous function,
- incorrect call arguments,
- incorrect call count,
- mock accepts behavior the real object would reject.

Useful checks include:

```python
mock_charge.assert_called_once()
mock_charge.assert_called_once_with(order_id=123)
```

## 43.3 Prefer interface-aware mocks

When practical, use specifications so a mock cannot silently invent attributes that the real object does not have.

Example:

```python
from unittest.mock import create_autospec

mock_service = create_autospec(PaymentService, instance=True)
```

This makes the mock more faithful to the real interface.

## 43.4 Async code

For async collaborators, use async-aware mocking.

```python
from unittest.mock import AsyncMock

client.fetch = AsyncMock(return_value={"status": "ok"})
```

If an async API is mocked with a normal value or normal `Mock`, the test may fail for reasons unrelated to production behavior.

## 43.5 Over-mocking

If every internal method is mocked, the test may only prove that mocks call other mocks.

Prefer mocks at boundaries such as:

- HTTP clients,
- payment gateways,
- email providers,
- time/clock abstractions,
- external storage,
- expensive infrastructure.

Use integration tests to verify important collaborations with real components.

## 43.6 Debugging checklist

When a mocked test behaves strangely, ask:

```text
Did I patch the correct namespace?
Does the mock return the same shape/type as the real object?
Should this be AsyncMock?
Did the code call it with the arguments I expected?
Am I mocking an internal detail instead of a boundary?
Would a small integration test expose a contract mismatch?
```

---
# 44. Debugging Type Problems

Python is dynamically typed, so type-related bugs may appear at runtime.

Example:

```python
price = "100"
quantity = 3

print(price * quantity)
```

Output:

```text
100100100
```

This is valid Python but probably wrong business logic.

Check:

```python
print(type(price))
print(type(quantity))
```

Convert deliberately:

```python
price = int(price)
```

## Type hints help prevention

```python
def total(price: float, quantity: int) -> float:
    return price * quantity
```

Static type checkers can identify many mistakes before runtime, but type hints do not enforce types by themselves.

---

# 45. Debugging Dataclasses

Example:

```python
from dataclasses import dataclass

@dataclass
class User:
    name: str
    age: int
```

Inspect easily:

```python
user = User("Alice", 30)
print(user)
```

Output:

```text
User(name='Alice', age=30)
```

## Mutable defaults

Avoid:

```python
@dataclass
class Team:
    members: list = []
```

Use:

```python
from dataclasses import dataclass, field

@dataclass
class Team:
    members: list = field(default_factory=list)
```

---

# 46. Debugging Decorators

Decorators can make stack traces harder to understand.

Example:

```python
def log_call(func):
    def wrapper(*args, **kwargs):
        print("Calling", func.__name__)
        return func(*args, **kwargs)
    return wrapper
```

Use `functools.wraps`:

```python
from functools import wraps

def log_call(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        print("Calling", func.__name__)
        return func(*args, **kwargs)

    return wrapper
```

This preserves metadata such as function names and helps debugging and introspection.

---

# 47. Debugging Generators and Iterators

Generators are lazy.

```python
def numbers():
    yield 1
    yield 2
    yield 3
```

Nothing inside executes until iteration starts.

```python
gen = numbers()
print(gen)
```

does not produce all values.

```python
print(list(gen))
```

does.

## Exhaustion bug

```python
gen = numbers()

print(list(gen))
print(list(gen))
```

Output:

```text
[1, 2, 3]
[]
```

A generator is normally consumed once.

---

# 48. Debugging Context Managers

Context managers control setup and cleanup.

```python
with open("file.txt") as f:
    data = f.read()
```

The file is closed automatically.

Custom context manager errors often involve:

- cleanup not running
- swallowed exceptions
- incorrect `__enter__`
- incorrect `__exit__`

Debug the lifecycle:

```text
enter
  -> body
  -> exit
```

and verify whether an exception occurred in the body.

---

# 49. Debugging Recursion

Recursive code can fail due to:

- missing base case
- base case never reached
- wrong recursive argument
- exponential repeated work

Bug:

```python
def countdown(n):
    print(n)
    countdown(n - 1)
```

There is no base case.

Correct:

```python
def countdown(n):
    if n <= 0:
        return

    print(n)
    countdown(n - 1)
```

If recursion is hard to understand, print or debug:

```python
print("n =", n)
```

on every call.

---

# 50. Debugging Async Python

Async bugs often involve:

- missing `await`
- blocking synchronous work
- forgotten tasks
- cancellation
- timeouts
- event-loop lifecycle
- exceptions inside tasks

Example bug:

```python
async def main():
    result = fetch_data()
    print(result)
```

If `fetch_data()` is async, `result` may be a coroutine object.

Correct:

```python
async def main():
    result = await fetch_data()
    print(result)
```

## Forgotten task exception

If a task is created and never awaited or inspected, its exception may be easy to miss.

Prefer structured ownership of tasks:

```python
task = asyncio.create_task(worker())

try:
    result = await task
finally:
    ...
```

## Avoid blocking the event loop

Bad:

```python
async def handler():
    time.sleep(5)
```

This blocks the event loop.

Use an async-compatible operation when available:

```python
await asyncio.sleep(5)
```

---

# 51. Debugging Threads

Thread bugs can be intermittent.

Problems include:

- races
- deadlocks
- lost updates
- non-thread-safe libraries
- shared mutable state

Add thread names to logs:

```python
import logging

logging.basicConfig(
    format="%(asctime)s %(threadName)s %(levelname)s %(message)s"
)
```

Inspect:

- which thread changed state
- lock ownership
- operation order
- shared object lifetime

---

# 52. Debugging Multiprocessing

Multiprocessing introduces separate processes and usually separate memory.

Common problems:

- code works in one process but not child processes
- object cannot be pickled
- missing `if __name__ == "__main__":`
- child exception not surfaced clearly
- duplicated initialization
- file/socket sharing issues

Typical pattern:

```python
from multiprocessing import Process

def worker():
    print("Working")

if __name__ == "__main__":
    process = Process(target=worker)
    process.start()
    process.join()
```

The `__main__` guard is especially important on platforms that start new interpreter processes rather than forking the parent state.

---

# 53. Debugging Race Conditions

A race condition occurs when output depends on execution timing.

Example concept:

```python
counter = counter + 1
```

This is not conceptually one indivisible operation across arbitrary concurrent access.

If multiple threads or processes modify shared state, use appropriate synchronization or redesign to reduce sharing.

Useful techniques:

- locks
- queues
- immutable messages
- single-writer design
- database transactions
- atomic operations provided by the chosen system

Race conditions are often exposed by:

- higher concurrency
- slower machines
- added latency
- repeated tests

---

# 54. Debugging Performance Problems

A performance bug means the program may be functionally correct but does not meet its latency, throughput, CPU, memory, or responsiveness requirements.

Do not optimize based only on intuition. First identify **where the time goes**.

## 54.1 Define the symptom precisely

Bad description:

```text
The API is slow.
```

Better:

```text
GET /orders/123
p50: 120 ms
p95: 2.8 s
slow only when order has > 500 line items
```

Useful questions:

- Is the delay CPU time, waiting time, or both?
- Does it affect one input size or every request?
- Is it Python code, database work, network I/O, filesystem I/O, serialization, locking, or another service?
- Is the function slow once, or simply called far too many times?
- Did performance change after a deployment or dependency update?

## 54.2 Measure a focused operation

For elapsed wall-clock time:

```python
from time import perf_counter

start = perf_counter()

do_work()

elapsed = perf_counter() - start

print(f"Elapsed: {elapsed:.4f}s")
```

`perf_counter()` is appropriate for measuring elapsed durations.

For tiny isolated expressions, use `timeit` instead of hand-written one-shot timing.

## 54.3 Watch for I/O disguised as Python slowness

Example:

```python
for user in users:
    load_orders_from_database(user.id)
```

The loop itself may be cheap while the database call dominates total time.

Measure external dependencies separately when possible.

## 54.4 Scale matters

An algorithm that is fast for 100 records may be unusable for 1,000,000.

Test realistic:

- input sizes,
- concurrency,
- payload sizes,
- database row counts,
- network conditions.

A microbenchmark cannot replace an application-level benchmark.

## 54.5 After measurement

Once a hotspot is proven:

1. create a reproducible benchmark,
2. change one bottleneck,
3. measure again,
4. verify correctness,
5. record the before/after result.

---
# 55. Profiling CPU Usage

A profiler answers a different question from a debugger.

A debugger asks:

> What state and control flow caused this behavior?

A CPU profiler asks:

> Which functions consumed execution time, and how often were they called?

## 55.1 `cProfile`

Python includes the deterministic profiler `cProfile`.

Run a script:

```bash
python -m cProfile app.py
```

Sort by cumulative time:

```bash
python -m cProfile -s cumulative app.py
```

Save profiling data for later analysis:

```bash
python -m cProfile -o profile.stats app.py
```

Then inspect it programmatically:

```python
import pstats

stats = pstats.Stats("profile.stats")
stats.sort_stats("cumulative")
stats.print_stats(20)
```

## 55.2 Important columns

Profiler output commonly includes concepts such as:

| Field | Meaning |
|---|---|
| call count | How many calls occurred |
| total/internal time | Time spent in the function body, excluding subcalls |
| cumulative time | Time in the function plus functions it called |

A tiny function called millions of times can matter more than one large-looking function.

## 55.3 Profile representative work

Do not profile only application startup if the real problem occurs during a large import, API request, or data transformation.

Profile the workload that reproduces the slowdown.

## 55.4 Profiling changes execution

Instrumentation adds overhead. Treat profiler numbers as diagnostic evidence, not perfect production timing.

For production-like profiling, consider lower-overhead sampling profilers where appropriate, and validate any tool's operational impact before using it on critical systems.

## 55.5 Optimization rule

Do not optimize a function merely because it looks complex.

Optimize only after evidence shows:

```text
important to users
+ measurably expensive
+ safely improvable
```

---
# 56. Debugging Memory Problems

Memory problems can appear as:

- steadily increasing process memory,
- sudden spikes,
- large temporary allocations,
- caches that never evict,
- unexpectedly retained objects,
- `MemoryError`,
- swapping and severe slowdown.

First distinguish **Python allocations** from total operating-system process memory. Native extensions and external libraries can allocate memory that `tracemalloc` does not fully explain.

## 56.1 Measure current and peak traced allocations

Python's built-in `tracemalloc` tracks Python memory allocations.

```python
import tracemalloc

tracemalloc.start()

data = [str(i) for i in range(100_000)]

current, peak = tracemalloc.get_traced_memory()

print("Current:", current)
print("Peak:", peak)

tracemalloc.stop()
```

The values are bytes.

## 56.2 Start tracing early enough

`tracemalloc` cannot explain allocations that happened before tracing started.

If startup allocations matter, enable tracing near process start or use the relevant interpreter option/environment configuration for your runtime.

## 56.3 Take snapshots

```python
import tracemalloc

tracemalloc.start()

before = tracemalloc.take_snapshot()

do_work()

after = tracemalloc.take_snapshot()

for stat in after.compare_to(before, "lineno")[:10]:
    print(stat)
```

This helps answer:

```text
Which source locations increased allocations?
How much?
How many blocks?
```

## 56.4 Do not confuse high memory with a leak

An application may legitimately hold a large dataset.

A leak-like pattern usually means memory remains retained after the application no longer needs the data, or grows without an intended bound.

Measure memory over repeated operations, not just one snapshot.

---
# 57. Debugging Memory Leaks

In garbage-collected Python, a "memory leak" often means objects remain **reachable** even though the application no longer needs them. Native extensions can also have genuine lower-level leaks.

Example of unbounded retention:

```python
cache = []

def process(item):
    cache.append(item)
```

If `cache` grows forever, every processed item remains reachable.

## 57.1 Common retention sources

Investigate:

- unbounded global lists/dictionaries,
- caches without size or expiration policies,
- queues that producers fill faster than consumers drain,
- event listeners/callback registries,
- closures retaining large objects,
- long-lived tasks,
- reference cycles with unusual finalization behavior,
- native extensions,
- ORM/session identity maps,
- accidental copies of large datasets.

## 57.2 Snapshot comparison

```python
import tracemalloc

tracemalloc.start()

before = tracemalloc.take_snapshot()

for _ in range(100):
    do_work()

after = tracemalloc.take_snapshot()

for stat in after.compare_to(before, "lineno")[:10]:
    print(stat)
```

Repeating the workload is important: a leak often becomes obvious as a trend.

## 57.3 Prove that the growth is retained

A useful experiment is:

```text
measure baseline
→ perform operation many times
→ allow normal cleanup
→ measure again
→ repeat
```

If the retained amount keeps increasing roughly with each cycle, investigate what references remain.

## 57.4 Garbage collection is not a universal fix

Calling:

```python
import gc
gc.collect()
```

may help an experiment determine whether collectable objects are pending, but repeatedly forcing collection is not a proper fix for an unbounded cache or retained reference.

## 57.5 Real-world example

A worker processes uploaded files. Memory grows by 20 MB per job.

Investigation shows every parsed document is stored in:

```python
processed_documents.append(document)
```

The code was originally added for debugging and never removed.

The correct fix is to remove or bound the retention, not to increase the machine's memory limit.

---
# 58. Debugging Subprocesses

Example:

```python
import subprocess

result = subprocess.run(
    ["python", "--version"],
    capture_output=True,
    text=True,
)

print("returncode:", result.returncode)
print("stdout:", result.stdout)
print("stderr:", result.stderr)
```

Check:

- executable path
- current directory
- environment
- exit code
- stdout
- stderr
- timeout

For required success:

```python
subprocess.run(command, check=True)
```

Then non-zero exit status raises an exception.

---

# 59. Debugging Unicode and Encoding

Typical errors:

```text
UnicodeDecodeError
UnicodeEncodeError
```

Always determine:

- source encoding
- destination encoding
- actual bytes
- expected text

Example:

```python
text = "café"

encoded = text.encode("utf-8")
decoded = encoded.decode("utf-8")

print(decoded)
```

Inspect bytes:

```python
print(encoded)
```

Do not "fix" encoding bugs by randomly trying encodings until one does not crash. That may silently corrupt data.

---

# 60. Debugging Regular Expressions

Regex bugs are often caused by:

- wrong escaping
- greedy matching
- unexpected anchors
- multiline behavior
- Unicode assumptions

Example:

```python
import re

pattern = r"\d+"

text = "Order 123"

match = re.search(pattern, text)

print(match.group() if match else None)
```

Output:

```text
123
```

Use raw strings for regex patterns when practical:

```python
r"\d+"
```

instead of:

```python
"\\d+"
```

Break large regex patterns into smaller tested pieces.

---

# 61. Debugging Configuration Problems

Configuration problems often masquerade as code bugs.

Check:

- config file loaded?
- expected environment selected?
- correct database?
- correct URL?
- correct feature flag?
- config type correct?
- fallback/default unexpectedly used?

Bad:

```python
DEBUG = os.getenv("DEBUG", False)
```

If environment contains:

```text
DEBUG=false
```

the Python value is the string `"false"`, which is truthy.

Better:

```python
DEBUG = os.getenv("DEBUG", "").lower() in {"1", "true", "yes", "on"}
```

---

# 62. Debugging CLI Programs

CLI programs have multiple data sources:

```text
shell
  -> arguments
  -> parser
  -> validation
  -> command handler
  -> output
  -> exit status
```

Inspect the parsed arguments.

With `argparse`:

```python
args = parser.parse_args()
print(args)
```

Test:

- missing arguments
- invalid values
- quoted strings
- spaces
- paths
- stdin
- exit codes

Use meaningful exit codes for automation.

---

# 63. Debugging Dockerized Python

A program that works locally but fails in Docker may differ in:

- Python version
- installed dependencies
- OS libraries
- environment variables
- file paths
- permissions
- DNS
- network routing
- working directory
- mounted volumes
- user identity

Useful checks inside the container:

```bash
python --version
python -m pip list
pwd
ls -la
env
```

Inspect logs:

```bash
docker logs <container>
```

Open a shell when appropriate:

```bash
docker exec -it <container> sh
```

or if Bash is available:

```bash
docker exec -it <container> bash
```

Never assume `localhost` inside a container means the host machine.

---

# 64. Debugging CI/CD Failures

A test may pass locally and fail in CI due to:

- different Python version
- different dependency version
- clean filesystem
- missing environment variables
- timezone
- locale
- case-sensitive filesystem
- test order
- parallel execution
- unavailable external service

Compare environments explicitly.

Log:

```python
import os
import platform
import sys

print("Python:", sys.version)
print("Executable:", sys.executable)
print("Platform:", platform.platform())
print("Working directory:", os.getcwd())
```

Do not print secrets from CI environment variables.

---

# 65. Remote Debugging

Remote debugging means the debugger UI and the Python process run in different environments.

Common scenarios:

- Docker containers,
- virtual machines,
- remote Linux servers,
- Kubernetes pods,
- development containers,
- cloud development environments.

## 65.1 `debugpy` concept

A common Python remote-debugging backend is `debugpy`.

A development-only pattern can listen for a debugger:

```python
import debugpy

debugpy.listen(("127.0.0.1", 5678))
print("Waiting for debugger...")
debugpy.wait_for_client()

run_application()
```

Then an IDE can attach to the listening process.

Do not copy this pattern blindly into production startup code.

## 65.2 VS Code attach example

A typical local attach configuration is:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Python: Attach",
      "type": "debugpy",
      "request": "attach",
      "connect": {
        "host": "127.0.0.1",
        "port": 5678
      }
    }
  ]
}
```

Exact networking and path behavior depends on whether Python runs locally, in Docker, through SSH, or in another remote environment.

## 65.3 Path mappings

If the runtime reports source paths different from your local workspace, the debugger may need path mappings.

Example concept:

```text
remote: /app/src
local:  C:\Projects\myapp\src
```

If breakpoints appear unverified, confirm:

- the runtime loaded the same source revision,
- local and remote paths map correctly,
- the process uses the expected interpreter,
- the debugger is attached to the correct process.

## 65.4 Security

A debugger can inspect variables and often execute code in the target process.

Therefore:

- bind to loopback when possible,
- prefer SSH tunnels or trusted private networks,
- do not expose a debug port directly to the public internet,
- remove temporary remote-debug startup code after diagnosis,
- avoid pausing production traffic unless the operational impact is understood.

For production diagnosis, logs, traces, metrics, profiling, and controlled reproductions are usually safer than an attached interactive debugger.

---
# 66. Production Debugging

Production debugging should prioritize observability and safety.

Useful evidence:

- structured logs
- exception tracking
- metrics
- traces
- request IDs
- deployment version
- feature flags
- database/query timing
- dependency health

## Correlation ID example

```python
logger.info(
    "request_completed request_id=%s user_id=%s status=%s duration_ms=%s",
    request_id,
    user_id,
    status_code,
    duration_ms,
)
```

A request ID lets you connect multiple log entries from the same request.

## Avoid "debugging by changing production randomly"

Prefer:

1. collect evidence
2. reproduce safely
3. create fix
4. test
5. deploy
6. monitor

---

# 67. Security-Safe Debugging

Debugging can accidentally expose confidential information.

Never casually include:

- passwords
- auth headers
- JWTs
- cookies
- API keys
- private keys
- database credentials
- unredacted customer records

Redact before logging.

Example:

```python
safe_headers = {
    key: ("***" if key.lower() == "authorization" else value)
    for key, value in headers.items()
}
```

Also avoid returning internal stack traces to untrusted users in production.

---

# 68. Reproducing Intermittent Bugs

Intermittent bugs need controlled experiments.

Record:

- timestamp
- input
- user/account
- request ID
- process/thread
- machine/container
- dependency response
- application version
- timing
- random seed if applicable

## Make randomness reproducible

```python
import random

random.seed(12345)
```

This helps reproduce random-dependent behavior.

Do not rely on fixed seeds in contexts where cryptographic randomness is required.

---

# 69. Reducing a Bug to a Minimal Reproduction

A minimal reproduction is the smallest program that still fails.

Original system:

```text
web app
+ database
+ queue
+ cache
+ external API
+ authentication
```

Maybe the bug can be reduced to:

```python
payload = {"amount": "10.5"}
total = payload["amount"] + 2
```

which immediately reveals:

```text
TypeError
```

Benefits:

- faster debugging
- easier reasoning
- easier bug reports
- easier testing
- easier collaboration

---

# 70. Binary Search Debugging

When a pipeline has many stages:

```text
A -> B -> C -> D -> E -> F
```

do not necessarily inspect A, then B, then C one by one.

Check the middle:

```text
A -> B -> C | D -> E -> F
```

If C is correct, the bug is later.

Then check E.

This is similar to binary search and can quickly narrow large systems.

Use it for:

- data pipelines
- request processing
- transformations
- multi-layer applications

---

# 71. Git Bisect for Regression Bugs

If a feature worked before and now fails, `git bisect` can help identify the commit that introduced the bug.

Conceptual workflow:

```bash
git bisect start
git bisect bad
git bisect good <known-good-commit>
```

Git checks out a midpoint commit.

You test it and mark:

```bash
git bisect good
```

or:

```bash
git bisect bad
```

Repeat until Git identifies the likely first bad commit.

Then finish:

```bash
git bisect reset
```

This is extremely effective when many commits occurred between working and broken versions.

---

# 72. Rubber Duck Debugging

Explain the problem step by step as if teaching another person:

```text
This function receives an order.
First it loads items.
Then it calculates tax.
Then it applies discount...
```

While explaining, you may notice:

> "Wait—the discount is being applied before tax, but our rule says after tax."

The "duck" does not need to solve the problem. Explaining forces you to make hidden assumptions explicit.

---

# 73. Debugging Real-World Scenarios

## Scenario 1: `NoneType` error

Error:

```text
AttributeError: 'NoneType' object has no attribute 'strip'
```

Code:

```python
name = get_name()
clean_name = name.strip()
```

Investigation:

```python
print(repr(name))
print(type(name))
```

If:

```text
None
<class 'NoneType'>
```

ask **why** `get_name()` returned `None`.

Possible fix if `None` is expected:

```python
if name is None:
    clean_name = ""
else:
    clean_name = name.strip()
```

Possible fix if `None` is invalid:

```python
if name is None:
    raise ValueError("Name is required")
```

Do not blindly write:

```python
clean_name = (name or "").strip()
```

unless converting every falsy value to an empty string matches the domain rules.

---

## Scenario 2: API returns HTTP 200 but code fails

Code:

```python
response = requests.get(url, timeout=10)
data = response.json()
print(data["user"]["email"])
```

Error:

```text
KeyError: 'user'
```

Debug:

```python
print(response.status_code)
print(response.headers.get("content-type"))
print(response.text[:1000])
```

Maybe the API returns:

```json
{
  "error": "account_not_found"
}
```

The transport succeeded, but the business request did not.

---

## Scenario 3: Works locally, fails on Linux server

Potential cause:

```python
open("Config.json")
```

Local case-insensitive filesystem may tolerate a file actually named:

```text
config.json
```

A case-sensitive filesystem may not.

Debug:

```python
from pathlib import Path

for path in Path(".").iterdir():
    print(path.name)
```

Fix the filename mismatch.

---

## Scenario 4: Wrong loop result

```python
numbers = [1, 2, 3, 4]

total = 0

for number in numbers:
    total = number

print(total)
```

Output:

```text
4
```

Expected:

```text
10
```

Bug:

```python
total = number
```

Correct:

```python
total += number
```

---

## Scenario 5: Shared mutable default argument

Bug:

```python
def add_item(item, items=[]):
    items.append(item)
    return items
```

Calls:

```python
print(add_item("A"))
print(add_item("B"))
```

Output:

```text
['A']
['A', 'B']
```

The default list is created once.

Correct:

```python
def add_item(item, items=None):
    if items is None:
        items = []

    items.append(item)
    return items
```

---

## Scenario 6: Function changes caller's list unexpectedly

```python
def prepare(items):
    items.sort()
    return items
```

`sort()` mutates the original list.

If mutation is not intended:

```python
def prepare(items):
    return sorted(items)
```

Debug object identity when needed:

```python
print(id(items))
```

---

## Scenario 7: `is` vs `==`

Wrong:

```python
if value is 1000:
    ...
```

Use equality for values:

```python
if value == 1000:
    ...
```

Use `is` mainly for identity checks such as:

```python
if value is None:
    ...
```

---

## Scenario 8: Default argument evaluated once

```python
from datetime import datetime

def create_record(created_at=datetime.now()):
    return created_at
```

The default time is created when the function definition executes, not every call.

Better:

```python
def create_record(created_at=None):
    if created_at is None:
        created_at = datetime.now()

    return created_at
```

---

## Scenario 9: Silent exception hides data loss

Bad:

```python
for file in files:
    try:
        upload(file)
    except Exception:
        pass
```

You may silently lose uploads.

Better:

```python
for file in files:
    try:
        upload(file)
    except UploadError:
        logger.exception("Upload failed for file=%s", file)
        failed_files.append(file)
```

---

## Scenario 10: SQL query returns unexpected row

Debug:

```text
database host
database name
schema
query
parameters
ordering
limit
transaction
```

A common logic mistake:

```sql
SELECT *
FROM orders
LIMIT 1;
```

without `ORDER BY`.

"First row" is not meaningful unless ordering is specified.

---

## Scenario 11: Pagination skips records

Suppose:

```python
page_size = 10
offset = page * page_size
```

If `page` starts at `1`, page 1 starts at offset 10 and skips the first 10 rows.

Correct:

```python
offset = (page - 1) * page_size
```

Test boundaries:

```text
page 1
page 2
last page
empty page
```

---

## Scenario 12: Production-only timeout

Local database:

```text
5 ms
```

Production database:

```text
3 seconds
```

The bug may be a hidden performance assumption.

Measure each stage:

```python
start = perf_counter()
result = load_data()
logger.info("load_data duration=%.3fs", perf_counter() - start)
```

Then determine whether the delay is:

- connection
- query
- serialization
- network
- application processing

---

# 74. Common Debugging Mistakes

## 1. Guessing before reading the traceback

Read the evidence first.

## 2. Changing many things at once

You lose causal knowledge.

## 3. Catching every exception

```python
except Exception:
    pass
```

can turn obvious bugs into silent corruption.

## 4. Fixing the symptom instead of the cause

Example:

```python
try:
    ...
except KeyError:
    return None
```

may hide malformed input.

## 5. Leaving debug prints everywhere

Use logging or remove temporary debug code.

## 6. Logging secrets

Never trade security for convenience.

## 7. Ignoring types

Always inspect unexpected values with:

```python
type(value)
repr(value)
```

## 8. Assuming external data is valid

Validate API, file, queue, form, and database inputs.

## 9. Debugging without a reproduction

A reproducible failing case is one of your strongest tools.

## 10. Believing the last changed line must be the bug

The last change is a clue, not proof.

---

# 75. Debugging Best Practices

1. Reproduce first.
2. Preserve the failing input.
3. Read the complete traceback.
4. Inspect types as well as values.
5. Use small experiments.
6. Reduce the problem.
7. Change one thing at a time.
8. Add useful context to logs.
9. Keep development and production behavior separate.
10. Use assertions for internal invariants, not security checks.
11. Write regression tests.
12. Use static analysis and type checking.
13. Format and lint code.
14. Keep dependencies reproducible.
15. Record environment information.
16. Use version control.
17. Prefer deterministic tests.
18. Keep functions small enough to reason about.
19. Avoid unnecessary shared mutable state.
20. Measure before optimizing.
21. Preserve original exceptions when wrapping.
22. Use correlation/request IDs in distributed systems.
23. Remove secrets from logs and bug reports.
24. Document strange fixes so they are not "mystery code."
25. Verify the fix against both normal and edge cases.

---

# 76. Bug Report Template

Use this format when reporting bugs.

```markdown
# Bug Title

## Summary

A short description of the problem.

## Expected Behavior

What should happen?

## Actual Behavior

What actually happens?

## Steps to Reproduce

1. ...
2. ...
3. ...

## Minimal Code Example

```python
...
```

## Error / Traceback

```text
...
```

## Input Data

```text
...
```

## Environment

- Python version:
- Operating system:
- Package versions:
- Runtime/container:
- Database:
- Browser/client, if relevant:

## Frequency

- Always
- Sometimes
- Once
- Unknown

## Last Known Working Version

...

## Recent Changes

...

## Investigation Already Done

...

## Sensitive Data Removed?

Yes / No
```

---

# 77. Debugging Checklist

## When Python crashes

- [ ] Read the full exception type.
- [ ] Read the full exception message.
- [ ] Read the entire traceback.
- [ ] Find the first relevant line in your own code.
- [ ] Inspect values involved.
- [ ] Inspect their types.
- [ ] Reproduce with the same input.
- [ ] Check boundary conditions.
- [ ] Check external data shape.
- [ ] Check environment and dependencies.

## When output is wrong

- [ ] Write expected vs actual values.
- [ ] Verify inputs.
- [ ] Check formulas.
- [ ] Check operators.
- [ ] Check comparison boundaries.
- [ ] Check boolean logic.
- [ ] Check ordering.
- [ ] Check indexes and ranges.
- [ ] Check mutation.
- [ ] Check default values.

## When it works locally but not elsewhere

- [ ] Compare Python versions.
- [ ] Compare package versions.
- [ ] Compare OS.
- [ ] Compare architecture.
- [ ] Compare environment variables.
- [ ] Compare file paths.
- [ ] Compare permissions.
- [ ] Compare current working directory.
- [ ] Compare database/API targets.
- [ ] Compare timezone and locale.

## Before closing a bug

- [ ] Root cause identified.
- [ ] Fix implemented.
- [ ] Original reproduction now passes.
- [ ] Regression test added.
- [ ] Related edge cases tested.
- [ ] Temporary debug code removed.
- [ ] Logs do not expose secrets.
- [ ] Documentation updated if needed.
- [ ] Deployment monitoring considered.

---

# 78. Python Debugging Toolkit Reference

## Built-in tools

### `print()`

Quickly inspect values.

```python
print(value)
```

### `repr()`

Reveal developer-friendly representation.

```python
print(repr(value))
```

### `type()`

Inspect runtime type.

```python
print(type(value))
```

### `dir()`

Inspect available names.

```python
print(dir(obj))
```

### `vars()`

Inspect object attribute dictionary when available.

```python
print(vars(obj))
```

### `breakpoint()`

Enter the configured debugger.

```python
breakpoint()
```

### `pdb`

Built-in debugger.

```bash
python -m pdb app.py
```

### `logging`

Structured diagnostic records.

```python
import logging
```

### `traceback`

Programmatic traceback utilities.

```python
import traceback

try:
    1 / 0
except Exception:
    traceback.print_exc()
```

### `inspect`

Runtime introspection.

```python
import inspect

print(inspect.signature(my_function))
```

### `dis`

Inspect Python bytecode when investigating advanced behavior.

```python
import dis

dis.dis(my_function)
```

### `timeit`

Measure small code snippets.

```bash
python -m timeit "sum(range(1000))"
```

### `cProfile`

CPU profiler.

```bash
python -m cProfile app.py
```

### `tracemalloc`

Track Python memory allocations.

```python
import tracemalloc
```

## External categories worth learning

Depending on your project, useful tool categories include:

- IDE debuggers
- test runners
- type checkers
- linters
- formatters
- exception monitoring
- application performance monitoring
- distributed tracing
- database query profilers
- memory profilers

The tool is secondary. The core skill remains gathering evidence and narrowing the problem systematically.

---

# 79. Learning Exercises

## Exercise 1: Find the type bug

```python
def total(price, quantity):
    return price * quantity

print(total("20", 3))
```

Expected business result:

```text
60
```

Actual Python output:

```text
202020
```

Tasks:

1. Inspect both argument types.
2. Explain why Python produced the output.
3. Fix the input conversion.
4. Add validation for invalid numeric text.

---

## Exercise 2: Fix the boundary bug

```python
def can_vote(age):
    return age > 18
```

Test:

```python
assert can_vote(18) is True
```

Find the incorrect comparison.

---

## Exercise 3: Find the shared-state bug

```python
def remember(value, history=[]):
    history.append(value)
    return history

print(remember("A"))
print(remember("B"))
```

Explain why the second output contains `"A"`.

---

## Exercise 4: Investigate a missing key

```python
payload = {
    "user": {
        "name": "Alice"
    }
}

print(payload["user"]["email"])
```

Create two valid fixes:

1. One where `email` is optional.
2. One where `email` is required.

---

## Exercise 5: Debug loop boundaries

```python
items = [10, 20, 30]

for i in range(1, len(items)):
    print(items[i])
```

Why is the first item skipped?

---

## Exercise 6: Debug mutation

```python
def normalize(values):
    values.sort()
    return values

original = [3, 1, 2]
normalized = normalize(original)

print(original)
```

If the caller expects `original` to remain unchanged, redesign the function.

---

## Exercise 7: Debug a file path

```python
with open("settings/config.json") as f:
    ...
```

Add diagnostics showing:

- current working directory
- absolute resolved path
- whether the file exists

---

## Exercise 8: Debug a swallowed exception

```python
try:
    important_operation()
except Exception:
    pass
```

Rewrite it so the failure is observable without exposing secrets.

---

## Exercise 9: Debug an async mistake

```python
async def main():
    data = fetch_data()
    print(data)
```

Assume `fetch_data` is async. Fix the code.

---

## Exercise 10: Create a regression test

Imagine a tax calculator previously failed for amount `0`.

Write a test that ensures this exact bug never returns.

---

# 80. Final Debugging Strategy

When you encounter a bug, remember this sequence:

```text
OBSERVE
  ↓
REPRODUCE
  ↓
REDUCE
  ↓
READ THE ERROR
  ↓
INSPECT STATE
  ↓
FORM A HYPOTHESIS
  ↓
TEST ONE THING
  ↓
LOCATE ROOT CAUSE
  ↓
FIX
  ↓
ADD REGRESSION TEST
  ↓
VERIFY
  ↓
MONITOR
```

A strong debugger does not need to know the answer immediately.

A strong debugger knows how to turn:

```text
"I have no idea why this is broken."
```

into:

```text
"I know exactly what evidence I need next."
```

That is the central skill behind professional debugging.

---

# Appendix A: Debugging Questions to Memorize

When stuck, ask these in order:

1. What exactly is failing?
2. What did I expect?
3. What actually happened?
4. Can I reproduce it?
5. What is the smallest input that reproduces it?
6. What is the exact traceback?
7. Which value is unexpected?
8. What is its type?
9. Where did that value come from?
10. When was it last correct?
11. What changed after that?
12. Is the problem code, data, configuration, environment, or dependency?
13. Can I prove my current hypothesis?
14. What test should fail before the fix?
15. What test should pass after the fix?

---

# Appendix B: Beginner Debugging Command Cheat Sheet

```bash
# Show Python version
python --version

# Show interpreter path
python -c "import sys; print(sys.executable)"

# Show package installer being used
python -m pip --version

# List installed packages
python -m pip list

# Show package details
python -m pip show <package>

# Check dependency compatibility
python -m pip check

# Start built-in debugger
python -m pdb app.py

# Profile CPU usage
python -m cProfile app.py

# Benchmark a small expression
python -m timeit "sum(range(1000))"

# Run tests
pytest

# Stop after first pytest failure
pytest -x

# Enter debugger on pytest failure
pytest --pdb
```

---

# Appendix C: Recommended Debugging Progression for Learners

## Beginner

Learn:

- tracebacks
- exception types
- `print()`
- `repr()`
- `type()`
- `breakpoint()`
- `pdb` basics
- VS Code/PyCharm breakpoints
- `try` / `except`
- simple tests

## Intermediate

Learn:

- logging
- pytest
- mocking
- type hints
- environment debugging
- dependency debugging
- API debugging
- database debugging
- profiling
- `tracemalloc`

## Advanced

Learn:

- concurrency debugging
- async debugging
- race conditions
- deadlocks
- remote debugging
- distributed tracing
- production observability
- profiling under realistic workloads
- memory-retention analysis
- regression isolation with `git bisect`
- incident debugging

---

# Appendix D: Golden Rule

> **Never ask only "How do I make the error disappear?"**

Ask:

> **"Why did the program reach this invalid state, and how can I make that state impossible or correctly handled?"**

That question leads from temporary patches to reliable software.

---

# Appendix E: Recommended Python Debugging Tools and Configuration

This appendix turns the concepts in the handbook into a practical toolchain. Tool behavior can change over time, so prefer the official documentation for your installed version when an option differs.

## E.1 Minimal beginner toolchain

A strong starter setup is:

```text
Python interpreter
+ VS Code or PyCharm
+ IDE debugger
+ pytest
+ logging
+ Git
```

Add static analysis, profiling, and observability as your projects become larger.

## E.2 VS Code: recommended extensions

For Python work in VS Code, install the official/current Python tooling offered by Microsoft, especially:

- **Python** — interpreter selection and Python development integration.
- **Python Debugger** — debugging through `debugpy`.
- **Pylance** — language analysis, navigation, and type-aware editor diagnostics.

Use the Extensions view and verify the publisher before installing similarly named extensions.

### Select the correct interpreter

Open the Command Palette and choose:

```text
Python: Select Interpreter
```

Then verify in the terminal:

```bash
python -c "import sys; print(sys.executable)"
python --version
```

The IDE interpreter and the terminal interpreter should match the environment you intend to debug.

### Create `.vscode/launch.json`

A simple current-file configuration:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Python: Current File",
      "type": "debugpy",
      "request": "launch",
      "program": "${file}",
      "console": "integratedTerminal"
    }
  ]
}
```

Use a project-specific entry point for web applications instead of always debugging the current file.

### Useful debugger features

Learn these in order:

```text
line breakpoint
→ conditional breakpoint
→ logpoint
→ Step Over
→ Step Into
→ Step Out
→ Call Stack
→ Watch
→ Debug Console
→ exception breakpoints
```

## E.3 PyCharm configuration

PyCharm already includes its debugger.

Recommended workflow:

1. Configure the project's Python interpreter.
2. Create or select the correct Run/Debug configuration.
3. Set a breakpoint.
4. Start with **Debug**.
5. Inspect Variables and Frames.
6. Add an exception breakpoint when you need the original raise location.
7. Debug one failing test before debugging the whole suite.

If a breakpoint never binds, verify the interpreter, source path, run configuration, and whether that code path actually executes.

## E.4 `pdb`

No third-party installation is required.

Start a script under `pdb`:

```bash
python -m pdb app.py
```

Common commands:

```text
l / list        show source
n / next        execute next line in current frame
s / step        step into
r / return      run until current function returns
c / continue    continue
w / where       show stack
u / up          move to caller frame
d / down        move toward newer frame
p expr          print expression
pp expr         pretty-print expression
q / quit        leave debugger
```

Inside source code, prefer:

```python
breakpoint()
```

over hard-coding debugger imports unless you specifically need a debugger API.

## E.5 pytest as a debugging tool

Install in your development environment:

```bash
python -m pip install pytest
```

Run all tests:

```bash
pytest
```

Run one file:

```bash
pytest tests/test_orders.py
```

Run one test by node ID:

```bash
pytest tests/test_orders.py::test_discount_boundary
```

Stop at first failure:

```bash
pytest -x
```

Enter post-mortem debugger on failure:

```bash
pytest --pdb
```

Show live output when needed:

```bash
pytest -s
```

Use `-s` carefully because large suites can become noisy.

## E.6 Type checking and linting

Static tools do not replace runtime debugging, but they can prevent many bugs from reaching runtime.

Useful categories include:

- type checker,
- linter,
- formatter,
- import/dependency checker.

For example, a type checker can warn about a possibly-`None` value before the line becomes an `AttributeError` in production.

Adopt strictness gradually on an existing codebase rather than generating thousands of ignored warnings.

## E.7 Built-in diagnostic modules worth memorizing

### Tracebacks

```python
import traceback
traceback.print_exc()
```

### Crash and hang tracebacks

Python's `faulthandler` can dump Python tracebacks for severe faults and can also help with timeout/hang diagnosis.

A simple command-line option is:

```bash
python -X faulthandler app.py
```

### CPU profiling

```bash
python -m cProfile -s cumulative app.py
```

### Small benchmarks

```bash
python -m timeit "sum(range(1000))"
```

### Memory allocations

```python
import tracemalloc
tracemalloc.start()
```

## E.8 Git for regression debugging

When a bug appeared sometime in history, use Git rather than manually checking random commits.

Typical workflow:

```bash
git bisect start
git bisect bad
git bisect good <known-good-commit>
```

Test the selected commit and mark it:

```bash
git bisect good
# or
git bisect bad
```

When finished:

```bash
git bisect reset
```

Automate the test with `git bisect run` when you have a reliable command that exits success/failure correctly.

## E.9 Docker and remote debugging

For containerized development:

```text
local editor
↕ debugger connection
container Python process
```

Check all four dimensions:

```text
network reachability
debugger listen/connect direction
source path mapping
same source revision
```

Never solve a path-mapping problem by exposing a debug port publicly.

## E.10 Production tool categories

Production debugging should emphasize evidence collection without stopping the service.

Useful categories:

| Category | Helps answer |
|---|---|
| Centralized logs | What happened? |
| Error tracking | Which exceptions affect users and how often? |
| Metrics | Is the system healthy? |
| Distributed tracing | Where did a request spend time across services? |
| Profiling | Where is CPU/time being consumed? |
| Memory monitoring | Is memory growing or spiking? |
| Database monitoring | Are queries slow, blocked, or excessive? |

Do not send passwords, tokens, private keys, payment data, or unnecessary personal data to debugging/observability tools.

## E.11 Recommended configuration philosophy

Keep three modes conceptually separate:

### Local development

```text
verbose diagnostics
interactive debugger allowed
developer-friendly errors
test data
```

### Staging/test

```text
production-like configuration
safe verbose logs when needed
reproducible test traffic
debug access restricted
```

### Production

```text
no public debug mode
sanitized structured logs
metrics/traces
controlled profiling
least-privilege diagnostic access
```

The best debugging setup is not the one with the most extensions. It is the one that gives you reliable evidence while minimizing risk and noise.

## E.12 Official references

- Python debugging and profiling: <https://docs.python.org/3/library/debug.html>
- Python `tracemalloc`: <https://docs.python.org/3/library/tracemalloc.html>
- VS Code Python debugging: <https://code.visualstudio.com/docs/python/debugging>
- VS Code Python testing: <https://code.visualstudio.com/docs/python/testing>
- PyCharm debugger documentation: <https://www.jetbrains.com/help/pycharm/debugging-code.html>
- pytest failure/debugging guide: <https://docs.pytest.org/en/stable/how-to/failures.html>

---
