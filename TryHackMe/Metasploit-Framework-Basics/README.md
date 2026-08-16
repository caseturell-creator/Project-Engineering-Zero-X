# Metasploit Framework

## Overview

Metasploit Framework is a security testing platform used to discover, test, and validate vulnerabilities during authorized security assessments.

Instead of manually building every scanner, exploit, or payload from scratch, Metasploit organizes security tools into reusable modules that can be configured and executed through a common interface.

The main idea is:

```text
Choose a module
      ↓
Configure it
      ↓
Test the target
      ↓
Analyze the result
```

---

## Starting Metasploit

Metasploit is normally started with:

```bash
msfconsole
```

After loading, the console displays a prompt similar to:

```text
msf6 >
```

This means commands are now being entered inside the Metasploit Framework console rather than directly into the normal Linux shell.

---

# Metasploit Modules

Metasploit contains different categories of modules.

```text
Metasploit
    |
    +-- exploit
    |
    +-- auxiliary
    |
    +-- payload
    |
    +-- post
```

Each category serves a different purpose.

---

## Exploit Modules

An exploit module contains code designed to take advantage of a specific vulnerability.

Conceptually:

```text
Target system
     ↓
Vulnerability exists
     ↓
Exploit module
     ↓
Vulnerability triggered
```

An exploit does not automatically mean full access will be obtained.

Its purpose is to trigger the weakness.

What happens afterward may depend on the payload.

---

## Auxiliary Modules

Auxiliary modules perform supporting security testing tasks.

These commonly include:

- Scanning
- Enumeration
- Service discovery
- Login testing
- Information gathering

Unlike exploit modules, auxiliary modules do not necessarily attempt to exploit a vulnerability.

Conceptually:

```text
Auxiliary Module
      ↓
Interact with service
      ↓
Collect information
```

---

## Payload Modules

A payload defines what Metasploit attempts to execute after an exploit successfully triggers a vulnerability.

A useful mental model is:

```text
Exploit = creates the opening

Payload = determines what happens through that opening
```

Example structure:

```text
Vulnerability
     ↓
Exploit
     ↓
Payload
     ↓
Result
```

The exploit and payload perform different jobs.

---

## Post Modules

Post modules are designed to be used after access to a system has already been obtained during an authorized assessment.

They can be used for tasks such as:

- Gathering system information
- Examining configuration
- Identifying users
- Performing additional security checks

Conceptually:

```text
Access obtained
      ↓
Post module
      ↓
Further analysis
```

---

# Searching for Modules

Metasploit contains many modules, so they are normally searched rather than memorized.

The basic command is:

```text
search <keyword>
```

Example:

```text
search ssh
```

This searches Metasploit's module database for modules related to SSH.

Search results can include information such as:

```text
Module name
Module type
Rank
Description
```

---

# Selecting a Module

A module can be selected using:

```text
use <module>
```

Example structure:

```text
use auxiliary/...
```

After selecting a module, the Metasploit prompt changes to show that the module is now active.

Conceptually:

```text
Metasploit
    ↓
Search
    ↓
Choose module
    ↓
use <module>
    ↓
Module becomes active
```

---

# Viewing Module Information

The `info` command displays detailed information about the currently selected module.

```text
info
```

Information may include:

- Module description
- Authors
- References
- Vulnerability information
- Available targets
- Required options

This is useful because it explains what the module is designed to do before it is executed.

---

# Viewing Module Options

The command:

```text
show options
```

displays the configurable parameters for the currently selected module.

Example options may include:

```text
RHOSTS
RPORT
LHOST
LPORT
```

Not every module uses all of these.

---

# RHOSTS

`RHOSTS` refers to the remote host or hosts that the module will interact with.

```text
RHOSTS
   ↓
Remote target
```

Example structure:

```text
set RHOSTS <target>
```

---

# RPORT

`RPORT` refers to the remote network port used by the service being tested.

Conceptually:

```text
Target machine
     ↓
RPORT
     ↓
Target service
```

For example, different services may listen on different ports.

---

# LHOST

`LHOST` refers to the local host address used by certain payload configurations.

```text
LHOST
   ↓
Local testing machine
```

