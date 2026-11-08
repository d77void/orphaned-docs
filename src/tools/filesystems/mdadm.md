# mdadm: software RAID

**Package:** `mdadm` · **Writes to disks:** assembling read-write does

d77orphaned never assembles RAID arrays on its own. mdadm also reads the
Intel Rapid Storage (IMSM) RAID sets that many desktops use.

```sh
cat /proc/mdstat                                # arrays the kernel knows about
sudo mdadm --examine /dev/sdX1                  # RAID metadata on one member
sudo mdadm --examine --scan                     # arrays found on all disks
sudo mdadm --assemble --readonly /dev/md0 /dev/sdX1 /dev/sdY1   # assemble read-only
sudo mdadm --detail /dev/md0                    # state of an assembled array
sudo mdadm --stop /dev/md0
```

> Not verified yet in d77orphaned: read-only assembly. When the data
> matters, image each member disk first and assemble the images (through
> [losetup](../disks/losetup.md)).
