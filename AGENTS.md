# resume-tex

A one-page LaTeX resume: `resume.tex` → `resume.pdf`. Use the `resume-writing` skill for any change to it.

## Build

```
pnpm pdf       # latexmk -pdf, one build
pnpm watch     # continuous rebuild while editing
pnpm preview   # open resume.pdf
pnpm build     # pdf + clean aux files
pnpm clean     # latexmk -c
```

Verify one page after every content change: `pnpm pdf && pdfinfo resume.pdf | grep Pages`.

## Deliberate deviations

Flag these when relevant; don't "fix" them unprompted:

- `\textbf{}` emphasis for skill categories.
- Colored, underlined hyperlinks (`RoyalBlue` in the `hyperref` setup).
- Phone number and LinkedIn/X links in the header.
- Most bullets carry no metric. The indoor-positioning accuracy bullet is the model to imitate.

## Skill

`skills/resume-writing` is the source of the skill published on skills.sh. Edit it there, then refresh the installed
copies in `.agents/skills` and `.claude/skills` with `npx skills add . --skill resume-writing -a claude-code -a codex -a cursor -y`.
