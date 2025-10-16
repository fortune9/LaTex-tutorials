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
