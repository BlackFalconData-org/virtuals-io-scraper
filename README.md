# Virtuals Protocol AI Agent Scraper [Just 💰$0.9]

Extract structured data from [virtuals.io](https://virtuals.io) — AI agents from virtuals.io by keyword, status or chain. Each row carries the token address, market cap and holder count the source publishes. Optional detail lookups add live USD price, market cap and FDV. Incremental mode reports only new or changed agents between runs.

**[Virtuals Protocol AI Agent Scraper [Just 💰$0.9] on Apify →](https://apify.com/blackfalcondata/virtuals-io-scraper?fpr=1h3gvi)**

---

## 🚀 How to use this actor

> ### 💚 $5 free Apify credits — every month
> No credit card required. No commitment. Cancel anytime.

### 👉 [Sign up free on Apify →](https://console.apify.com/sign-up?fpr=1h3gvi)

1. **Click sign up** — pick GitHub, Google, or email; takes ~30 seconds
2. **Open this actor** — input is pre-filled with a working example
3. **Click Start** — export results as JSON, CSV, or Excel

Your **$5 monthly platform credit** is enough to run this actor right away — and again every month — scraping typically several hundred to several thousand results per run, depending on your input.

## Key features

**Search with filters** — Search by keyword. Filter by 🚦 agent status, ⛓️ chain, 📝 description format, and more.

**Detail enrichment** — Fetch full descriptions, structured metadata for each company.

**Incremental mode** — Only get new or changed companies since your last run. Content hash per company — no duplicates, no re-processing.

**Change classification** — Track cross-run duplicate detection across runs. Build audit trails of how companies evolve over time.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Description truncation** — Cap description length per ${NOUN} to control output size and cost.

**Result cap** — Stop after N companies (up to 1.000). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every company returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases

**Data pipeline automation**
Integrate with your ETL pipeline to collect structured companies from virtuals.io on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor companies, track trends, and analyze market dynamics with structured, deduplicated data from virtuals.io.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired ${NOUNS}. Perfect for price-tracking, churn analysis, and alerting pipelines.

**AI / LLM training data**
Structured JSON per company is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

---

## Quick start

```json
{
  "query": "ai agent",
  "maxResults": 100,
  "includeDetails": true,
  "descriptionMaxLength": 0,
  "compact": false,
  "excludeEmptyFields": false,
  "incrementalMode": false,
  "skipReposts": false,
  "notifyOnlyChanges": false,
  "notificationLimit": 5,
  "descriptionFormat": "all"
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | Matched against agent name or token symbol (case-insensitive). Leave empty to browse all agents. Use a JSON array for multiple searches, e.g. ["trading","gaming"]. |
| `status` | enum | `""` | Only return agents at this stage of their lifecycle. Leave empty for all. Use a JSON array to cover several. |
| `chain` | enum | `""` | Only return agents whose token lives on this chain. Leave empty for all chains. |
| `maxResults` | integer | `100` | Maximum total results (0 = unlimited). |
| `startUrls` | array | `[]` | Paste raw search URLs from the target site. Each URL becomes its own search task; results are merged and deduped by agent across all URLs. When provided, startUrls REPLACE the search fields (each supported URL becomes one task; unsupported URLs are skipped, and if none is supported the run stops with an input error). |
| `includeDetails` | boolean | `true` | Also fetch each agent's live USD market data (price, market cap, FDV, reserves, 24h net buy volume). |
| `descriptionMaxLength` | integer | `0` | Truncate each agent description to N characters. 0 = no truncation. |
| `compact` | boolean | `false` | Core fields only (for AI-agent/MCP workflows). |
| `excludeEmptyFields` | boolean | `false` | Drop null, empty-string, and empty-array fields from each record before push. Smaller payloads for AI agents and dashboards. |
| `incrementalMode` | boolean | `false` | Compare against previous run state. stateKey is optional — defaults to a value derived from your search inputs (queries, status, chain, startUrls) so different filter sets never share state. |
| `stateKey` | string | — | Optional. Stable identifier for the tracked search universe. Leave empty to auto-generate from search inputs. |
| `skipReposts` | boolean | `false` | When incremental, skip agents whose content matches an agent that disappeared in a prior run (cross-run duplicate detection). |
| `notifyOnlyChanges` | boolean | `false` | When Incremental Mode is on, only send notifications for NEW and UPDATED agents. Has no effect outside incremental mode. |
| `notificationLimit` | integer | `5` | Maximum number of listings included in each notification message (1–20). |
| `telegramToken` | string | — | Telegram bot token (from @BotFather). Required for Telegram notifications. |
| `telegramChatId` | string | — | Telegram chat or channel ID (e.g. "-100123456789"). Required when telegramToken is set. |
| `discordWebhookUrl` | string | — | Discord incoming webhook URL. Server Settings → Integrations → Webhooks → New Webhook. |
| `slackWebhookUrl` | string | — | Slack incoming webhook URL. api.slack.com/messaging/webhooks. |
| `whatsappPhoneNumberId` | string | — | Your WhatsApp Business phone-number ID (numeric, from Meta dashboard). Required when whatsappAccessToken is set. |
| `whatsappAccessToken` | string | — | WhatsApp Cloud API permanent access token (System User token from Meta Business). Recipient must have messaged the business number within the last 24h (service-conversation window — free since Nov 2024). |
| `whatsappTo` | string | — | Recipient phone in E.164 format without + (e.g. "436641234567"). Recipient must have messaged your business number within last 24h. |
| `webhookUrl` | string | — | Receives a JSON POST with {metadata, items} after each run. Universal escape hatch for n8n / Make / Zapier / custom backends. |
| `webhookHeaders` | object | — | Optional JSON object of custom headers (e.g. {"Authorization":"Bearer ..."}). |
| `appConnector` | string | — | Optional. Pick a connected app under Settings → API & Integrations to receive your results (including any contact details). Best-effort across MCP connectors as Apify expands its catalog. |
| `mcpIssueTeam` | string | — | Only when the connected app is an issue tracker: the team (name or ID) the summary issue is created under, if that app requires one. |
| `descriptionFormat` | enum | `"all"` | Choose which representation of the listing description to include. `all` keeps every variant; the others keep only the selected one. |

---

## Output fields

Every company returns the same 61-field schema. Missing values are `null` — never omitted.

- `_type`
- `rank`
- `name`
- `symbol`
- `category`
- `role`
- `chain`
- `status`
- `description`
- `token_address`
- `dao_address`
- `price_change_pct_5m`
- `price_change_pct_1h`
- `price_change_pct_6h`
- `price_change_pct_24h`
- `momentum_label`
- `volume_usd_5m`
- `volume_usd_1h`
- `volume_usd_6h`
- `volume_usd_24h`
- `tvl_usd`
- `market_cap_virtual`
- `fdv_virtual`
- `liquidity_usd`
- `holder_count`
- `holder_count_change_pct_24h`
- `top_10_holder_pct`
- `dev_holding_pct`
- `mindshare`
- `cores`
- `launched_at`
- `created_at`
- `agent_url`
- `portalUrl`
- `token_explorer_url`
- `twitter_url`
- `is_verified`
- `agent_id`
- `uid`
- `website_url`
- `image_url`
- `pre_token_address`
- `lp_address`
- `wallet_address`
- `total_supply`
- `circulating_supply`
- `token_price_usd`
- `virtual_price_usd`
- `market_cap_usd`
- `fdv_usd`
- `market_cap_usd_derived`
- `reserve_usd`
- `net_buy_volume_usd_24h`
- `listingId`
- `searchQuery`
- `contentQuality`
- `detailFetched`
- `scrapedAt`
- `source`
- `contentHash`
- `changeType`

---

## Sample output

One object per company. Here is a real example from a production run:

```json
{
  "_type": "agent",
  "rank": 1,
  "name": "Satoshi AI agent",
  "symbol": "SAINT",
  "category": "IP MIRROR",
  "role": "INFORMATION",
  "chain": "BASE",
  "status": "AVAILABLE",
  "description": "Discover everything about #blockchain and #cryptocurrency with the $SAINT AI Agent. Chat as if you’re speaking directly to #SatoshiNakamoto — market trend, On-chain data, market in…",
  "token_address": "0x7588880d9c78E81FAde7b7e8DC0781E95995a792",
  "dao_address": "0xb67012F32C0879aA61aa50aF61E988d41A014E31",
  "price_change_pct_5m": 0
}
```

*Truncated — full records contain 61 fields. See Output fields for the complete schema.*

**[Try Virtuals Protocol AI Agent Scraper [Just 💰$0.9] now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/virtuals-io-scraper?fpr=1h3gvi)**

---

## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.01 |
| Result | $0.0009 |

See the [actor on Apify](https://apify.com/blackfalcondata/virtuals-io-scraper?fpr=1h3gvi) for current pricing.

---

## FAQ

**How do I scrape virtuals.io?**
Use this actor on Apify to extract structured data from virtuals.io. Configure your search query and filters in the input, then click Start — no coding required.

**How do I get virtuals.io data as JSON, CSV, or Excel?**
The actor writes each company to Apify's dataset. Download as JSON, CSV, or Excel from the Console, stream via the API, or push to Make, Zapier, Airbyte, or Keboola.

**Is it legal to scrape virtuals.io?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check virtuals.io's terms of service for your specific use case.

**How much does it cost?**
Pay-per-event pricing — you only pay for ${NOUNS} extracted. Apify's free $5 credit is enough to run thousands of results before you pay anything.

**How does incremental mode work?**
Each company gets a content hash. On subsequent runs, only new or changed companies are emitted — saving time, compute, and storage. Expired companies can be tracked separately.

**Do I need an API key or credentials?**
No. Just sign up for Apify, paste your input, and click Start. No credit card required.

---

## Related products by Black Falcon Data

[Browse all Black Falcon Data actors →](https://apify.com/blackfalcondata?fpr=1h3gvi)

---

## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. Sign up — $5 platform credit included
2. Open [Virtuals Protocol AI Agent Scraper [Just 💰$0.9]](https://apify.com/blackfalcondata/virtuals-io-scraper?fpr=1h3gvi) and configure your input
3. Click **Start** — export results as JSON, CSV, or Excel

Need more later? [See Apify pricing](https://apify.com/pricing?fpr=1h3gvi).

---

## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---

*Last updated: 2026 10*
