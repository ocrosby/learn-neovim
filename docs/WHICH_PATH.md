# Which Learning Path Should I Follow?

Use this guide to find the fastest path for your situation.

## Quick Decision Tree

```
Are you brand new to Vim/Neovim?
│
├─ YES → Have you completed :Tutor?
│   │
│   ├─ NO  → Start here: Run :Tutor (30 min)
│   │        Then: Read QUICKSTART.md
│   │        Then: Use minimal config for Week 1
│   │
│   └─ YES → Follow FIRST_WEEK_CHECKLIST.md
│             Use minimal config
│             Focus on muscle memory
│
└─ NO (I know Vim basics) → Are you comfortable with hjkl, modes, basic editing?
    │
    ├─ YES → Ready for plugins and LSP!
    │        • Try the basic example config
    │        • Start Module 3: Configuration
    │        • Add features gradually
    │
    └─ NO  → Review the basics first
              • Module 1: Basics
              • Practice with minimal config
              • Focus on fundamentals
```

## By Time Available

### I Have 30 Minutes
**Goal:** Understand what Neovim is and try it

1. Read [QUICKSTART.md](QUICKSTART.md) (10 min)
2. Open Neovim and run `:Tutor` (20 min)
3. Done! Come back when you have more time

### I Have 1 Hour
**Goal:** Get functional with Neovim

1. Complete `:Tutor` (30 min)
2. Practice survival commands in a scratch file (15 min)
3. Try editing one real file (15 min)
4. Bookmark [FIRST_WEEK_CHECKLIST.md](FIRST_WEEK_CHECKLIST.md) for tomorrow

### I Have 1 Day
**Goal:** Complete Day 1 of your learning journey

1. Morning: Complete `:Tutor` + survival commands (1 hour)
2. Afternoon: Practice basic navigation (1 hour)
3. Evening: Real work practice (1-2 hours)
4. End: Review [FIRST_WEEK_CHECKLIST.md](FIRST_WEEK_CHECKLIST.md) Day 1

### I Have 1 Week
**Goal:** Become functional with Neovim

Follow [FIRST_WEEK_CHECKLIST.md](FIRST_WEEK_CHECKLIST.md) day by day:
- Days 1-3: Survival and basics (hardest part)
- Days 4-5: Speed and power commands
- Days 6-7: Real work and assessment

After 1 week, you'll be functional!

### I Have 1 Month
**Goal:** Become proficient and build your perfect setup

**Week 1:** [FIRST_WEEK_CHECKLIST.md](FIRST_WEEK_CHECKLIST.md) with minimal config  
**Week 2:** [Module 2: Intermediate](../docs/02-intermediate/) - Text objects, registers, macros  
**Week 3:** [Module 3: Configuration](../docs/03-configuration/) + try basic config  
**Week 4:** [Module 4-5: Plugins & LSP](../docs/04-plugin-management/) - Add IDE features  

After 1 month, you'll be faster than your old editor!

## By Background

### Coming from VSCode
**You'll love:** LSP integration, fuzzy finding, Git integration  
**You'll miss:** Mouse usage, GUI features  
**Strategy:**
1. Week 1: Learn Neovim basics with minimal config
2. Week 2: Switch to basic config (feels more like VSCode)
3. Week 3+: Gradually add your favorite VSCode features

**Quick wins:**
- `Ctrl-p` equivalent: Telescope (in basic config)
- File explorer: nvim-tree (in basic config)
- Git gutter: gitsigns (in basic config)

### Coming from JetBrains (PyCharm, IntelliJ)
**You'll love:** Speed, keyboard-focused workflow  
**You'll miss:** Heavy refactoring tools, visual debugger  
**Strategy:**
1. Week 1-2: Learn basics with minimal config
2. Week 3: Add LSP (basic config)
3. Week 4+: Add debugging (language-specific configs)

**Quick wins:**
- Go to definition: Built-in LSP
- Refactoring: LSP + custom functions
- Debugging: nvim-dap (in Python/Web configs)

### Coming from Sublime/Atom
**You'll love:** Speed, extensibility, modal editing  
**You'll miss:** Simplicity, immediate usability  
**Strategy:**
1. Week 1: Basics with minimal config (embrace the learning curve)
2. Week 2: Basic config (feels familiar again)
3. Week 3+: Customize to match your Sublime workflow

**Quick wins:**
- Multiple cursors: Visual block mode (`Ctrl-v`)
- Fuzzy search: Telescope
- Project-wide search: Telescope + ripgrep

### Coming from Emacs
**You'll love:** Speed, simplicity, focus  
**You'll miss:** Org-mode, infinite customization  
**Strategy:**
1. Week 1: Learn modal editing (different from Emacs)
2. Week 2-3: Basic + intermediate features
3. Week 4+: Explore Lua scripting (similar power to elisp)

**Quick wins:**
- Keybinding changes: Easy with `vim.keymap.set()`
- Custom functions: Lua is simpler than elisp
- Modes: More focused than Emacs major/minor modes

## By Learning Style

### I Learn by Doing
**Your path:**
1. Run `:Tutor` immediately
2. Practice with real work from Day 1
3. Look up commands as you need them
4. Use [QUICKSTART.md](QUICKSTART.md) as reference

**Resources:**
- [FIRST_WEEK_CHECKLIST.md](FIRST_WEEK_CHECKLIST.md)
- Practice exercises in `docs/01-basics/exercises/`

