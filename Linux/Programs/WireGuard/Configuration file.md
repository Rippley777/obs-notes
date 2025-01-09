### Where to Add the Configuration File

1. **On Linux**:
    
    - Save the configuration file in `/etc/wireguard/`.
    - For example, if your configuration file is named `wg0.conf`, its path would be `/etc/wireguard/wg0.conf`.
    - Use the `wg-quick` command to manage the interface:
        
        bash
        
        Copy code
        
        `sudo wg-quick up wg0 sudo wg-quick down wg0`
        
2. **On Other Operating Systems**:
    
    - For Windows, macOS, or mobile apps, use the WireGuard GUI. The configuration file can be imported directly into the application.
    - For the GUI, you’ll usually copy-paste the configuration details or select the file to import.
3. **For Docker Containers**:
    
    - Mount the configuration file into the container at the appropriate location. For example:
        
        bash
        
        Copy code
        
        `docker run --rm -v /path/to/wg0.conf:/etc/wireguard/wg0.conf my-wireguard-image`