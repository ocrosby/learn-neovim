# Installing Language Servers with Mason

Mason is a package manager for Neovim that makes installing and managing language servers, formatters, and linters incredibly easy.

## Why Mason?

**Without Mason**: Install language servers manually:
```bash
npm install -g typescript-language-server
pip install pyright
gem install solargraph
go install golang.org/x/tools/gopls@latest
```

**With Mason**: Install from within Neovim:
```vim
:MasonInstall pyright typescript-language-server lua-ls
```

## Benefits

- ✅ Install servers from within Neovim
- ✅ Cross-platform (works on Linux, macOS, Windows)
- ✅ Automatic updates
- ✅ No system dependencies
- ✅ Integrates with nvim-lspconfig

## Installation

Add these plugins to your lazy.nvim configuration:

```lua
{
  "williamboman/mason.nvim",
  "williamboman/mason-lspconfig.nvim",
  "neovim/nvim-lspconfig",
}
```

## Basic Setup

Here's a minimal configuration:

```lua
{
  "williamboman/mason.nvim",
  config = function()
    require("mason").setup()
  end,
},
{
  "williamboman/mason-lspconfig.nvim",
  dependencies = { "williamboman/mason.nvim" },
  config = function()
    require("mason-lspconfig").setup({
      ensure_installed = {
        "lua_ls",
        "pyright",
        "ts_ls",
      },
      automatic_installation = true,
    })
  end,
},
{
  "neovim/nvim-lspconfig",
  dependencies = {
    "williamboman/mason.nvim",
    "williamboman/mason-lspconfig.nvim",
  },
  config = function()
    local lspconfig = require("lspconfig")
    
    lspconfig.lua_ls.setup({})
    lspconfig.pyright.setup({})
    lspconfig.ts_ls.setup({})
  end,
},
```

## The Mason Workflow

1. **Mason** - Installs packages (language servers, formatters, linters)
2. **mason-lspconfig** - Bridges Mason with nvim-lspconfig
3. **nvim-lspconfig** - Configures language servers

```
Mason
  ↓ (installs binaries)
mason-lspconfig
  ↓ (maps to server names)
nvim-lspconfig
  ↓ (configures servers)
LSP running in Neovim
```

## Using Mason

### Open Mason UI

```vim
:Mason
```

This opens an interactive interface:

```
╭─ Mason ────────────────────────────────────────╮
│                                                 │
│  1  Install    Update    Uninstall             │
│                                                 │
│  ● lua-language-server                         │
│  ● pyright                                     │
│  ○ typescript-language-server                  │
│  ○ rust-analyzer                               │
│                                                 │
│  i = install  u = update  X = uninstall        │
│  / = search   q = close                        │
╰─────────────────────────────────────────────────╯
```

### Install from UI

1. Press `/` to search
2. Navigate with `j`/`k`
3. Press `i` to install
4. Press `u` to update
5. Press `X` to uninstall

### Install from Command

```vim
:MasonInstall pyright
:MasonInstall lua-language-server rust-analyzer
```

### Check Installed

```vim
:Mason
```

Installed packages show `●`, available show `○`.

## Automatic Installation

Configure Mason to automatically install servers:

```lua
require("mason-lspconfig").setup({
  ensure_installed = {
    "lua_ls",       -- Lua
    "pyright",      -- Python
    "ts_ls",        -- TypeScript/JavaScript
    "rust_analyzer",-- Rust
    "gopls",        -- Go
    "clangd",       -- C/C++
  },
  automatic_installation = true,
})
```

Now these servers install automatically on first run!

## Common Language Servers

| Language | Mason Name | Server Name (lspconfig) |
|----------|------------|-------------------------|
| Lua | lua-language-server | lua_ls |
| Python | pyright | pyright |
| TypeScript/JavaScript | typescript-language-server | ts_ls |
| Rust | rust-analyzer | rust_analyzer |
| Go | gopls | gopls |
| C/C++ | clangd | clangd |
| Java | jdtls | jdtls |
| Ruby | solargraph | solargraph |
| HTML | html-lsp | html |
| CSS | css-lsp | cssls |
| JSON | json-lsp | jsonls |
| Bash | bash-language-server | bashls |

## Complete Configuration Example

