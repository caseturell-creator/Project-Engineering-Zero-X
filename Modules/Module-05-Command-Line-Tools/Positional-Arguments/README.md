# Positional Arguments

## Overview

Not every command-line program requires flags for every piece of information.

Many programs determine what an argument means simply by **where it appears** in the command.

These are called **positional arguments**.

Understanding positional arguments is important because they appear throughout Linux, PowerShell, Git, and many cybersecurity tools.

---

# What Is a Positional Argument?

A positional argument is an argument whose meaning is determined by its position within the command.

Unlike flags, positional arguments do not have labels.

Instead, the program expects them in a specific order.

---

# Example

Consider the command:

```bash
cp report.txt backup.txt
```

The program interprets the arguments like this:

| Position | Meaning |
|----------|---------|
| First | Source file |
| Second | Destination file |

Because `cp` knows the expected order, flags are unnecessary.

---

# Another Example

```bash
ping google.com
```

Program:

```text
ping
```

Positional Argument:

```text
google.com
```

The program already knows the first argument should be the host to ping.

---

# Mixing Positional Arguments and Flags

Many commands use both.

Example:

```bash
ping -c 4 google.com
```

Breaking it down:

| Component | Purpose |
|-----------|---------|
| `ping` | Program |
| `-c` | Flag |
| `4` | Argument for `-c` |
| `google.com` | Positional argument |

The program understands both because it knows which values belong to flags and which values belong to positions.

---

# Why Position Matters

Imagine typing:

```bash
cp backup.txt report.txt
```

This command is valid.

However, it performs the opposite operation because the arguments have changed positions.

Even though the same filenames are used, their meaning changes based on where they appear.

---

# Flags vs Positional Arguments

Flags:

```bash
curl -o output.txt https://example.com
```

The flag tells the program exactly what the value represents.

---

Positional:

```bash
ping google.com
```

The program knows what the first argument represents simply because of its position.

---

# Mental Model

Think of positional arguments like seats in a car.

Seat 1:

Driver

Seat 2:

Passenger

Seat 3:

Rear passenger

Even if the same people are in the car, moving them to different seats changes their role.

Commands work the same way.

The position determines the meaning.

---

# Key Takeaways

- Positional arguments do not require flags.
- Their meaning is determined by their location within the command.
- Many programs combine positional arguments with flags.
- Changing the order of positional arguments can completely change what a command does.
- Understanding positional arguments makes command syntax much easier to read.
