# Simple Article Example

A basic academic article demonstrating common LaTeX features.

**Ready-to-compile file**: [`simple_article.tex`](simple_article.tex)

## LaTeX Source Code

Below is the complete source code (also available in `simple_article.tex`):

```latex
\documentclass[11pt,a4paper]{article}

% Packages
\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}
\usepackage[margin=1in]{geometry}
\usepackage{amsmath}
\usepackage{graphicx}
\usepackage{hyperref}

% Document information
\title{A Simple LaTeX Article}
\author{Your Name \\ Your Institution}
\date{\today}

\begin{document}

\maketitle

\begin{abstract}
This is a simple example of a LaTeX article demonstrating basic formatting, mathematics, figures, and references. It serves as a template for academic papers and reports.
\end{abstract}

\tableofcontents

\section{Introduction}

LaTeX is a powerful document preparation system widely used in academia. It excels at typesetting documents with complex mathematical formulas, scientific notation, and precise formatting requirements.

This document demonstrates:
\begin{itemize}
    \item Basic document structure
    \item Text formatting
    \item Mathematical equations
    \item Figures and tables
    \item Cross-references
\end{itemize}

\section{Mathematical Formulas}

\subsection{Inline Mathematics}

Einstein's famous equation is $E = mc^2$, where $E$ is energy, $m$ is mass, and $c$ is the speed of light.

\subsection{Display Equations}

The quadratic formula solves equations of the form $ax^2 + bx + c = 0$:

\begin{equation}
    x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
    \label{eq:quadratic}
\end{equation}

Euler's identity is often called the most beautiful equation in mathematics:

\begin{equation}
    e^{i\pi} + 1 = 0
    \label{eq:euler}
\end{equation}

\subsection{Multi-line Equations}

Using the \texttt{align} environment:

\begin{align}
    (x + y)^2 &= x^2 + 2xy + y^2 \label{eq:expand1} \\
    (x - y)^2 &= x^2 - 2xy + y^2 \label{eq:expand2}
\end{align}

\section{Lists and Formatting}

\subsection{Unordered Lists}

Benefits of using LaTeX:
\begin{itemize}
    \item Professional typesetting quality
    \item Excellent mathematical notation
    \item Automatic numbering and cross-referencing
    \item Version control friendly (plain text)
    \item Free and open source
\end{itemize}

\subsection{Ordered Lists}

Steps to create a LaTeX document:
\begin{enumerate}
    \item Write the content in a \texttt{.tex} file
    \item Compile using \texttt{pdflatex} or similar
    \item Review the PDF output
    \item Make corrections and recompile
\end{enumerate}

\subsection{Text Emphasis}

You can make text \textbf{bold}, \textit{italic}, \underline{underlined}, or \texttt{monospaced}. You can also \emph{emphasize} text, which adapts to context.

\section{Tables}

Table~\ref{tab:comparison} shows a comparison of compilation engines.

\begin{table}[htbp]
    \centering
    \caption{LaTeX Compilation Engines}
    \label{tab:comparison}
    \begin{tabular}{|l|c|c|c|}
        \hline
        \textbf{Engine} & \textbf{Speed} & \textbf{Fonts} & \textbf{Unicode} \\
        \hline
        pdfLaTeX & Fast & Limited & Basic \\
        XeLaTeX & Medium & System & Full \\
        LuaLaTeX & Medium & System & Full \\
        \hline
    \end{tabular}
\end{table}

\section{Figures}

% Note: This is a placeholder - you would need an actual image file
% For demonstration, we'll comment it out

% \begin{figure}[htbp]
%     \centering
%     \includegraphics[width=0.6\textwidth]{example-image}
%     \caption{An example figure showing LaTeX capabilities}
%     \label{fig:example}
% \end{figure}

% Figure~\ref{fig:example} demonstrates how to include images in your document.

To include an image, use:
\begin{verbatim}
\begin{figure}[htbp]
    \centering
    \includegraphics[width=0.6\textwidth]{filename}
    \caption{Your caption here}
    \label{fig:label}
\end{figure}
\end{verbatim}

\section{Cross-References}

LaTeX provides excellent cross-referencing capabilities. For example:
\begin{itemize}
    \item Equation~\ref{eq:quadratic} shows the quadratic formula
    \item Equation~\ref{eq:euler} is Euler's identity
    \item Table~\ref{tab:comparison} compares compilation engines
    \item This is Section~\ref{sec:conclusions}
\end{itemize}

\section{Conclusions}
\label{sec:conclusions}

This document has demonstrated basic LaTeX features including:
\begin{itemize}
    \item Document structure and organization
    \item Mathematical typesetting (Equations~\ref{eq:quadratic} and~\ref{eq:euler})
    \item Lists and text formatting
    \item Tables (Table~\ref{tab:comparison})
    \item Cross-referencing
\end{itemize}

LaTeX provides consistent, professional-quality typesetting that is ideal for academic and technical documents.

\section*{Acknowledgments}

This template can be used freely for your own documents. Modify it to suit your needs.

% Bibliography (optional)
\begin{thebibliography}{9}

\bibitem{lamport1994}
Leslie Lamport.
\textit{LaTeX: A Document Preparation System}.
Addison-Wesley, 2nd edition, 1994.

\bibitem{knuth1986}
Donald Knuth.
\textit{The TeXbook}.
Addison-Wesley, 1986.

\end{thebibliography}

\end{document}
```

## How to Use This Example

### 1. Use the Provided File

The file `simple_article.tex` is ready to compile in the same directory as this tutorial.

Alternatively, you can copy the code above and save it as your own file.

### 2. Compile

```bash
# Using pdflatex
pdflatex simple_article.tex

# Or using latexmk (recommended)
latexmk -pdf simple_article.tex
```

### 3. View the Result

Open the generated `simple_article.pdf` file.

## Customization Tips

### Change Fonts

Add to preamble:
```latex
\usepackage{times}  % Times font
% or
\usepackage{palatino}  % Palatino font
```

### Adjust Margins

Modify the geometry package:
```latex
\usepackage[top=1in, bottom=1in, left=1.25in, right=1.25in]{geometry}
```

### Line Spacing

```latex
\usepackage{setspace}
\doublespacing  % or \onehalfspacing
```

### Add Headers/Footers

```latex
\usepackage{fancyhdr}
\pagestyle{fancy}
\fancyhead[L]{Article Title}
\fancyhead[R]{\thepage}
```

## Next Steps

- Learn about [document structure](../01-basics/01-document-structure.md)
- Explore [mathematical typesetting](../05-advanced/01-mathematics.md)
- Study [bibliography management](../05-advanced/03-bibliography.md)
