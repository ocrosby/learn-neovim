# Configuring LSP

Learn how to configure LSP features, set up keybindings, add autocompletion, and customize diagnostics for the perfect development experience.

## Prerequisites

Before configuring LSP, ensure you have:
- Mason installed ([see Mason guide](mason.md))
- At least one language server installed
- nvim-lspconfig plugin

## LSP Keybindings

### Default Keybindings

Neovim LSP has no default keybindings. You must configure them.

### Recommended Keybindings

Add this to your LSP configuration:

```lua
local on_attach = function(client, bufnr)
  local opts = { buffer = bufnr, remap = false }

  vim.keymap.set("n", "gd", function() vim.lsp.buf.definition() end, opts)
  vim.keymap.set("n", "K", function() vim.lsp.buf.hover() end, opts)
  vim.keymap.set("n", "<leader>vws", function() vim.lsp.buf.workspace_symbol() end, opts)
  vim.keymap.set("n", "<leader>vd", function() vim.diagnostic.open_float() end, opts)
  vim.keymap.set("n", "[d", function() vim.diagnostic.goto_next() end, opts)
  vim.keymap.set("n", "]d", function() vim.diagnostic.goto_prev() end, opts)
  vim.keymap.set("n", "<leader>vca", function() vim.lsp.buf.code_action() end, opts)
  vim.keymap.set("n", "<leader>vrr", function() vim.lsp.buf.references() end, opts)
  vim.keymap.set("n", "<leader>vrn", function() vim.lsp.buf.rename() end, opts)
  vim.keymap.set("i", "<C-h>", function() vim.lsp.buf.signature_help() end, opts)
end

require("lspconfig").lua_ls.setup({
  on_attach = on_attach,
})
```

### Keybinding Reference

| Key | Action | Description |
|-----|--------|-------------|
| `gd` | Go to definition | Jump to where symbol is defined |
| `K` | Hover | Show documentation |
| `<leader>vws` | Workspace symbol | Search symbols in workspace |
| `<leader>vd` | View diagnostic | Show error details |
| `[d` | Next diagnostic | Jump to next error/warning |
| `]d` | Previous diagnostic | Jump to previous error/warning |
| `<leader>vca` | Code action | Show available fixes |
| `<leader>vrr` | References | Find all references |
| `<leader>vrn` | Rename | Rename symbol |
| `<C-h>` (insert) | Signature help | Show function signature |

## Complete LSP Configuration

Here's a complete, production-ready LSP setup:

```lua
return {
  {
    "neovim/nvim-lspconfig",
    dependencies = {
      "williamboman/mason.nvim",
      "williamboman/mason-lspconfig.nvim",
      "hrsh7th/cmp-nvim-lsp",
    },
    config = function()
      local lspconfig = require("lspconfig")
      local cmp_nvim_lsp = require("cmp_nvim_lsp")

      local on_attach = function(client, bufnr)
        local opts = { buffer = bufnr, remap = false }

        vim.keymap.set("n", "gd", vim.lsp.buf.definition, opts)
        vim.keymap.set("n", "gD", vim.lsp.buf.declaration, opts)
        vim.keymap.set("n", "K", vim.lsp.buf.hover, opts)
        vim.keymap.set("n", "gi", vim.lsp.buf.implementation, opts)
        vim.keymap.set("n", "<leader>vrr", vim.lsp.buf.references, opts)
        vim.keymap.set("n", "<leader>vrn", vim.lsp.buf.rename, opts)
        vim.keymap.set("n", "<leader>vca", vim.lsp.buf.code_action, opts)
        vim.keymap.set("n", "[d", vim.diagnostic.goto_prev, opts)
        vim.keymap.set("n", "]d", vim.diagnostic.goto_next, opts)
        vim.keymap.set("n", "<leader>vd", vim.diagnostic.open_float, opts)
        vim.keymap.set("i", "<C-h>", vim.lsp.buf.signature_help, opts)
      end

      local capabilities = cmp_nvim_lsp.default_capabilities()

      local servers = { "lua_ls", "pyright", "ts_ls" }
      
      for _, server in ipairs(servers) do
        lspconfig[server].setup({
          on_attach = on_attach,
          capabilities = capabilities,
        })
      end

      lspconfig.lua_ls.setup({
        on_attach = on_attach,
        capabilities = capabilities,
        settings = {
          Lua = {
            diagnostics = {
              globals = { "vim" },
            },
            workspace = {
              library = vim.api.nvim_get_runtime_file("", true),
            },
            telemetry = {
              enable = false,
            },
          },
        },
      })
    end,
  },
}
```

