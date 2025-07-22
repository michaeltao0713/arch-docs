# To-Do List

## Ironically...

Install and configure a to-do list app. Options:

Planify:
Features



## Re-Installing Linux

~~Upload a list of essential packages from previous cycle.~~

~~Keep track of reference dotfile repos~~

~~Verify documentation repo is up to date.~~

~~Verify dotfiles repo is up to date.~~

Research CachyOS and decide if it's better than Arch for what I want.

Etch iso onto a USB drive (on windows probably)

Install Linux

Go through my own documentation and set up basic functionality.

Go through the Wiki and continue setting things up.



## Install and Configure

REMEMBER, UNLESS IT'S MEGA IMPORTANT, CONFIGURE WHAT YOU INSTALL. OR ELSE YOU'LL HAVE ONE TRILLION TERRIBLE DEFAULT APPS AND HAVE TO CONFIGURE EVERYTHING AT ONCE. Don't forget to take your time and enjoy the ride.

##### File Manager

GUI options only (unfortunate)
Thunar (GTK)
Dolphin (QT I think)
yazi (cool, but was a pain)

##### VSCode

VSCode
VSCodium

- set up copilot
- actually configure the thing

##### Notification Daemon

dunst (basically make your own)
mako (basically make your own)
swaync (beefier and GTK (bad) but has built in notification control panel/history)

##### Status Bar

Waybar (easy, temp solution?)
- Install a widget system
- Extensions for waybar would be:
- workspaces https://github.com/Alexays/Waybar/wiki/Module:-Hyprland
- applets (NM, discord, pavucontrol)
Quickshell (create your own widgets, pain, time consuming, could look so good)
Ewww
AGS

##### Discord

Discord (telemetry, old Electron)
Vesktop (auto install vencord, cool themes, popular)

##### QT Apps Themeing

qt6ct, qt5ct, kvantum
- Choose a system theme (Catppuccin Mocha Mauve)

##### GTK Apps Themeing

nwg-look
- choose a system theme
- need environment variables from the hyrpland wiki

##### Archive Manager

Just use tarball? (painful)
7zip
...

##### Screenshot Tool

Hyprshot (if using hyprland)
Flameshot
...

##### Image Viewer

...

##### Video Viewer

VLC
...

##### Bluetooth Manager

...

##### Network Manager (better looking than NM please, also an applet/widget for status bar?)

Network Manager
systemd-networkd
Make your own widget (specifically for interfacing with the network manager)
...

##### Volume Control Panel

pavucontrol
pwvucontrol
Make your own widget with quickshell?
...

##### On Screen Display (for volume change, brightness change, capslock, etc.)

swayOSD
Make your own widget?
...

##### Virtualization

Virtual Box (I used this on Windows)
Docker (Containers instead of VM)
...

##### Password Manager

Bitwarden (ugly)
Bitwarden CLI (needs nodejs-lts version, conflicts) (makes life hard)




## Configuration

##### Idle and Sleep

Hypridle:
- timings

Hyprlock:
- Aesthetic

##### Bootloader

rEFInd:
Secure Boot
looks

##### App Launcher

rofi-wayland:
make it look better

##### Btop

idk, it kinda already looks good. see what options there are

##### Fastfetch

Funky Icons (nerd font?)
images

##### Terminal

oh my posh would be nice i think,
make kitty look good, (translucent?)
aliasing even?

## Other

Find some good wallpapers
va11halla live wallpaper?
https://github.com/D3Ext/aesthetic-wallpapers/tree/main




## Far Future

Check boot times and trouble shoot using `systemd-analyze blame`

Set up wallpaper switch script? Use Hyprpaper? idk, does it use rofi? reference Ari's dotfiles

Figure this out https://wiki.hypr.land/Useful-Utilities/Screen-Sharing/
Read through hyprland wiki again for things I missed

Install Neovim and ACTUALLY LEARN how to use it. Install some plugins, configure it, and document the journey.
- Possibly write a pacman hook that will run the plugin manager's update alongside system update.
