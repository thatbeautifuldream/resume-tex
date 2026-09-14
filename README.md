# resume-tex

[![skills.sh](https://skills.sh/b/thatbeautifuldream/resume-tex)](https://www.skills.sh/thatbeautifuldream/resume-tex/resume-writing)

A single-page LaTeX resume. Edit `resume.tex` and build it to get `resume.pdf`.

It also ships `resume-writing`, an agent skill that helps Claude Code, Codex, Cursor, and other agents write and review resumes. View it on [skills.sh](https://www.skills.sh/thatbeautifuldream/resume-tex/resume-writing), or install it in any project:

```bash
npx skills add thatbeautifuldream/resume-tex --skill resume-writing
```

Add `-g` to install it for all your projects. See [Agent skill](#agent-skill) for details.

## Requirements

- A TeX distribution with `latexmk` and `pdflatex`:
  - macOS: [MacTeX](https://www.tug.org/mactex/) (`brew install --cask mactex`)
  - Linux: TeX Live (`sudo apt install texlive-latex-extra latexmk`)
  - Windows: [MiKTeX](https://miktex.org/) or TeX Live
- [pnpm](https://pnpm.io/) (optional). It only runs the scripts below, and there are no packages to install.

If you use a smaller TeX install such as BasicTeX, add the packages the resume needs:

```bash
sudo tlmgr install latexmk titlesec marvosym enumitem fancyhdr
```

## Usage

```bash
git clone https://github.com/thatbeautifuldream/resume-tex.git
cd resume-tex
pnpm build
```

| Command        | What it does                                               |
| -------------- | ---------------------------------------------------------- |
| `pnpm build`   | Build `resume.pdf` and remove the intermediate files       |
| `pnpm pdf`     | Build `resume.pdf` and keep the intermediate files         |
| `pnpm watch`   | Rebuild every time `resume.tex` is saved                   |
| `pnpm preview` | Open `resume.pdf` (macOS only)                             |
| `pnpm clean`   | Remove the intermediate files (`.aux`, `.log`, `.fls`, ...) |

Without pnpm, run latexmk directly:

```bash
latexmk -pdf -interaction=nonstopmode -halt-on-error resume.tex
latexmk -c resume.tex
```

## Making it your own

Edit `resume.tex` and replace the heading, skills, experience, and education with your own. Each section is built from these macros:

- `\resumeSubheading{title}{company}{dates}{location}` for a role or degree
- `\resumeItemListStart` and `\resumeItemListEnd` around a role's bullets
- `\resumeItem{...}` for a single bullet

Escape `&`, `%`, `$`, `#`, and `_` as `\&`, `\%`, `\$`, `\#`, and `\_`. Write date ranges with `--`, which prints an en dash.

To make sure the resume still fits on one page, run:

```bash
pnpm pdf && pdfinfo resume.pdf | grep Pages
```

## Agent skill

`skills/resume-writing` is an [agent skill](https://skills.sh/docs) for writing and reviewing a one-page software engineering resume using the [r/EngineeringResumes wiki](https://www.reddit.com/r/EngineeringResumes/wiki/index/) standards. It works with Claude Code, Codex, Cursor, and other agents that support skills.

Install it in your own project, or globally with `-g`:

```bash
npx skills add thatbeautifuldream/resume-tex --skill resume-writing
npx skills add thatbeautifuldream/resume-tex --skill resume-writing -g
```

Pick specific agents with `-a`, for example `-a claude-code -a codex`. Once installed, ask your agent to review or edit your resume and it will load the skill.

This repo has the skill installed in `.agents/skills` and `.claude/skills`, and `skills-lock.json` records it. After editing `skills/resume-writing`, refresh those installed copies:

```bash
npx skills add . --skill resume-writing -a claude-code -a codex -a cursor -y
```

Repo-specific notes for agents, such as build commands and deliberate rule deviations, are in `AGENTS.md`.
