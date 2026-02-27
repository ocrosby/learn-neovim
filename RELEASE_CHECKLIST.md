# GitHub Release Checklist

Complete checklist for releasing learn-neovim v1.0.0 to the public.

## Pre-Release (Before Publishing)

### Repository Settings

- [ ] **Set repository description**
  ```
  A comprehensive, step-by-step guide to mastering Neovim from beginner to advanced. Includes 8 learning modules, 4 example configs, and extensive documentation.
  ```

- [ ] **Add repository topics** (GitHub → Settings → Topics)
  - neovim
  - vim
  - tutorial
  - learning
  - lua
  - lsp
  - plugin-manager
  - editor
  - education
  - documentation
  - neovim-config
  - nvim
  - beginners
  - examples
  - cheatsheet

- [ ] **Enable features**
  - [x] Issues
  - [x] Discussions (enable for Q&A and community)
  - [x] Projects (optional)
  - [x] Wiki (optional for additional content)

- [ ] **Set homepage** (if you have one)
  - Optional: Create a GitHub Pages site

### Code Quality

- [x] All example configs have valid Lua syntax
- [x] Configs tested and load without errors
- [x] All internal links verified
- [x] No broken external links (check major ones)
- [ ] Spell check major documents
  - README.md
  - CONTRIBUTING.md
  - docs/00-introduction/README.md

### Documentation

- [x] README.md complete and polished
- [x] CONTRIBUTING.md exists
- [x] LICENSE file present (MIT)
- [x] PROJECT_SUMMARY.md created
- [ ] CHANGELOG.md created (for v1.0.0)
- [x] All modules have README files
- [x] All examples have README files

### Content Verification

- [x] 8 modules complete (00-07)
- [x] 4 example configs ready
- [x] 4 cheatsheets created
- [x] Resources section filled
- [x] GitHub templates created
- [x] All exercises present

## Release Preparation

### Version Tagging

- [ ] **Create CHANGELOG.md** (see template below)
- [ ] **Decide on version number**: v1.0.0
- [ ] **Tag the release**
  ```bash
  git tag -a v1.0.0 -m "Release v1.0.0: Complete Neovim learning resource"
  git push origin v1.0.0
  ```

### Release Notes

- [ ] **Draft release notes on GitHub**
  - Go to Releases → Draft a new release
  - Tag: v1.0.0
  - Title: "Learn Neovim v1.0.0 - Complete Educational Resource"
  - Use release notes template (see below)

### Final Checks

- [ ] All commits pushed to main branch
- [ ] No outstanding critical issues
- [ ] Example configs working
- [ ] README badges correct (if using any)
- [ ] Links to repository updated (if any hardcoded)

## Post-Release (After Publishing)

### Announcements

- [ ] **Reddit - r/neovim**
  - Post announcement (see template)
  - Respond to questions
  - Gather feedback

- [ ] **Reddit - r/vim** (if appropriate)
  - Crosspost or create separate post

- [ ] **Hacker News** (optional)
  - Post: "Show HN: Learn Neovim - Complete Guide from Beginner to Advanced"

- [ ] **Neovim Discourse**
  - Announce in appropriate category
  - https://neovim.discourse.group/

- [ ] **Twitter/X** (if you have account)
  - Announcement tweet
  - Thread highlighting features

### Community Setup

- [ ] **Enable GitHub Discussions**
  - Create categories:
    - Q&A
    - General
    - Ideas
    - Show and tell
  - Pin welcome message

- [ ] **Create Discussion welcome post**
  - Welcome contributors
  - Link to getting started
  - Highlight how to contribute

- [ ] **Monitor issues**
  - Set up notifications
  - Respond to first issues quickly
  - Be welcoming to contributors

### Promotion

- [ ] Add to awesome lists:
  - [ ] [awesome-neovim](https://github.com/rockerBOO/awesome-neovim)
  - [ ] [awesome-vim](https://github.com/akrawchyk/awesome-vim)
  - [ ] [awesome-learning-resources](https://github.com/lauragift21/awesome-learning-resources)

- [ ] Share in communities:
  - [ ] Neovim Matrix/Gitter
  - [ ] Dev.to (write article)
  - [ ] Hashnode (if applicable)

### Maintenance

- [ ] **Set up issue templates** (already done ✓)
- [ ] **Set up PR template** (already done ✓)
- [ ] **Create CODEOWNERS file** (optional)
- [ ] **Set up GitHub Actions** (optional, Priority 3)
  - Link checker
  - Markdown linting
  - Spell checker

## Monitoring (First Week)

### Metrics to Track

- [ ] Stars/forks count
- [ ] Issues opened
- [ ] Questions asked
- [ ] Pull requests submitted
- [ ] Discussion activity

### Community Engagement

- [ ] Respond to all issues within 24 hours
- [ ] Answer questions in discussions
- [ ] Thank contributors
- [ ] Update README if common questions arise

## One Month Later

### Review & Iterate

- [ ] Analyze common questions → update FAQ
- [ ] Identify missing content → create issues
- [ ] Review contributor feedback
- [ ] Plan v1.1.0 features based on feedback
- [ ] Update documentation based on real usage

---

## Templates

### CHANGELOG.md Template

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

## [1.0.0] - 2026-02-26

### Added
- Complete learning path with 8 progressive modules
- 4 production-ready example configurations
- 4 comprehensive cheatsheets (basics, LSP, Lua, plugins)
- GitHub issue and PR templates
- Contribution guidelines
- MIT License
- Comprehensive README and documentation

### Modules
- Module 0: Introduction
- Module 1: Basics
- Module 2: Intermediate
- Module 3: Configuration
- Module 4: Plugin Management
- Module 5: LSP
- Module 6: Advanced
- Module 7: Workflows

### Example Configs
- Minimal (0 plugins, learning focused)
- Basic (14 plugins, general purpose)
- Python Development (17 plugins, Python optimized)
- Web Development (18 plugins, JS/TS/React optimized)

### Resources
- Cheatsheets for quick reference
- Curated articles and videos
- Community links and support channels

[1.0.0]: https://github.com/ocrosby/learn-neovim/releases/tag/v1.0.0
```

### Repository Description

**Short (350 chars for GitHub)**:
```
A comprehensive, step-by-step guide to mastering Neovim. Includes 8 progressive learning modules (15-25 hrs), 4 production-ready configs, LSP setup, plugin management, and advanced workflows. Learn by doing with exercises, examples, and cheatsheets. Build your perfect Neovim setup.
```

**Longer (for README/About)**:
```
Learn Neovim is a complete educational resource for mastering Neovim from absolute beginner to advanced user. Unlike pre-built distributions, this is a structured learning path that teaches you to build your own perfect setup.

What you'll learn:
• Modal editing and Vim motions
• Building init.lua from scratch
• Plugin management with lazy.nvim
• LSP for IDE features
• Lua scripting and automation
• Git workflows and debugging
• Language-specific optimizations

Includes 8 progressive modules, 4 example configurations, comprehensive cheatsheets, and hands-on exercises.
```

---

## Quick Reference

### Typical Release Timeline

**Day 0 (Release Day)**:
- Morning: Final checks, create release
- Afternoon: Post to Reddit, Discourse
- Evening: Monitor feedback, respond to questions

**Days 1-3**:
- Respond to all issues/questions
- Fix any critical bugs
- Thank contributors

**Week 1**:
- Continue monitoring
- Update docs based on feedback
- Start planning v1.1.0

**Month 1**:
- Review metrics
- Major doc updates
- Community building

---

**Ready to release?** Check off items as you complete them! 🚀
