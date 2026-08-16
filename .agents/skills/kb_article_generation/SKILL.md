---
name: kb_article_generation
description: Instructions and guidelines for autonomously generating and formatting new knowledge base articles for the Overseer AI. Triggered when requested to "create a new knowledge base article", "write an article for Overseer", or similar for the overseer_knowledgebase project.
---

# Knowledge Base Article Generation

When tasked with creating or modifying a knowledge base article for the Overseer AI in the `overseer_knowledgebase` repository, you MUST follow these strict guidelines. 

The Overseer AI relies on these articles as its authoritative source of truth.

## 1. File Location
- **All** articles MUST be placed inside the `Content/` directory.
- You may place articles directly in `Content/` or inside logical subdirectories (e.g., `Content/guides/`, `Content/mechanics/`).
- Do NOT place articles at the root of the repository.

## 2. File Naming
- Filenames MUST use `snake_case.md`. 
- Example: `Content/weapon_enchantment.md`

## 3. YAML Frontmatter (Required)
Every article must begin with a YAML frontmatter block containing exactly two fields: `title` and `summary`.

- **`title`**: A concise, human-readable title (e.g., "Weapon Enchantment Guide"). This is displayed to the user when Overseer cites the article.
- **`summary`**: A single-line, highly descriptive summary (e.g., "Explains how to enchant weapons, scroll types, and safe enchantment limits"). This summary is critical: Overseer uses it to determine whether the article is relevant to the user's current question. Make it keyword-rich.

**Example Format:**
```markdown
---
title: Weapon Enchantment Guide
summary: Explains how to enchant weapons, scroll types, and safe enchantment limits
---

Content begins here...
```

## 4. Content Guidelines
- **Be Factual and Concise**: Avoid fluff. Overseer reads this to answer questions quickly.
- **Structure**: Use standard Markdown headings (`##`), bulleted lists, and bold text to organize information logically.
- **Code Blocks**: If showing syntax or commands, use properly fenced code blocks.

## 5. Global Rules Reminder
- **No Automatic Commits**: You must NEVER automatically `git commit` or `git push` the new article. 
- Leave the newly created or modified file untracked/modified in the workspace.
- Explicitly tell the user that the article is ready for them to review, commit, and push manually.
