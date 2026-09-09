# Testing Results

## Dataset

Twelve synthetic Salesforce Leads were used to exercise different industries, company sizes, personas, intent levels, and completeness conditions.

## Verified workflow behavior

| Scenario | Expected behavior | Result |
| --- | --- | --- |
| Complete High Lead | Score, Gemini qualification, Salesforce PATCH | Passed |
| Incomplete Lead with successful enrichment | Enrich, merge, rescore, route | Passed at node level |
| Enriched Lead reaches High tier | Gemini qualification after enrichment | Passed at node level |
| Enriched Lead remains Medium | Salesforce write-back without Gemini | Passed at node level |
| Missing website | API returns 422 and Salesforce receives Failed state | Passed |
| Unknown company | API returns 404 with structured error | Passed |
| Complete Low Lead | Salesforce receives Skipped state | Passed |
| Gemini output parsing | Validate required strings, confidence range, arrays, and Lead ID | Passed |

## Representative results

| Lead | Before enrichment | After enrichment | Terminal path |
| --- | ---: | ---: | --- |
| Maya Rao | 100 High | Not required | Gemini and Completed |
| Priya Shah | 53 Medium | 100 High | Enrichment, Gemini, Completed |
| Neha Kapoor | 37 Low | 67 Medium | Enrichment and Completed without Gemini |
| Kavya Nair | 16 Low | Failed | Missing-domain failure |
| Oliver Smith | 28 Low | Not required | Skipped |

## Known validation limitation

During the final combined rerun, two test records retained previously enriched Salesforce fields, so they did not re-enter the enrichment branch. Every affected enrichment, rescoring, AI, and write-back node had already been verified independently with the intended payload. A clean full-regression run after resetting all source fields remains a planned hardening task.

