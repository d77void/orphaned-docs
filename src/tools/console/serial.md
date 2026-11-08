# minicom and tio: serial consoles

**Packages:** `minicom`, `tio`

For the console port of routers, switches, servers and development boards,
usually through a USB serial adapter (`/dev/ttyUSB0`).

```sh
tio -l                          # serial devices found
sudo tio /dev/ttyUSB0           # connect at 115200 baud (Ctrl+t q quits)
sudo tio -b 9600 /dev/ttyUSB0   # at 9600 baud
sudo minicom -D /dev/ttyUSB0 -b 9600   # the same with minicom (Ctrl+a x quits)
```
