# Debugging in Neovim

Set up a complete debugging environment with nvim-dap (Debug Adapter Protocol) for breakpoints, step-through debugging, and variable inspection—all without leaving Neovim.

## What is DAP?

Debug Adapter Protocol (DAP) is like LSP but for debuggers. It provides a standardized way for editors to communicate with debuggers.

```
┌─────────────┐                    ┌──────────────┐
│   Neovim    │ ◄──── DAP ──────► │   Debugger   │
│ (nvim-dap)  │    (JSON-RPC)      │  (Python,    │
│             │                    │   Node, etc) │
└─────────────┘                    └──────────────┘
```

## Core Plugins

### nvim-dap

The DAP client for Neovim:

```lua
{
  "mfussenegger/nvim-dap",
  dependencies = {
    "rcarriga/nvim-dap-ui",
    "theHamsta/nvim-dap-virtual-text",
  },
  keys = {
    { "<leader>db", function() require("dap").toggle_breakpoint() end, desc = "Toggle breakpoint" },
    { "<leader>dc", function() require("dap").continue() end, desc = "Continue" },
    { "<leader>di", function() require("dap").step_into() end, desc = "Step into" },
    { "<leader>do", function() require("dap").step_over() end, desc = "Step over" },
    { "<leader>dO", function() require("dap").step_out() end, desc = "Step out" },
    { "<leader>dr", function() require("dap").repl.open() end, desc = "Open REPL" },
    { "<leader>dl", function() require("dap").run_last() end, desc = "Run last" },
    { "<leader>dt", function() require("dap").terminate() end, desc = "Terminate" },
  },
}
```

### nvim-dap-ui

Visual debugging UI:

```lua
{
  "rcarriga/nvim-dap-ui",
  dependencies = { "mfussenegger/nvim-dap", "nvim-neotest/nvim-nio" },
  keys = {
    { "<leader>du", function() require("dapui").toggle() end, desc = "Toggle UI" },
  },
  config = function()
    local dap, dapui = require("dap"), require("dapui")
    
    dapui.setup()

    dap.listeners.after.event_initialized["dapui_config"] = function()
      dapui.open()
    end
    dap.listeners.before.event_terminated["dapui_config"] = function()
      dapui.close()
    end
    dap.listeners.before.event_exited["dapui_config"] = function()
      dapui.close()
    end
  end,
}
```

### nvim-dap-virtual-text

Show variable values inline:

```lua
{
  "theHamsta/nvim-dap-virtual-text",
  dependencies = "mfussenegger/nvim-dap",
  opts = {},
}
```

## Language-Specific Setup

### Python (debugpy)

Install debugpy:
```bash
pip install debugpy
```

Configure:
```lua
local dap = require("dap")

dap.adapters.python = {
  type = "executable",
  command = "python",
  args = { "-m", "debugpy.adapter" },
}

dap.configurations.python = {
  {
    type = "python",
    request = "launch",
    name = "Launch file",
    program = "${file}",
    pythonPath = function()
      return "/usr/bin/python3"
    end,
  },
}
```

### JavaScript/TypeScript (node)

Install vscode-js-debug via Mason:
```vim
:MasonInstall js-debug-adapter
```

Configure:
```lua
local dap = require("dap")

dap.adapters.node2 = {
  type = "executable",
  command = "node",
  args = { vim.fn.stdpath("data") .. "/mason/packages/js-debug-adapter/js-debug/src/dapDebugServer.js" },
}

dap.configurations.javascript = {
  {
    type = "node2",
    request = "launch",
    name = "Launch Program",
    program = "${file}",
    cwd = vim.fn.getcwd(),
    sourceMaps = true,
    protocol = "inspector",
  },
}

dap.configurations.typescript = dap.configurations.javascript
```

### Go (delve)

Install delve:
```bash
go install github.com/go-delve/delve/cmd/dlv@latest
```

