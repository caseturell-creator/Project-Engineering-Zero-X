# PowerShell Command Syntax and Error Reading

## Overview

PowerShell errors are not always caused by a difficult technical problem.

Many failures come from small issues such as:

- Misspelled command names
- Missing command parameters
- Running a parameter by itself
- Searching from the wrong directory
- Confusing wrapped terminal output with separate text
- Copying the PowerShell prompt as part of a command

Learning how to read the error before changing anything makes troubleshooting faster and prevents random guessing.

---

## PowerShell Cmdlet Structure

Most PowerShell cmdlets follow this pattern:

```text
Verb-Noun
```

Examples:

```powershell
Get-ChildItem
Get-Content
Get-FileHash
Set-Location
Select-Object
```

The verb describes the action.

The noun describes what the command acts on.

Example:

```powershell
Get-FileHash
```

Breakdown:

```text
Get      = retrieve or calculate information
FileHash = the information being requested
```

---

## Cmdlet Spelling Matters

PowerShell cannot automatically understand a command when its name is misspelled.

Incorrect:

```powershell
Get-Hash
```

Incorrect:

```powershell
Get-FlashHash
```

Correct:

```powershell
Get-FileHash
```

A small letter-order mistake can create a completely different command name that does not exist.

---

## Understanding “Command Not Found”

Example error:

```text
The term 'Get-FlashHash' is not recognized as the name of a cmdlet,
function, script file, or executable program.
```

This usually means PowerShell could not find a command with that exact name.

Possible causes include:

- The command was misspelled
- The wrong command name was used
- A required module is unavailable
- A parameter was entered as though it were a command

The first check should be the command's exact spelling.

---

## Parameters Are Not Commands

A parameter modifies how a command behaves.

Example:

```powershell
Get-ChildItem -Force
```

Here:

```text
Get-ChildItem = command
-Force        = parameter
```

Running only the parameter will fail:

```powershell
-Force
```

PowerShell treats it as though it were the name of a command.

Correct:

```powershell
Get-ChildItem -Force
```

---

## Commands Can Be Valid but Incomplete

This command is valid:

```powershell
Get-FileHash .\big-treasure.txt | Select-Object
```

However, it does not tell `Select-Object` which property should be selected.

To display only the complete hash, the command needs:

```powershell
-ExpandProperty Hash
```

Complete command:

```powershell
Get-FileHash .\big-treasure.txt |
    Select-Object -ExpandProperty Hash
```

The problem was not that `Select-Object` was misspelled.

The command simply stopped before the required property instructions were included.

---

## Command, Parameter, and Argument

Consider:

```powershell
Get-ChildItem C:\Users\p1r4t3 -Force
```

Breakdown:

```text
Get-ChildItem      = command
C:\Users\p1r4t3   = path argument
-Force             = parameter
```

Another example:

```powershell
Select-Object -ExpandProperty Hash
```

Breakdown:

```text
Select-Object     = command
-ExpandProperty   = parameter
Hash              = argument supplied to the parameter
```

The command performs the action.

The parameter changes or specifies the action.

The argument provides the value the command or parameter should use.

---

## Reading Path Errors

Example error:

```text
Cannot find path because it does not exist.
```

This does not always mean the folder is absent.

It may mean PowerShell searched from the wrong location.

For example, while located in:

```text
C:\Users\captain
```

this command:

```powershell
Set-Location .\hidden-treasure-chest
```

searches for:

```text
C:\Users\captain\hidden-treasure-chest
```

If the folder actually belongs to another user, the correct path may be:

```powershell
Set-Location C:\Users\p1r4t3\hidden-treasure-chest
```

Before assuming a file or folder is missing, check the current location:

```powershell
Get-Location
```

---

## Relative and Full Paths

### Relative path

```powershell
.\big-treasure.txt
```

