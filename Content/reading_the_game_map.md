---
title: Reading the GnollHack Game Map
summary: How to read the ASCII map in a GnollHack snapshot — grid layout, coordinates, blank cells, hero memory, and the complete monster, object, terrain and trap symbol tables
---

## 1. Grid Layout and Coordinates

The dungeon level in a game snapshot is a plain ASCII grid written by `dump_map_ai()` in `src/detect.c`. It has no ruler, no row numbers, no border and no legend — it is 21 bare lines of text:

- **21 rows**, always all of them, in order. The first map line is row `y = 0`, the last is `y = 20`. Fully blank rows are still written, so the Nth line of the block is always `y = N - 1`.
- **79 columns per row**: the first character of a line is `x = 1`, the last is `x = 79`. There is no `x = 0` column.
- Coordinates in this article and in GnollHack level files are written `<x,y>`, column first — `<24,7>` is column 24, row 7.
- **There is no coordinate ruler.** To give a coordinate, count characters from the start of the line and add 1. To compare two positions, compare their line numbers and their character offsets. Never guess a coordinate you have not counted.
- Rows are padded to full width, so column N is at the same character offset on every row. Trailing blanks are real map cells, not formatting.

## 2. Blank Cells and Hero Memory

- **A blank cell is not empty floor.** ` ` means *unexplored* territory or solid, unexcavated rock (`defsyms` entries `unexplored` and `stone` both use `' '`). Blank margins are places the hero has never seen. On the Plane of Air a blank is open air, and a ghost is also rendered as a blank.
- **The map is the hero's memory, not live vision.** Every glyph is what the hero remembers of that cell. A monster or item is drawn where it was last seen; a monster that has moved out of sight can leave a stale glyph behind until that cell is seen again. Never state as fact that a monster is *currently* at a remembered position.
- **Symset caveat.** Terrain glyphs are forced to the plain ASCII defaults, but monster and object glyphs come from the display symbol table, so a player using a custom symbol set could see different characters for those two categories. The tables below are the defaults.

## 3. Monster Class Symbols (`def_monsyms`, `include/monsym.h`)

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

## 4. Object Class Symbols (`def_oc_syms`, `include/objclass.h`)

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

## 5. Terrain and Feature Symbols (`defsyms`, `src/drawing.c`)

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

## 6. Traps

Almost every discovered trap is drawn as `^`: arrow, dart and falling rock traps; squeaky board; bear trap; land mine; rolling boulder trap; sleeping gas, rust and fire traps; pit and spiked pit; hole and trap door; teleportation trap, level teleporter, magic portal and geometric magic portal; statue trap; magic trap; anti-magic field; polymorph trap.

Three do not: `"` web, `~` vibrating square, `\` lever.

`^` therefore tells you a trap is remembered there, not which trap. Use the in-game messages in the snapshot, or ask the player, before naming a trap type.

## 7. Ambiguous Symbols

One character can mean several things. Resolve by context — surrounding terrain, the snapshot's message log and dungeon overview, and the player's own account.

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

A monster or object glyph hides the terrain beneath it: the hero standing on a staircase shows `@`, not `<`.

---
*Sources: `src/detect.c` (`dump_map_ai`), `src/drawing.c`, `include/monsym.h`, `include/objclass.h`, `include/global.h` in the GnollHack C core.*
