# Essential Plugins Cheatsheet

Quick reference for the most common Neovim plugins and their keybindings.

## Plugin Manager - lazy.nvim

### Commands

```vim
:Lazy                " Open Lazy UI
:Lazy sync           " Install missing + update plugins
:Lazy update         " Update plugins
:Lazy clean          " Remove unused plugins
:Lazy profile        " Show startup profiling
:Lazy log            " Show log
:Lazy check          " Check for updates
```

### UI Navigation

| Key | Action |
|-----|--------|
| `U` | Update all |
| `I` | Install missing |
| `X` | Clean unused |
| `C` | Check updates |
| `L` | Show log |
| `P` | Profile |
| `q` | Quit |

---

## Telescope - Fuzzy Finder

### Common Pickers

| Command | Keybinding | Description |
|---------|------------|-------------|
| `:Telescope find_files` | `<leader>ff` | Find files |
| `:Telescope live_grep` | `<leader>fg` | Search in files |
| `:Telescope buffers` | `<leader>fb` | List buffers |
| `:Telescope help_tags` | `<leader>fh` | Search help |
| `:Telescope oldfiles` | `<leader>fr` | Recent files |
| `:Telescope grep_string` | `<leader>fw` | Search word under cursor |
| `:Telescope git_files` | `<leader>gf` | Git files |
| `:Telescope git_commits` | `<leader>gc` | Git commits |

### Navigation in Picker

| Key | Action |
|-----|--------|
| `<C-j>` / `<C-n>` | Next item |
| `<C-k>` / `<C-p>` | Previous item |
| `<CR>` | Select item |
| `<C-x>` | Open in horizontal split |
| `<C-v>` | Open in vertical split |
| `<C-t>` | Open in new tab |
| `<C-u>` | Scroll preview up |
| `<C-d>` | Scroll preview down |
| `<C-/>` / `?` | Show keymaps |
| `<Esc>` | Close |

---

## nvim-tree - File Explorer

### Basic Commands

```vim
:NvimTreeToggle      " Toggle tree
:NvimTreeFocus       " Focus tree
:NvimTreeFindFile    " Find current file
:NvimTreeCollapse    " Collapse all
```

### Navigation & Actions

| Key | Action |
|-----|--------|
| `<CR>` | Open file/folder |
| `o` | Open file/folder |
| `<Tab>` | Preview file |
| `H` | Toggle hidden files |
| `R` | Refresh |
| `-` | Go to parent directory |
| `a` | Create file/folder |
| `d` | Delete |
| `r` | Rename |
| `x` | Cut |
| `c` | Copy |
| `p` | Paste |
| `y` | Copy name |
| `Y` | Copy relative path |
| `gy` | Copy absolute path |
| `s` | Open with system app |
| `q` | Close |

---

## Treesitter - Syntax Highlighting

### Commands

```vim
:TSInstall <lang>    " Install language parser
:TSUpdate            " Update parsers
:TSUninstall <lang>  " Remove parser
:TSModuleInfo        " Show module info
```

### Text Objects (if enabled)

| Key | Action |
|-----|--------|
| `vaf` | Select outer function |
| `vif` | Select inner function |
| `vac` | Select outer class |
| `vic` | Select inner class |

---

## Gitsigns - Git Integration

### Navigation

| Key | Command | Description |
|-----|---------|-------------|
| `]c` | `next_hunk()` | Next change |
| `[c` | `prev_hunk()` | Previous change |

### Actions

| Key | Command | Description |
|-----|---------|-------------|
| `<leader>hs` | `stage_hunk()` | Stage hunk |
| `<leader>hr` | `reset_hunk()` | Reset hunk |
| `<leader>hS` | `stage_buffer()` | Stage buffer |
| `<leader>hu` | `undo_stage_hunk()` | Undo stage |
| `<leader>hR` | `reset_buffer()` | Reset buffer |
| `<leader>hp` | `preview_hunk()` | Preview hunk |
| `<leader>hb` | `blame_line()` | Show blame |
| `<leader>hd` | `diffthis()` | Diff this |

---

## Comment.nvim - Commenting

### Normal Mode

| Key | Action |
|-----|--------|
| `gcc` | Toggle comment on line |
| `gbc` | Toggle block comment on line |
| `gc{motion}` | Comment using motion |
| `gc3j` | Comment next 3 lines |
| `gcap` | Comment paragraph |

### Visual Mode

| Key | Action |
|-----|--------|
| `gc` | Toggle line comment |
| `gb` | Toggle block comment |

---

## nvim-autopairs - Auto Close Brackets

### Insert Mode

Automatically closes:
- `(` → `()` with cursor in middle
- `{` → `{}` with cursor in middle
- `[` → `[]` with cursor in middle
- `"` → `""` with cursor in middle
- `'` → `''` with cursor in middle

### Special

- `<CR>` - Smart newline (expands brackets)
- `<BS>` - Smart backspace (deletes pair)

