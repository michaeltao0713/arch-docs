# Graphical User Interface

[General Recommendations](https://wiki.archlinux.org/title/General_recommendations#Graphical_user_interface)

We're almost able to escape the cold and dark tty console, and start using an actual desktop environment. We'll be going over the entirety of section 4 of [General Recommendations](https://wiki.archlinux.org/title/General_recommendations#Graphical_user_interface) to set up an interatable system.

## Choosing a Display Server

[Wayland](https://wiki.archlinux.org/title/Wayland)\
[Xorg](https://wiki.archlinux.org/title/Xorg)

The display server is a protocol that runs underneath your entire GUI setup. There are two: Xorg and Wayland. Wayland is newer and current Desktop Environments are starting to phase out the use of Xorg. I suggest using Wayland and reading through it's Wiki.

If you're using a Nvidia GPU, you might need to set some environment variables to be able to use Hyprland, but we'll do that later. For future me: this is already done in the hyprland.conf file in your dotfiles.

We'll need to install `xorg-xwayland` for backwards compatibility with x11 only applications.

For GUI libraries:

gtk3 and later will support Wayland, nothing needs to be done.

`qt5` and `qt6` need `qt5-wayland` and `qt6-wayland` respectively. Will probably be installed automatically with `hyprland`.

Electron is terrible and still doesn't really support Wayland. I'll be setting the environment variable later when setting up hyprland.

## Desktop Environments

A desktop environment is a bundle of programs that make up a desktop. KDE is probably the current best DE, with it's incredible customization and support. GNOME is apparently highly unoptimized. Cinnamon is a bit outdate. Cosmic is looking good, but still in Alpha. We're not going to use a DE; we'll be using Hyprland, a compositor based on Wayland.

I find desktop environments to be, kind of bloated, and install packages that you perhaps would not want. But KDE Plasma is still an incredible choice, if you want a more Windows-like experience.

## Window Managers and Compositors

I'll be using Hyprland, a dynamic compositor that looks very pretty and is very customizable. Might be jumping on the bandwagon, but it is a very popular choice for dynamic tiling window capabilities. We'll get to Display Manager when installing applications for the Hyprland setup.

Our next topic is on setting up Hyprland with very basic functionality.
