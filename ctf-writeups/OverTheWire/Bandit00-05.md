# 🚩 Bandit Level 00 → 01

## 📌 Problem Description
Connect to the Bandit server using SSH and retrieve the password for the next level.

---

## 💻 Solution

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
+
________________________________________
🧠 Explanation
The challenge introduces the use of SSH (Secure Shell) to connect to a remote machine.
We use the provided credentials (username: bandit0, port: 2220) to access the system.
________________________________________
📝 Summary
ssh bandit0@bandit.labs.overthewire.org -p 2220
The password to the level 01's box is boJ9jbbUNNfktd78OOpsqOltutMc3MY1
________________________________________


🚩 Bandit Level 01 → 02
📌 Problem Description
The password is stored in a file named -.
________________________________________
💻 Solution
cat ./-
________________________________________
🧠 Explanation
The filename - is treated as standard input (stdin) in Linux.
Using ./- ensures the shell treats it as a file in the current directory.
________________________________________
📝 Summary
cat ./-
________________________________________
The password to gain access to the level 02's box is CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9






🚩 Bandit Level 02 → 03
📌 Problem Description
The password is stored in a file with spaces in its name.
________________________________________
💻 Solution
cat "spaces in this filename"
________________________________________
🧠 Explanation
Spaces in filenames must be handled properly:
•	Use quotes " " 
•	OR escape spaces using \ 
________________________________________
📝 Summary
cat "spaces in this filename"
________________________________________
The password to gain access to the level 03's box is UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK






🚩 Bandit Level 03 → 04
📌 Problem Description
The password is stored in a hidden file inside a directory.
________________________________________
💻 Solution
ls -a
cat .hidden
________________________________________
🧠 Explanation
Hidden files start with . and are not shown with normal ls.
Using ls -a reveals hidden files.
________________________________________
📝 Summary
ls -a
cat .hidden
________________________________________




🚩 Bandit Level 04 → 05
📌 Problem Description
Find the only human-readable file among multiple files.
________________________________________
💻 Solution
file ./*
cat ./-file07
________________________________________
🧠 Explanation
The file command helps identify file types.
Only one file contains readable ASCII text — that’s the target.
________________________________________
📝 Summary
file ./*
cat ./-file07
________________________________________
🧠 Key Learnings
•	Handling special filenames (-, spaces) 
•	Working with hidden files 
•	File type identification using file 
•	Importance of enumeration 
________________________________________
🚀 Conclusion
This challenge demonstrates how fundamental Linux commands are used during reconnaissance and enumeration phases in VAPT. Mastering these basics builds a strong foundation for real-world penetration testing.