## Autocompletion with nvim-cmp

LSP provides completion data, but you need a completion plugin to display it nicely.

### Install nvim-cmp

```lua
{
  "hrsh7th/nvim-cmp",
  dependencies = {
    "hrsh7th/cmp-nvim-lsp",     -- LSP completions
    "hrsh7th/cmp-buffer",       -- Buffer completions
    "hrsh7th/cmp-path",         -- Path completions
    "L3MON4D3/LuaSnip",         -- Snippet engine
    "saadparwaiz1/cmp_luasnip", -- Snippet completions
  },
  config = function()
    local cmp = require("cmp")
    local luasnip = require("luasnip")

    cmp.setup({
      snippet = {
        expand = function(args)
          luasnip.lsp_expand(args.body)
        end,
      },
      mapping = cmp.mapping.preset.insert({
        ["<C-k>"] = cmp.mapping.select_prev_item(),
        ["<C-j>"] = cmp.mapping.select_next_item(),
        ["<C-b>"] = cmp.mapping.scroll_docs(-4),
        ["<C-f>"] = cmp.mapping.scroll_docs(4),
        ["<C-Space>"] = cmp.mapping.complete(),
        ["<C-e>"] = cmp.mapping.abort(),
        ["<CR>"] = cmp.mapping.confirm({ select = false }),
      }),
      sources = cmp.config.sources({
        { name = "nvim_lsp" },
        { name = "luasnip" },
        { name = "buffer" },
        { name = "path" },
      }),
    })
  end,
}
```

### nvim-cmp Keybindings

| Key | Action |
|-----|--------|
| `<C-k>` | Previous item |
| `<C-j>` | Next item |
| `<C-Space>` | Trigger completion |
| `<CR>` | Confirm selection |
| `<C-e>` | Close completion menu |
| `<C-b>` | Scroll docs up |
| `<C-f>` | Scroll docs down |

## Diagnostic Configuration

Customize how errors and warnings are displayed:

```lua
vim.diagnostic.config({
  virtual_text = true,
  signs = true,
  update_in_insert = false,
  underline = true,
  severity_sort = true,
  float = {
    focusable = false,
    style = "minimal",
    border = "rounded",
    source = "always",
    header = "",
    prefix = "",
  },
})

local signs = {
  Error = " ",
  Warn = " ",
  Hint = " ",
  Info = " ",
}

for type, icon in pairs(signs) do
  local hl = "DiagnosticSign" .. type
  vim.fn.sign_define(hl, { text = icon, texthl = hl, numhl = hl })
end
```

### Diagnostic Display Options

- `virtual_text` - Show errors inline
- `signs` - Show icons in sign column
- `underline` - Underline problematic code
- `severity_sort` - Sort by severity (errors first)
- `float.border` - Floating window border style

## Language-Specific Configuration

### Python (pyright)

```lua
lspconfig.pyright.setup({
  on_attach = on_attach,
  capabilities = capabilities,
  settings = {
    python = {
      analysis = {
        typeCheckingMode = "basic",
        autoSearchPaths = true,
        useLibraryCodeForTypes = true,
      },
    },
  },
})
```

### TypeScript (ts_ls)

```lua
lspconfig.ts_ls.setup({
  on_attach = on_attach,
  capabilities = capabilities,
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
lspconfig.rust_analyzer.setup({
  on_attach = on_attach,
  capabilities = capabilities,
  settings = {
    ["rust-analyzer"] = {
      cargo = {
        allFeatures = true,
      },
      checkOnSave = {
        command = "clippy",
      },
    },
  },
})
```

