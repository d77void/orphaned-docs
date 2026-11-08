# Hardware and boot

Identify a machine's hardware, check it under load, and look at (or fix)
how it boots. For disk health, see [smartctl](../disks/smartctl.md).

| Tool | For |
|---|---|
| [inxi](inxi.md) | a one-screen summary of the whole machine |
| [lshw, hwinfo, dmidecode](inventory.md) | detailed hardware inventory, serial numbers |
| [lspci and lsusb](lspci.md) | PCI and USB devices, and their drivers |
| [sensors and acpi](sensors.md) | temperatures, fans, battery |
| [memtester and Memtest86+](memory.md) | testing RAM |
| [stress and fio](stress.md) | load tests: CPU, memory, disk |
| [cpuid and cpupower](cpu.md) | CPU details and frequency |
| [efibootmgr, efivar, os-prober](boot.md) | UEFI boot entries, finding installed systems |
| [chntpw](chntpw.md) | Windows local accounts (reset a password) |
| [lynis](lynis.md) | security audit of a Linux system |
