# VS Code + LaTeX Workshop Troubleshooting

This guide addresses common issues when using VS Code with the LaTeX Workshop extension.

## Table of Contents
- [Formatter Issues](#formatter-issues)
- [Compilation Problems](#compilation-problems)
- [PDF Viewer Issues](#pdf-viewer-issues)
- [IntelliSense Not Working](#intellisense-not-working)
- [SyncTeX Issues](#synctex-issues)

---

## Formatter Issues

### Error: "LaTeX formatter is set to 'none'"

**Problem**: LaTeX Workshop shows a warning that the formatter is disabled.

**Solutions**:

#### Solution 1: Enable latexindent (Recommended)

1. **Verify latexindent is installed**:
   ```bash
   # Check if latexindent exists
   latexindent --version
   ```
   
   If not found, it should be included with:
   - TeX Live (full installation)
   - MiKTeX (install `latexindent` package)
   - MacTeX (included by default)

2. **Add to VS Code settings** (`settings.json`):
   ```json
   {
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

3. **Format your document**:
   - Press `Shift+Alt+F` (Windows/Linux) or `Shift+Option+F` (macOS)
   - Or right-click → Format Document

#### Solution 2: Disable the Warning

If you don't need automatic formatting:

```json
{
    "latex-workshop.formatting.latex": "none"
}
```

This explicitly sets it to "none" and suppresses the warning.

#### Solution 3: Use Alternative Formatters

**LaTeX-formatter** (external tool):
```json
{
    "latex-workshop.formatting.latex": "latexformatter",
    "latex-workshop.formatting.latexformatter.path": "/path/to/latexformatter"
}
```

---

## Compilation Problems

### LaTeX command not found

**Problem**: Error message says `pdflatex` or `xelatex` not found.

**Solution**:

1. **Verify installation**:
   ```bash
   pdflatex --version
   xelatex --version
   ```

2. **Add to PATH** (if not found):
   - **Windows**: Add TeX installation to System PATH
     - MiKTeX: `C:\Program Files\MiKTeX\miktex\bin\x64\`
     - TeX Live: `C:\texlive\2024\bin\windows\`
   - **macOS**: Usually automatic, but check:
     ```bash
     echo $PATH | grep tex
     ```
   - **Linux**: Should be in PATH after installation

3. **Restart VS Code** after PATH changes

### Compilation hangs or times out

**Problem**: LaTeX compilation never finishes.

**Solution**:

1. **Check for errors in terminal**:
   - View → Terminal
   - Look for prompts waiting for input

2. **Use non-interactive mode** (should already be configured):
   ```json
   {
       "latex-workshop.latex.tools": [
           {
               "name": "pdflatex",
               "command": "pdflatex",
               "args": [
                   "-interaction=nonstopmode",
                   "-synctex=1",
                   "%DOC%"
               ]
           }
       ]
   }
   ```

3. **Clean auxiliary files**:
   - Right-click in editor → LaTeX Workshop → Clean up auxiliary files

### Package not found errors

**Problem**: `! LaTeX Error: File 'packagename.sty' not found.`

**Solution**:

- **MiKTeX**: Enable automatic package installation
  - MiKTeX Console → Settings → Always install missing packages on-the-fly
  
- **TeX Live**: Install package manually
  ```bash
  tlmgr install packagename
  ```
  
- **macOS (MacTeX)**:
  ```bash
  sudo tlmgr install packagename
  ```

---

## PDF Viewer Issues

### PDF not updating after compilation

**Problem**: Changes don't appear in the PDF viewer.

**Solution**:

1. **Check autoBuild setting**:
   ```json
   {
       "latex-workshop.latex.autoBuild.run": "onSave"
   }
   ```

2. **Manually rebuild**:
   - Press `Ctrl+Alt+B` (Windows/Linux) or `Cmd+Option+B` (macOS)

3. **Clean and rebuild**:
   - Right-click → LaTeX Workshop → Clean up auxiliary files
   - Save file again to trigger rebuild

### PDF viewer shows blank page

**Problem**: PDF opens but shows empty/white page.

**Solution**:

1. **Try different viewer**:
   ```json
   {
       "latex-workshop.view.pdf.viewer": "tab",  // or "browser" or "external"
   }
   ```

2. **Check PDF file directly**:
   - Open the `.pdf` file from file explorer with external viewer
   - If blank there too, it's a compilation issue

3. **Check for errors**:
   - View → Output → Select "LaTeX Compiler" from dropdown
   - Look for errors in compilation log

---

## IntelliSense Not Working

### No autocomplete suggestions

**Problem**: Package commands, environments, or citations don't autocomplete.

**Solution**:

1. **Enable IntelliSense**:
   ```json
   {
       "latex-workshop.intellisense.package.enabled": true,
       "latex-workshop.intellisense.citation.label": "bibtex key",
       "latex-workshop.intellisense.unimathsymbols.enabled": true
   }
   ```

2. **Trigger manually**:
   - Press `Ctrl+Space` to trigger IntelliSense

3. **Check language mode**:
   - Bottom right corner should show "LaTeX"
   - If not, click and select "LaTeX"

### Citations not showing

**Problem**: `\cite{}` doesn't show bibliography entries.

**Solution**:

1. **Ensure `.bib` file exists** and is referenced in your document:
   ```latex
   \bibliography{references}  % for BibTeX
   % or
   \addbibresource{references.bib}  % for BibLaTeX
   ```

2. **Compile with bibliography**:
   - Use `latexmk` recipe or
   - Manually run: pdfLaTeX → BibTeX → pdfLaTeX → pdfLaTeX

---

## SyncTeX Issues

### Forward/Reverse search not working

**Problem**: Can't jump between `.tex` source and PDF.

**Solution**:

1. **Ensure SyncTeX is enabled**:
   ```json
   {
       "latex-workshop.synctex.afterBuild.enabled": true
   }
   ```

2. **Verify compilation includes `-synctex=1`**:
   ```json
   {
       "latex-workshop.latex.tools": [
           {
               "name": "pdflatex",
               "command": "pdflatex",
               "args": [
                   "-interaction=nonstopmode",
                   "-synctex=1",  // This is required!
                   "%DOC%"
               ]
           }
       ]
   }
   ```

3. **Recompile after enabling SyncTeX**

4. **Use correct shortcuts**:
   - **Forward search** (source → PDF): `Ctrl+Alt+J`
   - **Reverse search** (PDF → source): `Ctrl+Click` on PDF

---

## Choosing Compilation Recipe

LaTeX Workshop provides multiple ways to select which recipe (compilation method) to use for building your document.

### Method 1: Build LaTeX Project Menu (Easiest)

1. **Click the TeX icon** in the left sidebar (Activity Bar)
2. Under **"Build LaTeX project"** section, you'll see:
   - **Build LaTeX project** - Uses default recipe
   - **Recipe: latexmk** - Click to use specific recipe
   - **Recipe: XeLaTeX** - Click to use XeLaTeX
   - **Recipe: pdfLaTeX → BibTeX → pdfLaTeX × 2** - For documents with bibliographies
   - Other custom recipes you've defined

3. **Click on any recipe** to compile with that specific method

### Method 2: Command Palette

1. Press `Ctrl+Shift+P` (Windows/Linux) or `Cmd+Shift+P` (macOS)
2. Type "LaTeX Workshop: Build with recipe"
3. Select your desired recipe from the list

**Keyboard shortcut**: `Ctrl+Alt+B` (or `Cmd+Option+B` on macOS)

### Method 3: Magic Comments (Recommended for Specific Engines)

Add special comments at the **top of your `.tex` file** to specify the compilation method:

```latex
% !TEX program = xelatex
% !BIB program = biber

\documentclass{article}
...
```

**Supported magic comments**:
- `% !TEX program = pdflatex` - Use pdfLaTeX
- `% !TEX program = xelatex` - Use XeLaTeX
- `% !TEX program = lualatex` - Use LuaLaTeX
- `% !BIB program = bibtex` - Use BibTeX for bibliography
- `% !BIB program = biber` - Use Biber for bibliography (BibLaTeX)

**Advantages**:
- Recipe choice is embedded in the document
- Portable - works for anyone who opens the file
- Automatically selects correct engine when building

### Method 4: Default Recipe Setting

Set a default recipe in your `settings.json`:

```json
{
    "latex-workshop.latex.recipe.default": "lastUsed"  // or "first"
}
```

Options:
- `"lastUsed"` - Uses the last recipe you selected
- `"first"` - Always uses the first recipe in your recipes list

### Method 5: Right-Click Context Menu

1. **Right-click** anywhere in your `.tex` file
2. Select **"Build LaTeX Project"** from context menu
3. This uses the default recipe

### Example Recipes Configuration

Here's a comprehensive `settings.json` with multiple recipes including XeLaTeX:

```json
{
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
            "name": "pdfLaTeX → BibTeX → pdfLaTeX × 2",
            "tools": ["pdflatex", "bibtex", "pdflatex", "pdflatex"]
        },
        {
            "name": "XeLaTeX → Biber → XeLaTeX × 2",
            "tools": ["xelatex", "biber", "xelatex", "xelatex"]
        }
    ],
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
            "name": "xelatexmk",
            "command": "latexmk",
            "args": ["-xelatex", "-interaction=nonstopmode", "-synctex=1", "%DOC%"]
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

### When to Use Which Recipe

- **latexmk (pdfLaTeX)**: Default, fastest, works for most documents
- **XeLaTeX**: When using system fonts, Unicode characters, or fontspec package
- **LuaLaTeX**: Advanced font features, Lua scripting, complex typography
- **pdfLaTeX → BibTeX → pdfLaTeX × 2**: Documents with BibTeX bibliographies
- **XeLaTeX → Biber → XeLaTeX × 2**: XeLaTeX documents with BibLaTeX bibliographies

### Troubleshooting Recipe Selection

**Problem**: Magic comment not working

**Solution**:
1. Ensure magic comment is at the **very top** of the file (before `\documentclass`)
2. Check spelling: must be exactly `% !TEX program = xelatex` (case-insensitive)
3. Reload VS Code window: `Ctrl+Shift+P` → "Reload Window"

**Problem**: Recipe not appearing in menu

**Solution**:
1. Check your `settings.json` syntax (no missing commas, brackets)
2. Ensure recipe names are unique
3. Restart VS Code

---

## General Tips

### Reset to default settings

If all else fails, remove custom LaTeX Workshop settings:

1. Open Command Palette (`Ctrl+Shift+P`)
2. Type "Open Settings (JSON)"
3. Remove all `latex-workshop.*` entries
4. Restart VS Code

### Enable detailed logging

For debugging:

```json
{
    "latex-workshop.message.log.show": true,
    "latex-workshop.message.badbox.show": true
}
```

Check logs:
- View → Output → Select "LaTeX Workshop" from dropdown

### Update LaTeX Workshop

1. Extensions view (`Ctrl+Shift+X`)
2. Find "LaTeX Workshop"
3. Click "Update" if available

---

## Additional Resources

- [LaTeX Workshop Wiki](https://github.com/James-Yu/LaTeX-Workshop/wiki)
- [VS Code LaTeX Setup Guide](../03-setup/01-setup-windows.md)
- [Compilation Guide](../04-compilation/01-compiling-latex.md)

---

## Quick Reference: VS Code Settings Location

### Open settings.json:

1. **Command Palette** (`Ctrl+Shift+P`):
   - Type: "Preferences: Open Settings (JSON)"

2. **Alternative**:
   - File → Preferences → Settings
   - Click the "Open Settings (JSON)" icon (top right)

### Workspace vs. User Settings:

- **User settings**: Apply to all projects
  - Location: `~/.config/Code/User/settings.json` (Linux)
  - Location: `%APPDATA%\Code\User\settings.json` (Windows)
  - Location: `~/Library/Application Support/Code/User/settings.json` (macOS)

- **Workspace settings**: Apply only to current project
  - Location: `<project>/.vscode/settings.json`
  - Recommended for project-specific LaTeX engine choices

---

**Last Updated**: October 2025
