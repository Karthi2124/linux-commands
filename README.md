# Linux is Everywhere 🐧

A comprehensive, beginner-to-advanced reference guide for understanding Linux operating systems, terminal environments, file systems, and commands.

---

## 📚 Table of Contents

| Topic | Document | Description |
| :--- | :--- | :--- |
| **Terminal Prompt** | [Terminal-Prompt-Explanation.md](./Terminal-Prompt-Explanation.md) | Understanding `user@hostname:~$`, paths, and `$` vs `#` privileges. |
| **Interfaces** | [GUI-vs-CLI.md](./GUI-vs-CLI.md) | Graphical vs Command Line Interface, Terminal vs Shell, and why Linux servers rely on CLI. |
| **Commands Overview**| [What-is-Linux-Command.md](./What-is-Linux-Command.md) | Anatomy of a command, short vs long flags, command types, `$PATH`, and help tools. |
| **Command Cheat Sheet** | [Linux-Commands.md](./Linux-Commands.md) | Categorized reference guide covering navigation, file management, permissions, processes, and networking. |
| **File System** | [Linux-File-System.md](./Linux-File-System.md) | FHS directory tree hierarchy, "Everything is a file", `/` vs `/root`, dotfiles, and permissions. |
| **User Types** | [User-Types.md](./User-Types.md) | Root Superuser, Regular Users, and Service Users (`daemon`), UID ranges, and `/etc/passwd`. |
| **Tips & Shortcuts** | [Linux-Tips.md](./Linux-Tips.md) | Terminal keyboard shortcuts, productivity tricks (`sudo !!`, `!$`), redirection, pipes, and safety rules. |

---

## 🚀 Quick Start: The Linux Philosophy

1. **Everything is a File**: Hardware, running processes, configurations, and directories are represented as files or file descriptors.
2. **Small Programs Combined via Pipes**: Programs do one job well and chain together via pipelines (`|`).
3. **Plain Text Configuration**: System settings and user accounts are managed through readable plain text files under `/etc`.
4. **Principle of Least Privilege**: Users and system services run with minimal necessary permissions to ensure system security.
