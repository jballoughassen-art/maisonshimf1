# Maison Shim — Project Specification

**Course project:** Homework 2 — AI-Assisted Development and Testing  
**Project:** Maison Shim — Pâtisserie website and order-management interface  
**Repository:** https://github.com/jballoughassen-art/maisonshimf1  
**Working branch:** `main` (create a feature branch before implementation)  
**Specification status:** Draft v1.0 — to be reviewed by the Developer and Tester  
**Date:** 17 November 2026

## 1. Project overview

Maison Shim is an existing, browser-based website for a Tunisian pastry business. The current application presents the business and its products, lets visitors interact with a shopping cart, prepares orders for WhatsApp, and provides a client-side administration interface for editing the product catalogue.

For Homework 2, the team will improve and test this existing application rather than replace it with an unrelated or pre-built project. The team will retain the current HTML, CSS, JavaScript and Tailwind CSS approach unless implementation evidence demonstrates that a change is necessary.

The assignment's main learning objective is to use AI assistants during development and testing, then critically evaluate their output. AI-generated code and tests must be reviewed by the team. Actual defects, test results, AI mistakes and human corrections must be recorded as evidence.

## 2. Team and responsibilities

| Member | Role | Main responsibilities |
|---|---|---|
| Ghassen | Developer | Inspect the existing code, maintain the specification, implement agreed improvements, review AI-generated code, fix defects and commit development changes. |
| Narimen | Tester | Prepare the test plan and test cases, request AI-generated test ideas and scripts, execute manual and automated tests, report reproducible defects and commit testing documentation/results. |

Both members must make meaningful commits to the GitHub repository using their own GitHub accounts. Each member is responsible for understanding and reviewing the work committed under their account.

## 3. Existing application and baseline

The following points are based on inspection of the supplied repository ZIP, which contains `index.html`, `README.md` and `SECURITY.md`.

### 3.1 Technology observed

- HTML for the page structure.
- CSS, including embedded custom styles.
- JavaScript embedded in `index.html`.
- Tailwind CSS loaded from its CDN.
- Browser `localStorage` for product data persistence.
- WhatsApp `wa.me` links for order hand-off.

No server-side application, backend API, database, package manifest or automated test framework was identified in the supplied ZIP. This is a statement about the supplied archive, not a claim that no such services exist outside it.

### 3.2 Existing features observed in the source

- Business landing page and navigation.
- Product catalogue rendered by JavaScript.
- Category filtering.
- Shopping cart with add, remove and quantity-update operations.
- Individual product ordering through WhatsApp.
- Click & Collect form that prepares an order message for WhatsApp.
- Contact form interface.
- Client-side administrator login interface.
- Administrator product-management interface, including product creation, editing and deletion.
- Product data stored in browser `localStorage`.

The team must verify these features in a browser before treating them as fully working requirements.

## 4. Project goals

1. Preserve the Maison Shim identity and existing customer-facing experience.
2. Make existing catalogue, cart and order interactions more reliable.
3. Validate user input and product data before changing or using it.
4. Handle missing or malformed browser-stored product data without an unhandled application failure.
5. make user feedback accurate: the interface must not claim that a message or order was delivered when it only opened or prepared an external WhatsApp message.
6. Improve maintainability without an unnecessary framework migration.
7. Establish repeatable manual and automated tests.
8. Record AI prompts, generated suggestions, human review, corrections and observed limitations.

## 5. Scope

### 5.1 In scope

- Existing landing page and responsive navigation.
- Product display and category filtering.
- Shopping cart operations and total calculation.
- Product data validation.
- Product persistence and recovery from invalid stored data.
- Click & Collect form validation and WhatsApp hand-off behaviour.
- Contact form behaviour and truthful submission feedback.
- Client-side administrator interface and product CRUD behaviour.
- Regression testing of existing functionality.
- Accessibility and basic usability checks where practical.
- AI-assisted development and test generation, with human review and evidence logs.

### 5.2 Out of scope for this iteration

Unless the team explicitly changes this scope and documents the decision:

- Real online payment processing.
- A production backend, hosted database or server-side order storage.
- Real customer accounts or multi-user authorization.
- Production-grade administrator authentication or authorization.
- Guaranteed delivery of contact messages or orders to the business.
- A full React/Node.js rewrite.
- Deployment infrastructure beyond the existing hosting arrangement.

**Security note:** A password checked in browser JavaScript and data stored in `localStorage` do not provide production-grade authentication or secure data storage. The current admin interface must be treated as a demonstration/client-side management feature, not as a secure production admin system. The team must not describe a frontend-only password check as secure authentication.

## 6. Functional requirements and acceptance criteria

The following requirements define the target behaviour for this project. They are proposed acceptance criteria and must be checked against the current application and agreed by both team members before implementation.

### FR-01 — Display the product catalogue

