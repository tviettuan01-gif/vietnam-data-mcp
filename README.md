# Vietnam Data MCP (donerightlabs)

Two pay-per-use data tools for Vietnam that AI agents can call through the Apify MCP server:

| Tool (Apify Actor) | What it does | Base price (pay-per-event) |
|---|---|---|
| [`donerightlabs/tender-intelligence`](https://apify.com/donerightlabs/tender-intelligence) | Searches Vietnam's national e-procurement portal (VNEPS, muasamcong.mpi.gov.vn) by keyword and returns open public tenders: notice number, title, bid closing date, province/district, investment field, as JSON. | $0.05 per run + $0.50 per keyword |
| [`donerightlabs/vn-einvoice-xml-normalizer`](https://apify.com/donerightlabs/vn-einvoice-xml-normalizer) | Converts Vietnamese VAT e-invoice XML files (Decree 123/2020, Circular 78/2021; any provider) into one unified JSON schema for bookkeeping agents. Reads only files the caller already has. Buyer personal data is hidden by default. | $0.01 per run + $0.05 per invoice |

Lower prices apply automatically on higher Apify plans (Bronze/Silver/Gold discounts). The Pricing tab of each Actor is the source of truth.

## Try it first (no setup)

Each tool has a published example run with sample input:

- Tender search example (keyword "thiết bị"): https://apify.com/donerightlabs/tender-intelligence/examples/tender-intelligence-task-tim-goi-thau-thiet-bi-vi-du-mau
- E-invoice example (synthetic sample invoice): https://apify.com/donerightlabs/vn-einvoice-xml-normalizer/examples/vn-einvoice-xml-normalizer-task

## Connect over MCP

This entry points to Apify's hosted MCP server, restricted to these two tools. Sign in with OAuth in the browser on first use:

```json
{
  "mcpServers": {
    "vietnam-data": {
      "url": "https://mcp.apify.com?tools=donerightlabs/tender-intelligence,donerightlabs/vn-einvoice-xml-normalizer"
    }
  }
}
```

If your client does not support OAuth, use an Apify API token:

```json
{
  "mcpServers": {
    "vietnam-data": {
      "url": "https://mcp.apify.com?tools=donerightlabs/tender-intelligence,donerightlabs/vn-einvoice-xml-normalizer",
      "headers": { "Authorization": "Bearer <APIFY_TOKEN>" }
    }
  }
}
```

Runs are billed to the connected Apify account at the prices above.

## Agent payments without an Apify account

Both tools are eligible for Apify's agentic payments: an AI agent can discover, run and pay per use with **x402** (USDC) or **Skyfire**, without creating an Apify account. See Apify's documentation for [x402](https://docs.apify.com/platform/integrations/x402) and [Skyfire](https://docs.apify.com/platform/integrations/skyfire).

## Example prompts

1. "Find open Vietnamese government tenders about medical equipment and list the three closing soonest." → `tender-intelligence` with keyword `thiết bị y tế`.
2. "Tìm các gói thầu công đang mở liên quan đến 'thi công sửa chữa' và cho tôi tên gói thầu, tỉnh và ngày đóng thầu." → `tender-intelligence`.
3. "Here are three Vietnamese e-invoice XML files. Normalize them and total the tax amounts per seller." → `vn-einvoice-xml-normalizer`.
4. "Đọc file XML hoá đơn điện tử này và cho tôi số hoá đơn, ngày lập, người bán, tổng thanh toán." → `vn-einvoice-xml-normalizer`.

Tip: a tender search takes about 1–2 minutes per keyword, so ask for 1–3 keywords per call.

## Data and privacy

- `tender-intelligence` returns package-level public procurement data only; it collects no personal data.
- `vn-einvoice-xml-normalizer` does not scrape and does not look anyone's invoice up. It only parses XML supplied by the caller. When the buyer looks like an individual (no tax code, a 12-digit personal ID used as tax code, or an ID-card/passport field present), the buyer's name, address and ID numbers are hidden by default, including in the raw-data output; the caller can switch this off for their own bookkeeping.
- The tools keep no data beyond the Apify run itself, which follows Apify's platform retention settings.

## Support

Issues and feedback: the Issues tab on each Actor's Apify Store page.

## Status

Independent tools by donerightlabs. Not affiliated with, or endorsed by, any Vietnamese government agency or e-invoice provider.
