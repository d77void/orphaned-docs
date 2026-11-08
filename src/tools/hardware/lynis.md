# lynis: security audit

**Package:** `lynis` · **Writes to disks:** only its log in /var/log

```sh
sudo lynis audit system          # audit the running system (the live system itself)
```

Lynis checks the system it runs on. To audit an installed Linux from
d77orphaned, it has to run inside it (for example in a `chroot`); results
from the live system describe d77orphaned, not the installed machine.
