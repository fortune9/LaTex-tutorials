# LaTeX Engine Comparison and Usage Guide

This document provides a quick reference for choosing and using different LaTeX compilation engines.

## Available Engines

### 1. pdfLaTeX
- **Default engine** in most distributions
- **Fastest** compilation speed
- **Best compatibility** with packages
- **Limited to** Type 1 and bitmap fonts
- **No native Unicode** support
- **Best for:** Standard documents, maximum compatibility

### 2. XeLaTeX
- **Modern engine** with full Unicode support
- **Can use** any system font (TrueType, OpenType)
- **Requires** `fontspec` package for font selection
- **Slower** than pdfLaTeX
- **Best for:** Custom fonts, multilingual documents, Unicode text

### 3. LuaLaTeX
- **Modern engine** like XeLaTeX
- **Full Unicode** and system font support
- **Lua scripting** capabilities
- **Better memory** management for large documents
- **Best for:** Complex documents, programmable typesetting

### 4. LaTeX (classic)
- **Original engine** producing DVI files
- **Requires** additional step to convert to PDF
- **Rarely used** today
- **Best for:** Legacy workflows, DVI output needed

## Quick Comparison Table

| Feature | pdfLaTeX | XeLaTeX | LuaLaTeX |
|---------|----------|---------|----------|
| Speed | ⚡⚡⚡ Fast | ⚡⚡ Medium | ⚡⚡ Medium |
| Fonts | Type 1 only | System fonts | System fonts |
| Unicode | Limited | Full | Full |
| Packages | Most | Most | Growing |
| Output | PDF | PDF | PDF |
| Use case | Standard | Fonts/Unicode | Advanced |

## Installation

### Windows

**MiKTeX**: All engines included automatically.

**TeX Live**:
```bash
# All engines are included
xelatex --version
lualatex --version
```

### macOS

**MacTeX**: All engines included.

**BasicTeX**:
```bash
sudo tlmgr install xetex luatex fontspec
```

### Linux

**Full installation** includes everything.

**Minimal installation**:
```bash
# Ubuntu/Debian
sudo apt install texlive-xetex texlive-luatex texlive-latex-extra

# Fedora
sudo dnf install texlive-xetex texlive-luatex texlive-fontspec

# Arch
sudo pacman -S texlive-core texlive-fontsextra
```

## Command Line Usage

```bash
# pdfLaTeX
pdflatex document.tex

# XeLaTeX
xelatex document.tex

# LuaLaTeX
lualatex document.tex

# With latexmk
latexmk -pdf document.tex        # pdfLaTeX
latexmk -xelatex document.tex    # XeLaTeX
latexmk -lualatex document.tex   # LuaLaTeX
```

## Editor Configuration

### Specify Engine in Document

Add to the **first line** of your `.tex` file:

```latex
% !TEX program = xelatex
\documentclass{article}
...
```

Supported values: `pdflatex`, `xelatex`, `lualatex`, `latex`

### TeXstudio

**Options → Configure TeXstudio → Build → Default Compiler**

Choose: pdfLaTeX, XeLaTeX, LuaLaTeX, or LaTeX

Or use **Tools menu** for one-time compilation with specific engine.

### Visual Studio Code (LaTeX Workshop)

Add to `.vscode/settings.json`:

```json
{
    "latex-workshop.latex.recipes": [
        {"name": "XeLaTeX", "tools": ["xelatex"]},
        {"name": "LuaLaTeX", "tools": ["lualatex"]},
        {"name": "pdfLaTeX", "tools": ["pdflatex"]}
    ],
    "latex-workshop.latex.tools": [
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
            "name": "pdflatex",
            "command": "pdflatex",
            "args": ["-interaction=nonstopmode", "-synctex=1", "%DOC%"]
        }
    ]
}
```

Press **Ctrl+Alt+B** (Windows/Linux) or **Cmd+Option+B** (macOS) to select recipe.

### Overleaf

**Menu → Compiler** → Choose pdfLaTeX, XeLaTeX, or LuaLaTeX

## Using System Fonts (XeLaTeX/LuaLaTeX)

### Basic Example

```latex
\documentclass{article}
\usepackage{fontspec}

\setmainfont{Times New Roman}
\setsansfont{Arial}
\setmonofont{Courier New}

\begin{document}
This uses system fonts!
\end{document}
```

Compile with `xelatex` or `lualatex`.

### Finding Available Fonts

**Windows**:
- Check `C:\Windows\Fonts\`
- Or use Font Settings app

**macOS**:
```bash
fc-list : family | sort | uniq
# Or use Font Book.app
```

**Linux**:
```bash
fc-list : family | sort | uniq
fc-list | grep -i "liberation"
```

### Font Package Requirements

For XeLaTeX/LuaLaTeX, you need:

```bash
# Install fontspec
tlmgr install fontspec

# Optional but recommended
tlmgr install unicode-math
tlmgr install tex-gyre
tlmgr install tex-gyre-math
```

## Common Issues

### "fontspec error: The fontspec package requires XeTeX or LuaTeX"

**Problem**: Document uses `fontspec` but compiled with pdfLaTeX.

**Solution**: 
```bash
# Change to XeLaTeX
xelatex document.tex
# Or LuaLaTeX
lualatex document.tex
```

### Font Not Found

**Problem**: System font not available or wrong name.

**Solution**:
```bash
# List fonts to find exact name
fc-list : family | grep -i "font-name"

# Use exact font name in document
\setmainfont{Exact Font Name}
```

### Package Incompatibility

**Problem**: Some packages don't work with XeLaTeX/LuaLaTeX.

**Solution**: 
- Check package documentation
- Use package alternatives designed for modern engines
- Consider staying with pdfLaTeX if compatibility is critical

## Best Practices

1. **Start with pdfLaTeX** unless you need specific features
2. **Use XeLaTeX** when you need system fonts or Unicode
3. **Use LuaLaTeX** for very large or complex documents
4. **Specify engine** in document with `% !TEX program =` comment
5. **Install fontspec** if using XeLaTeX/LuaLaTeX
6. **Test compilation** after switching engines
7. **Check package compatibility** before switching

## Migration Guide

### From pdfLaTeX to XeLaTeX

1. **Add fontspec**:
   ```latex
   \usepackage{fontspec}
   ```

2. **Remove font encoding** (not needed):
   ```latex
   % Remove these lines:
   % \usepackage[T1]{fontenc}
   % \usepackage[utf8]{inputenc}
   ```

3. **Optionally set fonts**:
   ```latex
   \setmainfont{Your Preferred Font}
   ```

4. **Compile with XeLaTeX**:
   ```bash
   xelatex document.tex
   ```

### From XeLaTeX to LuaLaTeX

Usually works without changes! Same packages, same syntax.

```bash
# Just change the compiler
lualatex document.tex
```

## Performance Tips

- **Draft mode**: Use `\documentclass[draft]{article}` for faster compilation
- **Partial compilation**: Comment out sections during editing
- **Use latexmk**: Automates multiple passes efficiently
- **pdfLaTeX is fastest**: Use it when you don't need modern features

## Additional Resources

- [Fonts Tutorial](../02-formatting/01-fonts.md)
- [Compilation Guide](../04-compilation/01-compiling-latex.md)
- [fontspec Manual](http://mirrors.ctan.org/macros/latex/contrib/fontspec/fontspec.pdf)
- [XeLaTeX vs LuaLaTeX Discussion](https://tex.stackexchange.com/questions/36/differences-between-luatex-context-and-xetex)
