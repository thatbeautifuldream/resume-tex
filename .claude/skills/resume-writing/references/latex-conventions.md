# LaTeX conventions in this repo

`resume.tex` is a single-column, Jake's-resume-style template — exactly the shape the wiki recommends.
Edit it in place; don't swap templates or introduce new packages without being asked.

## Build

```
pnpm pdf       # latexmk -pdf, one build
pnpm watch     # continuous rebuild while editing
pnpm preview   # open resume.pdf
pnpm build     # pdf + clean aux files
pnpm clean     # latexmk -c
```

Page count check after every content change:

```
pdfinfo resume.pdf | grep Pages
```

## Macros

```latex
\resumeSubheading{Role}{Company}{Dates}{Location}   % 2x2 grid, dates right-aligned
\resumeItemListStart ... \resumeItemListEnd         % bullets for one role
\resumeItem{...}                                    % one bullet
\resumeSubHeadingListStart ... \resumeSubHeadingListEnd  % wraps all roles in a section
```

Sections are `\section{Skills}`, `\section{Professional Experience}`, `\section{Education}` — small-caps
with a rule underneath, defined by the `\titleformat` block.

Education reuses `\resumeSubheading` with the argument order shifted:
`{School}{Location}{Degree}{Graduation date}`.

## Typography

- `--` renders an en dash. Date ranges: `{Feb 2025 -- Present}` → "Feb 2025 – Present". Keep the spaces.
- Escape `&`, `%`, `$`, `#`, `_` as `\&`, `\%`, `\$`, `\#`, `\_`. A bare `&` inside `\resumeItem` breaks
  the build with a misplaced-alignment error.
- The `~` character is a non-breaking space, not a tilde. Use `\textasciitilde` for a literal one.
- `\textbf{}` inside bullets is emphasis the wiki advises against — see the deviations note in SKILL.md.
- The document is `\raggedright`; never turn on justification.
- Links use `\href{url}{display text}`. Display text should be the bare domain form
  (`github.com/user`), never the full URL with `https://www.`.

## Fitting one page

One page is a hard invariant — see the SKILL.md section on it. Verify with
`pnpm pdf && pdfinfo resume.pdf | grep Pages` after every content change, and cut content in the order
given there.

The geometry is already at its limit and is **not** a lever:

- `\addtolength` block: 0.5in side margins, tightened top margin, +1.35in text height
- `\resumeItem`, `\resumeSubheading`, and `\resumeItemListEnd` each carry negative `\vspace` already
- `\resumeItem` wraps content in `\small` (≈9pt on a 10pt base)

Do not shrink the font further, cut margins below 0.4in, add negative `\vspace`, switch to two columns,
or reduce line spacing below 1.07. If it doesn't fit, there is too much content.

Rough capacity at the current geometry: **~34 bullet lines** across all roles once the header, skills
block, section rules, and education take their share. A one-line bullet costs 1, a wrapped bullet costs 2.
Budget before writing: five 2-line bullets in the current role leaves roughly 24 lines for everything else.

## Watch for

- A bullet that wraps and leaves 1–4 orphan words on the last line — rewrite it shorter or longer.
- A bullet extending past the right edge of the dates column.
- Hyphenated word breaks across lines (add `\hyphenation{}` or reword).
- Overfull `\hbox` warnings in the latexmk output — they mean text is spilling into the margin.
