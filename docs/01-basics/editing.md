# Lesson 3: Basic Editing

Now that you understand modes and navigation, let's combine them to edit text efficiently. This is where Neovim's power becomes apparent.

## The Editing Grammar

Neovim commands follow a composable grammar:

```
[count] [operator] [motion/text-object]
```

**Components**:
- **Count**: How many times (optional)
- **Operator**: What to do (delete, change, yank)
- **Motion/Text Object**: Where to do it

**Examples**:
- `d2w` - Delete 2 words
- `c$` - Change to end of line
- `y3j` - Yank 3 lines down

## Core Operators

| Operator | Action | Leaves you in |
|----------|--------|---------------|
| `d` | Delete | Normal mode |
| `c` | Change (delete + insert) | Insert mode |
| `y` | Yank (copy) | Normal mode |
| `p` | Paste after | Normal mode |
| `P` | Paste before | Normal mode |

### Delete Operator

Delete removes text and stays in Normal mode.

| Command | Action |
|---------|--------|
| `dw` | Delete word |
| `d$` | Delete to end of line |
| `dd` | Delete entire line |
| `d2w` | Delete 2 words |
| `dt)` | Delete until `)` |

**Remember**: Deleted text goes into a register (like clipboard).

### Change Operator

Change deletes and enters Insert mode (delete + enter insert).

| Command | Action |
|---------|--------|
| `cw` | Change word |
| `c$` | Change to end of line |
| `cc` | Change entire line |
| `ct)` | Change until `)` |
| `ci"` | Change inside quotes |

**Use case**: When you want to replace text, not just delete it.

### Yank (Copy) Operator

Yank copies text without deleting.

| Command | Action |
|---------|--------|
| `yw` | Yank word |
| `y$` | Yank to end of line |
| `yy` | Yank entire line |
| `Y` | Yank entire line (shortcut) |
| `yap` | Yank a paragraph |

