# PostgreSQL Master Handbook

> **Beginner → Intermediate → Advanced → Production**
>
> A single-file learning handbook for understanding PostgreSQL from first principles through real-world database design, SQL, transactions, indexing, performance, security, backup/recovery, replication, administration, troubleshooting, and application development.

---

## Handbook status and version note

This handbook focuses on **durable PostgreSQL concepts** that remain useful across supported releases. Examples target modern PostgreSQL and version-sensitive material is separated from timeless fundamentals where practical.

As of **August 17, 2026**, PostgreSQL **18** is the current stable major version and **18.6** is its current minor release. PostgreSQL 19 is still a development/beta line, so PostgreSQL 19-only behavior is not treated as a production default in this handbook.

For production, do not stop at the first `.0` release of a major version. PostgreSQL minor releases contain bug, security, and data-corruption fixes, and the PostgreSQL project recommends running the current minor release for your chosen supported major version.

When a feature is especially version-sensitive, this handbook labels it explicitly. Always check the documentation for the exact server version you operate before using new syntax in production.

---

## Who this handbook is for

Use this handbook if you are:

- completely new to databases;
- learning SQL for backend or full-stack development;
- moving from MySQL, SQL Server, Oracle, or SQLite;
- preparing for interviews;
- maintaining PostgreSQL in development or production;
- learning query tuning and indexing;
- building APIs, reporting systems, financial systems, SaaS applications, data platforms, or internal enterprise applications.

You do **not** need previous PostgreSQL experience. Basic programming knowledge helps but is not required.

---

## How to use this handbook

Do not try to memorize every command. Learn in layers:

1. Understand relational database fundamentals.
2. Learn basic SQL and table design.
3. Practice joins, aggregation, subqueries, CTEs, and window functions.
4. Learn transactions, constraints, and concurrency.
5. Learn indexes and `EXPLAIN`.
6. Learn PostgreSQL-specific features such as `jsonb`, arrays, ranges, full-text search, generated columns, extensions, and row-level security.
7. Learn production topics: roles, backups, WAL, replication, vacuum, monitoring, configuration, upgrades, and troubleshooting.

For each topic, ask:

> **What is it? → Why do I need it? → How does it work? → How do I use it? → What can go wrong?**

---

# Table of Contents

