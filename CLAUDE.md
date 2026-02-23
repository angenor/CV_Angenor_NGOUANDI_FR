# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a LaTeX CV/resume for Angenor N'Gouandi, built on the **AltaCV** class (v1.6.5b fork by Nicolás Omar González Passerino). The CV is written in French.

## Build Commands

Compile with pdfLaTeX (default):
```bash
pdflatex main.tex
```

For XeLaTeX (required for `academicons` option or custom OpenType fonts):
```bash
xelatex -shell-escape -output-driver="xdvipdfmx -z 0" main.tex
```

If using bibliography (`sample.bib`), the full build chain is:
```bash
pdflatex main.tex && biber main && pdflatex main.tex
```

The project is also configured for **Overleaf** (see `.overleaf/settings.json`).

## Architecture

- **main.tex** — The CV document. Contains all content: personal info, skills, experience, missions, education. Uses a two-column `paracol` layout with a 25/75 split (`\columnratio{0.25}`). Left column has skills, languages, permits; right column has experience, missions, education.
- **altacv.cls** — The document class. Defines all custom commands (`\cvevent`, `\cvtag`, `\cvlang`, `\cvskill`, `\cvref`, `\wheelchart`, `\photoL`/`\photoR`, etc.) and handles light/dark mode theming.
- **pubs-authoryear.cfg** / **pubs-num.cfg** — Biblatex configuration for publication lists (APA6 vs IEEE style). Currently not loaded in main.tex.
- **sample.bib** — Sample bibliography file (not currently used).

## Key Conventions

- **Document class options** are set on line 31 of main.tex: `[10pt,a4paper,ragged2e,withhyper]`. To enable dark mode, add `darkmode` to these options.
- **Color scheme** is defined in main.tex (lines 59-83) with separate palettes for light and dark modes. Colors are mapped via `\colorlet` to semantic names: `name`, `tagline`, `heading`, `headingrule`, `accent`, `emphasis`, `body`.
- **Photo** is set with `\photoL{4cm}{angenor}` (circular crop by default; use `normalphoto` class option for rectangular).
- **Fonts**: Roboto Slab (serif/headings) and Lato (sans-serif/body) via packages when using pdfLaTeX; via `fontspec` when using XeLaTeX/LuaLaTeX.
- Content is in French — section names, descriptions, and dates should remain in French.
