# Gikz — GeoGebra TikZ Code Cleaner

## What is Gikz?

Gikz is a CLI tool that cleans GeoGebra's verbose TikZ exports into concise, readable LaTeX code.
It is a single Node.js script (`gikz.js`) with zero dependencies.

## When to use Gikz

When the user has `.txt` or `.tex` files exported from GeoGebra containing raw TikZ code, use Gikz to clean them before inserting into LaTeX documents.

Signs that code needs cleaning:
- Contains `\definecolor{...}{rgb}{...}` with long decimal color definitions
- Has `line width=2pt` or `color=rvwvcq` style noise
- Coordinates have 15+ decimal places
- Points are drawn with `\draw [fill=rvwvcq]` instead of clean `\draw[fill=black]`
- Wrapped in `\begin{scriptsize}...\end{scriptsize}`

## How to invoke

```bash
# Basic: clean a single file, output to stdout
node gikz.js <input-file>

# Standalone document (compilable with pdflatex)
node gikz.js -s <input-file>

# Save to file
node gikz.js -s -o output.tex <input-file>

# Batch: clean multiple files into a directory
node gikz.js file1.txt file2.txt -o output_dir/

# Pipe from stdin
cat export.txt | node gikz.js -s

# Options
#   -s, --standalone    Wrap in standalone document class
#   -t, --tikzonly      Output tikzpicture only (default)
#   --no-points         Omit point markers
#   --no-labels         Omit point labels
#   --no-round          Keep original coordinate precision
#   -o, --output PATH   Output to file or directory
```

## Typical workflow

1. User exports TikZ from GeoGebra → gets a `.txt` file with messy code
2. Run: `node gikz.js -s -o clean.tex export.txt`
3. The output `clean.tex` is ready to compile or include in a document

## What the tool does

- Extracts `tikzpicture` environment from full LaTeX documents
- Maps raw coordinates to named labels (A, B, C...)
- Rounds coordinates to 3 decimal places
- Strips `line width`, `color=...` noise from draw commands
- Converts dash patterns to TikZ shorthands (`dashed`, `dotted`, `dash dot`)
- Detects circles, ellipses, arcs, sectors, angle marks, function plots, Bézier curves
- Smart label positioning (above/below/left/right based on point geometry)
- Groups output by category with comments

## Error handling

- If no `tikzpicture` environment is found, the tool throws an error
- Invalid files are skipped in batch mode with error messages
- Exit code 1 if any file fails
