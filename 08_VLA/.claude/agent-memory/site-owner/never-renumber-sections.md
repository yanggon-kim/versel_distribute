---
name: never-renumber-sections
description: Part III/IV section numbers are cited as plain text across pages and inside auditor strings — add unnumbered asides instead of renumbering
metadata:
  type: feedback
---

Never renumber an h2 section of a site page. Add new explanatory material as an **unnumbered aside**:
`<section class="card" id="…">` with a plain `<h2>` (no `<span class="num">`), an inline
`style="border-left:4px solid var(--accent);"` to mark it visually, a lead paragraph that says
"an aside, not a numbered section", and an italic TOC line without a number.

**Why:** "Part III §3 / §10 / §11" and "Part IV §2 / §6 / §7 / §8" are hard-coded prose in other pages,
nothing verifies them, and some of those sentences are carried by auditor strings in
`verify_claims.py` (microarch-owner's file). Renumbering silently breaks cross-page prose *and* forces a
change in a file this owner may not touch. The 2026-09-23 "Peek: our AiM P1 design" aside between Part III
§2 and §3 is the pattern to copy. See [[auditor-additive-text-safe]].

**How to apply:** if a task asks for "a new §N", push back and deliver an unnumbered aside unless the
requester explicitly accepts the ripple.
