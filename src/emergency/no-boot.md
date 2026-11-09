# The computer does not boot

**Writes to the disk:** yes, the boot loader and its configuration. Your files are
not touched, but [copy them first](dying-disk.md) if the disk is at all suspect.

This page is for a Linux system whose boot loader is gone or broken, after a disk
swap, a Windows reinstall, or a failed update. It reinstalls GRUB from inside the
installed system.

## 1. Find out what you have

Boot d77orphaned and look:

```sh
lsblk -o NAME,SIZE,FSTYPE,LABEL,PARTLABEL,MOUNTPOINT
sudo os-prober
[ -d /sys/firmware/efi ] && echo UEFI || echo BIOS
```

The last line says how **d77orphaned** started, which is how you should start it
for the repair: the computer should boot the stick in the same mode as the
installed system.

You are looking for the system's root partition, its `/boot` if separate, and on
UEFI the EFI System Partition (`vfat`, usually 100 MB to 1 GB).

## 2. Mount the system

Plain partition, replacing `sdXn` with what you found:

```sh
sudo mount /dev/sdXn /mnt
```

Encrypted, with LVM, which d77orphaned never opens by itself:

```sh
sudo cryptsetup open /dev/sdXn cr
sudo vgchange -ay vg0              # your volume group: see `sudo vgs`
sudo mount /dev/vg0/root /mnt
```

Then whichever exist, in this order:

```sh
sudo mount /dev/sdXb /mnt/boot             # a separate /boot
sudo mount /dev/sdXe /mnt/boot/efi         # the EFI partition (or /mnt/efi: see the system's /etc/fstab)
```

Check with `cat /mnt/etc/fstab` that this matches what the system expects.

## 3. Enter the system

```sh
sudo xchroot /mnt /bin/bash
```

`xchroot` sets up `/dev`, `/proc`, `/sys` and DNS, and undoes them when you leave.
From here on, commands run with the **installed system's own programs**, so its
`grub` is the one used.

## 4. Reinstall the boot loader

BIOS, on the **whole disk** (`sdX`, not `sdX1`):

```sh
grub-install --target=i386-pc /dev/sdX
```

UEFI:

```sh
grub-install --target=x86_64-efi --efi-directory=/boot/efi --removable --no-nvram
```

`--removable` puts GRUB in the fallback location that firmware looks in by itself,
so this works even if the firmware's boot entries were lost, and it needs no
changes to them. Some firmware prefers a named entry, which is what happens
without those two options, with `--bootloader-id=Void`. That form was not tested.

Then rebuild the menu, by distribution (only Void was tested):

| System | Command |
|---|---|
| Void | `grub-mkconfig -o /boot/grub/grub.cfg` |
| Arch | `grub-mkconfig -o /boot/grub/grub.cfg` |
| Debian, Ubuntu | `update-grub` |
| Fedora | `grub2-mkconfig -o /boot/grub2/grub.cfg`, and `grub2-install` above |

If the initramfs is also suspect, rebuild it. On Void:
`xbps-reconfigure -f linux6.18` (your version: see `ls /usr/lib/modules`).

## 5. Leave and restart

```sh
exit
sudo umount -R /mnt
sudo vgchange -an vg0 && sudo cryptsetup close cr     # only if you opened them
sudo reboot
```

## If it still does not boot

- Check the firmware's boot order, and on UEFI, `efibootmgr -v`
  ([more](../tools/hardware/boot.md)).
- Windows is on another disk or in the same firmware? Its loader can be the one
  starting first.
- GRUB's own prompt (`grub>`) usually means the configuration, not the loader:
  repeat the `grub-mkconfig` step, and check `/boot` was mounted.
- If the system was installed in the other mode, BIOS or UEFI, change the
  firmware back rather than converting the system.

> Tested in a virtual machine, with Void Linux installed on a test disk, on both a
> plain ext4 root and LUKS2 + LVM with a separate `/boot`. The boot loader and EFI
> directory were destroyed so the disk no longer started; after this procedure it
> booted with both BIOS and UEFI. Not tested: real firmware, an encrypted `/boot`,
> a named UEFI entry, other distributions, or dual-boot with Windows.
