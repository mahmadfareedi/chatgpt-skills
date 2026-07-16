# Resume and Gmail Attachment MCP Contract

A Skill can control the workflow, but it cannot add binary attachment support to a mail connector. The complete one-click draft workflow requires an MCP or connector exposing equivalent tools.

## Tool 1: get_resume_pdf

Purpose: Fetch the configured resume PDF from the latest commit on the configured GitHub branch and return a usable file reference.

Suggested input:

```json
{
  "repository_full_name": "mahmadfareedi/resume",
  "ref": "master",
  "path": "Muhammad_Ahmad_Senior_Data_Analyst.pdf"
}
```

Required output:

```json
{
  "file": "<connector file reference or mounted local path>",
  "filename": "Muhammad_Ahmad_Senior_Data_Analyst.pdf",
  "mime_type": "application/pdf",
  "size_bytes": 123456,
  "source_commit_sha": "<full latest commit sha>",
  "git_blob_sha": "<github blob sha>",
  "sha256": "<file checksum>",
  "retrieved_at": "<ISO 8601 timestamp>"
}
```

Required implementation behavior:

1. Resolve the latest commit on `master` through the GitHub API.
2. Fetch the file from that exact commit, not from an unpinned cached URL.
3. Confirm the response starts with `%PDF-`.
4. Store the PDF in temporary connector storage.
5. Return a connector file reference or mounted path.

## Tool 2: create_gmail_draft_with_attachments

Purpose: Create a Gmail draft with one or more real file attachments.

Suggested input:

```json
{
  "to": "talent@example.com",
  "subject": "Application for Senior Data Analyst",
  "body": "<approved email body>",
  "attachments": ["<file reference from get_resume_pdf>"]
}
```

Required output:

```json
{
  "draft_id": "<gmail draft id>",
  "display_url": "<open in Gmail URL>",
  "attachment_names": ["Muhammad_Ahmad_Senior_Data_Analyst.pdf"]
}
```

The implementation must use Gmail multipart MIME draft creation and must not send the message.

## Optional Tool 3: send_gmail_draft

Purpose: Send an already reviewed draft only after a separate explicit user instruction.

Required input:

```json
{
  "draft_id": "<reviewed draft id>"
}
```

Do not combine draft creation and sending into one automatic action.

## Security requirements

- Use OAuth with the minimum GitHub and Gmail scopes required.
- Never log email bodies, OAuth tokens, private repository content, or attachment bytes.
- Store temporary PDFs only as long as needed.
- Reject files that are not PDFs or exceed the configured size limit.
- Require explicit user confirmation before sending.