1. [PostgreSQL in simple words](#1-postgresql-in-simple-words)
2. [Database fundamentals](#2-database-fundamentals)
3. [PostgreSQL architecture](#3-postgresql-architecture)
4. [Installation and first connection](#4-installation-and-first-connection)
5. [`psql` command-line client](#5-psql-command-line-client)
6. [SQL syntax fundamentals](#6-sql-syntax-fundamentals)
7. [Databases, schemas, tables, and namespaces](#7-databases-schemas-tables-and-namespaces)
8. [Data types](#8-data-types)
9. [Creating and altering tables](#9-creating-and-altering-tables)
10. [Constraints and data integrity](#10-constraints-and-data-integrity)
11. [INSERT, UPDATE, DELETE, and MERGE](#11-insert-update-delete-and-merge)
12. [SELECT fundamentals](#12-select-fundamentals)
13. [Filtering, sorting, pagination, and NULL](#13-filtering-sorting-pagination-and-null)
14. [Functions, operators, expressions, and CASE](#14-functions-operators-expressions-and-case)
15. [Joins](#15-joins)
16. [Aggregation and grouping](#16-aggregation-and-grouping)
17. [Subqueries](#17-subqueries)
18. [Common Table Expressions](#18-common-table-expressions)
19. [Set operations](#19-set-operations)
20. [Window functions](#20-window-functions)
21. [Views and materialized views](#21-views-and-materialized-views)
22. [Sequences, identity, and generated columns](#22-sequences-identity-and-generated-columns)
23. [Transactions and ACID](#23-transactions-and-acid)
24. [MVCC and concurrency](#24-mvcc-and-concurrency)
25. [Isolation levels](#25-isolation-levels)
26. [Locks and deadlocks](#26-locks-and-deadlocks)
27. [Indexes](#27-indexes)
28. [Query planner and EXPLAIN](#28-query-planner-and-explain)
29. [Statistics and ANALYZE](#29-statistics-and-analyze)
30. [VACUUM, autovacuum, bloat, and freeze](#30-vacuum-autovacuum-bloat-and-freeze)
31. [Partitioning](#31-partitioning)
32. [JSON and JSONB](#32-json-and-jsonb)
33. [Arrays](#33-arrays)
34. [Range and multirange types](#34-range-and-multirange-types)
35. [UUIDs](#35-uuids)
36. [Full-text search](#36-full-text-search)
37. [Functions and procedures](#37-functions-and-procedures)
38. [PL/pgSQL](#38-plpgsql)
39. [Triggers and event triggers](#39-triggers-and-event-triggers)
40. [Extensions](#40-extensions)
41. [Foreign Data Wrappers](#41-foreign-data-wrappers)
42. [COPY, import, and export](#42-copy-import-and-export)
43. [Roles, privileges, and security](#43-roles-privileges-and-security)
44. [Row-Level Security](#44-row-level-security)
45. [Authentication and `pg_hba.conf`](#45-authentication-and-pg_hbaconf)
46. [Configuration and memory](#46-configuration-and-memory)
47. [Connections and pooling](#47-connections-and-pooling)
48. [Write-Ahead Logging](#48-write-ahead-logging)
49. [Backup and restore](#49-backup-and-restore)
50. [Point-in-time recovery](#50-point-in-time-recovery)
51. [Physical replication and high availability](#51-physical-replication-and-high-availability)
52. [Logical replication](#52-logical-replication)
53. [Monitoring and system catalogs](#53-monitoring-and-system-catalogs)
54. [Logging and troubleshooting](#54-logging-and-troubleshooting)
55. [Upgrading PostgreSQL](#55-upgrading-postgresql)
56. [Application development patterns](#56-application-development-patterns)
57. [Database design and normalization](#57-database-design-and-normalization)
58. [Common anti-patterns](#58-common-anti-patterns)
59. [Performance tuning workflow](#59-performance-tuning-workflow)
60. [Real-world scenarios](#60-real-world-scenarios)
61. [PostgreSQL vs MySQL and SQL Server](#61-postgresql-vs-mysql-and-sql-server)
62. [Error-handling guide](#62-error-handling-guide)
63. [Useful `psql` and SQL cheat sheet](#63-useful-psql-and-sql-cheat-sheet)
64. [Interview and self-test questions](#64-interview-and-self-test-questions)
65. [Practice projects](#65-practice-projects)
66. [Learning roadmap](#66-learning-roadmap)
67. [PostgreSQL 18 highlights](#67-postgresql-18-highlights)
68. [Production checklist](#68-production-checklist)
69. [Official references](#69-official-references)

**Appendices**

- [Appendix A — A complete learning schema](#appendix-a--a-complete-learning-schema)
- [Appendix B — Debugging decision tree](#appendix-b--debugging-decision-tree)
- [Appendix C — SQL style guide](#appendix-c--sql-style-guide)
- [Appendix D — Glossary](#appendix-d--glossary)
- [Appendix E — Additional advanced PostgreSQL concepts](#appendix-e--additional-advanced-postgresql-concepts)

---

# 1. PostgreSQL in simple words

## What is PostgreSQL?

PostgreSQL, often shortened to **Postgres**, is an open-source database management system.

A database stores information. PostgreSQL gives applications a safe, structured, efficient way to:

- create data;
- read data;
- update data;
- delete data;
- enforce business rules;
- run complex queries;
- handle many users at the same time;
- recover after crashes;
- protect data with permissions;
- replicate data to other servers.

PostgreSQL is usually described as an **object-relational database management system (ORDBMS)**. For day-to-day learning, think of it primarily as a powerful relational database with many advanced data types and extensibility features.

## PostgreSQL vs SQL

These are not the same thing.

- **SQL** is a language used to work with relational databases.
- **PostgreSQL** is database software that understands SQL and adds PostgreSQL-specific features.

For example:

```sql
SELECT name
FROM customers
WHERE active = true;
```

That is SQL executed by PostgreSQL.

## Why developers choose PostgreSQL

Common reasons include:

- strong transactional correctness;
- rich SQL support;
- advanced indexing;
- `jsonb` for semi-structured data;
- window functions and analytical SQL;
- full-text search;
- geospatial support through extensions such as PostGIS;
- robust concurrency through MVCC;
- physical and logical replication;
- extensibility through functions, data types, operators, procedural languages, and extensions.

## Where PostgreSQL is used

Typical workloads include:

- e-commerce;
- banking and finance;
- ERP systems;
- SaaS products;
- authentication systems;
- APIs;
- analytics;
- geospatial applications;
- content management systems;
- audit and workflow systems;
- event and telemetry data;
- AI/ML metadata stores.

---

# 2. Database fundamentals

Before learning PostgreSQL syntax, understand the model.

## Database

A **database** is an organized collection of data.

Example database:

```text
shop_db
```

It may contain tables such as:

```text
customers
products
orders
order_items
payments
```

## Table

A table stores related records in rows and columns.

Example `customers` table:

| customer_id | name | email | active |
|---:|---|---|---|
| 1 | Aisha | aisha@example.com | true |
| 2 | Rahul | rahul@example.com | true |

## Row

A **row** represents one record.

For example:

```text
1 | Aisha | aisha@example.com | true
```

## Column

A **column** represents one attribute of the record.

Examples:

- `customer_id`
- `name`
- `email`
- `active`

Each column has a data type.

## Primary key

A primary key uniquely identifies a row.

```sql
customer_id bigint PRIMARY KEY
```

## Foreign key

A foreign key connects rows between tables.

```sql
customer_id bigint REFERENCES customers(customer_id)
```

## Relation

In relational theory, a table-like data set is a relation. In PostgreSQL documentation, **relation** may also refer more broadly to table-like storage objects such as tables and indexes depending on context.

## Schema

A schema is a namespace inside a database.

```text
Database: shop_db
  Schema: public
    Table: customers
  Schema: billing
    Table: invoices
```

## RDBMS

RDBMS means **Relational Database Management System**.

Important relational ideas:

- structured tables;
- keys;
- relationships;
- constraints;
- declarative queries;
- transactions.

## OLTP vs OLAP

### OLTP

Online Transaction Processing.

Examples:

- creating an order;
- booking a ticket;
- posting a payment;
- updating user profile data.

Typical characteristics:

- many short queries;
- high concurrency;
- frequent inserts and updates;
- strict correctness requirements.

### OLAP

Online Analytical Processing.

Examples:

- monthly revenue report;
- customer retention analysis;
- year-over-year trend report.

Typical characteristics:

- fewer but heavier queries;
- aggregations over many rows;
- larger scans;
- reporting or analytics focus.

PostgreSQL can support both, but architecture and tuning choices differ.

---

# 3. PostgreSQL architecture

Understanding the architecture makes later topics such as connections, memory, locks, WAL, and vacuum much easier.

## Client-server model

PostgreSQL normally runs as a server process.

```text
Application / psql / BI Tool
          |
          | TCP/IP or Unix socket
          v
    PostgreSQL Server
          |
          v
       Database
```

The client sends SQL. PostgreSQL parses, plans, executes, and returns results.

## PostgreSQL cluster

The word **cluster** can be confusing because PostgreSQL uses it differently from many cloud and distributed-system products.

In core PostgreSQL terminology, a **database cluster** is the complete set of databases managed by one PostgreSQL server instance and stored under one data directory. A freshly initialized cluster commonly contains databases such as `postgres`, `template0`, and `template1`, and you can create additional databases inside the same cluster.

It does **not** automatically mean a multi-server high-availability cluster.

A useful mental model is:

```text
One PostgreSQL server instance / data directory
    ├── database_a
    │     ├── schemas
    │     └── tables, indexes, functions, ...
    ├── database_b
    │     ├── schemas
    │     └── tables, indexes, functions, ...
    └── shared cluster-level objects/settings
          └── roles, some configuration, WAL, etc.
```

A client connection chooses one database in the cluster. Schemas organize objects **inside** that database.

## Main process concepts

A PostgreSQL installation contains a server process often called `postgres` plus background processes.

Important concepts include:

- client backend processes;
- checkpointer;
- background writer;
- WAL writer;
- autovacuum launcher/workers;
- replication processes;
- logical replication workers;
- optional parallel workers.

Exact process details vary with version and configuration.

## One connection, one backend concept

In PostgreSQL's traditional process model, each established client session is handled by a dedicated server backend process. The backend parses SQL, plans and executes statements, participates in transactions, and communicates results back to that client.

Conceptually:

```text
App connection 1 ──> backend process 1
App connection 2 ──> backend process 2
App connection 3 ──> backend process 3
```

This does **not** mean every backend is continuously consuming a CPU core. An idle backend can sleep while waiting for the next client command. However, every connection still has memory and operating-system/process overhead, and large numbers of active sessions can compete for CPU, locks, memory, and storage.

That is why simply increasing `max_connections` is not a complete scaling strategy. Web applications commonly use connection pools so many application requests can share a controlled number of database sessions. Connection pooling is covered in Chapter 47.

## Shared memory

Although client backends are separate processes, they must coordinate. PostgreSQL therefore uses shared-memory structures that all relevant server processes can access.

Important examples include:

- **shared buffers** — a PostgreSQL-managed cache of database pages;
- **lock tables** — coordination for heavyweight locks and related concurrency state;
- **WAL-related state** — information needed to coordinate durability and WAL processing;
- **process/session state** — structures used for communication and coordination between server processes.

`shared_buffers` is important, but it is not PostgreSQL's only cache. PostgreSQL also benefits from the operating system's filesystem cache. This is why production memory tuning must consider the whole machine rather than assuming every byte not assigned to `shared_buffers` is wasted.

## Data directory

The PostgreSQL data directory, often called `PGDATA`, contains the physical state of the database cluster. It includes relation storage, WAL-related directories/state, transaction-status information, and other files PostgreSQL needs to operate. Depending on packaging and operating system, some configuration files may be stored in or referenced from locations outside the data directory.

### Important safety rule

Do **not** manually open, rename, copy, or edit table/index files in the data directory as a way to change database contents. Their format and consistency are managed by PostgreSQL and are tied to WAL, transactions, checkpoints, catalogs, and version-specific storage rules.

Use SQL and supported administration tools for normal database changes, backups, restores, and upgrades.

If you need to discover the active data directory from SQL:

```sql
SHOW data_directory;
```

Treat the returned path as production infrastructure, not as ordinary application files.

---

# 4. Installation and first connection

Installation differs by operating system and packaging method.

## Common installation approaches

- official or vendor-provided Windows installer;
- Linux distribution packages;
- PostgreSQL community package repositories;
- Homebrew on macOS;
- containers for local development;
- managed database services in the cloud.

For production, use a supported release and keep current with minor updates.

## Confirm installation

```bash
psql --version
```

Example:

```text
psql (PostgreSQL) 18.6
```

## Connect

```bash
psql -h localhost -p 5432 -U postgres -d postgres
```

Parameters:

| Option | Meaning |
|---|---|
| `-h` | host |
| `-p` | port |
| `-U` | database user/role |
| `-d` | database name |

The default PostgreSQL TCP port is commonly `5432`.

## Create a learning database

Inside `psql`:

```sql
CREATE DATABASE learning_db;
```

Connect to it:

```text
\c learning_db
```

## First table

```sql
CREATE TABLE students (
    student_id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    name text NOT NULL,
    email text UNIQUE,
    joined_at timestamptz NOT NULL DEFAULT now()
);
```

Insert data:

```sql
INSERT INTO students (name, email)
VALUES ('Aisha Khan', 'aisha@example.com');
```

Read it:

```sql
SELECT * FROM students;
```

Possible output:

```text
 student_id |    name     |       email       |          joined_at
------------+-------------+-------------------+-------------------------------
          1 | Aisha Khan  | aisha@example.com | 2026-08-17 10:00:00+05:30
```

---

# 5. `psql` command-line client

`psql` is PostgreSQL's interactive command-line client.

It accepts both SQL commands and special `psql` meta-commands.

## SQL command

```sql
SELECT current_database();
```

SQL commands normally end with `;`.

## Meta-command

```text
\dt
```

Meta-commands begin with a backslash and do not use a semicolon.

## Essential `psql` commands

| Command | Purpose |
|---|---|
| `\l` | list databases |
| `\c dbname` | connect to a database |
| `\dn` | list schemas |
| `\dt` | list tables |
| `\d table_name` | describe a table |
| `\di` | list indexes |
| `\df` | list functions |
| `\du` | list roles |
| `\x` | toggle expanded display |
| `\timing` | show query execution time |
| `\conninfo` | show current connection info |
| `\q` | quit |
| `\?` | `psql` help |
| `\h SELECT` | SQL help for a command |

## Run a SQL file

From the shell:

```bash
psql -U postgres -d learning_db -f schema.sql
```

Inside `psql`:

```text
\i schema.sql
```

## Output to a file

```text
\o result.txt
SELECT * FROM students;
\o
```

## Expanded mode

Very useful for wide rows:

```text
\x
SELECT * FROM pg_stat_activity LIMIT 1;
```

---

# 6. SQL syntax fundamentals

## Statement termination

SQL statements are normally terminated with semicolons.

```sql
SELECT 1;
```

## Comments

Single line:

```sql
-- This is a comment
SELECT 1;
```

Block:

```sql
/*
  Multi-line comment
*/
SELECT 1;
```

## Keywords

SQL keywords are case-insensitive when unquoted.

These are equivalent:

```sql
select * from customers;
```

```sql
SELECT * FROM customers;
```

A common style is uppercase SQL keywords and lowercase object names.

## Identifiers

Unquoted identifiers are folded to lowercase by PostgreSQL.

```sql
CREATE TABLE CustomerOrders (...);
```

is effectively created as:

```text
customerorders
```

Quoted identifiers preserve case:

```sql
CREATE TABLE "CustomerOrders" (...);
```

Then you must keep quoting it:

```sql
SELECT * FROM "CustomerOrders";
```

### Best practice

Prefer simple lowercase `snake_case` names:

```text
customer_orders
invoice_items
created_at
```

Avoid quoted mixed-case identifiers unless you have a strong reason.

## String literals

```sql
SELECT 'PostgreSQL';
```

Escape a single quote by doubling it:

```sql
SELECT 'It''s PostgreSQL';
```

## Dollar-quoted strings

Useful for function bodies or strings containing many quotes:

```sql
SELECT $$It's easy to include 'quotes' here.$$;
```

## Type casts

Standard syntax:

```sql
SELECT CAST('123' AS integer);
```

PostgreSQL shorthand:

```sql
SELECT '123'::integer;
```

Both produce integer `123`.

---

# 7. Databases, schemas, tables, and namespaces

## Database boundary

A PostgreSQL server cluster may contain multiple databases.

```sql
CREATE DATABASE app_db;
```

Connections are made to one database at a time.

Cross-database queries are not handled like cross-schema queries. If you need external access, consider approaches such as foreign data wrappers or application-level integration.

## Schemas

Create a schema:

```sql
CREATE SCHEMA billing;
```

Create a table inside it:

```sql
CREATE TABLE billing.invoices (
    invoice_id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    amount numeric(12,2) NOT NULL
);
```

Query it:

```sql
SELECT * FROM billing.invoices;
```

## `public` schema

New databases commonly contain a schema named `public`.

For larger applications, separate schemas can improve organization and privilege management.

Example:

```text
app.users
sales.orders
billing.invoices
audit.events
```

## `search_path`

PostgreSQL uses `search_path` to resolve unqualified object names.

```sql
SHOW search_path;
```

Instead of:

```sql
SELECT * FROM billing.invoices;
```

you may be able to write:

```sql
SELECT * FROM invoices;
```

if `billing` is in the effective search path.

### Security warning

Do not casually add schemas writable by untrusted users to a privileged user's `search_path`. Object name resolution can become a security boundary.

---

# 8. Data types

Choosing the correct data type improves correctness, storage, indexing, validation, and clarity. A type is not merely a storage format: it tells PostgreSQL and future developers what values are valid and what operations make sense.

## Quick type-selection guide

| Need | Strong default | Why |
|---|---|---|
| whole-number count/ID | `integer` or `bigint` | exact integer arithmetic |
| money/rates requiring exact decimals | `numeric(p,s)` | exact decimal semantics |
| scientific/measurement approximation | `double precision` | fast floating-point arithmetic |
| ordinary variable-length text | `text` | no artificial length rule |
| text with a real maximum length rule | `varchar(n)` or `text` + `CHECK` | encodes the rule |
| yes/no/unknown state | `boolean` | clearer than `0/1` text conventions |
| calendar date | `date` | no time component |
| real-world instant | `timestamptz` | represents an absolute instant |
| local wall-clock date/time with no global instant | `timestamp` | intentionally zone-less |
| globally unique identifier | `uuid` | native UUID type and operators |
| queryable semi-structured document | `jsonb` | indexing and JSON operators |
| IP/network address | `inet` / `cidr` | validation and network operators |

A common beginner mistake is storing values as `text` just because text is flexible. Prefer a domain-appropriate type whenever the database should understand and validate the value.

## Numeric types

### Integer types

| Type | Storage | Range (approx.) | Typical use |
|---|---:|---:|---|
| `smallint` | 2 bytes | ±32 thousand | small bounded values |
| `integer` / `int` | 4 bytes | ±2.1 billion | common counters and IDs |
| `bigint` | 8 bytes | ±9.2 quintillion | large IDs/counters |

```sql
age integer
order_id bigint
```

Choose based on the **largest value the system may reach**, not the value it contains today. Changing an integer column's type later can be operationally expensive on a large table, so high-growth identifiers often use `bigint` from the start.

### Exact decimal: `numeric`

```sql
price numeric(12,2)
```

`numeric(12,2)` means up to 12 significant decimal digits in total, with 2 digits after the decimal point. A typical maximum positive value is `9999999999.99`.

Use `numeric` when exact decimal arithmetic matters, such as:

- prices and invoice totals;
- tax rates where decimal precision is contractual;
- accounting calculations;
- quantities whose decimal representation must not drift through binary floating-point approximation.

Example:

```sql
SELECT 0.1::numeric + 0.2::numeric;
```

Expected result:

```text
0.3
```

### Floating point

```sql
measurement double precision
```

`real` and `double precision` are approximate binary floating-point types. They are appropriate for many measurements, scientific calculations, coordinates, and statistical workloads where approximation is expected.

Do not use floating-point types for exact currency calculations unless the business intentionally accepts floating-point approximation.

## Character types

### `text`

```sql
name text NOT NULL
```

For most ordinary variable-length text, `text` is an excellent default in PostgreSQL.

### `varchar(n)`

```sql
country_code varchar(2)
```

Use a length limit when the limit is itself a real rule. Do not add arbitrary limits such as `varchar(255)` merely because another database or framework traditionally did so.

For example, if an internal reference may contain at most 30 characters:

```sql
reference_code varchar(30) NOT NULL
```

An alternative is to keep `text` and express a more meaningful rule explicitly:

```sql
reference_code text NOT NULL
    CHECK (char_length(reference_code) BETWEEN 1 AND 30)
```

### `char(n)`

`char(n)` has fixed-length, blank-padded semantics. Those semantics are rarely needed in modern application schemas. Do not choose it merely because a code has a fixed *maximum* length.

### `text` vs `varchar(n)` vs `char(n)`

| Type | Best use | Common mistake |
|---|---|---|
| `text` | ordinary text | assuming it is inherently slower than `varchar` |
| `varchar(n)` | a genuine maximum-length rule | using arbitrary legacy limits |
| `char(n)` | intentionally fixed-width, blank-padded semantics | using it for ordinary codes/names |

## Boolean

```sql
is_active boolean NOT NULL DEFAULT true
```

Queries:

```sql
WHERE is_active
```

or:

```sql
WHERE is_active = true
```

Prefer a real `boolean` over conventions such as `'Y'/'N'`, `'true'/'false'` text, or `0/1` when the domain is genuinely Boolean.

## Date and time

Date/time modeling deserves special care because a **calendar value**, a **wall-clock value**, and an **instant in time** are different concepts.

### `date`

```sql
birth_date date
```

Use for calendar dates that do not need a time-of-day.

### `time`

```sql
opening_time time
```

Use for a time-of-day when no date is needed. A store's recurring opening time is a common example.

### `timestamp`

`timestamp` means **timestamp without time zone**. It stores a date and clock time without representing a universal instant.

```sql
local_event_time timestamp
```

Use it when the value is intentionally a local/wall-clock value whose meaning should not be shifted by session time zone, such as "the store opens at 2026-12-01 09:00 local time" before a location/zone is applied elsewhere.

### `timestamptz`

`timestamptz` means **timestamp with time zone semantics** and is commonly the safer choice for real events that happened at a specific instant.

```sql
created_at timestamptz NOT NULL DEFAULT now()
```

Typical uses:

- record creation/update times;
- payment timestamps;
- audit events;
- login events;
- message/event timestamps.

### `timestamp` vs `timestamptz`

| Question | Prefer |
|---|---|
| "When did this event actually happen?" | `timestamptz` |
| "What local wall-clock value was entered, independent of a zone?" | `timestamp` |
| "What calendar day?" | `date` |

### Common misunderstanding

`timestamptz` does **not** store a named zone such as `Asia/Kolkata` with every value. PostgreSQL represents an absolute instant and displays it according to the session time zone.

If the original named zone itself is business data — for example a user's preferred zone or an event venue's zone — store that separately as text validated by the application/domain rules.

## Interval

```sql
SELECT interval '2 days 3 hours';
```

Useful for durations and date/time arithmetic.

Example:

```sql
SELECT timestamptz '2026-08-17 10:00+05:30' + interval '2 hours';
```

## UUID

```sql
id uuid PRIMARY KEY
```

PostgreSQL 18 includes `uuidv7()` for generating timestamp-ordered UUIDv7 values.

```sql
SELECT uuidv7();
```

UUIDs are useful when identifiers must be generated independently across systems or should not expose a simple sequential count. They are larger than integer keys, so choose them for architectural reasons rather than because they look more "modern."

## JSON and JSONB

```sql
metadata jsonb
```

`jsonb` is usually preferred when you need querying, indexing, containment operators, or repeated processing. `json` preserves the original input text more directly, while `jsonb` stores a decomposed binary representation optimized for database operations.

JSON is covered in depth later.

## Arrays

```sql
tags text[]
```

Example:

```sql
INSERT INTO articles (tags)
VALUES (ARRAY['postgresql', 'sql']);
```

Arrays are useful when a value is naturally a small collection belonging to one row. Do not use arrays to hide a relationship that needs independent rows, foreign keys, attributes, or many-to-many querying.

## Byte data

```sql
file_content bytea
```

`bytea` stores binary values inside PostgreSQL. For very large files, consider whether object/blob storage plus a database reference is a better architecture, especially when streaming, CDN delivery, or independent retention policies matter.

## Enum

```sql
CREATE TYPE order_status AS ENUM (
    'pending',
    'paid',
    'shipped',
    'cancelled'
);
```

Then:

```sql
status order_status NOT NULL
```

Enums can be useful for stable domain values. If values, labels, ordering, metadata, or workflows change frequently, a lookup table or `CHECK`-based design can be easier to evolve.

## Domain

A domain creates a reusable constrained type.

```sql
CREATE DOMAIN positive_amount AS numeric(12,2)
CHECK (VALUE >= 0);
```

Then:

```sql
amount positive_amount
```

Domains are useful when the **same scalar rule** should be reused across many tables without repeating the constraint.

## Network types

Examples:

```text
inet
cidr
macaddr
```

These types validate network values and provide network-aware operators. Prefer them over plain text when the application performs subnet or address logic.

## Geometric, range, multirange, and specialized types

PostgreSQL includes many additional native types. Use them when the domain naturally matches their semantics instead of flattening everything into text.

## Common type-design mistakes

### Storing dates or numbers as text

Bad:

```sql
amount text
invoice_date text
```

This makes validation, ordering, arithmetic, indexing, and comparisons harder or incorrect.

Better:

```sql
amount numeric(12,2)
invoice_date date
```

### Using a type that cannot represent future scale

A counter that may eventually exceed `integer` should be designed accordingly. Do not optimize away a few bytes if the likely result is a risky production type migration later.

### Confusing missing with empty

`NULL`, `''`, `0`, and `false` mean different things. Choose nullability and types to express the domain rather than using sentinel values such as `-1`, `'N/A'`, or `'0000-00-00'`.

### Choosing JSON for every flexible field

Flexibility is useful, but columns with stable semantics often deserve proper types, constraints, and indexes. Use `jsonb` for genuinely semi-structured attributes, not as an escape from schema design.


---

# 9. Creating and altering tables

## Basic `CREATE TABLE`

```sql
CREATE TABLE products (
    product_id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    sku text NOT NULL UNIQUE,
    name text NOT NULL,
    price numeric(12,2) NOT NULL CHECK (price >= 0),
    stock_qty integer NOT NULL DEFAULT 0 CHECK (stock_qty >= 0),
    created_at timestamptz NOT NULL DEFAULT now()
);
```

This single definition establishes:

- types;
- nullability;
- default values;
- uniqueness;
- primary key;
- validation rules.

## Add a column

```sql
ALTER TABLE products
ADD COLUMN description text;
```

## Drop a column

```sql
ALTER TABLE products
DROP COLUMN description;
```

Use destructive DDL carefully in production.

## Rename column

```sql
ALTER TABLE products
RENAME COLUMN name TO product_name;
```

## Change type

```sql
ALTER TABLE products
ALTER COLUMN stock_qty TYPE bigint;
```

If conversion is not automatic:

```sql
ALTER TABLE some_table
ALTER COLUMN code TYPE integer
USING code::integer;
```

## Set a default

```sql
ALTER TABLE products
ALTER COLUMN stock_qty SET DEFAULT 0;
```

## Set `NOT NULL`

```sql
ALTER TABLE products
ALTER COLUMN sku SET NOT NULL;
```

Before doing this on existing data, ensure no rows contain `NULL`.

## Drop table

```sql
DROP TABLE products;
```

With dependencies:

```sql
DROP TABLE products CASCADE;
```

### Warning about `CASCADE`

`CASCADE` can remove dependent objects. Do not use it blindly.

## Temporary tables

```sql
CREATE TEMP TABLE temp_ids (
    id bigint PRIMARY KEY
);
```

Temporary tables are session-scoped by default and are useful for intermediate work, imports, or complex procedures.

## Unlogged tables

```sql
CREATE UNLOGGED TABLE staging_events (
    id bigint,
    payload jsonb
);
```

Unlogged tables reduce WAL overhead but sacrifice crash safety and are not replicated through physical WAL in the same way as logged table data. Use them only when data can be recreated.

---

# 10. Constraints and data integrity

Constraints move important rules into the database so **every** application path, migration, script, and integration must obey them. Application validation is still useful for friendly error messages, but database constraints are the final integrity boundary.

## `NOT NULL`

```sql
email text NOT NULL
```

Use `NOT NULL` when absence is not a valid state. It is clearer and more efficient than inventing sentinel values such as `''`, `'unknown'`, `0`, or `-1`.

A column should be nullable only when `NULL` has a legitimate business meaning such as "not known yet" or "not applicable."

## `UNIQUE`

```sql
email text UNIQUE
```

A unique constraint prevents duplicate values according to PostgreSQL's uniqueness semantics and automatically creates a supporting unique B-tree index.

### Multiple-column uniqueness

```sql
UNIQUE (tenant_id, external_reference)
```

This means the pair must be unique. The same `external_reference` may appear in different tenants.

### `NULL` and uniqueness

By default, PostgreSQL treats null values as **distinct** for a unique constraint, so multiple rows may contain `NULL`.

When business rules require only one null-equivalent value, PostgreSQL supports:

```sql
UNIQUE NULLS NOT DISTINCT (email)
```

Choose intentionally. Do not assume every database product handles nulls in unique constraints the same way.

## Primary key

```sql
customer_id bigint PRIMARY KEY
```

A primary key is the table's declared row identifier. It implies uniqueness and non-nullability and automatically creates a unique B-tree index.

A table has one primary-key constraint, but it can also have additional business `UNIQUE` constraints:

```sql
customer_id bigint PRIMARY KEY,
email text NOT NULL UNIQUE
```

The surrogate ID identifies the row; the email uniqueness protects a separate business invariant.

## Foreign key

A foreign key ensures a referencing value points to an allowed row in another table (or another key in the same table).

```sql
CREATE TABLE orders (
    order_id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    customer_id bigint NOT NULL,
    CONSTRAINT fk_orders_customer
        FOREIGN KEY (customer_id)
        REFERENCES customers(customer_id)
);
```

### What PostgreSQL indexes automatically

The referenced primary/unique key already has an index because of its constraint. PostgreSQL does **not** automatically create an index on the referencing foreign-key column.

For frequently joined or deleted/updated parent rows, an index on the referencing side is often important:

```sql
CREATE INDEX idx_orders_customer_id
ON orders(customer_id);
```

Whether it is worthwhile still depends on workload and table size.

## Referential actions

```sql
REFERENCES customers(customer_id)
ON DELETE CASCADE
```

Common choices:

| Action | Meaning | Typical use |
|---|---|---|
| `NO ACTION` | reject a violation, with normal/deferrable timing semantics | safe default |
| `RESTRICT` | prevent the referenced change immediately under its semantics | strict parent protection |
| `CASCADE` | propagate delete/update to referencing rows | owned child rows |
| `SET NULL` | set referencing column(s) to `NULL` | optional relationship |
| `SET DEFAULT` | set referencing column(s) to their defaults | only when that default remains valid |

### Example: owned line items

Deleting an order should usually delete its line items because the line items have no independent meaning:

```sql
CREATE TABLE order_items (
    order_item_id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    order_id bigint NOT NULL
        REFERENCES orders(order_id)
        ON DELETE CASCADE,
    product_id bigint NOT NULL REFERENCES products(product_id),
    quantity integer NOT NULL CHECK (quantity > 0)
);
```

But deleting a customer and automatically deleting years of financial orders may be inappropriate. Referential action is a **business rule**, not a convenience switch.

## Check constraint

A `CHECK` constraint validates a Boolean expression for each affected row.

```sql
CHECK (price >= 0)
```

Multiple columns:

```sql
CHECK (end_date IS NULL OR end_date >= start_date)
```

### Important `NULL` behavior

A `CHECK` constraint succeeds when its expression is `TRUE` **or `NULL`/unknown**. It fails only when the expression is `FALSE`.

Therefore:

```sql
price numeric CHECK (price > 0)
```

still allows `price = NULL`. If a value is required, combine the rules:

```sql
price numeric NOT NULL CHECK (price > 0)
```

### Do not use `CHECK` for cross-row or cross-table invariants

A `CHECK` expression is intended to validate the current row. Rules such as "no two active reservations overlap" or "this value must exist in another table" belong to mechanisms designed for cross-row relationships:

- `UNIQUE`;
- foreign keys;
- exclusion/temporal constraints;
- carefully designed triggers when no declarative constraint fits.

Using a row `CHECK` to query other rows can create dump/restore and consistency problems.

## Named constraints

Named constraints make errors, migrations, and application handling clearer:

```sql
CONSTRAINT chk_product_price_nonnegative
CHECK (price >= 0)
```

The name appears in PostgreSQL error diagnostics, which makes it easier to map a violation to a business rule.

## Exclusion constraints

PostgreSQL can enforce rules beyond simple equality uniqueness.

Classic example: prevent overlapping room reservations.

```sql
CREATE EXTENSION IF NOT EXISTS btree_gist;

CREATE TABLE room_bookings (
    room_id bigint NOT NULL,
    period tstzrange NOT NULL,
    EXCLUDE USING gist (
        room_id WITH =,
        period WITH &&
    )
);
```

Meaning: for the same room, booking periods may not overlap.

This is a powerful PostgreSQL feature for scheduling, allocation, and effective-dated systems because it prevents races that an application-level "check then insert" can miss.

## Deferrable constraints

Some constraints can be checked at transaction end instead of after each statement.

Useful for complex transactional reshuffling where intermediate states temporarily violate a rule but the final committed state is valid.

```sql
UNIQUE (position)
DEFERRABLE INITIALLY DEFERRED
```

You can also change the timing of a deferrable constraint within a transaction using `SET CONSTRAINTS`.

Not every constraint type is deferrable. In PostgreSQL, `UNIQUE`, `PRIMARY KEY`, `EXCLUDE`, and foreign-key constraints can use deferrability; ordinary `NOT NULL` and `CHECK` constraints are not made deferrable this way.

## Constraint design checklist

For each important column/table ask:

1. Can this value be missing? If not, use `NOT NULL`.
2. Must this value or combination be unique? Use `UNIQUE`.
3. What identifies one row? Declare a primary key.
4. Does this value reference another entity? Use a foreign key.
5. Is there a same-row numerical/date rule? Use `CHECK`.
6. Is the rule about overlap or ranges? Consider exclusion/temporal constraints.
7. What should happen when a parent is deleted or its key changes?
8. Should the rule be checked immediately or at transaction end?
9. Does the referencing foreign key need an index for the workload?

The strongest design is usually the one that makes invalid states difficult or impossible to commit.


---

# 11. INSERT, UPDATE, DELETE, and MERGE

These commands change rows.

## INSERT one row

```sql
INSERT INTO products (sku, name, price)
VALUES ('KB-001', 'Mechanical Keyboard', 4999.00);
```

## INSERT multiple rows

```sql
INSERT INTO products (sku, name, price)
VALUES
    ('MS-001', 'Wireless Mouse', 1299.00),
    ('HD-001', 'USB-C Hub', 2499.00);
```

## `RETURNING`

`RETURNING` makes a data-changing statement return columns or expressions from the rows it affected. It is available with `INSERT`, `UPDATE`, `DELETE`, and `MERGE` and often eliminates a race-prone follow-up `SELECT`.

### Insert and return generated values

```sql
INSERT INTO products (sku, name, price)
VALUES ('MON-001', '27-inch Monitor', 18999.00)
RETURNING product_id, sku, created_at;
```

Typical output:

```text
 product_id |   sku   |      created_at
------------+---------+------------------------
        101 | MON-001 | 2026-08-17 13:30:00+05:30
```

### Update and return the new state

```sql
UPDATE products
SET price = price * 1.05
WHERE product_id = 101
RETURNING product_id, price;
```

### PostgreSQL 18: return old and new values

PostgreSQL 18 lets DML `RETURNING` expressions explicitly refer to `old` and `new` row values. This is useful for audit output and change calculations without a second read.

```sql
UPDATE products
SET price = price * 1.10
WHERE price <= 99.99
RETURNING
    name,
    old.price AS old_price,
    new.price AS new_price,
    new.price - old.price AS price_change;
```

For a normal `INSERT`, the old row is normally null; for a normal `DELETE`, the new row is normally null. `UPDATE` can naturally expose both states. Conflict-handling and `MERGE` cases can have additional semantics, so test the exact statement shape you use.

### When to use it

Use `RETURNING` when the application needs:

- generated identity/UUID values;
- server defaults such as timestamps;
- the final value after an update;
- a deleted row for logging or downstream handling;
- old/new change information in PostgreSQL 18.

## UPSERT with `ON CONFLICT`

```sql
INSERT INTO inventory (product_id, stock_qty)
VALUES (10, 5)
ON CONFLICT (product_id)
DO UPDATE
SET stock_qty = inventory.stock_qty + EXCLUDED.stock_qty;
```

`EXCLUDED` refers to the row that was proposed for insertion.

### `DO NOTHING`

```sql
INSERT INTO users (email)
VALUES ('a@example.com')
ON CONFLICT (email) DO NOTHING;
```

## UPDATE

```sql
UPDATE products
SET price = 4599.00
WHERE sku = 'KB-001';
```

### Critical warning

Without `WHERE`:

```sql
UPDATE products
SET price = 0;
```

updates **every row**.

Before a risky update, preview the target rows:

```sql
SELECT *
FROM products
WHERE sku = 'KB-001';
```

## UPDATE with expression

```sql
UPDATE products
SET price = round(price * 1.05, 2)
WHERE active = true;
```

## UPDATE from another table

```sql
UPDATE products p
SET price = s.new_price
FROM price_staging s
WHERE s.sku = p.sku;
```

## DELETE

```sql
DELETE FROM products
WHERE product_id = 100;
```

Without `WHERE`, every row is deleted.

## `TRUNCATE`

```sql
TRUNCATE TABLE staging_events;
```

`TRUNCATE` removes all rows efficiently but has different locking, trigger, identity, and transactional characteristics from ordinary `DELETE`. Do not treat it as merely a faster `DELETE` without understanding those differences.

Reset identity values when appropriate:

```sql
TRUNCATE TABLE staging_events RESTART IDENTITY;
```

## MERGE

`MERGE` expresses conditional insert/update/delete logic based on matches between a target and a source.

Example:

```sql
MERGE INTO inventory AS i
USING incoming_inventory AS s
ON i.product_id = s.product_id
WHEN MATCHED THEN
    UPDATE SET stock_qty = s.stock_qty
WHEN NOT MATCHED THEN
    INSERT (product_id, stock_qty)
    VALUES (s.product_id, s.stock_qty);
```

### `MERGE` vs `INSERT ... ON CONFLICT`

Use `ON CONFLICT` when the operation is naturally an insert with uniqueness conflict handling.

Use `MERGE` when you need richer source-to-target matching and multiple conditional actions.

---

# 12. SELECT fundamentals

`SELECT` reads data.

## Select all columns

```sql
SELECT *
FROM products;
```

Useful for exploration, but production queries should often select only needed columns.

## Select specific columns

```sql
SELECT product_id, name, price
FROM products;
```

## Alias

```sql
SELECT
    name AS product_name,
    price AS unit_price
FROM products;
```

## Expressions

```sql
SELECT
    name,
    price,
    price * 1.18 AS price_with_tax
FROM products;
```

## Constants

```sql
SELECT 1;
SELECT now();
SELECT current_database();
```

## `DISTINCT`

```sql
SELECT DISTINCT country
FROM customers;
```

## PostgreSQL-specific `DISTINCT ON`

Get one selected row per group:

```sql
SELECT DISTINCT ON (customer_id)
    customer_id,
    order_id,
    created_at
FROM orders
ORDER BY customer_id, created_at DESC;
```

This returns the first row for each `customer_id` according to the `ORDER BY` order.

Typical use: latest order per customer.

### Important

The chosen row depends on ordering. Always use a deterministic `ORDER BY` when the exact row matters.

---
# 13. Filtering, sorting, pagination, and NULL

## WHERE

```sql
SELECT product_id, name, price
FROM products
WHERE price >= 2000;
```

## Multiple conditions

```sql
SELECT *
FROM products
WHERE price >= 2000
  AND stock_qty > 0;
```

```sql
SELECT *
FROM products
WHERE category = 'keyboard'
   OR category = 'mouse';
```

## Parentheses matter

```sql
WHERE active = true
  AND (category = 'keyboard' OR category = 'mouse')
```

Do not rely on memory of operator precedence for complex conditions. Parentheses improve clarity.

## IN

```sql
SELECT *
FROM orders
WHERE status IN ('paid', 'shipped');
```

Equivalent to multiple `OR` comparisons.

## BETWEEN

```sql
SELECT *
FROM products
WHERE price BETWEEN 1000 AND 5000;
```

`BETWEEN` is inclusive at both ends.

## LIKE

```sql
SELECT *
FROM customers
WHERE name LIKE 'A%';
```

Patterns:

- `%` = zero or more characters;
- `_` = exactly one character.

## ILIKE

PostgreSQL provides case-insensitive pattern matching:

```sql
SELECT *
FROM customers
WHERE name ILIKE 'a%';
```

## Regular expressions

```sql
SELECT *
FROM users
WHERE username ~ '^[a-z][a-z0-9_]+$';
```

Useful operators include:

- `~` case-sensitive regex match;
- `~*` case-insensitive regex match;
- `!~` not matching;
- `!~*` case-insensitive not matching.

## ORDER BY

```sql
SELECT name, price
FROM products
ORDER BY price ASC;
```

Descending:

```sql
ORDER BY price DESC;
```

Multiple keys:

```sql
ORDER BY category ASC, price DESC;
```

## NULL ordering

```sql
ORDER BY shipped_at DESC NULLS LAST;
```

Explicit null ordering is clearer than relying on defaults.

## LIMIT

```sql
SELECT *
FROM products
ORDER BY product_id
LIMIT 20;
```

## OFFSET

```sql
SELECT *
FROM products
ORDER BY product_id
LIMIT 20 OFFSET 40;
```

This returns a page after skipping 40 rows.

### OFFSET pagination problem

Large offsets become increasingly inefficient and can produce inconsistent page boundaries when data changes between requests.

For large systems, prefer **keyset pagination**.

```sql
SELECT product_id, name
FROM products
WHERE product_id > 5000
ORDER BY product_id
LIMIT 20;
```

For descending time-based pagination:

```sql
SELECT order_id, created_at
FROM orders
WHERE (created_at, order_id) < ($1, $2)
ORDER BY created_at DESC, order_id DESC
LIMIT 50;
```

The second key makes ordering deterministic when timestamps tie.

## NULL explained

`NULL` means missing, unknown, or not applicable. It is not the same as:

- `0`;
- empty string `''`;
- `false`;
- the text `'NULL'`.

This is wrong:

```sql
WHERE deleted_at = NULL
```

Use:

```sql
WHERE deleted_at IS NULL
```

or:

```sql
WHERE deleted_at IS NOT NULL
```

## Three-valued logic

Comparisons involving `NULL` often produce `UNKNOWN`, not `TRUE` or `FALSE`.

```sql
SELECT 10 = NULL;
```

Result is `NULL`/unknown.

This is why null-aware operators matter.

## `IS DISTINCT FROM`

A null-safe comparison:

```sql
SELECT 1 IS DISTINCT FROM NULL;
```

Returns `true`.

```sql
SELECT NULL IS DISTINCT FROM NULL;
```

Returns `false`.

This is useful when you want `NULL` to behave like a comparable value for equality-style logic.

---

# 14. Functions, operators, expressions, and CASE

PostgreSQL contains a large function and operator library. The goal is not memorization; learn the major families.

## String functions

```sql
SELECT lower('PostgreSQL');
SELECT upper('postgresql');
SELECT length('Postgres');
SELECT trim('  hello  ');
SELECT substring('PostgreSQL' FROM 1 FOR 4);
SELECT replace('a-b-c', '-', '/');
```

Example output:

```text
postgresql
POSTGRESQL
8
hello
Post
a/b/c
```

## Concatenation

```sql
SELECT first_name || ' ' || last_name AS full_name
FROM customers;
```

`concat()` handles nulls differently and can sometimes be more convenient:

```sql
SELECT concat(first_name, ' ', last_name);
```

## Numeric functions

```sql
SELECT round(12.345::numeric, 2);
SELECT ceil(10.1);
SELECT floor(10.9);
SELECT abs(-5);
SELECT power(2, 8);
```

## Date/time functions

```sql
SELECT now();
SELECT current_date;
SELECT current_timestamp;
```

Add an interval:

```sql
SELECT now() + interval '7 days';
```

Extract a field:

```sql
SELECT extract(year FROM current_date);
```

Truncate time:

```sql
SELECT date_trunc('month', now());
```

Useful for monthly reporting.

## `age()`

```sql
SELECT age(date '2026-08-17', date '2000-01-01');
```

This produces a calendar-style interval, not merely a number of seconds.

## COALESCE

Returns the first non-null expression.

```sql
SELECT COALESCE(phone, mobile, 'No phone')
FROM customers;
```

Common reporting example:

```sql
SELECT
    invoice_id,
    COALESCE(discount, 0) AS discount
FROM invoices;
```

## NULLIF

Returns `NULL` when two expressions are equal.

```sql
SELECT amount / NULLIF(quantity, 0)
FROM order_items;
```

This can help avoid division by zero.

## CASE

```sql
SELECT
    name,
    price,
    CASE
        WHEN price < 1000 THEN 'budget'
        WHEN price < 5000 THEN 'mid-range'
        ELSE 'premium'
    END AS price_band
FROM products;
```

## Simple CASE

```sql
SELECT
    status,
    CASE status
        WHEN 'P' THEN 'Pending'
        WHEN 'A' THEN 'Approved'
        WHEN 'R' THEN 'Rejected'
        ELSE 'Unknown'
    END AS status_label
FROM requests;
```

## Greatest and least

```sql
SELECT GREATEST(10, 20, 5);
SELECT LEAST(10, 20, 5);
```

## Type conversion

```sql
SELECT '2026-08-17'::date;
SELECT 123::text;
```

### Avoid unnecessary casts on indexed columns

A query like:

```sql
WHERE order_id::text = '123'
```

may prevent straightforward use of an index on `order_id`.

Prefer converting the parameter to the column's type:

```sql
WHERE order_id = '123'::bigint
```

---

# 15. Joins

Joins combine related rows from multiple tables.

Assume:

```text
customers
---------
customer_id
name

orders
------
order_id
customer_id
order_total
```

## INNER JOIN

Returns matching rows from both sides.

```sql
SELECT
    o.order_id,
    c.name,
    o.order_total
FROM orders o
JOIN customers c
  ON c.customer_id = o.customer_id;
```

Use when you only want rows that have a match.

## LEFT JOIN

Returns all rows from the left table plus matching rows from the right.

```sql
SELECT
    c.customer_id,
    c.name,
    o.order_id
FROM customers c
LEFT JOIN orders o
  ON o.customer_id = c.customer_id;
```

Customers without orders still appear, with `NULL` for order columns.

### Find customers with no orders

```sql
SELECT c.*
FROM customers c
LEFT JOIN orders o
  ON o.customer_id = c.customer_id
WHERE o.order_id IS NULL;
```

An equivalent and often clearer anti-join is `NOT EXISTS`:

```sql
SELECT c.*
FROM customers c
WHERE NOT EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

## RIGHT JOIN

Returns all rows from the right table plus matches from the left.

It is valid SQL, but many teams prefer rewriting as a `LEFT JOIN` by swapping table order for readability.

## FULL OUTER JOIN

Returns matched rows plus unmatched rows from both sides.

```sql
SELECT *
FROM source_a a
FULL JOIN source_b b
  ON b.code = a.code;
```

Useful for reconciliation.

## CROSS JOIN

Produces every combination.

```sql
SELECT s.size, c.color
FROM sizes s
CROSS JOIN colors c;
```

If there are 5 sizes and 4 colors, result has 20 rows.

### Warning

An accidental cross join can explode row counts.

## Self join

Suppose employees reference managers:

```text
employees
---------
employee_id
name
manager_id
```

```sql
SELECT
    e.name AS employee,
    m.name AS manager
FROM employees e
LEFT JOIN employees m
  ON m.employee_id = e.manager_id;
```

## Join condition in `ON` vs `WHERE`

This distinction is critical for outer joins.

Correct if you want all customers but only paid orders attached:

```sql
SELECT c.name, o.order_id
FROM customers c
LEFT JOIN orders o
  ON o.customer_id = c.customer_id
 AND o.status = 'paid';
```

This different query removes customers without paid orders:

```sql
SELECT c.name, o.order_id
FROM customers c
LEFT JOIN orders o
  ON o.customer_id = c.customer_id
WHERE o.status = 'paid';
```

The `WHERE` predicate rejects null-extended rows and effectively behaves like an inner join for that condition.

## LATERAL join

`LATERAL` allows a subquery in `FROM` to reference columns from earlier `FROM` items.

Example: latest order per customer.

```sql
SELECT
    c.customer_id,
    c.name,
    latest.order_id,
    latest.created_at
FROM customers c
LEFT JOIN LATERAL (
    SELECT o.order_id, o.created_at
    FROM orders o
    WHERE o.customer_id = c.customer_id
    ORDER BY o.created_at DESC, o.order_id DESC
    LIMIT 1
) AS latest ON true;
```

This is especially useful for "top N per parent" queries when paired with a suitable index.

---

# 16. Aggregation and grouping

Aggregates summarize many rows into fewer rows.

## Common aggregate functions

```sql
SELECT count(*) FROM orders;
SELECT sum(order_total) FROM orders;
SELECT avg(order_total) FROM orders;
SELECT min(order_total) FROM orders;
SELECT max(order_total) FROM orders;
```

## `count(*)` vs `count(column)`

```sql
COUNT(*)
```

counts rows.

```sql
COUNT(shipped_at)
```

counts non-null values in `shipped_at`.

## GROUP BY

```sql
SELECT
    customer_id,
    count(*) AS order_count,
    sum(order_total) AS total_spent
FROM orders
GROUP BY customer_id;
```

## HAVING

`WHERE` filters rows **before grouping**.

`HAVING` filters groups **after grouping**.

```sql
SELECT customer_id, sum(order_total) AS total_spent
FROM orders
WHERE status = 'paid'
GROUP BY customer_id
HAVING sum(order_total) > 100000;
```

## FILTER clause

PostgreSQL supports concise conditional aggregates.

```sql
SELECT
    customer_id,
    count(*) AS all_orders,
    count(*) FILTER (WHERE status = 'paid') AS paid_orders,
    count(*) FILTER (WHERE status = 'cancelled') AS cancelled_orders
FROM orders
GROUP BY customer_id;
```

This is often clearer than repeated `CASE` expressions.

## `string_agg`

```sql
SELECT
    customer_id,
    string_agg(status, ', ' ORDER BY created_at) AS status_history
FROM order_status_history
GROUP BY customer_id;
```

## `array_agg`

```sql
SELECT
    customer_id,
    array_agg(order_id ORDER BY order_id) AS order_ids
FROM orders
GROUP BY customer_id;
```

## `json_agg` / `jsonb_agg`

```sql
SELECT
    customer_id,
    jsonb_agg(
        jsonb_build_object(
            'order_id', order_id,
            'total', order_total
        )
        ORDER BY created_at
    ) AS orders
FROM orders
GROUP BY customer_id;
```

Useful for API-shaped database responses, though avoid turning the database into an unnecessarily complex presentation layer.

## GROUPING SETS

Compute multiple grouping levels in one query.

```sql
SELECT region, product_category, sum(amount)
FROM sales
GROUP BY GROUPING SETS (
    (region, product_category),
    (region),
    ()
);
```

`()` represents the grand total.

## ROLLUP

```sql
SELECT year, month, sum(amount)
FROM sales
GROUP BY ROLLUP (year, month);
```

Produces detail plus subtotals.

## CUBE

```sql
SELECT region, category, sum(amount)
FROM sales
GROUP BY CUBE (region, category);
```

Produces combinations of grouping dimensions.

---

# 17. Subqueries

A subquery is a query nested inside another SQL statement.

## Scalar subquery

Returns one value.

```sql
SELECT
    name,
    price,
    (SELECT avg(price) FROM products) AS avg_price
FROM products;
```

## Subquery in WHERE

```sql
SELECT *
FROM products
WHERE price > (
    SELECT avg(price)
    FROM products
);
```

## IN subquery

```sql
SELECT *
FROM customers
WHERE customer_id IN (
    SELECT customer_id
    FROM orders
    WHERE status = 'paid'
);
```

## EXISTS

```sql
SELECT c.*
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
      AND o.status = 'paid'
);
```

`EXISTS` asks whether at least one matching row exists.

## NOT EXISTS

```sql
SELECT p.*
FROM products p
WHERE NOT EXISTS (
    SELECT 1
    FROM order_items oi
    WHERE oi.product_id = p.product_id
);
```

This is often safer than `NOT IN` when null values may appear in the subquery.

## `NOT IN` and NULL trap

Consider:

```sql
WHERE id NOT IN (1, 2, NULL)
```

Because of SQL's three-valued logic, the `NULL` can make results surprising.

For anti-joins, prefer `NOT EXISTS` unless you have explicitly controlled nullability.

## Correlated subquery

A correlated subquery references the outer query.

```sql
SELECT c.customer_id, c.name
FROM customers c
WHERE (
    SELECT count(*)
    FROM orders o
    WHERE o.customer_id = c.customer_id
) >= 5;
```

The optimizer may transform such expressions, but conceptually the inner query depends on each outer row.

---

# 18. Common Table Expressions

A Common Table Expression (CTE) is introduced by `WITH`.

## Basic CTE

```sql
WITH paid_orders AS (
    SELECT *
    FROM orders
    WHERE status = 'paid'
)
SELECT customer_id, sum(order_total)
FROM paid_orders
GROUP BY customer_id;
```

CTEs can make complex queries easier to read.

## Multiple CTEs

```sql
WITH
paid_orders AS (
    SELECT * FROM orders WHERE status = 'paid'
),
customer_totals AS (
    SELECT customer_id, sum(order_total) AS total
    FROM paid_orders
    GROUP BY customer_id
)
SELECT c.name, ct.total
FROM customer_totals ct
JOIN customers c USING (customer_id);
```

## Data-modifying CTEs

PostgreSQL supports data-changing statements inside `WITH` when used appropriately.

```sql
WITH deleted AS (
    DELETE FROM sessions
    WHERE expires_at < now()
    RETURNING user_id
)
SELECT count(*)
FROM deleted;
```

## Recursive CTE

Useful for hierarchies and graph-like traversal.

Example employee hierarchy:

```sql
WITH RECURSIVE org AS (
    SELECT
        employee_id,
        manager_id,
        name,
        1 AS level
    FROM employees
    WHERE manager_id IS NULL

    UNION ALL

    SELECT
        e.employee_id,
        e.manager_id,
        e.name,
        org.level + 1
    FROM employees e
    JOIN org
      ON e.manager_id = org.employee_id
)
SELECT *
FROM org
ORDER BY level, employee_id;
```

A recursive CTE has:

1. a non-recursive starting query;
2. `UNION ALL` or related set operator;
3. a recursive term referencing the CTE.

### Common uses

- category trees;
- org charts;
- bill of materials;
- folder structures;
- graph traversal;
- generating series-like recursive calculations.

### Avoid infinite recursion

Always ensure recursion eventually stops. For arbitrary graphs, track visited nodes when cycles are possible.

---

# 19. Set operations

Set operations combine result sets.

## UNION

Combines results and removes duplicates.

```sql
SELECT email FROM customers
UNION
SELECT email FROM newsletter_subscribers;
```

## UNION ALL

Combines results and keeps duplicates.

```sql
SELECT email FROM customers
UNION ALL
SELECT email FROM newsletter_subscribers;
```

`UNION ALL` avoids duplicate elimination and is often faster when deduplication is unnecessary.

## INTERSECT

Rows common to both results:

```sql
SELECT email FROM customers
INTERSECT
SELECT email FROM newsletter_subscribers;
```

## EXCEPT

Rows in the first result but not the second:

```sql
SELECT email FROM customers
EXCEPT
SELECT email FROM unsubscribed_users;
```

## Compatibility requirement

Each branch must return the same number of columns with compatible types.

---

# 20. Window functions

Window functions are among the most important advanced SQL features.

They perform calculations across related rows **without collapsing them into one row per group**.

## GROUP BY vs window function

`GROUP BY`:

```sql
SELECT customer_id, sum(order_total)
FROM orders
GROUP BY customer_id;
```

One result row per customer.

Window:

```sql
SELECT
    order_id,
    customer_id,
    order_total,
    sum(order_total) OVER (PARTITION BY customer_id) AS customer_total
FROM orders;
```

Every order remains visible.

## ROW_NUMBER

```sql
SELECT
    order_id,
    customer_id,
    created_at,
    row_number() OVER (
        PARTITION BY customer_id
        ORDER BY created_at DESC, order_id DESC
    ) AS rn
FROM orders;
```

Latest order per customer:

```sql
WITH ranked AS (
    SELECT
        o.*,
        row_number() OVER (
            PARTITION BY customer_id
            ORDER BY created_at DESC, order_id DESC
        ) AS rn
    FROM orders o
)
SELECT *
FROM ranked
WHERE rn = 1;
```

## RANK vs DENSE_RANK

```sql
SELECT
    employee_id,
    salary,
    rank() OVER (ORDER BY salary DESC) AS rnk,
    dense_rank() OVER (ORDER BY salary DESC) AS dense_rnk
FROM employees;
```

If salaries are:

```text
100, 100, 90
```

then ranks are:

```text
RANK:       1, 1, 3
DENSE_RANK: 1, 1, 2
```

## LAG and LEAD

Previous value:

```sql
SELECT
    sales_date,
    amount,
    lag(amount) OVER (ORDER BY sales_date) AS previous_amount
FROM daily_sales;
```

Next value:

```sql
lead(amount) OVER (ORDER BY sales_date)
```

Useful for trends and change calculations.

## Running total

```sql
SELECT
    sales_date,
    amount,
    sum(amount) OVER (
        ORDER BY sales_date
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS running_total
FROM daily_sales;
```

## Moving average

```sql
SELECT
    sales_date,
    amount,
    avg(amount) OVER (
        ORDER BY sales_date
        ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
    ) AS seven_row_average
FROM daily_sales;
```

## FIRST_VALUE and LAST_VALUE

```sql
SELECT
    customer_id,
    order_id,
    first_value(order_total) OVER (
        PARTITION BY customer_id
        ORDER BY created_at
    ) AS first_order_total
FROM orders;
```

### `LAST_VALUE` surprise

The default window frame may not mean "last row in the whole partition." If you need that, define the frame explicitly.

```sql
last_value(order_total) OVER (
    PARTITION BY customer_id
    ORDER BY created_at
    ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
)
```

## Named windows

```sql
SELECT
    employee_id,
    department_id,
    salary,
    avg(salary) OVER dept_window AS dept_avg,
    rank() OVER dept_window AS dept_rank
FROM employees
WINDOW dept_window AS (
    PARTITION BY department_id
    ORDER BY salary DESC
);
```

---

# 21. Views and materialized views

## View

A view stores a query definition, not an ordinary copy of its result.

```sql
CREATE VIEW active_customers AS
SELECT customer_id, name, email
FROM customers
WHERE active = true;
```

Use:

```sql
SELECT * FROM active_customers;
```

## Why use views?

- simplify complex queries;
- expose a stable interface;
- limit visible columns;
- support reporting;
- centralize reusable relational logic.

## Replace a view

```sql
CREATE OR REPLACE VIEW active_customers AS
SELECT customer_id, name, email, created_at
FROM customers
WHERE active = true;
```

Be mindful of compatibility requirements when replacing view definitions.

## Materialized view

A materialized view stores query results physically.

```sql
CREATE MATERIALIZED VIEW monthly_sales AS
SELECT
    date_trunc('month', created_at) AS month,
    sum(order_total) AS revenue
FROM orders
WHERE status = 'paid'
GROUP BY 1;
```

Query it:

```sql
SELECT * FROM monthly_sales;
```

Refresh it:

```sql
REFRESH MATERIALIZED VIEW monthly_sales;
```

## Concurrent refresh

```sql
REFRESH MATERIALIZED VIEW CONCURRENTLY monthly_sales;
```

Concurrent refresh has requirements, including a suitable unique index, and may be slower, but it allows readers to continue using the materialized view during refresh.

## View vs materialized view

| Feature | View | Materialized view |
|---|---|---|
| Stores rows | No | Yes |
| Always current | Yes, based on current underlying data | No |
| Needs refresh | No | Yes |
| Can speed expensive report | Not by storage itself | Yes |

---

# 22. Sequences, identity, and generated columns

## Sequences

A sequence generates numeric values.

```sql
CREATE SEQUENCE invoice_number_seq;
```

Get next value:

```sql
SELECT nextval('invoice_number_seq');
```

## `serial` legacy shorthand

Older PostgreSQL schemas commonly use:

```sql
id serial PRIMARY KEY
```

`serial` is not a true standalone SQL type; it is shorthand that creates an integer column, a sequence, and a default.

Modern schemas should usually prefer SQL-standard identity columns.

## Identity columns

```sql
id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY
```

or:

```sql
id bigint GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY
```

### ALWAYS vs BY DEFAULT

`ALWAYS` means PostgreSQL normally generates the value and explicit user values require an override mechanism.

`BY DEFAULT` allows callers to supply a value explicitly.

For application-owned surrogate keys, `ALWAYS` is a strong default.

## Sequence gaps are normal

Do not assume identity or sequence values are gapless.

Gaps can occur because of:

- rolled-back transactions;
- cached values;
- failed inserts;
- explicit sequence calls;
- crashes or failover behavior.

If your business requires legally gapless numbers, model that requirement separately and understand the concurrency trade-offs.

## Generated columns

A generated column derives its value from other columns in the same row. Unlike a default, the value is recalculated according to the generation expression rather than being supplied independently by the caller.

### Stored generated column

A **stored** generated column is computed when the row is written and occupies storage.

```sql
CREATE TABLE line_items (
    quantity integer NOT NULL CHECK (quantity > 0),
    unit_price numeric(12,2) NOT NULL CHECK (unit_price >= 0),
    line_total numeric(14,2)
        GENERATED ALWAYS AS (quantity * unit_price) STORED
);
```

Insert only the source values:

```sql
INSERT INTO line_items (quantity, unit_price)
VALUES (3, 499.00);
```

Then:

```sql
SELECT quantity, unit_price, line_total
FROM line_items;
```

Expected `line_total`:

```text
1497.00
```

### Virtual generated column — PostgreSQL 18

PostgreSQL 18 supports **virtual** generated columns. A virtual value is computed when read and does not occupy storage for the generated value.

```sql
CREATE TABLE rectangles (
    width numeric NOT NULL,
    height numeric NOT NULL,
    area numeric GENERATED ALWAYS AS (width * height) VIRTUAL
);
```

In PostgreSQL 18, `VIRTUAL` is the default if neither `VIRTUAL` nor `STORED` is written:

```sql
area numeric GENERATED ALWAYS AS (width * height)
```

### Stored vs virtual

| Choice | Computed | Stored on disk | Good fit |
|---|---|---|---|
| `STORED` | when row is written | yes | expensive/read-heavy derived value, compatibility with features requiring storage |
| `VIRTUAL` | when column is read | no | inexpensive derived value where avoiding duplicated storage is useful |

### Generated column vs default

A default is used when an `INSERT` omits a value:

```sql
created_at timestamptz DEFAULT now()
```

After insertion, it behaves like an ordinary column and can be updated directly.

A generated column, by contrast, is tied to its expression and cannot be independently assigned an arbitrary value. The caller should normally omit it or specify `DEFAULT` where allowed.

### Important restrictions

Generation expressions must obey PostgreSQL's generated-column rules. Important points include:

- the expression can use columns from the current row;
- it cannot reference another generated column;
- functions/operators in the expression must be immutable;
- subqueries and references to other tables are not allowed;
- a generated column cannot simultaneously have a normal default or identity definition;
- generated columns cannot be partition keys;
- PostgreSQL 18 virtual generated columns have additional restrictions around user-defined types/functions compared with stored generated columns.

Generated columns are useful when the derived expression genuinely belongs to the data model and should never drift away from its source columns. If the logic depends on other rows, external services, volatile values, or complex business workflow, a generated column is usually the wrong tool.


---

# 23. Transactions and ACID

A **transaction** groups database operations into one logical unit of work. The main question is not "how many SQL statements are there?" but "which changes must succeed or fail together to preserve a business invariant?"

## Example: money transfer

You must not debit one account without crediting the other.

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 1000
WHERE account_id = 2;

COMMIT;
```

If the unit of work cannot be completed:

```sql
ROLLBACK;
```

`ROLLBACK` discards the transaction's uncommitted database changes.

### Add the invariant, not just the transaction

A transaction alone does not prevent an account from becoming negative. If that is forbidden, enforce it as part of the model and/or locking/isolation strategy, for example:

```sql
balance numeric(14,2) NOT NULL CHECK (balance >= 0)
```

Correctness usually comes from a combination of **transaction boundaries + constraints + appropriate concurrency control**.

## ACID

ACID is a useful way to reason about transaction guarantees.

### Atomicity — all or nothing

If a transaction contains five database changes and the transaction rolls back, none of those changes becomes committed.

In the transfer example, atomicity prevents a committed state where money was debited from account 1 but never credited to account 2.

### Consistency — valid state to valid state

A successful transaction should leave declared database constraints and required application invariants satisfied.

PostgreSQL can enforce what you actually declare: `NOT NULL`, keys, checks, exclusion constraints, triggers, and transactional rules. It cannot infer every business rule automatically.

### Isolation — concurrent work has controlled interaction

Two transactions may execute at the same time, but PostgreSQL's MVCC, locks, and selected isolation level determine what each can observe and when a conflicting transaction must wait or retry.

Isolation does **not** mean every transaction runs one at a time.

### Durability — committed changes survive crashes

Once PostgreSQL reports a transaction committed, WAL and the configured durability/storage stack are used so committed work can be recovered after a crash, subject to settings such as synchronous commit behavior and the reliability of the underlying storage.

## Transaction lifecycle

A common explicit transaction looks like:

```text
BEGIN
  statements succeed
  statements succeed
COMMIT
```

Failure path:

```text
BEGIN
  statement succeeds
  statement fails
  transaction becomes failed
ROLLBACK
```

Inside an explicit transaction, a normal SQL error usually leaves the transaction in an aborted state. Subsequent SQL does not simply continue as though nothing happened; roll back the transaction or roll back to an appropriate savepoint.

## Autocommit

Most clients operate in autocommit mode by default: each standalone statement is its own transaction unless you explicitly start a transaction block.

These two statements in autocommit mode are **two separate transactions**:

```sql
UPDATE accounts SET balance = balance - 100 WHERE account_id = 1;
UPDATE accounts SET balance = balance + 100 WHERE account_id = 2;
```

If they must be atomic together, wrap them in one transaction.

## `SAVEPOINT`

A savepoint creates a point inside a transaction to which part of the work can be rolled back without abandoning the entire transaction.

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 100
WHERE account_id = 1;

SAVEPOINT after_debit;

INSERT INTO audit_log(message)
VALUES ('transfer audit');

ROLLBACK TO SAVEPOINT after_debit;

COMMIT;
```

The audit insert is undone; work before the savepoint can remain part of the transaction.

Useful commands:

```sql
SAVEPOINT sp1;
ROLLBACK TO SAVEPOINT sp1;
RELEASE SAVEPOINT sp1;
```

Savepoints are useful for controlled partial error handling, but creating huge numbers of nested savepoints/subtransactions can add overhead.

## Many DDL changes are transactional

PostgreSQL can roll back many schema changes:

```sql
BEGIN;
CREATE TABLE test_table(id bigint);
ROLLBACK;
```

The table does not remain after the rollback.

This is valuable for safe migrations, but do not assume **every** administrative command is allowed or meaningful inside a transaction block. Check the command's documentation.

## Database rollback cannot undo external side effects

Suppose your transaction:

1. updates an order;
2. calls an external payment/email API;
3. later rolls back.

PostgreSQL can roll back its own database changes, but it cannot magically unsend the email or reverse an external API request.

For reliable integration, consider patterns covered later such as:

- transactional outbox;
- idempotency keys;
- retries with deduplication;
- sagas/compensating actions where appropriate.

## Keep transactions short

Long transactions can:

- hold row/table locks longer;
- delay vacuum cleanup by keeping old snapshots relevant;
- retain dead row versions;
- increase replication/recovery pressure;
- increase deadlock/conflict probability;
- make failures more expensive to retry.

Avoid opening a transaction and then waiting for:

- user input;
- a long file upload;
- arbitrary think time;
- slow external APIs;
- unrelated application work.

## Transaction best practices

1. Define the business invariant first.
2. Put all database writes that must be atomic in the same transaction.
3. Enforce durable rules with constraints where possible.
4. Keep the transaction short and deterministic.
5. Lock rows in a consistent order when concurrent updates can conflict.
6. Handle deadlock and serialization retries at the transaction boundary.
7. Never assume external side effects roll back with PostgreSQL.
8. Log enough context to diagnose failed/retried transactions without logging secrets.


---

# 24. MVCC and concurrency

MVCC means **Multi-Version Concurrency Control**. It is one of PostgreSQL's core mechanisms for allowing concurrent reads and writes while preserving transaction visibility rules.

## The problem MVCC solves

Suppose:

- Transaction A is reading a row.
- Transaction B updates that row at the same time.

A simplistic design could force readers and writers to block each other constantly. PostgreSQL instead keeps row versions and lets each statement/transaction see the versions visible to its snapshot.

## Conceptual row versions

Imagine the logical row:

```text
account_id = 1, balance = 100
```

Transaction B runs:

```sql
UPDATE accounts
SET balance = 80
WHERE account_id = 1;
```

PostgreSQL normally creates a **new tuple version** rather than overwriting the visible row in place in the simplistic sense. The old and new versions carry transaction visibility information.

Conceptually:

```text
old version: balance = 100   -> visible to some older snapshots
new version: balance = 80    -> visible after the updating transaction commits, according to isolation rules
```

The exact on-disk fields are internal implementation details; the important beginner idea is that different transactions can legitimately see different committed row versions at the same moment.

## Snapshot visibility

A snapshot answers questions such as:

- Which transactions were committed when this snapshot was taken?
- Which row version is visible to me?
- Is this newer version still uncommitted?
- Should I continue seeing an older committed version?

The lifetime of the snapshot depends on isolation level. At `READ COMMITTED`, ordinary statements generally get a fresh snapshot per statement. At `REPEATABLE READ` and `SERIALIZABLE`, transaction-level behavior provides a more stable snapshot model.

## Why MVCC matters

MVCC allows:

- readers to avoid blocking ordinary writers in many common cases;
- writers to avoid blocking ordinary readers in many common cases;
- consistent snapshots;
- transactional rollback;
- isolation semantics;
- read-heavy systems to keep working while rows are being updated.

## What MVCC does **not** mean

MVCC does not eliminate locking.

Two transactions trying to update the same row can still conflict and wait. DDL can take strong table locks. Foreign keys, unique checks, explicit locking, and isolation rules can all require coordination.

Think of MVCC as reducing unnecessary reader/writer interference — not as "PostgreSQL never blocks."

## Dead tuples

When a row is updated or deleted, old versions can eventually become invisible to every transaction. Those obsolete versions are often called **dead tuples**.

They do not immediately disappear from the table file. PostgreSQL's vacuum machinery makes their space reusable and performs important transaction-ID maintenance.

```text
UPDATE/DELETE activity
        |
        v
old row versions
        |
        v
no active snapshot needs them
        |
        v
VACUUM can reclaim/reuse space
```

This is why autovacuum is not optional housekeeping; it is part of normal MVCC operation.

## Long transactions and old snapshots

A long-running transaction can keep an old snapshot alive. That may prevent cleanup of row versions that would otherwise be removable.

Symptoms can include:

- growing dead-tuple counts;
- table/index bloat pressure;
- vacuum appearing unable to remove tuples;
- more WAL/resource use;
- old transaction ID pressure.

When investigating bloat, always look for long-running or `idle in transaction` sessions before blaming vacuum alone.

## HOT updates

PostgreSQL can sometimes perform **Heap-Only Tuple (HOT)** updates when indexed columns do not need new index entries and there is suitable space on the same heap page.

HOT updates can reduce index churn because PostgreSQL can link versions within the heap page without inserting a new tuple into every relevant index.

Factors influencing HOT opportunities include:

- whether indexed values change;
- page free space;
- table `fillfactor`;
- update pattern.

Do not remove useful indexes merely to chase HOT updates. Measure the actual workload and balance read/index needs against write cost.

## MVCC mental model

When troubleshooting concurrency, ask three separate questions:

1. **Visibility:** Which version should this transaction see?
2. **Locking:** Is another transaction preventing this operation from proceeding?
3. **Cleanup:** Are old versions still needed by any snapshot, and is vacuum keeping up?

Those three questions explain a large fraction of PostgreSQL concurrency behavior.


---

# 25. Isolation levels

Isolation controls what concurrent transactions are allowed to observe and which anomalies PostgreSQL must prevent or detect.

It is easiest to learn isolation from **business races**, not only definitions.

## Common anomalies

| Anomaly | Simple meaning |
|---|---|
| dirty read | read data another transaction has not committed |
| non-repeatable read | read the same row twice and get different committed values |
| phantom read | rerun a predicate query and see a changed set of matching rows |
| serialization anomaly | combined concurrent outcome could not have happened in any serial order |

PostgreSQL does not provide dirty reads: even `READ UNCOMMITTED` behaves as `READ COMMITTED`.

A useful PostgreSQL-oriented summary is:

| Level | Fresh snapshot behavior | Non-repeatable/phantom reads | Serialization anomalies |
|---|---|---|---|
| `READ COMMITTED` | normally each statement | possible | possible |
| `REPEATABLE READ` | stable transaction snapshot | prevented for ordinary snapshot reads | still possible |
| `SERIALIZABLE` | serializable transaction view | prevented | detected/prevented by aborting transactions when necessary |

## Read Committed

This is PostgreSQL's default isolation level.

```sql
BEGIN ISOLATION LEVEL READ COMMITTED;
```

Each ordinary statement sees a snapshot of committed data as of the start of that statement, plus the transaction's own changes.

### Scenario

Transaction A:

```sql
BEGIN;
SELECT status FROM orders WHERE order_id = 10;
-- returns 'pending'
```

Transaction B commits:

```sql
UPDATE orders
SET status = 'paid'
WHERE order_id = 10;
```

Transaction A runs the same query again:

```sql
SELECT status FROM orders WHERE order_id = 10;
-- can now return 'paid'
```

That is normal at `READ COMMITTED` because the two statements may use different snapshots.

### When to use

It is a good default for ordinary CRUD when each statement can safely react to the latest committed state and stronger transaction-wide snapshot guarantees are unnecessary.

## Repeatable Read

```sql
BEGIN ISOLATION LEVEL REPEATABLE READ;
```

PostgreSQL provides a stable snapshot for the transaction. Ordinary reads continue to see the database as of that transaction snapshot rather than seeing rows committed later by other transactions.

This prevents ordinary non-repeatable reads and phantom reads within that snapshot.

### Important limitation: snapshot consistency is not full serializability

Two transactions can each make a decision based on a consistent snapshot and still produce a combined outcome that no serial execution should allow. A common family of examples is **write skew**, where each transaction updates a different row after checking a multi-row invariant.

If the invariant must behave as though transactions ran one-by-one, use appropriate locking/constraints or `SERIALIZABLE` rather than assuming `REPEATABLE READ` is enough.

## Serializable

```sql
BEGIN ISOLATION LEVEL SERIALIZABLE;
```

This is PostgreSQL's strongest standard isolation level. Successful transactions are required to have an outcome consistent with some serial execution order.

PostgreSQL does not implement this by simply running one transaction at a time. It allows concurrency and tracks dangerous dependency patterns. When it cannot safely serialize the outcome, one transaction can fail with a **serialization failure**.

### Application requirement: retry the whole transaction

Conceptual application flow:

```text
attempt transaction
    BEGIN SERIALIZABLE
    read current state
    perform dependent writes
    COMMIT

if SQLSTATE 40001 (serialization_failure):
    retry the entire transaction with a bounded retry policy
```

Retrying only the final statement is often wrong because earlier reads and decisions belonged to the failed transaction snapshot.

### Serializable is not "no concurrency"

Multiple serializable transactions can run concurrently. PostgreSQL may let all of them commit if their dependency graph is safe; otherwise it aborts one to preserve serializable behavior.

## Read Uncommitted

SQL defines a `READ UNCOMMITTED` level, but PostgreSQL treats it like `READ COMMITTED`. Dirty reads are not exposed.

```sql
BEGIN ISOLATION LEVEL READ UNCOMMITTED;
```

Do not expect this to let you read another transaction's uncommitted changes.

## Isolation vs explicit locking

Isolation level and locks solve related but different problems.

Example: a worker wants to claim one job immediately. Even at the default isolation level, explicit row locking may be the right mechanism:

```sql
SELECT job_id
FROM jobs
WHERE status = 'pending'
ORDER BY job_id
FOR UPDATE SKIP LOCKED
LIMIT 1;
```

Conversely, a business invariant spanning rows might be easier to protect with `SERIALIZABLE` or a declarative constraint than with ad-hoc locking.

## Choosing an isolation level

Start from the invariant:

- **ordinary independent CRUD:** usually `READ COMMITTED`;
- **reports/business logic that need one stable transaction snapshot:** consider `REPEATABLE READ`;
- **multi-row decisions that must behave like serial execution:** consider `SERIALIZABLE` with retry logic;
- **specific rows must be reserved/claimed:** consider explicit row locks;
- **rule can be declaratively enforced:** prefer a constraint because every code path benefits.

Never choose isolation only by a vague idea that "higher is safer" or "lower is faster." Correctness requirements come first, then benchmark contention and retry behavior.


---

# 26. Locks and deadlocks

MVCC does not eliminate locking.

PostgreSQL uses multiple lock types to protect rows, relations, and internal structures.

## Row locks

Row-level locks coordinate transactions that need to modify or reserve the same logical rows. They do not normally block plain `SELECT` queries that only read visible row versions.

### `SELECT ... FOR UPDATE`

Use when the selected rows are about to be changed and other transactions must not acquire conflicting row locks first.

```sql
BEGIN;

SELECT balance
FROM accounts
WHERE account_id = 1
FOR UPDATE;

UPDATE accounts
SET balance = balance - 100
WHERE account_id = 1;

COMMIT;
```

If another transaction already holds a conflicting lock on that row, this statement normally waits until the conflict resolves or a timeout/cancel occurs.

## Other row-lock clauses

PostgreSQL provides multiple row-lock strengths:

| Clause | Conceptual intent |
|---|---|
| `FOR UPDATE` | strongest common row lock; row is intended for update/delete |
| `FOR NO KEY UPDATE` | update row while allowing more concurrency when key-identifying values are not being changed |
| `FOR SHARE` | shared protection against conflicting updates while allowing compatible shared lockers |
| `FOR KEY SHARE` | weaker shared protection, commonly relevant to key/reference safety |

You rarely need to memorize the entire conflict matrix. Start with the business requirement, use the weakest lock mode that correctly protects it, and consult the official lock-conflict table for sophisticated concurrency designs.

## `NOWAIT`

```sql
SELECT *
FROM jobs
WHERE job_id = 10
FOR UPDATE NOWAIT;
```

If a conflicting row lock is already held, `NOWAIT` fails immediately instead of waiting.

Use this when waiting is worse than returning "busy, try again" to the caller.

## `SKIP LOCKED`

`SKIP LOCKED` skips rows currently unavailable because of conflicting row locks.

```sql
SELECT job_id
FROM jobs
WHERE status = 'pending'
ORDER BY job_id
FOR UPDATE SKIP LOCKED
LIMIT 1;
```

This is excellent for queue-like worker coordination where multiple workers should claim different available rows.

### Queue pattern

```sql
BEGIN;

WITH next_job AS (
    SELECT job_id
    FROM jobs
    WHERE status = 'pending'
    ORDER BY job_id
    FOR UPDATE SKIP LOCKED
    LIMIT 1
)
UPDATE jobs j
SET status = 'processing',
    started_at = now()
FROM next_job
WHERE j.job_id = next_job.job_id
RETURNING j.*;

COMMIT;
```

### Important warning

`SKIP LOCKED` deliberately gives a view that can omit currently locked rows. That is useful for queue consumers, but it is usually wrong for general reporting or financial queries that require a complete logical set.

### Locking best practices

- lock only rows required by the current business action;
- keep the transaction short after obtaining a lock;
- acquire multiple resources in a consistent order;
- use `NOWAIT`/timeouts when indefinite waiting is unacceptable;
- use `SKIP LOCKED` for queue semantics, not as a generic performance trick;
- remember that a correct constraint can sometimes replace explicit "check then lock" application code.

## Table locks

PostgreSQL automatically acquires appropriate table-level lock modes for many operations.

You can explicitly lock:

```sql
LOCK TABLE accounts IN SHARE MODE;
```

Explicit table locks should be used only with a clear concurrency reason.

## Deadlock

Transaction A:

1. locks row 1;
2. waits for row 2.

Transaction B:

1. locks row 2;
2. waits for row 1.

Neither can continue.

PostgreSQL detects the deadlock and aborts one transaction.

## Preventing deadlocks

Acquire resources in a consistent order.

Bad pattern:

```text
Transaction A: account 1 → account 2
Transaction B: account 2 → account 1
```

Better:

```text
Always lock lower account_id first.
```

Application code should also be able to retry transactions that fail due to deadlock or serialization conditions where appropriate.

## Inspect locks

```sql
SELECT *
FROM pg_locks;
```

Join with `pg_stat_activity` for more useful diagnosis.

Example:

```sql
SELECT
    a.pid,
    a.usename,
    a.state,
    a.query,
    l.locktype,
    l.mode,
    l.granted
FROM pg_locks l
JOIN pg_stat_activity a
  ON a.pid = l.pid
ORDER BY a.pid;
```

---
# 27. Indexes

An index is an auxiliary data structure that helps PostgreSQL find rows without scanning an entire table.

Think of a book:

- without an index, you inspect every page;
- with an index, you jump near the correct page.

Indexes can dramatically improve reads, but they are not free.

Every index:

- uses disk space;
- consumes memory/cache;
- adds work to inserts;
- adds work to updates when indexed values change;
- adds work to deletes;
- needs vacuum/maintenance consideration.

## Create a basic B-tree index

```sql
CREATE INDEX idx_orders_customer_id
ON orders (customer_id);
```

Useful query:

```sql
SELECT *
FROM orders
WHERE customer_id = 1001;
```

## B-tree

B-tree is PostgreSQL's default and most common index type.

Good for:

- equality: `=`;
- ranges: `<`, `<=`, `>`, `>=`;
- ordered scans;
- many `ORDER BY` patterns;
- prefix portions of multicolumn indexes.

```sql
CREATE INDEX idx_orders_created_at
ON orders (created_at);
```

## Multicolumn index

```sql
CREATE INDEX idx_orders_customer_created
ON orders (customer_id, created_at DESC);
```

Good for:

```sql
SELECT *
FROM orders
WHERE customer_id = 1001
ORDER BY created_at DESC
LIMIT 20;
```

### Column order matters

An index on:

```text
(customer_id, created_at)
```

is not identical to:

```text
(created_at, customer_id)
```

Choose order based on real query patterns, selectivity, equality/range conditions, ordering, and PostgreSQL's planner capabilities.

### PostgreSQL 18 skip scan

PostgreSQL 18 expands cases where a multicolumn B-tree can be useful even when a leading column does not have a simple equality predicate, using skip-scan strategies where the planner estimates that doing so is beneficial.

Do not use this as an excuse to ignore index design. Verify with `EXPLAIN`.

## Unique index

```sql
CREATE UNIQUE INDEX uq_users_email
ON users (email);
```

A `UNIQUE` table constraint normally creates a supporting unique B-tree index automatically.

Prefer declaring data integrity as a constraint when it is truly a business rule.

## Partial index

Indexes only rows matching a condition.

```sql
CREATE INDEX idx_orders_open_created
ON orders (created_at)
WHERE status = 'open';
```

Useful if open orders are a small, frequently queried subset.

Query:

```sql
SELECT *
FROM orders
WHERE status = 'open'
ORDER BY created_at;
```

### Important

The query predicate must be recognizable as matching the index predicate. Highly parameterized or logically equivalent-but-difficult expressions may not use the partial index as expected.

## Expression index

```sql
CREATE INDEX idx_users_lower_email
ON users (lower(email));
```

Query:

```sql
SELECT *
FROM users
WHERE lower(email) = lower('Aisha@example.com');
```

This is useful for case-insensitive lookup if that is the intended semantics.

## Covering index with INCLUDE

```sql
CREATE INDEX idx_orders_customer_cover
ON orders (customer_id)
INCLUDE (order_total, created_at);
```

The included columns are not search keys but can allow index-only scans when visibility conditions permit.

Use `INCLUDE` selectively. Wider indexes cost more space and write I/O.

## Index-only scan

An index-only scan can return data from the index without fetching every heap tuple, when:

- all required columns are in the index;
- visibility information allows it.

Vacuum and the visibility map therefore influence index-only scan effectiveness.

## Hash index

```sql
CREATE INDEX idx_sessions_token_hash
ON sessions USING hash (token);
```

Hash indexes support equality-style searches. B-tree is still usually the default first choice for ordinary equality because it is more flexible.

## GIN

Generalized Inverted Index.

Common use cases:

- `jsonb` containment;
- arrays;
- full-text search.

Example:

```sql
CREATE INDEX idx_products_attributes_gin
ON products USING gin (attributes);
```

Then:

```sql
SELECT *
FROM products
WHERE attributes @> '{"color":"black"}'::jsonb;
```

## GiST

Generalized Search Tree.

Common use cases:

- ranges;
- geometric data;
- nearest-neighbor search for suitable operator classes;
- exclusion constraints;
- PostGIS indexing.

```sql
CREATE INDEX idx_bookings_period_gist
ON bookings USING gist (period);
```

## SP-GiST

Space-partitioned GiST supports data structures that naturally partition search space.

Useful for particular operator classes such as some geometric, text-prefix, and network-oriented data structures.

Do not choose SP-GiST just because it sounds advanced. Choose based on supported operators and workload.

## BRIN

Block Range INdex stores summaries for ranges of physical table blocks.

Excellent for very large tables where values correlate with physical row order.

Example log table:

```sql
CREATE INDEX idx_events_created_brin
ON events USING brin (created_at);
```

A BRIN index can be tiny compared with B-tree.

Great scenario:

- billions of append-mostly events;
- `created_at` generally increases with physical row position;
- queries commonly filter time ranges.

Poor scenario:

- small table;
- values randomly distributed across physical pages;
- queries require exact point lookup with high precision.

## Concurrent index creation

```sql
CREATE INDEX CONCURRENTLY idx_orders_status
ON orders (status);
```

This reduces blocking of normal writes compared with ordinary index creation, but takes more work and has restrictions.

It cannot run inside a normal transaction block.

## Reindex

```sql
REINDEX INDEX idx_orders_customer_id;
```

Or concurrently where supported:

```sql
REINDEX INDEX CONCURRENTLY idx_orders_customer_id;
```

Use reindexing to address specific index maintenance needs, not as a routine substitute for understanding the cause of bloat or corruption.

## Find unused indexes

Statistics can help identify candidates:

```sql
SELECT
    schemaname,
    relname AS table_name,
    indexrelname AS index_name,
    idx_scan
FROM pg_stat_user_indexes
ORDER BY idx_scan ASC;
```

### Warning

`idx_scan = 0` does **not** automatically mean "drop this index." Statistics may have reset, workload may be seasonal, or the index may support rare but critical operations or constraints.

## Foreign keys and indexes

PostgreSQL automatically indexes primary/unique referenced keys, but it does **not** automatically create an index on every foreign-key referencing column.

For example:

```sql
orders.customer_id REFERENCES customers(customer_id)
```

often benefits from:

```sql
CREATE INDEX idx_orders_customer_id
ON orders(customer_id);
```

especially for joins and parent deletes/updates.

## Common indexing mistakes

1. Index every column.
2. Create many overlapping indexes.
3. Ignore column order.
4. Assume an index is always used.
5. Function-wrap an indexed column without a matching expression index.
6. Use low-selectivity indexes without measuring benefit.
7. Forget write overhead.
8. Add indexes without running `EXPLAIN (ANALYZE, BUFFERS)`.
9. Keep redundant indexes forever.
10. Expect an index to fix a query returning a huge fraction of the table.

---

# 28. Query planner and EXPLAIN

You write declarative SQL: describe **what** result you need.

The PostgreSQL planner decides **how** to get it.

Possible operations include:

- sequential scan;
- index scan;
- index-only scan;
- bitmap index/heap scan;
- nested loop join;
- hash join;
- merge join;
- sort;
- aggregate;
- parallel operations.

## Basic EXPLAIN

```sql
EXPLAIN
SELECT *
FROM orders
WHERE customer_id = 1001;
```

This asks PostgreSQL to show the **estimated execution plan** without running the query.

Example shape:

```text
Index Scan using idx_orders_customer_id on orders
  Index Cond: (customer_id = 1001)
```

The planner chooses a plan based on table/index metadata, statistics, cost settings, and available operations. `EXPLAIN` tells you what PostgreSQL *plans* to do, not whether that estimate is accurate.

## `EXPLAIN ANALYZE`

```sql
EXPLAIN ANALYZE
SELECT *
FROM orders
WHERE customer_id = 1001;
```

`ANALYZE` in this context means **execute the statement and measure what really happened**. The output adds actual rows, timings, loop counts, and other runtime information.

### Critical warning

`EXPLAIN ANALYZE` executes the statement.

For:

```sql
DELETE ...
UPDATE ...
INSERT ...
MERGE ...
```

it changes data unless the surrounding transaction is rolled back.

A controlled exploration pattern is:

```sql
BEGIN;

EXPLAIN (ANALYZE, BUFFERS)
UPDATE accounts
SET balance = balance + 10
WHERE account_id = 1;

ROLLBACK;
```

Even then, be careful: execution can acquire locks, fire triggers, advance sequences, invoke functions, or cause external side effects that a database rollback cannot reverse.

## How to read a plan tree

Plans are trees. The top node produces the final result; its child nodes produce input for their parents.

Example:

```text
Nested Loop
  -> Index Scan on customers
  -> Index Scan on orders
```

A practical reading method:

1. identify the node that returns the final rows;
2. inspect its children and work downward;
3. compare **estimated rows** with **actual rows**;
4. inspect repeated nodes and `loops`;
5. look for large scans, filters, sorts, hashes, and temp I/O;
6. identify the first place where estimates or row counts become unexpectedly large.

Do not simply look for the node with the visually largest cost number and stop.

## Understanding `actual time`, `rows`, and `loops`

A runtime node may look like:

```text
(actual time=0.020..0.050 rows=3 loops=1000)
```

Key ideas:

- `actual time=a..b` shows time to first row and time to finish that node's work for an execution;
- `rows` is the average rows produced per loop when the node executes multiple times;
- `loops` tells you how many times the node ran.

A seemingly cheap inner node can dominate runtime when a nested loop executes it thousands of times. Always read `rows` together with `loops`.

## `BUFFERS`

```sql
EXPLAIN (ANALYZE, BUFFERS)
SELECT ...;
```

This is one of the most useful tuning forms because it reports buffer activity in addition to execution behavior.

Common terms include:

- **shared hit** — required block was already in PostgreSQL shared buffers;
- **shared read** — block had to be read into shared buffers;
- **dirtied/written** — execution dirtied or wrote buffers where relevant;
- **temp read/written** — work spilled to temporary files.

A high hit count is not automatically "bad" and a read is not automatically "bad." Use buffer evidence to understand how much data the query touches and whether it is doing repeated or spill-heavy work.

## Structured formats

```sql
EXPLAIN (ANALYZE, BUFFERS, FORMAT JSON)
SELECT ...;
```

JSON, XML, and YAML formats are useful for tools and programmatic plan analysis. Text format is often easiest for humans learning interactively.

## Cost

Plans show estimated costs such as:

```text
cost=0.42..8.44
```

The first number is startup cost; the second is total estimated cost. These are **planner cost units**, not milliseconds.

Do not interpret `cost=100` as "100 ms."

Costs are useful mainly for understanding why the planner prefers one candidate plan over another under its model.

## Rows estimate

Compare estimated rows and actual rows.

If PostgreSQL estimated:

```text
rows=10
```

but actual was:

```text
rows=500000
```

that estimation error can push the planner toward an inappropriate join order, scan type, or memory strategy.

Possible causes include:

- stale statistics;
- correlated columns;
- skewed data;
- parameter-sensitive distributions;
- expressions the planner cannot estimate well;
- missing extended statistics.

Before adding random indexes, understand why the estimate is wrong.

## Sequential scan is not bad

```text
Seq Scan
```

is often the correct plan when:

- the table is small;
- a large percentage of rows is needed;
- no useful selective index exists;
- rows are so widely distributed that random heap access would cost more;
- a parallel sequential scan can process a large relation efficiently.

Do not try to eliminate every sequential scan.

## Index scan

```text
Index Scan using idx_orders_customer_id
```

An index scan is often effective for selective lookups where the index can identify a relatively small set of rows and heap visits remain affordable.

Check:

- `Index Cond` — predicates used to navigate/filter through the index;
- `Filter` — predicates evaluated after rows are fetched;
- rows removed by filters;
- heap access and buffer counts.

## Index-only scan

An index-only scan can return required columns from the index without visiting the heap for many tuples, provided the index contains the needed data and visibility information allows it.

```text
Index Only Scan using idx_orders_customer_created
```

"Index only" does not guarantee **zero** heap fetches; MVCC visibility can still require heap checks.

## Bitmap scan

A bitmap plan often appears as:

```text
Bitmap Heap Scan
  -> Bitmap Index Scan
```

It is useful when more rows match than a simple index scan would fetch efficiently but fewer than justify reading the whole table.

Conceptually:

1. identify matching heap locations from one or more indexes;
2. build/merge a bitmap of needed pages;
3. fetch heap pages in a more page-friendly pattern.

Bitmap operations can also combine multiple indexes with bitmap `AND`/`OR` strategies.

## Nested loop

A nested loop takes rows from an outer input and executes/probes the inner input for each relevant outer row.

Excellent when:

- the outer side is small;
- the inner side has a cheap index lookup;
- only a small result is required.

Potential disaster:

```text
outer rows = 500,000
inner index/scan loops = 500,000
```

A bad row estimate can turn a normally excellent nested loop into repeated expensive work.

## Hash join

A hash join is mainly for equality joins. PostgreSQL typically builds a hash table from one input and probes it with rows from the other.

Conceptual shape:

```text
Hash Join
  Hash Cond: (o.customer_id = c.customer_id)
  -> Seq Scan on orders o
  -> Hash
       -> Seq Scan on customers c
```

Good fit:

- larger unsorted inputs;
- equality join;
- hash table fits reasonably in memory or batches acceptably.

Investigate excessive batching/temp I/O when the hash structure exceeds memory expectations.

## Merge join

A merge join walks two inputs ordered by the join keys.

Good fit when:

- inputs are already ordered by useful indexes; or
- sorting them is cheaper than alternative join strategies; and
- the join condition supports merge semantics, commonly equality.

A merge join can be very efficient for large ordered sets, but the required sorts can dominate if no useful ordering exists.

## Sort spilling to disk

Runtime plans can reveal disk-based sorts or temporary file activity.

Possible tuning areas:

- query design;
- an index supporting required ordering;
- reducing rows before sort;
- reducing row width;
- carefully increasing `work_mem` for the relevant operation/session.

Do not blindly raise global `work_mem`: one complex query can have several memory-consuming plan nodes, and many queries run concurrently.

## Planning time vs execution time

`EXPLAIN ANALYZE` reports planning and execution time separately. Most OLTP queries spend far more time executing than planning, but very complex dynamically generated SQL with many joins/partitions can also have meaningful planning overhead.

Optimize the measured bottleneck rather than assuming every slow request is execution I/O.

## A practical EXPLAIN checklist

Ask:

1. What is the slowest node?
2. Are row estimates close to actual rows?
3. Is a huge table being scanned unnecessarily?
4. Are many rows removed by filter?
5. Is a nested loop repeating an expensive inner operation?
6. Are sorts or hashes spilling?
7. Are indexes appropriate?
8. Is the query returning too much data?
9. Are statistics fresh?
10. Is the issue actually lock waiting rather than execution?

---

# 29. Statistics and ANALYZE

The query planner needs estimates about data distribution.

PostgreSQL collects statistics such as:

- approximate distinct values;
- most common values;
- histograms;
- null fractions;
- correlations.

## ANALYZE

```sql
ANALYZE orders;
```

Updates statistics for planning.

Often autovacuum's analyze function handles this automatically.

## VACUUM ANALYZE

```sql
VACUUM (ANALYZE) orders;
```

Performs vacuum work and updates planner statistics.

## Statistics target

For columns with complex distributions, increasing the statistics target can improve estimates.

```sql
ALTER TABLE orders
ALTER COLUMN status SET STATISTICS 500;
```

Then:

```sql
ANALYZE orders;
```

Higher targets increase planning-statistics detail and analysis cost/storage.

## Extended statistics

Columns can be correlated.

Example:

```text
country = 'IN'
state = 'Maharashtra'
```

Treating predicates independently may produce poor estimates.

Create extended statistics:

```sql
CREATE STATISTICS st_customer_location
(dependencies)
ON country, state
FROM customers;

ANALYZE customers;
```

Other extended-statistics kinds can capture distinct combinations and most-common-value combinations.

## Inspect column statistics

```sql
SELECT *
FROM pg_stats
WHERE tablename = 'orders';
```

Use this for diagnosis; do not build applications that depend on undocumented internal implementation details.

---

# 30. VACUUM, autovacuum, bloat, and freeze

This topic is essential for PostgreSQL production administration.

## Why VACUUM exists

Because PostgreSQL uses MVCC, updates and deletes leave old tuple versions that eventually become dead.

`VACUUM`:

- marks space from dead tuples reusable;
- updates visibility information;
- helps index-only scans;
- performs transaction ID maintenance;
- prevents transaction ID wraparound problems.

## Regular VACUUM

```sql
VACUUM orders;
```

Normal vacuum does not usually shrink the table file back to the operating system. It makes space reusable inside the relation.

## VACUUM ANALYZE

```sql
VACUUM (ANALYZE) orders;
```

Also refreshes planner statistics.

## VACUUM VERBOSE

```sql
VACUUM (VERBOSE, ANALYZE) orders;
```

Useful for understanding what vacuum did.

## VACUUM FULL

```sql
VACUUM FULL orders;
```

Rewrites the table and can return space to the OS, but requires an exclusive table lock and extra disk work.

Do **not** schedule `VACUUM FULL` routinely as normal maintenance.

## Autovacuum

Autovacuum automatically performs vacuum and analyze work based on activity thresholds and configuration.

Disabling autovacuum globally is usually a serious mistake.

## Why a busy table may need per-table tuning

Default thresholds may not be ideal for:

- huge tables with small hot subsets;
- tables with extremely high update rates;
- queue tables;
- append/delete workloads.

Example table storage parameters:

```sql
ALTER TABLE jobs SET (
    autovacuum_vacuum_scale_factor = 0.02,
    autovacuum_analyze_scale_factor = 0.01
);
```

Values are examples, not universal recommendations. Measure your workload.

## Bloat

Bloat means a relation occupies significantly more space than useful live data requires.

Possible contributors:

- frequent updates/deletes;
- long transactions blocking cleanup;
- insufficient vacuuming;
- indexes that grow through churn;
- workload patterns and page fragmentation.

Do not diagnose bloat only from "database size is large." Measure live/dead tuples and relation characteristics.

## Fillfactor

```sql
ALTER TABLE frequently_updated
SET (fillfactor = 80);
```

A lower fillfactor reserves space on pages for updates, which can help HOT updates in suitable workloads.

Trade-off: more disk space and fewer rows per page.

## Transaction ID wraparound

PostgreSQL transaction IDs are finite and their age must be managed.

Vacuum "freezes" old tuples so visibility remains safe as transaction IDs cycle.

This is one reason autovacuum is not optional housekeeping—it protects correctness.

## Long-running transactions

A transaction that stays open for hours or days can prevent cleanup of old row versions.

Find long transactions:

```sql
SELECT
    pid,
    usename,
    state,
    xact_start,
    query
FROM pg_stat_activity
WHERE xact_start IS NOT NULL
ORDER BY xact_start;
```

Pay special attention to `idle in transaction` sessions.

---

# 31. Partitioning

Partitioning splits one logical table into smaller physical partitions.

PostgreSQL provides declarative partitioning.

## Why partition?

Good reasons include:

- very large tables;
- efficient data lifecycle management;
- dropping old data by partition;
- queries naturally restricted by partition key;
- maintenance isolation;
- very large append-heavy time-series/event tables.

Bad reason:

> "The table has one million rows, so it must be partitioned."

A well-indexed non-partitioned table can handle far more than that. Partition only when it solves a measurable problem.

## Range partitioning

```sql
CREATE TABLE events (
    event_id bigint NOT NULL,
    created_at timestamptz NOT NULL,
    payload jsonb
) PARTITION BY RANGE (created_at);
```

Create partitions:

```sql
CREATE TABLE events_2026_08
PARTITION OF events
FOR VALUES FROM ('2026-08-01') TO ('2026-09-01');
```

```sql
CREATE TABLE events_2026_09
PARTITION OF events
FOR VALUES FROM ('2026-09-01') TO ('2026-10-01');
```

## List partitioning

```sql
CREATE TABLE customers_by_region (
    customer_id bigint,
    region_code text NOT NULL
) PARTITION BY LIST (region_code);
```

```sql
CREATE TABLE customers_india
PARTITION OF customers_by_region
FOR VALUES IN ('IN');
```

## Hash partitioning

```sql
CREATE TABLE telemetry (
    device_id bigint NOT NULL,
    recorded_at timestamptz NOT NULL,
    value double precision
) PARTITION BY HASH (device_id);
```

```sql
CREATE TABLE telemetry_p0
PARTITION OF telemetry
FOR VALUES WITH (MODULUS 4, REMAINDER 0);
```

Create corresponding remainder partitions.

## Partition pruning

If a query restricts the partition key:

```sql
SELECT *
FROM events
WHERE created_at >= '2026-08-10'
  AND created_at <  '2026-08-11';
```

PostgreSQL can avoid scanning irrelevant partitions.

## Partition indexes

Indexes defined on a partitioned table coordinate corresponding indexes on partitions.

Understand how index creation and attachment behaves for your version, especially for large production tables.

## Drop old data cheaply

Instead of deleting hundreds of millions of rows:

```sql
DROP TABLE events_2024_01;
```

or detach first:

```sql
ALTER TABLE events
DETACH PARTITION events_2024_01;
```

This is a major advantage for retention-based systems.

## Partitioning mistakes

- thousands of tiny partitions;
- partition key unrelated to queries;
- forgetting default/future partitions;
- assuming global indexes exist like in some other RDBMSs;
- failing to automate partition creation;
- ignoring unique-constraint restrictions involving partition keys;
- partitioning before basic indexing/query tuning.

---

# 32. JSON and JSONB

PostgreSQL supports both `json` and `jsonb`.

## `json`

Stores JSON text with validation.

## `jsonb`

Stores a decomposed binary representation optimized for processing and indexing.

For most application querying, `jsonb` is the preferred type.

## Create table

```sql
CREATE TABLE products (
    product_id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    name text NOT NULL,
    attributes jsonb NOT NULL DEFAULT '{}'::jsonb
);
```

Insert:

```sql
INSERT INTO products (name, attributes)
VALUES (
    'Laptop',
    '{
       "brand": "ExampleTech",
       "ram_gb": 16,
       "ports": ["usb-c", "hdmi"]
    }'
);
```

## Extract JSON field

`->` returns JSON/JSONB:

```sql
SELECT attributes -> 'brand'
FROM products;
```

Possible result:

```text
"ExampleTech"
```

`->>` returns text:

```sql
SELECT attributes ->> 'brand'
FROM products;
```

Result:

```text
ExampleTech
```

## Nested path

```sql
SELECT attributes #>> '{dimensions,width}'
FROM products;
```

## Containment

```sql
SELECT *
FROM products
WHERE attributes @> '{"ram_gb":16}'::jsonb;
```

This operator is a common reason to add a GIN index.

## GIN index

```sql
CREATE INDEX idx_products_attributes
ON products USING gin (attributes);
```

## Key existence

```sql
SELECT *
FROM products
WHERE attributes ? 'brand';
```

## Update JSON with `jsonb_set`

```sql
UPDATE products
SET attributes = jsonb_set(
    attributes,
    '{ram_gb}',
    '32'::jsonb,
    true
)
WHERE product_id = 1;
```

## Remove a key

```sql
UPDATE products
SET attributes = attributes - 'deprecated_key'
WHERE product_id = 1;
```

## Build JSON

```sql
SELECT jsonb_build_object(
    'id', product_id,
    'name', name,
    'price', price
)
FROM products;
```

## Aggregate JSON

```sql
SELECT jsonb_agg(
    jsonb_build_object(
        'id', product_id,
        'name', name
    )
)
FROM products;
```

## SQL/JSON path

Modern PostgreSQL supports SQL/JSON path operations.

Example concept:

```sql
SELECT jsonb_path_query(
    '{"items":[{"price":10},{"price":50}]}'::jsonb,
    '$.items[*] ? (@.price > 20)'
);
```

Use SQL/JSON path when complex traversal/filtering is clearer than chaining operators.

## When JSONB is appropriate

Good uses:

- external API payload fragments;
- optional flexible metadata;
- vendor-specific attributes;
- audit snapshots;
- sparse configuration;
- fields whose schema genuinely varies.

## When JSONB is a bad replacement for relational modeling

Do not put everything into one JSONB column because "schema changes are hard."

If you frequently need:

- foreign keys;
- joins;
- strict data types;
- uniqueness;
- frequent filtering on stable attributes;
- relational constraints;

then ordinary columns/tables are usually better.

### Hybrid design

Often ideal:

```text
product_id       relational PK
sku              relational, unique
price            relational numeric
category_id      relational FK
attributes       jsonb for variable metadata
```

---

# 33. Arrays

PostgreSQL supports native arrays.

## Define an array column

```sql
CREATE TABLE articles (
    article_id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    title text NOT NULL,
    tags text[] NOT NULL DEFAULT '{}'
);
```

## Insert

```sql
INSERT INTO articles (title, tags)
VALUES (
    'PostgreSQL Indexing',
    ARRAY['postgresql', 'database', 'performance']
);
```

## Access element

PostgreSQL arrays are commonly 1-based:

```sql
SELECT tags[1]
FROM articles;
```

## Contains

```sql
SELECT *
FROM articles
WHERE tags @> ARRAY['postgresql'];
```

## Overlap

```sql
SELECT *
FROM articles
WHERE tags && ARRAY['postgresql', 'mysql'];
```

## ANY

```sql
SELECT *
FROM articles
WHERE 'postgresql' = ANY(tags);
```

## Unnest

```sql
SELECT article_id, unnest(tags) AS tag
FROM articles;
```

## GIN index for arrays

```sql
CREATE INDEX idx_articles_tags
ON articles USING gin(tags);
```

## Array vs child table

Array is good when elements are simple values belonging directly to one row.

Use a normalized child/junction table when elements need:

- their own attributes;
- foreign keys;
- independent lifecycle;
- strong uniqueness rules across entities;
- rich joins/reporting.

For product-to-category many-to-many relationships, a junction table is usually better than `category_ids bigint[]`.

---

# 34. Range and multirange types

Range types represent intervals.

Built-in examples include:

- `int4range`;
- `int8range`;
- `numrange`;
- `tsrange`;
- `tstzrange`;
- `daterange`.

## Example

```sql
SELECT daterange('2026-08-01', '2026-09-01', '[)');
```

`[)` means:

- include lower bound;
- exclude upper bound.

This convention is excellent for adjacent time periods because:

```text
[Aug 1, Sep 1)
[Sep 1, Oct 1)
```

have no overlap and no gap.

## Contains

```sql
SELECT daterange('2026-08-01', '2026-09-01', '[)')
       @> date '2026-08-17';
```

## Overlap

```sql
SELECT daterange('2026-08-01', '2026-09-01', '[)')
       && daterange('2026-08-15', '2026-08-20', '[)');
```

## Booking example

```sql
CREATE TABLE bookings (
    booking_id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    room_id bigint NOT NULL,
    booking_period tstzrange NOT NULL
);
```

Find bookings overlapping a requested interval:

```sql
SELECT *
FROM bookings
WHERE booking_period && tstzrange($1, $2, '[)');
```

Add GiST index:

```sql
CREATE INDEX idx_bookings_period
ON bookings USING gist (booking_period);
```

## Multirange

A multirange represents multiple noncontiguous ranges as one value.

Use cases:

- availability windows;
- scheduled maintenance intervals;
- membership periods with gaps;
- temporal coverage sets.

PostgreSQL 18 further enhances temporal constraints involving range semantics. See the version highlights section.

---

# 35. UUIDs

UUIDs are 128-bit identifiers.

They are useful when IDs must be generated independently across systems or should be hard to guess sequentially.

## UUID column

```sql
CREATE TABLE api_requests (
    request_id uuid PRIMARY KEY,
    payload jsonb NOT NULL
);
```

## PostgreSQL 18 UUIDv7

PostgreSQL 18 provides `uuidv7()`:

```sql
CREATE TABLE events (
    event_id uuid PRIMARY KEY DEFAULT uuidv7(),
    created_at timestamptz NOT NULL DEFAULT now()
);
```

UUIDv7 values are time-ordered, making them friendlier to index locality than purely random UUIDv4 values while retaining UUID characteristics.

## bigint vs UUID

### bigint identity

Advantages:

- compact;
- simple;
- efficient indexes;
- human-friendly debugging.

### UUID

Advantages:

- decentralized generation;
- easier merging across systems;
- non-sequential public identifiers;
- useful in distributed architectures.

Do not choose UUID automatically because an application is "modern." Choose based on system requirements.

---

# 36. Full-text search

PostgreSQL includes built-in full-text search (FTS).

It is more language-aware than simple `LIKE '%word%'` searching.

## Core concepts

- **document** → `tsvector`;
- **query** → `tsquery`;
- matching operator → `@@`.

## Simple example

```sql
SELECT to_tsvector('english', 'PostgreSQL makes database search powerful');
```

Query:

```sql
SELECT to_tsvector('english', 'PostgreSQL makes database search powerful')
       @@ plainto_tsquery('english', 'database search');
```

## Search table

```sql
SELECT article_id, title
FROM articles
WHERE to_tsvector(
        'english',
        coalesce(title, '') || ' ' || coalesce(body, '')
      )
      @@ plainto_tsquery('english', $1);
```

## Generated search vector

For repeated search, store or generate a `tsvector` depending on design/version capabilities.

Example:

```sql
ALTER TABLE articles
ADD COLUMN search_vector tsvector
GENERATED ALWAYS AS (
    to_tsvector(
        'english',
        coalesce(title, '') || ' ' || coalesce(body, '')
    )
) STORED;
```

Index:

```sql
CREATE INDEX idx_articles_search
ON articles USING gin(search_vector);
```

Search:

```sql
SELECT article_id, title
FROM articles
WHERE search_vector @@ websearch_to_tsquery('english', $1);
```

## Query constructors

- `plainto_tsquery` — simple words;
- `phraseto_tsquery` — phrase semantics;
- `websearch_to_tsquery` — web-search-like input;
- `to_tsquery` — explicit tsquery syntax.

## Ranking

```sql
SELECT
    title,
    ts_rank(search_vector, q) AS rank
FROM articles,
     websearch_to_tsquery('english', 'postgres database') AS q
WHERE search_vector @@ q
ORDER BY rank DESC;
```

## Highlighting

```sql
SELECT ts_headline(
    'english',
    body,
    websearch_to_tsquery('english', 'postgres database')
)
FROM articles;
```

## Full-text search vs external search engine

PostgreSQL FTS is excellent for many application search requirements.

Consider a specialized engine when you require sophisticated distributed search, advanced relevance tooling, very large independent search infrastructure, typo tolerance/fuzzy behavior beyond your PostgreSQL design, or search features your workload cannot efficiently support in-database.

Start with requirements and measurement rather than fashion.

---

# 37. Functions and procedures

PostgreSQL can run server-side routines.

## SQL function

```sql
CREATE FUNCTION add_tax(amount numeric, tax_rate numeric)
RETURNS numeric
LANGUAGE sql
IMMUTABLE
RETURN amount * (1 + tax_rate);
```

Use:

```sql
SELECT add_tax(100, 0.18);
```

Result:

```text
118.00
```

## Function inputs and outputs

A function can:

- accept parameters;
- return one scalar;
- return a row;
- return a set of rows;
- return `void`;
- use SQL or procedural languages.

## Function volatility categories

A function's volatility category is a **promise to the optimizer** about how its result can change. Incorrectly marking a function more stable than it really is can produce wrong or surprising behavior; it is not a performance hint to manipulate casually.

| Category | Promise | Typical examples/use |
|---|---|---|
| `IMMUTABLE` | same arguments always produce the same result under the relevant database semantics | pure calculations |
| `STABLE` | result may depend on database/session state but is stable within one statement | values such as current statement time; read-oriented lookup functions when semantics fit |
| `VOLATILE` | result may change between calls or may have side effects | `random()`, sequence operations, state-changing functions |

### `IMMUTABLE`

A pure arithmetic function can be immutable:

```sql
CREATE FUNCTION double_value(x integer)
RETURNS integer
LANGUAGE sql
IMMUTABLE
AS $$
    SELECT x * 2;
$$;
```

Because PostgreSQL may fold or precompute immutable expressions, never label a function `IMMUTABLE` if it reads mutable table state, depends on changing configuration in a way that affects the result, or otherwise can return different values for the same arguments.

### `STABLE`

A stable function may legitimately depend on state that is considered stable for one statement. This gives the planner more freedom than `VOLATILE` while not claiming timeless immutability.

### `VOLATILE`

`VOLATILE` is the default when you do not declare another category. Use it when results can change on successive calls or the function has effects that must not be optimized away/reordered under stronger assumptions.

Examples include concepts such as:

```sql
SELECT random();
SELECT nextval('invoice_number_seq');
```

### Why volatility matters

Volatility affects:

- constant folding/precomputation opportunities;
- how often PostgreSQL may evaluate an expression;
- whether expression indexes/generated-column expressions can legally use a function;
- snapshot/optimization assumptions.

Do not mark a function `IMMUTABLE` merely to make PostgreSQL accept it in an index or generated column. Fix the function semantics or choose a different design.

## Set-returning function

```sql
CREATE FUNCTION expensive_products(min_price numeric)
RETURNS TABLE(product_id bigint, name text, price numeric)
LANGUAGE sql
STABLE
AS $$
    SELECT product_id, name, price
    FROM products
    WHERE price >= min_price;
$$;
```

Use:

```sql
SELECT *
FROM expensive_products(5000);
```

## Procedure

Procedures are invoked with `CALL`.

```sql
CREATE PROCEDURE archive_old_logs(cutoff timestamptz)
LANGUAGE plpgsql
AS $$
BEGIN
    DELETE FROM logs
    WHERE created_at < cutoff;
END;
$$;
```

```sql
CALL archive_old_logs(now() - interval '1 year');
```

Functions and procedures differ in invocation and transaction-control capabilities. Choose based on required semantics rather than naming preference.

## Security definer

A function can execute with its owner's privileges using `SECURITY DEFINER`.

This is powerful and security-sensitive.

If using it:

- lock down executable privileges;
- use a safe `search_path`;
- schema-qualify sensitive objects;
- validate inputs;
- understand privilege escalation risks.

---

# 38. PL/pgSQL

PL/pgSQL is PostgreSQL's built-in procedural SQL language.

It adds:

- variables;
- conditions;
- loops;
- exception handling;
- dynamic SQL;
- procedural flow around SQL.

## Basic function

```sql
CREATE OR REPLACE FUNCTION order_label(p_total numeric)
RETURNS text
LANGUAGE plpgsql
IMMUTABLE
AS $$
BEGIN
    IF p_total >= 100000 THEN
        RETURN 'high-value';
    ELSIF p_total >= 10000 THEN
        RETURN 'medium-value';
    ELSE
        RETURN 'standard';
    END IF;
END;
$$;
```

## Variables

```sql
CREATE OR REPLACE FUNCTION customer_order_count(p_customer_id bigint)
RETURNS bigint
LANGUAGE plpgsql
STABLE
AS $$
DECLARE
    v_count bigint;
BEGIN
    SELECT count(*)
    INTO v_count
    FROM orders
    WHERE customer_id = p_customer_id;

    RETURN v_count;
END;
$$;
```

## `SELECT INTO`

Inside PL/pgSQL:

```sql
SELECT order_total
INTO v_total
FROM orders
WHERE order_id = p_order_id;
```

This PL/pgSQL `SELECT INTO` meaning should not be confused with SQL usages in other database systems that create a table.

## Loop

```sql
FOR r IN
    SELECT order_id
    FROM orders
    WHERE status = 'pending'
LOOP
    RAISE NOTICE 'Order %', r.order_id;
END LOOP;
```

## Exception handling

```sql
BEGIN
    -- risky work
EXCEPTION
    WHEN unique_violation THEN
        RAISE NOTICE 'Duplicate value';
END;
```

### Warning

Do not use exception handling as normal control flow when a direct SQL approach exists.

## Dynamic SQL

```sql
EXECUTE format(
    'SELECT count(*) FROM %I.%I',
    p_schema,
    p_table
)
INTO v_count;
```

Use `format()` with `%I` for identifiers and parameterization for values.

Never concatenate untrusted text into executable SQL.

## Set-based SQL vs loops

Prefer set-based SQL when possible.

Slow procedural pattern:

```text
for every row:
  query another table
  update one row
```

Often better:

```sql
UPDATE target t
SET value = s.value
FROM source s
WHERE s.id = t.id;
```

The database optimizer is built to process sets efficiently.

---

# 39. Triggers and event triggers

A trigger automatically runs a function when a table event occurs.

## Common trigger events

- `INSERT`;
- `UPDATE`;
- `DELETE`;
- `TRUNCATE` in applicable trigger forms.

Timing can include:

- `BEFORE`;
- `AFTER`;
- `INSTEAD OF` for suitable views.

## Audit timestamp trigger

```sql
CREATE OR REPLACE FUNCTION set_updated_at()
RETURNS trigger
LANGUAGE plpgsql
AS $$
BEGIN
    NEW.updated_at := now();
    RETURN NEW;
END;
$$;
```

```sql
CREATE TRIGGER trg_products_updated_at
BEFORE UPDATE ON products
FOR EACH ROW
EXECUTE FUNCTION set_updated_at();
```

## OLD and NEW

Inside row triggers:

- `OLD` represents the previous row where applicable;
- `NEW` represents the new row where applicable.

Example audit:

```sql
CREATE OR REPLACE FUNCTION audit_price_change()
RETURNS trigger
LANGUAGE plpgsql
AS $$
BEGIN
    IF NEW.price IS DISTINCT FROM OLD.price THEN
        INSERT INTO product_price_audit(
            product_id,
            old_price,
            new_price,
            changed_at
        )
        VALUES (
            OLD.product_id,
            OLD.price,
            NEW.price,
            now()
        );
    END IF;

    RETURN NEW;
END;
$$;
```

## Statement vs row triggers

- `FOR EACH ROW` runs per affected row;
- statement-level trigger runs once per statement.

For large updates, per-row trigger cost can be significant.

## Transition tables

For suitable triggers, transition relations can expose sets of old/new rows to statement-level logic.

This can be more efficient than row-by-row auditing for some designs.

## Trigger risks

Triggers hide behavior from ordinary application SQL.

Possible problems:

- unexpected writes;
- recursive effects;
- performance surprises;
- lock/deadlock complexity;
- harder debugging;
- business logic duplicated across application and database.

Use triggers for rules that truly benefit from database-level automatic enforcement.

## Event triggers

Event triggers react to database DDL events rather than ordinary table row changes.

They can be used for:

- schema-change auditing;
- governance;
- blocking certain DDL patterns.

They are powerful administrative tools and can break deployments if written incorrectly.

---

# 40. Extensions

Extensions package additional PostgreSQL functionality.

## List available extensions

```sql
SELECT name, default_version, installed_version
FROM pg_available_extensions
ORDER BY name;
```

## Install extension

```sql
CREATE EXTENSION IF NOT EXISTS pg_trgm;
```

## List installed extensions

Inside `psql`:

```text
\dx
```

or SQL:

```sql
SELECT *
FROM pg_extension;
```

## Useful examples

### `pg_trgm`

Trigram-based similarity and indexing for text search patterns.

```sql
CREATE EXTENSION IF NOT EXISTS pg_trgm;

CREATE INDEX idx_customers_name_trgm
ON customers USING gin (name gin_trgm_ops);
```

Can accelerate suitable `LIKE`/`ILIKE` and similarity searches.

### `citext`

Case-insensitive text semantics.

Before using it, decide whether database collation and application identity rules match the extension's behavior.

### `btree_gist`

Provides B-tree-like operator classes usable in GiST, especially helpful in exclusion constraints involving scalar values plus ranges.

### `pg_stat_statements`

Tracks aggregated SQL execution statistics and is extremely useful for production performance analysis.

It normally requires server configuration and extension creation.

```sql
CREATE EXTENSION pg_stat_statements;
```

### PostGIS

A major external extension adding geospatial data types, functions, and indexes.

Use it for serious GIS/geospatial workloads rather than storing latitude/longitude only as unrelated numeric columns when spatial operations are required.

## Extension security

Extensions execute database/server-side code or install objects.

Only install trusted extensions from reputable sources, use compatible versions, and include them in upgrade/backup planning.

---
# 41. Foreign Data Wrappers

Foreign Data Wrappers (FDWs) let PostgreSQL access external data sources as foreign tables.

A common built-in-contrib example is `postgres_fdw`, which connects one PostgreSQL database/server to another.

## Conceptual flow

```text
Local PostgreSQL
      |
      | Foreign Data Wrapper
      v
Remote PostgreSQL / external system
```

## PostgreSQL-to-PostgreSQL example

```sql
CREATE EXTENSION postgres_fdw;
```

Create server definition:

```sql
CREATE SERVER remote_sales
FOREIGN DATA WRAPPER postgres_fdw
OPTIONS (
    host '10.0.0.20',
    dbname 'sales_db',
    port '5432'
);
```

Create user mapping:

```sql
CREATE USER MAPPING FOR app_user
SERVER remote_sales
OPTIONS (
    user 'remote_reader',
    password 'secret'
);
```

In production, manage credentials securely; do not place secrets casually in scripts or source control.

Import schema:

```sql
IMPORT FOREIGN SCHEMA public
LIMIT TO (orders, customers)
FROM SERVER remote_sales
INTO remote_sales_schema;
```

Query:

```sql
SELECT *
FROM remote_sales_schema.orders
LIMIT 10;
```

## Why use an FDW?

- occasional cross-server joins;
- phased migrations;
- data federation;
- querying archives;
- integrating external systems.

## Limitations and risks

Remote access adds:

- network latency;
- distributed failure modes;
- remote planner limitations;
- authentication complexity;
- transaction semantics you must understand;
- possible large data transfer if predicates cannot be pushed down.

Use `EXPLAIN` to verify what work is executed remotely.

---

# 42. COPY, import, and export

`COPY` is PostgreSQL's high-performance bulk data transfer command.

## Import CSV server-side

```sql
COPY customers(name, email)
FROM '/data/customers.csv'
WITH (
    FORMAT csv,
    HEADER true
);
```

The file path is interpreted on the **database server** and requires appropriate server-side privileges.

## Export CSV server-side

```sql
COPY (
    SELECT customer_id, name, email
    FROM customers
    WHERE active = true
)
TO '/data/active_customers.csv'
WITH (
    FORMAT csv,
    HEADER true
);
```

## `\copy` in psql

`\copy` reads/writes files from the client machine running `psql`.

```text
\copy customers(name, email) FROM 'customers.csv' CSV HEADER
```

This distinction solves many beginner permission/path problems.

## STDIN / STDOUT

```sql
COPY customers(name, email)
FROM STDIN
WITH (FORMAT csv);
```

Applications and drivers can stream data efficiently using PostgreSQL's COPY protocol.

## Bulk loading strategy

For large controlled imports:

1. validate the source format;
2. load into a staging table;
3. inspect rejected/business-invalid rows;
4. transform types;
5. merge into final tables;
6. update statistics;
7. build or validate indexes/constraints at the correct stage for your workload.

Example staging table:

```sql
CREATE UNLOGGED TABLE customer_import_stage (
    name text,
    email text,
    birth_date_raw text
);
```

Then validate before inserting into the strongly typed production table.

## Why staging helps

Real CSV data may contain:

- invalid dates;
- empty strings where null is expected;
- duplicate IDs;
- bad encoding;
- unexpected delimiters;
- malformed numeric fields.

A permissive staging table isolates dirty external input from production constraints.

---

# 43. Roles, privileges, and security

PostgreSQL uses **roles** for both users and groups.

A role with `LOGIN` can connect like a user.

## Create login role

```sql
CREATE ROLE app_user
LOGIN
PASSWORD 'use-a-secret-management-process';
```

## Create group-style role

```sql
CREATE ROLE app_readonly;
```

Grant membership:

```sql
GRANT app_readonly TO analyst_user;
```

## Principle of least privilege

Applications should receive only the permissions they need.

Bad pattern:

```text
application connects as superuser
```

Better:

```text
migration role → DDL privileges
application role → required CRUD privileges
reporting role → read-only access
admin role → controlled operational privileges
```

## Database CONNECT

```sql
GRANT CONNECT ON DATABASE app_db TO app_user;
```

## Schema usage

```sql
GRANT USAGE ON SCHEMA app TO app_user;
```

## Table privileges

```sql
GRANT SELECT, INSERT, UPDATE, DELETE
ON app.orders
TO app_user;
```

Read-only:

```sql
GRANT SELECT
ON app.orders
TO reporting_role;
```

## Sequence privileges

Identity/sequence-backed inserts may require appropriate sequence privileges depending on ownership and security design.

```sql
GRANT USAGE, SELECT
ON SEQUENCE app.orders_order_id_seq
TO app_user;
```

## All tables in schema

```sql
GRANT SELECT
ON ALL TABLES IN SCHEMA reporting
TO reporting_role;
```

## Default privileges

A common mistake is granting existing tables but forgetting future tables.

```sql
ALTER DEFAULT PRIVILEGES
IN SCHEMA reporting
GRANT SELECT ON TABLES TO reporting_role;
```

### Important

Default privileges are associated with the role that creates future objects. Configure them under the correct object-owning role.

## Revoke public privileges deliberately

Review what `PUBLIC` can do in your databases and schemas.

Example:

```sql
REVOKE CREATE ON SCHEMA public FROM PUBLIC;
```

Modern defaults and upgrades can differ, so inspect actual privileges rather than assuming them.

## Role attributes

Examples:

```sql
CREATE ROLE dba LOGIN CREATEDB CREATEROLE;
```

Sensitive attributes include:

- `SUPERUSER`;
- `CREATEDB`;
- `CREATEROLE`;
- `REPLICATION`;
- `BYPASSRLS`.

Grant only when necessary.

## Ownership

Object ownership is different from privileges.

The owner usually has powerful control over an object, including the ability to alter/drop it and manage permissions.

A robust production pattern is often:

- objects owned by a non-login owner role;
- migration role can assume ownership role;
- runtime app role cannot own schema objects.

## SQL injection

Never build SQL by concatenating untrusted values.

Unsafe:

```python
sql = "SELECT * FROM users WHERE email = '" + email + "'"
```

Use parameters through your driver:

```text
SELECT * FROM users WHERE email = $1
```

Parameterization protects **values**, not arbitrary identifiers such as table names. Dynamic identifiers require controlled allowlists or safe identifier-quoting APIs.

---

# 44. Row-Level Security

Row-Level Security (RLS) can enforce which rows a role can see or modify.

This is useful for multi-tenant systems and sensitive data access.

## Enable RLS

```sql
ALTER TABLE invoices ENABLE ROW LEVEL SECURITY;
```

## Example tenant policy

Suppose the application sets a trusted session setting containing the current tenant.

```sql
CREATE POLICY tenant_isolation
ON invoices
USING (
    tenant_id = current_setting('app.tenant_id')::bigint
);
```

Now queries are filtered according to the policy for roles subject to RLS.

## INSERT/UPDATE checks

Use `WITH CHECK` to control rows a user may create or transform into.

```sql
CREATE POLICY tenant_write
ON invoices
FOR ALL
USING (
    tenant_id = current_setting('app.tenant_id')::bigint
)
WITH CHECK (
    tenant_id = current_setting('app.tenant_id')::bigint
);
```

## FORCE ROW LEVEL SECURITY

Table owners normally have special behavior regarding RLS. Where required:

```sql
ALTER TABLE invoices FORCE ROW LEVEL SECURITY;
```

Understand owner, superuser, and `BYPASSRLS` semantics before claiming RLS protects every possible connection.

## Multi-tenant request flow

Conceptually:

```sql
BEGIN;
SET LOCAL app.tenant_id = '42';
SELECT * FROM invoices;
COMMIT;
```

`SET LOCAL` limits the setting to the transaction.

This is much safer with connection pools than leaving tenant state attached to a reused session indefinitely.

## RLS strengths

- central database enforcement;
- protects multiple application query paths;
- can reduce accidental cross-tenant leaks;
- works with normal SQL once policies are configured.

## RLS risks

- policy complexity;
- performance overhead if predicates are poorly designed;
- privileged roles may bypass it;
- session-context mistakes;
- difficult debugging if developers forget policies are active.

Test policies with realistic roles, not only as a superuser.

---

# 45. Authentication and `pg_hba.conf`

Authentication answers:

> Who is allowed to connect, from where, to which database, and how must they prove identity?

Two major configuration areas are:

- server listening configuration;
- host-based authentication rules in `pg_hba.conf`.

## `listen_addresses`

Controls interfaces on which PostgreSQL accepts TCP/IP connections.

Example:

```text
listen_addresses = 'localhost'
```

or explicitly selected internal addresses.

Avoid listening on every interface unless network controls and requirements justify it.

## `pg_hba.conf`

Example conceptual rules:

```text
# TYPE  DATABASE  USER      ADDRESS          METHOD
local   all       all                        peer
host    app_db    app_user  10.10.0.0/16     scram-sha-256
```

Columns represent:

1. connection type;
2. database;
3. user;
4. client address where applicable;
5. authentication method;

Rules are evaluated in order; the first matching rule determines the authentication method.

## SCRAM

For password authentication, modern PostgreSQL deployments should prefer SCRAM-based password authentication over legacy MD5 password authentication.

PostgreSQL 18 deprecates MD5 password authentication and warns that support will be removed in a future major release.

## TLS/SSL

Production network connections may require TLS.

Server configuration, certificates, client verification mode, hostnames, and trust chains all matter.

Client-side SSL modes are important. A mode that merely encrypts without verifying server identity provides weaker protection than certificate and hostname verification.

## Reload configuration

Many configuration changes can be reloaded:

```sql
SELECT pg_reload_conf();
```

Some settings require restart.

Check parameter context:

```sql
SELECT name, setting, context
FROM pg_settings
WHERE name = 'shared_buffers';
```

## Common connection failure checklist

If you get "connection refused":

1. Is PostgreSQL running?
2. Is it listening on the expected port/interface?
3. Is the host/port correct?
4. Is a firewall blocking it?
5. Is a container/VM port exposed?

If you get `no pg_hba.conf entry`:

1. verify source IP;
2. verify database/user;
3. add the narrowest correct rule;
4. reload configuration.

If you get password failure:

1. verify role;
2. verify password;
3. verify authentication method;
4. verify client supports method;
5. ensure you are reaching the expected server.

---

# 46. Configuration and memory

PostgreSQL exposes many server parameters. Do not tune by copying random internet values.

Tune for:

- available RAM;
- CPU;
- storage;
- workload;
- concurrency;
- query shapes;
- latency goals;
- reliability requirements.

## Inspect setting

```sql
SHOW shared_buffers;
```

```sql
SELECT current_setting('work_mem');
```

## `shared_buffers`

Memory PostgreSQL uses for its shared buffer cache.

It is **not** the only cache. The operating system also caches filesystem data.

Avoid simplistic rules like "set it to exactly X% on every server." Use a sensible starting point for your environment, then measure.

## `work_mem`

Memory budget for certain query operations such as sorts and hashes.

Critical point:

> `work_mem` is not a single global pool per server.

A complex query can use multiple work-memory allocations, and many queries can run concurrently.

A very high global value can exhaust RAM under load.

Set locally for one heavy report when appropriate:

```sql
BEGIN;
SET LOCAL work_mem = '256MB';
-- run controlled report
COMMIT;
```

The exact value is workload-specific.

## `maintenance_work_mem`

Memory for maintenance operations such as some index creation and vacuum-related work.

Maintenance tasks are different from ordinary query sorts, so this can often be larger than `work_mem`, subject to concurrency.

## `effective_cache_size`

Planner estimate of how much cache is likely available across PostgreSQL and OS caching.

It does not allocate that amount of memory.

## `max_connections`

Maximum client connections.

Raising this substantially increases resource pressure and is often inferior to connection pooling.

## `statement_timeout`

Abort statements that exceed a duration.

```sql
SET statement_timeout = '5s';
```

Useful as an application safety guard, but different workloads may need different limits.

## `lock_timeout`

Abort if waiting too long to acquire a lock.

```sql
SET lock_timeout = '2s';
```

Useful for migrations that should fail instead of blocking production traffic for a long time.

## `idle_in_transaction_session_timeout`

Helps terminate sessions that sit idle inside a transaction too long.

This can protect vacuum and concurrency, but choose a value compatible with real application behavior.

## Configuration levels

Settings can be applied at multiple levels, including:

- server configuration;
- database;
- role;
- role-in-database combinations;
- session;
- transaction-local scope.

Example:

```sql
ALTER ROLE reporting_user SET statement_timeout = '2min';
```

---

# 47. Connections and pooling

Opening a PostgreSQL connection has cost, and each backend consumes server resources.

Web applications often use a **connection pool**.

## Application-side pooling

Most language ecosystems provide pools:

- Java: HikariCP and framework pools;
- Node.js: driver pools;
- Python: framework/driver pools;
- .NET: provider-managed pooling;
- PHP: architecture-dependent persistent/managed connections.

## External pooler

PgBouncer is a popular external connection pooler.

Common modes conceptually include:

- session pooling;
- transaction pooling;
- statement pooling.

Each mode has compatibility trade-offs with session state.

## Why pooling helps

Suppose:

```text
5 application instances × 500 possible web requests
```

Opening 2,500 database backends may be unnecessary.

Instead, the application can multiplex work over a smaller number of active database connections.

## Pool sizing

Bigger is not automatically better.

Too many active database sessions cause:

- CPU context switching;
- memory pressure;
- lock contention;
- storage saturation;
- worse tail latency.

Benchmark actual throughput and latency.

## Pooling and session state

Transaction pooling can break assumptions about session persistence.

Be careful with:

- temporary tables;
- session advisory locks;
- `SET` values that must persist across transactions;
- prepared statement behavior depending on pooler/version/config;
- LISTEN/NOTIFY;
- session-scoped tenant context.

Prefer transaction-scoped state such as `SET LOCAL` when compatible with your design.

---

# 48. Write-Ahead Logging

Write-Ahead Logging (WAL) is central to PostgreSQL durability and replication.

## Core idea

Before changed database pages need to be written to their final data files, PostgreSQL records enough information in WAL to recover changes after a crash.

Conceptually:

```text
Transaction changes
      |
      v
WAL records made durable
      |
      v
COMMIT acknowledged
      |
      v
Data pages can be flushed later
```

## Why WAL matters

WAL supports:

- crash recovery;
- physical replication;
- point-in-time recovery;
- backup consistency;
- logical decoding foundations.

## Checkpoints

A checkpoint establishes a recovery point and coordinates flushing dirty pages.

Too-frequent checkpoints can produce heavy I/O. Too-infrequent checkpoints can increase recovery time and WAL/storage requirements.

PostgreSQL tunes checkpoint behavior through parameters such as WAL sizing and checkpoint timing controls.

## `synchronous_commit`

This setting affects when PostgreSQL reports commit success relative to WAL durability/replication behavior.

Changing it is a durability decision, not a generic performance trick.

## `fsync`

Disabling `fsync` can risk unrecoverable corruption after crashes or power loss.

Do not disable durability settings in production just because a benchmark becomes faster.

## WAL volume

Heavy WAL can be generated by:

- bulk writes;
- index creation;
- full-page images;
- large updates/deletes;
- vacuum-related operations under certain circumstances;
- logical replication requirements.

Monitor WAL when planning replication bandwidth and archive storage.

---

# 49. Backup and restore

A backup is only useful if it can be restored.

Production backup planning must define:

- **RPO** — how much data loss is acceptable;
- **RTO** — how long recovery may take;
- backup frequency;
- retention;
- offsite copies;
- encryption;
- restore testing;
- disaster scenarios.

## Logical backup with `pg_dump`

Custom format:

```bash
pg_dump -h localhost -U postgres -d app_db -Fc -f app_db.dump
```

Benefits:

- portable logical representation;
- selective restore;
- parallel restore support for suitable formats;
- useful for migrations and smaller/medium databases.

## Restore custom dump

Create target database first when appropriate:

```bash
createdb -U postgres app_db_restore
```

Then:

```bash
pg_restore -U postgres -d app_db_restore app_db.dump
```

## Parallel restore

```bash
pg_restore -U postgres -d app_db_restore -j 4 app_db.dump
```

Choose job count based on CPU, storage, and schema characteristics.

## Plain SQL dump

```bash
pg_dump -U postgres -d app_db > app_db.sql
```

Restore:

```bash
psql -U postgres -d app_db_restore -f app_db.sql
```

## `pg_dumpall`

Dumps all databases plus cluster-wide objects in SQL form.

```bash
pg_dumpall -U postgres > cluster.sql
```

For large systems, many administrators use per-database `pg_dump` plus separate handling of globals instead of one huge all-in-one dump.

Dump globals:

```bash
pg_dumpall -U postgres --globals-only > globals.sql
```

## Physical base backup

`pg_basebackup` takes a physical copy suitable for replication/base-backup workflows.

Example concept:

```bash
pg_basebackup \
  -h primary-db \
  -U replicator \
  -D /backup/base \
  -Fp \
  -Xs \
  -P
```

Exact options should be chosen for your recovery architecture.

## Logical vs physical backup

| Property | Logical | Physical |
|---|---|---|
| Tool examples | `pg_dump` | `pg_basebackup` / filesystem-aware backup tools |
| Select individual tables | Yes | Not as ordinary logical restore |
| Cross-major portability | Often useful | Physical format tied to major/server compatibility rules |
| Large-cluster recovery speed | Can be slow | Often faster base restoration |
| PITR foundation | No by itself | Yes with WAL archiving |

## Backup mistakes

- keeping backup on same disk only;
- never testing restore;
- assuming replication is backup;
- not backing up roles/permissions;
- ignoring extensions;
- not measuring restore duration;
- losing WAL needed for PITR;
- storing unencrypted sensitive dumps insecurely.

## Replication is not backup

If a user runs:

```sql
DROP TABLE critical_data;
```

physical replication can replicate that deletion immediately.

Backups provide historical recovery points; replicas provide availability/read scaling depending on design.

---

# 50. Point-in-time recovery

Point-in-time recovery (PITR) lets you restore a base backup and replay archived WAL until a chosen moment or recovery target.

## Example disaster

At 14:32:

```sql
DELETE FROM invoices;
```

At 14:33 you notice the mistake.

With a valid base backup and complete WAL archive, you may restore to shortly before the damaging transaction.

## Conceptual process

```text
Base Backup
    +
Archived WAL segments
    |
    v
Restore database state
    |
    v
Replay WAL
    |
    v
Stop at recovery target
```

## Archive mode concepts

A typical PITR design enables WAL archiving and defines how completed WAL files are safely copied to durable archive storage.

Configuration includes concepts such as:

```text
wal_level
archive_mode
archive_command or archive modules/tooling
```

Use proven backup software or carefully tested archive scripts. A broken archive command can silently destroy your recovery objective if not monitored.

## Recovery targets

PostgreSQL can recover based on targets such as:

- timestamp;
- named restore point;
- transaction-related target;
- LSN depending on recovery method.

## Restore point

Before a risky deployment:

```sql
SELECT pg_create_restore_point('before_major_release');
```

A restore point is only useful if your WAL archival/recovery chain is complete.

## PITR testing

Regularly prove:

1. base backup is readable;
2. archived WAL is complete;
3. a fresh server can restore it;
4. recovery stops at intended target;
5. applications can connect;
6. data validation passes;
7. actual RTO is acceptable.

---

# 51. Physical replication and high availability

Physical streaming replication sends WAL from a primary server to standby servers.

## Conceptual architecture

```text
                   +--> Standby A
Primary ----------|
                   +--> Standby B
```

Standbys replay physical WAL changes.

## Why use replicas?

- failover/high availability;
- read scaling for suitable read-only workloads;
- disaster recovery;
- geographic copies;
- backup offloading in some architectures.

## Replication role

```sql
CREATE ROLE replicator
WITH LOGIN REPLICATION PASSWORD 'managed-secret';
```

Configure authentication narrowly for replica hosts.

## WAL sender / receiver

The primary sends WAL. The standby receives and replays it.

Monitor both transport and replay state.

## Replication slots

A physical replication slot can prevent required WAL from being removed before a replica consumes it.

Useful, but dangerous if a replica disappears indefinitely: WAL can accumulate until disk fills.

Monitor slot lag and retained WAL.

## Synchronous vs asynchronous replication

### Asynchronous

Primary can acknowledge commit before standby confirms receipt/durability.

Advantages:

- lower write latency;
- primary can continue if replica is unavailable.

Risk:

- recent acknowledged transactions may be lost in certain primary-failure scenarios before replica receives them.

### Synchronous

Commit waits for configured standby confirmation level.

Advantages:

- stronger cross-server durability guarantees.

Trade-offs:

- increased latency;
- availability may depend on synchronous standby configuration.

## Read replicas

Standbys can serve read-only queries using hot standby.

Be aware of:

- replication lag;
- read-after-write inconsistency;
- recovery conflicts with long standby queries;
- read workload affecting standby replay/resource use.

## Failover

Failover promotes a standby to primary after primary failure.

A complete HA design requires more than streaming replication:

- failure detection;
- leader election/orchestration;
- fencing to prevent split brain;
- client routing;
- DNS/proxy/service discovery;
- rejoining the old primary;
- monitoring and runbooks.

PostgreSQL provides core replication primitives; production HA often includes external orchestration/tooling.

## Split brain

Two servers both accepting writes as primary can create divergent histories.

Preventing split brain is a critical HA responsibility.

---

# 52. Logical replication

Logical replication publishes logical row-level changes instead of copying physical block changes.

## Main objects

- **publisher**;
- **publication**;
- **subscriber**;
- **subscription**.

## Publication

On publisher:

```sql
CREATE PUBLICATION sales_pub
FOR TABLE customers, orders;
```

## Subscription

On subscriber:

```sql
CREATE SUBSCRIPTION sales_sub
CONNECTION 'host=publisher dbname=app_db user=replicator password=secret'
PUBLICATION sales_pub;
```

Protect connection strings and secrets in real deployments.

## Uses

- selective table replication;
- major-version migrations;
- data distribution;
- feeding reporting systems;
- consolidating selected data;
- zero/low-downtime migration patterns.

## Replica identity

Updates/deletes need a way to identify rows on the subscriber.

Primary keys are strongly recommended for logically replicated mutable tables.

Where necessary:

```sql
ALTER TABLE some_table REPLICA IDENTITY FULL;
```

This increases WAL information and should not replace proper key design casually.

## DDL is different from data replication

Logical replication does not mean every schema change magically stays synchronized in every topology/version.

Plan schema changes explicitly and verify version-specific capabilities.

## Conflict planning

Standard logical replication is typically designed around a controlled write topology. If multiple nodes can modify the same logical data, conflict handling becomes a serious architectural concern.

---

# 53. Monitoring and system catalogs

PostgreSQL exposes rich statistics views and system catalogs.

## `pg_stat_activity`

See current sessions:

```sql
SELECT
    pid,
    usename,
    datname,
    client_addr,
    state,
    wait_event_type,
    wait_event,
    query_start,
    query
FROM pg_stat_activity
ORDER BY query_start NULLS LAST;
```

## Active queries

```sql
SELECT
    pid,
    now() - query_start AS runtime,
    wait_event_type,
    wait_event,
    query
FROM pg_stat_activity
WHERE state = 'active'
ORDER BY runtime DESC;
```

## Idle in transaction

```sql
SELECT
    pid,
    usename,
    now() - xact_start AS transaction_age,
    query
FROM pg_stat_activity
WHERE state = 'idle in transaction'
ORDER BY xact_start;
```

## Database statistics

```sql
SELECT *
FROM pg_stat_database;
```

Useful fields include transaction counts, temporary-file activity, deadlocks, blocks read/hit, and session-related statistics depending on version.

## Table statistics

```sql
SELECT
    relname,
    seq_scan,
    idx_scan,
    n_live_tup,
    n_dead_tup,
    last_autovacuum,
    last_autoanalyze
FROM pg_stat_user_tables
ORDER BY n_dead_tup DESC;
```

## Index statistics

```sql
SELECT
    relname AS table_name,
    indexrelname AS index_name,
    idx_scan,
    idx_tup_read,
    idx_tup_fetch
FROM pg_stat_user_indexes
ORDER BY idx_scan DESC;
```

## Database size

```sql
SELECT pg_size_pretty(pg_database_size(current_database()));
```

## Table total size

```sql
SELECT pg_size_pretty(pg_total_relation_size('orders'));
```

This includes associated indexes and TOAST data.

## Largest tables

```sql
SELECT
    schemaname,
    relname,
    pg_size_pretty(pg_total_relation_size(relid)) AS total_size
FROM pg_catalog.pg_statio_user_tables
ORDER BY pg_total_relation_size(relid) DESC
LIMIT 20;
```

## `pg_stat_statements`

One of the best tools for identifying expensive SQL over time.

Example:

```sql
SELECT
    calls,
    total_exec_time,
    mean_exec_time,
    rows,
    query
FROM pg_stat_statements
ORDER BY total_exec_time DESC
LIMIT 20;
```

Interpretation:

- high total time → major total database cost;
- high mean time → individually slow;
- high calls × small cost → chatty application pattern;
- rows vs calls → result-volume clues.

## Cache hit ratio caution

A high cache hit ratio does not prove the system is healthy, and a lower value does not automatically mean "add RAM."

Analyze query latency, working set, storage, access patterns, and I/O together.

## Replication monitoring

On primary, inspect replication views such as:

```sql
SELECT *
FROM pg_stat_replication;
```

Monitor lag in bytes/time and distinguish send, write, flush, and replay progress as relevant.

## WAL and I/O monitoring

Modern PostgreSQL exposes increasingly detailed WAL and I/O statistics. PostgreSQL 18 also includes asynchronous-I/O-related monitoring such as `pg_aios` for its new AIO subsystem.

Use the views appropriate to your exact server version.

---

# 54. Logging and troubleshooting

A good PostgreSQL troubleshooter asks:

> Is this a query problem, lock problem, connection problem, resource problem, storage problem, vacuum problem, replication problem, or application problem?

## Logging categories

Useful server logging can include:

- connection/disconnection;
- errors;
- slow statements;
- lock waits;
- checkpoints;
- autovacuum activity;
- temporary files;
- statement durations;
- structured log details.

Avoid logging every statement in a very busy production database without considering sensitive data, storage volume, and performance.

## Slow query investigation workflow

1. Identify SQL from `pg_stat_statements` or logs.
2. Capture parameters or representative values safely.
3. Run `EXPLAIN (ANALYZE, BUFFERS)` in a safe environment.
4. Compare estimated vs actual rows.
5. Inspect indexes.
6. Check lock waits.
7. Check I/O and temp spills.
8. Check table statistics/vacuum health.
9. Fix query/schema/config according to evidence.
10. Re-measure.

## Blocking queries

A useful function:

```sql
SELECT pg_blocking_pids(pid)
FROM pg_stat_activity
WHERE pid = 12345;
```

Find blocked sessions:

```sql
SELECT
    a.pid AS blocked_pid,
    a.query AS blocked_query,
    pg_blocking_pids(a.pid) AS blocking_pids
FROM pg_stat_activity a
WHERE cardinality(pg_blocking_pids(a.pid)) > 0;
```

## Cancel vs terminate

Cancel current query:

```sql
SELECT pg_cancel_backend(12345);
```

Terminate session:

```sql
SELECT pg_terminate_backend(12345);
```

Use termination carefully. It rolls back the session's active transaction and may affect application behavior.

## Too many connections

Symptoms:

```text
FATAL: remaining connection slots are reserved...
```

Investigate:

- application connection leaks;
- pool sizing;
- idle sessions;
- slow queries occupying connections;
- transaction leaks;
- `max_connections` sizing;
- reserved admin access.

Do not immediately multiply `max_connections`.

## Disk full

A full filesystem can stop writes and cause severe failures.

Check growth sources:

- base table/index growth;
- `pg_wal` retention;
- abandoned replication slots;
- archive failures;
- logs;
- temporary files;
- backup staging;
- bloat.

## WAL explosion from replication slot

Inspect slots:

```sql
SELECT
    slot_name,
    slot_type,
    active,
    restart_lsn,
    confirmed_flush_lsn
FROM pg_replication_slots;
```

Unused slots must be handled deliberately; dropping a needed slot can break replication, but leaving an abandoned slot can fill disk.

## Autovacuum cannot keep up

Check:

- dead tuples;
- long transactions;
- autovacuum timestamps;
- table-specific thresholds;
- worker capacity;
- I/O limits;
- write rate.

Fix the cause rather than scheduling `VACUUM FULL` as a reflex.

## Query is suddenly slow

Possible causes:

- data distribution changed;
- stale stats;
- plan changed;
- parameter-sensitive plan behavior;
- index dropped/bloated;
- cache cold;
- table grew;
- lock wait;
- storage latency;
- background maintenance;
- more concurrency;
- new application query pattern.

Always compare before/after evidence.

---

# 55. Upgrading PostgreSQL

PostgreSQL distinguishes **major** and **minor** releases.

Starting with PostgreSQL 10:

```text
18.6
^^ ^
|  |
|  +-- minor release
+----- major release
```

## Minor upgrade

Example:

```text
18.5 → 18.6
```

Minor releases contain fixes and remain storage-compatible within the same major release. Read release notes and follow packaging/service procedures.

## Major upgrade

Example:

```text
17 → 18
```

The internal data format may change, so you cannot simply point the new server binaries at the old data directory.

Common major-upgrade approaches:

1. logical dump/restore;
2. `pg_upgrade`;
3. logical replication migration.

## Dump/restore

Advantages:

- clean logical rebuild;
- opportunity to reorganize;
- straightforward conceptually.

Disadvantage:

- can require long downtime on large databases.

## `pg_upgrade`

Designed for fast in-place-style major upgrades by reusing/copying/linking data files as supported instead of logically rewriting all data.

Typical planning includes:

- compatible extension versions;
- old/new binaries;
- checks;
- backup;
- application compatibility testing;
- post-upgrade steps;
- rollback strategy.

PostgreSQL 18 improves `pg_upgrade` by retaining optimizer statistics, reducing the need to rebuild all statistics from scratch immediately after upgrade.

## Logical replication upgrade

A common low-downtime pattern:

```text
Old primary
    |
    | logical replication
    v
New PostgreSQL major version
```

Then:

1. initial data sync;
2. continuous change replication;
3. validate;
4. stop/redirect writes briefly;
5. catch up;
6. switch applications;
7. monitor closely.

Sequences, DDL, large objects, extensions, and non-replicated objects require explicit planning depending on setup.

## Upgrade checklist

Before upgrade:

- read every intervening major release note;
- test application drivers/ORMs;
- inspect deprecated features;
- verify extensions;
- test backup restore;
- test upgrade on production-sized copy;
- benchmark critical queries;
- inspect collation/locale considerations;
- validate authentication changes;
- measure expected downtime.

After upgrade:

- run prescribed post-upgrade steps;
- check extension updates;
- monitor logs;
- validate row counts/business totals;
- run smoke tests;
- compare query plans/performance;
- monitor replication and backups;
- keep rollback decision window explicit.

---
# 56. Application development patterns

PostgreSQL is most useful when application code treats the database as a transactional system, not merely a remote key/value store.

## Use parameterized queries

Conceptual SQL:

```sql
SELECT user_id, email
FROM users
WHERE email = $1;
```

The driver sends the SQL template and the value separately.

### Why?

- prevents SQL injection through values;
- handles quoting/types correctly;
- can support prepared-statement efficiencies;
- makes intent clearer.

## Do not interpolate values

Unsafe idea:

```text
"SELECT * FROM users WHERE email = '" + userInput + "'"
```

A malicious value can change query structure.

## Transaction boundary belongs to a business action

Bad:

```text
HTTP request
  SQL update 1 commits
  external work fails
  SQL update 2 never happens
```

Better when both database writes form one invariant:

```text
BEGIN
  update 1
  update 2
COMMIT
```

If external services are involved, a database transaction cannot magically make the remote service atomic. Consider patterns such as outbox/inbox, idempotency, sagas, or compensating actions.

## Transactional outbox pattern

Problem:

```text
1. save order in DB
2. publish message to broker
```

What if step 1 commits but step 2 fails?

Store both the business change and an outbox event in one transaction:

```sql
BEGIN;

INSERT INTO orders (...)
VALUES (...)
RETURNING order_id;

INSERT INTO outbox_events (
    event_type,
    aggregate_id,
    payload
)
VALUES (
    'order.created',
    $1,
    $2::jsonb
);

COMMIT;
```

A separate worker reliably publishes unsent outbox rows.

This does not provide magic exactly-once delivery; consumers should generally be idempotent.

## Idempotency key

For payment/API retry safety:

```sql
CREATE TABLE payment_requests (
    idempotency_key text PRIMARY KEY,
    response_payload jsonb,
    created_at timestamptz NOT NULL DEFAULT now()
);
```

Insert once:

```sql
INSERT INTO payment_requests(idempotency_key)
VALUES ($1)
ON CONFLICT DO NOTHING
RETURNING idempotency_key;
```

The application can distinguish the first request from retries.

## Optimistic concurrency control

Add a version column:

```sql
ALTER TABLE documents
ADD COLUMN version bigint NOT NULL DEFAULT 1;
```

Update only expected version:

```sql
UPDATE documents
SET
    content = $1,
    version = version + 1
WHERE document_id = $2
  AND version = $3
RETURNING version;
```

If no row returns, somebody changed the document first.

This prevents silent lost updates without holding a row lock during user editing.

## Pessimistic locking

Use when business flow needs to lock current database state briefly:

```sql
BEGIN;

SELECT *
FROM inventory
WHERE product_id = $1
FOR UPDATE;

-- validate and update stock

COMMIT;
```

Keep the transaction short.

## N+1 query problem

Bad ORM behavior:

```text
SELECT * FROM orders LIMIT 100;
then 100 separate queries for customer
```

Better:

```sql
SELECT
    o.order_id,
    o.order_total,
    c.customer_id,
    c.name
FROM orders o
JOIN customers c
  ON c.customer_id = o.customer_id
LIMIT 100;
```

Or use ORM eager-loading that produces efficient SQL.

## Batch inserts

Instead of thousands of single-row network round trips, use:

- multi-row `INSERT`;
- `COPY`;
- driver batch APIs;
- staging tables.

## Don't fetch more than needed

Bad:

```sql
SELECT *
FROM huge_events;
```

Better:

```sql
SELECT event_id, event_type, created_at
FROM huge_events
WHERE account_id = $1
ORDER BY created_at DESC
LIMIT 100;
```

## Application time zones

Strong pattern:

- store real instants as `timestamptz`;
- convert/display in user-specific time zone;
- store a separate IANA zone name when recurring local-time rules depend on a location.

Example:

```sql
SELECT created_at AT TIME ZONE 'Asia/Kolkata'
FROM orders;
```

Understand whether the expression is producing a timestamp with or without time zone based on input type.

## Soft delete

Typical schema:

```sql
deleted_at timestamptz
```

Active rows:

```sql
WHERE deleted_at IS NULL
```

Partial index:

```sql
CREATE INDEX idx_customers_active_email
ON customers(email)
WHERE deleted_at IS NULL;
```

### Soft-delete trade-offs

- queries must consistently filter deleted rows;
- uniqueness rules become more complex;
- table/index size keeps growing;
- foreign-key semantics need design;
- privacy/retention requirements may require real deletion.

Use it deliberately, not automatically.

## Prepared statements and plan behavior

Prepared statements can reduce parse/plan overhead and are natural with parameterized drivers.

However, generic plans vs parameter-sensitive custom plans can behave differently for highly skewed data. If one parameter value returns 2 rows and another returns 20 million, investigate plan behavior rather than assuming prepared statements are always faster.

---

## 56.1 Python example with psycopg-style parameterization

Conceptual modern Python:

```python
with conn.transaction():
    row = conn.execute(
        """
        INSERT INTO customers (name, email)
        VALUES (%s, %s)
        RETURNING customer_id
        """,
        (name, email),
    ).fetchone()
```

Driver placeholder syntax varies by library. Follow the exact driver documentation; never replace parameters with manual string interpolation.

## 56.2 Node.js example

Common PostgreSQL Node drivers use positional placeholders:

```javascript
const result = await client.query(
  `SELECT user_id, email
   FROM users
   WHERE email = $1`,
  [email]
);
```

Transaction pattern:

```javascript
await client.query('BEGIN');
try {
  await client.query(/* ... */);
  await client.query(/* ... */);
  await client.query('COMMIT');
} catch (err) {
  await client.query('ROLLBACK');
  throw err;
}
```

Use a dedicated checked-out pool connection for the whole transaction; do not let each transaction statement randomly use a different pooled connection.

## 56.3 PHP PDO example

```php
$stmt = $pdo->prepare(
    'SELECT user_id, email FROM users WHERE email = :email'
);
$stmt->execute(['email' => $email]);
$user = $stmt->fetch();
```

Transaction:

```php
$pdo->beginTransaction();
try {
    // database operations
    $pdo->commit();
} catch (Throwable $e) {
    $pdo->rollBack();
    throw $e;
}
```

## 56.4 Java JDBC example

```java
String sql = "SELECT user_id, email FROM users WHERE email = ?";
try (PreparedStatement ps = connection.prepareStatement(sql)) {
    ps.setString(1, email);
    try (ResultSet rs = ps.executeQuery()) {
        // read rows
    }
}
```

Use a pool in server applications and explicitly manage transaction boundaries where multiple statements form one business action.

---

# 57. Database design and normalization

Good SQL cannot fully rescue a poorly designed data model.

## Start from entities and business rules

Example online shop:

```text
Customer places Order
Order contains OrderItem
OrderItem references Product
Order has Payment attempts
Product belongs to Categories
```

Ask:

- What uniquely identifies each entity?
- Which attributes are required?
- Which relationships are one-to-one, one-to-many, many-to-many?
- Which rules must always hold?
- Which historical facts must not change when master data changes?

## First Normal Form (1NF)

A practical beginner interpretation of 1NF is: model rows and columns so each column represents one value of the declared domain, and avoid repeating column groups that really represent multiple related facts.

Bad repeating columns:

```text
order_id
product_1
product_2
product_3
```

Problems:

- maximum product count is baked into the schema;
- every query needs special handling for each numbered column;
- foreign keys and quantities become awkward;
- adding a fourth product requires a schema change.

Better:

```text
orders
order_items
```

One order can then have any number of line-item rows.

Do not oversimplify 1NF into "arrays are always forbidden." PostgreSQL arrays can be valid domain values. The design question is whether the elements need independent identity, constraints, relationships, or frequent relational querying.

## Second Normal Form (2NF)

2NF matters primarily when a table has a **composite candidate key**. Non-key attributes should depend on the whole key, not only one part of it.

Suppose this table is keyed by `(student_id, course_id)`:

```text
enrollment
----------
student_id
course_id
student_name
course_title
grade
```

Dependencies:

```text
student_id -> student_name
course_id  -> course_title
(student_id, course_id) -> grade
```

`student_name` depends only on `student_id`, and `course_title` depends only on `course_id`. Keeping them in `enrollment` repeats facts and creates update anomalies.

Better design:

```text
students(student_id, student_name)
courses(course_id, course_title)
enrollments(student_id, course_id, grade)
```

Now `grade` belongs to the whole enrollment key, while student/course facts live with their own entities.

## Third Normal Form (3NF)

3NF removes important **transitive dependencies**: non-key facts should not be stored merely because they can be reached through another non-key fact when they really describe a separate entity.

Bad current-state order data:

```text
order_id
customer_id
customer_name
customer_current_phone
```

If `customer_name` and current phone are attributes of the customer entity, repeatedly copying them to every order causes anomalies:

- updating a phone requires changing many rows;
- different orders may disagree about the customer's current phone;
- deleting the only order could accidentally remove the only stored copy of customer data.

Better:

```text
customers(customer_id, name, current_phone)
orders(order_id, customer_id, ...)
```

### Historical snapshots are different

An invoice may intentionally store:

```text
billed_name
billed_address
billed_tax_id
```

because the invoice must preserve what was legally issued at that moment even if the customer's master data changes later.

That duplication is **not automatically bad normalization**; it is a different fact with historical meaning.

Normalization is about functional dependencies and semantics, not blindly eliminating repeated-looking values.

## BCNF and higher normal forms

**Boyce-Codd Normal Form (BCNF)** strengthens the dependency rule: every determinant should be a candidate key. BCNF matters in schemas with unusual overlapping candidate keys where a table can satisfy 3NF yet still permit anomalies.

Fourth and fifth normal forms deal with multivalued and join dependencies. They matter in specialized models, but most application developers get the largest practical benefit from correctly modeling entities/relationships and understanding 1NF → 3NF/BCNF.

Do not force a schema into theoretical forms without understanding the business facts being represented.

## Many-to-many relationship

Products and categories:

```sql
CREATE TABLE products (
    product_id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    name text NOT NULL
);

CREATE TABLE categories (
    category_id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    name text NOT NULL UNIQUE
);

CREATE TABLE product_categories (
    product_id bigint NOT NULL
        REFERENCES products(product_id)
        ON DELETE CASCADE,
    category_id bigint NOT NULL
        REFERENCES categories(category_id)
        ON DELETE CASCADE,
    PRIMARY KEY (product_id, category_id)
);
```

The junction table is not "extra complexity"; it is the relational representation of the fact that one product can have many categories and one category can contain many products.

## Natural key vs surrogate key

### Natural key

A real business value or combination that identifies the fact:

```text
country_code = IN
```

Natural keys can be excellent when they are compact, truly stable, and have unambiguous business ownership.

### Surrogate key

A synthetic identifier:

```text
customer_id = 12345
```

Surrogate keys can simplify references and decouple relationships from mutable business identifiers.

Often you use both:

```sql
customer_id bigint PRIMARY KEY,
email text UNIQUE NOT NULL
```

The surrogate key supports stable relationships; the unique business key enforces reality.

## Do not assume a primary key replaces all unique constraints

A user table may need:

```sql
PRIMARY KEY (user_id)
UNIQUE (email)
UNIQUE (external_identity_provider, external_subject)
```

Each constraint protects a different invariant.

## Practical normalization workflow

When reviewing a table, ask:

1. What fact does **one row** represent?
2. What candidate keys uniquely identify that fact?
3. For every non-key column, "what does this value depend on?"
4. Is the value about this entity, or about another entity referenced by it?
5. Is repeated data accidental duplication or an intentional historical snapshot?
6. Could one update require changing many rows to keep one logical fact consistent?
7. Could deleting one row accidentally erase the only copy of a different fact?

If those questions are unclear, the schema probably needs more modeling work.

## Denormalization

Denormalization intentionally duplicates or precomputes data for performance/read simplicity.

Examples:

- cached aggregate counters;
- materialized views;
- precomputed reporting tables;
- search vectors;
- event snapshots.

Only denormalize when:

1. normalized design is understood;
2. performance need is measured;
3. consistency strategy is explicit.

---

# 58. Common anti-patterns

## 1. Everything is `text`

Bad:

```text
price text
created_at text
is_active text
```

Problems:

- invalid values;
- poor sorting semantics;
- repeated casts;
- weak constraints;
- worse query/index behavior.

Use proper types.

## 2. Everything is JSONB

JSONB is powerful, not a replacement for modeling stable relationships and constraints.

## 3. No foreign keys "for performance"

Removing referential integrity can create orphan data and shift correctness into every application code path.

Measure FK costs; do not remove them by superstition.

## 4. Random indexes everywhere

Each index increases write and maintenance cost.

Index actual queries and constraints.

## 5. `SELECT *` in APIs

Problems:

- unnecessary data transfer;
- fragile response shape;
- accidental exposure of sensitive columns;
- prevents some covering-index benefits.

## 6. Application loops instead of joins

Avoid N+1 queries.

## 7. Long transactions

Long transactions hurt cleanup and concurrency.

## 8. No timeout strategy

One accidental report can consume resources for hours.

Use workload-appropriate statement/lock/transaction safety limits.

## 9. Superuser application connection

A compromised application should not automatically become database superuser.

## 10. No tested backups

"Backup completed" is not the same as "recovery works."

## 11. OFFSET for deep pagination

Use keyset pagination for large ordered feeds.

## 12. `NOT IN` with nullable source

Prefer `NOT EXISTS` where null behavior could matter.

## 13. Function on indexed column

```sql
WHERE lower(email) = $1
```

will not automatically use a plain B-tree index on `email` for that expression.

Use the right index/design.

## 14. Casting the column

```sql
WHERE order_id::text = $1
```

Often better:

```sql
WHERE order_id = $1::bigint
```

## 15. Assuming row order

Without `ORDER BY`, SQL result order is not guaranteed.

## 16. `LIMIT` without deterministic order

Bad:

```sql
SELECT * FROM orders LIMIT 10;
```

If "latest 10" is intended:

```sql
SELECT *
FROM orders
ORDER BY created_at DESC, order_id DESC
LIMIT 10;
```

## 17. Storing comma-separated IDs

Bad:

```text
category_ids = '1,5,8'
```

Use a junction table or, for truly array-like scalar data, a PostgreSQL array with clear semantics.

## 18. Using sequence IDs as gapless invoice numbers

Sequence gaps are expected. Legal/business document numbering may need separate controlled logic.

## 19. Blind `CASCADE`

`DROP ... CASCADE` and FK `ON DELETE CASCADE` are useful but can have wide effects.

## 20. Manual edits inside PostgreSQL data directory

Never manipulate database relation files directly as normal administration.

---

# 59. Performance tuning workflow

Performance tuning is a measurement process, not a list of magical settings.

## Layer 1: Is the problem real?

Define:

- p50/p95/p99 latency;
- throughput;
- affected endpoint/query;
- start time;
- frequency;
- user impact.

"Database is slow" is not specific enough.

## Layer 2: Check waits and saturation

Look at:

- CPU;
- memory pressure;
- disk latency/throughput;
- connection count;
- lock waits;
- WAL pressure;
- replication lag;
- temp file use.

## Layer 3: Find expensive SQL

Use:

- `pg_stat_statements`;
- application tracing;
- slow query logs;
- `pg_stat_activity` for current work.

Prioritize total impact:

```text
5 ms × 10 million calls
```

may matter more than:

```text
5 seconds × 2 calls
```

## Layer 4: Analyze plan

```sql
EXPLAIN (ANALYZE, BUFFERS)
...
```

Check:

- estimates;
- scan types;
- join choices;
- loops;
- rows removed;
- sorts;
- memory/disk behavior;
- execution time.

## Layer 5: Fix query/model/index

Possible changes:

- add correct index;
- remove unnecessary columns;
- rewrite subquery/join;
- reduce rows earlier;
- fix datatype mismatch;
- use partial/expression index;
- change pagination;
- precompute expensive reporting result;
- partition for real lifecycle/query reasons.

## Layer 6: Statistics/maintenance

Check:

- `ANALYZE` freshness;
- autovacuum;
- bloat;
- extended stats;
- long transactions.

## Layer 7: Configuration

Only after workload/query issues are understood, consider:

- memory settings;
- parallelism;
- checkpoint/WAL settings;
- autovacuum parameters;
- planner cost parameters in specialized cases;
- connection limits/pooling.

## Layer 8: Architecture

When one database instance is genuinely at limits:

- caching;
- read replicas;
- queueing;
- sharding at application/platform layer;
- archival;
- workload isolation;
- specialized analytical/search stores.

Do not start with architecture complexity when a missing index would solve the problem.

---

# 60. Real-world scenarios

## Scenario 1: E-commerce inventory decrement

### Requirement

Prevent selling stock below zero under concurrent purchases.

### Safe atomic update

```sql
UPDATE inventory
SET stock_qty = stock_qty - $1
WHERE product_id = $2
  AND stock_qty >= $1
RETURNING stock_qty;
```

If zero rows return, insufficient stock or missing product.

Why this is better than:

```text
SELECT stock
if enough:
  UPDATE stock
```

Two concurrent requests could both read the same old stock before updating.

The conditional update makes the check and change one atomic SQL statement.

---

## Scenario 2: Latest status for every invoice

Tables:

```text
invoices
invoice_status_history
```

Using `DISTINCT ON`:

```sql
SELECT DISTINCT ON (invoice_id)
    invoice_id,
    status,
    changed_at
FROM invoice_status_history
ORDER BY invoice_id, changed_at DESC, status_history_id DESC;
```

Alternative with window function:

```sql
WITH ranked AS (
    SELECT
        h.*,
        row_number() OVER (
            PARTITION BY invoice_id
            ORDER BY changed_at DESC, status_history_id DESC
        ) AS rn
    FROM invoice_status_history h
)
SELECT *
FROM ranked
WHERE rn = 1;
```

Use a supporting index such as:

```sql
CREATE INDEX idx_invoice_status_latest
ON invoice_status_history (
    invoice_id,
    changed_at DESC,
    status_history_id DESC
);
```

---

## Scenario 3: Worker job queue

Schema:

```sql
CREATE TABLE jobs (
    job_id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    payload jsonb NOT NULL,
    status text NOT NULL DEFAULT 'pending',
    available_at timestamptz NOT NULL DEFAULT now(),
    started_at timestamptz,
    worker_id text
);
```

Partial index:

```sql
CREATE INDEX idx_jobs_pending
ON jobs (available_at, job_id)
WHERE status = 'pending';
```

Claim job:

```sql
BEGIN;

WITH candidate AS (
    SELECT job_id
    FROM jobs
    WHERE status = 'pending'
      AND available_at <= now()
    ORDER BY available_at, job_id
    FOR UPDATE SKIP LOCKED
    LIMIT 1
)
UPDATE jobs j
SET
    status = 'processing',
    started_at = now(),
    worker_id = $1
FROM candidate c
WHERE j.job_id = c.job_id
RETURNING j.*;

COMMIT;
```

Production queues also need:

- retry count;
- retry delay;
- stuck-job recovery;
- idempotent processing;
- dead-letter handling;
- observability.

---

## Scenario 4: Multi-tenant SaaS

Schema:

```sql
CREATE TABLE projects (
    tenant_id bigint NOT NULL,
    project_id bigint GENERATED ALWAYS AS IDENTITY,
    name text NOT NULL,
    PRIMARY KEY (tenant_id, project_id)
);
```

Every tenant-scoped query includes tenant identity:

```sql
SELECT *
FROM projects
WHERE tenant_id = $1
  AND project_id = $2;
```

Defense in depth may add RLS.

Index design often begins with tenant key for tenant-scoped access:

```sql
CREATE INDEX idx_projects_tenant_name
ON projects (tenant_id, name);
```

Do not use a tenant ID supplied by an untrusted client without tying it to authenticated authorization context.

---

## Scenario 5: Financial ledger

Prefer an append-oriented journal instead of directly mutating a single balance as the only source of truth.

```sql
CREATE TABLE ledger_entries (
    entry_id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    account_id bigint NOT NULL,
    transaction_id uuid NOT NULL,
    amount numeric(18,2) NOT NULL,
    created_at timestamptz NOT NULL DEFAULT now()
);
```

Current balance:

```sql
SELECT account_id, sum(amount) AS balance
FROM ledger_entries
WHERE account_id = $1
GROUP BY account_id;
```

At scale, snapshots/materialized aggregates may supplement the immutable journal.

Key principles:

- exact numeric types;
- transactional double-entry rules where applicable;
- immutable audit trail;
- idempotency;
- strong constraints;
- reconciliation queries.

---

## Scenario 6: Audit history

Base table:

```sql
CREATE TABLE employees (
    employee_id bigint PRIMARY KEY,
    name text NOT NULL,
    salary numeric(12,2) NOT NULL
);
```

Audit table:

```sql
CREATE TABLE employee_audit (
    audit_id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    employee_id bigint NOT NULL,
    action text NOT NULL,
    old_row jsonb,
    new_row jsonb,
    changed_at timestamptz NOT NULL DEFAULT now(),
    changed_by text NOT NULL
);
```

A trigger can capture row changes. Ensure the audit system cannot be casually modified by the same low-privilege application role if the audit trail is security-sensitive.

---

## Scenario 7: Time-series events

```sql
CREATE TABLE device_events (
    device_id bigint NOT NULL,
    recorded_at timestamptz NOT NULL,
    temperature double precision,
    payload jsonb
) PARTITION BY RANGE (recorded_at);
```

Useful design tools:

- monthly/daily partitions based on volume;
- BRIN on naturally ordered time;
- B-tree `(device_id, recorded_at DESC)` for recent device history;
- retention by dropping partitions.

Do not create one partition per device unless scale/query/lifecycle evidence supports it.

---

## Scenario 8: Search-as-you-type

For names:

```sql
CREATE EXTENSION IF NOT EXISTS pg_trgm;

CREATE INDEX idx_customer_name_trgm
ON customers USING gin (name gin_trgm_ops);
```

Query:

```sql
SELECT customer_id, name
FROM customers
WHERE name ILIKE '%' || $1 || '%'
ORDER BY similarity(name, $1) DESC
LIMIT 20;
```

Measure query behavior with realistic input sizes.

---

## Scenario 9: Prevent overlapping appointments

```sql
CREATE EXTENSION IF NOT EXISTS btree_gist;

CREATE TABLE appointments (
    appointment_id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    doctor_id bigint NOT NULL,
    slot tstzrange NOT NULL,
    EXCLUDE USING gist (
        doctor_id WITH =,
        slot WITH &&
    )
);
```

This moves a race-prone business rule into a database constraint.

---

## Scenario 10: Daily revenue report

```sql
SELECT
    created_at::date AS sales_date,
    count(*) AS order_count,
    sum(order_total) AS revenue
FROM orders
WHERE status = 'paid'
  AND created_at >= $1
  AND created_at < $2
GROUP BY created_at::date
ORDER BY sales_date;
```

For very large data, consider:

- expression/index strategy;
- date-range partitioning;
- materialized aggregate tables;
- reporting replica;
- pre-aggregation.

---

# 61. PostgreSQL vs MySQL and SQL Server

This section helps learners moving between systems. It is intentionally conceptual; exact features evolve by version.

## PostgreSQL vs MySQL

### Auto-increment

PostgreSQL modern style:

```sql
id bigint GENERATED ALWAYS AS IDENTITY
```

MySQL commonly uses:

```text
AUTO_INCREMENT
```

### Case-insensitive search

PostgreSQL:

```sql
ILIKE
```

MySQL behavior often depends heavily on selected collation.

### JSON

Both support JSON capabilities, but operators, indexing, functions, and storage semantics differ.

Do not copy MySQL JSON SQL directly into PostgreSQL.

### Upsert

PostgreSQL:

```sql
INSERT ... ON CONFLICT ...
```

MySQL:

```text
INSERT ... ON DUPLICATE KEY UPDATE
```

### Backticks

PostgreSQL does not use MySQL backticks for identifiers.

PostgreSQL quoted identifier:

```sql
"Order"
```

Prefer lowercase unquoted identifiers.

### Boolean

PostgreSQL has a real `boolean` type.

### `LIMIT`

PostgreSQL:

```sql
LIMIT 10 OFFSET 20
```

Do not assume every vendor's alternate `LIMIT` syntax is portable.

## PostgreSQL vs SQL Server

### TOP

SQL Server commonly:

```text
SELECT TOP 10 ...
```

PostgreSQL:

```sql
SELECT ...
LIMIT 10;
```

### Identity

Both support identity concepts, but syntax and surrounding behavior differ.

### `GETDATE()`

PostgreSQL commonly:

```sql
now()
current_timestamp
```

### `ISNULL()`

PostgreSQL commonly uses:

```sql
COALESCE(...)
```

### Square brackets

SQL Server often quotes identifiers with:

```text
[ColumnName]
```

PostgreSQL SQL-standard quoting uses double quotes:

```sql
"ColumnName"
```

Again, avoid mixed-case quoted naming when possible.

### Cross-database references

SQL Server commonly supports multipart cross-database naming within an instance.

PostgreSQL databases are stronger connection boundaries. Schemas are the normal namespace inside one database; use FDWs or other integration for cross-database access.

## Portability rule

SQL is standardized, but every database has extensions and behavioral differences.

When migrating:

1. migrate schema intentionally;
2. convert data types;
3. rewrite vendor-specific SQL;
4. review transaction/isolation semantics;
5. review collations/case behavior;
6. test ORM dialect;
7. rebuild indexes strategically;
8. validate data and query plans.

---

# 62. Error-handling guide

PostgreSQL errors include SQLSTATE codes. Applications should often react to codes/categories instead of brittle full error-message text.

## Common SQLSTATE codes

| SQLSTATE | Condition | Typical application response |
|---|---|---|
| `23505` | `unique_violation` | map expected duplicate to conflict/idempotent behavior |
| `23503` | `foreign_key_violation` | fix invalid relationship/workflow |
| `23502` | `not_null_violation` | validation/schema mismatch |
| `23514` | `check_violation` | input violates declared invariant |
| `40001` | `serialization_failure` | retry the **entire transaction** when safe |
| `40P01` | `deadlock_detected` | transaction is aborted; investigate lock order and retry when safe |
| `55P03` | `lock_not_available` | lock could not be obtained under the requested waiting policy |
| `57014` | `query_canceled` | cancellation/timeout; diagnose why it exceeded policy |

Drivers normally expose SQLSTATE in a structured error field. Prefer that field over parsing text such as `duplicate key value violates unique constraint`, because exact wording can change and may be localized or enriched by context.

## Unique violation

Typical situation:

```sql
INSERT INTO users(email)
VALUES ('existing@example.com');
```

when `email` is unique.

Use:

- `ON CONFLICT` if conflict is an expected workflow;
- catch unique-violation code if application logic needs it;
- do not pre-check then assume the insert cannot race.

## Foreign key violation

You insert:

```sql
customer_id = 99999
```

but no such customer exists.

Fix the data/workflow. Do not disable constraints as the first response.

## Not-null violation

A required field is missing.

Determine whether:

- application validation is wrong;
- column should actually be nullable;
- default is appropriate;
- data migration missed values.

## Check violation

Example:

```sql
price = -1
```

violates:

```sql
CHECK (price >= 0)
```

Treat the constraint as specification feedback.

## Serialization failure

At Serializable isolation, retry the **entire transaction**, not only the last statement.

Use bounded retry with jitter/backoff as appropriate.

## Deadlock detected

PostgreSQL aborts one transaction.

Actions:

1. retry when safe;
2. inspect involved statements;
3. acquire locks in consistent order;
4. shorten transactions.

## Lock timeout

The statement waited too long for a lock.

Investigate the blocker rather than simply increasing timeout indefinitely.

## Statement timeout

Query exceeded allowed time.

Possible causes:

- missing index;
- bad plan;
- unexpectedly large input;
- lock wait included in statement lifetime;
- overloaded system.

## Connection reset / server closed connection

Possible causes:

- database restart/failover;
- network interruption;
- backend terminated;
- out-of-memory/system failure;
- proxy/pool timeout.

Applications should have robust connection retry behavior, but transactions with unknown commit outcome require special care to avoid duplicate side effects.

## "Current transaction is aborted"

Inside an explicit transaction, after a statement error, PostgreSQL normally keeps the transaction in failed state until rollback.

Example:

```sql
BEGIN;
-- statement fails
SELECT 1;
```

The later query fails because the transaction must be rolled back or rolled back to a savepoint.

Fix:

```sql
ROLLBACK;
```

or use savepoints when intentionally handling partial errors.

---

# 63. Useful `psql` and SQL cheat sheet

## Connect

```bash
psql -h HOST -p 5432 -U USER -d DATABASE
```

## Database commands

```sql
CREATE DATABASE app_db;
DROP DATABASE app_db;
```

`psql`:

```text
\l
\c app_db
```

## Schema

```sql
CREATE SCHEMA app;
```

```text
\dn
```

## Tables

```text
\dt
\d app.orders
\d+ app.orders
```

## Roles

```text
\du
```

## Indexes

```text
\di
```

## Functions

```text
\df
```

## Extensions

```text
\dx
```

## Current context

```sql
SELECT current_database();
SELECT current_user;
SHOW search_path;
SHOW timezone;
```

## Create table

```sql
CREATE TABLE users (
    user_id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    email text NOT NULL UNIQUE,
    created_at timestamptz NOT NULL DEFAULT now()
);
```

## Insert

```sql
INSERT INTO users(email)
VALUES ($1)
RETURNING user_id;
```

## Update

```sql
UPDATE users
SET email = $1
WHERE user_id = $2
RETURNING *;
```

## Delete

```sql
DELETE FROM users
WHERE user_id = $1
RETURNING *;
```

## Select

```sql
SELECT user_id, email
FROM users
WHERE user_id = $1;
```

## Index

```sql
CREATE INDEX idx_orders_customer
ON orders(customer_id);
```

## Plan

```sql
EXPLAIN (ANALYZE, BUFFERS)
SELECT ...;
```

## Table size

```sql
SELECT pg_size_pretty(pg_total_relation_size('app.orders'));
```

## Active queries

```sql
SELECT pid, state, query_start, query
FROM pg_stat_activity;
```

## Cancel query

```sql
SELECT pg_cancel_backend(PID);
```

## Terminate connection

```sql
SELECT pg_terminate_backend(PID);
```

## Vacuum/analyze

```sql
VACUUM (ANALYZE) app.orders;
```

## Backup

```bash
pg_dump -Fc -d app_db -f app_db.dump
```

## Restore

```bash
pg_restore -d restored_db app_db.dump
```

---

# 64. Interview and self-test questions

Use these to test understanding, not memorized definitions.

## Beginner

1. What is the difference between PostgreSQL and SQL?
2. What is a primary key?
3. What is a foreign key?
4. What does `NOT NULL` enforce?
5. What is the difference between `WHERE` and `HAVING`?
6. Why does `column = NULL` not work as expected?
7. Difference between `INNER JOIN` and `LEFT JOIN`?
8. Difference between `DELETE`, `TRUNCATE`, and `DROP`?
9. Why use `numeric` for exact money values?
10. Why is `ORDER BY` required when row order matters?

## Intermediate

11. What is MVCC?
12. Why are old tuple versions created?
13. What does vacuum do?
14. What is autovacuum?
15. Why can a long transaction cause bloat?
16. What is a partial index?
17. What is an expression index?
18. What does `INCLUDE` do in an index?
19. Difference between `UNION` and `UNION ALL`?
20. `row_number()` vs `rank()`?
21. View vs materialized view?
22. Identity vs sequence?
23. `json` vs `jsonb`?
24. CTE vs subquery?
25. When would you use `FOR UPDATE SKIP LOCKED`?

## Advanced

26. Why can PostgreSQL choose a sequential scan despite an index?
27. What does a large estimated-vs-actual row mismatch suggest?
28. Explain B-tree, GIN, GiST, and BRIN use cases.
29. What is a HOT update?
30. Explain Read Committed, Repeatable Read, and Serializable.
31. How should applications handle serialization failures?
32. What causes a deadlock?
33. Why can `work_mem` be dangerous when globally set too high?
34. What is WAL?
35. Physical vs logical replication?
36. Why is a replication slot operationally dangerous if abandoned?
37. Why is a replica not a backup?
38. How does PITR work conceptually?
39. How does partition pruning help?
40. What are the risks of RLS?
41. Why can connection pooling change session-state assumptions?
42. Why should FK referencing columns often be indexed?
43. Why is `NOT EXISTS` often preferable to `NOT IN`?
44. What does `EXPLAIN (ANALYZE, BUFFERS)` tell you?
45. Why might extended statistics improve a plan?

## Design exercises

46. Design a booking system that prevents overlapping reservations.
47. Design an idempotent payment request table.
48. Design a multi-tenant schema with tenant isolation.
49. Design a job queue for 20 concurrent workers.
50. Design a retention strategy for 10 billion event rows.
51. Design a zero/low-downtime PostgreSQL major upgrade.
52. Design a backup plan for RPO 5 minutes and RTO 1 hour.

If you can explain trade-offs for these questions rather than only syntax, you are moving beyond beginner level.

---

# 65. Practice projects

## Project 1: Library system

Build:

- books;
- authors;
- book_authors;
- members;
- loans;
- loan history.

Practice:

- PK/FK;
- many-to-many;
- constraints;
- joins;
- overdue queries;
- indexes.

Challenge:

Prevent one physical copy from having overlapping active loans.

## Project 2: E-commerce database

Build:

- customers;
- addresses;
- products;
- categories;
- inventory;
- carts;
- orders;
- order_items;
- payments;
- shipments.

Practice:

- transactions;
- atomic stock decrement;
- order snapshots;
- reporting;
- JSON metadata;
- idempotency.

## Project 3: Invoice workflow

Build:

- vendors;
- invoices;
- invoice_items;
- approval_steps;
- approval_history;
- documents;
- audit events.

Practice:

- status constraints;
- window functions;
- approval routing;
- audit triggers;
- RLS;
- reporting views.

## Project 4: Multi-tenant SaaS

Build:

- tenants;
- users;
- memberships;
- projects;
- tasks;
- comments.

Practice:

- composite uniqueness;
- tenant-prefixed indexes;
- RLS;
- role design;
- connection-pool-safe context.

## Project 5: Job processing system

Build:

- jobs;
- attempts;
- dead-letter jobs;
- worker heartbeats.

Practice:

- `SKIP LOCKED`;
- partial indexes;
- retry scheduling;
- concurrent workers;
- idempotency.

## Project 6: Analytics/reporting

Generate millions of fake orders.

Practice:

- aggregation;
- window functions;
- grouping sets;
- materialized views;
- BRIN;
- `EXPLAIN`;
- partitioning.

## Project 7: Production operations lab

Use a disposable environment to practice:

- role creation;
- `pg_hba.conf`;
- backups;
- restores;
- replication;
- replication slots;
- intentional lock blocking;
- deadlocks;
- autovacuum observation;
- major-version test upgrade.

Never learn destructive administration commands for the first time on production.

---

# 66. Learning roadmap

## Stage 1 — SQL foundations

Learn:

- tables/rows/columns;
- types;
- `CREATE TABLE`;
- `INSERT`;
- `SELECT`;
- `WHERE`;
- `UPDATE`;
- `DELETE`;
- constraints;
- basic joins.

Goal:

Build a small relational CRUD application without copying SQL blindly.

## Stage 2 — Querying

Learn:

- all joins;
- aggregates;
- `HAVING`;
- subqueries;
- CTEs;
- set operations;
- window functions;
- date/time handling;
- null semantics.

Goal:

Write business reports confidently.

## Stage 3 — PostgreSQL features

Learn:

- `RETURNING`;
- `ON CONFLICT`;
- `DISTINCT ON`;
- `jsonb`;
- arrays;
- ranges;
- full-text search;
- extensions;
- generated columns.

Goal:

Use PostgreSQL because of its strengths, not as generic SQL storage.

## Stage 4 — Correctness and concurrency

Learn:

- transactions;
- MVCC;
- locks;
- isolation;
- deadlocks;
- idempotency;
- optimistic/pessimistic concurrency.

Goal:

Design code that remains correct with many users at once.

## Stage 5 — Performance

Learn:

- index types;
- multicolumn indexes;
- partial/expression indexes;
- `EXPLAIN`;
- planner statistics;
- `pg_stat_statements`;
- vacuum;
- partitioning.

Goal:

Tune based on evidence.

## Stage 6 — Production administration

Learn:

- roles;
- authentication;
- TLS;
- configuration;
- pooling;
- backup/restore;
- WAL;
- PITR;
- replication;
- monitoring;
- upgrades.

Goal:

Operate a recoverable, observable database.

## Stage 7 — Advanced architecture

Learn as needed:

- logical replication;
- FDWs;
- high availability orchestration;
- sharding approaches;
- CDC/logical decoding;
- server-side programming;
- custom extensions;
- specialized search/GIS/time-series extensions;
- incremental physical backup chains;
- failover rejoin workflows with `pg_rewind`;
- prepared transactions/2PC only when distributed transaction requirements justify them;
- integrity verification with checksums, `amcheck`, and backup/restore drills.

Goal:

Choose complexity only when requirements justify it.

---

# 67. PostgreSQL 18 highlights

This section intentionally separates version-specific features from timeless fundamentals.

PostgreSQL 18 was first released on **September 25, 2025**. As of **August 17, 2026**, the current 18.x minor release is **18.6**. Run the current minor release rather than treating `18.0` as the permanent target, because minor releases contain bug, security, and corruption fixes while remaining within the same major-version storage line.

PostgreSQL 19 is still a development/beta line at this date, so this handbook does not treat PostgreSQL 19-only behavior as production-stable.

## 67.1 Asynchronous I/O subsystem

PostgreSQL 18 introduced a new asynchronous I/O (AIO) subsystem. It allows supported read paths to submit multiple I/O requests without waiting for each one synchronously before proceeding.

Workloads that can benefit include supported operations such as:

- sequential scans;
- bitmap heap scans;
- vacuum-related reads;
- other paths integrated with PostgreSQL's read-streaming/AIO infrastructure.

PostgreSQL 18 exposes configuration and monitoring around this subsystem, including settings such as `io_method` and the `pg_aios` system view.

### Learning point

AIO is infrastructure, not a magic query accelerator. Query shape, selectivity, caching, storage latency, indexes, concurrency, and CPU can still dominate performance. Compare representative workload before/after and inspect actual plans/I/O.

## 67.2 B-tree skip scan

PostgreSQL 18 improved B-tree skip-scan planning so some multicolumn B-tree indexes can be useful even when the query does not have a simple equality condition on every leading index column.

Example index:

```sql
CREATE INDEX idx_people_region_email
ON people(region, email);
```

A query that constrains `email` but not `region` may sometimes use skip-scan behavior when planner estimates make that cheaper than alternatives.

```sql
SELECT person_id, region, email
FROM people
WHERE email = 'aisha@example.com';
```

Do **not** translate this into "column order no longer matters." Index order still strongly affects many workloads. Design around real predicates/orderings and validate with `EXPLAIN (ANALYZE, BUFFERS)`.

## 67.3 `uuidv7()`

PostgreSQL 18 includes native UUIDv7 generation:

```sql
SELECT uuidv7();
```

UUIDv7 is time-ordered, which can provide better insertion/index locality than fully random UUIDv4 while retaining UUID-style distributed identifier generation.

Good use cases include systems where multiple services generate IDs independently but the database still benefits from broadly increasing insertion order.

Do not assume UUIDv7 is globally "better" than `bigint` identity. Integer keys remain compact and excellent when central sequence allocation is acceptable.

## 67.4 Virtual generated columns

PostgreSQL 18 supports **virtual generated columns** and makes `VIRTUAL` the default generation mode.

```sql
CREATE TABLE rectangle (
    width numeric NOT NULL,
    height numeric NOT NULL,
    area numeric GENERATED ALWAYS AS (width * height)
);
```

Equivalent explicit declaration:

```sql
area numeric GENERATED ALWAYS AS (width * height) VIRTUAL
```

Stored form:

```sql
area numeric GENERATED ALWAYS AS (width * height) STORED
```

Key difference:

- virtual: computed when read, no storage for the generated value;
- stored: computed when written and physically stored.

Generation expressions must obey restrictions such as current-row references and immutable operations. PostgreSQL 18 virtual generated columns have additional restrictions involving user-defined functions/types; see Section 22 for the practical model.

## 67.5 `old` and `new` values in `RETURNING`

PostgreSQL 18 allows DML `RETURNING` expressions to explicitly access old and new row values.

Example:

```sql
UPDATE products
SET price = price * 1.10
WHERE price <= 99.99
RETURNING
    name,
    old.price AS old_price,
    new.price AS new_price,
    new.price - old.price AS price_change;
```

This can return before/after state atomically from the mutation itself, avoiding a separate read that could race with concurrent activity.

The feature applies across supported `INSERT`, `UPDATE`, `DELETE`, and `MERGE` contexts, but which of `old`/`new` is naturally populated depends on the operation. For example, a normal insert has no old row and a normal delete has no new row.

## 67.6 Temporal keys and foreign keys

PostgreSQL 18 expands temporal/range-based integrity with `WITHOUT OVERLAPS` on the final column of a `UNIQUE`/`PRIMARY KEY` and `PERIOD` in temporal foreign keys.

Example temporal primary key:

```sql
CREATE EXTENSION IF NOT EXISTS btree_gist;

CREATE TABLE employee_history (
    employee_id bigint NOT NULL,
    valid_at daterange NOT NULL,
    employee_name text NOT NULL,
    PRIMARY KEY (employee_id, valid_at WITHOUT OVERLAPS)
);
```

Meaning: the same `employee_id` can have multiple history rows, but their `valid_at` ranges cannot overlap.

A temporal foreign key can require the referenced history to cover the referencing row's entire period:

```sql
CREATE TABLE employee_assignments (
    assignment_id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    employee_id bigint NOT NULL,
    valid_at daterange NOT NULL,
    FOREIGN KEY (employee_id, PERIOD valid_at)
        REFERENCES employee_history (employee_id, PERIOD valid_at)
);
```

Temporal keys are especially useful for:

- effective-dated master data;
- contracts;
- subscriptions;
- employee assignments;
- pricing periods.

They have specific type, index/operator-class, and referential-action restrictions. Treat them as declarative temporal integrity, not simply syntax sugar for ordinary foreign keys.

## 67.7 `pg_upgrade` retains optimizer statistics

Historically, a major upgrade could require significant post-upgrade `ANALYZE` work before the new cluster had mature planner statistics again.

PostgreSQL 18 improves `pg_upgrade` by retaining planner/optimizer statistics through the upgrade path, reducing the post-upgrade statistics cold-start problem.

This does not eliminate upgrade validation. Still:

- follow the exact `pg_upgrade` instructions;
- update extensions as prescribed;
- run required post-upgrade scripts;
- compare critical query plans and latency;
- validate application behavior and backups.

## 67.8 OAuth authentication

PostgreSQL 18 adds OAuth authentication support and server/client infrastructure for OAuth-based flows.

This can integrate PostgreSQL authentication with modern identity infrastructure, but it is not a drop-in replacement for every password setup. Identity-provider discovery, issuer/audience validation, token handling, TLS, authorization mapping, and client support all matter.

Follow PostgreSQL 18's exact OAuth documentation and your identity provider's security requirements rather than copying a password-authentication example.

## 67.9 MD5 password authentication deprecation

PostgreSQL 18 deprecates MD5 password authentication, with removal planned in a future major release.

Modern password-based deployments should use SCRAM (`scram-sha-256`) where appropriate and should audit both password storage and `pg_hba.conf` authentication methods before a future major upgrade removes MD5 support.

## 67.10 Data checksums default for new clusters

PostgreSQL 18 enables data checksums by default for newly initialized clusters unless explicitly disabled.

Checksums can detect certain forms of on-disk page corruption, but they do **not** replace:

- tested backups;
- replication/high availability;
- reliable storage;
- filesystem/hardware monitoring;
- restore drills.

Treat a checksum error as evidence requiring investigation, not as something to silence.


---

# 68. Production checklist

Use this as a review list, not as a substitute for environment-specific engineering.

## Schema

- [ ] Primary keys defined.
- [ ] Natural/business uniqueness enforced.
- [ ] Foreign keys defined where relationships require integrity.
- [ ] FK referencing columns indexed when workload needs them.
- [ ] Correct numeric/date/time types used.
- [ ] Stable relational attributes are not hidden unnecessarily in JSON.
- [ ] Nullability reflects real business semantics.
- [ ] Check constraints protect critical invariants.
- [ ] Naming conventions are consistent.

## Queries

- [ ] Important queries use parameter binding.
- [ ] No accidental N+1 patterns.
- [ ] Pagination is deterministic.
- [ ] Deep feeds use keyset pagination where appropriate.
- [ ] Large reports are reviewed with `EXPLAIN`.
- [ ] `SELECT *` is avoided in stable APIs when unnecessary.
- [ ] Bulk operations use batching/COPY when appropriate.

## Concurrency

- [ ] Transaction boundaries match business invariants.
- [ ] Transactions are short.
- [ ] Deadlock-sensitive resources use consistent ordering.
- [ ] Serializable transactions have retry logic.
- [ ] Idempotency exists for retryable external requests.
- [ ] Worker queues use safe claiming logic.

## Security

- [ ] Runtime application is not superuser.
- [ ] Least privilege enforced.
- [ ] Passwords/secrets are not committed to source control.
- [ ] SCRAM/modern authentication is used rather than deprecated MD5.
- [ ] Network exposure is restricted.
- [ ] TLS verification is configured where required.
- [ ] RLS is tested using real application roles if used.
- [ ] `search_path` is reviewed for privileged code.
- [ ] `SECURITY DEFINER` routines are hardened.

## Reliability

- [ ] Automated backups exist.
- [ ] Restore tests are scheduled.
- [ ] RPO/RTO are documented.
- [ ] Backups are stored separately/offsite as required.
- [ ] PITR WAL archive is monitored if used.
- [ ] Replication is monitored.
- [ ] Replication slots cannot silently fill disk.
- [ ] Failover procedure is documented and tested.

## Maintenance

- [ ] Autovacuum is enabled.
- [ ] High-churn tables are monitored/tuned.
- [ ] Long/idle transactions are detected.
- [ ] Disk growth and WAL growth are alerted.
- [ ] Table/index growth is monitored.
- [ ] Statistics are fresh.
- [ ] Supported PostgreSQL major/minor release is used.

## Performance

- [ ] `pg_stat_statements` or equivalent observability is available.
- [ ] Slowest/highest-total-time queries are reviewed.
- [ ] Indexes correspond to real access patterns.
- [ ] Redundant/unused indexes are reviewed cautiously.
- [ ] Memory settings account for concurrency.
- [ ] Connection pooling is sized by measurement.
- [ ] Lock waits are monitored.
- [ ] Temp-file growth is monitored.

## Deployments

- [ ] Migrations are tested on production-like data volume.
- [ ] DDL lock impact is understood.
- [ ] `CREATE INDEX CONCURRENTLY` is considered where appropriate.
- [ ] Risky migrations use lock/statement timeouts intentionally.
- [ ] Rollback/roll-forward plan is explicit.
- [ ] Major upgrade release notes are reviewed.

---

# 69. Official references

For exact syntax, edge cases, compatibility, and version-specific behavior, the PostgreSQL manual is the final authority.

Recommended official references:

- PostgreSQL Documentation — `https://www.postgresql.org/docs/current/`
- SQL Language — `https://www.postgresql.org/docs/current/sql.html`
- SQL Commands Reference — `https://www.postgresql.org/docs/current/sql-commands.html`
- Indexes — `https://www.postgresql.org/docs/current/indexes.html`
- Concurrency Control — `https://www.postgresql.org/docs/current/mvcc.html`
- Performance Tips — `https://www.postgresql.org/docs/current/performance-tips.html`
- Server Administration — `https://www.postgresql.org/docs/current/admin.html`
- Backup and Restore — `https://www.postgresql.org/docs/current/backup.html`
- High Availability and Replication — `https://www.postgresql.org/docs/current/high-availability.html`
- Logical Replication — `https://www.postgresql.org/docs/current/logical-replication.html`
- PL/pgSQL — `https://www.postgresql.org/docs/current/plpgsql.html`
- PostgreSQL 18 Release Notes — `https://www.postgresql.org/docs/current/release-18.html`
- PostgreSQL Versioning Policy — `https://www.postgresql.org/support/versioning/`

---

# Appendix A — A complete learning schema

The following mini schema combines many concepts from this handbook.

```sql
CREATE SCHEMA shop;

CREATE TABLE shop.customers (
    customer_id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    public_id uuid NOT NULL DEFAULT uuidv7() UNIQUE,
    email text NOT NULL,
    name text NOT NULL,
    metadata jsonb NOT NULL DEFAULT '{}'::jsonb,
    active boolean NOT NULL DEFAULT true,
    created_at timestamptz NOT NULL DEFAULT now(),
    updated_at timestamptz NOT NULL DEFAULT now(),
    CONSTRAINT uq_customers_email UNIQUE (email)
);

CREATE TABLE shop.products (
    product_id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    sku text NOT NULL UNIQUE,
    name text NOT NULL,
    price numeric(12,2) NOT NULL CHECK (price >= 0),
    attributes jsonb NOT NULL DEFAULT '{}'::jsonb,
    active boolean NOT NULL DEFAULT true,
    created_at timestamptz NOT NULL DEFAULT now()
);

CREATE TABLE shop.inventory (
    product_id bigint PRIMARY KEY
        REFERENCES shop.products(product_id)
        ON DELETE CASCADE,
    stock_qty integer NOT NULL DEFAULT 0 CHECK (stock_qty >= 0),
    updated_at timestamptz NOT NULL DEFAULT now()
);

CREATE TABLE shop.orders (
    order_id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    order_uuid uuid NOT NULL DEFAULT uuidv7() UNIQUE,
    customer_id bigint NOT NULL
        REFERENCES shop.customers(customer_id),
    status text NOT NULL
        CHECK (status IN ('pending', 'paid', 'shipped', 'cancelled')),
    order_total numeric(14,2) NOT NULL CHECK (order_total >= 0),
    created_at timestamptz NOT NULL DEFAULT now()
);

CREATE TABLE shop.order_items (
    order_item_id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    order_id bigint NOT NULL
        REFERENCES shop.orders(order_id)
        ON DELETE CASCADE,
    product_id bigint NOT NULL
        REFERENCES shop.products(product_id),
    quantity integer NOT NULL CHECK (quantity > 0),
    unit_price numeric(12,2) NOT NULL CHECK (unit_price >= 0),
    line_total numeric(14,2)
        GENERATED ALWAYS AS (quantity * unit_price) STORED
);

CREATE INDEX idx_orders_customer_created
ON shop.orders(customer_id, created_at DESC);

CREATE INDEX idx_orders_paid_created
ON shop.orders(created_at DESC)
WHERE status = 'paid';

CREATE INDEX idx_products_attributes_gin
ON shop.products USING gin(attributes);

CREATE INDEX idx_order_items_product
ON shop.order_items(product_id);
```

## Query 1: customer lifetime value

```sql
SELECT
    c.customer_id,
    c.name,
    count(o.order_id) AS paid_orders,
    coalesce(sum(o.order_total), 0) AS lifetime_value
FROM shop.customers c
LEFT JOIN shop.orders o
  ON o.customer_id = c.customer_id
 AND o.status = 'paid'
GROUP BY c.customer_id, c.name
ORDER BY lifetime_value DESC;
```

## Query 2: latest order per customer

```sql
SELECT DISTINCT ON (o.customer_id)
    o.customer_id,
    o.order_id,
    o.status,
    o.order_total,
    o.created_at
FROM shop.orders o
ORDER BY o.customer_id, o.created_at DESC, o.order_id DESC;
```

## Query 3: atomically reserve stock

```sql
UPDATE shop.inventory
SET
    stock_qty = stock_qty - $1,
    updated_at = now()
WHERE product_id = $2
  AND stock_qty >= $1
RETURNING stock_qty;
```

## Query 4: monthly revenue with previous month

```sql
WITH monthly AS (
    SELECT
        date_trunc('month', created_at) AS month,
        sum(order_total) AS revenue
    FROM shop.orders
    WHERE status = 'paid'
    GROUP BY 1
)
SELECT
    month,
    revenue,
    lag(revenue) OVER (ORDER BY month) AS previous_revenue,
    revenue - lag(revenue) OVER (ORDER BY month) AS absolute_change
FROM monthly
ORDER BY month;
```

## Query 5: JSON attribute search

```sql
SELECT product_id, sku, name
FROM shop.products
WHERE attributes @> '{"color":"black"}'::jsonb;
```

---

# Appendix B — Debugging decision tree

When PostgreSQL behaves unexpectedly, use this order.

## "My query returns wrong rows"

Check:

1. `NULL` semantics;
2. join type;
3. outer-join filters in `WHERE` vs `ON`;
4. duplicate-producing joins;
5. date range boundaries;
6. time zone;
7. implicit casts;
8. `NOT IN` with nulls;
9. missing parentheses around boolean logic;
10. non-deterministic ordering.

## "My query is slow"

Check:

1. `pg_stat_statements` impact;
2. blocking/locks;
3. `EXPLAIN (ANALYZE, BUFFERS)`;
4. estimates vs actual rows;
5. missing/wrong indexes;
6. large returned row count;
7. sort/hash spill;
8. stale statistics;
9. table/index bloat;
10. CPU/I/O saturation.

## "My UPDATE hangs"

Likely possibilities:

- waiting for row/table lock;
- trigger performing slow work;
- FK check against slow/unindexed referencing data;
- huge update simply taking time.

Inspect `pg_stat_activity`, `wait_event`, and `pg_blocking_pids()`.

## "Disk usage is exploding"

Check:

- `pg_wal`;
- replication slots;
- archive failures;
- table growth;
- index growth;
- temp files;
- long transactions;
- logs;
- backup files.

## "Index is not used"

Ask:

1. Does query return a large fraction of table?
2. Is table tiny?
3. Is indexed column wrapped in expression/cast?
4. Do predicates match partial index condition?
5. Is column order useful?
6. Are stats fresh?
7. Are data types aligned?
8. Is an index scan actually more expensive?

## "Autovacuum runs constantly"

That may be normal on a write-heavy table.

Check whether it is keeping up before trying to suppress it.

## "Replica is behind"

Determine where lag occurs:

- primary WAL generation;
- network transfer;
- standby WAL write/flush;
- replay;
- standby resource saturation;
- recovery conflicts;
- long queries;
- storage performance.

---

# Appendix C — SQL style guide

Consistency makes SQL easier to review.

Recommended style:

```sql
SELECT
    o.order_id,
    o.created_at,
    c.customer_id,
    c.name AS customer_name,
    sum(oi.quantity * oi.unit_price) AS calculated_total
FROM orders AS o
JOIN customers AS c
  ON c.customer_id = o.customer_id
JOIN order_items AS oi
  ON oi.order_id = o.order_id
WHERE o.status = 'paid'
  AND o.created_at >= $1
  AND o.created_at < $2
GROUP BY
    o.order_id,
    o.created_at,
    c.customer_id,
    c.name
ORDER BY o.created_at DESC, o.order_id DESC;
```

Style principles:

- uppercase SQL keywords if your team likes it;
- lowercase `snake_case` object names;
- one selected column per line for complex queries;
- explicit join conditions;
- meaningful aliases;
- deterministic `ORDER BY`;
- parameterized values;
- comments explaining **why**, not obvious syntax;
- schema-qualify objects in security-sensitive routines/migrations.

---

# Appendix D — Glossary

**ACID** — atomicity, consistency, isolation, durability.

**Backend** — PostgreSQL server process/session handling a client connection.

**Bloat** — excess relation space caused by workload/storage history beyond useful live contents.

**Checkpoint** — recovery/flush coordination point in WAL processing.

**Cluster** — in core PostgreSQL terminology, databases managed by one server/data directory.

**CTE** — Common Table Expression introduced by `WITH`.

**DDL** — Data Definition Language, e.g. `CREATE`, `ALTER`, `DROP`.

**DML** — Data Manipulation Language, e.g. `INSERT`, `UPDATE`, `DELETE`, `MERGE`.

**FDW** — Foreign Data Wrapper.

**GIN** — Generalized Inverted Index.

**GiST** — Generalized Search Tree.

**HOT** — Heap-Only Tuple update optimization.

**Index-only scan** — scan where needed values can be returned from index and heap visibility permits avoiding many heap fetches.

**LSN** — Log Sequence Number, a position in WAL.

**MVCC** — Multi-Version Concurrency Control.

**ORDBMS** — Object-Relational Database Management System.

**PITR** — Point-In-Time Recovery.

**RLS** — Row-Level Security.

**RPO** — Recovery Point Objective; acceptable data-loss window.

**RTO** — Recovery Time Objective; acceptable recovery duration.

**Tuple** — PostgreSQL/database terminology for a row version in many contexts.

**WAL** — Write-Ahead Log.

---

# Appendix E — Additional advanced PostgreSQL concepts

These topics are not required for your first CRUD application, but they complete the mental model of PostgreSQL and become important in specialized systems.

## E.1 `information_schema` vs PostgreSQL catalogs

### `information_schema`

SQL-standard metadata views:

```sql
SELECT table_schema, table_name
FROM information_schema.tables
WHERE table_type = 'BASE TABLE';
```

Advantages:

- more portable SQL-standard interface;
- useful for generic tools.

### PostgreSQL catalogs

PostgreSQL stores internal metadata in catalogs such as:

```text
pg_class
pg_attribute
pg_namespace
pg_constraint
pg_index
pg_proc
pg_type
```

Example:

```sql
SELECT
    n.nspname AS schema_name,
    c.relname AS relation_name,
    c.relkind
FROM pg_class c
JOIN pg_namespace n
  ON n.oid = c.relnamespace
WHERE n.nspname NOT IN ('pg_catalog', 'information_schema');
```

Use PostgreSQL catalogs when you need PostgreSQL-specific metadata unavailable through `information_schema`.

Avoid depending on undocumented internal details that may change between major versions.

---

## E.2 System columns

PostgreSQL exposes special system columns for table rows, including concepts such as `ctid` and transaction visibility identifiers.

Example:

```sql
SELECT ctid, *
FROM products
LIMIT 5;
```

### `ctid`

`ctid` identifies a physical tuple location.

It can be useful for diagnostics or one-off maintenance, but it is **not a stable business identifier**. An update, table rewrite, or movement can change it.

Never use `ctid` as an application primary key.

---

## E.3 TOAST

PostgreSQL can store large column values using a mechanism commonly called TOAST — The Oversized-Attribute Storage Technique.

Large values such as:

- long `text`;
- `jsonb`;
- `bytea`;
- arrays;

may be compressed and/or stored out-of-line automatically.

### Why learners should care

A row containing a huge JSONB document may look like one row logically but cause extra storage and I/O behavior physically.

This matters when:

- repeatedly updating large values;
- reading only a small part of very large values;
- estimating table size;
- designing wide rows.

Do not manually manage TOAST for ordinary applications. Understand it so storage behavior is less mysterious.

---

## E.4 Tablespaces

A tablespace maps PostgreSQL objects to storage locations managed by the operating system/storage layout.

Example:

```sql
CREATE TABLESPACE fast_space
LOCATION '/mnt/fast_pg';
```

Then:

```sql
CREATE TABLE high_io_table (
    id bigint PRIMARY KEY,
    payload jsonb
) TABLESPACE fast_space;
```

### Use cases

- placing selected objects on different storage;
- specialized capacity/performance layouts.

### Warning

Tablespaces increase operational complexity. Backup, permissions, mount availability, recovery, and failover must all account for them.

Do not use them simply to create folder organization.

---

## E.5 Collation and locale

Collation controls text ordering/comparison behavior.

Two databases can produce different ordering for the same text depending on locale/collation settings.

This affects:

- `ORDER BY`;
- equality/order semantics for some collations;
- unique indexes;
- pattern operations;
- index behavior;
- application expectations.

Inspect database settings:

```sql
SELECT
    datname,
    datcollate,
    datctype
FROM pg_database
WHERE datname = current_database();
```

### Migration warning

Operating-system or collation-library upgrades can change sort rules. Large production upgrades should include collation compatibility/reindex planning where relevant.

---

## E.6 Advisory locks

Advisory locks are application-defined locks identified by integers rather than by automatically locked table rows.

Transaction-level example:

```sql
SELECT pg_advisory_xact_lock(12345);
```

Try without waiting:

```sql
SELECT pg_try_advisory_xact_lock(12345);
```

### Uses

- ensure one scheduler performs a task;
- serialize work for a logical resource that has no convenient row to lock;
- migration coordination;
- singleton background jobs.

### Risks

PostgreSQL does not know the business meaning of your lock key. Every code path must use the same locking convention.

Prefer row/constraint-based concurrency when the invariant naturally belongs to database rows.

---

## E.7 LISTEN and NOTIFY

PostgreSQL supports lightweight asynchronous notifications.

Listener:

```sql
LISTEN order_events;
```

Sender:

```sql
NOTIFY order_events, 'order-123-created';
```

Applications can subscribe through drivers.

### Good uses

- cache invalidation hints;
- wake-up signals;
- low-volume coordination;
- development/admin notification flows.

### Not a durable message queue

Notifications are not a substitute for a durable broker/outbox when messages must survive disconnected consumers or require robust retries/history.

Use them as signals, not as your only business-event storage.

---

## E.8 Prepared statements

Server-side prepared statement:

```sql
PREPARE get_user(text) AS
SELECT user_id, email
FROM users
WHERE email = $1;
```

Execute:

```sql
EXECUTE get_user('a@example.com');
```

Remove:

```sql
DEALLOCATE get_user;
```

Most applications should use their driver's normal parameterized/prepared-statement API rather than manually issuing these commands everywhere.

Prepared statements can improve repeated-query overhead, but highly skewed parameters can make generic-plan behavior worth investigating.

---

## E.9 Parallel query

PostgreSQL can use multiple worker processes for suitable queries.

Plans may contain nodes such as:

```text
Gather
Parallel Seq Scan
Parallel Hash
Partial Aggregate
Finalize Aggregate
```

Parallelism is useful for sufficiently expensive operations, especially large analytical scans/aggregations.

It is not free:

- workers must be launched/coordinated;
- data may need to be gathered;
- not every operation is parallel-safe;
- concurrency across many queries competes for CPU.

Use `EXPLAIN` to see actual parallel plans.

---

## E.10 JIT compilation

PostgreSQL can use Just-In-Time compilation for portions of expensive query execution.

JIT can help long-running CPU-heavy analytical queries, but compilation overhead can hurt short OLTP queries.

The planner uses cost thresholds to decide when JIT is worthwhile.

Do not enable/disable JIT globally based on one tiny benchmark. Evaluate representative workload.

---

## E.11 Data checksums

Data checksums help detect certain forms of on-disk page corruption.

PostgreSQL 18 changed `initdb` defaults so data checksums are enabled by default for newly initialized clusters unless explicitly disabled.

### Important distinction

Checksums detect corruption; they do not replace:

- backups;
- RAID/storage redundancy;
- replication;
- filesystem checks;
- monitoring.

A checksum error is evidence of a storage/corruption problem that must be investigated.

---

## E.12 Table inheritance

PostgreSQL supports table inheritance:

```sql
CREATE TABLE vehicles (
    vehicle_id bigint,
    manufacturer text
);

CREATE TABLE cars (
    doors integer
) INHERITS (vehicles);
```

Inheritance is a PostgreSQL-specific feature with special query/constraint semantics.

For table partitioning, prefer modern declarative partitioning rather than old inheritance-based partitioning designs.

Use inheritance only when you genuinely need its semantics and understand constraint/uniqueness behavior.

---

## E.13 Large Objects

PostgreSQL has a Large Object facility for storing large binary objects through a special API.

For many modern applications, alternatives include:

- `bytea` for manageable binary values;
- object/blob storage with database metadata references for very large files.

Choose based on transaction requirements, size, streaming, backup, and application architecture.

---

## E.14 `generate_series()`

A very useful PostgreSQL set-returning function:

```sql
SELECT generate_series(1, 5);
```

Output:

```text
1
2
3
4
5
```

Generate dates:

```sql
SELECT generate_series(
    date '2026-08-01',
    date '2026-08-07',
    interval '1 day'
);
```

### Reporting use case: show days with zero sales

```sql
WITH days AS (
    SELECT generate_series(
        $1::date,
        $2::date,
        interval '1 day'
    )::date AS day
),
sales AS (
    SELECT
        created_at::date AS day,
        sum(order_total) AS revenue
    FROM orders
    WHERE created_at >= $1
      AND created_at < $2::date + 1
    GROUP BY 1
)
SELECT
    d.day,
    coalesce(s.revenue, 0) AS revenue
FROM days d
LEFT JOIN sales s USING (day)
ORDER BY d.day;
```

This ensures missing dates appear with zero rather than disappearing.

---

## E.15 `RETURNING` as an application pattern

PostgreSQL's `RETURNING` is worth treating as a core application-development technique.

Insert and get generated ID:

```sql
INSERT INTO users(email)
VALUES ($1)
RETURNING user_id, created_at;
```

Update and get new state:

```sql
UPDATE orders
SET status = 'paid'
WHERE order_id = $1
RETURNING order_id, status, updated_at;
```

Delete and capture deleted row:

```sql
DELETE FROM temporary_tokens
WHERE token_id = $1
RETURNING *;
```

This reduces race-prone follow-up reads and network round trips.

---

## E.16 Rules system

PostgreSQL has a query rewrite rule system and supports `CREATE RULE`.

Rules are historically important and power some behavior such as views internally, but for ordinary application side effects, triggers are generally easier to reason about.

Do not reach for custom rules until you understand their rewrite semantics.

---

## E.17 Logical decoding and CDC

Logical decoding extracts logical changes from WAL through replication slots/output plugins.

It underpins many Change Data Capture (CDC) pipelines.

Conceptually:

```text
PostgreSQL WAL
   |
logical decoding
   |
output plugin / connector
   |
Kafka / analytics / downstream service
```

Operational concerns:

- replication slot retention;
- WAL growth;
- schema evolution;
- ordering;
- exactly-once claims vs actual end-to-end semantics;
- downstream idempotency;
- failover behavior.

Logical decoding is powerful infrastructure; monitor it like replication, not like a fire-and-forget export script.

---

## E.18 Session and transaction variables

Session:

```sql
SET statement_timeout = '10s';
```

Transaction-local:

```sql
BEGIN;
SET LOCAL statement_timeout = '2s';
-- statements
COMMIT;
```

Read:

```sql
SHOW statement_timeout;
```

Application-defined custom settings can be useful for trusted request context, especially with RLS/auditing, but must be managed safely with connection pools.

---

## E.19 Temporary schemas and temporary objects

Temporary tables are stored in per-session temporary schemas.

```sql
CREATE TEMP TABLE selected_ids (
    id bigint PRIMARY KEY
) ON COMMIT DROP;
```

`ON COMMIT` options can control what happens at transaction commit.

Temporary objects are useful for complex batch work but can become a scalability problem if an application creates/drops many temp tables at very high rates. Compare alternatives such as arrays, CTEs, staging tables, or set-based joins.

---

## E.20 Generated data and test datasets

PostgreSQL is excellent for building learning data without external scripts.

Example million rows:

```sql
CREATE TABLE demo_events AS
SELECT
    g AS event_id,
    now() - (g || ' seconds')::interval AS created_at,
    (g % 1000) + 1 AS account_id,
    jsonb_build_object('value', g) AS payload
FROM generate_series(1, 1000000) AS g;
```

Then:

```sql
ANALYZE demo_events;
```

Practice:

- sequential scans;
- B-tree vs BRIN;
- aggregation;
- indexes;
- `EXPLAIN (ANALYZE, BUFFERS)`.

Use disposable databases for large experiments.

---


## E.21 Incremental physical backups and `pg_combinebackup`

PostgreSQL can take **incremental physical base backups** with `pg_basebackup` (supported with PostgreSQL servers from version 17 onward). Instead of transmitting every unchanged block, an incremental backup can contain only blocks changed since the reference backup.

### Important: an incremental backup is not directly restorable

It depends on earlier backups. Before recovery, reconstruct a synthetic full backup with `pg_combinebackup`.

Conceptual workflow:

```bash
# Full backup
pg_basebackup -D backups/full -Fp -X stream -P

# Incremental backup using the previous backup manifest
pg_basebackup \
  -D backups/inc1 \
  -Fp -X stream -P \
  --incremental=backups/full/backup_manifest

# Reconstruct a synthetic full backup
pg_combinebackup \
  -o backups/synthetic_full \
  backups/full \
  backups/inc1

# Verify the reconstructed backup against its manifest
pg_verifybackup backups/synthetic_full
```

For a longer chain, pass all required backups to `pg_combinebackup` from **oldest to newest**.

### Operational lessons

Incremental backup depends on PostgreSQL WAL summary files covering the required LSN range between the reference backup and the new backup. If the required summaries are missing or have already been removed, the incremental backup fails.

- Keep dependency metadata/backup manifests; deleting an ancestor can make dependent incrementals unusable.
- `pg_combinebackup` validates the relationship of the backup chain, but backup integrity should still be checked with `pg_verifybackup`.
- Test a real restore, not only the backup command.
- Monitor the WAL summarizer and backup process when using incremental backup architecture.
- A backup strategy is incomplete until RPO/RTO and retention/offsite requirements are defined.

---

## E.22 `pg_rewind` after failover

After failover, an old primary may have diverged from the new primary's timeline. Copying the entire cluster again is sometimes unnecessary: `pg_rewind` can synchronize the old data directory with the new source so it can often rejoin as a standby.

Conceptually:

```text
Primary A ----writes----X
                      failover
Standby B -> new primary ----new writes---->

Old A has diverged history
        |
        | pg_rewind
        v
Old A synchronized to B's timeline, then recovered/rejoined
```

Typical command shape:

```bash
pg_rewind \
  --target-pgdata=/var/lib/postgresql/data \
  --source-server='host=new-primary dbname=postgres user=rewind_user'
```

### Requirements and warnings

`pg_rewind` requires the target cluster to have either `wal_log_hints` enabled or data checksums enabled, and `full_page_writes` must be on. Required WAL around the divergence/recovery path must be available.

After rewind, recovery/WAL replay must complete before the target becomes a consistent member again.

If `pg_rewind` fails partway through, the target data directory may no longer be safely usable; a fresh base backup is the conservative recovery path.

Use `pg_rewind` as part of a tested HA runbook, not as an improvised command during an outage.

---

## E.23 Two-phase commit and prepared transactions

PostgreSQL supports two-phase commit (2PC) for coordination by external distributed transaction managers.

Commands:

```sql
BEGIN;
-- transactional work
PREPARE TRANSACTION 'global-transaction-123';
```

Later, the coordinator decides:

```sql
COMMIT PREPARED 'global-transaction-123';
```

or:

```sql
ROLLBACK PREPARED 'global-transaction-123';
```

Inspect outstanding prepared transactions:

```sql
SELECT *
FROM pg_prepared_xacts;
```

### Why it exists

2PC separates "I am ready to commit" from the final commit decision so multiple transactional systems can coordinate one distributed outcome.

### Why ordinary applications should not use it casually

Prepared transactions can hold resources/locks and survive beyond the original session. If the coordinator fails or loses its decision record, transactions can remain prepared and interfere with normal work.

Use 2PC when a real external transaction manager requires it. For ordinary service integration, patterns such as transactional outbox + idempotent consumers are often operationally simpler.

Prepared transactions are controlled by `max_prepared_transactions`. If you do not operate a transaction manager, keeping this feature disabled (`max_prepared_transactions = 0`) prevents accidental prepared transactions from being forgotten.

Keep prepared states short and monitor `pg_prepared_xacts` when 2PC is enabled.

---

## E.24 Integrity verification with `amcheck` and backup verification

Checksums, logical integrity checks, and backup verification answer different questions.

### `amcheck`

The `amcheck` extension provides functions that verify structural/logical consistency of supported table/index structures.

```sql
CREATE EXTENSION IF NOT EXISTS amcheck;
```

A lightweight B-tree check can use:

```sql
SELECT bt_index_check('idx_orders_customer_id'::regclass);
```

More thorough checks can require stronger locks and more work. Do not run the heaviest integrity checks blindly on a busy production system.

### `pg_verifybackup`

For a physical base backup that has a backup manifest:

```bash
pg_verifybackup /backups/base_2026_08_17
```

This verifies the backup against its manifest. It is valuable, but still does not replace a **restore test** that proves your end-to-end recovery procedure works.

### Three layers to remember

```text
Data checksums      -> detect certain page corruption during database use
amcheck             -> inspect logical/structural consistency of supported relations
pg_verifybackup     -> validate a physical backup against its manifest
restore drill       -> prove the actual recovery process and application usability
```

Production reliability uses these as complementary tools rather than substitutes.

---

# Final principles to remember

If you remember only a few ideas from this handbook, remember these:

1. **Model business rules in the database, not only in UI code.**
2. **Use the correct data type.**
3. **Use constraints for invariants.**
4. **Parameterize application SQL.**
5. **Transactions protect multi-step correctness.**
6. **MVCC makes PostgreSQL concurrency powerful, and vacuum makes MVCC sustainable.**
7. **Indexes are workload-specific tools with write costs.**
8. **`EXPLAIN (ANALYZE, BUFFERS)` is evidence; guesses are not.**
9. **Short transactions are healthy transactions.**
10. **A replica is not a backup.**
11. **A backup you never restored is unproven.**
12. **Autovacuum is part of correctness and maintenance, not an optional cleanup script.**
13. **Least privilege reduces blast radius.**
14. **Do not tune configuration before finding the real bottleneck.**
15. **Read release notes before major upgrades.**
16. **Prefer simple relational design until complexity earns its place.**

---

**End of PostgreSQL Master Handbook**
