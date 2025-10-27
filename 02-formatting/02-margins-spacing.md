# Page Margins and Spacing in LaTeX

## Introduction

Proper page layout is crucial for creating professional-looking documents. This tutorial covers how to control margins, spacing, and overall page geometry in LaTeX.

## The geometry Package

The `geometry` package is the most powerful and flexible way to control page layout:

```latex
\usepackage{geometry}
```

### Setting All Margins

```latex
% Set all margins to 1 inch
\geometry{margin=1in}

% Set all margins to 2.5 cm
\geometry{margin=2.5cm}
```

### Individual Margin Control

```latex
\geometry{
    top=2cm,
    bottom=2cm,
    left=2.5cm,
    right=2.5cm
}
```

### Paper Size

```latex
% US Letter (default)
\geometry{letterpaper}

% A4 (European standard)
\geometry{a4paper}

% Other sizes
\geometry{legalpaper}
\geometry{b5paper}
```

### Complete Example

```latex
\usepackage[
    a4paper,
    top=2.5cm,
    bottom=2.5cm,
    left=3cm,
    right=3cm,
    headheight=14pt
]{geometry}
```

## Alternative: Manual Margin Setting

Without the geometry package (not recommended):

```latex
\setlength{\topmargin}{0cm}
\setlength{\oddsidemargin}{0cm}
\setlength{\evensidemargin}{0cm}
\setlength{\textwidth}{16cm}
\setlength{\textheight}{23cm}
```

## Line Spacing

### setspace Package

```latex
\usepackage{setspace}

% Double spacing
\doublespacing

% One and a half spacing
\onehalfspacing

% Single spacing (default)
\singlespacing

% Custom spacing
\setstretch{1.25}
```

### Local Spacing Changes

```latex
\begin{spacing}{1.5}
This paragraph has 1.5 line spacing.
\end{spacing}

This paragraph returns to normal spacing.
```

### baselineskip

Manual control of line spacing:

```latex
\setlength{\baselineskip}{1.5\baselineskip}
```

## Paragraph Spacing

### Paragraph Indentation

```latex
% Set indentation width
\setlength{\parindent}{0cm}  % No indentation
\setlength{\parindent}{1em}  % Default indentation

% Remove indentation for one paragraph
\noindent This paragraph is not indented.
```

### Space Between Paragraphs

```latex
\setlength{\parskip}{1em}  % Add space between paragraphs
\setlength{\parskip}{0pt}  % No space (default)
```

## Section Spacing

### Using titlesec Package

```latex
\usepackage{titlesec}

% Adjust spacing around sections
\titlespacing*{\section}
    {0pt}           % left margin
    {3.5ex plus 1ex minus .2ex}  % before spacing
    {2.3ex plus .2ex}  % after spacing

% Adjust subsections
\titlespacing*{\subsection}
    {0pt}
    {3.25ex plus 1ex minus .2ex}
    {1.5ex plus .2ex}
```

## Column Separation

For multi-column documents:

```latex
% Set column separation
\setlength{\columnsep}{1cm}

% Two-column document
\documentclass[twocolumn]{article}
```

## Header and Footer Spacing

```latex
\usepackage{geometry}

\geometry{
    headheight=15pt,  % Height of header
    headsep=12pt,     % Space between header and text
    footskip=30pt     % Space for footer
}
```

## Complete Example

```latex
\documentclass[11pt]{article}

% Geometry package for margins
\usepackage[
    a4paper,
    top=2.5cm,
    bottom=2.5cm,
    left=3cm,
    right=2.5cm,
    headheight=14pt
]{geometry}

% Line spacing
\usepackage{setspace}
\onehalfspacing

% Paragraph spacing
\setlength{\parindent}{1em}
\setlength{\parskip}{0.5em}

% Section spacing
\usepackage{titlesec}
\titlespacing*{\section}
    {0pt}{2ex plus 1ex minus .2ex}{1ex plus .2ex}

\begin{document}

\section{First Section}

This is a paragraph with custom spacing. The margins are set to provide a comfortable reading experience.

This is another paragraph. Notice the spacing between paragraphs and the indentation.

\section{Second Section}

The line spacing is set to one-and-a-half for better readability.

\end{document}
```

