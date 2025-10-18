# LaTeX Tutorials

A comprehensive collection of LaTeX tutorials and documentation for learners at all levels.

## 📚 Overview

This repository contains tutorials, guides, and examples for learning LaTeX, the powerful document preparation system. Whether you're a beginner just starting out or an experienced user looking for advanced techniques, you'll find helpful resources here.

LaTeX is widely used in academia, scientific research, and technical writing for its:
- Professional typesetting quality
- Superior mathematical notation
- Automatic numbering and cross-referencing
- Consistent formatting
- Version control friendliness

## 🗂️ Repository Structure

```
LaTex-tutorials/
├── 01-basics/              # Fundamental concepts
│   ├── 01-document-structure.md
│   └── 02-text-formatting-basics.md
├── 02-formatting/          # Styling and layout
│   ├── 01-fonts.md
│   ├── 02-margins-spacing.md
│   └── 03-headers-footers.md
├── 03-setup/              # Installation guides
│   ├── 01-setup-windows.md
│   ├── 02-setup-macos.md
│   ├── 03-setup-linux.md
│   └── 04-latex-engines.md
├── 04-compilation/        # Building PDFs
│   └── 01-compiling-latex.md
├── 05-advanced/           # Advanced topics
│   ├── 01-macros-commands.md
│   └── 02-custom-classes-templates.md
├── 06-resources/          # External resources
│   └── 01-useful-sites.md
└── examples/              # Complete examples
    ├── README.md
    ├── simple_article.tex
    └── 01-simple-article.md
```

## 🚀 Getting Started

### Prerequisites

Before diving into these tutorials, you should:
- Have basic computer literacy
- Be comfortable with text editors
- Understand basic file management
- Have patience for a learning curve (LaTeX is different from WYSIWYG editors)

No prior programming knowledge is required, though it can be helpful.

### Installation

Choose your operating system and follow the setup guide:

1. **[Windows Setup](03-setup/01-setup-windows.md)** - Install MiKTeX or TeX Live on Windows
2. **[macOS Setup](03-setup/02-setup-macos.md)** - Install MacTeX on Mac
3. **[Linux Setup](03-setup/03-setup-linux.md)** - Install TeX Live on Linux
4. **[LaTeX Engines Guide](03-setup/04-latex-engines.md)** - Compare pdfLaTeX, XeLaTeX, and LuaLaTeX

**VS Code Users** (Recommended for beginners):
- 📖 [VS Code Quick Reference](03-setup/06-vscode-quick-reference.md) - Complete configuration guide
- 🔧 [VS Code Troubleshooting](03-setup/05-vscode-troubleshooting.md) - Fix common issues
- ⚙️ [Example settings.json](03-setup/example-settings.json) - Copy-paste ready configuration

