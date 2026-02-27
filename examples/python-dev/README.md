# Python Development Configuration

A complete Neovim setup optimized for Python development with testing (pytest), debugging (DAP), linting, formatting, and virtual environment management.

## Features

### Python-Specific
- ✅ **pyright**: Advanced type checking and IntelliSense
- ✅ **ruff**: Fast linting (replaces flake8, pylint, isort)
- ✅ **pytest integration**: Run tests from Neovim (neotest)
- ✅ **Debugging**: Full DAP debugger with breakpoints
- ✅ **Virtual env**: Auto-detect and switch environments
- ✅ **Format on save**: Auto-format with Black (via ruff)
- ✅ **PEP 8**: 88-character line indicator (Black default)

### Development Tools
- Telescope fuzzy finder
- File explorer with Python-specific filters
- Git integration
- Treesitter syntax highlighting
- Autocompletion with type hints
- TODO search

## Prerequisites

### Required
- Neovim >= 0.9.0
- Python >= 3.8
- Git
- ripgrep (`brew install ripgrep` or `apt install ripgrep`)

### Recommended
- A Nerd Font for icons
- pyenv or virtualenv for environment management
- pytest for testing

### Python Tools (Auto-installed via Mason)
- pyright (LSP)
- ruff (linter/formatter)
- debugpy (debugger)

## Installation

### Quick Start

```bash
# Try without installing
nvim -u examples/python-dev/init.lua your_script.py

# Or install permanently
cp examples/python-dev/init.lua ~/.config/nvim/init.lua
nvim
```

### Full Setup

1. **Backup existing config**:
   ```bash
   mv ~/.config/nvim ~/.config/nvim.backup
   mv ~/.local/share/nvim ~/.local/share/nvim.backup
   ```

2. **Install config**:
   ```bash
   mkdir -p ~/.config/nvim
   cp examples/python-dev/init.lua ~/.config/nvim/init.lua
   ```

3. **First launch**:
   ```bash
   nvim
   ```
   Wait for plugins and LSP servers to install (~2 minutes).

4. **Verify installation**:
   ```bash
   # Check LSP servers
   :Mason
   
   # Should see: pyright, ruff_lsp, debugpy
   
   # Check health
   :checkhealth
   ```

## Python Workflow

### 1. Project Setup

```bash
cd my-python-project

python -m venv .venv

source .venv/bin/activate

pip install pytest black ruff

nvim
```

### 2. Select Virtual Environment

In Neovim:
```vim
<leader>vs    " Opens virtual environment selector
```

Choose your `.venv` or `venv` folder.

### 3. Start Coding

Open a Python file:
```bash
nvim main.py
```

You'll immediately get:
- Type checking from pyright
- Linting from ruff
- Autocompletion with type hints
- Go-to-definition (gd)
- Hover docs (K)

### 4. Run Your Code

| Key | Action |
|-----|--------|
| `<leader>r` | Run current file |
| `:terminal python %` | Run in terminal split |

### 5. Testing

Write tests following pytest conventions:

```python
# test_example.py
def test_addition():
    assert 1 + 1 == 2
```

Run tests:

| Key | Action |
|-----|--------|
| `<leader>tn` | Run test under cursor |
| `<leader>tf` | Run all tests in file |
| `<leader>ta` | Run entire test suite |
| `<leader>ts` | Toggle test summary |
| `<leader>to` | Show test output |

Navigate test results:
- Use summary tree to see pass/fail
- Jump to test with `<CR>`
- Re-run with `r`

### 6. Debugging

Set breakpoints and debug:

| Key | Action |
|-----|--------|
| `<leader>db` | Toggle breakpoint |
| `<leader>dc` | Start/continue debugging |
| `<leader>di` | Step into function |
| `<leader>do` | Step over line |
| `<leader>du` | Toggle debugger UI |

Example workflow:
1. Open file: `nvim script.py`
2. Set breakpoint: `<leader>db` on desired line
3. Start debugger: `<leader>dc`
4. Inspect variables in DAP UI
5. Step through code: `<leader>do`

## Keybindings

### Python-Specific

| Key | Action |
|-----|--------|
| `<leader>r` | Run current Python file |
| `<leader>tt` | Run all pytest tests |
| `<leader>tf` | Run tests in current file |
| `<leader>vs` | Select virtual environment |

### Testing (Neotest)

| Key | Action |
|-----|--------|
| `<leader>tn` | Run nearest test |
| `<leader>tf` | Run file tests |
| `<leader>ta` | Run all tests |
| `<leader>ts` | Test summary |
| `<leader>to` | Test output |

### Debugging (DAP)

| Key | Action |
|-----|--------|
| `<leader>db` | Toggle breakpoint |
| `<leader>dc` | Continue/Start |
| `<leader>di` | Step into |
| `<leader>do` | Step over |
| `<leader>du` | Toggle UI |

### LSP

| Key | Action |
|-----|--------|
| `gd` | Go to definition |
| `gr` | Find references |
| `K` | Hover documentation |
| `<leader>vrn` | Rename symbol |
| `<leader>vca` | Code actions |
| `[d` | Previous diagnostic |
| `]d` | Next diagnostic |

### File Navigation

