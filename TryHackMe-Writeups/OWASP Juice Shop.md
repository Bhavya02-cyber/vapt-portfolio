# TryHackMe — OWASP Juice Shop

- Category: OWASP Top 10 / Injection  
- Status: ✅ Completed

---

## Task 1 — Open for Business

- Juice Shop is a large vulnerable web application used to practice OWASP Top 10 vulnerabilities.

- Machine deployed and accessed through browser.

- Answer:
  - No answer needed

---

## Task 2 — Let’s Go on an Adventure

- Before attacking, perform reconnaissance by browsing the application.

- Burp Proxy was used to observe requests.

- While browsing products, a review by admin revealed the administrator email.

- Question:
  - What’s the Administrator’s email address?

- Answer:
  - admin@juice-sh.op

---

### Search Feature

- Click the search icon.

- The URL updates:

  ```
  /#/search?q=
  ```

- Question:
  - What parameter is used for searching?

- Answer:
  ```
  q
  ```
---

### Product Review Clue

- User Jim mentioned a **replicator** in his review.

- Research revealed this reference belongs to a famous TV show.

- Question:
  - What show does Jim reference?

- Answer:

  - Star Trek

---

## Task 3 — Inject the Juice

- Injection vulnerabilities allow attackers to interfere with database queries.

- Common types include:

  - SQL Injection
  - Command Injection
  - Email Injection

- In this challenge we perform **SQL Injection**.

---

### SQL Injection Login Bypass

- Payload example:

  ```

  ' OR 1=1 --

  ```

- Explanation:

  ```
  '  closes the SQL string
  OR  returns true
  1=1 always evaluates to true
  -- comments out remaining query
  ```

- This causes authentication bypass.

---

### Result

- Logged in as administrator.

- Flag obtained:

```

32a5e0f21372bcc1000a6088b93b458e41f0e02a

```

---

## Key Takeaways

- Injection vulnerabilities occur when user input reaches interpreters.

- Typical targets:

  ```
  SQL databases
  Operating system commands
  LDAP queries
  XML parsers
  ```

- SQL injection allows attackers to:

  ```
  Bypass authentication
  Dump database contents
  Modify or delete data
  ```
