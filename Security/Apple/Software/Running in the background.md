### **1. Check What’s Running in the Background**

#### **Option 1: Look at Background Items in macOS Settings**

1. Open **System Settings** → **General** → **Login Items**.
2. Scroll down to **“Allow in the background”** (this is where you saw the suspicious item).
3. If you see **"zhou huabing"** or any other weird app listed, **toggle it off** and click **Remove**.

#### **Option 2: Check Launch Agents & Daemons (Manual)**

Run these commands in **Terminal** to check for suspicious startup scripts:

##### **User Launch Agents (run at login)**


`ls -la ~/Library/LaunchAgents/`

##### **System-wide Launch Agents (run at login for all users)**
`ls -la /Library/LaunchAgents/`

##### **System-wide Launch Daemons (run even before login)**

`ls -la /Library/LaunchDaemons/`

If you see anything suspicious **like `zhouhuabing.plist` or a `.sh` script** in these directories, it’s likely the culprit.