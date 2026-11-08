# sensors and acpi: temperatures and battery

**Packages:** `lm_sensors`, `acpi` · **Writes to disks:** no

```sh
sensors              # CPU, chipset and drive temperatures, fan speeds
acpi -b              # battery level and state
acpi -V              # battery, AC adapter, thermal zones, cooling
upower -d            # battery details as the desktop sees them
```

`sudo sensors-detect` probes for more sensor chips; answer the questions
with the defaults (Enter). The modules it finds are lost at reboot.
