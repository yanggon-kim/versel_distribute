# ONBOARDING — 08_VLA ("VLA × LPDDR-PIM" site section)
*Stable facts. Paths relative to `/home/yanggon/versel_distribute/` unless absolute. Current state: `HANDOFF.md`.*

## 1. Identity
- **Is:** the public, hand-written HTML write-up of the VLA-on-LPDDR5-AiM research, five pages (Parts I–IV + III-2),
  one section of the static Vercel site <https://versel-distribute.vercel.app/>.
- **Is not:** a place where numbers are produced. Every number comes from `/home/yanggon/05_VLA_LPDDR/microarch` (via
  `evaluation/p1/numbers.md`) and is string-audited by `microarch/03_tools/verify_claims.py`. No build system, no JS
  framework, no tests. Not the paper, not the other `00_`–`07_` sections.

## 2. Layout
| Dir | Part | inline SVG | `assets/` |
|---|---|---|---|
| `08_VLA/00_vla_algorithm` | I | 3 | `roofline.png`, `paper_breakdown.png` |
| `08_VLA/01_deployment_platforms` | II | 0 | `platforms.png`, `energy.png` |
| `08_VLA/02_stock_aim_offload` | III | 17 | `phase3_step_latency.png`, `phase3_layer_breakdown.png`, `energy.png`, `crossover.png`, `phase3_overhead_sensitivity.png` (orphan) |
| `08_VLA/02b_samsung_pim` | III-2 | 1 | `vendor_compare.png` |
| `08_VLA/03_extended_isa` | IV | 8 | `phase6_ablation.png`, `scaling.png`, `energy.png` |
- **Hand-written:** every `report.html` (inline `<style>`, inline SVG). **Generated:** every PNG — microarch's
  `03_tools/plot_web_figs.py` / `plot_results.py`, copied in by `03_tools/sync_site_figs.py` (its `MAP`;
  `phase6_ablation.png` is really `phase12_ablation.png`, name kept for links). `vendor_compare.png` is not in that MAP
  (copied by hand from `microarch/06_figures/fig_vendor_compare.png`). `energy.png` exists in three asset folders from one
  source (`web_energy.png`): update through `sync_site_figs.py`, never one copy.
- **h2 sections** (each page also has an unnumbered "Overview" first and "Series & sources" last):
  - I: 1 End-to-end pipeline · 2 Flow matching & the denoising loop · 3 Suffix embedding · 4 Inside one Action-Expert layer · 5 Every module: shapes, FLOPs, bytes, arithmetic intensity · 6 The two-phase signature · 7 Measured execution breakdown, from the papers
  - II: 1 The platform landscape (2025–26) · 2 LPDDR is the deployment reality · 3 The XPU baseline ladder · 4 The Action-Expert ladder on each platform · 5 The deployment-baseline matrix · 6 The three anchor baselines · 7 Beyond NVIDIA
  - III: 1 LPDDR5 from the outside · 2 Inside the die · (aside `#peek`) · 3 Operating LPDDR5 · 4 From DRAM to PIM · 5 LPDDR5-AiM: the machine · 6 The ISR instruction set · 7 The simulator · 8 What to offload, and why · 9 Instruction-level mapping · 10 Stock AiM GEMV, cycle by cycle · 11 The problem, quantified · 12 Results, and the root cause · 13 Questions & answers `#qa`
  - III-2: 1 Samsung's PIM: the machine · 2 The ISA, and the one rule that matters · 3 The simulator, retimed to LPDDR5 · 4 How a GEMV runs · 5 The problem, quantified · 6 Why the problem is smaller here · 7 What the fix is worth, and the Samsung-specific ceiling
  - IV: 1 Eight problems · 2 CoRe — MAC_ABK_MV · 3 P4 — LOOP n … ENDLOOP (+P3, P7, P8) · 4 Validation · 5 Ablation · 6 The last bottleneck: activation broadcast · 7 System view · 8 Energy, and a fair baseline · 9 How this differs from prior in-DRAM designs

