# PowerShell Hidden File Discovery

## Overview

This exercise involved using PowerShell to search another Windows user's profile, reveal a hidden folder, locate a text file, and retrieve its complete SHA-256 hash.

The main concepts were:

- Navigating with full and relative paths
- Revealing hidden files with `-Force`
- Reading files with `Get-Content`
- Calculating hashes with `Get-FileHash`
- Extracting PowerShell object properties
- Understanding terminal line wrapping and shortened output

---

## Scenario

The PowerShell session started inside the current user's profile:

```text
C:\Users\captain
```

The target user was:

```text
p1r4t3
```

A hidden folder existed inside that user's profile:

```text
C:\Users\p1r4t3\hidden-treasure-chest
```

Inside the folder was the following file:

```text
big-treasure.txt
```

---

## 1. List Windows User Profiles

```powershell
Get-ChildItem C:\Users
```

This displays the user profile folders stored inside `C:\Users`.

It helped identify the target user:

```text
p1r4t3
```

---

## 2. Reveal Hidden Items

```powershell
Get-ChildItem C:\Users\p1r4t3 -Force
```

The `-Force` parameter tells PowerShell to include hidden files and folders in the results.

Without `-Force`, hidden items may not appear.

### Important

`-Force` is a parameter, not a command.

Incorrect:

```powershell
-Force
```

Correct:

```powershell
Get-ChildItem -Force
```

---

## 3. Enter the Hidden Folder

```powershell
Set-Location C:\Users\p1r4t3\hidden-treasure-chest
```

The full path was necessary because the current directory belonged to another user:

```text
C:\Users\captain
```

This relative-path command would search from the wrong location:

```powershell
Set-Location .\hidden-treasure-chest
```

The `.\` symbol means:

```text
Start from the current directory.
```

PowerShell would therefore search for:

```text
C:\Users\captain\hidden-treasure-chest
```

That path did not exist.

---

## 4. Confirm the Current Location

```powershell
Get-Location
```

Expected result:

```text
C:\Users\p1r4t3\hidden-treasure-chest
```

The PowerShell prompt also shows the current directory:

```text
PS C:\Users\p1r4t3\hidden-treasure-chest>
```

The prompt is not part of the command and should not be copied into an answer field.

---

## 5. List the Folder Contents

```powershell
Get-ChildItem -Force
```

This revealed the file:

```text
big-treasure.txt
```

A terminal may visually wrap a long filename onto another line.

For example:

```text
big-treasure.
txt
```

This does not necessarily mean there are two separate names. It can still be one filename:

```text
big-treasure.txt
```

---

## 6. Read the File

```powershell
Get-Content .\big-treasure.txt
```

`Get-Content` reads and displays the information stored inside a file.

The filename was only the container. The hidden answer was contained inside it.

---

## 7. Calculate the File Hash

```powershell
Get-FileHash .\big-treasure.txt
```

By default, `Get-FileHash` calculates a SHA-256 hash.

The result contains multiple properties:

```text
Algorithm
Hash
Path
```

Example:

```text
Algorithm : SHA256
Hash      : A long hexadecimal value
Path      : The file's full path
```

---

## 8. Display the Complete Hash

The regular table output may shorten a long hash using three dots:

```text
71FC5EC11C2497A32F8F08E61399687D90ABE6E204D2...
```

To display only the complete hash:

```powershell
Get-FileHash .\big-treasure.txt | Select-Object -ExpandProperty Hash
```

A shorter version is:

```powershell
(Get-FileHash .\big-treasure.txt).Hash
```

---

## Understanding `-ExpandProperty`

PowerShell commands return structured objects rather than only plain text.

This command:

```powershell
Get-FileHash .\big-treasure.txt
```

returns an object containing the file's:

- Algorithm
- Hash
- Path

The pipeline symbol:

```powershell
|
```

passes that object into the next command.

This section:

```powershell
Select-Object -ExpandProperty Hash
```

selects the `Hash` property and prints its complete value.

It essentially means:

```text
Take the Hash field out of the object and display only its value.
```

---

## Complete Workflow

```powershell
Get-ChildItem C:\Users

Get-ChildItem C:\Users\p1r4t3 -Force

Set-Location C:\Users\p1r4t3\hidden-treasure-chest

Get-Location

Get-ChildItem -Force

Get-Content .\big-treasure.txt

Get-FileHash .\big-treasure.txt | Select-Object -ExpandProperty Hash
```

---

## Errors Encountered

### Path Not Found

```text
Cannot find path because it does not exist.
```

Cause:

The hidden folder was searched for from the wrong user's directory.

Fix:

```powershell
Set-Location C:\Users\p1r4t3\hidden-treasure-chest
```

---

### `-Force` Was Treated as a Command

Incorrect:

```powershell
-Force
```

Correct:

```powershell
Get-ChildItem -Force
```

Parameters must be attached to commands that support them.

---

### Incorrect Cmdlet Name

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

PowerShell cmdlets commonly follow the structure:

```text
Verb-Noun
```

In this case:

- `Get` is the verb
- `FileHash` is the noun

---

### Hash Output Was Too Short

Cause:

PowerShell's table formatting shortened the displayed hash to fit the terminal width.

Fix:

```powershell
Get-FileHash .\big-treasure.txt | Select-Object -ExpandProperty Hash
```

A SHA-256 hash contains 64 hexadecimal characters.

---

## Key Lessons

- `Get-ChildItem` lists files, folders, and other child items.
- `-Force` reveals hidden items.
- Parameters cannot normally run by themselves.
- Relative paths begin from the current working directory.
- Full paths remove ambiguity when navigating between user profiles.
- `Set-Location` changes the current directory.
- `Get-Location` confirms the current directory.
- `Get-Content` reads a file.
- `Get-FileHash` calculates a cryptographic hash.
- PowerShell commands return structured objects.
- The pipeline passes objects between commands.
- `Select-Object -ExpandProperty` extracts one complete property value.
- Terminal wrapping does not automatically mean a filename is split.
- Error messages often reveal whether the problem is the path, spelling, or command structure.
