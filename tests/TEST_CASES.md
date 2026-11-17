# Maison Shim — Final Test Cases

**Project:** Homework 2 — AI-Assisted Development and Testing  
**Application:** Maison Shim  
**Branch:** `feature/homework2-improvements`  
**Final execution status:** 12/12 passed, based on the team's reported manual results  
**Date recorded:** 17 November 2026

## Execution summary

| ID | Test case | Result | Notes |
|---|---|---|---|
| TC01 | Homepage loads | PASS | Homepage displayed correctly. |
| TC02 | Navigation | PASS | Navigation was reported working. |
| TC03 | Product catalogue | PASS | Product catalogue was reported working. |
| TC04 | Category filter | PASS | Category filtering was reported working. |
| TC05 | Add product to cart | PASS | Product could be added to the cart. |
| TC06 | Update cart quantity | PASS | Quantity could be updated. |
| TC07 | Remove product from cart | PASS | Product could be removed. |
| TC08 | Cart persistence after refresh | PASS | Initially failed; passed after the cart-persistence fix was installed and retested. |
| TC09 | WhatsApp order hand-off | PASS | WhatsApp order hand-off was reported working. |
| TC10 | Contact form interaction | PASS | The form interaction was reported working. This result does not establish that a message is transmitted to a server or recipient. |
| TC11 | Admin interface | PASS | Admin interface was reported accessible and functional in the tested flow. |
| TC12 | Product management | PASS | Product-management flow was reported working. |

## Detailed regression test: TC08 — Cart persistence

**Precondition:** The application is open in the same browser profile.

**Steps:**
1. Add one or more products to the cart.
2. Record the selected products and quantities.
3. Refresh the page.
4. Reopen the cart.

**Expected result:** The previously selected products and quantities remain in the cart.

**Actual result:** The team reported that the cart remained intact after refresh with the updated `index.html`.

**Status:** PASS (retested after fix).

## Click & Collect cart-clearing check

This was an additional regression check reported by the team, not a separately numbered case in the original 12-case baseline.

**Steps:**
1. Add products to the cart.
2. Open the Click & Collect form.
3. Submit the form and complete the WhatsApp hand-off flow.
4. Check the cart in the application.

**Expected result:** The cart is cleared after the Click & Collect submission flow.

**Actual result:** The team confirmed that the cart cleared correctly.

**Status:** PASS (additional check).

## Test environment and evidence

The team has not supplied the exact browser version, operating-system build, viewport dimensions, screenshots, or screen recordings in the conversation. Add those details and attach genuine screenshots/logs if required by the instructor. Do not invent environment details or evidence.

## Important interpretation

A PASS result records the team's reported execution outcome for the stated test. It does not certify production readiness, server-side security, successful receipt of WhatsApp messages, or transmission of the contact form. The contact form's actual delivery behaviour should be described accurately in the project report.
