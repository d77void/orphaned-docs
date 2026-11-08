# nvme: NVMe drives

**Package:** `nvme-cli` · **Writes to disks:** only the commands marked below

```sh
sudo nvme list                   # NVMe drives: model, serial, size, firmware
sudo nvme smart-log /dev/nvme0   # health: temperature, wear, media errors
sudo nvme error-log /dev/nvme0   # the drive's error log
sudo nvme id-ctrl /dev/nvme0     # everything the controller reports about itself
```

> **Writes:** `nvme format` and `nvme sanitize` erase the drive. Never on a disk
> you want to keep; to erase one on purpose, see [NVMe sanitize and format](../erase/nvme.md).

[smartctl](smartctl.md) also reads NVMe health.
