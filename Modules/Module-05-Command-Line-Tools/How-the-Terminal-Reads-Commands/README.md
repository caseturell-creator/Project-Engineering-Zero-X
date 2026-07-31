# How the Terminal Reads Commands

## Overview

One of the most common misconceptions about the command line is that it "understands" what you're trying to do.

It doesn't.

The terminal simply **parses** your input by breaking it into individual pieces called **tokens** and passing them to the program exactly as you typed them.

Understanding this process explains why even a small typo or misplaced space can completely change the meaning of a command.

---

# The Parsing Process

When you press **Enter**, the shell reads your command from left to right.

It separates the command wherever it encounters whitespace (spaces or tabs).

For example:

```bash
gobuster dir -u http://example.com -w wordlist.txt
```

The shell breaks this into individual tokens:

```text
Token 1: gobuster
Token 2: dir
Token 3: -u
Token 4: http://example.com
Token 5: -w
Token 6: wordlist.txt
```

These tokens are then passed to the Gobuster program.

The shell does **not** determine what they mean.

Gobuster does.

---

# The Shell vs. The Program

Think of the shell as a delivery service.

Its job is simply to deliver the pieces of your command.

Example:

```bash
gobuster dir -u http://example.com
```

The shell says:

> "Here are six tokens."

Gobuster says:

> "I know how to interpret these tokens."

Each program decides what each token means.

---

# Why Spaces Matter

The shell uses spaces to separate tokens.

Example:

Correct:

```bash
-u http://example.com
```

Produces two tokens:

```text
-u
http://example.com
```

If you accidentally remove or add spaces in the wrong place, the program may receive completely different input.

Even one misplaced space can change how a command is interpreted.

---

# Programs Don't Guess

If a program expects:

```text
program
subcommand
flag
argument
```

and receives something different, it won't try to figure out what you meant.

Instead, it usually responds by:

- Displaying a help menu
- Reporting invalid syntax
- Returning an error message

Computers follow instructions exactly as written.

---

# Why This Matters

Understanding parsing helps explain many common problems:

- Missing arguments
- Invalid flags
- Incorrect option order
- Extra spaces
- Missing spaces
- Unexpected command output

Many "broken" commands are simply commands that were parsed differently than intended.

---

# Mental Model

Imagine placing labeled cards on a table.

```text
[gobuster]

[dir]

[-u]

[http://example.com]

[-w]

[wordlist.txt]
```

The shell hands these cards to Gobuster.

Gobuster decides how to interpret each one.

Neither the shell nor the program reads your mind.

---

# Key Takeaways

- The shell breaks commands into tokens.
- Spaces separate tokens.
- Programs interpret the tokens they receive.
- Computers execute commands exactly as written.
- Understanding parsing makes troubleshooting command-line problems much easier.
