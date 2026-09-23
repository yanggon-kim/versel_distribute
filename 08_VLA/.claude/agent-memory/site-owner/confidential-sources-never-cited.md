---
name: confidential-sources-never-cited
description: The SK hynix 12 GB LPDDR5 spec [S1] is stamped Confidential — cite the JEDEC text it embeds, never the document, even when a task names it
metadata:
  type: feedback
---

The primer's `[S1]` — SK hynix "496ball POP Specification, 12GB LPDDR5, H58GG6MK6GX037" Rev 1.1 (Oct 2020),
the source of almost every JEDEC number in
`microarch/00_doc/02_refs/lpddr5_primer/research_lpddr5_core.md` — is **stamped "SK hynix Confidential"**
although it is openly hosted (`research_lpddr5_interface.md:13`). It must not be named, linked or quoted
*as that document* on the site.

**Why:** standing user rule — private vendor correspondence is never cited and confidential-stamped
documents are never linked. It is also why Part III already attributes its 256-bit-transfer quote to
"a vendor package datasheet that reproduces the JESD209-5 text" and paraphrases the 12 GB package example.

**How to apply:** cite the **standard** instead — "JESD209-5 bank-architecture text (§2.2)" for the burst
structure ("…sixteen corresponding 16-bit wide, one half-WCK-clock-cycle data transfers at the I/O pins")
and its "Effective Burst Length (BL/n) Definition" table for the spacing (same bank group 4 tCK = 5 ns,
different bank group 2 tCK = 2.5 ns) — adding "read in a vendor package specification that embeds the JEDEC
text". This happened on 2026-09-23, when a task explicitly asked to prefer `[S1]` by name: report the
deviation rather than following it.
