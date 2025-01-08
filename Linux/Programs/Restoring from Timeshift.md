### **Pre-requisites**

1. A valid Timeshift backup on an accessible storage device (external drive, partition, etc.).
2. A working live USB/DVD of Ubuntu (or the Timeshift Live environment, if available) for recovery if your system is unbootable.

---

### **Restoring Your System Using Timeshift**

#### **If Your System Boots Normally**

1. **Launch Timeshift:**
    
    - Open Timeshift from your applications menu or via terminal:
        `sudo timeshift --restore`
        
2. **Select the Snapshot:**
    
    - Timeshift will show a list of available snapshots. Select the one you want to restore.
3. **Choose the Target Partition:**
    
    - Confirm the partition where Ubuntu is installed (e.g., `/dev/sda2`).
4. **Review and Confirm:**
    
    - Timeshift will display details of the restoration process. Confirm and proceed.
5. **Wait for Completion:**
    
    - The restoration process will begin. This may take some time, depending on the size of the snapshot.
6. **Reboot:**
    
    - Once the process completes, reboot your system.

---

#### **If Your System Is Unbootable**

1. **Boot into a Live Environment:**
    
    - Use an Ubuntu Live USB/DVD or any Linux live environment to boot your computer.
2. **Install Timeshift (if not pre-installed):**
    
    - In the live environment, install Timeshift:
        `sudo apt update sudo apt install timeshift`
        
3. **Mount Your Root Partition:**
    
    - Find your root partition (where Ubuntu is installed):
        
        `sudo fdisk -l`
        
    - Mount it to a directory (e.g., `/mnt`):
        
        `sudo mount /dev/sdXn /mnt`
        
        Replace `/dev/sdXn` with your actual partition identifier.
4. **Access the Backup Location:**
    
    - If your backup is on an external drive or another partition, mount it as well:
        
        `sudo mount /dev/sdYn /media/backup`
        
        Replace `/dev/sdYn` with the identifier of your backup drive.
5. **Run Timeshift:**
    
    - Start Timeshift with root privileges:
        
        `sudo timeshift --restore`
        
    - Timeshift will detect the snapshots in the backup location.
6. **Restore the Snapshot:**
    
    - Follow the prompts to select the desired snapshot and confirm the restoration.
7. **Fix GRUB (Optional):**
    
    - If the GRUB bootloader is broken, reinstall it:
        
        `sudo grub-install --boot-directory=/mnt/boot /dev/sdX`
        
        Replace `/dev/sdX` with your disk identifier (not the partition).
8. **Reboot:**
    
    - Once the restoration is complete, unmount all partitions:
        
        `sudo umount /mnt sudo umount /media/backup`
        
    - Reboot your system.

---

### **Important Notes**

- **Data Preservation:** Timeshift does not back up user files (in `/home`) by default. Check if you need to restore them separately.
- **Recheck Configuration:** If you encounter errors after restoration, verify configuration files (e.g., `/etc/fstab`) and hardware compatibility.
- **Backup Again After Restore:** Once your system is restored and stable, create a fresh backup.