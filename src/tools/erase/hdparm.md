# ATA Secure Erase with hdparm: SATA drives

**Package:** `hdparm` · **Writes to disks:** yes, the drive erases itself

For SATA SSDs and hard disks. The drive does the work, and it usually covers
areas software cannot reach. It does not normally work through USB adapters.

```sh
sudo hdparm -I /dev/sdX | grep -A8 Security   # supported? "not frozen"? how long will it take?
sudo hdparm --user-master u --security-set-pass erase /dev/sdX   # set a temporary password
sudo hdparm --user-master u --security-erase erase /dev/sdX      # erase (the password is removed)
sudo hdparm -I /dev/sdX | grep -A8 Security   # "not enabled" again
```

`--security-erase-enhanced` instead of `--security-erase` also covers
reallocated areas, if `hdparm -I` lists it as supported.

- **"frozen":** the BIOS froze the security commands at boot. Suspending and
  resuming the machine often clears it, as does plugging the drive in after
  boot; not all machines allow either.
- **Do not interrupt it,** or power off: a drive left locked needs the password
  (`--security-unlock erase`, then `--security-disable erase`) to be usable.

> Not verified on real drives by this project. On laptops, some firmwares have
> been reported to brick drives on these commands: try on a drive you can lose.
