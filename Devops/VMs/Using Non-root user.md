Using a non-root user on a Linux virtual machine (VM) web server is a good practice for security. Here's how you can create and configure a secondary user for this purpose:

---

### 1. **Create a New User**

Open your terminal and run:

`sudo adduser <username>`

Replace `<username>` with the desired username. You'll be prompted to:

- Set a password.
- Fill in additional information (you can press Enter to skip).

---

### 2. **Grant Administrative Privileges (Optional)**

If the user needs administrative permissions (e.g., to use `sudo`):

`sudo usermod -aG sudo <username>`

---

### 3. **Set Up SSH for the New User**

If you're using SSH to connect to the server:

- Switch to the new user:

    `su - <username>`
    
- Create an `.ssh` directory and set appropriate permissions:
    
    `mkdir ~/.ssh 
    `chmod 700 ~/.ssh`
    
- Add your public key to the `authorized_keys` file:
    
    `nano ~/.ssh/authorized_keys`
    
    Paste your public key and save the file.
- Set correct permissions:
    
    `chmod 600 ~/.ssh/authorized_keys`
    

---

### 4. **Disable Root SSH Login**

To enhance security, disable root login via SSH:

- Edit the SSH configuration file:
    
    bash
    
    Copy code
    
    `sudo nano /etc/ssh/sshd_config`
    
- Look for the line:
    
    plaintext
    
    Copy code
    
    `PermitRootLogin yes`
    
    Change it to:
    
    plaintext
    
    Copy code
    
    `PermitRootLogin no`
    
- Restart the SSH service:
    
    bash
    
    Copy code
    
    `sudo systemctl restart sshd`
    

---

### 5. **Adjust File Permissions for Web Server**

- If the user will manage web server files (e.g., `/var/www`), adjust ownership:
    
    bash
    
    Copy code
    
    `sudo chown -R <username>:<username> /var/www`
    
- If you need group-based permissions, you can create a group and add the user:
    
    bash
    
    Copy code
    
    `sudo groupadd webusers sudo usermod -aG webusers <username> sudo chown -R :webusers /var/www sudo chmod -R 775 /var/www`
    

---

### 6. **Test the Configuration**

- Log in as the new user:
    
    bash
    
    Copy code
    
    `ssh <username>@<server-ip>`
    
- Ensure the user can perform tasks required for the web server (e.g., manage files, restart services).

---

This setup ensures the new user has sufficient privileges for managing the web server while keeping root access restricted for better security.