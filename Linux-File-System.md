# Linux File System Architecture

The Linux file system manages how files, directories, device drivers, and system data are organized and accessed on storage drives. It follows the **Filesystem Hierarchy Standard (FHS)**.

---

## 1. What is the Linux File System?

In Linux, the file system is organized like an **inverted tree** (an upside-down tree structure):
* There is only **one root folder** at the very top, represented by a single forward slash: `/`
* All files, subdirectories, storage devices, and partitions are mounted inside this unified tree.

---

## 2. Core Linux Principle: "Everything is a File"

In Linux, almost every system resource—from text files and running processes to physical hardware—is exposed to the system as a file descriptor:

| Resource Type | Description | Linux Examples |
| :--- | :--- | :--- |
| **Regular Files** | Data files, scripts, text notes, media | `script.sh`, `notes.txt`, `kernel.img` |
| **Directories** | Special files containing a list of other file names | `/home`, `/etc`, `/var` |
| **Commands / Programs** | Executable binary files | `/bin/ls`, `/bin/bash`, `/usr/bin/python3` |
| **Hardware Devices** | Device nodes representing physical hardware | `/dev/sda` (disk), `/dev/tty` (terminal) |
| **Processes & System State**| Virtual files generated in RAM by the kernel | `/proc/cpuinfo`, `/proc/meminfo` |

---

## 3. The Linux Directory Tree (FHS)

```text
/ (Root Directory - Base of the entire system)
├── bin/          -> Essential user command binaries (ls, cp, rm, bash)
├── sbin/         -> Essential system binaries for admin (reboot, fdisk, iptables)
├── boot/         -> Bootloader files, Linux kernel, initramfs
├── dev/          -> Device files for hardware (disks, terminals, sound)
├── etc/          -> System-wide configuration files ("Editable Text Configuration")
├── home/         -> Personal home directories for regular users (/home/hp-81/)
├── root/         -> Personal home directory of the Superuser (root administrator)
├── lib/          -> Shared system libraries required by binaries in /bin and /sbin
├── media/        -> Automatic mount points for removable storage (USB flash drives)
├── mnt/          -> Manual temporary mount points for filesystems and disks
├── opt/          -> Optional third-party application software packages
├── proc/         -> Virtual filesystem containing process and kernel information
├── sys/          -> Virtual filesystem exposing kernel hardware devices and drivers
├── tmp/          -> Temporary files (cleared automatically on system reboot)
├── usr/          -> User System Resources - secondary hierarchy for applications
└── var/          -> Variable data files that change during system runtime (logs, spool)
```

---

## 4. Key Distinction: `/` vs `/root`

A common point of confusion for Linux beginners:

* **`/` (Slash)**: The **Root Directory**. It is the absolute base of the entire Linux filesystem hierarchy. Every single file and directory exists beneath this root.
* **`/root` (Folder)**: The **Superuser's Home Directory**. It is the private workspace of the administrative root user (analogous to `/home/username` for standard users).

---

## 5. Detailed Directory Breakdown

### `/home` — User Home Directories
* Contains personal files, documents, and user-specific configurations for all standard users.
* Each user gets their own subfolder (e.g., `/home/hp-81`).
* Standard users have full read/write permissions inside their own directory, but cannot access or alter other users' private files.

### `/root` — Superuser Home
* The personal home directory dedicated exclusively to the administrative `root` user.
* Kept on the primary root partition separate from `/home` to ensure the administrator can always access critical tools even if `/home` is unmounted or located on a remote network share.

### `/bin` — Essential User Binaries
* Contains primary executable programs and basic commands required for single-user mode and system recovery.
* Examples: `ls`, `cp`, `mv`, `rm`, `cat`, `mkdir`, `bash`, `ping`.

### `/sbin` — System Binaries
* Contains executable utilities intended for system administration, maintenance, and network management.
* Typically requires superuser privileges (`sudo` or `root`) to execute.
* Examples: `reboot`, `shutdown`, `fdisk`, `iptables`, `ip`.

