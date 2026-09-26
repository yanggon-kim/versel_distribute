# ONBOARDING — 08_VLA ("VLA × LPDDR-PIM" site section)
*Survey date 2026-09-20, repo HEAD `ebda70d`. Paths relative to `/home/yanggon/versel_distribute/` unless absolute. "(inferred)" marks anything not read directly from a file.*
## 1. Identity
- **Is:** the public, hand-written HTML write-up of the VLA-on-LPDDR5-AiM research, five pages ("Part I–IV" + "III-2"), published as one section of the static Vercel site <https://versel-distribute.vercel.app/> (`CLAUDE.md` §"What this repo is"; section box at `index.html:288-303`).
- **Is not:** a place where numbers are produced. Every quantitative claim comes from `/home/yanggon/05_VLA_LPDDR/microarch` (simulator caches, CSVs, figures) and is string-audited from there (`microarch/03_tools/verify_claims.py:1-18`). No build system, no JS framework, no tests in this repo (`CLAUDE.md` §Commands). Not the paper (`05_VLA_LPDDR/paper`), not the other `00_`–`07_` sections.
## 2. Layout
| Dir | Part | `report.html` (bytes / lines) | inline SVG | `assets/` |
|---|---|---|---|---|
| `08_VLA/00_vla_algorithm` | I | 49 919 / 460 | 3 | `roofline.png`, `paper_breakdown.png` |
| `08_VLA/01_deployment_platforms` | II | 24 478 / 209 | 0 | `platforms.png`, `energy.png` |
| `08_VLA/02_stock_aim_offload` | III | 285 069 / 2042 | 15 | `phase3_step_latency.png`, `phase3_layer_breakdown.png`, `energy.png`, `crossover.png`, `phase3_overhead_sensitivity.png` (orphan: no `<img>` uses it) |
| `08_VLA/02b_samsung_pim` | III-2 | 34 358 / 314 | 1 | `vendor_compare.png` |
| `08_VLA/03_extended_isa` | IV | 164 938 / 1308 | 8 | `phase6_ablation.png`, `scaling.png`, `energy.png` |
- **Hand-written:** all `report.html` (inline `<style>`, inline SVG). **Generated:** every PNG — made in microarch by `03_tools/plot_web_figs.py` / `plot_results.py`, copied by `03_tools/sync_site_figs.py` (mapping table at lines 21-42; `phase6_ablation.png` is really `phase12_ablation.png`, "name kept for links"). Not in that map: `vendor_compare.png` (byte-identical to `microarch/06_figures/fig_vendor_compare.png`, from `make_vendor_fig.py:128`; copied by hand — inferred) and the orphan above. `sync_site_figs.py --check` today: `0 file(s) stale`.
- **h2 sections** (each page also has unnumbered "Overview" first and "Series & sources" last):
  - I: 1 End-to-end pipeline · 2 Flow matching & the denoising loop · 3 Suffix embedding · 4 Inside one Action-Expert layer · 5 Every module: shapes, FLOPs, bytes, arithmetic intensity · 6 The two-phase signature · 7 Measured execution breakdown, from the papers
  - II: 1 The platform landscape (2025–26) · 2 LPDDR is the deployment reality · 3 The XPU baseline ladder ("floor", "optimistic 2×") · 4 The Action-Expert ladder on each platform · 5 The deployment-baseline matrix · 6 The three anchor baselines · 7 Beyond NVIDIA
  - III: 1 LPDDR5 from the outside · 2 Inside the die · 3 Operating LPDDR5 · 4 From DRAM to PIM · 5 LPDDR5-AiM: the machine · 6 The ISR instruction set · 7 The simulator · 8 What to offload, and why · 9 Instruction-level mapping · 10 Stock AiM GEMV, cycle by cycle · 11 The problem, quantified · 12 Results, and the root cause
  - III-2: 1 Samsung's PIM: the machine · 2 The ISA, and the one rule that matters · 3 The simulator, retimed to LPDDR5 · 4 How a GEMV runs · 5 The problem, quantified · 6 Why the problem is smaller here · 7 What the fix is worth, and the Samsung-specific ceiling
  - IV: 1 Eight problems · 2 CoRe (column reuse; formerly "P1") — MAC_ABK_MV · 3 P4 — LOOP n … ENDLOOP (+P3, P7, P8) · 4 Validation · 5 Ablation · 6 The last bottleneck: activation broadcast · 7 System view · 8 Energy, and a fair baseline · 9 How this differs from prior in-DRAM designs
