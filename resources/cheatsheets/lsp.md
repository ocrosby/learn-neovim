# LSP Commands Cheatsheet

Quick reference for Language Server Protocol commands and workflows in Neovim.

## Essential LSP Commands

### Navigation

| Command | Keybinding | Description |
|---------|------------|-------------|
| `:lua vim.lsp.buf.definition()` | `gd` | Go to definition |
| `:lua vim.lsp.buf.declaration()` | `gD` | Go to declaration |
| `:lua vim.lsp.buf.type_definition()` | `gt` | Go to type definition |
| `:lua vim.lsp.buf.implementation()` | `gi` | Go to implementation |
| `:lua vim.lsp.buf.references()` | `gr` | List all references |

### Information

| Command | Keybinding | Description |
|---------|------------|-------------|
| `:lua vim.lsp.buf.hover()` | `K` | Show hover documentation |
| `:lua vim.lsp.buf.signature_help()` | `<C-k>` | Show signature help (insert mode) |
| `:LspInfo` | - | Show LSP client info |
| `:lua vim.lsp.buf.document_symbol()` | - | List document symbols |
| `:lua vim.lsp.buf.workspace_symbol()` | - | Search workspace symbols |

### Refactoring

| Command | Keybinding | Description |
|---------|------------|-------------|
| `:lua vim.lsp.buf.rename()` | `<leader>rn` | Rename symbol |
| `:lua vim.lsp.buf.code_action()` | `<leader>ca` | Show code actions |
| `:lua vim.lsp.buf.format()` | `<leader>f` | Format buffer |
| `:lua vim.lsp.buf.range_formatting()` | `<leader>f` | Format selection (visual) |

### Diagnostics

| Command | Keybinding | Description |
|---------|------------|-------------|
| `:lua vim.diagnostic.open_float()` | `<leader>e` | Show diagnostic popup |
| `:lua vim.diagnostic.goto_next()` | `]d` | Next diagnostic |
| `:lua vim.diagnostic.goto_prev()` | `[d` | Previous diagnostic |
| `:lua vim.diagnostic.setloclist()` | `<leader>q` | Add to location list |
| `:lua vim.diagnostic.setqflist()` | - | Add to quickfix list |

## Management Commands

### LSP Client Control

```vim
:LspInfo              " Show attached clients
:LspStart             " Start LSP client
:LspStop              " Stop LSP client
:LspRestart           " Restart LSP client
```

### Mason (LSP Server Manager)

```vim
:Mason                " Open Mason UI
:MasonInstall <name>  " Install language server
:MasonUninstall <name>" Uninstall language server
:MasonUpdate          " Update all servers
:MasonLog             " View Mason log
```

### Health Check

```vim
:checkhealth lsp      " Check LSP health
:checkhealth mason    " Check Mason health
```

## Common Workflows

### 1. Jump to Definition and Back

```vim
gd         " Jump to definition
<C-o>      " Jump back (built-in Vim)
<C-i>      " Jump forward
```

### 2. Find All References

```vim
gr         " List all references
<CR>       " Jump to selected reference
:copen     " Open quickfix list
:cnext     " Next reference
:cprev     " Previous reference
```

### 3. Rename Symbol Everywhere

```vim
<leader>rn      " Start rename
type new name
<CR>            " Confirm
```

### 4. Fix Errors with Code Actions

```vim
]d              " Jump to diagnostic
<leader>ca      " Show code actions
j/k             " Select action
<CR>            " Apply action
```

### 5. Format on Save

Add to config:
```lua
vim.api.nvim_create_autocmd("BufWritePre", {
  pattern = "*.lua",
  callback = function()
    vim.lsp.buf.format({ async = false })
  end,
})
```

## Lua API Reference

### Diagnostic Functions

```lua
-- Get diagnostics for buffer
vim.diagnostic.get(bufnr)

-- Set diagnostics display
vim.diagnostic.config({
  virtual_text = true,
  signs = true,
  underline = true,
  update_in_insert = false,
  severity_sort = true,
})

-- Filter diagnostics by severity
vim.diagnostic.get(0, {
  severity = vim.diagnostic.severity.ERROR
})
```

### LSP Buffer Functions

```lua
-- Format buffer
vim.lsp.buf.format({
  async = false,
  timeout_ms = 2000,
})

-- Format range
vim.lsp.buf.range_formatting()

-- Request hover
vim.lsp.buf.hover()

-- Get signature help
vim.lsp.buf.signature_help()
```

### LSP Client Functions

```lua
-- Get active clients
vim.lsp.get_active_clients()

-- Get client by buffer
vim.lsp.get_active_clients({ bufnr = 0 })

-- Stop client
vim.lsp.stop_client(client_id)
```

## Configuration Examples

### Set Up LSP with Keybindings

