## Index

---
---
---

### Branches
```powershell
# Rename the current branch
git branch -m main

# If I've already pushed to remote
git branch -m master main
git push -u origin main
# Change the default branch on GitHub.
# Delete the old master branch from remote.
git push origin --delete master

# Set the default branch name globally
git config --global init.defaultBranch main
```