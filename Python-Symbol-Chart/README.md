# Python Symbol Chart

## Purpose

This is a quick-reference chart for Python symbols, operators, Boolean logic, comparisons, containers, and common syntax.

The goal is not to memorize every symbol.

The goal is to be able to look at Python code and quickly answer:

```text
What does this symbol mean?

What job is it doing here?
```

---

# Arithmetic Operators

| Symbol | Name | What It Does | Example | Result |
|---|---|---|---|---|
| `+` | Addition | Adds values | `5 + 3` | `8` |
| `-` | Subtraction | Subtracts values | `5 - 3` | `2` |
| `*` | Multiplication | Multiplies values | `5 * 3` | `15` |
| `/` | Division | Divides and returns a decimal | `5 / 2` | `2.5` |
| `//` | Floor division | Divides and removes the decimal remainder | `5 // 2` | `2` |
| `%` | Modulo | Returns the remainder | `5 % 2` | `1` |
| `**` | Exponent | Raises a number to a power | `5 ** 2` | `25` |

---

# `%` — Modulo

```python
75 % 23
```

means:

```text
How many complete groups of 23 fit into 75?

23 × 3 = 69

75 - 69 = 6
```

Result:

```text
6
```

Mental model:

```text
Modulo
=
What is left over?
```

---

# `**` — Exponent

```python
7 ** 3
```

means:

```text
7³
```

or:

```text
7 × 7 × 7
```

Result:

```text
343
```

Do not confuse:

```python
7 * 3
```

with:

```python
7 ** 3
```

They mean:

```text
*  = multiplication

** = exponentiation
```

---

# Assignment

| Symbol | Meaning | Example |
|---|---|---|
| `=` | Assign a value | `x = 5` |
| `+=` | Add then assign | `x += 1` |
| `-=` | Subtract then assign | `x -= 1` |
| `*=` | Multiply then assign | `x *= 2` |
| `/=` | Divide then assign | `x /= 2` |
| `//=` | Floor divide then assign | `x //= 2` |
| `%=` | Modulo then assign | `x %= 2` |
| `**=` | Raise to power then assign | `x **= 2` |

---

# `=` vs `==`

This is one of the most important distinctions.

```python
x = 5
```

means:

```text
Put the value 5 inside x.
```

But:

```python
x == 5
```

means:

```text
Is x equal to 5?
```

So:

```text
=
Assignment

==
Comparison
```

---

# Comparison Operators

Comparison operators produce:

```text
True
```

or:

```text
False
```

| Symbol | Meaning | Example |
|---|---|---|
| `==` | Equal to | `x == 5` |
| `!=` | Not equal to | `x != 5` |
| `>` | Greater than | `x > 5` |
| `<` | Less than | `x < 5` |
| `>=` | Greater than or equal to | `x >= 5` |
| `<=` | Less than or equal to | `x <= 5` |

---

# Boolean Values

Python Boolean values are:

```python
True
False
```

They represent:

```text
Yes / No

On / Off

Condition passed / Condition failed
```

---

# Boolean Operators

| Operator | Meaning | Rule |
|---|---|---|
| `and` | AND | Every joined condition must be true |
| `or` | OR | At least one joined condition must be true |
| `not` | NOT | Reverses True/False |

---

# `and`

```python
age >= 18 and has_id == True
```

Both conditions must be true.

Mental model:

```text
Condition A
   AND
Condition B

Both doors must open.
```

Truth chart:

| A | B | `A and B` |
|---|---|---|
| True | True | True |
| True | False | False |
| False | True | False |
| False | False | False |

Important:

```text
The Boolean operator that requires EVERY condition it joins to be true is:

and
```

It is NOT:

```text
==
```

`==` only compares two values.

---

# `or`

```python
is_admin or is_owner
```

Only one condition needs to be true.

```text
Condition A
    OR
Condition B

Either door can open.
```

Truth chart:

| A | B | `A or B` |
|---|---|---|
| True | True | True |
| True | False | True |
| False | True | True |
| False | False | False |

---

# `not`

```python
not logged_in
```

reverses the Boolean value.

```text
True  → False

False → True
```

Example:

```python
logged_in = False

if not logged_in:
    print("Please log in")
```

---

# Membership Operators

| Operator | Meaning |
|---|---|
| `in` | Value exists inside something |
| `not in` | Value does not exist inside something |

Example:

```python
"admin" in users
```

asks:

```text
Does "admin" exist inside users?
```

---

# Identity Operators

| Operator | Meaning |
|---|---|
| `is` | Same object |
| `is not` | Not the same object |

Example:

```python
x is None
```

A common use is checking for:

```python
None
```

Do not automatically treat:

```text
is
```

as another spelling of:

```text
==
```

They test different things.

---

# Parentheses `()`

Parentheses are used for several jobs.

## Function calls

```python
print("Hello")
```

