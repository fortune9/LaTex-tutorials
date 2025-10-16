# Headers and Footers in LaTeX

## Introduction

Headers and footers provide navigation information and document metadata. LaTeX offers several packages for customizing them.

## The fancyhdr Package

The most popular package for custom headers and footers:

```latex
\usepackage{fancyhdr}
\pagestyle{fancy}
```

## Basic Header/Footer Setup

```latex
\usepackage{fancyhdr}
\pagestyle{fancy}

% Clear default headers/footers
\fancyhf{}

% Set header
\fancyhead[L]{Left Header}
\fancyhead[C]{Center Header}
\fancyhead[R]{Right Header}

% Set footer
\fancyfoot[L]{Left Footer}
\fancyfoot[C]{\thepage}
\fancyfoot[R]{Right Footer}
```

## Position Codes

- `L` - Left
- `C` - Center
- `R` - Right
- `E` - Even pages
- `O` - Odd pages

```latex
% Different headers for odd/even pages
\fancyhead[LE,RO]{\thepage}  % Page number
\fancyhead[RE,LO]{Document Title}
```

## Header/Footer Lines

```latex
% Header rule thickness
\renewcommand{\headrulewidth}{0.4pt}

% Footer rule
\renewcommand{\footrulewidth}{0.4pt}

% Remove rules
\renewcommand{\headrulewidth}{0pt}
\renewcommand{\footrulewidth}{0pt}
```

## Common Patterns

### Simple: Page Number in Footer

```latex
\usepackage{fancyhdr}
\pagestyle{fancy}
\fancyhf{}
\fancyfoot[C]{\thepage}
\renewcommand{\headrulewidth}{0pt}
```

### Academic Paper Style

```latex
\usepackage{fancyhdr}
\pagestyle{fancy}
\fancyhf{}
\fancyhead[L]{\leftmark}  % Section name
\fancyhead[R]{\thepage}
\renewcommand{\headrulewidth}{0.4pt}
```

### Book Style

```latex
\usepackage{fancyhdr}
\pagestyle{fancy}
\fancyhf{}

% Odd pages (right side)
\fancyhead[RO]{\thepage}
\fancyhead[LO]{\rightmark}  % Section

% Even pages (left side)
\fancyhead[LE]{\thepage}
\fancyhead[RE]{\leftmark}   % Chapter

\renewcommand{\headrulewidth}{0.4pt}
```

## Special Page Styles

### First Page of Chapters

```latex
% Redefine plain style (used for chapter first pages)
\fancypagestyle{plain}{
    \fancyhf{}
    \fancyfoot[C]{\thepage}
    \renewcommand{\headrulewidth}{0pt}
}
```

### Custom Page Style

```latex
\fancypagestyle{mystyle}{
    \fancyhf{}
    \fancyhead[L]{Custom Header}
    \fancyfoot[C]{\thepage}
}

% Apply to specific pages
\thispagestyle{mystyle}
```

## Useful Variables

```latex
\thepage          % Current page number
\leftmark         % Current chapter
\rightmark        % Current section
\today            % Current date
\theauthor        % Document author
\thetitle         % Document title
```

## Width and Height Adjustments

```latex
\usepackage{geometry}
\geometry{
    headheight=15pt,     % Height of header
    headsep=12pt,        % Space between header and text
    footskip=30pt,       % Space for footer
    marginparwidth=2cm   % Width of margin notes
}
```

## Complete Example

```latex
\documentclass{article}

\usepackage{fancyhdr}
\usepackage{geometry}
\geometry{
    margin=1in,
    headheight=15pt
}

% Document info
\title{My Document}
\author{John Doe}
\date{\today}

% Configure fancy headers
\pagestyle{fancy}
\fancyhf{}
\fancyhead[L]{\nouppercase{\leftmark}}
\fancyhead[R]{\thepage}
\fancyfoot[C]{John Doe - My Document}

\renewcommand{\headrulewidth}{0.4pt}
\renewcommand{\footrulewidth}{0.4pt}

% Custom style for title page
\fancypagestyle{firststyle}{
    \fancyhf{}
    \fancyfoot[C]{\thepage}
    \renewcommand{\headrulewidth}{0pt}
}

\begin{document}

\thispagestyle{firststyle}
\maketitle

\section{Introduction}
This document has custom headers and footers.

\newpage
\section{Main Content}
Notice the headers change with sections.

\end{document}
```

## lastpage Package

For "Page X of Y" format:

```latex
\usepackage{lastpage}
\usepackage{fancyhdr}

\pagestyle{fancy}
\fancyhf{}
\fancyfoot[C]{Page \thepage\ of \pageref{LastPage}}
```

## Remove Headers on Empty Pages

```latex
\usepackage{emptypage}
% Automatically removes headers/footers from empty pages
```

## Multiline Headers

```latex
\fancyhead[L]{%
    Line 1\\
    Line 2
}
```

## Conditional Content

```latex
\usepackage{ifthen}

\fancyhead[L]{%
    \ifthenelse{\value{page}=1}%
        {First Page Header}%
        {Other Pages Header}%
}
```

## Best Practices

1. **Consistency**: Use the same style throughout the document
2. **Readability**: Don't overcrowd headers/footers
3. **Page numbers**: Always include them somewhere
4. **Height**: Set adequate `headheight` to avoid warnings
5. **Chapters**: Use different styles for chapter first pages
6. **Two-sided**: Use different odd/even page layouts for books

## Common Issues and Solutions

### "Package Fancyhdr Warning: \\headheight is too small"

```latex
% Increase headheight in geometry
\geometry{headheight=15pt}
```

### Headers showing uppercase section names

```latex
% Use nouppercase
\fancyhead[L]{\nouppercase{\leftmark}}
```

### First page has unwanted header

```latex
% Change first page style
\thispagestyle{plain}
% or
\thispagestyle{empty}
```

## Page Style Reference

| Style | Description |
|-------|-------------|
| `plain` | Page number in footer only |
| `empty` | No headers or footers |
| `headings` | Chapter/section in header |
| `fancy` | Custom (from fancyhdr) |

## Advanced: Graphical Headers

```latex
\usepackage{graphicx}
\usepackage{fancyhdr}

\fancyhead[L]{\includegraphics[height=1cm]{logo.png}}
\fancyhead[R]{Company Name}
```

## Next Steps

- Explore [page layout](02-margins-spacing.md)
- Learn about [document structure](../01-basics/01-document-structure.md)
- Study [book-specific formatting](../05-advanced/02-book-layout.md)
