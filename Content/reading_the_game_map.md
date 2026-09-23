---
title: Reading the GnollHack Game Map
summary: How to read the ASCII map in a GnollHack snapshot — column ruler, row-number gutter and <x,y> coordinates, the map legend and its (3n,2e) offsets, telling the player where things are relative to the hero, blank cells, hero memory, and the complete monster, object, terrain and trap symbol tables
---

## 1. Grid Layout and Coordinates

The dungeon level in a game snapshot is a plain-text grid written by `dump_map_ai()` in `src/detect.c`. It follows the map legend (section 2) under the label `Map grid:`, and has a two-line column ruler above it and a row number at the start of every row:

```
Map grid:
             1         2
    12345678901234567890
 0:
 1:        -------
 2:        |.....|
 3:        |..@..+
 4:        |>....|
 5:        -------
```

This excerpt stops at column 20 and row 5; a real snapshot's ruler runs to column 79 and its rows to 20. In it the hero `@` is at `<11,3>`, the door `+` at `<14,3>` and the staircase down `>` at `<9,4>`.

- **Coordinates** are written `<x,y>`, column first, as in the legend and in GnollHack level files: x = 1 to 79 left to right, y = 0 to 20 top to bottom. There is no `x = 0` column.
- **Row gutter.** Every map row starts with a 4-character gutter (`MAP_AI_GUTTER_WIDTH`, format `"%2d: "`): y right-aligned, then `": "`, from ` 0: ` to `20: `. The gutter is not part of the map. The xth character after the gutter is cell `<x,y>`; counted from the start of the whole line, cell x is character x + 4.
- **All 21 rows are always printed**, in order, blank rows included. Read y from the gutter rather than counting lines.
- **Column ruler.** The two lines between `Map grid:` and row 0 are indented by the same 4-character gutter. The first has the tens digit at every multiple of ten (`1` above x = 10, `2` above x = 20, … `7` above x = 70); the second runs `1234567890…` up to x = 79. To read a cell's x, take the units digit directly above it on the second line, and the tens digit from the nearest digit at or to the left of it on the first line (none, before column 10, means 0).
- **Rows may arrive right-trimmed** and have no end marker: a column missing from the end of a row is blank. The units ruler line ends in a digit, so it is never trimmed; it is the authoritative column scale.
- **Prefer the legend's coordinates.** The hero's position and the `<x,y>` of every notable location are printed in the legend. Take them from there, and use the ruler for anything the legend does not list. Never state a coordinate you have neither read from the legend nor counted against the ruler.
- A snapshot whose rows have no gutter and no ruler predates this layout; there the first character of each row is x = 1.

## 2. The Map Legend

Between the `Map:` heading and `Map grid:`, `dump_map_legend_ai()` in `src/pager.c` prints a legend for this particular map. Read it before the grid.

- **Reading notes** restate the coordinate system and the gutter, give the hero's position (`The hero is at <11,3>, shown as '@'.`), explain the offsets below, and warn when the hero is hallucinating (every description is unreliable), blind, engulfed (the map shows the inside of the engulfer, not the level), or on an arboreal level.
- **Symbols on this map** lists each character this map actually printed, with its section (Creatures, Objects, Traps, Dungeon features, Terrain, Other), its meaning and a cell count. Blank cells are counted separately as "never seen by the hero" and "solid rock", which shows how much of the level is still unexplored. The line for the hero's symbol says which cell is the hero.
- **Notable locations** gives one line per creature, object, trap and dungeon feature (doors, stairs, ladders, altars, fountains, sinks, thrones, graves, iron bars and the like), in the form `Kind <x,y> 'symbol' [color] description (offset)`. The description is the game's own look-at text, so it names the trap behind a `^` and says whether a `#` is a sink. Stairs and ladders also say where they lead. A feature covered by a creature, item or trap gets its own line, marked "the hero is standing on it" or "currently hidden under something", and the items remembered under a creature are listed after its line.
- **Offsets.** `(3n,2e)` after a location is its distance from the hero in cells, north/south first and then east/west: 3 north (up the screen) and 2 east (right). A location in line with the hero has one part, such as `(4w)`; `(adjacent, northwest)` is one step away in that direction. The hero's own cell has no offset.
- **Limits.** Bulk terrain (floor, corridor, walls, water, lava, trees and similar) gets a cell count but no location lines; read it from the grid. Each kind lists at most 40 locations, and `... and N more ... not listed (legend size limit)` means the rest appear only on the grid.

