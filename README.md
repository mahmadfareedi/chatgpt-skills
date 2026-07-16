# M. Ahmad's ChatGPT Skills

A private collection of reusable ChatGPT skills created for M. Ahmad.

## Skills

### Job Application Checker

Checks Gmail Sent mail before drafting a job application email. It detects previous applications using the recipient, company, and role title, reports when the earlier application was sent, and drafts a tailored email only when appropriate.

Source: `skills/job-application-checker/`

Packaged archive: `dist/job-application-checker.zip`

## Repository structure

```text
skills/
  job-application-checker/
    SKILL.md
    agents/openai.yaml
    references/application-profile.md

dist/
  job-application-checker.zip
```

## Privacy

Keep this repository private. Some skills can contain personal workflow preferences, professional profile details, and connector instructions.

## Adding another skill

Add each skill as its own folder inside `skills/`, then place its validated package inside `dist/` using the skill name as the ZIP filename.
