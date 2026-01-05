# 🧪 Devops‑07‑Lab‑07 – File & Directory Management on Ubuntu

## 📊 Metadata Information

| Description                                                                                           | Est. Read Time | Est. Lab Time | Total Time | Keywords                                                  | Author | Date       | Categories                                            | Tags                                         |
| ----------------------------------------------------------------------------------------------------- | -------------- | ------------- | ---------- | --------------------------------------------------------- | ------ | ---------- | ----------------------------------------------------- | -------------------------------------------- |
| Hands‑on lab to practice `cp`, `mv`, `rm`, `mkdir`, `touch` and `vi` on a remote Ubuntu EC2 instance. | 10‑15 min      | 15‑20 min     | 25‑35 min  | linux, cli, file‑management, ubuntu, wsl, powershell, ssh | B.U.   | 2026‑01‑05 | Cloud Computing, Linux Basics, File‑System Navigation | linux‑fundamentals, cli‑file‑ops, aws‑ubuntu |

----------------------

 ← **Back to the theory** ← <a href="../Concepts/Devops-07-Concept-07-File-Directory-Management.md#metadata-information" target="_blank" rel="noreferrer noopener" title="Ctrl/Cmd‑click or Middle‑click to open in a new tab">**Devops-07-Concept-07-File-Directory-Management - jump to 📊 Metadata Information** </a>

 ---

## 📚 Topics Covered

- Using `cp` with options `-v`, `-i`, `-u`, `-r`
- Moving & renaming files with `mv`
- Deleting files/directories safely with `rm` (`-v`, `-f`, `-r`, `-i`)
- Creating files (`touch`) and directories (`mkdir -p`)
- Editing a file with `vi`/`vim` (insert mode, save & quit)
- Combining commands to perform a realistic workflow

---

## 📋 Summary

In this lab you will connect to a remote Ubuntu EC2 instance (via PowerShell or WSL) and execute a series of commands that cover the full lifecycle of file and directory handling. Each step includes a verification command (`ls`, `cat`, `pwd`) to confirm the expected outcome.

---

## 🗂️ Lab Overview

**Prerequisites** – An Ubuntu EC2 instance (or any remote Ubuntu VM) reachable via SSH.

1️⃣ **Connect & Verify** – `ssh ubuntu@<public‑ip>` → `pwd`

2️⃣ **Create a Working Directory** – `mkdir -p ~/lab07/project && cd $_`

3️⃣ **Create & Edit a File** – `touch notes.txt` → `vi notes.txt` (add “Learning file ops”) → `:wq`

4️⃣ **Copy Files** – Demonstrate `cp` with various flags

5️⃣ **Move / Rename** – Use `mv` for relocation and renaming

6️⃣ **Delete Safely** – Practice `rm` with interactive and forced options

7️⃣ **Clean‑Up** – Remove all created artefacts

---

### Detailed Steps

#### 1️⃣ Connect & Verify

bash

```bash
ssh ubuntu@<your‑ec2‑public‑ip> 
pwd # should show /home/ubuntu
```

#### 2️⃣ Create Working Directory

bash

```bash
mkdir -p ~/lab07/project 
cd ~/lab07/project 
ls -l # empty directory
```

#### 3️⃣ Create & Edit a File

bash 

```bash
touch notes.txt 
vi notes.txt # press i, type "Learning file ops", Esc, :wq 
cat notes.txt # verify content

touch sample.txt
vi sample.txt # press i, type "Sample file ops", Esc, :wq 
cat sample.txt # verify content
```

#### 4️⃣ Copy Files

bash

```bash
# a) Simple copy with verbosity 
cp -v notes.txt /tmp/ 
# b) Copy only if newer 
cp -u notes.txt /tmp/ 
# c) Recursive copy of the whole project 
mkdir /tmp/lab07-copy
cp -rv . /tmp/lab07-copy
```

#### 5️⃣ Move / Rename

bash

```bash
# a) Rename within the same directory
mv notes.txt diary.txt 
# b) Move to /tmp 
mv diary.txt /tmp/ 
# c) Move multiple files into a new directory 
mkdir /tmp/archive 
mv /tmp/sample.txt /tmp/diary.txt /tmp/archive/
```

#### 6️⃣ Delete Safely

bash

```bash
# -------------------------------------------------
# 1️⃣ Interactive delete of a single file
# -------------------------------------------------
# Delete it interactively – you will be prompted to confirm
rm -i /tmp/diary.txt


# -------------------------------------------------
# 2️⃣ Force‑delete all .txt files in /tmp
# -------------------------------------------------
# Create a few .txt files for the demo
touch /tmp/file1.txt /tmp/file2.txt /tmp/file3.txt

# Remove them all without prompting, showing each removal
rm -vf /tmp/*.txt
rm -vf /tmp/archive


# -------------------------------------------------
# 3️⃣ Recursive delete of a directory tree
# -------------------------------------------------
# Build a small directory tree under /tmp/lab07
mkdir -p /tmp/lab07-copy/subdir1
mkdir -p /tmp/lab07-copy/subdir2
touch /tmp/lab07-copy/fileA.txt
touch /tmp/lab07-copy/subdir1/fileB.txt
touch /tmp/lab07-copy/subdir2/fileC.txt

# Verify the structure before removal (install "tree" if you don’t have it)
#   sudo apt-get install tree   # Debian/Ubuntu
tree /tmp/lab07-copy

# Recursively delete the whole tree, showing what gets removed
rm -rv /tmp/lab07-copy
```

#### 7️⃣ Clean‑Up

bash

```bash
cd ~ 
rm -rv ~/lab07
```

---

## ❓ Q&A

| #   | Question                                                                              | Answer                                                                                                                               |
| --- | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| 1   | What happens if I run `cp -r dir1 dir2` and **dir2** already exists?                  | The contents of **dir1** are copied **into** **dir2**, preserving the original directory name (`dir2/dir1/...`).                     |
| 2   | How can I preview which files `rm -r` will delete before actually removing them?      | Use `echo rm -rv /path/to/dir/*` or first run `ls -R /path/to/dir` to list recursively.                                              |
| 3   | Why does `mv source/ dest/` sometimes ask for confirmation?                           | If `dest/` already contains a file with the same name, `mv` will overwrite it silently unless you use the `-i` (interactive) option. |
| 4   | Can `cp -u` be combined with `-r`?                                                    | Yes – `cp -ru source_dir/ dest_dir/` copies only newer files recursively.                                                            |
| 5   | Is there a way to copy a file **preserving** its original permissions and timestamps? | Add the `-p` flag: `cp -vp source.txt /tmp/`.                                                                                        |
| 6   | How do I create an empty file **and** set its modification time to a specific date?   | Use `touch -t YYYYMMDDhhmmss filename`. Example: `touch -t 202601010800 myfile.txt`.                                                 |

--- 

← **Back to the theory** ← <a href="../Concepts/Devops-07-Concept-07-File-Directory-Management.md#metadata-information" target="_blank" rel="noreferrer noopener" title="Ctrl/Cmd‑click or Middle‑click to open in a new tab">**Devops-07-Concept-07-File-Directory-Management - jump to 📊 Metadata Information** </a>

-------------
