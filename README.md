# Crypto Futures Fee Index — open data

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23410593.svg)](https://doi.org/10.5281/zenodo.23410593)

Standard (VIP 0) taker and maker fees on USDT-margined perpetual futures, by exchange. Every row carries the date it was last checked against the exchange's official fee page and a link to that page. CSV and JSON, licensed CC BY 4.0.

- Data as of: **2026-10-16** (latest row check date)
- Source: loweef Crypto Futures Fee Index — https://loweef.io/en/crypto-futures-fee-index/ (method and FAQ)

## Fees only (current data)

From `fees-only.csv` / `fees-only.json`. Fees are in percent of notional per fill.

| Exchange | Taker | Maker | Last checked | Official source |
|---|---|---|---|---|
| MEXC* | 0.04% | 0% | 2026-10-16 | https://www.mexc.com/fee |
| Binance | 0.05% | 0.02% | 2026-10-12 | https://www.binance.com/en/fee/futureFee |
| BingX | 0.05% | 0.02% | 2026-10-16 | https://bingx.com/en/support/costs/futures |
| Kraken | 0.05% | 0.02% | 2026-10-12 | https://www.kraken.com/features/fee-schedule |
| OKX | 0.05% | 0.02% | 2026-10-16 | https://www.okx.com/fees |
| Bybit | 0.055% | 0.02% | 2026-10-16 | https://www.bybit.com/en/help-center/article/Trading-Fee-Structure |
| Bitget | 0.06% | 0.02% | 2026-10-12 | https://www.bitget.com/support/articles/12560603817155 |

Footnotes:

- MEXC (`takerFeePct`): Taker 0.04% is the standard rate for the USDT-M BTCUSDT perpetual. MEXC sets futures fees per contract, and this value matches the official fee page (Futures tab, checked 2026-10-14), the public contract API (BTC_USDT, checked 2026-10-08) and the fee charged on a real trade (checked 2026-08-24). Other contracts can differ (for example ETHUSDT taker 0.02%), so a table that lists 0.02% for MEXC may be quoting a different contract.
- MEXC (`makerFeePct`): MEXC may apply a different futures maker fee in some regions (such as parts of Asia, the Middle East, Africa and Latin America). Go by the rate shown on your trading screen.

## Quick start

Python (pandas) — the first CSV line is a license/source comment:

```python
import pandas as pd
fees = pd.read_csv("https://raw.githubusercontent.com/loweef/crypto-futures-fees/main/fees-only.csv", comment="#")
```

Shell (JSON):

```sh
curl -s https://raw.githubusercontent.com/loweef/crypto-futures-fees/main/fees-only.json
```

Columns: `exchange_id`, `exchange`, `taker_fee_pct`, `maker_fee_pct`, `last_checked`, `source`, `notes`.

## Files

| File | Content |
|---|---|
| `fees-only.json` / `fees-only.csv` | Fees only: exchange, taker and maker fee, check date, official source and footnotes. No rebate columns |
| `latest.json` | Full dataset (schema v1), including the rebate columns described below |
| `latest.csv` | Same rows as `latest.json` as CSV (first line is a license/source comment) |
| `changelog.json` | Every published change, newest first, with a link to the snapshot |
| `snapshots/YYYY-MM-DD.json` | Immutable copy of the full dataset on the day its content changed (includes the rebate columns) |

This repository only mirrors the published files. Commits happen only when the content changes. Live copies: https://loweef.io/data/fees/v1/latest.json · https://loweef.io/data/fees/v1/latest.csv · https://loweef.io/data/fees/v1/changelog.json

## Full dataset: rebate columns

Disclosure: loweef is a fee-rebate service with affiliate ties to some of the listed exchanges; the fees-only files exclude all commercial fields.

`latest.*` and `snapshots/` add these columns to the same rows: `kind`, `user_rebate_pct`, `welcome_boost_*`, `effective_*`. The rebate is the share of trading fees returned to the user through loweef; the effective taker fee is the standard taker fee after that rebate.

| Exchange | Type | User rebate | Welcome boost | Effective taker |
|---|---|---|---|---|
| MEXC | partner | 50% | — | 0.02% |
| Binance | reference | — | — | 0.05% |
| BingX | partner | 60% | 70% for 2 weeks | 0.02% |
| Kraken | reference | — | — | 0.05% |
| OKX | partner | 50% | 60% for 2 weeks | 0.025% |
| Bybit | partner | 37% | 47% for 2 weeks | 0.0347% |
| Bitget | reference | — | — | 0.06% |

## Fields

- `userRebatePct`: Total share of each trading fee returned to the trader. null = no rebate via loweef.
- `effectiveTakerFeePct`: takerFeePct × (1 − userRebatePct/100).
- `welcomeBoost`: Higher userRebatePct during the first N weeks after linking an account; null when none.
- `lastChecked`: Date the row was last checked against the exchange's official fee page. Rows older than staleDays are removed.
- `takerFeePct` / `makerFeePct`: standard fee in percent of notional per fill.
- `kind`: `partner` (a rebate is available via loweef) or `reference` (standard fee only; `userRebatePct` is `null`, not 0).
- `generatedAt`: build time of the file, not a check date.

## Corrections

If a fee here differs from the exchange's official fee page, open an issue with the **Fee correction** template (or use the form on https://loweef.io/en/crypto-futures-fee-index/#report-error). A report never changes the data by itself: the value is checked against the official page first, and there is no reward. Accepted reports can be credited by display name in the change feed and the monthly report, only if you ask for it. This repository is public, so do not post email addresses, UIDs or API keys in issues.

## License and attribution

The data is licensed under [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/) (see `LICENSE`). You may copy, share and adapt it, including for commercial use, if you credit the source with a link:

```html
Source: <a href="https://loweef.io/en/crypto-futures-fee-index/">loweef Crypto Futures Fee Index</a> (CC BY 4.0)
```

Plain text: Source: loweef Crypto Futures Fee Index, https://loweef.io/en/crypto-futures-fee-index/

DOI (all versions, archived on Zenodo): https://doi.org/10.5281/zenodo.23410593. Each GitHub release also gets its own version DOI on Zenodo.

Citation metadata: `CITATION.cff` and `.zenodo.json` describe the same dataset; Zenodo archives each GitHub release using `.zenodo.json`, which takes precedence over `CITATION.cff` there.

## Recent changes

- 2026-10-20: Removed AlphaX; Bybit userRebatePct none → 37; Bybit effectiveTakerFeePct 0.055 → 0.0347; Bybit effectiveMakerFeePct 0.02 → 0.0126; Bybit lastChecked 2026-10-12 → 2026-10-16; Bybit welcomeBoost none → 47 for 2 weeks
- 2026-10-17: MEXC lastChecked 2026-10-08 → 2026-10-16
- 2026-10-16: AlphaX lastChecked 2026-09-18 → 2026-10-16; BingX lastChecked 2026-09-15 → 2026-10-16; OKX lastChecked 2026-09-27 → 2026-10-16
- 2026-10-15: MEXC source https://loweef.io/en/exchange/mexc/ → https://www.mexc.com/fee; AlphaX source https://loweef.io/en/exchange/alphax/ → https://www.alphax.com/en-us/fees; BingX source https://loweef.io/en/exchange/bingx/ → https://bingx.com/en/support/costs/futures; OKX source https://loweef.io/en/exchange/okx/ → https://www.okx.com/fees
- 2026-10-14: Initial public release (8 exchanges)

Exchanges change their fees. Check the exchange before you trade. This data is information, not financial advice.
