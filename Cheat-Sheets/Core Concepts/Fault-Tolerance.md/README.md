# Fault Tolerance

## Definition

Fault tolerance is the ability of a system to continue operating even when one or more of its components fail.

---

## My First Thought

Fault tolerance is like a safety net.

If one part of the system fails, there's another part ready to keep everything running.

---

## Refined Understanding

Fault tolerance means designing a system to expect failures. Instead of crashing when something breaks, the system continues operating by relying on backups, redundancy, or alternative components.

---

## My Analogy

Imagine a circus with a safety net.

If someone falls, the performance doesn't end because the safety net catches them.

Fault tolerance works the same way. It provides a backup so one failure doesn't bring down the entire system.

---

## Real World Example

DNS uses many servers around the world.

If one DNS server goes offline due to a power outage, hardware failure, or network issue, another DNS server can answer the request, allowing the Internet to continue functioning.

---

## Where I've Seen This

- MIT 6.033
- DNS
- Internet infrastructure

---

## Why It Matters

Failures are inevitable.

Hardware breaks.

Power goes out.

Networks fail.

Good engineers assume failures will happen and design systems that continue operating instead of collapsing.
