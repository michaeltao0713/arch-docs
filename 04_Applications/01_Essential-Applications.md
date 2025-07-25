# Essential Applications

This page will go over some applications you'll want to get more basic functionality. You probably can't control sound right now.

## Sound

[ALSA](https://wiki.archlinux.org/title/Advanced_Linux_Sound_Architecture)\
[Sound System](https://wiki.archlinux.org/title/Sound_system)

Follow the Advanced Linux Sound Architecture (ALSA) wiki page. Although, the most important content is in Section 1, as we'll be using `pipewire` as a sound server to handle everything else.

ALSA should have already been installed with the linux kernel. If you're on laptop and can't hear sound, install `sof-firmware`.

For initial audio management, install `alsa-utils` and run `alsamixer`. You don't really need this step at all though.

### Sound Manager GUI (PipeWire)

You'll probably want a GUI for switching audio devices and changing volume and muting applications quickly. Check out the [Sound System](https://wiki.archlinux.org/title/Sound_system) wiki for Sound Server options.

I will be using PipeWire. It's newer and aims to replace JACK and PulseAudio which were the previous favorites. Since I'm going to using Hyrpland, it also recommends using Pipewire with Wireplumber session manager. PipeWire is also used for screensharing.

Install `pipewire` and `wireplumber`. Again, if you're using Steam, good idea to install `lib32-pipewire` too. Also install `pipewire-pulse`, `pipewire-alsa` and `pipewire-jack` so that PipeWire can run for applications reliant on PulseAudio, ALSA and JACK respectively.

Wireplumber is a session manager that allows PipeWire to watch for new streams and connect. It is the recommended session manager.

Consider a GUI as well, for volume sliders and ability to mute certain sources of sound. I'm using `pavucontrol`, but I might switch it out later since it doesn't look very good... 

### Configuration

Not much, you can configure default devices in the pavucontrol menu by opening it via terminal or application manager. Your volume control macros should also work automatically.

## Browser

You should've already downloaded one and started using it. Just set it up how you would any browser. Not much to say here.

## Setting up a File Manager

You'll want to pick a file manager. Thunar is a decent option for a GUI file manager. I chose to use `yazi` which is a CLI file manager. Honestly, I don't recommend this, it's a lot of work and has compatability issues with trying to download files on browsers and other apps.

### TUI Default File Manager

If you like pain and decided to use a TUI file manager, you'll want to do these extra steps so that Discord or your browser can use your TUI for downloading and uploading files.

From the AUR, install `xdg-desktop-portal-termfilechooser-hunkyburrito-git` using `paru` or `yay`. This allows you to specify a terminal-based file manager as the system default file manager so that applications like the browser or discord can open it for uploading files.

There is a default `config` file in either `/usr/local/share/xdg-desktop-portal-termfilechooser/` or `/usr/share/xdg-desktop-portal-termfilechooser/`. In my case, it was the latter. Copy the `config` file to your `~/.config/xdg-desktop-portal-termfilechooser/` folder and make sure the correct wrapper script is run for your chosen file manager (in my case, `yazi`).

Do a quick `systemctl restart xdg-desktop-portal` and you should be good. I still don't really recommend this, as your browser's "Show in File Manager" button won't work. I think it's because it's not opening `yazi` in either download mode, or upload mode, so it self-destructs.

## File Editor

I suggest using Visual Studio Code, but you can use Neovim if you're just built like that. [Setting up VSCode](App-Setups/01_Visual-Studio-Code.md). Set it as your default file editor in a GUI File Manager by right clicking on a file you want to edit and setting VSCode (or whatever you want) as the default.

## Discord/Vesktop

Check out [this](App-Setups/03_Discord.md).

## Steam

Check out [this](App-Setups/04a_Steam.md).