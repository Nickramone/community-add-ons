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

- **Level-ups**: one row per level (class, hit die, HP rolled or the average,
  and a choice: Ability Score Improvement as +2 / +1 / +1 columns, feat,
  subclass, spells). The level, maximum hit points (first level at the full
  die) and the Proficiency Bonus follow the rows; a sheet with no rows keeps
  using the Level field. The ASI picks add to the ability scores
- **Level up button** under Level: asks for the hit points rolled (0 = the
  average), then, on the levels your class grants one, an Ability Score
  Improvement (+2, or +1/+1) or a feat you qualify for (General, or an Epic
  Boon from level 19; level, ability score, spellcasting and armour training
  are checked), and a subclass at the class's subclass level. It adds the
  level-up row and the feat for you
- **Class feature choices** right after Level up, only on a level that has
  them: a Fighting Style feat (Fighter 1, Paladin 2, Ranger 2, Champion 7;
  Blessed Warrior and Druidic Warrior only for their class), one option of
  Divine Order, Primal Order, Blessed Strikes or Elemental Fury (added as a
  class feature whose effects the sheet works out: Heavy or Medium armour and
  Martial weapons for Protector and Warden, Wisdom added to Arcana, Religion or
  Nature checks for Thaumaturge and Magician), Expertise in skills you are
  proficient in, and the skill, language and tool proficiencies a class or
  subclass feature lets you choose. The levels come from the class and
  subclass entries (`*_by_level` fields)
- **Metamagic, Eldritch Invocations and Maneuvers**: a *Class Option* catalogue
  type (`option`, with its prerequisites as fields: `prereq_level`,
  `prereq_option` for an invocation that needs a Pact or another invocation,
  `repeatable`) and a list under Class Features. Class feature choices asks
  for the new ones on each level that grants them (`option_type` and
  `options_by_level` on the class or subclass: Sorcerer, Warlock, Battle
  Master), up to three, leaving out those you have unless repeatable and those
  whose prerequisite you lack; on any later level you may replace one with
  another, each question naming the kind (Metamagic, Eldritch Invocation,
  Maneuver). Replacing needs `unpick`, the headings `label_formula`, from the
  Grimoire fork
- **Subclass feature choices** (land of the Circle of the Land, Hunter's Prey and
  Defensive Tactics, Aspect of the Wilds, Elemental Affinity, Primal Companion,
  Dread Allegiance): a *Choice* on the feature's row in Class Features, offering
  only that feature's options (`choice_options`). Level up asks for the first
  one among the *Class Option* entries of that feature (`option_type` is the
  feature's name), each opening to show what it does (`choice_by_level` and
  `choice_label_by_level` on the subclass); those you may change after a rest
  you change on the row. A feature with no choice made is flagged. Writing the
  answer onto the row needs `row._ref` in an `each` step, the row's own options
  `options_filter` and `width` on a per-entry select, from the Grimoire fork
