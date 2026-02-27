# Basic Neovim Configuration

A complete, production-ready Neovim configuration for users who have completed the basics and want a fully-featured editor with all essential plugins.

## What's Included

### Core Features
- ✅ **Plugin Manager**: lazy.nvim for fast plugin loading
- ✅ **Colorscheme**: tokyonight.nvim
- ✅ **LSP**: Full language server support (Lua, Python, TypeScript)
- ✅ **Autocompletion**: nvim-cmp with multiple sources
- ✅ **File Navigation**: Telescope fuzzy finder + nvim-tree file explorer
- ✅ **Syntax Highlighting**: Treesitter for accurate syntax
- ✅ **Git Integration**: gitsigns for diff markers and hunk management
- ✅ **UI Enhancements**: lualine, bufferline, which-key, indent guides

### Plugins (14 total)

1. **tokyonight.nvim** - Modern colorscheme
2. **telescope.nvim** - Fuzzy finder for files, text, buffers
3. **nvim-tree.lua** - File explorer sidebar
4. **nvim-treesitter** - Better syntax highlighting
5. **gitsigns.nvim** - Git diff indicators
6. **nvim-autopairs** - Auto-close brackets and quotes
7. **Comment.nvim** - Smart commenting with gc
8. **which-key.nvim** - Keybinding hints
9. **lualine.nvim** - Status line
10. **bufferline.nvim** - Buffer/tab line
11. **indent-blankline.nvim** - Indent guides
12. **mason.nvim** - LSP server installer
13. **nvim-lspconfig** - LSP configurations
14. **nvim-cmp** - Autocompletion engine

## Installation

### Prerequisites

