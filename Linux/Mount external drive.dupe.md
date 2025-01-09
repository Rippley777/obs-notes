
####  Identify drive
	`lsblk` or `sudo fdisk -l`

#### Create Mount Point
`sudo mkdir -p /mnt/external`

#### **Mount the Drive**

`sudo mount /dev/sdX1 /mnt/external`

#### Check mount
``
`df -h`
``

#### Access Drive
`cd /mnt/external`

#### Unmount Drive
`sudo umount /mnt/external`



If you want the drive to mount automatically, edit the `/etc/fstab` file:

1. Find the drive's UUID:
2. `blkid`

Edit `/etc/fstab`
	`sudo nano /etc/fstab`