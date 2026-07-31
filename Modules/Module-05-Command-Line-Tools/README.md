# Command-Line Programs and Subcommands

## Overview

One of the biggest realizations when learning cybersecurity is that many command-line tools don't perform an action simply because you typed their name.

Typing a program's name only launches the program. You must usually tell it **what job to perform** by providing a subcommand.

Understanding this pattern makes learning new tools much easier because thousands of Linux utilities follow the same design.

---

## The General Pattern

Every command generally follows this structure:

```text
program subcommand options arguments
```

Example:

```bash
git clone
git status
git push
```

Here:

- `git` is the program.
- `clone`, `status`, and `push` are subcommands that tell Git what job to perform.

---

## Gobuster Example

### Incorrect

```bash
gobuster
```

Result:

The help menu is displayed because Gobuster doesn't know what task you want it to perform.

It is essentially asking:

> "Which mode would you like to use?"

---

## Gobuster Modes

### Directory Enumeration

```bash
gobuster dir
```

Searches for hidden directories and files.

### DNS Enumeration

```bash
gobuster dns
```

Searches for subdomains.

Each mode performs a completely different task.

---

## Running a Directory Scan

Long syntax:

```bash
gobuster dir --url http://www.onlineshop.thm/ -w /usr/share/wordlists/dirbuster/directory-list.txt
```

Short syntax:

```bash
gobuster dir -u http://www.onlineshop.thm/ -w /usr/share/wordlists/dirbuster/directory-list.txt
```

Breaking it down:

| Part | Purpose |
|------|---------|
| `gobuster` | Launches the Gobuster program |
| `dir` | Selects directory enumeration mode |
| `-u` / `--url` | Specifies the target website |
| `-w` / `--wordlist` | Specifies the wordlist to use |

---

## Why the Help Menu Appears

If Gobuster doesn't receive enough information to determine which task to perform, it displays the help page instead of running.

This is normal behavior.

The help page is not an error.

It is documentation explaining how to use the tool.

---

## Mental Model

Think of the command as a sentence.

```text
Gobuster,
use directory mode,
scan this website,
using this wordlist.
```

Each piece contributes one part of the instruction.

---

## This Pattern Exists Everywhere

### Git

```bash
git clone
git pull
git push
```

### Docker

```bash
docker run
docker build
docker ps
```

### Systemctl

```bash
systemctl start
systemctl stop
systemctl restart
```

### Gobuster

```bash
gobuster dir
gobuster dns
```

Learning this pattern makes it much easier to pick up new command-line tools.

---

## Key Takeaways

- Typing only the program name usually does **not** execute a task.
- Many CLI tools organize functionality into **subcommands**.
- Options (flags) modify how the selected subcommand behaves.
- A help menu usually means the command syntax is incomplete, not that the program is broken.

---

## Personal Insight

This was the point where I stopped memorizing Gobuster commands and started recognizing a universal CLI pattern.

Instead of thinking:

> "I need to memorize Gobuster."

I now think:

> "Every command-line program has a program name, a job (subcommand), and options."

That mental model transfers directly to Git, Docker, PowerShell, Nmap, Metasploit, Kubernetes, and countless other command-line tools.
