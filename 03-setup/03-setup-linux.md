# Setting Up LaTeX on Linux

## Introduction

This guide covers installing and configuring LaTeX on various Linux distributions.

## TeX Live (Recommended)

TeX Live is the standard LaTeX distribution for Linux systems.

## Installation by Distribution

### Ubuntu/Debian

```bash
# Minimal installation (~500 MB)
sudo apt update
sudo apt install texlive

# Recommended: Full installation (~5 GB)
sudo apt install texlive-full

# Medium installation (~2 GB) - common packages
sudo apt install texlive-latex-extra texlive-fonts-recommended \
                 texlive-fonts-extra texlive-lang-european

# Additional tools
sudo apt install latexmk texlive-xetex texlive-luatex
```

### Fedora/RHEL/CentOS

```bash
# Minimal installation
sudo dnf install texlive

# Full installation
sudo dnf install texlive-scheme-full

# Recommended packages
sudo dnf install texlive-collection-latexextra \
                 texlive-collection-fontsrecommended \
                 texlive-xetex texlive-luatex

# Additional tools
sudo dnf install latexmk
```

### Arch Linux

```bash
# Minimal installation
sudo pacman -S texlive-core

# Full installation
sudo pacman -S texlive-most texlive-lang

# Additional tools
sudo pacman -S texlive-bin latexmk
```

### openSUSE

```bash
# Minimal
sudo zypper install texlive

# Full installation
sudo zypper install texlive-scheme-full

# Additional tools
sudo zypper install latexmk
```

## Manual TeX Live Installation

For the latest version or distributions without packages:

### Download and Install

```bash
# Download installer
wget https://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz

# Extract
tar -xzf install-tl-unx.tar.gz
cd install-tl-*

# Run installer
sudo ./install-tl

# Follow prompts - full installation takes time
```

### Add to PATH

Add to `~/.bashrc` or `~/.zshrc`:

```bash
# Add TeX Live to PATH
export PATH="/usr/local/texlive/2024/bin/x86_64-linux:$PATH"
export MANPATH="/usr/local/texlive/2024/texmf-dist/doc/man:$MANPATH"
export INFOPATH="/usr/local/texlive/2024/texmf-dist/doc/info:$INFOPATH"

# Reload
source ~/.bashrc
```

## Package Management

### Using tlmgr (TeX Live Manager)

```bash
# Initialize (if needed)
sudo tlmgr init-usertree

# Update tlmgr itself
sudo tlmgr update --self

# Update all packages
sudo tlmgr update --all

# Search for packages
tlmgr search --global <keyword>

# Install a package
sudo tlmgr install <package-name>

# List installed packages
tlmgr list --only-installed

# Package information
tlmgr info <package-name>

# Remove a package
sudo tlmgr remove <package-name>
```

### Using Distribution Package Managers

```bash
# Ubuntu/Debian - search
apt-cache search texlive

# Install specific package
sudo apt install texlive-science

# Fedora
sudo dnf search texlive
sudo dnf install texlive-beamer

# Arch
pacman -Ss texlive
sudo pacman -S texlive-science
```

## Text Editors and IDEs

### TeXstudio

```bash
# Ubuntu/Debian
sudo apt install texstudio

# Fedora
sudo dnf install texstudio

# Arch
sudo pacman -S texstudio
```

**Features**:
- Integrated PDF viewer
- Syntax highlighting
- Auto-completion
- Spell checking
- Structure view

**Changing Compilation Engine**:
- Options → Configure TeXstudio → Build
- Default Compiler: Choose "pdfLaTeX", "XeLaTeX", or "LuaLaTeX"
- Or use Tools menu to select engine for individual compilations

**Features**:
- Integrated PDF viewer
- Syntax highlighting
- Auto-completion
- Spell checking
- Structure view

### TeXmaker

```bash
# Ubuntu/Debian
sudo apt install texmaker

# Fedora
sudo dnf install texmaker

# Arch
sudo pacman -S texmaker
```

### Visual Studio Code

```bash
# Install VS Code (Ubuntu/Debian)
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -o root -g root -m 644 packages.microsoft.gpg /etc/apt/trusted.gpg.d/
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'
sudo apt update
sudo apt install code

# Or use snap
sudo snap install code --classic

# Install LaTeX Workshop extension
code --install-extension James-Yu.latex-workshop
```

