# Module 2: Intermediate Neovim

Now that you're comfortable with basic modal editing, it's time to level up your efficiency with advanced text objects, registers, macros, and more.

## Learning Objectives

By the end of this module, you will:

- Master advanced text objects
- Understand and use registers effectively
- Record and replay macros
- Use marks for quick navigation
- Work with multiple windows and buffers
- Understand Neovim's powerful undo tree

## Estimated Time

3-4 hours (with practice)

## Prerequisites

- Completed [Module 1: Basics](../01-basics/README.md)
- Comfortable with modes, basic navigation, and operators
- Practiced basic editing for at least a few days

## Lessons

1. **[Text Objects](text-objects.md)** - Advanced semantic editing
2. **[Operators](operators.md)** - More operators and combinations
3. **[Registers](registers.md)** - The clipboard system on steroids
4. **[Macros](macros.md)** - Recording and replaying complex edits

## Why These Skills Matter

**Text objects** let you think in semantic units: "change inside function", "delete around paragraph"

**Registers** give you unlimited clipboards and powerful paste options

**Macros** automate repetitive edits that would take forever manually

**Marks** let you bookmark locations and jump around large codebases

These are the skills that separate beginner Neovim users from power users.

## Module Philosophy

At this stage, focus on:

1. **Semantic thinking** - "change inside quotes" not "move, select, delete, insert"
2. **Composability** - Combining operators + text objects + counts
3. **Repeatability** - Making edits that can be repeated with `.`
4. **Automation** - Recording macros for repetitive tasks

## Quick Reference

### Advanced Text Objects

| Command | Action |
|---------|--------|
| `ip` / `ap` | Inside/around paragraph |
| `is` / `as` | Inside/around sentence |
| `it` / `at` | Inside/around tag |
| `i{` / `a{` | Inside/around braces |

### Registers

| Register | Purpose |
|----------|---------|
| `"` | Default (unnamed) |
| `0` | Last yank |
| `+` | System clipboard |
| `a-z` | Named registers |

### Macros

| Command | Action |
|---------|--------|
| `q{reg}` | Start recording to register |
| `q` | Stop recording |
| `@{reg}` | Play macro |
| `@@` | Replay last macro |

## Practice Approach

For each lesson:

1. **Read the lesson** to understand the concepts
2. **Try each command** in a test file
3. **Complete the exercises** to build muscle memory
4. **Use in real work** - Force yourself to use new skills
5. **Return to basics** when you feel overwhelmed

Don't try to memorize everything. Learn the patterns.

## Assessment

You're ready for Module 3 when you can:

- ✅ Use text objects fluently (ciw, di", ca{, etc.)
- ✅ Copy/paste using named registers
- ✅ Copy to/from system clipboard
- ✅ Record and replay a simple macro
- ✅ Understand when to use macros vs dot command
- ✅ Use marks for navigation in large files

## Exercises

Each lesson has practice exercises:

- [Exercise 1: Text Objects](exercises/01-text-objects.txt)
- [Exercise 2: Registers](exercises/02-registers.txt)
- [Exercise 3: Macros](exercises/03-macros.txt)

## Next Steps

After completing this module:

1. **Practice for at least a week** using these skills in real work
2. **Don't configure yet** - Learn vanilla Neovim first
3. When comfortable, proceed to [Module 3: Configuration](../03-configuration/README.md)

## Additional Resources

- `:help text-objects`
- `:help registers`
- `:help recording`
- `:help complex-repeat`
- [Mastering the Vim Language](https://www.youtube.com/watch?v=wlR5gYd6um0)

---

**Ready to become more efficient?** Start with [Lesson 1: Text Objects](text-objects.md)
