# Reading Help Menus

## Overview

One of the most valuable habits when learning command-line tools is understanding how to read a help menu.

Many beginners see a help screen and immediately think something went wrong.

In reality, the help menu is the program's built-in documentation.

Learning to read it allows you to solve many problems without searching the internet.

---

## When Does a Help Menu Appear?

A program may display its help menu when:

- You provide no arguments.
- Your syntax is incomplete.
- You type an invalid option.
- You explicitly request help.

Example:

```bash
gobuster
```

Since Gobuster wasn't told what mode to use, it displays its help menu.

---

## Help Flags

Most command-line programs provide one or both of these options:

```bash
--help
```

or

```bash
-h
```

Example:

```bash
gobuster --help
```

This displays the program's documentation directly in the terminal.

---

## Reading the Output

A help page usually contains several sections.

Example:

```text
Usage:
```

Shows the correct command format.

Example:

```text
Available Commands:
```

Lists the subcommands the program supports.

Example:

```text
Flags:
```

Lists available options and their descriptions.

---

## Gobuster Example

Help output:

```text
Available Commands:

dir
dns
```

This tells you Gobuster supports at least two modes:

- `dir` → Directory enumeration
- `dns` → DNS enumeration

The answer to your problem was already on the screen.

---

## Learn to Investigate

Instead of immediately searching online, ask yourself:

- What is the program telling me?
- Did I forget a required argument?
- Does the help menu show the syntax?
- Is the command I need listed?

These questions often solve the issue in seconds.

---

## Why This Matters

Professional penetration testers constantly use help menus.

Nobody memorizes every option for every tool.

Experienced professionals know **where to find the information**, not necessarily every command from memory.

---

## Key Takeaways

- A help menu is documentation, not an error.
- Learn to read the sections of the help output.
- Most tools support `-h` or `--help`.
- Help menus often contain the exact syntax needed to fix your command.
- Building the habit of reading documentation will make learning new tools much faster.
