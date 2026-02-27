# Setup and Verification

Now that Neovim is installed, let's launch it and verify everything is working correctly.

## First Launch

Open your terminal and type:

```bash
nvim
```

You should see the Neovim welcome screen with version information and helpful tips.

**Important**: Don't panic if the editor feels strange! Neovim is modal, which means you're in "Normal mode" by default—not "Insert mode" where you can type text.

## Your First Commands

Let's verify Neovim is working with a few simple commands:

### Entering Command Mode

Press `:` (colon) to enter Command mode. You'll see a `:` appear at the bottom of the screen.

### Checking the Version

Type:
```
:version
```

Then press `Enter`. You'll see detailed version information.

### Accessing Built-in Help

Type:
```
:help
```

Then press `Enter`. This opens Neovim's extensive built-in documentation.

Press `:q` and `Enter` to close the help window.

### Running the Built-in Tutorial

Type:
```
:Tutor
```

Then press `Enter`. This launches an interactive 30-minute tutorial. Highly recommended for beginners!

Press `:q` and `Enter` to exit when you're done.

### Quitting Neovim

To quit Neovim:
1. Press `:` to enter Command mode
2. Type `q` (for quit)
3. Press `Enter`

Or use the shortcut: `:q` followed by `Enter`.

If you've made changes and want to quit without saving:
```
:q!
```

## Creating a Test File

Let's create and edit a simple file to verify everything works:

1. **Launch Neovim with a filename**:
   ```bash
   nvim test.txt
   ```

2. **Enter Insert mode** by pressing `i`
   - You should see `-- INSERT --` at the bottom

3. **Type some text**:
   ```
   Hello, Neovim!
   This is my first file.
   ```

4. **Exit Insert mode** by pressing `Esc`
   - The `-- INSERT --` indicator disappears

5. **Save the file** by typing:
   ```
   :w
   ```
   (stands for "write")

6. **Quit** by typing:
   ```
   :q
   ```

7. **Verify the file was created**:
   ```bash
   cat test.txt
   ```

Congratulations! You've just created your first file in Neovim.

## Understanding the Interface

### Status Line

At the bottom of Neovim, you'll see a status line showing:
- Current mode (INSERT, NORMAL, VISUAL, etc.)
- File name
- Cursor position
- File type

### Command Line

The very bottom line where you type commands (after pressing `:`)

### Buffer Area

The main editing area where your text appears

## Health Check

Neovim includes a health check system to verify everything is configured correctly.

Run:
```
:checkhealth
```

This will show:
- What's working correctly (✓)
- What's missing or misconfigured (✗)
- Suggestions for fixing issues (!)

Don't worry if some things are missing—we'll address plugin-related items in later modules.

## Common Issues

### "Cannot open file for writing"

You don't have write permissions. Either:
- Edit the file with appropriate permissions
- Use `:w !sudo tee %` to write with elevated permissions (Linux/macOS)

### Accidentally pressed Ctrl+S and Neovim froze

This is a terminal flow control issue. Press `Ctrl+Q` to unfreeze.

### Can't exit Neovim

The classic problem! Use:
- `:q` - Quit (fails if unsaved changes)
- `:q!` - Quit without saving
- `:wq` - Write and quit
- `ZZ` - Write and quit (Normal mode shortcut)

### Terminal colors look wrong

Your terminal may not support true color. Add to your shell config:
```bash
export TERM=xterm-256color
```

Or use a modern terminal emulator (iTerm2, Alacritty, WezTerm, Windows Terminal).

## Quick Reference Card

Print this or keep it handy:

| Command | Action |
|---------|--------|
| `i` | Enter Insert mode |
| `Esc` | Return to Normal mode |
| `:w` | Write (save) file |
| `:q` | Quit |
| `:wq` | Write and quit |
| `:q!` | Quit without saving |
| `:help` | Open help |
| `:Tutor` | Start tutorial |

## Configuration Files (Preview)

Right now, you're running Neovim with default settings. Later in [Module 3: Configuration](../03-configuration/README.md), you'll create:

- `~/.config/nvim/init.lua` - Main configuration file
- `~/.config/nvim/lua/` - Additional Lua modules

But for now, focus on learning the basics without any configuration.

## Recommended Next Steps

1. **Run `:Tutor`** - Spend 30 minutes on the built-in tutorial
2. **Practice basic navigation** - Even just moving around in `:help` pages
3. **Don't configure yet** - Learn vanilla Neovim first
4. **Move to [Module 1: Basics](../01-basics/README.md)** when comfortable

## Important Philosophy

**Learn vanilla Neovim first.** Many beginners immediately install a pre-configured distribution (LazyVim, NvChad, AstroNvim) without understanding Neovim itself. This makes troubleshooting difficult and prevents you from building the configuration you actually want.

Resist the urge to install plugins until you understand:
- Modal editing
- Basic navigation
- Text objects and operators
- What problems plugins actually solve

## Additional Resources

- [`:help user-manual`](https://neovim.io/doc/user/) - Official user manual
- [`:help quickref`](https://neovim.io/doc/user/quickref.html) - Quick reference
- [Neovim Documentation](https://neovim.io/doc/)
- [Vim Cheat Sheet](https://vim.rtorr.com/) - Applicable to Neovim

## Module Complete!

You've successfully:
- ✅ Installed Neovim
- ✅ Launched Neovim
- ✅ Executed basic commands
- ✅ Created and saved a file
- ✅ Verified your installation

**Ready to learn modal editing?** Proceed to [Module 1: Basics](../01-basics/README.md)
