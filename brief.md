# AI Assistant Brief

## Part A — Semantic HTML

**Prompt 1 (Initial):**
> Please help me refactor `index.html` to replace generic `<div>` tags with appropriate semantic HTML elements so that the self-check in `check.js` passes with 8/8.
>
> **Constraints:**
> 1. Keep every `id` and `class` exactly as they are (`style.css`, `app.js`, and `check.js` query elements by them).
> 2. Do not touch or modify `style.css` or `check.js`.
> 3. Visual appearance must remain completely identical before and after the change (no styling regressions).
> 4. Ensure elements match accessibility and semantic guidelines (landmarks, heading hierarchy, list elements, form controls, real buttons).

**Prompt 2 (Follow-up / Correction):**
> The previous response suggested turning layout boxes (`.brand`, `.price`, `.stock`, `.more`) into `<section>` tags.
> Please keep those pure layout wrapper boxes as `<div>` elements — only use `<section>` or other semantic tags where there is distinct standalone content or true semantic meaning.
>
> Requirements from `check.js`:
> - Landmarks: exactly one `<main>`, plus `<header>`, `<nav>`, and `<footer>`.
> - Exactly one `<h1>` for the page title. Product names must be `<h2>` (including inside `<template id="card-template">`), with no skipped levels.
> - Catalogue `#catalogue` must be `<ul>`, and every `.card` must be `<li>` (including inside `<template>`).
> - Search box must be inside a `<form>` and its input `#q` must have an associated `<label for="q">`.
> - Every `.button` and `.add` must be a real `<button>` (including inside `<template>`), with no inline `onclick`. Add the native `disabled` attribute to the sold-out Tote bag button.

---

## Part B1 — Add to Cart (One Listener)

**Prompt:**
> Please implement task B1 in `app.js` following the specification in the TODO comments:
> - Attach ONE click event listener on the `catalogue` container (event delegation), not on individual buttons.
> - When clicked on an `.add` button, find its card with `event.target.closest('.card')`, get `card.dataset.id`, and increment `cart[id]`.
> - If the button is disabled / sold-out or the click is elsewhere, do nothing (`if (!addButton || addButton.disabled) return;`).
> - Implement `renderCart()` to sum all quantities with `Object.values(cart).reduce(...)` and write the count into `cartCount` using `textContent`.
>
> **Constraints:**
> - Keep event delegation on `#catalogue` so products added later by "Load more" work automatically.
> - Do not modify `style.css` or `check.js`.
> - Check against Done means rows 4, 5, 6.

---

## Part B2 — Filter as You Type

**Prompt:**
> Please implement task B2 in `app.js` following the specification in the TODO comments:
> - Implement `applyFilter()`:
>   1. Read `searchInput.value`, `trim()` it, and convert to lower case with `toLowerCase()`.
>   2. For every `.card`: set `card.hidden = true` unless its `.name` text contains the query (case-insensitive).
>   3. Write status message into `statusBox` using `textContent` (NEVER `innerHTML`):
>      - Empty query -> `''` (empty string, unhide all cards).
>      - Some cards match -> `'Showing X of Y products'` (where Y is dynamically counted from `#catalogue`).
>      - Nothing matches -> `'No products match "<user-typed-query>"'`.
> - Attach `applyFilter` to the `'input'` event of `searchInput`.
>
> **Constraints:**
> - NEVER use `innerHTML` when displaying user input (must prevent XSS).
> - Test against Done means row 7 (`scarf`, `SCARF`, clear) and row 8 (`<img src=x onerror=alert(1)>`).

---

## Part B3 — Prevent Search Form Reload

**Prompt:**
> Please implement task B3 in `app.js` following the specification in the TODO comments:
> - Listen for the `'submit'` event on `searchInput.form`.
> - Call `event.preventDefault()` to stop the browser from reloading the page and appending `?q=...` to the address bar.
> - Call `applyFilter()` to ensure search results update on submit.
>
> **Constraints:**
> - Preserves client state (cart contents and count) when pressing Enter.
> - Test against Done means row 9.

---

## Part B4 (Stretch) — Calculate and Display Cart Total Price

**Prompt:**
> Please implement task B4 (stretch goal) in `app.js`:
> - In `renderCart()`, calculate the total price of all items currently in `cart`.
> - Query `card.dataset.price` from the cards in `#catalogue` and convert to number with `Number()` to avoid string concatenation.
> - Format the total as Vietnamese currency: `total.toLocaleString('vi-VN') + ' đ'`.
> - Write `' · ' + formattedTotal` into `cartTotal` using `textContent` when items exist; write `''` when cart is empty.
>
> **Constraints:**
> - Correctly look up prices for both initial cards and dynamically loaded cards (e.g. Belt).
> - Test against Done means row 4 and README example: `Cart (3) · 540.000 đ`.

---

## Verification — 2026-10-25

**Prompt:**
> Please help me verify all 11 rows of the Done means table in `README.md` against the current implementation in `index.html` and `app.js`:
> 1. Row 1: Session 4 self-check 8/8 passed in Console.
> 2. Row 2: Visual match with original starter layout.
> 3. Row 3: Keyboard Tab navigation reaches every active Add button and Search, skipping the sold-out Tote bag. Orange focus ring visible.
> 4. Row 4: T-shirt x2 + Tote bag click -> Cart shows 2.
> 5. Row 5: Tab to Add + Enter -> Cart count increments by 1.
> 6. Row 6: Click "Load more", then click Add on Belt -> Cart count increments by 1.
> 7. Row 7: Search `scarf`, then `SCARF` -> 1 card shown with "Showing 1 of 12 products"; clear input -> all 12 cards restored and status empty.
> 8. Row 8: Search `<img src=x onerror=alert(1)>` -> renders verbatim with textContent, no alert, no broken image.
> 9. Row 9: Type `cap` and press Enter -> page does not reload, URL stays clean without `?q=cap`, cart count preserved.
> 10. Row 10: Check Console -> 0 red errors.
> 11. Row 11: Scope verification -> `git diff --stat 7bfa5d2` confirms only `index.html` and `app.js` changed in codebase, with `style.css` and `check.js` untouched.
>
> **Constraints:**
> - Do not mock DOM events or modify `check.js`/`style.css` to bypass checks.
> - Perform tests in real browser environment against the actual files.
> - Ensure Row 7 is verified after Row 6 so the catalogue contains 12 products as specified in README note.
