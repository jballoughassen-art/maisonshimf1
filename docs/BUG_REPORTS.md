# Maison Shim — Bug Reports

**Project:** Homework 2 — AI-Assisted Development and Testing  
**Branch:** `feature/homework2-improvements`  
**Last updated:** 17 November 2026

## BUG-001 — Cart contents were lost after page refresh

| Field | Value |
|---|---|
| Status | FIXED — retest passed |
| Severity | Medium |
| Priority | Medium |
| Area | Shopping cart / browser persistence |
| Related test | TC08 |
| Fix commit | `8859826` |
| Commit message | `Fix cart persistence and Click and Collect` |

### Description

Cart contents were held only in application memory. Refreshing the page cleared the cart instead of restoring its products and quantities.

### Steps to reproduce (before fix)

1. Open Maison Shim.
2. Add a product to the cart.
3. Refresh the page.
4. Reopen the cart.

### Expected result

The cart should retain its products and quantities after a refresh in the same browser profile.

### Actual result before fix

The cart was empty after refresh.

### Root cause

The cart state was not being persisted to browser `localStorage`.

### Resolution

Cart state was saved to and restored from `localStorage` using the `maisonShimCart` key. Cart persistence was connected to the relevant add, remove and quantity-update operations. The Click & Collect submission flow also saves the cleared cart state.

### Retest

The team reported that TC08 passed after replacing the application file with the repaired `index.html`. The team also confirmed that the cart clears correctly after Click & Collect submission.

### Final status

**FIXED.** TC08 passed on retest. The additional Click & Collect cart-clearing check also passed.

---

## Additional source-review observation (not a confirmed execution failure)

The contact form's client-side handler was observed to display a success toast and reset the form without a configured message-transmission service in the inspected source. TC10 was reported as PASS for the form interaction, but this must not be described as proof that a message was actually delivered. Treat accurate contact-form delivery feedback as a known limitation or follow-up improvement, not as a failed test unless a specific delivery test is performed.
