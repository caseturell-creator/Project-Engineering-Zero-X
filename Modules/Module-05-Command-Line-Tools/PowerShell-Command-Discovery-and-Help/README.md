# PowerShell Command Discovery and Built-In Help

## Overview

PowerShell includes built-in tools for finding commands, confirming their spelling, viewing available parameters, and reading usage examples.

These tools are useful when:

- A command is not recognized
- The exact cmdlet name is forgotten
- A parameter is unfamiliar
- A command works but does not produce the expected output
- A similar command needs to be found

The two main cmdlets are:

```powershell
Get-Command
Get-Help
```

---

## PowerShell Cmdlet Naming

PowerShell cmdlets commonly follow this structure:

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

```text
Get-FileHash

Get      = retrieve or calculate
FileHash = the information being requested
```

---

## Confirm That a Command Exists

```powershell
Get-Command Get-FileHash
```

This checks whether `Get-FileHash` exists and displays information about it.

Example output may include:

```text
CommandType
Name
Version
Source
```

This is useful when PowerShell reports:

```text
The term is not recognized as the name of a cmdlet.
```

---

## Search for Commands by Keyword

Wildcards can be used when only part of the command name is known.

```powershell
Get-Command *Hash*
```

This searches for commands containing the word `Hash`.

Another example:

```powershell
Get-Command *File*
```

The asterisk means:

```text
Match any characters before or after this word.
```

---

## Search by Verb

```powershell
Get-Command -Verb Get
```

This displays commands using the verb `Get`.

Other common verbs include:

```text
Set
New
Remove
Start
Stop
Select
Test
```

Example:

```powershell
Get-Command -Verb Remove
```

---

## Search by Noun

```powershell
Get-Command -Noun FileHash
```

Wildcards can also be used:

```powershell
Get-Command -Noun *File*
```

This helps locate commands related to a particular subject.

---

## Read Basic Command Help

```powershell
Get-Help Get-FileHash
```

This displays information such as:

- Command description
- Syntax
- Parameters
- Related commands

---

## View Command Examples

```powershell
Get-Help Get-FileHash -Examples
```

Examples are often the fastest way to understand how a command should be written.

Example usage:

```powershell
Get-FileHash .\big-treasure.txt
```

---

## View Detailed Help

```powershell
Get-Help Get-FileHash -Detailed
```

Detailed help includes more information about:

- Parameters
- Accepted inputs
- Returned objects
- Command behavior

---

## View Full Help

```powershell
Get-Help Get-FileHash -Full
```

This displays the most complete locally available help information.

It may include:

- Full parameter descriptions
- Input and output types
- Notes
- Multiple examples

---

## View Online Help

```powershell
Get-Help Get-FileHash -Online
```

This opens the official online documentation when internet access and a browser are available.

---

## View Only the Syntax

```powershell
Get-Command Get-FileHash -Syntax
```

Example structure:

```text
Get-FileHash [-Path] <String[]> [-Algorithm <String>]
```

Syntax helps identify:

- Required arguments
- Optional parameters
- Accepted value types

---

## Understanding Syntax Symbols

Example:

```text
Get-FileHash [-Path] <String[]> [-Algorithm <String>]
```

### Square brackets

```text
[ ]
```

Usually indicate an optional part of the syntax.

### Angle brackets

```text
< >
```

Describe the type of value expected.

Example:

```text
<String>
```

means the command expects text.

### Empty square brackets after a type

```text
<String[]>
```

means the parameter can accept one or more text values.

---

## Inspect a Specific Parameter

```powershell
Get-Help Get-FileHash -Parameter Algorithm
```

This displays information about the `-Algorithm` parameter.

Another example:

```powershell
Get-Help Get-ChildItem -Parameter Force
```

This helps explain exactly what `-Force` does.

---

## Discover Available Parameters

```powershell
(Get-Command Get-FileHash).Parameters
```

To display only the parameter names:

```powershell
(Get-Command Get-FileHash).Parameters.Keys
```

Example output:

```text
Path
LiteralPath
InputStream
Algorithm
ErrorAction
Verbose
```

---

## Use Tab Completion

Begin typing a command:

```powershell
Get-Fi
```

Then press:

```text
Tab
```

PowerShell may complete it as:

```powershell
Get-FileHash
```

Tab completion can also complete:

- Parameters
- File names
- Folder paths
- Command names

Example:

```powershell
Get-FileHash -Al
```

Pressing `Tab` may complete:

```powershell
Get-FileHash -Algorithm
```

This reduces spelling mistakes.

---

## Correcting a Command-Not-Found Error

Incorrect command:

```powershell
Get-FlashHash
```

PowerShell reports that the command is not recognized.

Search for related commands:

```powershell
Get-Command *Hash*
```

The result reveals:

```powershell
Get-FileHash
```

Then view examples:

```powershell
Get-Help Get-FileHash -Examples
```

---

## Command Discovery Workflow

```powershell
Get-Command *Hash*

Get-Command Get-FileHash -Syntax

Get-Help Get-FileHash

Get-Help Get-FileHash -Examples

Get-Help Get-FileHash -Parameter Algorithm
```

This workflow moves from discovery to understanding:

```text
Find the command
        |
        v
Confirm its syntax
        |
        v
Read its description
        |
        v
View examples
        |
        v
Inspect specific parameters
```

---

## When Help Is Missing

PowerShell may display limited help information if the local help files have not been downloaded.

Help files can be updated with:

```powershell
Update-Help
```

This may require:

- Administrator permission
- Internet access
- Access to the relevant PowerShell help source

Even without updated help files, basic syntax information is often still available through:

```powershell
Get-Command CommandName -Syntax
```

---

## Key Lessons

- `Get-Command` finds and verifies PowerShell commands.
- Wildcards help search when the exact command name is unknown.
- `Get-Help` explains how a command works.
- `-Examples` displays practical command examples.
- `-Detailed` provides expanded help.
- `-Full` displays the most complete local help.
- `-Parameter` explains one specific parameter.
- `-Syntax` shows the command structure.
- Tab completion reduces spelling and path errors.
- PowerShell's built-in help should be checked before repeatedly guessing command syntax.
