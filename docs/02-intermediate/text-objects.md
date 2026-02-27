# Lesson 1: Text Objects

Text objects are one of Neovim's most powerful features. They allow you to operate on semantic units of text rather than individual characters or lines.

## What Are Text Objects?

Text objects represent logical units of text:
- Words
- Sentences
- Paragraphs
- Quoted strings
- Parenthesized expressions
- Code blocks

Instead of thinking "move and delete", you think "delete inside quotes" or "change around function".

## The Two Modifiers: `i` and `a`

Every text object has two versions:

| Modifier | Meaning | Behavior |
|----------|---------|----------|
| `i` | **i**nner | Operates inside the object (excludes delimiters) |
| `a` | **a**round | Operates around the object (includes delimiters) |

**Example**:
```
"Hello World"
    ^
    cursor

di"  → ""                    (delete inside quotes)
da"  → (empty)               (delete around quotes, including quotes)
```

## Word Text Objects

| Command | Description |
|---------|-------------|
| `iw` | Inner word |
| `aw` | A word (includes trailing space) |
| `iW` | Inner WORD (whitespace-delimited) |
| `aW` | A WORD (includes trailing space) |

**Example**:
```
The quick-brown fox jumps
        ^
        cursor

ciw   → The quick-brown fox jumps  (change "brown")
caw   → The quickfox jumps          (change "brown" and space)
ciW   → The  fox jumps              (change "quick-brown")
```

**Difference**: `word` stops at punctuation, `WORD` stops at whitespace.

## Quote Text Objects

| Command | Description |
|---------|-------------|
| `i"` | Inside double quotes |
| `a"` | Around double quotes |
| `i'` | Inside single quotes |
| `a'` | Around single quotes |
| `` i` `` | Inside backticks |
| `` a` `` | Around backticks |

**Example**:
```javascript
const message = "Hello, World!";
                    ^
                    cursor anywhere in quotes

ci"   → const message = "";
ca"   → const message = ;
yi"   → yanks "Hello, World!" (without quotes)
ya"   → yanks "Hello, World!" (with quotes)
```

**Smart behavior**: You don't need to be precisely on a delimiter. Anywhere inside the quotes works!

## Parentheses, Brackets, and Braces

| Command | Aliases | Description |
|---------|---------|-------------|
| `i(` | `ib` | Inside parentheses |
| `a(` | `ab` | Around parentheses |
| `i{` | `iB` | Inside braces |
| `a{` | `aB` | Around braces |
| `i[` | | Inside brackets |
| `a[` | | Around brackets |
| `i<` | | Inside angle brackets |
| `a<` | | Around angle brackets |

**Example**:
```javascript
function greet(name, age) {
    console.log("Hello");
}

Cursor in "name, age":
  ci(  → function greet() {
  ca(  → function greet {

Cursor inside function body:
  di{  → function greet(name, age) {}
  da{  → function greet(name, age)
```

**Works with nesting**: Neovim is smart about which pair of delimiters to use.

```javascript
foo(bar(baz))
        ^
        cursor

ci(  → foo(bar())     (operates on inner parentheses)
ca(  → foo()          (removes bar(baz))
```

## Tag Text Objects (HTML/XML)

| Command | Description |
|---------|-------------|
| `it` | Inside tag |
| `at` | Around tag (includes tags) |

**Example**:
```html
<div class="container">
    <p>Hello World</p>
</div>

Cursor in "Hello World":
  cit  → <p></p>
  cat  → (empty, removes entire <p>Hello World</p>)

Cursor in div content:
  dit  → <div class="container"></div>
  dat  → (removes entire div and content)
```

**Works with**:
- HTML tags
- XML tags
- JSX/TSX components

## Sentence and Paragraph Objects

| Command | Description |
|---------|-------------|
| `is` | Inner sentence |
| `as` | A sentence (includes trailing space) |
| `ip` | Inner paragraph |
| `ap` | A paragraph (includes trailing newline) |

**Example**:
```
This is sentence one. This is sentence two. This is sentence three.

Cursor in "sentence two":
  cis  → This is sentence one. . This is sentence three.
  cas  → This is sentence one.This is sentence three.

Multiple paragraphs:

Paragraph one.
Another line.

Paragraph two.

Cursor in paragraph one:
  dip  → (deletes paragraph one, keeps blank line)
  dap  → (deletes paragraph one and blank line)
```

**Use cases**:
- Prose editing
- Documentation
- Comments

## Combining with Operators

Text objects shine when combined with operators:

### Delete + Text Objects

| Command | Action |
|---------|--------|
| `diw` | Delete inner word |
| `di"` | Delete inside quotes |
| `di(` | Delete inside parentheses |
| `dap` | Delete a paragraph |
| `dat` | Delete around tag |

### Change + Text Objects

| Command | Action |
|---------|--------|
| `ciw` | Change inner word |
| `ci"` | Change inside quotes |
| `ci{` | Change inside braces |
| `cit` | Change inside tag |
| `cis` | Change inner sentence |

**Most common pattern**: `ci` followed by delimiter.

### Yank + Text Objects

| Command | Action |
|---------|--------|
| `yiw` | Yank inner word |
| `yi"` | Yank inside quotes |
| `yap` | Yank a paragraph |
| `ya{` | Yank around braces (includes braces) |

