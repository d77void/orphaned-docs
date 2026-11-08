# iperf3: bandwidth

**Package:** `iperf3`

```sh
iperf3 -s                          # on one machine: server
iperf3 -c 192.168.1.10             # on the other: test upload to it (10 s)
iperf3 -c 192.168.1.10 -R          # test download (reverse)
iperf3 -c 192.168.1.10 -P 4 -t 30  # 4 parallel streams, 30 seconds
```

Tells a slow cable, switch port or Wi-Fi link apart from a slow server.
