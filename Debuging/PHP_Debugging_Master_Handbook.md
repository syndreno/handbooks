# PHP Debugging Master Handbook

> A beginner-to-advanced, practical handbook for finding, understanding, reproducing, fixing, and preventing bugs in modern PHP applications.

---

## Table of Contents

1. [How to Use This Handbook](#1-how-to-use-this-handbook)
2. [What Debugging Really Means](#2-what-debugging-really-means)
3. [The Debugging Mindset](#3-the-debugging-mindset)
4. [Build a Reproducible Debugging Process](#4-build-a-reproducible-debugging-process)
5. [Know Which PHP Environment Is Actually Running](#5-know-which-php-environment-is-actually-running)
6. [PHP Error Reporting Fundamentals](#6-php-error-reporting-fundamentals)
7. [PHP Errors, Exceptions, and `Throwable`](#7-php-errors-exceptions-and-throwable)
8. [Reading PHP Error Messages and Stack Traces](#8-reading-php-error-messages-and-stack-traces)
9. [Fast Inspection with `var_dump()`, `print_r()`, and Friends](#9-fast-inspection-with-var_dump-printr-and-friends)
10. [Logging with `error_log()` and Application Logs](#10-logging-with-error_log-and-application-logs)
11. [Custom Error and Exception Handlers](#11-custom-error-and-exception-handlers)
12. [Debugging Fatal Shutdown Problems](#12-debugging-fatal-shutdown-problems)
13. [Assertions for Development-Time Checks](#13-assertions-for-development-time-checks)
14. [Xdebug: The Essential PHP Debugger](#14-xdebug-the-essential-php-debugger)
15. [Step Debugging with VS Code](#15-step-debugging-with-vs-code)
16. [Breakpoints, Watches, Call Stacks, and Step Controls](#16-breakpoints-watches-call-stacks-and-step-controls)
17. [Debugging PHP from the Command Line](#17-debugging-php-from-the-command-line)
18. [Debugging Web Requests and HTTP Problems](#18-debugging-web-requests-and-http-problems)
19. [Debugging APIs and JSON](#19-debugging-apis-and-json)
20. [Debugging HTML Forms and Request Data](#20-debugging-html-forms-and-request-data)
21. [Debugging File Uploads](#21-debugging-file-uploads)
22. [Debugging Sessions and Cookies](#22-debugging-sessions-and-cookies)
23. [Debugging Headers and Redirects](#23-debugging-headers-and-redirects)
24. [Debugging Include, Require, Autoload, and Composer Problems](#24-debugging-include-require-autoload-and-composer-problems)
25. [Debugging Namespaces and Class Resolution](#25-debugging-namespaces-and-class-resolution)
26. [Debugging Types, Null Values, and Function Arguments](#26-debugging-types-null-values-and-function-arguments)
27. [Debugging Arrays and Collections](#27-debugging-arrays-and-collections)
28. [Debugging Strings, Encoding, and Unicode](#28-debugging-strings-encoding-and-unicode)
29. [Debugging Date, Time, and Time Zones](#29-debugging-date-time-and-time-zones)
30. [Debugging Regular Expressions](#30-debugging-regular-expressions)
31. [Debugging PDO Database Code](#31-debugging-pdo-database-code)
32. [Debugging MySQLi Database Code](#32-debugging-mysqli-database-code)
33. [Debugging Transactions](#33-debugging-transactions)
34. [Debugging SQL Logic and Data Problems](#34-debugging-sql-logic-and-data-problems)
35. [Debugging AJAX and Frontend-to-PHP Requests](#35-debugging-ajax-and-frontend-to-php-requests)
36. [Debugging Authentication and Authorization](#36-debugging-authentication-and-authorization)
37. [Debugging Filesystem and Permission Problems](#37-debugging-filesystem-and-permission-problems)
38. [Debugging Email and External Services](#38-debugging-email-and-external-services)
39. [Debugging cURL and Third-Party APIs](#39-debugging-curl-and-third-party-apis)
40. [Debugging Memory Problems](#40-debugging-memory-problems)
41. [Debugging Slow PHP Applications](#41-debugging-slow-php-applications)
42. [Profiling, Tracing, and Code Coverage](#42-profiling-tracing-and-code-coverage)
43. [Debugging PHP-FPM, Apache, and Nginx](#43-debugging-php-fpm-apache-and-nginx)
44. [Debugging Dockerized PHP](#44-debugging-dockerized-php)
45. [Debugging Queues, Cron Jobs, and Background Commands](#45-debugging-queues-cron-jobs-and-background-commands)
46. [Debugging Production Safely](#46-debugging-production-safely)
47. [Framework Debugging Notes](#47-framework-debugging-notes)
48. [Testing as a Debugging Tool](#48-testing-as-a-debugging-tool)
49. [Static Analysis and Automated Bug Detection](#49-static-analysis-and-automated-bug-detection)
50. [Common PHP Bugs: Symptoms, Causes, and Fixes](#50-common-php-bugs-symptoms-causes-and-fixes)
51. [Real-World Debugging Scenarios](#51-real-world-debugging-scenarios)
52. [A Professional Debugging Workflow](#52-a-professional-debugging-workflow)
53. [Debugging Anti-Patterns](#53-debugging-anti-patterns)
54. [Debugging Best Practices](#54-debugging-best-practices)
55. [Debugging Checklists](#55-debugging-checklists)
56. [PHP Debugging Cheat Sheet](#56-php-debugging-cheat-sheet)
57. [Recommended Learning Exercises](#57-recommended-learning-exercises)
58. [Official References](#58-official-references)
59. [Appendix A — Recommended PHP Debugging Tools and Configuration](#appendix-a--recommended-php-debugging-tools-and-configuration)

---

# 1. How to Use This Handbook

This handbook is designed to work in two ways:

1. **Learn debugging from the beginning.**
2. **Use it as a troubleshooting reference when something breaks.**

If you are new to PHP debugging, read roughly in this order:

```text
Debugging mindset
      ↓
PHP errors and exceptions
      ↓
Dumping variables
      ↓
Logging
      ↓
Stack traces
      ↓
Xdebug and breakpoints
      ↓
HTTP / database / files / APIs
      ↓
Production debugging
      ↓
Performance and advanced techniques
```

If you already have a bug, search this handbook for the symptom:

```text
"500 error"
"undefined array key"
"headers already sent"
"PDOException"
"class not found"
"invalid JSON"
"memory exhausted"
"permission denied"
"session"
"Xdebug"
```

---

# 2. What Debugging Really Means

Debugging is the process of finding **why the program behaves differently from what you intended**.

A bug can be obvious:

```php
<?php

echo $userName;
```

when `$userName` was never created.

But many real bugs are not obvious:

```php
if ($status = 'approved') {
    processPayment();
}
```

The programmer probably intended:

```php
if ($status === 'approved') {
    processPayment();
}
```

The first version assigns `'approved'` to `$status`. It does not compare the value.

Debugging therefore involves more than "finding an error message."

You may need to investigate:

- incorrect values
- incorrect assumptions
- unexpected control flow
- invalid database data
- API failures
- environment differences
- configuration problems
- race conditions
- file permissions
- incorrect HTTP requests
- expired sessions
- dependency problems
- performance bottlenecks
- production-only failures

A useful mental model is:

```text
Expected behavior
        ↓
Actual behavior
        ↓
Find the first point where they become different
        ↓
Understand why
        ↓
Fix the underlying cause
        ↓
Verify the fix
        ↓
Prevent regression
```

---

# 3. The Debugging Mindset

Good debugging is an investigation, not random code editing.

## 3.1 Start with facts

Bad approach:

> "It is probably MySQL."

Better approach:

> "The request reaches the controller, but the repository throws a `PDOException` while executing query X."

The second statement gives you something testable.

## 3.2 Separate symptoms from causes

Suppose the browser shows:

```text
500 Internal Server Error
```

That is a **symptom**.

Possible causes include:

- syntax error
- uncaught exception
- missing PHP extension
- file permission problem
- database failure
- exhausted memory
- invalid server configuration
- autoloader failure

Do not "fix the 500 error." Find what produced it.

## 3.3 Change one thing at a time

If you modify five parts of the application simultaneously, you may fix the bug without learning which change fixed it.

Prefer:

```text
Observation
→ hypothesis
→ one controlled change
→ retest
```

## 3.4 Reduce the problem

If a 2,000-line workflow fails, try to build a 20-line reproducer.

For example, instead of debugging the entire invoice application:

```php
<?php

$pdo = new PDO($dsn, $user, $password);

$stmt = $pdo->prepare(
    'SELECT id, invoice_no FROM invoices WHERE invoice_no = ?'
);

$stmt->execute(['INV-1001']);

var_dump($stmt->fetch(PDO::FETCH_ASSOC));
```

If this fails, you have isolated the database/query layer.

## 3.5 Never trust assumptions

Verify:

- Is this variable actually a string?
- Is this config file actually loaded?
- Is PHP CLI using the same `php.ini` as PHP-FPM?
- Did the API really return JSON?
- Did the SQL query really return one row?
- Is the requested file path really correct?
- Is the code running on the version you think it is?

---

# 4. Build a Reproducible Debugging Process

A professional debugging loop can be summarized as:

```text
REPRODUCE
   ↓
OBSERVE
   ↓
ISOLATE
   ↓
HYPOTHESIZE
   ↓
TEST
   ↓
FIX
   ↓
VERIFY
   ↓
PREVENT
```

## 4.1 Reproduce

Write the exact steps:

```text
1. Login as finance user.
2. Open invoice INV-1042.
3. Change status to Approved.
4. Click Save.
5. HTTP 500 appears.
```

Compare that with:

```text
"Sometimes approval fails."
```

The first description is actionable.

## 4.2 Capture the input

Record relevant input without exposing secrets.

Example:

```php
error_log(json_encode([
    'invoice_id' => $invoiceId,
    'status' => $status,
    'user_id' => $userId,
]));
```

Do **not** log:

```php
[
    'password' => $password,
    'access_token' => $token,
    'card_number' => $cardNumber,
]
```

## 4.3 Identify the last known-good point

Add temporary checkpoints:

```php
error_log('A: request entered controller');

$invoice = loadInvoice($id);

error_log('B: invoice loaded');

saveInvoice($invoice);

error_log('C: invoice saved');
```

If logs contain A and B but not C, the problem is around `saveInvoice()`.

---

# 5. Know Which PHP Environment Is Actually Running

A major source of confusion is having multiple PHP installations.

You may have:

- PHP CLI
- Apache PHP module
- PHP-FPM
- Docker PHP
- XAMPP/WAMP PHP
- Composer using another PHP executable

## 5.1 Check CLI PHP version

```bash
php -v
```

Example:

```text
PHP 8.x.x (cli)
```

## 5.2 Find the PHP executable

Linux/macOS:

```bash
which php
```

Windows:

```bat
where php
```

## 5.3 Find loaded configuration

```bash
php --ini
```

This tells you:

- main `php.ini`
- additional scanned `.ini` files

## 5.4 Inspect configuration values

```bash
php -i
```

Search specific settings:

Linux/macOS:

```bash
php -i | grep error_log
```

Windows:

```bat
php -i | findstr error_log
```

## 5.5 Web PHP may use another configuration

Create a temporary local development file:

```php
<?php

phpinfo();
```

Then open it through the web server.

Look at:

```text
Loaded Configuration File
Server API
PHP Version
extension_dir
```

> **Security warning:** Never leave a public `phpinfo()` page accessible on a production system. It exposes detailed environment information.

## 5.6 CLI vs FPM example

You run:

```bash
php -m
```

and see:

```text
pdo_mysql
```

But your website reports:

```text
could not find driver
```

Possible explanation:

```text
CLI PHP    → has pdo_mysql
PHP-FPM    → does not
```

Always verify the SAPI that handles the failing request.

---

# 6. PHP Error Reporting Fundamentals

PHP can report, display, and log errors.

These are different concepts:

| Setting | Purpose |
|---|---|
| `error_reporting` | Which error levels PHP reports |
| `display_errors` | Whether errors are printed to output |
| `log_errors` | Whether errors are written to a log |
| `error_log` | Where PHP sends logged errors |

## 6.1 Recommended development setup

For local development:

```ini
error_reporting = E_ALL
display_errors = On
log_errors = On
```

Or temporarily in a script:

```php
<?php

error_reporting(E_ALL);
ini_set('display_errors', '1');
```

This is useful when debugging locally.

## 6.2 Production setup

A common production approach is:

```ini
error_reporting = E_ALL
display_errors = Off
log_errors = On
```

Why?

Displaying a raw exception such as:

```text
PDOException:
SQLSTATE[HY000] [1045] Access denied for user...
```

to visitors may reveal:

- database technology
- file paths
- source code structure
- usernames
- SQL
- internal architecture

Production users should receive a controlled error response while detailed information goes to logs.

## 6.3 `error_reporting()`

### What it does

Sets which PHP errors are reported during the current script execution.

### Syntax

```php
error_reporting(?int $error_level = null): int
```

### Common use

```php
error_reporting(E_ALL);
```

### Read the current level

```php
$current = error_reporting();

var_dump($current);
```

## 6.4 `ini_set()`

Changes a configurable PHP setting for the current request.

```php
ini_set('display_errors', '1');
```

It does not permanently modify `php.ini`.

## 6.5 Why `ini_set()` may not solve every startup error

If PHP fails before your script gets far enough to execute:

```php
ini_set('display_errors', '1');
```

then that line cannot help.

In such cases inspect:

- PHP error log
- web server log
- PHP-FPM log
- `php.ini`
- startup messages
- service logs

---

# 7. PHP Errors, Exceptions, and `Throwable`

Modern PHP uses multiple error-handling mechanisms.

At a high level:

```text
Throwable
├── Error
│   ├── TypeError
│   ├── ValueError
│   ├── ParseError
│   └── ...
└── Exception
    ├── RuntimeException
    ├── InvalidArgumentException
    ├── PDOException
    └── ...
```

Both `Error` and `Exception` implement `Throwable`.

## 7.1 Catching an exception

```php
try {
    throw new RuntimeException('Could not load invoice');
} catch (RuntimeException $e) {
    echo $e->getMessage();
}
```

Output:

```text
Could not load invoice
```

## 7.2 Catching a type error

```php
function add(int $a, int $b): int
{
    return $a + $b;
}

try {
    add([], 10);
} catch (TypeError $e) {
    echo $e->getMessage();
}
```

## 7.3 Catching any `Throwable`

At a high-level application boundary:

```php
try {
    runApplication();
} catch (Throwable $e) {
    error_log($e->__toString());

    http_response_code(500);

    echo 'Something went wrong.';
}
```

Use this carefully.

Catching `Throwable` everywhere can hide programming mistakes.

A good pattern is:

```text
Specific low-level catches where recovery is possible
+
One high-level global boundary for unexpected failures
```

## 7.4 `try`, `catch`, and `finally`

```php
$handle = fopen('data.txt', 'r');

try {
    processFile($handle);
} catch (RuntimeException $e) {
    error_log($e->getMessage());
} finally {
    if (is_resource($handle)) {
        fclose($handle);
    }
}
```

`finally` executes whether or not an exception occurs.

Typical uses:

- close resources
- release locks
- cleanup temporary files
- reset temporary state

## 7.5 Multiple catches

```php
try {
    processOrder();
} catch (InvalidArgumentException $e) {
    // Bad input
} catch (PDOException $e) {
    // Database problem
} catch (RuntimeException $e) {
    // Application problem
}
```

Put more specific catches before broad ones.

## 7.6 Multi-catch

```php
try {
    processOrder();
} catch (InvalidArgumentException | DomainException $e) {
    error_log($e->getMessage());
}
```

Use it when different exception classes should be handled the same way.

---

# 8. Reading PHP Error Messages and Stack Traces

An error often tells you:

```text
WHAT happened
WHERE it happened
HOW execution reached that point
```

Example:

```text
Fatal error: Uncaught TypeError:
calculateTotal(): Argument #1 ($amount) must be of type float, string given
in /app/src/Invoice.php:42

Stack trace:
#0 /app/public/index.php(18): calculateTotal('abc')
#1 {main}
```

Break it down:

```text
Type: TypeError

Function:
calculateTotal()

Problem:
Argument #1 should be float

Actual input:
string

Failure location:
/app/src/Invoice.php:42

Caller:
/app/public/index.php:18
```

## 8.1 Do not only inspect the top line

The most useful frame may be the caller.

Example:

```text
#0 calculateTotal('abc')
#1 InvoiceService->create(...)
#2 InvoiceController->store(...)
```

The function itself may be correct.

The real bug may be in the code that passed `'abc'`.

## 8.2 Useful exception methods

```php
catch (Throwable $e) {
    echo $e->getMessage();
    echo $e->getFile();
    echo $e->getLine();
    echo $e->getTraceAsString();
}
```

Useful methods include:

```php
$e->getMessage();
$e->getCode();
$e->getFile();
$e->getLine();
$e->getTrace();
$e->getTraceAsString();
$e->getPrevious();
```

## 8.3 Logging an exception

Instead of manually formatting every property:

```php
error_log((string) $e);
```

This generally includes useful stack information.

---

# 9. Fast Inspection with `var_dump()`, `print_r()`, and Friends

Sometimes the fastest debugging tool is simply inspecting a value.

---

## 9.1 `var_dump()`

### What it does

Displays:

- type
- value
- string length
- array structure
- object structure

Example:

```php
$user = [
    'id' => 10,
    'name' => 'Asha',
    'active' => true,
];

var_dump($user);
```

Typical output:

```text
array(3) {
  ["id"]=>
  int(10)
  ["name"]=>
  string(4) "Asha"
  ["active"]=>
  bool(true)
}
```

### When to use

Use `var_dump()` when **type matters**.

For example:

```php
var_dump("10");
var_dump(10);
```

Output differs:

```text
string(2) "10"
int(10)
```

That distinction can explain bugs involving strict comparison.

---

## 9.2 `print_r()`

Good for quickly viewing arrays and objects.

```php
print_r($_POST);
```

Example:

```text
Array
(
    [name] => Asha
    [email] => asha@example.com
)
```

Compared with `var_dump()`, it is often easier to read but contains less type information.

---

## 9.3 `var_export()`

Produces a PHP-like representation.

```php
$config = [
    'debug' => true,
    'limit' => 20,
];

var_export($config);
```

Output:

```php
array (
  'debug' => true,
  'limit' => 20,
)
```

A useful property is that `var_export($value, true)` returns the representation as a string.

```php
error_log(var_export($config, true));
```

---

## 9.4 `gettype()`

```php
$value = '123';

echo gettype($value);
```

Output:

```text
string
```

---

## 9.5 `is_*()` helpers

Examples:

```php
is_string($value);
is_int($value);
is_float($value);
is_array($value);
is_object($value);
is_null($value);
is_bool($value);
is_callable($value);
is_resource($value);
```

Useful when debugging uncertain input.

---

## 9.6 `isset()` vs `array_key_exists()`

These are often confused.

```php
$data = [
    'name' => null,
];
```

Then:

```php
var_dump(isset($data['name']));
```

Output:

```text
bool(false)
```

But:

```php
var_dump(array_key_exists('name', $data));
```

Output:

```text
bool(true)
```

Why?

`isset()` returns false when the value is `null`.

`array_key_exists()` checks whether the key exists even if its value is `null`.

---

## 9.7 `dump-and-die` pattern

Plain PHP does not need a framework helper.

You can temporarily write:

```php
var_dump($value);
exit;
```

or:

```php
print_r($value);
die;
```

Useful during local debugging, but remove temporary debugging exits before merging code.

---

# 10. Logging with `error_log()` and Application Logs

Printing debug output changes the HTTP response.

Logging is often safer.

## 10.1 Basic logging

```php
error_log('Invoice processing started');
```

## 10.2 Log a variable

```php
error_log(var_export($invoice, true));
```

or:

```php
error_log(json_encode($invoice));
```

## 10.3 Structured logging

Instead of:

```php
error_log('Invoice error');
```

prefer:

```php
error_log(json_encode([
    'event' => 'invoice_processing_failed',
    'invoice_id' => $invoiceId,
    'user_id' => $userId,
    'request_id' => $requestId,
]));
```

Structured logs are easier to search and process.

## 10.4 Add correlation/request IDs

Imagine 100 users call the API simultaneously.

This log:

```text
Payment failed
```

is difficult to investigate.

This is better:

```text
request_id=9fd12 invoice_id=4201 payment failed
```

Generate a request identifier:

```php
$requestId = bin2hex(random_bytes(8));
```

Then include it in related logs.

## 10.5 Never log secrets

Avoid logging:

- passwords
- session IDs
- private API tokens
- full authorization headers
- access tokens
- refresh tokens
- private keys
- credit card data
- full personal records unless truly necessary

Instead:

```php
error_log(json_encode([
    'user_id' => $userId,
    'token_present' => isset($token),
]));
```

---

# 11. Custom Error and Exception Handlers

PHP allows you to register application-level handlers.

---

## 11.1 `set_error_handler()`

Registers a callback for many PHP runtime errors.

Example:

```php
set_error_handler(
    function (
        int $severity,
        string $message,
        string $file,
        int $line
    ): bool {
        error_log(
            "PHP error [$severity] $message in $file:$line"
        );

        return true;
    }
);
```

### Parameters

The handler can receive:

```text
severity → error level
message  → error description
file     → source file
line     → source line
```

### Return value

Returning `true` means your handler handled the error.

Returning `false` allows PHP's normal error handler to continue.

---

## 11.2 Convert selected PHP errors into `ErrorException`

A commonly used development pattern:

```php
set_error_handler(
    function (
        int $severity,
        string $message,
        string $file,
        int $line
    ): bool {
        if (!(error_reporting() & $severity)) {
            return false;
        }

        throw new ErrorException(
            $message,
            0,
            $severity,
            $file,
            $line
        );
    }
);
```

Now many traditional PHP warnings/notices can behave like exceptions.

Use with care because not every PHP engine error can be handled through `set_error_handler()`.

---

## 11.3 `set_exception_handler()`

Handles uncaught exceptions/throwables at the application boundary.

```php
set_exception_handler(
    function (Throwable $e): void {
        error_log((string) $e);

        http_response_code(500);

        echo 'Unexpected application error.';
    }
);
```

Once this handler runs for an uncaught throwable, normal execution does not continue.

---

# 12. Debugging Fatal Shutdown Problems

Sometimes you want information at shutdown.

PHP provides:

```php
register_shutdown_function()
```

and:

```php
error_get_last()
```

Example:

```php
register_shutdown_function(
    function (): void {
        $error = error_get_last();

        if ($error !== null) {
            error_log(json_encode([
                'type' => $error['type'],
                'message' => $error['message'],
                'file' => $error['file'],
                'line' => $error['line'],
            ]));
        }
    }
);
```

This can be useful as an application-level last-resort logger.

Do not treat it as a replacement for proper exceptions and logging.

---

# 13. Assertions for Development-Time Checks

Assertions document assumptions.

```php
assert($invoiceId > 0);
```

A more informative version:

```php
assert(
    $invoiceId > 0,
    'Invoice ID must be positive'
);
```

Typical development use:

```php
function calculateDiscount(float $amount): float
{
    assert($amount >= 0);

    return $amount * 0.10;
}
```

Assertions are for internal invariants, not normal user-input validation.

Do **not** replace:

```php
if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
    // reject user input
}
```

with:

```php
assert(filter_var($email, FILTER_VALIDATE_EMAIL));
```

External input must always be validated explicitly.

---

# 14. Xdebug: The Essential PHP Debugger

Xdebug is a PHP extension designed for development and debugging.

It can help with:

- step debugging
- breakpoints
- stack traces
- variable inspection
- function traces
- profiling
- code coverage
- improved development diagnostics

## 14.1 Why Xdebug is different from `var_dump()`

With `var_dump()`:

```text
Edit code
→ refresh
→ inspect
→ edit
→ refresh
```

With a step debugger:

```text
Set breakpoint
→ run request
→ PHP pauses
→ inspect variables
→ step line by line
→ inspect call stack
```

This is much more powerful for complex control flow.

## 14.2 Check whether Xdebug is installed

```bash
php -v
```

or:

```bash
php -m
```

You can also run:

```bash
php --ri xdebug
```

If installed, this prints Xdebug configuration.

## 14.3 Important Xdebug 3 settings

Typical development configuration:

```ini
zend_extension=xdebug

xdebug.mode=develop,debug
xdebug.start_with_request=yes
xdebug.client_host=127.0.0.1
xdebug.client_port=9003
```

For trigger-based debugging:

```ini
xdebug.start_with_request=trigger
```

This avoids starting a debugger connection for every request.

## 14.4 `xdebug.mode`

Common modes include:

```text
develop
debug
profile
trace
coverage
gcstats
```

You normally enable only what you need.

For everyday step debugging:

```ini
xdebug.mode=debug
```

For improved developer information plus step debugging:

```ini
xdebug.mode=develop,debug
```

Avoid enabling expensive modes unnecessarily in production.

## 14.5 Xdebug diagnostic information

Create a temporary local page:

```php
<?php

xdebug_info();
```

This can help diagnose:

- enabled modes
- configuration
- debugger connection settings
- loaded ini file

---

# 15. Step Debugging with VS Code

A common setup is:

```text
PHP + Xdebug
      ↕ DBGp
VS Code + PHP Debug extension
```

## 15.1 Basic VS Code launch configuration

A typical `.vscode/launch.json` entry:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Listen for Xdebug",
      "type": "php",
      "request": "launch",
      "port": 9003
    }
  ]
}
```

Workflow:

```text
1. Install Xdebug.
2. Configure `xdebug.mode=debug`.
3. Configure port 9003.
4. Install a PHP debugger extension in VS Code.
5. Start "Listen for Xdebug".
6. Add a breakpoint.
7. Open the PHP page/request.
8. Execution pauses at the breakpoint.
```

## 15.2 Path mapping

If PHP runs inside Docker or on a remote server, PHP may report:

```text
/var/www/html/app/Service.php
```

while VS Code has:

```text
C:\Projects\app\Service.php
```

The debugger needs path mapping.

Example:

```json
{
  "name": "Listen for Xdebug in Docker",
  "type": "php",
  "request": "launch",
  "port": 9003,
  "pathMappings": {
    "/var/www/html": "${workspaceFolder}"
  }
}
```

Incorrect path mappings are a common reason for:

```text
Xdebug connects
but breakpoints do not bind
```

---

# 16. Breakpoints, Watches, Call Stacks, and Step Controls

## 16.1 Breakpoint

A breakpoint tells the debugger:

> Pause when execution reaches this line.

Example:

```php
$invoice = $repository->find($invoiceId); // breakpoint here
```

When paused, inspect:

```text
$invoiceId
$invoice
$_POST
$_SESSION
$this
```

## 16.2 Conditional breakpoint

Pause only when a condition is true.

Example idea:

```text
$invoiceId === 4201
```

Useful when a loop runs thousands of times.

## 16.3 Step Over

Execute the current line without entering called functions.

```php
$total = calculateTotal($items);
```

Step Over executes `calculateTotal()` and stops on the next line.

## 16.4 Step Into

Enter the called function.

```php
$total = calculateTotal($items);
```

Step Into opens the internals of `calculateTotal()`.

## 16.5 Step Out

Finish the current function and return to its caller.

Useful when you accidentally step into library code.

## 16.6 Continue

Resume normal execution until:

- another breakpoint
- an exception breakpoint
- script completion

## 16.7 Watch expressions

You can monitor expressions such as:

```php
count($items)
```

```php
$invoice['status'] ?? null
```

```php
$total > 100000
```

Use watches when repeatedly checking the same value.

## 16.8 Call stack

Suppose execution is:

```text
index.php
  → InvoiceController::store()
    → InvoiceService::approve()
      → InvoiceRepository::update()
```

The call stack helps answer:

> How did execution get here?

---

# 17. Debugging PHP from the Command Line

CLI programs often behave differently from web requests.

## 17.1 Run a script

```bash
php script.php
```

## 17.2 Enable maximum error reporting from CLI

```bash
php -d display_errors=1 -d error_reporting=E_ALL script.php
```

## 17.3 Syntax check without execution

```bash
php -l script.php
```

Expected success:

```text
No syntax errors detected in script.php
```

This is extremely useful in:

- pre-commit hooks
- CI
- deployment validation
- quick syntax checks

## 17.4 Inspect CLI arguments

```php
<?php

var_dump($argv);
```

Run:

```bash
php command.php invoice 1001
```

Possible output:

```text
array(3) {
  [0]=> string(...) "command.php"
  [1]=> string(7) "invoice"
  [2]=> string(4) "1001"
}
```

## 17.5 Exit codes

CLI tools should use exit codes.

```php
if ($failed) {
    fwrite(STDERR, "Import failed\n");
    exit(1);
}

exit(0);
```

Conventionally:

```text
0     success
non-0 failure
```

This matters in shell scripts and CI/CD.

---

# 18. Debugging Web Requests and HTTP Problems

A PHP web request involves more than PHP source code.

Simplified flow:

```text
Browser
  ↓
DNS / network
  ↓
Web server
  ↓
PHP-FPM or PHP runtime
  ↓
Application router/controller
  ↓
Business logic
  ↓
Database/API/files
  ↓
Response
  ↓
Browser
```

A failure may happen at any stage.

## 18.1 Inspect the browser Network panel

Developer Tools → Network helps you inspect:

- URL
- method
- status code
- request headers
- request body
- response headers
- response body
- duration

## 18.2 Important HTTP status codes

| Status | Meaning |
|---|---|
| 200 | Request succeeded |
| 201 | Resource created |
| 204 | Success with no response body |
| 400 | Bad client request |
| 401 | Authentication required/failed |
| 403 | Authenticated but forbidden, or access denied |
| 404 | Resource not found |
| 405 | HTTP method not allowed |
| 409 | Conflict |
| 422 | Semantically invalid/validation error |
| 429 | Too many requests |
| 500 | Internal server/application error |
| 502 | Bad gateway/upstream problem |
| 503 | Service unavailable |
| 504 | Gateway timeout |

Do not assume every `500` is a PHP syntax problem.

## 18.3 Inspect request method

```php
var_dump($_SERVER['REQUEST_METHOD']);
```

## 18.4 Inspect URI

```php
var_dump($_SERVER['REQUEST_URI']);
```

## 18.5 Check response status

Set explicitly:

```php
http_response_code(404);
```

---

# 19. Debugging APIs and JSON

API bugs often involve:

```text
Wrong content type
Wrong JSON shape
Invalid JSON
Incorrect status
Missing auth header
Unexpected null
API timeout
Different field type
```

## 19.1 Read JSON request body

```php
$raw = file_get_contents('php://input');

$data = json_decode($raw, true);
```

## 19.2 Detect JSON decoding failure

Prefer throwing behavior when appropriate:

```php
try {
    $data = json_decode(
        $raw,
        true,
        512,
        JSON_THROW_ON_ERROR
    );
} catch (JsonException $e) {
    http_response_code(400);

    echo json_encode([
        'error' => 'Invalid JSON',
    ]);
}
```

## 19.3 Without `JSON_THROW_ON_ERROR`

You can inspect:

```php
$data = json_decode($raw, true);

if (json_last_error() !== JSON_ERROR_NONE) {
    echo json_last_error_msg();
}
```

## 19.4 Encode a JSON response

```php
header('Content-Type: application/json');

echo json_encode([
    'success' => true,
    'data' => $result,
], JSON_THROW_ON_ERROR);
```

## 19.5 Debug response contamination

A common API failure:

```php
var_dump($user);

echo json_encode($response);
```

The response becomes something like:

```text
array(2) { ... }
{"success":true}
```

That is no longer valid JSON.

For APIs, prefer logs over browser-facing dumps.

---

# 20. Debugging HTML Forms and Request Data

## 20.1 Inspect `$_GET`

URL:

```text
/search.php?q=php
```

PHP:

```php
var_dump($_GET);
```

## 20.2 Inspect `$_POST`

```php
var_dump($_POST);
```

## 20.3 Missing form field

Unsafe:

```php
$name = $_POST['name'];
```

If `name` is missing, PHP may report an undefined array key.

Safer:

```php
$name = $_POST['name'] ?? null;
```

Then validate:

```php
if ($name === null || trim($name) === '') {
    // validation failure
}
```

## 20.4 HTML field must have `name`

This:

```html
<input type="text" id="email">
```

will not create a normal form field called `email`.

Use:

```html
<input type="text" id="email" name="email">
```

## 20.5 Check form method

HTML:

```html
<form method="post">
```

PHP must inspect:

```php
$_POST
```

not:

```php
$_GET
```

---

# 21. Debugging File Uploads

HTML form:

```html
<form method="post" enctype="multipart/form-data">
    <input type="file" name="document">
    <button type="submit">Upload</button>
</form>
```

PHP:

```php
var_dump($_FILES);
```

## 21.1 Important upload fields

```php
$_FILES['document']['name'];
$_FILES['document']['type'];
$_FILES['document']['tmp_name'];
$_FILES['document']['error'];
$_FILES['document']['size'];
```

## 21.2 Check upload error first

```php
if (
    !isset($_FILES['document']) ||
    $_FILES['document']['error'] !== UPLOAD_ERR_OK
) {
    throw new RuntimeException('Upload failed');
}
```

## 21.3 Common causes

- missing `multipart/form-data`
- file exceeds `upload_max_filesize`
- request exceeds `post_max_size`
- temporary directory issue
- destination permission failure
- incorrect `move_uploaded_file()` target
- reverse proxy upload limit

## 21.4 Never trust browser MIME type alone

Validate the actual file content/type using appropriate server-side checks.

---

# 22. Debugging Sessions and Cookies

## 22.1 Start the session before using `$_SESSION`

```php
session_start();

$_SESSION['user_id'] = 10;
```

## 22.2 Inspect session data

```php
var_dump($_SESSION);
```

## 22.3 Common session problems

- `session_start()` not called
- session cookie not sent
- cookie domain mismatch
- HTTP/HTTPS mismatch
- output already sent
- session storage permission problem
- load balancer sends requests to different servers without shared session storage
- session regenerated or destroyed unexpectedly

## 22.4 Inspect session ID

Development-only:

```php
var_dump(session_id());
```

Do not expose real session identifiers publicly or log them unnecessarily.

## 22.5 Cookie debugging

Inspect:

```php
var_dump($_COOKIE);
```

Also inspect browser DevTools:

```text
Application/Storage → Cookies
```

Check flags such as:

- Secure
- HttpOnly
- SameSite
- Domain
- Path
- expiration

---

# 23. Debugging Headers and Redirects

## 23.1 `headers already sent`

Example:

```php
echo 'Debug';

header('Location: dashboard.php');
```

PHP has already started sending response content.

Then changing headers may fail.

Correct pattern:

```php
header('Location: dashboard.php');
exit;
```

Do not output content before the redirect.

## 23.2 Find where output started

Use:

```php
if (headers_sent($file, $line)) {
    error_log("Headers already sent at $file:$line");
}
```

## 23.3 Common invisible causes

- whitespace before `<?php`
- output from an included file
- debugging `echo`
- BOM in a source file
- warning printed before `header()`

---

# 24. Debugging Include, Require, Autoload, and Composer Problems

## 24.1 `include` vs `require`

```php
include 'config.php';
```

Failure generally raises a warning and the script may continue.

```php
require 'config.php';
```

Failure prevents normal continuation.

For essential bootstrap files, `require` is usually more appropriate.

## 24.2 Use `__DIR__`

Fragile:

```php
require '../config/config.php';
```

More predictable:

```php
require __DIR__ . '/../config/config.php';
```

This anchors the path to the current file.

## 24.3 Debug path problems

```php
$path = __DIR__ . '/../config/config.php';

var_dump($path);
var_dump(file_exists($path));
var_dump(realpath($path));
```

## 24.4 Composer autoload

Typical:

```php
require __DIR__ . '/vendor/autoload.php';
```

If classes are not found, investigate:

```text
Was `composer install` run?
Does vendor/autoload.php exist?
Does composer.json contain correct autoload rules?
Does namespace match directory structure?
Was autoload metadata regenerated?
```

Useful Composer command:

```bash
composer dump-autoload
```

For environment diagnostics:

```bash
composer diagnose
```

---

# 25. Debugging Namespaces and Class Resolution

Example file:

```php
namespace App\Service;

class InvoiceService
{
}
```

Usage:

```php
use App\Service\InvoiceService;

$service = new InvoiceService();
```

## 25.1 Common mistake

Class namespace:

```php
namespace App\Services;
```

Usage:

```php
use App\Service\InvoiceService;
```

Notice:

```text
Services
vs
Service
```

## 25.2 Debug class availability

```php
var_dump(class_exists(App\Service\InvoiceService::class));
```

## 25.3 Inspect resolved class name

```php
echo InvoiceService::class;
```

---

# 26. Debugging Types, Null Values, and Function Arguments

Modern PHP applications often fail because the value is not the type the programmer expects.

## 26.1 Strict comparison

```php
$value = '10';

var_dump($value == 10);
var_dump($value === 10);
```

Typical result:

```text
bool(true)
bool(false)
```

`===` compares value **and type**.

Use strict comparisons when type matters.

## 26.2 Nullable values

```php
function findUser(int $id): ?array
{
    // ...
}
```

Caller:

```php
$user = findUser(10);

echo $user['name'];
```

If `findUser()` returns `null`, the caller fails.

Better:

```php
if ($user === null) {
    // handle missing user
}
```

## 26.3 Null-safe operator

```php
$name = $user?->profile?->name;
```

This prevents dereferencing a null object at those points.

However, do not use `?->` merely to hide a state that should never be null.

## 26.4 Inspect values before boundaries

Before calling:

```php
createInvoice($vendorId, $amount);
```

inspect:

```php
var_dump([
    'vendorId' => $vendorId,
    'vendorIdType' => gettype($vendorId),
    'amount' => $amount,
    'amountType' => gettype($amount),
]);
```

This often reveals hidden string/integer/null problems.

---

# 27. Debugging Arrays and Collections

## 27.1 Undefined array key

Problem:

```php
echo $user['email'];
```

when:

```php
$user = ['name' => 'Asha'];
```

Better:

```php
$email = $user['email'] ?? null;
```

But ask **why the key is missing**.

The null coalescing operator is not a substitute for understanding the data contract.

## 27.2 Dump keys

```php
var_dump(array_keys($user));
```

Useful when data shape is unexpected.

## 27.3 Count safely

If you are not sure the value is an array:

```php
if (!is_array($items)) {
    throw new UnexpectedValueException(
        'Expected items to be an array'
    );
}

echo count($items);
```

## 27.4 Debug mapping transformations

```php
$result = array_map(
    fn ($item) => $item['price'] * $item['qty'],
    $items
);
```

If it fails, inspect one input:

```php
var_dump($items[0] ?? null);
```

Then verify the expected keys and types.

---

# 28. Debugging Strings, Encoding, and Unicode

## 28.1 Visualize hidden whitespace

```php
var_dump($value);
```

If:

```php
$value = "approved\n";
```

then:

```php
$value === 'approved'
```

is false.

Try:

```php
$value = trim($value);
```

## 28.2 Inspect bytes when needed

```php
echo bin2hex($value);
```

Useful for invisible bytes or encoding issues.

## 28.3 JSON and UTF-8

`json_encode()` expects valid UTF-8 strings.

Prefer:

```php
json_encode($data, JSON_THROW_ON_ERROR);
```

so invalid encoding becomes visible as an exception rather than a silently ignored problem.

## 28.4 Multibyte strings

For Unicode-aware string operations, the `mbstring` extension is often needed.

Example:

```php
mb_strlen($text, 'UTF-8');
```

Do not assume byte length equals character length.

---

# 29. Debugging Date, Time, and Time Zones

Time bugs are common because a timestamp depends on:

```text
input
+ format
+ timezone
+ daylight-saving rules
+ database storage convention
```

## 29.1 Check runtime timezone

```php
echo date_default_timezone_get();
```

## 29.2 Set timezone intentionally

```php
date_default_timezone_set('Asia/Kolkata');
```

Application-wide configuration is preferable to random timezone changes in different files.

## 29.3 Use immutable date objects when practical

```php
$createdAt = new DateTimeImmutable(
    '2026-08-17 10:00:00',
    new DateTimeZone('Asia/Kolkata')
);
```

## 29.4 Debug formatted values

```php
var_dump([
    'timezone' => $createdAt->getTimezone()->getName(),
    'iso' => $createdAt->format(DATE_ATOM),
    'timestamp' => $createdAt->getTimestamp(),
]);
```

## 29.5 Common bug

Database stores UTC:

```text
2026-08-17 04:30:00 UTC
```

UI assumes it is already local:

```text
2026-08-17 04:30
```

The displayed time becomes incorrect.

Define a project convention, for example:

```text
Store UTC
→ convert to user timezone at presentation boundary
```

---

# 30. Debugging Regular Expressions

Regex bugs can be hard to see.

Example:

```php
$matched = preg_match('/^\d{6}$/', '400009');

var_dump($matched);
```

Possible return values:

```text
1      matched
0      did not match
false  regex error
```

Use strict checking:

```php
$result = preg_match($pattern, $subject);

if ($result === false) {
    throw new RuntimeException(
        preg_last_error_msg()
    );
}

if ($result === 1) {
    // matched
}
```

Do not write:

```php
if (!preg_match(...)) {
```

if you must distinguish "no match" from "regex failure."

---

# 31. Debugging PDO Database Code

PDO can expose database problems through exceptions.

## 31.1 Connection example

```php
$pdo = new PDO(
    $dsn,
    $username,
    $password,
    [
        PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
    ]
);
```

Modern PDO behavior should still be made explicit in reusable examples so the intended error mode is obvious.

## 31.2 Query with prepared statement

```php
$stmt = $pdo->prepare(
    'SELECT id, email
     FROM users
     WHERE id = :id'
);

$stmt->execute([
    'id' => $userId,
]);

$user = $stmt->fetch(PDO::FETCH_ASSOC);
```

## 31.3 Catch database failures

```php
try {
    $stmt->execute(['id' => $userId]);
} catch (PDOException $e) {
    error_log((string) $e);

    throw new RuntimeException(
        'Unable to load user',
        0,
        $e
    );
}
```

Notice that the public/application exception does not need to expose the SQL error to the user.

## 31.4 Debug SQL input safely

Instead of concatenating SQL:

```php
$sql = "SELECT * FROM users WHERE email = '$email'";
```

prefer:

```php
$sql = 'SELECT * FROM users WHERE email = :email';

$stmt = $pdo->prepare($sql);

$stmt->execute([
    'email' => $email,
]);
```

Prepared statements improve safety and make input boundaries clearer.

## 31.5 Inspect row count assumptions

If your code expects one row:

```php
$user = $stmt->fetch(PDO::FETCH_ASSOC);

if ($user === false) {
    // no row
}
```

Do not assume `fetch()` always returns an array.

## 31.6 `errorInfo()`

When using an error mode where you need manual inspection:

```php
var_dump($pdo->errorInfo());
```

For statement-level errors:

```php
var_dump($stmt->errorInfo());
```

The statement and connection can have different last-operation error information.

---

# 32. Debugging MySQLi Database Code

Modern MySQLi can be configured to report failures as exceptions.

```php
mysqli_report(
    MYSQLI_REPORT_ERROR | MYSQLI_REPORT_STRICT
);

$mysqli = new mysqli(
    $host,
    $username,
    $password,
    $database
);
```

Then:

```php
$stmt = $mysqli->prepare(
    'SELECT id, email FROM users WHERE id = ?'
);

$stmt->bind_param('i', $userId);
$stmt->execute();
```

Catch:

```php
try {
    // query
} catch (mysqli_sql_exception $e) {
    error_log((string) $e);
}
```

Manual diagnostics include:

```php
$mysqli->errno;
$mysqli->error;
$mysqli->error_list;
```

Prefer exceptions or centralized error handling instead of scattering manual checks everywhere.

---

# 33. Debugging Transactions

Transactions create bugs when:

- rollback does not happen
- commit happens too early
- exceptions are swallowed
- one database update succeeds but another fails
- external side effects occur inside a transaction

## 33.1 Correct basic pattern

```php
$pdo->beginTransaction();

try {
    createInvoice($pdo, $invoice);
    createLedgerEntry($pdo, $invoice);

    $pdo->commit();
} catch (Throwable $e) {
    if ($pdo->inTransaction()) {
        $pdo->rollBack();
    }

    throw $e;
}
```

## 33.2 Debug transaction boundaries

Log:

```php
error_log('TX BEGIN');
error_log('INSERT INVOICE');
error_log('INSERT LEDGER');
error_log('TX COMMIT');
```

If you see:

```text
TX BEGIN
INSERT INVOICE
```

but no later entries, investigate the second operation.

## 33.3 Do not debug only the final database state

A rollback may correctly erase partial changes.

Logs and stack traces can show the point of failure.

---

# 34. Debugging SQL Logic and Data Problems

Sometimes SQL executes successfully but returns the wrong result.

That is a logic bug, not a database connection error.

## 34.1 Verify inputs

```php
error_log(json_encode([
    'invoice_no' => $invoiceNo,
    'company_id' => $companyId,
    'location_id' => $locationId,
]));
```

## 34.2 Reproduce the query directly

Use your database client to run a safe equivalent with known values.

Questions:

```text
Does the row exist?
Are filters too restrictive?
Is NULL involved?
Are dates formatted correctly?
Is collation/case behavior relevant?
Did a JOIN remove rows?
Is a LEFT JOIN accidentally behaving like INNER JOIN?
```

## 34.3 Check `NULL`

SQL:

```sql
WHERE deleted_at = NULL
```

is generally not the correct null test.

Use:

```sql
WHERE deleted_at IS NULL
```

## 34.4 Debug joins progressively

Start:

```sql
SELECT *
FROM invoices
WHERE id = 1001;
```

Then add:

```sql
JOIN vendors ...
```

Then:

```sql
JOIN locations ...
```

This helps identify which join removes or duplicates rows.

---

# 35. Debugging AJAX and Frontend-to-PHP Requests

When JavaScript calls PHP, debug both ends.

Example frontend:

```javascript
fetch('/api/invoices/1001')
  .then(async response => {
    const text = await response.text();

    console.log(response.status);
    console.log(text);
  });
```

Why inspect text first?

Because if the backend accidentally returns:

```text
Warning: Undefined array key...
{"success":true}
```

calling:

```javascript
response.json()
```

may only tell you:

```text
Unexpected token...
```

The raw response reveals the PHP warning.

Backend:

```php
header('Content-Type: application/json');

try {
    $data = loadInvoice(1001);

    echo json_encode([
        'success' => true,
        'data' => $data,
    ], JSON_THROW_ON_ERROR);
} catch (Throwable $e) {
    error_log((string) $e);

    http_response_code(500);

    echo json_encode([
        'success' => false,
        'error' => 'Internal error',
    ]);
}
```

---

# 36. Debugging Authentication and Authorization

Do not treat these as the same problem.

```text
Authentication:
Who are you?

Authorization:
Are you allowed to perform this action?
```

## 36.1 Useful checkpoints

```php
error_log(json_encode([
    'authenticated' => $user !== null,
    'user_id' => $user?->id,
    'action' => 'invoice.approve',
    'invoice_id' => $invoiceId,
]));
```

Avoid logging secrets.

## 36.2 Debug decision layers

Example:

```text
Request
→ session/token accepted?
→ user loaded?
→ account active?
→ role loaded?
→ permission mapped?
→ resource ownership/department rule?
→ action allowed?
```

This is better than simply dumping:

```php
var_dump($user);
```

and guessing.

---

# 37. Debugging Filesystem and Permission Problems

Common errors:

```text
Permission denied
No such file or directory
Failed to open stream
Read-only file system
```

## 37.1 Inspect exact path

```php
var_dump($path);
var_dump(file_exists($path));
var_dump(is_readable($path));
var_dump(is_writable(dirname($path)));
```

## 37.2 Relative paths are risky

Instead of:

```php
file_get_contents('data/config.json');
```

prefer an anchored path:

```php
file_get_contents(
    __DIR__ . '/data/config.json'
);
```

## 37.3 Web process identity matters

A file may be writable by your SSH user but not by:

- PHP-FPM user
- Apache user
- container user

So:

```text
"It works when I manually run PHP"
```

does not prove the web process has permission.

## 37.4 Avoid the lazy `chmod 777` fix

World-writable permissions can create security problems.

Determine:

```text
Which user needs access?
Which group should own the directory?
What minimum permission is required?
```

Fix ownership and permission intentionally.

---

# 38. Debugging Email and External Services

External operations can fail outside your code.

Examples:

- DNS failure
- connection timeout
- SMTP rejection
- TLS/certificate problem
- invalid credentials
- provider rate limit
- invalid recipient
- provider outage

Your application should record enough context to distinguish:

```text
"sendMail() returned failure"
```

from:

```text
"SMTP connection timed out after N seconds"
```

Log:

- provider/service
- operation
- non-sensitive request identifier
- recipient domain if appropriate
- exception type
- error code
- latency

Do not log full email contents unless your data policy permits it.

---

# 39. Debugging cURL and Third-Party APIs

## 39.1 Basic cURL error inspection

```php
$ch = curl_init('https://api.example.com/data');

curl_setopt_array($ch, [
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_TIMEOUT => 10,
]);

$response = curl_exec($ch);

if ($response === false) {
    throw new RuntimeException(
        curl_error($ch)
    );
}

$status = curl_getinfo(
    $ch,
    CURLINFO_RESPONSE_CODE
);

curl_close($ch);
```

## 39.2 Transport success is not API success

`curl_exec()` may succeed while the server returns:

```text
401
404
422
500
```

Always inspect both:

```text
transport error
HTTP status
response body
```

## 39.3 Log carefully

Good:

```php
error_log(json_encode([
    'service' => 'payment-api',
    'status' => $status,
    'request_id' => $requestId,
]));
```

Dangerous:

```php
error_log($authorizationHeader);
```

---

# 40. Debugging Memory Problems

Typical error:

```text
Allowed memory size ... bytes exhausted
```

Do not immediately increase `memory_limit`.

First investigate why memory grows.

## 40.1 Measure memory

```php
echo memory_get_usage(true);
```

Peak:

```php
echo memory_get_peak_usage(true);
```

## 40.2 Format readable memory values

```php
function formatBytes(int $bytes): string
{
    return round($bytes / 1024 / 1024, 2) . ' MB';
}

echo formatBytes(memory_get_usage(true));
```

## 40.3 Common memory causes

- loading a huge database result into an array
- reading a large file completely
- decoding giant JSON
- keeping unnecessary references
- recursive logic
- image/PDF processing
- processing thousands of records in one batch
- ORM hydration of huge datasets

## 40.4 Process in chunks

Instead of:

```php
$rows = fetchOneMillionRows();
```

use pagination, streaming, or chunked processing when supported by your architecture.

---

# 41. Debugging Slow PHP Applications

A slow page does not tell you what is slow.

Possible components:

```text
PHP CPU
Database
Filesystem
DNS
Third-party API
Network
Locking
Session
Template rendering
Serialization
Cache miss
```

## 41.1 Simple timing

```php
$start = microtime(true);

$result = expensiveOperation();

$duration = microtime(true) - $start;

error_log(
    'expensiveOperation duration=' .
    round($duration, 4) .
    's'
);
```

## 41.2 Measure multiple stages

```php
$t0 = microtime(true);

$user = loadUser();
$t1 = microtime(true);

$orders = loadOrders();
$t2 = microtime(true);

$html = renderPage();
$t3 = microtime(true);

error_log(json_encode([
    'load_user_ms' => ($t1 - $t0) * 1000,
    'load_orders_ms' => ($t2 - $t1) * 1000,
    'render_ms' => ($t3 - $t2) * 1000,
]));
```

Now you know where time is spent.

## 41.3 Database performance checks

Investigate:

- number of queries
- duplicate queries
- N+1 query patterns
- missing indexes
- large scans
- unbounded result sets
- locks
- slow joins
- sorting large datasets

## 41.4 Do not optimize guesses

Measure first.

---

# 42. Profiling, Tracing, and Code Coverage

These tools solve different problems.

| Technique | Main question |
|---|---|
| Step debugging | What is happening line by line? |
| Logging | What happened during real execution? |
| Tracing | Which functions were called, in what order? |
| Profiling | Where is execution time/resources being spent? |
| Code coverage | Which code did tests execute? |
| Static analysis | What likely bugs can be found without running code? |

## 42.1 Xdebug tracing

Tracing can help understand complex call flow.

Conceptually:

```text
Controller
→ Service
→ Repository
→ Mapper
→ Validator
→ ...
```

A trace records function activity so you can see how execution traveled.

## 42.2 Profiling

Profiling answers questions such as:

```text
Why is this request 4 seconds?
Which function uses most time?
Which function is called 20,000 times?
```

Profiling can add overhead.

Enable it intentionally during diagnosis rather than permanently on a busy production server.

## 42.3 Code coverage

Coverage answers:

```text
Which lines/branches did my tests execute?
```

Coverage does **not** prove that tested code is correct.

100% line coverage can still contain logic bugs.

---

# 43. Debugging PHP-FPM, Apache, and Nginx

PHP may be correct while the server integration is not.

## 43.1 Common PHP-FPM symptoms

```text
502 Bad Gateway
504 Gateway Timeout
File not found
Connection refused
upstream timed out
```

Investigate:

- FPM service status
- socket/port
- pool configuration
- worker availability
- permissions
- PHP error log
- web server upstream config

## 43.2 Useful Linux service checks

Examples vary by distribution/version, but commonly:

```bash
systemctl status php-fpm
```

or a versioned service name.

Inspect logs:

```bash
journalctl -u php-fpm
```

Use the actual service name on your system.

## 43.3 Nginx + PHP-FPM path mistakes

The request may reach PHP-FPM with an incorrect script filename.

Symptoms can look like:

```text
File not found
Primary script unknown
```

Inspect:

```text
root
fastcgi_pass
fastcgi_param SCRIPT_FILENAME
location matching
```

## 43.4 Apache logs

Inspect:

- Apache error log
- access log
- PHP error log

The exact path depends on your operating system and configuration.

## 43.5 A key rule

When the browser only shows:

```text
500
502
504
```

do not debug by staring at the browser.

Open the server logs.

---

# 44. Debugging Dockerized PHP

Containers introduce another environment layer.

Your architecture may look like:

```text
Host machine
├── nginx container
├── php-fpm container
└── mysql container
```

## 44.1 Check containers

```bash
docker ps
```

## 44.2 Inspect logs

```bash
docker logs <container-name>
```

Follow:

```bash
docker logs -f <container-name>
```

## 44.3 Run command inside PHP container

```bash
docker exec -it <php-container> php -v
```

Check extensions:

```bash
docker exec -it <php-container> php -m
```

Now you are checking the PHP installation that actually runs in the container.

## 44.4 Xdebug inside Docker

Common problem:

```text
Xdebug is in container
IDE is on host
```

Therefore:

```ini
xdebug.client_host=127.0.0.1
```

may point to the **container itself**, not your IDE host.

You must configure networking appropriate to:

- Docker Desktop
- Linux Docker
- WSL
- remote Docker host

Also configure IDE path mappings.

## 44.5 File mismatch

If your host source differs from code copied into an image, you may set breakpoints in one version while PHP runs another.

Verify the exact file in the container.

---

# 45. Debugging Queues, Cron Jobs, and Background Commands

Background processes often fail silently because there is no browser response.

## 45.1 Always capture logs

For cron:

```text
command output
stderr
exit status
application log
```

## 45.2 Cron environment is different

A command that works interactively may fail under cron because of:

- different `PATH`
- different working directory
- missing environment variables
- different user
- different permissions
- different PHP executable

Use absolute paths where appropriate.

Instead of relying on:

```text
php script.php
```

the actual scheduled command may need the intended PHP executable and full script path.

## 45.3 Log job context

```php
error_log(json_encode([
    'job' => 'invoice-import',
    'file' => $fileName,
    'started_at' => date(DATE_ATOM),
]));
```

Include a run/job ID for correlation.

## 45.4 Idempotency matters

If a job crashes halfway and reruns, can it duplicate:

- payments?
- invoices?
- emails?
- database rows?

A debugging fix must consider retry behavior.

---

# 46. Debugging Production Safely

Production debugging has a different goal:

```text
Get enough evidence
without exposing users
or destabilizing the system
```

## 46.1 Never enable public raw error display casually

Avoid production:

```ini
display_errors = On
```

Prefer:

```ini
display_errors = Off
log_errors = On
```

## 46.2 Use structured application logs

Log useful context such as:

```text
timestamp
severity
request_id
user_id or account_id
route
operation
safe business identifier
exception class
safe error message
stack trace
duration
```

## 46.3 Mask sensitive values

Example:

```php
function maskEmail(string $email): string
{
    [$name, $domain] = explode('@', $email, 2);

    return substr($name, 0, 1) . '***@' . $domain;
}
```

The exact masking strategy depends on your security requirements.

## 46.4 Reproduce outside production

Once evidence is captured:

```text
Production symptom
→ isolate input/state
→ reproduce in staging/local
→ debug deeply there
→ create fix
→ test
→ deploy safely
```

## 46.5 Add temporary logging carefully

Temporary production logs should be:

- narrowly scoped
- safe
- rate-limited if needed
- removed after investigation

Do not dump entire request/session/database records into logs.

---

# 47. Framework Debugging Notes

Frameworks provide their own debugging layers.

The exact locations and commands can vary by framework version, so always check the documentation for the version used by your project.

---

## 47.1 Laravel

Common debugging tools/concepts include:

```text
application logs
exception handler
debug configuration
dump()/dd()
request validation errors
database query inspection
Artisan CLI
Laravel Telescope for supported projects
```

Development:

```php
dump($value);
```

or:

```php
dd($value);
```

`dd()` means effectively:

```text
dump
+
stop execution
```

Do not leave `dd()` calls in production code paths.

Production should not expose detailed debug pages.

---

## 47.2 Symfony

Common debugging facilities include:

```text
Profiler
Web Debug Toolbar
logs
exception pages in development
console commands
dependency container diagnostics
```

The profiler is particularly useful for inspecting:

- request
- response
- routing
- database queries
- events
- cache
- timing

---

## 47.3 CodeIgniter 3

Common areas to investigate:

```text
ENVIRONMENT
application/config
application/logs
database configuration
routing
controllers/models
PHP/server logs
```

Debugging questions:

```text
Is the expected environment active?
Is logging enabled at the needed level?
Is the controller method reached?
Does the model return expected data?
Does the view receive the expected variables?
```

---

## 47.4 CodeIgniter 4

Common debugging areas include:

```text
environment configuration
writable/logs
debug toolbar in development
exceptions
routes
filters
database layer
CLI commands
```

Do not assume a CodeIgniter 3 debugging solution applies unchanged to CodeIgniter 4; their architecture is significantly different.

---

# 48. Testing as a Debugging Tool

A good regression test turns a discovered bug into a permanent guardrail.

Suppose this bug exists:

```php
function calculateDiscount(float $amount): float
{
    if ($amount > 1000) {
        return 100;
    }

    return 0;
}
```

Requirement:

```text
Exactly 1000 should also receive discount.
```

A test exposes it:

```php
public function testExactly1000GetsDiscount(): void
{
    $this->assertSame(
        100.0,
        calculateDiscount(1000.0)
    );
}
```

Fix:

```php
if ($amount >= 1000) {
```

Now the test prevents regression.

## 48.1 Debugging with a minimal failing test

Instead of repeatedly testing through the entire browser workflow, create a focused test:

```text
Given X
When Y
Then Z should happen
```

This makes debugging faster and repeatable.

## 48.2 Types of tests

```text
Unit test
→ one small unit/function/class

Integration test
→ multiple components together

Database integration test
→ code + real/test database behavior

HTTP/feature test
→ route/request → response behavior

End-to-end test
→ full user workflow
```

Choose the smallest test that reliably reproduces the bug.

---

# 49. Static Analysis and Automated Bug Detection

Debugging does not have to begin after runtime failure.

Static analysis examines code without executing the failing production path and can catch many defects earlier.

Popular PHP tools include:

- PHPStan
- Psalm
- IDE language analysis
- PHP's own syntax check
- framework-specific analyzers

They can identify problems such as:

```text
possibly null value
incorrect argument type
undefined method
impossible condition
incorrect return type
invalid property access
unreachable code
inconsistent array shapes
```

## 49.1 Example: nullable return

```php
function findUser(int $id): ?User
{
    // ...
}

$user = findUser(10);

echo $user->name;
```

A static analyzer can warn that `$user` may be `null`.

Correct code depends on the domain:

```php
$user = findUser(10);

if ($user === null) {
    throw new RuntimeException('User not found');
}

echo $user->name;
```

## 49.2 PHP syntax check

Before deeper debugging, verify syntax:

```bash
php -l path/to/file.php
```

For an entire project, run the command through your build/CI process rather than checking files manually one by one.

## 49.3 PHPStan setup

Install as a development dependency:

```bash
composer require --dev phpstan/phpstan
```

Analyze application and tests:

```bash
vendor/bin/phpstan analyse src tests
```

A basic `phpstan.neon` can centralize configuration:

```neon
parameters:
    level: 6
    paths:
        - src
        - tests
```

Start at a realistic level for an existing project and increase strictness as findings are fixed.

Do not immediately generate a huge ignore list just to make CI green. Every ignored issue becomes hidden debugging debt.

## 49.4 Static analysis is not runtime truth

Static analysis cannot prove that:

- the database is reachable,
- an external API returns the documented payload,
- filesystem permissions are correct,
- session storage is healthy,
- a race condition never occurs.

Combine:

```text
static analysis
+ tests
+ runtime logging
+ debugger
+ integration checks
```

## 49.5 CI usage

A practical quality gate can run:

```text
composer validate
PHP syntax checks
static analysis
unit/integration tests
security/dependency checks
```

Run the same commands locally when possible so CI failures are reproducible.

---
# 50. Common PHP Bugs: Symptoms, Causes, and Fixes

## 50.1 Blank white page

Possible causes:

- error display disabled
- fatal error
- output intentionally empty
- server configuration issue

Check:

```text
PHP log
web server log
FPM log
application log
```

Development-only:

```php
error_reporting(E_ALL);
ini_set('display_errors', '1');
```

---

## 50.2 `Undefined variable`

Problem:

```php
echo $total;
```

before `$total` is defined.

Fix the control flow:

```php
$total = 0;
```

or ensure every required branch assigns it.

Do not hide the warning with `@`.

---

## 50.3 `Undefined array key`

Problem:

```php
$email = $_POST['email'];
```

Fix:

```php
$email = $_POST['email'] ?? null;
```

Then validate why it may be missing.

---

## 50.4 `Trying to access array offset on value of type null`

Problem:

```php
$user = findUser($id);

echo $user['name'];
```

If no user exists, `$user` may be null.

Fix:

```php
if ($user === null) {
    // handle missing user
}
```

---

## 50.5 `Call to a member function ... on null`

Problem:

```php
$user->profile->save();
```

One object is null.

Use a breakpoint or staged checks:

```php
var_dump($user);
var_dump($user?->profile);
```

Then fix the missing-state logic.

---

## 50.6 `Class ... not found`

Check:

```text
namespace
use statement
filename/case
Composer autoload
vendor directory
autoload configuration
container build
deployment artifact
```

Try:

```bash
composer dump-autoload
```

---

## 50.7 `Failed opening required ...`

Inspect:

```php
var_dump(__DIR__);
var_dump($path);
var_dump(file_exists($path));
```

Prefer absolute/anchored paths.

---

## 50.8 `Headers already sent`

Search for output before:

```php
header()
setcookie()
session_start()
```

Use:

```php
headers_sent($file, $line);
```

---

## 50.9 `Maximum execution time exceeded`

Possible causes:

- infinite loop
- slow query
- API timeout
- huge file operation
- deadlock/locking wait
- inefficient algorithm

Measure components before simply increasing timeout.

---

## 50.10 `Allowed memory size exhausted`

Investigate object/array/file growth before raising memory.

Use:

```php
memory_get_usage(true);
memory_get_peak_usage(true);
```

---

## 50.11 `SQLSTATE...`

Read the complete error.

It may indicate:

- authentication failure
- connection failure
- duplicate key
- constraint failure
- syntax problem
- missing table/column
- deadlock
- invalid data type

Do not expose raw SQL errors to public users.

---

## 50.12 `could not find driver`

Check the PHP instance handling the request.

```bash
php -m
```

is only relevant to CLI PHP.

For the web request, verify PHP-FPM/Apache extension configuration too.

---

## 50.13 Works locally but not server

Compare:

```text
PHP version
extensions
php.ini
environment variables
filesystem case sensitivity
permissions
database version/config
web server config
timezone
locale
dependency lockfile/install
cache
container image
```

Differences are evidence.

---

# 51. Real-World Debugging Scenarios

## 51.1 Scenario 1: API Returns HTTP 500 After Saving an Invoice

### Symptom

Frontend receives:

```text
500 Internal Server Error
```

### Bad debugging approach

```php
echo 'here 1';
echo 'here 2';
echo 'here 3';
```

This may corrupt JSON responses.

### Better process

Add structured logs:

```php
error_log(json_encode([
    'event' => 'invoice_update_start',
    'invoice_id' => $invoiceId,
]));

$invoice = $repo->find($invoiceId);

error_log(json_encode([
    'event' => 'invoice_loaded',
    'found' => $invoice !== null,
]));

$service->approve($invoice);

error_log(json_encode([
    'event' => 'invoice_approved',
]));
```

Suppose the logs end after:

```text
invoice_loaded
```

Now set a breakpoint inside:

```php
$service->approve($invoice);
```

You discover:

```php
$invoice->vendor
```

is null.

Root cause:

```text
invoice data existed
but associated vendor had been deleted/not mapped
```

Fix the actual invariant, not merely the HTTP status.

---

## 51.2 Scenario 2: `json_decode()` Returns `null`

### Code

```php
$data = json_decode($response, true);
```

### Problem

Developer assumes:

```text
null means API returned null
```

But invalid JSON can also be involved when not using throwing mode.

### Better

```php
try {
    $data = json_decode(
        $response,
        true,
        512,
        JSON_THROW_ON_ERROR
    );
} catch (JsonException $e) {
    error_log('Invalid API JSON: ' . $e->getMessage());
}
```

Now malformed JSON becomes explicit.

---

## 51.3 Scenario 3: SQL Returns No Rows but Row Exists

Query:

```sql
SELECT *
FROM invoices
WHERE invoice_no = :invoice_no
  AND location_id = :location_id
  AND company_id = :company_id
```

Debug inputs:

```php
error_log(var_export([
    'invoice_no' => $invoiceNo,
    'location_id' => $locationId,
    'company_id' => $companyId,
], true));
```

You discover:

```text
location_id expected: 9
location_id actual: "9 "
```

The visible UI looked correct.

Debugging the exact runtime value revealed whitespace.

---

## 51.4 Scenario 4: Form Field Is Always Missing

HTML:

```html
<input id="vendor" type="text">
```

PHP:

```php
$_POST['vendor']
```

is missing.

Why?

The input has no:

```html
name="vendor"
```

Correct:

```html
<input id="vendor" name="vendor" type="text">
```

---

## 51.5 Scenario 5: Xdebug Does Not Stop at Breakpoints

Checklist:

```text
1. Is Xdebug loaded?
2. Is `xdebug.mode=debug` active?
3. Is the IDE listening?
4. Is port 9003 consistent?
5. Does Xdebug start for this request?
6. Is `client_host` correct?
7. If Docker/remote, are path mappings correct?
8. Is PHP executing the same file you opened?
9. Did you restart FPM/Apache after config change?
10. Does `xdebug_info()` show connection/config diagnostics?
```

The problem is often configuration, not the breakpoint itself.

---

## 51.6 Scenario 6: CLI Works but Browser Fails

CLI:

```bash
php script.php
```

works.

Browser:

```text
could not find driver
```

Debug:

```bash
php --ini
php -m
```

Then check web `phpinfo()` locally/staging.

Result:

```text
CLI uses PHP A with pdo_mysql
FPM uses PHP B without pdo_mysql
```

Root cause found.

---

## 51.7 Scenario 7: User Is Logged Out Randomly

Investigate:

```text
session cookie
session ID changes
load balancer
session storage
cookie domain
HTTPS
SameSite
session lifetime
deployment/restart
```

Add safe logs:

```php
error_log(json_encode([
    'event' => 'auth_check',
    'user_id' => $_SESSION['user_id'] ?? null,
    'session_has_user' => isset($_SESSION['user_id']),
]));
```

Do not log the actual session identifier unless there is a justified, protected diagnostic process.

---

## 51.8 Scenario 8: Import Dies After 20,000 Rows

Add progress diagnostics:

```php
foreach ($rows as $index => $row) {
    if ($index % 1000 === 0) {
        error_log(json_encode([
            'row' => $index,
            'memory_mb' =>
                round(memory_get_usage(true) / 1048576, 2),
        ]));
    }

    processRow($row);
}
```

If memory grows:

```text
50 MB
90 MB
150 MB
300 MB
...
```

you now have evidence of accumulated memory.

Investigate:

- retained arrays
- buffered query results
- ORM entity manager/unit of work
- unclosed resources
- large per-row data

---

## 51.9 Scenario 9: Redirect Does Nothing

Code:

```php
echo 'Saved';

header('Location: success.php');
```

Check:

```php
if (headers_sent($file, $line)) {
    var_dump($file, $line);
}
```

Fix output order:

```php
header('Location: success.php');
exit;
```

---

## 51.10 Scenario 10: `foreach` Crashes Only for Some Records

Code:

```php
foreach ($invoice['items'] as $item) {
    // ...
}
```

Some invoice has:

```php
'invoice' => [
    'items' => null,
]
```

Debug contract:

```php
if (!isset($invoice['items']) || !is_array($invoice['items'])) {
    throw new UnexpectedValueException(
        'Invoice items must be an array'
    );
}
```

Fix the upstream data model or validation rather than silently converting every invalid state to an empty array unless that is truly the business rule.

---

# 52. A Professional Debugging Workflow

Use this procedure for serious bugs.

## Step 1 — State expected behavior

Example:

```text
Approving invoice 1001 should update status from Pending to Approved.
```

## Step 2 — State actual behavior

```text
The API returns HTTP 500 and status remains Pending.
```

## Step 3 — Reproduce consistently

Document exact:

```text
user
route
input
record
environment
timestamp
```

## Step 4 — Capture the first real error

Inspect:

```text
application log
PHP log
web server log
browser Network
exception trace
```

## Step 5 — Locate the failing layer

```text
HTTP?
routing?
controller?
service?
database?
filesystem?
external API?
configuration?
```

## Step 6 — Build hypotheses

Example:

```text
H1: invoice is null
H2: vendor relationship is null
H3: SQL update fails
H4: authorization rejects action
```

## Step 7 — Test hypotheses

Breakpoint:

```php
$invoice = $repo->find($id);
```

Inspect.

Then next boundary.

## Step 8 — Find root cause

Do not stop at:

```text
"variable was null"
```

Ask:

```text
Why was it null?
```

Maybe:

```text
migration allowed invalid data
import missed vendor mapping
repository used wrong filter
test fixture was incomplete
```

## Step 9 — Fix at the right layer

If database data violates an invariant, adding:

```php
if ($vendor === null) {
    return;
}
```

may hide corruption.

The correct fix might involve:

- validation
- database constraint
- migration
- import correction
- domain rule
- better exception

## Step 10 — Add regression test

Reproduce the failing condition in a test.

## Step 11 — Remove temporary diagnostics

Remove:

```php
var_dump();
print_r();
die();
dd();
temporary debug routes
temporary verbose production logs
```

## Step 12 — Verify surrounding behavior

Test:

```text
happy path
failure path
boundary values
permissions
empty values
large values
retry behavior
```

---

# 53. Debugging Anti-Patterns

## 53.1 Suppressing errors with `@`

Example:

```php
$content = @file_get_contents($path);
```

This hides useful information.

Prefer explicit failure handling.

```php
$content = file_get_contents($path);

if ($content === false) {
    throw new RuntimeException(
        "Unable to read file: $path"
    );
}
```

## 53.2 Catching and ignoring everything

Bad:

```php
try {
    processPayment();
} catch (Throwable $e) {
}
```

The program now fails silently.

At minimum:

```php
catch (Throwable $e) {
    error_log((string) $e);

    throw $e;
}
```

if the current layer cannot recover.

## 53.3 Random `echo` debugging in APIs

```php
echo 'test';
```

can break:

- JSON
- file downloads
- headers
- redirects

Prefer logging or a step debugger.

## 53.4 Changing production data while investigating

Do not repeatedly "test" by altering important production rows manually unless there is a controlled recovery procedure.

Use:

- safe read-only diagnostics
- staging reproductions
- transactions where appropriate
- backups
- audit trails

## 53.5 Fixing the symptom only

Symptom:

```text
Undefined array key "email"
```

Superficial fix:

```php
$email = $data['email'] ?? '';
```

But if email is required, the correct fix is probably:

```text
validate required input
reject invalid payload
fix producer contract
```

## 53.6 Leaving debug mode enabled

Verbose debug systems can expose internal data and add overhead.

Development and production configurations should be intentionally different.

---

# 54. Debugging Best Practices

1. **Reproduce before editing.**
2. **Capture the exact error message.**
3. **Read the full stack trace.**
4. **Verify runtime values, not assumptions.**
5. **Check types as well as values.**
6. **Use logs for server-side evidence.**
7. **Use breakpoints for complex control flow.**
8. **Use request IDs to correlate distributed logs.**
9. **Do not expose secrets in logs or debug pages.**
10. **Keep production error display off.**
11. **Measure performance before optimizing.**
12. **Create the smallest reliable reproducer.**
13. **Compare environment configuration when behavior differs.**
14. **Write a regression test for meaningful bugs.**
15. **Remove temporary debugging code after diagnosis.**
16. **Fix causes, not only symptoms.**
17. **Use strict types/comparisons where appropriate.**
18. **Validate external input at boundaries.**
19. **Prefer explicit exceptions for exceptional failures.**
20. **Centralize observability instead of scattering ad-hoc output.**

---

# 55. Debugging Checklists

## 55.1 Generic PHP bug checklist

- [ ] Can I reproduce the bug?
- [ ] What should happen?
- [ ] What actually happens?
- [ ] What is the exact error?
- [ ] What file and line fail?
- [ ] What does the stack trace show?
- [ ] What input triggered it?
- [ ] What are the runtime types?
- [ ] Which PHP version is running?
- [ ] Which `php.ini` is loaded?
- [ ] Are required extensions loaded?
- [ ] Is this CLI, FPM, Apache, or container PHP?
- [ ] What do application logs show?
- [ ] What do server logs show?
- [ ] Is database/API/filesystem involved?
- [ ] Can I isolate the failing layer?
- [ ] Can I reproduce it with a smaller example?
- [ ] Does the fix address root cause?
- [ ] Did I add a regression test?
- [ ] Did I remove temporary debugging code?

## 55.2 HTTP 500 checklist

- [ ] Browser Network response inspected
- [ ] PHP error log checked
- [ ] application log checked
- [ ] web server log checked
- [ ] FPM log checked
- [ ] recent deployment/change reviewed
- [ ] exception stack trace identified
- [ ] database connectivity checked
- [ ] file permissions checked
- [ ] environment/config values checked
- [ ] memory/timeout issues considered

## 55.3 Database checklist

- [ ] connection works
- [ ] correct database selected
- [ ] correct user/permissions
- [ ] exact SQL known
- [ ] exact parameter values known
- [ ] parameter types known
- [ ] prepared statement used
- [ ] row existence verified
- [ ] NULL logic checked
- [ ] joins tested progressively
- [ ] transaction state checked
- [ ] constraints checked
- [ ] slow query/index issue checked when relevant

## 55.4 Xdebug checklist

- [ ] Xdebug installed
- [ ] correct PHP SAPI has Xdebug
- [ ] `xdebug.mode=debug`
- [ ] debugger start mode correct
- [ ] IDE is listening
- [ ] client host correct
- [ ] client port is 9003 unless intentionally customized
- [ ] firewall/network allows connection
- [ ] Docker/remote mapping correct
- [ ] source file matches executed source
- [ ] PHP service restarted after configuration changes

## 55.5 Production checklist

- [ ] `display_errors` off
- [ ] logging enabled
- [ ] sensitive values masked
- [ ] request/correlation ID available
- [ ] exact deployment version known
- [ ] issue timestamp known
- [ ] impact/scope known
- [ ] safe reproduction attempted
- [ ] temporary logging narrowly scoped
- [ ] rollback strategy understood
- [ ] regression test prepared before final deployment when practical

---

# 56. PHP Debugging Cheat Sheet

## Environment

```bash
php -v
php --ini
php -m
php -i
php --ri xdebug
```

## Syntax check

```bash
php -l file.php
```

## Maximum development error reporting

```php
error_reporting(E_ALL);
ini_set('display_errors', '1');
```

## Inspect value and type

```php
var_dump($value);
```

## Human-readable array/object

```php
print_r($value);
```

## Export as string

```php
error_log(var_export($value, true));
```

## Log

```php
error_log('message');
```

## JSON-safe exception behavior

```php
$data = json_decode(
    $json,
    true,
    512,
    JSON_THROW_ON_ERROR
);
```

## Catch anything throwable at a boundary

```php
try {
    run();
} catch (Throwable $e) {
    error_log((string) $e);
}
```

## Debug current stack

```php
debug_print_backtrace();
```

or:

```php
$trace = debug_backtrace();
```

## Check a file path

```php
var_dump([
    'path' => $path,
    'exists' => file_exists($path),
    'readable' => is_readable($path),
]);
```

## Check headers

```php
if (headers_sent($file, $line)) {
    var_dump($file, $line);
}
```

## Memory

```php
memory_get_usage(true);
memory_get_peak_usage(true);
```

## Timing

```php
$start = microtime(true);

// operation

$seconds = microtime(true) - $start;
```

## PDO exception mode

```php
$pdo = new PDO(
    $dsn,
    $user,
    $pass,
    [
        PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
    ]
);
```

## MySQLi strict reporting

```php
mysqli_report(
    MYSQLI_REPORT_ERROR |
    MYSQLI_REPORT_STRICT
);
```

## Xdebug 3 baseline

```ini
xdebug.mode=develop,debug
xdebug.start_with_request=trigger
xdebug.client_port=9003
```

---

# 57. Recommended Learning Exercises

## Exercise 1 — Undefined variable

Create:

```php
<?php

echo $username;
```

Tasks:

1. Run it.
2. Read the diagnostic.
3. Enable `E_ALL` if needed.
4. Fix the real cause.

---

## Exercise 2 — Wrong type

```php
<?php

declare(strict_types=1);

function multiply(int $a, int $b): int
{
    return $a * $b;
}

multiply('hello', 10);
```

Tasks:

1. Identify exception type.
2. Read file/line.
3. Inspect stack.
4. Catch `TypeError`.
5. Fix the input.

---

## Exercise 3 — Invalid JSON

```php
$json = '{"name":"Asha",}';
```

Decode it with:

```php
JSON_THROW_ON_ERROR
```

Catch and log `JsonException`.

---

## Exercise 4 — Missing array key

```php
$user = ['name' => 'Asha'];

echo $user['email'];
```

Fix it in two ways:

1. optional email
2. required email

Notice that these require different business logic.

---

## Exercise 5 — Database bug

Create a PDO query that requests a nonexistent column.

Observe:

- exception class
- SQLSTATE
- stack trace

Then replace public output with safe logging.

---

## Exercise 6 — Xdebug

Write:

```php
function calculate(int $a, int $b): int
{
    $result = $a * $b;
    return $result;
}

echo calculate(10, 20);
```

Set a breakpoint on:

```php
$result = $a * $b;
```

Practice:

- Continue
- Step Over
- Step Into
- Step Out
- Watch `$a`
- Watch `$result`
- inspect call stack

---

## Exercise 7 — Performance

Create:

```php
for ($i = 0; $i < 1000000; $i++) {
    $value = sqrt($i);
}
```

Measure it with:

```php
microtime(true)
```

Then compare different implementations.

---

## Exercise 8 — Build a mini error pipeline

Create a small application containing:

```text
custom error handler
global exception handler
request ID
structured log
JSON error response
```

Trigger:

- validation exception
- TypeError
- invalid JSON
- database failure

Observe how each is reported.

---

# 58. Official References

For version-sensitive behavior, verify against the documentation for the PHP/Xdebug versions installed in your environment.

## PHP Manual

- PHP documentation: https://www.php.net/manual/en/
- Error handling: https://www.php.net/manual/en/book.errorfunc.php
- Runtime error configuration: https://www.php.net/manual/en/errorfunc.configuration.php
- `error_reporting()`: https://www.php.net/manual/en/function.error-reporting.php
- `set_error_handler()`: https://www.php.net/manual/en/function.set-error-handler.php
- `set_exception_handler()`: https://www.php.net/manual/en/function.set-exception-handler.php
- Exceptions: https://www.php.net/manual/en/language.exceptions.php
- PDO: https://www.php.net/manual/en/book.pdo.php
- PDO error handling: https://www.php.net/manual/en/pdo.error-handling.php
- MySQLi: https://www.php.net/manual/en/book.mysqli.php

## Xdebug

- Xdebug documentation: https://xdebug.org/docs/
- Step debugging: https://xdebug.org/docs/step_debug
- Configuration settings: https://xdebug.org/docs/all_settings
- Xdebug 2 → 3 migration guide: https://xdebug.org/docs/upgrade_guide

---

# Final Mental Model

When something breaks, remember:

```text
Do not guess.
Observe.

Do not hide the error.
Capture it safely.

Do not inspect only the symptom.
Follow the stack and data flow.

Do not change everything.
Test one hypothesis at a time.

Do not stop at "what failed?"
Ask "why could this state exist?"

Do not finish when the page works.
Add a test so the same bug stays fixed.
```

A strong PHP debugger can answer five questions quickly:

```text
1. What exactly failed?
2. Where exactly did it fail?
3. What values and types existed at that moment?
4. Why did execution reach that invalid state?
5. How can we prevent the same state in the future?
```

That is the difference between randomly fixing code and systematically debugging software.

---

# Appendix A — Recommended PHP Debugging Tools and Configuration

This appendix provides a practical setup for local, container, and production debugging.

## A.1 Recommended starter toolchain

```text
PHP CLI
+ Composer
+ VS Code or PhpStorm
+ Xdebug
+ PHPUnit/framework tests
+ PHPStan
+ Git
```

Add application monitoring and profiling when you begin operating production services.

## A.2 Verify the PHP runtime first

Before configuring any debugger:

```bash
php -v
php --ini
php -m
```

On Windows:

```bat
where php
```

On Linux/macOS:

```bash
which php
```

Remember that CLI PHP and web-server PHP may load different executables and different `php.ini` files.

For web/FPM debugging, verify the SAPI-specific configuration rather than assuming CLI output proves the web runtime is identical.

## A.3 Install and verify Xdebug

Installation varies by operating system and PHP build, so use Xdebug's official installation guidance for the exact PHP version/architecture.

After installation:

```bash
php --ri xdebug
```

or:

```bash
php -v
```

The output should show that Xdebug is loaded.

## A.4 Recommended Xdebug step-debug settings

A practical development configuration is:

```ini
zend_extension=xdebug

xdebug.mode=develop,debug
xdebug.start_with_request=trigger
xdebug.client_host=127.0.0.1
xdebug.client_port=9003
```

Why trigger mode?

```text
normal request
→ no debugger connection attempt

request with XDEBUG_TRIGGER
→ Xdebug tries to connect to IDE
```

This avoids starting step debugging for every request.

For a dedicated local debugging environment, you may temporarily use:

```ini
xdebug.start_with_request=yes
```

but trigger-based activation is often less noisy.

Restart PHP-FPM, Apache, or the relevant runtime after changing configuration.

## A.5 Xdebug connection diagnostics

Temporarily configure an Xdebug log when the debugger will not connect:

```ini
xdebug.log=/tmp/xdebug.log
xdebug.log_level=7
```

Choose a writable path for your operating system/container.

Inspect the log for:

```text
which host Xdebug tried
which port it used
whether the connection succeeded
```

Disable or reduce verbose diagnostic logging after the problem is solved.

## A.6 VS Code

VS Code supports PHP step debugging through the **PHP Debug** extension.

Create `.vscode/launch.json`:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Listen for Xdebug",
      "type": "php",
      "request": "launch",
      "port": 9003
    }
  ]
}
```

Workflow:

```text
1. Start "Listen for Xdebug"
2. Set breakpoint
3. Send request with debugging trigger
4. Xdebug connects to port 9003
5. VS Code pauses at breakpoint
```

## A.7 Docker path mapping

Suppose PHP sees:

```text
/var/www/html
```

but your editor workspace is the local project folder.

A VS Code configuration may need:

```json
{
  "name": "Listen for Xdebug in Docker",
  "type": "php",
  "request": "launch",
  "port": 9003,
  "pathMappings": {
    "/var/www/html": "${workspaceFolder}"
  }
}
```

If Xdebug connects but breakpoints are unverified, path mapping is one of the first things to check.

## A.8 Docker `client_host`

Inside a container, `127.0.0.1` refers to the container itself, not automatically to your host editor.

The correct `xdebug.client_host` depends on your container platform/network.

Use the host-reachable name/IP supported by your environment and verify it from inside the container.

Do not copy one platform's special hostname into every Linux server and assume it will work.

## A.9 PhpStorm

PhpStorm includes PHP debugging support.

Typical setup:

1. Configure the PHP interpreter.
2. Configure Xdebug in the PHP runtime.
3. Make sure the IDE is listening for PHP debug connections.
4. Configure server/path mappings for Docker or remote files.
5. Set a breakpoint.
6. Trigger the request.

The same network rule applies: Xdebug initiates a connection to the configured debugging client.

## A.10 PHPUnit/framework test debugging

A failing test is one of the best reproducible debugging entry points.

Run a focused test:

```bash
vendor/bin/phpunit --filter testMethodName
```

Then run the same test through your IDE debugger.

For framework projects, use the framework's supported test command when it adds environment/bootstrap behavior.

## A.11 PHPStan

Install:

```bash
composer require --dev phpstan/phpstan
```

Run:

```bash
vendor/bin/phpstan analyse src tests
```

Example configuration:

```neon
parameters:
    level: 6
    paths:
        - src
        - tests
```

Increase strictness gradually.

A static-analysis failure is not something to suppress automatically; first understand whether it reveals a real contract/type bug.

## A.12 Composer diagnostics

Useful dependency/configuration commands include:

```bash
composer validate
composer diagnose
composer show
composer show --outdated
composer audit
```

Use these when a failure may involve:

- malformed project metadata,
- dependency resolution,
- platform requirements,
- missing extensions,
- security advisories.

Always inspect the exact Composer error before deleting lock files or reinstalling the whole dependency tree.

## A.13 Web-server and PHP-FPM tools

When the browser shows a generic `500`, correlate all relevant logs:

```text
application log
PHP error log
PHP-FPM log
Apache/Nginx error log
reverse proxy/load balancer log
```

Useful Linux commands depend on service names, for example:

```bash
systemctl status php-fpm
journalctl -u php-fpm
```

Distribution/package names differ, so use the actual service unit on your machine.

## A.14 Profiling

Xdebug includes profiling support for development analysis.

Enable only when needed:

```ini
xdebug.mode=profile
xdebug.start_with_request=trigger
```

Then trigger the profiling request and analyze the generated profiler output with a compatible visualization tool.

Do not leave heavy profiling enabled for every production request.

For production performance diagnosis, prefer tools designed for controlled low-overhead observability/profiling and validate their impact first.

## A.15 Browser and HTTP tools

Many PHP bugs are really request/response bugs.

Use browser DevTools Network panel to inspect:

```text
method
URL
status
request headers
request payload/form data
response headers
response body
timing
cookies
```

For command-line reproduction:

```bash
curl -i https://example.test/api/orders/123
```

Add only the headers/body required for the failing case and never paste live secrets into bug reports.

## A.16 Database tools

For PDO/MySQLi bugs, capture:

```text
SQL template
bound parameter names
sanitized parameter values
parameter types
selected database/schema
transaction state
exact exception/error
```

Then reproduce the SQL safely in a database client when appropriate.

Use `EXPLAIN`/execution-plan tools for query-performance problems rather than guessing which index is missing.

## A.17 Production-safe configuration

A typical production philosophy is:

```ini
display_errors=Off
log_errors=On
error_reporting=E_ALL
```

Application frameworks may add their own exception/error handling.

Never turn on a public debug toolbar, raw stack trace page, `phpinfo()`, or Xdebug step listener as a quick permanent production fix.

## A.18 Recommended VS Code additions

For PHP debugging work, useful extension categories are:

- PHP Debug/Xdebug integration,
- PHP language analysis,
- Composer support,
- test integration,
- static-analysis integration.

Install only maintained extensions from publishers you trust. Avoid stacking several competing PHP language servers because duplicate diagnostics and indexing can make debugging harder.

## A.19 Official references

- PHP manual: <https://www.php.net/manual/>
- Xdebug step debugging: <https://xdebug.org/docs/step_debug>
- Xdebug settings: <https://xdebug.org/docs/all_settings>
- Xdebug installation: <https://xdebug.org/docs/install>
- VS Code PHP guide: <https://code.visualstudio.com/docs/languages/php>
- PHPStan getting started: <https://phpstan.org/user-guide/getting-started>
- PHPStan configuration: <https://phpstan.org/config-reference>

---