```lua
local on_attach = function(client, bufnr)
  local opts = { buffer = bufnr, noremap = true, silent = true }
  
  vim.keymap.set("n", "gd", vim.lsp.buf.definition, opts)
  vim.keymap.set("n", "K", vim.lsp.buf.hover, opts)
  vim.keymap.set("n", "<leader>rn", vim.lsp.buf.rename, opts)
  vim.keymap.set("n", "<leader>ca", vim.lsp.buf.code_action, opts)
  vim.keymap.set("n", "gr", vim.lsp.buf.references, opts)
  vim.keymap.set("n", "[d", vim.diagnostic.goto_prev, opts)
  vim.keymap.set("n", "]d", vim.diagnostic.goto_next, opts)
end

require("lspconfig").lua_ls.setup({
  on_attach = on_attach,
})
```

### Customize Diagnostic Display

```lua
-- Change diagnostic symbols
local signs = {
  Error = " ",
  Warn = " ",
  Hint = " ",
  Info = " ",
}

for type, icon in pairs(signs) do
  local hl = "DiagnosticSign" .. type
  vim.fn.sign_define(hl, { text = icon, texthl = hl })
end

-- Configure display
vim.diagnostic.config({
  virtual_text = {
    prefix = "●",
    spacing = 4,
  },
  signs = true,
  underline = true,
  update_in_insert = false,
  severity_sort = true,
})
```

### Enable Inlay Hints

```lua
-- Enable inlay hints (Neovim 0.10+)
vim.lsp.inlay_hint.enable(bufnr, true)

-- Toggle inlay hints
vim.keymap.set("n", "<leader>h", function()
  vim.lsp.inlay_hint.enable(0, not vim.lsp.inlay_hint.is_enabled())
end, { desc = "Toggle inlay hints" })
```

## Language-Specific Tips

### Python (pyright)

```lua
require("lspconfig").pyright.setup({
  settings = {
    python = {
      analysis = {
        typeCheckingMode = "basic",  -- or "strict"
        autoSearchPaths = true,
        useLibraryCodeForTypes = true,
      },
    },
  },
})
```

### TypeScript (ts_ls)

```lua
require("lspconfig").ts_ls.setup({
  settings = {
    typescript = {
      inlayHints = {
        includeInlayParameterNameHints = "all",
        includeInlayFunctionParameterTypeHints = true,
      },
    },
  },
})
```

### Rust (rust-analyzer)

```lua
require("lspconfig").rust_analyzer.setup({
  settings = {
    ["rust-analyzer"] = {
      cargo = { allFeatures = true },
      checkOnSave = { command = "clippy" },
    },
  },
})
```

## Troubleshooting

### LSP Not Starting

```vim
:LspInfo            " Check if server is running
:messages           " Check for errors
:checkhealth lsp    " Run health check
```

### Server Not Found

```vim
:Mason              " Verify server is installed
:MasonLog           " Check installation logs
```

### Diagnostics Not Showing

```lua
-- Check diagnostic config
:lua vim.print(vim.diagnostic.config())

-- Manually trigger diagnostics
:lua vim.diagnostic.show()
```

### Format Not Working

```lua
-- Check if server supports formatting
:lua vim.print(vim.lsp.get_active_clients()[1].server_capabilities.documentFormattingProvider)

-- Try manual format
:lua vim.lsp.buf.format()
```

## Performance Tips

```lua
-- Disable semantic tokens for large files
vim.api.nvim_create_autocmd("LspAttach", {
  callback = function(args)
    local client = vim.lsp.get_client_by_id(args.data.client_id)
    if client then
      client.server_capabilities.semanticTokensProvider = nil
    end
  end,
})

-- Limit diagnostic updates
vim.diagnostic.config({
  update_in_insert = false,
})
```

## Resources

- `:help lsp` - Built-in LSP documentation
- `:help vim.lsp` - Lua LSP API
- `:help vim.diagnostic` - Diagnostic API
- [nvim-lspconfig docs](https://github.com/neovim/nvim-lspconfig)
- [LSP Specification](https://microsoft.github.io/language-server-protocol/)

## Quick Setup Template

```lua
-- Minimal LSP setup
local lspconfig = require("lspconfig")

-- Setup function with common config
local function setup_server(server)
  lspconfig[server].setup({
    on_attach = function(_, bufnr)
      -- Keybindings
      local opts = { buffer = bufnr }
      vim.keymap.set("n", "gd", vim.lsp.buf.definition, opts)
      vim.keymap.set("n", "K", vim.lsp.buf.hover, opts)
      vim.keymap.set("n", "<leader>ca", vim.lsp.buf.code_action, opts)
      vim.keymap.set("n", "<leader>rn", vim.lsp.buf.rename, opts)
    end,
  })
end

-- Setup your servers
setup_server("lua_ls")
setup_server("pyright")
setup_server("ts_ls")
```

---

**Print this page or keep it handy while learning LSP!**
