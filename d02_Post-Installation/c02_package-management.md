# Package Management Post-Install

This will be about managing packages with pacman and AUR, which you should have done quite a bit already in previous chapters.

### Arch Linux Updates

It's recommended to sign up for the Arch Linux mailing list. They send out updates if manual intervention is required for a recent pacman update (and at the time of writing, a manual intervention notice went out last week!). Sign up here: https://lists.archlinux.org/mailman3/lists/arch-announce.lists.archlinux.org/ and follow further instructions.

### Useful pacman commands

Update all packages: `sudo pacman -Syu`
Update all packages (including AUR): `paru -Syu`
Remove a package (Removes unneeded dependencies and config files): `sudo pacman -Rns *package_name*
Check for orphaned dependencies: `pacman -Qtd`
Check for services and sockets given by a package: `pacman -Qql *package_name* | grep -Fe .service -e .socket`

### Cleaning package cache

We want to periodically clean the package cache directory, as it can grow in size indefinitely. It will be fine just to install the pacman-contrib package, and enable paccache.timer which will start the paccache service once a week.

You can edit the `/etc/conf.d/pacman-contrib` file to add arguments to the paccache service run. Should be fine to leave as is.

### Configuring pacman

The configuration file for pacman is located at `/etc/pacman.conf`.

You can uncomment `#Color` to allow colors in pacman outputs.

You can uncomment `#VerbosePkgLists` to see old and new versions of available packages.

I've done the above to my pacman.

Now we move on to the pacman/Tips and Tricks Wiki page.

### Tips and Tricks


