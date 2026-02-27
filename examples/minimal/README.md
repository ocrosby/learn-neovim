# Minimal Neovim Configuration

The absolute bare minimum to get started with Neovim. No plugins, just essential settings and keybindings. Perfect for beginners or when you need a lightweight config.

## Philosophy

This config demonstrates that Neovim is powerful even without plugins. Learn the fundamentals first, then add plugins only when you understand what problems they solve.

## What's Included

### Options (10 essential settings)
- **Line numbers**: Both absolute and relative for efficient navigation
- **Mouse support**: Click and scroll (optional, can disable)
- **Smart search**: Case-insensitive unless you type uppercase
- **Indentation**: 4-space tabs with auto-expand
- **No line wrapping**: See full lines

### Keybindings (9 essential mappings)
- **Leader key**: Space (standard in modern configs)
- **Save/Quit**: `<leader>w` and `<leader>q`
- **Escape insert mode**: `jk` (alternative to Esc key)
- **Window navigation**: `Ctrl-h/j/k/l` to move between splits

### What's NOT Included
- ❌ No plugins
- ❌ No LSP
- ❌ No autocomplete
- ❌ No file explorer
- ❌ No fuzzy finding
- ❌ No git integration
- ❌ No custom colorscheme

This is intentional. Learn core Vim/Neovim first.

## Installation

### Try It Out (Recommended First Step)

Test without affecting your current config:

```bash
cd /path/to/learn-neovim
nvim -u examples/minimal/init.lua
```

This loads the minimal config for this session only.

### Install Permanently

**⚠️ Warning**: This will replace your existing Neovim config.

```bash
# Backup existing config (if any)
mv ~/.config/nvim ~/.config/nvim.backup
mv ~/.local/share/nvim ~/.local/share/nvim.backup

# Create config directory
mkdir -p ~/.config/nvim

# Copy minimal config
cp examples/minimal/init.lua ~/.config/nvim/init.lua

# Start Neovim
nvim
```

### Verify Installation

1. Open Neovim: `nvim`
2. Check line numbers are visible on the left
3. Press `:` and type `set number?` and press Enter
   - Should show: `number`
4. Press Space (leader key) - nothing should happen, this is normal
5. Type `:echo mapleader` and press Enter
   - Should show a space character

## Learning Exercises

Use this config to master Neovim basics before adding complexity.

### Week 1: Modal Editing
1. **Stay in Normal mode**: Resist the urge to stay in Insert mode
2. **Practice movements**: `h j k l` (left, down, up, right)
3. **Word navigation**: `w` (next word), `b` (back word), `e` (end word)
4. **Line navigation**: `0` (start), `^` (first char), `$` (end)
5. **File navigation**: `gg` (top), `G` (bottom), `{number}G` (go to line)

### Week 2: Operators
1. **Delete**: `dd` (line), `dw` (word), `d$` (to end of line)
2. **Change**: `cc` (line), `cw` (word), `ciw` (inner word)
3. **Yank (copy)**: `yy` (line), `yiw` (word)
4. **Paste**: `p` (after), `P` (before)
5. **Undo/Redo**: `u` (undo), `Ctrl-r` (redo)

### Week 3: Visual Mode & Search
1. **Visual select**: `v` (character), `V` (line), `Ctrl-v` (block)
2. **Search**: `/pattern` (forward), `?pattern` (backward)
3. **Navigate matches**: `n` (next), `N` (previous)
4. **Replace**: `:%s/old/new/g` (file-wide), `:s/old/new/g` (line)

### Week 4: Splits & Files
1. **Split windows**: `:split` (horizontal), `:vsplit` (vertical)
2. **Navigate splits**: `Ctrl-h/j/k/l` (using config keybindings)
3. **Close split**: `:q` or `Ctrl-w q`
4. **Open files**: `:e filename`
5. **Save as**: `:saveas newname`

## Keybinding Reference

### Custom Mappings (Defined in Config)

| Mode | Key | Action | Description |
|------|-----|--------|-------------|
| Normal | `<leader>w` | `:w<CR>` | Save file (Space + w) |
| Normal | `<leader>q` | `:q<CR>` | Quit (Space + q) |
| Insert | `jk` | `<Esc>` | Exit insert mode (faster than Esc) |
| Normal | `<C-h>` | `<C-w>h` | Move to left window |
| Normal | `<C-j>` | `<C-w>j` | Move to bottom window |
| Normal | `<C-k>` | `<C-w>k` | Move to top window |
| Normal | `<C-l>` | `<C-w>l` | Move to right window |

### Built-in Vim Keybindings (Always Available)

