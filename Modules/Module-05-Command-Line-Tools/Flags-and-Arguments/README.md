# Flags and Arguments

## Overview

After selecting a program and a subcommand, you often need to provide additional information.

This is done using **flags (options)** and **arguments**.

Understanding the difference between these two concepts is essential because almost every command-line tool uses them.

---

# What Is a Flag?

A **flag** (also called an **option**) changes or controls how a command behaves.

Flags usually begin with one or two hyphens.

Examples:

```bash
-u
-v
-h
-w
--help
--url
--wordlist
```

Flags **do not usually contain the information themselves**.

Instead, they describe **what kind of information comes next**.

---

# What Is an Argument?

An **argument** is the actual value supplied to the command.

For example:

```bash
-u http://example.com
```

Here:

Flag:

```text
-u
```

Argument:

```text
http://example.com
```

The flag tells the program **what** the value represents.

The argument is the value itself.

---

# Example

```bash
gobuster dir -u http://www.onlineshop.thm/ -w wordlist.txt
```

Breaking it down:

| Component | Description |
|-----------|-------------|
| `gobuster` | Program |
| `dir` | Subcommand |
| `-u` | Flag |
| `http://www.onlineshop.thm/` | Argument |
| `-w` | Flag |
| `wordlist.txt` | Argument |

---

# Short Flags vs Long Flags

Many programs provide both short and long versions.

Short:

```bash
-u
```

Long:

```bash
--url
```

Example:

```bash
gobuster dir -u http://example.com
```

and

```bash
gobuster dir --url http://example.com
```

Both commands perform the same task.

The only difference is readability.

---

# Why Use Flags?

Imagine typing:

```bash
gobuster dir http://example.com wordlist.txt
```

How would Gobuster know:

- Which value is the URL?
- Which value is the wordlist?

Flags remove ambiguity.

Instead, you write:

```bash
-u http://example.com
-w wordlist.txt
```

Now the program knows exactly what each value represents.

---

# Mental Model

Think of flags as labels.

Instead of saying:

> Here are two pieces of information.

You are saying:

> This is the URL.

> This is the wordlist.

Programs understand labels much more reliably than guessing.

---

# Key Takeaways

- Flags describe what information is being provided.
- Arguments are the actual values supplied to the program.
- Most command-line tools rely heavily on flags.
- Short and long flags often perform the same function.
- Flags make commands easier for both humans and computers to understand.