**Configuration** (`.vscode/settings.json`):
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
- Press Ctrl+Alt+B to compile and select the desired recipe from the menu
- Press Shift+Alt+F to format your LaTeX document
- Documents will auto-format on save if `editor.formatOnSave` is enabled

### Vim/Neovim with vimtex

```bash
# Install vim-plug (plugin manager)
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

# Add to ~/.vimrc
cat >> ~/.vimrc << 'EOF'
call plug#begin()
Plug 'lervag/vimtex'
call plug#end()

let g:vimtex_view_method = 'zathura'
let g:vimtex_compiler_method = 'latexmk'
EOF

# Install plugins
vim +PlugInstall +qall
```

### Emacs with AUCTeX

```bash
# Install Emacs
sudo apt install emacs  # Ubuntu/Debian

# Install AUCTeX
# Add to ~/.emacs:
(require 'package)
(add-to-list 'package-archives '("melpa" . "https://melpa.org/packages/"))
(package-initialize)
; M-x package-install RET auctex RET
```

### Overleaf (Online)

- Visit: https://www.overleaf.com/
- No installation required
- Browser-based
- Collaborative editing

## PDF Viewers

### Zathura (Recommended for auto-reload)

```bash
# Ubuntu/Debian
sudo apt install zathura

# Fedora
sudo dnf install zathura

# Arch
sudo pacman -S zathura zathura-pdf-poppler
```

**Auto-reload** when PDF changes - perfect for continuous compilation.

### Evince

```bash
sudo apt install evince  # Ubuntu/Debian
```

Default GNOME PDF viewer, auto-reloads.

### Okular

```bash
sudo apt install okular  # Ubuntu/Debian
```

KDE PDF viewer with annotations.

## LaTeX Engines

Linux distributions include multiple compilation engines with TeX Live. Here's what's available:

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

# List all available engines
which -a pdflatex xelatex lualatex latex
```

### Installing Additional Engines

**Full TeX Live installation** (`texlive-full`) includes all engines. For minimal installations, install specific collections:

#### Ubuntu/Debian

```bash
# Install XeLaTeX
sudo apt install texlive-xetex

# Install LuaLaTeX
sudo apt install texlive-luatex

# Install fontspec (essential for XeLaTeX/LuaLaTeX)
sudo apt install texlive-latex-extra

# Install additional font packages
sudo apt install texlive-fonts-extra
```

#### Fedora/RHEL/CentOS

```bash
# Install XeLaTeX
sudo dnf install texlive-xetex

# Install LuaLaTeX
sudo dnf install texlive-luatex

# Install fontspec and extras
sudo dnf install texlive-fontspec
sudo dnf install texlive-collection-fontsrecommended
```

#### Arch Linux

```bash
# XeLaTeX and LuaLaTeX are in texlive-core
sudo pacman -S texlive-core

# Additional font packages
sudo pacman -S texlive-fontsextra
```

#### Manual TeX Live Installation

If using manual TeX Live installation:

```bash
# Update tlmgr
sudo tlmgr update --self

# Install XeLaTeX
sudo tlmgr install xetex

# Install LuaLaTeX
sudo tlmgr install luatex

# Install fontspec
sudo tlmgr install fontspec

# Install unicode-math
sudo tlmgr install unicode-math

# Install TeX Gyre fonts
sudo tlmgr install tex-gyre tex-gyre-math
```

### Additional Packages for Modern Engines

```bash
# Multilingual support
sudo tlmgr install babel polyglossia

# Font tools
sudo tlmgr install fontspec fontawesome5

# Advanced typography
sudo tlmgr install microtype

# For Ubuntu/Debian using apt
sudo apt install texlive-lang-european texlive-lang-other
```

## Command Line Usage

### Basic Compilation

```bash
# Navigate to document directory
cd ~/documents/latex

# Compile with pdfLaTeX (default)
pdflatex document.tex

# Compile with XeLaTeX (for system fonts)
xelatex document.tex

# Compile with LuaLaTeX (modern alternative)
lualatex document.tex

# View PDF
zathura document.pdf &
# or
xdg-open document.pdf
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

### Using latexmk (Recommended)

