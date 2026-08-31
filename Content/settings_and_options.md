---
title: Settings, Options, and the Options File
summary: The three ways to configure GnollHack (app Settings, the defaults.gnh options file, and the in-game O command), which knobs live where, what is locked once a run starts, and what is stored in the save file
---

## Scope

This article describes the **modern .NET MAUI ports of GnollHack: Android, iOS, macOS, and Windows**. These are the versions distributed through the app stores and the GnollHack website, and they are what a player is using unless they say otherwise. If the platform is unknown, assume a modern port.

**macOS is supported by running the iOS build** on Macs with an M1 processor or later — there is no separate Mac Catalyst version. Everything in this article that applies to iOS applies to a Mac; "desktop" here means the Windows build. Intel Macs are not supported.

Legacy and terminal builds (Linux `~/.gnollhackrc`, public servers, the legacy Windows GUI with a `defaults.gnh` beside the executable) have **no Settings pages at all** — every knob is in the options file. Symbol and terminal options (`SYMBOLS`, `BOULDER`, `symset`, `term_cols`, curses/X11/Qt/Amiga/MSDOS options) matter only in those builds, or in a modern port switched to ASCII graphics. Do not mention them unless the player asks.

## The Three Configuration Surfaces

| Surface | Where it is stored | How the player reaches it | Applies |
|---|---|---|---|
| **App Settings** | App preferences, outside the game core | Main Menu → Settings, or In-Game Menu → Settings | Immediately for UI/audio; at next game start for gameplay values |
| **Options file** (`defaults.gnh`) | Text file in the game folder | Main Menu → **Options** (requires Developer Mode) | At the start of the next game |
| **In-game options** | Live game state | The `O` command (More Commands → Options) | Immediately, for the current game |

**Precedence at game start** (later wins):

```
built-in defaults  →  app Settings  →  options file  →  in-game O changes
```

Then, **when a save file is loaded, the save file's own stored values replace all of the above** for every option it contains (see Persistence).

Consequences worth stating to a player:

- The options file **overrides** a matching app Setting when a new game starts.
- The app never rewrites `defaults.gnh`. Changes made with `O` do not appear in the file.
- Most Settings are pure client settings with no options-file equivalent (graphics, layout, volume, posting, replays). A dozen are **mirrored** — see the mirror table below.

## 1. Available Settings

Settings are organised into these categories. Full per-setting tables with defaults live on the wiki page **Settings**.

| # | Category | Notable contents |
|---|---|---|
| 1 | **General** | GPU Acceleration, Graphics (Tiles/ASCII), Map FPS, Screen Scale, Silent Mode, Dark Mode, Tournament Mode, Show Battery/FPS/Zoom |
| 2 | **Adventuring** | Starting and Gifted Pets, Allow Ghost Levels (bones) |
| 3 | **Layout** | Simple Command Layout, Desktop Buttons, Single Commands Page, and the optional map corner buttons (Alternative Zoom, Travel Mode, Auto-Dig, Ignore Stopping), Skill/Polearm context buttons |
| 4 | **Status Bar** | Classic Status Bar, Desktop Status Bar, Show Score, Show XP, Right-Aligned on 2nd Row |
| 5 | **Interface** | Grid + Grid Opacity, Hit Point Bars, Player Mark, Targeting, Show Pets, Pet Rows, Orbs, Show Max HP/Mana, Messages count, Walk Arrows, Default Auto-Center, Show Keyboard Shortcuts |
| 6 | **Drawing** | Lighter Unlit Areas, Colored X-Ray Vision, Draw Wall Ends, Breathing Animations |
| 7 | **Format** | Metric System, Show Dice as Ranges, Show Damage Formula |
| 8 | **Menu Appearance** | Menu Fade Effects, Improved Menu Images, Highlighted Menu Keys, Show Equipment Icons, Equipment Flip Animation, Worn Shows Equipment |
| 9 | **Behavior** | Empty Wish is Nothing, Character Click Action, OK on Double Click, Traditional Get Position, Auto-Dig, Ignore Stopping, Right/Middle Mouse Button, Quick Engrave Text and Style |
| 10 | **Bar Commands** | Which commands appear in the command bar |
| 11 | **Volume** | Master, Music, Ambient, Dialogue, Effects, Interface |
| 12 | **Forum Posting** | Post Game Progress, Discord Webhook Link, Post Diagnostic Data |
| 13 | **Server Posting** | Account URL, User Name, Password, Post Top Scores, Share Bones Files, whitelist/blacklist, Save File Tracking |
| 14 | **Replays** | Record Game, Show Recording, Auto-Upload to Cloud, Cloud Storage |
| 15 | **Overseer** | Allow Spoilers, Verbose Responses, Send Game Context, Client Data Access, Game Actions *(unavailable in this version)*, Data Consent |
| 16 | **System** | Developer Mode, logging switches, dumplog format, sound-bank loading, Skia/GPU rendering switches, Default Vi-Keys, On Switching Apps, GPU cache sizes |

