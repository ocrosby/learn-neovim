# Autocommands

Autocommands (autocmds) let you automatically execute code when specific events occur in Neovim. Automate repetitive tasks and customize behavior without manual intervention.

## What Are Autocommands?

Autocommands trigger actions based on events:
- **BufWritePre** - Before saving a file
- **BufEnter** - When entering a buffer
- **FileType** - When a file type is detected
- **VimEnter** - When Neovim starts

## Basic Syntax

### Vimscript (Old Way)

```vim
autocmd BufWritePre * echo "Saving..."
```

### Lua (Modern Way)

```lua
vim.api.nvim_create_autocmd("BufWritePre", {
  pattern = "*",
  callback = function()
    print("Saving...")
  end,
})
```

## Common Events

| Event | When It Triggers |
|-------|------------------|
| `VimEnter` | After Neovim starts |
| `BufReadPre` | Before reading a buffer |
| `BufRead`, `BufReadPost` | After reading a buffer |
| `BufNewFile` | When creating a new file |
| `BufWritePre` | Before writing a buffer |
| `BufWrite`, `BufWritePost` | After writing a buffer |
| `BufEnter` | When entering a buffer |
| `BufLeave` | When leaving a buffer |
| `FileType` | When file type is set |
| `InsertEnter` | When entering insert mode |
| `InsertLeave` | When leaving insert mode |
| `CursorHold` | When cursor hasn't moved (updatetime) |
| `TextYankPost` | After yanking text |
| `VimResized` | When window is resized |
| `ColorScheme` | After loading a colorscheme |

## Practical Examples

### 1. Highlight on Yank

Flash highlighted text when you yank:

```lua
vim.api.nvim_create_autocmd("TextYankPost", {
  desc = "Highlight when yanking text",
  callback = function()
    vim.highlight.on_yank({ higroup = "IncSearch", timeout = 200 })
  end,
})
```

### 2. Auto-format on Save

Format code before saving:

```lua
vim.api.nvim_create_autocmd("BufWritePre", {
  pattern = { "*.lua", "*.py", "*.js" },
  callback = function()
    vim.lsp.buf.format({ async = false })
  end,
})
```

### 3. Remove Trailing Whitespace

Strip trailing spaces before saving:

```lua
vim.api.nvim_create_autocmd("BufWritePre", {
  pattern = "*",
  callback = function()
    local save = vim.fn.winsaveview()
    vim.cmd([[%s/\s\+$//e]])
    vim.fn.winrestview(save)
  end,
})
```

### 4. File Type Specific Settings

Configure settings per file type:

```lua
vim.api.nvim_create_autocmd("FileType", {
  pattern = "python",
  callback = function()
    vim.opt_local.tabstop = 4
    vim.opt_local.shiftwidth = 4
    vim.opt_local.expandtab = true
  end,
})

vim.api.nvim_create_autocmd("FileType", {
  pattern = { "markdown", "text" },
  callback = function()
    vim.opt_local.spell = true
    vim.opt_local.wrap = true
  end,
})
```

### 5. Auto-create Parent Directories

Create directories when saving new files:

```lua
vim.api.nvim_create_autocmd("BufWritePre", {
  callback = function()
    local dir = vim.fn.expand("<afile>:p:h")
    if vim.fn.isdirectory(dir) == 0 then
      vim.fn.mkdir(dir, "p")
    end
  end,
})
```

### 6. Return to Last Position

Jump to last cursor position when opening files:

```lua
vim.api.nvim_create_autocmd("BufReadPost", {
  callback = function()
    local mark = vim.api.nvim_buf_get_mark(0, '"')
    local lcount = vim.api.nvim_buf_line_count(0)
    if mark[1] > 0 and mark[1] <= lcount then
      pcall(vim.api.nvim_win_set_cursor, 0, mark)
    end
  end,
})
```

### 7. Close Certain Windows with q

Press `q` to close help, quickfix, etc:

```lua
vim.api.nvim_create_autocmd("FileType", {
  pattern = { "help", "qf", "lspinfo", "man" },
  callback = function(event)
    vim.bo[event.buf].buflisted = false
    vim.keymap.set("n", "q", "<cmd>close<cr>", { buffer = event.buf })
  end,
})
```

