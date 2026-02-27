# Installing Neovim

This guide covers installing Neovim on macOS, Linux, and Windows.

## Version Requirements

For this learning resource, we recommend **Neovim 0.9.0 or later**. Many modern features (LSP, TreeSitter) require recent versions.

Check the [official releases](https://github.com/neovim/neovim/releases) for the latest stable version.

## Installation by Platform

### macOS

**Homebrew (Recommended)**:
```bash
brew install neovim
```

**MacPorts**:
```bash
sudo port install neovim
```

**From Source**:
```bash
git clone https://github.com/neovim/neovim.git
cd neovim
make CMAKE_BUILD_TYPE=Release
sudo make install
```

### Linux

**Ubuntu/Debian**:
```bash
sudo apt-get install neovim
```

Note: Ubuntu's default repositories may have older versions. For the latest stable release:
```bash
sudo add-apt-repository ppa:neovim-ppa/stable
sudo apt-get update
sudo apt-get install neovim
```

**Fedora**:
```bash
sudo dnf install neovim
```

**Arch Linux**:
```bash
sudo pacman -S neovim
```

**AppImage (Universal)**:
Download from [GitHub Releases](https://github.com/neovim/neovim/releases):
```bash
curl -LO https://github.com/neovim/neovim/releases/latest/download/nvim.appimage
chmod u+x nvim.appimage
./nvim.appimage
```

Optionally, move to your PATH:
```bash
sudo mv nvim.appimage /usr/local/bin/nvim
```

### Windows

**Chocolatey**:
```powershell
choco install neovim
```

**Scoop**:
```powershell
scoop install neovim
```

**Winget**:
```powershell
winget install Neovim.Neovim
```

**Manual Installation**:
1. Download the latest release from [GitHub](https://github.com/neovim/neovim/releases)
2. Extract the zip file
3. Add the `bin` directory to your PATH

## Verifying Installation

After installation, verify Neovim is available:

```bash
nvim --version
```

You should see output like:
```
NVIM v0.9.5
Build type: Release
LuaJIT 2.1.0-beta3
...
```

## Installing Dependencies

For a full Neovim experience, you'll want these tools:

**Git** (required for plugin managers):
```bash
git --version
```

**Node.js** (for many LSP servers and plugins):
```bash
node --version
npm --version
```

**Python 3** (for some plugins):
```bash
python3 --version
```

**Ripgrep** (for fast searching):
```bash
rg --version
```

Install if missing:
- macOS: `brew install ripgrep`
- Linux: `sudo apt-get install ripgrep` (or equivalent)
- Windows: `choco install ripgrep`

**fd** (better file finding):
```bash
fd --version
```

Install if missing:
- macOS: `brew install fd`
- Linux: `sudo apt-get install fd-find` (or equivalent)
- Windows: `choco install fd`

## Configuration Location

Neovim looks for configuration in these locations:

**Linux/macOS**:
- `~/.config/nvim/init.lua` (or `init.vim`)
- `~/.config/nvim/`

**Windows**:
- `%LOCALAPPDATA%\nvim\init.lua` (or `init.vim`)
- `%LOCALAPPDATA%\nvim\`

You don't need to create these yet—we'll cover configuration in [Module 3](../03-configuration/README.md).

## Creating an Alias (Optional)

Many users create a `vim` alias to launch `nvim`:

**Bash/Zsh** (`~/.bashrc` or `~/.zshrc`):
```bash
alias vim='nvim'
alias vi='nvim'
```

**Fish** (`~/.config/fish/config.fish`):
```fish
alias vim nvim
alias vi nvim
```

**PowerShell** (Windows):
```powershell
Set-Alias vim nvim
Set-Alias vi nvim
```

## Troubleshooting

### Command not found

If `nvim` isn't found after installation:
1. Verify the installation completed successfully
2. Check if the binary is in your PATH
3. Try restarting your terminal
4. On Windows, ensure the installation directory is in your PATH environment variable

### Old Version

If you have an old version:
1. Remove the old installation
2. Install using the recommended method for your platform
3. Verify with `nvim --version`

### Permission Issues

On Linux/macOS, if you get permission errors:
- Don't run Neovim with `sudo` unless absolutely necessary
- Ensure your user has write permissions to `~/.config/nvim/`

## Next Steps

Now that Neovim is installed, proceed to [Setup and Verification](setup.md) to launch Neovim for the first time.

## Additional Resources

- [Official Installation Guide](https://github.com/neovim/neovim/wiki/Installing-Neovim)
- [Building from Source](https://github.com/neovim/neovim/wiki/Building-Neovim)
- [Troubleshooting Installation](https://github.com/neovim/neovim/wiki/FAQ#installation)
