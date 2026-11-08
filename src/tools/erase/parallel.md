# parallel: run on several disks at once

**Package:** `parallel`

Runs a command once per item, several at a time, keeping each one's output
separate. Useful for tools that handle a single disk.

```sh
parallel --tag sudo smartctl -H {} ::: /dev/sda /dev/sdb /dev/sdc      # a safe first try
parallel --tag --dry-run sudo blkdiscard {} ::: /dev/sdb /dev/sdc      # show the commands, run nothing
parallel --tag sudo nvme sanitize {} --sanact=2 ::: /dev/nvme0 /dev/nvme1
```

- `{}` is replaced by each item after `:::`.
- `--tag` starts each line of output with the item it belongs to.
- `--dry-run` only prints what would run: use it first on anything destructive.
- `--jobs N` limits how many run at a time.

It works with anything, not only disks. For overwriting, [nwipe](nwipe.md)
already handles several disks at a time.
