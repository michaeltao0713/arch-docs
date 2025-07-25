# Basic Hyprland

[Hyprland Arch Wiki](https://wiki.archlinux.org/title/Hyprland)\
[Hyprland Upstream Wiki](https://wiki.hypr.land/Getting-Started/)

## Installing Hyprland

`sudo pacman -S hyprland`

You'll also want to install `kitty` for a terminal and `polkit`.

Also install `xdg-desktop-portal` and the hyprland backend `xdg-desktop-portal-hyprland`. This is used for allowing things like screensharing to operate, or allow your browser to open your file manager when uploading a file.

Don't run `hyprland` just yet if you have a Nvidia GPU. There's a seperate [page](https://wiki.hypr.land/Nvidia/) on the upstream Wiki on setting up Hyprland with a Nvidia GPU. They mention how to set up the drivers, but we've done this already. Just follow the steps. Some of these, we've done already in our driver setup.

I suggest adding the `nvidia.conf` file under `/etc/modprobe.d/` and add this line to the file:

`options nvidia_drm modeset=1`

We'll need to set some environment variables, and rather than throwing it into the system environment variables, I like to put these in the `hyprland.conf` file and reduce the scope to just my user. The variables I set are in my [dotfiles](https://github.com/michaeltao0713/hyprland-dotfiles/blob/main/.config/hypr/hyprland.conf).

About using a multi monitor and multi GPU setup. Connect the external monitor directly to your integrated graphics card. Or else it will spike your CPU usage and be pretty much unusable in terms of lag. If that is not possible, then go into your BIOS settings and turn off dynamic/hybrid graphics, and switch to discrete only. Not a big deal on desktop, but will eat through battery on a laptop. At least it gets rid of the lag.

You should be able to launch Hyprland now. Use Windows+Q to open terminal (assuming you haven't changed the keybinds). Welcome to hyprland!

## Basic Setup

You'll want to install some apps for basic functionality on your system:

Brower: I like Vivaldi (I can no longer like without tab stacks/groups). Install `vivaldi` with pacman.

File Manager: For something with a GUI, use `thunar` or `dolphin`. You can also use a terminal based file manager like `yazi`. I used one for a while because it was nifty, but you run into problems like your browser being unable to open them, and not having the basic functionality of downloading a file.

I use `thunar`. Make sure to install the `xdg-desktop-portal-gtk` package to allow for browsers or an app like discord to open it.

Application Manager: You'll want one so you can launch apps without a terminal. Install `rofi-wayland`.

You'll have to set them as your default apps in the hyprland.conf file. Dotfiles should have these already set.

We'll install more apps and start configuring things later.

## Brightness/Volume Change 

Install `brightnessctl` to be able to use your keyboard brightness change macros. Install `playerctl` to be able to use volume control macros like pause and play.
