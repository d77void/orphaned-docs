# john: testing and recovering passwords

**Install:** `sudo xbps-install -S john` ([about installing](index.md)) · Only for your
own systems and files, or with authorization

John the Ripper tries many passwords against a password hash until one matches. It
is for recovering a forgotten password, or checking whether a system's passwords
are weak.

```sh
sudo john --wordlist=/usr/share/john/password.lst --format=crypt hashes.txt
sudo john --show hashes.txt                 # what it found so far
john --list=formats                         # the hash types it knows
```

`hashes.txt` holds lines like those in `/etc/shadow`: `user:$6$...`. Linux hashes
(`$6$`) need `--format=crypt`.

Using a password you did not know, on an account or file that is not yours, is a
crime in most places.

> Installed and tested: it found a test password in a SHA-512 hash, with that
> command. For files such as ZIPs, john's converters were not tested.
