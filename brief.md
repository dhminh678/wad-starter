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
