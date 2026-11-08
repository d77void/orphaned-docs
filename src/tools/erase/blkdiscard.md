# blkdiscard: quick discard on SSDs

**Package:** `util-linux` · **Writes to disks:** yes

Tells an SSD that all its blocks are free, which is very fast, but it is **not a
guaranteed erasure**: use it to prepare a drive for reuse, not for sensitive data.

```sh
sudo blkdiscard /dev/sdX            # discard everything
sudo blkdiscard --secure /dev/sdX   # secure discard, if the drive supports it
sudo blkdiscard --zeroout /dev/sdX  # write zeros instead of discarding
```
