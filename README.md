# versel_distribute

This repository is connected to a Vercel project for web publication.

Live website: <https://versel-distribute.vercel.app/>

## Coding Agent Job Description

Maintain this repository as a simple static HTML website. The main role of the
coding agent is to add, organize, and link HTML pages so they are easy to browse
from the published site.

## Current Structure

- `index.html`: the main landing page and link index.
- `00_DAE/`: section directory for DAE-related pages.
- `00_DAE/00_kernel/report.html`: GPU kernel performance model report.
- `01_GPU_memory_access/`: section directory for GPU memory-access pages.
- `01_GPU_memory_access/00_cc/report.html`: interactive report on whether LLM
  weights and KV cache are accessed as contiguous tile streams (RTX 5080).
- `01_GPU_memory_access/00_cc/assets/`: figures for the stream report.
- `01_GPU_memory_access/01_cx/report.html`: experiment-driven report from live
  NVBit traces for GPT-2, GPT-OSS-20B, and Qwen2.5-1.5B, including methodology,
  target kernels, environment, results, and compression block-size
  recommendations.
- `02_HBM_MC/`: section directory for HBM memory-controller pages.
- `02_HBM_MC/00_cc/report.html`: an HBM3 memory-controller design explainer —
  Ramulator 2's behavioral controller model, its limitations, and a synthesizable
  SystemVerilog re-implementation that reproduces it bit-exactly (microarchitecture
  block diagram, 1:1 function→RTL mapping, side-by-side C++/SV pseudocode, timing,
  worked examples, and the bit-exact verification).
- `02_HBM_MC/01_cx/report.html`: a cited literature/industry survey of how real
  DDR/HBM memory controllers are implemented (Synopsys uMCTL2 & HBM3 controller,
  AMD/Xilinx AXI HBM IP, JEDEC HBM3, Ramulator 2), with confidence labels and how
  each fact maps onto the bit-exact controller in this project.

## Editing Rules

- Keep `index.html` as the central list of links to HTML files stored in
  subdirectories.
- Editing rule automation: when the user says `apply the edit rule`, inspect the
  repository for new files and edited files, then add those files into git. If a
  new or edited file is an HTML file in a subdirectory, add a relative link to it
  in the correct section box of `index.html`. If a new section box is necessary,
  add that section box in `index.html`. Do not add a link to `index.html`
  itself.
- When adding a new topic directory, add a visible section box for it in
  `index.html`.
- When adding a new HTML page inside a subdirectory, add a link to that page in
  the correct section of `index.html`.
- Use relative links so pages work correctly after publication on Vercel.
- Keep pages as basic static HTML and CSS unless the user asks for a different
  stack or build system.
- Commit and push completed changes to the repository so Vercel can publish the
  updated site.
