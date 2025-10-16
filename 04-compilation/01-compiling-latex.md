# Compiling LaTeX Documents to PDF

## Introduction

This guide covers various methods and tools for compiling LaTeX source files (`.tex`) into PDF documents.

## LaTeX Compilation Engines

### 1. pdfLaTeX (Most Common)

The traditional and most widely used engine:

```bash
pdflatex document.tex
```

**Pros**:
- Fast compilation
- Wide compatibility
- Standard for most documents
- Extensive package support

**Cons**:
- Limited font support (mainly Type 1 fonts)
- No direct Unicode support
- Cannot use system fonts

**Best for**: Standard documents, academic papers, articles

### 2. XeLaTeX

Modern engine with Unicode and system font support:

```bash
xelatex document.tex
```

**Pros**:
- Full Unicode support
- Can use system fonts (TrueType, OpenType)
- Better multilingual support
- Modern font technologies

**Cons**:
- Slower than pdfLaTeX
- Some packages incompatible

**Best for**: Documents with special fonts, multilingual documents

**Example**:
```latex
\documentclass{article}
\usepackage{fontspec}
\setmainfont{Times New Roman}

\begin{document}
Using system fonts with XeLaTeX!
Unicode: α β γ δ ε 你好
\end{document}
```

### 3. LuaLaTeX

Combines pdfLaTeX speed with XeLaTeX features:

```bash
lualatex document.tex
```

**Pros**:
- Unicode support
- System fonts support
- Lua scripting capabilities
- Better memory management

**Cons**:
- Still maturing
- Some compatibility issues

**Best for**: Complex documents, programmable typesetting

## Compilation Workflows

### Single-Pass Compilation

For simple documents without references:

```bash
pdflatex document.tex
```

### Multi-Pass Compilation

For documents with references, citations, table of contents:

```bash
# First pass: process document
pdflatex document.tex

# Second pass: generate references
pdflatex document.tex

# Third pass: finalize cross-references
pdflatex document.tex
```

### With Bibliography

```bash
# Compile main document
pdflatex document.tex

# Process bibliography
bibtex document

# Recompile to include citations
pdflatex document.tex

# Final pass for cross-references
pdflatex document.tex
```

### With Biblatex/Biber

```bash
pdflatex document.tex
biber document
pdflatex document.tex
pdflatex document.tex
```

## Using latexmk (Recommended)

latexmk automates the compilation process:

### Basic Usage

```bash
# Automatic multi-pass compilation
latexmk -pdf document.tex
```

### Continuous Compilation

Recompile automatically when files change:

```bash
latexmk -pdf -pvc document.tex
```

Press `Ctrl+C` to stop.

### Different Engines

```bash
# Use XeLaTeX
latexmk -xelatex document.tex

# Use LuaLaTeX
latexmk -lualatex document.tex

# Use pdfLaTeX (default)
latexmk -pdf document.tex
```

### Cleaning Up

```bash
# Remove auxiliary files
latexmk -c

# Remove all generated files (including PDF)
latexmk -C
```

### Configuration File

Create `.latexmkrc` in your project directory:

```perl
# Set PDF mode
$pdf_mode = 1;

# Use XeLaTeX
$pdflatex = 'xelatex -interaction=nonstopmode -synctex=1 %O %S';

# Set PDF viewer (Linux example)
$pdf_previewer = 'zathura';

# Clean extra extensions
$clean_ext = 'synctex.gz synctex.gz(busy) run.xml tex.bak bbl bcf fdb_latexmk run tdo %R-blx.bib';
```

## IDE and Editor Integration

### TeXstudio

- **Compile**: Press `F5` or `F6`
- **View**: Automatic preview on compile
- **Settings**: Options → Configure TeXstudio → Commands

### TeXmaker

- **Compile**: Tools → LaTeX or `F1`
- **Quick Build**: Tools → Quick Build or `F1`
- **View**: Tools → View PDF

### Visual Studio Code (LaTeX Workshop)

