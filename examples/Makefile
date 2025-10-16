# Makefile for LaTeX examples
# Usage:
#   make              - Compile simple_article.tex
#   make view         - Compile and open PDF
#   make clean        - Remove auxiliary files
#   make distclean    - Remove all generated files
#   make watch        - Continuous compilation

# Main document (without .tex extension)
MAIN = simple_article

# LaTeX compiler
LATEX = pdflatex
BIBTEX = bibtex

# Flags
LATEXFLAGS = -interaction=nonstopmode -synctex=1

# Output
PDF = $(MAIN).pdf

.PHONY: all clean distclean view watch help

all: $(PDF)

# Compile the document (multiple passes for cross-references)
$(PDF): $(MAIN).tex
	@echo "Compiling $(MAIN).tex..."
	$(LATEX) $(LATEXFLAGS) $(MAIN)
	@if grep -q "\\bibliography" $(MAIN).tex; then \
		echo "Running BibTeX..."; \
		$(BIBTEX) $(MAIN) || true; \
		$(LATEX) $(LATEXFLAGS) $(MAIN); \
	fi
	$(LATEX) $(LATEXFLAGS) $(MAIN)
	@echo "✓ Compilation complete: $(PDF)"

# Clean auxiliary files
clean:
	@echo "Cleaning auxiliary files..."
	rm -f *.aux *.log *.out *.toc *.bbl *.blg *.synctex.gz
	rm -f *.fls *.fdb_latexmk *.nav *.snm *.vrb
	@echo "✓ Clean complete"

# Remove all generated files including PDF
distclean: clean
	@echo "Removing PDF..."
	rm -f $(PDF)
	@echo "✓ Distclean complete"

# View the PDF (cross-platform)
view: $(PDF)
	@echo "Opening $(PDF)..."
	@if command -v xdg-open > /dev/null 2>&1; then \
		xdg-open $(PDF) & \
	elif command -v open > /dev/null 2>&1; then \
		open $(PDF) & \
	elif command -v start > /dev/null 2>&1; then \
		start $(PDF) & \
	else \
		echo "Could not detect PDF viewer. Please open $(PDF) manually."; \
	fi

# Continuous compilation (requires latexmk)
watch:
	@echo "Starting continuous compilation..."
	@echo "Press Ctrl+C to stop"
	@if command -v latexmk > /dev/null 2>&1; then \
		latexmk -pdf -pvc $(MAIN); \
	else \
		echo "Error: latexmk not found. Install it first."; \
		exit 1; \
	fi

# Show help
help:
	@echo "LaTeX Example Makefile"
	@echo ""
	@echo "Available targets:"
	@echo "  make           - Compile $(MAIN).tex to PDF"
	@echo "  make view      - Compile and open the PDF"
	@echo "  make clean     - Remove auxiliary files"
	@echo "  make distclean - Remove all generated files (including PDF)"
	@echo "  make watch     - Continuous compilation (requires latexmk)"
	@echo "  make help      - Show this help message"
	@echo ""
	@echo "Examples:"
	@echo "  make                 # Compile the document"
	@echo "  make view            # Compile and view"
	@echo "  make clean           # Clean up auxiliary files"
	@echo "  make watch           # Auto-recompile on changes"
