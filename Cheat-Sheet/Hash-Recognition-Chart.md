# Hash Recognition Chart

## Purpose

This chart is for recognizing common hash and password-storage formats during authorized labs, password auditing, and cryptography exercises.

Important rule:

```text
Length is a clue.

Prefix is a clue.

Context is a clue.

None of them alone always prove the algorithm.
```

Some formats are visually ambiguous.

---

# Quick Recognition Chart

| Type | Visual Clue | Typical Length / Prefix | Hashcat Mode | Common John Format |
|---|---|---|---:|---|
| MD5 | Hex only | 32 hex characters | `0` | `Raw-MD5` |
| NTLM | Hex only | 32 hex characters | `1000` | `NT` |
| LM | Hex only | commonly 32 hex characters | `3000` | `LM` |
| SHA-1 | Hex only | 40 hex characters | `100` | `Raw-SHA1` |
| SHA-224 | Hex only | 56 hex characters | `1300` | `Raw-SHA224` |
| SHA-256 | Hex only | 64 hex characters | `1400` | `Raw-SHA256` |
| SHA-384 | Hex only | 96 hex characters | `10800` | `Raw-SHA384` |
| SHA-512 | Hex only | 128 hex characters | `1700` | `Raw-SHA512` |
| SHA3-512 | Hex only | 128 hex characters | `17600` | `Raw-SHA3` |
| Whirlpool | Hex only | 128 hex characters | `6100` | verify build with `--list=formats` |
| md5crypt | Modular crypt string | starts `$1$` | `500` | `crypt-md5` / build-dependent alias |
| sha256crypt | Modular crypt string | starts `$5$` | `7400` | SHA256crypt / crypt-sha256 build label |
| sha512crypt | Modular crypt string | starts `$6$` | `1800` | SHA512crypt / crypt-sha512 build label |
| bcrypt | Modular string | `$2a$`, `$2b$`, `$2y$` | `3200` | `bcrypt` |
| PBKDF2-HMAC-SHA256 | Structured salted string | often contains `sha256:` or product-specific marker | `10900` for generic Hashcat format | `pbkdf2-hmac-sha256` |
| Argon2 | Structured string | `$argon2id$`, `$argon2i$`, etc. | `34000` for Hashcat Argon2 support | `argon2` / verify build |
| Kerberos etype 23 AS-REQ | Structured | `$krb5pa$23$...` | `7500` | Kerberos-specific format |
| Kerberos etype 23 TGS-REP | Structured | `$krb5tgs$23$...` | `13100` | `krb5tgs` |
| Kerberos etype 23 AS-REP | Structured | `$krb5asrep$23$...` | `18200` | `krb5asrep` |

---

# Raw Hex Length Recognition

## 32 Hex Characters

Example shape:

```text
8743b52063cd84097a65d1633f5c74f5
```

Possible types include:

```text
MD5

NTLM

LM-related encodings

Other 128-bit values
```

Therefore:

```text
32 hex characters
DOES NOT automatically mean MD5.
```

Context matters.

---

# MD5 vs NTLM Collision Problem

Both commonly appear as:

```text
32 hexadecimal characters
```

Example shape:

```text
8846f7eaee8fb117ad06bdd830b7586c
```

Looking at the string alone may not tell you whether it is:

```text
MD5

or

NTLM
```

Ask:

```text
Where did the hash come from?
```

If it came from:

```text
Windows SAM
```

NTLM is far more likely.

If it came from:

```text
A web application storing a raw digest
```

MD5 may be possible.

---

# John Ambiguity Warning

John the Ripper may recognize one string as multiple possible formats.

That is expected.

Example concept:

```text
32 hex characters
      ↓
Could match several algorithms
      ↓
John warns about ambiguity
```

Do not blindly select the first detected format.

Use:

```text
Source context

Prefix

Application

Operating system

Expected algorithm
```

to determine the correct type.

---

# MD5

Visual shape:

```text
32 hex characters
```

Example structure:

```text
098f6bcd4621d373cade4e832627b4f6
```

Hashcat:

```text
-m 0
```

John common format:

```text
--format=Raw-MD5
```

But remember:

```text
32 hex ≠ guaranteed MD5
```

---

# NTLM

NTLM password hashes are based on MD4 processing of the password in Microsoft's expected encoding.

Recognition:

```text
32 hex characters
```

Hashcat:

```text
-m 1000
```

John:

```text
--format=NT
```

Strong contextual clue:

```text
Windows local-account hash
```

---

# Windows SAM Connection

Local Windows account password hashes are associated with the:

```text
Security Account Manager
```

or:

```text
SAM
```

So:

```text
Windows SAM
    ↓
Local account
    ↓
NTLM hash context
```

This context is more useful than simply counting characters.

---

# SHA-1

Recognition:

```text
40 hexadecimal characters
```

Hashcat:

```text
-m 100
```

John:

```text
--format=Raw-SHA1
```

---

# SHA-224

Recognition:

```text
56 hexadecimal characters
```

Hashcat:

```text
-m 1300
```

John:

