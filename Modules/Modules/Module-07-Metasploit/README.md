# Module 07 — Metasploit

## What Is Metasploit?

Metasploit is a penetration-testing framework used to organize and run security testing modules against authorized targets.

Instead of manually building every part of an attack, Metasploit provides reusable modules for tasks such as:

- vulnerability checking
- exploitation
- payload delivery
- scanning
- post-exploitation

---

## Metasploit Modules

A module is a piece of code designed to perform a specific security-testing task.

Common module types include:

```text
exploit
auxiliary
payload
post
encoder
nop
```

### Exploit

An exploit module attempts to take advantage of a specific vulnerability.

```text
vulnerability
     ↓
exploit module
     ↓
attempt exploitation
```

### Auxiliary

Auxiliary modules perform supporting tasks that do not necessarily exploit a vulnerability.

Examples include:

```text
scanning
enumeration
service discovery
```

### Payload

A payload is the code that runs after successful exploitation.

Conceptually:

```text
Exploit = gets access
Payload = what runs after access is gained
```

---

## Selecting a Module

A Metasploit module can be selected with:

```text
use
```

Example structure:

```text
use exploit/...
```

After selecting a module, Metasploit changes context to that module.

---

## Viewing Required Options

Use:

```text
show options
```

This displays the settings required or available for the selected module.

Common options may include:

```text
RHOSTS
RPORT
LHOST
LPORT
```

---

## RHOSTS and LHOST

### RHOSTS

```text
RHOSTS = Remote Hosts
```

The target system or systems.

### LHOST

```text
LHOST = Local Host
```

The attack/testing machine that should receive a connection when required by the payload.

A simple way to remember it:

```text
R = Remote target
L = Local machine
```

---

## The `check` Command

Some exploit modules support:

```text
check
```

The `check` command tests whether the target appears vulnerable without proceeding directly into exploitation.

Conceptually:

```text
Target
  ↓
check
  ↓
Does the vulnerability appear to exist?
```

Not every Metasploit module supports `check`.

---

## The Exploitation Phase

Once the module is configured and the target is ready, exploitation can be started with:

```text
exploit
```

A common equivalent command is:

```text
run
```

For exploit modules, `exploit` clearly represents the transition into the exploitation phase.

---

## Basic Workflow

```text
Start Metasploit
      ↓
Search for module
      ↓
Select module
      ↓
View options
      ↓
Configure target/settings
      ↓
Check vulnerability if supported
      ↓
Run exploit
      ↓
Payload executes if successful
```

Example command flow:

```text
search
use
show options
set
check
exploit
```

---

## Important Distinction

Metasploit is the framework.

An exploit is one component inside that framework.

A payload is another component.

```text
Metasploit
    │
    ├── Exploit
    │      ↓
    │   gains access
    │
    └── Payload
           ↓
        runs after exploitation
```

---

## Key Takeaways

- Metasploit is a penetration-testing framework.
- Modules perform specific security-testing tasks.
- Exploit modules attempt to take advantage of vulnerabilities.
- Auxiliary modules perform tasks such as scanning and enumeration.
- Payloads execute after successful exploitation.
- `show options` displays module settings.
- `RHOSTS` refers to remote target hosts.
- `LHOST` refers to the local testing machine.
- `check` tests whether a target appears vulnerable when the module supports it.
- `exploit` proceeds with the exploitation phase.
