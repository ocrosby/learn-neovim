# Neovim Basics Cheat Sheet

Quick reference for essential Neovim commands. Print this or keep it handy while learning.

## Modes

| Key | Mode |
|-----|------|
| `Esc` | Normal mode (from any mode) |
| `i` | Insert mode (before cursor) |
| `a` | Insert mode (after cursor) |
| `v` | Visual mode (character) |
| `V` | Visual mode (line) |
| `Ctrl-v` | Visual mode (block) |
| `:` | Command mode |

## Navigation

### Basic Movement
| Key | Action |
|-----|--------|
| `h` | Left |
| `j` | Down |
| `k` | Up |
| `l` | Right |

### Word Movement
| Key | Action |
|-----|--------|
| `w` | Next word start |
| `e` | Next word end |
| `b` | Previous word start |
| `W` | Next WORD (whitespace) |

### Line Movement
| Key | Action |
|-----|--------|
| `0` | Line start |
| `^` | First non-blank |
| `$` | Line end |
| `g_` | Last non-blank |

### File Movement
| Key | Action |
|-----|--------|
| `gg` | First line |
| `G` | Last line |
| `{n}G` | Go to line n |
| `%` | Matching bracket |

### Search
| Key | Action |
|-----|--------|
| `/pattern` | Search forward |
| `?pattern` | Search backward |
| `n` | Next match |
| `N` | Previous match |
| `*` | Search word under cursor |

### Find on Line
| Key | Action |
|-----|--------|
| `f{char}` | Find next char |
| `F{char}` | Find previous char |
| `t{char}` | Till next char |
| `T{char}` | Till previous char |
| `;` | Repeat find |
| `,` | Repeat find reverse |

## Editing

### Operators
| Key | Action |
|-----|--------|
| `d` | Delete |
| `c` | Change (delete + insert) |
| `y` | Yank (copy) |
| `p` | Paste after |
| `P` | Paste before |

### Common Combinations
| Key | Action |
|-----|--------|
| `dd` | Delete line |
| `cc` | Change line |
| `yy` | Yank line |
| `dw` | Delete word |
| `cw` | Change word |
| `d$` | Delete to end of line |
| `c$` | Change to end of line |

### Text Objects
| Key | Action |
|-----|--------|
| `iw` | Inner word |
| `aw` | A word (with space) |
| `i"` | Inside quotes |
| `a"` | Around quotes |
| `i(` | Inside parentheses |
| `a(` | Around parentheses |
| `i{` | Inside braces |
| `a{` | Around braces |

### Quick Edits
| Key | Action |
|-----|--------|
| `x` | Delete character |
| `r{char}` | Replace character |
| `~` | Toggle case |
| `u` | Undo |
| `Ctrl-r` | Redo |
| `.` | Repeat last change |
| `J` | Join lines |

## Counts

Most commands accept counts:

| Example | Action |
|---------|--------|
| `3w` | Move 3 words |
| `5j` | Move 5 lines down |
| `2dd` | Delete 2 lines |
| `3cw` | Change 3 words |

## Visual Mode

| Key | Action |
|-----|--------|
| `v` | Character-wise |
| `V` | Line-wise |
| `Ctrl-v` | Block-wise |
| (move) | Extend selection |
| `d` | Delete selection |
| `c` | Change selection |
| `y` | Yank selection |
| `>` | Indent right |
| `<` | Indent left |

## File Operations

| Command | Action |
|---------|--------|
| `:w` | Write (save) |
| `:q` | Quit |
| `:wq` | Write and quit |
| `:q!` | Quit without saving |
| `:e file` | Edit file |
| `:saveas file` | Save as |

## Windows

| Command | Action |
|---------|--------|
| `:split` | Horizontal split |
| `:vsplit` | Vertical split |
| `Ctrl-w h/j/k/l` | Navigate windows |
| `Ctrl-w q` | Close window |
| `Ctrl-w o` | Close other windows |

## Help

| Command | Action |
|---------|--------|
| `:help` | Open help |
| `:help {topic}` | Help on topic |
| `:Tutor` | Interactive tutorial |
| `Ctrl-]` | Follow help link |
| `Ctrl-o` | Go back |

## Tips

1. **Stay in Normal mode** - Return to Normal mode after editing
2. **Think in operators + motions** - `d3w` not `dwdwdw`
3. **Use text objects** - `ciw` not manual selection
4. **Use the dot command** - Repeat last change with `.`
5. **Search, don't scroll** - Use `/` to find, not manual navigation

---

**Remember**: This is a reference, not a memorization list. Learn patterns, not individual commands.
