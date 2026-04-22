# Filesystem

## Room Metadata
* **Platform:** [TryHackMe](https://tryhackme.com)
* **Category:** Linux / Blue Team
* **Room:** [Linux Fundamentals](https://tryhackme.com/room/linuxfundamentalspart1)
* **Difficulty:** Easy
* **Status:** `Completed`

## Objective
Mastering essential Linux terminal commands for directory navigation and file viewing.

## Tools Used
- **Linux**
- **ls** - list directory contents
- **cd** - change the directory
- **cat** - concatenate and display file content
- **pwd** - print working directory

## Methodology
1. **Directory Reconnaissance:** Identify the initial directory structure and contents using `ls`.
2. **Navigation:** Use `cd` to move between directories based on requirements.
3. **Path Verification:** Confirm current directory with `pwd` before extracting or viewing files.
4. **Data Extraction:** Utilize `cat` to view file contents and understand structure.

## Key Findings
- **Hidden Data:** Often, important files are hidden; use `ls -a` to view them.
- **Absolute vs Relative Paths:** Understanding the difference is crucial for efficient navigation.
- **Efficiency:** Proper CLI command usage significantly reduces time for navigation and data retrieval.

## Reflection
Real-world CLI navigation skills are critical for Red Team and VAPT engagements. Proficiency in command-line tools enhances the ability to perform reconnaissance, enumeration, and exploitation efficiently. It allows security testers to interact directly with target systems, automate tasks, and identify vulnerabilities more effectively during penetration testing activities.
