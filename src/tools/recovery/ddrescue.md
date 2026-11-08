# ddrescue: copy a failing disk

**Package:** `ddrescue` (GNU ddrescue) · **Writes to disks:** only to the output you name

Copies a disk or partition to an image file (or another disk), reading the
easy parts first and coming back to the bad areas later. The **map file**
records what has been copied, so a copy can be stopped and resumed.

```sh
# 1. First pass: copy everything that reads easily, skip the bad areas
sudo ddrescue -n /dev/sdX /mnt/target/disk.img /mnt/target/disk.map

# 2. Second pass: go back to the bad areas, 3 retries, direct disk access
sudo ddrescue -d -r3 /dev/sdX /mnt/target/disk.img /mnt/target/disk.map

# Copy to another disk instead of a file (-f is needed to write to a device)
sudo ddrescue -f -n /dev/sdX /dev/sdY /mnt/target/disk.map
```

- `-n`: no scraping; leaves the slowest, worst areas for later.
- `-d`: reads the source directly, bypassing the kernel cache.
- `-r3`: retries bad sectors three times.

The target must be **at least as big** as the source, on a different, healthy
disk, mounted read-write on purpose. Keep the map file next to the image:
rerunning the same command continues where it stopped.

> **Writes:** to the output. Double-check the order: source first, then the
> image or target disk. Swapping them overwrites the disk you are rescuing.
