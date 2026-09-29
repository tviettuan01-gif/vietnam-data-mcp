# Vietnam Data MCP (donerightlabs)

A pay-per-use data tool for Vietnam that AI agents can call through the Apify MCP server:

| Tool (Apify Actor) | What it does | Base price (pay-per-event) |
|---|---|---|
| [`donerightlabs/tender-intelligence`](https://apify.com/donerightlabs/tender-intelligence) | Searches Vietnam's national e-procurement portal (VNEPS, muasamcong.mpi.gov.vn) by keyword and returns open public tenders: notice number, title, bid closing date, province/district, investment field, as JSON. | $0.05 per run + $0.50 per keyword |

Lower prices apply automatically on higher Apify plans (Bronze/Silver/Gold discounts). The Pricing tab of the Actor is the source of truth.

> **Note (29 Sep 2026):** the former second tool, `vn-einvoice-xml-normalizer`, has been temporarily withdrawn from the Apify Store while its compliance with Vietnam's rules on personal-data processing services is reviewed.

## Try it first (no setup)

A published example run with sample input:

- Tender search example (keyword "thiết bị"): https://apify.com/donerightlabs/tender-intelligence/examples/tender-intelligence-task-tim-goi-thau-thiet-bi-vi-du-mau

## Connect over MCP

This entry points to Apify's hosted MCP server, restricted to this tool. Sign in with OAuth in the browser on first use:

```json
{
  "mcpServers": {
    "vietnam-data": {
      "url": "https://mcp.apify.com?tools=donerightlabs/tender-intelligence"
    }
  }
}
```

If your client does not support OAuth, use an Apify API token:

```json
{
  "mcpServers": {
    "vietnam-data": {
      "url": "https://mcp.apify.com?tools=donerightlabs/tender-intelligence",
      "headers": { "Authorization": "Bearer <APIFY_TOKEN>" }
    }
  }
}
```

Runs are billed to the connected Apify account at the prices above.

## Agent payments without an Apify account

The tool is eligible for Apify's agentic payments: an AI agent can discover, run and pay per use with **x402** (USDC) or **Skyfire**, without creating an Apify account. See Apify's documentation for [x402](https://docs.apify.com/platform/integrations/x402) and [Skyfire](https://docs.apify.com/platform/integrations/skyfire).

## Example prompts

1. "Find open Vietnamese government tenders about medical equipment and list the three closing soonest." → `tender-intelligence` with keyword `thiết bị y tế`.
2. "Tìm các gói thầu công đang mở liên quan đến 'thi công sửa chữa' và cho tôi tên gói thầu, tỉnh và ngày đóng thầu." → `tender-intelligence`.

Tip: a tender search takes about 1–2 minutes per keyword, so ask for 1–3 keywords per call.

## Data and privacy

- `tender-intelligence` returns package-level public procurement data only; it collects no personal data.
- The tool keeps no data beyond the Apify run itself, which follows Apify's platform retention settings.

## Support

Issues and feedback: the Issues tab on the Actor's Apify Store page.

## Status

Independent tools by donerightlabs. Not affiliated with, or endorsed by, any Vietnamese government agency.
