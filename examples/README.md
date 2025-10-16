# LaTeX Examples

This directory contains complete, working LaTeX examples that demonstrate various features and document types.

## Available Examples

### 1. Simple Article (`simple_article.tex`)

A basic academic article template demonstrating:
- Document structure and organization
- Mathematical equations (inline and display)
- Lists (itemize, enumerate)
- Tables with formatting
- Cross-references
- Bibliography

**View the tutorial**: [01-simple-article.md](01-simple-article.md)

**Compile**:
```bash
# Using pdfLaTeX
pdflatex simple_article.tex

# Using latexmk (recommended)
latexmk -pdf simple_article.tex

# Continuous compilation (auto-recompile on save)
latexmk -pdf -pvc simple_article.tex

# Using Make (easiest!)
make              # Compile
make view         # Compile and open PDF
make clean        # Remove auxiliary files
make watch        # Continuous compilation
```

**Clean up**:
```bash
latexmk -c  # Remove auxiliary files
latexmk -C  # Remove all generated files including PDF

# Or using Make
make clean        # Remove auxiliary files
make distclean    # Remove all generated files
```

## How to Use These Examples

### 1. Copy and Modify

```bash
# Copy example to your project
cp simple_article.tex my_document.tex

# Edit the file
nano my_document.tex  # or use your preferred editor

# Compile
pdflatex my_document.tex
```

### 2. Learn by Experimenting

- Modify sections and see what changes
- Try different packages
- Adjust formatting options
- Add your own content

### 3. Use as Templates

These examples serve as starting points for:
- Academic papers
- Technical reports
- Research articles
- Class assignments
- Thesis chapters

## File Structure

Each example includes:

- **`.tex` file** - The actual LaTeX source code (ready to compile)
- **`.md` file** - Tutorial with explanations and customization tips

## Prerequisites

Ensure you have LaTeX installed:
- **Windows**: [MiKTeX](../03-setup/01-setup-windows.md) or [TeX Live](../03-setup/01-setup-windows.md)
- **macOS**: [MacTeX](../03-setup/02-setup-macos.md)
- **Linux**: [TeX Live](../03-setup/03-setup-linux.md)

## Compilation Tips

### Multiple Passes

Some features (like cross-references) require multiple compilation passes:

```bash
# Manual approach
pdflatex document.tex  # First pass
pdflatex document.tex  # Second pass (resolves references)

# Automatic approach (recommended)
latexmk -pdf document.tex
```

### With Bibliography

If the example includes a bibliography:

```bash
pdflatex document.tex
bibtex document
pdflatex document.tex
pdflatex document.tex

# Or use latexmk
latexmk -pdf document.tex
```

### Different Engines

```bash
# Use XeLaTeX (for system fonts)
xelatex simple_article.tex

# Use LuaLaTeX
lualatex simple_article.tex

# With latexmk
latexmk -xelatex simple_article.tex
latexmk -lualatex simple_article.tex
```

See [LaTeX Engines Guide](../03-setup/04-latex-engines.md) for more details.

## Troubleshooting

### Missing Packages

**Error**: `File 'package.sty' not found`

**Solution**:
```bash
# MiKTeX (Windows) - usually automatic
# Or manually: mpm --install=package-name

# TeX Live (macOS/Linux)
sudo tlmgr install package-name
```

### Compilation Errors

1. **Read the error message** - It usually indicates the line number
2. **Check the `.log` file** - Contains detailed information
3. **Compile again** - Sometimes a second pass resolves issues
4. **Comment out sections** - Isolate the problem area

### PDF Not Generated

- Check for error messages in terminal/console
- Look for errors in the `.log` file
- Ensure all required packages are installed
- Try compiling with `pdflatex -interaction=nonstopmode`

## Customization Ideas

### Change Paper Size

```latex
\documentclass[11pt,letterpaper]{article}  % US Letter
% or
\documentclass[11pt,a4paper]{article}      % A4
```

### Adjust Margins

```latex
\usepackage[margin=1.5in]{geometry}
% or
\usepackage[top=1in, bottom=1in, left=1.25in, right=1.25in]{geometry}
```

### Change Fonts

```latex
\usepackage{times}      % Times font
\usepackage{palatino}   % Palatino font
\usepackage{helvet}     % Helvetica (sans serif)
```

### Line Spacing

```latex
\usepackage{setspace}
\onehalfspacing  % 1.5 spacing
% or
\doublespacing   % Double spacing
```

### Add Headers/Footers

```latex
\usepackage{fancyhdr}
\pagestyle{fancy}
\fancyhead[L]{Left Header}
\fancyhead[C]{Center Header}
\fancyhead[R]{Right Header}
\fancyfoot[C]{\thepage}
```

## Additional Resources

- [Document Structure Tutorial](../01-basics/01-document-structure.md)
- [Text Formatting Guide](../01-basics/02-text-formatting-basics.md)
- [Compilation Guide](../04-compilation/01-compiling-latex.md)
- [LaTeX Resources](../06-resources/01-useful-sites.md)

## Contributing Examples

Have a useful LaTeX example to share? Contributions are welcome!

1. Create both `.tex` and `.md` files
2. Follow the existing format
3. Include clear comments in the LaTeX code
4. Test that it compiles successfully
5. Submit a pull request

See [Contributing Guidelines](../README.md#contributing) for details.

## Coming Soon

More examples for:
- Beamer presentations
- CV/Resume templates
- Thesis/dissertation templates
- Technical reports
- Lab reports
- Book chapters
- Letters

---

**Happy LaTeXing!** 📄✨

For questions or issues, see the [main README](../README.md) or open an issue on GitHub.
