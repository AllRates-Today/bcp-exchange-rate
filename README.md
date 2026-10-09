# Banco Central del Paraguay Exchange Rates API — bcp-exchange-rate

[![npm version](https://img.shields.io/npm/v/bcp-exchange-rate.svg)](https://www.npmjs.com/package/bcp-exchange-rate)
[![license](https://img.shields.io/npm/l/bcp-exchange-rate.svg)](https://github.com/AllRates-Today/bcp-exchange-rate/blob/main/LICENSE)
[![zero dependencies](https://img.shields.io/badge/dependencies-0-brightgreen.svg)](https://www.npmjs.com/package/bcp-exchange-rate)
[![TypeScript](https://img.shields.io/badge/TypeScript-types%20included-3178C6.svg)](https://www.typescriptlang.org/)
[![USD/PYG today](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fallratestoday.com%2Fapi%2Fopen%2Fcentral-bank%2Fbcp%3Fsource%3DUSD%26target%3DPYG&query=%24.rate&label=USD%2FPYG%20published%20by%20Banco%20Central%20del%20Paraguay&color=0A7E8C&cacheSeconds=3600)](https://allratestoday.com/central-bank-rates-api/bcp/)
[![rate date](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fallratestoday.com%2Fapi%2Fopen%2Fcentral-bank%2Fbcp%3Fsource%3DUSD%26target%3DPYG&query=%24.rate_date&label=rate%20date&color=555&cacheSeconds=3600)](https://allratestoday.com/central-bank-rates-api/bcp/)

**Official Banco Central del Paraguay (Paraguay) daily exchange rates for Node.js and TypeScript. The published central bank rates behind tax filings, customs valuations, audits, and compliant invoicing — not market estimates, but the numbers Banco Central del Paraguay itself prints, every business day.**

## 🚀 Why this client?

- 🏛️ **Official published rates** — Banco Central del Paraguay's own table, with the publisher's own `rate_date` on every response
- 📅 **History back to 2016** — point-in-time tables and daily series for any past date
- 🔀 **Published vs derived, always flagged** — computed inverse/cross pairs carry `derived: true`, never mixed with official prints
- ⚡ **Zero dependencies** — pure ESM + CJS over global `fetch`; Node 18+, Bun, Deno, and edge runtimes
- 🔷 **Type-safe** — full TypeScript definitions shipped with the package
- 🧾 **Compliance-grade metadata** — `rate_type`, publication date, and source disclaimer on every response

> **Official rate, not mid-market:** every value here is a number Banco Central del Paraguay itself published, fixed once printed and carrying the central bank's own `rate_date` — what filings and audits require. Need the live mid-market rate for pricing or display instead? Use the [mid-market API](https://allratestoday.com/docs/) or [`@allratestoday/sdk`](https://www.npmjs.com/package/@allratestoday/sdk). The two can diverge by several percent.

## ⚡ Try it without a key

The latest Banco Central del Paraguay table is also served keyless, CORS-open and edge-cached, for evaluation, embeds and AI agents:

```bash
curl "https://allratestoday.com/api/open/central-bank/bcp?source=USD&target=PYG"
```

```js
const r = await fetch('https://allratestoday.com/api/open/central-bank/bcp').then((x) => x.json());
console.log(r.rate_date, r.rates.length); // the central bank's latest published table, no key
```

The open endpoint serves the *latest* table only and asks for a visible attribution link. The client below uses the keyed API, which adds point-in-time tables, history, and CSV/XML/Excel output.

## 📈 Latest published table

Today's full Banco Central del Paraguay table, straight from the central bank's latest publication. On GitHub it is refreshed by [a daily Action](.github/workflows/daily-table.yml) that reads the keyless endpoint above and commits only when the central bank publishes a new table; the copy on npm is as of the package's publish date.

<!-- daily-table:start -->
Published **2026-10-09** by Banco Central del Paraguay — 26 rates. Updated 2026-10-09.

| Base | Quote | Type | Rate |
| --- | --- | --- | ---: |
| AED | PYG | reference | 1550.4 |
| ARS | PYG | reference | 3.76 |
| AUD | PYG | reference | 3972.46 |
| BOB | PYG | reference | 480.55 |
| BRL | PYG | reference | 1142.3 |
| CAD | PYG | reference | 3989.96 |
| CHF | PYG | reference | 6852.55 |
| CLP | PYG | reference | 5.82 |
| CNY | PYG | reference | 850.91 |
| COP | PYG | reference | 1.78 |
| DKK | PYG | reference | 852.98 |
| EUR | PYG | reference | 6374.96 |
| GBP | PYG | reference | 7532.08 |
| JPY | PYG | reference | 35.96 |
| MXN | PYG | reference | 309.81 |
| NOK | PYG | reference | 595.2 |
| NZD | PYG | reference | 3193.46 |
| PEN | PYG | reference | 1647.71 |
| SEK | PYG | reference | 569.58 |
| SGD | PYG | reference | 4444.64 |
| TWD | PYG | reference | 178.65 |
| USD | PYG | reference | 5694.47 |
| UYU | PYG | reference | 141.98 |
| XAU | PYG | reference | 23823270.8 |
| XDR | PYG | reference | 7706.33 |
| ZAR | PYG | reference | 344.57 |

Source: [Official rates published by BCP, served by AllRatesToday](https://allratestoday.com/central-bank-rates-api/bcp/). Rates are as printed by the central bank; AllRatesToday is not affiliated with it.
<!-- daily-table:end -->

## 🔑 Get your API key

Get a free API key at [allratestoday.com/register](https://allratestoday.com/register) — no credit card required. Latest rates are on every plan, including free.

## 📦 Installation

```bash
npm install bcp-exchange-rate
```

```bash
yarn add bcp-exchange-rate
```

```bash
pnpm add bcp-exchange-rate
```

Requires Node 18+ (global `fetch`); also runs on Bun, Deno and edge runtimes. Also published under the org scope as [`@allratestoday/bcp-exchange-rate`](https://www.npmjs.com/package/@allratestoday/bcp-exchange-rate) — same code, same versions.

## 🏁 Quick start

```js
import { getRate } from 'bcp-exchange-rate';

const pair = await getRate('USD', 'PYG', { apiKey: 'art_live_...' });
console.log(pair.rate, pair.rate_date); // the official Banco Central del Paraguay rate, on the central bank's own date
```

## 📚 API reference

- [Latest pair rate](#latest-pair-rate) — one pair from the latest published table
- [Full published table](#full-published-table) — everything the central bank printed, in one call
- [Table for a date](#table-for-a-date) — the official table for an invoice or filing date
- [Daily time series](#daily-time-series) — one pair across a date range

---

### Latest pair rate

Free plan and up. Pairs the central bank does not print directly are resolved from its table and flagged (see *Published vs derived rates* below).

```js
const pair = await getRate('USD', 'PYG', { apiKey: 'art_live_...' });
```

**Response:**

```javascript
{
  bank: 'bcp',
  name: 'Banco Central del Paraguay',
  rate_date: '2026-10-08',   // Banco Central del Paraguay's own publication date
  source: 'USD',
  target: 'PYG',
  rate: 5706.18,
  rate_type: 'reference',
  derived: false,
  method: 'published',
  disclaimer: 'Official rates as published by the named central bank. On weekends/holidays the most recent published rate_date is returned.'
}
```

### Full published table

Free plan and up. The complete table for the latest publication date.

```js
import { getLatestRates } from 'bcp-exchange-rate';

const table = await getLatestRates({ apiKey: 'art_live_...' });
console.log(table.rate_date, table.rates.length);
```

**Response:**

```javascript
{
  bank: 'bcp',
  name: 'Banco Central del Paraguay',
  rate_date: '2026-10-08',
  rates: [
    { "base": "USD", "quote": "PYG", "type": "reference", "value": 5706.18 },
    // … the rest of the published table (26 currencies vs PYG)
  ],
  disclaimer: '…'
}
```

### Table for a date

Paid plans. The official table for any date since 2016 — weekends and holidays return the most recent published date, flagged via `published_on_requested_date`, which is exactly the in-force rate a filing needs.

```js
import { getRatesForDate } from 'bcp-exchange-rate';

const day = await getRatesForDate('2026-06-30', { apiKey: 'art_live_...' });
// Optionally narrow to one pair:
const one = await getRatesForDate('2026-06-30', { apiKey: 'art_live_...', source: 'USD', target: 'PYG' });
```

**Response:**

```javascript
{
  bank: 'bcp',
  requested_date: '2026-06-30',
  rate_date: '2026-06-30',                // the date actually published
  published_on_requested_date: true,      // false when a weekend/holiday fell back
  rates: [ /* the full table for that date */ ],
  disclaimer: '…'
}
```

### Daily time series

Paid plans. One resolved rate per publication date — ready for charting, revaluation runs, or audit workpapers.

```js
import { getHistory } from 'bcp-exchange-rate';

const series = await getHistory(
  { source: 'USD', target: 'PYG', from: '2026-01-01', to: '2026-10-08' },
  { apiKey: 'art_live_...' }
);
```

**Response:**

```javascript
{
  bank: 'bcp',
  source: 'USD',
  target: 'PYG',
  from: '2026-01-01',
  to: '2026-10-08',
  count: 152,
  rates: [
    // one entry per publication date
    { date: '2026-10-08', rate: 5706.18, rate_type: 'reference', derived: false, method: 'published' },
    // …
  ],
  disclaimer: '…'
}
```

Pass `{ symbol: 'USD' }` instead of `source`/`target` to get the raw published rows for one currency (all rate types, no pair resolution).

---

## 🗺️ Currencies covered

Banco Central del Paraguay currently publishes rates covering **26 currencies** against the PYG (as of the latest table):

🇦🇪 `AED` · 🇦🇷 `ARS` · 🇦🇺 `AUD` · 🇧🇴 `BOB` · 🇧🇷 `BRL` · 🇨🇦 `CAD` · 🇨🇭 `CHF` · 🇨🇱 `CLP` · 🇨🇳 `CNY` · 🇨🇴 `COP` · 🇩🇰 `DKK` · 🇪🇺 `EUR` · 🇬🇧 `GBP` · 🇯🇵 `JPY` · 🇲🇽 `MXN` · 🇳🇴 `NOK` · 🇳🇿 `NZD` · 🇵🇪 `PEN` · 🇸🇪 `SEK` · 🇸🇬 `SGD` · 🇹🇼 `TWD` · 🇺🇸 `USD` · 🇺🇾 `UYU` · `XAU` · `XDR` · 🇿🇦 `ZAR`

## 🏛️ Source

The Banco Central del Paraguay publishes its daily planilla de cotizaciones each afternoon: guaraní rates for around 26 currencies plus each currency's dollar cross. It is the official reference for Paraguayan banking, customs valuation, and accounting.

- Publisher's own page: [Planilla de cotizaciones](https://www.bcp.gov.py/webapps/web/cotizacion/monedas) · [www.bcp.gov.py](https://www.bcp.gov.py)
- Publication: every business day; the exact schedule, freshness status and any current delay are on the [Banco Central del Paraguay rates page](https://allratestoday.com/central-bank-rates-api/bcp/)
- Values are stored unmodified, with the publisher's own `rate_date` on every row — see the [methodology](https://allratestoday.com/official-rates-methodology/)

## 🧭 Reading the numbers

- `value` is always **quote currency per 1 unit of base currency** (`base: "EUR", quote: "USD", value: 1.15` means 1 EUR = 1.15 USD).
- Banco Central del Paraguay quotes **PYG per 1 unit of foreign currency** (e.g. `base: "USD", quote: "PYG"` means PYG per one US dollar).
- Need the other way round? Ask `getRate(target, source)` and the API inverts or crosses for you, flagged `derived: true` — never divide a published rate yourself in a compliance workflow.
- Precious-metal codes (`XAU`, `XAG`, `XPT`, `XPD`) are quoted **per troy ounce**.
- `rate_type` tells you which of the central bank's series a row belongs to (`reference` here); some publishers print buy/sell or several fixings for the same pair.

## 🧩 ERP & accounting systems

Loading the official Banco Central del Paraguay rate into an accounting system is a supported workflow, not a hack. Step-by-step guides with the direction each system expects:

- [Dynamics 365 Business Central](https://allratestoday.com/docs/integrations/business-central/) — built-in Currency Exchange Rate Service, no code
- [Xero](https://allratestoday.com/docs/integrations/xero/) · [QuickBooks Online](https://allratestoday.com/docs/integrations/quickbooks/) · [SAP S/4HANA and ECC](https://allratestoday.com/docs/integrations/sap/) · [Odoo](https://allratestoday.com/docs/integrations/odoo/)

The same keyed endpoints return `?format=csv`, `?format=xml` and `?format=xlsx`, and accept the key as `?api_key=` on the URL for importers that cannot send headers:

```bash
curl "https://allratestoday.com/api/v1/central-bank/bcp/latest?format=xml&api_key=art_live_..."
```

## 🤖 AI agents

- MCP server: `npx -y @allratestoday/central-bank-mcp` (stdio) or the hosted endpoint `https://allratestoday.com/api/mcp` — tools for official rates, history, cross-bank comparison and publication calendars
- Already using the general SDK or MCP server? Since 2026-10-01 [`@allratestoday/sdk`](https://www.npmjs.com/package/@allratestoday/sdk) 1.4+ has `officialRates('bcp')` and [`@allratestoday/mcp-server`](https://www.npmjs.com/package/@allratestoday/mcp-server) 0.6+ has a `get_official_rates` tool — both return this source's latest table with no key, so you can add it without a second dependency
- Claude Code plugin (no key): `/plugin marketplace add AllRates-Today/claude-code-plugin` then `/plugin install allratestoday@allratestoday` — bundles both MCP servers plus an `/official-rate bcp ...` command
- Machine-readable site guide: [llms.txt](https://allratestoday.com/llms.txt) · [for-ai-agents](https://allratestoday.com/for-ai-agents/)

## ⚖️ Published vs derived rates

If Banco Central del Paraguay does not print a pair directly, the API resolves it from the central bank's own table and says so — official and computed values are never confused:

| `method` | `derived` | Meaning |
| --- | --- | --- |
| `published` | `false` | The central bank printed this pair directly |
| `inverse` | `true` | Computed as 1 ÷ the published opposite direction |
| `cross` | `true` | Computed via PYG from two published rates |

## 🛡️ Error handling

Errors are thrown as `Error` with `status` (HTTP code) and `body` (the API's JSON error) attached:

```js
try {
  const pair = await getRate('USD', 'XXX', { apiKey: 'art_live_...' });
} catch (err) {
  console.log(err.message); // human-readable reason
  console.log(err.status);  // e.g. 404
}
```

| Status | Meaning |
| ------ | ------- |
| — | Missing `apiKey` (thrown before any request) |
| `400` | Malformed date or parameters |
| `401` | Invalid API key |
| `403` | Endpoint needs a [paid plan](https://allratestoday.com/pricing/) (historical dates & series) |
| `404` | Pair or date range not covered by Banco Central del Paraguay |
| `429` | Monthly quota exceeded |

## 🔷 TypeScript

Full definitions ship with the package — no `@types` install:

```ts
import type { LatestRates, PairRate, DatedRates, RateEntry, HistoryQuery, RequestOptions } from 'bcp-exchange-rate';
```

## 📦 CommonJS

```javascript
const { getRate } = require('bcp-exchange-rate');

getRate('USD', 'PYG', { apiKey: 'art_live_...' }).then((pair) => console.log(pair.rate));
```

## 💡 Quota tips

- Rates change once per business day — cache the published table locally and a small monthly quota goes a long way.
- Every request counts toward your AllRatesToday quota, shared across all AllRatesToday endpoints on your key.

## 📖 Methods reference

| Method | Plan | Description |
| ------ | ---- | ----------- |
| `getRate(source, target, { apiKey })` | Free | Latest rate for one pair, resolved from the published table |
| `getLatestRates({ apiKey })` | Free | The central bank's full latest published table |
| `getRatesForDate(date, { apiKey, source?, target? })` | Paid | The official table (or one pair) for a YYYY-MM-DD date |
| `getHistory({ symbol \| source+target, from?, to? }, { apiKey })` | Paid | Daily series since 2016 |

## 📥 Bulk data (no key)

Need the whole archive rather than an API call? The same published tables are mirrored daily as open data:

- Hugging Face: [AllRates/central-bank-exchange-rates](https://huggingface.co/datasets/AllRates/central-bank-exchange-rates) — one CSV per institution (`rates/bcp.csv`)
- Kaggle: [allratestoday/central-bank-exchange-rates](https://www.kaggle.com/datasets/allratestoday/central-bank-exchange-rates)
- CDN JSON: `https://cdn.jsdelivr.net/gh/AllRates-Today/central-bank-exchange-rates@main/data/bcp/latest.json`

## 🔗 Links

- [Banco Central del Paraguay rates page](https://allratestoday.com/central-bank-rates-api/bcp/) — live table, publication cadence, FAQ
- [All central bank sources](https://allratestoday.com/central-bank-rates-api/)
- [Package docs on the site](https://allratestoday.com/docs/sdk/bcp-exchange-rate/) · [ERP integration guides](https://allratestoday.com/docs/integrations/)
- [API documentation](https://allratestoday.com/docs/#central-bank) · [Interactive reference](https://allratestoday.com/api-reference/) · [Methodology](https://allratestoday.com/official-rates-methodology/)
- [Register (free)](https://allratestoday.com/register) · [Pricing](https://allratestoday.com/pricing/)
- [GitHub](https://github.com/AllRates-Today/bcp-exchange-rate)

## 📜 License

MIT
