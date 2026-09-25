# HANDOFF — site
*Root: /home/yanggon/versel_distribute/08_VLA · Owner: site-owner · Last updated: 2026-09-25 (rename P1 → CoRe committed, **unpushed**: waits for microarch-owner's `verify_claims.py` update and the three PNG relabels)*

> **Server paths moved.** This root is now `/home/yanggon/versel_distribute/08_VLA`, the workspace is
> `/home/yanggon/05_VLA_LPDDR` (no `0007_26summer` prefix). `ONBOARDING.md` still spells the old prefix
> throughout — read every path there with the new prefix.

## Current status
**2026-09-25 — rename "P1" → "CoRe" (Column Reuse), committed, NOT pushed (main's task; user's decision 2026-09-25).**
Push only when main says so: first microarch-owner must (a) repoint the 14 auditor checks below and (b) relabel
the three PNGs that still bake in "P1". Definition used (from `microarch/00_doc/02_refs/related_work/README.md`,
"how P1 differs from DOTS"): one column access per column, shared across the V-vector activation tile resident in
the GB, one command; weights stay latched in the PU while only the activation changes each beat.
- **Renamed, by meaning:** Part III 24 (3 hand-worded + 21 plain; incl. the `#peek` title / TOC / Overview, SVG
  text in the §2 die figure (GB note) and in Fig. 6b (panel title, aria-label, caption)), Part III-2 5 (+ definition added to the §5 lead), Part IV 73 of 75
  (TOC, §2 h2 + lead, table heads, SVG labels in Figs. 1b/1c/6a/6b, alt texts, prior-art rows "Ours (CoRe)", all
  "CoRe alone", "CoRe + P4 + SW", "+CoRe+P4+SW"); Parts I and II, root `README.md` / `index.html`: 0 occurrences.
- **First definition with "access":** Part III Overview sentence + `#peek` paragraph ("Our CoRe (column reuse;
  `MAC_ABK_MV`, V = 26) changes which operand moves: one column access shared across the whole resident tile");
  Part III-2 §5 lead; Part IV §2 lead (+ "the column's weights stay latched in the PU while only the activation
  changes each beat"). Part IV DOTS callout now reads "DOTS reuses the row; CoRe reuses each column access across
  the whole resident tile. What DOTS saves is the row activation and the drain." (replaced "we reuse the fetch").
- **Scope trap fixed:** Part III `#peek` credited P1 with "the layer figure … 2.077 → 0.460 ms, 4.5×", which §7's
  table labels *full design*; now "the mechanism at the core of the full design (CoRe plus `LOOP` and the software
  fixes of Part IV) whose layer figure is …" (audited substring untouched). Full-design sentences stay full design.
- **Left as "P1" on purpose (problem id, not the mechanism):** Part IV §1 row label `P1` and "P1&ndash;P6 refine the
  classic AiM gaps" — the problem table numbers problems P1–P8; the Fix cell now says "**CoRe** (column reuse):
  `MAC_ABK_MV` + …". Ids `#p1`, `#p1-toy`, `#fig-frames-p1` kept (inbound anchors from Part III).
- **Observation, not changed:** Part IV quotes two "CoRe alone" D = 4 steps — 12.29 ms (ablation tier `p1_v26`,
  `paper_ablation.csv`, §2 table / §5 / scaling alt) and 18.21 ms (§9 prior-art rows, `c5_p1_5ns`, "stock attention
  path and no P4/SW" per that caption). Pre-existing; main's brief says 18.21. For evaluation-owner if it matters.
- **For microarch-owner (before the push):** relabel "P1" → "CoRe" in `phase6_ablation.png` ("+P1 MAC_ABK_MV (V = 26)",
  `plot_results.py` tiers list), `scaling.png` (same label, `plot_web_figs.py:200`) and `vendor_compare.png`
  ("AiM, +P1", `make_vendor_fig.py:67,76`); the alt texts / captions already say CoRe.
- Checks: HTML well-formed on all five pages (only the known `arrF` duplicate); `git diff --check` clean; the six
  changed inline SVGs rendered — no new collisions (pre-existing overflow in Part IV Fig. 6a's right panel noted).
- **Auditor against the working tree (scratch copy, `V` repointed; script untouched): 408 checks, 14 FAIL, 0 WAIT —
  all 14 are the renamed strings below; every "new" string was verified present in the normalised page.**
  For microarch-owner, old → new, verbatim (labels as the script prints them):

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

### Earlier status (2026-09-23)
**2026-09-23 — pushed `7710ac3` + `a512bc8` (user approved; mirror pulled, auditor 408 / 0 FAIL / 0 WAIT at `a512bc8`):** Part III (`02_stock_aim_offload/report.html`) gained an
**unnumbered** section `#peek` “Peek: our AiM P1 design” between §2 and §3 (48 lines added, 1 line
reworded-by-append). It answers the two questions the user asked while reading §2 (what toggles the DQ pins
16 times inside one burst — WCK 3.2 GHz, one beat per edge, 8 periods × 2 edges × 2 B = 32 B, with the
CA-sampled-every-0.625 ns command side as contrast; and how many PU cycles fit the same window — beat =
16 / (lanes × clk_GHz), D table at the 5 ns column: 200 MHz/16 lanes D = 1, 400/32 and 800/16 D = 4,
1 GHz/16 D = 5), then lands on D: stock `MAC_ABK` can use one beat per column (50 / 40 / 25 / 20 % from
§7 and Fig. 6c), P1 `MAC_ABK_MV` V = 26 uses all D (§7's 2.077 → 0.460 ms, 4.5×). Keeps the fairness
callout (stock rows carry the column-matched 200 MHz PU at 100 %; 25 % is headroom, not waste), the
why-800-MHz callout (edges coincide with CK → no new clock domain; hence “no arithmetic added” only for
fast-narrow) and the warn callout on the unit trap (“4-cycle BL” = 4 × 0.625 ns [A0] = 2 tCK real, vs
4 tCK = 5 ns = the same-bank-group spacing [A1]). A0/A1/A2 tagged. Also added: a TOC link (italic, no
number) and one appended sentence in the Overview's “How this page is organised” paragraph.
**Deliberately unnumbered** — §3/§7/§10/§11 are cited as text from Parts II and IV and carried by auditor
strings; renumbering would ripple into `verify_claims.py`, which is microarch-owner's.
**Deviation from the task, accepted by main and the user (2026-09-23) — keep it as written:** the task asked to cite the burst/BL-n facts to “[S1] the publicly
posted SK hynix 12 GB LPDDR5 spec H58GG6MK6GX037 Rev 1.1” by name. That document is stamped “SK hynix
Confidential” (primer `research_lpddr5_interface.md:13`, `research_lpddr5_core.md:11`), and the standing rule
is that confidential-stamped documents are neither named nor linked — which is also why the page already
attributes the quote to “a vendor package datasheet that reproduces the JESD209-5 text”. The aside therefore
cites the **standard's own text** (JESD209-5 bank-architecture §2.2 verbatim, incl. “one half-WCK-clock-cycle
data transfers at the I/O pins”) and its **“Effective Burst Length (BL/n) Definition” table** (4 tCK = 5 ns
same BG, 2 tCK = 2.5 ns different BG), read “in a vendor package specification that embeds the JEDEC text”.
No Rockchip / systemverilog.io rendering exists on this page, so nothing had to be displaced.
**Auditor:** 408 checks, 0 FAIL, 0 WAIT — both against the mirror at `9650131` and against this working tree
(scratch copy of `verify_claims.py` with `V` repointed; never edit the script). Re-run after the push.
HTML well-formed on all five pages, only the known duplicate `arrF` id; no inline SVG changed, so no PNG render
was needed. No numbers were wanted that the page or the primer did not already carry.

**2026-09-23, second aside pass — `b5d9be5` (pushed; user approved):** the `#peek` aside gained an h4 block
“Why that period is 5 ns and not 2.5 ns — and why the longer period is not a loss”, inserted after the D
table (not between the introducing sentence and its own table). It answers the user's follow-up: one burst
comes from one bank, while 32 B *every* 2.5 ns needs two bank groups taking turns; `MAC_ABK` hits every group
at once so consecutive MAC columns pay the same-bank-group 4 tCK = 5 ns (`nCCDMAC`, optional rank-level timing
param on `vla-aim-ext-d1`, `src/dram/impl/LPDDR5.cpp:661`; 8 cycles of 0.625 ns [A0] while RD/WR keep 4); that
5 ns is reasoned, not quoted [A1], which is why the 2.5 ns column stays as the optimistic sensitivity, and the
one citable escape is spatial (CD-PIM's split GBL/BLSA, 2 × 32 B per 5 ns, 400 MHz CUs, at the cost of a
bank-architecture change); 5 ns is per bank in parallel — 512 B / 5 ns = 102.4 GB/s per die, 8× external, with
6.4 GB/s per bank and 409.6 GB/s per x64 rank from the primer's published-figures list
(`00_doc/02_refs/lpddr_pim` notes, F4 and the bandwidth bullet); and the asymmetry — stock still uses one beat,
so utilisation falls 40 % → 25 % [A2] and the ISA fix is worth more at the honest period (3.60× vs 4.5× on the
layer). 11 lines, 0 deletions: nothing reworded, nothing for microarch-owner. Auditor 408 / 0 FAIL / 0 WAIT
against both the working tree and the mirror, now at `c74855b`. Pushed 2026-09-23 as part of
`a512bc8..c74855b` (`a041371`, `bd24019` bookkeeping, `b5d9be5` this block, `c74855b` its HANDOFF note);
only this closing HANDOFF edit is local and unpushed.

**2026-09-23, third aside pass — unpushed commit `4e6e853`:** the `#peek` aside gained a third h4 block,
“Where the PU clock comes from: CK, and a divider [assumption A2]”, after the 5 ns block (20 insertions,
0 deletions). Two clock inputs only (CK always on, WCK gated, no die oscillator); the die can divide but not
multiply (the standard's clocking figure puts oscillator/PLL on the controller side; LPDDR drops even the DLL —
Graham Allan / Synopsys 2012 and Malladi et al. ISCA'12, both named); **why CK and not WCK, written as the
correction it is** — the MAC datapath never touches the DQ pins, so no design needs WCK for the MAC and AiM
mode does **not** force WCK always-on; P1 does *less* pin traffic per unit of compute (1,925,760 GB refills vs
4,223,616 MAC columns, ~1 per 2.2 commands, §7); derivation table (800 = CK × 1 with no divider, 400 = CK ÷ 2,
200 = CK ÷ 4, all edge-aligned → no CDC; 1 GHz reachable from neither input: × 5/4, WCK ÷ 3 = 1.067 GHz,
WCK ÷ 4 = 800 MHz); divider vs PLL as a difference in kind (PIM-GPT's 1.5× DRAM routing factor); a warn callout
that **no CK divider exists today** (LPDDR5's ÷ 2 is in the WCK tree, whose initial state is “unpredictable” —
hence WCK2CK sync), so it is new but trivially cheap logic against 2.30 / 1.22 mm² of PIM block; and a win
callout closing on both realisations being CK-derivable while 1 GHz fails twice (no clock source, no rail;
CK-native only on GDDR6, where the fabbed preset's tCK = 1.0 ns). This is now where [A2] gets its rationale.
Included the WCK-restart observation, explicitly flagged “not modelled … an observation rather than a measured
cost”. **Dropped** the 0.10 / 0.14 mm² per-bank PU areas (not on any page; used the published 2.30 / 1.22 mm²
instead) — no new quantitative claim anywhere in the block. Sources read:
`00_doc/02_refs/lpddr5_primer/research_lpddr5_interface.md` §A5 + the WCK-divider bullet,
`research_lpddr_pim.md` (rail/frequency ceiling, PIM-GPT routing). Auditor 408 / 0 FAIL / 0 WAIT against both
the working tree and the mirror at `c74855b`. **Unpushed:** `927a45a`, `cdb5516` (bookkeeping) and `4e6e853`.

### Previous status
Five pages live and in sync with `origin/main` at `7be5ecf` (pushed 2026-09-22; mirror checkout pulled). **Claim auditor: 398 PASS, 0 FAIL, 0 WAIT** — the third pass committed microarch's corrected PNGs (`platforms.png` legend below the axes, `crossover.png` 2.5 ns point 8.15, `scaling.png` hollow curve 13.96 / 8.15 / 5.29), rounded the NX latency ratio once (12.6055 / 16.272 = 0.7747 → 0.77×, six sentences on Parts II and IV) and re-worded the Part III Fig. 4 alt text (8.15 ms at 2.5 ns). The seven `wait=` flags in `verify_claims.py` now PASS and can be dropped by microarch-owner (strings in `AUDITOR_STRINGS.md`, "Third pass").
Previous state (second pass, `8f13a75`): **The site is restated at the primary design point** (user decision 2026-09-21: 5 ns all-bank column, PU rate D = 4 realised as fast-narrow 16 @ 800 MHz on CK or slow-wide 32 @ 400 MHz, 1.05 V / 0.9 V; D = 2 = 15.32 ms and D = 1 = 27.44 ms beside; the 2.5 ns column / 1 GHz PU = 8.15 ms is a sensitivity). Numbers come from `evaluation/p1/numbers.md` (+ `paper_ablation.csv` for the V sweep and the Orin NX 8-ch point, `prior_art_5ns.csv` for CENT / P3-LLM / LP-Spec at 5 ns, the paper for the 15/30 W ratios). **Second pass done 2026-09-22:** the nine PNGs are at the primary point and captioned so (no "pending" label left), the seven rounding WAITs are fixed (55 mJ, 0.86×, ≈6.7×, 7 %), Orin NX is restated at the primary point (16.27 ms; only its 15 W energy and Thor's 40 W energy stay at 2.5 ns, `†`-labelled), Part IV §9's primary table holds all seven mechanisms at 5 ns, Part III-2's KPI is P1 alone at V = 26 (4.0× / 3.1×). **Claim auditor after the push: 11 FAIL, 1 WAIT** — every one is a check whose sentence the task restated on purpose (the NX column / scale-down / partition sentences, the breakdown-figure alt text) or whose `wait=` should now be dropped; the exact new strings and CSV selectors are in `AUDITOR_STRINGS.md` ("Second pass"). The pre-push validation used a scratch copy of `verify_claims.py` with `V` pointed at the working tree (never edit the script itself).
HTML well-formed on all pages (the known duplicate `arrF` marker in Part III remains); every href, `#anchor`, `<img src>` and `url(#…)` resolves; `realistic` 0 hits. Working tree clean. The site carries no PDFs.

### What each page says now
- **Part IV** (`03_extended_isa`): title/h1/KPIs 40.24 → 9.31 ms (4.32×), 5.87 ms at 32 ch (1.07× under the 6.30 ms bound), 2.59 Hz. §2: new callout `#rate-d` (D defined once, the two realisations, "no arithmetic added" scoped to fast-narrow), "Charged honestly" restated to the simulated PU (52 cycles per MV column at V = 26), GB delivery 1.25 / 2.5 ns [ASSUMPTION], V = 16 clock walk restated (2,260 cycles / 141 per token, [computed here]); V sweep and "where the time goes" tables kept and labelled 2.5 ns / 1 GHz with the paper's primary-point V sweep quoted in prose; lane ladder at 800 MHz (16/32/64/128 lanes = 9.31 / 6.30 / 4.81 / 4.24 ms) with slow-wide, D = 2 / D = 1 and 1 GHz rows; primary-point counters table (263,976 → 10,224 MAC16, 3,322,766 → 736,603 cycles) above the old itemised table (labelled). §5: primary ladder table (40.24 → 12.29 → 10.45 → 11.97 head-of-line → 9.45 → 9.31; 32 ch beside; D = 2 / D = 1 / 1 GHz rows) above the old tier ladder (labelled; the only place 8 ch / P7 / GB tiers survive). §6: two-fixes table labelled, primary-point paragraph added. §7: system table at 414 / 387 ms (2.41 / 2.59 Hz, 32 ch rows), overlap SVG rescaled (1.93 px/ms). §8: energy 470 vs 194 vs 138 / 130 / 117 mJ (PU-priced model; PIM-GPT anchor beside), EDP 0.95× / 1.24×, new trade-off table (`#tradeoff`, mirrors the paper's tab:tradeoff) and D-ratio table (tab:dratio), platform matrix with a primary-point AGX column and the NX / Thor columns labelled 2.5 ns / 1 GHz. §9: prior-art table at 5 ns (stock, DOTS-26 charged/hidden, P1 at D = 1/2/4, slow-wide rows) above the old 2.5 ns transplant table (CENT / P3-LLM / LP-Spec kept, labelled); depth table uses the paper's V mapping (26.41 / 15.37 / 14.99 / 11.97). Stale in-page §-refs fixed (§8 → §7 for system view, §7 → §6 for broadcast).
- **Part III** (`02_stock_aim_offload`): title "loses 6.4×"; KPIs 40.2 ms, 8×, S ≤ ~7. §2: sentences that stated 2.5 ns as ours now call it the sensitivity (bank-groups callout, column-path pacing, Fig. 0a-3 caption/paragraph/callout). §3: tCCD row shows 4 (RD/WR) / 8 (all-bank MAC). §4: opportunity table highlights the 5 ns / 8× row; assumptions callout A0/A1/A2 as decided. §5/§6: 8× gap, 64 % / 11 % shares. §7: timing bullets (8-cycle MAC column, simulated D = 4 PU), retiming table with a 5 ns column (2.077 / 0.460 ms, 4.5×). §8: 1.64 TB/s, 0.38 ms. §10: frames cost "8 cyc each × 64", clock walk 652 / 684 cycles, budget table 4,096 / 1,152 / 256, **Fig. 6b regenerated** (`#fig-slot`, 25 % busy, 32 cycles per MV column; generator not kept), `#where60` heading "Where the idle 75 % comes from" (id kept), vocabulary/derivation at 5 ns and D = 4, "nCCD = 2 nBL" paragraph, substrate table with 5 ns rows, **Fig. 6c** extended to five rows (viewBox 330), `#gbrate` at 1.25 / 2.5 ns with the D = 1 / D = 2 fallbacks (27.44 / 15.32), vendor-choice table (a) 200 MHz, (b) 20 %, (c) D = 4. §11: Fig. 7a bars 64 / 14 / 11 / 5 / 6 % of 2.08 ms, fetch floor 21 µs, table cycles row, ideal caption. §12: tables at 40.24 / 23.64 ms with the 2.5 ns rows beside, energy 470 vs 194 (138 / 130 / 117), crossover S ≈ 7, 1.64 TB/s / 1.6 TFLOP/s. §13 Q8: 512 cycles, 5 %.
- **Part II** (`01_deployment_platforms`): KPI 14.6× / 24×; 10 of 12 cells; matrix with a primary-point AGX column (14.6 / 24.2, 1.35 / 2.52, 0.68 / 1.41, 0.34 / 0.86) and a primary-point NX column on latency (1.55 / 0.77 / 0.39×; energy cells `†` = 2.5 ns, 124 mJ at 15 W) beside the AGX-sensitivity and Thor columns labelled 2.5 ns / 1 GHz; compiled-Thor rung ≈2.6× (primary) / ≈2.9× and ≈6.7× (sensitivity); §4 lead / Fig. 1 / §6 anchors and scale-down at 16.27 ms (1.29× the NX bound; 14.01 ms beside); 32 ch 5.87 ms. PNG captions and alt texts describe the primary-point figures.
- **Part I**: forward reference 4.32×, 37 ms, 387 ms / 2.59 Hz; "Parts III–III" typo fixed. **Part III-2**: AiM cross-references labelled as the 2.5 ns column; its own numbers untouched (Samsung model not re-run at 5 ns); KPI now "AiM P1 alone at V = 26: 4.0× at its 5 ns primary point, 3.1× at this page's 2.5 ns column" (`paper_ablation.csv` tier `p1_v26`, sim: 2.077 → 0.524, 1.427 → 0.459) and the comparison row split into P1 alone (3.1×) / full design (3.6×) — like-for-like with Samsung's MACV-only 1.11×.
- **Part III** additions of the second pass: figure captions at the primary point (breakdown figure = hybrid-B layer 2.55 ms = 63 / 9 / 3 / 12 / 6 / 7 %, the prose keeps the Strategy-A 2.08 ms = 64 / 14 / 11 / 6 / 5 %), overhead-sweep caption 38.6 → 43.6 ms (26.9 → 31.9 at 2.5 ns), host idle 55 mJ. **Part IV** additions: §5 / §6 / §8 captions and alt texts at the primary point (ablation 40.24 → 12.29 → 10.45 → 11.97 → 9.45 → 9.31 with the 2.5 ns hollow bars 28.55 / 11.13 / 9.29 / 8.19 / 8.00 / 8.11; scaling 16.27 / 9.31 / 5.87), §7 partition note and §8 scale-down / matrix / callout at NX 16.27 ms, trade-off row 32-ch slow-wide 1.05 V PIM-GPT 1.19× (ledger value; the hand-off said 1.20), §9 primary table with CENT 38.80 / 1.04× / 462 mJ, P3-LLM 25.61 / 1.57× / 327, LP-Spec 19.36 / 2.08× / 307 (PU beat per design: 16 @ 200, 16 @ 400, 64 @ 200; ours 16 @ 800), the standing change "P1 alone 18.21 beats LP-Spec 19.36 with a quarter of the multipliers; at 2.5 ns it did not (15.15 vs 14.81)", the 2.5 ns table kept as the labelled sensitivity.
- Root `index.html` 08_VLA box and `README.md` 08_VLA block: new titles; README paths / part order corrected.

### Decisions taken in this pass (report them; not reopened)
- Second pass: NX latency restated at the primary point from `paper_ablation.csv` (not the ledger); NX 15 W and Thor 40 W energies stay at 2.5 ns with a `†` footnote under both matrices. The 2.5 ns prior-art table is kept as a labelled sensitivity (not folded into a column). PIM-GPT 32-ch slow-wide ratio written as 1.19× (ledger / CSV: 231.5 / 194.0), not the 1.20× in the hand-off. Part III-2 KPI shows P1-only 4.0× (5 ns) with 3.1× (2.5 ns) beside, the 3.6× row relabelled "full design".
- First pass: NX (8 ch) and Thor (40 W) columns kept at the 2.5 ns / 1 GHz point, labelled — no primary-point row exists in the ledger. AGX column restated. Same in Part IV §8.
- V-sweep table and "where the time goes" kept at 2.5 ns / 1 GHz (labelled); the paper's primary-point V sweep (26.41 … 19.35 ms) quoted in prose — those values are from `paper_ablation.csv`, not the ledger.
- Prior art: DOTS restated at 5 ns with 26 latches (ledger); CENT / P3-LLM / LP-Spec kept in a second labelled 2.5 ns table (no 5 ns rows).
- Pedagogical cycle walks (Part III §10, Part IV §2 V = 16 example) recomputed from A0–A2 and tagged "[computed here]" as before.
- 15 / 30 W energy ratios (1.22× / 1.74×) quoted from the paper (auditor-checked there; not in the ledger).

### Key numbers (primary point, 16 ch unless said; ledger ids in `AUDITOR_STRINGS.md`)
Stock 40.24 ms / 470 mJ (32 ch 23.64 / 535); 6.4× the 6.30 ms optimistic bound (2× floor), 12.8× the 3.15 ms floor. Full design 9.31 ms (4.32×; 1.48× above the bound; 14.6× vs the 136 ms measured stack), 5.87 ms at 32 ch (4.02×; 1.07× under the bound). Ladder 40.24 → 12.29 → 10.45 → (11.97 with 64-col lines) → 9.45 → 9.31; 32 ch 23.64 → 9.27 → 7.43 → 7.21 → 5.94 → 5.87. D = 2 15.32 (8.93), D = 1 27.44 (15.10), 2.5 ns / 1 GHz 8.15 (5.29). Energy fast-narrow / slow-wide 1.05 V / 0.9 V: 138 / 130 / 117 mJ (0.71 / 0.67 / 0.60× of 194; PIM-GPT 227 / 200 / 168 = 1.17 / 1.03 / 0.87×); 32 ch 168 / 161 / 148. Sweep power 558 / 434 / 322 mW (2.89 / 2.25 / 1.67× stock 193); area 2.30 / 2.96 / 2.96 mm² (3.8 / 4.9 %), +1.07 over stock 1.22, +0.66 slow-wide over fast-narrow. e2e N = 4: serial 414 ms 2.41 Hz (16 ch), 401 ms 2.50 Hz (32); overlapped 387 ms 2.59 Hz, 380 ms 2.63 Hz; bound 402 ms 2.49 Hz; N = 10 2.41 / 2.52 vs 2.27 Hz. P1-only 18.21 ms (2.21×; 2.37× / 1.71× vs DOTS-26 charged 43.06 / hidden 31.21); full design 4.63× / 3.35× (cross-scope). cmdbreak at 5 ns: 64 / 11 / 14 / 6 / 5 % (MAC / TMOD / GB / blocking / row) of 2.08 ms. Never 8.19 ms, never 295 mJ, never "realistic".

## Recent decisions
- 2026-09-23 `7710ac3` `a512bc8` (main's task; push approved by the user the same day): Part III unnumbered aside `#peek` “Peek: our
  AiM P1 design” after §2. Purely additive text (plus one appended Overview sentence and a TOC line), so no
  audited string moved; nothing for microarch-owner. Provenance cited to the JEDEC text and its BL/n table
  rather than to the confidential-stamped vendor spec (see Current status).
- 2026-09-22 `3380b81` `7be5ecf` (main's task; push approved): **third pass — auditor fully green.** Three corrected PNGs from microarch committed (looked at each: legends and labels clear; cosmetic only: in `crossover.png` the "8.15 (2.5 ns)" label touches the green staircase, in `scaling.png` the "XPU optimistic 2× (6.30)" label crosses the green curve). NX ratio 0.78 → 0.77× (rounded once from the CSV: 12.6055 / 16.272) in Part IV §8 NX best / matrix 2× NX cell / callout and Part II Fig. 1 caption / matrix 2× NX cell / anchors NX; the `0.78×` left on Part IV (§8 trade-off notes, MAC-sweep power) is a different ratio. Part III Fig. 4 alt: "about 8.2 ms" → "8.15 ms at 2.5 ns". Auditor on the mirror at `7be5ecf`: 398 PASS, 0 FAIL, 0 WAIT.
- 2026-09-22 `d3b8199` `b7e82eb` `d2973c6` `cffc606` `dc09c3a` `8f13a75` (main's task; push approved): **second primary-point pass** — PNGs committed, captions / alt texts rewritten, seven rounding slips fixed, NX at 16.27 ms, prior art at 5 ns, III-2 KPI. For microarch-owner (figures): `crossover.png` labels the 2.5 ns full-design point "8.19" (the 64-column tier) while `phase6_ablation.png` says 8.11 and `scaling.png` ≈ 8.15; `platforms.png`'s legend overlaps the Thor bars' value labels.
- 2026-09-22 `ccc96cf` `8281ca2` `045359a` `9cc4f0b` (user: "Do it"; push approved): **site restated at the primary design point** — see "What each page says now" above and `AUDITOR_STRINGS.md`. Auditor 35 site FAILs pending microarch-owner's re-pointing; paper checks 0 FAIL.
- 2026-09-21 `4dd20c1` (user asked, approved push): **Q8 `#faq-tras-tccd` "relationship between tRAS and tCCD" added** to §13 group `#qa-s2` after Q7, with new inline timeline **Fig. L2-2** `#fig-tras-tccd` (row path grey, column path green, no markers; cases n = 2 and n = 10). §2 `#cell` gained a pointer paragraph to Q8 right after Fig. L2. Values checked against `microarch/00_doc/02_refs/lpddr5_primer/research_lpddr5_core.md` §B (tRCD 18, tRAS 42, tWR 34, tRBTP 5 ns, BL/n 5 / 2.5 ns): all agree. One nuance: the notes define tRBTP from the *end of the read burst slot* (BL/n_min = 2.5 ns after RD), so RD → PRE is 7.5 ns, not 5; the figure draws RD as a 2.5 ns slot followed by a 5 ns tRBTP box (PRE at 30.5 / 70.5 ns) and the text only says "about 5 ns … that follows the last read", "about 70 ns", "about five columns", "≈ 340 ns", which hold under either reading. Crossover and 340 ns are tagged "[computed here]"; the traces paragraph is tagged "[preset, in simulator cycles]" and uses only on-page numbers (34, 256, 56, 17 cycles, 26 beats, 7%). Figure was produced by a throw-away generator (not kept); edit the SVG in place.
- 2026-09-21 (user: "delete all the pdfs from the vercel pages"): **PDF exports deleted; the site carries no PDFs; do not regenerate or commit exports unless asked.** Removed the untracked `08_VLA/pdf/` (five WeasyPrint exports of 2026-09-17 + `print.css`). Never tracked, never linked, so nothing was published: no commit, no push, no auditor run needed. Reverses the 2026-09-20 "keep and commit `pdf/`" decision. Recipe (command + `print.css` verbatim) preserved in `ONBOARDING.md` §10. The external `.pdf` source links on the pages are untouched.
- 2026-09-21 `8620062` (user asked, approved push): **Q4 `#faq-phy` fact-checked against public sources; Q7 `#faq-act` added** (one ACT = one full-width row of the bank; `pre.cmd` text sketch; Fig. L3 caption links to it, SVG untouched). New source bullet "Memory PHY and HBM interface" in `#lpddr-sources`. Fact-check note (claim → verdict → source → change):
  1. PHY = mixed-signal block between controller and pins; controller = protocol/timing → **TRUE** — Feldmann et al. arXiv 2503.11654; DFI spec (ddr-phy.org). No change.
  2. PHY functions (serialise, RDQS capture + FIFO, PLL, drivers/ODT/ZQ/VREF, LPDDR5X equalisation, delay lines + trainings, drift) → **TRUE** — NXP AMF-AUT-T3361 (PHY PLL, Read FIFO, ZQ, VREF, CBT / write leveling / gate / eye / VREF training, delay-line VT compensation); Synopsys LPDDR5X/5/4X PHY page (firmware training, DFE + pre-emphasis, DCA, DFI 5.0). Wording tightened ("typically through a read FIFO", "on-die termination", equalisation named, firmware training + drift compensation).
  3. "no DLL so the PHY absorbs all timing uncertainty / matters more than for DDR" → **PARTLY** — NXP deck: DDR4 also needs write leveling, gate, eye and VREF training; only LPDDR4 needs DQS drift detection because "tDQSCK for DDR3/4 are kept relatively constant by DRAM". Rewritten as "LPDDR leaves more of the timing burden on the host"; "all" removed; bracket says the published example is LPDDR4.
  4. DFI is the controller–PHY boundary, hence separate IP → **TRUE with nuance** — Synopsys DFI blog ("designed separately – often by different companies"; DFI not needed when designed together). Reworded to "exists so that … fit together".
  5. HBM: "1,700 signals" → **PARTLY**: 1,024-bit data bus; ~1,700 *interconnects* including control, power, ground (Rambus "Why HBM2 is all about the PHY", Rambus HBM2E guide). Few mm + unterminated → **TRUE** (FGDRAM MICRO'17 §3.3: 5–7 mm, "simple unterminated signaling"). "far less energy per bit" → **UNVERIFIABLE as a comparison** (the page's own LPDDR5 VDDQ-only arithmetic is 0.34–0.52 pJ/bit, same order as HBM2's 0.3): comparison removed, kept FGDRAM's 0.3 of 3.97 pJ/bit. Training → TRUE (Synopsys HBM3 PHY: PHY-independent training, DFI 5.0). Lane repair / IEEE 1500 → TRUE (Rambus). Base die holds PHYs next to TSV area → TRUE (FGDRAM §3.2–3.3).
  6. "PIM sends only commands through the PHY" → **series' framing, and overstated** vs §5/§10 (WR_GB writes the input vector, RD_MAC reads results over the pins). Callout now labelled "our framing, not a sourced fact": weights never cross; commands, the short input vector and the short result do.
  Not independently sourced (left as general background, no number): WCK2CK leveling and duty-cycle adjustment as *PHY-side* state machines (they are JEDEC LPDDR5 trainings per the Synopsys LPDDR5 article already cited); Cadence PHY pages returned HTTP 403 and were not used.
- 2026-09-21 `178c614` (user asked, approved push): **questions live in the last section, content and figures stay in the body.** Part III gained §13 `#qa` with six items: `#faq-ranks`, `#faq-clocks`, `#faq-rate` (moved from §1, ids kept), new `#faq-phy`, `#faq-die` (group `#qa-s1`, about §1) and `#faq-subarray` (group `#qa-s2`, about §2); each ends with a "Back to the page" line. `#lpddr-faq` survives as an empty `<span>` at the top of §13. §1 keeps Fig. L1-2 under a new h3 `#ranks` with a body paragraph, plus a "Two reading aids" paragraph (differential CK; 6,400 MT/s per pin). §2 `#hier` now says the row is sensed in place by the sense amplifiers of its own sub-array (2 KB real / 32 KB simulator). Overview's "How this page is organised" mentions §13. Source list gained RowClone (MICRO'13) and LISA (HPCA'16). New questions go into §13 under the group of the section they refer to (add `#qa-s3` … as needed), numbered Q7 onward; facts needed by later sections go in the body with a link to the answer.
- 2026-09-21 `ad31892` (user asked, approved push): Part III §1 gained a "Common questions" block `#lpddr-faq` (`#faq-ranks`, `#faq-clocks`, `#faq-rate`) between the Fig. L1 bandwidth paragraph and "Four supply rails", with new inline figure **Fig. L1-2** `#fig-ranks` (two ranks on one x16 channel, private CS0/CS1, rank-level timeline; no SVG markers used). Background only: no audited string touched, no new source. The 12 GB "4 channels × 2 chip-selects" package example is paraphrased, not quoted, because its datasheet is stamped confidential; the Orin rank/die split is labelled as an example. The figure was produced by a throw-away generator script (not kept); edit the SVG in place.
- 2026-09-20 (user): ~~keep and commit `pdf/`~~ (reversed 2026-09-21, above); site-owner runs the auditor itself after a push; site-owner owns the 08_VLA block of `README.md` and its `index.html` box; Part III-2 is to be added to the auditor (microarch-owner).
- 2026-09-20 `ebda70d`: Part III re-organised into 12 sections; §1–4 are an LPDDR5 primer (figures L1–L5, 0a, 0a-2, 0a-3, 0b); assumptions labelled A0 (0.625 ns cycle), A1 (2.5 ns all-bank column; real LPDDR5 5 ns per bank group), A2 (1 GHz PU).
- 2026-09-19 `ff6efe4`: the 6.30 ms rung is the "optimistic bound (2× floor)", never "realistic" (0 hits today).
- 2026-09-18 `f79b717`: GB-delivery-rate assumption behind P1 stated on Parts III/IV (`#gbrate`); DOTS compared at D = 1.
- 2026-09-15 `c1ad207` / `1331001`: part order I algorithm, II platforms, III problem, IV solution; Part III-2 added.
- Standing: private vendor correspondence never cited or named; confidential-stamped documents not linked; commit identity `yanggon-kim <yanggon@g.ucla.edu>`.

## Open issues
0. ~~**P0** — 11 FAIL + 1 WAIT after `8f13a75`~~ done: microarch re-pointed the checks (`14d5515`), third pass fixed the rounding; 0 FAIL, 0 WAIT at `7be5ecf`. Left for microarch-owner: drop the seven now-passing `wait=` arguments in `verify_claims.py` (cosmetic; they only print when a string is missing).
0b. ~~**P1** — Stale PNGs~~ done 2026-09-22 (second pass).
0c. **P2** — No primary-point *energy* rows for Orin NX (15 W) and Thor (40 W): those cells stay at 2.5 ns, `†`-labelled — for evaluation-owner / microarch-owner. The NX latency is restated (`paper_ablation.csv`, not in the ledger — for evaluation-owner to collect).
0d. **P3** — Part II KPI tag / callout "10 of 12 cells" predates the extra primary-point columns (the matrix now has 16 energy cells, 13 favorable); wording untouched, unaudited.
1. ~~**P1** — Part IV stale internal section numbers~~ fixed 2026-09-22 (§8 → §7 for the system view, §7 → §6 for broadcast, the 1.02× sentence rewritten; "priced in §6" is correct).
2. ~~**P1** — Part IV KPI "2.65 Hz" vs "2.60 Hz"~~ superseded: every rate now reads 2.59 Hz (primary point).
3. ~~**P1** — Part III-2 KPI "AiM: 2.70×"~~ fixed 2026-09-22 (P1 alone 4.0× / 3.1×; check string for `p3b kpi` in `AUDITOR_STRINGS.md`).
4. **P2** — Duplicate SVG marker id `arrF` ×4 in Part III (`:260, 853, 1231, 1775`).
5. **P2** — Part IV `:587` "(Fig. 6b)" means Part III's figure but collides with Part IV's own Fig. 6b (`:1061`); labels "Fig. 11a" (`:519`) and "Fig. 3a/3b" vs "Fig. 3" are confusing.
6. **P2** — Repo `README.md:46-57` lists old 08_VLA directory names, old part order, 9.77 ms / 5.8× (shared file — needs permission).
7. **P3** — Orphan `02_stock_aim_offload/assets/phase3_overhead_sensitivity.png`; `vendor_compare.png` absent from `sync_site_figs.py` MAP.
8. **P3** — A0/A1/A2 labels exist only in Part III; Parts III-2 and IV depend on A1 without naming it (paper-side caveat also pending, per microarch).

## Next steps
0. ~~Push `7710ac3`~~ done: `9650131..a512bc8` pushed 2026-09-23, mirror pulled, auditor 408 checks, 0 FAIL,
   0 WAIT. **Queued as its own task (do not fold into other work):** rewrite the stale `0007_26summer/` path
   prefix in `ONBOARDING.md` (11 places) and `HANDOFF.md` (2) — `relocate.sh` missed this root's own two
   files and `check_setup.py` does not read them, so no gate caught it (main, 2026-09-23).
   Follow-up pushed too: `a512bc8..c74855b` (2026-09-23), mirror pulled, auditor 408 / 0 FAIL / 0 WAIT.
1. ~~Auditor green~~ done (`7be5ecf`: 398 PASS, 0 FAIL, 0 WAIT). After microarch drops the `wait=` flags, re-run once to confirm nothing changed.
2. ~~Corrected PNGs + crossover alt~~ done `3380b81` / `7be5ecf`.
3. Issues 4–5 (rename markers `arrF1…4`; qualify cross-page figure refs as "Part III Fig. 6b").
4. If evaluation-owner collects the V sweep and the 15 / 30 W rows into the ledger, swap the paper-sourced citations in `AUDITOR_STRINGS.md` for ledger ids.

## Interfaces with other sub-projects
- **microarch-owner** (`/home/yanggon/0007_26summer/05_VLA_LPDDR/microarch`): provides every number (`04_data`, `05_reports`), every PNG (`plot_web_figs.py` → `sync_site_figs.py`, which writes into `08_VLA/*/assets/`), and the claim auditor + its read-only checkout `03_tools/versel_distribute`. Site changes that alter an audited string require a matching auditor edit by microarch-owner; after each push: pull checkout, run auditor from cwd = microarch, expect `0 FAIL(s)`.
- **paper-owner**: none (paper and site share the auditor but not files; keep wording rules aligned).
- **jetson-owner**: none directly; future measured Jetson numbers arrive via microarch (data → figures → auditor) before appearing on the pages.
