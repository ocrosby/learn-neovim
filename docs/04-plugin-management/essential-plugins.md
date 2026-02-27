# Essential Plugins

A curated list of must-have plugins to transform Neovim into a powerful development environment.

## Philosophy

Start with minimal plugins and add only what you need. Each plugin here solves a specific problem.

## Core Utilities

### plenary.nvim

**Purpose**: Library of Lua functions used by many plugins

```lua
"nvim-lua/plenary.nvim"
```

**Why**: Required dependency for Telescope, Gitsigns, and many others. No configuration needed.

---

## File Navigation

### Telescope

**Purpose**: Fuzzy finder for files, text, buffers, and more

```lua
{
  "nvim-telescope/telescope.nvim",
  dependencies = { "nvim-lua/plenary.nvim" },
  cmd = "Telescope",
  keys = {
    { "<leader>ff", "<cmd>Telescope find_files<cr>", desc = "Find Files" },
    { "<leader>fg", "<cmd>Telescope live_grep<cr>", desc = "Live Grep" },
    { "<leader>fb", "<cmd>Telescope buffers<cr>", desc = "Buffers" },
    { "<leader>fh", "<cmd>Telescope help_tags<cr>", desc = "Help Tags" },
  },
  opts = {
    defaults = {
      file_ignore_patterns = { "node_modules", ".git/", "*.pyc" },
      mappings = {
        i = {
          ["<C-j>"] = "move_selection_next",
          ["<C-k>"] = "move_selection_previous",
        },
      },
    },
  },
}
```

**Key Features**:
- `<leader>ff` - Find files
- `<leader>fg` - Search text in files (requires ripgrep)
- `<leader>fb` - Switch between open buffers
- `<leader>fh` - Search help documentation

### nvim-tree

**Purpose**: File explorer sidebar

```lua
{
  "nvim-tree/nvim-tree.lua",
  dependencies = { "nvim-tree/nvim-web-devicons" },
  cmd = { "NvimTreeToggle", "NvimTreeFocus" },
  keys = {
    { "<leader>e", "<cmd>NvimTreeToggle<cr>", desc = "Toggle File Explorer" },
  },
  opts = {
    view = {
      width = 30,
      side = "left",
    },
    renderer = {
      group_empty = true,
    },
    filters = {
      dotfiles = false,
    },
  },
}
```

**Key Features**:
- `<leader>e` - Toggle file tree
- `a` - Create new file
- `d` - Delete file
- `r` - Rename file
- `y` - Copy file name

