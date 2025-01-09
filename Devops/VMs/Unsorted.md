#### **2. Monitor Network Traffic**

Inspect real-time network connections to identify unusual traffic:

`sudo netstat -tulnp sudo iftop`

#### **3. Review Logs**

Check logs for abnormal activity:

`sudo cat /var/log/auth.log | grep "Failed" sudo cat /var/log/auth.log | grep "Accepted" sudo tail -f /var/log/syslog`

#### **Verify Running Services**

Ensure no unauthorized services are running:

`sudo systemctl list-units --type=service`

#### **Scan for Malware**

Use `ClamAV` or a similar tool to scan for malicious files:

```
sudo apt install clamav
sudo freshclam
sudo clamscan -r /

```

Check for unexpected files:

`find / -type f -mtime -1`


#### **Analyze port Network Activity**

If this process is generating network activity, use:

`sudo netstat -tulnp | grep 3347`