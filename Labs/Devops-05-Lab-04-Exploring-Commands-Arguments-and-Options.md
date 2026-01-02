# 🧪 Devops‑05‑Lab‑04 – Exploring Commands, Arguments, and Options

### 📊 Metadata Information

# Metadata Information

| 📖 Description                                                                                                                  | ⏱️ Est. Read Time | ⏱️Est. Lab Time | ⏱️Total Time | 🏷️ Keywords                                               | ✍️ Author | 📅 Date    | 📂 Categories                                        | 🏷️ Tags                                    |
| ------------------------------------------------------------------------------------------------------------------------------- | ----------------- | --------------- | ------------ | ---------------------------------------------------------- | --------- | ---------- | ---------------------------------------------------- | ------------------------------------------- |
| Hands‑on lab to locate commands, inspect options, and use arguments to manage files/directories on a remote Ubuntu EC2 instance | 10‑15 min         | 10 - 15 min     | 20 - 30 min  | linux, cli, aws, ec2, wsl, powershell, ssh, mkdir, history | B.U.      | 2026‑01‑02 | Cloud Computing, Linux Basics, Arguments and Options | linux‑fundamentals, cli‑options, aws‑ubuntu |

### 🔗 Concept linked to this lab

▶️ **Read the Concept →** 

<a href="../Concepts/Devops-05-Concept-05-Arguments-and-Options-of-Linux-Commands.md#metadata-information" target="_blank" rel="noreferrer noopener" ▶️ **Run the Lab →** <a href="../Labs/Devops-05-Lab-04-Exploring-Commands-Arguments-and-Options.md#metadata-information" target="_blank" rel="noreferrer noopener" title="Ctrl/Cmd‑click or Middle‑click to open in a new tab"> Devops-05-Lab-04-Exploring-Commands-Arguments-and-Options - jump to "📊 Metadata Information> Devops‑05‑Concept‑05‑Arguments‑and‑Options‑of‑Commands - jump to "📊 Metadata Information </a>

---

## 📚 Topics Covered

- 🔎 Locating binaries with `which`
- 📖 Viewing command help (`--help`, `man`)
- 📂 Creating nested directories in one line (`mkdir -p` / `--parents`)
- 📁 Listing files with various `ls` flags (colour‑coded output)
- ⏳ Enabling history timestamps
- ⏹️ Stopping an EC2 instance from inside the SSH session or via the AWS console

---

## 📋 Summary

This lab reinforces the theoretical concepts by having you work on a live Ubuntu EC2 instance, discover command locations, explore options, create directories, list files with colour‑coded output, enable timestamped history, and finally shut the instance down cleanly.

---

## 🗂️ Lab Overview

**If you haven’t created an EC2 instance yet—or if the instance you had was terminated—follow these steps to launch a new one:**

1️⃣ **Launch & Connect** – Rather than repeating the initial setup, refer to the previous lab for the start‑up instructions: **<a href="../Labs/Devops‑04‑Lab‑03- Creating-Files-and-Directories-on-Remote-Ubuntu-Instance.md#start-the-ec2-instance" target="_blank" rel="noreferrer noopener"> Devops‑04‑Lab‑03 – Starting & Connecting to the Remote Ubuntu Instance – Jump to 1️⃣ Start the EC2 Instance</a>**. After establishing an active SSH session, proceed with the remaining steps.

*If you already have an Ubuntu instance available, simply start it and continue with the instructions below.*

2️⃣ **Verify command locations** with `which`.

3️⃣ **Inspect options** for `mkdir`.

4️⃣ **Create a nested directory tree** using a single command.

5️⃣ **List files** with several `ls` variations.

6️⃣ **Enable and view history timestamps**.

7️⃣ **Clean‑up** by stopping the instance (inside SSH or from the console).

---

## 🛠️ **Detailed Steps**

### 1️⃣ Verify Command Locations

bash

```bash
which mkdir # expected: /usr/bin/mkdir 
which poweroff # expected: /sbin/poweroff 
which hostnamectl # expected: /usr/bin/hostnamectl

#If any command returns nothing, note that it is not in your `$PATH`.
```

### 2️⃣ Inspect Options

bash

```bash
mkdir --help | head -n 20 
# or
man mkdir | col -b | grep -A3 "^OPTIONS"
```

### 3️⃣ Create a Nested Directory Structure (single command)

bash

```bash
mkdir -pv /tmp/administration/linux 
# Verify 
ls -R /tmp/administration
#Repeat using the long form:
mkdir --parents /tmp/automation/ansible
```

### 4️⃣ List Files in Various Ways

bash

```bash
ls --color=auto
#Simple list 
ls /tmp 
# Include hidden entries 
ls -a /tmp 
# Long listing with human‑readable sizes 
ls -lh /tmp 
# Recursive listing 
ls -R /tmp
 # Sort by modification time (newest first) 
ls -t /var/log
```

Notice the colour coding (white = file, dark blue = directory, light blue = symlink, green background = world‑rw‑x).

### 5️⃣ Experiment with History Timestamps

bash

```bash
# Enable timestamps for this session 
export HISTTIMEFORMAT="%F %T " 
# Run a few commands, then view history 
history | tail -n 5
```

To make it permanent, append the export line to `~/.bashrc` and reload:

bash

```bash
echo 'export HISTTIMEFORMAT="%F %T "' >> ~/.bashrc source ~/.bashrc
```

### 6️⃣ Clean‑Up (Stop the Instance)

You have two choices:

#### A – From Inside the SSH Session

```
sudo poweroff 
# immediate halt 
# or 
sudo shutdown -h now # graceful halt
```

The SSH connection will close automatically.

#### B – From the AWS Console

1. Exit the SSH session (`exit`).
2. In the EC2 Dashboard, select the instance → **Actions → Instance State → Stop**.

Confirm the instance state changes to **stopped**.

---

## ❓ Q&A

| #   | 🤔 Question                                                                                            | ✅ Answer                                                                                                                                                                                                                            |
| --- | ------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Which option flag did you find most useful when creating deep directory trees, and why?                | `-p` (or `--parents`) – it builds the whole hierarchy in one shot, avoiding multiple `mkdir` calls.                                                                                                                                 |
| 2   | After enabling `HISTTIMEFORMAT`, how does the timestamp help you debug your command history?           | It shows the exact time each command ran, letting you correlate actions with logs or system events.                                                                                                                                 |
| 3   | Between `sudo poweroff` and `sudo shutdown -h now`, which do you prefer for automated scripts and why? | `shutdown -h now` is preferred when you might later need a delayed halt (`+5`) or a broadcast message; `poweroff` is a blunt immediate stop.                                                                                        |
| 4   | How can you verify that a command you located with `which` is the version you expect?                  | Run `<full‑path> --version` or `dpkg -S $(which <cmd>)` (Debian‑based) to see package info.                                                                                                                                         |
| 5   | How can you verify that the options you discovered with `--help` actually affect command behaviour?    | Run the command with the option on a test object and compare the output before and after. For example, `mkdir -p test/dir && ls -R test` versus `mkdir test/dir && ls -R test` clearly shows the parent‑creation behaviour of `-p`. |

---

### 🔙 Back to the Concept

▶️ **Read the Concept →** <a href="../Concepts/Devops-05-Concept-05-Arguments-and-Options-of-Linux-Commands.md#metadata-information" target="_blank" rel="noreferrer noopener" title="Ctrl/Cmd‑click or Middle‑click to open in a new tab"> Devops‑05‑Concept‑05‑Arguments‑and‑Options‑of‑Commands - jump to "📊 Metadata Information </a>
