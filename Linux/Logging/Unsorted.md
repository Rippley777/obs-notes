

---

## 1. Viewing UFW Logs

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

---

## 2. Viewing WireGuard Logs

WireGuard logs provide insights into VPN activity, such as handshake failures and connection states.

### Logs with `journalctl`

If WireGuard is managed by `wg-quick` and `systemd`, view logs with:
```bash
sudo journalctl -u wg-quick@<wg-interface> -f
```
Replace `<wg-interface>` with your interface name (e.g., `wg0`).

### Debugging Connection Issues

Increase verbosity for detailed logs:
1. Add the following to the `[Interface]` section of your WireGuard configuration file:
   ```
   [Interface]
   ...
   PostUp = wg show
   PostDown = wg show
   ````
2. Restart the service:
   ```bash
   sudo systemctl restart wg-quick@<wg-interface>
   ```

View logs again:
```bash
sudo journalctl -u wg-quick@<wg-interface>
```

---

## 3. Viewing Traefik Logs

Traefik logs include details about routing, certificate issues, and errors.

### Logs in Systemd

If Traefik runs as a systemd service:
```bash
sudo journalctl -u traefik -f
```

### Logs in Docker

If Traefik runs in a Docker container, view logs with:
```bash
docker logs -f <traefik-container-name>
```

Find the container name:
```bash
docker ps
```

### Customize Traefik Logging

To configure log levels, edit the Traefik configuration file (YAML or TOML):

#### YAML Example:
```yaml
log:
  level: DEBUG
  filePath: "/var/log/traefik.log"
```

#### TOML Example:
```toml
[log]
  level = "DEBUG"
  filePath = "/var/log/traefik.log"
```

Restart Traefik to apply changes:
```bash
sudo systemctl restart traefik
```

---

## General Tips for Viewing Logs

### Follow Logs in Real-Time

Use `-f` to follow logs as they are written:
```bash
tail -f /path/to/log/file
```

### Search Within Logs

Use `grep` to filter log entries:
```bash
grep "keyword" /path/to/log/file
```

### Rotate and Manage Logs

Ensure logs don’t grow too large by configuring log rotation:
1. Check `/etc/logrotate.d/` for relevant log files.
2. Customize rotation settings (e.g., size, frequency).

---

This guide ensures you can monitor and troubleshoot UFW, WireGuard, and Traefik effectively. Adjust verbosity and configurations based on your specific needs.
