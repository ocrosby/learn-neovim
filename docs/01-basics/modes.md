# Lesson 1: Modes

The most fundamental concept in Neovim is modal editing. Unlike traditional editors where every key types a character, Neovim has different modes where keys perform different actions.

## The Four Primary Modes

### 1. Normal Mode (Default)

**Purpose**: Navigate and manipulate text

**How to enter**: Press `Esc` from any mode

**What you can do**:
- Navigate the file
- Delete, copy, paste text
- Execute commands
- Enter other modes

**Visual indicator**: No mode indicator shown

Normal mode is your home base. You should spend most of your time here, not in Insert mode.

**Key philosophy**: Treat Normal mode like your default. When you finish typing, immediately press `Esc` to return to Normal mode.

### 2. Insert Mode

**Purpose**: Type text like a traditional editor

**How to enter**:
- `i` - Insert before cursor
- `a` - Append after cursor
- `I` - Insert at start of line
- `A` - Append at end of line
- `o` - Open new line below
- `O` - Open new line above

**How to exit**: Press `Esc`

**Visual indicator**: `-- INSERT --` at the bottom

**Best practice**: Enter Insert mode, type your text, immediately exit with `Esc`. Don't navigate in Insert mode.

### 3. Visual Mode

**Purpose**: Select text for operations

**How to enter**:
- `v` - Character-wise visual mode
- `V` - Line-wise visual mode
- `Ctrl-v` - Block-wise visual mode

**How to exit**: Press `Esc`

**Visual indicator**: `-- VISUAL --`, `-- VISUAL LINE --`, or `-- VISUAL BLOCK --`

**What you can do**:
- Select text by moving the cursor
- Delete, copy, or change the selection
- Perform operations on the selection

### 4. Command Mode

**Purpose**: Execute commands

**How to enter**: Press `:` from Normal mode

**How to exit**: Press `Esc` or `Enter` (after command)

**Visual indicator**: `:` prompt at the bottom

**Common commands**:
- `:w` - Write (save)
- `:q` - Quit
- `:wq` - Write and quit
- `:help` - Open help
- `:%s/old/new/g` - Search and replace

## Mode Transitions

```
        i,a,o,I,A,O
  ┌──────────────────────┐
  │                      │
  ▼                      │
Normal ──────────────> Insert
  │           Esc        │
  │                      │
  │ v,V,Ctrl-v          │ Esc
  │                      │
  ▼                      │
Visual ◄────────────────┘
  │
  │ :
  ▼
Command
```

## Practical Examples

### Example 1: Insert Text

```
Goal: Add "Hello" at the current cursor position

1. (In Normal mode) Press i to enter Insert mode
2. Type "Hello"
3. Press Esc to return to Normal mode
```

### Example 2: Delete a Line

```
Goal: Delete the current line

1. (In Normal mode) Press dd
2. Line is deleted
3. Still in Normal mode
```

### Example 3: Select and Delete

```
Goal: Select 3 lines and delete them

1. (In Normal mode) Press V to enter Visual Line mode
2. Press 2j to extend selection down 2 lines (total 3 lines)
3. Press d to delete
4. Back in Normal mode
```

## Common Mistakes

### Mistake 1: Staying in Insert Mode

**Wrong**: Enter Insert mode and try to navigate with arrow keys
**Right**: Use Normal mode for navigation, Insert mode only for typing

### Mistake 2: Not Knowing Which Mode You're In

**Solution**: Always check the mode indicator at the bottom. If unsure, press `Esc` to return to Normal mode.

### Mistake 3: Trying to Type in Normal Mode

**Symptom**: Random characters disappear or strange things happen
**Solution**: Press `i` to enter Insert mode before typing

### Mistake 4: Pressing `i` Multiple Times

**Symptom**: The letter "i" appears in your text
**Cause**: You're already in Insert mode
**Solution**: Press `Esc` first, then `i`

## Special Modes (Preview)

There are a few other modes you'll encounter later:

- **Replace Mode** - `R` - Overwrite text
- **Terminal Mode** - `:terminal` - Interact with shell
- **Select Mode** - Rarely used, similar to Visual

We'll cover these in advanced modules.

## Exercises

### Exercise 1: Mode Recognition

Open a file and practice identifying which mode you're in:

1. Start in Normal mode (press `Esc`)
2. Press `i` - You're in Insert mode (check indicator)
3. Press `Esc` - Back to Normal mode
4. Press `v` - In Visual mode
5. Press `Esc` - Back to Normal mode
6. Press `:` - In Command mode
7. Press `Esc` - Back to Normal mode

Repeat until you can identify modes instantly.

### Exercise 2: Mode Switching Drills

Practice these sequences 10 times each:

**Drill 1**: Normal → Insert → Normal
```
Esc → i → (type something) → Esc
```

**Drill 2**: Normal → Visual → Normal
```
Esc → v → (move cursor) → Esc
```

**Drill 3**: Normal → Command → Normal
```
Esc → : → (type command) → Esc
```

### Exercise 3: Practical Application

Open the file [exercises/01-modes.txt](exercises/01-modes.txt):

1. Navigate to line 5 (in Normal mode: `5G`)
2. Enter Insert mode with `i`
3. Type "Hello, Neovim!"
4. Exit to Normal mode with `Esc`
5. Visual select the line you just typed with `V`
6. Delete it with `d`

## Inserting Text: The Complete List

| Command | Action |
|---------|--------|
| `i` | Insert before cursor |
| `a` | Append after cursor |
| `I` | Insert at beginning of line |
| `A` | Append at end of line |
| `o` | Open new line below and insert |
| `O` | Open new line above and insert |
| `s` | Substitute character (delete char and insert) |
| `S` | Substitute line (delete line and insert) |
| `C` | Change to end of line |

Start with `i`, `a`, and `o`. Learn the others when comfortable.

## Tips for Building Muscle Memory

1. **Disable arrow keys** in Insert mode (forces you to use Normal mode for navigation)
2. **Press `Esc` immediately** after typing
3. **Use `jk` or `jj`** as an alternative to `Esc` (can remap in configuration)
4. **Practice mode switching** without thinking about it
5. **Use Visual mode sparingly** - Often operators + motions are faster

## Quick Reference Card

```
Normal Mode (default)
  ├─ i,a,I,A,o,O ──> Insert Mode (-- INSERT --)
  ├─ v,V,Ctrl-v ──> Visual Mode (-- VISUAL --)
  └─ : ──────────> Command Mode (:)

All modes: Press Esc to return to Normal Mode
```

## Assessment

You understand modes when you can:

- ✅ Switch between modes without looking at the indicator
- ✅ Press `Esc` reflexively after typing
- ✅ Know what mode you're in at all times
- ✅ Use `i`, `a`, `o` to enter Insert mode appropriately
- ✅ Use `v` or `V` to visually select text

## Next Lesson

Once you're comfortable with modes, proceed to [Lesson 2: Navigation](navigation.md) to learn efficient movement.

## Additional Resources

- `:help vim-modes` - Official modes documentation
- `:help mode-switching` - Mode transition details
- `:help Insert` - Insert mode specifics
- `:help Visual-mode` - Visual mode details
