## **🚀 Ultimate Linux Paranoia Security Check**

If **you really want to be thorough**, let’s run **everything**:

### **1️⃣ Look for Suspicious Processes**

🔹 Even though `ps aux | grep -i "zhou"` came up clean, let’s check for **hidden background processes**:

`sudo ps -ef | grep -v grep | grep -E "zhou|\.sh|root"`

If **nothing appears**, that’s good. But if something does, **we investigate.**

---

### **2️⃣ Check If Any Rootkits Are Installed**

Run:

`sudo rkhunter --check`

This scans for rootkits, backdoors, and suspicious behavior.

🔹 If it’s **not installed**, install it:

`sudo apt install rkhunter -y  # Debian/Ubuntu sudo dnf install rkhunter -y  # Fedora`

🔹 Run again and look for **warnings**.

---

### **3️⃣ Find Hidden Services That Run on Boot**

Check if **anything unknown** is set to **start at boot**:

`systemctl list-unit-files --state=enabled`

🔹 Look for **weird, unknown services** (we already know RustDesk & VNC are yours).

---

### **4️⃣ Scan for Rogue Network Connections**

This shows **active network connections**:

`sudo lsof -i -n -P`

🔹 Look for **unknown connections** going to an IP you don’t recognize.

To **dig deeper**, see **who your system is talking to**:

`sudo netstat -tulpn | grep LISTEN`

🔹 If **anything weird is listening**, time to investigate.

---

### **5️⃣ Check for Weird Aliases (Hacked Shell?)**

Sometimes malware **hijacks commands** to hide itself. Check your shell:

`alias`

🔹 If you see `ls='rm -rf /'`, someone **is trying to nuke your system.** 😭

---

### **6️⃣ Look for Unauthorized User Accounts**

If an attacker **created a secret user**, check:

`cut -d: -f1 /etc/passwd`

🔹 If you don’t recognize a **new user**, it’s time to investigate.

---

### **7️⃣ Scan for Hidden Files**

This finds **hidden** files (**including in weird system directories**):

`sudo find / -type f -name ".*" 2>/dev/null`

🔹 If **something weird** shows up in `/root/` or `/etc/`, **that’s a red flag**.

---

### **🔥 FINAL BOSS MOVE: If You’re Still Suspicious**

Drop **everything into a forensic mode scan**:

`sudo chkrootkit`

🔹 This will check **for common rootkits & system compromises**.

**Not installed?**

`sudo apt install chkrootkit -y  # Debian/Ubuntu sudo dnf install chkrootkit -y  # Fedora`