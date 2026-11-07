# Sessions and logging in

D77orphaned has two optional graphical environments. The console (TTYs 1 to
6, `Ctrl+Alt+F1` to `F6`) always works, with or without them.

| Session | Display system | What you get |
|---|---|---|
| **pwm** | X11 | a tiling window manager with a status bar, the `st` terminal and `dmenu` |
| **wasp + Utumno** | Wayland | a tiling compositor with the Utumno bar and launcher, the `alacritty` terminal and `wmenu` |

Both come from the d77void project. Kantele, the settings program for pwm
and wasp (keyboard, appearance, …), is installed for both.

## What happens at boot

1. With the normal entry, **pwm starts on its own** as the user `anon`. pwm
   is the default because X11 works on the widest range of hardware.
2. When you leave pwm, the **login screen** (greeter) appears on the same
   screen (TTY 7). Type `anon` and `voidlinux`, then choose the session:
   **pwm** or **wasp**.
3. From then on, each time you leave a session you return to the greeter.

The automatic login happens only once per boot.

## Without a graphics driver (`nomodeset`)

With the *graphics disabled* entry, there is no graphics driver. In this mode:

- pwm still starts on its own, on the basic VESA or framebuffer display. In
  a virtual machine it ran at 1920×1080.
- The graphical greeter needs a working graphics driver, so it is replaced by
  a **text login** (`agreety`). After pwm ends, log in there with `anon` and
  `voidlinux` to get a shell. Typing `startx /usr/bin/env dbus-launch pwm`
  there should start pwm again (not verified yet).
- wasp is not available.

## Console only (`d77.nogui`)

With the *console only* entry, no graphical session starts. Log in on any
TTY. The greeter service (`greetd`) is stopped; `sudo sv up greetd` starts it
if you change your mind.

## Without a GPU

wasp normally needs a GPU. D77orphaned allows it to fall back to software
rendering (`WLR_RENDERER_ALLOW_SOFTWARE=1`, set in
`/etc/profile.d/d77orphaned-wlr.sh`), so it also starts in virtual machines.
It is slower, and you may see leftovers of the greeter in the background.

> Not verified yet: both sessions with a real GPU on real hardware.
