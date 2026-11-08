# LVM: logical volumes

**Package:** `lvm2` · **Writes to disks:** not with the commands below

d77orphaned never activates LVM volumes on its own.

```sh
sudo pvs; sudo vgs; sudo lvs           # physical volumes, volume groups, logical volumes
sudo vgchange -ay --config 'activation { read_only_volume_list = [ "myvg" ] }' myvg
sudo lvs myvg                          # attributes "-Ri-a-": active (a) and read-only (R)
sudo mount -o ro,noload /dev/myvg/root /mnt
sudo umount /mnt && sudo vgchange -an myvg     # deactivate when done
```

Verified in a virtual machine: the logical volumes were active and
read-only, writes failed and the disk's hash did not change.

> **Avoid** `vgchange -ay --readonly` (activates nothing) and
> `lvchange -pr` (writes the permission into the metadata on the disk).
