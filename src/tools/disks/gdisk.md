# gdisk and sgdisk: GPT partition tables

**Package:** `gptfdisk` · **Writes to disks:** yes, when told to

```sh
sudo gdisk -l /dev/sdX                 # list the partition table (read-only)
sudo sgdisk -p /dev/sdX                # the same, non-interactive
sudo sgdisk -i 1 /dev/sdX              # details of partition 1 (type GUID, unique GUID, name)
sudo sgdisk -b gpt-sdX.bin /dev/sdX    # save the GPT to a file (backup)
```

Keep a backup of the table (`-b`) before trying any repair. `sgdisk -l
<file>` loads it back; that one writes.

`gdisk` without `-l` is interactive: nothing is written until you type `w`,
and `q` quits without saving. Its recovery menu (`r`) can rebuild a damaged
GPT from the backup copy at the end of the disk.
