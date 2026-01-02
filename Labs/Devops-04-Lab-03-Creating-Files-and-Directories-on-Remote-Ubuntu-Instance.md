## **DevOps‑04‑Lab‑03 – Creating Files and Directories (Remote Ubuntu Instance)**

Metadata (single‑row table)

| Description                                                                                                           | Est. Read  Time | Est. Lab Time | Total  Time | Keywords                                                               | Author | Date       | Categories                    | Tags                                                                                     |
| --------------------------------------------------------------------------------------------------------------------- | --------------- | ------------- | ----------- | ---------------------------------------------------------------------- | ------ | ---------- | ----------------------------- | ---------------------------------------------------------------------------------------- |
| Hands‑on practice creating files/directories, using basic editors, and managing permissions on an AWS Ubuntu instance | 5‑7 min         | 15‑20 min     | 20‑27 min   | linux, file creation, directory creation, aws, ubuntu, wsl, powershell | B.U.   | 2026‑01‑01 | Cloud Computing, Linux Basics | lab‑linux‑paths, file creation, directory creation, aws‑ubuntu, cli‑practice, powershell |

---

**← Back to the theory [← Concept → Devops-04-Concept-04-Creating-Files-and-Directories-in-Linux](../Concepts/Devops‑04-Concept- 04-Creating-Files-and-Directories-in-Linux.md)**

---

### 📊 Summary

| Phase        | Action                                                                                                          | Expected outcome                                                        |
| ------------ | --------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| **Start**    | Launch the stopped EC2 Ubuntu instance from the AWS console                                                     | Instance state becomes **running** and a public DNS is assigned.        |
| **Connect**  | SSH into the instance from **WSL** or **PowerShell** using the `.pem` key                                       | You land in `/home/ubuntu` as the `ubuntu` user.                        |
| **Operate**  | Run commands to create directories (`mkdir`), files (`touch`), edit with `vim`, and list contents (`ls`, `cat`) | Directory hierarchy and file contents appear as described in the steps. |
| **Clean‑up** | Power off the VM (`sudo poweroff` or `sudo shutdown -h now`) **or** stop it via the AWS console                 | Instance state changes to **stopped**, releasing resources.             |

---

### 🎯 Topics Covered

- Starting & stopping an EC2 instance
- SSH access from Windows (WSL & PowerShell)
- Basic navigation (`pwd`, `ls`, `cd`)
- Creating directories (`mkdir`) and files (`touch`)
- Editing files with **vim** (insert mode, command mode, save + quit)
- Verifying changes with `cat` and `ls -l`
- Cleaning up resources safely

----

### 📄 Lab Overview

You will:

1. Start the EC2 instance.
2. Connect via **WSL** or **PowerShell**.
3. Execute a series of commands that create a directory hierarchy, create and edit a text file, and list the results.
4. Shut down the instance either from the SSH session or via the AWS console.

> **Prerequisite:** 
> 
> The EC2 instance must already exist and you must have the private key (`*.pem`) stored locally.
> 
> If the EC2 instance does not yet exist, create it first using the following link: **[Create EC2 instance – Lab Setup Guide](../Labs/Devops-02-Lab-01-Spin-Up-An-EC2-Instance.md)**

-----

### 🔧 Preparation – Replace Placeholders

| Placeholder                               | Substitute with                                              |
| ----------------------------------------- | ------------------------------------------------------------ |
| `<YOUR_WINDOWS_USERNAME>`                 | Your Windows login name (folder containing `keys`).          |
| `YOUR_KEY_NAME.pem`                       | Name of the PEM file you downloaded (e.g., `Ubuntu-KP.pem`). |
| `ec2‑xx‑xx‑xx‑xx.compute-1.amazonaws.com` | Public DNS of **your** EC2 instance.                         |

---------------------

### 1️⃣ Start the EC2 Instance

1. Open **AWS Management Console → EC2 Dashboard**.
2. Locate your Ubuntu instance (e.g., `EC2‑Ubuntu‑Distro`).
3. Choose **Actions → Instance State → Start**.
4. Wait until the **Instance state** reads **running**.

------------------

### 2️⃣ Connect to the Instance

**Option A – WSL**

bash

```bash
cd /mnt/c/Users/<YOUR_WINDOWS_USERNAME>/keys 
chmod 400 YOUR_KEY_NAME.pem # only if needed 
ssh -i "YOUR_KEY_NAME.pem" ubuntu@ec2-xx-xx-xx-xx.compute-1.amazonaws.com
```

**Option B – PowerShell**

bash

```bash
cd C:\Users\<YOUR_WINDOWS_USERNAME>\keys 
ssh -i "YOUR_KEY_NAME.pem" ubuntu@ec2-xx-xx-xx-xx.compute-1.amazonaws.com
```

You will land in `/home/ubuntu`.

