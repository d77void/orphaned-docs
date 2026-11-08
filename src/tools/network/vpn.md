# WireGuard and OpenVPN

**Packages:** `wireguard-tools`, `openvpn`

```sh
sudo wg-quick up ./wg0.conf        # bring up a WireGuard tunnel from a config file
sudo wg show                       # its state, peers and traffic
sudo wg-quick down ./wg0.conf
sudo openvpn --config client.ovpn  # an OpenVPN connection (Ctrl+C to stop)
```

NetworkManager can also import these: `nmcli connection import type
wireguard file wg0.conf` (and `type openvpn` needs a plugin that is not
installed).
