# Self-assessment — IA#2
Submitted by: 24120090 — Đặng Hồng Minh
Total I claim: 100 / 100

| Criterion | Max | I claim | Evidence |
|---|---|---|---|
| Behaviour | 45 | 45 | All 11 rows of Done means table pass in browser: B1 cart count on catalogue click, B2 filter as you type with XSS-safe textContent, B3 prevent reload on Enter, B4 total price calculation (540.000 đ / 680.000 đ with Belt) |
| Scope | 10 | 10 | `git diff --stat 7bfa5d2`: only `index.html` and `app.js` changed in codebase; `style.css` and `check.js` untouched |
| Brief | 15 | 15 | `brief.md` — full prompts with constraints: preserve all id/class, do not edit style.css/check.js, event delegation, textContent, no page reload |
| AI-LOG.md | 20 | 20 | `AI-LOG.md` — 6 complete entries (Part A, B1, B2, B3, B4, Done means verification) with tool, prompts, Kept, and specific Changed/Rejected entries |
| Commit history | 10 | 10 | 6 atomic commits: starter commit first (`7bfa5d2`), then one commit per part (A, B1, B2, B3, B4) |

## What I did not manage
All required specifications (B1–B4, stretch goal B4, and 11/11 Done means rows) are fully met and verified. However, some advanced production features were out of scope and not implemented:
- **Cart persistence across page reloads**: Cart state resets when refreshing the page because `localStorage` / `sessionStorage` was not part of the starter specification.
- **Cart item removal/decrement**: The interface only provides "Add" buttons without a way to decrease item quantities or empty the cart.
- **Debounced search**: `applyFilter()` executes synchronously on every keystroke (`input` event); while instantaneous for 8–12 items, a debounced handler would be preferable for large datasets.
- **Accent-insensitive Vietnamese search**: Matching is case-insensitive, but searching without accents (e.g., `ao so mi` for `Áo sơ mi`) is not supported without Unicode NFD normalization.

## What I would do differently
- **State negative constraints upfront in the brief**: In Part A, the assistant initially suggested converting pure layout wrappers (`.brand`, `.price`, `.stock`) into `<section>`. Providing strict negative constraints ("do not change layout-only divs") in the very first prompt avoided corrective back-and-forth.
- **Decouple cart calculations from DOM querying**: In B4, prices are looked up directly from `card.dataset.price` in the DOM on each render. In a larger application, building a lightweight in-memory product map upon page load would be cleaner and avoid repeated `querySelector` calls.
- **Automate the Done means test suite early**: Rather than manually testing all 11 browser check rows through DevTools console and UI clicks after each part, writing a small automated headless runner early on would speed up regression testing.

