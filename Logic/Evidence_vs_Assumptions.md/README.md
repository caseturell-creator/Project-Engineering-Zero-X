
# 🔍 Evidence vs Assumptions

## Why This Matters

Engineers, cybersecurity analysts, and developers make better decisions by separating what they **know** from what they **think**.

Poor decisions often happen when assumptions are mistaken for facts.

---

## Evidence

Evidence is information that can be observed, measured, verified, or reproduced.

Examples:

- An error appears in the logs.
- The server CPU is at 100%.
- The website returns HTTP 500.
- A packet capture shows dropped packets.

---

## Assumptions

Assumptions are explanations that have not yet been proven.

Examples:

- "The server must have crashed."
- "It's probably DNS."
- "Someone hacked us."
- "The database is broken."

---

## Engineering Rule

Evidence ➜ Hypothesis ➜ Test ➜ Conclusion

Never skip directly from evidence to conclusion.

---

## Real Example

Evidence:
- Users report the website is slow.
- CPU usage is normal.
- Database response time increased after a deployment.

Hypothesis:
- The new deployment introduced an inefficient database query.

Test:
- Roll back the deployment or profile the queries.

Conclusion:
- Accept or reject the hypothesis based on the results.

---

## Zero X Principle

Collect evidence before creating explanations.

Evidence beats assumptions.
