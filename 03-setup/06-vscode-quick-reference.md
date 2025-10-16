# Quick Reference: VS Code LaTeX Workshop Configuration

This document provides a quick reference for configuring VS Code with LaTeX Workshop, including all common recipes and how to use them.

## Complete Settings Configuration

Copy this into your `settings.json` (see below for location):

```json
{
    // LaTeX Formatter Configuration
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
    },
    
    // Auto-build and PDF viewer
    "latex-workshop.latex.autoBuild.run": "onSave",
    "latex-workshop.view.pdf.viewer": "tab",
    
    // Recipes (compilation methods)
    "latex-workshop.latex.recipes": [
        {
            "name": "latexmk (pdfLaTeX)",
            "tools": ["latexmk"]
        },
        {
            "name": "XeLaTeX",
            "tools": ["xelatex"]
        },
        {
            "name": "latexmk (XeLaTeX)",
            "tools": ["xelatexmk"]
        },
        {
            "name": "LuaLaTeX",
            "tools": ["lualatex"]
        },
        {
            "name": "pdfLaTeX -> BibTeX -> pdfLaTeX * 2",
            "tools": ["pdflatex", "bibtex", "pdflatex", "pdflatex"]
        },
        {
            "name": "XeLaTeX -> Biber -> XeLaTeX * 2",
            "tools": ["xelatex", "biber", "xelatex", "xelatex"]
        }
    ],
    
    // Tools (individual commands)
    "latex-workshop.latex.tools": [
        {
            "name": "latexmk",
            "command": "latexmk",
            "args": ["-pdf", "-interaction=nonstopmode", "-synctex=1", "%DOC%"]
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
            "name": "xelatexmk",
            "command": "latexmk",
            "args": ["-xelatex", "-interaction=nonstopmode", "-synctex=1", "%DOC%"]
        },
        {
            "name": "pdflatex",
            "command": "pdflatex",
            "args": ["-interaction=nonstopmode", "-synctex=1", "%DOC%"]
        },
        {
            "name": "bibtex",
            "command": "bibtex",
            "args": ["%DOCFILE%"]
        },
        {
            "name": "biber",
            "command": "biber",
            "args": ["%DOCFILE%"]
        }
    ]
}
```

## How to Open settings.json

### Method 1: Command Palette (Easiest)
1. Press `Ctrl+Shift+P` (Windows/Linux) or `Cmd+Shift+P` (macOS)
2. Type: **"Preferences: Open Settings (JSON)"**
3. Press Enter

### Method 2: Settings UI
1. Go to File → Preferences → Settings (or `Ctrl+,`)
2. Click the **"Open Settings (JSON)"** icon in the top-right corner

### Method 3: Direct File Access

**Windows**: `%APPDATA%\Code\User\settings.json`
```
C:\Users\YourUsername\AppData\Roaming\Code\User\settings.json
```

**macOS**: `~/Library/Application Support/Code/User/settings.json`

**Linux**: `~/.config/Code/User/settings.json`

## How to Choose Compilation Recipe

### 🎯 Method 1: Sidebar (Easiest)
1. Click the **TeX icon** in the left sidebar
2. Under "Build LaTeX project", click any recipe:
   - **XeLaTeX**
   - **latexmk (pdfLaTeX)**
   - **pdfLaTeX → BibTeX → pdfLaTeX × 2**

### ⌨️ Method 2: Keyboard Shortcut
1. Press `Ctrl+Alt+B` (Windows/Linux) or `Cmd+Option+B` (macOS)
2. Select recipe from dropdown menu

### 🪄 Method 3: Magic Comments (Recommended)
Add at the **top** of your `.tex` file:

```latex
% !TEX program = xelatex
% !BIB program = biber

\documentclass{article}
...
```

**Available programs**:
- `pdflatex` - Default engine
- `xelatex` - For Unicode and system fonts
- `lualatex` - Advanced features
- `bibtex` - Classic bibliography
- `biber` - Modern bibliography (BibLaTeX)

### 🖱️ Method 4: Command Palette
1. Press `Ctrl+Shift+P` (or `Cmd+Shift+P`)
2. Type: **"LaTeX Workshop: Build with recipe"**
3. Select your recipe

### 📝 Method 5: Right-Click
1. Right-click in your `.tex` file
2. Select **"Build LaTeX Project"**
3. Uses default recipe

## Recipe Cheat Sheet

| Recipe | When to Use | Speed | Features |
|--------|-------------|-------|----------|
| **latexmk (pdfLaTeX)** | Default, most documents | ⚡⚡⚡ Fast | Standard LaTeX |
| **XeLaTeX** | Unicode, system fonts, fontspec | ⚡⚡ Medium | Modern fonts |
| **LuaLaTeX** | Lua scripting, complex typography | ⚡ Slow | Most features |
| **pdfLaTeX + BibTeX** | Documents with bibliography | ⚡⚡ Medium | Classic citations |
| **XeLaTeX + Biber** | Unicode docs with bibliography | ⚡ Slow | Modern everything |

## Common Keyboard Shortcuts

| Action | Windows/Linux | macOS |
|--------|--------------|-------|
| Build LaTeX | `Ctrl+Alt+B` | `Cmd+Option+B` |
| View PDF | `Ctrl+Alt+V` | `Cmd+Option+V` |
| Format Document | `Shift+Alt+F` | `Shift+Option+F` |
| SyncTeX (forward) | `Ctrl+Alt+J` | `Cmd+Option+J` |
| SyncTeX (reverse) | `Ctrl+Click` | `Cmd+Click` |

## When to Use Each Engine

### Use pdfLaTeX when:
- ✅ Writing standard academic papers
- ✅ Speed is important
- ✅ Using only ASCII or basic accented characters
- ✅ Not using system fonts

### Use XeLaTeX when:
- ✅ Using Unicode characters (中文, العربية, etc.)
- ✅ Need system fonts (Arial, Times New Roman, etc.)
- ✅ Using `fontspec` package
- ✅ Writing multilingual documents

Example with XeLaTeX:
```latex
% !TEX program = xelatex
\documentclass{article}
\usepackage{fontspec}
\setmainfont{Times New Roman}

\begin{document}
Hello 世界! مرحبا
\end{document}
```

### Use LuaLaTeX when:
- ✅ Need Lua scripting capabilities
- ✅ Processing large documents
- ✅ Advanced typography features
- ✅ Custom document processing

## Quick Fixes

### "Formatter is set to 'none'" Error
Add to settings.json:
```json
{
    "latex-workshop.formatting.latex": "latexindent"
}
```

### PDF not updating
1. Save file (`Ctrl+S`)
2. Check: `"latex-workshop.latex.autoBuild.run": "onSave"`

### Magic comment not working
1. Must be at **top** of file (before `\documentclass`)
2. Check spelling exactly: `% !TEX program = xelatex`
3. Reload window: `Ctrl+Shift+P` → "Reload Window"

### Recipe not appearing
1. Check JSON syntax (commas, brackets)
2. Restart VS Code
3. Check extension is installed and updated

## Additional Resources

📖 **Full Documentation**:
- [Complete Troubleshooting Guide](05-vscode-troubleshooting.md)
- [Windows Setup Guide](01-setup-windows.md)
- [LaTeX Engines Comparison](04-latex-engines.md)
- [Compilation Guide](../04-compilation/01-compiling-latex.md)

🔧 **Official Resources**:
- [LaTeX Workshop Wiki](https://github.com/James-Yu/LaTeX-Workshop/wiki)
- [VS Code Documentation](https://code.visualstudio.com/docs)

---

**Last Updated**: October 2025
