---
title: Using the Gnoll Overseer App
summary: Player guide to the Gnoll Overseer web app — chatting, managing conversations, choosing an AI model, every setting on the Settings page, and bringing your own API key to add your own models
---

## What the Overseer Is

The **Gnoll Overseer** is GnollHack's AI assistant. It answers questions about the game by looking things up in real sources — the GnollHack source code, the GnollHack Wiki, this knowledge base, the NetHack Wiki, monster and item data, and your own game logs — instead of guessing.

It runs as a web application at **overseer.gnollhack.com** and can be opened three ways:

| Where you open it from | What it gets |
|---|---|
| **In-Game Menu → Overseer** | Your live game context: the current snapshot and recent messages, if **Send Game Context** is on in the game's Overseer settings |
| **About → Overseer** | General knowledge only, no live game data |
| **A browser** at overseer.gnollhack.com | General knowledge only, no live game data |

The Overseer is free and fully opt-in. Nothing is transmitted during ordinary offline play — only when you open the Overseer and send a message. It requires an internet connection; without one it shows an "Overseer requires an internet connection" notice.

## Logging In

The Overseer uses your **GnollHack Account** — the same username and password you use at account.gnollhack.com and in the game's Server Posting settings. There is no separate Overseer account.

The login screen has **Forgot Password?** and **Don't have an account? Sign Up** links; both lead to the GnollHack Account site.

## 1. Using the Chat

The screen is split into a **sidebar** (your conversations) and the **chat area**. On narrow screens the sidebar is hidden behind the ☰ button in the top-left; on desktop you can drag its right edge to resize it.

### Sending a message

- Type in the **Ask the Overseer** box at the bottom.
- **Enter** sends the message. **Shift+Enter** inserts a line break.
- The paper-plane button also sends.
- While the Overseer is answering, a progress bar appears with a status line and a **■ Stop** button that aborts the request.
- Unsent text is saved as a draft, so switching conversations does not lose what you typed.

### Attachments

- The **+** button attaches files; you can also paste an image straight into the input box.
- **Up to 5 files per message.** Accepted types: `.html`, `.htm`, `.txt`, `.md`, `.png`, `.jpg`, `.jpeg`, `.webp`.
- Maximum file size is set by the server (15 MB by default).
- Images can be previewed in a dialog; any attachment can be downloaded again from the message it was sent with.
- Useful for sending a dump log, a screenshot of the map, or an exported log file.

### Reading a reply

Each message shows who wrote it (**You** or **Overseer**) and how long ago. Assistant messages additionally show, on the right:

- the **model** that produced the answer and its badges (thinking level, reasoning mode, service tier);
- the **time to first token** and the **total response time**.

Buttons on a message:

| Button | What it does |
|---|---|
| **Copy** | Copies the message text to the clipboard |
| **Report message** | Reports that message to the developer, after a confirmation dialog |

### Thinking and tool blocks

While working, the Overseer shows what it is doing — which tools it is calling and, on models that expose it, a summary of its reasoning. How much of this you see is controlled by **Show Thinking and Tool Use** in Settings. Tool blocks can be expanded, and each tool result has its own **Copy Result** button. If a subagent is running, it has a **■** button of its own to cancel just that subagent.

A tool call can also finish as **Partial** (the subagent ran out of budget) or **Canceled**.

### Conversations in the sidebar

| Control | What it does |
|---|---|
| **New Chat** | Starts an empty conversation |
| **Search chats...** | Filters conversations by title *and* by message content; Esc clears it |
| **✕** on a conversation | Moves it to Trash |
| **Pin** on a conversation | Pins it; pinned chats are protected from automatic deletion |
| **Load more** | Loads the next page of older conversations |
| **✏️** next to the chat title | Renames the conversation |

**Titles are generated automatically** from your first message, if Title Generation is enabled on the Models page. While one is being generated a second progress bar appears, with a **■** button to cancel it. You can always rename a chat yourself afterwards.

### Quotas, Trash, and retention

