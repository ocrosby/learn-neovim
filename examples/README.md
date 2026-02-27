# Neovim Configuration Examples

Ready-to-use Neovim configurations for different experience levels and use cases. Each example is fully documented and can be tried without affecting your current setup.

## 🎯 Which Config Should I Use?

**Brand new to Neovim?** → Start with [Minimal](./minimal/)  
**Finished `:Tutor` and basic lessons?** → Try [Basic](./basic/)  
**Comfortable with Neovim?** → Use language-specific configs

## Quick Start

Try any config without installing:

```bash
# From repository root

# 👈 START HERE - No plugins, perfect for learning
nvim -u examples/minimal/init.lua

# Try after you're comfortable with basics
nvim -u examples/basic/init.lua
nvim -u examples/python-dev/init.lua
nvim -u examples/web-dev/init.lua
```

## Available Configurations

### 1. [Minimal](./minimal/) - 👈 **START HERE**

**No plugins. Just essential Vim/Neovim settings.**

```lua
-- 31 lines total
-- 10 options, 7 keybindings
-- 0 plugins
```

**Perfect for:**
- Absolute beginners learning Vim motions
- Understanding core Neovim without abstractions
- Lightweight remote editing
- Learning fundamentals before adding complexity

**What you'll learn:**
- Modal editing basics
- Line numbers and navigation
- Window splits
- Essential keybindings

[View minimal configuration →](./minimal/)

---

### 2. [Basic](./basic/) - Complete Starter

**Full-featured modern editor with essential plugins.**

```lua
-- ~300 lines total
-- 14 plugins
-- LSP support (Lua, Python, TypeScript)
```

**Perfect for:**
- New users who completed the basics
- Those wanting a solid foundation
- Users migrating from VSCode/other editors
- General-purpose development

**Features:**
- Plugin management (lazy.nvim)
- LSP with Mason
- Fuzzy finding (Telescope)
- File explorer
- Git integration
- Syntax highlighting
- Autocompletion
- Modern UI

**Languages supported:**
- Lua (Neovim config development)
- Python
- TypeScript/JavaScript

[View basic configuration →](./basic/)

---

### 3. [Python Development](./python-dev/) - Python Specialist

**Optimized for Python with testing, debugging, and virtual env support.**

```lua
-- ~350 lines total
-- 17 plugins
-- Python-specific tools
```

**Perfect for:**
- Python developers
- Data scientists
- Django/Flask developers
- Anyone writing Python daily

**Additional features:**
- pyright (advanced type checking)
- ruff (fast linting & formatting)
- pytest integration (neotest)
- Debugging (nvim-dap)
- Virtual environment detection
- Format on save
- PEP 8 / Black standards

**Includes:**
- Test runner in Neovim
- Breakpoint debugging
- Type hint completions
- Project-aware Python path

[View Python configuration →](./python-dev/)

---

### 4. [Web Development](./web-dev/) - JavaScript/TypeScript/React

**Optimized for modern web development.**

```lua
-- ~340 lines total
-- 18 plugins
-- Full web stack support
```

**Perfect for:**
- Frontend developers
- Full-stack developers
- React/Vue/Next.js development
- TypeScript projects

**Additional features:**
- TypeScript/JavaScript LSP
- ESLint integration
- HTML/CSS with Emmet
- Tailwind CSS completions
- Auto-close JSX tags
- Jest/Vitest testing
- npm script shortcuts
- Package.json integration

**Frameworks supported:**
- React (JSX/TSX)
- Vue
- Next.js
- Svelte (with customization)
- Any JavaScript/TypeScript project

[View web dev configuration →](./web-dev/)

---

## Choosing a Configuration

### By Experience Level

| Experience | Recommended Config | When to Use |
|------------|-------------------|-------------|
| Complete beginner | [Minimal](./minimal/) | **Days 1-7** - Focus on Neovim itself |
| Completed `:Tutor` | [Basic](./basic/) | **Week 2-4** - Add modern features |
| Comfortable with Neovim | Language-specific | **Week 4+** - Optimize for your work |

### By Use Case

| Use Case | Recommended Config |
|----------|-------------------|
| Learning Vim | [Minimal](./minimal/) |
| General programming | [Basic](./basic/) |
| Python development | [Python Dev](./python-dev/) |
| Web development | [Web Dev](./web-dev/) |
| Multiple languages | Start with [Basic](./basic/), customize |

### By Customization Preference

| Preference | Recommended Config |
|------------|-------------------|
| Want to build from scratch | [Minimal](./minimal/) |
| Want a solid starting point | [Basic](./basic/) |
| Want optimized for my language | Language-specific |

## Installation Methods

### Method 1: Try First (Recommended)

Test without affecting your current config:

```bash
cd /path/to/learn-neovim
nvim -u examples/basic/init.lua
```

### Method 2: Temporary Switch

Use for one session:

```bash
alias nvim-basic='nvim -u ~/.config/nvim-examples/basic/init.lua'
nvim-basic
```

### Method 3: Full Installation

Replace your current config (backup first!):

```bash
# Backup existing config
mv ~/.config/nvim ~/.config/nvim.backup
mv ~/.local/share/nvim ~/.local/share/nvim.backup

# Copy chosen config
mkdir -p ~/.config/nvim
cp examples/basic/init.lua ~/.config/nvim/init.lua

# Launch
nvim
```

### Method 4: Multiple Configs

Keep multiple configs side by side:

```bash
# Install as separate configs
mkdir -p ~/.config/nvim-basic
cp examples/basic/init.lua ~/.config/nvim-basic/init.lua

mkdir -p ~/.config/nvim-python
cp examples/python-dev/init.lua ~/.config/nvim-python/init.lua

# Use with aliases
alias nvim-basic='NVIM_APPNAME=nvim-basic nvim'
alias nvim-python='NVIM_APPNAME=nvim-python nvim'
```

## Feature Comparison

| Feature | Minimal | Basic | Python | Web Dev |
|---------|---------|-------|--------|---------|
| **Lines of code** | 31 | ~300 | ~350 | ~340 |
| **Plugins** | 0 | 14 | 17 | 18 |
| **LSP** | ❌ | ✅ | ✅ | ✅ |
| **Autocompletion** | ❌ | ✅ | ✅ | ✅ |
| **File explorer** | ❌ | ✅ | ✅ | ✅ |
| **Fuzzy finder** | ❌ | ✅ | ✅ | ✅ |
| **Git integration** | ❌ | ✅ | ✅ | ✅ |
| **Testing** | ❌ | ❌ | ✅ | ✅ |
| **Debugging** | ❌ | ❌ | ✅ | ❌ |
| **Language-specific** | ❌ | ❌ | ✅ | ✅ |
| **Format on save** | ❌ | ❌ | ✅ | ✅ |

## Upgrade Path

Recommended learning progression:

```
Minimal (Week 1)
  ↓ Focus on Vim motions, modes, and navigation
  ↓ Run :Tutor, practice daily with real work
  ↓ Goal: Comfortable with hjkl, basic editing
  
Basic (Weeks 2-3)
  ↓ Learn plugins, LSP, fuzzy finding
  ↓ Add IDE features gradually
  ↓ Goal: Productive for real work
  
Language-Specific (Week 4+)
  ↓ Optimize for your primary language
  ↓ Add testing, debugging, linting
  ↓ Goal: Faster than your old editor
  
Custom Config (Ongoing)
  ↓ Build your perfect setup
  ↓ Add exactly what you need
  ↓ Goal: Editor that fits like a glove
```

**Don't skip steps!** Each phase builds essential muscle memory and understanding.

## Customization

All configs are designed to be modified:

### Start Simple, Add Gradually
1. Start with a config that matches your needs
2. Use it for a week to understand it
3. Add one plugin at a time
4. Remove what you don't use

### Common Customizations

**Change colorscheme:**
```lua
-- Replace tokyonight with:
"catppuccin/nvim"  -- Pastel colors
"ellisonleao/gruvbox.nvim"  -- Retro
"rebelot/kanagawa.nvim"  -- Japanese theme
```

**Adjust indentation:**
```lua
vim.opt.tabstop = 2      -- 2 spaces (web dev)
vim.opt.tabstop = 4      -- 4 spaces (Python)
vim.opt.expandtab = false  -- Use real tabs
```

**Add languages:**
```lua
-- In mason-lspconfig ensure_installed:
"rust_analyzer",  -- Rust
"gopls",          -- Go
"clangd",         -- C/C++
```

## Prerequisites

All configs require:
- Neovim >= 0.9.0 (check with `nvim --version`)
- Git

Language-specific configs also need:
- **Python Dev**: Python 3.8+, pip
- **Web Dev**: Node.js 16+, npm

Optional but recommended:
- A [Nerd Font](https://www.nerdfonts.com/) for icons
- ripgrep for fuzzy finding (`brew install ripgrep`)

## Troubleshooting

### Plugins Not Installing

```vim
:Lazy sync
:checkhealth lazy
```

### LSP Not Working

```vim
:LspInfo         " Check if server attached
:Mason           " Verify servers installed
:checkhealth lsp " Diagnose issues
```

### Config Not Loading

Check you're using the right path:
```bash
nvim -u /full/path/to/init.lua
```

### Want to Reset

```bash
# Remove all plugin data
rm -rf ~/.local/share/nvim

# Remove all state/cache
rm -rf ~/.local/state/nvim
rm -rf ~/.cache/nvim

# Restart Neovim
nvim
```

## Getting Help

Each example has detailed documentation:
- [Minimal README](./minimal/README.md)
- [Basic README](./basic/README.md)
- [Python Dev README](./python-dev/README.md)
- [Web Dev README](./web-dev/README.md)

Also see:
- [Full course modules](../docs/)
- [Community resources](../resources/communities.md)
- [Video tutorials](../resources/videos.md)
- `:help` in Neovim

## Contributing

Found an issue or improvement? See [../CONTRIBUTING.md](../CONTRIBUTING.md)

Suggestions for new example configs:
- Rust development
- Go development
- Data science (Jupyter integration)
- DevOps (Terraform, Docker, K8s)

## Philosophy

These configs follow these principles:

1. **Understandable**: Every line is documented
2. **Minimal**: Only essential features for the use case
3. **Practical**: Real-world development workflows
4. **Educational**: Learn by reading the config
5. **Modifiable**: Easy to customize

## What's Next?

After trying an example:

1. **Read the code**: Understand what each plugin does
2. **Use it daily**: Give it at least a week
3. **Customize**: Modify to fit your workflow
4. **Learn more**: Read the [full modules](../docs/)
5. **Build your own**: Create your perfect config

Remember: The best config is one you understand completely!

---

**Happy configuring!** 🚀