## 3. Telling the Player Where Things Are

- **The player does not see map coordinates.** GnollHack does not normally show them; only the `whatis_coord` option, off by default, adds them to the description shown when the player moves the cursor to look at something. `<x,y>` is for cross-referencing within the snapshot. Give coordinates to the player only if they ask for them.
- **Describe a location relative to the hero**: direction and distance in words, such as "three squares north and two east" or "right next to you, to the northwest". North is up on the screen, south is down, east is right and west is left.
- **Take direction and distance from the legend's offset**, such as `(3n,2e)`, rather than working them out from coordinates, and put it into words; do not quote the `(3n,2e)` shorthand to the player either. In the section 1 example, the staircase down at `(1s,2w)` is "one square south and two squares west of you".
- **A nearby landmark helps** — a door, a fountain, the stairs.

## 4. Blank Cells and Hero Memory

- **A blank cell is not empty floor.** ` ` means *unexplored* territory or solid, unexcavated rock (`defsyms` entries `unexplored` and `stone` both use `' '`). Blank margins are places the hero has never seen. On the Plane of Air a blank is open air, and a ghost is also rendered as a blank. On an arboreal level, never-seen cells are drawn as trees (`#`) instead of blanks; the legend says when this applies.
- **The map is the hero's memory, not live vision.** Every glyph is what the hero remembers of that cell. A monster or item is drawn where it was last seen; a monster that has moved out of sight can leave a stale glyph behind until that cell is seen again. Never state as fact that a monster is *currently* at a remembered position.
- **Symset caveat.** Terrain glyphs are forced to the plain ASCII defaults, but monster and object glyphs come from the display symbol table, so a player using a custom symbol set could see different characters for those two categories. The tables below are the defaults; the legend's *Symbols on this map* list quotes the character this map actually printed, with its meaning, so trust it where the two differ.

## 5. Monster Class Symbols (`def_monsyms`, `include/monsym.h`)

| Symbol | Class |
|---|---|
| `a` | ants and other insects |
| `b` | blobs |
| `c` | cockatrices |
| `d` | dogs, other canines, and hyenas |
| `e` | eyes, gazers, and spheres |
| `f` | cats and other felines |
| `g` | gnomes, gremlins, and gargoyles |
| `h` | dwarves, humanoids, and tentacled ones |
| `i` | imps and other minor demons |
| `j` | jellies |
| `k` | kobolds |
| `l` | leprechauns |
| `m` | mimics |
| `n` | nymphs |
| `o` | orcs |
| `p` | piercers |
| `q` | quadrupeds |
| `r` | rodents |
| `s` | arachnids and centipedes |
| `t` | trappers and lurkers above |
| `u` | unicorns and horses |
| `v` | vortices |
| `w` | worms |
| `x` | xans and other mythical/fantastic insects |
| `y` | lights |
| `z` | zombies, skeletons, and other lesser undead |
| `A` | angelic beings |
| `B` | bats and birds |
| `C` | centaurs |
| `D` | dragons |
| `E` | elementals |
| `F` | fungi and molds |
| `G` | gnolls |
| `H` | giant humanoids |
| `I` | remembered, unseen invisible monster |
| `J` | jabberwocks and juggernauts |
| `K` | Keystone Kops |
| `L` | liches |
| `M` | modrons |
| `N` | nagas |
| `O` | ogres |
| `P` | puddings and oozes |
| `Q` | quantum mechanics |
| `R` | rust monsters, disenchanters, and rakshasas |
| `S` | snakes |
| `T` | trolls and monsters with similar powers |
| `U` | umbral hulks, otyughs, and chimeras |
| `V` | vampires |
| `W` | wraiths |
| `X` | xorns |
| `Y` | ape- and bear-like creatures |
| `Z` | mummies and other greater undead |
| `@` | humans and elves, including the hero |
| `&` | major demons and devils |
| `'` | golems |
| `;` | sea monsters (eels, krakens) |
| `:` | lizards and hydras |
| `#` | treants |
| `~` | long worm tails |
| `]` | mimic imitating an object |
| ` ` | ghosts |

