
# Narimen – Testing Contribution

## Role
Tester – Maison Shim Homework 2

## Responsibilities
- Review the project specification.
- Prepare and execute functional test cases.
- Check boundary and negative scenarios.
- Record actual test results.
- Report bugs to the developer.
- Use an AI assistant to generate and review test ideas.

## Test Execution

| Test ID | Scenario | Expected Result | Actual Result | Status |
|---|---|---|---|---|
| TC01 | View the homepage | Homepage displays correctly | To be completed | Not run |
| TC02 | Add a product to the cart | Product appears in cart | To be completed | Not run |
| TC03 | Change product quantity | Cart quantity updates | To be completed | Not run |
| TC04 | Remove a product | Product disappears from cart | To be completed | Not run |
| TC05 | Refresh the page | Cart remains saved | To be completed | Not run |
| TC06 | Submit Click & Collect order | Order confirmation appears | To be completed | Not run |

## AI Testing Assistance
AI tool: [ChatGPT (OpenAI), web interface. The exact model version used during the testing discussions was not recorded.]

Prompts used:
- ["Help us design test cases for the Maison Shim website, covering the homepage, product catalogue, shopping cart, cart persistence, Click & Collect, contact form, and admin features."

"Analyze the baseline test results, identify the cause of the shopping cart persistence failure, and suggest a correction and a retesting procedure."

"Help us document the test results, report the identified bug, and prepare the final testing documentation."]
- [The AI-generated test ideas were reviewed against the project specification and the actual website features. The team selected relevant scenarios, executed the available tests manually, compared the observed results with the expected results, and updated the test documentation. AI suggestions were not considered successful until they had been checked against the application.]

## Findings
[During the initial testing phase, the team identified one functional bug:

BUG-001 – Shopping cart data lost after page refresh

Description: Products added to the shopping cart disappeared when the page was refreshed.

Expected result: The shopping cart should retain its contents after refreshing the page.

Actual result: The cart was reset after refreshing the page.

Cause: The shopping cart data was not being saved persistently.

Correction: The developer implemented localStorage persistence and updated the cart operations to save changes.

Retest result: The team confirmed that the cart contents remained available after refreshing the page.

The team also verified that the cart was cleared after a Click & Collect submission.

One limitation identified during source review was that the contact form displayed a success message without a configured message-delivery service. Therefore, displaying the confirmation message does not prove that the message was actually delivered.]

## Conclusion
[The team reported that all 12 planned functional test cases passed after the correction of the shopping cart persistence bug. An additional check confirmed that the cart was cleared after a Click & Collect submission.

AI assistance was useful for generating test ideas, organizing test cases, analyzing the reported bug, and preparing testing documentation. However, AI-generated suggestions and code required human review and validation.

The testing activities documented for this project were primarily manual. Automated test execution was not confirmed. The experience demonstrated that AI can support software testing, but it cannot replace actual execution, observation, and human judgment.
]
