# Setting Up LaTeX on Windows

## Introduction

This guide walks you through installing and setting up a complete LaTeX environment on Windows systems.

## Option 1: MiKTeX (Recommended for Beginners)

MiKTeX is a popular LaTeX distribution for Windows with automatic package installation.

### Installation Steps

1. **Download MiKTeX**
   - Visit: https://miktex.org/download
   - Download the installer (Basic or Net Installer)
   - Choose 64-bit version for modern systems

2. **Run the Installer**
   - Double-click the downloaded file
   - Choose "Install MiKTeX for: Just me" (recommended)
   - Select installation directory (default: `C:\Users\[username]\AppData\Local\Programs\MiKTeX`)
   - Choose "Yes" for installing missing packages on-the-fly

3. **Complete Installation**
   - Wait for installation to complete (may take 10-15 minutes)
   - MiKTeX Console will open automatically

4. **Update MiKTeX**
   - Open MiKTeX Console
   - Click "Updates" tab
   - Click "Check for updates"
   - Click "Update now" if updates are available

### MiKTeX Configuration

```bash
# Check installation
pdflatex --version

# Update package database
mpm --update-db

# Install a package manually
mpm --install=<package-name>
```

## Option 2: TeX Live

TeX Live is a comprehensive LaTeX distribution, standard on Linux/macOS.

### Installation Steps

1. **Download TeX Live**
   - Visit: https://tug.org/texlive/acquire-netinstall.html
   - Download `install-tl-windows.exe`

2. **Run Installer**
   - Run as Administrator
   - Choose "Install" (full installation ~7 GB)
   - Wait for installation (1-2 hours depending on internet speed)

3. **Verify Installation**
   ```bash
   pdflatex --version
   xelatex --version
   lualatex --version
   ```

### TeX Live Manager

```bash
# Update package database
tlmgr update --self --all

# Install a package
tlmgr install <package-name>

# Search for packages
tlmgr search --global <keyword>
```

## Text Editors and IDEs

### TeXstudio (Recommended for Beginners)

1. **Download**: https://texstudio.sourceforge.net/
2. **Install**: Run the installer
3. **Features**:
   - Integrated PDF viewer
   - Syntax highlighting
   - Auto-completion
   - Built-in spell checker
   - Error detection

**Configuration**:
- Options → Configure TeXstudio → Commands
- Ensure paths point to your LaTeX installation

**Changing Compilation Engine**:
- Options → Configure TeXstudio → Build
- Default Compiler: Choose "pdfLaTeX", "XeLaTeX", or "LuaLaTeX"
- Or use Tools menu to select engine for individual compilations

### TeXmaker

1. **Download**: https://www.xm1math.net/texmaker/
2. **Install**: Run the installer
3. **Similar features** to TeXstudio
4. **Configure**: Options → Configure Texmaker

**Changing Compilation Engine**:
- Options → Configure Texmaker → Commands
- Set paths for pdflatex, xelatex, lualatex
- Use Tools menu to choose which engine to use

### Visual Studio Code

1. **Install VS Code**: https://code.visualstudio.com/
2. **Install LaTeX Workshop Extension**:
   - Open Extensions (Ctrl+Shift+X)
   - Search "LaTeX Workshop"
   - Click Install

3. **Configure** (create `.vscode/settings.json`):
```json
{
    "latex-workshop.latex.autoBuild.run": "onSave",
    "latex-workshop.view.pdf.viewer": "tab",
    "latex-workshop.latex.recipes": [
        {
            "name": "pdfLaTeX",
            "tools": ["pdflatex"]
        },
        {
            "name": "XeLaTeX",
            "tools": ["xelatex"]
        },
        {
            "name": "LuaLaTeX",
            "tools": ["lualatex"]
        },
        {
            "name": "latexmk (pdfLaTeX)",
            "tools": ["latexmk-pdf"]
        },
        {
            "name": "latexmk (XeLaTeX)",
            "tools": ["latexmk-xelatex"]
        }
    ],
    "latex-workshop.latex.tools": [
        {
            "name": "pdflatex",
            "command": "pdflatex",
            "args": ["-interaction=nonstopmode", "-synctex=1", "%DOC%"]
        },
        {
            "name": "xelatex",
            "command": "xelatex",
            "args": ["-interaction=nonstopmode", "-synctex=1", "%DOC%"]
        },
        {
            "name": "lualatex",
            "command": "lualatex",
            "args": ["-interaction=nonstopmode", "-synctex=1", "%DOC%"]
        },
        {
            "name": "latexmk-pdf",
            "command": "latexmk",
            "args": ["-pdf", "-interaction=nonstopmode", "-synctex=1", "%DOC%"]
        },
        {
            "name": "latexmk-xelatex",
            "command": "latexmk",
            "args": ["-xelatex", "-interaction=nonstopmode", "-synctex=1", "%DOC%"]
        }
    ],
    "latex-workshop.formatting.latex": "latexindent",
    "latex-workshop.formatting.latexindent.args": [
        "-c",
        "%DIR%/",
        "%TMPFILE%",
        "-y=defaultIndent: '%INDENT%'"
    ],
    "[latex]": {
        "editor.formatOnSave": true,
        "editor.formatOnPaste": false
    }
}
```

