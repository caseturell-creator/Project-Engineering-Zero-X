# PowerShell Objects, Pipelines, and Property Extraction

## Overview

PowerShell commands often return structured objects instead of ordinary text.

An object can contain several named properties. The pipeline can pass that object into another command, allowing specific information to be selected or extracted.

This became important when a file hash appeared shortened in the terminal.

---

## PowerShell Returns Objects

Running:

```powershell
Get-FileHash .\big-treasure.txt
```

returns an object containing multiple properties:

```text
Algorithm
Hash
Path
```

The command does not return only the hash value.

Conceptually, the result looks like:

```text
FileHash Object
├── Algorithm: SHA256
├── Hash: Full hexadecimal hash
└── Path: File location
```

---

## The Pipeline

The pipeline symbol is:

```powershell
|
```

It passes the result from the command on the left into the command on the right.

Example:

```powershell
Get-FileHash .\big-treasure.txt | Select-Object Hash
```

The process is:

```text
Get-FileHash
      |
      v
Select-Object
```

The first command creates the object.

The second command receives that object and selects information from it.

---

## Selecting a Property

```powershell
Get-FileHash .\big-treasure.txt | Select-Object Hash
```

This selects the `Hash` property, but it still returns an object containing a property named `Hash`.

The output may still be displayed as a table:

```text
Hash
----
71FC5EC11C2497A32F8F08E61399687D...
```

Because PowerShell is formatting the result as a table, a long value may be shortened to fit the terminal window.

---

## Expanding a Property

```powershell
Get-FileHash .\big-treasure.txt |
    Select-Object -ExpandProperty Hash
```

`-ExpandProperty` extracts the value stored inside the selected property.

Instead of returning an object containing a `Hash` field, it prints the hash value directly.

Conceptually:

```text
Select-Object Hash
```

returns:

```text
Object
└── Hash: ABC123...
```

While:

```text
Select-Object -ExpandProperty Hash
```

returns:

```text
ABC123...
```

---

## Why Expansion Matters

Regular table output may shorten long values using:

```text
...
```

Example:

```text
71FC5EC11C2497A32F8F08E61399687D90ABE6E204D2...
```

The original value is still complete inside the object. Only its displayed version has been shortened.

Expanding the property avoids the table formatter:

```powershell
Get-FileHash .\big-treasure.txt |
    Select-Object -ExpandProperty Hash
```

This prints the complete SHA-256 hash.

---

## Direct Property Access

A shorter method is:

```powershell
(Get-FileHash .\big-treasure.txt).Hash
```

The parentheses run the command first:

```powershell
(Get-FileHash .\big-treasure.txt)
```

Then:

```powershell
.Hash
```

accesses the `Hash` property directly.

This produces the same complete value without using `Select-Object`.

---

## Comparing the Commands

### Display the Entire Object

```powershell
Get-FileHash .\big-treasure.txt
```

Returns:

```text
Algorithm
Hash
Path
```

### Select the Hash Property

```powershell
Get-FileHash .\big-treasure.txt |
    Select-Object Hash
```

Returns an object containing only the `Hash` property.

### Extract the Hash Value

```powershell
Get-FileHash .\big-treasure.txt |
    Select-Object -ExpandProperty Hash
```

Returns only the value inside the `Hash` property.

### Access the Property Directly

```powershell
(Get-FileHash .\big-treasure.txt).Hash
```

Also returns only the complete hash value.

---

## Viewing Available Properties

To examine the structure of an object:

```powershell
Get-FileHash .\big-treasure.txt | Get-Member
```

`Get-Member` displays the object's:

- Type
- Properties
- Methods

This helps identify which properties can be selected or accessed.

For example:

```text
Algorithm
Hash
Path
```

Once a property name is known, it can be extracted with:

```powershell
Select-Object -ExpandProperty PropertyName
```

Or accessed directly with:

```powershell
(Command).PropertyName
```

---

## General Examples

### Extract a Process Name

```powershell
Get-Process |
    Select-Object -ExpandProperty ProcessName
```

### Extract Service Display Names

```powershell
Get-Service |
    Select-Object -ExpandProperty DisplayName
```

### Extract File Names

```powershell
Get-ChildItem |
    Select-Object -ExpandProperty Name
```

The same pattern works across many PowerShell commands because they return structured objects.

---

## Command Structure

```powershell
Command |
    Select-Object -ExpandProperty PropertyName
```

Breakdown:

```text
Command
```

Creates or retrieves an object.

```text
|
```

Passes the object forward.

```text
Select-Object
```

Selects information from the object.

```text
-ExpandProperty
```

Extracts the property's stored value.

```text
PropertyName
```

Identifies which property should be extracted.

---

## Common Mistake: Stopping Too Early

This command is valid:

```powershell
Get-FileHash .\big-treasure.txt |
    Select-Object
```

However, it does not specify what should be selected or expanded.

To retrieve the complete hash, the command must include:

```powershell
-ExpandProperty Hash
```

Complete command:

```powershell
Get-FileHash .\big-treasure.txt |
    Select-Object -ExpandProperty Hash
```

The command was not misspelled. It was incomplete for the intended result.

---

## Key Lessons

- PowerShell commands return structured objects.
- Objects contain named properties.
- The pipeline passes objects between commands.
- `Select-Object` selects properties from an object.
- `-ExpandProperty` extracts the value inside a property.
- Table formatting may visually shorten long values.
- Shortened display output does not mean the stored value is incomplete.
- `(Command).Property` provides direct property access.
- `Get-Member` reveals the properties and methods available on an object.
- Understanding objects makes PowerShell more powerful than treating its output as plain text.
