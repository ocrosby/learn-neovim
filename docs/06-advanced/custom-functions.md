# Custom Functions

Build reusable utility functions to extend Neovim with exactly the features you need. Learn patterns for creating maintainable, powerful custom functionality.

## Why Custom Functions?

- **Solve your specific problems** - Build exactly what you need
- **No plugin overhead** - Lightweight, tailored solutions
- **Learn Neovim deeply** - Understand how things work
- **Portable** - Easy to share across configs

## Function Organization

### Simple Functions (in init.lua)

For quick utilities:

```lua
local function toggle_numbers()
  vim.opt.number = not vim.opt.number:get()
end

vim.keymap.set("n", "<leader>tn", toggle_numbers)
```

### Module Functions (in lua/utils/)

For larger collections:

**~/.config/nvim/lua/utils/init.lua**
```lua
local M = {}

function M.toggle_numbers()
  vim.opt.number = not vim.opt.number:get()
end

function M.greet(name)
  return "Hello, " .. name
end

return M
```

**~/.config/nvim/init.lua**
```lua
local utils = require("utils")
vim.keymap.set("n", "<leader>tn", utils.toggle_numbers)
```

## Practical Function Examples

### 1. Smart Buffer Delete

Close buffer without closing window:

```lua
local function buf_delete()
  local bufnr = vim.api.nvim_get_current_buf()
  local buffers = vim.fn.getbufinfo({ buflisted = 1 })
  
  if #buffers > 1 then
    vim.cmd("bprevious")
  end
  
  vim.api.nvim_buf_delete(bufnr, { force = false })
end

vim.keymap.set("n", "<leader>bd", buf_delete, { desc = "Delete buffer" })
```

### 2. Quick Grep

Grep for word under cursor:

```lua
local function grep_word()
  local word = vim.fn.expand("<cword>")
  vim.cmd("grep " .. word)
  vim.cmd("copen")
end

vim.keymap.set("n", "<leader>gw", grep_word, { desc = "Grep word under cursor" })
```

### 3. Toggle Diagnostics

Turn diagnostics on/off:

```lua
local diagnostics_enabled = true

local function toggle_diagnostics()
  diagnostics_enabled = not diagnostics_enabled
  
  if diagnostics_enabled then
    vim.diagnostic.enable()
    vim.notify("Diagnostics enabled", vim.log.levels.INFO)
  else
    vim.diagnostic.disable()
    vim.notify("Diagnostics disabled", vim.log.levels.WARN)
  end
end

vim.keymap.set("n", "<leader>td", toggle_diagnostics, { desc = "Toggle diagnostics" })
```

### 4. Smart Split Navigation

Create split or navigate if exists:

```lua
local function smart_split(direction)
  return function()
    local current_win = vim.api.nvim_get_current_win()
    vim.cmd("wincmd " .. direction)
    
    if current_win == vim.api.nvim_get_current_win() then
      if direction == "h" or direction == "l" then
        vim.cmd("vsplit")
      else
        vim.cmd("split")
      end
      vim.cmd("wincmd " .. direction)
    end
  end
end

vim.keymap.set("n", "<C-h>", smart_split("h"))
vim.keymap.set("n", "<C-j>", smart_split("j"))
vim.keymap.set("n", "<C-k>", smart_split("k"))
vim.keymap.set("n", "<C-l>", smart_split("l"))
```

### 5. Project Root Finder

Find project root and change directory:

```lua
local function find_root()
  local markers = { ".git", "package.json", "Cargo.toml", "go.mod", "pyproject.toml" }
  local path = vim.fn.expand("%:p:h")
  
  while path ~= "/" do
    for _, marker in ipairs(markers) do
      local marker_path = path .. "/" .. marker
      if vim.fn.filereadable(marker_path) == 1 or vim.fn.isdirectory(marker_path) == 1 then
        return path
      end
    end
    path = vim.fn.fnamemodify(path, ":h")
  end
  
  return vim.fn.getcwd()
end

local function cd_root()
  local root = find_root()
  vim.cmd("cd " .. root)
  vim.notify("Changed to: " .. root, vim.log.levels.INFO)
end

vim.keymap.set("n", "<leader>cd", cd_root, { desc = "CD to project root" })
```

### 6. Zoom Current Window

