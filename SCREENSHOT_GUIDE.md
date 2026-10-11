# Screenshot Guide

Use screenshots to make a case study easier to follow and to show evidence from your own Splunk investigation.

## Required screenshots for a completed case
1. **Event ingestion:** a small set of events with the actual index, sourcetype, and time range visible.
2. **Query and results:** the exact SPL shown in the write-up with the actual table/chart returned by Splunk.
3. **Investigation evidence:** a relevant event detail or follow-up query that supports the conclusion in the report.

## How to add screenshots
1. Run the query in your own Splunk instance using the dataset described in the case study.
2. Capture the search bar and meaningful output. Keep the time range visible where relevant.
3. Redact private usernames, email addresses, sensitive IPs, tokens, and host details.
4. Save the images as `screenshots/01-data-ingested.png`, `screenshots/02-query-results.png`, and `screenshots/03-event-details.png`.
5. Commit the images to the matching project folder or link them from the Markdown page with:

```markdown
### Evidence: Query results
![Splunk query and results](screenshots/02-query-results.png)
```

## Evidence integrity
The updated case-study pages intentionally do not reuse older screenshots because they have not been re-verified against the revised queries. I cannot run your Splunk environment through GitHub, and will not create mock result images that could be mistaken for real evidence.

Until new screenshots are captured, the text examples should be treated as query templates requiring validation, not proof of successful execution.
