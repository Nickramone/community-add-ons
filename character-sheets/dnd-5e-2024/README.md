# D&D 5th Edition (2024)

A character sheet for the 2024 revision of D&D 5th Edition, with a custom HTML
layout that follows the shape of the published sheet.

On a phone the sheet has its own layout, `dnd-5e-2024.mobile.html` and
`.mobile.css`, with the same content in one column across seven tabs:
**Main** (hit points, AC, initiative, speed, proficiency, active effects,
heroic inspiration, resources with the hit dice, death saves, and each
ability's modifier, score and save - what play reaches for), **Skills**
(passive Perception and every skill, then each ability's base and bonus),
**Combat** (attack bonuses, weapons, class features, feats, species traits and
equipment training), **Spells**, **Gear**, **Story** (background,
species, the other details, portrait, appearance and backstory) and **Notes**.

## What it covers

- **Abilities** with live modifiers, and saving throws that add proficiency
  where you have it
- **Armour class, initiative, passive Perception and proficiency bonus**, all
  derived — proficiency scales `2 + floor((level - 1) / 4)`, and passive
  Perception picks up your Perception proficiency automatically
- **Armour class from what you wear**: the best equipped armour (Dexterity
  added in full for light armour, up to +2 for medium, not at all for heavy),
  equipped shields, and the AC bonus of magic items that are equipped (and
  attuned, where they need it). With no armour: 10 + Dexterity, plus
  Constitution for a Barbarian or Wisdom for a Monk (Unarmored Defense, picked
  as a class feature; the Monk's version is lost with a shield). Bracers of
  Defense count only with no armour and no shield. Magic armour such as +1
  Armor is added as a magic item next to the ordinary armour it enchants.
  *Armour Class Bonus* in Other details is for anything else (a fighting style,
  a spell). Needs the per-row forms (`sum_each`, `max_each`) of the Grimoire
  fork. Freeform items (typed in rather than picked) never add to AC, saves,
  attacks or spells: bonuses come only from catalogue entries.
  With a shield in the equipment, a *Shield* box under the armour class equips
  or unequips it without opening the list (`<g-check>`, also from the fork)
- **Skill proficiency tiers** — none, half (`floor(proficiency / 2)`), proficient,
  or expertise — via the skill ladder (useful for Jack of All Trades-style half
  proficiency on individual skills)
- **Spellcasting** that only appears for casters: pick the ability and the save
  DC and attack bonus follow
- **Equipment** picked from the catalogue or typed in, each with a quantity,
  and carried weight - counting quantity - against a `Strength × 15` capacity
- **Magic items**, each marked equipped and, only for those that need it,
  attuned: past three attuned items the box can no longer be ticked
  (`visible_if` and `disabled_if` on per-entry fields, from the Grimoire
  fork). Items equipped (and attuned, where they need it) add their bonuses:
  saving throws (Cloak of Protection), spell attack and save DC (Rod of the
  Pact Keeper), attack and damage on a line of their own under the attack
  bonuses (+1 Weapon, Staff of Power, Bracers of Archery on ranged damage
  only, Sword of Kas's critical range), ability scores set to a value
  (Amulet of Health, Belts of Giant Strength) or raised up to a maximum (Ioun
  Stones, Belt of Dwarvenkind, Manuals and Tomes while they are in the list
  and equipped), proficiency bonus (Ioun Stone of Mastery), ability checks
  (Stone of Good Luck), walking speed (Boots of Striding and Springing), other
  speeds as a line under Speed and resistances and immunities among the
  active effects. Potions never count, and neither do items that let you
  choose the ability (Book of Vile Darkness, Deck of Many Things). The item
  lines need `<g-repeat>` over a content list and `<g-value formula>` from the
  Grimoire fork
- **Active effects**: exhaustion (0-6), concentration, the fourteen other
  conditions and a list for anything else (Bless, a potion, a curse). Each
  active one is summarised in one line, and the numbers follow: exhaustion
  lowers saves, skills, initiative, AC, spell save DC and the attack bonuses,
  and Grappled, Restrained, Paralyzed, Petrified, Unconscious or exhaustion
  level 6 bring the current speed to 0. Losing concentration while
  incapacitated, and exhaustion level 6, raise a warning
- **Campaign house rules switch** (on by default): exhaustion as a table
  rule - −1 per level to AC, spell save DC, saving throws, ability checks,
  attack rolls and damage, −10 ft of speed from level 3, a long rest removes
  two levels. Switched off, the 2024 rule: −2 per level to every d20 Test and
  −5 ft of speed per level
- **Resources**: one list of what the character spends - uses, maximum, how it
  comes back (short rest, long rest, dawn) and where it comes from - shown
  under the hit dice
- **Class feature uses**: each feature with uses (Rage, Channel Divinity,
  Bardic Inspiration, Superiority Dice and so on) gets a line under the
  resources with one box per use, ticked as they are spent - as many as the
  character's level (`uses_by_level`) and ability modifier (`uses_ability`)
  allow, with how many are left - and how it comes back. Past 20 (Lay on
  Hands) the boxes give way to a number. Features without uses get no box,
  in the tracker or in the Class Features list. The Short rest button resets the short-rest ones and gives back
  `short_regain` uses of the ones that return one use on a short rest (Rage,
  Channel Divinity, Wild Shape, Second Wind); Long rest resets all. The level
  is the character's level, until the sheet tracks classes one by one. Needs
  `by_level` and `<g-pips formula per>` from the Grimoire fork
- **Species trait uses**: species traits with uses (Breath Weapon,
  Stonecunning, Giant Ancestry, Adrenaline Rush, Healing Hands and so on)
  get the same boxes - `uses`, `uses_by_level` or `uses_pb` (as many as the
  Proficiency Bonus) - reset by the rest buttons
- **From the class and species**: armour training and weapon proficiencies
  start from the class; the HP maximum adds Dwarven Toughness (+1 per level)
  and the Tough feat (+2 per level)
- **Magic item charges**: each equipped or attuned magic item with `charges`
  gets a line under the feature uses, one box per charge (a number past 20),
  with how many are left and its `recharge`. Short rest resets the
  short-rest ones; Long rest resets short, long and dawn ones in full (a
  dawn item that regains only some charges is corrected by hand)
- **Lineage**: a species with a sub-choice (Elf, Dragonborn, Goliath, Gnome,
  Tiefling) shows a Lineage picker under it, labelled with the species' own
  name for the choice (Elven Lineage, Draconic Ancestry...); a lineage of
  another species is flagged. Catalogue type `lineage` (`species`, `label`,
  `damage_type`, `darkvision`, `speed`, cantrips and level 1/3/5 spells with
  their ids, uses and recovery); species carry `lineage_label` and `lineages`.
  Under the picker, the lineage's damage type, darkvision and speed; its
  speed becomes the base speed; its spells, by character level, above the
  spell list; its free uses (`lineage_used`) tracked in Resources and reset
  by a long rest
- **Catalogue data for weapon rows**: weapons (equipment and magic items) carry
  `damage_dice`, `damage_type`, `damage_versatile`, `range_normal`,
  `range_long` and the `ranged`, `thrown`, `finesse`, `light`, `heavy`,
  `two_handed`, `reach` flags; magic weapons with a known base carry
  `base_item`, and magic weapons and armour with a known base `base_item_ref`
  (the base's id); feats carry `resource`, `uses`, `uses_pb` and `recovery`;
  species traits carry a saving throw (`save_ability`, `dc_ability`) and an
  effect (`effect_label`, `effect_die`, `effect_dice_pb`,
  `effect_dice_by_level`, `effect_flat_pb`)
- **Base of a generic magic weapon or armour** (+1 Weapon, +1 Armor): a Base
  Weapon or Base Armor pick on the Magic Items row, from the weapons or the
  armour only, filled in from `base_item_ref` when the item names its base.
  The attack row uses the base's dice and properties, and the AC the base's
  armour with the item's bonus on top; equip the magic item, not the base.
  Needs a Grimoire with per-entry picks (catalogue picks inside a row)
- **Attacks** in one box: Unarmed Strike; a row for each equipped weapon and
  magic weapon (with a Versatile two-handed row and a thrown row where they
  apply), with the attack bonus (proficiency where the weapon training
  covers the weapon, Finesse taking the better of Strength and Dexterity,
  ranged weapons Dexterity, Archery's +2), damage dice, modifier and type,
  range or reach, and a magic weapon's own bonuses and critical range; magic
  items with attack or damage bonuses and no weapon data keep a Strength and a
  Dexterity row; the spell attack and save DC for a caster; notes for
  Dueling, Great Weapon Fighting, Two-Weapon Fighting, Great Weapon Master,
  Heavy Armor Master, Defensive Duelist and Defense, with the proficiency
  bonus filled in. The typed list below is for other attacks and damage
  cantrips
- **Feats worked into the numbers**: Alert adds proficiency to initiative,
  Speedy (+10 ft) and Boon of Speed (+30 ft) add to the current speed,
  Boon of Fortitude adds 40 to the HP maximum, Defense +1 AC in armour
- **Where a score comes from**: under each ability, the starting score, the
  background bonus and what magic items add; the base box is labelled
  Starting score, the bonus box Background
- **Background increases**: three menus under the background, +1 each (the
  same ability twice is +2, three times is flagged), with the abilities the
  background lists beside them; they fill the Background boxes. Tools come
  from the class and the background
- **Attack rows**: damage as large as the hit bonus, with "to hit" and the
  damage type beneath; Unarmed Strike last. **Subclass** from level 3;
  cantrips have no Prepared box
- **Attacks list**, feats, and a catalogue of classes, subclasses, species,
  backgrounds, feats
  and spells
- **Custom class, species, or background** — type a homebrew name when the
  catalogue entry is missing (or you prefer not to pick one)
- **Picking a class** adds its level 1 features, and **picking a subclass** adds
  the features it grants at the level it is chosen
- **Your character's art, large** on the Spells & Details page, beside their
  appearance - framed the way you chose (click it to choose)

## With the SRD 5.2 pack

The [`dnd-5e-srd`](../../content-packs/dnd-5e-srd/) pack carries the SRD's
classes, its subclasses and every class and subclass feature, species and
their traits,
backgrounds, feats, all of its spells, its equipment (weapons with damage,
properties and mastery; armour with its AC, Strength and Stealth) and its
magic items.

## Licence

The SRD 5.2 is published under **CC BY 4.0**, which permits redistribution and
adaptation with attribution.

The credit Grimoire displays, reproduced in `attribution`:

> This work includes material from the System Reference Document 5.2 ("SRD 5.2")
> by Wizards of the Coast LLC, available at https://www.dndbeyond.com/srd. The
> SRD 5.2 is licensed under the Creative Commons Attribution 4.0 International
> License, available at https://creativecommons.org/licenses/by/4.0/legalcode.

- Licence: <https://creativecommons.org/licenses/by/4.0/>
- SRD: <https://www.dndbeyond.com/srd>

This sheet reproduces the *structure* of a character, not the text of the rules.
No artwork or page scans are included. A content pack carrying SRD entries
themselves is a separate download and carries the same notice.
