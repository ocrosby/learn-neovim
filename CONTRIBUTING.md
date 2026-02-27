# Contributing to Learn Neovim

Thank you for your interest in contributing to Learn Neovim! This is a community resource, and contributions of all kinds are welcome.

## 🎯 Types of Contributions

### 1. **Documentation Improvements**
- Fix typos, grammar, or unclear explanations
- Add missing information
- Improve code examples
- Update outdated content

### 2. **New Content**
- Add exercises to existing modules
- Create new example configurations
- Write additional cheatsheets
- Add language-specific guides

### 3. **Bug Reports**
- Report broken links
- Identify incorrect information
- Note missing prerequisites
- Report config issues

### 4. **Feature Suggestions**
- Suggest new modules or topics
- Propose new example configs
- Recommend additional resources

## 🚀 Getting Started

### Prerequisites

- Git installed
- Neovim 0.9+ installed
- Familiarity with Markdown
- Basic understanding of Neovim (if contributing technical content)

### Fork and Clone

```bash
# Fork the repository on GitHub, then:
git clone https://github.com/YOUR-USERNAME/learn-neovim.git
cd learn-neovim

# Add upstream remote
git remote add upstream https://github.com/ocrosby/learn-neovim.git
```

### Create a Branch

```bash
# Sync with upstream
git checkout main
git pull upstream main

# Create a feature branch
git checkout -b fix/typo-in-basics
# or
git checkout -b feature/add-rust-example
```

## 📝 Contribution Guidelines

### Documentation Standards

#### Markdown Formatting

- Use ATX-style headers (`#`, `##`, `###`)
- Include blank lines before and after headers
- Use fenced code blocks with language identifiers
- Keep lines under 120 characters when possible

**Example:**

```markdown
## Section Title

Explanatory text here.

### Subsection

More text.

```lua
-- Code example with language identifier
vim.opt.number = true
```
\`\`\`
```

#### Writing Style

- **Be clear and concise**: Assume readers are learning
- **Use active voice**: "Press `i` to enter Insert mode" not "Insert mode is entered by pressing `i`"
- **Provide examples**: Show, don't just tell
- **Link to official docs**: Use `:help` references when relevant
- **Be encouraging**: Learning Neovim can be challenging

#### Code Examples

- **Test all code**: Ensure examples actually work
- **Include comments**: Explain what the code does
- **Show output**: When relevant, show what users should see
- **Use realistic examples**: Prefer real-world use cases

**Good example:**

```lua
-- Set line numbers and relative line numbers
vim.opt.number = true           -- Show line numbers
vim.opt.relativenumber = true   -- Show relative numbers for easier navigation
```

**Less helpful:**

```lua
-- Some options
vim.opt.number = true
vim.opt.relativenumber = true
```

### Configuration Standards

When contributing example configurations:

#### File Organization

```lua
-- =============================================================================
-- Section Name (e.g., OPTIONS, KEYMAPS, PLUGINS)
-- =============================================================================
-- Brief description if needed

-- Code here
```

#### Configuration Principles

1. **Commented thoroughly**: Every section and non-obvious line explained
2. **Tested**: Verify the config works in a fresh Neovim install
3. **Documented**: Include a comprehensive README
4. **Minimal**: Only include what's necessary for the use case
5. **Follow conventions**: Use patterns from existing examples

#### README for Configurations

Every example config must include:

- **What's included**: List of plugins and features
- **Prerequisites**: Required software and tools
- **Installation**: Step-by-step setup instructions
- **Keybindings**: Table of custom keybindings
- **Usage**: How to use key features
- **Customization**: How to modify the config
- **Troubleshooting**: Common issues and solutions

### Commit Message Guidelines

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>: <description>

[optional body]

[optional footer]
```

**Types:**

- `docs:` Documentation changes
- `feat:` New feature or content
- `fix:` Bug fix
- `chore:` Maintenance tasks
- `refactor:` Code restructuring
- `test:` Adding tests

**Examples:**

```bash
docs: fix typo in LSP configuration guide

fix: correct broken link in Module 3 README

feat: add Rust development example configuration

