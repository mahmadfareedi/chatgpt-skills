---
name: resume-attachment-manager
description: Retrieve and verify M. Ahmad's current Senior Data Analyst resume PDF from the fixed GitHub path, then attach it to an approved Gmail application draft when an attachment-capable connector or MCP tool is available. Use when a job application needs the resume, when the user asks to attach the CV from the resume repository, or when another skill needs the verified PDF. Always resolve the file from the latest commit on master, never claim an attachment without tool confirmation, and never send automatically.
---

# Resume Attachment Manager

Use this skill as the file and attachment stage of the job application workflow. It does not replace the duplicate-application check.

## Non-negotiable rules

- Never run before the job application workflow resolves the role and completes its Gmail duplicate check.
- Always use the configured PDF unless the user explicitly provides a replacement.
- Never claim that a resume is attached unless the mail tool confirms the attachment filename.
- Never send an email automatically.
- Create an attachment-ready Gmail draft only after the user approves the email text or explicitly asks to prepare it in Gmail.
- If no attachment-capable Gmail tool is available, stop and explain the limitation.
- Do not attach a GitHub HTML page, repository source file, JSON file, or ZIP in place of the PDF.

## 1. Resolve the fixed resume source

Read `references/resume-source.md` and use exactly:

- Repository: `mahmadfareedi/resume`
- Branch: `master`
- Path: `Muhammad_Ahmad_Senior_Data_Analyst.pdf`
- Filename: `Muhammad_Ahmad_Senior_Data_Analyst.pdf`

Treat `latest` as the version of this path at the latest commit on `master` at execution time. Do not cache an older copy across applications.

## 2. Retrieve the PDF

Prefer an installed attachment MCP or connector that implements `references/mcp-contract.md`.

The retrieval tool must:

1. Resolve the latest commit SHA on `master`.
2. Fetch `Muhammad_Ahmad_Senior_Data_Analyst.pdf` from that exact commit.
3. Return a real connector file reference or mounted local path, not only a URL.
4. Return the filename, MIME type, file size, source commit SHA, Git blob SHA, and checksum when available.

Accept only a file that meets all of these conditions:

- MIME type is `application/pdf`
- Filename is exactly `Muhammad_Ahmad_Senior_Data_Analyst.pdf`
- File is non-empty
- PDF signature starts with `%PDF-`
- Source commit matches the latest resolved commit on `master`

If retrieval fails, report the repository, branch, path, and failure reason. Do not proceed to attachment.

## 3. Present the selected resume

Before creating a Gmail draft, state:

- PDF filename
- Source repository, branch, and path
- Source commit short SHA
- File size when available

When the email is not yet approved, provide these details but do not create a draft.

## 4. Create a Gmail draft with the PDF attached

Use an attachment-capable Gmail connector or MCP tool. The tool must accept a connector file reference or local path as an attachment.

Before calling it, verify:

1. Recipient email is known.
2. Subject and body are the approved versions.
3. The PDF passed all checks above.
4. The user explicitly asked to prepare or save the Gmail draft.

After creation, verify the result includes:

- Gmail draft identifier
- Attachment filename exactly matching `Muhammad_Ahmad_Senior_Data_Analyst.pdf`
- Gmail display URL when available

Respond:

`The Gmail draft is ready with Muhammad_Ahmad_Senior_Data_Analyst.pdf attached. Please review it in Gmail before sending.`

Do not say it is attached if the tool response does not confirm the filename.

## 5. Send only after separate confirmation

Treat sending as a separate action. Send only when the user explicitly asks to send the reviewed draft after attachment verification.

If the user says only `write the email`, `apply`, `prepare it`, or `draft it`, do not send.

## Fallback when attachment tools are unavailable

Use this exact behavior:

`I verified the resume source, but the connected Gmail tool cannot add file attachments. I have not created a misleading draft. An attachment-capable Gmail MCP or connector is required to create the one-click Gmail draft with Muhammad_Ahmad_Senior_Data_Analyst.pdf included.`

Then provide the repository path and latest source commit when available. Do not claim the workflow is complete.
