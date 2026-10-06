# Linux Terminal Tips, Tricks & Shortcuts

Essential command line tips, shell keyboard shortcuts, productivity techniques, and safety rules for working in Linux.

---

## 1. Essential Bash & Terminal Keyboard Shortcuts

| Shortcut | Action | Description |
| :--- | :--- | :--- |
| **`Tab`** | Auto-completion | Press **once** to autocomplete file paths or commands; press **twice** to view all available possibilities. |
| **`Ctrl + C`** | Cancel / Interrupt | Sends `SIGINT` to terminate the currently executing foreground program. |
| **`Ctrl + L`** | Clear Screen | Clears the terminal screen buffer (same effect as the `clear` command). |
| **`Ctrl + D`** | Exit / EOF | Closes current terminal session or logs out of active user shell. |
| **`Ctrl + A`** | Move to Start | Jumps cursor immediately to the beginning of the command line. |
| **`Ctrl + E`** | Move to End | Jumps cursor immediately to the end of the command line. |
| **`Ctrl + U`** | Cut to Start | Deletes all text from the current cursor position back to the beginning of the line. |
| **`Ctrl + K`** | Cut to End | Deletes all text from the current cursor position forward to the end of the line. |
| **`Ctrl + W`** | Cut Word | Deletes the word immediately preceding the cursor. |
| **`Ctrl + R`** | Reverse History Search | Interactively search through previously run shell commands by typing keywords. Press `Ctrl + R` repeatedly to cycle backwards. |

---

## 2. Command Line Productivity Tricks

### Re-run Failed Privileged Command: `sudo !!`
If you run a command and encounter a permission denied error, re-run it with elevated privileges without retyping the entire command:
```bash
apt update
# E: Could not open lock file - Permission denied
sudo !!
# Runs: sudo apt update
```

### Reuse the Last Argument: `!$` or `Alt + .`
Quickly reuse the final parameter of the previous command:
```bash
mkdir -p /var/www/my-site
cd !$
# Expands automatically to: cd /var/www/my-site
```

### Toggle Between Two Directories: `cd -`
Jump between your current and previous directory:
```bash
cd /var/log/nginx
cd /home/hp-81/projects
cd -
# Navigates straight back to: /var/log/nginx
```

### Return Directly Home: `cd`
Typing `cd` without any arguments instantly returns you to your home folder (`~`):
```bash
cd
# Working directory is now: /home/hp-81
```

---

## 3. Input & Output Redirection

By default, Linux commands receive input from the keyboard (`stdin`) and write output to the terminal screen (`stdout` and `stderr`):

| Operator | Action | Example |
| :--- | :--- | :--- |
| `>` | **Redirect and Overwrite** | `ls -la > directory_list.txt` |
| `>>` | **Redirect and Append** | `echo "Task completed" >> audit.log` |
| `<` | **Read from File** | `mysql -u root -p database < backup.sql` |
| `2>` | **Redirect Standard Error Only** | `find / -name "*.conf" 2> /dev/null` *(suppresses permission denied errors)* |
| `&>` | **Redirect Both Output and Errors** | `make &> compilation.log` |

---

## 4. Linux Pipelines (`|`)

The pipe operator (`|`) routes the standard output of one command directly into the standard input of the next:

```bash
# 1. Filter running processes for a specific service:
ps aux | grep "nginx"

# 2. Count total number of files in a directory:
ls -1 /etc | wc -l

# 3. View large command output with interactive paging:
cat /var/log/dpkg.log | less

# 4. Find the 5 largest directories consuming disk space:
du -sh /* 2>/dev/null | sort -hr | head -n 5
```

---

## 5. Shell Wildcards (Globbing)

| Wildcard | Match Rule | Linux Example |
| :--- | :--- | :--- |
| `*` | Matches zero or more characters | `rm *.log` *(deletes all files ending in .log)* |
| `?` | Matches exactly one single character | `ls file?.txt` *(matches file1.txt, fileA.txt)* |
| `[abc]` | Matches any single character in the set | `ls image[1-3].png` *(matches image1, image2, image3)* |
| `[^abc]` | Matches any character NOT in the set | `ls file[^0-9].txt` |

---

## 6. Linux Safety Best Practices

1. **Verify Location Before Recursive Deletion**:
   Always run `pwd` before running `rm -rf` to ensure you are in the intended directory.
2. **Perform Dry Runs**:
   Before deleting with a wildcard pattern (`rm *.log`), list them first using `ls *.log` to verify which files match.
3. **Always Backup System Configurations Before Editing**:
   ```bash
   sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.orig
   ```
