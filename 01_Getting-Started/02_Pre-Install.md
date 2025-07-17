# Pre-Installation

This is a collection of background information that you should at least skim through to understand (even just a little) about how Arch and Linux in general works under the hood. Most of this information is taken from the Arch Wiki.

Some important topics to familiarize yourself would include *systemd* and *mkinitcpio*. You will likely have to interact with these throughout your time using Arch.

## Systemd

[systemd](https://wiki.archlinux.org/title/Systemd)

I highly recommend reading and understanding what *systemd* does. In summary, it is the first process that runs on your computer during boot and will either directly or indirectly start all other processes. It allows us to specify which apps we want run on boot. It also allows us to set schedules for certain other apps to run perhaps once a week. This is incredibly powerful for automating your system (and preventing the need for us to manually connect to the internet everytime we boot). Give the Wiki a quick read, and try to remember some of the commands, we'll definitely be using them soon.

Some uses of *systemd* include starting a Display Manager on boot so that we can log in to our system, refreshing the pacman mirrorlist weekly, regularly synchronizing the system time using the SNTP protocol, etc...

We can check whether a package we install has services or sockets that can be run by using the following command:\
`pacman -Qql package_name | grep -Fe .service -e .socket`

## initramfs and mkinitcpio

[initramfs](https://wiki.archlinux.org/title/Arch_boot_process#initramfs)\
[mkinitcpio](https://wiki.archlinux.org/title/Mkinitcpio)

*initramfs* is used to load kernel parameters and other stuff during early boot. So things like microcode updates for your CPU will be done in early boot. If you have a Nvidia GPU (big mistake) then you'll need to use *mkinitcpio* to edit the *initramfs*. You can think of it as like, a checklist of things the kernel needs to do in the early stages of booting.

There are a couple of ways to edit your *initramfs* images, and *mkinicpio* is the default. You will be using this a couple of times, and it will be confusing everytime.

## pacman

[pacman](https://wiki.archlinux.org/title/Pacman)

To install new applications on our Arch Linux system, we use a package manager called *pacman*. We use *pacman* to install new packages and update installed packages from the official Arch repositories. There will be a more robust page on *pacman* and configuring it after we install Arch.

While the official repositories are great, you will eventually need packages from the [Arch User Repositories (AUR)](https://aur.archlinux.org). These packages cannot be installed using *pacman*, so we'll need an AUR helper later on.

## Other

[Frequently Asked Questions](https://wiki.archlinux.org/title/Frequently_asked_questions)

I recommend at least skimming through the second article linked in section 3.2 to understand how Linux manages your memory, which will be very different from Windows (maybe not MacOS since it's UNIX based?)

## Preparing for Installation

[Arch Installation Guide](https://wiki.archlinux.org/title/Installation_guide)

You are now almost ready to install Arch Linux! Set aside a few hours (as it can get confusing) for the install itself, and prepare a USB flash drive with the Arch Linux iso file. You can read section 1.1 through 1.3 in the [Arch Installation Guide](https://wiki.archlinux.org/title/Installation_guide) for steps to do this. I find Balena Etcher to be the most straight-forward way to do this step.
