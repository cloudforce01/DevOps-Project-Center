## **DevOps‑03‑Lab‑02 – Absolute & Relative Paths on an AWS Ubuntu Instance**

### Metadata Information

| Description                                                                                                 | Estimated Read Time | Estimated Lab Time | Total Time | Keywords                                                          | Author | Date       | Categories                    | Tags                                                  |
| ----------------------------------------------------------------------------------------------------------- | ------------------- | ------------------ | ---------- | ----------------------------------------------------------------- | ------ | ---------- | ----------------------------- | ----------------------------------------------------- |
| Hands‑on practice navigating the Linux filesystem, switching hostnames, and managing the instance lifecycle | 5‑7 min             | 15‑20 min          | 20‑27 min  | linux, absolute path, relative path, aws, ubuntu, wsl, powershell | B.U.   | 2025‑12‑30 | Cloud Computing, Linux Basics | lab‑linux‑paths, aws‑ubuntu, cli‑practice, powershell |

----

**← Back to the theory [← Concept → DevOps-03-Concept-03-Linux-Absolute-and-Relative-Paths](../Concepts/Devops-03-Concept-03-Linux-Absolute-and-Relative-Paths.md)**

---

## 🗂️ Topics Covered

- **Absolute vs. Relative Path Navigation** – using `/`, `..`, `.` and `~`.
- **Hostname Manipulation** – viewing, setting, and persisting a custom hostname with `hostnamectl`.
- **Instance Lifecycle Management** – starting, stopping, and verifying EC2 state.
- **SSH Access from Windows** – WSL and PowerShell connection methods.
- **Basic Linux Commands** – `whoami`, `pwd`, `ls`, `history`.

------ 

## 📖 Summary

| **Aspect**           | **Details**                                                                                                                                                                                              |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Goal**             | Practice navigating the Linux filesystem, manipulate hostnames, and control the EC2 instance lifecycle.                                                                                                  |
| **Main Tasks**       | 1️⃣ Start the EC2 instance <br/>2️⃣ SSH in (WSL or PowerShell) <br/>3️⃣ Validate the session <br/>4️⃣ Play with hostname <br/>5️⃣ Explore absolute/relative paths <br/>6️⃣ Shut down / stop the instance |
| **Key Commands**     | `ssh`, `whoami`, `hostname`, `pwd`, `cd`, `sudo hostnamectl set-hostname …`, `sudo poweroff` **or** `sudo shutdown -h now`                                                                               |
| **Expected Outcome** | The instance runs, you can move around the filesystem, change the hostname, and finally stop the VM (it appears **stopped** in the AWS console).                                                         |

----

## 📄 Lab Overview

You will:

1. **Start** the stopped EC2 instance.
2. **Connect** via **WSL** *or* **PowerShell** using the `.pem` key you downloaded earlier.
3. **Run** commands that demonstrate absolute vs. relative navigation, hostname manipulation, and basic instance control.
4. **Clean up** by stopping the instance for future labs.

> **Prerequisite:**
> 
> 1. If the EC2 instance does not yet exist, create it first using the following link: **[Create EC2 instance – Lab Setup Guide](../Labs/Devops-02-Lab-01-Spin-Up-An-EC2-Instance.md)**
> 2. The private key must be stored locally. Remember to keep it secure (`chmod 400 <YOUR_KEY_NAME.pem>`).

---

### What to replace before you run the lab

| Placeholder                               | What to put there                                                                |
| ----------------------------------------- | -------------------------------------------------------------------------------- |
| `<YOUR_WINDOWS_USERNAME>`                 | Your Windows login name (the folder that contains the `keys` directory).         |
| `YOUR_KEY_NAME.pem`                       | The exact name of the PEM file you downloaded from AWS (e.g., `Ubuntu‑KP.pem`).  |
| `ec2‑xx‑xx‑xx‑xx.compute‑1.amazonaws.com` | The public DNS shown in the **Connect → SSH client** pane for **your** instance. |

---

## 1️⃣ ⚡ Start the Instance

1. Open the **AWS Management Console** → **EC2 Dashboard**.
2. Find the instance you’ll work with (e.g., `EC2‑Ubuntu‑Distro`).
3. Choose **Actions → Instance State → Start**.
4. Wait until the status changes to **running**.

---

## 2️⃣ 🔗 Connect to the Instance

You can use **either** WSL (Linux‑style shell) **or** Windows PowerShell.

### Option A – Using **WSL**

bash

```bash
# 1. Open your WSL terminal 
# 2. Go to the folder that holds your private key 
cd /mnt/c/Users/<YOUR_WINDOWS_USERNAME>/keys 

# 3. (Optional) Ensure the key has the correct permissions 
chmod 400 YOUR_KEY_NAME.pem # run only if the file isn’t already 400 

# 4. SSH into the instance (replace the DNS name with the one shown in the EC2 console) 
ssh -i "YOUR_KEY_NAME.pem" ubuntu@ec2-xx-xx-xx-xx.compute-1.amazonaws.com
```

