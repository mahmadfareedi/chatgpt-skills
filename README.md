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
6. Writes a tailored email in normal chat only when no duplicate is found or the user explicitly approves continuing.
7. Creates or sends a Gmail message only after a separate explicit request.

Source: `skills/job-application-checker/`

Packaged archive: `dist/job-application-checker.zip`

## Repository structure

```text
skills/
  job-application-checker/
    SKILL.md
    agents/openai.yaml
    references/application-profile.md
    references/workflow-tests.md

dist/
  job-application-checker.zip
```

## Privacy

Keep this repository private. Some skills can contain personal workflow preferences, professional profile details, and connector instructions.

## Adding another skill

Add each skill as its own folder inside `skills/`, then place its validated package inside `dist/` using the skill name as the ZIP filename.
