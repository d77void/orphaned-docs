# memtester and Memtest86+: testing RAM

**Packages:** `memtester`; Memtest86+ is in the boot menu

```sh
sudo memtester 1G 2      # test 1 GiB of free RAM, 2 passes
```

`memtester` tests only memory that Linux is not using. For a full test,
reboot and choose **Memtest86+** in the [boot menu](../../getting-started/boot-menu.md),
and let it run at least one complete pass. Any error there means faulty
RAM.
