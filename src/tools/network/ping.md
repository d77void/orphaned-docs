# ping, traceroute, mtr: reachability and path

**Packages:** `iputils`, `traceroute`, `mtr`

```sh
ping -c 4 1.1.1.1              # is the internet reachable? (no DNS involved)
ping -c 4 voidlinux.org        # … and does DNS work?
traceroute voidlinux.org       # the routers on the way
mtr voidlinux.org              # live traceroute with loss per hop (q quits)
mtr -r -c 20 -n voidlinux.org  # report after 20 probes, numeric addresses
```

If `ping 1.1.1.1` works but `ping voidlinux.org` does not, the problem is
DNS; see [dig](dns.md).
