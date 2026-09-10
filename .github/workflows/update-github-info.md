---
name: update-github-info
description: Read the latest GitHub news and changelog, then propose an update to Mona's GitHub Info page.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
tools:
  edit: true
  web-fetch:
  github:
    mode: local
    toolsets: [repos]
network:
  allowed:
    - github.blog
    - github.com
safe-outputs:
  create-pull-request:
    draft: true
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

## Task

Read `notes/mona-notes.md` to understand Mona and the intended content of the GitHub Info page.

Use the web-fetch tool to read both:

- [GitHub Blog latest](https://github.blog/latest/)
- [GitHub Changelog](https://github.blog/changelog/)

Use the edit tool to update only `site/content/github-info.md` with accurate, useful information supported by those sources and consistent with Mona's notes. Preserve the existing page structure and avoid inventing facts. When repository guidance or reference files from GitHub are needed, read them with the configured GitHub repository API tools rather than terminal, CLI, or sandboxed commands.

When there is a meaningful update, use the configured `create-pull-request` safe output to open a draft pull request for Mona to review. Describe the sources consulted and summarize the proposed content change in the pull request body. Do not write directly to `main`.

If the sources contain no meaningful update for the page, or if the evidence is insufficient, use `noop` with a short explanation instead of editing the file or opening a pull request.

## Safe Outputs

- Use only `create-pull-request` for the visible change.
- The pull request may modify only `site/content/github-info.md`.
- Use `noop` when no meaningful, evidence-supported update is needed.
