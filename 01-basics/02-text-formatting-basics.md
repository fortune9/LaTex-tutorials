# Basic Text Formatting in LaTeX

## Introduction

LaTeX provides various commands for formatting text. This tutorial covers the fundamental text formatting techniques.

## Text Emphasis

### Bold, Italic, and Underline

```latex
\textbf{Bold text}
\textit{Italic text}
\underline{Underlined text}
\emph{Emphasized text}
```

### Combining Formats

```latex
\textbf{\textit{Bold and italic}}
\underline{\textbf{Bold and underlined}}
```

## Font Sizes

LaTeX provides several predefined font size commands (from smallest to largest):

```latex
{\tiny Tiny text}
{\scriptsize Script size}
{\footnotesize Footnote size}
{\small Small text}
{\normalsize Normal size}
{\large Large text}
{\Large Larger text}
{\LARGE Even larger}
{\huge Huge text}
{\Huge Largest text}
```

## Text Alignment

### Left, Center, and Right

```latex
\begin{flushleft}
Left-aligned text
\end{flushleft}

\begin{center}
Centered text
\end{center}

\begin{flushright}
Right-aligned text
\end{flushright}
```

## Lists

### Unordered Lists

```latex
\begin{itemize}
    \item First item
    \item Second item
    \item Third item
        \begin{itemize}
            \item Nested item
            \item Another nested item
        \end{itemize}
\end{itemize}
```

### Ordered Lists

```latex
\begin{enumerate}
    \item First step
    \item Second step
    \item Third step
\end{enumerate}
```

### Description Lists

```latex
\begin{description}
    \item[LaTeX] A document preparation system
    \item[TeX] The underlying typesetting system
    \item[Package] Extension to LaTeX functionality
\end{description}
```

## Paragraphs and Line Breaks

```latex
% New paragraph (leave a blank line)
First paragraph.

Second paragraph.

% Force line break
First line \\
Second line

% Prevent line break
First~word second~word
```

## Special Characters

Some characters have special meaning in LaTeX and need to be escaped:

```latex
\# \$ \% \& \_ \{ \}
\textbackslash  % for backslash
\textasciitilde % for tilde
\textasciicircum % for caret
```

## Quotation Marks

```latex
`single quotes'
``double quotes''
```

## Spacing

### Horizontal Spacing

```latex
Word\,word      % thin space
Word\ word      % normal space
Word\quad word  % quad space
Word\qquad word % double quad space
Word\hspace{2cm}word  % custom space
```

### Vertical Spacing

```latex
\vspace{1cm}    % vertical space
\bigskip        % big vertical skip
\medskip        % medium skip
\smallskip      % small skip
```

## Example Document

```latex
\documentclass{article}

\begin{document}

\section{Text Formatting Examples}

This is \textbf{bold text}, \textit{italic text}, and \underline{underlined text}.

\subsection{Font Sizes}

{\small Small text} compared to {\large large text}.

\subsection{Lists}

Benefits of LaTeX:
\begin{itemize}
    \item Professional appearance
    \item Excellent for mathematical typesetting
    \item Free and open source
\end{itemize}

Steps to create a document:
\begin{enumerate}
    \item Write the LaTeX code
    \item Compile to PDF
    \item Review the output
\end{enumerate}

\subsection{Special Formatting}

Use \texttt{texttt} for \texttt{monospace/code text}.

\begin{center}
This text is centered.
\end{center}

\end{document}
```

## Best Practices

1. Use `\emph{}` for emphasis rather than `\textit{}` - it adapts to context
2. Don't manually adjust spacing unless necessary
3. Use semantic markup (e.g., `\section{}`) rather than manual formatting
4. Let LaTeX handle paragraph spacing automatically
5. Use `~` (non-breaking space) to keep words together (e.g., `Figure~1`)

## Next Steps

- Learn about [fonts and font families](../02-formatting/01-fonts.md)
- Explore [page margins and spacing](../02-formatting/02-margins-spacing.md)
- Study [document structure](01-document-structure.md)
