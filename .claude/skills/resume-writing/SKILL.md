---
name: resume-writing
description: Write, edit, and review this LaTeX resume using the r/EngineeringResumes wiki standards (US/Canada engineering resumes). Use whenever resume.tex is being changed — rewriting bullet points, adding or reordering a role, tailoring to a job description, trimming to one page, fixing skills/education/contact sections, or reviewing the resume before sending it out.
---

# Resume writing (r/EngineeringResumes standards)

Rules distilled from the [r/EngineeringResumes wiki](https://www.reddit.com/r/EngineeringResumes/wiki/index/),
the [Ultimate Guide to SWE Bullet Points](https://archive.ph/Xmdqt), and
[36 Resume Rules for Software Engineers](https://www.nicksingh.com/posts/36-resume-rules-for-software-engineers).
They target **US/Canada** engineering resumes. They are strong defaults, not laws — say so when breaking one.

This repo holds a single LaTeX resume: `resume.tex` → `resume.pdf`.

## Workflow

1. **Read `resume.tex` first.** Never rewrite from scratch; edit in place, preserving the macros
   (`\resumeSubheading`, `\resumeItem`, `\resumeItemListStart/End`).
2. **Ask for raw material, don't invent it.** Metrics, scale, team size, and outcomes must come from the
   user. Never fabricate numbers, users, revenue, or latency figures. If a bullet needs a number the user
   hasn't given, write the bullet without it and ask.
3. **Tailor when a job description is supplied.** Reorder roles/bullets by relevance, mirror the JD's
   vocabulary where it's honest, cut what doesn't support the target role.
4. **Apply the rules** in `references/rules.md` (structure, sections, formatting) and
   `references/bullet-points.md` (the part people get wrong).
5. **Build and verify one page** after every content change — this is a hard invariant, see below.
6. **Review before finishing** with `references/review-checklist.md`. Report any rule the current file
   still breaks rather than silently leaving it.

## The one-page invariant

**This resume is always exactly one page.** Not "usually", not "unless the content is good" — always.
It is the single constraint that outranks every other preference here, including anything the user asked
for earlier in the conversation. Never hand back a two-page build, and never end a turn without checking.

After every change that touches content:

```
pnpm pdf && pdfinfo resume.pdf | grep Pages
```

If it reads `Pages: 2`, the work is not done. Fix it in this order, stopping as soon as it fits:

1. **Cut the weakest bullet.** The one with no metric, no named technology, and a trailing list of
   directional claims ("improving speed, quality, and consistency"). There is almost always one.
2. **Merge two overlapping bullets** in the same role into a single stronger one.
3. **Tighten wording** — drop adverbs and hedges, collapse a 3-line bullet to 2, a 2-line to 1.
4. **Drop the oldest role's weakest content**, then the oldest role entirely if it no longer earns space.
5. **Cut a whole section** that doesn't support the target role.

Never buy space by changing the geometry. The following are off limits:
font size below 10.5pt (or removing `\small` scaling as a *space* tactic), margins below 0.4in,
`\vspace` beyond the values already in the macros, two columns, or line spacing below 1.07.
A cramped one-pager reads worse than a well-edited one — the fix is always less content, never smaller type.

**Adding content is a trade, not an addition.** Before adding a bullet, name the bullet it replaces.
If the user asks for something that doesn't fit, add it, cut the weakest thing to pay for it, rebuild,
and tell them explicitly what you cut and why — don't silently drop it, and don't silently overflow.

The only exception is 10+ years of experience or a genuine senior/staff+ profile, where two pages are
defensible. That is not the case for this resume today; treat it as one page until the user says otherwise.

## The rules that matter most

**Purpose.** A resume is a 30-second elevator pitch whose only job is to get an interview. Optimize for
skimmability first, aesthetics never.

**Layout.** Single column. No icons, images, graphics, or multiple columns. Bullet points, not paragraphs.
Comma-separated skills. Black text, 10.5pt+, no justified text, margins ≥ 0.4in. One page.

**Section order** (this resume is a mid-level engineer with full-time experience):
`Experience > Skills > Education` or `Skills > Experience > Education`. Students/new grads lead with
Education. No summary/objective unless senior/staff+, career changer, or explaining a gap. No references section.

**Bullet points.** Each one starts with a strong past-tense action verb and follows STAR / XYZ / CAR:
what you built, the technical challenge, the impact. 1–2 lines, aim for one sentence, best bullet first,
3–5 per role. No personal pronouns, no trailing periods, no "responsible for", no `utilize`/`spearheaded`/
`leveraged`. Show technical specifics, not a buzzword string — see `references/bullet-points.md` for the
good/bad examples and verb lists.

**Skills.** Comma-separated, ≤3 lines, ordered by importance, grouped into categories if useful. Only things
you could interview in and that appear in your bullets. No soft skills, no proficiency ratings, no IDEs,
no OSes, no GitHub-as-a-skill (use "Git"). Spelling matters: `JavaScript`, `TypeScript`, `Node.js`, `PyTorch`,
`GitHub Actions` — full list in `references/rules.md`.

**Contact line.** Name, one email, portfolio, GitHub — plain text, no `https://www.`, no "Email:" prefixes,
no colored/underlined links. The wiki considers phone number and LinkedIn unnecessary; keep them only if the
user wants them. No address, no photo, no personal details that invite bias (age, gender, marital status,
nationality, religion).

**Dates.** `Mar 2022 – Present`, en dash with spaces around it (`--` in LaTeX), right-aligned, no abbreviated
years, no digit months, proper month abbreviations (Jan, Feb, Mar, Apr, May, June, July, Aug, Sept, Oct, Nov, Dec).

## Known deviations in this resume

Flag these when relevant; don't "fix" them unprompted — some are deliberate:

- `\textbf{}` emphasis inside bullet points — the wiki says don't bold keywords within bullets (distracting).
- Colored hyperlinks (`RoyalBlue` in the `hyperref` setup) — the wiki wants plain black, print-safe text.
- Phone number and LinkedIn/X links in the header — allowed, just not recommended.
- Skills list contains soft/process items (PR Reviews, Mentorship) and editors (Cursor, Claude Code), which
  the wiki excludes from a skills section.
- Most bullets carry no metric. The indoor-positioning accuracy bullet is the model to imitate.

## References

- `references/rules.md` — full rule set by section (formatting, contact, experience, education, skills, projects, seniority).
- `references/bullet-points.md` — STAR/XYZ/CAR, action verbs, banned words, annotated good vs bad bullets, sample bullets.
- `references/latex-conventions.md` — this repo's macros, build/watch commands, one-page tactics, LaTeX escaping.
- `references/review-checklist.md` — final pass, run it before declaring the resume done.