### Option B – Using **PowerShell**

```powershell
# 1. Open a PowerShell window 
# 2. Change to the folder holding your private key 
cd C:\Users\<YOUR_WINDOWS_USERNAME>\keys 

# 3. (PowerShell does not enforce chmod, just make sure the file isn’t world‑readable) 

# 4. SSH into the instance (use the exact public DNS provided in your EC2 instance details) 
ssh -i "YOUR_KEY_NAME.pem" ubuntu@ec2-xx-xx-xx-xx.compute-1.amazonaws.com
```

> **Tip:** Whichever method you choose, the SSH command and the resulting session are identical—you’ll land in the same `ubuntu` user account on the EC2 instance.

---

## 3️⃣ 🖥️ Validate Your Session

| Command    | Expected output                                          |
| ---------- | -------------------------------------------------------- |
| `whoami`   | `ubuntu`                                                 |
| `hostname` | Default AWS‑generated hostname (e.g., `ip-172-31-26-84`) |
| `pwd`      | `/home/ubuntu` (displayed as `~`)                        |
| `ls`       | List of files in the home directory (often empty)        |
| `history`  | Shows previously entered commands                        |

---

### 4️⃣ 🔧 Play with Hostname

bash

```bash
# Change the hostname (requires sudo) 
sudo hostnamectl set-hostname workstation.example.com 
# Verify the change hostname
#You should now see `workstation.example.com`.
```

---

### 5️⃣ 📂 Navigate the Filesystem

bash

```bash
# 1️⃣ Absolute path – go straight to /var
cd /var
pwd          # => /var

# 2️⃣ List contents
ls

# 3️⃣ Relative path – move into the log directory
cd log
pwd          # => /var/log
ls

# 4️⃣ One step back (parent directory)
cd ..
pwd          # => /var

# 5️⃣ Relative path from /var to /var/lib
cd ../lib
pwd          # => /var/lib
ls
```

> **Note:** The tilde (`~`) disappears once you leave the home directory; you’ll see the full path instead.

--------------------

### 6️⃣ 🔁 Return Home & Clean Up

bash

```bash
# Return to your home directory using the tilde shortcut
# Return to your home directory using the tilde shortcut
cd ~

# Verify
pwd   # => /home/ubuntu (displayed as ~)

# When you’re finished, you have two ways to stop the instance:

## Option A – Shut down from inside the SSH session
sudo poweroff          
# or: 
sudo shutdown -h now
```

> **Note:** Both commands (`poweroff` and `shutdown -h now`) halt the VM, after which the instance will appear **stopped** in the AWS console. You can use either one. 
> **Difference:** `shutdown` lets you schedule a halt (e.g., `sudo shutdown -h +5` to stop in 5 minutes) or broadcast a message, while `poweroff` performs an immediate halt with no scheduling options.

Option B – Stop the instance from the AWS console

1. Log out of the SSH session (or simply close the terminal).
2. In the AWS Management Console, select the instance → **Actions → Instance State → Stop** 

**After either option** the instance is in the *stopped* state, and you can safely end the SSH session:

```bash
exit
```

Feel free to use whichever shutdown method best fits your workflow.

----

## ❓ Question & Answer

| #   | Question                                                                     | Answer                                                                                                                                                                                                                                               |
| --- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | **How can I tell if a path is absolute or relative?**                        | An **absolute** path starts with `/` (e.g., `/var/log`). A **relative** path does **not** start with `/` and is resolved from the current working directory (`pwd`).                                                                                 |
| 2   | **Why does `cd ..` move up one level while `cd ../../` moves up two?**       | `..` denotes the parent directory. Chaining them (`../..`) tells the shell to resolve the parent of the parent, moving two levels upward.                                                                                                            |
| 3   | **Are `sudo poweroff` and `sudo shutdown -h now` the same?**                 | Both halt the VM, after which the instance appears **stopped** in the AWS console. The difference: `shutdown` can be scheduled (`sudo shutdown -h +5`) or broadcast a message; `poweroff` performs an immediate halt with no scheduling options.     |
| 4   | **After changing the hostname, why does my prompt still show the old name?** | The hostname change takes effect immediately, but the shell prompt may cache the old value. Run `exec bash` (or log out/in) to refresh.                                                                                                              |
| 5   | **How do I verify the instance really stopped after `sudo poweroff`?**       | The SSH session ends. In the AWS Console, the **Instance State** column changes from **running** to **stopped**. You can also confirm via the AWS CLI: `aws ec2 describe-instances --instance-ids <id>` which returns `"State": {"Name":"stopped"}`. |

-----------

**← Back to the theory [← Concept → DevOps-03-Concept-03-Linux-Absolute-and-Relative-Paths](../Concepts/Devops-03-Concept-03-Linux-Absolute-and-Relative-Paths.md)**

---