Configure:
```lua
local dap = require("dap")

dap.adapters.go = {
  type = "executable",
  command = "dlv",
  args = { "dap" },
}

dap.configurations.go = {
  {
    type = "go",
    name = "Debug",
    request = "launch",
    program = "${file}",
  },
  {
    type = "go",
    name = "Debug test",
    request = "launch",
    mode = "test",
    program = "${file}",
  },
}
```

### Rust (lldb)

Install codelldb via Mason:
```vim
:MasonInstall codelldb
```

Configure:
```lua
local dap = require("dap")

dap.adapters.codelldb = {
  type = "server",
  port = "${port}",
  executable = {
    command = vim.fn.stdpath("data") .. "/mason/bin/codelldb",
    args = { "--port", "${port}" },
  },
}

dap.configurations.rust = {
  {
    name = "Launch",
    type = "codelldb",
    request = "launch",
    program = function()
      return vim.fn.input("Path to executable: ", vim.fn.getcwd() .. "/", "file")
    end,
    cwd = "${workspaceFolder}",
    stopOnEntry = false,
  },
}
```

## Mason Integration

Use mason-nvim-dap to automatically install debug adapters:

```lua
{
  "jay-babu/mason-nvim-dap.nvim",
  dependencies = { "williamboman/mason.nvim", "mfussenegger/nvim-dap" },
  opts = {
    ensure_installed = { "python", "codelldb", "js" },
    handlers = {},
  },
}
```

## Basic Debugging Workflow

1. **Set Breakpoint**
   ```vim
   <leader>db
   ```
   Sets/removes breakpoint on current line

2. **Start Debugging**
   ```vim
   <leader>dc
   ```
   Starts debugger or continues to next breakpoint

3. **Step Through Code**
   - `<leader>di` - Step into function
   - `<leader>do` - Step over function
   - `<leader>dO` - Step out of function

4. **Inspect Variables**
   - Hover over variable
   - Check Scopes panel in dap-ui
   - Use REPL: `<leader>dr`

5. **Terminate**
   ```vim
   <leader>dt
   ```

## DAP UI

When debugging starts, dap-ui shows:

```
┌──────────────┬──────────────────┬──────────────┐
│  Scopes      │   Code Window    │  Breakpoints │
│  Variables   │   (your code)    │  Stack       │
│  Watches     │                  │  REPL        │
└──────────────┴──────────────────┴──────────────┘
```

### Panels

- **Scopes** - Local/global variables
- **Watches** - Custom expressions to track
- **Stack** - Call stack
- **Breakpoints** - All breakpoints
- **REPL** - Interactive evaluation

## Advanced Features

### Conditional Breakpoints

```lua
vim.keymap.set("n", "<leader>dB", function()
  require("dap").set_breakpoint(vim.fn.input("Condition: "))
end, { desc = "Conditional breakpoint" })
```

Usage:
```vim
<leader>dB
Condition: x > 10
```

### Log Points

Print without stopping:

```lua
require("dap").set_breakpoint(nil, nil, vim.fn.input("Log message: "))
```

### Run to Cursor

```lua
vim.keymap.set("n", "<leader>dC", function()
  require("dap").run_to_cursor()
end, { desc = "Run to cursor" })
```

### Watches

Add expression to watch:

```lua
vim.keymap.set("n", "<leader>dw", function()
  require("dapui").elements.watches.add(vim.fn.expand("<cword>"))
end, { desc = "Watch variable" })
```

## REPL Commands

Open REPL with `<leader>dr`, then:

- `.help` - Show help
- `.exit` - Close REPL
- `.c` or `.continue` - Continue execution
- `.n` or `.next` - Step over
- `.into` - Step into
- `.out` - Step out
- `.up` - Go up in stack
- `.down` - Go down in stack

Evaluate expressions:
```
> variable_name
> some_function()
> x + y
```

## Debugging Tests

### Python with pytest