```bash
# Compile with pdfLaTeX (default)
latexmk -pdf document.tex

# Compile with XeLaTeX
latexmk -xelatex document.tex

# Compile with LuaLaTeX
latexmk -lualatex document.tex

# Continuous mode (recompile on save)
latexmk -pdf -pvc document.tex

# Clean auxiliary files
latexmk -c

# Clean everything including PDF
latexmk -C
```

### Example: Using System Fonts with XeLaTeX

Create `xelatex-linux-test.tex`:

```latex
% !TEX program = xelatex
\documentclass{article}
\usepackage{fontspec}

% Use common Linux fonts (install if needed)
\setmainfont{Liberation Serif}  % Or "DejaVu Serif", "Noto Serif"
\setsansfont{Liberation Sans}   % Or "DejaVu Sans", "Noto Sans"
\setmonofont{Liberation Mono}   % Or "DejaVu Sans Mono", "Noto Mono"

\begin{document}

\section{Testing XeLaTeX on Linux}

This document uses Liberation Serif as the main font.

\textsf{This sentence uses Liberation Sans (sans serif).}

\texttt{This sentence uses Liberation Mono (monospace).}

Unicode characters work perfectly: α β γ δ ε 你好 مرحبا 日本語

\end{document}
```

Compile with:
```bash
xelatex xelatex-linux-test.tex
```

**Note**: Install fonts if missing:
```bash
# Ubuntu/Debian
sudo apt install fonts-liberation fonts-dejavu fonts-noto

# Fedora
sudo dnf install liberation-fonts dejavu-fonts google-noto-fonts

# Arch
sudo pacman -S ttf-liberation ttf-dejavu noto-fonts
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
This is a test document to verify LaTeX installation on Linux.

Mathematical equation:
\begin{equation}
    E = mc^2
\end{equation}

\end{document}
```

### Compile

```bash
cd ~/Documents
pdflatex test.tex
```

A `test.pdf` should be created successfully.

## PDF Viewers

### Example: Using System Fonts with XeLaTeX

First, list available fonts on your system:

```bash
# List all fonts
fc-list : family | sort | uniq

# Search for specific font
fc-list | grep -i "liberation"
fc-list | grep -i "dejavu"
```

Create `xelatex-test.tex`:

```latex
\documentclass{article}
\usepackage{fontspec}

% Use Linux system fonts
\setmainfont{Liberation Serif}
\setsansfont{Liberation Sans}
\setmonofont{Liberation Mono}

% Alternative: DejaVu fonts
% \setmainfont{DejaVu Serif}
% \setsansfont{DejaVu Sans}
% \setmonofont{DejaVu Sans Mono}

\begin{document}

\section{Testing XeLaTeX on Linux}

This document uses Liberation Serif as the main font.

\textsf{This sentence uses Liberation Sans (sans serif).}

\texttt{This sentence uses Liberation Mono (monospace).}

Unicode characters work perfectly: α β γ δ ε 你好 مرحبا ℝ ℕ ℤ

\subsection{Font Features}

With XeLaTeX, you can access OpenType features:

\begin{itemize}
    \item Full Unicode support
    \item Any installed system font
    \item Advanced typography
    \item Multiple language scripts
\end{itemize}

\end{document}
```

Compile with:
```bash
xelatex xelatex-test.tex

# View the result
zathura xelatex-test.pdf &
```

### Bibliography with BibTeX

```bash
pdflatex document.tex
bibtex document
pdflatex document.tex
pdflatex document.tex

# Or let latexmk handle it
latexmk -pdf document.tex
```

## Testing Your Installation

### Create Test Document

```bash
# Create test directory
mkdir -p ~/latex-test
cd ~/latex-test

# Create test.tex
cat > test.tex << 'EOF'
\documentclass{article}
\usepackage[utf8]{inputenc}
\usepackage{amsmath}
\usepackage{graphicx}

\title{Linux LaTeX Test}
\author{Your Name}
\date{\today}

\begin{document}

\maketitle

\section{Introduction}
Testing LaTeX on Linux.

\subsection{Mathematics}
\begin{equation}
    \int_0^\infty e^{-x^2} dx = \frac{\sqrt{\pi}}{2}
\end{equation}

\subsection{Lists}
\begin{itemize}
    \item First item
    \item Second item
    \item Third item
\end{itemize}

\end{document}
EOF

# Compile
pdflatex test.tex

# View
xdg-open test.pdf
# or
zathura test.pdf
```

## System Fonts with XeLaTeX

List available fonts:

