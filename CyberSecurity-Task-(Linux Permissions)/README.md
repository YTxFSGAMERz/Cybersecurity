# 🔐 Task 2 — Linux Permissions

**Platform:** TryHackMe | [tutedude-cybersec room](https://tryhackme.com/jr/tutedude-cybersec)

**Target Machine:** Ubuntu 24.04.4 LTS via SSH (`student@192.168.155.129`)

---

## 📁 Repository Structure

```
CyberSecurity-Task-(Linux Permissions)/
├── Linux_Permissions_Task.docx
├── 2. Linux Permissions.docx.md
├── screenshot.png
└── README.md
```

## 🎯 Objective

Understand how permissions work in Linux and read the content of `/home/student/practice/restricted_file.txt`

---

## 🚩 Flag

```
flag{you_understood_permissions}
```

---

## 💻 Commands Used

```bash
ls -la                        # List files with permissions
cd practice                   # Navigate to practice directory
ls -l restricted_file.txt     # Check the initial permissions of the file
chmod u+r restricted_file.txt # Add read permission for the user/owner
cat restricted_file.txt       # Read the restricted file successfully
```

---

## 📸 Output Screenshot

![Linux Permissions Output](./screenshot.png)

---

## 📖 Understanding Linux Permissions

### The Permission Model
Linux file permissions are based on the `rwx` model and apply to three categories of users:
1. **User (u)**: The owner of the file.
2. **Group (g)**: Users who belong to the file's group.
3. **Other (o)**: Everyone else on the system.

For each category, three types of access can be granted or denied:
* `r` (Read): Permission to read the contents of the file.
* `w` (Write): Permission to modify or delete the file.
* `x` (Execute): Permission to run the file as a program.

When you run `ls -l`, you see a 10-character string representing these permissions, like `-rw-r--r--`.
* The first character indicates the file type (`-` for regular file, `d` for directory).
* The next 3 characters (`rw-`) are the **User** permissions.
* The next 3 characters (`r--`) are the **Group** permissions.
* The last 3 characters (`r--`) are the **Other** permissions.

### Task Analysis: The Restricted File
In this task, the file `/home/student/practice/restricted_file.txt` was restricted to prevent reading. 

**Initial State:** Without the `r` (read) permission bit explicitly set for our user, attempting to use `cat restricted_file.txt` resulted in a "Permission denied" error. The operating system's access control strictly prevents reading the file's contents, even if you are the owner, because the read permission was revoked.

**Modifying Permissions:** 
Since we are the owner of the file (or running as a user with sufficient privileges), we can modify the permissions using the `chmod` (change mode) command.

To read the file, we must grant ourselves read access. The command `chmod u+r restricted_file.txt` was used:
* `u` stands for "user" (the owner).
* `+` stands for "add permission".
* `r` stands for "read".

By running this command, the permission bits were updated to include read access for the owner (e.g., modifying it from something like `---------` or `--w-------` to `-r--------` or `-rw-------`). This change successfully satisfies the system's access control checks, allowing the `cat` command to read and display the flag.

---

> Made with 🔥 by [YTxFSGAMERz](https://github.com/YTxFSGAMERz)