**Quick Start (Online)**:
If you want to try LaTeX without installation, use [Overleaf](https://www.overleaf.com/) - a free online LaTeX editor.

### Your First Document

After installation, follow the [Document Structure](01-basics/01-document-structure.md) tutorial to create your first LaTeX document.

## 📖 Learning Path

### For Beginners

1. **Setup** (30 minutes)
   - [Choose your OS setup guide](03-setup/)
   - Install LaTeX distribution
   - Choose a text editor

2. **Basics** (2-3 hours)
   - [Document Structure](01-basics/01-document-structure.md) - Learn the skeleton of every LaTeX document
   - [Text Formatting Basics](01-basics/02-text-formatting-basics.md) - Basic styling and formatting
   - [Compiling Documents](04-compilation/01-compiling-latex.md) - Turn `.tex` files into PDFs

3. **Formatting** (3-4 hours)
   - [Fonts](02-formatting/01-fonts.md) - Typography and font management
   - [Margins and Spacing](02-formatting/02-margins-spacing.md) - Page layout control
   - [Headers and Footers](02-formatting/03-headers-footers.md) - Document navigation

4. **Practice** (ongoing)
   - [Simple Article Example](examples/01-simple-article.md) - Complete working example
   - Modify examples for your needs
   - Create your own documents

### For Intermediate Users

If you're already familiar with LaTeX basics:

1. **Advanced Techniques** (4-8 hours)
   - [Custom Commands and Macros](05-advanced/01-macros-commands.md) - Create reusable commands
   - [Custom Classes and Templates](05-advanced/02-custom-classes-templates.md) - Build document classes
   - Study complex examples in `examples/`
   - Learn about specialized packages
   - Optimize your workflow with automation

2. **Specialization**
   - Create your own document classes for consistent formatting
   - Choose packages for your field (math, chemistry, linguistics, etc.)
   - Explore bibliography management (BibTeX, BibLaTeX)
   - Learn figure and table best practices

### For Advanced Users

- Contribute to this repository
- Create custom document classes
- Develop LaTeX packages
- Share your expertise

## 📝 Topics Covered

### Current Content

#### Basics
- Document structure and preamble
- Text formatting (bold, italic, lists)
- Sectioning and organization

#### Formatting
- Font families and sizes
- Page geometry and margins
- Line and paragraph spacing
- Headers and footers with fancyhdr

#### Setup
- Windows (MiKTeX, TeX Live)
- macOS (MacTeX, BasicTeX)
- Linux (distribution-specific guides)
- **[LaTeX Engines](03-setup/04-latex-engines.md)** - pdfLaTeX, XeLaTeX, LuaLaTeX comparison and usage
- Editor setup (TeXstudio, VS Code, Vim, etc.)
- Installing additional engines and packages

#### Compilation
- pdfLaTeX, XeLaTeX, LuaLaTeX
- latexmk automation
- Bibliography compilation
- Error debugging

#### Advanced Topics
- **[Custom Commands and Macros](05-advanced/01-macros-commands.md)** - Create reusable commands and automate repetitive tasks
  - Basic command definition with `\newcommand`
  - Commands with arguments (single and multiple)
  - Optional arguments and default values
  - Declarations vs commands
  - Advanced techniques with `xparse`
  - Best practices and common use cases
  - Complete working examples

- **[Custom Classes and Templates](05-advanced/02-custom-classes-templates.md)** - Build your own document classes
  - Understanding classes vs templates vs packages
  - Basic class structure and components
  - Creating simple custom classes
  - Implementing class options and parameters
  - Custom title pages and formatting
  - Complete examples (academic papers, company letters, theses)
  - Template creation and distribution
  - Best practices and documentation

#### Examples
- Simple article template
- Academic paper structure

#### Resources
- **[Useful Sites](06-resources/01-useful-sites.md)** - Curated collection of external learning resources
  - Tutorial websites and interactive learning platforms
  - Reference materials and quick guides
  - Video tutorials and YouTube channels
  - Online tools and converters
  - Books, communities, and specialized resources

### Coming Soon

- Mathematical typesetting (advanced)
- Bibliography management (BibTeX, Biblatex)
- Figure and table management
- Presentations with Beamer
- Book-length documents
- Custom environments and packages (.sty files)
- TikZ graphics
- Multi-file project organization
- And more!

## 🔧 Tools and Editors

### Recommended Editors

**For Beginners**:
- [TeXstudio](https://texstudio.sourceforge.net/) - Feature-rich, beginner-friendly
- [Overleaf](https://www.overleaf.com/) - Online, no installation needed

**For Advanced Users**:
- [Visual Studio Code](https://code.visualstudio.com/) with LaTeX Workshop extension
- [Vim](https://www.vim.org/) with vimtex plugin
- [Emacs](https://www.gnu.org/software/emacs/) with AUCTeX

### Compilation Tools

- **pdflatex** - Standard LaTeX compiler
- **xelatex** - Supports system fonts and Unicode
- **lualatex** - Modern, programmable LaTeX engine
- **latexmk** - Automated build tool (highly recommended)

### Additional Tools

- **BibDesk** (macOS) - Bibliography manager
- **JabRef** (cross-platform) - Bibliography reference manager
- **TeXworks** - Simple editor included with MiKTeX
- **latexdiff** - Show differences between document versions

## 🎯 Use Cases

LaTeX is ideal for:

- **Academic papers** - Articles, theses, dissertations
- **Scientific documents** - Research papers with equations
- **Books** - Long-form content with chapters
- **Presentations** - Professional slides with Beamer
- **CVs and resumes** - Professional-looking documents
- **Technical documentation** - Manuals and reports
- **Letters** - Formal correspondence

## 💡 Tips for Success

1. **Start Simple** - Begin with basic documents before complex projects
2. **Compile Often** - Catch errors early by compiling frequently
3. **Use Version Control** - Git works great with LaTeX source files
4. **Read Error Messages** - They're usually helpful once you learn to interpret them
5. **Search Online** - [TeX Stack Exchange](https://tex.stackexchange.com/) is invaluable
6. **Keep Backups** - Always backup your `.tex` source files
7. **Use Templates** - Save time by reusing working preambles
8. **Learn Incrementally** - Master one topic before moving to the next

## 🤝 Contributing

We welcome contributions! Here's how you can help:

### Types of Contributions

- **New tutorials** - Write guides on topics not yet covered
- **Improvements** - Enhance existing documentation
- **Examples** - Add practical, working examples
- **Translations** - Translate tutorials to other languages
- **Bug fixes** - Correct errors or outdated information
- **Feedback** - Report issues or suggest improvements

### Contribution Guidelines

1. **Fork the repository**
2. **Create a new branch** for your changes
   ```bash
   git checkout -b feature/your-tutorial-name
   ```
3. **Follow the existing style**:
   - Use Markdown for tutorials
   - Include code examples
   - Provide clear explanations
   - Add cross-references to related topics
4. **Test your examples** - Ensure LaTeX code compiles
5. **Submit a pull request** with a clear description

### Writing Guidelines

- **Clear and concise** - Avoid unnecessary jargon
- **Well-structured** - Use headings, lists, and code blocks
- **Beginner-friendly** - Explain concepts from first principles
- **Accurate** - Test all code examples
- **Complete** - Include prerequisites and next steps
- **Formatted** - Use proper Markdown syntax

### File Naming

- Use lowercase with hyphens: `document-structure.md`
- Number files for ordering: `01-basics.md`
- Be descriptive: `compiling-with-xelatex.md`

## 📚 Additional Resources

For a comprehensive, curated list of external LaTeX resources including tutorials, videos, tools, and more, see:

### 🌟 **[External Resources Guide](06-resources/01-useful-sites.md)**

This guide includes:
- **Tutorial Sites** - Interactive learning platforms and comprehensive guides
- **Reference Materials** - Documentation, quick references, and symbol finders
- **Video Tutorials** - YouTube channels and online courses
- **Online Tools** - Editors, converters, and helper utilities
- **Books** - Free and paid learning materials
- **Communities** - Forums, Q&A sites, and social media
- **Specialized Resources** - Subject-specific guides (chemistry, linguistics, music, etc.)
- **Package Documentation** - Popular packages and their usage

### Quick Links

**Official Documentation:**
- [LaTeX Project](https://www.latex-project.org/) - Official LaTeX website
- [CTAN](https://ctan.org/) - Comprehensive TeX Archive Network
- [TeX Live Documentation](https://tug.org/texlive/doc.html)

**Essential Communities:**
- [TeX Stack Exchange](https://tex.stackexchange.com/) - Q&A community (most helpful!)
- [LaTeX subreddit](https://www.reddit.com/r/LaTeX/) - Discussion forum
- [LaTeX Community](https://latex.org/forum/) - Help forum

**Must-Have Tools:**
- [Detexify](http://detexify.kirelabs.org/classify.html) - Draw symbols to find LaTeX commands
- [Overleaf](https://www.overleaf.com/) - Online LaTeX editor
- [Tables Generator](https://www.tablesgenerator.com/) - Visual table creator

## 📜 License

This repository is licensed under the [MIT License](LICENSE) - feel free to use, modify, and share these tutorials.

## 🙏 Acknowledgments

This repository is maintained as a personal learning resource and shared with the community. Thanks to:
- The LaTeX Project team
- All contributors to LaTeX packages
- The TeX Stack Exchange community
- Everyone who contributes to this repository

## 📬 Contact

Questions or suggestions? Feel free to:
- Open an issue in this repository
- Submit a pull request
- Reach out through GitHub discussions

---

**Happy LaTeXing!** 🎓

Remember: LaTeX has a learning curve, but the professional results are worth the effort. Take your time, practice regularly, and don't hesitate to ask for help.
