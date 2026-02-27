# Learn Neovim

> Your friendly guide to learning Neovim, one step at a time.

[![Neovim](https://img.shields.io/badge/Neovim-0.9+-green.svg)](https://neovim.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

**New to Neovim?** You're in the right place! This guide teaches you Neovim from scratch with clear lessons, practical exercises, and real examples. No experience required.

## ⚡ Your First Hour with Neovim

### Survival Commands (Memorize These First!)

```
i           Start typing (INSERT mode)
Esc         Stop typing (NORMAL mode)
:wq         Save and quit
:q!         Quit without saving (emergency exit!)
u           Undo
```

**That's it!** Everything else can wait. These 5 commands are your lifeline.

### Try Neovim Right Now (5 Minutes)

```bash
# Option 1: Just open Neovim (if installed)
nvim

# Option 2: Try our minimal config (no plugins, perfect for learning)
git clone https://github.com/ocrosby/learn-neovim.git
cd learn-neovim
nvim -u examples/minimal/init.lua
```

**Once inside Neovim:** Type `:Tutor` and press Enter. This 30-minute interactive tutorial teaches you the basics.

🚀 **[Complete Getting Started Guide →](docs/GETTING_STARTED.md)** - All onboarding paths in one place!

Or jump to specific guides:
- 📄 [QUICKSTART](docs/QUICKSTART.md) - First hour guide with printable cheatsheet
- 📋 [First Week Checklist](docs/FIRST_WEEK_CHECKLIST.md) - Day-by-day plan
- 🗺️ [Which Path?](docs/WHICH_PATH.md) - Find your learning path

### 🆘 I'm Stuck!

**Can't type?** Press `i` to enter INSERT mode  
**Have random characters?** Press `Esc` to get back to NORMAL mode  
**Can't quit?** Press `Esc`, then type `:q!` and press Enter  
**Messed something up?** Press `Esc`, then press `u` to undo  
**Screen is frozen?** You probably pressed `Ctrl-s` by accident - press `Ctrl-q`

### Your First Day Plan

**Hour 1:** Run `:Tutor` inside Neovim (30 min), then practice what you learned  
**Hour 2:** Open a scratch file and practice basic navigation  
**Hour 3:** Try editing one real file from your work  

**Days 2-7:** Use Neovim for ONE small task each day. Just one! Build the muscle memory slowly.

**Reality check:** You'll feel slower for 2-3 days. This is completely normal. By day 4-5, things start clicking.

---

Not ready to try yet? [Learn what Neovim is first](#-what-is-neovim)

## 👥 Is This For You?

- ✅ Never used Vim or Neovim before
- ✅ Coming from VSCode, Sublime, or other editors
- ✅ Want to code more efficiently
- ✅ Curious about modal editing
- ✅ Want to understand your tools deeply

**You don't need:** Prior Vim experience, Lua knowledge, or programming expertise beyond the basics.

## ⏱️ Realistic Timeline

- **1 hour:** Know the survival commands, complete `:Tutor`
- **1 day:** Can edit files (slowly and awkwardly)
- **3 days:** The "aha!" moment - modal editing starts making sense
- **1 week:** Functional and no longer fighting the editor
- **2 weeks:** Comfortable and approaching your old speed
- **1 month:** Faster than before and wondering why you waited so long

**The hardest part is days 1-3.** If you push through, you'll never look back.

## 🎯 What You'll Build

By following this guide, you'll:

1. **Learn modal editing** - Navigate and edit text efficiently
2. **Build your own config** - Create a setup that's perfect for you
3. **Add IDE features** - Code completion, go-to-definition, and more
4. **Master your workflow** - Git, debugging, and testing integration

## 📖 Learning Path

### Complete Beginner? Start Here 👇

**Step 1:** [Installation & Setup](docs/00-introduction/installation.md) (10 minutes)  
**Step 2:** Run `:Tutor` inside Neovim (30 minutes)  
**Step 3:** [Module 1: Basics](docs/01-basics/) (practice over 3-7 days)  

**That's your first week.** Don't skip ahead!

### After You're Comfortable

**Week 2+:** [Module 2: Intermediate](docs/02-intermediate/) - Text objects and powerful commands  
**Week 3+:** [Module 3: Configuration](docs/03-configuration/) - Build your own config  
**Week 4+:** [Module 4: Plugins](docs/04-plugin-management/) - Add features  
**Week 5+:** [Module 5: LSP](docs/05-lsp/) - Get IDE features  
**Week 6+:** [Modules 6-7: Advanced](docs/06-advanced/) - Master everything

<details>
<summary>📊 See detailed module breakdown</summary>


### [Module 0: Introduction](docs/00-introduction/)
Why Neovim, installation, and first-time setup.

### [Module 1: Basics](docs/01-basics/)
Modes, navigation, and basic editing. **Start here if Neovim is already installed.**

### [Module 2: Intermediate](docs/02-intermediate/)
Text objects, operators, registers, and macros.

### [Module 3: Configuration](docs/03-configuration/)
Build your `init.lua` config from scratch.

### [Module 4: Plugin Management](docs/04-plugin-management/)
Add plugins with lazy.nvim.

### [Module 5: LSP](docs/05-lsp/)
Get IDE features with language servers.

### [Module 6: Advanced](docs/06-advanced/)
Lua scripting and custom functions.

### [Module 7: Workflows](docs/07-workflows/)
Git, debugging, and testing integration.

</details>

## 💻 Example Configs You Can Try

<details>
<summary>🔍 View all example configurations</summary>

### [Minimal](examples/minimal/) - 31 lines, no plugins
Perfect for learning without distractions.
```bash
nvim -u examples/minimal/init.lua
```

### [Basic](examples/basic/) - Complete starter config
Modern setup with LSP, fuzzy finding, and Git.
```bash
nvim -u examples/basic/init.lua
```

### [Python Development](examples/python-dev/)
Python-specific with testing and debugging.
```bash
nvim -u examples/python-dev/init.lua
```

### [Web Development](examples/web-dev/)
JavaScript/TypeScript/React optimized.
```bash
nvim -u examples/web-dev/init.lua
```

[See all examples →](examples/)

</details>

## ❓ Common Questions

### How long until I'm productive?

**1 day:** Can use it (uncomfortably)  
**1 week:** Functional for daily work  
**2 weeks:** Comfortable and approaching old speed  

You'll be slower for the first few days—this is normal and temporary!

### Should I commit fully or gradually switch?

**Gradually!** Start with one small task per day. Use your old editor when you're under pressure. No need to go cold turkey.

### Do I need to know Vim?

Nope! This guide assumes zero Vim experience.

### Do I need to know Lua?

No—we teach you the Lua you need as you go.

### Can I still use VSCode?

Absolutely! Many developers use both. Try Neovim for remote editing or when you want speed.

### What if I get stuck?

- Press `Esc` then type `:help <topic>` inside Neovim
- Check the [🆘 I'm Stuck!](#-im-stuck) section above
- Ask in [communities](resources/communities.md)
- Open an issue in this repository

### When should I start customizing?

**Not yet!** Use vanilla Neovim (or our minimal config) for at least a week. Learn the fundamentals first, then customize.

<details>
<summary>🛠️ What do I need installed?</summary>

### Required
- **Neovim** 0.9.0 or newer
- **Git**

### Optional (can add later)
- **A Nerd Font** for icons
- **ripgrep** for fuzzy finding
- **Node.js** for web development
- **Python 3** for Python development

[Detailed installation guide →](docs/00-introduction/installation.md)

</details>

<details>
<summary>📖 Additional resources</summary>

### Cheatsheets
- [Basic Commands](resources/cheatsheets/basics.md)

### External Resources
- [Articles](resources/articles.md)
- [Videos](resources/videos.md)
- [Communities](resources/communities.md)

</details>

<details>
<summary>📊 Repository structure</summary>

```
learn-neovim/
├── docs/                      # Learning modules (0-7)
├── examples/                 # Ready-to-use configs
├── resources/               # Cheatsheets and references
└── README.md               # You are here!
```

</details>

## 🤝 Contributing

Found a typo? Have a suggestion? Want to share your learning experience? 

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to help make this guide better.

## 🚦 Ready to Start?

### Absolute Beginner Path

1. **Install Neovim:** [Installation Guide](docs/00-introduction/installation.md)
2. **Learn survival commands:** Scroll back up to [Your First Hour](#-your-first-hour-with-neovim)
3. **Run `:Tutor`:** Open Neovim and type `:Tutor` then press Enter
4. **Practice daily:** Even just 15 minutes on real work

### Quick Start (Neovim Already Installed)

```bash
# Just open Neovim and run the tutorial
nvim
# Inside Neovim, type: :Tutor
```

### Try Our Minimal Config (Recommended)

```bash
git clone https://github.com/ocrosby/learn-neovim.git
cd learn-neovim
nvim -u examples/minimal/init.lua
# Inside Neovim, type: :Tutor
```

---

**Remember:** Days 1-3 are the hardest. By day 4-5, it clicks. Stick with it! 🚀

<details>
<summary>📄 License & Acknowledgments</summary>

MIT License - use, modify, and share freely!

Thanks to the Neovim community, lazy.nvim, kickstart.nvim, and all the educators who make learning Neovim accessible.

</details>
