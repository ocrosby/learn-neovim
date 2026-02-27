# Your First Week with Neovim - Daily Checklist

This checklist breaks down your first week into manageable daily goals. Check off each item as you complete it!

## Day 1: Survival & Tutorial ☑️

**Time commitment:** 1-2 hours

### Morning/First Session
- [ ] Install Neovim
- [ ] Open Neovim: `nvim`
- [ ] Memorize the 5 survival commands:
  - [ ] `i` - Start typing
  - [ ] `Esc` - Stop typing
  - [ ] `:wq` - Save and quit
  - [ ] `:q!` - Quit without saving
  - [ ] `u` - Undo

### Main Session
- [ ] Run `:Tutor` and complete it (30 minutes)
- [ ] Create a practice file: `nvim practice.txt`
- [ ] Practice the survival commands 10 times:
  - [ ] Press `i`, type something, press `Esc`
  - [ ] Type `:q!` to quit
  - [ ] Repeat until it feels natural

### End of Day
- [ ] Try editing one real file from your work
- [ ] Practice for at least 15 minutes
- [ ] Can you save and quit without looking at notes?

**Goal:** Don't panic when Neovim opens. Know how to get out!

---

## Day 2: Basic Navigation ☑️

**Time commitment:** 30-60 minutes

### Morning Practice (15 min)
- [ ] Open a file: `nvim somefile.txt`
- [ ] Practice hjkl navigation:
  - [ ] `h` - left (10 times)
  - [ ] `j` - down (10 times)
  - [ ] `k` - up (10 times)
  - [ ] `l` - right (10 times)
- [ ] Avoid arrow keys completely

### Main Practice (30 min)
- [ ] Practice word navigation:
  - [ ] `w` - next word (try 20 times)
  - [ ] `b` - back word (try 20 times)
- [ ] Practice line navigation:
  - [ ] `0` - start of line (try 10 times)
  - [ ] `$` - end of line (try 10 times)

### Real Work (15 min)
- [ ] Open a real file from your work
- [ ] Navigate using only `hjkl` and `w/b`
- [ ] No arrow keys!

**Goal:** Navigate without arrow keys. It will feel weird - that's OK!

---

## Day 3: Basic Editing ☑️

**Time commitment:** 30-60 minutes

### Morning Review (10 min)
- [ ] Can you navigate with `hjkl` without thinking?
- [ ] If not, practice more before continuing

### Learn Editing Commands (20 min)
- [ ] Practice INSERT modes:
  - [ ] `i` - insert before cursor
  - [ ] `a` - insert after cursor
  - [ ] `o` - insert on new line below
- [ ] Practice deleting:
  - [ ] `x` - delete character
  - [ ] `dd` - delete line
  - [ ] `u` - undo (practice undoing mistakes!)

### Practice Pattern (30 min)
Try this sequence 10 times:
- [ ] Navigate to a line with `j/k`
- [ ] Delete it with `dd`
- [ ] Press `u` to undo
- [ ] Insert new text with `o`
- [ ] Type something
- [ ] Press `Esc`

### Real Work
- [ ] Do ONE small editing task in a real file
- [ ] Keep your old editor open for "important" work

**Goal:** Edit and undo comfortably. Don't fear making mistakes!

---

## Day 4: Building Speed ☑️

**Time commitment:** 30-60 minutes

**This is when it starts to click!**

### Morning Practice (15 min)
- [ ] Review all commands from Days 1-3
- [ ] Time yourself: Can you do these in 5 seconds each?
  - [ ] Open file, insert text, save, quit
  - [ ] Navigate to bottom of file and back
  - [ ] Delete a line and undo

### Combine Commands (30 min)
- [ ] Practice `d` with motions:
  - [ ] `dw` - delete word
  - [ ] `d$` - delete to end of line
  - [ ] `d0` - delete to start of line
- [ ] Practice with counts:
  - [ ] `3j` - down 3 lines
  - [ ] `2dd` - delete 2 lines
  - [ ] `5w` - forward 5 words

### Real Work (15 min)
- [ ] Use Neovim for 2-3 small tasks today
- [ ] Notice what feels faster, what feels slower

**Goal:** Start combining commands. Feel the power building!

---

## Day 5: Text Objects ☑️

**Time commitment:** 30-60 minutes

**Game changer day!**

### Learn Text Objects (20 min)
- [ ] Practice `ciw` - change inner word (10 times)
- [ ] Practice `diw` - delete inner word (10 times)
- [ ] Practice `yiw` - yank (copy) inner word (10 times)
- [ ] Try `ci"` - change inside quotes
- [ ] Try `ci(` - change inside parentheses