### `/etc` — System Configuration
* Stands for *"Editable Text Configuration"*.
* Stores all host-specific, system-wide configuration files and startup scripts in plain text.
* Examples:
  * `/etc/passwd` — User account details.
  * `/etc/hostname` — The machine's network host name.
  * `/etc/fstab` — Disk storage mount configurations.

### `/var` — Variable Data
* Contains files whose contents dynamically grow and change as the system runs.
* Examples:
  * `/var/log` — System, kernel, and service log files (e.g., `syslog`, `auth.log`).
  * `/var/spool` — Print queues and queued cron jobs.
  * `/var/mail` — User mailboxes.

### `/usr` — User System Resources
* The secondary hierarchy containing shareable, read-only user data, utilities, and applications installed by package managers (`apt`, `dnf`, `pacman`).
* Common subdirectories:
  * `/usr/bin` — General user programs and commands.
  * `/usr/sbin` — Non-critical system administration binaries.
  * `/usr/lib` — Libraries for `/usr/bin` programs.
  * `/usr/share` — Architecture-independent data (documentation, icons, fonts).

### `/opt` — Optional Software
* Designed for standalone, third-party software packages that keep all their files (binaries, libraries, configs) self-contained in a single directory.
* Examples: `/opt/google/chrome`, `/opt/discord`.

### `/boot` — Boot Loader Files
* Holds all critical static files needed to start the Linux operating system.
* Contains the compiled Linux Kernel (`vmlinuz`), the initial RAM disk (`initrd` / `initramfs`), and the GRUB bootloader configuration files.

### `/dev` — Device Files
* Contains special device nodes that represent physical hardware devices connected to the system.
* In Linux, reading from or writing to these files communicates directly with the kernel hardware drivers.
* Examples:
  * `/dev/sda` — First physical storage drive.
  * `/dev/sda1` — First partition on the first storage drive.
  * `/dev/null` — The "black hole" device (discards all data written to it).
  * `/dev/urandom` — Cryptographically secure pseudo-random number generator.

### `/media` & `/mnt` — Mount Points
* **`/media`**: Automatic mount directory used by the OS for removable media (e.g., plugging in a USB flash drive or external drive).
* **`/mnt`**: Manual temporary mount point used by system administrators to mount filesystems, external partitions, or network shares manually.

### `/proc` & `/sys` — Virtual In-Memory Filesystems
* These directories do **not** take up space on disk. They are generated dynamically in RAM by the Linux kernel.
* **`/proc`**: Exposes live process and kernel runtime parameters:
  * `cat /proc/cpuinfo` — View CPU architecture and cores.
  * `cat /proc/meminfo` — View live RAM statistics.
* **`/sys`**: Exposes kernel subsystem information, device drivers, and hardware bus structures.

### `/tmp` — Temporary Files
* A shared directory where programs and users can write temporary data files during execution.
* Writable by all users.
* Files in `/tmp` are automatically purged upon reboot or on a periodic schedule.

---

## 6. Hidden Files (Dotfiles) in Linux

* In Linux, any file or directory that starts with a dot (`.`) is considered a **hidden file**.
* **Purpose**: Used primarily for user settings, shell environment profiles, and application configurations without cluttering your regular folders.
* **Examples**:
  * `.bashrc` — Shell configuration script executed on interactive terminal launch.
  * `.profile` — Environmental path variables loaded upon login.
  * `.git/` — Git version control tracking directory.
* **How to view hidden files**:
  ```bash
  ls -a
  ```
  *(The `-a` flag stands for "all")*

---

## 7. File Permissions vs. File Extensions

* Unlike operating systems that depend strictly on file extensions (like `.exe`), Linux determines file behavior using **file permissions** and **magic bytes** (file signatures):
  * **Executable Permission (`x`)**: A file can only be run as a program if its execution permission bit is set (`chmod +x script.sh`).
  * Extensions like `.sh`, `.conf`, or `.txt` in Linux are purely conventions for human readability.
