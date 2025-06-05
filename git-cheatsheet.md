---
id: 13
date: 2025-06-05T00:00:00Z
title: Git Cheatsheet
author: Jeremy Novak
summary: Cheatsheet for git and gh commands
slug: git-cheatsheet
tags:
  - git
  - gh
  - GitHub
published: true
---

# Git & GitHub CLI (gh) Cheatsheet

---

## Installation

### Git
- **Linux**
```bash
sudo apt update && sudo apt install git   # Debian/Ubuntu
sudo dnf install git                      # Fedora
sudo yum install git                      # CentOS/RHEL
```
- **macOS**
```bash
brew install git
```
- **Windows**
1. Download the installer from [https://git-scm.com/download/win](https://git-scm.com/download/win)
2. Run the installer and follow the prompts

### GitHub CLI (`gh`)
- **Linux**
```bash
# Debian/Ubuntu
type -p curl >/dev/null || sudo apt install curl -y
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
sudo chmod go+r /usr/share/keyrings/githubcli-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
sudo apt update
sudo apt install gh
```
- **macOS**
```bash
brew install gh
```
- **Windows**
1. Download the installer from [https://github.com/cli/cli/releases/latest](https://github.com/cli/cli/releases/latest)
2. Or use [winget](https://github.com/microsoft/winget-cli):
```powershell
winget install --id GitHub.cli
```

---

## Configuration

- Set your name and email
```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

- Set default branch name
```bash
git config --global init.defaultBranch main
```

- Set up credential caching
```bash
git config --global credential.helper cache
```

- View all config
```bash
git config --list
```

---

## Creating & Cloning Repos

- Initialize a new repo
```bash
git init
```

- Clone a repo
```bash
git clone https://github.com/user/repo.git
```

- Create a new repo on GitHub (gh)
```bash
gh repo create myrepo --public --source=. --remote=origin
```

---

## Basic Workflow

- Check repo status
```bash
git status
```

- Add files to staging
```bash
git add <file>
git add .
```

- Commit changes
```bash
git commit -m "Commit message"
```

- View commit history
```bash
git log --oneline --graph --decorate --all
```

- Push to remote
```bash
git push origin main
```

- Pull from remote
```bash
git pull
```

---

## Branching & Merging

- List branches
```bash
git branch
```

- Create new branch (classic)
```bash
git checkout -b feature/my-feature
```

- Create new branch (modern)
```bash
git switch -c feature/my-feature
```

- Switch branches (classic)
```bash
git checkout main
```

- Switch branches (modern)
```bash
git switch main
```

- Merge branch
```bash
git merge feature/my-feature
```

- Delete branch
```bash
git branch -d feature/my-feature
```

- View branch graph
```bash
git log --oneline --graph --all
```

---

## Stashing & Cleaning

- Stash changes
```bash
git stash
```

- List stashes
```bash
git stash list
```

- Apply latest stash
```bash
git stash apply
```

- Drop latest stash
```bash
git stash drop
```

- Clean untracked files
```bash
git clean -fd
```

---

## Remote Repositories

- Add remote
```bash
git remote add origin https://github.com/user/repo.git
```

- Show remotes
```bash
git remote -v
```

- Change remote URL
```bash
git remote set-url origin https://github.com/user/new-repo.git
```

---

## Tagging & Releases

- Create a tag
```bash
git tag v1.0.0
```

- Push tags
```bash
git push origin --tags
```

- List tags
```bash
git tag
```

- Create a GitHub release (gh)
```bash
gh release create v1.0.0 --title "v1.0.0" --notes "First release"
```

---

## Collaboration & Pull Requests

- Fetch all branches
```bash
git fetch --all
```

- Rebase your branch
```bash
git pull --rebase origin main
```

- Create a pull request (gh)
```bash
gh pr create --base main --head feature/my-feature --title "Add feature" --body "Description"
```

- List pull requests (gh)
```bash
gh pr list
```

- Checkout a pull request (gh)
```bash
gh pr checkout <number>
```

---

## Troubleshooting

- See what changed in working directory
```bash
git status
git diff
```

- Undo last commit (keep changes staged)
```bash
git reset --soft HEAD~1
```

- Undo last commit (discard changes)
```bash
git reset --hard HEAD~1
```

- Restore a deleted file
```bash
git checkout HEAD -- <file>
```

- Fix merge conflicts
```bash
git status
# Edit conflicted files, then:
git add <file>
git commit
```

- Remove file from staging
```bash
git reset <file>
```

- Remove file from repo but keep locally
```bash
git rm --cached <file>
```

- Set upstream for a branch
```bash
git push --set-upstream origin my-branch
```

- See which branch tracks which remote
```bash
git branch -vv
```

- See which files are ignored
```bash
git check-ignore -v *
```

---

## Useful Aliases

- Shorter log
```bash
git config --global alias.lg "log --oneline --graph --decorate --all"
```

- Quick add & commit
```bash
git config --global alias.ac '!git add -A && git commit -m'
```

---

## Resources

- [Pro Git Book](https://git-scm.com/book/en/v2)
- [GitHub CLI Docs](https://cli.github.com/manual/)
- [GitHub Learning Lab](https://lab.github.com/)
- [Oh My Git! (interactive)](https://ohmygit.org/) 