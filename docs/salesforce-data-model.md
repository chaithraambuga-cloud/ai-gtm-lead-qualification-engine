# Salesforce Lead Data Model

The workflow uses standard Salesforce Lead fields for firmographic and contact data and eleven custom fields for scoring, orchestration state, AI output, and auditability.

| Field API name | Suggested type | Purpose |
| --- | --- | --- |
| `Intent_Score__c` | Number 3,0 | Upstream buying-intent signal from 0 to 100 |
| `ICP_Score__c` | Number 3,0 | Deterministic qualification score |
| `ICP_Tier__c` | Picklist | High, Medium, or Low |
| `Enrichment_Status__c` | Picklist | Pending, Processing, Completed, Failed, or Skipped |
| `AI_Qualification_Summary__c` | Long Text Area | Gemini-generated fit summary |
| `AI_Next_Best_Action__c` | Long Text Area | Gemini-generated sales action |
| `AI_Confidence_Score__c` | Number | Validated Gemini confidence from 0 to 100 |
| `Enrichment_Source__c` | Text 100 | Data and processing source |
| `Last_Enriched_At__c` | Date/Time | Enrichment or AI-processing timestamp |
| `Workflow_Run_ID__c` | Text 100 | n8n execution identifier for traceability |
| `Enrichment_Error__c` | Long Text Area | Structured failure code and message |

## Standard fields used

`Id`, `FirstName`, `LastName`, `Company`, `Title`, `Email`, `Website`, `Industry`, `NumberOfEmployees`, `AnnualRevenue`, `Country`, `LeadSource`, `Status`, and `Description`.

`Description` is selected by SOQL but is not used in the `WHERE` clause because Salesforce Long Text Area fields are not filterable in a standard query.

## State model

| State | Meaning |
| --- | --- |
| Pending | Eligible for retrieval by the main SOQL query |
| Processing | Reserved for a future record-locking enhancement |
| Completed | Qualification or enrichment completed successfully |
| Failed | Enrichment could not be completed |
| Skipped | Deterministic score was below the action threshold |

