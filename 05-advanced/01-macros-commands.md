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
- [Custom Environments with `\newenvironment`](#custom-environments-with-newenvironment)
- [Advanced Environment Definition with xparse](#advanced-environment-definition-with-xparse)
- [Pre-defined LaTeX Commands and Macros](#pre-defined-latex-commands-and-macros)
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

## Advanced Environment Definition with xparse

The `xparse` package provides `\NewDocumentEnvironment` and `\RenewDocumentEnvironment`, which are more powerful and flexible alternatives to `\newenvironment` and `\renewenvironment`.

### What is xparse?

`xparse` is a package that provides a unified interface for parsing command and environment arguments with more advanced features than the standard LaTeX approach. It's part of the LaTeX3 experimental toolkit and offers better control over argument types and error handling.

### Key Differences: `\newenvironment` vs `\NewDocumentEnvironment`

| Feature | `\newenvironment` | `\NewDocumentEnvironment` |
|---------|------------------|---------------------------|
| **Argument Syntax** | `[num_args][default]` | More flexible: `o`, `O`, `m`, `r`, `R`, `s`, `t`, `v`, `b`, `d` |
| **Multiple Optionals** | Only one optional | Can have multiple optional arguments |
| **Error Handling** | Limited | Better error messages |
| **Flexibility** | Basic | Supports complex argument patterns |
| **Documentation** | Less clear | Self-documenting with spec strings |
| **Package Required** | None | `xparse` |
| **Arguments in End Code** | Need manual save | Can be accessed directly in end code |

### `\NewDocumentEnvironment` Syntax

```latex
\usepackage{xparse}

\NewDocumentEnvironment{envname}{arg-spec}{begin-code}{end-code}
```

where `arg-spec` is a string describing the arguments using these codes:

#### Argument Specifiers for xparse

| Code | Type | Example |
|------|------|---------|
| `m` | Mandatory | `\begin{env}{arg}` |
| `r` | Required delimited | `\begin{env}<arg>` requires `<>` |
| `R` | Required delimited with default | `\begin{env}` or `\begin{env}<arg>` |
| `o` | Optional with default empty | `\begin{env}` or `\begin{env}[arg]` |
| `O` | Optional with custom default | `\begin{env}` or `\begin{env}[arg]` |
| `d` | Delimiter with default empty | `\begin{env}` or `\begin{env}<arg>` |
| `D` | Delimiter with custom default | `\begin{env}` or `\begin{env}<arg>` |
| `s` | Star modifier (boolean) | `\begin{env}*` or `\begin{env}` |
| `t` | Token modifier | `\begin{env}[token]` or `\begin{env}` |
| `v` | Verbatim/literal content | For protected content |
| `b` | Body between begin/end | The environment content |

### Simple `\NewDocumentEnvironment` Examples

#### Example 1: Basic Conversion from `\newenvironment`

**Old style (`\newenvironment`):**
```latex
\newenvironment{mybox}[1]
    {\begin{center}\textbf{#1}\end{center}}
    {}
```

**New style (`\NewDocumentEnvironment`):**
```latex
\usepackage{xparse}

\NewDocumentEnvironment{mybox}{m}
    {\begin{center}\textbf{#1}\end{center}}
    {}
```

#### Example 2: Multiple Optional Arguments

This is where `\NewDocumentEnvironment` shines! With `\newenvironment`, you can only have one optional argument. With `\NewDocumentEnvironment`, you can have multiple:

```latex
\usepackage{xparse}

% Two optional arguments with defaults
\NewDocumentEnvironment{colorbox}{O{blue} O{white}}
    {\begin{center}\colorbox{#1}{\textcolor{#2}{Content}}\end{center}}
    {}

% Usage
\begin{colorbox}
    % Blue background (default), white text (default)
\end{colorbox}

\begin{colorbox}[red]
    % Red background, white text (default)
\end{colorbox}

\begin{colorbox}[red][black]
    % Red background, black text
\end{colorbox}
```

#### Example 3: Optional with Custom Default

```latex
\NewDocumentEnvironment{emphasized}
    {O{emph}}  % Optional argument with default "emph"
    {%
        \IfValueTF{#1}{%
            \ifx #1emph\itshape\fi
            \ifx #1strong\bfseries\fi
            \ifx #1code\ttfamily\fi
        }{\itshape}%
    }
    {\normalfont}

% Usage
\begin{emphasized}
    Emphasize (default italic)
\end{emphasized}

\begin{emphasized}[strong]
    Strong emphasis (bold)
\end{emphasized}

\begin{emphasized}[code]
    Code formatting (typewriter)
\end{emphasized}
```

#### Example 4: Star Modifier

```latex
\NewDocumentEnvironment{theorem}{s m}
    {%
        \begin{center}
        \textbf{Theorem\IfBooleanT{#1}{*}: #2}
        \end{center}
    }
    {}

% Usage
\begin{theorem}{Pythagorean Theorem}
    $a^2 + b^2 = c^2$
\end{theorem}

\begin{theorem}*{Pythagorean Theorem}
    $a^2 + b^2 = c^2$ (without numbering)
\end{theorem}
```

#### Example 5: Delimiter Arguments

```latex
\NewDocumentEnvironment{formula}{r<>}
    {\[\text{Formula: } #1 \quad \text{or} \quad }
    {\]}

% Usage - requires <> delimiters
\begin{formula}<x^2 + y^2 = z^2>
    a^2 + b^2 = c^2
\end{formula}
```

#### Example 6: Arguments Available in Both Begin and End

This is a major advantage of `\NewDocumentEnvironment`! Arguments are available in both sections:

```latex
\NewDocumentEnvironment{titledbox}{m}
    {\textbf{#1:}\begin{quote}}
    {\end{quote}\textit{End of: #1}}  % #1 is accessible here!

% Usage
\begin{titledbox}{Warning}
    This is a warning message.
\end{titledbox}

% Output:
% Warning:
%     This is a warning message.
% End of: Warning
```

**Without xparse, you'd need:**
```latex
\newenvironment{titledbox}[1]
    {\def\mytitle{#1}\textbf{\mytitle:}\begin{quote}}
    {\end{quote}\textit{End of: \mytitle}}  % Must save it manually
```

#### Example 7: Complex Formatting Environment

```latex
\usepackage{xparse, tcolorbox}

\NewDocumentEnvironment{lesson}
    {m O{blue} m}  % name (required), color (optional), author (required)
    {%
        \begin{tcolorbox}[colback=#2!5, colframe=#2, title=Lesson: #1, subtitle=by #3]
    }
    {%
        \end{tcolorbox}
    }

% Usage
\begin{lesson}{Calculus}{green}{Dr. Smith}
    Content of the lesson goes here.
    This can span multiple paragraphs.
\end{lesson}

\begin{lesson}{Algebra}{red}{Prof. Jones}
    Another lesson with different color and author.
\end{lesson}
```

### `\RenewDocumentEnvironment` - Redefining Environments

Just like `\renewenvironment` renews existing environments, `\RenewDocumentEnvironment` does the same but with xparse's advanced features:

```latex
\usepackage{xparse}

% Redefine the standard itemize environment
\RenewDocumentEnvironment{itemize}{s}
    {\IfBooleanT{#1}
        {\begin{enumerate}}%
        {\begin{itemize}}%
    }
    {\IfBooleanT{#1}
        {\end{enumerate}}%
        {\end{itemize}}%
    }

% Usage
\begin{itemize}
    \item Bulleted item
\end{itemize}

\begin{itemize}*
    \item Numbered item  % Because we used star
\end{itemize}
```

### Conditional Logic in xparse

Use `\IfValueT`, `\IfValueF`, and `\IfValueTF` to handle optional arguments:

```latex
\NewDocumentEnvironment{note}{O{}}
    {%
        \textbf{Note\IfValueT{#1}{: #1}:}%
        \begin{quote}\small
    }
    {%
        \end{quote}
    }

% Usage
\begin{note}
    This is a generic note.
\end{note}

\begin{note}[Important]
    This is an important note.
\end{note}
```

### Comparison: Complete Example

Here's a complete example showing the same environment with both approaches:

**Method 1: Traditional `\newenvironment`**

```latex
\documentclass{article}
\usepackage{tcolorbox}

\newcounter{example}
\newenvironment{examplebox}[2][Example]
    {\stepcounter{example}
     \def\exampletitle{#1}
     \def\examplesubtitle{#2}
     \begin{tcolorbox}[colback=yellow!10, colframe=orange,
                       title=\exampletitle\ \theexample: \examplesubtitle]}
    {\end{tcolorbox}}

\begin{document}

\begin{examplebox}{Basic Usage}
    This is example 1.
\end{examplebox}

\begin{examplebox}[Custom]{Advanced Usage}
    This is example 2.
\end{examplebox}

\end{document}
```

**Method 2: Modern `\NewDocumentEnvironment`**

```latex
\documentclass{article}
\usepackage{xparse, tcolorbox}

\newcounter{example}

\NewDocumentEnvironment{examplebox}{O{Example} m}
    {%
        \stepcounter{example}%
        \begin{tcolorbox}[colback=yellow!10, colframe=orange,
                          title=#1\ \theexample: #2]%
    }
    {%
        \end{tcolorbox}%
    }

\begin{document}

\begin{examplebox}{Basic Usage}
    This is example 1.
\end{examplebox}

\begin{examplebox}[Custom]{Advanced Usage}
    This is example 2.
\end{examplebox}

\end{document}
```

The second approach is cleaner and more maintainable!

### Advantages of `\NewDocumentEnvironment`

1. **Multiple Optional Arguments**: Handle complex argument combinations
2. **Better Documentation**: Argument spec is self-explanatory
3. **Cleaner Syntax**: No need to manually save arguments
4. **Arguments in End Code**: Direct access to #1, #2, etc. everywhere
5. **More Flexible**: Support for delimiters, star modifiers, verbatim content
6. **Error Handling**: Better error messages from xparse
7. **Future-Proof**: Uses LaTeX3 infrastructure

### When to Use What

| Scenario | Recommendation |
|----------|-----------------|
| Simple environment, one optional arg | Either works, use `\newenvironment` if no xparse dependency |
| Multiple optional arguments | **Use `\NewDocumentEnvironment`** |
| Star modifier needed | **Use `\NewDocumentEnvironment`** |
| Complex argument patterns | **Use `\NewDocumentEnvironment`** |
| Arguments needed in end code | **Use `\NewDocumentEnvironment`** |
| Minimal dependencies needed | Use `\newenvironment` |
| Modern, well-maintained code | **Use `\NewDocumentEnvironment`** |

---

## Pre-defined LaTeX Commands and Macros

LaTeX provides many built-in commands and macros for common tasks. Here's a comprehensive reference of frequently used ones:

### Spacing Commands

| Command | Function | Usage |
|---------|----------|-------|
| `\par` | End paragraph | `\par` (same as blank line) |
| `\medskip` | Medium vertical space (~0.5 line) | `\medskip` |
| `\smallskip` | Small vertical space (~0.25 line) | `\smallskip` |
| `\bigskip` | Large vertical space (~1 line) | `\bigskip` |
| `\vspace{length}` | Custom vertical space | `\vspace{1cm}` |
| `\hspace{length}` | Custom horizontal space | `\hspace{2em}` |
| `\\` | Line break | `Line 1 \\ Line 2` |
| `\\[length]` | Line break with space | `\\[0.5cm]` |
| `\noindent` | Suppress paragraph indent | `\noindent Text` |
| `\indent` | Force paragraph indent | `\indent Text` |
| `\linebreak` | Break line, justify | `Text \linebreak more` |
| `\newline` | Break line, no justify | `Text \newline more` |
| `\newpage` | Start new page | `\newpage` |
| `\clearpage` | Flush floats, start page | `\clearpage` |
| `\quad` | 1 em space | `Text \quad more` |
| `\qquad` | 2 em space | `Text \qquad more` |
| `\enspace` | 0.5 em space | `Text \enspace more` |
| `\,` | Thin space (~3/18 em) | `Text \, more` |
| `\:` | Medium space (~4/18 em) | `Text \: more` |
| `\;` | Thick space (~5/18 em) | `Text \; more` |
| `\!` | Negative thin space | `Text \! more` |

### Text Formatting Commands

| Command | Function | Usage |
|---------|----------|-------|
| `\textbf{text}` | Bold text | `\textbf{bold}` |
| `\textit{text}` | Italic text | `\textit{italic}` |
| `\texttt{text}` | Typewriter/monospace | `\texttt{code}` |
| `\textsc{text}` | Small caps | `\textsc{Small Caps}` |
| `\textsl{text}` | Slanted text | `\textsl{slanted}` |
| `\textrm{text}` | Roman (serif) | `\textrm{roman}` |
| `\textsf{text}` | Sans serif | `\textsf{sans}` |
| `\textmd{text}` | Medium weight | `\textmd{medium}` |
| `\textup{text}` | Upright (non-italic) | `\textup{upright}` |
| `\emph{text}` | Emphasis (toggle italic) | `\emph{emphasized}` |
| `\underline{text}` | Underlined text | `\underline{underlined}` |
| `\uppercase{text}` | Uppercase text | `\uppercase{Small}` → `SMALL` |
| `\lowercase{text}` | Lowercase text | `\lowercase{SMALL}` → `small` |
| `\MakeUppercase{text}` | Make uppercase | `\MakeUppercase{text}` |
| `\MakeLowercase{text}` | Make lowercase | `\MakeLowercase{TEXT}` |

### Font Commands

| Command | Function | Usage |
|---------|----------|-------|
| `\bfseries` | Bold series (declaration) | `{\bfseries bold text}` |
| `\itshape` | Italic shape (declaration) | `{\itshape italic text}` |
| `\ttfamily` | Typewriter family (declaration) | `{\ttfamily code}` |
| `\sffamily` | Sans serif family (declaration) | `{\sffamily sans}` |
| `\rmfamily` | Roman family (declaration) | `{\rmfamily roman}` |
| `\mdseries` | Medium series (declaration) | `{\mdseries medium}` |
| `\normalfont` | Reset to normal | `{\bfseries text \normalfont normal}` |
| `\slshape` | Slanted shape (declaration) | `{\slshape slanted}` |
| `\upshape` | Upright shape (declaration) | `{\upshape upright}` |
| `\tiny` | Tiny size | `{\tiny tiny}` |
| `\scriptsize` | Script size | `{\scriptsize small}` |
| `\footnotesize` | Footnote size | `{\footnotesize smaller}` |
| `\small` | Small size | `{\small small}` |
| `\normalsize` | Normal size | `{\normalsize normal}` |
| `\large` | Large size | `{\large large}` |
| `\Large` | Larger size | `{\Large larger}` |
| `\LARGE` | Very large size | `{\LARGE very large}` |
| `\huge` | Huge size | `{\huge huge}` |
| `\Huge` | Largest size | `{\Huge largest}` |

### Paragraph Formatting

| Command | Function | Usage |
|---------|----------|-------|
| `\centering` | Center text (declaration) | `{\centering centered}` |
| `\raggedright` | Left-align (declaration) | `{\raggedright left}` |
| `\raggedleft` | Right-align (declaration) | `{\raggedleft right}` |
| `\justify` | Justify text (declaration) | `{\justify justified}` |
| `\singlespacing` | Single spacing | `{\singlespacing text}` |
| `\onehalfspacing` | 1.5 spacing (needs setspace) | `{\onehalfspacing text}` |
| `\doublespacing` | Double spacing (needs setspace) | `{\doublespacing text}` |

### Structural Commands

| Command | Function | Usage |
|---------|----------|-------|
| `\section{title}` | First-level heading | `\section{Introduction}` |
| `\subsection{title}` | Second-level heading | `\subsection{Background}` |
| `\subsubsection{title}` | Third-level heading | `\subsubsection{Details}` |
| `\paragraph{title}` | Paragraph heading | `\paragraph{Note}` |
| `\subparagraph{title}` | Sub-paragraph heading | `\subparagraph{Detail}` |
| `\section*{title}` | Unnumbered heading | `\section*{Appendix}` |
| `\tableofcontents` | Generate table of contents | `\tableofcontents` |
| `\listoffigures` | List of figures | `\listoffigures` |
| `\listoftables` | List of tables | `\listoftables` |
| `\appendix` | Start appendix | `\appendix` |

### References and Labels

| Command | Function | Usage |
|---------|----------|-------|
| `\label{name}` | Create label | `\label{fig:example}` |
| `\ref{name}` | Reference number | `See \ref{fig:example}` |
| `\pageref{name}` | Reference page number | `Page \pageref{fig:example}` |
| `\cite{key}` | Citation | `\cite{author2020}` |
| `\footnote{text}` | Footnote | `Text\footnote{note}` |
| `\index{term}` | Index entry (needs makeidx) | `\index{term}` |

### List Commands

| Command | Function | Usage |
|---------|----------|-------|
| `\item` | List item | In `itemize`, `enumerate`, `description` |
| `\begin{itemize}` | Unordered list | `\begin{itemize}\item text\end{itemize}` |
| `\begin{enumerate}` | Ordered list | `\begin{enumerate}\item text\end{enumerate}` |
| `\begin{description}` | Description list | `\begin{description}\item[term]definition\end{description}` |
| `\setcounter{enumi}{n}` | Set list counter | `\setcounter{enumi}{5}` |

### Box and Frame Commands

| Command | Function | Usage |
|---------|----------|-------|
| `\mbox{text}` | No-break box | `\mbox{no break}` |
| `\makebox[width]{text}` | Box with width | `\makebox[5cm]{centered}` |
| `\fbox{text}` | Framed box | `\fbox{boxed text}` |
| `\framebox[width]{text}` | Framed box with width | `\framebox[5cm]{text}` |
| `\parbox{width}{text}` | Paragraph in box | `\parbox{5cm}{multiline text}` |
| `\begin{minipage}{width}` | Mini page environment | `\begin{minipage}{5cm}...\end{minipage}` |
| `\rule{width}{height}` | Horizontal rule | `\rule{5cm}{1pt}` |
| `\hline` | Horizontal line in table | Used in tabular |
| `\vline` | Vertical line in table | Used in tabular |

### Math Mode Commands

| Command | Function | Usage |
|---------|----------|-------|
| `$...$` | Inline math | `$x^2 + y^2 = z^2$` |
| `\(...\)` | Inline math (alternative) | `\(x^2\)` |
| `$$...$$` | Display math | `$$x^2 + y^2 = z^2$$` |
| `\[...\]` | Display math (alternative) | `\[x^2 + y^2 = z^2\]` |
| `\begin{equation}` | Numbered equation | `\begin{equation}...\end{equation}` |
| `\begin{equation*}` | Unnumbered equation | `\begin{equation*}...\end{equation*}` |
| `\frac{num}{den}` | Fraction | `$\frac{1}{2}$` |
| `\sqrt{x}` | Square root | `$\sqrt{x}$` |
| `\sqrt[n]{x}` | n-th root | `$\sqrt[3]{x}$` |
| `\sum` | Summation | `$\sum_{i=1}^{n}$` |
| `\prod` | Product | `$\prod_{i=1}^{n}$` |
| `\int` | Integral | `$\int_a^b f(x)dx$` |
| `\lim` | Limit | `$\lim_{x \to \infty}$` |
| `\sin`, `\cos`, `\tan` | Trig functions | `$\sin(x)$` |
| `\log`, `\ln`, `\exp` | Logarithm functions | `$\log(x)$` |
| `\mathbb{R}` | Blackboard bold | `$\mathbb{R}$` for ℝ |
| `\mathbf{v}` | Bold vector | `$\mathbf{v}$` |
| `\mathit{text}` | Italic in math | `$\mathit{text}$` |
| `\mathcal{L}` | Calligraphic letters | `$\mathcal{L}$` |
| `\mathrm{text}` | Roman in math mode | `$\mathrm{const}$` |

### Special Characters and Symbols

| Command | Function | Output |
|---------|----------|--------|
| `\`{a}` | Accent grave | à |
| `\'{a}` | Accent acute | á |
| `\^{a}` | Circumflex accent | â |
| `\"{a}` | Diaeresis (umlaut) | ä |
| `\~{a}` | Tilde | ã |
| `\={a}` | Macron | ā |
| `\u{a}` | Breve | ă |
| `\v{a}` | Caron | ǎ |
| `\H{a}` | Double acute | ő |
| `\t{aa}` | Tie bar | a͡a |
| `\c{c}` | Cedilla | ç |
| `\d{a}` | Dot below | ạ |
| `\b{a}` | Bar below | a̶ |
| `\copyright` | Copyright | © |
| `\textregistered` | Registered | ® |
| `\dag` | Dagger | † |
| `\ddag` | Double dagger | ‡ |
| `\S` | Section sign | § |
| `\P` | Pilcrow | ¶ |
| `\pounds` | Pound sign | £ |
| `\textyen` | Yen sign | ¥ |
| `\textcurrency` | Currency sign | ¤ |
| `\textdegree` | Degree | ° |
| `\textpromile` | Per mille | ‰ |
| `\ldots` | Ellipsis | … |
| `\textendash` | En-dash | – |
| `\textemdash` | Em-dash | — |
| `\textquoteleft` | Left quote | ' |
| `\textquoteright` | Right quote | ' |
| `\textquotedblleft` | Left double quote | " |
| `\textquotedblright` | Right double quote | " |

### Counter Commands

| Command | Function | Usage |
|---------|----------|-------|
| `\newcounter{name}` | Create counter | `\newcounter{mycnt}` |
| `\setcounter{name}{value}` | Set counter value | `\setcounter{page}{1}` |
| `\addtocounter{name}{value}` | Add to counter | `\addtocounter{page}{2}` |
| `\stepcounter{name}` | Increment counter | `\stepcounter{section}` |
| `\the<counter>` | Display counter | `\thepage`, `\thesection` |
| `\arabic{name}` | Arabic numerals | `\arabic{counter}` |
| `\roman{name}` | Lowercase Roman | `\roman{counter}` |
| `\Roman{name}` | Uppercase Roman | `\Roman{counter}` |
| `\alph{name}` | Lowercase letters | `\alph{counter}` |
| `\Alph{name}` | Uppercase letters | `\Alph{counter}` |

### Conditional Commands

| Command | Function | Usage |
|---------|----------|-------|
| `\ifx` | Compare tokens | `\ifx a b ... \fi` |
| `\ifdim` | Compare dimensions | `\ifdim 5cm > 3cm ... \fi` |
| `\ifnum` | Compare numbers | `\ifnum 5 > 3 ... \fi` |
| `\ifvoid` | Check box | `\ifvoid 0 ... \fi` |
| `\iftrue` | Always true | `\iftrue ... \fi` |
| `\iffalse` | Always false | `\iffalse ... \fi` |
| `\else` | Else clause | `\if ... \else ... \fi` |
| `\fi` | End conditional | Required |

### Commonly Used Utility Commands

| Command | Function | Usage |
|---------|----------|-------|
| `\strut` | Invisible strut | `\strut text` (for alignment) |
| `\phantom{text}` | Invisible space | Reserve space for text |
| `\hphantom{text}` | Horizontal phantom | `\hphantom{text}` |
| `\vphantom{text}` | Vertical phantom | `\vphantom{text}` |
| `\smash{text}` | Remove height/depth | `\smash{text}` |
| `\relax` | No operation | `\relax` |
| `\protect` | Protect command | `\protect\command` |
| `\expandafter` | Expand next token | Advanced usage |
| `\input{file}` | Include file | `\input{header}` |
| `\include{file}` | Include with page break | `\include{chapter1}` |
| `\includeonly{file}` | Only process certain files | `\includeonly{chapter1,chapter2}` |

### Example: Using Pre-defined Macros

```latex
\documentclass{article}

\begin{document}

% Spacing examples
\noindent This paragraph starts without indentation.
\par
Normal paragraph starts here with indentation.

\smallskip
\noindent Small gap above this line.

\medskip
\noindent Medium gap above this line.

\bigskip
\noindent Big gap above this line.

% Text formatting examples
Normal text \textbf{bold text} \textit{italic text} \texttt{code}.

% Font size examples
{\tiny Tiny text}
{\small Small text}
{\normalsize Normal text}
{\large Large text}
{\LARGE Very large text}
{\huge Huge text}

% Box examples
\fbox{This text is in a box}

\parbox{5cm}{This is a paragraph box with a width of 5cm.
It can contain multiple lines of text.}

\end{document}
```

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
