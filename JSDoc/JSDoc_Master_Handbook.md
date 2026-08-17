# JSDoc Master Handbook

> A beginner-to-advanced, practical guide to documenting JavaScript with JSDoc, improving IntelliSense, adding type checking to JavaScript, generating API documentation, and understanding equivalent documentation systems in other languages.

**Last reviewed:** August 17, 2026

---

## Table of Contents

1. [What Is JSDoc?](#1-what-is-jsdoc)
2. [Why JSDoc Matters](#2-why-jsdoc-matters)
3. [JSDoc vs Comments vs TypeScript](#3-jsdoc-vs-comments-vs-typescript)
4. [Installing and Running JSDoc](#4-installing-and-running-jsdoc)
5. [Anatomy of a JSDoc Comment](#5-anatomy-of-a-jsdoc-comment)
6. [Your First JSDoc Examples](#6-your-first-jsdoc-examples)
7. [JSDoc Type Expressions](#7-jsdoc-type-expressions)
8. [Documenting Function Parameters](#8-documenting-function-parameters)
9. [Documenting Return Values](#9-documenting-return-values)
10. [Documenting Variables, Constants, and Properties](#10-documenting-variables-constants-and-properties)
11. [Custom Object Types with `@typedef`](#11-custom-object-types-with-typedef)
12. [Callbacks with `@callback`](#12-callbacks-with-callback)
13. [Generics with `@template`](#13-generics-with-template)
14. [Examples with `@example`](#14-examples-with-example)
15. [Errors with `@throws`](#15-errors-with-throws)
16. [Optional, Default, Rest, and Destructured Parameters](#16-optional-default-rest-and-destructured-parameters)
17. [Async Functions and Promises](#17-async-functions-and-promises)
18. [Generator Functions and `@yields`](#18-generator-functions-and-yields)
19. [Classes and Object-Oriented JavaScript](#19-classes-and-object-oriented-javascript)
20. [Inheritance, Interfaces, and Overrides](#20-inheritance-interfaces-and-overrides)
21. [Access and Visibility Tags](#21-access-and-visibility-tags)
22. [Modules: ES Modules and CommonJS](#22-modules-es-modules-and-commonjs)
23. [Namespaces and Namepaths](#23-namespaces-and-namepaths)
24. [Events, Emitters, and Listeners](#24-events-emitters-and-listeners)
25. [Mixins and Advanced Relationships](#25-mixins-and-advanced-relationships)
26. [Documentation Metadata Tags](#26-documentation-metadata-tags)
27. [Less-Common and Advanced JSDoc Tags](#27-less-common-and-advanced-jsdoc-tags)
28. [Inline Tags](#28-inline-tags)
29. [JSDoc with VS Code IntelliSense](#29-jsdoc-with-vs-code-intellisense)
30. [Type-Checking JavaScript with JSDoc and TypeScript](#30-type-checking-javascript-with-jsdoc-and-typescript)
31. [TypeScript-Specific JSDoc Features](#31-typescript-specific-jsdoc-features)
32. [Generating `.d.ts` Files from JavaScript](#32-generating-dts-files-from-javascript)
33. [JSDoc Configuration](#33-jsdoc-configuration)
34. [Important JSDoc CLI Options](#34-important-jsdoc-cli-options)
35. [README, Package Metadata, and Tutorials](#35-readme-package-metadata-and-tutorials)
36. [Markdown Inside JSDoc](#36-markdown-inside-jsdoc)
37. [JSDoc Plugins](#37-jsdoc-plugins)
38. [Templates and Custom Documentation Sites](#38-templates-and-custom-documentation-sites)
39. [Linting JSDoc with ESLint](#39-linting-jsdoc-with-eslint)
40. [Real-World Patterns](#40-real-world-patterns)
41. [Frontend, React, Node.js, and Express Examples](#41-frontend-react-nodejs-and-express-examples)
42. [Testing and Maintaining Documentation](#42-testing-and-maintaining-documentation)
43. [Common Mistakes](#43-common-mistakes)
44. [Best Practices](#44-best-practices)
45. [When Not to Use JSDoc](#45-when-not-to-use-jsdoc)
46. [JSDoc Tag Quick Reference](#46-jsdoc-tag-quick-reference)
47. [JSDoc in Other Languages: What to Use Instead](#47-jsdoc-in-other-languages-what-to-use-instead)
48. [VS Code Extension Recommendations](#48-vs-code-extension-recommendations)
49. [Suggested Project Setups](#49-suggested-project-setups)
50. [Practice Exercises](#50-practice-exercises)
51. [Final Learning Roadmap](#51-final-learning-roadmap)
52. [Official References](#52-official-references)

### Appendix

- [Appendix A: Final Cheat Sheet](#appendix-a-final-cheat-sheet)

---

# 1. What Is JSDoc?

JSDoc is a documentation system for JavaScript.

You write specially formatted comments directly above functions, classes, variables, modules, and other parts of your code. Tools can then read those comments to:

- generate API documentation;
- display better IntelliSense in editors;
- explain parameters and return values;
- describe custom object structures;
- show deprecation messages;
- describe errors and side effects;
- help developers understand how to use your code;
- provide type information for JavaScript;
- let TypeScript's language service type-check plain `.js` files.

A JSDoc block normally starts with `/**` rather than an ordinary `/*`.

```js
/**
 * Adds two numbers.
 *
 * @param {number} a - First number.
 * @param {number} b - Second number.
 * @returns {number} The sum.
 */
function add(a, b) {
  return a + b;
}
```

The code still remains normal JavaScript. JSDoc is stored in comments.

This makes JSDoc especially useful when you want better documentation and editor assistance without converting the entire project to TypeScript.

## One comment, several possible consumers

A JSDoc comment can be read by more than one tool, and those tools do not all interpret every tag in exactly the same way.

| Consumer | Main purpose | Example |
|---|---|---|
| JSDoc documentation generator | Produce API documentation/doclets | `npx jsdoc src -r` |
| VS Code / TypeScript language service | IntelliSense and JavaScript type analysis | `@param {string} name` |
| ESLint plugins | Enforce documentation rules | Require descriptions or matching parameter names |
| Humans | Understand the public contract | Purpose, units, side effects, examples |

This distinction matters because **a tag being useful to JSDoc does not automatically mean TypeScript uses it for type checking**, and TypeScript-aware JSDoc supports some type syntax that the JSDoc documentation generator may treat differently.

A safe mental model is:

> **JSDoc comments describe code; the JavaScript runtime does not execute the annotations.**

If an annotation says a value is a `number` but the program actually passes a string, the comment alone does not stop the call. Static-analysis tooling may warn you, but runtime validation requires JavaScript code.


---

# 2. Why JSDoc Matters

Consider this function:

```js
function calculate(a, b, c) {
  // ...
}
```

A new developer has several questions:

- What is `a`?
- Is `b` a number or string?
- Is `c` optional?
- What does the function return?
- Can it throw an error?
- What values are valid?
- Does it modify anything outside the function?
- Is it safe to call asynchronously?

Now compare:

```js
/**
 * Calculates the final order amount after discount.
 *
 * @param {number} subtotal - Order subtotal before discount.
 * @param {number} taxRate - Tax rate as a decimal, such as 0.18.
 * @param {number} [discount=0] - Optional discount amount.
 * @returns {number} Final payable amount.
 * @throws {RangeError} If subtotal, tax rate, or discount is negative.
 */
function calculate(subtotal, taxRate, discount = 0) {
  if (subtotal < 0 || taxRate < 0 || discount < 0) {
    throw new RangeError("Values cannot be negative.");
  }

  return subtotal + subtotal * taxRate - discount;
}
```

The second version communicates the function's contract without requiring the reader to inspect its implementation.

## Documentation is a contract

Good documentation answers:

> "What can callers rely on?"

Implementation answers:

> "How is it currently done?"

Those are different questions.

A caller normally needs the contract first.

---

# 3. JSDoc vs Comments vs TypeScript

These concepts are related but not identical.

## 3.1 Ordinary comments

```js
// Add two numbers.
function add(a, b) {
  return a + b;
}
```

Useful for humans, but tools usually cannot infer much structured information from it.

## 3.2 JSDoc

```js
/**
 * Adds two numbers.
 * @param {number} a
 * @param {number} b
 * @returns {number}
 */
function add(a, b) {
  return a + b;
}
```

Useful for:

- humans;
- IDEs;
- documentation generators;
- static-analysis tools.

## 3.3 TypeScript

```ts
function add(a: number, b: number): number {
  return a + b;
}
```

TypeScript puts types into the programming language syntax itself.

## 3.4 JSDoc + JavaScript

```js
// @ts-check

/**
 * @param {number} a
 * @param {number} b
 * @returns {number}
 */
function add(a, b) {
  return a + b;
}
```

This lets TypeScript's language service check ordinary JavaScript.

For many existing JavaScript projects, this is an excellent middle ground.

## 3.5 Choosing between them

| Situation | Good starting choice |
|---|---|
| Tiny internal note about *why* code exists | Ordinary comment |
| Existing JavaScript project that needs better API documentation | JSDoc |
| JavaScript project that wants editor type checking without conversion | JSDoc + `// @ts-check` or `checkJs` |
| New project that wants language-level static type syntax everywhere | TypeScript |
| Public library with JavaScript source and TypeScript consumers | JSDoc + declaration generation can be a practical option |

These approaches can also be combined. TypeScript projects still benefit from explanatory comments, and JSDoc-enabled JavaScript still needs clear variable and function names.

### What JSDoc does not replace

JSDoc does not replace:

- runtime validation of untrusted input;
- tests;
- meaningful names;
- API design;
- TypeScript when your project specifically requires TypeScript syntax and tooling;
- security checks.

Use documentation to make a contract understandable, not to pretend a contract is enforced at runtime.


---

# 4. Installing and Running JSDoc

## 4.1 Prerequisites

You normally need:

- Node.js;
- npm, pnpm, or Yarn;
- a JavaScript project.

Check:

```bash
node --version
npm --version
```

## 4.2 Install locally

Recommended:

```bash
npm install --save-dev jsdoc
```

Why local installation?

- each project controls its own dependency;
- different projects can use different versions;
- CI/CD can reproduce your environment;
- developers do not need a global installation.

## 4.3 Run with `npx`

For one file:

```bash
npx jsdoc src/math.js
```

JSDoc's default output directory is normally:

```text
out/
```

Open the generated `index.html` in your browser.

## 4.4 Document an entire source directory

```bash
npx jsdoc src -r
```

`-r` means recurse into subdirectories.

## 4.5 Add an npm script

`package.json`:

```json
{
  "scripts": {
    "docs": "jsdoc -c jsdoc.json"
  }
}
```

Run:

```bash
npm run docs
```

This is better than asking every developer to remember a long command.

## 4.6 Choose the output directory explicitly

For a real project, an explicit destination is easier to understand than relying on the default output folder:

```bash
npx jsdoc src -r -d docs
```

Inputs:

- `src` — source path to document;
- `-r` / `--recurse` — also scan nested directories;
- `-d docs` / `--destination docs` — write generated documentation to `docs/`.

Typical output:

```text
docs/
├── index.html
├── fonts/
├── scripts/
└── styles/
```

The exact generated files depend on the template.

### When not to install JSDoc globally

A global installation can be convenient for experiments, but it makes project builds less reproducible because the globally installed version may differ between machines. For team projects and CI, prefer a local development dependency and an npm script.


---

# 5. Anatomy of a JSDoc Comment

A typical JSDoc block:

```js
/**
 * Calculates the area of a rectangle.
 *
 * More detailed explanation can go here.
 *
 * @param {number} width - Width in pixels.
 * @param {number} height - Height in pixels.
 * @returns {number} Rectangle area.
 */
function area(width, height) {
  return width * height;
}
```

It contains several parts.

## 5.1 Opening marker

```js
/**
```

This is important.

Ordinary block comments start with:

```js
/*
```

JSDoc documentation blocks normally start with:

```js
/**
```

## 5.2 Description

```text
Calculates the area of a rectangle.
```

Explain purpose, not implementation trivia.

Poor:

```text
Loops over some stuff and returns a value.
```

Better:

```text
Calculates the total payable amount for an invoice.
```

## 5.3 Blank separator

A blank `*` line improves readability:

```js
/**
 * Short summary.
 *
 * Longer explanation.
 */
```

## 5.4 Tags

Tags begin with `@`.

Examples:

```text
@param
@returns
@throws
@example
@deprecated
```

## 5.5 Closing marker

```text
 */
```

## A reliable reading order

When you see a JSDoc block, read it in this order:

1. **Summary** — what does the symbol do?
2. **Long description** — what important behavior or constraints are not obvious?
3. **Inputs** — `@param`, properties, callbacks, type parameters.
4. **Output** — `@returns`, `@yields`, or produced side effects.
5. **Failures** — meaningful `@throws` conditions.
6. **Usage** — `@example`, links, deprecation guidance.

Not every block needs every part. The purpose of the structure is to make the public contract easy to scan.


---

# 6. Your First JSDoc Examples

## 6.1 Function without parameters

```js
/**
 * Returns the current application name.
 *
 * @returns {string} Application name.
 */
function getAppName() {
  return "Invoice Portal";
}
```

## 6.2 Function with parameters

```js
/**
 * Creates a greeting.
 *
 * @param {string} name - Person to greet.
 * @returns {string} Greeting message.
 */
function greet(name) {
  return `Hello, ${name}!`;
}
```

Expected:

```js
greet("Asha");
// "Hello, Asha!"
```

## 6.3 Function returning nothing

```js
/**
 * Logs a message.
 *
 * @param {string} message - Message to log.
 * @returns {void}
 */
function logMessage(message) {
  console.log(message);
}
```

You may also omit `@returns` when no useful return information needs documenting, depending on your team's style.

## 6.4 Boolean result

```js
/**
 * Checks whether a user is an adult.
 *
 * @param {number} age - Age in years.
 * @returns {boolean} `true` when age is at least 18.
 */
function isAdult(age) {
  return age >= 18;
}
```

---

# 7. JSDoc Type Expressions

Types are normally written inside `{}`.

```js
/** @type {string} */
let username = "Shoeb";
```

## 7.1 Primitive types

Common examples:

```text
string
number
boolean
bigint
symbol
undefined
null
Object
Function
Date
RegExp
Error
Promise
```

Examples:

```js
/** @type {string} */
let title;

/** @type {number} */
let count;

/** @type {boolean} */
let enabled;
```

## 7.2 Arrays

Common styles:

```js
/** @type {string[]} */
const names = [];

/** @type {Array<string>} */
const cities = [];
```

JSDoc/Closure-style syntax may also appear:

```js
/** @type {Array.<string>} */
const countries = [];
```

For modern code intended mainly for VS Code/TypeScript tooling, many teams prefer:

```text
string[]
Array<string>
```

because they resemble TypeScript syntax.

## 7.3 Union types

Value can be one of several types:

```js
/** @type {string | number} */
let id;
```

Classic JSDoc syntax also often appears as:

```js
/** @type {(string|number)} */
let id;
```

Example use:

```js
/**
 * @param {string | number} id
 */
function findUser(id) {}
```

## 7.4 Any value

```js
/** @type {*} */
let anything;
```

Avoid this when a more useful type can be expressed.

## 7.5 Unknown value

When using TypeScript-aware JSDoc:

```js
/** @type {unknown} */
let payload;
```

`unknown` is usually safer than `any` because it forces validation before use.

## 7.6 Nullable values

Classic Closure/JSDoc type expressions include nullable and non-nullable notation.

Example:

```js
/** @type {?string} */
let nickname;
```

In TypeScript-aware JavaScript, this style is often clearer:

```js
/** @type {string | null} */
let nickname;
```

## 7.7 Object literal type

```js
/** @type {{name: string, age: number}} */
const user = {
  name: "Asha",
  age: 30
};
```

Useful for small one-off structures.

For a structure used repeatedly, prefer `@typedef`.

## 7.8 Record/map type

```js
/** @type {Object<string, number>} */
const marks = {
  math: 90,
  science: 85
};
```

TypeScript-style alternative:

```js
/** @type {Record<string, number>} */
const marks = {};
```

## 7.9 Function type

```js
/** @type {(value: number) => number} */
const double = value => value * 2;
```

Closure-style form:

```js
/** @type {function(number): number} */
const double = value => value * 2;
```

Be aware that JSDoc's documentation generator and TypeScript's JSDoc parser overlap heavily, but they are not exactly the same dialect. Choose conventions that work with the tools used by your project.

---

# 8. Documenting Function Parameters

The basic syntax is:

```text
@param {Type} name - Description
```

Example:

```js
/**
 * Updates a customer's email address.
 *
 * @param {number} customerId - Database identifier.
 * @param {string} email - New email address.
 */
function updateCustomerEmail(customerId, email) {}
```

## Why describe parameters if names are obvious?

Because names do not explain:

- accepted range;
- units;
- expected format;
- nullability;
- side effects;
- business meaning.

Weak:

```js
@param {number} timeout - Timeout.
```

Better:

```js
@param {number} timeout - Maximum wait time in milliseconds.
```

## 8.1 Parameter constraints

```js
/**
 * Sets retry count.
 *
 * @param {number} retries - Integer from 0 through 5.
 */
function setRetries(retries) {}
```

## 8.2 Units

```js
/**
 * @param {number} durationMs - Duration in milliseconds.
 */
```

Do not leave units ambiguous.

## 8.3 Format

```js
/**
 * @param {string} invoiceDate - Date in `YYYY-MM-DD` format.
 */
```

## 8.4 Business meaning

```js
/**
 * @param {number} taxRate - Tax rate as a decimal; use `0.18` for 18%.
 */
```

This is far more useful than simply writing "tax rate."

## Reading an `@param` tag from left to right

A common parameter tag has three important parts:

```text
@param {Type} parameterName - Human-readable description.
```

For example:

```js
/**
 * @param {number} quantity - Number of items being ordered.
 */
```

- `{number}` describes the expected type.
- `quantity` must refer to the actual function parameter being documented.
- The description explains meaning that the name and type do not communicate, such as units, allowed ranges, format, or business meaning.

### Document meaning, not just type

Weak:

```js
/**
 * @param {number} timeout - Timeout.
 */
```

Better:

```js
/**
 * @param {number} timeoutMs - Maximum wait time in milliseconds before the request is aborted.
 */
```

The second version tells a caller what the value *means* and which unit it uses.

### Keep names synchronized with code

If the implementation changes from:

```js
function send(message) {}
```

to:

```js
function send(payload) {}
```

update `@param message` to `@param payload`. Documentation linters can help catch stale parameter names.


---

# 9. Documenting Return Values

Use:

```text
@returns {Type} Description
```

or the synonym:

```text
@return
```

Example:

```js
/**
 * Finds the larger of two numbers.
 *
 * @param {number} a
 * @param {number} b
 * @returns {number} The larger value.
 */
function max(a, b) {
  return a > b ? a : b;
}
```

## 9.1 Returning an object

```js
/**
 * Creates a user.
 *
 * @returns {{id: number, name: string}} Newly created user.
 */
function createUser() {
  return {
    id: 1,
    name: "Riya"
  };
}
```

For repeated object structures, prefer `@typedef`.

## 9.2 Returning an optional value

```js
/**
 * Finds a user by ID.
 *
 * @param {number} id
 * @returns {User | undefined} Matching user, or `undefined` when not found.
 */
function findUser(id) {}
```

The description explains the meaning of the missing value.

## 9.3 Promise return

```js
/**
 * Loads a user.
 *
 * @param {number} id
 * @returns {Promise<User>} A promise resolving to the user.
 */
async function loadUser(id) {}
```

## Runtime value vs documented type

`@returns` describes what the caller receives from the function.

```js
/**
 * @returns {number} Total price in rupees.
 */
```

It does not create or convert that value. The implementation must actually return a number for the documentation to remain truthful.

For an `async` function, document the promise:

```js
/**
 * @returns {Promise<User>} A promise that fulfills with the user.
 */
async function loadUser() {}
```

The caller receives a `Promise` immediately; the `User` is the fulfillment value.

### When a return description matters most

Include more than the type when the result has special meaning:

- `undefined` means “not found”;
- `null` means “known to have no value”;
- an empty array is valid and not an error;
- a number uses a particular unit or currency;
- an object is a snapshot rather than a live mutable object.

Those semantics are often more valuable than the type annotation itself.


---

# 10. Documenting Variables, Constants, and Properties

Use `@type`.

```js
/** @type {number} */
let retryCount = 0;
```

## 10.1 Constant

```js
/**
 * Maximum number of login attempts.
 *
 * @constant
 * @type {number}
 */
const MAX_LOGIN_ATTEMPTS = 5;
```

Compact form:

```js
/** @const {number} */
const MAX_LOGIN_ATTEMPTS = 5;
```

## 10.2 Default value

```js
/**
 * Default request timeout.
 *
 * @type {number}
 * @default 5000
 */
const DEFAULT_TIMEOUT = 5000;
```

## 10.3 Read-only value

```js
/**
 * Unique order ID.
 *
 * @readonly
 * @type {string}
 */
const orderId = "ORD-1001";
```

Note: documentation tags do not magically enforce runtime immutability. JavaScript semantics still determine what can actually be modified.

---


## 10.4 Enumerations with `@enum`

Use `@enum` when a group of constants represents a fixed set of related choices.

```js
/**
 * Supported order statuses.
 *
 * @enum {string}
 */
const OrderStatus = {
  PENDING: "pending",
  APPROVED: "approved",
  REJECTED: "rejected"
};
```

A function can then refer to the enum:

```js
/**
 * Changes an order's status.
 *
 * @param {number} orderId - Order identifier.
 * @param {OrderStatus} status - New order status.
 */
function updateOrderStatus(orderId, status) {
  // ...
}
```

### `@enum` vs a string union

For TypeScript-aware JSDoc, a reusable string-union typedef is another good option:

```js
/**
 * @typedef {"pending" | "approved" | "rejected"} OrderStatusValue
 */

/**
 * @param {OrderStatusValue} status
 */
function setStatus(status) {}
```

Use an enum-like object when your runtime code needs named constants such as `OrderStatus.APPROVED`.

Use a union typedef when you primarily need a type-level restriction and do not need a runtime object.

Do not confuse JSDoc `@enum` with TypeScript's native `enum` declaration. One is documentation/tooling metadata around JavaScript values; the other is TypeScript language syntax.


# 11. Custom Object Types with `@typedef`

`@typedef` is one of the most useful JSDoc features.

Suppose several functions use a user object:

```js
{
  id: 1,
  name: "Asha",
  email: "asha@example.com"
}
```

Instead of repeating the full object shape, define it once.

```js
/**
 * Represents an application user.
 *
 * @typedef {Object} User
 * @property {number} id - Unique user ID.
 * @property {string} name - Display name.
 * @property {string} email - Email address.
 */
```

Now reuse it:

```js
/**
 * Sends a welcome message.
 *
 * @param {User} user - User who should receive the message.
 */
function sendWelcomeMessage(user) {}
```

## 11.1 Optional properties

```js
/**
 * @typedef {Object} UserProfile
 * @property {number} id
 * @property {string} name
 * @property {string} [avatarUrl] - Optional avatar URL.
 */
```

## 11.2 Nested structures

```js
/**
 * @typedef {Object} Address
 * @property {string} city
 * @property {string} state
 * @property {string} country
 */

/**
 * @typedef {Object} Customer
 * @property {number} id
 * @property {string} name
 * @property {Address} address
 */
```

## 11.3 Nested properties inline

You can also document nested properties directly:

```js
/**
 * @typedef {Object} Customer
 * @property {number} id
 * @property {Object} address
 * @property {string} address.city
 * @property {string} address.country
 */
```

Separate typedefs are often cleaner when the nested object is meaningful on its own.

## 11.4 Union typedef

```js
/**
 * @typedef {string | number} UserId
 */
```

Then:

```js
/**
 * @param {UserId} id
 */
function getUser(id) {}
```

## 11.5 When to use `@typedef`

Use it when:

- an object shape is reused;
- a structure has business meaning;
- a union is used repeatedly;
- inline types become hard to read;
- you want IntelliSense for an object.

Do not create a typedef for every tiny one-off value. Too many named types can make documentation harder rather than easier.

---

# 12. Callbacks with `@callback`

A callback is a function passed to another function.

Define a callback type:

```js
/**
 * Called when a request completes.
 *
 * @callback RequestCallback
 * @param {Error | null} error - Error, or `null` when successful.
 * @param {string} data - Response data.
 * @returns {void}
 */
```

Use it:

```js
/**
 * Reads data.
 *
 * @param {RequestCallback} callback - Called when reading completes.
 */
function readData(callback) {}
```

## Real-world example

```js
/**
 * @typedef {Object} User
 * @property {number} id
 * @property {string} name
 */

/**
 * Handles a user selection.
 *
 * @callback UserSelectedHandler
 * @param {User} user - Selected user.
 * @returns {void}
 */

/**
 * Registers a user-selection handler.
 *
 * @param {UserSelectedHandler} handler
 */
function onUserSelected(handler) {}
```

A named callback is more readable than repeatedly writing a large function type.

## Why name a callback type?

Use `@callback` when the same function contract appears in multiple places or when an inline function type would be difficult to read.

```js
/**
 * Called after a payment attempt completes.
 *
 * @callback PaymentCompleteHandler
 * @param {string} transactionId - Payment transaction identifier.
 * @param {boolean} success - Whether the payment completed successfully.
 * @returns {void}
 */

/**
 * @param {PaymentCompleteHandler} onComplete - Completion callback.
 */
function processPayment(onComplete) {}
```

The callback definition tells a caller:

- how many arguments the function receives;
- the type and meaning of each argument;
- what the callback is expected to return.

### Optional callback

```js
/**
 * @param {PaymentCompleteHandler} [onComplete] - Optional completion callback.
 */
function processPayment(onComplete) {}
```

### When not to create a named callback

For a one-off, very small function type, an inline type may be easier:

```js
/**
 * @param {(value: string) => void} onValue
 */
```

That arrow-function type is especially natural when TypeScript's language service is the primary consumer. If generated JSDoc HTML is your main goal, prefer syntax supported by the documentation tool and test the generated output.


---

# 13. Generics with `@template`

Generics describe relationships between types.

This is especially useful when TypeScript's language service interprets JSDoc.

## 13.1 Identity function

```js
/**
 * Returns the same value that was provided.
 *
 * @template T
 * @param {T} value
 * @returns {T}
 */
function identity(value) {
  return value;
}
```

Usage:

```js
const a = identity(123);     // inferred number
const b = identity("hello"); // inferred string
```

The important idea is:

> the return type is the same type as the input.

Without a generic, you might lose that relationship.

## 13.2 Generic array helper

```js
/**
 * Returns the first item in an array.
 *
 * @template T
 * @param {T[]} items
 * @returns {T | undefined}
 */
function first(items) {
  return items[0];
}
```

## 13.3 Multiple type parameters

```js
/**
 * Creates a key-value pair.
 *
 * @template K
 * @template V
 * @param {K} key
 * @param {V} value
 * @returns {{key: K, value: V}}
 */
function pair(key, value) {
  return { key, value };
}
```

## Important distinction

`@template` is widely used by TypeScript-aware JSDoc tooling. If your goal is HTML generation with a specific JSDoc template or plugin, verify how that tool renders generic information.

## What problem a generic solves

A generic type parameter preserves a relationship between input and output.

Without a generic, this helper could be documented only as “takes some value and returns some value,” which loses information:

```js
/**
 * @template T
 * @param {T} value
 * @returns {T}
 */
function identity(value) {
  return value;
}
```

If a caller passes a string, tooling can infer a string result; if the caller passes a `User`, the result remains a `User`.

### Do not use a generic when types are unrelated

A type parameter is useful only when the same type variable connects meaningful positions. If a function always returns a string regardless of input, `@returns {string}` is clearer than inventing `T`.


---

# 14. Examples with `@example`

Examples show consumers how to use your API.

```js
/**
 * Adds two numbers.
 *
 * @param {number} a
 * @param {number} b
 * @returns {number}
 *
 * @example
 * add(2, 3);
 * // => 5
 */
function add(a, b) {
  return a + b;
}
```

## Multiple examples

```js
/**
 * Formats a name.
 *
 * @param {string} first
 * @param {string} last
 * @returns {string}
 *
 * @example
 * formatName("Asha", "Patel");
 * // => "Asha Patel"
 *
 * @example
 * formatName("", "Patel");
 * // => "Patel"
 */
function formatName(first, last) {
  return `${first} ${last}`.trim();
}
```

## What makes a good example?

A good example should:

- be short;
- use realistic values;
- demonstrate the common case first;
- show expected output when useful;
- avoid irrelevant setup;
- remain correct when the API changes.

Examples are executable-looking documentation. Stale examples are particularly dangerous because developers tend to copy them directly.

## Make examples copyable and observable

A useful example should usually show:

- the minimum setup;
- the call;
- an important result or effect.

```js
/**
 * @example
 * const total = addTax(100, 0.18);
 * console.log(total);
 * // 118
 */
```

Avoid examples that depend on undeclared variables, hidden global state, or a large setup that the reader cannot reproduce.

For public libraries, consider running important examples as tests or documentation tests so refactoring does not silently make them stale.


---

# 15. Errors with `@throws`

Use `@throws` or its synonym `@exception` to document exceptions that callers can reasonably expect and may need to handle.

```js
/**
 * Divides two numbers.
 *
 * @param {number} numerator - Number to divide.
 * @param {number} denominator - Number to divide by.
 * @returns {number} Division result.
 * @throws {RangeError} If `denominator` is zero.
 */
function divide(numerator, denominator) {
  if (denominator === 0) {
    throw new RangeError("Cannot divide by zero.");
  }

  return numerator / denominator;
}
```

Caller:

```js
try {
  console.log(divide(10, 0));
} catch (error) {
  console.error(error.message);
}
```

Possible output:

```text
Cannot divide by zero.
```

## 15.1 Multiple error types

A function can expose more than one meaningful failure contract:

```js
/**
 * Parses application configuration.
 *
 * @param {string} text - JSON configuration text.
 * @returns {Object} Parsed configuration object.
 * @throws {TypeError} If `text` is not a string.
 * @throws {SyntaxError} If `text` is not valid JSON.
 */
function parseConfig(text) {
  if (typeof text !== "string") {
    throw new TypeError("Configuration must be a string.");
  }

  return JSON.parse(text);
}
```

Do not list every theoretical exception from every internal function. Document failures that are part of the useful public contract.

## 15.2 Important async distinction

An exception thrown inside an `async` function does **not** escape to the caller as an immediate synchronous exception. The returned promise is rejected.

```js
/**
 * Loads a customer.
 *
 * @param {number} id - Customer ID.
 * @returns {Promise<Customer>} Promise that fulfills with the customer.
 */
async function loadCustomer(id) {
  if (id <= 0) {
    throw new RangeError("id must be positive");
  }

  // ...
}
```

Call it with promise-aware error handling:

```js
try {
  const customer = await loadCustomer(-1);
} catch (error) {
  console.error(error.message);
}
```

When documenting asynchronous APIs, describe important rejection conditions in prose and keep the `Promise<T>` return contract accurate. Do not assume that a documentation tag by itself gives the TypeScript checker a complete model of promise rejection types.

---

# 16. Optional, Default, Rest, and Destructured Parameters

## 16.1 Optional parameter

```js
/**
 * Greets a person.
 *
 * @param {string} [name] - Optional name.
 */
function greet(name) {}
```

## 16.2 Optional with default

```js
/**
 * Greets a person.
 *
 * @param {string} [name="Guest"] - Name to greet.
 */
function greet(name = "Guest") {
  return `Hello, ${name}`;
}
```

## 16.3 Rest parameters

```js
/**
 * Adds any number of values.
 *
 * @param {...number} values - Numbers to add.
 * @returns {number} Total.
 */
function sum(...values) {
  return values.reduce((total, value) => total + value, 0);
}
```

## 16.4 Object parameter

```js
/**
 * Creates a product.
 *
 * @param {Object} options - Product options.
 * @param {string} options.name - Product name.
 * @param {number} options.price - Product price.
 * @param {boolean} [options.active=true] - Whether the product is active.
 */
function createProduct(options) {}
```

## 16.5 Destructured parameter

```js
/**
 * Creates a product.
 *
 * @param {Object} options
 * @param {string} options.name
 * @param {number} options.price
 */
function createProduct({ name, price }) {
  return { name, price };
}
```

## Better approach for larger objects

```js
/**
 * @typedef {Object} ProductOptions
 * @property {string} name
 * @property {number} price
 * @property {boolean} [active=true]
 */

/**
 * Creates a product.
 *
 * @param {ProductOptions} options
 */
function createProduct(options) {}
```

This scales better.

## Keep JavaScript syntax and documentation in agreement

These two contracts should describe the same reality:

```js
function connect(host, timeout = 5000) {}
```

```js
/**
 * @param {string} host
 * @param {number} [timeout=5000]
 */
```

If the implementation default changes, update the documentation too.

### Rest parameters

For:

```js
function sum(...values) {}
```

document that callers may pass multiple values and type the repeated values appropriately.

### Destructuring

For destructured options, document the object itself and then its properties. This is easier to understand than pretending each property is a separate positional argument.


---

# 17. Async Functions and Promises

Async functions return promises.

```js
/**
 * Fetches a customer.
 *
 * @param {number} id - Customer ID.
 * @returns {Promise<Customer>} Customer loaded from the API.
 */
async function getCustomer(id) {
  // ...
}
```

## 17.1 Optional explicit `@async`

JSDoc provides an `@async` tag:

```js
/**
 * Fetches a customer.
 *
 * @async
 * @param {number} id
 * @returns {Promise<Customer>}
 */
async function getCustomer(id) {}
```

For normal `async function` declarations, the syntax already shows that it is async, so many teams prioritize documenting the promise result rather than repeating obvious syntax.

## 17.2 Promise resolving to nothing

```js
/**
 * Saves pending changes.
 *
 * @returns {Promise<void>}
 */
async function saveChanges() {}
```

## 17.3 Promise with optional result

```js
/**
 * Finds a cached item.
 *
 * @param {string} key
 * @returns {Promise<string | undefined>}
 */
async function findCachedValue(key) {}
```

## 17.4 Fulfillment and rejection are different outcomes

Think of an async function as returning a promise with two broad paths:

```text
call async function
        |
        v
    Promise<T>
     /      \
fulfill    reject
   |          |
   T        Error/reason
```

`@returns {Promise<T>}` describes the successful fulfillment value. Important rejection conditions should be explained in the description, examples, or error documentation because JavaScript promises do not carry an enforced “rejection type” parameter comparable to the fulfillment type.

### Common mistake

Incorrect mental model:

```text
async function returns T
```

Better mental model:

```text
async function returns Promise<T>
```

Even this function returns a promise:

```js
/**
 * @returns {Promise<number>}
 */
async function answer() {
  return 42;
}
```

Usage:

```js
console.log(await answer());
// 42
```


---

# 18. Generator Functions and `@yields`

Generator functions produce values over time.

```js
/**
 * Generates numbers from 1 through `max`.
 *
 * @generator
 * @param {number} max
 * @yields {number} Next number in the sequence.
 */
function* range(max) {
  for (let i = 1; i <= max; i++) {
    yield i;
  }
}
```

Usage:

```js
for (const value of range(3)) {
  console.log(value);
}
```

Output:

```text
1
2
3
```

For generator output, use `@yields` rather than describing each yielded value with `@returns`.

## 18.1 What the caller actually receives

Calling a generator function does not immediately run it to completion. It returns an iterator/generator object.

```js
const iterator = range(3);

console.log(iterator.next());
// { value: 1, done: false }
```

Each `yield` pauses execution and produces the next value.

`@yields` documents those repeatedly produced values. A generator can also have a final `return` value, which is conceptually different from the yielded sequence.

### TypeScript-aware advanced note

When TypeScript's language service is the consumer, a generator can be described with a type such as:

```js
/** @returns {Generator<number, void, unknown>} */
function* ids() {
  yield 1;
  yield 2;
}
```

The generic positions represent the yielded value, final return value, and value accepted by `next(...)`. Use this only when that extra precision is helpful; for generated API documentation, `@generator` plus `@yields` is often easier for readers.


---

# 19. Classes and Object-Oriented JavaScript

Modern JavaScript classes are normally recognized by JSDoc without needing `@class`.

```js
/**
 * Represents a bank account.
 */
class BankAccount {
  /**
   * Creates an account.
   *
   * @param {string} owner - Account holder name.
   * @param {number} [balance=0] - Opening balance.
   */
  constructor(owner, balance = 0) {
    this.owner = owner;
    this.balance = balance;
  }

  /**
   * Deposits money.
   *
   * @param {number} amount
   * @returns {number} New balance.
   */
  deposit(amount) {
    this.balance += amount;
    return this.balance;
  }
}
```

## 19.1 Traditional constructor function

Older JavaScript may use:

```js
/**
 * Represents a user.
 *
 * @constructor
 * @param {string} name
 */
function User(name) {
  this.name = name;
}
```

`@class` is a synonym of `@constructor`.

## 19.2 `@classdesc`

Useful when you need a dedicated class description:

```js
/**
 * @class
 * @classdesc Provides methods for managing invoice workflows.
 */
function InvoiceWorkflow() {}
```

## 19.3 Static method

```js
class MathUtil {
  /**
   * Adds two numbers.
   *
   * @static
   * @param {number} a
   * @param {number} b
   * @returns {number}
   */
  static add(a, b) {
    return a + b;
  }
}
```

For modern class syntax, JSDoc can often infer the static nature from the code, so the explicit tag may be unnecessary.

## Document the contract at the right level

For a class, prioritize:

- what an instance represents;
- constructor requirements;
- public properties;
- public methods;
- lifecycle rules;
- errors or side effects that callers need to know.

Do not repeat the same description on the class, constructor, and every method.

### JavaScript class syntax still controls runtime behavior

JSDoc can describe a class relationship, but the runtime inheritance and private-field behavior come from JavaScript syntax such as `extends`, `super`, static members, and `#privateField`.


---

# 20. Inheritance, Interfaces, and Overrides

## 20.1 `@extends` / `@augments`

```js
/**
 * Represents an administrator.
 *
 * @extends User
 */
class Admin extends User {}
```

Modern JavaScript syntax already shows the inheritance, but the tag can help in generated documentation or unusual patterns.

## 20.2 `@implements`

```js
/**
 * @interface
 */
class Serializable {
  serialize() {}
}

/**
 * @implements Serializable
 */
class User {
  serialize() {
    return JSON.stringify(this);
  }
}
```

JavaScript itself does not have runtime interfaces in the same sense as Java or TypeScript. Treat this as documentation/tooling metadata.

## 20.3 `@override`

```js
class Parent {
  /**
   * Prints a message.
   */
  print() {}
}

class Child extends Parent {
  /**
   * Prints the child-specific message.
   *
   * @override
   */
  print() {}
}
```

## 20.4 `@abstract`

```js
/**
 * Base storage provider.
 *
 * @abstract
 */
class StorageProvider {
  /**
   * Saves data.
   *
   * @abstract
   * @param {string} key
   * @param {string} value
   */
  save(key, value) {
    throw new Error("Not implemented.");
  }
}
```

Again, JSDoc describes the contract; JavaScript itself does not automatically enforce abstract classes.

## Keep runtime inheritance separate from documentation relationships

If JavaScript already says:

```js
class AdminService extends UserService {}
```

the runtime relationship comes from `extends`. JSDoc can explain or expose that relationship to documentation tooling, but it does not create inheritance by itself.

Likewise, interface-style tags are documentation/static-analysis concepts in JavaScript projects; they do not make JavaScript enforce an interface at runtime.

### Override documentation

When an override keeps exactly the same contract, avoid duplicating a long parent description unless the tool requires it. Document what changes: stronger constraints, different side effects, different errors, or different semantics.


---

# 21. Access and Visibility Tags

JSDoc supports visibility-related documentation tags.

Common tags:

```text
@public
@private
@protected
@package
@access
```

## 21.1 Private documentation

```js
/**
 * Builds an internal cache key.
 *
 * @private
 * @param {number} id
 * @returns {string}
 */
function buildCacheKey(id) {
  return `user:${id}`;
}
```

## 21.2 Protected method

```js
/**
 * Validates a token before subclasses process it.
 *
 * @protected
 * @param {string} token
 */
function validateToken(token) {}
```

## Important

A JSDoc visibility tag is not necessarily the same as actual JavaScript privacy.

Actual private class fields use `#`:

```js
class Counter {
  #value = 0;
}
```

Documentation metadata and language-level enforcement are separate concepts.

## Documentation visibility vs runtime enforcement

Keep three layers separate:

| Layer | Example | What it affects |
|---|---|---|
| Documentation metadata | `@private` | How tools describe/classify a symbol |
| Static analysis | TypeScript-aware JSDoc visibility | What an editor/checker may allow or warn about |
| JavaScript runtime privacy | `#secret` | What JavaScript itself permits at runtime |

For example, adding `@private` to an ordinary property does not transform it into a JavaScript private field.

Use `#privateField` when runtime language-level privacy is required. Use JSDoc visibility tags when you also need the API documentation or static-analysis layer to communicate intended access.


---

# 22. Modules: ES Modules and CommonJS

## 22.1 ES module

`math.js`:

```js
/**
 * Mathematical helper functions.
 *
 * @module math
 */

/**
 * Adds two numbers.
 *
 * @param {number} a
 * @param {number} b
 * @returns {number}
 */
export function add(a, b) {
  return a + b;
}
```

Import:

```js
import { add } from "./math.js";
```

## 22.2 Default export

```js
/**
 * Application configuration.
 *
 * @module config
 */

const config = {
  timeout: 5000
};

export default config;
```

## 22.3 CommonJS

```js
/**
 * Utility functions.
 *
 * @module utils
 */

/**
 * Converts text to uppercase.
 *
 * @param {string} text
 * @returns {string}
 */
function upper(text) {
  return text.toUpperCase();
}

module.exports = {
  upper
};
```

## 22.4 `@requires`

```js
/**
 * Payment module.
 *
 * @module payment
 * @requires module:httpClient
 */
```

Use relationships like this when they add value to generated API documentation. Do not document every obvious import merely because it exists.

## Let module syntax speak when it can

Modern JavaScript already has module syntax:

```js
export function formatInvoice(invoice) {}
```

or CommonJS:

```js
module.exports = { formatInvoice };
```

Do not add module-related tags merely because they exist. Use tags such as `@module`, `@exports`, or explicit namepaths when generated documentation cannot infer or present the relationship clearly, or when documenting a non-standard structure.

### Generated-doc name vs runtime module

A JSDoc module name is documentation metadata. It does not change:

- the file path;
- Node.js module resolution;
- `import` / `require` behavior;
- package exports.

Treat runtime module configuration and documentation naming as separate concerns.


---

# 23. Namespaces and Namepaths

Namepaths tell JSDoc how symbols relate.

Common separators:

```text
.
#
~
```

A useful mental model:

| Symbol | Typical meaning |
|---|---|
| `.` | static/member of a namespace |
| `#` | instance member |
| `~` | inner member |

Examples:

```text
Utils.formatDate
User#save
Database~ConnectionOptions
```

## 23.1 Namespace

```js
/**
 * Utility functions.
 *
 * @namespace Utils
 */
const Utils = {};
```

## 23.2 Static namespace function

```js
/**
 * Formats a date.
 *
 * @memberof Utils
 * @param {Date} date
 * @returns {string}
 */
Utils.formatDate = function (date) {
  return date.toISOString();
};
```

## 23.3 Module namepath

JSDoc module references commonly use:

```text
module:payments
```

Example:

```js
/**
 * @see module:payments
 */
```

## 23.4 Event namepath

Events may be represented using:

```text
event:ready
```

or scoped under another symbol depending on the design.

## Why namepaths matter

They become important when:

- generated docs contain many symbols;
- code uses old JavaScript patterns;
- a symbol's actual relationship is not obvious from syntax;
- you link between related API members.

Modern ES modules and classes often reduce the need for manual namepath management.

---

# 24. Events, Emitters, and Listeners

JSDoc includes:

```text
@event
@fires
@emits
@listens
```

## Example

```js
/**
 * Fired after an order is successfully created.
 *
 * @event OrderService#orderCreated
 * @type {Object}
 * @property {number} orderId - Created order ID.
 */
```

Method that emits it:

```js
/**
 * Creates an order.
 *
 * @fires OrderService#orderCreated
 * @param {Object} payload
 */
function createOrder(payload) {
  // ...
}
```

Listener:

```js
/**
 * Handles created orders.
 *
 * @listens OrderService#orderCreated
 */
function handleOrderCreated(event) {
  // ...
}
```

This is especially useful in:

- EventEmitter-based Node.js systems;
- plugin architectures;
- UI event systems;
- message-driven applications.

## What these tags do—and do not do

These tags describe an event relationship for documentation. They do **not** register a JavaScript listener or emit an event at runtime.

For example, this documentation:

```js
/**
 * @fires OrderService#orderCreated
 */
```

still requires real event-emission code in the implementation.

`@fires` and `@emits` are used to describe emitted events. `@listens` describes a listener relationship. `@event` creates documentation for the event itself.

### Document the payload contract

An event name alone is rarely enough. Callers usually need to know:

- when the event occurs;
- whether it can occur more than once;
- the payload shape;
- whether delivery is synchronous or asynchronous;
- whether listener failures affect the emitter.

If the payload has a reusable structure, a named `@typedef` can be clearer than repeating a generic `Object`.


---

# 25. Mixins and Advanced Relationships

These tags are less common but useful in framework-heavy or legacy JavaScript.

## 25.1 `@mixin`

```js
/**
 * Logging capabilities.
 *
 * @mixin
 */
const Loggable = {
  log(message) {
    console.log(message);
  }
};
```

## 25.2 `@mixes`

```js
/**
 * Service with logging support.
 *
 * @mixes Loggable
 */
class UserService {}
```

## 25.3 `@borrows`

Documents that one object uses a member from another object.

## 25.4 `@lends`

Useful when properties of an object literal should be documented as members of another symbol.

These are advanced features. Do not force them into ordinary projects.

Prefer code structures that are self-explanatory whenever possible.

## Choosing between the relationship tags

| Tag | Use it to describe |
|---|---|
| `@mixin` | A symbol intended to contribute reusable members |
| `@mixes` | A symbol that receives members from a mixin |
| `@borrows` | A documented member exposed under another name or owner |
| `@lends` | Members of an object literal that should be documented as belonging to another symbol |

These tags are most valuable when the runtime pattern is real but difficult for a documentation generator to infer.

### When not to use them

Do not model ordinary class inheritance as a mixin relationship. Use inheritance tags and normal class syntax for inheritance.

Also avoid elaborate documentation relationships merely to compensate for confusing architecture. If readers need a diagram to understand a simple helper object, simplifying the code may be more valuable than adding more tags.


---

# 26. Documentation Metadata Tags

## 26.1 `@author`

```js
/**
 * @author Development Team
 */
```

For shared codebases, a team name is often more maintainable than individual ownership.

## 26.2 `@version`

```js
/**
 * @version 2.1.0
 */
```

## 26.3 `@since`

```js
/**
 * @since 2.0.0
 */
```

Meaning:

> This API became available in version 2.0.0.

## 26.4 `@deprecated`

```js
/**
 * Retrieves a user.
 *
 * @deprecated Use {@link getUserById} instead.
 */
function getUser(id) {}
```

A good deprecation message says what to use instead.

Poor:

```text
@deprecated Old.
```

Better:

```text
@deprecated Use `getUserById()`; this method will be removed in v4.
```

## 26.5 `@license`

```js
/**
 * @license MIT
 */
```

## 26.6 `@copyright`

```js
/**
 * @copyright 2026 Example Company
 */
```

## 26.7 `@todo`

```js
/**
 * @todo Add retry support for temporary network failures.
 */
```

Do not let JSDoc comments become your primary project-management system. An issue tracker is usually better for work that needs ownership and scheduling.

## Metadata is useful when it changes a reader's decision

Tags such as `@since`, `@deprecated`, `@version`, `@author`, and `@license` are most useful when they answer a practical question.

For example, a deprecation should tell the reader what to use instead:

```js
/**
 * @deprecated Use {@link createUserV2} instead.
 */
```

A bare `@deprecated` warns the reader but leaves them to discover the migration path.

Avoid metadata that is already maintained more reliably elsewhere. For example, duplicating a package version in hundreds of source comments can create stale information.


---

# 27. Less-Common and Advanced JSDoc Tags

The official JSDoc tag set includes many tags that beginners rarely need.

This section explains when they become useful.

## `@alias`

Treat a symbol as having another name.

Useful when code structure and public API names differ.

## `@constructs`

Indicates that a function acts as the constructor for a previously described class.

Mostly relevant to non-standard class factories and older patterns.

## `@exports`

Identifies what a module exports.

Useful especially in some module patterns where automatic detection is difficult.

## `@external` / `@host`

Represents an external class, namespace, or module that your code references but does not define.

## `@file` / `@fileoverview` / `@overview`

Documents a source file.

```js
/**
 * Invoice-calculation utilities.
 *
 * @file
 */
```

## `@function` / `@func` / `@method`

Explicitly declares that a documented symbol is a function.

Normally unnecessary when JSDoc can infer it.

## `@global`

Marks a symbol as global.

Global APIs should generally be minimized in modern modular JavaScript.

## `@hideconstructor`

Hides a constructor from generated documentation.

Useful when consumers should use a factory method.

## `@ignore`

Omits a symbol from generated documentation.

```js
/**
 * @ignore
 */
function temporaryHelper() {}
```

Use carefully. Sometimes undocumented internal code is better represented by visibility rules rather than hiding arbitrary items.

## `@inheritdoc`

Inherit documentation from a parent.

Useful when an overriding method behaves exactly according to the parent contract.

## `@inner`

Marks an inner member.

## `@instance`

Marks an instance member.

## `@kind`

Explicitly describes symbol kind.

Examples may include class, function, member, module, namespace, and others depending on JSDoc.

## `@member` / `@var`

Explicitly documents a member.

## `@memberof`

Associates a symbol with another symbol.

## `@name`

Overrides/informs the documented name.

## `@summary`

Provides a shorter description.

Useful when templates show summaries in lists or navigation.

## `@this`

Documents what `this` refers to.

Particularly helpful in callback-heavy code where lexical context can be confusing.

```js
/**
 * @this UserService
 */
function handler() {
  // this is documented as UserService
}
```

## `@variation`

Distinguishes symbols with the same name.

Rare in ordinary projects.

---

# 28. Inline Tags

Inline tags appear inside text.

## 28.1 `{@link}`

```js
/**
 * Saves the user.
 *
 * See {@link validateUser} before calling this method.
 */
function saveUser(user) {}
```

Custom label:

```js
/**
 * See {@link validateUser|the validation helper}.
 */
```

## 28.2 `{@linkcode}`

Like `{@link}`, but intended to display the linked text as code where supported.

## 28.3 `{@linkplain}`

Link displayed as plain text where supported.

## 28.4 `{@tutorial}`

Links to a configured tutorial.

Inline references are useful because they connect documentation into a navigable API graph.

## Inline-link forms

Useful forms include:

```text
{@link target}
{@link target|custom label}
{@linkcode target}
{@linkplain target}
{@tutorial tutorial-name}
```

Use `{@link ...}` when the target is another documented symbol or URL and a navigable reference helps the reader. Use `{@tutorial ...}` for a tutorial that has been configured as a JSDoc tutorial.

### Common mistake: guessing the target name

Namepaths can become non-obvious for modules, instance members, static members, and namespaces. If a generated link is broken, inspect the generated symbol/namepath rather than repeatedly changing punctuation at random.

Also remember that inline-tag rendering is a documentation-generator feature. An editor may show the raw tag differently from the generated HTML.


---

# 29. JSDoc with VS Code IntelliSense

VS Code already includes powerful JavaScript and TypeScript language features.

For many JSDoc use cases, you do **not** need a special JSDoc extension.

Example:

```js
/**
 * Calculates total price.
 *
 * @param {number} quantity
 * @param {number} unitPrice
 * @returns {number}
 */
function total(quantity, unitPrice) {
  return quantity * unitPrice;
}
```

When another developer types:

```js
total(
```

VS Code can show parameter and documentation information.

## 29.1 Hover information

Hovering over:

```js
total
```

can show:

- function signature;
- description;
- parameter documentation;
- return type.

## 29.2 IntelliSense for typedefs

```js
/**
 * @typedef {Object} Invoice
 * @property {string} number
 * @property {number} total
 */

/** @type {Invoice} */
const invoice = {
  number: "INV-001",
  total: 2500
};
```

When typing:

```js
invoice.
```

VS Code can suggest:

```text
number
total
```

This is one of the strongest reasons to use JSDoc in plain JavaScript.

## What IntelliSense can learn from JSDoc

Depending on the annotation and context, VS Code's JavaScript language service can surface:

- parameter types and descriptions;
- return types;
- custom typedefs;
- overload-like information;
- generic relationships;
- deprecation notices;
- hover documentation;
- completion information.

The important limitation is that editor assistance reflects the types you wrote. A wrong annotation can create a confident but wrong suggestion.

Use `// @ts-check` or project-level `checkJs` when you want the language service to actively report more inconsistencies instead of only displaying documentation.


---

# 30. Type-Checking JavaScript with JSDoc and TypeScript

JSDoc is not only for generated HTML documentation.

TypeScript's language service can use JSDoc annotations to type-check JavaScript.

## 30.1 Per-file checking with `// @ts-check`

```js
// @ts-check

/**
 * @param {number} a
 * @param {number} b
 * @returns {number}
 */
function add(a, b) {
  return a + b;
}

add("10", 20);
```

The last line should produce a type warning/error in TypeScript-aware tooling because `"10"` is a string, not a number.

## 30.2 Disable checking for one file

```js
// @ts-nocheck
```

Use sparingly.

## 30.3 Ignore one line

```js
// @ts-ignore
someLegacyCall();
```

Prefer fixing the type problem or modeling it correctly. Ignoring diagnostics should be a last resort.

## 30.4 Project-wide checking

Create `jsconfig.json`:

```json
{
  "compilerOptions": {
    "checkJs": true,
    "strict": true,
    "noEmit": true
  },
  "include": ["src/**/*.js"]
}
```

Or use `tsconfig.json` in a mixed JS/TS project.

## 30.5 Why `checkJs` matters

Without type checking, this is documentation:

```js
/** @param {number} amount */
function pay(amount) {}
```

With type checking, tools can report incorrect usage:

```js
pay("500");
```

That changes JSDoc from passive documentation into an active development aid.

---

# 31. TypeScript-Specific JSDoc Features

TypeScript recognizes a documented subset/superset of JSDoc syntax in JavaScript files.

Important examples include:

```text
@type
@param
@returns
@typedef
@callback
@template
@satisfies
@import
@public
@private
@protected
@readonly
@override
@extends
@implements
@class
@this
@deprecated
@see
@link
@enum
```

Some tags understood by the JSDoc documentation generator are not necessarily meaningful to TypeScript's type checker.

That is why you must ask:

> Which tool is consuming this comment?

Possible consumers:

- JSDoc HTML generator;
- VS Code;
- TypeScript compiler;
- ESLint;
- documentation templates;
- other static-analysis tools.

## 31.1 `@satisfies`

TypeScript-aware JavaScript can use `@satisfies` to check that a value satisfies a type without necessarily replacing the value's inferred type.

Example:

```js
// @ts-check

/**
 * @typedef {Object} AppConfig
 * @property {"development" | "production"} mode
 * @property {number} timeout
 */

/** @satisfies {AppConfig} */
const config = {
  mode: "development",
  timeout: 5000
};
```

This can catch invalid configuration while retaining useful inference.

## 31.2 `@import`

TypeScript-aware JSDoc can import types for use in JavaScript annotations.

A common alternative is:

```js
/** @typedef {import("./types.js").User} User */
```

or direct inline import types:

```js
/**
 * @param {import("./types.js").User} user
 */
function saveUser(user) {}
```

Choose the form supported by your toolchain and JavaScript module setup.

---

# 32. Generating `.d.ts` Files from JavaScript

A powerful advanced workflow is:

1. write JavaScript;
2. add JSDoc types;
3. let TypeScript analyze the JavaScript;
4. emit declaration (`.d.ts`) files.

Example `tsconfig.json`:

```json
{
  "compilerOptions": {
    "allowJs": true,
    "checkJs": true,
    "declaration": true,
    "emitDeclarationOnly": true,
    "outDir": "types"
  },
  "include": ["src/**/*.js"]
}
```

Then run:

```bash
npx tsc
```

Suppose:

```js
/**
 * Adds two numbers.
 *
 * @param {number} a
 * @param {number} b
 * @returns {number}
 */
export function add(a, b) {
  return a + b;
}
```

A generated declaration may conceptually look like:

```ts
export function add(a: number, b: number): number;
```

## Why this is useful

You can publish a JavaScript library while still providing excellent type information to TypeScript consumers.

## 32.5 What declaration generation actually gives you

Declaration generation asks TypeScript to analyze JavaScript plus its JSDoc types and emit type declarations for consumers. It does not convert the implementation to TypeScript.

A useful checklist is:

```text
JavaScript source
      +
JSDoc types
      +
TypeScript compiler settings
      |
      v
generated .d.ts declarations
```

Before publishing generated declarations:

1. ensure public exports are intentional;
2. inspect the emitted `.d.ts` files;
3. verify package metadata points consumers to the declarations when required;
4. type-test a small consumer project;
5. regenerate declarations in CI so they do not drift from source.

Poor or missing JSDoc on exported JavaScript can lead to declarations that are less precise than expected.


---

# 33. JSDoc Configuration

Instead of putting all options on the command line, create a configuration file.

Example `jsdoc.json`:

```json
{
  "source": {
    "include": ["src"],
    "exclude": ["src/vendor"],
    "includePattern": ".+\\.js$",
    "excludePattern": "(^|\\/|\\\\)_"
  },
  "plugins": [
    "plugins/markdown"
  ],
  "opts": {
    "destination": "docs",
    "recurse": true,
    "readme": "README.md"
  },
  "templates": {
    "cleverLinks": false,
    "monospaceLinks": false
  }
}
```

Run:

```bash
npx jsdoc -c jsdoc.json
```

## 33.1 `source.include`

Paths that should be considered.

```json
{
  "source": {
    "include": ["src"]
  }
}
```

## 33.2 `source.exclude`

Paths to ignore.

```json
{
  "source": {
    "exclude": ["src/generated"]
  }
}
```

## 33.3 `source.includePattern`

Regular expression controlling which filenames are included.

## 33.4 `source.excludePattern`

Regular expression controlling which matching filenames are ignored.

## 33.5 `sourceType`

Common values:

```text
module
script
```

Modern projects normally use `module`.

## 33.6 `plugins`

```json
{
  "plugins": [
    "plugins/markdown"
  ]
}
```

## 33.7 `opts.destination`

```json
{
  "opts": {
    "destination": "./docs"
  }
}
```

## 33.8 `opts.recurse`

```json
{
  "opts": {
    "recurse": true
  }
}
```

## 33.9 `opts.tutorials`

```json
{
  "opts": {
    "tutorials": "./tutorials"
  }
}
```

## Configuration is the reproducible build contract

A configuration file should answer:

```text
What source files are included?
What is excluded?
Which plugins run?
Which template is used?
Where is output written?
Are private symbols included?
Where are tutorials?
```

Keep this file in version control so local builds and CI use the same rules.

### Important distinction

JSDoc configuration controls documentation generation. `jsconfig.json` or `tsconfig.json` controls the TypeScript language service/compiler behavior for JavaScript type checking. They solve different problems even though both may consume JSDoc comments.


---

# 34. Important JSDoc CLI Options

Common commands:

## Help

```bash
npx jsdoc --help
```

## Version

```bash
npx jsdoc --version
```

## Configuration

```bash
npx jsdoc -c jsdoc.json
```

Equivalent long form:

```bash
npx jsdoc --configure jsdoc.json
```

## Destination

```bash
npx jsdoc src -r -d docs
```

## Recursive scan

```bash
npx jsdoc src -r
```

## README

```bash
npx jsdoc src -r -R README.md
```

## Tutorials

```bash
npx jsdoc src -r -u tutorials
```

## Include private symbols

```bash
npx jsdoc src -r --private
```

Be careful before publishing private/internal APIs publicly.

## 34.1 Quick option reference

| Purpose | Short form | Long form | Typical value |
|---|---|---|---|
| Configuration file | `-c` | `--configure` | `jsdoc.json` |
| Output directory | `-d` | `--destination` | `docs` |
| Recurse into subdirectories | `-r` | `--recurse` | no value |
| README | `-R` | `--readme` | `README.md` |
| Tutorials directory | `-u` | `--tutorials` | `tutorials` |
| Template | `-t` | `--template` | template path |
| Include private symbols | `-p` | `--private` | no value |
| Help | `-h` | `--help` | no value |
| Version | `-v` | `--version` | no value |

A CLI option changes how JSDoc processes input or writes output. It does not change JavaScript runtime behavior.

### Prefer a checked-in configuration for repeatable builds

This:

```bash
npx jsdoc -c jsdoc.json
```

is generally easier to maintain than a long command copied into documentation, because source paths, plugins, templates, and output settings can live in one version-controlled file.


---

# 35. README, Package Metadata, and Tutorials

API reference is only one part of good documentation.

A strong library normally needs:

- introduction;
- installation;
- quick start;
- API reference;
- examples;
- migration notes;
- conceptual tutorials;
- troubleshooting.

## 35.1 README

A README is useful as the documentation landing page.

Example command:

```bash
npx jsdoc src -r -R README.md
```

## 35.2 `package.json`

JSDoc can incorporate package information such as project name and version.

## 35.3 Tutorials

Tutorial files let you add concept-oriented documentation beside generated API pages.

Use tutorials for topics such as:

```text
Authentication flow
Plugin development
Database setup
Migration guide
Advanced configuration
```

Avoid putting a complete tutorial into every function comment.

API reference and tutorials serve different purposes.

## Which documentation belongs where?

| Place | Best for |
|---|---|
| README | Project purpose, installation, quick start, high-level examples |
| Generated API pages | Functions, classes, parameters, return values, symbols |
| Tutorials | Multi-step workflows and conceptual guides |
| `package.json` metadata | Machine-readable package information and entry points |

Avoid making a generated API page carry the entire onboarding story. A new user usually needs the README first, then tutorials, then detailed API reference.


---

# 36. Markdown Inside JSDoc

JSDoc includes a Markdown plugin.

Configuration:

```json
{
  "plugins": ["plugins/markdown"]
}
```

Then descriptions can contain Markdown more naturally.

Example:

```js
/**
 * Loads a configuration.
 *
 * **Important:** The file must contain valid JSON.
 *
 * Steps:
 *
 * 1. Read the file.
 * 2. Parse JSON.
 * 3. Validate settings.
 *
 * @param {string} path - Configuration path.
 */
function loadConfig(path) {}
```

Do not over-format comments. Source code still needs to remain readable.

## What the Markdown plugin changes

The Markdown plugin processes Markdown in selected JSDoc text such as descriptions so the generated documentation can render emphasis, lists, code, and related formatting more naturally.

It does not turn the JavaScript file into a Markdown file, and it does not change the JavaScript runtime.

### When to use it

Use Markdown inside JSDoc when formatting genuinely improves comprehension:

- short lists of constraints;
- emphasis for warnings;
- concise inline code;
- links;
- short procedural steps.

Move long tutorials out of source comments and into dedicated tutorial or documentation files. Very large comment blocks make implementation files harder to scan.


---

# 37. JSDoc Plugins

JSDoc plugins can hook into the parsing and documentation-generation process.

Possible uses include:

- custom tag handling;
- preprocessing source;
- modifying doclets;
- adding Markdown support;
- producing summaries;
- enforcing project-specific behavior.

Example configuration:

```json
{
  "plugins": [
    "plugins/markdown"
  ]
}
```

## When to create a custom plugin

Consider a custom plugin only when:

- your framework has custom syntax;
- documentation must understand project-specific metadata;
- ordinary JSDoc tags are insufficient;
- the behavior will be reused across many files.

Do not create a plugin simply to avoid writing clear documentation.

## How a plugin participates in JSDoc

A plugin can participate at different points in the documentation pipeline, for example by:

- defining event handlers for parser/doclet lifecycle events;
- defining custom tags;
- visiting syntax-tree nodes;
- transforming or augmenting generated documentation data.

Conceptually:

```text
source code
   ↓
JSDoc parsing
   ↓
plugin hooks / transformations
   ↓
doclets
   ↓
template
   ↓
generated documentation
```

Because plugins can affect interpretation, keep the plugin list version-controlled and test documentation generation in CI. A plugin that silently stops working can change documentation even when source comments are unchanged.


---

# 38. Templates and Custom Documentation Sites

JSDoc separates parsed documentation data from presentation through templates.

The default template generates HTML.

A custom or third-party template may provide:

- different navigation;
- search;
- different styling;
- dark mode;
- improved mobile layout;
- custom branding.

## Important rule

A template changes presentation, not the correctness of your source comments.

First make the documentation semantically correct.

Then improve appearance.

## Default-template features

JSDoc's default template can be configured to change behavior such as:

- whether source files are displayed;
- static file inclusion;
- date display;
- long names in navigation;
- custom layout files.

Use these only after establishing a stable documentation workflow.

## Template selection

A template is selected through configuration or the CLI. For example:

```bash
npx jsdoc src -r -t path/to/template
```

or through the `opts.template` configuration setting.

Before adopting a third-party template, check:

- compatibility with your JSDoc version;
- maintenance status;
- accessibility;
- behavior for large APIs;
- whether custom plugins/tags render correctly;
- whether generated assets work in your deployment target.

A visually attractive template cannot repair missing parameter descriptions, incorrect types, or stale examples.


---

# 39. Linting JSDoc with ESLint

Documentation can become incorrect just like code.

A JSDoc linter can catch problems such as:

- missing parameter documentation;
- parameter names that do not match code;
- invalid tag syntax;
- missing descriptions;
- malformed types;
- duplicate tags.

A widely used package is:

```bash
npm install --save-dev eslint eslint-plugin-jsdoc
```

Exact ESLint configuration depends on the versions and configuration style used by your project.

## Why lint comments?

Suppose:

```js
/**
 * @param {string} username
 */
function login(email) {}
```

The documentation says `username`, but the actual parameter is `email`.

A linter can help detect this kind of drift.

## Recommended philosophy

Use lint rules to improve correctness, not to create needless comment bureaucracy.

A small function named:

```js
function isEmpty(value) {}
```

does not always need a paragraph of obvious prose.

## Treat lint rules as version-sensitive configuration

`eslint-plugin-jsdoc` and ESLint configuration formats evolve. Do not copy an old configuration block from a blog and assume every rule name or preset still exists.

A safer workflow is:

1. install the versions your project will use;
2. read the plugin's documentation for those versions;
3. start with a small rule set;
4. run linting on existing files;
5. increase strictness gradually.

Useful rule categories include checking that parameter names match the function signature, descriptions are present where required, and type syntax is valid for the chosen mode.


---

# 40. Real-World Patterns

This section combines multiple JSDoc concepts.

## 40.1 API response

```js
/**
 * @typedef {Object} ApiError
 * @property {string} code - Machine-readable error code.
 * @property {string} message - Human-readable error message.
 */

/**
 * @template T
 * @typedef {Object} ApiResponse
 * @property {boolean} success
 * @property {T} [data]
 * @property {ApiError} [error]
 */
```

Usage:

```js
/**
 * Retrieves a customer.
 *
 * @param {number} id
 * @returns {Promise<ApiResponse<Customer>>}
 */
async function getCustomer(id) {}
```

Note: generic typedef rendering/interpretation may differ between tools. Test this pattern with your specific TypeScript/JSDoc setup.

## 40.2 Pagination

```js
/**
 * @typedef {Object} Pagination
 * @property {number} page - Current page number, starting at 1.
 * @property {number} pageSize - Number of records per page.
 * @property {number} totalItems - Total number of matching records.
 * @property {number} totalPages - Total available pages.
 */
```

## 40.3 Query options

```js
/**
 * @typedef {Object} UserQuery
 * @property {string} [search] - Search text.
 * @property {"active" | "inactive"} [status] - Optional status filter.
 * @property {number} [page=1] - Page number.
 * @property {number} [pageSize=20] - Records per page.
 */
```

## 40.4 Service method

```js
/**
 * Searches users.
 *
 * @param {UserQuery} query - Search filters.
 * @returns {Promise<User[]>} Matching users.
 * @throws {RangeError} If `page` or `pageSize` is less than 1.
 *
 * @example
 * const users = await searchUsers({
 *   search: "asha",
 *   status: "active",
 *   page: 1,
 *   pageSize: 20
 * });
 */
async function searchUsers(query) {}
```

This is much more useful than merely writing:

```js
// Search users
```

## Prefer reusable named domain types

In production code, repeated inline object shapes become difficult to keep consistent.

If several functions accept the same invoice structure, define it once:

```js
/**
 * @typedef {Object} Invoice
 * @property {string} id
 * @property {number} total
 * @property {string} currency
 */
```

Then reuse `Invoice` in parameters, returns, callbacks, and collections.

This improves both documentation and editor consistency, and it gives reviewers one place to inspect the domain contract.


---

# 41. Frontend, React, Node.js, and Express Examples

## 41.1 Browser DOM helper

```js
/**
 * Finds an element or throws a descriptive error.
 *
 * @param {string} selector - CSS selector.
 * @param {ParentNode} [root=document] - Node in which to search.
 * @returns {Element} Matching element.
 * @throws {Error} If no matching element exists.
 */
function requireElement(selector, root = document) {
  const element = root.querySelector(selector);

  if (!element) {
    throw new Error(`Element not found: ${selector}`);
  }

  return element;
}
```

## 41.2 Event handler

```js
/**
 * Handles the save-button click.
 *
 * @param {MouseEvent} event
 */
function handleSaveClick(event) {
  event.preventDefault();
}
```

## 41.3 React component props in JavaScript

```js
/**
 * @typedef {Object} UserCardProps
 * @property {string} name
 * @property {string} email
 * @property {() => void} onSelect
 */

/**
 * Displays a user card.
 *
 * @param {UserCardProps} props
 */
function UserCard({ name, email, onSelect }) {
  return (
    <button onClick={onSelect}>
      {name} - {email}
    </button>
  );
}
```

In modern React projects, your exact documentation strategy may differ depending on whether you use JavaScript, TypeScript, PropTypes, generated component docs, or a component explorer.

## 41.4 Express-style controller

If your project has the Express type definitions available, you can import types in JSDoc:

```js
/**
 * Creates a user.
 *
 * @param {import("express").Request} req
 * @param {import("express").Response} res
 * @param {import("express").NextFunction} next
 */
async function createUser(req, res, next) {
  try {
    // ...
  } catch (error) {
    next(error);
  }
}
```

This gives excellent IntelliSense without converting the file to TypeScript.

## 41.5 Node.js filesystem helper

```js
/**
 * Reads and parses a UTF-8 JSON file.
 *
 * @param {string} filePath
 * @returns {Promise<unknown>} Parsed JSON value.
 * @throws {SyntaxError} If the file does not contain valid JSON.
 */
async function readJson(filePath) {
  // ...
}
```

Returning `unknown` is often more correct than pretending unvalidated JSON has a known structure.

## Framework examples need two layers of documentation

A framework can tell you *how* a function is called, while your JSDoc should explain the application's contract.

For example, documenting an Express handler only as `req`, `res`, and `next` adds little value if their framework types are already known. More useful documentation explains:

- required route parameters;
- expected request body fields;
- authentication assumptions;
- response shape/status behavior;
- important errors.

Similarly, React component documentation is most valuable when it explains prop meaning, defaults, controlled/uncontrolled behavior, and side effects rather than restating JSX syntax.


---

# 42. Testing and Maintaining Documentation

Documentation quality decays when code changes.

Treat important documentation as maintainable engineering work.

## 42.1 Review documentation during code review

When a function signature changes from:

```js
function send(to, subject) {}
```

to:

```js
function send(to, subject, priority) {}
```

check whether JSDoc also changed.

## 42.2 Lint documentation

Use tools such as `eslint-plugin-jsdoc`.

## 42.3 Test examples where practical

Important code examples can sometimes be extracted into tests or duplicated as tested examples.

The goal is to reduce stale documentation.

## 42.4 Generate docs in CI

A CI pipeline can run:

```bash
npm run docs
```

This verifies that documentation generation does not break.

For stricter projects, you may also publish generated docs automatically.

## 42.5 Do not document implementation that changes frequently

Bad:

```js
/**
 * Uses a for-loop with index `i` to scan the array.
 */
```

Better:

```js
/**
 * Returns the first active user.
 */
```

The second description remains true even if implementation changes from a loop to `.find()`.

---

# 43. Common Mistakes

## Mistake 1: Writing `/*` instead of `/**`

Wrong:

```js
/*
 * @param {string} name
 */
```

Correct:

```js
/**
 * @param {string} name
 */
```

## Mistake 2: Parameter name mismatch

Wrong:

```js
/**
 * @param {string} username
 */
function login(email) {}
```

Correct:

```js
/**
 * @param {string} email
 */
function login(email) {}
```

## Mistake 3: Documenting obvious syntax instead of meaning

Weak:

```js
/**
 * Sets amount.
 * @param {number} amount - Amount.
 */
```

Better:

```js
/**
 * Sets the invoice amount before tax.
 *
 * @param {number} amount - Amount in INR, excluding tax.
 */
```

## Mistake 4: Incorrect return type

```js
/**
 * @returns {User}
 */
async function getUser() {}
```

An `async` function returns a promise.

Better:

```js
/**
 * @returns {Promise<User>}
 */
async function getUser() {}
```

## Mistake 5: Using `Object` everywhere

Weak:

```js
/**
 * @param {Object} user
 */
```

Better:

```js
/**
 * @typedef {Object} User
 * @property {number} id
 * @property {string} name
 */

/**
 * @param {User} user
 */
```

## Mistake 6: Overusing `any`/`*`

```js
/**
 * @param {*} data
 */
```

If the structure is known, document it.

## Mistake 7: Treating JSDoc as runtime validation

This:

```js
/**
 * @param {number} age
 */
function setAge(age) {}
```

does not prevent:

```js
setAge("abc");
```

unless another tool catches it or your runtime code validates it.

JSDoc does not replace runtime validation for untrusted data.

## Mistake 8: Duplicating TypeScript declarations unnecessarily

TypeScript:

```ts
function add(a: number, b: number): number {}
```

Poor redundant comment:

```ts
/**
 * @param {number} a
 * @param {number} b
 * @returns {number}
 */
```

The types are already in the language.

In TypeScript, use comments to explain meaning:

```ts
/**
 * Calculates the amount payable after applying the configured discount policy.
 */
```

## Mistake 9: Writing documentation that is longer than the code but adds no information

Good documentation is not measured by line count.

## Mistake 10: Stale deprecation information

If you write:

```text
@deprecated Use newMethod().
```

make sure `newMethod()` actually exists and remains the recommended replacement.

---

# 44. Best Practices

## 44.1 Explain "why" and contract

Prefer:

```text
Returns `undefined` when the user is not present.
```

over:

```text
Returns a user.
```

## 44.2 Document units

```text
milliseconds
seconds
bytes
MB
percentage
decimal rate
pixels
degrees
currency
```

## 44.3 Document formats

Example:

```text
ISO 8601
YYYY-MM-DD
UUID
email address
absolute URL
```

## 44.4 Use named typedefs for business entities

Examples:

```text
Invoice
Customer
Payment
User
Pagination
SearchFilter
ApiResponse
```

## 44.5 Document edge cases

```text
Returns an empty array when no records match.
```

## 44.6 Document side effects

```js
/**
 * Saves the token to `localStorage`.
 *
 * @param {string} token
 */
function storeToken(token) {}
```

## 44.7 Document mutation

```js
/**
 * Sorts the provided array in place.
 *
 * @param {number[]} values - Array that will be mutated.
 * @returns {number[]} The same array instance after sorting.
 */
function sortInPlace(values) {
  return values.sort((a, b) => a - b);
}
```

This is important because callers may assume an input remains unchanged.

## 44.8 Prefer examples for non-obvious APIs

If a developer is likely to ask:

> "How exactly do I call this?"

add `@example`.

## 44.9 Prefer precise types

Better:

```text
"pending" | "approved" | "rejected"
```

than:

```text
string
```

when only those values are valid.

## 44.10 Keep documentation close to code

JSDoc works well because the contract lives beside the implementation.

---

# 45. When Not to Use JSDoc

JSDoc is useful, but not every line needs it.

## Do not document trivial implementation details

This:

```js
const counter = 0;
```

usually does not need:

```js
/**
 * Counter variable.
 * @type {number}
 */
const counter = 0;
```

unless it is a meaningful public API or the type is not obvious.

## Do not use JSDoc as a substitute for naming

Bad:

```js
/**
 * User email.
 */
const x = ...
```

Better code:

```js
const userEmail = ...
```

## Do not use documentation instead of runtime validation

If data comes from:

- HTTP requests;
- forms;
- databases;
- files;
- external APIs;

validate it at runtime.

## Do not duplicate native type information endlessly in TypeScript

In TypeScript, comments should normally explain behavior, constraints, business rules, and examples rather than repeating visible types.

## A simple decision test

Before adding a block, ask:

1. **Will this tell the caller something the code cannot express clearly?**
2. **Will a tool consume the information?**
3. **Is the contract likely to remain stable enough to maintain the comment?**

If all three answers are “no,” a JSDoc block may add maintenance cost without helping anyone.

For example, this usually adds little value:

```js
/**
 * Increments count.
 * @param {number} count - Count.
 * @returns {number} Count.
 */
function increment(count) {
  return count + 1;
}
```

A business rule deserves more explanation:

```js
/**
 * Returns the next invoice sequence number for the current financial year.
 *
 * Sequence numbers restart when the configured financial year changes.
 *
 * @param {number} current - Current sequence number.
 * @returns {number} Next sequence number.
 */
function nextInvoiceSequence(current) {
  return current + 1;
}
```

Document **meaning, constraints, and contracts**, not obvious syntax.


---

# 46. JSDoc Tag Quick Reference

The following table groups important JSDoc tags.

| Tag | Purpose |
|---|---|
| `@abstract` / `@virtual` | Marks something that should be implemented/overridden |
| `@access` | Specifies access level |
| `@alias` | Treats a symbol as another name |
| `@async` | Marks an async function |
| `@augments` / `@extends` | Documents inheritance |
| `@author` | Identifies author |
| `@borrows` | Documents borrowing from another object |
| `@callback` | Defines a callback type |
| `@class` / `@constructor` | Documents a constructor/class pattern |
| `@classdesc` | Provides class description |
| `@constant` / `@const` | Documents a constant |
| `@constructs` | Associates a function with construction |
| `@copyright` | Copyright information |
| `@default` / `@defaultvalue` | Default value |
| `@deprecated` | Marks API as deprecated |
| `@description` / `@desc` | Description |
| `@enum` | Documents a collection of related values |
| `@event` | Documents an event |
| `@example` | Usage example |
| `@exports` | Documents module export |
| `@external` / `@host` | External symbol |
| `@file` / `@fileoverview` / `@overview` | File description |
| `@fires` / `@emits` | Events emitted by a symbol |
| `@function` / `@func` / `@method` | Explicitly marks a function |
| `@generator` | Marks generator function |
| `@global` | Marks global symbol |
| `@hideconstructor` | Hides constructor in docs |
| `@ignore` | Omits symbol |
| `@implements` | Documents interface implementation |
| `@inheritdoc` | Inherits parent documentation |
| `@inner` | Inner member |
| `@instance` | Instance member |
| `@interface` | Documents an interface |
| `@kind` | Explicit symbol kind |
| `@lends` | Treats object-literal members as belonging elsewhere |
| `@license` | License information |
| `@listens` | Events a symbol listens to |
| `@member` / `@var` | Documents a member |
| `@memberof` | Assigns parent symbol |
| `@mixes` | Documents applied mixin |
| `@mixin` | Defines a mixin |
| `@module` | Documents a module |
| `@name` | Explicit documented name |
| `@namespace` | Documents namespace |
| `@override` | Marks overridden member |
| `@package` | Package-private visibility |
| `@param` / `@arg` / `@argument` | Function parameter |
| `@private` | Private API |
| `@property` / `@prop` | Object property |
| `@protected` | Protected API |
| `@public` | Public API |
| `@readonly` | Read-only intent |
| `@requires` | Module dependency |
| `@returns` / `@return` | Return value |
| `@see` | Related symbol/resource |
| `@since` | Version where API was introduced |
| `@static` | Static member |
| `@summary` | Short description |
| `@this` | Documents `this` type/context |
| `@throws` / `@exception` | Possible exception |
| `@todo` | Future work |
| `@tutorial` | Tutorial reference |
| `@type` | Value type |
| `@typedef` | Reusable custom type |
| `@variation` | Distinguishes same-named symbols |
| `@version` | Version information |
| `@yields` / `@yield` | Generator yield type/value |
| `{@link ...}` | Inline link |
| `{@linkcode ...}` | Inline code-styled link |
| `{@linkplain ...}` | Inline plain-text link |

### Tool-specific tags

TypeScript's JavaScript type checker also understands some JSDoc-like tags/conventions such as:

```text
@template
@satisfies
@import
```

These are particularly relevant when JSDoc comments are being used for type checking, not just HTML generation.

---

# 47. JSDoc in Other Languages: What to Use Instead

JSDoc is primarily for JavaScript.

Do not assume that PHP, Java, Python, C#, Go, or Rust should use JSDoc itself.

They have their own documentation conventions and tools.

## 47.1 Concept comparison

| Language | Common documentation system |
|---|---|
| JavaScript | JSDoc |
| TypeScript | TSDoc-style comments / JSDoc documentation tags |
| PHP | PHPDoc + phpDocumentor |
| Java | Javadoc |
| Python | Docstrings + pydoc/Sphinx and conventions such as Google/NumPy/reStructuredText styles |
| C# | XML documentation comments |
| Kotlin | KDoc |
| Ruby | YARD/RDoc |
| Rust | Rustdoc |
| Go | Go documentation comments + `go doc` / pkgsite |

The philosophy is similar:

> Put structured documentation close to the code so tools and developers can use it.

---

## 47.2 Same function in JavaScript with JSDoc

```js
/**
 * Adds two numbers.
 *
 * @param {number} a - First number.
 * @param {number} b - Second number.
 * @returns {number} Sum of the numbers.
 */
function add(a, b) {
  return a + b;
}
```

---

## 47.3 PHP: PHPDoc

PHP commonly uses DocBlocks.

```php
/**
 * Adds two numbers.
 *
 * @param int $a First number.
 * @param int $b Second number.
 *
 * @return int Sum of the numbers.
 */
function add(int $a, int $b): int
{
    return $a + $b;
}
```

Typical ecosystem:

```text
PHPDoc
phpDocumentor
PHPStan
Psalm
IDE language servers
```

### Why PHPDoc still matters when PHP has native types

Native PHP types describe machine-checkable types:

```php
function add(int $a, int $b): int
```

PHPDoc can still explain:

- meaning;
- array shapes;
- generics used by static analyzers;
- business rules;
- deprecations;
- examples;
- thrown exceptions.

Example:

```php
/**
 * Finds an invoice.
 *
 * @param int $invoiceId Database identifier.
 *
 * @return Invoice|null Invoice when found, otherwise null.
 *
 * @throws RuntimeException When the database is unavailable.
 */
function findInvoice(int $invoiceId): ?Invoice
{
    // ...
}
```

For PHP API documentation generation, investigate **phpDocumentor**.

---

## 47.4 Java: Javadoc

Java uses Javadoc-style comments.

```java
/**
 * Adds two numbers.
 *
 * @param a first number
 * @param b second number
 * @return sum of the numbers
 */
public int add(int a, int b) {
    return a + b;
}
```

Common Javadoc tags include:

```text
@param
@return
@throws
@see
@since
@deprecated
@author
@version
```

Example with exception:

```java
/**
 * Divides two numbers.
 *
 * @param numerator numerator
 * @param denominator denominator
 * @return division result
 * @throws IllegalArgumentException if denominator is zero
 */
public double divide(double numerator, double denominator) {
    if (denominator == 0) {
        throw new IllegalArgumentException("Denominator cannot be zero");
    }

    return numerator / denominator;
}
```

Generate documentation with the JDK `javadoc` tool.

Modern Javadoc also supports richer documentation features, and newer JDKs support Markdown-style documentation comments in addition to traditional forms.

---

## 47.5 Python: Docstrings

Python normally uses docstrings rather than `/** ... */`.

Basic:

```python
def add(a: int, b: int) -> int:
    """Add two numbers and return their sum."""
    return a + b
```

More descriptive:

```python
def divide(numerator: float, denominator: float) -> float:
    """
    Divide one number by another.

    Args:
        numerator: Value to divide.
        denominator: Value to divide by.

    Returns:
        Division result.

    Raises:
        ValueError: If denominator is zero.
    """
    if denominator == 0:
        raise ValueError("Denominator cannot be zero")

    return numerator / denominator
```

Popular docstring styles include:

- Google style;
- NumPy style;
- reStructuredText/Sphinx style.

Python's built-in `pydoc` reads docstrings.

For larger documentation sites, Sphinx and MkDocs-based toolchains are common choices.

---

## 47.6 TypeScript

TypeScript has native type annotations, so avoid repeating them unnecessarily.

```ts
/**
 * Returns the invoice total after applying the discount.
 *
 * @param subtotal - Amount before discount.
 * @param discount - Discount to subtract.
 * @returns Final invoice total.
 */
function calculateTotal(
  subtotal: number,
  discount: number
): number {
  return subtotal - discount;
}
```

Notice that the comment does not repeat:

```text
{number}
```

because TypeScript already knows the types.

The best TypeScript documentation explains meaning.

---

## 47.7 C#: XML documentation comments

```csharp
/// <summary>
/// Adds two numbers.
/// </summary>
/// <param name="a">First number.</param>
/// <param name="b">Second number.</param>
/// <returns>Sum of the numbers.</returns>
public int Add(int a, int b)
{
    return a + b;
}
```

Common tags include:

```xml
<summary>
<param>
<returns>
<exception>
<remarks>
<example>
<see>
```

---

## 47.8 Kotlin: KDoc

```kotlin
/**
 * Adds two numbers.
 *
 * @param a first number
 * @param b second number
 * @return sum of the numbers
 */
fun add(a: Int, b: Int): Int {
    return a + b
}
```

---

## 47.9 Rust: Rustdoc

Rust documentation commonly uses `///`.

```rust
/// Adds two numbers.
///
/// # Examples
///
/// ```
/// let result = add(2, 3);
/// assert_eq!(result, 5);
/// ```
fn add(a: i32, b: i32) -> i32 {
    a + b
}
```

Rust's documentation tooling is tightly integrated with the language ecosystem.

---

## 47.10 Go

Go documentation favors natural comments starting with the exported symbol's name.

```go
// Add returns the sum of a and b.
func Add(a int, b int) int {
    return a + b
}
```

Go usually avoids tag-heavy documentation in ordinary code.

---

## 47.11 The transferable skill

Do not memorize only tag names.

Learn the documentation questions:

1. What does this API do?
2. Why would someone use it?
3. What inputs does it accept?
4. What values and formats are valid?
5. What does it return?
6. What errors can occur?
7. What side effects happen?
8. What are the important edge cases?
9. Is it deprecated?
10. What should callers use instead?
11. Can one concise example make usage obvious?

Those questions transfer to every language.

---

# 48. VS Code Extension Recommendations

## First recommendation: use VS Code's built-in JavaScript/TypeScript support

VS Code already understands a large amount of JSDoc.

Before installing anything, test:

```js
// @ts-check

/**
 * @typedef {Object} User
 * @property {number} id
 * @property {string} name
 */

/**
 * @param {User} user
 */
function printUser(user) {
  console.log(user.name);
}
```

You should already get useful IntelliSense and diagnostics.

## 48.1 JSDoc Generator

Marketplace extension:

```text
JSDoc Generator
Publisher: Crystal Spider
Extension ID: crystal-spider.jsdoc-generator
```

Useful when you want:

- automatic comment skeleton generation;
- parameters detected from functions;
- return tags generated;
- JavaScript/TypeScript/React support;
- customizable generated tags.

Use generated comments as a starting point. Do not accept empty or meaningless descriptions blindly.

## 48.2 ESLint

Marketplace extension:

```text
ESLint
Publisher: Microsoft
Extension ID: dbaeumer.vscode-eslint
```

Recommended when your project uses ESLint.

Combine it with the npm package:

```bash
npm install --save-dev eslint-plugin-jsdoc
```

This is often more valuable for long-term quality than a comment generator because it helps detect documentation drift.

## 48.3 Inline JSDoc Hints

An optional extension can surface JSDoc summaries more visibly in completions.

Useful if your team relies heavily on rich symbol documentation.

Do not install it simply because it exists; first see whether VS Code's built-in hover and completion UI already meets your needs.

## 48.4 Prettier

Prettier is not a JSDoc documentation generator, but it is useful for overall code consistency.

Marketplace extension:

```text
Prettier - Code formatter
Extension ID: esbenp.prettier-vscode
```

Use project-local formatting configuration so that the entire team gets consistent behavior.

## 48.5 Suggested extension priority

For a normal JavaScript project:

1. VS Code built-in JS/TS language features;
2. ESLint extension;
3. `eslint-plugin-jsdoc` npm package;
4. JSDoc Generator if you want automatic comment skeletons;
5. optional JSDoc display/folding helpers only if they solve a real workflow problem.

Avoid installing many overlapping documentation generators.

---

# 49. Suggested Project Setups

## 49.1 Beginner JavaScript project

Install:

```bash
npm install --save-dev jsdoc
```

`package.json`:

```json
{
  "scripts": {
    "docs": "jsdoc src -r -d docs"
  }
}
```

Use basic tags:

```text
@param
@returns
@throws
@example
@typedef
@property
```

This is enough to learn the foundation.

---

## 49.2 JavaScript project with type checking

`jsconfig.json`:

```json
{
  "compilerOptions": {
    "checkJs": true,
    "strict": true,
    "noEmit": true
  },
  "include": ["src/**/*.js"]
}
```

Then use:

```text
@type
@param
@returns
@typedef
@callback
@template
```

This gives you much of the editor safety people associate with TypeScript while remaining in `.js`.

---

## 49.3 Library project

Recommended goals:

- public API documented;
- typedefs for public data structures;
- examples for non-obvious methods;
- generated HTML docs;
- README as landing page;
- documentation linting;
- CI documentation build;
- `.d.ts` generation if TypeScript consumers need types.

Example scripts:

```json
{
  "scripts": {
    "docs": "jsdoc -c jsdoc.json",
    "typecheck": "tsc --noEmit",
    "lint": "eslint ."
  }
}
```

---

## 49.4 Large application

Do not document every internal helper.

Prioritize:

- service boundaries;
- reusable utilities;
- public modules;
- complex data structures;
- integration points;
- business rules;
- non-obvious error behavior;
- framework hooks;
- event contracts.

A 20-line private helper with excellent names may need no JSDoc.

A 5-line function implementing a critical financial rule may deserve extensive documentation.

Complexity is not measured only by line count.

---

# 50. Practice Exercises

Try these in order.

## Exercise 1: Basic function

Write JSDoc for:

```js
function multiply(a, b) {
  return a * b;
}
```

Include:

- description;
- two params;
- return type;
- example.

## Exercise 2: Optional parameter

Document:

```js
function greet(name = "Guest") {
  return `Hello ${name}`;
}
```

## Exercise 3: Typedef

Create a `Product` type with:

```text
id
name
price
category
active
```

Make `category` optional.

## Exercise 4: Async function

Document:

```js
async function getProduct(id) {
  // ...
}
```

Return:

```text
Promise<Product>
```

## Exercise 5: Error handling

Document a divide function that throws when denominator is zero.

## Exercise 6: Callback

Create:

```text
PaymentCompleteHandler
```

with:

```text
transactionId
success
```

## Exercise 7: Generic helper

Write a generic `last()` function using `@template`.

## Exercise 8: Type-check JavaScript

Enable:

```js
// @ts-check
```

and intentionally pass the wrong type to a function.

Observe VS Code's error.

## Exercise 9: Generate docs

Install JSDoc and run:

```bash
npx jsdoc src -r -d docs
```

Explore the generated site.

## Exercise 10: Real project

Choose one existing module and document only its public API.

Then ask:

- Is the contract understandable without reading implementation?
- Do examples match actual behavior?
- Are nullable/optional values clear?
- Are errors documented?
- Are units and formats clear?

---

# 51. Final Learning Roadmap

Follow this order.

## Level 1 — Foundation

Learn:

```text
/**
 * ...
 */
@param
@returns
@type
@example
@throws
```

Goal:

> Clearly document ordinary functions.

## Level 2 — Data modeling

Learn:

```text
@typedef
@property
@callback
optional parameters
union types
arrays
object shapes
```

Goal:

> Model real application data.

## Level 3 — Modern JavaScript

Learn:

```text
Promise<T>
async functions
classes
ES modules
destructuring
rest parameters
```

Goal:

> Document production JavaScript.

## Level 4 — Editor type safety

Learn:

```text
// @ts-check
checkJs
strict
@template
import() types
@satisfies
```

Goal:

> Get TypeScript-powered checking while writing JavaScript.

## Level 5 — Documentation generation

Learn:

```text
jsdoc CLI
jsdoc.json
README integration
Markdown plugin
tutorials
templates
```

Goal:

> Build a browsable API documentation site.

## Level 6 — Team quality

Learn:

```text
ESLint
eslint-plugin-jsdoc
CI documentation builds
review rules
deprecation policies
example testing
```

Goal:

> Keep documentation correct as the codebase evolves.

## Level 7 — Cross-language documentation

Understand the equivalent idea in:

```text
PHPDoc
Javadoc
Python docstrings
C# XML docs
KDoc
Rustdoc
Go docs
```

Goal:

> Transfer documentation skills between technologies.

---

# 52. Official References

The following sources are recommended for checking current syntax and tool behavior.

## JSDoc

- Official documentation: https://jsdoc.app/
- Getting started: https://jsdoc.app/about-getting-started
- JSDoc tags index: https://jsdoc.app/
- `@param`: https://jsdoc.app/tags-param
- `@returns`: https://jsdoc.app/tags-returns
- `@type`: https://jsdoc.app/tags-type
- `@typedef`: https://jsdoc.app/tags-typedef
- `@callback`: https://jsdoc.app/tags-callback
- Configuration: https://jsdoc.app/about-configuring-jsdoc
- CLI options: https://jsdoc.app/about-commandline
- Markdown plugin: https://jsdoc.app/plugins-markdown

## TypeScript + JSDoc

- JSDoc reference: https://www.typescriptlang.org/docs/handbook/jsdoc-supported-types.html
- Compiler options: https://www.typescriptlang.org/docs/handbook/compiler-options.html

## PHP

- phpDocumentor: https://docs.phpdoc.org/
- PHPDoc reference: https://docs.phpdoc.org/guide/references/phpdoc/

## Java

- Oracle Javadoc documentation: https://docs.oracle.com/en/java/javase/

## Python

- `pydoc`: https://docs.python.org/3/library/pydoc.html
- Python documentation-string guidance: https://docs.python.org/3/tutorial/controlflow.html#documentation-strings

## VS Code extensions

Search the Visual Studio Marketplace for:

```text
JSDoc Generator — crystal-spider.jsdoc-generator
ESLint — dbaeumer.vscode-eslint
Prettier - Code formatter — esbenp.prettier-vscode
Inline JSDoc Hints — Peckage.inline-jsdoc-hints
```

Extension availability and versions can change, so verify the Marketplace page before standardizing one across a team.

---

# Appendix A: Final Cheat Sheet

```js
/**
 * Short description.
 *
 * Longer explanation when needed.
 *
 * @template T
 * @param {T} value - Input value.
 * @param {Object} [options] - Optional settings.
 * @param {boolean} [options.enabled=true] - Whether processing is enabled.
 * @returns {Promise<T>} Processed value.
 * @throws {TypeError} When input is invalid.
 * @deprecated Use `newFunction()` instead.
 * @since 2.0.0
 * @see {@link newFunction}
 *
 * @example
 * const result = await oldFunction("hello", { enabled: true });
 */
async function oldFunction(value, options = {}) {
  return value;
}
```

Do not copy every tag into every function.

Use only the tags that communicate useful information.

The best JSDoc is not the longest JSDoc.

The best JSDoc lets another developer use the code correctly without having to reverse-engineer the implementation.
