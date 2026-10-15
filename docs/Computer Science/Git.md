
# Git


## work on someone else's code
When work on someone else's repo (original repo), push only to our own repo, and pull updates from the original repo.

- origin = your private repo (push here)
- upstream = original repo (pull only)

### One‑time Setup: 
```bash
# 1) Clone the original repo (example GIOS course project 1)
git clone https://github.gatech.edu/gios-spr-26/pr1.git
cd pr1

# 2) Point origin to your repo
git remote set-url origin https://github.gatech.edu/<gtid>/gios-spr-26-pr1.git

# 3) Add the original repo as upstream (read‑only)
git remote add upstream https://github.gatech.edu/gios-spr-26/pr1.git

# 4) Disable pushing to upstream (safety)
git remote set-url --push upstream PUSH_DISABLED

# 5) Verify
git remote -v
```

### Later Workflow (sync update + develop)
```bash
# Optional: If you have local uncommitted changes before pulling
git stash -u

# Get updates from original repo when needed
git checkout main
git pull --rebase upstream main
# Optional: keep your private repo's main in sync too
git push origin main

# Optional: If you have local uncommitted changes and ran git stash -u before
git stash pop

# Work on your code
# Create a new feature branch (Don’t develop directly on main!). Use -b only once for first creation
git checkout -b my-feature

# Push your feature branch to your private repo
git push -u origin my-feature
```

Then next time on same feature branch:
```bash
git checkout my-feature
git pull --rebase
git push
```


### Move and Rename

#### Option 1 : Preferred (keeps history clearly)

- Move a file or folder:
  ```bash
  git mv "Old Path" "New Path"
  ```

##### Common Examples within the same path

- Rename a file:
  ```bash
  git mv old.md new.md
  ```

- Move a folder:
  ```bash
  git mv "Old Folder Name" "New Folder Name"
  ```
#### Option 2 : If you already moved files outside Git

1. Stage all changes:
  ```bash
  git add -A
  ```

2. Check rename detection:
  ```bash
  git status -sb
  ```

3. Commit:
  ```bash
  git commit -m "Move/rename files"
  ```

### Notes

- Git detects renames based on content similarity after staging. You can tune detection: git config diff.renames true
  ```bash
  git config diff.renames true
  ```




