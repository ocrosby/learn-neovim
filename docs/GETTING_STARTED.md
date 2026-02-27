# Getting Started with Neovim - Complete Guide

**Goal:** Get you from zero to productive as fast as possible.

## 🎯 Choose Your Starting Point

### I've Never Used Neovim Before

👉 **Start here:** [5-Minute Quick Start](#5-minute-quick-start)

### I've Tried :Tutor But Want Structure

👉 **Start here:** [First Week Plan](#first-week-plan)

### I Know Vim/Neovim Basics

👉 **Start here:** [Add IDE Features](#add-ide-features)

### I'm Not Sure Where to Start

👉 **Start here:** [Decision Helper](#decision-helper)

---

## 5-Minute Quick Start

**Perfect for:** Absolute beginners who want to try immediately

### Step 1: Open Neovim (2 minutes)

```bash
# If you don't have Neovim installed:
# macOS:    brew install neovim
# Ubuntu:   sudo apt install neovim
# Windows:  winget install Neovim.Neovim

# Open Neovim
nvim
```

### Step 2: Run the Tutorial (30 minutes)

Inside Neovim, type exactly this and press Enter:

```
:Tutor
```

Follow the interactive tutorial. **Don't skip this!** It's the single best 30 minutes you can invest.

### Step 3: Practice These 5 Commands (3 minutes)

After :Tutor, practice until these feel natural:

```
i           Press this to start typing
Esc         Press this to stop typing
:wq         Type this to save and quit
:q!         Type this to quit without saving
u           Press this to undo
```

### ✅ Success Criteria

You're ready to move on when you can:
- Open Neovim without fear
- Enter and exit INSERT mode
- Save and quit intentionally
- Undo mistakes

**Next:** Continue to [First Week Plan](#first-week-plan)

---

## First Week Plan

**Perfect for:** People who completed :Tutor and want daily structure

### Overview

```
Day 1: Survival + :Tutor             [1-2 hours]
Day 2: Navigation                    [30-60 min]
Day 3: Basic Editing                 [30-60 min]
Day 4: Building Speed                [30-60 min]
Day 5: Text Objects (game changer!)  [30-60 min]
Day 6: Real Work Practice            [use as much as possible]
Day 7: Assessment & Celebration      [1 hour]
```

### Detailed Daily Plan

📋 **[Complete First Week Checklist →](FIRST_WEEK_CHECKLIST.md)**

This checklist includes:
- ☑️ Specific goals for each day
- ☑️ Checkboxes to track progress
- ☑️ Time commitments
- ☑️ Skills assessments
- ☑️ Emergency help reminders

### Daily Practice Tips

**Morning (10-15 min):**
- Review previous day's commands
- Quick practice session

**Work Time:**
- Use Neovim for ONE small task
- Keep old editor open for "urgent" work
- Take notes on what's hard

**Evening (5-10 min):**
- Reflect on what you learned
- Preview tomorrow's goals

### ✅ Success Criteria

After one week, you should:
- Navigate with hjkl without thinking
- Edit files comfortably (even if slowly)
- Use text objects (ciw, di", etc.)
- Know where to get help

**Next:** Start [Module 2: Intermediate Skills](../docs/02-intermediate/)

---

## Add IDE Features

**Perfect for:** Comfortable with Neovim basics, want LSP/plugins

### Prerequisites

Before adding IDE features, ensure you can:
- Navigate efficiently (hjkl, w/b, f/t, /)
- Edit with operators and motions (d, c, y)
- Use text objects (ciw, ci", ca()
- Work in Neovim for 30+ minutes without frustration

**If not confident:** Go back to [First Week Plan](#first-week-plan)

### Quick Start with Plugins

#### Option 1: Use Our Basic Config (Recommended)

```bash
cd learn-neovim
nvim -u examples/basic/init.lua
```

This includes:
- ✅ Plugin manager (lazy.nvim)
- ✅ LSP with Mason
- ✅ Fuzzy finder (Telescope)
- ✅ File explorer
- ✅ Git integration
- ✅ Syntax highlighting

#### Option 2: Build Your Own Config

Follow these modules in order:
1. [Module 3: Configuration](../docs/03-configuration/)
2. [Module 4: Plugins](../docs/04-plugin-management/)
3. [Module 5: LSP](../docs/05-lsp/)

**Time needed:** 4-8 hours over several days

### Language-Specific Setup

Once comfortable with basic config:

**Python:** Try [Python Dev Config](../examples/python-dev/)
- Includes: pyright, ruff, pytest, debugging

**JavaScript/TypeScript:** Try [Web Dev Config](../examples/web-dev/)
- Includes: tsserver, ESLint, Tailwind, Jest

**Other languages:** Start with basic config and add your language server

### ✅ Success Criteria

You're productive when you have:
- Code completion working
- Go-to-definition/references
- Error diagnostics
- Fuzzy file finding
- Basic Git integration

**Next:** [Module 6-7: Advanced Features](../docs/06-advanced/)

---

## Decision Helper

**Not sure which path to follow?** Answer these questions:

### 1. Have you ever used Vim/Neovim before?

**No** → Start with [5-Minute Quick Start](#5-minute-quick-start)  
**Yes, but not recently** → Start with [5-Minute Quick Start](#5-minute-quick-start)  
**Yes, I'm comfortable** → Jump to [Add IDE Features](#add-ide-features)

### 2. How much time do you have right now?

**30 minutes** → Run `:Tutor` and bookmark this guide  
**1 hour** → Complete [5-Minute Quick Start](#5-minute-quick-start)  
**1 day** → Do Day 1 of [First Week Plan](#first-week-plan)  
**1 week** → Follow complete [First Week Plan](#first-week-plan)

### 3. What's your learning style?

**Learn by doing** → Start with [5-Minute Quick Start](#5-minute-quick-start)  
**Learn by reading** → Read [QUICKSTART.md](QUICKSTART.md) first  
**Learn by watching** → Check [Video Resources](../resources/videos.md) first  
**Learn by example** → Try [Minimal Config](../examples/minimal/) immediately

### 4. What's your goal?

**Just want to edit files on servers** → [5-Minute Quick Start](#5-minute-quick-start) is enough  
**Want to be productive quickly** → Follow [First Week Plan](#first-week-plan)  
**Want to replace my IDE** → Complete Week 1, then [Add IDE Features](#add-ide-features)  
**Want to master Neovim** → Follow all modules (start with Week 1)

### Still not sure?

🗺️ **[Complete Path Guide →](WHICH_PATH.md)** has detailed decision trees for:
- Different backgrounds (VSCode, JetBrains, etc.)
- Different languages (Python, JavaScript, etc.)
- Different time commitments
- Different goals

---

## Common Questions

### How long until I'm productive?

**Realistic timeline:**
- 1 hour: Can survive in Neovim
- 1 day: Can edit (slowly)
- 3 days: Things start clicking
- 1 week: Functional for work
- 2 weeks: Comfortable and approaching old speed
- 1 month: Faster than before

### Will I be slower at first?

**Yes!** Days 1-3 are the hardest. You'll feel slower and frustrated. This is:
- ✅ Normal
- ✅ Temporary  
- ✅ Worth pushing through

By day 4-5, things start clicking. By week 2, you'll be back to your old speed or faster.

### Should I switch completely or gradually?

**Gradually!** 

Week 1: Use for one small task per day  
Week 2: Use for 50% of your work  
Week 3: Use as primary editor  
Week 4: Rarely use old editor

Keep your old editor available for high-pressure situations.

### Do I need to memorize everything?

**No!** You'll naturally memorize the commands you use frequently. Focus on:
- The 5 survival commands
- Basic navigation (hjkl, w, b)
- A few editing commands (d, c, y)

Everything else can be learned gradually.

### When should I customize?

**Not yet!** 

Use vanilla Neovim or our minimal config for at least Week 1. Learn the fundamentals before adding:
- Plugins
- Custom keybindings  
- Fancy colorschemes

Once you understand what you're doing, customization is easy.

### What if I get stuck?

**Multiple levels of help:**

**Level 1 - Emergency:** Scroll to [🆘 I'm Stuck!](../README.md#-im-stuck) section  
**Level 2 - Command help:** Type `:help <command>` in Neovim  
**Level 3 - Quick reference:** Check [QUICKSTART.md](QUICKSTART.md)  
**Level 4 - Community:** Ask in [Reddit/Discord](../resources/communities.md)  
**Level 5 - Issue:** Open an issue on this repo

---

## Quick Reference

### Essential Resources (Bookmark These!)

| Resource | When to Use |
|----------|-------------|
| [QUICKSTART.md](QUICKSTART.md) | First hour, need quick commands |
| [FIRST_WEEK_CHECKLIST.md](FIRST_WEEK_CHECKLIST.md) | Days 1-7, need daily structure |
| [WHICH_PATH.md](WHICH_PATH.md) | Not sure what to do next |
| [Module 1: Basics](../docs/01-basics/) | Week 1-2, learning fundamentals |
| [Example Configs](../examples/) | Week 2+, ready for plugins |

### The 5 Survival Commands (Always Keep Visible!)

```
┌─────────────────────────────────┐
│  i     Start typing             │
│  Esc   Stop typing              │
│  :wq   Save and quit            │
│  :q!   Quit without saving      │
│  u     Undo                     │
└─────────────────────────────────┘
```

### Your First Week at a Glance

```
Week 1: Learn the basics
├── Day 1: Survival + :Tutor
├── Day 2: Navigation (hjkl, w, b)
├── Day 3: Editing (d, c, y, p)
├── Day 4: Speed (counts, combinations)
├── Day 5: Text objects (ciw, di", ca()
├── Day 6: Real work practice
└── Day 7: Assessment

Result: Functional with Neovim! 🎉
```

---

## Ready to Start?

### Path 1: The Fast Track (Recommended for Most)

```bash
# 1. Open Neovim
nvim

# 2. Run the tutorial (type this inside Neovim)
:Tutor

# 3. After :Tutor, bookmark this guide and follow
#    the First Week Checklist day by day
```

### Path 2: The Cautious Approach

1. Read [QUICKSTART.md](QUICKSTART.md) (10 min)
2. Watch a [video tutorial](../resources/videos.md) (30 min)
3. Then follow Path 1

### Path 3: The Dive-In Approach

```bash
# Clone and try our config immediately
git clone https://github.com/ocrosby/learn-neovim.git
cd learn-neovim
nvim -u examples/minimal/init.lua

# Inside Neovim:
:Tutor
```

---

**Pick a path and start!** The hardest part is the first 30 minutes. After that, you're on your way. 🚀

**Questions?** Check [WHICH_PATH.md](WHICH_PATH.md) or open an issue.

**Stuck?** See the [🆘 I'm Stuck!](../README.md#-im-stuck) section.

**Ready for more?** After Week 1, continue to [Module 2: Intermediate](../docs/02-intermediate/).
