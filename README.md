Guides and usable resources that I found using Internet and AI-search

# Resources

MarkDown Editor

[Online Markdown Editor - Dillinger](https://dillinger.io/)
---

# WSL - common commands

1. **List your currently installed WSL distributions:**
```powershell
wsl --list --verbose
```

2. **Set `Ubuntu-22.04` as the default distribution:**
```powershell
wsl --setdefault Ubuntu-22.04
```

# WSL - relocate ext4.vhdx file

1. **Export your current Ubuntu-22.04 WSL distro to a tar file** (store it on the drive with enough space):
```powershell
wsl --export Ubuntu-22.04 D:\wsl_backup\ubuntu2204.tar
```

2. **Unregister the current Ubuntu-22.04 distro** (this removes it from WSL but does not delete the export):
```powershell
wsl --unregister Ubuntu-22.04
```

3. **Import the distro to a new location** (where you want it moved, for example D:\WSL\Ubuntu22.04):
```powershell
wsl --import Ubuntu-22.04 D:\WSL\Ubuntu22.04 D:\wsl_backup\ubuntu2204.tar --version 2
```

4. **Verify your new distro location** by listing WSL distros:
```powershell
wsl --list --verbose
```

5. **Launch the distro as usual**:
```powershell
wsl -d Ubuntu-22.04
```



# WSL - Shrink ext4.vhdx file

To shrink an ext4.vhdx file (common for WSL2 or Docker on Windows using dynamic virtual hard disks), you can follow these steps:

1. **Clean up the disk inside the VM or WSL:**
   - Delete unnecessary files, clear caches, and empty the trash to free up space inside the virtual disk.
   - Use commands like `sudo apt-get clean` and `fstrim -v /` inside the Linux system to free up unused blocks.

2. **Shutdown WSL or VM:**
   - Run in Windows PowerShell or CMD as Administrator:
     ```
     wsl --shutdown
     ```
   - This ensures no processes are locking the vhdx file.

3. **Use `diskpart` to compact the vhdx file:**
   - Open PowerShell as Administrator.
   - Enter diskpart:
     ```
     diskpart
     ```
   - Select the vhdx file (replace with your actual vhdx path):
     ```
     select vdisk file="C:\Users\<user>\AppData\Local\Packages\<distro>\LocalState\ext4.vhdx"
     ```
   - Run compact:
     ```
     compact vdisk
     ```
   - After the process finishes, type `exit` to quit diskpart.

4. **Alternative with `Optimize-VHD` PowerShell cmdlet (Windows Pro and higher):**
   - You can also run:
     ```
     Optimize-VHD -Path "C:\path\to\ext4.vhdx" -Mode Full
     ```
   - This also compacts the virtual disk efficiently.

Following this process can reduce the size of your ext4.vhdx file significantly by reclaiming unused space.

Note:
- Make sure no WSL or Docker instances are running while performing this.
- The effectiveness depends on how much free space was inside the virtual disk before shrinking.

These instructions have proven effective for many users to shrink the WSL2 ext4.vhdx virtual disk. You can find a detailed step-by-step guide on this topic in multiple online resources.
