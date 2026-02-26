# Gikz

**Clean GeoGebra TikZ exports into concise, readable LaTeX code.**

A zero-dependency Node.js CLI tool that transforms GeoGebra's verbose TikZ output into clean, hand-written-style code ready for your `.tex` files.

> Derived from [GGB-Tikz-Code-Filter](https://github.com/By990920/GGB-Tikz-Code-Filter) by [By990920](https://github.com/By990920). Licensed under GPL-2.0.

## Features

- Strips redundant styles (`line width`, colors, `scriptsize` wrappers)
- Rounds coordinates to 3 decimal places (configurable)
- Replaces raw coordinates with named labels (`(A)`, `(B)`, …)
- Smart label positioning based on point geometry
- Converts line styles (`dash pattern=...` → `dashed`)
- Supports: points, lines, circles, ellipses, arcs, sectors, angle marks, function plots, Bézier curves, text labels
- Output as `tikzpicture` fragment or complete `standalone` document
- Batch processing & stdin/stdout piping

## Installation

```bash
# Global install (recommended)
npm install -g gikz

# Or run directly
npx gikz export.txt

# Or clone and use
git clone https://github.com/YOUR_USERNAME/gikz.git
cd gikz
node gikz.js export.txt
```

## Usage

```bash
# Basic — output tikzpicture to terminal
gikz export.txt

# Standalone document — ready for pdflatex
gikz -s export.txt

# Write to file
gikz -s -o clean.tex export.txt

# Batch — multiple files to a directory
gikz fig1.txt fig2.txt fig3.txt -o output/

# Pipe from stdin
cat export.txt | gikz -s > clean.tex

# Skip points and labels
gikz --no-points --no-labels export.txt

# Keep original coordinate precision
gikz --no-round export.txt
```

## Options

| Flag | Description |
|---|---|
| `-s`, `--standalone` | Output complete `standalone` LaTeX document |
| `-t`, `--tikzonly` | Output `tikzpicture` fragment only (default) |
| `--no-points` | Omit point markers (`\draw[fill=black]...`) |
| `--no-labels` | Omit point labels (`\node...`) |
| `--no-round` | Keep original coordinate precision |
| `-o`, `--output <path>` | Write to file (or directory for batch) |
| `-h`, `--help` | Show help |

## Example

**Input** (GeoGebra export):
```latex
\draw [line width=2pt,color=rvwvcq] (-2.75,2.1)-- (-4.89,-2.06);
\draw [fill=rvwvcq] (-2.75,2.1) circle (2.5pt);
\draw[color=rvwvcq] (-2.6468416958718426,2.3645220512615386) node {$A$};
```

**Output** (Gikz):
```latex
\coordinate (A) at (-2.75,2.1);
\draw (A) -- (B);
\draw[fill=black] (A) circle (1pt);
\node [above] at (A) {$A$};
```

## AI Coding Agent Integration

Gikz includes skill files for AI coding agents:

| Agent | File | Usage |
|---|---|---|
| Claude Code | `CLAUDE.md` | Auto-detected in workspace |
| OpenAI Codex | `AGENTS.md` | Auto-detected in workspace |

These files teach the agent how to invoke `gikz` to clean TikZ code within your project.

## Requirements

- Node.js ≥ 14

No other dependencies.

## License

GPL-2.0 — See [LICENSE](LICENSE).

Derived from [GGB-Tikz-Code-Filter](https://github.com/By990920/GGB-Tikz-Code-Filter) by [By990920](https://github.com/By990920).