- **Auto-compile**: Saves automatically compile
- **Manual**: Ctrl+Alt+B (Windows/Linux) or Cmd+Option+B (Mac)
- **View**: Ctrl+Alt+V (Windows/Linux) or Cmd+Option+V (Mac)

**Configuration** (`.vscode/settings.json`):
```json
{
    "latex-workshop.latex.autoBuild.run": "onFileChange",
    "latex-workshop.latex.recipes": [
        {
            "name": "latexmk",
            "tools": ["latexmk"]
        },
        {
            "name": "pdflatex × 2",
            "tools": ["pdflatex", "pdflatex"]
        }
    ],
    "latex-workshop.latex.tools": [
        {
            "name": "latexmk",
            "command": "latexmk",
            "args": [
                "-pdf",
                "-interaction=nonstopmode",
                "-synctex=1",
                "%DOC%"
            ]
        },
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

### Vim/Neovim with vimtex

- **Compile**: `\ll` (default mapping)
- **View**: `\lv`
- **Clean**: `\lc`

### Emacs with AUCTeX

- **Compile**: `C-c C-c` (prompts for command)
- **View**: `C-c C-v`

## Command-Line Options

### Common pdflatex Options

```bash
# Non-stop mode (don't pause on errors)
pdflatex -interaction=nonstopmode document.tex

# Batch mode (suppresses output)
pdflatex -interaction=batchmode document.tex

# Enable SyncTeX (for editor-PDF sync)
pdflatex -synctex=1 document.tex

# Set output directory
pdflatex -output-directory=build document.tex

# Shell escape (for external programs)
pdflatex -shell-escape document.tex

# Draft mode (faster, no images)
pdflatex -draftmode document.tex
```

### Complete Example

```bash
pdflatex -interaction=nonstopmode -synctex=1 -output-directory=build document.tex
```

## Makefile for Automation

Create `Makefile`:

```makefile
# Main file without extension
MAIN = document

# LaTeX compiler
LATEX = pdflatex
BIBTEX = bibtex

# Flags
LATEXFLAGS = -interaction=nonstopmode -synctex=1

# Output
PDF = $(MAIN).pdf

.PHONY: all clean view watch

all: $(PDF)

$(PDF): $(MAIN).tex
	$(LATEX) $(LATEXFLAGS) $(MAIN)
	$(BIBTEX) $(MAIN) || true
	$(LATEX) $(LATEXFLAGS) $(MAIN)
	$(LATEX) $(LATEXFLAGS) $(MAIN)

clean:
	rm -f *.aux *.log *.out *.toc *.bbl *.blg *.synctex.gz

distclean: clean
	rm -f $(PDF)

view: $(PDF)
	xdg-open $(PDF) &

watch:
	latexmk -pdf -pvc $(MAIN)
```

Usage:
```bash
make          # Compile
make view     # Open PDF
make clean    # Remove aux files
make watch    # Continuous compilation
```

## Shell Scripts

### Simple Compile Script

```bash
#!/bin/bash
# compile.sh

FILE=${1:-document.tex}
BASE=${FILE%.tex}

pdflatex -interaction=nonstopmode "$FILE"
bibtex "$BASE" 2>/dev/null
pdflatex -interaction=nonstopmode "$FILE"
pdflatex -interaction=nonstopmode "$FILE"

echo "✓ Compilation complete: $BASE.pdf"
```

Usage:
```bash
chmod +x compile.sh
./compile.sh document.tex
```

### Advanced Script with Error Checking

```bash
#!/bin/bash
# build.sh

set -e

FILE=${1:-document.tex}
BASE=${FILE%.tex}
ENGINE=${2:-pdflatex}

echo "Compiling $FILE with $ENGINE..."

# First pass
$ENGINE -interaction=nonstopmode -synctex=1 "$FILE"

# Bibliography if .bib exists
if ls *.bib 1> /dev/null 2>&1; then
    echo "Processing bibliography..."
    bibtex "$BASE" || true
fi

# Final passes
$ENGINE -interaction=nonstopmode -synctex=1 "$FILE"
$ENGINE -interaction=nonstopmode -synctex=1 "$FILE"

