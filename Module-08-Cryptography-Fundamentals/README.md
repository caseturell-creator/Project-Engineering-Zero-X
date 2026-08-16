# Modular Arithmetic and Exponents

## Overview

Modular arithmetic is mathematics focused on:

```text
Remainders
```

Instead of only asking:

```text
How many times does one number go into another?
```

modular arithmetic asks:

```text
What is left over?
```

This becomes extremely important in:

- Cryptography
- Computer science
- Public-key encryption
- Number theory
- Programming

---

# The Core Idea

Example:

```text
17 ÷ 5
```

Five fits into seventeen:

```text
3 times
```

because:

```text
5 × 3 = 15
```

Then:

```text
17 - 15 = 2
```

So:

```text
17 mod 5 = 2
```

The answer we care about is:

```text
2
```

because that is the remainder.

---

# My Manual Mental Model

The way I naturally worked these problems out was:

```text
Big number
    ↓
How many FULL times does the divisor fit?
    ↓
Multiply
    ↓
Subtract
    ↓
What is left?
    ↓
Remainder
```

That remainder is the modulo result.

---

# Division vs Modulo

Division asks:

```text
How many times does it fit?
```

Modulo asks:

```text
What is left over?
```

Example:

```text
How many times does 23 go into 75?
```

23 fits:

```text
3 times
```

because:

```text
23 × 3 = 69
```

Then:

```text
75 - 69 = 6
```

Therefore:

```text
75 ÷ 23 = 3 remainder 6
```

and:

```text
75 mod 23 = 6
```

---

# Quotient and Remainder

Integer division can be represented as:

```text
Dividend = Divisor × Quotient + Remainder
```

Example:

```text
75 = 23 × 3 + 6
```

Where:

```text
75 = Dividend

23 = Divisor

3 = Quotient

6 = Remainder
```

---

# The Modulo Operator

Mathematically:

```text
75 mod 23 = 6
```

Programming languages commonly use:

```text
%
```

So in Python:

```python
75 % 23
```

returns:

```text
6
```

The `%` symbol is therefore asking:

```text
What is the remainder?
```

---

# Remainder Range

When calculating:

```text
x mod 29
```

the possible remainder must be:

```text
0 through 28
```

The remainder cannot be:

```text
29
```

because another complete group of 29 could still be removed.

Generally:

```text
0 ≤ remainder < modulus
```

---

# Clock Analogy

A clock is a simple example of modular arithmetic.

A clock has:

```text
12 positions
```

After 12, it wraps back around.

Suppose it is:

```text
10 o'clock
```

and five hours pass.

Normal arithmetic:

```text
10 + 5 = 15
```

But on a clock:

```text
15 mod 12 = 3
```

So the time is:

```text
3 o'clock
```

Modulo creates a number system that wraps around.

---

# Circular Number System

Normal counting:

```text
0
1
2
3
4
5
6
7
8
...
```

Modulo 5 behaves like:

```text
0
1
2
3
4
0
1
2
3
4
0
...
```

Conceptually:

```text
0 → 1 → 2 → 3 → 4
↑                 ↓
└─────────────────┘
```

Complete laps do not matter.

Only the final position matters.

---

# Same Spot Mental Model

Consider:

```text
2
7
12
17
22
```

All of them produce:

```text
2
```

when divided modulo 5.

```text
2 mod 5 = 2

7 mod 5 = 2

12 mod 5 = 2

17 mod 5 = 2

22 mod 5 = 2
```

They are different numbers normally.

But modulo 5, they all land on the:

```text
same spot
```

---

# Congruence

Modular arithmetic often uses:

```text
≡
```

which means:

```text
Congruent to
```

Example:

```text
17 ≡ 2 mod 5
```

because:

```text
17 mod 5 = 2
```

---

# Bucket Analogy

Another useful way to think about modulo:

Imagine buckets that each hold exactly:

```text
29 objects
```

If you have a massive pile, every completely full bucket can be ignored.

Example:

```text
Millions of objects
      ↓
Fill bucket after bucket of 29
      ↓
Ignore all complete buckets
      ↓
Count objects in final unfinished bucket
```

That final bucket is:

```text
The remainder
```

So:

```text
x mod 29
```

means:

```text
How many objects are left
after creating every complete group of 29?
```

---

# Why Huge Numbers Become Manageable

Consider:

```text
762939453125 mod 29
```

The original number is huge.

But modulo does not care about the gigantic quotient.

It only cares about:

```text
What remains after removing
every complete group of 29?
```

So conceptually:

```text
Huge number
    ↓
Remove complete groups
    ↓
Small remainder
```

---

# Exponents

An exponent represents repeated multiplication.

Example:

```text
7³
```

means:

```text
7 × 7 × 7
```

which equals:

```text
343
```

---

# Base and Exponent

In:

```text
7³
```

the:

```text
7
```

is the:

```text
Base
```

and:

```text
3
```

is the:

```text
Exponent
```

---

# Powers Grow Quickly

Example:

```text
5¹ = 5

5² = 25

5³ = 125

5⁴ = 625

5⁵ = 3125
```