**Remember**: `y` is "yank", not "copy" (Vim's terminology).

### Paste

| Command | Action |
|---------|--------|
| `p` | Paste after cursor/line |
| `P` | Paste before cursor/line |
| `gp` | Paste and move cursor after |
| `gP` | Paste before and move cursor |

**Behavior**:
- Line-wise yanks paste on new line
- Character-wise yanks paste after cursor

## Common Editing Commands

### Quick Edits

| Command | Action |
|---------|--------|
| `x` | Delete character under cursor |
| `X` | Delete character before cursor |
| `r{char}` | Replace single character |
| `s` | Substitute character (delete + insert) |
| `S` | Substitute line (delete line + insert) |
| `~` | Toggle case |
| `u` | Undo |
| `Ctrl-r` | Redo |
| `.` | Repeat last change |

**The dot command** (`.`) is incredibly powerful. It repeats your last change.

### Combining Lines

| Command | Action |
|---------|--------|
| `J` | Join current line with next |
| `gJ` | Join without space |

## Text Objects (Introduction)

Text objects allow you to operate on semantic units:

### Word Objects

| Command | Action |
|---------|--------|
| `iw` | Inner word |
| `aw` | A word (includes space) |
| `iW` | Inner WORD |
| `aW` | A WORD |

**Example**:
```
Hello world
  ^
  cursor

ciw  - Change inner word (just "Hello")
caw  - Change a word (includes trailing space)
```

### Quote Objects

| Command | Action |
|---------|--------|
| `i"` | Inside double quotes |
| `a"` | Around double quotes (includes quotes) |
| `i'` | Inside single quotes |
| `a'` | Around single quotes |
| `` i` `` | Inside backticks |
| `` a` `` | Around backticks |

**Example**:
```
const str = "Hello World";
             ^
             cursor anywhere in quotes

ci"  - Change inside quotes: "Hello World" → ""
ca"  - Change around quotes: removes entire "Hello World"
```

### Bracket Objects

| Command | Action |
|---------|--------|
| `i(` or `ib` | Inside parentheses |
| `a(` or `ab` | Around parentheses |
| `i{` or `iB` | Inside braces |
| `a{` or `aB` | Around braces |
| `i[` | Inside brackets |
| `a[` | Around brackets |
| `i<` | Inside angle brackets |
| `a<` | Around angle brackets |

**Example**:
```
function(arg1, arg2)
            ^
            cursor

ci(  - Clear function arguments
ca(  - Remove parentheses and contents
```

### Tag Objects (HTML/XML)

| Command | Action |
|---------|--------|
| `it` | Inside tag |
| `at` | Around tag |

**Example**:
```html
<div>Hello</div>
     ^

cit  - Change "Hello"
cat  - Delete entire <div>Hello</div>
```

## Practical Examples

### Example 1: Change a Word

```
Before: The quick brown fox
              ^
              cursor

Command: ciw
Result: The  brown fox
Mode: Insert (cursor ready to type)
```

### Example 2: Delete Inside Quotes

```
Before: print("Hello, World!")
                  ^

Command: di"
Result: print("")
```

### Example 3: Yank and Paste

```
1. yy     - Yank current line
2. 3j     - Move down 3 lines
3. p      - Paste below current line
```

### Example 4: Dot Repeat

```
Before: one two three four five

1. ciwNUMBER<Esc>  - Change "one" to "NUMBER"
   Result: NUMBER two three four five

2. w               - Move to "two"
3. .               - Repeat change
   Result: NUMBER NUMBER three four five

4. w.              - Move and repeat
   Result: NUMBER NUMBER NUMBER four five
```

The dot command (`.`) repeats the entire change operation.

## Common Patterns

### Pattern 1: Delete and Paste

```
1. dd    - Delete line
2. 5j    - Move down 5 lines
3. p     - Paste
```

### Pattern 2: Change Inner Word

```
1. ciw        - Change inner word
2. type new   - Type replacement
3. Esc        - Exit insert mode
4. w          - Move to next word
5. .          - Repeat change
```

### Pattern 3: Visual Select and Delete

```
1. v     - Enter visual mode
2. 3j    - Select 3 lines down
3. d     - Delete selection
```

## Registers (Preview)

When you delete or yank, text goes into registers:

| Register | Purpose |
|----------|---------|
| `"` | Default (unnamed) |
| `0` | Last yank |
| `1-9` | Delete history |
| `a-z` | Named registers |
| `+` | System clipboard |
| `*` | System selection |

**Using registers**:
```
"ayy    - Yank line into register 'a'
"ap     - Paste from register 'a'
"+yy    - Yank to system clipboard
"+p     - Paste from system clipboard
```

We'll cover registers in depth in [Module 2: Intermediate](../02-intermediate/README.md).

## Undo Tree

| Command | Action |
|---------|--------|
| `u` | Undo |
| `Ctrl-r` | Redo |
| `:earlier 10m` | Go back 10 minutes |
| `:later 5m` | Go forward 5 minutes |
| `g-` | Move back in undo tree |
| `g+` | Move forward in undo tree |

Neovim maintains an undo tree (not just linear undo).

## Exercises

### Exercise 1: Basic Operators

Open [exercises/03-editing.txt](exercises/03-editing.txt):

1. Delete a word with `dw`
2. Change a word with `cw`
3. Yank a line with `yy`
4. Paste it with `p`
5. Undo with `u`
6. Redo with `Ctrl-r`

### Exercise 2: Text Objects

Using the same file:

1. Find a word in quotes
2. Delete inside quotes with `di"`
3. Find a function call
4. Change inside parentheses with `ci(`
5. Find a word
6. Change the whole word with `caw`

### Exercise 3: Dot Command

1. Change a word with `ciwnew<Esc>`
2. Move to another similar word with `w`
3. Repeat the change with `.`
4. Practice this pattern 10 times

### Exercise 4: Combined Operations

1. Search for a word with `/word<Enter>`
2. Change it with `ciw`
3. Type replacement and `Esc`
4. Find next occurrence with `n`
5. Repeat change with `.`

## Efficiency Tips

1. **Use text objects** - `ciw` is faster than `bdwi`
2. **Use the dot command** - Make repeatable changes
3. **Think in operations** - "change inside quotes" not "move, delete, insert"
4. **Learn `c` vs `d`** - Use `c` when you know you'll insert
5. **Visual mode is slower** - Operators + motions are often faster

## Building Muscle Memory

**Day 1-3**: Focus on `d`, `c`, `y`, `p` with basic motions (`w`, `$`, `j`)
**Day 4-7**: Add text objects (`iw`, `i"`, `i(`)
**Week 2**: Practice dot command and combining operations
**Week 3**: Add registers and advanced text objects

Practice daily on real code.

## Assessment

You're proficient when you can:

- ✅ Use `d`, `c`, `y`, `p` without thinking
- ✅ Combine operators with motions (`d2w`, `c$`)
- ✅ Use text objects (`ciw`, `di"`, `ca(`)
- ✅ Repeat changes with `.`
- ✅ Undo/redo comfortably
- ✅ Think "change inside word" not "delete and insert"

## Quick Reference Card

```
Operators:
  d - delete    c - change    y - yank    p - paste

Motions:
  w - word      $ - end       0 - start   j/k - lines

Text Objects:
  iw - inner word      aw - a word
  i" - inside quotes   a" - around quotes
  i( - inside parens   a( - around parens

Special:
  u - undo      Ctrl-r - redo    . - repeat
  x - delete char    r - replace char
```

## Common Mistakes

1. **Using Visual mode unnecessarily** - `ciw` is faster than `viwc`
2. **Not using text objects** - `di"` is more reliable than manual selection
3. **Forgetting the dot command** - Repeating changes manually
4. **Not staying in Normal mode** - Return to Normal after each edit
5. **Using undo as delete** - Use `d` to delete, `u` to undo mistakes

## Module Complete!

You've now learned:
- ✅ Modal editing (Normal, Insert, Visual, Command)
- ✅ Efficient navigation (hjkl, w/b, f/t, search)
- ✅ Core operators (d, c, y, p)
- ✅ Text objects (iw, i", i()
- ✅ The dot command

**Practice these fundamentals** for at least a few days before moving to the next module.

## Next Steps

1. **Practice daily** with real work
2. **Complete all exercises** in this module
3. When comfortable, proceed to [Module 2: Intermediate](../02-intermediate/README.md)

## Additional Resources

- `:help operator` - All operators
- `:help text-objects` - All text objects
- `:help registers` - Register system
- `:help undo` - Undo tree
- `:help .` - Dot command
- [Vim Text Objects: The Definitive Guide](https://blog.carbonfive.com/vim-text-objects-the-definitive-guide/)
