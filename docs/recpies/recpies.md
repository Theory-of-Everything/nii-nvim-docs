# Recipes

Recipes are curated sets of configuration snippets to add extra functionality to nii-nvim.

If you want to contribute a recipe, consider sending a patch or pull request.

## Traditional-looking tabs

```lua
use({
	'kdheepak/tabline.nvim',
	config = function()
		require('tabline').setup({
			-- Defaults configuration options
			enable = true,
			options = {
				-- If lualine is installed tabline will use separators configured in lualine by default.
				-- These options can be used to override those settings.
				section_separators = {'', ''},
				component_separators = {'', ''},
				max_bufferline_percent = 66, -- set to nil by default, and it uses vim.o.columns * 2/3
				show_tabs_always = false, -- this shows tabs only when there are more than one tab or if the first tab is named
				show_devicons = true, -- this shows devicons in buffer section
				show_bufnr = false, -- this appends [bufnr] to buffer section,
				show_filename_only = true, -- shows base filename only instead of relative path in filename
			},
		})
	end,
	requires = { { 'hoob3rt/lualine.nvim', opt = true }, { 'kyazdani42/nvim-web-devicons', opt = true } },
})
```

## Go LSP sever

(Make sure you have the `gopls` binary installed on your system)

Create a new file in the `lua/config/lsp/go_lsp.lua` directory

```lua
local lspconfig = require('lspconfig')
lspconfig.gopls.setup({
    cmd = { 'gopls', 'serve' },
    filtypes = { 'go', 'go.mod' },
})
```

In lsp/init.lua

```
return {
    -- ...
    require(config.lsp.go_lsp')
    -- ...
}
```

## Python Lsp server

New file `lua/config/lsp/python_lsp.lua`

```lua

local lspconfig = require('lspconfig')
lspconfig.pyright.setup({
	cmd = { 'pyright-langserver', '--stdio' },
	filetypes = { 'python' },
	root_dir = function(fname)
	    local root_files = {
	        'pyproject.toml',
	        'setup.py',
	        'setup.cfg',
	        'requirements.txt',
	        'Pipfile',
	        'pyrightconfig.json',
	    }
	    return lspconfig.util.root_pattern(unpack(root_files))(fname) or lspconfig.util.find_git_ancestor(fname) or lspconfig.util.path.dirname(fname)
	end,
	settings = {
	    python = {
	        analysis = {
	            autoSearchPaths = true,
	            diagnosticMode = 'workspace',
	            useLibraryCodeForTypes = true,
	        },
	    },
	},
})
```

In `lsp/init.lua`

```
return {
    -- ...
    require(config.lsp.python_lsp')
    -- ...
}
```
