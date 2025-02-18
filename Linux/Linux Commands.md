
-find all logs on system
find / -type f -name "*.log" 2>/dev/null | wc -l

-get installed pkgs
dpkg -l | grep '^ii' | wc -l

xxd

bindwalk -Me  recursive 

cut
cat /etc/passwd | grep -v "false\|nologin" | cut -d":" -f1


cat /etc/passwd | grep -v "false\|nologin"

replace text
cat /etc/passwd | grep -v "false\|nologin" | tr ":" " "

column 
cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | column -t

awk (select specific)
cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}'

sed
cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}' | sed 's/bin/HTB/g'


word count
 cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}' | wc -l


services running
systemctl list-units --type=service --state=running

list listening
ss -ltn | wc -l

check user running service
ps -eo user,comm | grep proftpd

Curl

//[[Retrieve source code]]



## Mount APFS Partition (Read-Only)
Install APFS Tools:
`sudo apt install apfsprogs libfsapfs-utils`

List APFS Volumes:
`sudo fsapfsmount -o ro /dev/sdX /mnt/apfs`

Inspect Partition for Errors
`sudo fsapfsinfo /mnt/apfs`

Linux has limited repair capabilities for APFS. If errors appear:
`sudo fsck.apfs /dev/sdX`


**Hex Dump Partition:**
`sudo xxd /dev/sdX | less`

Forensic Clone:
`sudo dd if=/dev/sdX of=/mnt/external/mac_partition.img bs=4M status=progress`



## Automated backups
Automate Backups with `rsync`
`sudo rsync -av --exclude={"/mnt/*","/proc/*","/sys/*","/dev/*","/tmp/*","/run/*","/lost+found"} / /mnt/kali_backup`

**Schedule Backups**:  
Add this to `cron` to run every Sunday at 3 AM

```bash
sudo crontab -e

0 3 * * 7 rsync -av --delete --exclude={"/mnt/*","/proc/*","/sys/*","/dev/*","/tmp/*","/run/*","/lost+found"} / /mnt/kali_backup

```

### Encrypted backups
Install LUKS :
`sudo apt install cryptsetup`

Encrypt the Partition
`sudo cryptsetup luksFormat /dev/nvme0n1p2`

Open and format:
`sudo cryptsetup luksOpen /dev/nvme0n1p2 backup sudo mkfs.ext4 /dev/mapper/backup`

Mount:
```bash
sudo mkdir /mnt/secure_backup
sudo mount /dev/mapper/kali_backup /mnt/secure_backup

```

Backup:
`sudo rsync -av --exclude={"/mnt/*","/proc/*","/sys/*","/dev/*","/tmp/*","/run/*","/lost+found"} / /mnt/secure_backup`

Lock it down:
```bash
sudo umount /mnt/secure_backup
sudo cryptsetup luksClose kali_backup
```
**Pro Tip:**  
Store the encryption key on a USB or safe place. Dont forget the password you created on step 2