Warning glyphs `0`–`6` (`def_warnsyms`) mark an unseen creature detected by warning, in ascending order of threat. Only `0` collides with an object class (iron ball). Glyphs `1`–`6` are unambiguous warning indicators.

## 6. Object Class Symbols (`def_oc_syms`, `include/objclass.h`)

| Symbol | Class |
|---|---|
| `)` | weapons |
| `[` | armor |
| `=` | rings |
| `"` | amulets |
| `(` | tools (pick-axes, keys, lamps, bags, horns, instruments) |
| `%` | food and corpses |
| `!` | potions |
| `?` | scrolls |
| `+` | spellbooks |
| `/` | wands |
| `$` | gold coins (`'` is an alternate coin symbol) |
| `*` | gems and rocks |
| `` ` `` | boulders and statues (large stones) |
| `0` | iron balls |
| `_` | iron chains |
| `.` | splashes of venom |
| `]` | illegal objects, and mimics imitating an object |
| `9` | reagents |
| `8` | miscellaneous items |
| `7` | art objects |

## 7. Terrain and Feature Symbols (`defsyms`, `src/drawing.c`)

| Symbol | Terrain / feature |
|---|---|
| ` ` | unexplored, solid stone, or open air |
| `\|` | vertical wall, open door, grave, brazier, or signpost |
| `-` | horizontal wall, wall corner or junction, or open door |
| `.` | room floor, dark room floor, doorway, broken door, open portcullis, ice, or lowered drawbridge |
| `,` | grass, soil, or sand |
| `#` | corridor, iron bars, tree, sink, raised drawbridge, cloud, or poison cloud |
| `<` | staircase or ladder up |
| `>` | staircase or ladder down |
| `+` | closed door |
| `^` | trap (see below) |
| `}` | water, moat, pool, or molten lava |
| `{` | fountain |
| `_` | altar or anvil |
| `\` | opulent throne or lever |
| `0` | boulder |
| `"` | web |
| `~` | vibrating square |

## 8. Traps

Almost every discovered trap is drawn as `^`: arrow, dart and falling rock traps; squeaky board; bear trap; land mine; rolling boulder trap; sleeping gas, rust and fire traps; pit and spiked pit; hole and trap door; teleportation trap, level teleporter, magic portal and geometric magic portal; statue trap; magic trap; anti-magic field; polymorph trap.

Three do not: `"` web, `~` vibrating square, `\` lever.

`^` on the grid therefore tells you a trap is remembered there, not which trap. The legend's `Trap <x,y> '^'` line for that cell names it. If there is no such line (past the legend's size limit, for example), use the in-game messages in the snapshot, or ask the player, before naming a trap type.

## 9. Ambiguous Symbols

One character can mean several things. For a creature, object, trap or dungeon feature, the legend's *Notable locations* line for that cell resolves it. Bulk terrain has no such line, so resolve it by context — surrounding terrain, the snapshot's message log and dungeon overview, and the player's own account.

- ` ` — unexplored, solid stone, open air, or a ghost
- `#` — corridor, iron bars, tree, sink, raised drawbridge, cloud, poison cloud, or a treant
- `.` — room floor, doorway, broken door, open portcullis, ice, lowered drawbridge, or a splash of venom
- `+` — closed door or a spellbook
- `-` — horizontal wall, corner, or open door
- `\|` — vertical wall, open door, grave, brazier, or signpost
- `_` — altar, anvil, or an iron chain
- `\` — opulent throne or a lever
- `"` — amulet or a web
- `~` — long worm tail or the vibrating square
- `]` — mimic imitating an object, or an illegal object
- `'` — golem or a pile of coins
- `0` — boulder, iron ball, or a warning glyph for an unseen creature

A monster or object glyph hides the terrain beneath it: the hero standing on a staircase shows `@`, not `<`. The legend still lists a hidden dungeon feature, marked "the hero is standing on it" or "currently hidden under something".

---
*Sources: `src/detect.c` (`dump_map_ai`, `dump_map_ai_ruler`), `src/pager.c` (`dump_map_legend_ai`), `src/do_name.c` (`coord_desc`), `include/config.h` (`MAP_AI_GUTTER_WIDTH`), `src/drawing.c`, `include/monsym.h`, `include/objclass.h`, `include/global.h` in the GnollHack C core.*
