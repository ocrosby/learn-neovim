# Module 1: Neovim Basics

Welcome to the core of Neovim! This module teaches you the fundamental concepts of modal editing, navigation, and basic editing operations.

## Learning Objectives

By the end of this module, you will:

- Understand and use Neovim's different modes
- Navigate efficiently without arrow keys
- Perform basic editing operations
- Understand the modal editing grammar
- Build muscle memory for common commands

## Estimated Time

2-3 hours (with practice exercises)

## Prerequisites

- Completed [Module 0: Introduction](../00-introduction/README.md)
- Neovim installed and verified
- Completed `:Tutor` (highly recommended)

## Lessons

1. **[Modes](modes.md)** - Normal, Insert, Visual, and Command modes
2. **[Navigation](navigation.md)** - Moving around efficiently
3. **[Basic Editing](editing.md)** - Core editing operations

## The Modal Editing Grammar

Neovim's power comes from its composable command structure:

```
[count] [operator] [motion/text-object]
```

**Examples**:
- `d2w` - Delete 2 words
- `c3j` - Change 3 lines down
- `y$` - Yank (copy) to end of line

You'll learn each component in this module.

## Practice Philosophy

**Disable arrow keys** (temporarily) to build proper muscle memory. Add this to a scratch file and practice:

```
Arrow keys have been disabled to help you learn the hjkl navigation.
Use h (left), j (down), k (up), l (right) instead.
```

**Practice with real files**. Edit actual code or text, not just practice files. Discomfort is part of learning.

**Focus on accuracy over speed**. Speed comes naturally with practice.

## Exercises

Each lesson has accompanying exercises in the [exercises](exercises/) directory:

- [Exercise 1: Mode Switching](exercises/01-modes.txt)
- [Exercise 2: Navigation](exercises/02-navigation.txt)
- [Exercise 3: Basic Editing](exercises/03-editing.txt)

## Quick Reference

### Essential Commands

| Command | Action |
|---------|--------|
| `i` | Insert before cursor |
| `a` | Append after cursor |
| `o` | Open new line below |
| `Esc` | Return to Normal mode |
| `h,j,k,l` | Left, Down, Up, Right |
| `w` | Next word |
| `b` | Previous word |
| `d` | Delete operator |
| `y` | Yank (copy) operator |
| `p` | Paste |
| `u` | Undo |
| `Ctrl-r` | Redo |

### Mode Indicators

| Mode | Indicator | Purpose |
|------|-----------|---------|
| Normal | (none) | Navigate and command |
| Insert | `-- INSERT --` | Type text |
| Visual | `-- VISUAL --` | Select text |
| Command | `:` prompt | Execute commands |

## Common Beginner Mistakes

1. **Staying in Insert mode** - Normal mode is your default
2. **Using arrow keys** - hjkl is more efficient
3. **Repeating commands manually** - Use counts: `3j` not `jjj`
4. **Not using undo** - `u` is your friend, experiment freely
5. **Forgetting which mode you're in** - Watch the mode indicator

## Tips for Success

- **Practice daily** - Even 15 minutes builds muscle memory
- **Use `:help`** - If you forget a command, `:help motion` or `:help operator`
- **Don't memorize** - Understand the patterns, the rest follows
- **Be patient** - You'll feel slower at first, this is normal
- **Use vanilla Neovim** - No plugins yet, learn the foundation

## Lesson Progression

Follow the lessons in order:

1. **[Start with Modes](modes.md)** - Understand Normal, Insert, Visual, Command
2. **[Then Navigation](navigation.md)** - Move efficiently without arrow keys
3. **[Finally Basic Editing](editing.md)** - Combine operators and motions

Each lesson builds on the previous one.

## Assessment

You're ready for Module 2 when you can:

- Switch between modes without thinking
- Navigate a file using hjkl, w/b, f/t without arrow keys
- Use operators with motions (dw, caw, yap)
- Undo/redo comfortably
- Use counts with commands (3j, 2dw)

## Next Steps

After completing this module:

1. Practice for at least a few days with real work
2. Complete all exercises
3. Move to [Module 2: Intermediate](../02-intermediate/README.md)

## Additional Resources

- [`:help motion.txt`](https://neovim.io/doc/user/motion.html) - All movement commands
- [`:help operator.txt`](https://neovim.io/doc/user/motion.html#operator) - All operators
- [`:help insert.txt`](https://neovim.io/doc/user/insert.html) - Insert mode details
- [Vim Golf](https://www.vimgolf.com/) - Practice efficiency (when ready)
- [Vim Adventures](https://vim-adventures.com/) - Gamified learning

## Getting Help

If you're stuck on a concept:

1. Use `:help <topic>` (e.g., `:help w`)
2. Review the `:Tutor` sections
3. Practice the specific exercise for that topic
4. Ask in [r/neovim](https://www.reddit.com/r/neovim/) or [Neovim Discourse](https://neovim.discourse.group/)

---

**Ready to master modal editing?** Start with [Lesson 1: Modes](modes.md)
