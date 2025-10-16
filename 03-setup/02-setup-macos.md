# Setting Up LaTeX on macOS

## Introduction

This guide covers installing and configuring a complete LaTeX environment on macOS systems.

## MacTeX Distribution (Recommended)

MacTeX is the standard TeX Live distribution packaged specifically for macOS.

### Installation Steps

1. **Download MacTeX**
   - Visit: https://www.tug.org/mactex/
   - Download MacTeX.pkg (~4.5 GB)
   - Or download Smaller BasicTeX (~100 MB, minimal installation)

2. **Install MacTeX**
   - Double-click the downloaded `.pkg` file
   - Follow installation wizard
   - Requires ~7 GB of disk space
   - Installation takes 10-15 minutes
   - Requires administrator password

3. **Verify Installation**
   ```bash
   pdflatex --version
   which pdflatex
   # Should show: /Library/TeX/texbin/pdflatex
   ```

### What's Included

MacTeX includes:
- Full TeX Live distribution
- TeXShop editor
- LaTeXiT (equation editor)
- BibDesk (bibliography manager)
- TeX Live Utility (package manager)
- Ghostscript and other utilities

## BasicTeX (Minimal Installation)

For users who want a smaller footprint:

### Installation

```bash
# Using Homebrew
brew install --cask basictex

# Or download from: https://www.tug.org/mactex/morepackages.html
```

### Install Additional Packages

```bash
# Update tlmgr first
sudo tlmgr update --self

# Install commonly used packages
sudo tlmgr install collection-fontsrecommended
sudo tlmgr install collection-latexextra
sudo tlmgr install latexmk
```

## Package Management with TeX Live Utility

### GUI Tool (Included with MacTeX)

1. Open "TeX Live Utility" from Applications
2. Click "Update" to check for package updates
3. Search for packages in the search bar
4. Select and install packages

### Command Line (tlmgr)

```bash
# Update tlmgr itself
sudo tlmgr update --self

# Update all packages
sudo tlmgr update --all

# Search for a package
tlmgr search --global <package-name>

# Install a package
sudo tlmgr install <package-name>

# List installed packages
tlmgr list --only-installed

# Info about a package
tlmgr info <package-name>
```

## Text Editors and IDEs

### TeXShop (Included with MacTeX)

**Location**: `/Applications/TeX/`

**Features**:
- Native macOS app
- Integrated PDF viewer
- Syntax highlighting
- Macro support
- Templates

**Usage**:
- Open `.tex` file
- Press Cmd+T to typeset
- PDF appears in separate window

**Changing Compilation Engine**:
- TeXShop → Preferences → Engine
- Choose default engine (TeX + DVI, pdfTeX, XeTeX, LuaTeX)
- Or add `%!TEX program = xelatex` at the top of your document

### Visual Studio Code

1. **Install VS Code**
   ```bash
   brew install --cask visual-studio-code
   ```

2. **Install LaTeX Workshop Extension**
   - Open Extensions (Cmd+Shift+X)
   - Search "LaTeX Workshop"
   - Install it

3. **Configuration** (`settings.json`):
   ```json
   {
       "latex-workshop.latex.autoBuild.run": "onFileChange",
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
- Press Cmd+Option+B to compile and select the desired recipe from the menu
- Press Shift+Option+F to format your LaTeX document
- Documents will auto-format on save if `editor.formatOnSave` is enabled

### Sublime Text with LaTeXTools

```bash
# Install Sublime Text
brew install --cask sublime-text

# Install Package Control, then install LaTeXTools
```

### TeXstudio

```bash
brew install --cask texstudio
```

Cross-platform editor with extensive features.

### Overleaf (Online)

- Visit: https://www.overleaf.com/
- No local installation needed
- Collaborative editing
- Works in any browser

## Using Homebrew for Installation

Homebrew is the popular package manager for macOS.

### Install Homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### Install LaTeX via Homebrew

```bash
# Full MacTeX
brew install --cask mactex

# Or BasicTeX (minimal)
brew install --cask basictex

