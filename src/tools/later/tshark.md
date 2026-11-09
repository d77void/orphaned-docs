# tshark and termshark: analysing captures

**Install:** `sudo xbps-install -S wireshark termshark` ([about installing](index.md)) ·
For networks you are authorized to test

`tshark` is Wireshark for the console, and comes in the `wireshark` package.
`termshark` is a full-screen interface over it. To only capture, you do not need
either: [tcpdump](../network/tcpdump.md) is in the image, and you can analyse the file
later on another computer.

```sh
sudo tshark -D                                  # the interfaces
sudo tshark -i eth0 -c 100                      # capture 100 packets
sudo tshark -i eth0 -f "port 53" -w dns.pcapng  # a capture filter, to a file
tshark -r dns.pcapng                            # read a file
tshark -r dns.pcapng -Y "dns.qry.name contains example"     # a display filter
tshark -r dns.pcapng -T fields -e ip.src -e dns.qry.name    # only some fields
termshark -r dns.pcapng                         # explore a file, full screen
sudo termshark -i eth0                          # capture live
```

The graphical program is a separate package, `wireshark-qt`. It was not tested here.

> Installed. Tested: `tshark -r` on a `tcpdump` capture. Other options checked
> against the help. `termshark` was not run with a capture.
