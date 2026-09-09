# Setup Guide

## Required accounts

- Salesforce Developer environment
- n8n workspace
- Google AI Studio API key

## Credentials

Create credentials inside n8n rather than entering secrets in workflow fields:

1. Salesforce OAuth2 API credential using the External Client App consumer key and secret.
2. Google Gemini API credential using the Google AI Studio key.
3. Header Auth credential for the mock enrichment webhook using `x-enrichment-api-key` and a private random value.

After import, reselect these credentials in all applicable nodes because sanitized exports intentionally omit credential IDs.

## Salesforce query

The main workflow queries Leads where `Enrichment_Status__c = 'Pending'`. Confirm all custom field API names match the data model before execution.

## Safe activation order

1. Import and activate the mock enrichment API.
2. Update the main workflow's Salesforce and n8n host placeholders.
3. Test the main workflow using Manual Trigger and synthetic records.
4. Add record-locking, centralized error handling, and verified retries.
5. Activate the main schedule only after the production-hardening checks pass.