## Common Presets

### Academic Paper

```latex
\usepackage[
    letterpaper,
    margin=1in
]{geometry}
\usepackage{setspace}
\doublespacing
```

### Book Layout

```latex
\usepackage[
    a5paper,
    top=2cm,
    bottom=2cm,
    inner=2.5cm,  % Binding side
    outer=2cm
]{geometry}
```

### Narrow Margins for Drafts

```latex
\usepackage[
    margin=0.75in
]{geometry}
```

## Advanced: Dynamic Spacing

### Flexible Spacing

```latex
% Add flexible vertical space
\vspace{1cm plus 2mm minus 1mm}

% Let LaTeX optimize spacing
\vspace{\fill}
```

### Adjust Spacing Factors

```latex
% Stretch factor between paragraphs
\linespread{1.3}

% Spacing around floats
\setlength{\textfloatsep}{10pt plus 2pt minus 2pt}
\setlength{\floatsep}{10pt plus 2pt minus 2pt}
```

## Checking Your Layout

### Show page layout

```latex
\usepackage{geometry}
\geometry{showframe}  % Shows page boundaries
```

### Layout package

```latex
\usepackage{layout}
% In document:
\layout  % Displays layout parameters
```

## Quick Reference: Spacing & Margin Commands Cheatsheet

This section provides a quick lookup for common spacing, margin, and dimension commands used throughout LaTeX.

### Unit Abbreviations

| Unit | Meaning | Size | Usage |
|------|---------|------|-------|
| `em` | Current font width | ~width of letter "M" | Font-relative spacing |
| `ex` | Current font height | ~height of letter "x" | Font-relative heights |
| `pt` | Points | 1/72 inch | Absolute sizing |
| `mm` | Millimeters | 1/10 cm | Metric measurements |
| `cm` | Centimeters | 10mm | Metric measurements |
| `in` | Inches | 2.54 cm | Imperial measurements |
| `pc` | Picas | 12 pt | Typography measurements |
| `bp` | Big points | ~1/72 inch | PDF measurement |
| `sp` | Scaled points | 1/65536 pt | Internal TeX unit |

### Common Spacing Commands

| Command | Purpose | Example | Result |
|---------|---------|---------|--------|
| `\par` | End paragraph, apply spacing | `text\par more text` | Creates paragraph break |
| `\\` | Line break (not paragraph) | `line1\\line2` | New line, same paragraph |
| `\newline` | Forced new line | `text\newline more` | New line without paragraph space |
| `\break` | Line break at optimal point | `text\break more` | Breaks line for better layout |
| `\medskip` | Medium vertical space | `text\medskip text` | ~1.5 lines space |
| `\bigskip` | Big vertical space | `text\bigskip text` | ~3 lines space |
| `\smallskip` | Small vertical space | `text\smallskip text` | ~0.5 lines space |
| `\vspace{1cm}` | Custom vertical space | `\vspace{1cm}` | Exact space: 1 cm |
| `\hspace{1em}` | Horizontal space | `\hspace{1em}text` | Space of width 1em |
| `\quad` | Horizontal space | `text\quad text` | Space equal to font size |
| `\qquad` | Double horizontal space | `text\qquad text` | Space = 2× font size |
| `\:` | Medium space (math mode) | `$a\:b$` | ~3/18 of em |
| `\;` | Large space (math mode) | `$a\;b$` | ~5/18 of em |
| `\,` | Small space (math mode) | `$a\,b$` | ~3/18 of em |
| `\!` | Negative space (math mode) | `$a\!b$` | Removes ~3/18 of em |
| `~` | Non-breaking space | `author~\cite{ref}` | Space that won't break |

### Margin & Page Dimension Commands

