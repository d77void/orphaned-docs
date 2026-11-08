# nmap: hosts and open ports

**Package:** `nmap` (Void's "nonfree" repository) · For networks you are authorized to test

```sh
sudo nmap -sn 192.168.1.0/24                 # which hosts are up (no port scan)
nmap 192.168.1.10                            # the 1000 most common TCP ports
nmap -p 22,80,443 192.168.1.10               # only these ports
nmap -p- 192.168.1.10                        # all 65535 TCP ports (slow)
sudo nmap -sV 192.168.1.10                   # versions of the services found
sudo nmap -O 192.168.1.10                    # guess the operating system
nmap -Pn 192.168.1.10                        # scan even if it does not answer ping
nmap -oN scan.txt 192.168.1.0/24             # save the results
```
