# Self-Assessment Report — IA#2: Dynamic HTML

- **Student Name:** [Your Name / Điền họ và tên]
- **Student ID:** [Your Student ID / Điền MSSV]
- **Repository / Directory:** IA2/starter
- **Total Claimed Points:** 100 / 100

---

## Rubric Breakdown and Evidence

| # | Criterion | Max Points | Claimed Points | Evidence & Verification |
|---|---|---|---|---|
| **1** | **Behaviour (B1–B4)** | 45 | 45 | All 11 rows of the **Done means** table verified in browser: <br>• **B1**: Single event listener on `#catalogue` (`app.js`), `cartCount` updates correctly; sold-out Tote bag does nothing (Row 4). Tab & Enter adds items (Row 5). <br>• **B2**: Case-insensitive filter (`scarf` vs `SCARF` in Row 7); all 12 cards restored on clear; XSS payload `<img src=x onerror=alert(1)>` rendered verbatim via `textContent` without alert or broken images (Row 8). <br>• **B3**: Search form submit event intercepted with `preventDefault()`; Enter does not reload or alter address bar (`?q=cap`), cart count preserved (Row 9). <br>• **B4 (Stretch)**: Total price calculated via `dataset.price` using `Number()` and formatted with `toLocaleString('vi-VN') + ' đ'`; displays correctly with initial items and newly loaded Belt (`Cart (3) · 540.000 đ`). |
| **2** | **Scope** | 10 | 10 | Verified by `git diff --stat 7bfa5d2` (starter commit): only `index.html` and `app.js` differ in code. `style.css` and `check.js` are 100% untouched. |
| **3** | **The Brief (`brief.md`)** | 15 | 15 | `brief.md` documents complete, ordered prompts for Part A and Parts B1–B4 with all critical constraints: preserving all `id` and `class` attributes, prohibiting edits to `style.css` and `check.js`, requiring event delegation on `#catalogue`, mandating `textContent` over `innerHTML`, and testing against the Done means table. |
| **4** | **`AI-LOG.md`** | 20 | 20 | `AI-LOG.md` contains dedicated entries for Part A and every subtask (B1, B2, B3, B4). Each entry specifies the tool, exact request, what was kept, and what was changed or rejected (e.g. rejecting `innerHTML` to avoid XSS, ignoring clicks on disabled buttons, avoiding unnecessary `<section>` tags). |
| **5** | **Commit History** | 10 | 10 | Clean, step-by-step git history with starter commit first, followed by one commit per part: <br>• `7bfa5d2 starter` <br>• `14655e1 Part A: semantic HTML and self-check 8/8` <br>• `c080b1a B1: add to cart with single event listener` <br>• `8376e45 B2: filter as you type with textContent` <br>• `83bf008 B3: prevent search form reload on enter` <br>• `f289168 B4: calculate and display cart total price` |

**Total:** 100 / 100

---

## What I Did Not Manage / Gaps
- None. All requirements B1, B2, B3, and stretch goal B4 have been completely fulfilled and pass every row in the Done means table without any errors.