## 3. Build, test, run
No build. Checks (all read-only; run before every commit):
```bash
# (a) well-formedness + duplicate ids, all five pages
python3 - <<'EOF'
import glob
from html.parser import HTMLParser
VOID=set("meta link br img input hr line rect path circle stop col polygon polyline ellipse use".split())
class P(HTMLParser):
    def __init__(s): super().__init__(); s.st=[]; s.err=[]; s.ids=[]
    def handle_starttag(s,t,a):
        s.ids+=[v for k,v in a if k=='id']; t in VOID or s.st.append((t,s.getpos()[0]))
    def handle_startendtag(s,t,a): s.ids+=[v for k,v in a if k=='id']
    def handle_endtag(s,t):
        if t not in VOID: s.st.pop() if s.st and s.st[-1][0]==t else s.err.append((t,s.getpos()[0]))
for f in sorted(glob.glob('/home/yanggon/versel_distribute/08_VLA/*/report.html')):
    p=P(); p.feed(open(f,encoding='utf-8').read()); print(f.split('/')[-2],'mismatch',p.err,'unclosed',p.st,'dup-ids',sorted({i for i in p.ids if p.ids.count(i)>1}))
EOF
# (b) render every inline SVG of one page to PNG (look for label collisions); OUT = a scratch dir outside the repo
/home/yanggon/05_VLA_LPDDR/microarch/.venv/bin/python - PAGE.html OUT <<'EOF'
import re,sys,os,html,cairosvg
src=open(sys.argv[1],encoding='utf-8').read(); os.makedirs(sys.argv[2],exist_ok=True)
for i,m in enumerate(re.finditer(r'<svg.*?</svg>',src,re.S)):
    s=m.group(0)
    if 'xmlns=' not in s[:300]: s=s.replace('<svg','<svg xmlns="http://www.w3.org/2000/svg"',1)
    s=re.sub(r'&(?!amp;|lt;|gt;|quot;|#)\w+;',lambda e:html.unescape(e.group(0)),s)   # &mdash; etc. are not XML
    s=re.sub(r'var\(--[\w-]+\)','#172033',s)
    cairosvg.svg2png(bytestring=s.encode(),write_to=f'{sys.argv[2]}/svg{i:02d}.png',output_width=1800,background_color='white'); print(i,'line',src.count('\n',0,m.start())+1)
EOF
# (c) preview:  cd /home/yanggon/versel_distribute && python3 -m http.server 8000   → http://localhost:8000/08_VLA/…
# (d) git -C /home/yanggon/versel_distribute diff --check
```
**Publish:** commit + `git push origin main` → Vercel redeploys (`CLAUDE.md` §Conventions, `README.md` "Editing Rules"). **Auditor hand-off after every push** (microarch-owner's checkout; ask main/microarch-owner, or if permitted): `git -C /home/yanggon/05_VLA_LPDDR/microarch/03_tools/versel_distribute pull` then `cd /home/yanggon/05_VLA_LPDDR/microarch && .venv/bin/python 03_tools/verify_claims.py` → must end `0 FAIL(s)`. The auditor reads the *checkout*, not this working tree, so it cannot pre-validate uncommitted edits unless pointed elsewhere (variable `V`, `verify_claims.py:10`).
## 4. Git
- Repo `/home/yanggon/versel_distribute`, remote `origin git@github.com:yanggon-kim/versel_distribute.git`, branch `main` tracking `origin/main`. No `.gitignore`, no `vercel.json`. `ONBOARDING.md` / `HANDOFF.md` (and their `.history.md`) are tracked.
- **Writers:** all 219 commits are `yanggon-kim` / `Yang-gon Kim <yanggon@g.ucla.edu>` (`git log --format='%an <%ae>'`). This owner writes `08_VLA/**` plus the 08_VLA link block in `index.html:288-303`; the user's other projects write `00_DAE … 07_3dic` and their `index.html` boxes (`05_VLA_LPDDR/CLAUDE.md:25,37`). `microarch/03_tools/sync_site_figs.py` also **writes PNGs into `08_VLA/*/assets/`** from outside (default `--site ../../versel_distribute/08_VLA`). The repo's own `CLAUDE.md`/`AGENTS.md` contain no who-edits-what rule; the split comes from `05_VLA_LPDDR/CLAUDE.md`.
## 5. Existing guidance (read, do not restate)
- `CLAUDE.md` — site rules. Binding here: "Relative links only"; "Plain HTML/CSS only unless the user explicitly asks"; "Two-space indentation; lowercase filenames"; "Commits: short imperative summaries, one logical change each … Commit and push so Vercel republishes"; the **edit rule** ("apply the edit rule" → `git add` new/edited files and add `<a class="report-link">` to the matching `index.html` box; "Never add a link to `index.html` itself").
- `AGENTS.md` — pointer to `CLAUDE.md` only. `AGENTS.history.md` — archived former long form, not live. `README.md` — job description + structure list. **Its 08_VLA entries are stale** (`README.md:46-57`: old dirs `01_stock_aim_offload`, `02_extended_isa`, `03_deployment_platforms`, old part order, "9.77 ms", "loses 5.8x", no Part III-2).
- `/home/yanggon/05_VLA_LPDDR/CLAUDE.md:25,37,63` — owner registry row for site-owner ("after each change the claim auditor in microarch must report 0 FAIL"), and "Private vendor correspondence is never cited or named".
## 6. Conventions and traps
- **Naming (user, 2026-09-25):** the ISA mechanism formerly "P1" is **CoRe — Column Reuse** (one column access shared across the whole resident activation tile, one command; instruction `MAC_ABK_MV` keeps its mnemonic). "P1" survives only as the *problem* id in Part IV §1 (row label, "P1&ndash;P6") and in the ids `#p1`, `#p1-toy`, `#fig-frames-p1` (inbound anchors, keep). CoRe alone = 18.21 ms/step at D = 4; the 9.31 ms / 4.32× headline is the full design (CoRe + `LOOP` + SW) — never let "CoRe" carry full-design numbers. DOTS contrast line: "DOTS reuses the row; CoRe reuses each column access across the whole resident tile."
- **Confirmed in files:** page skeleton `header.page` + `nav.toc#toc` + `section.card#<id>` with `<h2><span class="num">N</span>…`; colour tokens `#172033 #647083 #1f6feb #d8dee8 #f1f4f9 #b54708 #1a7f37 #6f42c1` present in all pages (882 hits in Part III); classes `lead`, `callout [win|warn]`, `pre.cmd`, `code.k`, `ul.notes`, `.scroll`, `.kpi`/`.headline`; figures `<div class="fig" id="fig-…"><svg viewBox="0 0 900 H" role="img" aria-label=…>` + `<p class="cap">` (one exception: Part I `:219` uses `viewBox="0 0 760 260"`); footer "author : yang-gon kim · email : yanggon@g.ucla.edu" on every page. Assumption labels A0/A1/A2 occur only in Part III (e.g. `:828`, `:902`, `:931`); Part II uses `[ASSUMPTION]` (`:154`).
- **Inbound anchors — do not rename these ids:** II `#baselines` ← I:400, II:89/145 (self, via `../01_…` path), IV:928/1209/1217 · IV `#bcast` ← II:121, IV:638 · IV `#energy` ← II:169, III:1984 · IV `#system` ← II:181 · IV `#p1` ← III:1947 · IV `#prior` ← III-2:293 · III `#gbrate` ← IV:591 · III `#aim`, `#where60` ← in-page. All resolve today (checked by script).
- **Section numbers are cited as text across pages** and are *not* checked by anything: "Part II §3" (IV:928,1209; II:89), "Part III §3/§10/§11" (IV:691,591,668), "Part IV §2/§6/§7/§8" (III:931,1525,1620,1627,1762,1766; II:121,154,171,181). Renumbering a page silently breaks these and the TOC labels in `nav.toc`.
- **Auditor = exact substrings** after whitespace normalisation (`verify_claims.py:35-40`), including entities (`'making it 3.5&times; faster'`, `'shrinks it to 33&nbsp;ms'`). Rephrasing a sentence that carries a number, or swapping `&times;` for `×`, produces a FAIL. It covers Parts I, III, IV, II, III-2 (`p3b …` checks) and `paper/main.tex`. Its variable names `P2,P3,P4` map to III, IV, II and its check labels are historical (label "p2 5.6x" checks the string 'Loses 4.5&times;') — do not read them as part numbers.
- Figure numbering is historical, not sequential: Part III uses L1–L5, 0a, 0a-2, 0a-3, 0b, 1, 2, 6a–6c, 7a, 3, 4; Part IV uses 1b, 1c, 11a, 3a, 3b, 6a, 6b, 2, 3, 4. Every label referenced in Part III is defined. Cross-page figure references do not name the page (HANDOFF open issues).
- `energy.png` exists in three asset folders (II, III, IV) — same source `web_energy.png`; update through `sync_site_figs.py`, never one copy.
- The site carries **no PDFs** (the `pdf/` exports were deleted 2026-09-21; recipe in `ONBOARDING.history.md`). The `.pdf` hrefs on the pages are external datasheet/source links and stay. · HTML named entities inside inline SVG are fine in browsers but break XML tools — hence the unescape step in snippet (b).
## 7. Current state
Lives in `HANDOFF.md` (state) — survey-time findings moved to `ONBOARDING.history.md`.
## 8. Proposed owner scope
- **Owns:** `08_VLA/**` (pages, assets, `ONBOARDING.md`, `HANDOFF.md`) and the VLA section box of `index.html` (lines 288-303 only). **Excludes:** `00_DAE … 07_3dic`, the rest of `index.html`, `CLAUDE.md`, `AGENTS*.md` (and `README.md` except, with main's approval, its 08_VLA bullet list).
- **Reads outside root:** `/home/yanggon/05_VLA_LPDDR/microarch/{03_tools/verify_claims.py, 03_tools/sync_site_figs.py, 03_tools/plot_web_figs.py, 04_data, 05_reports, 06_figures}`, the venv python for cairosvg, and `05_VLA_LPDDR/CLAUDE.md`.
- **Shares the git repository with:** the user's other projects (sections 00–07) — commit only own paths (`git add 08_VLA index.html`, never `git add -A`), pull/rebase before push.
## 9. Standing decisions
- The site carries no PDFs; do not regenerate or commit exports unless asked (recipe: `ONBOARDING.history.md`).
- The main agent decided: site-owner **may itself** `git -C /home/yanggon/05_VLA_LPDDR/microarch/03_tools/versel_distribute pull` and run the auditor (`cd /home/yanggon/05_VLA_LPDDR/microarch && .venv/bin/python 03_tools/verify_claims.py`, expect `0 FAIL(s)`) after a push. That checkout is a mirror of this repository, so pulling it is not an edit of microarch. Changing `verify_claims.py` itself stays with microarch-owner ("for microarch-owner: …").
- site-owner **owns the 08_VLA block** of the repository-level `README.md` and its own section box in the root `index.html`; nothing else in those two files.
- Part III-2 is in the auditor (checks `p3b …`, added by microarch-owner).
