---
name: auditor-additive-text-safe
description: The claim auditor matches positive substrings, so purely additive page text cannot FAIL; how to pre-validate a working-tree page before pushing
metadata:
  type: feedback
---

`microarch/03_tools/verify_claims.py` checks that each expected string is **present** in the page after
whitespace normalisation. So text that only *adds* sentences, tables or sections can never break a check;
only rewording or deleting an existing sentence can. Appending a sentence at the end of an existing
paragraph is also safe — every prior substring survives.

**Why:** the script builds its expected strings with f-strings from CSVs, and its own header rule says
impact analysis must *run* it, never grep it (grepping for a literal number finds nothing and leads to
adding a duplicate check beside a stale one). Rewording a sentence that carries a number therefore needs
microarch-owner to repoint the check, reported as "old → new".

**How to apply:** prefer additive text for every new explanatory material. Pre-validate before committing
by copying the script to the scratchpad and repointing only its `V` variable to the working tree, then
running it from cwd = `/home/yanggon/05_VLA_LPDDR/microarch` with `.venv/bin/python`:
`sed 's|^V = "03_tools/versel_distribute/08_VLA/"|V = "/home/yanggon/versel_distribute/08_VLA/"|' …`.
Never edit the real script. After a push, pull `microarch/03_tools/versel_distribute` and run the real one
(2026-09-23 baseline: 408 checks, 0 FAIL, 0 WAIT). See [[never-renumber-sections]].
