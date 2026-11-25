# Maison Shim — AI Testing Log

**Project:** Homework 2 — AI-Assisted Development and Testing  
**Application:** Maison Shim  
**Tester:** Narimen  
**Developer:** Ghassen  
**Branch:** `feature/homework2-improvements`  
**Date:** 17 November 2026

## 1. Purpose

This log records the AI-assisted test planning and the test outcomes reported by the team. AI suggestions were treated as proposals; the team remained responsible for reviewing and executing tests.

## 2. Testing activities and recorded outcomes

| Activity | AI assistance / team action | Outcome |
|---|---|---|
| Define functional test coverage | AI helped organize test coverage for homepage, navigation, catalogue, filtering, cart, WhatsApp, contact form and admin features. | Test cases were prepared for the existing application. |
| Baseline execution | The team supplied the initial results for TC01–TC12. | 11 passed; TC08 failed. |
| Defect analysis | AI helped identify that the cart was in memory and needed persistence to browser storage. | BUG-001 was documented. |
| Regression fix review | AI prepared a repaired `index.html` with cart save/restore behaviour and updates to cart actions. | Inline JavaScript syntax was checked with `node --check`; this was a syntax check, not a complete browser test. |
| Browser retest | The team replaced the application file and tested the application. | The team reported that the application worked smoothly and TC08 passed after refresh. |
| Click & Collect regression check | The team submitted a Click & Collect flow and checked the cart afterwards. | The team confirmed that the cart cleared correctly. |
| Git version control | The developer committed `index.html`. | Commit `8859826` on `feature/homework2-improvements`. |

## 3. Final reported test results

The team reported all 12 original test cases as passing after the fix.

- TC01–TC07: PASS (reported baseline results).
- TC08: PASS after the cart-persistence fix and retest.
- TC09–TC12: PASS (reported baseline results).
- Additional Click & Collect cart-clearing check: PASS (team-confirmed).

**Reported final result: 12/12 original test cases passed.**

## 4. AI output review and limitations

- An earlier attempt to insert the persistence code manually resulted in a broken application file. The team reported that the app became non-functional. The implementation was then reconstructed from the clean original file rather than continuing to patch the corrupted copy.
- AI-assisted JavaScript syntax validation cannot prove that every browser interaction works. Browser execution and user testing were still required.
- The team, not the AI, confirmed that the application worked smoothly, that TC08 passed after refresh, and that the cart cleared after Click & Collect.
- The contact form's successful UI interaction must not be confused with actual message delivery. The inspected frontend handler did not demonstrate a configured delivery service.
- The admin password is checked in client-side JavaScript; this is not secure production authentication.
- Browser version, viewport, screenshots and recordings were not supplied for this log. Add genuine test evidence if required by the assignment.

## 5. Development commit associated with retesting

```text
Branch: feature/homework2-improvements
Commit: 8859826
Message: Fix cart persistence and Click and Collect
File: index.html
```

## 6. Final assessment

The reported functional regression is resolved and the team reports 12/12 original test cases passing. The Click & Collect cart-clearing check also passed. The result is a successful functional test milestone, not a claim that the frontend-only application is production-secure or that external messages are guaranteed to be delivered.