```text
--format=Raw-SHA224
```

---

# SHA-256

Recognition:

```text
64 hexadecimal characters
```

Hashcat:

```text
-m 1400
```

John:

```text
--format=Raw-SHA256
```

---

# SHA-384

Recognition:

```text
96 hexadecimal characters
```

Hashcat:

```text
-m 10800
```

John:

```text
--format=Raw-SHA384
```

---

# SHA-512

Recognition:

```text
128 hexadecimal characters
```

Hashcat:

```text
-m 1700
```

John:

```text
--format=Raw-SHA512
```

Important:

```text
128 hex characters
```

is NOT enough to prove SHA-512.

Other 512-bit hashes can have the same visual length.

---

# SHA3-512

Recognition:

```text
128 hexadecimal characters
```

Hashcat:

```text
-m 17600
```

John:

```text
--format=Raw-SHA3
```

Collision clue:

```text
SHA-512
SHA3-512
Whirlpool
```

can all produce:

```text
128 hexadecimal characters
```

So length alone cannot distinguish them.

---

# Whirlpool

Whirlpool produces a:

```text
512-bit digest
```

which is commonly displayed as:

```text
128 hexadecimal characters
```

Hashcat:

```text
-m 6100
```

Again:

```text
128 hex
```

could visually resemble:

```text
SHA-512

SHA3-512

Whirlpool
```

Use context.

---

# Unix Modular-Crypt Formats

These formats are easier to recognize because they contain prefixes.

Mental model:

```text
Prefix
 ↓
Algorithm family clue
```

---

# md5crypt

Starts with:

```text
$1$
```

Example shape:

```text
$1$salt$hash
```

Hashcat:

```text
-m 500
```

John's exact current format label can depend on build/version.

Current Jumbo documentation uses full labels such as:

```text
crypt-md5
```

When unsure:

```bash
john --list=formats
```

---

# sha256crypt

Starts with:

```text
$5$
```

Example:

```text
$5$rounds=5000$salt$hash
```

Hashcat:

```text
-m 7400
```

Recognition shortcut:

```text
$5$
 ↓
sha256crypt
```

---

# sha512crypt

Starts with:

```text
$6$
```

Example:

```text
$6$salt$hash
```

Hashcat:

```text
-m 1800
```

Recognition shortcut:

```text
$6$
 ↓
sha512crypt
```

---

# bcrypt

Common prefixes:

```text
$2a$

$2b$

$2y$
```

Example shape:

```text
$2b$12$...
```

The number such as:

```text
12
```

represents the bcrypt cost factor.

Hashcat:

```text
-m 3200
```

John:

```text
--format=bcrypt
```

Recognition:

```text
$2...
 ↓
Think bcrypt
```

---

# PBKDF2-HMAC-SHA256

PBKDF2 is not simply:

```text
a raw SHA-256 hash
```

It includes repeated key-derivation work and a salt.

Generic Hashcat representation can resemble:

```text
sha256:1000:<salt>:<derived-key>
```

Hashcat generic mode:

```text
-m 10900
```

John Jumbo commonly exposes:

```text
pbkdf2-hmac-sha256
```

Important:

Different applications may store PBKDF2-HMAC-SHA256 in different textual formats.

Therefore:

```text
Application format matters.
```

---

# Argon2

Common prefixes include:

```text
$argon2id$

$argon2i$

$argon2d$
```

Example structure:

```text
$argon2id$v=19$m=65536,t=3,p=1$...
```

The string includes parameters such as:

```text
Version

Memory cost

Time cost

Parallelism

Salt

Result
```

Hashcat supports Argon2 formats, including an Argon2 mode:

```text
34000
```

Recognition is normally much easier than a raw digest because:

```text
$argon2...
```

identifies the family.

---

# Kerberos

Kerberos material has highly recognizable structured prefixes.

Examples:

```text
$krb5pa$23$
```

```text
$krb5tgs$23$
```

```text
$krb5asrep$23$
```

These are not interchangeable.

---

# Kerberos AS-REQ Pre-Auth

Prefix:

```text
$krb5pa$23$
```

Hashcat:

```text
-m 7500
```

Think:

```text
Kerberos 5

etype 23

AS-REQ pre-authentication
```

---

# Kerberos TGS-REP

Prefix:

```text
$krb5tgs$23$
```

Hashcat:

```text
-m 13100
```

John:

```text
krb5tgs
```

---

# Kerberos AS-REP

Prefix:

```text
$krb5asrep$23$
```

Hashcat:

```text
-m 18200
```

John:

```text
krb5asrep
```

---

# Prefix Recognition Chart

| Prefix | Think |
|---|---|
| `$1$` | md5crypt |
| `$2a$` / `$2b$` / `$2y$` | bcrypt |
| `$5$` | sha256crypt |
| `$6$` | sha512crypt |
| `$argon2id$` | Argon2id |
| `$argon2i$` | Argon2i |
| `$krb5pa$` | Kerberos pre-auth |
| `$krb5tgs$` | Kerberos TGS |
| `$krb5asrep$` | Kerberos AS-REP |

