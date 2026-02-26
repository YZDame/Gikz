# Gikz — GeoGebra TikZ Code Cleaner

## Tool

`gikz.js` is a zero-dependency Node.js CLI that cleans GeoGebra TikZ exports.

## Commands

```bash
# Clean a GeoGebra export file
node gikz.js <file.txt>

# Output as standalone LaTeX document
node gikz.js -s <file.txt>

# Save output to file
node gikz.js -s -o clean.tex <file.txt>

# Batch process
node gikz.js *.txt -o output_dir/

# Pipe
cat file.txt | node gikz.js -s > out.tex
```

## Options

- `-s` / `--standalone` — standalone LaTeX document
- `-t` / `--tikzonly` — tikzpicture fragment (default)
- `--no-points` — omit point markers
- `--no-labels` — omit point labels
- `--no-round` — keep full precision
- `-o PATH` — output path

## When to use

Use when processing `.txt` files exported from GeoGebra that contain verbose TikZ code with long decimal coordinates, color definitions, and line width specifications. The tool strips noise, rounds coordinates, maps to named labels, and outputs clean TikZ.
