# Introduction to lazy.nvim

lazy.nvim is a modern plugin manager for Neovim that focuses on performance through lazy-loading and has a clean, declarative configuration style.

## Why lazy.nvim?

- **Fast startup**: Plugins load only when needed
- **Simple setup**: Declarative plugin specifications
- **Built-in features**: Update checking, lockfile, profiling
- **Modern**: Written specifically for Neovim (not Vim compatible)

## Installation

Add this to your `~/.config/nvim/init.lua`:

```lua
-- Bootstrap lazy.nvim
local lazypath = vim.fn.stdpath("data") .. "/lazy/lazy.nvim"
if not vim.loop.fs_stat(lazypath) then
  vim.fn.system({
    "git",
    "clone",
    "--filter=blob:none",
    "https://github.com/folke/lazy.nvim.git",
    "--branch=stable",
    lazypath,
  })
end
vim.opt.rtp:prepend(lazypath)

-- Setup lazy.nvim
require("lazy").setup({
  -- Plugins will go here
})
```

## Basic Plugin Installation

### Simple Plugin (No Configuration)

```lua
require("lazy").setup({
  "nvim-lua/plenary.nvim",  -- Utility functions (many plugins need this)
})
```

### Plugin with Configuration

```lua
require("lazy").setup({
  {
    "folke/tokyonight.nvim",
    config = function()
      vim.cmd.colorscheme("tokyonight")
    end,
  },
})
```

### Plugin with Options

```lua
require("lazy").setup({
  {
    "nvim-telescope/telescope.nvim",
    dependencies = { "nvim-lua/plenary.nvim" },
    keys = {
      { "<leader>ff", "<cmd>Telescope find_files<cr>", desc = "Find Files" },
      { "<leader>fg", "<cmd>Telescope live_grep<cr>", desc = "Live Grep" },
    },
    opts = {
      defaults = {
        file_ignore_patterns = { "node_modules", ".git/" },
      },
    },
  },
})
```

## Plugin Specification Properties

| Property | Purpose | Example |
|----------|---------|---------|
| `dependencies` | Other plugins this plugin needs | `{ "nvim-lua/plenary.nvim" }` |
| `lazy` | Load plugin lazily | `true` |
| `event` | Load on Neovim event | `"BufRead"` |
| `cmd` | Load when command is run | `"Telescope"` |
| `keys` | Load on key mapping | `{ "<leader>ff" }` |
| `ft` | Load for file types | `{ "lua", "python" }` |
| `config` | Configuration function | `function() ... end` |
| `opts` | Options table (passes to setup) | `{ theme = "dark" }` |
| `init` | Always runs (even if lazy) | `function() ... end` |

## Lazy Loading

Lazy loading means plugins don't load until needed, keeping startup fast.

### Load on Event

```lua
{
  "nvim-treesitter/nvim-treesitter",
  event = { "BufReadPost", "BufNewFile" },
}
```

### Load on Command

```lua
{
  "kyazdani42/nvim-tree.lua",
  cmd = "NvimTreeToggle",
}
```

### Load on Keymap

```lua
{
  "numToStr/Comment.nvim",
  keys = {
    { "gc", mode = { "n", "v" } },
    { "gb", mode = { "n", "v" } },
  },
}
```

### Load for File Types

```lua
{
  "rust-lang/rust.vim",
  ft = "rust",
}
```

## Managing Plugins

### Plugin Commands

- `:Lazy` - Open lazy.nvim UI
- `:Lazy update` - Update all plugins
- `:Lazy sync` - Install missing and update plugins
- `:Lazy clean` - Remove unused plugins
- `:Lazy profile` - Show startup profiling

### The Lazy.nvim UI

Press `:Lazy` to open the UI where you can:
- See all installed plugins
- Update plugins with `U`
- Profile startup time with `P`
- View plugin details
- Check for breaking changes

## Organizing Plugins

For larger configs, split plugins into separate files:

**~/.config/nvim/init.lua**
```lua
require("lazy").setup("plugins")
```

**~/.config/nvim/lua/plugins/init.lua**
```lua
return {
  "nvim-lua/plenary.nvim",
  require("plugins.telescope"),
  require("plugins.treesitter"),
}
```

**~/.config/nvim/lua/plugins/telescope.lua**
```lua
return {
  "nvim-telescope/telescope.nvim",
  dependencies = { "nvim-lua/plenary.nvim" },
  config = function()
    require("telescope").setup({
      -- config here
    })
  end,
}
```

## Common Patterns

### Plugin That Needs Setup

```lua
{
  "numToStr/Comment.nvim",
  opts = {},  -- Calls require("Comment").setup({})
}
```

### Plugin with Complex Configuration

```lua
{
  "neovim/nvim-lspconfig",
  config = function()
    local lspconfig = require("lspconfig")
    lspconfig.lua_ls.setup({})
    lspconfig.pyright.setup({})
  end,
}
```

### Plugin That Needs Init (Before Loading)

```lua
{
  "folke/which-key.nvim",
  init = function()
    vim.o.timeout = true
    vim.o.timeoutlen = 300
  end,
  config = function()
    require("which-key").setup()
  end,
}
```

## Exercises

1. **Install lazy.nvim** - Add the bootstrap code to your `init.lua`
2. **Add a colorscheme** - Install and configure tokyonight.nvim or catppuccin.nvim
3. **Add a plugin** - Install nvim-autopairs with proper configuration
4. **Explore the UI** - Run `:Lazy` and explore the interface
5. **Profile startup** - Use `:Lazy profile` to see load times

## Troubleshooting

### Plugin Not Loading

- Check `:Lazy` to see if it's installed
- Check if lazy-loading conditions are met
- Try `:Lazy load <plugin-name>` to force load
- Read `:checkhealth lazy`

### Plugin Errors

- Read the error message carefully
- Check plugin README for required dependencies
- Ensure configuration is correct
- Try `:Lazy sync` to reinstall

### Slow Startup

- Run `:Lazy profile` to identify slow plugins
- Add lazy-loading where possible
- Consider removing unused plugins

## Best Practices

1. **Start minimal** - Add plugins only when you need them
2. **Lazy load** - Use events, commands, or keys when possible
3. **Read documentation** - Check plugin READMEs for proper setup
4. **Pin versions** - Use `version` or `commit` for stability
5. **Regular updates** - Run `:Lazy update` periodically
6. **Clean up** - Remove plugins you don't use

## Next Steps

Continue to [Essential Plugins](essential-plugins.md) to learn which plugins to install first.
