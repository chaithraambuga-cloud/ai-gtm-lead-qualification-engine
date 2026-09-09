# ICP Scoring Logic

The scoring model is deterministic and totals 100 points. It executes before any Gemini call and executes again after successful enrichment.

## Industry fit

15 points for Technology, Finance, Banking, Insurance, Consulting, or Telecommunications; otherwise 0.

## Company size

| Employees | Points |
| ---: | ---: |
| 1,000 or more | 15 |
| 200-999 | 10 |
| 50-199 | 5 |
| Below 50 or unknown | 0 |

## Annual revenue

| Annual revenue | Points |
| ---: | ---: |
| 100 million or more | 10 |
| 25 million-99,999,999 | 7 |
| 5 million-24,999,999 | 3 |
| Below 5 million or unknown | 0 |

## Buyer persona

| Title signal | Points |
| --- | ---: |
| Chief, CDO, CTO, CIO, VP, Vice President, Head, or Director | 25 |
| Manager, Lead, or Senior | 15 |
| Other populated title | 5 |
| Missing title | 0 |

## Intent signal

| Intent score | Points |
| ---: | ---: |
| 80-100 | 25 |
| 60-79 | 18 |
| 40-59 | 10 |
| 0-39 | 3 |

## Data completeness

The Lead starts with 10 points. Each missing enrichment field deducts 2.5 points. The four evaluated fields are Website, Industry, Number of Employees, and Annual Revenue.

## Tier and AI gate

- High: score >= 70
- Medium: score >= 40 and < 70
- Low: score < 40
- Gemini is invoked only when score >= 70 and no required enrichment field is missing.

