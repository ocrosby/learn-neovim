# Neovim Quickstart - Your First Day

**Goal:** Get functional with Neovim in one hour.

## The 5 Commands You Must Know

```
i           Start typing (INSERT mode)
Esc         Stop typing (NORMAL mode)
:wq         Save and quit
:q!         Quit without saving
u           Undo
```

**Practice right now:** Open Neovim, press `i`, type something, press `Esc`, type `:q!` and press Enter.

## Understanding Modes

Neovim has different "modes" - think of them like gears in a car:

### INSERT Mode - For Typing
- Press `i` to enter
- Type like a normal editor
- Press `Esc` to exit back to NORMAL mode

**When to use:** When you need to type text

### NORMAL Mode - For Everything Else
- This is your default mode
- Navigate, delete, copy, paste
- Press `Esc` to get here from any mode

**When to use:** When you're NOT typing

### VISUAL Mode - For Selecting
- Press `v` to enter
- Move cursor to select text
- Press `d` to delete, `y` to copy

**When to use:** When you need to select text

## Your First Hour

### Step 1: Run the Tutorial (30 min)

```bash
nvim
# Inside Neovim, type:
:Tutor
```

Follow along with the interactive tutorial. Don't skip this!

### Step 2: Practice in a Scratch File (15 min)

```bash
nvim practice.txt
```

Try these exercises:
1. Press `i`, type "Hello World", press `Esc`
2. Press `i` again, type a few more lines, press `Esc`
3. Try undo: press `u` a few times
4. Save and quit: type `:wq` and press Enter

### Step 3: Learn Basic Navigation (15 min)

Open Neovim again and practice:

```
h j k l     Left, Down, Up, Right (instead of arrow keys)
w           Jump forward one word
b           Jump back one word
0           Go to start of line
$           Go to end of line
gg          Go to top of file
G           Go to bottom of file
```

**Exercise:** Open a real file and navigate using only these keys. No arrow keys!

## Day 1 Cheatsheet - Print This!

### Getting In and Out
```
nvim file.txt       Open file
:w                  Save
:q                  Quit
:wq                 Save and quit
:q!                 Quit without saving (emergency!)
:e filename         Open another file
```

### Modes
```
i                   INSERT before cursor
a                   INSERT after cursor
o                   INSERT on new line below
Esc                 Back to NORMAL mode (from any mode)
v                   VISUAL mode (select)
```

### Basic Movement (NORMAL mode)
```
h j k l             Left, Down, Up, Right
w                   Next word
b                   Previous word
0                   Start of line
$                   End of line
gg                  Top of file
G                   Bottom of file
```

### Basic Editing (NORMAL mode)
```
x                   Delete character
dd                  Delete line
u                   Undo
Ctrl-r              Redo
p                   Paste
yy                  Copy line
```

### Search
```
/text               Search for "text"
n                   Next match
N                   Previous match
```

## Common Problems & Solutions

### "I can't type anything!"
**Solution:** Press `i` to enter INSERT mode

### "Random characters appear when I try to move!"
**Solution:** Press `Esc` to get to NORMAL mode first

### "How do I quit?"
**Solution:** Press `Esc`, then type `:q!` and press Enter

### "I accidentally deleted something!"
**Solution:** Press `Esc`, then press `u` to undo

### "The screen froze!"
**Solution:** You pressed `Ctrl-s`. Press `Ctrl-q` to unfreeze

### "Everything is acting weird!"
**Solution:** Press `Esc` several times to get back to NORMAL mode

## Your First Week Strategy

### Day 1: Survival Mode
- Complete `:Tutor`
- Practice in a scratch file
- Goal: Understand modes and basic navigation

### Days 2-3: Real Work (Small Tasks)
- Use Neovim for ONE small editing task
- Keep your old editor open for "real" work
- Goal: Build muscle memory

### Days 4-7: Increasing Use
- Use Neovim for multiple tasks
- Start to feel less awkward
- Goal: Stop thinking about the keys

### Week 2: Commit
- Use Neovim as primary editor
- Learn more commands as needed
- Goal: Match your old speed

## Next Steps

Once you're comfortable (after 3-7 days):

1. **[Module 1: Basics](../01-basics/)** - Deep dive into fundamentals
2. **[Module 2: Intermediate](../02-intermediate/)** - Text objects and power commands
3. **[Module 3: Configuration](../03-configuration/)** - Customize your setup

## The Most Important Tip

**You will be slower for 2-3 days.** This is normal. This is temporary. This is worth it.

By day 4-5, things start clicking. By week 2, you'll wonder why you waited so long.

**Stick with it!**

## Visual Learning Guide

### The Mode Flow

```
           ┌─────────────┐
           │   NORMAL    │ ← You start here
           │   (default) │
           └─────────────┘
                 │
      ┌──────────┼──────────┐
      │          │          │
      ↓          ↓          ↓
  ┌───────┐  ┌────────┐  ┌────────┐
  │INSERT │  │ VISUAL │  │COMMAND │
  │ type  │  │ select │  │ :wq    │
  └───────┘  └────────┘  └────────┘
      │          │          │
      └──────────┼──────────┘
                 ↓
        Press Esc to return
```

### How to Think About Modes

**NORMAL mode** = "Command mode" - You're telling Neovim what to do  
**INSERT mode** = "Typing mode" - You're adding text  
**VISUAL mode** = "Selection mode" - You're highlighting text  
**COMMAND mode** = "Action mode" - You're executing commands

### Common Editing Patterns

**Pattern: Change a word**
```
1. Make sure you're in NORMAL mode (press Esc)
2. Move cursor to the word
3. Press: ciw
4. Type the new word
5. Press Esc
```

**Pattern: Delete a line**
```
1. In NORMAL mode
2. Move cursor to the line
3. Press: dd
```

**Pattern: Copy and paste a line**
```
1. In NORMAL mode
2. Move cursor to the line
3. Press: yy (to copy)
4. Move to where you want to paste
5. Press: p (to paste)
```

## Quick Reference Card (Keep This Visible)

```
┌─────────────────────────────────────────┐
│  NEOVIM SURVIVAL CARD                   │
├─────────────────────────────────────────┤
│  Modes:                                 │
│    i     → Start typing                 │
│    Esc   → Stop typing                  │
│                                         │
│  Save/Quit:                             │
│    :w    → Save                         │
│    :q    → Quit                         │
│    :wq   → Save and quit                │
│    :q!   → Quit without saving          │
│                                         │
│  Movement:                              │
│    h j k l → Left Down Up Right         │
│    w       → Next word                  │
│    b       → Previous word              │
│                                         │
│  Undo:                                  │
│    u       → Undo                       │
│                                         │
│  Emergency:                             │
│    Press Esc, then type :q!             │
└─────────────────────────────────────────┘
```

Print this and keep it next to your monitor for the first week!

---

## What to Read Next

**After your first hour:**
- 📋 [First Week Checklist](FIRST_WEEK_CHECKLIST.md) - Day-by-day plan for Week 1
- 🗺️ [Which Path Should I Follow?](WHICH_PATH.md) - Find the right learning path

**When you're ready for more:**
- 📖 [Module 1: Basics](../01-basics/) - Deep dive into fundamentals
- 💻 [Example Configs](../../examples/) - Try pre-built configurations
- 📚 [Full Course](../00-introduction/) - Complete learning path

**Need help?**
- `:help` inside Neovim
- [Communities](../../resources/communities.md)
- [Open an issue](https://github.com/ocrosby/learn-neovim/issues)
