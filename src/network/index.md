# Network

## Wired

A wired connection works by itself: `dhcpcd` runs at boot and configures
every interface that gets a DHCP answer. Check with:

```sh
ip -br addr
ping -c 3 voidlinux.org
```

Verified in a virtual machine: address, route and DNS were set automatically.

The clock is set over the network by `chronyd`, which also runs at boot.

## Wi-Fi

There is no NetworkManager. Wi-Fi uses `wpa_supplicant`, and `dhcpcd` then
gets an address for it. Find the interface name with `ip -br link` (here
`wlan0`):

```sh
wpa_passphrase "NetworkName" 'the passphrase' | sudo tee -a /etc/wpa_supplicant/wpa_supplicant.conf
sudo wpa_supplicant -B -i wlan0 -c /etc/wpa_supplicant/wpa_supplicant.conf
ip -br addr show wlan0          # an address appears after a few seconds
```

Some Wi-Fi cards need firmware that is not free software; the image has the
firmware from Void's `linux-firmware` package only.

> Not verified yet: Wi-Fi on real hardware.

The network indicator in Utumno's bar reads NetworkManager, so it shows
"offline" even when the connection works. Trust `ip addr` instead.

## Nothing listens

No network service is running: the system listens on no TCP port. Check with
`ss -tlnp`.

## SSH server

`sshd` is installed but not enabled. The passwords are the same on every
copy of the ISO, so change them first:

```sh
sudo passwd anon
sudo passwd root
sudo ln -s /etc/sv/sshd /var/service/
```

`sudo sv up sshd` does not work on its own: the service has to be linked
into `/var/service` first, as above. To stop it again, remove the link:
`sudo rm /var/service/sshd`.

## Privacy

Utumno's bar normally fetches the weather from `wttr.in` when the wasp
session starts. That would tell an outside service your public IP address, so
D77orphaned blocks it (`/etc/hosts`). The bar shows "weather unavailable";
this is expected.
