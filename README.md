# NEAR Investment Thesis — Re-run Package v2 (14 Nov 2026 snapshot)

**Verdict: NEAR is priced for delivery.**

This package lets anyone re-run the model, the figures, and the six
falsifiers behind the thesis. It is the **model + data + figures** package
for the React repo (`github.com/0xrard/Near-Hackathon`).

**This package does NOT contain or build the dashboard.** The React
dashboard (`index.html`) and terminal (`terminal.html`) live in the
Near-Hackathon repo and are built in the artifact system. There is
intentionally no `dashboard/` folder and no `build_dashboard.py` here —
that script built the OLD HTML dashboard (13 Nov), not the React one.
Do not expect this package to reproduce the dashboard; it reproduces the
model outputs, the falsifier readings, and the figures.

## The 14 Nov 2026 snapshot — frozen

The numbers below are the frozen snapshot. Re-running the model from the
shipped CSVs reproduces them (see "Snapshot pins" for the three values
pinned to the snapshot time).

| Item | 14 Nov 2026 |
|---|---|
| NEAR price | $3.33 (CoinGecko; 13 Nov close $3.51) |
| Market cap | $4,362,731,157 ($4.36B), rank #22 |
| F1 — Intents volume, 30d avg (15 Oct–13 Nov) | $126.58M/day (DefiLlama total30d $3,797,462,047 / 30) |
| Cumulative Intents volume | $37.78B (87.3% trailing 12 months) |
| Gross fees, annualised (30d $5,831,933 × 12) | $69.98M/year |
| P/S, gross | 62.3× |
| P/S, captured (145×) | $30.03M/year (Oct net $2.50M/month) |
| F2 — net take / capture, 60d (15 Sep–13 Nov) | 5.13 bps / 31.5% |
| V\* — deflationary threshold @ 2.5% issuance | $573M/day (4.5× current volume) |
| V\* @ 1.6% (HSP-029 target) | $367M/day (2.9×) |
| V\* grid, take 5/10/16/20 bps | $1,835M / $918M / $573M / $459M |
| Scenarios, year 5 (fees) | Bear $46.20B ($73.92M) / Base $92.93B ($148.69M) / Bull $171.55B ($274.47M) |
| F4 — buyback wallet, 30d (15 Oct–14 Nov) | 2,280,770.08 NEAR, 768 receipts, inbound 287,393.71 NEAR, outflow 0.00 |
| F6 — net revenue run-rate vs baseline | $22.28M/year vs $1.41M/year = 15.8× |
| Offset (buybacks / emissions), Nov MTD | 18.8% (Sep peak 25.2%, Oct 18.4%) |
| October capture | 39.2% (net $2,502,470 / gross $6,388,076) |
| Falsifiers triggered | **0 of 6** |
| Fig5 — TVL / stablecoins | $159.15M / $132.03M (83.0% of TVL) |
| Fig8 — peer P/S median | 402× (Tron 101.4×, ARB 151.6×, SOL 229.8×, BNB 575.2×, AVAX 807.8×, ETH 979.3×) |
| Fig9 — lead/lag | r = +0.01 at lag 0 (n = 526), max |r| = 0.07 at lag −4, placebo p = 0.554 |

**Buyback wallet, full history (corrected):** 3,408 receipts, 18 Mar–14 Nov
2026; inflows 2,293,097 NEAR (3,391 inbound, 3,360 from intents.near);
outflow exactly 3 transactions totalling 12,025 NEAR (20 NEAR on 20 Mar,
5 NEAR on 20 Mar, 12,000 NEAR on 10 Jul 2026 — the only material outflow);
balance 2,281,071.57 NEAR. The 1.74M NEAR figure is the revenue
dashboard's attribution, not the on-chain total. (An earlier claim that
total outflow was negligible was wrong and is not in this package.)

## What is re-run vs quoted

| Part | Status |
|---|---|
| Model (`model/model.py` + `model/config.yaml`) | Re-run 14 Nov 2026 → `data/model_outputs.json` |
| Falsifiers F1–F6 (`scripts/check_falsifiers.py`) | Re-run 14 Nov 2026 → `data/falsifiers.json` (0/6) |
| Figures 1–9 (`scripts/generate_chapter*_figures.py`) | Regenerated 14 Nov 2026 → `figures/fig1–fig9.png`, `data/captions.json`, `data/stats.json` |
| DefiLlama / CoinGecko / revenue.near.org / NearBlocks | Re-fetched 14 Nov 2026 (keyless, no credentials) |
| BigQuery G1–G6 (`data/bq_*.csv`, `queries/`) | **Quoted, not re-run.** Pulled 11 Nov 2026; no GCP credentials in this package. Used only for hypothesis test B (correlation) in `model_outputs.json`. See Appendix A.5 of THESIS.md. |
| Fig4 chart data | Live NearBlocks `/v1/charts`, retrieved 2026-11-14 (the generator fetches it; it does not read the `bq_*` CSVs). |

## Snapshot pins (frozen values, documented not hidden)

Three values were pinned to the 14 Nov 2026 snapshot time so the frozen
package matches the frozen dashboard. Each pin is recorded in
`data/manifest.json` (`snapshot_notes`):

1. **Market cap** — `data/near_market.json` pinned to $4,362,731,157.
   The live CoinGecko pull gave $4,362,059,250 (0.015% lower, intraday drift).