### The Pattern (20 min)
Understand: `[operator][inner/around][object]`
- [ ] `ciw` = change inner word
- [ ] `daw` = delete a word (includes space)
- [ ] `yi"` = yank inside quotes

Practice this pattern 20 times with different combinations.

### Real Work (20 min)
- [ ] Find code with function calls: `function(arg1, arg2)`
- [ ] Try `ci(` to change the arguments
- [ ] Find quoted strings
- [ ] Try `ci"` to change inside quotes

**Goal:** Text objects make you 10x faster. This is Neovim's superpower!

---

## Day 6: Real Work Day ☑️

**Time commitment:** Use Neovim as much as possible today

### Morning
- [ ] Use Neovim for your first task of the day
- [ ] Keep notes of what feels hard

### Throughout Day
- [ ] Use Neovim for at least 50% of your work
- [ ] Fall back to old editor when under time pressure (that's OK!)
- [ ] Try one new command: `/` for search
  - [ ] `/word` - search for "word"
  - [ ] `n` - next match
  - [ ] `N` - previous match

### End of Day Reflection
- [ ] What was faster in Neovim?
- [ ] What was slower?
- [ ] What do you need to practice tomorrow?

**Goal:** Use Neovim for real work. Feel the progress!

---

## Day 7: Review & Assessment ☑️

**Time commitment:** 1 hour

### Skills Check (30 min)
Can you do these without thinking?

**Navigation:**
- [ ] Move with `hjkl` fluently
- [ ] Jump words with `w` and `b`
- [ ] Go to start/end of line with `0` and `$`
- [ ] Search with `/` and navigate matches with `n`

**Editing:**
- [ ] Enter INSERT mode with `i`, `a`, `o`
- [ ] Delete with `x` and `dd`
- [ ] Undo with `u`
- [ ] Copy line with `yy` and paste with `p`

**Text Objects:**
- [ ] Change inner word with `ciw`
- [ ] Delete inner word with `diw`
- [ ] Change inside quotes with `ci"`

### Real Work Test (30 min)
- [ ] Complete a real coding task in Neovim
- [ ] Time yourself
- [ ] Compare to your old editor (you might be close now!)

### Celebrate!
- [ ] You made it through the hardest week!
- [ ] You're now a Neovim user
- [ ] The hard part is behind you

**Goal:** Assess your progress and celebrate making it through the first week!

---

## After Week 1: What's Next?

### You're Ready For:
- [ ] [Module 2: Intermediate Skills](../docs/02-intermediate/) - Learn registers, macros, advanced operators
- [ ] Trying the [basic example config](../examples/basic/) with plugins
- [ ] Customizing your setup

### Continue Daily Practice:
- Use Neovim as your primary editor
- Learn one new command per day
- Practice what feels awkward
- Don't try to learn everything at once

### Week 2 Goals:
- [ ] Learn Visual mode (`v`, `V`, `Ctrl-v`)
- [ ] Master window splits (`:split`, `:vsplit`)
- [ ] Learn more text objects (`ap`, `i{`, `it`)
- [ ] Start using registers (`"ayy`, `"ap`)

## Tips for Success

### Do's ✅
- ✅ Practice every day, even just 15 minutes
- ✅ Use Neovim for real work, not just exercises
- ✅ Focus on accuracy first, speed comes later
- ✅ Celebrate small wins
- ✅ Keep the [QUICKSTART.md](QUICKSTART.md) reference nearby

### Don'ts ❌
- ❌ Don't try to learn everything at once
- ❌ Don't give up on Day 2 or 3 (it gets better!)
- ❌ Don't compare your Day 3 speed to your old editor
- ❌ Don't add plugins yet - learn the fundamentals first
- ❌ Don't use arrow keys - break the habit now!

## Emergency Reminders

**Can't type?** Press `i`  
**Can't quit?** Press `Esc`, then `:q!`  
**Messed up?** Press `Esc`, then `u` to undo  
**Lost?** Press `Esc` multiple times, you'll get to NORMAL mode  

## Progress Tracker

Track your confidence level each day (1-10):

| Day | Confidence | Notes |
|-----|-----------|-------|
| 1   | ___/10   | |
| 2   | ___/10   | |
| 3   | ___/10   | |
| 4   | ___/10   | |
| 5   | ___/10   | |
| 6   | ___/10   | |
| 7   | ___/10   | |

**If any day is below 5/10:** Spend another day on that content before moving forward.

---

**You've got this!** The first week is the hardest. After that, it's all uphill. 🚀

Print this checklist and keep it visible during your first week!
