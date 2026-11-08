# nmcli and nmtui: connecting

**Package:** `NetworkManager`

NetworkManager starts at boot and connects wired networks by itself (DHCP).
For Wi-Fi:

```sh
nmtui                                         # menus: "Activate a connection" lists Wi-Fi networks
nmcli device wifi list                        # visible Wi-Fi networks
nmcli device wifi connect "NetworkName" password 'the passphrase'
nmcli device status                           # each interface and its state
nmcli connection show                         # saved connections
nmcli connection down "NetworkName"           # disconnect
nmcli radio wifi off                          # turn Wi-Fi off
```

The live user can run these without `sudo`. Saved connections are lost at
reboot, like everything else.

To stay **offline** (e.g. when examining a machine that must not touch a
network): `nmcli networking off`, and `nmcli networking on` to come back.
