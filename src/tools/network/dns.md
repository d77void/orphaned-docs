# dig, host, whois: DNS and domains

**Packages:** `bind-utils`, `whois`

```sh
dig voidlinux.org              # full answer, with the server that replied
dig +short voidlinux.org       # just the addresses
dig voidlinux.org MX           # mail servers (also NS, TXT, AAAA, …)
dig @9.9.9.9 voidlinux.org     # ask a specific DNS server
dig -x 1.1.1.1                 # reverse lookup
host voidlinux.org             # short form
whois voidlinux.org            # who registered the domain
cat /etc/resolv.conf           # DNS servers in use
```