| Key | Action |
|-----|--------|
| `<leader>ff` | Find files |
| `<leader>fg` | Live grep |
| `<leader>ft` | Find TODOs |
| `<leader>e` | File explorer |

## Python Best Practices

### Type Hints

pyright works best with type hints:

```python
def greet(name: str) -> str:
    return f"Hello, {name}"

# Get completions and type checking
result: str = greet("World")
```

### Testing Structure

```
my_project/
├── src/
│   └── my_module.py
├── tests/
│   ├── __init__.py
│   └── test_my_module.py
├── .venv/
├── requirements.txt
└── pyproject.toml
```

### Format on Save

Files auto-format when you save (`:w`). To disable:

Remove this autocommand from init.lua:
```lua
vim.api.nvim_create_autocmd("BufWritePre", {
  pattern = "*.py",
  callback = function()
    vim.lsp.buf.format({ async = false })
  end,
})
```

### Line Length

Default is 88 characters (Black standard):

```lua
vim.opt.colorcolumn = "88"  -- Visual guide
```

Change to 79 (PEP 8):
```lua
vim.opt.colorcolumn = "79"
```

## Virtual Environment

### Auto-Detection

The config auto-detects these folders:
- `.venv`
- `venv`
- `.env`
- `env`

### Manual Selection

```vim
:VenvSelect
```

Choose from detected environments or browse manually.

### Indicator

Current venv shows in status line (lualine).

## Common Workflows

### Django Project

```bash
cd my_django_project
python -m venv .venv
source .venv/bin/activate
pip install django pytest-django
nvim
```

In Neovim:
1. Select venv: `<leader>vs`
2. Navigate: `<leader>ff` to find views.py
3. Edit with LSP support
4. Run: `<leader>r` or `:terminal python manage.py runserver`

### Data Science

```bash
cd my_notebook
python -m venv .venv
source .venv/bin/activate
pip install numpy pandas matplotlib
nvim analysis.py
```

Get completions for pandas/numpy with type stubs:
```bash
pip install types-pandas types-numpy
```

### Testing TDD

1. Write test first: `test_feature.py`
2. Run test: `<leader>tn` (should fail)
3. Implement feature: `feature.py`
4. Run test: `<leader>tn` (should pass)
5. Refactor with confidence

## Troubleshooting

### LSP Not Working

```vim
:LspInfo
```

Should show pyright attached. If not:
1. Check venv is activated
2. Restart LSP: `:LspRestart`
3. Check Mason: `:Mason`

### Tests Not Found

1. Ensure pytest is installed in venv
2. Check test file naming: `test_*.py` or `*_test.py`
3. Check test function naming: `def test_*()`
4. Verify treesitter: `:TSInstall python`

### Debugger Not Starting

1. Ensure debugpy is installed: `pip install debugpy`
2. Check DAP config: `:lua print(vim.inspect(require("dap").configurations.python))`
3. Try manually: `:lua require("dap").continue()`

### Virtual Env Not Detected

1. Check folder exists: `.venv`, `venv`, etc.
2. Manually select: `<leader>vs`
3. Check status line for indicator

### Format Not Working

1. Ensure ruff is running: `:LspInfo`
2. Manual format: `:lua vim.lsp.buf.format()`
3. Check ruff is installed: `:Mason`

## Customization

### Change Formatter

Use Black directly instead of ruff:

1. Install: `pip install black`
2. Install black via Mason: `:MasonInstall black`
3. Update autocommand:
   ```lua
   vim.api.nvim_create_autocmd("BufWritePre", {
     pattern = "*.py",
     callback = function()
       vim.fn.system("black " .. vim.fn.expand("%"))
       vim.cmd("edit!")
     end,
   })
   ```

### Add More Linters

Install additional linters:
```vim
:MasonInstall mypy pylint
```

### Custom Test Runner

Change pytest arguments in neotest config:
```lua
require("neotest-python")({
  runner = "pytest",
  args = { "-v", "--tb=short", "-x", "--maxfail=1" },
})
```

## Example Project

Try this config with a sample project:

```python
# calculator.py
def add(a: int, b: int) -> int:
    """Add two numbers."""
    return a + b

def subtract(a: int, b: int) -> int:
    """Subtract b from a."""
    return a - b

# test_calculator.py
from calculator import add, subtract

def test_add():
    assert add(2, 3) == 5
    assert add(-1, 1) == 0

def test_subtract():
    assert subtract(5, 3) == 2
    assert subtract(0, 5) == -5
```

Try:
1. Open: `nvim calculator.py`
2. Hover over `add`: Press `K`
3. Run tests: `<leader>ta`
4. Set breakpoint in `add`: `<leader>db`
5. Debug test: Switch to test file, `<leader>dc`

## Resources

- [pytest docs](https://docs.pytest.org/)
- [pyright docs](https://github.com/microsoft/pyright)
- [ruff docs](https://docs.astral.sh/ruff/)
- [Python type hints](https://docs.python.org/3/library/typing.html)
- [neotest-python](https://github.com/nvim-neotest/neotest-python)

## Next Steps

1. Learn pytest fixtures and parameterization
2. Add coverage reporting
3. Set up pre-commit hooks
4. Explore Django/Flask-specific plugins
5. Add AI code completion (copilot.vim, codeium, etc.)

---

Happy Python coding! 🐍
