# 🖥️ Task 4 — Bash Scripting

**Platform:** TryHackMe | [tutedude-cybersec room](https://tryhackme.com/jr/tutedude-cybersec)

**Target Machine:** Ubuntu 24.04.4 LTS via SSH (`student@192.168.155.129`)

---

## 📁 Repository Structure

```
CyberSecurity-Task-(Bash Scripting)/
├── Bash_Scripting_Task.docx
├── 4. Bash Scripting.docx.md
├── screenshot.png
├── screenshot_1.png
├── screenshot_2.png
└── README.md
```

---

## 🎯 Objective

Write a Bash script to read the contents of a protected file (`secret.txt`) using `read_secret.sh` and print the output on screen.

---

## ❓ Question & Answer

| # | Question | Answer |
|---|----------|--------|
| 1 | Write a script to read `secret.txt`. What is inside it? | `flag{you_wrote_an_script}` |

---

## 🚩 Flag

```
flag{you_wrote_an_script}
```

---

## 📝 Bash Script Written

File: `read_secret.sh`

```bash
#!/bin/bash

FILE="secret.txt"

# 1. Error handling: Check if the file actually exists
if [ ! -f "$FILE" ]; then
    echo "Error: File '$FILE' does not exist in the current directory."
    exit 1
fi

# 2. Attempt to read the file into a variable, suppressing standard error output
secret=$(cat "$FILE" 2>/dev/null)

# 3. Error handling: Check if the previous command (cat) succeeded
if [ $? -ne 0 ]; then
    echo "Error: Permission denied. You do not have the rights to read '$FILE'."
    exit 1
fi

# 4. Print the value of the variable if successful
echo "The secret is: $secret"
```

---

## 💻 Commands Used

```bash
nano read_secret.sh         # Write the bash script
cat read_secret.sh          # Verify script content
chmod +x read_secret.sh     # Attempt execute permission (not permitted)
./run_secret secret.txt     # Execute via run_secret → flag captured
```

---

## 🔍 Security Analysis: Permissions & Privilege Escalation

### Why did `chmod +x` fail?
When trying to make the script executable (`chmod +x read_secret.sh`), it failed with a permission error. This typically happens for a few reasons in a locked-down CTF environment:
1. **Ownership Restrictions:** You can only change the permissions of a file if you are the owner or the root user. If the file was created in a restricted directory with enforced group ownership or a restrictive `umask`, you might not have the right to modify its execution bits.
2. **Mount Restrictions (`noexec`):** The filesystem or directory (like `/tmp`) might be mounted with the `noexec` flag, which prevents any file from being made executable or run directly.
3. **AppArmor / SELinux:** Advanced security modules might be configured to prevent standard users from executing arbitrary scripts.

### How did `run_secret` bypass permissions?
The file `secret.txt` is a **protected file**, meaning its read permissions are likely restricted to `root` or a specific admin user (e.g., `chmod 600 secret.txt`). A standard user cannot `cat` it directly. 

The `run_secret` executable bypassed this restriction because it is likely a **SUID (Set Owner User ID)** binary or runs via specific `sudo` rules. 
* When a binary has the SUID bit set (`chmod u+s`), it executes with the privileges of the file's owner (usually `root`), regardless of who runs it.
* Therefore, when we executed `./run_secret secret.txt`, the program temporarily assumed elevated privileges, successfully read the protected file, and returned the output to us.

### Alternative Escalation Methods
In a real-world scenario, if you encounter a protected file you need to read but lack a convenient SUID wrapper like `run_secret`, you would look for other **Privilege Escalation** vectors:
* **Misconfigured `sudo` rights:** Checking `sudo -l` to see if you can run commands like `cat`, `less`, `vim`, or `awk` as root without a password.
* **Exploiting other SUID binaries:** Finding other common binaries with the SUID bit set (`find / -perm -4000 2>/dev/null`) and using them to read files (e.g., `base64`, `tar`, `cp`).
* **Cron Jobs:** Finding a script that runs automatically as root, which is writable by your user, and injecting a `cat secret.txt > /tmp/flag` command into it.

---

## 📸 Screenshots

**Screenshot 1** — Full terminal workflow  
![Full Terminal Output](./screenshot.png)

**Screenshot 2** — Flag output  
![Flag Output](./screenshot_1.png)

**Screenshot 3** — Script content  
![Script Content](./screenshot_2.png)

---

## 🧰 Tools & Environment

- **OS:** Ubuntu 24.04.4 LTS
- **Access:** SSH via PowerShell
- **Platform:** TryHackMe
- **Editor:** nano

---

> Made with 🔥 by [YTxFSGAMERz](https://github.com/YTxFSGAMERz)
