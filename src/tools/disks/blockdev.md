# blockdev: read-only flag and device size

**Package:** `util-linux` · **Writes to disks:** no

```sh
sudo blockdev --report                # every block device: read-only flag, size, sector size
sudo blockdev --setro /dev/sdX        # make the kernel refuse writes to the disk
sudo blockdev --setro /dev/sdX1       # … and to each partition you will use
sudo blockdev --getro /dev/sdX1       # 1 = read-only
sudo blockdev --getsize64 /dev/sdX    # size in bytes
```

Set disks read-only **before** mounting or examining them. The flag lasts
until the device is removed or the computer restarts. See
[Working safely with disks](../../disks/index.md).
