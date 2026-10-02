---
url: https://kunavo.com/use-cases/data-extraction
retrieved: 2026-10-02
command: firecrawl scrape https://kunavo.com/use-cases/data-extraction --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title: Extracting Structured Data From Invoices With One LLM Call
---
[Back to use cases](https://kunavo.com/use-cases)

Data Processing

# AI data extraction — structured output from PDFs, invoices, and unstructured text

The boring, valuable use case. Invoices, receipts, contracts, leads, resumes — anywhere you'd previously have built a parser, an LLM held to a JSON schema does it in 30 lines, more accurately, and you can ship in a day instead of a quarter.

[Get started](https://kunavo.com/app/signup) [See pricing](https://kunavo.com/pricing)

## Recommended models

- [claude-haiku-4-5](https://kunavo.com/models/claude-haiku-4-5)
- [claude-sonnet-5](https://kunavo.com/models/claude-sonnet-5)

Last reviewed onJuly 24, 2026.

## The boring valuable use case

For two decades, structured data extraction from unstructured documents was a quarter-long project: OCR pipeline, regex rules, edge case handling, layout templates per vendor. With an LLM held to a JSON schema, it's 30 lines of code, accurate on first pass, and ships in a day. The examples below run on Kunavo, an independent OpenAI-compatible gateway, but the pattern is the models' and works the same against any of them.

**Extracting invoices specifically?** This page is the cross-document overview. The dedicated [invoice data extraction guide](https://kunavo.com/guides/invoice-data-extraction-api) goes deeper on that one document type: how the older template-and-model approaches compare against a vision-LLM call, the full schema-constrained Python tutorial, the arithmetic guardrail, two-tier model routing, and per-invoice cost.

Categories where this works exceptionally well:

- [Invoices](https://kunavo.com/guides/invoice-data-extraction-api), receipts, purchase orders
- Contracts, legal agreements (extract parties, dates, obligations)
- Resumes / CVs (parse to ATS-friendly structure)
- Lead enrichment from email signatures or web pages
- Medical records, lab reports (with PII handling)
- Real estate listings, product catalogs
- Email triage and structured ingestion

## The core pattern in 30 lines

extract.py

```
import json
from openai import OpenAI
client = OpenAI(api_key="sk-kn-...", base_url="https://api.kunavo.com/v1")

# The schema is the output contract. Claude enforces a json_schema
# response_format (json_object it does not), so the reply has this shape
# unless max_tokens cuts it off (finish_reason == "length").
STR = {"type": ["string", "null"]}
NUM = {"type": ["number", "null"]}
INVOICE = {
    "type": "object",
    "properties": {
        "vendor": {"type": "string"},
        "invoice_number": STR, "date_iso": STR, "due_date_iso": STR,
        "currency": STR, "subtotal": NUM, "tax": NUM, "total": NUM,
        "line_items": {"type": "array", "items": {
            "type": "object",
            "properties": {"description": {"type": "string"},
                           "qty": NUM, "unit_price": NUM, "amount": NUM},
            "required": ["description", "qty", "unit_price", "amount"],
            "additionalProperties": False,
        }},
    },
    "required": ["vendor", "invoice_number", "date_iso", "due_date_iso",\
                 "currency", "subtotal", "tax", "total", "line_items"],
    "additionalProperties": False,
}
RESPONSE_FORMAT = {"type": "json_schema",
                   "json_schema": {"name": "invoice", "schema": INVOICE}}
RULES = "Extract the invoice. Use null for missing fields. Dates in ISO 8601."

# Extract structured fields from an invoice PDF (after OCR)
def extract_invoice(ocr_text: str) -> dict:
    resp = client.chat.completions.create(
        model="claude-haiku-4-5",
        messages=[\
            {"role": "system", "content": RULES},\
            {"role": "user", "content": ocr_text},\
        ],
        response_format=RESPONSE_FORMAT,
        max_tokens=1200,
    )
    return json.loads(resp.choices[0].message.content)

# Extract from an image directly (no OCR step needed)
def extract_invoice_from_image(image_url: str) -> dict:
    resp = client.chat.completions.create(
        model="claude-haiku-4-5",   # vision + an enforced schema
        messages=[\
            {"role": "system", "content": RULES},\
            {"role": "user", "content": [\
                {"type": "text", "text": "Extract this invoice:"},\
                {"type": "image_url", "image_url": {"url": image_url}},\
            ]},\
        ],
        response_format=RESPONSE_FORMAT,
        max_tokens=1200,
    )
    return json.loads(resp.choices[0].message.content)
```

Two flows: text-only (after a separate OCR step) and vision-direct (a vision model reads the image and outputs JSON in one call). The vision path is faster to build but slightly more expensive per call; the OCR-then-LLM path is cheaper at scale because OCR is one-time cost per page.

## Accuracy benchmarks

On a public invoice dataset (1,000 invoices from 50 vendors), JSON mode with a 200-word system prompt:

- **Claude Haiku 4.5**: 96% field-level accuracy
- **Claude Sonnet 4.6**: 98% field-level accuracy
- **Traditional templating**: 80-90% on known vendors, 0% on new

The LLM handles new vendor layouts zero-shot. Add 2-3 example pairs in the system prompt (few-shot) and Haiku approaches Sonnet's accuracy at a fraction of the cost.

## Cost per document

- Invoice (~2K input tokens, ~500 output): Haiku ~$0.003, Sonnet ~$0.02
- One-page contract (~5K input): Haiku ~$0.005, Sonnet ~$0.04
- 10-page contract (~50K input, structured summary out): Sonnet ~$0.30
- Resume (~3K input): Haiku ~$0.003
- Receipt image with vision: Haiku, about an invoice's cost — the image counts as roughly 1.5K input tokens

Processing 10,000 invoices/month: ~$30 with Haiku. The closest commercial alternative (Rossum, AWS Textract + post-processing) runs ~$2,000-5,000/month for the same volume.

## The 5 patterns that keep accuracy high

- **Explicit null handling**: tell the model to use`null` for missing fields, not "N/A" or empty strings. Downstream code can distinguish "absent" from "intentionally blank"
- **ISO 8601 dates**: state explicitly. The model otherwise picks regional formats and downstream parsing breaks
- **Currency as ISO code**: "USD" not "$"; "EUR" not "€". Avoid ambiguity ($ for USD vs CAD vs AUD)
- **Validate the JSON**: use Pydantic / Zod to enforce your schema. If invalid, re-prompt with the error
- **Spot-check 1% manually for a week**, then 0.1% ongoing. Track field-level accuracy, not just record-level

## When to use which model

| Document type | Recommended model |
| --- | --- |
| Simple structured (invoice, receipt) | Claude Haiku 4.5 |
| Long contracts / agreements | Claude Sonnet 5 (handles long context) |
| Vision-direct (PDF without OCR) | Claude Haiku 4.5, or Claude Sonnet 5 for large pages |
| High-stakes (legal, medical) | Claude Sonnet 5 + human verification |
| Bulk ingestion (100K+/day) | Haiku 4.5 + few-shot examples + caching |

## Compliance considerations

For documents containing PII (invoices have names, addresses; medical records have everything), pseudonymize before extraction or use Zero Data Retention upstream. See the [compliance guide](https://kunavo.com/guides/compliance) for region-specific patterns and the [DSGVO deep dive](https://kunavo.com/de/blog/dsgvo-konformer-llm-einsatz) for the German playbook.

Start: [/app/signup](https://kunavo.com/app/signup) — pay-as-you-go from a $10 top-up covers ~3,000 invoice extractions, and your balance never expires. Read the chat docs at [/docs/chat](https://kunavo.com/docs/chat#json-output) for what`response_format` enforces on each model family, and for tool-use patterns.

## FAQ

### How much does it cost to extract data from a document with an LLM?

About $0.003–$0.005 per document on Claude Haiku 4.5 and about $0.02–$0.04 on Claude Sonnet 4.6. Processing 10,000 invoices a month costs roughly $30, against $2,000–$5,000 for commercial extraction services.

### How accurate is zero-shot LLM data extraction?

95–98% field-level accuracy zero-shot, in about 30 lines of code — accurate enough to replace an OCR-plus-regex pipeline.

### Which model should I use for document extraction?

Simple structured documents such as invoices and receipts go to Claude Haiku 4.5. Long contracts go to Claude Sonnet 4.6. Documents read directly as images go to Claude Haiku 4.5, or Sonnet 4.6 for large pages.

### How do I keep extraction accurate in production?

Five patterns: explicit null handling, ISO 8601 dates, ISO currency codes, schema validation with a re-prompt on invalid output, and a manual spot-check — 1% of outputs in the first week, 0.1% ongoing. Track field-level accuracy rather than record-level.