```lua
return {
  {
    "williamboman/mason.nvim",
    config = function()
      require("mason").setup({
        ui = {
          icons = {
            package_installed = "✓",
            package_pending = "➜",
            package_uninstalled = "✗",
          },
        },
      })
    end,
  },
  
  {
    "williamboman/mason-lspconfig.nvim",
    dependencies = { "williamboman/mason.nvim" },
    config = function()
      require("mason-lspconfig").setup({
        ensure_installed = {
          "lua_ls",
          "pyright",
          "ts_ls",
          "rust_analyzer",
        },
        automatic_installation = true,
      })
    end,
  },

  {
    "neovim/nvim-lspconfig",
    dependencies = {
      "williamboman/mason.nvim",
      "williamboman/mason-lspconfig.nvim",
    },
    config = function()
      local lspconfig = require("lspconfig")
      local capabilities = require("cmp_nvim_lsp").default_capabilities()

      local servers = { "lua_ls", "pyright", "ts_ls", "rust_analyzer" }
      
      for _, server in ipairs(servers) do
        lspconfig[server].setup({
          capabilities = capabilities,
        })
      end

      lspconfig.lua_ls.setup({
        capabilities = capabilities,
        settings = {
          Lua = {
            diagnostics = {
              globals = { "vim" },
            },
          },
        },
      })
    end,
  },
}
```

## Mason + Handlers (Advanced)

Automatically configure all installed servers:

```lua
require("mason-lspconfig").setup({
  ensure_installed = { "lua_ls", "pyright", "ts_ls" },
})

require("mason-lspconfig").setup_handlers({
  function(server_name)
    require("lspconfig")[server_name].setup({})
  end,
  
  ["lua_ls"] = function()
    require("lspconfig").lua_ls.setup({
      settings = {
        Lua = {
          diagnostics = {
            globals = { "vim" },
          },
        },
      },
    })
  end,
})
```

This automatically configures all installed servers with default config, plus custom config for Lua.

## Managing Other Tools

Mason also installs formatters and linters:

```vim
:MasonInstall prettier       " JavaScript/TypeScript formatter
:MasonInstall black          " Python formatter
:MasonInstall stylua         " Lua formatter
:MasonInstall eslint_d       " JavaScript linter
:MasonInstall shellcheck     " Bash linter
```

For formatting integration, see [null-ls.nvim](https://github.com/jose-elias-alvarez/null-ls.nvim) or [conform.nvim](https://github.com/stevearc/conform.nvim).

## Troubleshooting

### Server Not Starting

Check installation:
```vim
:Mason
```

Check LSP status:
```vim
:LspInfo
```

### Server Name Confusion

Mason names ≠ lspconfig names:

```lua
:MasonInstall lua-language-server   -- Mason name
lspconfig.lua_ls.setup({})          -- lspconfig name
```

Use `mason-lspconfig` to handle mapping automatically.

### Health Check

```vim
:checkhealth mason
:checkhealth lsp
```

### Logs

View logs if server fails:
```vim
:lua vim.cmd('e ' .. vim.lsp.get_log_path())
```

## Mason Commands

| Command | Purpose |
|---------|---------|
| `:Mason` | Open Mason UI |
| `:MasonInstall <package>` | Install package |
| `:MasonUninstall <package>` | Uninstall package |
| `:MasonUpdate` | Update all packages |
| `:MasonLog` | View Mason log |

## Best Practices

1. **Use ensure_installed** - Declare servers in config, not manual installs
2. **Enable automatic_installation** - Install missing servers automatically
3. **Use handlers** - Automatically configure all installed servers
4. **Check health** - Run `:checkhealth mason` after setup
5. **Update regularly** - Run `:MasonUpdate` to keep servers current

## Exercises

1. **Install Mason** - Add Mason plugins to your config
2. **Install servers** - Use `:Mason` to install language servers for your languages
3. **Test LSP** - Open a file and verify LSP features work (`:LspInfo`)
4. **Explore packages** - Browse available packages in `:Mason`
5. **Auto-install** - Configure `ensure_installed` for your workflow

## Next Steps

Now that Mason is set up, continue to [LSP Configuration](configuration.md) to learn how to:
- Set up keybindings
- Configure autocompletion
- Customize diagnostics
- Add formatting on save

## Resources

- [Mason GitHub](https://github.com/williamboman/mason.nvim)
- [mason-lspconfig GitHub](https://github.com/williamboman/mason-lspconfig.nvim)
- [Available Packages](https://mason-registry.dev/registry/list)
- [nvim-lspconfig servers](https://github.com/neovim/nvim-lspconfig/blob/master/doc/server_configurations.md)
