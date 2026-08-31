---
title: Settings Reference
summary: Every setting in the modern GnollHack ports (Android, iOS, macOS, Windows) with its values, default, platform limits and effect — General, Adventuring, Layout, Status Bar, Interface, Drawing, Format, Menu Appearance, Behavior, Bar Commands, Volume, Forum Posting, Server Posting, Replays, Overseer, System
---

## Scope

This article covers the **modern .NET MAUI ports: Android, iOS, macOS, and Windows**. Legacy and terminal builds (Linux, public servers, the old Windows GUI) have no Settings screen at all — everything there is configured through the options file instead.

**macOS runs the iOS build.** Macs with an M1 processor or later install the iOS app from the App Store; there is no separate Mac Catalyst version. A Mac therefore shows the **iOS** settings, not the Windows/desktop ones — see *Settings That Differ by Platform*. Intel Macs are not supported.

Settings are **app preferences**. They follow the app and the device, not the character, and are never stored in a save file — with the Group A exception noted under *Settings That Mirror Game Options*.

The per-setting detail below is verified against the .NET MAUI client source, so prefer this article over the wiki wherever the two disagree.

## Reaching Settings

- **Main Menu → Settings** — before starting or loading a game.
- **In-Game Menu → Settings** — mid-game, without ending the run.

## When a Change Takes Effect

| Timing | Which settings |
|---|---|
| **Immediately** | Graphics, layout, status bar, interface overlays, drawing, menu appearance, volume, and all display toggles — including mid-game |
| **At the start of the next game** | Any setting that mirrors a game option (see *Settings That Mirror Game Options*), plus Allow Ghost Levels, Tournament Mode, and Save File Tracking |
| **After restarting the app** | **Windowed Mode** and **Edge to Edge** |

Those two are the only settings that need a restart; the app shows a "Restart Required" popup for each. Do not assume other rendering or audio settings need one.

**Greyed out while a game is running.** Five settings cannot be changed mid-game — the app disables the control until you leave the game:

| Setting | Category | Why |
|---|---|---|
| Tournament Mode | General | Would change the rules of a run in progress |
| Allow Ghost Levels | Adventuring | Bones loading is decided when the game starts |
| Record Game | Replays | Starting or stopping mid-run would leave the replay incomplete |
| GZip Replay Compression | Replays | Would change format mid-recording |
| Save File Tracking | Server Posting | Anti-cheat measure; cannot be switched off mid-game |

To change any of these, save and exit to the Main Menu first.

## How the Settings Screen Is Organised

Settings is **one long scrolling page**, not a set of sub-pages. The 16 categories below are bold section headings within it, in exactly the order listed. "Settings → System" therefore means scrolling to the **System** heading, not opening a separate page.

**Built-in help:** tapping or clicking a setting's *name* (not its switch) opens a popup with a full description of what it does. On desktop, hovering the name also shows a one-line tooltip and changes the cursor to an info cursor. The app carries its own text for every setting, so this is the quickest answer to "what does this one do?" — tell players about it. The wiki's Settings page documents this too.

The wiki's Settings page groups the categories thematically (a "General Settings" group containing General, Format, and Menu Appearance, and so on). That grouping is a wiki device only; the app does not have it.

## Category Index

| # | Category | Covers |
|---|---|---|
| 1 | General | Rendering, resolution, scale, sound/dark mode, status icons, Tournament Mode |
| 2 | Adventuring | Starting pets, ghost levels |
| 3 | Layout | Command rows, map corner buttons, context buttons |
| 4 | Status Bar | Classic vs modern bar, which fields appear |
| 5 | Interface | Grid, HP bars, targeting, pets, orbs, messages, walk arrows |
| 6 | Drawing | Lighting, X-ray tint, wall ends, breathing animations |
| 7 | Format | Metric system, dice ranges, damage formula |
| 8 | Menu Appearance | Menu images, hotkey highlighting, equipment screen |
| 9 | Behavior | Wishes, click actions, auto-dig, mouse buttons, quick engrave |
| 10 | Bar Commands | Which commands sit in the command bar |
| 11 | Volume | Six audio channels |
| 12 | Forum Posting | Discord progress posting, diagnostics |
| 13 | Server Posting | GnollHack Account, scores, bones sharing, save tracking |
| 14 | Replays | Recording and cloud upload |
| 15 | Overseer | Spoiler policy, verbosity, game context, client data access, consent |
| 16 | System | Logging, sound banks, rendering internals, dumplogs, caches |

## 1. General

