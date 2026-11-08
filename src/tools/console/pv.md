# pv and mbuffer: progress in pipes

**Packages:** `pv`, `mbuffer`

```sh
pv disk.img | zstd -T0 > disk.img.zst          # compress with a progress bar
sudo pv /dev/sdX > /mnt/target/disk.img        # copy a (healthy) disk with progress
pv -p disk.img | ssh user@host 'cat > disk.img'   # send over SSH with progress
```

For failing disks, use [ddrescue](../recovery/ddrescue.md) instead.
`mbuffer` smooths transfers between slow and fast ends (tape, network).