The bar at the bottom of the sidebar shows three counters. Clicking one is a shortcut to the matching bulk action.

| Counter | Default limit | Notes |
|---|---|---|
| **Active chats** | 50 | Click to move all active chats to Trash |
| **Pinned chats** | 5 | Click to unpin all; pinned chats are exempt from automatic deletion |
| **Trash** | — | Click to open the Trash dialog |

In the **Trash** dialog you can search deleted chats, **restore** one, **delete one permanently**, or **empty all trash**. Restoring is blocked while your active-chat quota is full — delete or permanently remove something first.

Retention on the server, with the default configuration:

- Chats in Trash are permanently deleted after **30 days**.
- Active chats that have been inactive for **90 days** are removed automatically. **Pinned chats are protected from this.**
- Stored tool-call results are pruned after **30 days**, which shortens very old conversations without deleting them.

### Opening the Overseer from the game

When the game hands you over to the Overseer, a **"Consulting the Overseer…"** screen appears while the game's context is delivered. If it does not arrive within 60 seconds the overlay is dismissed and you can carry on normally.

## 2. Selecting an AI Model

The model selector sits directly above the input box.

- If you have **more than one** model available, it is a dropdown, grouping entries under **Your Models** and **System Models**.
- If only one model is available, it is shown as plain text with no dropdown.

Each entry shows the display name plus badges: **thinking level**, **reasoning mode** (when it is not the standard one), the **provider**, and — when parallel execution is restricted for the key — **Sequential** or **On request**.

**How your choice is remembered.** The Overseer picks a model in this order:

1. The model you last used **in this conversation**;
2. otherwise the model you last used **anywhere**;
3. otherwise the **first model in your list** — your own models before system models.

Because the list order decides the fallback, dragging your preferred model to the top of the Models page makes it the default. You may switch models in the middle of a conversation; each reply permanently records which model wrote it.

**System models** are configured by the administrators. They may be available to everyone, to a group, or to a single user, and they use the server's API key — you do not need your own key to use them.

If the chat shows a **Settings Missing** box, you have no API key, no model, or neither; the button in the box takes you to the page that fixes it.

## 3. Settings and What They Do

Reach the Settings page from the link at the bottom of the sidebar. Changes save automatically — a **Saving… / Saved** indicator appears next to the heading, with a **Retry** button if a save fails.

### General

| Setting | Values | Default | What it does |
|---|---|---|---|
| **Spoiler-Free Mode** | On / Off | **On** | Limits hints so the Overseer does not spoil things you have not discovered. This is the web equivalent of the game's **Allow Spoilers** setting, inverted. |
| **Show Source Code References** | On / Off | Off | Lets the AI cite source file names and line numbers in its replies. Overridden by the game's Developer Mode. |
| **Show parallel-execution badge in the model selector** | On / Off | On | Shows the *Sequential* / *On request* badges in the model dropdowns. Only appears when the server has the feature enabled. |
| **Show Thinking and Tool Use** | Minimal / Blocks / Text / Blocks and text | **Minimal** | How much of the AI's background work you see. *Blocks* shows collapsible tool-call blocks, *Text* shows its running commentary, *Blocks and text* shows both. |

### AI Permissions

These are tiered by risk. Each tier is independent except where noted.

| Setting | Tier | Default | What it allows |
|---|---|---|---|
| **Enable Web Search** | 1 | On | Searching the public internet for outside information. Lowest risk. |
| **Enable Server Tools** | 2 | On | Overseer's own server-side tools — wiki search, knowledge base, source code lookup, monster and item stats. No access to your game client. |
| **Enable Subagent Use** | 2 | **Off** | Lets the coordinating AI delegate research and analysis to autonomous specialist subagents. Slower and more expensive, but better on hard questions. |
| **Enable Client Data Access** | 3 | On | Lets the AI read your live game state, inventory, and device logs. |
| **Enable Game Actions** | 4 | **Off** | Lets the AI execute commands in your game, such as movement and attacks. **Requires Tier 3** — the checkbox is disabled until Client Data Access is on, and turning Client Data Access off forces this off too. Highest risk. |

