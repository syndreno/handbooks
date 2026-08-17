# Excel Mastery Handbook
## Beginner → Intermediate → Advanced → Expert

> A single-file learning handbook for mastering Microsoft Excel through explanations, examples, real-world scenarios, exercises, and best practices.

---

# Table of Contents

1. [How to Use This Handbook](#1-how-to-use-this-handbook)
2. [What Excel Is and Where It Is Used](#2-what-excel-is-and-where-it-is-used)
3. [Excel Interface and Workbook Basics](#3-excel-interface-and-workbook-basics)
4. [Cells, Ranges, Rows, Columns, and References](#4-cells-ranges-rows-columns-and-references)
5. [Entering, Editing, and Cleaning Data](#5-entering-editing-and-cleaning-data)
6. [Formatting and Professional Spreadsheet Design](#6-formatting-and-professional-spreadsheet-design)
7. [Excel Tables](#7-excel-tables)
8. [Formula Fundamentals](#8-formula-fundamentals)
9. [Cell References: Relative, Absolute, and Mixed](#9-cell-references-relative-absolute-and-mixed)
10. [Essential Math and Statistical Functions](#10-essential-math-and-statistical-functions)
11. [Logical Functions](#11-logical-functions)
12. [Text Functions](#12-text-functions)
13. [Date and Time Functions](#13-date-and-time-functions)
14. [Lookup and Reference Functions](#14-lookup-and-reference-functions)
15. [Dynamic Array Functions](#15-dynamic-array-functions)
16. [Error Handling and Formula Debugging](#16-error-handling-and-formula-debugging)
17. [Conditional Formatting](#17-conditional-formatting)
18. [Data Validation and Controlled Input](#18-data-validation-and-controlled-input)
19. [Sorting, Filtering, and Subtotals](#19-sorting-filtering-and-subtotals)
20. [Charts and Data Visualization](#20-charts-and-data-visualization)
21. [PivotTables and PivotCharts](#21-pivottables-and-pivotcharts)
22. [What-If Analysis](#22-what-if-analysis)
23. [Named Ranges and Named Formulas](#23-named-ranges-and-named-formulas)
24. [Advanced Formula Design](#24-advanced-formula-design)
25. [LET and LAMBDA](#25-let-and-lambda)
26. [Power Query](#26-power-query)
27. [Data Model and Power Pivot](#27-data-model-and-power-pivot)
28. [DAX Fundamentals](#28-dax-fundamentals)
29. [Dashboard Design](#29-dashboard-design)
30. [Financial and Accounting Use Cases](#30-financial-and-accounting-use-cases)
31. [HR and Payroll Use Cases](#31-hr-and-payroll-use-cases)
32. [Sales and Operations Use Cases](#32-sales-and-operations-use-cases)
33. [Inventory and Procurement Use Cases](#33-inventory-and-procurement-use-cases)
34. [Data Cleaning and Reconciliation](#34-data-cleaning-and-reconciliation)
35. [Importing and Exporting Data](#35-importing-and-exporting-data)
36. [Protection, Security, and Collaboration](#36-protection-security-and-collaboration)
37. [Macros and VBA](#37-macros-and-vba)
38. [Office Scripts and Modern Automation](#38-office-scripts-and-modern-automation)
39. [Performance Optimization](#39-performance-optimization)
40. [Common Excel Mistakes](#40-common-excel-mistakes)
41. [Keyboard Shortcuts](#41-keyboard-shortcuts)
42. [Real-World Projects](#42-real-world-projects)
43. [Excel Interview Questions](#43-excel-interview-questions)
44. [Learning Roadmap](#44-learning-roadmap)
45. [Function Cheat Sheet](#45-function-cheat-sheet)
46. [Final Mastery Checklist](#46-final-mastery-checklist)


### Additional Advanced Chapters

47. [Financial Functions](#47-financial-functions)
48. [Statistical and Analytical Functions](#48-statistical-and-analytical-functions)
49. [Reference, Information, and Utility Functions](#49-reference-information-and-utility-functions)
50. [Printing, Page Layout, and Report Delivery](#50-printing-page-layout-and-report-delivery)
51. [View, Navigation, Grouping, and Large-Sheet Productivity](#51-view-navigation-grouping-and-large-sheet-productivity)
52. [Notes, Comments, Links, and Documentation](#52-notes-comments-links-and-documentation)
53. [Sparklines, Icons, and In-Cell Visualization](#53-sparklines-icons-and-in-cell-visualization)
54. [Advanced Workbook Architecture](#54-advanced-workbook-architecture)
55. [Formula Design Patterns Worth Memorizing](#55-formula-design-patterns-worth-memorizing)
56. [Auditing and Control Framework for Business Excel](#56-auditing-and-control-framework-for-business-excel)
57. [Expert-Level Questions to Ask Before Building](#57-expert-level-questions-to-ask-before-building)

The final practice sections and mastery map are intentionally kept outside the numbered chapter sequence.

---

# 1. How to Use This Handbook

Excel is too large to master by memorizing formulas. The better approach is to learn **how to think in Excel**.

For each topic:

1. Understand **what problem the feature solves**.
2. Learn the basic syntax.
3. Re-create the example yourself.
4. Change the values and observe the result.
5. Apply the concept to a business scenario.
6. Combine it with previously learned concepts.

A useful learning sequence is:

```text
Data Entry
   ↓
Formatting
   ↓
Formulas
   ↓
Functions
   ↓
Tables
   ↓
Lookups
   ↓
Data Cleaning
   ↓
PivotTables
   ↓
Charts
   ↓
Power Query
   ↓
Power Pivot / DAX
   ↓
Dashboards
   ↓
Automation
```

Do not try to memorize every function. Learn the most common patterns and know where to look when you need something specialized.

---

# 2. What Excel Is and Where It Is Used

Microsoft Excel is a spreadsheet application used to store, calculate, analyze, transform, and visualize structured data.

Typical uses include:

- Accounting
- Budgeting
- Payroll
- Financial reporting
- Invoice tracking
- Procurement
- Inventory management
- Sales reporting
- Project management
- Data reconciliation
- HR reporting
- MIS reports
- KPI dashboards
- Forecasting
- Data cleaning
- Data analysis
- Business intelligence
- Automation

## Example

A company has this sales data:

| Invoice | Customer | Quantity | Price |
|---|---|---:|---:|
| INV001 | ABC Ltd | 10 | 500 |
| INV002 | XYZ Ltd | 5 | 1,000 |

Excel can calculate:

```excel
=Quantity * Price
```

Result:

| Invoice | Customer | Quantity | Price | Amount |
|---|---|---:|---:|---:|
| INV001 | ABC Ltd | 10 | 500 | 5,000 |
| INV002 | XYZ Ltd | 5 | 1,000 | 5,000 |

The same data could later be summarized using PivotTables, displayed in charts, cleaned with Power Query, and used in a dashboard.

---

# 3. Excel Interface and Workbook Basics

## Workbook

An Excel file is called a **workbook**.

Common extensions:

```text
.xlsx  Standard workbook
.xlsm  Macro-enabled workbook
.xlsb  Binary workbook
.csv   Comma-separated text file
.xls   Older Excel format
```

## Worksheet

Each tab inside a workbook is a **worksheet**.

Example:

```text
Sales.xlsx
├── Raw_Data
├── Customer_Master
├── Analysis
└── Dashboard
```

A good workbook normally separates:

- Raw data
- Master data
- Calculations
- Reports
- Dashboards

## Ribbon

The Ribbon contains tabs such as:

- Home
- Insert
- Page Layout
- Formulas
- Data
- Review
- View
- Automate

## Formula Bar

Shows the value or formula stored in the selected cell.

## Name Box

Displays the active cell address.

Example:

```text
B12
```

You can also type a range such as:

```text
A1:D100
```

into the Name Box to select it quickly.

---

# 4. Cells, Ranges, Rows, Columns, and References

## Cell

A cell is the intersection of a row and column.

```text
A1
B5
D20
```

## Range

A group of cells.

```text
A1:A10
A1:D20
```

## Entire Column

```text
A:A
```

## Entire Row

```text
5:5
```

## Multiple Ranges

Functions sometimes support multiple ranges.

```excel
=SUM(A1:A10,C1:C10)
```

## Cross-Sheet Reference

```excel
=Sales!B2
```

If the sheet has spaces:

```excel
='Sales Data'!B2
```

## Cross-Workbook Reference

Excel can also reference another workbook.

Conceptually:

```excel
='[Budget.xlsx]Jan'!B2
```

External links should be used carefully because moved or renamed files can break them.

## How Excel Reads a Reference

A reference tells Excel **where to get a value from**. The reference itself is not the value.

If `B2` contains `500`, then:

```excel
=B2
```

returns:

```text
500
```

This distinction matters because formulas usually work with **references to cells**, not copied values.

### Reference operators

| Pattern | Meaning | Example |
|---|---|---|
| `:` | Continuous range | `A2:A20` |
| `,` | Separate references supplied to a function | `SUM(A1:A5,C1:C5)` |
| `!` | Separates sheet name from cell/range | `Sales!B2` |
| `#` | Refers to an entire spilled dynamic-array result | `G2#` |

### Entire-column references: useful but not always ideal

A formula such as:

```excel
=COUNTIF(A:A,"Open")
```

is convenient and usually fine in small workbooks. In large calculation-heavy models, thousands of formulas that repeatedly scan entire columns can increase recalculation work. Prefer Excel Tables or realistically bounded ranges when performance matters.

### Common beginner mistake: selecting only one column before sorting

A reference can point to one column, but a **record** usually spans several columns. If you sort only the Amount column while Customer and Invoice columns are not included, records can become misaligned. When working with datasets, select the whole table or let Excel detect the current region.


---

# 5. Entering, Editing, and Cleaning Data

Good analysis starts with clean data.

## Recommended Tabular Structure

Use:

```text
One row = one record
One column = one field
One header row
```

Good:

| Invoice | Vendor | Date | Amount |
|---|---|---|---:|
| 1001 | ABC | 01-Jan-2026 | 5000 |
| 1002 | XYZ | 02-Jan-2026 | 7000 |

Avoid:

- Blank rows inside data
- Merged cells inside datasets
- Multiple header rows
- Totals embedded in raw data
- Different data types in one column

## Fill Handle

Drag the bottom-right corner of a selected cell to copy formulas or continue patterns.

Example:

```text
Jan
Feb
Mar
```

Excel can continue:

```text
Apr
May
Jun
```

## Flash Fill

Flash Fill recognizes a pattern.

If:

```text
A2 = Shoeb Shaikh
B2 = Shoeb
```

and you begin typing first names, Excel can infer the remaining pattern.

Shortcut:

```text
Ctrl + E
```

Useful for:

- Extracting first names
- Reformatting IDs
- Combining codes
- Splitting structured text

## Find and Replace

Shortcut:

```text
Ctrl + H
```

Example:

Replace:

```text
Ltd.
```

with:

```text
Limited
```

Useful when standardizing vendor or customer names.

## Remove Duplicates

Use:

```text
Data → Remove Duplicates
```

Scenario:

A customer master contains repeated customer IDs. Select the Customer ID column and remove duplicates.

Be careful: duplicate removal permanently deletes rows from that range.

---

# 6. Formatting and Professional Spreadsheet Design

Formatting improves readability, but excessive formatting makes workbooks harder to maintain.

## Number Formats

Common formats:

```text
General
Number
Currency
Accounting
Percentage
Date
Time
Text
Custom
```

## Example

Stored value:

```text
0.18
```

Percentage format displays:

```text
18%
```

The underlying value remains `0.18`.

## Custom Number Formats

Examples:

```text
0
0.00
#,##0
#,##0.00
₹#,##0.00
0.0%
```

Show zero as dash:

```text
#,##0;-#,##0;-
```

Display values in millions:

```text
0.0,,"M"
```

## Professional Formatting Guidelines

Prefer:

- One consistent font
- Clear headers
- Thousands separators
- Appropriate decimal places
- Consistent date formats
- Limited color usage
- Freeze panes for long reports
- Meaningful worksheet names

Avoid:

- Random colors
- Too many borders
- Merged cells in data tables
- Hard-to-read fonts
- Excessive decimals

---

# 7. Excel Tables

Excel Tables are one of the most important features for reliable spreadsheet models.

Create a table:

```text
Ctrl + T
```

Example data:

| Date | Customer | Product | Amount |
|---|---|---|---:|
| 01-Jan | ABC | Laptop | 50,000 |
| 02-Jan | XYZ | Mouse | 1,000 |

After converting to a table, Excel provides:

- Automatic filtering
- Automatic formatting
- Formula auto-fill
- Dynamic expansion
- Structured references
- Easier PivotTable sources

## Structured Reference

Traditional formula:

```excel
=D2*E2
```

Table formula:

```excel
=[@Quantity]*[@Price]
```

Sum table column:

```excel
=SUM(Sales[Amount])
```

## Scenario

If new sales records are added tomorrow, formulas and PivotTable source ranges are easier to manage when the source is an Excel Table.

---

# 8. Formula Fundamentals

A formula starts with:

```text
=
```

Examples:

```excel
=A1+B1
=A1-B1
=A1*B1
=A1/B1
=A1^2
```

## Operator Order

Excel generally follows:

```text
()
^
* /
+ -
```

Example:

```excel
=10+5*2
```

Result:

```text
20
```

because multiplication is calculated before addition.

Use parentheses when intention should be explicit:

```excel
=(10+5)*2
```

Result:

```text
30
```

## Comparison Operators

```text
=   Equal to
<>  Not equal to
>   Greater than
<   Less than
>=  Greater than or equal
<=  Less than or equal
```

Example:

```excel
=A2>=10000
```

Returns:

```text
TRUE
FALSE
```

## Formula Anatomy

A formula can contain:

```text
= function(arguments) operator reference
```

Example:

```excel
=ROUND(B2*C2,2)
```

Breakdown:

| Part | Meaning |
|---|---|
| `=` | Tells Excel this is a formula |
| `ROUND` | Function being called |
| `B2*C2` | First argument: calculation to round |
| `2` | Second argument: number of decimal places |
| Result | One calculated value returned to the cell |

A function's **inputs** are called arguments. The value produced by the formula is its **result** or return value.

## Text, Numbers, and Quotes

Text constants inside formulas normally need double quotes:

```excel
=IF(A2="Approved","Release","Hold")
```

Numbers normally do not:

```excel
=IF(B2>100000,"High","Normal")
```

A common mistake is writing:

```excel
=IF(A2=Approved,Release,Hold)
```

Excel may interpret those words as names instead of text.

## Formula vs Displayed Value

Formatting does not normally change the underlying number.

If a cell stores:

```text
0.185
```

and is formatted as a percentage with one decimal place, it may display:

```text
18.5%
```

Formulas still calculate using the underlying value.

## When a Formula Should Not Be Used

Do not create a formula merely because Excel can. Prefer:

- Power Query for repeatable data transformation,
- PivotTables for flexible aggregation,
- database logic for large multi-user transactional systems,
- a helper column when one huge nested formula becomes difficult to audit.

The best Excel solution is the one that remains understandable and maintainable.


---

# 9. Cell References: Relative, Absolute, and Mixed

Understanding references is essential.

## Relative Reference

```excel
=A2*B2
```

When copied down:

```text
=A3*B3
=A4*B4
```

Use when the referenced row or column should move.

## Absolute Reference

```excel
=A2*$F$1
```

`$F$1` remains fixed when copied.

Scenario:

| A | B | F |
|---|---|---|
| Amount | Tax | Tax Rate |
| 1000 | ? | 18% |

Formula:

```excel
=A2*$F$1
```

Copy down.

## Mixed References

```text
$A1
A$1
```

`$A1` fixes column A but allows row to move.

`A$1` fixes row 1 but allows column to move.

## Shortcut

While editing a reference, press:

```text
F4
```

to cycle:

```text
A1
$A$1
A$1
$A1
```

---

# 10. Essential Math and Statistical Functions

## SUM

Adds numbers.

```excel
=SUM(B2:B10)
```

Scenario: Total invoice amount.

## AVERAGE

```excel
=AVERAGE(B2:B10)
```

Scenario: Average order value.

## MIN

```excel
=MIN(B2:B10)
```

## MAX

```excel
=MAX(B2:B10)
```

## COUNT

Counts numeric cells.

```excel
=COUNT(B2:B100)
```

## COUNTA

Counts non-empty cells.

```excel
=COUNTA(A2:A100)
```

## COUNTBLANK

```excel
=COUNTBLANK(A2:A100)
```

## ROUND

```excel
=ROUND(A2,2)
```

Example:

```text
123.456 → 123.46
```

## ROUNDUP

```excel
=ROUNDUP(A2,0)
```

## ROUNDDOWN

```excel
=ROUNDDOWN(A2,0)
```

## INT

Returns the integer portion.

```excel
=INT(10.95)
```

Result:

```text
10
```

## MOD

Returns the remainder.

```excel
=MOD(10,3)
```

Result:

```text
1
```

Useful for repeating patterns.

## ABS

Returns absolute value.

```excel
=ABS(-500)
```

Result:

```text
500
```

Useful in reconciliation and variance analysis.

## SUMIF

Single-condition sum.

```excel
=SUMIF(B:B,"Mumbai",D:D)
```

Scenario: Total sales for Mumbai.

## SUMIFS

Multiple-condition sum.

```excel
=SUMIFS(D:D,B:B,"Mumbai",C:C,"Laptop")
```

Scenario:

> Sum sales where City = Mumbai and Product = Laptop.

## COUNTIF

```excel
=COUNTIF(C:C,"Approved")
```

## COUNTIFS

```excel
=COUNTIFS(B:B,"Mumbai",C:C,"Approved")
```

## AVERAGEIF

```excel
=AVERAGEIF(B:B,"Sales",C:C)
```

## AVERAGEIFS

```excel
=AVERAGEIFS(D:D,B:B,"Mumbai",C:C,"Active")
```

## MEDIAN

```excel
=MEDIAN(B2:B100)
```

Median is useful when extreme values would distort an average.

## LARGE

```excel
=LARGE(B2:B100,3)
```

Returns the third-largest value.

## SMALL

```excel
=SMALL(B2:B100,2)
```

Returns the second-smallest value.

## RANK.EQ

```excel
=RANK.EQ(B2,$B$2:$B$20,0)
```

Ranks from largest to smallest.

## How to Read the Main Aggregation Functions

| Function | Typical syntax | Main inputs | Returns | Use when |
|---|---|---|---|---|
| `SUM` | `SUM(number1,[number2],...)` | Numbers or ranges | Total | You need an unconditional total |
| `AVERAGE` | `AVERAGE(number1,[number2],...)` | Numeric values | Arithmetic mean | You need a typical average |
| `COUNT` | `COUNT(value1,...)` | Values/ranges | Count of numeric cells | Only numeric entries should count |
| `COUNTA` | `COUNTA(value1,...)` | Values/ranges | Count of non-empty cells | Text and numbers should count |
| `COUNTBLANK` | `COUNTBLANK(range)` | Range | Number of blank cells | You are checking missing entries |
| `SUMIF` | `SUMIF(range,criteria,[sum_range])` | Criteria range, condition, optional sum range | Conditional total | One condition is enough |
| `SUMIFS` | `SUMIFS(sum_range,criteria_range1,criteria1,...)` | Sum range plus pairs of criteria ranges and criteria | Conditional total | Multiple conditions must all be met |
| `COUNTIF` | `COUNTIF(range,criteria)` | Range and condition | Matching count | You need one-condition counting |
| `COUNTIFS` | `COUNTIFS(criteria_range1,criteria1,...)` | Criteria pairs | Matching count | Multiple conditions must all be met |

### Criteria examples

```excel
=SUMIFS(D:D,B:B,"Mumbai",C:C,">="&DATE(2026,1,1))
```

The date condition is built by joining the comparison operator to a real Excel date value.

### Common mistake: mismatched `SUMIFS` ranges

In `SUMIFS`, the sum range and every criteria range should cover corresponding rows.

Risky:

```excel
=SUMIFS(D2:D100,B2:B90,"Mumbai")
```

Better:

```excel
=SUMIFS(D2:D100,B2:B100,"Mumbai")
```

### `ROUND`, `ROUNDUP`, and `ROUNDDOWN`

```excel
=ROUND(number,num_digits)
=ROUNDUP(number,num_digits)
=ROUNDDOWN(number,num_digits)
```

They return numbers, not formatted text. Use them when the **stored result** must be rounded. If you only want fewer decimals on screen, change the number format instead.


---

# 11. Logical Functions

Logical functions allow formulas to make decisions.

## IF

Syntax:

```excel
=IF(condition,value_if_true,value_if_false)
```

Example:

```excel
=IF(B2>=50,"Pass","Fail")
```

## Business Scenario

If invoice amount exceeds ₹100,000:

```excel
=IF(D2>100000,"Approval Required","Auto Process")
```

## Nested IF

```excel
=IF(B2>=90,"A",IF(B2>=75,"B",IF(B2>=60,"C","D")))
```

Nested IF works, but large formulas become difficult to maintain.

## IFS

Cleaner alternative:

```excel
=IFS(
B2>=90,"A",
B2>=75,"B",
B2>=60,"C",
TRUE,"D"
)
```

## AND

Returns TRUE only if every condition is TRUE.

```excel
=AND(B2>=50,C2="Active")
```

## OR

Returns TRUE if at least one condition is TRUE.

```excel
=OR(B2="Mumbai",B2="Pune")
```

## NOT

Reverses TRUE/FALSE.

```excel
=NOT(B2="Closed")
```

## IF + AND

```excel
=IF(AND(B2>=50000,C2="Approved"),"Release","Hold")
```

## IF + OR

```excel
=IF(OR(B2="Critical",C2>7),"Escalate","Normal")
```

## SWITCH

Useful when comparing one value against several known options.

```excel
=SWITCH(A2,
"IN","India",
"US","United States",
"UK","United Kingdom",
"Unknown")
```

## Inputs and Return Values

| Function | Inputs | Returns |
|---|---|---|
| `IF(test, true_result, false_result)` | One logical test and two possible results | One of the two results |
| `AND(test1,...)` | Multiple tests | `TRUE` only when all are true |
| `OR(test1,...)` | Multiple tests | `TRUE` when at least one is true |
| `NOT(test)` | One logical test | Reversed Boolean value |
| `IFS(test1,result1,...)` | Ordered condition/result pairs | Result belonging to first true condition |
| `SWITCH(expression,value1,result1,...,[default])` | One expression and comparison/result pairs | Matching result or optional default |

### Order matters in `IFS`

Excel evaluates conditions from top to bottom. Put more restrictive/highest-threshold conditions first.

Correct grading pattern:

```excel
=IFS(B2>=90,"A",B2>=75,"B",B2>=60,"C",TRUE,"D")
```

If `B2>=60` came first, a score of 95 would match that earlier condition and never reach the `"A"` rule.

### When not to nest more logic

If the business rule contains many mappings such as 30 status codes or tax slabs, a lookup table is often easier to maintain than a very long `IF`/`SWITCH` formula.


---

# 12. Text Functions

Text cleaning is extremely common in business data.

## CONCAT

```excel
=CONCAT(A2,B2)
```

## Text Concatenation Operator

```excel
=A2&" "&B2
```

Example:

```text
Shoeb + Shaikh → Shoeb Shaikh
```

## TEXTJOIN

```excel
=TEXTJOIN(", ",TRUE,A2:A10)
```

Combines multiple values using a separator.

## LEFT

```excel
=LEFT(A2,3)
```

If:

```text
IND-MUM-001
```

Result:

```text
IND
```

## RIGHT

```excel
=RIGHT(A2,3)
```

Result:

```text
001
```

## MID

```excel
=MID(A2,5,3)
```

Result:

```text
MUM
```

## LEN

```excel
=LEN(A2)
```

Useful for validating IDs.

## TRIM

Removes unnecessary spaces.

```excel
=TRIM(A2)
```

## CLEAN

Removes non-printable characters.

```excel
=CLEAN(A2)
```

Common import-cleaning pattern:

```excel
=TRIM(CLEAN(A2))
```

## UPPER

```excel
=UPPER(A2)
```

## LOWER

```excel
=LOWER(A2)
```

## PROPER

```excel
=PROPER(A2)
```

## FIND

Case-sensitive.

```excel
=FIND("@",A2)
```

## SEARCH

Case-insensitive.

```excel
=SEARCH("invoice",A2)
```

## SUBSTITUTE

Replace matching text.

```excel
=SUBSTITUTE(A2,"Ltd.","Limited")
```

## REPLACE

Replace characters by position.

```excel
=REPLACE(A2,1,3,"IND")
```

## TEXT

Converts numbers or dates into formatted text.

```excel
=TEXT(A2,"dd-mmm-yyyy")
```

```excel
=TEXT(B2,"₹#,##0.00")
```

## VALUE

Converts numeric text to number.

```excel
=VALUE(A2)
```

## TEXTBEFORE

```excel
=TEXTBEFORE(A2,"-")
```

## TEXTAFTER

```excel
=TEXTAFTER(A2,"-")
```

## TEXTSPLIT

```excel
=TEXTSPLIT(A2,",")
```

Very useful for delimited values.

## Function Inputs, Outputs, and Differences

| Function | Key inputs | Returns | Important distinction |
|---|---|---|---|
| `LEFT(text,[num_chars])` | Text and optional character count | Leftmost text | Position-based |
| `RIGHT(text,[num_chars])` | Text and optional character count | Rightmost text | Position-based |
| `MID(text,start_num,num_chars)` | Text, starting position, length | Middle portion | Position-based |
| `FIND(find_text,within_text,[start_num])` | Search text and source text | Character position | Case-sensitive |
| `SEARCH(find_text,within_text,[start_num])` | Search text and source text | Character position | Case-insensitive; supports wildcards |
| `SUBSTITUTE(text,old_text,new_text,[instance_num])` | Text values | Modified text | Replaces matching text |
| `REPLACE(old_text,start_num,num_chars,new_text)` | Text and positions | Modified text | Replaces by character position |
| `TEXT(value,format_text)` | Number/date plus format pattern | **Text** | Good for display strings; result is no longer numeric |
| `VALUE(text)` | Numeric text | Number | Useful when imported numbers are stored as text |

### `TEXT` warning

This formula:

```excel
=TEXT(A2,"dd-mmm-yyyy")
```

returns text such as `14-Aug-2026`. If later calculations require a real date, keep the source as a date and use cell formatting instead.

### Cleaning imported text

A common baseline is:

```excel
=TRIM(CLEAN(A2))
```

But `TRIM` is not a complete data-standardization solution. Non-breaking spaces, inconsistent punctuation, alternate spellings, and vendor aliases may require `SUBSTITUTE`, Power Query, or a maintained mapping table.


---

# 13. Date and Time Functions

Excel stores dates as serial numbers.

This allows date arithmetic.

## TODAY

```excel
=TODAY()
```

Returns today's date.

## NOW

```excel
=NOW()
```

Returns current date and time.

## DATE

```excel
=DATE(2026,8,12)
```

## YEAR

```excel
=YEAR(A2)
```

## MONTH

```excel
=MONTH(A2)
```

## DAY

```excel
=DAY(A2)
```

## EDATE

Adds months.

```excel
=EDATE(A2,3)
```

Scenario: Warranty expiration three months later.

## EOMONTH

Returns month-end date.

```excel
=EOMONTH(A2,0)
```

## DATEDIF

Example:

```excel
=DATEDIF(A2,B2,"Y")
```

Years between dates.

```excel
=DATEDIF(A2,B2,"M")
```

Months.

```excel
=DATEDIF(A2,B2,"D")
```

Days.

## DAYS

```excel
=DAYS(B2,A2)
```

## NETWORKDAYS

Counts working days excluding weekends.

```excel
=NETWORKDAYS(A2,B2)
```

With holidays:

```excel
=NETWORKDAYS(A2,B2,$H$2:$H$20)
```

## WORKDAY

Returns a future working date.

```excel
=WORKDAY(A2,10)
```

## Scenario: Payment Due

Invoice date:

```text
01-Aug-2026
```

Payment term:

```text
30 days
```

Formula:

```excel
=A2+30
```

For business-day payment logic:

```excel
=WORKDAY(A2,30,Holidays)
```

## Dates Are Numbers, Times Are Fractions of a Day

In the default date system used by modern Excel workbooks, valid dates are stored as serial numbers and times are stored as fractions of a day. That is why subtraction works:

```excel
=B2-A2
```

If `A2` and `B2` are dates, the result is a number of days.

## Main Date-Function Inputs and Outputs

| Function | Typical syntax | Returns |
|---|---|---|
| `TODAY()` | No arguments | Current date |
| `NOW()` | No arguments | Current date and time |
| `DATE(year,month,day)` | Numeric year/month/day | Valid Excel date |
| `EDATE(start_date,months)` | Date and month offset | Date shifted by months |
| `EOMONTH(start_date,months)` | Date and month offset | Last day of target month |
| `DAYS(end_date,start_date)` | Two dates | Difference in days |
| `NETWORKDAYS(start_date,end_date,[holidays])` | Date range and optional holidays | Count of working days |
| `WORKDAY(start_date,days,[holidays])` | Start date, working-day offset, optional holidays | Future/past working date |

### Calendar days vs working days

Use:

```excel
=A2+30
```

when the rule literally means 30 calendar days.

Use:

```excel
=WORKDAY(A2,30,Holidays)
```

when weekends and optional holidays should be excluded.

### Common mistakes

- Typing ambiguous date text such as `01/02/26` without knowing the locale.
- Comparing a date-time value to a date while forgetting the time portion.
- Using `TEXT` to turn dates into text and then expecting normal date arithmetic.
- Assuming `DATEDIF(...,"Y")` plus separate month/day calculations automatically forms a precise age breakdown without checking the boundary logic.


---

# 14. Lookup and Reference Functions

Lookup functions connect related datasets.

Example master:

| Vendor Code | Vendor Name | GSTIN |
|---|---|---|
| V001 | ABC Ltd | GST001 |
| V002 | XYZ Ltd | GST002 |

Transaction:

| Vendor Code | Amount |
|---|---:|
| V002 | 15000 |

We want Vendor Name from the master.

## XLOOKUP

Preferred modern lookup.

```excel
=XLOOKUP(A2,VendorMaster[Vendor Code],VendorMaster[Vendor Name],"Not Found")
```

Advantages:

- Can look left or right
- Exact match by default
- Cleaner syntax
- Built-in not-found handling

## VLOOKUP

Classic function:

```excel
=VLOOKUP(A2,$F$2:$H$100,2,FALSE)
```

Limitations:

- Lookup column must be first
- Column index numbers are fragile
- Cannot naturally look left

## HLOOKUP

Horizontal version of VLOOKUP.

Less common in well-structured datasets.

## INDEX + MATCH

Classic advanced lookup:

```excel
=INDEX(C2:C100,MATCH(A2,B2:B100,0))
```

Useful where XLOOKUP is unavailable.

## XMATCH

```excel
=XMATCH(A2,B2:B100,0)
```

Returns a matching position.

## Two-Way Lookup

Suppose:

| Product | Jan | Feb | Mar |
|---|---:|---:|---:|
| Laptop | 10 | 20 | 30 |
| Mouse | 40 | 50 | 60 |

Lookup product in A10 and month in B10:

```excel
=INDEX(B2:D3,
MATCH(A10,A2:A3,0),
MATCH(B10,B1:D1,0))
```

## Approximate Lookup

Useful for slabs.

| Minimum Score | Grade |
|---:|---|
| 0 | D |
| 60 | C |
| 75 | B |
| 90 | A |

Possible modern approach:

```excel
=XLOOKUP(B2,$A$2:$A$5,$B$2:$B$5,,-1)
```

Always understand whether you need exact or approximate matching.

## XLOOKUP Syntax Explained

```excel
=XLOOKUP(lookup_value,lookup_array,return_array,[if_not_found],[match_mode],[search_mode])
```

| Argument | Purpose |
|---|---|
| `lookup_value` | Value you are trying to find |
| `lookup_array` | One row/column containing possible matches |
| `return_array` | Row/column from which Excel returns the result |
| `if_not_found` | Optional fallback instead of `#N/A` |
| `match_mode` | Optional exact/approximate/wildcard behavior |
| `search_mode` | Optional search direction/method |

For ordinary master-data lookups, exact matching is usually safest.

### Why approximate lookup needs care

Approximate matching is powerful for slabs, brackets, and thresholds, but the data must be designed for that purpose. Do not use approximate matching simply to hide bad master data.

### `INDEX` + `MATCH` mental model

```excel
=INDEX(return_range,MATCH(lookup_value,lookup_range,0))
```

1. `MATCH` returns the position of the item.
2. `INDEX` returns the value at that position.

This decomposition makes the formula easier to debug.

### Duplicate keys

A normal lookup returns one match. If the lookup key is not unique, that may hide a data-quality problem. For one-to-many results, consider `FILTER`:

```excel
=FILTER(Orders,Orders[CustomerID]=A2,"No orders")
```

### When not to use a cell-by-cell lookup

For hundreds of thousands of rows or repeatable merges between large datasets, Power Query, the Data Model, SQL, or another data-processing tool may be more maintainable and performant.


---

# 15. Dynamic Array Functions

Modern Excel can return multiple values from one formula.

## FILTER

```excel
=FILTER(A2:D100,D2:D100>10000)
```

Returns rows where Amount > 10,000.

Multiple criteria:

```excel
=FILTER(A2:D100,(B2:B100="Mumbai")*(D2:D100>10000))
```

## UNIQUE

```excel
=UNIQUE(B2:B100)
```

Returns distinct values.

## SORT

```excel
=SORT(A2:D100,4,-1)
```

Sort by column 4 descending.

## SORTBY

```excel
=SORTBY(A2:D100,D2:D100,-1)
```

## SEQUENCE

```excel
=SEQUENCE(12)
```

Returns numbers 1 through 12.

## TAKE

```excel
=TAKE(A2:D100,10)
```

Returns first 10 rows.

## DROP

```excel
=DROP(A2:D100,1)
```

Drops first row.

## CHOOSECOLS

```excel
=CHOOSECOLS(A2:F100,1,3,6)
```

## CHOOSEROWS

```excel
=CHOOSEROWS(A2:F100,1,5,10)
```

## VSTACK

```excel
=VSTACK(JanData,FebData,MarData)
```

Combines tables vertically.

## HSTACK

Combines arrays horizontally.

```excel
=HSTACK(A2:A10,C2:C10)
```

## Spill Range Operator

If a dynamic formula is in G2:

```excel
=UNIQUE(A2:A100)
```

You can reference all spilled values using:

```excel
=G2#
```

## What "Spill" Means

A dynamic-array formula is entered once but may return many cells. The top-left cell owns the formula; the surrounding cells are the **spill range**.

If something blocks the required output area, Excel can return:

```text
#SPILL!
```

Common causes include existing values, merged cells, or a formula placed where the required spill area is unavailable.

## Key Inputs and Outputs

| Function | Main inputs | Output |
|---|---|---|
| `FILTER(array,include,[if_empty])` | Source array and Boolean include array | Matching rows/columns |
| `UNIQUE(array,[by_col],[exactly_once])` | Array plus optional uniqueness behavior | Distinct values |
| `SORT(array,[sort_index],[sort_order],[by_col])` | Array and sort rules | Sorted array |
| `SORTBY(array,by_array1,[sort_order1],...)` | Array plus one or more sort arrays | Sorted array |
| `TAKE(array,rows,[columns])` | Array and requested count | Leading/trailing rows/columns |
| `DROP(array,rows,[columns])` | Array and count to remove | Remaining rows/columns |
| `VSTACK(array1,[array2],...)` | Arrays | Vertically combined array |
| `HSTACK(array1,[array2],...)` | Arrays | Horizontally combined array |

### Boolean include arrays

This formula:

```excel
=FILTER(A2:D100,(B2:B100="Mumbai")*(D2:D100>10000))
```

uses multiplication as logical AND because `TRUE/FALSE` values are coerced to `1/0`.

For logical OR, addition is commonly used:

```excel
=FILTER(A2:D100,(B2:B100="Mumbai")+(B2:B100="Pune"))
```

### Do not type into the spill area

Edit the formula in the top-left cell. Values typed inside the intended spill output can block future expansion.


---

# 16. Error Handling and Formula Debugging

Common Excel errors:

| Error | Meaning |
|---|---|
| `#DIV/0!` | Division by zero |
| `#N/A` | Value not found |
| `#VALUE!` | Wrong data type |
| `#REF!` | Invalid reference |
| `#NAME?` | Unknown name/function |
| `#NUM!` | Invalid numeric result |
| `#SPILL!` | Dynamic array cannot spill |
| `#CALC!` | Calculation issue |

## IFERROR

```excel
=IFERROR(A2/B2,0)
```

## IFNA

Handles only `#N/A`.

```excel
=IFNA(XLOOKUP(A2,F:F,G:G),"Not Found")
```

## Formula Auditing

Useful tools:

```text
Formulas → Trace Precedents
Formulas → Trace Dependents
Formulas → Evaluate Formula
```

## Debugging Method

For a complex formula:

```excel
=IF(XLOOKUP(A2,F:F,G:G)>10000,"High","Low")
```

Test parts separately:

```excel
=XLOOKUP(A2,F:F,G:G)
```

Then:

```excel
=XLOOKUP(A2,F:F,G:G)>10000
```

Finally rebuild the entire formula.

---

# 17. Conditional Formatting

Conditional Formatting changes a cell's appearance based on rules.

Use:

```text
Home → Conditional Formatting
```

## Common Scenarios

### Highlight Overdue Invoices

If Due Date is in D2:

```excel
=D2<TODAY()
```

and status is not Paid:

```excel
=AND($D2<TODAY(),$E2<>"Paid")
```

### Highlight Duplicates

Built-in:

```text
Highlight Cells Rules → Duplicate Values
```

### Top 10

Useful for sales and performance analysis.

### Color Scales

Useful for heatmaps.

### Data Bars

Useful to compare values visually inside cells.

## Rule Formula Example

Highlight whole row where status is `Rejected`:

```excel
=$E2="Rejected"
```

The `$` locks the status column while allowing the row number to change.

---

# 18. Data Validation and Controlled Input

Data Validation prevents bad input.

Use:

```text
Data → Data Validation
```

## Drop-Down List

Possible statuses:

```text
Pending
Approved
Rejected
```

Source:

```text
Pending,Approved,Rejected
```

Better: reference a master list.

## Number Validation

Allow only amounts greater than zero.

## Date Validation

Allow dates only inside a financial year.

## Custom Formula Validation

Example: ID must contain exactly 8 characters.

```excel
=LEN(A2)=8
```

## Dependent Drop-Down Concept

Country:

```text
India
USA
```

City list changes depending on the chosen country.

Common ways:

- Named ranges + INDIRECT
- Modern dynamic-array approach
- Master-table driven design

For large systems, a proper normalized master table is easier to maintain.

---

# 19. Sorting, Filtering, and Subtotals

## Sorting

Single level:

```text
Amount → Largest to Smallest
```

Multi-level:

```text
Department
then Employee
then Date
```

## Filtering

Filters can restrict rows by:

- Text
- Number
- Date
- Color

Example:

```text
Company = ABC
Status = Pending
Amount > 50000
```

## Advanced Filter

Useful for complex criteria and extracting unique records.

## SUBTOTAL

Unlike SUM, SUBTOTAL can ignore filtered-out rows.

```excel
=SUBTOTAL(9,D2:D100)
```

`9` means SUM.

Common codes:

```text
1   AVERAGE
2   COUNT
3   COUNTA
9   SUM
```

Codes `101–111` can also ignore manually hidden rows.

## Sorting Safely

A sort changes row order; it should not break the relationship between fields in the same record.

For a sales table:

```text
Invoice | Customer | Date | Amount
```

sort the complete dataset, not just the Amount cells.

### Multi-level sort

Example business requirement:

```text
1. Region ascending
2. Customer ascending
3. Amount descending
```

Use the Sort dialog and add levels in that priority order.

## Filtering

Filtering temporarily hides records that do not meet the selected criteria. It does **not** delete them.

Useful filters include:

- text contains/begins with,
- number greater than/less than/between,
- dates by year/month/quarter,
- multiple selected categories,
- color or icon filters where applicable.

After copying visible filtered data, verify whether your workflow should copy only visible cells; careless copy/paste operations can affect hidden rows depending on the action.

## Subtotals

The classic Subtotal command works best on a normal sorted range where records for each group are adjacent.

Typical process:

```text
Sort by Department
→ Data > Subtotal
→ At each change in Department
→ Use SUM
→ Add subtotal to Amount
```

For modern analysis, PivotTables are often more flexible because they summarize without inserting subtotal rows into the source data.

### When not to use manual subtotal rows

Do not embed manual totals throughout raw source data. They make filtering, Power Query, PivotTables, and database-style processing harder.


---

# 20. Charts and Data Visualization

Charts should communicate a business message, not merely decorate a worksheet.

## Common Chart Types

### Column Chart

Good for comparing categories.

Example:

```text
Sales by Product
```

### Bar Chart

Good when category labels are long.

### Line Chart

Best for trends over time.

Example:

```text
Monthly Revenue
```

### Pie / Donut Chart

Use sparingly.

Best only when:

- Few categories
- Total equals 100%
- Exact comparison is not important

### Area Chart

Useful for volume over time but can become cluttered.

### Scatter Plot

Best for relationships between numeric variables.

Example:

```text
Advertising Spend vs Revenue
```

### Combo Chart

Combines chart types.

Example:

```text
Revenue = columns
Margin % = line
```

### Waterfall Chart

Useful for:

- Profit bridges
- Budget vs actual bridges
- Movement analysis

### Histogram

Useful for distributions.

### Box & Whisker

Useful for distribution, spread, and outliers.

## Chart Design Rules

Prefer:

- Clear title
- Meaningful units
- Limited gridlines
- Direct labels where useful
- Logical sort order
- Appropriate axis scale

Avoid:

- 3D charts
- Excessive colors
- Excessive legends
- Decorative shapes that hide information

---

# 21. PivotTables and PivotCharts

PivotTables summarize large datasets quickly.

Suppose:

| Date | Region | Product | Salesperson | Amount |
|---|---|---|---|---:|

You want:

```text
Total Amount by Region
```

Create:

```text
Insert → PivotTable
```

Place:

```text
Rows   → Region
Values → Amount
```

## Pivot Areas

```text
Filters
Columns
Rows
Values
```

## Example

Rows:

```text
Region
```

Columns:

```text
Month
```

Values:

```text
Sum of Amount
```

Result becomes a monthly region sales matrix.

## Value Calculations

PivotTables can show:

- Sum
- Count
- Average
- Min
- Max
- % of Grand Total
- % of Row Total
- Running Total
- Difference From
- Rank

## Grouping Dates

A date field can be grouped into:

- Year
- Quarter
- Month

## Slicers

Slicers are interactive visual filters.

Useful dashboard filters:

```text
Region
Department
Status
Product
```

## Timeline

Timeline is a visual date filter.

## Refresh

When source data changes:

```text
Data → Refresh All
```

If you use Excel Tables as sources, new rows are easier to include.

---

# 22. What-If Analysis

Excel can answer:

> What happens if an input changes?

## Goal Seek

Find the input required to reach a target.

Scenario:

```text
Profit = Revenue - Cost
```

You need Profit = ₹1,000,000.

Goal Seek can determine the Revenue required.

Use:

```text
Data → What-If Analysis → Goal Seek
```

## Scenario Manager

Compare multiple sets of assumptions.

Example:

```text
Best Case
Base Case
Worst Case
```

## Data Tables

Test how one or two inputs change a formula result.

Example:

Loan payment at different:

```text
Interest rates
Loan amounts
```

## Solver

Solver can optimize a result subject to constraints.

Examples:

- Maximize profit
- Minimize transportation cost
- Allocate budget
- Production planning
- Staff scheduling

---

# 23. Named Ranges and Named Formulas

Instead of:

```excel
=B2*$F$1
```

you could name F1:

```text
TaxRate
```

and write:

```excel
=B2*TaxRate
```

Advantages:

- Easier to read
- Easier to maintain
- Useful in models
- Useful in validation

## Name Manager

Use:

```text
Formulas → Name Manager
```

## Good Names

```text
TaxRate
SalesData
HolidayList
ExchangeRate
```

Avoid confusing names such as:

```text
A1
R1C1
Sales Data
```

Names cannot contain normal spaces.

## What a Name Actually Represents

A defined name is an alias that can refer to:

- a cell,
- a range,
- a constant,
- a formula,
- or a `LAMBDA`.

Example constant:

```text
Name: TaxRate
Refers to: =0.18
```

Then:

```excel
=B2*TaxRate
```

## Scope

A name can normally be workbook-scoped or worksheet-scoped.

- **Workbook scope:** available throughout the workbook.
- **Worksheet scope:** local to one worksheet.

Prefer workbook scope for shared assumptions unless there is a specific reason to keep names local.

## Creating a Name

A reliable workflow:

1. Select the target cell/range.
2. Use **Formulas → Define Name** or **Name Manager**.
3. Give the name a meaningful description.
4. Confirm the `Refers to` expression.
5. Test it in a formula.

## Dynamic Data: Prefer Tables

Older workbooks often used `OFFSET` or complicated formulas to create expanding named ranges. For ordinary tabular data, an Excel Table is usually simpler:

```excel
=SUM(Sales[Amount])
```

The table column expands automatically when new records are added.

## Common Mistakes

- Creating names that look like cell references.
- Reusing the same name with different worksheet scopes and confusing readers.
- Leaving obsolete names that point to deleted ranges.
- Using a name when a structured table reference would be clearer.

Use Name Manager periodically to audit names and broken references.


---

# 24. Advanced Formula Design

A good formula should be:

- Correct
- Understandable
- Maintainable
- Efficient

## Prefer Helper Columns When Helpful

One giant formula is not always better.

Instead of:

```excel
=IFERROR(IF(XLOOKUP(...)*SUMIFS(...)/NETWORKDAYS(...)>...),"",...)
```

split logic into:

```text
Lookup Value
Working Days
Calculated Amount
Final Status
```

This makes debugging easier.

## Boolean Arithmetic

TRUE/FALSE can behave as 1/0.

Example:

```excel
=SUMPRODUCT((A2:A100="Mumbai")*(B2:B100="Approved")*C2:C100)
```

## SUMPRODUCT

Powerful for multi-condition calculations.

```excel
=SUMPRODUCT((A2:A100="Mumbai")*(B2:B100>10000))
```

## AGGREGATE

Can perform calculations while ignoring hidden rows or errors.

## OFFSET

Creates dynamic references but is volatile.

Example concept:

```excel
=OFFSET(A1,0,0,COUNTA(A:A),1)
```

Prefer Excel Tables or modern functions where possible because volatile formulas can affect performance.

## INDIRECT

Builds references from text.

```excel
=INDIRECT("'"&A2&"'!B5")
```

Powerful but volatile and can create fragile workbook designs.

---

# 25. LET and LAMBDA

## LET

LET assigns names to intermediate calculations.

Without LET:

```excel
=(A2*B2)-(A2*B2*C2)
```

With LET:

```excel
=LET(
gross,A2*B2,
discount,gross*C2,
gross-discount
)
```

Benefits:

- Easier to read
- Reuses calculations
- Can improve efficiency

## LAMBDA

LAMBDA allows you to create reusable custom worksheet functions without traditional VBA.

Example:

```excel
=LAMBDA(amount,rate,amount*rate)
```

A named LAMBDA could become:

```excel
=GSTAmount(A2,B2)
```

## Example Custom Function

Name:

```text
NETAMOUNT
```

Definition:

```excel
=LAMBDA(gross,discount,gross-discount)
```

Then:

```excel
=NETAMOUNT(A2,B2)
```

LAMBDA becomes especially powerful when combined with dynamic arrays and helper functions.

## `LET` Syntax, Inputs, and Return Value

```excel
=LET(name1,name_value1,[name2,name_value2,...],calculation)
```

`LET` creates temporary names that exist only inside that formula. The **last argument is the calculation returned by the function**.

Example:

```excel
=LET(
    qty,B2,
    price,C2,
    gross,qty*price,
    ROUND(gross,2)
)
```

Inputs:

```text
B2 = quantity
C2 = unit price
```

Output:

```text
Rounded quantity × price
```

Use `LET` when a complex expression is repeated or when meaningful intermediate names make the formula easier to read. It can also avoid recalculating the same expression repeatedly.

## `LAMBDA` Syntax, Inputs, and Return Value

```excel
=LAMBDA([parameter1,parameter2,...],calculation)
```

Parameters are inputs supplied when the function is called. The final calculation is the return value.

Test a LAMBDA directly:

```excel
=LAMBDA(amount,rate,amount*rate)(1000,0.18)
```

Result:

```text
180
```

Once tested, define it in Name Manager:

```text
Name: TaxAmount
Refers to: =LAMBDA(amount,rate,amount*rate)
```

Then use:

```excel
=TaxAmount(B2,$F$1)
```

## Common Errors

- A LAMBDA typed into a cell but not called can return `#CALC!`.
- Passing the wrong number of arguments can return an error.
- Recursive LAMBDAs need a valid stopping condition; uncontrolled recursion can fail.
- Parameter names must follow Excel naming rules.

## When Not to Use LAMBDA

Do not hide simple arithmetic inside dozens of custom functions. Use LAMBDA when reuse and clarity improve. For processes that import files, modify workbook structure, send data elsewhere, or require side effects, Power Query, VBA, Office Scripts, or an external application may be more appropriate.


---

# 26. Power Query

Power Query is one of the most valuable Excel tools for repeatable data preparation.

It follows the ETL concept:

```text
Extract
Transform
Load
```

## Typical Sources

Power Query can work with data from sources such as:

- Excel files
- CSV
- Text files
- Folders
- Databases
- Web-based sources
- Other structured data connectors

## Example Scenario

Every month Finance receives:

```text
Jan.xlsx
Feb.xlsx
Mar.xlsx
Apr.xlsx
```

Instead of manually copying data into one sheet:

```text
Data → Get Data → From Folder
```

Power Query can combine the files automatically.

Next month:

```text
Drop May.xlsx into folder
Refresh
```

The combined dataset updates.

## Common Transformations

### Remove Columns

Delete unnecessary fields.

### Change Data Type

Convert:

```text
Text → Date
Text → Number
```

### Split Column

Example:

```text
IND-MUM-001
```

split by `-`.

### Merge Columns

Combine fields.

### Replace Values

Standardize names.

### Trim

Remove excess spaces.

### Clean

Remove invalid characters.

### Fill Down

Useful in reports where labels appear only once.

### Unpivot

Convert:

| Product | Jan | Feb | Mar |
|---|---:|---:|---:|

into:

| Product | Month | Amount |
|---|---|---:|

This normalized form is better for analysis.

### Pivot

Reverse of unpivot.

### Merge Queries

Comparable to database joins.

Join types include:

```text
Left Outer
Right Outer
Full Outer
Inner
Left Anti
Right Anti
```

### Append Queries

Stack datasets vertically.

Equivalent conceptually to:

```text
UNION ALL
```

## Power Query Best Practices

- Keep raw source untouched.
- Use meaningful step names.
- Set data types explicitly.
- Remove unnecessary columns early.
- Build reusable transformations.
- Use parameters where useful.
- Load only what you need.

---

# 27. Data Model and Power Pivot

The Data Model allows Excel to work with multiple related tables rather than one giant flat table.

Example tables:

```text
Sales
Customer
Product
Date
Employee
```

Relationships:

```text
Customer[CustomerID] 1 ─── * Sales[CustomerID]

Product[ProductID]   1 ─── * Sales[ProductID]

Date[Date]           1 ─── * Sales[Date]
```

This structure is similar to relational database modeling.

## Why Use a Data Model?

Benefits:

- Avoid repeated master data
- Analyze larger datasets
- Create relationships
- Use DAX
- Create advanced PivotTables
- Build scalable dashboards

## Star Schema

Recommended analytical model:

```text
              Date
               |
Customer — Sales — Product
               |
             Region
```

The central transaction table is the **fact table**.

Lookup/master tables are **dimension tables**.

---

# 28. DAX Fundamentals

DAX is the formula language used in Power Pivot and related Microsoft analytical tools.

DAX looks similar to Excel formulas but works with data models and filter context.

## Calculated Column

Calculated row by row.

Example:

```DAX
Sales[LineAmount] =
Sales[Quantity] * Sales[UnitPrice]
```

## Measure

Calculated dynamically depending on report filters.

```DAX
Total Sales :=
SUM(Sales[Amount])
```

## Basic Measures

```DAX
Total Sales :=
SUM(Sales[Amount])
```

```DAX
Total Quantity :=
SUM(Sales[Quantity])
```

```DAX
Average Order Value :=
DIVIDE([Total Sales], DISTINCTCOUNT(Sales[InvoiceNo]))
```

## CALCULATE

One of the most important DAX functions.

```DAX
Mumbai Sales :=
CALCULATE(
    [Total Sales],
    Customer[City] = "Mumbai"
)
```

## DISTINCTCOUNT

```DAX
Customers :=
DISTINCTCOUNT(Sales[CustomerID])
```

## DIVIDE

Preferred over `/` for safer division.

```DAX
Margin % :=
DIVIDE([Profit],[Sales])
```

## Time Intelligence

A proper Date table enables calculations such as:

```DAX
Previous Year Sales :=
CALCULATE(
    [Total Sales],
    SAMEPERIODLASTYEAR('Date'[Date])
)
```

```DAX
YTD Sales :=
TOTALYTD(
    [Total Sales],
    'Date'[Date]
)
```

## Core DAX Concepts to Master

- Row context
- Filter context
- Context transition
- Measures
- Calculated columns
- CALCULATE
- FILTER
- ALL
- VALUES
- RELATED
- DISTINCTCOUNT
- Time intelligence

---

# 29. Dashboard Design

A dashboard provides decision-ready information at a glance.

Example executive dashboard:

```text
-----------------------------------------
Revenue        Profit        Margin %
₹12.5M         ₹2.4M         19.2%
-----------------------------------------
Monthly Revenue Trend
-----------------------------------------
Revenue by Region   Revenue by Product
-----------------------------------------
Top Customers
-----------------------------------------
Filters:
Year | Region | Product | Salesperson
-----------------------------------------
```

## Dashboard Elements

### KPI Cards

Examples:

```text
Revenue
Profit
Orders
Average Order Value
Pending Invoices
Outstanding Amount
```

### Trend Charts

Example:

```text
Monthly Sales
```

### Comparison Charts

Example:

```text
Actual vs Budget
```

### Slicers

Interactive filters.

## Dashboard Design Principles

1. Put important KPIs near the top.
2. Use consistent number formats.
3. Minimize unnecessary decoration.
4. Use the same date grain across visuals where possible.
5. Highlight exceptions.
6. Avoid too many charts.
7. Design for the question the dashboard should answer.

---

# 30. Financial and Accounting Use Cases

Excel is heavily used in Finance.

## Trial Balance Analysis

Columns:

```text
GL Code
GL Description
Opening
Debit
Credit
Closing
```

Closing:

```excel
=Opening+Debit-Credit
```

## Budget vs Actual

| Department | Budget | Actual |
|---|---:|---:|
| IT | 1,000,000 | 1,100,000 |

Variance:

```excel
=Actual-Budget
```

Variance %:

```excel
=IFERROR((Actual-Budget)/Budget,0)
```

## Accounts Payable Aging

Columns:

```text
Vendor
Invoice Date
Due Date
Outstanding
Age
Bucket
```

Age:

```excel
=MAX(0,TODAY()-C2)
```

Bucket:

```excel
=IFS(
E2<=30,"0-30",
E2<=60,"31-60",
E2<=90,"61-90",
TRUE,"90+"
)
```

## Reconciliation

ERP amount:

```text
₹100,000
```

Bank amount:

```text
₹99,999.50
```

Difference:

```excel
=A2-B2
```

Tolerance check:

```excel
=IF(ABS(A2-B2)<=1,"Matched","Mismatch")
```

## GST / Tax Calculation

Tax amount:

```excel
=ROUND(B2*C2,2)
```

Net:

```excel
=B2+D2
```

## Payment Due Date

```excel
=A2+30
```

or business days:

```excel
=WORKDAY(A2,30,Holidays)
```

---

# 31. HR and Payroll Use Cases

## Attendance Tracking

Columns:

```text
Employee ID
Employee Name
Date
In Time
Out Time
Hours
Status
```

Hours:

```excel
=E2-D2
```

Format as time.

## Attendance Status

```excel
=IF(F2>=TIME(8,30,0),"Present","Short Hours")
```

## Employee Tenure

```excel
=DATEDIF(DateOfJoining,TODAY(),"Y")
```

## Attrition Analysis

PivotTable:

```text
Rows   → Department
Values → Count of Employees
Filter → Status = Left
```

## Salary Increment

```excel
=CurrentSalary*(1+IncrementPercent)
```

## Bonus Eligibility

```excel
=IF(AND(Rating>=4,Tenure>=1),"Eligible","Not Eligible")
```

## Attendance Percentage

Suppose:

```text
B2 = Working Days
C2 = Present Days
```

Formula:

```excel
=IFERROR(C2/B2,0)
```

Format the result as Percentage.

**Input:** present days and working days.  
**Output:** attendance rate.  
**Why `IFERROR`:** protects the report when working days is zero or missing, but you should still investigate unexpected zero denominators instead of silently ignoring bad source data.

## Overtime Hours

If a policy counts only hours above 9:

```excel
=MAX(0,D2-9)
```

This returns `0` instead of a negative number when total hours are below the threshold.

## Payroll Design Practice

Keep these separate:

```text
Employee master
Attendance input
Pay components
Statutory/configuration rates
Calculation sheet
Payslip/report output
```

Avoid embedding changing tax, benefit, or payroll rules directly into many formulas. Put controlled assumptions in a clearly documented configuration table and have the workbook reviewed by the responsible payroll/finance team.


---

# 32. Sales and Operations Use Cases

## Sales Target Achievement

```excel
=Actual/Target
```

Formatted as percentage.

Status:

```excel
=IF(B2>=C2,"Achieved","Pending")
```

## Top Customer

```excel
=LARGE(CustomerTotals,1)
```

or use a PivotTable sorted descending.

## Month-over-Month Growth

```excel
=(CurrentMonth-PreviousMonth)/PreviousMonth
```

## Sales Pipeline

Columns:

```text
Opportunity
Stage
Deal Value
Probability
Expected Revenue
```

Expected Revenue:

```excel
=DealValue*Probability
```

Example:

```text
₹1,000,000 * 60% = ₹600,000
```

## SLA Tracking

```excel
=IF(ResolvedDate<=DueDate,"Within SLA","SLA Breach")
```

## Target Variance

```excel
=Actual-Target
```

Variance percentage:

```excel
=IFERROR((Actual-Target)/Target,0)
```

A positive number is not automatically "good" in every KPI. Higher cost, defect, or delay may be unfavorable, so define KPI direction explicitly.

## Weighted Sales Pipeline

If:

```text
C2 = Opportunity Value
D2 = Probability
```

then:

```excel
=C2*D2
```

can provide a simple weighted amount.

This is a planning estimate, not guaranteed revenue. Probability should come from a defined sales methodology rather than arbitrary user guesses.

## Conversion Rate

```excel
=IFERROR(WonDeals/QualifiedDeals,0)
```

Always state the denominator. "Conversion rate" is ambiguous unless the report says which stages are being compared.

## Operations Dashboard Pattern

Useful measures might include:

```text
Orders received
Orders fulfilled
Backlog
On-time %
Average cycle time
Exceptions older than SLA
```

Use PivotTables or the Data Model when users need to slice these measures by region, product, owner, or month.


---

# 33. Inventory and Procurement Use Cases

## Stock Balance

```excel
=Opening+Receipts-Issues
```

## Reorder Flag

```excel
=IF(CurrentStock<=ReorderLevel,"Reorder","OK")
```

## Inventory Value

```excel
=Quantity*UnitCost
```

## Purchase Price Variance

```excel
=ActualPrice-StandardPrice
```

## PO vs Invoice Check

```excel
=IF(ABS(POAmount-InvoiceAmount)<=Tolerance,"Match","Mismatch")
```

## Three-Way Match Concept

Typical comparison:

```text
Purchase Order
Goods Receipt
Invoice
```

Example checks:

```text
PO Quantity vs Received Quantity
Received Quantity vs Invoice Quantity
PO Price vs Invoice Price
```

Excel can be used to build exception reports where any mismatch is highlighted.

## Reorder Status

A simple rule:

```excel
=IF(CurrentStock<=ReorderPoint,"REORDER","OK")
```

Inputs:

- current usable stock,
- agreed reorder point.

Output:

- a status label.

A real reorder point may also consider lead time, demand variability, safety stock, open purchase orders, and reserved stock.

## Available Stock

```excel
=OnHand-Reserved
```

If open inbound quantity should be shown separately, do not automatically add it to physically available stock unless the business definition says so.

## Purchase Price Variance

```excel
=ActualPrice-StandardPrice
```

Percentage:

```excel
=IFERROR((ActualPrice-StandardPrice)/StandardPrice,0)
```

## Aging Open Purchase Orders

```excel
=IF(Status="Open",TODAY()-PODate,"")
```

Use conditional formatting or buckets to highlight old open items.

### Data-model warning

Do not store repeated supplier names, product descriptions, or categories independently in every transaction if a controlled master-data model is available. Use stable IDs and lookups/Power Query/Data Model relationships where appropriate.


---

# 34. Data Cleaning and Reconciliation

Real-world data is often messy.

Common issues:

```text
Extra spaces
Different capitalization
Duplicate records
Numbers stored as text
Inconsistent dates
Missing values
Different vendor naming
Leading/trailing symbols
Incorrect data types
```

## Clean Text

```excel
=UPPER(TRIM(CLEAN(A2)))
```

## Normalize Vendor Name

```excel
=SUBSTITUTE(
UPPER(TRIM(A2)),
" PRIVATE LIMITED",
" PVT LTD"
)
```

For large-scale standardization, maintain a mapping table.

## Find Duplicate IDs

```excel
=COUNTIF($A:$A,A2)>1
```

## Compare Two Lists

List A in A column.

List B in D column.

```excel
=IF(COUNTIF($D:$D,A2)>0,"Found","Missing")
```

Modern:

```excel
=IF(ISNUMBER(XMATCH(A2,$D:$D)),"Found","Missing")
```

## Reconciliation by Composite Key

Sometimes Invoice Number alone is not unique.

Create key:

```excel
=A2&"|"&B2&"|"&TEXT(C2,"0.00")
```

Example:

```text
Vendor|InvoiceNo|Amount
```

Then match keys across systems.

## Tolerance-Based Match

```excel
=IF(ABS(SystemA-SystemB)<=0.5,"Match","Mismatch")
```

---

# 35. Importing and Exporting Data

Excel regularly exchanges data with other systems.

## CSV

CSV is plain text with comma-separated values.

Important limitations:

- No formatting
- No formulas
- One table
- Leading zeros may be affected if opened carelessly
- Date interpretation may vary

## Text to Columns

Useful for delimited data.

Example:

```text
V001|ABC Ltd|Mumbai
```

Delimiter:

```text
|
```

## Get Data

For repeatable imports, prefer Power Query.

## Export

Possible outputs include:

- XLSX
- CSV
- PDF
- Text

Before exporting CSV, verify:

- Correct delimiter
- Character encoding
- Date format
- Decimal separator
- Leading-zero IDs

---

# 36. Protection, Security, and Collaboration

## Protect Sheet

Can prevent editing of cells.

Workflow:

1. Unlock input cells.
2. Leave formula cells locked.
3. Protect worksheet.

## Protect Workbook Structure

Can prevent:

- Adding sheets
- Deleting sheets
- Renaming sheets

## Hidden vs Very Hidden

VBA supports a `VeryHidden` sheet state, which users cannot unhide through the normal Excel UI.

Do not treat hidden sheets as real security.

## Password Protection

Workbook passwords provide some protection, but never use Excel as a replacement for proper enterprise security controls.

## Collaboration

Modern Excel supports shared editing in supported cloud environments.

Good collaborative practices:

- Avoid conflicting workbook copies.
- Maintain clear ownership.
- Use comments/notes appropriately.
- Use version history when available.
- Keep master data centralized.

---

# 37. Macros and VBA

Macros automate repetitive desktop Excel tasks.

## Macro Recorder

Use:

```text
View → Macros → Record Macro
```

Example automation:

1. Format report header
2. Autofit columns
3. Apply filters
4. Freeze panes
5. Set number formats

The recorder generates VBA.

## Basic VBA Macro

```vb
Sub HelloExcel()

    MsgBox "Hello Excel"

End Sub
```

## Write Value

```vb
Sub WriteValue()

    Range("A1").Value = "Completed"

End Sub
```

## Loop Through Rows

```vb
Sub CheckStatus()

    Dim lastRow As Long
    Dim i As Long

    lastRow = Cells(Rows.Count, "A").End(xlUp).Row

    For i = 2 To lastRow

        If Cells(i, "D").Value > 100000 Then
            Cells(i, "E").Value = "High Value"
        Else
            Cells(i, "E").Value = "Normal"
        End If

    Next i

End Sub
```

## Last Row

Common pattern:

```vb
lastRow = Cells(Rows.Count, "A").End(xlUp).Row
```

## Worksheet Object

```vb
Dim ws As Worksheet
Set ws = ThisWorkbook.Worksheets("Sales")
```

Then:

```vb
ws.Range("A1").Value = "Revenue"
```

## Error Handling

```vb
Sub Example()

    On Error GoTo ErrorHandler

    ' Code here

    Exit Sub

ErrorHandler:

    MsgBox Err.Description

End Sub
```

## VBA Best Practices

- Use `Option Explicit`.
- Avoid `Select` and `Activate`.
- Qualify worksheet references.
- Use meaningful variable names.
- Break large macros into procedures.
- Handle errors deliberately.
- Avoid hard-coded ranges when possible.
- Document business rules.

## `Sub` vs `Function`

A `Sub` performs actions and does not directly return a value to the caller.

```vb
Sub ClearInput()
    Range("B2:B10").ClearContents
End Sub
```

A VBA `Function` can accept parameters and return a value:

```vb
Function NetAmount(ByVal Gross As Double, ByVal Discount As Double) As Double
    NetAmount = Gross - Discount
End Function
```

Inputs:

```text
Gross
Discount
```

Return value:

```text
Gross - Discount
```

Use a worksheet formula when the logic is naturally cell calculation. Use VBA when you need procedural automation such as creating sheets, opening files, looping through workbook objects, or coordinating multiple actions.

### Workbook qualification matters

Risky:

```vb
Range("A1").Value = "Done"
```

It acts on the active sheet.

Safer:

```vb
ThisWorkbook.Worksheets("Sales").Range("A1").Value = "Done"
```

This makes the target explicit.

### Macro security

Macros can modify files and data. Keep macro-enabled files (`.xlsm`) from trusted sources only, sign/deploy code according to organizational policy, and never tell users to bypass security warnings simply to make a workbook run.


---

# 38. Office Scripts and Modern Automation

Office Scripts provide a TypeScript-based automation approach for supported Excel web environments.

Conceptual example:

```typescript
function main(workbook: ExcelScript.Workbook) {
    const sheet = workbook.getWorksheet("Sales");
    sheet.getRange("A1").setValue("Processed");
}
```

Potential scenarios:

- Format recurring reports
- Clean uploaded data
- Create recurring workbook transformations
- Integrate with workflow automation
- Process standardized templates

## VBA vs Office Scripts

| VBA | Office Scripts |
|---|---|
| Traditional Excel automation | Modern web-oriented automation |
| Visual Basic | TypeScript |
| Strong desktop integration | Stronger cloud workflow fit |
| Large legacy ecosystem | Modern automation ecosystem |

It is useful to know both if you work with enterprise Excel automation.

## `main` Function

An Office Script normally exposes a `main` function:

```typescript
function main(workbook: ExcelScript.Workbook) {
    // automation steps
}
```

**Input:** the current workbook object supplied by the Office Scripts runtime.  
**Output:** scripts can optionally return a value, but many automation scripts primarily modify workbook content.

Example with a returned value:

```typescript
function main(workbook: ExcelScript.Workbook): string {
    const sheet = workbook.getActiveWorksheet();
    return sheet.getName();
}
```

Use Office Scripts when your environment supports them and the workflow fits web/cloud automation. Use VBA when desktop object-model integration or a legacy VBA ecosystem is required. Neither is automatically "better"; platform, governance, deployment, and maintenance requirements decide.


---

# 39. Performance Optimization

Large workbooks can become slow.

## Common Causes

- Entire-column formulas across many rows
- Volatile functions
- Too many array calculations
- Excessive conditional formatting
- Repeated lookups
- External links
- Large Pivot caches
- Poorly designed VBA loops
- Huge used ranges

## Volatile Functions

Examples include functions such as:

```text
NOW
TODAY
OFFSET
INDIRECT
RAND
RANDBETWEEN
```

They may recalculate frequently.

## Better Formula Pattern

Instead of repeating:

```excel
=XLOOKUP(A2,Master!A:A,Master!D:D)
```

many times for the same row, consider:

- Helper columns
- LET
- Returning multiple fields where appropriate
- Power Query merges
- Data Model relationships

## VBA Optimization

Typical pattern:

```vb
Application.ScreenUpdating = False
Application.Calculation = xlCalculationManual

' Code

Application.Calculation = xlCalculationAutomatic
Application.ScreenUpdating = True
```

Always restore application state even when errors occur.

## Power Query Optimization

- Filter early.
- Remove unused columns early.
- Avoid unnecessary steps.
- Prefer source-side filtering where supported.
- Reuse staged queries carefully.

---

# 40. Common Excel Mistakes

## 1. Hard-Coding Numbers Inside Formulas

Bad:

```excel
=A2*0.18
```

Better:

```excel
=A2*$F$1
```

where F1 contains the tax rate.

Why?

Business rates can change.

## 2. Merged Cells in Raw Data

Merged cells make sorting, filtering, formulas, and Power Query harder.

## 3. One Sheet for Everything

Better structure:

```text
Raw
Master
Calculation
Report
Dashboard
```

## 4. Inconsistent Dates

Avoid mixing:

```text
01/02/2026
1-Feb-26
2026-02-01
Feb 1
```

Use one standard representation.

## 5. Numbers Stored as Text

Symptoms:

- SUM gives unexpected result
- Numbers align differently
- Lookup fails

Fix using:

```excel
=VALUE(A2)
```

or Power Query data-type conversion.

## 6. Using VLOOKUP Everywhere

Modern Excel often benefits from:

```text
XLOOKUP
XMATCH
INDEX/MATCH
Power Query Merge
Data Model relationships
```

Choose based on the problem.

## 7. No Error Handling

Instead of:

```excel
=A2/B2
```

for reporting:

```excel
=IFERROR(A2/B2,0)
```

But do not hide errors that should be investigated.

## 8. Copy-Paste Reporting Every Month

If the same transformation is repeated, consider:

```text
Power Query
PivotTables
Macros
Office Scripts
```

## 9. Too Many Colors

Formatting should encode meaning.

Example:

```text
Red    = exception
Amber  = warning
Green  = acceptable
```

## 10. No Data Validation

Free-text status fields often produce:

```text
Approved
approve
Aprroved
APPROVED
```

Use controlled lists.

---

# 41. Keyboard Shortcuts

Shortcuts significantly improve Excel speed.

| Shortcut | Purpose |
|---|---|
| `Ctrl + N` | New workbook |
| `Ctrl + O` | Open |
| `Ctrl + S` | Save |
| `Ctrl + P` | Print |
| `Ctrl + C` | Copy |
| `Ctrl + X` | Cut |
| `Ctrl + V` | Paste |
| `Ctrl + Z` | Undo |
| `Ctrl + Y` | Redo |
| `Ctrl + F` | Find |
| `Ctrl + H` | Replace |
| `Ctrl + A` | Select current region / all |
| `Ctrl + T` | Create Table |
| `Ctrl + E` | Flash Fill |
| `Ctrl + ;` | Current date |
| `Ctrl + Shift + ;` | Current time |
| `Ctrl + Arrow` | Jump to data edge |
| `Ctrl + Shift + Arrow` | Select to data edge |
| `Ctrl + Space` | Select column |
| `Shift + Space` | Select row |
| `Ctrl + 1` | Format Cells |
| `F2` | Edit active cell |
| `F4` | Toggle reference type / repeat action |
| `Alt + =` | AutoSum |
| `Ctrl + D` | Fill down |
| `Ctrl + R` | Fill right |
| `Ctrl + Shift + L` | Toggle filters |
| `Ctrl + PageUp` | Previous sheet |
| `Ctrl + PageDown` | Next sheet |
| `Ctrl + Home` | Go to A1 |
| `Ctrl + End` | Last used cell |
| `Ctrl + Shift + +` | Insert cells/rows/columns |
| `Ctrl + -` | Delete cells/rows/columns |

## Paste Special

Shortcut sequence can vary by environment, but learn the Paste Special menu for:

- Values
- Formulas
- Formats
- Transpose
- Multiply
- Divide

One of the most important operations is:

```text
Paste Values
```

because it replaces formulas with their current results.

---

# 42. Real-World Projects

Complete these projects in order.

## Project 1 — Expense Tracker

Columns:

```text
Date
Category
Description
Payment Method
Amount
```

Practice:

- SUM
- SUMIFS
- Tables
- Filters
- Conditional formatting
- Pie/column charts

## Project 2 — Sales Dashboard

Dataset:

```text
Date
Invoice
Customer
Region
Product
Quantity
Price
Revenue
Cost
Profit
```

Requirements:

- Revenue
- Profit
- Margin %
- Monthly trend
- Region comparison
- Product comparison
- Top 10 customers
- Slicers

Practice:

- Tables
- PivotTables
- PivotCharts
- GETPIVOTDATA or measures
- Dashboard layout

## Project 3 — Accounts Payable Aging

Fields:

```text
Vendor
Invoice No
Invoice Date
Due Date
Invoice Amount
Paid Amount
Outstanding
Age
Bucket
```

Build:

- Aging buckets
- Vendor summary
- Overdue list
- Outstanding KPI
- Top overdue vendors

## Project 4 — Reconciliation Tool

System A:

```text
Invoice
Vendor
Amount
```

System B:

```text
Invoice
Vendor
Amount
```

Requirements:

- Exact match
- Missing in A
- Missing in B
- Amount mismatch
- Tolerance match

Practice:

- XLOOKUP
- XMATCH
- ABS
- IF
- FILTER
- Conditional formatting

## Project 5 — Monthly File Consolidation

Input folder:

```text
Jan.xlsx
Feb.xlsx
Mar.xlsx
...
```

Use Power Query to:

- Read folder
- Combine files
- Clean columns
- Standardize types
- Remove blanks
- Load final table
- Refresh next month

## Project 6 — HR Attendance Dashboard

Fields:

```text
Employee
Department
Date
In Time
Out Time
Working Hours
Status
```

Build:

- Attendance %
- Late count
- Short-hours count
- Department summary
- Employee drill-down
- Monthly trend

## Project 7 — Inventory Reorder Model

Fields:

```text
SKU
Product
Opening
Receipts
Issues
Current Stock
Reorder Level
Lead Time
Average Daily Usage
```

Add:

```excel
=CurrentStock/AverageDailyUsage
```

for days of inventory.

Reorder rule:

```excel
=IF(CurrentStock<=ReorderLevel,"REORDER","OK")
```

## Project 8 — Power Pivot Business Model

Create:

```text
FactSales
DimCustomer
DimProduct
DimDate
DimRegion
```

Build relationships and measures:

```text
Total Sales
Total Profit
Margin %
Customers
Orders
YTD Sales
Previous Year Sales
Growth %
```

## Project 9 — Automated Monthly Report

Use either VBA or Office Scripts to:

- Refresh data
- Apply formatting
- Update report date
- Export output
- Clear temporary ranges

---

# 43. Excel Interview Questions

## Beginner

### What is a workbook?

An Excel file containing one or more worksheets.

### What is the difference between formula and function?

Formula:

```excel
=A1+B1
```

Function:

```excel
=SUM(A1:B1)
```

A formula can contain functions.

### What is an absolute reference?

A reference locked with `$`.

```excel
=$A$1
```

### Difference between COUNT and COUNTA?

`COUNT` counts numeric cells.

`COUNTA` counts non-empty cells.

## Intermediate

### VLOOKUP vs XLOOKUP?

XLOOKUP is generally more flexible:

- Exact match by default
- Can look left
- Supports not-found value
- More maintainable syntax

### SUMIF vs SUMIFS?

`SUMIF` supports one condition.

`SUMIFS` supports multiple conditions.

### What is a PivotTable?

A tool for dynamically grouping and aggregating data.

### What is a Table?

A structured dynamic Excel range with headers, filters, formatting, and structured references.

## Advanced

### Why use Power Query?

To create repeatable data ingestion and transformation workflows.

### What is the Data Model?

A relational analytical model containing multiple connected tables.

### Calculated column vs measure?

Calculated column:

- Stored per row
- Calculated during refresh/recalculation

Measure:

- Calculated based on current filter context
- Better for dynamic analysis

### What is CALCULATE?

A DAX function that evaluates an expression under modified filter context.

### What is a star schema?

A model where a central fact table connects to surrounding dimension tables.

### Why can OFFSET and INDIRECT hurt performance?

They are volatile and can force repeated recalculation.

### When should you use VBA instead of a formula?

When the task requires procedural automation, repetitive interaction with workbook objects, file operations, or actions beyond worksheet calculation.

---

# 44. Learning Roadmap

## Stage 1 — Beginner

Learn:

```text
Workbook navigation
Cell references
Formatting
Sorting
Filtering
Tables
Basic formulas
SUM
AVERAGE
COUNT
MIN
MAX
IF
```

Goal:

> Comfortably create clean spreadsheets and simple reports.

## Stage 2 — Intermediate

Learn:

```text
SUMIF/SUMIFS
COUNTIF/COUNTIFS
Text functions
Date functions
XLOOKUP
INDEX/MATCH
Conditional Formatting
Data Validation
PivotTables
Charts
```

Goal:

> Build business reports without manual calculations.

## Stage 3 — Advanced

Learn:

```text
Dynamic arrays
LET
LAMBDA
SUMPRODUCT
Advanced lookups
Advanced PivotTables
Power Query
What-If Analysis
Dashboard design
```

Goal:

> Build refreshable analytical workbooks.

## Stage 4 — Expert

Learn:

```text
Data Model
Power Pivot
DAX
Star schemas
Performance optimization
VBA
Office Scripts
Enterprise workbook architecture
```

Goal:

> Build scalable analytics and automation solutions.

---

# 45. Function Cheat Sheet

## Math

```excel
SUM()
SUMIF()
SUMIFS()
ROUND()
ROUNDUP()
ROUNDDOWN()
ABS()
INT()
MOD()
SUMPRODUCT()
SUBTOTAL()
AGGREGATE()
```

## Statistical

```excel
AVERAGE()
AVERAGEIF()
AVERAGEIFS()
COUNT()
COUNTA()
COUNTBLANK()
COUNTIF()
COUNTIFS()
MIN()
MAX()
MEDIAN()
LARGE()
SMALL()
RANK.EQ()
```

## Logical

```excel
IF()
IFS()
AND()
OR()
NOT()
SWITCH()
IFERROR()
IFNA()
```

## Text

```excel
LEFT()
RIGHT()
MID()
LEN()
TRIM()
CLEAN()
UPPER()
LOWER()
PROPER()
CONCAT()
TEXTJOIN()
FIND()
SEARCH()
SUBSTITUTE()
REPLACE()
TEXT()
VALUE()
TEXTBEFORE()
TEXTAFTER()
TEXTSPLIT()
```

## Date and Time

```excel
TODAY()
NOW()
DATE()
YEAR()
MONTH()
DAY()
EDATE()
EOMONTH()
DATEDIF()
DAYS()
NETWORKDAYS()
WORKDAY()
```

## Lookup

```excel
XLOOKUP()
XMATCH()
VLOOKUP()
HLOOKUP()
INDEX()
MATCH()
```

## Dynamic Arrays

```excel
FILTER()
UNIQUE()
SORT()
SORTBY()
SEQUENCE()
TAKE()
DROP()
CHOOSECOLS()
CHOOSEROWS()
VSTACK()
HSTACK()
```

## Advanced

```excel
LET()
LAMBDA()
OFFSET()
INDIRECT()
```

---

# 46. Final Mastery Checklist

Use this checklist to evaluate your Excel skill level.

## Core Fundamentals

- [ ] I understand workbook, worksheet, cell, range, row, and column concepts.
- [ ] I can enter and format data properly.
- [ ] I understand number, date, percentage, and custom formats.
- [ ] I can use relative references.
- [ ] I can use absolute references.
- [ ] I understand mixed references.
- [ ] I can create and use Excel Tables.

## Formula Skills

- [ ] I can write arithmetic formulas.
- [ ] I can use SUM, AVERAGE, MIN, and MAX.
- [ ] I can use COUNT, COUNTA, and COUNTBLANK.
- [ ] I can use SUMIF and SUMIFS.
- [ ] I can use COUNTIF and COUNTIFS.
- [ ] I can use IF, IFS, AND, and OR.
- [ ] I can handle errors with IFERROR and IFNA.
- [ ] I understand text functions.
- [ ] I understand date functions.
- [ ] I can build lookup formulas.
- [ ] I can use XLOOKUP.
- [ ] I understand INDEX/MATCH.
- [ ] I can use dynamic arrays.
- [ ] I can use LET.
- [ ] I understand the purpose of LAMBDA.

## Data Skills

- [ ] I can clean imported data.
- [ ] I can remove duplicates.
- [ ] I can find mismatches between two datasets.
- [ ] I can standardize text.
- [ ] I can convert data types.
- [ ] I can build data-validation lists.
- [ ] I can create conditional-formatting rules.
- [ ] I can sort and filter efficiently.

## Analysis

- [ ] I can create PivotTables.
- [ ] I can group dates in PivotTables.
- [ ] I can create calculated summaries.
- [ ] I can use slicers.
- [ ] I can build PivotCharts.
- [ ] I understand Goal Seek.
- [ ] I understand Scenario Manager.
- [ ] I understand Solver use cases.

## Visualization

- [ ] I know when to use line, column, bar, combo, waterfall, scatter, and histogram charts.
- [ ] I can design a readable chart.
- [ ] I can build KPI cards.
- [ ] I can design a usable dashboard.

## Power Query

- [ ] I can import CSV and Excel files.
- [ ] I can combine files from a folder.
- [ ] I can change data types.
- [ ] I can split and merge columns.
- [ ] I can pivot and unpivot data.
- [ ] I can merge queries.
- [ ] I can append queries.
- [ ] I can build refreshable pipelines.

## Data Model and DAX

- [ ] I understand fact and dimension tables.
- [ ] I understand one-to-many relationships.
- [ ] I understand star schema.
- [ ] I can create measures.
- [ ] I can use SUM and DISTINCTCOUNT in DAX.
- [ ] I understand CALCULATE.
- [ ] I understand filter context.
- [ ] I can create basic time-intelligence measures.

## Automation

- [ ] I can record a macro.
- [ ] I understand basic VBA syntax.
- [ ] I can loop through rows.
- [ ] I can work with worksheets and ranges in VBA.
- [ ] I understand VBA error handling.
- [ ] I understand the purpose of Office Scripts.
- [ ] I can identify tasks worth automating.

## Professional Excel Design

- [ ] I separate raw data, master data, calculations, and reports.
- [ ] I avoid merged cells in raw tables.
- [ ] I avoid unnecessary hard-coded values.
- [ ] I document important assumptions.
- [ ] I use consistent formatting.
- [ ] I optimize large workbooks.
- [ ] I understand when Excel is no longer the right tool.

---

# When Excel Is Not the Best Tool

Excel is extremely powerful, but it has limits.

Consider a database when:

- Multiple users continuously update the same structured data.
- Millions of transaction rows must be stored reliably.
- Data integrity and relationships are critical.
- Audit trails and permissions must be enforced centrally.

Consider Python/R when:

- Advanced statistical analysis is required.
- Large-scale automation is required.
- Reproducible code pipelines are more appropriate.
- Machine learning is involved.

Consider Power BI or another BI platform when:

- Dashboards must be shared at scale.
- Data models are large.
- Centralized refresh is required.
- Row-level security is required.
- Many business users need governed reports.

A strong Excel professional also knows **when not to use Excel**.

---

# Recommended Practice Dataset Structure

Create a workbook called:

```text
Excel_Practice_Master.xlsx
```

Suggested sheets:

```text
01_Basics
02_Formulas
03_Text
04_Dates
05_Lookups
06_DynamicArrays
07_Validation
08_ConditionalFormatting
09_Pivot
10_Charts
11_Reconciliation
12_Finance
13_HR
14_Inventory
15_PowerQuery
16_DataModel
17_Dashboard
18_VBA
19_Projects
```

Build examples yourself rather than only reading them.

A useful practice workbook should contain both **clean master data** and **imperfect transaction data** so you can practice validation and reconciliation.

Example transaction columns:

| Column | Example | Intended type |
|---|---|---|
| InvoiceNo | `INV-10025` | Text |
| VendorCode | `V0031` | Text |
| InvoiceDate | `14-Aug-2026` | Date |
| Department | `IT` | Text/category |
| Quantity | `5` | Number |
| UnitPrice | `1250.00` | Number/currency |
| Status | `Approved` | Controlled text |
| PaymentDate | blank or date | Date/blank |

Add a separate vendor master with `VendorCode`, `VendorName`, `Category`, and `IsActive`. Then deliberately create a few duplicates, missing codes, text-formatted numbers, and inconsistent names in a copy of the raw data. Use formulas, validation, Power Query, and PivotTables to clean and analyze it without modifying the original raw-data sheet.


---

# Suggested 30-Day Practice Plan

## Days 1–5

```text
Navigation
Formatting
Tables
References
Basic formulas
```

## Days 6–10

```text
IF
SUMIFS
COUNTIFS
Text functions
Date functions
```

## Days 11–15

```text
XLOOKUP
INDEX/MATCH
Dynamic arrays
Conditional formatting
Data validation
```

## Days 16–20

```text
PivotTables
PivotCharts
Charts
What-if analysis
Reconciliation
```

## Days 21–24

```text
Power Query
Merge
Append
Unpivot
Folder import
```

## Days 25–27

```text
Data Model
Power Pivot
DAX
Measures
```

## Days 28–30

```text
Dashboard
VBA
Office Scripts
Final project
```

## How to Use the Plan

Spend more time **building** than reading. A useful daily routine is:

```text
10 min  Review yesterday's concept
25 min  Rebuild one example without copying
15 min  Apply it to the practice dataset
10 min  Write down one mistake and how you fixed it
```

At the end of each week, rebuild one small report from a blank workbook. If you can explain why each formula, table, query, or chart exists, you are learning the model rather than memorizing clicks.


---

# Final Advice

To become genuinely strong in Excel, practice solving business problems instead of memorizing menus.

When you see a task, ask:

```text
1. Is the data clean?
2. Should this be a Table?
3. Can a formula solve it?
4. Would a PivotTable be simpler?
5. Is this transformation repeated?
6. Should Power Query automate it?
7. Does the data belong in a Data Model?
8. Is a dashboard actually necessary?
9. Is manual repetition indicating a need for automation?
10. Has the workbook become complex enough that another tool would be better?
```

The highest level of Excel skill is not knowing the largest number of functions.

It is being able to choose the **simplest, most reliable, maintainable solution** for the business problem.

---

# Quick Master Reference

```text
Need to add numbers?
→ SUM

Need conditional totals?
→ SUMIF / SUMIFS

Need conditional counts?
→ COUNTIF / COUNTIFS

Need logic?
→ IF / IFS / AND / OR

Need error handling?
→ IFERROR / IFNA

Need to find related data?
→ XLOOKUP

Need classic flexible lookup?
→ INDEX + MATCH

Need unique values?
→ UNIQUE

Need filtered result rows?
→ FILTER

Need sorted dynamic results?
→ SORT / SORTBY

Need clean imported text?
→ TRIM / CLEAN / SUBSTITUTE

Need reusable transformations?
→ Power Query

Need fast summary?
→ PivotTable

Need multiple related tables?
→ Data Model / Power Pivot

Need model calculations?
→ DAX measures

Need repeated desktop task automation?
→ VBA

Need modern web-oriented automation?
→ Office Scripts
```

---


# 47. Financial Functions

Excel contains dedicated functions for loans, investments, cash flows, and financial modeling.

## PMT — Loan Payment

Calculates periodic payment for a loan.

```excel
=PMT(rate,nper,pv)
```

Example:

```excel
=PMT(10%/12,60,-500000)
```

Meaning:

```text
Loan amount      = ₹500,000
Annual rate      = 10%
Monthly periods  = 60
```

The result is the approximate monthly payment.

## PV — Present Value

```excel
=PV(rate,nper,pmt)
```

Useful for finding today's value of future payments.

## FV — Future Value

```excel
=FV(rate,nper,pmt,pv)
```

Scenario:

> How much will a monthly investment grow to after 10 years?

## NPV

```excel
=NPV(rate,B2:B6)
```

Used for discounted cash-flow analysis.

Be careful with timing: Excel's `NPV` assumes the listed cash flows occur at regular periods after the initial date, so an initial investment at time zero is commonly handled separately.

## XNPV

For irregular dates:

```excel
=XNPV(rate,values,dates)
```

## IRR

```excel
=IRR(B2:B8)
```

Returns the internal rate of return for periodic cash flows.

## XIRR

Better when cash flows occur on irregular dates.

```excel
=XIRR(B2:B8,A2:A8)
```

## RATE

```excel
=RATE(nper,pmt,pv)
```

## NPER

```excel
=NPER(rate,pmt,pv)
```

Calculates the number of periods required.

## Business Practice

Build a loan model with:

```text
Principal
Interest Rate
Tenure
EMI
Opening Balance
Interest
Principal Repaid
Closing Balance
```

This teaches absolute references, dates, financial functions, and amortization.

## Sign Convention

Financial functions distinguish cash received from cash paid. A common model uses opposite signs for inflows and outflows.

For example:

```excel
=PMT(10%/12,60,500000)
```

usually returns a negative payment because the loan principal is treated as money received and periodic payments are money paid.

If you want a positive payment display, you may use:

```excel
=-PMT(10%/12,60,500000)
```

or pass the present value as negative, as shown earlier.

## Important Optional Arguments

Many financial functions support optional arguments such as:

- `fv` — desired future value,
- `type` — whether payments occur at end (`0`) or beginning (`1`) of a period,
- `guess` — starting estimate for iterative rate functions.

Always match the periodic interest rate to the period count. If `nper` is months, the rate should normally be a monthly rate too.

## `NPV` vs `XNPV`, `IRR` vs `XIRR`

Use periodic functions when cash flows are equally spaced. Use `XNPV`/`XIRR` when real dates are irregular.

Do not choose between them based only on convenience; timing assumptions materially affect financial results.


---

# 48. Statistical and Analytical Functions

These become important in analytical work.

## STDEV.S

Sample standard deviation:

```excel
=STDEV.S(B2:B100)
```

## STDEV.P

Population standard deviation:

```excel
=STDEV.P(B2:B100)
```

## VAR.S / VAR.P

Variance:

```excel
=VAR.S(B2:B100)
```

## PERCENTILE.INC

```excel
=PERCENTILE.INC(B2:B100,0.9)
```

Returns the 90th percentile.

## QUARTILE.INC

```excel
=QUARTILE.INC(B2:B100,1)
```

First quartile.

## CORREL

```excel
=CORREL(B2:B100,C2:C100)
```

Measures linear correlation.

Interpretation is roughly:

```text
+1   Strong positive relationship
 0   Little/no linear relationship
-1   Strong negative relationship
```

Correlation does not prove causation.

## MODE.SNGL

```excel
=MODE.SNGL(B2:B100)
```

Returns the most frequently occurring number.

## FREQUENCY

Useful for frequency distributions.

## FORECAST.LINEAR

```excel
=FORECAST.LINEAR(x,known_y,known_x)
```

## TREND

Returns values along a linear trend.

```excel
=TREND(known_y,known_x,new_x)
```

## Analysis ToolPak

Depending on your Excel installation, the Analysis ToolPak can provide tools such as:

```text
Descriptive Statistics
Regression
Correlation
Histogram
Moving Average
ANOVA
t-Test
z-Test
```

These tools are useful for analysts, but you should still understand the statistical concepts behind them.

## Choosing Sample vs Population Functions

Use:

```excel
=STDEV.S(range)
=VAR.S(range)
```

when your data is a sample used to estimate a larger population.

Use:

```excel
=STDEV.P(range)
=VAR.P(range)
```

when the range represents the entire population you intend to describe.

## Percentiles

```excel
=PERCENTILE.INC(array,k)
```

`k` is typically between `0` and `1`.

Example:

```excel
=PERCENTILE.INC(B2:B1000,0.9)
```

returns the value at the 90th percentile according to the inclusive method.

## Correlation Caution

`CORREL` returns a value between `-1` and `1` describing linear association. It does not tell you:

- whether one variable causes the other,
- whether the relationship is nonlinear,
- whether outliers are driving the result,
- whether the result is statistically meaningful for your decision.

Visualize the data and understand the business process before interpreting the coefficient.


---

# 49. Reference, Information, and Utility Functions

These functions are extremely useful in advanced workbook design.

## ROW

```excel
=ROW()
```

Returns current row number.

```excel
=ROW(A10)
```

returns:

```text
10
```

## COLUMN

```excel
=COLUMN()
```

## ROWS

```excel
=ROWS(A2:A100)
```

Returns number of rows in a range.

## COLUMNS

```excel
=COLUMNS(A:D)
```

## ADDRESS

```excel
=ADDRESS(5,3)
```

Returns a cell address such as:

```text
$C$5
```

## CHOOSE

```excel
=CHOOSE(2,"Low","Medium","High")
```

Result:

```text
Medium
```

## ISBLANK

```excel
=ISBLANK(A2)
```

## ISNUMBER

```excel
=ISNUMBER(A2)
```

## ISTEXT

```excel
=ISTEXT(A2)
```

## ISERROR

```excel
=ISERROR(A2)
```

## ISNA

```excel
=ISNA(A2)
```

## TYPE

Can help identify the underlying value type.

## FORMULATEXT

```excel
=FORMULATEXT(A2)
```

Returns the formula stored in a cell as text.

Useful for auditing and documentation.

## Why Information Functions Matter

These functions are often used to make formulas defensive.

Example:

```excel
=IF(ISNUMBER(A2),A2*1.18,"Check input")
```

The formula first checks the input type before calculating.

### Blank vs empty string

A formula that returns:

```excel
=""
```

looks blank but is not always equivalent to a truly empty cell. This matters for some counting, filtering, and downstream logic. Test the exact behavior your model requires.

### `FORMULATEXT`

`FORMULATEXT(reference)` returns the formula stored in the referenced cell as text. It is useful for documentation and auditing, but it does not evaluate that text as a formula.

### Volatility and indirect references

Functions such as `INDIRECT` and `OFFSET` can be useful but may make dependencies harder to trace and can contribute to recalculation overhead. Prefer direct references, Tables, `INDEX`, or modern dynamic-array patterns when they solve the same problem more transparently.


---

# 50. Printing, Page Layout, and Report Delivery

A workbook that looks good on screen may print badly.

## Page Layout Concepts

Learn:

```text
Orientation
Margins
Paper Size
Print Area
Page Breaks
Headers
Footers
Scaling
Repeat Header Rows
```

## Print Area

Select a report and define:

```text
Page Layout → Print Area → Set Print Area
```

## Print Titles

For multi-page tables, repeat headers on every printed page.

Example:

```text
Rows to repeat at top: $1:$2
```

## Scaling

Typical options:

```text
Fit Sheet on One Page
Fit All Columns on One Page
Fit All Rows on One Page
```

Avoid forcing a huge report onto one page because it can become unreadable.

## Header/Footer

Useful information:

```text
Company Name
Report Name
Confidential
Printed Date
Page X of Y
```

## Export to PDF

Before exporting:

1. Check print preview.
2. Confirm print area.
3. Confirm page orientation.
4. Confirm scaling.
5. Verify headers and footers.
6. Verify no columns are unexpectedly cut off.

---

# 51. View, Navigation, Grouping, and Large-Sheet Productivity

## Freeze Panes

Useful when a table has many rows or columns.

Common choices:

```text
Freeze Top Row
Freeze First Column
Freeze Panes
```

## Split

Creates separate scrollable areas in the same worksheet.

## Hide / Unhide

Rows, columns, and worksheets can be hidden.

Do not use hiding as a security mechanism.

## Group / Outline

Useful for hierarchical reports.

Example:

```text
Revenue
  Product Revenue
  Service Revenue
Expenses
  Payroll
  IT
  Travel
```

Rows can be grouped so users can expand or collapse detail.

## Go To

Shortcut:

```text
Ctrl + G
```

Useful for navigating to:

```text
A10000
Named ranges
Special cell types
```

## Go To Special

Very powerful for selecting:

```text
Blanks
Formulas
Constants
Visible cells only
Data validation
Conditional formatting
```

A particularly useful case is:

```text
Visible cells only
```

when copying filtered data.

---

# 52. Notes, Comments, Links, and Documentation

Complex workbooks require documentation.

## Notes

Useful for static explanatory annotations.

## Comments

In collaborative environments, comments can support threaded discussion.

## Hyperlinks

```excel
=HYPERLINK("https://example.com","Open")
```

You can also link between sheets.

Example concept:

```text
Dashboard → Detailed Report
```

## Documentation Sheet

For important workbooks, create a sheet such as:

```text
README
```

Include:

```text
Workbook purpose
Owner
Data sources
Refresh process
Business rules
Assumptions
Definitions
Version history
Known limitations
```

This is especially important when someone else may maintain the workbook later.

## Comments vs Notes

In modern Excel:

- **Comments** are threaded and designed for collaboration/replies.
- **Notes** are simple cell annotations similar to the older comment behavior.

Use a comment when discussion is expected. Use a note for a short explanation that does not need a conversation.

## Hyperlinks

A hyperlink can point to a web address, file, email target, or a location in the workbook.

For internal navigation, prefer meaningful labels:

```text
Go to assumptions
Open source documentation
View exception report
```

instead of displaying long raw URLs.

## Documentation Pattern

For important workbooks, document:

```text
Purpose
Owner
Source systems
Refresh process
Key assumptions
Critical formulas
Named ranges
Macros/scripts
Control totals
Known limitations
Change history
```

Good documentation is part of the workbook design, not an afterthought.


---

# 53. Sparklines, Icons, and In-Cell Visualization

## Sparklines

Small charts displayed inside cells.

Useful for:

```text
Monthly sales trend by customer
Daily stock movement
Attendance trend
KPI movement
```

Common sparkline types:

```text
Line
Column
Win/Loss
```

## Icon Sets

Conditional Formatting can show:

```text
↑
→
↓
```

for trends or status.

Example logic:

```text
Green ↑ = Above target
Amber → = Near target
Red ↓ = Below target
```

Icons should supplement numbers, not replace them.

## Sparklines

A sparkline is a tiny chart stored in a cell. It is useful for showing a trend beside a row without creating a full chart.

Good use:

```text
Product | Jan | Feb | Mar | Apr | Trend
A       |  10 |  12 |   9 |  15 | [sparkline]
```

Use sparklines for compact pattern recognition. Do not rely on them when exact values or detailed axes are required.

## Icon Sets and Data Bars

Conditional-formatting icon sets can classify values visually, while data bars show relative magnitude inside cells.

Always define the rule explicitly. A red/amber/green icon should not depend on arbitrary default thresholds when it represents a business KPI.

### Accessibility

Do not communicate status by color or icon alone. Pair visual indicators with text such as:

```text
Overdue
At Risk
On Track
```

so the meaning remains understandable for users who cannot distinguish the visual encoding.


---

# 54. Advanced Workbook Architecture

For important business workbooks, structure matters as much as formulas.

## Recommended Layered Design

```text
01_README
02_CONFIG
03_RAW
04_MASTER
05_TRANSFORMED
06_CALC
07_PIVOT
08_REPORT
09_DASHBOARD
```

## RAW Layer

Contains original source data.

Rule:

> Avoid manual editing whenever possible.

## MASTER Layer

Contains controlled dimensions:

```text
Vendor master
Customer master
Employee master
GL master
Department master
Status master
```

## CONFIG Layer

Stores assumptions:

```text
Tax Rate
Tolerance
Report Date
Financial Year
Thresholds
Folder Paths
```

Formulas should reference config values instead of embedding assumptions directly.

## TRANSFORMED Layer

Power Query outputs or normalized data.

## CALC Layer

Helper calculations and model logic.

## REPORT Layer

Detailed user-facing reports.

## DASHBOARD Layer

High-level visualization.

## Naming Convention

Example:

```text
tblSales
tblVendor
rngTaxRate
qryInvoice
ptRegionSales
```

Consistency makes a workbook easier to maintain.

---

# 55. Formula Design Patterns Worth Memorizing

## Status by Multiple Conditions

```excel
=IFS(
AND(B2="Approved",C2<=100000),"Ready",
B2="Rejected","Rejected",
C2>100000,"High Value Review",
TRUE,"Pending"
)
```

## Safe Percentage

```excel
=IFERROR(A2/B2,0)
```

## Aging Bucket

```excel
=LET(
age,MAX(0,TODAY()-C2),
IFS(
age<=30,"0-30",
age<=60,"31-60",
age<=90,"61-90",
TRUE,"90+"
))
```

## Lookup with Fallback

```excel
=XLOOKUP(A2,Vendor[Code],Vendor[Name],
         XLOOKUP(A2,LegacyVendor[Code],LegacyVendor[Name],"Not Found"))
```

## Case-Insensitive Presence Check

```excel
=ISNUMBER(SEARCH("invoice",A2))
```

## Exact Text Comparison

```excel
=EXACT(A2,B2)
```

## Extract Distinct Sorted List

```excel
=SORT(UNIQUE(A2:A1000))
```

## Filter Open Items

```excel
=FILTER(A2:F1000,F2:F1000="Open","No open records")
```

## Top 10 Records by Amount

```excel
=TAKE(SORTBY(A2:F1000,F2:F1000,-1),10)
```

## Combine Monthly Tables

```excel
=VSTACK(tblJan,tblFeb,tblMar)
```

## How to Adapt These Patterns

Treat every formula here as a **pattern**, not a copy-paste rule.

Before reusing one, identify:

1. **Inputs** — which cells, columns, or names the formula expects.
2. **Business rule** — what condition or transformation it represents.
3. **Return value** — number, text status, Boolean, or spilled array.
4. **Failure behavior** — what should happen for blanks, missing lookups, zeros, or errors.

For example, the safe percentage pattern:

```excel
=IFERROR(A2/B2,0)
```

returns `0` for *any* error, not only division by zero. In an audited model you may prefer:

```excel
=IF(B2=0,"",A2/B2)
```

so unexpected errors are not silently hidden.

Likewise, a lookup fallback should only return `"Not Found"` when that is the intended business outcome; missing master data may need an exception flag instead.


---

# 56. Auditing and Control Framework for Business Excel

Business spreadsheets often contain financial or operational decisions. Build controls into the workbook.

## Control Totals

Examples:

```text
Source Row Count
Loaded Row Count
Source Amount
Loaded Amount
Difference
```

Formula:

```excel
=SourceTotal-LoadedTotal
```

Expected:

```text
0
```

## Duplicate Control

```excel
=COUNTIFS(InvoiceNoRange,A2,VendorRange,B2)>1
```

## Missing Master Control

```excel
=IFNA(XLOOKUP(A2,Master[Code],Master[Name]),"MISSING MASTER")
```

## Balance Control

Example:

```excel
=ROUND(Debit-Credit,2)
```

Expected:

```text
0.00
```

## Reconciliation Status

```excel
=IF(ABS(SystemA-SystemB)<=Tolerance,"MATCH","REVIEW")
```

## Why Controls Matter

Without controls, a workbook can produce a polished report from incomplete data.

A strong Excel model validates:

```text
Completeness
Uniqueness
Accuracy
Validity
Reconciliation
```

before presenting results.

---

# 57. Expert-Level Questions to Ask Before Building

Before creating any important workbook, answer:

```text
What is the business question?

Who will use the workbook?

What are the source systems?

How much data will exist?

How frequently will it refresh?

Will users manually enter data?

What validations are required?

What controls prove completeness?

Which assumptions may change?

What should be configurable?

What should be automated?

Does the workbook require collaboration?

Does it contain sensitive information?

How will errors be surfaced?

Who will maintain it?

At what point should the solution move to a database,
Power BI, Python, or an application?
```

This mindset separates basic spreadsheet usage from professional Excel engineering.

---

# Extended Mastery Map

```text
LEVEL 1 — Spreadsheet User
  Navigation
  Formatting
  Basic formulas
  Sort/filter

LEVEL 2 — Business Excel User
  Tables
  IF
  SUMIFS
  Text/date functions
  XLOOKUP
  Conditional formatting
  Validation

LEVEL 3 — Analyst
  PivotTables
  Charts
  Dynamic arrays
  Reconciliation
  Statistical analysis
  What-if analysis

LEVEL 4 — Advanced Analyst
  Power Query
  Data modeling
  Dashboard design
  Advanced formula architecture
  Control frameworks

LEVEL 5 — Excel Developer / Expert
  Power Pivot
  DAX
  VBA
  Office Scripts
  Performance optimization
  Enterprise workbook architecture
```


**End of Excel Mastery Handbook**

## A Practical Definition of Mastery

You do not need to know every Excel feature. A strong practitioner can:

- choose a clean data structure before writing formulas,
- explain formula inputs and outputs,
- recognize when Tables/PivotTables/Power Query are better than manual work,
- design checks that prove data completeness and reconciliation,
- debug errors without random trial and error,
- build reports another person can maintain,
- automate only after the manual process is understood,
- recognize when the problem has outgrown Excel.

A useful final exercise is to take one real business process and implement it three ways—formula-based, Power Query/Pivot-based, and automated—then compare maintainability, refresh effort, risk, and scalability.