# Additional tools
brew install latexdiff
brew install pdf2svg
```

## LaTeX Engines

MacTeX and BasicTeX include multiple compilation engines. Here's what you get:

### Available Engines

1. **pdfLaTeX** - Default, fastest, standard LaTeX compiler
2. **XeLaTeX** - Modern engine with Unicode and system font support
3. **LuaLaTeX** - Modern engine with Lua scripting capabilities
4. **LaTeX** - Classic engine (produces DVI instead of PDF)

### Verify Engine Installation

Open Terminal and check:

```bash
# Check pdfLaTeX
pdflatex --version

# Check XeLaTeX
xelatex --version

# Check LuaLaTeX
lualatex --version

# Check standard LaTeX
latex --version

# List all TeX binaries
ls -la /Library/TeX/texbin/
```

All engines are installed automatically with MacTeX. For BasicTeX, you may need to install additional components:

```bash
# Update tlmgr first
sudo tlmgr update --self

# Ensure XeLaTeX is available
sudo tlmgr install xetex

# Ensure LuaLaTeX is available
sudo tlmgr install luatex

# Install fontspec (essential for XeLaTeX/LuaLaTeX)
sudo tlmgr install fontspec
```

### Installing fontspec (Required for XeLaTeX/LuaLaTeX)

The `fontspec` package is essential for using system fonts:

```bash
# Install fontspec and dependencies
sudo tlmgr install fontspec

# Install unicode-math for mathematical typesetting
sudo tlmgr install unicode-math

# Install recommended font packages
sudo tlmgr install tex-gyre
sudo tlmgr install tex-gyre-math

# Install multilingual support
sudo tlmgr install babel
sudo tlmgr install polyglossia
```

### Additional Packages for Modern Engines

```bash
# Math typesetting with Unicode
sudo tlmgr install unicode-math

# Font tools and additional fonts
sudo tlmgr install fontawesome5

# Advanced typography
sudo tlmgr install microtype

# Additional language support
sudo tlmgr install collection-langenglish
sudo tlmgr install collection-langeuropean
```

## Command Line Usage

### Using Terminal

```bash
# Navigate to your document directory
cd ~/Documents/LaTeX/myproject

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

# Or use latexmk (recommended - handles multiple passes automatically)
latexmk -pdf document.tex           # pdfLaTeX
latexmk -xelatex document.tex       # XeLaTeX
latexmk -lualatex document.tex      # LuaLaTeX

# Auto-compile on file changes
latexmk -pdf -pvc document.tex
```

### When to Use Each Engine

**Use pdfLaTeX when:**
- ✅ Writing standard academic papers
- ✅ You don't need special fonts
- ✅ You want the fastest compilation
- ✅ Maximum package compatibility is needed

**Use XeLaTeX when:**
- ✅ Using Unicode characters (中文, العربية, etc.)
- ✅ Need system fonts (SF Pro, Helvetica Neue, etc.)
- ✅ Using `fontspec` package
- ✅ Writing multilingual documents

**Use LuaLaTeX when:**
- ✅ Need XeLaTeX features plus Lua scripting
- ✅ Working with very large documents
- ✅ Requiring advanced font features
- ✅ Need better memory management

### Example: Using macOS System Fonts with XeLaTeX

Create `xelatex-mac-test.tex`:

```latex
% !TEX program = xelatex
\documentclass{article}
\usepackage{fontspec}

% Use macOS system fonts
\setmainfont{Helvetica Neue}
\setsansfont{SF Pro Display}
\setmonofont{Menlo}

\begin{document}

\section{Testing XeLaTeX on macOS}

This document uses Helvetica Neue as the main font.

\textsf{This sentence uses SF Pro Display (sans serif).}

\texttt{This sentence uses Menlo (monospace).}

Unicode characters work perfectly: α β γ δ ε 你好 مرحبا 日本語

\end{document}
```

Compile with:
```bash
xelatex xelatex-mac-test.tex
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
This is a test document to verify LaTeX installation on macOS.

Mathematical equation:
\begin{equation}
    E = mc^2
\end{equation}

