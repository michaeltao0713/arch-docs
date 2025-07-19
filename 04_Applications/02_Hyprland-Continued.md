# Hyperland Continued

[Hyprland Arch Wiki](https://wiki.archlinux.org/title/Hyprland#xdg-desktop-portal-hyprland)\
[Hyprland Upstream Wiki](https://wiki.hypr.land/Getting-Started/Master-Tutorial/#launching-hyprland)

We'll now install some apps and change some configurations for our Hyprland setup to make it more usable.

## Display Manager

When we boot our computer, we want a nice login screen as opposed to a tty console. I'll be installing `ly`, a minimal TUI Display Manager. Note that if we want Hyprland to lock the screen after idling, we'll need a different piece of software.

Do a bit of configuration or pull a config file from dotfiles, and then (make sure this is how it is for your display manager of choice) enable the display manager service with `systemctl enable`.

## "Must Have" Software

[Must Have](https://wiki.hypr.land/Useful-Utilities/Must-have/)

We'll be installing these, as they're pretty important.

First up is a notification daemon, apparently Electron apps like Discord can freeze without them but I haven't had an issue yet.

I'm thinking of using `swaync` honestly, even though it relies on gtk, it just looks the best out of box. I'll need to do more research into this.


