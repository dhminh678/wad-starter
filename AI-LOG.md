# AI Interaction Log (`AI-LOG.md`)

## Part A: Semantic HTML (`index.html`)

- **Tool:** Gemini 3.8 Flash (Antigravity Assistant)
- **Request:**
  "Refactor `index.html` to replace generic `<div>` elements with appropriate semantic HTML tags. Constraints: Keep all `id` and `class` attributes intact, do not edit `style.css` or `check.js`, and pass all 8 checks in `check.js` (8/8) without altering visual design."
- **Kept:**
  - Landmarks: `<header class="toolbar">`, `<nav class="menu">`, `<main class="page">`, and `<footer class="footer">`.
  - Headings: `<h1 class="title">` for the page title, and `<h2 class="name">` for all product titles (including inside `<template id="card-template">`).
  - List structure: `<ul class="catalogue" id="catalogue">` and `<li class="card">` (including inside `<template>`).
  - Search accessibility: Wrapped search controls inside `<form class="search" role="search">` and added `<label class="search-label" for="q">`.
  - Buttons: Replaced `.button` and `.button.add` with `<button type="button">` and `<button type="submit">`, with `disabled` attribute on sold-out item.
- **Changed / Rejected:**
  - Rejected converting layout wrappers like `.brand`, `.price`, `.stock`, and `.more` into `<section>` or `<article>` tags; kept them as `<div>` because they are purely for layout/styling.
  - Ensured the sold-out Tote bag button has the native `disabled` attribute in addition to `.disabled` class so keyboard Tab navigation skips it (Row 3 & 4 of Done means).
- **Check Results:**
  - `check.js`: 8/8 passed.
  - Visual check: No change in layout or appearance compared to starter.
  - Git diff: Only `index.html` changed in the codebase (plus `brief.md` and `AI-LOG.md`).

## Part B1: Add to Cart (`app.js`)

- **Tool:** Gemini 3.8 Flash (Antigravity Assistant)
- **Request:**
  "Implement task B1 in `app.js`: Add to cart with ONE listener on `#catalogue`. Read `dataset.id` from `event.target.closest('.card')`, increment `cart[id]`, and call `renderCart()` to update `cartCount` using `textContent`."
- **Kept:**
  - Event delegation listener placed directly on `catalogue` element.
  - Cart item counter summation using `Object.values(cart).reduce(...)`.
  - Updating `#cart-count` via `textContent`.
- **Changed / Rejected:**
  - Added check `if (!addButton || addButton.disabled) return;` to explicitly reject clicks on sold-out products (Row 4: Tote bag must not increment cart count).
  - Verified that using event delegation on `#catalogue` rather than attaching listeners to each button allows newly appended cards from "Load more" (Row 6: Belt) to work without reattaching listeners.
- **Check Results:**
  - Row 4: Added T-shirt twice, clicked sold-out Tote bag -> Cart showed `2`.
  - Row 5: Tabbed to Add button and pressed Enter -> Count incremented to `3`.
  - Row 6: Clicked "Load more", clicked Add on Belt -> Count incremented to `4`.

## Part B2: Filter as You Type (`app.js`)

- **Tool:** Gemini 3.8 Flash (Antigravity Assistant)
- **Request:**
  "Implement task B2 in `app.js`: Filter cards as user types in `#q`. Convert input to lowercase, hide non-matching cards using `card.hidden`, update `statusBox` using `textContent`, and register listener on input event."
- **Kept:**
  - Case-insensitive comparison between `card.querySelector('.name').textContent` and search query.
  - Setting `card.hidden = false` for all cards and clearing status text when query is empty.
  - Dynamically counting `allCards.length` from `#catalogue` to handle both initial 8 products and 12 products after "Load more".
- **Changed / Rejected:**
  - Strictly insisted on using `statusBox.textContent` instead of `statusBox.innerHTML` to prevent script execution when testing XSS strings (Row 8: `<img src=x onerror=alert(1)>`).
  - Rendered `rawQuery` verbatim inside quotes for the not-found message: `No products match "${rawQuery}"`.
- **Check Results:**
  - Row 7: Typed `scarf` -> `Showing 1 of 12 products`. Typed `SCARF` -> identical result. Cleared input -> all 12 cards restored, status line empty.
  - Row 8: Typed `<img src=x onerror=alert(1)>` -> displayed literal string `No products match "<img src=x onerror=alert(1)>"` without alert or broken image.

## Part B3: Prevent Form Reload (`app.js`)

- **Tool:** Gemini 3.8 Flash (Antigravity Assistant)
- **Request:**
  "Implement task B3 in `app.js`: Intercept form submit event on `searchInput.form`, call `event.preventDefault()`, and invoke `applyFilter()`."
- **Kept:**
  - Checking `searchInput.form` existence.
  - Calling `event.preventDefault()` to cancel native GET submission.
  - Triggering `applyFilter()` immediately upon submit.
- **Changed / Rejected:**
  - Confirmed that form submission was intercepted without causing any page reloads or URL query parameters (`?q=...`), keeping in-memory cart state completely intact.
- **Check Results:**
  - Row 9: Typed `cap` and pressed Enter in search box -> Page did NOT reload, URL remained unchanged, and cart count remained unchanged.

## Part B4 (Stretch): Cart Total Price Calculation (`app.js`)

- **Tool:** Gemini 3.8 Flash (Antigravity Assistant)
- **Request:**
  "Implement stretch task B4 in `app.js`: Calculate the total cart price from `card.dataset.price`, convert dataset strings using `Number()`, format with `toLocaleString('vi-VN') + ' đ'`, and display in `cartTotal`."
- **Kept:**
  - Converting `dataset.price` string via `Number()` to prevent string concatenation bugs.
  - Using `total.toLocaleString('vi-VN') + ' đ'` for standard Vietnamese currency formatting.
  - Setting `cartTotal.textContent = ''` when `totalCount === 0`.
- **Changed / Rejected:**
  - Ensured lookup uses `catalogue.querySelector(`.card[data-id="${id}"]`)` so price is correctly found even if cards are filtered/hidden, and handles dynamically added cards (e.g. Belt at 140.000 đ) after "Load more".
- **Check Results:**
  - Added 3 T-shirts (180.000 đ each) -> Cart header displayed `Cart (3) · 540.000 đ`.
  - Added Belt (140.000 đ) -> Header updated to `Cart (4) · 680.000 đ`.




