# Common problems

Problems seen while testing, with their cause and what to do.

## Black or garbled screen after booting

The graphics driver does not work with this display. Reboot and choose
**(graphics disabled)** in the [boot menu](../getting-started/boot-menu.md).
If that fails too, choose **(console only)**, which always gives a text
console.

## The session ended and a login screen appeared

That is the greeter: the automatic login happens only once per boot. Log in
as `anon` with the password `voidlinux`, and pick **pwm** or **wasp**.

In versions before pwm 0.6.8, pwm sometimes quit right after starting (about
one start in twenty), which dropped you to the greeter. pwm 0.6.8 fixes it.

## With "graphics disabled", logging out restarts pwm, and Ctrl+Alt+F2 does nothing

That is expected: on some computers, leaving X in this mode leaves a black
screen for good. Use shutdown or reboot in pwm's menu (`super+x`). See
[Sessions and logging in](../sessions/index.md#without-a-graphics-driver-nomodeset).

## Utumno says "weather unavailable"

Expected: d77orphaned blocks the weather request on purpose. See
[Network](../network/index.md#privacy).

## No network

Wired networks connect by themselves. For Wi-Fi, use `nmtui` or
`nmcli device wifi connect …`; see [Network](../network/index.md#wi-fi).

## Programs crash at random, or `SQUASHFS error` / `Input/output error`

The system cannot read the USB stick reliably. Programs then fail in strange
ways, such as a segmentation fault in `su`. Seen on an old laptop with a stick
that works elsewhere. Try another USB port (no hubs), then the **(RAM)** boot
entry, which copies the system to memory at boot. If it persists, run
**Memtest86+** from the boot menu. See also [Download](../getting-started/download.md)
to check the stick.

## nwipe's screen is unreadable

In pwm's terminal it is. See [nwipe](../tools/erase/nwipe.md).

## A disk does not show up as mounted

Nothing is mounted automatically, on purpose. See
[Working safely with disks](../disks/index.md).

## `sv up sshd` fails

The service has to be linked into `/var/service` first. See
[Network](../network/index.md#ssh-server).
