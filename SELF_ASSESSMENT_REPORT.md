# Self-assessment — IA#2
Submitted by: <student ID> — <full name>
Total I claim: 100 / 100

| Criterion | Max | I claim | Evidence |
|---|---|---|---|
| Behaviour | 45 | 45 | All 11 rows of Done means table pass in browser: B1 cart count on catalogue click, B2 filter as you type with XSS-safe textContent, B3 prevent reload on Enter, B4 total price calculation (540.000 đ / 680.000 đ with Belt) |
| Scope | 10 | 10 | `git diff --stat 7bfa5d2`: only `index.html` and `app.js` changed in codebase; `style.css` and `check.js` untouched |
| Brief | 15 | 15 | `brief.md` — full prompts with constraints: preserve all id/class, do not edit style.css/check.js, event delegation, textContent, no page reload |
| AI-LOG.md | 20 | 20 | `AI-LOG.md` — 5 complete entries (Part A, B1, B2, B3, B4) with tool, prompts, Kept, and specific Changed/Rejected entries |
| Commit history | 10 | 10 | 6 atomic commits: starter commit first (`7bfa5d2`), then one commit per part (A, B1, B2, B3, B4) |

## What I did not manage
None. All requirements B1–B4 and stretch goal B4 are completed and pass every check in the Done means table.

## What I would do differently
None. Applying atomic commits and writing the brief and AI-LOG concurrently during each step kept the workflow clean, verifiable, and well-documented.