| Command | Purpose | Example | Notes |
|---------|---------|---------|-------|
| `\topmargin` | Top margin distance | `\setlength{\topmargin}{0cm}` | Distance from top of page |
| `\headheight` | Header height | `\setlength{\headheight}{14pt}` | Must be ≥ 12pt |
| `\headsep` | Header to text space | `\setlength{\headsep}{12pt}` | Space below header |
| `\textheight` | Text body height | `\setlength{\textheight}{23cm}` | Actual text area height |
| `\textwidth` | Text body width | `\setlength{\textwidth}{16cm}` | Actual text area width |
| `\oddsidemargin` | Left margin (odd pages) | `\setlength{\oddsidemargin}{0cm}` | For single-sided documents |
| `\evensidemargin` | Left margin (even pages) | `\setlength{\evensidemargin}{0cm}` | For two-sided documents |
| `\marginparwidth` | Side note width | `\setlength{\marginparwidth}{2cm}` | Width of margin notes |
| `\marginparsep` | Margin note separation | `\setlength{\marginparsep}{1em}` | Space from text to note |
| `\footskip` | Footer space | `\setlength{\footskip}{30pt}` | Space for footer text |
| `\baselineskip` | Line spacing | `\setlength{\baselineskip}{1.5\baselineskip}` | Space between lines |
| `\parindent` | Paragraph indent | `\setlength{\parindent}{1em}` | First line indent (set 0pt for no indent) |
| `\parskip` | Space between paragraphs | `\setlength{\parskip}{0.5em}` | Add space between paragraphs |

### List and Table Spacing Commands

| Command | Purpose | Example | Typical Value |
|---------|---------|---------|---|
| `\tabcolsep` | Space before/after column | `\setlength{\tabcolsep}{6pt}` | 6pt (default) |
| `\arrayrulewidth` | Table line thickness | `\setlength{\arrayrulewidth}{0.5pt}` | 0.5pt (default) |
| `\doublerulesep` | Double line spacing | `\setlength{\doublerulesep}{2pt}` | 2pt (default) |
| `\itemsep` | Space between list items | `\setlength{\itemsep}{0.5em}` | 0pt (default) |
| `\parsep` | Space within list item | `\setlength{\parsep}{0.5em}` | 4pt plus 2pt minus 1pt |
| `\topsep` | Space before/after list | `\setlength{\topsep}{0.5em}` | 8pt plus 2pt minus 4pt |
| `\leftmargin` | List left indent | `\setlength{\leftmargin}{2em}` | Varies by level |
| `\listparindent` | Paragraph indent in list | `\setlength{\listparindent}{1em}` | 0pt (default) |

### Float and Box Spacing Commands

| Command | Purpose | Example | Notes |
|---------|---------|---------|-------|
| `\textfloatsep` | Space before/after floats | `\setlength{\textfloatsep}{10pt plus 2pt}` | For figures, tables |
| `\floatsep` | Space between floats | `\setlength{\floatsep}{10pt plus 2pt}` | When multiple floats |
| `\intextsep` | Space around inline floats | `\setlength{\intextsep}{12pt plus 2pt}` | For h placement |
| `\abovecaptionskip` | Space above caption | `\setlength{\abovecaptionskip}{10pt}` | Before figure/table caption |
| `\belowcaptionskip` | Space below caption | `\setlength{\belowcaptionskip}{10pt}` | After figure/table caption |
| `\fboxsep` | Space in framed boxes | `\setlength{\fboxsep}{3pt}` | Inside `\fbox` borders |
| `\fboxrule` | Frame box line width | `\setlength{\fboxrule}{0.4pt}` | Border thickness |

### Dimension Expressions

| Expression | Meaning | Example | Result |
|-----------|---------|---------|--------|
| `1.5\baselineskip` | Multiple of baseline | `\vspace{1.5\baselineskip}` | 1.5× current line spacing |
| `0.75\textwidth` | Percentage of text width | `\setlength{\parindent}{0.05\textwidth}` | 75% of text area width |
| `\baselineskip plus 5pt` | Flexible spacing | `\vspace{\baselineskip plus 5pt}` | Can stretch to 5pt more |
| `2em minus 1pt` | Shrinkable spacing | `\parskip{2em minus 1pt}` | Can shrink by 1pt |
| `\fill` | Fill available space | `\vspace{\fill}` | Expands to fill page |
| `2in plus 1in minus 0.5in` | Complex flexibility | For advanced layout control | Stretch/shrink both ways |

### Quick Examples

#### Setting Custom Spacing

