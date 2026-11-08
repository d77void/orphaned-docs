# iw and ethtool: link details

**Packages:** `iw`, `ethtool`

```sh
iw dev                          # Wi-Fi interfaces
iw dev wlan0 link               # the access point, signal and bitrate
sudo iw dev wlan0 scan | grep -E 'SSID|signal'   # nearby networks
ethtool eth0                    # Ethernet speed, duplex, "Link detected"
sudo ethtool -i eth0            # driver and firmware
```

`rfkill list` (from `util-linux`) shows whether Wi-Fi is blocked by a switch
or key; `rfkill unblock wifi` lifts a software block.
