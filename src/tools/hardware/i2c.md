# i2c-tools: the I2C/SMBus buses

**Package:** `i2c-tools` · **Writes:** `i2cset`, and `i2cdetect` can disturb some devices

Lists the small chips on a computer's internal bus: RAM SPD, sensors, and so on.

```sh
sudo modprobe i2c-dev        # the devices appear in /dev
sudo i2cdetect -l            # the buses
sudo i2cdetect 0             # which addresses answer on bus 0 (it asks to confirm)
sudo i2cdump 0 0x50          # read a chip's registers
```

> Probing some chips can upset them, and writing to the wrong one (with `i2cset`)
> has been known to damage hardware, such as RAM SPD. Read only, unless you know
> exactly what the chip is.
