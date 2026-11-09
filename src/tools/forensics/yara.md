# yara: search with rules

**Package:** `yara` · **Writes to disks:** no

Looks for patterns (text, bytes, conditions) described in rule files, typically
to recognise malware or known files. d77orphaned ships no rules: bring your own.

```sh
yara rules.yar suspicious.exe              # which rules match this file
yara -r rules.yar /mnt/evidence            # a whole folder, recursively
yara -s rules.yar suspicious.exe           # also show the matching strings
```

A minimal rule, in `rules.yar`:

```
rule contains_password {
    strings:
        $a = "password" nocase
    condition:
        $a
}
```
