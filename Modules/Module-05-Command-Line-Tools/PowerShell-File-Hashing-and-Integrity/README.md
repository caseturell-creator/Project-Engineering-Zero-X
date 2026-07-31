# PowerShell File Hashing and Integrity Verification

## Overview

A file hash is a fixed-length value calculated from the contents of a file.

Even a tiny change to the file normally produces a completely different hash. This makes hashes useful for checking whether a file has been modified, corrupted, or replaced.

PowerShell provides the `Get-FileHash` cmdlet for calculating file hashes.

---

## What Is a File Hash?

A hash function processes the contents of a file and produces a hexadecimal value.

Example:

```text
File
  |
  v
Hashing algorithm
  |
  v
A4F29C...
```

The resulting value acts like a digital fingerprint for the file.

Two files with identical contents should produce the same hash when the same algorithm is used.

Files with different contents should produce different hashes.

---

## Calculate a File Hash

```powershell
Get-FileHash .\big-treasure.txt
```

By default, PowerShell uses the SHA-256 algorithm.

Example output:

```text
Algorithm  Hash                                                             Path
---------  ----                                                             ----
SHA256     71FC5EC11C2497A32F8F08E61399687D90ABE6E204D2...                 C:\...
```

The result contains three main properties:

```text
Algorithm
Hash
Path
```

---

## Default Algorithm

The default algorithm used by `Get-FileHash` is:

```text
SHA256
```

A SHA-256 hash contains:

```text
64 hexadecimal characters
```

Hexadecimal characters use:

```text
0-9
A-F
```

Example structure:

```text
71FC5EC11C2497A32F8F08E61399687D90ABE6E204D2A34E76A11F43B52C21AB9
```

---

## Display Only the Full Hash

PowerShell may shorten long values in table output using:

```text
...
```

To display the complete hash:

```powershell
Get-FileHash .\big-treasure.txt |
    Select-Object -ExpandProperty Hash
```

A shorter equivalent is:

```powershell
(Get-FileHash .\big-treasure.txt).Hash
```

Both commands return only the complete hash value.

---

## Choose a Different Algorithm

The `-Algorithm` parameter allows a specific hashing algorithm to be selected.

### SHA-256

```powershell
Get-FileHash .\big-treasure.txt -Algorithm SHA256
```

### SHA-512

```powershell
Get-FileHash .\big-treasure.txt -Algorithm SHA512
```

### SHA-1

```powershell
Get-FileHash .\big-treasure.txt -Algorithm SHA1
```

### MD5

```powershell
Get-FileHash .\big-treasure.txt -Algorithm MD5
```

For modern integrity checks, SHA-256 or SHA-512 is generally preferred over older algorithms such as MD5 and SHA-1.

---

## Why the Algorithm Must Match

The same file produces different values when different algorithms are used.

Example:

```text
SHA256: 64 hexadecimal characters
SHA512: 128 hexadecimal characters
MD5:    32 hexadecimal characters
```

A SHA-256 hash cannot be directly compared with an MD5 hash.

Both the file and the algorithm must match.

---

## Compare a File Against an Expected Hash

Suppose a trusted source provides this expected hash:

```powershell
$ExpectedHash = "71FC5EC11C2497A32F8F08E61399687D90ABE6E204D2A34E76A11F43B52C21AB9"
```

Calculate the file's current hash:

```powershell
$ActualHash = (Get-FileHash .\big-treasure.txt).Hash
```

Compare them:

```powershell
$ActualHash -eq $ExpectedHash
```

Possible results:

```text
True
```

The hashes match.

```text
False
```

The hashes do not match.

---

## Complete Integrity Check

```powershell
$ExpectedHash = "EXPECTED_HASH_HERE"
$ActualHash = (Get-FileHash .\big-treasure.txt -Algorithm SHA256).Hash

if ($ActualHash -eq $ExpectedHash) {
    Write-Output "The file matches the expected hash."
}
else {
    Write-Output "Warning: The file hash does not match."
}
```

