# What is LSP?

LSP (Language Server Protocol) is a standardized protocol that provides IDE-like features (autocomplete, go-to-definition, diagnostics) for any editor that implements it.

## The Problem LSP Solves

**Before LSP**: Every editor needed custom integration for each language.

- Vim needed a Python plugin, a JavaScript plugin, a Rust plugin, etc.
- Each language * editor combination required separate tools
- Maintainers had to support multiple editors

**With LSP**: One language server works with all editors.

- Write a language server once
- Works with Neovim, VSCode, Emacs, Sublime, etc.
- Editors implement LSP client, servers provide language intelligence

## How LSP Works

```
┌─────────────┐                    ┌─────────────────┐
│   Neovim    │ ◄─── LSP ───────► │ Language Server │
│  (Client)   │   (JSON-RPC)       │   (pyright,     │
│             │                    │   rust-analyzer)│
└─────────────┘                    └─────────────────┘
```

1. **You edit code** in Neovim
2. **Neovim sends** file changes to language server
3. **Server analyzes** code (type checking, syntax analysis)
4. **Server responds** with diagnostics, completions, etc.
5. **Neovim displays** the results

## What LSP Provides

### 1. Diagnostics

Real-time error and warning messages:

```python
def greet(name):
    return f"Hello {nme}"  # ← Error: 'nme' is not defined
```

### 2. Autocompletion

Smart suggestions based on context:

```lua
local M = {}
M.greet = function(name)
  return "Hello " .. name
end

M.  -- ← Completion suggests: greet
```

### 3. Go to Definition

Jump to where a function/variable is defined:

```javascript
import { formatDate } from './utils'
//       └─────┬─────┘
//    gd jumps here ─────┐
//                        ↓
// utils.js
export function formatDate(date) { ... }
```

### 4. Hover Documentation

View documentation without leaving your file:

```typescript
Math.floor(3.7)
//   └─┬──┘
// Hover shows: Returns the largest integer less than or equal to a number
```

### 5. Find References

See everywhere a symbol is used:

```go
func calculateTotal(items []Item) float64 { ... }
//   └──────┬──────┘
// gr finds all calls to calculateTotal
```

### 6. Code Actions

Quick fixes and refactoring:

```python
x = 5
unused_variable = 10  # ← Code action: Remove unused variable
```

### 7. Rename Symbol

Rename across entire project:

```ruby
def old_name
  ...
end

old_name()  # Rename to new_name everywhere
```

### 8. Formatting

Auto-format code according to style guide:

```javascript
// Before
function    hello(   name   ){return "Hi "+name}

// After formatting
function hello(name) {
  return "Hi " + name
}
```

## Popular Language Servers

| Language | Server | Install |
|----------|--------|---------|
| Python | pyright | `pip install pyright` |
| JavaScript/TypeScript | typescript-language-server | `npm i -g typescript-language-server` |
| Lua | lua-ls | Via Mason |
| Rust | rust-analyzer | Via rustup |
| Go | gopls | `go install golang.org/x/tools/gopls@latest` |
| C/C++ | clangd | Package manager |
| Java | jdtls | Via Mason |
| Ruby | solargraph | `gem install solargraph` |

## Neovim's Built-in LSP Client

Neovim 0.5+ includes a native LSP client, meaning:

- ✅ No external dependencies needed
- ✅ Fast and integrated
- ✅ Actively maintained by core team
- ✅ Standard Lua API

**What you need**:
1. **nvim-lspconfig** - Configurations for common language servers
2. **A language server** - The actual language server binary
3. **nvim-cmp** (optional) - Better completion UI

## LSP vs. Traditional Tools

### Traditional: Linters and CTags

```
┌──────────┐     ┌──────────┐     ┌──────────┐
│  Linter  │     │  CTags   │     │ AutoComp │
│ (pylint) │     │(Generate)│     │ (Youcomp)│
└──────────┘     └──────────┘     └──────────┘
     ↓                ↓                 ↓
  Separate tools, different configs, outdated info
```

### LSP: Unified Interface

```
         ┌─────────────────────────┐
         │   Language Server       │
         │ (All features in one)   │
         └─────────────────────────┘
                    ↓
  Always up-to-date, single configuration
```

## LSP Workflow Example

Let's say you're writing Python:

1. **Start Neovim** - LSP client is ready
2. **Open Python file** - Neovim starts `pyright`
3. **Type code**:
   ```python
   import reques
   #         └─┬──┘
   #  Completion suggests: requests
   ```
4. **Make an error**:
   ```python
   result = my_function()
   #        └────┬─────┘
   #   Diagnostic: 'my_function' is not defined
   ```
5. **Hover over stdlib**:
   ```python
   print()
   # Shows: print(*values, sep=' ', end='\n', file=sys.stdout, flush=False)
   ```

## Limitations

LSP is powerful but not magic:

- **Requires language server**: Must install for each language
- **Setup needed**: Configuration required per language
- **Memory usage**: Language servers can be resource-intensive
- **Project-specific**: Some servers need project configuration (tsconfig.json, Cargo.toml)

## What's Next

Now that you understand LSP:

1. **[Install Mason](mason.md)** - Easy language server installation
2. **[Configure LSP](configuration.md)** - Set up keybindings and features

## Key Takeaways

- LSP = standardized protocol for editor ↔ language server communication
- One server works with all LSP-compatible editors
- Provides: diagnostics, completion, go-to-definition, formatting, etc.
- Neovim has built-in LSP client (no plugins needed for core)
- Still need: nvim-lspconfig (configs) + language servers (binaries)

## Exercises

1. **Check LSP support** - Run `:checkhealth lsp` in Neovim
2. **Read about servers** - Visit [nvim-lspconfig server list](https://github.com/neovim/nvim-lspconfig/blob/master/doc/server_configurations.md)
3. **Identify your languages** - List language servers you'll need for your workflow

## Resources

- [LSP Specification](https://microsoft.github.io/language-server-protocol/)
- [Neovim LSP Docs](https://neovim.io/doc/user/lsp.html)
- [nvim-lspconfig](https://github.com/neovim/nvim-lspconfig)