### 8. Auto-save

Auto-save when leaving insert mode or buffer:

```lua
vim.api.nvim_create_autocmd({ "InsertLeave", "TextChanged" }, {
  pattern = "*",
  callback = function()
    if vim.bo.modified and vim.fn.expand("%") ~= "" then
      vim.cmd("silent! write")
    end
  end,
})
```

### 9. Check for External File Changes

Reload file if changed externally:

```lua
vim.api.nvim_create_autocmd({ "FocusGained", "TermClose", "TermLeave" }, {
  callback = function()
    vim.cmd("checktime")
  end,
})
```

### 10. Disable Line Numbers in Terminal

```lua
vim.api.nvim_create_autocmd("TermOpen", {
  callback = function()
    vim.opt_local.number = false
    vim.opt_local.relativenumber = false
  end,
})
```

## Autocommand Groups

Group related autocommands for organization and clearing:

```lua
local augroup = vim.api.nvim_create_augroup("MyAutoCommands", { clear = true })

vim.api.nvim_create_autocmd("BufWritePre", {
  group = augroup,
  pattern = "*.lua",
  callback = function()
    vim.lsp.buf.format()
  end,
})

vim.api.nvim_create_autocmd("BufWritePost", {
  group = augroup,
  pattern = "*.lua",
  callback = function()
    print("Lua file saved!")
  end,
})
```

Benefits of groups:
- **Organization** - Related autocmds together
- **Clear on reload** - `clear = true` removes old autocmds
- **Easy management** - Enable/disable groups

## Pattern Matching

### Wildcards

```lua
vim.api.nvim_create_autocmd("BufRead", {
  pattern = "*.lua",
})
```

### Multiple Patterns

```lua
vim.api.nvim_create_autocmd("BufRead", {
  pattern = { "*.lua", "*.vim", "*.py" },
})
```

### Specific Paths

```lua
vim.api.nvim_create_autocmd("BufRead", {
  pattern = "/home/user/projects/*",
})
```

## Callback vs Command

### Using Callback (Recommended)

```lua
vim.api.nvim_create_autocmd("BufWritePre", {
  callback = function()
    vim.lsp.buf.format()
  end,
})
```

### Using Command

```lua
vim.api.nvim_create_autocmd("BufWritePre", {
  command = "lua vim.lsp.buf.format()",
})
```

## Advanced Examples

### Smart Tab Completion

```lua
vim.api.nvim_create_autocmd("InsertCharPre", {
  callback = function()
    if vim.fn.pumvisible() == 0 and vim.v.char:match("%s") then
      vim.fn.feedkeys(vim.api.nvim_replace_termcodes("<C-x><C-o>", true, true, true), "n")
    end
  end,
})
```

### Auto-compile on Save

```lua
vim.api.nvim_create_autocmd("BufWritePost", {
  pattern = "*.tex",
  callback = function()
    vim.fn.jobstart("pdflatex " .. vim.fn.expand("%"))
  end,
})
```

### Project-Specific Config

```lua
vim.api.nvim_create_autocmd("BufEnter", {
  pattern = "/path/to/project/*",
  callback = function()
    vim.opt_local.tabstop = 2
    vim.opt_local.shiftwidth = 2
  end,
})
```

### LSP Attach Autocommand

```lua
vim.api.nvim_create_autocmd("LspAttach", {
  callback = function(args)
    local bufnr = args.buf
    local client = vim.lsp.get_client_by_id(args.data.client_id)
    
    if client.supports_method("textDocument/formatting") then
      vim.api.nvim_create_autocmd("BufWritePre", {
        buffer = bufnr,
        callback = function()
          vim.lsp.buf.format({ bufnr = bufnr })
        end,
      })
    end
  end,
})
```

## Buffer-Specific Autocommands

Autocommands can be buffer-specific:

```lua
vim.api.nvim_create_autocmd("BufWritePre", {
  buffer = bufnr,
  callback = function()
    print("Saving this specific buffer")
  end,
})
```

## Once-Only Autocommands

Run an autocommand only once:

```lua
vim.api.nvim_create_autocmd("VimEnter", {
  once = true,
  callback = function()
    print("This runs once on startup")
  end,
})
```

## Debugging Autocommands

