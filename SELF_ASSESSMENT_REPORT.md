# Self-assessment — IA#2
Submitted by: 24120090 — Đặng Hồng Minh
Total I claim: 100 / 100

| Criterion | Max | I claim | Evidence |
|---|---|---|---|
| Behaviour | 45 | 45 | All 11 rows of Done means table pass in browser: Row 1 selfCheck 8/8 passed; Row 3-5 keyboard Tab & Enter adds items, disabled button ignored; Row 4 & 6 cart count works with single delegated listener on `#catalogue` (`app.js:34`), Belt adds properly after Load more; Row 7 case-insensitive filter (`scarf`/`SCARF`); Row 8 XSS payload `<img src=x onerror=alert(1)>` rendered safely via `textContent` (`app.js:106`); Row 9 Enter does not reload (`app.js:125`); Row 10 zero console errors; B4 total price calculated correctly (`app.js:55-67`, Cart (3) · 540.000 đ / 680.000 đ with Belt). |
| Scope | 10 | 10 | `git diff --stat 7bfa5d2` (Done means Row 11): only `index.html` and `app.js` changed in code. `style.css` and `check.js` are 100% untouched. |
| Brief | 15 | 15 | `brief.md`: complete, ordered prompts for Part A and Parts B1–B4. Strictly specifies all critical constraints: preserve every `id` and `class`, do not edit `style.css` or `check.js`, one delegated listener on `#catalogue`, `textContent` over `innerHTML` for XSS protection, `preventDefault()` on form submit, and explicit verification steps against the Done means table. |
| AI-LOG.md | 20 | 20 | `AI-LOG.md`: 5 complete entries (Part A, B1, B2, B3, B4). Each entry specifies tool (Gemini 3.8 Flash), exact request, Kept, and specific Changed/Rejected items referencing the Done means table (e.g. rejecting layout `<section>` tags in Part A, rejecting per-button listeners broken by Belt in Row 6, rejecting `innerHTML` to prevent XSS in Row 8, rejecting `keydown` on input in Row 9). |
| Commit history | 10 | 10 | Clean git history with starter commit first (`7bfa5d2 starter`), followed by atomic commits for each part: `14655e1` (Part A), `c080b1a` (B1), `8376e45` (B2), `83bf008` (B3), `f289168` (B4), with clear messages matching the exact diffs. |

## What I did not manage
None. All requirements B1–B4 (including stretch goal B4) have been completely fulfilled and pass every row in the Done means table without errors.

## What I would do differently
None. Applying atomic commits and writing the brief and AI-LOG concurrently during each step kept the workflow clean, verifiable, and well-documented.

