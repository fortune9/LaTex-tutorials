# LaTeX Macros and Commands Tutorial - Quick Index

This index helps you quickly find information in the expanded `01-macros-commands.md` tutorial.

## 🎯 Quick Navigation

### By Topic

#### **Creating Custom Commands**
- [Why Use Custom Commands?](01-macros-commands.md#why-use-custom-commands)
- [Basic Command Definition](01-macros-commands.md#basic-command-definition)
- [Commands with Arguments](01-macros-commands.md#commands-with-arguments)
- [Optional Arguments](01-macros-commands.md#optional-arguments)

#### **Managing Existing Commands**
- [Renewing and Providing Commands](01-macros-commands.md#renewing-and-providing-commands)
- [Declarations vs Commands](01-macros-commands.md#declarations-vs-commands)

#### **Creating Environments**
- [Custom Environments with `\newenvironment`](01-macros-commands.md#custom-environments-with-newenvironment)
- [Advanced Environment Definition with xparse](01-macros-commands.md#advanced-environment-definition-with-xparse) - **NEW**

#### **Using Pre-built Commands**
- [Pre-defined LaTeX Commands and Macros](01-macros-commands.md#pre-defined-latex-commands-and-macros) - **NEW**

#### **Advanced Topics**
- [Advanced Techniques](01-macros-commands.md#advanced-techniques)
- [Best Practices](01-macros-commands.md#best-practices)
- [Common Use Cases](01-macros-commands.md#common-use-cases)

---

## 📚 By Use Case

### "I want to create a custom command"
1. Read: [Why Use Custom Commands?](01-macros-commands.md#why-use-custom-commands)
2. Learn: [Basic Command Definition](01-macros-commands.md#basic-command-definition)
3. Enhance: [Commands with Arguments](01-macros-commands.md#commands-with-arguments)
4. Master: [Optional Arguments](01-macros-commands.md#optional-arguments)
5. Best Practices: [Best Practices](01-macros-commands.md#best-practices)

### "I want to create a custom environment"
1. Start: [Custom Environments with `\newenvironment`](01-macros-commands.md#custom-environments-with-newenvironment)
2. Upgrade: [Advanced Environment Definition with xparse](01-macros-commands.md#advanced-environment-definition-with-xparse) - **NEW**
3. Compare: [Key Differences Table](01-macros-commands.md#key-differences-newenvironment-vs-newdocumentenvironment)
4. Reference: [Argument Specifiers Table](01-macros-commands.md#argument-specifiers-for-xparse)

### "I need to look up a LaTeX command"
→ Go directly to [Pre-defined LaTeX Commands and Macros](01-macros-commands.md#pre-defined-latex-commands-and-macros)

See quick links below!

### "I'm upgrading from old LaTeX style to modern xparse"
1. Review: [Key Differences Table](01-macros-commands.md#key-differences-newenvironment-vs-newdocumentenvironment)
2. Study: [Conversion Example](01-macros-commands.md#example-1-basic-conversion-from-newenvironment)
3. Learn: [Why xparse is Better](01-macros-commands.md#advantages-of-newdocumentenvironment)
4. Practice: [Working Examples](01-macros-commands.md#simple-newdocumentenvironment-examples)

---

## 🔍 Quick Command Reference

### Most Commonly Used Pre-defined Commands

**Spacing** - [Full Reference](01-macros-commands.md#spacing-commands)
- `\par` - End paragraph
- `\medskip`, `\smallskip`, `\bigskip` - Vertical spacing
- `\quad`, `\qquad` - Horizontal spacing
- `\\` - Line break

**Text Formatting** - [Full Reference](01-macros-commands.md#text-formatting-commands)
- `\textbf{text}` - Bold
- `\textit{text}` - Italic
- `\texttt{text}` - Monospace (code)
- `\emph{text}` - Emphasis

**Font Control** - [Full Reference](01-macros-commands.md#font-commands)
- `\bfseries` - Bold (declaration)
- `\itshape` - Italic (declaration)
- `\normalfont` - Reset to normal
- Size: `\tiny`, `\small`, `\normalsize`, `\large`, `\huge`

**Math Mode** - [Full Reference](01-macros-commands.md#math-mode-commands)
- `$...$` - Inline math
- `\[...\]` - Display math
- `\frac{a}{b}` - Fraction
- `\sqrt{x}` - Square root

**Boxes and Frames** - [Full Reference](01-macros-commands.md#box-and-frame-commands)
- `\fbox{text}` - Simple box
- `\parbox{width}{text}` - Paragraph box
- `\mbox{text}` - Unbreakable box

---

## 📋 Reference Tables

### New xparse Argument Specifiers
[See Table](01-macros-commands.md#argument-specifiers-for-xparse)

| Code | Meaning | Common Use |
|------|---------|-----------|
| `m` | Mandatory argument | `{arg}` |
| `o` | Optional argument | `[arg]` or nothing |
| `s` | Star modifier | `*` or nothing |

**Full reference with all types:** See [Argument Specifiers for xparse](01-macros-commands.md#argument-specifiers-for-xparse)

### Command Categories

| Category | # Commands | See |
|----------|-----------|-----|
| Spacing | 22 | [Spacing Commands](01-macros-commands.md#spacing-commands) |
| Text Formatting | 15 | [Text Formatting Commands](01-macros-commands.md#text-formatting-commands) |
| Font Commands | 19 | [Font Commands](01-macros-commands.md#font-commands) |
| Paragraph | 5 | [Paragraph Formatting](01-macros-commands.md#paragraph-formatting) |
| Structural | 11 | [Structural Commands](01-macros-commands.md#structural-commands) |
| References | 6 | [References and Labels](01-macros-commands.md#references-and-labels) |
| Lists | 5 | [List Commands](01-macros-commands.md#list-commands) |
| Boxes | 8 | [Box and Frame Commands](01-macros-commands.md#box-and-frame-commands) |
| Math | 30+ | [Math Mode Commands](01-macros-commands.md#math-mode-commands) |
| Symbols | 35+ | [Special Characters and Symbols](01-macros-commands.md#special-characters-and-symbols) |
| Counters | 9 | [Counter Commands](01-macros-commands.md#counter-commands) |
| Conditionals | 8 | [Conditional Commands](01-macros-commands.md#conditional-commands) |
| Utilities | 11 | [Commonly Used Utility Commands](01-macros-commands.md#commonly-used-utility-commands) |

**Total Commands Referenced: 150+**

---

## 🆕 What's New in This Expansion?

### Added Section 1: Advanced Environment Definition with xparse

**Why it matters:**
- Create environments with **multiple optional arguments** (impossible with standard LaTeX!)
- Access arguments in both begin AND end code (no manual saving needed)
- Better error messages and cleaner code
- Modern, future-proof approach

**Key Topics:**
- [What is xparse?](01-macros-commands.md#what-is-xparse)
- [Comparison Table](01-macros-commands.md#key-differences-newenvironment-vs-newdocumentenvironment)
- [7 Practical Examples](01-macros-commands.md#simple-newdocumentenvironment-examples)
- [When to Use Each](01-macros-commands.md#when-to-use-what)

### Added Section 2: Pre-defined LaTeX Commands and Macros

**Why it matters:**
- Quick reference for 150+ built-in commands
- Organized by category for easy lookup
- Learn what's available before creating custom alternatives
- Save time by using existing solutions

**Key Topics:**
- [Spacing Commands](01-macros-commands.md#spacing-commands) - `\par`, `\medskip`, etc.
- [Text Formatting](01-macros-commands.md#text-formatting-commands) - Bold, italic, mono
- [Font Commands](01-macros-commands.md#font-commands) - Sizes and styles
- [Math Mode](01-macros-commands.md#math-mode-commands) - Equations and symbols
- [All 13 Categories](01-macros-commands.md#pre-defined-latex-commands-and-macros)

---

## 💡 Key Learnings

### When Creating Commands

✅ **DO:**
- Use semantic names: `\important` not `\red`
- Document your commands
- Group related commands together
- Test edge cases

❌ **DON'T:**
- Use cryptic abbreviations
- Duplicate built-in functionality
- Forget to handle edge cases
- Skip the testing phase

### When Creating Environments

✅ **Use `\newenvironment` for:**
- Simple single-argument environments
- When you don't need xparse

✅ **Use `\NewDocumentEnvironment` for:**
- Multiple optional arguments
- Complex argument patterns
- When arguments needed in end code
- Modern, well-maintained projects

### When Using Built-in Commands

✅ **DO:**
- Use `\par` for paragraph breaks (not blank lines in macros)
- Use spacing commands: `\medskip`, `\bigskip`
- Use `\normalfont` to reset to default
- Use appropriate math mode: `$...$` vs `\[...\]`

❌ **DON'T:**
- Redefine built-in commands without checking first
- Manually calculate spacing (use built-ins)
- Create custom math mode when standard exists
- Forget scoping with declarations

---

## 📖 Suggested Reading Path

**For Beginners:**
1. Start → [Why Use Custom Commands?](01-macros-commands.md#why-use-custom-commands)
2. Learn → [Basic Command Definition](01-macros-commands.md#basic-command-definition)
3. Lookup → [Common Use Cases](01-macros-commands.md#common-use-cases)
4. Reference → [Pre-defined Commands](01-macros-commands.md#pre-defined-latex-commands-and-macros)

**For Intermediate Users:**
1. Review → [Commands with Arguments](01-macros-commands.md#commands-with-arguments)
2. Explore → [Custom Environments with `\newenvironment`](01-macros-commands.md#custom-environments-with-newenvironment)
3. Discover → [Best Practices](01-macros-commands.md#best-practices)
4. Reference → [Pre-defined Commands](01-macros-commands.md#pre-defined-latex-commands-and-macros)

**For Advanced Users:**
1. Master → [Advanced Environment Definition with xparse](01-macros-commands.md#advanced-environment-definition-with-xparse) - **NEW**
2. Study → [Advanced Techniques](01-macros-commands.md#advanced-techniques)
3. Practice → [Argument Specifiers](01-macros-commands.md#argument-specifiers-for-xparse)
4. Reference → [All Tables](01-macros-commands.md#pre-defined-latex-commands-and-macros)

---

## 🎓 Learning Resources Referenced

- **xparse documentation**: Part of LaTeX3 experimental toolkit
- **Official LaTeX2e documentation**: Standard commands and environments
- **Best practices**: From the LaTeX community and professional typesetting

---

## File Information

- **File**: `/home/ubuntu/work/github/LaTex-tutorials/05-advanced/01-macros-commands.md`
- **Lines**: 1835 (expanded from 1202)
- **Size**: 48KB
- **Format**: Markdown with LaTeX code examples
- **Last Updated**: October 27, 2025
- **Total Commands Referenced**: 150+
- **Code Examples**: 60+
- **Reference Tables**: 13

---

## 🔗 Related Files

- **`02-custom-classes-templates.md`** - For creating document classes
- **`03-pandoc-templates.md`** - For template conversion
- **`../02-formatting/01-fonts.md`** - For font-related commands
- **`../02-formatting/02-margins-spacing.md`** - For spacing documentation

---

## 📝 How to Use This Index

1. **Quick Lookup**: Scroll to the section that matches your need
2. **Click Links**: Use markdown links to jump to specific topics
3. **Tables**: Find the command category you need in the reference tables
4. **Examples**: Always read example code before implementing
5. **Best Practices**: Review before creating custom commands

---

## Need Help?

- **"I can't find command X"** → Check [all 13 reference tables](01-macros-commands.md#pre-defined-latex-commands-and-macros)
- **"When do I use xparse?"** → See [When to Use What](01-macros-commands.md#when-to-use-what)
- **"Show me examples"** → Browse [7 xparse examples](01-macros-commands.md#simple-newdocumentenvironment-examples) or [common use cases](01-macros-commands.md#common-use-cases)
- **"I want to learn best practices"** → Go to [Best Practices](01-macros-commands.md#best-practices)

---

**Happy LaTeX'ing!** 🎓

