# HANDOFF — site
*Root: /home/yanggon/versel_distribute/08_VLA · Owner: site-owner · Current state only; the commit log is the record.*

## Current status
- **Pages:** five pages live (Parts I, II, III, III-2, IV), all at the primary design point (5 ns column, D = 4; 2.5 ns /
  1 GHz kept as labelled sensitivity). Mechanism named **CoRe** everywhere, PNGs included ("+CoRe"). Scope labels match
  the paper: CoRe alone 18.21 ms, +CoRe rung (attention included) 12.29 ms, full design 9.31 ms.
- **Git:** everything committed is pushed; `origin/main` and the auditor mirror are in step.
- **Auditor** (mirror pulled, cwd = microarch): 416 checks, 0 FAIL, 0 WAIT, 125 PARKED (paper sections awaiting the ISCA
  template migration; not the site's). No open site hand-off in `AUDITOR_STRINGS.md`.
- The site carries no PDFs. Markdown in this root: `ONBOARDING.md`, `HANDOFF.md`, `AUDITOR_STRINGS.md` only.

## Key numbers (primary point, 16 ch unless said; ledger `evaluation/p1/numbers.md`)
Stock 40.24 ms / 470 mJ (32 ch 23.64); 6.4× the 6.30 ms optimistic bound (2× floor). Full design 9.31 ms (4.32×), 5.87 ms
at 32 ch (1.07× under the bound), Orin NX (8 ch) 16.27 ms. Ladder 40.24 → 12.29 (+CoRe rung) → 10.45 → (11.97) → 9.45 →
9.31. D = 2 15.32, D = 1 27.44, 2.5 ns / 1 GHz 8.15. Energy 138 / 130 / 117 mJ vs 194. e2e overlapped 387 ms, 2.59 Hz.
CoRe alone 18.21 ms (2.21×; 1.71× / 2.37× vs DOTS-26 hidden / charged); full design vs DOTS 3.35× is cross-scope (say
so). Never 8.19 ms, never 295 mJ, never "realistic".

## Standing decisions (not reopened)
- User 2026-09-25: CoRe naming; "P1" only as the Part IV §1 problem id and ids `#p1`, `#p1-toy`, `#fig-frames-p1`;
  D = 1 vs DOTS "at most tie".
- Part III unnumbered aside `#peek` (burst/beats, why 5 ns, PU clock from CK [A2]) cites the JEDEC text / BL/n table,
  never the confidential-stamped vendor spec.
- NX 15 W / Thor 40 W energies stay at 2.5 ns with `†`; 2.5 ns tables are kept, labelled, never deleted.
- Reader questions go to Part III §13 `#qa`; PDFs are not regenerated unless asked.
- A0/A1/A2 labels; "optimistic bound (2× floor)"; vendor correspondence never cited; confidential documents not linked.
- site-owner runs the auditor after a push and owns the 08_VLA block of the root `README.md` / `index.html`.
- Markdown is kept lean (user, 2026-10-08): no history files; superseded HANDOFF text is deleted, not moved.

## Open issues
1. **P2** — No primary-point energy rows for Orin NX 15 W / Thor 40 W (cells at 2.5 ns, `†`); NX latency, the Part IV
   V sweep and the 15 / 30 W energy ratios are cited from `paper_ablation.csv` / `paper_energy.csv`, not the ledger —
   for evaluation-owner / microarch-owner.
2. **P2** — Duplicate marker id `arrF` ×4 in Part III. Part IV "(Fig. 6b)" means Part III's figure (collides with its own);
   "Fig. 11a", "Fig. 3a/3b" vs "Fig. 3" confusing.
3. **P3** — Part II "10 of 12 cells" predates the extra columns (16 energy cells, 13 favourable); unaudited. A0/A1/A2 named
   only in Part III. Orphan `phase3_overhead_sensitivity.png`; `vendor_compare.png` absent from `sync_site_figs.py` MAP.
4. **P3** — Cosmetic: text overflow in Part IV Fig. 6a right panel; label touches in `crossover.png` / `scaling.png`.

## Next steps
1. Issue 2: rename markers `arrF1…4`; qualify cross-page figure refs as "Part III Fig. 6b".
2. For microarch-owner (cosmetic): drop the passing `wait=` arguments in `verify_claims.py`; add `vendor_compare.png` to
   the `sync_site_figs.py` MAP (source `06_figures/fig_vendor_compare.png`).
3. If evaluation-owner collects the V sweep and the 15 / 30 W rows into the ledger, cite ledger ids on the pages' sources.

## Interfaces
- **microarch-owner:** every number (`04_data`, `05_reports`), every PNG (`plot_web_figs.py` → `sync_site_figs.py`), the
  claim auditor and its read-only mirror `03_tools/versel_distribute`. A site change that alters an audited string needs
  a matching auditor edit by microarch-owner.
- **evaluation-owner:** numbers via `evaluation/p1/numbers.md`. **paper-owner:** shares the auditor; keep scope labels
  aligned. **jetson-owner:** none directly.
