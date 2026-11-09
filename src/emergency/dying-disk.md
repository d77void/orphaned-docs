# The disk is dying

**Writes to the disk:** none to the failing disk. All writes go to the healthy disk
you choose.

Signs: read errors, a system suddenly slow or freezing, files that vanish, SMART
warnings, clicks. **Copy first, diagnose later.** Every hour running can be one of
the last, so do not run long tests, `fsck`, or defragmentation.

## 1. You need another disk

At least as big as the failing disk, and healthy. Mount it, read-write on purpose:

```sh
lsblk -d -o NAME,SIZE,MODEL,SERIAL,TRAN      # identify both disks
sudo mount /dev/sdYn /mnt/target
```

## 2. A quick look, without stressing it

```sh
sudo smartctl -H -A /dev/sdX                 # verdict and attributes
sudo smartctl -l error /dev/sdX              # the errors it remembers
```

A failed verdict confirms it. A passed verdict does **not** clear it: drives often
fail without warning. Do not start a long self-test on a disk you suspect.
See [smartctl](../tools/disks/smartctl.md), or [nvme](../tools/disks/nvme.md).

## 3. Copy it

```sh
# First pass: what reads easily, leaving the bad areas for later
sudo ddrescue -n /dev/sdX /mnt/target/disk.img /mnt/target/disk.map

# Second pass: back to the bad areas, 3 retries
sudo ddrescue -d -r3 /dev/sdX /mnt/target/disk.img /mnt/target/disk.map
```

**Source first, then the image.** Swapping them overwrites the disk you are saving.
Keep the map file: if the disk disappears or the power goes, the same command
carries on from where it stopped. If the disk drops off, power it off for a while,
then resume. See [ddrescue](../tools/recovery/ddrescue.md).

To see how much was lost:

```sh
ddrescuelog -t /mnt/target/disk.map
```

## 4. Get the files from the image

From here on, work only on the image, and leave the failing disk alone.

```sh
sudo losetup -rPf --show /mnt/target/disk.img     # prints /dev/loopN; -r: read only
sudo mount -o ro,noload /dev/loopNp1 /mnt/rescue  # ext4; for XFS: ro,norecovery
```

If a file system does not mount, work on a **second copy** of the image with
[fsck or TestDisk](../tools/filesystems/index.md); [photorec](../tools/recovery/photorec.md)
recovers files by their contents when nothing else does.

## Encrypted disks

Copy the whole disk the same way. Then open the image: the same
`cryptsetup open /dev/loopNpM cr`. Bad sectors in a LUKS header can make the whole
volume unreadable, which is why [a header backup](../tools/filesystems/cryptsetup.md)
is worth having beforehand.

> Tested in a virtual machine: a disk with 64 unreadable sectors simulated with
> device-mapper. Both passes completed, the map recorded the bad area, and the
> image mounted read-only with the files identical. Not tested on a disk really
> failing, where reads can hang and the disk can disappear.
