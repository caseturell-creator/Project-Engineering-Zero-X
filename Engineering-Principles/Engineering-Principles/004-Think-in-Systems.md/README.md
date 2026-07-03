# Engineering Principle #004 - Think in Systems

## The Principle

Every computer system is made of smaller systems working together.

Never study a component in isolation.

Always ask what it connects to.

---

## What I Learned

While learning about virtual machines, I realized they are only one part of a larger system.

A virtual machine depends on:

- Physical Hardware
- Hypervisor
- Operating System
- Applications
- Network
- Storage

Every layer depends on the one below it.

---

## Engineering Questions

Whenever I learn something new, I should ask:

- What is above it?
- What is below it?
- What does it communicate with?
- What depends on it?
- What does it depend on?

---

## Example

Application

↓

Operating System

↓

Hypervisor

↓

Physical Hardware

Each layer provides services to the layer above it.

---

## Engineering Takeaway

Engineers don't see isolated parts.

They see connected systems.
