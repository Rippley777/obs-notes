
If your USB drive keeps getting split into small partitions on macOS, follow these steps to completely wipe and repartition it properly.

### **Step 1: Identify Your USB Drive**

1. Plug in the USB drive.
2. Open **Terminal** and type:
    
    ```sh
    diskutil list
    ```
    
3. Look for your USB drive (e.g., `/dev/disk2`). Ensure you identify the correct disk, as erasing it will delete all data.

### **Step 2: Unmount and Erase the Drive**

4. Unmount the drive:
    
    ```sh
    diskutil unmountDisk /dev/diskX
    ```
    
    (Replace `diskX` with your actual disk number, e.g., `/dev/disk2`.)
    
5. Wipe all partitions:
    
    ```sh
    diskutil eraseDisk free EMPTY /dev/diskX
    ```
    
    This removes all partitions but does not create a new file system.
    

### **Step 3: Format the Drive with a Single Partition**

To create a new partition with a GUID Partition Table (GPT) and format it as exFAT (or any format you need):

```sh
diskutil partitionDisk /dev/diskX GPT exFAT "USB" 100%
```

- Replace **"USB"** with your preferred name.
- Replace **exFAT** with the format you want (`HFS+`, `FAT32`, `APFS`, etc.).

### **Alternative: Use Disk Utility (GUI)**

6. Open **Disk Utility** (`Cmd + Space`, type "Disk Utility").
7. Select your USB drive (not just a partition).
8. Click **Erase**, then choose:
    - **Format**: `exFAT` (for compatibility) or `Mac OS Extended (Journaled)` (for macOS use)
    - **Scheme**: `GUID Partition Map`
9. Click **Erase**.

### **Fix for Persistent Small Partitions**

If you still see multiple partitions appearing, hidden system partitions may be causing issues. Try:

```sh
   diskutil eraseDisk JHFS+ "USB" GPT /dev/diskX
```

This ensures a clean format with macOS-compatible settings.

Let me know if you need further assistance! 🚀