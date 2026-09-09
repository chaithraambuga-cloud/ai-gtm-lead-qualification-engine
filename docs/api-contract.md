# Mock Enrichment API Contract

## Endpoint

`POST https://YOUR_N8N_HOST/webhook/mock-company-enrichment`

Authentication uses a private header credential managed by n8n. The implementation uses the header name `x-enrichment-api-key`; the value is never included in the workflow export.

## Request

```json
{
  "salesforceLeadId": "00QXXXXXXXXXXXXXXX",
  "website": "https://dataharbor-labs.example.com"
}
```

## Successful response

HTTP `200`

```json
{
  "success": true,
  "statusCode": 200,
  "salesforceLeadId": "00QXXXXXXXXXXXXXXX",
  "domain": "dataharbor-labs.example.com",
  "enrichmentSource": "Mock Company Enrichment API",
  "enrichedAt": "2026-09-09T09:46:43.993Z",
  "company": {
    "companyName": "DataHarbor Labs",
    "industry": "Technology",
    "numberOfEmployees": 1200,
    "annualRevenue": 180000000,
    "headquartersCountry": "India"
  }
}
```

## Unknown company

HTTP `404`

```json
{
  "success": false,
  "statusCode": 404,
  "errorCode": "COMPANY_NOT_FOUND",
  "errorMessage": "No enrichment profile found for domain: unknown-company.example.com",
  "salesforceLeadId": "TEST_UNKNOWN",
  "domain": "unknown-company.example.com"
}
```

## Missing website

HTTP `422`

```json
{
  "success": false,
  "statusCode": 422,
  "errorCode": "MISSING_DOMAIN",
  "errorMessage": "A company website is required for enrichment",
  "salesforceLeadId": "TEST_KAVYA"
}
```

