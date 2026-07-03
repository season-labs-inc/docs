# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Documentation site for the **Era SDK** (`@season/era-sdk`), built on [Mintlify](https://mintlify.com). Era is a "cognitive context" service: agents call `era.turnContext(messages)` each turn, get back a text block describing the user's intent/goal/emotion, and append it to the system prompt. There is no application code here — only MDX content and site configuration.

## Commands

```bash
npm i -g mint     # install the Mintlify CLI (one-time)
mint dev          # local preview at http://localhost:3000 (run from repo root, where docs.json lives)
mint update       # update the CLI if the dev server misbehaves
```

There is no build, lint, or test step. Publishing happens automatically on push to `main` via the Mintlify GitHub app.

## Structure

- `docs.json` — site config **and navigation**. Every new page must be added to the `navigation.pages` groups here or it won't appear in the sidebar.
- Pages are `.mdx` files with YAML frontmatter (`title`, `description`). Mintlify components (`<Steps>`, `<Card>`, `<CardGroup>`, `<Note>`) are available without imports.
- Content is organized as: `index.mdx` / `quickstart.mdx` (getting started), `when-to-use.mdx` + `use-cases/` (motivation, before/after examples), `concepts/` (async vs sync modes, fail-open, sessions), `sdk/` (API reference: Era class, types, helpers), `integrations/` (Vercel AI SDK).
- `drafts/` and `*.draft.mdx` are excluded from the published site (`.mintignore`).

## Writing style (from AGENTS.md)

- Active voice, second person ("you")
- Sentence case for headings
- Bold for UI elements; code formatting for file names, commands, paths, and code references
- One idea per sentence

## Content conventions

- Internal links use root-relative paths without extension: `/concepts/async-sync`, `/sdk/types#eraoptions`.
- Docs consistently emphasize two product behaviors — keep new content consistent with them: Era is **fail-open** (`turnContext()` returns `""` if unreachable or on the first async turn), and **async mode** (the default) returns the previous turn's block instantly while computing the current one in the background.
- Example `[STATE]`/`[GOAL]`/`[INTENT]`/`[CAUSAL]`/`[REC]` blocks appear across several pages; match their format when adding examples.
