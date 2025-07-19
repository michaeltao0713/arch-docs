# Setting Up

[General Recommendations](https://wiki.archlinux.org/title/General_recommendations)

So now we have a basic installation of Arch Linux. We'll want to set up some basic functionality to be able to actually use our computer. We'll be referencing the General Recommendations Wiki here, although we'll do a lot of skipping and hopping around.

## Connecting to the Internet

We'll want to run `systemctl enable NetworkManager` here so that your computer will be able to find a network to connect to on boot. If you currently aren't connected to the internet (check by running `ping google.com`), then you'll want to run `nmtui`, the Network Manager GUI for connecting.

## Adding your user to sudoers

This would fall under section 1.1 of the [General Recommendations](https://wiki.archlinux.org/title/General_recommendations) Wiki page.

Just type `EDITOR=nvim visudo` and replace nvim with your console text editor of choice. Search for wheel, and uncomment the line that allows users in group wheel to use sudo.

You can now sudo as your regular user for admin permissions. Test it out by installing a package as that user with `sudo pacman -S *package*`.

## Installing Drivers

[AMDGPU](https://wiki.archlinux.org/title/AMDGPU)\
[NVIDIA](https://wiki.archlinux.org/title/NVIDIA) 

We'll want a desktop environment up and running as soon as possible, so we'll first configure the drivers for our CPU and GPU(s).

For CPUs, as long as you installed the correct Microcode during pacstrap during the Arch install, you'll be good.

For GPUs, follow the [AMDGPU](https://wiki.archlinux.org/title/AMDGPU) and [NVIDIA](https://wiki.archlinux.org/title/NVIDIA) Wiki pages. I think Intel has a page too. My laptop had both a AMD and Nvidia GPU so I followed both. If you have a Nvidia GPU, I'm sorry. I do too. It is painful.

In summary for AMD GPU users, install `mesa` and `vulkan-radeon`. If you intend to play games from Steam (which is the best platform for games on linux right now), then you should also enable the `multilib` database in pacman and install `lib32-mesa` and `lib32-vulkan-radeon` to support 32-bit games.

*Sigh*, Nvidia is a pain. Find out which family your GPU belongs to and download either `nvidia`, or `nvidia-lts` depending on kernel version, or use `nvidia-dkms`. I'm using dkms currently which means also installing the kernel headers e.g. `linux-headers`. I had some trouble with nouveau being selected as the driver for the GPU later on, but can be fixed by configuring the boot loader to early load `nvidia-drm` during early boot. (In rEFInd, this means finding the options string and appending `nvidia-drm.modeset=1` to it. Do this a bit later though.

Install `lib32-nvidia-utils` and `nvidia-settings` as well.

Set up DRM kernel mode setting. I like to set it with `modprobe` for late kernel loading, as well as `mkinitcpio` and configuring directly in the boot loader for early loading.

Follow the steps in the WiKi for the modprobe and the mkinitcpio steps. For bootloader, it's dependent on which one you use. The steps for rEFInd is up above. If not using dkms, set up the pacman hook to remake the initramfs everytime nvidia updates.

Be sure to check the rest of the Wiki pages for AMD and NVIDIA past the install, everything I'm writing here only relates to an AMD iGPU + NVIDIA dGPU setup. You can also check out [NVIDIA/Tips and Tricks](https://wiki.archlinux.org/title/NVIDIA/Tips_and_tricks).

## Verifying Hardware Acceleration

[Hardware Video Acceleration](https://wiki.archlinux.org/title/Hardware_video_acceleration)

Read through the Wiki if you have a different set up, I have a Nvidia discrete GPU so I'll be verifying for VDPAU.

Install and run `vdpauinfo` and make sure it detectes your GPU and lists decoder capabilities. That's pretty much it. If not, check out the Configuration section.

## Monitoring CPU and GPU

`btop` for system CPU and RAM usage. Very pretty.

`nvtop` for GPU since it supports both AMD and Nvidia.

## Hybrid Graphics Configuration

[Hybrid Graphics](https://wiki.archlinux.org/title/Hybrid_graphics)\
[NVIDIA Optimus](https://wiki.archlinux.org/title/NVIDIA_Optimus)\
[PRIME](https://wiki.archlinux.org/title/PRIME)

I have a hybrid graphics setup, using an AMD iGPU + NVIDIA dGPU. Read NVIDIA Optimus if you are using NVIDIA's proprietary drivers and read PRIME if using AMD dGPUs or NVIDIA's open source Nouveau driver.

For Nvidia Optimus, you'd pretty much want to skip the sections on iGPU only or dGPU only.

Honestly, if you're using a desktop, it's not really a big deal, and since I'm using Hyprland, it's very easy to screw something up since Nvidia is not supported. So I'm not going to do anything here.

## What Next

We'll set up a basic desktop environment so you can do things like, use a browser, open multiple terminals, etc...
