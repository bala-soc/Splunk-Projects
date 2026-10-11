# Screenshots and Evidence

Screenshots help reviewers see the investigation workflow and confirm that a project has visual documentation. Each case study currently includes one screenshot retained from an earlier repository version as a **visual reference**, not as proof that the revised examples were rerun.

## Replace the reference with fresh evidence

For each completed investigation, add screenshots from your own current Splunk run:

1. `01-data-ingested.png` — a few events with the actual index, sourcetype, and time range visible.
2. `02-query-results.png` — the current SPL query and its actual results.
3. `03-event-details.png` — a relevant event detail or follow-up correlation supporting the written conclusion.

Place the screenshots in a `screenshots/` folder inside the project or use the original GitHub image link. Link images in Markdown, for example:

```markdown
### Evidence: SPL query results
![Splunk query and results](screenshots/02-query-results.png)
```

## Quality requirements
- Use original screenshots from your own Splunk instance.
- Ensure screenshots match the SPL and field names in the current write-up.
- Show meaningful results and a readable query, with the time range visible when relevant.
- Redact usernames, sensitive IPs, email addresses, tokens, and other private information.
- Caption what each image demonstrates.
- Do not fabricate Splunk output or present an illustrative mock-up as observed results.
- If you have not rerun a case yet, keep the existing reference clearly labelled and do not claim that it validates the revised query.

A reviewer should be able to reproduce the query from the write-up and understand how the screenshot supports the conclusion.
