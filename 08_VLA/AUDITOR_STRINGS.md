# Auditor hand-off — site strings for microarch-owner

`microarch/03_tools/verify_claims.py` matches exact page substrings. When a site edit rewords or deletes a sentence an
audited check carries, list it here before pushing, one row per check, then hand it to microarch-owner and clear the row
once the auditor reads 0 FAIL. New number-bearing sentences that deserve a check go in the same table with "(new)".

| check label | old string | new string on the page (exact) | source (ledger id or CSV selector) |
|---|---|---|---|
| the 20 `p3 …` checks with `wait=AREA_WAIT` (rate-D callout, overhead, tradeoff lead / cells / prose, prior rows) | pre-EV-35 areas | already carried verbatim (scratch-copy run: 0 FAIL, 0 site WAIT) | drop `wait=AREA_WAIT` from them once the push lands |
| (new) p3 LP-Spec area | — | `7.66 mm&sup2; of PIM area against LP-Spec-like&rsquo;s 3.80, 2.02&times;, while CoRe&rsquo;s PU logic alone is 0.84&times; LP-Spec-like&rsquo;s` | `prior_art_5ns.ours.die_mm2`, `.lpspec.die_mm2`, `.lpspec.ours_area_over_row`; 0.84 from `spec_dac_point.md` §0 |
| (new) p3 overhead GB | — | `and the 52 KB GB is 5.15 mm&sup2; of it, priced as flip-flops at 12.08 &micro;m&sup2;/bit` | `pu_design_full.P1b.gb_mm2` |
| (new) Part III CK-divider callout | — | `against a PIM block of 7.75 mm&sup2; per die for the fast-narrow design and 1.24 mm&sup2; for stock AiM` | `c5_fd_5ns.FD-16x800.die_mm2`, `c5_p1_5ns.S.die_mm2` (file `02_stock_aim_offload`) |

*Open since the EV-35 area restatement (2026-10-11), for microarch-owner after the push.*