Increasing the exponent causes numbers to grow extremely quickly.

---

# Large Powers

Something like:

```text
7¹⁷
```

means multiplying:

```text
7
```

by itself:

```text
17 times
```

The result is:

```text
232630513987207
```

This is where modular arithmetic becomes extremely useful.

---

# Modular Exponentiation

Instead of caring about the entire result of:

```text
7¹⁷
```

we may only care about:

```text
7¹⁷ mod 29
```

Meaning:

```text
Raise 7 to the 17th power
        ↓
Divide by 29
        ↓
Keep only the remainder
```

This is called:

```text
Modular Exponentiation
```

---

# Why This Matters

Cryptographic systems often work with powers so large that calculating and storing the full number would be inefficient.

Modulo lets us repeatedly shrink the number back down.

Conceptually:

```text
Multiply
   ↓
Number grows
   ↓
Modulo
   ↓
Number becomes small again
   ↓
Continue
```

---

# Reduce as You Go

We do not always need to calculate the giant number first.

Example:

```text
7² = 49
```

Now reduce:

```text
49 mod 29 = 20
```

Therefore:

```text
7² ≡ 20 mod 29
```

For modular calculations, we can often continue working with:

```text
20
```

instead of carrying:

```text
49
```

forward.

---

# Repeated Squaring

Large modular powers can be calculated efficiently using:

```text
Repeated squaring
```

Suppose we want:

```text
7¹⁷ mod 29
```

Instead of multiplying 7 seventeen times, build:

```text
7¹

7²

7⁴

7⁸

7¹⁶
```

Each new power is created by squaring the previous one.

---

# Example: 7¹⁷ mod 29

Start:

```text
7¹ mod 29 = 7
```

Square:

```text
7² = 49
```

Reduce:

```text
49 mod 29 = 20
```

Therefore:

```text
7² ≡ 20 mod 29
```

---

Square again:

```text
20² = 400
```

Now divide by 29:

```text
29 × 13 = 377
```

Subtract:

```text
400 - 377 = 23
```

Therefore:

```text
7⁴ ≡ 23 mod 29
```

---

Square again:

```text
23² = 529
```

29 fits into 529:

```text
18 times
```

because:

```text
29 × 18 = 522
```

Then:

```text
529 - 522 = 7
```

Therefore:

```text
7⁸ ≡ 7 mod 29
```

---

Square again:

```text
7² = 49
```

Reduce:

```text
49 mod 29 = 20
```

Therefore:

```text
7¹⁶ ≡ 20 mod 29
```

---

Now:

```text
17 = 16 + 1
```

So:

```text
7¹⁷
=
7¹⁶ × 7¹
```

Use the reduced values:

```text
20 × 7 = 140
```

29 fits into 140:

```text
4 times
```

because:

```text
29 × 4 = 116
```

Subtract:

```text
140 - 116 = 24
```

Therefore:

```text
7¹⁷ mod 29 = 24
```

---

# Why We Keep Reducing

We could have calculated:

```text
232630513987207
```

and then divided that enormous number by 29.

But that would be unnecessary.

Instead:

```text
7
 ↓
Square
 ↓
Reduce
 ↓
Square
 ↓
Reduce
 ↓
Square
 ↓
Reduce
```

We keep the intermediate numbers small.

This is the key idea behind efficient modular exponentiation.

---

# Addition With Modulo

Example:

```text
18 + 11 = 29
```

Then:

```text
29 mod 7 = 1
```

Therefore:

```text
(18 + 11) mod 7 = 1
```

---

# Multiplication With Modulo

Example:

```text
8 × 9 = 72
```

Then:

```text
72 mod 7 = 2
```

Therefore:

```text
(8 × 9) mod 7 = 2
```

---

# Reduce Before Multiplication

Suppose:

```text
123 × 456 mod 7
```

Instead of multiplying first:

```text
123 mod 7 = 4
```

and:

```text
456 mod 7 = 1
```

Now:

```text
4 × 1 = 4
```

Therefore:

```text
123 × 456 mod 7 = 4
```

Reducing early prevents numbers from growing unnecessarily.

---

# Python Exponents

Python uses:

```python
**
```

for exponentiation.

Example:

```python
7 ** 3
```

returns:

```text
343
```

---

# Multiplication vs Exponentiation

These are different:

```python
7 * 3
```

means:

```text
21
```

while:

```python
7 ** 3
```

means:

```text
343
```

Mental model:

```text
*
=
Multiply two values

**
=
Raise to a power
```

---

# Python Modulo

Python uses:

```python
%
```

Example:

```python
75 % 23
```

returns:

```text
6
```

---

# Python Modular Exponentiation

Python provides:

```python
pow()
```

For example:

```python
pow(7, 17, 29)
```

means:

```text
7¹⁷ mod 29
```

and returns:

```text
24
```

---

# Two Ways to Calculate It

This works:

```python
(7 ** 17) % 29
```

But Python can perform modular exponentiation more efficiently with:

```python
pow(7, 17, 29)
```

This becomes much more important when the exponent is enormous.

