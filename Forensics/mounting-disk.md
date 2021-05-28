# Mounting disks

***DO NOT ATTACH THE DISK UNTIL SETUP IS DONE***
## Setup
Before we start mounting disks we need to make sure we don't contaminate any data.
To do this we need to make sure our os doesn't mount disk automatically by disabling udisks2.
```bash
systemctl stop udisks2.service
systemctl mask udisks2.service
```

After we've done this it'd be recommended to monitor udevadm so we can keep track of what's happening in the next steps
```bash
udevadm monitor
```
## Attaching the disk

First of all, you can attach the disk to your device now. As we disabled udisks2 it shouldn't be discovered by your os. Now we can tell our os to rescan the SCSI bus.
1. First of all we need to switch to a root terminal as sudo doesn't work 100% of the time
2. Next we can rescan our busses. While doing so watch you `udevadm monitor` once you see the disk attaching you don't have to continue scanning the other hosts.
```bash
echo "- - -" > /sys/class/scsi_host/host0/scan
echo "- - -" > /sys/class/scsi_host/host1/scan
echo "- - -" > /sys/class/scsi_host/host2/scan
```

## Backing up the disk

First of all let's make a md5 checksum so we can prove nothing changed to the disk.
```bash
md5sum /dev/sdb > disk-checksum
```
next we are going to make a image of the disk using `dd`
```bash
dd if=/dev/sdb of=sdb-backup.img status=progress
```
Now we create a checksum of the backup file and compare it to the original
```bash
md5sum sdb-backup.img >> disk-checksum
md5sum -c disk-checksum
```
Both should be `OK`

## Mounting the disk

> It is recommended to not do your forensics analisis on the actual disk. That's why you should backup the disk and work on that disk instead.

#### Mounting an actual disk

To mount the disk you first look at what partitions are on the disk using `lsblk` 
You should see something similar to
```bash
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda      8:0    0   40G  0 disk 
├─sda1   8:1    0   39G  0 part /
├─sda2   8:2    0    1K  0 part 
└─sda5   8:5    0  975M  0 part [SWAP]
sdb      8:16   0   60G  0 disk 
└─sdb1   8:17   0   60G  0 part
```
In this case `sdb` is the disk we just attached and `sdb1` is the partition on the disk. This is what we mount.
Mounting is done with the following command
```bash
mount /dev/sdb1 /mnt/<point to mount to>
```
After doing so we should could run `lsblk` again to confirm the partition is mounted
```bash
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda      8:0    0   40G  0 disk 
├─sda1   8:1    0   39G  0 part /
├─sda2   8:2    0    1K  0 part 
└─sda5   8:5    0  975M  0 part [SWAP]
sdb      8:16   0   60G  0 disk 
└─sdb1   8:17   0   60G  0 part /mnt/suspectdisk
```

#### Mounting a backed up disk

First do a losetup of the img
```bash
losetup -fPr sdb-backup.img--show
```
This will create a loop device
Once this one is created. We can mount the loop device
```bash
mount /dev/loop0 /mnt/<point to mount to>
```

*Remember when mounting a disk make sure if there are partitions you specify what partition to mount*