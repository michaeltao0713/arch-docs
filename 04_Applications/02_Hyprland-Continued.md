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

### Notifiation Daemon

First up is a notification daemon, apparently Electron apps like Discord can freeze without them but I haven't had an issue yet.

I'll be using `swaync`. It's a bit hunkier than `dunst` but it has a built in notifications panel. Install it and put the following in your `hyprland.conf`:

`exec-once = swaync`

and also a keybind for the notification control panel:

`bind = $mainMod, N, exec, swaync-client -t`

Reboot and it should be working now.

### Authentication Agent

We already have PipeWire and XDG-Desktop-Portal, so next up is an Authentication Agent.

Install `hyprpolkitagent` and add this to your hyprland config files: `exec-once = systemctl --user start hyprpolkitagent`. Reboot afterwards.

### QT Wayland Support

Just install both of those libraries: `qt6-wayland` and `qt5-wayland`.

## Monitor Configuration

[Monitors](https://wiki.hypr.land/Configuring/Monitors/)

Just follow the Wiki, it's pretty shrimple and dependent on your set up.

## Uniform Theming

Some apps use `gtk` for their UI, and some use `qt`. `pavucontrol` uses `gtk`. The pop up that shows when Hyprland is updated is `qt` (I think). These are packages made specific Desktop Environments like KDE and GNOME. They also look really out of place and are hard to configure individually.

First thing we'll do is install the generic `xdg-desktop-portal-gtk` and the `qt6ct` packages. Then, write the following into the `hyprland.conf` file.

```
exec-once = gsettings set org.gnome.desktop.interface gtk-theme "YOUR_DARK_GTK3_THEME"   # for GTK3 apps
exec-once = gsettings set org.gnome.desktop.interface color-scheme "prefer-dark"   # for GTK4 apps

env = QT_QPA_PLATFORMTHEME,qt6ct   # for Qt apps
```

Go into `qt6ct.conf` in your configs folder and remove this line: `gui_effects=@Invalid()`.

Might have to change from `exec-once` to `exec`. Reboot after this.

We can use `kvantum` as a gui for setting our `qt` theme, and install a theme from a repo like [this](https://github.com/catppuccin/Kvantum/tree/main), and then configure it further.

We can use `nwg-look` as a gui for setting out `gtk` theme, and install a theme from a repo like [this](https://github.com/catppuccin/gtk/tree/main).

## Status Bar

[Status Bars](https://wiki.hypr.land/Useful-Utilities/Status-Bars/)

Install `waybar`. Copy over the config files or pull from dotfiles repo. Add `exec-once = waybar` to `hyprland.conf`. We'll configure this later because, it's a big one.

We'll also install a widget system later when configuring.

## Idle and Lock

[Hypridle](https://wiki.hypr.land/Hypr-Ecosystem/hypridle/)\
[Hyprlock](https://wiki.hypr.land/Hypr-Ecosystem/hyprlock/)

Install `hypridle` and `hyprlock` and create config files. Sample config files are on the wiki, and my dotfiles.

## Clipboard Manager

[Clipboard Manager](https://wiki.hypr.land/Useful-Utilities/Clipboard-Managers/)

Use `cliphist`. Install with `pacman`.

Follow the set up on the linked page to set up the config.