Toggle window zoom (maximize/restore):

```lua
local is_zoomed = false
local saved_layout = nil

local function toggle_zoom()
  if is_zoomed then
    if saved_layout then
      vim.fn.winrestview(saved_layout)
    end
    vim.cmd("wincmd =")
    is_zoomed = false
  else
    saved_layout = vim.fn.winsaveview()
    vim.cmd("wincmd |")
    vim.cmd("wincmd _")
    is_zoomed = true
  end
end

vim.keymap.set("n", "<leader>z", toggle_zoom, { desc = "Toggle window zoom" })
```

### 7. Scratch Buffer

Create a disposable scratch buffer:

```lua
local function scratch_buffer()
  local buf = vim.api.nvim_create_buf(false, true)
  vim.api.nvim_buf_set_option(buf, "bufhidden", "wipe")
  vim.api.nvim_set_current_buf(buf)
  vim.api.nvim_buf_set_lines(buf, 0, -1, false, { "-- Scratch Buffer --", "" })
end

vim.keymap.set("n", "<leader>bs", scratch_buffer, { desc = "Create scratch buffer" })
```

### 8. Rename File

Rename current file and buffer:

```lua
local function rename_file()
  local old_name = vim.fn.expand("%")
  local new_name = vim.fn.input("New name: ", old_name, "file")
  
  if new_name ~= "" and new_name ~= old_name then
    vim.cmd("saveas " .. new_name)
    vim.fn.delete(old_name)
    vim.cmd("bdelete " .. vim.fn.bufnr(old_name))
    vim.notify("Renamed to: " .. new_name, vim.log.levels.INFO)
  end
end

vim.keymap.set("n", "<leader>fr", rename_file, { desc = "Rename file" })
```

### 9. Duplicate Line/Selection

Duplicate current line or visual selection:

```lua
local function duplicate()
  local mode = vim.fn.mode()
  
  if mode == "n" then
    vim.cmd('normal! yyp')
  elseif mode == "v" or mode == "V" then
    vim.cmd('normal! y`>p')
  end
end

vim.keymap.set({ "n", "v" }, "<leader>d", duplicate, { desc = "Duplicate line/selection" })
```

### 10. Toggle Quickfix

Open/close quickfix window:

```lua
local function toggle_quickfix()
  local windows = vim.fn.getwininfo()
  
  for _, win in ipairs(windows) do
    if win.quickfix == 1 then
      vim.cmd("cclose")
      return
    end
  end
  
  vim.cmd("copen")
end

vim.keymap.set("n", "<leader>q", toggle_quickfix, { desc = "Toggle quickfix" })
```

## Advanced Patterns

### Stateful Functions

Maintain state across calls:

```lua
local state = {
  counter = 0,
  last_search = "",
}

local function increment_counter()
  state.counter = state.counter + 1
  print("Counter: " .. state.counter)
end

local function reset_counter()
  state.counter = 0
  print("Counter reset")
end
```

### Async Functions

Run operations asynchronously:

```lua
local function async_grep(pattern)
  local results = {}
  
  vim.fn.jobstart({ "rg", "--vimgrep", pattern }, {
    stdout_buffered = true,
    on_stdout = function(_, data)
      results = data
    end,
    on_exit = function()
      vim.schedule(function()
        vim.fn.setqflist({}, "r", { lines = results })
        vim.cmd("copen")
      end)
    end,
  })
end
```

### Higher-Order Functions

Functions that return functions:

```lua
local function make_toggler(option)
  return function()
    vim.opt[option] = not vim.opt[option]:get()
    print(option .. ": " .. tostring(vim.opt[option]:get()))
  end
end

vim.keymap.set("n", "<leader>tn", make_toggler("number"))
vim.keymap.set("n", "<leader>tr", make_toggler("relativenumber"))
vim.keymap.set("n", "<leader>tw", make_toggler("wrap"))
```

### Decorator Pattern

Wrap functions with additional behavior:

```lua
local function with_save(func)
  return function(...)
    local modified = vim.bo.modified
    func(...)
    if modified then
      vim.cmd("write")
    end
  end
end

local function format_buffer()
  vim.lsp.buf.format()
end

local format_and_save = with_save(format_buffer)
```

## Building a Utility Module

**~/.config/nvim/lua/utils/buffer.lua**
```lua
local M = {}

