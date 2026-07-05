# 🌳 Root Cause Analysis

## What is Root Cause Analysis?

Root Cause Analysis (RCA) is the process of finding the **actual cause** of a problem instead of only fixing its symptoms.

Good engineers solve causes.

Great engineers prevent them from happening again.

---

## Symptom vs Root Cause

### Symptom

What you notice.

Examples:

- Website is slow.
- Computer won't boot.
- User cannot log in.
- Program crashes.

### Root Cause

The underlying reason the symptom exists.

Examples:

- Database query is inefficient.
- Hard drive has failed.
- Account permissions are incorrect.
- Memory leak causes the crash.

---

## The Five Whys

Keep asking "Why?" until you reach the real cause.

Example:

Website is slow.

↓

Why?

Database is overloaded.

↓

Why?

A query is taking too long.

↓

Why?

The query isn't indexed.

↓

Why?

The new table was deployed without indexes.

↓

Root Cause:
Deployment process missed a required database optimization.

---

## Fix vs Prevention

Fix:
Restart the server.

Prevention:
Improve monitoring, indexing, testing, and deployment procedures.

---

## Engineering Checklist

☐ What happened?

☐ What evidence supports it?

☐ What assumptions am I making?

☐ What caused the issue?

☐ How can I prove it?

☐ How do we prevent it from happening again?

---

## Zero X Principle

Never stop at the symptom.

Find the root.
