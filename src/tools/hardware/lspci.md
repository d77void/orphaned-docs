# lspci and lsusb: PCI and USB devices

**Packages:** `pciutils`, `usbutils` · **Writes to disks:** no

```sh
lspci                 # PCI devices: graphics, network, storage, …
lspci -k              # with the kernel driver in use
lspci -nn             # with vendor:device IDs (to search for driver support)
lsusb                 # USB devices
lsusb -t              # USB tree, with drivers and speeds
```

A device with no "Kernel driver in use" line in `lspci -k` has no working
driver, a common cause of missing Wi-Fi or graphics.