| Setting | Values | Default | What it does |
|---|---|---|---|
| GPU Acceleration | On / Off | On | Renders with the GPU; Off falls back to CPU rendering. Turning it **off** fixes crashes and graphics artifacts on some devices. |
| Graphics | Tiles / ASCII | Tiles | Shows the game in 2D tile graphics or as ASCII text. |
| Map FPS | Default / 20 / 30 / 40 / 60 / 72 / 80 FPS | Default | Caps the map refresh rate. Lower saves battery; higher is smoother. The device default is typically 60 FPS. |
| Screen Resolution | Several resolutions | Native | *(Windows only)* Rendering resolution of the game map. |
| Screen Scale | Percentage | 100% | Makes UI components larger or smaller than normal. |
| Windowed Mode | On / Off | Off | *(Desktop only)* Windowed instead of fullscreen. **Requires an app restart.** |
| Edge to Edge | On / Off | Off | *(Mobile only)* Expands the game into the screen's safe area (notches, cutouts). |
| Cursor Style | Green Block / Underline | Green Block | *(ASCII graphics only)* How the player character is marked. |
| Hide Navigation | On / Off | On | *(Android only)* Hides the OS navigation buttons. |
| Hide Status Bar | On / Off | On | *(iOS only)* Hides the OS status bar. |
| Show Battery | On / Off | Off | Battery-level icon in the status bar. |
| Show FPS | On / Off | Off | Current refresh rate in the status bar. |
| Show Zoom | On / Off | Off | Current map zoom level in the status bar. |
| Silent Mode | On / Off | Off | Plays no sounds or music. |
| Dark Mode | On / Off | Off | Off: light menu/text backgrounds with black text. On: dark backgrounds with white text. |
| Tournament Mode | On / Off | Off | Forces the settings tournaments require and forces Casual-Classic Mode. See *Settings Forced by Tournament Mode*. |

## 2. Adventuring

| Setting | Values | Default | What it does |
|---|---|---|---|
| Starting and Gifted Pets | On / Off | On | Whether you start with a pet and receive gifted pets. Turn **off** for a petless conduct. Mirrors the `pets_not_gifted` option, inverted. |
| Allow Ghost Levels | On / Off | On | Whether the game loads bones files — levels left behind by dead characters. Mirrors the `bones` option. |

## 3. Layout

| Setting | Values | Default | What it does |
|---|---|---|---|
| Simple Command Layout | On / Off | Off (Desktop) / On (Mobile) | Off: two rows of command buttons plus a full More Commands list. On: one row and only the most important extra commands. |
| Alternative Zoom Button | On / Off | Off | Shows the alternative zoom toggle in the map's top-right corner. |
| Travel Mode Button | On / Off | Off | Shows the Travel Mode toggle in the map's top-right corner. |
| Auto-Dig Button | On / Off | Off | Shows the Auto-Dig toggle in the map's top-right corner. |
| Ignore Stopping Button | On / Off | Off | Shows the Ignore Stopping toggle in the map's top-right corner. |
| Desktop Buttons | On / Off | On (Desktop) / Off (Mobile) | Shows Stats and Equipment buttons beside the command buttons. When off, tap the top-left and top-right screen corners instead. |
| Skill Context Button | On / Off | On | Shows the skill context button on the left side of the screen. |
| Polearm Context Button | On / Off | Off | Shows the polearm context button on the left side of the screen. |
| Single Commands Page | On / Off | On (Desktop) / Off (Mobile) | One large More Commands page instead of several categorised pages. |

## 4. Status Bar

| Setting | Values | Default | What it does |
|---|---|---|---|
| Classic Status Bar | On / Off | Off | Off: the modern graphical status bar. On: a NetHack-style text status bar. |
| Desktop Status Bar | On / Off | On (Desktop) / Off (Mobile) | Adds ability scores, alignment, and other extra fields, using the wider desktop screen. |
| Show Score | On / Off | On (Desktop) / Off (Mobile) | Shows the game score in the status bar. |
| Show XP | On / Off | On (Desktop) / Off (Mobile) | Shows experience points in the status bar. |
| Right-Aligned on 2nd Row | On / Off | Off | Moves score, XP, and gold to the second status bar row. |
| Show Status Screen | On / Off | Off | Toggles the status screen — the same as tapping the middle of the status bar. |

## 5. Interface

