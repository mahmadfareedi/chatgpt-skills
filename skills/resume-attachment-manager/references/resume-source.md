# Resume Source Configuration

## Fixed source

- Repository: `mahmadfareedi/resume`
- Branch: `master`
- File path: `Muhammad_Ahmad_Senior_Data_Analyst.pdf`
- Attachment filename: `Muhammad_Ahmad_Senior_Data_Analyst.pdf`
- GitHub page: `https://github.com/mahmadfareedi/resume/blob/master/Muhammad_Ahmad_Senior_Data_Analyst.pdf`
- Public raw URL: `https://raw.githubusercontent.com/mahmadfareedi/resume/master/Muhammad_Ahmad_Senior_Data_Analyst.pdf`

## Freshness rule

Resolve the latest commit on `master` every time the attachment workflow runs, then fetch this exact path from that commit. The filename remains stable while its contents can change.

Do not rely on a previously downloaded local copy, browser cache, upload timestamp, or a URL that cannot identify the source commit.

## Retrieval preference

Use the first available option:

1. An MCP tool that resolves the latest branch commit and returns the PDF as a connector file reference.
2. The GitHub connector fetching the exact repository, path, and commit, followed by a supported conversion into a connector file reference.
3. A trusted deployed service that returns the PDF and the source commit SHA.

A URL alone is not enough for Gmail attachment creation when the mail tool requires a file reference.

## Validation

Accept the result only when:

- MIME type is `application/pdf`
- Filename is exactly `Muhammad_Ahmad_Senior_Data_Analyst.pdf`
- Content starts with `%PDF-`
- Size is greater than zero
- The source commit is the latest commit on `master`