Turning off Server Tools does not make the Overseer faster or smarter; it only removes its ability to look things up, so answers fall back on the model's own memory and are more likely to be wrong.

### AI Performance Settings

Each of these offers a few preset choices plus **Custom…**; the allowed range is shown under the custom field. Leaving one unset uses the server default.

| Setting | Server default | Allowed range | What it does |
|---|---|---|---|
| **Max Result Length** | 10 000 characters | 1 000 – 100 000 | Maximum length of text the AI processes per tool result. Longer results are truncated. |
| **Max Calls Per Session** | 50 | 5 – 500 | Maximum number of interactions permitted in one chat session. |
| **Max Tool Iterations** | 15 | 3 – 50 | Maximum number of consecutive tool-calling rounds before the AI must stop and answer. |
| **Max Parallel Tool Calls** | 6 | 1 – 10 | How many tool calls may run at the same time within one turn. |
| **API Request Timeout** | 1 800 seconds | 5 – 3 600 | How long to wait for a reply before aborting the request. |

Raising the limits lets the Overseer dig deeper into hard questions, at the cost of time and — with your own API key — money. Lowering them makes it answer faster and more cheaply, but more shallowly.

> These are *your* ceilings. The server applies its own hard limits on top, so a setting can be capped in practice.

### Chat Data Management

Shows your **Active**, **Pinned**, and **Trash** counts, with three bulk actions: **Move All to Trash**, **Unpin All Chats**, and **Manage Trash** (the same Trash dialog as in the sidebar). Moving active chats to Trash optionally includes pinned ones, via a checkbox in the confirmation dialog.

### Version

Shows the Overseer version and a **Release Notes** button. A gold sparkle appears next to *Settings* in the sidebar, and next to this button, when there are release notes you have not read.

## 4. Bringing Your Own API Key and Adding Your Own Models

You can run the Overseer on your own AI provider account. This is optional — system-provided models work without a key — but it lets you choose exactly which model answers, and how hard it thinks.

**You pay the provider directly.** Overseer sends the requests using your key; whatever the provider charges for those requests appears on your own bill with that provider. GnollHack does not invoice for it and does not take a cut.

The order matters: **add the key first, then add models.** The model list for a provider is fetched live from that provider using your saved key.

### Step 1 — Add an API key

Open **API Keys** from the bottom of the sidebar. There is one card per supported provider: **OpenAI**, **Anthropic**, and **Google**. Each card shows **Key Saved** or **No Key**.

To add one, paste the key into the field and press **Save Key**. Keys are encrypted before being stored in the database, are never shown back to you, and can be removed with **Delete Key** (a confirmation dialog appears first).

The **i** button on each card explains where to get a key:

| Provider | Where to create a key |
|---|---|
| **OpenAI** | platform.openai.com/api-keys → *Create new secret key* |
| **Anthropic** | console.anthropic.com/settings/keys → *Create Key* |
| **Google** | aistudio.google.com/app/apikey → *Create API key* |

OpenAI and Anthropic accounts must be funded. A Google free-tier key works but is subject to rate limits.

### Step 2 — Set parallel execution for the key

Each key card has a **Parallel execution** dropdown that controls whether Overseer may run tool calls and subagents simultaneously on that key.

| Value | Meaning |
|---|---|
| **Allowed** (default) | No restriction |
| **On request** | A request to the model rather than a hard limit |
| **Sequential only** | One at a time — choose this for free or low-tier keys that hit rate limits |

The chosen mode appears as a badge in the model selector.

### Step 3 — Add models

Open **Models** from the bottom of the sidebar, then press **Add Model**.

1. **Provider** — pick one you have a key for. *(The provider cannot be changed later; delete the entry and add a new one instead.)*
2. **Models** — the list is fetched from the provider with your key and filtered to models Overseer supports. A **⭐** marks recommended models. The list can be sorted newest or oldest first, or A→Z. **Custom…** lets you type a model ID by hand.
   - "No models available or API key not configured" means the key for that provider is missing, invalid, or unfunded.