| Setting | Values | Default | What it does |
|---|---|---|---|
| Grid | On / Off | Off | Draws grid lines between tiles so tile positions are easier to read. |
| Grid Opacity | Default (100%) / 5%–100% | Default (100%) | Opacity of those grid lines. |
| Hit Point Bars | On / Off | Off | HP bars under the player, pets, and monsters. |
| Player Mark | On / Off | Off | Green targeting icon above the player character. |
| Targeting | On / Off | Off | Red targeting icon above hostile monsters. |
| Show Pets | On / Off | On | Pet icons below the status bar. |
| Pet Rows | 1–4 / Maximum | 2 | How many rows of pet icons are allowed. |
| Orbs | On / Off | On | Health and mana orbs in the top-left corner. |
| Show Max Hit Points | On / Off | Off | Shows maximum HP under current HP in the health orb. |
| Show Max Mana | On / Off | Off | Shows maximum mana under current mana in the mana orb. |
| Messages | 1–50 | 5 | How many messages are shown in the bottom-left corner. |
| Show All | On / Off | Off | Shows all messages — the same as tapping the message area. |
| Walk Arrows | On / Off | On | Shows walk arrows when Travel Mode is off. |
| Default Auto-Center | On / Off | On | Whether the in-game Auto-Center button starts enabled. |
| Show Keyboard Shortcuts | On / Off | On (Desktop) / Off (Mobile) | Shows keyboard shortcut indicators in menus and on buttons. |

## 6. Drawing

| Setting | Values | Default | What it does |
|---|---|---|---|
| Lighter Unlit Areas | On / Off | On | On: unlit areas are lighter. Off: darker. |
| Colored X-Ray Vision | On / Off | On | Tints tiles and creatures seen through X-ray vision with a semi-transparent blue overlay. |
| Draw Wall Ends | On / Off | On | Draws wall end graphics. Can be disabled to save processor time. |
| Breathing Animations | On / Off | On | Shows creatures' breathing animations. |

## 7. Format

| Setting | Values | Default | What it does |
|---|---|---|---|
| Metric System | On / Off | Off | On: kilograms, grams, tons. Off: pounds, ounces, hundredweights. Mirrors the `metric_system` option. |
| Show Dice as Ranges | On / Off | On | On: `2-12`. Off: traditional `2d6` notation. Mirrors the `show_dice_as_ranges` option. |
| Show Damage Formula | On / Off | Off | Shows the underlying dice formula (e.g. `1d6+2`) when examining an item. Mirrors the `show_damage_formula` option. |

## 8. Menu Appearance

| Setting | Values | Default | What it does |
|---|---|---|---|
| Menu Fade Effects | On / Off | On | *(Android only)* Fades menu and text page contents in and out. |
| Improved Menu Images | On / Off | On | On: bilinear interpolation, better quality. Off: nearest neighbour, faster. |
| Highlighted Menu Keys | On / Off | On (Desktop) / Off (Mobile) | On: hotkeys coloured black or white to match light/dark mode. Off: hotkeys greyed. |
| Show Equipment Icons | On / Off | On | Equipment slot icons in the inventory menu. |
| Equipment Flip Animation | On / Off | On | 3D flip animation when moving between inventory and equipment screens. |
| Worn Shows Equipment | On / Off | On | On: the worn-items command (`]`) opens the graphical equipment screen. Off: a plain text list. Mirrors the `worn_shows_equipment` option. |

## 9. Behavior

| Setting | Values | Default | What it does |
|---|---|---|---|
| Empty Wish is Nothing | On / Off | On | On: a blank wish grants nothing, preserving wishless conduct. Off: a blank wish grants a random item. |
| Character Click Action | On / Off | Off | Clicking your own character performs the action appropriate to the tile (descend stairs, rest). Mirrors the `self_click_action` option. |
| OK on Double Click | On / Off | On (Desktop) / Off (Mobile) | Double-clicking a menu item also presses OK. |
| Traditional Get Position | On / Off | Off | Select map locations by moving a tile cursor with arrows or the keyboard instead of clicking the map. |
| Auto-Dig | On / Off | On | Digs through rock or walls when you move into them while wielding a digging tool. Mirrors the `autodig` option. |
| Ignore Stopping | On / Off | Off | Travel does not stop for items, closed doors, or engravings. Mirrors the `ignore_stopping` option. |
| Right Mouse Button | A game command | By Role | Command bound to right-click. "By role" uses role-specific defaults. Mirrors the `right_click_command` option. |
| Middle Mouse Button | A game command | By Role | Command bound to middle-click. Mirrors the `middle_click_command` option. |
| Quick Engrave Text | Text | *(none)* | Default text for the quick engrave command — commonly "Elbereth". Mirrors the `engrave_quicktext` option. |
| Quick Engrave Style | Always ask / Always finger / Last item | Always ask | Which engraving tool the quick engrave command uses. Mirrors the `engrave_quickstyle` option. |

