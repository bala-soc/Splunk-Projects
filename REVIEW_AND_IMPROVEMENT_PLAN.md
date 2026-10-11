# Splunk Projects — Review & Improvement Plan

This document records a quality review of the existing Splunk log-analysis exercises and prioritises the fixes needed to make them technically reliable and useful in SOC Analyst L1 interviews.

## Highest-priority fixes

1. **Use the correct data source in every query.** The FTP write-up contains many queries using `sourcetype=dnslog`; these must use the configured FTP sourcetype. Review the SMTP, DHCP, HTTP, and SSH queries as well for field/sourcetype consistency.
2. **Avoid broad index searches in final queries.** Prefer a documented lab index such as `index=security_lab` and specify the correct sourcetype. Change the examples only after matching your actual Splunk setup.
3. **Define the data schema.** For every sample dataset, record the exact source, file format, timestamp format, Splunk index, sourcetype, and available fields. A field such as `src_ip`, `fqdn`, `recipient_address`, or `leased_ip` may not exist unless automatic extraction or your own `rex` extraction creates it.
4. **Correct placeholder and unrelated fields.** Examples using fields like `attachment_type`, `session_id`, or `lease_renewal` should only be included when those fields exist in the dataset. Do not describe SMTP transport logs as if they necessarily contain message attachments or mailbox login activity.
5. **Explain what each query proves.** A count or time chart alone does not prove an attack. Document what is observed, plausible benign explanations, what needs corroboration, and the analyst's confidence.
6. **Replace generic conclusions with evidence-based findings.** Do not claim suspicious domains, brute force, tunnelling, or malicious activity was detected unless the dataset and results support that conclusion.
7. **Document reproducibility.** Include a brief setup summary, source attribution, sample event, query, expected output, actual tested output, and known limitations. Mark expected results as expected rather than observed.
8. **Repair consistency and typos.** Fix incorrect repository links, spelling, copied conclusions from another protocol, duplicated heading numbers, and inconsistent query formatting.

## Review by project

| Project | Priority review |
|---|---|
| DNS | Validate sourcetype and field extraction; the current generic regex matches words in raw text but does not reliably extract structured DNS fields. Check the query for DNS-specific fields before using `stats`. |
| FTP | Critical correction: several later queries reference `sourcetype=dnslog`. Use FTP sourcetype consistently, verify the event format, and use valid extracted fields before counting downloads/uploads or failures. |
| HTTP | Verify the actual access-log schema; review the HTTP status code, source/destination and URL extractions. Remove login/session fields unless they really exist in the data. Correct the copied FTP conclusion. |
| SSH | Confirm the data contains the expected fields and result values (for example, `failure`). Keep brute-force thresholds labelled as tuning examples and investigate successful logons after repeated failures if the data permits. |
| Tunnel/Zeek | Confirm the dataset is actually Zeek tunnel data and field names match its format. Counts and time charts show activity, not necessarily malicious tunnelling. Add a baseline and context before calling activity anomalous. |
| SMTP | Confirm schema and extracted sender/recipient fields. Remove attachment and account-login examples unless those fields are present in the chosen dataset; basic SMTP logs may not contain this information. |
| DHCP | Align field names: some queries use `leased_ip` while the extraction uses `assigned_ip`. Verify the event format and avoid interpreting frequent leases or client IDs as malicious without context. |

## Interview-ready format for each project

1. **Objective:** one clear SOC question.
2. **Dataset and setup:** source URL/name, timestamp range, index, sourcetype, and schema.
3. **Query:** the SPL that was tested, with short explanations.
4. **Validation:** sample event, result screenshot/output, and any test case.
5. **Findings:** specific observation, severity rationale, confidence, and limitations.
6. **False positives:** common legitimate reasons for the same pattern.
7. **Next steps:** the additional evidence the analyst should review or response recommended.

## Suggested build order

1. Fix the FTP sourcetype inconsistency and audit the other queries.
2. Pick the strongest one or two cases (SSH failed logons and HTTP suspicious request patterns are good candidates) and validate them end to end.
3. Add a short investigation report for each validated case.
4. Keep the remaining protocol exercises as learning notes until their queries and results have been verified.

> This is a review plan, not a claim that the queries have been executed in the owner's Splunk instance. Validate the dataset schema and every query before presenting results in a resume or interview.
