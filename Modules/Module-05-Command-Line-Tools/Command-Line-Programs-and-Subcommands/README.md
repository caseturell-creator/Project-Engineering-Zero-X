# Command-Line Programs and Subcommands

## Overview

One of the most important concepts in command-line interfaces (CLI) is understanding that simply typing a program's name rarely tells it enough to perform a task.

Most modern command-line applications are built around the idea of **subcommands**, where the program first needs to know **what type of operation** you want to perform before it can execute it.

Learning this pattern makes it much easier to learn new command-line tools because the same design appears throughout Linux, Windows, and cybersecurity applications.

---

# The General Structure

Many commands follow a structure similar to this:

```text
program subcommand [options] [arguments]
```

Each part has a specific purpose.

| Component | Purpose |
|-----------|---------|
| **Program** | The application you want to run. |
| **Subcommand** | The action or mode the program should use. |
| **Options (Flags)** | Modify how the action is performed. |
| **Arguments** | The values supplied to the program. |

---

# Breaking Down an Example

Command:

```bash
gobuster dir -u http://www.onlineshop.thm/ -w wordlist.txt
```

| Part | Meaning |
|------|---------|
| `gobuster` | The program being executed. |
| `dir` | The subcommand (directory enumeration mode). |
| `-u` | Option specifying the target URL. |
| `http://www.onlineshop.thm/` | Argument supplied to `-u`. |
| `-w` | Option specifying the wordlist. |
| `wordlist.txt` | Argument supplied to `-w`. |

When read like a sentence:

> Run **Gobuster**, use **directory mode**, scan **this website**, and use **this wordlist**.

---

# What Happens if the Subcommand Is Missing?

If you execute:

```bash
gobuster
```

Gobuster launches successfully, but it doesn't know **which job** you want it to perform.

Instead of scanning, it displays its help menu.

This is normal behavior.

The program is not broken.

It is asking for additional instructions.

---

# Real-World Examples

## Git

```bash
git clone
git pull
git push
git status
```

Program:

```text
git
```

Subcommands:

```text
clone
pull
push
status
```

---

## Docker

```bash
docker run
docker build
docker ps
```

Program:

```text
docker
```

Subcommands:

```text
run
build
ps
```

---

## Systemctl

```bash
systemctl start
systemctl stop
systemctl restart
systemctl status
```

Program:

```text
systemctl
```

Subcommands:

```text
start
stop
restart
status
```

---

## Gobuster

```bash
gobuster dir
gobuster dns
```

Program:

```text
gobuster
```

Subcommands:

```text
dir
dns
```

---

# Why This Design Exists

Instead of creating separate programs for every task, developers group related functionality into a single application.

For example, Gobuster can perform multiple types of enumeration.

Rather than creating programs like:

```text
gobuster-dir
gobuster-dns
```

the developer created one program with multiple operating modes.

This keeps tools organized, easier to maintain, and more consistent to use.

---

# Mental Model

Think of the command as giving instructions to another person.

```text
Program:
"Who am I talking to?"

↓

Subcommand:
"What do I want you to do?"

↓

Options:
"How should you do it?"

↓

Arguments:
"What information do you need?"
```

Every command becomes a complete instruction.

---

# Key Takeaways

- Typing only the program name usually does **not** perform a task.
- Many command-line tools use **subcommands** to organize their functionality.
- Flags (options) modify how a subcommand behaves.
- Arguments provide the information needed to perform the task.
- Understanding the structure of commands is more valuable than memorizing individual commands.
- Once you learn this pattern, you'll recognize it across Git, Docker, PowerShell, Gobuster, Metasploit, Nmap, Hydra, and many other command-line tools.

---

# Personal Insight

This was the point where I stopped memorizing individual commands and started recognizing the architecture behind command-line tools.

Instead of asking:

> "What's the Gobuster command?"

I started asking:

> "What is the program, what job am I asking it to do, and what information does it need?"

That change in thinking made learning new CLI tools significantly easier because the underlying pattern remains remarkably consistent.
