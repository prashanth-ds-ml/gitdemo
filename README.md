# 🧠 Git & GitHub Practice: Multi-Account Setup & Workflow

This repository is used to practice essential Git and GitHub commands, understand version control workflows, and manage multiple GitHub accounts from the same machine using SSH.

---

## 🔄 What is Git?

**Git** is a distributed version control system that helps developers:

- Track changes in source code over time
- Collaborate effectively with other developers
- Revert to previous versions when needed

---

## 🌐 What is GitHub?

**GitHub** is a web-based platform built on Git that allows developers to:

- Host and manage Git repositories online
- Collaborate with teams
- Track issues, pull requests, and branches

---

## 🧪 Git File Lifecycle

| State       | Meaning                                    |
|-------------|--------------------------------------------|
| Untracked   | File not yet tracked by Git                |
| Modified    | File has been changed but not staged       |
| Staged      | File is ready to be committed              |
| Committed   | File changes are saved to local repo       |
| Pushed      | Changes uploaded to remote repo (GitHub)   |

---

## 🧰 Common Git Commands

```bash
# Global Git configuration (runs once per machine)
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --list               # See all git config values

# Repo-related operations
git clone <repo_url>           # Clone a repo
git init                       # Initialize a new local repo
git status                     # View file state changes
git add <file>                 # Stage file changes
git commit -m "message"        # Commit staged changes
git push origin main           # Push to remote repo

# Branching
git branch                     # List all branches
git checkout <branch>          # Switch branches
git checkout -b <new-branch>   # Create and switch to a new branch
git branch -d <branch>         # Delete a branch
git merge <branch>             # Merge branch into current branch

# Misc
git diff <branch/file>         # View changes between branches/files
ls -a                          # Show hidden files like .git/
````

---

## 🔐 Managing Multiple GitHub Accounts via SSH

If you have **two or more GitHub accounts** (e.g., `work` and `personal`), here's how to configure SSH for each account.

### 🎯 Goal

Be able to push to different GitHub accounts without login conflicts or credential errors.

---

### 📁 1. Generate Separate SSH Keys

```bash
# For personal account (e.g., prashanth-ds-ml)
ssh-keygen -t rsa -b 4096 -C "prashanth01071995@gmail.com" -f ~/.ssh/id_rsa_prashanth

# (Optional) For work account
ssh-keygen -t rsa -b 4096 -C "work.email@example.com" -f ~/.ssh/id_rsa_work
```

---

### 🔗 2. Add SSH Keys to GitHub

Copy each key:

```bash
cat ~/.ssh/id_rsa_prashanth.pub
cat ~/.ssh/id_rsa_work.pub  # if applicable
```

Add them to: [GitHub SSH Settings](https://github.com/settings/keys)

---

### ⚙️ 3. Configure SSH Aliases

Edit (or create) your SSH config file:

```bash
nano ~/.ssh/config
```

Paste this:

```ini
# Personal GitHub Account
Host github-prashanth
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_prashanth

# Work GitHub Account (optional)
Host github-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_work
```

Save and exit.

---

### 🚀 4. Use SSH Alias in Remote URL

Update the Git remote to use the right identity (e.g., for `prashanth-ds-ml`):

```bash
git remote set-url origin git@github-prashanth:prashanth-ds-ml/your-repo-name.git
```

> Example:

```bash
git remote set-url origin git@github-prashanth:prashanth-ds-ml/Time_Tracker.git
```

You can now push:

```bash
git push origin main
```

---

### 🔐 Optional: SSH Passphrase

When creating the SSH key, you can set a passphrase for security. You'll be prompted for it when pushing/pulling, unless you use an SSH agent to cache it.

To cache your key:

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa_prashanth
```

---

## 💡 Tips for VS Code Users

* VS Code automatically uses the Git configuration and SSH keys of your terminal.
* You can commit/push directly from VS Code after setting up SSH keys properly.
* Make sure you open the correct folder (`your-repo`) in VS Code before using Git features.

---

## 📌 Summary

With this setup:

* You can manage multiple GitHub accounts securely.
* You avoid the "403: permission denied" errors.
* You streamline your workflow across personal and work projects.

---

**Author**: [Katakam Prashanth](https://github.com/prashanth-ds-ml)

```

---

Let me know if you'd like to add:
- GitHub Desktop usage
- Pull request workflow
- GitHub Actions intro

I can also help you publish this to GitHub Pages or customize it with badges and visuals.
```
