# Screenshot Guide

Use screenshots to document the key steps and findings in each Splunk case study.

## Recommended screenshots
1. **Event ingestion:** sample events with the index, sourcetype, and time range visible.
2. **Query results:** the SPL used in the case study alongside its output.
3. **Investigation evidence:** an event detail or follow-up query supporting the written findings.

## Add screenshots
1. Run the query in Splunk using the dataset described in the case study.
2. Capture the search bar and relevant output, keeping the time range visible where useful.
3. Redact private usernames, email addresses, sensitive IPs, tokens, and host details.
4. Save images in a `screenshots/` folder in the relevant project directory.
5. Embed them in Markdown, for example:

```markdown
### Query results
![Splunk query and results](screenshots/02-query-results.png)
```

Make sure screenshots correspond to the query and conclusions in the case study.