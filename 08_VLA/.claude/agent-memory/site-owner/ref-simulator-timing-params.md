---
name: ref-simulator-timing-params
description: Where to verify a simulator timing name before putting it on a page — nCCDMAC and friends live in the aim_simulator LPDDR5 model on vla-aim-ext-d1
metadata:
  type: reference
---

Before naming a simulator parameter on a page, check it in microarch's simulator clone rather than trusting a
brief: `/home/yanggon/05_VLA_LPDDR/microarch/02_sim/aim_simulator`, branch `vla-aim-ext-d1`,
`src/dram/impl/LPDDR5.cpp`. `nCCDMAC` (around line 661) is an **optional** rank-level timing parameter applied
between `MAC16` / `EWMUL16` commands and defaulting to `nCCD` — which is what makes the page's claim accurate
that the 8-cycle (5 ns) spacing constrains only MAC-class columns while RD/WR, GB writes and register accesses
stay on `nCCD` (4 cycles, 2.5 ns). Confirmed independently by main, 2026-09-23.

Reading that clone is fine; editing anything under `microarch/` is microarch-owner's. See
[[auditor-additive-text-safe]].
