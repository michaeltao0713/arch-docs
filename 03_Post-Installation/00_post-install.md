# Post Installation

We'll be following the General Recommendations Wiki here, it's incredibly expansive.
We'll also want to run `systemctl enable NetworkManager` here so that your computer will be able to find a network to connect to on boot.

### Adding your user to sudoers
Just type `EDITOR=nvim visudo` and replace nvim with your console text editor of choice. Search for wheel, and uncomment the line that allows users in group wheel to use sudo.

You can now sudo as your regular user for admin permissions. Test it out by installing a package as that user with `sudo pacman -S *package*`.

### Install drivers
Sike, we're not following the Wiki actually, we're going to get a desktop set up as quickly as possible so you can things like actually search up stuff on a browser and listen to music. To do this, we'll need drivers for our GPUs and CPUs to render the desktop environments well.

For CPUs, as long as you installed the correct Microcode during pacstrap during the Arch install, you'll be good.

For GPUs, follow the AMDGPU and NVIDIA Wiki pages. I think Intel has a page too. My laptop had both a AMD and Nvidia GPU so I followed both. If you have a Nvidia GPU, I'm sorry. I do too. It is painful.

In summary for AMD GPU users, install mesa and vulkan-radeon. If you intend to play games from Steam (which is the best platform for games on linux right now), then you should also enable the multilib database in pacman and install lib32-mesa and lib32-vulkan-radeon to support 32-bit games. (metal gear!!! i think).


In summary for Nvidia, ~kill yourself~. Find our which family your GPU belongs to and download either nvidia, nvidia-lts depending on kernel version, or use nvidia-dkms. I'm using dkms currently which means also installing the kernel headers e.g. `linux-headers`. Had some trouble with nouveau being selected as the driver for the GPU later on, but can be fixed by configuring the boot loader to early load nvidia-drm during early boot. (In rEFInd, this means finding the options string and appending `nvidia-drm.modeset=1` to it. Do this a bit later though.

Install lib32-nvidia-utils and nvidia-settings as well.

Set up DRM kernel mode setting. I like to set it with modprobe for late kernel loading, as well as mkinitcpio and configuring directly in the boot loader for early loading.

Follow the steps in the WiKi for the modprobe and the mkinitcpio steps. For bootloader, it's dependent on which one you use. The steps for rEFInd is up above. If not using dkms, set up the pacman hook to remake the initramfs everytime nvidia updates.

If you have a hybrid GPU setup, it's good to think about using nvidia optimus.

### Choose a desktop environment
Here's a hard choice, find a desktop environment. I recommend any that use Wayland, since it's newer and going to phase out xorg. Either you install a fully packaged DE like GNOME or KDE Plasma (I recommend plasma, it's cleaner, less bloated, and apparently GNOME is incredibly unoptimized). You could also take the option of using a minimal DE like Hyprland, which also is a Tiling DE. I implore you to check out how KDE and Hyprland look and feel before making your choice. r/unixporn is a great place to look for inspiration on how you want your DE to look.

I will be using Hyprland, which means I will also not have a lot of basic functionality installed. If you chose KDE or GNOME, you'll basically have a full system working. That is not the case for Hyprland or something similar like Sway. There will be a bunch of Hyprland specific guides now, that can be skipped if using a "normal" DE.

### Installing Hyprland
`sudo pacman -S hyprland`.
Also follow the nvidia setup guide and read through the master tutorial. Make sure to also install kitty, the terminal emulator. Skip the configuration for now, just install a browser (Vivaldi!) and other basic functionality like a file manager (thunar), application manager (rofi-wayland).

Follow the guides in the Hyprland folder for more.
