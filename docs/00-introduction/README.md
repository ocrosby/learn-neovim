# Module 0: Introduction to Neovim

Welcome to your Neovim learning journey! This module covers the fundamentals you need to understand before diving into Neovim itself.

## Learning Objectives

By the end of this module, you will:

- Understand what Neovim is and why it's worth learning
- Have Neovim installed and verified on your system
- Understand the basic Neovim philosophy and design
- Know where to find help and documentation

## Estimated Time

30-45 minutes

## Prerequisites

- Basic command line familiarity
- A willingness to learn a different editing paradigm
- No prior Vim/Neovim experience required

## Lessons

1. **[What is Neovim?](#what-is-neovim)** - Philosophy and design principles
2. **[Installation](installation.md)** - Installing Neovim on your platform
3. **[Setup and Verification](setup.md)** - Verifying your installation and first launch

## What is Neovim?

Neovim is a modern, extensible, and highly customizable text editor. It's a fork of Vim that aims to:

- **Modernize the codebase** while maintaining Vim compatibility
- **Enable better plugin architecture** with Lua scripting
- **Improve the user experience** with better defaults
- **Support modern development workflows** with built-in LSP, TreeSitter, and async operations

### Why Learn Neovim?

**Productivity**: Once mastered, modal editing is significantly faster than traditional editing.

**Customization**: Build exactly the editor you want, not what someone else decided.

**Universality**: Vim/Neovim is available on virtually every system. SSH into a server? Vim is there.

**Longevity**: Skills you learn today will be relevant for decades. Vim has been around since 1991.

**Modern Features**: Unlike Vim, Neovim has first-class support for LSP, TreeSitter, Lua configuration, and modern terminal features.

### The Modal Editing Paradigm

The core concept that makes Vim/Neovim different:

- **Normal Mode**: Navigate and manipulate text (default mode)
- **Insert Mode**: Type text like a traditional editor
- **Visual Mode**: Select text
- **Command Mode**: Execute commands

This separation allows you to keep your hands on the home row and compose powerful editing commands.

### Neovim vs Vim

| Feature | Vim | Neovim |
|---------|-----|--------|
| Configuration | Vimscript | Lua (and Vimscript) |
| Plugin API | Vimscript | Lua with better async |
| LSP | Via plugins | Built-in |
| TreeSitter | Not available | Built-in |
| Defaults | Minimal | More sensible |
| Development | Primarily one maintainer | Active community |

### Philosophy: Composability

Neovim commands are composable. Instead of memorizing hundreds of commands, you learn:

- **Operators**: What to do (delete, change, yank)
- **Motions**: Where to do it (word, paragraph, line)
- **Text Objects**: What to operate on (inside quotes, around brackets)

Example: `d` (delete) + `i` (inside) + `w` (word) = delete inside word

This composability is what makes Neovim powerful once you understand the grammar.

## Next Steps

1. [Install Neovim](installation.md)
2. [Verify your setup](setup.md)
3. Move on to [Module 1: Basics](../01-basics/README.md)

## Additional Resources

- [Official Neovim Website](https://neovim.io/)
- [Why Neovim?](https://neovim.io/charter/)
- [Neovim GitHub Repository](https://github.com/neovim/neovim)
- [Vim vs Neovim](https://github.com/neovim/neovim/wiki/FAQ#what-is-the-project-status)

## Getting Help

- `:help` - Built-in help system (you'll use this a lot!)
- `:Tutor` - Built-in interactive tutorial
- [Neovim Discourse](https://neovim.discourse.group/)
- [r/neovim](https://www.reddit.com/r/neovim/)