```bash
fc-list : family | sort | uniq
```

Use in document:

```latex
\documentclass{article}
\usepackage{fontspec}

\setmainfont{Liberation Serif}
\setsansfont{Liberation Sans}
\setmonofont{Liberation Mono}

\begin{document}
This uses system fonts!
\end{document}
```

Compile:
```bash
xelatex document.tex
```

## Environment Variables

Usually set automatically, but if needed:

```bash
# Add to ~/.bashrc
export PATH="/usr/local/texlive/2024/bin/x86_64-linux:$PATH"
export MANPATH="/usr/local/texlive/2024/texmf-dist/doc/man:$MANPATH"
export INFOPATH="/usr/local/texlive/2024/texmf-dist/doc/info:$INFOPATH"

# Reload
source ~/.bashrc
```

## Troubleshooting

### Command Not Found

```bash
# Check if installed
which pdflatex

# Find where it is
find /usr -name pdflatex 2>/dev/null

# Add to PATH if needed
export PATH="/usr/local/texlive/2024/bin/x86_64-linux:$PATH"
```

### Permission Denied for tlmgr

```bash
# Use sudo for system-wide packages
sudo tlmgr install <package>

# Or use user mode
tlmgr init-usertree
tlmgr --usermode install <package>
```

### Missing Packages

```bash
# Ubuntu/Debian - install more packages
sudo apt install texlive-latex-extra texlive-fonts-extra

# Or use tlmgr
sudo tlmgr install <package-name>
```

### Font Cache Issues

```bash
# Rebuild font cache
fc-cache -fv
```

### Encoding Problems

```bash
# Check file encoding
file -i document.tex

# Convert if needed
iconv -f ISO-8859-1 -t UTF-8 document.tex > document-utf8.tex
```

## Automation Scripts

### Makefile for LaTeX

Create `Makefile`:

```makefile
.PHONY: all clean view

MAIN = document
PDF = $(MAIN).pdf

all: $(PDF)

$(PDF): $(MAIN).tex
	latexmk -pdf $(MAIN).tex

view: $(PDF)
	zathura $(PDF) &

clean:
	latexmk -C
	rm -f *.aux *.log *.out *.toc *.bbl *.blg

watch:
	latexmk -pdf -pvc $(MAIN).tex
```

Usage:
```bash
make          # Compile
make view     # View PDF
make clean    # Clean aux files
make watch    # Continuous compilation
```

### Shell Script for Multiple Compilations

```bash
#!/bin/bash
# compile.sh

FILE=$1

pdflatex $FILE
bibtex ${FILE%.tex}
pdflatex $FILE
pdflatex $FILE

echo "Compilation complete: ${FILE%.tex}.pdf"
```

## Docker for LaTeX

Portable LaTeX environment:

```bash
# Pull image
docker pull texlive/texlive

# Compile document
docker run --rm -v $(pwd):/work texlive/texlive pdflatex document.tex

# Or create alias
alias dlatex='docker run --rm -v $(pwd):/work texlive/texlive pdflatex'
dlatex document.tex
```

## Performance Tips

1. **Use latexmk**: Smarter compilation
2. **Draft mode**: `\documentclass[draft]{article}`
3. **Partial compilation**: Comment out sections
4. **SSD storage**: Faster I/O
5. **RAM disk**: For temporary files (advanced)

## Best Practices

1. **Keep Updated**: Regular `sudo tlmgr update --all`
2. **Version Control**: Use Git for `.tex` files
3. **Project Organization**: Separate folders for projects
4. **Backup**: Regular backups of source files
5. **Templates**: Reuse working preambles

## Distribution Package Comparison

| Distro | Size | Packages | Update Method |
|--------|------|----------|---------------|
| texlive | ~500 MB | Basic | apt/dnf |
| texlive-full | ~5 GB | Complete | apt/dnf |
| Manual install | ~7 GB | Latest | tlmgr |

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
- Explore [compilation methods](../04-compilation/01-compiling-latex.md)
- Try [example documents](../../examples/)
- Compare [Windows](01-setup-windows.md) or [macOS](02-setup-macos.md) setup

## Resources

- TeX Live: https://tug.org/texlive/
- CTAN: https://ctan.org/
- LaTeX Project: https://www.latex-project.org/
- TeX Stack Exchange: https://tex.stackexchange.com/
