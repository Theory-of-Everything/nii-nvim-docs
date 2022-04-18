### Understanding the init.lua

The init.lua file in the root directory of nii-nvim is going to be the basic entry-point for basic modifications of the default configuration.
Most of the core modules are loaded in the init.lua file, along with setting initialization and theme setting.

In general, the init will usually have all of the relevant `require()`s and reference the `scheme` library for theme setting.
Generally, you probably won't want to be adding code in the init file, as its main purpose is to require any needed modules for startup.
However, quick code testing here might prove useful, as you don't need to keep track of a extra file and require.

### Adding New Plugins

Adding in plugins is a trivial task, however, this base configuration has some basic organization rules that (I would hope) that you would replicate
If you want to add a plugin, these are the basic steps that nii-nvim takes.

Plugins to install with packer are defined in the `lua/plug.lua` file so add your plug to the file. (In this case we will be installing [presence.nvim](https://github.com/andweeb/presence.nvim))

```lua
return require('packer').startup(function(use)
...
    use {'andweeb/presence.nvim'}
...
end)
```

Next you will want to create the configuration file for initialization of the plugin.

-   Plugin config files are made in the `lua/config/` directory.
-   Make a file `lua/config/presence.lua` ndn write all the code for the plugin to startup as desired.
-   Lastly, require the file in the `init.lua`

```lua
...
require('config.presence')
...
```

### Changing Keybinds

If you want to change or add custom keybinds for nvim, all keybinds are defined in the file `lua/keymap.lua`.

To add a custom keybind, insert the following into `keymap.lua`
(for example we will make a keybind that replaces all `"` with `'`)

```lua
...
-- map() is a wrapper function for setting keybinds with nvim's lua api
-- Arg1 specifies the mode of the keybind (similar to imap, nmap, etc.)
-- Arg2 is the actual keybind
-- Arg3 is the command to execute
-- Arg4 is for aany extra options (noremap and silent are true by default)
-- you can also pass in an empty table or the opt var if you don't want any options.

map("n", "<leader>s", ":%s/\"/\'/g\'", opts)
...
```

### Custom Colorschemes

#### Changing the colorscheme

By default, nii-nvim (should) be using the onedark colorscheme for both nvim and lualine, however, if you want to change the theme, you can do that pretty easily in your `init.lua` there should be a line:

```
scheme.load_shared_scheme('onedark')
```

This is the code that sets the colorscheme configuration for both nvim and lualine.
There are a multitude of popular themes included with nii-nvim, with a complete list being:
**Text Editor:**

-   Ondark
-   Nord
-   Monokai
-   Gruvbox
-   Everforest
-   Bluewery
-   Night Owl

**Lualine:**

-   Ondark
-   Nord
-   Monokai
-   Gruvbox
-   Everforest
-   Bluewery
-   Night Owl
-   MinimalDark
-   Custom (Boilerplate code)

To define a separate text editor theme and lualine theme, you can use the following:

```lua
scheme.load_scheme('Nord')
scheme.load_lualine_scheme('minimaldark')
```

#### Adding Colorschemes

nii-nvim handles colorschemes in a different manner than most normal configurations, as loading is handled by the scheme module. All theme loading files are defined in `lua/themes/`. To add a theme (whether installed via plugin or custom) crate a file in the themes folder, then add all required code for the theme so load:

**Sample: (Gruvbox)**

```lua
-- File in lua/themes/gruvbox.lua
vim.opt.termguicolors = true
vim.cmd('colorscheme gruvbox')
-- EOF
```

You can also create custom statusline themes by taking the boilerplate code in `lua/themes/lualine/custom.lua` and create your own statusline theme.

-   **NOTE:** The scheme loading functions directly depend on the filename, so when specifying a theme, make sure that you use the filename when you use scheme functions.
