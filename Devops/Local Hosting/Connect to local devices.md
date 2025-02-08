

This guide will show you how to connect to and identify devices on your local network using various tools and techniques.

---

## **1. Using the Router**

1. **Access the Router's Admin Panel:**
   - Open a web browser.
   - Enter the router's IP address (e.g., `192.168.1.1` or `192.168.0.1`).
   - Log in with the router's admin credentials (check the manual or device label for default credentials if unknown).

2. **Check Connected Devices:**
   - Look for a section like **"Connected Devices"**, **"Attached Devices"**, or **"DHCP Client List"**.
   - This will list the devices with their IP addresses, MAC addresses, and sometimes hostnames.

---

## **2. Using Command-Line Tools**

### **Linux/macOS**

#### **View ARP Table**
```bash
arp -a
```
This command lists all devices connected to the network along with their IP and MAC addresses.

#### **Using Nmap**
1. Install Nmap if not already installed:
   ```bash
   sudo apt install nmap       # On Debian/Ubuntu
   brew install nmap           # On macOS
   ```
2. Perform a network scan:
   ```bash
   nmap -sn 192.168.1.0/24
   ```
   Replace `192.168.1.0/24` with your network's subnet.

### **Windows**

#### **View ARP Table**
```cmd
arp -a
```
This lists connected devices with their IP and MAC addresses.

#### **Using Nmap**
1. Download and install Nmap from [nmap.org](https://nmap.org/).
2. Open Command Prompt or PowerShell and scan:
   ```cmd
   nmap -sn 192.168.1.0/24
   ```

---

## **3. Using Network Scanning Tools**

### **Fing**
- Install **Fing** on your phone or desktop:
  - Android/iOS: Available in app stores.
  - macOS/Windows: Download from [fing.com](https://www.fing.com/).
- Run the app to scan your network and list all connected devices.

### **Advanced IP Scanner (Windows)**
1. Download from [advanced-ip-scanner.com](https://www.advanced-ip-scanner.com/).
2. Install and run the tool.
3. Scan the network to see all connected devices.

### **Zenmap (Nmap GUI)**
1. Install Zenmap from [nmap.org](https://nmap.org/zenmap/).
2. Launch the GUI and enter the target network range (e.g., `192.168.1.0/24`).
3. Start the scan and review the results.

---

## **4. Using Wireshark**

1. Install Wireshark from [wireshark.org](https://www.wireshark.org/).
2. Run Wireshark with admin/root privileges.
3. Select the appropriate network interface.
4. Monitor network traffic:
   - Use filters to narrow down results (e.g., `ip.addr == 192.168.1.1`).

---

## **5. On Android/iOS**

1. Install network scanning apps:
   - **Fing**
   - **Network Scanner**
2. Open the app and start a scan.
3. Review the list of connected devices.

---

## **6. Using Linux Tools**

### **Netdiscover**
1. Install Netdiscover:
   ```bash
   sudo apt install netdiscover
   ```
2. Run the tool to discover devices:
   ```bash
   sudo netdiscover -r 192.168.1.0/24
   ```

### **Nmap**
1. Install Nmap (if not already installed):
   ```bash
   sudo apt install nmap
   ```
2. Scan the network:
   ```bash
   sudo nmap -sn 192.168.1.0/24
   ```

---



## **7. Remotely Logging Into Devices**

Once you have the hostname, IP address, and credentials, you can remotely log into a device to move files around:

### **Using SSH (Linux/Mac/Windows)**

1. Open a terminal (or PowerShell on Windows with OpenSSH installed).
2. Connect to the device:
   ```bash
   ssh username@192.168.x.x
   ```
   Replace `username` with the device's username and `192.168.x.x` with the device's IP address.
3. Use SCP (Secure Copy Protocol) to move files:
   - **Copy files to the device:**
     ```bash
     scp /path/to/local/file username@192.168.x.x:/path/to/remote/directory
     ```
   - **Copy files from the device:**
     ```bash
     scp username@192.168.x.x:/path/to/remote/file /path/to/local/directory
     ```

### **Using SFTP**
1. Start an SFTP session:
   ```bash
   sftp username@192.168.x.x
   ```
2. Use commands like `get` and `put` to transfer files.
   - Example:
     ```bash
     get /path/to/remote/file /path/to/local/directory
     put /path/to/local/file /path/to/remote/directory
     ```

### **Using SMB/Windows File Sharing**
1. Enable file sharing on the target device (if not already enabled).
2. Access the shared folders:
   - **On Windows:**
     - Open File Explorer and enter `\\192.168.x.x` in the address bar.
   - **On Linux:**
     - Use a file manager or mount the share with:
       ```bash
       sudo mount -t cifs -o username=your_username //192.168.x.x/share /mnt/share
       ```
3. Transfer files using the file manager or command line.

---


## **8. Opening SSH Port on Different Operating Systems**

To enable SSH access, ensure the SSH port (default is 22) is open and the SSH server is running. The following steps will also enable password authentication for temporary local setups.

### **Linux**
1. Install the OpenSSH server:
   ```bash
   sudo apt install openssh-server       # On Debian/Ubuntu
   sudo yum install openssh-server       # On CentOS/RHEL
   ```
2. Start the SSH service:
   ```bash
   sudo systemctl start ssh
   sudo systemctl enable ssh
   ```
3. Allow password authentication:
   - Edit the SSH configuration file:
     ```bash
     sudo nano /etc/ssh/sshd_config
     ```
   - Find and set the following lines:
     ```
     PasswordAuthentication yes
     PermitRootLogin yes   # Only if root access is necessary
     ```
   - Save the file and restart the SSH service:
     ```bash
     sudo systemctl restart ssh
     ```
4. Check that port 22 is open:
   ```bash
   sudo ufw allow ssh
   sudo ufw enable
   ```

### **macOS**
1. Open **System Preferences > Sharing**.
2. Enable **Remote Login**.
3. Specify which users are allowed to connect via SSH.
4. macOS supports password authentication by default.

### **Windows**
1. Install OpenSSH server (if not already installed):
   - Go to **Settings > Apps > Optional Features**.
   - Add **OpenSSH Server**.
2. Start the SSH service:
   ```powershell
   Start-Service sshd
   ```
3. Allow password authentication:
   - Open the SSH configuration file:
     ```powershell
     notepad $env:ProgramData\ssh\sshd_config
     ```
   - Find and set the following lines:
     ```
     PasswordAuthentication yes
     PermitRootLogin yes   # Only if root access is necessary
     ```
   - Save the file and restart the SSH service:
     ```powershell
     Restart-Service sshd
     ```
4. Configure the firewall to allow SSH:
   ```powershell
   New-NetFirewallRule -Name "OpenSSH" -DisplayName "OpenSSH" -Protocol TCP -LocalPort 22 -Action Allow -Direction Inbound
   ```
5. Ensure the SSH service starts on boot:
   ```powershell
   Set-Service -Name sshd -StartupType Automatic
   ```

### **General Notes**
- Ensure port forwarding is configured on your router if accessing the device from outside the local network.
- Use a strong password or SSH keys for authentication for non-temporary setups.

---

## **9. Tips for Security**

- Regularly check for unknown devices on your network.
- Secure your Wi-Fi with WPA3 encryption and a strong password.
- Use MAC address filtering if supported by your router.
- Disable unused services on your devices to reduce exposure.
