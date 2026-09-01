# Instal and configure git on local system and perform basic git operations.

---

## 1. Overview

Git is a version control system. It keeps track of changes to your files over time and lets you save, undo, and share your work. When you use Git together with GitHub, your code moves through four stages:

```
Working Directory --> Staging Area --> Local Repository --> GitHub Remote
   (git add)           (git commit)                          (git push)
```

- **Working Directory:** The normal folder on your computer where you create and edit files. This is just a regular folder until Git is told to track it.
- **Staging Area:** A waiting area where you place the specific changes you want to save next. This lets you choose exactly what goes into each commit, instead of saving everything at once.
- **Local Repository:** Git's private database, stored in a hidden `.git` folder. Every time you commit, a permanent snapshot of your staged changes is stored here on your own machine.
- **GitHub Remote:** An online copy of your repository hosted on GitHub. Pushing sends your local commits there, so your code is backed up and can be shared with others.

Understanding these four stages makes the rest of the commands easier to follow, since each command below simply moves your files from one stage to the next.

---

## 2. Installing Git on Windows

Windows does not come with Git installed, so it must be downloaded and set up manually.

1. Open your browser and go to [git-scm.com](https://git-scm.com/). This is the official Git website, so it is safe to download from here.
2. Click **Download for Windows**, then choose the 64-bit standalone installer. This matches almost all modern Windows computers.
3. Once downloaded, run the installer file. During setup, you will be shown a series of option screens. Use the following choices:
   - **Destination folder:** Leave this at the default location.
   - **Components:** Enable "Git Bash Here" and "Git GUI Here." This adds convenient right-click options in File Explorer.
   - **Default editor:** Choose Vim, or Visual Studio Code if you already use it. This is only used if Git ever opens a text editor for you, such as when writing a longer commit message.
   - **Default branch name:** Set this to `main`. This decides what your first branch will be called in new repositories.
   - **PATH option:** Choose "Git from the command line and also from third-party software." This allows Git to be used from any terminal, not just Git Bash.
   - **SSH executable:** Choose "Use bundled OpenSSH." This is the version of SSH that comes packaged with Git and works without extra setup.
   - **Line endings:** Choose "Checkout Windows-style, commit Unix-style." Windows and other operating systems handle the invisible end-of-line characters in text files differently; this setting prevents unnecessary file changes from being detected due to that difference.
   - **Terminal emulator:** Choose MinTTY, which is the default terminal window used by Git Bash.
   - **Credential helper:** Choose "Git Credential Manager." This safely stores your GitHub login so you are not asked to sign in every time.
4. Click **Install** and wait for the process to finish, then click **Finish**.

### Verify installation

Open Git Bash and run:

```bash
git --version
```

If Git installed correctly, this will print a version number, confirming that the `git` command is ready to use.

---

## 3. Initial Configuration

Before making any commits, Git needs to know who you are, since every commit is labeled with an author name and email.

```bash
git config --global user.name "4IK25CS217"
git config --global user.email "2025cs_surajsp_g@nie.ac.in"
```

- The `--global` flag means these settings apply to every Git repository on your computer, not just one project.
- `user.name` and `user.email` should match the identity you plan to use, ideally the same email associated with your GitHub account.
- `init.defaultBranch main` ensures every new repository starts with a branch named `main` instead of the older default name `master`.

To confirm your settings were saved correctly, run:

```bash
git config --list
```

This displays all current Git configuration values, including the ones you just set.

---

## 4. Creating a Project Folder and File

This step creates a sample project folder and a text file to practice with, entirely from the terminal.

```bash
cd ~
mkdir CDD-LAB-01
cd CDD-LAB-01
```

- `cd ~` moves you to your home directory, a consistent starting point.
- `mkdir project-folder` creates a new, empty folder named `CDD-LAB-01`.
- `cd CDD-LAB-01` moves you inside that new folder so any following commands apply there.

```bash
echo "Header: My First Git Log" > notes.txt
echo "Created on: 2026-08-31" >> notes.txt
echo "Environment: Windows Git Bash" >> notes.txt
```

- `echo "text" > notes.txt` creates a new file called `notes.txt` and writes the given text into it. If the file already existed, this would erase its previous content and replace it.
- `echo "text" >> notes.txt` adds a new line to the end of the file without deleting what is already there. The double arrow (`>>`) means "append," while the single arrow (`>`) means "overwrite."

To check that the file was created correctly:

```bash
ls -la
```

This lists all files in the current folder, including hidden ones, along with details such as size and permissions.

---

## 5. Local Git Workflow

These commands turn the folder into a Git repository and save your first snapshot.

```bash
git init
```

This creates a hidden `.git` folder inside `project-folder`, turning it into a Git repository. From this point on, Git can track changes to any file inside it.

```bash
git status
```

This shows the current state of your files. At this point, it will list `notes.txt` as an "untracked file," meaning Git sees it but is not yet saving its history.

```bash
git add notes.txt
```

This moves `notes.txt` into the staging area, marking it as ready to be included in the next commit.

```bash
git status
```

Running this again now shows `notes.txt` listed under "changes to be committed," confirming it is staged.

```bash
git commit -m "Initial commit: add notes.txt"
```

This saves a permanent snapshot of the staged file into the local repository. The text after `-m` is the commit message, a short description of what changed and why.

```bash
git log --oneline
```

This displays the history of commits in a compact, one-line-per-commit format, letting you confirm your commit was saved.

---

## 6. Connecting to GitHub

This step links your local repository to an online repository on GitHub so it can be backed up and shared.

1. Log in to [GitHub.com](https://github.com).
2. Create a new repository. Leave the options to add a README, `.gitignore`, or license unchecked, since your project already has its own files and an existing history; adding these on GitHub could create conflicting files.
3. After creating the repository, GitHub will show a URL similar to:
   `https://github.com/suraj-sp-nie/CDD-LAB-01.git`
   Copy this URL.

In Git Bash, run:

```bash
git remote add origin https://github.com/4IK25CS217/CDD-LAB-01.git
```

This tells your local repository where its online counterpart lives, giving it the nickname `origin`, which is the standard name used for the main remote.

```bash
git remote -v
```

This lists the remote connections currently configured, letting you confirm the URL was added correctly.

---

## 7. Pushing to GitHub

This step uploads your local commits to GitHub.

```bash
git push -u origin main
```

- `push` sends your commits to the remote repository.
- `origin main` specifies that you are pushing to the `main` branch of the `origin` remote.
- The `-u` flag sets this as the default connection, so future pushes can simply use `git push` without repeating the full command.

The first time you push, a Git Credential Manager window will appear. Choose "Sign in with your browser," then approve the request in the browser tab that opens. After this, your login is saved, so future pushes will not require signing in again.

Once the push finishes, refresh your repository page on GitHub to confirm that your files now appear there.

---

## 8. Command Reference

| Operation | Command | Description |
|---|---|---|
| Create directory | `mkdir folder_name` | Creates a new directory |
| Change directory | `cd folder_name` | Navigates into a directory |
| Create file | `echo "text" > file.txt` | Creates or overwrites a file |
| Append to file | `echo "text" >> file.txt` | Adds a line to an existing file |
| Initialize repository | `git init` | Creates a local Git repository |
| Check status | `git status` | Shows working directory and staging status |
| Stage file | `git add file.txt` | Adds a file to the staging area |
| Commit changes | `git commit -m "message"` | Saves staged changes to history |
| Add remote | `git remote add origin <URL>` | Links local repository to GitHub |
| Push changes | `git push -u origin main` | Uploads commits to GitHub |