## Grouping calculations

```python
(5 + 3) * 2
```

## Function definitions

```python
def greet(name):
```

Mental model:

```text
()
=
Inputs / grouping / function interaction
```

---

# Square Brackets `[]`

Commonly used for:

```text
Lists

Indexes

Slices
```

Example list:

```python
users = ["Tony", "Alex", "Sam"]
```

Access first item:

```python
users[0]
```

Result:

```text
Tony
```

Python indexing normally starts at:

```text
0
```

---

# Curly Braces `{}`

Curly braces commonly create:

```text
Dictionaries

Sets
```

Dictionary:

```python
user = {
    "name": "Tony",
    "role": "admin"
}
```

Set:

```python
numbers = {1, 2, 3}
```

---

# Colon `:`

The colon commonly starts an indented block.

Example:

```python
if x == 5:
    print("Yes")
```

Also used in:

```text
Functions

Loops

Dictionaries

Slices
```

Examples:

```python
def test():
```

```python
for item in items:
```

```python
"name": "Tony"
```

```python
items[1:4]
```

---

# Comma `,`

Separates values.

Example:

```python
print("Tony", 32)
```

List:

```python
[1, 2, 3]
```

Function:

```python
def add(x, y):
```

---

# Dot `.`

The dot accesses something belonging to an object or module.

Example:

```python
hashlib.md5()
```

Think:

```text
hashlib
   ↓
contains/accesses
   ↓
md5
```

Another example:

```python
text.lower()
```

---

# Quotes

Strings can use:

```python
"Hello"
```

or:

```python
'Hello'
```

The quotes tell Python:

```text
Treat this as text.
```

Without quotes:

```python
hello
```

Python interprets it as a name such as a variable.

---

# Comments `#`

```python
# This is a comment
```

Python ignores the comment during normal execution.

Use comments to explain:

```text
Why code exists

What a section does

Important assumptions
```

---

# Backslash `\`

A backslash is commonly used as an escape character inside strings.

Example:

```python
print("Tony\nAtlas")
```

`\n` means:

```text
New line
```

Common escapes:

| Sequence | Meaning |
|---|---|
| `\n` | New line |
| `\t` | Tab |
| `\\` | Literal backslash |
| `\"` | Literal double quote |
| `\'` | Literal single quote |

---

# Underscore `_`

The underscore is valid inside variable and function names.

Example:

```python
user_name
```

```python
password_hash
```

Python naming commonly uses:

```text
snake_case
```

---

# If / Elif / Else

```python
if condition:
    ...
elif other_condition:
    ...
else:
    ...
```

Mental model:

```text
IF this is true
    ↓
Do this

ELSE IF something else is true
    ↓
Do that

ELSE
    ↓
Do fallback
```

---

# `for`

Used to iterate through items.

```python
for password in passwords:
    print(password)
```

Mental model:

```text
For every item in this collection:

Do something.
```

---

# `while`

Repeats while a condition remains:

```text
True
```

Example:

```python
while x < 10:
    x += 1
```

Important:

```python
while True:
```

creates a loop whose condition never naturally becomes false.

Unless something such as:

```python
break
```

stops it, it can continue indefinitely.

---

# `break`

Stops the current loop.

```python
while True:
    if found:
        break
```

---

# `continue`

Skips the rest of the current loop iteration and starts the next one.

---

# `return`

Sends a result back from a function.

```python
def add(x, y):
    return x + y
```

---

# Common Built-In Functions

| Function | Job |
|---|---|
| `print()` | Display output |
| `input()` | Get user input |
| `int()` | Convert to integer |
| `str()` | Convert to string |
| `float()` | Convert to decimal number |
| `len()` | Get length/count |
| `type()` | Show data type |
| `range()` | Generate a numeric range |
| `bool()` | Convert to Boolean |

---

# Fast Recognition Chart

| You See | Think |
|---|---|
| `=` | Assign |
| `==` | Compare equality |
| `!=` | Not equal |
| `and` | ALL conditions |
| `or` | ANY condition |
| `not` | Reverse Boolean |
| `%` | Remainder |
| `**` | Power |
| `()` | Function/grouping |
| `[]` | List/index |
| `{}` | Dictionary/set |
| `:` | Start block / key-value separator |
| `.` | Access method/member |
| `#` | Comment |
| `in` | Membership |
| `True` / `False` | Boolean |

---

# Engineering Takeaway

Do not read Python as a wall of symbols.

Break it into jobs:

```text
Values
   ↓
Operators
   ↓
Conditions
   ↓
Decisions
   ↓
Actions
```

Example:

```python
if age >= 18 and has_id:
    allow_entry()
```

Read it as:

```text
INPUT

age
has_id

        ↓

DECISION

age must be at least 18
AND
has_id must be true

        ↓

OUTPUT

allow_entry()
```

The symbols are just a compact language for expressing the logic.
