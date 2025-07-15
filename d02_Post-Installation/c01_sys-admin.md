# More on what to do after installation

Assuming you have a basic desktop environment setup, at least enough to open the Wiki on a browser.

### Installing an AUR helper

There are two options, yay and paru. yay is more fun to type and 3 characters long, paru has a bit better functionality.

Read through the AUR wiki page and AUR Helper Wiki page.

Make sure base-devel and git are installed.
git clone your desired AUR helper (I will be using paru):
```
git clone https://aur.archlinux.org/paru.git
cd paru
makepkg -si
```

I like to choose the rustup option, and if an error occurs, just run `rustup default stable`. 

Now you can use `paru -S` to install AUR packages, and `paru -Syu` to update all AUR packages (will also do the same as pacman -Syu so you don't have to run both)

### Setting up System Time
It's nice to have your system and hardware clock synced with the world's universal timer, and we do this by syncing our clocks everytime we access an internet network with NTP set up.

We'll be setting up NTP in this section. System Time Arch Wiki page is a good reference.

Before we do that though, if you are dual-booting Windows, you may notice your Windows clock going out of sync. This is because Windows is not based on UTC + timezone, it configures directly to timezone. Change it in your Windows settings. See section 4.1 in System Time Wiki page.

For time synchronization, we only want a single NTP client to run... otherwise they will overcorrect each other and cause great confusion. This includes Windows' NTP client if you are double booting. Windows' is apparently less accurate so it's recommended to turn it off.

We can have Network Manager change our timezone automatically when it detects a certain IP address. Use the script in 5.1.1, and don't forget to replace `up` with `connectivity-change` when using a VPN (which you should be!)

If you use a laptop that you bring with you everywhere, might be better to use Chrony, since it implements NTP. Otherwise, just use systemd-timesyncd for SNTP, it's perfectly fine and lightweight.

### Setting default text editor in Thunar

In order to set up using neovim or vim or nano (maybe) after double clicking a file in your file manager, first try using the GUI in the file manager to set the default editor.

If that doesn't work, do the following:
Create/edit the `~.local/share/applications/nvim.desktop` file.
Add the following to the file:
```
[Desktop Entry]
Name=Neovim
Exec=kitty nvim %F
Terminal=false
Type=Application
MimeType=text/plain;
```
And then use this command: `update-desktop-database ~/.local/share/applications`

You should be able to double click a md file or text file and open it in the editor.

### Setting up mirrorlist automatic updates

Paste this into /etc/xdg/reflector/reflector.conf:
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

Make sure the following tags are present in the service file for reflector:
```
[Unit]
...
Wants=network-online.target
After=network-online.target
...
```

We also need to enable the network wait service of the network manager; in our case, the Network Manager's services: `NetworkManager-wait-online.service`. If status shows disabled, enable it.

...... and I trolled you, using the service is actually not a great idea since it will run during boot and increase boot times. It's better to use the timer. It uses the configuration in the service file, so you didn't do wasted work. First disable the reflector.service, and then enable reflector.timer. It will start reflector.service once every week.

### Security

Read through the security pages on Wiki. Honestly, not much to do here, I'm not exactly running a highly sought after server.

Firewall is a decent one to take a look at though.

### Discord

I got bored so I'm talking about Discord now. Linux only supports Electron version, so it's the browser version of Discord. Just install discord normally using pacman.

Sometimes there is an update for Discord, but the Arch repo will not have the update yet. This prevents Discord from being used. Go to section 2.2 in Discord Arch wiki for fix.

### Fonts

For rendering foreign characters, install noto-fonts-cjk.
For rendering most emojis in browser, install noto-fonts-emoji.
For rendering emojis in discord channel names, install ttf-twemoji from AUR using yay or paru.

### System backup

You probably should do this, buy an external drive for regular system snapshots. I don't and I'm not too attached to this computer anyways so I won't bother for now.

You can make a pacman hook for keeping track of installed packages though, just read through section 2.5 on pacman Arch wiki page.

Make the hooks folder under /etc/pacman.d/ and then paste the text into a pkglist.hook file. This will create and update a pkglist.txt file under /etc/ everytime a package is installed or removed.
