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

# Personal Realizations

These go beyond what I learned. They show how my thinking has changed.

---

## 1. Understanding a System Changes What I Can Learn

I can probably learn anything, as long as I understand the system.

Something being unfamiliar doesn't mean I can't do it.

Once I understand how a system works, its parts become easier to investigate, predict, and control.

---

## 2. Cybersecurity Gave My Thinking Structure

I was already analyzing behaviour, anticipating outcomes, and spotting patterns before I studied cybersecurity.

Cybersecurity didn't create that.

It's teaching me to turn those instincts into repeatable methods backed by evidence, technical knowledge, and verification.

---

## 3. Evidence Beats a Convincing Explanation

My process has become:

Evidence

↓

Hypothesis

↓

Test

↓

Conclusion

Something making logical sense doesn't make it true.

Even a strong prediction needs evidence, especially when investigating a security incident.

---

## 4. An Indicator Is Not a Conclusion

During SOC investigations, I saw activity that looked suspicious until more context explained it.

Spotting an anomaly and proving malicious intent are two different jobs.

A good analyst doesn't just recognize suspicious behaviour. They investigate what it actually means.

---

## 5. Understanding an Adversary Means Understanding Their Reasoning

I can't fully anticipate someone's actions by only studying what they did.

I need to understand why they thought those actions were reasonable or worth it.

In cybersecurity, that becomes threat modelling: anticipating attacker behaviour and finding weaknesses before they're exploited.

Understanding someone's reasoning is not the same as agreeing with it.

---

## 6. Security Is Not Just a Checklist

In a hospital vulnerability scenario, the technically ideal security fix would have caused unacceptable problems for critical services.

I chose to keep those services running while temporarily reducing exposure.

Security engineering means weighing the consequences of a decision, not just following a procedure.

---

## 7. Recognizing Repeated Failure Is Debugging

While building my AI projects, generating code and testing it over and over wasn't enough.

I identified the failures that kept coming back, questioned approaches that weren't fixing them, and changed direction.

Engineering means finding out why a solution keeps failing, not just producing another one.

---

## 8. Tools Get Less Impressive as I Understand What's Beneath Them

Kali Linux started to feel almost like a toy compared with what I was building on Ubuntu.

As terminals, Linux, scripting, and system architecture became familiar, individual tools stopped feeling mysterious.

I started thinking about building capabilities instead of only using prebuilt ones.

---

## 9. Documenting My Learning Might Be Teaching It

Project Engineering Zero X is becoming almost a course, written as I learn.

Breaking subjects down until I genuinely understand them could help someone starting from absolutely nothing.

That turns this repository from a collection of notes into a record of how someone can teach themselves technical subjects.

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

Three ideas are becoming the foundation of Project Engineering Zero X:

- **Understanding over memorization:** learning the underlying system creates knowledge that transfers to other technologies.
- **Evidence over assumption:** intuition produces hypotheses. Investigation decides whether they're correct.
- **Engineering over tool dependency:** understanding failure, architecture, and consequences matters more than knowing which commands to run.

I started by trying to understand what computers do.

Now I'm asking why systems were designed the way they were, where they can fail, and how I would build them differently.

That's the shift from learning technology to engineering it.
