

## Prerequisites
Ensure your system is up to date and has the necessary dependencies installed.

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install wget unzip -y
```

## Download BzMiner
Visit the official BzMiner website or GitHub page to find the latest release. Replace `<version>` with the latest available version.

```bash
wget https://www.bzminer.com/downloads/bzminer_v<version>_linux.zip -O bzminer.zip
```

## Extract the Archive

```bash
unzip bzminer.zip -d bzminer
cd bzminer
```

## Set Executable Permissions

```bash
chmod +x bzminer
```

## Run BzMiner

You can start BzMiner with the following command:

```bash
./bzminer -h
```

To mine using a specific pool and wallet address, modify the command accordingly:

```bash
./bzminer -a ethash -o stratum+tcp://pool.example.com:4444 -u YourWalletAddress -p x
```

## Optional: Create a Systemd Service

To run BzMiner as a service:

1. Create a systemd service file:

   ```bash
   sudo nano /etc/systemd/system/bzminer.service
   ```

2. Add the following content:

   ```ini
   [Unit]
   Description=BzMiner Service
   After=network.target

   [Service]
   ExecStart=/path/to/bzminer -a ethash -o stratum+tcp://pool.example.com:4444 -u YourWalletAddress -p x
   Restart=always
   User=youruser
   Group=yourgroup
   WorkingDirectory=/path/to/bzminer

   [Install]
   WantedBy=multi-user.target
   ```

3. Reload systemd and start the service:

   ```bash
   sudo systemctl daemon-reload
   sudo systemctl enable bzminer
   sudo systemctl start bzminer
   ```

4. Check the service status:

   ```bash
   sudo systemctl status bzminer
   ```

## Troubleshooting

- If BzMiner fails to start, ensure your system has the correct drivers for your GPU.
- Check logs for errors:
  
  ```bash
  journalctl -u bzminer --no-pager -n 50
  
