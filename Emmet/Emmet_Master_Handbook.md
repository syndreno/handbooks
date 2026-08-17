# Emmet Master Handbook
## The Essential Toolkit for Web Developers

> **Goal:** Learn Emmet from absolute beginner level to advanced day-to-day usage.
>
> **Audience:** Beginners, students, frontend developers, full-stack developers, UI developers, and anyone who frequently writes HTML, JSX, XML, CSS, SCSS, Less, or related markup/style languages.
>
> **Approach:** Every important topic is explained using:
>
> **What is it? → Why use it? → How does it work? → Syntax → Examples → Expected output → Real-world use → Common mistakes → Best practices → Advanced notes**
>
> **Last verified:** 17 August 2026  
> **Primary references:** Official Emmet documentation and current Visual Studio Code Emmet documentation.

---

## Table of Contents

1. [What Is Emmet?](#1-what-is-emmet)
2. [Why Developers Use Emmet](#2-why-developers-use-emmet)
3. [What Emmet Is Not](#3-what-emmet-is-not)
4. [How Emmet Works](#4-how-emmet-works)
5. [Getting Started](#5-getting-started)
6. [Your First Emmet Abbreviations](#6-your-first-emmet-abbreviations)
7. [Core HTML/Markup Syntax](#7-core-htmlmarkup-syntax)
8. [Elements and Custom Elements](#8-elements-and-custom-elements)
9. [Child Operator `>`](#9-child-operator-)
10. [Sibling Operator `+`](#10-sibling-operator-)
11. [Climb-Up Operator `^`](#11-climb-up-operator-)
12. [Multiplication Operator `*`](#12-multiplication-operator-)
13. [Grouping with Parentheses `()`](#13-grouping-with-parentheses-)
14. [IDs with `#`](#14-ids-with-)
15. [Classes with `.`](#15-classes-with-)
16. [Custom Attributes with `[]`](#16-custom-attributes-with-)
17. [Text with `{}`](#17-text-with-)
18. [Numbering with `$`](#18-numbering-with-)
19. [Changing Numbering Direction and Start](#19-changing-numbering-direction-and-start)
20. [Implicit Tag Names](#20-implicit-tag-names)
21. [Lorem Ipsum Generator](#21-lorem-ipsum-generator)
22. [Combining Operators Correctly](#22-combining-operators-correctly)
23. [HTML Boilerplate and Common Snippets](#23-html-boilerplate-and-common-snippets)
24. [Practical HTML Scenarios](#24-practical-html-scenarios)
25. [Forms with Emmet](#25-forms-with-emmet)
26. [Tables with Emmet](#26-tables-with-emmet)
27. [Navigation and Menu Patterns](#27-navigation-and-menu-patterns)
28. [Cards, Grids, and Repeated Components](#28-cards-grids-and-repeated-components)
29. [Semantic HTML with Emmet](#29-semantic-html-with-emmet)
30. [Emmet in JSX and React Workflows](#30-emmet-in-jsx-and-react-workflows)
31. [CSS Abbreviations](#31-css-abbreviations)
32. [CSS Values and Units](#32-css-values-and-units)
33. [Multiple CSS Values](#33-multiple-css-values)
34. [Negative CSS Values](#34-negative-css-values)
35. [Colors in CSS Abbreviations](#35-colors-in-css-abbreviations)
36. [Unitless CSS Properties](#36-unitless-css-properties)
37. [`!important` Modifier](#37-important-modifier)
38. [CSS Fuzzy Search](#38-css-fuzzy-search)
39. [Common CSS Emmet Abbreviations](#39-common-css-emmet-abbreviations)
40. [Flexbox with Emmet](#40-flexbox-with-emmet)
41. [CSS Grid with Emmet](#41-css-grid-with-emmet)
42. [Positioning and Sizing](#42-positioning-and-sizing)
43. [Typography](#43-typography)
44. [Backgrounds, Borders, and Effects](#44-backgrounds-borders-and-effects)
45. [Transitions and Transforms](#45-transitions-and-transforms)
46. [Gradients](#46-gradients)
47. [Vendor Prefix Features](#47-vendor-prefix-features)
48. [Emmet Actions](#48-emmet-actions)
49. [Expand Abbreviation](#49-expand-abbreviation)
50. [Wrap with Abbreviation](#50-wrap-with-abbreviation)
51. [Balance Outward and Inward](#51-balance-outward-and-inward)
52. [Go to Matching Pair](#52-go-to-matching-pair)
53. [Go to Edit Point](#53-go-to-edit-point)
54. [Select Item](#54-select-item)
55. [Toggle Comment](#55-toggle-comment)
56. [Split/Join Tag](#56-splitjoin-tag)
57. [Remove Tag](#57-remove-tag)
58. [Merge Lines](#58-merge-lines)
59. [Update Image Size](#59-update-image-size)
60. [Evaluate Math Expression](#60-evaluate-math-expression)
61. [Increment/Decrement Number](#61-incrementdecrement-number)
62. [Reflect CSS Value](#62-reflect-css-value)
63. [Encode/Decode Image as Data URL](#63-encodedecode-image-as-data-url)
64. [Filters](#64-filters)
65. [Comment Filter](#65-comment-filter)
66. [BEM Filter](#66-bem-filter)
67. [Trim Filter](#67-trim-filter)
68. [Escape Filter](#68-escape-filter)
69. [Custom Emmet Snippets](#69-custom-emmet-snippets)
70. [Tab Stops and Placeholders](#70-tab-stops-and-placeholders)
71. [Emmet Variables](#71-emmet-variables)
72. [VS Code Emmet Configuration](#72-vs-code-emmet-configuration)
73. [Enable Tab Expansion in VS Code](#73-enable-tab-expansion-in-vs-code)
74. [Enable Emmet in Other Languages](#74-enable-emmet-in-other-languages)
75. [Exclude Languages](#75-exclude-languages)
76. [Control Suggestions](#76-control-suggestions)
77. [Syntax Profiles](#77-syntax-profiles)
78. [Preferences](#78-preferences)
79. [Extensions Path and Custom Snippets](#79-extensions-path-and-custom-snippets)
80. [Multi-Cursor Workflows](#80-multi-cursor-workflows)
81. [Troubleshooting](#81-troubleshooting)
82. [Common Beginner Mistakes](#82-common-beginner-mistakes)
83. [Best Practices](#83-best-practices)
84. [When Not to Use Emmet](#84-when-not-to-use-emmet)
85. [Productivity Workflows](#85-productivity-workflows)
86. [Real-World Mini Projects](#86-real-world-mini-projects)
87. [Practice Exercises](#87-practice-exercises)
88. [Interview and Revision Questions](#88-interview-and-revision-questions)
89. [Quick Reference Cheat Sheet](#89-quick-reference-cheat-sheet)
90. [Learning Roadmap](#90-learning-roadmap)
91. [Official References](#91-official-references)

### Final material and appendices

- [Final Advice](#final-advice)
- [Appendix A — Scenario Drill Pack](#appendix-a--scenario-drill-pack)
- [Appendix B — Learn Emmet by Reading Trees](#appendix-b--learn-emmet-by-reading-trees)
- [Appendix C — Recommended Daily Practice](#appendix-c--recommended-daily-practice)
- [Appendix D — Personal Emmet Snippet Starter File for VS Code](#appendix-d--personal-emmet-snippet-starter-file-for-vs-code)
- [Appendix E — Emmet vs Editor Snippets](#appendix-e--emmet-vs-editor-snippets)
- [Appendix F — Emmet vs AI Code Completion](#appendix-f--emmet-vs-ai-code-completion)
- [Appendix G — Mastery Checklist](#appendix-g--mastery-checklist)

---

# 1. What Is Emmet?

**Emmet** is a productivity toolkit for writing HTML, XML-like markup, CSS, and related languages faster.

Instead of manually typing a large block such as:

```html
<ul class="menu">
    <li class="menu-item"><a href=""></a></li>
    <li class="menu-item"><a href=""></a></li>
    <li class="menu-item"><a href=""></a></li>
</ul>
```

you can type an abbreviation:

```text
ul.menu>li.menu-item*3>a
```

and expand it.

The editor generates the full structure for you.

The main idea is simple:

> **Describe the structure you want instead of manually typing every tag.**

Emmet abbreviations resemble CSS selectors, so developers who already know basic CSS syntax can learn Emmet quickly.

---

# 2. Why Developers Use Emmet

Emmet helps reduce repetitive typing.

It is especially useful when you repeatedly create:

- HTML page structures
- navigation menus
- lists
- forms
- tables
- cards
- grids
- repeated components
- semantic page layouts
- CSS properties
- Flexbox declarations
- CSS Grid declarations
- dimensions and spacing
- typography rules
- test content

For example, instead of typing:

```html
<div class="card">
    <h2 class="card-title">Product</h2>
    <p class="card-description">Description</p>
</div>
```

you can write:

```text
.card>h2.card-title{Product}+p.card-description{Description}
```

Emmet is not only about saving keystrokes. It can also help you think structurally.

---

# 3. What Emmet Is Not

Emmet is **not**:

- an HTML framework
- a CSS framework
- a JavaScript library
- a templating engine
- a compiler
- a replacement for understanding HTML or CSS
- a replacement for accessibility knowledge
- a replacement for semantic HTML
- a replacement for code review

Emmet can generate code quickly, but **you still need to understand the code it generates**.

For example:

```text
div>div>div>div
```

may be fast to create, but that does not mean deeply nested `<div>` elements are good HTML.

Use Emmet to write good code faster—not to generate unnecessary code faster.

---

# 4. How Emmet Works

Consider:

```text
nav>ul>li*3>a
```

Emmet roughly interprets the abbreviation as a tree:

```text
nav
└── ul
    ├── li
    │   └── a
    ├── li
    │   └── a
    └── li
        └── a
```

Then it renders the tree in the syntax appropriate for the current document.

In HTML:

```html
<nav>
    <ul>
        <li><a href=""></a></li>
        <li><a href=""></a></li>
        <li><a href=""></a></li>
    </ul>
</nav>
```

This tree-based mental model makes complicated abbreviations easier to understand.

## The most useful mental model

Treat a markup abbreviation as a compact description of a tree.

```text
parent
├── child
├── sibling
└── repeated child
```

The operators tell Emmet how to build that tree; the active editor language tells it how to render the tree.

This explains why the same idea may render differently in HTML, JSX, XML, or another supported syntax.

### Important parsing rule: spaces matter

In markup abbreviations, a normal space can terminate the abbreviation rather than meaning “descendant” as it does in a CSS selector.

Prefer:

```text
ul>li>a
```

rather than trying to write a CSS-selector-style descendant expression with spaces.

When an abbreviation unexpectedly stops expanding, accidental whitespace is one of the first things to check.


---

# 5. Getting Started

## 5.1 In Visual Studio Code

VS Code has built-in Emmet support. You normally do **not** need to install a separate Emmet extension.

Create an HTML file:

```text
index.html
```

Type:

```text
!
```

Then choose the Emmet suggestion or run **Emmet: Expand Abbreviation**.

A basic HTML document will be generated.

## 5.2 Expansion methods

Depending on your editor and configuration, you can expand using:

- the Emmet suggestion in autocomplete
- the editor's **Expand Abbreviation** command
- `Tab` if configured
- a custom keyboard shortcut

### VS Code

To allow Tab expansion:

```json
{
    "emmet.triggerExpansionOnTab": true
}
```

Do not assume that every editor uses the same shortcut.

---

# 6. Your First Emmet Abbreviations

## Example 1: A paragraph

Abbreviation:

```text
p
```

Typical HTML output:

```html
<p></p>
```

## Example 2: A heading

```text
h1
```

Output:

```html
<h1></h1>
```

## Example 3: A div with a class

```text
.container
```

Output in HTML:

```html
<div class="container"></div>
```

## Example 4: A div with an ID

```text
#app
```

Output:

```html
<div id="app"></div>
```

## Example 5: Nested elements

```text
ul>li
```

Output:

```html
<ul>
    <li></li>
</ul>
```

---

# 7. Core HTML/Markup Syntax

These operators form the foundation of Emmet markup abbreviations:

| Syntax | Meaning |
|---|---|
| `>` | child |
| `+` | sibling |
| `^` | climb up one level |
| `*` | repeat |
| `()` | group |
| `#` | ID |
| `.` | class |
| `[]` | attributes |
| `{}` | text |
| `$` | item number |
| `@` | numbering modifier |

Once you understand these operators, you can generate most common HTML structures.

## Read complex abbreviations in layers

Do not try to memorize a long abbreviation as one string.

For:

```text
section.cards>article.card*3>h2{Product $}+p.description
```

read it as:

1. create `section.cards`;
2. move inside it with `>`;
3. create three `article.card` elements with `*3`;
4. inside each article create an `h2`;
5. number the heading text with `$`;
6. add a sibling paragraph with `+`.

This “one operator at a time” method is more reliable than guessing from the final expansion.

### Common mistake

Emmet syntax resembles CSS selectors, but it is **not a CSS selector language**. Some characters look familiar while having Emmet-specific parsing behavior.


---

# 8. Elements and Custom Elements

Type an element name:

```text
section
```

Output:

```html
<section></section>
```

Emmet can also expand unknown/custom names as tags.

```text
my-widget
```

Possible output:

```html
<my-widget></my-widget>
```

This is useful for:

- Web Components
- framework-specific custom elements
- XML
- domain-specific markup

### Important

Emmet accepting a tag name does **not** mean that the tag is a valid standard HTML element.

## Emmet generates syntax; it does not validate semantics

If you type a known HTML element, Emmet can create the element quickly. If you type an unknown/custom tag, Emmet may still expand it.

That is useful for Web Components and XML-like languages, but it means **successful expansion is not proof that the resulting element is valid for your project**.

After expansion, rely on HTML/framework validation and your editor's language tooling for correctness.


---

# 9. Child Operator `>`

Use `>` when one element should be inside another.

```text
div>p
```

Output:

```html
<div>
    <p></p>
</div>
```

Another example:

```text
nav>ul>li>a
```

Output:

```html
<nav>
    <ul>
        <li><a href=""></a></li>
    </ul>
</nav>
```

## Real-world use

A card:

```text
article.card>header>h2
```

Output:

```html
<article class="card">
    <header>
        <h2></h2>
    </header>
</article>
```

### Mental model

Every `>` means:

> Move one level deeper.

## Common mistake

`>` changes hierarchy. Compare:

```text
ul>li>a
```

with:

```text
ul+li+a
```

The first builds a nested tree; the second builds siblings.

When output is nested incorrectly, read every `>` as “go inside the element on the left.”


---

# 10. Sibling Operator `+`

Use `+` when elements should be at the same level.

```text
h1+p
```

Output:

```html
<h1></h1>
<p></p>
```

Example:

```text
header+main+footer
```

Output:

```html
<header></header>
<main></main>
<footer></footer>
```

## Real-world use

Article header:

```text
h1.title+p.subtitle+p.meta
```

## Real-world use

Siblings are common in component skeletons:

```text
header+main+footer
```

Use `+` when elements share the same parent.

If a later element should leave a deeply nested branch and become a sibling of an ancestor, use the climb-up operator `^` or grouping instead of stacking `+` operators blindly.


---

# 11. Climb-Up Operator `^`

The `^` operator moves back up the generated tree.

Consider:

```text
div>section>p^footer
```

The `footer` should not be inside `section`.

Output:

```html
<div>
    <section>
        <p></p>
    </section>
    <footer></footer>
</div>
```

## Multiple climb-ups

```text
main>section>article>p^^footer
```

Each `^` climbs one level.

### Beginner tip

If `^` becomes difficult to reason about, use grouping with parentheses instead.

Often this:

```text
main>(section>article>p)+footer
```

is easier to understand.

## Why `^` exists

After `>` moves you deeper into a tree, `^` moves the insertion point back toward an ancestor.

Think:

```text
>  go down
^  go up
+  stay at current level and add sibling
```

For complicated structures, parentheses are often easier to read than several consecutive `^` operators.


---

# 12. Multiplication Operator `*`

Use `*` to repeat an element or group.

```text
li*5
```

Output:

```html
<li></li>
<li></li>
<li></li>
<li></li>
<li></li>
```

Nested example:

```text
ul>li*4
```

Output:

```html
<ul>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
</ul>
```

## Real-world use

Generate six cards:

```text
.cards>.card*6
```

Output:

```html
<div class="cards">
    <div class="card"></div>
    <div class="card"></div>
    <div class="card"></div>
    <div class="card"></div>
    <div class="card"></div>
    <div class="card"></div>
</div>
```

## Repeat structure, not meaningful data

`*` is excellent for scaffolding:

```text
li.item*5
```

But repeated placeholder markup is not a substitute for rendering real application data with a loop/component.

Use multiplication while authoring static structure; use your programming language/framework when repetition depends on runtime data.


---

# 13. Grouping with Parentheses `()`

Grouping lets you treat multiple elements as one logical block.

```text
div>(header>h1)+main+footer
```

Output:

```html
<div>
    <header>
        <h1></h1>
    </header>
    <main></main>
    <footer></footer>
</div>
```

Another example:

```text
(section>h2+p)*3
```

Output:

```html
<section>
    <h2></h2>
    <p></p>
</section>
<section>
    <h2></h2>
    <p></p>
</section>
<section>
    <h2></h2>
    <p></p>
</section>
```

## When grouping is useful

Use parentheses when:

- repeating a complete component
- controlling operator precedence
- making sibling/child relationships clearer

## Best practice

Avoid extremely long one-line abbreviations.

This is possible:

```text
div#app>(header.site-header>nav>ul>li*5>a)+(main>section*4>h2+p*2)+footer
```

but several shorter expansions may be easier to maintain and less error-prone.

## Group when precedence becomes hard to see

Parentheses make the intended subtree explicit.

```text
(header>nav)+(main>section)+footer
```

is easier to reason about than a long expression that relies on repeated climb-up operators.

Use grouping for readability, not merely because the syntax allows it.


---

# 14. IDs with `#`

Use `#` for an ID.

```text
div#app
```

Output:

```html
<div id="app"></div>
```

Because `div` is commonly implied:

```text
#app
```

also typically produces:

```html
<div id="app"></div>
```

Example:

```text
main#content
```

Output:

```html
<main id="content"></main>
```

## When to use an ID

Emmet makes IDs fast to type, but HTML rules still apply.

```text
main#app
```

can expand to:

```html
<main id="app"></main>
```

Do not repeat the same ID simply because multiplication makes it easy:

```text
div#item*3
```

would create invalid duplicate IDs in normal HTML. If repeated elements need identifiers, combine numbering:

```text
div#item-$*3
```

Typical output:

```html
<div id="item-1"></div>
<div id="item-2"></div>
<div id="item-3"></div>
```


---

# 15. Classes with `.`

Use `.` for a class.

```text
div.card
```

Output:

```html
<div class="card"></div>
```

Multiple classes:

```text
div.card.featured.active
```

Output:

```html
<div class="card featured active"></div>
```

Implicit div:

```text
.card
```

Output:

```html
<div class="card"></div>
```

## BEM-style classes

```text
article.product-card>h2.product-card__title
```

Output:

```html
<article class="product-card">
    <h2 class="product-card__title"></h2>
</article>
```

## Multiple classes

You can chain class shorthand:

```text
button.btn.btn-primary
```

Typical output:

```html
<button class="btn btn-primary"></button>
```

Emmet saves typing but does not know whether those class names exist in your CSS framework. A successful expansion can still reference a nonexistent class.


---

# 16. Custom Attributes with `[]`

Use square brackets to add attributes.

```text
input[type=text]
```

Typical output:

```html
<input type="text">
```

Multiple attributes:

```text
input[type=email name=email required]
```

Output:

```html
<input type="email" name="email" required>
```

Attribute values containing spaces should be quoted:

```text
button[type=button aria-label="Open menu"]
```

Output:

```html
<button type="button" aria-label="Open menu"></button>
```

## Data attributes

```text
div[data-id=42 data-role=card]
```

Output:

```html
<div data-id="42" data-role="card"></div>
```

## ARIA attributes

```text
button[aria-expanded=false aria-controls=menu]
```

Output:

```html
<button aria-expanded="false" aria-controls="menu"></button>
```

### Best practice

Emmet can generate accessibility attributes quickly, but it cannot decide whether your ARIA usage is semantically correct.

## Quote values when the value needs it

Attributes are useful for forms, ARIA metadata, data attributes, and framework-specific markup.

Keep accessibility semantics in mind: Emmet can create `aria-*` attributes quickly, but it cannot decide whether the role/value is correct.

For complex values containing spaces or special characters, preview the generated markup and verify quoting.


---

# 17. Text with `{}`

Use `{}` to place text inside an element.

```text
button{Save}
```

Output:

```html
<button>Save</button>
```

Example:

```text
h1{Welcome to My Website}
```

Output:

```html
<h1>Welcome to My Website</h1>
```

Mix text and elements:

```text
p>{Read our }+a[href=/terms]{terms}+{ before continuing.}
```

Output:

```html
<p>Read our <a href="/terms">terms</a> before continuing.</p>
```

## Why `>` appears before text in this example

Text blocks can affect the current tree context. When mixing multiple pieces of text and elements, explicit grouping or child operators make intent clearer.

## Text is literal scaffolding

Text insertion is useful for prototypes:

```text
button{Save}
```

But do not hard-code user-facing content through Emmet when the real application uses localization, dynamic data, or framework bindings.

Use `{}` to generate the initial source structure, then replace it with the appropriate application content mechanism.


---

# 18. Numbering with `$`

`$` inserts the current repetition number.

```text
ul>li.item$*4
```

Output:

```html
<ul>
    <li class="item1"></li>
    <li class="item2"></li>
    <li class="item3"></li>
    <li class="item4"></li>
</ul>
```

Number text:

```text
ol>li{Step $}*5
```

Output:

```html
<ol>
    <li>Step 1</li>
    <li>Step 2</li>
    <li>Step 3</li>
    <li>Step 4</li>
    <li>Step 5</li>
</ol>
```

Number IDs:

```text
section#section$*3
```

## Zero padding

Use multiple dollar signs.

```text
li.item$$*3
```

Result:

```html
<li class="item01"></li>
<li class="item02"></li>
<li class="item03"></li>
```

Three digits:

```text
li.item$$$*3
```

becomes roughly:

```html
<li class="item001"></li>
<li class="item002"></li>
<li class="item003"></li>
```

## Numbering is evaluated inside repetition

`$` is most useful with `*`.

```text
li.item-$*3
```

Typical output:

```html
<li class="item-1"></li>
<li class="item-2"></li>
<li class="item-3"></li>
```

Use multiple `$` characters when you need zero-padded numbers:

```text
li.item-$$*3
```

Typical output:

```html
<li class="item-01"></li>
<li class="item-02"></li>
<li class="item-03"></li>
```

Numbering is a code-generation convenience; it does not create application state or data IDs at runtime.


---

# 19. Changing Numbering Direction and Start

## Start from another number

```text
li.item$@5*3
```

Numbers begin from 5:

```html
<li class="item5"></li>
<li class="item6"></li>
<li class="item7"></li>
```

## Descending numbering

```text
li.item$@-*4
```

Output numbering:

```text
item4
item3
item2
item1
```

## Descending with a custom base

```text
li.item$@-3*5
```

This uses reverse numbering with a base modifier.

### Useful scenarios

- rank lists
- generated step identifiers
- repeated IDs during mockups
- numbered demo cards
- numbered CSS utility examples

## Use numbering modifiers with a clear sequence

Numbering modifiers are most useful for generated demo structures, ordered IDs/classes, or reverse sequences.

Before relying on a clever modifier, expand a three-item sample and verify the first and last values. A short preview is faster than debugging a large incorrectly numbered block.


---

# 20. Implicit Tag Names

Sometimes you can omit the element name and write only the class.

```text
.wrapper
```

In a normal HTML context this usually becomes:

```html
<div class="wrapper"></div>
```

But Emmet can infer other elements from the parent context.

## List context

Inside `ul` or `ol`, an unnamed repeated element is inferred as `li`.

```text
ul>.item*3
```

Equivalent idea:

```text
ul>li.item*3
```

## Table context

Inside table-related parents, Emmet can infer table elements.

Examples include contextual inference such as:

- `li` inside `ul`/`ol`
- `tr` inside table sections
- `td` inside `tr`
- `option` inside `select`

## Why implicit names matter

They make abbreviations shorter.

However, when teaching beginners or writing a complex abbreviation, explicit element names may be clearer.

## Implicit tags depend on context

An abbreviation such as:

```text
ul>.item
```

can infer an appropriate child element from the parent context.

This saves typing, but explicit tag names are sometimes clearer for learners and code review.

Use implicit tags when the context is obvious; use explicit tags when ambiguity would make the abbreviation harder to understand.


---

# 21. Lorem Ipsum Generator

Emmet includes a Lorem Ipsum generator.

```text
lorem
```

generates placeholder text.

Control approximate word count:

```text
lorem10
```

Use it inside an element:

```text
p>lorem20
```

Repeat it:

```text
article*3>h2{Article $}+p>lorem25
```

## Real-world use

Useful when testing:

- card heights
- text wrapping
- responsive layouts
- typography
- overflow behavior
- line clamping
- content-heavy UI

## Warning

Lorem Ipsum is good for layout testing, but realistic test data is often better for validating real user interfaces.

## Use placeholder text responsibly

Lorem text is useful for testing:

- wrapping;
- card heights;
- typography;
- overflow;
- responsive layouts.

It is not realistic content. Before shipping a design, test with:

- very short text;
- very long text;
- long unbroken words/URLs;
- translated text;
- real headings and labels.

A layout that works only with Lorem Ipsum is not fully tested.


---

# 22. Combining Operators Correctly

The biggest jump in Emmet skill comes from combining operators.

Suppose you want:

```html
<section class="products">
    <article class="product">
        <h2>Product 1</h2>
        <p></p>
    </article>
    <article class="product">
        <h2>Product 2</h2>
        <p></p>
    </article>
    <article class="product">
        <h2>Product 3</h2>
        <p></p>
    </article>
</section>
```

Abbreviation:

```text
section.products>article.product*3>h2{Product $}+p
```

Breakdown:

```text
section.products
```

Create the parent.

```text
>
```

Enter the section.

```text
article.product*3
```

Create three articles.

```text
>
```

Put child elements inside each article.

```text
h2{Product $}+p
```

Create a heading and sibling paragraph.

## Debugging complex abbreviations

If an abbreviation expands incorrectly:

1. Expand only the first part.
2. Verify the tree.
3. Add one operator at a time.
4. Use parentheses when structure becomes ambiguous.
5. Prefer several simple expansions over one giant abbreviation.

## Debug a long abbreviation by reducing it

If this is confusing:

```text
main>section.products>(article.card>h2{Item $}+p)*3+aside
```

do not keep adding characters. Reduce it:

```text
main
main>section.products
main>section.products>article.card
main>section.products>article.card*3
```

Then add grouping and siblings back one step at a time.

This is the Emmet equivalent of debugging a program with a minimal reproducible example.

### Prefer readable abbreviations

The official Emmet syntax can express very large trees, but very long abbreviations are harder to review than the HTML they replace. For reusable complex structures, a custom snippet or framework component is often clearer.


---

# 23. HTML Boilerplate and Common Snippets

Emmet contains predefined snippets in addition to dynamically parsed abbreviations.

## HTML5 document

```text
!
```

or commonly:

```text
html:5
```

generates an HTML5 document skeleton.

A typical result includes:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>

</body>
</html>
```

Exact output can vary by editor integration and Emmet version/configuration.

## Common snippet families

You may encounter abbreviations such as:

```text
a
a:link
a:mail
link
link:css
script
script:src
meta
meta:vp
input
input:text
input:email
input:password
```

Because predefined snippets can evolve, use your editor's Emmet suggestion preview and the official cheat sheet to confirm exact output.

## Boilerplate is a starting point

The `!` abbreviation is useful for creating a basic HTML document quickly.

After expansion, review the generated document for project-specific needs such as:

- page title;
- language;
- viewport behavior;
- stylesheet/script loading;
- metadata;
- accessibility;
- framework entry points.

Do not treat generated boilerplate as a complete production page.


---

# 24. Practical HTML Scenarios

## 24.1 Basic page shell

```text
header.site-header+main#main+footer.site-footer
```

## 24.2 Article

```text
article.post>header>h1.post-title+p.post-meta^section.post-content>p*3
```

A clearer grouped version:

```text
article.post>(header>h1.post-title+p.post-meta)+(section.post-content>p*3)
```

## 24.3 Dashboard shell

```text
.app>aside.sidebar+main.main-content
```

## 24.4 Two-column layout

```text
.container>main.content+aside.sidebar
```

## 24.5 Hero section

```text
section.hero>.hero-content>h1{Build Faster}+p{A practical web development workflow}+a.btn[href=#start]{Get Started}
```

## 24.6 FAQ

```text
section.faq>article.faq-item*5>h3{Question $}+p>lorem15
```

## 24.7 Pricing plans

```text
section.pricing>.plan*3>h2{Plan $}+p.price{₹$}+ul>li*4{Feature $}
```

Note: `$` is a numbering token. If you need a literal dollar symbol, editor behavior and escaping can matter; review the preview before expansion.

## Translate the layout into a tree first

Before writing an abbreviation, describe the desired structure:

```text
page
├── header
├── main
│   ├── section
│   └── aside
└── footer
```

Then convert relationships into `>`, `+`, grouping, and repetition.

This is easier than starting with punctuation and hoping the expansion resembles the design.


---

# 25. Forms with Emmet

Forms contain many repetitive attributes, making them excellent Emmet candidates.

## 25.1 Basic login form

```text
form.login-form>label[for=email]{Email}+input#email[type=email name=email required]+label[for=password]{Password}+input#password[type=password name=password required]+button[type=submit]{Login}
```

Possible output:

```html
<form class="login-form">
    <label for="email">Email</label>
    <input type="email" id="email" name="email" required>
    <label for="password">Password</label>
    <input type="password" id="password" name="password" required>
    <button type="submit">Login</button>
</form>
```

## 25.2 Search form

```text
form.search[role=search]>input[type=search name=q aria-label="Search"]+button[type=submit]{Search}
```

## 25.3 Field wrapper pattern

```text
.form-group>label[for=name]{Name}+input#name[type=text name=name]
```

## 25.4 Repeated field structure

```text
form>.field*3>label+input
```

Then fill names manually.

### Best practice

Emmet helps create the structure, but you should still review:

- correct `label` associations
- input types
- `name` attributes
- validation rules
- autocomplete attributes
- accessibility
- server-side validation

## Fast form markup still needs form semantics

After expanding a form, check:

- each control has an appropriate label;
- `for` and `id` relationships match;
- `name` values are present when submission requires them;
- correct input types are used;
- required/optional behavior is intentional;
- validation messages are accessible.

Emmet accelerates typing; it does not design the form contract.


---

# 26. Tables with Emmet

## Basic table

```text
table>thead>tr>th*3^^tbody>tr*4>td*3
```

Grouping is often easier:

```text
table>(thead>tr>th*3)+(tbody>tr*4>td*3)
```

## With headings

```text
table>(thead>tr>th{Column $}*3)+(tbody>tr*5>td{Data $}*3)
```

## Accessible table starter

```text
table>caption{Sales Report}+(thead>tr>th[scope=col]*4)+(tbody>tr*5>td*4)
```

### Reminder

Generated structure does not guarantee accessible table semantics. Use `scope`, captions, headers, and table structure appropriately for the data.

## Use tables only for tabular data

Emmet can generate table rows and cells quickly, but HTML tables should represent data with row/column relationships.

For real tables, review:

- headings (`th`);
- scope/association where appropriate;
- captions when needed;
- responsive behavior;
- empty states.

Do not use a table simply as a page-layout grid.


---

# 27. Navigation and Menu Patterns

## Simple navigation

```text
nav>ul>li*4>a[href=#]{Menu $}
```

## Navigation with class naming

```text
nav.main-nav>ul.main-nav__list>li.main-nav__item*4>a.main-nav__link[href=#]{Menu $}
```

## Nested menu

```text
nav>ul>li*3>a{Item $}+ul>li*2>a{Subitem $}
```

Be careful: complex nested numbering can produce repeated numbering patterns. Preview the output.

## Breadcrumb

```text
nav[aria-label=Breadcrumb]>ol.breadcrumb>li.breadcrumb__item*4>a[href=#]{Level $}
```

## Structure is only the first layer

A quick abbreviation can build a navigation list, but production navigation also needs:

- meaningful link text;
- valid destinations;
- current-page state where appropriate;
- keyboard usability;
- responsive behavior.

Emmet generates the skeleton; navigation behavior and accessibility still belong to your application.


---

# 28. Cards, Grids, and Repeated Components

## Product cards

```text
.products>article.product-card*4>img.product-card__image[src="product$.jpg" alt="Product $"]+h2.product-card__title{Product $}+p.product-card__price{Price}+button[type=button]{Add to cart}
```

## Blog cards

```text
.blog-grid>article.post-card*6>h2{Post $}+p>lorem15+a[href=#]{Read more}
```

## Team members

```text
.team>.member*4>img[src="member$.jpg" alt="Team member $"]+h3{Member $}+p.role{Role}
```

### Why Emmet shines here

Repeated UI skeletons are one of Emmet's strongest use cases because `*` and `$` eliminate repetitive structure typing.

## Prefer components for repeated application UI

Emmet repetition is ideal for static mockups:

```text
article.card*3
```

In React, Vue, Angular, server templates, or another dynamic system, real cards are normally produced from data/components rather than permanently copied markup.

Use Emmet to prototype the structure, then move repetition into the framework when data drives the UI.


---

# 29. Semantic HTML with Emmet

Prefer semantic elements when they represent the content correctly.

Instead of:

```text
div.header+div.main+div.footer
```

consider:

```text
header+main+footer
```

Instead of:

```text
div.article
```

consider:

```text
article
```

Possible semantic elements include:

```text
header
nav
main
section
article
aside
footer
figure
figcaption
details
summary
time
address
```

### Rule

Emmet makes both semantic and non-semantic HTML equally easy. The developer must choose the right element.

## Semantic names should come before speed

Prefer an abbreviation that reflects meaning:

```text
main>article>header+h2
```

over a generic structure such as:

```text
div>div>div
```

when the semantic elements match the content.

Emmet is most valuable when it makes **good HTML** faster.


---

# 30. Emmet in JSX and React Workflows

VS Code supports Emmet in JSX syntax.

A common abbreviation:

```text
div.card>h2.title{Hello}+p.description{Welcome}
```

In JSX-oriented output, Emmet can apply JSX-aware transformations such as using `className` instead of HTML's `class`.

Typical JSX-style result:

```jsx
<div className="card">
    <h2 className="title">Hello</h2>
    <p className="description">Welcome</p>
</div>
```

## Enabling Emmet in JavaScript files in VS Code

If you write JSX inside `.js` files, you can map JavaScript to `javascriptreact`:

```json
{
    "emmet.includeLanguages": {
        "javascript": "javascriptreact"
    }
}
```

### Important warning

Enabling Emmet in a broader language can cause suggestions to appear in places where you do not want them. Use the mapping only when it fits your workflow.

## React component example

Inside a component return block:

```text
section.dashboard>h1{Dashboard}+.stats>.stat*3>h2{Stat $}+p{Value}
```

### JSX review checklist

After expansion, check:

- `className`
- self-closing component/tag syntax
- event handler syntax
- expressions in `{...}`
- framework-specific attributes
- component capitalization

Emmet is a structure generator, not a React correctness checker.

## JSX is not HTML

After expansion, review JSX-specific output carefully. Framework syntax may require differences such as:

- `className` instead of `class`;
- JSX-compatible self-closing tags;
- JavaScript expressions inside `{}`;
- component names beginning with an uppercase letter.

Editor integrations can adapt Emmet output to JSX, but Emmet does not understand your component's props, state, accessibility requirements, or business rules.

### VS Code language mapping

When Emmet is not active in a JavaScript language mode, `emmet.includeLanguages` can map that language to an Emmet syntax. For example:

```json
{
  "emmet.includeLanguages": {
    "javascript": "javascriptreact"
  }
}
```

Use mappings narrowly. Enabling HTML-like expansion in every JavaScript context can create noisy or irrelevant suggestions.


---

# 31. CSS Abbreviations

Emmet also expands CSS abbreviations.

Example:

```text
m10
```

Output:

```css
margin: 10px;
```

Example:

```text
p20
```

Output:

```css
padding: 20px;
```

Example:

```text
w100
```

Output:

```css
width: 100px;
```

The exact abbreviation system combines:

1. a CSS property abbreviation
2. optional value information

## How a CSS abbreviation is interpreted

A CSS abbreviation normally combines:

```text
[property shorthand] + [value information]
```

Example:

```text
m10
```

can be read as:

```text
m   → margin
10  → 10 with the default length unit for this context
```

and expands to:

```css
margin: 10px;
```

This is why learning a small set of property abbreviations first is more useful than memorizing hundreds of complete strings.

### Use suggestion preview as documentation

Emmet supports fuzzy matching for CSS abbreviations. If you only partly remember an abbreviation, use the editor's suggestion list and preview instead of guessing and accepting an incorrect property.


---

# 32. CSS Values and Units

## Integer values

Commonly:

```text
m10
```

becomes:

```css
margin: 10px;
```

## Floating-point values

Emmet's default float unit may be `em` depending on configuration.

Example:

```text
m1.5
```

can produce:

```css
margin: 1.5em;
```

Because implicit units can surprise developers, many teams prefer writing the unit explicitly in less-obvious cases.

## Explicit units

```text
m2rem
```

```css
margin: 2rem;
```

```text
w50vw
```

```css
width: 50vw;
```

```text
h100vh
```

```css
height: 100vh;
```

## Defaults are conveniences, not CSS rules

Emmet may add a unit for numeric values according to its abbreviation rules.

For example:

```text
m10
```

commonly becomes:

```css
margin: 10px;
```

But CSS itself—not Emmet—decides which units are valid for a property.

When a unit matters explicitly, include it in the abbreviation using the syntax supported by Emmet and preview the expansion before accepting it.

### Real-world caution

A fast expansion such as `w100` can be syntactically valid and still be the wrong design choice. Responsive layouts often need percentages, `rem`, viewport units, `min()`, `max()`, `clamp()`, flex sizing, or grid tracks instead of fixed pixels.


---

# 33. Multiple CSS Values

Use hyphen-separated values for many CSS abbreviations.

```text
m10-20
```

Output:

```css
margin: 10px 20px;
```

Four values:

```text
m10-20-30-40
```

Typical output:

```css
margin: 10px 20px 30px 40px;
```

Padding:

```text
p8-16
```

Output:

```css
padding: 8px 16px;
```

## Read hyphens as value separators in CSS abbreviations

A multi-value abbreviation can compactly express properties such as margin/padding.

Always preview the expansion when negative numbers or units are involved because punctuation can affect parsing.

The generated declaration must still follow normal CSS value order and property rules.


---

# 34. Negative CSS Values

Negative values require careful use of separators.

Example concept:

```text
m-10
```

means a negative margin.

For multiple negative values, Emmet's syntax distinguishes separators from negative signs.

Always preview unfamiliar abbreviations before committing them.

### Real-world examples

```text
mt-10
```

Potential output:

```css
margin-top: -10px;
```

Useful for:

- offsetting decorative elements
- controlled overlap
- transforms and positioning

But avoid negative spacing merely to "fix" a layout that should be redesigned.

## Make the sign unambiguous

Negative values are useful for properties that permit them, but not every CSS property accepts a negative value.

Emmet can help type the declaration; CSS validation determines whether the result is legal and sensible.

After expansion, confirm both the sign and unit.


---

# 35. Colors in CSS Abbreviations

Emmet understands compact hexadecimal color input.

Example:

```text
c#3
```

can produce:

```css
color: #333;
```

Example:

```text
bgc#fff
```

can produce:

```css
background-color: #fff;
```

A short value may be expanded/normalized according to Emmet preferences.

## Practical examples

```text
c#222
```

```css
color: #222;
```

```text
bd1#ddd
```

may resolve into a border declaration depending on the recognized abbreviation.

### Tip

When a CSS abbreviation becomes cryptic, use the editor preview.

Clarity beats saving two characters.

## Color shorthand is authoring convenience

Emmet can accelerate common color declarations, but your project may prefer:

- CSS custom properties;
- design tokens;
- theme variables;
- utility classes.

If the same literal color appears repeatedly, a reusable design token is usually more maintainable than repeatedly expanding a raw hex value.


---

# 36. Unitless CSS Properties

Some CSS properties naturally use unitless numeric values.

Examples include common cases such as:

```css
line-height: 1.5;
font-weight: 600;
z-index: 10;
opacity: 0.8;
```

Emmet's stylesheet resolver understands a set of unitless properties and does not automatically add `px` to them.

Examples:

```text
lh1.5
```

```text
fw600
```

```text
z10
```

Do not depend on memory alone; inspect the expansion if you are unsure.

## Unitless does not mean “any property can omit units”

Some CSS properties accept unitless numbers, while length properties generally need units except where CSS specifically allows zero without one.

Emmet knows common patterns, but always think in terms of the CSS property being generated.

For example:

```css
line-height: 1.5;
z-index: 10;
opacity: 0.8;
```

are naturally unitless, while:

```css
margin: 10px;
```

is a length.

If an expansion surprises you, check the resulting CSS rather than assuming the abbreviation is wrong or that CSS accepts the value.


---

# 37. `!important` Modifier

A trailing `!` can add `!important` to a CSS expansion.

Example concept:

```text
m10!
```

Typical result:

```css
margin: 10px !important;
```

## When to use it

Rarely.

`!important` can be useful for:

- constrained overrides
- third-party styles
- narrowly scoped utility behavior

But frequent use often signals specificity problems.

Emmet makes `!important` easy to type; that does not make it a good default.

## `!important` is not a conflict-resolution strategy

Emmet can append `!important` quickly, but CSS cascade problems should normally be solved by understanding specificity, source order, layers, and component architecture.

Use `!important` only when the project's CSS strategy intentionally calls for it.


---

# 38. CSS Fuzzy Search

You do not always need to remember an exact CSS abbreviation.

Emmet uses fuzzy matching for many stylesheet abbreviations.

For example, variations of an overflow-hidden abbreviation may still resolve correctly.

This helps because the official CSS abbreviation list is large.

## Why this matters

Instead of memorizing hundreds of abbreviations, you can:

1. type a logical short form
2. inspect the preview
3. accept it if correct

## Warning

Fuzzy matching can occasionally select something other than what you intended.

Always check the suggestion preview for unfamiliar abbreviations.

## Fuzzy search is a discovery tool

You do not need perfect memorization to benefit from Emmet. In supported editors, start typing the part of a property you remember and inspect the suggested expansion.

Use fuzzy search when:

- you remember the concept but not the shorthand;
- several properties have similar names;
- you are learning a new CSS area.

Do not accept a fuzzy suggestion solely because it is first in the list. Read the generated property and value.


---

# 39. Common CSS Emmet Abbreviations

The following are useful patterns. Exact resolution can depend on the current Emmet version and editor integration, so preview when uncertain.

| Abbreviation | Typical meaning |
|---|---|
| `m` | margin |
| `mt` | margin-top |
| `mr` | margin-right |
| `mb` | margin-bottom |
| `ml` | margin-left |
| `p` | padding |
| `pt` | padding-top |
| `pr` | padding-right |
| `pb` | padding-bottom |
| `pl` | padding-left |
| `w` | width |
| `h` | height |
| `maw` | max-width |
| `mih` | min-height |
| `d` | display |
| `db` | display: block |
| `dib` | display: inline-block |
| `dn` | display: none |
| `pos` | position |
| `posa` / `pos:a` | absolute positioning |
| `posr` / `pos:r` | relative positioning |
| `t` | top |
| `r` | right |
| `b` | bottom |
| `l` | left |
| `z` | z-index |
| `c` | color |
| `bg` | background |
| `bgc` | background-color |
| `bd` | border |
| `bdrs` | border-radius |
| `fz` | font-size |
| `fw` | font-weight |
| `lh` | line-height |
| `ta` | text-align |
| `td` | text-decoration |
| `ov` | overflow |
| `op` | opacity |
| `cur` | cursor |

---

# 40. Flexbox with Emmet

Modern layout work frequently uses Flexbox.

Typical useful abbreviations include forms such as:

```text
df
```

Typical expansion:

```css
display: flex;
```

Other common patterns may include abbreviations for:

```css
flex-direction
flex-wrap
justify-content
align-items
align-content
gap
flex
flex-grow
flex-shrink
order
```

## Common workflow

Instead of trying to memorize every possible shorthand immediately:

1. start with `d:f` or the editor's `df` suggestion
2. use autocomplete for `justify-content`
3. inspect Emmet suggestions
4. gradually learn the abbreviations you use most often

## Example layout

Desired CSS:

```css
.toolbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 1rem;
}
```

A productive Emmet-assisted workflow might use separate expansions for each property rather than one obscure combined expression.

### Best practice

Optimize for fast **correct** code, not maximum abbreviation density.

## Expand, then reason about the layout

Flexbox abbreviations save typing for declarations such as display, direction, alignment, and gaps.

But layout behavior depends on both parent and child properties. When a flex layout does not work, inspect:

- which element is the flex container;
- main vs cross axis;
- wrapping;
- child basis/grow/shrink;
- available width/height.

Emmet cannot infer those design decisions.


---

# 41. CSS Grid with Emmet

Grid properties are also candidates for Emmet expansion and fuzzy search.

Common concepts:

```css
display: grid;
grid-template-columns
grid-template-rows
grid-column
grid-row
gap
place-items
justify-items
align-items
```

For example, typing a logical abbreviation and checking the suggestion list can be faster than memorizing every exact Grid shorthand.

## Real-world example

```css
.cards {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1.5rem;
}
```

Use Emmet for the straightforward properties, then write complex function values such as `repeat()` clearly if that is easier to read.

## Grid syntax can outgrow tiny abbreviations

Emmet is useful for common grid declarations, but complex track definitions often become clearer when written directly.

Use Emmet for repetitive property names and simple values; use normal CSS when `repeat()`, `minmax()`, named lines/areas, or responsive calculations are easier to read explicitly.


---

# 42. Positioning and Sizing

Useful Emmet-style patterns:

```text
posa
```

→ absolute positioning.

```text
posr
```

→ relative positioning.

```text
t0
r0
b0
l0
```

→ directional offsets.

Example desired result:

```css
.badge {
    position: absolute;
    top: 0;
    right: 0;
}
```

Possible workflow:

```text
posa
t0
r0
```

Sizing examples:

```text
w100
h50
maw1200
mih100vh
```

Remember that implicit units may be added.

---

# 43. Typography

Frequently useful properties include:

```text
fz16
fw700
lh1.5
ta:c
td:n
```

Typical meanings:

```css
font-size: 16px;
font-weight: 700;
line-height: 1.5;
text-align: center;
text-decoration: none;
```

Other useful typography concepts:

- font-family
- font-style
- text-transform
- letter-spacing
- word-spacing
- white-space
- text-overflow

Use fuzzy search rather than forcing yourself to memorize every abbreviation.

---

# 44. Backgrounds, Borders, and Effects

Useful targets include:

```css
background
background-color
background-image
background-position
border
border-width
border-style
border-color
border-radius
box-shadow
opacity
```

Examples:

```text
bgc#fff
```

```text
bdrs8
```

```text
op.5
```

Inspect the generated units and values.

## Example card

```css
.card {
    background-color: #fff;
    border-radius: 8px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, .1);
}
```

Emmet is particularly useful for the simple properties. Complex shadow syntax is often clearer when written normally or inserted from a custom snippet.

---

# 45. Transitions and Transforms

Emmet can help discover and expand properties related to:

```css
transition
transition-property
transition-duration
transform
transform-origin
```

VS Code's current Emmet documentation gives examples of fuzzy property/value usage such as transform-related abbreviations.

## Practical advice

Use Emmet to reach the property quickly, then edit the value.

For example:

```css
transform: rotate(10deg);
```

or:

```css
transition: opacity 200ms ease;
```

Trying to encode every complex value into the shortest possible abbreviation is not always faster.

---

# 46. Gradients

Emmet supports gradient-related expansion.

A common concept is:

```text
lg(...)
```

for a linear-gradient expression.

Example:

```text
lg(90deg,#111,#555)
```

The resulting output may be transformed into an appropriate CSS gradient representation according to the current Emmet implementation.

## Real-world use

```css
.hero {
    background: linear-gradient(90deg, #111, #555);
}
```

## Important modern-development note

Older Emmet documentation discusses generating multiple legacy vendor-prefixed gradient forms. Modern browser support and build pipelines have changed significantly.

Today, always review whether extra prefixes are actually required for your browser support policy. Tools such as Autoprefixer are commonly a better place to handle compatibility systematically.

---

# 47. Vendor Prefix Features

Historically, Emmet included features for generating and reflecting vendor-prefixed properties.

Modern development commonly relies on:

- standards-based properties
- browserslist configuration
- Autoprefixer/PostCSS
- framework/build-tool prefix handling

Use Emmet's prefix-oriented actions only when they fit your actual project requirements.

Do not add prefixes simply because an editor can generate them.

## Why build tooling is usually better for production prefixes

A manually generated prefix becomes static source code. A build tool such as Autoprefixer can instead derive needed prefixes from the project's browser-support targets.

That makes maintenance easier when supported browsers change.

Use an Emmet prefix/reflection action mainly for:

- inspecting or editing existing prefixed code;
- a codebase that intentionally manages prefixes manually;
- a quick local transformation.

Do not use it as a substitute for a defined browser-support policy.


---

# 48. Emmet Actions

Emmet is more than abbreviation expansion.

The official action set includes capabilities such as:

- Expand Abbreviation
- Balance
- Go to Matching Pair
- Wrap with Abbreviation
- Go to Edit Point
- Select Item
- Toggle Comment
- Split/Join Tag
- Remove Tag
- Merge Lines
- Update Image Size
- Evaluate Math Expression
- Increment/Decrement Number
- Reflect CSS Value
- Encode/Decode Image to data URL

Availability and keyboard shortcuts vary by editor.

## Actions operate on editor context

Unlike a simple abbreviation, many Emmet actions use the current:

- caret position;
- selection;
- tag pair;
- CSS declaration;
- numeric literal;
- image reference.

Conceptually:

```text
editor context
     +
Emmet action
     ↓
transformed source
```

This means the same action may do nothing when the caret is in the wrong place.

### Core Emmet vs editor integration

The Emmet project defines actions, but an editor decides how they are exposed. A particular action may have:

- no default keyboard shortcut;
- a different command name;
- partial support;
- editor-specific behavior.

When an action described here is missing, search your editor's command palette before assuming Emmet itself lacks the feature.


---

# 49. Expand Abbreviation

This is the core Emmet action.

Input:

```text
ul>li*3
```

Run **Expand Abbreviation**.

Output:

```html
<ul>
    <li></li>
    <li></li>
    <li></li>
</ul>
```

## Best use cases

- new markup
- repeated structures
- CSS property generation
- snippets
- boilerplate

### Input → output

Input:

```text
ul>li.item*3
```

Action: **Expand Abbreviation**

Output:

```html
<ul>
    <li class="item"></li>
    <li class="item"></li>
    <li class="item"></li>
</ul>
```

Use the explicit command when Tab is reserved for indentation or when you want predictable expansion independent of suggestion selection.


---

# 50. Wrap with Abbreviation

Wrap with Abbreviation takes existing selected content and places it inside newly generated markup.

Suppose you have:

```text
Home
Products
About
Contact
```

Select the lines and run **Wrap with Abbreviation**.

Use an abbreviation concept such as:

```text
nav>ul>li*>a
```

The repeated `*` in wrapping workflows can use the selected lines as repeated input.

Possible result:

```html
<nav>
    <ul>
        <li><a href="">Home</a></li>
        <li><a href="">Products</a></li>
        <li><a href="">About</a></li>
        <li><a href="">Contact</a></li>
    </ul>
</nav>
```

## Why this is powerful

You can transform plain text from:

- requirements
- copied content
- CMS exports
- menus
- lists

into structured markup without manually wrapping each line.

### Real-world scenario

Suppose you select:

```text
Home
Products
Contact
```

and wrap with:

```text
ul>li*>a
```

the selected lines can become repeated list items/links according to the integration's wrap behavior.

This action is especially useful when content already exists and you want to add structure around it instead of generating empty elements first.


---

# 51. Balance Outward and Inward

Tag balancing selects meaningful HTML regions based on the caret position.

Imagine:

```html
<div class="card">
    <h2>Title</h2>
    <p>Hello <strong>world</strong>.</p>
</div>
```

Place the caret near `world`.

**Balance Outward** can progressively select:

1. the nearest text/tag region
2. the surrounding `<strong>`
3. the paragraph
4. the card

**Balance Inward** can shrink the selection.

## Use cases

- refactoring nested HTML
- moving blocks
- deleting complete structures
- wrapping selected markup
- understanding nesting

### Mental model

**Balance outward** expands the selection to the next meaningful enclosing markup structure.

**Balance inward** moves back toward a smaller inner structure.

Use it when nested HTML is difficult to select precisely with the mouse. It is a structural selection tool, not a formatting command.


---

# 52. Go to Matching Pair

This action jumps between matching opening and closing tags.

Example:

```html
<section>
    ...
</section>
```

If your caret is in one tag, the action can move to the matching partner.

Useful in deeply nested markup where scrolling manually is slow.

### When it helps

Place the caret on or inside one side of a tag pair and invoke the action to move to its matching opening/closing side.

This is useful in long nested markup where visually tracing indentation is slow. It depends on the editor being able to recognize the current markup pair.


---

# 53. Go to Edit Point

Emmet can move between important editing positions such as:

- empty attributes
- positions between tags
- useful blank/indented locations

Example:

```html
<a href=""></a>
```

An edit-point action can help move directly to `href=""` or another meaningful location.

## Good use case

After generating a large structure, navigate quickly through places that need values.

### What counts as an edit point?

Emmet identifies places that are likely to need input, such as empty attribute values or empty elements. The action moves the caret between those places.

Use it after generating a larger structure to fill in blanks efficiently. Do not treat edit points as semantic validation; Emmet cannot know every field your application actually requires.


---

# 54. Select Item

Select Item helps select meaningful HTML or CSS parts.

Potential targets include:

- tag names
- attributes
- attribute values
- CSS properties
- CSS values

This is useful when you repeatedly need to replace one logical unit without dragging the mouse.

### Why use it?

Structured selection is useful for quickly replacing:

- a tag name;
- an attribute;
- an attribute value;
- a CSS property;
- a CSS value.

It reduces character-by-character selection mistakes. Exact selectable items depend on the current syntax and editor integration.


---

# 55. Toggle Comment

Emmet's Toggle Comment action can understand nearby HTML or CSS context.

Example:

```html
<section class="promo">
    ...
</section>
```

Instead of selecting every line manually, context-aware commenting can target the relevant structure.

Editor support varies.

### Context matters

The action chooses comment syntax based on the current document context. In markup it may produce an HTML-style comment; in stylesheets it may use CSS comment syntax.

Always inspect the result in mixed-language files such as templates, because the editor determines the active language context.


---

# 56. Split/Join Tag

This action can change between a self-closing form and a paired form in XML-style contexts.

Concept:

```xml
<example />
```

can become:

```xml
<example></example>
```

and vice versa.

Useful in:

- XML
- XSL
- custom markup
- JSX/XML-like workflows, subject to editor support

For standard HTML, remember that HTML void elements have their own syntax rules.

### Example idea

Split:

```html
<div class="box"></div>
```

into a form appropriate to an empty/self-closing representation when the syntax allows it, or join the reverse form.

Whether a tag *should* be self-closing is controlled by the target language. HTML, XML, and JSX do not have identical rules, so preview the transformation.


---

# 57. Remove Tag

Remove Tag removes the surrounding tag while preserving its content.

Before:

```html
<div class="wrapper">
    <p>Hello</p>
</div>
```

Remove the `div` tag:

```html
<p>Hello</p>
```

This is excellent when simplifying unnecessary wrapper markup.

### What makes this different from Delete?

The useful behavior is structural: remove the surrounding tag while keeping its inner content when the action/integration supports that context.

Example goal:

```html
<div><strong>Hello</strong></div>
```

remove the `strong` wrapper while preserving:

```html
<div>Hello</div>
```

Use it when refactoring unnecessary wrappers.


---

# 58. Merge Lines

Merge Lines combines selected lines into one line.

Before:

```html
<p>
    Hello
    world
</p>
```

After merging, depending on context:

```html
<p>Hello world</p>
```

Useful for:

- compact inline markup
- SVG/XML snippets
- generated content cleanup

Do not sacrifice readability simply to reduce line count.

### Use case

After pasting or expanding markup, related content may be spread across several lines. Merge Lines can compact the selected structure.

This is a source-editing convenience, not a minifier. Do not use it as a replacement for a formatter or production HTML/CSS minification.


---

# 59. Update Image Size

Some Emmet integrations can inspect an image referenced in HTML or CSS and add/update dimensions.

Example:

```html
<img src="images/logo.png" alt="Company logo">
```

The action may update it to include intrinsic dimensions:

```html
<img src="images/logo.png" alt="Company logo" width="..." height="...">
```

This can help reduce layout shift when the dimensions are known.

## Limitations

Behavior depends on:

- editor integration
- path resolution
- local/remote file accessibility
- image type

Modern frameworks may also handle images through build pipelines, so this action is not always applicable.

### What it tries to do

For a supported local image reference, the action can inspect image dimensions and update width/height information in source.

This depends on the editor integration being able to resolve and read the image. Remote URLs, generated assets, or framework loaders may not work the same way.

For responsive images, fixed intrinsic dimensions and CSS display size are separate concerns.


---

# 60. Evaluate Math Expression

Emmet can evaluate simple math expressions in supported editors.

Example:

```text
20*4
```

becomes:

```text
80
```

Useful while editing numeric CSS values.

Example scenario:

You have:

```css
width: 320px;
```

Need one quarter:

```text
320/4
```

Evaluate:

```text
80
```

This avoids switching to a calculator for small arithmetic.

### Example

If the editor contains a numeric expression such as:

```text
10 * 3 + 5
```

the action can evaluate the expression in a supported context and replace it with the result:

```text
35
```

Use it for quick source calculations, not for business logic that belongs in application code.


---

# 61. Increment/Decrement Number

Emmet can change the number under the caret by a step.

Example:

```css
margin: 10px;
```

Increment by 1:

```css
margin: 11px;
```

Possible action variants may increment/decrement by values such as:

- 1
- 0.1
- 10

depending on editor integration.

## Useful for

- tuning spacing
- adjusting opacity
- changing pixel dimensions
- iterating transform values

### Typical use

Place the caret on a numeric value such as:

```css
margin: 20px;
```

and use an increment/decrement action to change the number without manually selecting it.

Different actions may use different step sizes. Check your editor's command names/keybindings before building muscle memory around a shortcut.


---

# 62. Reflect CSS Value

This action historically synchronizes values across vendor-prefixed versions of the same CSS property.

Example concept:

```css
-webkit-transform: rotate(10deg);
transform: rotate(10deg);
```

Changing one and reflecting can update related declarations.

## Modern note

If your build pipeline uses Autoprefixer, you may rarely need this manually.

### Why it exists

Legacy or manually prefixed CSS may contain several versions of the same declaration. Reflect CSS Value can help keep related prefixed values synchronized.

In modern build pipelines, prefer generated prefixing where possible so you do not have to maintain several declarations by hand.


---

# 63. Encode/Decode Image as Data URL

Emmet includes an action for converting image references to/from a `data:` URL in supported integrations.

Potential use cases:

- tiny embedded assets
- self-contained HTML demos
- small test fixtures

## Do not overuse data URLs

Large embedded assets can:

- make CSS/HTML difficult to read
- increase source size
- prevent normal caching behavior
- complicate debugging

Use them selectively.

### Trade-off

Encoding a small image as a data URL can remove a separate file reference, but it also makes the source larger and less readable.

Use it intentionally for very small assets or specific build requirements. For normal application assets, let your build system and caching strategy guide the decision.


---

# 64. Filters

Filters are post-processors.

That means:

1. Emmet parses your abbreviation.
2. It creates an internal tree.
3. A filter modifies the generated result.
4. The final output is inserted.

A filter can be appended with `|`.

Example concept:

```text
div#page|c
```

applies a comment filter in environments that support it.

Filters can be configured globally in some editor integrations.

## Think of filters as output transformations

A filter is applied after Emmet understands the abbreviation.

```text
abbreviation
    ↓
parsed tree
    ↓
normal expansion
    ↓
filter
    ↓
final text
```

That means a filter cannot rescue a structurally invalid abbreviation. First make sure the abbreviation expands correctly, then add the filter.

Filter support is also integration-sensitive. If a filter shown in core Emmet documentation does not work in your editor, check that editor's Emmet documentation.


---

# 65. Comment Filter

The comment filter can add comments near significant tags, commonly elements with classes or IDs.

Example abbreviation:

```text
div#page>section.content|c
```

A possible output style:

```html
<div id="page">
    <section class="content"></section>
    <!-- /.content -->
</div>
<!-- /#page -->
```

This style was more common in older float-based layouts.

Modern developers often do not need closing comments for every wrapper, but the feature can still help in long generated markup.

---

# 66. BEM Filter

BEM means:

- **Block**
- **Element**
- **Modifier**

Example class names:

```text
card
card__title
card__button
card--featured
```

Emmet has BEM-related filtering support.

This can help teams that consistently use BEM naming conventions.

## Important

BEM filters are workflow tools—not a requirement for BEM.

You can also simply type BEM classes directly:

```text
article.card>h2.card__title+button.card__button
```

---

# 67. Trim Filter

The trim filter is particularly relevant to **Wrap with Abbreviation**.

When copied text contains line markers, numbering, or prefixes, trim behavior can remove unwanted leading markers during wrapping.

Use it when transforming text lists into structured markup.

Support and exact behavior vary by Emmet integration.

## Practical wrapping example

Trim is most useful with **Wrap with Abbreviation** when selected lines begin with markers you do not want to preserve.

Input text:

```text
1. Alpha
2. Beta
3. Gamma
```

The trim behavior can remove the leading markers while the wrapping abbreviation creates the target structure.

Because wrap/filter details can differ between integrations, test the transformation on a small selection before applying it to a large document.


---

# 68. Escape Filter

The escape filter converts XML-unsafe characters in generated markup into entities.

Concept:

```text
div.example|e
```

Instead of outputting actual markup, it may produce escaped text suitable for displaying code.

For example:

```html
&lt;div class="example"&gt;&lt;/div&gt;
```

Useful for:

- documentation
- tutorials
- code examples rendered inside HTML

---

# 69. Custom Emmet Snippets

If you repeatedly type the same project-specific structure, create a custom Emmet snippet.

Example goal:

```text
cardx
```

could expand to your team's card pattern.

In current VS Code Emmet integration, custom snippets are placed in a file named:

```text
snippets.json
```

Example:

```json
{
    "html": {
        "snippets": {
            "cardx": "article.card>h2.card__title{${1:Title}}+p.card__text{${2:Description}}"
        }
    }
}
```

## Why custom snippets matter

Emmet is most powerful when it reflects your actual project patterns.

Good snippet candidates:

- standard form field
- Bootstrap/Tailwind-independent component structure
- card
- modal skeleton
- page section
- company-specific data table
- accessibility pattern
- framework template structure

## Prefer snippets for stable team patterns

A custom snippet is a good fit when the same skeleton appears repeatedly and the structure is stable.

It is a poor fit when:

- the structure depends heavily on runtime data;
- a framework component already encapsulates it;
- the snippet would generate dozens of lines that developers rarely inspect;
- the pattern changes every week.

### Treat `snippets.json` as project tooling

If a team depends on custom Emmet snippets, version-control the snippet file or document how developers obtain it. Otherwise each developer can end up with a different expansion for the same abbreviation.


---

# 70. Tab Stops and Placeholders

Current VS Code custom Emmet snippets use TextMate-style tab stops.

```text
${1}
${2}
```

Placeholder:

```text
${1:Title}
```

Example:

```json
{
    "html": {
        "snippets": {
            "fieldx": "div.form-field>label[for=${1:id}]{${2:Label}}+input#${1}[name=${1}]"
        }
    }
}
```

After expansion, Tab can move through editable placeholders if supported by the editor.

## Final cursor

Snippet systems often support `$0`/`${0}` as a final position, but behavior can depend on the integration. Follow your editor's documented snippet behavior.

## Current VS Code custom-snippet syntax

For VS Code's Emmet integration, use TextMate-style tab stops in custom snippets:

```text
${1}
${2}
${1:default text}
${0}
```

`$0`/`${0}` represents the final cursor position in the underlying snippet system.

Older Emmet examples found online may use legacy cursor markers such as `|` or `${cursor}`. Do not assume those examples apply to current VS Code Emmet custom snippets.

### Reusing a tab stop

Using the same number more than once can mirror the same input:

```text
label[for=${1:id}]+input#${1}
```

Entering `email` for tab stop `1` can populate both linked locations, depending on the editor's snippet behavior.


---

# 71. Emmet Variables

Variables let you customize values used by snippets.

In VS Code:

```json
{
    "emmet.variables": {
        "lang": "en",
        "charset": "UTF-8"
    }
}
```

A language variable can affect snippets such as HTML boilerplate that reference `${lang}`.

Example for another language:

```json
{
    "emmet.variables": {
        "lang": "hi"
    }
}
```

This is useful when your projects consistently use a specific document language.

---

# 72. VS Code Emmet Configuration

As of the current VS Code documentation, useful Emmet settings include:

```text
emmet.includeLanguages
emmet.excludeLanguages
emmet.syntaxProfiles
emmet.variables
emmet.showExpandedAbbreviation
emmet.showAbbreviationSuggestions
emmet.extensionsPath
emmet.triggerExpansionOnTab
emmet.showSuggestionsAsSnippets
emmet.preferences
```

A sample configuration:

```json
{
    "emmet.triggerExpansionOnTab": true,
    "emmet.showSuggestionsAsSnippets": true,
    "editor.snippetSuggestions": "top",
    "emmet.includeLanguages": {
        "javascript": "javascriptreact"
    },
    "emmet.variables": {
        "lang": "en"
    }
}
```

Do not copy every setting blindly. Add only what improves your workflow.

## What each setting category controls

| Setting | Main purpose |
|---|---|
| `emmet.includeLanguages` | Map an additional VS Code language ID to an Emmet syntax |
| `emmet.excludeLanguages` | Disable Emmet in selected language IDs |
| `emmet.syntaxProfiles` | Customize generated syntax/output style |
| `emmet.variables` | Override Emmet variables such as `lang` |
| `emmet.triggerExpansionOnTab` | Allow Tab to expand valid abbreviations |
| `emmet.showExpandedAbbreviation` | Control expanded-abbreviation suggestions |
| `emmet.showAbbreviationSuggestions` | Control Emmet abbreviation suggestions |
| `emmet.showSuggestionsAsSnippets` | Surface Emmet suggestions as snippets |
| `emmet.extensionsPath` | Point to a directory containing custom `snippets.json` |
| `emmet.preferences` | Configure supported Emmet preferences |

Use language IDs, not human display names, when a setting expects a language.

### Configuration debugging rule

If Emmet behaves strangely, temporarily remove custom Emmet settings and confirm default behavior. Then reintroduce settings one at a time. This separates an Emmet problem from a configuration problem.


---

# 73. Enable Tab Expansion in VS Code

VS Code does not require you to use Tab for Emmet.

If you want it:

```json
{
    "emmet.triggerExpansionOnTab": true
}
```

This allows Tab to expand a recognized Emmet abbreviation while still serving as indentation when the text is not an abbreviation.

## If Tab does not expand

Check:

1. Is the file language recognized?
2. Is the abbreviation valid?
3. Is `emmet.triggerExpansionOnTab` enabled?
4. Is another extension intercepting Tab?
5. Does **Emmet: Expand Abbreviation** work from the Command Palette?
6. Is the built-in Emmet extension disabled?

## Trade-off

Enabling:

```json
{
  "emmet.triggerExpansionOnTab": true
}
```

is convenient when you use Emmet constantly, but Tab also has important roles in indentation, completion, and snippet navigation.

If Tab expansion feels unpredictable, leave it disabled and use:

- the Emmet suggestion from IntelliSense; or
- **Emmet: Expand Abbreviation** from the command palette / a dedicated keybinding.

Choose one predictable workflow rather than enabling every completion mechanism at once.


---

# 74. Enable Emmet in Other Languages

Use:

```json
{
    "emmet.includeLanguages": {
        "javascript": "javascriptreact",
        "razor": "html"
    }
}
```

The left side is your file's language ID.

The right side is the Emmet syntax to use.

## Example mental model

```text
"my language" : "treat it like this Emmet language"
```

## Warning

Emmet does not automatically understand the grammar of every mapped language.

You can get irrelevant suggestions if the mapping is too broad.

## Mapping does not add language intelligence

This configuration:

```json
{
  "emmet.includeLanguages": {
    "some-template-language": "html"
  }
}
```

means “offer HTML-style Emmet behavior in this VS Code language mode.”

It does **not** teach Emmet:

- the template language's directives;
- its component model;
- server-side syntax;
- validation rules.

Test a mapping in a representative file before applying it across a workspace.


---

# 75. Exclude Languages

To disable Emmet for selected languages, use:

```json
{
    "emmet.excludeLanguages": [
        "markdown"
    ]
}
```

This can help if Emmet suggestions interfere with another workflow.

## Input and effect

`emmet.excludeLanguages` accepts VS Code language IDs.

```json
{
  "emmet.excludeLanguages": [
    "markdown",
    "plaintext"
  ]
}
```

Use it when Emmet suggestions compete with prose, another snippet system, or a language-specific completion provider.

Excluding a language only changes Emmet participation; it does not disable the language extension or the editor's other completion features.


---

# 76. Control Suggestions

## Hide expanded abbreviation suggestions

```json
{
    "emmet.showExpandedAbbreviation": "never"
}
```

You can still manually run **Emmet: Expand Abbreviation**.

Other supported modes include behavior that limits suggestions to markup/stylesheets or allows broader display.

## Show Emmet suggestions as snippets

```json
{
    "emmet.showSuggestionsAsSnippets": true,
    "editor.snippetSuggestions": "top"
}
```

This is useful if you want Emmet suggestions near the top of IntelliSense.

## Abbreviation suggestions

VS Code also exposes:

```json
{
    "emmet.showAbbreviationSuggestions": true
}
```

This can help discover snippets you have not memorized.

---

# 77. Syntax Profiles

Syntax profiles customize generated output.

Example VS Code configuration:

```json
{
    "emmet.syntaxProfiles": {
        "html": {
            "attr_quotes": "single"
        },
        "jsx": {
            "self_closing_tag": true
        }
    }
}
```

## Important distinction

`emmet.syntaxProfiles` is for changing output style.

Use `emmet.includeLanguages` to map additional languages.

Do not use `syntaxProfiles` as a replacement for language mapping.

## Output profile vs language mapping

Keep this distinction memorized:

```text
includeLanguages → Where should Emmet run, and which syntax should it behave like?
syntaxProfiles   → How should generated output be styled for a syntax?
```

A syntax profile can influence output preferences such as attribute quoting or self-closing behavior where supported. It does not make an unsupported language become HTML-aware.


---

# 78. Preferences

VS Code exposes a supported subset of Emmet preferences through:

```json
{
    "emmet.preferences": {
    }
}
```

Examples of configurable areas include:

- CSS property ending
- value separator
- default units
- unit aliases
- BEM separators
- comment filter formatting
- indentation behavior
- fuzzy search threshold

Example:

```json
{
    "emmet.preferences": {
        "bem.elementSeparator": "__",
        "bem.modifierSeparator": "--"
    }
}
```

Support for individual preferences depends on the VS Code Emmet integration.

---

# 79. Extensions Path and Custom Snippets

In VS Code, `emmet.extensionsPath` points to a **directory** containing `snippets.json`.

Example:

```json
{
    "emmet.extensionsPath": "C:\\Users\\YourName\\emmet"
}
```

Directory:

```text
C:\Users\YourName\emmet\
└── snippets.json
```

On Linux/macOS:

```json
{
    "emmet.extensionsPath": "/home/user/.config/emmet"
}
```

## Current custom snippet rules worth remembering

For VS Code Emmet 2.0:

- custom snippets live under the `snippets` property
- CSS snippet names should not use `:`
- CSS snippet values should normally omit the final semicolon
- use `${1}`, `${2}`, `${1:placeholder}` style tab stops
- old cursor markers such as `|` are not the current VS Code custom snippet syntax

## Portable setup suggestion

Instead of hard-coding a personal absolute path in team instructions, consider keeping a shared `snippets.json` in a documented tooling folder and tell each developer how to point `emmet.extensionsPath` to it.

After changing the file or path:

1. confirm the JSON parses;
2. confirm the file is literally named `snippets.json`;
3. verify the top-level language key;
4. reload/restart the editor if the integration does not immediately pick up changes;
5. test one minimal custom abbreviation.

This is faster than debugging a complex snippet first.


---

# 80. Multi-Cursor Workflows

VS Code supports many Emmet actions with multiple cursors.

Example scenario:

```html
<div></div>
<div></div>
<div></div>
```

Place a cursor inside each element, then use a supported Emmet action or abbreviation expansion.

## Useful multi-cursor tasks

- add the same child structure to several components
- edit matching properties
- generate repeated nested elements
- update values across related CSS declarations

Use multi-cursor + Emmet when repetitions are similar but not easily represented by one `*` expression.

---

# 81. Troubleshooting

## Problem 1: Abbreviation does not expand

Check the current file language.

VS Code enables Emmet by default in many markup and stylesheet languages, including HTML, JSX, XML, CSS, SCSS, Sass, Less, and related inherited modes.

If your language is not included, configure `emmet.includeLanguages`.

## Fast diagnostic sequence

When Emmet fails, check in this order:

```text
1. Is the file in the language mode I think it is?
2. Does a basic abbreviation such as `div` expand?
3. Does the explicit Expand Abbreviation command work?
4. Is the language excluded?
5. Is includeLanguages mapping needed?
6. Is Tab expansion the only thing failing?
7. Are custom settings/snippets causing the problem?
8. Does the editor integration support this action/filter?
```

This sequence starts with the simplest dependency and avoids changing several settings at once.

## Compatibility note

Emmet core documentation and VS Code Emmet documentation describe overlapping but not identical surfaces. When the handbook discusses a VS Code setting such as `emmet.includeLanguages`, treat the VS Code documentation as the source of truth for that setting. When it discusses core abbreviation syntax or actions, use Emmet's own documentation as the baseline and then verify editor support.


---

## Problem 2: Tab only indents

Enable:

```json
{
    "emmet.triggerExpansionOnTab": true
}
```

Or use the Emmet command directly.

---

## Problem 3: Suggestions do not appear

Possible causes:

- quick suggestions are disabled
- Emmet suggestions are hidden
- wrong language mode
- Emmet built-in extension is disabled
- abbreviation is not valid in current context

In VS Code, manually trigger suggestions using:

```text
Ctrl+Space
```

on Windows/Linux.

---

## Problem 4: Custom snippet does not work

Check:

- file is named `snippets.json`
- `emmet.extensionsPath` points to its directory
- JSON is valid
- correct syntax section is used
- current VS Code Emmet 2.0 snippet format is followed
- tab stops use `${1}` style
- CSS snippet names do not use `:`
- CSS snippet values do not incorrectly include syntax-specific punctuation

---

## Problem 5: Custom tags are not suggested

VS Code intentionally avoids suggesting every unknown single word as a custom tag because that would create excessive noise.

A custom tag may work when part of a richer expression, and Tab expansion can help when enabled.

---

## Problem 6: Expansion is not what you expected

Do this:

1. inspect the suggestion preview
2. reduce the abbreviation
3. verify each operator
4. check current syntax mode
5. check custom snippets
6. check syntax profile
7. check filters
8. check editor-specific Emmet behavior

---

# 82. Common Beginner Mistakes

## Mistake 1: Adding spaces inside an abbreviation

Wrong:

```text
ul > li * 5
```

Spaces can terminate Emmet parsing.

Use:

```text
ul>li*5
```

---

## Mistake 2: Confusing child and sibling

```text
div>h2+p
```

means:

```text
div
├── h2
└── p
```

But:

```text
div>h2>p
```

means:

```text
div
└── h2
    └── p
```

These are very different.

---

## Mistake 3: Forgetting operator precedence

When structure becomes complicated, use parentheses.

Instead of fighting:

```text
...
```

use clearly grouped blocks.

---

## Mistake 4: Creating giant abbreviations

A 150-character abbreviation may be harder to type and debug than five short expansions.

The goal is productivity, not abbreviation golf.

---

## Mistake 5: Assuming generated code is automatically correct

Review:

- semantics
- accessibility
- IDs
- attributes
- form labels
- ARIA
- responsive behavior
- CSS units
- JSX syntax

---

## Mistake 6: Memorizing too many CSS shortcuts at once

Learn the 15–20 properties you use daily.

Use fuzzy search and suggestion previews for the rest.

---

## Mistake 7: Assuming every editor behaves like VS Code

Emmet integration differs among editors.

Shortcut names, actions, configuration paths, filters, and snippet handling may differ.

---

# 83. Best Practices

## 83.1 Learn structure before shortcuts

Master these first:

```text
>
+
*
#
.
[]
{}
$
()
^
```

Once these are natural, Emmet becomes much easier.

## 83.2 Preview before expanding unfamiliar abbreviations

Especially for CSS fuzzy search.

## 83.3 Prefer semantic HTML

Use:

```text
header
main
nav
article
section
footer
```

where appropriate.

## 83.4 Keep abbreviations small enough to reason about

Good:

```text
section.features>.feature*3>h2+p
```

Potentially excessive:

```text
div#app>(header>nav>ul>li*6>a)+(main>(section*4>article*3>h2+p*2+a))+footer>...
```

## 83.5 Create custom snippets for repeated project patterns

If you type the same structure every day, turn it into a snippet.

## 83.6 Do not let Emmet hide fundamentals

You should be able to explain the final HTML/CSS without Emmet.

## 83.7 Let build tools handle compatibility where appropriate

Use modern tools such as Autoprefixer rather than manually filling your stylesheet with unnecessary prefixes.

---

# 84. When Not to Use Emmet

Do not force Emmet when:

- the markup is highly irregular
- you only need one short tag
- the abbreviation is harder to remember than the code
- generated output needs heavy editing
- the task is better handled by a framework component
- a project-specific snippet is clearer
- accessibility requires careful custom markup
- server-side/template syntax conflicts with Emmet parsing

Example:

Typing:

```html
<main>
```

may be just as easy as thinking about an abbreviation.

The best developer workflow uses Emmet selectively.

---

# 85. Productivity Workflows

## Workflow 1: Build structure first, content second

1. Generate page skeleton.
2. Generate repeated components.
3. Move through edit points.
4. Fill real content.
5. review semantics.

---

## Workflow 2: Convert copied text to markup

Input:

```text
Home
Services
Pricing
Contact
```

Use **Wrap with Abbreviation**:

```text
nav>ul>li*>a
```

Then add URLs.

---

## Workflow 3: Prototype component grids

```text
section.cards>article.card*12>h2{Card $}+p>lorem12
```

Great for testing responsive grid behavior quickly.

---

## Workflow 4: CSS tuning

Use:

- short CSS abbreviations
- increment/decrement number
- evaluate math
- multi-cursor edits

to rapidly test dimensions.

---

## Workflow 5: Project snippet library

Create snippets for:

```text
field
card
modal
alert
table
pagination
empty-state
dashboard-section
```

This produces more value than memorizing obscure one-off abbreviations.

---

# 86. Real-World Mini Projects

## Project 1: Landing Page Skeleton

Abbreviation:

```text
(header.site-header>nav.main-nav>ul>li*4>a[href=#]{Link $})+(main>(section.hero>h1{Build Better Websites}+p>lorem15+a.btn[href=#cta]{Start Now})+(section.features>.feature*3>h2{Feature $}+p>lorem20))+footer.site-footer
```

### Learning goals

- grouping
- siblings
- children
- repetition
- classes
- attributes
- text
- Lorem Ipsum

---

## Project 2: Product Grid

```text
main>section.products>article.product-card*6>img[src="images/product$.jpg" alt="Product $"]+h2{Product $}+p.description>lorem12^p.price{₹999}+button[type=button]{Add to cart}
```

### What to review after expansion

- alt text
- pricing data
- image dimensions
- button behavior
- semantic structure

---

## Project 3: Registration Form

```text
form.registration>h1{Create Account}+.field>label[for=name]{Name}+input#name[type=text name=name autocomplete=name required]^.field>label[for=email]{Email}+input#email[type=email name=email autocomplete=email required]^.field>label[for=password]{Password}+input#password[type=password name=password autocomplete=new-password required]^button[type=submit]{Register}
```

### Learning goals

- attributes
- IDs
- sibling/child control
- climb-up
- accessibility basics

---

## Project 4: Blog Layout

```text
main.blog>(article.post>header>h1{Post Title}+p.meta{Published today}^section.content>p*4>lorem25)+aside.sidebar>h2{Related Posts}+ul>li*5>a[href=#]{Post $}
```

---

## Project 5: Dashboard

```text
div.dashboard>aside.sidebar>nav>ul>li*5>a[href=#]{Menu $}^^main.dashboard-main>(header.dashboard-header>h1{Dashboard})+(section.stats>.stat-card*4>h2{Metric $}+p.value{0})+(section.activity>h2{Recent Activity}+ul>li*8{Activity $})
```

---

# 87. Practice Exercises

Try each exercise before reading the solution.

## Exercise 1

Create:

```html
<ul>
    <li></li>
    <li></li>
    <li></li>
</ul>
```

Solution:

```text
ul>li*3
```

---

## Exercise 2

Create five buttons named `Button 1` to `Button 5`.

Solution:

```text
button{Button $}*5
```

---

## Exercise 3

Create:

```html
<div class="container">
    <header></header>
    <main></main>
    <footer></footer>
</div>
```

Solution:

```text
.container>header+main+footer
```

---

## Exercise 4

Create three cards with a title and paragraph.

Solution:

```text
.cards>.card*3>h2{Card $}+p
```

---

## Exercise 5

Create a link with `target="_blank"` and `rel="noopener"`.

Solution:

```text
a[href=# target=_blank rel=noopener]
```

---

## Exercise 6

Create numbered IDs:

```text
section1
section2
section3
```

Solution:

```text
section#section$*3
```

---

## Exercise 7

Generate 20 words of placeholder text in a paragraph.

Solution:

```text
p>lorem20
```

---

## Exercise 8

Write an abbreviation for:

```html
<nav>
    <a href="/">Home</a>
    <a href="/about">About</a>
</nav>
```

Possible solution:

```text
nav>a[href=/]{Home}+a[href=/about]{About}
```

---

## Exercise 9

Write CSS abbreviation(s) for:

```css
margin: 20px;
padding: 10px 15px;
width: 100%;
```

Possible answers:

```text
m20
p10-15
w100p
```

---

## Exercise 10

Build a table containing:

- 4 column headings
- 5 body rows
- 4 cells per row

Solution:

```text
table>(thead>tr>th*4)+(tbody>tr*5>td*4)
```

---

# 88. Interview and Revision Questions

## Beginner

1. What problem does Emmet solve?
2. What does `>` mean?
3. What does `+` mean?
4. What does `*` mean?
5. How do you add a class?
6. How do you add an ID?
7. How do you add attributes?
8. How do you insert text?
9. What does `$` do?
10. What does `lorem20` do?

## Intermediate

1. What is the difference between `>` and `+`?
2. When is `^` useful?
3. Why use grouping?
4. What are implicit tag names?
5. How does numbering work with repetition?
6. How can Emmet help with CSS?
7. What is fuzzy search?
8. What does Wrap with Abbreviation do?
9. What are Emmet filters?
10. What are custom snippets?

## Advanced

1. When should you avoid a large Emmet abbreviation?
2. How does editor context affect expansion?
3. What is the difference between `emmet.includeLanguages` and `emmet.syntaxProfiles` in VS Code?
4. How are custom snippet tab stops defined?
5. Why can CSS fuzzy matching be both useful and risky?
6. When would a project-specific custom snippet be better than a native Emmet abbreviation?
7. Why should modern prefix management often be delegated to build tooling?
8. How can multi-cursor editing and Emmet complement each other?
9. Why is Emmet not a substitute for semantic HTML?
10. How would you debug an abbreviation that expands incorrectly?

---

# 89. Quick Reference Cheat Sheet

## HTML structure

```text
div                → element
.container         → class
#app               → id
div.card.active    → multiple classes
div#app.container  → id + class
```

## Relationships

```text
div>p              → child
h1+p               → sibling
div>section^footer → climb up
li*5               → repeat
(section>h2+p)*3   → repeated group
```

## Attributes

```text
a[href=#]
input[type=email]
button[type=submit disabled]
div[data-id=10]
```

## Text

```text
h1{Hello}
button{Save}
a{Read More}
```

## Numbering

```text
li.item$*5
li.item$$*5
li.item$@3*5
li.item$@-*5
```

## Lorem

```text
lorem
lorem10
p>lorem30
p*3>lorem12
```

## Common structures

```text
ul>li*5
nav>ul>li*5>a
table>(thead>tr>th*4)+(tbody>tr*5>td*4)
.cards>.card*6>h2+p
form>.field*4>label+input
```

## Common CSS patterns

```text
m10
mt20
p10-20
w100
w100p
h100vh
fz16
fw700
lh1.5
c#333
bgc#fff
bdrs8
posa
t0
r0
```

## VS Code settings

```json
{
    "emmet.triggerExpansionOnTab": true,
    "emmet.showSuggestionsAsSnippets": true,
    "editor.snippetSuggestions": "top"
}
```

Enable JSX-style Emmet in JavaScript:

```json
{
    "emmet.includeLanguages": {
        "javascript": "javascriptreact"
    }
}
```

---

# 90. Learning Roadmap

## Stage 1 — First 30 minutes

Learn:

```text
>
+
*
.
#
{}
[]
```

Practice:

```text
ul>li*5
.card>h2+p
nav>ul>li*4>a
```

## Verification habit for advanced use

When you move beyond basic abbreviations, keep two references bookmarked:

- the official Emmet documentation for abbreviation syntax and actions;
- your editor's Emmet integration documentation for settings, keybindings, and compatibility.

This prevents a common problem: copying an old Emmet configuration that was written for a different editor generation.


---

## Stage 2 — First day

Learn:

```text
$
()
^
lorem
```

Practice:

```text
.cards>.card*6>h2{Card $}+p>lorem15
```

---

## Stage 3 — First week

Use Emmet during real development.

Focus on:

- forms
- navigation
- tables
- card lists
- layout shells
- CSS spacing
- sizing
- typography

Do not try to memorize the whole cheat sheet.

---

## Stage 4 — Productive user

Learn actions:

- Wrap with Abbreviation
- Balance
- Matching Pair
- Remove Tag
- Increment/Decrement Number
- Evaluate Math

---

## Stage 5 — Advanced workflow

Add:

- custom snippets
- variables
- filters
- syntax profiles
- editor configuration
- multi-cursor workflows

---

## Stage 6 — Team workflow

Create a small shared convention for common component abbreviations.

For example:

```text
cardx
fieldx
modalx
tablex
emptyx
```

Document each custom abbreviation in your project.

---

# 91. Official References

Use these sources when you need exact current behavior.

## Emmet

- Official documentation: https://docs.emmet.io/
- Abbreviation syntax: https://docs.emmet.io/abbreviations/syntax/
- Abbreviations overview: https://docs.emmet.io/abbreviations/
- Implicit tag names: https://docs.emmet.io/abbreviations/implicit-names/
- Lorem Ipsum generator: https://docs.emmet.io/abbreviations/lorem-ipsum/
- CSS abbreviations: https://docs.emmet.io/css-abbreviations/
- CSS fuzzy search: https://docs.emmet.io/css-abbreviations/fuzzy-search/
- CSS gradients: https://docs.emmet.io/css-abbreviations/gradients/
- Actions: https://docs.emmet.io/actions/
- Wrap with Abbreviation: https://docs.emmet.io/actions/wrap-with-abbreviation/
- Filters: https://docs.emmet.io/filters/
- Customization: https://docs.emmet.io/customization/
- Cheat sheet: https://docs.emmet.io/cheat-sheet/

## Visual Studio Code

- Emmet in VS Code: https://code.visualstudio.com/docs/languages/emmet

---

# Final Advice

Emmet becomes valuable when you stop thinking of it as a list of magic shortcuts and start thinking in **HTML trees and CSS intentions**.

For markup, master this mental vocabulary:

```text
parent > child
sibling + sibling
repeat * n
class .name
id #name
attributes [name=value]
text {content}
number $
group ()
climb ^
```

Then an expression such as:

```text
section.features>.feature*3>h2{Feature $}+p>lorem15
```

becomes easy to read:

> Create a `section.features`, put three `.feature` blocks inside it, and inside every feature place a numbered heading followed by a paragraph containing placeholder text.

For CSS, focus on the properties you use every day and rely on Emmet's suggestion preview and fuzzy search for less-common abbreviations.

The objective is not to write the shortest abbreviation possible.

The objective is:

> **Write correct, readable web code faster while keeping full understanding of the generated result.**

---

# Appendix A — Scenario Drill Pack

This appendix gives short tasks you can repeatedly practice until the syntax feels natural.

## A.1 Header with logo and menu

```text
header.site-header>a.logo[href=/]{Brand}+nav>ul>li*4>a[href=#]{Link $}
```

## A.2 Hero with two buttons

```text
section.hero>h1{Build Something Great}+p>lorem20+div.actions>a.btn.primary[href=#]{Get Started}+a.btn.secondary[href=#]{Learn More}
```

If the hierarchy is not what you intended, group the action links:

```text
section.hero>h1{Build Something Great}+p>lorem20+(div.actions>a.btn.primary[href=#]{Get Started}+a.btn.secondary[href=#]{Learn More})
```

## A.3 Feature list

```text
section.features>article.feature*4>h2{Feature $}+p>lorem18
```

## A.4 Testimonial list

```text
section.testimonials>blockquote.testimonial*3>p>lorem20^footer{Customer $}
```

## A.5 Footer columns

```text
footer.site-footer>.footer-column*4>h2{Column $}+ul>li*5>a[href=#]{Link $}
```

## A.6 Pagination

```text
nav[aria-label=Pagination]>ul.pagination>li*5>a[href=#]{Page $}
```

## A.7 Definition list

```text
dl>dt{Term $}+dd{Definition $}
```

Repeat the pair using grouping:

```text
dl>(dt{Term $}+dd{Definition $})*4
```

## A.8 Image gallery

```text
.gallery>figure*8>img[src="image$.jpg" alt="Image $"]+figcaption{Image $}
```

## A.9 Notification list

```text
ul.notifications>li.notification*5>strong{Notification $}+p>lorem8
```

## A.10 Settings panel

```text
section.settings>h1{Settings}+.setting*5>label{Setting $}+input[type=checkbox]
```

---

# Appendix B — Learn Emmet by Reading Trees

Translate each abbreviation into a tree before expanding it.

## B.1

```text
div>p+span
```

Tree:

```text
div
├── p
└── span
```

## B.2

```text
div>p>span
```

Tree:

```text
div
└── p
    └── span
```

## B.3

```text
div>(p+span)*2
```

Tree:

```text
div
├── p
├── span
├── p
└── span
```

## B.4

```text
main>(section>h2+p)+aside
```

Tree:

```text
main
├── section
│   ├── h2
│   └── p
└── aside
```

## B.5

```text
ul>li*3>a
```

Tree:

```text
ul
├── li
│   └── a
├── li
│   └── a
└── li
    └── a
```

If you can predict these trees, you understand the core Emmet grammar.

---

# Appendix C — Recommended Daily Practice

For one week, use this routine.

## Day 1

Practice only:

```text
>
+
*
```

## Day 2

Add:

```text
.
#
```

## Day 3

Add:

```text
[]
{}
```

## Day 4

Add:

```text
$
()
```

## Day 5

Add:

```text
^
lorem
```

## Day 6

Practice CSS abbreviations you actually use.

Example set:

```text
m10
p10
w100p
h100vh
fz16
fw700
lh1.5
bgc#fff
c#222
bdrs8
```

## Day 7

Learn:

- Wrap with Abbreviation
- Balance
- multi-cursor use
- custom snippets

By the end of the week, normal HTML structure generation should feel much faster.

---

# Appendix D — Personal Emmet Snippet Starter File for VS Code

Create:

```text
snippets.json
```

Example starter:

```json
{
    "html": {
        "snippets": {
            "cardx": "article.card>h2.card__title{${1:Title}}+p.card__text{${2:Description}}",
            "fieldx": "div.form-field>label[for=${1:field}]{${2:Label}}+input#${1}[name=${1}]",
            "emptyx": "section.empty-state>h2{${1:Nothing here yet}}+p{${2:Try again later.}}",
            "sectionx": "section.page-section>div.container>h2{${1:Section title}}+p{${2:Section introduction}}"
        }
    },
    "css": {
        "snippets": {
            "cardbase": "background: ${1:#fff}; border-radius: ${2:8px}; padding: ${3:1rem}",
            "centerflex": "display: flex; align-items: center; justify-content: center",
            "truncate1": "overflow: hidden; text-overflow: ellipsis; white-space: nowrap"
        }
    }
}
```

Remember that CSS custom snippet handling follows the current Emmet integration rules of your editor. In VS Code, avoid a trailing semicolon at the end of the custom CSS snippet definition because Emmet adds syntax-appropriate endings.

---

# Appendix E — Emmet vs Editor Snippets

Both solve repetitive typing, but they are not identical.

| Feature | Emmet | Normal editor snippet |
|---|---|---|
| Dynamic HTML tree syntax | Excellent | Usually fixed |
| Repetition with `*` | Built in | Usually fixed/manual |
| Numbering with `$` | Built in | Depends on snippet system |
| CSS abbreviation resolver | Yes | Usually no |
| Project-specific boilerplate | Customizable | Excellent |
| Complex fixed code template | Possible | Often better |
| Easy discoverability | Suggestion preview | Depends on editor |

## Rule of thumb

Use **Emmet** for dynamic structures:

```text
ul>li*8>a
```

Use a **normal custom snippet** when the output is mostly fixed and contains framework/business logic.

Use **custom Emmet snippets** when you want a reusable shortcut that still benefits from Emmet-style structure.

---

# Appendix F — Emmet vs AI Code Completion

AI coding tools and Emmet solve different problems.

## Emmet

Best for:

- deterministic structure
- predictable expansion
- zero-prompt markup
- repetitive CSS declarations
- fast keyboard workflows

## AI completion

Best for:

- logic
- contextual code
- larger components
- business rules
- transformations requiring interpretation

## Example

For:

```html
<ul>
    <li><a></a></li>
    ...
</ul>
```

Emmet is often faster:

```text
ul>li*5>a
```

For:

> "Build an accessible searchable product table with sorting and pagination"

AI may be more appropriate because the request requires design and logic decisions.

The strongest workflow uses the right tool for the right job.

---

# Appendix G — Mastery Checklist

Use this checklist to confirm that you truly understand Emmet.

- [ ] I can explain what Emmet is.
- [ ] I understand that Emmet does not replace HTML/CSS knowledge.
- [ ] I can expand a basic abbreviation.
- [ ] I understand the `>` child operator.
- [ ] I understand the `+` sibling operator.
- [ ] I understand the `^` climb-up operator.
- [ ] I can repeat elements with `*`.
- [ ] I can group structures using `()`.
- [ ] I can add classes using `.`.
- [ ] I can add IDs using `#`.
- [ ] I can add attributes using `[]`.
- [ ] I can add text using `{}`.
- [ ] I can use `$` for numbering.
- [ ] I understand zero-padded numbering.
- [ ] I know how to change numbering direction/base.
- [ ] I understand implicit tag names.
- [ ] I can generate Lorem Ipsum.
- [ ] I can build a navigation menu with one abbreviation.
- [ ] I can build a form skeleton.
- [ ] I can build a table skeleton.
- [ ] I can build repeated card layouts.
- [ ] I use semantic HTML rather than blindly generating divs.
- [ ] I understand basic CSS abbreviations.
- [ ] I understand implicit and explicit CSS units.
- [ ] I know that CSS fuzzy search exists.
- [ ] I preview uncertain CSS expansions.
- [ ] I know what Wrap with Abbreviation does.
- [ ] I know what Balance does.
- [ ] I know what Go to Matching Pair does.
- [ ] I know what Remove Tag does.
- [ ] I understand Emmet filters conceptually.
- [ ] I know how custom Emmet snippets work.
- [ ] I can use `${1}` and `${1:placeholder}` tab stops.
- [ ] I know what `emmet.includeLanguages` does in VS Code.
- [ ] I know what `emmet.syntaxProfiles` is for.
- [ ] I know how to enable Tab expansion.
- [ ] I can troubleshoot a non-expanding abbreviation.
- [ ] I know when not to use Emmet.
- [ ] I prefer clarity over extremely clever abbreviations.
- [ ] I review generated code for accessibility and semantics.
- [ ] I can create my own small Emmet productivity workflow.

If you can confidently complete this checklist, you have moved beyond basic Emmet usage and can apply it productively in real projects.
