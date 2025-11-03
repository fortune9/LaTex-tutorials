# LaTeX Document Structure

## Introduction

Every LaTeX document has a basic structure that defines how the content is organized and processed. Understanding this structure is fundamental to creating any LaTeX document.

## Basic Document Structure

A minimal LaTeX document consists of the following elements:

```latex
\documentclass{article}

\begin{document}
Hello, World!
\end{document}
```

## Document Components

### 1. Document Class

The first line of every LaTeX document specifies the document class:

```latex
\documentclass[options]{class}
```

Common document classes:
- `article` - For short documents, articles, and papers
- `report` - For longer documents with chapters
- `book` - For books with front matter and back matter
- `beamer` - For presentations
- `letter` - For letters

Example with options:
```latex
\documentclass[12pt, a4paper, twocolumn]{article}
```

## Document Class Options

Document class options are specified in square brackets and control various aspects of your document's appearance and behavior. Multiple options are separated by commas.

### Font Size Options

The font size option sets the default font size for the entire document.

| Option | Size | Description | Availability |
|--------|------|-------------|--------------|
| `10pt` | 10 points | Default for most classes | All classes |
| `11pt` | 11 points | Slightly larger | All classes |
| `12pt` | 12 points | Larger, good for readability | All classes |
| `9pt` | 9 points | Smaller (extarticle/extbook only) | extarticle, extbook |
| `14pt` | 14 points | Large (extarticle/extbook only) | extarticle, extbook |
| `17pt` | 17 points | Very large (extarticle/extbook only) | extarticle, extbook |
| `20pt` | 20 points | Extra large (extarticle/extbook only) | extarticle, extbook |

**Example:**
```latex
\documentclass[11pt]{article}  % 11-point font
\documentclass[12pt]{report}   % 12-point font
```

**Note:** The font size affects not just body text but also headings, which are scaled proportionally.

### Paper Size Options

The paper size option determines the physical dimensions of your document.

| Option | Dimensions | Description |
|--------|------------|-------------|
| `letterpaper` | 8.5" × 11" | US standard (default) |
| `a4paper` | 210mm × 297mm | International standard |
| `a5paper` | 148mm × 210mm | Half of A4, good for small books |
| `b5paper` | 176mm × 250mm | Between A5 and A4 |
| `legalpaper` | 8.5" × 14" | US legal documents |
| `executivepaper` | 7.25" × 10.5" | US executive size |

**Example:**
```latex
\documentclass[a4paper]{article}        % A4 paper
\documentclass[letterpaper]{report}     % US Letter
\documentclass[a5paper]{book}           % A5 for small book
```

### Page Layout Options

Control how content is arranged on the page.

| Option | Effect | Best For |
|--------|--------|----------|
| `oneside` | Single-sided printing (default for article/report) | Articles, reports |
| `twoside` | Double-sided printing (default for book) | Books, theses |
| `onecolumn` | Single column layout (default) | Most documents |
| `twocolumn` | Two-column layout | Journals, newsletters |
| `landscape` | Landscape orientation | Wide tables, presentations |

**Example:**
```latex
\documentclass[twoside]{article}        % For double-sided printing
\documentclass[twocolumn]{article}      % Two-column layout
\documentclass[landscape, a4paper]{article}  % Landscape A4
```

### Title Page Options

Control whether a separate title page is created.

| Option | Effect | Default For |
|--------|--------|-------------|
| `titlepage` | Creates separate title page | book, report |
| `notitlepage` | Title on first page of content | article |

**Example:**
```latex
\documentclass[titlepage]{article}      % Separate title page
\documentclass[notitlepage]{report}     % No separate title page
```

### Equation Numbering Options

Control how equations are numbered in the document.

| Option | Effect | Default For |
|--------|--------|-------------|
| `leqno` | Equation numbers on the left | - |
| `reqno` | Equation numbers on the right (default) | All classes |
| `fleqn` | Flush left equations (not centered) | - |

**Example:**
```latex
\documentclass[leqno]{article}          % Equation numbers on left
\documentclass[fleqn, leqno]{article}   % Left-aligned, left numbers
```

### Chapter Opening Options (book class)

For the `book` class, control where chapters begin.

| Option | Effect |
|--------|--------|
| `openright` | Chapters start on right-hand (odd) pages (default) |
| `openany` | Chapters can start on any page |

**Example:**
```latex
\documentclass[openany]{book}           % Chapters on any page
\documentclass[openright]{book}         % Chapters on odd pages only
```

### Draft Mode Options

