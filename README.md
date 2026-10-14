# Crypto Futures Fee Index — open data

Source: loweef Crypto Futures Fee Index — https://loweef.io/en/crypto-futures-fee-index/ (CC BY 4.0)

Standard (VIP 0) USDT-margined perpetual futures taker and maker fees by exchange, the user fee-rebate rate available via [loweef](https://loweef.io/en/crypto-futures-fee-index/), and the resulting effective fee. Every row carries the date it was last checked against the exchange's official fee page.

- Data as of: **2026-10-12** (latest row check date)
- Human-readable page, method and FAQ: https://loweef.io/en/crypto-futures-fee-index/
- Live files: https://loweef.io/data/fees/v1/latest.json · https://loweef.io/data/fees/v1/latest.csv · https://loweef.io/data/fees/v1/changelog.json

## Files

| File | Content |
|---|---|
| `latest.json` | Current dataset (schema v1) |
| `latest.csv` | Same rows as CSV (first line is a license/source comment) |
| `changelog.json` | Every published change, newest first, with a link to the snapshot |
| `snapshots/YYYY-MM-DD.json` | Immutable copy of the dataset on the day its content changed |

This repository only mirrors the published files. Commits happen only when the content changes.

## Current data

| Exchange | Type | Taker | Maker | User rebate | Welcome boost | Effective taker | Last checked |
|---|---|---|---|---|---|---|---|
| MEXC | partner | 0.04% | 0%* | 55% | 65% for 2 weeks | 0.018% | 2026-10-08 |
| AlphaX | partner | 0.05% | 0.02% | 65% | — | 0.0175% | 2026-09-18 |
| Binance | reference | 0.05% | 0.02% | — | — | 0.05% | 2026-10-12 |
| BingX | partner | 0.05% | 0.02% | 60% | 70% for 2 weeks | 0.02% | 2026-09-15 |
| Kraken | reference | 0.05% | 0.02% | — | — | 0.05% | 2026-10-12 |
| OKX | partner | 0.05% | 0.02% | 50% | 60% for 2 weeks | 0.025% | 2026-09-27 |
| Bybit | reference | 0.055% | 0.02% | — | — | 0.055% | 2026-10-12 |
| Bitget | reference | 0.06% | 0.02% | — | — | 0.06% | 2026-10-12 |

\* MEXC: MEXC may apply a different futures maker fee in some regions (such as parts of Asia, the Middle East, Africa and Latin America). Go by the rate shown on your trading screen.

## Fields

- `userRebatePct`: Total share of each trading fee returned to the trader. null = no rebate via loweef.
- `effectiveTakerFeePct`: takerFeePct × (1 − userRebatePct/100).
- `welcomeBoost`: Higher userRebatePct during the first N weeks after linking an account; null when none.
- `lastChecked`: Date the row was last checked against the exchange's official fee page. Rows older than staleDays are removed.
- `takerFeePct` / `makerFeePct`: standard fee in percent of notional per fill.
- `kind`: `partner` (a rebate is available via loweef) or `reference` (standard fee only; `userRebatePct` is `null`, not 0).
- `generatedAt`: build time of the file, not a check date.

## License and attribution

The data is licensed under [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/) (see `LICENSE`). You may copy, share and adapt it, including for commercial use, if you credit the source with a link:

```html
Source: <a href="https://loweef.io/en/crypto-futures-fee-index/">loweef Crypto Futures Fee Index</a> (CC BY 4.0)
```

Plain text: Source: loweef Crypto Futures Fee Index, https://loweef.io/en/crypto-futures-fee-index/

## Recent changes

- 2026-10-14: Initial public release (8 exchanges)

Exchanges change their fees. Check the exchange before you trade. This data is information, not financial advice.