echo "✓ Success: $BASE.pdf"

# Open PDF
if command -v xdg-open &> /dev/null; then
    xdg-open "$BASE.pdf" &
fi
```

Usage:
```bash
./build.sh document.tex
./build.sh document.tex xelatex
```

## Debugging Compilation Errors

### Reading Error Messages

Error format:
```
! LaTeX Error: File `package.sty' not found.
```

Key information:
- `!` indicates error
- Line number usually provided
- Error description follows

### Common Strategies

1. **Check the .log file**:
   ```bash
   less document.log
   # Search for "Error" or "!"
   ```

2. **Compile with errors shown**:
   ```bash
   pdflatex -interaction=errorstopmode document.tex
   ```

3. **Check for missing packages**:
   ```bash
   tlmgr search --global --file <missing-file>
   ```

4. **Isolate the problem**:
   Comment out sections until document compiles

### Common Errors

| Error | Cause | Solution |
|-------|-------|----------|
| File not found | Missing package/file | Install package or check path |
| Undefined control sequence | Typo or missing package | Check command spelling |
| Missing $ inserted | Math without $ | Add math delimiters |
| Overfull/Underfull hbox | Text overflow | Rephrase or adjust margins |
| ! Emergency stop | Serious error | Check log for specifics |

## Output Management

### Organize Output Files

Keep auxiliary files separate:

```bash
# Create build directory
mkdir -p build

# Compile to build directory
pdflatex -output-directory=build document.tex

# Copy PDF back
cp build/document.pdf .
```

### latexmk Configuration

In `.latexmkrc`:
```perl
$out_dir = 'build';
$pdf_mode = 1;
$pdflatex = 'pdflatex -interaction=nonstopmode -synctex=1 %O %S';
```

## SyncTeX (Editor-PDF Synchronization)

Enable source-PDF syncing:

```bash
pdflatex -synctex=1 document.tex
```

**Usage**:
- Forward search: Click in editor → jump to PDF location
- Backward search: Click in PDF → jump to source location

Supported by TeXstudio, TeXmaker, VS Code, Vim (with proper setup).

## Parallel Compilation

For documents with independent chapters:

```bash
# Compile chapters in parallel
pdflatex chapter1.tex &
pdflatex chapter2.tex &
pdflatex chapter3.tex &
wait

# Combine PDFs (using pdftk)
pdftk chapter1.pdf chapter2.pdf chapter3.pdf cat output complete.pdf
```

## Best Practices

1. **Use latexmk**: Automates complexity
2. **Version control**: Git for `.tex` files, ignore auxiliary files
3. **Build directory**: Keep source clean
4. **Error checking**: Address warnings
5. **Incremental builds**: Use `-draftmode` for speed
6. **Modern engines**: Use XeLaTeX/LuaLaTeX for complex typography
7. **SyncTeX**: Enable for efficient editing

## Performance Tips

1. **Draft mode**: `\documentclass[draft]{article}`
2. **Selective compilation**: `\include` with `\includeonly`
3. **Precompiled headers**: For large packages
4. **SSD storage**: Faster I/O
5. **Reduce images**: Lower resolution for drafts

## Engine Comparison

| Feature | pdfLaTeX | XeLaTeX | LuaLaTeX |
|---------|----------|---------|----------|
| Speed | Fast | Medium | Medium |
| Fonts | Limited | System fonts | System fonts |
| Unicode | Basic | Full | Full |
| Packages | Most | Most | Growing |
| Best for | Standard docs | Fonts | Programmable |

## Next Steps

- Learn about [document structure](../01-basics/01-document-structure.md)
- Explore [fonts](../02-formatting/01-fonts.md)
- Check [setup guides](../03-setup/) for your OS
- Try [example documents](../../examples/)

## Resources

- latexmk documentation: `man latexmk`
- TeX Stack Exchange: https://tex.stackexchange.com/
- LaTeX Wikibook: https://en.wikibooks.org/wiki/LaTeX/