OK on Double Click and On Switching Apps (System) ship with different desktop and mobile defaults; the wiki's Settings page lists only the mobile value for each.

## 10. Bar Commands

This page has no on/off settings. It configures **which commands appear in the command bar** at the bottom of the game screen, letting a player put the commands they use most within one tap. It pairs with Layout → Simple Command Layout, which decides how many rows the bar has.

## 11. Volume

Six independent channels, scaled 0–100.

| Setting | Default | What it does |
|---|---|---|
| Master | 100 | Scales all sound and music. |
| Music | 50 | Music volume. |
| Ambient | 50 | Ambient sound volume. |
| Dialogue | 50 | Voice-over volume. |
| Effects | 50 | Sound effect volume. |
| Interface | 50 | UI sounds such as button clicks. |

Silent Mode (General) overrides all six. The channels also exist as the `sound_volume_*` game options, so a loaded save can carry its own volume levels.

## 12. Forum Posting

| Setting | Values | Default | What it does |
|---|---|---|---|
| Post Game Progress | On / Off | Off | Posts your journey's events to a Discord channel. |
| Webhook Link | URL | The player-log channel on the GnollHack Discord | Which Discord channel receives those posts. |
| Post Diagnostic Data | On / Off | Off | Posts anonymous diagnostics and crash logs to the developer server. |

## 13. Server Posting

| Setting | Values | Default | What it does |
|---|---|---|---|
| Account | URL | account.gnollhack.com | The GnollHack Server address, and the link used to register. |
| User Name | Text | *(none)* | Your GnollHack Server username. |
| Password | Text | *(none)* | Your GnollHack Server password. |
| Post Top Scores | On / Off | Off | Posts your score to the server when a game ends. |
| Share Bones Files | On / Off | Off | Uploads your bones files and lets you encounter other players' ghosts, if Allow Ghost Levels is on. |
| Use Blacklist | On / Off | Off | Whether the name list below is a blacklist (blocked) or a whitelist (allowed). |
| Whitelist / Blacklist | Comma-separated names | *(none)* | Which players' bones files are allowed or blocked. |
| Save File Tracking | On / Off | Off | *(Desktop only)* Lets the server track save files as an anti-cheat measure. **Cannot be switched off once a game has started.** |

## 14. Replays

| Setting | Values | Default | What it does |
|---|---|---|---|
| Record Game | On / Off | Off | Records a replay of your game. |
| Show Recording | On / Off | On | Red dot in the status bar while recording. |
| Auto-Upload to Cloud | On / Off | Off | Uploads the finished replay to Azure cloud storage. |
| Cloud Storage | URL / Edit | *(none)* | A custom Azure storage connection string to upload to. |

## 15. Overseer

Behaviour of the Gnoll Overseer AI assistant.

| Setting | Values | Default | What it does |
|---|---|---|---|
| Allow Spoilers | On / Off | Off | On: the Overseer freely discusses game mechanics, item identities, monster stats, and optimal strategies. Off: it avoids revealing information you have not discovered yet. |
| Verbose Responses | On / Off | Off | On: detailed explanations and longer responses. Off: concise, action-oriented answers. |
| Send Game Context | On / Off | On | On: opening the Overseer from the game menu automatically sends the current game snapshot and message history. Off: no such data is sent. |
| Client Data Access | On / Off | On | Lets the Overseer request extra data from your game client, such as the full message history. That data is sent to the AI provider. Turning this off also forces Game Actions off. |
| Game Actions | On / Off | Off | Would let the Overseer suggest and perform in-game actions, each requiring your confirmation. **Unavailable in this version** — the switch is greyed out. |
| Data Consent | Status + Revoke button | None | Not a toggle. Shows whether you have accepted the AI data-processing disclosure ("Accepted" or "None"). The **Revoke** button is enabled only once consent has been accepted; revoking makes the disclosure appear again the next time you open the Overseer. |

**Spoiler policy.** Allow Spoilers governs only the third tier of a three-tier policy. Core mechanics (damage formulas, AC, encumbrance, skill training, status effects, controls) are always explained. Specific item identities, monster abilities, and artifact powers are revealed only once the Overseer verifies you have already encountered them. Future dungeon branches, unencountered bosses, quest objectives, endgame content, and optimal meta-strategies are withheld unless Allow Spoilers is on.

