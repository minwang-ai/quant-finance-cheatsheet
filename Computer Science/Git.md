# Git Cheat Sheet

## Move and Rename

### Option 1 : Preferred (keeps history clearly)
- Move a file or folder:
  ```bash
  git mv "Old Path" "New Path"
  ```

#### Common Examples within the same path
- Rename a file:
  ```bash
  git mv old.md new.md
  ```
- Move a folder:
  ```bash
  git mv "Old Folder Name" "New Folder Name"
  ```
### Option 2 : If you already moved files outside Git
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

## Notes
- Git detects renames based on content similarity after staging. You can tune detection: git config diff.renames true
  ```bash
  git config diff.renames true
  ```




