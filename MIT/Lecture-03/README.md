# MIT 6.033 - Lecture 3: Naming

**Date:** June 30, 2026

---

# 1. The Problem

What problem were engineers trying to solve?

People are bad at remembering numerical IP addresses, while computers require them to communicate. As the Internet grew, engineers needed a way for humans to use simple names while allowing computers to continue using IP addresses.

---

# 2. The Big Idea

DNS translates human-friendly names into IP addresses so computers know where to send data.

---

# 3. How It Works

(To be completed as we continue reading.)

---

# 4. Real World Examples

Google can move from one server to another without users knowing.

Yesterday:

google.com → Server A

Today:

google.com → Server B

Users still type "google.com."

DNS quietly finds Google's new location.

---

# 5. Tony's Analogy

I imagine the Internet like a giant digital world.

An IP address is like the address of a house.

DNS is like GPS or my phone contacts.

Google may move to another house tomorrow, but I never need to know where it moved because I keep typing "google.com" and DNS finds its new address.

---

# 6. Connections

Linux
- File paths are names.

Windows
- C:\Windows is a name.

Networking
- IP addresses identify destinations.

TryHackMe
- SSH uses hostnames or IP addresses to reach another machine.

---

# 7. Engineering Insights

### Insight #1

DNS separates identity from location.

Names stay the same.

Locations can change.

---

# 8. Questions

- Why are root servers necessary?
- Why can't one DNS server handle everything?
- How does DNS verify that answers are legitimate?

---

# 9. My Explanation

DNS exists because humans are bad at remembering IP addresses. It lets people use names while computers continue communicating with numerical addresses. DNS also allows websites and services to move between servers without users needing to know where they moved.
