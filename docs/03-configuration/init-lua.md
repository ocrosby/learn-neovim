# Understanding init.lua

Learn how to structure your Neovim configuration using Lua.

## What is init.lua?

`init.lua` is the main entry point for your Neovim configuration. When Neovim starts, it looks for this file and executes it.

**Location**:
- **Linux/macOS**: `~/.config/nvim/init.lua`
- **Windows**: `%LOCALAPPDATA%\nvim\init.lua`

## Why Lua over Vimscript?

**Performance**: Lua is faster than Vimscript

**Modern**: Lua is the future of Neovim configuration

**Powerful**: Access to full Neovim API

**Readable**: More familiar syntax for programmers

**Plugin ecosystem**: Modern plugins use Lua

## Your First init.lua

Create the directory structure:

```bash
# Linux/macOS
mkdir -p ~/.config/nvim

# Windows (PowerShell)
New-Item -ItemType Directory -Force $env:LOCALAPPDATA\nvim
```

Create `~/.config/nvim/init.lua`:

```lua
-- My Neovim Configuration

-- Set leader key
vim.g.mapleader = " "

-- Enable line numbers
vim.opt.number = true

-- Basic keymap
vim.keymap.set("n", "<leader>w", ":w<CR>")

print("Neovim config loaded!")
```

Launch Neovim—you should see "Neovim config loaded!" at the bottom.

## Lua Basics for Neovim

### Comments

```lua
-- Single line comment

--[[
  Multi-line
  comment
]]
```

### Variables

```lua
local name = "value"        -- Local variable (preferred)
global_var = "value"        -- Global variable (avoid)
```

**Always use `local`** unless you need global scope.

### Vim Namespaces

Neovim provides these main namespaces:

```lua
vim.opt      -- Options (like :set)
vim.g        -- Global variables
vim.b        -- Buffer-scoped variables
vim.w        -- Window-scoped variables
vim.t        -- Tab-scoped variables
vim.env      -- Environment variables
vim.api      -- Neovim API functions
vim.fn       -- Vimscript functions
vim.keymap   -- Keymappings
vim.cmd      -- Execute Vimscript commands
```

### Setting Options

```lua
-- Boolean options
vim.opt.number = true
vim.opt.wrap = false

-- Number options
vim.opt.tabstop = 4
vim.opt.shiftwidth = 4

-- String options
vim.opt.colorscheme = "default"

-- List options
vim.opt.listchars = { tab = "» ", trail = "·" }
```

Equivalent Vimscript:
```vim
set number
set nowrap
set tabstop=4
set shiftwidth=4
```

### Global Variables

```lua
-- Set leader key (must be before plugins)
vim.g.mapleader = " "
vim.g.maplocalleader = " "

-- Plugin configuration
vim.g.netrw_liststyle = 3
```

### Executing Vimscript Commands

When Lua doesn't have an equivalent:

```lua
-- Single command
vim.cmd("colorscheme desert")

-- Multiple commands
vim.cmd([[
  augroup MyGroup
    autocmd!
    autocmd BufWritePre * :%s/\s\+$//e
  augroup END
]])
```

## Structuring Your Configuration

### Single File (Beginner)

```
~/.config/nvim/
└── init.lua
```

Everything in one file. Good for learning, not scalable.

### Modular Structure (Recommended)

```
~/.config/nvim/
├── init.lua              # Entry point
└── lua/
    └── config/
        ├── options.lua   # All vim.opt settings
        ├── keymaps.lua   # All keybindings
        └── autocmds.lua  # Autocommands
```

**init.lua**:
```lua
-- Load configuration modules
require("config.options")
require("config.keymaps")
require("config.autocmds")
```

**lua/config/options.lua**:
```lua
-- Options
local opt = vim.opt

opt.number = true
opt.relativenumber = true
opt.tabstop = 4
-- ... more options
```

### Advanced Structure (With Plugins)

```
~/.config/nvim/
├── init.lua
└── lua/
    ├── config/
    │   ├── options.lua
    │   ├── keymaps.lua
    │   └── autocmds.lua
    └── plugins/
        ├── init.lua
        ├── telescope.lua
        ├── lsp.lua
        └── treesitter.lua
```

## The require() Function

`require()` loads Lua modules:

```lua
-- Loads lua/config/options.lua
require("config.options")

-- Loads lua/plugins/telescope.lua
require("plugins.telescope")
```

**How it works**:
- Looks in `lua/` directory in `runtimepath`
- Converts dots to directory separators
- Adds `.lua` extension
- Executes the file

**Example**:
```lua
require("config.keymaps")
-- Searches for:
-- 1. ~/.config/nvim/lua/config/keymaps.lua
-- 2. ~/.config/nvim/lua/config/keymaps/init.lua
```

## Returning Values from Modules

Modules can return values:

**lua/config/defaults.lua**:
```lua
local M = {}

M.tabstop = 4
M.shiftwidth = 4
M.colorscheme = "desert"

return M
```

**init.lua**:
```lua
local defaults = require("config.defaults")
vim.opt.tabstop = defaults.tabstop
vim.opt.shiftwidth = defaults.shiftwidth
```

## Conditional Configuration

Load config based on conditions:

```lua
-- OS-specific settings
if vim.fn.has("mac") == 1 then
  vim.opt.clipboard = "unnamed"
elseif vim.fn.has("unix") == 1 then
  vim.opt.clipboard = "unnamedplus"
end

-- Environment-specific
if vim.env.TERM == "xterm-kitty" then
  vim.g.kitty_mode = true
end

-- Neovim version check
if vim.fn.has("nvim-0.10") == 1 then
  -- Use new features
end
```

## Debugging Your Config

### Print Debugging

```lua
print("Config loaded")
print(vim.inspect(vim.opt.tabstop))  -- Inspect complex values
```

### Checking Option Values

```lua
-- In your config
vim.opt.number = true

-- In Neovim command line
:lua print(vim.opt.number:get())
```

### Error Messages

Lua errors show file and line number:
```
Error detected while processing init.lua:
line 15: attempt to index nil value
```

### Testing Config Changes

Test without affecting your config:

```bash
nvim -u /path/to/test-init.lua
nvim -u NONE  # No config
nvim --clean  # Default config, no plugins
```

## Common Patterns

### Local Variables for Vim Namespaces

```lua
local opt = vim.opt
local keymap = vim.keymap
local cmd = vim.cmd

opt.number = true
keymap.set("n", "<leader>w", ":w<CR>")
cmd("colorscheme desert")
```

Reduces repetition and improves readability.

### Protected Calls

Safely load optional modules:

```lua
local ok, module = pcall(require, "optional_module")
if ok then
  module.setup()
else
  print("Module not found")
end
```

### Checking if Command Exists

```lua
if vim.fn.executable("rg") == 1 then
  -- ripgrep is available
  vim.opt.grepprg = "rg --vimgrep"
end
```

## Migration from init.vim

If you have an `init.vim`, migrate gradually:

### Option 1: Call Vimscript from Lua

**init.lua**:
```lua
vim.cmd("source ~/.config/nvim/legacy.vim")
```

### Option 2: Convert Gradually

**Before (init.vim)**:
```vim
set number
set relativenumber
nnoremap <leader>w :w<CR>
```

**After (init.lua)**:
```lua
vim.opt.number = true
vim.opt.relativenumber = true
vim.keymap.set("n", "<leader>w", ":w<CR>")
```

## Best Practices

1. **Set leader early**: Before any plugins or keymaps
2. **Use local variables**: Faster and cleaner
3. **Organize logically**: Group related settings
4. **Comment your config**: Future you will thank you
5. **Use modular structure**: Easier to maintain
6. **Test incrementally**: Add options one at a time
7. **Use `:checkhealth`**: Verify configuration

## Example Minimal init.lua

```lua
-- Leader key (must be first)
vim.g.mapleader = " "
vim.g.maplocalleader = " "

-- Options
local opt = vim.opt

opt.number = true
opt.relativenumber = true
opt.mouse = "a"
opt.ignorecase = true
opt.smartcase = true
opt.hlsearch = false
opt.wrap = false
opt.breakindent = true
opt.tabstop = 4
opt.shiftwidth = 4
opt.expandtab = true
opt.undofile = true
opt.signcolumn = "yes"
opt.colorcolumn = "80"
opt.scrolloff = 8
opt.splitright = true
opt.splitbelow = true

-- Keymaps
local keymap = vim.keymap

keymap.set("n", "<leader>w", ":w<CR>", { desc = "Save" })
keymap.set("n", "<leader>q", ":q<CR>", { desc = "Quit" })
keymap.set("i", "jk", "<Esc>", { desc = "Exit insert" })
keymap.set("n", "<C-h>", "<C-w>h", { desc = "Left window" })
keymap.set("n", "<C-j>", "<C-w>j", { desc = "Down window" })
keymap.set("n", "<C-k>", "<C-w>k", { desc = "Up window" })
keymap.set("n", "<C-l>", "<C-w>l", { desc = "Right window" })

-- Autocommands
local augroup = vim.api.nvim_create_augroup
local autocmd = vim.api.nvim_create_autocmd

local yank_group = augroup("YankHighlight", { clear = true })
autocmd("TextYankPost", {
  group = yank_group,
  pattern = "*",
  callback = function()
    vim.highlight.on_yank({ timeout = 200 })
  end,
})
```

## Exercises

1. **Create init.lua**: Set up your first configuration file
2. **Add 5 options**: Choose from `:help options`
3. **Create 3 keymaps**: Customize to your workflow
4. **Modularize**: Split into separate option and keymap files
5. **Add an autocommand**: Highlight on yank

## Troubleshooting

### Config not loading

- Check file location: `:echo stdpath('config')`
- Check for syntax errors in Lua
- Try `:luafile %` to reload current file

### Options not working

- Verify option name: `:help options`
- Check if plugin overrides your setting
- Try setting in command mode: `:lua vim.opt.number = true`

### Module not found

- Check file path matches `require()` statement
- Ensure file is in `lua/` directory
- Use forward slashes, not backslashes

## Next Steps

1. Understand your init.lua structure
2. Proceed to [Lesson 2: Options](options.md)
3. Learn [Lesson 3: Keymaps](keymaps.md)

## Additional Resources

- `:help lua-guide` - Official Lua guide
- `:help lua-intro` - Lua introduction
- `:help api` - Neovim API reference
- [Learn Lua in Y Minutes](https://learnxinyminutes.com/docs/lua/)
- [Nvim Lua Guide](https://github.com/nanotee/nvim-lua-guide)