This creates a basic file-integrity verification process.

---

## Compare Two Files

Calculate the first file's hash:

```powershell
$Hash1 = (Get-FileHash .\file1.txt).Hash
```

Calculate the second file's hash:

```powershell
$Hash2 = (Get-FileHash .\file2.txt).Hash
```

Compare them:

```powershell
$Hash1 -eq $Hash2
```

If the result is:

```text
True
```

the files contain identical data according to the selected hashing algorithm.

If the result is:

```text
False
```

their contents differ.

---

## Hash Multiple Files

```powershell
Get-ChildItem -File |
    Get-FileHash
```

This calculates hashes for the files in the current directory.

To include files inside subfolders:

```powershell
Get-ChildItem -File -Recurse |
    Get-FileHash
```

This can be useful when creating an integrity record for a directory.

---

## Export Hash Results

```powershell
Get-ChildItem -File |
    Get-FileHash |
    Export-Csv .\file-hashes.csv -NoTypeInformation
```

This saves the results into:

```text
file-hashes.csv
```

The file can contain:

```text
Algorithm
Hash
Path
```

This creates a record that can later be used for comparison.

---

## Hashes Are Not Encryption

Hashing and encryption are different operations.

### Hashing

```text
File → Hash value
```

Hashing is designed to be one-way.

The original file cannot normally be reconstructed from its hash.

### Encryption

```text
Readable data → Encrypted data → Decryption → Readable data
```

Encryption is designed to be reversible with the correct key.

A hash verifies data. It does not hide or encrypt the data.

---

## Hashes Do Not Prove a File Is Safe

A matching hash confirms that the file matches another copy or an expected value.

It does not automatically prove that the file is harmless.

For example, a malicious file can still have a valid hash.

The hash must come from a trusted source for the comparison to be meaningful.

---

## Common Errors

### Incorrect Cmdlet

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

---

### File Not Found

Example:

```text
Cannot find path because it does not exist.
```

Confirm the current location:

```powershell
Get-Location
```

List the available files:

```powershell
Get-ChildItem -Force
```

Then verify the filename and path.

---

### Hash Appears Too Short

Example:

```text
71FC5EC11C2497A32F8F08E61399687D90ABE6E204D2...
```

The hash has not necessarily been calculated incorrectly.

PowerShell may only be shortening the displayed table value.

Use:

```powershell
(Get-FileHash .\big-treasure.txt).Hash
```

---

### Hashes Do Not Match

Possible reasons include:

- The file was modified
- The file was corrupted
- The wrong file was selected
- Different algorithms were used
- The expected hash was copied incorrectly
- Extra spaces or missing characters were included
- The trusted source published a different version of the file

---

## Complete Workflow

```powershell
Get-Location

Get-ChildItem -Force

Get-FileHash .\big-treasure.txt

(Get-FileHash .\big-treasure.txt).Hash

Get-FileHash .\big-treasure.txt -Algorithm SHA256
```

For comparison:

```powershell
$ExpectedHash = "EXPECTED_HASH_HERE"
$ActualHash = (Get-FileHash .\big-treasure.txt -Algorithm SHA256).Hash
$ActualHash -eq $ExpectedHash
```

---

## Key Lessons

- A file hash acts as a digital fingerprint.
- Identical files should produce identical hashes using the same algorithm.
- Changing a file changes its hash.
- `Get-FileHash` calculates file hashes in PowerShell.
- SHA-256 is the default algorithm.
- A SHA-256 hash contains 64 hexadecimal characters.
- `-Algorithm` selects a hashing algorithm.
- Both hashes must use the same algorithm before they can be compared.
- `Select-Object -ExpandProperty Hash` displays the complete hash value.
- `(Get-FileHash FileName).Hash` directly accesses the hash property.
- Hashes can help detect modification or corruption.
- Hashing is not the same as encryption.
- A matching hash does not automatically prove a file is safe.
- Expected hashes should come from a trusted source.
