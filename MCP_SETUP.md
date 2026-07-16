# Resume Mailer MCP Setup

## Why an MCP is required

The Skills define the workflow, but a real email attachment requires a Gmail action that accepts files. The standard Gmail actions available to this workflow create drafts from recipients, subject, and body only, so they cannot attach the resume PDF.

For a one-click application draft, connect an MCP or app that can:

1. Retrieve the configured PDF from GitHub.
2. Return the PDF as a connector file reference or mounted local path.
3. Create a Gmail draft with that file attached.
4. Send the reviewed draft only after a separate explicit instruction.

## Configured PDF

- Repository: `mahmadfareedi/resume`
- Branch: `master`
- Path: `Muhammad_Ahmad_Senior_Data_Analyst.pdf`
- MIME type: `application/pdf`

Retrieve the file through the GitHub contents API or connector. Do not use the GitHub HTML page as the attachment.

## Required MCP tools

### `get_resume_pdf`

Input:

```json
{
  "repository_full_name": "mahmadfareedi/resume",
  "ref": "master",
  "path": "Muhammad_Ahmad_Senior_Data_Analyst.pdf"
}
```

Output:

```json
{
  "file": "<connector-file-reference-or-mounted-path>",
  "filename": "Muhammad_Ahmad_Senior_Data_Analyst.pdf",
  "mime_type": "application/pdf",
  "size_bytes": 123456,
  "source_commit_sha": "<latest-master-commit>",
  "git_blob_sha": "<blob-sha>",
  "sha256": "<checksum>"
}
```

### `create_gmail_draft_with_attachments`

Input:

```json
{
  "to": "recipient@example.com",
  "subject": "Application for Senior Data Analyst",
  "body": "Approved email body",
  "attachments": ["<file-reference-or-mounted-path>"]
}
```

Output must confirm the attachment:

```json
{
  "draft_id": "<draft-id>",
  "display_url": "<gmail-url>",
  "attachment_names": ["Muhammad_Ahmad_Senior_Data_Analyst.pdf"]
}
```

### `send_gmail_draft`

Use only after the user separately asks to send the reviewed draft.

## Authentication and safety

- Use minimum GitHub and Gmail OAuth scopes.
- Keep credentials in the MCP host secret manager or environment.
- Never commit credentials or log OAuth tokens, email bodies, or PDF bytes.
- Fetch from the latest `master` commit for each application.
- Verify `%PDF-`, MIME type, filename, and nonzero size.
- Never silently drop an attachment.
- Create a draft by default and send only after explicit approval.
