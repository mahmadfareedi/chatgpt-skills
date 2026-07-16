---
name: job-application-checker
description: Check Gmail before drafting job application emails to prevent duplicate applications, then create a concise, tailored email for review. Use when the user shares a LinkedIn job post, job advertisement, recruiter email, application email address, screenshot, or job description and asks to apply, write an application email, or check whether they already applied. Search Sent mail using the recipient, job title, and company; report any matching prior application with its date and elapsed time; otherwise draft the email without sending it.
---

# Job Application Checker

Use this workflow in order. Never send an application email automatically.

## 1. Extract the application details

Identify:

- Exact job title
- Company name
- Recipient email address
- Location, when relevant
- Subject line required by the post, if specified
- Three to five requirements most relevant to the candidate

If the user provides only a LinkedIn or public job-post URL, open it and extract the details. If the page is inaccessible, use any text or screenshot in the conversation. Ask for pasted content only when the role, recipient, or application method cannot otherwise be determined.

## 2. Check Gmail Sent mail first

Use the connected Gmail account before drafting.

Search in this order:

1. `in:sent to:<recipient-email>`
2. `in:sent to:<recipient-email> subject:"<job-title>"`
3. `in:sent "<company-name>" "<distinctive-job-title-words>"`

Read the most relevant candidate messages. Compare normalized recipient addresses, company names, and role titles. Ignore capitalization, punctuation, abbreviations, and harmless word-order differences.

Classify the result:

- **Definite duplicate:** Same recipient email and same or closely matching job title.
- **Possible duplicate:** Same company and closely matching role, but a different recipient or incomplete evidence.
- **No duplicate:** No relevant sent application found.

Do not treat a similar role at another company as a duplicate.

## 3. Respond when a prior application exists

For a definite duplicate, stop before drafting. Report:

- That the user already applied
- Exact job title and company found
- Recipient email
- Previous email subject
- Exact sent date
- Natural elapsed time, such as `4 days ago`, `3 weeks ago`, or `about 2 months ago`

Then ask one direct question: `You already applied for this role. Do you want me to prepare another application email?`

For a possible duplicate, explain the uncertainty and show the same available details. Ask whether to continue with a new draft.

Do not create or send a second email until the user confirms.

## 4. Draft when no duplicate exists

Create a tailored application email for review. Use the current CV or profile details available in the conversation. Consult `references/application-profile.md` for stable defaults, but prefer newer CV information whenever available.

Follow these rules:

- Use US English.
- Keep the email concise, usually 120 to 180 words.
- Use a simple, professional, natural tone.
- Tailor two or three sentences to the post's main requirements.
- Mention only skills and experience supported by the CV, conversation, or profile reference.
- Do not invent machine learning, forecasting, leadership, domain, salary, relocation, or certification claims.
- Avoid generic praise, excessive enthusiasm, emojis, hashtags, and dash punctuation.
- Use `Dear Hiring Team,` when no person's name is available.
- Use `M. Ahmad` as the closing signature.
- If the post specifies a subject, use it exactly. Otherwise use `Application for <Exact Job Title>`.
- Mention an attached CV only when the user intends to attach one. Add a brief reminder outside the email to attach the updated CV before sending.

Return the finished email as a reviewable email draft. Do not send it and do not create a Gmail draft unless the user explicitly asks to save it in Gmail.

## 5. Optional Gmail draft

When the user explicitly asks to save the approved version in Gmail:

1. Use the extracted recipient and approved subject.
2. Create a Gmail draft, not a sent email.
3. Do not claim the CV is attached unless an attachment was actually added.
4. Confirm that the draft was saved for review.

Only send when the user explicitly asks to send the approved Gmail draft.

## Output patterns

### Definite duplicate

`You already applied for <Job Title> at <Company> on <Exact Date>, <elapsed time>. The email was sent to <recipient> with the subject “<subject>”. Do you want me to prepare another application email?`

### No duplicate

Start with: `I did not find a matching application in your Sent mail.`

Then provide the complete reviewable application email and a short reminder to attach the latest CV when applicable.
