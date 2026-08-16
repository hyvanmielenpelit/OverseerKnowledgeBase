# Overseer Knowledge Base

This repository contains the curated first-party reference articles used by [Overseer](https://github.com/hyvanmielenpelit/MobileGnollHackLogger/tree/main/Overseer), the AI assistant for [GnollHack](https://github.com/hyvanmielenpelit/GnollHack). When a player asks Overseer a question about the GnollHack app, Overseer retrieves the relevant article from this knowledge base before consulting other sources such as the wiki or source code.

## How It Works

1. All knowledge base articles are Markdown files stored in the `Content/` directory.
2. The Overseer application reads the `Content/` directory (including subdirectories) every 10 minutes and loads any `.md` files it finds.
3. On the production server, a scheduled task runs `git pull` periodically to keep this repository up to date. New or updated articles are picked up automatically by the Overseer without requiring a restart.

## Article Format

Each article is a Markdown file with optional YAML frontmatter:

```markdown
---
title: Human-Readable Title
summary: One-line description shown in the topic list
---

Article content goes here.
```

- **`title`** — Displayed to the user when Overseer cites the article. Falls back to the filename if omitted.
- **`summary`** — Shown in the topic listing that Overseer includes in its system prompt, helping it decide which article to retrieve.
- **Content** — The body text that Overseer returns to the AI model when the article is requested.

## Repository Structure

```
overseer_knowledgebase/
├── Content/           # All knowledge base articles (*.md)
│   ├── article.md
│   └── subcategory/   # Subdirectories are supported
│       └── article.md
├── .agents/           # AI agent rules
├── .gitignore
└── README.md          # This file
```

Only files inside `Content/` are loaded by the Overseer. Everything else (`README.md`, `.gitignore`, `.agents/`, etc.) is safely ignored.

## Adding or Editing Articles

1. Create or edit a `.md` file inside the `Content/` directory.
2. Include `title` and `summary` in the YAML frontmatter.
3. Commit and push your changes. The production server will pull them automatically.

The topic key used by Overseer is derived from the file's path relative to `Content/`, without the `.md` extension. The path will always use forward slashes (`/`), even on Windows servers, to ensure consistency. For example:
- `Content/troubleshooting.md` → topic key `troubleshooting`
- `Content/guides/getting_started.md` → topic key `guides/getting_started`
