# Git Branch Operations

## 1. List Branches
```
### Local branches
git branch

# Local + Remote branches
git branch -a

# Local branches with tracking info
git branch -vv
```

## 2. Create & Switch to New Branch
```
git checkout -b <new-branch> [starting-point]
# or modern syntax
git switch -c <new-branch> [starting-point]
```

## 3. Rename Local Branch
```
# Rename current branch
git branch -m <new-branch>

# Rename specific branch
git branch -m <old-branch> <new-branch>
```

## 4. Push Local Branch to Remote
```
git push origin -u <branch-name>
```
*`-u` sets upstream tracking for future `git pull/push`*

## 5. Delete Local Branch
```
# Switch to another branch first
git switch main

# Safe delete (merged branches only)
git branch -d <branch-name>

# Force delete (unmerged branches)
git branch -D <branch-name>
```

## 6. Delete Remote Branch
```
git push origin --delete <branch-name>
# or
git push origin :<branch-name>
```

## 7. Fetch Latest Remote Branches
```
git fetch origin
git branch -r  # List remote branches
```

## 8. Complete Branch Rename Workflow
```
# Rename local
git branch -m old-branch new-branch

# Push new branch
git push origin -u new-branch

# Delete old remote branch
git push origin --delete old-branch
```

## 9. Switch Between Branches
```
git switch <branch-name>
git checkout <branch-name>
```

## 🔒 Safety Notes
- **Always switch away** from a branch before deleting it
- Use `-d` (lowercase) for **safe deletion**
- Use `-D` (uppercase) only when **sure** about discarding work
- **Coordinate with team** before deleting shared remote branches

## ✅ Verification Commands
```
git branch -vv     # Check tracking
git status         # Current branch status
git ls-remote --heads origin  # Remote branches
```

