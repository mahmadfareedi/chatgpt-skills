# Workflow Regression Tests

Use these examples to verify that the mandatory gates are followed.

## Test 1: LinkedIn URL and confirmed duplicate

Input: `Write email for it` plus a LinkedIn URL.

Expected path:

1. Open and inspect the post.
2. Extract the company, role, and application email.
3. Search Gmail Sent mail and read relevant matches.
4. Report the previous application date and elapsed time.
5. Ask whether the user really wants another email.
6. Do not draft anything before confirmation.

## Test 2: LinkedIn URL and no duplicate

Expected path:

1. Inspect the post.
2. Search Gmail Sent mail with at least two applicable queries.
3. State that no matching application was found.
4. Return the email as normal chat text.
5. Do not open a Gmail compose card.

## Test 3: LinkedIn page cannot be accessed

Expected path:

1. Use supplied text or screenshot.
2. When details remain incomplete, ask the user to paste the post or upload a screenshot.
3. Do not infer details from the URL slug.
4. Do not draft an email.

## Test 4: Gmail unavailable

Expected path:

1. State that Sent mail could not be checked.
2. Ask whether to proceed without verification.
3. Do not draft unless the user confirms.

## Test 5: User confirms another application

Expected path:

1. After a duplicate warning, accept explicit confirmation.
2. Write the new email in normal chat text.
3. Do not create or send a Gmail message unless separately requested.

## Test 6: User asks to save the approved email

Expected path:

1. Confirm recipient, subject, and approved body.
2. Create a Gmail draft.
3. Do not send it.
