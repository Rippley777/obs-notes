In WireGuard, a **peer** is any device participating in the VPN. Each peer requires its own unique [[configuration file]] because each one has:

- A **private key** and a **public key**.
- Its **own IP address** within the VPN's subnet.

The `AllowedIPs` parameter in the `[Peer]` section specifies what traffic the peer is allowed to route.

#### Example Use Case:

1. **Server Configuration (`wg0.conf`)**:
    
    - The server acts as the "hub" for multiple peers:
        
        `[Interface] PrivateKey = <server_private_key> Address = 10.0.0.1/24 ListenPort = 51820  [Peer] PublicKey = <peer1_public_key> AllowedIPs = 10.0.0.2/32 PersistentKeepalive = 25  [Peer] PublicKey = <peer2_public_key> AllowedIPs = 10.0.0.3/32`
        
2. **Peer 1 Configuration**:
    
    `[Interface] PrivateKey = <peer1_private_key> Address = 10.0.0.2/24  [Peer] PublicKey = <server_public_key> AllowedIPs = 0.0.0.0/0  # Route all traffic through the VPN Endpoint = <server_ip>:51820 PersistentKeepalive = 25`
    
3. **Peer 2 Configuration**:
    
    `[Interface] PrivateKey = <peer2_private_key> Address = 10.0.0.3/24  [Peer] PublicKey = <server_public_key> AllowedIPs = 0.0.0.0/0 Endpoint = <server_ip>:51820 PersistentKeepalive = 25`
    

---

### Summary

- Add the configuration file in `/etc/wireguard/` on Linux systems or import it into the WireGuard application on other platforms.
- Each **peer** in the VPN requires a unique configuration file with its own private/public keys and IP address.
- A "peer" refers to a VPN participant (like a client or server), not a separate VPN connection. Each peer can connect to one or more other peers as defined in its configuration.