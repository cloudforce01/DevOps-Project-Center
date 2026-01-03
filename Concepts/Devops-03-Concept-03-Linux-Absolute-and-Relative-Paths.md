## Devops-03-Concept-03–Linux-Absolute-and-Relative-Paths

### Metadata Information

| **Description**                                                                                                                           | **Est. Read Time** | **Keywords**                                                      | **Author** | **Date**   | **Categories**                | **Tags**                               |
| ----------------------------------------------------------------------------------------------------------------------------------------- | ------------------ | ----------------------------------------------------------------- | ---------- | ---------- | ----------------------------- | -------------------------------------- |
| An introductory guide to the Linux filesystem hierarchy, user contexts on AWS‑hosted Ubuntu instances, and essential navigation commands. | 7‑10 min           | linux, filesystem, absolute path, relative path, aws, ubuntu, wsl | B.U.       | 2025‑12‑30 | Cloud Computing, Linux Basics | linux‑fundamentals, paths, aws‑ubuntu, |

---

👉 **Ready for the hands‑on portion?** The theory is covered below. When you feel comfortable, jump straight to the practical lab: 

<a href="../Labs/DevOps-03-Lab-02-Absolute-and-Relative-Paths.md#metadata-information" target="_blank" rel="noreferrer noopener" title="Ctrl/Cmd‑click or Middle‑click to open in a new tab">▶️ **Run the Lab** → DevOps-03-Lab-02-Absolute-and-Relative-Paths - jump to "📊 Metadata Information </a>

---

### 📄 Summary

| #       | Core Take‑aways                                                                                                                                                                                         |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1️⃣** | **Linux filesystem hierarchy** – All absolute paths start with `/`. The root (`/`) branches into standard directories (`/bin`, `/etc`, `/var`, `/home`, …).                                             |
| **2️⃣** | **User home locations** – `root` lives in `/root`; the default Ubuntu user `ubuntu` lives in `/home/ubuntu`. Other users default to `/home/<username>`.                                                 |
| **3️⃣** | **Absolute vs. relative paths** – Absolute paths begin with `/` (e.g., `/var/log`). Relative paths never start with `/` and are interpreted from the current working directory (e.g., `log`, `../lib`). |
| **4️⃣** | **Common CLI commands** – `pwd`, `ls`, `cd`, `whoami`, `hostname`, `sudo hostnamectl set‑hostname …`, `exit`, `history`, `sudo reboot`, `sudo poweroff`.                                                |
| **5️⃣** | **AWS‑specific user model** – `root` is disabled for direct SSH; you always log in as `ubuntu` (or another IAM‑created user).                                                                           |

---

### 1️⃣ ☁️ Linux Filesystem Overview

*(This is just a miniature overview and does not include all files within the Linux filesystem.)*

/
├─ bin – essential binaries
├─ sbin – system binaries
├─ lib – shared libraries
├─ etc – configuration files
├─ var – variable data (logs, caches)
├─ tmp – temporary files
└─ home
├─ ubuntu → /home/ubuntu (default non‑root user on AWS)
└─ → /home/

*The tilde (`~`) is a shortcut for the current user’s home directory.*

- For **root**: `~` → `/root`
- For **ubuntu**: `~` → `/home/ubuntu`

-------------------

### 2️⃣ 🔹 Navigating with `cd`

| Command     | Meaning                                                                   |
| ----------- | ------------------------------------------------------------------------- |
| `cd /`      | Move to the **absolute** root directory.                                  |
| `cd /var`   | Jump directly to `/var` using an absolute path.                           |
| `cd log`    | Move into a sub‑directory named `log` **relative** to the current folder. |
| `cd ..`     | Go **up** one level (parent directory).                                   |
| `cd ../lib` | From `/var/log`, go up to `/var` then into `lib`.                         |
| `cd ~`      | Return to the home directory (`/home/ubuntu` for the default user).       |

> **Tip:** The tilde only appears when you are *already* in your home directory. Once you `cd` elsewhere, the prompt shows the full path.

------------------------------

### 3️⃣ 🛠️ Essential Commands Recap

| Command                                    | What it does                                  |
| ------------------------------------------ | --------------------------------------------- |
| `whoami`                                   | Prints the current username.                  |
| `pwd`                                      | Shows the present working directory.          |
| `ls`                                       | Lists files/folders in the current directory. |
| `history`                                  | Displays previously executed commands.        |
| `hostname`                                 | Returns the current hostname.                 |
| `sudo hostnamectl set‑hostname <new-name>` | Changes the system hostname (requires sudo).  |
| `exit`                                     | Logs out of the current shell session.        |
| `sudo reboot`                              | Restarts the instance.                        |
| `sudo poweroff`                            | Powers off the instance.                      |

---

### ❓ Question & Answer

| #      | Question                                                                          | Answer                                                                                                                                                                                                                                     |
| ------ | --------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Q1** | *What is the difference between an absolute and a relative path?*                 | An **absolute** path begins with `/` and describes the location from the filesystem root (e.g., `/var/log`). A **relative** path does **not** start with `/` and is resolved from the current working directory (e.g., `log` or `../lib`). |
| **Q2** | *Where does the `ubuntu` user’s home directory reside on an AWS Ubuntu instance?* | `/home/ubuntu` (shown as `~` when you are in that directory).                                                                                                                                                                              |
| **Q3** | *Why can’t you SSH directly as `root` on an AWS Ubuntu instance?*                 | For security, AWS disables direct root login; you must connect as `ubuntu` (or another non‑privileged user) and then use `sudo` for elevated actions.                                                                                      |
| **Q4** | *Which command changes the system hostname permanently?*                          | `sudo hostnamectl set‑hostname <new-hostname>`                                                                                                                                                                                             |
| **Q5** | *What does `chmod 400 <key>.pem` achieve before SSH?*                             | It restricts the private key file to read‑only for the owner, satisfying SSH’s security requirements.                                                                                                                                      |

---

👉 **Ready for the hands‑on part?**  

The theory is covered above. When you’re comfortable, move on to the practical lab:

<a href="../Labs/DevOps-03-Lab-02-Absolute-and-Relative-Paths.md#metadata-information" target="_blank" rel="noreferrer noopener" title="Ctrl/Cmd‑click or Middle‑click to open in a new tab">▶️ **Run the Lab** → DevOps-03-Lab-02-Absolute-and-Relative-Paths - jump to "📊 Metadata Information </a>

---
