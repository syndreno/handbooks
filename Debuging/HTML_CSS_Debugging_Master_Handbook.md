# HTML & CSS Debugging Master Handbook

> A beginner-friendly, practical, and in-depth guide for finding, understanding, reproducing, and fixing HTML/CSS problems.

---

## Table of Contents

1. [How to Use This Handbook](#1-how-to-use-this-handbook)
2. [What Debugging Really Means](#2-what-debugging-really-means)
3. [The Browser Rendering Pipeline](#3-the-browser-rendering-pipeline)
4. [The Master Debugging Workflow](#4-the-master-debugging-workflow)
5. [Build a Minimal Reproduction](#5-build-a-minimal-reproduction)
6. [Browser DevTools Fundamentals](#6-browser-devtools-fundamentals)
7. [HTML Syntax and Parsing Bugs](#7-html-syntax-and-parsing-bugs)
8. [DOM Structure Bugs](#8-dom-structure-bugs)
9. [Semantic HTML Bugs](#9-semantic-html-bugs)
10. [Links, Paths, Resources, and Loading Problems](#10-links-paths-resources-and-loading-problems)
11. [Forms and Validation Debugging](#11-forms-and-validation-debugging)
12. [Images, Video, Audio, and Replaced Elements](#12-images-video-audio-and-replaced-elements)
13. [CSS Syntax Errors](#13-css-syntax-errors)
14. [Selector Debugging](#14-selector-debugging)
15. [Cascade, Origins, Importance, and Source Order](#15-cascade-origins-importance-and-source-order)
16. [Specificity Debugging](#16-specificity-debugging)
17. [Inheritance and Initial Values](#17-inheritance-and-initial-values)
18. [Cascade Layers](#18-cascade-layers)
19. [CSS Custom Properties](#19-css-custom-properties)
20. [The Box Model](#20-the-box-model)
21. [Width, Height, Min/Max Sizing](#21-width-height-minmax-sizing)
22. [CSS Units](#22-css-units)
23. [Display and Formatting Contexts](#23-display-and-formatting-contexts)
24. [Normal Flow](#24-normal-flow)
25. [Margin Collapsing](#25-margin-collapsing)
26. [Positioning](#26-positioning)
27. [Containing Blocks](#27-containing-blocks)
28. [Stacking Context and z-index](#28-stacking-context-and-z-index)
29. [Overflow and Scrolling](#29-overflow-and-scrolling)
30. [Flexbox Debugging](#30-flexbox-debugging)
31. [CSS Grid Debugging](#31-css-grid-debugging)
32. [Floats, Clear, Multi-column, and Legacy Layouts](#32-floats-clear-multi-column-and-legacy-layouts)
33. [Table Layout Debugging](#33-table-layout-debugging)
34. [Typography and Text Layout](#34-typography-and-text-layout)
35. [Backgrounds, Borders, Shadows, and Clipping](#35-backgrounds-borders-shadows-and-clipping)
36. [Transforms](#36-transforms)
37. [Transitions and Animations](#37-transitions-and-animations)
38. [Pseudo-classes and Pseudo-elements](#38-pseudo-classes-and-pseudo-elements)
39. [Responsive Design Debugging](#39-responsive-design-debugging)
40. [Media Queries](#40-media-queries)
41. [Container Queries](#41-container-queries)
42. [Viewport and Mobile Bugs](#42-viewport-and-mobile-bugs)
43. [Logical Properties and Writing Modes](#43-logical-properties-and-writing-modes)
44. [Accessibility Debugging](#44-accessibility-debugging)
45. [Focus, Keyboard, and Interaction States](#45-focus-keyboard-and-interaction-states)
46. [Cross-browser Debugging](#46-cross-browser-debugging)
47. [Feature Detection and Progressive Enhancement](#47-feature-detection-and-progressive-enhancement)
48. [Print CSS Debugging](#48-print-css-debugging)
49. [Shadow DOM and Style Isolation](#49-shadow-dom-and-style-isolation)
50. [Performance-related CSS Problems](#50-performance-related-css-problems)
51. [Linting, Validation, and Automated Checks](#51-linting-validation-and-automated-checks)
52. [CSS Architecture That Prevents Bugs](#52-css-architecture-that-prevents-bugs)
53. [Real-world Debugging Scenarios](#53-real-world-debugging-scenarios)
54. [Fast Diagnostic Decision Tree](#54-fast-diagnostic-decision-tree)
55. [Master Debugging Checklists](#55-master-debugging-checklists)
56. [Common Anti-patterns](#56-common-anti-patterns)
57. [Debugging Exercises](#57-debugging-exercises)
58. [Glossary](#58-glossary)
59. [Recommended Learning and Reference Resources](#59-recommended-learning-and-reference-resources)
60. [Final Debugging Principles](#60-final-debugging-principles)
61. [Appendix A — Debugging Scratchpad Template](#appendix-a-a-practical-debugging-scratchpad-template)
62. [Appendix B — Temporary Debug CSS Toolkit](#appendix-b-temporary-debug-css-toolkit)
63. [Appendix C — Useful Console Snippets](#appendix-c-useful-console-snippets-for-htmlcss-debugging)
64. [Appendix D — Beginner Debugging Practice Project](#appendix-d-beginner-debugging-practice-project)
65. [Appendix E — One-Minute Debugging Routine](#appendix-e-one-minute-debugging-routine)
66. [Appendix F — Advanced Modern CSS Debugging](#appendix-f-advanced-modern-css-debugging)
67. [Appendix G — HTML Document-Level Debugging](#appendix-g-html-document-level-debugging)
68. [Appendix H — Browser Defaults, Resets, and Normalization](#appendix-h-browser-defaults-resets-and-normalization)
69. [Appendix I — Framework and Utility-CSS Debugging](#appendix-i-framework-and-utility-css-debugging)
70. [Appendix J — Production-Only HTML/CSS Bugs](#appendix-j-production-only-htmlcss-bugs)
71. [Appendix K — Additional Real-World Scenarios](#appendix-k-additional-real-world-scenarios)
72. [Appendix L — Debugging by Symptom](#appendix-l-debugging-by-symptom)
73. [Appendix M — Master Learning Roadmap](#appendix-m-master-learning-roadmap)

---

# 1. How to Use This Handbook

This handbook is not only a list of CSS and HTML rules. It is designed to teach **how to think when a page does not look or behave as expected**.

You can use it in three ways:

- **Beginner:** read from the beginning and reproduce the examples.
- **Working developer:** jump directly to a symptom such as `z-index`, flexbox overflow, missing styles, form validation, or mobile layout.
- **Debugging reference:** use the checklists and decision trees near the end.

A strong debugger does not randomly edit values until the page looks correct. A strong debugger answers questions such as:

1. Is the expected element actually in the DOM?
2. Is the expected stylesheet loaded?
3. Does my selector match?
4. Is my declaration valid?
5. Did another declaration win in the cascade?
6. Is the value inherited or overridden?
7. Is the element constrained by its parent?
8. Is the problem caused by layout, paint, clipping, or stacking?
9. Does the bug happen only at a particular viewport size?
10. Is browser support or accessibility behavior involved?

That sequence is much faster than guessing.

---

# 2. What Debugging Really Means

## 2.1 Definition

Debugging is the process of:

1. **Observing a problem**
2. **Reproducing it**
3. **Isolating the cause**
4. **Understanding why it happens**
5. **Applying the smallest reliable fix**
6. **Verifying that the fix does not create another problem**

For HTML and CSS, the visible symptom can be misleading.

Example:

> "My button color is not working."

Possible causes include:

- the stylesheet did not load;
- the selector does not match;
- another selector has higher priority;
- an inline style overrides the rule;
- `!important` is involved;
- the property is invalid;
- a CSS variable is invalid;
- the button is disabled and a different rule applies;
- the element is actually a link styled to look like a button;
- a browser extension is injecting styles;
- the developer is editing a different file than the one being served.

Therefore:

> **The symptom is not the cause.**

---

## 2.2 Debugging vs fixing

A fix that you do not understand is fragile.

Bad debugging:

```css
.card {
  width: 100% !important;
  position: relative !important;
  z-index: 999999 !important;
}
```

This might hide the symptom while creating more problems.

Better debugging:

- identify what sets the current width;
- inspect the containing block;
- find the competing declaration;
- understand whether stacking is relevant;
- change only the necessary rule.

---

# 3. The Browser Rendering Pipeline

Understanding the browser pipeline explains many "mysterious" bugs.

A simplified page-rendering model is:

```text
HTML
  ↓
HTML parser
  ↓
DOM

CSS
  ↓
CSS parser
  ↓
CSSOM / style rules

DOM + applicable CSS
  ↓
style calculation
  ↓
layout
  ↓
paint
  ↓
compositing
  ↓
pixels on screen
```

JavaScript may modify the DOM or styles at any time, causing parts of the process to run again.

## 3.1 DOM

The **Document Object Model (DOM)** is the browser's tree representation of the HTML document.

Source:

```html
<main>
  <h1>Hello</h1>
  <p>Welcome</p>
</main>
```

Conceptual DOM:

```text
main
├── h1
│   └── "Hello"
└── p
    └── "Welcome"
```

Important:

The DOM seen in DevTools may not exactly match the source text because the browser's HTML parser can recover from malformed markup.

---

## 3.2 Style calculation

The browser determines which CSS declarations apply to every element.

It considers concepts such as:

- selector matching;
- origins;
- cascade layers;
- importance;
- specificity;
- source order;
- inheritance;
- computed values.

A rule can exist in the stylesheet and still not win.

---

## 3.3 Layout

Layout determines geometry:

- width;
- height;
- x/y position;
- line breaks;
- grid tracks;
- flex item sizes;
- scrollable overflow.

If an element has the correct color but the wrong position, the bug is probably a layout issue rather than selector matching.

---

## 3.4 Paint

Painting draws visual details such as:

- backgrounds;
- borders;
- text;
- shadows;
- outlines.

---

## 3.5 Compositing

Certain layers may be composited separately, especially around transforms, opacity, and animations.

This becomes relevant for:

- strange overlapping;
- animation performance;
- fixed/sticky elements;
- transformed ancestors.

---

# 4. The Master Debugging Workflow

Use this workflow before changing random code.

## Step 1: Reproduce the bug

Write down exactly what fails.

Weak description:

> The layout is broken.

Better description:

> At viewport widths from about 720px to 820px, the `.profile-actions` row overflows the card horizontally.

A reproducible bug is easier to solve.

---

## Step 2: Inspect the correct element

Open browser DevTools.

Typical shortcut:

```text
F12
```

or:

```text
Ctrl + Shift + I
```

Use the element picker and click the visible element.

Confirm:

- tag name;
- classes;
- IDs;
- attributes;
- parent;
- children;
- state.

---

## Step 3: Check whether the CSS rule matches

In the Styles panel, search for your expected property.

If the rule does not appear at all:

- selector may not match;
- stylesheet may not be loaded;
- media query may not match;
- CSS may contain a syntax error;
- rule may be inside an unsupported/incorrect conditional block.

---

## Step 4: Check crossed-out declarations

A crossed-out declaration usually means another declaration won.

Example:

```css
.button {
  color: blue;
}

#checkout .button {
  color: red;
}
```

The first declaration may appear crossed out because the second rule has greater specificity.

---

## Step 5: Check computed styles

The **Computed** panel answers:

> What value did the browser finally decide to use?

For example, you might write:

```css
width: 100%;
```

but the actual computed width may be `640px` because percentages resolve relative to another size.

---

## Step 6: Inspect the box model

Check:

- content size;
- padding;
- border;
- margin.

Many "width bugs" are actually padding, min-width, or overflow problems.

---

## Step 7: Disable rules one by one

DevTools allows temporary checkbox-like disabling of declarations.

This is one of the fastest debugging techniques.

If removing:

```css
min-width: 600px;
```

immediately fixes the mobile overflow, you have found an important cause.

---

## Step 8: Change values live

Try temporary values in DevTools.

Example:

```css
min-width: 0;
```

If that fixes a flex item, you now have evidence before editing source files.

---

## Step 9: Find the smallest permanent fix

Do not copy every temporary experiment.

Change only the source rule required to solve the actual cause.

---

## Step 10: Regression test

After fixing:

- resize the viewport;
- check keyboard navigation;
- test long content;
- test empty content;
- test different browsers where relevant;
- check dark/light themes if supported;
- check form states;
- check zoom.

---

# 5. Build a Minimal Reproduction

A **minimal reproduction** is the smallest example that still demonstrates the bug.

Suppose your production page contains:

- 5,000 lines of CSS;
- 15 scripts;
- three UI libraries;
- 20 nested components.

Instead of debugging all of that, create:

```html
<div class="card">
  <div class="content">Very long content...</div>
</div>
```

```css
.card {
  display: flex;
  width: 300px;
}

.content {
  white-space: nowrap;
}
```

If the overflow still occurs, the bug has been isolated.

## Why minimal reproductions are powerful

They remove:

- unrelated selectors;
- framework styles;
- JavaScript side effects;
- application data;
- component complexity.

They also expose incorrect assumptions.

---

# 6. Browser DevTools Fundamentals

Modern browser DevTools are the primary debugging environment for HTML and CSS.

## 6.1 Elements/Inspector panel

Use it to:

- inspect DOM structure;
- add/remove classes;
- edit attributes;
- temporarily change HTML;
- view matched CSS;
- inspect pseudo-elements.

---

## 6.2 Styles panel

Use it to:

- view matching rules;
- see overridden declarations;
- toggle declarations;
- add test declarations;
- inspect inherited styles;
- understand selector priority.

---

## 6.3 Computed panel

Use it when you need the final result.

Example questions:

- Why is this text `16px`?
- Why is the width `412px`?
- What is the final `display` value?
- Which rule produced this margin?

---

## 6.4 Box-model visualization

This usually shows:

```text
margin
  border
    padding
      content
```

Use it to find unexplained space.

---

## 6.5 Layout overlays

DevTools can visually inspect layout systems such as:

- Grid;
- Flexbox.

Grid overlays are especially useful for:

- track boundaries;
- gaps;
- line numbers;
- named areas.

Flex tools are useful for:

- direction;
- alignment;
- wrapping;
- gaps.

---

## 6.6 Device emulation

Use responsive/device mode to test:

- viewport width;
- viewport height;
- orientation;
- touch-like dimensions;
- responsive breakpoints.

Important:

Device emulation is useful, but final testing on real devices is still valuable.

---

## 6.7 Network panel

If styles or images are missing, inspect network requests.

Look for:

```text
404
403
500
blocked
cancelled
wrong content type
redirect loops
```

A CSS problem can actually be a resource-loading problem.

---

# 7. HTML Syntax and Parsing Bugs

Browsers are forgiving. This is useful for users but dangerous for debugging.

## 7.1 Missing closing tags

Buggy:

```html
<div class="card">
  <h2>Title
  <p>Hello
</div>
```

The browser may recover, but the resulting DOM may differ from what you imagined.

Prefer:

```html
<div class="card">
  <h2>Title</h2>
  <p>Hello</p>
</div>
```

---

## 7.2 Incorrect nesting

Buggy:

```html
<p>
  Paragraph
  <div>Block content</div>
</p>
```

HTML parsing rules may implicitly close the paragraph before the `<div>`.

This means your CSS selector:

```css
p div {
  color: red;
}
```

may match nothing.

### Debugging technique

Do not only inspect **View Source**.

Inspect the actual DOM in DevTools.

---

## 7.3 Duplicate IDs

Bad:

```html
<section id="profile">...</section>
<section id="profile">...</section>
```

An `id` is intended to identify one element in a document.

Use:

```html
<section class="profile">...</section>
<section class="profile">...</section>
```

for repeated components.

Duplicate IDs can create confusing behavior for:

- fragment navigation;
- labels;
- scripts;
- accessibility relationships;
- CSS selectors.

---

## 7.4 Unquoted attribute mistakes

Legal in some simple cases:

```html
<input type=text>
```

Safer and clearer:

```html
<input type="text">
```

Quoting prevents accidental parsing problems when values contain spaces or special characters.

---

## 7.5 Boolean attributes

A common beginner misunderstanding:

```html
<input disabled="false">
```

For HTML boolean attributes, presence is what matters. The above input is disabled.

To enable it, remove the attribute:

```html
<input>
```

Similarly:

```html
<input required>
<input checked>
<option selected>
```

---

## 7.6 Case behavior

HTML element names are commonly written lowercase:

```html
<div></div>
```

CSS class names are case-sensitive in normal HTML/CSS matching situations:

```html
<div class="ProfileCard"></div>
```

This does not match:

```css
.profilecard {
  ...
}
```

Use consistent naming.

---

# 8. DOM Structure Bugs

Many CSS selectors depend on parent/child relationships.

Suppose CSS expects:

```css
.card > .title {
  font-weight: bold;
}
```

Expected HTML:

```html
<div class="card">
  <h2 class="title">Hello</h2>
</div>
```

But actual HTML:

```html
<div class="card">
  <header>
    <h2 class="title">Hello</h2>
  </header>
</div>
```

The child combinator `>` requires the title to be a **direct child**, so the rule does not match.

Options:

```css
.card .title {
  font-weight: bold;
}
```

or keep the stricter CSS and correct the structure.

## The DOM is the structure CSS actually sees

The browser may insert, move, or implicitly close elements while parsing invalid or special HTML. That means **View Source** and the live DOM can differ.

Classic example:

```html
<table>
  <tr><td>A</td></tr>
</table>
```

Browsers commonly expose a `<tbody>` in the parsed DOM even when it was not written explicitly. A selector or JavaScript traversal that assumes a particular parent may therefore behave differently from the source text.

## Debugging workflow

When a structure-dependent selector fails:

1. inspect the element in the Elements/Inspector panel;
2. expand its real parents and children;
3. test the selector in the Console:

```js
document.querySelectorAll(".card > .title").length
```

4. compare the result with the relationship the selector requires;
5. fix either the HTML structure or the selector—whichever better represents the intended component contract.

## Common structural causes

- framework/component wrappers inserted at runtime;
- malformed nesting corrected by the parser;
- conditional rendering adding an extra wrapper;
- table parsing introducing expected table-group elements;
- an element rendered in a portal, iframe, or shadow tree instead of under the visible logical parent.

A selector is not "broken" when the DOM relationship it asks for does not exist.

---

# 9. Semantic HTML Bugs

Semantic HTML communicates meaning.

Instead of:

```html
<div class="button" onclick="save()">Save</div>
```

prefer:

```html
<button type="button">Save</button>
```

Why?

A native button already provides useful behavior such as:

- keyboard focusability;
- keyboard activation;
- recognizable semantics;
- form-related behavior.

Likewise, prefer meaningful elements where appropriate:

```html
<header>
<nav>
<main>
<article>
<section>
<aside>
<footer>
<button>
<label>
<table>
```

## Debugging question

When an interaction behaves strangely, ask:

> Am I fighting against the native semantics of the element I chose?

## Semantic mistakes can become behavior bugs

Choosing an element is not only about accessibility labels. Native elements bring built-in browser behavior.

For example:

```html
<a href="/settings">Settings</a>
```

means navigation, while:

```html
<button type="button">Open settings panel</button>
```

means an action.

Using an anchor with a fake `href="#"` for an action can introduce unwanted URL/hash changes and extra `preventDefault()` code. Using a `<div>` as a button requires you to rebuild focus, keyboard activation, disabled behavior, and semantics manually.

## Debugging checklist

When an interactive control behaves differently for mouse and keyboard, inspect:

- the actual tag name;
- `type` on `<button>`;
- `href` on links;
- label/control relationships;
- whether a disabled state is native or only visual;
- whether JavaScript is compensating for the wrong element choice.

### Best practice

Start with the native element whose behavior most closely matches the feature, then style it. Add ARIA only when native semantics cannot express the required state/relationship; ARIA does not automatically add missing keyboard behavior.

---

# 10. Links, Paths, Resources, and Loading Problems

A missing stylesheet can make the entire page look broken.

## 10.1 Relative path confusion

Directory:

```text
project/
├── index.html
├── css/
│   └── app.css
└── pages/
    └── about.html
```

From `index.html`:

```html
<link rel="stylesheet" href="css/app.css">
```

From `pages/about.html`:

```html
<link rel="stylesheet" href="../css/app.css">
```

---

## 10.2 Debugging a missing stylesheet

Check:

1. Network panel.
2. Requested URL.
3. HTTP status.
4. Response body.
5. `href`.
6. spelling and capitalization.
7. deployment path.
8. cache.

Bad:

```html
<link rel="stylesheet" href="/css/style.css">
```

if the application is deployed under:

```text
https://example.com/myapp/
```

and the file actually lives at:

```text
/myapp/css/style.css
```

---

## 10.3 Stylesheet order

HTML:

```html
<link rel="stylesheet" href="base.css">
<link rel="stylesheet" href="components.css">
<link rel="stylesheet" href="overrides.css">
```

For otherwise equal rules, later declarations can win.

Changing file order can therefore change the page.

---

## 10.4 Cache confusion

Symptom:

> I changed the CSS file, but nothing changed.

Check:

- hard reload;
- network cache settings in DevTools;
- generated build output;
- service worker;
- CDN/browser cache;
- whether you edited the correct source file.

Never assume "browser cache" is automatically the cause. Confirm it.

---

# 11. Forms and Validation Debugging

Forms combine HTML semantics, browser validation, CSS states, and server behavior.

## 11.1 Labels

Good:

```html
<label for="email">Email</label>
<input id="email" name="email" type="email">
```

A label should be associated with its control.

Another valid pattern:

```html
<label>
  Email
  <input name="email" type="email">
</label>
```

---

## 11.2 `name` is not the same as `id`

```html
<input id="user-email" name="email">
```

`id`:

- identifies an element;
- can connect `<label for="...">`;
- can be selected by `#id`.

`name`:

- identifies submitted form data.

If `name` is missing, the value may not be included as expected in normal form submission.

---

## 11.3 Validation attributes

Example:

```html
<input
  type="email"
  name="email"
  required
  minlength="6"
>
```

Useful validation-related attributes include:

- `required`;
- `min`;
- `max`;
- `minlength`;
- `maxlength`;
- `pattern`;
- input-specific constraints.

---

## 11.4 `:valid` and `:invalid`

```css
input:invalid {
  border-color: crimson;
}

input:valid {
  border-color: green;
}
```

Be careful: styling every invalid field immediately can create a poor experience before the user has interacted.

A more deliberate state strategy may be better.

---

## 11.5 Button defaults

Inside a form:

```html
<button>Cancel</button>
```

may behave as a submit button.

When you mean a normal button:

```html
<button type="button">Cancel</button>
```

For submission:

```html
<button type="submit">Save</button>
```

---

## 11.6 Disabled vs readonly

```html
<input disabled>
```

vs:

```html
<input readonly>
```

They are not interchangeable.

Debug the intended user behavior and submission behavior rather than choosing based only on appearance.

---

# 12. Images, Video, Audio, and Replaced Elements

Images often create layout bugs because their intrinsic dimensions participate in sizing.

## 12.1 Responsive image baseline

```css
img {
  max-width: 100%;
  height: auto;
}
```

This prevents a large image from exceeding the width of its container in many common layouts.

---

## 12.2 `object-fit`

For a fixed image frame:

```css
.avatar {
  width: 120px;
  height: 120px;
  object-fit: cover;
}
```

`cover` fills the box and may crop.

`contain` preserves the whole image and may leave empty space.

---

## 12.3 Aspect ratio

```css
.video-frame {
  aspect-ratio: 16 / 9;
  width: 100%;
}
```

Useful when a responsive element needs a consistent shape.

---

## 12.4 Inline image bottom gap

Images are inline by default and can participate in text baseline alignment.

If you see an unexplained small gap below an image, try:

```css
img {
  display: block;
}
```

or inspect `vertical-align` behavior if it needs to remain inline.

---

# 13. CSS Syntax Errors

A CSS declaration has this form:

```css
selector {
  property: value;
}
```

## 13.1 Missing colon

Wrong:

```css
.card {
  color red;
}
```

Correct:

```css
.card {
  color: red;
}
```

---

## 13.2 Invalid property name

Wrong:

```css
.card {
  text-color: red;
}
```

The browser ignores unknown declarations.

Correct:

```css
.card {
  color: red;
}
```

---

## 13.3 Invalid value

```css
.card {
  width: banana;
}
```

The declaration is invalid and ignored.

DevTools often shows warning indicators for invalid declarations.

---

## 13.4 Missing closing brace

Buggy:

```css
.card {
  color: red;

.title {
  font-size: 2rem;
}
```

A missing brace can affect parsing of later CSS.

Use formatting and linting to catch this early.

---

## 13.5 Comments

Correct:

```css
/* comment */
```

Do not use JavaScript-style single-line comments:

```css
// not a normal CSS comment
```

---

# 14. Selector Debugging

A selector can be valid but still match zero elements.

## 14.1 Class

HTML:

```html
<div class="card"></div>
```

CSS:

```css
.card {}
```

---

## 14.2 ID

HTML:

```html
<div id="profile"></div>
```

CSS:

```css
#profile {}
```

---

## 14.3 Attribute

```css
input[type="email"] {}
```

---

## 14.4 Descendant

```css
.card .title {}
```

Matches `.title` anywhere inside `.card`.

---

## 14.5 Direct child

```css
.card > .title {}
```

Matches only direct children.

---

## 14.6 Adjacent sibling

```css
label + input {}
```

Matches an `input` immediately after a `label`.

---

## 14.7 General sibling

```css
h2 ~ p {}
```

Matches later sibling paragraphs sharing the same parent.

---

## 14.8 Compound selector

```css
button.primary {}
```

Means:

> A `button` that also has class `primary`.

It does **not** mean a `.primary` descendant inside a button.

Compare:

```css
button.primary {}
button .primary {}
```

These are different.

---

## 14.9 Debug selector matching in console

In the browser console:

```js
document.querySelector(".card")
```

If the result is:

```text
null
```

your selector did not find an element in the current document.

For all matches:

```js
document.querySelectorAll(".card")
```

---

# 15. Cascade, Origins, Importance, and Source Order

CSS means **Cascading Style Sheets**. The cascade decides which declaration wins when multiple declarations apply.

Do not reduce the cascade to:

> "The last CSS rule always wins."

That is only true after more important cascade factors are tied.

A practical debugging model is:

1. Is the declaration relevant to the current element/state?
2. What origin/importance/layer does it belong to?
3. What is the selector specificity?
4. If still tied, which comes later?

---

## 15.1 Source order example

```css
.button {
  color: blue;
}

.button {
  color: red;
}
```

The second declaration wins because the selectors have equal weight and it appears later.

---

## 15.2 Inline styles

```html
<button style="color: purple">Buy</button>
```

An ordinary stylesheet rule such as:

```css
button {
  color: red;
}
```

will not normally override that inline declaration.

Do not immediately add `!important`. First ask why inline styling exists.

---

## 15.3 `!important`

Example:

```css
.alert {
  color: red !important;
}
```

`!important` changes cascade priority.

It can be useful in controlled situations, but overuse creates a priority war.

Bad architecture:

```css
.button {
  color: red !important;
}

.page .button {
  color: blue !important;
}

#checkout .page .button {
  color: green !important;
}
```

This becomes difficult to reason about.

---

# 16. Specificity Debugging

Specificity is a weight used when competing selectors are compared within the relevant cascade context.

A beginner-friendly mental model is to consider:

```text
ID selectors         → strong
class/attribute/state → medium
element/pseudo-element → lower
```

Example:

```css
#app .button {
  color: red;
}

.button {
  color: blue;
}
```

The first rule has greater selector specificity.

---

## 16.1 Do not "solve" specificity by adding more selectors

Bad:

```css
body #app main .page .panel .button.primary {
  color: blue;
}
```

This creates future maintenance problems.

Prefer class-based component selectors when practical:

```css
.button--primary {
  color: blue;
}
```

---

## 16.2 `:where()` and specificity

`:where()` is useful when you want selector matching without adding specificity from its arguments.

Example:

```css
:where(.article, .page) h2 {
  margin-block-start: 2rem;
}
```

This can be useful for low-priority base styling.

---

## 16.3 Debugging specificity

In DevTools:

1. inspect the element;
2. find the property;
3. look for crossed-out declarations;
4. inspect the selectors that compete;
5. identify whether specificity is actually the deciding factor.

Do not calculate specificity if a media query is not active or the selector does not match.

---

# 17. Inheritance and Initial Values

Some CSS properties inherit naturally; others generally do not.

Commonly inherited examples include:

```css
color
font-family
font-size
line-height
```

Commonly non-inherited examples include:

```css
margin
padding
border
width
height
background
```

Example:

```css
body {
  color: #222;
  font-family: system-ui, sans-serif;
}
```

Descendants generally inherit the text color and font unless overridden.

---

## 17.1 Useful CSS-wide keywords

```css
inherit
initial
unset
revert
revert-layer
```

They are not identical.

When debugging a reset or inheritance issue, inspect the computed value rather than guessing.

## Four values beginners often confuse

These CSS-wide keywords answer different questions:

| Keyword | Simplified meaning |
|---|---|
| `inherit` | Use the parent's computed value. |
| `initial` | Use the property's CSS-defined initial value. |
| `unset` | Behave like `inherit` for inherited properties, otherwise like `initial`. |
| `revert` | Roll back to the value from an earlier cascade origin/context. |
| `revert-layer` | Roll back within cascade-layer ordering. |

Do not assume `initial` means "browser default stylesheet". The CSS initial value and the browser's user-agent stylesheet are different concepts.

## Debug example

```css
button {
  color: inherit;
}
```

This can make the button use its parent's text color instead of a browser/framework button color.

To trace an inherited value:

1. select the element in DevTools;
2. inspect Computed styles;
3. expand the property to see the winning declaration;
4. inspect the ancestor that supplied the inherited value.

## Custom properties are inherited by default

This is especially important for variables:

```css
:root {
  --accent: blue;
}

.dialog {
  --accent: purple;
}
```

Descendants of `.dialog` normally see the purple custom property unless another declaration changes it.

---

# 18. Cascade Layers

Cascade layers allow authors to organize groups of CSS with explicit cascade ordering.

Example:

```css
@layer reset, base, components, utilities;

@layer base {
  button {
    font: inherit;
  }
}

@layer components {
  .button {
    padding: 0.75rem 1rem;
  }
}
```

Why useful?

Large projects often contain:

- third-party CSS;
- reset styles;
- theme styles;
- components;
- utility classes.

Layers can make precedence more deliberate and reduce specificity battles.

Debugging question:

> Is my rule losing because it is in a lower-priority layer?

DevTools can help reveal cascade context.

## Layer order is separate from specificity

For normal author declarations, a rule in a later/higher-priority layer can beat a more specific selector in an earlier/lower-priority layer.

Example:

```css
@layer vendor, components;

@layer vendor {
  #checkout .button {
    color: red;
  }
}

@layer components {
  .button {
    color: blue;
  }
}
```

Even though `#checkout .button` is more specific, layer precedence is considered before specificity among declarations from different layers.

## Important unlayered-style gotcha

Normal author rules that are **not placed in a layer** have higher priority than normal author rules inside layers.

That can surprise a developer who carefully organizes framework CSS into layers but leaves an old override unlayered.

## Debugging order

When a declaration loses, inspect in this order:

```text
origin / importance
→ layer
→ specificity
→ scope/proximity where applicable
→ source order
```

Do not keep increasing selector specificity if the real cause is layer ordering.

### `!important` caution

Important declarations follow special cascade ordering, including reversed layer precedence compared with normal declarations. Use DevTools to inspect the actual winner instead of trying to memorize a "specificity number" alone.

---

# 19. CSS Custom Properties

Custom properties are commonly called CSS variables.

```css
:root {
  --brand-color: #2563eb;
}

.button {
  background: var(--brand-color);
}
```

---

## 19.1 Fallback

```css
.button {
  background: var(--button-bg, #333);
}
```

If `--button-bg` is unavailable/invalid at the point of use, the fallback can be used.

---

## 19.2 Scope

```css
:root {
  --text-color: black;
}

.dark-theme {
  --text-color: white;
}

.card {
  color: var(--text-color);
}
```

A variable may resolve differently depending on where the element is in the DOM.

---

## 19.3 Common bug

```css
.card {
  color: var(--card-color);
}
```

But `--card-color` was never defined.

Use:

```css
.card {
  color: var(--card-color, #222);
}
```

where a fallback is appropriate.

---

## 19.4 Debugging custom properties

Inspect:

- where the variable is defined;
- whether another declaration overrides it;
- whether it inherits into the element;
- whether the final substituted value is valid.

---

# 20. The Box Model

Every normal CSS box can be thought of as:

```text
┌─────────────────────────── margin ──────────────────────────┐
│ ┌──────────────────────── border ─────────────────────────┐ │
│ │ ┌───────────────────── padding ───────────────────────┐ │ │
│ │ │                    content                         │ │ │
│ │ └────────────────────────────────────────────────────┘ │ │
│ └────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

---

## 20.1 `content-box`

Default sizing behavior for many elements:

```css
.box {
  box-sizing: content-box;
  width: 300px;
  padding: 20px;
  border: 5px solid;
}
```

Total outer width before margins:

```text
300 + 40 + 10 = 350px
```

---

## 20.2 `border-box`

```css
.box {
  box-sizing: border-box;
  width: 300px;
  padding: 20px;
  border: 5px solid;
}
```

The declared width includes content + padding + border.

A common global setup:

```css
*,
*::before,
*::after {
  box-sizing: border-box;
}
```

---

## 20.3 Common width bug

```css
.container {
  width: 100%;
  padding: 24px;
}
```

With `content-box`, the padding can make the rendered box wider than the containing space.

Diagnose with the box-model panel.

---

# 21. Width, Height, Min/Max Sizing

Sizing bugs frequently come from constraints rather than the `width` you are staring at.

Inspect:

```css
width
min-width
max-width
height
min-height
max-height
```

---

## 21.1 `width: 100%` does not mean viewport width

It generally resolves relative to an appropriate containing block.

Example:

```css
.parent {
  width: 500px;
}

.child {
  width: 100%;
}
```

The child is based on the parent, not automatically the browser window.

---

## 21.2 `min-width` can defeat responsiveness

```css
.card {
  width: 100%;
  min-width: 700px;
}
```

On a 390px mobile viewport, overflow is expected.

---

## 21.3 `max-width` pattern

```css
.container {
  width: min(100% - 2rem, 70rem);
  margin-inline: auto;
}
```

This creates a fluid container with a maximum width.

---

## 21.4 Height percentage confusion

```css
.child {
  height: 100%;
}
```

Percentage heights depend on sizing conditions of ancestors. If the reference height is not established as expected, the result may surprise you.

When debugging, inspect ancestor heights.

---

# 22. CSS Units

## Absolute-like CSS pixel unit

```css
px
```

Good for many UI details such as borders and precise dimensions.

---

## Font-relative

```css
em
rem
```

`em` often depends on the current element's font size.

`rem` depends on the root font size.

---

## Viewport-relative

```css
vw
vh
dvw
dvh
svh
lvh
```

Mobile browser UI can make viewport units an important debugging topic. Modern viewport variants help express different viewport concepts.

---

## Container-relative

Container query units include forms such as:

```css
cqw
cqh
cqi
cqb
```

Use them when sizing relative to a query container.

---

## Percentage

```css
%
```

Percentages resolve relative to a property-specific reference.

A key debugging principle:

> Always ask: "percentage of what?"

---

# 23. Display and Formatting Contexts

The `display` property changes how an element participates in layout.

Common values:

```css
block
inline
inline-block
flex
grid
none
```

---

## 23.1 Inline sizing surprise

Example:

```css
span {
  width: 300px;
}
```

A normal inline element does not behave like a block box for width in the way beginners often expect.

Try:

```css
span {
  display: inline-block;
  width: 300px;
}
```

if that matches the intended design.

---

## 23.2 `display: none`

```css
.hidden {
  display: none;
}
```

The element does not generate a normal box.

Compare with:

```css
visibility: hidden;
```

which hides visibility while preserving layout space.

And:

```css
opacity: 0;
```

which makes the element transparent but does not automatically remove it from layout or interaction.

These are different tools.

---

# 24. Normal Flow

Before flexbox, grid, absolute positioning, or transforms, elements participate in **normal flow**.

Block-level boxes generally stack vertically.

Inline content flows within lines.

Debugging strategy:

1. temporarily remove `position`;
2. remove transforms;
3. disable flex/grid;
4. see how the element behaves in normal flow.

This often reveals which layout system introduced the issue.

## What participates in normal flow

Normal flow is the browser's default layout behavior before special layout/positioning changes are applied.

In simplified terms:

- block boxes are laid out one after another in the block direction;
- inline content forms line boxes and wraps;
- margins and intrinsic content affect surrounding geometry.

Some features move elements partly or fully out of normal flow. A classic example is:

```css
.badge {
  position: absolute;
}
```

The absolutely positioned badge no longer reserves normal-flow space where it would otherwise have appeared.

## Why this matters for debugging

Symptom:

> "The next element moved up underneath my badge."

If the badge became `position: absolute`, the following element is not required to reserve its old space.

Compare by temporarily toggling:

```css
position: static;
```

in DevTools.

## Normal flow is a useful baseline

Before adding another `top`, `left`, transform, negative margin, or `z-index`, ask:

> What would the document do if I removed the special positioning?

Often the simplest permanent fix is to let flexbox/grid/normal flow express the relationship instead of compensating with offsets.

---

# 25. Margin Collapsing

Vertical margins of certain block boxes can collapse rather than add together in the intuitive way beginners expect.

Example:

```css
h2 {
  margin-bottom: 30px;
}

p {
  margin-top: 20px;
}
```

You might expect 50px of space. Under collapsing conditions, the result can differ.

If vertical spacing seems strange:

- inspect margins in DevTools;
- understand the surrounding formatting context;
- consider layout models such as flex/grid where margin-collapsing behavior differs.

Modern layout often benefits from parent-controlled spacing:

```css
.stack {
  display: grid;
  gap: 1rem;
}
```

## Where collapsing commonly appears

Margin collapsing primarily affects block-axis margins in normal block formatting contexts. Common cases include:

- adjacent vertical margins between block siblings;
- a first/last child's margin interacting with a parent under certain conditions;
- an empty block's own vertical margins.

It does **not** work the same way inside Flexbox or Grid formatting, which is why changing `display` can appear to "fix" mysterious spacing.

## Debugging parent/child spacing

Example:

```html
<div class="section">
  <h2>Title</h2>
</div>
```

```css
h2 {
  margin-top: 2rem;
}
```

The visible space may appear outside the parent in a way a beginner does not expect.

Do not immediately add arbitrary padding. First inspect the box model and determine whether margin collapse is occurring.

## Ways to express intentional component spacing

Depending on design, prefer one clear spacing owner:

```css
.stack {
  display: grid;
  gap: 1rem;
}
```

or explicit parent padding, or carefully controlled child margins.

Choose the layout model for semantic/layout reasons—not solely to suppress margin collapse accidentally.

---

# 26. Positioning

Common `position` values:

```css
static
relative
absolute
fixed
sticky
```

---

## 26.1 Relative

```css
.card {
  position: relative;
}
```

Often used to establish positioning context for an absolutely positioned descendant.

---

## 26.2 Absolute

```css
.badge {
  position: absolute;
  top: 0;
  right: 0;
}
```

The badge is positioned relative to its relevant containing block, not simply "the nearest parent" in every possible scenario.

A common pattern:

```css
.card {
  position: relative;
}

.badge {
  position: absolute;
  inset-block-start: 0;
  inset-inline-end: 0;
}
```

---

## 26.3 Fixed

```css
.help {
  position: fixed;
  right: 1rem;
  bottom: 1rem;
}
```

Usually positioned relative to the viewport, but certain ancestor effects can complicate expectations.

---

## 26.4 Sticky

```css
.header {
  position: sticky;
  top: 0;
}
```

Sticky debugging checklist:

- is an inset such as `top` specified?
- which ancestor provides the scrolling area?
- does an ancestor's overflow behavior change the scroll container?
- is there enough scroll distance?
- is the sticky element larger than the available region?

---

# 27. Containing Blocks

Positioned and percentage-sized elements often resolve against a **containing block**.

This is one of the most important advanced debugging concepts.

When an absolute element appears in the wrong location, ask:

> Which box is it actually positioning against?

Do not assume it is the visible parent.

Inspect ancestor layout and positioning properties.

## Why containing blocks matter

Many CSS values need a reference box. The browser uses a **containing block** to resolve geometry such as percentage sizing and positioned offsets.

For a common absolutely positioned case:

```html
<div class="card">
  <span class="badge">New</span>
</div>
```

```css
.card {
  position: relative;
}

.badge {
  position: absolute;
  top: 0;
  right: 0;
}
```

The positioned `.card` establishes the reference for the badge, so `top: 0; right: 0` pins the badge to the card.

If `position: relative` is accidentally removed, the badge may position against a different ancestor/reference and appear far away.

## Debugging steps

1. inspect the positioned element;
2. walk upward through ancestors;
3. identify which ancestor establishes its containing block;
4. toggle suspicious `position`, `transform`, `filter`, `contain`, or related properties;
5. inspect percentage widths/heights against the box they actually resolve from.

## Fixed positioning caveat

`position: fixed` is commonly relative to the viewport, but certain ancestor properties—most notably transforms—can establish a containing block that changes the result. If a "fixed" panel scrolls or positions like it belongs to a component, inspect transformed ancestors first.

---

# 28. Stacking Context and z-index

`z-index` is frequently misunderstood.

A common bad fix:

```css
.modal {
  z-index: 999999999;
}
```

Large numbers do not escape stacking context boundaries.

---

## 28.1 Simple example

```css
.a {
  position: relative;
  z-index: 2;
}

.b {
  position: relative;
  z-index: 1;
}
```

Within a comparable stacking context, `.a` can paint above `.b`.

---

## 28.2 Why z-index "does nothing"

Possible causes:

- the elements are in different stacking contexts;
- an ancestor creates a stacking context;
- the element is clipped by overflow;
- the visual issue is not actually stacking;
- another element is a descendant of a higher stacking context.

Properties/conditions that can participate in stacking context creation include several modern CSS features, so inspect the full ancestor chain rather than memorizing only one trigger.

---

## 28.3 Debugging strategy

1. Inspect the overlapping element.
2. Inspect its ancestors.
3. Identify stacking contexts.
4. Compare sibling stacking contexts.
5. Fix the hierarchy rather than only increasing numbers.

---

# 29. Overflow and Scrolling

Common values:

```css
overflow: visible;
overflow: hidden;
overflow: auto;
overflow: scroll;
overflow: clip;
```

---

## 29.1 Horizontal overflow debugging

Symptom:

> The page has a horizontal scrollbar.

Possible causes:

- fixed-width child;
- `min-width`;
- long unbreakable text;
- image wider than container;
- `100vw` combined with surrounding layout;
- negative margins;
- absolute positioning;
- transform;
- grid/flex minimum sizing;
- preformatted code;
- table width.

Temporary diagnostic CSS:

```css
* {
  outline: 1px solid rgba(255, 0, 0, 0.15);
}
```

Use only for debugging.

You can also inspect:

```js
document.documentElement.scrollWidth
document.documentElement.clientWidth
```

If `scrollWidth > clientWidth`, the document has horizontal overflow.

---

## 29.2 Do not hide the symptom

This:

```css
html,
body {
  overflow-x: hidden;
}
```

may hide the scrollbar without fixing the oversized element.

Find the overflowing box first.

---

# 30. Flexbox Debugging

Flexbox is excellent for one-dimensional layout, but it has important sizing rules.

Basic container:

```css
.row {
  display: flex;
  gap: 1rem;
}
```

---

## 30.1 Main axis vs cross axis

With:

```css
flex-direction: row;
```

main axis is horizontal.

With:

```css
flex-direction: column;
```

main axis is vertical.

Therefore:

```css
justify-content
```

works along the main axis.

```css
align-items
```

works along the cross axis.

This is a common beginner confusion.

---

## 30.2 `flex-wrap`

Without wrapping:

```css
.toolbar {
  display: flex;
}
```

items may shrink or overflow.

For wrapping:

```css
.toolbar {
  display: flex;
  flex-wrap: wrap;
}
```

---

## 30.3 `min-width: auto` surprise

A classic flex bug:

```html
<div class="row">
  <aside>...</aside>
  <main class="content">
    AVeryVeryVeryVeryLongUnbreakableString
  </main>
</div>
```

```css
.row {
  display: flex;
}

.content {
  flex: 1;
}
```

The content may refuse to shrink as expected because of automatic minimum sizing.

A common fix:

```css
.content {
  flex: 1;
  min-width: 0;
}
```

Use this when your diagnosis confirms the flex item's minimum size is causing overflow.

---

## 30.4 `flex: 1`

Commonly:

```css
.item {
  flex: 1;
}
```

is shorthand-like behavior that makes items participate in flexible growth/shrinkage.

When debugging, inspect the resolved:

- `flex-grow`;
- `flex-shrink`;
- `flex-basis`.

---

## 30.5 Equal columns not equal?

Example:

```css
.row {
  display: flex;
}

.col {
  flex: 1;
}
```

Columns can still appear unequal because:

- padding differs;
- borders differ;
- min-content sizing matters;
- `box-sizing` differs;
- nested content prevents shrinking.

Inspect actual box sizes.

---

## 30.6 Flex debugging checklist

Check:

```text
flex-direction
flex-wrap
justify-content
align-items
align-self
gap
flex-grow
flex-shrink
flex-basis
min-width / min-height
overflow
```

Use the Flexbox overlay/tools in DevTools when available.

---

# 31. CSS Grid Debugging

Basic grid:

```css
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
}
```

---

## 31.1 Grid overflow with `1fr`

Consider:

```css
.grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
}
```

Long minimum content can sometimes make tracks larger than expected.

A common robust pattern:

```css
.grid {
  grid-template-columns:
    minmax(0, 1fr)
    minmax(0, 1fr);
}
```

This allows tracks to shrink below their automatic minimum when appropriate.

---

## 31.2 Auto-placement surprise

If explicit placement is missing, grid auto-placement may place items differently than expected.

Inspect:

```css
grid-column
grid-row
grid-auto-flow
```

---

## 31.3 Implicit tracks

You define:

```css
grid-template-columns: repeat(3, 1fr);
```

but create more placement than the explicit grid accommodates.

The browser may create implicit tracks.

Debug them using the grid overlay.

---

## 31.4 `auto-fit` vs `auto-fill`

Responsive pattern:

```css
.cards {
  display: grid;
  grid-template-columns:
    repeat(auto-fit, minmax(min(100%, 16rem), 1fr));
  gap: 1rem;
}
```

`auto-fit` and `auto-fill` differ in how empty tracks are treated.

When the grid leaves unexpected empty space, inspect which one matches your intent.

---

## 31.5 Grid area typo

```css
.layout {
  grid-template-areas:
    "header header"
    "sidebar main";
}

.main {
  grid-area: mian;
}
```

Typo: `mian`.

The item does not enter the intended named area.

---

## 31.6 Grid debugging checklist

Check:

- number of explicit rows/columns;
- gaps;
- `minmax()`;
- item minimum sizes;
- named areas;
- line numbers;
- implicit tracks;
- placement rules;
- overflow.

---

# 32. Floats, Clear, Multi-column, and Legacy Layouts

Modern layouts usually favor flexbox/grid for application layout, but legacy code may use floats.

Example:

```css
.image {
  float: left;
  margin-right: 1rem;
}
```

Text wraps around the floated image.

---

## 32.1 Parent appears to have zero height

Legacy float layouts can make a parent's visual height surprising.

A classic clearfix pattern exists, but in modern code you may be able to establish a new formatting context with:

```css
.container {
  display: flow-root;
}
```

Use the solution appropriate to the existing architecture.

## What a float does

A float shifts a box to a side and allows inline content to wrap around it. It was designed for content-wrapping patterns such as an image beside text, not as a general-purpose application layout system.

```css
.article-image {
  float: inline-start;
  margin-inline-end: 1rem;
}
```

## `clear`

`clear` prevents a box from sitting beside earlier floats on the selected side(s):

```css
.footer {
  clear: both;
}
```

If a footer unexpectedly rises beside floated columns, inspect whether clearing or a containing formatting context is missing.

## Why `flow-root` helps

```css
.container {
  display: flow-root;
}
```

creates a new block formatting context. Among other effects, this lets the container account for its floats without pseudo-element clearfix hacks.

## Legacy debugging strategy

Do not rewrite a stable legacy float layout to Grid/Flexbox in the middle of an unrelated bug fix unless the change is justified and regression-tested. First understand the existing float/clear behavior, fix the specific defect, then consider modernization as a separate refactor.

---

# 33. Table Layout Debugging

Tables have specialized layout behavior.

Proper structure:

```html
<table>
  <caption>Monthly sales</caption>
  <thead>
    <tr>
      <th scope="col">Month</th>
      <th scope="col">Sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>January</td>
      <td>₹10,000</td>
    </tr>
  </tbody>
</table>
```

---

## 33.1 Responsive table

For wide data tables, a wrapper can provide horizontal scrolling:

```css
.table-scroll {
  overflow-x: auto;
}
```

```html
<div class="table-scroll">
  <table>...</table>
</div>
```

Avoid destroying table semantics merely to make it fit.

---

## 33.2 `table-layout`

```css
table {
  table-layout: fixed;
  width: 100%;
}
```

can make column sizing more predictable, but content overflow then needs careful handling.

## Automatic vs fixed table layout

With the default automatic layout, cell content can strongly influence column widths.

With:

```css
table {
  table-layout: fixed;
  width: 100%;
}
```

the browser can use the table/column sizing rules more predictably without measuring all content the same way, but long unbreakable content can overflow.

Debug with test data such as:

```text
INV-2026-000000000000000000001
averylongemailaddress@example.example
https://example.com/a/very/long/unbroken/path
```

Then decide whether cells should wrap, clip, scroll, or expand.

## Do not convert real data tables to generic divs just for styling

Native table elements carry row/column relationships useful to browsers and assistive technology. If the information is tabular, preserve the semantic table and solve responsiveness around it.

## Sticky headers

When using:

```css
thead th {
  position: sticky;
  top: 0;
}
```

inspect the actual scrolling ancestor, overflow settings, background, and stacking context. A sticky header can technically stick but appear broken because it is transparent or covered.

---

# 34. Typography and Text Layout

Text bugs affect both readability and layout.

## 34.1 Font not loading

Symptoms:

- wrong font;
- layout shifts;
- text width differs;
- fallback font visible.

Check the Network panel and computed `font-family`.

---

## 34.2 Line-height

```css
body {
  line-height: 1.5;
}
```

Unitless line-height is often useful for inherited body text.

---

## 34.3 Long words/URLs

A long token can overflow.

Possible solution:

```css
.content {
  overflow-wrap: anywhere;
}
```

Use deliberately; verify that breaking behavior is acceptable.

---

## 34.4 Ellipsis not working

Typical single-line truncation:

```css
.title {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
```

If it still does not work, inspect whether the element actually has a constrained width.

In flex layouts, `min-width: 0` may also be relevant.

---

## 34.5 Web fonts and fallback

Example:

```css
body {
  font-family: "Inter", system-ui, sans-serif;
}
```

If the first font fails, the browser uses the next available option.

---

# 35. Backgrounds, Borders, Shadows, and Clipping

## 35.1 Background shorthand overwrites

This:

```css
.card {
  background-color: red;
  background: url(hero.png);
}
```

The shorthand can reset background subproperties.

When a background color unexpectedly disappears, inspect shorthand declarations.

---

## 35.2 Border changes element size

With `content-box`:

```css
.card {
  width: 300px;
  border: 10px solid;
}
```

the border contributes to outer size.

Use the box model to verify.

---

## 35.3 `border-radius` and child overflow

A rounded parent may not automatically clip all descendants the way you expect.

If clipping is intended, you may need appropriate overflow handling:

```css
.card {
  border-radius: 1rem;
  overflow: hidden;
}
```

But this can affect:

- shadows;
- sticky descendants;
- positioned content.

Do not add it blindly.

---

# 36. Transforms

Example:

```css
.box {
  transform: translateX(20px);
}
```

Transforms affect visual positioning differently from normal layout.

The original layout space may still be reserved.

This explains:

> "I moved the box, but the next element did not move."

Use margins/grid/flex if you want to change normal layout spacing.

---

## 36.1 Transform creates surprising positioning behavior

Transforms can affect containing blocks and stacking/compositing behavior.

If `position: fixed` or `z-index` behaves unexpectedly, inspect transformed ancestors.

## Common transform functions

```css
transform: translate(20px, 10px);
transform: scale(1.1);
transform: rotate(5deg);
```

A transform changes the rendered coordinate space. It does not normally cause surrounding normal-flow siblings to recalculate as if the transformed visual bounds were the new layout size.

## `transform-origin`

Unexpected rotation/scaling often comes from the pivot point:

```css
.box {
  transform-origin: center;
}
```

Inspect `transform-origin` when an element rotates around a surprising point.

## Stacking and containing-block effects

A non-`none` transform can create a stacking context and can affect the containing block used by descendants, including behavior that surprises developers working with `position: fixed` or absolutely positioned descendants.

This is why adding:

```css
transform: translateZ(0);
```

as a "performance trick" can change layout/stacking behavior even when the visual transform looks like a no-op.

## Debugging technique

Temporarily disable `transform` on the element and ancestors. If positioning or `z-index` suddenly behaves correctly, investigate stacking-context and containing-block effects before increasing `z-index`.

---

# 37. Transitions and Animations

Transition:

```css
.button {
  transition: background-color 150ms ease;
}
```

Animation:

```css
@keyframes pulse {
  from { opacity: 0.5; }
  to   { opacity: 1; }
}

.badge {
  animation: pulse 1s alternate infinite;
}
```

---

## 37.1 Transition does not run

Possible causes:

- property is not changing;
- declaration is overridden;
- changed property is not animating as expected;
- element is inserted already in final state;
- duration is zero;
- reduced-motion handling changes behavior.

---

## 37.2 Prefer transform/opacity for many motion effects

Animation performance depends on many factors, but transforms and opacity are often easier for browsers to optimize than properties that repeatedly require layout.

Always measure rather than relying on slogans.

---

## 37.3 Reduced motion

Respect user preferences where appropriate:

```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    scroll-behavior: auto;
  }

  .decorative-animation {
    animation: none;
    transition: none;
  }
}
```

Do not automatically remove every essential state change; preserve usability.

---

# 38. Pseudo-classes and Pseudo-elements

Pseudo-class examples:

```css
:hover
:focus
:focus-visible
:checked
:disabled
:required
:invalid
:first-child
:last-child
:nth-child()
:not()
:is()
:where()
:has()
```

Pseudo-elements:

```css
::before
::after
::first-letter
::selection
```

---

## 38.1 `::before` not visible

Common cause:

```css
.badge::before {
  background: red;
}
```

Many generated pseudo-elements need `content` to generate a box:

```css
.badge::before {
  content: "";
  display: inline-block;
  width: 0.5rem;
  height: 0.5rem;
  background: red;
}
```

---

## 38.2 `:nth-child()` confusion

HTML:

```html
<div class="list">
  <h3>Title</h3>
  <p>A</p>
  <p>B</p>
</div>
```

```css
p:nth-child(2) {
  color: red;
}
```

The first `<p>` is the second child, so it matches.

`nth-child` counts siblings, not only siblings of the same tag.

Compare with `:nth-of-type()` when that is the intended relationship.

---

# 39. Responsive Design Debugging

Responsive bugs are not only "mobile problems."

Test a range of widths.

Do not test only:

```text
desktop
tablet
phone
```

Bugs commonly appear between popular breakpoints.

---

## 39.1 Content-first debugging

Use hostile test data:

```text
VeryLongUserNameThatDoesNotFit
a-really-long-email-address@example-long-domain.example
₹99,99,99,999.00
```

Also test:

- empty values;
- one-character values;
- 10x longer descriptions;
- translated text;
- many navigation items.

---

## 39.2 Avoid fixed layouts when content is dynamic

Fragile:

```css
.card {
  width: 320px;
  height: 180px;
}
```

If content can vary, fixed height may cause overflow.

Use constraints based on the actual design need.

## Find the failure width, not the device label

Instead of starting with a named device, drag the viewport until the design first fails and record that width.

Example scratchpad:

```text
Works at: 812px
Fails at: 811px
First overflowing element: .toolbar
Cause: three fixed-width controls + gap > available inline size
```

This turns "tablet is broken" into a measurable layout constraint.

## Test more than width

Responsive failures can depend on:

- viewport height;
- browser zoom;
- text scaling;
- on-screen keyboard;
- safe areas;
- orientation;
- pointer/hover capabilities;
- reduced-motion/contrast preferences;
- component/container width rather than viewport width.

## Prefer intrinsic breakpoints

A useful principle is:

> Add a breakpoint when the content/layout needs one, not because a popular device has that width.

If a card needs two columns only when it has 35rem of space, a container query may express the requirement more accurately than a global viewport breakpoint.

---

# 40. Media Queries

Example:

```css
.layout {
  grid-template-columns: 1fr 1fr;
}

@media (max-width: 700px) {
  .layout {
    grid-template-columns: 1fr;
  }
}
```

---

## 40.1 Media query not working

Check:

- exact query syntax;
- current viewport size;
- source order;
- whether another rule still wins;
- whether the viewport meta tag is correct on mobile;
- whether the tested device mode reflects intended dimensions.

---

## 40.2 Overlapping breakpoints

Example:

```css
@media (min-width: 600px) {
  .card { color: blue; }
}

@media (max-width: 900px) {
  .card { color: red; }
}
```

From 600px through 900px, both can match.

Source order/cascade decides between otherwise equal rules.

This is not necessarily wrong, but it must be intentional.

## What a media query controls

A media query condition decides whether the rules inside it participate in the cascade. It does **not** guarantee those declarations win.

Therefore this can be true at the same time:

```text
Media query matches
Rule appears in DevTools
Property still has no visible effect
```

because a competing declaration wins later in the cascade.

## Common media features

Examples include:

```css
@media (min-width: 48rem) { ... }

@media (orientation: landscape) { ... }

@media (hover: hover) and (pointer: fine) { ... }

@media (prefers-reduced-motion: reduce) { ... }
```

Use capability/preferences queries for the behavior they describe; do not use them as unreliable proxies for a specific device model.

## Debugging with JavaScript

The browser can expose whether a media query currently matches:

```js
const query = matchMedia("(max-width: 700px)");

console.log(query.matches);
```

Expected output is a boolean:

```text
true
```

or:

```text
false
```

This is useful when CSS and JavaScript must coordinate around the same condition.

### Unit caution

Media-query relative units have defined reference behavior and should not be assumed to track an individual component's font size. If the design requirement is component size, consider a container query.

---

# 41. Container Queries

Container queries allow styles to respond to the size or features of an ancestor container rather than only the viewport.

Example:

```css
.card-wrapper {
  container-type: inline-size;
}

@container (min-width: 35rem) {
  .card {
    display: grid;
    grid-template-columns: 10rem 1fr;
  }
}
```

Use case:

The same component appears in:

- a narrow sidebar;
- a wide main column.

Viewport-based breakpoints may not know the component's actual available space. Container queries can.

---

## Debugging container queries

Check:

1. Is a query container established?
2. Is the query using the intended container?
3. Is the relevant container dimension available?
4. Does the condition currently match?
5. Does a later rule override the result?

## Named containers

A large page can have several possible query containers. Naming them makes intent clearer:

```css
.sidebar {
  container: sidebar / inline-size;
}

@container sidebar (min-width: 30rem) {
  .profile-card {
    grid-template-columns: 8rem 1fr;
  }
}
```

## What `container-type: inline-size` means

It establishes size-query containment for the inline axis so descendants can query the container's inline size.

A frequent debugging mistake is adding an `@container` rule but never establishing an eligible query container.

## Container vs media query

Use a media query when the design genuinely depends on the **environment/viewport**.

Use a container query when a reusable component should react to **the space its container gives it**.

A component may therefore switch layout at different viewport widths depending on whether it is placed in a sidebar, dialog, dashboard grid, or main content column.

## Debugging nested containers

When several ancestors are containers:

1. identify whether the query names a container;
2. inspect which ancestor is selected;
3. measure that ancestor, not the component itself;
4. confirm the condition;
5. then inspect ordinary cascade conflicts.

---

# 42. Viewport and Mobile Bugs

## 42.1 Viewport meta tag

Typical responsive document:

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

Without an appropriate viewport configuration, mobile layout can behave very differently from expectations.

---

## 42.2 `100vh` mobile issues

Mobile browser chrome can affect available viewport space.

Depending on the desired behavior, consider modern viewport units such as:

```css
min-height: 100dvh;
```

rather than assuming one viewport unit always represents the visible area you want.

Test on real devices.

---

## 42.3 Touch targets

A control that visually works with a mouse may be difficult to use on touch.

Test:

- target size;
- spacing;
- hover-only behavior;
- keyboard operation;
- focus states.

## Understand modern viewport units

Modern CSS provides several viewport-height families that help distinguish browser UI behavior:

```text
svh → small viewport height
lvh → large viewport height
dvh → dynamic viewport height
```

For an app panel intended to track the currently visible viewport as browser chrome changes, `dvh` can be useful:

```css
.app-shell {
  min-height: 100dvh;
}
```

Do not mechanically replace every `100vh`; choose the unit matching the intended behavior and target-browser requirements.

## Safe-area insets

On devices with display cutouts or edge UI, full-bleed layouts may need environment insets:

```css
.toolbar {
  padding-inline: max(1rem, env(safe-area-inset-left));
}
```

Test on real devices/emulators that expose the relevant geometry.

## Mobile debugging checklist

- zoom to 200% and test text reflow;
- rotate orientation;
- open the software keyboard;
- test long localized labels;
- inspect fixed/sticky controls;
- verify horizontal scrolling is intentional;
- check focus is not hidden behind the keyboard or fixed UI.

---

# 43. Logical Properties and Writing Modes

Physical properties:

```css
margin-left
padding-right
top
bottom
```

Logical alternatives:

```css
margin-inline-start
padding-inline-end
inset-block-start
inset-block-end
```

These can improve adaptability for:

- right-to-left languages;
- vertical writing modes;
- component reuse.

Debugging international layouts becomes easier when layout logic follows flow direction instead of hard-coded left/right assumptions.

## Think in axes instead of left/right

Logical properties describe layout relative to text flow:

```text
inline axis → the direction text runs within a line
block axis  → the direction lines/blocks are stacked
```

In a common left-to-right horizontal document:

```text
inline-start ≈ left
inline-end   ≈ right
block-start  ≈ top
block-end    ≈ bottom
```

But those mappings can change in right-to-left or vertical writing modes.

## Example

Physical:

```css
.notice {
  border-left: 4px solid;
  padding-left: 1rem;
}
```

Flow-relative:

```css
.notice {
  border-inline-start: 4px solid;
  padding-inline-start: 1rem;
}
```

The second version can adapt naturally when the inline direction changes.

## Debugging mixed codebases

If one rule sets `margin-left` and another sets `margin-inline-start`, both may affect the same physical side depending on writing direction.

When spacing changes unexpectedly:

1. inspect `direction` and `writing-mode`;
2. check both physical and logical properties in Computed styles;
3. avoid mixing the two systems for the same component without a clear reason.

Use physical properties when the design is genuinely tied to a physical side (for example, a screen-edge decoration), not merely because the page currently uses LTR text.

---

# 44. Accessibility Debugging

A page can look correct and still be functionally broken.

Accessibility debugging includes:

- semantic structure;
- accessible names;
- labels;
- keyboard access;
- focus order;
- focus visibility;
- heading structure;
- color contrast;
- alternative text;
- form errors;
- state communication.

---

## 44.1 Images

Informative image:

```html
<img
  src="chart.png"
  alt="Revenue increased from January to March."
>
```

Decorative image:

```html
<img src="decorative-wave.svg" alt="">
```

The correct alternative depends on purpose, not file type.

---

## 44.2 Buttons vs links

Use a link for navigation:

```html
<a href="/pricing">View pricing</a>
```

Use a button for an action:

```html
<button type="button">Open menu</button>
```

Styling should not replace semantics.

---

## 44.3 Heading hierarchy

Do not choose heading levels only based on font size.

Use CSS for visual size:

```css
.page-title {
  font-size: 3rem;
}
```

Choose `<h1>`, `<h2>`, etc. according to document structure.

---

## 44.4 Accessibility tree

Browser DevTools can expose accessibility information.

When debugging a control, inspect:

- role;
- accessible name;
- states;
- relationships.

---

# 45. Focus, Keyboard, and Interaction States

Never debug only with the mouse.

Try navigating using:

```text
Tab
Shift + Tab
Enter
Space
Arrow keys (where appropriate)
Escape (where appropriate)
```

---

## 45.1 Dangerous focus removal

Bad:

```css
*:focus {
  outline: none;
}
```

This can make keyboard focus difficult or impossible to see.

Prefer an intentional focus style:

```css
:focus-visible {
  outline: 3px solid currentColor;
  outline-offset: 3px;
}
```

---

## 45.2 Hover-only UI

Bad idea:

> Important content appears only on `:hover`.

Touch devices may not have equivalent hover behavior.

Provide an accessible interaction model.

## Focus is application state

A visible focus ring answers an important debugging question:

> Which control will receive the next keyboard action?

Do not judge focus only by whether a CSS outline looks attractive.

Inspect:

```js
console.log(document.activeElement);
```

after Tab/Shift+Tab navigation.

## `:focus` vs `:focus-visible`

- `:focus` matches an element that has focus.
- `:focus-visible` lets the browser apply heuristics about when a visible focus indicator is especially appropriate, commonly for keyboard-like interaction.

A common pattern is to keep a strong `:focus-visible` style while avoiding blanket focus removal.

## Native keyboard behavior differs by control

A `<button>` and a link do not have identical semantics. Test the expected keys for the chosen native element instead of forcing every control to respond to every key.

## Interaction regression checklist

After CSS changes, verify:

- focus indicator is not clipped by `overflow`;
- focused content is not hidden under a sticky header;
- a modal does not visually hide the focused control;
- disabled-looking controls are actually non-interactive when intended;
- hover styling is not the only cue for selected/expanded/error state.

---

# 46. Cross-browser Debugging

Different browsers may expose bugs because of:

- different support levels;
- platform font rendering;
- form-control styling;
- scrollbar behavior;
- OS-specific defaults;
- implementation bugs;
- vendor-specific history.

---

## 46.1 Debugging strategy

1. Reproduce in browser A.
2. Test same reduced reproduction in browser B.
3. Check whether the syntax is valid.
4. Check feature support.
5. Confirm whether the issue is browser-specific or your assumption is incorrect.
6. Use progressive enhancement/fallback where appropriate.

---

## 46.2 Avoid browser sniffing when feature detection works

Fragile mindset:

```text
If Chrome → do X
If Firefox → do Y
```

Prefer detecting the feature/capability where possible.

## Separate three kinds of differences

When browsers disagree, classify the difference before adding a workaround:

1. **Invalid/ambiguous code** — browsers recover differently.
2. **Support difference** — one browser does not implement the feature/value.
3. **Browser bug** — valid supported behavior is implemented incorrectly.

The first category should usually be fixed in your code. The second may need progressive enhancement. The third may need a narrowly scoped workaround plus a reproducible test.

## Build a reduced cross-browser case

Remove framework/app code until only the browser difference remains. Then capture:

```text
browser + version
operating system
minimal HTML/CSS
expected result
actual result
feature/support reference
```

This makes bug reports and future cleanup possible.

## Avoid permanent UA-string branches for CSS behavior

A browser name/version test can become stale and may misidentify Chromium-based browsers, embedded webviews, or future versions.

Prefer:

```css
@supports (...)
```

or:

```js
CSS.supports(...)
```

when capability detection answers the real question.

---

# 47. Feature Detection and Progressive Enhancement

CSS supports feature queries:

```css
@supports (display: grid) {
  .layout {
    display: grid;
  }
}
```

Progressive enhancement means starting from a functional baseline and adding enhancements where supported.

Example:

```css
.cards {
  display: block;
}

@supports (display: grid) {
  .cards {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
  }
}
```

This is often more robust than assuming every environment supports every enhancement identically.

## `@supports` answers a syntax/support question

Example:

```css
@supports (display: grid) {
  .layout {
    display: grid;
  }
}
```

This asks whether the browser supports that property/value combination sufficiently to accept it. It does not prove that every edge case of your intended layout behaves identically across browsers.

## Negative feature query

A fallback can also be targeted:

```css
@supports not (display: grid) {
  .layout {
    display: block;
  }
}
```

Use negative queries sparingly; a good baseline often works without special fallback rules.

## JavaScript equivalent

When JavaScript needs the same capability check:

```js
console.log(CSS.supports("display", "grid"));
```

Output:

```text
true
```

or:

```text
false
```

## Progressive enhancement mindset

Start with content and core interactions that work with a simpler feature set. Add enhancements such as advanced layout, animation, or visual effects without making them the only path to essential content/actions.

Do not confuse feature detection with browser sniffing. "This browser is X" is usually less useful than "this environment supports the capability I need."

---

# 48. Print CSS Debugging

Web pages may be printed or saved as PDF.

Example:

```css
@media print {
  nav,
  .no-print {
    display: none !important;
  }

  body {
    background: white;
  }
}
```

Debug:

- page breaks;
- hidden interactive controls;
- overflowing tables;
- link readability;
- background assumptions;
- fixed elements.

Use browser print preview during testing.

## Print is a different layout environment

Print/PDF output introduces constraints that do not exist on a scrolling screen:

- finite pages;
- page fragmentation;
- printer/PDF margins;
- limited usefulness of hover/focus controls;
- different background-color/image settings;
- long tables that may split.

## Useful break controls

For content that should avoid splitting when practical:

```css
@media print {
  .card,
  figure,
  pre {
    break-inside: avoid;
  }
}
```

For explicit section boundaries:

```css
@media print {
  .chapter {
    break-before: page;
  }
}
```

Browsers may still make pragmatic fragmentation choices when content cannot fit.

## `@page`

Basic page setup can be expressed with:

```css
@page {
  margin: 15mm;
}
```

Support for advanced paged-media features varies, so verify in the actual browsers/PDF workflow your users use.

## Print debugging checklist

1. open print preview;
2. test short and very long content;
3. check tables and code blocks;
4. verify URLs/meaning are still understandable without hover;
5. check fixed/sticky headers and footers;
6. decide whether interactive-only UI should be hidden;
7. test "background graphics" both enabled and disabled.

---

# 49. Shadow DOM and Style Isolation

Web Components may use Shadow DOM.

A normal document selector may not cross a shadow boundary the way you expect.

Symptom:

> I can see the element, but my global CSS never applies.

Inspect whether the target is inside a shadow root.

Styling options depend on how the component exposes customization, for example:

- CSS custom properties;
- `::part()`;
- component APIs.

Do not try to defeat encapsulation with arbitrary global selectors.

## Why the selector cannot "reach in"

A shadow root creates an encapsulation boundary. A selector in the outer document does not simply continue matching arbitrary internal shadow elements.

Example conceptually:

```html
<user-card></user-card>
```

The visible button inside `<user-card>` may live in its shadow tree. This outer rule:

```css
user-card button {
  color: red;
}
```

does not mean the same thing as ordinary descendant styling in light DOM.

## Component-controlled styling hooks

A component may intentionally expose:

```css
user-card {
  --accent: rebeccapurple;
}

user-card::part(action) {
  font-weight: bold;
}
```

Custom properties can cross the boundary through inheritance when the component uses them, and `::part()` styles explicitly exposed parts.

Inside component-authored shadow CSS, `:host` can style the host element based on the component's rules.

## Debugging workflow

1. inspect whether DevTools shows a shadow root;
2. determine whether the component is open/inspectable;
3. inspect its documented custom properties/parts;
4. check theme values on the host;
5. avoid adding global selectors that assume internal markup is a stable public API.

If the component exposes no styling hook, changing its internals may require changing the component itself rather than increasing CSS specificity outside it.

---

# 50. Performance-related CSS Problems

A visually correct page can still feel slow.

Potential contributors include:

- extremely large stylesheets;
- unnecessary style recalculation from application behavior;
- heavy visual effects;
- very large DOM trees;
- expensive paint areas;
- layout triggered repeatedly by scripts;
- large images and fonts;
- animations that repeatedly trigger costly work.

Use browser Performance tooling to measure.

Do not optimize based only on assumptions.

---

## 50.1 Layout shift

Unexpected movement can occur when:

- images load without reserved dimensions;
- fonts change metrics after loading;
- ads/embeds insert content;
- async components appear above existing content.

For images, reserving dimensions/aspect ratio can help layout stability.

Example:

```html
<img
  src="product.jpg"
  width="800"
  height="600"
  alt="..."
>
```

The browser can use intrinsic ratio information before the file finishes loading.

---

# 51. Linting, Validation, and Automated Checks

Manual DevTools work is essential, but automated tools catch repeatable mistakes.

## 51.1 HTML validation

HTML validators can catch problems such as:

- invalid nesting;
- duplicate attributes;
- missing required relationships;
- invalid markup.

Treat validator output as evidence, not as a substitute for understanding the browser's DOM.

---

## 51.2 CSS linting

Stylelint can help enforce and detect issues such as:

- invalid patterns;
- duplicate declarations;
- naming conventions;
- project-specific rules.

Example ecosystem command:

```bash
npx stylelint "**/*.css"
```

Exact setup depends on your project and Stylelint configuration.

---

## 51.3 Editor support

Useful editor capabilities include:

- HTML validation;
- CSS diagnostics;
- auto-completion;
- formatters;
- linters;
- browser inspection integrations.

Do not install many extensions that duplicate each other. Keep the toolchain understandable.

---

## 51.4 CI checks

A project can run validation/linting during continuous integration.

Conceptual flow:

```text
commit
  ↓
CI
  ├── HTML checks
  ├── CSS linting
  ├── tests
  └── build
```

This prevents some bugs from reaching production.

---

# 52. CSS Architecture That Prevents Bugs

Debugging starts before the bug exists.

## 52.1 Keep selectors understandable

Prefer:

```css
.card-title {}
```

over deeply coupled selectors:

```css
main .content section:nth-child(2) > div.card > header h3 {}
```

The latter is fragile when markup changes.

---

## 52.2 Separate responsibilities

Example:

```css
/* Layout */
.stack {
  display: grid;
  gap: 1rem;
}

/* Component */
.card {
  border: 1px solid;
  border-radius: 0.75rem;
}

/* State */
.card.is-selected {
  outline: 2px solid;
}
```

This is easier to reason about than one selector controlling everything.

---

## 52.3 Naming strategy

Choose a strategy and be consistent.

Examples:

```text
BEM-like
component classes
utility classes
CSS Modules
scoped component styles
design-system tokens
```

No naming system magically removes bugs. Consistency and ownership boundaries matter.

---

## 52.4 Design tokens

```css
:root {
  --space-1: 0.25rem;
  --space-2: 0.5rem;
  --space-4: 1rem;

  --radius-sm: 0.375rem;
  --radius-md: 0.75rem;
}
```

Tokens reduce random values and make visual inconsistencies easier to audit.

---

# 53. Real-world Debugging Scenarios

This section applies the earlier concepts to realistic bugs.

---

## Scenario 1: CSS file is completely ignored

### Symptom

Page displays mostly browser defaults.

### HTML

```html
<link rel="stylesheet" href="styles/app.css">
```

### Debugging

1. Open Network panel.
2. Reload.
3. Find `app.css`.
4. Check status.
5. Open response.
6. Confirm path.

### Possible cause

Actual file:

```text
/assets/css/app.css
```

### Fix

```html
<link rel="stylesheet" href="/assets/css/app.css">
```

Use the path appropriate for the deployed application.

---

## Scenario 2: One property is crossed out

### CSS

```css
.button {
  color: blue;
}

.checkout .button {
  color: red;
}
```

### Symptom

Button is red.

### Explanation

Both selectors match, but the second selector has greater specificity.

### Better debugging action

Inspect matched rules instead of adding `!important`.

---

## Scenario 3: Mobile page has horizontal scrolling

### CSS

```css
.panel {
  width: 100%;
}

.chart {
  min-width: 800px;
}
```

### Cause

The child cannot shrink below 800px.

### Possible design choices

- allow a horizontal scroll region;
- make chart responsive;
- change minimum size at smaller breakpoints.

Example scroll region:

```css
.chart-wrapper {
  overflow-x: auto;
}
```

---

## Scenario 4: Flex child refuses to shrink

```css
.row {
  display: flex;
}

.text {
  flex: 1;
}
```

The child contains a long unbreakable value.

Try after confirming the cause:

```css
.text {
  flex: 1;
  min-width: 0;
  overflow-wrap: anywhere;
}
```

`min-width: 0` and text wrapping solve different parts of the problem.

---

## Scenario 5: `z-index: 99999` still appears behind

### Symptom

A dropdown is behind another panel.

### Debugging

Inspect ancestor stacking contexts.

You may discover:

```css
.sidebar {
  position: relative;
  z-index: 1;
}

.main {
  position: relative;
  z-index: 2;
}
```

The dropdown is trapped inside the sidebar's stacking context.

### Lesson

Fix stacking hierarchy, not only the descendant's `z-index`.

---

## Scenario 6: Sticky header does not stick

```css
.header {
  position: sticky;
  top: 0;
}
```

But ancestor:

```css
.wrapper {
  overflow: auto;
}
```

The sticky element may now relate to that scrolling ancestor.

Inspect which element actually scrolls.

---

## Scenario 7: Absolute badge appears at top of page

```css
.badge {
  position: absolute;
  top: 0;
  right: 0;
}
```

Expected card-relative positioning.

Fix the positioning context:

```css
.card {
  position: relative;
}
```

provided that matches the intended containing block.

---

## Scenario 8: Ellipsis does not appear

```css
.title {
  text-overflow: ellipsis;
}
```

Incomplete.

Typical single-line pattern:

```css
.title {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
```

Also verify the element is width-constrained.

---

## Scenario 9: Grid card is wider than its column

```css
.grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
}
```

A child contains long minimum content.

Try:

```css
.grid {
  grid-template-columns:
    minmax(0, 1fr)
    minmax(0, 1fr);
}
```

and/or address the content's wrapping behavior.

---

## Scenario 10: Button submits form unexpectedly

```html
<form>
  <button>Open preview</button>
</form>
```

Use:

```html
<button type="button">Open preview</button>
```

if it is not a submit action.

---

## Scenario 11: `disabled="false"` still disables input

```html
<input disabled="false">
```

Boolean attribute is present.

Fix:

```html
<input>
```

---

## Scenario 12: CSS class exists but rule never matches

HTML:

```html
<div class="userCard"></div>
```

CSS:

```css
.user-card {}
```

Different names.

Inspect actual class names instead of assuming.

---

## Scenario 13: Direct-child selector broke after adding wrapper

Before:

```html
<div class="card">
  <h2 class="title">Title</h2>
</div>
```

After:

```html
<div class="card">
  <header>
    <h2 class="title">Title</h2>
  </header>
</div>
```

CSS:

```css
.card > .title {}
```

No longer matches.

Decide whether to update markup or selector based on intended structure.

---

## Scenario 14: Margin appears to disappear

Two vertical margins may collapse.

Use DevTools box model and inspect formatting context.

If parent-controlled spacing is suitable:

```css
.stack {
  display: grid;
  gap: 1rem;
}
```

---

## Scenario 15: Image stretches strangely

```css
.avatar {
  width: 120px;
  height: 120px;
}
```

Without appropriate fit behavior, image content may distort.

Use:

```css
.avatar {
  width: 120px;
  height: 120px;
  object-fit: cover;
}
```

---

## Scenario 16: `height: 100%` does nothing useful

```css
.child {
  height: 100%;
}
```

Inspect whether the ancestor height creates a usable percentage reference.

If the goal is a viewport-height app shell, design the whole ancestor sizing chain intentionally.

---

## Scenario 17: Modal gets clipped

Ancestor:

```css
.panel {
  overflow: hidden;
}
```

Modal is rendered inside that panel.

Even a high `z-index` cannot necessarily overcome clipping.

Possible architectural solution:

Render the overlay in an appropriate top-level overlay layer rather than inside the clipping container.

---

## Scenario 18: `position: fixed` behaves like it is inside a parent

Inspect ancestors for properties such as transforms that can alter containing-block behavior.

Reduce the example until the triggering ancestor is obvious.

---

## Scenario 19: Hover menu works on desktop, fails on touch

CSS:

```css
.menu-item:hover .submenu {
  display: block;
}
```

The interaction depends on hover.

Use an interaction model that also supports:

- keyboard;
- focus;
- touch/click.

Do not treat CSS hover alone as a complete accessible menu system.

---

## Scenario 20: Responsive media query works in desktop emulator but not phone

Check:

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

Then test actual viewport conditions and deployed CSS.

---

## Scenario 21: Background color disappears after another rule

```css
.hero {
  background-color: navy;
}

.hero {
  background: url(hero.jpg) center / cover no-repeat;
}
```

The shorthand resets background-related subproperties.

Use a combined declaration or separate properties intentionally.

---

## Scenario 22: Pseudo-element not visible

Wrong:

```css
.icon::before {
  width: 10px;
  height: 10px;
  background: red;
}
```

Add generated content and an appropriate display mode:

```css
.icon::before {
  content: "";
  display: inline-block;
  width: 10px;
  height: 10px;
  background: red;
}
```

---

## Scenario 23: Invalid form field is red before user touches it

CSS:

```css
input:invalid {
  border-color: red;
}
```

Required empty fields may already be invalid.

Design a validation-state strategy that accounts for user interaction or submission attempt.

---

## Scenario 24: A transparent element blocks clicks

```css
.overlay {
  opacity: 0;
}
```

It can still occupy space and receive pointer interaction.

Depending on intended behavior, use a different hiding strategy.

Do not assume transparent means nonexistent.

---

## Scenario 25: `display: none` removes animation target

If an element starts at:

```css
display: none;
```

there is no rendered box to transition in the same way as a visible rendered state.

Consider an animation strategy based on properties appropriate to the component lifecycle.

---

## Scenario 26: Footer floats halfway up page

The page has little content and no full-page layout strategy.

Possible layout:

```css
body {
  min-height: 100dvh;
  display: flex;
  flex-direction: column;
}

main {
  flex: 1;
}
```

This allows the main region to fill remaining vertical space.

---

## Scenario 27: Text is vertically misaligned inside button

Inspect:

- line-height;
- padding;
- font metrics;
- inline icons;
- flex alignment.

A robust button pattern:

```css
.button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
}
```

---

## Scenario 28: SVG icon inherits unexpected color

SVG may use:

```css
fill: currentColor;
```

Then the icon follows the element's computed `color`.

Inspect inherited `color`.

---

## Scenario 29: Component works alone but breaks in sidebar

The problem may be container width rather than viewport width.

Possible solution:

- make internal layout fluid;
- use container queries;
- avoid hard-coded global breakpoints inside reusable components.

---

## Scenario 30: Production CSS differs from local CSS

Check:

- build pipeline;
- minification;
- generated filenames;
- old deployment artifact;
- CDN/service-worker cache;
- CSS ordering;
- environment-specific asset path.

Compare the network-delivered file, not only your source editor.

---

# 54. Fast Diagnostic Decision Tree

Use this when you need a quick path.

```text
START
  |
  |-- Is the element visible in the DOM?
  |       |
  |       |-- NO → HTML/rendering/JS/conditional issue
  |       |
  |       └-- YES
  |
  |-- Is the expected stylesheet loaded?
  |       |
  |       |-- NO → path/network/cache/build issue
  |       |
  |       └-- YES
  |
  |-- Does the expected selector match?
  |       |
  |       |-- NO → selector/DOM/state/media-query issue
  |       |
  |       └-- YES
  |
  |-- Is the declaration valid?
  |       |
  |       |-- NO → syntax/property/value issue
  |       |
  |       └-- YES
  |
  |-- Is the declaration overridden?
  |       |
  |       |-- YES → cascade/layer/importance/specificity/order
  |       |
  |       └-- NO
  |
  |-- Is computed value what you expected?
  |       |
  |       |-- NO → inheritance/unit/percentage/variable/constraint issue
  |       |
  |       └-- YES
  |
  |-- Is geometry wrong?
  |       |
  |       |-- YES → box model/flex/grid/position/overflow/containing block
  |       |
  |       └-- NO
  |
  |-- Is visibility/overlap wrong?
  |       |
  |       |-- YES → stacking/clipping/opacity/visibility/transform
  |       |
  |       └-- NO
  |
  |-- Only at certain width?
  |       |
  |       |-- YES → responsive/media/container/min-content issue
  |       |
  |       └-- NO
  |
  |-- Only in one browser?
          |
          |-- YES → support/default/platform/browser-specific investigation
          |
          └-- NO → reduce reproduction further
```

---

# 55. Master Debugging Checklists

## 55.1 CSS not applying

- [ ] Is the CSS file loaded?
- [ ] Is the URL correct?
- [ ] Is the selector correct?
- [ ] Does the selector match the actual DOM?
- [ ] Is the rule inside a media/container query that currently matches?
- [ ] Is the property name valid?
- [ ] Is the value valid?
- [ ] Is another declaration winning?
- [ ] Is `!important` involved?
- [ ] Is an inline style involved?
- [ ] Is a cascade layer involved?
- [ ] Is a custom property unresolved?
- [ ] Are you editing the file actually served to the browser?
- [ ] Is cached/generated CSS involved?

---

## 55.2 Wrong spacing

- [ ] Check margin.
- [ ] Check padding.
- [ ] Check `gap`.
- [ ] Check line-height.
- [ ] Check inline baseline behavior.
- [ ] Check margin collapsing.
- [ ] Check absolute-positioned children.
- [ ] Check default browser margins on headings/paragraphs.
- [ ] Check box sizing.

---

## 55.3 Horizontal overflow

- [ ] Check fixed widths.
- [ ] Check `min-width`.
- [ ] Check images.
- [ ] Check tables.
- [ ] Check long words/URLs.
- [ ] Check `white-space: nowrap`.
- [ ] Check flex item minimum sizing.
- [ ] Check grid min-content sizing.
- [ ] Check negative margins.
- [ ] Check transforms.
- [ ] Check absolute/fixed-positioned elements.
- [ ] Check viewport-unit assumptions.

---

## 55.4 Flexbox issue

- [ ] Confirm flex container.
- [ ] Confirm `flex-direction`.
- [ ] Check main vs cross axis.
- [ ] Check wrapping.
- [ ] Check `gap`.
- [ ] Inspect grow/shrink/basis.
- [ ] Try `min-width: 0` only if minimum sizing is the cause.
- [ ] Check child intrinsic content.
- [ ] Check auto margins.
- [ ] Check nested flex containers.

---

## 55.5 Grid issue

- [ ] Inspect grid overlay.
- [ ] Check explicit tracks.
- [ ] Check implicit tracks.
- [ ] Check item placement.
- [ ] Check `minmax()`.
- [ ] Check long content.
- [ ] Check named-area spelling.
- [ ] Check gaps.
- [ ] Check auto-placement.

---

## 55.6 `z-index` issue

- [ ] Is stacking really the problem?
- [ ] Is the element positioned/participating as expected?
- [ ] Which ancestors create stacking contexts?
- [ ] Is an ancestor stacking context below another?
- [ ] Is overflow clipping the element?
- [ ] Is a transform involved?
- [ ] Can the overlay be moved to a better DOM layer?
- [ ] Avoid escalating to huge arbitrary `z-index` values.

---

## 55.7 Responsive issue

- [ ] Test intermediate widths.
- [ ] Check viewport meta.
- [ ] Check min/max widths.
- [ ] Check wrapping.
- [ ] Check media query overlap.
- [ ] Check container size.
- [ ] Test long content.
- [ ] Test zoom.
- [ ] Test landscape/portrait.
- [ ] Test real device when important.

---

## 55.8 Accessibility issue

- [ ] Use semantic element.
- [ ] Check accessible name.
- [ ] Check label association.
- [ ] Test keyboard.
- [ ] Check focus visibility.
- [ ] Check heading structure.
- [ ] Check alternative text.
- [ ] Check error communication.
- [ ] Check color contrast.
- [ ] Inspect accessibility tree when useful.

---

# 56. Common Anti-patterns

## 56.1 `!important` everywhere

Why bad:

- masks cascade problems;
- makes overrides harder;
- creates escalation.

Use only when you understand the priority requirement.

---

## 56.2 Giant selectors

Bad:

```css
html body #app main section.content div.card ul li a.button.primary {}
```

Problems:

- fragile;
- difficult to override;
- tightly coupled to DOM structure.

---

## 56.3 Arbitrary z-index scale

Bad:

```css
z-index: 9999999999;
```

Prefer a controlled layer system.

Example conceptual tokens:

```css
:root {
  --z-base: 0;
  --z-dropdown: 10;
  --z-sticky: 20;
  --z-modal: 30;
  --z-toast: 40;
}
```

Remember: token values do not remove stacking-context boundaries.

---

## 56.4 Fixed heights for dynamic content

```css
.card {
  height: 200px;
}
```

If content changes, it may overflow.

Prefer natural height unless the design truly requires a fixed frame.

---

## 56.5 Hiding overflow globally

```css
body {
  overflow-x: hidden;
}
```

This can hide the symptom and make content unreachable.

---

## 56.6 Removing outlines

```css
button:focus {
  outline: none;
}
```

If you remove a default focus indicator, provide an accessible replacement.

---

## 56.7 Using `<br>` for layout spacing

Bad:

```html
<h2>Title</h2>
<br><br><br>
<p>Body</p>
```

Use CSS spacing:

```css
h2 {
  margin-bottom: 2rem;
}
```

---

## 56.8 Using empty elements for spacing

Bad:

```html
<div class="spacer"></div>
```

Use layout properties such as:

```css
gap
margin
padding
```

unless the element has genuine semantic/layout purpose.

---

# 57. Debugging Exercises

Try to solve these before reading the hints.

---

## Exercise 1: Why is the text red?

```html
<p id="message" class="message">Hello</p>
```

```css
#message {
  color: red;
}

.message {
  color: blue;
}
```

### Hint

Compare selector specificity.

### Answer

The ID selector has greater specificity than the class selector in this competition, so red wins.

---

## Exercise 2: Why is the child outside the screen?

```css
.parent {
  width: 320px;
}

.child {
  width: 100%;
  padding: 40px;
}
```

### Hint

Check `box-sizing`.

### Possible fix

```css
.child {
  box-sizing: border-box;
}
```

---

## Exercise 3: Why does the selector not match?

```html
<div class="card">
  <header>
    <h2 class="title">Test</h2>
  </header>
</div>
```

```css
.card > .title {
  color: red;
}
```

### Answer

`.title` is not a direct child of `.card`.

---

## Exercise 4: Why does `z-index` fail?

```css
.left {
  position: relative;
  z-index: 1;
}

.right {
  position: relative;
  z-index: 2;
}

.dropdown {
  position: absolute;
  z-index: 9999;
}
```

The dropdown is inside `.left` and must overlap `.right`.

### Hint

Compare the ancestor stacking contexts.

---

## Exercise 5: Why does the page overflow?

```css
.row {
  display: flex;
  width: 100%;
}

.main {
  flex: 1;
}

.code {
  white-space: nowrap;
}
```

### Investigation

Inspect minimum sizing and long unbreakable content.

Potential tools:

```css
.main {
  min-width: 0;
}

.code {
  overflow-wrap: anywhere;
}
```

Use only the changes your design needs.

---

# 58. Glossary

## Cascade

The process that decides which competing CSS declaration takes precedence.

## Specificity

A selector weight used as part of the cascade.

## Inheritance

The mechanism by which some computed property values are passed from ancestors to descendants.

## DOM

Browser representation of the document structure.

## CSSOM

A representation of CSS/style information used by the browser.

## Computed value

A resolved CSS value after the browser processes cascade/inheritance and value computation.

## Box model

The content, padding, border, and margin areas associated with a CSS box.

## Containing block

The reference box used for certain positioning and sizing calculations.

## Formatting context

A layout environment that determines how boxes participate in layout.

## Stacking context

A local stacking environment that groups elements for painting order.

## Intrinsic size

A size influenced by the content or replaced resource itself.

## Overflow

Content extending beyond a box's available dimensions.

## Reflow/Layout

The geometry-calculation stage where element sizes and positions are determined.

## Paint

Drawing visual parts such as backgrounds, text, borders, and shadows.

## Pseudo-class

A selector component representing a state or structural condition, such as `:hover`.

## Pseudo-element

A selector representing a generated or special subpart, such as `::before`.

## Media query

A conditional CSS mechanism based on media/environment features.

## Container query

A conditional styling mechanism based on a containing element's features or size.

## Minimal reproduction

The smallest example that still demonstrates a bug.

## Regression

A previously working behavior that breaks after a change.

---

# 59. Recommended Learning and Reference Resources

Use standards/documentation as your source of truth when behavior is unclear.

## HTML

- MDN HTML: https://developer.mozilla.org/en-US/docs/Web/HTML
- WHATWG HTML Living Standard: https://html.spec.whatwg.org/

## CSS

- MDN CSS: https://developer.mozilla.org/en-US/docs/Web/CSS
- MDN CSS Specificity: https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Cascade/Specificity
- MDN CSS Box Model: https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Box_model
- MDN Handling Common HTML and CSS Problems: https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Testing/HTML_and_CSS

## Browser DevTools

- Chrome DevTools CSS: https://developer.chrome.com/docs/devtools/css
- Chrome DevTools Grid: https://developer.chrome.com/docs/devtools/css/grid
- Chrome DevTools Flexbox: https://developer.chrome.com/docs/devtools/css/flexbox
- Firefox Developer Tools: https://firefox-source-docs.mozilla.org/devtools-user/

## Accessibility

- W3C WAI Introduction: https://www.w3.org/WAI/fundamentals/accessibility-intro/
- W3C WAI Forms Tutorial: https://www.w3.org/WAI/tutorials/forms/
- W3C WAI Page Structure Tutorials: https://www.w3.org/WAI/tutorials/page-structure/

## Validation / quality tools

- W3C Nu HTML Checker: https://validator.w3.org/nu/
- Stylelint: https://stylelint.io/

---

# 60. Final Debugging Principles

Remember these rules:

1. **Inspect before editing.**
2. **Reproduce before guessing.**
3. **Check the DOM, not only the source file.**
4. **Verify the stylesheet actually loaded.**
5. **A selector must match before specificity matters.**
6. **A valid declaration can still lose the cascade.**
7. **Computed styles tell you what the browser finally chose.**
8. **Box-model inspection solves many spacing and sizing mysteries.**
9. **Flexbox and Grid have intrinsic/minimum sizing behavior.**
10. **Large `z-index` values cannot escape stacking contexts.**
11. **`overflow: hidden` can hide symptoms and clip useful content.**
12. **Test intermediate viewport widths, not only preset devices.**
13. **Use hostile content to expose fragile layouts.**
14. **A visually correct page can still have semantic or accessibility bugs.**
15. **Browser DevTools is an experiment environment—use it.**
16. **Reduce complex bugs to a minimal reproduction.**
17. **Understand the cause before adding `!important`.**
18. **Prefer small, local fixes over global hacks.**
19. **Validate the fix in multiple states and screen sizes.**
20. **The best debugging skill is building a correct mental model of how the browser works.**

---

# Appendix A: A Practical Debugging Scratchpad Template

Copy this into an issue or notes file when debugging a difficult UI problem.

````md
## Bug

What is visibly wrong?

## Expected behavior

What should happen?

## Actual behavior

What happens instead?

## Reproduction steps

1.
2.
3.

## Environment

- Browser:
- OS:
- Viewport:
- Zoom:
- Input method:
- Theme:

## DOM element

Selector / markup:

## Expected CSS rule

```css
...
```

## Computed value

Property:
Expected:
Actual:

## Competing declarations

1.
2.
3.

## Parent constraints

- width:
- min-width:
- max-width:
- overflow:
- display:
- position:
- transform:

## Experiments

- Disabled:
- Changed:
- Result:

## Root cause

...

## Final fix

...

## Regression tests

- [ ] desktop
- [ ] mobile
- [ ] long content
- [ ] keyboard
- [ ] browser B
````

---

# Appendix B: Temporary Debug CSS Toolkit

Use temporarily during development.

## Outline every element

```css
* {
  outline: 1px solid rgba(255, 0, 0, 0.15);
}
```

## Highlight a suspicious element

```css
.debug {
  outline: 3px solid magenta !important;
  background: rgba(255, 0, 255, 0.08) !important;
}
```

## Show focus visibly during keyboard testing

```css
:focus {
  outline: 3px solid currentColor !important;
  outline-offset: 3px !important;
}
```

Remove temporary debugging styles before production unless they are intentionally part of the design.

---

# Appendix C: Useful Console Snippets for HTML/CSS Debugging

## Find one element

```js
document.querySelector(".card")
```

## Find all matching elements

```js
document.querySelectorAll(".card")
```

## Check computed style

```js
getComputedStyle(document.querySelector(".card")).display
```

## Check a custom property

```js
getComputedStyle(document.querySelector(".card"))
  .getPropertyValue("--card-color")
```

## Check document width overflow

```js
({
  scrollWidth: document.documentElement.scrollWidth,
  clientWidth: document.documentElement.clientWidth
})
```

## Find elements extending beyond viewport width

```js
[...document.querySelectorAll("*")].filter((el) => {
  const r = el.getBoundingClientRect();
  return r.right > document.documentElement.clientWidth || r.left < 0;
});
```

This is a diagnostic aid, not proof that every returned element is a bug. Transforms, intentional off-canvas UI, and animations can produce legitimate results.

---

# Appendix D: Beginner Debugging Practice Project

Create this file:

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Debug Practice</title>

  <style>
    *,
    *::before,
    *::after {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      font-family: system-ui, sans-serif;
    }

    .page {
      width: min(100% - 2rem, 70rem);
      margin-inline: auto;
    }

    .cards {
      display: grid;
      grid-template-columns:
        repeat(auto-fit, minmax(min(100%, 16rem), 1fr));
      gap: 1rem;
    }

    .card {
      border: 1px solid #bbb;
      border-radius: 0.75rem;
      padding: 1rem;
    }

    .card img {
      display: block;
      width: 100%;
      aspect-ratio: 16 / 9;
      object-fit: cover;
      border-radius: 0.5rem;
    }

    .actions {
      display: flex;
      flex-wrap: wrap;
      gap: 0.5rem;
      margin-top: 1rem;
    }

    .button {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      min-height: 2.5rem;
      padding-inline: 1rem;
      border: 1px solid;
      border-radius: 0.5rem;
      text-decoration: none;
    }

    .button:focus-visible {
      outline: 3px solid currentColor;
      outline-offset: 3px;
    }
  </style>
</head>

<body>
  <main class="page">
    <h1>Debug Practice</h1>

    <section class="cards">
      <article class="card">
        <img
          src="https://picsum.photos/800/450"
          alt="Random practice image"
          width="800"
          height="450"
        >

        <h2>Example card</h2>

        <p>
          Resize the browser, inspect this card, change its CSS in
          DevTools, and observe the computed box model.
        </p>

        <div class="actions">
          <a class="button" href="#">Details</a>
          <button class="button" type="button">Save</button>
        </div>
      </article>
    </section>
  </main>
</body>
</html>
```

Practice tasks:

1. Make the card overflow and diagnose it.
2. Add a conflicting selector and inspect specificity.
3. Add `min-width: 600px` and reproduce mobile overflow.
4. Add an absolute badge and debug its containing block.
5. Create two stacking contexts and reproduce a `z-index` surprise.
6. Add a long URL and fix wrapping.
7. Remove the viewport meta tag and observe mobile emulation.
8. Add a pseudo-element and intentionally forget `content`.
9. Add a form and test invalid states.
10. Navigate using only the keyboard.

---

# Appendix E: One-Minute Debugging Routine

When a CSS problem appears, do this:

```text
1. Inspect the element.
2. Confirm DOM/class/state.
3. Confirm rule appears.
4. Confirm property is valid.
5. Check crossed-out declarations.
6. Check computed value.
7. Inspect box model.
8. Inspect parent layout.
9. Disable suspicious constraints.
10. Make one temporary change.
11. Confirm the hypothesis.
12. Implement the smallest source fix.
```

If you cannot explain the root cause after step 12, you have probably patched the symptom rather than fully debugged the problem.

---


# Appendix F: Advanced Modern CSS Debugging

These topics appear frequently in modern component systems and design systems. You do not need to memorize every feature. Learn how each one changes the browser's sizing, selector, or cascade decisions.

---

## F.1 Intrinsic sizing: `min-content`, `max-content`, and `fit-content`

Intrinsic sizing means that the content itself helps determine the size.

Example:

```css
.sidebar {
  width: max-content;
}
```

This can produce a width based on the content's preferred unwrapped size.

Useful keywords include:

```css
min-content
max-content
fit-content
```

### Typical debugging problem

A column becomes much wider than expected because a long piece of content establishes a large minimum or preferred size.

Inspect:

- long words;
- URLs;
- `white-space`;
- minimum track sizing;
- flex/grid automatic minimums.

### Grid example

```css
.layout {
  display: grid;
  grid-template-columns: max-content 1fr;
}
```

If the first column contains unexpectedly wide content, it can consume more horizontal space than expected.

When you need a hard upper bound, combine sizing rules deliberately rather than hoping the content will shrink.

---

## F.2 `min()`, `max()`, and `clamp()`

These functions help express fluid constraints.

### `min()`

```css
width: min(100%, 70rem);
```

Use the smaller result.

### `max()`

```css
padding-inline: max(1rem, 4vw);
```

Use the larger result.

### `clamp()`

```css
font-size: clamp(1.5rem, 3vw, 3rem);
```

Conceptually:

```text
minimum ≤ preferred fluid value ≤ maximum
```

### Debugging `clamp()`

If the output surprises you:

1. inspect the computed value;
2. calculate the preferred expression at the current viewport/container size;
3. check which bound is currently winning.

Do not assume `clamp()` is "responsive magic." It is still a numeric constraint.

---

## F.3 `calc()`

Example:

```css
main {
  min-height: calc(100dvh - 4rem);
}
```

`calc()` can combine compatible values.

Common mistakes:

```css
width: calc(100%-2rem);
```

Prefer clear operator spacing:

```css
width: calc(100% - 2rem);
```

Another common problem is using an expression that is mathematically valid but based on the wrong reference size.

Always inspect the computed value.

---

## F.4 CSS nesting

Modern CSS can express nested selectors.

Conceptual example:

```css
.card {
  padding: 1rem;

  & .title {
    font-weight: 700;
  }

  &:hover {
    box-shadow: 0 0 0 1px currentColor;
  }
}
```

### Debugging nesting

When nested CSS does not behave as expected:

- inspect the final selector logic;
- understand what `&` represents;
- check whether build tools transform your source;
- verify the CSS actually delivered to the browser;
- distinguish native CSS nesting from preprocessor syntax.

Do not assume Sass/LESS nesting syntax and native CSS syntax are always interchangeable.

---

## F.5 `@scope`

Scoped styling can limit where selectors apply.

Conceptual form:

```css
@scope (.article) {
  h2 {
    margin-block-start: 2rem;
  }
}
```

This can help large applications avoid styles leaking into unrelated components.

### Debugging question

If a rule appears correct but is missing from another component, ask:

> Is this declaration intentionally limited by a scope boundary?

When adopting newer CSS features, verify the browser support required by your project.

---

## F.6 Subgrid

Subgrid allows a nested grid to participate in tracks established by an ancestor grid.

Conceptual example:

```css
.cards {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}

.card {
  display: grid;
  grid-template-rows: subgrid;
}
```

### Debugging subgrid

Inspect:

- whether the child is actually a grid item;
- which axis uses `subgrid`;
- the ancestor's explicit tracks;
- gaps and track inheritance behavior.

Grid overlays are extremely useful here.

---

## F.7 CSS containment

Containment can limit how a subtree participates in layout, style, or paint calculations.

Example forms include:

```css
contain: layout;
contain: paint;
contain: content;
```

Containment can improve isolation/performance, but it can also change assumptions about:

- sizing;
- overflow;
- positioning;
- painting.

If a component behaves correctly until `contain` is added, treat containment as part of the layout model, not only as a performance flag.

---

## F.8 `content-visibility`

Example:

```css
.long-section {
  content-visibility: auto;
}
```

This can allow the browser to skip some rendering work for off-screen content.

When debugging, be aware that rendering optimizations can affect what DevTools shows at different moments and can interact with intrinsic sizing.

Use measurement and documentation before adding it to every section.

---

## F.9 Registered custom properties with `@property`

A custom property can be registered with type information.

Conceptual example:

```css
@property --progress {
  syntax: "<number>";
  inherits: false;
  initial-value: 0;
}
```

Then:

```css
.progress {
  --progress: 0.5;
}
```

This becomes especially relevant for animation and validation of custom property values.

Debug:

- syntax descriptor;
- inheritance;
- initial value;
- actual property value.

---

## F.10 Scroll snapping

Example:

```css
.gallery {
  display: flex;
  overflow-x: auto;
  scroll-snap-type: x mandatory;
}

.gallery > * {
  scroll-snap-align: start;
}
```

### Common problems

- snap points feel too aggressive;
- child width is wrong;
- hidden overflow prevents intended scrolling;
- nested scrolling areas compete;
- focus moves to an item but scroll position feels unexpected.

Debug the scroll container first.

---

## F.11 `overscroll-behavior`

Nested scroll areas can propagate scroll behavior to ancestors.

Example:

```css
.modal-body {
  overflow: auto;
  overscroll-behavior: contain;
}
```

Use only when you actually need to control scroll chaining.

If scrolling becomes "stuck," inspect:

- which element scrolls;
- overflow;
- overscroll behavior;
- touch behavior;
- fixed/sticky ancestors.

---

# Appendix G: HTML Document-Level Debugging

---

## G.1 Correct document skeleton

A good starting point:

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Page title</title>
</head>
<body>
  <main>
    ...
  </main>
</body>
</html>
```

Each part has a different purpose.

### `<!doctype html>`

Tells modern browsers to use standards-oriented HTML rendering behavior rather than old compatibility modes.

If an old page has strange box-model/layout differences, inspect its doctype.

### `lang`

```html
<html lang="en">
```

Communicates the page language to user agents and assistive technologies.

### Charset

```html
<meta charset="utf-8">
```

If characters appear corrupted, encoding is part of the debugging checklist.

---

## G.2 Character encoding bugs

Symptom:

```text
₹ becomes strange characters
é becomes mojibake
```

Check:

- document encoding declaration;
- server response encoding;
- file encoding;
- database/API encoding if data is dynamic.

Do not try to fix an encoding problem with CSS fonts until you know the characters themselves are correct.

---

## G.3 Base URL surprises

HTML can contain:

```html
<base href="/app/">
```

This changes how relative URLs are resolved.

If many links/images suddenly point to unexpected locations, inspect whether a `<base>` element exists.

---

## G.4 `hidden` attribute

```html
<section hidden>
  Secret panel
</section>
```

If an element appears in the DOM but not visually, inspect attributes as well as CSS.

The issue may not be a `display` rule you wrote.

---

## G.5 `details` and `summary`

Native disclosure:

```html
<details>
  <summary>Advanced settings</summary>
  <p>...</p>
</details>
```

Debug:

- `open` attribute/state;
- focus styles;
- custom marker styling;
- nested interactive controls.

Use native semantics unless your design genuinely requires a custom widget.

---

## G.6 Dialog debugging

Native dialog:

```html
<dialog id="confirm">
  <p>Delete item?</p>
  <button type="button">Cancel</button>
</dialog>
```

Dialogs have special top-layer/modal behavior when used through their appropriate APIs.

When a dialog behaves differently from a normal absolutely positioned element, do not debug it as though it were just another `<div>`.

Check:

- whether it is open;
- whether it is modal or non-modal;
- focus handling;
- backdrop styling;
- form/button behavior inside it.

---

## G.7 Iframe layout

Example:

```html
<iframe
  src="report.html"
  title="Sales report">
</iframe>
```

An iframe contains a separate document.

A selector in the parent document does not simply style arbitrary content inside the child document.

Debug:

- iframe dimensions;
- iframe URL;
- child document;
- cross-origin restrictions;
- responsive sizing.

---

## G.8 Script loading can create "HTML/CSS" symptoms

Example:

```html
<script src="app.js" defer></script>
```

A JavaScript application may:

- add classes;
- remove classes;
- inject style attributes;
- render elements conditionally;
- create portals/overlays.

If CSS seems to "change by itself," watch the DOM and attributes while reproducing the bug.

HTML/CSS debugging sometimes requires proving that JavaScript is mutating the inputs.

---

# Appendix H: Browser Defaults, Resets, and Normalization

Browsers provide built-in user-agent styles.

For example, headings normally appear larger/bolder and paragraphs have default spacing.

If you never wrote:

```css
h1 {
  font-size: ...;
}
```

but the heading is still large, DevTools may show a user-agent stylesheet.

---

## H.1 Debugging browser defaults

Inspect the matched styles.

Do not assume every visible rule comes from your stylesheet.

Common defaults affect:

- headings;
- paragraphs;
- lists;
- buttons;
- inputs;
- fieldsets;
- links;
- tables.

---

## H.2 Simple reset example

```css
*,
*::before,
*::after {
  box-sizing: border-box;
}

body {
  margin: 0;
}

img,
picture,
video,
canvas,
svg {
  max-width: 100%;
}

button,
input,
textarea,
select {
  font: inherit;
}
```

A reset changes defaults. It is not automatically "better"; it establishes a project baseline.

---

## H.3 Framework reset conflicts

UI frameworks may ship:

- resets;
- base typography;
- utility classes;
- component styles;
- variables.

If a plain element behaves differently after adding a framework, inspect framework rules before creating overrides.

---

# Appendix I: Framework and Utility-CSS Debugging

The core browser rules in this handbook still apply when using Bootstrap, Tailwind CSS, component frameworks, CSS Modules, or CSS-in-JS.

Framework abstractions do not replace the cascade.

---

## I.1 Utility class conflict

Example HTML:

```html
<div class="hidden md:block custom-panel">
```

If a utility framework generates responsive display rules, your `.custom-panel` declaration may compete with generated CSS.

Debug using the **actual generated stylesheet**, not only framework documentation.

---

## I.2 Build-time class generation

Some utility systems scan source files to determine which classes to emit.

A dynamically assembled class can fail to appear in the generated CSS depending on the tool configuration.

Symptom:

> Class exists in HTML at runtime, but there is no matching generated CSS rule.

Debug:

1. inspect DOM;
2. search Styles panel;
3. search delivered CSS;
4. inspect build configuration/content scanning.

This is a build problem, not selector specificity.

---

## I.3 CSS Modules

Source:

```css
.title {
  color: red;
}
```

A build system may transform the class into a generated name.

If hand-written HTML uses:

```html
<div class="title">
```

it may not match the generated module class.

Debug the rendered DOM and generated CSS.

---

## I.4 CSS-in-JS

Runtime style systems can insert `<style>` elements dynamically.

Possible issues:

- injection order;
- server/client mismatch;
- theme/provider state;
- generated specificity;
- duplicate library versions.

Again, DevTools shows the browser's final reality.

---

# Appendix J: Production-Only HTML/CSS Bugs

Production differs from local development.

---

## J.1 Minification

Minification removes whitespace and may combine files.

If a production stylesheet is difficult to read:

- use source maps if available;
- search for selectors/property values;
- inspect source references in DevTools.

Do not edit the minified production file as the long-term fix unless that is truly your source of record.

---

## J.2 Hashed asset filenames

Production may generate:

```text
app.3f82a1.css
```

instead of:

```text
app.css
```

A stale HTML document can reference an old hash that no longer exists.

Symptoms:

```text
404 stylesheet
unstyled page
only some users affected
```

Check the exact request URL in the Network panel.

---

## J.3 CDN/cache mismatch

A deployment can temporarily combine:

- new HTML;
- old CSS;
- old JavaScript;
- stale service-worker content.

Debug using response headers and actual downloaded assets rather than assuming the local build is what users received.

---

## J.4 Content Security Policy

Security policy can block certain resource or style patterns.

If DevTools Console reports that a stylesheet or inline style is blocked by policy, changing selector specificity will never fix it.

Treat console security errors as first-class debugging evidence.

---

## J.5 Source order changed by bundling

Development:

```text
base.css
components.css
overrides.css
```

Production bundler accidentally emits:

```text
overrides.css
base.css
components.css
```

The page can look different even though every individual declaration is unchanged.

Compare generated order.

---

# Appendix K: Additional Real-World Scenarios

---

## Scenario 31: `width: 100vw` creates horizontal scrolling

A page uses:

```css
.hero {
  width: 100vw;
}
```

but the normal containing block already fills the available width.

Depending on scrollbar/layout conditions, viewport width can produce a result wider than the content area.

Try whether:

```css
.hero {
  width: 100%;
}
```

better expresses the design.

Do not make the substitution automatically; understand the intended reference box.

---

## Scenario 32: A grid item spans the wrong tracks

```css
.item {
  grid-column: 1 / 4;
}
```

The developer assumed "three columns" means ending at line 3.

Grid lines surround tracks. Three columns have four boundary lines.

Use the DevTools line-number overlay.

---

## Scenario 33: `margin: auto` seems magical in flexbox

```css
.actions {
  display: flex;
}

.logout {
  margin-left: auto;
}
```

The auto margin absorbs available space and pushes the item.

When an item jumps away from siblings, inspect auto margins before changing `justify-content`.

---

## Scenario 34: A hidden checkbox still affects layout

```css
.checkbox {
  opacity: 0;
}
```

Opacity does not remove the box.

If it should be visually hidden while remaining accessible, use a deliberate visually-hidden technique appropriate to the control—not random zero dimensions or opacity without understanding interaction.

---

## Scenario 35: `overflow: hidden` breaks sticky positioning

A wrapper was given:

```css
.wrapper {
  overflow: hidden;
}
```

to crop a decoration.

Later a sticky child no longer behaves as expected.

The overflow change altered the scrolling/layout context.

Reconsider whether clipping belongs on another nested element.

---

## Scenario 36: `transform: scale()` changes appearance but not layout allocation

```css
.card {
  transform: scale(0.8);
}
```

The card looks smaller, but surrounding layout may still reserve its original geometry.

If you need smaller layout dimensions, change sizing/layout rather than only transforming the visual result.

---

## Scenario 37: Icon and text do not align

HTML:

```html
<button class="save">
  <svg>...</svg>
  Save
</button>
```

Instead of adjusting SVG with arbitrary `top: 2px`, use a predictable inline-flex layout:

```css
.save {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
}
```

Then inspect SVG intrinsic dimensions.

---

## Scenario 38: CSS variable changes in the wrong subtree

```css
:root {
  --accent: blue;
}

.sidebar {
  --accent: purple;
}

.button {
  background: var(--accent);
}
```

A button inside `.sidebar` becomes purple.

This is inheritance/scope, not a random override.

---

## Scenario 39: Media query is correct but overridden later

```css
@media (max-width: 600px) {
  .nav {
    display: none;
  }
}

.nav {
  display: flex;
}
```

If the later rule has equal cascade priority and matches, it can restore `display: flex`.

Move/organize rules intentionally or use a clearer architecture.

---

## Scenario 40: Framework class disappears after production build

Runtime markup:

```html
<div class="bg-${theme}">
```

The build tool may not detect the possible generated class names.

Inspect the generated CSS. If the class is absent, no amount of DevTools specificity editing will make it exist in production.

---

# Appendix L: Debugging by Symptom

Use this index when you know the symptom but not the CSS concept.

| Symptom | First concepts to inspect |
|---|---|
| Style not applied | resource loading, selector matching, cascade |
| Property crossed out | cascade, specificity, source order |
| Element too wide | box model, min-width, intrinsic sizing, overflow |
| Element too tall | content, fixed height, line-height, min-height |
| Horizontal scrollbar | overflow, min-content, fixed width, transforms |
| Dropdown behind content | stacking context, clipping |
| Sticky not working | scroll container, overflow, inset |
| Absolute item in wrong place | containing block |
| Grid columns overflow | minmax, intrinsic sizing |
| Flex child overflow | auto minimum size, long content |
| Text refuses to wrap | white-space, overflow-wrap, intrinsic width |
| Ellipsis missing | width constraint, overflow, white-space |
| Image distorted | width/height, aspect ratio, object-fit |
| Blank space around page | body/default margin, container sizing |
| Mobile layout zoomed out | viewport metadata |
| CSS differs in production | build output, order, cache, asset hash |
| Keyboard focus invisible | focus CSS |
| Form submits unexpectedly | button type/form semantics |
| `disabled="false"` disabled | HTML boolean attributes |
| Pseudo-element missing | `content`, display, size |
| Animation does not run | state change, overridden values, duration |
| Component breaks in sidebar | container size, intrinsic sizing |
| User-agent style visible | browser defaults/reset |
| Global style cannot reach component | Shadow DOM/style isolation |

---

# Appendix M: Master Learning Roadmap

A beginner does not need every advanced topic on day one.

## Stage 1 — Foundation

Learn and practice:

- valid HTML structure;
- classes and IDs;
- CSS declarations;
- selectors;
- DevTools element inspection;
- box model;
- normal flow;
- basic responsive design.

Goal:

> You can explain why a simple CSS rule does or does not apply.

---

## Stage 2 — Working developer

Add:

- cascade;
- specificity;
- inheritance;
- flexbox;
- grid;
- positioning;
- overflow;
- media queries;
- forms;
- accessibility basics.

Goal:

> You can solve most production UI bugs without random trial-and-error.

---

## Stage 3 — Advanced debugging

Add:

- containing blocks;
- intrinsic sizing;
- stacking contexts;
- custom properties;
- cascade layers;
- container queries;
- performance tooling;
- Shadow DOM;
- build-generated CSS;
- production asset debugging.

Goal:

> You can reduce complex layout bugs to a precise browser rule or build/runtime cause.

---

## Stage 4 — Expert habits

Develop these habits:

- create minimal reproductions;
- read computed styles;
- use overlays;
- test adverse content;
- verify browser support;
- test keyboard/accessibility;
- validate production artifacts;
- write regression tests;
- design CSS architecture that avoids priority wars.

Goal:

> Your debugging process becomes systematic, teachable, and fast.

**End of HTML & CSS Debugging Master Handbook**
