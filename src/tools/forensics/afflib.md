# affinfo: AFF images

**Package:** `afflib` · **Writes to disks:** no

```sh
affinfo image.aff          # metadata and segments of an AFF image
affinfo -a image.aff       # all segments, including data segments
```

To read the contents of an AFF image, present it as a raw disk with
[xmount](xmount.md).
