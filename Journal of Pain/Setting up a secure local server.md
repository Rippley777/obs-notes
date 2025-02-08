# Docker, Traefik, UFW, and WireGuard: Pain Points and Learnings

## Introduction

This markdown file summarizes the challenges, solutions, and lessons learned during the process of setting up Docker containers, configuring Traefik as a reverse proxy, managing UFW (Uncomplicated Firewall), and setting up WireGuard VPN. These notes aim to provide insights for future reference and troubleshooting.

---

## 1. **Docker and Traefik Setup**

### Pain Points:

1. **Network Configuration:**
    
    - Traefik wasn’t detecting services because it wasn’t connected to the `proxy` network.
    - `app1` was visible in the Docker network, but Traefik wasn’t.
2. **Service Routing:**
    
    - The `/app1` route was unreachable due to incorrect Traefik labels.
    - The default Traefik dashboard worked, but custom services didn’t appear under routers or services.
3. **Permission Issues:**
    
    - The Docker socket (`/var/run/docker.sock`) needed proper access for Traefik.

### Learnings:

- Ensure both Traefik and services are connected to the same Docker network.
- Traefik labels must include:
    - `traefik.enable=true`
    - Correct `PathPrefix` routing rules.
    - The correct internal port (`loadbalancer.server.port`).
- Test service connectivity using `curl` or `wget` from within the Traefik container.

---

## 2. **UFW (Uncomplicated Firewall)**

### Pain Points:

1. **Default Deny Policy:**
    
    - UFW blocked essential traffic, including WireGuard and Docker communication.
2. **Port Conflicts:**
    
    - Opening multiple ports for services caused confusion and misrouting.

### Learnings:

- **Allow Specific Ports:**
    - WireGuard: `sudo ufw allow 51820/udp`
    - Traefik: `sudo ufw allow 80/tcp` and `sudo ufw allow 443/tcp`.
- **Restrict to Specific IPs:**
    - Limit WireGuard to the cloud VM IP:
        
        ```bash
        sudo ufw allow from <cloud_vm_ip> to any port 51820 proto udp
        ```
        
- **Test Rules Incrementally:**
    - Use `ufw status verbose` to verify active rules.

---

## 3. **WireGuard VPN**

### Pain Points:

1. **Configuration Mismatch:**
    
    - The client and server configuration had overlapping IP ranges (`10.0.0.1/24` vs `10.0.0.2/32`).
2. **Connectivity Issues:**
    
    - The server was reachable locally, but not via the VPN.
    - Pings worked, but services didn’t.
3. **IP Forwarding:**
    
    - Traffic didn’t route properly without enabling IP forwarding on the server.

### Learnings:

- Use separate subnets for WireGuard (`10.0.0.0/24`):
    - Server: `10.0.0.1`
    - Client: `10.0.0.2`
- Enable IP forwarding:
    
    ```bash
    sudo sysctl -w net.ipv4.ip_forward=1
    ```
    
    Persist this in `/etc/sysctl.conf`.
- Test VPN traffic with simple tools like `nc` (Netcat):
    
    ```bash
    echo "Hello, WireGuard!" | nc -u <client_ip> 12345
    ```
    

---

## 4. **General Troubleshooting Tips**

### Logs and Debugging:

- **Traefik Logs:**
    
    ```bash
    docker logs traefik
    ```
    
- **Docker Networking:**
    
    ```bash
    docker network inspect <network_name>
    ```
    
- **Service Logs:**
    
    ```bash
    docker logs <service_name>
    ```
    

### Testing Connectivity:

- From Traefik container:
    
    ```bash
    docker exec -it traefik sh
    wget -qO- http://app1:5000
    ```
    
- From the host:
    
    ```bash
    curl http://127.0.0.1/app1
    ```
    

### Configuration Management:

- Back up `docker-compose.yml` files and configuration directories.
- Use version control (e.g., Git) for configuration changes.

---

## Conclusion

This experience reinforced the importance of methodical troubleshooting and network configuration. By addressing Docker networking, Traefik labels, firewall rules, and WireGuard settings, the entire stack was successfully set up. These notes serve as a valuable reference for similar projects in the future.

---

**Remember:** Backup configurations and volumes regularly to avoid repeating these steps!