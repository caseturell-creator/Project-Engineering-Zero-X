# Understanding Command Syntax

## Overview

Almost every command-line instruction is built from the same building blocks.

Learning these pieces is more valuable than memorizing individual commands because the structure repeats across thousands of tools.

---

## Basic Structure

```text
program subcommand options arguments
```

Not every command uses every part, but most modern CLI tools follow this format.

---

## Program

The program is the executable you want to run.

Examples:

```bash
git
gobuster
docker
ping
python
powershell
```

Think of it as opening an application from the terminal.

---

## Subcommand

A subcommand tells the program **what action to perform**.

Examples:

```bash
git clone
git status
docker run
gobuster dir
gobuster dns
```

Without the subcommand, many programs don't know which feature you want to use.

---

## Options (Flags)

Flags modify how the command behaves.

Examples:

```bash
-u
-w
-v
-h
--help
--url
--wordlist
```

Many tools provide both:

Short version:

```bash
-u
```

Long version:

```bash
--url
```

Both usually perform the same function.

---

## Arguments

Arguments are the actual values supplied to the command.

Example:

```bash
gobuster dir -u http://www.onlineshop.thm/
```

Here:

Program:

```text
gobuster
```

Subcommand:

```text
dir
```

Flag:

```text
-u
```

Argument:

```text
http://www.onlineshop.thm/
```

---

## Reading Commands Like a Sentence

Instead of memorizing symbols, read commands as instructions.

Example:

```bash
gobuster dir -u http://www.onlineshop.thm/ -w wordlist.txt
```

Can be read as:

> Run Gobuster, use directory mode, scan this website, and use this wordlist.

---

## Why This Matters

Once you recognize these building blocks, you can approach unfamiliar tools with confidence.

Instead of asking:

> "Do I know this command?"

You begin asking:

- What is the program?
- What job am I asking it to do?
- Which flags change its behavior?
- What values am I providing?

Those four questions apply to an enormous number of command-line tools used in cybersecurity.

---

## Key Takeaways

- Every command begins with a program.
- Many programs require a subcommand.
- Flags modify behavior.
- Arguments provide the data the program needs.
- Learn the structure, not just individual commands.
