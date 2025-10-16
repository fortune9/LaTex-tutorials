# Fonts in LaTeX

## Introduction

LaTeX provides comprehensive font management capabilities, allowing you to control font families, sizes, weights, and styles throughout your document.

## Font Families

LaTeX has three main font families:

### 1. Roman (Serif) - Default

```latex
\textrm{Roman text}
{\rmfamily This is roman text}
```

### 2. Sans Serif

```latex
\textsf{Sans serif text}
{\sffamily This is sans serif text}
```

### 3. Typewriter (Monospace)

```latex
\texttt{Typewriter text}
{\ttfamily This is typewriter text}
```

## Font Styles

### Weight and Shape

```latex
\textbf{Bold face}
\textmd{Medium weight (default)}

\textit{Italic}
\textsl{Slanted}
\textsc{Small Caps}
\textup{Upright (default)}
```

### Combining Styles

```latex
\textbf{\textit{Bold italic}}
\textsf{\textbf{Sans serif bold}}
\texttt{\textbf{Bold typewriter}}
```

## Font Sizes

### Relative Sizing

```latex
{\tiny tiny}
{\scriptsize scriptsize}
{\footnotesize footnotesize}
{\small small}
{\normalsize normalsize}
{\large large}
{\Large Large}
{\LARGE LARGE}
{\huge huge}
{\Huge Huge}
```

### Absolute Sizing

```latex
\fontsize{12pt}{14pt}\selectfont Specific font size
```

The first parameter is the font size, the second is the baseline skip (line spacing).

## Popular Font Packages

### Computer Modern (Default)

LaTeX's default font - no package needed.

### Latin Modern

```latex
\usepackage{lmodern}
```

Modern version of Computer Modern with better PDF rendering.

### Times-like Fonts

```latex
\usepackage{mathptmx}  % Times for text and math
\usepackage{newtxtext, newtxmath}  % New TX fonts
```

### Palatino

```latex
\usepackage{palatino}
\usepackage{newpxtext, newpxmath}  % Modern alternative
```

### Helvetica (Sans Serif)

```latex
\usepackage{helvet}
\renewcommand{\familydefault}{\sfdefault}
```

### Courier (Monospace)

```latex
\usepackage{courier}
```

### Bookman

```latex
\usepackage{bookman}
```

## Modern Font Systems

### fontspec (XeLaTeX/LuaLaTeX)

Use system fonts with XeLaTeX or LuaLaTeX:

```latex
\usepackage{fontspec}
\setmainfont{Times New Roman}
\setsansfont{Arial}
\setmonofont{Courier New}
```

Example with custom fonts:

```latex
\usepackage{fontspec}
\setmainfont{TeX Gyre Termes}  % Times-like
\setsansfont{TeX Gyre Heros}   % Helvetica-like
\setmonofont{TeX Gyre Cursor}  % Courier-like
```

## Font Encoding

### Traditional LaTeX (pdfLaTeX)

```latex
\usepackage[T1]{fontenc}
\usepackage[utf8]{inputenc}
```

### Modern Engines (XeLaTeX/LuaLaTeX)

```latex
\usepackage{fontspec}
% UTF-8 support is automatic
```

## Changing Default Font Family

```latex
% Use sans serif as default
\renewcommand{\familydefault}{\sfdefault}

% Use typewriter as default
\renewcommand{\familydefault}{\ttdefault}
```

## Complete Example

```latex
\documentclass{article}

% Traditional approach (pdfLaTeX)
\usepackage[T1]{fontenc}
\usepackage[utf8]{inputenc}
\usepackage{lmodern}

% Font packages
\usepackage{helvet}  % Sans serif
\usepackage{courier} % Monospace

\begin{document}

\section{Font Family Examples}

Default roman text with \textbf{bold} and \textit{italic}.

\textsf{This is sans serif text with \textbf{bold}.}

\texttt{This is typewriter text with \textbf{bold}.}

\section{Font Size Examples}

{\tiny Tiny text} 
{\small small text} 
{\normalsize normal text} 
{\large large text} 
{\Huge Huge text}

\section{Mixed Formatting}

\textbf{\large Bold and Large}

\textsf{\textit{Sans serif italic}}

\textsc{Small Caps Text}

\end{document}
```

## Modern Example with fontspec

```latex
\documentclass{article}

\usepackage{fontspec}

% Set fonts
\setmainfont{TeX Gyre Termes}
\setsansfont{TeX Gyre Heros}
\setmonofont{TeX Gyre Cursor}

% Optional: set different fonts for specific purposes
\newfontfamily\headingfont{TeX Gyre Adventor}

\begin{document}

\section{Modern Font Usage}

This document uses TeX Gyre fonts for professional typography.

\textsf{Sans serif text for contrast.}

\texttt{Monospace for code: def hello(): print("Hi")}

{\headingfont Custom font family for special text.}

\end{document}
```

## Best Practices

1. **Consistency**: Stick to one or two font families per document
2. **Readability**: Use serif fonts for body text, sans serif for headings
3. **Monospace**: Reserve for code, file paths, and technical terms
4. **Modern engines**: Use XeLaTeX/LuaLaTeX with fontspec for better font support
5. **Encoding**: Always use `\usepackage[T1]{fontenc}` with pdfLaTeX
6. **Math fonts**: Ensure math fonts match your text fonts

## Font Comparison Table

| Package | Text Font | Math Support | Engine |
|---------|-----------|--------------|--------|
| lmodern | Latin Modern | Yes | pdfLaTeX |
| mathptmx | Times | Yes | pdfLaTeX |
| newtxtext | Times | With newtxmath | pdfLaTeX |
| newpxtext | Palatino | With newpxmath | pdfLaTeX |
| fontspec | Any system font | Requires unicode-math | XeLaTeX/LuaLaTeX |

## Troubleshooting

- **Fonts look pixelated in PDF**: Use vector fonts like `lmodern`
- **Special characters missing**: Check font encoding (`\usepackage[T1]{fontenc}`)
- **Math fonts don't match**: Use matching math font packages
- **System fonts not working**: Use XeLaTeX/LuaLaTeX with fontspec

## Next Steps

- Learn about [margins and spacing](02-margins-spacing.md)
- Explore [document structure](../01-basics/01-document-structure.md)
- Study [compilation methods](../04-compilation/01-compiling-latex.md)
