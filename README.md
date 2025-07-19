# Arch Linux Documentation

This is a collection of documents regarding my experience with installing and setting up Arch Linux on my personal laptop. This is for when I inevitably switch to different hardware and will need to go through this process once again. It is my hope that this provides much aid to my future self.

## Table of Contents

- Getting Started
    - [Overview](01_Getting-Started/01_Overview.md)
    - [Pre-Installation](01_Getting-Started/02_Pre-Installation.md)
- Installation
    - [Installing Arch](02_Installation/01_Installing-Arch.md)
- Post Installation
    - [Setting Up](03_Post-Installation/01_Setting-Up.md)
    - [Desktop Environment](03_Post-Installation/02_Graphical-User-Interface.md)
    - [Basic Hyprland](03_Post-Installation/03_Basic-Hyprland.md)
    - [Package Management](03_Post-Installation/04_Package-Management.md)
    - [System Administration](03_Post-Installation/05_System-Administration.md)
- Applications
    - [Essential Applications](04_Applications/01_Essential-Applications.md)



Do next:

Write about configuring hyprland (using arch wiki and upstream wiki)
Write about setting up discord, and steam.
Write about configuring neovim. (A pacman hook for lazy.nvim updates?)
Read and write about section 3, section 5-12 in General Recommendations Wiki Page for more things to do.

Figure out media play macro
Read the Hyprland Arch Wiki page for tips and tricks

Install (and Configure):
Hyprland recommended applications on their Wiki.
Notification daemon
Waybar
    Extensions for waybar would be:
    workspaces
    applets (NM, discord, pavucontrol)
Clipboard manager (there is a Wiki page for this)
Screenshot tool
ly or whatever display manager i want to use. (can I just use hyprlock?)
look into a better pavucontrol or whatever for pipewire audio.
bluetooth capabilities
onscreen volume adjustment notification.
volume control widget for waybar (show all audio devices, like wimdows, might need something like ewww)
Virtual Machine/Virtualization/Docker?
New Cursor for funsies
A better discord (no Electron perhaps??)
Bitwarden (CLI version wants nodejs-lts, yarn for nvim wants nodejs, figure out lazy.nvim without yarn?)

Configure:
Yazi
rEFInd boot loader
htop
fastfetch
Kitty and bash
neovim and plugins (also learn how to vim in the first place).
rofi-wayland
network manager (especially the applet for waybar)

Misc:
Set up secure boot (write about this in the post install doc)
Check boot times and trouble shoot using `systemd-analyze blame`


Learn:
Vim

