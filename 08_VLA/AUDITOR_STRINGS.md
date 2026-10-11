# Auditor hand-off — site strings for microarch-owner

`microarch/03_tools/verify_claims.py` matches exact page substrings. When a site edit rewords or deletes a sentence an
audited check carries, list it here before pushing, one row per check, then hand it to microarch-owner and clear the row
once the auditor reads 0 FAIL. New number-bearing sentences that deserve a check go in the same table with "(new)".

| check label | old string | new string on the page (exact) | source (ledger id or CSV selector) |
|---|---|---|---|
| the 20 `p3 …` checks with `wait=AREA_WAIT` (rate-D callout, overhead, tradeoff lead / cells / prose, prior rows) | EV-35 (flip-flop GB) areas | already carried verbatim at EV-38 (scratch-copy run: 0 FAIL, 0 site WAIT) | drop `wait=AREA_WAIT` from them once the push lands |
| (new) p3 LP-Spec area | — | `2.86 mm&sup2; of PIM area against LP-Spec-like&rsquo;s 3.06, 0.93&times;, with CoRe&rsquo;s PU logic alone 0.84&times; LP-Spec-like&rsquo;s` | `prior_art_5ns.ours.die_mm2`, `.lpspec.die_mm2`, `.lpspec.ours_area_over_row`; 0.84 from `area_gb_sram.md` §0 / `spec_dac_point.md` §0 |
| (new) p3 prior caption | — | `CoRe&rsquo;s 2.86 mm&sup2; is 0.93&times; LP-Spec-like&rsquo;s 3.06` · `stock-depth designs&rsquo; 1.06&ndash;1.21 mm&sup2;` · flip-flop sensitivity `(7.66 against 3.80 mm&sup2;)` | as above; range = `c5_p1_5ns.S` … `prior_art_5ns.p3llm.die_mm2`; sensitivity = `area_gbsram.csv` old column (`PIM_GB_PRICE=flipflop`) |
| (new) p3 overhead GB | — | `and the 52 KB GB is 0.34 mm&sup2; of it, priced as DRAM-process SRAM in four 13 KB cuts at 0.80 &micro;m&sup2;/bit` · band `2.82 / 3.28 / 3.98 mm&sup2;` · `the GB would be 5.15 mm&sup2; and the design 7.75 mm&sup2; (12.7%)` | `pu_design_full.P1b.gb_mm2`; 0.80 and band from `area_gbsram_points.csv` (`area_gb_sram.md` §0–1) |
| (new) p3 storage callout / novelty | — | `the whole fast-narrow design is +1.88 mm&sup2; over stock AiM, of which the GB, priced as DRAM-process SRAM, is 0.34 mm&sup2;` · `PIM area is 2.94 mm&sup2; per die (4.8 %), +1.88 mm&sup2; over stock AiM` | `c5_fd_5ns.FD-16x800.die_mm2 / .die_pct / .added_area_vs_stock_mm2` |
| (new) GB read-rate bound (Part III `#gbrate` callout; Part IV beats callout) | — | `at most +0.26 mm&sup2; (3.20 mm&sup2; instead of 2.94)` (file `02_stock_aim_offload`) · `at most +0.26 mm&sup2; if the pairing cannot be static` | `area_gbsram_feas.csv` (`area_gb_sram.md` §2) |
| (new) Part III CK-divider callout | — | `against a PIM block of 2.94 mm&sup2; per die for the fast-narrow design and 1.06 mm&sup2; for stock AiM` | `c5_fd_5ns.FD-16x800.die_mm2`, `c5_p1_5ns.S.die_mm2` (file `02_stock_aim_offload`) |

*Open since the EV-38 area restatement (2026-10-11; supersedes the EV-35 rows), for microarch-owner after the push.*
