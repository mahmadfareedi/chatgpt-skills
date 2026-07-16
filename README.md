# M. Ahmad's ChatGPT Skills

A private collection of reusable ChatGPT skills created for M. Ahmad.

## Skills

### Job Application Checker

Uses a strict gated workflow for job applications:

1. Opens and resolves the LinkedIn post or supplied job description.
2. Extracts the role, company, application email, subject, and key requirements.
3. Searches Gmail Sent mail before writing anything.
4. Reports a definite or possible previous application with its sent date and elapsed time.
5. Asks for confirmation before preparing another email when a prior application exists.
6. Writes a tailored email only when the duplicate check allows it.
7. Uses the Resume Attachment Manager when the user requests a Gmail draft with the resume attached.
8. Sends only after a separate explicit instruction.

Source: `skills/job-application-checker/`

Packaged archive: `dist/job-application-checker.zip`

### Resume Attachment Manager

Retrieves and verifies the configured resume PDF from the latest commit on GitHub, then attaches it to an approved Gmail draft when an attachment-capable email MCP or connector is available.

Configured resume source:

- Repository: `mahmadfareedi/resume`
- Branch: `master`
- Path: `Muhammad_Ahmad_Senior_Data_Analyst.pdf`

The skill never claims the resume is attached unless the email tool confirms the exact attachment filename.

Source: `skills/resume-attachment-manager/`

Packaged archive: `dist/resume-attachment-manager.zip`

### English Corrector

Corrects, rewrites, and formats text in clear, natural US English. It preserves the original meaning, returns only the finished text by default, follows M. Ahmad's concise professional style, avoids unnecessary dash punctuation, and keeps normal email writing separate from Gmail draft or send actions.

It also defers job application emails to the Job Application Checker so the Gmail duplicate check is not bypassed.

Source: `skills/english-corrector/`

Packaged archive: `dist/english-corrector.zip`

## Resume attachment MCP

See `MCP_SETUP.md` for the required GitHub file retrieval and Gmail attachment actions. The Skills control the workflow, while the MCP performs the actual binary attachment.

## Skill sync agent

Use `AGENT_PROMPT.md` with an agent that can access the skills and GitHub. The prompt checks for meaningful differences, validates changed skills, rebuilds packages, and pushes only necessary updates.

## Repository structure

```text
AGENT_PROMPT.md
MCP_SETUP.md

skills/
  job-application-checker/
    SKILL.md
    agents/openai.yaml
    references/application-profile.md
    references/workflow-tests.md

  resume-attachment-manager/
    SKILL.md
    agents/openai.yaml
    references/resume-source.md
    references/mcp-contract.md

  english-corrector/
    SKILL.md
    agents/openai.yaml
    assets/icon.svg

dist/
  job-application-checker.zip
  resume-attachment-manager.zip
  english-corrector.zip
```

## Privacy

Keep this repository private. Some skills contain personal workflow preferences, professional profile details, resume locations, and connector instructions.

## Adding another skill

Add each skill as its own folder inside `skills/`, then place its validated package inside `dist/` using the skill name as the ZIP filename.
