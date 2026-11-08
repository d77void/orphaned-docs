# lsblk and blkid: list disks and file systems

**Package:** `util-linux` · **Writes to disks:** no

The first thing to run: which disks and partitions the computer has, how big
they are, what is on them and whether anything is mounted.

```sh
lsblk                          # disks, partitions, sizes, mount points
lsblk -f                       # with file system type, label and UUID
lsblk -d -o NAME,SIZE,MODEL,SERIAL,TRAN   # one line per disk: model, serial, USB/SATA/NVMe
lsblk -S                       # SCSI/SATA/USB disks with vendor and model
sudo blkid                     # every file system and its UUID, label and type
sudo blkid /dev/sdX1           # one partition
```

`lsblk` reads what the kernel already knows; `blkid` reads the start of each
partition to find its type. Neither changes anything.

Use the model, size and serial number (`lsblk -d -o …`) to be sure which disk
is which before running anything that writes.