**Usage**: 
- Press Ctrl+Alt+B to compile and select the desired recipe from the menu
- Press Shift+Alt+F to format your LaTeX document
- Documents will auto-format on save if `editor.formatOnSave` is enabled

### Overleaf (Online)

No installation required!
- Visit: https://www.overleaf.com/
- Create free account
- Start writing immediately
- Collaborative editing
- Limited compilation time on free tier

## Installing Additional Packages

### Automatic (MiKTeX)

MiKTeX installs packages automatically when needed. Configure in MiKTeX Console:
- Settings → General
- Package installation: "Ask me first" or "Yes"

### Manual Installation

```bash
# MiKTeX
mpm --install=packagename

# TeX Live
tlmgr install packagename
```

## Essential Packages to Install

Most come pre-installed, but you can verify:

```latex
% In your document preamble
\usepackage{geometry}    % Page layout
\usepackage{graphicx}    % Images
\usepackage{amsmath}     % Math
\usepackage{hyperref}    % Hyperlinks
\usepackage{biblatex}    % Bibliography
\usepackage{listings}    % Code listings
\usepackage{xcolor}      % Colors
```

## LaTeX Engines

Both MiKTeX and TeX Live come with multiple compilation engines. Here's what's included:

### Available Engines

1. **pdfLaTeX** - Default, fastest, standard LaTeX compiler
2. **XeLaTeX** - Modern engine with Unicode and system font support
3. **LuaLaTeX** - Modern engine with Lua scripting capabilities
4. **LaTeX** - Classic engine (produces DVI instead of PDF)

### Verify Engine Installation

Open Command Prompt or PowerShell and check:

```bash
# Check pdfLaTeX
pdflatex --version

# Check XeLaTeX
xelatex --version

# Check LuaLaTeX
lualatex --version

# Check standard LaTeX
latex --version
```

All engines should be installed automatically with MiKTeX or TeX Live. If any are missing:

**MiKTeX**: They will be installed automatically on first use, or manually via MiKTeX Console.

**TeX Live**: All engines are included in the full installation. For minimal installations, install the required collections:

```bash
# Install XeLaTeX components
tlmgr install xetex

# Install LuaLaTeX components
tlmgr install luatex

# Install font support for modern engines
tlmgr install fontspec
```

### Installing fontspec (Required for XeLaTeX/LuaLaTeX)

The `fontspec` package is essential for using system fonts with XeLaTeX and LuaLaTeX:

**MiKTeX**: Installs automatically when you compile a document using `fontspec`.

**TeX Live**: Install manually if needed:

```bash
tlmgr install fontspec
```

### Additional Packages for Modern Engines

```bash
# Unicode math support
tlmgr install unicode-math

# Additional font packages
tlmgr install tex-gyre
tlmgr install tex-gyre-math

# Multilingual support
tlmgr install babel
tlmgr install polyglossia
```

## Command Line Usage

### Open Command Prompt or PowerShell

```bash
# Compile with pdfLaTeX (default)
pdflatex document.tex

# Compile with XeLaTeX (for custom fonts and Unicode)
xelatex document.tex

# Compile with LuaLaTeX (modern alternative)
lualatex document.tex

# BibTeX for bibliography
bibtex document
pdflatex document.tex
pdflatex document.tex
```

### When to Use Each Engine

**Use pdfLaTeX when:**
- Creating standard documents
- You don't need special fonts
- You want the fastest compilation
- Maximum package compatibility is needed

**Use XeLaTeX when:**
- You need to use system fonts (TrueType, OpenType)
- Working with multilingual documents
- Requiring full Unicode support
- Creating documents with custom typography

**Use LuaLaTeX when:**
- You need XeLaTeX features plus Lua scripting
- Working with very large documents
- Requiring advanced font features
- Need better memory management

### Example: Using System Fonts with XeLaTeX

Create `xelatex-test.tex`:

