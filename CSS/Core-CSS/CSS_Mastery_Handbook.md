# CSS Mastery Handbook
## A Beginner-to-Advanced Single-File Guide for Learning Modern CSS

> **Goal:** This handbook is designed to be a single reference for learning, revising, and mastering CSS.  
> It starts from the absolute basics and progresses into responsive design, layout systems, modern CSS, architecture patterns, accessibility, performance, debugging, and real-world UI patterns.

---

# Table of Contents

1. [What CSS Is](#1-what-css-is)
2. [How CSS Works With HTML](#2-how-css-works-with-html)
3. [Ways to Add CSS](#3-ways-to-add-css)
4. [CSS Syntax](#4-css-syntax)
5. [Comments](#5-comments)
6. [Selectors](#6-selectors)
7. [Combinators](#7-combinators)
8. [Pseudo-classes](#8-pseudo-classes)
9. [Pseudo-elements](#9-pseudo-elements)
10. [The Cascade](#10-the-cascade)
11. [Specificity](#11-specificity)
12. [Inheritance](#12-inheritance)
13. [CSS Values and Units](#13-css-values-and-units)
14. [Colors](#14-colors)
15. [CSS Custom Properties](#15-css-custom-properties)
16. [The Box Model](#16-the-box-model)
17. [Width and Height](#17-width-and-height)
18. [Margin](#18-margin)
19. [Padding](#19-padding)
20. [Borders](#20-borders)
21. [Outline](#21-outline)
22. [Border Radius](#22-border-radius)
23. [Box Shadows](#23-box-shadows)
24. [Display](#24-display)
25. [Normal Document Flow](#25-normal-document-flow)
26. [Overflow](#26-overflow)
27. [Positioning](#27-positioning)
28. [Z-index and Stacking Context](#28-z-index-and-stacking-context)
29. [Float and Clear](#29-float-and-clear)
30. [Flexbox](#30-flexbox)
31. [CSS Grid](#31-css-grid)
32. [Subgrid](#32-subgrid)
33. [Responsive Web Design](#33-responsive-web-design)
34. [Media Queries](#34-media-queries)
35. [Container Queries](#35-container-queries)
36. [Responsive Units and Fluid Sizing](#36-responsive-units-and-fluid-sizing)
37. [Typography](#37-typography)
38. [Web Fonts](#38-web-fonts)
39. [Text Styling](#39-text-styling)
40. [Lists](#40-lists)
41. [Tables](#41-tables)
42. [Backgrounds](#42-backgrounds)
43. [Gradients](#43-gradients)
44. [Images and Replaced Elements](#44-images-and-replaced-elements)
45. [object-fit and object-position](#45-object-fit-and-object-position)
46. [Aspect Ratio](#46-aspect-ratio)
47. [Forms](#47-forms)
48. [Buttons](#48-buttons)
49. [Transforms](#49-transforms)
50. [Transitions](#50-transitions)
51. [Animations](#51-animations)
52. [Filters](#52-filters)
53. [Blend Modes](#53-blend-modes)
54. [Clipping and Masking](#54-clipping-and-masking)
55. [CSS Functions](#55-css-functions)
56. [calc(), min(), max(), clamp()](#56-calc-min-max-clamp)
57. [Logical Properties](#57-logical-properties)
58. [Writing Modes and Internationalization](#58-writing-modes-and-internationalization)
59. [CSS Nesting](#59-css-nesting)
60. [Cascade Layers](#60-cascade-layers)
61. [@scope](#61-scope)
62. [Scroll Behavior](#62-scroll-behavior)
63. [Scroll Snap](#63-scroll-snap)
64. [Sticky UI Patterns](#64-sticky-ui-patterns)
65. [Multi-column Layout](#65-multi-column-layout)
66. [Print CSS](#66-print-css)
67. [Dark Mode and Theming](#67-dark-mode-and-theming)
68. [Accessibility](#68-accessibility)
69. [Reduced Motion](#69-reduced-motion)
70. [CSS Architecture](#70-css-architecture)
71. [BEM](#71-bem)
72. [OOCSS](#72-oocss)
73. [SMACSS](#73-smacss)
74. [ITCSS](#74-itcss)
75. [Utility-First CSS](#75-utility-first-css)
76. [CSS Modules and Scoped Styles](#76-css-modules-and-scoped-styles)
77. [Design Tokens](#77-design-tokens)
78. [Reusable Component Patterns](#78-reusable-component-patterns)
79. [Common Layout Recipes](#79-common-layout-recipes)
80. [Navigation Patterns](#80-navigation-patterns)
81. [Card Patterns](#81-card-patterns)
82. [Modal Pattern](#82-modal-pattern)
83. [Tooltip Pattern](#83-tooltip-pattern)
84. [Form Layout Patterns](#84-form-layout-patterns)
85. [Dashboard Layout Pattern](#85-dashboard-layout-pattern)
86. [Holy Grail Layout](#86-holy-grail-layout)
87. [Responsive Sidebar Pattern](#87-responsive-sidebar-pattern)
88. [Truncation and Long Content](#88-truncation-and-long-content)
89. [CSS Reset and Normalize](#89-css-reset-and-normalize)
90. [Browser Compatibility](#90-browser-compatibility)
91. [Progressive Enhancement](#91-progressive-enhancement)
92. [CSS Performance](#92-css-performance)
93. [Debugging CSS](#93-debugging-css)
94. [Common CSS Mistakes](#94-common-css-mistakes)
95. [Naming and File Organization](#95-naming-and-file-organization)
96. [Real-World Mini Projects](#96-real-world-mini-projects)
97. [Interview Questions](#97-interview-questions)
98. [CSS Checklist](#98-css-checklist)
99. [Learning Roadmap](#99-learning-roadmap)
100. [Quick Reference Cheat Sheet](#100-quick-reference-cheat-sheet)

---

# 1. What CSS Is

CSS stands for **Cascading Style Sheets**.

HTML defines the structure of a page.

CSS controls how that structure looks and behaves visually.

Example HTML:

```html
<h1>Hello World</h1>
<p>This is my first page.</p>
```

Example CSS:

```css
h1 {
  color: navy;
  font-size: 40px;
}

p {
  color: #444;
}
```

CSS can control:

- colors
- fonts
- spacing
- borders
- backgrounds
- alignment
- page layout
- responsive behavior
- animations
- hover states
- print styles
- themes
- component appearance

## Real-world scenario

Suppose you build an invoice application.

HTML may contain:

```html
<section class="invoice">
  <h1>Invoice</h1>
  <p>Total: ₹12,500</p>
</section>
```

CSS can make it look like a professional invoice card:

```css
.invoice {
  max-width: 700px;
  margin: 2rem auto;
  padding: 2rem;
  border: 1px solid #ddd;
  border-radius: 12px;
  background: white;
  box-shadow: 0 10px 30px rgb(0 0 0 / 8%);
}
```

---

# 2. How CSS Works With HTML

A browser roughly performs these steps:

1. Parses HTML into the DOM.
2. Parses CSS into CSS rules.
3. Matches selectors with DOM elements.
4. Resolves the cascade and specificity.
5. Calculates layout.
6. Paints pixels.
7. Composites visual layers.

This explains why changing CSS can affect layout, painting, or animation performance.


## A more useful mental model

HTML and CSS are processed separately and then combined by the browser. HTML contributes the **DOM tree**; CSS contributes style rules. The browser matches selectors to DOM elements, resolves competing declarations through the cascade, computes each element's final values, performs layout, paints the result, and may place some painted parts on separate compositing layers.

This distinction helps when debugging:

```text
Wrong element/structure?      → inspect HTML/DOM
Rule does not match?          → inspect selector
Rule matches but loses?       → inspect cascade/specificity
Correct style but bad layout? → inspect box sizes/layout context
Animation feels slow?         → inspect rendering/performance
```

Changing a property does not always have the same cost. A color change usually affects painting, while changing dimensions can require layout. Do not optimize blindly; use browser DevTools when performance is actually a problem.

---

# 3. Ways to Add CSS

## 3.1 Inline CSS

```html
<p style="color: red;">Important message</p>
```

### Good for

- very small experiments
- dynamically generated values in limited cases

### Avoid for

- normal application styling
- reusable UI

---

## 3.2 Internal CSS

```html
<head>
  <style>
    body {
      font-family: Arial, sans-serif;
    }
  </style>
</head>
```

Useful for:

- standalone demo pages
- prototypes
- email templates in some workflows

---

## 3.3 External CSS

```html
<link rel="stylesheet" href="styles.css">
```

```css
/* styles.css */
body {
  margin: 0;
}
```

This is usually the preferred method for ordinary websites and applications.


## How to choose

For a normal multi-page site or application, prefer an external stylesheet or the stylesheet system provided by your framework/build tool. It keeps styling reusable and allows the browser to cache CSS independently of the HTML.

Inline styles have an important limitation: they are hard to reuse and have high cascade priority. They are sometimes reasonable for values that are truly data-driven, such as a runtime CSS custom property:

```html
<div class="progress" style="--progress: 72%">...</div>
```

```css
.progress {
  width: var(--progress);
}
```

Internal `<style>` blocks are useful for demos, prototypes, or page-specific critical styles, but large applications become easier to maintain when styles are organized outside individual HTML documents.

**Common mistake:** choosing inline CSS to "fix specificity." That usually hides the cascade problem instead of solving it.

---

# 4. CSS Syntax

Basic format:

```css
selector {
  property: value;
}
```

Example:

```css
.card {
  width: 320px;
  padding: 20px;
  background-color: white;
}
```

Terminology:

```css
.card             /* selector */
{
  width: 320px;   /* declaration */
}
```

Inside the declaration:

- `width` = property
- `320px` = value


## Declaration blocks, parsing, and invalid values

A rule can contain many declarations:

```css
.card {
  width: 20rem;
  padding: 1rem;
  color: #1f2937;
}
```

A semicolon separates declarations. The final semicolon is optional in many cases, but keeping it is safer when another declaration is added later.

Browsers are fault tolerant. If one declaration is invalid, the browser normally ignores that declaration rather than discarding the whole stylesheet:

```css
.card {
  color: definitely-not-a-color; /* ignored */
  padding: 1rem;                 /* still applied */
}
```

Use DevTools when a property appears crossed out or has a warning icon. That often means the syntax/value is invalid, the property does not apply in the current context, or another declaration won the cascade.

**Best practice:** format one declaration per line in maintained code. It makes diffs, debugging, and reviews easier.

---

# 5. Comments

```css
/* This is a CSS comment */
```

Use comments to explain **why**, not obvious syntax.

Bad:

```css
/* Makes text red */
.error {
  color: red;
}
```

Better:

```css
/* Uses the same danger color as server-side validation messages */
.error {
  color: var(--color-danger);
}
```


## What comments are good for

Comments are most valuable when they preserve context that the code cannot express by itself:

```css
/* Keep above the sticky table header used by the vendor grid. */
.invoice-toolbar {
  z-index: 30;
}
```

They are also useful for section boundaries in a small stylesheet, compatibility notes, and temporary migration guidance.

Avoid leaving secrets, credentials, internal URLs, or sensitive operational details in CSS comments. Production CSS is downloaded by the browser and can be read by users even when it is minified.

**Maintenance rule:** when code changes, update or delete the related comment. An outdated comment is often more dangerous than no comment because future developers may trust it.

---

# 6. Selectors

Selectors tell CSS which elements should receive a style.

## 6.1 Type selector

```css
p {
  color: #333;
}
```

Targets every `<p>`.

---

## 6.2 Class selector

```css
.button {
  padding: 0.75rem 1rem;
}
```

```html
<button class="button">Save</button>
```

Classes are the most common reusable styling mechanism.

---

## 6.3 ID selector

```css
#header {
  background: black;
}
```

IDs are highly specific. Prefer classes for reusable UI styles.

---

## 6.4 Universal selector

```css
* {
  box-sizing: border-box;
}
```

Targets all elements.

A common setup is:

```css
*,
*::before,
*::after {
  box-sizing: border-box;
}
```

---

## 6.5 Attribute selector

```css
input[type="email"] {
  border-color: steelblue;
}
```

Other examples:

```css
a[target="_blank"] {}
input[disabled] {}
[data-status="approved"] {}
```

Prefix match:

```css
a[href^="https"] {}
```

Suffix match:

```css
a[href$=".pdf"] {}
```

Contains:

```css
[class*="icon-"] {}
```

---

## 6.6 Grouping selector

```css
h1,
h2,
h3 {
  line-height: 1.2;
}
```

---

# 7. Combinators

Combinators describe relationships between elements.

## Descendant

```css
.card p {
  color: #555;
}
```

Targets any `<p>` inside `.card`.

---

## Child

```css
.menu > li {
  list-style: none;
}
```

Targets only direct children.

---

## Adjacent sibling

```css
h2 + p {
  margin-top: 0;
}
```

Targets the first `p` immediately after an `h2`.

---

## General sibling

```css
h2 ~ p {
  color: #555;
}
```

Targets later sibling paragraphs.


## Choosing the right relationship

Use the narrowest relationship that reflects the actual HTML structure.

```html
<ul class="menu">
  <li><a href="/">Home</a></li>
</ul>
```

```css
.menu > li { ... }  /* direct list items only */
.menu a { ... }     /* links anywhere inside the menu */
```

A descendant selector such as `.card p` is intentionally broad: it also matches paragraphs inside nested components. A child selector such as `.card > p` is more precise when only direct children should be styled.

Sibling combinators are useful for "element after element" patterns:

```css
.form-field + .form-field {
  margin-top: 1rem;
}
```

This adds spacing only when one field follows another.

**Common mistake:** encoding the entire DOM path in selectors. Deep selectors become fragile when markup changes. Prefer stable component classes when the relationship is not semantically important.

---

# 8. Pseudo-classes

Pseudo-classes represent a state or structural condition.

## Hover

```css
.button:hover {
  background: #222;
}
```

---

## Focus

```css
input:focus {
  outline: 3px solid dodgerblue;
}
```

Prefer `:focus-visible` for keyboard-focused UI:

```css
button:focus-visible {
  outline: 3px solid #4c9ffe;
  outline-offset: 3px;
}
```

---

## Active

```css
button:active {
  transform: translateY(1px);
}
```

---

## Checked

```css
input:checked + label {
  font-weight: bold;
}
```

---

## Disabled

```css
button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
```

---

## Structural pseudo-classes

```css
li:first-child {}
li:last-child {}
li:nth-child(2) {}
li:nth-child(odd) {}
li:nth-child(3n) {}
```

---

## :not()

```css
button:not(.primary) {
  background: transparent;
}
```

---

## :is()

```css
:is(h1, h2, h3) {
  line-height: 1.2;
}
```

Useful for reducing repetition.

---

## :where()

```css
:where(article, section) h2 {
  margin-block-start: 2rem;
}
```

`:where()` has zero specificity, making it excellent for low-priority defaults.

---

## :has()

```css
.card:has(.badge-new) {
  border-color: green;
}
```

A powerful parent-aware selector.

Example form:

```css
.form-group:has(input:invalid) {
  border-left: 4px solid crimson;
}
```

---

# 9. Pseudo-elements

Pseudo-elements style a virtual part of an element.

## ::before and ::after

```css
.required::after {
  content: " *";
  color: red;
}
```

---

## ::first-letter

```css
.article::first-letter {
  font-size: 3rem;
}
```

---

## ::selection

```css
::selection {
  background: gold;
  color: black;
}
```

---

## ::placeholder

```css
input::placeholder {
  color: #999;
}
```


## Pseudo-element vs real content

Pseudo-elements are generated presentation boxes; they are not a substitute for meaningful HTML.

```css
.external-link::after {
  content: " ↗";
}
```

This is fine as a decorative cue, but essential instructions, form errors, prices, or accessible labels should live in the document rather than only in `content`.

`::before` and `::after` normally require `content` to generate a box:

```css
.badge::before {
  content: "";
  inline-size: 0.5rem;
  block-size: 0.5rem;
  border-radius: 50%;
  background: currentColor;
}
```

Use pseudo-elements for decorative shapes, icons that are non-essential, overlays, and visual affordances.

**Common mistake:** absolutely positioning a pseudo-element without establishing the intended containing block. If it should be positioned relative to a component, that component often needs `position: relative`.

---

# 10. The Cascade

CSS is called **Cascading** Style Sheets because multiple rules can target the same element.

The browser determines the winner based on concepts such as:

- origin
- importance
- cascade layer
- specificity
- source order

Example:

```css
p {
  color: blue;
}

p {
  color: red;
}
```

When priority is otherwise equal, the later rule wins.

Result: red.


## How to reason about a conflict

Do not reduce the cascade to "the last rule wins." Source order is only one step. A practical debugging order is:

```text
1. Is the declaration relevant to this element/property?
2. Which origin and importance wins?
3. Which cascade layer wins?
4. Which selector has greater specificity?
5. If still tied, which declaration appears later?
```

For example, a later low-specificity selector does not automatically beat an earlier ID selector:

```css
#save { color: red; }
button { color: blue; }
```

The button remains red if both rules apply.

Cascade layers (`@layer`) can deliberately order groups of CSS without increasing selector specificity. This is useful when combining resets, third-party CSS, components, and utilities.

**Best practice:** use DevTools' Styles/Computed panels to see exactly which declaration won instead of guessing.

---

# 11. Specificity

Specificity decides which selector wins when competing rules have similar cascade priority.

A useful simplified mental model:

- inline styles are very strong
- IDs are stronger than classes
- classes, attributes, pseudo-classes are stronger than element selectors
- element selectors and pseudo-elements are lower

Example:

```css
p {
  color: blue;
}

.message {
  color: green;
}

#warning {
  color: red;
}
```

```html
<p id="warning" class="message">Alert</p>
```

Result: usually red because the ID selector is more specific.

## Avoid specificity wars

Bad:

```css
body main .content .panel .button.primary {
  background: blue;
}
```

Better:

```css
.button--primary {
  background: blue;
}
```


## Specificity is not a score to maximize

Specificity only participates after higher-priority cascade decisions such as origin, importance, and layer ordering. Within comparable rules, think of selector components in groups rather than as a decimal number.

```css
#app .button       /* includes an ID: difficult to override */
.button.is-active  /* two class-like components */
button             /* one type component */
```

Modern selectors also have special behavior. For example, `:where(...)` contributes zero specificity, which makes it useful for low-priority defaults:

```css
:where(.prose) a {
  color: var(--link-color);
}
```

**Common mistake:** fixing every conflict by adding more selectors or `!important`. This produces a specificity arms race. Prefer a clear architecture, controlled source order/layers, and selectors that are as specific as necessary—but no more.

---

# 12. Inheritance

Some CSS properties are inherited by children.

Often inherited:

- `color`
- `font-family`
- `font-size`
- `line-height`

Usually not inherited:

- `margin`
- `padding`
- `border`
- `width`
- `height`

Example:

```css
body {
  color: #222;
  font-family: system-ui, sans-serif;
}
```

Most text inside the body inherits these values.

Useful keywords:

```css
property: inherit;
property: initial;
property: unset;
property: revert;
```


## Inherited, initial, and computed values

Inheritance is evaluated per property. Text-oriented properties often inherit because that produces useful defaults; box-model and layout properties generally do not.

```css
.card {
  color: #334155;
}

.card strong {
  /* inherits #334155 unless another rule changes color */
}
```

CSS custom properties inherit by default too, which makes them especially useful for component theming:

```css
.panel {
  --accent: rebeccapurple;
}

.panel .button {
  background: var(--accent);
}
```

Useful reset keywords have different meanings:

- `inherit` — explicitly take the parent's computed value.
- `initial` — use the property's specification-defined initial value.
- `unset` — inherit if the property normally inherits; otherwise use its initial value.
- `revert` — roll back to the value from an earlier cascade origin/layer.

Use these intentionally; they are not interchangeable.

---

# 13. CSS Values and Units

## Absolute unit

```css
border-width: 1px;
```

`px` is useful when you need a consistent CSS pixel size.

---

## Relative units

### em

Relative to the current element's font size.

```css
button {
  padding: 0.75em 1.2em;
}
```

Useful when button spacing should scale with its text size.

---

### rem

Relative to the root font size.

```css
.card {
  padding: 1.5rem;
}
```

Excellent for consistent spacing systems.

---

### %

```css
.container {
  width: 90%;
}
```

Relative to a containing dimension depending on property.

---

### vw / vh

```css
.hero {
  min-height: 100vh;
}
```

Viewport relative units.

Modern viewport units include variants such as:

```css
100svh
100lvh
100dvh
```

These can be helpful on mobile browsers where browser chrome changes visible height.

---

### ch

Approximately based on the width of the `0` character.

```css
.article {
  max-width: 70ch;
}
```

Useful for readable text line length.

---

# 14. Colors

## Named colors

```css
color: tomato;
```

---

## Hex

```css
color: #1e293b;
```

With alpha:

```css
background: #00000080;
```

---

## rgb()

```css
color: rgb(30 41 59);
```

With transparency:

```css
background: rgb(0 0 0 / 0.5);
```

---

## hsl()

```css
color: hsl(220 60% 45%);
```

HSL is convenient for theme manipulation.

---

## Modern color thinking

Build semantic color variables:

```css
:root {
  --color-bg: #ffffff;
  --color-text: #1f2937;
  --color-primary: #2563eb;
  --color-danger: #dc2626;
  --color-success: #15803d;
}
```

Avoid scattering raw color values everywhere.


## Choosing a color format

No single color syntax is always best. Hex is compact for fixed RGB values; modern `rgb()` is readable and supports alpha; HSL can be intuitive for hue-based adjustments; newer color spaces such as `oklch()` can be valuable in design systems that need more perceptually consistent scales.

For application code, **semantic tokens** matter more than the literal syntax:

```css
:root {
  --surface: #ffffff;
  --text: #111827;
  --action: #2563eb;
}

.button {
  background: var(--action);
}
```

This lets the design change without searching for every copy of a raw value.

**Accessibility:** never assume that "red" automatically means an accessible error color. Foreground/background contrast and non-color cues still need to be checked.

**Common mistake:** mixing dozens of nearly identical raw colors instead of defining a deliberate palette.

---

# 15. CSS Custom Properties

Also called CSS variables.

```css
:root {
  --space-1: 0.25rem;
  --space-2: 0.5rem;
  --space-3: 1rem;
  --brand: #2563eb;
}
```

Usage:

```css
.button {
  padding: var(--space-2) var(--space-3);
  background: var(--brand);
}
```

Fallback:

```css
color: var(--text-color, #222);
```

Scoped variables:

```css
.alert {
  --alert-color: crimson;
  border-color: var(--alert-color);
}
```

## Real-world theme scenario

```css
:root {
  --bg: white;
  --text: #111;
}

[data-theme="dark"] {
  --bg: #111827;
  --text: #f9fafb;
}

body {
  background: var(--bg);
  color: var(--text);
}
```


## Runtime variables, not text substitution

A custom property participates in the normal cascade and is resolved by the browser at runtime. That makes it different from a preprocessor variable.

```css
.card {
  --card-accent: #2563eb;
  border-color: var(--card-accent);
}

.card--danger {
  --card-accent: #dc2626;
}
```

The modifier changes one token and every descendant using that token can update.

Custom properties are also useful with JavaScript:

```js
document.documentElement.style.setProperty("--sidebar-width", "320px");
```

Use a fallback when the variable may not exist:

```css
color: var(--text-color, #111827);
```

A fallback does **not** repair every invalid value; it is primarily used when the referenced custom property is missing or resolves invalidly in the relevant context.

**When not to use them:** do not turn every one-off literal into a variable. Create variables for values with real reuse, semantics, configuration, or runtime variability.

---

# 16. The Box Model

Every element can be imagined as:

```text
margin
  border
    padding
      content
```

Default box sizing can make width calculations confusing.

Recommended:

```css
*,
*::before,
*::after {
  box-sizing: border-box;
}
```

Then:

```css
.card {
  width: 300px;
  padding: 20px;
  border: 2px solid;
}
```

The declared 300px includes padding and border.


## Why `border-box` is easier

With the default `content-box`, a declared width applies only to the content box. Padding and borders are then added outside it:

```text
rendered width = declared content width + left/right padding + left/right border
```

With `box-sizing: border-box`, the declared width includes content, padding, and border. This makes components easier to size predictably.

Margin sits outside the border and is never included in `width`.

Use DevTools' box-model diagram when an element is unexpectedly larger or smaller than expected. It shows the computed content, padding, border, and margin values.

**Edge case:** `box-sizing` does not mean every element will have exactly the declared width. Min/max constraints, intrinsic sizing, flex/grid algorithms, and available space can still affect final layout.

---

# 17. Width and Height

```css
.box {
  width: 300px;
  height: 200px;
}
```

Often better:

```css
.box {
  width: 100%;
  max-width: 1200px;
}
```

Useful properties:

```css
min-width
max-width
min-height
max-height
```

## Scenario: centered page container

```css
.container {
  width: min(1120px, calc(100% - 2rem));
  margin-inline: auto;
}
```


## Prefer constraints over unnecessary fixed sizes

Fixed dimensions are appropriate when the design truly requires them, but content-driven interfaces are usually more robust with constraints:

```css
.dialog {
  width: min(32rem, calc(100% - 2rem));
  max-height: calc(100dvh - 2rem);
  overflow: auto;
}
```

This allows the dialog to fit narrow viewports while limiting its desktop size.

`min-width`/`min-height` establish a lower bound; `max-width`/`max-height` establish an upper bound. Percentage sizes depend on the relevant containing block and can be surprising when the parent's size is indefinite.

**Common mistake:** giving text cards a fixed `height` to make them equal. Longer translations or zoomed text can overflow. Prefer Grid/Flexbox equal-height behavior or `min-height` when appropriate.

---

# 18. Margin

Margin creates space outside an element.

```css
.card {
  margin: 20px;
}
```

Shorthand:

```css
margin: 10px;             /* all */
margin: 10px 20px;        /* vertical horizontal */
margin: 10px 20px 30px;   /* top horizontal bottom */
margin: 10px 20px 30px 40px;
```

Center a block:

```css
.container {
  max-width: 1000px;
  margin-inline: auto;
}
```


## Margin behavior worth knowing

Vertical margins of block elements can **collapse** in normal flow, so two adjacent margins do not always add together. Flex and grid item margins do not collapse in the same way.

Prefer `gap` when spacing items inside a flex or grid layout:

```css
.stack {
  display: grid;
  gap: 1rem;
}
```

This expresses "space between children" directly instead of placing margin on each child.

Logical properties improve writing-direction support:

```css
.card {
  margin-block: 1rem;
  margin-inline: auto;
}
```

**Common mistake:** using negative margins as a routine layout tool. They can be useful, but if they are compensating for misunderstood container spacing, fix the underlying layout first.

---

# 19. Padding

Padding creates space inside the border.

```css
.card {
  padding: 1.5rem;
}
```

Button example:

```css
.button {
  padding: 0.75rem 1rem;
}
```


## Padding changes the clickable/content area

Padding belongs inside an element's border, so it is especially useful for buttons, form controls, cards, and other surfaces:

```css
.button {
  padding-block: 0.75rem;
  padding-inline: 1rem;
}
```

Unlike margin, padding cannot be negative and does not collapse. The element's background is painted through the padding box by default.

When `box-sizing: border-box` is active, padding is included inside an explicitly declared width/height. Without it, padding increases the rendered size beyond the content-box dimension.

**Best practice:** use logical properties (`padding-inline`, `padding-block`) when left/right or top/bottom semantics are not important. They adapt more naturally to writing direction.

---

# 20. Borders

```css
.card {
  border: 1px solid #ddd;
}
```

Individual sides:

```css
border-top: 2px solid;
border-inline-start: 4px solid;
```


## Border anatomy

A visible border needs a width, style, and color:

```css
.panel {
  border: 1px solid #cbd5e1;
}
```

You can set logical sides for internationalized layouts:

```css
.notice {
  border-inline-start: 4px solid var(--accent);
}
```

Borders participate in the box model. With `border-box`, their thickness is included in declared dimensions; with `content-box`, it is added outside the content width/height.

Use `currentColor` when the border should follow the element's text color:

```css
.icon-button {
  color: #2563eb;
  border: 1px solid currentColor;
}
```

**Border vs outline:** borders affect box geometry; outlines generally do not and are often better for focus indication.

---

# 21. Outline

Outline does not affect box dimensions like borders do.

Common keyboard focus style:

```css
button:focus-visible {
  outline: 3px solid #2563eb;
  outline-offset: 2px;
}
```

Do not remove focus outlines without providing an accessible replacement.


## Why outlines are ideal for focus

An outline is drawn around the element without taking up normal layout space, so adding a keyboard focus ring does not push nearby content.

```css
:focus-visible {
  outline: 2px solid currentColor;
  outline-offset: 3px;
}
```

`:focus-visible` lets browsers show the focus treatment when it is useful for the user's interaction method, commonly keyboard navigation.

**Do not write** `outline: none` globally unless you provide an equally visible alternative focus indicator. Removing focus visibility can make an interface very difficult to use without a mouse.

Outlines can also be useful temporarily while debugging layout:

```css
* {
  outline: 1px solid rgb(255 0 0 / 0.15);
}
```

Remove diagnostic rules before production.

---

# 22. Border Radius

```css
.card {
  border-radius: 12px;
}
```

Circle:

```css
.avatar {
  width: 80px;
  aspect-ratio: 1;
  border-radius: 50%;
}
```

Pill:

```css
.badge {
  border-radius: 999px;
}
```


## How radius behaves

`border-radius` rounds the border box and also affects clipping of backgrounds. It can accept one to four corner values, and each corner may have horizontal/vertical radii.

```css
.card {
  border-radius: 1rem 1rem 0 0;
}
```

For a circular avatar, make the box square and use `50%`:

```css
.avatar {
  inline-size: 4rem;
  aspect-ratio: 1;
  object-fit: cover;
  border-radius: 50%;
}
```

A very large fixed radius such as `9999px` is a common way to create a pill when the element's height can vary.

**Common mistake:** applying `overflow: hidden` only to make child media follow a radius, then accidentally clipping focus rings or positioned content. Clip deliberately, not automatically.

---

# 23. Box Shadows

```css
.card {
  box-shadow: 0 8px 24px rgb(0 0 0 / 0.1);
}
```

Syntax:

```text
offset-x offset-y blur spread color
```

Inset shadow:

```css
input {
  box-shadow: inset 0 1px 2px rgb(0 0 0 / 0.08);
}
```


## Reading the shadow syntax

For:

```css
box-shadow: 0 8px 24px -8px rgb(15 23 42 / 0.25);
```

the values mean:

```text
x offset | y offset | blur radius | spread radius | color
```

Multiple shadows can be comma-separated. `inset` draws the shadow inside the border box.

Shadows are useful for elevation cues, but a large blurred shadow over a large animated region can increase painting/compositing cost. Use them based on the design, not as the only way to communicate hierarchy.

**Accessibility/design tip:** do not rely on a subtle shadow as the only boundary between controls and their background. Borders, spacing, and contrast may communicate structure more reliably.

---

# 24. Display

Common values:

```css
display: block;
display: inline;
display: inline-block;
display: flex;
display: grid;
display: none;
```

## block

Usually starts on a new line and can take full available width.

## inline

Flows inside text.

Width and height do not behave like normal blocks.

## inline-block

Flows inline while allowing box dimensions.

## none

Removes the element from layout.


## Display has an outer and inner role

A useful modern mental model is that `display` influences both how the element participates in its parent layout and how its children are laid out.

```css
.toolbar {
  display: flex;
}
```

The toolbar itself participates as a box in its parent; its children become flex items.

`display: none` removes the element and its descendants from visual layout and, in normal browser accessibility behavior, from the accessibility tree. Do not use it for content that must remain available to assistive technology.

`inline-block` is still useful for inline-flow elements that need dimensions, but Flexbox and Grid are usually better for multi-item layout.

**Debugging:** when width, margin, or alignment seems ignored, check the element's display type and the layout context created by its parent.

---

# 25. Normal Document Flow

Before learning flexbox or grid, understand normal flow.

Block elements naturally stack vertically.

Inline content naturally flows horizontally within text.

Good CSS often works **with** normal flow rather than forcing everything with absolute positioning.


## Why normal flow is your default layout engine

In normal flow, block-level boxes generally follow one another in the block direction, while inline content flows into line boxes. This provides a resilient baseline: content can grow, translations can become longer, and the page can scroll naturally.

Before adding `position: absolute`, ask whether normal flow plus margin/gap, Flexbox, or Grid can solve the layout. Absolute positioning removes an element from normal flow, so following content no longer reserves space for it.

A simple article often needs very little layout CSS:

```css
article {
  max-width: 70ch;
  margin-inline: auto;
  padding: 1rem;
}
```

Working with normal flow usually produces fewer overlap bugs and better behavior when content changes.

---

# 26. Overflow

```css
.box {
  overflow: hidden;
}
```

Values:

```css
visible
hidden
auto
scroll
clip
```

Scrollable table wrapper:

```css
.table-wrapper {
  overflow-x: auto;
}
```

Avoid applying `overflow: hidden` casually because it may clip focus indicators, shadows, popovers, or sticky children.


## Overflow creates important side effects

`overflow: auto` adds scrolling only when needed; `scroll` reserves a scrolling mechanism even when content fits in many environments; `hidden` clips overflow and establishes special scrolling/formatting behavior; `clip` clips without providing scrolling.

For wide data:

```css
.table-scroll {
  max-width: 100%;
  overflow-x: auto;
}
```

Keep the table itself semantically intact inside the wrapper.

Overflow can also affect `position: sticky`, focus rings, box shadows, and absolutely positioned descendants. If a sticky element "doesn't work," inspect the overflow values on its ancestors and identify the actual scrolling container.

**Best practice:** solve the cause of accidental overflow—such as an unbreakable URL or inflexible grid track—instead of hiding it globally on `body`.

---

# 27. Positioning

## static

Default.

```css
position: static;
```

---

## relative

Keeps normal layout position but becomes a positioning reference.

```css
.card {
  position: relative;
}
```

---

## absolute

Removed from normal document flow.

```css
.badge {
  position: absolute;
  top: 8px;
  right: 8px;
}
```

Usually paired with:

```css
.card {
  position: relative;
}
```

---

## fixed

Relative to the viewport in common cases.

```css
.help-button {
  position: fixed;
  right: 1rem;
  bottom: 1rem;
}
```

---

## sticky

Behaves normally until a scroll threshold is reached.

```css
.table-header {
  position: sticky;
  top: 0;
}
```


## Containing blocks and offsets

For an absolutely positioned child, the reference box is determined by CSS containing-block rules. A common pattern is to deliberately create that reference with a positioned ancestor:

```css
.card {
  position: relative;
}

.card__badge {
  position: absolute;
  inset-block-start: 0.5rem;
  inset-inline-end: 0.5rem;
}
```

Use `inset`, `inset-inline-*`, and `inset-block-*` when logical directions are useful.

`fixed` is excellent for viewport-level UI such as a floating help action, but transformed/containing ancestors can affect its reference behavior in advanced cases. `sticky` needs a scroll threshold such as `top: 0` (or logical equivalent) and enough scrollable space.

**Common mistake:** using absolute positioning for primary page layout. It does not reserve normal-flow space and becomes fragile when text size or content changes.

---

# 28. Z-index and Stacking Context

`z-index` controls ordering among relevant positioned or stacking elements.

```css
.modal {
  position: fixed;
  z-index: 1000;
}
```

However, `z-index: 999999` does not solve every problem.

Certain properties can create new stacking contexts, such as:

- positioned elements with z-index
- transforms
- opacity below 1
- filters
- isolation
- some containment features

Create a sensible layer scale:

```css
:root {
  --z-dropdown: 100;
  --z-sticky: 200;
  --z-overlay: 900;
  --z-modal: 1000;
  --z-toast: 1100;
}
```


## Why a larger number sometimes does nothing

`z-index` values are compared **inside stacking contexts**. A child cannot escape its ancestor's stacking context merely by using a huge number.

Conceptual example:

```text
Parent A (z-index: 1)
  └── child (z-index: 9999)

Parent B (z-index: 2)
```

The child under A can still appear beneath B because the ancestor contexts are ordered first.

Properties such as `transform`, `filter`, `opacity < 1`, `isolation: isolate`, and certain positioned elements can create stacking contexts. Use DevTools to inspect ancestors when layering behaves unexpectedly.

A named layer scale is easier to maintain than arbitrary numbers:

```css
--z-dropdown: 10;
--z-sticky: 20;
--z-modal: 100;
```

Keep the scale small and document exceptional cases.

---

# 29. Float and Clear

Floats were historically used for layouts.

Modern page layouts should normally use flexbox or grid.

Float remains useful for text wrapping:

```css
.article-image {
  float: left;
  margin: 0 1rem 1rem 0;
}
```

Clear:

```css
.footer {
  clear: both;
}
```


## What float is still for

`float` was designed to let inline content wrap around a floated box, which is still a legitimate editorial pattern:

```css
.article__figure {
  float: inline-start;
  max-width: 40%;
  margin-inline-end: 1rem;
  margin-block-end: 0.75rem;
}
```

For application navigation, card rows, sidebars, or page columns, Flexbox and Grid express layout intent more clearly.

Historically, developers used clearfix patterns because floated children could escape a parent's normal height calculation. If maintaining old CSS, you may still encounter:

```css
.clearfix::after {
  content: "";
  display: table;
  clear: both;
}
```

Do not introduce float-based layout into new code unless text wrapping is actually the behavior you need.

---

# 30. Flexbox

Flexbox is ideal for **one-dimensional layouts**: mainly row or column.

## Basic example

```css
.toolbar {
  display: flex;
  gap: 1rem;
}
```

---

## Main concepts

A flex container has:

- main axis
- cross axis

Default direction:

```css
flex-direction: row;
```

Other options:

```css
row-reverse
column
column-reverse
```

---

## justify-content

Controls distribution along the main axis.

```css
justify-content: flex-start;
justify-content: center;
justify-content: space-between;
justify-content: space-around;
justify-content: space-evenly;
```

---

## align-items

Controls alignment on the cross axis.

```css
align-items: stretch;
align-items: center;
align-items: flex-start;
align-items: flex-end;
```

---

## gap

```css
.actions {
  display: flex;
  gap: 0.75rem;
}
```

Prefer `gap` over manually adding margins between items.

---

## flex-wrap

```css
.tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}
```

---

## flex-grow, flex-shrink, flex-basis

```css
.content {
  flex: 1 1 500px;
}
```

Equivalent conceptual parts:

- grow: may consume extra space
- shrink: may shrink if needed
- basis: preferred starting size

---

## Scenario: toolbar

```html
<div class="toolbar">
  <h2>Invoices</h2>
  <div class="toolbar__actions">
    <button>Export</button>
    <button>Add Invoice</button>
  </div>
</div>
```

```css
.toolbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
}

.toolbar__actions {
  display: flex;
  gap: 0.5rem;
}
```

---

## Scenario: responsive cards

```css
.cards {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
}

.card {
  flex: 1 1 280px;
}
```

---

## Common flexbox issue: child refuses to shrink

Use:

```css
.flex-child {
  min-width: 0;
}
```

Especially useful when long text causes overflow.

---

# 31. CSS Grid

Grid is excellent for **two-dimensional layout**.

## Basic grid

```css
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
}
```

---

## Fraction unit

```css
grid-template-columns: 1fr 2fr;
```

Second column receives twice the flexible share.

---

## repeat()

```css
grid-template-columns: repeat(4, 1fr);
```

---

## minmax()

```css
grid-template-columns: repeat(3, minmax(0, 1fr));
```

---

## Responsive auto-fit pattern

```css
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(240px, 100%), 1fr));
  gap: 1rem;
}
```

This creates responsive card columns without a media query.

---

## Grid rows

```css
grid-template-rows: auto 1fr auto;
```

---

## Column and row placement

```css
.sidebar {
  grid-column: 1;
}

.main {
  grid-column: 2 / 4;
}
```

---

## Named areas

```css
.layout {
  display: grid;
  grid-template:
    "header header" auto
    "sidebar main" 1fr
    "footer footer" auto
    / 240px 1fr;
}

header {
  grid-area: header;
}

aside {
  grid-area: sidebar;
}

main {
  grid-area: main;
}

footer {
  grid-area: footer;
}
```

---

## place-items

```css
.center {
  display: grid;
  place-items: center;
}
```

Excellent for simple centering.

---

## Grid vs Flexbox

Use flexbox when:

- layout mainly follows one direction
- toolbar
- button group
- navigation row
- alignment of small groups

Use grid when:

- rows and columns matter together
- dashboard
- page shell
- card gallery
- form fields aligned by columns

They are complementary, not competitors.

---

# 32. Subgrid

Subgrid allows a nested grid to use the parent grid's tracks.

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

Useful when multiple cards need aligned internal rows such as:

- title
- description
- metadata
- button

Always confirm browser requirements for your target environment when using newer layout features.


## How subgrid differs from a new nested grid

A normal nested grid creates its own independent tracks. `subgrid` lets a descendant grid reuse tracks defined by an ancestor grid.

A common card pattern is:

```css
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(16rem, 1fr));
}

.card {
  display: grid;
  grid-row: span 3;
  grid-template-rows: subgrid;
}
```

Now corresponding internal rows can align across sibling cards when the surrounding grid structure is designed for it.

Use subgrid when alignment must cross component boundaries. Do not use it just because a component is nested; an ordinary grid is simpler when the child should size itself independently.

Test the actual layout and your supported browsers, especially if maintaining older enterprise browser targets.

---

# 33. Responsive Web Design

Responsive design means the interface adapts to available space and user environment.

Core principles:

1. start with flexible layouts
2. avoid unnecessary fixed dimensions
3. use responsive images
4. use media queries where the layout truly needs a breakpoint
5. use container queries for reusable components
6. design mobile-first when practical


## Responsive means more than screen width

A robust interface adapts to content, available space, user preferences, input methods, text zoom, and sometimes writing direction—not only a few device widths.

Start with intrinsic sizing:

```css
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(16rem, 100%), 1fr));
  gap: 1rem;
}
```

This may need fewer breakpoints because the layout responds to available space itself.

Choose breakpoints where **content needs them**, not by memorizing device model widths. Resize slowly and watch for the point where the design becomes cramped or visually unbalanced.

Also test long names, translated text, 200% zoom, keyboard focus, landscape phones, and narrow containers. Responsive quality is a behavior, not a list of three screenshots.

---

# 34. Media Queries

Example:

```css
.card-grid {
  grid-template-columns: 1fr;
}

@media (min-width: 768px) {
  .card-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1100px) {
  .card-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}
```

## Mobile-first approach

Base styles serve smaller screens.

Then larger layouts are layered on with `min-width`.

This usually reduces overrides.

---

## User preference media queries

Dark mode:

```css
@media (prefers-color-scheme: dark) {
  body {
    background: #111;
    color: #eee;
  }
}
```

Reduced motion:

```css
@media (prefers-reduced-motion: reduce) {
  * {
    scroll-behavior: auto;
  }
}
```


## Media query inputs

Media queries can respond to more than viewport width:

```css
@media (hover: hover) { ... }
@media (pointer: coarse) { ... }
@media (prefers-reduced-motion: reduce) { ... }
@media (prefers-contrast: more) { ... }
```

Use capability/preference queries when the design decision is about that capability rather than width. For example, do not assume every wide device has hover.

Keep related responsive rules close enough to their component that future developers can understand the whole behavior.

**Common mistake:** creating many tiny breakpoints to force a pixel-perfect screenshot. Prefer flexible layout primitives and add a breakpoint only when the content/layout actually needs a structural change.

---

# 35. Container Queries

Media queries inspect the viewport.

Container queries inspect the size of a component's container.

```css
.card-wrapper {
  container-type: inline-size;
}
```

```css
@container (min-width: 500px) {
  .profile-card {
    display: grid;
    grid-template-columns: 120px 1fr;
  }
}
```

## Why useful

The same component may be:

- full-width on one page
- inside a narrow sidebar on another
- inside a dashboard tile elsewhere

Container queries let the component adapt to its own available space.


## Container setup and units

A size query needs an appropriate query container:

```css
.widget-shell {
  container-type: inline-size;
}
```

Then descendants can react to that container:

```css
@container (width >= 30rem) {
  .widget {
    grid-template-columns: auto 1fr;
  }
}
```

Container query units such as `cqi` can size values relative to a query container in supporting browsers:

```css
.widget__title {
  font-size: clamp(1rem, 4cqi, 1.5rem);
}
```

Use media queries for page/environment-level decisions and container queries for reusable components whose layout depends on where they are placed.

**Common mistake:** trying to query an element's own size and style that same element in a way that creates circular sizing. Usually query a parent container and style its descendants.

---

# 36. Responsive Units and Fluid Sizing

Example fluid heading:

```css
h1 {
  font-size: clamp(2rem, 5vw, 4rem);
}
```

Meaning:

- minimum 2rem
- fluid preferred value 5vw
- maximum 4rem

Responsive spacing:

```css
.section {
  padding-block: clamp(2rem, 6vw, 6rem);
}
```


## Choosing units deliberately

Useful unit categories include:

- `rem` — relative to the root font size; good for scalable type/spacing.
- `em` — relative to the element's font-size (or parent font-size for the `font-size` property); useful for component-relative sizing.
- `%` — relative to a property-specific reference size.
- `vw`/`vh` — viewport-relative; useful but can become too small/large without constraints.
- `dvh`/`svh`/`lvh` — viewport variants that help with mobile browser UI behavior.
- `ch` — roughly based on the width of the `0` glyph; useful for readable text measure.

Fluid values are strongest when bounded:

```css
.page-title {
  font-size: clamp(2rem, 1.5rem + 2vw, 4rem);
}
```

This gives responsive behavior without unlimited growth.

---

# 37. Typography

Typography affects readability, hierarchy, and usability.

A strong base:

```css
body {
  font-family:
    Inter,
    system-ui,
    -apple-system,
    BlinkMacSystemFont,
    "Segoe UI",
    sans-serif;
  line-height: 1.5;
}
```

Use meaningful hierarchy:

```css
h1 {
  font-size: clamp(2rem, 4vw, 3.5rem);
  line-height: 1.1;
}

h2 {
  font-size: 2rem;
  line-height: 1.2;
}

p {
  max-width: 70ch;
}
```


## Build a readable type system

Typography is not just `font-size`. Line length, line height, weight, spacing, font fallback, and hierarchy work together.

A practical body baseline:

```css
body {
  font-family: system-ui, sans-serif;
  font-size: 1rem;
  line-height: 1.5;
}

.prose {
  max-inline-size: 70ch;
}
```

Use relative units so browser/user text settings can participate. Avoid shrinking important text just to make a layout fit; fix the layout instead.

Headings should communicate document hierarchy in HTML, while CSS controls their visual size. Do not choose `<h3>` merely because it "looks smaller."

**Common mistake:** using light font weights or low-contrast gray text everywhere. A fashionable appearance is not useful if reading becomes difficult.

---

# 38. Web Fonts

Example:

```css
@font-face {
  font-family: "MyFont";
  src: url("/fonts/myfont.woff2") format("woff2");
  font-display: swap;
}
```

Then:

```css
body {
  font-family: "MyFont", sans-serif;
}
```

Best practices:

- prefer WOFF2 where appropriate
- limit unnecessary font weights
- provide fallback fonts
- use `font-display`
- consider loading performance


## Loading strategy

Each font file adds network and rendering cost, so ship only the families, styles, scripts, and weights the product actually needs. A variable font can sometimes replace multiple static files, but measure its real size.

A stronger `@font-face` definition may include descriptors that match the file:

```css
@font-face {
  font-family: "App Sans";
  src: url("/fonts/app-sans.woff2") format("woff2");
  font-weight: 400 700;
  font-style: normal;
  font-display: swap;
}
```

`font-display: swap` allows fallback text to render while the web font loads. Choose fallbacks with reasonably similar metrics to reduce layout shift.

**Do not** embed fonts you are not licensed to redistribute. Performance and licensing both matter in production.

---

# 39. Text Styling

Important properties:

```css
font-size
font-weight
font-style
line-height
letter-spacing
text-align
text-decoration
text-transform
text-indent
text-shadow
white-space
word-break
overflow-wrap
```

Example:

```css
.price {
  font-size: 1.5rem;
  font-weight: 700;
  letter-spacing: -0.02em;
}
```

Long text handling:

```css
.description {
  overflow-wrap: anywhere;
}
```


## Separate content semantics from visual treatment

CSS can transform appearance without changing the underlying text. For example, `text-transform: uppercase` displays uppercase letters but does not replace the original DOM string.

Use `line-height` generously enough for readable multi-line text and test longer content:

```css
.description {
  line-height: 1.6;
  overflow-wrap: anywhere;
}
```

`white-space` is powerful but easy to misuse. `white-space: nowrap` can force controls or labels to overflow narrow screens. Use it only where a single line is truly required.

For truncation, make sure the complete value remains obtainable when it matters—for example through expansion, a details view, or another accessible presentation. Visual neatness should not hide critical data.

---

# 40. Lists

Remove default list styling:

```css
.clean-list {
  list-style: none;
  margin: 0;
  padding: 0;
}
```

Custom marker:

```css
.features li::marker {
  color: green;
}
```

Do not remove semantic `<ul>` / `<ol>` structure just for visual design.


## Keep list semantics when the content is a list

Navigation menus, feature lists, steps, and grouped options are often semantically lists even when bullets are not desired.

```css
.nav-list {
  list-style: none;
  margin: 0;
  padding: 0;
}
```

Removing markers changes only presentation; the HTML can remain `<ul>` or `<ol>`.

`::marker` can style markers without replacing list semantics:

```css
.steps li::marker {
  color: var(--accent);
  font-weight: 700;
}
```

Use an ordered list when sequence/order carries meaning. Use an unordered list when it does not.

**Common mistake:** using `div` elements purely because the default bullets are unwanted. Reset the presentation with CSS instead of discarding meaningful structure.

---

# 41. Tables

Basic table styling:

```css
table {
  width: 100%;
  border-collapse: collapse;
}

th,
td {
  padding: 0.75rem;
  border-bottom: 1px solid #ddd;
  text-align: left;
}
```

Responsive wrapper:

```css
.table-scroll {
  overflow-x: auto;
}
```

Sticky header:

```css
thead th {
  position: sticky;
  top: 0;
  background: white;
}
```


## Table CSS should preserve table semantics

Use tables for genuinely tabular relationships, not general page layout. CSS can make a semantic table easier to read without changing its structure.

```css
.data-table {
  width: 100%;
  border-collapse: collapse;
}

.data-table th {
  font-weight: 600;
}

.data-table :is(th, td) {
  padding: 0.75rem 1rem;
}
```

For narrow screens, horizontal scrolling is often safer than converting every row into visually unrelated blocks:

```css
.table-scroll {
  overflow-x: auto;
  overscroll-behavior-inline: contain;
}
```

If you make headers sticky, give them an opaque background and appropriate stacking so body cells do not paint through them.

**Accessibility:** CSS cannot replace `<caption>`, proper `<th>`, and `scope`/header relationships where needed.

---

# 42. Backgrounds

```css
.hero {
  background-color: #111827;
  background-image: url("hero.jpg");
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
}
```

Shorthand:

```css
background: #111827 url("hero.jpg") center / cover no-repeat;
```


## Background layers do not affect document semantics

Background images are decorative by default. They do not provide accessible alternative text, so do not use a CSS background as the only representation of meaningful content.

Multiple backgrounds are layered from first to last:

```css
.hero {
  background:
    linear-gradient(rgb(0 0 0 / 0.45), rgb(0 0 0 / 0.45)),
    url("/images/hero.jpg") center / cover no-repeat;
}
```

The gradient is painted above the image.

Useful related properties include `background-origin`, `background-clip`, `background-attachment`, and `background-blend-mode`.

**Common mistake:** using `background-size: cover` and assuming the whole image remains visible. `cover` may crop; use real `<img>` content or `contain` when the complete image matters.

---

# 43. Gradients

Linear:

```css
background: linear-gradient(135deg, #2563eb, #7c3aed);
```

Radial:

```css
background: radial-gradient(circle, white, #ddd);
```

Gradient overlay:

```css
.hero {
  background:
    linear-gradient(rgb(0 0 0 / 0.5), rgb(0 0 0 / 0.5)),
    url("hero.jpg") center / cover;
}
```


## Gradients are generated images

A CSS gradient produces an image that can be used anywhere an image value is accepted. It can include multiple color stops and transparency.

```css
.badge {
  background: linear-gradient(
    90deg,
    #2563eb 0%,
    #7c3aed 60%,
    #db2777 100%
  );
}
```

Gradients are useful for decorative surfaces, overlays, masks, and subtle depth. They should not make text contrast unpredictable.

For a text overlay on photography, test the worst part of the image—not just the mockup. A gradient overlay can improve readability, but it is still your responsibility to ensure sufficient contrast.

**Maintainability:** if the same gradient is reused, consider a semantic custom property rather than duplicating a long function everywhere.

---

# 44. Images and Replaced Elements

Responsive image rule:

```css
img,
video {
  max-width: 100%;
  height: auto;
}
```

Avoid forcing image dimensions without considering aspect ratio.


## What "replaced element" means

Some elements, such as `<img>`, `<video>`, and many form controls, have intrinsic content/dimensions that CSS lays out as an external object rather than ordinary child boxes. This is why properties such as `object-fit` apply to images/video but not to a normal `<div>`.

A resilient media baseline is:

```css
img,
svg,
video {
  max-inline-size: 100%;
}

img,
video {
  block-size: auto;
}
```

For layout stability, supply intrinsic `width` and `height` attributes in HTML when you know them. CSS can still resize the image responsively while the browser reserves the correct aspect-ratio space before it loads.

Do not use CSS background images for content that needs alt text or document meaning.

---

# 45. object-fit and object-position

Card thumbnail:

```css
.thumbnail {
  width: 100%;
  height: 220px;
  object-fit: cover;
}
```

Show whole image:

```css
.logo {
  object-fit: contain;
}
```

Control crop position:

```css
.profile-photo {
  object-fit: cover;
  object-position: center top;
}
```


## When these properties matter

`object-fit` controls how the intrinsic media is fitted **inside a box whose dimensions have been established**.

```css
.product-photo {
  width: 100%;
  aspect-ratio: 4 / 3;
  object-fit: cover;
}
```

- `cover` fills the box and may crop.
- `contain` shows the entire object and may leave empty space.
- `fill` stretches to the box and may distort.
- `none` keeps intrinsic sizing behavior within the object box.
- `scale-down` chooses a smaller result from `none`/`contain`.

`object-position` changes which part stays visible when cropping occurs:

```css
.product-photo {
  object-position: 50% 20%;
}
```

Use it for focal-point adjustment, not as a substitute for serving appropriately composed images.

---

# 46. Aspect Ratio

```css
.video {
  aspect-ratio: 16 / 9;
}
```

Square:

```css
.avatar {
  aspect-ratio: 1;
}
```

Useful for preventing layout shifts and maintaining consistent media dimensions.


## Aspect ratio participates in sizing

`aspect-ratio` supplies a preferred width-to-height relationship when at least one dimension can be derived automatically.

```css
.video-frame {
  width: 100%;
  aspect-ratio: 16 / 9;
}
```

A declared width plus ratio lets the browser calculate height. If both width and height are definite, those dimensions normally control the box and the ratio may not change the result.

For replaced elements such as images, intrinsic dimensions may already provide an aspect ratio. An explicit CSS ratio is useful for consistent card media or placeholders.

**Layout stability:** HTML `width` and `height` attributes are still valuable for images because browsers can reserve space before CSS and the image resource finish loading.

---

# 47. Forms

Good base styling:

```css
label {
  display: block;
  margin-bottom: 0.375rem;
  font-weight: 600;
}

input,
select,
textarea,
button {
  font: inherit;
}

input,
select,
textarea {
  width: 100%;
  padding: 0.75rem;
  border: 1px solid #cbd5e1;
  border-radius: 8px;
}
```

Focus:

```css
input:focus-visible,
select:focus-visible,
textarea:focus-visible {
  outline: 3px solid rgb(37 99 235 / 0.25);
  border-color: #2563eb;
}
```

Invalid:

```css
input:invalid:not(:placeholder-shown) {
  border-color: #dc2626;
}
```


## Styling cannot replace form semantics

Keep real labels, input types, names, descriptions, and error relationships in HTML. CSS should make those states visible.

A good field pattern distinguishes focus, error, disabled, and readonly states:

```css
.field-control:focus-visible {
  outline: 3px solid rgb(37 99 235 / 0.25);
  outline-offset: 1px;
}

.field-control[aria-invalid="true"] {
  border-color: #dc2626;
}

.field-control:disabled {
  cursor: not-allowed;
  opacity: 0.6;
}
```

Be careful with `:invalid`: native form controls can match it before the user has interacted, which may make a new form look full of errors. Modern selectors such as `:user-invalid` can improve timing where supported, or your application can add an explicit validation state class/attribute.

Never use placeholder text as the only label.

---

# 48. Buttons

Reusable base:

```css
.button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  min-height: 44px;
  padding: 0.75rem 1rem;
  border: 1px solid transparent;
  border-radius: 8px;
  font: inherit;
  font-weight: 600;
  cursor: pointer;
}
```

Primary:

```css
.button--primary {
  background: #2563eb;
  color: white;
}
```

Danger:

```css
.button--danger {
  background: #dc2626;
  color: white;
}
```

Disabled:

```css
.button:disabled {
  cursor: not-allowed;
  opacity: 0.55;
}
```


## Style the correct element

Use `<button>` for actions and `<a href>` for navigation. CSS can make them look similar, but their semantics and keyboard behavior are different.

Build states deliberately:

```css
.button:hover { ... }

.button:focus-visible {
  outline: 3px solid rgb(37 99 235 / 0.35);
  outline-offset: 2px;
}

.button:active {
  transform: translateY(1px);
}

.button:disabled {
  opacity: 0.55;
}
```

A disabled native `<button>` is not submitted/activated like an enabled control. A visual class named `.disabled` does not create the same behavior by itself.

**Common mistake:** removing the focus ring because the mouse design looks cleaner. Keep a strong keyboard-visible focus state and test the control at zoomed text sizes.

---

# 49. Transforms

```css
transform: translateX(10px);
transform: translateY(-5px);
transform: scale(1.05);
transform: rotate(5deg);
```

Combined:

```css
transform: translateY(-2px) scale(1.02);
```

Transforms are useful for visual movement without changing normal document flow.


## Transforms change the visual coordinate system

Transforms affect how a box is rendered without moving surrounding normal-flow content.

```css
.card:hover {
  transform: translateY(-0.25rem);
}
```

The original layout space remains reserved, so nearby items do not reflow around the transformed position.

Transforms are applied as a composed transform operation; order can matter because operations use coordinate systems:

```css
transform: translateX(2rem) rotate(10deg);
```

may not produce the same visual result as the reversed sequence.

Transforms can also create stacking/containing-block effects, which matters for `z-index` and positioned descendants.

Use them for visual movement, scaling, rotation, and performant UI animation—but avoid scaling text so aggressively that it becomes blurry or difficult to read.

---

# 50. Transitions

```css
.button {
  background: #2563eb;
  transform: translateY(0);
  transition:
    background-color 150ms ease,
    transform 150ms ease;
}

.button:hover {
  background: #1d4ed8;
  transform: translateY(-1px);
}
```

Avoid:

```css
transition: all 0.3s;
```

Prefer listing only the properties you intend to animate.


## What can transition

A transition interpolates a property from one computed value to another when the value changes.

```css
.button {
  transition:
    background-color 150ms ease,
    color 150ms ease,
    transform 150ms ease;
}
```

Not every property animates in the same way, and some values are discrete rather than smoothly interpolated.

Prefer transitions for small state changes such as hover, expansion cues, and color changes. For repeated/keyframed motion, an animation may be clearer.

Respect motion preferences:

```css
@media (prefers-reduced-motion: reduce) {
  .button {
    transition-duration: 0.01ms;
  }
}
```

**Common mistake:** `transition: all`. It can animate a property you did not intend, making later CSS changes surprising. Name the properties deliberately.

---

# 51. Animations

```css
@keyframes pulse {
  0%,
  100% {
    opacity: 1;
  }

  50% {
    opacity: 0.5;
  }
}

.loading {
  animation: pulse 1.5s ease-in-out infinite;
}
```

Animation properties:

```css
animation-name
animation-duration
animation-timing-function
animation-delay
animation-iteration-count
animation-direction
animation-fill-mode
animation-play-state
```


## Animation shorthand and lifecycle

A complete animation can be written with longhands or shorthand:

```css
.loading {
  animation: pulse 1.5s ease-in-out 0s infinite alternate;
}
```

Animation does not automatically communicate application state to assistive technology. A spinning icon may visually indicate loading, but the UI may still need suitable text/status semantics in HTML.

Use animation for purposeful feedback or storytelling. Avoid continuous decorative motion on large areas when it distracts users or wastes rendering resources.

```css
@media (prefers-reduced-motion: reduce) {
  .loading {
    animation: none;
  }
}
```

When an animation should finish in a specific final visual state, understand `animation-fill-mode`; when JavaScript needs to react to completion, use the relevant animation events rather than a guessed timeout.

---

# 52. Filters

```css
filter: blur(4px);
filter: grayscale(1);
filter: brightness(1.1);
filter: contrast(1.2);
```

Backdrop effect:

```css
.glass {
  background: rgb(255 255 255 / 0.5);
  backdrop-filter: blur(12px);
}
```

Use effects carefully for readability and performance.


## Filter vs backdrop-filter

`filter` changes the rendering of the element itself and its contents:

```css
.preview--disabled {
  filter: grayscale(1) opacity(0.7);
}
```

`backdrop-filter` changes what is visible **behind** a partially transparent element:

```css
.frosted {
  background: rgb(255 255 255 / 0.65);
  backdrop-filter: blur(12px);
}
```

Backdrop effects require content behind the element to be visible through it, so an opaque background hides the effect.

These effects can create new stacking/compositing behavior and may be expensive when used over large moving regions.

**Accessibility:** blur, contrast, or opacity effects can reduce readability. Do not apply them to important text unless you have tested the result.

---

# 53. Blend Modes

Example:

```css
.overlay {
  mix-blend-mode: multiply;
}
```

Background blend:

```css
.hero {
  background-image:
    linear-gradient(red, blue),
    url("photo.jpg");
  background-blend-mode: multiply;
}
```

These are useful for artistic visual treatments but can complicate contrast and compositing.


## How blending differs from opacity

A blend mode changes how colors are mathematically combined with content/background beneath them. It is not simply transparency.

`mix-blend-mode` blends an element with what is behind it; `background-blend-mode` blends an element's own multiple background layers.

Because the result depends on surrounding colors, contrast can change unexpectedly as content moves or themes change. This makes blend modes best suited to controlled decorative artwork rather than essential text or controls.

If a blended component should not interact with unrelated content outside itself, `isolation: isolate` on an appropriate parent can create a separate stacking/blending context:

```css
.artwork {
  isolation: isolate;
}
```

Always test light/dark themes and real imagery, not only a single mockup.

---

# 54. Clipping and Masking

Simple clipping:

```css
.avatar {
  clip-path: circle(50%);
}
```

Polygon:

```css
.banner {
  clip-path: polygon(0 0, 100% 0, 90% 100%, 0 100%);
}
```

Masking can create more complex transparency-based shapes.

Because feature requirements can vary by browser, verify compatibility before using advanced masking in production.


## Clip vs mask

`clip-path` defines the visible geometric region of an element. Content outside that region is clipped.

A mask controls visibility using an image/gradient's alpha or luminance information, which allows softer transparency effects than a hard clip.

```css
.fade-edge {
  mask-image: linear-gradient(to right, transparent, black 15%, black 85%, transparent);
}
```

These are visual effects; they do not change document semantics or remove hidden source content from the DOM.

**Interaction caution:** complex clipping can create a visible shape that differs from what users expect as the hit target. Test pointer interaction and keyboard focus indication.

Provide a simple fallback when the shape is decorative and advanced masking is not available in a target browser.

---

# 55. CSS Functions

Common CSS functions include:

```css
var()
calc()
min()
max()
clamp()
rgb()
hsl()
linear-gradient()
radial-gradient()
url()
attr()
counter()
```


## Functions compute values

A CSS function accepts arguments and produces a value used by a property. Different functions belong to different value types.

```css
.card {
  width: min(30rem, 100%);
  padding: calc(1rem + 1vw);
  color: rgb(15 23 42 / 0.9);
  background-image: linear-gradient(white, #f8fafc);
}
```

Functions can be nested:

```css
width: min(100%, calc(40rem + 2vw));
```

Do not assume every function is valid for every property. `url()` returns an image/resource reference in contexts that accept one; `var()` substitutes a custom-property value; math functions work where compatible numeric types can be resolved.

When a function expression is invalid, the declaration can become invalid at computed-value time. Inspect the Computed panel when a variable/function chain produces surprising output.

---

# 56. calc(), min(), max(), clamp()

## calc()

```css
.main {
  min-height: calc(100vh - 64px);
}
```

---

## min()

```css
.container {
  width: min(1120px, 100% - 2rem);
}
```

---

## max()

```css
.sidebar {
  width: max(240px, 20vw);
}
```

---

## clamp()

```css
.title {
  font-size: clamp(2rem, 5vw, 4rem);
}
```

Excellent for fluid design.


## Think of them as constraints

These math functions let layout express relationships instead of hard-coded breakpoint jumps.

```css
.container {
  width: min(70rem, 100% - 2rem);
}
```

means "use the smaller of 70rem and the available width minus gutters."

`clamp(min, preferred, max)` is especially useful for fluid design:

```css
.page-title {
  font-size: clamp(2rem, 1rem + 3vw, 4rem);
}
```

The middle value can grow, but never below the first value or above the third.

`calc()` can combine compatible units:

```css
min-height: calc(100dvh - var(--header-height));
```

The browser performs the calculation at runtime, so viewport/custom-property changes can update the result without recompiling CSS.

---

# 57. Logical Properties

Instead of physical directions:

```css
margin-left
margin-right
padding-top
```

Use logical directions:

```css
margin-inline-start
margin-inline-end
padding-block
padding-inline
```

Example:

```css
.card {
  padding-block: 1rem;
  padding-inline: 1.5rem;
}
```

Benefits:

- easier RTL support
- writing-mode support
- more semantic spacing


## Map styles to flow, not physical directions

Physical properties say "left/right/top/bottom." Logical properties say "inline start/end" and "block start/end," which adapt to writing mode and text direction.

```css
.callout {
  padding-inline: 1rem;
  padding-block: 0.75rem;
  border-inline-start: 4px solid var(--accent);
}
```

In a typical English horizontal writing mode, inline start is left. In an RTL language it becomes right automatically.

Logical sizing also exists:

```css
max-inline-size: 70ch;
min-block-size: 3rem;
```

Use physical directions when the physical side itself matters (for example an effect tied to the actual top of the viewport). Use logical properties for content-flow spacing and alignment that should internationalize naturally.

---

# 58. Writing Modes and Internationalization

```css
.vertical-label {
  writing-mode: vertical-rl;
}
```

When building multilingual applications, prefer logical properties so the layout can adapt more naturally to right-to-left languages.


## Direction and writing mode are different concepts

`direction: rtl` changes inline text direction for languages such as Arabic or Hebrew. `writing-mode` changes how lines of text themselves are laid out, including vertical writing systems.

Do not force `direction` merely to move UI elements to the other side; use layout/logical properties for visual positioning.

A component designed with logical properties adapts more easily:

```css
.message {
  margin-inline-start: 1rem;
  text-align: start;
}
```

Also test:

- longer translated strings,
- different fonts/scripts,
- bidirectional text such as an Arabic sentence containing an invoice number,
- icon placement,
- truncation behavior.

Internationalization problems are often content-and-layout problems together. CSS should support the document's real language/direction rather than simulating them.

---

# 59. CSS Nesting

Modern CSS can express nested relationships in supported environments.

Example:

```css
.card {
  padding: 1rem;

  & .title {
    font-weight: 700;
  }

  &:hover {
    box-shadow: 0 8px 24px rgb(0 0 0 / 0.1);
  }
}
```

Keep nesting shallow.

Bad mental model:

```text
page -> section -> card -> body -> text -> span -> icon
```

Deep nesting increases coupling and specificity.


## What nesting expands to

Nesting keeps related selectors together, but the browser still applies the resulting selector relationships.

```css
.card {
  color: #334155;

  & > .title {
    color: #0f172a;
  }
}
```

Conceptually targets:

```css
.card > .title { ... }
```

Nesting is most useful for states, variants, and closely related descendants. It is not a reason to mirror every level of the DOM tree.

```css
.button {
  &:hover { ... }
  &[aria-pressed="true"] { ... }
}
```

**Best practice:** keep selectors shallow and inspect their effective specificity. If a nested block is becoming difficult to understand, move the child into its own component rule.

When supporting older browsers/build pipelines, confirm whether native nesting is accepted directly or must be transformed.

---

# 60. Cascade Layers

Cascade layers let you explicitly control groups of styles.

```css
@layer reset, base, components, utilities;
```

```css
@layer reset {
  * {
    box-sizing: border-box;
  }
}

@layer components {
  .button {
    padding: 0.75rem 1rem;
  }
}

@layer utilities {
  .hidden {
    display: none;
  }
}
```

Useful in large applications and design systems because it can reduce specificity conflicts.


## Layer order beats selector specificity between layers

Once layer order is established, a declaration in a later-priority layer can beat a more specific selector in an earlier layer without a specificity contest.

```css
@layer reset, base, components, utilities;
```

This order is part of your CSS architecture. For example, low-priority reset rules can stay low even if their selectors are somewhat specific.

Unlayered normal author styles have different cascade placement than layered styles, so introduce layers deliberately when integrating existing CSS.

A practical architecture might be:

```text
reset → base → components → utilities → project overrides
```

Use layers to model responsibility, not to create dozens of microscopic priority groups.

**Debugging:** DevTools in modern browsers can show cascade layers, which is often the fastest way to understand why a rule lost.

---

# 61. @scope

Scoping can limit rules to a specific region.

Conceptual example:

```css
@scope (.invoice-panel) {
  h2 {
    color: #1e3a8a;
  }
}
```

This can help prevent styles leaking into unrelated areas.

When relying on newer CSS features, verify support requirements for your project's browser matrix.


## Scope controls where selectors are allowed to match

`@scope` lets you define a scoping root and, optionally, a lower boundary. This can make component or content-region CSS less dependent on globally unique selector names.

```css
@scope (.article) {
  h2 {
    margin-block-start: 2em;
  }
}
```

The rule targets `h2` elements inside `.article` without changing the HTML class of every heading.

Scoping and shadow DOM are not the same. `@scope` is still ordinary CSS operating in the document's cascade; it does not create the strong encapsulation boundary of a shadow root.

Use it when a region needs locally targeted styles. For widely distributed production code, verify browser support against your supported-browser policy before making it a required baseline.

---

# 62. Scroll Behavior

Smooth scroll:

```css
html {
  scroll-behavior: smooth;
}
```

Respect reduced-motion preferences:

```css
@media (prefers-reduced-motion: reduce) {
  html {
    scroll-behavior: auto;
  }
}
```


## Smooth scrolling is presentation, not navigation logic

`scroll-behavior: smooth` affects programmatic/anchor scrolling performed by the scroll container, but it does not make every user scroll gesture animate.

Use it as an enhancement:

```css
html {
  scroll-behavior: smooth;
  scroll-padding-top: var(--sticky-header-height);
}
```

`scroll-padding-top` can prevent an anchored heading from ending up underneath a sticky header.

Motion preferences matter. A user asking for reduced motion should not be forced through long animated scrolls:

```css
@media (prefers-reduced-motion: reduce) {
  html { scroll-behavior: auto; }
}
```

For focus/navigation changes, make sure the destination is also semantically and keyboard-accessibly appropriate; smooth movement alone does not manage focus.

---

# 63. Scroll Snap

Horizontal carousel:

```css
.carousel {
  display: flex;
  overflow-x: auto;
  scroll-snap-type: x mandatory;
  gap: 1rem;
}

.carousel > * {
  flex: 0 0 80%;
  scroll-snap-align: start;
}
```

Useful for:

- image galleries
- mobile card lists
- onboarding panels

Do not make scrolling difficult or trap users.


## Snap the scroll container, then align children

The parent defines the snapping axis/strictness; children define their alignment.

```css
.scroller {
  display: grid;
  grid-auto-flow: column;
  grid-auto-columns: min(80%, 22rem);
  gap: 1rem;
  overflow-x: auto;
  scroll-snap-type: x proximity;
}

.scroller > * {
  scroll-snap-align: start;
}
```

`mandatory` snapping is stronger than `proximity`. Prefer `proximity` when strict snapping would make it difficult to stop at arbitrary content.

Useful companion properties include `scroll-padding`, `scroll-margin`, and `scroll-snap-stop`.

**Accessibility/UX:** preserve normal scrolling controls, keyboard reachability, and content visibility. CSS scroll snap should improve navigation, not imitate a carousel that traps the user.

---

# 64. Sticky UI Patterns

Sticky header:

```css
.site-header {
  position: sticky;
  top: 0;
  z-index: 100;
}
```

Sticky table column:

```css
td:first-child,
th:first-child {
  position: sticky;
  left: 0;
  background: white;
}
```

Sticky can fail if an ancestor's overflow/layout behavior prevents the expected scroll context.


## Sticky is constrained by its scroll container

A sticky element behaves like a normal-flow element until a threshold is crossed, then stays within the bounds of its containing/scrolling context.

```css
.section-nav {
  position: sticky;
  top: 1rem;
  align-self: start;
}
```

In grid/flex layouts, stretching can leave no room for visible sticky movement, so `align-self: start` is sometimes important.

Common reasons sticky appears broken:

- no inset such as `top`,
- an ancestor is the unexpected scroll container,
- the sticky element is as tall as its container,
- layout/stretching leaves no travel range.

Use sticky for headers, section navigation, or key table columns when persistent context helps users. Avoid covering too much of a small screen.

---

# 65. Multi-column Layout

Useful for article-like content:

```css
.article {
  columns: 3 18rem;
  column-gap: 2rem;
}
```

Avoid for UI layouts where row alignment matters.


## Columns are for flowing content

Multi-column layout automatically flows content from one column into the next, similar to newspaper columns:

```css
.article {
  column-width: 18rem;
  column-gap: 2rem;
}
```

This is different from Grid. You generally do not place independent cards into exact row/column coordinates.

Control awkward breaks when useful:

```css
.article h2 {
  break-after: avoid;
}

.figure {
  break-inside: avoid;
}
```

Multi-column text can be hard to read on short viewports because users may need to scroll down and then back up to the next column. Test the real reading experience before using many columns.

Use Grid/Flexbox for application UI; use multicol for continuous editorial content.

---

# 66. Print CSS

```css
@media print {
  nav,
  .no-print,
  button {
    display: none;
  }

  body {
    color: black;
    background: white;
  }

  .invoice {
    box-shadow: none;
    border: 0;
  }
}
```

Useful for:

- invoices
- reports
- receipts
- printable forms


## Print is a different output medium

A page that works on screen may waste paper or hide useful link destinations when printed. Print styles can simplify navigation, remove interactive-only controls, and avoid awkward page breaks.

```css
@media print {
  a[href]::after {
    content: " (" attr(href) ")";
  }

  table,
  figure {
    break-inside: avoid;
  }
}
```

Only add printed URLs when they are actually useful; internal anchors or very long tracking URLs can create noise.

Useful print-related properties include `break-before`, `break-after`, and `break-inside`. Browser print engines differ, so test the output for invoices/reports that are operationally important.

**Security note:** hiding something with print CSS does not make sensitive data private. Control sensitive content at the application/data level.

---

# 67. Dark Mode and Theming

A variable-based theme:

```css
:root {
  --bg: #ffffff;
  --surface: #f8fafc;
  --text: #0f172a;
  --border: #e2e8f0;
}

[data-theme="dark"] {
  --bg: #0f172a;
  --surface: #1e293b;
  --text: #f8fafc;
  --border: #334155;
}

body {
  background: var(--bg);
  color: var(--text);
}
```

System preference:

```css
@media (prefers-color-scheme: dark) {
  :root {
    --bg: #111827;
    --text: #f9fafb;
  }
}
```


## Separate preference from explicit user choice

A common strategy is:

1. use semantic custom properties;
2. provide a light set;
3. provide a dark set;
4. optionally initialize from `prefers-color-scheme`;
5. let an explicit application preference override the system setting.

```css
:root {
  color-scheme: light dark;
}
```

`color-scheme` can also tell the browser which color schemes the page supports so built-in UI such as form controls can render appropriately.

Do not create dark mode by simply inverting colors. Re-evaluate surfaces, borders, muted text, images, charts, focus rings, shadows, and status colors.

**Common mistake:** defining both system dark mode and `[data-theme]` rules without a clear priority model. Decide which source wins when the user explicitly chooses a theme.

---

# 68. Accessibility

CSS can improve or damage accessibility.

## Keep visible keyboard focus

```css
:focus-visible {
  outline: 3px solid #2563eb;
  outline-offset: 3px;
}
```

---

## Avoid relying only on color

Bad:

```text
red = error
green = success
```

Better:

Use:

- icon
- text
- border
- label
- color

together.

---

## Contrast

Text should have sufficient contrast against its background.

---

## Touch target size

Avoid tiny clickable areas.

A practical pattern:

```css
.icon-button {
  min-width: 44px;
  min-height: 44px;
}
```

---

## Do not visually reorder meaningful content carelessly

CSS grid/flex order can create a mismatch between visual order and keyboard/screen-reader reading order.

Keep DOM order meaningful.


## CSS accessibility is part of component correctness

Test more than color contrast. A component should still work when:

- browser zoom is increased,
- text size is enlarged,
- content becomes longer,
- focus moves by keyboard,
- high-contrast/forced-color modes are active where relevant,
- animation is reduced.

Avoid CSS that hides overflow around focused controls:

```css
.panel {
  overflow: visible; /* or provide enough focus-ring space */
}
```

Do not use `order`, grid placement, or absolute positioning to create a visual reading order that contradicts the DOM's logical order.

For state, combine visual and semantic signals. CSS can style `[aria-invalid="true"]`, `[aria-current="page"]`, or `[aria-expanded="true"]`, but JavaScript/HTML must set those states correctly.

Accessibility is not a final polish step; it changes how layout and states should be designed.

---

# 69. Reduced Motion

```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

A more refined implementation can selectively preserve useful state changes while removing decorative motion.


## Prefer targeted reduction over a universal kill switch

The common "set every duration to 0.01ms" snippet is useful as a defensive baseline, but a production design can be more intentional.

```css
@media (prefers-reduced-motion: reduce) {
  .decorative-parallax,
  .ambient-spinner {
    animation: none;
    transform: none;
  }

  .accordion {
    transition-duration: 0.01ms;
  }
}
```

Some motion communicates a state change; removing it entirely may make the interface harder to understand. The goal is to remove or reduce non-essential movement, especially large, continuous, parallax, or zooming effects.

Also remember that JavaScript animation libraries need to respect the same preference; CSS media queries do not automatically disable script-driven motion.

---

# 70. CSS Architecture

CSS architecture is how you organize and scale styles.

A good system tries to achieve:

- predictable naming
- low specificity
- reusable components
- minimal leakage
- easy deletion
- clear ownership
- consistent spacing and colors
- theme support
- manageable overrides

Common approaches:

- BEM
- OOCSS
- SMACSS
- ITCSS
- utility-first
- CSS Modules
- component-scoped CSS
- design tokens


## Architecture is about change cost

A CSS architecture succeeds when a developer can safely answer:

```text
Where should this rule live?
What can it affect?
How do I override it?
Can I delete it?
Which values are shared?
```

Do not choose BEM, ITCSS, utilities, or modules because the acronym sounds professional. Choose conventions that match the team, codebase size, framework, and component boundaries.

A small site may need only:

```text
tokens.css
base.css
components.css
utilities.css
```

A large design system may justify layers, package boundaries, linting, and documented public component APIs.

**Best practice:** keep specificity predictable, make global rules rare and intentional, and treat generated/third-party CSS separately from application-owned CSS.

---

# 71. BEM

BEM means:

- Block
- Element
- Modifier

Example:

```html
<article class="card card--featured">
  <h2 class="card__title">Premium Plan</h2>
  <p class="card__description">For larger teams.</p>
</article>
```

```css
.card {}
.card__title {}
.card__description {}
.card--featured {}
```

Advantages:

- clear relationship
- reusable naming
- predictable specificity

Avoid:

```css
.card__header__title__icon
```

BEM elements belong to the block, not to a chain of parent element names.


## When BEM helps

BEM is useful in global CSS codebases because a class name carries the component relationship without depending on DOM depth.

```css
.invoice-card {}
.invoice-card__total {}
.invoice-card--overdue {}
```

A modifier describes a variation/state of the block or element; it normally appears alongside the base class:

```html
<article class="invoice-card invoice-card--overdue">
```

BEM does not require every descendant to have a class. Semantic elements can remain unclassed when no styling hook is needed.

**Common mistake:** reproducing DOM nesting in class names such as `.card__header__title__icon`. Prefer `.card__icon` if that is still an element of the card block, or split a genuinely independent subcomponent into its own block.

---

# 72. OOCSS

Object-Oriented CSS encourages separation of:

- structure
- skin/appearance

Example structure:

```css
.media {
  display: flex;
  gap: 1rem;
}
```

Appearance:

```css
.surface {
  background: white;
  border: 1px solid #ddd;
  border-radius: 12px;
}
```

Then combine:

```html
<div class="media surface">
  ...
</div>
```


## The two classic ideas

OOCSS is commonly summarized as:

1. separate structure from skin;
2. separate container from content.

A reusable media object's spacing/layout should not depend on whether it appears in a sidebar, modal, or main page.

```css
.media { display: flex; gap: 1rem; }
.surface--raised { box-shadow: var(--shadow-md); }
```

Composition can reduce duplication, but too many tiny classes can drift toward a utility system. That is not inherently bad; the team should be explicit about the chosen abstraction style.

Use OOCSS ideas when repeated visual objects share layout behavior across contexts. Do not force every style into a reusable "object" if it only belongs to one component.

---

# 73. SMACSS

SMACSS organizes styles into categories such as:

- Base
- Layout
- Module
- State
- Theme

Example conceptual folders:

```text
styles/
  base/
  layout/
  modules/
  states/
  themes/
```

Useful when teams want category-based CSS organization.


## The categories answer "what kind of rule is this?"

A SMACSS-style codebase separates concerns:

```text
Base    → element defaults
Layout  → major page regions
Module  → reusable UI components
State   → temporary/interactive states
Theme   → visual theme differences
```

For example:

```css
/* Module */
.card { ... }

/* State */
.card.is-loading { ... }
```

The value of SMACSS is not the exact folder names; it is the discipline of recognizing that a global element rule, a page-shell rule, and a component state have different responsibilities.

Use it when category-based organization helps a team navigate a large global stylesheet. In component-scoped ecosystems, some of these boundaries may already be enforced by tooling.

---

# 74. ITCSS

ITCSS organizes styles from broad/low-specificity rules to narrow/high-specificity rules.

Typical conceptual order:

```text
settings
tools
generic
elements
objects
components
utilities
```

This can make the cascade easier to control in large codebases.


## The triangle idea

ITCSS arranges CSS from broad, low-specificity, far-reaching concerns toward narrow, more explicit concerns. Earlier layers should generally be easier for later layers to override.

A common sequence:

```text
Settings   → tokens/variables
Tools      → mixins/functions (preprocessor)
Generic    → resets
Elements   → unclassed element defaults
Objects    → layout abstractions
Components → concrete UI
Utilities  → narrow overrides
```

The exact names can vary. The important idea is **dependency direction and cascade control**.

ITCSS is most useful in large global CSS/preprocessor codebases. If CSS Modules or shadow DOM already isolates most components, you may use only parts of the model rather than reproducing the entire structure.

---

# 75. Utility-First CSS

Utility classes perform one narrow styling job.

```css
.flex {
  display: flex;
}

.items-center {
  align-items: center;
}

.gap-2 {
  gap: 0.5rem;
}
```

HTML:

```html
<div class="flex items-center gap-2">
  ...
</div>
```

Advantages:

- fast composition
- predictable behavior
- fewer one-off selectors

Tradeoffs:

- markup can become class-heavy
- requires conventions
- abstraction strategy differs from semantic component CSS


## Utilities move composition into markup

A utility is intentionally small and reusable:

```css
.stack-sm { gap: 0.5rem; }
.text-muted { color: var(--text-muted); }
```

A mature utility system needs a constrained design scale; otherwise developers create endless one-off classes and lose consistency.

Utilities are excellent for spacing, display, alignment, and common design tokens. Component classes can still be valuable for complex or repeated domain-specific visuals. Many real systems combine both approaches.

**Common mistake:** judging utility-first only by class-list length. The real tradeoff is where the styling API lives—markup vs stylesheet—and how reuse, consistency, state variants, and design constraints are managed.

---

# 76. CSS Modules and Scoped Styles

A CSS Module may contain:

```css
.card {
  padding: 1rem;
}
```

A build tool can generate a scoped class name so `.card` does not collide globally.

Useful in component frameworks.

Other ecosystems may provide framework-specific scoped styles.


## What problem they solve

Global CSS shares one selector namespace across the page. In a large component application, two unrelated `.title` rules can collide.

CSS Modules solve this at build time by mapping local class names to generated identifiers:

```js
import styles from "./Card.module.css";

// conceptual usage
<div className={styles.card}>...</div>
```

The source can stay readable while the emitted class name is scoped.

"Scoped styles" in frameworks are implementation-specific; some rewrite selectors with generated attributes, while shadow DOM provides a different browser-level boundary. Learn the behavior of your framework rather than assuming all scoping systems are identical.

Global styles are still appropriate for resets, tokens, typography defaults, and truly global utilities.

---

# 77. Design Tokens

Design tokens are reusable design decisions.

```css
:root {
  --color-primary-500: #2563eb;
  --color-danger-500: #dc2626;

  --space-1: 0.25rem;
  --space-2: 0.5rem;
  --space-3: 0.75rem;
  --space-4: 1rem;
  --space-6: 1.5rem;
  --space-8: 2rem;

  --radius-sm: 6px;
  --radius-md: 10px;
  --radius-lg: 16px;

  --shadow-sm: 0 1px 2px rgb(0 0 0 / 0.08);
  --shadow-md: 0 8px 24px rgb(0 0 0 / 0.1);
}
```

Semantic mapping:

```css
:root {
  --color-action: var(--color-primary-500);
  --color-error: var(--color-danger-500);
}
```

This makes redesigns much easier.


## Raw tokens vs semantic tokens

Raw/primitives describe the palette/scale:

```css
--blue-600: #2563eb;
--space-4: 1rem;
```

Semantic tokens describe intent:

```css
--color-action: var(--blue-600);
--space-card-padding: var(--space-4);
```

Components should prefer semantic intent when possible:

```css
.button--primary {
  background: var(--color-action);
}
```

Then a brand or theme can remap the semantic token without rewriting the component.

Tokens can represent color, spacing, radius, typography, shadow, motion, and z-index. Do not create a token for every literal automatically; a token is most useful when the value is shared, constrained, themeable, or part of a deliberate design decision.

Document token meaning so names do not become another set of unexplained magic values.

---

# 78. Reusable Component Patterns

A component should generally have:

- a base
- optional variants
- optional sizes
- states
- clear child element classes

Example:

```css
.alert {
  display: flex;
  gap: 0.75rem;
  padding: 1rem;
  border: 1px solid;
  border-radius: 10px;
}

.alert--success {
  color: #166534;
  background: #f0fdf4;
  border-color: #bbf7d0;
}

.alert--danger {
  color: #991b1b;
  background: #fef2f2;
  border-color: #fecaca;
}
```


## Define a stable component API

A maintainable CSS component makes its variations predictable:

```text
base      .alert
element   .alert__icon
variant   .alert--danger
state     .is-loading or [aria-busy="true"]
```

Keep the base responsible for shared structure; variants should change only what is different.

```css
.alert {
  --alert-accent: #2563eb;
  border-inline-start: 4px solid var(--alert-accent);
}

.alert--danger {
  --alert-accent: #dc2626;
}
```

This token-based variant avoids duplicating the whole component.

Test components with missing optional content, long text, narrow containers, disabled/loading states, and different themes. A component is reusable only if its assumptions are clear and its edge cases do not require ad-hoc overrides everywhere.

---

# 79. Common Layout Recipes

## Center anything

```css
.center {
  display: grid;
  place-items: center;
}
```

---

## Sidebar + main

```css
.layout {
  display: grid;
  grid-template-columns: minmax(220px, 280px) 1fr;
  gap: 2rem;
}
```

Responsive:

```css
@media (max-width: 800px) {
  .layout {
    grid-template-columns: 1fr;
  }
}
```

---

## Auto-responsive cards

```css
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(260px, 100%), 1fr));
  gap: 1rem;
}
```

---

## Full-height application shell

```css
.app {
  min-height: 100dvh;
  display: grid;
  grid-template-rows: auto 1fr auto;
}
```


## Choose the recipe by layout intent

Use Grid for page/track relationships and Flexbox for alignment/distribution along one main axis.

For example, a toolbar is naturally flex-based:

```css
.toolbar {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 0.75rem;
}
```

A dashboard card region is naturally grid-based:

```css
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(18rem, 100%), 1fr));
  gap: 1rem;
}
```

Avoid copying a recipe without understanding its constraints. `minmax(0, 1fr)` is often used in application shells so long content can shrink rather than force overflow. `min(260px, 100%)` keeps a minimum-track recipe from overflowing containers narrower than 260px.

Treat recipes as starting points, then test real content.

---

# 80. Navigation Patterns

Horizontal navigation:

```css
.nav {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.nav a {
  color: inherit;
  text-decoration: none;
}

.nav a:hover {
  text-decoration: underline;
}
```

Responsive wrapping:

```css
.nav {
  flex-wrap: wrap;
}
```

Do not hide important navigation solely based on hover because touch devices do not have reliable hover interaction.


## Styling navigation also means styling states

A usable navigation component usually needs:

- default links,
- hover,
- keyboard focus,
- current/active state,
- wrapping or an intentional mobile strategy.

```css
.nav a[aria-current="page"] {
  font-weight: 700;
  text-decoration-thickness: 0.15em;
}

.nav a:focus-visible {
  outline: 2px solid currentColor;
  outline-offset: 3px;
}
```

CSS should not turn a long navigation into an inaccessible hover-only dropdown. Menus with disclosure behavior need appropriate HTML/JavaScript state and keyboard handling.

When navigation wraps, verify that spacing works between rows as well as columns (`gap` is useful). On small screens, prefer a deliberately designed pattern rather than simply shrinking text until everything fits.

---

# 81. Card Patterns

```css
.card {
  display: grid;
  gap: 1rem;
  padding: 1.25rem;
  border: 1px solid #e2e8f0;
  border-radius: 12px;
  background: white;
}

.card__image {
  width: 100%;
  aspect-ratio: 16 / 10;
  object-fit: cover;
  border-radius: 8px;
}

.card__title {
  margin: 0;
}

.card__actions {
  display: flex;
  gap: 0.75rem;
  margin-top: auto;
}
```


## Cards are a visual pattern, not an HTML element

Choose the HTML based on meaning: a product card might be `<article>`, a navigation card may contain a link, and a purely visual grouping may be a `<div>`.

For equal-height action alignment:

```css
.card {
  display: flex;
  flex-direction: column;
}

.card__actions {
  margin-block-start: auto;
}
```

But do not force equal heights if it creates excessive empty space or hides variable content.

If the whole card is clickable, be careful not to nest interactive controls inside an enclosing link. Often it is better to make the title link the primary navigation target and style the card hover/focus state around it.

Test card grids with long titles, missing images, and localized text.

---

# 82. Modal Pattern

Visual CSS example:

```css
.modal-backdrop {
  position: fixed;
  inset: 0;
  display: grid;
  place-items: center;
  padding: 1rem;
  background: rgb(0 0 0 / 0.55);
  z-index: var(--z-modal);
}

.modal {
  width: min(600px, 100%);
  max-height: min(80dvh, 700px);
  overflow: auto;
  padding: 1.5rem;
  border-radius: 14px;
  background: white;
}
```

Important: modal accessibility cannot be solved with CSS alone. You also need correct semantics, focus handling, keyboard behavior, and appropriate scripting.


## CSS is only the visual layer

A production modal also needs behavior:

```text
open → move focus appropriately
while open → prevent confusing background interaction as required
Escape/close control → close
close → restore focus to the trigger when appropriate
```

Use the native `<dialog>` element when it fits the product/browser requirements because it provides useful platform behavior, but you still need correct labeling and application logic.

For CSS, allow small-screen overflow:

```css
.modal {
  width: min(40rem, calc(100% - 2rem));
  max-height: calc(100dvh - 2rem);
  overflow: auto;
}
```

**Common mistake:** giving the modal a fixed height or hiding overflow, which can make fields/buttons unreachable when text grows or the on-screen keyboard reduces the viewport.

---

# 83. Tooltip Pattern

Basic visual styling:

```css
.tooltip {
  position: absolute;
  max-width: 240px;
  padding: 0.5rem 0.75rem;
  border-radius: 6px;
  background: #111827;
  color: white;
  font-size: 0.875rem;
}
```

Tooltips need more than CSS for complete accessible interaction behavior in many real applications.


## Decide whether a tooltip is the right pattern

A tooltip is supplementary information attached to a trigger. Essential instructions should be visible without requiring hover.

A robust implementation needs to consider:

- keyboard focus as well as pointer hover,
- touch interaction,
- accessible association with the trigger,
- positioning near viewport edges,
- dismissal behavior,
- keeping the tooltip available long enough to read.

CSS handles the appearance; JavaScript or a well-tested UI primitive often handles positioning and interaction.

If the content is interactive or contains multiple actions, it is no longer a simple tooltip; a popover/disclosure pattern is usually more appropriate.

---

# 84. Form Layout Patterns

Two-column form:

```css
.form-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 1rem;
}

.form-field--full {
  grid-column: 1 / -1;
}

@media (max-width: 700px) {
  .form-grid {
    grid-template-columns: 1fr;
  }
}
```

Use this for:

- user profile
- invoice metadata
- purchase order details
- registration forms


## Let field content determine row height

Grid is excellent for multi-column forms, but keep logical reading/tab order in the DOM. Do not visually rearrange fields into an order that differs from keyboard navigation.

A responsive pattern can avoid a hard-coded breakpoint:

```css
.form-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(18rem, 100%), 1fr));
  gap: 1rem;
}
```

Use explicit full-width spans for fields such as addresses or notes when needed.

Keep labels and error/help text in the same field component, and allow errors to wrap without overlapping neighboring fields.

**Common mistake:** fixing row heights to keep a pristine mockup. Validation messages and translations are variable content; the layout should expand naturally.

---

# 85. Dashboard Layout Pattern

```css
.dashboard {
  display: grid;
  grid-template-columns: 260px minmax(0, 1fr);
  min-height: 100dvh;
}

.dashboard__main {
  min-width: 0;
  padding: 1.5rem;
}

.dashboard__cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(220px, 100%), 1fr));
  gap: 1rem;
}
```

`min-width: 0` is important when charts/tables or long content would otherwise force overflow.


## Build the shell and content regions separately

A dashboard shell often has a navigation region and a fluid main region, but the main region itself should establish sensible overflow behavior.

```css
.dashboard__main {
  min-width: 0;
}

.chart-card,
.table-card {
  min-width: 0;
}
```

Without `min-width: 0`, grid/flex items can honor their min-content size and force the entire page wider than the viewport.

On small screens, a sidebar may become an off-canvas/disclosure interface. CSS can change visibility/layout, but opening/closing a modal-like drawer needs accessible interaction behavior.

Avoid a single giant `overflow: hidden` on the dashboard root; it can hide focus rings and prevent expected document scrolling.

---

# 86. Holy Grail Layout

```css
.page {
  min-height: 100dvh;
  display: grid;
  grid-template:
    "header header header" auto
    "left main right" 1fr
    "footer footer footer" auto
    / 220px minmax(0, 1fr) 220px;
}
```

Responsive version:

```css
@media (max-width: 900px) {
  .page {
    grid-template:
      "header" auto
      "main" 1fr
      "left" auto
      "right" auto
      "footer" auto
      / 1fr;
  }
}
```


## Why Grid fits this pattern

The "Holy Grail" layout historically meant header/footer plus main content and two sidebars. Old techniques used floats and complex source-order tricks; Grid can name regions directly.

Named areas are especially readable:

```css
.page__header { grid-area: header; }
.page__left   { grid-area: left; }
.page__main   { grid-area: main; }
.page__right  { grid-area: right; }
.page__footer { grid-area: footer; }
```

Keep the DOM in a meaningful reading order even when the visual grid changes.

Do not assume both sidebars are always present. Real components may need conditional layouts or a simpler `minmax()` track definition. Test long main content so side columns do not unexpectedly expand.

---

# 87. Responsive Sidebar Pattern

```css
.shell {
  display: grid;
  grid-template-columns: 260px minmax(0, 1fr);
}

@media (max-width: 768px) {
  .shell {
    grid-template-columns: 1fr;
  }

  .sidebar {
    display: none;
  }
}
```

In a real accessible navigation drawer, JavaScript may control open/close state, focus management, and ARIA attributes.


## Hiding is not the only mobile strategy

`display: none` is fine when the sidebar content is genuinely optional at that breakpoint. Navigation and filters often remain important, so they usually need a trigger that reveals the same content as a drawer/disclosure.

A CSS layout can switch tracks:

```css
@media (width < 48rem) {
  .shell {
    grid-template-columns: 1fr;
  }
}
```

Then application state can control whether a drawer is open.

Do not maintain separate desktop and mobile copies of the same navigation unless you have a strong reason; duplicated DOM can create inconsistent state, duplicate IDs, and extra maintenance. Prefer one semantic source that changes presentation where practical.

---

# 88. Truncation and Long Content

Single line:

```css
.truncate {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
```

Breaking long values:

```css
.break-anywhere {
  overflow-wrap: anywhere;
}
```

For multi-line clamping, browser-specific behavior may be needed depending on the project requirements. Always keep critical information accessible rather than relying on visual truncation alone.


## Truncation requires a product decision

Ellipsis is useful when users can identify an item from the visible prefix and the complete value is available elsewhere. It is dangerous for invoice numbers, filenames, email addresses, or other values where the hidden ending may distinguish records.

For flexible layouts, also allow children to shrink:

```css
.row__content {
  min-width: 0;
}

.row__title {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
```

Without `min-width: 0`, a flex/grid child may refuse to shrink and the ellipsis never appears.

For long URLs/IDs that should wrap, prefer:

```css
overflow-wrap: anywhere;
```

Test copy/select behavior and accessible names before truncating operational data.

---

# 89. CSS Reset and Normalize

Browsers provide default styles.

A minimal reset:

```css
*,
*::before,
*::after {
  box-sizing: border-box;
}

html {
  -webkit-text-size-adjust: 100%;
}

body {
  margin: 0;
  min-height: 100dvh;
}

img,
picture,
video,
canvas,
svg {
  display: block;
  max-width: 100%;
}

input,
button,
textarea,
select {
  font: inherit;
}
```

A reset removes or standardizes defaults.

A normalization approach tries to preserve useful defaults while making browser behavior more consistent.


## Reset vs normalize vs project baseline

A reset aggressively removes browser defaults; normalization keeps useful defaults while smoothing inconsistencies; a project baseline adds your own opinionated foundations.

A small modern baseline often includes:

```css
*,
*::before,
*::after {
  box-sizing: border-box;
}

body {
  margin: 0;
}

button,
input,
select,
textarea {
  font: inherit;
}
```

Do not blindly remove every default style. Native margins, focus indicators, list markers, and form-control behavior often carry usability value.

If using a framework, understand whether it already includes a reset/reboot. Adding a second global reset can produce confusing differences.

Keep baseline rules low-specificity so components can override them without a cascade fight.

---

# 90. Browser Compatibility

Before using a new CSS feature in production:

1. know your supported browser list
2. check feature support
3. provide fallbacks where needed
4. test real target browsers
5. use progressive enhancement

Example fallback:

```css
.card {
  display: block;
}

@supports (display: grid) {
  .card-list {
    display: grid;
  }
}
```


## Compatibility is a project requirement, not a universal list

Define the browsers/versions your product supports based on users, contractual requirements, analytics, and organizational policy. Then evaluate features against that matrix.

Use three strategies:

```text
fallback              → older browser gets a simpler value
progressive enhancement → advanced feature only when supported
transformation/polyfill → build/runtime tool supplies compatibility
```

`@supports` is useful when support can be detected with a CSS condition, but it cannot represent every behavioral browser bug.

Keep compatibility tests in real target browsers or a reliable browser-testing service. "Works in my Chrome" is not a compatibility strategy.

When a new feature is only decorative, a graceful fallback may be much cheaper than shipping a complex polyfill.

---

# 91. Progressive Enhancement

Start with a working baseline.

Then add advanced styling where supported.

```css
.gallery {
  display: block;
}

@supports (display: grid) {
  .gallery {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
  }
}
```

Your page should remain usable even when a decorative enhancement is unavailable.


## Start from the required outcome

Progressive enhancement asks: "What is the simplest version that still lets the user complete the task?" Then richer layout/effects are layered on.

For a product grid:

```css
.products > * + * {
  margin-top: 1rem;
}

@supports (display: grid) {
  .products {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(16rem, 1fr));
    gap: 1rem;
  }

  .products > * + * {
    margin-top: 0;
  }
}
```

The baseline remains readable if Grid is unavailable.

This principle also applies to motion, container queries, masks, and other newer features. Decide whether the feature is **required for function** or merely an enhancement; that determines how much fallback work is necessary.

---

# 92. CSS Performance

CSS performance usually matters most when large pages, complex rendering, animations, and heavy effects interact.

Good practices:

- keep selectors understandable
- avoid huge unused stylesheets
- split critical and non-critical CSS appropriately
- minimize expensive visual effects on large regions
- avoid animating layout-heavy properties when a transform can achieve the same visual effect
- reduce unnecessary web fonts
- compress production CSS
- cache static CSS assets
- remove dead styles
- avoid massive DOM + CSS combinations
- profile rather than guessing

## Animation example

Often preferable:

```css
.item {
  transform: translateX(0);
}

.item.is-open {
  transform: translateX(200px);
}
```

Rather than repeatedly animating layout dimensions when not required.


## Measure the actual bottleneck

"Complex selector" micro-optimizations are rarely the first place to look in a normal application. More common costs include large DOMs, heavy paint effects, layout thrashing caused by script, oversized/unnecessary CSS, and animations that trigger repeated layout/paint work.

A useful investigation flow:

```text
1. reproduce the slowdown
2. record a Performance trace
3. identify layout/paint/composite work
4. reduce the expensive cause
5. record again
```

Properties such as `transform` and `opacity` are often animation-friendly, but they are not magically free. Large layers, blur/filter effects, and excessive `will-change` can consume memory.

Use `content-visibility`/containment only when you understand the layout/accessibility implications and have measured a benefit.

Optimize delivery too: minify, compress, cache, and remove CSS that the application never uses.

---

# 93. Debugging CSS

A systematic process:

## Step 1: Is the selector matching?

Use browser DevTools.

Check whether the rule appears.

---

## Step 2: Is the declaration crossed out?

If yes, another rule may be winning.

Inspect:

- specificity
- source order
- layer order
- `!important`
- inherited values

---

## Step 3: Is the property valid?

Example typo:

```css
widht: 100%;
```

Browser ignores unknown properties.

---

## Step 4: Check box sizes

Inspect:

- content
- padding
- border
- margin

---

## Step 5: Check layout parent

For flex/grid problems, inspect the parent first.

---

## Step 6: Add temporary debug outlines

```css
* {
  outline: 1px solid rgb(255 0 0 / 0.15);
}
```

Use only temporarily.

---

## Step 7: Reduce the problem

Create a minimal reproduction.

Remove unrelated styles until the issue becomes obvious.

---

# 94. Common CSS Mistakes

## Mistake 1: Using fixed widths everywhere

Bad:

```css
.card {
  width: 600px;
}
```

Better:

```css
.card {
  width: min(600px, 100%);
}
```

---

## Mistake 2: Excessive absolute positioning

Do not use absolute positioning to build the entire page layout.

Use flexbox or grid.

---

## Mistake 3: Too much `!important`

Bad:

```css
.button {
  color: white !important;
}
```

Use `!important` deliberately, not as a default conflict solver.

---

## Mistake 4: Deep selectors

Bad:

```css
main .content .section .card .body p span {
  color: red;
}
```

Better:

```css
.card__highlight {
  color: red;
}
```

---

## Mistake 5: Removing focus styles

Bad:

```css
button {
  outline: none;
}
```

Better:

```css
button:focus-visible {
  outline: 3px solid #2563eb;
}
```

---

## Mistake 6: Using `<br>` for spacing

Spacing belongs in CSS.

---

## Mistake 7: Magic numbers everywhere

Bad:

```css
margin-top: 37px;
padding-left: 13px;
```

Prefer a spacing system.

---

## Mistake 8: Styling globally without scope

Risky:

```css
div {
  margin: 10px;
}
```

This can unintentionally affect every component.

---

# 95. Naming and File Organization

Example structure:

```text
styles/
├── reset.css
├── tokens.css
├── base.css
├── layout/
│   ├── container.css
│   ├── grid.css
│   └── app-shell.css
├── components/
│   ├── button.css
│   ├── card.css
│   ├── modal.css
│   └── table.css
├── utilities/
│   ├── spacing.css
│   └── visibility.css
└── themes/
    ├── light.css
    └── dark.css
```

Rules of thumb:

- name classes by purpose
- avoid names tied to current color when semantic meaning matters
- keep components small
- centralize repeated design values
- avoid giant files with unrelated styles

Bad:

```css
.red-button {}
.left-box {}
.big-text {}
```

Better:

```css
.button--danger {}
.sidebar {}
.page-title {}
```


## Organize around ownership and deletion

A folder tree is useful only if developers can predict where a change belongs. Pick one primary organizing idea—components, layers, routes, or packages—and document it.

For component-oriented CSS:

```text
components/
  button.css
  card.css
  invoice-table.css
```

Each file should ideally be removable with the component. Shared tokens/base rules live elsewhere.

Naming should describe purpose rather than accidental appearance:

```css
.status--danger   /* semantic */
.mt-2             /* deliberate utility */
```

is generally clearer than:

```css
.red-text-left
```

Avoid creating both a global class and a component-scoped class with the same responsibility. Duplication makes future changes inconsistent.

Use linting/formatting where it helps enforce agreed conventions, but keep the rules understandable to the team.

---

# 96. Real-World Mini Projects

Use these projects to practice progressively.

## Project 1: Profile card

Practice:

- box model
- typography
- border radius
- shadows
- flexbox

---

## Project 2: Responsive pricing page

Practice:

- CSS Grid
- cards
- media queries
- buttons
- badges

---

## Project 3: Login form

Practice:

- form styling
- focus states
- validation states
- responsive sizing
- accessibility

---

## Project 4: Admin dashboard

Practice:

- page shell
- sidebar
- responsive grid
- tables
- sticky header
- design tokens
- dark mode

---

## Project 5: Invoice page

Practice:

- print CSS
- tables
- grid/flex layout
- responsive behavior
- typography
- totals section

Example:

```css
.invoice {
  width: min(900px, 100%);
  margin-inline: auto;
  padding: clamp(1rem, 4vw, 3rem);
  background: white;
}

.invoice__meta {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 1rem;
}

.invoice__total {
  margin-left: auto;
  width: min(320px, 100%);
}

@media print {
  .invoice {
    width: 100%;
    padding: 0;
  }

  .no-print {
    display: none;
  }
}
```

---

## Project 6: Product gallery

Practice:

- responsive grid
- `object-fit`
- aspect ratio
- hover states
- badges
- text truncation

---

## Project 7: Component library

Build:

- button
- input
- select
- checkbox
- card
- alert
- badge
- modal
- tabs
- table
- pagination

Practice:

- naming
- tokens
- variants
- states
- accessibility
- architecture

---

# 97. Interview Questions

## What is the CSS box model?

Content, padding, border, and margin.

---

## What does `box-sizing: border-box` do?

It makes the declared width and height include padding and border.

---

## Flexbox vs Grid?

Flexbox is generally best for one-dimensional layout.

Grid is generally best for two-dimensional layout.

---

## Difference between `display: none` and `visibility: hidden`?

`display: none` removes the element from layout.

`visibility: hidden` keeps its layout space while hiding it visually.

---

## Difference between relative and absolute positioning?

`position: relative` keeps the element in normal flow and can establish a positioning context.

`position: absolute` removes the element from normal flow and positions it relative to a relevant containing block.

---

## What is specificity?

The selector weighting system used when competing declarations are otherwise at comparable cascade priority.

---

## What is the cascade?

The process the browser uses to choose which declaration wins.

---

## What is inheritance?

The mechanism through which some property values pass from parent elements to descendants.

---

## `em` vs `rem`?

`em` is based on font sizing in the current/local context.

`rem` is based on the root font size.

---

## What is a stacking context?

An isolated stacking environment that affects how z-index values are compared.

---

## What is the difference between pseudo-class and pseudo-element?

Pseudo-class:

```css
button:hover
```

Represents state or structural condition.

Pseudo-element:

```css
p::first-line
```

Represents a virtual part of an element.

---

## What does `min-width: 0` fix in flex/grid?

It allows an item to shrink below its min-content width, often preventing unexpected overflow.

---

## What is mobile-first CSS?

Write base rules for smaller screens, then progressively enhance for wider screens using `min-width` media queries.

---

## Why prefer `gap`?

It expresses spacing between layout items directly and avoids special margin rules for first/last items.

---

## Why are custom properties useful?

They allow reusable dynamic values for:

- themes
- design tokens
- components
- states
- responsive calculations

---

# 98. CSS Checklist

Before calling a page finished, check:

- [ ] `box-sizing: border-box` is applied consistently.
- [ ] Layout works on narrow screens.
- [ ] Layout works on wide screens.
- [ ] Text can grow without breaking layout.
- [ ] Long words/IDs/URLs do not destroy layout.
- [ ] Keyboard focus is visible.
- [ ] Color contrast is sufficient.
- [ ] Buttons have hover, focus, active, and disabled states when relevant.
- [ ] Forms clearly show labels and errors.
- [ ] Images are responsive.
- [ ] Images use proper aspect behavior.
- [ ] Tables are usable on small screens.
- [ ] Motion respects reduced-motion preferences.
- [ ] Print styles exist when the feature needs printing.
- [ ] CSS class names are understandable.
- [ ] Specificity is controlled.
- [ ] `!important` is not being used as a routine fix.
- [ ] No unnecessary fixed heights clip content.
- [ ] No unexplained z-index values such as `999999`.
- [ ] Components work in different container sizes.
- [ ] Dark mode has been checked if supported.
- [ ] Browser compatibility matches project requirements.
- [ ] Unused CSS is removed.
- [ ] DevTools shows no obvious overridden/invalid declarations caused by mistakes.
- [ ] Focus indicators are not clipped by overflow.
- [ ] UI still works at zoomed text/browser settings.
- [ ] Semantic DOM order matches meaningful reading order.

---

# 99. Learning Roadmap

## Stage 1: Absolute beginner

Learn:

1. syntax
2. selectors
3. colors
4. fonts
5. margin
6. padding
7. borders
8. width/height
9. box model

Build:

- profile card
- simple landing page section

---

## Stage 2: Layout fundamentals

Learn:

1. normal flow
2. display
3. position
4. flexbox
5. grid
6. overflow

Build:

- navbar
- two-column page
- card grid

---

## Stage 3: Responsive design

Learn:

1. percentages
2. `rem`
3. viewport units
4. `min()`
5. `max()`
6. `clamp()`
7. media queries
8. responsive images
9. container queries

Build:

- responsive pricing page
- mobile dashboard

---

## Stage 4: Component styling

Learn:

1. forms
2. buttons
3. tables
4. cards
5. modals
6. tooltips
7. badges
8. states

Build a small design system.

---

## Stage 5: Advanced CSS

Learn:

1. custom properties
2. cascade layers
3. nesting
4. scope
5. subgrid
6. advanced selectors
7. logical properties
8. transitions
9. animations
10. accessibility preferences

---

## Stage 6: Production CSS

Learn:

1. architecture
2. BEM / utility patterns
3. tokens
4. themes
5. browser compatibility
6. performance
7. debugging
8. maintainability
9. automated testing strategy around UI
10. team conventions

---

# 100. Quick Reference Cheat Sheet

## Center a page container

```css
.container {
  width: min(1120px, calc(100% - 2rem));
  margin-inline: auto;
}
```

## Center an item

```css
.center {
  display: grid;
  place-items: center;
}
```

## Flex row

```css
.row {
  display: flex;
  align-items: center;
  gap: 1rem;
}
```

## Space between

```css
.toolbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
}
```

## Responsive grid

```css
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(240px, 100%), 1fr));
  gap: 1rem;
}
```

## Truncate one line

```css
.truncate {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
```

## Responsive image

```css
img {
  max-width: 100%;
  height: auto;
}
```

## Cover image

```css
.image {
  width: 100%;
  height: 220px;
  object-fit: cover;
}
```

## Square item

```css
.square {
  aspect-ratio: 1;
}
```

## Sticky header

```css
.header {
  position: sticky;
  top: 0;
  z-index: 100;
}
```

## Full-screen overlay

```css
.overlay {
  position: fixed;
  inset: 0;
}
```

## Fluid heading

```css
h1 {
  font-size: clamp(2rem, 5vw, 4rem);
}
```

## Accessible focus

```css
:focus-visible {
  outline: 3px solid #2563eb;
  outline-offset: 3px;
}
```

## Theme variable

```css
:root {
  --brand: #2563eb;
}
```

## Basic card

```css
.card {
  padding: 1.25rem;
  border: 1px solid #e2e8f0;
  border-radius: 12px;
  background: white;
}
```

## Responsive two-column layout

```css
.layout {
  display: grid;
  grid-template-columns: 260px minmax(0, 1fr);
  gap: 2rem;
}

@media (max-width: 768px) {
  .layout {
    grid-template-columns: 1fr;
  }
}
```

---

# Bonus: A Strong Starter CSS File

```css
/* =========================
   1. Design tokens
   ========================= */

:root {
  --color-bg: #ffffff;
  --color-surface: #f8fafc;
  --color-text: #0f172a;
  --color-muted: #64748b;
  --color-border: #e2e8f0;
  --color-primary: #2563eb;
  --color-danger: #dc2626;

  --space-1: 0.25rem;
  --space-2: 0.5rem;
  --space-3: 0.75rem;
  --space-4: 1rem;
  --space-6: 1.5rem;
  --space-8: 2rem;

  --radius-sm: 6px;
  --radius-md: 10px;
  --radius-lg: 16px;

  --shadow-sm: 0 1px 3px rgb(0 0 0 / 0.08);
  --shadow-md: 0 10px 30px rgb(0 0 0 / 0.1);

  --content-width: 1120px;
}

/* =========================
   2. Reset
   ========================= */

*,
*::before,
*::after {
  box-sizing: border-box;
}

html {
  -webkit-text-size-adjust: 100%;
}

body {
  margin: 0;
  min-height: 100dvh;
  font-family:
    Inter,
    system-ui,
    -apple-system,
    BlinkMacSystemFont,
    "Segoe UI",
    sans-serif;
  line-height: 1.5;
  color: var(--color-text);
  background: var(--color-bg);
}

img,
picture,
video,
canvas,
svg {
  display: block;
  max-width: 100%;
}

input,
button,
textarea,
select {
  font: inherit;
}

button {
  cursor: pointer;
}

/* =========================
   3. Typography
   ========================= */

h1,
h2,
h3,
p {
  margin-block-start: 0;
}

h1,
h2,
h3 {
  line-height: 1.2;
}

p {
  max-width: 70ch;
}

/* =========================
   4. Layout
   ========================= */

.container {
  width: min(var(--content-width), calc(100% - 2rem));
  margin-inline: auto;
}

.stack {
  display: grid;
  gap: var(--space-4);
}

.cluster {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: var(--space-3);
}

.auto-grid {
  display: grid;
  grid-template-columns: repeat(
    auto-fit,
    minmax(min(240px, 100%), 1fr)
  );
  gap: var(--space-4);
}

/* =========================
   5. Components
   ========================= */

.button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: var(--space-2);
  min-height: 44px;
  padding: 0.75rem 1rem;
  border: 1px solid transparent;
  border-radius: var(--radius-md);
  font-weight: 600;
}

.button--primary {
  color: white;
  background: var(--color-primary);
}

.button--danger {
  color: white;
  background: var(--color-danger);
}

.card {
  padding: var(--space-6);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-lg);
  background: var(--color-bg);
  box-shadow: var(--shadow-sm);
}

/* =========================
   6. Accessibility
   ========================= */

:focus-visible {
  outline: 3px solid rgb(37 99 235 / 0.35);
  outline-offset: 3px;
}

@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    scroll-behavior: auto !important;
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

# Bonus: CSS Decision Guide

Ask these questions when choosing a technique.

## I need to align items in one row

Use Flexbox.

```css
display: flex;
```

---

## I need rows and columns

Use Grid.

```css
display: grid;
```

---

## I need a component to adapt to its parent size

Consider a container query.

---

## I need a page to adapt to viewport width

Use flexible layout plus media queries when required.

---

## I need an item in a corner of its card

Use a relatively positioned parent and absolutely positioned child.

---

## I need an element pinned to the viewport

Use `position: fixed`.

---

## I need an element that follows scrolling and then sticks

Use `position: sticky`.

---

## I need responsive text size

Use `clamp()`.

---

## I need reusable colors or spacing

Use custom properties/design tokens.

---

## I need a visual variant of a component

Use a modifier class or data attribute.

Example:

```css
.button[data-variant="danger"] {
  background: #dc2626;
}
```

---

# Bonus: Practice Challenges

Try solving these without copying the answer first.

## Challenge 1

Create a button group where:

- buttons sit in a row
- they wrap on small screens
- spacing stays consistent

Hint: Flexbox + `gap` + `flex-wrap`.

---

## Challenge 2

Create a card grid where:

- large screens show many columns
- smaller screens automatically show fewer columns
- no breakpoint is required

Hint:

```css
repeat(auto-fit, minmax(...))
```

---

## Challenge 3

Create an invoice layout where:

- supplier information is left
- customer information is right
- mobile view stacks them
- print view removes action buttons

---

## Challenge 4

Create a sidebar dashboard where:

- sidebar is 260px
- main area fills remaining space
- main tables do not force the page wider than the viewport

Hint:

```css
grid-template-columns: 260px minmax(0, 1fr);
```

---

## Challenge 5

Create a theme using only custom properties.

Switch between:

- light
- dark

without duplicating component declarations.

---

# Final Principles to Remember

1. **Understand the cascade before fighting it.**
2. **Prefer classes over overly specific selectors.**
3. **Use Flexbox and Grid instead of layout hacks.**
4. **Design for flexible content, not only perfect sample text.**
5. **Use responsive constraints instead of fixed dimensions everywhere.**
6. **Keep keyboard focus visible.**
7. **Use semantic HTML and let CSS style it.**
8. **Treat CSS variables as a design-system tool, not only a convenience.**
9. **Keep component selectors shallow and predictable.**
10. **Use design tokens for repeated colors, sizes, spacing, radius, and shadows.**
11. **Use media queries for viewport-level changes and container queries for reusable component-level changes.**
12. **Use `min-width: 0` when flex/grid children overflow unexpectedly.**
13. **Do not use `!important` as your default conflict-resolution strategy.**
14. **Test real content: long names, large numbers, errors, empty states, and translations.**
15. **Respect reduced-motion and user color preferences when relevant.**
16. **Use DevTools constantly.**
17. **Prefer maintainable CSS over clever CSS.**
18. **Learn patterns, then understand when not to use them.**
19. **CSS mastery comes from building layouts, debugging failures, and refactoring working code.**
20. **A good stylesheet should be easy for another developer to understand and safely change.**

---

# Suggested Mastery Sequence

```text
HTML structure
    ↓
CSS syntax
    ↓
Selectors
    ↓
Cascade + Specificity + Inheritance
    ↓
Box Model
    ↓
Normal Flow
    ↓
Flexbox
    ↓
Grid
    ↓
Responsive Design
    ↓
Typography + Forms + Media
    ↓
Pseudo Classes + Pseudo Elements
    ↓
Custom Properties
    ↓
Transforms + Transitions + Animations
    ↓
Modern CSS
    ↓
Accessibility
    ↓
Architecture + Design Systems
    ↓
Performance + Debugging
    ↓
Production Projects
```

---

## End of CSS Mastery Handbook

Use this file in three ways:

1. **Learn:** study one section at a time.
2. **Practice:** recreate each example without copying.
3. **Revise:** use the table of contents and quick-reference sections before interviews or project work.

The fastest path to mastering CSS is not memorizing every property. It is understanding the layout system, cascade, sizing behavior, responsive constraints, component patterns, and debugging process well enough to reason about unfamiliar designs.
