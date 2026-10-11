# Screenshots and Evidence

This repository uses screenshots as supporting evidence. Existing screenshots from earlier versions were removed when the write-ups were simplified; they should be restored only when they correspond to a real, reproducible Splunk run and are labelled accurately.

## What screenshots to add

For each protocol case study, add up to three screenshots under `screenshots/`:

1. `01-data-ingested.png` — Splunk search showing a few ingested events, with index, sourcetype, and time range visible.
2. `02-query-results.png` — the exact SPL query and resulting table/chart.
3. `03-investigation-evidence.png` — a relevant event detail or follow-up correlation supporting the written conclusion.

## Quality requirements
- Use original screenshots from your own Splunk instance.
- Show the query and meaningful results; crop away unrelated desktop areas.
- Redact usernames, public IPs where sensitive, tokens, email addresses, and other personal data.
- Do not create screenshots with fabricated data and present them as observed Splunk output.
- Ensure the query in the screenshot matches the query in the Markdown file.
- Include an image caption explaining what the screenshot demonstrates.
- If results are not yet available, leave the screenshot section marked as pending instead of showing a mock result.

## Add images in Markdown
After committing genuine screenshots to a project's `screenshots/` folder, link them like this:

```markdown
### Evidence: Query results
![Splunk query results](screenshots/02-query-results.png)
```