---------------------

### 3️⃣ Validate Your Session

bash

```bash
whoami # → ubuntu hostname # default AWS hostname, e.g., ip-172-31-26-84 
pwd # → /home/ubuntu (or ~) 
ls # list files in home history 
# view prior commands
```

---------------------

### 4️⃣ Create Files & Directories

1. **Show current directory**
   
   bash
   
   ```bash
   pwd
   ```

2. **List current items**
   
   bash
   
   ```bash
   ls
   ```

3. **Create directory `dev`**
   
   bash
   
   ```bash
   mkdir dev
   ls
   ```

4. **Create a file with initial content using `vim`**
   
   bash
   
   ```bash
   vim file1.txt
   ```
   
   - Inside `vim`: press `i`, type `Welcome to Linux`, press `Esc`, then type `:wq` and press **Enter**.

5. **Append a new line “Happy Learning”**
   
   bash
   
   ```bash
   vim file1.txt
   ```
   
   - Inside `vim`: press `Esc`, then `o`, type `Happy Learning`, press `Esc`, then `:wq` and **Enter**.

6. **Create a nested directory inside `devops`**
   
   bash
   
   ```bash
   # ------------------------------------------------------------
   # Create the whole tree in one go (parents are created as needed)
   # ------------------------------------------------------------
   mkdir -p devops/terraform devops/ansible
   #   ^^^^  creates the top‑level folder if it doesn't exist
   #   |      then creates the two sub‑folders underneath it
   ls devops
   
   # OR
   
   # ------------------------------------------------------------
   # Same thing, but using brace expansion for a tidier command
   # ------------------------------------------------------------
   mkdir -p devops/{terraform,ansible}
   #   devops/               → parent directory (created if missing)
   #   {terraform,ansible}   → expands to devops/terraform  devops/ansible
   ls devops
   
   # OR
   
   # ------------------------------------------------------------
   # If you only need the 'terraform' sub‑folder 
   # ------------------------------------------------------------
   mkdir -p devops/terraform
   #   Creates devops (if absent) and then devops/terraform
   
   ls devops
   
   # OR
   
   # ------------------------------------------------------------
   # Creating multiple independent paths at once (no -p needed
   # because the parent already exists)
   # ------------------------------------------------------------
   # First ensure the parent exists:
   mkdir -p devops
   # Then add the two children:
   mkdir devops/terraform devops/ansible
   # If 'devops' already existed, the last line would succeed without -p.
   ls devops
   
   # OR
   
   # ------------------------------------------------------------
   # Trying to create a deep path without -p (will fail if any parent is missing)
   # ------------------------------------------------------------
   # This will error out unless 'devops' already exists:
   mkdir devops/terraform/ansible
   #   Error: cannot create directory ‘devops/terraform/ansible’: No such file or directory
   # Use -p to avoid the error:
   mkdir -p devops/terraform/ansible
   ls devops
   ```

7. **Create an additional empty file**
   
   bash
   
   ```
   touch file2.txt 
   ls -l file2.txt
   ```

---------

### 5️⃣ Clean‑Up – Stop the Instance

**Option A – From inside SSH**

bash

```basg
sudo poweroff # immediate halt 
# or 
sudo shutdown -h now # graceful halt (can be scheduled)
```

The SSH session will close and the instance will appear **stopped** in the console.

**Option B – From the AWS Console**

1. Exit the SSH session (`exit` or simply close the terminal).
2. In the console, select the instance → **Actions → Instance State → Stop**.

--------------

### ❓ Question & Answer

| #   | Question                                                                                                         | Answer                                                                                                                                                                             |
| --- | ---------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | **What command creates an empty file without opening an editor?**                                                | `touch <filename>` creates the file (or updates its timestamp if it already exists).                                                                                               |
| 2   | **How do you create a nested directory structure in a single command?**                                          | Use `mkdir -p parent/child/grandchild`; the `-p` flag creates any missing intermediate directories.                                                                                |
| 3   | **Why can the default `ubuntu` user write only inside its home directory without `sudo`?**                       | The `ubuntu` account has write permission on `/home/ubuntu` but lacks ownership of system directories like `/etc` or `/var`; `sudo` is required to gain temporary root privileges. |
| 4   | **What is the difference between `cd ..` and `cd ../..`?**                                                       | `cd ..` moves up one level to the parent directory; `cd ../..` moves up two levels (parent of the parent).                                                                         |
| 5   | **Which command displays the current working directory, and why is it useful when working with relative paths?** | `pwd` prints the absolute path of the current directory, helping you understand the base from which relative paths are resolved.                                                   |

---

**← Back to the theory [← Concept → Devops-04-Concept-04-Creating-Files-and-Directories-in-Linux](../Concepts/Devops‑04-Concept- 04-Creating-Files-and-Directories-in-Linux.md)**

---
