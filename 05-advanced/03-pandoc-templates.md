# Pandoc Templates: Creating Custom Document Conversions

## Introduction

Pandoc templates allow you to control how Pandoc converts documents from one format to another. Templates are especially powerful for creating customized LaTeX/PDF outputs, HTML documents, and other formats with consistent styling and structure.

## Table of Contents

- [What are Pandoc Templates?](#what-are-pandoc-templates)
- [When to Use Pandoc Templates](#when-to-use-pandoc-templates)
- [Template Basics](#template-basics)
- [Creating a Simple LaTeX Template](#creating-a-simple-latex-template)
- [Template Variables](#template-variables)
- [Conditional Content](#conditional-content)
- [Loops and Iteration](#loops-and-iteration)
- [Using Templates](#using-templates)
- [Complete Working Examples](#complete-working-examples)
- [RMarkdown Templates](#rmarkdown-templates)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)

---

## What are Pandoc Templates?

**Pandoc templates** are text files with special syntax that control how Pandoc formats output documents. They act as blueprints that wrap your content with appropriate formatting, headers, and structure.

### How Templates Work

```
Markdown → Pandoc → Template → Output (PDF, HTML, DOCX, etc.)
```

1. You write content in Markdown (or another input format)
2. Pandoc processes the content
3. Template defines the output structure
4. Final document is generated

### Template vs Custom Class

| Feature | Pandoc Template | LaTeX Class |
|---------|----------------|-------------|
| Purpose | Control Pandoc output | Define LaTeX document type |
| File type | `.tex`, `.html`, etc. | `.cls` |
| Usage | `pandoc --template=...` | `\documentclass{...}` |
| Flexibility | Works across formats | LaTeX-specific |
| Best for | Content conversion | Pure LaTeX documents |

### Pandoc Template vs Pure LaTeX Template

Understanding the differences is crucial for choosing the right tool:

| Aspect | Pandoc Template | Pure LaTeX Template |
|--------|----------------|---------------------|
| **Syntax** | Pandoc's `$variable$` syntax | Pure LaTeX commands |
| **Variables** | `$title$`, `$author$`, etc. | `\def\mytitle{...}` or `\newcommand` |
| **Conditionals** | `$if(var)$...$endif$` | `\ifthenelse{}{}{}` or custom macros |
| **Loops** | `$for(items)$...$endfor$` | LaTeX `\foreach` or custom loops |
| **Content** | `$body$` placeholder | Direct LaTeX content |
| **Input format** | Markdown, reST, docx, etc. | Only `.tex` files |
| **Processing** | Pandoc converts → template applies | LaTeX compiles directly |
| **Portability** | Multiple output formats | PDF only |

#### Syntax Comparison Example

**Pandoc Template** (`pandoc-article.tex`):
```latex
\documentclass{article}

% Pandoc variables with defaults
\title{$title$}
\author{$if(author)$$author$$else$Anonymous$endif$}
\date{$date$}

\begin{document}

$if(title)$
\maketitle
$endif$

$if(abstract)$
\begin{abstract}
$abstract$
\end{abstract}
$endif$

% Pandoc inserts converted content here
$body$

\end{document}
```

**Pure LaTeX Template** (`latex-article.tex`):
```latex
\documentclass{article}

% LaTeX commands for variables
\newcommand{\mytitle}{Default Title}
\newcommand{\myauthor}{Anonymous}
\newcommand{\mydate}{\today}

% User must redefine these in their document
\title{\mytitle}
\author{\myauthor}
\date{\mydate}

\begin{document}

\maketitle

\begin{abstract}
Abstract text goes here directly in LaTeX
\end{abstract}

% User writes LaTeX content directly
\section{Introduction}
Content written in pure LaTeX...

\end{document}
```

**Usage Comparison**:

```bash
# Pandoc template - write content in Markdown
echo "---
title: My Paper
author: Jane Smith
abstract: This is my paper
---
# Introduction
Content in *Markdown*
" | pandoc -o output.pdf --template=pandoc-article.tex

# Pure LaTeX - write content in LaTeX
cat > document.tex << 'EOF'
\input{latex-article.tex}
\renewcommand{\mytitle}{My Paper}
\renewcommand{\myauthor}{Jane Smith}
\section{Introduction}
Content in \textit{LaTeX}
\end{document}
EOF
pdflatex document.tex
```

#### When to Use Each

**Use Pandoc Templates when**:
- Writing content in Markdown or other lightweight formats
- Need multiple output formats (PDF, HTML, DOCX)
- Want to separate content from presentation
- Collaborating with non-LaTeX users
- Automating document generation from data

**Use Pure LaTeX Templates when**:
- Complex mathematical typesetting
- Need full LaTeX control and features
- Working entirely in LaTeX ecosystem
- Creating specialized document classes
- Performance-critical compilation (LaTeX is faster)

#### Hybrid Approach

You can combine both:

```latex
% hybrid-template.tex - Pandoc template using custom LaTeX class
\documentclass{myarticle}  % Your custom .cls file

% Pandoc variables feed into LaTeX class
\title{$title$}
\author{$author$}
\customfield{$if(customfield)$$customfield$$endif$}

\begin{document}
$body$
\end{document}
```

This gives you:
- Markdown input convenience (Pandoc)
- Custom formatting power (LaTeX class)
- Best of both worlds!

---

## When to Use Pandoc Templates

Use Pandoc templates when you:

1. **Convert Markdown to PDF** with custom styling
2. **Generate reports** from plain text with consistent formatting
3. **Create HTML documents** with specific layouts
4. **Batch process** multiple documents with same format
5. **Separate content from presentation** (write in Markdown, format via template)
6. **Integrate with automation** (CI/CD, static site generators)

### Common Use Cases

- Academic papers from Markdown
- Technical documentation
- Reports and presentations
- CV/Resume generation
- Book manuscripts
- Slide decks (beamer)
- Corporate documents with branding

---

## Template Basics

### Template Syntax

Pandoc uses a simple templating language with these key elements:

#### 1. Variables

```
$variable$
```

Insert the value of a variable.

#### 2. Conditional Blocks

```
$if(variable)$
  Content shown if variable exists
$endif$
```

#### 3. For Loops

```
$for(items)$
  Process each item: $items$
$endfor$
```

#### 4. Partial Templates

```
$partial(filename.tex)$
```

Include another template file.

### Finding Default Templates

View Pandoc's default template for any format:

```bash
# LaTeX template
pandoc -D latex > default.tex

# HTML template
pandoc -D html > default.html

# Beamer (slides) template
pandoc -D beamer > default.beamer

# Markdown template
pandoc -D markdown > default.md
```

**Tip**: Start by modifying a default template rather than creating from scratch.

---

## Creating a Simple LaTeX Template

Let's create a basic template for academic papers.

### Step 1: Create `simple-paper.tex`

```latex
% simple-paper.tex - Pandoc Template for Academic Papers
\documentclass[$if(fontsize)$$fontsize$$else$12pt$endif$]{article}

% Packages
\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}
\usepackage{geometry}
\usepackage{graphicx}
\usepackage{hyperref}
\usepackage{xcolor}

% Page layout
\geometry{
    margin=$if(margin)$$margin$$else$1in$endif$
}

% Hyperlink colors
\hypersetup{
    colorlinks=true,
    linkcolor=$if(linkcolor)$$linkcolor$$else$blue$endif$,
    urlcolor=$if(urlcolor)$$urlcolor$$else$blue$endif$,
    citecolor=$if(citecolor)$$citecolor$$else$blue$endif$
}

% Document metadata
$if(title)$
\title{$title$}
$endif$

$if(author)$
\author{$for(author)$$author$$sep$ \and $endfor$}
$endif$

$if(date)$
\date{$date$}
$else$
\date{\today}
$endif$

\begin{document}

$if(title)$
\maketitle
$endif$

$if(abstract)$
\begin{abstract}
$abstract$
\end{abstract}
$endif$

$if(toc)$
\tableofcontents
\newpage
$endif$

% Main content
$body$

\end{document}
```

### Step 2: Create Markdown Document

```markdown
---
title: "My Research Paper"
author:
  - Jane Smith
  - John Doe
date: "October 17, 2025"
abstract: |
  This paper explores custom Pandoc templates for academic writing.
  We demonstrate how templates simplify document generation.
toc: true
fontsize: 11pt
margin: 1in
linkcolor: darkblue
---

# Introduction

This is the introduction to my paper.

# Methods

Here we describe our methods...

# Results

Our findings are presented here.

# Conclusion

We conclude that Pandoc templates are powerful!
```

### Step 3: Compile

```bash
pandoc paper.md -o paper.pdf --template=simple-paper.tex
```

---

## Template Variables

### Metadata Variables

Set in YAML front matter:

```yaml
---
title: "Document Title"
author: "Author Name"
date: "2025-10-17"
lang: en-US
fontsize: 12pt
---
```

Access in template:

```latex
\title{$title$}
\author{$author$}
\date{$date$}
```

### Common Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `$title$` | Document title | "My Paper" |
| `$author$` | Author(s) | "Jane Smith" |
| `$date$` | Date | "2025-10-17" |
| `$abstract$` | Abstract text | "This paper..." |
| `$toc$` | Include TOC | true/false |
| `$body$` | Main content | (Converted Markdown) |
| `$lang$` | Language | en-US, fr-FR |
| `$fontsize$` | Font size | 10pt, 11pt, 12pt |

### Custom Variables

Define your own:

```yaml
---
institution: "MIT"
department: "Computer Science"
supervisor: "Prof. Smith"
logo: "university-logo.png"
---
```

Use in template:

```latex
$if(institution)$
\textbf{Institution:} $institution$\\
$endif$

$if(logo)$
\includegraphics[width=2cm]{$logo$}
$endif$
```

---

## Conditional Content

### Basic If Statement

```latex
$if(variable)$
  Content shown if variable is defined
$endif$
```

### If-Else

```latex
$if(abstract)$
\begin{abstract}
$abstract$
\end{abstract}
$else$
% No abstract provided
$endif$
```

### Multiple Conditions

```latex
$if(titlepage)$
  \maketitle
  \newpage
$else$
  $if(title)$
    {\Large\bfseries $title$\par}
    \vspace{1em}
  $endif$
$endif$
```

### Checking for Empty

```latex
$if(keywords)$
\textbf{Keywords:} $for(keywords)$$keywords$$sep$, $endfor$
$endif$
```

---

## Loops and Iteration

### For Loop Basics

```latex
$for(variable)$
  Process $variable$
$endfor$
```

### Author List Example

Markdown:
```yaml
---
author:
  - Jane Smith
  - John Doe
  - Alice Johnson
---
```

Template:
```latex
\author{
$for(author)$
  $author$$sep$ \and
$endfor$
}
```

Output:
```latex
\author{
  Jane Smith \and
  John Doe \and
  Alice Johnson
}
```

### Complex Iteration

```yaml
---
affiliations:
  - name: "MIT"
    department: "CS"
  - name: "Stanford"
    department: "EE"
---
```

Template:
```latex
\begin{itemize}
$for(affiliations)$
  \item $affiliations.name$ -- $affiliations.department$
$endfor$
\end{itemize}
```

### Bibliography Example

```latex
$if(bibliography)$
\bibliographystyle{$if(biblio-style)$$biblio-style$$else$plain$endif$}
\bibliography{$for(bibliography)$$bibliography$$sep$,$endfor$}
$endif$
```

---

## Using Templates

### Basic Usage

```bash
pandoc input.md -o output.pdf --template=mytemplate.tex
```

### With Variables from Command Line

```bash
pandoc input.md -o output.pdf \
  --template=mytemplate.tex \
  -V author="Jane Smith" \
  -V date="2025-10-17" \
  -V fontsize=11pt
```

### Template Search Path

Pandoc looks for templates in:

1. Current directory
2. `~/.pandoc/templates/` (user templates)
3. System templates directory

Install template globally:

```bash
# Create directory if needed
mkdir -p ~/.pandoc/templates/

# Copy template
cp mytemplate.tex ~/.pandoc/templates/

# Use by name only
pandoc input.md -o output.pdf --template=mytemplate
```

### Multiple Templates

```bash
# Use different templates for different outputs
pandoc input.md -o paper.pdf --template=academic.tex
pandoc input.md -o report.pdf --template=corporate.tex
pandoc input.md -o slides.pdf --template=beamer.tex
```

---

## Complete Working Examples

### Example 1: Academic Thesis Template

#### Template: `thesis.tex`

```latex
% thesis.tex - Pandoc Template for Thesis
\documentclass[12pt,a4paper,oneside]{book}

% Packages
\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}
\usepackage[margin=1in]{geometry}
\usepackage{graphicx}
\usepackage{fancyhdr}
\usepackage{titlesec}
\usepackage{hyperref}
\usepackage{setspace}

% Spacing
$if(doublespacing)$
\doublespacing
$else$
\onehalfspacing
$endif$

% Header/Footer
\pagestyle{fancy}
\fancyhf{}
\fancyhead[R]{\thepage}
\fancyhead[L]{\nouppercase{\leftmark}}
\renewcommand{\headrulewidth}{0.4pt}

% Hyperlinks
\hypersetup{
    colorlinks=true,
    linkcolor=blue,
    urlcolor=blue,
    citecolor=blue
}

% Title page commands
\newcommand{\thesistitle}{$title$}
\newcommand{\thesissubtitle}{$if(subtitle)$$subtitle$$endif$}
\newcommand{\thesisauthor}{$author$}
\newcommand{\thesisinstitution}{$if(institution)$$institution$$else$University Name$endif$}
\newcommand{\thesisdepartment}{$if(department)$$department$$else$Department Name$endif$}
\newcommand{\thesissupervisor}{$if(supervisor)$$supervisor$$endif$}
\newcommand{\thesisdate}{$date$}

\begin{document}

% Title page
\begin{titlepage}
    \centering
    \vspace*{2cm}
    
    $if(logo)$
    \includegraphics[width=0.3\textwidth]{$logo$}\\[1cm]
    $endif$
    
    {\Large\thesisinstitution\par}
    \vspace{0.5cm}
    {\large\thesisdepartment\par}
    \vspace{2cm}
    
    {\Huge\bfseries\thesistitle\par}
    $if(subtitle)$
    \vspace{0.5cm}
    {\Large\thesissubtitle\par}
    $endif$
    \vspace{2cm}
    
    {\large\textbf{Author:} \thesisauthor\par}
    \vspace{0.5cm}
    
    $if(supervisor)$
    {\large\textbf{Supervisor:} \thesissupervisor\par}
    $endif$
    
    \vfill
    
    {\large\thesisdate\par}
\end{titlepage}

% Front matter
\frontmatter

$if(abstract)$
\chapter*{Abstract}
\addcontentsline{toc}{chapter}{Abstract}
$abstract$
$endif$

$if(acknowledgments)$
\chapter*{Acknowledgments}
\addcontentsline{toc}{chapter}{Acknowledgments}
$acknowledgments$
$endif$

\tableofcontents

$if(lof)$
\listoffigures
$endif$

$if(lot)$
\listoftables
$endif$

% Main matter
\mainmatter

$body$

% Back matter
\backmatter

$if(bibliography)$
\bibliographystyle{$if(biblio-style)$$biblio-style$$else$plain$endif$}
\bibliography{$for(bibliography)$$bibliography$$sep$,$endfor$}
$endif$

$if(appendix)$
\appendix
$for(appendix)$
\chapter{$appendix.title$}
$appendix.content$
$endfor$
$endif$

\end{document}
```

#### Markdown: `thesis.md`

```markdown
---
title: "Machine Learning Applications in Bioinformatics"
subtitle: "A Comprehensive Study"
author: "Jane Smith"
institution: "Massachusetts Institute of Technology"
department: "Department of Computer Science"
supervisor: "Prof. John Doe"
date: "October 2025"
logo: "mit-logo.png"
abstract: |
  This thesis explores the application of machine learning techniques
  to biological sequence analysis. We present novel algorithms for
  protein structure prediction and demonstrate their effectiveness
  on benchmark datasets.
acknowledgments: |
  I would like to thank my supervisor, Prof. John Doe, for his
  guidance and support throughout this research.
doublespacing: false
lof: true
lot: true
bibliography:
  - references.bib
biblio-style: "IEEEtran"
---

# Introduction

This chapter introduces the research problem...

## Background

Machine learning has revolutionized bioinformatics...

## Research Questions

1. How can deep learning improve protein prediction?
2. What are the computational constraints?

# Literature Review

Previous work in this area includes...

# Methodology

We developed a novel approach using...

## Data Collection

Data was obtained from...

## Model Architecture

Our model consists of...

# Results

We achieved the following results...

# Discussion

These findings suggest that...

# Conclusion

In conclusion, we have demonstrated...
```

#### Compile

```bash
pandoc thesis.md -o thesis.pdf \
  --template=thesis.tex \
  --pdf-engine=xelatex \
  --number-sections
```

---

### Example 2: Technical Report Template

#### Template: `techreport.tex`

```latex
% techreport.tex - Pandoc Template for Technical Reports
\documentclass[11pt]{article}

% Packages
\usepackage[utf8]{inputenc}
\usepackage[margin=1in]{geometry}
\usepackage{graphicx}
\usepackage{fancyhdr}
\usepackage{xcolor}
\usepackage{listings}
\usepackage{hyperref}

% Colors
\definecolor{codebackground}{RGB}{248,248,248}
\definecolor{codecomment}{RGB}{0,128,0}
\definecolor{codekeyword}{RGB}{0,0,255}

% Code listings
\lstset{
    backgroundcolor=\color{codebackground},
    basicstyle=\ttfamily\small,
    commentstyle=\color{codecomment},
    keywordstyle=\color{codekeyword},
    numbers=left,
    numberstyle=\tiny,
    frame=single,
    breaklines=true,
    showstringspaces=false
}

% Header/Footer
\pagestyle{fancy}
\fancyhf{}
\fancyhead[L]{$if(project)$$project$$endif$}
\fancyhead[R]{$if(reportnumber)$Report \#$reportnumber$$endif$}
\fancyfoot[C]{\thepage}
\renewcommand{\headrulewidth}{0.4pt}

% Title formatting
\makeatletter
\renewcommand{\maketitle}{
    \begin{titlepage}
        \centering
        $if(company-logo)$
        \includegraphics[width=0.4\textwidth]{$company-logo$}\\[1cm]
        $endif$
        
        $if(company)$
        {\Large\textbf{$company$}\par}
        \vspace{0.5cm}
        $endif$
        
        $if(department)$
        {\large $department$\par}
        \vspace{2cm}
        $endif$
        
        {\Huge\bfseries $title$\par}
        \vspace{1cm}
        
        $if(reportnumber)$
        {\large Report Number: $reportnumber$\par}
        \vspace{0.5cm}
        $endif$
        
        $if(version)$
        {\large Version: $version$\par}
        \vspace{2cm}
        $endif$
        
        {\large
        $if(author)$
        \textbf{Prepared by:}\\
        $for(author)$
        $author$\\
        $endfor$
        \vspace{1cm}
        $endif$
        
        $if(reviewer)$
        \textbf{Reviewed by:} $reviewer$\\
        \vspace{1cm}
        $endif$
        
        $if(date)$
        \textbf{Date:} $date$
        $else$
        \textbf{Date:} \today
        $endif$
        }
        
        \vfill
        
        $if(confidential)$
        {\color{red}\large\textbf{CONFIDENTIAL}}
        $endif$
    \end{titlepage}
}
\makeatother

\begin{document}

\maketitle

$if(revisionhistory)$
\section*{Revision History}
\begin{tabular}{|l|l|l|p{6cm}|}
\hline
\textbf{Version} & \textbf{Date} & \textbf{Author} & \textbf{Changes} \\
\hline
$for(revisionhistory)$
$revisionhistory.version$ & $revisionhistory.date$ & $revisionhistory.author$ & $revisionhistory.changes$ \\
\hline
$endfor$
\end{tabular}
\newpage
$endif$

$if(executive-summary)$
\section*{Executive Summary}
$executive-summary$
\newpage
$endif$

$if(toc)$
\tableofcontents
\newpage
$endif$

$body$

$if(appendix)$
\appendix
$for(appendix)$
\section{$appendix.title$}
$appendix.content$
$endfor$
$endif$

\end{document}
```

#### Markdown: `report.md`

```markdown
---
title: "System Performance Analysis"
project: "Project Phoenix"
reportnumber: "TR-2025-042"
version: "1.2"
company: "Acme Corporation"
department: "Engineering Division"
company-logo: "acme-logo.png"
author:
  - "Jane Smith (Lead Engineer)"
  - "John Doe (Data Analyst)"
reviewer: "Dr. Alice Johnson"
date: "October 17, 2025"
confidential: true
toc: true
revisionhistory:
  - version: "1.0"
    date: "2025-09-01"
    author: "Jane Smith"
    changes: "Initial draft"
  - version: "1.1"
    date: "2025-10-01"
    author: "John Doe"
    changes: "Added performance metrics"
  - version: "1.2"
    date: "2025-10-17"
    author: "Jane Smith"
    changes: "Final review and updates"
executive-summary: |
  This report analyzes the performance of our new system architecture.
  Key findings show a 40% improvement in throughput and 25% reduction
  in latency compared to the previous system.
---

# Introduction

## Background

Our system handles millions of requests daily...

## Objectives

The objectives of this analysis are:

1. Measure current performance
2. Identify bottlenecks
3. Recommend improvements

# Methodology

## Test Environment

Tests were conducted on AWS EC2 instances...

## Performance Metrics

We measured the following metrics:

- Throughput (requests/second)
- Latency (milliseconds)
- Error rate (%)

# Results

## Throughput Analysis

Average throughput: 10,000 requests/second

## Latency Analysis

95th percentile latency: 45ms

# Recommendations

Based on our analysis, we recommend:

1. Upgrade to larger EC2 instances
2. Implement caching layer
3. Optimize database queries

# Conclusion

This analysis demonstrates significant performance gains...
```

#### Compile

```bash
pandoc report.md -o report.pdf \
  --template=techreport.tex \
  --pdf-engine=pdflatex
```

---

### Example 3: Simple CV/Resume Template

#### Template: `cv.tex`

```latex
% cv.tex - Pandoc Template for CV/Resume
\documentclass[11pt,a4paper]{article}

\usepackage[utf8]{inputenc}
\usepackage[margin=0.75in]{geometry}
\usepackage{enumitem}
\usepackage{hyperref}
\usepackage{xcolor}
\usepackage{titlesec}

% No page numbers
\pagestyle{empty}

% Section formatting
\titleformat{\section}
  {\Large\bfseries\color{blue}}
  {}
  {0em}
  {}
  [\titlerule]

\titleformat{\subsection}
  {\large\bfseries}
  {}
  {0em}
  {}

% Compact lists
\setlist{nosep, leftmargin=*}

% Custom commands
\newcommand{\CVitem}[4]{
  \subsection*{#1}
  \textit{#2} \hfill #3\\
  #4
  \vspace{0.5em}
}

\begin{document}

% Header
\begin{center}
  {\Huge\bfseries $name$}\\[0.5em]
  $if(title)$
  {\large $title$}\\[0.5em]
  $endif$
  $if(email)$Email: \href{mailto:$email$}{$email$}$endif$
  $if(phone)$ | Phone: $phone$$endif$
  $if(website)$ | Web: \href{$website$}{$website$}$endif$
  $if(linkedin)$ | LinkedIn: \href{$linkedin$}{Profile}$endif$
  $if(github)$ | GitHub: \href{$github$}{$github$}$endif$
end{center}

\vspace{1em}

$if(summary)$
\section*{Summary}
$summary$
$endif$

$if(education)$
\section*{Education}
$for(education)$
\CVitem{$education.degree$}{$education.institution$}{$education.date$}{$education.details$}
$endfor$
$endif$

$if(experience)$
\section*{Work Experience}
$for(experience)$
\CVitem{$experience.title$}{$experience.company$}{$experience.date$}{
  $experience.description$
  $if(experience.achievements)$
  \begin{itemize}
  $for(experience.achievements)$
    \item $experience.achievements$
  $endfor$
  \end{itemize}
  $endif$
}
$endfor$
$endif$

$if(skills)$
\section*{Skills}
$for(skills)$
\textbf{$skills.category$:} $for(skills.items)$$skills.items$$sep$, $endfor$\\[0.3em]
$endfor$
$endif$

$if(publications)$
\section*{Publications}
\begin{itemize}
$for(publications)$
  \item $publications$
$endfor$
\end{itemize}
$endif$

$if(awards)$
\section*{Awards \& Honors}
\begin{itemize}
$for(awards)$
  \item $awards$
$endfor$
\end{itemize}
$endif$

$body$

\end{document}
```

#### Markdown: `cv.md`

```markdown
---
name: "Jane Smith"
title: "Senior Software Engineer"
email: "jane.smith@email.com"
phone: "+1 (555) 123-4567"
website: "https://janesmith.dev"
linkedin: "https://linkedin.com/in/janesmith"
github: "https://github.com/janesmith"
summary: |
  Experienced software engineer with 8+ years in backend development,
  cloud architecture, and machine learning. Passionate about building
  scalable systems and mentoring junior developers.
education:
  - degree: "M.S. Computer Science"
    institution: "MIT"
    date: "2015-2017"
    details: "Focus: Distributed Systems and Machine Learning"
  - degree: "B.S. Computer Science"
    institution: "Stanford University"
    date: "2011-2015"
    details: "Summa Cum Laude, GPA: 3.9/4.0"
experience:
  - title: "Senior Software Engineer"
    company: "Tech Corp"
    date: "2019-Present"
    description: "Lead backend development for cloud platform"
    achievements:
      - "Designed microservices architecture serving 10M+ users"
      - "Reduced API latency by 60% through optimization"
      - "Mentored 5 junior engineers"
  - title: "Software Engineer"
    company: "Startup Inc"
    date: "2017-2019"
    description: "Full-stack development for SaaS product"
    achievements:
      - "Built real-time analytics dashboard"
      - "Implemented CI/CD pipeline reducing deployment time by 80%"
skills:
  - category: "Languages"
    items:
      - "Python"
      - "Go"
      - "JavaScript"
      - "SQL"
  - category: "Technologies"
    items:
      - "AWS"
      - "Docker"
      - "Kubernetes"
      - "PostgreSQL"
      - "Redis"
  - category: "Frameworks"
    items:
      - "Django"
      - "FastAPI"
      - "React"
      - "TensorFlow"
publications:
  - "Smith, J. et al. (2023). 'Scalable ML Inference', ICML 2023"
  - "Smith, J. & Doe, J. (2021). 'Distributed Systems', ACM SIGMOD"
awards:
  - "Best Paper Award, ICML 2023"
  - "Employee of the Year, Tech Corp, 2022"
---
```

#### Compile

```bash
pandoc cv.md -o cv.pdf --template=cv.tex
```

---

## Best Practices

### 1. Start with Default Template

```bash
# Get default and modify
pandoc -D latex > mytemplate.tex
# Edit mytemplate.tex to customize
```

### 2. Test Incrementally

```bash
# Test with minimal document first
echo "# Test\n\nContent" | pandoc -o test.pdf --template=mytemplate.tex
```

### 3. Use Meaningful Variable Names

```latex
% Good
$if(show-header)$...$endif$
$if(company-logo)$...$endif$

% Bad
$if(sh)$...$endif$
$if(logo1)$...$endif$
```

### 4. Provide Defaults

```latex
% Always provide fallback
$if(fontsize)$$fontsize$$else$12pt$endif$
$if(author)$$author$$else$Anonymous$endif$
```

### 5. Document Your Template

```latex
% At top of template file
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% Template: techreport.tex
% Purpose: Technical report generation from Markdown
% Version: 1.0 (2025-10-17)
%
% Required variables:
%   - title: Report title
%   - author: Author name(s)
%
% Optional variables:
%   - company: Company name
%   - logo: Path to logo image
%   - confidential: Add confidential watermark
%
% Usage:
%   pandoc input.md -o output.pdf --template=techreport.tex
%
% Author: Your Name
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
```

### 6. Validate YAML Front Matter

Use a schema or validator:

```bash
# Install yq for YAML validation
sudo apt install yq

# Validate YAML
yq eval document.md
```

### 7. Create Template Examples

Include example Markdown with every template:

```
templates/
├── thesis.tex
├── thesis-example.md
├── cv.tex
├── cv-example.md
└── README.md
```

---

## Troubleshooting

### Common Issues

#### 1. Template Not Found

**Error**: `pandoc: Could not find template`

**Solution**:
```bash
# Use absolute path
pandoc input.md -o output.pdf --template=/full/path/to/template.tex

# Or install to user directory
mkdir -p ~/.pandoc/templates/
cp template.tex ~/.pandoc/templates/
```

#### 2. Variable Not Substituted

**Problem**: `$variable$` appears in output literally

**Solution**:
- Check variable name spelling in YAML
- Ensure YAML syntax is correct (proper indentation)
- Verify variable is defined

```yaml
# Wrong
author:"Jane Smith"  # Missing space after colon

# Correct
author: "Jane Smith"
```

#### 3. Conditional Not Working

**Problem**: Content shows even when variable undefined

**Solution**:
```latex
% Wrong - checks if string "false" exists (always true)
$if(toc)$...$endif$

% Correct - checks if variable exists and is truthy
$if(toc)$
$toc$
$endif$
```

Set to false in YAML:
```yaml
toc: false  # or omit entirely
```

#### 4. LaTeX Errors in PDF Generation

**Error**: LaTeX compilation fails

**Solution**:
```bash
# Use --verbose for detailed errors
pandoc input.md -o output.pdf --template=mytemplate.tex --verbose

# Test template validity
pandoc -D latex > test.tex
# Compare your template structure to test.tex
```

#### 5. Special Characters in Variables

**Problem**: LaTeX special characters (`&`, `%`, `$`, etc.) break

**Solution**:
```latex
% Use raw block for content with special chars
$if(company)$
\textbf{$company$}  % This works if company="Acme & Co"
$endif$
```

In YAML, escape or quote:
```yaml
company: "Acme & Co"  # Pandoc handles escaping
title: "Cost: $500"   # Quote to preserve literal $
```

#### 6. Loop Not Iterating

**Problem**: Only first item shows

**Solution**:
```latex
% Wrong - missing $endfor$
$for(author)$
$author$

% Correct
$for(author)$
$author$$sep$, 
$endfor$
```

---

## RMarkdown Templates

RMarkdown is a powerful framework for creating dynamic documents that combine R code, analysis, and narrative text. RMarkdown uses Pandoc (and optionally LaTeX) templates under the hood.

### How RMarkdown Uses Templates

**RMarkdown Processing Pipeline**:
```
.Rmd file → knitr (R execution) → .md file → Pandoc + Template → Output
```

1. **knitr** executes R code chunks and generates Markdown
2. **Pandoc** converts Markdown to output format using template
3. **LaTeX** (if PDF output) compiles to final document

### RMarkdown YAML Header

RMarkdown extends YAML front matter with additional options:

```yaml
---
title: "My Analysis Report"
author: "Jane Smith"
date: "`r Sys.Date()`"  # R code in YAML!
output:
  pdf_document:
    template: mytemplate.tex
    toc: true
    number_sections: true
  html_document:
    theme: united
---
```

### Using Custom Pandoc Templates in RMarkdown

#### Method 1: Specify Template in YAML

```yaml
---
title: "Custom Report"
output:
  pdf_document:
    template: "custom-template.tex"
---
```

#### Method 2: Create RMarkdown Template Package

For reusable templates, create an R package structure:

```
mytemplate/
├── inst/
│   └── rmarkdown/
│       └── templates/
│           └── academic_paper/
│               ├── skeleton/
│               │   └── skeleton.Rmd
│               └── template.yaml
└── DESCRIPTION
```

### Complete Working Example: Data Analysis Report

Let's create a complete RMarkdown template for data analysis reports.

#### Step 1: Create Pandoc/LaTeX Template

**File**: `analysis-report.tex`

```latex
% analysis-report.tex - Template for R Analysis Reports
\documentclass[$if(fontsize)$$fontsize$$else$11pt$endif$]{article}

% Packages
\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}
\usepackage[margin=1in]{geometry}
\usepackage{graphicx}
\usepackage{booktabs}  % Beautiful tables
\usepackage{longtable} % Multi-page tables
\usepackage{fancyhdr}
\usepackage{xcolor}
\usepackage{hyperref}
\usepackage{listings}  % Code listings

% Colors for code
\definecolor{codebackground}{RGB}{248,248,248}
\definecolor{codecomment}{RGB}{96,96,96}
\definecolor{codekeyword}{RGB}{0,0,255}
\definecolor{codestring}{RGB}{163,21,21}

% Code formatting
\lstset{
    backgroundcolor=\color{codebackground},
    basicstyle=\ttfamily\small,
    commentstyle=\color{codecomment},
    keywordstyle=\color{codekeyword},
    stringstyle=\color{codestring},
    breaklines=true,
    showstringspaces=false,
    frame=single
}

% Header/Footer
\pagestyle{fancy}
\fancyhf{}
\fancyhead[L]{$if(shorttitle)$$shorttitle$$else$$title$$endif$}
\fancyhead[R]{$date$}
\fancyfoot[C]{\thepage}
\renewcommand{\headrulewidth}{0.4pt}

% Title page customization
$if(logo)$
\usepackage{eso-pic}
\newcommand\BackgroundPic{%
\put(0,0){%
\parbox[b][\paperheight]{\paperwidth}{%
\vfill
\centering
\includegraphics[width=0.3\paperwidth]{$logo$}%
\vfill
}}}
$endif$

% Metadata
\title{$title$}
\author{$for(author)$$author$$sep$ \and $endfor$}
\date{$date$}

% Hyperlinks
\hypersetup{
    colorlinks=true,
    linkcolor=blue,
    urlcolor=blue,
    citecolor=blue,
    pdfauthor={$for(author)$$author$$sep$, $endfor$},
    pdftitle={$title$}
}

\begin{document}

$if(logo)$
\AddToShipoutPicture*{\BackgroundPic}
$endif$

% Title page
\maketitle

$if(abstract)$
\begin{abstract}
$abstract$
\end{abstract}
$endif$

% Table of contents
$if(toc)$
\newpage
\tableofcontents
\newpage
$endif$

% Main content (converted from RMarkdown)
$body$

% Session info section
$if(sessioninfo)$
\newpage
\section*{R Session Information}
This analysis was conducted using the following R environment:
\begin{verbatim}
$sessioninfo$
\end{verbatim}
$endif$

\end{document}
```

#### Step 2: Create RMarkdown Document

**File**: `analysis.Rmd`

```rmarkdown
---
title: "Customer Behavior Analysis"
shorttitle: "Customer Analysis"
author:
  - "Jane Smith (Data Scientist)"
  - "John Doe (Analyst)"
date: "`r format(Sys.Date(), '%B %d, %Y')`"
abstract: |
  This report analyzes customer purchase patterns using regression
  analysis and clustering techniques. We identify key customer segments
  and provide actionable recommendations.
output:
  pdf_document:
    template: analysis-report.tex
    toc: true
    number_sections: true
    fig_caption: true
    keep_tex: false
  html_document:
    toc: true
    theme: united
params:
  data_file: "customers.csv"
  analysis_date: !r Sys.Date()
---

```{r setup, include=FALSE}
# Chunk options
knitr::opts_chunk$set(
  echo = TRUE,           # Show code
  warning = FALSE,       # Hide warnings
  message = FALSE,       # Hide messages
  fig.width = 7,         # Figure width
  fig.height = 5,        # Figure height
  fig.align = 'center'   # Center figures
)

# Load libraries
library(ggplot2)
library(dplyr)
library(knitr)
library(kableExtra)
```

# Introduction

This analysis examines customer behavior patterns from our e-commerce
platform. Our dataset contains `r nrow(customers)` customer records.

## Research Questions

1. What factors influence purchase amount?
2. Can we identify distinct customer segments?
3. What are the characteristics of high-value customers?

# Data Overview

```{r load-data}
# Load data (in practice, use params$data_file)
set.seed(123)
customers <- data.frame(
  customer_id = 1:200,
  age = rnorm(200, mean = 35, sd = 10),
  income = rnorm(200, mean = 50000, sd = 15000),
  purchases = rpois(200, lambda = 5),
  total_spent = rnorm(200, mean = 500, sd = 200)
)

# Clean data
customers <- customers %>%
  filter(age > 18, income > 0, total_spent > 0)
```

Our cleaned dataset contains **`r nrow(customers)`** customers.

## Summary Statistics

```{r summary-table}
# Create summary table
summary_stats <- customers %>%
  summarise(
    `Mean Age` = round(mean(age), 1),
    `Mean Income` = round(mean(income), 0),
    `Mean Purchases` = round(mean(purchases), 1),
    `Mean Spent` = round(mean(total_spent), 2)
  ) %>%
  tidyr::pivot_longer(
    everything(),
    names_to = "Metric",
    values_to = "Value"
  )

# Display table
kable(summary_stats,
      caption = "Summary Statistics",
      booktabs = TRUE,
      format.args = list(big.mark = ",")) %>%
  kable_styling(latex_options = c("striped", "hold_position"))
```

# Exploratory Analysis

## Age Distribution

```{r age-histogram, fig.cap="Distribution of Customer Ages"}
ggplot(customers, aes(x = age)) +
  geom_histogram(bins = 20, fill = "steelblue", color = "white") +
  labs(
    title = "Customer Age Distribution",
    x = "Age (years)",
    y = "Count"
  ) +
  theme_minimal()
```

The age distribution shows most customers are between 25 and 45 years old.

## Spending vs Income

```{r spending-income, fig.cap="Relationship between Income and Spending"}
ggplot(customers, aes(x = income, y = total_spent)) +
  geom_point(alpha = 0.6, color = "darkgreen") +
  geom_smooth(method = "lm", color = "red") +
  labs(
    title = "Income vs Total Spending",
    x = "Annual Income ($)",
    y = "Total Spent ($)"
  ) +
  scale_x_continuous(labels = scales::dollar) +
  scale_y_continuous(labels = scales::dollar) +
  theme_minimal()
```

There is a positive relationship between income and spending (r = `r round(cor(customers$income, customers$total_spent), 2)`).

# Statistical Analysis

## Regression Model

```{r regression-model}
# Fit linear model
model <- lm(total_spent ~ age + income + purchases, data = customers)

# Display results
summary(model)
```

### Model Results

```{r model-table}
# Extract coefficients
coef_table <- data.frame(
  Variable = names(coef(model)),
  Coefficient = round(coef(model), 2),
  `Std Error` = round(summary(model)$coefficients[, 2], 2),
  `P-value` = format.pval(summary(model)$coefficients[, 4], digits = 3)
)

kable(coef_table,
      caption = "Regression Coefficients",
      booktabs = TRUE,
      row.names = FALSE) %>%
  kable_styling(latex_options = "hold_position")
```

The model explains **`r round(summary(model)$r.squared * 100, 1)`%** of the variance in spending (R² = `r round(summary(model)$r.squared, 3)`).

## Customer Segmentation

```{r clustering}
# K-means clustering
set.seed(42)
clusters <- kmeans(customers[, c("age", "income", "total_spent")], centers = 3)
customers$segment <- factor(clusters$cluster,
                            labels = c("Budget", "Premium", "Luxury"))

# Segment summary
segment_summary <- customers %>%
  group_by(segment) %>%
  summarise(
    Count = n(),
    `Avg Age` = round(mean(age), 1),
    `Avg Income` = round(mean(income), 0),
    `Avg Spent` = round(mean(total_spent), 2)
  )

kable(segment_summary,
      caption = "Customer Segments",
      booktabs = TRUE,
      format.args = list(big.mark = ",")) %>%
  kable_styling(latex_options = "hold_position")
```

# Conclusions

## Key Findings

Based on our analysis, we found:

1. **Income is the strongest predictor** of spending (β = `r round(coef(model)["income"], 4)`, p < 0.001)
2. **Three distinct segments** emerge from clustering analysis
3. **Premium segment** represents the highest value customers

## Recommendations

1. Target marketing to premium segment customers
2. Develop retention programs for high-income customers
3. Create age-appropriate product recommendations

# Technical Details

```{r session-info, echo=FALSE, results='asis'}
# Capture session info
si <- capture.output(sessionInfo())
cat("```\n")
cat(paste(si, collapse = "\n"))
cat("\n```\n")
```

---

**Analysis completed**: `r Sys.time()`  
**R version**: `r getRversion()`  
**Platform**: `r R.version$platform`
```

#### Step 3: Render the Document

**In R Console**:

```r
# Method 1: Using rmarkdown package
rmarkdown::render("analysis.Rmd")

# Method 2: With parameters
rmarkdown::render(
  "analysis.Rmd",
  params = list(
    data_file = "my_data.csv",
    analysis_date = Sys.Date()
  )
)

# Method 3: Multiple formats
rmarkdown::render("analysis.Rmd", output_format = "all")
```

**In RStudio**: Click "Knit" button or press `Ctrl/Cmd + Shift + K`

**Command Line**:

```bash
# Requires R and rmarkdown package installed
Rscript -e "rmarkdown::render('analysis.Rmd')"
```

### RMarkdown Template Features

#### 1. Dynamic Content with R Code

```rmarkdown
The mean age is `r mean(customers$age)` years.

We analyzed `r nrow(customers)` customers on `r Sys.Date()`.
```

#### 2. Code Chunks with Options

```rmarkdown
```{r analysis, echo=TRUE, fig.cap="My Plot", cache=TRUE}
# This code will be shown and cached
plot(x, y)
```
```

Common chunk options:
- `echo`: Show code (TRUE/FALSE)
- `eval`: Run code (TRUE/FALSE)
- `include`: Include output (TRUE/FALSE)
- `warning`, `message`: Show warnings/messages
- `fig.width`, `fig.height`: Figure dimensions
- `cache`: Cache results

#### 3. Child Documents

```rmarkdown
```{r child='chapter1.Rmd'}
```

```{r child='chapter2.Rmd'}
```
```

#### 4. Parameterized Reports

**In YAML**:
```yaml
params:
  region: "North"
  year: 2025
  threshold: 100
```

**In document**:
```rmarkdown
Analysis for region: `r params$region`

```{r}
data %>% filter(region == params$region, year == params$year)
```
```

**Render with different parameters**:
```r
rmarkdown::render("report.Rmd", params = list(region = "South", year = 2024))
```

### Advanced: Custom RMarkdown Template Package

Create a reusable template package for your organization.

#### Package Structure

```
myreport/
├── DESCRIPTION
├── NAMESPACE
└── inst/
    └── rmarkdown/
        └── templates/
            └── company_report/
                ├── skeleton/
                │   └── skeleton.Rmd
                └── template.yaml
```

#### Files

**`DESCRIPTION`**:
```
Package: myreport
Type: Package
Title: Company Report Templates
Version: 1.0.0
Author: Your Name
Description: RMarkdown templates for company reports
License: MIT
Encoding: UTF-8
```

**`inst/rmarkdown/templates/company_report/template.yaml`**:
```yaml
name: Company Report
description: Standard company analysis report
create_dir: false
```

**`inst/rmarkdown/templates/company_report/skeleton/skeleton.Rmd`**:
```rmarkdown
---
title: "Company Report"
author: "Your Name"
date: "`r Sys.Date()`"
output:
  pdf_document:
    template: company-template.tex
---

# Introduction

Your content here...
```

#### Install and Use

```r
# Install package
devtools::install("myreport")

# In RStudio: File > New File > R Markdown > From Template > Company Report
```

### RMarkdown vs Pandoc Templates Summary

| Feature | RMarkdown | Pure Pandoc |
|---------|-----------|-------------|
| **Input** | `.Rmd` with R code | `.md` without code |
| **Processing** | R execution → Pandoc | Pandoc only |
| **Dynamic content** | Yes (R code) | No |
| **Use case** | Data analysis, reports | Static documents |
| **Learning curve** | Steeper (R + Markdown) | Easier |
| **Output** | PDF, HTML, Word, etc. | Same |
| **Template syntax** | Same (Pandoc) | Pandoc syntax |

**When to use RMarkdown**:
- Data analysis reports
- Reproducible research
- Dynamic dashboards
- Literate programming

**When to use Pandoc only**:
- Static documentation
- Non-R users
- Simple conversions
- Faster processing

---

## Summary

**Key Takeaways**:

1. **Templates** control Pandoc's output format and structure
2. Use **variables** (`$var$`) for dynamic content
3. **Conditionals** (`$if(var)$...$endif$`) enable flexibility
4. **Loops** (`$for(var)$...$endfor$`) handle lists
5. Start from **default templates** and customize
6. Test with **simple documents** first
7. **Document** your templates and provide examples

**Template Development Workflow**:
1. Get default template: `pandoc -D latex > base.tex`
2. Customize incrementally
3. Test with minimal Markdown
4. Add variables and conditionals
5. Document usage
6. Create example documents
7. Install to `~/.pandoc/templates/`

**Next Steps**:
- Create templates for your common document types
- Explore HTML and DOCX templates
- Study existing templates on GitHub
- Integrate with build automation (Makefiles, CI/CD)
- Create template library for team/organization

---

## Additional Resources

### Documentation
- **Pandoc Manual**: https://pandoc.org/MANUAL.html#templates
- **Template Syntax**: https://pandoc.org/MANUAL.html#template-syntax
- **Default Templates**: https://github.com/jgm/pandoc-templates

### Example Templates
- **Eisvogel**: https://github.com/Wandmalfarbe/pandoc-latex-template (Beautiful LaTeX template)
- **Awesome Pandoc**: https://github.com/jgm/pandoc/wiki/User-contributed-templates

### Tools
- **Pandoc-scholar**: Academic writing templates
- **Pandoc-crossref**: Cross-referencing support
- **Pandoc-citeproc**: Citation processing

### Communities
- **Pandoc Discussion**: https://groups.google.com/g/pandoc-discuss
- **Stack Overflow**: `[pandoc]` tag
- **GitHub Discussions**: https://github.com/jgm/pandoc/discussions

---

**Last Updated**: October 2025
