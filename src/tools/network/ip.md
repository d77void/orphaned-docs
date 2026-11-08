# ip: addresses, routes, interfaces

**Package:** `iproute2`

```sh
ip -br addr             # each interface with its addresses, one line each
ip -br link             # interfaces and whether the link is up
ip route                # routing table (the "default via" line is the gateway)
ip neigh                # neighbours (ARP/NDP cache)
sudo ip link set eth0 down       # take an interface down (and "up" again)
sudo ip addr add 192.168.1.50/24 dev eth0   # add a static address by hand
```

Interfaces managed by NetworkManager are better changed with
[nmcli](networkmanager.md); manual changes may be overwritten.