Draft mode helps during document preparation.

| Option | Effect |
|--------|--------|
| `draft` | Shows overfull boxes, doesn't include images (placeholders only) |
| `final` | Full rendering (default) |

**Example:**
```latex
\documentclass[draft]{article}          % Draft mode for faster compilation
\documentclass[final, 12pt]{report}     % Final version
```

### Reference Options (article class)

| Option | Effect |
|--------|--------|
| `openbib` | Open bibliography format with line breaks |

**Example:**
```latex
\documentclass[openbib]{article}
```

## Class-Specific Options Summary

### article Class Options

The `article` class is designed for short documents without chapters.

**Commonly Used Options:**
```latex
\documentclass[
    11pt,           % Font size
    a4paper,        % Paper size
    twocolumn,      % Two-column layout
    twoside,        % Double-sided printing
    titlepage,      % Separate title page
    leqno,          % Left equation numbers
    fleqn,          % Left-aligned equations
    draft           % Draft mode
]{article}
```

**Default Values:**
- Font size: `10pt`
- Paper size: `letterpaper`
- Layout: `onecolumn`, `oneside`
- Title: `notitlepage`
- Equations: `reqno` (right), centered

### report Class Options

The `report` class is for longer documents with chapters but no \part divisions.

**Commonly Used Options:**
```latex
\documentclass[
    12pt,           % Font size
    a4paper,        % Paper size
    oneside,        % Single-sided (or twoside)
    openany,        % Chapters on any page (or openright)
    titlepage,      % Separate title page (default)
    draft           % Draft mode
]{report}
```

**Default Values:**
- Font size: `10pt`
- Paper size: `letterpaper`
- Layout: `onecolumn`, `oneside`
- Title: `titlepage`
- Chapters: `openright`

**Key Difference from article:** Has `\chapter` command and separate title page by default.

### book Class Options

The `book` class is designed for books with front matter, main matter, and back matter.

**Commonly Used Options:**
```latex
\documentclass[
    11pt,           % Font size
    a5paper,        % Paper size (common for books)
    twoside,        % Double-sided (default)
    openright,      % Chapters on odd pages (default)
    titlepage,      % Separate title page (default)
    final           % Final mode
]{book}
```

**Default Values:**
- Font size: `10pt`
- Paper size: `letterpaper`
- Layout: `onecolumn`, `twoside`
- Title: `titlepage`
- Chapters: `openright`

**Key Features:**
- Always double-sided by default
- Chapters open on right (odd) pages by default
- Supports `\frontmatter`, `\mainmatter`, `\backmatter`

### beamer Class Options

The `beamer` class is for presentations and has its own unique options.

**Commonly Used Options:**
```latex
\documentclass[
    11pt,               % Font size
    aspectratio=169,    % 16:9 aspect ratio
    handout,            % Handout mode (no overlays)
    trans,              % Transparency effects
    compress,           % Compress navigation bar
    t                   % Top-align content
]{beamer}
```

**Beamer-Specific Options:**

| Option | Effect |
|--------|--------|
| `aspectratio=169` | 16:9 widescreen (also: 1610, 149, 54, 43, 32) |
| `handout` | Create handout without overlays |
| `trans` | Enable transparency effects |
| `t` | Top-align slide content |
| `c` | Center slide content (default) |
| `compress` | Compress navigation elements |

### letter Class Options

The `letter` class is for correspondence.

**Commonly Used Options:**
```latex
\documentclass[
    11pt,           % Font size
    letterpaper     % Paper size
]{letter}
```

**Note:** The `letter` class has fewer options than other classes as it's designed for a specific purpose.

## Complete Options Reference Table

This table summarizes all standard document class options across different classes.

