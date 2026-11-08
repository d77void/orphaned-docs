# fdisk: list partitions

**Package:** `util-linux` · **Writes to disks:** only after `w` in interactive mode

```sh
sudo fdisk -l                # every disk with its partitions, sizes and types
sudo fdisk -l /dev/sdX       # one disk
sudo fdisk -x /dev/sdX       # more detail
```

`fdisk /dev/sdX` (without `-l`) opens the interactive editor. Changes stay in
memory until `w`; `q` quits without writing.