```latex
% Custom margins with manual commands
\setlength{\topmargin}{0cm}
\setlength{\oddsidemargin}{1.5cm}
\setlength{\textwidth}{15cm}
\setlength{\textheight}{24cm}

% Custom paragraph spacing
\setlength{\parindent}{0.5em}      % 0.5em first-line indent
\setlength{\parskip}{0.5\baselineskip}  % Space between paragraphs

% Table spacing
\setlength{\tabcolsep}{8pt}        % More space in columns
\setlength{\arrayrulewidth}{1pt}   % Thicker table lines
```

#### Using Relative Units

```latex
% Font-relative spacing (scales with font size)
\vspace{2em}           % 2× current font size
\hspace{3ex}           % 3× current "x" height
\setlength{\parindent}{1.5em}

% Flexible spacing
\vspace{1cm plus 2mm minus 1mm}    % Can vary for layout
\vspace{\fill}                      % Fills remaining space
```

#### List Customization

```latex
% Tighter list spacing
\setlength{\itemsep}{0pt}          % No space between items
\setlength{\parsep}{0pt}           % No space within items
\setlength{\topsep}{0pt}           % No space before/after list

% Looser list spacing
\setlength{\itemsep}{1em}          % Large space between items
\setlength{\topsep}{1em}           % Large space before list
```

#### Table Customization

```latex
% Compact table
\setlength{\tabcolsep}{3pt}        % Narrow columns
\renewcommand{\arraystretch}{0.8}  % Reduce row height

% Spacious table
\setlength{\tabcolsep}{12pt}       % Wide columns
\renewcommand{\arraystretch}{1.5}  % Increase row height
```

### When to Use Each Command

| Situation | Command | Why |
|-----------|---------|-----|
| Add space between lines | `\vspace{1cm}` | Precise control |
| Add space in text | `\hspace{1em}` | Inline control |
| Small spacing gap | `\smallskip` | Easy quick spacing |
| Medium spacing gap | `\medskip` | Common use |
| Large spacing gap | `\bigskip` | Notable break |
| Flexible line spacing | Use `setspace` package | Better than `\baselineskip` |
| Page-level margins | Use `geometry` package | Easiest approach |
| Manual dimension control | `\setlength{\topmargin}{...}` | Last resort |
| Font-relative sizing | Use `em`, `ex` units | Scales with font |
| Absolute sizing | Use `pt`, `cm`, `in` units | Fixed size |
| Math mode spacing | `\:`, `\;`, `\,`, `\!` | Built-in spacing |
| Non-breaking space | `~` | Keeps items together |

### Common Spacing Values

| Purpose | Common Values |
|---------|---|
| Small indent | 0.5em, 5mm, 10pt |
| Standard indent | 1em, 10mm, 18pt |
| Large indent | 1.5em, 15mm, 27pt |
| Small gap | \smallskip or 5pt |
| Medium gap | \medskip or 10pt |
| Large gap | \bigskip or 20pt |
| Single spacing | 1.0 (multiplier) |
| 1.5 spacing | 1.5 (multiplier) |
| Double spacing | 2.0 (multiplier) |

## Best Practices

1. **Use geometry package**: More intuitive than manual settings
2. **Consistent margins**: Typically 1 inch or 2.5 cm all around
3. **Line spacing**: 1.5 or double spacing for drafts, single for final
4. **Paragraph indentation**: Use either indentation OR spacing, not both
5. **Readability**: 60-70 characters per line is optimal
6. **Headers/footers**: Ensure adequate space (headheight ≥ 12pt)

## Paper Size Reference

| Size | Dimensions | Use Case |
|------|------------|----------|
| letterpaper | 8.5" × 11" | US standard |
| a4paper | 210mm × 297mm | International standard |
| a5paper | 148mm × 210mm | Small books |
| b5paper | 176mm × 250mm | Books |
| legalpaper | 8.5" × 14" | Legal documents |

## Troubleshooting

- **Text too close to edge**: Increase margins
- **Too much white space**: Decrease margins
- **Headers cut off**: Increase `headheight`
- **Uneven spacing**: Check for manual spacing commands
- **Overfull boxes**: Text too wide - adjust margins or word spacing

## Next Steps

- Learn about [fonts](01-fonts.md)
- Explore [headers and footers](03-headers-footers.md)
- Study [page layout for books](../05-advanced/02-book-layout.md)
