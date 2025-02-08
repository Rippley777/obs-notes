

## Viewing UFW Logs

UFW logs provide information about firewall activity, such as blocked or allowed connections.

### Enable UFW Logging

If logging is not enabled, turn it on:
```bash
sudo ufw logging on
```

Logging levels available:
- `low`: Minimal information.
- `medium`: Recommended for most users (default).
- `high`: Most verbose.

Set the desired logging level:
```bash
sudo ufw logging medium
```

### View UFW Logs in Real-Time

Logs are stored in `/var/log/ufw.log`. To view them live:
```bash
sudo tail -f /var/log/ufw.log
```

### View Historical UFW Logs

Use `less` or `grep` to examine past logs:
```bash
sudo less /var/log/ufw.log
```

Filter logs for specific entries (e.g., `BLOCK`):
```bash
grep BLOCK /var/log/ufw.log
```

### Reading Logs

### Ex 1:

`Jan 13 07:35:10 exo kernel: [ 2235.495193] [UFW BLOCK] IN=br-4ee3e112b251 OUT=br-4ee3e112b251 PHYSIN=veth3d41a08 PHYSOUT=veth3302b95 MAC=33:33:00:00:00:16:7a:7f:34:6e:5c:b1:86:dd SRC=0000:0000:0000:0000:0000:0000:0000:0000 DST=ff02:0000:0000:0000:0000:0000:0000:0016 LEN=96 TC=0 HOPLIMIT=1 FLOWLBL=0 PROTO=ICMPv6 TYPE=143 CODE=0 MARK=0xd4`

1. **Date and Time**:  
    `Jan 13 07:35:10` - The date and time when the log was recorded.
    
2. **Hostname**:  
    `exo` - The hostname of the system that logged this packet.
    
3. **Kernel Info**:  
    `[ 2235.495193]` - Kernel timestamp indicating system uptime when the log was generated.
    
4. **Action**:  
    `[UFW BLOCK]` - Indicates the packet was blocked by UFW.
    
5. **Network Interfaces**:
    
    - `IN=br-4ee3e112b251` - The bridge interface where the packet entered.
    - `OUT=br-4ee3e112b251` - The bridge interface where the packet was supposed to leave.
    - `PHYSIN=veth3d41a08` - Physical input interface (a virtual Ethernet interface, likely a container or VM).
    - `PHYSOUT=veth3302b95` - Physical output interface.
6. **MAC Address**:  
    `MAC=33:33:00:00:00:16:7a:7f:34:6e:5c:b1` - MAC addresses of source and destination.
    
7. **Source (SRC) and Destination (DST)**:
    
    - `SRC=0000:0000:0000:0000:0000:0000:0000:0000` - Source IPv6 address.
    - `DST=ff02:0000:0000:0000:0000:0000:0000:0016` - Destination IPv6 multicast address.
8. **Packet Details**:
    
    - `LEN=96` - Length of the packet in bytes.
    - `PROTO=ICMPv6` - Protocol (IPv6 ICMP in this case).
    - `TYPE=143` and `CODE=0` - ICMPv6 message type and code.





### Ex 2: 
```
`Jan 13 07:35:27 exo kernel: [ 2251.950787] [UFW BLOCK] IN=eth0 OUT= MAC=dc:a6:32:9c:a7:d4:f6:e8:06:60:46:63:08:00 SRC=192.168.1.209 DST=192.168.1.227 LEN=52 TOS=0x00 PREC=0x00 TTL=64 ID=0 DF PROTO=TCP SPT=51804 DPT=8080 WINDOW=2049 RES=0x00 ACK FIN URGP=0`
```

- **Interfaces**:
    
    - `IN=eth0` - The physical Ethernet interface where the packet entered.
    - `OUT=` - No outgoing interface specified, indicating the packet was blocked before being routed.
- **MAC Address**:  
    `MAC=dc:a6:32:9c:a7:d4:f6:e8:06:60:46:63:08:00` - MAC addresses of source and destination.
    
- **Source and Destination**:
    
    - `SRC=192.168.1.209` - Source IP address.
    - `DST=192.168.1.227` - Destination IP address.
- **Packet Details**:
    
    - `LEN=52` - Packet size in bytes.
    - `PROTO=TCP` - Transmission Control Protocol.
    - `SPT=51804` - Source port (likely random/high port).
    - `DPT=8080` - Destination port (usually an HTTP proxy or web service).
- **TCP Flags**:
    
    - `ACK FIN` - The packet has both `ACK` (acknowledgment) and `FIN` (finish) flags set, indicating the end of a TCP connection.

### Ex 3: 


```
Jan 13 07:35:30 exo kernel: [ 2255.120161] [UFW BLOCK] IN=eth0 OUT= MAC=dc:a6:32:9c:a7:d4:58:07:f8:43:cf:52:08:00 SRC=185.42.12.84 DST=192.168.1.227 LEN=40 TOS=0x00 PREC=0x00 TTL=238 ID=42841 PROTO=TCP SPT=58981 DPT=2016 WINDOW=1024 RES=0x00 SYN URGP=0
```
- **Source**:  
    `SRC=185.42.12.84` - The source IP address is external, indicating this could be a scanning or connection attempt.
    
- **Destination**:  
    `DST=192.168.1.227` - Destination is your local machine.
    
- **Packet Details**:
    
    - `PROTO=TCP` - TCP protocol.
    - `SPT=58981` - Source port.
    - `DPT=2016` - Destination port.
    - `SYN` - This is a connection initiation attempt (SYN packet).


### Key Points:

- **ICMPv6**: Multicast traffic (`DST=ff02::16`) is normal but can be blocked if not needed.
- **TCP Traffic**: Look out for external source IPs (`SRC`), especially if they target unusual ports like `2016`.
- **Local Traffic**: Internal blocked packets (`SRC` and `DST` within the local network) might indicate misconfigured services or over-restrictive rules.

---

### Recommendations:

1. **Evaluate Rules**:
    - If certain multicast traffic or TCP traffic is legitimate, adjust UFW rules to allow it.
2. **Investigate External Traffic**:
    - Research the source IP (`185.42.12.84`) to determine if it's malicious.
3. **Monitor Repeated Patterns**:
    - Repeated blocks on specific ports might indicate a brute force or scanning attempt.
4. **Harden UFW**:
    - Allow only necessary ports and protocols. For example:
        
        `sudo ufw allow 22/tcp  # SSH sudo ufw allow 51280/udp  # WireGuard`