**Alternative**: [neo-tree.nvim](https://github.com/nvim-neo-tree/neo-tree.nvim) - More features, slightly heavier

---

## Code Editing

### nvim-treesitter

**Purpose**: Better syntax highlighting, code understanding, and text objects

```lua
{
  "nvim-treesitter/nvim-treesitter",
  build = ":TSUpdate",
  event = { "BufReadPost", "BufNewFile" },
  config = function()
    require("nvim-treesitter.configs").setup({
      ensure_installed = { "lua", "vim", "vimdoc", "python", "javascript" },
      auto_install = true,
      highlight = {
        enable = true,
        additional_vim_regex_highlighting = false,
      },
      indent = {
        enable = true,
      },
    })
  end,
}
```

**Why**: Dramatically better syntax highlighting using parse trees instead of regex.

### nvim-autopairs

**Purpose**: Automatically close brackets, quotes, and parentheses

```lua
{
  "windwp/nvim-autopairs",
  event = "InsertEnter",
  opts = {},
}
```

### Comment.nvim

**Purpose**: Smart commenting with `gc` operator

```lua
{
  "numToStr/Comment.nvim",
  keys = {
    { "gc", mode = { "n", "v" }, desc = "Comment toggle linewise" },
    { "gb", mode = { "n", "v" }, desc = "Comment toggle blockwise" },
  },
  opts = {},
}
```

**Usage**:
- `gcc` - Toggle comment on current line
- `gc3j` - Comment next 3 lines
- Visual mode + `gc` - Comment selection

### vim-surround

**Purpose**: Easily add/change/delete surrounding characters

```lua
{
  "tpope/vim-surround",
  event = "BufReadPost",
}
```

**Usage**:
- `ysiw"` - Surround word with quotes
- `cs"'` - Change surrounding " to '
- `ds"` - Delete surrounding "
- `yss)` - Surround entire line with ()

---

## Git Integration

### gitsigns.nvim

**Purpose**: Git decorations and hunk management

```lua
{
  "lewis6991/gitsigns.nvim",
  event = "BufReadPre",
  opts = {
    signs = {
      add = { text = "│" },
      change = { text = "│" },
      delete = { text = "_" },
      topdelete = { text = "‾" },
      changedelete = { text = "~" },
    },
    on_attach = function(bufnr)
      local gs = package.loaded.gitsigns
      local function map(mode, l, r, opts)
        opts = opts or {}
        opts.buffer = bufnr
        vim.keymap.set(mode, l, r, opts)
      end

      map("n", "]c", function()
        if vim.wo.diff then return "]c" end
        vim.schedule(function() gs.next_hunk() end)
        return "<Ignore>"
      end, { expr = true })

      map("n", "[c", function()
        if vim.wo.diff then return "[c" end
        vim.schedule(function() gs.prev_hunk() end)
        return "<Ignore>"
      end, { expr = true })

      map("n", "<leader>hs", gs.stage_hunk)
      map("n", "<leader>hr", gs.reset_hunk)
      map("n", "<leader>hp", gs.preview_hunk)
      map("n", "<leader>hb", function() gs.blame_line({ full = true }) end)
    end,
  },
}
```

**Key Features**:
- See added/changed/deleted lines in sign column
- `]c` / `[c` - Navigate between hunks
- `<leader>hp` - Preview hunk diff
- `<leader>hb` - Show git blame

---

## UI Enhancements

### which-key.nvim

**Purpose**: Display available keybindings in popup

```lua
{
  "folke/which-key.nvim",
  event = "VeryLazy",
  init = function()
    vim.o.timeout = true
    vim.o.timeoutlen = 300
  end,
  opts = {},
}
```

**Why**: Never forget keybindings. Shows popup after delay.

### lualine.nvim

**Purpose**: Fast and customizable statusline

```lua
{
  "nvim-lualine/lualine.nvim",
  dependencies = { "nvim-tree/nvim-web-devicons" },
  opts = {
    options = {
      theme = "auto",
      component_separators = { left = "|", right = "|" },
      section_separators = { left = "", right = "" },
    },
    sections = {
      lualine_a = { "mode" },
      lualine_b = { "branch", "diff", "diagnostics" },
      lualine_c = { "filename" },
      lualine_x = { "encoding", "fileformat", "filetype" },
      lualine_y = { "progress" },
      lualine_z = { "location" },
    },
  },
}
```

### bufferline.nvim

**Purpose**: Tab-like buffer line at the top

```lua
{
  "akinsho/bufferline.nvim",
  dependencies = "nvim-tree/nvim-web-devicons",
  event = "VeryLazy",
  keys = {
    { "<leader>bp", "<cmd>BufferLineTogglePin<cr>", desc = "Toggle pin" },
    { "<leader>bP", "<cmd>BufferLineGroupClose ungrouped<cr>", desc = "Close non-pinned buffers" },
    { "<S-h>", "<cmd>BufferLineCyclePrev<cr>", desc = "Prev buffer" },
    { "<S-l>", "<cmd>BufferLineCycleNext<cr>", desc = "Next buffer" },
  },
  opts = {
    options = {
      diagnostics = "nvim_lsp",
      always_show_bufferline = false,
    },
  },
}
```

### indent-blankline.nvim

**Purpose**: Show indent guides

```lua
{
  "lukas-reineke/indent-blankline.nvim",
  main = "ibl",
  event = "BufReadPost",
  opts = {
    indent = {
      char = "│",
    },
    scope = {
      enabled = false,
    },
  },
}
```

---

## Colorschemes

### tokyonight.nvim

```lua
{
  "folke/tokyonight.nvim",
  lazy = false,
  priority = 1000,
  config = function()
    vim.cmd.colorscheme("tokyonight-night")
  end,
}
```

**Alternatives**:
- [catppuccin](https://github.com/catppuccin/nvim)
- [gruvbox](https://github.com/ellisonleao/gruvbox.nvim)
- [kanagawa](https://github.com/rebelot/kanagawa.nvim)
- [nord](https://github.com/shaunsingh/nord.nvim)

---

## Complete Starter Configuration

Here's a complete `init.lua` with all essential plugins:

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

-- Leader key
vim.g.mapleader = " "
vim.g.maplocalleader = " "

-- Setup plugins
require("lazy").setup({
  "nvim-lua/plenary.nvim",

  {
    "nvim-telescope/telescope.nvim",
    dependencies = { "nvim-lua/plenary.nvim" },
    cmd = "Telescope",
    keys = {
      { "<leader>ff", "<cmd>Telescope find_files<cr>" },
      { "<leader>fg", "<cmd>Telescope live_grep<cr>" },
      { "<leader>fb", "<cmd>Telescope buffers<cr>" },
    },
  },

  {
    "nvim-tree/nvim-tree.lua",
    cmd = "NvimTreeToggle",
    keys = {
      { "<leader>e", "<cmd>NvimTreeToggle<cr>" },
    },
    opts = {},
  },

  {
    "nvim-treesitter/nvim-treesitter",
    build = ":TSUpdate",
    event = { "BufReadPost", "BufNewFile" },
    config = function()
      require("nvim-treesitter.configs").setup({
        ensure_installed = { "lua", "vim", "vimdoc" },
        auto_install = true,
        highlight = { enable = true },
      })
    end,
  },

  {
    "windwp/nvim-autopairs",
    event = "InsertEnter",
    opts = {},
  },

  {
    "numToStr/Comment.nvim",
    keys = { "gc", "gb" },
    opts = {},
  },

  {
    "lewis6991/gitsigns.nvim",
    event = "BufReadPre",
    opts = {},
  },

  {
    "folke/which-key.nvim",
    event = "VeryLazy",
    opts = {},
  },

  {
    "nvim-lualine/lualine.nvim",
    opts = {
      options = { theme = "auto" },
    },
  },

  {
    "folke/tokyonight.nvim",
    lazy = false,
    priority = 1000,
    config = function()
      vim.cmd.colorscheme("tokyonight")
    end,
  },
})
```

## Plugin Installation Checklist

1. ✅ **Plugin Manager** - lazy.nvim
2. ✅ **File Navigation** - Telescope + nvim-tree
3. ✅ **Syntax Highlighting** - nvim-treesitter
4. ✅ **Code Editing** - autopairs, Comment.nvim
5. ✅ **Git Integration** - gitsigns
6. ✅ **UI** - which-key, lualine
7. ✅ **Colorscheme** - tokyonight

## Next Steps

After installing these essentials:
1. Restart Neovim and let plugins install
2. Run `:checkhealth` to verify everything works
3. Experiment with keybindings
4. Continue to [Module 5: LSP](../05-lsp/README.md) for IDE features

## Exercises

1. **Install essentials** - Copy the complete configuration above
2. **Explore Telescope** - Try `<leader>ff`, `<leader>fg`, and `<leader>fb`
3. **Test commenting** - Use `gcc` to comment lines
4. **Check git signs** - Open a git repository and see change indicators
5. **Customize theme** - Try a different colorscheme from the alternatives

## Resources

- [awesome-neovim](https://github.com/rockerBOO/awesome-neovim) - Comprehensive plugin list
- [lazy.nvim docs](https://github.com/folke/lazy.nvim)
- Plugin READMEs - Always read before installing
