## Devops‑04-Concept- 04–Creating Files-and-Directories-in-Linux

## Metadata Information

| Description                                                                                                                               | Estimated Read Time | Keywords                                                          | Author | Date       | Categories                    | Tags                                  |
| ----------------------------------------------------------------------------------------------------------------------------------------- | ------------------- | ----------------------------------------------------------------- | ------ | ---------- | ----------------------------- | ------------------------------------- |
| Intro to the Linux shell on an AWS Ubuntu instance: navigation (pwd, cd, ls), file‑system basics (touch, mkdir), and simple Vim editing.. | 7‑10 min            | linux, filesystem, absolute path, relative path, aws, ubuntu, wsl | B.U.   | 2026‑01‑01 | Cloud Computing, Linux Basics | linux‑fundamentals, paths, aws‑ubuntu |

--------------------


👉 Ready for the hands‑on part? The theory is covered above. When you’re comfortable with the concepts, jump straight to the practical lab:

<a href="../Labs/Devops-04-Lab-03-Creating-Files-and-Directories-on-Remote-Ubuntu-Instance.md#metadata-information" target="_blank" rel="noreferrer noopener" title="Ctrl/Cmd‑click or Middle‑click to open in a new tab">▶️ **Run the Lab** → Devops-04-Lab-03-Creating-Files-and-Directories-on-Remote-Ubuntu-Instance - jump to "📊 Metadata Information </a>

----------



## 📖 Summary

| Topic                     | Key Take‑away                                                                                                 |
| ------------------------- | ------------------------------------------------------------------------------------------------------------- |
| **Shell identification**  | Use `echo $SHELL` to display the absolute path of the current shell (e.g., `/bin/bash`).                      |
| **`ls` colour coding**    | White = file, Dark blue = directory, Light blue = symlink, Green background = world‑rw‑x permission.          |
| **Permission model**      | `ubuntu` can write only in locations it owns (e.g., `/home/ubuntu`). Use `sudo` for other paths.              |
| **Creating files / dirs** | `touch <filename>` → empty file; `mkdir <dirname>` → empty directory; `mkdir -p a/b/c` → nested directories.  |
| **Case sensitivity**      | Filenames are case‑sensitive (`aws` ≠ `AWS`).                                                                 |
| **CLI editors**           | `vim/vi` (modal), `nano`, `emacs`, `gedit`. `vim` basics: `i` → insert, `Esc` → command, `:wq` → save + quit. |
| **History timestamps**    | Add `export HISTTIMEFORMAT="%F %T "` to `~/.bashrc` (or `~/.zshrc`) to see timestamps in `history`.           |

### 1️⃣ What is a Shell?

A shell is the program that gives you a Command‑Line Interface (CLI) to interact with the operating system. It is itself an application, just like any other program you run on your computer. There are many different shells available, such as bash, sh, zsh, csh, and PowerShell on Windows. On most Linux, Unix, and macOS systems the default shell is Bash (or a symbolic link to `sh`).

To find out which shell you are currently using, run the following command:

bash

```bash
echo $SHELL
```

## 2️⃣ Colors in `ls` output (default theme)

| Color                | Meaning                                                                |
| -------------------- | ---------------------------------------------------------------------- |
| **White**            | Regular file                                                           |
| **Dark blue**        | Directory                                                              |
| **Light blue**       | Symbolic link                                                          |
| **Green background** | File with world‑read/write/execute permission (accessible to everyone) |

### 3️⃣ Permissions basics

- The default **ubuntu** user can create files only in locations where it has write permission (e.g., its home directory).
- To write elsewhere (e.g., `/opt`, `/var/www`), prepend the command with **`sudo`**.

### 4️⃣ Creating empty files & directories

| Command            | Purpose                                                                |
| ------------------ | ---------------------------------------------------------------------- |
| `touch <filename>` | Creates an empty file (or updates the timestamp if it already exists). |
| `mkdir <dirname>`  | Creates an empty directory.                                            |
| `mkdir -p a/b/c`   | Creates nested directories in one step.                                |

> **Note:** Linux file‑system names are **case‑sensitive** – `aws` and `AWS` are distinct objects.

### 5️⃣ Text editors available from the CLI

- **vi / vim** – modal editor (command mode ↔ insert mode).
  - Press `i` to enter **insert** mode.
  - Press `Esc` to return to **command** mode.
  - Save & quit: `:w` (write), `:q` (quit), `:wq` (write + quit).
- **nano**, **emacs**, **gedit** (GUI) are alternatives.

### 6️⃣ History timestamps (optional)

Add the following line to `~/.bashrc` (or `~/.zshrc`) to prefix each command in the history with a timestamp:

```bash
export HISTTIMEFORMAT="%F %T "
```

After reloading the shell (`source ~/.bashrc`), `history` will display timestamps.

### 7️⃣ Quick reference cheat‑sheet

| Action                                | Command                          |
| ------------------------------------- | -------------------------------- |
| Show current directory                | `pwd`                            |
| List files/directories (colorized)    | `ls --color=auto`                |
| Create a directory                    | `mkdir mydir`                    |
| Create an empty file                  | `touch myfile.txt`               |
| Edit a file with **vim**              | `vim myfile.txt`                 |
| Add a line in **vim** (after opening) | `o` → type → `Esc` → `:wq`       |
| Switch to **root** temporarily        | `sudo -i`                        |
| Set history timestamps                | `export HISTTIMEFORMAT="%F %T "` |

## ❓ Question & Answer

| #   | Question                                                                   | Answer                                                                                                         |
| --- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| 1   | **What does `echo $SHELL` show?**                                          | It prints the absolute path of the shell program currently being used (e.g., `/bin/bash`).                     |
| 2   | **Why are colours useful in `ls`?**                                        | They give a quick visual cue about file types and permission levels, helping you avoid mistakes.               |
| 3   | **Can I create a file in `/etc` as the `ubuntu` user?**                    | No – you need `sudo` because `/etc` is owned by `root`. Use `sudo touch /etc/example`.                         |
| 4   | **What is the difference between `touch` and `vim` when creating a file?** | `touch` creates an empty file (no content). `vim` opens an editor so you can add content immediately.          |
| 5   | **How do I make the history timestamps permanent?**                        | Add `export HISTTIMEFORMAT="%F %T "` to your shell’s rc file (`~/.bashrc` or `~/.zshrc`) and reload the shell. |

-----------

👉 Ready for the hands‑on part? The theory is covered above. When you’re comfortable with the concepts, jump straight to the practical lab:

<a href="../Labs/Devops-04-Lab-03-Creating-Files-and-Directories-on-Remote-Ubuntu-Instance.md#metadata-information" target="_blank" rel="noreferrer noopener" title="Ctrl/Cmd‑click or Middle‑click to open in a new tab">▶️ **Run the Lab** → Devops-04-Lab-03-Creating-Files-and-Directories-on-Remote-Ubuntu-Instance - jump to "📊 Metadata Information </a>

-----
