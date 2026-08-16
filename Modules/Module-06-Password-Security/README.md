# Module 06 — Password Security

## Hashing

A hash function takes input data and produces a fixed-length output called a hash.

```text
password
   ↓
hash function
   ↓
hash value
```

A normal hash function does not require a secret key.

Hashes are designed to be one-way. Instead of decrypting a password hash, password-cracking tools generate candidate passwords, hash them, and compare the results.

---

## Salts

A salt is random data added to a password before hashing.

```text
password + salt
       ↓
   hash function
       ↓
   stored hash
```

The salt does **not** need to be secret.

Its purpose is to make identical passwords produce different hashes and make precomputed attacks such as rainbow tables less effective.

---

## Dictionary Attack vs Brute Force

### Dictionary Attack

Tests likely passwords from a predefined wordlist.

Example:

```text
password
dragon
football
letmein
...
```

Tools may use wordlists such as:

```text
rockyou.txt
```

### Brute-Force Attack

Systematically generates possible character combinations.

Example:

```text
a
b
c
...
aa
ab
ac
...
```

The major difference:

> A dictionary attack tries likely passwords, while brute force systematically attempts possible combinations.

---

## John the Ripper

John the Ripper is a password-hash cracking tool.

General workflow:

```text
Hash
  ↓
Identify hash format
  ↓
Choose wordlist / attack mode
  ↓
John hashes candidate passwords
  ↓
Compare against target hash
  ↓
Matching candidate = recovered password
```

For an NT hash / NTLM password hash, John's format name is:

```text
NT
```

---

## Windows Password Hashes

Windows stores local account information in the:

```text
SAM
```

SAM stands for:

```text
Security Account Manager
```

It contains local user account information, including password hashes.

Windows commonly uses NT hashes for local account passwords.

Important distinction:

```text
SAM  = database/location containing account information and hashes
NT   = hash format
John = tool capable of testing candidate passwords against hashes
```

---

## Key Takeaways

- Hashing is not encryption.
- Normal hash functions do not require a secret key.
- Salts do not need to remain secret.
- Salts make precomputed attacks less effective.
- Dictionary attacks use likely-password lists.
- Brute force systematically generates possible combinations.
- John the Ripper tests candidate passwords against hashes.
- John's NTLM/NT hash format is `NT`.
- Windows local account password hashes are stored in the SAM.