Includes:
- rust-analyzer LSP setup
- cargo integration
- debugging configuration
```

### Pull Request Process

1. **Ensure your changes work**
   - Test any code examples
   - Verify links are valid
   - Check formatting

2. **Update documentation**
   - Update relevant READMEs if needed
   - Add yourself to acknowledgments if you'd like

3. **Create a clear PR**
   - Use a descriptive title
   - Explain what changes and why
   - Reference any related issues

4. **Be responsive**
   - Address review comments
   - Make requested changes
   - Be patient (this is maintained by volunteers)

**PR Template:**

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Documentation fix/improvement
- [ ] New content
- [ ] Bug fix
- [ ] New feature

## Checklist
- [ ] I have tested my changes
- [ ] I have updated documentation as needed
- [ ] My code follows the style guidelines
- [ ] I have added comments to complex code

## Related Issues
Fixes #123
```

## 🎓 Content Guidelines

### Adding New Modules

If proposing a new learning module:

1. **Discuss first**: Open an issue to discuss the module idea
2. **Follow structure**: Match existing module format
3. **Include exercises**: Practical exercises for each concept
4. **Link appropriately**: Connect to previous and next modules
5. **Estimate time**: Include time estimate for completion

### Adding Example Configurations

New example configs should:

1. **Fill a gap**: Address a specific use case not covered
2. **Be complete**: Fully functional, not partial
3. **Be tested**: Verify in clean Neovim install
4. **Be documented**: Comprehensive README
5. **Be minimal**: Only include what's necessary

**Good example ideas:**
- Rust development configuration
- Data science (Jupyter) configuration
- Golang development configuration
- DevOps tools configuration

**Less suitable:**
- Variations of existing configs
- Very niche/personal configurations
- Configs requiring proprietary tools

### Adding Resources

When adding to `resources/`:

- **Verify links work**: Check URLs before submitting
- **Provide context**: Explain why the resource is valuable
- **Keep organized**: Add to appropriate category
- **Avoid duplicates**: Check if resource already exists

## 🐛 Reporting Issues

### Before Creating an Issue

1. **Search existing issues**: Your issue may already exist
2. **Check documentation**: Verify it's not already addressed
3. **Test on latest**: Ensure issue exists on latest version

### Creating Good Issues

**Bug Report Template:**

```markdown
## Description
Clear description of the bug

## Steps to Reproduce
1. Step one
2. Step two
3. See error

## Expected Behavior
What should happen

## Actual Behavior
What actually happens

## Environment
- Neovim version: (output of `nvim --version`)
- OS: macOS/Linux/Windows
- Example config: minimal/basic/python-dev/web-dev
```

**Content Suggestion Template:**

```markdown
## Suggestion
What content or feature you'd like to see

## Motivation
Why this would be valuable

## Possible Implementation
Ideas for how to implement it (optional)
```

## ✅ Review Process

1. **Automated checks**: Links, markdown formatting (when CI is set up)
2. **Maintainer review**: Content accuracy, style consistency
3. **Feedback**: Maintainers may request changes
4. **Merge**: Once approved, changes are merged

## 🙏 Code of Conduct

### Our Standards

- **Be respectful**: Treat everyone with respect
- **Be patient**: Remember everyone is learning
- **Be constructive**: Offer helpful feedback
- **Be inclusive**: Welcome all contributors
- **Be understanding**: Mistakes happen

### Unacceptable Behavior

- Harassment or discriminatory language
- Personal attacks
- Trolling or inflammatory comments
- Publishing others' private information

## 📄 License

By contributing, you agree that your contributions will be licensed under the MIT License.

## 🎉 Recognition

Contributors will be:
- Listed in acknowledgments (if desired)
- Credited in commit history
- Appreciated by learners worldwide!

## ❓ Questions?

- **General questions**: Open a discussion on GitHub
- **Quick clarifications**: Comment on relevant issue/PR
- **Private matters**: Contact maintainers directly

## 🚀 Getting Help

If you're stuck:

1. Check existing documentation
2. Look at similar merged PRs
3. Ask in the discussion forum
4. Reach out to maintainers

## 📚 Resources for Contributors

- [Markdown Guide](https://www.markdownguide.org/)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [Neovim Documentation](https://neovim.io/doc/)
- [Git Basics](https://git-scm.com/book/en/v2/Getting-Started-Git-Basics)

---

Thank you for contributing to Learn Neovim! Your contributions help developers worldwide master Neovim. 🚀
