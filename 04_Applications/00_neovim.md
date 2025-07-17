# Neovim
[Neovim Arch Wiki Page](https://wiki.archlinux.org/title/Neovim)

## Installation
Run `sudo pacman -S neovim`.

Run Neovim by passing a file name or open its file manager by passing a directory name: `nvim filename`.

To set Neovim as the default editor for the user, open `~/.bashrc` or `~/.zshrc` depending on whichever shell you are using. Add the following lines to the end:
```
export EDITOR=nvim
export VISUAL=nvim
```
Run the following to reload: `source ~/.bashrc`.

## Plugin Setup
[lazy.nvim](https://lazy.folke.io)

We'll be using lazy.nvim as our plugin manager for Neovim. It is not from the official Arch repos or the AUR, so we'll have to manually update it occasionally (or perhaps set up a pacman hook?).

Follow the Installation steps on the documentation site for a Structured Setup. After that, we can start adding plugins to the spec tables.

We can pull the configuration and plugin files from the dotfiles repository.

## Plugin List
### Color Scheme
[catppuccin](https://deepwiki.com/catppuccin/nvim/1.1-installation-and-setup)

### Fuzzy Finder
[telescope](https://deepwiki.com/nvim-telescope/telescope.nvim)
^ Need to install and configure

### Live Markdown Preview
[iamcco](https://deepwiki.com/iamcco/markdown-preview.nvim/5-installation#using-lazynvim)
- Will need to install `nodejs` and `yarn` dependencies from official repositories.
- Copy the plugin spec for lazy.nvim from the repository.
- May need to `cd ~/.local/share/nvim/lazy/markdown-preview.nvim/app` and run `yarn install`.








Configure the init.lua as well (automatic tabbing when newline? automatic closed brackets?)
Actually learn how to use Vim
Go through the DeVries tutorial
Set up a pacman hook for automatic updates
