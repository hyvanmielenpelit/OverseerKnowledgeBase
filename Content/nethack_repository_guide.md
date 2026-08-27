---
title: NetHack 5.0 Repository Guide
summary: NetHack 5.0 repository structure, key file locations for monsters, objects, artifacts, and critical structural differences from GnollHack (which is based on NetHack 3.6.2)
---

## Repository Overview

NetHack 5.0.0 was released May 2, 2026. The repository is on branch `NetHack-5.0`.
GnollHack is derived from NetHack 3.6.2 and retains a similar directory structure, but NetHack 5.0 has diverged significantly in how game data is organized.

## Directory Structure

| Directory | Contents |
|:---|:---|
| `src/` | C source files — game logic, combat, spells, items, monsters, dungeon generation (~134 files) |
| `include/` | Header files — data structures, macros, constants, and **game data definitions** (see below) |
| `dat/` | Game data — level descriptions (`.des`), rumors, quest text, dungeon definitions |
| `doc/` | Documentation, release notes, guidebook |
| `util/` | Build utilities — makedefs, lev_comp, dgn_comp, dlb, recover |
| `win/` | Windowing interfaces — tty, curses, X11, Qt, win32 (NO .NET MAUI frontend) |
| `sys/` | Platform-specific code — Unix, Windows, macOS |
| `test/` | Test files |

## Key File Locations

### Game Data Definitions

**Critical difference from GnollHack**: NetHack 5.0 moved game data definitions from `.c` files into `.h` headers.

| Data | NetHack 5.0 Location | GnollHack Location |
|:---|:---|:---|
| Monster definitions | `include/monsters.h` (3,928 lines) | `src/monst.c` (inline, ~8000+ lines) |
| Object definitions | `include/objects.h` (1,660 lines) | `src/objects.c` (inline) |
| Artifact definitions | `include/artilist.h` (334 lines) | `include/artilist.h` (similar location) |

In NetHack 5.0, `src/monst.c` is a 90-line stub that `#include`s `monsters.h`, and `src/objects.c` is a 39-line stub that `#include`s `objects.h`.

### Core Game Mechanics (shared file names with GnollHack)

| File | Mechanics |
|:---|:---|
| `src/potion.c` | Potion effects |
| `src/read.c` | Scroll effects |
| `src/zap.c` | Wand and spell beam effects |
| `src/uhitm.c` | Player attacking monsters |
| `src/mhitu.c` | Monsters attacking player |
| `src/mhitm.c` | Monster-vs-monster combat |
| `src/mon.c` | Monster behavior and lifecycle |
| `src/mondata.c` | Monster data accessors and property checks |
| `src/makemon.c` | Monster creation and placement |
| `src/spell.c` | Spellcasting mechanics |
| `src/artifact.c` | Artifact properties and effects |
| `src/trap.c` | Trap mechanics |
| `src/pray.c` | Prayer mechanics |
| `src/eat.c` | Eating and nutrition |
| `src/weapon.c` | Weapon skills and damage |
| `src/shk.c` | Shopkeeper interactions |
| `include/monst.h` | `struct monst` (monster instance) |
| `include/obj.h` | `struct obj` (object instance) |
| `include/permonst.h` | `struct permonst` (monster template) |
| `include/objclass.h` | `struct objclass` (object template) |
| `include/mondata.h` | Monster property macros |
| `include/youprop.h` | Player property macros |

### Macro Differences

NetHack 5.0 uses a simpler `MON()` macro (14 arguments) with helper macros:
- `MON(nam, sym, lvl, gen, atk, siz, mr1, mr2, flg1, flg2, flg3, d, col, bn)`
- `NAM(name)` / `NAMS(namm, namf, namn)` — monster names
- `LVL(lvl, mov, ac, mr, aln)` — level, speed, AC, MR, alignment
- `SIZ(wt, nut, snd, siz)` — weight, nutrition, sounds, size
- `ATTK(at, ad, n, d)` / `A(a1, a2, a3, a4, a5, a6)` — attacks

GnollHack extends this with wrapper macros: `ANIMATED_MON()`, `ENLARGED_MON()`, `ENLARGED_ANIMATED_MON()` that add animation, soundset, and enlarged-size parameters.

NetHack 5.0 uses `OBJECT()` macro (15 args) for items. GnollHack uses the more familiar `WEAPON()`, `ARMOR()`, `FOOD()`, etc. shorthand macros.

## GnollHack-Only Additions (not in NetHack)

- `win/win32/xpl/` — .NET MAUI cross-platform graphical frontend
- FMOD audio system (sound effects, music, voiceovers)
- Animation and soundset systems
- Tile layer rendering system
- Item quality tiers (exceptional, elite, celestial, mythic, legendary)
- Runeword system
- 7 difficulty levels and 4 gameplay modes
- Expanded spell schools and mana system
