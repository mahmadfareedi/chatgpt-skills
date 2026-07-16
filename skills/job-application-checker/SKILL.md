---
name: job-application-checker
description: Enforce a strict job application workflow that resolves the LinkedIn post or job description, checks Gmail Sent mail for a prior application, and only then writes a tailored application email in normal chat for review. Use when the user shares a LinkedIn URL, recruiter post, job advertisement, screenshot, recipient email, or job description and asks to apply or write an email. Never draft, open an email compose card, create a Gmail draft, or send anything before completing the duplicate check or receiving explicit permission to proceed without it.
---

# Job Application Checker

Follow the workflow as a strict state machine. Do not skip, reorder, or combine the gates.

## Non-negotiable rules

- Never write the application email before the Gmail duplicate check is complete.
- Never open an email compose card merely because the user says `write an email` or `apply`.
- Never call Gmail draft or send actions during the checking stage.
- Return the email as normal chat text after a confirmed `No duplicate` result.
- Create a Gmail draft only when the user explicitly asks to save the approved email as a Gmail draft.
- Send only when the user explicitly asks to send an approved email.
- If job details or Gmail access are insufficient, stop and explain what is missing. Do not silently continue.

## Gate 1: Resolve the job post

First inspect all supplied material and extract:

- Exact job title
- Company name
- Recipient email address, when listed
- Recruiter or contact name, only when explicitly stated
- Location, when relevant
- Required application subject, when stated
- Application method
- Three to five requirements most relevant to the candidate

For a LinkedIn or public job-post URL:

1. Open the URL and inspect its content before doing anything else.
2. Use text or screenshots already supplied in the conversation when the page is inaccessible.
3. If the page cannot be accessed and the conversation does not contain enough details, ask the user to paste the post or upload a screenshot.
4. Do not infer the recruiter's name, company, role, or email from the URL slug alone.
5. Do not proceed to drafting while the job title or company is unresolved.

Mark this gate complete only after the role and company are known and the application method has been checked.

## Gate 2: Check Gmail Sent mail

Use the connected Gmail account and search `in:sent`. This check is mandatory even when the user only says `write email for it`.

Search in this order, using every applicable query:

1. When an application email is known: `in:sent to:<recipient-email>`
2. `in:sent subject:"<exact-job-title>"`
3. `in:sent "<company-name>" "<distinctive-job-title-words>"`
4. When the title has common variants, repeat the subject or keyword search with the closest variant.

Do not rely on search snippets alone. Read the most relevant candidate messages and compare:

- Normalized recipient address
- Company name
- Job title and close title variants
- Email subject
- Sent date
- Application wording or attachment context when needed

Run at least two applicable searches before declaring `No duplicate`. A recipient-only search is not sufficient because the same company may use multiple recruiting addresses.

If Gmail is not connected, inaccessible, or returns an error:

- State that the duplicate check could not be completed.
- Do not write an email yet.
- Ask: `I could not verify your Sent mail. Do you want me to proceed without the duplicate check?`
- Continue only after the user explicitly confirms.

## Gate 3: Classify and stop or continue

Classify the evidence as one of these states:

### Definite duplicate

Use when the same recipient and same or closely matching role are found, or when the message clearly shows an application for the same company and role.

Stop before drafting. Report:

- Exact or closest job title found
- Company
- Recipient email
- Previous subject
- Exact sent date
- Natural elapsed time, such as `4 days ago`, `3 weeks ago`, or `about 2 months ago`

Then ask exactly one confirmation question:

`You already applied for this role. Do you really want me to prepare another application email?`

Do not draft, create a Gmail draft, or send anything until the user confirms.

### Possible duplicate

Use when the company and a closely matching role are found but the recipient differs or the evidence is incomplete.

Explain the uncertainty, show the available details and elapsed time, then ask whether to prepare another email. Stop until the user confirms.

### No duplicate

Use only after the required Gmail searches and message review find no relevant application.

State:

`I checked your Sent mail and did not find a matching application for this role.`

Only now proceed to Gate 4.

## Gate 4: Write the email in chat

Write a tailored application email as normal chat text. Do not open a compose card and do not create a Gmail draft.

Use the current CV or profile details available in the conversation. Consult `references/application-profile.md` for stable defaults, but prefer newer CV evidence.

Follow these rules:

- Use US English.
- Keep the email concise, usually 120 to 180 words.
- Use a professional, natural, respectful tone.
- Tailor two or three sentences to the post's main requirements.
- Mention only experience supported by the CV, conversation, or profile reference.
- Do not invent machine learning, forecasting, leadership, domain, salary, relocation, or certification claims.
- Avoid generic praise, excessive enthusiasm, emojis, hashtags, and dash punctuation.
- Use `Dear Hiring Team,` when no person's name is confirmed.
- Never address the LinkedIn post author by name unless the post explicitly identifies that person as the application contact.
- Use `M. Ahmad` as the signature.
- If the post specifies a subject, use it exactly. Otherwise use `Application for <Exact Job Title>`.
- Mention an attached CV only when the user intends to attach one.
- Add a short reminder outside the email to attach the latest CV when applicable.
- If no recipient email was found, state that clearly outside the email. Never create a Gmail draft with an empty recipient.

## Gate 5: Optional Gmail action

Treat these as separate explicit actions:

- `Save this as a Gmail draft`: create a Gmail draft using the approved recipient, subject, and body.
- `Send this email`: send only the approved version and only after the user explicitly requests sending.

Before creating a Gmail draft or sending:

1. Confirm the recipient is known.
2. Use the approved subject and body.
3. Do not claim the CV is attached unless an attachment was actually added.
4. Do not repeat the duplicate check unless the job details changed or significant time has passed.

## Required output patterns

### Definite duplicate

`You already applied for <Job Title> at <Company> on <Exact Date>, <elapsed time>. The email was sent to <recipient> with the subject "<subject>". Do you really want me to prepare another application email?`

### Possible duplicate

`I found a possible previous application for <Role> at <Company>, sent on <Exact Date>, <elapsed time>. The recipient or title is not an exact match. Do you want me to prepare a new application email anyway?`

### No duplicate

Start with:

`I checked your Sent mail and did not find a matching application for this role.`

Then provide the subject and complete email in normal chat text.

### Blocked because details are missing

`I have not drafted the email yet because I could not verify the complete job post. Please paste the job details or upload a screenshot so I can check the role, company, application email, and your Sent mail first.`

### Blocked because Gmail is unavailable

`I could not verify your Sent mail, so I have not drafted the application email. Do you want me to proceed without the duplicate check?`

## Regression check

Before responding, verify the current path against `references/workflow-tests.md`. If the response would draft an email before Gate 2 and Gate 3 are complete, stop and correct the workflow.
