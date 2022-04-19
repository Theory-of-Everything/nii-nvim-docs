## Installation Prequisites:

-   Neovim 
-   FZF
-   ripgrep
-   Python 3
-   Git
-   A Nerdfont

## Migration of older nii-nvim versions

If you are currently tracking changes from the `master` branch,
please check out the [Migration guide](https://docs.theoryware.net/nii-nvim/migration-branch/).

## Manual Install

First install [packer.nvim](https://github.com/wbthomason/packer.nvim)

```bash
git clone --depth 1 https://github.com/wbthomason/packer.nvim\
 ~/.local/share/nvim/site/pack/packer/start/packer.nvim
```

Next, you'll want to clone the repository into your `~/.config/` folder and
replace the nested `nvim/` dir

```bash
cd ~/.config/
mv ./nvim ./nvim.old
git clone https://git.sr.ht/~theorytoe/nii-nvim ./nvim
cd ./nvim
git checkout main
nvim +PackerInstall
```

Now you should be good to go, to update plugins to the latest run this command
in nvim

```
:PackerSync
```

Now nii-nvim should be installed to pull the latest updates (note, these aren't
always "stable"), run this in your config directory: If you have local changes,
you will want to stash changes, pull from remote, then pop stashed changes

```bash
git stash
git pull
git pop
```

Otherwise (no local changes):

```bash
git pull
```

## Post-Install

### Installing sumnkeo lua language server

If you haven't already, make sure that nii-nvim is on the latest commit. They
you will want to run nvim. Behind the scenes, nvim will check for (and create if
not present) a directory in `~/.local/share/nvim/lspservers`. This is where you
can install & manage lsp servers (with the added benefit of this directory being
easily accessible with the nvim lua runtime).

- To install the lua language server, clone the repo and follow build instructions.

```bash
git clone https://github.com/sumneko/lua-language-server ~/.local/share/nvim/lspservers/lua-language-server
# and do all of the build instructions required to have a binary
```

- The lsp config files in nii-nvim should do the rest of the heavy lifting for you.

### Neoformat formatters

Neoformat doesn't format buffers, but acts as a wrapper for various formatting
tools. You can refer to a list of formatters for various languages
[here](https://github.com/sbdchd/neoformat#supported-filetypes) You can
generally install these formatters with your system's package manager.

## Script Install

Currently a work in progress
