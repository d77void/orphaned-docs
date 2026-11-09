# clamav: scanning for malware

**Install:** `sudo xbps-install -S clamav` ([about installing](index.md)) · **Writes
to disks:** not unless you ask it to move or remove files

Scans files for known malware, such as a Windows disk you are recovering files from.

```sh
sudo freshclam                                   # download the signatures, first
sudo mkdir -p /mnt/win
sudo mount -o ro,noload /dev/sdXn /mnt/win       # ext4; NTFS: see below
sudo clamscan -r -i /mnt/win                     # the whole tree; only list what it finds
```

On NTFS: `sudo ntfs-3g -o ro /dev/sdXn /mnt/win` ([NTFS](../filesystems/ntfs.md)).

Exit code 0 means nothing found, and 1 means it found something. A clean result
does not prove a disk is clean: it knows only what is in its signatures. On evidence,
avoid `--move` and `--remove`.

The signatures are large, and vanish at reboot along with the program. To avoid
downloading them each time, keep them in [persistence](../../persistence/index.md):

```sh
sudo mkdir -p /mnt/d77-data/clamav
sudo freshclam --datadir=/mnt/d77-data/clamav
sudo clamscan -d /mnt/d77-data/clamav -r -i /mnt/win
```

> Installed and tested: `freshclam` downloaded the signatures, and `clamscan`
> detected the EICAR test file. Scanning takes 10 seconds or more just to load
> them. Keeping signatures in persistence was not tested.