### Visual Select + Text Objects

| Command | Action |
|---------|--------|
| `viw` | Visually select inner word |
| `vi"` | Visually select inside quotes |
| `vit` | Visually select inside tag |
| `vap` | Visually select a paragraph |

**Use case**: When you want to see the selection before operating.

## Practical Examples

### Example 1: Refactoring Function Arguments

```javascript
function calculate(x, y, z) {
    return x + y + z;
}

Task: Clear the arguments

1. Place cursor anywhere in "x, y, z"
2. Press ci(
3. Result: function calculate() {
```

### Example 2: Changing String Content

```python
print("The quick brown fox")

Task: Change the message

1. Place cursor anywhere in the string
2. Press ci"
3. Type new message
4. Press Esc
5. Result: print("new message")
```

### Example 3: Duplicating a Paragraph

```markdown
This is a paragraph that I want to duplicate.
It has multiple lines.
And important content.

Task: Duplicate this paragraph

1. Place cursor anywhere in paragraph
2. Press yap (yank a paragraph)
3. Press p (paste)
4. Result: Paragraph duplicated with blank line
```

### Example 4: Deleting HTML Content

```html
<div>
    <h1>Title</h1>
    <p>Some content here</p>
</div>

Task: Clear the div content but keep the div

1. Place cursor inside div
2. Press dit
3. Result: <div></div>
```

### Example 5: Editing Function Calls

```javascript
const result = someFunction(arg1, arg2, arg3);

Task: Change all arguments

1. Press /someFunction to find it
2. Press f( to jump to opening paren
3. Press ci(
4. Type new arguments
5. Result: const result = someFunction(newArgs);
```

## Advanced Patterns

### Pattern 1: Swap Quote Types

```javascript
const str = "Hello";

Task: Change to single quotes

1. ca"'Hello'<Esc>  (change around double quotes, type single quotes)

Alternative:
1. di"              (delete inside double quotes)
2. r'               (replace " with ')
3. p                (paste content)
4. $r'              (go to end, replace " with ')
```

### Pattern 2: Extract to Variable

```javascript
doSomething(calculateValue() + 10);

Task: Extract calculateValue() + 10

1. ci(
2. temp<Esc>
3. O const temp = calculateValue() + 10;
4. Result:
   const temp = calculateValue() + 10;
   doSomething(temp);
```

### Pattern 3: Wrap in Quotes

```javascript
const word = hello;

Task: Wrap hello in quotes

1. ciw"hello"<Esc>

Alternative using surround (plugin):
1. ysiw"  (if vim-surround installed)
```

## Efficiency Tips

1. **Think semantically** - "change inside quotes" not "find quote, delete to quote"
2. **Cursor position doesn't matter** - Works anywhere inside the text object
3. **Combine with search** - `/*` to find word, `ci"` to change it
4. **Use `a` for deletion** - Usually want to remove delimiters too
5. **Use `i` for change** - Usually want to keep delimiters

## Building Muscle Memory

**Week 1**: Focus on `iw`, `i"`, `i(` with `c` and `d`
**Week 2**: Add `aw`, `a"`, `a(` and understand the difference
**Week 3**: Add `it`, `ip`, and other objects
**Week 4**: Combine with search and advanced patterns

Practice pattern:
1. Find text object to edit
2. Think about what you want to do
3. Use operator + text object
4. Resist the urge to manually select

## Common Mistakes

1. **Manually selecting** - `viwd` instead of just `diw`
2. **Using Visual mode unnecessarily** - Text objects are faster
3. **Wrong modifier** - Using `i` when you want `a` or vice versa
4. **Forgetting it works anywhere** - No need to position cursor precisely
5. **Not using with search** - Text objects work great after `/` search

## Assessment

You're proficient when you can:

- ✅ Use `ciw`, `ci"`, `ci(` without thinking
- ✅ Know when to use `i` vs `a`
- ✅ Combine text objects with `d`, `c`, `y` operators
- ✅ Edit quoted strings without selecting manually
- ✅ Clear function arguments with `ci(`
- ✅ Think in semantic units, not character movements

## Quick Reference Card

```
Word Objects:
  iw/aw - inner/around word
  iW/aW - inner/around WORD

Quote Objects:
  i"/a" - inside/around double quotes
  i'/a' - inside/around single quotes
  i`/a` - inside/around backticks

Bracket Objects:
  i(/a( - inside/around parentheses
  i{/a{ - inside/around braces
  i[/a[ - inside/around brackets
  i</a< - inside/around angle brackets

Other Objects:
  it/at - inside/around tag
  is/as - inner/around sentence
  ip/ap - inner/around paragraph

Pattern: [operator][i or a][object]
  ciw - change inner word
  da" - delete around quotes
  yap - yank a paragraph
```

## Next Lesson

Once comfortable with text objects, proceed to [Lesson 2: Operators](operators.md) to learn more powerful operators and combinations.

## Additional Resources

- `:help text-objects`
- `:help object-select`
- `:help word`
- `:help sentence`
- `:help paragraph`
- [Vim Text Objects: The Definitive Guide](https://blog.carbonfive.com/vim-text-objects-the-definitive-guide/)
