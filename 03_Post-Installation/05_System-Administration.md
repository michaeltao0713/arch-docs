# System Administration

[General Recommendations](https://wiki.archlinux.org/title/General_recommendations#Graphical_user_interface)

This is a collection of things you should do to further set up your system after installation. We'll finally be following section 1 of General Recommendataions.

## Setting up System Time

[System Time](https://wiki.archlinux.org/title/System_time)\
[systemd-timesyncd](https://wiki.archlinux.org/title/Systemd-timesyncd)

It's nice to have your system and hardware clock synced with the world's universal timer, and we do this by syncing our clocks everytime we access an internet network with NTP set up.

Before we do that though, if you are dual-booting Windows, you may notice your Windows clock going out of sync. This is because Windows is not based on UTC + timezone, it configures directly to timezone. Change it in your Windows settings. See section 4.1 in System Time Wiki page.

For time synchronization, we only want a single NTP client to run... otherwise they will overcorrect each other and cause great confusion. This includes Windows' NTP client if you are double booting. Windows' is apparently less accurate so it's recommended to turn it off.

We can have Network Manager update our timezone value automatically when it detects a certain IP address. Use the script in 5.1.1, and don't forget to replace `up` with `connectivity-change` when using a VPN (which you should be!). Now when you travel to a different time zone, the system clock should automatically change.

If you use a laptop that you bring with you everywhere, might be better to use Chrony, since it implements NTP. Otherwise, just use systemd-timesyncd for SNTP, it's perfectly fine and lightweight.

Just run: `timedatectl set-ntp true`. You can check if it's on using `timedatectl status`.

## Security

[Security](https://wiki.archlinux.org/title/Security)

I highly recommend giving this page a read through, it shares tips on how to be more security conscious.

### Password Manager

It's a good idea to use a password manager to randomize passwords. Make sure you never use your master password for anything other than the password manager! I like bitwarden so it's the one I use.

### Firewall

I like to use `ufw` since it's easy to set up. On Arch, you would have to install `iptables-nft` and have it delete `iptables` as an anti-requisite. Then, install `ufw` and enable and start it using `systemctl`. After, run `sudo ufw enable`. You'll want to set:

```
sudo ufw default deny incoming
sudo ufw defautl allow outgoing
sudo ufw limit 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw allow 123
```

which will drop packets from all inbound traffic except for the SSH, HTTP, HTTPS and NTP ports respectively. This should be sufficient for a personal workstation setup.

You can check your ruleset by using `sudo ufw status`.

### SSH

You can enforce public key authentication on your SSH port. This is kinda overkill for me, but I'm putting it here in case I want to do this in the future.

## Service Management

Not much to do here, but do give a read through the `systemd` page and the `journal` page.

## System Maintenance

[System Maintenance](https://wiki.archlinux.org/title/System_maintenance)

I suggest giving this page a bookmark and coming back to it to refresh and go through the motions to maintaining your system. Ideally you set up a script for some of these steps as well.

### Setting up a dotfiles Repository

[Dotfiles](https://wiki.archlinux.org/title/Dotfiles)\
[My dotfiles](https://github.com/michaeltao0713/hyprland-dotfiles/tree/main)

We want to keep track of our app configurations so we won't have to make the same changes every time we set up a new system (or we break something). Most applications create and use hidden files in your home directory, or in the `.config` directory to store these configurations. We want to create a repository to track these files on Git Hub.

I already have a dotfiles repository, but let's go over making a repo (since I'm forgetful).

Create a dotfiles repo on GitHub and git clone to `~` directory as the `.dotfiles/` directory:

`git clone git_url ~/.dotfiles`

Set up SSH key authentication with GitHub if you haven't already (install `openssh` and refer to GitHub documentation)

We want the actual files to be located in the `.dotfiles/`, so cut and paste the original config file on your system to the `.dotfiles/` and then create a symlink like this:

`ln -s ~/.dotfiles/file_name ~/file_name`

or like this:

`ln -s ~/.dotfiles/.config/file_name ~/.config/file_name`

And of course, keep the git repo updated whenever you change the configs.

### System backup

[System Backup](https://wiki.archlinux.org/title/System_backup)\
[Backup Programs](https://wiki.archlinux.org/title/Synchronization_and_backup_programs)

It is recommended to make backups and automate the process of creating them. However, you'd need a seperate drive and this current workstation I'm using is fated to die soon.

Highly recommend you do set it up though, I definitely will in the future. You'll probably want `syncthing` for data synchronization, and `timeshift` for backups.
