# Pre-Installation

### Arch
Read the Arch Linux and the Frequently asked questions pages.

Topics of note in the Arch Linux page include systemd and initcpio with mkinitcpio under section 1.2 Modernity. The other topics are useful to read about as well, but systemd and initcpio are both things you will have to interact with relatively regularly. The pacman page is also something you should read. I'll give a brief summary here and maybe a more detailed explanation when we need to use them.

### Systemd
I highly recommend trying to understand what systemd is, and how to use it. Which means reading through the Wiki page and also the official project page. A summary of systemd is that it is the progenitor process on your OS. It will be the first thing that runs when you start up your computer. And this process will start all the other processes necessary to boot your computer and set up services (and sockets and a bunch of other stuff).

The reason why we need to interact with systemd is that sometimes we will need to start or enable a service we install. For example, after I install Arch, I may want a login screen instead of a terminal after boot. We can install a "Display Manager" (which are basically the login screens). When we reboot, we'll find that we will still be placed in the terminal and you have to start the Display Manager manually. If you want the login screen to start automatically, we would have to *enable* it using systemd, so that the Display Manager *service* is run everytime on boot.

Another example would be a network manager. When we boot up our computer, we ideally want to be automatically connected to a known WiFi connection. We have to use systemd to enable the network manager service so that it tries to find available connections on system boot.

After installing a package, you can use the following script to check for services provided by the package:
`pacman -Qql _package_ | grep -Fe .service -e .socket`
Should probably find behavior when the package installs dependencies.

### initramfs and mkinitcpio
initramfs is used to load kernel parameters and other stuff during early boot. So things like microcode updates will be done in early boot. If you have a Nvidia GPU (big mistake) then you'll need to use mkinitcpio to edit the initramfs. You can think of it as like, a checklist of things the kernel needs to do in the early stages of booting.

There are a couple of ways to edit your initramfs images, and mkinicpio is the default. You will be using this some amount of times, and it will be confusing everytime.

### pacman
pacman is like the Windows Store for Windows, if removing it didn't cause your apps to implode. This is how you download and install packages or programs for your system to run from the official Arch repositories. You can also use pacman to check for any updates to your installed packages.

Eventually you will need packages from off the official repositories, and in the Arch User Repositories (AUR). You either install them manually using mkpkg, or use an AUR helper (there is a good reason why we use this that we'll talk about later).

For now, just know that this will probably be the most run command during the early days of your Arch install.

### Frequently asked questions
I recommend reading at least the second article linked in section 3.2 to understand how Linux manages your memory, which will be very different from Windows (maybe not MacOS since it's UNIX based?)

### Preparing for Installation
And finally, to prepare for an Arch installation, I recommend pushing aside a few hours of free time to do the install (it is the most difficult distro for a reason). Also make sure you have a USB drive handy.
