---
name: server-paths-moved
description: Site root is /home/yanggon/versel_distribute/08_VLA and the workspace /home/yanggon/05_VLA_LPDDR — ONBOARDING.md still spells the old 0007_26summer prefix
metadata:
  type: project
---

Since the 2026-09-22 server move the absolute paths are `/home/yanggon/versel_distribute/08_VLA` (site) and
`/home/yanggon/05_VLA_LPDDR/microarch` (numbers, figures, auditor). `08_VLA/ONBOARDING.md` was written
before the move and still spells every path with the `0007_26summer/` prefix, including the copy-paste
check scripts in its §3.

**Why:** the repository moved on the server; the tracked ONBOARDING/HANDOFF travelled with it but the text
was not rewritten.

**How to apply:** read ONBOARDING paths with the new prefix and fix the prefix in any snippet copied from
it before running (the HTML well-formedness / duplicate-id script and the cairosvg render script).
