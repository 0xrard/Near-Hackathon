# Snapshot manifest — 14 Nov 2026

This submission's evidence is a frozen snapshot: data as of 13 Nov 2026, taken 14 Nov 2026 (the daily series end 13 Nov by design; 14 Nov enters only as the intraday market snapshot, $3.33 / $4.36B).

[`data/SHA256SUMS.txt`](data/SHA256SUMS.txt) lists the SHA-256 of every file under `data/` — 24 files, including `falsifiers.json`, the raw buyback-wallet census, and the full F1 margin series. The hashes were computed on 14 Nov 2026, before the submission deadline, against the files exactly as shipped.

Verify from the repo root:

```
sha256sum -c data/SHA256SUMS.txt
```

If every line reads OK, the numbers in THESIS.md, the terminal and the dashboard rest on the same bytes the author froze — nothing in the evidence base has been edited after the fact. Post-deadline readings live only in the terminal's live re-check, which is labelled live wherever it appears and never writes back into `data/`.
