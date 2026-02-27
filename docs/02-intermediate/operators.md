# Lesson 2: Advanced Operators

Building on the basic operators from Module 1, let's explore more powerful editing operators and combinations.

## Review: Basic Operators

| Operator | Action |
|----------|--------|
| `d` | Delete |
| `c` | Change (delete + insert) |
| `y` | Yank (copy) |
| `p` | Paste after |
| `P` | Paste before |

## Additional Operators

### Indentation Operators

| Command | Action |
|---------|--------|
| `>` | Indent right |
| `<` | Indent left |
| `=` | Auto-indent (format) |

**Examples**:
```
>>    - Indent current line
>}    - Indent to end of paragraph
>G    - Indent to end of file
<3j   - Un-indent 3 lines down
=ap   - Auto-format paragraph
```

### Case Operators

| Command | Action |
|---------|--------|
| `~` | Toggle case of character |
| `gu` | Make lowercase |
| `gU` | Make UPPERCASE |
| `g~` | Toggle case |

**Examples**:
```
guu   - Lowercase current line
gUU   - UPPERCASE current line
g~w   - Toggle case of word
gUiw  - UPPERCASE inner word
```

### Comment Operator (with plugin)

Most comment plugins provide `gc` operator:
```
gcc   - Comment/uncomment line
gcap  - Comment/uncomment paragraph
gc3j  - Comment 3 lines down
```

## Operator Combinations

### Doubling Operators

When you double an operator, it operates on the current line:

| Command | Action |
|---------|--------|
| `dd` | Delete line |
| `cc` | Change line |
| `yy` | Yank line |
| `>>` | Indent line |
| `<<` | Un-indent line |
| `==` | Auto-indent line |
| `guu` | Lowercase line |
| `gUU` | UPPERCASE line |

### Operators with Counts

Counts can come before or after the operator:

```
d3w   - Delete 3 words
3dw   - Delete 3 words (same)
3dd   - Delete 3 lines
y5j   - Yank 5 lines down
2>}   - Indent next 2 paragraphs
```

### Operators with Motions

Combine any operator with any motion:

```
d$    - Delete to end of line
c^    - Change to start of line
y%    - Yank to matching bracket
dt,   - Delete until comma
cf)   - Change to (and including) )
y/end - Yank until "end"
```

### Operators with Text Objects

Most powerful combination:

```
diw   - Delete inner word
ci"   - Change inside quotes
yap   - Yank a paragraph
da{   - Delete around braces
vi(   - Visual select inside parens
=i{   - Auto-format inside braces
gUaw  - UPPERCASE a word
```

## Visual Mode Operators

Apply operators to visual selections:

### Character-wise Visual (`v`)

```
1. v     - Enter visual mode
2. 3w    - Select 3 words
3. d     - Delete selection
```

### Line-wise Visual (`V`)

```
1. V     - Enter visual line mode
2. 2j    - Select 3 lines total
3. >     - Indent selection
```

### Block Visual (`Ctrl-v`)

```
1. Ctrl-v  - Enter visual block mode
2. 5j      - Select down 5 lines
3. I       - Insert at start of each line
4. //      - Type comment
5. Esc     - Apply to all lines
```

## Special Operators

### Replace Mode

| Command | Action |
|---------|--------|
| `r{char}` | Replace single character |
| `R` | Enter Replace mode |
| `gr{char}` | Virtual replace (respects tabs) |
| `gR` | Enter Virtual Replace mode |

**Example**:
```
Hello World
  ^
  cursor

rx    - "Hexlo World"
R     - Enter Replace mode, type over
```

### Substitute

| Command | Action |
|---------|--------|
| `s` | Substitute character (delete + insert) |
| `S` | Substitute line (delete line + insert) |
| `C` | Change to end of line |
| `D` | Delete to end of line |

**Equivalents**:
```
s  = cl   (change letter)
S  = cc   (change line)
C  = c$   (change to end)
D  = d$   (delete to end)
```

### Join Lines

| Command | Action |
|---------|--------|
| `J` | Join current line with next (add space) |
| `gJ` | Join without adding space |
| `3J` | Join 3 lines |

**Example**:
```
Before:
Hello
World

After J:
Hello World

After gJ:
HelloWorld
```

## Filter Operator

| Command | Action |
|---------|--------|
| `!` | Filter through external command |

**Examples**:
```
!}sort       - Sort paragraph
!Gsort       - Sort to end of file
!ipjq .      - Format JSON in paragraph
5!!tr 'a-z' 'A-Z'  - UPPERCASE 5 lines
```

### Visual Mode Filtering

```
1. Select lines with V
2. Press !
3. Type shell command
4. Press Enter
```

**Use cases**:
- `sort` - Sort lines
- `uniq` - Remove duplicates
- `column -t` - Align columns
- `jq .` - Format JSON
- `xmllint --format -` - Format XML

## Operator Pending Mode

After typing an operator, you're in "operator-pending mode":

