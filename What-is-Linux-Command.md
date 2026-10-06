# What is a Linux Command?

A Linux command is an instruction given to a Linux system via the command line interface to carry out a specific operation.

When you enter a command and press `Enter`:
1. The **Shell** interprets your input.
2. The shell resolves the program location via the `$PATH` variable.
3. The **Linux Kernel** executes the program and manages the required system hardware and memory.
4. The output is streamed back to your terminal screen.

---

## 1. Anatomy of a Linux Command

Standard Linux commands are composed of three parts:

```text
command    [options / flags]    [arguments / targets]
───────    ─────────────────    ─────────────────────
   │               │                      │
   │               │                      └─ The target file, path, or text to act on
   │               └─ Modifies or customizes the command's behavior
   └─ The executable program or built-in to run
```

### Examples:

```bash
# Example 1: Long listing of a specific directory
ls -l /var/log
# ├── ls        -> Command (list directory contents)
# ├── -l        -> Option (detailed long format)
# └── /var/log  -> Argument (target directory)

# Example 2: Create parent directories automatically
mkdir -p projects/linux/scripts
# ├── mkdir     -> Command (make directory)
# ├── -p        -> Option (create parent directories if missing)
# └── projects..-> Argument (target path)
```

---

## 2. Options and Flags: Short vs. Long

Options modify how a command behaves:

| Style | Syntax | Example | Details |
| :--- | :--- | :--- | :--- |
| **Short Flag** | Single hyphen (`-`) followed by a single letter | `ls -a`<br>`ls -l -a` | Can be combined into a single flag:<br>`ls -la` |
| **Long Flag** | Double hyphens (`--`) followed by a full word | `ls --all`<br>`ls --human-readable` | Self-documenting and easier to read in shell scripts |

---

## 3. The 4 Types of Linux Commands

In Linux, not all commands are standalone files on disk:

1. **Shell Built-in Commands**:
   * Integrated directly into the shell executable (`bash`) for speed.
   * Do not require spawning a new child process.
   * Examples: `cd`, `pwd`, `echo`, `exit`, `history`.

2. **Executable Binaries**:
   * Compiled binary files stored in directories like `/bin`, `/usr/bin`, or `/usr/local/bin`.
   * Examples: `ls`, `grep`, `find`, `cat`, `python3`.

3. **Aliases**:
   * Custom shortcuts defined by users to simplify long or repetitive commands.
   * Example: `alias ll='ls -la'`

4. **Shell Functions & Scripts**:
   * Executable text files starting with a shebang (`#!/bin/bash`) containing a series of sequential Linux commands.

> [!TIP]
> You can discover the type of any command in Linux using the `type` command:
> ```bash
> type cd    # Output: cd is a shell builtin
> type ls    # Output: ls is aliased to `ls --color=auto`
> type grep  # Output: grep is /usr/bin/grep
> ```

---

## 4. How Linux Finds Commands: The `$PATH` Variable

When you execute a command (e.g., `grep`), Linux searches through a colon-separated list of directories defined in the `$PATH` environment variable:

```bash
echo $PATH
# Output: /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

If the command binary does not reside in any of these directories, the shell returns:
```text
bash: command not found
```

---

## 5. Built-in Help and Manuals

Linux includes comprehensive built-in documentation so you never need to rely on guesswork:

```bash
# 1. Quick command help (flags and basic usage)
ls --help

# 2. Complete reference manual page (press 'q' to exit)
man grep

# 3. One-line description of what a command does
whatis tar

# 4. Find the exact binary path on the filesystem
which python3
```
