### Resources
[Get started with Windows PowerShell](https://learn.microsoft.com/en-us/training/paths/get-started-windows-powershell)

### Deletion
```powershell
# Delete an empty directory
Remove-Item "C:\path\to\directory"

# Delete a directory and all its contents (files and subdirectories)
Remove-Item "C:\path\to\directory" -Recurse

# Delete with confirmation prompt for each item
Remove-Item "C:\path\to\directory" -Recurse -Confirm

# Delete without any confirmation prompts (use carefully!)
Remove-Item "C:\path\to\directory" -Recurse -Force
```

### List
```powershell
# List items
ls

# List hidden items
ls -Force
```