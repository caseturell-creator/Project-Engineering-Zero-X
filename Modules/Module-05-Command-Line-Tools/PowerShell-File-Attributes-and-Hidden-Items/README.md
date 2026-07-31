# PowerShell File Attributes and Hidden Items

## Overview

Windows files and folders can have attributes that affect how they appear and behave.

One common attribute is `Hidden`. File Explorer and PowerShell may omit hidden items from normal directory listings unless explicitly instructed to include them.

This topic covers:

- Windows file attributes
- The PowerShell `Mode` column
- Revealing hidden items
- Checking an item's attributes
- Adding or removing the Hidden attribute
- The difference between hidden and protected

---

## Normal Directory Listing

```powershell
Get-ChildItem
```

`Get-ChildItem` lists the files and folders inside a location.

Example:

```powershell
Get-ChildItem C:\Users\p1r4t3
```

However, hidden items may not appear in the normal output.

---

## Reveal Hidden Items

```powershell
Get-ChildItem -Force
```

The `-Force` parameter tells PowerShell to include items that would normally be hidden.

Example:

```powershell
Get-ChildItem C:\Users\p1r4t3 -Force
```

This revealed the hidden folder:

```text
hidden-treasure-chest
```

---

## Understanding `-Force`

`-Force` changes how a command behaves.

It is a parameter, not an independent command.

Incorrect:

```powershell
-Force
```

Correct:

```powershell
Get-ChildItem -Force
```

Conceptually:

```text
Get-ChildItem = List the items
-Force        = Include normally hidden items
```

---

## The `Mode` Column

`Get-ChildItem` may display a `Mode` column.

Example:

```text
Mode                 Name
----                 ----
d----                 Documents
d--h-                 hidden-treasure-chest
-a---                 notes.txt
```

The letters indicate attributes or item types.

Common indicators include:

```text
d = Directory
a = Archive
r = Read-only
h = Hidden
s = System
l = Link
```

The exact appearance can vary between PowerShell versions.

The important clue in this exercise was the presence of:

```text
h
```

This indicated that the item had the Hidden attribute.

---

## Check an Item's Attributes

```powershell
Get-Item .\hidden-treasure-chest -Force |
    Select-Object Name, Attributes
```

Example output:

```text
Name                     Attributes
----                     ----------
hidden-treasure-chest    Hidden, Directory
```

This shows that the item is:

- A directory
- Marked as hidden

---

## Access the Attributes Directly

```powershell
(Get-Item .\hidden-treasure-chest -Force).Attributes
```

Example result:

```text
Hidden, Directory
```

The parentheses run `Get-Item` first.

The `.Attributes` section retrieves only the object's `Attributes` property.

---

## Check Whether an Item Is Hidden

```powershell
$item = Get-Item .\hidden-treasure-chest -Force

$item.Attributes -match "Hidden"
```

Possible result:

```text
True
```

This means the item has the Hidden attribute.

```text
False
```

This means the item is not marked as hidden.

---

## Hide a File or Folder

A file can be marked as hidden through its `Attributes` property.

```powershell
$item = Get-Item .\notes.txt

$item.Attributes += "Hidden"
```

For a folder:

```powershell
$item = Get-Item .\Treasure-Chest

$item.Attributes += "Hidden"
```

Afterward, the item may disappear from a normal listing:

```powershell
Get-ChildItem
```

It can still be displayed with:

```powershell
Get-ChildItem -Force
```

---

## Remove the Hidden Attribute

```powershell
$item = Get-Item .\notes.txt -Force

$item.Attributes -= "Hidden"
```

The item should then appear in a normal directory listing again.

```powershell
Get-ChildItem
```

---

## Alternative Attribute Syntax

The Hidden attribute can also be added using a bitwise operation:

```powershell
$item = Get-Item .\notes.txt

$item.Attributes = $item.Attributes -bor
    [System.IO.FileAttributes]::Hidden
```

It can be removed with:

```powershell
$item.Attributes = $item.Attributes -band
    -bnot [System.IO.FileAttributes]::Hidden
```

This method is more explicit and useful when working with several attributes.

For basic use, the shorter method is easier:

```powershell
$item.Attributes += "Hidden"
```

---

## View All Items and Their Attributes

```powershell
Get-ChildItem -Force |
    Select-Object Name, Attributes
```

Example:

```text
Name                     Attributes
----                     ----------
Documents                Directory
hidden-treasure-chest    Hidden, Directory
notes.txt                Archive
```

This provides clearer attribute information than relying only on the abbreviated `Mode` column.

---

## Search for Hidden Items

### Current directory

```powershell
Get-ChildItem -Force |
    Where-Object {
        $_.Attributes -match "Hidden"
    }
```

### Include subdirectories

```powershell
Get-ChildItem -Force -Recurse |
    Where-Object {
        $_.Attributes -match "Hidden"
    }
```

Breakdown:

```text
Get-ChildItem -Force
```

Includes hidden items.

```text
-Recurse
```

Searches through subdirectories.

```text
Where-Object
```

Filters the results.

```text
$_.Attributes
```

Represents the attributes of the current item moving through the pipeline.

---

## Hidden Does Not Mean Secure

The Hidden attribute only changes normal visibility.

It does not:

- Encrypt the file
- Require a password
- Prevent access
- Remove the file
- Protect the contents
- Stop another user with permission from reading it

Anyone who runs:

```powershell
Get-ChildItem -Force
```

can reveal the item if they have permission to access the location.

The Hidden attribute is closer to closing a curtain than locking a vault.

---

## Hidden Items and Permissions

Visibility and access permission are separate concepts.

An item may be:

```text
Visible but inaccessible
```

or:

```text
Hidden but fully accessible
```

`-Force` reveals hidden items, but it does not bypass Windows security permissions.

If access is denied, PowerShell may display an error such as:

```text
Access to the path is denied.
```

The user would then need the correct permissions or an authorized elevated session.

---

## Hidden Versus System Attributes

A file may have both:

```text
Hidden
System
```

Example:

```text
Hidden, System, Archive
```

System files are often important Windows files.

They should not be modified merely because they appear in a `-Force` listing.

Always identify the file and understand its purpose before changing attributes or contents.

---

## Complete Investigation Workflow

```powershell
Get-ChildItem C:\Users\p1r4t3

Get-ChildItem C:\Users\p1r4t3 -Force

Get-Item C:\Users\p1r4t3\hidden-treasure-chest -Force |
    Select-Object Name, Attributes

Set-Location C:\Users\p1r4t3\hidden-treasure-chest

Get-ChildItem -Force
```

---

## Key Lessons

- Windows files and folders can contain attributes.
- The Hidden attribute removes an item from normal listings.
- `Get-ChildItem -Force` reveals hidden items.
- `-Force` is a parameter and cannot run independently.
- The `Mode` column provides abbreviated attribute information.
- `Get-Item` retrieves information about a specific item.
- The `Attributes` property shows the complete attribute list.
- Hidden items can still be accessed when permissions allow it.
- Hidden does not mean encrypted or protected.
- `-Force` does not bypass access permissions.
- `Where-Object` can filter results by attribute.
- `-Recurse` searches inside subdirectories.
- System files should be handled carefully.
