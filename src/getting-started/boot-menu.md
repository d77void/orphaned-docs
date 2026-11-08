# The boot menu

The same entries appear on BIOS computers (isolinux menu) and on UEFI
computers (GRUB menu). The default entry starts after a short timeout.

| Entry | What it does | When to use it |
|---|---|---|
| **d77orphaned** | Normal boot: the pwm session starts on its own | most of the time |
| **(RAM)** | Copies the whole system into memory first (`rd.live.ram`) | to remove the USB stick after booting; the system image is about 1.4 GB, so it needs more RAM than that (not verified on real hardware) |
| **(graphics disabled)** | Boots with `nomodeset`: no graphics driver, basic VESA/framebuffer display | when the normal entry shows a black or garbled screen |
| **(console only)** | Boots with `d77.nogui`: no graphical session at all | for text-only work, or when graphics do not work at all |
| **Memtest86+** | Memory test, without starting Linux | to check RAM |

The BIOS menu also has *Boot first HD found by BIOS*, *Reboot* and *Power Off*.
The UEFI menu has *UEFI Firmware Settings*, *System restart* and *System
shutdown*.

## What every entry has in common

Every Linux entry passes these options to the kernel:

```
rd.luks=0 rd.md=0 rd.dm=0 rd.lvm=0
```

They stop the early boot stage from unlocking LUKS, assembling RAID or
activating LVM and device-mapper volumes on the computer's disks. After
boot, d77orphaned also disables the rules that would do this later. See
[Working safely with disks](../disks/index.md).

## Keyboard layout and language

The ISO boots with the `us` keyboard layout and `en_US.UTF-8`. To change them
for one boot, edit the entry (`Tab` in the BIOS menu, `e` in GRUB) and change
`vconsole.keymap=` and `locale.LANG=`, for example
`vconsole.keymap=pt-latin1`.

In the graphical sessions, Kantele (the settings program for pwm and wasp)
sets the keyboard layout. From an X11 terminal, `setxkbmap pt` also works for
the current session.

> Not verified yet: changing the layout from the boot menu. Kantele's keyboard
> setting was tested on real hardware.
