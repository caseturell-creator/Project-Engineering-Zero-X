# Engineering Journal

**Date:** October 20, 2026

> Catch-up entry covering August 16 to October 20, 2026.

---

# Focus Since the Last Update

- TryHackMe SOC Level 1
- Linux and Ubuntu system administration
- Python
- KAGOME: from AI agent to custom desktop environment

---

# What I Accomplished

- Completed the TryHackMe SOC Level 1 learning path and earned the certificate.
- Started the TryHackMe Security Engineering learning path.
- Built KAGOME's AI agent with memory, session continuity, and shell tools.
- Turned the agent's failures into a custom Hyprland desktop environment that I now use daily.
- Planned my next portfolio projects, starting with the SOC Automation Engine.

---

# Biggest Realizations

## Tests Are Not Results

My agent passed 42 regression tests but still could not reliably finish complex tasks.

A passing test only proves what it actually checks.

---

## Verify Before Trusting

When fixing YouTube playback in KAGOME, I downloaded new tools from the internet.

Before running them, I verified each one against its published SHA256 checksum.

This connects directly to [PowerShell File Hashing and Integrity](../../Modules/Module-05-Command-Line-Tools/PowerShell-File-Hashing-and-Integrity/README.md).

---

## Rules Have Scope

Floating windows ignore the space reserved for the top bar.

That rule only applies to tiled windows.

Knowing where a rule applies matters as much as knowing the rule.

---

## AI Reports Are Claims

My AI tools reported passing tests and working fixes more than once when the real task still failed.

I learned to verify their claims the same way I verify any other evidence.

---

## Check If the Setting Exists

My terminal "ignored" the new theme.

It wasn't ignoring anything. The colour settings had never been written.

---

# Questions I Still Have

- How do Wayland compositors decide which window is on top?
- How does `sudo` safely read a password from a terminal?
- How do SOC teams automate alert triage without missing real threats?

---

# Engineering Quote of the Day

> "A test that passes on the wrong thing proves nothing."

---

# Reflection

These two months were about building, not just studying.

KAGOME forced me to troubleshoot real problems: windows, permissions, `PATH`, outdated packages, and downloads I had to verify.

The agent phase taught me that results matter more than reports.
