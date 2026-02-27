# Web Development Configuration

Complete Neovim setup optimized for modern web development with JavaScript, TypeScript, React, Vue, HTML, and CSS.

## Features

### Language Support
- ✅ **TypeScript/JavaScript**: Advanced type checking and IntelliSense
- ✅ **React/JSX**: Component intelligence and auto-closing tags
- ✅ **HTML/CSS**: Emmet abbreviations and autocompletion
- ✅ **Tailwind CSS**: Class name completions
- ✅ **JSON/YAML**: Configuration file support

### Development Tools
- ✅ **ESLint**: Real-time linting
- ✅ **Prettier**: Format on save (via LSP)
- ✅ **Jest/Vitest**: Test runner integration
- ✅ **Auto-close tags**: HTML/JSX tag completion
- ✅ **npm scripts**: Quick access to package.json scripts
- ✅ **Project detection**: Shows project name in statusline

### Editor Features
- Fuzzy file finding (Telescope)
- Git integration (gitsigns)
- Syntax highlighting (Treesitter)
- File explorer with filters
- Auto-pairs for brackets and quotes

## Prerequisites

### Required
- Neovim >= 0.9.0
- Node.js >= 16
- npm or yarn
- Git
- ripgrep

### Recommended
- A Nerd Font
- Prettier installed globally (`npm i -g prettier`)
- ESLint configured in your projects

## Installation

### Quick Start

```bash
# Try without installing
cd your-web-project
nvim -u /path/to/examples/web-dev/init.lua

# Or install permanently
cp examples/web-dev/init.lua ~/.config/nvim/init.lua
nvim
```

### Full Installation

1. **Backup existing config**:
   ```bash
   mv ~/.config/nvim ~/.config/nvim.backup
   mv ~/.local/share/nvim ~/.local/share/nvim.backup
   ```

2. **Install**:
   ```bash
   mkdir -p ~/.config/nvim
   cp examples/web-dev/init.lua ~/.config/nvim/init.lua
   ```

3. **First launch**:
   ```bash
   cd your-web-project
   nvim
   ```
   
   Plugins and LSP servers will auto-install (~2 minutes).

4. **Verify**:
   ```vim
   :Mason          " Check LSP servers installed
   :checkhealth    " Verify setup
   ```

## Web Development Workflow

### 1. Start a Project

```bash
# React with Vite
npm create vite@latest my-app -- --template react-ts
cd my-app
npm install
nvim
```

Or with existing project:
```bash
cd my-existing-project
nvim
```

### 2. File Navigation

| Key | Action |
|-----|--------|
| `<leader>ff` | Find files (ignores node_modules) |
| `<leader>fg` | Search in files |
| `<leader>fb` | List open buffers |
| `<leader>fc` | Find TODOs/FIXMEs |
| `<leader>e` | Toggle file tree |

### 3. Editing Features

#### Auto-close Tags
Type `<div>` and it auto-completes to `<div></div>` with cursor in middle.

#### Emmet Abbreviations
In HTML/JSX files:
```
div.container>ul>li*3    →  <div class="container"><ul><li></li><li></li><li></li></ul></div>
```

Type the abbreviation and press `<C-y>,`

#### Tailwind Completions
Start typing class names:
```jsx
<div className="flex items-c...
              ↓ (shows completions)
         items-center
```

### 4. LSP Features

| Key | Action | Example |
|-----|--------|---------|
| `gd` | Go to definition | Jump to function/component definition |
| `gr` | Find references | See where component is used |
| `K` | Hover docs | See TypeScript type info |
| `<leader>vrn` | Rename | Rename variable across project |
| `<leader>vca` | Code actions | Quick fixes, imports |
| `[d` / `]d` | Navigate diagnostics | Jump to errors/warnings |

#### Example: Import a Component

```typescript
// cursor on ComponentName
<ComponentName />  // Error: not imported

// Press <leader>vca (code action)
// Select: "Add import from './ComponentName'"
```

### 5. Running npm Scripts

| Key | Action |
|-----|--------|
| `<leader>nd` | npm run dev |
| `<leader>nb` | npm run build |
| `<leader>nt` | npm test |

Or run any script:
```vim
:terminal npm run lint
:terminal npm run storybook
```

### 6. Testing

Write tests following Jest/Vitest conventions:

```typescript
// MyComponent.test.tsx
describe('MyComponent', () => {
  it('renders correctly', () => {
    // test code
  });
});
```

Run tests:
| Key | Action |
|-----|--------|
| `<leader>tn` | Run test under cursor |
| `<leader>tf` | Run all tests in file |
| `<leader>ts` | Toggle test summary |

### 7. Linting & Formatting

**Auto-format on save** for:
- `.js`, `.jsx`
- `.ts`, `.tsx`
- `.json`
- `.css`, `.html`

Manual format:
```vim
:lua vim.lsp.buf.format()
```

ESLint runs automatically, showing errors/warnings inline.

## Keybindings

### npm/Development

| Key | Action |
|-----|--------|
| `<leader>nd` | npm run dev |
| `<leader>nb` | npm run build |
| `<leader>nt` | npm test |

### File Navigation

| Key | Action |
|-----|--------|
| `<leader>ff` | Find files |
| `<leader>fg` | Live grep |
| `<leader>fb` | Buffers |
| `<leader>fc` | Find TODOs |
| `<leader>e` | File tree |

### LSP

| Key | Action |
|-----|--------|
| `gd` | Go to definition |
| `gr` | References |
| `K` | Hover docs |
| `<leader>vrn` | Rename |
| `<leader>vca` | Code actions |
| `[d` / `]d` | Diagnostics |

### Testing