**Not in these settings.** Choosing an AI model, providing your own API key (BYOK), and managing conversation history are done in the **web interface** at overseer.gnollhack.com, not in the in-game Settings screen.

The Overseer is free and fully opt-in: nothing is transmitted during ordinary offline play, only when a player opens the Overseer and sends a message. It can be opened from the In-Game Menu (with live game context), from the About menu (general knowledge only), or on the web.

## 16. System

| Setting | Values | Default | What it does |
|---|---|---|---|
| Developer Mode | On / Off | Off | Unlocks Wizard Mode, the Reset menu, the options file editor, and the debug settings below. |
| Debug Logging | On / Off | Off | Writes debug information to the app log. *(Needs Developer Mode.)* |
| Low-Level Logging | On / Off | Off | Extensive low-level logging; fills the app log quickly. *(Needs Developer Mode.)* |
| Screen Logging | On / Off | Off | Prints log messages directly on the game screen. |
| Debug Post Channel | On / Off | Off | Posts to an alternative channel instead of the Post Game Progress one. *(Needs Developer Mode.)* |
| Show Memory | On / Off | Off | Shows current managed memory usage on the game screen. |
| Frame Time Profiler | On / Off | Off | Gathers frame-time data, for investigating stuttering. *(Needs Developer Mode.)* |
| Low Disk Space Warning | On / Off | On | Warns below 5 GB free, to prevent save game corruption. |
| Load Sound Banks | On / Off | On | Off saves memory but removes all audio. A workaround for memory pressure on minimum-spec devices. |
| Streaming Banks to Memory | On / Off | Off | Reads sound banks into memory and streams from there. Uses more memory. |
| Streaming Banks to Disk | On / Off | Off | Copies sound banks to storage and streams from there. Uses more storage. |
| Longer Message History | On / Off | Off | 16,384 messages instead of 250, with a search bar. Switches itself off on restart or on new messages, for performance. |
| Hide Message History | On / Off | Off | Hides recent messages entirely — useful for clean screenshots. |
| Use Single Dumplog | On / Off | On | On: opens the format chosen below. Off: asks each time whether to open plain text or HTML. |
| Use HTML Dumplog | On / Off | On | With Use Single Dumplog on, chooses HTML (On) or plain text (Off). |
| GZip Replay Compression | On / Off | On | On: GZip. Off: Zip. |
| Platform Render Loop | On / Off | On | On: a platform render loop tied to the display refresh rate. Off: the UI framework's animation system. |
| Runtime GL Effects | On / Off | Off | *(Experimental)* Runtime GL shaders for advanced map effects. |
| GL Only on Map | On / Off | Off | On: GL rendering on the map only, CPU rendering elsewhere. Off: GL on map, menus, and More Commands. |
| Mipmapping on Map | On / Off | Off | Mipmapping in map rendering. Mostly obsolete. |
| Adjust Rectangles | On / Off | On | Adjusts tile rectangles to stop thin seams appearing between tiles. |
| Fix Filtering | On / Off | On (iOS) / Off (others) | Adjusts texture coordinates to prevent filtering artifacts on some devices. |
| Disable Windows Key | On / Off | Off | *(Windows only)* Stops the Windows key opening the Start menu mid-game. |
| Default Vi-Keys | On / Off | Off | Chooses the starting value of the `number_pad` option: On selects vi-keys for movement, Off selects number keys. Only sets the default — changing `number_pad` in game does not change this setting back. |
| On Switching Apps | Save Game / Checkpoint | Checkpoint (Desktop) / Save Game (Mobile) | **Save Game**: saves and returns to the main menu, closing menus. **Checkpoint**: keeps menus open and recovers to the checkpoint only if the app is killed. |
| Map GPU Cache | Number | Varies by device | Skia GPU cache size for the map. Large values can cause out-of-memory. |
| Menu GPU Cache | Number | Varies by device | Skia GPU cache size for menus and the More Commands page. |

## Settings That Differ by Platform

| Availability | Settings |
|---|---|
| Windows only | Screen Resolution, Disable Windows Key |
| Desktop only (Windows) | Windowed Mode, Save File Tracking |
| Mobile only (Android, iOS, macOS) | Edge to Edge |
| Android only | Hide Navigation, Menu Fade Effects |
| iOS only (iPhone, iPad, macOS) | Hide Status Bar |
| ASCII graphics only | Cursor Style |

