# Testing in Neovim

Run, watch, and manage tests directly from Neovim with neotest and language-specific test runners. Never switch to a terminal.

## neotest

Unified testing framework for Neovim that works with multiple languages.

### Installation

```lua
{
  "nvim-neotest/neotest",
  dependencies = {
    "nvim-neotest/nvim-nio",
    "nvim-lua/plenary.nvim",
    "antoinemadec/FixCursorHold.nvim",
    "nvim-treesitter/nvim-treesitter",
    
    "nvim-neotest/neotest-python",
    "nvim-neotest/neotest-jest",
    "nvim-neotest/neotest-go",
    "rouge8/neotest-rust",
  },
  keys = {
    { "<leader>tn", function() require("neotest").run.run() end, desc = "Run nearest test" },
    { "<leader>tf", function() require("neotest").run.run(vim.fn.expand("%")) end, desc = "Run file" },
    { "<leader>ta", function() require("neotest").run.run(vim.fn.getcwd()) end, desc = "Run all tests" },
    { "<leader>ts", function() require("neotest").summary.toggle() end, desc = "Toggle summary" },
    { "<leader>to", function() require("neotest").output.open({ enter = true }) end, desc = "Show output" },
    { "<leader>tO", function() require("neotest").output_panel.toggle() end, desc = "Toggle output panel" },
    { "<leader>tS", function() require("neotest").run.stop() end, desc = "Stop test" },
  },
  config = function()
    require("neotest").setup({
      adapters = {
        require("neotest-python")({
          dap = { justMyCode = false },
          runner = "pytest",
        }),
        require("neotest-jest")({
          jestCommand = "npm test --",
          env = { CI = true },
          cwd = function()
            return vim.fn.getcwd()
          end,
        }),
        require("neotest-go"),
        require("neotest-rust"),
      },
    })
  end,
}
```

## Language-Specific Setup

### Python (pytest)

Install adapter:
```lua
"nvim-neotest/neotest-python"
```

Configure:
```lua
require("neotest").setup({
  adapters = {
    require("neotest-python")({
      dap = { justMyCode = false },
      runner = "pytest",
      args = { "--log-level", "DEBUG" },
      python = function()
        return vim.fn.exepath("python3")
      end,
    }),
  },
})
```

### JavaScript/TypeScript (Jest)

Install adapter:
```lua
"nvim-neotest/neotest-jest"
```

Configure:
```lua
require("neotest").setup({
  adapters = {
    require("neotest-jest")({
      jestCommand = "npm test --",
      jestConfigFile = "jest.config.js",
      env = { CI = true },
    }),
  },
})
```

### Go

Install adapter:
```lua
"nvim-neotest/neotest-go"
```

Configure:
```lua
require("neotest").setup({
  adapters = {
    require("neotest-go")({
      experimental = {
        test_table = true,
      },
      args = { "-count=1", "-timeout=60s" },
    }),
  },
})
```

### Rust

Install adapter:
```lua
"rouge8/neotest-rust"
```

Configure:
```lua
require("neotest").setup({
  adapters = {
    require("neotest-rust"),
  },
})
```

## Basic Testing Workflow

### Run Tests

1. **Run Nearest Test**
   ```vim
   <leader>tn
   ```
   Runs test under cursor (function or class)

2. **Run Current File**
   ```vim
   <leader>tf
   ```
   Runs all tests in file

3. **Run All Tests**
   ```vim
   <leader>ta
   ```
   Runs entire test suite

### View Results

1. **Test Summary**
   ```vim
   <leader>ts
   ```
   Opens tree view of all tests with status

2. **Test Output**
   ```vim
   <leader>to
   ```
   Shows output of last test

3. **Output Panel**
   ```vim
   <leader>tO
   ```
   Toggle persistent output panel

### Test Navigation

Navigate summary tree:
- `j/k` - Move up/down
- `<CR>` - Jump to test
- `o` - Show output
- `d` - Debug test
- `s` - Stop test
- `r` - Run test

## Test Status Indicators

Tests show status in sign column:

- ✓ - Passed
- ✗ - Failed
- ● - Running
- ◌ - Not run
- ⚠ - Skipped

## Watch Mode

Run tests automatically on file save:

```lua
vim.api.nvim_create_autocmd("BufWritePost", {
  pattern = "*_test.*",
  callback = function()
    require("neotest").run.run(vim.fn.expand("%"))
  end,
})
```

## Debugging Tests

Debug test under cursor:

```lua
vim.keymap.set("n", "<leader>td", function()
  require("neotest").run.run({ strategy = "dap" })
end, { desc = "Debug test" })
```

Requires nvim-dap configuration for your language.

## Coverage

Some adapters support coverage:

```lua
vim.keymap.set("n", "<leader>tc", function()
  require("neotest").run.run({ coverage = true })
end, { desc = "Run with coverage" })
```

## Parameterized Tests

Neotest detects parameterized tests:

**Python**
```python
@pytest.mark.parametrize("input,expected", [
    (1, 2),
    (2, 3),
])
def test_increment(input, expected):
    assert input + 1 == expected
```

Run individual parameter or all:
- Cursor on `@pytest.mark.parametrize` → runs all
- Cursor on specific case → runs that case

## Custom Commands

### Run Last Test

```lua
vim.keymap.set("n", "<leader>tl", function()
  require("neotest").run.run_last()
end, { desc = "Run last test" })
```

### Run Failed Tests

