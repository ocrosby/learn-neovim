# Project-Specific Configuration

Learn how to customize Neovim settings per project using `.nvim.lua`, exrc, and directory-specific configurations.

## Why Project-Specific Config?

Different projects have different needs:
- **Code style** - Tabs vs spaces, indent size
- **Language servers** - Different LSP settings
- **Build commands** - Project-specific tasks
- **Environment** - Virtual envs, node versions
- **Team conventions** - Shared settings

## Methods

### 1. Local .nvim.lua (Recommended)

Create `.nvim.lua` in project root:

**Enable in your config:**
```lua
vim.opt.exrc = true
vim.opt.secure = true
```

**Example `.nvim.lua`:**
```lua
vim.opt_local.tabstop = 2
vim.opt_local.shiftwidth = 2
vim.opt_local.expandtab = true

vim.keymap.set("n", "<leader>r", ":!npm run dev<CR>", { buffer = true })

require("lspconfig").ts_ls.setup({
  settings = {
    typescript = {
      format = {
        indentSize = 2,
      },
    },
  },
})
```

**Security Note**: Only load `.nvim.lua` for projects you trust.

### 2. Per-Directory Autocommands

Automatically apply settings for specific paths:

```lua
vim.api.nvim_create_autocmd("BufEnter", {
  pattern = "/path/to/project/*",
  callback = function()
    vim.opt_local.tabstop = 2
    vim.opt_local.shiftwidth = 2
  end,
})
```

### 3. EditorConfig

Use `.editorconfig` for basic settings:

Install plugin:
```lua
{
  "editorconfig/editorconfig-vim",
}
```

**Example `.editorconfig`:**
```ini
root = true

[*]
charset = utf-8
end_of_line = lf
insert_final_newline = true
trim_trailing_whitespace = true

[*.py]
indent_style = space
indent_size = 4

[*.js]
indent_style = space
indent_size = 2

[Makefile]
indent_style = tab
```

### 4. Project.nvim

Automatic project detection:

```lua
{
  "ahmedkhalf/project.nvim",
  config = function()
    require("project_nvim").setup({
      detection_methods = { "pattern", "lsp" },
      patterns = { ".git", "package.json", "Cargo.toml", "go.mod" },
    })
  end,
}
```

Automatically changes directory to project root.

## Common Project Configurations

### Python Project

**.nvim.lua**
```lua
vim.opt_local.tabstop = 4
vim.opt_local.shiftwidth = 4
vim.opt_local.expandtab = true

vim.env.PYTHONPATH = vim.fn.getcwd()

vim.keymap.set("n", "<leader>r", function()
  vim.cmd("terminal python -m main")
end, { buffer = true, desc = "Run main" })

vim.keymap.set("n", "<leader>t", function()
  vim.cmd("terminal pytest -v")
end, { buffer = true, desc = "Run tests" })

require("lspconfig").pyright.setup({
  settings = {
    python = {
      venvPath = vim.fn.getcwd() .. "/venv",
      pythonPath = vim.fn.getcwd() .. "/venv/bin/python",
    },
  },
})
```

### JavaScript/TypeScript Project

**.nvim.lua**
```lua
vim.opt_local.tabstop = 2
vim.opt_local.shiftwidth = 2
vim.opt_local.expandtab = true

vim.keymap.set("n", "<leader>r", ":!npm run dev<CR>", { buffer = true })
vim.keymap.set("n", "<leader>b", ":!npm run build<CR>", { buffer = true })
vim.keymap.set("n", "<leader>t", ":!npm test<CR>", { buffer = true })

require("lspconfig").ts_ls.setup({
  init_options = {
    preferences = {
      importModuleSpecifierPreference = "relative",
    },
  },
})
```

### Go Project

**.nvim.lua**
```lua
vim.opt_local.tabstop = 4
vim.opt_local.shiftwidth = 4
vim.opt_local.expandtab = false

vim.keymap.set("n", "<leader>r", ":!go run .<CR>", { buffer = true })
vim.keymap.set("n", "<leader>b", ":!go build<CR>", { buffer = true })
vim.keymap.set("n", "<leader>t", ":!go test -v ./...<CR>", { buffer = true })

vim.api.nvim_create_autocmd("BufWritePre", {
  pattern = "*.go",
  callback = function()
    local params = vim.lsp.util.make_range_params()
    params.context = { only = { "source.organizeImports" } }
    local result = vim.lsp.buf_request_sync(0, "textDocument/codeAction", params)
    for _, res in pairs(result or {}) do
      for _, r in pairs(res.result or {}) do
        if r.edit then
          vim.lsp.util.apply_workspace_edit(r.edit, "utf-8")
        end
      end
    end
    vim.lsp.buf.format()
  end,
})
```