- Neovim >= 0.9.0 (check with `nvim --version`)
- Git
- A [Nerd Font](https://www.nerdfonts.com/) for icons (optional but recommended)
- ripgrep for Telescope live_grep (`brew install ripgrep` or `apt install ripgrep`)

### Method 1: Try Without Installing

Test this config without affecting your current setup:

```bash
# From the repository root
nvim -u examples/basic/init.lua
```

### Method 2: Fresh Install

**Backup your existing config first!**

```bash
# Backup existing config (if any)
mv ~/.config/nvim ~/.config/nvim.backup
mv ~/.local/share/nvim ~/.local/share/nvim.backup

# Copy this config
mkdir -p ~/.config/nvim
cp examples/basic/init.lua ~/.config/nvim/init.lua

# Launch Neovim
nvim
```

On first launch, lazy.nvim will:
1. Install itself
2. Install all plugins
3. Install language servers via Mason

This may take 1-2 minutes.

### Method 3: Use as Template

Copy and modify for your own config:

```bash
mkdir -p ~/.config/nvim
cp examples/basic/init.lua ~/.config/nvim/init.lua
# Edit init.lua to customize
nvim ~/.config/nvim/init.lua
```

## Quick Start Guide

### Essential Keybindings

**Leader key is `Space`**

#### File Operations
| Key | Action |
|-----|--------|
| `<leader>w` | Save file |
| `<leader>q` | Quit |
| `<leader>e` | Toggle file explorer |

#### Finding Files
| Key | Action |
|-----|--------|
| `<leader>ff` | Find files |
| `<leader>fg` | Live grep (search in files) |
| `<leader>fb` | List buffers |
| `<leader>fh` | Search help tags |
| `<leader>fr` | Recent files |

#### Navigation
| Key | Action |
|-----|--------|
| `Ctrl-h/j/k/l` | Move between windows |
| `Shift-h` | Previous buffer |
| `Shift-l` | Next buffer |
| `gd` | Go to definition (LSP) |
| `gr` | Go to references (LSP) |
| `K` | Hover documentation (LSP) |

#### Editing
| Key | Action |
|-----|--------|
| `gcc` | Toggle line comment |
| `gc` (visual) | Toggle comment on selection |
| `jk` | Exit insert mode |
| `Alt-j/k` | Move line up/down |

#### Git
| Key | Action |
|-----|--------|
| `]c` | Next git hunk |
| `[c` | Previous git hunk |
| `<leader>hp` | Preview hunk |
| `<leader>hs` | Stage hunk |
| `<leader>hr` | Reset hunk |

#### LSP
| Key | Action |
|-----|--------|
| `gd` | Go to definition |
| `K` | Hover info |
| `<leader>vrn` | Rename symbol |
| `<leader>vca` | Code actions |
| `]d` | Next diagnostic |
| `[d` | Previous diagnostic |

## First Steps

1. **Open a file**:
   ```bash
   nvim myfile.py
   ```

2. **Explore file tree**: Press `<leader>e` (Space + e)

3. **Find files**: Press `<leader>ff` (Space + f + f)

4. **Install a language server**:
   - Open `:Mason`
   - Navigate with `j/k`
   - Press `i` to install a server
   - Or wait for automatic installation when opening supported files

5. **Test LSP**: Open a Python/Lua/TypeScript file
   - Hover over a function, press `K` for documentation
   - Press `gd` to jump to definition
   - Start typing for autocompletion

## Customization

### Change Colorscheme

Replace `tokyonight.nvim` with another scheme:

```lua
-- In the plugins section, replace:
{
  "folke/tokyonight.nvim",
  -- with:
  "catppuccin/nvim",
  name = "catppuccin",
  config = function()
    vim.cmd.colorscheme("catppuccin")
  end,
}
```

Popular alternatives:
- `catppuccin/nvim`
- `ellisonleao/gruvbox.nvim`
- `rebelot/kanagawa.nvim`

### Add More Language Servers

Edit the `mason-lspconfig` section:

```lua
require("mason-lspconfig").setup({
  ensure_installed = { 
    "lua_ls", 
    "pyright", 
    "ts_ls",
    "rust_analyzer",  -- Add Rust
    "gopls",          -- Add Go
  },
})
```

Then add setup in the `nvim-lspconfig` section:

```lua
lspconfig.rust_analyzer.setup({ capabilities = capabilities, on_attach = on_attach })
lspconfig.gopls.setup({ capabilities = capabilities, on_attach = on_attach })
```

### Change Indentation

Modify the options section:

```lua
vim.opt.tabstop = 2      -- 2 spaces for tabs
vim.opt.shiftwidth = 2   -- 2 spaces for indentation
vim.opt.expandtab = true -- Use spaces, not tabs
```

### Add Custom Keybindings

Add after the keymaps section:

```lua
vim.keymap.set("n", "<leader>gg", "<cmd>terminal lazygit<CR>", { desc = "LazyGit" })
```

## Troubleshooting

### Plugins Not Installing

1. Check internet connection
2. Run `:Lazy sync`
3. Check `:checkhealth lazy`

### LSP Not Working

1. Check language server is installed: `:Mason`
2. Check LSP status: `:LspInfo`
3. Restart LSP: `:LspRestart`
4. Check health: `:checkhealth lsp`

### Telescope Can't Find Files

1. Ensure ripgrep is installed: `rg --version`
2. Check you're in the right directory
3. Try `:Telescope find_files hidden=true` for hidden files

### Icons Not Showing

Install a Nerd Font:
1. Download from [nerdfonts.com](https://www.nerdfonts.com/)
2. Install the font on your system
3. Configure your terminal to use it

## Learning Path

After getting comfortable with this config:

1. **Read the code**: Understand what each plugin does
2. **Customize**: Modify keybindings, options, plugins
3. **Add more**: Explore [awesome-neovim](https://github.com/rockerBOO/awesome-neovim)
4. **Learn advanced features**: See the full course modules
5. **Build from scratch**: Try creating your own config

## Structure for Growth

When your config outgrows a single file:

```
~/.config/nvim/
├── init.lua              # Entry point (minimal)
├── lua/
│   ├── options.lua       # Vim options
│   ├── keymaps.lua       # Keybindings
│   ├── autocmds.lua      # Autocommands
│   └── plugins/
│       ├── init.lua      # Plugin list
│       ├── telescope.lua # Telescope config
│       ├── lsp.lua       # LSP config
│       └── ...
```

## Resources

- **Modules**: See [docs/](../../docs/) for in-depth guides
- **Help**: Use `:help <topic>` in Neovim
- **Community**: See [resources/communities.md](../../resources/communities.md)
- **Plugins**: Explore each plugin's GitHub page for more options

## What's Next

- **Debug setup**: Add nvim-dap for debugging (see [debugging guide](../../docs/07-workflows/debugging.md))
- **Test runner**: Add neotest (see [testing guide](../../docs/07-workflows/testing.md))
- **More Git**: Add fugitive or neogit (see [git guide](../../docs/07-workflows/git-integration.md))
- **Language-specific**: See Python or Web Dev example configs

## Support

Having issues? Check:
1. `:checkhealth` - Diagnose problems
2. Plugin READMEs - Each plugin has documentation
3. `:help <command>` - Built-in help system
4. [Community resources](../../resources/communities.md) - Ask for help

---

**Happy coding!** This config should serve you well as you continue your Neovim journey.
