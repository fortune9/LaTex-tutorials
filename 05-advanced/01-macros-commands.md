# Custom Commands, Macros, and Declarations

## Introduction

LaTeX allows you to define custom commands (also called macros) to automate repetitive tasks, simplify complex expressions, and create consistent formatting throughout your document. This tutorial covers creating and using custom commands effectively.

## Table of Contents

- [Why Use Custom Commands?](#why-use-custom-commands)
- [Basic Command Definition](#basic-command-definition)
- [Commands with Arguments](#commands-with-arguments)
- [Optional Arguments](#optional-arguments)
- [Renewing and Providing Commands](#renewing-and-providing-commands)
- [Declarations vs Commands](#declarations-vs-commands)
- [Advanced Techniques](#advanced-techniques)
- [Best Practices](#best-practices)
- [Common Use Cases](#common-use-cases)

---

## Why Use Custom Commands?

Custom commands offer several benefits:

1. **Consistency**: Ensure uniform formatting across your document
2. **Maintainability**: Change formatting in one place affects all instances
3. **Simplification**: Complex expressions become simple commands
4. **Readability**: Code becomes more semantic and easier to understand
5. **Efficiency**: Reduce typing and potential errors

### Example: Before and After

**Without custom commands**:
```latex
\textbf{\textcolor{blue}{Important}}: This is crucial.
\textbf{\textcolor{blue}{Important}}: Another critical point.
```

**With custom commands**:
```latex
\newcommand{\important}[1]{\textbf{\textcolor{blue}{#1}}}

\important{Important}: This is crucial.
\important{Important}: Another critical point.
```

---

## Basic Command Definition

### The `\newcommand` Syntax

```latex
\newcommand{\commandname}{definition}
```

### Simple Examples

```latex
% Define a command for your university name
\newcommand{\myuni}{Massachusetts Institute of Technology}

% Use it in the document
I study at \myuni.
```

```latex
% Define a command for mathematical notation
\newcommand{\R}{\mathbb{R}}  % Real numbers
\newcommand{\N}{\mathbb{N}}  % Natural numbers
\newcommand{\Z}{\mathbb{Z}}  % Integers

% Usage
Let $f: \R \to \R$ be a function...
The set $\N$ contains all natural numbers...
```

### Text Formatting Shortcuts

```latex
\newcommand{\emph}[1]{\textit{\textbf{#1}}}
\newcommand{\keyword}[1]{\texttt{\textcolor{purple}{#1}}}
\newcommand{\code}[1]{\texttt{#1}}

% Usage
This is an \emph{important} concept.
The \keyword{LaTeX} system is powerful.
Use the \code{print()} function.
```

---

## Commands with Arguments

### Single Argument

```latex
\newcommand{\commandname}[number_of_args]{definition using #1, #2, etc.}
```

### Examples

```latex
% Bold and colored text
\newcommand{\highlight}[1]{\textbf{\textcolor{red}{#1}}}

% Usage
This is \highlight{very important}.
```

```latex
% Mathematical vector notation
\newcommand{\vect}[1]{\mathbf{#1}}
\newcommand{\norm}[1]{\left\| #1 \right\|}

% Usage
The vector $\vect{v}$ has norm $\norm{\vect{v}}$.
```

### Multiple Arguments

```latex
% Command with two arguments
\newcommand{\frac}[2]{\frac{#1}{#2}}

% Matrix notation
\newcommand{\mat}[2]{\ensuremath{\begin{bmatrix} #1 \\ #2 \end{bmatrix}}}

% Usage
\mat{1}{2}  % Creates a 2x1 matrix
```

```latex
% Colored box with custom text
\newcommand{\colorbox}[2]{\fcolorbox{#1}{#1!20}{\textcolor{#1}{\textbf{#2}}}}

% Usage
\colorbox{blue}{Information}
\colorbox{red}{Warning}
\colorbox{green}{Success}
```

### More Complex Example

```latex
% Define a theorem-like environment shortcut
\newcommand{\theorem}[2]{
    \begin{tcolorbox}[colback=blue!5, colframe=blue!75!black, title=Theorem: #1]
        #2
    \end{tcolorbox}
}

% Usage
\theorem{Pythagorean Theorem}{
    In a right triangle, $a^2 + b^2 = c^2$.
}
```

---

## Optional Arguments

### Syntax with Default Values

```latex
\newcommand{\commandname}[num_args][default_value]{definition}
```

The first argument becomes optional with the specified default value.

### Examples

```latex
% Section with optional subtitle
\newcommand{\mysection}[2][]{
    \section{#2}
    \ifx&#1&% Check if argument is empty
    \else
        \textit{#1}
    \fi
}

% Usage
\mysection{Introduction}  % No subtitle
\mysection[Overview of the topic]{Introduction}  % With subtitle
```

```latex
% Mathematical derivative with optional order
\newcommand{\diff}[2][1]{
    \ifnum#1=1
        \frac{d#2}{dx}
    \else
        \frac{d^{#1}#2}{dx^{#1}}
    \fi
}

% Usage
\diff{f}        % First derivative: df/dx
\diff[2]{f}     % Second derivative: d²f/dx²
\diff[3]{f}     % Third derivative: d³f/dx³
```

```latex
% Colored text with optional color
\newcommand{\colortext}[2][red]{\textcolor{#1}{#2}}

% Usage
\colortext{This is red}              % Default red
\colortext[blue]{This is blue}       % Custom blue
\colortext[green]{This is green}     % Custom green
```

---

## Renewing and Providing Commands

### `\renewcommand` - Redefine Existing Commands

```latex
% Redefine an existing command
\renewcommand{\abstractname}{Summary}
\renewcommand{\contentsname}{Table of Contents}

% Redefine emphasis to use bold instead of italic
\renewcommand{\emph}[1]{\textbf{#1}}
```

**Warning**: Only use `\renewcommand` for commands that already exist. If you're not sure, use `\providecommand`.

### `\providecommand` - Define Only If Not Exists

```latex
% Define command only if it doesn't already exist
\providecommand{\R}{\mathbb{R}}

% Safe to use even if another package defines \R
```

### `\def` vs `\newcommand`

```latex
% \def - TeX primitive (use with caution)
\def\mycommand{definition}

% \newcommand - LaTeX way (preferred, safer)
\newcommand{\mycommand}{definition}
```

**Recommendation**: Always use `\newcommand` in LaTeX unless you have specific reasons to use `\def`. `\newcommand` checks if the command already exists and prevents accidental redefinition.

---

## Declarations vs Commands

### Commands (Local Effect)

Commands affect only their arguments:

```latex
\newcommand{\bold}[1]{\textbf{#1}}

Normal text \bold{bold text} normal again.
```

### Declarations (Global or Scoped Effect)

Declarations affect everything that follows until the scope ends:

```latex
% Declaration
\newcommand{\makebold}{\bfseries}

Normal text {\makebold bold text still bold} normal again.
```

### Font Declarations

```latex
% Common declarations
\bfseries   % Bold
\itshape    % Italic
\ttfamily   % Typewriter (monospace)
\sffamily   % Sans serif
\rmfamily   % Roman (default)
\normalfont % Reset to normal
```

### Creating Custom Declarations

```latex
% Custom font size declaration
\newcommand{\largetext}{\fontsize{14}{16}\selectfont}

% Usage
{\largetext This text is larger.} Back to normal.
```

### Switching Between Command and Declaration Style

```latex
% Command style (with argument)
\newcommand{\textred}[1]{\textcolor{red}{#1}}

% Declaration style (affects following text)
\newcommand{\red}{\color{red}}

% Usage comparison
\textred{This is red} and this is not.
{\red This is red and so is this} but not this.
```

---

## Custom Environments with `\newenvironment`

### What Are Environments?

Environments in LaTeX are structures that have a **beginning** and an **end**, like `\begin{...}` and `\end{...}`. They define a scope where specific formatting or behavior applies.

### Key Differences: Commands vs Environments

| Feature | Commands (`\newcommand`) | Environments (`\newenvironment`) |
|---------|-------------------------|----------------------------------|
| **Syntax** | `\mycommand{text}` | `\begin{myenv} ... \end{myenv}` |
| **Scope** | Applies to argument(s) | Applies to content between begin/end |
| **Use Case** | Short inline formatting | Block-level formatting, longer content |
| **Structure** | Single definition | Two parts: begin code and end code |
| **Nesting** | Can be nested in arguments | Can contain paragraphs, lists, etc. |

### Basic `\newenvironment` Syntax

```latex
\newenvironment{envname}
    {begin code}      % Code executed at \begin{envname}
    {end code}        % Code executed at \end{envname}
```

### Simple Examples

```latex
% Custom quote environment with styling
\newenvironment{myquote}
    {\begin{quote}\itshape\color{blue}}
    {\end{quote}}

% Usage
\begin{myquote}
    This is a custom styled quotation.
    It can span multiple lines.
\end{myquote}
```

```latex
% Warning box environment
\newenvironment{warning}
    {\begin{center}\begin{tabular}{|p{0.9\textwidth}|}
    \hline
    \textbf{Warning:} }
    {\\ \hline
    \end{tabular}\end{center}}

% Usage
\begin{warning}
    This operation is irreversible!
\end{warning}
```

### Environments with Arguments

```latex
\newenvironment{envname}[num_args]
    {begin code using #1, #2, etc.}
    {end code}
```

**Important**: Arguments are only available in the **begin code**, not in the end code.

### Examples with Arguments

```latex
% Titled box environment
\newenvironment{titlebox}[1]
    {\begin{center}\textbf{#1}\\\begin{tabular}{|p{0.9\textwidth}|}
    \hline}
    {\\\hline\end{tabular}\end{center}}

% Usage
\begin{titlebox}{Important Information}
    This content appears in a box with a title.
\end{titlebox}
```

```latex
% Colored section environment
\usepackage{xcolor}

\newenvironment{coloredsection}[2]
    {\section{#1}\color{#2}}
    {\color{black}}

% Usage
\begin{coloredsection}{Introduction}{blue}
    This entire section will be in blue.
\end{coloredsection}
```

### Environments with Optional Arguments

```latex
\newenvironment{envname}[num_args][default]
    {begin code}
    {end code}
```

### Example with Optional Argument

```latex
% Note environment with optional type
\newenvironment{note}[1][Note]
    {\begin{center}\begin{minipage}{0.9\textwidth}
    \textbf{#1:} \itshape}
    {\end{minipage}\end{center}}

% Usage
\begin{note}
    This is a standard note.
\end{note}

\begin{note}[Tip]
    This is a tip.
\end{note}

\begin{note}[Warning]
    This is a warning.
\end{note}
```

### When to Use Commands vs Environments

#### Use Commands (`\newcommand`) when:

1. **Inline formatting**: Short text or symbols
2. **Single argument**: Simple text transformation
3. **Mathematical notation**: Operators, symbols
4. **Quick replacements**: Abbreviations, names

```latex
% ✅ Good use of commands
\newcommand{\R}{\mathbb{R}}
\newcommand{\highlight}[1]{\textcolor{yellow}{#1}}
\newcommand{\important}[1]{\textbf{#1}}
```

#### Use Environments (`\newenvironment`) when:

1. **Block-level content**: Paragraphs, lists, multiple elements
2. **Complex formatting**: Headers, footers, borders
3. **Scope management**: Temporary settings
4. **Structural elements**: Theorems, examples, exercises

```latex
% ✅ Good use of environments
\newenvironment{theorem}
    {\begin{tcolorbox}[title=Theorem]\itshape}
    {\end{tcolorbox}}

\newenvironment{example}
    {\par\noindent\textbf{Example:}\begin{quote}}
    {\end{quote}}
```

### Advanced Environment Techniques

#### 1. Saving Arguments for End Code

Since arguments aren't available in end code, you need to save them:

```latex
\newenvironment{savingbox}[1]
    {\def\savedtitle{#1}% Save argument
    \begin{center}\textbf{\savedtitle}\\
    \begin{tabular}{|p{0.8\textwidth}|}
    \hline}
    {\\\hline
    \end{tabular}\\\textit{End of \savedtitle}
    \end{center}}

% Usage
\begin{savingbox}{My Title}
    Content goes here.
\end{savingbox}
```

#### 2. Counters in Environments

```latex
\newcounter{examplenum}
\newenvironment{example}
    {\stepcounter{examplenum}
    \par\noindent\textbf{Example \theexamplenum:}\begin{quote}}
    {\end{quote}}

% Usage
\begin{example}
    First example content.
\end{example}

\begin{example}
    Second example content (automatically numbered).
\end{example}
```

#### 3. Theorem-like Environments

```latex
\usepackage{amsthm}
\usepackage{tcolorbox}

% Custom theorem environment with colored box
\newenvironment{mytheorem}[1][]
    {\begin{tcolorbox}[colback=blue!5, colframe=blue!75!black, title=Theorem]
    \ifx&#1&\else\textbf{(#1)}\fi\par}
    {\end{tcolorbox}}

% Usage
\begin{mytheorem}
    In a right triangle, $a^2 + b^2 = c^2$.
\end{mytheorem}

\begin{mytheorem}[Pythagorean]
    In a right triangle, $a^2 + b^2 = c^2$.
\end{mytheorem}
```

#### 4. Environments with Different Begin/End Formatting

```latex
\usepackage{framed, xcolor}

\newenvironment{importantbox}
    {\begin{leftbar}\color{red}\textbf{Important:}\par}
    {\end{leftbar}}

% Usage
\begin{importantbox}
    This is critical information that needs attention.
    It can span multiple paragraphs.

    Like this one.
\end{importantbox}
```

### Practical Environment Examples

#### 1. Exercise Environment with Numbering

```latex
\newcounter{exercisenum}[section]  % Reset per section

\newenvironment{exercise}
    {\stepcounter{exercisenum}
    \par\medskip\noindent
    \textbf{Exercise \thesection.\theexercisenum:}\par\nopagebreak}
    {\par\medskip}

% Usage
\section{Calculus}

\begin{exercise}
    Calculate the derivative of $f(x) = x^2 + 3x + 2$.
\end{exercise}

\begin{exercise}
    Find the integral of $g(x) = \sin(x)$.
\end{exercise}
```

#### 2. Code Listing Environment

```latex
\usepackage{listings, xcolor}

\newenvironment{pythoncode}
    {\lstset{language=Python,
             basicstyle=\ttfamily\small,
             backgroundcolor=\color{gray!10},
             frame=single,
             numbers=left}
    \lstset{}}
    {}

% Usage
\begin{pythoncode}
def factorial(n):
    if n == 0:
        return 1
    return n * factorial(n-1)
\end{pythoncode}
```

#### 3. Solution Environment (Toggle Visibility)

```latex
\usepackage{comment}

% Define a boolean for showing solutions
\newif\ifshowsolutions
\showsolutionstrue  % Set to \showsolutionsfalse to hide

\ifshowsolutions
    \newenvironment{solution}
        {\par\noindent\textbf{Solution:}\begin{quote}\color{blue}}
        {\end{quote}}
\else
    \excludecomment{solution}
\fi

% Usage
\begin{exercise}
    Prove that $1 + 1 = 2$.
\end{exercise}

\begin{solution}
    This follows from the Peano axioms.
\end{solution}
```

#### 4. Multi-Column Environment

```latex
\usepackage{multicol}

\newenvironment{twocolumns}
    {\begin{multicols}{2}}
    {\end{multicols}}

% Usage
\begin{twocolumns}
    This text will automatically flow into two columns.
    
    It can contain multiple paragraphs and will balance
    the content between columns.
\end{twocolumns}
```

### Combining Commands and Environments

You can create powerful combinations:

```latex
% Environment for exercises
\newcounter{exercisenum}
\newenvironment{exercise}
    {\stepcounter{exercisenum}\par\medskip\noindent
    \textbf{Exercise \theexercisenum:}\par}
    {\par\medskip}

% Command for referencing exercises
\newcommand{\exref}[1]{Exercise~\ref{ex:#1}}

% Usage
\begin{exercise}\label{ex:first}
    Calculate $2 + 2$.
\end{exercise}

As we saw in \exref{first}, basic arithmetic is important.
```

### Renewing Environments

```latex
% Renew existing environment
\renewenvironment{quote}
    {\begin{center}\begin{minipage}{0.8\textwidth}\itshape}
    {\end{minipage}\end{center}}

% Now all \begin{quote}...\end{quote} will use new format
```

### Best Practices for Environments

1. **Use semantic names**: `\begin{theorem}` not `\begin{bluebox}`
2. **Document your environments**: Explain purpose and usage
3. **Handle spacing properly**: Use `\par`, `\medskip`, etc.
4. **Consider nesting**: Will your environment work inside others?
5. **Test edge cases**: Empty content, long content, special characters
6. **Use packages**: `amsthm`, `tcolorbox`, `mdframed` for complex boxes

### Common Mistakes to Avoid

```latex
% ❌ Bad: Trying to use argument in end code
\newenvironment{badbox}[1]
    {\textbf{#1:}}
    {\textit{End of #1}}  % #1 not available here!

% ✅ Good: Save argument for later use
\newenvironment{goodbox}[1]
    {\def\savedtitle{#1}\textbf{\savedtitle:}}
    {\textit{End of \savedtitle}}
```

```latex
% ❌ Bad: Forgetting scoping
\newenvironment{colortext}
    {\color{blue}}
    {}  % Color continues after environment!

% ✅ Good: Proper scoping
\newenvironment{colortext}
    {\color{blue}}
    {\color{black}}  % Reset color
```

### Complete Example: Custom Document Structure

```latex
\documentclass{article}
\usepackage{xcolor, tcolorbox, amsmath}

% ===================================
% CUSTOM ENVIRONMENTS
% ===================================

% Theorem environment
\newcounter{theoremnum}
\newenvironment{theorem}[1][]
    {\stepcounter{theoremnum}
    \begin{tcolorbox}[colback=blue!5, colframe=blue!75!black,
                      title=Theorem \thetheorem num\ifx&#1&\else: #1\fi]}
    {\end{tcolorbox}}

% Example environment
\newcounter{examplenum}
\newenvironment{example}
    {\stepcounter{examplenum}
    \par\medskip\noindent\textbf{Example \theexamplenum:}\par\nopagebreak}
    {\par\medskip}

% Solution environment
\newenvironment{solution}
    {\par\noindent\textit{Solution:}\begin{quote}}
    {\end{quote}}

% Note box
\newenvironment{notebox}[1][Note]
    {\begin{center}\begin{tcolorbox}[colback=yellow!10, colframe=orange,
                                      title=#1, width=0.9\textwidth]}
    {\end{tcolorbox}\end{center}}

% ===================================
% CUSTOM COMMANDS (for comparison)
% ===================================

\newcommand{\R}{\mathbb{R}}
\newcommand{\important}[1]{\textbf{\textcolor{red}{#1}}}

\begin{document}

\section{Mathematical Foundations}

\begin{theorem}[Fundamental Theorem of Calculus]
    Let $f: [a,b] \to \R$ be continuous. Then:
    \[
        \int_a^b f(x)\,dx = F(b) - F(a)
    \]
    where $F$ is an antiderivative of $f$.
\end{theorem}

\begin{example}
    Calculate $\int_0^1 x^2\,dx$.
\end{example}

\begin{solution}
    Using the power rule:
    \[
        \int_0^1 x^2\,dx = \left[\frac{x^3}{3}\right]_0^1 = \frac{1}{3}
    \]
\end{solution}

\begin{notebox}[Important]
    The \important{Fundamental Theorem of Calculus} connects
    differentiation and integration.
\end{notebox}

\end{document}
```

### Summary: Commands vs Environments

**Use `\newcommand` for:**
- ✅ Inline text/symbols
- ✅ Short formatting
- ✅ Mathematical notation
- ✅ Single-argument transformations

**Use `\newenvironment` for:**
- ✅ Block-level content
- ✅ Multiple paragraphs
- ✅ Complex formatting with begin/end structure
- ✅ Structural document elements
- ✅ Scoped settings

**Remember:**
- Commands process their arguments immediately
- Environments create a scope from `\begin` to `\end`
- Environments can contain multiple elements (paragraphs, lists, etc.)
- Environment arguments are only available in begin code (save them if needed in end code)

---

## Advanced Techniques

### Starred Commands

Define variants with and without star using `xparse` package:

```latex
\usepackage{xparse}

% Define command with optional star
\NewDocumentCommand{\myemph}{s m}{
    \IfBooleanTF{#1}
        {\textit{\textbf{#2}}}  % Starred version: italic and bold
        {\textit{#2}}           % Regular version: just italic
}

% Usage
\myemph{regular emphasis}
\myemph*{strong emphasis}
```

### Commands with Multiple Optional Arguments

```latex
\usepackage{xparse}

% Command with two optional arguments
\NewDocumentCommand{\mybox}{O{blue} O{white} m}{
    \colorbox{#1}{\textcolor{#2}{#3}}
}

% Usage
\mybox{text}                    % Default: blue background, white text
\mybox[red]{text}               % Red background, white text
\mybox[green][black]{text}      % Green background, black text
```

### Robust Commands

Make commands work in moving arguments (like captions):

```latex
\DeclareRobustCommand{\mycommand}[1]{definition}

% Or protect when using
\caption{This is a \protect\mycommand{special} caption}
```

### Conditional Commands

```latex
% Check if argument is empty
\newcommand{\optionaltext}[1]{
    \ifx&#1&
        Default text
    \else
        #1
    \fi
}
```

### Commands with Counters

```latex
\newcounter{examplecounter}
\newcommand{\example}{
    \stepcounter{examplecounter}
    \textbf{Example \theexamplecounter:}
}

% Usage
\example This is the first example.
\example This is the second example.
```

---

## Best Practices

### 1. Naming Conventions

```latex
% ✅ Good: Descriptive, clear names
\newcommand{\highlight}[1]{\textcolor{yellow}{#1}}
\newcommand{\vectornorm}[1]{\left\| #1 \right\|}

% ❌ Bad: Cryptic, unclear names
\newcommand{\h}[1]{\textcolor{yellow}{#1}}
\newcommand{\vn}[1]{\left\| #1 \right\|}
```

### 2. Use Semantic Names

```latex
% ✅ Good: Semantic naming
\newcommand{\important}[1]{\textbf{#1}}
\newcommand{\technical}[1]{\texttt{#1}}

% ❌ Bad: Presentation-focused naming
\newcommand{\bold}[1]{\textbf{#1}}
\newcommand{\mono}[1]{\texttt{#1}}
```

### 3. Document Your Commands

```latex
% ===================================
% CUSTOM COMMANDS
% ===================================

% \highlight{text} - Highlights text in yellow
\newcommand{\highlight}[1]{\colorbox{yellow}{#1}}

% \vect{symbol} - Formats mathematical vectors
\newcommand{\vect}[1]{\mathbf{#1}}

% \diff[order]{function} - Derivative notation
% Optional: order (default 1)
% Required: function
\newcommand{\diff}[2][1]{\frac{d^{#1}#2}{dx^{#1}}}
```

### 4. Group Related Commands

```latex
% ===================================
% MATHEMATICAL NOTATION
% ===================================
\newcommand{\R}{\mathbb{R}}
\newcommand{\N}{\mathbb{N}}
\newcommand{\Z}{\mathbb{Z}}
\newcommand{\Q}{\mathbb{Q}}
\newcommand{\C}{\mathbb{C}}

% ===================================
% TEXT FORMATTING
% ===================================
\newcommand{\important}[1]{\textbf{\textcolor{red}{#1}}}
\newcommand{\keyword}[1]{\texttt{\textcolor{blue}{#1}}}
\newcommand{\note}[1]{\textit{\textcolor{gray}{#1}}}
```

### 5. Use Packages for Complex Needs

For very complex command definitions, consider using dedicated packages:

- `xparse` - Advanced command definitions
- `etoolbox` - Programming tools
- `xifthen` - Enhanced conditionals
- `calc` - Calculations

### 6. Test Your Commands

```latex
% Always test edge cases
\newcommand{\divide}[2]{\frac{#1}{#2}}

% Test with:
\divide{1}{2}           % Simple
\divide{a+b}{c-d}       % Expressions
\divide{\frac{1}{2}}{3} % Nested
```

---

## Common Use Cases

### 1. Mathematical Notation

```latex
% Common mathematical sets
\newcommand{\R}{\mathbb{R}}
\newcommand{\N}{\mathbb{N}}
\newcommand{\Z}{\mathbb{Z}}

% Vector and matrix operations
\newcommand{\vect}[1]{\boldsymbol{#1}}
\newcommand{\mat}[1]{\mathbf{#1}}
\newcommand{\transpose}[1]{#1^{\top}}

% Calculus
\newcommand{\diff}[2]{\frac{\partial #1}{\partial #2}}
\newcommand{\integral}[4]{\int_{#1}^{#2} #3 \, d#4}

% Usage
Let $f: \R \to \R$ with $\vect{x} \in \R^n$.
The derivative is $\diff{f}{x}$.
```

### 2. Consistent Formatting

```latex
% Document-specific terms
\newcommand{\projectname}{Project Phoenix}
\newcommand{\version}{v2.1.3}
\newcommand{\company}{Acme Corporation}

% Formatting shortcuts
\newcommand{\code}[1]{\texttt{#1}}
\newcommand{\file}[1]{\texttt{\textcolor{blue}{#1}}}
\newcommand{\path}[1]{\texttt{\textcolor{gray}{#1}}}

% Usage
Welcome to \projectname{} version \version{}.
Open the \file{config.json} file in \path{/etc/app/}.
```

### 3. Shorthand for Complex Expressions

```latex
% Probability notation
\newcommand{\prob}[1]{\mathbb{P}\left(#1\right)}
\newcommand{\expect}[1]{\mathbb{E}\left[#1\right]}
\newcommand{\variance}[1]{\text{Var}\left(#1\right)}

% Usage
$\prob{X > 0} = 0.5$
$\expect{X} = \mu$
$\variance{X} = \sigma^2$
```

### 4. Theorem Environments

```latex
\usepackage{amsthm}

% Define theorem styles
\theoremstyle{definition}
\newtheorem{theorem}{Theorem}[section]
\newtheorem{lemma}[theorem]{Lemma}
\newtheorem{proposition}[theorem]{Proposition}

% Custom command for quick theorems
\newcommand{\thm}[2]{
    \begin{theorem}[#1]
        #2
    \end{theorem}
}

% Usage
\thm{Pythagorean Theorem}{
    In a right triangle, $a^2 + b^2 = c^2$.
}
```

### 5. Abbreviations

```latex
% Common abbreviations
\newcommand{\eg}{e.g.,\xspace}
\newcommand{\ie}{i.e.,\xspace}
\newcommand{\etc}{etc.\xspace}
\newcommand{\vs}{vs.\xspace}

% Usage (note: requires \usepackage{xspace})
This is useful, \eg when writing papers.
Multiple options exist, \ie option A, B, or C.
```

### 6. Citation Shortcuts

```latex
% Enhanced citations
\newcommand{\figref}[1]{Figure~\ref{fig:#1}}
\newcommand{\tabref}[1]{Table~\ref{tab:#1}}
\newcommand{\eqref}[1]{Equation~(\ref{eq:#1})}
\newcommand{\secref}[1]{Section~\ref{sec:#1}}

% Usage
As shown in \figref{results}, the data supports...
See \tabref{comparison} for details.
According to \eqref{main}, we have...
```

---

## Complete Example

Here's a complete document demonstrating custom commands:

```latex
\documentclass{article}
\usepackage{amsmath, amssymb}
\usepackage{xcolor}
\usepackage{xspace}

% ===================================
% CUSTOM COMMANDS
% ===================================

% Mathematical notation
\newcommand{\R}{\mathbb{R}}
\newcommand{\N}{\mathbb{N}}
\newcommand{\vect}[1]{\mathbf{#1}}
\newcommand{\norm}[1]{\left\| #1 \right\|}

% Derivatives
\newcommand{\diff}[2]{\frac{d#1}{d#2}}
\newcommand{\pdiff}[2]{\frac{\partial #1}{\partial #2}}

% Text formatting
\newcommand{\important}[1]{\textbf{\textcolor{red}{#1}}}
\newcommand{\keyword}[1]{\texttt{\textcolor{blue}{#1}}}

% Document-specific
\newcommand{\coursename}{Advanced Calculus}
\newcommand{\university}{MIT}

% Abbreviations
\newcommand{\eg}{e.g.,\xspace}
\newcommand{\ie}{i.e.,\xspace}

\title{Custom Commands Example}
\author{Student Name}
\date{\today}

\begin{document}

\maketitle

\section{Introduction}

Welcome to \coursename{} at \university. This document demonstrates custom commands.

\section{Mathematical Notation}

Let $f: \R \to \R$ be a differentiable function. The derivative is:
\[
    \diff{f}{x} = \lim_{h \to 0} \frac{f(x+h) - f(x)}{h}
\]

For a vector $\vect{v} \in \R^n$, the norm is $\norm{\vect{v}}$.

\section{Text Formatting}

The \keyword{gradient descent} algorithm is \important{fundamental} in optimization.

\section{Partial Derivatives}

For $f(x,y)$, the partial derivatives are:
\[
    \pdiff{f}{x} \quad \text{and} \quad \pdiff{f}{y}
\]

\section{Conclusion}

Custom commands make documents consistent and maintainable, \eg in mathematical notation.

\end{document}
```

---

## Additional Resources

- **LaTeX2e Command Reference**: https://www.latex-project.org/help/documentation/
- **xparse Package Documentation**: https://ctan.org/pkg/xparse
- **TeX Stack Exchange**: https://tex.stackexchange.com/questions/tagged/macros
- **Overleaf Custom Commands**: https://www.overleaf.com/learn/latex/Commands

---

## Summary

**Key Takeaways**:

1. Use `\newcommand` to define custom commands
2. Arguments are referenced with `#1`, `#2`, etc.
3. Optional arguments use `[default]` syntax
4. Use semantic naming for maintainability
5. Document your custom commands
6. Commands improve consistency and readability
7. Test edge cases thoroughly

**Command Types**:
- `\newcommand` - Define new command
- `\renewcommand` - Redefine existing command
- `\providecommand` - Define only if not exists
- `\DeclareRobustCommand` - For moving arguments

**Next Steps**:
- Experiment with simple commands
- Create your own command library
- Explore the `xparse` package for advanced features
- Study package source code for inspiration

---

**Last Updated**: October 2025
