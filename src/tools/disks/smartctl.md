# smartctl: disk health (SMART)

**Package:** `smartmontools` · **Writes to disks:** no (a self-test runs inside the drive and does not change data)

Reads the health data that SATA and NVMe drives keep about themselves:
reallocated sectors, read errors, temperature, power-on hours.

```sh
sudo smartctl -H /dev/sdX            # overall verdict: PASSED or FAILED
sudo smartctl -a /dev/sdX            # everything: identity, attributes, error log, self-tests
sudo smartctl -x /dev/sdX            # even more (extended logs)
sudo smartctl -i /dev/nvme0          # identity: model, serial, firmware, capacity
sudo smartctl -t short /dev/sdX      # start a short self-test (about 2 minutes)
sudo smartctl -t long /dev/sdX       # start a long self-test (can take hours)
sudo smartctl -l selftest /dev/sdX   # results of the self-tests
sudo smartctl -X /dev/sdX            # abort a running self-test
```

What to look at in `-a` for a SATA disk: `Reallocated_Sector_Ct`,
`Current_Pending_Sector` and `Offline_Uncorrectable` above zero mean the disk
is losing sectors; copy the data off it first (see [ddrescue](../recovery/ddrescue.md)).
For NVMe, look at `Media and Data Integrity Errors` and `Percentage Used`.

USB enclosures sometimes hide SMART; `-d sat` (for example
`sudo smartctl -a -d sat /dev/sdX`) often gets through.
