# Linux User Types Explained

Linux is a multi-user operating system engineered to allow multiple users to log in, run concurrent processes, and access system resources independently without compromising system security.

---

## The 3 Types of Linux Users

```text
                     ┌────────────────────────────────────────┐
                     │          LINUX USER ACCOUNTS           │
                     └───────────────────┬────────────────────┘
                                         │
         ┌───────────────────────────────┼───────────────────────────────┐
         ▼                               ▼                               ▼
 ┌──────────────┐                ┌──────────────┐                ┌──────────────┐
 │  SUPERUSER   │                │ REGULAR USER │                │ SERVICE USER │
 │    (root)    │                │ (interactive)│                │   (system)   │
 │   UID = 0    │                │  UID >= 1000 │                │ UID: 1 - 999 │
 └──────────────┘                └──────────────┘                └──────────────┘
```

---

## 1. Superuser (`root`)

* **User ID (UID)**: Fixed at **`0`**.
* **Home Directory**: `/root`
* **Shell Prompt**: Ends with `#` (e.g., `root@server:~#`).
* **Privileges**: **Unrestricted**.
  * Total administrative authority over all hardware, the Linux kernel, processes, and memory.
  * Can read, write, modify, or delete any file on the filesystem, bypassing permission restrictions.
  * Can create, alter, or purge any account.
* **Security Rule**: Direct root login should be disabled on production servers. Administrators should log in as a normal user and use `sudo` to execute commands requiring root permissions.

---

## 2. Regular / Normal Users

* **User ID (UID)**: Starts at **`1000`** on modern Linux systems (e.g., Ubuntu, Debian, CentOS, RHEL) and can go up to `60000`.
* **Home Directory**: Located under `/home/<username>` (e.g., `/home/hp-81`).
* **Shell Prompt**: Ends with `$` (e.g., `hp-81@karthi-ubuntu:~$`).
* **Privileges**: **Restricted**.
  * Complete permissions within their personal `/home/<username>` tree.
  * Restricted from modifying system-wide configurations in `/etc` or files owned by other users.
  * Permitted to run elevated commands only if added to the `sudo` group (defined in `/etc/sudoers`).

---

## 3. System / Service Users (Daemon Accounts)

* **User ID (UID)**: Ranging from **`1` to `999`**.
* **Home Directory**: Typically set to `/nonexistent` or a service-specific path (e.g., `/var/www` or `/var/lib/mysql`).
* **Login Shell**: `/usr/sbin/nologin` or `/bin/false` (**No interactive login allowed**).
* **Common Service Users**:
  * `www-data` — Web servers (Apache, Nginx).
  * `mysql` — MySQL/MariaDB database server.
  * `sshd` — OpenSSH daemon.
  * `systemd-resolve` — Network DNS resolver.
  * `daemon` / `bin` — Legacy system maintenance tasks.

### The Security Principle of Least Privilege
System services run under dedicated non-login service users rather than `root`. If an attacker exploits a vulnerability in a web server running as `www-data`, they are contained inside `www-data` privileges and cannot access `/root`, read `/etc/shadow`, or manipulate operating system binaries.

---

## 4. Key User Configuration Files in Linux

Linux stores user and group data in plain-text configuration files:

| Configuration File | Permissions | Contents |
| :--- | :--- | :--- |
| **`/etc/passwd`** | Readable by all (`644`) | User account records: username, encrypted password placeholder (`x`), UID, GID, comment/name, home directory, login shell. |
| **`/etc/shadow`** | Readable by root only (`640` / `600`) | Securely hashed passwords, password age, expiration, and lock flags. |
| **`/etc/group`** | Readable by all (`644`) | Defines user group names, Group IDs (GIDs), and group member lists. |

### `/etc/passwd` Field Format Breakdown:
```text
hp-81:x:1000:1000:hp-81,,,:/home/hp-81:/bin/bash
  │   │  │    │     │           │         │
  │   │  │    │     │           │         └─ Default Login Shell
  │   │  │    │     │           └─────────── Home Directory
  │   │  │    │     └─────────────────────── User Comment / Full Name
  │   │  │    └───────────────────────────── Group ID (GID)
  │   │  └────────────────────────────────── User ID (UID)
  │   └───────────────────────────────────── Password marker (stored in /etc/shadow)
  └───────────────────────────────────────── Username
```

---

## 5. User Inspection Commands

```bash
# Print your currently active username
whoami

# View your UID, GID, and all group memberships
id

# List all groups the current user belongs to
groups

# View all user accounts configured on the Linux machine
cat /etc/passwd

# Filter to see only regular interactive users
grep -E ":[1-9][0-9]{3}:" /etc/passwd
```
