# efibootmgr, efivar, os-prober: boot

**Packages:** `efibootmgr`, `efivar`, `os-prober` · **Writes:** `efibootmgr` changes firmware settings when told to

```sh
efibootmgr                 # UEFI boot entries and boot order
efibootmgr -v              # with the file each entry starts
efivar -l                  # all UEFI variables
sudo os-prober             # other operating systems installed on the disks
```

Missing or wrong boot entries are a common reason for "no bootable device"
after a disk swap or a Windows update. `efibootmgr` can create, reorder and
delete entries (`-c`, `-o`, `-B`).

> **Writes:** `efibootmgr` options that change entries write to the
> firmware's memory, not to disks; a wrong boot order can still make the
> machine boot into the wrong system. `os-prober` mounts partitions to look
> inside them; on disks under examination, mark them read-only first
> ([blockdev](../disks/blockdev.md)).
