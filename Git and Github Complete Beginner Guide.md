
# Git & GitHub - Complete Beginner Guide

> These are my personal notes from learning Git & GitHub hands-on while pushing my Windows Server 2022 home lab to GitHub. Every lesson here came from real troubleshooting.

---

## What is Git?

Git is a **version control system**. Think of it like a save system for your files — but way smarter than just hitting Ctrl+S.

- It tracks **every change** you make to your files over time
- You can **go back** to any previous version
- Multiple people can **work on the same project** without overwriting each other's work
- It works **locally on your computer** — you don't need internet to use Git

**Analogy:** Imagine writing a research paper and saving a new copy every time you make changes — `paper_v1.docx`, `paper_v2_final.docx`, `paper_v2_FINAL_final.docx`. Git does this automatically and way more organized.

---

## What is GitHub?

GitHub is a **website that hosts Git repositories online**. Think of it as the cloud storage for your Git projects.

- Git = the tool that runs on your computer
- GitHub = the website where your code lives online so others can see it
- They are **not the same thing** — Git works without GitHub, but GitHub needs Git

**Analogy:** Git is like your local filing cabinet. GitHub is like Google Drive for your filing cabinet — it puts your files in the cloud so others can access them and you have a backup.

---

## Key Vocabulary

|Term|What It Means|Real-World Analogy|
|---|---|---|
|**Repository (Repo)**|A project folder that Git is tracking|A filing cabinet for one project|
|**Commit**|A snapshot/save point of your files at a moment in time|Hitting "save" on a video game|
|**Branch**|A separate version of your project you can work on without affecting the main one|Making a copy of a document to try edits before committing to them|
|**Main/Master**|The default primary branch — the "official" version|The final draft of your paper|
|**Remote**|The version of your repo that lives online (like on GitHub)|The Google Drive copy|
|**Local**|The version of your repo on your computer|The copy on your hard drive|
|**Clone**|Downloading a full copy of a GitHub repo to your computer|Downloading a folder from Google Drive|
|**Push**|Sending your local commits up to GitHub|Uploading your updated files to Google Drive|
|**Pull**|Downloading updates from GitHub to your local repo|Syncing new files from Google Drive to your computer|
|**Stage (git add)**|Marking files to be included in your next commit|Putting papers in a pile that you're about to file|
|**Merge**|Combining two branches together|Taking edits from your draft copy and putting them into the final copy|
|**Fork**|Making your own copy of someone else's repo on GitHub|Photocopying someone's binder so you can make your own edits|
|**Pull Request (PR)**|Asking the repo owner to review and merge your changes|Submitting your edits to your boss for approval|
|**.gitignore**|A file that tells Git which files to NOT track|A "do not file" list|
|**HEAD**|A pointer to your current position in the commit history|A bookmark showing where you are in a book|
|**Untracked**|Files that Git sees but isn't tracking yet|Papers on your desk that haven't been filed yet|
|**Origin**|The default name for your remote repository (GitHub)|The nickname for your cloud backup|

---

## How Git Actually Works — The Flow

```
Your Files → Stage (git add) → Commit (git commit) → Push (git push) → GitHub
```

Think of it like mailing a package:

1. **Working Directory** = Your desk where you're working on files
2. **Staging Area (git add)** = Putting items in a box, deciding what to ship
3. **Commit (git commit)** = Sealing the box and labeling it with a description
4. **Push (git push)** = Dropping the box off at the post office (sending to GitHub)

You don't have to send everything at once. You **choose** what goes in each box.

---

## Setting Up Git for the First Time

Before Git lets you do anything, it needs to know who you are. This only needs to be done once per computer.

powershell

```powershell
# Set your name (shows up on your commits)
git config --global user.name "YourName"

# Set your email (should match your GitHub email)
git config --global user.email "your.email@example.com"

# Verify your settings
git config --global --list
```

> ⚠️ **Lesson Learned:** If you skip this step, Git will throw an "Author identity unknown" error when you try to commit. It won't let you save anything until it knows who's saving it.

---

## Two Ways to Start a Project

### Option A: Start on GitHub First (Recommended for Beginners)

This is the cleanest way — avoids the "unrelated histories" problem.

powershell

```powershell
# 1. Create a repo on GitHub (with or without README)
# 2. Clone it to your computer
git clone https://github.com/YourUsername/YourRepo.git

# 3. Move into the folder
cd YourRepo

# 4. Add your files to the folder, then:
git add .
git commit -m "Add my project files"
git push
```

### Option B: Start on Your Computer First

powershell

```powershell
# 1. Navigate to your project folder
cd "C:\Your\Project\Folder"

# 2. Initialize Git in that folder
git init

# 3. Connect it to a GitHub repo
git remote add origin https://github.com/YourUsername/YourRepo.git

# 4. Stage, commit, and push
git add .
git commit -m "Initial commit"
git branch -M main
git push -u origin main
```

> ⚠️ **WARNING:** If you created the GitHub repo WITH a README and you use Option B, you will get a push rejection error. See the Troubleshooting section below for the fix.

---

## The Essential Commands

### Day-to-Day Workflow

powershell

```powershell
# Check what's changed
git status

# Stage all changes
git add .

# Stage a specific file
git add filename.ps1

# Commit with a message
git commit -m "Describe what you changed"

# Push to GitHub
git push
```

### Checking Things

powershell

```powershell
# See all your commits
git log --oneline

# See what branch you're on
git branch

# See your remote connection
git remote -v

# See what's changed but not staged
git diff
```

### Branching

powershell

