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