---

## which-key - Keybinding Helper

Automatically shows available keybindings after you type a leader key.

### Usage

1. Type `<leader>` (Space)
2. Wait ~300ms
3. See available commands

No special commands needed - works automatically!

---

## Lualine - Status Line

Displays automatically at bottom. No keybindings needed.

### Components Shown

- **Mode** (Normal, Insert, Visual, etc.)
- **Git branch**
- **Git diff** (additions, modifications, deletions)
- **Diagnostics** (errors, warnings)
- **File name**
- **File encoding** (utf-8, etc.)
- **File format** (unix, dos, mac)
- **File type**
- **Progress** (position in file)
- **Location** (line:column)

---

## Bufferline - Buffer Tabs

### Navigation

| Key | Action |
|-----|--------|
| `<S-h>` | Previous buffer |
| `<S-l>` | Next buffer |
| `<leader>bp` | Toggle pin |
| `<leader>bd` | Delete buffer |

### Mouse

- Click buffer to switch
- Middle-click to close

---

## nvim-cmp - Autocompletion

### Insert Mode

| Key | Action |
|-----|--------|
| `<C-Space>` | Trigger completion |
| `<C-j>` / `<C-n>` | Next item |
| `<C-k>` / `<C-p>` | Previous item |
| `<CR>` | Confirm selection |
| `<C-e>` | Close menu |
| `<C-b>` | Scroll docs up |
| `<C-f>` | Scroll docs down |
| `<Tab>` | Next snippet placeholder (if snippets enabled) |
| `<S-Tab>` | Previous snippet placeholder |

---

## Mason - LSP Manager

### Commands

```vim
:Mason               " Open Mason UI
:MasonInstall <pkg>  " Install package
:MasonUninstall <pkg>" Uninstall package
:MasonUpdate         " Update all
:MasonLog            " View log
```

### UI Navigation

| Key | Action |
|-----|--------|
| `i` | Install package |
| `u` | Update package |
| `X` | Uninstall package |
| `U` | Update all |
| `/` | Filter packages |
| `g?` | Show help |
| `q` | Close |

---

## neotest - Test Runner

### Commands

| Key | Command | Description |
|-----|---------|-------------|
| `<leader>tn` | `run.run()` | Run nearest test |
| `<leader>tf` | `run.run(vim.fn.expand("%"))` | Run file tests |
| `<leader>ta` | `run.run(vim.fn.getcwd())` | Run all tests |
| `<leader>ts` | `summary.toggle()` | Toggle summary |
| `<leader>to` | `output.open()` | Show output |
| `<leader>tO` | `output_panel.toggle()` | Toggle panel |

### Summary Tree

| Key | Action |
|-----|--------|
| `<CR>` | Jump to test |
| `o` | Show output |
| `r` | Run test |
| `d` | Debug test |
| `s` | Stop test |

---

## nvim-dap - Debugger

### Commands

| Key | Command | Description |
|-----|---------|-------------|
| `<leader>db` | `toggle_breakpoint()` | Toggle breakpoint |
| `<leader>dc` | `continue()` | Start/continue |
| `<leader>di` | `step_into()` | Step into |
| `<leader>do` | `step_over()` | Step over |
| `<leader>dO` | `step_out()` | Step out |
| `<leader>dr` | `repl.open()` | Open REPL |
| `<leader>dl` | `run_last()` | Run last config |
| `<leader>dt` | `terminate()` | Terminate session |

### DAP UI

| Key | Command | Description |
|-----|---------|-------------|
| `<leader>du` | `toggle()` | Toggle UI |

---

## vim-fugitive - Git

### Commands

```vim
:Git                 " Git status
:Git commit          " Commit
:Git push            " Push
:Git pull            " Pull
:Git blame           " Show blame
:Gdiffsplit          " Diff split
:Gread               " Checkout current file
:Gwrite              " Stage current file
```

### In Status Buffer

| Key | Action |
|-----|--------|
| `s` | Stage file |
| `u` | Unstage file |
| `-` | Stage/unstage file |
| `=` | Inline diff |
| `cc` | Commit |
| `ca` | Amend commit |
| `q` | Close |

---

## Additional Quick Tips

### Universal Patterns

Most plugins follow these conventions:

- `<leader>` - Primary actions (Space by default)
- `]` / `[` - Next/previous navigation
- `g` prefix - Go to / Get commands
- `<CR>` - Confirm/select
- `q` - Quit/close windows
- `?` - Help/show keymaps

### Finding Plugin Keybindings

```vim
:map                 " Show all mappings
:map <leader>        " Show leader mappings
:Telescope keymaps   " Search keymaps with Telescope
```

### Getting Plugin Help

```vim
:help <plugin-name>  " e.g., :help telescope
:checkhealth         " Verify plugin installation
```

---

**Print this for quick reference while you learn each plugin!**
