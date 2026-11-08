# nc and socat: raw connections

**Packages:** `nmap` (provides `nc`, which is `ncat`), `socat`

```sh
nc -zv 192.168.1.10 22                       # is the port open?
nc -l 9000 > received.img                    # receiver: listen on port 9000
nc 192.168.1.20 9000 < disk.img              # sender: send a file to it
socat - TCP:192.168.1.10:80                  # talk to a TCP port by hand
socat TCP-LISTEN:8080,fork TCP:10.0.0.5:80   # forward a local port to another host
```

`nc` here is **Ncat** (from the nmap package), not the OpenBSD netcat; the
basic options above work in both. Data sent with `nc` is not encrypted; use
[ssh/rsync](ssh.md) over untrusted networks.
