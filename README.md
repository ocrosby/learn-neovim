# Learn Neovim

> A structured, comprehensive guide to mastering Neovim from beginner to advanced.

[![Neovim](https://img.shields.io/badge/Neovim-0.9+-green.svg)](https://neovim.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

**Learn Neovim** is a complete learning path for Neovim with clear documentation, practical exercises, working examples, and real-world workflows. This is not a Neovim distribution or pre-built config—it's a curated educational resource to help you build your own perfect setup.

## 🎯 What You'll Learn

- **Fundamentals**: Modal editing, motions, and Vim's composable language
- **Configuration**: Build your own `init.lua` from scratch
- **Plugin Management**: Install and configure essential plugins with lazy.nvim
- **LSP Integration**: Transform Neovim into a full IDE with language servers
- **Advanced Techniques**: Lua scripting, autocommands, and custom functions
- **Complete Workflows**: Git integration, debugging, testing, and project-specific configs

## 👥 Who This Is For

- ✅ **Beginners**: Never used Vim or Neovim before
- ✅ **Vim Users**: Want to migrate to Neovim and use modern features
- ✅ **IDE Users**: Coming from VSCode, JetBrains, etc.
- ✅ **Curious Developers**: Want to understand their editor deeply
- ✅ **Efficiency Seekers**: Want to code faster and more efficiently

## 🚀 Quick Start

### Try an Example Config (No Installation Required)

```bash
# Clone the repository
git clone https://github.com/ocrosby/learn-neovim.git
cd learn-neovim

# Try the basic example
nvim -u examples/basic/init.lua

# Or try the minimal example (no plugins)
nvim -u examples/minimal/init.lua
```

### Start the Learning Path

1. **Install Neovim** (if you haven't): [Installation Guide](docs/00-introduction/installation.md)
2. **Start with Module 0**: [Introduction](docs/00-introduction/README.md)
3. **Work through modules** in order
4. **Try example configs** as you progress
5. **Build your own config** using what you've learned

## 📚 Learning Modules

### [Module 0: Introduction](docs/00-introduction/)
- Why Neovim?
- Installation for macOS, Linux, Windows
- First-time setup

**Time**: 30 minutes

### [Module 1: Basics](docs/01-basics/)
- Understanding modes (Normal, Insert, Visual, Command)
- Navigation with `hjkl` and motions
- Basic editing commands
- Working with files and buffers

**Time**: 2-3 hours | **Exercises**: 15+

### [Module 2: Intermediate](docs/02-intermediate/)
- Text objects (`iw`, `ap`, `i"`, etc.)
- Operators and motions (`d`, `c`, `y`)
- Registers and the clipboard
- Macros for repetitive tasks

**Time**: 2-3 hours | **Exercises**: 12+

### [Module 3: Configuration](docs/03-configuration/)
- Understanding `init.lua`
- Setting options (`vim.opt`)
- Creating keymaps (`vim.keymap.set`)
- Configuration best practices

**Time**: 1-2 hours

### [Module 4: Plugin Management](docs/04-plugin-management/)
- Installing lazy.nvim
- Essential plugins (Telescope, nvim-tree, Treesitter, etc.)
- Plugin configuration patterns
- Lazy loading for performance

**Time**: 2-3 hours

### [Module 5: LSP (Language Server Protocol)](docs/05-lsp/)
- What is LSP and why it matters
- Installing language servers with Mason
- Configuring LSP features
- Autocompletion with nvim-cmp

**Time**: 2-4 hours

### [Module 6: Advanced](docs/06-advanced/)
- Lua scripting for Neovim
- Creating autocommands
- Building custom functions
- Understanding the Neovim API

**Time**: 3-5 hours

### [Module 7: Workflows](docs/07-workflows/)
- Git integration (gitsigns, fugitive, diffview)
- Debugging with nvim-dap
- Testing with neotest
- Project-specific configurations

**Time**: 3-4 hours

**Total Learning Time**: 15-25 hours spread over several weeks

## 💻 Example Configurations

Ready-to-use configs you can try immediately:

### [Minimal](examples/minimal/) - 31 lines, 0 plugins
Perfect for learning core Vim/Neovim without distractions.

```bash
nvim -u examples/minimal/init.lua
```

### [Basic](examples/basic/) - ~300 lines, 14 plugins
Complete, modern setup with LSP, fuzzy finding, Git integration.

```bash
nvim -u examples/basic/init.lua
```

### [Python Development](examples/python-dev/) - ~350 lines, 17 plugins
Optimized for Python with pytest, debugging, virtual env support.

```bash
nvim -u examples/python-dev/init.lua
```

### [Web Development](examples/web-dev/) - ~340 lines, 18 plugins
Built for JavaScript/TypeScript/React with ESLint, Tailwind, Jest.

```bash
nvim -u examples/web-dev/init.lua
```

[See all examples →](examples/)

## 📖 Resources

### Cheatsheets
- [Basic Commands](resources/cheatsheets/basics.md) - Essential Vim/Neovim commands

### External Resources
- [Articles](resources/articles.md) - Curated blog posts and guides
- [Videos](resources/videos.md) - YouTube tutorials and screencasts
- [Communities](resources/communities.md) - Where to get help and connect

## 🎓 Learning Philosophy

This resource follows these principles:

### 1. **Progressive Learning**
Start with basics, gradually add complexity. No overwhelming config dumps.

### 2. **Understanding Over Copying**
Learn *why* things work, not just *what* to copy-paste.

### 3. **Hands-On Practice**
Every module includes exercises and practical examples.

### 4. **Build Your Own**
Create your personalized config from scratch, understanding every line.

### 5. **Well-Documented**
Clear explanations with links to official docs for deeper learning.

## 🗺️ Recommended Learning Path

### Week 1-2: Fundamentals
- Complete Modules 0-1 (Introduction & Basics)
- Use the [minimal config](examples/minimal/)
- Focus on staying in Normal mode
- Practice basic motions daily

### Week 3-4: Intermediate Skills
- Complete Module 2 (Intermediate)
- Learn text objects and operators
- Start using macros
- Continue with minimal config

### Week 5-6: Configuration & Plugins
- Complete Modules 3-4 (Configuration & Plugin Management)
- Switch to [basic config](examples/basic/)
- Add plugins one at a time
- Understand what each plugin does

### Week 7-8: IDE Features
- Complete Module 5 (LSP)
- Set up language servers for your languages
- Configure autocompletion
- Learn LSP keybindings

### Week 9-10: Advanced & Workflows
- Complete Modules 6-7 (Advanced & Workflows)
- Try language-specific examples
- Add debugging and testing
- Create project-specific configs

### Ongoing: Mastery
- Customize your config
- Explore new plugins
- Help others learn
- Contribute back

## 🛠️ Prerequisites

### Required
- **Neovim** 0.9.0 or newer
- **Git**
- **Terminal** that supports 256 colors

### Recommended
- **A Nerd Font** for icons (optional but nice)
- **ripgrep** for fuzzy finding (`brew install ripgrep`)
- **Node.js** for some LSP servers (web development)
- **Python 3** for some LSP servers (Python development)

See [Installation Guide](docs/00-introduction/installation.md) for detailed setup.

## 📊 Repository Structure

```
learn-neovim/
├── docs/                      # Learning modules
│   ├── 00-introduction/       # Getting started
│   ├── 01-basics/            # Fundamental concepts
│   ├── 02-intermediate/      # Text objects, operators
│   ├── 03-configuration/     # Understanding init.lua
│   ├── 04-plugin-management/ # lazy.nvim and plugins
│   ├── 05-lsp/              # Language Server Protocol
│   ├── 06-advanced/         # Lua scripting
│   └── 07-workflows/        # Git, debugging, testing
├── examples/                 # Ready-to-use configs
│   ├── minimal/             # No plugins (31 lines)
│   ├── basic/               # Complete starter (300 lines)
│   ├── python-dev/          # Python optimized
│   └── web-dev/             # Web development
├── resources/               # Reference materials
│   ├── cheatsheets/        # Quick references
│   ├── articles.md         # Curated articles
│   ├── videos.md           # Video tutorials
│   └── communities.md      # Where to get help
└── README.md               # You are here!
```

## 🤝 Contributing

Contributions are welcome! Whether it's:

- 🐛 Fixing typos or errors
- 📝 Improving documentation
- 💡 Suggesting new content
- 🎓 Sharing your learning experience
- 🔧 Adding example configs

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## ❓ FAQ

### Is this a Neovim distribution like LazyVim or NvChad?

No. This is an educational resource to help you build your own config. Distributions are great, but understanding how to build your own gives you complete control.

### Do I need to know Vim first?

No! This guide starts from the very beginning and assumes no Vim/Neovim experience.

### Do I need to know Lua?

No! We teach you the Lua you need as you go. You'll learn by doing.

### Can I use this if I'm happy with VSCode?

Absolutely! Many developers use both. Neovim excels at remote editing, efficient text manipulation, and can be faster once you master it.

### How long does it take to become productive?

- **Basic proficiency**: 2-4 weeks of daily use
- **Comfortable**: 2-3 months
- **Advanced**: 6-12 months
- **Mastery**: Years (like any tool)

The key is daily practice!

### Do I need to use all the plugins?

No! Start minimal and add only what you need. The example configs show different levels of complexity.

### What if I get stuck?

- Check the built-in help: `:help <topic>`
- Read the relevant module
- Ask in [communities](resources/communities.md)
- Open an issue in this repository

## 🙏 Acknowledgments

This resource builds on the excellent work of the Neovim community:

- [Neovim](https://neovim.io) core team
- [lazy.nvim](https://github.com/folke/lazy.nvim) by folke
- [kickstart.nvim](https://github.com/nvim-lua/kickstart.nvim) for inspiration
- ThePrimeagen, TJ DeVries, and other Neovim educators
- The entire Vim and Neovim community

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

Feel free to use, modify, and share this resource however it helps you learn!

## ⭐ Support This Project

If this resource helped you learn Neovim:

- ⭐ Star this repository
- 🐦 Share it with others
- 🤝 Contribute improvements
- 💬 Share your success story

## 🚦 Ready to Start?

Begin your Neovim journey:

**→ [Start with Module 0: Introduction](docs/00-introduction/README.md)**

Or jump straight to trying an example:

```bash
git clone https://github.com/ocrosby/learn-neovim.git
cd learn-neovim
nvim -u examples/basic/init.lua
```

---

**Happy learning!** Remember: everyone starts as a beginner. Take it step by step, practice daily, and you'll be amazed at how productive you can become. 🚀
