# Vietnam Data MCP (donerightlabs)

Public procurement data from **Vietnam's national e-procurement system** (VNEPS, [muasamcong.mof.gov.vn](https://muasamcong.mof.gov.vn)) for AI agents, through Apify's hosted MCP server. Pay per use.

One tool, [`donerightlabs/tender-intelligence`](https://apify.com/donerightlabs/tender-intelligence), covers the full tender lifecycle:

| `recordType` | Ask it | Returns |
|---|---|---|
| `plans` | "What is the government planning to buy?" | Procurement plans (KHLCNT), published before the tender notice, with planned packages and estimated prices |
| `notices` (default) | "Which tenders are open?" | Tender notices: package name, closing date, location, field |
| `awards` | "Who won, and at what price?" | Award results by keyword, nationwide: winning contractor, tax ID, price in VND, duration, lots, joint ventures |
| `awards_by_date` | "All awards in Gia Lai last week?" | Every award result in one province within a date range, no keyword |

## Pricing

Pay-per-event, billed to the connected Apify account:

- $0.05 per run
- $0.15 per keyword searched (or per date-range search in `awards_by_date`)
- $0.03 per package whose award result is read in full

One keyword costs $0.20. Search fees apply only after a search succeeds. Lower rates apply on higher Apify plans. The Actor's [Pricing tab](https://apify.com/donerightlabs/tender-intelligence) is the source of truth.

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

## Agent payments without an Apify account

The tool is eligible for Apify's agentic payments: an AI agent can discover, run and pay per use with **x402** (USDC) or **Skyfire**, without creating an Apify account. See Apify's documentation for [x402](https://docs.apify.com/platform/integrations/x402) and [Skyfire](https://docs.apify.com/platform/integrations/skyfire).

## Example prompts

1. "Find open Vietnamese government tenders for medical equipment and list the three closing soonest." → `notices`, keyword `thiết bị y tế`.
2. "Tìm kế hoạch lựa chọn nhà thầu liên quan đến 'camera giám sát'." → `plans`.
3. "Who won recent packages for demining work, and at what price?" → `awards`, keyword `rà phá bom mìn`.
4. "List all contract awards published in Tỉnh Gia Lai from 12/10/2026 to 19/10/2026." → `awards_by_date`.

Tips for agents: translate the topic into short Vietnamese keywords with diacritics; ask for 1–3 keywords per call (about 1–2 minutes each); show the user the maximum cost first; records with a `trang_thai` field are status messages, not tenders.

Published example run (keyword "thiết bị"): https://apify.com/donerightlabs/tender-intelligence/examples/tender-intelligence-task-tim-goi-thau-thiet-bi-vi-du-mau

## Data and privacy

- Source: public pages of VNEPS. Vietnam's Law on Bidding 22/2023/QH15, Article 51(1), requires the system to ensure public, unrestricted access to information published on it.
- Award results list winning contractors (usually organizations) and their tax IDs. Winners that look like individuals (12-digit personal ID as tax code, or a personal name with no organization marker) are redacted, and phone numbers/emails in free-text fields are masked. This is pattern-based and cannot guarantee that no personal detail ever appears.
- Runs and results stay in the caller's Apify account under Apify's retention settings. donerightlabs does not access them.
- Policy: https://donerightlabs.tviettuan01.workers.dev/chinh-sach

## Support

Issues and feedback: https://apify.com/donerightlabs/tender-intelligence/issues

## Status

Independent tool by donerightlabs. Not affiliated with, or endorsed by, any Vietnamese government agency or by Apify.
