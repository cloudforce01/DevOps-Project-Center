# 🚀 Devops‑07‑Concept‑07 – File & Directory Management on Linux

## 📊 Metadata Information

| Description                                                                                        | Est. Read Time | Keywords                                                                           | Author | Date       | Categories                                            | Tags                                         |
| -------------------------------------------------------------------------------------------------- | -------------- | ---------------------------------------------------------------------------------- | ------ | ---------- | ----------------------------------------------------- | -------------------------------------------- |
| Overview of basic Linux commands for creating, copying, moving and deleting files and directories. | 10‑15 min      | linux, cli, file‑management, ubuntu, wsl, powershell, cp, mv, rm, mkdir, touch, vi | B.U.   | 2026‑01‑05 | Cloud Computing, Linux Basics, File‑System Navigation | linux‑fundamentals, cli‑file‑ops, aws‑ubuntu |

### 🔗 Lab linked to this concept

 <a href="../Labs/Devops-07-Lab-06-File-Directory-Management.md#metadata-information" target="_blank" rel="noreferrer noopener" title="Ctrl/Cmd‑click or Middle‑click to open in a new tab">**▶️ Run the Lab → Devops-07-Lab-06-File-Directory-Management - jump to 📊 Metadata Information** </a>

---

## 📚 Summary

This concept introduces the core Linux commands you need to manage files and directories on a remote Ubuntu instance. You will learn the syntax, most‑used options, and typical pitfalls when copying, moving, renaming or deleting resources.

---

### 1️⃣ Copying Files – `cp`

| Option | Meaning                                                                                           | Example                     |
| ------ | ------------------------------------------------------------------------------------------------- | --------------------------- |
| `-v`   | Verbose – shows each file processed                                                               | `cp -v source.txt /tmp/`    |
| `-i`   | Interactive – ask before overwriting                                                              | `cp -i *.conf /etc/`        |
| `-u`   | Update – copy only when the **source is newer** *or* when the destination file does **not** exist | `cp -u report.log /backup/` |
| `-r`   | Recursive – copy directories and their contents                                                   | `cp -rv project/ /tmp/`     |

> **Note:** Without `-i`, Ubuntu overwrites existing files silently.

---

### 2️⃣ Moving & Renaming – `mv`

- Syntax: `mv <source>… <destination>`
- If `<destination>` is a **file name** that does not exist → the command **renames** the source.
- If `<destination>` is an **existing file** → it is **overwritten**.
- If `<destination>` is a **directory** → the source(s) are moved inside it.

bash

```bash
#Rename a file 
mv old-name.txt new-name.txt 
# Move several files into a directory 
mv file1.txt file2.txt /tmp/ 
```

---

### 3️⃣ Removing Files & Directories – `rm`

| Option | Meaning                                           | Example                    |
| ------ | ------------------------------------------------- | -------------------------- |
| `-v`   | Verbose – list each removal                       | `rm -v temp.txt`           |
| `-f`   | Force – ignore nonexistent files, never prompt    | `rm -f *.bak`              |
| `-r`   | Recursive – delete directories and their contents | `rm -rv /tmp/old-project/` |
| `-i`   | Interactive – ask before each removal             | `rm -i secret.txt`         |

> **Caution:** `rm -rf /` would erase the whole filesystem. Use with extreme care.

---

### 4️⃣ Creating Files & Directories

| Command      | Purpose                                                      | Example                     |
| ------------ | ------------------------------------------------------------ | --------------------------- |
| `touch`      | Create an empty file or update timestamps                    | `touch README.md`           |
| `mkdir`      | Make a new directory (`-p` creates parents as needed)        | `mkdir -p projects/app/src` |
| `vi` / `vim` | Text editor – `i` to insert, `Esc` then `:wq` to save & quit | `vi notes.txt`              |

---

### 5️⃣ Common Workflows (Demo)

bash

```bash
#1. Create a directory and a file inside it 
mkdir -p ~/demo/project 
touch ~/demo/project/info.txt 

# 2. Write a line into the file (using echo for brevity) 
echo "Learning Linux file ops" > ~/demo/project/info.txt 

# 3. Copy the whole project to /tmp with verbosity 
cp -rv ~/demo/project /tmp/ 

# 4. Rename the copied file 
mv /tmp/project/info.txt /tmp/project/summary.txt 

# 5. Remove the original directory recursively 
rm -rv ~/demo/project
```

---

## ❓ Q&A

| #   | Question                                                                       | Answer                                                                                                           |
| --- | ------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------- |
| 1   | How can I copy a directory **without** its sub‑directories?                    | Use `cp -v source_dir/* destination/` – the wildcard expands only the files in the top level.                    |
| 2   | What does `cp -u` do when the destination file is **newer** than the source?   | It skips the copy because the destination is already up‑to‑date.                                                 |
| 3   | When should I prefer `mv` over `cp` + `rm`?                                    | When you simply need to relocate or rename a file – `mv` is atomic and faster because it doesn’t duplicate data. |
| 4   | How can I safely delete many files that match a pattern?                       | Use `rm -i pattern*` to be prompted for each file, or first preview with `ls pattern*`.                          |
| 5   | Is there a way to see what `rm -r` would delete **without** actually deleting? | Run `echo rm -rv /path/to/dir/*` – `echo` shows the expanded command without execution.                          |
| 6   | Can `cp` preserve file permissions and timestamps?                             | Yes, add `-p` (or `--preserve=mode,ownership,timestamps`).                                                       |

---

### 🔗 Lab linked to this concept

 <a href="../Labs/Devops-07-Lab-06-File-Directory-Management.md#metadata-information" target="_blank" rel="noreferrer noopener" title="Ctrl/Cmd‑click or Middle‑click to open in a new tab">**▶️ Run the Lab → Devops-07-Lab-06-File-Directory-Management - jump to 📊 Metadata Information** </a>