### Lua (lua_ls)

```lua
lspconfig.lua_ls.setup({
  on_attach = on_attach,
  capabilities = capabilities,
  settings = {
    Lua = {
      runtime = {
        version = "LuaJIT",
      },
      diagnostics = {
        globals = { "vim" },
      },
      workspace = {
        library = vim.api.nvim_get_runtime_file("", true),
        checkThirdParty = false,
      },
      telemetry = {
        enable = false,
      },
    },
  },
})
```

## Formatting

### Format on Save

```lua
local on_attach = function(client, bufnr)
  if client.supports_method("textDocument/formatting") then
    vim.api.nvim_create_autocmd("BufWritePre", {
      buffer = bufnr,
      callback = function()
        vim.lsp.buf.format({ async = false })
      end,
    })
  end
end
```

### Manual Formatting

```lua
vim.keymap.set("n", "<leader>f", function()
  vim.lsp.buf.format({ async = true })
end, { desc = "Format buffer" })
```

## Useful LSP Commands

| Command | Purpose |
|---------|---------|
| `:LspInfo` | Show attached LSP clients |
| `:LspStart` | Start LSP client |
| `:LspStop` | Stop LSP client |
| `:LspRestart` | Restart LSP client |
| `:Mason` | Open Mason UI |
| `:checkhealth lsp` | Check LSP health |

## Advanced Features

### Inlay Hints

Show type hints inline (supported by some servers):

```lua
vim.lsp.inlay_hint.enable(true)
```

### Codelens

Show executable actions above code:

```lua
vim.api.nvim_create_autocmd({ "BufEnter", "CursorHold", "InsertLeave" }, {
  pattern = "<buffer>",
  callback = vim.lsp.codelens.refresh,
})
```

### Workspace Folders

Manage multi-root workspaces:

```lua
vim.keymap.set("n", "<leader>wa", vim.lsp.buf.add_workspace_folder)
vim.keymap.set("n", "<leader>wr", vim.lsp.buf.remove_workspace_folder)
```

## Troubleshooting

### LSP Not Starting

Check if server is attached:
```vim
:LspInfo
```

### No Completions

1. Verify nvim-cmp is installed
2. Check capabilities are passed to server:
   ```lua
   local capabilities = require("cmp_nvim_lsp").default_capabilities()
   lspconfig.pyright.setup({ capabilities = capabilities })
   ```

### Slow LSP

Some servers are resource-intensive. Optimize:

```lua
lspconfig.ts_ls.setup({
  on_attach = function(client)
    client.server_capabilities.documentFormattingProvider = false
  end,
})
```

### View LSP Logs

```vim
:lua vim.cmd('e ' .. vim.lsp.get_log_path())
```

## Complete Example

See [examples/basic/init.lua](../../examples/basic/init.lua) for a complete, working configuration.

## Best Practices

1. **Use on_attach** - Configure keybindings per buffer
2. **Set capabilities** - Enable completion support
3. **Configure diagnostics** - Customize error display
4. **Add formatting** - Format on save for consistency
5. **Language-specific** - Tune settings per language
6. **Check health** - Run `:checkhealth lsp` regularly

## Exercises

1. **Add keybindings** - Set up LSP keybindings in your config
2. **Install nvim-cmp** - Add completion support
3. **Test features** - Try gd, K, and code actions
4. **Customize diagnostics** - Change error icons and display
5. **Add formatting** - Enable format on save

## Next Steps

You now have a complete LSP setup! Continue to:
- [Module 6: Advanced](../06-advanced/README.md) - Lua scripting and automation
- Explore language-specific plugins
- Customize your workflow further

## Resources

- [nvim-lspconfig docs](https://github.com/neovim/nvim-lspconfig)
- [nvim-cmp docs](https://github.com/hrsh7th/nvim-cmp)
- [Neovim LSP guide](https://neovim.io/doc/user/lsp.html)
- [Server configurations](https://github.com/neovim/nvim-lspconfig/blob/master/doc/server_configurations.md)
