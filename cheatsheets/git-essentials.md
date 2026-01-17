# Git Essentials

The commands you actually need.

## TL;DR

```bash
git add .                    # Stage all changes
git commit -m "message"      # Commit with message
git push                     # Push to remote
git pull                     # Get latest changes
```

---

## Setup

```bash
# Configure identity
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

# Initialize new repo
git init

# Clone existing repo
git clone https://github.com/user/repo.git
```

---

## Daily Workflow

```bash
# Check status
git status

# Stage changes
git add .                    # All files
git add file.txt             # Specific file
git add src/                 # Specific folder

# Commit
git commit -m "Add feature"

# Push to remote
git push
git push origin main         # Explicit branch

# Pull latest
git pull
```

---

## Branches

```bash
# List branches
git branch                   # Local
git branch -a                # All (including remote)

# Create branch
git checkout -b feature-name

# Switch branch
git checkout main
git switch main              # Newer syntax

# Delete branch
git branch -d feature-name   # Safe delete
git branch -D feature-name   # Force delete

# Push new branch
git push -u origin feature-name
```

---

## Merging

```bash
# Merge branch into current
git merge feature-name

# Abort merge (if conflicts)
git merge --abort

# After resolving conflicts
git add .
git commit -m "Resolve merge conflicts"
```

---

## Undoing Things

```bash
# Unstage file
git reset HEAD file.txt

# Discard changes in file
git checkout -- file.txt
git restore file.txt         # Newer syntax

# Undo last commit (keep changes)
git reset --soft HEAD~1

# Undo last commit (discard changes)
git reset --hard HEAD~1

# Revert a commit (creates new commit)
git revert <commit-hash>
```

---

## Viewing History

```bash
# View log
git log
git log --oneline            # Compact
git log --oneline -10        # Last 10

# View changes
git diff                     # Unstaged changes
git diff --staged            # Staged changes
git diff HEAD~1              # Since last commit

# Show specific commit
git show <commit-hash>
```

---

## Stashing

```bash
# Save changes temporarily
git stash

# List stashes
git stash list

# Apply latest stash
git stash pop

# Apply specific stash
git stash apply stash@{0}

# Drop stash
git stash drop
```

---

## Remote

```bash
# View remotes
git remote -v

# Add remote
git remote add origin https://github.com/user/repo.git

# Change remote URL
git remote set-url origin https://github.com/user/new-repo.git

# Fetch without merge
git fetch origin
```

---

## .gitignore

```bash
# Common patterns
node_modules/
.env
.env.local
*.log
.DS_Store
dist/
build/
.next/
__pycache__/
*.pyc
venv/
```

---

## Quick Fixes

```bash
# Amend last commit message
git commit --amend -m "New message"

# Add to last commit (no new commit)
git add forgotten-file.txt
git commit --amend --no-edit

# Remove file from git (keep locally)
git rm --cached file.txt

# Clean untracked files
git clean -fd
```

---

## Aliases (Optional)

Add to `~/.gitconfig`:

```ini
[alias]
    s = status
    co = checkout
    br = branch
    ci = commit
    lg = log --oneline -10
    undo = reset --soft HEAD~1
```

Then use: `git s`, `git co main`, etc.

---

## Common Workflows

### Feature Branch

```bash
git checkout main
git pull
git checkout -b feature/new-thing
# ... make changes ...
git add .
git commit -m "Add new thing"
git push -u origin feature/new-thing
# Create PR on GitHub
```

### Quick Fix

```bash
git checkout main
git pull
# ... make fix ...
git add .
git commit -m "Fix bug"
git push
```

### Sync Fork

```bash
git remote add upstream https://github.com/original/repo.git
git fetch upstream
git checkout main
git merge upstream/main
git push
```

---

*Commit early. Commit often.*
