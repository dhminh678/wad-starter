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