The `.\` symbol means:

```text
Begin from the current directory.
```

Relative paths depend on where the terminal is currently located.

### Full path

```powershell
C:\Users\p1r4t3\hidden-treasure-chest\big-treasure.txt
```

A full path starts from the drive and identifies the complete location.

Full paths are useful when the current working directory is uncertain.

---

## The PowerShell Prompt Is Not Part of the Command

A PowerShell prompt may look like:

```text
PS C:\Users\p1r4t3\hidden-treasure-chest>
```

Only type the command after the `>` symbol.

Example screen:

```text
PS C:\Users\p1r4t3\hidden-treasure-chest> Get-Content .\big-treasure.txt
```

The actual command is:

```powershell
Get-Content .\big-treasure.txt
```

Do not copy:

```text
PS C:\Users\p1r4t3\hidden-treasure-chest>
```

That text only shows the current shell and directory.

---

## Terminal Line Wrapping

A terminal may wrap long output onto the next visual line.

Example:

```text
hidden-treasure-
chest
```

This may still represent one folder:

```text
hidden-treasure-chest
```

Another example:

```text
big-treasure.
txt
```

This may still be one filename:

```text
big-treasure.txt
```

Line wrapping changes how output appears on the screen. It does not necessarily change the actual filename.

---

## Truncated Output

PowerShell may shorten long values with three dots:

```text
71FC5EC11C2497A32F8F08E61399687D90ABE6E204D2...
```

This does not mean the original value is incomplete.

It means the table formatter shortened the displayed version to fit the terminal.

To display the complete property value:

```powershell
Get-FileHash .\big-treasure.txt |
    Select-Object -ExpandProperty Hash
```

---

## Verify Commands Before Retyping Them

When PowerShell says a command is not recognized, compare the typed command with the intended command one section at a time.

Example:

```text
Typed:    Get-FlashHash
Correct:  Get-FileHash
```

Compare:

```text
Get-
FlashHash
FileHash
```

This is more reliable than repeatedly retyping the entire command from memory.

---

## Useful Verification Commands

### Find a command

```powershell
Get-Command Get-FileHash
```

### Search commands by keyword

```powershell
Get-Command *Hash*
```

### Read command help

```powershell
Get-Help Get-FileHash
```

### View examples

```powershell
Get-Help Get-FileHash -Examples
```

### View detailed help

```powershell
Get-Help Get-FileHash -Detailed
```

These commands help confirm:

- Whether a cmdlet exists
- Its correct spelling
- Which parameters it accepts
- How it should be used

---

## Troubleshooting Process

When a PowerShell command fails, check the following in order:

### 1. Read the first line of the error

Identify whether PowerShell is reporting:

```text
Command not found
Path not found
Parameter not found
Access denied
```

### 2. Check the command spelling

Confirm the complete `Verb-Noun` name.

### 3. Check the current directory

```powershell
Get-Location
```

### 4. Confirm the target exists

```powershell
Get-ChildItem -Force
```

### 5. Check whether the command is incomplete

Look for missing parameters or arguments.

### 6. Use PowerShell help

```powershell
Get-Help CommandName -Examples
```

This process is faster than making random changes to the command.

---

## Complete Example

```powershell
Get-Location

Get-ChildItem C:\Users\p1r4t3 -Force

Set-Location C:\Users\p1r4t3\hidden-treasure-chest

Get-ChildItem -Force

Get-Content .\big-treasure.txt

Get-FileHash .\big-treasure.txt |
    Select-Object -ExpandProperty Hash
```

Each line has a specific job:

```text
Get-Location       = confirm the current directory
Get-ChildItem      = list items
-Force             = include hidden items
Set-Location       = change directories
Get-Content        = read the file
Get-FileHash       = calculate the file hash
|                  = pass the object forward
Select-Object      = select information
-ExpandProperty    = extract one property value
Hash               = property being extracted
```

---

## Key Lessons

- PowerShell cmdlets commonly use a `Verb-Noun` naming structure.
- A small spelling error can produce a command-not-found message.
- Parameters must be attached to commands.
- Arguments provide values to commands and parameters.
- A command can be valid but incomplete for the intended task.
- Relative paths begin from the current directory.
- Full paths eliminate uncertainty about location.
- The PowerShell prompt is not part of the command.
- Terminal wrapping does not necessarily split a filename.
- Three dots usually indicate shortened display output.
- Error messages should guide troubleshooting instead of triggering random guesses.
- `Get-Command` and `Get-Help` can verify syntax before repeating a command.