---

# Why Tools Are Still Important

The point is not to manually divide gigantic numbers forever.

The progression is:

```text
Understand the math manually
        ↓
Understand what the operator means
        ↓
Use the computer to automate it
        ↓
Interpret the result correctly
```

The computer handles repetitive arithmetic.

The engineer understands what the result means.

---

# Input → Process → Output

Modulo can be modeled as:

```text
INPUT

Number
Modulus

        ↓

PROCESS

Remove every complete group
of the modulus

        ↓

OUTPUT

Remainder
```

Example:

```text
INPUT

75
23

        ↓

PROCESS

23 × 3 = 69

75 - 69 = 6

        ↓

OUTPUT

6
```

---

# Modular Exponentiation Model

```text
INPUT

Base
Exponent
Modulus

        ↓

PROCESS

Repeated multiplication

+

Repeated modulo reduction

        ↓

OUTPUT

Final remainder
```

This is why gigantic powers can still produce manageable results.

---

# Cryptography Connection

Modular arithmetic is heavily used in public-key cryptography.

Important systems include:

```text
RSA

Diffie-Hellman
```

These systems rely on mathematical operations involving:

```text
Large numbers

Exponents

Prime numbers

Modulo operations
```

---

# Diffie-Hellman Connection

A simplified Diffie-Hellman-style calculation has the form:

```text
g^a mod p
```

Where:

```text
g = base

a = secret exponent

p = modulus
```

This is modular exponentiation.

---

# RSA Connection

RSA also uses modular exponentiation.

The structure includes calculations similar to:

```text
message^exponent mod n
```

The full RSA system contains additional mathematics, but the underlying operation uses the same concepts:

```text
Exponent
+
Modulo
```

---

# Why Cryptography Likes This Math

Some mathematical operations are easy to calculate forward but extremely difficult to reverse when extremely large numbers are involved.

This allows cryptographic systems to create relationships where:

```text
Certain information can be public
```

while:

```text
Secret information remains difficult to recover.
```

Large modular arithmetic is one of the foundations that makes this possible.

---

# Even and Odd Numbers

Modulo also has simple everyday uses.

Example:

```text
8 mod 2 = 0
```

So:

```text
8 is even
```

But:

```text
9 mod 2 = 1
```

So:

```text
9 is odd
```

Python:

```python
number % 2 == 0
```

tests whether a number is even.

---

# Divisibility

If:

```text
a mod b = 0
```

then:

```text
a is evenly divisible by b
```

Example:

```text
30 mod 5 = 0
```

Therefore:

```text
30 is divisible by 5
```

---

# Common Mistake: Division vs Modulo

```python
75 / 23
```

asks:

```text
What is the division result?
```

while:

```python
75 % 23
```

asks:

```text
What is the remainder?
```

These are different questions.

---

# Common Mistake: Remainder Equal to the Modulus

Example:

```text
29 mod 29
```

The answer is:

```text
0
```

not:

```text
29
```

because one complete group of 29 can be removed.

---

# Common Mistake: Remainder Too Large

If calculating:

```text
x mod 29
```

and you get:

```text
35
```

you are not finished.

Because:

```text
35 - 29 = 6
```

So the correct reduced remainder is:

```text
6
```

---

# Common Mistake: Calculating Giant Powers First

For something like:

```text
7^1000000 mod 29
```

it makes no sense to manually construct:

```text
7^1000000
```

first.

Instead:

```text
Multiply
 ↓
Reduce
 ↓
Multiply
 ↓
Reduce
```

The modulo operation keeps the calculation manageable.

---

# Engineering Mental Model

Modulo is not just:

```text
A weird math symbol.
```

It represents a very simple process:

```text
Create complete groups
        ↓
Ignore those complete groups
        ↓
Keep what is left
```

Then modular exponentiation adds:

```text
Repeated multiplication
```

while repeatedly shrinking the result back down.

So:

```text
Huge mathematical space
        ↓
Modulo
        ↓
Small repeating space
```

---

# Fast Recognition

If you see:

```text
%
```

think:

```text
Remainder
```

If you see:

```text
**
```

think:

```text
Exponent
```

If you see:

```text
mod
```

think:

```text
Complete groups disappear.
Keep what remains.
```

If you see:

```text
g^a mod p
```

think:

```text
Modular exponentiation
```

---

# Python Quick Reference

Modulo:

```python
75 % 23
```

Exponent:

```python
7 ** 17
```

Modular exponent:

```python
pow(7, 17, 29)
```

Even number:

```python
number % 2 == 0
```

Odd number:

```python
number % 2 != 0
```

---

# Key Takeaway

```text
Division
=
How many times does it fit?

Modulo
=
What is left over?

Exponent
=
Repeated multiplication

Modular Exponentiation
=
Repeated multiplication
while repeatedly reducing
to the remainder
```

My simplest mental model:

```text
Modulo = buckets.

Every full bucket can be ignored.

Only the unfinished bucket matters.
```

And when huge powers appear:

```text
Do not carry the whole mountain.

Keep reducing the number
to the remainder you actually need.
```
