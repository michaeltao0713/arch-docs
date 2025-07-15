# Installation
Again, you will need to follow the Wiki steps for installation yourself. I will just add some footnotes for explanation of confusing steps and reasons for why we do some of the things we do.

I am qualified because I've installed Arch like 5 times now (not as good as the guy who sped ran Arch Install in just over a minute).

Also, I installed on an x86_64 system with UEFI, a lot of the things I mention here will be very different if you are using a BIOS system, and you'll need to pay more attention to the official documentation.

### Section 1.1 to 1.4
Not much to say here, I downloaded from a worldwide mirror, so I did the verify signature steps (I recommend following a video for the verification because I still don't know what I did).

For actually flashing the drive, I used Balena Etcher to flash the ISO to a USB (need at least like, 2 GB I think).

Secure boot can be turned off in your BIOS settings which can be accessed by rebooting your computer and mashing f2 (might be the delete key on your system).

Reboot your system and go to BIOS, and change boot settings so that you boot from the USB.

### Section 1.5 to 1.8
If you use a standard qwerty keyboard, use `us` for your keymap.

You can use the `setfont ter-132b` command if the terminal text is too small. It will not affect your Arch system.

If on Ethernet, just ping google.com or smth. If on WiFi, click into the iwctl page and follow the steps there, it's pretty straightforward. Ignore the part about systemd-networkd and systemd-resolved, we will be using Network Manager for those purposes instead. You can also ignore the part about systemd-timesyncd, we'll talk about it when we set up time synchronization after the install.
### Section 1.9
This the part where you can nuke drives that are loaded on your computer. Be careful with setting up the partition, and read through the fdisk page carefully on how to use it.

We want to create partitions on our storage drive for different uses. For most, there will be three partition types. Boot, which will contain the Linux kernel and the bootloader for starting your computer; Root, which will contain the main file system with all your files and programs; and Swap Space, which is used for virtual memory (you can think of this as magically making your RAM larger).

The boot partition should be allocated around 1 to 2 GiB (gibibytes, using the 'G' character means gibibytes in fdisk). Swap space is determined by how much RAM you have. Since this is where your RAM contents will be copied to during hibernation, it should be at least as large as your RAM. I've seen different conventions for allocating this space. I believe Windows allocates 22GB for a 16GB RAM system. I myself allocated 20 GB. Some people suggest 1.5 times your RAM. Honestly, just choose a number, you can edit it later probably.

Use t to choose the typing for your partitions. EFI system for boot, Linux swap for swap space, and Linux root (x86_64) for root.

### Section 1.10 to 1.11
Honestly, if you have a UEFI system, you can just follow the steps directly.
### Section 2.1
The mirrorlist will be the source of all the packages you download, and they vary in speed and stability depending on the source and its relative location to you. Ideally, we want a list of mirrors that are fast, stable, and in sync with the updates to the repositories. We can do this initially in 2.1, and then set up an automated way of sorting and refreshing this list after the install.

2.1 is an optional step, and we'll be overwriting our changes here after we make our full install, but it's a good idea to try it out anyways. Click into the "mirror servers" link and follow section 3.1.1. It is crucial to run `pacman -S pacman-contrib` before attempting to copy the mirrorlist to a backup (do it before the line of code with cp at the start). Otherwise, when you run the rankmirrors script later, it'll overwrite your mirrorlist file with a new line and it will become empty.

Run those two commands and you'll be good.
### Section 2.2
Another important section that requires a lot of research and reading. This step is for installing some packages for your new system so that you can actually do something when you change root into it. If you ran pacstrap without reading the second half of this section, you can run pacstrap again, it'll be fine.

I recommend you read through each of those bullet points and decide for yourself what you'll need for your system. I'll go through what I installed.

Microcode: Install the one for your CPU; either amd-ucode or intel-ucode. This is for updating your CPU automatically on boot.
sof-firmware: This is for audio drivers, I didn't install it initially, but it will be a dependency for packages later on most likely, so you'll end up installing it later anyways. If you find that you can't hear audio on your new install, try installing this first to see if it fixes.
Networks: Install a network manager; I recommend NetworkManager, it's easy to use and supports basically all the uses of a network manager.
Text Editor: Install either nano or vim or neovim, depending on what you're comfortable with.
Other: man-db, man-pages for manual pages for your commands
My Extras: sudo, so you can allow your user to run with admin permissions

Run pacstrap and it'll take a couple minutes probably

### Section 3
Just follow the steps here. If you're going to use the rEFInd boot loader, I recommend taking a picture of the output of `cat /mnt/etc/fstab`. If you don't know what bootloader to use, I suggest just taking the picture anyways.

`arch-chroot /mnt` will change root into your new installation. So now, you're interfacing with your new Linux install directly. 

If you live in Toronto, I recommend using Region = America and City = Toronto. This will allow for daylight savings to be applied automatically.

We can do the time synchronization later.

Localization is for how you want your dates and times to be displayed. Always uncomment `en_US.UTF-8`, and you can uncomment any other that you'd want. I uncommented `en_CA.UTF-8` as well. And then you run `locale-gen`.

Set LANG="whatever locale you uncommented"
Set KEYMAP="us" if you have a standard qwerty keyboard, or whatever you selected earlier in the install.

Create a hostname for your computer, it can whatever you want; I chose arch-legion since I installed Arch on my Lenovo Legion laptop.

You can skip the initramfs step, since mkinitcpio has already generated the initramfs image for during pacstrap.

Set a root password. Make it strong, it will *not* be your normal user password.

### Extra step before boot loader
Let's create a new user before we finish off installation. Use the command:
`useradd -m -G wheel -s /usr/bin/bash name`
replacing *name* with your desired name for your user.

wheel is the name of the group of users that will be granted permission to use sudo, to run things as the administrator. For example on windows, you can let certain users run things as admin, and restrict other users to not allow them. Adding a user to the wheel group is the same as granting them that permission.

### Installing a bootloader
Please do not reboot until you finish this entire section. It's easy to miss a step here. Click into the boot loader page and take a look through the options. There's pretty much four main options for a UEFI system and I'll break them down for you.

GRUB is the classic, oldie but works like a charm default boot loader. It just works, and you can do some customization to make it look like the Minecraft main menu screen. I did have the problem where it would not recognize my Windows system on a second SSD drive however, which is why I switched from GRUB to a different boot loader.

systemd-boot is from systemd (I hope you read a bit about it earlier). This one has minimal configuration since it's just a really simple process. I haven't tried this one yet, but apparently it should be able to recognize other OSes on other drives.

EFI boot stub: basically, no boot loader, I don't really know how this one work to be honest. You should read more about it. Not a very popular option.

Finally, rEFInd. This is the boot loader I use. Honestly, it's not much different from GRUB, other than being a bit more customizable, and being able to detect my Windows system without any other configuration. The installation of rEFInd during the installation of Arch is a bit tedious though.

Whichever boot loader you choose, you must install it first before rebooting. First, you run `pacman -S boot_loader_name`, and then you check the bootloader's page for further installation steps.

For rEFInd, it's kind of complicated, so I'll break it down. After running pacman, run `refind-install`, and then use your console editor to edit the /boot/refind_linux.conf file. You will want to delete everything in that file, and write something like:
`"Boot using defautl options"	"root=UUID=XXXXXXXXX rw"`
where UUID is from the fstab file I told you to take a picture of earlier. You will want the UUID of the root partition specifically.

I encourage to read all of the related pages so that you actually know what you are doing and can verify whether my steps are correct or not.

Once that's all done, you can type exit to exit the change root system, and then optionally unmount all your partitions. Then, typr reboot to boot into your new Arch system.

yippeee