| Option | article | report | book | beamer | letter | Description |
|--------|---------|--------|------|--------|--------|-------------|
| **Font Sizes** |
| `10pt` | ✓ (default) | ✓ (default) | ✓ (default) | ✓ | ✓ (default) | 10-point font |
| `11pt` | ✓ | ✓ | ✓ | ✓ | ✓ | 11-point font |
| `12pt` | ✓ | ✓ | ✓ | ✓ | ✓ | 12-point font |
| **Paper Sizes** |
| `letterpaper` | ✓ (default) | ✓ (default) | ✓ (default) | - | ✓ (default) | 8.5" × 11" |
| `a4paper` | ✓ | ✓ | ✓ | - | ✓ | 210mm × 297mm |
| `a5paper` | ✓ | ✓ | ✓ | - | ✓ | 148mm × 210mm |
| `b5paper` | ✓ | ✓ | ✓ | - | ✓ | 176mm × 250mm |
| `legalpaper` | ✓ | ✓ | ✓ | - | ✓ | 8.5" × 14" |
| `executivepaper` | ✓ | ✓ | ✓ | - | ✓ | 7.25" × 10.5" |
| **Page Layout** |
| `oneside` | ✓ (default) | ✓ (default) | ✓ | - | ✓ (default) | Single-sided layout |
| `twoside` | ✓ | ✓ | ✓ (default) | - | ✓ | Double-sided layout |
| `onecolumn` | ✓ (default) | ✓ (default) | ✓ (default) | - | ✓ (default) | Single column |
| `twocolumn` | ✓ | ✓ | ✓ | - | ✓ | Two columns |
| `landscape` | ✓ | ✓ | ✓ | ✓ | ✓ | Landscape orientation |
| **Title Page** |
| `titlepage` | ✓ | ✓ (default) | ✓ (default) | - | - | Separate title page |
| `notitlepage` | ✓ (default) | ✓ | ✓ | - | - | No separate title page |
| **Chapter Opening** |
| `openright` | - | ✓ (default) | ✓ (default) | - | - | Chapters on odd pages |
| `openany` | - | ✓ | ✓ | - | - | Chapters on any page |
| **Equations** |
| `leqno` | ✓ | ✓ | ✓ | ✓ | - | Equation numbers left |
| `reqno` | ✓ (default) | ✓ (default) | ✓ (default) | ✓ (default) | - | Equation numbers right |
| `fleqn` | ✓ | ✓ | ✓ | ✓ | - | Left-aligned equations |
| **Mode** |
| `draft` | ✓ | ✓ | ✓ | ✓ | ✓ | Draft mode |
| `final` | ✓ (default) | ✓ (default) | ✓ (default) | ✓ (default) | ✓ (default) | Final mode |
| **Bibliography** |
| `openbib` | ✓ | ✓ | ✓ | - | - | Open bibliography format |
| **Beamer-Specific** |
| `aspectratio=X` | - | - | - | ✓ | - | Aspect ratio (169, 1610, etc.) |
| `handout` | - | - | - | ✓ | - | Handout mode |
| `trans` | - | - | - | ✓ | - | Transparency effects |
| `t` | - | - | - | ✓ | - | Top-align frames |
| `c` | - | - | - | ✓ (default) | - | Center frames |

## Practical Examples

### Academic Paper (US Format)
```latex
\documentclass[12pt, letterpaper, oneside]{article}
```

### Academic Paper (European Format)
```latex
\documentclass[12pt, a4paper, oneside]{article}
```

### Two-Column Journal Article
```latex
\documentclass[10pt, a4paper, twocolumn, twoside]{article}
```

### Master's Thesis
```latex
\documentclass[12pt, a4paper, oneside, openany]{report}
```

### PhD Thesis
```latex
\documentclass[11pt, a4paper, twoside, openright]{report}
```

### Printed Book
```latex
\documentclass[11pt, a5paper, twoside, openright]{book}
```

### E-Book
```latex
\documentclass[11pt, a4paper, oneside, openany]{book}
```

### Conference Presentation (16:9)
```latex
\documentclass[11pt, aspectratio=169]{beamer}
```

### Formal Letter
```latex
\documentclass[11pt, letterpaper]{letter}
```

### Draft Document (Fast Compilation)
```latex
\documentclass[12pt, a4paper, draft]{article}
```

## How Options Work Together

### Font Size and Readability

Font size affects readability and the amount of content per page:

```latex
% More content, smaller text
\documentclass[10pt]{article}

% Balanced
\documentclass[11pt]{article}

% Best readability, less content per page
\documentclass[12pt]{article}
```

**Rule of thumb:** Use 12pt for documents to be read on screen or by older readers, 11pt for general use, 10pt for journals or when space is limited.

### Paper Size and Margins

Different paper sizes work best with different margins:

```latex
% US Letter with 1-inch margins
\documentclass[letterpaper]{article}
\usepackage[margin=1in]{geometry}

% A4 with 2.5cm margins
\documentclass[a4paper]{article}
\usepackage[margin=2.5cm]{geometry}

% A5 book with custom margins
\documentclass[a5paper, twoside]{book}
\usepackage[inner=2cm, outer=1.5cm, top=2cm, bottom=2cm]{geometry}
```

### Two-Sided vs One-Sided

Two-sided affects margins and page numbering:

