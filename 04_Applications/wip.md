### Discord

I got bored so I'm talking about Discord now. Linux only supports Electron version, so it's the browser version of Discord. Just install discord normally using pacman.

Sometimes there is an update for Discord, but the Arch repo will not have the update yet. This prevents Discord from being used. Go to section 2.2 in Discord Arch wiki for fix.


### Fonts

For rendering foreign characters, install noto-fonts-cjk.
For rendering most emojis in browser, install noto-fonts-emoji.
For rendering emojis in discord channel names, install ttf-twemoji from AUR using yay or paru.



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

