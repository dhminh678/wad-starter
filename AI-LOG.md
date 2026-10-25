# AI Interaction Log (`AI-LOG.md`)

## 2026-10-23 — Part A: semantic HTML tags (index.html)
Tool: Gemini 3.8 Flash (Antigravity).
Asked for: Replace generic div tags in index.html with semantic HTML elements while preserving all IDs and classes to pass selfCheck 8/8.
Kept: Landmark elements (<header>, <nav>, <main>, <footer>), <h1> title, <h2> product headings, and <form> search box.
Changed: Converted #catalogue to <ul> and every .card (including inside <template>) to <li> to satisfy the catalogue list check.
Rejected: The assistant's initial suggestion to turn layout boxes (.brand, .price, .stock, .more) into <section>; kept them as <div> since they only do layout.
By hand: Added the native `disabled` attribute to the sold-out Tote bag button so keyboard Tab navigation skips it (Done means row 3 & 4).

## 2026-10-23 — Part B1: add to cart (app.js)
Tool: Gemini 3.8 Flash (Antigravity).
Asked for: Implement B1 in app.js with one delegated click listener on #catalogue and update cartCount in renderCart().
Kept: The event delegation pattern using event.target.closest('.card') and card.dataset.id to increment cart quantities.
Changed: Summed up quantities with Object.values(cart).reduce() and wrote to cartCount via textContent.
Rejected: Any per-button click listeners; an earlier attempt attached listeners on .add which broke when new items were appended by "Load more" (Row 6: Belt).
By hand: Guard check `if (!addButton || addButton.disabled) return;` so clicking the sold-out Tote bag does nothing.

## 2026-10-23 — Part B2: filter as you type (app.js)
Tool: Gemini 3.8 Flash (Antigravity).
Asked for: Implement applyFilter() to filter products by name on input events and update statusBox with match counts.
Kept: Case-insensitive query matching (toLowerCase()), toggling card.hidden, and querying allCards from catalogue.
Changed: Dynamically evaluated allCards.length so status shows "of 8" before Load more and "of 12" after Load more (Row 7).
Rejected: Using innerHTML for the status message; strictly used statusBox.textContent to prevent XSS execution when testing with `<img src=x onerror=alert(1)>` (Row 8).
By hand: The exact message template strings for empty query, matching count, and non-matching query.

## 2026-10-23 — Part B3: prevent search form reload (app.js)
Tool: Gemini 3.8 Flash (Antigravity).
Asked for: Stop the search form from reloading the page when pressing Enter in the search input.
Kept: Attaching a submit listener to searchInput.form and calling event.preventDefault().
Changed: Added applyFilter() call right after preventDefault() to refresh search results immediately upon form submission.
Rejected: Listening for keydown (Enter) on the input field instead of the form's submit event.
By hand: Verified in browser that URL does not get `?q=cap` and cart count is preserved after pressing Enter (Row 9).

## 2026-10-23 — Part B4: calculate cart total price (app.js)
Tool: Gemini 3.8 Flash (Antigravity).
Asked for: Calculate total price of items in cart and display formatted VND currency in cartTotal.
Kept: Iterating cart items, looking up card.dataset.price, and formatting total with toLocaleString('vi-VN') + ' đ'.
Changed: Wrapped string conversion with Number(card.dataset.price) to prevent string concatenation bugs.
Rejected: Computing price from a static array; queried from catalogue DOM so dynamically added items (Belt) are priced correctly.
By hand: Resetting cartTotal.textContent to empty string when cart is empty (totalCount === 0).

## 2026-10-25 — Testing & verification: 11 rows of Done means table
Tool: Gemini 3.8 Flash (Antigravity).
Asked for: Verify all 11 rows of the Done means table in README.md via browser interaction and script inspection to ensure full compliance before submission.
Kept: Systematically testing every row: console 8/8 check (Row 1), visual comparison (Row 2), keyboard Tab focus ring (Row 3), cart count on T-shirt and disabled Tote (Row 4), Enter on focused button (Row 5), dynamic Load more + Add on Belt (Row 6), case-insensitive search with 'scarf'/'SCARF' (Row 7), XSS string handling with literal rendering (Row 8), Enter on search form without reload (Row 9), clean console with 0 errors (Row 10), and git scope check (Row 11).
Changed: Adjusted the verification test order so that Row 7 matches "Showing 1 of 12 products" strictly after Row 6 clicks "Load more" (as noted in README note: before Load more it displays "of 8").
Rejected: Assistant's suggestion to mock DOM events or rewrite check.js/style.css to bypass checks; insisted on running live browser interactions against the untouched check.js and style.css files.
By hand: Checked the orange focus ring visually on keyboard navigation (Row 3), confirmed the URL query string stayed empty on Enter (Row 9), and ran `git diff --stat 7bfa5d2` to confirm exactly zero changes to check.js and style.css (Row 11).
