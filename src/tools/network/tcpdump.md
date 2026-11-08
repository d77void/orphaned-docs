# tcpdump: capture traffic

**Package:** `tcpdump` · For networks you are authorized to monitor

```sh
sudo tcpdump -D                                  # interfaces you can capture on
sudo tcpdump -i eth0 -n                          # live, numeric addresses
sudo tcpdump -i eth0 -n port 53                  # only DNS
sudo tcpdump -i eth0 -n host 192.168.1.10        # only one host
sudo tcpdump -i eth0 -c 1000 -w capture.pcap     # save 1000 packets to a file
tcpdump -n -r capture.pcap                       # read a capture back
```

`.pcap` files open in Wireshark on another machine.
