
`systemctl` is a command-line tool used to interact with and control the `systemd` init system and service manager. It is used to manage services, units, and the system's overall state on modern Linux distributions.

## Key Concepts

### What is `systemd`?
- `systemd` is a system and service manager for Linux, designed to provide better boot performance and easier service management.
- It uses units to represent and manage system resources like services, mounts, devices, etc.

### Units in `systemd`
- **Service Units (`.service`)**: Represent services or daemons (e.g., `nginx.service`).
- **Socket Units (`.socket`)**: Represent inter-process communication sockets.
- **Target Units (`.target`)**: Group units for specific states (e.g., `multi-user.target`).
- **Mount Units (`.mount`)**: Represent mount points.
- **Timer Units (`.timer`)**: Schedule tasks (like cron jobs).

## Common Commands

### Managing Services

#### Start a Service:
```bash
sudo systemctl start <service_name>
```
Example:
```bash
sudo systemctl start nginx
```

#### Stop a Service:
```bash
sudo systemctl stop <service_name>
```

#### Restart a Service:
```bash
sudo systemctl restart <service_name>
```

#### Reload Service Configuration (without restarting):
```bash
sudo systemctl reload <service_name>
```

#### Enable a Service (start at boot):
```bash
sudo systemctl enable <service_name>
```

#### Disable a Service (prevent it from starting at boot):
```bash
sudo systemctl disable <service_name>
```

#### Check Service Status:
```bash
systemctl status <service_name>
```
Example Output:
```
● nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
     Active: active (running) since Thu 2025-01-06 12:34:56 UTC; 10min ago
```

### Analyzing the System State

#### List All Units:
```bash
systemctl list-units
```

#### List Only Active Units:
```bash
systemctl list-units --type=service
```

#### Check the Status of All Services:
```bash
systemctl list-units --type=service --all
```

#### Get Detailed Unit Information:
```bash
systemctl show <unit_name>
```

### Managing Targets (Runlevels)

#### View Current Target:
```bash
systemctl get-default
```

#### Change Target:
```bash
sudo systemctl set-default <target_name>
```
Example:
```bash
sudo systemctl set-default multi-user.target
```

#### Switch to a Target Immediately:
```bash
sudo systemctl isolate <target_name>
```

### Logs and Diagnostics

#### View Logs for a Service:
```bash
journalctl -u <service_name>
```

#### View Logs Since Boot:
```bash
journalctl -b
```

#### View Real-Time Logs:
```bash
journalctl -f
```

### Creating Custom Units

1. **Create a Unit File:**
   ```bash
   sudo nano /etc/systemd/system/<custom_unit>.service
   ```

   Example:
   ```ini
   [Unit]
   Description=My Custom Service
   After=network.target

   [Service]
   ExecStart=/usr/bin/my_custom_script.sh
   Restart=always

   [Install]
   WantedBy=multi-user.target
   ```

2. **Reload Systemd Configuration:**
   ```bash
   sudo systemctl daemon-reload
   ```

3. **Enable and Start the Unit:**
   ```bash
   sudo systemctl enable <custom_unit>
   sudo systemctl start <custom_unit>
   ```

4. **Verify the Status:**
   ```bash
   systemctl status <custom_unit>
   ```

## Advanced Usage

### Masking and Unmasking Services
- **Mask a Service (prevent it from being started):**
  ```bash
  sudo systemctl mask <service_name>
  ```

- **Unmask a Service:**
  ```bash
  sudo systemctl unmask <service_name>
  ```

### Checking Dependencies
- **Show Unit Dependencies:**
  ```bash
  systemctl list-dependencies <unit_name>
  ```

- **Reverse Dependencies:**
  ```bash
  systemctl list-dependencies --reverse <unit_name>
  ```

### Debugging
- **Start a Service in Debug Mode:**
  ```bash
  sudo SYSTEMD_LOG_LEVEL=debug systemctl start <service_name>
  ```

- **Analyze Boot Performance:**
  ```bash
  systemd-analyze
  ```

- **View Critical Chain:**
  ```bash
  systemd-analyze critical-chain
  ```

## Tips and Best Practices
- Always check the status of services after starting, stopping, or restarting them.
- Use `journalctl` for detailed logs when diagnosing issues.
- Use `daemon-reload` whenever you make changes to unit files.
- Avoid editing unit files in `/lib/systemd/system/`; use `/etc/systemd/system/` instead for custom configurations.
- Remember to enable services if you want them to start at boot.

## Resources
- Official Documentation: [https://www.freedesktop.org/wiki/Software/systemd/](https://www.freedesktop.org/wiki/Software/systemd/)
- `man systemctl`: Detailed information about all `systemctl` commands.
