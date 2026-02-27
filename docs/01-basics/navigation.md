# Lesson 2: Navigation

Efficient navigation is what makes Neovim powerful. This lesson teaches you to move around files quickly without using arrow keys or the mouse.

## Basic Movement: hjkl

The foundation of Vim navigation:

```
       k (up)
        ↑
h (left) ← → l (right)
        ↓
      j (down)
```

**Why not arrow keys?**
- Keeps hands on home row
- Faster once learned
- Available on all keyboards/systems
- Forces you to learn Neovim's efficient movements

**Practice**: Disable arrow keys mentally for the first week. Trust the process.

## Word Movement

Moving word-by-word is much faster than character-by-character:

| Command | Action |
|---------|--------|
| `w` | Next word (start) |
| `e` | Next word (end) |
| `b` | Previous word (start) |
| `ge` | Previous word (end) |
| `W` | Next WORD (whitespace-separated) |
| `E` | Next WORD (end) |
| `B` | Previous WORD |

**word vs WORD**:
- `word`: Delimited by punctuation (`foo-bar` is 3 words: `foo`, `-`, `bar`)
- `WORD`: Delimited by whitespace (`foo-bar` is 1 WORD)

**Example**:
```
The quick-brown fox jumps
    w w w   w   w
    W   W   W   W
```

Use `w` for code, `W` for prose.

## Line Movement

| Command | Action |
|---------|--------|
| `0` | Start of line |
| `^` | First non-blank character |
| `$` | End of line |
| `g_` | Last non-blank character |

**Remember**: `0` is absolute start, `^` is practical start.

## Screen Movement

| Command | Action |
|---------|--------|
| `H` | Top of screen (High) |
| `M` | Middle of screen |
| `L` | Bottom of screen (Low) |
| `Ctrl-u` | Scroll up half page |
| `Ctrl-d` | Scroll down half page |
| `Ctrl-b` | Scroll up full page (Back) |
| `Ctrl-f` | Scroll down full page (Forward) |
| `zt` | Move current line to top |
| `zz` | Center current line |
| `zb` | Move current line to bottom |

**Use case**: Quickly reposition code you're working on.

## File Movement

| Command | Action |
|---------|--------|
| `gg` | Go to first line |
| `G` | Go to last line |
| `{number}G` | Go to line number (e.g., `42G`) |
| `{number}gg` | Go to line number (e.g., `42gg`) |
| `%` | Jump to matching bracket/paren |

**Example**: `:set number` to see line numbers, then `42G` to jump to line 42.

## Find and Search

### Character Find

| Command | Action |
|---------|--------|
| `f{char}` | Find next `{char}` on line (inclusive) |
| `F{char}` | Find previous `{char}` on line |
| `t{char}` | Till next `{char}` on line (exclusive) |
| `T{char}` | Till previous `{char}` on line |
| `;` | Repeat last find forward |
| `,` | Repeat last find backward |

**Example**:
```
const myVariable = getValue();
      f          fv   ft
      ^          ^    ^
```

- `fv` - Find next 'v'
- `;` - Find next 'v' (repeat)
- `ft` - Find next 't'

**Use case**: `dt)` deletes until the next `)` character.

### Pattern Search

| Command | Action |
|---------|--------|
| `/pattern` | Search forward for pattern |
| `?pattern` | Search backward for pattern |
| `n` | Next match (same direction) |
| `N` | Previous match (opposite direction) |
| `*` | Search forward for word under cursor |
| `#` | Search backward for word under cursor |

**Example**:
```
/function<Enter>    " Search for "function"
n                   " Next match
N                   " Previous match
```

**Tips**:
- Use `*` on a variable to find all uses
- Use `/` for precision searching
- `:noh` to clear search highlighting

## Marks and Jumps

### Automatic Marks

| Command | Action |
|---------|--------|
| `` ` ` `` | Jump to last position |
| `''` | Jump to last position (line start) |
| `Ctrl-o` | Jump to older position |
| `Ctrl-i` | Jump to newer position |

**Jump list**: Neovim remembers where you've been. Navigate with `Ctrl-o` and `Ctrl-i`.

### Manual Marks

| Command | Action |
|---------|--------|
| `m{a-z}` | Set mark (local to buffer) |
| `m{A-Z}` | Set mark (global across files) |
| `` `{mark}`` | Jump to mark |
| `'{mark}` | Jump to mark (line start) |
| `:marks` | List all marks |