\end{document}
```

### Compile

```bash
cd ~/Desktop
pdflatex test.tex
```

A `test.pdf` should be created successfully.

## Basic Compilation

### Basic Compilation

```bash
# Navigate to your document directory
cd ~/Documents/latex-projects

# Compile with pdfLaTeX (default)
pdflatex document.tex

# Compile with XeLaTeX (for system fonts)
xelatex document.tex

# Compile with LuaLaTeX (modern alternative)
lualatex document.tex
```

### When to Use Each Engine

**Use pdfLaTeX when:**
- Creating standard documents
- You don't need special fonts
- You want the fastest compilation
- Maximum package compatibility is needed

**Use XeLaTeX when:**
- You need to use macOS system fonts
- Working with multilingual documents
- Requiring full Unicode support
- Creating documents with custom typography

**Use LuaLaTeX when:**
- You need XeLaTeX features plus Lua scripting
- Working with very large documents
- Requiring advanced font features
- Need better memory management

### Using latexmk (Recommended)

latexmk automatically runs LaTeX the correct number of times:

```bash
# Compile with pdfLaTeX (default)
latexmk -pdf document.tex

# Compile with XeLaTeX
latexmk -xelatex document.tex

# Compile with LuaLaTeX
latexmk -lualatex document.tex

# Continuous compilation (recompiles on save)
latexmk -pdf -pvc document.tex

# Clean auxiliary files
latexmk -c

# Clean all generated files including PDF
latexmk -C
```

### Example: Using macOS Fonts with XeLaTeX

Create `xelatex-test.tex`:

```latex
\documentclass{article}
\usepackage{fontspec}

% Use macOS system fonts
\setmainfont{Helvetica Neue}
\setsansfont{Avenir}
\setmonofont{Menlo}

\begin{document}

\section{Testing XeLaTeX on macOS}

This document uses Helvetica Neue as the main font.

\textsf{This sentence uses Avenir (sans serif).}

\texttt{This sentence uses Menlo (monospace).}

Unicode characters work perfectly: α β γ δ ε 你好 مرحبا 🎉

\subsection{Listing Available Fonts}

To see all available fonts on your system:
\begin{verbatim}
fc-list : family | sort | uniq
\end{verbatim}

Or use Font Book.app to browse fonts visually.

\end{document}
```

Compile with:
```bash
xelatex xelatex-test.tex
open xelatex-test.pdf
```

### BibTeX for Bibliographies

```bash
pdflatex document.tex
bibtex document
pdflatex document.tex
pdflatex document.tex

# Or use latexmk to handle it automatically
latexmk -pdf document.tex
```

## Testing Your Installation

### Create Test Document

Create `test.tex`:

```latex
\documentclass{article}
\usepackage[utf8]{inputenc}
\usepackage{amsmath}
\usepackage{graphicx}

\title{macOS LaTeX Test}
\author{Your Name}
\date{\today}

\begin{document}

\maketitle

\section{Introduction}
This tests the LaTeX installation on macOS.

\subsection{Mathematics}
Einstein's famous equation:
\begin{equation}
    E = mc^2
\end{equation}

\subsection{Text Formatting}
\textbf{Bold text}, \textit{italic text}, and \texttt{monospace text}.

\end{document}
```

### Compile

```bash
cd path/to/test/file
pdflatex test.tex
open test.pdf
```

## PATH Configuration

LaTeX should be automatically added to PATH. Verify:

```bash
echo $PATH | grep tex
# Should show: /Library/TeX/texbin
```

If not in PATH, add to `~/.zshrc` (or `~/.bash_profile` for older macOS):

```bash
# Add to ~/.zshrc
export PATH="/Library/TeX/texbin:$PATH"

# Reload configuration
source ~/.zshrc
```

## macOS-Specific Features

### Using macOS Fonts with XeLaTeX

```latex
\documentclass{article}
\usepackage{fontspec}

% Use macOS system fonts
\setmainfont{Helvetica Neue}
\setsansfont{Avenir}
\setmonofont{Menlo}

