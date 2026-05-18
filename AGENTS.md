# Repository Guidelines

## Project Structure & Module Organization

This repository is a static HTML site published through Vercel at
`https://versel-distribute.vercel.app/`. The root `index.html` is the report
archive and should list links to report HTML files stored in subdirectories.
Project sections use numbered directories such as `00_DAE/`; nested report areas
use paths such as `00_DAE/00_kernel/`. Keep report-specific images in an
`assets/` directory beside the report, for example
`00_DAE/00_kernel/assets/`.

## Build, Test, and Development Commands

There is no package manager or build step. Useful commands:

- `python3 -m http.server 8000`: serve the site locally from the repo root.
- `git status --short --branch`: check changed and untracked files.
- `git diff --check`: catch whitespace problems before committing.

Open `http://localhost:8000/` after starting the server to review navigation and
relative asset paths.

## Coding Style & Naming Conventions

Use plain HTML and CSS unless the user requests another stack. Use two-space
indentation in hand-edited HTML/CSS. Prefer lowercase file names with hyphens or
underscores, such as `report.html` or `dram_bw_utilization_vs_ncu.png`. Use
relative links only, so pages work both locally and after Vercel publication.

## Testing Guidelines

No automated test framework is configured. Manually verify that `index.html`
loads, every report link opens, and all report images render. For HTML report
updates, check that the page still works from its subdirectory and that asset
paths such as `assets/example.png` are correct.

## Commit & Pull Request Guidelines

Recent commits use short, imperative summaries, for example
`Clarify edit rule automation` and `Apply edit rule for kernel report updates`.
Keep commits focused on one logical change. Pull requests should describe the
updated report or navigation change, mention affected paths, and include
screenshots when the visible page layout changes.

## Agent-Specific Instructions

When asked to `apply the edit rule`, inspect for new or edited files and add
them to git. If a new or edited file is a subdirectory HTML file, add it to the
appropriate section box in `index.html`; create a new section box only when the
directory represents a new section. Do not add a link to `index.html` itself.
