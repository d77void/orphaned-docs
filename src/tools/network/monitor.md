# iftop and nethogs: who uses the network

**Packages:** `iftop`, `nethogs`

```sh
sudo iftop -i eth0 -n -P     # bandwidth per connection, numeric, with ports (q quits)
sudo nethogs eth0            # bandwidth per process
```
