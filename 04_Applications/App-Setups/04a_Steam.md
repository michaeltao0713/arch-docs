# Steam

[Steam](https://wiki.archlinux.org/title/Steam)

We'll go over installing Steam, setting a proton to use for games, and maybe also how to use Steam proton to launch non-Steam Games.

## Installation

You should have most if not all of the packages already installed.

Just install `steam` from the official repos. As always, follow the Arch Wiki and read through all of it. Good idea to check out the "Gaming" Wiki page too.

I recommend running `steam` in a terminal and if it doesn't work, reboot and try again.

If you run into specific font not rendering correctly, then you might need to install either `ttf-liberation` or a package from the Microsoft Fonts Wiki page. (I haven't run into this problem *yet*).

Not a part of the installation process, but a good idea to bookmark ProtonDB to check for linux compatibility on games.

## Proton

You will need proton to play most games on steam, it allows you to play Windows-only games on Linux.

Go to `Steam > Settings > Compatibility` and enable Steam Play for all titles. Then, choose a version of Proton to use. This might have to be changed depending on the game.

Might be better to use Proton GE, a fork of Steam's official proton with more support and maintained by Glorius Eggroll. Install via the git repository or the AUR custom bin. Make sure the check out the docs in the git repo, install driver packages and whatnot.

I'm going to install via the AUR so that paru will auto update it when it can. Simply install `proton-ge-custom-bin`. Restart Steam completely, and then you can set Proton GE in the compatibility options.

I recommend checking ProtonDB for every new game you want to play, and forcing the game to run on the version of proton people say worked best for them. For example, Limbus Company seems to work flawlessly on Proton GE, so I can go to Limbus Company properties and force it to use Proton GE.

Also take the time to see other people's launch options, some may need to be set for each game. Don't forget to add `%command%` after the launch options, or else the game won't start.

## Performance Overlay

Steam has a neat overlay you can turn on to see FPS and other stats. `Steam > Settings > In Game` and turn on Overlay Performance Monitor.

## Recording

Turn this on if you want to clip game moments. `Steam > Settings > Game Recording` and turn on Record in Background. I like to remove the `Ctrl+F11` keybind from "Start/stop saving a clip" and bind it to "Save the last __ seconds of gameplay as a clip". I usually use 60 seconds.

I also like to adjust the length of recorded background footage to 40 minutes instead of 120 (who needs that many amiright?). Can also toggle "Record Microphone".
