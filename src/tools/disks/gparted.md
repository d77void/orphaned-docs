# gparted: partitions, graphically

**Package:** `gparted` · **Writes to disks:** only when you apply

Create, delete, move, resize and check partitions in a window.

```sh
sudo -E gparted            # in pwm or wasp
sudo -E gparted /dev/sdX   # open one disk
```

Operations queue up and **nothing is written until you click Apply**; until
then, you can undo them.

> **Moving or resizing can lose data if interrupted.** Never on a failing disk or
> on evidence: copy it first with [ddrescue](../recovery/ddrescue.md). Do not
> use it on a disk you are examining.

Opening it changes nothing: in a virtual machine, a disk holding ext4, swap, LUKS
and LVM stayed identical, byte for byte, with nothing mounted or activated. In
wasp, plain `sudo gparted` fails with `cannot open display`; `-E` fixes it.
