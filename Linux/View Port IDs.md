### **1. Using `netstat`**

The `netstat` command displays network connections, routing tables, and port usage.

1. Install `net-tools` if `netstat` is not available:
    `sudo apt install net-tools    # Debian/Ubuntu sudo yum install net-tools    # CentOS/RHEL sudo pacman -S net-tools      # Arch`
    
2. List processes and their associated ports:
    
    `sudo netstat -tulnp`
    
    - `-t`: Show TCP connections.
    - `-u`: Show UDP connections.
    - `-l`: Show listening ports.
    - `-n`: Display numerical addresses (skip DNS resolution).
    - `-p`: Show the process name and PID.

Example output:

`Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      1234/nginx`

---

### **2. Using `ss`**

The `ss` command is a modern alternative to `netstat` and is usually pre-installed on most Linux distributions.

1. Display all listening and established ports with their processes:
    
    `sudo ss -tulnp`
    
    Example output:
    
    `Netid  State   Recv-Q  Send-Q  Local Address:Port   Peer Address:Port   Process tcp    LISTEN  0       128     0.0.0.0:22          0.0.0.0:*           users:(("sshd",pid=1234,fd=3))`
    

---

### **3. Using `lsof`**

The `lsof` command lists open files, including network sockets.

1. List processes using specific ports:
    `sudo lsof -i -P -n`
    
    - `-i`: List network files.
    - `-P`: Show port numbers (no service name resolution).
    - `-n`: Do not resolve hostnames.
2. Filter by specific ports or protocols:
    
    `sudo lsof -iTCP -sTCP:LISTEN`
    

Example output:

`COMMAND  PID  USER   FD   TYPE  DEVICE SIZE/OFF NODE NAME sshd     1234 root    3u  IPv4  123456      0t0  TCP *:22 (LISTEN)`

---

### **4. Using `ps` Combined with `grep`**

If you know the process name and want to find the port it uses:

1. Get the PID of the process:
    
    `ps aux | grep <process_name>`
    
2. Use `netstat` or `lsof` to find the port:
    
    `sudo netstat -tulnp | grep <PID> sudo lsof -i | grep <PID>`
    

---

### **5. Using `fuser`**

The `fuser` command identifies which process is using a specific port.

1. Install `fuser` if needed:
    
    `sudo apt install psmisc    # Debian/Ubuntu`
    
2. Find the process using a port:
    
    `sudo fuser -n tcp 80`
    

---

### **6. Using `pidstat` (Advanced Analysis)**

For detailed monitoring of process and port usage, you can use `pidstat` if installed:

`pidstat -p ALL`

### **Example to See Port 8080**

If you specifically want to check which process is using port `8080`:
`sudo lsof -i :8080`

Example output:

`COMMAND  PID  USER   FD   TYPE  DEVICE SIZE/OFF NODE NAME nginx    5678 root    6u  IPv4  123457      0t0  TCP *:8080 (LISTEN)`