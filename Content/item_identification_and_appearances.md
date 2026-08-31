---
title: Item Identification & Randomized Appearances
summary: Which item appearances are randomized each game, and how to identify unknown items
---

#### 1. Overview of Randomized Appearances
In GnollHack, the visual appearances, colors, and descriptions of magical items are randomized at the beginning of each game by `shuffle_all()` in `src/o_init.c`. Compile-time definitions in `src/objects.c` and static wiki appearance tables only list the pool of possible appearances, never the actual assignment in the current game.

#### 2. Shuffling Rules & Material Permutations
GnollHack divides item shuffling into three distinct groups:
- **Whole Classes (Appearance & Materials Randomized):** Amulets, potions, scrolls, spellbooks, and venoms.
- **Type Ranges (Appearance Only, Materials Fixed):** Helmets, gloves, shirts, cloaks, boots, staves, bags, candles, lamps, whistles, flutes, horns, harps, drums, and jars of extra healing salve. For these items, only the description is permuted; the item's material remains fixed.
- **Type Ranges (Appearance & Materials Both Randomized):** Wands, rings, robes, bracers, brooches, nose rings, headbands, ioun stones, lenses, goggles, belts, crowns, cornuthaum-class hats, and mushrooms. Note that wands and rings are shuffled by type ranges (`WAN_LIGHT` through `LAST_SHUFFLED_WAND`, and `RIN_ADORNMENT` through `RIN_PROTECTION_FROM_SHAPE_CHANGERS`), unlike NetHack where they are whole classes.
- **Excluded From Shuffling:** Magic swords and all other weapons (except staves); the potion of water and every potion type defined at or after it in the enum; non-magic and unique amulets, scrolls, and spellbooks; and reagents.

#### 3. Why Source Code & Wiki Tables Do Not Identify Items
Strings like `SCROLL("remove curse", "PRATYAVAYAH", ...)` in `src/objects.c` represent pre-shuffle compile-time initializers. In a live game, `PRATYAVAYAH` could be a scroll of fire, teleportation, or create monster. Overseer will never use source code appearance strings or wiki tables to identify an unidentified item for the player.

#### 4. Formal & In-Game Identification Methods
To identify items safely and reliably during gameplay:
- **Scroll / Spell of Identify:** Identifies one or more inventory items definitively. Blessed identify can reveal the entire inventory.
- **Altar BUC Testing:** Dropping an item on a co-aligned altar reveals whether it is Blessed (glowing flash), Uncursed, or Cursed (black glow).
- **Shop Price Identification:** Selling and buying price brackets narrow down unknown scrolls, potions, rings, and wands to specific price tiers.
- **Wand Engraving:** Engraving on the floor with a wand (`E`) tests wand effects without expending valuable charges on some types.
- **Observation on Use:** Safe consumption or zapping in controlled environments can reveal identities.

#### 5. Quick Answer Reference
- **Are item appearances fixed?** No, magical item appearances are reshuffled every game.
- **Are materials randomized too?** Yes for whole classes, wands, rings, and select jewelry/armor; No for helmets, gloves, cloaks, boots, and staves (materials are fixed).
- **Are swords shuffled?** No, magic swords are not shuffled.
- **What will Overseer tell you?** Overseer explains mechanics, identification techniques, and price brackets, but will never guess an unidentified item's identity based on appearance strings.
