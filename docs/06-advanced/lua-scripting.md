# Lua Scripting for Neovim

Master Lua scripting to extend and customize Neovim beyond what plugins offer. Write your own utilities, functions, and integrations.

## Why Lua for Neovim?

- **Native integration** - Neovim's built-in language
- **Fast** - Much faster than Vimscript
- **Modern** - Cleaner syntax than Vimscript
- **First-class** - Full access to Neovim API

## Lua Basics Quick Reference

### Variables and Types

```lua
local name = "John"           -- string
local age = 30                -- number
local is_active = true        -- boolean
local items = { 1, 2, 3 }     -- table (array)
local config = { key = "val" } -- table (dict)
```

### Functions

```lua
local function greet(name)
  return "Hello, " .. name
end

local result = greet("World")
```

### Conditionals

```lua
if age > 18 then
  print("Adult")
elseif age > 13 then
  print("Teen")
else
  print("Child")
end
```

### Loops

```lua
for i = 1, 10 do
  print(i)
end

for index, value in ipairs(items) do
  print(index, value)
end

for key, value in pairs(config) do
  print(key, value)
end
```

### Tables

```lua
local person = {
  name = "John",
  age = 30,
  greet = function(self)
    print("Hello, I'm " .. self.name)
  end
}

person:greet()
```

## Neovim Lua API

The `vim` global table provides access to all Neovim functionality.

### vim.cmd

Execute Ex commands:

```lua
vim.cmd("colorscheme tokyonight")
vim.cmd("set number")
vim.cmd([[
  augroup MyGroup
    autocmd!
    autocmd BufWritePre * echo "Saving..."
  augroup END
]])
```

### vim.api

Low-level Neovim API:

```lua
vim.api.nvim_set_keymap("n", "<leader>w", ":w<CR>", { noremap = true })
vim.api.nvim_buf_set_lines(0, 0, -1, false, { "Hello", "World" })
vim.api.nvim_win_set_cursor(0, { 1, 0 })
```

### vim.opt

Set options (modern way):

```lua
vim.opt.number = true
vim.opt.relativenumber = true
vim.opt.tabstop = 4
vim.opt.shiftwidth = 4
vim.opt.expandtab = true
```

### vim.keymap

Set keymaps (modern way):

```lua
vim.keymap.set("n", "<leader>w", ":w<CR>", { desc = "Save file" })
vim.keymap.set("n", "<leader>q", ":q<CR>", { desc = "Quit" })
vim.keymap.set("v", "J", ":m '>+1<CR>gv=gv", { desc = "Move line down" })
```

### vim.fn

Call Vim functions:

```lua
local current_file = vim.fn.expand("%")
local file_exists = vim.fn.filereadable("init.lua")
local lines = vim.fn.getline(1, "$")
```

## Practical Examples

### 1. Toggle Line Numbers

```lua
local function toggle_numbers()
  if vim.opt.number:get() then
    vim.opt.number = false
    vim.opt.relativenumber = false
  else
    vim.opt.number = true
    vim.opt.relativenumber = true
  end
end

vim.keymap.set("n", "<leader>tn", toggle_numbers, { desc = "Toggle line numbers" })
```

### 2. Quick File Switcher

```lua
local function switch_to_test()
  local current = vim.fn.expand("%")
  local test_file
  
  if current:match("_test%.") then
    test_file = current:gsub("_test%.", ".")
  else
    test_file = current:gsub("(%.[^.]+)$", "_test%1")
  end
  
  vim.cmd("edit " .. test_file)
end

vim.keymap.set("n", "<leader>tt", switch_to_test, { desc = "Toggle test file" })
```

### 3. Insert Date/Time

```lua
local function insert_date()
  local date = os.date("%Y-%m-%d")
  local pos = vim.api.nvim_win_get_cursor(0)
  vim.api.nvim_buf_set_text(0, pos[1] - 1, pos[2], pos[1] - 1, pos[2], { date })
end

vim.keymap.set("n", "<leader>id", insert_date, { desc = "Insert date" })
```

### 4. Auto-create Parent Directories

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

### 5. Highlight on Yank

```lua
vim.api.nvim_create_autocmd("TextYankPost", {
  callback = function()
    vim.highlight.on_yank({ higroup = "IncSearch", timeout = 200 })
  end,
})
```

### 6. Strip Trailing Whitespace

```lua
local function strip_trailing_whitespace()
  local save = vim.fn.winsaveview()
  vim.cmd([[%s/\s\+$//e]])
  vim.fn.winrestview(save)
end

vim.api.nvim_create_autocmd("BufWritePre", {
  pattern = "*",
  callback = strip_trailing_whitespace,
})
```

### 7. Project Root Finder

```lua
local function find_project_root()
  local markers = { ".git", "package.json", "Cargo.toml", "go.mod" }
  local current = vim.fn.expand("%:p:h")
  
  while current ~= "/" do
    for _, marker in ipairs(markers) do
      if vim.fn.filereadable(current .. "/" .. marker) == 1 or
         vim.fn.isdirectory(current .. "/" .. marker) == 1 then
        return current
      end
    end
    current = vim.fn.fnamemodify(current, ":h")
  end
  
  return vim.fn.getcwd()
end

local function cd_to_project_root()
  local root = find_project_root()
  vim.cmd("cd " .. root)
  print("Changed to: " .. root)
end

vim.keymap.set("n", "<leader>cr", cd_to_project_root, { desc = "CD to project root" })
```

