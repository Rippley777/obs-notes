To turn on devices remotely for a better VNC/RDP experience, you can use Wake-on-LAN (WoL) technology. Here's how to set it up:

## Enable Wake-on-LAN

1. Configure BIOS settings:
    
    - Restart your computer and enter the BIOS setup.
    - Look for options like "Wake on LAN," "Wake from PCIe," or "Resume By PCI-E Device"[4](https://www.pcmag.com/how-to/turn-on-computer-from-across-the-house-with-wake-on-lan).
    - Enable these options to allow network-based wake-up.
    
2. Enable WoL in Windows:
    
    - Open Device Manager.
    - Expand "Network Adapters" and right-click your Ethernet adapter.
    - In Properties, go to the Advanced tab.
    - Enable "Wake on Magic Packet" if available[4](https://www.pcmag.com/how-to/turn-on-computer-from-across-the-house-with-wake-on-lan).
    
3. Configure power settings:
    
    - Open Control Panel > Hardware and Sound > Power Options.
    - Click "Change plan settings" > "Change advanced power settings".
    - Ensure PCI Express power settings are set to "Off"[2](https://www.reddit.com/r/HomeNetworking/comments/196i3w9/my_guide_to_wake_on_lan/).
    

## Using Wake-on-LAN

Once configured, you can wake up your devices using:

4. Dedicated WoL software:
    
    - Use tools like WakeMeOnLan.
    - Scan for devices on your network.
    - Select the target device and choose "Wake Up Selected Computers"[8](https://www.windowscentral.com/how-enable-and-use-wake-lan-wol-windows-10).
    
5. Mobile apps or custom solutions:
    
    - Some users create custom setups using devices like ESP8266 and Telegram bots for remote wake-up[2](https://www.reddit.com/r/HomeNetworking/comments/196i3w9/my_guide_to_wake_on_lan/).
    

By implementing Wake-on-LAN, you can remotely power on your devices before initiating VNC or RDP sessions, ensuring they're always accessible when needed.