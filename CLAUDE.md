# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A **static HTML site** published through Vercel at <https://versel-distribute.vercel.app/>. There is no package manager, build step, or framework — pages are hand-written HTML/CSS served as-is. The git repository root is this directory (`00_repo/`); a sibling `../01_temp/` holds scratch HTML that is *not* part of the published site.

## Commands

- `python3 -m http.server 8000` — serve locally from the repo root, then open `http://localhost:8000/` to check navigation and relative asset paths.
- `git status --short --branch` — see new/changed files.
- `git diff --check` — catch whitespace errors before committing.

No test framework. "Testing" means manually opening `index.html`, confirming every report link opens, and confirming report images render from their `assets/` paths.

## Architecture

`index.html` is the central **report archive / link index** — the only navigation surface. Everything else is a self-contained report page in a numbered section directory.

Layout convention:
- Top-level numbered dirs are **sections** (`00_DAE/`, `01_GPU_memory_access/`, `02_HBM_MC/`).
- Inside a section, numbered subdirs are individual **report areas** (e.g. `01_GPU_memory_access/00_cc/`, `.../01_cx/`), each typically holding a `report.html`.
- A report's images live in an `assets/` directory beside that report (e.g. `00_DAE/00_kernel/assets/`).

Each section in `index.html` is a `<section aria-labelledby="...">` "section box" containing a `<ul>` of `<a class="report-link" href="relative/path/report.html">` entries. All styling is in the single `<style>` block in `index.html`; report pages are independently styled.

## The edit rule (core workflow)

When the user says **"apply the edit rule"**:
1. Inspect the repo for new and edited files; `git add` them.
2. For each new/edited HTML file in a subdirectory, add a relative `<a class="report-link">` link to it in the matching section box of `index.html`.
3. If the file belongs to a new section/directory, add a new `<section>` box (mirror the existing box markup, including `style="margin-top: 22px;"` on boxes after the first).
4. Never add a link to `index.html` itself.

## Conventions

- Plain HTML/CSS only unless the user explicitly asks for another stack.
- **Relative links only** so pages work both locally and after Vercel publication.
- Two-space indentation; lowercase filenames with `-`/`_` (`report.html`, `dram_bw_utilization_vs_ncu.png`).
- Commits: short imperative summaries, one logical change each (e.g. `Apply edit rule for kernel report updates`). Commit and push so Vercel republishes.
