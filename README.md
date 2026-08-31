# Student's Log: Windows Git Setup, Bash File Operations, and GitHub Push 🚀

> **Author:** Student Developer  
> **System:** Windows 10/11 with Git Bash (MinTTY)  
> **Goal:** Complete guide from downloading Git from the web to pushing code to GitHub entirely via terminal.

---

## 📌 1. Conceptual Overview: The Git Lifecycle

Before running commands, it helps to understand how Git manages code across your local Windows machine and GitHub:

```text
 [ Windows Disk ] --------> [ Staging Area ] --------> [ Local Repository ] --------> [ GitHub Cloud ]
(Working Directory)            (git add)                  (git commit)                (git push)
```

1. **Working Directory:** The local folder on your Windows computer where you create and edit files.
2. **Staging Area (Index):** A middle ground where you draft and select changes to include in your next save point.
3. **Local Repository (`.git`):** Git's hidden database on your machine storing permanent snapshots (commits).
4. **GitHub Remote:** The online repository hosting your code in the cloud for backup and sharing.

---

## 📥 2. Step-by-Step Installation of Git on Windows

Since Windows does not ship with Git pre-installed, download and configure it from the official site.

### 2.1 Download the Installer
1. Open your browser and go to **[git-scm.com](https://git-scm.com/)**.
2. Click **Download for Windows**.
3. Choose the **64-bit Git for Windows Setup** standalone executable file.
4. Save the `.exe` file to your `Downloads` directory.

### 2.2 Navigating the Windows Installer Wizard
Run the downloaded setup file as Administrator and configure the setup options step-by-step:

1. **Information & License:** Click **Next**.
2. **Select Destination Location:** Leave as default (`C:\Program Files\Git`) $
ightarrow$ Click **Next**.
3. **Select Components:** 
   * Check **Git Bash Here** (adds right-click terminal access in Explorer).
   * Check **Git GUI Here**.
   * Click **Next**.
4. **Default Editor:** Choose **Vim** (or **Visual Studio Code** if preferred) $
ightarrow$ Click **Next**.
5. **Initial Branch Name:** Select **Override default branch name for new repositories** and set it to `main` $
ightarrow$ Click **Next**.
6. **PATH Environment:** Select **Git from the command line and also from 3rd-party software** $
ightarrow$ Click **Next**.
7. **SSH Executable:** Select **Use bundled OpenSSH** $
ightarrow$ Click **Next**.
8. **Line Ending Conversion:** Select **Checkout Windows-style, commit Unix-style line endings** (`core.autocrlf = true`). *Crucial on Windows to avoid line break errors.*
9. **Terminal Emulator:** Select **Use MinTTY (the default terminal of MSYS2)** $
ightarrow$ Click **Next**.
10. **Credential Helper:** Select **Git Credential Manager** $
ightarrow$ Click **Next**.
11. Click **Install**, and once finished, click **Finish**.

### 2.3 Verify Installation
Launch **Git Bash** (Press `Win Key` $
ightarrow$ type `Git Bash` $
ightarrow$ `Enter`) and run:

```bash
git --version
```
*Expected Output:* `git version 2.55.0.windows.1`

---

## ⚙️ 3. First-Time Configuration

Configure your identity so Git tags your snapshots with your name and email address.

```bash
# Set your author name
git config --global user.name "suraj-sp-nie"

# Set your GitHub-associated email
git config --global user.email "2025cs_surajsp_g@nie.ac.in"

# Set default branch to main
git config --global init.defaultBranch main
```

Verify your settings:
```bash
git config --list
```

---

## 📁 4. Creating Directories, Files, and Appending Content via Bash

Perform all folder and file operations exclusively inside **Git Bash**.

### 4.1 Create and Enter Project Directory
```bash
# Move to home directory
cd ~

# Create project folder
mkdir CDD-LAB-01

# Navigate into directory
cd CDD-LAB-01


### 4.2 Create a File and Append Content in Bash
Instead of opening a graphical text editor, write and append content directly from the command line:

```bash
# 1. Create a new file with initial text using single redirection (>)
echo "Header: My First Git Log" > notes.txt

# 2. Append additional content to the existing file using double redirection (>>)
echo "Created on: 2026-08-31" >> notes.txt
echo "Environment: Windows Git Bash" >> notes.txt


### 4.3 Verify File Content
```bash

# List directory details
ls -la
```

---

## 🔄 5. Local Git Workflow

Track your file changes locally using the core Git cycle.

### 5.1 Initialize Repository
Turn the folder into a Git repository:

```bash
git init
```
*Output:* `Initialized empty Git repository in C:/Users/User/CDD-LAB-01/.git/`

### 5.2 Check Working Tree Status
```bash
git status
```
*Output shows `notes.txt` highlighted in red under "Untracked files".*

### 5.3 Stage the File (`git add`)
Move `notes.txt` to the Staging Area:

```bash
git add notes.txt
```

Verify staging:
```bash
git status
```
*Output shows `new file: notes.txt` highlighted in green under "Changes to be committed".*

### 5.4 Commit Staged Changes (`git commit`)
Save the snapshot to local history:

```bash
git commit -m "Initial commit: Add notes.txt with appended content"
```

### 5.5 Inspect Commit Log
```bash
git log --oneline
```
*Output:* `a1b2c3d (HEAD -> main) Initial commit: Add notes.txt with appended content`

---

## 🌐 6. Linking Local Repository to GitHub

1. Open your browser and log into **[GitHub.com](https://github.com)**.
2. Click **+** (top right) $
ightarrow$ **New repository**.
3. **Repository name:** `CDD-LAB-01`.
4. **Initialize options:** Keep all options (README, `.gitignore`, license) **UNCHECKED**.
5. Click **Create repository**.
6. Copy the repository HTTPS URL (e.g., `https://github.com/suraj-sp-nie/CDD-LAB-01.git`).

In your **Git Bash** terminal, set the remote location:

```bash
git remote add origin https://github.com/suraj-sp-nie/CDD-LAB-01.git
```

Verify remote connection:
```bash
git remote -v
```

---

## 🚀 7. Pushing Code to GitHub

Upload local commits to the remote GitHub cloud repository:

```bash
git push -u origin main
```

### 🔑 Authentication (Git Credential Manager)
When pushing for the first time on Windows:
1. A **Git Credential Manager** pop-up window will appear.
2. Click **Sign in with your browser**.
3. Authorize Git for Windows in your opened web browser.
4. Credentials will be securely cached in Windows Credential Manager for future pushes.

*Successful Terminal Output:*
```text
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 410 bytes | 410.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/your-username/my-git-demo.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
```

Refresh your GitHub repository in your browser to view your `notes.txt` file online.

---

## 📊 8. Command Reference Summary Table

| Operation | Git Bash Command | Description |
| :--- | :--- | :--- |
| **Directory Creation** | `mkdir folder_name` | Creates a new Windows directory |
| **Directory Navigation** | `cd folder_name` | Navigates into directory |
| **File Creation** | `echo "text" > file.txt` | Overwrites or creates file with text |
| **Appending Content** | `echo "text" >> file.txt` | Appends single line to end of file |
| **Git Init** | `git init` | Initializes `.git` local repository |
| **Git Status** | `git status` | Displays state of working folder & staging |
| **Git Add** | `git add file.txt` | Stages file for commit |
| **Git Commit** | `git commit -m "msg"` | Saves staged snapshot into history |
| **Git Remote** | `git remote add origin <URL>` | Links local repo to GitHub |
| **Git Push** | `git push -u origin main` | Pushes local branch to GitHub |
