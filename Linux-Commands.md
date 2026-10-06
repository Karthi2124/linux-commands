# Essential Linux Commands Reference Guide

A structured reference of essential Linux terminal commands categorized by function.

---

## 1. Directory Navigation

| Command | Description | Example |
| :--- | :--- | :--- |
| `pwd` | **Print Working Directory**: outputs the full absolute path of your current location. | `pwd` |
| `cd <dir>` | **Change Directory**: navigate into a target folder. | `cd /var/log` |
| `cd ..` | Move up one level to the **parent directory**. | `cd ..` |
| `cd ~` | Return directly to your **user home directory** (`/home/username`). | `cd ~` or `cd` |
| `cd -` | Switch back to the **previous working directory**. | `cd -` |

---

## 2. Listing Files and Folders (`ls`)

| Command | Description |
| :--- | :--- |
| `ls` | List visible files and directories in current working location. |
| `ls <path>` | List contents of a designated folder (e.g., `ls /etc`). |
| `ls -l` | **Long listing format**: shows file permissions, owner, group, file size, and timestamp. |
| `ls -a` | **All files**: includes hidden dotfiles (files starting with `.`). |
| `ls -lh` | **Human-readable**: formats file sizes into KB, MB, or GB. |
| `ls -la` | Combined detailed listing including hidden files. |
| `ls -R` | **Recursive**: lists all subdirectories and nested contents. |
| `ls -lt` | Sort listings by last modification timestamp (newest first). |

---

## 3. File and Directory Management

| Command | Description | Example |
| :--- | :--- | :--- |
| `touch <file>` | Create a new empty file or refresh the timestamp of an existing file. | `touch app.log` |
| `mkdir <dir>` | Create a new directory. | `mkdir scripts` |
| `mkdir -p <path>` | Create parent directories as needed without throwing errors. | `mkdir -p project/src/utils` |
| `cp <src> <dest>` | Copy a file to another name or location. | `cp config.env config.backup` |
| `cp -r <src> <dest>` | Copy an entire directory recursively. | `cp -r ./src ./src_backup` |
| `mv <src> <dest>` | Move or rename a file or folder. | `mv old_name.txt new_name.txt` |
| `rm <file>` | Permanently delete a file. | `rm obsolete.log` |
| `rm -r <dir>` | Recursively delete a directory and all its contents. | `rm -r old_builds/` |
| `rm -rf <dir>` | Force delete directory and contents without confirmation prompts. | `rm -rf cache/` |

> [!CAUTION]
> Linux does not have a Recycle Bin or Trash when using `rm`. Deletions via `rm` are permanent.

---

## 4. Reading and Searching Files

| Command | Description | Example |
| :--- | :--- | :--- |
| `cat <file>` | Concatenate and print entire file contents to terminal. | `cat /etc/os-release` |
| `less <file>` | Open file in an interactive, scrollable reader (press `q` to quit). | `less /var/log/syslog` |
| `head -n <lines> <file>` | View the first *N* lines of a file. | `head -n 20 error.log` |
| `tail -n <lines> <file>` | View the last *N* lines of a file. | `tail -n 20 error.log` |
| `tail -f <file>` | Continuously stream new appended lines in real-time. | `tail -f /var/log/nginx/access.log` |
| `grep "<pattern>" <file>`| Search for a specific text pattern inside a file. | `grep "404" access.log` |
| `grep -r "<pattern>" .` | Recursively search for pattern across all files in directory. | `grep -r "DATABASE_URL" ./src` |
| `find <path> -name "<name>"` | Locate files and directories by name pattern. | `find . -name "*.conf"` |

---

## 5. System, Storage and Hardware Diagnostics

| Command | Description | Example |
| :--- | :--- | :--- |
| `whoami` | Print the current authenticated Linux username. | `whoami` |
| `uname -a` | Print comprehensive Linux kernel and system architecture information. | `uname -a` |
| `uptime` | Display how long system has been up and current load averages. | `uptime` |
| `df -h` | **Disk Free**: display disk space usage per mounted partition in human-readable units. | `df -h` |
| `du -sh *` | **Disk Usage**: calculate size of each file and folder in current directory. | `du -sh *` |
| `free -h` | Display total, used, and available RAM and swap memory. | `free -h` |
| `cal` | Output a text calendar into the terminal. | `cal` |

---

## 6. Process and Service Management

| Command | Description | Example |
| :--- | :--- | :--- |
| `ps` | Display snapshot of processes running in current terminal. | `ps` |
| `ps aux` | Display all processes running across the entire Linux system. | `ps aux` |
| `top` | Interactive real-time process manager (press `q` to exit). | `top` |
| `htop` | Interactive graphical process viewer with color-coded CPU and memory bars. | `htop` |
| `kill <PID>` | Send termination signal (`SIGTERM`) to process ID. | `kill 1420` |
| `kill -9 <PID>` | Force kill process immediately (`SIGKILL`). | `kill -9 1420` |

---

## 7. User and Permission Management

| Command | Description | Example |
| :--- | :--- | :--- |
| `sudo <command>` | Execute a command with elevated superuser privileges. | `sudo apt update` |
| `su - <user>` | Switch session to another Linux user account. | `su - hp-81` |
| `passwd` | Update your user password. | `passwd` |
| `sudo passwd <user>` | Reset password for a specific user (admin operation). | `sudo passwd john` |
| `sudo passwd -l <user>`| Lock a user's password to disable password-based login. | `sudo passwd -l john` |
| `sudo useradd -m <user>`| Create a new Linux user account and generate their home folder. | `sudo useradd -m devuser` |
| `sudo userdel -r <user>`| Delete a user account along with their home directory. | `sudo userdel -r devuser` |
| `chmod <mode> <file>` | Modify file read (`r`), write (`w`), and execute (`x`) permissions. | `chmod +x deploy.sh` |
| `chown <user>:<grp> <file>`| Reassign file ownership to a designated user and group. | `sudo chown hp-81:hp-81 app.js` |

---

## 8. Linux Networking and Connectivity

| Command | Description | Example |
| :--- | :--- | :--- |
| `ip a` (or `ip addr`) | Display all network interfaces, MAC addresses, and assigned IP addresses. | `ip a` |
| `ping <host>` | Send ICMP ECHO_REQUEST packets to verify network connectivity (Ctrl+C to stop). | `ping 8.8.8.8` |
| `curl <URL>` | Transfer data to or from a server over HTTP, HTTPS, or FTP. | `curl https://icanhazip.com` |
| `ssh <user>@<host>` | Secure Shell: establish an encrypted remote session to a Linux server. | `ssh admin@192.168.1.100` |
| `ss -tulpn` | Inspect open ports and listening network sockets. | `sudo ss -tulpn` |

---

## 9. Terminal Utilities and Command History

| Command | Description | Example |
| :--- | :--- | :--- |
| `clear` | Clear the terminal viewport (Keyboard shortcut: `Ctrl + L`). | `clear` |
| `history` | List command history executed in the current user session. | `history` |
| `history <N>` | List the last *N* executed commands. | `history 25` |
| `which <cmd>` | Print the exact absolute path of the executable invoked by a command. | `which bash` |
| `whereis <cmd>` | Locate the binary, source files, and man pages for a command. | `whereis python3` |
| `sort <file>` | Sort file lines in alphabetical order. | `sort names.txt` |
| `sort -n <file>` | Sort file lines in numeric order. | `sort -n scores.txt` |