Platform-conditional settings:

| Only on | Settings |
|---|---|
| Windows / desktop | Screen Resolution, Windowed Mode, Disable Windows Key, Save File Tracking |
| Mobile | Edge to Edge |
| Android | Hide Navigation, Menu Fade Effects |
| iOS | Hide Status Bar |

## 2. How to Edit the Options File

On the modern ports the options file is `defaults.gnh` in the game's own folder, and it is edited **inside the app** — the player does not need a file manager.

1. Main Menu → **Settings** → **System** → turn **Developer Mode** on.
2. Return to the Main Menu. An **Options** button is now visible.
3. Tap **Options** to open the built-in text editor for `defaults.gnh`.
4. Edit and save.
5. **Start a new game** (or load a save) for the changes to be read. The file is parsed once, at game start; editing it mid-game does nothing to the running game.

Notes:

- Developer Mode also enables Wizard Mode and the extra logging settings. It is the only way to reach the options file on the modern ports.
- The app **never writes** to `defaults.gnh`. Options changed with the `O` command are not recorded there.
- On other platforms: Linux uses `~/.gnollhackrc`; public servers (Hardfought, server.gnollhack.com) use the server's web interface; legacy Windows GUI ports use a `defaults.gnh` next to the executable.

## 3. Options File Syntax

One directive per line. `#` starts a comment. A boolean is turned off by prefixing `!` or `no`.

```
# Booleans
OPTIONS=autopickup
OPTIONS=!autoopen
OPTIONS=nosparkle

# Values, and several on one line
OPTIONS=pickup_types:$?!/
OPTIONS=number_pad:1
OPTIONS=runmode:walk,pile_limit:3,sortloot:full

# Text values
OPTIONS=engrave_quicktext:Elbereth
OPTIONS=fruit:mango
```

Other directives, each with its own keyword:

```
MENUCOLOR=" cursed " = red
MENUCOLOR=" cursed .* (being worn)" = orange&underline
HILITE_STATUS=hitpoints/<33%/red&bold
MSGTYPE=hide "You see here a .*"
AUTOPICKUP_EXCEPTION=">*cursed*"
BINDINGS=x:d
BINDINGS=v:look
```

`SYMBOLS=` and `BOULDER=` only affect ASCII graphics mode. Details for all directives are on the wiki page **Additional Options**.

## 4. Options That Can Only Be Set in the Options File

These cannot be changed with `O` in game and have no Settings equivalent except where noted.