```latex
% Single-sided: symmetric margins
\documentclass[oneside]{article}

% Double-sided: alternating margins for binding
\documentclass[twoside]{book}
\usepackage[inner=3cm, outer=2cm]{geometry}  % More space on binding side
```

### Combining Options

Options can be combined freely:

```latex
% Complete setup for a professional article
\documentclass[
    11pt,           % Readable font size
    a4paper,        % International standard
    twoside,        % For printing
    twocolumn,      % Journal style
    final           % Full rendering
]{article}

% Complete setup for a book
\documentclass[
    11pt,           % Comfortable reading
    a5paper,        % Standard book size
    twoside,        % Double-sided printing
    openright       % Chapters on odd pages
]{book}
```

## Tips for Choosing Options

1. **Start with defaults**: Only add options you need
2. **Consider your audience**: Screen readers may prefer 12pt, print can use 10-11pt
3. **Match your publisher**: Journals often specify exact requirements
4. **Test print**: Always test a printed page before printing the full document
5. **Paper size matters**: Use `a4paper` outside the US, `letterpaper` in the US
6. **Two-sided for books**: Use `twoside` for anything to be bound
7. **Draft mode saves time**: Use `draft` during writing for faster compilation
8. **Combine with geometry**: Use `geometry` package for fine-tuned control

## Common Mistakes to Avoid

1. **Mixing paper sizes**: Don't use US margins with A4 paper
   ```latex
   % Wrong: default letterpaper with A4 geometry
   \documentclass{article}
   \usepackage[a4paper]{geometry}
   
   % Right: specify A4 in document class
   \documentclass[a4paper]{article}
   \usepackage{geometry}
   ```

2. **Wrong font size syntax**: Font size must include `pt`
   ```latex
   % Wrong
   \documentclass[12]{article}
   
   % Right
   \documentclass[12pt]{article}
   ```

3. **Conflicting options**: Some options don't work together
   ```latex
   % Wrong: oneside and openright conflict
   \documentclass[oneside, openright]{book}
   
   % Right: use twoside with openright
   \documentclass[twoside, openright]{book}
   ```

4. **Too many options**: Only specify what you need
   ```latex
   % Overcomplicated
   \documentclass[10pt, letterpaper, oneside, onecolumn, notitlepage, reqno, final]{article}
   
   % Better: these are defaults anyway
   \documentclass{article}
   ```

### 2. Preamble

The preamble is everything between `\documentclass` and `\begin{document}`. Here you:
- Load packages
- Define custom commands
- Set document properties

```latex
\documentclass{article}

% Load packages
\usepackage{graphicx}
\usepackage{amsmath}

% Set document information
\title{My First LaTeX Document}
\author{Your Name}
\date{\today}

\begin{document}
```

### 3. Document Body

Everything between `\begin{document}` and `\end{document}` is the actual content:

```latex
\begin{document}

\maketitle

\section{Introduction}
This is the introduction.

\section{Main Content}
This is the main content.

\end{document}
```

## Common Preamble Packages

```latex
\usepackage[utf8]{inputenc}     % Input encoding
\usepackage[T1]{fontenc}        % Font encoding
\usepackage{graphicx}           % Include images
\usepackage{amsmath}            % Math symbols
\usepackage{hyperref}           % Hyperlinks
\usepackage{geometry}           % Page layout
\usepackage{babel}              % Language support
```

## Example: Complete Document

```latex
\documentclass[11pt, a4paper]{article}

% Packages
\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}
\usepackage{geometry}
\geometry{margin=1in}

% Document info
\title{Understanding LaTeX Structure}
\author{LaTeX Learner}
\date{\today}

\begin{document}

\maketitle

\tableofcontents

\section{Introduction}
LaTeX is a powerful typesetting system.

\section{Why Use LaTeX?}
LaTeX provides:
\begin{itemize}
    \item Professional typesetting
    \item Excellent math support
    \item Automatic numbering and references
    \item Consistent formatting
\end{itemize}

\section{Conclusion}
Understanding the basic structure is the first step to mastering LaTeX.

\end{document}
```

## Key Takeaways

1. Every document must have `\documentclass` as the first line
2. The preamble configures the document
3. Content goes between `\begin{document}` and `\end{document}`
4. Packages extend LaTeX functionality
5. Commands start with backslash `\`
6. Environments are enclosed with `\begin{}` and `\end{}`

## Next Steps

- Learn about [formatting text](../02-formatting/01-fonts.md)
- Explore [page layout and margins](../02-formatting/02-margins-spacing.md)
- Set up [your LaTeX environment](../03-setup/README.md)