| Key | Action |
|-----|--------|
| `<leader>tn` | Run nearest test |
| `<leader>tf` | Run file tests |
| `<leader>ts` | Test summary |

### General

| Key | Action |
|-----|--------|
| `<leader>w` | Save |
| `Shift-h/l` | Previous/next buffer |
| `Ctrl-h/j/k/l` | Navigate windows |
| `gcc` | Comment line |
| `jk` | Exit insert mode |

## Framework-Specific Tips

### React

**Component intelligence**:
```tsx
// Get prop completions
<MyComponent prop↓   // Shows available props with types
```

**Import auto-complete**:
```tsx
import { useState↓ } from 'react'  // Auto-completes hooks
```

**JSX formatting**:
- Auto-indents JSX
- Auto-closes tags: `<div>` → `<div></div>`

### Vue

Add Vue support:

In Mason (`:Mason`), install:
- `vue-language-server` (Volar)

Add to LSP config:
```lua
lspconfig.volar.setup({
  capabilities = capabilities,
  on_attach = on_attach,
})
```

### Next.js

Works out of the box! Features:
- API route completions
- App router support
- TypeScript integration

### Tailwind CSS

Requires `tailwind.config.js` in project root.

Get completions in:
- `className="..."`
- `class="..."`
- `@apply ...` in CSS

## Project Structure

Typical project layout:

```
my-web-app/
├── node_modules/       # Ignored by Telescope
├── src/
│   ├── components/
│   ├── pages/
│   ├── utils/
│   └── App.tsx
├── public/
├── package.json
├── tsconfig.json       # TypeScript config
├── .eslintrc.json      # ESLint config
└── tailwind.config.js  # Tailwind config
```

## Common Workflows

### Component Development

1. Create file: `nvim src/components/Button.tsx`
2. Type Emmet: `div.button`
3. Press `<C-y>,` for expansion
4. Add props with TypeScript:
   ```tsx
   interface ButtonProps {
     label: string;
     onClick: () => void;
   }
   ```
5. Get autocompletion for props

### Debugging TypeScript Errors

1. See error inline (red underline)
2. Press `K` on error for details
3. Press `<leader>vca` for quick fixes
4. Navigate errors: `]d` (next), `[d` (prev)

### Adding Dependencies

```bash
npm install axios
```

In code:
```typescript
import axios from 'axios'  // Get completions!
axios.↓                     // See available methods
```

### Refactoring

1. Place cursor on symbol
2. Press `<leader>vrn` (rename)
3. Type new name
4. Press Enter
5. Updates across entire project!

## Troubleshooting

### TypeScript Server Slow

Large projects may be slow. Solutions:

1. Exclude files in `tsconfig.json`:
   ```json
   {
     "exclude": ["node_modules", "dist", "build"]
   }
   ```

2. Restart LSP: `:LspRestart`

### Tailwind Completions Not Working

1. Ensure `tailwind.config.js` exists
2. Check LSP attached: `:LspInfo`
3. Restart: `:LspRestart tailwindcss`

### ESLint Not Showing Errors

1. Ensure `.eslintrc.json` exists
2. Install ESLint: `npm install eslint`
3. Check Mason: `:Mason` → ensure `eslint` installed

### Format Not Working

1. Check LSP is running: `:LspInfo`
2. Manual format: `:lua vim.lsp.buf.format()`
3. Install Prettier: `npm install -D prettier`

### Node Modules in Search Results

Should be automatically filtered. If not, update Telescope:
```lua
file_ignore_patterns = { "node_modules", ".git/" }
```

## Customization

### Use Prettier Directly

Instead of LSP formatting:

```lua
vim.api.nvim_create_autocmd("BufWritePre", {
  pattern = { "*.js", "*.jsx", "*.ts", "*.tsx" },
  callback = function()
    vim.fn.system("prettier --write " .. vim.fn.expand("%"))
    vim.cmd("edit!")
  end,
})
```

### Change Indentation

4 spaces instead of 2:
```lua
vim.opt.tabstop = 4
vim.opt.shiftwidth = 4
```

### Add Svelte Support

In `:Mason`, install `svelte-language-server`

Add to LSP config:
```lua
lspconfig.svelte.setup({ capabilities = capabilities, on_attach = on_attach })
```

### Add GraphQL Support

Install via Mason: `graphql-language-service-cli`

## Example Files

### React Component (TypeScript)

```tsx
// Button.tsx
interface ButtonProps {
  label: string;
  variant?: 'primary' | 'secondary';
  onClick: () => void;
}

export function Button({ label, variant = 'primary', onClick }: ButtonProps) {
  return (
    <button 
      className={`btn btn-${variant}`}
      onClick={onClick}
    >
      {label}
    </button>
  );
}
```

Try in Neovim:
1. `gd` on `ButtonProps` → jump to interface
2. `K` on `variant` → see type info
3. `<leader>vrn` on `onClick` → rename everywhere

### API Route (Next.js)

```typescript
// pages/api/users.ts
import type { NextApiRequest, NextApiResponse } from 'next'

export default async function handler(
  req: NextApiRequest,
  res: NextApiResponse
) {
  const users = await fetchUsers()
  res.status(200).json(users)
}
```

Get completions for Next.js types!

## Resources

- [TypeScript docs](https://www.typescriptlang.org/docs/)
- [React docs](https://react.dev/)
- [Tailwind docs](https://tailwindcss.com/docs)
- [ESLint docs](https://eslint.org/docs/latest/)
- [Prettier docs](https://prettier.io/docs/en/)

## Next Steps

1. Add debugging with nvim-dap-chrome
2. Set up snippet library
3. Add AI code completion (GitHub Copilot)
4. Explore React-specific plugins
5. Set up pre-commit hooks with Husky

---

Happy web coding! 🌐
