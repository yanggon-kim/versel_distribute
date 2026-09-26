# HANDOFF — site
*Root: /home/yanggon/versel_distribute/08_VLA · Owner: site-owner · Last updated: 2026-09-25 · State only; superseded
and per-task notes are in `HANDOFF.history.md`.*

## Current status
- **Pages:** five pages live (Parts I, II, III, III-2, IV), all at the primary design point (5 ns column, D = 4; 2.5 ns /
  1 GHz kept as labelled sensitivity). Mechanism named **CoRe** (column reuse; formerly "P1") on Parts III, III-2, IV; scope
  labels match paper `41e3425`: "CoRe alone" = 18.21 ms, "+CoRe rung (attention included)" = 12.29 ms, full design = 9.31 ms.
- **Git:** `origin/main` at `93d186a` (pushed 2026-09-25, incl. the CoRe rename). **Committed, NOT pushed** (push is main's
  call, on user approval): `ee0b6f1` (HANDOFF), `ee05dd0` (scope relabel, Parts III-2 / IV), plus this HANDOFF trim.
- **Auditor: knowingly red until microarch-owner's wave 3.** Mirror at `93d186a`: 408 checks, 14 FAIL, 0 WAIT = exactly
  items 1–14 below. Working tree (scratch copy, `V` repointed): 408 checks, 18 FAIL (the same 14 + 4 paper), 0 WAIT.
  After wave 3 lands and the local commits are pushed: pull the mirror, run the auditor, expect 0 FAIL.
- Last edit: HTML well-formed (only the known `arrF` duplicate), `git diff --check` clean. The site carries **no PDFs**.

## Pending wave 3 (live — microarch-owner is applying this now)
**(a) Auditor strings, old → new, verbatim** (labels as `verify_claims.py` prints them). Items 3, 4, 8, 13, 14: the
**DELTA** block below supersedes their "new" string; every final string was verified present in the normalised page.

1. `p2 vendor callout` (Part III)
   - old: `the full design is worth 4.32&times; per step (P1 alone 2.21&times;)`
   - new: `the full design is worth 4.32&times; per step (CoRe alone 2.21&times;)`
2. `(unlabelled, after "p2 vendor callout")` (Part III)
   - old: `1.47&times; (P1 alone 1.22&times;)`
   - new: `1.47&times; (CoRe alone 1.22&times;)`
3. `p3 toy table` (Part IV)
   - old: `40.24 &rarr; 12.29 ms/step (3.3&times;, P1 alone; 5 ns column, D = 4)`
   - new: `40.24 &rarr; 12.29 ms/step (3.3&times;, CoRe alone; 5 ns column, D = 4)`
4. `p3 P4 measured` (Part IV)
   - old: `12.29 &rarr; 10.45 ms per step at 16 channels when P4 is added on top of P1 (&sect;5, primary point) &mdash; 1.18&times;`
   - new: `12.29 &rarr; 10.45 ms per step at 16 channels when P4 is added on top of CoRe (&sect;5, primary point) &mdash; 1.18&times;`
5. `p3 scaling alt` (Part IV)
   - old: `Stock AiM: 75.10, 40.24, 23.64 ms. +P1 MAC_ABK_MV V = 26: 18.69, 12.29, 9.27 ms`
   - new: `Stock AiM: 75.10, 40.24, 23.64 ms. +CoRe MAC_ABK_MV V = 26: 18.69, 12.29, 9.27 ms`
6. `p3 ablation alt` (Part IV)
   - old: `stock AiM 40.24 ms (28.55 at 2.5 ns); +P1 MAC_ABK_MV V = 26: 12.29 (11.13); +P4 LOOP macros 10.45 (9.29); +dedup and token-parallel x2 with 64-column lines 11.97 (8.19); +8-column MV lines 9.45 (8.00); +drain-later accumulator file, the headline, 9.31 (8.11)`
   - new: `stock AiM 40.24 ms (28.55 at 2.5 ns); +CoRe MAC_ABK_MV V = 26: 12.29 (11.13); +P4 LOOP macros 10.45 (9.29); +dedup and token-parallel x2 with 64-column lines 11.97 (8.19); +8-column MV lines 9.45 (8.00); +drain-later accumulator file, the headline, 9.31 (8.11)`
7. `p3 DOTS fetches` (Part IV)
   - old: `26 tokens against one column cost DOTS 26 fetches = 208 cycles, and cost P1 one fetch plus 26 PU beats = 52 cycles at D = 4`
   - new: `26 tokens against one column cost DOTS 26 fetches = 208 cycles, and cost CoRe one fetch plus 26 PU beats = 52 cycles at D = 4`
8. `p3 P1 vs DOTS D=2/4` (Part IV)
   - old: `At D = 2 (16 lanes @ 400 MHz, 23.15 ms) P1 is 1.35&times; ahead of the hidden row; at the D = 4 design point (18.21 ms) it is 1.71&times; ahead of the hidden row and 2.37&times; ahead of the charged one`
   - new: `At D = 2 (16 lanes @ 400 MHz, 23.15 ms) CoRe is 1.35&times; ahead of the hidden row; at the D = 4 design point (18.21 ms) it is 1.71&times; ahead of the hidden row and 2.37&times; ahead of the charged one`
