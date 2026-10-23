# AI Assistant Brief

## Part A — Semantic HTML

**Prompt:**
> Please help me refactor `index.html` to use semantic HTML elements instead of generic `<div>` tags, so that all 8 self-checks in `check.js` pass with 8/8.
>
> **Constraints (Strict):**
> 1. Keep every `id` and `class` exactly as they are (`style.css`, `app.js`, and `check.js` query elements by them).
> 2. Do not touch or modify `style.css` or `check.js`.
> 3. Only replace layout `<div>`s that have clear semantic meaning; do not turn every box into `<section>`.
> 4. Requirements from `check.js`:
>    - Landmarks: exactly one `<main>`, plus a `<header>`, a `<nav>`, and a `<footer>`.
>    - Exactly one `<h1>` for the page title.
>    - Headings must not skip levels (h1 -> h2). Product names must be headings (`<h2>`), including inside `<template id="card-template">`.
>    - The catalogue `#catalogue` must be a list (`<ul>`), and every card `.card` must be an `<li>` (including inside `<template id="card-template">`).
>    - The search box must be inside a `<form>` and its input `#q` must have an associated `<label>`.
>    - Every `.button` and `.add` must be a real `<button>` (including inside `<template id="card-template">`), with no inline `onclick` attributes. The sold-out button should use the `disabled` attribute.
> 5. The visual appearance must remain completely identical before and after the change (no styling regressions).
>
> Check: `Session 4 self-check: 8/8 passed` in Console.

## Part B1 — Add to Cart (One Listener)

**Prompt:**
> Please implement task B1 in `app.js` following the specification in the TODO comments:
> - Attach ONE click event listener on the `catalogue` container (event delegation), not on individual buttons.
> - When clicked on an `.add` button, find its card with `event.target.closest('.card')`, get `card.dataset.id`, and increment `cart[id]`.
> - If the button is disabled / sold-out or the click is elsewhere, do nothing.
> - Implement `renderCart()` to sum all quantities with `Object.values(cart)` and write the count into `cartCount` using `textContent`.
>
> **Constraints:**
> - Keep event delegation on `#catalogue` so products added later by "Load more" work automatically.
> - Do not modify `style.css` or `check.js`.
> - Check against Done means rows 4, 5, 6.

