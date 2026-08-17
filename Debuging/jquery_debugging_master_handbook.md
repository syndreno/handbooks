# jQuery Debugging Master Handbook

> **A beginner-to-advanced practical guide for finding, understanding, and fixing jQuery problems**
>
> Covers jQuery 1.x/2.x/3.x legacy code and modern jQuery 4.x debugging, with browser DevTools, selectors, events, DOM manipulation, Ajax, forms, animations, plugins, migration problems, performance, security, testing, and real-world troubleshooting.

---

## Handbook goals

This handbook is designed to be a **single reference file** you can return to whenever a jQuery page is not behaving as expected.

It teaches debugging in this order:

1. Understand what the code is supposed to do.
2. Reproduce the problem reliably.
3. Identify whether the problem is HTML, CSS, JavaScript, jQuery, the network, the backend, or a plugin.
4. Inspect the actual values and DOM state instead of guessing.
5. Reduce the problem to the smallest failing example.
6. Fix the root cause.
7. Verify that the fix does not introduce a second bug.
8. Add defensive code or tests so the problem is easier to detect next time.

The examples are intentionally small first, then become more realistic.

---

# Table of Contents

- [1. What Debugging Means](#1-what-debugging-means)
- [2. How jQuery Fits Into JavaScript](#2-how-jquery-fits-into-javascript)
- [3. Current jQuery Version Notes](#3-current-jquery-version-notes)
- [4. Build a Debugging Mindset](#4-build-a-debugging-mindset)
- [5. Minimum Debugging Setup](#5-minimum-debugging-setup)
- [6. Verify jQuery Is Actually Loaded](#6-verify-jquery-is-actually-loaded)
- [7. Full Build vs Slim Build](#7-full-build-vs-slim-build)
- [8. Read Browser Console Errors](#8-read-browser-console-errors)
- [9. Use Breakpoints and the JavaScript Debugger](#9-use-breakpoints-and-the-javascript-debugger)
- [10. Debugging Selectors](#10-debugging-selectors)
- [11. Debugging Empty jQuery Objects](#11-debugging-empty-jquery-objects)
- [12. DOM Ready and Timing Problems](#12-dom-ready-and-timing-problems)
- [13. jQuery Objects vs DOM Elements](#13-jquery-objects-vs-dom-elements)
- [14. Debugging Method Chaining](#14-debugging-method-chaining)
- [15. Debugging Events](#15-debugging-events)
- [16. Direct Events vs Delegated Events](#16-direct-events-vs-delegated-events)
- [17. Dynamic Elements and Event Delegation](#17-dynamic-elements-and-event-delegation)
- [18. Duplicate Event Handlers](#18-duplicate-event-handlers)
- [19. Event Bubbling, Propagation, and Default Actions](#19-event-bubbling-propagation-and-default-actions)
- [20. `this`, `event.target`, `event.currentTarget`, and `delegateTarget`](#20-this-eventtarget-eventcurrenttarget-and-delegatetarget)
- [21. Debugging `.on()` and `.off()`](#21-debugging-on-and-off)
- [22. Debugging DOM Manipulation](#22-debugging-dom-manipulation)
- [23. `.text()` vs `.html()`](#23-text-vs-html)
- [24. `.attr()` vs `.prop()`](#24-attr-vs-prop)
- [25. `.data()` vs `data-*` Attributes](#25-data-vs-data--attributes)
- [26. Debugging `.val()` and Form Fields](#26-debugging-val-and-form-fields)
- [27. Debugging Classes and CSS](#27-debugging-classes-and-css)
- [28. Visibility Problems](#28-visibility-problems)
- [29. Dimensions and Position Problems](#29-dimensions-and-position-problems)
- [30. Debugging Forms](#30-debugging-forms)
- [31. Preventing Double Form Submission](#31-preventing-double-form-submission)
- [32. Debugging `serialize()` and `serializeArray()`](#32-debugging-serialize-and-serializearray)
- [33. Ajax Debugging Fundamentals](#33-ajax-debugging-fundamentals)
- [34. Debugging `$.ajax()`](#34-debugging-ajax)
- [35. Debugging `$.get()`, `$.post()`, and `$.getJSON()`](#35-debugging-get-post-and-getjson)
- [36. Understanding jqXHR](#36-understanding-jqxhr)
- [37. HTTP Status Codes for Frontend Debugging](#37-http-status-codes-for-frontend-debugging)
- [38. `contentType` vs `dataType`](#38-contenttype-vs-datatype)
- [39. Sending JSON Correctly](#39-sending-json-correctly)
- [40. Sending `FormData` Correctly](#40-sending-formdata-correctly)
- [41. CORS Problems](#41-cors-problems)
- [42. CSRF Problems](#42-csrf-problems)
- [43. Ajax Parser Errors](#43-ajax-parser-errors)
- [44. Race Conditions and Stale Ajax Responses](#44-race-conditions-and-stale-ajax-responses)
- [45. Aborting Ajax Requests](#45-aborting-ajax-requests)
- [46. Global Ajax Error Logging](#46-global-ajax-error-logging)
- [47. Deferreds and Promise-Like Behavior](#47-deferreds-and-promise-like-behavior)
- [48. Debugging `$.when()`](#48-debugging-when)
- [49. Async Error Handling Mistakes](#49-async-error-handling-mistakes)
- [50. Debugging Animations](#50-debugging-animations)
- [51. Animation Queues](#51-animation-queues)
- [52. Plugin Debugging](#52-plugin-debugging)
- [53. `$.fn.pluginName is not a function`](#53-fnpluginname-is-not-a-function)
- [54. `$ is not defined` and `$ is not a function`](#54--is-not-defined-and--is-not-a-function)
- [55. `jQuery.noConflict()`](#55-jquerynoconflict)
- [56. Multiple jQuery Versions on One Page](#56-multiple-jquery-versions-on-one-page)
- [57. Debugging Third-Party Widgets](#57-debugging-third-party-widgets)
- [58. jQuery Migrate](#58-jquery-migrate)
- [59. Debugging jQuery 4 Upgrade Problems](#59-debugging-jquery-4-upgrade-problems)
- [60. Removed and Deprecated APIs](#60-removed-and-deprecated-apis)
- [61. Security Debugging](#61-security-debugging)
- [62. XSS and Unsafe HTML Insertion](#62-xss-and-unsafe-html-insertion)
- [63. Debugging Performance Problems](#63-debugging-performance-problems)
- [64. Layout Thrashing and Repeated DOM Work](#64-layout-thrashing-and-repeated-dom-work)
- [65. Memory Leaks and Cleanup](#65-memory-leaks-and-cleanup)
- [66. Logging Patterns That Scale](#66-logging-patterns-that-scale)
- [67. Reusable Debug Helpers](#67-reusable-debug-helpers)
- [68. Debugging Production Minified Code](#68-debugging-production-minified-code)
- [69. Source Maps](#69-source-maps)
- [70. Testing jQuery Code](#70-testing-jquery-code)
- [71. QUnit Basics for jQuery Projects](#71-qunit-basics-for-jquery-projects)
- [72. Building a Minimal Reproduction](#72-building-a-minimal-reproduction)
- [73. Common Real-World Debugging Scenarios](#73-common-real-world-debugging-scenarios)
- [74. Debugging Decision Tree](#74-debugging-decision-tree)
- [75. Fast Troubleshooting Checklist](#75-fast-troubleshooting-checklist)
- [76. Debugging Best Practices](#76-debugging-best-practices)
- [77. Common Anti-Patterns](#77-common-anti-patterns)
- [78. Beginner Practice Exercises](#78-beginner-practice-exercises)
- [79. Intermediate Practice Exercises](#79-intermediate-practice-exercises)
- [80. Advanced Debugging Challenges](#80-advanced-debugging-challenges)
- [81. jQuery Debugging Cheat Sheet](#81-jquery-debugging-cheat-sheet)
- [82. Final Debugging Workflow](#82-final-debugging-workflow)
- [83. Official References](#83-official-references)
- [84. Debugging Traversal Methods](#84-debugging-traversal-methods)
- [85. `.each()` vs `$.each()`](#85-each-vs-each)
- [86. `.filter()`, `.not()`, `.is()`, and `.has()`](#86-filter-not-is-and-has)
- [87. `.closest()` vs `.parents()` vs `.parent()`](#87-closest-vs-parents-vs-parent)
- [88. `.remove()` vs `.detach()` vs `.empty()`](#88-remove-vs-detach-vs-empty)
- [89. Cloning Elements and Event Handlers](#89-cloning-elements-and-event-handlers)
- [90. Custom Events, `.trigger()`, and `.triggerHandler()`](#90-custom-events-trigger-and-triggerhandler)
- [91. One-Time Event Handlers with `.one()`](#91-one-time-event-handlers-with-one)
- [92. Debugging Ajax Timeouts, Retries, and Authentication](#92-debugging-ajax-timeouts-retries-and-authentication)
- [93. `$.ajaxSetup()` and Hidden Global Configuration](#93-ajaxsetup-and-hidden-global-configuration)
- [94. Debounce, Throttle, Scroll, Resize, and Input Storms](#94-debounce-throttle-scroll-resize-and-input-storms)
- [95. Debugging Bundlers and ES Modules](#95-debugging-bundlers-and-es-modules)
- [96. Debugging jQuery in WordPress and Other noConflict Environments](#96-debugging-jquery-in-wordpress-and-other-noconflict-environments)
- [97. jQuery 4 Focus and Blur Behavior](#97-jquery-4-focus-and-blur-behavior)
- [98. CSP, Trusted Types, and Script Injection Problems](#98-csp-trusted-types-and-script-injection-problems)
- [99. Code Review Checklist for jQuery Debuggability](#99-code-review-checklist-for-jquery-debuggability)
- [100. Master Symptom-to-Cause Matrix](#100-master-symptom-to-cause-matrix)

---

# 1. What Debugging Means

**Debugging** is the process of finding why software behaves differently from what you expected.

A bug may be:

- a syntax error
- a wrong selector
- a missing element
- code running too early
- an event handler that was never attached
- an event handler attached multiple times
- a wrong Ajax URL
- incorrect request data
- invalid JSON
- a backend error
- CSS hiding the result
- a plugin compatibility issue
- an old jQuery API removed by a newer version
- a race condition
- an asynchronous timing issue
- a browser security restriction
- a logic error where the code runs but produces the wrong result

A debugger should avoid asking only:

> "Why is jQuery not working?"

Instead ask smaller questions:

- Is the script file loaded?
- Is jQuery defined?
- Is my selector matching anything?
- Is my handler being attached?
- Is the event firing?
- Is the callback entering?
- What are the actual values?
- Is the Ajax request being sent?
- What status code came back?
- What did the server actually return?
- Did another script throw an earlier error?
- Did CSS hide the DOM change?
- Is a plugin expecting a different jQuery version?

Debugging becomes much easier when you turn one vague problem into several observable questions.

---

# 2. How jQuery Fits Into JavaScript

jQuery is a JavaScript library. It does not replace JavaScript.

This code:

```js
$("#save").on("click", function () {
    $("#message").text("Saved");
});
```

still depends on:

- JavaScript syntax
- the browser DOM
- browser events
- CSS selectors
- JavaScript functions
- JavaScript variables
- JavaScript scope
- browser networking if Ajax is used

Therefore, many errors that appear in a jQuery project are really ordinary JavaScript, HTML, CSS, HTTP, or backend errors.

## A useful debugging classification

| Area | Example symptom |
|---|---|
| HTML | Duplicate IDs, missing input name |
| CSS | Element updated but invisible |
| JavaScript | `ReferenceError`, wrong scope |
| jQuery | Empty selector, wrong method usage |
| Event system | Click handler never runs |
| Network | 404, 500, timeout |
| Backend | Validation error or invalid JSON |
| Browser security | CORS/CSP restriction |
| Plugin | Plugin method missing |
| Version compatibility | Removed/deprecated API |
| Timing | DOM or data not ready yet |

Always identify the layer before changing code.

---

# 3. Current jQuery Version Notes

As of this handbook update, the official current jQuery 4.x release is **jQuery 4.0.0**.

jQuery 4 contains modernization and some breaking changes compared with jQuery 3.

For debugging legacy projects, you may encounter:

- jQuery 1.x
- jQuery 2.x
- jQuery 3.x
- jQuery 4.x
- jQuery Migrate
- old plugins written for earlier jQuery versions

Do not assume code that worked with jQuery 1.12 will work unchanged with jQuery 4.

## Check the version at runtime

```js
console.log($.fn.jquery);
```

Example output:

```text
4.0.0
```

This is one of the first checks you should make when debugging a legacy application.

---

# 4. Build a Debugging Mindset

A strong debugger works with **evidence**, not guesses.

Use this loop:

```text
Observe
  ↓
Reproduce
  ↓
Form a hypothesis
  ↓
Inspect values
  ↓
Test one change
  ↓
Verify
  ↓
Keep or reject the hypothesis
```

## Bad debugging

```text
Button does not work
→ change selector
→ change CSS
→ reinstall jQuery
→ copy code from Stack Overflow
→ add setTimeout
→ still broken
```

## Better debugging

```text
Button does not work
→ inspect Console
→ no error
→ check $("#save").length
→ returns 1
→ add console.log inside handler
→ nothing prints
→ inspect when handler is attached
→ button is inserted later by Ajax
→ switch to delegated event
→ retest
```

The second approach finds the cause instead of randomly changing the application.

---

# 5. Minimum Debugging Setup

Use browser developer tools.

In Chrome/Edge/Firefox, learn these panels:

- **Elements / Inspector** — inspect actual DOM and CSS
- **Console** — errors, logs, expressions
- **Sources / Debugger** — breakpoints and call stack
- **Network** — Ajax requests and responses
- **Application / Storage** — cookies, local storage, session storage
- **Performance** — expensive scripting/layout
- **Memory** — leaks and retained objects

## Start every debugging session with the Console

Look for red errors.

One earlier JavaScript error can stop the rest of a file from running.

Example:

```js
console.log(user.name); // user is not defined

$("#save").on("click", function () {
    console.log("clicked");
});
```

Because the first line throws, the handler below may never be attached.

---

# 6. Verify jQuery Is Actually Loaded

Open DevTools Console and run:

```js
typeof jQuery
```

Expected:

```text
"function"
```

Then:

```js
typeof $
```

Often:

```text
"function"
```

Then:

```js
$.fn.jquery
```

Expected:

```text
"4.0.0"
```

or the version used by your application.

## Error: `jQuery is not defined`

Possible causes:

1. jQuery script failed to load.
2. Your application script loads before jQuery.
3. CDN request failed.
4. Content Security Policy blocked the script.
5. Incorrect script URL.
6. Integrity hash mismatch.
7. The file returned HTML instead of JavaScript.
8. Module/bundler configuration did not expose jQuery globally.

### Wrong order

```html
<script src="app.js"></script>
<script src="jquery.js"></script>
```

If `app.js` uses jQuery immediately, it can fail.

### Better

```html
<script src="jquery.js"></script>
<script src="app.js"></script>
```

## Network check

Open **Network**, reload the page, and inspect `jquery*.js`.

Confirm:

- status is 200
- Content-Type is JavaScript-compatible
- response is actually jQuery code
- request is not blocked
- URL is correct

---

# 7. Full Build vs Slim Build

This is an important modern jQuery debugging issue.

The **slim build** excludes modules that some applications expect.

The official jQuery 4 slim build excludes:

- Ajax
- effects
- Deferreds
- Callbacks

So if you load a slim file and then use Ajax:

```html
<script src="jquery-4.0.0.slim.min.js"></script>
```

```js
$.ajax({
    url: "/api/users"
});
```

you may see a failure because Ajax is not part of that build.

## Check the loaded filename

Look at the Network panel or page source.

If the file contains:

```text
slim
```

ask whether the application needs Ajax, effects, Deferreds, or Callbacks.

## Fix

Use the full build when those modules are required.

## What "build" means

A **build** is a packaged variant of the same jQuery release. The API available at runtime depends on which build you loaded, so the filename is part of your debugging evidence.

A useful capability check is more reliable than assuming from the version number alone:

```js
console.table({
    jquery: $.fn.jquery,
    ajax: typeof $.ajax,
    deferred: typeof $.Deferred,
    callbacks: typeof $.Callbacks,
    animate: typeof $.fn.animate,
    queue: typeof $.fn.queue
});
```

Typical interpretation:

```text
"function"   → that API is present
"undefined"  → that API is not present on this jQuery instance
```

In jQuery 4, the slim build omits Ajax and effects and also omits the Deferred, Callbacks, and queue modules. A page can therefore have a perfectly valid `$.fn.jquery === "4.0.0"` while a particular method is still missing.

## When to use each build

Use the **full build** when legacy code or plugins depend on Ajax, jQuery effects, Deferred/Callbacks, or queue APIs.

Use the **slim build** only when you know those modules are unnecessary and your code uses alternatives such as `fetch()`, native `Promise`, and CSS transitions/animations.

### Debugging warning

Do not fix `$.ajax is not a function` by loading a second copy of jQuery. First confirm the existing build. Two jQuery instances can create harder plugin and event problems.

---

# 8. Read Browser Console Errors

Console errors often tell you:

- what failed
- where it failed
- the file
- the line number
- the stack trace

## Common errors

### `ReferenceError`

```text
ReferenceError: userId is not defined
```

Meaning: JavaScript cannot find that variable.

### `TypeError`

```text
TypeError: $(...).pluginName is not a function
```

Meaning: the value exists, but the requested method does not.

Typical plugin causes:

- plugin script not loaded
- plugin loaded before jQuery
- wrong plugin version
- plugin failed during initialization
- multiple jQuery copies
- plugin attached to another jQuery instance

### Syntax error

```text
SyntaxError: Unexpected token '}'
```

The browser could not parse the JavaScript.

### JSON parsing error

```text
SyntaxError: Unexpected token '<'
```

A very common cause is that the code expected JSON but the server returned HTML, often an error page.

---

# 9. Use Breakpoints and the JavaScript Debugger

`console.log()` is useful, but breakpoints are stronger.

Given:

```js
$("#save").on("click", function () {
    const amount = $("#amount").val();
    const total = calculateTotal(amount);
    $("#result").text(total);
});
```

Set a breakpoint on:

```js
const amount = $("#amount").val();
```

Then inspect:

- `amount`
- `typeof amount`
- `this`
- local variables
- call stack
- closures

## Add a debugger statement

```js
$("#save").on("click", function () {
    debugger;

    const amount = $("#amount").val();
});
```

When DevTools is open, execution pauses there.

Do not leave `debugger;` statements in production code intentionally unless your project has a controlled reason.

---

# 10. Debugging Selectors

Selectors are one of the most common jQuery failure points.

Example:

```html
<button id="saveBtn">Save</button>
```

Wrong:

```js
$("#save").on("click", function () {
    // ...
});
```

The code does not throw. It simply matches zero elements.

## Check the selector

```js
console.log($("#save").length);
```

Output:

```text
0
```

Correct:

```js
console.log($("#saveBtn").length);
```

Output:

```text
1
```

## Useful debugging pattern

```js
const $button = $("#saveBtn");

console.log("save button matches:", $button.length);

if (!$button.length) {
    console.warn("Save button was not found");
}
```

## Common selector mistakes

### Missing `#` for an ID

Wrong:

```js
$("saveBtn")
```

This looks for a `<saveBtn>` element.

Correct:

```js
$("#saveBtn")
```

### Missing `.` for a class

Wrong:

```js
$("product")
```

Correct:

```js
$(".product")
```

### Wrong attribute selector

HTML:

```html
<input name="email">
```

Correct:

```js
$('input[name="email"]')
```

### Generated IDs containing special characters

IDs from server-side frameworks may contain characters that require escaping.

Prefer stable classes or `data-*` attributes when possible.

---

# 11. Debugging Empty jQuery Objects

A useful characteristic of jQuery is that many operations on an empty selection do not throw.

```js
$("#does-not-exist").text("Hello");
```

This usually does nothing.

That convenience can hide bugs.

## Detect an empty selection

```js
const $el = $("#does-not-exist");

if ($el.length === 0) {
    console.error("Element not found");
}
```

## Exactly one expected element

```js
if ($el.length !== 1) {
    console.warn("Expected exactly one element, found:", $el.length);
}
```

This is especially useful for:

- modal containers
- form IDs
- unique toolbar buttons
- single-page initialization roots

---

# 12. DOM Ready and Timing Problems

This can fail when the script runs before the DOM element exists:

```js
$("#save").on("click", saveData);
```

If the script is in `<head>` without appropriate loading behavior, `#save` may not exist yet.

## jQuery ready shorthand

```js
$(function () {
    $("#save").on("click", saveData);
});
```

Equivalent idea:

> Run this initialization after the document DOM is ready.

## Debugging timing

Log:

```js
console.log("readyState:", document.readyState);
console.log("save count:", $("#save").length);
```

Possible states:

- `loading`
- `interactive`
- `complete`

## Important distinction

DOM ready only means the document structure is ready.

It does **not** mean:

- every Ajax request is finished
- every image is loaded
- every plugin is initialized
- every dynamically generated element exists
- your application state has arrived from the server

---

# 13. jQuery Objects vs DOM Elements

This confusion causes many beginner bugs.

```js
const $box = $("#box");
```

`$box` is a jQuery object.

A DOM element can be accessed with:

```js
const box = $box[0];
```

or:

```js
const box = $box.get(0);
```

## jQuery method

```js
$box.addClass("active");
```

## Native DOM method/property

```js
box.classList.add("active");
```

### Wrong

```js
$box.classList.add("active");
```

`classList` belongs to the DOM element, not the jQuery wrapper.

### Wrong

```js
box.addClass("active");
```

`addClass()` belongs to jQuery, not the raw DOM element.

## Debug both

```js
console.log($box);
console.log($box[0]);
```

---

# 14. Debugging Method Chaining

jQuery frequently returns a jQuery object so methods can be chained.

```js
$("#message")
    .addClass("success")
    .text("Saved")
    .show();
```

When a long chain fails, split it.

Instead of:

```js
$("#panel").find(".row").eq(index).addClass("selected").show();
```

debug:

```js
const $panel = $("#panel");
console.log("panel:", $panel.length);

const $rows = $panel.find(".row");
console.log("rows:", $rows.length);

const $row = $rows.eq(index);
console.log("selected row:", $row.length, "index:", index);

$row.addClass("selected").show();
```

This makes the exact failing stage visible.

---

# 15. Debugging Events

Suppose:

```js
$("#save").on("click", function () {
    console.log("clicked");
});
```

If nothing happens, check in this order:

1. Did the selector match?
2. Did initialization code run?
3. Was the handler attached?
4. Is the element later replaced?
5. Is another element covering it?
6. Is it disabled?
7. Is another handler stopping propagation?
8. Is a JavaScript error occurring before binding?
9. Is the element inside an iframe or shadow root?
10. Is the expected event actually being generated?

## Add logs around binding

```js
console.log("binding save button");

const $save = $("#save");
console.log("matches:", $save.length);

$save.on("click", function (event) {
    console.log("save clicked", event);
});
```

---

# 16. Direct Events vs Delegated Events

## Direct binding

```js
$(".delete-btn").on("click", function () {
    // ...
});
```

This binds to elements that exist at binding time.

## Delegated binding

```js
$("#items").on("click", ".delete-btn", function () {
    // ...
});
```

The handler is attached to `#items`.

When a click bubbles up from a matching `.delete-btn`, the handler runs.

Use delegation when matching child elements may be added later.

## How the two models differ

With **direct binding**, jQuery stores the handler on every matched element:

```js
const $buttons = $(".delete-btn");
$buttons.on("click", handler);
```

If five buttons match, all five existing buttons receive the handler. A sixth button inserted later does not automatically inherit it.

With **delegation**, the handler is stored on a stable ancestor and jQuery checks the bubbled event against the child selector:

```js
$("#items").on("click", ".delete-btn", handler);
```

The delegated handler can therefore handle matching descendants added later.

## Choosing the delegation root

Prefer the closest stable ancestor that owns the dynamic children:

```js
$("#items").on("click.orders", ".delete-btn", handler);
```

rather than delegating everything to `document`. A closer root reduces accidental matches and makes ownership/cleanup clearer.

## When delegation is not appropriate

Delegation depends on event propagation and selector matching. It is less useful when:

- the event does not reach the chosen ancestor as expected;
- the target lives in a different iframe/shadow tree;
- direct per-element state/lifecycle is simpler;
- the ancestor itself is replaced.

### Debug proof

Log all three values:

```js
$("#items").on("click", ".delete-btn", function (event) {
    console.log({
        target: event.target,
        currentTarget: event.currentTarget,
        delegateTarget: event.delegateTarget
    });
});
```

This reveals where the event originated, which descendant matched, and where the delegated handler is installed.

---

# 17. Dynamic Elements and Event Delegation

A classic bug:

```js
$(".remove").on("click", function () {
    $(this).closest(".row").remove();
});

$("#add").on("click", function () {
    $("#rows").append('<button class="remove">Remove</button>');
});
```

The newly added `.remove` button may not have the original direct handler.

## Fix with delegation

```js
$("#rows").on("click", ".remove", function () {
    $(this).closest(".row").remove();
});
```

## Debugging proof

After adding the button:

```js
console.log($(".remove").length);
```

The selector finds the new button, but that does not mean an earlier direct event binding was attached to it.

---

# 18. Duplicate Event Handlers

Symptom:

> One click sends the Ajax request twice.

Possible cause:

```js
function init() {
    $("#save").on("click", save);
}

init();
init();
```

Now the same handler is attached twice.

## Detect

Add:

```js
console.count("save handler fired");
```

One click might output:

```text
save handler fired: 1
save handler fired: 2
```

## Better initialization design

Make initialization run only once where possible.

Or use event namespaces:

```js
$("#save")
    .off("click.orderForm")
    .on("click.orderForm", save);
```

This removes the named handler group before rebinding.

Do not casually use:

```js
$("#save").off();
```

because it can remove unrelated handlers.

---

# 19. Event Bubbling, Propagation, and Default Actions

HTML:

```html
<a id="link" href="/dashboard">
    <span>Open dashboard</span>
</a>
```

## Prevent browser default behavior

```js
$("#link").on("click", function (event) {
    event.preventDefault();
});
```

This prevents navigation.

## Stop bubbling

```js
event.stopPropagation();
```

This prevents the event from continuing to ancestor handlers.

## Debugging caution

If a parent click handler unexpectedly does not run, search for:

```js
stopPropagation()
```

and:

```js
return false
```

In jQuery event handlers, `return false` has broader behavior than a normal JavaScript return; it prevents default behavior and stops propagation.

Prefer explicit intent:

```js
event.preventDefault();
```

or:

```js
event.stopPropagation();
```

when that is what you actually mean.

---

# 20. `this`, `event.target`, `event.currentTarget`, and `delegateTarget`

These values are frequently confused.

HTML:

```html
<button class="save">
    <span class="icon">💾</span>
    Save
</button>
```

Code:

```js
$(document).on("click", ".save", function (event) {
    console.log("target:", event.target);
    console.log("currentTarget:", event.currentTarget);
    console.log("delegateTarget:", event.delegateTarget);
    console.log("this:", this);
});
```

If the user clicks the `<span>`:

- `event.target` → the `<span>`
- `event.currentTarget` → the matched `.save` button for the current handler
- `this` → normally the matched `.save` element in a traditional function handler
- `event.delegateTarget` → the element where the delegated handler was attached, here `document`

## Arrow function trap

```js
$(".save").on("click", (event) => {
    console.log(this);
});
```

Arrow functions do not bind their own `this`.

If your code expects jQuery's handler `this`, use:

```js
$(".save").on("click", function (event) {
    console.log(this);
});
```

Or avoid `this` ambiguity:

```js
$(".save").on("click", function (event) {
    const $button = $(event.currentTarget);
});
```

---

# 21. Debugging `.on()` and `.off()`

`.on()` attaches event handlers.

Typical signatures include:

```js
$el.on("click", handler);
```

and delegated:

```js
$root.on("click", ".child", handler);
```

`.off()` removes handlers.

## Namespaced events

Recommended for larger applications/plugins:

```js
$(window).on("resize.dashboard", refreshDashboard);
```

Cleanup:

```js
$(window).off("resize.dashboard");
```

This avoids removing someone else's resize handler.

## Common bug

Binding with one function but trying to remove another:

```js
$("#save").on("click", function () {
    save();
});

$("#save").off("click", save);
```

The anonymous wrapper and `save` are different function references.

Better:

```js
function handleSave() {
    save();
}

$("#save").on("click", handleSave);
$("#save").off("click", handleSave);
```

---

# 22. Debugging DOM Manipulation

Common methods:

- `.append()`
- `.prepend()`
- `.before()`
- `.after()`
- `.remove()`
- `.empty()`
- `.replaceWith()`
- `.clone()`

When DOM manipulation appears not to work, inspect:

1. Did the selector match?
2. Was the expected parent selected?
3. Was the element inserted but hidden?
4. Was it immediately removed or overwritten?
5. Did another render replace the parent?
6. Did malformed HTML change how the browser parsed it?
7. Did an exception occur before the mutation?

## Debug actual DOM

After insertion:

```js
$("#list").append("<li>New</li>");

console.log($("#list").html());
console.log($("#list li").length);
```

Also inspect the **Elements** panel rather than assuming the page visually represents the DOM correctly.

---

# 23. `.text()` vs `.html()`

## `.text()`

Treats content as text.

```js
$("#message").text("<b>Hello</b>");
```

Visible output:

```text
<b>Hello</b>
```

## `.html()`

Interprets content as HTML.

```js
$("#message").html("<b>Hello</b>");
```

Visible output:

**Hello**

## Debugging and security rule

If the value comes from a user, database, query string, or API and does not intentionally contain trusted HTML, prefer:

```js
.text(value)
```

instead of:

```js
.html(value)
```

This helps reduce XSS risk.

## Getter behavior

Both methods can also read content.

```js
console.log($("#message").text());
console.log($("#message").html());
```

Typical difference for:

```html
<div id="message"><b>Hello</b> world</div>
```

is conceptually:

```text
.text() → "Hello world"
.html() → "<b>Hello</b> world"
```

`.text()` returns textual content; `.html()` returns serialized inner markup.

## When to use which

Use `.text()` when the value is ordinary display text.

Use `.html()` when the application intentionally owns/trusts the markup being inserted or has safely sanitized allowed rich content.

If you only need to create fixed markup with dynamic text, structured construction is often clearer:

```js
const $strong = $("<strong>").text(userName);
$("#message").empty().append("Hello ", $strong);
```

This keeps untrusted text separate from markup.

---

# 24. `.attr()` vs `.prop()`

This causes many checkbox bugs.

HTML:

```html
<input id="agree" type="checkbox" checked>
```

## Attribute

```js
$("#agree").attr("checked");
```

Describes the HTML attribute.

## Property

```js
$("#agree").prop("checked");
```

Describes the current live checked state.

For current boolean state, usually use:

```js
$("#agree").prop("checked")
```

## Example

```js
$("#agree").on("change", function () {
    console.log($(this).prop("checked"));
});
```

Output:

```text
true
```

or:

```text
false
```

depending on the user's current action.

## Attribute = markup/configuration; property = live DOM state

An HTML attribute participates in the element's initial markup/configuration. A DOM property is the JavaScript state on the live element.

This matters beyond checkboxes.

```js
const input = document.querySelector("#name");

console.log(input.getAttribute("value")); // markup attribute
console.log(input.value);                 // current live value
```

After the user types, those values can differ.

In jQuery:

```js
$("#name").attr("value");
$("#name").prop("value");
```

For normal form values, `.val()` is usually the clearer API:

```js
$("#name").val();
```

## Boolean properties

Use `.prop()` for live booleans such as:

```js
$("#agree").prop("checked");
$("#save").prop("disabled");
$("option:selected").prop("selected");
```

Do not use `.attr("checked")` to answer "is the box checked right now?"

## Setter examples

```js
$("#save").prop("disabled", true);
$("#field").attr("aria-label", "Search");
```

ARIA states are attributes, not DOM boolean properties. Do not convert ARIA values to `.prop()` merely because the string looks boolean.

---

# 25. `.data()` vs `data-*` Attributes

HTML:

```html
<div id="user" data-user-id="42"></div>
```

Read:

```js
$("#user").data("userId");
```

Likely result:

```text
42
```

A subtle issue: jQuery can cache data values internally after initial access.

If you later modify the raw attribute:

```js
$("#user").attr("data-user-id", "99");
```

then:

```js
$("#user").data("userId");
```

may still reflect the cached jQuery data rather than behaving like a fresh raw attribute lookup.

For the raw string attribute:

```js
$("#user").attr("data-user-id");
```

## Debug both when confused

```js
console.log("data():", $("#user").data("userId"));
console.log("attr():", $("#user").attr("data-user-id"));
```

Choose one storage/update approach consistently.

---

# 26. Debugging `.val()` and Form Fields

For:

```html
<input id="qty" value="5">
```

```js
const qty = $("#qty").val();
```

Remember that form values are commonly strings.

```js
console.log(qty, typeof qty);
```

Possible output:

```text
5 string
```

## Classic arithmetic bug

```js
const a = $("#a").val(); // "10"
const b = $("#b").val(); // "20"

console.log(a + b);
```

Output:

```text
1020
```

Fix:

```js
const a = Number($("#a").val());
const b = Number($("#b").val());

console.log(a + b);
```

Output:

```text
30
```

## Validate conversion

```js
const qty = Number($("#qty").val());

if (!Number.isFinite(qty)) {
    console.error("Invalid quantity");
}
```

---

# 27. Debugging Classes and CSS

Suppose:

```js
$("#panel").addClass("open");
```

but nothing looks different.

Check:

```js
console.log($("#panel").attr("class"));
console.log($("#panel").hasClass("open"));
```

If the class exists, the problem may be CSS rather than jQuery.

Inspect computed styles.

Possible causes:

- selector specificity
- `!important`
- stylesheet not loaded
- incorrect class name
- media query
- animation overriding the property
- another class wins
- inline style overrides expected style
- parent layout constrains the result

---

# 28. Visibility Problems

jQuery changes can succeed while the result remains invisible.

Check:

```js
console.log($("#panel").is(":visible"));
console.log($("#panel").css("display"));
console.log($("#panel").css("visibility"));
console.log($("#panel").css("opacity"));
```

Also inspect ancestors.

An element can be hidden because its parent is hidden.

Example:

```html
<div style="display:none">
    <div id="panel">Visible CSS on child cannot overcome hidden parent</div>
</div>
```

## "Visible" has several meanings

A user can fail to see an element even when `display` is not `none`.

Check for:

- `visibility: hidden`;
- `opacity: 0`;
- zero width/height;
- clipping/overflow;
- off-screen positioning;
- another element covering it;
- hidden/collapsed ancestors;
- a transform moving it;
- color/background making it appear blank.

## DOM presence vs user visibility

These answer different questions:

```js
console.log($("#panel").length);        // does the selection contain an element?
console.log($("#panel").is(":visible")); // jQuery visibility test
```

Do not use visibility as a substitute for existence.

## Debug ancestors quickly

```js
$("#panel").parents().each(function () {
    const $el = $(this);

    if ($el.css("display") === "none" || $el.css("visibility") === "hidden") {
        console.warn("hidden ancestor:", this);
    }
});
```

For stacking/overlap bugs, switch to the Elements panel and inspect the actual box under the pointer rather than adding a larger `z-index` blindly.

---

# 29. Dimensions and Position Problems

Useful methods:

```js
.width()
.height()
.innerWidth()
.innerHeight()
.outerWidth()
.outerHeight()
.offset()
.position()
.scrollTop()
.scrollLeft()
```

When dimensions look wrong, inspect:

- `box-sizing`
- padding
- border
- margin
- hidden state
- transforms
- parent constraints
- page zoom
- fonts loading later
- timing of measurement

## Hidden element issue

Measuring an element while it or an ancestor is `display:none` can produce unexpected results.

Debug:

```js
const $panel = $("#panel");

console.log({
    visible: $panel.is(":visible"),
    width: $panel.width(),
    outerWidth: $panel.outerWidth(),
    offset: $panel.offset()
});
```

---

# 30. Debugging Forms

Example:

```js
$("#userForm").on("submit", function (event) {
    event.preventDefault();

    console.log("form submitted");
});
```

If the handler does not run:

1. verify the form selector
2. confirm there is an actual `<form>`
3. check for earlier errors
4. check dynamically replaced form
5. verify submit button behavior
6. inspect native validation
7. inspect whether another handler stops execution

## Native validation can block submit

HTML:

```html
<input type="email" required>
```

If invalid, the browser may prevent the submit event flow you expect.

Check the browser validation UI.

---

# 31. Preventing Double Form Submission

A common production bug is double-clicking.

```js
let submitting = false;

$("#orderForm").on("submit", function (event) {
    event.preventDefault();

    if (submitting) {
        return;
    }

    submitting = true;

    const $button = $("#submitOrder");
    $button.prop("disabled", true);

    $.ajax({
        url: "/orders",
        method: "POST",
        data: $(this).serialize()
    })
    .done(function () {
        console.log("Order created");
    })
    .fail(function (xhr) {
        console.error("Order failed", xhr.status);
    })
    .always(function () {
        submitting = false;
        $button.prop("disabled", false);
    });
});
```

Backend idempotency is still valuable because frontend prevention alone cannot guarantee a request is sent only once.

---

# 32. Debugging `serialize()` and `serializeArray()`

Example:

```html
<form id="profileForm">
    <input name="name" value="Asha">
    <input name="email" value="asha@example.com">
</form>
```

```js
console.log($("#profileForm").serialize());
```

Possible output:

```text
name=Asha&email=asha%40example.com
```

## Missing fields

A frequent problem is forgetting the `name` attribute.

This:

```html
<input id="email" value="asha@example.com">
```

does not provide a `name`, so form serialization will not include it as a successful control.

Fix:

```html
<input id="email" name="email" value="asha@example.com">
```

## Debug

```js
console.table($("#profileForm").serializeArray());
```

---

# 33. Ajax Debugging Fundamentals

Ajax debugging is not only about JavaScript.

An Ajax transaction involves:

```text
jQuery
  ↓
browser request
  ↓
DNS/network/proxy
  ↓
web server
  ↓
application/backend
  ↓
database/other services
  ↓
response
  ↓
browser
  ↓
jQuery parser/converter
  ↓
your callback
```

A failure anywhere can look like "Ajax does not work."

## Always inspect the Network panel

For each failed request, inspect:

- Request URL
- Request Method
- Status Code
- Request Headers
- Request Payload / Form Data
- Response Headers
- Response Body
- Timing
- Redirects
- Cookies
- CORS messages

The Network panel is usually more trustworthy than guessing from UI behavior.

---

# 34. Debugging `$.ajax()`

A strong debugging template:

```js
$.ajax({
    url: "/api/users",
    method: "GET",
    dataType: "json"
})
.done(function (data, textStatus, jqXHR) {
    console.log("success", {
        textStatus,
        status: jqXHR.status,
        data
    });
})
.fail(function (jqXHR, textStatus, errorThrown) {
    console.error("ajax failed", {
        status: jqXHR.status,
        textStatus,
        errorThrown,
        responseText: jqXHR.responseText
    });
})
.always(function () {
    console.log("request finished");
});
```

This gives much more information than:

```js
$.get("/api/users", function (data) {
    // ...
});
```

during debugging.

## Parameters to understand

Common `$.ajax()` options:

| Option | Purpose |
|---|---|
| `url` | Destination |
| `method` / `type` | HTTP method |
| `data` | Request data |
| `dataType` | Expected response data type |
| `contentType` | Request Content-Type |
| `headers` | Extra HTTP headers |
| `timeout` | Client timeout |
| `processData` | Whether jQuery transforms `data` |
| `cache` | Request caching behavior in relevant cases |
| `beforeSend` | Hook before sending |
| `success` | Success callback style |
| `error` | Error callback style |
| `complete` | Runs after success/failure |

For modern composition, jqXHR `.done()`, `.fail()`, and `.always()` are often clearer.

---

# 35. Debugging `$.get()`, `$.post()`, and `$.getJSON()`

Shorthand methods are convenient, but do not omit failure handling.

```js
$.get("/api/profile")
    .done(function (data) {
        console.log(data);
    })
    .fail(function (xhr, status, error) {
        console.error(status, error, xhr.responseText);
    });
```

## Why this matters

If you only provide a success path, errors may be easy to miss from the application UI.

During debugging, always include `.fail()` or inspect the Network panel.

## What the shorthand methods do

These functions are convenience wrappers around jQuery's Ajax system.

Common intent:

```js
$.get(url, data);
$.post(url, data);
$.getJSON(url, data);
```

They return a jqXHR, so you can attach `.done()`, `.fail()`, and `.always()` just like with `$.ajax()`.

## When to switch to `$.ajax()`

Use the shorthand when the request is simple and its defaults are clear.

Prefer `$.ajax()` when you need explicit control over options such as:

- request headers;
- timeout;
- `contentType`;
- `dataType`;
- credentials/cross-origin behavior;
- `processData`;
- custom converters or lifecycle hooks.

## Debug the expanded request, not the helper name

Whether code used `$.get()` or `$.post()`, the Network panel remains the source of truth for:

```text
final URL
HTTP method
query string / body
request headers
response status
response headers
response body
timing
```

A shorthand call can be syntactically correct while the route, data, or server contract is wrong.

---

# 36. Understanding jqXHR

jQuery Ajax methods return a `jqXHR` object.

Example:

```js
const request = $.ajax({
    url: "/api/users"
});
```

Useful operations:

```js
request.done(...);
request.fail(...);
request.always(...);
request.abort();
```

Useful response information in failure callbacks:

```js
jqXHR.status
jqXHR.statusText
jqXHR.responseText
jqXHR.responseJSON
jqXHR.getResponseHeader(...)
```

## Debug dump

```js
.fail(function (xhr, textStatus, errorThrown) {
    console.log("status", xhr.status);
    console.log("statusText", xhr.statusText);
    console.log("textStatus", textStatus);
    console.log("errorThrown", errorThrown);
    console.log("responseText", xhr.responseText);
    console.log("responseJSON", xhr.responseJSON);
});
```

## jqXHR is more than the raw browser request

`jqXHR` is jQuery's request object. It exposes XMLHttpRequest-like response information plus jQuery Deferred-style methods.

Success callbacks commonly receive:

```js
.done(function (data, textStatus, jqXHR) {
    // ...
});
```

Failure callbacks commonly receive:

```js
.fail(function (jqXHR, textStatus, errorThrown) {
    // ...
});
```

Notice the argument order differs.

## Return value

Because `$.ajax()` returns jqXHR immediately, this does **not** return the eventual server data:

```js
const users = $.ajax("/api/users");
```

`users` is the request object, not the parsed user array.

Consume the asynchronous result:

```js
$.ajax("/api/users")
    .done(function (users) {
        console.log(users);
    });
```

## Header inspection

```js
request.done(function (data, status, xhr) {
    console.log(xhr.getResponseHeader("Content-Type"));
});
```

Do not assume the response type from the URL extension or endpoint name; inspect headers and the actual body.

---

# 37. HTTP Status Codes for Frontend Debugging

Common interpretations:

| Status | Typical meaning |
|---|---|
| 200 | Request succeeded |
| 201 | Resource created |
| 204 | Success with no response body |
| 301/302 | Redirect |
| 304 | Not modified / caching path |
| 400 | Bad request |
| 401 | Not authenticated |
| 403 | Forbidden |
| 404 | Route/resource not found |
| 405 | HTTP method not allowed |
| 409 | Conflict |
| 415 | Unsupported media type |
| 422 | Validation/unprocessable input |
| 429 | Too many requests |
| 500 | Server error |
| 502 | Bad gateway |
| 503 | Service unavailable |
| 504 | Gateway timeout |

Do not treat every non-200 response as a "jQuery issue."

A `500` usually means you need server-side logs too.

---

# 38. `contentType` vs `dataType`

These are frequently confused.

## `contentType`

Describes what you are **sending**.

Example:

```js
contentType: "application/json"
```

## `dataType`

Tells jQuery what response type you expect or want processed as.

Example:

```js
dataType: "json"
```

## JSON request example

```js
$.ajax({
    url: "/api/users",
    method: "POST",
    contentType: "application/json",
    dataType: "json",
    data: JSON.stringify({
        name: "Asha"
    })
});
```

Think:

```text
contentType = request body format
dataType    = expected response format
```

## They describe opposite directions

Visualize one request:

```text
browser
  -- request body + Content-Type --> server
  <-- response body + Content-Type -- server
```

`contentType` configures the media type jQuery sends for the **request body**.

`dataType` tells jQuery how you want the **response** interpreted. If omitted, jQuery can infer behavior from response headers and other request settings.

## They do not have to match

A request can send form encoding and receive JSON:

```js
$.ajax({
    url: "/login",
    method: "POST",
    data: {
        username: "asha",
        password: "..."
    },
    dataType: "json"
});
```

Or send JSON and receive no body:

```js
$.ajax({
    url: "/api/items/10",
    method: "DELETE",
    contentType: "application/json"
});
```

Do not add `dataType: "json"` merely because the request body is JSON.

## Debugging clue

A parser error often means the response body does not match the declared/expected `dataType`, even if the request `contentType` is correct.

---

# 39. Sending JSON Correctly

Wrong:

```js
$.ajax({
    url: "/api/users",
    method: "POST",
    contentType: "application/json",
    data: {
        name: "Asha"
    }
});
```

Depending on processing, the body may not be the JSON your server expects.

Better:

```js
$.ajax({
    url: "/api/users",
    method: "POST",
    contentType: "application/json",
    data: JSON.stringify({
        name: "Asha"
    })
});
```

## Debug request body

Use Network → Payload.

Expected:

```json
{
  "name": "Asha"
}
```

If you see:

```text
name=Asha
```

your backend may be expecting a different encoding.

## `processData` and JSON strings

jQuery normally processes non-string `data` into URL-encoded form. `JSON.stringify()` produces a string, so the JSON example can be sent as-is.

A fuller pattern is:

```js
const payload = {
    name: "Asha",
    active: true
};

$.ajax({
    url: "/api/users",
    method: "POST",
    contentType: "application/json; charset=UTF-8",
    dataType: "json",
    data: JSON.stringify(payload)
});
```

## Inputs and output

Input JavaScript object:

```js
{ name: "Asha", active: true }
```

Serialized request body:

```json
{"name":"Asha","active":true}
```

The server must be configured to parse JSON for that route. Frontend correctness alone cannot make a form-only backend accept JSON.

## Common mistakes

- setting `contentType: "application/json"` but not stringifying the object;
- double-stringifying an already serialized string;
- sending dates/numbers in a shape the API contract does not accept;
- expecting `undefined` object properties to appear in JSON;
- forgetting CSRF/auth headers required by the backend.

Always compare the Network payload with the API contract.

---

# 40. Sending `FormData` Correctly

For file uploads:

```js
const formData = new FormData();
formData.append("name", "Asha");
formData.append("avatar", $("#avatar")[0].files[0]);

$.ajax({
    url: "/api/profile",
    method: "POST",
    data: formData,
    processData: false,
    contentType: false
});
```

## Why?

`processData: false`

prevents jQuery from converting the `FormData` object into a query string.

`contentType: false`

lets the browser set the multipart Content-Type including the required boundary.

## Common wrong pattern

```js
contentType: "multipart/form-data"
```

Manually setting this usually omits the browser-generated boundary.

## Construct from an existing form

You can build FormData from a form element:

```js
const form = document.querySelector("#profileForm");
const formData = new FormData(form);
```

This uses successful form controls according to browser form rules.

Inspect entries while debugging:

```js
for (const [key, value] of formData.entries()) {
    console.log(key, value);
}
```

For files, `value` may be a `File` object rather than a string.

## Browser-controlled multipart boundary

A multipart header looks conceptually like:

```text
Content-Type: multipart/form-data; boundary=----BrowserGeneratedBoundary
```

The boundary must match separators in the encoded body. That is why `contentType: false` is important with jQuery FormData uploads.

## When not to use FormData

If the API contract expects JSON and no file/blob upload is involved, ordinary JSON is often easier to inspect, validate, and test. Choose the encoding expected by the server rather than using FormData as a universal request format.

---

# 41. CORS Problems

A request from one origin to another may be restricted by the browser.

Origins differ when scheme, host, or port differs.

Examples:

```text
https://app.example.com
https://api.example.com
```

Different host → cross-origin.

```text
http://localhost:3000
http://localhost:8080
```

Different port → cross-origin.

## Symptoms

Console may mention:

```text
CORS policy
Access-Control-Allow-Origin
preflight
```

## Important principle

You generally cannot "fix CORS in jQuery."

CORS is controlled by browser security rules and server response headers.

Debug:

1. inspect OPTIONS preflight if present
2. inspect response headers
3. verify allowed origin
4. verify allowed methods
5. verify allowed headers
6. verify credential settings

Do not disable browser security as a production solution.

---

# 42. CSRF Problems

A POST may work in one environment but return 403 in another because a CSRF token is required.

Example pattern:

```html
<meta name="csrf-token" content="TOKEN_VALUE">
```

```js
const token = $('meta[name="csrf-token"]').attr("content");

$.ajax({
    url: "/api/order",
    method: "POST",
    headers: {
        "X-CSRF-Token": token
    },
    data: {
        itemId: 10
    }
});
```

Exact token names and transport rules depend on your backend framework.

Debug the request headers and backend CSRF configuration.

## What CSRF protection is checking

Cross-Site Request Forgery protection helps a server reject state-changing requests that appear to come from an untrusted origin/context while still carrying a user's authenticated session.

The exact mechanism is framework-specific. Common designs use:

- a token in a form field;
- a token in a custom request header;
- a cookie + matching header/token;
- origin/referer validation;
- framework middleware combining several checks.

## Debugging sequence

For a 403/419-like failure on a write request:

1. confirm the user is authenticated;
2. inspect whether the CSRF cookie/token was issued;
3. inspect the request header/body containing the token;
4. compare token names/casing with backend configuration;
5. verify credentials/cookies are actually sent;
6. inspect SameSite/Secure behavior;
7. read the server error/log if available.

## Do not "fix" by disabling protection

If a route requires CSRF protection, removing middleware or globally disabling checks is a security regression. Fix the client/server token flow or use the framework's documented exemption only for routes that truly use a different security model.

---

# 43. Ajax Parser Errors

You may get:

```text
parsererror
```

when jQuery expects JSON but cannot parse the response.

Example:

```js
$.ajax({
    url: "/api/user",
    dataType: "json"
})
.fail(function (xhr, textStatus, errorThrown) {
    console.log(textStatus);
    console.log(xhr.responseText);
});
```

Imagine the server returned:

```html
Warning: Undefined variable $user
```

or:

```html
<!doctype html>
<html>
...
```

That is not valid JSON.

## Debugging rule

When JSON parsing fails, inspect **raw `responseText` first**.

Common causes:

- PHP warning before JSON
- login page redirect
- 404 HTML page
- proxy error page
- invalid JSON syntax
- trailing debug output
- wrong endpoint
- wrong Content-Type or data expectation

---

# 44. Race Conditions and Stale Ajax Responses

Search-as-you-type can create races.

```js
$("#search").on("input", function () {
    $.get("/search", { q: this.value })
        .done(renderResults);
});
```

User types:

```text
c
ca
cat
```

The `cat` request might finish before the `ca` request.

Then an old response can overwrite newer results.

## Solution: sequence token

```js
let searchVersion = 0;

$("#search").on("input", function () {
    const version = ++searchVersion;
    const query = this.value;

    $.get("/search", { q: query })
        .done(function (data) {
            if (version !== searchVersion) {
                return;
            }

            renderResults(data);
        });
});
```

Another approach is aborting the previous request.

---

# 45. Aborting Ajax Requests

```js
let currentRequest = null;

$("#search").on("input", function () {
    if (currentRequest) {
        currentRequest.abort();
    }

    currentRequest = $.ajax({
        url: "/search",
        data: {
            q: this.value
        }
    })
    .done(renderResults)
    .fail(function (xhr, textStatus) {
        if (textStatus !== "abort") {
            console.error("Search failed");
        }
    });
});
```

An aborted request is not necessarily an application error.

Handle `"abort"` separately if needed.

## What `abort()` does

`$.ajax()` returns a **jqXHR** object. Calling:

```js
currentRequest.abort();
```

asks jQuery to cancel that request from the page's point of view. The failure callbacks still run, normally with a status such as `"abort"`, which is why cancellation should usually be distinguished from a real network/server failure.

## When aborting is useful

Common cases include:

- live search where an older query is no longer relevant;
- typeahead/autocomplete;
- switching tabs while a tab-specific request is still in flight;
- replacing a page/component before its request finishes.

## Important limitation

Cancellation does not guarantee that the server stopped all work. The server may already have received or processed the request.

For a read-only search request this is usually harmless. For a write operation such as "create order" or "charge payment", do not assume client-side abort is equivalent to transaction cancellation.

## Cleanup pattern

After the request settles, clear the reference so later code does not mistake a finished request for an active one:

```js
currentRequest = $.ajax({
    url: "/search",
    data: { q: term }
})
.always(function () {
    currentRequest = null;
});
```

When race conditions matter, also use request IDs or compare the query that produced the response before rendering it.

---

# 46. Global Ajax Error Logging

During development, you can add global logging:

```js
$(document).ajaxError(function (event, jqXHR, ajaxSettings, thrownError) {
    console.error("Global Ajax error", {
        url: ajaxSettings.url,
        method: ajaxSettings.type,
        status: jqXHR.status,
        thrownError,
        responseText: jqXHR.responseText
    });
});
```

Use this for observability, not as a replacement for feature-specific error handling.

A user-facing feature should still handle its own failures appropriately.

## Parameters explained

The global handler receives:

- `event` — the jQuery event object;
- `jqXHR` — the request/response object;
- `ajaxSettings` — the effective Ajax settings for the request;
- `thrownError` — an error value supplied by the failure path when available.

During debugging, useful fields often include:

```js
$(document).ajaxError(function (event, xhr, settings, error) {
    console.groupCollapsed("[Ajax error]", settings.type, settings.url);
    console.log("status:", xhr.status);
    console.log("statusText:", xhr.statusText);
    console.log("responseJSON:", xhr.responseJSON);
    console.log("responseText:", xhr.responseText);
    console.log("error:", error);
    console.groupEnd();
});
```

## What not to log

Production logging should avoid exposing:

- passwords;
- authentication tokens;
- session identifiers;
- personal or financial data;
- entire response bodies containing sensitive information.

Global diagnostics are best for detecting patterns. Feature-level code should still translate failures into an appropriate user experience and decide whether retrying is safe.

---

# 47. Deferreds and Promise-Like Behavior

jQuery Deferreds are an older asynchronous abstraction used heavily by Ajax APIs.

Example:

```js
const request = $.get("/api/user");

request
    .done(function (data) {
        console.log("success", data);
    })
    .fail(function (xhr) {
        console.error("failed", xhr.status);
    });
```

## Important jQuery 4 slim-build note

The jQuery 4 **slim** build removes Deferreds and Callbacks along with Ajax/effects-related omissions.

Do not debug Deferred-based code for hours before confirming which jQuery build is loaded.

## Native Promise interoperability

Modern applications increasingly use native `Promise`, `fetch()`, and `async/await`.

When maintaining jQuery code, be careful not to assume every jqXHR detail is identical to a native `Promise`.

---

# 48. Debugging `$.when()`

Example:

```js
$.when(
    $.get("/api/user"),
    $.get("/api/permissions")
)
.done(function (userResult, permissionResult) {
    console.log(userResult);
    console.log(permissionResult);
})
.fail(function () {
    console.error("At least one request failed");
});
```

When debugging:

- inspect each individual request
- add `.fail()` to each request temporarily if needed
- verify which operation rejected
- do not assume the first listed request failed

For new code, evaluate whether native `Promise.all()` is more suitable, especially outside legacy jQuery architecture.

## What `$.when()` is for

`$.when()` coordinates one or more Deferred/jqXHR-like values and runs success logic when all required operations resolve.

With multiple jqXHR values, each `.done()` argument represents that request's resolution tuple rather than only the response body.

For Ajax requests you may see:

```js
.done(function (userResult, permissionResult) {
    const userData = userResult[0];
    const userStatus = userResult[1];
    const userXhr = userResult[2];
});
```

That shape is a common source of confusion.

## Failure behavior

If any coordinated operation rejects, the combined `.fail()` path runs. Other requests may still be in flight; `$.when()` does not automatically cancel them.

## Slim-build warning

jQuery 4's slim build omits Deferred-related functionality, so legacy code relying on `$.when()` belongs on the full build or should be migrated to an appropriate native Promise design.

## Native comparison

`Promise.all()` is often the clearer choice for new non-jQuery asynchronous code, but jqXHR values and native Promises are not identical APIs. Test callback values and error behavior when migrating rather than replacing syntax mechanically.

---

# 49. Async Error Handling Mistakes

Wrong mental model:

```js
let result;

$.get("/api/data", function (data) {
    result = data;
});

console.log(result);
```

Possible output:

```text
undefined
```

Why?

The console line runs before the network request finishes.

## Correct: use the callback

```js
$.get("/api/data")
    .done(function (data) {
        console.log(data);
    });
```

## Modern wrapper example

If appropriate in your codebase:

```js
function getData() {
    return $.get("/api/data");
}

getData().done(function (data) {
    render(data);
});
```

The key idea is:

> asynchronous values must be consumed after they become available.

---

# 50. Debugging Animations

Example:

```js
$("#panel").fadeIn();
```

If it fails:

1. verify the element exists
2. verify full jQuery build is loaded
3. check current `display`
4. check parent visibility
5. check queued animations
6. inspect CSS transitions/animations
7. inspect whether code immediately hides it again

## Debug

```js
const $panel = $("#panel");

console.log({
    matches: $panel.length,
    display: $panel.css("display"),
    visible: $panel.is(":visible")
});
```

## What jQuery effects change

Effects such as `.fadeIn()`, `.fadeOut()`, `.slideUp()`, `.slideDown()`, and `.animate()` repeatedly change style values over time. They therefore depend on:

- the effects module being present;
- a non-empty jQuery selection;
- a meaningful start/end state;
- CSS that does not immediately override or hide the result;
- the animation queue not being blocked by older work.

## Inspect whether an element is currently animated

```js
console.log($("#panel").is(":animated"));
```

If the value remains `true` unexpectedly, inspect the queue:

```js
console.log($("#panel").queue("fx"));
```

## Prefer state changes when CSS owns presentation

For many modern interfaces, a class plus CSS transition is easier to debug:

```js
$("#panel").addClass("is-open");
```

```css
#panel {
  opacity: 0;
  transition: opacity 200ms ease;
}

#panel.is-open {
  opacity: 1;
}
```

Use jQuery effects when they fit the existing application, but do not introduce JavaScript animation solely because jQuery can animate a property.

### Accessibility note

If motion is decorative, consider a reduced-motion design. Debug with the operating system/browser reduced-motion preference enabled so important UI behavior does not depend on animation completing visibly.

---

# 51. Animation Queues

Repeated hover/click events can queue animations:

```js
$("#menu").hover(
    function () {
        $(this).slideDown();
    },
    function () {
        $(this).slideUp();
    }
);
```

Rapid interactions may produce a backlog.

Common pattern:

```js
$(this).stop(true, true).slideDown();
```

Understand the effect of `.stop()` before using it blindly.

Possible debugging question:

> Is the animation wrong, or is an old queued animation still running?

## The default `fx` queue

Most jQuery effects use the queue named `fx`. If five animations are started before the first finishes, later ones normally wait.

Inspect it:

```js
const $menu = $("#menu");

console.log($menu.queue("fx").length);
```

A growing number during rapid mouse movement is a strong clue that the visual lag comes from queued work rather than from the final CSS value.

## Understanding `.stop()`

A common signature is:

```js
$menu.stop(clearQueue, jumpToEnd);
```

- `clearQueue` — when `true`, removes animations waiting in the queue;
- `jumpToEnd` — when `true`, completes the current animation immediately at its end state.

Examples:

```js
$menu.stop(true, false); // stop current work and discard queued effects
$menu.stop(true, true);  // discard queue and jump current effect to its end
```

The second form can fire completion behavior sooner than expected, so choose it intentionally.

## When not to "fix" with `.stop(true, true)`

If the real bug is duplicate event handlers, fixing only the animation queue hides the cause. Use `console.count()` inside the event handler to confirm how many times the event logic starts.

---

# 52. Plugin Debugging

A jQuery plugin commonly extends:

```js
$.fn
```

Example:

```js
$.fn.highlight = function () {
    return this.addClass("highlight");
};
```

Then:

```js
$(".item").highlight();
```

When a plugin fails, verify:

- jQuery loaded first
- plugin loaded second
- initialization loaded after both
- plugin version supports your jQuery version
- plugin CSS loaded if required
- required dependencies loaded
- selector matched
- expected HTML structure exists
- initialization options are valid

## How a typical jQuery plugin works

A plugin adds a method to `$.fn`, the prototype used by jQuery objects:

```js
$.fn.highlight = function (options) {
    const settings = $.extend({
        className: "highlight"
    }, options);

    return this.each(function () {
        $(this).addClass(settings.className);
    });
};
```

Usage:

```js
$(".item").highlight({
    className: "important"
});
```

Here:

- input is the selected jQuery collection plus any plugin options;
- the plugin processes each matched element;
- returning `this` preserves jQuery method chaining.

## Fast capability checks

Before debugging plugin options, verify that the method exists:

```js
console.log("jQuery:", $.fn.jquery);
console.log("plugin:", typeof $.fn.highlight);
console.log("matches:", $(".item").length);
```

Expected for a loaded plugin:

```text
plugin: "function"
```

## Plugin lifecycle problems

Many plugins have separate operations such as initialize, refresh/update, and destroy/dispose. Reinitializing a plugin on the same node can create:

- duplicate DOM wrappers;
- duplicate event handlers;
- extra timers;
- memory leaks.

Use the plugin's documented lifecycle API rather than guessing at cleanup.

### When the selector matches but the plugin still fails

Inspect the HTML structure the plugin expects. A plugin can be loaded correctly but fail because required child elements, attributes, data options, or CSS are missing.

---

# 53. `$.fn.pluginName is not a function`

Typical error:

```text
TypeError: $(...).datepicker is not a function
```

Potential causes:

### 1. Plugin JS missing

Check Network panel.

### 2. Wrong script order

Wrong:

```html
<script src="plugin.js"></script>
<script src="jquery.js"></script>
```

Correct:

```html
<script src="jquery.js"></script>
<script src="plugin.js"></script>
```

### 3. Multiple jQuery copies

Plugin may attach to one instance while `$` later points to another.

Check:

```js
console.log($.fn.jquery);
console.log(typeof $.fn.datepicker);
```

### 4. Plugin script threw during loading

Look for earlier errors.

### 5. Plugin removed support for your environment

Read the plugin's official compatibility notes.

---

# 54. `$ is not defined` and `$ is not a function`

## `$ is not defined`

Likely jQuery not loaded or `$` not globally available.

Check:

```js
typeof jQuery
typeof $
```

## `$ is not a function`

Another library may own `$`, or `$` may have been overwritten.

Example accidental overwrite:

```js
const $ = "price";
```

Then:

```js
$("#box");
```

fails.

## Debug

```js
console.log($);
console.log(typeof $);
console.log(window.jQuery);
```

## Distinguish the two errors

These errors point to different stages:

| Error | Meaning |
|---|---|
| `$ is not defined` | No variable named `$` is visible in the current scope. |
| `$ is not a function` | `$` exists, but its current value is not callable as jQuery. |

Run:

```js
console.table({
    dollarType: typeof window.$,
    jqueryType: typeof window.jQuery,
    sameObject: window.$ === window.jQuery
});
```

If `window.jQuery` is a function but `$` is missing/different, investigate `noConflict()` or another library.

If both are missing, investigate loading order, failed script requests, CSP, bundler scope, or an earlier syntax error.

## Module scope matters

In bundled code this may work:

```js
import $ from "jquery";
```

while this is still `undefined`:

```js
window.$
```

That is not necessarily a bug. It becomes a problem only when legacy code/plugins require a global jQuery variable.

## Common bad fix

Do not create a random global alias before knowing which jQuery instance a plugin uses. A plugin attached to one instance will not automatically appear on a second instance.

---

# 55. `jQuery.noConflict()`

Some libraries also use `$`.

jQuery can release `$`:

```js
jQuery.noConflict();
```

Then use:

```js
jQuery("#box").hide();
```

A convenient scoped alias:

```js
jQuery(function ($) {
    $("#box").hide();
});
```

Inside that function, `$` refers to jQuery.

## Debugging clue

If `jQuery(...)` works but `$(...)` does not, check whether `noConflict()` is being used or another library owns `$`.

## What `noConflict()` changes

Calling:

```js
jQuery.noConflict();
```

releases jQuery's claim to the global `$` alias while leaving the global `jQuery` name available.

Store the returned jQuery reference if you want a private alias:

```js
const jq = jQuery.noConflict();

jq("#box").hide();
```

jQuery also supports a "deep" form:

```js
const jq = jQuery.noConflict(true);
```

This can restore both `$` and `jQuery` globals to values that existed before this jQuery copy loaded. Use it only when you understand why multiple global versions are present.

## Safe local alias

A common pattern is:

```js
(function ($) {
    $("#box").hide();
})(jQuery);
```

or the ready callback form already shown above.

This keeps `$` convenient inside a controlled scope without taking ownership of `$` globally.

### Debugging checklist

When `jQuery()` works but `$()` fails:

1. inspect `window.$`;
2. search for `noConflict`;
3. inspect script load order;
4. check whether another framework/library uses `$`;
5. confirm that plugins attach to the same jQuery instance your code calls.

---

# 56. Multiple jQuery Versions on One Page

Avoid this unless you have a strong compatibility requirement.

Example problem:

```html
<script src="jquery-4.js"></script>
<script src="plugin.js"></script>
<script src="jquery-3.js"></script>
```

The plugin may have attached itself to jQuery 4, while global `$` now points to jQuery 3.

Result:

```text
$(...).pluginName is not a function
```

## Detect script duplication

Inspect page source and Network requests for:

```text
jquery
```

Also log at different points:

```js
console.log($.fn.jquery);
```

## `noConflict(true)`

jQuery provides advanced support for restoring a previous global jQuery instance, but this should be treated as a compatibility technique rather than a normal architecture.

---

# 57. Debugging Third-Party Widgets

For datepickers, grids, editors, modal libraries, and legacy plugins, isolate layers:

```text
jQuery core
→ plugin JavaScript
→ plugin CSS
→ dependencies
→ required HTML
→ initialization
→ remote data
```

## Example checklist

```js
console.log("jQuery:", $.fn.jquery);
console.log("plugin exists:", typeof $.fn.somePlugin);
console.log("target count:", $(".widget").length);
```

Then check plugin initialization:

```js
try {
    $(".widget").somePlugin(options);
} catch (error) {
    console.error("Plugin initialization failed", error);
}
```

Do not catch and ignore errors permanently. The `try/catch` above is for diagnosis.

---

# 58. jQuery Migrate

jQuery Migrate helps identify compatibility problems when upgrading old jQuery code.

It can:

- produce migration warnings
- temporarily restore certain deprecated behavior
- help locate old APIs
- make upgrade work more systematic

Use the **uncompressed development version** while fixing warnings.

Do not treat Migrate as a permanent excuse to leave every warning unfixed.

## Migration strategy

Typical high-level path:

```text
old jQuery
→ compatible latest release in that major line
→ appropriate Migrate version
→ fix warnings
→ remove Migrate
→ upgrade next major version
→ repeat
```

For moving jQuery 3.x to 4.x, use the official jQuery 4 upgrade guidance and Migrate 4.x.

---

# 59. Debugging jQuery 4 Upgrade Problems

jQuery 4 removes several previously deprecated APIs and changes some behaviors.

When an application breaks after upgrading:

1. confirm exact old version
2. confirm exact new version
3. install/use jQuery Migrate for the intended upgrade stage
4. inspect Console warnings
5. update third-party plugins
6. search project for removed APIs
7. test event behavior
8. test Ajax paths
9. test selectors
10. test focus/blur behavior
11. test HTML parsing/insertion
12. test custom plugins
13. test old browser requirements

Do not upgrade core and ten plugins at the same time if you can avoid it. Incremental changes make regressions easier to isolate.

## High-risk jQuery 4 changes to test explicitly

The official 4.0 upgrade guidance identifies changes that are easy to miss during a large migration. In addition to removed deprecated APIs, test code that depends on:

- JSON-to-JSONP auto-promotion;
- Ajax script execution without `dataType: "script"`;
- old `toggleClass(boolean/undefined)` behavior;
- unitless numeric CSS values that previously gained `px` automatically;
- legacy custom selector pseudos;
- focus/focusin/blur/focusout ordering;
- package/bundler entry points;
- the slimmer slim build.

A migration bug can therefore be behavioral even when no method is "missing".

## Practical migration worksheet

Record these before changing anything:

```text
Current core version:
Target core version:
Migrate version:
jQuery UI version:
Plugin list + versions:
Supported browsers:
Full or slim build:
Bundler/CDN/script-tag loading:
```

Then upgrade one layer at a time and keep a reproducible test case for every regression.

### Important distinction

jQuery Migrate 4.x focuses on changes relevant to moving from jQuery 3.x to jQuery 4.x. Very old 1.x/2.x applications may need staged migration using the earlier Migrate line before the 4.x step.

---

# 60. Removed and Deprecated APIs

Legacy jQuery code may use APIs that are deprecated or removed.

Examples you may encounter:

```js
$.parseJSON(...)
$.trim(...)
$.type(...)
$.now()
.live(...)
.bind(...)
.delegate(...)
```

Some were deprecated long ago and later removed.

## Modern replacements vary

### `$.parseJSON`

Legacy:

```js
const value = $.parseJSON(text);
```

Modern:

```js
const value = JSON.parse(text);
```

### `.live()`

Legacy:

```js
$(".delete").live("click", handler);
```

Modern delegated pattern:

```js
$(document).on("click", ".delete", handler);
```

Prefer a closer stable ancestor instead of `document` when possible:

```js
$("#rows").on("click", ".delete", handler);
```

### `.bind()`

Legacy:

```js
$("#save").bind("click", handler);
```

Modern:

```js
$("#save").on("click", handler);
```

## Debugging rule

When seeing an unknown legacy method:

1. check the official API
2. confirm when it was deprecated
3. confirm whether it was removed
4. identify the recommended replacement
5. test behavior, not just syntax

## jQuery 4 removals vs older removals

Do not assume every legacy API in an old codebase was removed specifically by jQuery 4.

For example, `.live()` disappeared much earlier, while jQuery 4 removed a separate group of long-deprecated helpers such as:

```text
jQuery.isArray
jQuery.isFunction
jQuery.isNumeric
jQuery.isWindow
jQuery.now
jQuery.parseJSON
jQuery.trim
jQuery.type
```

The jQuery 4 upgrade guide also lists internal/less-common removals. The exact migration depends on which API your application actually uses.

## Replacement examples

```js
// jQuery 3-era helper
const isArray = $.isArray(value);

// native
const isArray = Array.isArray(value);
```

```js
// legacy
const now = $.now();

// native
const now = Date.now();
```

```js
// legacy
const trimmed = $.trim(value);

// native
const trimmed = String(value).trim();
```

### Do not perform blind search-and-replace

A native replacement can differ at edge cases. Add a focused test around existing application inputs before mass replacement, especially for type checks and code that accepted unusual values.

---

# 61. Security Debugging

Security bugs often look like ordinary rendering bugs.

Review code paths where external data reaches:

- `.html()`
- `.append()`
- `.prepend()`
- `.before()`
- `.after()`
- dynamic script execution
- URL construction
- attributes
- event handler attributes
- plugin HTML templates

Ask:

> Can an untrusted value become executable HTML or JavaScript?

## Think in sources and sinks

A useful security-debugging model is:

```text
untrusted source
      ↓
validation / transformation
      ↓
dangerous or safe sink
```

Possible **sources** include query-string values, form input, API responses containing user-authored data, database content, and `postMessage` data.

Potentially dangerous **sinks** include HTML insertion, script execution, event-handler attributes, and URL/navigation construction.

The key question is not merely "did this value come from my server?" Data stored in your own database may still have originally come from an untrusted user.

## Context matters

The safe handling for text is different from the safe handling for a URL, CSS, an HTML attribute, or intentional rich HTML.

For plain text, prefer text APIs:

```js
$("#message").text(untrustedValue);
```

For rich HTML, use a well-reviewed sanitization approach designed for HTML. Do not rely on escaping or regex snippets copied without understanding the output context.

## Debugging security defects

1. identify the exact untrusted input;
2. trace every transformation;
3. identify where it reaches the DOM/network;
4. inspect the browser's resulting DOM, not only the source string;
5. verify CSP/Trusted Types behavior if your application uses them;
6. add a regression test for the unsafe input.

Security fixes should remove or constrain the dangerous path rather than merely hide the visible payload.

---

# 62. XSS and Unsafe HTML Insertion

Risky:

```js
const name = getValueFromUser();

$("#welcome").html("<p>Welcome " + name + "</p>");
```

If `name` contains hostile markup, it may create an XSS path.

Safer composition:

```js
const $p = $("<p>").text("Welcome " + name);

$("#welcome").empty().append($p);
```

Or:

```js
$("#welcome").text("Welcome " + name);
```

Use HTML sanitization when your application intentionally permits a controlled subset of user-authored HTML.

Do not invent a regex-based HTML sanitizer.

## `.text()` vs HTML insertion

When the goal is to display characters literally:

```js
$("#result").text('<img src=x onerror="alert(1)">');
```

the markup is inserted as text, not interpreted as an element.

By contrast:

```js
$("#result").html('<strong>Approved HTML</strong>');
```

asks the browser/jQuery DOM machinery to treat the string as HTML.

## Safer structured construction

Build fixed markup with DOM/jQuery APIs and place untrusted values only in text positions:

```js
const $row = $("<div>").addClass("user-row");
const $name = $("<span>").addClass("user-name").text(user.name);

$row.append($name);
$("#users").append($row);
```

This makes the trust boundary visible in code review.

## Common mistake: sanitizing too early

If an application sanitizes a string, then later concatenates new untrusted content into it, the final result is not automatically safe. Treat sanitization as part of the final context-sensitive rendering path.

### What not to do

Do not create an "HTML sanitizer" from a blacklist such as:

```js
html.replace(/<script.*?>.*?<\/script>/gi, "")
```

XSS has many execution paths beyond literal `<script>` tags.

---

# 63. Debugging Performance Problems

Common jQuery performance issues include:

- repeatedly querying the same DOM node
- huge delegated event roots
- handlers attached to thousands of elements unnecessarily
- repeated layout reads/writes
- frequent DOM insertion inside loops
- excessive animation
- expensive selectors executed continuously
- scroll/resize handlers doing heavy work
- memory leaks from long-lived handlers
- updating DOM for every item instead of batching

## Cache repeated selections

Less efficient:

```js
$("#total").text(calculate());
$("#total").addClass("ready");
$("#total").show();
```

Better:

```js
const $total = $("#total");

$total
    .text(calculate())
    .addClass("ready")
    .show();
```

Do not over-optimize a selector used once. Measure first.

---

# 64. Layout Thrashing and Repeated DOM Work

Code that repeatedly reads layout and writes layout can trigger expensive recalculation.

Example conceptually:

```js
$(".row").each(function () {
    const width = $(this).width();
    $(this).width(width + 10);
});
```

On large pages, repeated layout-dependent reads/writes may become expensive.

Better approaches can include:

- calculating in batches
- using CSS classes
- using flex/grid
- minimizing synchronous measurements
- using browser Performance tools to confirm bottlenecks

Performance debugging should be evidence-driven.

## Read/write pattern that causes trouble

Layout-sensitive reads can include operations such as:

```js
$el.width()
$el.height()
$el.offset()
$el.position()
element.getBoundingClientRect()
```

Style/DOM writes include:

```js
$el.css(...)
$el.addClass(...)
$el.append(...)
$el.width(value)
```

Repeatedly alternating a read that requires fresh layout with a write that invalidates layout can force the browser to recalculate geometry many times.

## Batch when practical

Instead of reading and writing every item interleaved, separate measurement from mutation:

```js
const measurements = $(".row").map(function () {
    return $(this).width();
}).get();

$(".row").each(function (index) {
    $(this).width(measurements[index] + 10);
});
```

This is an illustration, not a guarantee of optimal performance; browser engines optimize many cases. Confirm with the Performance panel before refactoring.

## Better question

Do not ask "How do I make jQuery faster?" Ask:

> Which specific operation dominates this interaction, and can CSS/layout or batched DOM work remove it?

---

# 65. Memory Leaks and Cleanup

Long-lived pages can accumulate:

- window/document event handlers
- timers
- references to detached DOM
- plugin instances
- subscriptions
- cached data
- repeated modal initialization

## Namespaced cleanup

```js
function mountDashboard() {
    $(window).on("resize.dashboard", refreshDashboard);
}

function unmountDashboard() {
    $(window).off(".dashboard");
}
```

For plugins, use their official destroy/dispose API when one exists.

Do not assume removing DOM automatically performs every third-party cleanup operation.

## jQuery cleanup vs external resources

jQuery's own removal APIs can clean jQuery-managed data/events for removed nodes, but your component may own resources jQuery cannot infer, such as:

- `setInterval`/`setTimeout`;
- `requestAnimationFrame`;
- native `addEventListener` handlers attached elsewhere;
- observers;
- WebSocket/subscription callbacks;
- third-party plugin instances.

Track those resources explicitly.

## `.remove()` and `.detach()` differ

When debugging disappearing/reappearing widgets, remember:

- `.remove()` removes matched elements and is intended to discard their jQuery data/events;
- `.detach()` removes them while preserving jQuery data/events so they can be reinserted.

Using `.detach()` indefinitely for elements that will never return can retain more state than intended.

## Component teardown checklist

```text
Unbind namespaced events
Clear timers
Abort obsolete requests where useful
Destroy plugin instances
Disconnect observers/subscriptions
Remove or release DOM references
```

Use the browser Memory panel and repeated mount/unmount testing when a long-lived single-page screen grows over time.

---

# 66. Logging Patterns That Scale

Avoid unstructured logs like:

```js
console.log("here");
console.log("here2");
console.log("test");
```

Prefer meaningful context:

```js
console.log("[OrderForm] submit started", {
    orderId,
    total,
    itemCount: items.length
});
```

Useful console methods:

```js
console.log()
console.info()
console.warn()
console.error()
console.table()
console.group()
console.groupCollapsed()
console.groupEnd()
console.count()
console.time()
console.timeEnd()
console.trace()
```

## Example

```js
console.groupCollapsed("[UserSearch] response");
console.log("query:", query);
console.log("status:", xhr.status);
console.table(data.users);
console.groupEnd();
```

## Log transitions, not noise

Useful debugging logs answer:

```text
What operation started?
With which identifier/input?
Which branch did it take?
How long did it take?
How did it end?
```

Example:

```js
console.time("[OrderForm] submit");

console.info("[OrderForm] submit", {
    orderId,
    itemCount: items.length
});

saveOrder()
    .always(function () {
        console.timeEnd("[OrderForm] submit");
    });
```

## Add correlation IDs when requests overlap

```js
const requestId = crypto.randomUUID();

console.log("[Search]", requestId, "started", query);
```

Carry the same ID into success/failure logs so stale-response problems are easier to see.

## Production caution

Never log secrets merely because DevTools is convenient. Avoid tokens, passwords, raw cookies, payment data, and unnecessary personal data. Prefer small structured fields that are enough to reconstruct the control flow.

---

# 67. Reusable Debug Helpers

## Assert selector count

```js
function debugSelection(label, selector) {
    const $items = $(selector);

    console.log(label, {
        selector,
        count: $items.length,
        items: $items.toArray()
    });

    return $items;
}

const $save = debugSelection("Save button", "#save");
```

## Ajax failure formatter

```js
function logAjaxFailure(label, xhr, textStatus, errorThrown) {
    console.error(label, {
        status: xhr.status,
        statusText: xhr.statusText,
        textStatus,
        errorThrown,
        responseText: xhr.responseText,
        responseJSON: xhr.responseJSON
    });
}
```

Usage:

```js
$.ajax({
    url: "/api/order"
})
.fail(function (xhr, textStatus, errorThrown) {
    logAjaxFailure("Order request failed", xhr, textStatus, errorThrown);
});
```

## Timing helper

```js
function measure(label, fn) {
    console.time(label);

    try {
        return fn();
    } finally {
        console.timeEnd(label);
    }
}
```

---

# 68. Debugging Production Minified Code

Production bundles may look like:

```js
!function(a){a("#x").on("click",function(){...})}(jQuery);
```

Strategies:

1. reproduce in development build
2. use source maps if available
3. pretty-print minified code in DevTools
4. inspect stack trace
5. add release/version metadata
6. compare deployed files with expected build
7. confirm cache/CDN version
8. preserve useful server request IDs

Never edit a minified production file directly as your normal source-of-truth workflow.

Fix source code and rebuild.

## Confirm you are debugging the deployed artifact

Production-only bugs frequently come from version mismatch rather than minification itself.

Record:

```text
application release/build ID
script URL
response ETag/hash
jQuery version/build
source-map availability
API base URL
```

Then compare those values with the release you believe is deployed.

## Use pretty-print as a fallback

DevTools can format a one-line minified file to make control flow easier to inspect. Pretty-printing improves readability but does not restore original variable names or module boundaries.

Source maps are preferable when trustworthy maps exist.

## Conditional breakpoints and exception pausing

When logs are hard to add to production, use:

- pause on uncaught exceptions;
- conditional breakpoints;
- XHR/fetch breakpoints;
- event-listener breakpoints;
- DOM mutation breakpoints.

These tools can isolate the path without editing production assets.

### Preserve evidence before forcing reloads

If the failure is intermittent, capture the console, Network request/response metadata, stack trace, and release ID before clearing caches or reloading. A refresh can destroy the best evidence.

---

# 69. Source Maps

Source maps help DevTools map minified/compiled output back to original source.

Official jQuery distributions provide source-map assets even though source maps may not be automatically referenced by all compressed releases.

For your own application bundles, configure your build system intentionally.

Security and deployment policy may affect whether production source maps are public.

During debugging, source maps can make stack traces dramatically easier to understand.

## What a source map contains

A source map describes how generated JavaScript locations correspond to original source locations. It does **not** change runtime behavior; it changes the debugging view.

Without a source map, an error may point to:

```text
app.min.js:1:48217
```

With a valid map, DevTools may show the original module/file and line instead.

## Debugging a missing source map

Check:

1. whether the `.map` file exists;
2. whether the minified file references it with a `sourceMappingURL` comment or the server/browser provides another mapping mechanism;
3. whether DevTools source-map support is enabled;
4. whether deployment rewrote paths;
5. whether the map is intentionally withheld in production.

A 404 for a source map normally affects debugging quality rather than the execution of the minified JavaScript itself.

## Security consideration

Source maps can reveal readable application source, comments, paths, or other implementation details. Decide deliberately whether production maps are public, access-controlled, uploaded only to an error-monitoring service, or omitted.

---

# 70. Testing jQuery Code

Testing catches regressions that manual debugging may miss.

Good test candidates:

- selector-dependent behavior
- form validation
- button state
- event delegation
- DOM rendering
- Ajax success/failure handling
- plugin initialization
- utility functions
- parsing and transformation
- upgrade regressions

Keep business logic separated from DOM manipulation when possible.

Instead of embedding every rule inside an event handler:

```js
$("#discount").on("click", function () {
    const price = Number($("#price").val());

    if (price > 1000) {
        $("#result").text(price * 0.9);
    } else {
        $("#result").text(price);
    }
});
```

extract logic:

```js
function calculateDiscount(price) {
    return price > 1000 ? price * 0.9 : price;
}
```

This function is easier to unit-test.

---

# 71. QUnit Basics for jQuery Projects

QUnit is historically associated with the jQuery ecosystem and remains useful for JavaScript unit testing.

Conceptual example:

```js
QUnit.module("calculateDiscount");

QUnit.test("applies 10% discount over 1000", function (assert) {
    const result = calculateDiscount(2000);

    assert.equal(result, 1800);
});
```

DOM behavior test idea:

```js
QUnit.test("save click updates message", function (assert) {
    const $fixture = $("#qunit-fixture");

    $fixture.html(`
        <button id="save">Save</button>
        <div id="message"></div>
    `);

    $("#save").on("click", function () {
        $("#message").text("Saved");
    });

    $("#save").trigger("click");

    assert.equal($("#message").text(), "Saved");
});
```

Use a test fixture so tests do not permanently pollute the page.

---

# 72. Building a Minimal Reproduction

When a bug is confusing, reduce it.

Original application may contain:

```text
30 scripts
12 plugins
framework template
Ajax
authentication
CSS framework
analytics
hundreds of DOM nodes
```

Create:

```html
<!doctype html>
<html>
<head>
    <meta charset="utf-8">
    <title>Bug reproduction</title>
</head>
<body>
    <button id="save">Save</button>

    <script src="jquery.js"></script>
    <script>
        $("#save").on("click", function () {
            console.log("clicked");
        });
    </script>
</body>
</html>
```

Then gradually add the behavior required to reproduce the bug.

This tells you whether the cause is:

- jQuery itself
- your code
- a plugin
- CSS
- backend
- integration between components

---

# 73. Common Real-World Debugging Scenarios

This section acts as a practical troubleshooting playbook.

## Scenario 1: Click handler never runs

Code:

```js
$("#save").on("click", function () {
    console.log("clicked");
});
```

Debug:

```js
console.log($("#save").length);
```

If output is:

```text
0
```

check selector and timing.

If element is inserted later, use delegation:

```js
$(document).on("click", "#save", function () {
    console.log("clicked");
});
```

Prefer a stable closer ancestor when available.

---

## Scenario 2: Click handler runs twice

Add:

```js
console.count("save");
```

If one click increments twice, look for:

- initialization called twice
- modal open callback rebinding
- SPA partial load rebinding
- both direct and delegated handler
- duplicate script inclusion

Use namespaced binding if re-initialization is expected:

```js
$("#save")
    .off("click.order")
    .on("click.order", handleSave);
```

---

## Scenario 3: Ajax success handler never runs

Add failure handling:

```js
$.ajax({
    url: "/api/users"
})
.done(function (data) {
    console.log("success", data);
})
.fail(function (xhr, status, error) {
    console.error({
        httpStatus: xhr.status,
        status,
        error,
        response: xhr.responseText
    });
});
```

Then inspect Network.

---

## Scenario 4: `Unexpected token '<'`

Inspect:

```js
xhr.responseText
```

Likely the server returned HTML instead of JSON.

Examples:

- login page
- 404 page
- PHP warning page
- server exception page

Fix the response at the source.

---

## Scenario 5: `.val()` gives wrong calculation

```js
const qty = $("#qty").val();
const price = $("#price").val();

console.log(qty * price);
```

Multiplication converts numeric strings, but addition does not behave the same:

```js
console.log(qty + price);
```

Could concatenate strings.

Convert intentionally:

```js
const qty = Number($("#qty").val());
const price = Number($("#price").val());
```

---

## Scenario 6: Checkbox always appears checked

Wrong:

```js
if ($("#agree").attr("checked")) {
    // ...
}
```

For current state:

```js
if ($("#agree").prop("checked")) {
    // ...
}
```

---

## Scenario 7: Newly added button has no click behavior

Direct binding happened before insertion.

Fix:

```js
$("#list").on("click", ".remove", function () {
    // ...
});
```

---

## Scenario 8: Plugin method missing

Error:

```text
$(...).select2 is not a function
```

Check:

```js
console.log("jquery", $.fn.jquery);
console.log("select2", typeof $.fn.select2);
```

Then inspect script order and duplicate jQuery loads.

---

## Scenario 9: `$` suddenly stops working

Check:

```js
console.log(typeof $);
console.log(typeof jQuery);
```

If `jQuery` works but `$` does not, inspect `noConflict()` or another library.

---

## Scenario 10: Element exists but UI does not change

After:

```js
$("#panel").addClass("open");
```

check:

```js
console.log($("#panel").hasClass("open"));
```

If true, move to CSS debugging.

---

## Scenario 11: Ajax works in GET but not POST

Inspect:

- CSRF
- route method
- payload format
- authentication
- request Content-Type
- validation response
- CORS preflight
- server logs

A 405 suggests the route may not permit POST.

---

## Scenario 12: Ajax works locally but fails in production

Compare:

- URL base paths
- HTTPS vs HTTP
- CORS
- reverse proxy rules
- authentication cookies
- SameSite cookies
- CSP
- CSRF
- cache
- environment variables
- API host
- deployed jQuery build
- minified bundle version

Do not assume production has the same document base URL or backend path.

---

## Scenario 13: Modal handler accumulates each time modal opens

Problem:

```js
function openModal() {
    $("#modalSave").on("click", saveModal);
    $("#modal").show();
}
```

Every open can bind again.

Better:

```js
function initModal() {
    $("#modalSave").on("click.modal", saveModal);
}
```

Call initialization once.

Or controlled rebind:

```js
$("#modalSave")
    .off("click.modal")
    .on("click.modal", saveModal);
```

---

## Scenario 14: `.data()` does not show updated attribute

You changed:

```js
$("#item").attr("data-status", "done");
```

but read:

```js
$("#item").data("status");
```

Debug both:

```js
console.log($("#item").attr("data-status"));
console.log($("#item").data("status"));
```

Pick consistent semantics.

---

## Scenario 15: Fade method is undefined

Check whether you loaded:

```text
jquery.slim...
```

If yes, effects are omitted.

Use full jQuery or implement the behavior with CSS classes/transitions.

---

## Scenario 16: `$.ajax is not a function`

First suspect:

- slim build
- `$` is not jQuery
- malformed/partial library load
- jQuery overwritten

Debug:

```js
console.log(typeof $);
console.log($.fn && $.fn.jquery);
console.log(typeof $.ajax);
```

---

## Scenario 17: Form serializer misses checkbox

Only successful controls are serialized.

Check:

- checkbox is checked
- input has a `name`
- input is not disabled
- control belongs to expected form

Debug:

```js
console.table($("#form").serializeArray());
```

---

## Scenario 18: Button click submits form and reloads page

Inside a form:

```html
<button id="preview">Preview</button>
```

A button may act as a submit button depending on markup/default behavior.

Use:

```html
<button type="button" id="preview">Preview</button>
```

or intentionally handle form submission.

---

## Scenario 19: `this` is wrong in click handler

Problem:

```js
$(".item").on("click", () => {
    console.log(this);
});
```

Use:

```js
$(".item").on("click", function () {
    console.log(this);
});
```

Or:

```js
$(".item").on("click", (event) => {
    console.log(event.currentTarget);
});
```

---

## Scenario 20: Old code breaks after jQuery 4 upgrade

Check:

- Console
- jQuery Migrate warnings
- removed methods
- old plugins
- selector behavior
- focus/blur assumptions
- Ajax/deferred assumptions
- exact loaded build

Search legacy patterns:

```text
.live(
.bind(
.delegate(
$.parseJSON(
$.trim(
$.type(
```

Then verify each replacement against official documentation.

---

## Scenario 21: CSS selector works in DevTools but not in code

Likely timing or DOM replacement.

Log at the exact time code executes:

```js
console.log("time:", Date.now());
console.log("count now:", $(".target").length);
```

The element might exist later but not at initialization time.

---

## Scenario 22: Response is correct but page still shows old data

Check:

- stale Ajax race
- cache
- DOM selector points to wrong row
- second render overwrites first
- frontend state remains old
- browser displays a different element
- duplicate IDs
- old response arrives later

Add request IDs or sequence numbers in logs.

---

## Scenario 23: Only some dynamically generated rows work

Inspect generated HTML for:

- duplicate IDs
- malformed nested tags
- missing classes
- incorrect data attributes
- event delegation root
- row-specific data

Avoid assigning the same `id` to many rows.

Use classes:

```html
<button class="edit">Edit</button>
```

and row data:

```html
<tr data-id="123">
```

---

## Scenario 24: `preventDefault()` does nothing

Check:

- did your handler run?
- are you preventing the correct event?
- is another navigation triggered manually?
- is a different element responsible?
- did code throw before `preventDefault()`?

Log:

```js
$("#link").on("click", function (event) {
    console.log("handler entered");
    event.preventDefault();
    console.log("defaultPrevented:", event.isDefaultPrevented());
});
```

---

## Scenario 25: A handler disappears after partial page refresh

If a framework or Ajax render replaces the element, direct handlers attached to the old node disappear with it.

Use delegation on a stable ancestor or reinitialize after the render.

---

## Scenario 26: Page works only after adding `setTimeout`

That is a warning sign.

Instead of:

```js
setTimeout(initPlugin, 1000);
```

find the actual dependency:

- DOM ready
- Ajax completion
- plugin script load
- modal shown event
- image load
- framework render completion

Fix synchronization at the event/source rather than guessing a delay.

---

## Scenario 27: JSON response has extra debug text

Expected:

```json
{"ok":true}
```

Actual:

```text
DEBUG START
{"ok":true}
```

The response is no longer valid JSON.

Remove debug output from the API response channel. Send diagnostics to server logs instead.

---

## Scenario 28: Ajax sends old form values

Possible causes:

- data captured before user changes fields
- cached variable reused
- wrong form selected
- duplicate IDs
- `.data()` used instead of current `.val()`

Read current values at submit time:

```js
$("#form").on("submit", function (event) {
    event.preventDefault();

    const payload = $(this).serialize();

    console.log(payload);
});
```

---

## Scenario 29: Event works on desktop but not touch interaction

Investigate:

- actual event being used
- overlay elements
- CSS pointer-events
- disabled states
- browser-specific behavior
- plugin compatibility

Prefer semantic controls such as `<button>` and appropriate click handling when possible.

---

## Scenario 30: UI freezes during large operation

Investigate Performance tools.

Possible causes:

- huge synchronous loop
- thousands of DOM writes
- repeated selector work
- layout recalculation
- large HTML parse
- expensive plugin rendering

Measure:

```js
console.time("render");

renderLargeTable();

console.timeEnd("render");
```

Then profile rather than guessing.

---

# 74. Debugging Decision Tree

Use this compact decision tree.

```text
Something is not working
|
+-- Is there a Console error?
|   |
|   +-- Yes -> fix the earliest relevant error first
|   |
|   +-- No
|
+-- Is jQuery loaded?
|   |
|   +-- No -> fix script/network/order/CSP
|   |
|   +-- Yes
|
+-- Is the correct jQuery version/build loaded?
|   |
|   +-- No -> fix dependency/build
|   |
|   +-- Yes
|
+-- Does the selector match?
|   |
|   +-- No -> selector/timing/DOM problem
|   |
|   +-- Yes
|
+-- Is an event expected?
|   |
|   +-- Yes -> log binding and firing
|       |
|       +-- dynamic element? -> consider delegation
|       +-- duplicate firing? -> inspect repeated binding
|
+-- Is Ajax involved?
|   |
|   +-- Yes -> inspect Network
|       |
|       +-- request not sent -> frontend flow
|       +-- 4xx -> request/auth/validation/routing
|       +-- 5xx -> backend/server
|       +-- 2xx but fail callback -> parsing/dataType
|       +-- correct response but wrong UI -> render/state/race
|
+-- DOM changed but UI looks wrong?
    |
    +-- inspect CSS/layout/visibility
```

---

# 75. Fast Troubleshooting Checklist

When jQuery code fails, check:

- [ ] Open Console and read the first relevant error.
- [ ] Check `typeof jQuery`.
- [ ] Check `$.fn.jquery`.
- [ ] Confirm full vs slim build.
- [ ] Confirm script order.
- [ ] Check Network for failed `.js` files.
- [ ] Check selector `.length`.
- [ ] Confirm DOM timing.
- [ ] Add a log inside the handler.
- [ ] Check whether the element is dynamically inserted/replaced.
- [ ] Check for duplicate handler binding.
- [ ] Check `this` vs arrow-function behavior.
- [ ] Inspect raw DOM in Elements.
- [ ] Check CSS visibility.
- [ ] If Ajax: inspect Network request.
- [ ] Check status code.
- [ ] Check request payload.
- [ ] Check response body.
- [ ] Check JSON validity.
- [ ] Check CORS/CSRF.
- [ ] Check race conditions.
- [ ] Check plugin existence in `$.fn`.
- [ ] Check duplicate jQuery versions.
- [ ] Check deprecated/removed APIs.
- [ ] Use jQuery Migrate for supported upgrade diagnostics.
- [ ] Reproduce in a minimal page.
- [ ] Verify the fix with the original failure case.
- [ ] Test nearby behavior for regressions.

---

# 76. Debugging Best Practices

## 1. Fix the earliest error first

Later errors may only be consequences.

## 2. Log values with labels

Bad:

```js
console.log(data);
```

Better:

```js
console.log("[Order] response data", data);
```

## 3. Check type as well as value

```js
console.log(value, typeof value);
```

## 4. Check selector counts

```js
console.log($(".row").length);
```

## 5. Prefer stable selectors

Use meaningful classes and `data-*` attributes rather than fragile DOM paths.

## 6. Keep initialization organized

```js
function initOrderPage() {
    bindOrderEvents();
    loadOrderData();
}
```

## 7. Name important event handlers

Easier debugging:

```js
function handleSaveClick(event) {
    // ...
}

$("#save").on("click.order", handleSaveClick);
```

## 8. Add failure paths for asynchronous work

Do not code only the happy path.

## 9. Avoid magic timeouts

Synchronize with real events or promises.

## 10. Separate business logic from DOM code

It improves testing and reasoning.

## 11. Use event namespaces in reusable modules/plugins

```js
.on("click.myWidget", ...)
.off(".myWidget")
```

## 12. Verify deployment artifacts

A bug may be caused by stale cache or the wrong file version, not source code.

## 13. Remove temporary noisy diagnostics before release

Keep structured observability where useful.

---

# 77. Common Anti-Patterns

## Blindly wrapping everything in `try/catch`

Bad:

```js
try {
    brokenCode();
} catch (e) {
}
```

This hides the bug.

Use error handling when you can actually handle or report the error.

## Huge delegated root for everything

```js
$(document).on("click", ".anything", handler);
```

Sometimes valid, but prefer a stable closer ancestor when available.

## Rebinding on every render

```js
function render() {
    // render DOM
    $(".edit").on("click", edit);
}
```

If `render()` runs many times, handlers may accumulate.

## Duplicate IDs

Wrong:

```html
<button id="edit">Edit</button>
<button id="edit">Edit</button>
```

Use a class:

```html
<button class="edit">Edit</button>
<button class="edit">Edit</button>
```

## Storing everything globally

```js
window.currentUser = ...
window.order = ...
window.data = ...
```

Global mutable state makes debugging harder.

## Using `.html()` for plain text

Prefer `.text()` for plain, untrusted strings.

## Using synchronous thinking for async work

Do not expect an Ajax result immediately after sending a request.

## Guessing with `setTimeout`

Fix the actual lifecycle dependency.

---

# 78. Beginner Practice Exercises

## Exercise 1: Fix selector

HTML:

```html
<button id="save">Save</button>
```

Broken:

```js
$(".save").on("click", function () {
    alert("Saved");
});
```

Goal: make the handler run.

Hint:

```js
console.log($(".save").length);
```

---

## Exercise 2: Convert string values

HTML:

```html
<input id="a" value="10">
<input id="b" value="20">
```

Broken:

```js
const total = $("#a").val() + $("#b").val();
```

Goal:

```text
30
```

not:

```text
1020
```

---

## Exercise 3: Dynamic button

Insert a button after page load and make its click handler work with delegation.

---

## Exercise 4: Checkbox

Use `.prop("checked")` to display the current checkbox state.

---

## Exercise 5: Ajax failure

Write a request that logs:

- status
- response body
- error text

in `.fail()`.

---

# 79. Intermediate Practice Exercises

## Exercise 1: Duplicate submission

Create a form where clicking submit quickly twice does not create duplicate frontend requests.

Also explain why backend idempotency may still be needed.

## Exercise 2: Search race condition

Create live search that ignores stale responses.

## Exercise 3: Plugin compatibility

Given:

```text
$(...).widget is not a function
```

write a diagnostic checklist and the console commands you would run.

## Exercise 4: Data cache confusion

Create an element with a `data-count` attribute, read it with `.data()`, mutate it with `.attr()`, then compare both values.

## Exercise 5: Namespaced events

Build a component with:

```js
mount()
unmount()
```

that attaches and correctly cleans up window events.

---

# 80. Advanced Debugging Challenges

## Challenge 1: Legacy upgrade

You have a jQuery 1.x application using:

- `.live()`
- `.bind()`
- `$.parseJSON()`
- an old modal plugin

Design a staged upgrade to modern jQuery without changing everything at once.

## Challenge 2: Intermittent stale UI

A user types quickly and an old response sometimes replaces the newest data.

Diagnose and fix the race.

## Challenge 3: Memory growth in dashboard

A SPA-like dashboard opens and closes modules repeatedly. Memory grows over time.

Investigate:

- event cleanup
- plugin destroy APIs
- timers
- detached DOM
- retained references

Use browser Memory and Performance tools.

## Challenge 4: Production-only failure

Development works, production fails with:

```text
$.ajax is not a function
```

Investigate build pipeline, CDN, asset fingerprint, cache, and accidental slim-build deployment.

## Challenge 5: Multiple jQuery copies

One plugin initializes, another says its method is missing.

Use runtime version checks and script inspection to determine whether plugins attached to different jQuery instances.

---

# 81. jQuery Debugging Cheat Sheet

## Version

```js
$.fn.jquery
```

## Is jQuery loaded?

```js
typeof jQuery
```

## What is `$`?

```js
typeof $
```

## Selector count

```js
$("#id").length
$(".class").length
```

## Inspect matched DOM nodes

```js
$(".item").toArray()
```

## Current checkbox state

```js
$("#check").prop("checked")
```

## Raw attribute

```js
$("#item").attr("data-id")
```

## jQuery data

```js
$("#item").data("id")
```

## Current value

```js
$("#input").val()
```

## Visible?

```js
$("#panel").is(":visible")
```

## Plugin installed?

```js
typeof $.fn.pluginName
```

## Ajax diagnostic

```js
$.ajax({
    url: "/api/test"
})
.done(function (data, status, xhr) {
    console.log("OK", xhr.status, data);
})
.fail(function (xhr, status, error) {
    console.error("FAIL", {
        httpStatus: xhr.status,
        status,
        error,
        response: xhr.responseText
    });
});
```

## Event diagnostic

```js
$(document).on("click.debug", "#save", function (event) {
    console.log("clicked", {
        target: event.target,
        currentTarget: event.currentTarget,
        delegateTarget: event.delegateTarget
    });
});
```

Remove:

```js
$(document).off(".debug");
```

## Timing

```js
console.log(document.readyState);
```

## Performance

```js
console.time("task");
doWork();
console.timeEnd("task");
```

## Count duplicate handler execution

```js
console.count("handler");
```

## Stack trace

```js
console.trace();
```

---

# 82. Final Debugging Workflow

When facing a real jQuery problem, use this sequence.

## Step 1 — Write the expected behavior

Example:

```text
When the user clicks Save, one POST request should be sent.
If successful, #message should display "Saved".
```

This makes success measurable.

## Step 2 — Reproduce consistently

Document exact actions.

```text
1. Open edit page
2. Change quantity to 3
3. Click Save once
4. Two POST requests appear
```

## Step 3 — Read Console

Fix earlier errors first.

## Step 4 — Verify jQuery

```js
typeof jQuery
$.fn.jquery
typeof $.ajax
```

The last check can reveal accidental slim-build usage in Ajax-heavy code.

## Step 5 — Verify selector

```js
$("#save").length
```

## Step 6 — Verify handler

```js
console.count("save handler");
```

## Step 7 — Inspect network if applicable

Confirm:

- URL
- method
- body
- status
- response

## Step 8 — Inspect state and types

```js
console.log({
    quantity,
    quantityType: typeof quantity
});
```

## Step 9 — Reduce the failing code

Split chains, remove unrelated plugins, isolate functions.

## Step 10 — Fix root cause

Do not hide the symptom with arbitrary delays or swallowed exceptions.

## Step 11 — Verify regression safety

Test:

- normal case
- empty input
- repeated click
- error response
- slow response
- dynamic DOM
- browser refresh
- back/forward navigation where relevant

## Step 12 — Add protection

Depending on the bug:

- a test
- an assertion
- a structured log
- a better selector
- namespaced cleanup
- error UI
- validation
- request sequencing
- migration cleanup

---

# 83. Official References

Use primary documentation when verifying version-sensitive behavior.

- jQuery website: https://jquery.com/
- jQuery API: https://api.jquery.com/
- jQuery 4.0 Upgrade Guide: https://jquery.com/upgrade-guide/4.0/
- jQuery Core Upgrade Guides: https://jquery.com/upgrade-guide/
- jQuery releases: https://releases.jquery.com/jquery/
- jQuery download page: https://jquery.com/download/
- jQuery 4.0.0 release announcement: https://blog.jquery.com/2026/01/17/jquery-4-0-0/
- `.on()`: https://api.jquery.com/on/
- `.off()`: https://api.jquery.com/off/
- `$.ajax()`: https://api.jquery.com/jQuery.ajax/
- `$.getJSON()`: https://api.jquery.com/jQuery.getJSON/
- `$.when()`: https://api.jquery.com/jQuery.when/
- `.data()`: https://api.jquery.com/data/
- `jQuery.noConflict()`: https://api.jquery.com/jQuery.noConflict/
- `jQuery.readyException()`: https://api.jquery.com/jQuery.readyException/
- Removed APIs: https://api.jquery.com/category/removed/

---


# 84. Debugging Traversal Methods

jQuery traversal lets you move through related DOM elements.

Common methods include:

```js
.find()
.children()
.parent()
.parents()
.closest()
.siblings()
.next()
.prev()
.filter()
.not()
.eq()
.first()
.last()
```

A traversal bug often happens because the developer has the wrong mental model of the DOM tree.

## Example HTML

```html
<div class="order" data-id="10">
    <div class="toolbar">
        <button class="delete">Delete</button>
    </div>

    <div class="details">
        <span class="status">Draft</span>
    </div>
</div>
```

Inside the delete handler:

```js
$(".delete").on("click", function () {
    const $order = $(this).closest(".order");

    console.log($order.data("id"));
});
```

Output:

```text
10
```

## Debug traversal step by step

If this returns nothing:

```js
$(this).closest(".order").find(".status").text("Deleted");
```

split it:

```js
const $button = $(this);
console.log("button", $button.length);

const $order = $button.closest(".order");
console.log("order", $order.length);

const $status = $order.find(".status");
console.log("status", $status.length);

$status.text("Deleted");
```

## Important principle

Traversal operates on the **actual DOM structure**, not the structure you think your server template generated.

Inspect the Elements panel.

Browsers may repair malformed HTML, especially table markup, and the final DOM may differ from source text.

---

# 85. `.each()` vs `$.each()`

These methods look similar but start from different kinds of values.

## jQuery collection `.each()`

```js
$(".row").each(function (index, element) {
    console.log(index, element);
});
```

Use it when iterating over a jQuery collection.

Inside a traditional function:

```js
$(this)
```

wraps the current DOM element.

## Utility `$.each()`

```js
const users = [
    { id: 1, name: "Asha" },
    { id: 2, name: "Ravi" }
];

$.each(users, function (index, user) {
    console.log(index, user.name);
});
```

## Common bug: argument order

Developers sometimes assume every iteration API uses the same callback argument order.

Verify the specific API instead of relying on memory.

## Early exit

With jQuery `.each()`, returning `false` can stop iteration.

```js
$(".row").each(function () {
    if ($(this).hasClass("target")) {
        return false;
    }
});
```

This is different from a normal `Array.prototype.forEach()`, where returning a value does not break the loop.

---

# 86. `.filter()`, `.not()`, `.is()`, and `.has()`

These methods answer different questions.

## `.filter()`

Keep matching elements:

```js
const $enabled = $(".item").filter(".enabled");
```

## `.not()`

Remove matching elements from the set:

```js
const $editable = $(".item").not(".locked");
```

## `.is()`

Return a Boolean:

```js
if ($("#panel").is(":visible")) {
    console.log("Panel is visible");
}
```

## `.has()`

Keep elements containing a matching descendant:

```js
const $rowsWithErrors = $(".row").has(".error");
```

## Debugging strategy

Log counts after each transformation:

```js
const $rows = $(".row");
const $active = $rows.filter(".active");
const $editable = $active.not(".locked");

console.log({
    rows: $rows.length,
    active: $active.length,
    editable: $editable.length
});
```

This is much easier than debugging one long chain.

---

# 87. `.closest()` vs `.parents()` vs `.parent()`

Consider:

```html
<div class="dialog">
    <section class="body">
        <div class="row">
            <button class="save">Save</button>
        </div>
    </section>
</div>
```

## `.parent()`

Only the immediate parent:

```js
$(".save").parent();
```

Returns:

```html
<div class="row">
```

## `.parents()`

All matching ancestors:

```js
$(".save").parents("div");
```

May return both `.row` and `.dialog`.

## `.closest()`

Starts from the current element and finds the first matching element while moving upward:

```js
$(".save").closest(".dialog");
```

Usually the right choice for finding the logical component container.

## Common bug

```js
$(this).parent(".dialog")
```

returns nothing when `.dialog` is not the immediate parent.

Fix:

```js
$(this).closest(".dialog")
```

---

# 88. `.remove()` vs `.detach()` vs `.empty()`

These operations are not interchangeable.

## `.remove()`

Removes the matched elements from the DOM.

```js
$("#panel").remove();
```

Use when the element is being discarded.

## `.detach()`

Removes elements while preserving jQuery data/events for potential reinsertion.

```js
const $panel = $("#panel").detach();

// Later
$("#container").append($panel);
```

Use deliberately when temporarily moving/removing initialized content.

## `.empty()`

Removes child content but keeps the selected container:

```js
$("#list").empty();
```

## Debugging issue

A developer may accidentally remove the event delegation root:

```js
$("#list").remove();
```

Then later append a new `#list`, assuming handlers remain.

They do not belong to the new node.

If the goal was to clear rows:

```js
$("#list").empty();
```

might have been intended.

---

# 89. Cloning Elements and Event Handlers

Basic clone:

```js
const $copy = $("#template").clone();
```

A common misconception is that every kind of attached state is always copied.

jQuery's `.clone()` has options related to copying event handlers/data.

Example:

```js
const $copy = $("#template").clone(true, true);
```

Before using this approach, ask whether cloning handlers is actually desirable.

## Duplicate behavior risk

If the clone will live under a delegated handler root:

```js
$("#list").on("click", ".delete", deleteRow);
```

you usually do **not** need to clone a direct click handler onto the child.

Otherwise you can create duplicate execution.

## Better component pattern

Use HTML templates/data plus delegated events instead of cloning complex live state whenever practical.

---

# 90. Custom Events, `.trigger()`, and `.triggerHandler()`

jQuery supports custom application events.

Example:

```js
$("#cart").on("cart:updated", function (event, cart) {
    console.log("cart changed", cart);
});
```

Trigger:

```js
$("#cart").trigger("cart:updated", [
    { itemCount: 3, total: 1200 }
]);
```

## Debugging custom events

If a custom event does not fire, check:

- exact event name
- event namespace
- selected element
- binding timing
- element replacement
- propagation expectations
- whether `.trigger()` is called on the same logical event path

## `.trigger()` vs `.triggerHandler()`

They differ in behavior, including bubbling/default-action-related semantics and what is triggered.

Do not replace one with the other just because both "run a handler."

Verify the official API when the distinction matters.

## Avoid accidental recursion

```js
$("#save").on("save:run", function () {
    $("#save").trigger("save:run");
});
```

This recursively triggers itself.

Use logs/call stacks when you see:

```text
Maximum call stack size exceeded
```

---

# 91. One-Time Event Handlers with `.one()`

`.one()` attaches a handler that runs at most once per element for the specified event.

```js
$("#start").one("click", function () {
    console.log("First click only");
});
```

Useful for:

- one-time initialization
- onboarding actions
- "load once" UI behavior
- a transition that should initialize something once

## Debugging trap

If a handler worked once and then "stopped working," search for:

```js
.one(
```

The one-time behavior may be intentional.

## Parameters and behavior

A common form is:

```js
$elements.one(events, handler);
```

- `events` — one or more event types, optionally namespaced;
- `handler` — the function to execute;
- return value — the original jQuery collection, so chaining remains possible.

The "once" behavior is **per element per event type**. If the collection contains three buttons, each button can run its own one-time handler.

## Example with several elements

```js
$(".tip").one("mouseenter", function () {
    console.log("first hover for", this);
});
```

Hovering one `.tip` does not consume the one-time handler on every other `.tip`.

## Use `.one()` when

- an element should initialize itself on first interaction;
- analytics should record a specific first interaction;
- a temporary lifecycle handler should self-remove.

Do not use `.one()` for logic that must survive repeated user attempts, such as a submit handler that should work again after validation fails.

---

# 92. Debugging Ajax Timeouts, Retries, and Authentication

## Timeout

```js
$.ajax({
    url: "/api/report",
    timeout: 10000
})
.fail(function (xhr, textStatus) {
    if (textStatus === "timeout") {
        console.error("Request timed out");
    }
});
```

A timeout does not necessarily mean the server stopped processing the request.

For operations that create or modify data, blindly retrying can duplicate work.

## Retry strategy

Retries are more appropriate when:

- the operation is idempotent
- the failure is temporary
- the server/API permits retries
- you use backoff
- you cap retry count

Do not automatically retry every `POST`.

## Authentication debugging

A request may fail because:

- cookie not sent
- session expired
- token expired
- Authorization header missing
- cross-origin credentials configuration differs
- server redirects to login
- SameSite cookie behavior matters

Inspect:

- request headers
- cookies
- response status
- redirect chain
- response body

A "JSON parse problem" may actually be an HTML login page returned after session expiration.

---

# 93. `$.ajaxSetup()` and Hidden Global Configuration

`$.ajaxSetup()` can configure defaults globally.

Example:

```js
$.ajaxSetup({
    headers: {
        "X-App-Version": "2026.08"
    }
});
```

This can be convenient, but hidden global behavior makes debugging harder.

Imagine a library does:

```js
$.ajaxSetup({
    cache: false
});
```

or modifies headers, converters, timeout, or credentials behavior.

Now individual requests behave differently even though their local `$.ajax()` calls look normal.

## Debugging rule

When Ajax behavior seems impossible from the local code, search the project for:

```text
$.ajaxSetup(
$.ajaxPrefilter(
$.ajaxTransport(
```

jQuery's Ajax system supports extensibility, so global prefilters/transports/converters can affect requests.

Prefer explicit local configuration for feature-specific behavior where practical.

---

# 94. Debounce, Throttle, Scroll, Resize, and Input Storms

Some browser events can fire rapidly:

- `input`
- `scroll`
- `resize`
- mouse movement
- pointer movement

A handler that performs DOM queries or Ajax on every event may cause performance problems.

## Simple debounce helper

```js
function debounce(fn, delay) {
    let timer;

    return function (...args) {
        clearTimeout(timer);

        timer = setTimeout(() => {
            fn.apply(this, args);
        }, delay);
    };
}
```

Usage:

```js
$("#search").on("input", debounce(function () {
    console.log("search:", this.value);
}, 300));
```

## Debug event frequency

```js
$("#search").on("input.debug", function () {
    console.count("input events");
});
```

For scroll/resize performance, use the browser Performance panel instead of assuming jQuery itself is slow.

---

# 95. Debugging Bundlers and ES Modules

Modern projects may load jQuery through npm rather than a `<script>` tag.

Conceptually:

```js
import $ from "jquery";
```

In this environment, the module-local `$` may exist while:

```js
window.$
```

does not.

A legacy plugin may expect global:

```js
window.jQuery
window.$
```

while your bundler keeps jQuery module-scoped.

## Symptom

Your own imported code works:

```js
import $ from "jquery";
$("#x").hide();
```

but a legacy plugin fails to attach.

## Debug

Check:

```js
console.log("module $", $);
console.log("window.$", window.$);
console.log("window.jQuery", window.jQuery);
```

Then inspect the plugin's documented loading requirements.

Do not expose globals unless required by the architecture. Prefer module-compatible plugin packages when available.

## Bundle duplication

A bundler can also package multiple jQuery copies through dependency resolution.

Inspect the dependency tree and final bundle when plugin identity problems occur.

---

# 96. Debugging jQuery in WordPress and Other noConflict Environments

Many CMS/plugin environments intentionally avoid assigning jQuery to global `$`.

Code like:

```js
$(function () {
    // ...
});
```

may fail even though jQuery exists.

Use a scoped alias:

```js
jQuery(function ($) {
    $("#menu").on("click", function () {
        console.log("clicked");
    });
});
```

Or an IIFE:

```js
(function ($) {
    "use strict";

    // jQuery code
})(jQuery);
```

## Debug

```js
console.log(typeof jQuery);
console.log(typeof $);
```

Do not globally override `$` just to silence the error. Another library may legitimately own it.

---

# 97. jQuery 4 Focus and Blur Behavior

Focus-related event ordering has historically been difficult across browsers.

jQuery 4 modernized focus/blur behavior to align more closely with current browser standards instead of preserving older normalization behavior in supported modern browsers.

If an application depends on the exact sequence of:

```text
focus
focusin
blur
focusout
```

retest it carefully during a jQuery 3 → 4 upgrade.

## Debug exact order

```js
$("#field").on("focus blur focusin focusout", function (event) {
    console.log(event.type, performance.now());
});
```

Test in every browser your application officially supports.

Do not rely on assumptions learned from an old jQuery version.

## The order to expect in jQuery 4

For supported modern browsers other than IE, jQuery 4 stops overriding native focus-event order. The documented sequence when focus moves from one element to another is:

```text
blur
focusout
focus
focusin
```

Older jQuery normalized a different order:

```text
focusout
blur
focusin
focus
```

This matters when handlers mutate shared state, validate a field, open/close a widget, or depend on another focus handler having already run.

## Reproduce with two fields

```html
<input id="first">
<input id="second">
```

```js
$("#first, #second").on("blur focusout focus focusin", function (event) {
    console.log(event.type, this.id);
});
```

Click the first field and then the second. Compare the log on the old and new jQuery versions instead of relying on remembered event order.

### Migration best practice

If the business logic requires a particular state transition, make that dependency explicit in your code. Avoid coupling correctness to incidental cross-event ordering when one explicit event or a dedicated state function is enough.

---

# 98. CSP, Trusted Types, and Script Injection Problems

Modern applications may enforce **Content Security Policy (CSP)**.

A CSP can block:

- inline scripts
- `eval`-like execution
- scripts from unapproved hosts
- injected script sources
- some unsafe DOM patterns depending on policy

jQuery 4 also includes Trusted Types-related modernization.

## Debugging symptoms

Console may contain messages mentioning:

```text
Content Security Policy
Refused to execute inline script
Refused to load script
Trusted Types
```

This is a browser security policy issue, not something to bypass casually.

## Correct approach

1. identify which operation is blocked
2. inspect the active CSP header
3. remove unsafe code patterns where possible
4. use approved script sources/nonces/hashes according to your application's security design
5. use Trusted Types-compatible patterns where required
6. test after tightening security policies

Do not "fix" CSP by turning it off in production without security review.

---

# 99. Code Review Checklist for jQuery Debuggability

Use this during code review.

## Dependencies

- [ ] jQuery version is intentional.
- [ ] Full/slim build is intentional.
- [ ] Plugin versions are compatible.
- [ ] jQuery is not duplicated.
- [ ] Script/module order is correct.
- [ ] Upgrade warnings have been handled.

## Selectors and DOM

- [ ] IDs are unique.
- [ ] Selectors are stable.
- [ ] Dynamic nodes use appropriate event delegation.
- [ ] Traversal is not unnecessarily fragile.
- [ ] DOM updates use `.text()` for plain/untrusted text.
- [ ] `.attr()`, `.prop()`, and `.data()` are used intentionally.

## Events

- [ ] Initialization does not bind duplicates.
- [ ] Reusable modules namespace events.
- [ ] Cleanup exists for long-lived/global handlers.
- [ ] Arrow functions are not used where handler `this` is required.
- [ ] `preventDefault()` and `stopPropagation()` are intentional.
- [ ] `return false` is not used vaguely.

## Ajax

- [ ] Requests have failure handling.
- [ ] Payload encoding is correct.
- [ ] `contentType` and `dataType` are not confused.
- [ ] `FormData` uses proper jQuery options.
- [ ] Authentication/CSRF requirements are handled.
- [ ] Race conditions are considered.
- [ ] Double submission is considered.
- [ ] Loading and failure UI are defined.

## Maintainability

- [ ] Business logic is testable separately.
- [ ] Logs contain useful context.
- [ ] Magic timeouts are avoided.
- [ ] Errors are not silently swallowed.
- [ ] Deprecated APIs are not newly introduced.
- [ ] Important behavior has tests.

---

# 100. Master Symptom-to-Cause Matrix

| Symptom | First checks | Common causes |
|---|---|---|
| `$ is not defined` | `typeof jQuery`, script Network request | jQuery missing, order issue, noConflict |
| `$ is not a function` | inspect `$` value | global conflict, overwritten `$` |
| `$.ajax is not a function` | version/build, `typeof $.ajax` | slim build, wrong `$`, bad load |
| `$(...).plugin is not a function` | `typeof $.fn.plugin`, scripts | plugin missing, wrong order, multiple jQuery |
| Click does nothing | selector count, handler log | wrong selector, timing, replaced element |
| Click fires twice | `console.count()` | duplicate binding, duplicate script |
| New row button does nothing | inspect binding model | direct handler attached before insertion |
| Handler `this` is wrong | inspect function syntax | arrow function lexical `this` |
| Checkbox state wrong | compare attr/prop | using `.attr()` for live state |
| `.data()` looks stale | compare `.data()`/`.attr()` | jQuery data cache semantics |
| Number addition is wrong | `typeof value` | `.val()` returned strings |
| UI updated in DOM but not visible | Elements/computed CSS | CSS, parent hidden, overlay |
| Ajax request not visible | log handler, Network | event not fired, validation, code error |
| Ajax returns 404 | request URL | wrong path/base URL/route |
| Ajax returns 405 | HTTP method | method not allowed |
| Ajax returns 403 | headers/cookies/body | auth/CSRF/authorization |
| Ajax returns 415 | Content-Type | wrong request body media type |
| Ajax returns 422 | response JSON/body | validation failure |
| Ajax returns 500 | response + server logs | backend exception |
| Ajax says parsererror | raw response | invalid JSON, HTML error/login page |
| Production only fails | deployed assets | cache, CSP, base URL, slim build |
| Old code fails after upgrade | Migrate + API search | removed/deprecated API |
| Animation method missing | build filename | slim build |
| UI shows stale search result | request ordering | race condition |
| Memory grows over time | Memory panel, cleanup | leaked handlers/timers/plugins |
| Scroll page becomes slow | Performance panel | expensive frequent handler |
| Code only works with timeout | lifecycle tracing | real async/timing dependency |
| Handler disappears after render | inspect replaced node | direct handler belonged to old DOM |
| Form serialization misses input | `serializeArray()` | no `name`, disabled/unchecked control |
| Custom event not received | event name/root | wrong element/name/timing |
| Focus behavior changed after upgrade | log event sequence | version-specific focus normalization |
| CSP errors after deployment | Console + headers | security policy blocks code/resource |


# Closing Notes

The most important debugging skill is not memorizing every jQuery method.

It is learning to ask:

```text
What do I know?
What am I assuming?
What can I inspect?
At exactly which step does expected behavior become actual wrong behavior?
```

For jQuery specifically, the highest-value checks are usually:

```js
// 1. Did jQuery load?
typeof jQuery

// 2. Which version?
$.fn.jquery

// 3. Did my selector match?
$("#target").length

// 4. Did my handler run?
console.count("handler")

// 5. What values am I actually using?
console.log(value, typeof value)

// 6. Did the request really succeed?
// Inspect Network + jqXHR fail data

// 7. Is this a jQuery problem at all?
// Check HTML, CSS, JavaScript, HTTP, backend, plugins, and version compatibility.
```

If you build the habit of proving each layer one by one, even large legacy jQuery applications become much easier to debug.

---

## Suggested Learning Path

For a complete beginner, study the handbook in this order:

```text
Console
→ selectors
→ DOM ready
→ jQuery object vs DOM element
→ events
→ event delegation
→ values/attributes/properties/data
→ forms
→ Ajax
→ jqXHR and asynchronous flow
→ plugins
→ migration/version compatibility
→ performance
→ testing
```

Then revisit the scenario section and practice diagnosing each problem before reading its solution.

---

**End of jQuery Debugging Master Handbook**
