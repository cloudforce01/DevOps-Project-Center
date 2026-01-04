# 🚀 **Devops‑06‑Concept‑06 – Globbing and Wildcards**

### **📊 Metadata Information**

| **Description**                                                                                | **Est. Read Time** | **Keywords**                                                              | **Author** | **Date**   | **Categories**                                        | **Tags**                                     |
| ---------------------------------------------------------------------------------------------- | ------------------ | ------------------------------------------------------------------------- | ---------- | ---------- | ----------------------------------------------------- | -------------------------------------------- |
| Symbols and patterns that let you match groups of files or directories in the Linux filesystem | 10‑15 min          | linux, cli, globbing, wildcard, pattern‑matching, ubuntu, wsl, powershell | B.U.       | 2026‑01‑04 | Cloud Computing, Linux Basics, File‑System Navigation | linux‑fundamentals, cli‑globbing, aws‑ubuntu |

---

### 🔗 Lab linked to this concept

 <a href="../Labs/Devops-06-Lab-05-Globbing-and-Wildcards.md#metadata-information" target="_blank" rel="noreferrer noopener" title="Ctrl/Cmd‑click or Middle‑click to open in a new tab">**▶️ Run the Lab → Devops-06-Lab-05-Globbing-and-Wildcards.md - jump to 📊 Metadata Information** </a>

---

### 📚 Summary

This concept introduces the globbing (wildcard) syntax used in Bash and other shells. You will learn the meaning of each special character, how to combine them, and how to apply them for bulk operations such as creating many directories or selecting files with specific naming patterns.

---

## 1️⃣ Introduction to Globbing

Globbing (also called wildcard expansion) lets you specify **path‑pattern symbols** that the shell expands to matching filenames. It is essential for efficient navigation and batch processing on Linux systems.

| **Symbol** | **Meaning**                            | **Example**                                                               |
| ---------- | -------------------------------------- | ------------------------------------------------------------------------- |
| `.`        | Current directory                      | `cd .`                                                                    |
| `..`       | Parent directory                       | `cd ..`                                                                   |
| `~`        | Home directory of the logged‑in user   | `ls ~`                                                                    |
| `~dev1`    | Home directory of user *dev1*          | `ls ~dev1`                                                                |
| `?`        | Exactly one character                  | `ls /etc/?.conf` matches `/etc/a.conf` but not `/etc/ab.conf`             |
| `??`       | Exactly two characters                 | `ls /etc/??.conf`                                                         |
| `*`        | Zero or more characters                | `ls a*` matches `a`, `ab`, `abc.txt`                                      |
| `[ab]`     | One character, either *a* or *b*       | `ls /etc/[ab]*`                                                           |
| `[!ab]`    | One character, **not** *a* nor *b*     | `ls /etc/[!ab]*`                                                          |
| `[a‑j]`    | Range of characters                    | `ls /etc/[a‑j]*`                                                          |
| `[!a‑j]`   | Exclude a range                        | `ls /etc/[!a‑j]*`                                                         |
| `{1..20}`  | Brace expansion – generates a sequence | `mkdir dir{1..20}` creates `dir1` … `dir20`                               |
| `{01‑31}`  | Brace expansion with leading zeros     | `touch 202512{01‑31}.log` creates log files for each day of December 2025 |

---

## 2️⃣ Using Globs for Bulk Creation

bash

```bash
#Create a series of directories named project1 … project10 
mkdir project{1..10} 
# Create daily log files for December 2025 
touch 202512{01-31}.log 
```

---

## 3️⃣ Practical Globbing Commands

| **Task**                                                             | **Command**                                   | **Explanation**                     |
| -------------------------------------------------------------------- | --------------------------------------------- | ----------------------------------- |
| List files in the current directory                                  | `ls`                                          | Simple listing                      |
| List files in the parent directory                                   | `ls ..`                                       | Shows `..` contents                 |
| Change to `/var/log`                                                 | `cd /var/log`                                 | Moves to log folder                 |
| List files in the home directory                                     | `ls ~`                                        | Uses `~` shortcut                   |
| List two‑character entries in `/etc`                                 | `ls -d /etc/??`                               | `??` matches exactly two characters |
| List entries that start with `r` and have three characters in `/etc` | `ls -d /etc/r??`                              | `r??` = `r` + two more chars        |
| List everything that starts with `r` in `/etc`                       | `ls -d /etc/r*`                               | `*` matches any length              |
| List files ending with `.conf` in `/etc` (long format)               | `ls -dl /etc/*.conf`                          | `*.conf` selects conf files         |
| List entries that start with `a` or `b` in `/etc`                    | `ls -dl /etc/[ab]*`                           | Character class                     |
| List entries **not** starting with `a` or `b`                        | `ls -dl /etc/[!ab]*`                          | Negated class                       |
| List entries that start with letters `a`‑`f`                         | `ls -dl /etc/[a-f]*`                          | Range                               |
| List entries that start with `u`‑`z` (or exclude `a`‑`v`)            | `ls -dl /etc/[u-z]*` or `ls -dl /etc/[!a-v]*` | Two ways to achieve the same result |

---

## 4️⃣ Combining Paths

bash

```bash
# List contents of both /var/log and /var/lib in one command 
ls /var/{log,lib}
```

---

## 5️⃣ Quick Reference Cheat‑Sheet

| **Action**                    | **Command**              |
| ----------------------------- | ------------------------ |
| Show current directory        | `pwd`                    |
| List all files (colourised)   | `ls --color=auto`        |
| List hidden files             | `ls -a`                  |
| List files matching a pattern | `ls *.conf`              |
| Create multiple directories   | `mkdir dir{1..5}`        |
| Create a range of files       | `touch file{01..10}.txt` |
| Show expanded glob (dry run)  | `echo /etc/[a-c]*`       |

---

## ❓ Q&A

| #   | **Question**                                                                          | **Answer**                                                                                                         |
| --- | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| 1   | How does `*` differ from `?` in a pattern?                                            | `*` matches **zero or more** characters, while `?` matches **exactly one** character.                              |
| 2   | When would you use `[!a‑j]` instead of `[a‑j]`?                                       | `[!a‑j]` selects files whose first character is **not** in the range `a`‑`j`; useful for excluding a set of names. |
| 3   | Can brace expansion be combined with globs?                                           | Yes. Example: `ls /var/log/*{error,warning}.log` lists files ending with `error.log` or `warning.log`.             |
| 4   | Why might `ls -d /etc/??` return fewer results than expected?                         | It only matches entries whose **basename** is exactly two characters long; longer names are ignored.               |
| 5   | How can you verify what a glob will expand to before executing a destructive command? | Use `echo` first: `echo /etc/[ab]*` shows the matched paths without performing any operation.                      |
| 6   | Is globbing performed by the shell or the command itself?                             | The **shell** expands globs before invoking the command; the command receives the list of matching filenames.      |

---

### 🔗 Lab linked to this concept

 <a href="../Labs/Devops-06-Lab-05-Globbing-and-Wildcards.md#metadata-information" target="_blank" rel="noreferrer noopener" title="Ctrl/Cmd‑click or Middle‑click to open in a new tab">**▶️ Run the Lab → Devops-06-Lab-05-Globbing-and-Wildcards.md - jump to 📊 Metadata Information** </a>

------