**Example**:
```
ma          " Set mark 'a'
(navigate away)
`a          " Jump back to mark 'a'
```

## Combining with Counts

All movements can use counts:

| Command | Action |
|---------|--------|
| `3w` | Move forward 3 words |
| `5j` | Move down 5 lines |
| `2}` | Move forward 2 paragraphs |

**Don't**: `wwwww` (5 keystrokes)
**Do**: `5w` (2 keystrokes)

## Text Objects (Preview)

While technically editing, these are navigation-related:

| Command | Action |
|---------|--------|
| `(` / `)` | Previous/next sentence |
| `{` / `}` | Previous/next paragraph |
| `[[` / `]]` | Previous/next section |

## Practical Examples

### Example 1: Navigate to Function Definition

```
Goal: Find the function "getUserData"

1. Press * on the word "getUserData"
2. Press n to find the next occurrence
3. Press n again to find the definition
```

### Example 2: Jump to Line 42

```
Goal: Go to line 42

Method 1: :42<Enter>
Method 2: 42G
Method 3: 42gg
```

### Example 3: Navigate Function Call

```
Code: myFunction(arg1, arg2, arg3);

1. Position cursor on 'm' in myFunction
2. Press f( to jump to opening paren
3. Press % to jump to closing paren
```

## Common Navigation Patterns

### Pattern 1: Finding and Editing

```
1. * to search for word under cursor
2. n to find next occurrence
3. ciw to change inner word
```

### Pattern 2: Quick Line Navigation

```
1. ^ to jump to first non-blank
2. (make edit)
3. $ to jump to end of line
```

### Pattern 3: Function Navigation

```
1. [[ to jump to previous function
2. ]] to jump to next function
3. % to jump between braces
```

## Exercises

### Exercise 1: Basic Movement

Open [exercises/02-navigation.txt](exercises/02-navigation.txt):

1. Move to line 10 using `10G`
2. Move to the first non-blank character with `^`
3. Move to the end of the line with `$`
4. Move down 5 lines with `5j`
5. Move up 3 lines with `3k`

### Exercise 2: Word Movement

Using the same file:

1. Find a long line
2. Practice `w` (next word) and `b` (previous word)
3. Notice difference between `w` and `W` on hyphenated words
4. Use `e` to jump to word ends

### Exercise 3: Find and Search

1. Press `f` followed by a letter to find it on the current line
2. Press `;` to repeat the find
3. Press `,` to reverse the find
4. Use `*` on a word to search for it in the file
5. Use `n` and `N` to navigate matches

### Exercise 4: Combined Navigation

Navigate to a function definition:

1. Use `/function<Enter>` to search
2. Use `n` to find your target function
3. Use `%` to jump between opening and closing braces
4. Use `Ctrl-o` to jump back to where you started

## Efficiency Tips

1. **Think in chunks**: Move by words/paragraphs, not characters/lines
2. **Use search**: `/` is often faster than manual navigation
3. **Use `*`**: Quick way to find word under cursor
4. **Relative line numbers**: Makes `{count}j/k` easier (`:set relativenumber`)
5. **Learn `f` and `t`**: Incredibly fast for intra-line movement

## Building Muscle Memory

**Phase 1**: Focus only on `hjkl`, `w`, `b`, `0`, `$`
**Phase 2**: Add `f`, `t`, `/`, `*`
**Phase 3**: Add `gg`, `G`, `{`, `}`
**Phase 4**: Add marks, jumps, and advanced movements

Don't try to learn everything at once.

## Assessment

You're proficient when you can:

- ✅ Navigate a file without arrow keys
- ✅ Use `w` and `b` more than `l` and `h`
- ✅ Jump to specific lines with `G`
- ✅ Find characters on a line with `f` and `t`
- ✅ Search with `/` and navigate with `n`/`N`
- ✅ Use `*` to search for word under cursor
- ✅ Not think about which key to press

## Quick Reference Card

```
Basic: hjkl (left, down, up, right)
Words: w, e, b (next word, end, back)
Line:  0, ^, $ (start, first non-blank, end)
File:  gg, G (top, bottom)
Find:  f, F, t, T, ;, , (find char, repeat)
Search: /, ?, n, N, *, # (search, next, prev)
Jump:  Ctrl-o, Ctrl-i (older, newer position)
```

## Next Lesson

Once comfortable with navigation, proceed to [Lesson 3: Basic Editing](editing.md) to combine movements with operators.

## Additional Resources

- `:help navigation` - All navigation commands
- `:help motion.txt` - Detailed motion reference
- `:help jumps` - Jump list documentation
- `:help search` - Search command details
- [Vim Golf](https://www.vimgolf.com/) - Practice efficient navigation
