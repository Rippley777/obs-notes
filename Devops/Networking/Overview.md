### Networking: The Core Concepts

Networking is about how devices communicate over shared mediums (like wires, Wi-Fi, or fiber optics) by breaking down communication into **layers**, each responsible for a specific aspect of the process. It’s the ultimate **system of systems**, and understanding it well starts with the **OSI Model** or its more practical sibling, the **TCP/IP Model**.

---

### 1. **IP Addresses: Logical Locators**

- **IPv4** (e.g., `192.168.1.100`) and **IPv6** (e.g., `fe80::1`) are like digital mailing addresses for your devices.
- IP addresses are hierarchical: they help route packets between **networks** and **devices within networks**.
- On local networks, IP addresses are typically private (e.g., `192.168.x.x`), with the router acting as the gateway to the outside (public internet).

> **DHCP** dynamically assigns IPs. If you allocate a "static IP," you’re essentially reserving a slot for that device, ensuring consistency.

---

### 2. **Hostnames: Human-Friendly Identifiers**

- Devices have hostnames because no one remembers IPs unless they’re Rain Man.
- **DNS (Domain Name System)** translates hostnames (like `mycoolpi.local`) to IPs, much like a phonebook. On your local network, this might involve **mDNS**, **NetBIOS**, or even your router's DHCP settings.
- If your router assigned a new hostname, it might be because:
    1. The Pi sent no hostname in its DHCP request.
    2. The router treated it as a "new" device due to a different MAC address.

---

### 3. **Data Movement: Packet Routing and Switching**

- Data flows as **packets**, tiny chunks of information wrapped in metadata:
    - **IP Headers:** Tell routers where the packet should go.
    - **TCP/UDP Headers:** Define how to deliver the packet to the correct app.
- **Routers** use forwarding tables to decide the best path for each packet.
- On a local network, the router doubles as a **default gateway**, forwarding packets it doesn’t recognize to the broader internet.

---

### 4. **Protocols: The Languages of Networking**

- **TCP:** Reliable, ensures packets arrive in order and without errors (used for web pages, file downloads).
- **UDP:** Fast and doesn’t care about order or errors (used for gaming, video streaming).
- **ARP (Address Resolution Protocol):** Maps IP addresses to MAC addresses on your local network.

---

### 5. **Network Address Translation (NAT): Sharing a Single IP**

- Your router performs **NAT** to allow multiple devices to share a single public IP address. When packets leave your network, the router rewrites them to appear as though they come from its public IP, keeping track of which internal device sent what.

---

### 6. **Routing vs. Switching:**

- **Switches** work at Layer 2 (Data Link) to connect devices within the same network using MAC addresses.
- **Routers** operate at Layer 3 (Network) to forward packets between different networks, using IP addresses and routing tables.

---

### 7. **Your Issue: Dynamic Hostname or DHCP Quirks**

- If your router gave your Raspberry Pi a new hostname, it’s likely tied to:
    1. **DHCP Behavior:** The Pi may not have sent its custom hostname during the DHCP handshake, leading the router to generate one.
    2. **Device Cache:** The router’s DHCP lease table might have expired or treated the Pi as a new device.
    3. **MAC Address Changes:** If the Pi’s network interface was reconfigured, the router sees it as a different device.
- Fix by setting both a **static hostname** on the Pi and a **reserved IP address** in the router’s DHCP settings.

---

### 8. **Why Networking Is Hard**

- It’s a complex, emergent system: Layers interact, devices behave differently, and routers can be inconsistent.
- Tools like Wireshark and logs help debug issues, but often it’s trial and error because every network is unique.