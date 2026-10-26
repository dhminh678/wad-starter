# Self-assessment — IA#2
Submitted by: 24120090 — Đặng Hồng Minh
Total I claim: 92 / 100

| Criterion | Max | I claim | Evidence |
|---|---|---|---|
| Behaviour | 45 | 42 | All 11 rows of Done means table pass in live browser: Row 1 selfCheck 8/8 (`check.js:100`); Rows 3–5 keyboard Tab & Enter adds items, disabled button skipped (`index.html:61`, `app.js:36`); Rows 4 & 6 single delegated listener on `#catalogue` (`app.js:34`), Belt adds after Load more; Row 7 case-insensitive filter (`scarf`/`SCARF`, `app.js:98`); Row 8 XSS payload `<img src=x onerror=alert(1)>` rendered literally via `textContent` (`app.js:106`); Row 9 Enter does not reload (`app.js:125-128`); Row 10 zero console errors; B4 total price calculated correctly (`app.js:55-67`, `Cart (3) · 540.000 đ` and `Cart (4) · 680.000 đ`). Claiming 42 within the 40–45 band as conservative calibration for purely in-memory cart state without persistence across page reloads. |
| Scope | 10 | 10 | `git diff --stat 7bfa5d2`: only `index.html` and `app.js` differ in project code; `style.css` and `check.js` are 100% untouched. Starter markdown docs (`PART_A.md`, `README.md`, `REQUIREMENTS.md`) are untouched. Required documentation (`brief.md`, `AI-LOG.md`, `SELF_ASSESSMENT_REPORT.md`) are provided as specified in rubric. |
| Brief | 15 | 15 | `brief.md` — complete, ordered prompts for Part A, B1–B4, and Verification. Strictly specifies all constraints: preserve all `id`/`class`, do not edit `style.css`/`check.js`, one delegated listener on `#catalogue`, `textContent` over `innerHTML`, `preventDefault()` on form submit, and explicit row-by-row checks. |
| AI-LOG.md | 20 | 15 | `AI-LOG.md` — 6 structured entries (Part A, B1, B2, B3, B4, Verification) with Tool, Asked for, Kept, Changed, Rejected, By hand, and Checked. Records genuine assistant mistakes and corrections (rejecting `<section>` for layout boxes in Part A; rejecting mock/file edits in verification), row verification outcomes, and consistency with git history. Claiming 15 as conservative self-assessment within rubric tier because several prompts provided strict negative constraints upfront resulting in fewer assistant errors to log. |
| Commit history | 10 | 10 | Clean git history with starter commit first (`7bfa5d2 starter`), followed by atomic commits for each part: `14655e1` (Part A), `c080b1a` (B1), `8376e45` (B2), `83bf008` (B3), `f289168` (B4), with clear messages matching diffs. |

## What I did not manage
All required specifications (B1–B4, stretch goal B4, and 11/11 Done means rows) are fully met and verified. However, some advanced production features were out of scope and not implemented:
- **Cart persistence across page reloads**: Cart state resets when refreshing the page because `localStorage` / `sessionStorage` was not part of the starter specification.
- **Cart item removal/decrement**: The interface only provides "Add" buttons without a way to decrease item quantities or empty the cart.
- **Debounced search**: `applyFilter()` executes synchronously on every keystroke (`input` event); while instantaneous for 8–12 items, a debounced handler would be preferable for large datasets.
- **Accent-insensitive Vietnamese search**: Matching is case-insensitive, but searching without accents (e.g., `ao so mi` for `Áo sơ mi`) is not supported without Unicode NFD normalization.

## What I would do differently
- **State negative constraints upfront in the brief**: In Part A, the assistant initially suggested converting pure layout wrappers (`.brand`, `.price`, `.stock`) into `<section>`. Providing strict negative constraints ("do not change layout-only divs into section") in the very first prompt avoids an extra corrective prompt.
- **Decouple cart calculations from DOM querying**: In B4, prices are looked up directly from `card.dataset.price` in the DOM on each render. In a larger application, building a lightweight in-memory product map upon page load would be cleaner and avoid repeated `querySelector` calls.
- **Automate the Done means test suite early**: Rather than manually testing all 11 browser check rows through DevTools console and UI clicks after each part, writing a small automated headless runner early on would speed up regression testing.
