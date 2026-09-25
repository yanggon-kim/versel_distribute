# ONBOARDING history — 08_VLA
*Survey-time snapshots, dated narrative and the retired PDF recipe, moved verbatim out of `ONBOARDING.md` on 2026-09-25 (nothing deleted). Not current state — see `HANDOFF.md`.*

## From §3 (survey-time check results)
Result today: (a) 0 mismatches on all pages, one duplicate id (§7). (b) verified working on Part III-2.
- Auditor result at survey time (moved from the §3 "Publish" paragraph): today: 123 PASS, 0 FAIL, checkout at `ebda70d`.

## From §4 Git (survey-time snapshot)
- Repo `/home/yanggon/0007_26summer/versel_distribute`, remote `origin git@github.com:yanggon-kim/versel_distribute.git`, branch `main` tracking `origin/main`, in sync at `ebda70d`. No `.gitignore`, no `vercel.json`.
- `git status --short` now: clean (the untracked `08_VLA/pdf/` exports were deleted 2026-09-21, see §9–§10). (`08_VLA/ONBOARDING.md`, `08_VLA/HANDOFF.md` are hidden via `.git/info/exclude`.)
- Last 5 commits touching `08_VLA` (56 in total): `ebda70d` 09-20 Part III: four-section LPDDR5 primer, re-ordered and renumbered (12 sections), fact-checked · `ff6efe4` 09-19 rename 'realistic' → 'optimistic' (text, alt text, figures) · `13aa637` 09-19 Part III §1: die by timing domain + 2.5 ns ruler · `f79b717` 09-18 Parts III/IV: GB-delivery-rate assumption behind P1; DOTS at D = 1 · `dba8d17` 09-18 Part IV §9: DOTS re-measured.

## §7 Current state (survey-time findings, 2026-09-20; most since fixed or tracked in HANDOFF open issues)
Latest change: `ebda70d` (2026-09-20 13:44) re-organised Part III into 12 sections with the LPDDR5 primer; `index.html` titles already match (4.5×, 28.55 → 8.15). Auditor 0 FAIL; all hrefs, anchors, `<img src>` and `url(#…)` resolve. Findings (not fixed):
1. **Part IV stale internal section refs (off by one; inferred from content):** `03_extended_isa/report.html:114` and `:883` say P3 "enables §8" (concurrency is §7 System view; §8 is Energy); `:669` "§8 shows the end-to-end gap between 16 and 64 lanes is only 1.02×" (overlap is §7, and "1.02" occurs nowhere else on the page — claim unsupported); `:938`, `:941` "§7 below — the broadcast fix" (broadcast is §6). `:887` "priced in §6" — verify.
2. **Part IV KPI inconsistent:** `03_extended_isa/report.html:101` "2.65 Hz" vs table `:1138` and text `:1186` "2.60 Hz" (the audited string is 2.60, `verify_claims.py` check "p3 fresh tail"). **Part III-2 KPI inconsistent:** `02b_samsung_pim/report.html:99` "AiM: 2.70×" vs the same page `:274` "1.427 → 0.396 ms/layer (3.6×)" and Part IV's 3.5× (`03_extended_isa/report.html:85`). Unaudited page.
3. **Duplicate marker id** `arrF` ×4 in Part III (`02_stock_aim_offload/report.html:260, 853, 1231, 1775`) — violates the unique-marker rule; definitions look identical so rendering is unaffected (inferred). Part IV has its own single `arrF` (`:364`), which is fine.
4. **Ambiguous figure reference:** `03_extended_isa/report.html:587` "(Fig. 6b)" means Part III's Fig. 6b (PU busy 40 %), but Part IV has its own Fig. 6b (`:1061`). Odd label "Fig. 11a" at `:519`; "Fig. 3a/3b" (`:774,830`) coexist with "Fig. 3" (`:1183`).
5. `README.md:46-57` stale 08_VLA paths/numbers (repo-level file; shared).
6. Orphan asset `02_stock_aim_offload/assets/phase3_overhead_sensitivity.png`; `vendor_compare.png` not in `sync_site_figs.py` MAP. · (`pdf/` exports: deleted 2026-09-21.)
7. Clean greps: "realistic" — 0 hits in all five pages; "tCCD_L/tCCD_S" — only in literature context (III:525, 1760, 2028; IV:1258, 1268), consistent with A1 wording. · Assumption labels A0–A2 are defined only in Part III; Parts III-2 (`:192` "tCCD = 4 … identical to Part III") and IV rely on them without the label (IV:591 links to III `#gbrate`).

## From §9 Decisions (dated narrative)
## 9. Decisions by the user (2026-09-20) — no open questions
- **2026-09-21 (user): PDF exports deleted; the site carries no PDFs; do not regenerate or commit exports unless asked.** This reverses the 2026-09-20 decision to keep and commit `08_VLA/pdf/`. The folder was never tracked or linked, so nothing was ever published. Recipe preserved in §10.
- Part III-2 **joins the auditor**: adding the checks is microarch-owner's work; the correct value of its "AiM: 2.70×" KPI is settled with microarch-owner's data before the page is changed.

## 10. PDF export recipe (exports are not kept)
Only if the user asks for PDFs again. The five exports (deleted 2026-09-21) were made with WeasyPrint (`~/.local/bin/weasyprint`, not in the microarch venv), one run per page, with this print stylesheet saved as `print.css`:
```bash
~/.local/bin/weasyprint -s print.css <page>/report.html <out>.pdf   # e.g. 00_vla_algorithm/report.html Part_I_VLA_Algorithm.pdf
```
Output names used: `Part_I_VLA_Algorithm.pdf`, `Part_II_Deployment_Platforms.pdf`, `Part_III_Stock_AiM_Offload.pdf`, `Part_III-2_Samsung_PIM.pdf`, `Part_IV_Extended_ISA.pdf`. `print.css` verbatim:
```css
@page { size: A4; margin: 14mm 12mm 16mm 12mm; @bottom-center { content: counter(page) " / " counter(pages); font-size: 8pt; color: #647083; } }
nav.toc { display: none !important; }
.wrap { display: block !important; width: auto !important; padding: 0 !important; }
body { background: #fff !important; font-size: 10pt; line-height: 1.45; }
section.card { box-shadow: none !important; border: none !important; padding: 4mm 0 !important; margin-bottom: 6mm !important; break-inside: auto; }
section.card > h2 { break-after: avoid; }
h3, h4 { break-after: avoid; }
.scroll { overflow: visible !important; }
table { font-size: 7.5pt !important; table-layout: auto; width: 100% !important; break-inside: auto; }
th, td { padding: 3px 5px !important; word-break: break-word; overflow-wrap: anywhere; }
tr { break-inside: avoid; }
pre.cmd { font-size: 7pt !important; line-height: 1.35 !important; white-space: pre-wrap; overflow-wrap: anywhere; break-inside: avoid; }
.fig, figure, .callout, .kpi { break-inside: avoid; }
.fig svg { max-height: 120mm; }
figure img { max-height: 110mm; width: auto; max-width: 100%; }
a { color: inherit; text-decoration: none; }
.headline { grid-template-columns: repeat(4, 1fr) !important; }
header.page h1 { font-size: 20pt !important; line-height: 1.2; }
header.page .sub { font-size: 9.5pt; }
```


## Footer of the original ONBOARDING.md
*`ONBOARDING.md` / `HANDOFF.md` are tracked since the 2026-09-22 server move, so site-owner's state travels with the repo.*
