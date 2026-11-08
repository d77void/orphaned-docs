# sg_sanitize: SAS and SCSI disks

**Package:** `sg3_utils` · **Writes to disks:** yes, the drive erases itself

```sh
sudo sg_sanitize --dry-run --block /dev/sdX   # check the command, send nothing
sudo sg_sanitize --block --wait /dev/sdX      # block erase, and wait
sudo sg_sanitize --crypto --wait /dev/sdX     # cryptographic erase
sudo sg_sanitize --overwrite --wait /dev/sdX  # overwrite
```

It works only if the drive supports the SCSI SANITIZE command, and it can take
hours. It usually does not work through USB adapters.

> Not verified on real drives by this project.
