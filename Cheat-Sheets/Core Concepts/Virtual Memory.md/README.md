# Virtual Memory

## Definition

Virtual memory is a memory management technique that allows the operating system to use storage on a hard drive or SSD as temporary memory when physical RAM becomes full.

---

## My First Thought

Virtual memory gives the illusion that my computer has more RAM than it physically does so it doesn't crash in panic when it runs out of memory.

---

## Refined Understanding

Virtual memory allows the operating system to temporarily move less frequently used data from RAM to storage, freeing up physical memory for active programs. This creates the illusion that more memory is available, allowing programs to continue running even when physical RAM is full.

---

## My Analogy

Imagine my desk is completely covered with papers.

Instead of throwing everything away, I move the papers I'm not currently using into a filing cabinet.

Whenever I need one of those papers again, I take it back out and put it on my desk.

RAM is the desk.

The SSD or hard drive is the filing cabinet.

Virtual memory manages moving papers back and forth so I can keep working.

---

## Real World Example

My computer has 8 GB of RAM.

I open Chrome, Discord, Spotify, FL Studio, Photoshop, and VS Code.

Instead of crashing when RAM fills up, Windows temporarily moves inactive data to the SSD or hard drive while keeping active programs in RAM. This allows me to continue working, although programs that have been moved may take longer to respond when I switch back to them.

---

## Where I've Seen This

- MIT 6.033
- Windows
- Operating Systems

---

## Why It Matters

Physical RAM is limited.

Virtual memory allows computers to run more programs than would otherwise fit into RAM by intelligently managing where data is stored. Although using storage is much slower than using RAM, virtual memory helps keep the system stable and prevents programs from crashing simply because memory is full.
