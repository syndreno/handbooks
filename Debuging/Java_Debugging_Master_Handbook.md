# Java Debugging Master Handbook

> **A beginner-friendly, practical, and in-depth guide to debugging Java applications — from simple syntax mistakes to JVM memory analysis, concurrency bugs, remote debugging, production incidents, and performance troubleshooting.**

---

## Table of Contents

1. [How to Use This Handbook](#1-how-to-use-this-handbook)
2. [What Is Debugging?](#2-what-is-debugging)
3. [The Debugging Mindset](#3-the-debugging-mindset)
4. [Types of Java Bugs](#4-types-of-java-bugs)
5. [The Java Execution Model You Need for Debugging](#5-the-java-execution-model-you-need-for-debugging)
6. [Your First Debugging Workflow](#6-your-first-debugging-workflow)
7. [Reading Compiler Errors](#7-reading-compiler-errors)
8. [Reading Exceptions and Stack Traces](#8-reading-exceptions-and-stack-traces)
9. [Using `System.out.println()` Effectively](#9-using-systemoutprintln-effectively)
10. [Assertions](#10-assertions)
11. [Logging for Debugging](#11-logging-for-debugging)
12. [Debugger Fundamentals](#12-debugger-fundamentals)
13. [Breakpoints](#13-breakpoints)
14. [Stepping Through Code](#14-stepping-through-code)
15. [Inspecting Variables and Expressions](#15-inspecting-variables-and-expressions)
16. [Call Stack and Stack Frames](#16-call-stack-and-stack-frames)
17. [Debugging in IntelliJ IDEA](#17-debugging-in-intellij-idea)
18. [Debugging in Eclipse](#18-debugging-in-eclipse)
19. [Debugging Java in VS Code](#19-debugging-java-in-vs-code)
20. [Command-Line Debugging with `jdb`](#20-command-line-debugging-with-jdb)
21. [Debugging with `jshell`](#21-debugging-with-jshell)
22. [Exception Debugging](#22-exception-debugging)
23. [Common Java Exceptions and How to Debug Them](#23-common-java-exceptions-and-how-to-debug-them)
24. [NullPointerException Deep Dive](#24-nullpointerexception-deep-dive)
25. [Collections Debugging](#25-collections-debugging)
26. [String Debugging](#26-string-debugging)
27. [Numeric and Precision Bugs](#27-numeric-and-precision-bugs)
28. [Date and Time Debugging](#28-date-and-time-debugging)
29. [File and I/O Debugging](#29-file-and-io-debugging)
30. [JSON and Serialization Debugging](#30-json-and-serialization-debugging)
31. [Database Debugging](#31-database-debugging)
32. [HTTP and API Debugging](#32-http-and-api-debugging)
33. [Debugging Java Web Applications](#33-debugging-java-web-applications)
34. [Spring and Spring Boot Debugging](#34-spring-and-spring-boot-debugging)
35. [Dependency Injection Problems](#35-dependency-injection-problems)
36. [Hibernate/JPA Debugging](#36-hibernatejpa-debugging)
37. [Unit-Test-Driven Debugging](#37-unit-test-driven-debugging)
38. [JUnit Debugging Techniques](#38-junit-debugging-techniques)
39. [Mocking and Mockito Debugging](#39-mocking-and-mockito-debugging)
40. [Concurrency Debugging](#40-concurrency-debugging)
41. [Race Conditions](#41-race-conditions)
42. [Deadlocks](#42-deadlocks)
43. [Thread Dumps](#43-thread-dumps)
44. [ExecutorService and Thread Pool Problems](#44-executorservice-and-thread-pool-problems)
45. [CompletableFuture Debugging](#45-completablefuture-debugging)
46. [Memory Debugging](#46-memory-debugging)
47. [OutOfMemoryError](#47-outofmemoryerror)
48. [Memory Leaks](#48-memory-leaks)
49. [Heap Dumps](#49-heap-dumps)
50. [Garbage Collection Debugging](#50-garbage-collection-debugging)
51. [JVM Diagnostic Tools](#51-jvm-diagnostic-tools)
52. [`jps`](#52-jps)
53. [`jcmd`](#53-jcmd)
54. [`jstack`](#54-jstack)
55. [`jmap`](#55-jmap)
56. [`jstat`](#56-jstat)
57. [JConsole, VisualVM, JFR, and JMC](#57-jconsole-visualvm-jfr-and-jmc)
58. [CPU and Performance Debugging](#58-cpu-and-performance-debugging)
59. [Remote Debugging](#59-remote-debugging)
60. [Debugging in Docker and Containers](#60-debugging-in-docker-and-containers)
61. [Debugging Environment and Configuration Problems](#61-debugging-environment-and-configuration-problems)
62. [Classpath and Dependency Debugging](#62-classpath-and-dependency-debugging)
63. [Build Tool Debugging: Maven](#63-build-tool-debugging-maven)
64. [Build Tool Debugging: Gradle](#64-build-tool-debugging-gradle)
65. [Class Loading Problems](#65-class-loading-problems)
66. [Reflection Debugging](#66-reflection-debugging)
67. [Generics Debugging](#67-generics-debugging)
68. [Lambda and Stream Debugging](#68-lambda-and-stream-debugging)
69. [Debugging Recursive Algorithms](#69-debugging-recursive-algorithms)
70. [Debugging Data Structures and Algorithms](#70-debugging-data-structures-and-algorithms)
71. [Production Debugging](#71-production-debugging)
72. [Safe Production Troubleshooting](#72-safe-production-troubleshooting)
73. [Observability: Logs, Metrics, Traces](#73-observability-logs-metrics-traces)
74. [Security-Sensitive Debugging](#74-security-sensitive-debugging)
75. [Debugging Patterns and Anti-Patterns](#75-debugging-patterns-and-anti-patterns)
76. [Scientific Debugging](#76-scientific-debugging)
77. [Binary Search Debugging](#77-binary-search-debugging)
78. [Rubber Duck Debugging](#78-rubber-duck-debugging)
79. [Minimal Reproducible Examples](#79-minimal-reproducible-examples)
80. [Debugging Legacy Code](#80-debugging-legacy-code)
81. [Scenario Playbooks](#81-scenario-playbooks)
82. [Common Java Error Reference](#82-common-java-error-reference)
83. [Debugging Checklist](#83-debugging-checklist)
84. [Production Incident Checklist](#84-production-incident-checklist)
85. [Beginner Exercises](#85-beginner-exercises)
86. [Intermediate Exercises](#86-intermediate-exercises)
87. [Advanced Exercises](#87-advanced-exercises)
88. [Debugging Interview Questions](#88-debugging-interview-questions)
89. [Command Cheat Sheet](#89-command-cheat-sheet)
90. [Glossary](#90-glossary)
91. [Final Learning Path](#91-final-learning-path)
92. [Appendix H — Recommended Java Debugging Tools and Configuration](#appendix-h--recommended-java-debugging-tools-and-configuration)

---

# 1. How to Use This Handbook

This handbook is designed to work as a **single reference file** for Java debugging.

You do not have to read it from beginning to end every time.

Use it in three ways:

## If you are a complete beginner

Start with:

1. What debugging is.
2. Types of bugs.
3. Compiler errors.
4. Stack traces.
5. `System.out.println()`.
6. IDE debugger basics.
7. Breakpoints.
8. Variable inspection.
9. Common exceptions.

## If you already write Java applications

Focus on:

- logging,
- unit-test-driven debugging,
- HTTP/API problems,
- Spring Boot,
- JPA/Hibernate,
- Maven/Gradle,
- configuration,
- remote debugging.

## If you work with production systems

Focus on:

- thread dumps,
- heap dumps,
- JVM tools,
- GC,
- JFR,
- deadlocks,
- memory leaks,
- CPU profiling,
- observability,
- production troubleshooting.

---

# 2. What Is Debugging?

**Debugging is the process of finding, understanding, and fixing the reason a program behaves differently from what you intended.**

A program can:

- fail to compile,
- crash,
- return the wrong result,
- become slow,
- consume too much memory,
- hang,
- fail only for certain users,
- fail only in production,
- work sometimes and fail sometimes.

All of these are debugging problems.

## Example

Suppose you write:

```java
int price = 100;
int quantity = 3;

System.out.println(price + quantity);
```

You expected:

```text
300
```

But got:

```text
103
```

Java is behaving correctly. The bug is in your logic.

Correct code:

```java
System.out.println(price * quantity);
```

Debugging means discovering **why `103` happened** and correcting the real cause.

---

# 3. The Debugging Mindset

Good debugging is not random code changing.

Avoid this approach:

```text
Maybe this fixes it.
No.
Try something else.
No.
Restart.
Still no.
Delete code.
Add code.
Search random error.
```

Instead use a repeatable process.

## The core debugging cycle

```text
Observe
  ↓
Reproduce
  ↓
Collect evidence
  ↓
Form a hypothesis
  ↓
Test the hypothesis
  ↓
Locate root cause
  ↓
Fix
  ↓
Verify
  ↓
Prevent regression
```

## Five important questions

Whenever something fails, ask:

1. **What did I expect?**
2. **What actually happened?**
3. **Where do the expected and actual behavior first differ?**
4. **What evidence proves the cause?**
5. **How will I prove the fix works?**

---

# 4. Types of Java Bugs

Java bugs can be divided into several broad categories.

## 4.1 Syntax errors

The Java source is invalid.

```java
System.out.println("Hello")
```

Missing semicolon.

Compiler error:

```text
';' expected
```

Correct:

```java
System.out.println("Hello");
```

---

## 4.2 Compilation errors

The syntax may look reasonable, but Java cannot compile the program.

```java
int age = "27";
```

Error:

```text
incompatible types: String cannot be converted to int
```

---

## 4.3 Runtime errors

The code compiles but fails while running.

```java
int[] values = {10, 20, 30};
System.out.println(values[5]);
```

Runtime exception:

```text
ArrayIndexOutOfBoundsException
```

---

## 4.4 Logical errors

The application runs but gives the wrong result.

```java
double discount = 10;
double price = 1000;

double finalPrice = price - discount;
```

If `discount` represents 10%, this is wrong.

Correct:

```java
double finalPrice = price - (price * discount / 100);
```

---

## 4.5 Performance bugs

The result is correct but takes too long.

Example:

```java
for (User user : users) {
    database.loadOrders(user.getId());
}
```

If `users` contains 50,000 entries, this may create 50,000 database queries.

---

## 4.6 Concurrency bugs

Multiple threads interfere with each other.

Common examples:

- race condition,
- deadlock,
- lost update,
- visibility problem,
- thread starvation.

---

## 4.7 Resource leaks

A program does not release resources correctly.

Examples:

- database connections,
- file streams,
- HTTP connections,
- threads,
- memory references.

---

## 4.8 Configuration bugs

Code is correct, but configuration is wrong.

Examples:

```text
Wrong database URL
Wrong port
Missing environment variable
Wrong Spring profile
Wrong credentials
Wrong file path
```

---

## 4.9 Integration bugs

Two components work individually but fail when connected.

Examples:

- frontend sends `userId`, backend expects `user_id`,
- API returns ISO date but parser expects another format,
- database column is nullable but Java field is primitive.

---

# 5. The Java Execution Model You Need for Debugging

Understanding the Java execution flow makes debugging easier.

Typical flow:

```text
.java source
    ↓ javac
.class bytecode
    ↓ JVM class loader
JVM runtime
    ↓
JIT compilation / interpretation
    ↓
Operating system
```

## Why this matters

A failure can happen at different layers.

| Layer | Example failure |
|---|---|
| Source | syntax error |
| Compiler | type mismatch |
| Classpath | class not found |
| JVM | OutOfMemoryError |
| Application | NullPointerException |
| OS | permission denied |
| Network | timeout |
| Database | constraint violation |

Always identify **which layer is failing**.

---

# 6. Your First Debugging Workflow

Consider:

```java
public class Calculator {

    public static int divide(int a, int b) {
        return a / b;
    }

    public static void main(String[] args) {
        int result = divide(10, 0);
        System.out.println(result);
    }
}
```

Output:

```text
Exception in thread "main" java.lang.ArithmeticException: / by zero
    at Calculator.divide(Calculator.java:4)
    at Calculator.main(Calculator.java:8)
```

## Step 1 — Read the exception

```text
ArithmeticException: / by zero
```

Java tells you the immediate problem.

## Step 2 — Read the first relevant application frame

```text
Calculator.divide(Calculator.java:4)
```

This is usually where you should begin.

## Step 3 — Inspect inputs

```java
a = 10
b = 0
```

## Step 4 — Ask why

Why was `b` zero?

That question moves you from **symptom** to **root cause**.

## Step 5 — Fix safely

```java
public static int divide(int a, int b) {
    if (b == 0) {
        throw new IllegalArgumentException("b must not be zero");
    }

    return a / b;
}
```

---

# 7. Reading Compiler Errors

Compiler errors often look intimidating because one mistake can produce multiple messages.

## Example

```java
public class App {
    public static void main(String[] args) {
        int age = "25";
        System.out.println(age)
    }
}
```

You may receive multiple compiler errors.

Fix errors from **top to bottom**, because later errors may be consequences of earlier ones.

## Common compiler messages

### `cannot find symbol`

```java
System.out.println(userName);
```

But variable is:

```java
String username = "Alice";
```

Potential causes:

- typo,
- variable out of scope,
- missing import,
- missing dependency,
- wrong class name.

---

### `incompatible types`

```java
int value = "100";
```

Fix:

```java
int value = Integer.parseInt("100");
```

---

### `method ... cannot be applied to given types`

```java
Math.max(1);
```

`Math.max()` expects two values.

```java
Math.max(1, 2);
```

---

### `non-static method cannot be referenced from a static context`

```java
class App {

    void hello() {
        System.out.println("Hello");
    }

    public static void main(String[] args) {
        hello();
    }
}
```

Fix by creating an instance:

```java
App app = new App();
app.hello();
```

Or make the method static if that matches the design.

---

# 8. Reading Exceptions and Stack Traces

A stack trace is one of the most important debugging tools in Java.

Example:

```text
Exception in thread "main" java.lang.NullPointerException:
Cannot invoke "User.getName()" because "user" is null
    at UserService.printUser(UserService.java:25)
    at OrderService.process(OrderService.java:48)
    at Application.main(Application.java:10)
```

Read it in this order:

## 8.1 Exception type

```text
java.lang.NullPointerException
```

## 8.2 Exception message

```text
Cannot invoke "User.getName()" because "user" is null
```

## 8.3 First relevant source line

```text
UserService.java:25
```

## 8.4 Call chain

```text
Application.main()
  → OrderService.process()
      → UserService.printUser()
          → NullPointerException
```

## Important rule

Do not automatically assume the line where an exception is thrown is the root cause.

Example:

```java
user.getAddress().getCity().toUpperCase()
```

The failure may be caused by:

- `user == null`,
- `user.getAddress() == null`,
- `getCity() == null`.

Modern JVM messages often tell you which reference is null, but you should still understand the chain.

---

# 9. Using `System.out.println()` Effectively

Printing values is the simplest debugging technique.

## Weak debugging print

```java
System.out.println(user);
```

You may not know why it was printed.

## Better

```java
System.out.println("DEBUG user before validation = " + user);
```

## Better for multiple variables

```java
System.out.printf(
    "DEBUG orderId=%s customerId=%s total=%s status=%s%n",
    orderId,
    customerId,
    total,
    status
);
```

## Boundary debugging

When a bug exists in a long method, print values at important boundaries.

```java
System.out.println("input = " + input);

String normalized = normalize(input);
System.out.println("normalized = " + normalized);

Result result = calculate(normalized);
System.out.println("result = " + result);
```

This helps identify the point where data first becomes incorrect.

## When not to rely on `System.out`

Avoid using it as your primary production debugging method.

Problems include:

- poor structure,
- no levels,
- hard to search,
- can expose secrets,
- may create performance problems,
- difficult correlation between requests.

Use a logging framework for real applications.

---

# 10. Assertions

Assertions express assumptions that should be true during development.

```java
int count = calculateCount();

assert count >= 0 : "Count must not be negative";
```

Run with assertions enabled:

```bash
java -ea App
```

Without `-ea`, assertions are normally disabled.

## Good use

Internal invariants:

```java
assert startIndex <= endIndex;
```

## Bad use

Do not use assertions to validate required user input or business rules.

Bad:

```java
assert user != null;
```

If the application requires `user`, prefer:

```java
Objects.requireNonNull(user, "user must not be null");
```

or explicit validation.

---

# 11. Logging for Debugging

Logging records application behavior in a structured way.

Popular Java logging APIs/frameworks include:

- SLF4J API,
- Logback,
- Log4j 2,
- `java.util.logging`.

## Example with SLF4J

```java
private static final Logger log =
    LoggerFactory.getLogger(OrderService.class);

public void process(Order order) {
    log.debug("Processing order id={}", order.getId());
}
```

## Logging levels

| Level | Typical purpose |
|---|---|
| TRACE | extremely detailed internal behavior |
| DEBUG | developer diagnostics |
| INFO | normal important events |
| WARN | unexpected but recoverable situation |
| ERROR | failed operation requiring attention |

## Prefer structured messages

Weak:

```java
log.debug("Processing order " + orderId);
```

Better:

```java
log.debug("Processing order orderId={}", orderId);
```

## Do not log secrets

Never log:

```text
Passwords
API keys
Session tokens
Authorization headers
Private keys
Full credit-card numbers
Sensitive personal information
```

---

# 12. Debugger Fundamentals

A Java debugger controls a running JVM through debugging interfaces so you can pause threads, inspect program state, and step through source-level execution.

A debugger does **not** automatically tell you the root cause. It gives you evidence.

## 12.1 Core pieces

| Concept | Meaning |
|---|---|
| Debug target | The JVM/process being investigated |
| Debugger client | IntelliJ IDEA, Eclipse, VS Code, `jdb`, or another frontend |
| Breakpoint | A location or condition where execution should pause |
| Stack frame | One active method call and its local state |
| Watch | An expression repeatedly evaluated while paused |
| Step operation | Controlled execution to the next relevant point |

## 12.2 Launch vs attach

Two common modes are:

### Launch

The IDE starts the Java application itself.

```text
IDE
→ starts JVM with debug support
→ program runs
→ breakpoint pauses execution
```

This is simplest for local development.

### Attach

The JVM is started separately with remote-debug support, and the debugger connects later.

```text
JVM already running
← debugger attaches
```

This is common for:

- application servers,
- Docker containers,
- remote development machines,
- services started by scripts.

## 12.3 What to inspect when paused

Do not inspect only the variable named in the exception.

Check:

```text
method arguments
local variables
object fields
current thread
call stack
caller frames
collection sizes
nullability
state transitions
```

A bad value is often created several calls before the line that finally fails.

## 12.4 Stepping changes timing

Pausing a thread can change the behavior of concurrent programs.

A race condition may disappear while single-stepping.

For concurrency bugs, combine the debugger with:

- thread dumps,
- structured logging,
- repeated stress tests,
- JFR,
- metrics.

This effect is often called a **Heisenbug**: observing the program changes the conditions that trigger the bug.

## 12.5 Safety

Never expose an unauthenticated remote-debug port to an untrusted network. A debugger can provide deep access to application internals and can often evaluate code in the target JVM.

---
# 13. Breakpoints

A breakpoint tells the debugger to pause execution at a specific location.

Example:

```java
public double calculateTotal(Order order) {
    double subtotal = calculateSubtotal(order); // breakpoint
    double tax = subtotal * 0.18;
    return subtotal + tax;
}
```

When execution pauses, inspect:

```text
order
subtotal
order.items
order.customer
```

## 13.1 Line breakpoint

Pause whenever the line is reached.

## 13.2 Conditional breakpoint

Pause only when a condition is true.

Example condition:

```java
order.getId() == 5001
```

Useful when the method executes thousands of times but only one record fails.

## 13.3 Hit-count breakpoint

Pause after a line is reached a certain number of times.

Useful for bugs that happen after repeated execution.

## 13.4 Exception breakpoint

Pause whenever a selected exception is thrown.

Very useful for:

```text
NullPointerException
IllegalArgumentException
SQLException
```

## 13.5 Method breakpoint

Pause when entering or leaving a method.

These can be slower than line breakpoints, so use them selectively.

## 13.6 Field watchpoint

Some debuggers can pause when a field is read or changed.

Useful for:

```java
private Status status;
```

when you do not know which code changes it unexpectedly.

---

# 14. Stepping Through Code

Once the debugger pauses, you decide how execution continues.

## Step Over

Execute the current line without entering called methods.

```java
Result result = service.calculate(data);
```

Step Over runs `calculate()` and pauses at the next line.

Use when you trust the called method.

---

## Step Into

Enter the method being called.

```java
Result result = service.calculate(data);
```

Step Into takes you inside:

```java
calculate(data)
```

Use when you suspect the bug is inside that method.

---

## Step Out

Finish the current method and return to its caller.

Useful when you accidentally stepped into library code.

---

## Resume

Continue running until:

- next breakpoint,
- exception breakpoint,
- process completion.

---

## Run to Cursor

Continue execution until the selected source line without creating a permanent breakpoint.

---

# 15. Inspecting Variables and Expressions

When paused, inspect variables.

Example:

```java
int price = 100;
int quantity = 3;
int total = price + quantity;
```

You might inspect:

```text
price = 100
quantity = 3
total = 103
```

This immediately reveals the mistake.

## Watches

A watch repeatedly evaluates an expression while stepping.

Examples:

```java
order.getItems().size()
user.getAddress() == null
price * quantity
list.stream().filter(x -> x.isActive()).count()
```

## Evaluate Expression

Most IDEs allow one-time expression evaluation.

Example:

```java
customer.getOrders().size()
```

Be careful: evaluating methods may have side effects.

Avoid evaluating expressions like:

```java
service.deleteEverything()
```

or methods that mutate state.

---

# 16. Call Stack and Stack Frames

The call stack shows how execution reached the current method.

Example:

```text
Application.main()
  → Controller.createOrder()
      → OrderService.create()
          → PaymentService.pay()
              → BankClient.charge()
```

Each entry is a **stack frame**.

A stack frame contains:

- parameters,
- local variables,
- current line,
- method context.

You can select an older stack frame to inspect values from the caller.

This is extremely useful when a value was passed incorrectly.

---

# 17. Debugging in IntelliJ IDEA

Typical workflow:

1. Open a Java project.
2. Click the gutter next to a source line to set a breakpoint.
3. Start the application using **Debug** instead of Run.
4. Wait for the breakpoint.
5. Inspect the Variables panel.
6. Use Step Over / Step Into / Step Out.
7. Add watches when necessary.
8. Resume execution.

## Useful IntelliJ techniques

### Conditional breakpoint

Right-click the breakpoint and specify a condition.

Example:

```java
customerId == 12345
```

### Evaluate expression

Use the Evaluate Expression action while paused.

### Smart Step Into

Useful when one line contains several method calls.

```java
validate(transform(loadData()));
```

Smart Step Into lets you choose which method to enter.

### Drop Frame

Some debugging situations allow you to reset execution to an earlier stack frame and run that section again.

Use carefully because external side effects may already have happened.

---

# 18. Debugging in Eclipse

Eclipse includes Java debugging support as part of its Java development tooling.

## 18.1 Basic workflow

1. Open the project.
2. Set a breakpoint in the editor gutter.
3. Choose **Debug As** for the application or test.
4. Reproduce the failing path.
5. Use the Debug perspective/views to inspect threads, stack frames, variables, and breakpoints.
6. Step through only the suspicious area.
7. Resume and verify the outcome.

## 18.2 Useful breakpoint types

Besides ordinary line breakpoints, Eclipse debugging can help with conditions such as:

- a specific variable value,
- an exception being thrown,
- method entry depending on tooling/version,
- watchpoints for field access/modification in supported cases.

Conditional breakpoints are especially useful inside loops:

```java
order.getId() == 4201
```

Without the condition, the debugger might stop thousands of times.

## 18.3 Exception breakpoints

When an exception is caught and wrapped later, the visible stack trace may hide the earliest interesting moment.

Configure the debugger to suspend when the relevant exception type is thrown, then inspect:

```text
current frame
caller
method arguments
object state
```

Avoid suspending on every possible exception in a large framework because normal library behavior can produce many irrelevant pauses.

## 18.4 Common "breakpoint not hit" causes

Check:

```text
Is this class actually loaded?
Is the source file the same version as the running .class?
Was the application restarted after recompilation?
Is the breakpoint in an executable line?
Are you debugging the correct process?
Is hot code replacement hiding a larger structural change?
```

A debugger cannot reliably map a stale source file to different bytecode.

---
# 19. Debugging Java in VS Code

VS Code supports Java debugging through the **Debugger for Java** extension. For a complete Java setup, the **Extension Pack for Java** is the simplest starting point because it bundles the core Java tooling.

## 19.1 Basic workflow

1. Install the Java extension pack.
2. Open the Java project as a folder/workspace.
3. Wait for project import/build information to finish loading.
4. Set a breakpoint.
5. Press `F5` or choose **Run > Start Debugging**.
6. Inspect Variables, Watch, Call Stack, Threads, and the Debug Console.

For many simple projects, VS Code can find the main class and create an in-memory debug configuration automatically.

## 19.2 Persistent `launch.json`

Create `.vscode/launch.json` when you need repeatable project-specific settings.

Example:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "java",
      "name": "Debug Application",
      "request": "launch",
      "mainClass": "com.example.Application"
    }
  ]
}
```

Use the real fully qualified main class for your project.

## 19.3 Useful features

VS Code's Java debugger supports features such as:

- launch and attach,
- line and conditional breakpoints,
- exception breakpoints,
- stepping,
- variable inspection,
- call stacks and threads,
- expression evaluation,
- Hot Code Replace in supported changes.

## 19.4 Debugging tests

The **Test Runner for Java** extension can run and debug supported Java tests directly from VS Code.

When one test fails, debug that test first rather than launching the entire suite.

## 19.5 Common configuration problems

If debugging fails, verify:

```text
JDK selected by VS Code
project imported successfully
main class is correct
classpath/module path is correct
source matches compiled bytecode
the failing code path is actually executed
```

For Maven or Gradle projects, resolve the build first if the project model itself is broken.

---
# 20. Command-Line Debugging with `jdb`

`jdb` is the Java Debugger available with the JDK.

Compile with debug information:

```bash
javac -g App.java
```

Start debugger:

```bash
jdb App
```

Common concepts include:

```text
stop at ClassName:line
run
next
step
cont
locals
where
print variable
```

Example:

```text
stop at App:10
run
locals
print total
next
```

`jdb` is useful when:

- no full IDE is available,
- debugging on servers,
- learning the underlying debugger model.

---

# 21. Debugging with `jshell`

`jshell` is useful for testing small Java expressions and APIs interactively.

Start:

```bash
jshell
```

Example:

```text
jshell> "hello".toUpperCase()
$1 ==> "HELLO"
```

Test a date expression:

```java
LocalDate.parse("2026-08-17")
```

Test a regex:

```java
"INV-123".matches("INV-\\d+")
```

`jshell` is excellent for isolating small assumptions without running a full application.

---

# 22. Exception Debugging

When an exception occurs:

1. Identify the exception class.
2. Read the message.
3. Find the first relevant application stack frame.
4. Inspect variables.
5. Determine why the invalid state existed.
6. Fix the root cause.
7. Add a regression test.

Do not immediately write:

```java
try {
    riskyCode();
} catch (Exception e) {
}
```

This hides the problem.

A catch block should have a reason.

Example:

```java
try {
    return repository.load(id);
} catch (SQLException e) {
    log.error("Failed to load order id={}", id, e);
    throw new OrderRepositoryException("Unable to load order", e);
}
```

Preserve the original cause.

---

# 23. Common Java Exceptions and How to Debug Them

## `NullPointerException`

Cause:

```java
String name = null;
name.length();
```

Investigate why `name` became null.

---

## `ArrayIndexOutOfBoundsException`

```java
int[] numbers = {1, 2, 3};
System.out.println(numbers[3]);
```

Valid indices are:

```text
0, 1, 2
```

---

## `IndexOutOfBoundsException`

Usually from lists.

```java
List<String> names = List.of("A", "B");
names.get(2);
```

---

## `NumberFormatException`

```java
Integer.parseInt("ABC");
```

Debug the original input.

---

## `ClassCastException`

```java
Object value = "hello";
Integer number = (Integer) value;
```

Inspect the runtime type.

---

## `IllegalArgumentException`

Usually indicates an invalid parameter.

---

## `IllegalStateException`

Usually indicates the object is in a state where the operation is not valid.

---

## `ConcurrentModificationException`

Often caused by modifying a collection while iterating over it.

---

## `StackOverflowError`

Usually:

- uncontrolled recursion,
- circular method calls,
- extremely deep recursion.

---

## `OutOfMemoryError`

The JVM cannot allocate required memory.

This is not automatically proof of a memory leak.

---

# 24. NullPointerException Deep Dive

Consider:

```java
String city =
    order.getCustomer()
         .getAddress()
         .getCity()
         .toUpperCase();
```

Potential nulls:

```text
order
customer
address
city
```

## Debugging strategy

Break the chain:

```java
Customer customer = order.getCustomer();
Address address = customer.getAddress();
String city = address.getCity();
String result = city.toUpperCase();
```

Now each step is easier to inspect.

## Avoid blindly replacing NPE with Optional

Bad mental model:

```text
NullPointerException → put Optional everywhere
```

First determine the domain rule.

If every order must have a customer:

```java
Objects.requireNonNull(
    order.getCustomer(),
    "Order must have a customer"
);
```

If the address is legitimately optional, handle that intentionally.

---

# 25. Collections Debugging

Common collection bugs include:

- wrong index,
- unexpected empty list,
- duplicate values,
- mutation,
- iteration problems,
- incorrect equality,
- hash code mistakes.

## Example: duplicate-looking objects in `HashSet`

```java
Set<User> users = new HashSet<>();
users.add(new User(1, "A"));
users.add(new User(1, "A"));
```

If `User` does not implement suitable `equals()` and `hashCode()`, both objects may remain.

Debug:

```java
System.out.println(users.size());
```

Inspect:

```text
equals()
hashCode()
identity
field values
```

## Example: modifying while iterating

Bad:

```java
for (String name : names) {
    if (name.isBlank()) {
        names.remove(name);
    }
}
```

Possible `ConcurrentModificationException`.

Safer:

```java
names.removeIf(String::isBlank);
```

---

# 26. String Debugging

Strings often fail because of invisible or unexpected characters.

Example:

```java
String role = "ADMIN ";
System.out.println(role.equals("ADMIN"));
```

Output:

```text
false
```

Debug:

```java
System.out.println("[" + role + "]");
System.out.println(role.length());
```

Potential problems:

- leading/trailing spaces,
- newline,
- tab,
- Unicode character,
- case mismatch,
- wrong encoding.

Use:

```java
role.trim()
role.strip()
equalsIgnoreCase()
```

only when those semantics are actually desired.

---

# 27. Numeric and Precision Bugs

## Integer division

```java
int result = 5 / 2;
```

Output:

```text
2
```

If you expect `2.5`:

```java
double result = 5.0 / 2;
```

---

## Floating-point precision

```java
double result = 0.1 + 0.2;
System.out.println(result);
```

May not print exactly:

```text
0.3
```

For money, prefer `BigDecimal`.

```java
BigDecimal a = new BigDecimal("0.1");
BigDecimal b = new BigDecimal("0.2");

System.out.println(a.add(b));
```

Output:

```text
0.3
```

---

## Integer overflow

```java
int max = Integer.MAX_VALUE;
System.out.println(max + 1);
```

The result wraps around.

Use suitable ranges and methods such as:

```java
Math.addExact(a, b)
```

when overflow must be detected.

---

# 28. Date and Time Debugging

Date/time bugs commonly involve:

- wrong timezone,
- wrong format,
- UTC vs local time,
- daylight saving transitions,
- parsing failures,
- inclusive/exclusive boundaries.

Prefer `java.time`.

Example:

```java
LocalDate date = LocalDate.parse("2026-08-17");
```

If the input includes time and offset:

```java
OffsetDateTime
```

If it represents a global instant:

```java
Instant
```

Debug by logging:

```java
log.debug(
    "timestamp={} zone={} instant={}",
    zonedDateTime,
    zonedDateTime.getZone(),
    zonedDateTime.toInstant()
);
```

---

# 29. File and I/O Debugging

Common failures:

```text
FileNotFoundException
AccessDeniedException
NoSuchFileException
MalformedInputException
IOException
```

## Debug the actual path

```java
Path path = Path.of("data/orders.csv");

System.out.println(path.toAbsolutePath());
System.out.println(Files.exists(path));
System.out.println(Files.isReadable(path));
```

Relative paths are resolved from the process working directory, which may differ between:

- IDE,
- terminal,
- test runner,
- application server,
- container.

## Use try-with-resources

```java
try (BufferedReader reader =
         Files.newBufferedReader(path)) {

    // read
}
```

This helps prevent resource leaks.

---

# 30. JSON and Serialization Debugging

Common JSON problems:

- field name mismatch,
- missing fields,
- unexpected `null`,
- wrong date format,
- number represented as string,
- unknown property,
- recursive object graph,
- enum mismatch.

Suppose JSON contains:

```json
{
  "user_id": 10
}
```

Java object:

```java
class Request {
    private int userId;
}
```

Depending on configuration, this may not bind automatically.

Debug by checking:

1. raw HTTP body,
2. content type,
3. DTO field names,
4. serializer configuration,
5. exception cause.

Avoid logging sensitive full request bodies in production.

---

# 31. Database Debugging

Database problems often involve several layers.

```text
Java code
 → connection pool
 → JDBC driver
 → network
 → database
 → SQL
 → schema/data
```

## Common symptoms

- connection refused,
- authentication failure,
- timeout,
- deadlock,
- duplicate key,
- foreign key failure,
- incorrect query result,
- N+1 queries,
- transaction not committed.

## Useful questions

- Which database URL is the application actually using?
- Which user?
- Which schema?
- Which SQL statement?
- What parameters were bound?
- Is the transaction committed?
- Is connection pooling exhausted?
- Is the problem data-specific?

## JDBC example

```java
try (PreparedStatement ps =
         connection.prepareStatement(
             "SELECT id, name FROM users WHERE id = ?"
         )) {

    ps.setLong(1, userId);

    try (ResultSet rs = ps.executeQuery()) {
        // inspect result
    }
}
```

Prefer parameterized SQL over string concatenation.

---

# 32. HTTP and API Debugging

For API problems, debug each boundary.

```text
Client
  ↓
DNS
  ↓
TCP/TLS
  ↓
HTTP request
  ↓
Server routing
  ↓
Controller
  ↓
Service
  ↓
Database/external API
  ↓
HTTP response
```

Record:

```text
HTTP method
URL/path
status code
request ID
headers when safe
response body when safe
latency
timeout
```

## Example status interpretation

| Status | Meaning to investigate |
|---|---|
| 400 | invalid request |
| 401 | authentication |
| 403 | authorization |
| 404 | path/resource |
| 409 | conflict |
| 422 | semantic validation |
| 500 | server-side failure |
| 502 | upstream/gateway |
| 503 | unavailable |
| 504 | upstream timeout |

---

# 33. Debugging Java Web Applications

A common web flow is:

```text
HTTP request
 → filter
 → controller
 → service
 → repository
 → database
 → response
```

If a request returns `500`, do not debug the whole application at once.

Find where the failure occurs.

Add correlation IDs or request IDs so one request can be followed across logs.

Example:

```text
requestId=2f3c... orderId=5001
```

Then search all logs for the same ID.

---

# 34. Spring and Spring Boot Debugging

Spring Boot failures can happen during:

- startup,
- bean creation,
- configuration binding,
- web request handling,
- database initialization,
- dependency injection,
- auto-configuration.

## Startup failure strategy

Read the **bottom-most meaningful cause**.

Example:

```text
BeanCreationException
  caused by ConfigurationPropertiesBindException
    caused by IllegalArgumentException
```

The outer exception may be generic. The inner cause usually contains the useful detail.

## Enable useful diagnostics selectively

Use Spring Boot debug output when appropriate:

```text
--debug
```

or configuration-based logging.

Avoid enabling extremely verbose logging globally in production without understanding the impact.

---

# 35. Dependency Injection Problems

Example error:

```text
No qualifying bean of type 'PaymentService' available
```

Investigate:

1. Is the implementation annotated?
2. Is it in component-scan scope?
3. Is there more than one implementation?
4. Is a qualifier required?
5. Is a profile disabling it?
6. Is conditional configuration preventing creation?
7. Is constructor injection correct?

Example:

```java
@Service
class StripePaymentService implements PaymentService {
}
```

Constructor injection:

```java
@Service
class OrderService {

    private final PaymentService paymentService;

    OrderService(PaymentService paymentService) {
        this.paymentService = paymentService;
    }
}
```

---

# 36. Hibernate/JPA Debugging

Common problems:

- lazy loading,
- detached entities,
- N+1 queries,
- cascade mistakes,
- transaction boundaries,
- incorrect mappings,
- wrong join columns,
- stale data,
- flush timing.

## N+1 example

```java
List<Order> orders = orderRepository.findAll();

for (Order order : orders) {
    System.out.println(order.getItems().size());
}
```

If each `getItems()` triggers a query, you may generate one query for orders plus one query per order.

Debug using:

- SQL logs,
- query count,
- profiler,
- fetch strategy inspection.

Do not solve every N+1 problem by making everything `EAGER`. That can create different performance problems.

---

# 37. Unit-Test-Driven Debugging

A powerful debugging workflow is:

1. reproduce the bug in a small test,
2. watch the test fail,
3. fix the code,
4. watch the test pass.

Example bug:

```java
public int calculateDiscount(int price) {
    return price - 10;
}
```

Expected: 10% discount.

Test:

```java
@Test
void shouldApplyTenPercentDiscount() {
    assertEquals(900, service.calculateDiscount(1000));
}
```

The test creates a permanent regression check.

---

# 38. JUnit Debugging Techniques

## Debug a single test

Instead of starting the entire application, debug one failing unit test.

Advantages:

- faster,
- fewer unrelated variables,
- easy reproducibility.

## Parameterized tests

Useful when a bug occurs only for certain values.

Conceptual example:

```java
@ParameterizedTest
@CsvSource({
    "100, 90",
    "200, 180",
    "0, 0"
})
void appliesDiscount(int input, int expected) {
    assertEquals(expected, discount(input));
}
```

## Test boundary values

For a range `1–100`, test:

```text
0
1
100
101
```

Bugs frequently live at boundaries.

---

# 39. Mocking and Mockito Debugging

Mocking problems often come from:

- method not stubbed,
- wrong argument,
- mock returning default `null`,
- verifying wrong call,
- over-mocking,
- mocking the class under test.

Example:

```java
when(repository.findById(10L))
    .thenReturn(Optional.of(user));
```

But production code calls:

```java
repository.findById(11L)
```

The stub does not match.

Inspect actual arguments.

Use argument captors when useful.

Also remember: a passing mock-heavy unit test does not prove real database/network integration works.

---

# 40. Concurrency Debugging

Concurrency bugs are difficult because timing affects behavior.

Symptoms include:

- random incorrect result,
- occasional test failure,
- application hang,
- missing updates,
- duplicate work,
- CPU spike,
- thread pool exhaustion.

Important concepts:

```text
atomicity
visibility
ordering
mutual exclusion
thread safety
happens-before
```

---

# 41. Race Conditions

Example:

```java
class Counter {
    int value = 0;

    void increment() {
        value++;
    }
}
```

`value++` is not a single indivisible operation.

Conceptually:

```text
read value
add 1
write value
```

Two threads can interfere.

Safer option:

```java
AtomicInteger value = new AtomicInteger();

void increment() {
    value.incrementAndGet();
}
```

Or synchronize when the operation requires locking.

## How to debug races

Look for:

- shared mutable state,
- unsynchronized writes,
- compound read-modify-write operations,
- collections not safe for concurrent access.

---

# 42. Deadlocks

A deadlock occurs when threads wait forever for resources held by each other.

Example pattern:

```text
Thread A:
holds Lock 1
waits for Lock 2

Thread B:
holds Lock 2
waits for Lock 1
```

Example code shape:

```java
synchronized (lockA) {
    synchronized (lockB) {
        // ...
    }
}
```

Elsewhere:

```java
synchronized (lockB) {
    synchronized (lockA) {
        // ...
    }
}
```

## Prevention

Use consistent lock ordering.

```text
Always acquire lockA before lockB
```

Thread dumps are one of the best tools for diagnosing deadlocks.

---

# 43. Thread Dumps

A thread dump shows the state and stack of JVM threads.

Useful when:

- application hangs,
- CPU is high,
- requests stop progressing,
- suspected deadlock,
- thread pool starvation.

A thread may be:

```text
RUNNABLE
BLOCKED
WAITING
TIMED_WAITING
```

Look for:

- many threads blocked on the same monitor,
- repeated stack traces,
- deadlock information,
- pool threads waiting,
- one thread continuously running expensive code.

---

# 44. ExecutorService and Thread Pool Problems

Typical issue:

```java
ExecutorService pool =
    Executors.newFixedThreadPool(5);
```

If five tasks block indefinitely, new tasks queue but never execute.

Investigate:

```text
pool size
active threads
queue size
task duration
timeouts
blocked I/O
rejections
```

Always think about:

- bounded queues,
- timeouts,
- rejection policies,
- shutdown behavior.

---

# 45. CompletableFuture Debugging

Async code separates the point where work starts from the point where failure becomes visible.

Example:

```java
CompletableFuture
    .supplyAsync(this::loadData)
    .thenApply(this::transform)
    .thenAccept(this::save);
```

Exceptions may be wrapped.

Useful pattern:

```java
future.exceptionally(ex -> {
    log.error("Async pipeline failed", ex);
    return fallback;
});
```

Debug each stage independently.

Name thread pools when possible so thread dumps and logs are easier to understand.

---

# 46. Memory Debugging

Memory problems include:

- heap growth,
- memory leak,
- excessive allocations,
- retained caches,
- thread-local leaks,
- classloader leaks,
- direct memory exhaustion.

Important memory areas include:

```text
Java heap
Metaspace
Thread stacks
Direct/native memory
Code cache
```

Not every memory problem is a Java heap problem.

---

# 47. OutOfMemoryError

Common forms include:

```text
Java heap space
GC overhead limit exceeded
Metaspace
Unable to create native thread
Direct buffer memory
```

Each suggests a different investigation.

## Java heap space

Possible causes:

- heap genuinely too small,
- memory leak,
- unexpectedly large workload,
- massive object graph,
- unbounded cache.

## Unable to create native thread

Possible causes:

- too many threads,
- OS process/thread limits,
- native memory pressure.

Do not automatically solve every OOM by increasing `-Xmx`.

First determine **why memory demand is high**.

---

# 48. Memory Leaks

Java has garbage collection, but Java applications can still leak memory.

A leak happens when objects remain reachable even though the application no longer needs them.

Example:

```java
static final List<byte[]> CACHE = new ArrayList<>();

void process() {
    CACHE.add(new byte[1024 * 1024]);
}
```

Because the static list keeps references, the arrays cannot be collected.

## Common leak sources

- static collections,
- unbounded caches,
- listeners never removed,
- ThreadLocal values,
- classloader references,
- sessions,
- maps keyed by unique IDs,
- queued tasks.

---

# 49. Heap Dumps

A heap dump captures objects currently in Java heap memory.

Useful questions:

```text
Which classes use the most memory?
Which objects have the largest retained size?
Why is this object still reachable?
What is retaining millions of objects?
```

Heap dumps can be analyzed with tools such as:

- Eclipse Memory Analyzer,
- VisualVM,
- other JVM memory-analysis tools.

## Important concepts

### Shallow size

Memory occupied directly by an object.

### Retained size

Memory that would become collectible if the object were removed.

### GC roots

Starting points the garbage collector treats as reachable.

Examples include:

- thread stacks,
- static fields,
- JNI references.

---

# 50. Garbage Collection Debugging

GC problems can cause:

- high CPU,
- latency spikes,
- long pauses,
- low throughput,
- OOM after repeated collections.

Questions:

```text
How often is GC running?
How much memory is reclaimed?
Are old-generation collections frequent?
Are pauses too long?
Does heap continue growing after full GC?
```

Use JVM-supported GC logging and diagnostic tools appropriate for your JDK.

Do not tune GC blindly.

First understand the application workload and allocation behavior.

---

# 51. JVM Diagnostic Tools

The JDK ships with diagnostic tools that are extremely valuable when an application is already running and attaching an interactive debugger is unsafe or impractical.

Common tools include:

```text
jcmd
jstack
jmap
jstat
jps
jfr
```

Availability and exact commands vary by JDK distribution and release. Always check the tools present on the actual runtime machine.

## 51.1 Prefer evidence before intervention

For production incidents, begin with low-risk observations:

```text
process identity
JVM command line
thread states
GC behavior
CPU
memory trend
JFR/metrics
application logs
```

Avoid immediately forcing full garbage collections or heap dumps on a critical process without understanding the impact.

## 51.2 `jcmd` as a diagnostic front door

`jcmd` can list JVMs and send supported diagnostic commands to a target JVM.

Discover commands on the actual JVM:

```bash
jcmd <pid> help
```

Get help for one command:

```bash
jcmd <pid> help Thread.print
```

Useful command availability is runtime-specific, so this discovery step is more reliable than memorizing every option.

---
# 52. `jps`

`jps` lists Java processes visible to the tool.

Basic use:

```bash
jps
```

Show more identifying information:

```bash
jps -l
```

This can help you find the PID before using another diagnostic tool.

Example:

```text
18420 com.example.Application
19102 jdk.jcmd/sun.tools.jps.Jps
```

## Important limitations

Do not assume `jps` always finds every Java process in containers, restricted environments, or across different users.

Also verify the target with operating-system tools such as:

```bash
ps
```

on Unix-like systems, or the appropriate process viewer on Windows.

The important goal is not "find a Java-looking PID." It is to prove you are diagnosing the correct process.

---
# 53. `jcmd`

`jcmd` sends diagnostic command requests to a running JVM.

List visible JVMs:

```bash
jcmd -l
```

or simply:

```bash
jcmd
```

List supported commands for one JVM:

```bash
jcmd <pid> help
```

## 53.1 Thread dump

```bash
jcmd <pid> Thread.print
```

Use this for:

- deadlocks,
- thread-pool starvation,
- blocked threads,
- request hangs,
- high-CPU thread investigation.

## 53.2 Class histogram

A commonly available diagnostic command is:

```bash
jcmd <pid> GC.class_histogram
```

This helps identify object counts and approximate memory usage by class.

A histogram is not the same as a heap dump. It gives a summary, not the complete object graph.

## 53.3 Heap dump

On supported HotSpot JVMs, a heap dump can be requested with the JVM's available `GC.heap_dump` diagnostic command.

Before using it:

```bash
jcmd <pid> help GC.heap_dump
```

Follow the syntax reported by that JVM.

Heap dumps can be large and operationally expensive. Confirm free disk space, storage permissions, and incident impact first.

## 53.4 Java Flight Recorder

Check recording support/options:

```bash
jcmd <pid> help JFR.start
```

Typical lifecycle:

```text
JFR.start
→ collect evidence
→ JFR.check
→ JFR.dump or JFR.stop
→ analyze .jfr file in JMC or another compatible tool
```

JFR is often a better production diagnostic starting point than attaching an interactive debugger because it records many JVM/application events with controlled configuration.

## 53.5 Same-user / same-host considerations

Diagnostic attachment can be restricted by operating-system permissions, container boundaries, and JVM settings.

If `jcmd` cannot see or attach to the target, verify:

- same host/container namespace,
- effective user,
- JDK tools available,
- target JVM compatibility,
- security restrictions.

---
# 54. `jstack`

`jstack` prints Java thread stack traces for a target JVM process.

Basic use:

```bash
jstack <pid>
```

Save for comparison:

```bash
jstack <pid> > threads-1.txt
```

For many modern HotSpot troubleshooting workflows, this can also be collected through:

```bash
jcmd <pid> Thread.print
```

## What to look for

A thread dump shows thread names, states, and stack frames.

Investigate patterns such as:

```text
many request threads BLOCKED on the same monitor
many worker threads waiting on one future
all pool threads occupied by slow external calls
same RUNNABLE stack repeated in multiple dumps
deadlock information
```

## Take multiple dumps

One thread dump is a snapshot.

For intermittent hangs or high CPU, take several dumps separated by a short interval and compare them.

A thread repeatedly stuck in the same stack is stronger evidence than a single momentary state.

## Warning

Thread dumps can include class names, file paths, request-processing details, and sometimes values embedded in thread names. Treat production dumps as potentially sensitive diagnostic artifacts.

---
# 55. `jmap`

`jmap` is a JDK diagnostic utility associated with heap and object-memory inspection on supported JVMs.

Typical use cases include:

- heap information,
- object histograms,
- heap dump generation on supported runtimes.

However, JVM diagnostic tooling evolves across JDK releases. For modern HotSpot environments, also learn the equivalent `jcmd` diagnostic commands and prefer the command supported and recommended for your actual JDK.

## Before creating a heap dump

Ask:

```text
Do I have enough disk space?
Can this pause or stress the target process?
Does the dump contain secrets or personal data?
Where will the dump be stored?
Who can access it?
```

A heap dump may contain:

- passwords,
- tokens,
- HTTP payloads,
- user data,
- cached records,
- cryptographic material.

Protect it like sensitive production data.

## Analysis

The dump itself is only evidence.

Use a heap analysis tool to investigate:

```text
largest retained objects
dominator tree
GC roots
unexpected object counts
retained collections/caches
class-loader retention
```

Do not conclude "memory leak" only because one class has many instances; determine why those objects remain reachable.

---
# 56. `jstat`

`jstat` samples JVM performance statistics.

A common GC-oriented command is:

```bash
jstat -gc <pid> 1000
```

The final number is the sampling interval in milliseconds.

This can help observe trends such as:

- young/old generation occupancy,
- collection counts,
- collection time,
- changing GC behavior.

## How to use it

Do not interpret one row in isolation.

Collect a short time series and correlate it with:

```text
request load
latency
CPU
application logs
heap usage
GC logs/JFR
```

For example, repeatedly growing old-generation occupancy plus frequent long collections may justify deeper memory analysis.

## Limitation

`jstat` field names and behavior are JVM/JDK-specific implementation details. Use:

```bash
jstat -options
```

and the documentation/help for the installed JDK.

For long-term production monitoring, application/JVM metrics systems are usually more appropriate than leaving an ad-hoc terminal sampling command running forever.

---
# 57. JConsole, VisualVM, JFR, and JMC

These tools overlap, but they are not identical.

| Tool | Strong use |
|---|---|
| JConsole | JMX-based monitoring and management |
| VisualVM | Visual JVM/process inspection and profiling workflows |
| JFR | JVM event recording |
| JMC | Rich analysis of Java Flight Recorder data |

## 57.1 JConsole

JConsole can connect to JVM management data through JMX.

Useful areas include:

- memory pools,
- threads,
- classes,
- MBeans,
- basic runtime monitoring.

Treat remote JMX configuration as a security-sensitive production change.

## 57.2 VisualVM

VisualVM provides a graphical view of JVM processes and can help inspect:

- CPU behavior,
- memory,
- threads,
- heap dumps,
- profiling/sampling depending on setup.

It is particularly useful for developers who are learning to connect JVM metrics with source-level behavior.

## 57.3 Java Flight Recorder (JFR)

JFR records JVM and application events into a `.jfr` recording.

It is useful for investigating:

- CPU hotspots,
- allocation pressure,
- locks,
- thread scheduling,
- garbage collection,
- I/O,
- latency-related events,
- JVM internals.

The exact event set depends on runtime/version and recording settings.

## 57.4 Java Mission Control (JMC)

JMC is a graphical analysis tool commonly used to inspect JFR recordings.

A practical workflow is:

```text
capture representative JFR
→ open in JMC
→ inspect automated/general findings
→ correlate CPU, allocations, locks, GC, and threads
→ return to code with a specific hypothesis
```

## 57.5 Do not collect everything blindly

More events are not automatically better.

Choose a recording duration and settings appropriate to:

- the symptom,
- production overhead tolerance,
- storage limits,
- privacy/security requirements.

For exact JFR commands supported by your JVM:

```bash
jcmd <pid> help JFR.start
```

---
# 58. CPU and Performance Debugging

Suppose CPU reaches 100%.

Do not immediately optimize random code.

Investigate.

## Workflow

1. Identify the Java process.
2. Identify hot threads.
3. Capture thread dumps or a profiling/JFR recording.
4. Find repeatedly executing stack frames.
5. Correlate with workload.
6. Reproduce if possible.
7. Optimize based on measurement.

## Common causes

- infinite loop,
- excessive retries,
- expensive regex,
- serialization,
- inefficient algorithm,
- too many allocations,
- busy waiting,
- excessive GC,
- runaway logging.

---

# 59. Remote Debugging

The JVM supports remote debugging through JDWP.

A commonly used agent configuration shape is:

```text
-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:5005
```

The exact secure configuration depends on environment and JDK behavior.

Then the IDE attaches to the configured host/port.

## Important security warning

A debug port can provide extremely powerful access to the JVM.

Do not expose it publicly.

Use:

- firewall rules,
- private network,
- SSH tunnel,
- VPN,
- short-lived debugging sessions,
- access controls.

Avoid production remote debugging unless absolutely necessary and properly secured.

---

# 60. Debugging in Docker and Containers

Containerized Java introduces additional variables:

```text
image
container filesystem
environment variables
network
ports
CPU limits
memory limits
JVM container awareness
mounted volumes
service discovery
```

## Useful checks

```bash
docker ps
docker logs <container>
docker inspect <container>
```

Enter a running container when appropriate:

```bash
docker exec -it <container> sh
```

or:

```bash
docker exec -it <container> bash
```

if the image contains Bash.

## Common bug

Application listens on:

```text
127.0.0.1
```

inside the container, but should accept connections through the container interface.

Another common issue:

```text
container memory limit < expected JVM memory requirement
```

---

# 61. Debugging Environment and Configuration Problems

A program can work locally and fail elsewhere because the environments differ.

Compare:

```text
JDK version
OS
architecture
timezone
locale
environment variables
system properties
working directory
filesystem permissions
database
network
dependency versions
configuration files
Spring profiles
container limits
```

## Print configuration safely

Example:

```java
log.info("Active profile={}", activeProfile);
log.info("Java version={}", System.getProperty("java.version"));
```

Do not print secrets.

---

# 62. Classpath and Dependency Debugging

Typical errors:

```text
ClassNotFoundException
NoClassDefFoundError
NoSuchMethodError
NoSuchFieldError
```

These can indicate dependency/classpath problems.

## `ClassNotFoundException`

A class loader attempted to load a class but could not find it.

## `NoClassDefFoundError`

A class needed at runtime could not be defined/loaded, sometimes because initialization previously failed.

## `NoSuchMethodError`

Often means the application was compiled against one version of a dependency but runs with another incompatible version.

Debug by checking:

- resolved dependency tree,
- packaged JAR contents,
- runtime classpath,
- duplicate JARs,
- application server libraries.

---

# 63. Build Tool Debugging: Maven

Useful commands include:

```bash
mvn test
mvn package
mvn dependency:tree
mvn help:effective-pom
```

For more diagnostics:

```bash
mvn -X ...
```

Use verbose debug output selectively because it can be very large and may expose configuration details.

## Dependency conflict workflow

```text
NoSuchMethodError
  ↓
mvn dependency:tree
  ↓
Find duplicate/conflicting versions
  ↓
Understand dependency mediation
  ↓
Align versions or exclude intentionally
```

---

# 64. Build Tool Debugging: Gradle

Useful commands include:

```bash
./gradlew test
./gradlew build
./gradlew dependencies
```

For a specific dependency configuration, use Gradle dependency-reporting tools appropriate to the project.

Useful diagnostics may include:

```text
--stacktrace
--info
--debug
```

Use progressively:

```text
normal
→ --stacktrace
→ --info
→ --debug
```

rather than starting with maximum output.

---

# 65. Class Loading Problems

Java applications may use multiple class loaders.

Class-loading bugs are common in:

- application servers,
- plugin architectures,
- hot-reload systems,
- containers,
- modular applications.

Two classes with the same fully qualified name loaded by different class loaders can be considered different runtime types.

Debug:

```java
System.out.println(
    SomeClass.class.getClassLoader()
);
```

Also inspect:

```text
runtime classpath
JAR location
duplicate classes
server-provided libraries
```

---

# 66. Reflection Debugging

Reflection hides some compile-time safety.

Example:

```java
Method method =
    clazz.getMethod("calculate", int.class);

Object result =
    method.invoke(instance, 10);
```

Possible failures:

```text
NoSuchMethodException
IllegalAccessException
InvocationTargetException
```

`InvocationTargetException` often wraps the exception thrown by the invoked method.

Inspect:

```java
e.getCause()
```

or the underlying target exception.

---

# 67. Generics Debugging

Generics can become confusing because of type erasure and unchecked casts.

Warning example:

```java
List raw = new ArrayList();
raw.add("hello");

List<Integer> numbers = raw;
```

This may compile with warnings and fail later.

Treat unchecked warnings seriously.

Prefer:

```java
List<String> values = new ArrayList<>();
```

from the start.

---

# 68. Lambda and Stream Debugging

Streams are concise but long chains can be hard to debug.

Example:

```java
users.stream()
    .filter(User::isActive)
    .map(User::getEmail)
    .filter(Objects::nonNull)
    .map(String::trim)
    .forEach(this::send);
```

If something is wrong, temporarily split stages:

```java
Stream<User> active =
    users.stream().filter(User::isActive);

Stream<String> emails =
    active.map(User::getEmail);

Stream<String> nonNull =
    emails.filter(Objects::nonNull);

Stream<String> trimmed =
    nonNull.map(String::trim);

trimmed.forEach(this::send);
```

Or use a debugger breakpoint inside lambda bodies.

## Be careful with `peek()`

`peek()` is primarily intended for observing stream elements in a pipeline, but relying on it as business logic is a mistake.

---

# 69. Debugging Recursive Algorithms

Example:

```java
int factorial(int n) {
    return n * factorial(n - 1);
}
```

Missing base case causes stack overflow.

Correct:

```java
int factorial(int n) {
    if (n <= 1) {
        return 1;
    }

    return n * factorial(n - 1);
}
```

When debugging recursion, track:

```text
current parameter
base condition
return value
depth
```

IDE call stacks make recursive execution easier to visualize.

---

# 70. Debugging Data Structures and Algorithms

For algorithm bugs, use small input.

Instead of debugging:

```text
1,000,000 elements
```

reduce to:

```text
5–10 elements
```

Example sorting input:

```text
[4, 2, 3, 1]
```

Record state after each iteration.

For binary search, inspect:

```text
low
high
mid
array[mid]
target
```

For graph algorithms:

```text
visited
queue/stack
current node
parent
distance
```

---

# 71. Production Debugging

Production debugging should be evidence-driven and low-risk.

Your goals are:

1. understand impact,
2. stabilize service,
3. collect evidence,
4. identify cause,
5. fix safely,
6. prevent recurrence.

Production is not the place for random code changes.

Useful evidence:

```text
logs
metrics
traces
thread dumps
heap dumps
JFR
deployment history
configuration changes
database metrics
network metrics
request IDs
```

---

# 72. Safe Production Troubleshooting

Avoid dangerous actions such as:

```text
restart repeatedly without collecting evidence
delete files blindly
change JVM flags randomly
enable full TRACE logging everywhere
run expensive heap operations without considering impact
expose debug ports publicly
modify production data to "test"
```

Before restarting a hung JVM, when possible collect:

- thread dumps,
- process metrics,
- relevant logs,
- JFR,
- heap information if memory is the issue.

A restart may remove the evidence.

---

# 73. Observability: Logs, Metrics, Traces

Debugging production systems is much easier with observability.

## Logs

Explain individual events.

```text
Order 1001 failed validation.
```

## Metrics

Show numeric behavior over time.

```text
requests/second
error rate
CPU
heap usage
GC pause
database latency
```

## Traces

Show how one request moves through multiple services.

```text
API Gateway
  → Order Service
      → Payment Service
          → Bank API
```

Good systems use all three.

---

# 74. Security-Sensitive Debugging

Debugging can accidentally expose sensitive information.

Avoid recording:

```text
passwords
JWTs
session IDs
API keys
authorization headers
database passwords
private keys
financial data
sensitive personal information
```

Use masking where needed:

```text
card=**** **** **** 1234
```

Do not copy production secrets into public bug reports or AI prompts.

---

# 75. Debugging Patterns and Anti-Patterns

## Good patterns

### Reproduce first

Do not change code before understanding the behavior when reproduction is possible.

### Change one variable at a time

If you change five things, you do not know which change mattered.

### Keep evidence

Save:

```text
stack trace
failing input
logs
request ID
test case
```

### Write regression tests

Once fixed, prevent the same bug from returning.

---

## Anti-pattern: swallow exceptions

Bad:

```java
try {
    process();
} catch (Exception e) {
}
```

---

## Anti-pattern: log and throw repeatedly

Bad:

```java
catch (Exception e) {
    log.error("Failed", e);
    throw e;
}
```

if every layer repeats the same logging. This can produce duplicate noisy stack traces.

Choose deliberate logging boundaries.

---

## Anti-pattern: catch `Throwable`

Usually avoid:

```java
catch (Throwable t)
```

because this catches serious JVM errors too.

---

## Anti-pattern: random sleeps

Adding:

```java
Thread.sleep(1000);
```

to “fix” race conditions is usually hiding the real synchronization problem.

---

# 76. Scientific Debugging

Treat debugging as hypothesis testing.

Bug:

```text
User login occasionally fails.
```

Weak approach:

```text
Maybe database.
Maybe cache.
Maybe token.
Maybe browser.
```

Scientific approach:

## Observation

```text
Failure happens only after token refresh.
```

## Hypothesis

```text
Refreshed token is not persisted correctly.
```

## Experiment

Log safe token metadata:

```text
issuedAt
expiresAt
userId
refresh result
```

## Result

The refreshed expiry is already in the past because of timezone conversion.

Now you have evidence.

---

# 77. Binary Search Debugging

When a large code path contains the bug, divide it in half.

Suppose:

```text
Input
 → A
 → B
 → C
 → D
 → E
 → Output
```

Expected output is wrong.

Check value after `C`.

If correct:

```text
bug is probably D or E
```

If incorrect:

```text
bug is probably A, B, or C
```

Repeat.

This technique is extremely effective in large transformations.

---

# 78. Rubber Duck Debugging

Explain the code line by line as if teaching someone who knows nothing about it.

Example:

```text
This variable contains quantity.
Then I multiply...
Wait. I am adding price instead of multiplying.
```

Many logical mistakes become obvious when spoken or written in plain language.

---

# 79. Minimal Reproducible Examples

A minimal reproducible example is the smallest code/data setup that still demonstrates the bug.

Instead of sharing:

```text
200 classes
Spring Boot
Database
Kafka
Docker
Redis
```

reduce to:

```java
public class BugDemo {
    public static void main(String[] args) {
        // minimum code that fails
    }
}
```

Benefits:

- easier reasoning,
- faster testing,
- easier bug reports,
- easier team collaboration.

---

# 80. Debugging Legacy Code

Legacy code may have:

- few tests,
- shared mutable state,
- giant methods,
- hidden side effects,
- unclear naming.

Safe workflow:

1. reproduce behavior,
2. create characterization tests,
3. add logging/breakpoints,
4. understand current behavior,
5. make the smallest safe change,
6. run regression tests,
7. refactor separately from behavior change when possible.

A characterization test records what the code currently does, even if the behavior is strange.

---

# 81. Scenario Playbooks

## Scenario A — Application does not compile

Checklist:

```text
Read first compiler error
Check source line
Check variable/method spelling
Check imports
Check types
Check method parameters
Check braces and semicolons
Recompile
```

---

## Scenario B — Application crashes on startup

Checklist:

```text
Read full stack trace
Find root cause / caused-by chain
Check configuration
Check port conflicts
Check database connection
Check missing dependencies
Check environment variables
Check active profile
```

---

## Scenario C — API returns HTTP 500

Checklist:

```text
Find request ID
Find server exception
Identify controller/service/repository boundary
Inspect input
Inspect database/external service calls
Reproduce locally/test environment
Add regression test
```

---

## Scenario D — Works locally, fails on server

Compare:

```text
JDK version
OS
filesystem path
permissions
timezone
locale
environment variables
database
network
dependency packaging
configuration
container limits
```

---

## Scenario E — Application hangs

Collect:

```text
thread dumps
CPU usage
JFR if possible
request/thread pool metrics
database connection pool metrics
```

Look for:

```text
deadlock
blocked I/O
thread starvation
infinite loop
external timeout
```

---

## Scenario F — Memory keeps increasing

Investigate:

```text
heap after GC
allocation rate
object histogram
heap dump
cache sizes
sessions
queues
ThreadLocal
static collections
```

---

## Scenario G — CPU is 100%

Investigate:

```text
hot threads
repeated stack traces
JFR/profile
GC CPU
retry loops
regex
serialization
infinite loop
```

---

## Scenario H — Database connections exhausted

Inspect:

```text
active connections
idle connections
waiters
connection timeout
long transactions
unclosed connections
slow queries
pool size
database limit
```

Ensure resources are closed properly.

---

## Scenario I — Random duplicate records

Investigate:

```text
request retries
missing idempotency
race conditions
transaction isolation
duplicate message delivery
double-click/user retries
unique constraints
```

---

## Scenario J — Only one customer/order fails

Use:

- conditional breakpoint,
- request-specific logs,
- exact failing input,
- database row comparison.

Avoid testing only with generic sample data.

---

# 82. Common Java Error Reference

| Error / Exception | Typical area to inspect |
|---|---|
| `NullPointerException` | unexpected null |
| `ArrayIndexOutOfBoundsException` | invalid array index |
| `IndexOutOfBoundsException` | invalid list/string index |
| `NumberFormatException` | invalid numeric input |
| `ClassCastException` | wrong runtime type |
| `IllegalArgumentException` | invalid parameter |
| `IllegalStateException` | invalid object/application state |
| `ConcurrentModificationException` | mutation during iteration |
| `StackOverflowError` | recursion/call cycle |
| `OutOfMemoryError` | heap/native/metaspace/thread resources |
| `ClassNotFoundException` | classloader/classpath |
| `NoClassDefFoundError` | runtime class definition/loading |
| `NoSuchMethodError` | dependency version mismatch |
| `SQLException` | SQL/database/connection |
| `ConnectException` | network endpoint unavailable |
| `SocketTimeoutException` | network timeout |
| `FileNotFoundException` | missing file/path/permissions |
| `AccessDeniedException` | filesystem permissions |
| `BeanCreationException` | Spring bean initialization |
| `UnsatisfiedDependencyException` | Spring injection dependency |
| `LazyInitializationException` | JPA session/transaction boundary |

---

# 83. Debugging Checklist

When something fails:

- [ ] Can I reproduce the problem?
- [ ] What exactly did I expect?
- [ ] What actually happened?
- [ ] What is the smallest failing input?
- [ ] Did I read the complete error?
- [ ] Did I read the complete stack trace?
- [ ] What is the first relevant application frame?
- [ ] What values were passed into that method?
- [ ] Where does the data first become incorrect?
- [ ] Did I check environment/configuration?
- [ ] Did I change only one thing at a time?
- [ ] Did I verify the root cause rather than only the symptom?
- [ ] Did I create a regression test?
- [ ] Did I remove temporary debug output?
- [ ] Did I ensure logs do not expose secrets?

---

# 84. Production Incident Checklist

- [ ] Identify affected users/services.
- [ ] Determine severity and impact.
- [ ] Record exact start time.
- [ ] Check recent deployments/configuration changes.
- [ ] Capture relevant logs.
- [ ] Capture metrics.
- [ ] Capture request/trace IDs.
- [ ] Capture thread dumps for hangs/CPU/thread issues.
- [ ] Capture memory evidence for memory issues.
- [ ] Consider JFR for JVM/performance issues.
- [ ] Avoid destructive debugging actions.
- [ ] Stabilize the system when necessary.
- [ ] Identify root cause.
- [ ] Validate the fix.
- [ ] Add monitoring/tests.
- [ ] Document prevention actions.

---

# 85. Beginner Exercises

## Exercise 1 — Wrong arithmetic

Find the bug:

```java
public static int area(int width, int height) {
    return width + height;
}
```

Expected:

```text
width=5
height=4
area=20
```

---

## Exercise 2 — Null value

```java
String name = null;
System.out.println(name.toUpperCase());
```

Questions:

1. Which exception occurs?
2. Where should validation happen?
3. Is null valid in the domain?

---

## Exercise 3 — Index problem

```java
List<String> values =
    List.of("A", "B", "C");

for (int i = 0; i <= values.size(); i++) {
    System.out.println(values.get(i));
}
```

Find the off-by-one bug.

---

## Exercise 4 — Integer division

```java
double average = 5 / 2;
```

Why is the result not `2.5`?

---

## Exercise 5 — Stack trace practice

Given:

```text
java.lang.NumberFormatException: For input string: "12A"
    at java.base/java.lang.Integer.parseInt(...)
    at InvoiceParser.parseQuantity(InvoiceParser.java:42)
    at InvoiceService.importInvoice(InvoiceService.java:88)
```

Answer:

```text
Which method should you inspect first?
What input caused the failure?
Where did the input come from?
```

---

# 86. Intermediate Exercises

## Exercise 1 — Concurrent counter

Fix:

```java
class Counter {
    int count;

    void increment() {
        count++;
    }
}
```

when used by multiple threads.

---

## Exercise 2 — Resource handling

Improve:

```java
FileInputStream in =
    new FileInputStream("data.txt");

byte[] data = in.readAllBytes();
```

Ensure the stream is closed even when an exception occurs.

---

## Exercise 3 — N+1 problem

You load 1,000 orders and access each order's items.

Determine:

```text
How many SQL statements execute?
How would you measure this?
What fetch/query strategy is appropriate?
```

---

## Exercise 4 — Async exception

A `CompletableFuture` silently appears not to finish.

Add exception handling and logging.

---

## Exercise 5 — Dependency mismatch

The application starts with:

```text
NoSuchMethodError
```

Use Maven/Gradle dependency inspection to find version conflicts.

---

# 87. Advanced Exercises

## Exercise 1 — Memory leak

Create a test program with an unbounded static cache, run it with a controlled heap, capture a heap dump, and identify the retaining reference.

## Exercise 2 — Deadlock

Create two locks and two threads that acquire them in opposite order. Capture a thread dump and identify the deadlock.

## Exercise 3 — CPU hotspot

Write an intentionally expensive loop, capture a JFR recording, and identify the hot method.

## Exercise 4 — Thread pool starvation

Use a small fixed thread pool and submit blocking tasks. Observe queue growth and thread state.

## Exercise 5 — Production simulation

Build a small Spring Boot API that can intentionally:

- sleep,
- allocate memory,
- throw an exception,
- execute a slow query.

Practice using logs, metrics, thread dumps, and JFR to diagnose each mode.

---

# 88. Debugging Interview Questions

## Beginner

1. What is the difference between compile-time and runtime errors?
2. What is a stack trace?
3. What is a breakpoint?
4. Difference between Step Into and Step Over?
5. What causes `NullPointerException`?
6. What is a logical bug?
7. Why is `System.out.println()` not ideal for production logging?

## Intermediate

1. Difference between `ClassNotFoundException` and `NoClassDefFoundError`?
2. What usually causes `NoSuchMethodError`?
3. How do you debug a Spring Boot startup failure?
4. How do you investigate an API returning 500?
5. How do you debug an N+1 query problem?
6. What is a race condition?
7. What is a deadlock?

## Advanced

1. How do you investigate 100% CPU in a JVM?
2. How do you investigate heap growth?
3. When would you capture a thread dump?
4. What is retained heap?
5. What are GC roots?
6. How would you diagnose thread-pool starvation?
7. What is Java Flight Recorder useful for?
8. How would you debug an intermittent production problem without attaching an IDE?
9. Why can increasing `-Xmx` hide rather than solve a memory issue?
10. How do class-loader conflicts produce runtime type problems?

---

# 89. Command Cheat Sheet

## Compile with debug information

```bash
javac -g App.java
```

## Run with assertions

```bash
java -ea App
```

## Start `jshell`

```bash
jshell
```

## Start `jdb`

```bash
jdb App
```

## List Java processes

```bash
jps -l
```

## List `jcmd` processes

```bash
jcmd
```

## Show commands available for a JVM

```bash
jcmd <pid> help
```

## Thread dump

```bash
jstack <pid>
```

## JVM GC statistics sampling

```bash
jstat -gc <pid> 1000
```

## Maven tests

```bash
mvn test
```

## Maven dependency tree

```bash
mvn dependency:tree
```

## Maven effective POM

```bash
mvn help:effective-pom
```

## Gradle tests

```bash
./gradlew test
```

## Gradle dependencies

```bash
./gradlew dependencies
```

## Docker logs

```bash
docker logs <container>
```

## Enter container

```bash
docker exec -it <container> sh
```

> **Note:** Diagnostic command support and exact options can vary by JDK and runtime environment. Use each command's built-in help on the actual machine you are debugging.

---

# 90. Glossary

## Breakpoint

A location where the debugger pauses program execution.

## Call stack

The chain of active method calls.

## Stack frame

The local execution context of one active method.

## Watch

An expression the debugger repeatedly evaluates while paused.

## Heap

The JVM memory area where most Java objects are allocated.

## Thread dump

A snapshot of JVM thread stacks and states.

## Heap dump

A snapshot of objects in Java heap memory.

## Race condition

A bug where behavior depends on timing between threads.

## Deadlock

Two or more threads wait indefinitely for each other's resources.

## Memory leak

Objects remain reachable even though the application no longer needs them.

## GC

Garbage collection — automatic reclamation of unreachable objects.

## GC root

A root reference from which object reachability is determined.

## JFR

Java Flight Recorder.

## JMC

Java Mission Control.

## JDWP

Java Debug Wire Protocol, used for debugger communication.

## Root cause

The underlying reason the bug exists, not merely the visible symptom.

## Regression

A previously working behavior becomes broken again.

## Reproducible case

A reliable sequence of actions/input that causes the failure.

## Observability

The ability to understand system behavior using logs, metrics, traces, and related telemetry.

---

# 91. Final Learning Path

Use this learning progression.

## Stage 1 — Beginner

Master:

```text
compiler errors
exceptions
stack traces
println debugging
breakpoints
step over
step into
variables
call stack
```

Practice on small console applications.

---

## Stage 2 — Application Developer

Master:

```text
logging
JUnit
Mockito
HTTP debugging
database debugging
Maven/Gradle
Spring Boot startup
JPA/Hibernate
configuration
```

Practice on CRUD and REST applications.

---

## Stage 3 — Advanced Java Developer

Master:

```text
threads
race conditions
deadlocks
thread dumps
heap dumps
GC
JVM diagnostics
class loading
remote debugging
```

---

## Stage 4 — Production Engineer

Master:

```text
JFR/JMC
profiling
observability
incident response
safe production diagnostics
performance analysis
memory analysis
distributed tracing
capacity/resource debugging
```

---

# Appendix A — A Complete Debugging Example

Consider:

```java
public class PaymentService {

    public double calculateFinalAmount(
            double amount,
            Integer discountPercent) {

        double discount =
            amount * discountPercent / 100;

        return amount - discount;
    }
}
```

Sometimes this throws:

```text
NullPointerException
```

## Step 1 — Reproduce

Input:

```text
amount = 1000
discountPercent = null
```

## Step 2 — Understand why

Java unboxes:

```java
Integer
```

into:

```java
int
```

during arithmetic.

Unboxing `null` throws `NullPointerException`.

## Step 3 — Determine business rule

Question:

```text
Does null mean no discount?
Or is null invalid?
```

### Option A — null means zero discount

```java
int percent =
    discountPercent == null
        ? 0
        : discountPercent;
```

### Option B — null is invalid

```java
Objects.requireNonNull(
    discountPercent,
    "discountPercent must not be null"
);
```

The correct fix depends on the domain, not only the exception.

## Step 4 — Add tests

```java
@Test
void nullDiscountUsesZeroWhenAllowed() {
    assertEquals(
        1000.0,
        service.calculateFinalAmount(1000, null)
    );
}
```

This is the difference between merely silencing an error and designing a correct fix.

---

# Appendix B — Debugging a Wrong Result Step by Step

Bug:

```java
public double calculateAverage(
        int total,
        int count) {

    return total / count;
}
```

Input:

```text
total = 5
count = 2
```

Expected:

```text
2.5
```

Actual:

```text
2.0
```

## Investigation

Both operands are `int`.

```java
5 / 2
```

is integer division:

```text
2
```

Then Java converts `2` to:

```text
2.0
```

Fix:

```java
return (double) total / count;
```

Test:

```java
assertEquals(
    2.5,
    calculateAverage(5, 2),
    0.000001
);
```

---

# Appendix C — Debugging a Slow Loop

Suppose:

```java
for (Order order : orders) {
    User user =
        userRepository.findById(order.getUserId());

    enrich(order, user);
}
```

For:

```text
100,000 orders
```

this may cause up to 100,000 user lookups.

## Debugging evidence

Measure:

```text
method execution time
query count
database latency
CPU
allocation rate
```

Possible improvements depend on semantics:

- batch query,
- join,
- bulk load,
- cache repeated users,
- restructure algorithm.

Never optimize before confirming the bottleneck.

---

# Appendix D — Debugging a Deadlock Example

```java
public class DeadlockDemo {

    private final Object lockA = new Object();
    private final Object lockB = new Object();

    void first() {
        synchronized (lockA) {
            sleep();

            synchronized (lockB) {
                System.out.println("first");
            }
        }
    }

    void second() {
        synchronized (lockB) {
            sleep();

            synchronized (lockA) {
                System.out.println("second");
            }
        }
    }

    private void sleep() {
        try {
            Thread.sleep(100);
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
    }
}
```

Potential lock order:

```text
Thread 1: A → B
Thread 2: B → A
```

Fix by using consistent ordering:

```text
A → B
```

everywhere.

---

# Appendix E — Debugging Logging Strategy

Avoid producing logs like:

```text
start
inside
value
here
error
done
```

These are difficult to understand in multi-threaded systems.

Prefer:

```text
requestId=abc123 event=order_validation_started orderId=5001
requestId=abc123 event=order_validation_failed orderId=5001 reason=missing_customer
```

Useful context may include:

```text
request ID
trace ID
user ID when permitted
order ID
job ID
service name
operation name
duration
result
```

Do not log sensitive data unnecessarily.

---

# Appendix F — Questions to Ask Before You Fix a Bug

Before changing code, answer as many as possible:

1. Can I reproduce it?
2. Is it deterministic?
3. Which exact input causes it?
4. Which environment?
5. Which application version?
6. Did it ever work?
7. What changed?
8. Which request/job/user is affected?
9. Is there a stack trace?
10. What is the earliest suspicious value?
11. Is the issue code, data, configuration, environment, dependency, or infrastructure?
12. Does the same input fail in a unit test?
13. Is concurrency involved?
14. Is time/timezone involved?
15. Is the failure actually downstream?
16. What evidence would prove my hypothesis?
17. Can I write a test before fixing it?
18. Will the fix change public behavior?
19. Could the fix introduce another edge case?
20. How will I monitor the fix after deployment?

---

# Appendix G — Master Rule Set

Remember these rules:

> **Read the entire error before editing code.**

> **Reproduce before guessing whenever possible.**

> **Inspect data at boundaries.**

> **Find where the value first becomes wrong.**

> **Fix the root cause, not only the exception.**

> **Use the debugger for state, logs for history, tests for reproducibility, and JVM tools for runtime behavior.**

> **Collect evidence before restarting a production JVM.**

> **Never expose secrets while debugging.**

> **Every important bug fix should ideally produce a regression test or monitoring improvement.**

---

# Appendix H — Recommended Java Debugging Tools and Configuration

This appendix is a practical setup guide for the debugging tools referenced throughout the handbook.

## H.1 Beginner setup

Recommended baseline:

```text
JDK
+ IntelliJ IDEA or VS Code/Eclipse
+ JUnit
+ Maven or Gradle
+ Git
```

For JVM diagnostics, learn `jcmd`, thread dumps, JFR, and JMC after you are comfortable with source-level debugging.

## H.2 IntelliJ IDEA

No separate Java debugger extension is required.

Setup:

1. Configure the project SDK/JDK.
2. Import Maven/Gradle project metadata if applicable.
3. Set a breakpoint.
4. Start the application or test with **Debug**.
5. Inspect Frames and Variables.
6. Learn conditional and exception breakpoints.
7. Use **Evaluate Expression** to test a hypothesis without editing source.

When the source and runtime disagree, verify the module/classpath and that the running build was produced from the source you opened.

## H.3 VS Code extensions

The easiest complete Java setup is the **Extension Pack for Java**.

It includes the core language/debug/testing/project-management tooling needed for typical Java development, including **Debugger for Java**.

A simple launch configuration is:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "java",
      "name": "Debug Application",
      "request": "launch",
      "mainClass": "com.example.Application"
    }
  ]
}
```

Many simple projects do not need a manually written `launch.json`; create one when you need persistent custom settings.

## H.4 Eclipse

Eclipse Java tooling includes source-level debugging.

Recommended first features to learn:

```text
line breakpoint
conditional breakpoint
exception breakpoint
Step Over
Step Into
Step Return
Variables
Expressions
Debug/Threads view
```

Use a dedicated launch configuration when the application needs specific VM arguments, environment variables, classpath settings, or working directory.

## H.5 Remote debugging with JDWP

A development JVM can expose JDWP for a debugger to attach.

A commonly used modern syntax is:

```bash
java -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:5005 -jar app.jar
```

**Security warning:** `address=*:5005` listens beyond loopback on many systems. Use it only in a trusted/restricted development network or container setup.

For local-only debugging, prefer a loopback-bound configuration supported by your JDK/environment, or tunnel the port through SSH.

Typical IDE attach settings:

```text
host: localhost
port: 5005
```

If `suspend=y`, the JVM waits for a debugger before application execution continues. This is useful for startup bugs but can make a service appear hung if no debugger attaches.

## H.6 Maven and Gradle

### Maven

Compile/test evidence:

```bash
mvn test
mvn -X test
mvn dependency:tree
mvn help:effective-pom
```

Use `-X` only when Maven's own debug output is needed; it can be very verbose.

### Gradle

```bash
./gradlew test
./gradlew dependencies
./gradlew --stacktrace test
./gradlew --info test
```

Escalate to more verbose logging only when ordinary failure output is insufficient.

## H.7 JVM process and thread diagnosis

Identify JVMs:

```bash
jcmd -l
jps -l
```

List diagnostic commands:

```bash
jcmd <pid> help
```

Thread dump:

```bash
jcmd <pid> Thread.print
```

Alternative:

```bash
jstack <pid>
```

Take several thread dumps for intermittent hangs.

## H.8 JFR and JMC

Discover recording syntax on the target JVM:

```bash
jcmd <pid> help JFR.start
```

A typical workflow is:

```text
start recording
→ reproduce or wait for symptom
→ dump/stop recording
→ open .jfr in JMC
→ inspect CPU, allocation, GC, locks, threads, and latency evidence
```

Do not use an old JFR command copied from a different JDK without checking the target JVM's `jcmd` help.

## H.9 Heap analysis

Before a heap dump, check:

```text
free disk space
operational pause/overhead risk
file permissions
sensitive data handling
artifact transfer/storage policy
```

Then use the heap-dump mechanism supported by the actual JDK, and analyze the result with a compatible heap-analysis tool.

Questions to answer:

```text
Which objects retain the most memory?
What are their GC-root paths?
Is a cache unbounded?
Is a class loader retaining an old application?
Are queues/listeners/sessions growing?
```

## H.10 Static bug detection

Debuggers find runtime state; static analyzers can prevent common defects earlier.

Useful Java tool categories include:

- compiler warnings,
- IDE inspections,
- SpotBugs-style bytecode analysis,
- style/static rule tools,
- nullness/type analysis,
- dependency vulnerability scanning.

Use static-analysis findings as hypotheses. Not every warning is a runtime bug, and suppressions should be documented rather than used to silence unfamiliar results.

## H.11 Production diagnostic order

A safe default order is:

```text
1. Confirm impact and timeline
2. Check logs/metrics/traces
3. Identify correct JVM
4. Capture low-risk thread/runtime evidence
5. Use JFR when appropriate
6. Capture heap dump only when justified
7. Reproduce outside production
8. Apply fix + regression test
```

Interactive remote debugging is usually not the first production tool because pausing threads can affect users and change timing-sensitive behavior.

## H.12 Official references

- VS Code Java debugging: <https://code.visualstudio.com/docs/java/java-debugging>
- VS Code Java extensions: <https://code.visualstudio.com/docs/java/extensions>
- VS Code Java testing: <https://code.visualstudio.com/docs/java/java-testing>
- Oracle `jcmd` reference: <https://docs.oracle.com/en/java/javase/23/docs/specs/man/jcmd.html>
- Oracle `jstack` reference: <https://docs.oracle.com/en/java/javase/17/docs/specs/man/jstack.html>
- IntelliJ IDEA documentation: <https://www.jetbrains.com/help/idea/>
- Java Mission Control / Flight Recorder documentation: <https://docs.oracle.com/javacomponents/jmc/>

---

# End of Java Debugging Master Handbook