```lua
{
  type = "python",
  request = "launch",
  name = "Debug Test",
  module = "pytest",
  args = { "${file}", "-v" },
}
```

### JavaScript with Jest

```lua
{
  type = "node2",
  request = "launch",
  name = "Jest",
  program = "${workspaceFolder}/node_modules/.bin/jest",
  args = { "--runInBand", "--no-coverage", "${file}" },
  cwd = "${workspaceFolder}",
}
```

## Complete Configuration Example

```lua
return {
  {
    "mfussenegger/nvim-dap",
    dependencies = {
      "rcarriga/nvim-dap-ui",
      "theHamsta/nvim-dap-virtual-text",
      "nvim-neotest/nvim-nio",
    },
    keys = {
      { "<leader>db", function() require("dap").toggle_breakpoint() end },
      { "<leader>dc", function() require("dap").continue() end },
      { "<leader>di", function() require("dap").step_into() end },
      { "<leader>do", function() require("dap").step_over() end },
      { "<leader>dO", function() require("dap").step_out() end },
      { "<leader>dt", function() require("dap").terminate() end },
      { "<leader>du", function() require("dapui").toggle() end },
    },
    config = function()
      local dap = require("dap")
      local dapui = require("dapui")

      dapui.setup()
      require("nvim-dap-virtual-text").setup()

      dap.listeners.after.event_initialized["dapui_config"] = function()
        dapui.open()
      end

      dap.adapters.python = {
        type = "executable",
        command = "python",
        args = { "-m", "debugpy.adapter" },
      }

      dap.configurations.python = {
        {
          type = "python",
          request = "launch",
          name = "Launch file",
          program = "${file}",
          pythonPath = function()
            return "/usr/bin/python3"
          end,
        },
      }
    end,
  },
}
```

## Keybinding Reference

| Key | Action |
|-----|--------|
| `<leader>db` | Toggle breakpoint |
| `<leader>dB` | Conditional breakpoint |
| `<leader>dc` | Continue / Start |
| `<leader>di` | Step into |
| `<leader>do` | Step over |
| `<leader>dO` | Step out |
| `<leader>dt` | Terminate |
| `<leader>du` | Toggle UI |
| `<leader>dr` | Open REPL |
| `<leader>dl` | Run last config |
| `<leader>dC` | Run to cursor |

## Troubleshooting

### Debugger Not Starting

Check adapter installation:
```vim
:checkhealth dap
```

Check configuration:
```lua
print(vim.inspect(require("dap").configurations.python))
```

### Breakpoints Not Hitting

- Ensure code path is executed
- Check file paths match
- Verify source maps for JS/TS
- Check conditional breakpoint expressions

### No Variable Values

- Ensure debug symbols are compiled
- Check if virtual-text is enabled
- Open dap-ui to see scopes panel

## Best Practices

1. **Use conditional breakpoints** - Avoid stopping on every iteration
2. **Watch key variables** - Track important state changes
3. **Use REPL** - Test expressions interactively
4. **Log points** - Print without stopping
5. **Step strategically** - Step over unless you need details
6. **Clean up breakpoints** - Remove old breakpoints regularly

## Exercises

1. **Install nvim-dap** - Set up dap for your language
2. **Debug a program** - Set breakpoint and step through code
3. **Inspect variables** - Check variable values at breakpoint
4. **Use REPL** - Evaluate expressions in REPL
5. **Conditional breakpoint** - Set breakpoint with condition

## Next Steps

Continue to [Testing](testing.md) to learn how to run and manage tests from Neovim.

## Resources

- [nvim-dap](https://github.com/mfussenegger/nvim-dap)
- [nvim-dap-ui](https://github.com/rcarriga/nvim-dap-ui)
- [Debug Adapter Protocol](https://microsoft.github.io/debug-adapter-protocol/)
- [mason-nvim-dap](https://github.com/jay-babu/mason-nvim-dap.nvim)