```powershell
# Create a new branch and switch to it
git checkout -b new-feature

# Switch between branches
git checkout main
git checkout new-feature

# Merge a branch into main
git checkout main
git merge new-feature

# Delete a branch after merging
git branch -d new-feature
```

---

## Opening PowerShell in a Specific Folder

You need PowerShell open in your project folder to run Git commands. Two easy ways:

1. **Address bar method:** In File Explorer, click the address bar, type `powershell`, hit Enter
2. **Shift + Right-click:** In the empty space of the folder, hold Shift and right-click → "Open PowerShell window here"

---

## Authentication — How GitHub Knows It's You

GitHub no longer accepts plain passwords when pushing from the command line. You have two options:

### Option 1: Browser Authentication

When you push for the first time, Git may open your browser and ask you to log into GitHub. Once you authorize it, you're good.

### Option 2: Personal Access Token (PAT)

1. Go to GitHub → Settings → Developer Settings → Personal Access Tokens → Generate New Token
2. Give it a name, set permissions (at minimum: `repo`)
3. Copy the token — you'll only see it once
4. When Git asks for your password, paste the token instead

### Option 3: GitHub CLI

powershell

```powershell
# Install GitHub CLI, then:
gh auth login
# Follow the prompts to authenticate
```

---

## .gitignore — Telling Git What to Ignore

Some files shouldn't go to GitHub (passwords, large files, system files). Create a `.gitignore` file in your project root:

```
# Ignore Windows system files
Thumbs.db
desktop.ini

# Ignore environment/config files with secrets
.env
*.key
*.pem

# Ignore large folders
node_modules/
.vscode/
```

---

## Writing Good Commit Messages

Your commit messages are like labels on your save files. Future you (and anyone reading your repo) will thank you for writing clear ones.

**Good Examples:**

- `Add AD user creation PowerShell script`
- `Fix DHCP scope configuration screenshot`
- `Update forest setup documentation`
- `Remove unused test files`

**Bad Examples:**

- `stuff`
- `update`
- `fixed things`
- `asdfgh`

**Format tip:** Start with a verb — Add, Fix, Update, Remove, Create, Refactor

---

## Troubleshooting — Common Errors & Fixes

### Error: "Author identity unknown"

```
fatal: unable to auto-detect email address
```

**What happened:** Git doesn't know who you are yet.

**Fix:**

powershell

```powershell
git config --global user.name "YourName"
git config --global user.email "your.email@example.com"
```

---

### Error: "Updates were rejected — fetch first"

```
! [rejected] main -> main (fetch first)
```

**What happened:** The GitHub repo has commits (like a README) that your local repo doesn't have. Git won't let you overwrite them.

**Why it happens:** You created the repo on GitHub WITH a README (giving it its own history), then created a separate repo on your computer (with its own history). Git sees two strangers trying to share a house.

**Fix:**

powershell

```powershell
git pull origin main --allow-unrelated-histories
# Then push again
git push -u origin main
```

**Prevention:** Either create the GitHub repo WITHOUT a README, or clone the repo first before adding files.

---

### Error: "src refspec main does not match any"

```
error: src refspec main does not match any
```

**What happened:** You're trying to push to a branch called `main` but your local branch has a different name (probably `master`).

**Fix:**

powershell

```powershell
# Rename your branch to main
git branch -M main
# Then push
git push -u origin main
```

---

### Warning: "Adding embedded git repository"

```
hint: You've added another git repository inside your current repository.
```

**What happened:** There's a `.git` folder inside one of your subfolders — meaning there's a repo inside your repo. Git doesn't know how to handle this.

**Common cause:** You cloned a repo into your project folder by accident.

**Fix:**

powershell

```powershell
# Remove the nested repo from Git's tracking
git rm --cached -f FolderName

# Delete the nested folder entirely
Remove-Item -Recurse -Force FolderName
```

---

### Error: "non-fast-forward"

```
! [rejected] main -> main (non-fast-forward)
```

**What happened:** Your local branch is behind the remote. Someone (or you on another machine) pushed changes that you don't have locally.

**Fix:**

powershell

```powershell
git pull origin main --allow-unrelated-histories
git push -u origin main
```

---

## Quick Reference Cheat Sheet

```
git init                              → Start tracking a folder
git clone <url>                       → Download a repo from GitHub
git status                            → See what's changed
git add .                             → Stage all files
git commit -m "message"               → Save a snapshot
git push                              → Send to GitHub
git pull                              → Download from GitHub
git branch                            → See your branches
git branch -M main                    → Rename branch to main
git checkout -b <name>                → Create & switch to new branch
git merge <branch>                    → Merge a branch into current
git log --oneline                     → See commit history
git remote -v                         → See remote connections
git remote add origin <url>           → Connect to GitHub repo
git config --global user.name "name"  → Set your Git identity
git config --global user.email "email"→ Set your Git email
```

---

## My Real-World Experience

When pushing my Windows Server 2022 home lab to GitHub, I hit three walls:

1. **Identity Error** — Git wouldn't commit because I hadn't configured my name and email. Quick config fix.
2. **Embedded Repo** — I had accidentally cloned my ADScripts repo inside the same folder, creating a repo inside a repo. Had to force remove it.
3. **Rejected Push** — GitHub had a README with its own history, my computer had a separate history. Used `--allow-unrelated-histories` to merge them together.

**Lesson:** Next time, either skip the README when creating the repo OR clone it first before adding files. Problem avoided entirely.

---

## Tags

#Git #GitHub #VersionControl #HomeLab #CyberSecurity #DevOps #PowerShell #CheatSheet