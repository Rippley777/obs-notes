## Passing Data Between WireGuard Server and Client

Passing data between a WireGuard **server** and **client** involves setting up proper routing and ensuring the data flows through the VPN tunnel. Below is a detailed guide to achieve this:

---

### **How Data Flows in WireGuard**

1. **VPN Subnet (Virtual Network):**
    
    - The **server** and **client** communicate using their VPN-assigned IPs (e.g., `10.0.0.1` for the server and `10.0.0.2` for the client).
    - These IPs are isolated within the VPN subnet (`10.0.0.0/24`).
2. **Routing:**
    
    - The **server** acts as the gateway that routes traffic between the VPN and other networks (e.g., the internet or local resources).
    - The **client** routes traffic through the VPN based on its `AllowedIPs` configuration.
3. **Data Transfer Workflow:**
    
    - A client sends data destined for the VPN or external networks.
    - The server receives this data, processes it, and forwards it to the target network or resource.
    - Replies are sent back through the server to the client.

---

### **1. Basic Server-to-Client Data Passing**

#### **Scenario: Access Server Resources**

If you want the client to access resources on the server (e.g., a local web server or file), follow these steps:

1. **Ensure Routing:**
    
    - The server must know how to route traffic to the client. This is typically handled by the WireGuard configuration:
    
    **Server Configuration:**
    
    ```ini
    [Peer]
    PublicKey = <client_public_key>
    AllowedIPs = 10.0.0.2/32
    ```
    
    **Client Configuration:**
    
    ```ini
    [Peer]
    PublicKey = <server_public_key>
    Endpoint = <server_public_ip>:51820
    AllowedIPs = 10.0.0.1/32
    ```
    
2. **Test Communication:**
    
    - From the client, ping the server’s VPN IP:
        
        ```bash
        ping 10.0.0.1
        ```
        
3. **Access a Service on the Server:**
    
    - If the server is running a web service (e.g., NGINX), access it from the client:
        
        ```bash
        curl http://10.0.0.1
        ```
        

---

### **2. Pass Internet Traffic Through the Server**

If the goal is for the client to route all internet traffic through the server (for privacy or security), additional steps are required.

#### **On the Server: Enable NAT**

1. Add a NAT rule to your server’s firewall:
    
    ```bash
    sudo iptables -t nat -A POSTROUTING -s 10.0.0.0/24 -o eth0 -j MASQUERADE
    ```
    
    - Replace `eth0` with the name of your server’s network interface.
2. Enable IP forwarding on the server:
    
    ```bash
    sudo sysctl -w net.ipv4.ip_forward=1
    ```
    
    Make it permanent by editing `/etc/sysctl.conf`:
    
    ```ini
    net.ipv4.ip_forward=1
    ```
    
3. Restart WireGuard to apply changes:
    
    ```bash
    sudo wg-quick down wg0
    sudo wg-quick up wg0
    ```
    

#### **On the Client: Route All Traffic Through the VPN**

1. In the client’s WireGuard configuration, set:
    
    ```ini
    AllowedIPs = 0.0.0.0/0, ::/0
    ```
    
    - This routes all traffic (IPv4 and IPv6) through the VPN.
2. Test the setup:
    
    - Check the client’s public IP:
        
        ```bash
        curl ifconfig.me
        ```
        
    - It should return the server’s public IP.

---

### **3. Access Local Network Resources**

If you want the client to access devices on the server’s local network (e.g., a printer or NAS):

#### **On the Server: Enable LAN Routing**

1. Add a route for the local network:
    
    ```bash
    sudo iptables -A FORWARD -i wg0 -o eth0 -s 10.0.0.0/24 -d 192.168.1.0/24 -j ACCEPT
    sudo iptables -A FORWARD -i eth0 -o wg0 -d 10.0.0.0/24 -s 192.168.1.0/24 -j ACCEPT
    ```
    
    - Replace `eth0` with the server’s LAN interface.
    - Replace `192.168.1.0/24` with your LAN’s subnet.
2. Update the client’s `AllowedIPs`:
    
    ```ini
    AllowedIPs = 0.0.0.0/0, ::/0, 192.168.1.0/24
    ```
    
3. Test LAN Connectivity:
    
    - From the client, ping a local device (e.g., `192.168.1.100`):
        
        ```bash
        ping 192.168.1.100
        ```
        

---

### **4. Advanced Scenarios**

#### **Multi-Client Communication**

If multiple clients need to communicate through the VPN:

- Add each client as a peer on the server.
- Ensure `AllowedIPs` for each peer include the other clients’ IPs.

**Example:**

- Client 1: `10.0.0.2`
- Client 2: `10.0.0.3`

**Server Configuration:**

```ini
[Peer]
PublicKey = <client1_public_key>
AllowedIPs = 10.0.0.2/32

[Peer]
PublicKey = <client2_public_key>
AllowedIPs = 10.0.0.3/32
```

#### **VLAN Integration**

- Configure VLANs on the server to segment network traffic.
- Use `iptables` rules to forward traffic between the VPN and VLANs.

---

### **Troubleshooting Tips**

1. **Check WireGuard Status:**
    
    ```bash
    sudo wg show
    ```
    
    Look for "latest handshake" and data transfer under "transfer."
    
2. **Verify Routing:**
    
    ```bash
    ip route
    ```
    
    Ensure traffic for `10.0.0.0/24` is routed through `wg0`.
    
3. **Test Connectivity:**
    
    - Ping VPN IPs, LAN devices, or external addresses.
4. **Inspect Logs:**
    
    ```bash
    sudo journalctl -u wg-quick@wg0
    ```
    

---

