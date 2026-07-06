<div align="center">

# 🐧 Linux Essentials

![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Bash](https://img.shields.io/badge/Bash-4EAA25?style=for-the-badge&logo=gnubash&logoColor=white)
![Level](https://img.shields.io/badge/Level-Beginner%20to%20Intermediate-brightgreen?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Interview%20Ready-blue?style=for-the-badge)

**A simple, beginner-friendly guide to understand Linux and answer interview questions with confidence**

</div>

---

## 📖 Table of Contents

1. [What is Linux](#-what-is-linux)
2. [Linux Distributions](#-linux-distributions)
3. [Linux File System Structure](#-linux-file-system-structure)
4. [Basic Navigation Commands](#-basic-navigation-commands)
5. [File and Directory Operations](#-file-and-directory-operations)
6. [Viewing and Editing Files](#-viewing-and-editing-files)
7. [File Permissions](#-file-permissions)
8. [Users and Groups](#-users-and-groups)
9. [Process Management](#-process-management)
10. [Package Management](#-package-management)
11. [Environment Variables](#-environment-variables)
12. [Piping and Redirection](#-piping-and-redirection)
13. [Searching with grep and find](#-searching-with-grep-and-find)
14. [Networking Commands](#-networking-commands)
15. [Disk and Storage](#-disk-and-storage)
16. [Compression and Archiving](#-compression-and-archiving)
17. [Shell Scripting Basics](#-shell-scripting-basics)
18. [Cron Jobs (Scheduling Tasks)](#-cron-jobs-scheduling-tasks)
19. [SSH and Remote Access](#-ssh-and-remote-access)
20. [System Monitoring](#-system-monitoring)
21. [Security Basics](#-security-basics)
22. [Common Interview Questions](#-common-interview-questions-spoken-style-answers)
23. [Quick Cheat Sheet](#-quick-cheat-sheet)

---

## 🐧 What is Linux

Linux is an open source operating system kernel that powers everything from servers and cloud infrastructure to smartphones and embedded devices. It is known for being stable, secure, and highly customizable, which is why most of the internet actually runs on Linux servers.

**Spoken answer:** I would describe Linux as the operating system that sits underneath most servers and cloud environments today. It's open source, which means anyone can view and modify the code, and it's built around a strong permission system and a powerful command line, which gives developers a lot of control over the machine.

---

## 📦 Linux Distributions

| Distribution | Common Use Case |
|---|---|
| Ubuntu | General use, beginner friendly, widely used on servers |
| Debian | Stable, used as a base for other distros |
| CentOS / Rocky Linux | Enterprise servers |
| Fedora | Cutting edge features, used by developers |
| Alpine | Lightweight, common in Docker containers |

**Spoken answer:** A distribution, or distro, is basically a version of Linux packaged together with a specific set of tools, package manager, and defaults. I usually work with Ubuntu for general development and Alpine for Docker images because of how small and lightweight it is.

---

## 🗂️ Linux File System Structure

```
/
├── bin      → essential command binaries
├── etc      → configuration files
├── home     → user personal directories
├── var      → logs, variable data
├── usr      → user installed programs
├── tmp      → temporary files
├── root     → home directory for root user
```

**Spoken answer:** Linux organizes everything under a single root directory represented by a forward slash. Unlike Windows, there are no separate drive letters, everything, including external drives, gets mounted somewhere under that root structure. Configuration files live in `/etc`, user files live in `/home`, and logs usually live in `/var/log`.

---

## 🧭 Basic Navigation Commands

```bash
pwd              # print current directory
ls                # list files
ls -la            # list all files with details
cd /path/to/dir   # change directory
cd ..             # go up one directory
cd ~              # go to home directory
```

**Spoken answer:** These are the commands I use constantly just to move around. `pwd` tells me where I currently am, `ls` lists what's in the folder, and `cd` changes my location. Adding `-la` to `ls` shows hidden files and details like permissions and file size.

---

## 📁 File and Directory Operations

```bash
mkdir new_folder        # create a directory
touch file.txt          # create an empty file
cp file.txt backup.txt  # copy a file
mv file.txt folder/     # move or rename a file
rm file.txt             # delete a file
rm -r folder/           # delete a folder and its contents
```

**Spoken answer:** These commands handle basic file management. `cp` copies, `mv` both moves and renames depending on how I use it, and `rm` deletes. I'm always careful with `rm -r`, especially with `-f` added, because Linux does not ask for confirmation and deleted files don't go to a recycle bin.

---

## 📄 Viewing and Editing Files

```bash
cat file.txt      # print whole file
less file.txt     # scroll through file
head -n 10 file.txt   # first 10 lines
tail -n 10 file.txt   # last 10 lines
tail -f app.log       # follow a file live, great for logs
nano file.txt         # simple terminal editor
vim file.txt          # powerful terminal editor
```

**Spoken answer:** `cat` is good for small files, but for anything large I use `less` since it lets me scroll without loading the whole thing into the terminal. `tail -f` is something I use almost daily when debugging, since it shows new lines being added to a log file in real time.

---

## 🔐 File Permissions

```bash
ls -l file.txt
# -rwxr-xr--  1 haseeb  staff  120 Jul 6 file.txt

chmod 755 file.txt     # change permissions
chmod +x script.sh     # make a file executable
chown haseeb:staff file.txt   # change owner and group
```

**Spoken answer:** Every file in Linux has permissions for three groups, the owner, the group, and everyone else, each with read, write, and execute rights. The numbers in `chmod 755` represent those permissions in octal, where 7 means read, write, and execute, and 5 means read and execute only. `chown` changes who owns the file.

---

## 👥 Users and Groups

```bash
whoami                  # current user
sudo adduser newuser    # create a new user
sudo usermod -aG sudo newuser   # add user to sudo group
groups                  # show groups for current user
```

**Spoken answer:** Linux is a multi-user system by design, so every file and process belongs to a specific user and group. `sudo` lets a permitted user run a command with elevated, administrator level privileges, which is safer than always being logged in directly as the root user.

---

## ⚙️ Process Management

```bash
ps aux              # list running processes
top                 # live view of processes and resource usage
htop                # improved, interactive version of top
kill 1234           # stop a process by its ID
kill -9 1234        # force kill a process
```

**Spoken answer:** `ps aux` gives me a snapshot of every running process along with its process ID, which I need if something is stuck and I want to kill it. `top` and `htop` give me a live, constantly updating view, which is useful when I'm trying to figure out what is using too much CPU or memory.

---

## 📦 Package Management

```bash
# Debian / Ubuntu
sudo apt update
sudo apt install nginx
sudo apt remove nginx

# CentOS / RHEL
sudo yum install nginx

# Fedora
sudo dnf install nginx
```

**Spoken answer:** Package managers handle installing, updating, and removing software along with their dependencies automatically. Different distributions use different tools, `apt` for Debian based systems like Ubuntu, and `yum` or `dnf` for Red Hat based systems like CentOS or Fedora.

---

## 🌍 Environment Variables

```bash
echo $HOME
export MY_VAR="hello"
echo $MY_VAR
printenv
```

**Spoken answer:** Environment variables store configuration values that programs can access, like the current user's home directory or an API key. `export` sets a variable for the current session, and I usually add permanent ones to a file like `.bashrc` or `.env` so they persist across sessions.

---

## 🔗 Piping and Redirection

```bash
ls -l | grep ".txt"       # pipe output into another command
command > output.txt      # redirect output to a file, overwrite
command >> output.txt     # redirect output to a file, append
command 2> error.txt      # redirect only error output
```

**Spoken answer:** A pipe, written as a vertical bar, takes the output of one command and feeds it as input to another, which lets me chain small commands together to do something powerful. Redirection with `>` or `>>` sends output into a file instead of printing it to the screen.

---

## 🔍 Searching with grep and find

```bash
grep "error" app.log             # search for a word in a file
grep -r "TODO" ./src             # search recursively in a folder
find . -name "*.py"              # find files by name
find . -type d -name "node_modules"  # find directories by name
```

**Spoken answer:** `grep` searches through file content for a pattern, which I use constantly when digging through log files for errors. `find` searches for files and directories themselves based on name, type, or other properties, which is different from `grep`, which searches inside the files.

---

## 🌐 Networking Commands

```bash
ping google.com          # check connectivity
curl https://api.site.com   # make an HTTP request
wget https://file.url/file.zip  # download a file
netstat -tulpn           # show open ports and listening services
ifconfig / ip a          # show network interfaces
```

**Spoken answer:** `ping` checks if a server is reachable, `curl` lets me test an API directly from the terminal, and `netstat` or `ss` shows me which ports are open and what is listening on them, which is very useful when debugging why a service isn't reachable.

---

## 💽 Disk and Storage

```bash
df -h        # show disk space usage
du -sh folder/   # show size of a folder
mount /dev/sdb1 /mnt/data   # mount a drive
lsblk        # list block devices
```

**Spoken answer:** `df -h` shows me how much disk space is used and available across mounted drives, in a human readable format. `du -sh` tells me the size of a specific folder, which is helpful when I'm trying to find out what is eating up disk space.

---

## 🗜️ Compression and Archiving

```bash
tar -czvf archive.tar.gz folder/    # create a compressed archive
tar -xzvf archive.tar.gz            # extract a compressed archive
zip -r archive.zip folder/          # create a zip file
unzip archive.zip                   # extract a zip file
```

**Spoken answer:** `tar` combined with gzip compression is the most common way to package files on Linux. The flags are easy to remember, `c` for create, `x` for extract, `z` for gzip compression, `v` for verbose output, and `f` to specify the file name.

---

## 📜 Shell Scripting Basics

```bash
#!/bin/bash

name="Haseeb"
echo "Hello, $name"

if [ -f "file.txt" ]; then
    echo "File exists"
else
    echo "File not found"
fi

for i in 1 2 3; do
    echo "Number: $i"
done
```

**Spoken answer:** A shell script is just a file full of commands that run in sequence, which is great for automating repetitive tasks. It starts with a shebang line telling the system which interpreter to use, and supports variables, conditionals, and loops just like any programming language, though the syntax takes a bit of getting used to.

---

## ⏰ Cron Jobs (Scheduling Tasks)

```bash
crontab -e

# Run a script every day at 2 AM
0 2 * * * /home/haseeb/backup.sh
```

**Spoken answer:** Cron is a built-in scheduler that runs commands automatically at specified times. The five values before the command represent minute, hour, day of month, month, and day of week. I use cron for things like scheduled backups or cleanup scripts that need to run without me manually triggering them.

---

## 🔑 SSH and Remote Access

```bash
ssh user@192.168.1.10          # connect to a remote server
ssh-keygen -t rsa               # generate an SSH key pair
scp file.txt user@server:/path  # copy file to remote server
```

**Spoken answer:** SSH lets me securely connect to and control a remote server through an encrypted connection. Instead of typing a password every time, I usually set up SSH keys, a public key on the server and a private key on my machine, which is both more secure and more convenient.

---

## 📊 System Monitoring

```bash
uptime          # how long the system has been running
free -h         # show memory usage
df -h           # disk usage
top / htop      # live process and resource monitor
journalctl -xe  # view system logs
```

**Spoken answer:** When something feels off on a server, I usually start with `top` or `htop` to check CPU and memory, `free -h` for memory specifically, and `journalctl` to check recent system logs for errors, which together usually point me toward what's going wrong.

---

## 🛡️ Security Basics

- Never run everyday tasks as the root user, use `sudo` when needed
- Keep the system updated with security patches regularly
- Disable password based SSH login, use SSH keys instead
- Set proper file permissions, avoid using `chmod 777`
- Use a firewall like `ufw` to control open ports
- Regularly check logs for unusual activity

**Spoken answer:** Security on Linux servers mostly comes down to limiting access. I avoid logging in directly as root, use SSH keys instead of passwords, keep permissions as tight as possible, and make sure only the ports that are actually needed are open through the firewall.

---

## 💬 Common Interview Questions (Spoken-Style Answers)

**Q: What is the difference between a process and a thread?**
A process is an independent running instance of a program with its own memory space. A thread is a smaller unit within a process that shares the same memory, which makes threads lighter but also means they need careful synchronization to avoid conflicts.

**Q: What is the difference between hard link and soft link?**
A hard link points directly to the same data on disk as the original file, so both point to the same inode. A soft link, or symbolic link, is more like a shortcut that points to the file's path, and it breaks if the original file is moved or deleted.

**Q: What does chmod 755 mean?**
It means the owner can read, write, and execute the file, while the group and others can only read and execute it. Each digit represents a set of permissions in order, owner, group, and others.

**Q: How do you check which process is using a specific port?**
I would use a command like `sudo lsof -i :8080` or `netstat -tulpn | grep 8080` to find out which process is bound to that port.

**Q: What is the difference between a soft reboot and hard reboot?**
A soft reboot restarts the system gracefully through the operating system, closing processes properly first. A hard reboot cuts power abruptly, which can risk data corruption if something was mid-write, so it's only used when the system is unresponsive.

**Q: What is the purpose of the /etc/passwd file?**
It stores information about user accounts on the system, like username, user ID, home directory, and default shell, though the actual passwords are stored securely in a separate file called `/etc/shadow`.

**Q: How would you find and kill a process that is using too much memory?**
I would run `top` or `htop` to identify the process ID with the highest memory usage, then use `kill <pid>` to stop it gracefully, or `kill -9 <pid>` if it does not respond to the normal signal.

---

## ⚡ Quick Cheat Sheet

| Task | Command |
|---|---|
| Current directory | `pwd` |
| List files | `ls -la` |
| Change directory | `cd path` |
| Create folder | `mkdir name` |
| Copy file | `cp source dest` |
| Move or rename | `mv source dest` |
| Delete file | `rm file` |
| Delete folder | `rm -r folder` |
| View file | `cat file` / `less file` |
| Follow log live | `tail -f file.log` |
| Change permissions | `chmod 755 file` |
| Change owner | `chown user:group file` |
| List processes | `ps aux` |
| Kill process | `kill -9 pid` |
| Install package | `sudo apt install name` |
| Search in files | `grep -r "text" .` |
| Find files | `find . -name "*.txt"` |
| Compress folder | `tar -czvf file.tar.gz folder/` |
| Disk usage | `df -h` |
| Connect remote server | `ssh user@host` |
| Schedule task | `crontab -e` |

---

<div align="center">

**Made for interview prep by Haseeb Javed**
Good luck with your Linux interviews! 🚀

</div>