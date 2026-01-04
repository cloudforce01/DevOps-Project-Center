# 🧪 **Devops‑06‑Lab‑05 – Globbing and Wildcard **

### **📊 Metadata Information**

| **Description**                                                                                                                               | **Est.  Read Time** | **Est.  Lab Time** | **Total Time** | **Keywords**                                                   | **Author** | **Date**   | **Categories**                                        | **Tags**                                     |
| --------------------------------------------------------------------------------------------------------------------------------------------- | ------------------- | ------------------ | -------------- | -------------------------------------------------------------- | ---------- | ---------- | ----------------------------------------------------- | -------------------------------------------- |
| Hands‑on lab to explore globbing patterns, create multiple directories/files, and practise selective listings on a remote Ubuntu EC2 instance | 10‑15 min           | 15‑20 min          | 25‑35 min      | linux, cli, globbing, wildcard, aws, ec2, wsl, powershell, ssh | B.U.       | 2026‑01‑04 | Cloud Computing, Linux Basics, File‑System Navigation | linux‑fundamentals, cli‑globbing, aws‑ubuntu |

--------

**← Back to the theory** <a href="../Concepts/Devops-06-Concept-06-Globbing-and-Wildcards.md#metadata-information" target="_blank" rel="noreferrer noopener" title="Ctrl/Cmd‑click or Middle‑click to open in a new tab">** ← Devops-06-Concept-06-Globbing-and-Wildcards - jump to 📊 Metadata Information** </a>

---

### 📚 Topics Covered

- Understanding and using `?`, `*`, `[ ]`, `{ }` patterns
- Listing files/directories with selective globbing
- Creating many directories/files with brace expansion
- Combining multiple paths in a single command
- Safe testing of glob expansions with `echo`

---

### 📋 Summary

In this lab you will connect to a remote Ubuntu EC2 instance (via PowerShell or WSL), then perform a series of tasks that demonstrate how globbing simplifies bulk operations. You will list, create, and verify files/directories using the patterns introduced in the concept.

---

### 🗂️ Lab Overview

If you don’t already have an EC2 instance, launch an Ubuntu instance (t2.micro) and open an SSH session from PowerShell (`ssh ubuntu@<public‑ip>`). Once connected, follow the steps below or refer to the previous lab for the start‑up instructions: **<a href="../Labs/Devops-02-Lab-01-Spin-Up-An-EC2-Instance.md#step‑by‑step-launching-an-ubuntu-ec2-instance" target="_blank" rel="noreferrer noopener" title="Ctrl/Cmd‑click or Middle‑click to open in a new tab">Create EC2 Instance - Lab Setup Guide</a>**.

1️⃣ **Verify the working directory** – `pwd`  

2️⃣ **List files with basic globs** – `ls *`, `ls ?.conf`  

3️⃣ **Create multiple directories** – `mkdir project{1..10}`  

4️⃣ **Create a series of log files** – `touch 202512{01-31}.log`  

5️⃣ **List selective entries in `/etc`** using the patterns from the concept (e.g., `ls -d /etc/[ab]*`)  

6️⃣ **Combine paths** – `ls /var/{log,lib}`  

7️⃣ **Safe preview** – use `echo` before any destructive command  

8️⃣ **Cleanup** – remove the test directories/files you created

---

### 🛠️ Detailed Steps

#### 1️⃣ Connect & Verify

bash

```bash
ssh ubuntu@<your‑ec2‑public‑ip> pwd
```

#### 2️⃣ Basic Glob Listings

bash

```bash
#All entries in the current folder 
ls * 
# Files with exactly one character before .conf 
ls /etc/?.conf 
# Two‑character entries in /etc 
ls -d /etc/??
```

#### 3️⃣ Bulk Directory Creation

bash

```bash
mkdir project{1..10} 
ls project*
```

#### 4️⃣ Bulk Log‑File Creation

bash

```bash
touch 202512{01-31}.log ls 202512*.log
```

#### 5️⃣ Selective `/etc` Listings

bash

```bash
# Starts with a or b 
ls -dl /etc/[ab]* 
# Does NOT start with a or b 
ls -dl /etc/[!ab]* 
# Range a‑f 
ls -dl /etc/[a-f]* 
# Excluding a‑v (i.e., showing u‑z) 
ls -dl /etc/[!a-v]*
```

#### 6️⃣ Combine Multiple Paths

bash

```bash
ls /var/{log,lib}
```

#### 7️⃣ Safe Preview with `echo`

Before removing anything, preview the expansion:

bash

```bash
echo rm -r project{1..10}
```

Only execute the `rm` once you are sure the list is correct.

#### 8️⃣ Cleanup

bash

```bash
rm -r project{1..10} 
rm 202512{01-31}.log
```

---

### ❓ Q&A

| #   | **Question**                                                                            | **Answer**                                                                                                                                                                   |
| --- | --------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Which glob pattern is most useful for selecting files that end with `.conf`?            | `*.conf` – the `*` matches any preceding characters.                                                                                                                         |
| 2   | How can you list files that start with a digit followed by exactly two more characters? | `ls -d [0-9]??` – `[0-9]` matches a digit, `??` matches two additional characters.                                                                                           |
| 3   | What is the advantage of using `echo` before a destructive command that uses globs?     | It shows the exact list of files the glob will expand to, preventing accidental deletion of unintended files.                                                                |
| 4   | How does brace expansion differ from globbing?                                          | Brace expansion (`{1..10}`) generates a **static list** of strings before the command runs, while globbing (`*`, `?`, `[ ]`) matches existing filesystem entries at runtime. |
| 5   | If a glob matches no files, what does the shell do by default?                          | The pattern is left unchanged and passed literally to the command (e.g., `ls *.nothing` prints `*.nothing`). Some shells can enable `nullglob` to treat it as an empty list. |
| 6   | Can you combine multiple character classes in one pattern? Give an example.             | Yes. Example: `ls /etc/[a-c][0-9]*` matches files that start with a‑c followed by a digit.                                                                                   |
| 7   | Why might `ls -d /etc/[ab]*` be preferable to `ls /etc/a* /etc/b*`?                     | The single pattern is shorter, easier to read, and guarantees the results are sorted together rather than in two separate listings.                                          |

---

### 🔙 Back to the Concept

**← Back to the theory** <a href="../Concepts/Devops-06-Concept-06-Globbing-and-Wildcards.md" target="_blank" rel="noreferrer noopener" title="Ctrl/Cmd‑click or Middle‑click to open in a new tab">** ← Devops-06-Concept-06-Globbing-and-Wildcards - jump to 📊 Metadata Information** </a>

-----
