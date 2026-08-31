# Install and configure git locally on your machine and perform basic git operations.

## 1. Overview

Git manages code through four stages:

```
Working Directory --> Staging Area --> Local Repository --> GitHub Remote
   (git add)           (git commit)                          (git push)
```

- **Working Directory:** The local folder where files are created and edited.
- **Staging Area:** Holds changes selected for the next commit.
- **Local Repository:** Git's local database of saved commits (the `.git` folder).
- **GitHub Remote:** The online copy of the repository.

---

## 2. Installing Git on Windows

1. Go to [git-scm.com](https://git-scm.com/) and download the 64-bit Git for Windows installer.
2. Run the installer and use the following settings:
   - Destination: default
   - Components: enable Git Bash Here and Git GUI Here
   - Default editor: Vim or Visual Studio Code
   - Default branch name: `main`
   - PATH option: Git from the command line and also from third-party software
   - SSH: use bundled OpenSSH
   - Line endings: checkout Windows-style, commit Unix-style (`core.autocrlf = true`)
   - Terminal: MinTTY
   - Credential helper: Git Credential Manager
3. Click Install, then Finish.

### Verify installation

```bash
git --version
```

---

## 3. Initial Configuration

```bash
git config --global user.name "sueaj-sp-nie"
git config --global user.email "2025cs_suraj_sp_g@nie.ac.in"
```

Check settings:

```bash
git config --list
```

---

## 4. Creating a Project Folder and File

```bash
cd ~
mkdir project-folder
cd project-folder

echo "Header: My First Git Log" > notes.txt
echo "Created on: 2026-08-18" >> notes.txt
echo "Environment: Windows Git Bash" >> notes.txt

ls -la
```

---

## 5. Local Git Workflow

```bash
git init
git status
git add notes.txt
git status
git commit -m "Initial commit: add notes.txt"
git log --oneline
```

---

## 6. Connecting to GitHub

1. Log in to [GitHub.com](https://github.com).
2. Create a new repository (do not initialize with README, .gitignore, or license).
3. Copy the repository URL, for example:
   `https://github.com/suraj-sp-nie/CDD-LAB-01.git`

In Git Bash:

```bash
git remote add origin https://github.com/suraj-sp-nie/CDD-LAB-01.git
git remote -v
```

---

## 7. Pushing to GitHub

```bash
git push -u origin main
```

On first push, a Git Credential Manager window will appear. Choose "Sign in with your browser" and authorize access. Credentials are then saved for future pushes.

Refresh the GitHub repository page to confirm the files were uploaded.

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
