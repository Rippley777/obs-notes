### 1. **Set Up Your Public Key on the VM**

- First, copy your **public key** to the VM:
    `ssh-copy-id -i ~/.ssh/id_rsa.pub user@your-vm-ip`
    
    Alternatively, manually append the key:
    
    `ssh user@your-vm-ip mkdir -p ~/.ssh echo "your-public-key" >> ~/.ssh/authorized_keys chmod 600 ~/.ssh/authorized_keys chmod 700 ~/.ssh`
    
    Replace `your-public-key` with the content of your `.pub` key.

---

### 2. **Lock Down SSH Configuration**

Edit the SSH daemon configuration file to enforce stronger security policies:
`sudo nano /etc/ssh/sshd_config`

Update or add the following settings:

- **Disable Root Login**:
    
    `PermitRootLogin no`
    
- **Disable Password Authentication**:
    
    `PasswordAuthentication no`
    
- **Allow Only Specific Users**: Limit SSH access to specific users (replace `your-username`):
    
    `AllowUsers your-username`
    
- **Use Protocol 2 Only**: SSH Protocol 2 is more secure:
    
    `Protocol 2`
    
- **Disable Unused Authentication Methods**:
    
    `ChallengeResponseAuthentication no UsePAM no`
    

Save and exit the file, then restart SSH:

`sudo systemctl restart ssh`

---

### 3. **Set File Permissions**

Ensure your `.ssh` directory and files on the VM are properly secured:

`chmod 700 ~/.ssh chmod 600 ~/.ssh/authorized_keys chmod 644 ~/.ssh/known_hosts`

---

### 4. **Set Up a Firewall**

Use a firewall to restrict SSH access to trusted IPs only:

- Install `ufw` (Uncomplicated Firewall):
    
    `sudo apt install ufw sudo ufw allow ssh`
    
- Allow access from specific IPs only (replace `your-ip`):
    `sudo ufw allow from your-ip to any port 22`
    
- Enable the firewall:
    
    `sudo ufw enable`
    

---

### 5. **Limit SSH Access by Port**

Change the default SSH port (optional, but adds obscurity):

- Edit `/etc/ssh/sshd_config`:
    
    `Port 2222`
    
- Restart SSH:
    
    `sudo systemctl restart ssh`
    
- Update your firewall to allow the new port:
    
    `sudo ufw allow 2222`
    

Make sure to include the new port in your SSH commands:

`ssh -p 2222 user@your-vm-ip`

---

### 6. **Enable Fail2Ban**

Fail2Ban blocks IPs with repeated failed login attempts:

- Install Fail2Ban:
    
    `sudo apt install fail2ban`
    
- Configure `/etc/fail2ban/jail.local` to protect SSH:
    
    `[sshd] enabled = true port = 22 maxretry = 5 bantime = 1h`
    
- Restart Fail2Ban:
    
    `sudo systemctl restart fail2ban`
    

---

### 7. **Enable 2FA (Optional but Recommended)**

Add two-factor authentication for SSH:

- Install `libpam-google-authenticator`:
    
    `sudo apt install libpam-google-authenticator`
    
- Run the setup:
    
    `google-authenticator`
    
- Enable `ChallengeResponseAuthentication` in `/etc/ssh/sshd_config`:
    
    `ChallengeResponseAuthentication yes`
    
- Restart SSH.

---

### 8. **Monitor Logs for Security**

Periodically check your server logs for suspicious activity:

`sudo cat /var/log/auth.log | grep "Failed" sudo cat /var/log/auth.log | grep "Accepted"`

---

### 9. **Backup Your Private Key**

- Store your private key in a secure location, such as a password manager.
- Never share the private key or leave it exposed on unsecured systems.