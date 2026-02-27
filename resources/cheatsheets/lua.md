# Lua for Neovim Cheatsheet

Quick reference for Lua scripting in Neovim configuration.

## Lua Basics

### Variables

```lua
local name = "value"        -- Local variable (preferred)
global_var = "value"        -- Global variable (avoid)

local number = 42
local boolean = true
local nothing = nil
```

### Strings

```lua
local str1 = "double quotes"
local str2 = 'single quotes'
local str3 = [[multi-line
string]]

-- Concatenation
local full = "Hello " .. "World"

-- String methods
str:upper()
str:lower()
str:sub(1, 5)
str:find("pattern")
str:gsub("old", "new")
```

### Tables (Arrays & Dictionaries)

```lua
-- Array (1-indexed!)
local arr = { "a", "b", "c" }
print(arr[1])  -- "a"

-- Dictionary
local dict = {
  key = "value",
  another = 123,
}
print(dict.key)  -- "value"
print(dict["key"])  -- "value"

-- Mixed
local mixed = {
  "item1",
  "item2",
  key = "value",
}
```

### Functions

```lua
-- Basic function
local function greet(name)
  return "Hello, " .. name
end

-- Anonymous function
local add = function(a, b)
  return a + b
end

-- Multiple return values
local function stats(n)
  return n, n * 2, n * 3
end
local a, b, c = stats(5)
```

### Conditionals

```lua
if condition then
  -- code
elseif other_condition then
  -- code
else
  -- code
end

-- Ternary-like
local result = condition and "yes" or "no"
```

### Loops

```lua
-- For loop
for i = 1, 10 do
  print(i)
end

-- For loop with step
for i = 10, 1, -1 do
  print(i)
end

-- Array iteration
for index, value in ipairs(array) do
  print(index, value)
end

-- Dictionary iteration
for key, value in pairs(dict) do
  print(key, value)
end

-- While loop
while condition do
  -- code
end
```

## Neovim API Basics

### vim.opt - Options

```lua
-- Set options
vim.opt.number = true
vim.opt.relativenumber = true
vim.opt.tabstop = 4
vim.opt.shiftwidth = 4
vim.opt.expandtab = true

-- Append to list
vim.opt.wildignore:append("*.pyc")

-- Remove from list
vim.opt.wildignore:remove("*.o")

-- Get option value
local ts = vim.opt.tabstop:get()
```

### vim.g - Global Variables

```lua
-- Set leader key
vim.g.mapleader = " "
vim.g.maplocalleader = " "

-- Plugin variables
vim.g.loaded_netrw = 1
vim.g.python3_host_prog = "/usr/bin/python3"
```

### vim.keymap - Keymaps

```lua
-- Basic keymap
vim.keymap.set("n", "<leader>w", ":w<CR>")

-- With options
vim.keymap.set("n", "<leader>w", ":w<CR>", {
  noremap = true,
  silent = true,
  desc = "Save file",
})

-- Multiple modes
vim.keymap.set({"n", "v"}, "gc", function()
  -- code
end)

-- Buffer-specific
vim.keymap.set("n", "K", vim.lsp.buf.hover, {
  buffer = bufnr,
})
```

### vim.api - Low-Level API

```lua
-- Create autocommand
vim.api.nvim_create_autocmd("BufWritePre", {
  pattern = "*.lua",
  callback = function()
    vim.lsp.buf.format()
  end,
})

-- Create autocommand group
local group = vim.api.nvim_create_augroup("MyGroup", { clear = true })
vim.api.nvim_create_autocmd("BufEnter", {
  group = group,
  callback = function() end,
})

-- Buffer operations
local bufnr = vim.api.nvim_get_current_buf()
vim.api.nvim_buf_set_lines(bufnr, 0, -1, false, {"line1", "line2"})
local lines = vim.api.nvim_buf_get_lines(bufnr, 0, -1, false)

-- Window operations
local win = vim.api.nvim_get_current_win()
vim.api.nvim_win_set_cursor(win, {1, 0})
local cursor = vim.api.nvim_win_get_cursor(win)
```

### vim.fn - Vim Functions

```lua
-- Call Vim functions
vim.fn.expand("%")          -- Current file
vim.fn.getcwd()             -- Current directory
vim.fn.filereadable("file") -- Check if file exists
vim.fn.system("ls")         -- Run shell command

-- Common functions
local file = vim.fn.expand("%:p")  -- Full path
local dir = vim.fn.expand("%:h")   -- Directory
local name = vim.fn.expand("%:t")  -- Filename
```

### vim.cmd - Execute Ex Commands

```lua
-- Single command
vim.cmd("colorscheme gruvbox")
vim.cmd("set number")

-- Multiple commands
vim.cmd([[
  augroup MyGroup
    autocmd!
    autocmd BufEnter * echo "Hello"
  augroup END
]])
```

## Common Patterns

### Check if Plugin Exists

```lua
local ok, plugin = pcall(require, "plugin-name")
if not ok then
  return
end

-- Use plugin
plugin.setup()
```

### Safe Function Call

```lua
local ok, result = pcall(function()
  return risky_function()
end)

if not ok then
  vim.notify("Error: " .. result, vim.log.levels.ERROR)
end
```

### Toggle Function

```lua
local function toggle_option(option)
  vim.opt[option] = not vim.opt[option]:get()
end

vim.keymap.set("n", "<leader>tn", function()
  toggle_option("number")
end)
```

### Module Pattern