```
d_       - Type d, waiting for motion
c_       - Type c, waiting for motion
y_       - Type y, waiting for motion
```

You can:
1. Complete with motion: `dw`, `c$`, `y}`
2. Cancel with `Esc`
3. Complete with text object: `diw`, `ca"`

## Custom Operators (with plugins)

Popular plugin operators:

### vim-surround

| Command | Action |
|---------|--------|
| `ys` | Surround (you surround) |
| `ds` | Delete surrounding |
| `cs` | Change surrounding |

**Examples**:
```
ysiw"   - Surround word with quotes
dst     - Delete surrounding tag
cs"'    - Change " to '
```

### vim-commentary

```
gc{motion}  - Comment/uncomment
gcc         - Comment line
gcap        - Comment paragraph
```

### vim-exchange

```
cx{motion}  - Exchange (swap) text
cxx         - Exchange line
```

## Operator Recipes

### Recipe 1: Swap Two Lines

```
ddp         - Delete line, paste below
```

### Recipe 2: Duplicate Line

```
yyp         - Yank line, paste below
Yp          - Same (Y = yy)
```

### Recipe 3: Move Line Up

```
ddkP        - Delete line, move up, paste before
```

### Recipe 4: Format Function

```
=i{         - Auto-indent inside braces
```

### Recipe 5: UPPERCASE Variable

```
gUiw        - UPPERCASE inner word
```

### Recipe 6: Sort Selection

```
Vip!sort    - Visual select paragraph, sort
```

### Recipe 7: Center Line

```
:center     - Center current line
```

## Practical Examples

### Example 1: Fix Indentation

```python
def hello():
print("world")
    print("indented wrong")

Solution:
1. Place cursor on "def"
2. =i}      - Auto-indent inside function
```

### Example 2: Change String Delimiters

```javascript
const str = "Hello World";

Task: Change to single quotes

Solution:
1. Cursor anywhere in string
2. cs"'    - Change surrounding " to ' (needs vim-surround)

Alternative without plugin:
1. ca"'Hello World'<Esc>
```

### Example 3: Comment Multiple Lines

```python
x = 1
y = 2
z = 3

Task: Comment out all three

Solution:
1. Place cursor on first line
2. Vjj     - Visual select 3 lines
3. gc      - Comment (with plugin)

Alternative:
1. Ctrl-v  - Visual block
2. jj      - Select 3 lines
3. I#<Esc> - Insert # at start
```

### Example 4: Sort CSS Properties

```css
.container {
  padding: 10px;
  color: red;
  background: blue;
  margin: 5px;
}

Task: Sort properties alphabetically

Solution:
1. Place cursor on first property
2. vi{     - Visual select inside braces
3. !sort   - Sort through external command
```

### Example 5: Swap Function Arguments

```javascript
function calculate(x, y) {
  return x + y;
}

Task: Swap x and y parameters

Solution:
1. ci(y, x<Esc>  - Change inside parens
```

## Building Muscle Memory

**Phase 1**: Focus on `d`, `c`, `y` with motions
**Phase 2**: Add `>`, `<`, `=` for indentation
**Phase 3**: Add `gu`, `gU` for case changes
**Phase 4**: Add visual mode operators

Practice pattern:
1. Identify what you want to change
2. Think in operator + motion/object
3. Execute in one command
4. Repeat with `.` if needed

## Common Mistakes

1. **Using visual mode unnecessarily** - `diw` is faster than `viwd`
2. **Not using text objects** - `ci"` beats manual selection
3. **Forgetting counts** - `3dd` not `ddjddjdd`
4. **Not using `.` to repeat** - Let Neovim repeat for you
5. **Not learning indentation operators** - `>` and `=` save tons of time

## Assessment

You're proficient when you can:

- ✅ Use all basic operators fluently (`d`, `c`, `y`, `p`)
- ✅ Indent with `>`, `<`, and format with `=`
- ✅ Change case with `gu`, `gU`, `~`
- ✅ Combine operators with counts and motions
- ✅ Use operators with text objects efficiently
- ✅ Apply operators in visual mode when needed
- ✅ Think in complete operations, not individual steps

## Quick Reference

```
Basic:
  d - delete    c - change     y - yank      p - paste

Indentation:
  > - indent    < - un-indent  = - format

Case:
  gu - lower    gU - UPPER     ~ - toggle

Line Operations:
  dd - delete line     cc - change line    yy - yank line
  >>- indent line      << - un-indent      == - format line

Special:
  J - join      r - replace    s - substitute
  ! - filter

With Text Objects:
  diw - delete inner word
  ci" - change inside quotes
  yap - yank a paragraph
  =i{ - format inside braces
```

## Next Lesson

Proceed to [Lesson 3: Registers](registers.md) to master Neovim's clipboard system.

## Additional Resources

- `:help operator` - Complete operator reference
- `:help motion.txt` - All motions
- `:help text-objects` - All text objects
- `:help visual-operators` - Visual mode operators
- `:help filter` - Filter operator details
