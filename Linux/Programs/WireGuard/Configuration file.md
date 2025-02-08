### Where to Add the Configuration File

1. **On Linux**:
    
    - Save the configuration file in `/etc/wireguard/`.
    - For example, if your configuration file is named `wg0.conf`, its path would be `/etc/wireguard/wg0.conf`.
    - Use the `wg-quick` command to manage the interface:
        
        `sudo wg-quick up wg0 sudo wg-quick down wg0`
        
2. **On Other Operating Systems**:
    
    - For Windows, macOS, or mobile apps, use the WireGuard GUI. The configuration file can be imported directly into the application.
    - For the GUI, you’ll usually copy-paste the configuration details or select the file to import.
3. **For Docker Containers**:
    
    - Mount the configuration file into the container at the appropriate location. For example:
        
        `docker run --rm -v /path/to/wg0.conf:/etc/wireguard/wg0.conf my-wireguard-image`


### **Client Configuration**

1. Create a WireGuard configuration file for the client:

    `sudo nano /etc/wireguard/wg0.conf`
    
2. Example `wg0.conf` for the **client**:
    
```
[Interface]
Address = 10.0.0.2/24            # Client's internal VPN IP
PrivateKey = <client_private_key>  # Replace with client's private key
DNS = 1.1.1.1                    # Optional: Use Cloudflare DNS (or another DNS)

[Peer]
PublicKey = <server_public_key>  # Replace with server's public key
Endpoint = <server_ip>:51820     # Replace <server_ip> with your server's public IP or domain
AllowedIPs = 0.0.0.0/0, ::/0     # Route all traffic through the VPN
PersistentKeepalive = 25         # Prevent NAT timeouts (optional)


```
    
3. Replace placeholders:
    
    - `<client_private_key>`: Generate the private key:
    
        `wg genkey`
        
    - `<server_public_key>`: Use the server’s public key, which you can generate with:
    
        `echo <server_private_key> | wg pubkey`


### **Server Configuration**

1. Create the WireGuard configuration file for the server:

    `sudo nano /etc/wireguard/wg0.conf`
    
2. Example `wg0.conf` for the **server**:
    
```

	[Interface]
Address = 10.0.0.1/24            # Server's internal VPN IP
ListenPort = 51820               # Default WireGuard port
PrivateKey = <server_private_key>  # Replace with server's private key
SaveConfig = true

# Allow traffic forwarding for VPN clients
PostUp = iptables -A FORWARD -i %i -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i %i -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE

# Client 1
[Peer]
PublicKey = <client_public_key>  # Replace with the client's public key
AllowedIPs = 10.0.0.2/32        # Client's VPN IP

```
    
3. Replace placeholders:
    
    - `<server_private_key>`: Generate a private key using:
   
        `wg genkey`
        
    - `<client_public_key>`: Use the client’s public key (see client config below).
4. Enable IP forwarding in `/etc/sysctl.conf`:
 
    `sudo nano /etc/sysctl.conf`
    
    Uncomment or add:

    `net.ipv4.ip_forward=1`
    
    Apply the change
    `sudo sysctl -p`