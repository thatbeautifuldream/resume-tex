# Review checklist

Run before declaring the resume done. Report every failure, even ones you were told not to change.

## Build — do this first, and again last

- [ ] `pnpm pdf` succeeds with no errors
- [ ] **`pdfinfo resume.pdf | grep Pages` → 1.** Hard invariant. A 2-page build means the task is
      unfinished — cut content per the SKILL.md order and rebuild. Never report done on 2 pages.
- [ ] Geometry untouched: no font below 10.5pt, no margins below 0.4in, no new negative `\vspace`
- [ ] No overfull `\hbox` warnings pushing text into the margin

## Layout

- [ ] Single column, no icons/images/graphics
- [ ] Sections clearly separated, consistent spacing between roles
- [ ] Text ragged-right, not justified
- [ ] Font ≥ 10.5pt, black, margins ≥ 0.4in
- [ ] Bold/italics used sparingly and never stacked
- [ ] No bullet extends past the right edge of the dates column
- [ ] No wrapped bullet with a 1–4 word orphan line, no hyphenated line breaks

## Header

- [ ] Name is the most prominent element
- [ ] Exactly one email, modern provider
- [ ] Links in plain domain form, no `https://www.`, no "Email:"/"Portfolio:" prefixes
- [ ] No street address; no city/state unless the target job is there
- [ ] No age, gender, marital status, nationality, photo
- [ ] GitHub/portfolio links are live and non-empty

## Sections

- [ ] Order matches experience level (see rules.md)
- [ ] No summary/objective unless senior/staff+, career change, or gap
- [ ] No references section
- [ ] Education: graduation date only, no start date, no coursework, GPA only if ≥3.75 and early-career
- [ ] Projects (if present): personal work only, no "Project" in titles, links included

## Bullets

- [ ] Every bullet starts with a strong past-tense action verb
- [ ] No `utilize`, `spearheaded`, `leveraged`, `responsible for`, `worked on`, `helped`, `assisted`
- [ ] No personal pronouns, no trailing periods
- [ ] 1–2 lines each, 3–5 per role
- [ ] Best/most relevant bullet first in each role, most relevant role first
- [ ] Each bullet shows technical substance, not a buzzword string
- [ ] Impact or outcome present wherever the user could supply one; metrics near the front
- [ ] No fluff bullets (standups, code reviews, Git, unit tests, "collaborated with the team")
- [ ] Every number is real and came from the user — nothing invented

## Skills

- [ ] Comma separated, ≤3 lines, ordered by importance
- [ ] No soft skills, no proficiency ratings, no IDEs/OSes/LaTeX, no GitHub-as-a-skill
- [ ] `C, C++` style splitting, no `C/C++`
- [ ] Capitalization correct (JavaScript, TypeScript, Node.js, PyTorch, GitHub Actions, …)
- [ ] Everything listed also appears in a bullet, and vice versa

## Language

- [ ] Grammar and spell checked; proper nouns only are capitalized
- [ ] Abbreviations expanded on first use
- [ ] Digits instead of spelled-out numbers
- [ ] No `&`, `/`, or apostrophes inside bullets
- [ ] Consistent tense: past for prior roles, consistent choice for the current role

## Tailoring (when a job description was given)

- [ ] Roles and bullets reordered toward the target role
- [ ] JD vocabulary mirrored where it's honest
- [ ] Content irrelevant to the target trimmed
