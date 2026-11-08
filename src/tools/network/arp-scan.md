# arp-scan: devices on the local network

**Package:** `arp-scan` · For networks you are authorized to test

```sh
sudo arp-scan -l                 # every device on the local subnet: IP, MAC, vendor
sudo arp-scan -I wlan0 -l        # on a specific interface
```

Finds devices that ignore ping, since every device must answer ARP.
