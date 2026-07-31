# Case Study - Recovering a Windows Boot Failure

## Objective

Recover an Acer Nitro 5 that could no longer boot normally without resetting the PC, reinstalling Windows, or deleting personal files and installed programs.

---

## The Problem

The laptop was experiencing several Windows problems:

- White screen after login
- Critical Start menu errors
- Chrome errors
- Windows components failing to load
- Automatic Repair loop
- Startup Repair unable to repair the PC

Startup Repair displayed:

```text
Startup Repair couldn't repair your PC
```

It also referenced this log file:

```text
D:\WINDOWS\System32\Logfiles\Srt\SrtTrail.txt
```

---

## Initial Observation

The Command Prompt opened inside the Windows Recovery Environment on the `X:` drive.

```text
X:\Windows\System32
```

The `X:` drive was not the laptop’s normal Windows installation. It was the temporary recovery environment.

Before running any repairs, I needed to locate the actual Windows partition.

---

## Investigation

### Step 1 - Check the C: Drive

I switched to the `C:` drive and listed its contents:

```cmd
C:
dir
```

The volume was labelled `Data` and did not contain the normal Windows directories.

This showed that `C:` was not the Windows partition inside the recovery environment.

---

### Step 2 - Check the D: Drive

I then checked the `D:` drive:

```cmd
D:
dir
```

The following directories appeared:

```text
Program Files
Program Files (x86)
Users
Windows
```

This confirmed that the Windows installation was located on `D:`.

Recovery mode can assign different drive letters than normal Windows, so verifying the correct partition was necessary before running repair commands.

---

### Step 3 - Check the File System and Drive

I ran:

```cmd
chkdsk D: /f /r
```

The options mean:

- `/f` repairs file-system errors.
- `/r` searches for bad sectors, attempts to recover readable data, and marks damaged areas so Windows avoids using them again.

CHKDSK discovered and replaced bad clusters in user files, including:

- A game file
- An FL Studio project file

This proved that the drive contained actual damaged storage areas or file-system corruption.

CHKDSK also displayed:

```text
Failed to transfer logged messages to the event log with status 6.
```

Because the command was running from the Windows Recovery Environment, it could not transfer the results into the normal Windows Event Log. This did not prevent the disk repair from completing.

---

### Step 4 - Repair Windows System Files

After CHKDSK completed, I ran System File Checker against the offline Windows installation:

```cmd
sfc /scannow /offbootdir=D:\ /offwindir=D:\Windows
```

The first attempt displayed the SFC help screen because `/offbootdir` was typed without the opening `/`.

After correcting the command, SFC completed successfully and reported:

```text
Windows Resource Protection found corrupt files and successfully repaired them.
```

This confirmed that protected Windows system files had also been corrupted.

---

## Root Cause

The evidence pointed to a combination of:

- File-system corruption
- Bad disk clusters
- Corrupted Windows system files

The exact event that originally caused the corruption was not confirmed.

Possible causes include:

- An improper shutdown
- Previous disk errors
- A storage drive beginning to degrade

---

## Resolution

The recovery sequence was:

```text
Identify Windows partition
        ↓
Repair file system with CHKDSK
        ↓
Repair Windows files with offline SFC
        ↓
Boot into Windows
        ↓
Perform a clean restart
        ↓
Full Windows functionality restored
```

The repairs made Windows bootable again.

However, the recovery was not completely finished during the first successful Windows session. Some components were still not functioning normally.

After performing a clean restart:

- The Start menu returned.
- Chrome worked again.
- The white-screen problem stopped.
- Windows components loaded normally.
- The laptop returned to full general operation.

The clean restart was an essential final step because it allowed Windows services, drivers, caches, and repaired system components to initialize from a clean state.

---

## Result

The laptop was successfully recovered without:

- Resetting the PC
- Reinstalling Windows
- Deleting personal files
- Removing installed applications

Windows became bootable and the previously broken Windows components returned to normal operation.

---

## Commands Used

```cmd
C:
dir

D:
dir

chkdsk D: /f /r

sfc /scannow /offbootdir=D:\ /offwindir=D:\Windows

exit
```

> These commands were specific to this recovery. Windows was confirmed to be on `D:` before any repair commands were executed.

---

## Lessons Learned

- Windows Recovery may assign different drive letters than normal Windows.
- Never assume which partition contains Windows.
- Verify the Windows directory before running offline repairs.
- A failed Startup Repair does not automatically mean Windows needs to be reinstalled.
- CHKDSK and SFC repair different layers of the system.
- CHKDSK repairs the file system and damaged disk areas.
- SFC repairs protected Windows system files.
- Command syntax matters. One missing `/` caused SFC to display its help screen instead of running.
- A successful boot does not always mean the recovery is completely finished.
- A clean restart may be required before all repaired Windows components function normally.
- The original symptoms should be tested again to confirm the repair.
- Bad clusters are a warning that important files should be backed up and the drive should be monitored.

---

## Final Status

**Windows boot failure: Resolved**

The laptop successfully boots, the Start menu works, Chrome works, and the previous Windows errors have stopped.
