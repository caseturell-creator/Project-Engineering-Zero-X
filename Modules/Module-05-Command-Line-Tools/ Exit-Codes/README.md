# Exit Codes

## Overview

Whenever a command-line program finishes running, it returns a small integer value to the operating system called an **exit code** (also known as a **return code** or **exit status**).

This number tells the shell whether the command completed successfully or encountered a problem.

Although many programs produce text output, computers primarily use exit codes to determine success or failure.

---

# Why Exit Codes Exist

Humans read text.

Computers read numbers.

Consider this output:

```text
Scan completed successfully.
```

A person immediately understands the result.

A script, however, cannot reliably interpret every possible success message from every program.

Instead, it checks the program's exit code.

---

# Common Exit Codes

Most command-line programs follow these conventions:

| Exit Code | Meaning |
|-----------|---------|
| `0` | Success |
| Non-zero | An error or abnormal termination occurred |

Examples:

```text
0
```

The command completed successfully.

```text
1
```

A general error occurred.

Different programs may assign different meanings to non-zero exit codes, so always consult the program's documentation.

---

# Example

Suppose you run:

```bash
ls
```

If everything works correctly:

```text
Exit Code: 0
```

If you attempt to list a directory that doesn't exist:

```bash
ls nonexistent_folder
```

You might receive:

```text
ls: cannot access 'nonexistent_folder': No such file or directory
```

The exit code would be non-zero because the command failed.

---

# Viewing the Last Exit Code

## Linux (Bash)

```bash
echo $?
```

This displays the exit code of the most recently executed command.

Example:

```bash
ls
echo $?
```

Output:

```text
0
```

---

## PowerShell

```powershell
$LASTEXITCODE
```

PowerShell stores the exit code of the last native command in the `$LASTEXITCODE` variable.

---

# Why This Matters

Exit codes are essential for:

- Shell scripting
- Automation
- Continuous Integration (CI)
- System administration
- Cybersecurity tools
- Error handling

Instead of checking printed text, scripts check the exit code to determine whether to continue or stop.

---

# Mental Model

Think of a command like a student taking a test.

After finishing, the student hands in a report card.

The report card is the exit code.

```text
0
```

"I completed the task successfully."

```text
Non-zero
```

"Something prevented me from completing the task."

---

# Key Takeaways

- Every command returns an exit code.
- `0` almost always means success.
- Non-zero values indicate some type of error.
- Scripts rely on exit codes far more than printed messages.
- Understanding exit codes makes troubleshooting and automation much more reliable.