```lua
-- lua/mymodule.lua
local M = {}

function M.setup(opts)
  opts = opts or {}
  -- initialization
end

function M.greet(name)
  return "Hello, " .. name
end

return M

-- In init.lua
require("mymodule").setup({ option = true })
```

### Autocommand with Callback

```lua
vim.api.nvim_create_autocmd("BufWritePost", {
  pattern = "*.lua",
  callback = function(args)
    print("Saved buffer: " .. args.buf)
    print("File: " .. args.file)
  end,
})
```

### User Command

```lua
vim.api.nvim_create_user_command("Hello", function(opts)
  print("Hello " .. opts.args)
end, {
  nargs = 1,
  desc = "Say hello",
})

-- Use: :Hello World
```

## Debugging

### Print Debugging

```lua
-- Simple print
print("value:", value)

-- Pretty print tables
print(vim.inspect(table))

-- Notify user
vim.notify("Message", vim.log.levels.INFO)
vim.notify("Warning!", vim.log.levels.WARN)
vim.notify("Error!", vim.log.levels.ERROR)
```

### Check Variable Types

```lua
print(type(var))  -- "string", "number", "table", "function", etc.

-- Check if nil
if var == nil then
  print("Variable is nil")
end

-- Check if table
if type(var) == "table" then
  print("It's a table")
end
```

## Working with Files

### Read File

```lua
local file = io.open("path/to/file", "r")
if file then
  local content = file:read("*all")
  file:close()
end

-- Or use vim.fn
local lines = vim.fn.readfile("path/to/file")
```

### Write File

```lua
local file = io.open("path/to/file", "w")
if file then
  file:write("content")
  file:close()
end

-- Or use vim.fn
vim.fn.writefile({"line1", "line2"}, "path/to/file")
```

### Check File Exists

```lua
local exists = vim.fn.filereadable("path/to/file") == 1

-- Or
local file = io.open("path/to/file", "r")
if file then
  file:close()
  -- exists
else
  -- doesn't exist
end
```

## Working with Paths

```lua
-- Join paths
local path = vim.fn.stdpath("config") .. "/init.lua"

-- Standard paths
local config = vim.fn.stdpath("config")  -- ~/.config/nvim
local data = vim.fn.stdpath("data")      -- ~/.local/share/nvim
local cache = vim.fn.stdpath("cache")    -- ~/.cache/nvim

-- Expand paths
local home = vim.fn.expand("~")
local current_file = vim.fn.expand("%:p")
local current_dir = vim.fn.expand("%:p:h")
```

## Useful Snippets

### Get Visual Selection

```lua
local function get_visual_selection()
  local start = vim.fn.getpos("'<")
  local finish = vim.fn.getpos("'>")
  local lines = vim.fn.getline(start[2], finish[2])
  return lines
end
```

### Execute in Current Directory

```lua
local function in_directory(dir, callback)
  local cwd = vim.fn.getcwd()
  vim.cmd("cd " .. dir)
  callback()
  vim.cmd("cd " .. cwd)
end
```

### Debounce Function

```lua
local function debounce(func, delay)
  local timer = vim.loop.new_timer()
  return function(...)
    local args = {...}
    timer:stop()
    timer:start(delay, 0, vim.schedule_wrap(function()
      func(unpack(args))
    end))
  end
end
```

### Find Root Directory

```lua
local function find_root(markers)
  local path = vim.fn.expand("%:p:h")
  while path ~= "/" do
    for _, marker in ipairs(markers) do
      if vim.fn.filereadable(path .. "/" .. marker) == 1 or
         vim.fn.isdirectory(path .. "/" .. marker) == 1 then
        return path
      end
    end
    path = vim.fn.fnamemodify(path, ":h")
  end
  return vim.fn.getcwd()
end

local root = find_root({".git", "package.json", "Cargo.toml"})
```

## Performance Tips

### Use Local Variables

```lua
-- Slow
for i = 1, 1000 do
  vim.api.nvim_buf_set_lines(0, i, i, false, {"line"})
end

-- Fast
local api = vim.api
local buf = api.nvim_get_current_buf()
for i = 1, 1000 do
  api.nvim_buf_set_lines(buf, i, i, false, {"line"})
end
```

### Batch Operations

```lua
-- Slow: multiple calls
for i = 1, 100 do
  vim.api.nvim_buf_set_lines(0, i, i, false, {tostring(i)})
end

-- Fast: single call
local lines = {}
for i = 1, 100 do
  table.insert(lines, tostring(i))
end
vim.api.nvim_buf_set_lines(0, 0, -1, false, lines)
```

## Common Gotchas

### Tables are 1-indexed

```lua
local arr = {"a", "b", "c"}
print(arr[0])  -- nil
print(arr[1])  -- "a"
```

### Nil in Tables

```lua
local arr = {1, 2, nil, 4}
print(#arr)  -- 2 (stops at nil!)

-- Use pairs, not ipairs with holes
for i, v in pairs(arr) do
  print(i, v)
end
```

### String Concatenation

```lua
-- Slow in loops
local str = ""
for i = 1, 1000 do
  str = str .. i
end

-- Fast
local parts = {}
for i = 1, 1000 do
  table.insert(parts, i)
end
local str = table.concat(parts)
```

## Resources

- `:help lua` - Lua in Neovim
- `:help vim.api` - API functions
- `:help vim.fn` - Vim function wrapper
- `:help lua-guide` - Lua guide
- [Learn Lua in Y Minutes](https://learnxinyminutes.com/docs/lua/)
- [Lua 5.1 Reference](https://www.lua.org/manual/5.1/)

---

**Keep this handy while writing your Neovim config!**
