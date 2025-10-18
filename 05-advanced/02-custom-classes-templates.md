# Creating Custom Classes and Templates

## Introduction

LaTeX classes and templates allow you to create reusable document structures with consistent formatting. This tutorial covers creating your own document classes (`.cls` files) and templates for specific document types.

## Table of Contents

- [Classes vs Templates vs Packages](#classes-vs-templates-vs-packages)
- [When to Create a Custom Class](#when-to-create-a-custom-class)
- [Basic Class Structure](#basic-class-structure)
- [Creating a Simple Class](#creating-a-simple-class)
- [Class Options](#class-options)
- [Loading Packages in Classes](#loading-packages-in-classes)
- [Custom Commands in Classes](#custom-commands-in-classes)
- [Page Layout and Formatting](#page-layout-and-formatting)
- [Complete Class Examples](#complete-class-examples)
- [Creating Document Templates](#creating-document-templates)
- [Best Practices](#best-practices)
- [Distribution and Sharing](#distribution-and-sharing)

---

## Classes vs Templates vs Packages

### Document Class (.cls)

A **class** defines the overall structure and default formatting of a document type.

```latex
\documentclass{myclass}  % Uses myclass.cls
```

**Use for**: Defining document types (article, book, report, custom formats)

### Template (.tex)

A **template** is a pre-configured LaTeX document ready to fill in.

```latex
% template.tex - already has documentclass, packages, structure
\documentclass{article}
\usepackage{...}
\title{...}
\begin{document}
...
\end{document}
```

**Use for**: Providing starting points for specific documents

### Package (.sty)

A **package** adds features and functionality to any document class.

```latex
\usepackage{mypackage}  % Uses mypackage.sty
```

**Use for**: Reusable functionality across different document types

### Quick Comparison

| Feature | Class (.cls) | Template (.tex) | Package (.sty) |
|---------|--------------|-----------------|----------------|
| Purpose | Document structure | Ready-to-use doc | Add features |
| File type | `.cls` | `.tex` | `.sty` |
| Usage | `\documentclass{}` | Copy & edit | `\usepackage{}` |
| Examples | article, book | CV, thesis | graphicx, amsmath |

---

## When to Create a Custom Class

Create a custom class when you need:

1. **Standardized documents** across an organization
2. **Repeated structure** for multiple similar documents
3. **Custom title pages** or formatting requirements
4. **Specific journal/conference** submission formats
5. **Company branding** requirements

### Examples of Good Class Candidates

- Company letterheads
- Academic theses with specific formatting
- Conference proceedings papers
- Internal technical reports
- Custom CVs/resumes
- Book series with consistent style

---

## Basic Class Structure

Every LaTeX class file has this basic structure:

```latex
% myclass.cls

% 1. Identification
\NeedsTeXFormat{LaTeX2e}
\ProvidesClass{myclass}[2025/10/17 My Custom Class]

% 2. Preliminary declarations
% (Options, variables, etc.)

% 3. Options processing
\DeclareOption*{\PassOptionsToClass{\CurrentOption}{article}}
\ProcessOptions\relax

% 4. Load base class
\LoadClass{article}

% 5. Main code
% (Packages, commands, formatting)

% 6. Additional declarations
% (Final setup)
```

### Essential Components Explained

#### 1. Identification

```latex
\NeedsTeXFormat{LaTeX2e}
\ProvidesClass{classname}[date description]
```

Specifies LaTeX version required and class information.

#### 2. Base Class Loading

```latex
\LoadClass[options]{baseclass}
```

Most custom classes build upon existing ones (article, report, book).

#### 3. Required Packages

```latex
\RequirePackage{packagename}
```

Similar to `\usepackage`, but used in class files.

---

## Creating a Simple Class

Let's create a simple class for technical reports.

### Step 1: Create `techreport.cls`

```latex
% techreport.cls - Simple Technical Report Class
\NeedsTeXFormat{LaTeX2e}
\ProvidesClass{techreport}[2025/10/17 Technical Report Class]

% Load base class
\LoadClass[12pt,a4paper]{article}

% Required packages
\RequirePackage{geometry}
\RequirePackage{fancyhdr}
\RequirePackage{graphicx}
\RequirePackage{xcolor}

% Page geometry
\geometry{
    left=1in,
    right=1in,
    top=1in,
    bottom=1in
}

% Custom colors
\definecolor{reportblue}{RGB}{0,51,102}

% Header and footer
\pagestyle{fancy}
\fancyhf{}
\fancyhead[L]{\leftmark}
\fancyhead[R]{\thepage}
\renewcommand{\headrulewidth}{0.4pt}

% Title formatting
\renewcommand{\maketitle}{%
    \begin{titlepage}
        \centering
        \vspace*{2cm}
        {\Huge\bfseries\color{reportblue}\@title\par}
        \vspace{1cm}
        {\Large\@author\par}
        \vspace{0.5cm}
        {\large\@date\par}
        \vfill
    \end{titlepage}
}
```

### Step 2: Use the Class

```latex
% mydocument.tex
\documentclass{techreport}

\title{My Technical Report}
\author{John Doe}
\date{\today}

\begin{document}

\maketitle

\section{Introduction}
This is my technical report using the custom class.

\section{Methods}
Content here...

\end{document}
```

**Important**: The `.cls` file must be in the same directory as your `.tex` file, or in your LaTeX path.

---

## Class Options

Allow users to customize the class behavior with options.

### Declaring Options

```latex
% In your .cls file

% Boolean option
\newif\if@twocolumn
\@twocolumnfalse  % Default

\DeclareOption{twocolumn}{%
    \@twocolumntrue
}

% Option with parameter
\newcommand{\@fontsize}{12pt}
\DeclareOption{10pt}{\renewcommand{\@fontsize}{10pt}}
\DeclareOption{11pt}{\renewcommand{\@fontsize}{11pt}}
\DeclareOption{12pt}{\renewcommand{\@fontsize}{12pt}}

% Pass unknown options to base class
\DeclareOption*{\PassOptionsToClass{\CurrentOption}{article}}

% Process options
\ProcessOptions\relax

% Load base class with options
\LoadClass[\@fontsize]{article}
```

### Using Options

```latex
\documentclass[twocolumn,11pt]{myclass}
```

### Complete Example with Options

```latex
% report.cls - Class with options
\NeedsTeXFormat{LaTeX2e}
\ProvidesClass{report}[2025/10/17 Custom Report Class]

% Options
\newif\if@colorlinks
\@colorlinksfalse

\newif\if@draft
\@draftfalse

\DeclareOption{colorlinks}{\@colorlinkstrue}
\DeclareOption{draft}{\@drafttrue}
\DeclareOption*{\PassOptionsToClass{\CurrentOption}{article}}
\ProcessOptions\relax

\LoadClass[a4paper]{article}

% Conditional package loading
\if@colorlinks
    \RequirePackage[colorlinks=true,linkcolor=blue]{hyperref}
\else
    \RequirePackage[hidelinks]{hyperref}
\fi

\if@draft
    \RequirePackage[draft]{graphicx}
    \RequirePackage{draftwatermark}
    \SetWatermarkText{DRAFT}
    \SetWatermarkScale{5}
\fi
```

Usage:
```latex
\documentclass[colorlinks,draft]{report}
```

---

## Loading Packages in Classes

Use `\RequirePackage` instead of `\usepackage` in class files.

### Basic Package Loading

```latex
% In myclass.cls
\RequirePackage{amsmath}
\RequirePackage{graphicx}
\RequirePackage[utf8]{inputenc}
```

### Conditional Package Loading

```latex
% Load different packages based on options
\if@someOption
    \RequirePackage{packageA}
\else
    \RequirePackage{packageB}
\fi
```

### Package with Options

```latex
\RequirePackage[option1,option2]{packagename}
```

### Common Packages for Custom Classes

```latex
% Essential packages
\RequirePackage{geometry}      % Page layout
\RequirePackage{fancyhdr}      % Headers/footers
\RequirePackage{titlesec}      % Section formatting
\RequirePackage{xcolor}        % Colors
\RequirePackage{graphicx}      % Images
\RequirePackage{hyperref}      % Links

% Typography
\RequirePackage{fontspec}      % For XeLaTeX/LuaLaTeX
\RequirePackage{microtype}     % Typography improvements

% Math (if needed)
\RequirePackage{amsmath}
\RequirePackage{amssymb}

% Bibliography (if needed)
\RequirePackage[backend=biber]{biblatex}
```

---

## Custom Commands in Classes

Define commands that will be available in documents using your class.

### Document Metadata Commands

```latex
% In your .cls file

% Define storage commands
\newcommand{\@subtitle}{}
\newcommand{\@institution}{}
\newcommand{\@department}{}
\newcommand{\@supervisor}{}

% Define user commands
\newcommand{\subtitle}[1]{\renewcommand{\@subtitle}{#1}}
\newcommand{\institution}[1]{\renewcommand{\@institution}{#1}}
\newcommand{\department}[1]{\renewcommand{\@department}{#1}}
\newcommand{\supervisor}[1]{\renewcommand{\@supervisor}{#1}}
```

Usage in document:
```latex
\documentclass{myclass}

\title{My Thesis}
\subtitle{A Comprehensive Study}
\author{Jane Smith}
\institution{University of Example}
\department{Department of Computer Science}
\supervisor{Prof. John Doe}
```

### Formatting Commands

```latex
% In your .cls file

% Custom emphasis
\newcommand{\important}[1]{\textbf{\textcolor{red}{#1}}}

% Custom note boxes
\newcommand{\notebox}[1]{%
    \begin{center}
    \fcolorbox{black}{yellow!20}{%
        \parbox{0.9\textwidth}{%
            \textbf{Note:} #1
        }%
    }%
    \end{center}
}

% Chapter quotes (for book classes)
\newcommand{\chapterquote}[2]{%
    \begin{flushright}
        \textit{``#1''}\\
        --- #2
    \end{flushright}
}
```

---

## Page Layout and Formatting

### Custom Title Page

```latex
% In your .cls file

\renewcommand{\maketitle}{%
    \begin{titlepage}
        \centering
        \vspace*{2cm}
        
        % University logo (if provided)
        \ifx\@logo\undefined\else
            \includegraphics[width=0.3\textwidth]{\@logo}\\[1cm]
        \fi
        
        % Institution
        {\Large\@institution\par}
        \vspace{0.5cm}
        {\large\@department\par}
        \vspace{2cm}
        
        % Title
        {\Huge\bfseries\@title\par}
        \vspace{0.5cm}
        
        % Subtitle (if provided)
        \ifx\@subtitle\empty\else
            {\Large\@subtitle\par}
        \fi
        \vspace{2cm}
        
        % Author
        {\large\textbf{Author:} \@author\par}
        \vspace{0.5cm}
        
        % Supervisor (if provided)
        \ifx\@supervisor\empty\else
            {\large\textbf{Supervisor:} \@supervisor\par}
        \fi
        
        \vfill
        
        % Date
        {\large\@date\par}
    \end{titlepage}
}

% Logo command
\newcommand{\@logo}{}
\newcommand{\logo}[1]{\renewcommand{\@logo}{#1}}
```

### Section Formatting

```latex
% In your .cls file
\RequirePackage{titlesec}

% Format sections
\titleformat{\section}
    {\Large\bfseries\color{blue}}  % Format
    {\thesection}                   % Label
    {1em}                           % Sep
    {}                              % Before
    [\titlerule]                    % After

% Format subsections
\titleformat{\subsection}
    {\large\bfseries}
    {\thesubsection}
    {1em}
    {}

% Spacing
\titlespacing*{\section}{0pt}{3.5ex plus 1ex minus .2ex}{2.3ex plus .2ex}
```

### Headers and Footers

```latex
% In your .cls file
\RequirePackage{fancyhdr}

\pagestyle{fancy}
\fancyhf{}  % Clear all

% Header
\fancyhead[LE,RO]{\thepage}           % Page number
\fancyhead[LO]{\nouppercase{\rightmark}}  % Section
\fancyhead[RE]{\nouppercase{\leftmark}}   % Chapter

% Footer
\fancyfoot[C]{\@title}

% Line width
\renewcommand{\headrulewidth}{0.4pt}
\renewcommand{\footrulewidth}{0.4pt}

% Plain style (for chapter pages)
\fancypagestyle{plain}{%
    \fancyhf{}
    \fancyfoot[C]{\thepage}
    \renewcommand{\headrulewidth}{0pt}
}
```

---

## Complete Class Examples

### Example 1: Academic Paper Class

```latex
% academicpaper.cls
\NeedsTeXFormat{LaTeX2e}
\ProvidesClass{academicpaper}[2025/10/17 Academic Paper Class]

% Options
\newif\if@doublespacing
\@doublespacingfalse

\DeclareOption{doublespacing}{\@doublespacingtrue}
\DeclareOption*{\PassOptionsToClass{\CurrentOption}{article}}
\ProcessOptions\relax

% Base class
\LoadClass[12pt,a4paper]{article}

% Required packages
\RequirePackage[margin=1in]{geometry}
\RequirePackage{setspace}
\RequirePackage{titlesec}
\RequirePackage{abstract}
\RequirePackage{fancyhdr}
\RequirePackage[backend=biber,style=apa]{biblatex}

% Spacing
\if@doublespacing
    \doublespacing
\else
    \onehalfspacing
\fi

% Abstract formatting
\renewcommand{\abstractnamefont}{\normalfont\bfseries\large}
\renewcommand{\abstracttextfont}{\normalfont\small}

% Section formatting
\titleformat{\section}
    {\normalfont\Large\bfseries}
    {\thesection}{1em}{}

\titleformat{\subsection}
    {\normalfont\large\bfseries}
    {\thesubsection}{1em}{}

% Header/Footer
\pagestyle{fancy}
\fancyhf{}
\fancyhead[R]{\thepage}
\renewcommand{\headrulewidth}{0pt}

% Custom commands
\newcommand{\@keywords}{}
\newcommand{\keywords}[1]{\renewcommand{\@keywords}{#1}}

% Enhanced title
\renewcommand{\maketitle}{%
    \begin{center}
        {\LARGE\bfseries\@title\par}
        \vspace{1em}
        {\large\@author\par}
        \vspace{0.5em}
        {\normalsize\@date\par}
    \end{center}
    \vspace{2em}
}

% Keywords
\newcommand{\printkeywords}{%
    \ifx\@keywords\empty\else
        \noindent\textbf{Keywords:} \@keywords
        \vspace{1em}
    \fi
}
```

Usage:
```latex
\documentclass[doublespacing]{academicpaper}
\addbibresource{references.bib}

\title{The Impact of Custom Classes}
\author{Jane Researcher}
\date{\today}
\keywords{LaTeX, Document Classes, Typography}

\begin{document}
\maketitle

\begin{abstract}
This paper explores custom LaTeX classes...
\end{abstract}

\printkeywords

\section{Introduction}
Content here...

\printbibliography
\end{document}
```

### Example 2: Company Letter Class

```latex
% companyetter.cls
\NeedsTeXFormat{LaTeX2e}
\ProvidesClass{companyletter}[2025/10/17 Company Letter Class]

% Base class
\LoadClass[11pt]{letter}

% Required packages
\RequirePackage[margin=1in,top=2in]{geometry}
\RequirePackage{graphicx}
\RequirePackage{xcolor}
\RequirePackage{tikz}

% Company colors
\definecolor{companyblue}{RGB}{0,51,102}
\definecolor{companygray}{RGB}{128,128,128}

% Company information
\newcommand{\@companyname}{Company Name}
\newcommand{\@companyaddress}{}
\newcommand{\@companyphone}{}
\newcommand{\@companyemail}{}
\newcommand{\@companylogo}{}

% Setter commands
\newcommand{\companyname}[1]{\renewcommand{\@companyname}{#1}}
\newcommand{\companyaddress}[1]{\renewcommand{\@companyaddress}{#1}}
\newcommand{\companyphone}[1]{\renewcommand{\@companyphone}{#1}}
\newcommand{\companyemail}[1]{\renewcommand{\@companyemail}{#1}}
\newcommand{\companylogo}[1]{\renewcommand{\@companylogo}{#1}}

% Custom letterhead
\renewcommand{\ps@firstpage}{%
    \setlength{\headheight}{1.5in}
    \setlength{\headsep}{0.5in}
    \renewcommand{\@oddhead}{%
        \begin{minipage}{\textwidth}
            \begin{tikzpicture}[remember picture,overlay]
                % Logo
                \ifx\@companylogo\empty\else
                    \node[anchor=north west] at (0,0) {%
                        \includegraphics[height=1in]{\@companylogo}
                    };
                \fi
                
                % Company info
                \node[anchor=north east,align=right] at (\textwidth,0) {%
                    \color{companyblue}\Large\bfseries\@companyname\\[0.2cm]
                    \color{companygray}\small
                    \@companyaddress\\
                    Phone: \@companyphone\\
                    Email: \@companyemail
                };
                
                % Line
                \draw[companyblue,line width=2pt] 
                    (0,-1.3in) -- (\textwidth,-1.3in);
            \end{tikzpicture}
        \end{minipage}
    }
}

% Signature
\newcommand{\@signaturename}{}
\newcommand{\@signaturetitle}{}
\newcommand{\signaturename}[1]{\renewcommand{\@signaturename}{#1}}
\newcommand{\signaturetitle}[1]{\renewcommand{\@signaturetitle}{#1}}

\renewcommand{\closing}[1]{%
    \par\noindent
    #1\\[2cm]
    \@signaturename\\
    \textit{\@signaturetitle}
}
```

Usage:
```latex
\documentclass{companyletter}

\companyname{Acme Corporation}
\companyaddress{123 Business St., City, State 12345}
\companyphone{(555) 123-4567}
\companyemail{info@acme.com}
\companylogo{logo.png}

\signaturename{John Smith}
\signaturetitle{CEO}

\begin{document}
\begin{letter}{%
    Mr. Client\\
    456 Customer Ave.\\
    Town, State 67890
}

\opening{Dear Mr. Client,}

This is a professional business letter using our custom class...

\closing{Sincerely,}

\end{letter}
\end{document}
```

---

## Creating Document Templates

Templates are pre-configured `.tex` files ready to use.

### Simple Template Structure

```latex
% template.tex
\documentclass{article}  % or your custom class

% Packages
\usepackage{geometry}
\usepackage{graphicx}
\usepackage{hyperref}

% Configuration
\geometry{margin=1in}

% Metadata (user fills this in)
\title{Document Title Here}
\author{Your Name}
\date{\today}

\begin{document}

\maketitle

\begin{abstract}
Write your abstract here...
\end{abstract}

\section{Introduction}
Write your introduction here...

\section{Methods}
Describe your methods...

\section{Results}
Present your results...

\section{Conclusion}
Conclude your document...

\bibliographystyle{plain}
\bibliography{references}

\end{document}
```

### Template with Instructions

```latex
% thesis-template.tex
\documentclass{thesis}  % Custom thesis class

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% INSTRUCTIONS FOR USE
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% 1. Fill in your information below
% 2. Delete sections you don't need
% 3. Compile with: pdflatex -> biber -> pdflatex -> pdflatex
% 4. Remove these instructions before final submission
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

% Document information
\title{Your Thesis Title}
\subtitle{Optional Subtitle}
\author{Your Name}
\institution{Your University}
\department{Your Department}
\supervisor{Your Supervisor's Name}
\date{\today}

% Optional: Add logo
% \logo{university-logo.png}

\begin{document}

% Front matter
\maketitle
\tableofcontents
\listoffigures  % Optional
\listoftables   % Optional

% Main content
\chapter{Introduction}
% TODO: Write introduction

\chapter{Literature Review}
% TODO: Review literature

\chapter{Methodology}
% TODO: Describe methods

\chapter{Results}
% TODO: Present results

\chapter{Discussion}
% TODO: Discuss findings

\chapter{Conclusion}
% TODO: Conclude thesis

% Back matter
\appendix
\chapter{Additional Data}
% TODO: Add appendices if needed

\printbibliography

\end{document}
```

### Template Distribution

Create a template package with:

```
thesis-template/
├── template.tex          # Main template
├── mythesis.cls         # Custom class
├── references.bib       # Example bibliography
├── figures/             # Folder for images
│   └── example.png
├── chapters/            # Folder for chapter files
│   ├── chapter1.tex
│   └── chapter2.tex
├── README.md           # Instructions
└── Makefile            # Build automation
```

---

## Best Practices

### 1. Clear Documentation

```latex
% At the top of your .cls file
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% My Custom Class
% Version 1.0 (2025/10/17)
%
% Description:
%   This class provides formatting for technical reports
%   with custom title pages and section formatting.
%
% Usage:
%   \documentclass[options]{myclass}
%
% Options:
%   twocolumn - Use two-column layout
%   draft     - Enable draft mode with watermark
%
% Author: Your Name
% License: MIT
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
```

### 2. Namespace Your Commands

```latex
% Prefix commands with your class name to avoid conflicts
\newcommand{\myclass@internalcommand}{...}
\newcommand{\myclassTitle}[1]{...}
```

### 3. Provide Defaults

```latex
% Always provide sensible defaults
\newcommand{\@subtitle}{}      % Empty by default
\newcommand{\@institution}{University Name}  % Default value
```

### 4. Error Handling

```latex
% Check for required information
\AtBeginDocument{%
    \ifx\@author\empty
        \ClassError{myclass}{Author not specified}{%
            Please use \protect\author{} to specify the author.
        }
    \fi
}
```

### 5. Backwards Compatibility

```latex
% Deprecate commands gracefully
\newcommand{\oldcommand}{%
    \ClassWarning{myclass}{%
        \protect\oldcommand\space is deprecated.
        Use \protect\newcommand\space instead
    }%
    \newcommand
}
```

### 6. Testing

Create test documents:

```latex
% test-myclass.tex
\documentclass[alloptions]{myclass}

\title{Test Document}
\author{Test Author}

\begin{document}
\maketitle
Test all features...
\end{document}
```

### 7. Version Control

```latex
\ProvidesClass{myclass}[2025/10/17 v1.0 My Custom Class]
% Update version number and date with each release
```

---

## Distribution and Sharing

### Local Installation

1. **Per-project** (easiest):
   - Place `.cls` file in same directory as `.tex` file

2. **User texmf tree**:
   ```bash
   # Linux/macOS
   ~/texmf/tex/latex/myclass/myclass.cls
   
   # Windows
   C:\Users\YourName\texmf\tex\latex\myclass\myclass.cls
   ```

3. **System-wide**:
   ```bash
   # Find your texmf directory
   kpsewhich -var-value TEXMFHOME
   
   # Place class there and run:
   texhash
   ```

### Packaging for Distribution

Create a complete package:

```
myclass/
├── myclass.cls          # The class file
├── myclass.pdf          # Documentation
├── myclass-example.tex  # Example usage
├── myclass-example.pdf  # Compiled example
├── README.md            # Quick start guide
└── LICENSE              # License information
```

### Documentation Template

```latex
% myclass.tex (documentation source)
\documentclass{ltxdoc}  % LaTeX documentation class

\title{The \textsf{myclass} Class}
\author{Your Name}
\date{Version 1.0, \today}

\begin{document}
\maketitle

\begin{abstract}
Description of your class...
\end{abstract}

\section{Introduction}
What it does...

\section{Installation}
How to install...

\section{Usage}
\begin{verbatim}
\documentclass{myclass}
...
\end{verbatim}

\section{Options}
Available options...

\section{Commands}
\DescribeMacro{\mycommand}
Description of command...

\section{Examples}
Code examples...

\end{document}
```

### Sharing on CTAN

For wide distribution, consider submitting to [CTAN](https://ctan.org/):
1. Package your class properly
2. Include comprehensive documentation
3. Choose an appropriate license (LPPL recommended)
4. Submit via CTAN upload page

---

## Summary

**Key Takeaways**:

1. **Classes** define document structure; **templates** provide starting points
2. Use `\LoadClass` to build on existing classes
3. `\RequirePackage` loads packages in class files
4. Provide options with `\DeclareOption`
5. Define custom commands for document metadata
6. Document your class thoroughly
7. Test extensively before distribution

**Class File Checklist**:
- [ ] Identification (`\NeedsTeXFormat`, `\ProvidesClass`)
- [ ] Options declared and processed
- [ ] Base class loaded
- [ ] Required packages loaded
- [ ] Custom commands defined
- [ ] Page layout configured
- [ ] Documentation written
- [ ] Examples provided
- [ ] Tested with various content

**Next Steps**:
- Create a simple class for your needs
- Study existing classes (article.cls, book.cls)
- Explore advanced packages (xparse, etoolbox)
- Consider creating a package instead if appropriate

---

## Additional Resources

- **LaTeX2e for Class and Package Writers**: Official guide
- **CTAN**: https://ctan.org/ - Browse existing classes
- **clsguide.pdf**: Comprehensive class writing guide (included with LaTeX)
- **The LaTeX Companion**: Book with detailed class/package information
- **TeX Stack Exchange**: https://tex.stackexchange.com/questions/tagged/document-classes

---

**Last Updated**: October 2025
