# Sessions and logging in

d77orphaned has two optional graphical environments. The console (TTYs 1 to
6, `Ctrl+Alt+F1` to `F6`) always works, with or without them.

| Session | Display system | What you get |
|---|---|---|
| **pwm** | X11 | a tiling window manager with a status bar, the `st` terminal and `dmenu` |
| **wasp + Utumno** | Wayland | a tiling compositor with the Utumno bar and launcher, the `alacritty` terminal and `wmenu` |

Both come from the d77void project. Kantele, the settings program for pwm
and wasp (keyboard, theme, shell, …), is installed for both. In both
sessions there is sound (PipeWire), the battery level (UPower), Mullvad
Browser, and this documentation: run `d77-docs` (it works offline).

## pwm

- The wallpaper follows the pwm theme; changing the theme in Kantele
  changes the wallpaper too.
- A panel at the bottom left (conky) shows the kernel, CPU, memory, network
  address, disks and pwm's main keys.
- `super+return` terminal, `super+d` dmenu, `super+q` close a window,
  `super+x` log out or power off, `super+1…9` workspaces.
- The screen locks after 5 minutes without use, or with `super+t`. Unlock
  with the live user's password, `voidlinux`.
- On laptops, tapping the touchpad clicks.

## wasp + Utumno

- `super+y` opens Utumno's wallpaper picker; the images are in
  `~/Wallpaper`. `super+space` opens the launcher.
- Utumno's bar shows the network (NetworkManager), sound and battery.

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

wasp normally needs a GPU. d77orphaned allows it to fall back to software
rendering (`WLR_RENDERER_ALLOW_SOFTWARE=1`, set in
`/etc/profile.d/d77orphaned-wlr.sh`), so it also starts in virtual machines.
It is slower, and you may see leftovers of the greeter in the background.

> Not verified yet: both sessions with a real GPU on real hardware.
