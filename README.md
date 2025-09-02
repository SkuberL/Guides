# Guides
Guides that I found using Internet and AI-search for programming

# Resources

MarkDown Editor

    https://dillinger.io/

# WSL

## Shrink ext4.vhdx file

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
