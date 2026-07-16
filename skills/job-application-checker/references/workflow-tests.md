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
6. Do not draft or retrieve a resume before confirmation.

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

## Test 6: User asks to save an approved email without attachment support

Expected path:

1. Confirm recipient, subject, and approved body.
2. Do not claim the resume is attached.
3. Explain that an attachment-capable Gmail MCP or connector is required.
4. Do not send.

## Test 7: User asks for a Gmail draft with the resume attached

Expected path:

1. Complete the job-post and duplicate-check gates first.
2. Write or confirm the approved email.
3. Resolve the latest `master` commit in `mahmadfareedi/resume`.
4. Fetch `Muhammad_Ahmad_Senior_Data_Analyst.pdf` from that exact commit.
5. Verify the PDF and create a Gmail draft only through an attachment-capable tool.
6. Confirm the exact attachment filename from the tool response.
7. Do not send.

## Test 8: Attachment tool returns no attachment confirmation

Expected path:

1. Treat the draft as unverified.
2. Do not claim the resume is attached.
3. Ask the user to review the draft manually or retry after fixing the connector.

## Test 9: Resume path returns HTML or another file type

Expected path:

1. Reject the result.
2. Do not attach it.
3. Report that the configured PDF could not be verified.
4. Do not create or send a Gmail message.