See [resources/cheatsheets/basics.md](../../resources/cheatsheets/basics.md) for a comprehensive list.

## Options Explained

```lua
vim.opt.number = true           -- Show line numbers
vim.opt.relativenumber = true   -- Show relative line numbers (for movement commands)
vim.opt.mouse = "a"             -- Enable mouse in all modes
vim.opt.ignorecase = true       -- Ignore case when searching
vim.opt.smartcase = true        -- Unless search contains uppercase
vim.opt.hlsearch = false        -- Don't highlight search matches
vim.opt.wrap = false            -- Don't wrap long lines
vim.opt.breakindent = true      -- Preserve indentation in wrapped text
vim.opt.tabstop = 4             -- Tab width is 4 spaces
vim.opt.shiftwidth = 4          -- Indent width is 4 spaces
vim.opt.expandtab = true        -- Convert tabs to spaces
```

To understand any option:
```vim
:help number
:help relativenumber
```

## Customization

### Disable Mouse

```lua
vim.opt.mouse = ""
```

### Change Indentation to 2 Spaces

```lua
vim.opt.tabstop = 2
vim.opt.shiftwidth = 2
```

### Use Tabs Instead of Spaces

```lua
vim.opt.expandtab = false
```

### Enable Search Highlighting

```lua
vim.opt.hlsearch = true
```

### Disable Relative Line Numbers

```lua
vim.opt.relativenumber = false
```

## Common Commands to Learn

Even without plugins, Neovim is powerful:

### File Operations
```vim
:w              " Save
:q              " Quit
:wq or :x       " Save and quit
:q!             " Quit without saving
:e filename     " Open file
:saveas file    " Save as
```

### Editing
```vim
u               " Undo
Ctrl-r          " Redo
.               " Repeat last change
:undo 5         " Undo to change number 5
```

### Search & Replace
```vim
/pattern        " Search forward
?pattern        " Search backward
:%s/old/new/g   " Replace all in file
:%s/old/new/gc  " Replace with confirmation
```

### Navigation
```vim
gg              " Go to first line
G               " Go to last line
50G             " Go to line 50
%               " Go to matching bracket
```

## What to Do Next

### Option 1: Master the Basics
Stay with this minimal config for 2-4 weeks until movements feel natural.

**Signs you're ready for more:**
- You use `hjkl` without thinking
- You compose operators and motions (`d3w`, `c$`, `yiw`)
- You stay in Normal mode except when typing text
- You use text objects (`ciw`, `da"`, `vi(`)

### Option 2: Add Essentials Only
When ready, add just what you need:

1. **Colorscheme** (visual appeal)
2. **Treesitter** (better syntax highlighting)
3. **Telescope** (file navigation)
4. **LSP** (code intelligence)

See [basic example](../basic/) for these additions.

### Option 3: Learn More Built-in Features

Neovim has many powerful features built-in:

```vim
:help quickfix          " Built-in compiler output
:help terminal          " Built-in terminal
:help spell             " Spell checking
:help folding           " Code folding
:help macros            " Recording and replaying
```

## Troubleshooting

### Can't Save Files
- Try `:w!` to force save
- Check file permissions
- Make sure file path is correct

### jk Doesn't Work to Exit Insert Mode
- Type the letters quickly (< 300ms between them)
- Or use `Esc` key instead
- Or remove this mapping if you don't like it

### Numbers Not Showing
- Check `:set number?` - should show `number`
- Try `:set number` to enable manually

### Window Navigation Not Working
- Make sure you're in Normal mode (press Esc first)
- Create a split first: `:split` or `:vsplit`

## Resources

- **Vimtutor**: Run `vimtutor` in terminal for interactive tutorial
- **Built-in help**: Type `:help` in Neovim
- **Cheatsheet**: [resources/cheatsheets/basics.md](../../resources/cheatsheets/basics.md)
- **Course modules**: Start with [Module 1: Basics](../../docs/01-basics/README.md)

## Philosophy: Why Start Minimal?

1. **Learn fundamentals**: Understand Vim's language before adding shortcuts
2. **Appreciate plugins**: You'll know exactly what each plugin provides
3. **Avoid cargo cult**: Copy-paste configs without understanding what they do
4. **Build intentionally**: Add only what you need, when you need it
5. **Faster learning**: Fewer options = less cognitive load

## Upgrading Path

```
Minimal (you are here)
    ↓
Basic (add plugins)
    ↓
Language-specific (Python, Web, etc.)
    ↓
Custom (build your own perfect config)
```

---

**Remember**: The best Neovim config is one you understand completely. Start simple!