---

# Raw Digest Length Chart

| Hex Length | Possible Recognition |
|---:|---|
| 32 | MD5, NTLM, LM-related or other 128-bit values |
| 40 | SHA-1 and other 160-bit values |
| 56 | SHA-224 |
| 64 | SHA-256 and other 256-bit values |
| 96 | SHA-384 |
| 128 | SHA-512, SHA3-512, Whirlpool, other 512-bit values |

Important:

```text
Possible recognition
≠
Guaranteed identification
```

---

# Hexadecimal Reminder

Hexadecimal uses:

```text
0 1 2 3 4 5 6 7 8 9

A B C D E F
```

Each hexadecimal character represents:

```text
4 bits
```

Therefore:

```text
32 hex characters × 4 bits = 128 bits

40 × 4 = 160 bits

64 × 4 = 256 bits

128 × 4 = 512 bits
```

This explains why digest lengths appear the way they do.

---

# Hash vs Encoding

Do not assume every strange-looking string is a hash.

Example:

```text
Base64
```

is an:

```text
encoding
```

not a cryptographic hash.

Base64 data may contain:

```text
A-Z

a-z

0-9

+

/

=
```

and can normally be decoded back into the original bytes.

A cryptographic hash is designed as a one-way digest.

---

# Hash vs Encryption

```text
Hashing
```

and:

```text
Encryption
```

are different.

Hashing:

```text
Input
 ↓
Digest
```

There is normally no decryption key.

Encryption:

```text
Plaintext
 ↓
Key + algorithm
 ↓
Ciphertext
```

and authorized holders of the required key can decrypt it.

---

# Dictionary vs Brute Force

These are attack strategies, not hash types.

Dictionary attack:

```text
Try likely candidate passwords
```

Brute force:

```text
Systematically try combinations
```

The hash algorithm remains:

```text
the thing candidates are being tested against.
```

---

# Recognition Workflow

Do not start with:

```text
"It's 32 characters, so it's MD5."
```

Use:

```text
1. Look for a prefix

2. Check overall structure

3. Count characters if it is raw hex

4. Identify where the value came from

5. Consider the operating system/application

6. Let John/Hashcat validate the format

7. Treat ambiguous recognition as ambiguous until evidence resolves it
```

---

# Tool Verification

## John the Ripper

List formats available in the installed build:

```bash
john --list=formats
```

Filter for a likely family:

```bash
john --list=formats | grep -i sha
```

Force a known format:

```bash
john --format=<FORMAT> hashes.txt
```

John may warn that an encoding matches multiple formats.

That warning is useful evidence.

---

# Hashcat

Hashcat requires the correct hash mode.

Structure:

```bash
hashcat -m <MODE> <HASH_FILE> <WORDLIST>
```

Examples of mode numbers in this chart refer to the specific formats listed.

Do not assume:

```text
same digest length
=
same Hashcat mode
```

---

# Key Ambiguities

## 32 Hex

Could be:

```text
MD5

NTLM

LM-related

Other 128-bit data
```

---

## 64 Hex

Could be:

```text
SHA-256

or another 256-bit value
```

---

## 128 Hex

Could be:

```text
SHA-512

SHA3-512

Whirlpool

Other 512-bit values
```

---

# Context Beats Appearance

Example:

```text
32 hex characters
```

plus:

```text
Extracted from Windows SAM
```

strongly points toward:

```text
NTLM
```

The same visual string found in:

```text
a custom web application's old database
```

might instead be:

```text
MD5
```

So:

```text
Shape
+
Source
+
Context
=
Better identification
```

---

# Explicit Exclusions

This chart is NOT intended to contain every Hashcat or John format.

Those tools support hundreds of formats.

This reference focuses on formats relevant to the concepts and labs covered so far, including:

```text
Raw MD5

Windows NTLM / LM recognition

SHA family

SHA3-512

Whirlpool

Unix crypt formats

bcrypt

PBKDF2-HMAC-SHA256

Argon2

Kerberos formats
```

Not included unless they become relevant later:

```text
Database-specific proprietary formats

Cryptocurrency wallet formats

Encrypted archive formats

Office/PDF extraction formats

Router/vendor-specific password formats

Every nested or salted variant of MD5/SHA

Every Kerberos encryption type

Every PBKDF2 application-specific encoding
```

When one of those becomes part of an actual lab or project, add it then instead of bloating the chart with formats that have not been used.

---

# Fast Mental Model

```text
Prefix present?
    ↓
Use prefix first

No prefix?
    ↓
Check structure and length

Looks ambiguous?
    ↓
Use source/context

Still ambiguous?
    ↓
Let tools identify candidates
but verify the result
```

---

# Engineering Takeaway

A hash should be treated like evidence.

Do not force an identity onto it just because it resembles something familiar.

Use:

```text
Observation
   ↓
Possible types
   ↓
Context
   ↓
Tool validation
   ↓
Conclusion
```

Recognition is:

```text
pattern matching
+
context
+
verification
```

not:

```text
guessing from length alone.
```