```lua
vim.keymap.set("n", "<leader>tF", function()
  require("neotest").run.run({ status = "failed" })
end, { desc = "Run failed tests" })
```

### Jump to Next/Previous Test

```lua
vim.keymap.set("n", "]t", function()
  require("neotest").jump.next({ status = "failed" })
end, { desc = "Next failed test" })

vim.keymap.set("n", "[t", function()
  require("neotest").jump.prev({ status = "failed" })
end, { desc = "Previous failed test" })
```

## Alternative: vim-test

Simpler test runner without tree view:

```lua
{
  "vim-test/vim-test",
  keys = {
    { "<leader>tn", "<cmd>TestNearest<cr>", desc = "Test nearest" },
    { "<leader>tf", "<cmd>TestFile<cr>", desc = "Test file" },
    { "<leader>ts", "<cmd>TestSuite<cr>", desc = "Test suite" },
    { "<leader>tl", "<cmd>TestLast<cr>", desc = "Test last" },
  },
  config = function()
    vim.g["test#strategy"] = "neovim"
    vim.g["test#neovim#term_position"] = "vert botright 80"
  end,
}
```

**Pros**: Simple, language-agnostic
**Cons**: No tree view, less integration

## Language-Specific Runners

### Python - Run in Terminal

```lua
vim.keymap.set("n", "<leader>tp", function()
  vim.cmd("terminal pytest " .. vim.fn.expand("%"))
end, { desc = "Run pytest" })
```

### JavaScript - Run npm test

```lua
vim.keymap.set("n", "<leader>tj", function()
  vim.cmd("terminal npm test")
end, { desc = "Run npm test" })
```

### Go - Run go test

```lua
vim.keymap.set("n", "<leader>tg", function()
  vim.cmd("terminal go test -v")
end, { desc = "Run go test" })
```

## Test Output Formatting

Customize neotest output:

```lua
require("neotest").setup({
  output = {
    enabled = true,
    open_on_run = "short",
  },
  quickfix = {
    enabled = true,
    open = false,
  },
  summary = {
    enabled = true,
    expand_errors = true,
  },
})
```

## Integration with CI/CD

Run same tests locally as CI:

```lua
vim.keymap.set("n", "<leader>tci", function()
  vim.cmd("terminal npm run test:ci")
end, { desc = "Run CI tests" })
```

## Complete Configuration Example

```lua
return {
  {
    "nvim-neotest/neotest",
    dependencies = {
      "nvim-neotest/nvim-nio",
      "nvim-lua/plenary.nvim",
      "nvim-treesitter/nvim-treesitter",
      "nvim-neotest/neotest-python",
      "nvim-neotest/neotest-jest",
    },
    keys = {
      { "<leader>tn", function() require("neotest").run.run() end },
      { "<leader>tf", function() require("neotest").run.run(vim.fn.expand("%")) end },
      { "<leader>ta", function() require("neotest").run.run(vim.fn.getcwd()) end },
      { "<leader>ts", function() require("neotest").summary.toggle() end },
      { "<leader>to", function() require("neotest").output.open({ enter = true }) end },
      { "<leader>td", function() require("neotest").run.run({ strategy = "dap" }) end },
      { "]t", function() require("neotest").jump.next({ status = "failed" }) end },
      { "[t", function() require("neotest").jump.prev({ status = "failed" }) end },
    },
    config = function()
      require("neotest").setup({
        adapters = {
          require("neotest-python")({
            runner = "pytest",
          }),
          require("neotest-jest"),
        },
      })
    end,
  },
}
```

## Keybinding Reference

| Key | Action |
|-----|--------|
| `<leader>tn` | Run nearest test |
| `<leader>tf` | Run file tests |
| `<leader>ta` | Run all tests |
| `<leader>tl` | Run last test |
| `<leader>ts` | Toggle summary |
| `<leader>to` | Show output |
| `<leader>td` | Debug test |
| `]t` | Next failed test |
| `[t` | Previous failed test |

## Best Practices

1. **Run tests frequently** - Fast feedback loop
2. **Use watch mode** - Auto-run on save
3. **Debug failing tests** - Use `<leader>td` for tricky failures
4. **Organize tests** - Keep test files next to source
5. **Name tests clearly** - Descriptive test names
6. **Use parameterized tests** - Reduce duplication
7. **Check coverage** - Ensure code is tested

## Troubleshooting

### Tests Not Detected

- Check treesitter parser installed: `:TSInstall python`
- Verify test file naming (e.g., `test_*.py`, `*.test.js`)
- Check adapter configuration

### Tests Fail in Neovim but Pass in Terminal

- Check working directory
- Verify environment variables
- Check Python virtual environment

### Slow Test Runs

- Run specific tests, not entire suite
- Use test markers/tags to filter
- Parallelize tests if framework supports

## Exercises

1. **Install neotest** - Set up neotest for your language
2. **Run tests** - Execute tests at different scopes
3. **View summary** - Explore the test summary tree
4. **Debug test** - Debug a failing test with dap
5. **Watch mode** - Set up auto-run on save

## Next Steps

Continue to [Project-Specific Configuration](project-specific.md) to learn how to customize Neovim per project.

## Resources

- [neotest](https://github.com/nvim-neotest/neotest)
- [neotest-python](https://github.com/nvim-neotest/neotest-python)
- [neotest-jest](https://github.com/nvim-neotest/neotest-jest)
- [neotest-go](https://github.com/nvim-neotest/neotest-go)
- [vim-test](https://github.com/vim-test/vim-test)
