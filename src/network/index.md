# Network

## Wired

NetworkManager starts at boot and connects a wired network by itself
(DHCP). Check with:

```sh
ip -br addr
ping -c 3 voidlinux.org
```

Verified in a virtual machine: address, route and DNS were set automatically.

The clock is set over the network by `chronyd`, which also runs at boot.

## Wi-Fi

Use `nmtui` (menus) or `nmcli`:

```sh
nmcli device wifi list
nmcli device wifi connect "NetworkName" password 'the passphrase'
```

In the wasp session, Utumno's network indicator shows the connection. More
in [nmcli and nmtui](../tools/network/networkmanager.md).

Some Wi-Fi cards need firmware that is not free software; the image has the
firmware from Void's `linux-firmware` package only.

> Tested on real hardware by the user (Wi-Fi works with the right
> NetworkManager commands); not verified on other machines.

`dhcpcd` and `wpa_supplicant` are still installed for manual use, but not
started at boot, so they do not compete with NetworkManager.

## Staying offline

To examine a machine without touching any network, turn networking off
before connecting a cable: `nmcli networking off` (and `on` to come back).

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
d77orphaned blocks it (`/etc/hosts`). The bar shows "weather unavailable";
this is expected.
