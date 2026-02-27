# Module 3: Configuration

Now that you understand Neovim fundamentals, it's time to customize it to your workflow. This module teaches you how to configure Neovim using Lua.

## Learning Objectives

By the end of this module, you will:

- Understand the structure of `init.lua`
- Configure essential Neovim options
- Create custom keymappings
- Organize your configuration into modules
- Understand the difference between Lua and Vimscript configuration

## Estimated Time

2-3 hours

## Prerequisites

- Completed [Module 1: Basics](../01-basics/README.md)
- Completed [Module 2: Intermediate](../02-intermediate/README.md)
- Comfortable using vanilla Neovim
- Basic programming understanding (any language)

## Lessons

1. **[Understanding init.lua](init-lua.md)** - Configuration structure
2. **[Options](options.md)** - Essential Neovim settings
3. **[Keymaps](keymaps.md)** - Custom keyboard mappings

## Why Configure Neovim?

**Better defaults**: Neovim's defaults are good, but you can make them better for your workflow.

**Ergonomics**: Remap keys to positions that make sense for you.

**Workflow**: Configure Neovim to match how you work, not how someone else works.

**Understanding**: Building your own config means you understand every setting.

## Configuration Philosophy

**Start minimal**: Add options only when you understand what they do.

**Build incrementally**: Don't copy someone else's 1000-line config.

**Understand everything**: If you don't know what a setting does, look it up with `:help`.

**Use Lua**: Modern Neovim configuration uses Lua, not Vimscript.

## Configuration Location

**Linux/macOS**:
```
~/.config/nvim/
├── init.lua           # Main entry point
└── lua/
    └── config/
        ├── options.lua
        ├── keymaps.lua
        └── autocmds.lua
```

**Windows**:
```
%LOCALAPPDATA%\nvim\
├── init.lua
└── lua\
    └── config\
        ├── options.lua
        ├── keymaps.lua
        └── autocmds.lua
```

## Module Structure

This module focuses on **configuration without plugins**. Plugin management comes in [Module 4](../04-plugin-management/README.md).

## Examples

The [examples](examples/) directory contains:

- **minimal/** - Absolute minimal config
- **basic/** - Basic usable config with no plugins
- **commented/** - Heavily commented educational config

## Quick Reference

### Essential Options

```lua
vim.opt.number = true
vim.opt.relativenumber = true
vim.opt.expandtab = true
vim.opt.shiftwidth = 4
vim.opt.tabstop = 4
vim.opt.ignorecase = true
vim.opt.smartcase = true
```

### Creating Keymaps

```lua
vim.keymap.set('n', '<leader>w', ':w<CR>')
vim.keymap.set('n', '<C-h>', '<C-w>h')
vim.keymap.set('i', 'jk', '<Esc>')
```

## Assessment

You're ready for Module 4 when you can:

- ✅ Create and structure an `init.lua` file
- ✅ Set Neovim options in Lua
- ✅ Create custom keymaps
- ✅ Organize configuration into separate modules
- ✅ Use `:help` to look up options
- ✅ Understand the difference between Lua and Vimscript

## Exercises

- [Exercise 1: Create Your First init.lua](examples/minimal/README.md)
- [Exercise 2: Configure Options](examples/basic/README.md)
- [Exercise 3: Custom Keymaps](examples/basic/README.md)

## Common Mistakes

1. **Copying configs blindly** - Understand what you add
2. **Too many settings at once** - Add incrementally
3. **Not reading `:help`** - Every option is documented
4. **Using Vimscript instead of Lua** - Lua is the modern way
5. **Over-configuring** - Keep it simple at first

## Next Steps

After completing this module:

1. Use your minimal config for a few days
2. Add settings as you discover you need them
3. Proceed to [Module 4: Plugin Management](../04-plugin-management/README.md)

## Additional Resources

- `:help lua-guide` - Official Lua guide
- `:help options` - All available options
- `:help key-mapping` - Keymap documentation
- [Neovim Lua Guide](https://neovim.io/doc/user/lua-guide.html)
- [Learn X in Y Minutes: Lua](https://learnxinyminutes.com/docs/lua/)

---

**Ready to build your config?** Start with [Lesson 1: Understanding init.lua](init-lua.md)
