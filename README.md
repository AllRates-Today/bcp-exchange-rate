# Banco Central del Paraguay Exchange Rate API client

Official **Banco Central del Paraguay** (Paraguay) daily exchange rates in Node.js / TypeScript — 26 currencies against the PYG, with history back to 2016. Zero dependencies, works in Node 18+, Bun, Deno, and edge runtimes (uses global `fetch`).

These are the *published central bank rates* required for tax filings, customs valuations, audits, and compliant invoicing — not moving market rates. Every response carries the publisher's own publication date.

Powered by [AllRatesToday](https://allratestoday.com/central-bank-rates-api/bcp/). Get a free API key at [allratestoday.com/register](https://allratestoday.com/register) — no credit card required.

## Install

```bash
npm install bcp-exchange-rate
```

## Quick start

```js
import { getRate, getLatestRates } from 'bcp-exchange-rate';

// One pair at the official Banco Central del Paraguay rate
const pair = await getRate('USD', 'PYG', { apiKey: 'art_live_...' });
console.log(pair.rate, pair.rate_date); // e.g. USD -> PYG on the bank's own date

// The bank's full published table
const table = await getLatestRates({ apiKey: 'art_live_...' });
console.log(table.rate_date, table.rates.length);
```

## Historical data (paid plans)

```js
import { getRatesForDate, getHistory } from 'bcp-exchange-rate';

// The official table for an invoice date — weekends/holidays return the
// most recent published date, flagged via published_on_requested_date.
const day = await getRatesForDate('2026-06-30', { apiKey: 'art_live_...' });

// Daily series for one pair
const series = await getHistory(
  { source: 'USD', target: 'PYG', from: '2026-01-01' },
  { apiKey: 'art_live_...' }
);
```

## Currencies covered

Banco Central del Paraguay currently publishes rates covering **27 currencies** (as of the latest table):

`AED` · `ARS` · `AUD` · `BOB` · `BRL` · `CAD` · `CHF` · `CLP` · `CNY` · `COP` · `DKK` · `EUR` · `GBP` · `JPY` · `MXN` · `NOK` · `NZD` · `PEN` · `PYG` · `SEK` · `SGD` · `TWD` · `USD` · `UYU` · `XAU` · `XDR` · `ZAR`

Pairs the central bank does not print directly are resolved from this table (see below).

## Published vs derived rates

If Banco Central del Paraguay does not print a pair directly, the API resolves it from the bank's table (inverse, or a cross rate via PYG) and flags it `derived: true` with the `method` — so official and computed values are never confused.

## Notes

- Every request counts toward your AllRatesToday monthly quota. Rates change once per business day — cache a day's table locally and a small quota goes a long way.
- Latest rates are on every plan (including free); historical dates and time series need a [paid plan](https://allratestoday.com/pricing/).
- Full API reference: [allratestoday.com/docs#central-bank](https://allratestoday.com/docs/#central-bank) · All covered sources: [central bank rates API](https://allratestoday.com/central-bank-rates-api/)

## License

MIT
