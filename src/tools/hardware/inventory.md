# lshw, hwinfo, dmidecode: hardware inventory

**Packages:** `lshw`, `hwinfo`, `dmidecode` · **Writes to disks:** no

```sh
sudo lshw -short                  # every device in a compact table
sudo lshw -class disk -class storage   # only disks and controllers
sudo lshw -html > hardware.html   # full report as a web page
sudo lshw -sanitize -short        # without serial numbers
hwinfo --short                    # another summary, grouped by type
sudo dmidecode -t system          # manufacturer, model, serial number, UUID
sudo dmidecode -t memory          # RAM slots, sizes, speeds
sudo dmidecode -s bios-version    # one value
```

`dmidecode` reads the firmware's tables (SMBIOS): useful to identify a
machine for an inventory or a warranty claim.
