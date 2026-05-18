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

## Editing Rules

- Keep `index.html` as the central list of links to HTML files stored in
  subdirectories.
- Editing rule automation: when the user says `apply the edit rule`, inspect the
  repository for new directories and new HTML files. If a new directory needs a
  new section box in `index.html`, add that section box, then add relative links
  to the new HTML files in the correct section. Do not add a link to
  `index.html` itself.
- When adding a new topic directory, add a visible section box for it in
  `index.html`.
- When adding a new HTML page inside a subdirectory, add a link to that page in
  the correct section of `index.html`.
- Use relative links so pages work correctly after publication on Vercel.
- Keep pages as basic static HTML and CSS unless the user asks for a different
  stack or build system.
- Commit and push completed changes to the repository so Vercel can publish the
  updated site.
