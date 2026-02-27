# Git Integration

Integrate Git seamlessly into your Neovim workflow with powerful plugins and native features. Never leave your editor for version control.

## Core Git Plugins

### 1. gitsigns.nvim

Visual git diff and hunk management in the sign column.

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
      untracked = { text = "┆" },
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
      end, { expr = true, desc = "Next hunk" })

      map("n", "[c", function()
        if vim.wo.diff then return "[c" end
        vim.schedule(function() gs.prev_hunk() end)
        return "<Ignore>"
      end, { expr = true, desc = "Prev hunk" })

      map("n", "<leader>hs", gs.stage_hunk, { desc = "Stage hunk" })
      map("n", "<leader>hr", gs.reset_hunk, { desc = "Reset hunk" })
      map("v", "<leader>hs", function() gs.stage_hunk({ vim.fn.line("."), vim.fn.line("v") }) end, { desc = "Stage selection" })
      map("v", "<leader>hr", function() gs.reset_hunk({ vim.fn.line("."), vim.fn.line("v") }) end, { desc = "Reset selection" })
      
      map("n", "<leader>hS", gs.stage_buffer, { desc = "Stage buffer" })
      map("n", "<leader>hu", gs.undo_stage_hunk, { desc = "Undo stage" })
      map("n", "<leader>hR", gs.reset_buffer, { desc = "Reset buffer" })
      
      map("n", "<leader>hp", gs.preview_hunk, { desc = "Preview hunk" })
      map("n", "<leader>hb", function() gs.blame_line({ full = true }) end, { desc = "Blame line" })
      map("n", "<leader>tb", gs.toggle_current_line_blame, { desc = "Toggle blame" })
      map("n", "<leader>hd", gs.diffthis, { desc = "Diff this" })
      map("n", "<leader>hD", function() gs.diffthis("~") end, { desc = "Diff ~" })
      
      map({ "o", "x" }, "ih", ":<C-U>Gitsigns select_hunk<CR>", { desc = "Select hunk" })
    end,
  },
}
```

**Key Features**:
- Visual indicators for changes
- Stage/unstage hunks
- Preview diffs
- Navigate between changes
- Inline blame

### 2. vim-fugitive

Full-featured Git wrapper for Neovim.

```lua
{
  "tpope/vim-fugitive",
  cmd = { "Git", "G", "Gdiffsplit", "Gread", "Gwrite", "Ggrep", "GMove", "GRename", "GDelete", "GBrowse" },
  keys = {
    { "<leader>gs", "<cmd>Git<cr>", desc = "Git status" },
    { "<leader>gc", "<cmd>Git commit<cr>", desc = "Git commit" },
    { "<leader>gp", "<cmd>Git push<cr>", desc = "Git push" },
    { "<leader>gl", "<cmd>Git pull<cr>", desc = "Git pull" },
    { "<leader>gd", "<cmd>Gdiffsplit<cr>", desc = "Git diff" },
    { "<leader>gb", "<cmd>Git blame<cr>", desc = "Git blame" },
  },
}
```

**Key Commands**:
- `:Git` - Git status (stage with `-`, commit with `cc`)
- `:Git commit` - Commit with message
- `:Git push` - Push to remote
- `:Git pull` - Pull from remote
- `:Gdiffsplit` - Split diff view
- `:Git blame` - Show blame annotations

### 3. diffview.nvim

Enhanced diff viewing and merge conflict resolution.

```lua
{
  "sindrets/diffview.nvim",
  dependencies = "nvim-lua/plenary.nvim",
  cmd = { "DiffviewOpen", "DiffviewFileHistory" },
  keys = {
    { "<leader>dv", "<cmd>DiffviewOpen<cr>", desc = "Diff view" },
    { "<leader>dh", "<cmd>DiffviewFileHistory<cr>", desc = "File history" },
    { "<leader>dc", "<cmd>DiffviewClose<cr>", desc = "Close diff" },
  },
  opts = {},
}
```

**Key Features**:
- Side-by-side diffs
- File history browser
- Merge conflict resolution
- Stage/unstage from diff

### 4. neogit

Magit-like Git interface for Neovim.

```lua
{
  "NeogitOrg/neogit",
  dependencies = {
    "nvim-lua/plenary.nvim",
    "sindrets/diffview.nvim",
    "nvim-telescope/telescope.nvim",
  },
  cmd = "Neogit",
  keys = {
    { "<leader>gg", "<cmd>Neogit<cr>", desc = "Neogit" },
  },
  opts = {
    integrations = {
      diffview = true,
      telescope = true,
    },
  },
}
```

**Key Features**:
- Interactive Git UI
- Stage/unstage files
- Commit, push, pull
- Branch management
- Stash management

## Git Workflows

### Basic Workflow

1. **Check Status**
   ```vim
   :Git
   " Or use neogit
   :Neogit
   ```

2. **View Changes**
   ```vim
   " Navigate hunks
   ]c / [c
   
   " Preview hunk
   <leader>hp
   ```

3. **Stage Changes**
   ```vim
   " Stage current hunk
   <leader>hs
   
   " Stage entire file
   <leader>hS
   ```

4. **Commit**
   ```vim
   :Git commit
   " Write message, :wq to commit
   ```

5. **Push**
   ```vim
   :Git push
   ```

### Interactive Staging (Fugitive)

1. Open `:Git`
2. Navigate to file with `j/k`
3. Press `-` to stage/unstage file
4. Press `=` to see inline diff
5. Press `cc` to commit
6. Write message, `:wq` to commit

### Merge Conflict Resolution

Using **diffview.nvim**:

1. Open conflict file
2. `:DiffviewOpen`
3. Navigate conflicts with `[x` / `]x`
4. Choose version:
   - `<leader>co` - Choose ours
   - `<leader>ct` - Choose theirs
   - `<leader>cb` - Choose both
   - `<leader>c0` - Choose none
5. `:DiffviewClose`
6. Stage resolved files

### Branch Management

```vim
" Create branch
:Git checkout -b feature-name

" Switch branch
:Git checkout main

" List branches
:Git branch

" Delete branch
:Git branch -d feature-name
```

### Git Log and History

```vim
" View log
:Git log

" File history with diffview
:DiffviewFileHistory

" View specific commit
:Git show abc123

" Search commits
:Git log --grep="search term"
```

## Advanced Gitsigns Usage

### Inline Blame

```lua
require("gitsigns").toggle_current_line_blame()
```

Shows author and date for current line.

### Hunk Text Object

```vim
" Select hunk
vih

" Delete hunk
dih

" Yank hunk
yih
```

### Stage Buffer Partially

Visual select lines, then `<leader>hs` to stage selection.

### Diff Against Branch

```vim
:Gitsigns diffthis main
```

## Git Commands from Neovim

### Using vim.fn.system

```lua
local function git_branch()
  local branch = vim.fn.system("git branch --show-current")
  return branch:gsub("\n", "")
end

print(git_branch())
```

### Using Terminal

```lua
vim.keymap.set("n", "<leader>gt", ":terminal git ", { desc = "Git terminal" })
```

### Custom Git Functions

```lua
local function git_push()
  vim.cmd("Git push")
  vim.notify("Pushing...", vim.log.levels.INFO)
end

local function git_pull()
  vim.cmd("Git pull")
  vim.notify("Pulling...", vim.log.levels.INFO)
end

vim.keymap.set("n", "<leader>gp", git_push, { desc = "Git push" })
vim.keymap.set("n", "<leader>gP", git_pull, { desc = "Git pull" })
```

## GitHub Integration

### vim-rhubarb

GitHub integration for fugitive:

```lua
{
  "tpope/vim-rhubarb",
  dependencies = "tpope/vim-fugitive",
}
```

**Features**:
- `:GBrowse` - Open file/line on GitHub
- Works with fugitive commands

### octo.nvim

Full GitHub UI in Neovim:

```lua
{
  "pwntester/octo.nvim",
  dependencies = {
    "nvim-lua/plenary.nvim",
    "nvim-telescope/telescope.nvim",
    "nvim-tree/nvim-web-devicons",
  },
  cmd = "Octo",
  opts = {},
}
```

**Features**:
- View/create issues
- Review PRs
- Comment on code
- Manage labels/assignees

## Status Line Git Info

Show branch in status line:

```lua
{
  "nvim-lualine/lualine.nvim",
  opts = {
    sections = {
      lualine_b = {
        "branch",
        "diff",
        "diagnostics",
      },
    },
  },
}
```

## Best Practices

1. **Commit often** - Small, focused commits
2. **Write good messages** - Explain why, not what
3. **Review before staging** - Use `<leader>hp` to preview
4. **Use branches** - Keep main clean
5. **Pull before push** - Avoid conflicts
6. **Resolve conflicts immediately** - Don't let them pile up

## Keybinding Reference

| Key | Action | Plugin |
|-----|--------|--------|
| `]c` | Next hunk | gitsigns |
| `[c` | Previous hunk | gitsigns |
| `<leader>hs` | Stage hunk | gitsigns |
| `<leader>hr` | Reset hunk | gitsigns |
| `<leader>hp` | Preview hunk | gitsigns |
| `<leader>hb` | Blame line | gitsigns |
| `<leader>gs` | Git status | fugitive |
| `<leader>gc` | Git commit | fugitive |
| `<leader>gp` | Git push | fugitive |
| `<leader>gd` | Git diff | fugitive |
| `<leader>gg` | Neogit | neogit |
| `<leader>dv` | Diff view | diffview |

## Complete Git Config Example

```lua
return {
  {
    "lewis6991/gitsigns.nvim",
    event = "BufReadPre",
    opts = {
      signs = {
        add = { text = "│" },
        change = { text = "│" },
        delete = { text = "_" },
      },
      on_attach = function(bufnr)
        local gs = package.loaded.gitsigns
        vim.keymap.set("n", "]c", gs.next_hunk, { buffer = bufnr })
        vim.keymap.set("n", "[c", gs.prev_hunk, { buffer = bufnr })
        vim.keymap.set("n", "<leader>hs", gs.stage_hunk, { buffer = bufnr })
        vim.keymap.set("n", "<leader>hr", gs.reset_hunk, { buffer = bufnr })
        vim.keymap.set("n", "<leader>hp", gs.preview_hunk, { buffer = bufnr })
      end,
    },
  },

  {
    "tpope/vim-fugitive",
    cmd = "Git",
    keys = {
      { "<leader>gs", "<cmd>Git<cr>" },
      { "<leader>gc", "<cmd>Git commit<cr>" },
    },
  },

  {
    "sindrets/diffview.nvim",
    cmd = "DiffviewOpen",
    keys = {
      { "<leader>dv", "<cmd>DiffviewOpen<cr>" },
    },
    opts = {},
  },
}
```

## Exercises

1. **Setup gitsigns** - Install and configure gitsigns
2. **Stage hunks** - Practice staging individual hunks
3. **Use fugitive** - Commit using `:Git` interface
4. **Resolve conflict** - Create and resolve a merge conflict
5. **Review diff** - Use diffview to review changes

## Next Steps

Continue to [Debugging](debugging.md) to learn how to debug code from within Neovim.

## Resources

- [gitsigns.nvim](https://github.com/lewis6991/gitsigns.nvim)
- [vim-fugitive](https://github.com/tpope/vim-fugitive)
- [diffview.nvim](https://github.com/sindrets/diffview.nvim)
- [neogit](https://github.com/NeogitOrg/neogit)
- [Git Documentation](https://git-scm.com/doc)