**Description:** Visitors can view the products available in the catalogue.

**Acceptance criteria:**
- The catalogue displays each valid product's name, price, image and description when those fields are available.
- An empty catalogue displays a clear empty state rather than a broken layout.
- A product with missing or invalid required data is not allowed to break the entire catalogue.
- Product text is rendered safely and does not execute user-supplied HTML or script.

### FR-02 — Filter products by category

**Description:** Visitors can filter the catalogue by a category and return to the full catalogue.

**Acceptance criteria:**
- Selecting a category displays only products belonging to that category.
- Selecting the all-products option displays all valid products.
- Selecting a category with no matching products displays a clear empty state.
- Repeated category changes do not duplicate product cards or produce stale results.

### FR-03 — Add products to the cart

**Description:** Visitors can add a catalogue product to the shopping cart.

**Acceptance criteria:**
- Adding a valid product creates a cart entry with quantity one.
- Adding the same product again increases its quantity instead of creating an unintended duplicate entry.
- A product identifier that does not exist is ignored safely and does not corrupt the cart.
- The cart item count reflects the sum of item quantities.

### FR-04 — Update and remove cart items

**Description:** Visitors can change quantities and remove items.

**Acceptance criteria:**
- Increasing quantity updates the item quantity and cart total.
- Decreasing quantity updates the item quantity and cart total.
- Quantity cannot become zero or negative; reaching the minimum removes the item or follows one clearly documented behaviour.
- Removing an item removes it from the cart and refreshes the count and total.
- An empty cart displays a clear empty state and does not allow an order to be submitted.

### FR-05 — Calculate cart totals

**Description:** The application calculates the total from product prices and quantities.

**Acceptance criteria:**
- The displayed total equals the sum of each valid unit price multiplied by its quantity.
- Invalid, negative, non-finite or missing prices are rejected rather than silently converted to a valid-looking zero price.
- Quantity values must be valid positive integers.
- The total is recalculated after every cart change.

### FR-06 — Prepare an individual WhatsApp order

**Description:** A visitor can request an individual product through the configured WhatsApp contact.

**Acceptance criteria:**
- The generated message identifies the selected product and its displayed price.
- Message content is URL-encoded before it is placed in the WhatsApp URL.
- A missing product does not open an incorrect order message.
- The interface clearly describes this action as opening or preparing a WhatsApp message; it does not claim that the business has received an order merely because a new tab was opened.

### FR-07 — Submit a Click & Collect request through WhatsApp

**Description:** A visitor can provide the required collection details and hand the order off to WhatsApp.

**Acceptance criteria:**
- A non-empty cart is required.
- The customer name and requested collection time are required.
- The generated message includes the customer name, collection time, cart items, quantities and calculated total.
- Optional notes are included only when provided.
- Message content is URL-encoded.
- Invalid or incomplete form input is rejected with understandable feedback.
- The cart is not cleared before the application has successfully initiated the WhatsApp hand-off. The exact behaviour when a browser blocks the new window must be tested and documented.
- The interface does not claim that WhatsApp delivered or that the business confirmed the order.

### FR-08 — Handle the contact form truthfully

**Description:** Visitors can use the contact form interface.

**Acceptance criteria:**
- Required fields are validated.
- Invalid input does not produce a success message.
- The application must not claim that a message was sent or delivered if no message transmission service is configured.
- If the project remains frontend-only, the interface must clearly explain the available contact action or provide a real configured hand-off method.
- Form reset behaviour occurs only after the defined action has completed successfully.

### FR-09 — Administrator access interface

**Description:** The existing interface provides a client-side admin entry point for demonstrating catalogue management.

**Acceptance criteria:**
- Empty or incorrect credentials do not open the admin dashboard.
- A successful demonstration login opens the dashboard.
- Logout closes the dashboard and resets the in-memory login state.
- The team documents that client-side credential checks are not secure authentication and must not be used to protect real private data or privileged server operations.

### FR-10 — Create, edit and delete products

**Description:** The administrator interface allows catalogue items to be managed.

**Acceptance criteria:**
- A new product receives a unique identifier and valid initial field values.
- Product name and description cannot be saved as invalid empty values if they are required by the agreed validation rules.
- Product price must be a finite, non-negative number; the team should decide whether zero is allowed and record that decision in the test cases.
- Image URLs must pass the agreed URL validation.
- Category must be one of the supported categories.
- Editing a product updates the catalogue and persists the change.
- Deleting a product removes it from the catalogue and persists the change.
- Cancelling a delete confirmation leaves the product unchanged.

### FR-11 — Persist and recover product data

**Description:** The catalogue is saved in browser `localStorage`.