| Option | Effect | Settings equivalent |
|---|---|---|
| `bones` | Allow loading bones files (dead players' ghost levels) | Adventuring → Allow Ghost Levels |
| `herewindow` | Floating window listing objects on your tile | — |
| `dumplog` | Write a dumplog at game end (Android) | System → dumplog settings |
| `menu_deselect_all`, `menu_select_page`, `menu_search`, and the other `menu_*` entries | Rebind menu control keys | — |
| `autostatuslines`, `fullscreen`, `softkeyboard`, `use_darkgray` | Legacy/terminal display behaviour | — |
| `dungeon`, `effects`, `monsters`, `objects`, `traps` | ASCII symbol tables | — |

## 5. How to Set Options During a Game

Use the **`O` (options)** command. On the modern ports: **More Commands → Options** (or press `O` on a hardware keyboard). It works even while buried and does not consume a turn.

The menu has four blocks, in this order:

1. **Read-only booleans** — indented and not selectable. These record how the character was created (see section 7).
2. **Changeable booleans** — selecting one toggles it.
3. **Compounds** — selecting one prompts for a new value. `playmode`, `name`, `role`, `race`, `gender`, and `align` are listed first and are read-only.
4. **Other settings** — autopickup exceptions, menu colors, message types, status hilite rules. All editable in game.

Wizard-Mode-only options (`monpolycontrol`, `sanity_check`, `travel_debug`, `wiz_alwaysenc`, `wiz_mstatusline`, `wizweight`) appear **only** when the game is running in Wizard Mode.

Shortcut: the **`@` command** toggles `autopickup` on and off directly, without opening the options menu.

## 6. Options That Can Be Set During a Game

The **Saved** column answers "does this survive loading a save file?" — see section 9 for why.

### Autopickup and item handling

| Option | Effect | Saved |
|---|---|---|
| `autopickup` | Pick up items walked over | Yes |
| `pickup_types` | Which item classes autopickup takes (`$?!/` etc.) | Yes |
| `pickup_thrown` | Pick up thrown weapons and ammunition | Yes |
| `pickup_burden` | Encumbrance level at which autopickup prompts | Yes |
| `stash_on_autopickup` | Stash picked-up items into an active container | Yes |
| `knapsack_prompt` | Prompt for an action when the pack is full | Yes |
| `pile_limit` | Item count that triggers "there are many objects here" | Yes |
| autopickup exceptions | Per-pattern include/exclude rules ("Other settings") | No |

### Movement and travel

| Option | Effect | Saved |
|---|---|---|
| `travel` | Pathfinding travel by clicking a distant tile | Yes |
| `runmode` | Map redraw frequency while running/travelling | Yes |
| `run_spot_distance` | Distance at which spotting a monster stops travel | No |
| `ignore_stopping` | Do not stop travel for items, doors, engravings | Yes |
| `autoopen` | Walking into a closed door opens it | Yes |
| `autodig` | Walking into rock digs, with a digging tool wielded | Yes |
| `autounlock` | Walking into a locked door/box attempts to unlock it | Yes |
| `autokick` | Walking into a door attempts to kick it (Android) | Yes |
| `displace_peaceful` | Swap places with peacefuls and pets | Yes |
| `prefer_fast_move` | Movement keys run by default instead of walk | Yes |
| `rest_on_space` | Space bar waits one turn | Yes |
| `move_interval`, `crawl_interval` | Walk / crawl animation delay in milliseconds | Yes |

### Combat

| Option | Effect | Saved |
|---|---|---|
| `autoquiver` | Fill an empty quiver automatically when firing | Yes |
| `autoswap_launchers` | Swap to a launcher for ranged, back for melee | No |
| `autoswap_polearms` | Swap off a polearm when a monster gets adjacent | No |
| `multishot_always_fire` | Always fire the maximum number of projectiles | Yes |
| `swap_rhand_only` | Weapon swap leaves the off-hand alone | Yes |
| `pushweapon` | Previous weapon moves to the secondary slot | Yes |
| `confirm` | Ask before attacking peacefuls and pets | Yes |
| `safe_pet` | Prevent attacking your own pets | Yes |
| `search_box_traps` | Search checks adjacent boxes for traps first | Yes |

### Map and display

| Option | Effect | Saved |
|---|---|---|
| `dark_room` | Explored-but-unseen floor drawn darker | Yes |
| `lit_corridor` | Dark corridors drawn as lit once in view | Yes |
| `show_grid` | Grid lines between tiles | Yes |
| `show_tile_u_hp_bar`, `show_tile_pet_hp_bar`, `show_tile_mon_hp_bar` | HP bars under player / pets / monsters | Yes |
| `show_buff_timer` | Buff timers on tiles | Yes |
| `hitpointbar` | Coloured HP bar behind the status HP text | No |
| `sparkle` | Sparkle animation when magic resistance blocks a spell | Yes |
| `hilite_pile` | Highlight tiles holding item piles | No |
| `showrace` | Draw your character by race instead of role | Yes |
| `baseacasbonus` | Show AC as an ascending bonus rather than descending | Yes |
| `animation_interval`, `shield_effect_length`, `talk_effect_length`, `last_item_show_duration` | Animation frame timing and effect durations | Yes |

### Status bar

| Option | Effect | Saved |
|---|---|---|
| `showscore`, `showexp`, `showmove`, `showrealtime`, `time` | Show score / XP / speed / clock / turn count | Yes |
| `fullstatuslineorder` | Use the full status line field order | Yes |
| `show_weapon_style` | Show the wielded weapon type | Yes |
| `partydetails`, `partylinecolor`, `partymultiline` | Pet statistics detail, colour, and line layout | Yes |
| `statushilites` | Turn count for status highlighting | No |
| status hilite rules | Per-field highlight rules ("Other settings") | No |

### Inventory and menus

| Option | Effect | Saved |
|---|---|---|
| `sortpack`, `packorder` | Group inventory by type; class ordering | Yes |
| `sortloot` | Sorting of inventory and loot lists | Yes |
| `fixinv` | Items keep their inventory letters | Yes |
| `implicit_uncursed` | Omit the "uncursed" label | No |
| `inventory_weights_last`, `show_weight_summary`, `detailed_weights` | Weight placement, total-weight line, finer units | Yes |
| `metric_system` | Kilograms/grams instead of pounds/ounces | Yes |
| `show_comparison_stats` | AC/damage comparison against equipped gear | No |
| `show_dice_as_ranges`, `show_damage_formula` | `2-12` instead of `2d6`; show the damage formula | No |
| `goldX` | Classify gold as uncursed/unknown | No |
| `long_charge_text` | Verbose charge and recharge text | Yes |
| `lootabc` | `a/b/c` loot menu keys instead of mnemonics | Yes |
| `takeoff_uses_all` | Take-off removes all armor sequentially | No |
| `worn_shows_equipment` | `]` opens the graphical equipment screen | No |
| `force_invmenu`, `inventory_obj_cmd` | Item-selection menus; action menu on item select | Mixed (`force_invmenu` No, `inventory_obj_cmd` Yes) |
| `skill_table_format`, `spell_table_format` | Table layout for skill and spell menus | No |
| `menucolors`, `menu_objsyms` | Use menu colours; show object symbols in menus | No |
| menu colors | Per-pattern menu colour rules ("Other settings") | No |
| `spellorder` | Spell list sorting | Yes |
| `perm_invent` | Persistent inventory window | No |

### Input and clicking

| Option | Effect | Saved |
|---|---|---|
| `autodescribe` | Describe terrain under cursor automatically | No |
| `clickfire`, `clicklook`, `clickpole` | Fire / look / use polearm by clicking a tile | No |
| `self_click_action` | Clicking your own character performs a local action | Yes |
| `right_click_command`, `middle_click_command` | Command bound to right / middle mouse button | Yes |
| `number_pad` | Numpad movement mode, or vi-keys | No |
| `cmdassist` | Help text on invalid direction input | No |
| `herecmd_menu` | Popup menu of actions for the current tile | No |
| `whatis_menu`, `whatis_moveskip`, `whatis_filter`, `whatis_coord` | Location-targeting menu, cursor skipping, filtering, coordinates | No |
| `engrave_quicktext`, `engrave_quickstyle` | Default quick-engrave text and stylus choice | No |

### Sound

| Option | Effect | Saved |
|---|---|---|
| `sound_volume_general`, `sound_volume_music`, `sound_volume_ambient`, `sound_volume_dialogue`, `sound_volume_effects`, `sound_volume_ui` | The six volume levels, matching Settings → Volume | Yes |
| `acoustics` | Your character can hear in-game sounds | Yes |

### Messages, prompts, and end of game

| Option | Effect | Saved |
|---|---|---|
| `verbose` | Longer, more descriptive messages | Yes |
| `tellexp` | Report experience gained | Yes |
| `mention_walls` | Message when walking into a wall | No |
| `exchange_prompt` | Confirm when equipping requires removing gear | Yes |
| `paranoid_confirmation` | Which actions require typing "yes" in full | Yes |
| `help` | Full lore text on `whatis` lookups | Yes |
| `force_hint` | Show hints regardless of other settings | Yes |
| `tombstone` | Graphical tombstone at game over | Yes |
| `disclose` | What is revealed at game over | Yes |
| `scores` | Which part of the score list is shown | Yes |
| `suppress_alert` | Suppress version-specific feature alerts | Yes |
| `pets_not_gifted` | Receive no gifted pets (petless conduct) | Yes |
| `checkpoint` | Save state on each level change | Yes |
| message types | Per-pattern message hiding rules ("Other settings") | No |

## 7. Options Shown In Game but Not Changeable

These appear in the `O` menu for reference only. They record decisions made before the game began.

| Option | What it records |
|---|---|
| `playmode` | Classic / Modern / Casual / Explore / Debug / Reloadable |
| `name`, `role`, `race`, `gender`, `align`, `female` | Character identity |
| `blind`, `nudist` | Conducts declared at character creation |
| `pettype` | Which species your starting pet is |
| `catname`, `catbreed`, `catgender`, `dogname`, `dogbreed`, `doggender`, `horsename`, `horsegender`, `ramname`, `ramgender`, `wolfname`, `wolfgender`, `tigername`, `tigergender`, `luggagename` | Starting companion names, breeds, genders |
| `max_hint_difficulty` | Difficulty ceiling for showing hints |
| `player_selection` | Dialog or prompts during character creation |
| `legacy` | Whether the intro message was shown |
| `selectsaved` | Whether saves are listed at launch |

To change any of these, edit them in the options file (or the matching Setting) and **start a new game**.

## 8. Settings That Mirror Options

For this set, the Setting and the option are two views of one value, and the link is **two-way**: changing the option with `O` during a game also updates the Setting, so the change persists after the game ends.

| Setting | Option | Note |
|---|---|---|
| Character Click Action | `self_click_action` | |
| Metric System | `metric_system` | |
| Show Dice as Ranges | `show_dice_as_ranges` | |
| Show Damage Formula | `show_damage_formula` | |
| Worn Shows Equipment | `worn_shows_equipment` | |
| Starting and Gifted Pets | `pets_not_gifted` | **Inverted** — Setting On means option `false` |
| Auto-Dig | `autodig` | Also toggled by the Auto-Dig map button |
| Ignore Stopping | `ignore_stopping` | Also toggled by the Ignore Stopping map button |
| Quick Engrave Text | `engrave_quicktext` | |
| Quick Engrave Style | `engrave_quickstyle` | |
| Right Mouse Button | `right_click_command` | |
| Middle Mouse Button | `middle_click_command` | |

Two Settings push a value **one way** into an option and are not updated back: **Traditional Get Position** (no options-file equivalent) and **Default Vi-Keys**, which only chooses the starting value of `number_pad`. Changing `number_pad` with `O` does not change the Setting.

**The direction matters for the seven saved ones.** Changing `self_click_action`, `metric_system`, `pets_not_gifted`, `autodig`, `ignore_stopping`, `right_click_command`, or `middle_click_command` **from the Settings page while a game is running** updates only the running game — it does not write the app preference, so it will not carry to the next character. Outside a game, the same Setting sets the default for future games. The five unsaved ones (`show_dice_as_ranges`, `show_damage_formula`, `worn_shows_equipment`, `engrave_quicktext`, `engrave_quickstyle`) always write the preference. Changes made with the in-game `O` command are pushed back to the Setting in both groups.

Every other option changed with `O` affects the current game only (plus the save file, if it is a saved option).

## 9. Persistence

| Surface | Survives app restart | Survives loading a save | Notes |
|---|---|---|---|
| App Settings | Yes | Yes (the Setting itself) | Applied at game start; a saved option's stored value then overrides it |
| Options file | Yes | Yes (the file itself) | Parsed at game start; a saved option's stored value then overrides it |
| In-game `O` change, saved option | Via the save file | Yes | Written into the save file, restored on load |
| In-game `O` change, unsaved option | No | No | Reverts to defaults → Settings → options file on the next launch |
| In-game `O` change, mirrored option | Yes (as a Setting) | Yes | Pushed back into the app Setting |

**Stored in the save file.** The game's core option block is written to the save file whole and read back whole. Any option marked **Saved: Yes** in section 6 is in that block. When a save is loaded, the stored value **wins over both the app Setting and the options file** for that launch. This is the single most common source of confusion: a player edits `defaults.gnh`, loads an existing save, and sees no change — because that option was restored from the save.

**Not stored in the save file.** Options marked **Saved: No** are rebuilt on every launch from defaults → app Settings → options file. They are also the ones that respond to an options-file edit immediately on the next load of an existing save.

**Not part of the game core at all** and therefore never in a save file: everything in the General, Layout, Status Bar, Interface, Drawing, Menu Appearance, Bar Commands, Forum Posting, Server Posting, Replays, Overseer, and System categories — graphics, layout, status bar arrangement, interface overlays, drawing, menu appearance, bar commands, posting, replays, Overseer, and system/diagnostic switches. These are app preferences and follow the app, not the character.

**Volume** is a special case: the six volume levels exist both as Settings sliders and as saved options, so a loaded save can carry its own volume levels.

## 10. Locked for the Whole Run

None of these can be changed once a character exists. They require starting a new game.

| Locked | Chosen at |
|---|---|
| Gameplay mode: Classic / Modern / Casual / Casual-Classic | Main Menu toggles, before starting |
| Wizard Mode | Main Menu switch (needs Developer Mode), before starting |
| Tournament Mode | Main Menu toggle, before starting; forces Casual-Classic |
| Difficulty level | Character creation |
| Role, race, gender, alignment, character name | Character creation |
| Starting pet species, name, breed, gender | Character creation / options file |
| Blind and nudist conducts | Options file, before starting |
| Allow Ghost Levels / `bones` | Settings or options file, before starting |
| Save File Tracking | Settings, before starting — it cannot be switched off mid-game |

Changing `pets_not_gifted` mid-game is allowed, but it only affects **future gifted** pets; it cannot remove the pet you already started with.

## 11. Quick Decision Rules

| Player wants to… | Answer |
|---|---|
| Change autopickup, travel, prompts, or display mid-game | Use `O` (More Commands → Options). For autopickup alone, `@`. |
| Change graphics, layout, volume, or status bar mid-game | In-Game Menu → Settings. No new game needed. |
| Change role, race, difficulty, or game mode | Not possible. Start a new game. |
| Reach the options file | Settings → System → Developer Mode, then Main Menu → Options. |
| Understand why an options-file edit did nothing | Either they did not start/load a game since editing, or the option is stored in the save file and was restored from it. Start a new game, or change it with `O`. |
| Understand why an `O` change vanished | The option is not stored in the save file and is not mirrored to a Setting. Put it in the options file to make it stick. |
| Make an `O` change permanent | Put the same option in `defaults.gnh` — or use the matching Setting if the option is in the mirror table. |

> **See also:** get_knowledge_article("settings_reference") for the settings category list; get_knowledge_article("game_controls") for commands and input; get_knowledge_article("game_modes") for modes and difficulty; get_knowledge_article("developer_tools") for Developer and Wizard Mode; get_knowledge_article("save_management") for save files.
> **Wiki:** For every setting and option with its default and full description, search the wiki for the **Settings**, **Options**, **Additional Options**, and **Accessing Options File** pages.
