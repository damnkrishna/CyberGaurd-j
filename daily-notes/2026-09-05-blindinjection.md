# PortSwigger SQL Injection Labs — Notes

## Lab 1: Blind SQL Injection with Conditional Errors

**Level:** Practitioner
**Status:** Solved 

### Description

This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics and includes the value of that cookie in a SQL query. The results of the query are not returned to the user, and the application does not behave differently depending on whether the query returns rows. However, if the query causes a database error, the application returns a custom error message — and that's the oracle we exploit.

The database contains a `users` table with `username` and `password` columns. The goal is to exploit the blind SQL injection to extract the administrator's password and log in as them.

### Hint

This lab uses an **Oracle database**. See the [SQL injection cheat sheet](https://portswigger.net/web-security/sql-injection/cheat-sheet) for Oracle-specific syntax.

### Key Cookie

```
Cookie: TrackingId=bgL0TNQcHbUbpoEl; session=OJyMKFgDnQIjKNyiprdZYlrjn2d6I0es
```

### Approach

I wanted to understand the manual exploitation process myself before reaching for sqlmap — solving it by hand first, then verifying with automated tooling, was the goal.

The general manual method for conditional-error-based blind SQLi:

1. Send the `TrackingId` cookie value through Burp Repeater.
2. Inject a payload that triggers an error only when a condition is false (e.g. using `CASE WHEN ... THEN ... ELSE ... END` with a deliberate divide-by-zero or type-conversion error in Oracle).
3. Use this conditional error to test hypotheses one bit/character at a time:
   - Confirm the `users` table exists.
   - Confirm a row exists where `username = 'administrator'`.
   - Extract the password length.
   - Extract the password character-by-character using `SUBSTR()` and comparison operators.
4. Once the full password is recovered, log in as `administrator`.

**Result:** Solved successfully after working through it manually.

---

## Lab 2: Blind SQL Injection with Time Delays

**Level:** Practitioner
**Status:** In progress 🔄

### Initial Observations

- The input appears to be **reflected in the output**, which initially made me suspect this might just be a printing/reflection issue rather than a genuine database-backed injection point.
- Screenshots taken during testing:
  - ![Screenshot 1](https://github.com/user-attachments/assets/092a0048-fda5-489a-a3a8-abad71bf5172)
  - ![Screenshot 2](https://github.com/user-attachments/assets/ea693c9c-2f26-4aa3-abc8-56b2cf48c55c)

### Approach

- **sqlmap did not solve this lab automatically** — it failed to detect/exploit the injection point.
- Had to solve it **manually using Burp Intruder** to extract the administrator's password.
- The specific injection commands and syntax needed weren't things I was already familiar with, so this required more research and trial and error than the first lab.

### Takeaway

Going through these labs is changing my perception of SQL injection — it's more approachable than I originally thought, as long as you understand:
- How to use conditional logic (errors, boolean responses, or time delays) as an oracle when there's no direct output.
- Database-specific syntax quirks (Oracle vs MySQL vs others).
- How to iterate efficiently with Burp Intruder when automated tools like sqlmap fall short.

---

## General Notes for Future Labs

- Always try to solve manually first via Burp Repeater/Intruder before relying on sqlmap — it builds real understanding of *why* the payload works.
- Keep a cheat sheet of DB-specific syntax (Oracle, MySQL, PostgreSQL, MSSQL) handy, since payloads differ significantly between them.
- When sqlmap fails, it's often due to non-standard injection contexts (cookies, custom headers, unusual response behavior) — manual testing is more reliable in those cases.
