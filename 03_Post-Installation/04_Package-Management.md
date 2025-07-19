# Package Management

[General Recommendations](https://wiki.archlinux.org/title/General_recommendations#Graphical_user_interface)

We'll be skipping over System Administration once again, to set up pacman. This is section 2 of [General Recommendations](https://wiki.archlinux.org/title/General_recommendations#Graphical_user_interface).

## Installing an AUR helper

[Arch User Repository](https://wiki.archlinux.org/title/Arch_User_Repository)\
[AUR Helpers](https://wiki.archlinux.org/title/AUR_helpers)

`pacman` allows us to install packages from the official Arch Repositories and while the repos are very expansive, there will be packages you want created by other user. Thankfully, Arch has the Arch User Repository (AUR) which holds packages made by other users. Bit of a warning, only install packages you trust. As an indicator, you can check the number of votes a package has received on the AUR website. Popular packages can eventually be transfered to the official repositories.

While we could manually install these packages using `makepkg` and `pacman`, we'd have to manually update each package one by one, which can be very annoying the more packages we have. We want to install these packages and still be able to automatically update all of them with something similar to `pacman`'s `sudo pacman -Syu` command.

The solution is to use an AUR helper. They provide the same functionality as `pacman` but allow the installation of packages from the AUR. There are two options, `yay` and `paru`. `yay` is shorter to type and more fun! `paru` is a bit faster (written in rust) and makes you go through extra steps in an effort to make sure you want what you are installing. I chose to use `paru`.

I recommend at least skimming through the two Wiki pages linked above. Then we can continue with the installation.

Make sure `base-devel` and `git` are installed. `git clone` your desired AUR helper:

```
git clone https://aur.archlinux.org/paru.git
cd paru
makepkg -si
```

I like to choose the `rustup` option, and if an error occurs, just run `rustup default stable`. 

Now you can use `paru -S` to install AUR packages, and `paru -Syu` to update all AUR packages (will also run `pacman -Syu` so you don't need to do both). The helper will also be able to update itself.

## Arch Linux Updates

It's recommended to sign up for the Arch Linux mailing list. They send out updates if manual intervention is required for a recent pacman update (and at the time of writing, a manual intervention notice went out last week!). Sign up [here](https://lists.archlinux.org/mailman3/lists/arch-announce.lists.archlinux.org/) and follow further instructions.

## Useful pacman commands

[pacman](https://wiki.archlinux.org/title/Pacman)

Update all packages: `sudo pacman -Syu`\
Update all packages (including AUR): `paru -Syu`\
List all installed packages: `pacman -Q`\
List all explicitly installed packages: `pacman -Qe`\
List all installed packages with regex: `pacman -Qs regex`\
Remove a package (Removes unneeded dependencies and config files): `sudo pacman -Rns package`\
Check for orphaned dependencies: `pacman -Qtd`\
Check for services and sockets given by a package: `pacman -Qql *package_name* | grep -Fe .service -e .socket`\
Find the dependencies of a package (need to install `pacman-contrib`): `pactree package`

## Cleaning package cache

We want to periodically clean the package cache directory, as it can grow in size indefinitely. It will be fine just to install the `pacman-contrib` package, and enable `paccache.timer` which will start the paccache service once a week.

You can edit the `/etc/conf.d/pacman-contrib` file to add arguments to the paccache service run. Should be fine to leave as is.

## Configuring pacman

The configuration file for pacman is located at `/etc/pacman.conf`.

You can uncomment `#Color` to allow colors in pacman outputs.

You can uncomment `#VerbosePkgLists` to see old and new versions of available packages.

I've done the above to my pacman.

## List of Installed Packages

We can keep an automatically updating list of installated packages by using a pacman hook. Create the following file in `/etc/pacman.d/hooks/` called `pkglist.hook`:

```
[Trigger]
Operation = Install
Operation = Remove
Type = Package
Target = *

[Action]
When = PostTransaction
Exec = /bin/sh -c '/usr/bin/pacman -Qqe > /etc/pkglist.txt'
```

## Automatically Updating Mirrorlist

[Mirrors](https://wiki.archlinux.org/title/Mirrors)\
[Reflector](https://wiki.archlinux.org/title/Reflector)

Packages we download are from the mirrors, we'd want a list of mirrors that are fast, stable, and work. Mirror availability changes often, so we want a list that automatically updates regularly. We'll reflector for this.

Install `reflector` and paste this into `/etc/xdg/reflector/reflector.conf`:
```
# Set the output path where the mirrorlist will be saved (--save).
--save /etc/pacman.d/mirrorlist

# Select the transfer protocol (--protocol).
--protocol https

# Select the country (--country).
# Consult the list of available countries with "reflector --list-countries" and
# select the countries nearest to you or the ones that you trust. For example:
--country 'Canada,United States,France,Germany,'

# Use only the  most recently synchronized mirrors (--latest).
--latest 20

# Sort the mirrors by synchronization time (--sort).
--sort rate

# Use only mirrors synchronized within age amount of hours (--age).
# --age 24
```

Make sure the following tags are present in the service file for `reflector`:

```
[Unit]
...
Wants=network-online.target
After=network-online.target
...
```

We also need to enable the network wait service of the network manager; in our case, the Network Manager's services: `NetworkManager-wait-online.service`. If status shows disabled, enable it.

Finally, enable `reflector.timer`. It will start `reflector.service` once every week.