### I Learn by Reading
**Your path:**
1. Read [QUICKSTART.md](QUICKSTART.md) thoroughly
2. Read Module 0-1 documentation
3. Then practice with exercises
4. Refer back to docs frequently

**Resources:**
- All module documentation in `docs/`
- [Cheatsheets](../resources/cheatsheets/)
- `:help` in Neovim

### I Learn by Watching
**Your path:**
1. Watch videos first (see [resources/videos.md](../resources/videos.md))
2. Follow along in Neovim
3. Then try on your own
4. Watch again when stuck

**Resources:**
- [Video resources](../resources/videos.md)
- ThePrimeagen's Neovim tutorials
- TJ DeVries' streams

### I Learn by Example
**Your path:**
1. Try example configs immediately
2. Start with [minimal config](../examples/minimal/)
3. Read the code to understand
4. Modify and experiment

**Resources:**
- All [example configs](../examples/)
- Each config is heavily commented

## By Goal

### I Want to Be Productive ASAP
**Timeline:** 1 week to functional

**Fast track:**
1. Day 1: `:Tutor` + survival commands (2 hours)
2. Days 2-3: Practice with real work (1 hour/day)
3. Days 4-7: Use for all work, fall back when needed

**Skip:**
- Deep theory
- Advanced customization
- Perfect muscle memory

**Focus on:**
- Essential commands only
- Real work immediately
- Progress over perfection

### I Want to Master Neovim
**Timeline:** 1-3 months to mastery

**Thorough path:**
1. Week 1: Basics with minimal config
2. Week 2: Intermediate skills
3. Week 3-4: Configuration and plugins
4. Month 2: Language-specific optimization
5. Month 3+: Advanced features and customization

**Don't skip:**
- Any module
- Practice exercises
- Building your own config

**Focus on:**
- Understanding why, not just what
- Muscle memory through repetition
- Building a config you understand completely

### I Want to Replace My IDE
**Timeline:** 2-4 weeks to IDE-level features

**IDE replacement path:**
1. Week 1: Learn Neovim basics (minimal config)
2. Week 2: Add LSP (basic config)
3. Week 3: Add debugging and testing (language-specific)
4. Week 4: Polish and optimize

**Must-learn:**
- LSP (Module 5)
- Debugging with nvim-dap (Module 7)
- Git integration (Module 7)
- Language-specific configs

### I Just Want to Edit Files on Servers
**Timeline:** 1 day to functional for remote editing

**Minimal path:**
1. Learn survival commands (30 min)
2. Learn basic navigation (30 min)
3. Practice editing a file (30 min)

**That's it!** You don't need:
- Plugins
- Configuration
- Advanced features

**Use:**
- Vanilla Neovim
- [QUICKSTART.md](QUICKSTART.md) as reference

## By Language

### Python Developer
**Path:**
1. Weeks 1-2: Learn Neovim basics
2. Week 3: Switch to [Python config](../examples/python-dev/)
3. Features: pyright, ruff, pytest, debugging

**See:** [Python Dev Config](../examples/python-dev/)

### JavaScript/TypeScript Developer
**Path:**
1. Weeks 1-2: Learn Neovim basics
2. Week 3: Switch to [Web Dev config](../examples/web-dev/)
3. Features: tsserver, ESLint, Tailwind, Jest

**See:** [Web Dev Config](../examples/web-dev/)

### Other Languages
**Path:**
1. Weeks 1-2: Learn Neovim basics
2. Week 3: Start with [Basic config](../examples/basic/)
3. Week 4: Customize for your language

**Add your language server:**
```lua
-- In mason-lspconfig setup:
ensure_installed = {
  "rust_analyzer",  -- Rust
  "gopls",          -- Go
  "clangd",         -- C/C++
  "jdtls",          -- Java
}
```

## Still Not Sure?

### Default Path for Most People

This works for 90% of users:

1. **Day 1:** Run `:Tutor`, read [QUICKSTART.md](QUICKSTART.md)
2. **Week 1:** Follow [FIRST_WEEK_CHECKLIST.md](FIRST_WEEK_CHECKLIST.md)
3. **Week 2:** Start [Module 2: Intermediate](../docs/02-intermediate/)
4. **Week 3:** Add plugins with [Basic config](../examples/basic/)
5. **Week 4+:** Customize for your needs

### When in Doubt

**Start here:**
1. Open Neovim: `nvim`
2. Run the tutorial: `:Tutor`
3. Come back when done and follow [FIRST_WEEK_CHECKLIST.md](FIRST_WEEK_CHECKLIST.md)

**That's all you need to decide right now!**

## Quick Reference

| Your Situation | Start Here | Time Needed |
|---------------|------------|-------------|
| Never used Vim | `:Tutor` + [QUICKSTART.md](QUICKSTART.md) | 1 hour |
| Know Vim basics | [Module 1: Basics](../docs/01-basics/) | 2-3 hours |
| Want plugins | [Basic config](../examples/basic/) + Module 3 | 3-4 hours |
| Want IDE features | [Basic config](../examples/basic/) + Module 5 | 4-6 hours |
| Language-specific | [Example configs](../examples/) | 1 week |

---

**Can't decide?** Just run `:Tutor` - you'll know what to do next after that! 🚀