function M.delete()
  local bufnr = vim.api.nvim_get_current_buf()
  local buffers = vim.fn.getbufinfo({ buflisted = 1 })
  
  if #buffers > 1 then
    vim.cmd("bprevious")
  end
  
  vim.api.nvim_buf_delete(bufnr, { force = false })
end

function M.delete_others()
  local current = vim.api.nvim_get_current_buf()
  local buffers = vim.fn.getbufinfo({ buflisted = 1 })
  
  for _, buf in ipairs(buffers) do
    if buf.bufnr ~= current then
      vim.api.nvim_buf_delete(buf.bufnr, { force = false })
    end
  end
end

function M.scratch()
  local buf = vim.api.nvim_create_buf(false, true)
  vim.api.nvim_set_current_buf(buf)
end

return M
```

**~/.config/nvim/lua/utils/init.lua**
```lua
return {
  buffer = require("utils.buffer"),
}
```

**~/.config/nvim/init.lua**
```lua
local utils = require("utils")

vim.keymap.set("n", "<leader>bd", utils.buffer.delete)
vim.keymap.set("n", "<leader>bo", utils.buffer.delete_others)
vim.keymap.set("n", "<leader>bs", utils.buffer.scratch)
```

## Testing Functions

### Manual Testing

```lua
:lua require("utils").buffer.delete()
```

### Debug Prints

```lua
local function debug_func()
  print(vim.inspect(vim.fn.getbufinfo()))
end
```

### Error Handling

```lua
local function safe_func()
  local ok, result = pcall(function()
    return risky_operation()
  end)
  
  if not ok then
    vim.notify("Error: " .. result, vim.log.levels.ERROR)
    return
  end
  
  return result
end
```

## Documentation

Document your functions:

```lua
--- Toggle line numbers on/off
--- @return nil
local function toggle_numbers()
  vim.opt.number = not vim.opt.number:get()
  vim.opt.relativenumber = not vim.opt.relativenumber:get()
end

--- Find project root directory
--- @param markers table? List of root markers (default: {".git", "package.json"})
--- @return string Root directory path
local function find_root(markers)
  markers = markers or { ".git", "package.json" }
  -- Implementation
end
```

## Best Practices

1. **Keep functions focused** - One responsibility per function
2. **Use local** - Declare all variables as local
3. **Handle errors** - Use pcall for risky operations
4. **Provide feedback** - Use vim.notify for user feedback
5. **Make it reusable** - Parameterize where possible
6. **Document** - Add docstrings for complex functions
7. **Test thoroughly** - Test edge cases and error conditions

## Common Patterns

### User Input

```lua
local input = vim.fn.input("Enter value: ")
local choice = vim.fn.confirm("Save changes?", "&Yes\n&No\n&Cancel")
```

### Notifications

```lua
vim.notify("Success!", vim.log.levels.INFO)
vim.notify("Warning!", vim.log.levels.WARN)
vim.notify("Error!", vim.log.levels.ERROR)
```

### Cursor Position

```lua
local cursor = vim.api.nvim_win_get_cursor(0)
vim.api.nvim_win_set_cursor(0, { line, col })
```

### Buffer Content

```lua
local lines = vim.api.nvim_buf_get_lines(0, 0, -1, false)
vim.api.nvim_buf_set_lines(0, 0, -1, false, { "New content" })
```

## Performance Tips

1. **Cache expensive calls**
2. **Use local variables**
3. **Batch API calls**
4. **Avoid loops in hot paths**
5. **Use vim.schedule for async work**

## Exercises

1. **Toggle function** - Create a function to toggle between light/dark colorscheme
2. **Buffer utils** - Build a module for buffer management utilities
3. **Note taker** - Create a function to quickly create dated notes
4. **Code runner** - Build a function to run code for your language
5. **Custom workflow** - Solve a specific problem in your workflow

## Next Steps

You've completed the Advanced module! Continue to [Module 7: Workflows](../07-workflows/README.md) to integrate everything into complete development workflows.

## Resources

- [Neovim Lua API](https://neovim.io/doc/user/lua.html)
- [Lua Programming](https://www.lua.org/manual/5.1/)
- [nvim-lua-guide](https://github.com/nanotee/nvim-lua-guide)
