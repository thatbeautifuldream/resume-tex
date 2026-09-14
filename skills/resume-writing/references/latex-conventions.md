# LaTeX resume conventions

Most engineering LaTeX resumes are single-column, [Jake's Resume](https://github.com/jakegut/resume)-style
templates — exactly the shape the wiki recommends. Edit the file in place; don't swap templates or introduce
new packages without being asked. Read the preamble first: macro names and argument orders vary between forks.

## Build

Prefer the project's own command (`package.json` scripts, `Makefile`). Otherwise:

```
latexmk -pdf -interaction=nonstopmode -halt-on-error resume.tex   # one build
latexmk -pdf -pvc resume.tex                                      # continuous rebuild while editing
latexmk -c resume.tex                                             # remove aux files
```

Page count check after every content change:

```
pdfinfo resume.pdf | grep Pages
```

## Macros

The Jake's Resume macros:

```latex
\resumeSubheading{Role}{Company}{Dates}{Location}   % 2x2 grid, dates right-aligned
\resumeItemListStart ... \resumeItemListEnd         % bullets for one role
\resumeItem{...}                                    % one bullet
\resumeSubHeadingListStart ... \resumeSubHeadingListEnd  % wraps all roles in a section
```

Sections are `\section{Skills}`, `\section{Experience}`, `\section{Education}` — small-caps
with a rule underneath, defined by the `\titleformat` block.

Education usually reuses `\resumeSubheading` with the argument order shifted:
`{School}{Location}{Degree}{Graduation date}`.

Keep role titles in one format across every entry, e.g. `{Software Engineer -- Payments}` everywhere rather
than mixing `--` and commas.

## Typography

- `--` renders an en dash. Date ranges: `{Feb 2025 -- Present}` → "Feb 2025 – Present". Keep the spaces.
- Escape `&`, `%`, `$`, `#`, `_` as `\&`, `\%`, `\$`, `\#`, `\_`. A bare `&` inside `\resumeItem` breaks
  the build with a misplaced-alignment error.
- The `~` character is a non-breaking space, not a tilde. Use `\textasciitilde` for a literal one.
- `\textbf{}` inside bullets is emphasis the wiki advises against.
- The document should be `\raggedright`; never turn on justification.
- Links use `\href{url}{display text}`. Display text should be the bare domain form
  (`github.com/user`), never the full URL with `https://www.`.

## Fitting one page

One page is a hard invariant — see the SKILL.md section on it. Verify the page count after every content
change, and cut content in the order given there.

In Jake's Resume the geometry is already at its limit and is **not** a lever:

- `\addtolength` block: 0.5in side margins, tightened top margin, +1in or more text height
- `\resumeItem`, `\resumeSubheading`, and `\resumeItemListEnd` each carry negative `\vspace` already
- `\resumeItem` wraps content in `\small`

Do not shrink the font further, cut margins below 0.4in, add negative `\vspace`, switch to two columns,
or reduce line spacing below 1.07. If it doesn't fit, there is too much content.

Rough capacity at that geometry: **~34 bullet lines** across all roles once the header, skills
block, section rules, and education take their share. A one-line bullet costs 1, a wrapped bullet costs 2.
Budget before writing: five 2-line bullets in the current role leaves roughly 24 lines for everything else.

To see how lines actually wrap, extract the text layout: `pdftotext -layout resume.pdf -`.

## Watch for

- A bullet that wraps and leaves 1–4 orphan words on the last line — rewrite it shorter or longer.
- A skills line that wraps by a word or two — trim or regroup it.
- A bullet extending past the right edge of the dates column.
- Hyphenated word breaks across lines (add `\hyphenation{}` or reword).
- Overfull `\hbox` warnings in the latexmk output — they mean text is spilling into the margin.