\begin{document}
This uses macOS system fonts!
\end{document}
```

Compile with:
```bash
xelatex document.tex
```

### Quick Look for PDFs

```bash
# Quick look at generated PDF
qlmanage -p document.pdf
```

### BibDesk for Bibliography Management

Included with MacTeX, native macOS bibliography manager:
- Location: `/Applications/TeX/BibDesk.app`
- Manages `.bib` files
- Imports from web sources
- Integrates with macOS

## Troubleshooting

### Command Not Found

```bash
# Check if installed
which pdflatex

# If not found, check installation
ls -la /Library/TeX/texbin/

# Add to PATH in ~/.zshrc
export PATH="/Library/TeX/texbin:$PATH"
source ~/.zshrc
```

### Permission Denied for tlmgr

```bash
# Use sudo for system-wide installation
sudo tlmgr update --self
sudo tlmgr install <package>
```

### Font Not Found

```bash
# List available fonts (for XeLaTeX)
fc-list

# Or use fontspec to check
xelatex with fontspec package will report available fonts
```

### Package Installation Fails

```bash
# Update tlmgr and try again
sudo tlmgr update --self --all
sudo tlmgr install <package>

# Check TeX Live Utility for GUI alternative
```

### Encoding Issues

Ensure files are saved as UTF-8:
```bash
file -I document.tex
# Should show: charset=utf-8
```

## Updating MacTeX

### Annual Updates

New MacTeX released annually (usually summer):
1. Download new MacTeX.pkg
2. Install (replaces previous version)
3. Previous version moves to `/Library/TeX/Distributions/.DefaultTeX/Contents/Older`

### Package Updates

```bash
# Update all packages
sudo tlmgr update --all

# Or use TeX Live Utility GUI
```

## Uninstalling

### Complete Removal

```bash
# Remove MacTeX
sudo rm -rf /usr/local/texlive/2024
sudo rm -rf /Library/TeX
sudo rm -rf ~/Library/texlive

# If installed via Homebrew
brew uninstall --cask mactex
# or
brew uninstall --cask basictex
```

## Recommended Workflow

1. **Write**: Use TeXShop, VS Code, or your preferred editor
2. **Compile**: Cmd+T in TeXShop, or `latexmk -pdf -pvc` for auto-compilation
3. **View**: Integrated PDF viewer or Preview.app
4. **Version Control**: Use Git for backup and collaboration
5. **Bibliography**: Manage with BibDesk or JabRef

## Additional Tools

### Installing via Homebrew

```bash
# PDF manipulation
brew install pdftk-java

# Image conversion
brew install imagemagick

# Diff tool for LaTeX
brew install latexdiff

# Markdown to LaTeX
brew install pandoc

# Python tools
pip3 install pygments  # for code highlighting
```

## Performance Tips

1. **Use latexmk**: Smarter than running pdflatex multiple times
2. **Draft mode**: Use `\documentclass[draft]{article}` for faster compilation
3. **External editors**: Keep PDF viewer separate for instant updates
4. **SSD**: Store projects on SSD for faster I/O

## Best Practices

1. **Keep Updated**: Regularly run `sudo tlmgr update --all`
2. **Use Version Control**: Git for `.tex` files
3. **Project Structure**: Organize multi-file projects with folders
4. **Backup**: Use Time Machine or cloud backup
5. **Templates**: Save working preambles for reuse

## Comparison: MacTeX vs BasicTeX

| Feature | MacTeX | BasicTeX |
|---------|--------|----------|
| Size | ~7 GB | ~100 MB |
| Packages | Complete | Minimal |
| GUI Tools | Included | Need separate install |
| Best For | Most users | Minimal installs, servers |

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

- Learn [document structure](../01-basics/01-document-structure.md)
- Explore [compiling LaTeX](../04-compilation/01-compiling-latex.md)
- Try [example documents](../../examples/)
- Compare with [Windows](01-setup-windows.md) or [Linux](03-setup-linux.md) setup

## Resources

- MacTeX Website: https://www.tug.org/mactex/
- TeX on macOS: https://www.tug.org/mactex/
- MacTeX Documentation: Included in `/Library/TeX/Documentation/`
- TeX Users Group: https://tug.org/