9. `p3 prior order` (Part IV)
   - old: `<b>P1 alone (18.21 ms) is faster than LP-Spec (19.36 ms) with a quarter of the multipliers</b>, where at the 2.5 ns column it was not (15.15 vs 14.81)`
   - new: `<b>CoRe alone (18.21 ms) is faster than LP-Spec (19.36 ms) with a quarter of the multipliers</b>, where at the 2.5 ns column it was not (15.15 vs 14.81)`
10. `p3 prior LP-Spec measured` (Part IV)
   - old: `<b>Measured:</b> 19.36 ms, 2.08&times; at the primary point (four ALUs at the column rate, 64 lanes @ 200 MHz) &mdash; <b>behind P1 alone (18.21 ms) with four times the multipliers</b>; at the 2.5 ns / 1 GHz point it was the only row that beat P1 alone (14.81 vs our 15.15 ms)`
   - new: `<b>Measured:</b> 19.36 ms, 2.08&times; at the primary point (four ALUs at the column rate, 64 lanes @ 200 MHz) &mdash; <b>behind CoRe alone (18.21 ms) with four times the multipliers</b>; at the 2.5 ns / 1 GHz point it was the only row that beat CoRe alone (14.81 vs our 15.15 ms)`
11. `(unlabelled, after "p3 prior verdicts")` (Part IV)
   - old: `(LP-Spec, 2.08&times; at the primary point; 1.93&times; at 2.5 ns / 1 GHz, where it was the only row that beat P1 alone)`
   - new: `(LP-Spec, 2.08&times; at the primary point; 1.93&times; at 2.5 ns / 1 GHz, where it was the only row that beat CoRe alone)`
12. `(unlabelled, after "p3 prior verdicts")` (Part IV)
   - old: `(ours, 2.21&times; at the primary point, P1 alone at D = 4; 1.88&times; at the 2.5 ns / 1 GHz transplant point)`
   - new: `(ours, 2.21&times; at the primary point, CoRe alone at D = 4; 1.88&times; at the 2.5 ns / 1 GHz transplant point)`
13. `p3b layer row` (Part III-2)
   - old: `P1 alone: 1.427 &rarr; 0.459 ms/layer (<b>3.1&times;</b>); full design (P1 + P4 + SW): 1.427 &rarr; 0.396 ms/layer (<b>3.6&times;</b>)`
   - new: `CoRe alone: 1.427 &rarr; 0.459 ms/layer (<b>3.1&times;</b>); full design (CoRe + P4 + SW): 1.427 &rarr; 0.396 ms/layer (<b>3.6&times;</b>)`
14. `p3b kpi` (Part III-2)
   - old: `<div class="v">1.11&times;</div><div class="l">what the same ISA fix buys here (AiM P1 alone at V = 26: 4.0&times; at its 5 ns primary point, 3.1&times; at this page&rsquo;s 2.5 ns column)</div>`
   - new: `<div class="v">1.11&times;</div><div class="l">what the same ISA fix buys here (AiM CoRe alone at V = 26: 4.0&times; at its 5 ns primary point, 3.1&times; at this page&rsquo;s 2.5 ns column)</div>`

**DELTA (2026-09-25, scope relabel; supersedes the "new" strings of items 3, 4, 8, 13, 14 above; no other check affected;
all verified present in the normalised page):**
- 3. `p3 toy table` new: `40.24 &rarr; 12.29 ms/step (3.3&times;, the +CoRe rung, attention included; 5 ns column, D = 4)`
- 4. `p3 P4 measured` new: `12.29 &rarr; 10.45 ms per step at 16 channels when P4 is added on top of the +CoRe rung (&sect;5, primary point) &mdash; 1.18&times;`
- 8. `p3 P1 vs DOTS D=2/4` new: `At D = 2 (16 lanes @ 400 MHz, 23.15 ms) CoRe alone is 1.35&times; ahead of the hidden row; at the D = 4 design point (18.21 ms) it is 1.71&times; ahead of the hidden row and 2.37&times; ahead of the charged one`
- 13. `p3b layer row` new: `+CoRe rung (attention included): 1.427 &rarr; 0.459 ms/layer (<b>3.1&times;</b>); full design (CoRe + P4 + SW): 1.427 &rarr; 0.396 ms/layer (<b>3.6&times;</b>)`
- 14. `p3b kpi` new: `<div class="v">1.11&times;</div><div class="l">what the same ISA fix buys here (AiM&rsquo;s +CoRe rung at V = 26, attention included: 4.0&times; at its 5 ns primary point, 3.1&times; at this page&rsquo;s 2.5 ns column)</div>`
- Still passing and untouched (edits made around them): `p3 prior cap` (…3.35&times; faster than the two DOTS rows), `p3 P1 vs DOTS D=1` (ours 33.07 ms … (0.94&times;, i.e. slower) …).
- Optional for microarch-owner: the three PNGs' "+P1" labels become "+CoRe" (rung label, as in the paper's ablation), not "CoRe alone".
**(b) Three PNGs still say "P1" on the live site** (accepted as temporary): `phase6_ablation.png` ("+P1 MAC_ABK_MV (V = 26)",
`plot_results.py` tiers list), `scaling.png` (same label, `plot_web_figs.py:200`), `vendor_compare.png` ("AiM, +P1",
`make_vendor_fig.py:67,76`). When microarch's regenerated files arrive: look at each, commit them (site-owner), push on
approval. Alt texts / captions already say CoRe.