It is commonly relevant when a payload needs to communicate back to the machine running Metasploit.

---

# LPORT

`LPORT` refers to a local port used by certain payloads.

Conceptually:

```text
Target
   ↓
Connection
   ↓
LHOST : LPORT
```

Like `LHOST`, this option is only relevant when required by the selected payload or module.

---

# Setting Options

Options are configured using:

```text
set <OPTION> <VALUE>
```

Example structure:

```text
set RHOSTS <target>
```

Another example:

```text
set RPORT <port>
```

The `set` command changes the value of an option inside the currently selected module.

Conceptually:

```text
Module
   ↓
Option
   ↓
set
   ↓
Configured value
```

---

# The `check` Command

Some Metasploit exploit modules support the command:

```text
check
```

The purpose of `check` is to determine whether the target appears vulnerable without actually running the full exploit.

Conceptually:

```text
Target
   ↓
check
   ↓
Module performs vulnerability test
   ↓
Possible result
```

Possible responses may indicate that the target:

```text
Appears vulnerable

Does not appear vulnerable

Could not be determined
```

Not every exploit module supports `check`.

---

# Why `check` Is Useful

Running an exploit immediately is not always necessary.

If supported, `check` provides a safer way to first determine whether the target appears affected by the vulnerability.

The workflow becomes:

```text
Select exploit
      ↓
Configure options
      ↓
check
      ↓
Evaluate result
      ↓
Decide whether further authorized testing is necessary
```

This separates:

```text
Testing for vulnerability
```

from:

```text
Actually attempting exploitation
```

---

# Running a Module

Modules are commonly executed using commands such as:

```text
run
```

or:

```text
exploit
```

The exact command and resulting behavior depend on the type of module being used.

Conceptually:

```text
Module selected
      ↓
Options configured
      ↓
Module executed
      ↓
Result returned
```

---

# Basic Metasploit Workflow

A simple Metasploit workflow looks like this:

```text
Start Metasploit
      ↓
Search for module
      ↓
Select module
      ↓
Read module information
      ↓
View options
      ↓
Configure required options
      ↓
Check target if supported
      ↓
Run authorized test
      ↓
Analyze output
```

Commands associated with this workflow include:

```text
msfconsole

search

use

info

show options

set

check

run

exploit
```

---

# Framework vs Tool

Metasploit is better understood as a framework rather than a single attack tool.

A normal command-line security tool may perform one specialized task.

Metasploit provides one environment containing many different modules.

```text
Traditional Tool

Program
   ↓
Specific task
```

Compared with:

```text
Metasploit Framework
        ↓
     Modules
        ↓
Different security testing tasks
```

This is why Metasploit is called a framework.

---

# Important Mental Model

Metasploit separates several parts of the security testing process.

```text
Module
  |
  +-- What technique is being used?
  |
  +-- What target is being tested?
  |
  +-- What configuration is required?
  |
  +-- What should happen if successful?
```

This separation allows the same interface to be used across many different security tests.

---

# Engineering Takeaway

The important skill is not memorizing every Metasploit command.

The important skill is understanding the workflow:

```text
What am I testing?

        ↓

Which module performs that test?

        ↓

What information does the module require?

        ↓

What does each option control?

        ↓

Can the vulnerability be checked first?

        ↓

What does the resulting output actually mean?
```

Metasploit is an abstraction layer over many different security testing techniques.

Understanding what the selected module is doing is more valuable than simply knowing which command to type.

---

# Key Commands

```text
msfconsole
```

Starts the Metasploit Framework console.

```text
search <keyword>
```

Searches for modules.

```text
use <module>
```

Selects a module.

```text
info
```

Displays detailed information about the selected module.

```text
show options
```

Displays configurable module options.

```text
set <OPTION> <VALUE>
```

Sets an option.

```text
check
```

Checks whether a target appears vulnerable when supported by the module.

```text
run
```

Runs the selected module.

```text
exploit
```

Executes an exploit module.

---

# Key Takeaway

```text
Metasploit is not the exploit.

Metasploit is the framework.

The module defines the technique.

The options define the configuration.

The target defines where the test occurs.

The output tells you what happened.
```