### List All Autocommands

```vim
:autocmd
```

### List Specific Event

```vim
:autocmd BufWritePre
```

### List Specific Group

```vim
:autocmd MyGroup
```

### Test Callback

```lua
vim.api.nvim_create_autocmd("BufWritePre", {
  callback = function()
    print("Event triggered!")
    print("Buffer:", vim.fn.expand("<afile>"))
  end,
})
```

## Performance Considerations

### Avoid Heavy Operations

Bad (runs on every keystroke):
```lua
vim.api.nvim_create_autocmd("TextChanged", {
  callback = function()
    vim.fn.system("some-expensive-command")
  end,
})
```

Good (debounced):
```lua
local timer = vim.loop.new_timer()
vim.api.nvim_create_autocmd("TextChanged", {
  callback = function()
    timer:stop()
    timer:start(1000, 0, vim.schedule_wrap(function()
      vim.fn.system("some-expensive-command")
    end))
  end,
})
```

### Be Specific with Patterns

Bad (runs for all files):
```lua
vim.api.nvim_create_autocmd("BufRead", {
  pattern = "*",
  callback = function() ... end,
})
```

Good (runs only for specific files):
```lua
vim.api.nvim_create_autocmd("BufRead", {
  pattern = { "*.lua", "*.py" },
  callback = function() ... end,
})
```

## Best Practices

1. **Use groups** - Organize related autocommands
2. **Clear groups** - Set `clear = true` to prevent duplicates
3. **Be specific** - Use precise patterns to avoid unnecessary triggers
4. **Use desc** - Add descriptions for clarity
5. **Error handling** - Wrap risky code in pcall
6. **Performance** - Avoid heavy operations in frequently-triggered events

## Common Pitfalls

### Duplicate Autocommands

Problem: Autocommands stack when reloading config

Solution: Use groups with `clear = true`:
```lua
local group = vim.api.nvim_create_augroup("MyGroup", { clear = true })
```

### Wrong Pattern

Problem: Pattern doesn't match files

Solution: Test patterns carefully:
```lua
pattern = "*.py"  -- Correct
pattern = ".py"   -- Wrong (no wildcard)
```

## Complete Example

Here's a complete autocommands configuration:

```lua
local augroup = vim.api.nvim_create_augroup("UserAutoCommands", { clear = true })

vim.api.nvim_create_autocmd("TextYankPost", {
  group = augroup,
  desc = "Highlight on yank",
  callback = function()
    vim.highlight.on_yank({ timeout = 200 })
  end,
})

vim.api.nvim_create_autocmd("BufWritePre", {
  group = augroup,
  desc = "Remove trailing whitespace",
  callback = function()
    local save = vim.fn.winsaveview()
    vim.cmd([[%s/\s\+$//e]])
    vim.fn.winrestview(save)
  end,
})

vim.api.nvim_create_autocmd("FileType", {
  group = augroup,
  desc = "Close with q",
  pattern = { "help", "qf", "man", "lspinfo" },
  callback = function(event)
    vim.bo[event.buf].buflisted = false
    vim.keymap.set("n", "q", "<cmd>close<cr>", { buffer = event.buf })
  end,
})

vim.api.nvim_create_autocmd("BufReadPost", {
  group = augroup,
  desc = "Go to last position",
  callback = function()
    local mark = vim.api.nvim_buf_get_mark(0, '"')
    if mark[1] > 0 and mark[1] <= vim.api.nvim_buf_line_count(0) then
      pcall(vim.api.nvim_win_set_cursor, 0, mark)
    end
  end,
})
```

## Exercises

1. **Highlight yank** - Add the yank highlighting autocommand
2. **File-type settings** - Create autocommands for your common file types
3. **Auto-format** - Set up format-on-save for your languages
4. **Project config** - Create project-specific autocommands
5. **Custom workflow** - Build an autocommand for your specific workflow

## Next Steps

Continue to [Custom Functions](custom-functions.md) to learn how to build reusable utility functions.

## Resources

- [Neovim Autocommand Docs](https://neovim.io/doc/user/autocmd.html)
- [Neovim Lua API](https://neovim.io/doc/user/lua.html)
- [Event List](https://neovim.io/doc/user/autocmd.html#autocmd-events)