Because a Mac runs the **iOS** build, it gets the iOS and mobile settings (Hide Status Bar, Edge to Edge) and does **not** get the Windows/desktop ones (Screen Resolution, Windowed Mode, Disable Windows Key, Save File Tracking). "Desktop" throughout this article means the Windows build, not "a computer".

Six settings ship with different defaults on desktop and mobile, tuned for each: Single Commands Page, OK on Double Click, On Switching Apps, Desktop Status Bar, Desktop Buttons, and Show Keyboard Shortcuts. Highlighted Menu Keys, Simple Command Layout, Show Score, and Show XP also split this way.

## Settings Forced by Tournament Mode

Tournament Mode exists to guarantee a level playing field and to approximate public Linux server play. While it is on:

| Forced | Detail |
|---|---|
| Game mode | Classic Mode only — permadeath, save files load once |
| Difficulty | Expert or higher |
| Account | A registered GnollHack Account with username and password entered |
| Forced **on** | Post Game Progress, Post Top Scores, Allow Ghost Levels, Share Bones Files, Save File Tracking, Record Game, Auto-Upload to Cloud |
| Disabled | All custom links and webhooks in Server Posting |

Games played this way are marked **Tournament** on the GnollHack Account server's recent games and top scores pages.

## Settings That Mirror Game Options

These settings are two views of one value. Changing the option in game with the `O` command updates the setting, so the change outlives the run. Changing the *setting* behaves differently depending on which group it is in and whether a game is running.

**Group A — stored in the save file.** During a game, changing the setting changes only the running game; it does **not** update the saved preference. Outside a game, it sets the default for future games.

| Setting | Option |
|---|---|
| Character Click Action | `self_click_action` |
| Metric System | `metric_system` |
| Starting and Gifted Pets | `pets_not_gifted` *(inverted)* |
| Auto-Dig | `autodig` |
| Ignore Stopping | `ignore_stopping` |
| Right Mouse Button | `right_click_command` |
| Middle Mouse Button | `middle_click_command` |

**Group B — not stored in the save file.** Changing the setting always updates the saved preference, and also updates the running game if there is one.

| Setting | Option |
|---|---|
| Show Dice as Ranges | `show_dice_as_ranges` |
| Show Damage Formula | `show_damage_formula` |
| Worn Shows Equipment | `worn_shows_equipment` |
| Quick Engrave Text | `engrave_quicktext` |
| Quick Engrave Style | `engrave_quickstyle` |
| Traditional Get Position | *(no options-file equivalent)* |

Default Vi-Keys only chooses the starting value of `number_pad` and is never updated back. Allow Ghost Levels maps to the `bones` option, which is read at game start only.

**Practical upshot.** If a player changes a Group A setting mid-game and expects it to stick for the next character, it will not — it went into the save file, not the preferences. Tell them to change it from the Main Menu instead, before starting a game.

## Settings Used to Fix Problems

| Symptom | Setting to change |
|---|---|
| Game crashes on launch or during play | General → GPU Acceleration **off** |
| Graphics artifacts or corrupted tiles | General → GPU Acceleration **off**; System → Fix Filtering **on** |
| Out of memory on a minimum-spec device (3 GB RAM) | System → Load Sound Banks **off** (removes audio); lower Map GPU Cache and Menu GPU Cache. Below 3 GB the device is unsupported |
| Battery draining quickly | General → Map FPS lowered to 30 |
| Thin lines visible between tiles | System → Adjust Rectangles **on** |
| Save game corruption risk | System → Low Disk Space Warning **on**; free up disk space |
| Slow map rendering | Drawing → Draw Wall Ends **off**; Drawing → Breathing Animations **off** |
| Message history sluggish | System → Longer Message History **off** |

> **See also:** get_knowledge_article("settings_and_options") for the options file, in-game options, and what persists in save files; get_knowledge_article("app_navigation") for reaching Settings; get_knowledge_article("game_controls") for commands and input; get_knowledge_article("troubleshooting") for crashes and performance; get_knowledge_article("server_account") for accounts and score posting; get_knowledge_article("developer_tools") for Developer and Wizard Mode; get_knowledge_article("replay_system") for recording and playback.
> **Wiki:** For screenshots and any setting added after this article was written, search the wiki for the **Settings**, **Desktop Features**, and **Tournament Mode** pages. For the Overseer's settings and spoiler policy in depth, see **Introduction to Gnoll Overseer** and **Advanced Guide to Gnoll Overseer** under Guides.