3. **Display Name** — *Model Name*, *Model ID*, or *Custom…*. A live preview shows the result.
4. **Model Properties**:

| Property | What it does |
|---|---|
| **Context Window** | Read-only, shown for reference — how much text the model can hold at once |
| **Thinking Level** | How much effort the model spends reasoning before answering. Only levels the model supports are offered; ⭐ marks the recommended one. Higher is slower and costs more. |
| **Reasoning Mode** | Standard or an extended mode, on providers that offer one |
| **Reasoning Summary** | How much of the model's reasoning is exposed in the reply |
| **Service Tier** | The provider's speed/price tier for the request. Provider-specific; leave at *None (Default)* unless you know you want another. |
| **Max Input Tokens / Max Output Tokens** | Optional caps, clamped to what the model actually supports |

Each has a **Custom…** option for values not in the list.

5. Press **Add Model**.

### Managing your model list

- **Drag** entries by the handle to reorder them. The order decides which model is used by default and how the dropdown is arranged.
- The **pencil** button edits an entry; the **trash** button removes it, with confirmation.
- **System-Provided Models** are listed separately with a *System Config* badge. You cannot edit or delete them, but you can drag them into your preferred order, and the ↻ button resets that order to the default.

### Title Generation

At the bottom of the Models page is a **Title Generation** switch. When on, the Overseer names each new chat from your first message. By default it uses the first available title-generation model, falling back to the first available chat model; you can instead pick a specific model from the dropdown. Turning it off leaves chats unnamed until you rename them yourself.

Pointing title generation at a small, cheap model is a good way to keep costs down while still getting named conversations.

## 5. The Sidebar Links

| Link | What it opens |
|---|---|
| **Settings** | The Settings page described above |
| **API Keys** | Your provider API keys |
| **Models** | Your model list and title generation |
| **Admin** | Administrator dashboard — only shown to administrators |
| **Debug Log** | Client-side diagnostic log — only shown when the server enables it for you |
| **Logout** | Logs out, after a confirmation dialog |

## Troubleshooting

| Symptom | Cause and fix |
|---|---|
| **Settings Missing** box in the chat | No API key and/or no model. Follow the button in the box. |
| "No models available or API key not configured" when adding a model | The provider key is missing or wrong, or the account is unfunded. Re-check it on the API Keys page. |
| Requests fail or are rate-limited on a free key | Set that key's **Parallel execution** to *Sequential only*, and lower **Max Parallel Tool Calls**. |
| The Overseer keeps saying it cannot look something up | **Enable Server Tools** is off, or the answer needs a tool tier you have disabled. |
| It will not tell you something about an item or monster | **Spoiler-Free Mode** is on. Turn it off for full answers. |
| It cannot see your game | You opened it from the About menu or a browser rather than the In-Game Menu, or **Send Game Context** / **Client Data Access** is off in the game's Overseer settings. |
| Answers stop mid-way | **Max Tool Iterations** or **Max Calls Per Session** was reached, or the reply hit **API Request Timeout**. Raise the relevant limit. |
| A conversation vanished | It was inactive for 90 days, or it went to Trash and the 30-day grace period expired. Pin conversations you want to keep. |
| "Overseer requires an internet connection" | The Overseer is online-only; there is no offline mode. |

> **See also:** get_knowledge_article("settings_reference") for the **Overseer** category in the game's own Settings screen — Allow Spoilers, Send Game Context, Client Data Access, and Data Consent.
> **See also:** get_knowledge_article("gnollhack_account_website") for the GnollHack Account site whose login the Overseer shares.
> **See also:** get_knowledge_article("app_navigation") for reaching the Overseer from the In-Game and About menus.
> **Wiki:** For screenshots and any feature added after this article was written, search the wiki for **Introduction to Gnoll Overseer** and **Advanced Guide to Gnoll Overseer** under Guides.