- **A new character** (no class, no level-up rows) opens the Level up window by
  itself (`start_prompt`, from the Grimoire fork); put off, it waits under
  *Choices to make*
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
- **Spells** in one list, each with its origin (Class, Subclass, Spellbook,
  Feat, Species, Item, or Other for a spell added by hand; only Other and
  Spellbook can be changed, and Spellbook only for a Wizard), drawn by level,
  each level under its own gold rule: one **Spells** list (every spell, with the
  box to prepare it and ● on the always-prepared ones) or, for a Wizard,
  **Prepared** (cantrips, prepared and always-prepared spells, with
  components), **Known** and **Spellbook**; each row opens on its description (`<g-value
  markdown>`, from the Grimoire fork); the catalog filters spells by Spell List. Counters for cantrips, prepared spells and
  the spellbook come from the class's `cantrips_by_level`, `prepared_by_level`
  and `spellbook_by_level`. Past the class maximum the Prepared box can no
  longer be ticked; always-prepared spells (subclass, feat, species, item) do
  not count, a Bard's, Sorcerer's or Warlock's class spells change only on level
  up. Warnings: too many or too few cantrips and prepared spells, too few spells
  in a Wizard's book, a spell above the highest slot level (or Mystic Arcanum),
  a class or spellbook spell off the class list (any list for a Bard from
  Magical Secrets on), a spell taken at a level the character no longer has.
  **Level up** asks, in a Spells step after the class choices, for the new
  cantrips, the new spells (a Bard, Sorcerer or Warlock learns them, any other
  caster prepares them), a Wizard's new spellbook spells, a Warlock's Mystic
  Arcanum, and lets the character replace one class cantrip and, for a Bard,
  Sorcerer or Warlock, one class spell; only spells of the class list (and the
  Magical Secrets lists), up to the highest slot level and not already taken
  are offered, each with its level beside the name (`entries` prompt step and
  its `entry_note`, from the Grimoire fork). **Prepare
  spells**, in Spells for a Cleric, Druid, Paladin or Ranger, swaps prepared
  spells for others of the class list. **Choose missing spells** appears in Spells while
  cantrips, a Bard's, Sorcerer's or Warlock's spells, a Wizard's spellbook or a
  Mystic Arcanum are missing (a Level up skipped), and asks only for those. A
  **Choose missing species spells** grants the lineage spells (and asks for the chosen ones) that a skipped lineage prompt left out, skipping the ones already held. Skills picked from the class (at the class pick and at Level up) are also recorded in **Skills From Class**, and a warning shows when there are fewer than the class and subclass give by that level (a character made before 1.40.0 has the field empty: fill it by hand). Languages and tools chosen at Level up (Thieves' Cant, Deft Explorer, Student of War...) are recorded the same way in **Languages From Class** and **Tools From Class**, with the same warning (fields empty before 1.41.0: fill by hand). With Ritual Caster, Level up at 5, 9, 13 and 17 asks for one more level 1 Ritual spell (always prepared); the feat's casting ability is asked only while none of its spells has one, then taken from them. Bard's, Sorcerer's or Warlock's class spells show a fixed ✓ instead of the box. The spells a class or subclass always
  has prepared (domain, oath, circle, patron spells; Hunter's Mark, Divine
  Smite) arrive at the level that grants them: those of the level the class or
  subclass is chosen at with the pick, the later ones with Level up, from the
  converter's `auto_spell_*` and `auto_spell_*_N` lists. Spells of feats,
  species and items come the same way, always prepared and outside the limits:
  a feat asks for its spells when it is picked (Magic Initiate: the list, the
  ability, two cantrips and one level 1 spell; Fey-Touched and Shadow-Touched:
  the ability and one level 1 spell of the right schools, the fixed spell
  coming with it; Ritual Caster, Blessed Warrior, Druidic Warrior, Telepathic,
  Telekinetic), and so does a background that gives Magic Initiate; a species
  with a fixed spell (Aasimar: Light) and a magic item (Magic Items, from the
  catalogue's `granted_spell_*`, with the charge cost as its free uses) add
  theirs on pick, and removing the row takes them back. An item's spells show
  only while the item is active (equipped, and attuned if it needs attunement;
  a potion, which has no Eq. box, counts while it is on the list; the full list
  under «Add, remove or edit spells» still shows every row): a spell picked before 1.42.0 does
  not know its item and always shows, until the item is removed and picked
  again. A spell with a free
  use per rest gets a line in Resources (long rest, or short or long rest),
  cleared by the rest buttons, and a spell cast with another ability than the
  class's has its own save DC and attack under the spell counts
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
  incapacitated, and exhaustion level 6, raise a warning. Concentrating is a box (1.44.0): ticking it
  opens a window with the character's own Concentration spells, and the one
  picked shows beside the box until it is unticked; putting the window aside
  unticks it, and a rest or Current HP at 0 ends Concentration by itself
  (both need the Grimoire fork's field `on_change` and prompt `on_skip`)
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
  speed becomes the base speed; its spells come with the lineage (level 1)
  and with Level up (levels 3 and 5), always prepared, after one question for
  the spellcasting ability (Intelligence, Wisdom or Charisma, kept in
  `species_spell_ability`) and, for the High Elf, the Wizard cantrip
- **A feat of a category instead of the background's** (1.45.0): a background
  with `feat_category` (Ravenloft's Haunted One and Investigator: Survivor or
  Sharp Eye, or a Dark Gift feat; Mist Wanderer and Spirit Medium: a Dark Gift
  feat) grants no feat on its own; a window offers the feats of that category
  and the ones listed in `feat_options`, and the feat chosen goes away with
  the background
- **What feats and species grant** (1.45.0): skill proficiencies, Expertise,
  languages and damage resistances, immunities and condition immunities, fixed
  (`skill_proficiencies`, `expertise`, `language_proficiencies`,
  `resistances`, `immunities`, `condition_immunities`) or chosen in the feat's
  or species' window (`skill_options`/`skill_count`, `expertise_count` among
  the skills you have, `language_count`, `resist_options`/`resist_count`); a
  lineage's damage type is a resistance. What a feat adds goes away with it.
  **Defenses** box under Languages (Resistances, Immunities, Condition
  immunities, editable by hand) and a line for each among the active effects;
  darkvision (the larger of the species' and the lineage's) and the senses of
  feats (`senses`: Blindsight, Truesight) under Speed
- **Subclass spellcasters** (1.46.0): an Eldritch Knight or Arcane Trickster
  casts from its subclass, which carries the class's spellcasting fields
  (`spellcasting`, `caster_type` `third`, `caster_from_level`, `spell_list`
  Wizard, `cantrips_by_level`, `prepared_by_level`, `prepare_change`,
  `slot_max_by_level`). Caster Level is a third of the class level rounded up
  from level 3, so the slots follow the subclass table; Level up offers the
  cantrips and the spells learned from the Wizard list; spells off that list
  get the ⚠ mark; the subclass counts as Spellcasting for feat prerequisites
  (War Caster). The formulas `sub_caster` and `spell_class` pick the class or
  the subclass
- **Layout** (1.46.1): Level up heads the Main page on a phone; Heroic Inspiration is a checkbox beside the character name; the Campaign house rules switch sits under Other details (Story); Other Attacks & Damage Cantrips shows only when it holds text; the Metamagic / Invocations / Maneuvers box shows only for a class or subclass that has such options and takes their name; on a phone Initiative, Speed, Proficiency and Passive Perception share one style
- **Layout** (1.46.2): Short and Long rest sit in the Hit Points box; Exhaustion, Concentrating and Raging share one row and Exhaustion has only its six boxes; resistances, immunities and condition immunities are read-only text; armour training is text of the categories held; darkvision and feat senses are lines among the active effects; the pack item ids, names and quantities of a pack are hidden in the entry detail
- **Layout** (1.46.3): on the desktop sheet Level up sits under XP; armour training is stacked like weapons and tools; Exhaustion, Concentrating and Raging are rows of one column; read-only effect text shares the 12px of the other effects
- **Layout** (1.46.4): Equipment Training & Proficiencies moves to the Story page, before Languages; the languages known (`language_profs`) are read-only text
- **Layout** (1.46.5): Level up is a larger gold button with a glow, on the desktop sheet too; the rest buttons are no longer all capitals
- **Layout** (1.46.6): the text of the rest buttons and of Level up is centred; the Level box is wider so Level up fits
- **Layout** (1.46.7): on the desktop sheet XP folds under its caption (closed by default), the "follows your levels" mark beside Level is hidden, and Level up sits at the foot of the Level box, its text centred
- **Layout** (1.46.8): the stylesheet passes the app's style check again (no `content` property; the arrow beside XP is text in the summary)
- **Layout** (1.46.9): on the desktop sheet the Level figure sits on the row of the Hit Points figures and Level up has the size and row of the rest buttons
- **Layout** (1.46.10): saving-throw proficiency boxes are read-only (they follow the class; `*_save_prof` stays a field for the formulas); the "follows your class" mark beside Hit Dice Max is hidden
- **Layout** (1.46.11): the read-only text of resistances and immunities among the active effects takes the size of the effect line around it
- **Origin read-only** (1.47.0): Class, Subclass, Species, Lineage and Background are read-only on the sheet and open their entry's detail in a window (a fork feature); they are chosen in Level up, which now offers the Lineage of a species that has lineages, filtered to that species, and asks for it again while it is missing; the Level-ups rows cannot be reordered
- **Class tools and species size** (1.48.0): picking a class that lets you choose tools (Bard: three Musical Instruments; Monk: one Artisan's Tools or Musical Instrument) asks for them with the class skills; they go to the chosen tools and Tools From Class, and the Tools text lists them instead of the choice. Picking a species of more than one size (Human, Aasimar, Tiefling...) asks for the size, which Size then shows until the species changes
- **Armour effects** (1.49.0): wearing armour you lack training with shows, among the active effects, Disadvantage on Strength and Dexterity checks, saves and attacks and no spellcasting; armour with Stealth Disadvantage (also as the base of magic armour, except Mithral) shows it there too
- **Shield training and armour Strength** (1.50.0): a shield carried without Shield training adds nothing to AC (also a magic shield) and says so among the active effects; armour whose Strength requirement is above your Strength score (also as the base of magic armour, except Mithral) takes 10 ft from the current Speed, shown there too
- **Speed under heavy armour** (1.50.2): while armour above your Strength is worn, the Speed box shows the figure 10 ft lower in place of its input, with no "Now" line beneath (1.50.1 tried this in the field's default and was invalid)
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
- **Attacks** in one box: Unarmed Strike (with the die of Unarmed Fighting, Tavern Brawler or the Monk's Martial Arts, which also takes the better of Strength and Dexterity; Unarmed Fighting drops to a d6 while a weapon or Shield is held); a row for each equipped weapon and
  magic weapon (with a Versatile two-handed row and a thrown row where they
  apply), with the attack bonus (proficiency where the weapon training
  covers the weapon, Finesse (and a Monk weapon, with no armor or Shield) taking the better of Strength and Dexterity and, for a Monk weapon, the Martial Arts die when larger than the weapon's, a weapon ticked Pact (Pact of the Blade) taking Charisma when higher,
  ranged weapons Dexterity, Archery's +2), damage dice, modifier and type,
  range or reach, and a magic weapon's own bonuses and critical range; magic
  items with attack or damage bonuses and no weapon data keep a Strength and a
  Dexterity row; the spell attack and save DC for a caster, and for each other casting ability that a feat, species or item spell uses (a non-caster with a Magic Initiate spell gets its row too); Dueling (+2, one-handed melee weapon with no other weapon held), Thrown Weapon Fighting (+2 on thrown attacks),
  Great Weapon Master (+proficiency with a Heavy weapon) and Rage (a Raging box next to Concentrating On for a Barbarian: +2/+3/+4 on Strength attacks,
  cleared by a rest) are added to the damage; notes for
  Great Weapon Fighting, Two-Weapon Fighting,
  Heavy Armor Master, Defensive Duelist and Defense, with the proficiency
  bonus filled in. The typed list below is for other attacks and damage
  cantrips
- **Extra damage** (1.43.0): damage a hit can add but the row's number leaves
  out, because its type differs or it depends on the moment, is listed once in
  an Extra damage box under the attack rows, with its dice worked out for the
  character, and each attack row it can apply to shows its name in small type
  (Sneak Attack*): Sneak Attack (Finesse or Ranged weapons; Assassinate, and
  the cost of Cunning Strike and Devious Strikes in small type), Colossus
  Slayer (the Hunter's Prey choice), Divine Strike and Primal Strike (2d8 with
  the level 14 and 15 improvements), Radiant Strikes, Divine Fury and Frenzy
  (while raging), Brutal Strike (with its cost), Dreadful Strikes (Fey
  Wanderer) and Dreadful Strike (Gloom Stalker, with its uses), Hunter's Mark
  (d10 with Foe Slayer) and Hex while you are Concentrating on them, Divine Favor
  (an Active box, cleared by a rest), Eldritch Smite and Lifedrinker on the
  pact weapon, and the Smite spells the character has prepared (Divine,
  Searing, Thunderous, Wrathful, Shining, Blinding, Staggering, Banishing),
  each with its dice for every free slot level up to 5th and Paladin's Smite's
  free cast while unused. Critical hits are not worked out
- **Short feat and trait pages**: the entry shown in a pick or the Compendium keeps only the prerequisites and the description; the fields the sheet's formulas read are marked `visible_if: "false"`, which needs a Grimoire that hides them (the fork's `ContentEntryDetail`)
- **Feats worked into the numbers**: Alert adds proficiency to initiative,
  Speedy (+10 ft) and Boon of Speed (+30 ft) add to the current speed,
  Boon of Fortitude adds 40 to the HP maximum, Defense +1 AC in armour
- **Where a score comes from**: under each ability, the starting score, the
  background bonus and what magic items add; the base box is labelled
  Starting score; the Bonus box holds the background, level-up and feat increases, and the player can still add more there by hand, up to +10
- **Background increases**: picking a background opens a window to spread
  +2 and +1, or +1 to each of the three, over the abilities it lists; the
  result fills the Bonus boxes, together with the level-up rows and the
  ability increase set on a feat. Tools come from the class and the
  background
- **Attack rows**: damage as large as the hit bonus, with "to hit" and the
  damage type beneath; Unarmed Strike last. **Subclass** from level 3;
  cantrips have no Prepared box
- **Extra damage of magic weapons**: a magic item's Extra Damage (Sword of
  Wounding: 2d6 necrotic) shows beneath the weapon's damage in its attack row;
  Conditional Extra Damage (Flame Tongue, Slayer) shows as a note, not added.
  The explanations of Attacks and Resources sit behind the ⓘ beside the
  heading; the Resources headings appear only when they have rows
- **Your own order**: drag the ⋮⋮ handle beside an attack or a resource to
  move it (Spell and Unarmed Strike too; a weapon moves with its two-handed and
  thrown lines). Something newly equipped or gained comes first. Resources of
  every kind mix in one list; your own are added, removed and edited under
  "Add, remove or edit resources". Needs Grimoire with `<g-order>`
- **Generic magic weapons** are named after their base (+1 Weapon on a
  Quarterstaff reads +1 Quarterstaff; Weapon of Warning reads Weapon of Warning
  (Quarterstaff)); a weapon's **mastery** shows beneath its name when the class
  has Weapon Mastery (or with the Weapon Master feat)
- **Attacks list**, feats, and a catalogue of classes, subclasses, species,
  backgrounds, feats
  and spells
- **Custom class, species, or background** — type a homebrew name when the
  catalogue entry is missing (or you prefer not to pick one)
- **Picking a class** adds its level 1 features, and **picking a subclass** adds
  the features it grants at the level it is chosen
- **Your character's art, large** on the Story page, beside their
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
