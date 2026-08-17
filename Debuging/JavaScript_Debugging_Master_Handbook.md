# JavaScript Debugging Master Handbook

> **A beginner-friendly, practical, in-depth guide to finding, understanding, fixing, and preventing JavaScript bugs in browsers, Node.js, VS Code, APIs, asynchronous code, production applications, and real-world projects.**

---

## Table of Contents

1. [How to Use This Handbook](#1-how-to-use-this-handbook)
2. [What Debugging Really Means](#2-what-debugging-really-means)
3. [The JavaScript Execution Mental Model](#3-the-javascript-execution-mental-model)
4. [Types of JavaScript Bugs](#4-types-of-javascript-bugs)
5. [A Reliable Debugging Workflow](#5-a-reliable-debugging-workflow)
6. [Reading JavaScript Errors and Stack Traces](#6-reading-javascript-errors-and-stack-traces)
7. [Console Debugging](#7-console-debugging)
8. [Browser DevTools Overview](#8-browser-devtools-overview)
9. [Breakpoints](#9-breakpoints)
10. [Stepping Through Code](#10-stepping-through-code)
11. [Scope, Call Stack, Watch Expressions, and Closures](#11-scope-call-stack-watch-expressions-and-closures)
12. [Conditional Breakpoints and Logpoints](#12-conditional-breakpoints-and-logpoints)
13. [The `debugger` Statement](#13-the-debugger-statement)
14. [Source Maps, Bundled Code, and Minified Code](#14-source-maps-bundled-code-and-minified-code)
15. [Debugging Variables, Types, Coercion, and Data](#15-debugging-variables-types-coercion-and-data)
16. [Debugging Arrays and Objects](#16-debugging-arrays-and-objects)
17. [Debugging Functions, `this`, Closures, and Callbacks](#17-debugging-functions-this-closures-and-callbacks)
18. [Debugging DOM Problems](#18-debugging-dom-problems)
19. [Debugging Browser Events](#19-debugging-browser-events)
20. [Debugging Network Requests and APIs](#20-debugging-network-requests-and-apis)
21. [Debugging Promises and `async`/`await`](#21-debugging-promises-and-asyncawait)
22. [Debugging Timers, Race Conditions, and Concurrency](#22-debugging-timers-race-conditions-and-concurrency)
23. [Debugging Modules and Imports](#23-debugging-modules-and-imports)
24. [Debugging Browser Storage, Cookies, and Caching](#24-debugging-browser-storage-cookies-and-caching)
25. [Debugging Node.js Applications](#25-debugging-nodejs-applications)
26. [Debugging JavaScript in VS Code](#26-debugging-javascript-in-vs-code)
27. [Debugging with Tests](#27-debugging-with-tests)
28. [Error Handling as a Debugging Tool](#28-error-handling-as-a-debugging-tool)
29. [Debugging Memory Leaks](#29-debugging-memory-leaks)
30. [Debugging Performance Problems](#30-debugging-performance-problems)
31. [Debugging Web Workers and Service Workers](#31-debugging-web-workers-and-service-workers)
32. [Debugging Framework Applications](#32-debugging-framework-applications)
33. [Debugging Production Applications](#33-debugging-production-applications)
34. [Security-Sensitive Debugging](#34-security-sensitive-debugging)
35. [Real-World Debugging Scenarios](#35-real-world-debugging-scenarios)
36. [Common Debugging Anti-Patterns](#36-common-debugging-anti-patterns)
37. [Debugging Checklists](#37-debugging-checklists)
38. [Practice Labs](#38-practice-labs)
39. [JavaScript Debugging Cheat Sheet](#39-javascript-debugging-cheat-sheet)
40. [Glossary](#40-glossary)
41. [Final Debugging Mindset](#41-final-debugging-mindset)
42. [Appendix K: Recommended JavaScript Debugging Tools and Configuration](#appendix-k-recommended-javascript-debugging-tools-and-configuration)

---

# 1. How to Use This Handbook

This handbook is designed to be useful in three different ways:

- **Beginner learning:** read from the beginning and follow the examples.
- **Problem solving:** jump directly to the section that matches the bug you are facing.
- **Reference:** use the checklists and cheat sheet while debugging real projects.

The most important idea is this:

> Debugging is not guessing. Debugging is a process of collecting evidence until the cause of a problem becomes clear.

When you encounter a bug, do not immediately start changing random lines. First determine:

1. What did you expect?
2. What actually happened?
3. Where does reality first differ from your expectation?
4. What data reached that point?
5. What code produced that data?
6. Can the problem be reproduced consistently?
7. What is the smallest change that fixes the actual cause?

A professional debugger tries to **reduce uncertainty** step by step.

---

# 2. What Debugging Really Means

## 2.1 Definition

**Debugging** is the process of finding, understanding, and correcting defects in software.

A defect may be:

- invalid syntax,
- wrong logic,
- unexpected input,
- incorrect state,
- failed network communication,
- timing or race-condition behavior,
- memory growth,
- slow execution,
- bad configuration,
- incompatible environment,
- incorrect assumptions.

Debugging is broader than "fixing an error message." Some of the hardest bugs produce no error at all.

Example:

```js
function calculateDiscount(price) {
  return price * 20;
}

console.log(calculateDiscount(100));
```

The program runs successfully and prints:

```text
2000
```

But if the requirement is "20% discount", the logic is wrong.

Correct code:

```js
function calculateDiscount(price) {
  return price * 0.20;
}

console.log(calculateDiscount(100));
```

Output:

```text
20
```

There was no exception. This was a **logic bug**.

---

## 2.2 Debugging vs Testing

Testing and debugging are related but different.

| Activity | Main Question |
|---|---|
| Testing | Does the program behave correctly? |
| Debugging | Why does it behave incorrectly? |
| Logging | What happened while it ran? |
| Monitoring | Is the running system healthy? |
| Profiling | Where are time or resources being consumed? |

A test may tell you:

```text
Expected 10 but received 12
```

Debugging tells you **why** 12 was produced.

---

## 2.3 Debugging vs Troubleshooting

Troubleshooting is often broader.

Example:

A web page cannot load customer data.

Possible causes:

- frontend JavaScript bug,
- backend API error,
- authentication failure,
- CORS issue,
- expired token,
- DNS failure,
- browser extension,
- proxy,
- database timeout.

Debugging may focus on JavaScript code. Troubleshooting investigates the complete system.

In real development, you often do both.

---

# 3. The JavaScript Execution Mental Model

Understanding how JavaScript executes makes debugging much easier.

## 3.1 Source Code → Parsing → Execution

Before JavaScript runs, the engine must parse it.

Example:

```js
const name = "Shoeb";
console.log(name);
```

The engine:

1. reads the source,
2. parses the syntax,
3. creates internal structures,
4. prepares scopes,
5. executes statements,
6. calls functions,
7. manages memory,
8. schedules asynchronous callbacks when needed.

A syntax problem can prevent execution entirely.

---

## 3.2 Call Stack

JavaScript uses a **call stack** to track active function calls.

Example:

```js
function first() {
  second();
}

function second() {
  third();
}

function third() {
  console.log("Hello");
}

first();
```

Conceptually the stack becomes:

```text
first()
  second()
    third()
      console.log()
```

When `console.log()` completes, it returns. Then `third()`, `second()`, and `first()` return.

When an error occurs, the stack trace often shows this call path.

---

## 3.3 Scope

A scope determines where a variable can be accessed.

```js
const globalValue = "global";

function example() {
  const localValue = "local";

  console.log(globalValue);
  console.log(localValue);
}

example();
```

Inside `example()`, both variables are visible.

Outside it:

```js
console.log(localValue);
```

produces something like:

```text
ReferenceError: localValue is not defined
```

When debugging, inspect the scope where the code is paused.

---

## 3.4 Heap

Objects, arrays, functions, and many runtime values live in managed memory often described conceptually as the **heap**.

```js
const user = {
  id: 1,
  name: "Asha"
};
```

The variable `user` refers to an object in memory.

This matters when debugging:

- object mutation,
- shared references,
- memory leaks,
- unexpected state changes.

---

## 3.5 Event Loop

JavaScript can perform asynchronous work without blocking all execution.

Consider:

```js
console.log("A");

setTimeout(() => {
  console.log("B");
}, 0);

console.log("C");
```

Typical output:

```text
A
C
B
```

Why?

`setTimeout()` schedules work. It does not immediately execute the callback.

This execution model is essential when debugging:

- promises,
- timers,
- API requests,
- UI events,
- race conditions.

---

## 3.6 Microtasks and Tasks

Promise callbacks are normally scheduled as **microtasks**, while timers are scheduled as tasks.

Example:

```js
console.log("start");

setTimeout(() => console.log("timer"), 0);

Promise.resolve().then(() => {
  console.log("promise");
});

console.log("end");
```

Typical output:

```text
start
end
promise
timer
```

A common debugging mistake is assuming "0 ms" means "run immediately."

It means "eligible to run after the current execution and after higher-priority queued work such as pending microtasks."

---

# 4. Types of JavaScript Bugs

Understanding the category helps you choose the correct debugging tool.

## 4.1 Syntax Errors

A syntax error means the parser cannot understand the code.

```js
if (true {
  console.log("hello");
}
```

Problem: missing `)`.

Typical error:

```text
SyntaxError: Unexpected token '{'
```

Use:

- editor diagnostics,
- browser Console,
- Node.js error output,
- linting.

---

## 4.2 Reference Errors

A reference error usually means code refers to a variable that does not exist in the current scope.

```js
console.log(total);
```

Possible output:

```text
ReferenceError: total is not defined
```

Questions to ask:

- Was the variable declared?
- Is the spelling correct?
- Is it in another scope?
- Does it execute before initialization?
- Was an import forgotten?

---

## 4.3 Type Errors

A type error often occurs when a value does not support the operation being used.

```js
const user = null;
console.log(user.name);
```

Possible output:

```text
TypeError: Cannot read properties of null
```

The important evidence is not only the failing property access. Ask:

> Why was `user` null at this moment?

The root cause may be much earlier.

---

## 4.4 Range Errors

Example:

```js
const array = new Array(-1);
```

Possible output:

```text
RangeError: Invalid array length
```

Range errors can also arise from excessive recursion.

---

## 4.5 Logic Errors

The code runs but calculates the wrong result.

```js
function isAdult(age) {
  return age > 18;
}
```

If the requirement says age 18 is an adult, this is wrong.

Correct:

```js
return age >= 18;
```

---

## 4.6 State Bugs

An application may contain valid code but incorrect application state.

Example:

```js
let cartCount = 0;

function addItem() {
  cartCount++;
}

function resetView() {
  cartCount = 0; // accidental state loss
}
```

A UI may suddenly show `0` after navigation.

Debugging requires watching **when state changes**.

---

## 4.7 Timing Bugs

Example:

```js
let user;

fetch("/api/user")
  .then(response => response.json())
  .then(data => {
    user = data;
  });

console.log(user);
```

`console.log(user)` may print:

```text
undefined
```

The log executes before the request finishes.

---

## 4.8 Integration Bugs

Your JavaScript can be correct but fail because another system behaves differently.

Examples:

- API returns a changed field name,
- server returns HTML instead of JSON,
- authentication cookie is missing,
- browser blocks a CORS request,
- backend returns `500`,
- environment variable is incorrect.

---

## 4.9 Environment-Specific Bugs

Works on your machine but fails elsewhere.

Potential differences:

- browser version,
- Node version,
- operating system,
- timezone,
- locale,
- filesystem path case,
- environment variables,
- network,
- cache,
- build mode.

---

## 4.10 Performance Bugs

A page "works" but becomes slow or freezes.

Examples:

- expensive loops,
- repeated DOM layout,
- large JSON processing,
- uncontrolled rendering,
- too many event listeners.

---

## 4.11 Memory Bugs

The application continues allocating objects that are never released.

Symptoms:

- memory grows over time,
- tab becomes slow,
- app crashes after long use.

---

# 5. A Reliable Debugging Workflow

Use this workflow instead of random trial and error.

## Step 1: Reproduce the Problem

You need a reliable trigger.

Write down exact steps:

```text
1. Open /checkout
2. Add one item
3. Apply coupon SAVE10
4. Remove item
5. Total becomes negative
```

A reproducible bug is dramatically easier to investigate.

---

## Step 2: Define Expected vs Actual Behavior

Bad description:

```text
Checkout broken.
```

Better:

```text
Expected: total = 0 after removing the last item.
Actual: total = -500.
```

Now you have a measurable difference.

---

## Step 3: Read the First Useful Error

If an error exists, start there.

Do not focus only on the final error if earlier warnings indicate the real cause.

Example:

```text
GET /api/cart 401 Unauthorized
TypeError: Cannot read properties of undefined (reading 'items')
```

The type error may be secondary. The primary problem could be authentication.

---

## Step 4: Reduce the Search Area

Ask:

- Is the problem frontend or backend?
- Does the event handler run?
- Does the function receive correct inputs?
- Does the API response contain expected data?
- Does the state change before rendering?
- Does the bug occur before or after a specific function?

Use binary-search thinking.

If a pipeline is:

```text
Input → Validation → API → Transform → State → Render
```

check the middle.

If transformed data is already wrong, rendering is probably not the cause.

---

## Step 5: Inspect Data at Boundaries

Boundaries are ideal debugging points.

Examples:

- function input,
- function return,
- API request,
- API response,
- event payload,
- storage read,
- state update.

```js
function normalizeUser(rawUser) {
  console.log("normalizeUser input:", rawUser);

  const result = {
    id: rawUser.user_id,
    name: rawUser.full_name
  };

  console.log("normalizeUser output:", result);
  return result;
}
```

---

## Step 6: Form a Hypothesis

Example:

> "The total becomes negative because removeItem subtracts the price twice."

Now test that hypothesis.

Do not make five unrelated changes at once.

---

## Step 7: Prove the Root Cause

The root cause is the earliest incorrect assumption or state that explains the failure.

Symptom:

```text
Cannot read properties of undefined
```

Immediate cause:

```text
user.profile is undefined
```

Root cause:

```text
API returns `profile_data`, but frontend expects `profile`.
```

Fix the root cause, not only the symptom.

---

## Step 8: Make the Smallest Correct Fix

Avoid unrelated refactoring while fixing a bug unless necessary.

Smaller fixes are easier to review and safer to test.

---

## Step 9: Verify the Fix

Test:

- original failing scenario,
- neighboring scenarios,
- edge cases,
- regression risk.

If the bug involved age validation:

```text
17
18
19
null
"18"
-1
```

---

## Step 10: Prevent Regression

Add:

- automated test,
- validation,
- type checking,
- assertion,
- stronger error handling,
- documentation,
- monitoring.

---

# 6. Reading JavaScript Errors and Stack Traces

A stack trace is one of the most valuable debugging tools.

Consider:

```js
function calculateTotal(cart) {
  return cart.items.reduce((sum, item) => sum + item.price, 0);
}

function checkout(order) {
  return calculateTotal(order.cart);
}

checkout({});
```

A runtime might show:

```text
TypeError: Cannot read properties of undefined (reading 'items')
    at calculateTotal (app.js:2:15)
    at checkout (app.js:6:10)
    at app.js:9:1
```

Read it from the top:

- error type: `TypeError`
- error message: cannot read `items`
- immediate failure: `calculateTotal`
- caller: `checkout`
- original invocation: line 9

The code called:

```js
calculateTotal(order.cart);
```

but `order.cart` was undefined.

---

## 6.1 Error Location Does Not Always Equal Root Cause

Example:

```js
const settings = loadSettings();
renderTheme(settings.theme);
```

If `loadSettings()` returned invalid data, the failure may appear in `renderTheme`.

Always follow the data backward.

---

## 6.2 Preserve the Original Error

Bad:

```js
try {
  riskyOperation();
} catch {
  throw new Error("Something went wrong");
}
```

This discards useful context.

Better:

```js
try {
  riskyOperation();
} catch (error) {
  console.error("riskyOperation failed", error);
  throw error;
}
```

Or attach the original cause:

```js
try {
  riskyOperation();
} catch (error) {
  throw new Error("Unable to complete checkout", {
    cause: error
  });
}
```

---

## 6.3 Custom Error Classes

```js
class ValidationError extends Error {
  constructor(message, field) {
    super(message);
    this.name = "ValidationError";
    this.field = field;
  }
}

throw new ValidationError("Email is required", "email");
```

Custom errors make logs easier to classify.

---

# 7. Console Debugging

The console is the fastest entry point for many bugs.

## 7.1 `console.log()`

```js
const price = 500;
console.log(price);
```

Output:

```text
500
```

Use it to inspect:

- values,
- execution flow,
- function inputs,
- computed results.

But avoid flooding output with unlabeled values.

Bad:

```js
console.log(a);
console.log(b);
console.log(c);
```

Better:

```js
console.log("subtotal:", subtotal);
console.log("tax:", tax);
console.log("final total:", total);
```

---

## 7.2 Multiple Values

```js
console.log("user", userId, "role", role);
```

Or:

```js
console.log({ userId, role, isAdmin });
```

The object form is convenient because labels are automatic.

---

## 7.3 `console.error()`

```js
console.error("Payment failed", error);
```

Use for actual errors.

Do not use every console method interchangeably; meaningful severity improves readability.

---

## 7.4 `console.warn()`

```js
console.warn("Deprecated option used:", option);
```

Good for:

- fallback behavior,
- deprecated features,
- suspicious but recoverable states.

---

## 7.5 `console.info()`

```js
console.info("Application initialized");
```

Useful for informational events.

---

## 7.6 `console.table()`

Extremely useful for arrays of records.

```js
const users = [
  { id: 1, name: "Asha", active: true },
  { id: 2, name: "Ravi", active: false }
];

console.table(users);
```

This is easier to inspect than a long nested object log.

---

## 7.7 `console.dir()`

```js
console.dir(document.body);
```

Useful when you want an object-oriented inspection view.

---

## 7.8 `console.trace()`

```js
function save() {
  console.trace("save() called from");
}

function submit() {
  save();
}

submit();
```

This prints a stack trace without throwing an error.

Very useful when you know **what** is happening but not **who called it**.

---

## 7.9 `console.time()` and `console.timeEnd()`

```js
console.time("processing");

for (let i = 0; i < 1_000_000; i++) {
  Math.sqrt(i);
}

console.timeEnd("processing");
```

Possible output:

```text
processing: 8.4ms
```

Do not treat a single measurement as a scientific benchmark. Use profiling tools for serious performance work.

---

## 7.10 `console.count()`

```js
function render() {
  console.count("render called");
}

render();
render();
render();
```

Output:

```text
render called: 1
render called: 2
render called: 3
```

Excellent for detecting unexpected repeated execution.

---

## 7.11 `console.group()`

```js
console.group("Checkout debug");
console.log("cart", cart);
console.log("coupon", coupon);
console.log("total", total);
console.groupEnd();
```

Useful for organizing noisy logs.

---

## 7.12 `console.assert()`

```js
console.assert(total >= 0, "Total should never be negative", { total });
```

It can surface violated assumptions during development.

Do not rely on console assertions as your only production validation.

---

## 7.13 Structured Debug Logging

Instead of:

```js
console.log("here");
console.log("here2");
console.log("why");
```

use:

```js
console.debug("[checkout] before validation", {
  orderId,
  cartSize: cart.items.length,
  coupon
});
```

A useful debug log answers:

- where,
- what action,
- relevant identifiers,
- relevant state.

---

## 7.14 Common Console Mistake: Logging a Changing Object

Developer consoles may show objects interactively. Depending on tooling, expanding an object later can display its newer state rather than exactly what you mentally expected at log time.

If you need a simple snapshot:

```js
console.log("snapshot:", structuredClone(user));
```

Or log specific primitive fields:

```js
console.log({
  id: user.id,
  status: user.status
});
```

Be careful using JSON serialization as a generic clone because it has limitations with values such as `undefined`, `BigInt`, cycles, special object types, and custom prototypes.

---

# 8. Browser DevTools Overview

Modern browsers provide developer tools. Exact labels vary slightly between browsers.

Common panels include:

| Panel | Main Purpose |
|---|---|
| Elements | Inspect HTML and CSS |
| Console | Errors, logs, interactive JS |
| Sources | Debug JavaScript |
| Network | Requests and responses |
| Application | Storage, cookies, service workers |
| Performance | Runtime performance analysis |
| Memory | Heap and memory analysis |

---

## 8.1 Elements Panel

Use when:

- element does not appear,
- wrong text appears,
- class is missing,
- attribute changed,
- hidden element exists,
- event-related DOM changes need inspection.

You can often edit the DOM temporarily to test a hypothesis.

Remember: DevTools edits are normally temporary. Refreshing the page restores application output.

---

## 8.2 Console Panel

Use for:

- errors,
- warnings,
- manual expressions,
- reading state,
- calling functions,
- inspecting objects.

Example:

```js
document.querySelector("#submit")
```

---

## 8.3 Sources Panel

The main JavaScript debugger.

Use it to:

- open scripts,
- set breakpoints,
- step through code,
- inspect scope,
- evaluate expressions,
- pause on exceptions.

---

## 8.4 Network Panel

Use it to determine:

- whether a request was sent,
- URL,
- method,
- headers,
- status code,
- payload,
- response,
- timing,
- caching behavior.

This panel prevents many wasted hours.

If data is missing from the UI, first ask:

> Did the browser actually receive the expected data?

---

## 8.5 Application Panel

Useful for:

- `localStorage`,
- `sessionStorage`,
- cookies,
- IndexedDB,
- Cache Storage,
- service workers.

---

# 9. Breakpoints

A breakpoint pauses JavaScript execution at a selected location.

This lets you inspect the program **before it continues**.

## 9.1 Line Breakpoint

Suppose:

```js
function calculateInvoice(items) {
  const subtotal = items.reduce((sum, item) => sum + item.price, 0);
  const tax = subtotal * 0.18;
  const total = subtotal + tax;
  return total;
}
```

Set a breakpoint on:

```js
const tax = subtotal * 0.18;
```

When execution pauses, inspect:

```text
items
subtotal
```

You do not need to add logs and refresh repeatedly.

---

## 9.2 When Breakpoints Are Better Than Logs

Use breakpoints when:

- you need many values at one moment,
- execution order is unclear,
- an object is deeply nested,
- a loop fails only at one iteration,
- you need to inspect local variables,
- you need call stack information.

Use logs when:

- behavior is timing-sensitive,
- pausing would alter timing,
- the bug is intermittent,
- you need a history of many events,
- production execution cannot be paused.

---

## 9.3 Pause on Exceptions

DevTools can usually pause:

- on uncaught exceptions,
- optionally on caught exceptions.

This is powerful because the debugger stops at the moment the exception is created.

Without it, a framework may catch the error and show only a generic message.

---

## 9.4 DOM Breakpoints

You can often pause when an element:

- has subtree changes,
- has attribute changes,
- is removed.

Example problem:

> A class is mysteriously removed from a button.

Set an attribute-modification breakpoint on that element. The debugger can pause at the code that changes it.

---

## 9.5 Event Listener Breakpoints

You can pause when events fire, such as:

- click,
- keyboard,
- input,
- submit,
- timer,
- XHR/fetch-related events in some tools.

Useful when you do not know which handler is responsible.

---

# 10. Stepping Through Code

When paused, debugger controls usually include:

- Resume
- Step over
- Step into
- Step out

## 10.1 Resume

Continue execution until:

- next breakpoint,
- exception pause,
- manual pause,
- end of execution.

---

## 10.2 Step Over

Execute the current line without entering called functions.

Example:

```js
const total = calculateTotal(items);
```

**Step over** runs `calculateTotal()` and stops at the next line.

Use when the called function is not currently interesting.

---

## 10.3 Step Into

Enter the called function.

Use when you suspect the problem is inside:

```js
calculateTotal(items);
```

---

## 10.4 Step Out

Finish the current function and return to its caller.

Useful if you stepped into library code accidentally.

---

## 10.5 Debugging a Loop

```js
for (const item of items) {
  total += item.price * item.quantity;
}
```

If the error occurs on only one record, inspect each iteration.

Better: use a conditional breakpoint such as:

```js
item.id === 417
```

Now the debugger pauses only for the suspicious item.

---

# 11. Scope, Call Stack, Watch Expressions, and Closures

## 11.1 Scope Inspection

When paused, DevTools usually shows:

- local scope,
- closure scope,
- global scope,
- module scope where applicable.

Example:

```js
const taxRate = 0.18;

function calculate(price) {
  const tax = price * taxRate;
  return price + tax;
}
```

At the `return`, inspect:

```text
price
tax
taxRate
```

---

## 11.2 Call Stack

Suppose:

```js
submitOrder()
validateOrder()
validateAddress()
normalizePostalCode()
```

If the failure occurs in `normalizePostalCode()`, the call stack tells you how execution reached it.

This often answers:

> "Why is this function even being called?"

---

## 11.3 Watch Expressions

A watch expression is automatically reevaluated as you step.

Examples:

```js
items.length
subtotal + tax
user?.profile?.country
cart.items.filter(x => x.selected).length
```

Watch expressions are useful for derived values you care about repeatedly.

---

## 11.4 Closure Debugging

Example:

```js
function createCounter() {
  let count = 0;

  return function increment() {
    count++;
    return count;
  };
}

const counter = createCounter();
```

The returned function closes over `count`.

If state appears "hidden", inspect the closure scope while paused inside `increment()`.

---

# 12. Conditional Breakpoints and Logpoints

## 12.1 Conditional Breakpoint

Pause only when an expression is true.

Example:

```js
for (const user of users) {
  processUser(user);
}
```

Condition:

```js
user.id === 5001
```

This avoids stopping hundreds of times.

---

## 12.2 Useful Conditions

```js
total < 0
```

```js
item.price == null
```

```js
request.url.includes("/payments")
```

```js
index > 1000
```

---

## 12.3 Logpoints

A logpoint prints information without modifying source code.

Conceptually:

```text
Log when line executes:
"processing user", user.id, user.status
```

Benefits:

- no temporary `console.log()` edit,
- no rebuild in some workflows,
- convenient for repeated observations.

---

# 13. The `debugger` Statement

JavaScript supports:

```js
debugger;
```

Example:

```js
function calculateTotal(items) {
  debugger;

  return items.reduce((sum, item) => {
    return sum + item.price;
  }, 0);
}
```

When DevTools is open and debugging is enabled, execution can pause at that line.

## When to Use

Useful when:

- the location is known,
- setting a breakpoint in bundled code is awkward,
- teaching/debugging local development.

## When Not to Leave It

Do not accidentally ship random `debugger` statements into production code.

A linter can help catch them.

---

# 14. Source Maps, Bundled Code, and Minified Code

Production JavaScript is often transformed.

Your source:

```js
const greeting = name => `Hello ${name}`;
```

may become bundled or minified.

Without source maps, a stack trace might point to:

```text
app.8a9c.js:1:183742
```

That is difficult to interpret.

A **source map** maps generated code back to original source files.

---

## 14.1 Why Source Maps Matter

Source maps allow DevTools and error-monitoring tools to show:

```text
src/checkout/calculateTotal.js:42
```

instead of an unreadable bundle location.

---

## 14.2 Security Consideration

Public source maps can reveal source structure and original code depending on how the application is built and deployed.

Teams commonly choose among approaches such as:

- publish maps publicly,
- upload maps only to an error-monitoring service,
- store maps privately for debugging.

Choose based on operational and security requirements.

---

## 14.3 Debugging Transpiled Code

If using TypeScript, Babel, or another compiler/transpiler:

1. confirm source map generation,
2. confirm browser or debugger is using maps,
3. verify stack-trace paths match deployed build,
4. ensure monitoring receives the exact map for that build.

A source map from the wrong release can produce misleading stack locations.

---

# 15. Debugging Variables, Types, Coercion, and Data

JavaScript's dynamic typing creates many subtle bugs.

## 15.1 `typeof`

```js
console.log(typeof 10);          // "number"
console.log(typeof "10");        // "string"
console.log(typeof true);        // "boolean"
console.log(typeof undefined);   // "undefined"
console.log(typeof function(){});// "function"
```

Historical JavaScript behavior:

```js
console.log(typeof null);
```

returns:

```text
"object"
```

Do not use `typeof value === "object"` alone to distinguish null.

Use:

```js
value !== null && typeof value === "object"
```

---

## 15.2 `Array.isArray()`

```js
Array.isArray([]); // true
Array.isArray({}); // false
```

Use this rather than relying on `typeof`, because:

```js
typeof [] === "object";
```

---

## 15.3 String vs Number Bugs

```js
const price = "100";
const tax = 20;

console.log(price + tax);
```

Output:

```text
10020
```

because `+` performs string concatenation when one operand is a string.

Inspect:

```js
console.log({
  price,
  priceType: typeof price,
  tax,
  taxType: typeof tax
});
```

Fix with deliberate conversion:

```js
const numericPrice = Number(price);
```

But validate the conversion:

```js
if (!Number.isFinite(numericPrice)) {
  throw new Error("Invalid price");
}
```

---

## 15.4 `NaN`

```js
const value = Number("abc");
console.log(value);
```

Output:

```text
NaN
```

Use:

```js
Number.isNaN(value)
```

or, for a value that must be a finite number:

```js
Number.isFinite(value)
```

---

## 15.5 Equality Bugs

Loose equality performs coercion:

```js
0 == false; // true
```

Strict equality does not:

```js
0 === false; // false
```

As a general default, prefer strict equality:

```js
===
!==
```

unless coercive equality is intentionally required and understood.

---

## 15.6 Falsy Values

Falsy values include:

```text
false
0
-0
0n
""
null
undefined
NaN
```

Bug:

```js
function setQuantity(quantity) {
  if (!quantity) {
    quantity = 1;
  }

  return quantity;
}
```

If `0` is a valid quantity, it is incorrectly replaced.

Better:

```js
if (quantity == null) {
  quantity = 1;
}
```

or, depending on intent:

```js
quantity ??= 1;
```

The correct condition depends on the business rule.

---

## 15.7 `||` vs `??`

```js
const count = 0;

console.log(count || 10); // 10
console.log(count ?? 10); // 0
```

`||` falls back for all falsy values.

`??` falls back only for `null` or `undefined`.

This distinction prevents many bugs.

---

# 16. Debugging Arrays and Objects

## 16.1 Shared References

```js
const original = {
  name: "Asha"
};

const copy = original;
copy.name = "Ravi";

console.log(original.name);
```

Output:

```text
Ravi
```

`copy` is not an independent object. Both variables refer to the same object.

---

## 16.2 Shallow Copies

```js
const original = {
  profile: {
    name: "Asha"
  }
};

const copy = { ...original };
copy.profile.name = "Ravi";

console.log(original.profile.name);
```

Output:

```text
Ravi
```

The outer object was copied, but the nested object remained shared.

Debugging object mutation often requires checking reference relationships.

---

## 16.3 `structuredClone()`

For supported cloneable data:

```js
const copy = structuredClone(original);
```

This can produce a deep clone for many built-in structured data types.

It is not appropriate for every JavaScript value. For example, functions are not generally cloneable with `structuredClone()`.

---

## 16.4 Array Mutation

Methods such as these mutate the array:

```text
push
pop
shift
unshift
splice
sort
reverse
```

Others commonly return new arrays:

```text
map
filter
slice
concat
```

A common debugging scenario:

```js
const original = [3, 1, 2];
const sorted = original.sort();

console.log(original);
```

Output:

```text
[1, 2, 3]
```

`sort()` mutated `original`.

If you need to preserve the input:

```js
const sorted = [...original].sort();
```

Or use modern non-mutating alternatives where supported:

```js
const sorted = original.toSorted();
```

---

## 16.5 `map()` vs `forEach()`

Bug:

```js
const doubled = [1, 2, 3].forEach(n => n * 2);

console.log(doubled);
```

Output:

```text
undefined
```

`forEach()` is for iteration and does not return the transformed array.

Use:

```js
const doubled = [1, 2, 3].map(n => n * 2);
```

Output:

```text
[2, 4, 6]
```

---

## 16.6 Missing `return` in Arrow Callback

```js
const result = [1, 2, 3].map(n => {
  n * 2;
});

console.log(result);
```

Output:

```text
[undefined, undefined, undefined]
```

With braces, you need an explicit return:

```js
const result = [1, 2, 3].map(n => {
  return n * 2;
});
```

Or:

```js
const result = [1, 2, 3].map(n => n * 2);
```

---

# 17. Debugging Functions, `this`, Closures, and Callbacks

## 17.1 Function Inputs

Always inspect arguments when a function fails.

```js
function formatUser(user) {
  console.log("formatUser input", user);

  return user.name.toUpperCase();
}
```

If it receives:

```js
{}
```

the bug may be at the caller.

---

## 17.2 Function Return Values

Common bug:

```js
function calculate() {
  const result = 10 + 20;
}

const value = calculate();
console.log(value);
```

Output:

```text
undefined
```

The function forgot to return.

---

## 17.3 `this` Depends on How a Function Is Called

```js
const user = {
  name: "Asha",
  greet() {
    console.log(this.name);
  }
};

user.greet();
```

Output:

```text
Asha
```

But:

```js
const greet = user.greet;
greet();
```

`this` is no longer called as `user.greet()`. Its value depends on execution context and strictness rules, and may be `undefined` in modern module/strict contexts.

A debugging clue:

```js
console.log("this:", this);
```

---

## 17.4 Arrow Functions and `this`

Arrow functions do not create their own `this`.

Potential mistake:

```js
const user = {
  name: "Asha",
  greet: () => {
    console.log(this.name);
  }
};
```

Do not automatically use arrow functions for object methods when you need method-style dynamic `this`.

---

## 17.5 Callback Errors

```js
function loadUser(callback) {
  setTimeout(() => {
    callback({ id: 1 });
  }, 100);
}
```

If the callback throws, inspect both:

- data passed into callback,
- callback implementation.

---

## 17.6 Stale Closures

A closure may retain an earlier value.

This is especially relevant in UI frameworks and event handlers.

Debug by logging:

- when the closure is created,
- value captured,
- value at execution time,
- whether a new closure should have been created.

---

# 18. Debugging DOM Problems

## 18.1 `querySelector()` Returns `null`

```js
const button = document.querySelector("#save");
button.addEventListener("click", save);
```

If no matching element exists:

```text
TypeError: Cannot read properties of null
```

Debug:

```js
console.log(document.querySelector("#save"));
```

Questions:

- Is the selector correct?
- Does the element exist yet?
- Is the script running before DOM creation?
- Is the element inside another document/shadow root?
- Is the ID different?

---

## 18.2 Script Runs Too Early

Possible fix:

```html
<script src="app.js" defer></script>
```

or run after DOM is ready:

```js
document.addEventListener("DOMContentLoaded", () => {
  // DOM-safe initialization
});
```

Choose the approach appropriate for your loading strategy.

---

## 18.3 Inspect Current DOM, Not Only Source HTML

The Elements panel shows the live DOM after JavaScript modifications.

The original page source may not show dynamically inserted elements.

---

## 18.4 Debugging Wrong Text

```js
const label = document.querySelector("#total");
label.textContent = total;
```

Inspect:

```js
console.log({
  label,
  total,
  renderedText: label?.textContent
});
```

This separates:

- calculation problem,
- selector problem,
- rendering problem.

---

## 18.5 MutationObserver for Difficult DOM Changes

```js
const observer = new MutationObserver(mutations => {
  console.log(mutations);
});

observer.observe(document.body, {
  subtree: true,
  childList: true,
  attributes: true
});
```

Useful when you need a history of DOM modifications.

Do not leave broad observers running unnecessarily; they can be noisy or expensive.

---

# 19. Debugging Browser Events

Event bugs often fall into four categories:

1. handler never attached,
2. event never fires,
3. event fires multiple times,
4. event fires but handler logic is wrong.

---

## 19.1 Verify Attachment

```js
const button = document.querySelector("#save");

console.log("button found:", button);

button?.addEventListener("click", event => {
  console.log("save clicked", event);
});
```

---

## 19.2 `event.target` vs `event.currentTarget`

```js
container.addEventListener("click", event => {
  console.log("target:", event.target);
  console.log("currentTarget:", event.currentTarget);
});
```

- `target`: element where event originated
- `currentTarget`: element whose handler is running

This matters in event delegation.

---

## 19.3 Event Delegation

```js
document.querySelector("#list").addEventListener("click", event => {
  const button = event.target.closest("[data-delete-id]");

  if (!button) {
    return;
  }

  console.log("delete id:", button.dataset.deleteId);
});
```

If delegated behavior fails, inspect:

- `event.target`,
- `closest()` result,
- selector,
- propagation.

---

## 19.4 `preventDefault()`

Example:

```js
form.addEventListener("submit", event => {
  event.preventDefault();
  console.log("submit intercepted");
});
```

Without it, browser navigation may make debugging confusing.

But do not call it blindly. Understand the default behavior you are preventing.

---

## 19.5 Duplicate Listeners

Symptom:

> One click triggers the action three times.

Investigate whether code attaches the same listener repeatedly.

```js
console.count("attach save handler");
```

Also inspect lifecycle behavior in frameworks.

---

## 19.6 Event Propagation

Events may move through capture and bubble phases.

If a parent handler unexpectedly fires, inspect:

```js
event.target
event.currentTarget
```

and whether:

```js
event.stopPropagation();
```

is being used.

Use propagation stopping carefully; it can make event systems difficult to reason about.

---

# 20. Debugging Network Requests and APIs

Never debug API-related UI bugs using JavaScript logs alone. Inspect the Network panel.

## 20.1 A Basic `fetch()`

```js
async function loadUsers() {
  const response = await fetch("/api/users");

  if (!response.ok) {
    throw new Error(`Request failed: ${response.status}`);
  }

  return response.json();
}
```

Important:

`fetch()` normally resolves when an HTTP response is received, even for HTTP error statuses such as `404` or `500`. Therefore check `response.ok` or `response.status` when HTTP success matters.

---

## 20.2 Debugging Checklist for a Request

Inspect:

```text
URL
HTTP method
query parameters
request headers
request body
status code
response headers
response body
timing
redirects
cache
```

---

## 20.3 Wrong URL

Bug:

```js
fetch("/api/usres");
```

The typo may produce `404`.

The Network panel proves what URL was requested.

---

## 20.4 Wrong HTTP Method

Frontend:

```js
fetch("/api/users/1", {
  method: "GET"
});
```

Backend expects:

```text
DELETE /api/users/1
```

Inspect the actual method.

---

## 20.5 JSON Parsing Failure

```js
const response = await fetch("/api/data");
const data = await response.json();
```

If the server returns HTML:

```html
<html>
  <body>Server Error</body>
</html>
```

JSON parsing fails.

Debug by inspecting the raw response:

```js
const text = await response.text();
console.log(text);
```

Do this only while diagnosing; design normal production handling appropriately.

---

## 20.6 Request Body Mistake

```js
fetch("/api/orders", {
  method: "POST",
  body: {
    id: 1
  }
});
```

`fetch()` does not automatically JSON-encode a plain object body.

Common JSON request:

```js
fetch("/api/orders", {
  method: "POST",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({
    id: 1
  })
});
```

---

## 20.7 CORS

CORS is enforced by browsers.

Symptoms may include:

- request blocked,
- console CORS message,
- preflight request failure.

Debug:

1. inspect Console,
2. inspect Network,
3. inspect `OPTIONS` preflight if present,
4. inspect server CORS response headers,
5. verify origin/method/header policy.

Do not "fix" production CORS by disabling browser security.

---

## 20.8 Authentication Bugs

Inspect:

- `Authorization` header,
- cookies,
- token expiration,
- credentials option,
- server status code,
- redirect to login.

Never print secrets or full authentication tokens into logs.

A safe diagnostic log might record:

```js
console.debug({
  authenticated: Boolean(token),
  tokenPresent: Boolean(token)
});
```

not the token itself.

---

## 20.9 Abort and Cancellation

```js
const controller = new AbortController();

fetch("/api/search?q=javascript", {
  signal: controller.signal
});

controller.abort();
```

If requests appear to "randomly fail," check whether application code is cancelling them.

---

# 21. Debugging Promises and `async`/`await`

Asynchronous bugs are among the most common JavaScript debugging problems.

## 21.1 Forgotten `await`

Bug:

```js
async function getUser() {
  return { id: 1, name: "Asha" };
}

async function main() {
  const user = getUser();
  console.log(user.name);
}

main();
```

`user` is a Promise, not the resolved object.

Correct:

```js
const user = await getUser();
```

---

## 21.2 Missing Promise Return

Bug:

```js
function loadUser() {
  fetch("/api/user")
    .then(response => response.json());
}

loadUser().then(console.log);
```

`loadUser()` returns `undefined`.

Correct:

```js
function loadUser() {
  return fetch("/api/user")
    .then(response => response.json());
}
```

---

## 21.3 Missing Return Inside `.then()`

```js
fetch("/api/user")
  .then(response => {
    response.json();
  })
  .then(user => {
    console.log(user);
  });
```

The first callback does not return the parsing promise.

Correct:

```js
fetch("/api/user")
  .then(response => {
    return response.json();
  })
  .then(user => {
    console.log(user);
  });
```

---

## 21.4 Error Handling

```js
async function load() {
  try {
    const response = await fetch("/api/data");

    if (!response.ok) {
      throw new Error(`HTTP ${response.status}`);
    }

    const data = await response.json();
    return data;
  } catch (error) {
    console.error("load failed", error);
    throw error;
  }
}
```

Do not catch errors only to hide them:

```js
catch (error) {
  return {};
}
```

unless returning an empty object is truly a valid fallback and callers can distinguish fallback from success.

---

## 21.5 `Promise.all()`

```js
const [user, orders] = await Promise.all([
  fetchUser(),
  fetchOrders()
]);
```

If one rejects, `Promise.all()` rejects.

When debugging, identify which member failed.

One technique:

```js
const results = await Promise.allSettled([
  fetchUser(),
  fetchOrders()
]);

console.log(results);
```

`Promise.allSettled()` gives a result for every input, which is useful diagnostically and in workflows where partial results are meaningful.

---

## 21.6 Unhandled Rejections

If a promise rejects without proper handling, environments can report an unhandled rejection.

Debug by:

- enabling pause on exceptions,
- finding the original rejecting operation,
- following the promise chain,
- adding intentional error handling.

In browser diagnostics you can temporarily observe:

```js
window.addEventListener("unhandledrejection", event => {
  console.error("Unhandled rejection:", event.reason);
});
```

This is a diagnostic aid, not a substitute for handling errors where they belong.

---

## 21.7 Async Stack Traces

Modern devtools often preserve useful asynchronous stack information.

When an error occurs after an `await`, inspect the complete stack and async frames rather than only the final callback.

---

# 22. Debugging Timers, Race Conditions, and Concurrency

## 22.1 Race Condition Example

```js
let currentResult;

async function search(query) {
  const response = await fetch(`/api/search?q=${encodeURIComponent(query)}`);
  const result = await response.json();

  currentResult = result;
  render(result);
}
```

User types:

```text
j
ja
jav
java
```

Older requests may finish after newer ones. The UI can show stale data.

---

## 22.2 Debug with Request IDs

```js
let latestRequestId = 0;

async function search(query) {
  const requestId = ++latestRequestId;

  console.log("search start", { requestId, query });

  const response = await fetch(
    `/api/search?q=${encodeURIComponent(query)}`
  );

  const result = await response.json();

  console.log("search complete", { requestId, query });

  if (requestId !== latestRequestId) {
    console.log("discarding stale result", { requestId });
    return;
  }

  render(result);
}
```

This makes ordering visible.

---

## 22.3 Cancellation for Search

Another approach is to abort the previous request.

```js
let controller;

async function search(query) {
  controller?.abort();
  controller = new AbortController();

  try {
    const response = await fetch(
      `/api/search?q=${encodeURIComponent(query)}`,
      { signal: controller.signal }
    );

    const result = await response.json();
    render(result);
  } catch (error) {
    if (error.name !== "AbortError") {
      throw error;
    }
  }
}
```

---

## 22.4 `setInterval()` Overlap

If an async operation can take longer than the interval, repeated work may overlap.

```js
setInterval(async () => {
  await syncData();
}, 1000);
```

If `syncData()` takes 5 seconds, several calls can be in progress.

A sequential pattern:

```js
async function loop() {
  await syncData();
  setTimeout(loop, 1000);
}

loop();
```

Use the pattern that matches your desired scheduling semantics.

---

## 22.5 Timing-Sensitive Debugging Warning

Breakpoints stop execution. Pausing can change timing and make a race condition disappear.

For timing-sensitive bugs, prefer:

- timestamped logs,
- request IDs,
- performance marks,
- tracing,
- reproducible stress tests.

This is sometimes called a **Heisenbug**: observing the problem changes its behavior.

---

# 23. Debugging Modules and Imports

## 23.1 Named vs Default Exports

File:

```js
export function calculateTax() {
  // ...
}
```

Correct named import:

```js
import { calculateTax } from "./tax.js";
```

This is different from:

```js
export default function calculateTax() {
  // ...
}
```

which is commonly imported as:

```js
import calculateTax from "./tax.js";
```

---

## 23.2 Wrong Path

```js
import { config } from "./Config.js";
```

Filesystem case sensitivity may differ by platform.

A path that appears to work on a case-insensitive development machine may fail on a case-sensitive server.

Match filename casing exactly.

---

## 23.3 Circular Dependencies

Example:

```text
a.js imports b.js
b.js imports a.js
```

Circular modules may create partially initialized values or surprising execution ordering.

If an import is unexpectedly undefined:

1. inspect dependency graph,
2. check circular imports,
3. move shared code into a third module,
4. reduce cross-module initialization side effects.

---

## 23.4 Browser Module Errors

For browser ES modules:

```html
<script type="module" src="./app.js"></script>
```

If module loading fails, inspect:

- Network panel,
- MIME/content type,
- URL,
- server response,
- CORS,
- syntax error,
- import path.

---

# 24. Debugging Browser Storage, Cookies, and Caching

## 24.1 `localStorage`

```js
localStorage.setItem("theme", "dark");

const theme = localStorage.getItem("theme");
```

All normal `localStorage` values are strings.

Bug:

```js
localStorage.setItem("settings", { theme: "dark" });
```

This does not store the object as structured JSON.

Use:

```js
localStorage.setItem(
  "settings",
  JSON.stringify({ theme: "dark" })
);
```

Read:

```js
const settings = JSON.parse(
  localStorage.getItem("settings") ?? "{}"
);
```

---

## 24.2 Stale Storage

A bug may occur because an older application version stored a different shape.

Example old data:

```json
{
  "darkMode": true
}
```

New code expects:

```json
{
  "theme": "dark"
}
```

Debug using the Application panel and inspect exact stored values.

Production solutions may require schema versioning or migration.

---

## 24.3 Cookies

Debug:

- cookie name,
- domain,
- path,
- expiration,
- SameSite,
- Secure,
- HttpOnly,
- whether browser sends it.

An `HttpOnly` cookie intentionally cannot be read by client-side JavaScript.

If JavaScript cannot read it, that may be correct security behavior.

---

## 24.4 Browser Cache

When the browser appears to run old code:

1. confirm loaded asset URL,
2. inspect response headers,
3. inspect Network request,
4. use a hard reload during development,
5. verify service worker/cache behavior,
6. verify deployment produced a new asset hash/version.

Do not assume "cache" without evidence.

---

# 25. Debugging Node.js Applications

Node.js debugging uses many of the same JavaScript principles plus server-specific tools.

## 25.1 Basic Error Output

```js
function start() {
  throw new Error("Startup failed");
}

start();
```

Node prints an error and stack trace.

Start by reading the first relevant application frame.

---

## 25.2 Inspector

A Node process can be started with inspector support:

```bash
node --inspect app.js
```

A common break-on-start form is:

```bash
node --inspect-brk app.js
```

`--inspect-brk` pauses before user code begins, making startup bugs easier to debug.

Use an inspector-capable client such as a compatible DevTools or IDE debugger.

---

## 25.3 Debugging Environment Variables

```js
console.log({
  nodeEnv: process.env.NODE_ENV,
  apiBaseUrlPresent: Boolean(process.env.API_BASE_URL)
});
```

Do not print secrets.

Bad:

```js
console.log(process.env.DATABASE_PASSWORD);
```

---

## 25.4 File Path Bugs

Prefer platform-aware path utilities:

```js
import path from "node:path";

const fullPath = path.join("logs", "app.log");
```

Inspect:

```js
console.log({
  cwd: process.cwd(),
  fullPath
});
```

Many file bugs come from misunderstanding the current working directory.

---

## 25.5 `__dirname` and ES Modules

Traditional CommonJS provides `__dirname`.

ES modules use different patterns based on `import.meta.url`.

When debugging module/path issues, first confirm whether the project is running as:

- CommonJS,
- ES modules.

Do not mix assumptions from the two systems.

---

## 25.6 HTTP Server Debugging

Log structured request metadata:

```js
console.log({
  method: req.method,
  url: req.url
});
```

Useful server boundaries:

```text
request received
authentication completed
validation completed
database call started
database call completed
response sent
```

Avoid logging sensitive request bodies indiscriminately.

---

## 25.7 Process-Level Diagnostics

Diagnostic handlers can help during development:

```js
process.on("uncaughtException", error => {
  console.error("Uncaught exception", error);
});

process.on("unhandledRejection", reason => {
  console.error("Unhandled rejection", reason);
});
```

Important:

An uncaught exception may leave a process in an unknown or unsafe application state. Production strategy is typically broader than "catch globally and continue." Use process supervision, graceful shutdown, observability, and recovery appropriate to the system.

---

# 26. Debugging JavaScript in VS Code

VS Code can debug browser and Node.js applications.

The exact UI and configuration options evolve, but the core concepts remain:

- launch a program under the debugger,
- attach to an existing process,
- set breakpoints,
- inspect variables,
- inspect call stack,
- evaluate expressions.

---

## 26.1 Simple Node Debugging

Open a JavaScript file such as:

```js
function add(a, b) {
  return a + b;
}

const result = add(10, 20);
console.log(result);
```

Set a breakpoint inside `add()` and start a Node debugging session.

Inspect:

```text
a
b
result
```

---

## 26.2 Example `launch.json`

A common Node-style configuration can look like:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "launch",
      "name": "Debug Node App",
      "program": "${workspaceFolder}/app.js"
    }
  ]
}
```

Exact configuration depends on project structure and runtime.

---

## 26.3 Launch vs Attach

### Launch

Debugger starts the application.

Use when:

- developing locally,
- simple Node application,
- you control startup.

### Attach

Debugger connects to an already running debug-enabled process.

Use when:

- application is started by another tool,
- debugging a server process,
- using a development framework or process manager.

---

## 26.4 Debug Console

When paused, evaluate expressions such as:

```js
user.id
```

```js
items.map(x => x.price)
```

```js
JSON.stringify(config, null, 2)
```

Be careful: expressions can have side effects.

Bad diagnostic expression:

```js
cart.items.pop()
```

You just changed program state.

Prefer read-only inspection where possible.

---

## 26.5 Skip Library Code

Debuggers can often avoid stepping through dependency internals.

This is useful because you usually want your own application frames first.

But if the defect is an integration misuse or suspected dependency bug, library code may become relevant.

---

# 27. Debugging with Tests

Tests are one of the strongest debugging tools because they make failures reproducible.

## 27.1 Turn a Bug into a Test

Bug:

> Coupon `SAVE10` is applied twice.

Write a failing test first.

Conceptual example:

```js
test("applies SAVE10 only once", () => {
  const cart = {
    subtotal: 1000,
    coupons: ["SAVE10", "SAVE10"]
  };

  expect(calculateTotal(cart)).toBe(900);
});
```

Now you have:

- reproducible input,
- expected result,
- automatic regression protection.

---

## 27.2 Unit Tests

Good for pure logic:

```js
function addTax(amount, rate) {
  return amount + amount * rate;
}
```

Test:

```js
expect(addTax(100, 0.18)).toBe(118);
```

---

## 27.3 Integration Tests

Useful when the bug depends on multiple components.

Example:

```text
route → validation → service → database adapter
```

---

## 27.4 End-to-End Tests

Useful when the problem exists only in the complete application flow.

Example:

```text
login → search → add to cart → checkout
```

---

## 27.5 The Smallest Reproduction

If a huge project crashes, create the smallest code that still fails.

Original:

```text
React app + router + state library + API + chart
```

Reduced reproduction:

```js
const data = transform(serverResponse);
console.log(data);
```

If the reduced code still fails, debugging becomes much easier.

---

# 28. Error Handling as a Debugging Tool

Good error handling preserves useful evidence.

## 28.1 Validate Early

Bad:

```js
function processUser(user) {
  return user.profile.address.city.toUpperCase();
}
```

Better:

```js
function processUser(user) {
  if (!user?.profile?.address?.city) {
    throw new Error("User city is required");
  }

  return user.profile.address.city.toUpperCase();
}
```

Now the error describes the actual contract violation.

---

## 28.2 Guard Clauses

```js
function calculateDiscount(user, order) {
  if (!user) {
    throw new Error("User is required");
  }

  if (!order) {
    throw new Error("Order is required");
  }

  if (!Array.isArray(order.items)) {
    throw new Error("order.items must be an array");
  }

  // actual logic...
}
```

This makes invalid states fail closer to their source.

---

## 28.3 Contextual Errors

Weak:

```js
throw new Error("Failed");
```

Better:

```js
throw new Error(
  `Failed to load invoice ${invoiceId}`
);
```

Do not include sensitive data.

---

## 28.4 Avoid Empty Catch Blocks

Bad:

```js
try {
  await saveOrder();
} catch (error) {
}
```

The application silently ignores failure.

If failure is intentionally ignored, document why and consider recording an appropriate diagnostic signal.

---

# 29. Debugging Memory Leaks

JavaScript uses garbage collection, but memory can still leak when references are unintentionally retained.

## 29.1 Common Leak Sources

- event listeners never removed,
- timers never cleared,
- growing caches,
- detached DOM nodes,
- global arrays,
- closures retaining large objects,
- subscriptions not disposed,
- WebSocket/listener cleanup failures.

---

## 29.2 Event Listener Leak

```js
function mount() {
  window.addEventListener("resize", handleResize);
}
```

If `mount()` runs repeatedly without cleanup, listeners accumulate.

Cleanup:

```js
function unmount() {
  window.removeEventListener("resize", handleResize);
}
```

Framework lifecycle APIs provide equivalent cleanup mechanisms.

---

## 29.3 Timer Leak

```js
const intervalId = setInterval(refresh, 1000);
```

When no longer needed:

```js
clearInterval(intervalId);
```

---

## 29.4 Unbounded Cache

```js
const cache = new Map();

function remember(id, value) {
  cache.set(id, value);
}
```

If `id` is always new and entries never expire, memory can grow forever.

Possible strategies:

- size limit,
- TTL expiration,
- LRU cache,
- explicit cleanup,
- weak references for appropriate designs.

---

## 29.5 Heap Snapshots

Memory tools can capture heap snapshots.

A useful method:

1. open the page,
2. record baseline,
3. perform suspected action many times,
4. force/allow cleanup as tooling permits,
5. record another snapshot,
6. compare retained objects.

Look for objects whose count continuously grows.

---

## 29.6 Detached DOM Nodes

A DOM node removed from the document can still remain in memory if JavaScript keeps a reference.

Example:

```js
let savedNode;

function removePanel() {
  const panel = document.querySelector(".panel");
  savedNode = panel;
  panel.remove();
}
```

The node is detached but still referenced by `savedNode`.

---

# 30. Debugging Performance Problems

Performance debugging should be evidence-driven.

## 30.1 Common Symptoms

- slow input,
- freezing,
- slow scrolling,
- delayed click response,
- long page load,
- high CPU,
- repeated rendering.

---

## 30.2 Measure Before Optimizing

Bad approach:

> "This loop looks slow. Rewrite everything."

Better:

1. reproduce the slowdown,
2. record a profile,
3. identify expensive work,
4. optimize the actual bottleneck,
5. measure again.

---

## 30.3 Performance Timing

Simple measurement:

```js
performance.mark("start");

// work

performance.mark("end");
performance.measure("work", "start", "end");

console.log(performance.getEntriesByName("work"));
```

For complex applications use browser Performance profiling.

---

## 30.4 Accidental Quadratic Work

Example:

```js
for (const user of users) {
  const order = orders.find(order => order.userId === user.id);
}
```

If both arrays are large, repeated `.find()` can become expensive.

Index once:

```js
const ordersByUserId = new Map(
  orders.map(order => [order.userId, order])
);

for (const user of users) {
  const order = ordersByUserId.get(user.id);
}
```

Do this after measuring that this work matters.

---

## 30.5 Layout Thrashing

Repeated DOM reads and writes can force layout work.

Potential pattern:

```js
for (const el of elements) {
  el.style.width = `${el.offsetWidth + 1}px`;
}
```

This mixes layout read and write repeatedly.

Batching reads and writes can improve performance.

Use the Performance panel to confirm layout/recalculation costs.

---

## 30.6 Rendering Too Often

Use:

```js
console.count("render");
```

or framework devtools/profilers.

If one action causes dozens of unnecessary renders, inspect:

- state update frequency,
- changed object references,
- subscriptions,
- effects,
- parent rerenders.

---

# 31. Debugging Web Workers and Service Workers

## 31.1 Web Workers

Workers have separate execution contexts.

Problems may include:

- message never posted,
- message handler not registered,
- data cannot be cloned,
- worker script load failure,
- exception inside worker.

Example:

```js
worker.postMessage({ task: "calculate" });

worker.addEventListener("message", event => {
  console.log("worker response", event.data);
});

worker.addEventListener("error", error => {
  console.error("worker error", error);
});
```

Debug both sides of the message boundary.

---

## 31.2 Service Workers

Service workers can make debugging confusing because they intercept network requests and manage caches.

Symptoms:

- old app keeps appearing,
- requests return unexpected cached data,
- updates do not activate,
- offline behavior is incorrect.

Inspect:

- service worker registration,
- lifecycle state,
- Cache Storage,
- network responses,
- update behavior.

During development, know whether a service worker is controlling the page before blaming the normal browser cache.

---

# 32. Debugging Framework Applications

Frameworks change the shape of the code, but the fundamental debugging method remains the same.

## 32.1 React-Style Problems

Common categories:

- stale state,
- state mutation,
- effect dependencies,
- repeated renders,
- component lifecycle,
- wrong props,
- event handler closure,
- async race.

Debug boundaries:

```text
props in
state before update
state after update
effect execution
render count
API response
```

Framework-specific devtools can help inspect component trees and state.

---

## 32.2 Vue-Style Problems

Common categories:

- reactive state not what you expect,
- computed value logic,
- watcher behavior,
- prop flow,
- emitted event mismatch.

Inspect the component with framework devtools, then return to normal JavaScript debugging for the underlying data and functions.

---

## 32.3 Angular-Style Problems

Common categories:

- dependency injection/configuration,
- observable flow,
- template binding,
- change detection,
- HTTP interceptor behavior,
- lifecycle timing.

Use:

- browser debugger,
- network tools,
- RxJS-focused logging,
- framework devtools when available.

---

## 32.4 Framework Rule

Do not jump immediately to "framework bug."

First ask:

- Is the input correct?
- Is state correct?
- Is the function executing?
- Is the API correct?
- Is the DOM correct?
- Is lifecycle timing responsible?

Frameworks still execute JavaScript.

---

# 33. Debugging Production Applications

Production debugging is different because:

- you may not reproduce locally,
- users have different environments,
- code may be minified,
- sensitive data must be protected,
- you cannot pause a user's browser,
- logs may be incomplete.

---

## 33.1 What Production Diagnostics Should Capture

Useful non-sensitive context may include:

```text
timestamp
release/build version
route/screen
operation
error type
stack trace
request/correlation ID
browser/runtime
feature flag state
non-sensitive entity ID
```

---

## 33.2 Correlation IDs

Suppose:

```text
Browser request → API gateway → service → database
```

A shared request ID helps connect logs.

Frontend:

```js
const requestId = crypto.randomUUID();

fetch("/api/orders", {
  headers: {
    "X-Request-ID": requestId
  }
});
```

Whether you generate or propagate IDs depends on architecture.

The key debugging idea is end-to-end correlation.

---

## 33.3 Release Identification

Always know which code version produced an error.

Example metadata:

```js
const APP_VERSION = "2026.08.17.1";
```

In real deployments this is often injected by the build pipeline.

Without a build version, "the error happened in app.js" may be ambiguous after multiple releases.

---

## 33.4 Feature Flags

A production-only bug may depend on a feature flag.

Record relevant flag state:

```js
console.debug({
  newCheckoutEnabled: flags.newCheckout
});
```

Do not log confidential targeting data unnecessarily.

---

## 33.5 Reproduction from User Reports

Ask for facts, not interpretations.

Useful report:

```text
Browser:
Page:
Time:
Steps:
Expected:
Actual:
Screenshot:
Error message:
Does refresh fix it?
Does incognito reproduce it?
```

---

## 33.6 Logging Levels

Common conceptual levels:

- debug,
- info,
- warn,
- error.

Production environments often reduce debug-level noise while preserving enough metadata for diagnosis.

---

## 33.7 Never Log Secrets

Do not log:

- passwords,
- access tokens,
- refresh tokens,
- private keys,
- full payment card data,
- confidential personal data unless explicitly justified, protected, and compliant.

Debugging convenience is not a reason to violate security or privacy.

---

# 34. Security-Sensitive Debugging

Debugging can accidentally introduce vulnerabilities.

## 34.1 Do Not Disable Security as a Permanent Fix

Examples of unsafe "fixes":

- disabling CORS protection,
- turning off TLS validation,
- exposing secret keys in frontend code,
- allowing any origin without understanding consequences,
- bypassing authentication checks,
- logging credentials.

Use controlled development diagnostics instead.

---

## 34.2 Frontend Secrets Are Not Secret

Anything shipped to a browser can be inspected by the user.

Do not place private server credentials in:

```js
const SECRET_API_KEY = "...";
```

inside frontend bundles.

If a key must remain secret, keep it on a trusted server-side environment.

---

## 34.3 Be Careful with Error Messages

A detailed internal stack trace may help developers but reveal too much to end users.

Pattern:

```text
User-facing:
"Unable to process request."

Internal log:
full exception + request ID + safe context
```

---

# 35. Real-World Debugging Scenarios

This section demonstrates complete thought processes.

---

## Scenario 1: "Cannot Read Properties of Undefined"

Code:

```js
function renderUser(user) {
  document.querySelector("#name").textContent =
    user.profile.name;
}

renderUser({
  id: 1
});
```

Error:

```text
TypeError: Cannot read properties of undefined
```

### Step 1: Identify failing expression

```js
user.profile.name
```

### Step 2: Inspect input

```js
console.log(user);
```

Output:

```js
{
  id: 1
}
```

### Step 3: Root cause

The caller supplied no `profile`.

### Possible fixes

If `profile` is required:

```js
function renderUser(user) {
  if (!user?.profile?.name) {
    throw new Error("user.profile.name is required");
  }

  document.querySelector("#name").textContent =
    user.profile.name;
}
```

If it is optional:

```js
const name = user?.profile?.name ?? "Unknown";
```

The correct fix depends on the data contract.

---

## Scenario 2: Button Click Does Nothing

HTML:

```html
<button id="save">Save</button>
```

JavaScript:

```js
const button = document.querySelector("#Save");

button.addEventListener("click", () => {
  console.log("saved");
});
```

### Investigation

```js
console.log(button);
```

Output:

```text
null
```

Problem:

```text
#Save
```

does not match:

```text
id="save"
```

Correct:

```js
document.querySelector("#save");
```

---

## Scenario 3: Event Runs Twice

```js
function initialize() {
  document
    .querySelector("#save")
    .addEventListener("click", save);
}

initialize();
initialize();
```

One click calls `save()` twice.

### Debugging

Add:

```js
console.count("initialize");
```

and:

```js
function save() {
  console.count("save");
}
```

Now repeated attachment becomes visible.

Fix the lifecycle so the handler is attached exactly as intended.

---

## Scenario 4: API Returns 500 but UI Says JSON Error

```js
const response = await fetch("/api/orders");
const orders = await response.json();
```

Server returns an HTML error page.

The JSON parser fails.

### Debug correctly

Inspect Network:

```text
Status: 500
Content-Type: text/html
```

Root cause is server failure, not JSON itself.

Improve frontend:

```js
if (!response.ok) {
  throw new Error(`Orders API failed: ${response.status}`);
}
```

---

## Scenario 5: `0` Becomes Default Value

```js
function normalizeStock(stock) {
  return stock || 10;
}

console.log(normalizeStock(0));
```

Output:

```text
10
```

If `0` means "out of stock", this is a bug.

Correct:

```js
return stock ?? 10;
```

Now `0` remains `0`.

---

## Scenario 6: Async Search Shows Wrong Results

User quickly searches:

```text
java
javascript
```

The first request is slow. It returns after the second request and overwrites the screen.

### Evidence

Log:

```js
console.log("request start", { query, id });
console.log("request end", { query, id });
```

Example:

```text
start 1 java
start 2 javascript
end   2 javascript
end   1 java
```

Now the race is proven.

Fix with:

- cancellation, or
- latest-request checking.

---

## Scenario 7: Works on Windows, Fails on Linux

Import:

```js
import { config } from "./Config.js";
```

Actual file:

```text
config.js
```

A case-insensitive filesystem may hide the mistake.

Fix:

```js
import { config } from "./config.js";
```

Use exact casing consistently.

---

## Scenario 8: `sort()` Changes Original Data

```js
const users = [
  { name: "Ravi" },
  { name: "Asha" }
];

const sortedUsers = users.sort((a, b) =>
  a.name.localeCompare(b.name)
);
```

Later code assumes `users` retains original order.

It does not.

Use:

```js
const sortedUsers = [...users].sort((a, b) =>
  a.name.localeCompare(b.name)
);
```

or a supported non-mutating sorting API.

---

## Scenario 9: Loop Skips an Item

Buggy removal:

```js
for (let i = 0; i < items.length; i++) {
  if (items[i].remove) {
    items.splice(i, 1);
  }
}
```

Removing changes indexes.

Example:

```text
index 0 removed
old index 1 becomes new index 0
loop increments to 1
new index 0 is skipped
```

Potential alternative:

```js
const remaining = items.filter(item => !item.remove);
```

Or iterate carefully based on mutation requirements.

---

## Scenario 10: Date Is Wrong for Some Users

Code:

```js
const date = new Date("2026-08-17");
console.log(date.toString());
```

Dates are affected by:

- parsing rules,
- timezone,
- formatting,
- local vs UTC expectations.

Debug by logging:

```js
console.log({
  input: "2026-08-17",
  timestamp: date.getTime(),
  iso: date.toISOString(),
  local: date.toString(),
  timezone: Intl.DateTimeFormat().resolvedOptions().timeZone
});
```

Define the business meaning first:

> Is this a calendar date, local datetime, or global instant?

Many date bugs are requirement/modeling bugs, not only formatting bugs.

---

## Scenario 11: Form Refreshes Page Before Log Is Seen

```js
form.addEventListener("submit", () => {
  console.log("submitting");
});
```

The browser performs normal form submission and navigates.

For a client-side handled form:

```js
form.addEventListener("submit", event => {
  event.preventDefault();
  console.log("submitting");
});
```

Only prevent default when your code intentionally replaces the default behavior.

---

## Scenario 12: Object Looks Correct in Log but Was Wrong Earlier

```js
const config = { mode: "old" };

console.log(config);

config.mode = "new";
```

Interactive console inspection can make object-state debugging confusing.

Log snapshot fields:

```js
console.log({
  modeAtThisMoment: config.mode
});
```

---

## Scenario 13: Memory Grows Every Time a Modal Opens

```js
function openModal() {
  window.addEventListener("keydown", handleKeydown);
}
```

Each open adds another listener.

### Evidence

- open modal 50 times,
- take heap/listener measurements,
- key handler fires many times.

Fix lifecycle cleanup:

```js
function closeModal() {
  window.removeEventListener("keydown", handleKeydown);
}
```

---

## Scenario 14: Request Is Successful but UI Still Empty

Network response:

```json
{
  "data": [
    { "id": 1, "name": "Asha" }
  ]
}
```

Frontend expects:

```js
const users = response.users;
```

Network is correct; transformation contract is wrong.

Debug at boundary:

```js
console.log("raw API response", response);
console.log("users extracted", users);
```

Fix mapping:

```js
const users = response.data;
```

---

## Scenario 15: `forEach()` with Async Work Finishes Too Early

```js
async function saveAll(items) {
  items.forEach(async item => {
    await saveItem(item);
  });

  console.log("all saved");
}
```

`forEach()` does not await those callbacks.

Sequential approach:

```js
async function saveAll(items) {
  for (const item of items) {
    await saveItem(item);
  }

  console.log("all saved");
}
```

Concurrent approach:

```js
async function saveAll(items) {
  await Promise.all(
    items.map(item => saveItem(item))
  );

  console.log("all saved");
}
```

Choose based on concurrency, rate limits, ordering, and failure semantics.

---

# 36. Common Debugging Anti-Patterns

## 36.1 Random Code Changes

Bad loop:

```text
Change line
Refresh
Change another line
Refresh
Undo
Try something else
```

This destroys evidence.

Better:

```text
Observe
Hypothesize
Test one idea
Measure
Conclude
```

---

## 36.2 Adding `setTimeout()` to "Fix" Timing

Bad:

```js
setTimeout(() => {
  useData();
}, 2000);
```

This hides the real synchronization issue.

Wait for the actual event or promise instead.

---

## 36.3 Swallowing Errors

Bad:

```js
try {
  await load();
} catch {
}
```

The failure disappears.

---

## 36.4 Huge Console Dumps

Bad:

```js
console.log(appState);
```

when `appState` contains thousands of nested fields.

Better:

```js
console.log({
  userId: appState.user?.id,
  cartCount: appState.cart?.items?.length,
  checkoutStatus: appState.checkout?.status
});
```

Log the evidence you need.

---

## 36.5 Fixing the Symptom with Optional Chaining Everywhere

Bug:

```js
user.profile.name
```

Temporary change:

```js
user?.profile?.name
```

This may prevent the exception but can hide broken required data.

Use optional chaining only when absence is genuinely allowed.

---

## 36.6 Catching Everything at the Top

Global handlers are useful for last-resort reporting, but they do not replace local validation and proper error handling.

Handle errors where you understand:

- what operation failed,
- whether recovery is possible,
- what context is safe to record.

---

## 36.7 Ignoring Warnings

Warnings can reveal future errors:

```text
deprecated API
duplicate key
invalid HTML
failed source map
unhandled promise
```

Do not ignore them automatically.

---

## 36.8 Assuming the API Is Correct

Inspect the actual response.

Likewise, backend developers should not assume the frontend sent the expected payload. Inspect actual request data.

---

## 36.9 Assuming "Works for Me" Means Fixed

Test:

- another account,
- clean storage,
- another browser,
- slow network,
- empty data,
- large data,
- permissions,
- production build.

---

# 37. Debugging Checklists

## 37.1 General JavaScript Bug Checklist

- [ ] Can I reproduce the bug?
- [ ] What is expected?
- [ ] What actually happens?
- [ ] Is there an error or warning?
- [ ] What is the first useful stack frame?
- [ ] What input reached the failing function?
- [ ] What value first becomes wrong?
- [ ] Is type/coercion involved?
- [ ] Is the state mutated unexpectedly?
- [ ] Is timing involved?
- [ ] Does the bug depend on environment?
- [ ] Can I reduce the reproduction?
- [ ] Did I verify the root cause?
- [ ] Did I test the original failure after fixing?
- [ ] Should I add a regression test?

---

## 37.2 Browser UI Bug Checklist

- [ ] Does the element exist?
- [ ] Is the selector correct?
- [ ] Does script run after the DOM is available?
- [ ] Is the event listener attached?
- [ ] Does the event fire?
- [ ] Does the handler receive expected data?
- [ ] Does application state update?
- [ ] Does the DOM update?
- [ ] Is another script overwriting the change?
- [ ] Is CSS only making it appear missing?
- [ ] Is a framework rerender replacing the DOM?

---

## 37.3 API Bug Checklist

- [ ] Correct URL?
- [ ] Correct HTTP method?
- [ ] Correct query parameters?
- [ ] Correct request body?
- [ ] Correct content type?
- [ ] Authentication included?
- [ ] Correct cookies?
- [ ] CORS/preflight successful?
- [ ] Status code?
- [ ] Response body?
- [ ] Response data shape?
- [ ] JSON parsing successful?
- [ ] Request cancelled?
- [ ] Stale response race?
- [ ] Backend error/correlation ID available?

---

## 37.4 Async Bug Checklist

- [ ] Did I forget `await`?
- [ ] Did I forget `return`?
- [ ] Is a promise rejection handled?
- [ ] Are operations running concurrently?
- [ ] Can responses arrive out of order?
- [ ] Does a timer overlap with itself?
- [ ] Does a breakpoint alter timing?
- [ ] Should an earlier request be cancelled?
- [ ] Is stale state captured in a closure?

---

## 37.5 Node.js Bug Checklist

- [ ] Correct Node/runtime mode?
- [ ] CommonJS or ES modules?
- [ ] Correct environment variables?
- [ ] Correct working directory?
- [ ] Correct file path and case?
- [ ] Port available?
- [ ] Request reaches server?
- [ ] Database/service call completes?
- [ ] Promise rejection handled?
- [ ] Stack trace points to application code?
- [ ] Is inspector attached when needed?
- [ ] Are secrets excluded from logs?

---

## 37.6 Performance Checklist

- [ ] Is the problem reproducible?
- [ ] Did I record a profile?
- [ ] What consumes the most time?
- [ ] Is work repeated unnecessarily?
- [ ] Is there a large loop?
- [ ] Is DOM layout repeatedly forced?
- [ ] Are renders excessive?
- [ ] Is network latency the real bottleneck?
- [ ] Is JSON/data volume unexpectedly large?
- [ ] Did performance improve after the change?

---

## 37.7 Memory Leak Checklist

- [ ] Does memory continuously grow?
- [ ] Are listeners cleaned up?
- [ ] Are timers cleared?
- [ ] Are subscriptions disposed?
- [ ] Is cache bounded?
- [ ] Are detached DOM nodes retained?
- [ ] Are large values captured by closures?
- [ ] Do heap snapshots show growing object counts?

---

# 38. Practice Labs

These exercises are intentionally buggy. Try debugging them before reading the hints.

## Lab 1: Wrong Total

```js
function calculateTotal(price, quantity) {
  return price + quantity;
}

console.log(calculateTotal(100, 3));
```

Expected:

```text
300
```

### Hint

Check the business operation, not syntax.

---

## Lab 2: Missing User

```js
const users = [
  { id: 1, name: "Asha" },
  { id: 2, name: "Ravi" }
];

const user = users.find(user => user.id === "2");

console.log(user.name);
```

### Hint

Inspect both value and type.

### Root Cause

`user.id` is a number, but `"2"` is a string.

Possible intentional fix:

```js
const user = users.find(user => user.id === 2);
```

---

## Lab 3: Promise Instead of Data

```js
async function getSettings() {
  return {
    theme: "dark"
  };
}

function start() {
  const settings = getSettings();
  console.log(settings.theme);
}

start();
```

### Hint

Inspect `settings`.

---

## Lab 4: Mutation Surprise

```js
const original = {
  options: {
    debug: false
  }
};

const copy = {
  ...original
};

copy.options.debug = true;

console.log(original.options.debug);
```

Predict the output before running.

### Output

```text
true
```

### Why

The nested `options` object is shared.

---

## Lab 5: Async Loop

```js
async function wait(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function run() {
  [1, 2, 3].forEach(async number => {
    await wait(100);
    console.log(number);
  });

  console.log("done");
}

run();
```

Possible output:

```text
done
1
2
3
```

### Challenge

Rewrite it so `done` appears last.

Sequential:

```js
async function run() {
  for (const number of [1, 2, 3]) {
    await wait(100);
    console.log(number);
  }

  console.log("done");
}
```

---

## Lab 6: Event Delegation

HTML:

```html
<ul id="users">
  <li>
    Asha
    <span>
      <button data-id="1">Delete</button>
    </span>
  </li>
</ul>
```

Buggy JavaScript:

```js
document.querySelector("#users")
  .addEventListener("click", event => {
    if (!event.target.matches("li")) {
      return;
    }

    console.log("delete");
  });
```

Clicking the button does not print.

### Hint

Inspect `event.target` and use `closest()` based on the element you actually want.

---

## Lab 7: API Status

```js
async function load() {
  const response = await fetch("/missing");

  const data = await response.json();
  return data;
}
```

### Challenge

Improve error handling so the HTTP status is checked before data is used.

---

## Lab 8: Memory Leak

```js
function openPage() {
  setInterval(() => {
    console.log("refresh");
  }, 1000);
}

openPage();
openPage();
openPage();
```

### Questions

- How many intervals exist?
- How would you store IDs?
- When should they be cleared?

---

## Lab 9: Wrong Default

```js
function getPageSize(value) {
  return value || 25;
}

console.log(getPageSize(0));
```

If `0` is intentionally supported, fix the defaulting logic.

---

## Lab 10: Race Condition

```js
async function showUser(id) {
  const response = await fetch(`/api/users/${id}`);
  const user = await response.json();

  render(user);
}

showUser(1);
showUser(2);
```

If request 1 finishes last, user 1 can overwrite user 2.

### Challenge

Implement a latest-request guard or cancellation.

---

# 39. JavaScript Debugging Cheat Sheet

## Fast Mental Model

```text
Reproduce
↓
Expected vs Actual
↓
Read Error
↓
Locate First Wrong Value
↓
Trace Backward
↓
Form Hypothesis
↓
Test One Thing
↓
Fix Root Cause
↓
Regression Test
```

---

## Useful Console Calls

```js
console.log(value);
console.log({ value, type: typeof value });
console.error(error);
console.warn(message);
console.table(rows);
console.trace();
console.count("label");
console.time("label");
console.timeEnd("label");
console.group("label");
console.groupEnd();
console.assert(condition, "message");
```

---

## Useful Type Checks

```js
typeof value
Array.isArray(value)
value === null
Number.isNaN(value)
Number.isFinite(value)
```

---

## Useful Safe Access

```js
user?.profile?.name
```

Use when missing data is acceptable.

---

## Useful Defaulting

```js
value ?? fallback
```

Use when only `null`/`undefined` should trigger the fallback.

---

## Debug a Request

```js
const response = await fetch(url);

console.log({
  status: response.status,
  ok: response.ok,
  contentType: response.headers.get("content-type")
});
```

---

## Debug Function Input/Output

```js
function transform(input) {
  console.debug("transform input", input);

  const output = /* ... */;

  console.debug("transform output", output);
  return output;
}
```

---

## Node Inspector

```bash
node --inspect app.js
```

Break at start:

```bash
node --inspect-brk app.js
```

---

## Browser Debugger Controls

```text
Resume      → continue
Step over   → run line, do not enter function
Step into   → enter function
Step out    → finish current function
```

---

## Best Places to Add a Breakpoint

```text
function entry
before suspicious condition
before mutation
after API response
before render
inside failing loop
before return
```

---

## Red Flags

```text
"Cannot read properties of undefined"
"X is not a function"
"X is not defined"
"Unexpected token"
"Failed to fetch"
"Unhandled promise rejection"
"Maximum call stack"
"Out of memory"
```

Always investigate the underlying data and execution path.

---

# 40. Glossary

## Breakpoint

A location where the debugger pauses execution.

## Call Stack

The ordered stack of currently active function calls.

## Closure

A function together with access to variables from its lexical environment.

## CORS

Browser security mechanism controlling certain cross-origin requests.

## DevTools

Browser-provided developer debugging and inspection tools.

## Event Loop

The runtime mechanism coordinating synchronous execution with queued asynchronous work.

## Heap

Managed memory where objects and other runtime allocations are stored.

## Heisenbug

A bug whose behavior changes when you try to observe or debug it.

## Logpoint

A debugger location that logs a message without pausing or changing source code.

## Memory Leak

Memory retained unintentionally so usage keeps growing.

## Microtask

A high-priority queued unit of asynchronous work commonly used by Promise reactions.

## Network Request

Communication between the client and another resource/server.

## Race Condition

A bug where behavior depends on the order or timing of asynchronous operations.

## Regression

A previously working behavior that becomes broken after a change.

## Source Map

Metadata connecting generated/transformed JavaScript back to original source code.

## Stack Trace

A report showing function call frames around an error.

## Watch Expression

An expression automatically reevaluated by the debugger while paused or stepping.

---

# 41. Final Debugging Mindset

Great debuggers are not developers who never create bugs.

They are developers who can move from:

```text
"It is broken"
```

to:

```text
"At this exact boundary, this value becomes incorrect because this assumption is false."
```

The most important habits are:

1. **Reproduce before changing code.**
2. **Read errors completely.**
3. **Inspect actual values instead of assumptions.**
4. **Use breakpoints when logs are insufficient.**
5. **Use the Network panel for API problems.**
6. **Understand asynchronous execution.**
7. **Trace the first wrong value backward.**
8. **Separate symptoms from root causes.**
9. **Make one controlled change at a time.**
10. **Turn important bugs into regression tests.**
11. **Protect secrets while logging.**
12. **Measure performance and memory instead of guessing.**
13. **Record environment and release information for production problems.**
14. **Prefer evidence over intuition.**

A strong debugging question is not:

> "What code should I change?"

It is:

> "What evidence would prove where the program first stops behaving as intended?"

Once you can answer that reliably, debugging becomes a systematic engineering skill instead of trial and error.

---

# Appendix A: Extended Debugging Recipes

## Recipe A1: Find Where a Value Changes

Suppose:

```js
let status = "draft";
```

Later it unexpectedly becomes:

```text
"cancelled"
```

Possible approaches:

### Approach 1: Search assignments

Search project for:

```text
status =
```

and mutating operations.

### Approach 2: Encapsulate mutation

```js
let status = "draft";

function setStatus(nextStatus) {
  console.trace("status changed", {
    from: status,
    to: nextStatus
  });

  status = nextStatus;
}
```

Now every change has a call stack.

### Approach 3: Property setter for diagnostic experimentation

```js
const order = {
  _status: "draft",

  get status() {
    return this._status;
  },

  set status(value) {
    console.trace("status assignment", {
      from: this._status,
      to: value
    });

    this._status = value;
  }
};
```

This technique can help isolate unexpected property assignment in controlled debugging code.

---

## Recipe A2: Find Why a Function Runs Too Often

```js
function refresh() {
  console.count("refresh");
  console.trace("refresh caller");
}
```

Then inspect:

- repeated event listeners,
- repeated timers,
- rerender lifecycle,
- retry loops,
- subscriptions.

---

## Recipe A3: Debug a Broken Conditional

Bug:

```js
if (user.role === "admin" && user.active || user.isOwner) {
  allowAccess();
}
```

Do not stare at the whole expression.

Break it down:

```js
const isAdmin = user.role === "admin";
const isActive = user.active;
const isOwner = user.isOwner;

console.log({
  isAdmin,
  isActive,
  isOwner,
  result: (isAdmin && isActive) || isOwner
});
```

Parentheses make intention clear:

```js
if ((isAdmin && isActive) || isOwner) {
  allowAccess();
}
```

If the requirement differs, change the expression based on the rule, not intuition.

---

## Recipe A4: Debug a `filter()` Problem

```js
const activeUsers = users.filter(user => {
  user.active;
});
```

Output:

```text
[]
```

Why?

The callback with braces does not return.

Correct:

```js
const activeUsers = users.filter(user => {
  return user.active;
});
```

or:

```js
const activeUsers = users.filter(user => user.active);
```

---

## Recipe A5: Debug a `reduce()` Problem

Bug:

```js
const total = items.reduce((sum, item) => {
  sum + item.price;
}, 0);
```

The callback returns `undefined`.

Correct:

```js
const total = items.reduce((sum, item) => {
  return sum + item.price;
}, 0);
```

Debug intermediate accumulator:

```js
const total = items.reduce((sum, item) => {
  console.log({ sum, item });

  const next = sum + item.price;

  console.log({ next });

  return next;
}, 0);
```

---

## Recipe A6: Debug an Infinite Loop

```js
let i = 0;

while (i < 10) {
  console.log(i);
}
```

`i` never changes.

Possible safeguards during investigation:

```js
let i = 0;
let guard = 0;

while (i < 10) {
  if (++guard > 100) {
    throw new Error("Loop guard triggered");
  }

  // ...
}
```

A loop guard is diagnostic protection, not a substitute for fixing loop logic.

---

## Recipe A7: Debug Recursion

```js
function countDown(n) {
  return countDown(n - 1);
}
```

No base case.

Correct concept:

```js
function countDown(n) {
  if (n <= 0) {
    return;
  }

  console.log(n);
  countDown(n - 1);
}
```

When debugging recursion inspect:

- base condition,
- input changes,
- stack growth.

---

## Recipe A8: Debug an Unexpected `undefined`

Ask which of these categories applies:

```text
variable never assigned
function returned nothing
object property missing
array index out of range
optional API field absent
async work not finished
failed lookup (`find`)
wrong destructuring
wrong import
```

Example:

```js
const user = users.find(user => user.id === 999);
```

If no match exists:

```text
undefined
```

So:

```js
user.name
```

fails.

Debug the lookup result before using it.

---

## Recipe A9: Debug Destructuring

Bug:

```js
const response = {
  data: {
    user: {
      name: "Asha"
    }
  }
};

const { user } = response;

console.log(user.name);
```

`user` is undefined because it is nested under `data`.

Correct:

```js
const {
  data: { user }
} = response;
```

Or use clearer staged access:

```js
const data = response.data;
const user = data.user;
```

Staged access can be easier while debugging.

---

## Recipe A10: Debug Unexpected Mutation with `Object.freeze()`

During development:

```js
const config = Object.freeze({
  apiUrl: "/api",
  mode: "production"
});
```

This prevents changing direct properties of that object.

Important:

`Object.freeze()` is shallow.

Nested objects need separate handling if you want deep immutability.

Use strict mode/module semantics and suitable tooling to make mutation failures visible.

---

# Appendix B: Debugging Data Contracts

Many JavaScript bugs are actually **contract bugs**.

A contract defines what data is expected.

Example:

```js
/**
 * Expected:
 * {
 *   id: number,
 *   name: string,
 *   active: boolean
 * }
 */
function renderUser(user) {
  // ...
}
```

If server sends:

```json
{
  "user_id": "1",
  "full_name": "Asha",
  "is_active": 1
}
```

the problem is not necessarily in rendering. You need an adapter:

```js
function mapApiUser(raw) {
  return {
    id: Number(raw.user_id),
    name: raw.full_name,
    active: Boolean(raw.is_active)
  };
}
```

Debug contract boundaries rather than allowing raw external data to spread throughout the application.

---

## Runtime Validation

For critical data, validate explicitly.

```js
function assertUser(value) {
  if (!value || typeof value !== "object") {
    throw new TypeError("User must be an object");
  }

  if (typeof value.id !== "number") {
    throw new TypeError("User.id must be a number");
  }

  if (typeof value.name !== "string") {
    throw new TypeError("User.name must be a string");
  }
}
```

Then:

```js
const raw = await fetchUser();
assertUser(raw);
renderUser(raw);
```

This makes invalid data fail close to the boundary.

For large systems, schema-validation libraries or TypeScript can improve developer feedback, but runtime validation is still required for untrusted external data when correctness depends on it.

---

# Appendix C: Debugging Dates and Timezones

Date bugs deserve special attention.

## C.1 Distinguish Three Concepts

### Calendar date

```text
2026-08-17
```

Example: birthday or invoice date.

### Local datetime

```text
2026-08-17 09:30 in Mumbai
```

### Instant

A globally specific moment representable as a timestamp/UTC time.

Confusing these concepts creates timezone bugs.

---

## C.2 Log Date Diagnostics

```js
function debugDate(label, date) {
  console.log(label, {
    value: date,
    timestamp: date.getTime(),
    iso: Number.isNaN(date.getTime())
      ? "invalid"
      : date.toISOString(),
    local: date.toString(),
    timezone: Intl.DateTimeFormat()
      .resolvedOptions()
      .timeZone
  });
}
```

---

## C.3 Invalid Date

```js
const date = new Date("not a date");

console.log(date.toString());
```

Output:

```text
Invalid Date
```

Check:

```js
Number.isNaN(date.getTime())
```

---

# Appendix D: Debugging Numbers and Floating Point

JavaScript numbers use IEEE-754 floating-point semantics for the `number` type.

Classic example:

```js
console.log(0.1 + 0.2);
```

Output is commonly:

```text
0.30000000000000004
```

Do not debug financial calculations assuming all decimal fractions are exact binary floating-point values.

Depending on requirements, use strategies such as:

- integer smallest units, e.g. paise/cents,
- decimal arithmetic libraries,
- explicit rounding rules.

Example using integer paise:

```js
const pricePaise = 1999;
const taxPaise = 360;
const totalPaise = pricePaise + taxPaise;

console.log(totalPaise); // 2359
```

---

## Rounding Debugging

```js
const value = 1.005;
console.log(Math.round(value * 100) / 100);
```

Floating-point representation can produce results that surprise people.

When money or compliance matters, define exact rounding rules and test boundary values.

---

# Appendix E: Debugging Regular Expressions

Regex bugs are often caused by hidden assumptions.

Example:

```js
const pattern = /^\d+$/;

console.log(pattern.test("123"));  // true
console.log(pattern.test("12a"));  // false
```

Debug by testing small examples.

---

## Global Regex State

A regex with the `g` flag can maintain `lastIndex` state when using methods such as `.test()`.

Example:

```js
const regex = /a/g;

console.log(regex.test("a"));
console.log(regex.test("a"));
```

The second result can surprise learners because `lastIndex` changes.

Inspect:

```js
console.log(regex.lastIndex);
```

Reset when appropriate:

```js
regex.lastIndex = 0;
```

Or avoid the global flag when stateful scanning is not intended.

---

# Appendix F: Debugging JSON

## F.1 Parsing

```js
const text = '{"name":"Asha"}';
const user = JSON.parse(text);
```

Invalid:

```js
JSON.parse("{name:'Asha'}");
```

JSON requires its own strict syntax; it is not identical to JavaScript object literal syntax.

---

## F.2 Stringifying

```js
JSON.stringify({
  name: "Asha",
  age: 30
});
```

Formatted:

```js
JSON.stringify(object, null, 2);
```

Useful for snapshots, API payload inspection, and simple structured logging.

---

## F.3 Circular References

```js
const obj = {};
obj.self = obj;

JSON.stringify(obj);
```

throws because JSON cannot represent cycles.

Do not assume JSON serialization works for every JavaScript object graph.

---

# Appendix G: Debugging Prototypes and Classes

## G.1 Missing Method

```js
class User {
  greet() {
    return "hello";
  }
}

const raw = JSON.parse('{"name":"Asha"}');

console.log(raw.greet());
```

Error:

```text
raw.greet is not a function
```

Parsing JSON creates plain data objects, not class instances.

Debug prototypes:

```js
console.log(Object.getPrototypeOf(raw));
```

---

## G.2 Method Loses `this`

```js
class Counter {
  constructor() {
    this.count = 0;
  }

  increment() {
    this.count++;
  }
}

const counter = new Counter();
const increment = counter.increment;

increment();
```

The method is detached from the instance.

Possible deliberate binding:

```js
const increment = counter.increment.bind(counter);
```

The correct design depends on how callbacks are passed.

---

# Appendix H: Debugging Build and Dependency Problems

Sometimes JavaScript source is correct but the project cannot build or run.

## H.1 Clean Error Classification

Separate:

```text
syntax error
runtime error
module resolution error
package installation error
build tool error
environment/config error
type checker/linter error
```

Do not treat every terminal message as a JavaScript language bug.

---

## H.2 Dependency Version Mismatch

Symptoms:

```text
API missing
function signature changed
peer dependency conflict
works on one machine
```

Investigate:

- lockfile,
- installed package version,
- runtime version,
- package documentation for the installed version.

Avoid blindly deleting lockfiles as your first debugging step. A lockfile is valuable evidence of the dependency graph.

---

## H.3 Reproducible Installs

Keep dependency metadata and lockfiles under source control when appropriate for the project.

A reproducible environment reduces "works on my machine" bugs.

---

# Appendix I: A Senior-Level Root Cause Analysis Template

Use this for important defects.

## Incident Summary

```text
What failed?
Who/what was affected?
When did it begin?
How was it detected?
```

## Expected Behavior

```text
What should the system have done?
```

## Actual Behavior

```text
What happened instead?
```

## Reproduction

```text
Exact steps/input/environment
```

## Technical Root Cause

```text
The earliest incorrect assumption/state that caused the failure.
```

## Why Tests Did Not Catch It

```text
Missing scenario?
Wrong mock?
Environment difference?
No integration coverage?
```

## Fix

```text
What changed?
```

## Regression Protection

```text
Test added?
Validation added?
Monitoring added?
```

## Follow-Up Prevention

```text
Code review rule?
Schema validation?
Tooling?
Documentation?
Deployment safeguard?
```

The goal is not to blame a person. The goal is to improve the system so the same class of bug becomes less likely.

---

# Appendix J: Daily Debugging Habits

Before coding:

- understand data contracts,
- know expected behavior,
- identify edge cases.

While coding:

- use clear variable names,
- keep functions focused,
- validate boundaries,
- handle async failures,
- avoid hidden mutation.

When a bug appears:

- reproduce,
- observe,
- reduce,
- inspect,
- hypothesize,
- test,
- fix,
- verify.

Before closing the bug:

- remove temporary noisy logs,
- remove accidental `debugger` statements,
- keep useful structured diagnostics,
- add tests,
- document important assumptions.

---

**End of JavaScript Debugging Master Handbook**

---

# Appendix K: Recommended JavaScript Debugging Tools and Configuration

JavaScript debugging spans several runtimes. The correct tool depends on whether your code runs in a browser, Node.js, a worker, a test runner, a framework, or a bundled production build.

## K.1 Recommended beginner toolchain

For browser JavaScript:

```text
VS Code
+ browser DevTools
+ ESLint
+ tests
+ Git
```

For Node.js:

```text
VS Code built-in JavaScript debugger
+ Node.js Inspector
+ ESLint
+ tests
+ Git
```

## K.2 Browser DevTools

Chrome/Chromium DevTools provides a full JavaScript debugger in the **Sources** panel.

Learn these features first:

```text
line breakpoint
conditional breakpoint
logpoint
DOM/event-listener breakpoint
pause on exceptions
Step Over
Step Into
Step Out
Call Stack
Scope
Watch
Console
Network
Performance
Memory
```

A breakpoint is usually better than adding many `console.log()` statements because it pauses at the real state and lets you inspect several variables without editing the source.

## K.3 Pause on exceptions

Enable pause-on-exceptions when an exception is caught later or transformed by framework code.

Use the narrowest useful mode because many libraries throw/catch exceptions internally as part of normal behavior.

When paused, ask:

```text
What value caused the throw?
Where was it created?
Which async/caller path led here?
Is this authored code or framework/library code?
```

## K.4 Source maps

Bundlers/transpilers often execute generated JavaScript while you want to debug original source.

A source map connects:

```text
generated bundle
↔ original JS/TS source
```

For TypeScript, a common compiler setting is:

```json
{
  "compilerOptions": {
    "sourceMap": true
  }
}
```

If a breakpoint is unverified:

1. confirm source maps were generated,
2. confirm DevTools/VS Code loaded them,
3. confirm paths inside the map point to the correct sources,
4. confirm the running bundle is the build you expect.

Production source-map publication is an operational/security decision because maps may expose more source detail. Decide intentionally how they are stored and who can access them.

## K.5 VS Code built-in JavaScript debugger

VS Code includes JavaScript/Node debugging support; a separate Node debugger extension is normally unnecessary.

A simple Node launch configuration:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "launch",
      "name": "Debug Node App",
      "program": "${workspaceFolder}/app.js"
    }
  ]
}
```

Useful VS Code debugger features include:

- conditional breakpoints,
- logpoints,
- watch expressions,
- call stacks,
- loaded scripts,
- source-map support,
- attach to Node,
- browser debugging.

## K.6 Node.js Inspector

Start a Node process with Inspector enabled:

```bash
node --inspect app.js
```

To pause before application code begins:

```bash
node --inspect-brk app.js
```

Then attach with VS Code or compatible DevTools.

The inspector endpoint is powerful. Do not expose it to an untrusted network.

## K.7 Attach to Node from VS Code

A typical local attach configuration:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "attach",
      "name": "Attach to Node",
      "port": 9229
    }
  ]
}
```

If several Node processes exist, verify the PID/port and attach to the correct process.

## K.8 Browser debugging from VS Code

VS Code can launch/attach browser debugging workflows for supported browsers.

For simple debugging, browser DevTools may be faster.

Prefer VS Code browser debugging when you want:

- breakpoints beside your source project,
- one debugger UI for frontend and backend,
- workspace-aware source maps,
- reproducible launch configurations.

## K.9 ESLint

ESLint catches suspicious patterns before runtime and improves consistency.

Create/configure ESLint using its current official setup flow, then run:

```bash
npx eslint .
```

Modern ESLint projects commonly use a flat configuration file such as:

```js
// eslint.config.js
import { defineConfig } from "eslint/config";

export default defineConfig([
  {
    files: ["**/*.js"],
    rules: {
      "no-undef": "error",
      "no-unreachable": "error"
    }
  }
]);
```

Do not blindly enable hundreds of rules. Begin with a coherent recommended configuration and add project rules intentionally.

## K.10 ESLint in VS Code

The ESLint VS Code extension can show lint diagnostics while editing.

Useful workflow:

```text
editor warning
→ read exact rule
→ understand why it fired
→ fix code
→ run project lint command
→ run tests
```

Avoid disabling rules globally just because one line is inconvenient. Use a narrow suppression only when you can explain why the code is safe.

## K.11 TypeScript as a bug-prevention tool

Even in a JavaScript-focused project, type checking can prevent common runtime mistakes.

For TypeScript projects:

```bash
npx tsc --noEmit
```

can type-check without writing emitted JavaScript, depending on project configuration.

For JavaScript projects, JSDoc plus type-aware editor tooling can provide partial type checking without a full conversion.

Type checking does not replace runtime tests for API responses, storage, browser behavior, or timing bugs.

## K.12 Network debugging

For API bugs, inspect the browser Network panel before changing JavaScript.

Record:

```text
request URL
method
status
request headers
request payload
response headers
response body
timing
initiator
CORS/preflight behavior
```

A `TypeError` in frontend code may actually be caused by the server returning an HTML error page where JSON was expected.

## K.13 Node command-line diagnostics

Useful baseline commands:

```bash
node --version
npm --version
npm ls
npm explain <package>
```

For dependency problems, also inspect the lock file and exact package-manager error.

Do not "fix" dependency issues by deleting the lock file until you understand what changed.

## K.14 CPU performance

For browser code, record a representative workload in DevTools **Performance** panel.

For Node.js, you can start with Inspector:

```bash
node --inspect app.js
```

and connect compatible DevTools to record CPU/performance information.

A CPU profile answers:

```text
Which functions consumed time?
Which functions ran very frequently?
Was time spent in my code or runtime/library work?
```

Always reproduce a realistic workload.

## K.15 Memory debugging

Browser DevTools Memory tooling can help investigate:

- detached DOM nodes,
- retained listeners,
- accidental global references,
- large caches,
- object growth over repeated actions.

Use repeated snapshots/measurements:

```text
baseline
→ perform action repeatedly
→ allow cleanup
→ measure again
```

One large heap is not automatically a leak.

## K.16 Framework DevTools

Framework-specific DevTools can explain framework state that a generic JavaScript debugger cannot easily summarize.

Examples of useful categories:

```text
component tree
props/inputs
state
render/update timing
routing state
dependency injection
framework performance
```

Install the official/maintained DevTools for the framework and browser you actually use.

Still return to standard JavaScript evidence when the underlying problem is:

- network,
- promise timing,
- object mutation,
- source maps,
- browser APIs,
- Node/runtime behavior.

## K.17 Tests as debugging entry points

Use the smallest test that reproduces the bug.

Typical command pattern depends on the project:

```bash
npm test
```

or a test-runner-specific command.

A focused failing test gives you:

```text
known input
known expected output
repeatable failure
safe place for breakpoints
regression protection
```

After fixing it, run related tests and then the broader suite.

## K.18 Production debugging

Do not enable public debug endpoints or ship secrets inside logs/source maps.

Prefer:

```text
structured logs
error tracking
metrics
distributed tracing
release/build IDs
sanitized request context
performance monitoring
controlled profiling
```

Every production error should be traceable to the exact deployed build.

## K.19 A practical VS Code workspace setup

Example `.vscode/launch.json` with browser/backend concepts should remain project-specific rather than becoming a giant universal configuration.

Keep separate named configurations such as:

```text
Debug Node API
Debug Frontend
Attach to Node
Debug Tests
```

This makes the expected entry point and environment obvious.

## K.20 Tool-selection guide

| Problem | First tool |
|---|---|
| Wrong variable/state | breakpoint + Scope/Watch |
| Click handler not firing | Event Listener breakpoint |
| API fails | Network panel |
| Promise order bug | async stack + breakpoints |
| Node startup bug | `--inspect-brk` |
| Generated/minified code | source maps |
| Slow browser interaction | Performance panel |
| Suspected browser leak | Memory panel |
| Suspicious code pattern | ESLint/type checker |
| Regression after commit | tests + `git bisect` |
| Production exception | error tracking/logs + build ID |

## K.21 Official references

- Chrome DevTools JavaScript debugging: <https://developer.chrome.com/docs/devtools/javascript>
- Chrome DevTools breakpoints: <https://developer.chrome.com/docs/devtools/javascript/breakpoints>
- Chrome DevTools source maps: <https://developer.chrome.com/docs/devtools/javascript/source-maps>
- Chrome DevTools Performance: <https://developer.chrome.com/docs/devtools/performance/>
- VS Code Node.js debugging: <https://code.visualstudio.com/docs/nodejs/nodejs-debugging>
- VS Code browser debugging: <https://code.visualstudio.com/docs/nodejs/browser-debugging>
- ESLint getting started: <https://eslint.org/docs/latest/use/getting-started>
- ESLint configuration: <https://eslint.org/docs/latest/use/configure/configuration-files>

---