```latex
\documentclass{article}
\usepackage{fontspec}

% Use Windows system fonts
\setmainfont{Times New Roman}
\setsansfont{Arial}
\setmonofont{Courier New}

\begin{document}

\section{Testing XeLaTeX}

This document uses Times New Roman as the main font.

\textsf{This sentence uses Arial (sans serif).}

\texttt{This sentence uses Courier New (monospace).}

Unicode characters work perfectly: α β γ δ ε 你好 مرحبا

\end{document}
```

Compile with:
```bash
xelatex xelatex-test.tex
```

## Testing Your Installation

### Create Test Document

Create `test.tex`:

```latex
\documentclass{article}
\usepackage[utf8]{inputenc}
\usepackage{amsmath}

\title{Test Document}
\author{Your Name}
\date{\today}

\begin{document}

\maketitle

\section{Introduction}
This is a test document to verify LaTeX installation.

Mathematical equation:
\begin{equation}
    E = mc^2
\end{equation}

\end{document}
```

### Compile

```bash
cd path\to\test\file
pdflatex test.tex
```

A `test.pdf` should be created successfully.

## Environment Variables

### Add LaTeX to PATH

MiKTeX and TeX Live usually add themselves to PATH automatically. If not:

1. **Open System Properties**:
   - Right-click "This PC" → Properties
   - Advanced system settings → Environment Variables

2. **Edit PATH**:
   - Under "System variables", find "Path"
   - Click "Edit" → "New"
   - Add MiKTeX bin directory: `C:\Users\[username]\AppData\Local\Programs\MiKTeX\miktex\bin\x64`
   - Or TeX Live: `C:\texlive\2024\bin\windows`

3. **Verify**:
   ```bash
   pdflatex --version
   ```

## Troubleshooting

### "pdflatex is not recognized"

- Check if LaTeX is in PATH (see Environment Variables above)
- Restart Command Prompt/PowerShell
- Reinstall LaTeX distribution

### Package Installation Fails

```bash
# MiKTeX: Refresh package database
mpm --update-db

# TeX Live
tlmgr update --self
```

### Permission Denied Errors

- Run MiKTeX Console as Administrator
- Check write permissions in installation directory

### PDF Not Generated

- Check for errors in `.log` file
- Ensure all packages are installed
- Try compiling twice (for references)

### Fonts Not Found (XeLaTeX)

- Install the font in Windows (double-click .ttf/.otf file)
- Use font name exactly as it appears in Windows

## Recommended Workflow

1. **Write** in your preferred editor (TeXstudio, VS Code)
2. **Compile** with F1 or F5 (editor-specific)
3. **View** PDF in integrated viewer
4. **Debug** using error messages and log file
5. **Iterate** until satisfied

## Additional Tools

### Perl (for some packages)

Download: https://strawberryperl.com/
- Required by some LaTeX packages
- Install if you encounter Perl-related errors

### Python (for some tools)

Download: https://www.python.org/
- Useful for pygments (code highlighting)
- Install `pygments`: `pip install pygments`

### ImageMagick (for image conversion)

Download: https://imagemagick.org/
- Converts various image formats
- Useful for including non-standard image formats

## Best Practices

1. **Keep Updated**: Regularly update MiKTeX/TeX Live
2. **Backup**: Keep `.tex` files in version control (Git)
3. **Organization**: Use project folders for multi-file documents
4. **Editor**: Learn keyboard shortcuts for efficiency
5. **Templates**: Save working preambles as templates

## Comparison: MiKTeX vs TeX Live

| Feature | MiKTeX | TeX Live |
|---------|--------|----------|
| Size | Smaller initial install | Large (~7 GB) |
| Packages | Install on-demand | All included |
| Updates | Regular, easy | Annual releases |
| Best For | Windows users | Cross-platform consistency |

## Troubleshooting

Having issues with VS Code and LaTeX Workshop? Check out our comprehensive troubleshooting guide:

📖 **[VS Code + LaTeX Workshop Troubleshooting Guide](05-vscode-troubleshooting.md)**

Topics covered:
- Formatter configuration issues
- Compilation problems
- **How to choose compilation recipes** (sidebar, magic comments, command palette)
- PDF viewer issues
- IntelliSense and SyncTeX problems
- Complete example settings.json with XeLaTeX recipes

## Next Steps

- Learn [basic document structure](../01-basics/01-document-structure.md)
- Explore [compiling LaTeX documents](../04-compilation/01-compiling-latex.md)
- Try [example documents](../../examples/)
- Read setup guides for [macOS](02-setup-macos.md) or [Linux](03-setup-linux.md)

## Resources

- MiKTeX Documentation: https://docs.miktex.org/
- TeX Live Guide: https://tug.org/texlive/doc/texlive-en/texlive-en.html
- LaTeX Project: https://www.latex-project.org/
- CTAN (Package Repository): https://ctan.org/
