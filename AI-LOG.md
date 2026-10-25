# AI Interaction Log (`AI-LOG.md`)

## 2026-10-23 — Part A: semantic HTML tags (index.html)
- **Tool:** Gemini 3.8 Flash (Antigravity).
- **Asked for:** Replace generic `<div>` tags in `index.html` with semantic HTML elements while preserving all IDs and classes to pass `check.js` 8/8.
- **Kept:** Landmark elements (`<header>`, `<nav>`, `<main>`, `<footer>`), `<h1>` title, `<h2>` product names (including inside `<template id="card-template">`), `<ul>` catalogue with `<li>` cards, search `<form>` with `<label for="q">`, and `<button>` elements.
- **Changed:** Added native `disabled` attribute to the sold-out Tote bag button so keyboard Tab navigation skips it (Done means row 3 & 4).
- **Rejected:** The assistant's initial suggestion to turn layout boxes (`.brand`, `.price`, `.stock`, `.more`) into `<section>`; instructed assistant to keep them as `<div>` since they only serve visual layout (README: "if the assistant turned every one into <section>, say no").
- **By hand:** Verified visual layout in browser against starter screenshot to confirm zero styling regressions (Done means row 2).
- **Checked:** Row 1: `Session 4 self-check: 8/8 passed`; Row 2: visual appearance identical; Row 3: Tab navigation skips sold-out Tote bag.

## 2026-10-23 — Part B1: add to cart (app.js)
- **Tool:** Gemini 3.8 Flash (Antigravity).
- **Asked for:** Implement B1 in `app.js` with ONE click listener on `#catalogue` (event delegation), increment `cart[id]`, update `cartCount` via `textContent` in `renderCart()`.
- **Kept:** Event delegation pattern on `#catalogue` using `event.target.closest('.card')` and `card.dataset.id`; summing items via `Object.values(cart).reduce((sum, n) => sum + n, 0)`; updating `cartCount.textContent`.
- **Changed:** Added guard condition `if (!addButton || addButton.disabled) return;` so clicking the disabled Tote bag or outside `.add` does nothing.
- **Rejected:** Nothing went wrong — prompt specified a single event listener on `#catalogue` upfront. Verified that newly appended cards from "Load more" (Belt) work automatically without re-attaching listeners.
- **By hand:** Tested clicking interactions on initial cards and dynamically loaded cards.
- **Checked:** Row 4: T-shirt x2 + Tote bag -> `Cart (2)`; Row 5: Tab to Add + Enter -> count `3`; Row 6: "Load more" + Add on Belt -> count `4`.

## 2026-10-23 — Part B2: filter as you type (app.js)
- **Tool:** Gemini 3.8 Flash (Antigravity).
- **Asked for:** Implement `applyFilter()` in `app.js`: case-insensitive name matching on `input` event, toggle `card.hidden`, update `statusBox` via `textContent`.
- **Kept:** Case-insensitive query matching with `toLowerCase()`, toggling `card.hidden`, registering `applyFilter` on search input's `input` event.
- **Changed:** Dynamically counted `allCards.length` from `#catalogue` rather than hardcoding 8, so status displays "of 8" initially and "of 12" after "Load more".
- **Rejected:** Any usage of `innerHTML` for `statusBox`; strictly enforced `statusBox.textContent` to prevent XSS execution when testing `<img src=x onerror=alert(1)>`.
- **By hand:** Verified message template strings: empty string for blank query, `Showing X of Y products` for matches, `No products match "<rawQuery>"` for no matches.
- **Checked:** Row 7: `scarf` -> `Showing 1 of 12 products`; `SCARF` -> identical 1 card; clear input -> all 12 cards restored, status line empty. Row 8: typed `<img src=x onerror=alert(1)>` -> displayed literal string, 0 alerts, 0 broken images.

## 2026-10-23 — Part B3: prevent search form reload (app.js)
- **Tool:** Gemini 3.8 Flash (Antigravity).
- **Asked for:** Intercept search form submit in `app.js` with `event.preventDefault()` to stop page reload and URL query params, then call `applyFilter()`.
- **Kept:** Attaching `submit` listener to `searchInput.form` and calling `event.preventDefault()`, followed by `applyFilter()`.
- **Changed:** Added guard check `if (searchInput.form)` before adding listener.
- **Rejected:** Listening for `keydown` (Enter) on the input field instead of the form's `submit` event, ensuring submission works both via Enter key and clicking Search button.
- **By hand:** Checked browser address bar to verify URL does not get `?q=cap` and cart count is preserved after pressing Enter.
- **Checked:** Row 9: Typed `cap` and pressed Enter -> address bar unchanged, cart count intact.

## 2026-10-23 — Part B4: calculate cart total price (app.js)
- **Tool:** Gemini 3.8 Flash (Antigravity).
- **Asked for:** Implement stretch goal B4 in `app.js`: calculate cart total price from `card.dataset.price`, format with `toLocaleString('vi-VN') + ' đ'`, display in `cartTotal`.
- **Kept:** Querying cards from `#catalogue` by `data-id`, converting `card.dataset.price` using `Number()`, formatting with `total.toLocaleString('vi-VN') + ' đ'`, and displaying ` · <total>` in `cartTotal`.
- **Changed:** Handled empty cart display: resetting `cartTotal.textContent = ''` when `totalCount === 0`.
- **Rejected:** Computing price from a static array; queried `dataset.price` from DOM cards so newly loaded cards (Belt at 140.000 đ) are priced accurately.
- **By hand:** Verified currency punctuation (dot separator `540.000 đ` according to Vietnamese locale `vi-VN`).
- **Checked:** Added 3 T-shirts (180.000 đ each) -> `Cart (3) · 540.000 đ`; clicked "Load more" and added Belt (140.000 đ) -> `Cart (4) · 680.000 đ`.

## 2026-10-25 — Testing & verification: 11 rows of Done means table
- **Tool:** Gemini 3.8 Flash (Antigravity).
- **Asked for:** Run full verification checklist for all 11 rows of the Done means table in `README.md` and check scope compliance before final packaging.
- **Kept:** Systematically verifying every row 1–11: Row 1 (selfCheck 8/8), Row 2 (visual match), Row 3 (keyboard Tab focus & ring), Row 4 (cart count with sold-out disabled button), Row 5 (Enter key on Add), Row 6 (Load more + Belt), Row 7 (scarf/SCARF search), Row 8 (XSS string immunity), Row 9 (search Enter no-reload), Row 10 (0 console errors), Row 11 (git scope diff).
- **Changed:** Adjusted verification test order so Row 7 is tested after Row 6 (ensuring catalogue has 12 items as specified in the README note).
- **Rejected:** Assistant's suggestion to mock DOM events or rewrite `check.js`/`style.css` to fake pass results; strictly conducted live browser checks against the untouched original check and style files.
- **By hand:** Checked orange focus ring visually on keyboard navigation (Row 3), confirmed URL query string stayed empty on Enter (Row 9), and ran `git diff --stat 7bfa5d2` to confirm zero changes to `check.js` and `style.css` (Row 11).
- **Checked:** 11/11 Done means rows passed; 0 console errors; scope check clean.
