## **🔒 Before Resetting – Avoid Getting Locked Out**

If you **do** go for a full wipe, **do this first** to avoid an accidental brick:

### **1️⃣ Disable Activation Lock (iCloud Lock)**

This is **CRITICAL**—if Activation Lock is enabled, your Mac will **demand your Apple ID** after a reset.

- **Go to:** `System Settings` → Click your name (Apple ID) → **Find My Mac**
- **Toggle OFF** `Find My Mac` (it will ask for your password)
- **Sign out** of iCloud fully (to avoid any lingering lock)

🔹 **Check it’s really off!** Run this in Terminal:

`sudo ioreg -l | grep "ActivationLockStatus"`

- If it returns `1`, **Activation Lock is ON** (bad).
- If it returns `0`, **you’re safe to reset**.

---

### **2️⃣ Reset Your Password (If Needed)**

If you think there’s **any chance** you’ll forget your password after wiping, reset it now:

`sudo passwd $(whoami)`

**OR** reset via `System Settings` → `Users & Groups`.

---

### **3️⃣ Make a Bootable macOS USB (Just in Case)**

If **anything goes wrong**, having a macOS installer on USB **saves your life**:

`sudo /Applications/Install\ macOS\ Ventura.app/Contents/Resources/createinstallmedia --volume /Volumes/USB`

(Change `Ventura.app` to your macOS version.)

---

### **4️⃣ Backup Anything Important**

- **iCloud Drive / Google Drive / External Disk** – Whatever works for you.
- Run this command to **list what’s eating your storage** before you copy junk:
    
    `sudo du -sh /* | sort -h`
    

---

## **🛠 Reset Time – If You’re Committed**

1. **Boot into macOS Recovery**
    
    - **Intel Mac:** `⌘ Command + R` at startup.
    - **Apple Silicon (M1/M2):** Hold **Power** until "Options" appears.
2. **Erase the Drive**
    
    - Open **Disk Utility** → Select `Macintosh HD`
    - Click **Erase**, set to `APFS` + `MacOS Extended (Journaled)`.
    - **IMPORTANT:** Also erase `Macintosh HD - Data` if it exists.
3. **Reinstall macOS**
    
    - Go back to **macOS Utilities** → **Reinstall macOS**
    - Follow instructions, let it do its thing.
4. **Set Up Like New**
    
    - After reboot, **sign in fresh** (use iCloud if needed).
    - **DO NOT restore from Time Machine**—it’ll bring back junk.