# losetup: use an image file as a disk

**Package:** `util-linux` · **Writes to disks:** no, with `-r`

Turns a disk image (made with ddrescue or dd) into a device, so that the
usual tools can read its partitions.

```sh
sudo losetup -r -P -f --show disk.img   # read-only, with partitions; prints /dev/loopN
lsblk /dev/loop0                         # its partitions: /dev/loop0p1, …
sudo mount -o ro,noload /dev/loop0p1 /mnt
sudo umount /mnt
sudo losetup -d /dev/loop0               # detach
losetup -a                               # list loop devices in use
```

`-r` makes the loop device read-only, so nothing can change the image.