## Key numbers (primary point, 16 ch unless said; full set in `evaluation/p1/numbers.md`, ids in `AUDITOR_STRINGS.md`)
Stock 40.24 ms / 470 mJ (32 ch 23.64); 6.4× the 6.30 ms optimistic bound (2× floor). Full design 9.31 ms (4.32×), 5.87 ms
at 32 ch (1.07× under the bound), Orin NX 16.27 ms. Ladder 40.24 → 12.29 (+CoRe rung) → 10.45 → (11.97) → 9.45 → 9.31.
D = 2 15.32, D = 1 27.44, 2.5 ns / 1 GHz 8.15. Energy 138 / 130 / 117 mJ vs 194. e2e overlapped 387 ms, 2.59 Hz. CoRe
alone 18.21 ms (2.21×; 1.71× / 2.37× vs DOTS-26 hidden / charged); full design vs DOTS 3.35× is cross-scope (say so).
Never 8.19 ms, never 295 mJ, never "realistic". (Longer list: `HANDOFF.history.md`.)

## Recent decisions (not reopened; detail and commits in `HANDOFF.history.md`)
- 2026-09-25 (user): CoRe naming; "P1" only as Part IV §1 problem id and ids `#p1`, `#p1-toy`, `#fig-frames-p1`. Rename
  pushed ahead of the auditor update (red accepted until wave 3). Scope labels as in the paper; D = 1 vs DOTS "at most tie".
- 2026-09-23: Part III unnumbered aside `#peek` (burst/beats, why 5 ns, PU clock from CK [A2]); unnumbered on purpose. Cites
  the JEDEC text / BL/n table, never the confidential-stamped vendor spec (accepted by main and the user).
- 2026-09-22: site at the primary point; NX 15 W / Thor 40 W energies stay 2.5 ns, `†`; 2.5 ns tables kept, labelled.
- 2026-09-21: reader questions go to Part III §13 `#qa`; PDFs deleted, not regenerated unless asked.
- 2026-09-20: A0/A1/A2 labels; site-owner runs the auditor after a push; owns the 08_VLA block of `README.md` / `index.html`.
- Standing: "optimistic bound (2× floor)"; vendor correspondence never cited; confidential-stamped documents not linked.

## Open issues
1. **P2** — No primary-point energy rows for Orin NX 15 W / Thor 40 W (cells at 2.5 ns, `†`); NX latency from
   `paper_ablation.csv`, not the ledger — for evaluation-owner / microarch-owner.
2. **P2** — Duplicate marker id `arrF` ×4 in Part III. Part IV "(Fig. 6b)" means Part III's figure (collides with its own);
   "Fig. 11a", "Fig. 3a/3b" vs "Fig. 3" confusing.
3. **P3** — Part II "10 of 12 cells" predates the extra columns (16 energy cells, 13 favourable); unaudited. A0/A1/A2 named
   only in Part III. Orphan `phase3_overhead_sensitivity.png`; `vendor_compare.png` absent from `sync_site_figs.py` MAP.
4. **P3** — Cosmetic: text overflow in Part IV Fig. 6a right panel; label touches in `crossover.png` / `scaling.png`.

## Next steps
1. Wave 3: when microarch-owner reports the auditor repointed and the PNGs regenerated → commit the PNGs, then (on
   approval) push, pull the mirror, run the auditor from cwd = microarch, expect 0 FAIL.
2. Issue 2 (rename markers `arrF1…4`; qualify cross-page figure refs as "Part III Fig. 6b").
3. For microarch-owner (cosmetic): drop the passing `wait=` arguments in `verify_claims.py`; re-run once after.
4. If evaluation-owner collects the V sweep and the 15 / 30 W rows into the ledger, swap the paper-sourced citations in
   `AUDITOR_STRINGS.md` for ledger ids.

## Interfaces with other sub-projects
- **microarch-owner** (`/home/yanggon/05_VLA_LPDDR/microarch`): every number (`04_data`, `05_reports`), every PNG
  (`plot_web_figs.py` → `sync_site_figs.py`, writes into `08_VLA/*/assets/`), the claim auditor and its read-only mirror
  `03_tools/versel_distribute`. A site change that alters an audited string needs a matching auditor edit by microarch-owner.
- **evaluation-owner**: numbers via `evaluation/p1/numbers.md`. **paper-owner**: shares the auditor; keep scope labels aligned.
- **jetson-owner**: none directly; measured numbers arrive via microarch / evaluation.
