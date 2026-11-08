# Btrfs: check and restore

**Package:** `btrfs-progs` · **Writes to disks:** `btrfs restore` only to the target folder

```sh
sudo btrfs filesystem show                         # Btrfs file systems and their devices
sudo btrfs check --readonly /dev/sdX1              # check without changing anything
sudo btrfs restore -v /dev/sdX1 /mnt/target/out    # copy files off a damaged, unmountable Btrfs
sudo mount -o ro,rescue=usebackuproot /dev/sdX1 /mnt   # try an older tree root, read-only
```

`btrfs restore` reads the file system directly and writes the files it can
reach into a folder on **another** disk.

> **Writes:** `btrfs check --repair` exists but can make things worse; the
> Btrfs developers advise it only as a last resort. Prefer `restore`.