**Acceptance criteria:**
- Valid product changes remain after a page reload in the same browser profile.
- Missing stored data falls back to the defined default catalogue.
- Malformed JSON or an invalid stored data structure is handled without an uncaught startup error.
- Invalid stored records are rejected or safely recovered according to a documented strategy.
- Storage failures, including unavailable or full storage, do not leave the interface in a misleading success state.

### FR-12 — Responsive and usable interface

**Description:** The existing visual identity is preserved while core interactions remain usable on common screen sizes.

**Acceptance criteria:**
- Navigation, catalogue, cart and forms remain usable on desktop and mobile viewport sizes selected in the test plan.
- Interactive controls have understandable labels or accessible names.
- Keyboard users can reach and operate the primary controls where practical.
- Validation and error messages are visible and understandable.

## 7. Non-functional requirements

- **Reliability:** Invalid user input or browser storage data must not crash the application.
- **Usability:** Actions, validation messages and order hand-off behaviour must be understandable.
- **Maintainability:** Changes should be small, documented and consistent with the existing codebase.
- **Compatibility:** Test in the agreed modern desktop browser(s); record browser and version in test results.
- **Security awareness:** Do not store real secrets or claim frontend-only controls provide production security.
- **Testability:** Core logic should be structured so it can be tested without manually repeating every browser interaction.
- **Traceability:** Each implemented requirement should map to one or more test cases and, where relevant, a GitHub issue or commit.

## 8. Proposed technology stack

| Area | Technology |
|---|---|
| Markup | HTML5 |
| Styling | CSS3 and existing Tailwind CSS CDN |
| Client-side logic | Vanilla JavaScript |
| Product persistence | Browser `localStorage` |
| External order hand-off | WhatsApp `wa.me` URL |
| Version control | Git and GitHub |
| Browser automation | Playwright (proposed; confirm during test setup) |
| Unit testing | To be selected after the code is inspected and testable functions are identified |
| AI assistance | ChatGPT and/or another assistant explicitly recorded in the AI logs |

No framework migration is planned for this iteration. Any new testing dependency must be documented in the repository and installed through a reproducible setup.

## 9. Testing strategy overview

The Tester owns the test plan and execution evidence. The Developer supports reproduction and correction.

Testing must include:

- Functional tests for the catalogue, filters, cart, product management and forms.
- Boundary tests for empty cart, minimum quantity, zero and invalid prices, long text and empty catalogue.
- Negative tests for unknown product IDs, malformed `localStorage`, invalid URLs and incomplete forms.
- Regression tests after each bug fix.
- Browser-level end-to-end tests for the main visitor and administrator demonstration flows.
- Manual checks for responsive layout and WhatsApp hand-off behaviour.

AI may suggest test cases, test data and automation scripts. The Tester must review every test, remove irrelevant tests, add missing edge cases and record whether each test was actually executed. AI-generated tests must not be reported as passed until they have run and produced evidence.

## 10. AI usage and evidence requirements

The team will maintain:

- `docs/AI_DEVELOPMENT_LOG.md` — Developer prompts, model/tool, generated suggestions or code, files affected, human changes and review outcome.
- `docs/AI_TESTING_LOG.md` — Tester prompts, generated test ideas/data/scripts, human review, execution results and corrections.
- `docs/AI_LIMITATIONS.md` — Concrete examples of incorrect, incomplete, inefficient or context-losing AI output, with evidence and the team's correction.
- `docs/BUG_REPORTS.md` — Reproducible defect reports, severity, expected/actual result, steps, status and linked fix/test.

Logs must describe what actually happened. Do not invent AI failures, test results, prompts, model versions or execution evidence. Record the exact model and tool interface used at the time.

## 11. Definition of done

A requirement is complete only when:

1. Its implementation matches the agreed acceptance criteria.
2. The Developer has reviewed and understood the change.
3. The Tester has executed the relevant tests.
4. Test results and any remaining defects are recorded.
5. Relevant regression tests pass, or known failures are explicitly documented.
6. The change is committed to GitHub with a meaningful message.
7. AI assistance and human modifications are logged when AI was used.

The project submission is ready when the repository contains the specification, test plan, test cases, AI logs, bug reports, test evidence, final PDF report and presentation slides, and both team members have contributed commits.

## 12. Open decisions to confirm

The team must confirm these items before treating this draft as final:

- Exact browser(s) and viewport sizes for testing.
- Whether product price `0` is allowed or must be rejected.
- Exact expected behaviour if a WhatsApp tab/window is blocked.
- Whether the contact form should remain informational or use a real configured contact hand-off.
- Which automated unit-testing approach best fits the existing single-file JavaScript structure.
- Whether any feature observed in the live repository differs from the supplied ZIP baseline.

---

**Document history**

| Version | Date | Changes |
|---|---|---|
| 1.0 | 17 November 2026 | Initial draft based on inspection of the supplied repository ZIP; acceptance criteria proposed for team review. |