2. **November MTD net revenue** — `data/intents_revenue_monthly.csv`
   Nov 2026 pinned to $754,684 (the snapshot-time value). The live
   revenue.near.org value had moved to $822,495 by the later pull; using
   it would give F2 5.21 bps / 32.0% instead of the snapshot 5.13 bps /
   31.5%. The pin keeps the package consistent with the frozen dashboard.
3. **13 Nov close** — `data/near_price_daily.csv` 13 Nov close restored to
   $3.5118584696509734. A re-pull overwrote it with $3.419140 (CoinGecko
   revises the live point); the snapshot value is authoritative. The 14 Nov
   snapshot price row ($3.33) is the model input.
4. **Market-cap rank** — `data/stats.json` rank pinned to 22 (snapshot).
   Live CoinGecko rank at generation time was 25 (intraday drift).

**F4 intraday drift (not pinned, not hidden):** the fresh NearBlocks
snapshot in `data/buyback_wallet_30d.json` reads 2,281,071.57 NEAR / 767
receipts / inbound 287,235.39 NEAR, vs the dashboard snapshot 2,280,770.08 /
768 / 287,393.71. The 30-day window slides intraday, so the count and
balance move slightly; outflow is 0.00 in both, and F4 stays not triggered.
THESIS.md §7 and `data/manifest.json` record both readings.

**Figure drift notes (live-generated figures, documented):**
- Fig5 TVL caption ($155M) is the 14 Nov point of the live DefiLlama
  `historicalChainTvl` series at generation time (11:43 UTC); the frozen
  snapshot in THESIS.md uses $159.15M, which is the 13 Nov point of the
  same series (the latest available at the morning snapshot).
- Fig8 NEAR gross 61× uses the figure's documented ×365/30 annualisation
  (vs ×12 in Table 3 / model P/S 62.3×); the peer median (396× live vs
  402× snapshot) is live drift. The figure's method is stated on the
  figure itself.
- Fig1 uses Binance data (13 Nov close $3.445, MA50 4.57 / MA200 2.68)
  vs the CoinGecko close $3.51 / MA50 4.62 / MA200 2.66 used for the model
  snapshot; both are real price data from different exchanges.
- Fig9 placebo p = 0.592 in `model_outputs.json` (series extended to
  14 Nov) vs 0.554 in PDF v3; both are far above 0.05, same conclusion
  (no exploitable timing edge). THESIS.md cites 0.592 as primary.

**Capture calibration:** the model keeps `capture_rate: 0.326` in
`model/config.yaml` (the calibration). The measured 60d capture is 31.5%.
V\* is computed from the 0.326 calibration, as in the dashboard.

## How to re-run

Requirements: Python 3.10+ only (standard library for the model and the
falsifier check; `matplotlib` + `requests` for the figures — see
`requirements.txt`).

```bash
bash rebuild.sh --model-only   # no credentials: model + figures + falsifiers from shipped CSVs
bash rebuild.sh                # full: also re-fetches keyless sources (BigQuery needs GCP creds in .env)
```

`rebuild.sh` never builds a dashboard. It writes `data/model_outputs.json`,
`data/falsifiers.json`, `figures/fig1–fig9.png`, `data/captions.json`, and
`data/stats.json`. A re-run on a later date will move the live figures
(TVL, peer multiples, rank) — that is expected; the frozen snapshot above
is the 14 Nov 2026 reference.

## Contents

```
model/            config.yaml (all assumptions) + model.py
data/             CSVs + JSONs (see data/README.md); model_outputs.json, falsifiers.json,
                  buyback_wallet_30d.json, captions.json, stats.json, manifest.json
queries/          BigQuery SQL G1–G6 + 00-freshness.sql (quoted 11 Nov 2026 pull)
scripts/          fetch.py, check_falsifiers.py, fetch_f4_snapshot.py,
                  generate_chapter3/4/5_figures.py
figures/          fig1–fig9.png (regenerated 14 Nov 2026)
THESIS.md         Full thesis, 14 Nov 2026 figures (see Appendix A.5 for quoted vs re-run)
REFERENCES.md     Sources
requirements.txt  Python deps
rebuild.sh        Re-run entry point (model + figures + falsifiers; NO dashboard build)
.env.example      Credential template (BigQuery only; everything else is keyless)
.gitignore        Standard ignores
LICENSE           MIT
```

## Falsifiers (Table 5) — 0 of 6 triggered

| ID | Definition | 14 Nov reading | Status |
|---|---|---|---|
| F1 | Intents volume < $75M/day × 30d | $126.58M/day (15 Oct–13 Nov) | not triggered |
| F2 | Net take < 3 bps OR capture < 15% × 60d | 5.13 bps / 31.5% (15 Sep–13 Nov) | not triggered |
| F3 | HSP-029 not live by 30 Jun 2027 | Deadline not reached | not yet decidable |
| F4 | Buyback-wallet outflow > 5% / 30d | 0.00 NEAR (0.00% of balance) | not triggered |
| F5 | ETF outflows for 4+ weeks | No public endpoint | cannot check |
| F6 | Net-revenue run-rate not doubling in 4 quarters | $22.28M/year vs $1.41M/year = 15.8× | not triggered |

Sub-hypothesis B failed (levels r = −0.189/−0.102; active accounts −69.7%
YoY) and is kept as a burden in THESIS.md §6. Sub-hypothesis A cannot be
computed (no swapper-level data).