### 8. Quick Note Taking

```lua
local function quick_note()
  local notes_dir = vim.fn.expand("~/notes")
  local date = os.date("%Y-%m-%d")
  local file = notes_dir .. "/" .. date .. ".md"
  
  vim.cmd("edit " .. file)
end

vim.keymap.set("n", "<leader>nn", quick_note, { desc = "Open today's note" })
```

## Working with Buffers

### Get Current Buffer Info

```lua
local bufnr = vim.api.nvim_get_current_buf()
local filename = vim.api.nvim_buf_get_name(bufnr)
local lines = vim.api.nvim_buf_get_lines(bufnr, 0, -1, false)
```

### Modify Buffer Content

```lua
vim.api.nvim_buf_set_lines(bufnr, 0, 1, false, { "New first line" })
vim.api.nvim_buf_set_text(bufnr, 0, 0, 0, 5, { "Hello" })
```

### Buffer Keymaps

```lua
vim.api.nvim_buf_set_keymap(bufnr, "n", "<leader>x", ":echo 'Hi'<CR>", {
  noremap = true,
  silent = true,
})
```

## Working with Windows

### Get Window Info

```lua
local win = vim.api.nvim_get_current_win()
local cursor = vim.api.nvim_win_get_cursor(win)
local width = vim.api.nvim_win_get_width(win)
```

### Split Windows

```lua
vim.cmd("vsplit")
vim.cmd("split")
```

### Close Windows

```lua
vim.api.nvim_win_close(win, false)
```

## Creating Floating Windows

```lua
local function create_float()
  local buf = vim.api.nvim_create_buf(false, true)
  local width = 60
  local height = 10
  local win = vim.api.nvim_open_win(buf, true, {
    relative = "editor",
    width = width,
    height = height,
    col = (vim.o.columns - width) / 2,
    row = (vim.o.lines - height) / 2,
    style = "minimal",
    border = "rounded",
  })
  
  vim.api.nvim_buf_set_lines(buf, 0, -1, false, {
    "Hello from floating window!",
    "",
    "Press q to close",
  })
  
  vim.api.nvim_buf_set_keymap(buf, "n", "q", ":close<CR>", {
    noremap = true,
    silent = true,
  })
end

vim.keymap.set("n", "<leader>fw", create_float, { desc = "Open floating window" })
```

## Module System

Organize code in modules:

**~/.config/nvim/lua/utils/init.lua**
```lua
local M = {}

function M.greet(name)
  return "Hello, " .. name
end

function M.format_date()
  return os.date("%Y-%m-%d")
end

return M
```

**~/.config/nvim/init.lua**
```lua
local utils = require("utils")
print(utils.greet("Neovim"))
```

## Debugging Lua

### Print Debugging

```lua
print(vim.inspect(variable))
```

### Notifications

```lua
vim.notify("Hello!", vim.log.levels.INFO)
vim.notify("Warning!", vim.log.levels.WARN)
vim.notify("Error!", vim.log.levels.ERROR)
```

### Check for Errors

```lua
local ok, result = pcall(function()
  return some_risky_function()
end)

if not ok then
  print("Error: " .. result)
end
```

## Performance Tips

### Use Local Variables

```lua
local api = vim.api
for i = 1, 1000 do
  api.nvim_buf_set_lines(0, 0, 1, false, { "Line" })
end
```

### Avoid Repeated Function Calls

```lua
local current_buf = vim.api.nvim_get_current_buf()
for i = 1, 100 do
  vim.api.nvim_buf_set_lines(current_buf, i, i, false, { "Line" })
end
```

### Use vim.schedule for Async

```lua
vim.schedule(function()
  vim.cmd("edit file.txt")
end)
```

## Best Practices

1. **Use local** - Always declare variables as local
2. **Error handling** - Use pcall for risky operations
3. **Descriptive names** - Use clear function/variable names
4. **Modularize** - Split code into separate modules
5. **Document** - Add comments for complex logic
6. **Test** - Test functions before adding to config

## Exercises

1. **Toggle function** - Write a function to toggle between relative and absolute line numbers
2. **Word counter** - Create a function that counts words in the current buffer
3. **Quick fixer** - Write a function that fixes common typos (e.g., "teh" → "the")
4. **Status line component** - Create a custom function for your status line
5. **Floating scratch** - Build a floating window for quick notes

## Next Steps

Continue to [Autocommands](autocommands.md) to learn how to automate tasks based on events.

## Resources

- [Neovim Lua Guide](https://neovim.io/doc/user/lua-guide.html)
- [Lua 5.1 Reference](https://www.lua.org/manual/5.1/)
- [nvim-lua-guide](https://github.com/nanotee/nvim-lua-guide)
- [Learn Lua in Y Minutes](https://learnxinyminutes.com/docs/lua/)
