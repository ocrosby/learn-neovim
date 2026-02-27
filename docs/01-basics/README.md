# Module 1: Your First Steps in Neovim

This is where the fun begins! You'll learn the core skills that make Neovim powerful.

## What You'll Learn

- How to switch between modes
- Navigate without arrow keys (faster than you think!)
- Edit text efficiently
- Think in Neovim's "language"

**Time needed:** Practice these concepts over a few days. No rush!

## Before Starting

- ✅ Have Neovim installed ([Module 0](../00-introduction/README.md))
- ✅ Complete `:Tutor` (type it inside Neovim and press Enter)
- ✅ Know the survival commands: `i`, `Esc`, `:wq`, `:q!`, `u`

**Not done `:Tutor` yet?** Go do it now! It's the single best 30 minutes you can spend. Everything else builds on it.

**New to Neovim?** Start with the [First Day Guide](../QUICKSTART.md) instead!

**Important:** You'll feel slower at first. This is completely normal! Everyone goes through this phase.

## Three Simple Lessons

1. **[Modes](modes.md)** - Understanding Normal, Insert, Visual, and Command modes
2. **[Navigation](navigation.md)** - Moving around without arrow keys
3. **[Editing](editing.md)** - Your first editing commands

**Work through these in order.** Each lesson builds on the previous one.

## The Big Idea

Neovim commands work like a language:

```
[action] [count] [target]
```

Examples:
- `d2w` - **Delete 2 words**
- `c3j` - **Change 3 lines down**
- `y$` - **Yank (copy) to end of line**

Don't memorize these yet! Just understand the pattern.

## Tips for Learning

**Go slow** - Accuracy first, speed comes later.

**Practice daily** - Even 15 minutes helps build muscle memory.

**Use real work** - Practice on actual files, not just exercises.

**Be patient** - Feeling awkward is part of the process.

**Resist arrow keys** - Try using `h j k l` instead. It feels weird for a day, then clicks!

## Practice Exercises

Each lesson has exercises you can try:

- [Exercise 1: Mode Switching](exercises/01-modes.txt)
- [Exercise 2: Navigation](exercises/02-navigation.txt)
- [Exercise 3: Basic Editing](exercises/03-editing.txt)

## Quick Commands Reference

| Key | What It Does |
|-----|--------------|
| `i` | Start typing (Insert mode) |
| `Esc` | Stop typing (back to Normal mode) |
| `h j k l` | Move left, down, up, right |
| `w` | Jump to next word |
| `u` | Undo |
| `:q!` | Quit without saving |
| `:wq` | Save and quit |

**Stuck?** Type `:help` and press Enter inside Neovim for built-in help.

## Common Beginner Struggles

**"I can't type!"** - You're in Normal mode. Press `i` to enter Insert mode.

**"I keep getting random characters"** - You're in Insert mode. Press `Esc` to get to Normal mode.

**"hjkl feels weird"** - It does for a day or two, then it clicks. Stay with it!

**"I'm slower than before"** - Completely normal! Give it a few days.

## When Are You Ready for Module 2?

You can:
- Switch between modes without thinking
- Move around using `hjkl` and `w/b`
- Delete and edit text with basic commands
- Undo mistakes with `u`

Don't wait for perfection—move on when you're comfortable with the basics!

## Next Module

**→ [Module 2: Intermediate Skills](../02-intermediate/README.md)**

Take a few days to practice first!

<details>
<summary>📚 More resources</summary>

- [Vim Golf](https://www.vimgolf.com/) - Practice challenges
- [Vim Adventures](https://vim-adventures.com/) - Game-based learning
- Type `:help motion` inside Neovim for detailed docs

</details>

---

**Ready to start?** → [Lesson 1: Understanding Modes](modes.md)