### Rust Project

**.nvim.lua**
```lua
vim.opt_local.tabstop = 4
vim.opt_local.shiftwidth = 4
vim.opt_local.expandtab = true

vim.keymap.set("n", "<leader>r", ":!cargo run<CR>", { buffer = true })
vim.keymap.set("n", "<leader>b", ":!cargo build<CR>", { buffer = true })
vim.keymap.set("n", "<leader>t", ":!cargo test<CR>", { buffer = true })
vim.keymap.set("n", "<leader>c", ":!cargo clippy<CR>", { buffer = true })

require("lspconfig").rust_analyzer.setup({
  settings = {
    ["rust-analyzer"] = {
      cargo = {
        allFeatures = true,
      },
    },
  },
})
```

## Environment-Specific Settings

### Virtual Environments (Python)

Auto-detect and activate venv:

```lua
local function setup_python_venv()
  local venv = vim.fn.finddir("venv", vim.fn.getcwd() .. ";")
  if venv ~= "" then
    vim.env.VIRTUAL_ENV = venv
    vim.env.PATH = venv .. "/bin:" .. vim.env.PATH
    vim.notify("Activated venv: " .. venv, vim.log.levels.INFO)
  end
end

vim.api.nvim_create_autocmd("VimEnter", {
  pattern = "*.py",
  callback = setup_python_venv,
})
```

### Node Version (JavaScript)

Use project's Node version:

```lua
local function setup_node_version()
  local nvmrc = vim.fn.findfile(".nvmrc", vim.fn.getcwd() .. ";")
  if nvmrc ~= "" then
    vim.notify("Found .nvmrc, run: nvm use", vim.log.levels.INFO)
  end
end
```

## Build/Task Commands

### Custom Task Runner

```lua
local M = {}

function M.run_task(name)
  local tasks = {
    dev = "npm run dev",
    build = "npm run build",
    test = "npm test",
    lint = "npm run lint",
  }
  
  local cmd = tasks[name]
  if cmd then
    vim.cmd("terminal " .. cmd)
  else
    vim.notify("Task not found: " .. name, vim.log.levels.ERROR)
  end
end

vim.keymap.set("n", "<leader>tr", function()
  vim.ui.select({ "dev", "build", "test", "lint" }, {
    prompt = "Select task:",
  }, function(choice)
    if choice then
      M.run_task(choice)
    end
  end)
end, { desc = "Run task" })

return M
```

### Package.json Scripts

Run npm scripts interactively:

```lua
local function run_npm_script()
  local package_json = vim.fn.findfile("package.json", vim.fn.getcwd() .. ";")
  if package_json == "" then
    vim.notify("No package.json found", vim.log.levels.ERROR)
    return
  end
  
  local scripts = vim.fn.json_decode(vim.fn.readfile(package_json)).scripts
  local script_names = vim.tbl_keys(scripts)
  
  vim.ui.select(script_names, {
    prompt = "Select script:",
  }, function(choice)
    if choice then
      vim.cmd("terminal npm run " .. choice)
    end
  end)
end

vim.keymap.set("n", "<leader>ns", run_npm_script, { desc = "Run npm script" })
```

## Project Templates

### Create Project Template Function

