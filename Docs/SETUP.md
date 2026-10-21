# Team Git & GitHub Guide

A quick-start guide for working together in this repository. Read it once, then keep the [cheat sheet](#cheat-sheet) handy.

---

## Table of Contents

1. [One-Time Setup](#1-one-time-setup)
2. [Getting the Project](#2-getting-the-project)
3. [Team Workflow (Branch → PR → Merge)](#3-team-workflow)
4. [Commit Message Rules](#4-commit-message-rules)
5. [Staying in Sync](#5-staying-in-sync)
6. [Resolving Merge Conflicts](#6-resolving-merge-conflicts)
7. [STM32CubeIDE Tips](#7-stm32cubeide-tips)
8. [Cheat Sheet](#cheat-sheet)
9. [Troubleshooting](#troubleshooting)

---

## 1. One-Time Setup

### Install Git
- **Windows:** https://git-scm.com/download/win
  - Accept the defaults **except** on the *"Adjusting your PATH environment"* screen. Choose **"Use Git and optional Unix tools from the Command Prompt"**. This is what lets you run `bash` from Command Prompt.
  - Already installed Git without that option? Run the installer again and pick it.
- **macOS:** `brew install git` (or install Xcode Command Line Tools)
- **Linux:** `sudo apt install git`

### Open a terminal (bash)
All commands in this guide are written for **bash**. If you choose a different version it is on you to figure it out ¯\(ツ)/¯

**Windows (recommended setup)**
1. Install Git with the Unix tools option above.
2. Open **Command Prompt** (Start → type `cmd`) or **Windows Terminal**.
3. Type `bash` and press Enter. Your prompt changes to a bash prompt (usually ending in `$`).
4. Type `exit` to go back to Command Prompt.

#### Short tutorial

The `cd` command allows you to enter a new folder. You will see your name or the name of your device. For me its `zacmi@LAPTOP-59GLCC3J`. Then you will
see `MINGW64` followed by the directory (folder) that you are in. From there you can navigate just like file explorer. You can then `cd` into any of the folders that are inside of that folder.

The next command you need to know is `ls` this one is really simple it just lists what files/folders are inside of the directory you are currently in.
In this repo if you are in the main folder and run `ls` you will see `Modular Flight Computer`, `references`, and `README.md`

Quick tips: use `cd ..` to go back a directory (makes it easier to navigate), `code (file)` will open the code editor of your choice to edit a file, 
and finally `mkdir (folder)` this allows you to make a new folder.

**There will be a cheat sheet and troubleshooting guide at the bottom**

To start in the project folder, `cd` into the folder that you want to make the repo in. I would recommend having a seperate folder for this repository to be created in but not required.

**macOS**
Open **Terminal** (Cmd+Space, type `Terminal`). It runs zsh by default. Type `bash` to switch if you want to match everyone else. The Git commands behave identically either way.

**Linux**
Open your terminal (usually Ctrl+Alt+T). It's already bash.

**Verify your setup.** With bash open, run:
```bash
git --version
echo $SHELL
```
`git --version` should print a version number. `echo $SHELL` shows which shell you're in; on Windows it may show a Git path, which is fine.

### Tell Git who you are
Use the **same email as your GitHub account** so commits are linked to you.
```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
git config --global pull.rebase false
```

### Authenticate with GitHub
GitHub no longer accepts account passwords for Git operations. Pick one:

**Option A: HTTPS + Personal Access Token (easiest)**
1. GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic) → Generate new token
2. Give it the `repo` scope
3. When Git asks for a password, paste the token (Git Credential Manager will remember it)

**Option B: SSH key**
```bash
ssh-keygen -t ed25519 -C "you@example.com"
# press Enter through the prompts, then:
cat ~/.ssh/id_ed25519.pub
```
Copy the output into GitHub → Settings → SSH and GPG keys → New SSH key.
Test with `ssh -T git@github.com`.

---

## 2. Getting the Project

Clone the repository **once**:
```bash
git clone https://github.com/MSOE-High-Power-Rocket-Club-Avionics/Custom-Flight-Computer.git
cd Custom-Flight-Computer
```

You'll now have a local copy connected to GitHub (the remote is called `origin`).

---

## 3. Team Workflow

**The golden rule: never commit directly to `main`.** We want to avoid merge conflicts as much as possible please :)

### Step 1: Start from an up-to-date `main`
```bash
git checkout main
git pull
```

### Step 2: Create a branch for your task
```bash
git checkout -b feature/short-description
```

Branch naming:

| Prefix      | Use for                     | Example                      |
|-------------|-----------------------------|------------------------------|
| `feature/`  | New functionality           | `feature/touchscreen-driver` |
| `fix/`      | Bug fixes                   | `fix/uart-overflow`          |
| `docs/`     | Documentation only          | `docs/update-readme`         |
| `refactor/` | Cleanup, no behavior change | `refactor/adc-module`        |

### Step 3: Do your work, then commit often
```bash
git status                  # see what changed
git add path/to/file.c      # stage specific files (preferred)
git commit -m "Add ADC DMA initialization"
```

> Avoid `git add .` unless you've checked `git status` first, since it's how build files and secrets sneak in.

### Step 4: Push your branch
First push:
```bash
git push -u origin feature/short-description
```
Later pushes:
```bash
git push
```

### Step 5: Open a Pull Request
1. Go to the repo on GitHub. You'll see a **Compare & pull request** banner. Click it.
2. Write a clear title and short description: *what* changed, *why*, and *how to test it*.
3. Request a review from at least one teammate (This could just be me :) )

### Step 6: Review
- Reviewers: leave comments, then **Approve** or **Request changes**.
- Authors: push fixes to the same branch and the PR updates automatically.

### Step 7: Merge and clean up
Once approved and conflict-free, click **Merge pull request**, then:
```bash
git checkout main
git pull
git branch -d feature/short-description
```

---

## 4. Commit Message Rules

Good history saves hours later.

Just make sure that you write a little bit about what it is about

`asdf` `Final.V2` `stuff` aren't really all that helpful

---

## 5. Staying in Sync

While you work on a long-running branch, pull in changes from `main` regularly (at least daily) to avoid giant conflicts later:

```bash
git checkout main
git pull
git checkout feature/your-branch
git merge main
```

Always **pull before you start working** and **before you push**.

---

## 6. Resolving Merge Conflicts

Conflicts happen when two people edit the same lines. They're normal, not scary.

1. Run `git merge main` (or `git pull`). Git reports conflicted files.
2. Open each conflicted file and find the markers:
   ```
   <<<<<<< HEAD
   your version
   =======
   their version
   >>>>>>> main
   ```
3. Edit the file to the final correct version and **delete all marker lines**.
4. Finish:
   ```bash
   git add path/to/resolved_file.c
   git commit
   ```
5. Build and test before pushing.

If you're unsure which version is right, **ask the teammate who wrote the other change**.

To bail out of a merge and start over: `git merge --abort`

---

## 7. STM32CubeIDE Tips

If your project is generated with STM32CubeIDE / STM32CubeMX, a few extra habits will save you pain.

### Recommended `.gitignore`
Create a file named `.gitignore` in the repo root:
```gitignore
# Build output
Debug/
Release/
*.o
*.d
*.elf
*.map
*.bin
*.hex
*.list
*.su
*.cyclo

# IDE / workspace files
.metadata/
.settings/
*.launch
.idea/
.vscode/

# OS junk
.DS_Store
Thumbs.db
```

> Commit your source (`Core/`, `Drivers/`), the `.ioc` file, `.project`, `.cproject`, and linker scripts (`*.ld`). Those are needed to open the project on another machine.

### Code generation rules
- **Only write code between the `USER CODE BEGIN` / `USER CODE END` markers** in generated files. Anything outside gets overwritten when the `.ioc` is regenerated.
- Put your own logic in **separate `.c` / `.h` files** where possible; it also reduces merge conflicts.

### The `.ioc` file
- The `.ioc` (pin/clock configuration) is **hard to merge by hand**. **Only one person should edit it at a time**, and tell the team before you do.
- After changing the `.ioc`, commit the `.ioc` **and** the regenerated files together in one commit.
- After pulling someone else's `.ioc` change, re-open it and regenerate code if prompted.

### Importing the project
In STM32CubeIDE: **File → Import → General → Existing Projects into Workspace**, then select the cloned folder.

---

## Cheat Sheet

| I want to...                         | Command |
|--------------------------------------|---------|
| Download the repo                    | `git clone <url>` |
| See what changed                     | `git status` |
| See line-by-line changes             | `git diff` |
| Create and switch to a new branch    | `git checkout -b <branch>` |
| Switch branches                      | `git checkout <branch>` |
| List branches                        | `git branch` |
| Stage a file                         | `git add <file>` |
| Commit staged changes                | `git commit -m "message"` |
| Push my branch                       | `git push -u origin <branch>` (first time), `git push` after |
| Get latest changes                   | `git pull` |
| Merge `main` into my branch          | `git merge main` |
| See history                          | `git log --oneline --graph` |
| Undo unstaged changes to a file      | `git restore <file>` |
| Unstage a file                       | `git restore --staged <file>` |
| Temporarily shelve changes           | `git stash` / `git stash pop` |
| Delete a merged local branch         | `git branch -d <branch>` |

---

## Troubleshooting

**"I committed to `main` by accident (not pushed yet)."**
```bash
git branch feature/my-work     # save the commit on a new branch
git reset --hard origin/main   # move main back
git checkout feature/my-work
```

**"I need to switch branches but have uncommitted changes."**
```bash
git stash
git checkout other-branch
# ...later...
git stash pop
```

**"Push rejected: updates were rejected because the remote contains work you don't have."**
```bash
git pull
# resolve any conflicts, then
git push
```

**"I edited the wrong files / want to throw away my changes."**
```bash
git restore <file>     # one file
```
⚠️ This permanently discards uncommitted changes.

**"I accidentally committed a build folder or a secret."**
Tell the team. For build folders, add them to `.gitignore` and run `git rm -r --cached <folder>`, then commit. For secrets, rotate the credential immediately.

**"Authentication failed."**
You're likely using your GitHub password. Use a Personal Access Token (or SSH) instead; see [Setup](#authenticate-with-github).

---

## Need Help?

Ask in the team chat before running anything destructive (`reset --hard`, `push --force`, `clean -fd`). Almost every Git mistake is recoverable if you stop and ask.

Further reading: [Pro Git (free book)](https://git-scm.com/book) · [GitHub Docs](https://docs.github.com)