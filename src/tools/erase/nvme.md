# NVMe sanitize and format

**Package:** `nvme-cli` · **Writes to disks:** yes, the drive erases itself

Note the two device names: `/dev/nvme0` is the controller, `/dev/nvme0n1` the
namespace.

```sh
sudo nvme id-ctrl /dev/nvme0 -H | grep -iE 'format|crypto|sanitize'   # what it supports

# Sanitize: the strongest; covers the whole drive, and survives a power loss
sudo nvme sanitize /dev/nvme0 --sanact=2      # block erase
sudo nvme sanitize /dev/nvme0 --sanact=4      # crypto erase
sudo nvme sanitize-log /dev/nvme0             # progress and result

# Format: where sanitize is not supported
sudo nvme format /dev/nvme0n1 --ses=1         # erase user data
sudo nvme format /dev/nvme0n1 --ses=2         # crypto erase
```

Use the value the drive reports as supported. Sanitize keeps running in the
background after the command returns: check it with `sanitize-log`.

> Not verified on real drives by this project.