```lua
local function init_project(type)
  local templates = {
    python = {
      files = {
        ["main.py"] = "def main():\n    pass\n\nif __name__ == '__main__':\n    main()\n",
        [".nvim.lua"] = "vim.opt_local.tabstop = 4\nvim.opt_local.shiftwidth = 4\n",
      },
      commands = { "python -m venv venv" },
    },
    node = {
      files = {
        ["index.js"] = "console.log('Hello, World!');\n",
        ["package.json"] = '{\n  "name": "project",\n  "version": "1.0.0"\n}\n',
      },
      commands = { "npm install" },
    },
  }
  
  local template = templates[type]
  if not template then
    vim.notify("Unknown template: " .. type, vim.log.levels.ERROR)
    return
  end
  
  for file, content in pairs(template.files) do
    vim.fn.writefile(vim.split(content, "\n"), file)
  end
  
  for _, cmd in ipairs(template.commands) do
    vim.fn.system(cmd)
  end
  
  vim.notify("Project initialized: " .. type, vim.log.levels.INFO)
end

vim.api.nvim_create_user_command("InitProject", function(opts)
  init_project(opts.args)
end, { nargs = 1, complete = function() return { "python", "node" } end })
```

## Sharing Configurations

### Team Setup

Create `.nvim.lua` in project root and commit to Git:

**.nvim.lua**
```lua
vim.opt_local.tabstop = 2
vim.opt_local.shiftwidth = 2
vim.opt_local.expandtab = true

vim.notify("Loaded team Neovim config", vim.log.levels.INFO)
```

**Add to README:**
```markdown
## Neovim Setup

Enable project-specific config:
```lua
vim.opt.exrc = true
```

### Optional Features

Allow but don't require:

```lua
pcall(function()
  require("project-specific-plugin")
end)
```

## Security

### Safe Loading

Only load trusted project configs:

```lua
vim.opt.exrc = true
vim.opt.secure = true
```

`secure` prevents:
- Writing files
- Using shell commands
- Defining autocommands with shell commands

### Whitelist Projects

```lua
local trusted_projects = {
  "/home/user/projects/my-project",
  "/home/user/work/company-project",
}

vim.api.nvim_create_autocmd("VimEnter", {
  callback = function()
    local cwd = vim.fn.getcwd()
    if vim.tbl_contains(trusted_projects, cwd) then
      vim.opt.exrc = true
    end
  end,
})
```

## Best Practices

1. **Commit .nvim.lua** - Share with team
2. **Keep it simple** - Only project-specific settings
3. **Document** - Add comments explaining choices
4. **Use editorconfig** - For basic formatting
5. **Test thoroughly** - Ensure it works for all team members
6. **Avoid secrets** - Don't put API keys in .nvim.lua

## Complete Example

**.nvim.lua for a TypeScript React project:**
```lua
vim.opt_local.tabstop = 2
vim.opt_local.shiftwidth = 2
vim.opt_local.expandtab = true

local keymap_opts = { buffer = true, silent = true }

vim.keymap.set("n", "<leader>r", ":!npm run dev<CR>", keymap_opts)
vim.keymap.set("n", "<leader>b", ":!npm run build<CR>", keymap_opts)
vim.keymap.set("n", "<leader>t", ":!npm test<CR>", keymap_opts)
vim.keymap.set("n", "<leader>l", ":!npm run lint<CR>", keymap_opts)

require("lspconfig").ts_ls.setup({
  settings = {
    typescript = {
      format = {
        indentSize = 2,
      },
      preferences = {
        importModuleSpecifierPreference = "relative",
      },
    },
  },
})

vim.api.nvim_create_autocmd("BufWritePre", {
  buffer = 0,
  callback = function()
    vim.lsp.buf.format({ async = false })
  end,
})

vim.notify("Loaded React project config", vim.log.levels.INFO)
```

## Exercises

1. **Create .nvim.lua** - Add project-specific config to current project
2. **Team settings** - Set up shared formatting rules
3. **Task runner** - Create custom build/test commands
4. **Environment setup** - Auto-detect and configure environment
5. **Template** - Create a project template function

## Completion

Congratulations! You've completed all modules. You now have:
- ✅ Vim fundamentals
- ✅ Custom configuration
- ✅ Plugin management
- ✅ LSP integration
- ✅ Advanced Lua scripting
- ✅ Complete development workflows

## Next Steps

- **Practice daily** - Use Neovim for all editing
- **Customize further** - Tailor to your workflow
- **Explore plugins** - Discover new plugins
- **Join community** - Reddit, Discord, GitHub
- **Share knowledge** - Help others learn

## Resources

- [EditorConfig](https://editorconfig.org/)
- [project.nvim](https://github.com/ahmedkhalf/project.nvim)
- [Neovim exrc docs](https://neovim.io/doc/user/options.html#'exrc')
