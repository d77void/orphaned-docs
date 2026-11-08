# lsscsi and sg_inq: SCSI, SAS and USB disks

**Packages:** `lsscsi`, `sg3_utils` · **Writes to disks:** no (commands below)

```sh
lsscsi                  # SCSI/SATA/USB devices with vendor, model and /dev name
lsscsi -s               # with sizes
sudo sg_inq /dev/sdX    # the device's own identification (INQUIRY)
```

Useful when a disk sits behind a USB adapter or a SAS controller and
`lsblk` shows little about it.
