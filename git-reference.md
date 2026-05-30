# Git Reference Guide

A complete reference for Git commands and `.gitignore` configuration.

---

## Table of Contents

1. [Setup](#1-setup)
2. [Initialize](#2-initialize)
3. [Stage & Snapshot](#3-stage--snapshot)
4. [Branch & Merge](#4-branch--merge)
5. [Remote](#5-remote)
6. [Inspect & Compare](#6-inspect--compare)
7. [Undo](#7-undo)
8. [Advanced](#8-advanced)
9. [.gitignore](#9-gitignore)

---

## 1. Setup

```bash
git config --global user.name "Name"         # Set your global username
git config --global user.email "email"       # Set your global email
git config --global core.editor vim          # Set default text editor
git config --global color.ui auto            # Enable color in output
git config --list                            # List all config settings
git config --global alias.st status          # Create a command alias
git config --global core.autocrlf input      # Normalize line endings
```

---

## 2. Initialize

```bash
git init                                     # Initialize a new local repository
git init <directory>                         # Create repo in a specific folder
git clone <url>                              # Clone a remote repository
git clone <url> <directory>                  # Clone into a named folder
git clone --depth 1 <url>                    # Shallow clone (latest commit only)
git clone --branch <branch> <url>            # Clone a specific branch
```

---

## 3. Stage & Snapshot

```bash
git status                                   # Show working tree status
git add <file>                               # Stage a specific file
git add .                                    # Stage all changes in current directory
git add -p                                   # Interactively stage chunks (patch mode)
git add -A                                   # Stage all changes including deletions

git commit -m "message"                      # Commit with a message
git commit -am "message"                     # Stage tracked files and commit
git commit --amend                           # Modify the last commit
git commit --amend --no-edit                 # Amend without changing message

git reset HEAD <file>                        # Unstage a file
git rm <file>                                # Remove file from repo and disk
git rm --cached <file>                       # Untrack file but keep on disk
git mv <old> <new>                           # Move or rename a tracked file

git stash                                    # Stash current changes
git stash pop                                # Apply and drop the latest stash
git stash apply                              # Apply stash without dropping it
git stash list                               # List all stashes
git stash drop stash@{n}                     # Delete a specific stash
git stash clear                              # Delete all stashes
git stash branch <branch>                    # Create branch from stash
```

---

## 4. Branch & Merge

```bash
git branch                                   # List local branches
git branch -a                                # List all branches (local + remote)
git branch <name>                            # Create a new branch
git branch -d <name>                         # Delete a branch (safe)
git branch -D <name>                         # Force-delete a branch
git branch -m <old> <new>                    # Rename a branch
git branch -r                                # List remote-tracking branches

git checkout <branch>                        # Switch to a branch
git checkout -b <branch>                     # Create and switch to new branch
git checkout -b <branch> <remote>/<branch>   # Track a remote branch
git switch <branch>                          # Switch branch (modern syntax)
git switch -c <branch>                       # Create and switch branch (modern)

git merge <branch>                           # Merge branch into current
git merge --no-ff <branch>                   # Merge with a merge commit always
git merge --squash <branch>                  # Squash branch into one commit
git merge --abort                            # Abort an in-progress merge

git rebase <branch>                          # Rebase current onto branch
git rebase -i HEAD~n                         # Interactive rebase last n commits
git rebase --onto <new> <old> <branch>       # Rebase a range onto a new base
git rebase --abort                           # Abort an in-progress rebase
git rebase --continue                        # Continue after resolving conflicts

git cherry-pick <commit>                     # Apply a commit to current branch
git cherry-pick <A>..<B>                     # Cherry-pick a range of commits
git cherry-pick --no-commit <commit>         # Cherry-pick without committing
```

---

## 5. Remote

```bash
git remote                                   # List remotes
git remote -v                                # List remotes with URLs
git remote add <name> <url>                  # Add a remote
git remote remove <name>                     # Remove a remote
git remote rename <old> <new>                # Rename a remote
git remote set-url <name> <url>              # Change a remote's URL

git fetch                                    # Download changes without merging
git fetch <remote>                           # Fetch from a specific remote
git fetch --all                              # Fetch from all remotes
git fetch --prune                            # Remove deleted remote branches

git pull                                     # Fetch and merge from remote
git pull --rebase                            # Fetch and rebase instead of merge

git push                                     # Push current branch to remote
git push <remote> <branch>                   # Push specific branch to remote
git push -u origin <branch>                  # Push and set upstream tracking
git push --force-with-lease                  # Safe force push
git push --tags                              # Push all local tags
git push origin --delete <branch>            # Delete a remote branch
```

---

## 6. Inspect & Compare

```bash
git log                                      # Show commit history
git log --oneline                            # Compact one-line log
git log --oneline --graph --all              # Visual branch graph
git log -n 5                                 # Show last 5 commits
git log --author="name"                      # Filter commits by author
git log --since="2 weeks ago"               # Filter by date range
git log --grep="keyword"                     # Search commit messages
git log -S "string"                          # Find commits that added/removed text
git log <file>                               # Show history for a file
git log --follow <file>                      # Track file history across renames
git log --stat                               # Show file change stats per commit

git diff                                     # Show unstaged changes
git diff --staged                            # Show staged changes
git diff <branch1>..<branch2>               # Compare two branches
git diff <commit1> <commit2>                 # Compare two commits

git show <commit>                            # Show details of a commit
git show HEAD                                # Show the latest commit
git blame <file>                             # Show who changed each line
git shortlog -sn                             # Commits per author, sorted

git tag                                      # List all tags
git tag <name>                               # Create a lightweight tag
git tag -a <name> -m "msg"                  # Create an annotated tag
git describe --tags                          # Describe using nearest tag

git reflog                                   # Show history of HEAD movements
```

---

## 7. Undo

> **Safe** operations create new commits and don't rewrite history. **Destructive** operations rewrite history — avoid on shared branches.

| Command | Safe? | Effect |
|---|---|---|
| `git revert <commit>` | ✅ Safe | Creates a new undo commit |
| `git reset --soft HEAD~1` | ⚠️ Local only | Undo commit, keep staged |
| `git reset --mixed HEAD~1` | ⚠️ Local only | Undo commit, keep unstaged |
| `git reset --hard HEAD~1` | ❌ Destructive | Undo commit, discard changes |
| `git restore <file>` | ✅ Safe | Discard unstaged changes |
| `git clean -fd` | ❌ Destructive | Remove untracked files permanently |

```bash
git revert <commit>                          # Create undo commit (safe)
git revert HEAD                              # Revert the last commit
git revert <A>..<B>                          # Revert a range of commits

git reset --soft HEAD~1                      # Undo commit, keep staged
git reset --mixed HEAD~1                     # Undo commit, keep unstaged
git reset --hard HEAD~1                      # Undo commit, discard changes
git reset --hard <commit>                    # Reset to a specific commit
git reset HEAD <file>                        # Unstage a file

git restore <file>                           # Discard unstaged changes in file
git restore --staged <file>                  # Unstage a file (modern syntax)

git clean -fd                                # Remove untracked files and dirs
git clean -n                                 # Dry run: show what would be cleaned
```

---

## 8. Advanced

```bash
# Binary search for bugs
git bisect start
git bisect good <commit>                     # Mark a commit as good
git bisect bad <commit>                      # Mark a commit as bad
git bisect reset                             # End bisect session

# Submodules
git submodule add <url>                      # Add a submodule
git submodule update --init                  # Initialize and update submodules
git submodule foreach git pull               # Pull in all submodules

# Worktrees
git worktree add <path> <branch>             # Check out a branch in new folder
git worktree list                            # List all worktrees

# Maintenance
git archive --format=zip HEAD > out.zip      # Export repo snapshot as zip
git gc                                       # Clean up and optimize the repo
git fsck                                     # Check repo integrity

# Patches
git format-patch <branch>                    # Create patch files from commits
git apply <patch>                            # Apply a patch file
git bundle create <file> --all               # Bundle repo for offline transfer

# History rewriting
git notes add -m "note" <commit>             # Attach a note to a commit
git filter-branch --tree-filter "rm file" HEAD  # Rewrite history removing a file
```

---

## 9. .gitignore

### What is `.gitignore`?

A `.gitignore` file tells Git which files and directories to ignore — they will never be staged or committed. It lives at the root of your repository (or in any subdirectory for local rules).

### Syntax

```gitignore
# This is a comment

# Ignore a specific file
secret.env

# Ignore all files with an extension
*.log
*.tmp
*.DS_Store

# Ignore a specific directory
node_modules/
dist/
build/
.cache/

# Ignore everything inside a directory but keep the directory
logs/*
!logs/.gitkeep

# Ignore files in any subdirectory
**/debug.log
**/*.min.js

# Ignore only in the root (leading slash)
/config.local.js

# Negate a pattern — do NOT ignore this file even if a rule above matches it
!important.log

# Ignore files matching a pattern in any subfolder
docs/**/*.pdf
```

### Pattern rules

| Pattern | Meaning |
|---|---|
| `*` | Matches any string except `/` |
| `**` | Matches any path including `/` |
| `?` | Matches any single character |
| `[abc]` | Matches one of the characters in brackets |
| `!pattern` | Negates a pattern (un-ignores a file) |
| `trailing/` | Matches directories only |
| `leading/` | Anchors pattern to repo root |

### Common `.gitignore` templates

#### Node.js

```gitignore
node_modules/
npm-debug.log*
yarn-debug.log*
yarn-error.log*
.npm
.env
.env.local
.env.*.local
dist/
build/
.cache/
coverage/
*.tsbuildinfo
```

#### Python

```gitignore
__pycache__/
*.py[cod]
*.pyo
*.pyd
.Python
env/
venv/
.venv/
*.egg-info/
dist/
build/
.pytest_cache/
.coverage
*.log
```

#### Next.js / React

```gitignore
.next/
out/
build/
node_modules/
.env
.env.local
.env.development.local
.env.test.local
.env.production.local
*.log
.DS_Store
coverage/
```

#### General

```gitignore
# OS files
.DS_Store
Thumbs.db
desktop.ini

# Editor files
.vscode/
.idea/
*.swp
*.swo
*~

# Logs
*.log
logs/

# Environment
.env
.env.*
!.env.example

# Dependencies
node_modules/
vendor/
```

### Global `.gitignore`

Set up a global ignore file that applies to all your repos:

```bash
git config --global core.excludesfile ~/.gitignore_global
```

Then create `~/.gitignore_global` with rules for OS/editor files you always want to ignore (`.DS_Store`, `.idea/`, etc.).

### Useful commands

```bash
# Check if a file is being ignored and why
git check-ignore -v <file>

# List all ignored files in the repo
git ls-files --ignored --exclude-standard

# Stop tracking a file that is now in .gitignore
git rm --cached <file>
git rm --cached -r <directory>

# Re-apply .gitignore rules after editing it
git rm --cached -r .
git add .
```

### `.gitignore` vs other ignore files

| File | Scope | Committed? | Use case |
|---|---|---|---|
| `.gitignore` | Repo (shared) | ✅ Yes | Rules everyone on the team should share |
| `.git/info/exclude` | Repo (local) | ❌ No | Personal rules for this repo only |
| `~/.gitignore_global` | System-wide | ❌ No | Rules for all repos on your machine |

---

*Reference guide — Git 2.x and above.*
