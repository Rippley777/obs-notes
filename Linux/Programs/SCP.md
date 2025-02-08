### Using SCP on Linux or macOS

1. **Open your terminal.**
    
2. **Use the `scp` command with the `-r` option to recursively copy directories.**
    


```bash
scp -r /path/to/local/directory pi@raspberrypi.local:/path/to/destination/

```

1. - Replace `/path/to/local/directory` with the path of the directory on your local machine that you want to copy.
    - Replace `pi@raspberrypi.local` with the username and hostname or IP address of your Raspberry Pi. The default username is usually `pi`, and `raspberrypi.local` can be replaced with the Pi's IP address if `.local` doesn't resolve.
    - Replace `/path/to/destination/` with the path on your Raspberry Pi where you want to copy the directory.
2. **Enter your Raspberry Pi's password when prompted.**
    

### Using SCP on Windows

If you are using Windows and prefer a graphical interface, you can use **WinSCP**:

1. **Download and install WinSCP** from [https://winscp.net/](https://winscp.net/).
    
2. **Launch WinSCP** and in the session setup:
    
    - **File Protocol**: Choose SCP.
    - **Host name**: Enter your Raspberry Pi's IP address.
    - **Port number**: Typically, this is 22 for SSH.
    - **User name**: `pi` (or your Raspberry Pi's username).
    - **Password**: Input your Raspberry Pi's password.
3. **Once connected, you can drag and drop folders** from your Windows machine to your Raspberry Pi using the WinSCP interface.
    

### Troubleshooting

- **Connection Issues**: Make sure your Raspberry Pi is on the same network as your computer. Check the IP address and SSH configuration on your Pi.
- **Permission Issues**: If you encounter permissions errors, ensure that your user on the Raspberry Pi has the appropriate write permissions for the destination directory.
- **SSH Not Enabled**: If SSH is not enabled on your Raspberry Pi, you can enable it by placing a file named `ssh` (without any extension) onto the boot partition of the SD card from another computer.

Using `scp` is a straightforward way to transfer files and directories to your Raspberry Pi over your network securely.
