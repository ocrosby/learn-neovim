# Options

Learn essential Neovim options to customize your editing experience.

## Understanding Options

Options control Neovim's behavior. In Vimscript you use `:set`, in Lua you use `vim.opt`.

### Option Types

**Boolean**: true/false
```lua
vim.opt.number = true
```

**Number**: integers
```lua
vim.opt.tabstop = 4
```

**String**: text values
```lua
vim.opt.colorscheme = "desert"
```

**List**: arrays of values
```lua
vim.opt.listchars = { tab = "» ", trail = "·" }
```

## Essential Options

### Line Numbers

```lua
vim.opt.number = true              -- Show line numbers
vim.opt.relativenumber = true      -- Relative line numbers
vim.opt.numberwidth = 4            -- Width of number column
vim.opt.signcolumn = "yes"         -- Always show sign column
```

**Use case**: `relativenumber` makes vertical motions easier (`10j`, `5k`).

### Indentation

```lua
vim.opt.tabstop = 4                -- Width of tab character
vim.opt.shiftwidth = 4             -- Width of indent
vim.opt.expandtab = true           -- Use spaces instead of tabs
vim.opt.smartindent = true         -- Auto-indent new lines
vim.opt.autoindent = true          -- Copy indent from current line
vim.opt.breakindent = true         -- Wrapped lines continue visually indented
```

**Common presets**:

2-space (JavaScript, Ruby):
```lua
vim.opt.tabstop = 2
vim.opt.shiftwidth = 2
vim.opt.expandtab = true
```

4-space (Python):
```lua
vim.opt.tabstop = 4
vim.opt.shiftwidth = 4
vim.opt.expandtab = true
```

Tabs (Go, Makefiles):
```lua
vim.opt.tabstop = 4
vim.opt.shiftwidth = 4
vim.opt.expandtab = false
```

### Search

```lua
vim.opt.ignorecase = true          -- Case-insensitive search
vim.opt.smartcase = true           -- Case-sensitive if uppercase used
vim.opt.hlsearch = false           -- Don't highlight all matches
vim.opt.incsearch = true           -- Show match as you type
```

**How smartcase works**:
- `/foo` matches `foo`, `Foo`, `FOO`
- `/Foo` matches only `Foo`

### Display

```lua
vim.opt.wrap = false               -- Don't wrap long lines
vim.opt.linebreak = true           -- Wrap at word boundaries
vim.opt.showmode = false           -- Don't show mode (status line does this)
vim.opt.showcmd = true             -- Show partial commands
vim.opt.cursorline = true          -- Highlight current line
vim.opt.colorcolumn = "80"         -- Show column at 80 characters
vim.opt.scrolloff = 8              -- Keep 8 lines above/below cursor
vim.opt.sidescrolloff = 8          -- Keep 8 columns left/right of cursor
vim.opt.list = true                -- Show invisible characters
vim.opt.listchars = {              -- Define which invisible chars to show
  tab = "» ",
  trail = "·",
  nbsp = "␣",
  extends = "→",
  precedes = "←",
}
```

### Windows and Splits

```lua
vim.opt.splitright = true          -- Vertical splits open right
vim.opt.splitbelow = true          -- Horizontal splits open below
vim.opt.equalalways = false        -- Don't auto-resize splits
```

### Performance

```lua
vim.opt.updatetime = 250           -- Faster completion (default 4000ms)
vim.opt.timeoutlen = 300           -- Faster key sequence timeout
vim.opt.lazyredraw = false         -- Don't redraw during macros (can cause issues)
```

### Files and Buffers

```lua
vim.opt.hidden = true              -- Keep buffers open in background
vim.opt.backup = false             -- Don't create backup files
vim.opt.writebackup = false        -- Don't backup before overwriting
vim.opt.swapfile = false           -- Don't create swap files
vim.opt.undofile = true            -- Persistent undo
vim.opt.undodir = vim.fn.stdpath("data") .. "/undo"  -- Undo directory
```

**Persistent undo** lets you undo even after closing and reopening a file.

### Completion

```lua
vim.opt.completeopt = { "menu", "menuone", "noselect" }
vim.opt.pumheight = 10             -- Completion popup max height
```

### Mouse

```lua
vim.opt.mouse = "a"                -- Enable mouse in all modes
vim.opt.mousemoveevent = true      -- Enable mouse move events
```

**Why enable mouse?**
- Useful for beginners
- Quick window resizing
- Scroll with wheel
- Doesn't prevent keyboard usage

### Clipboard

```lua
-- macOS
vim.opt.clipboard = "unnamed"

-- Linux/WSL
vim.opt.clipboard = "unnamedplus"

-- Both
vim.opt.clipboard = { "unnamed", "unnamedplus" }
```

**Effect**: `y` yanks to system clipboard, `p` pastes from system clipboard.

### Visual

```lua
vim.opt.termguicolors = true       -- True color support
vim.opt.background = "dark"        -- Dark background (or "light")
vim.opt.conceallevel = 0           -- Show concealed text
```

### Wildmenu (Command-line Completion)

```lua
vim.opt.wildmenu = true            -- Enhanced command-line completion
vim.opt.wildmode = { "longest:full", "full" }
vim.opt.wildignore = {             -- Ignore these patterns
  "*.o", "*.obj", "*.class",
  "*/.git/*", "*/.hg/*", "*/.svn/*",
  "*/node_modules/*", "*/__pycache__/*",
}
```

### Formatting