## 3. Checks (read-only; run before every commit)
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
**Publish:** commit + `git push origin main` → Vercel redeploys. **After every push:**
`git -C /home/yanggon/05_VLA_LPDDR/microarch/03_tools/versel_distribute pull`, then
`cd /home/yanggon/05_VLA_LPDDR/microarch && .venv/bin/python 03_tools/verify_claims.py` → must end `0 FAIL(s)` (PARKED =
paper sections not yet migrated, not counted). The auditor reads the mirror, not this tree; to pre-validate uncommitted
edits, copy the script to the scratchpad with its `V = "03_tools/versel_distribute/08_VLA/"` line pointed at
`/home/yanggon/versel_distribute/08_VLA/` and run it with cwd = microarch. Never edit the real script.

## 4. Git and scope
- Repo `/home/yanggon/versel_distribute`, remote `origin git@github.com:yanggon-kim/versel_distribute.git`, branch `main`.
  No `.gitignore`, no `vercel.json`. Commit as `yanggon-kim <yanggon@g.ucla.edu>`.
- **Owns:** `08_VLA/**`, the 08_VLA box of the root `index.html` (the `08_VLA/…` report links) and the 08_VLA bullets of
  the root `README.md`. **Never:** `00_DAE … 07_3dic`, the rest of `index.html` / `README.md`, `CLAUDE.md`, `AGENTS*.md`.
  Stage by path (`git add 08_VLA index.html`), never `git add -A`; pull/rebase before push.
- `microarch/03_tools/sync_site_figs.py` writes PNGs into `08_VLA/*/assets/` from outside. Changing `verify_claims.py`
  is microarch-owner's ("for microarch-owner: …").
- Repo `CLAUDE.md` rules that bind here: relative links only; plain HTML/CSS unless the user asks; two-space indentation,
  lowercase filenames; short imperative commits, one logical change each; the **edit rule** (a new page gets
  `<a class="report-link">` in the matching `index.html` box; never link `index.html` itself).

## 5. Conventions and traps
- **Naming (user, 2026-09-25):** the mechanism formerly "P1" is **CoRe — Column Reuse** (`MAC_ABK_MV` keeps its
  mnemonic). "P1" survives only as the Part IV §1 *problem* id and in ids `#p1`, `#p1-toy`, `#fig-frames-p1`. Scopes never
  conflated: CoRe alone 18.21 ms · +CoRe rung (attention included) 12.29 ms · full design (CoRe + LOOP + SW) 9.31 ms.
- **Page skeleton:** `header.page` + `nav.toc#toc` + `section.card#<id>` with `<h2><span class="num">N</span>…`; colour
  tokens `#172033 #647083 #1f6feb #d8dee8 #f1f4f9 #b54708 #1a7f37 #6f42c1`; classes `lead`, `callout [win|warn]`,
  `pre.cmd`, `code.k`, `ul.notes`, `.scroll`, `.kpi`/`.headline`; figures `<div class="fig" id="fig-…"><svg viewBox="0 0
  900 H" role="img" aria-label=…>` + `<p class="cap">`; footer "author : yang-gon kim · email : yanggon@g.ucla.edu".
  A0/A1/A2 appear only in Part III; Part II uses `[ASSUMPTION]`.
- **Inbound anchors — never rename:** II `#baselines` · IV `#bcast`, `#energy`, `#system`, `#p1`, `#prior`, `#rate-d`,
  `#tradeoff` · III `#gbrate`, `#aim`, `#where60`, `#sim`, `#peek`, `#qa`.
- **Never renumber an h2.** "Part II §3", "Part III §3/§10/§11", "Part IV §2/§6/§7/§8" are cited as plain text across
  pages (nothing checks them) and some sit inside auditor strings. New material goes in an unnumbered aside
  (`<section class="card">`, plain `<h2>`, `border-left:4px solid var(--accent)`, italic TOC line), like `#peek`.
- **Auditor = exact substrings** after whitespace normalisation, entities included (`&times;` ≠ `×`). Additive text can
  never FAIL; rewording or deleting a number-bearing sentence can — list the exact new string + source for
  microarch-owner in `AUDITOR_STRINGS.md`. Its variable names `P2,P3,P4` = Parts III, IV, II and check labels are
  historical; do not read them as part numbers.
- Figure numbering is historical, not sequential (Part III: L1–L5, 0a…, 6a–6c, 7a, 3, 4; Part IV: 1b, 1c, 11a, 3a, 3b,
  6a, 6b, 2, 3, 4). Cross-page figure refs do not name the page.
- The site carries **no PDFs**; do not regenerate exports unless asked. `.pdf` hrefs on the pages are external links.
- HTML named entities inside inline SVG break XML tools — hence the unescape step in check (b).
