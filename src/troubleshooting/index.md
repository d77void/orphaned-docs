# Common problems

Problems seen while testing, with their cause and what to do.

## Black or garbled screen after booting

The graphics driver does not work with this display. Reboot and choose
**(graphics disabled)** in the [boot menu](../getting-started/boot-menu.md).
If that fails too, choose **(console only)**. The console works in every
case, on `Ctrl+Alt+F1`.

## The session ended and a login screen appeared

That is the greeter: the automatic login happens only once per boot. Log in
as `anon` with the password `voidlinux`, and pick **pwm** or **wasp**.

In versions before pwm 0.6.8, pwm sometimes quit right after starting (about
one start in twenty), which dropped you to the greeter. pwm 0.6.8 fixes it.

## With "graphics disabled", a text login appeared

That is expected. Without a graphics driver, the greeter is a text login.
Log in with `anon` and `voidlinux`; `startx /usr/bin/env dbus-launch pwm`
should then start pwm again (not verified yet). See
[Sessions and logging in](../sessions/index.md#without-a-graphics-driver-nomodeset).

## Utumno says "weather unavailable"

Expected: d77orphaned blocks the weather request on purpose. See
[Network](../network/index.md#privacy).

## No network

Wired networks connect by themselves. For Wi-Fi, use `nmtui` or
`nmcli device wifi connect …`; see [Network](../network/index.md#wi-fi).

## A disk does not show up as mounted

Nothing is mounted automatically, on purpose. See
[Working safely with disks](../disks/index.md).

## `sv up sshd` fails

The service has to be linked into `/var/service` first. See
[Network](../network/index.md#ssh-server).