```lua
vim.opt.formatoptions = vim.opt.formatoptions
  - "t"    -- Don't auto-wrap text
  + "c"    -- Auto-wrap comments
  + "r"    -- Continue comments on Enter
  - "o"    -- Don't continue comments with 'o'/'O'
  + "q"    -- Allow formatting comments with 'gq'
  - "a"    -- Don't auto-format paragraphs
  + "n"    -- Recognize numbered lists
  + "j"    -- Remove comment leader when joining
```

## Viewing Current Options

### In Command Mode

```vim
:set number?          " Show current value
:set number           " Show if enabled
:set all              " Show all options
```

### In Lua

```lua
:lua print(vim.opt.number:get())
:lua print(vim.inspect(vim.opt.listchars:get()))
```

## Setting Options

### Global Options

```lua
vim.opt.number = true
```

### Buffer-local Options

```lua
vim.bo.tabstop = 2           -- Just for current buffer
vim.opt_local.tabstop = 2    -- Same thing
```

### Window-local Options

```lua
vim.wo.wrap = false          -- Just for current window
vim.opt_local.wrap = false   -- Same thing
```

## Filetype-Specific Options

Use autocommands for filetype-specific settings:

```lua
-- lua/config/autocmds.lua
local augroup = vim.api.nvim_create_augroup
local autocmd = vim.api.nvim_create_autocmd

local filetype_group = augroup("FileTypeSettings", { clear = true })

autocmd("FileType", {
  group = filetype_group,
  pattern = "python",
  callback = function()
    vim.opt_local.tabstop = 4
    vim.opt_local.shiftwidth = 4
    vim.opt_local.colorcolumn = "88"  -- PEP 8
  end,
})

autocmd("FileType", {
  group = filetype_group,
  pattern = { "javascript", "typescript", "json" },
  callback = function()
    vim.opt_local.tabstop = 2
    vim.opt_local.shiftwidth = 2
  end,
})

autocmd("FileType", {
  group = filetype_group,
  pattern = "go",
  callback = function()
    vim.opt_local.expandtab = false  -- Go uses tabs
    vim.opt_local.tabstop = 4
  end,
})
```

## Recommended Starter Options

```lua
-- lua/config/options.lua
local opt = vim.opt

-- UI
opt.number = true
opt.relativenumber = true
opt.signcolumn = "yes"
opt.cursorline = true
opt.scrolloff = 8
opt.colorcolumn = "80"
opt.termguicolors = true

-- Editing
opt.tabstop = 4
opt.shiftwidth = 4
opt.expandtab = true
opt.smartindent = true
opt.wrap = false

-- Search
opt.ignorecase = true
opt.smartcase = true
opt.hlsearch = false
opt.incsearch = true

-- Splits
opt.splitright = true
opt.splitbelow = true

-- Files
opt.undofile = true
opt.backup = false
opt.swapfile = false

-- Performance
opt.updatetime = 250
opt.timeoutlen = 300

-- Mouse
opt.mouse = "a"

-- Clipboard
if vim.fn.has("mac") == 1 then
  opt.clipboard = "unnamed"
else
  opt.clipboard = "unnamedplus"
end

-- Completion
opt.completeopt = { "menu", "menuone", "noselect" }

-- Display
opt.showmode = false
opt.list = true
opt.listchars = { tab = "» ", trail = "·", nbsp = "␣" }
```

## Common Option Combinations

### Minimal Distraction

```lua
opt.number = false
opt.relativenumber = false
opt.signcolumn = "no"
opt.cursorline = false
opt.colorcolumn = ""
opt.laststatus = 0  -- No status line
```

### Code-focused

```lua
opt.number = true
opt.relativenumber = true
opt.signcolumn = "yes"
opt.cursorline = true
opt.colorcolumn = "80,120"
opt.list = true
```

### Writing Prose

```lua
opt.wrap = true
opt.linebreak = true
opt.spell = true
opt.spelllang = "en_us"
opt.textwidth = 80
```

## Testing Options

Try options temporarily in command mode:

```vim
:set number!          " Toggle
:set nonumber         " Disable
:set number           " Enable
:set number?          " Check current value
```

Or in Lua:

```vim
:lua vim.opt.number = not vim.opt.number:get()
```

## Option Reference

See all options:
```vim
:help options
:help option-list
```

Specific options:
```vim
:help 'number'
:help 'tabstop'
:help 'clipboard'
```

## Common Mistakes

### Wrong Syntax

```lua
-- Wrong
vim.opt.number = "true"  -- String, not boolean

-- Right
vim.opt.number = true
```

### Not Using Local

```lua
-- Wrong (slower)
vim.opt.tabstop = 4
vim.opt.shiftwidth = 4
vim.opt.expandtab = true

-- Right (faster)
local opt = vim.opt
opt.tabstop = 4
opt.shiftwidth = 4
opt.expandtab = true
```

### Setting Leader Too Late

```lua
-- Wrong - leader must be set before plugins
require("plugins")
vim.g.mapleader = " "

-- Right
vim.g.mapleader = " "
require("plugins")
```

## Exercises

1. **Set basic options**: Number, relativenumber, tabstop
2. **Customize search**: Try different combinations of ignorecase/smartcase
3. **Experiment with display**: Try different listchars and colorcolumn values
4. **Create filetype settings**: Different tabstop for different languages
5. **Toggle options**: Create keymaps to toggle wrap, number, etc.

## Next Lesson

Proceed to [Lesson 3: Keymaps](keymaps.md) to learn custom keyboard mappings.

## Additional Resources

- `:help options` - Complete option reference
- `:help option-summary` - Categorized options
- `:help setting-options` - How to set options
- `:help local-options` - Buffer/window-local options
