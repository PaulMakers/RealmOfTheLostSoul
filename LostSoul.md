# 🎮 Lost Soul — Master Game Bible v1.0

**Status:** Design locked at 100% completion

**Last Updated:** September 2026

**Developers:** PaulMaker + Team (2 devs, no deadline)

**Platform:** Roblox

**Target Players:** 1000 concurrent

---

## 📖 TABLE OF CONTENTS

1. [GAME OVERVIEW](https://claude.ai/chat/ee01c2bb-a9e7-4e42-9020-0f8fb5ace025#overview)
2. [CORE DESIGN PILLARS](https://claude.ai/chat/ee01c2bb-a9e7-4e42-9020-0f8fb5ace025#core-design)
3. [PROGRESSION SYSTEM](https://claude.ai/chat/ee01c2bb-a9e7-4e42-9020-0f8fb5ace025#progression)
4. [COMBAT & STATS](https://claude.ai/chat/ee01c2bb-a9e7-4e42-9020-0f8fb5ace025#combat)
5. [SKILL & ELEMENT SYSTEM](https://claude.ai/chat/ee01c2bb-a9e7-4e42-9020-0f8fb5ace025#skills)
6. [PATH SYSTEM](https://claude.ai/chat/ee01c2bb-a9e7-4e42-9020-0f8fb5ace025#paths)
7. [WORLD & GEOGRAPHY](https://claude.ai/chat/ee01c2bb-a9e7-4e42-9020-0f8fb5ace025#world)
8. [MAP STRUCTURE](https://claude.ai/chat/ee01c2bb-a9e7-4e42-9020-0f8fb5ace025#maps)
9. [ZONES & CONTENT](https://claude.ai/chat/ee01c2bb-a9e7-4e42-9020-0f8fb5ace025#zones)
10. [MONSTER SYSTEM](https://claude.ai/chat/ee01c2bb-a9e7-4e42-9020-0f8fb5ace025#monsters)
11. [DUNGEON SYSTEM](https://claude.ai/chat/ee01c2bb-a9e7-4e42-9020-0f8fb5ace025#dungeon)
12. [PvP & CRIMINAL SYSTEM](https://claude.ai/chat/ee01c2bb-a9e7-4e42-9020-0f8fb5ace025#pvp)
13. [QUEST SYSTEM](https://claude.ai/chat/ee01c2bb-a9e7-4e42-9020-0f8fb5ace025#quests)
14. [ECONOMY](https://claude.ai/chat/ee01c2bb-a9e7-4e42-9020-0f8fb5ace025#economy)
15. [GATHERING & CRAFTING](https://claude.ai/chat/ee01c2bb-a9e7-4e42-9020-0f8fb5ace025#gathering)
16. [GUILD SYSTEM](https://claude.ai/chat/ee01c2bb-a9e7-4e42-9020-0f8fb5ace025#guilds)
17. [NPC FRAMEWORK](https://claude.ai/chat/ee01c2bb-a9e7-4e42-9020-0f8fb5ace025#npcs)
18. [LORE & STORY](https://claude.ai/chat/ee01c2bb-a9e7-4e42-9020-0f8fb5ace025#lore)
19. [TECHNICAL NOTES](https://claude.ai/chat/ee01c2bb-a9e7-4e42-9020-0f8fb5ace025#technical)
20. [DEVELOPMENT CHECKLIST](https://claude.ai/chat/ee01c2bb-a9e7-4e42-9020-0f8fb5ace025#checklist)

---

# 🎯 OVERVIEW

**Genre:** Adventure Fantasy RPG (Isekai-inspired)

**World:** Open-world fantasy with safe zones (cities) and dangerous areas (hunting grounds, dungeons)

**Core Experience:** Exploration + Combat + Dungeon Crawling + Sandbox Progression

**Unique Hook:** No fixed classes — player builds identity through **Race + Stats + Weapon + Element + Skill + Path + Playstyle**

## Game Pillars

1. **Freedom** — No one "right" build; player defines their character
2. **Discovery** — Explore world, find hidden paths, uncover lore
3. **Progression** — Level up, learn skills, grow stronger at own pace
4. **Community** — PvP, trading, guilds, player-driven quests
5. **Mystery** — System origin is unknown; players gradually discover truth

## Target Player

- **Age:** 13+
- **Experience:** Casual to mid-core gamers
- **Interest:** Isekai anime fans, RPG enthusiasts, sandbox players
- **Session:** 30 min to 3+ hours

---

# 🏛️ CORE DESIGN PILLARS

### Isekai Inspiration

- Player in a game-like fantasy world where Level, Skill Books, Dungeons are normal
- System exists but **no one knows who created it** (mystery to uncover)
- Three distinct races, old conflicts, player chooses side or stays neutral

### Hybrid Gameplay

- **Combat:** Action-based (not turn-based)
- **Exploration:** Open-world zones, hidden areas, dungeons
- **Progression:** Non-linear; flexible paths based on playstyle
- **Sandbox:** Economy, guilds, player quests, community-driven content

### No Class System

- Race gives starting stats and elemental affinity, not playstyle restriction
- **Playstyle = Race + Stats Allocation + Weapon Choice + Element Choice + Path Evolution**
- Example: STR+Sword+Fire = Flame Swordsman; INT+Staff+Fire = Battle Mage (same element, different identity)

### Game-World Integration

- Masyarakat dalam game memahami Level, Dungeon, Skill Book sebagai normal
- **Tidak ada yang tahu siapa yang membuat System** — ini menjadi salah satu misteri besar

---

# 📊 PROGRESSION SYSTEM

## Level & Experience

- **Max Level:** 150
- **EXP Formula:** `EXP_to_next = 100 × level^1.8` (rounded) 
  - Early levels (1-15): Fast progression (\~1 hour per level)
  - Mid levels (15-75): Moderate grind (\~2-3 hours per level)
  - Late levels (75-150): Heavy grind (\~5-10+ hours per level)

**EXP per Kill (previously undefined — the pacing claims above can't be checked without this):**

```text
EXP per kill = Enemy_Level × 15
```

**Validation against the pacing targets above:**

| Transition EXP Needed Farming Rank EXP/hr (kills/hr × EXP/kill) Time      |       |                               |                     |          |
| ------------------------------------------------------------------------- | ----- | ----------------------------- | ------------------- | -------- |
| Lv 1 → 2                                                                  | 100   | E (Lv1 enemies, 60 kills/hr)  | 60 × 15 = 900/hr    | \~7 min  |
| Lv 5 → 6                                                                  | 1,540 | E (Lv5 enemies, 60 kills/hr)  | 60 × 75 = 4,500/hr  | \~21 min |
| Lv 10 → 11                                                                | 6,300 | D (Lv10 enemies, 50 kills/hr) | 50 × 150 = 7,500/hr | \~50 min |

This roughly holds up the "\~1 hour per level" claim for levels 1-15 — but it's a first-pass constant (K=15), not a guarantee. Treat it as the tuning lever: raise it if leveling feels too slow in playtesting, lower it if too fast. The Mid/Late-game hour estimates above haven't been validated the same way yet (they involve players splitting time between farming, dungeons, and quests, which this simple formula doesn't capture) — worth a follow-up pass once Quest EXP rewards are defined.

## Seven Main Stats

| Stat Function Formula    |                                   |                                                                         |
| ------------------------ | --------------------------------- | ----------------------------------------------------------------------- |
| **STR**                  | Physical damage, carry weight     | Physical ATK = Base + (STR × 2)                                         |
| **VIT**                  | Max HP, physical defense          | Max HP = Base + (VIT × 10)                                              |
| **INT**                  | Magic/elemental damage, max MP    | Magic ATK = Base + (INT × 2), Max MP = Base + (INT × 5)                 |
| **MND**                  | Magic defense, healing power      | Magic DEF = Base + (MND × 1.5), Healing = Base + (MND × 2%)             |
| **AGI**                  | Attack speed, move speed          | ATK Speed = Base + (AGI × 0.5%), Move Speed = Base + (AGI × 0.3%)       |
| **DEX**                  | Accuracy, critical rate           | Accuracy = Base + (DEX × 1%), Crit Rate = Base + (DEX × 0.2%)           |
| **LUK**                  | Rare drop rate, crit damage bonus | Crit Damage = Base + (LUK × 0.3%), Skill Book Drop = 1% + (LUK × 0.05%) |

## Starting Stats (Budget 70 per race)

| Stat Human Demon Elf     |    |    |    |
| ------------------------ | -- | -- | -- |
| STR                      | 10 | 13 | 7  |
| VIT                      | 10 | 11 | 9  |
| INT                      | 10 | 12 | 10 |
| MND                      | 12 | 8  | 10 |
| AGI                      | 9  | 9  | 12 |
| DEX                      | 10 | 8  | 12 |
| LUK                      | 9  | 9  | 10 |

## Stat Allocation on Level Up

- **Automatic Base Growth:** +1 per stat at level up (race-dependent variations possible)
- **Free Points:** `Level / 2` points per level to allocate manually
- **Hybrid System:** Player gets automatic baseline + can customize with free points

## Soft Cap (Diminishing Returns)

Berlaku berdasarkan **total poin yang dialokasikan ke satu stat**, bukan dari level:

| Points Allocated Effectiveness   |      |
| -------------------------------- | ---- |
| 0–50                             | 100% |
| 51–100                           | 70%  |
| 101+                             | 40%  |

**Purpose:** Encourages hybrid builds while allowing full specialization

---

# ⚔️ COMBAT & STATS

## Combat Style

**Action-based (not turn-based)**

- Player controls character movement + attacks in real-time
- Skills require button press (keybind or UI click)
- Cooldowns apply to each skill individually
- Damage calculated from Attacker's stats vs Defender's defense

## Damage Calculation (Basic)

```text
Physical Damage = (Base ATK + STR × 2 + Weapon Bonus) × (1 − Enemy_DEF% / 100)
Magic Damage = (Base Magic ATK + INT × 2 + Weapon Bonus) × (1 − Enemy_Magic_DEF% / 100)
Healing = (Base Heal + MND × 2%) × Healing Modifiers
```

> **Fixed:** `(100 - Enemy DEF%)` treated DEF as a raw number instead of a fraction — a monster with 50% DEF would have multiplied damage by 50 instead of cutting it in half. Now expressed as a proper 0–1 mitigation multiplier.

## Elemental Damage

- Physical attacks can be modified by equipped element
- Magic attacks are pure elemental
- Example: Sword + Fire element = Physical damage + Fire bonus

---

# 🔥 SKILL & ELEMENT SYSTEM

## Six Elements

### 🔥 Fire (Destruktif, Reborn from Ashes)

- Lv 1-2: Single-target damage (Fireball, Flame Lance)
- Lv 3-4: Damage + status effect (Burning Touch, Cinder Step)
- Lv 5-6: Small AoE (Fire Wave, Flame Circle)
- Lv 7-8: Large AoE (Meteor Drop, Inferno Dash)
- Lv 9: Heavy debuff (Scorch Curse)
- Lv 10: **Ultimate: Phoenix Blaze** — Large AoE + self-heal from damage dealt

### 💧 Water (Kontrol, CC)

- Lv 1-2: Single damage (Water Jet, Aqua Spike)
- Lv 3-4: Damage + slow (Frost Touch, Ripple Dash)
- Lv 5-6: Small AoE (Wave Slash, Whirlpool pull)
- Lv 7-8: Large AoE (Tidal Surge, Ice Dash)
- Lv 9: Heavy debuff (Frozen Curse)
- Lv 10: **Ultimate: Tsunami Requiem** — Massive AoE + lingering slow field

### 🌱 Earth (Pertahanan, Natural fit Elf)

- Lv 1-2: Single damage (Stone Throw, Rock Lance)
- Lv 3-4: Damage + root (Mud Grasp, Earthen Step)
- Lv 5-6: Small AoE (Stone Spikes, Quake Pulse)
- Lv 7-8: Large AoE (Boulder Fall, Tremor Charge)
- Lv 9: Heavy debuff (Petrify Curse)
- Lv 10: **Ultimate: Gaia's Wrath** — Large AoE + defensive barrier for party

### 🌪️ Wind (Kecepatan, Kebebasan)

- Lv 1-2: Single damage (Gust Slash, Wind Blade multi-hit)
- Lv 3-4: Damage + blind (Piercing Gale, Tailwind Step haste)
- Lv 5-6: Small AoE (Cyclone Slash, Vortex pull)
- Lv 7-8: Large AoE (Storm Surge, Gale Dash multi-hit)
- Lv 9: Heavy debuff (Silence Gale)
- Lv 10: **Ultimate: Tempest's Roar** — Large AoE + party haste buff

### ✨ Light (Human Exclusive, Recovery)

- 10 skills fokus healing/support
- Lv 1-2: Single heal (Heal, Cure)
- Lv 3-4: Heal + utility (Blessing Touch shield, Radiant Step party heal)
- Lv 5-6: AoE heal (Sanctuary Circle HoT, Purify Wave cleanse)
- Lv 7-8: Strong shield (Guardian Light, Resurrection Pulse)
- Lv 9: Party defense (Divine Barrier)
- Lv 10: **Ultimate: Aegis of the Radiant** — Massive heal + party shield + debuff immunity

### 🌑 Dark (Demon Exclusive, 5 Recovery + 5 Attack)

- **Attack Skills:** Shadow Bolt, Abyssal Slash, Void Strike, Nightmare Wave, Void Reaper
- **Recovery Skills:** Dark Absorb, Shadow Mend, Blood Pact, Soul Siphon, Abyssal Communion
- **Trade-off:** Damage +15% potency vs Light/Basic elements; Recovery costs additional HP (\~3% Max HP per cast)

## Skill Book System

- **Drop Source:** Monster Rank C and above (1% base chance, increased by LUK)
- **Learning:** Must learn sequentially per element (must have Lv 1-4 before learning Lv 5)
- **Rarity Progression:**

| Monster Rank Skill Book Level Rarity | | | |
| ------------------------------------ | ------------- | --------- | --- |
| E                                    | N/A (no drop) | —         |     |
| D                                    | Lv 1-3        | Common    |     |
| C                                    | Lv 4-6        | Uncommon  |     |
| B                                    | Lv 7-8        | Rare      |     |
| A                                    | Lv 9          | Epic      |     |
| S                                    | Lv 10         | Legendary |     |

> **Note:** LUK affects two separate systems with two separate rates on purpose — Skill Book drop chance here (+0.05%/LUK) and gold-per-kill in the Economy Balancing doc (+0.1%/LUK). They're not meant to match; flagging only so no one "fixes" one to match the other later.

---

# 🛤️ PATH SYSTEM

## What is a Path?

Path bukan class tradisional. Path adalah **identitas + arah perkembangan** berdasarkan bagaimana pemain bermain.

## 10 Starting Paths (Level 15 Recommendation)

| Path Stat Focus Weapon Identity     |                |               |                                    |
| ----------------------------------- | -------------- | -------------- | ---------------------------------- |
| **Swordsman**                       | STR + DEX      | Sword          | Balanced melee, damage + precision |
| **Knight**                          | VIT + STR      | Sword + Shield | Tank, survivability high           |
| **Berserker**                       | STR            | Great Axe      | Glass cannon, massive damage       |
| **Spearman**                        | STR + AGI      | Spear/Polearm  | Mid-range melee, mobile            |
| **Archer**                          | DEX + AGI      | Bow            | Ranged physical, precision         |
| **Assassin**                        | AGI + DEX      | Dagger         | Burst + evasion, fragile           |
| **Mage**                            | INT            | Staff          | Elemental ranged, pure magic       |
| **Spellblade**                      | STR/INT hybrid | Sword + Element| Melee + magic hybrid               |
| **Priest**                          | MND            | Wand           | Recovery/support, low damage       |
| **Explorer**                        | LUK            | Any            | Loot specialist, utility           |

## Path Passives (Examples)

- **Swordsman:** +Physical damage with Sword, +Accuracy
- **Knight:** +Defense with Shield, damage reduction when HP low
- **Berserker:** +Damage as HP decreases, -Defense
- **Archer:** +Attack speed ranged, +Crit when target unaware
- **Assassin:** +Movement speed out of combat, +Backstab damage
- **Mage:** +Elemental damage, -MP cost for elemental skills
- **Priest:** +Healing effectiveness, +MP regen
- **Explorer:** +Rare drop rate, +Movement speed in exploration, wider detection

## Path Evolution (Level 20+)

Tiap path awal bisa evolve ke 2 arah, tergantung stat emphasis:

| Path Awal Evolve A Evolve B    |                             |                                  |
| ------------------------------ | --------------------------- | -------------------------------- |
| Swordsman                      | **Blademaster** (STR)       | **Duelist** (DEX)                |
| Knight                         | **Guardian** (VIT)          | **Paladin** (VIT+MND)            |
| Berserker                      | **Juggernaut** (STR+VIT)    | **Warlord** (leadership)         |
| Spearman                       | **Dragoon** (STR burst)     | **Lancer** (AGI mobile)          |
| Archer                         | **Sniper** (DEX precision)  | **Ranger** (AGI mobile)          |
| Assassin                       | **Shadow Blade** (stealth)  | **Poison Blade** (DEX+INT DoT)   |
| Mage                           | **Elementalist** (INT pure) | **Sorcerer** (INT+MND CC)        |
| Spellblade                     | **Battlemage** (balanced)   | **Runeblade** (debuff)           |
| Priest                         | **Bishop** (pure heal)      | **Exorcist** (MND+INT offensive) |
| Explorer                       | **Treasure Hunter** (loot)  | **Trickster** (AGI evasion)      |

## Hidden Paths

- **Ancient Swordmaster** → Find Ancient Sword artifact + high STR
- **Dragon Slayer** → Solo-kill 1 S-Rank dragon monster
- **Archsage** → Master all 4 basic elements at Lv 10
- **Voidwalker** → Find hidden location related to System origin
- **Twilight Reaper** → Dark element + high PvP kills
- **Saint of Light** → Light element Lv 10 + special NPC quest

## Multiple Paths

Player dapat memiliki lebih dari satu Path sekaligus:

- Swordsman Lv 20 + Mage Lv 10 + Explorer Lv 8 (semuanya aktif)
- Switching primary Path anytime tanpa penalty
- Path lama tidak hilang, bisa developed later

## Path EXP

Path berkembang naturally melalui:

- **Activity:** Menggunakan weapon/skill yang sesuai path
- **Quest:** Quest yang relevant untuk path
- **Achievement:** Milestone tertentu
- **Hidden Condition:** Rahasia lainnya

Pemain tidak grind "Path EXP" secara eksplisit — semua organic.

---

# 🌍 WORLD & GEOGRAPHY

## Three Races

### 👤 Human

- **Territory:** Kingdom, structured monarki/council
- **City:** Human City (safe zone)
- **Element Access:** Light (recovery-focused)
- **Characteristic:** Balanced starting stats, +5% bonus EXP from quests
- **Dungeon:** Human Dungeon (ancient ruins theme)

### 👹 Demon

- **Territory:** War-like, rule by strength (strongest leads)
- **City:** Demon City (safe zone)
- **Element Access:** Dark (5 recovery + 5 attack skills, +15% potency, -HP cost)
- **Characteristic:** High STR/INT, low MND/DEX; Berserk trait (below 30% HP: +10% damage, -10% defense)
- **Dungeon:** Demon Dungeon (abyssal chambers theme)

### 🧝 Elf

- **Territory:** Elder-led, peaceful, nature-connected
- **City:** Elf City (safe zone, separate dimension via World Tree)
- **Element Access:** Earth (nature defense), all basic elements
- **Characteristic:** High AGI/DEX, low STR; Nature's Kin trait (+20% HP/MP regen in forest, fast World Tree access)
- **Dungeon:** Elf Dungeon (crystalline caverns theme)
- **Hunting Ground:** Separate Elf Hunting Ground in their dimension

## World Conflicts

- **Human vs Demon:** Centuries-old conflict over resources, Skill Books, power
- **Current Status:** Cold War (no open war, but skirmishes, sabotage, PvP at Central Hunting Ground)
- **Elf Role:** Neutral; occasional trade/alliance but independent

---

# 🗺️ MAP STRUCTURE & ZONES

## 8 Total Maps (Separate Roblox files for performance)

### Maps 1-3: Cities (Safe Zones)

#### MAP 1: HUMAN CITY

**Size:** Medium (10-20 min walk)

**Theme:** Medieval fantasy, organized, structured

**Safe Zone:** YES

**Zones:**

- Central Plaza (hub, orientation)
- Residential District (inn, blacksmith, armorer)
- Adventurer Guild (quest hub, **dungeon entrance basement**)
- Market District (shops, player stalls, trading)
- Temple District (light element story)
- Gathering Hub (buy tools)

**NPCs:** \~12 total

#### MAP 2: DEMON CITY

**Size:** Medium (10-20 min walk)

**Theme:** Medieval fantasy, aggressive, dark

**Safe Zone:** YES

**Zones:**

- War Plaza (hub, duel arena)
- Barracks District (weapons, armor)
- Demon Guild Hall (quest hub, **dungeon entrance basement**)
- Dark Market (shops, trading)
- Shadow Temple (dark element story)
- Gathering Hub (buy tools)

**NPCs:** \~12 total

#### MAP 4: ELF CITY (WORLD TREE DIMENSION)

**Size:** Medium (10-20 min walk)

**Theme:** Medieval fantasy, naturalistic, ethereal

**Safe Zone:** YES

**Access:** World Tree portal (Elf only)

**Zones:**

- World Tree Hub (central, lore)
- Residential District (inn, elf crafts)
- Elf Guild Hall (quest hub, **dungeon entrance basement**)
- Forest Market (shops, smaller than human/demon)
- Nature Temple (earth element story)
- Gathering Hub (buy tools, +20% gathering bonus)

**NPCs:** \~12 total

### Maps 5-6: Hunting Grounds (PvP Enabled)

#### MAP 3: CENTRAL HUNTING GROUND

**Size:** Large (exploration-heavy)

**Theme:** Wilderness, contested territory

**Safe Zone:** NO (PvP enabled)

**Access:** Portals from Human City + Demon City

**Zones:**

- **Hunter's Outpost** (hub, neutral zone, supply NPC)
- **Forest Zone Beginner** (East, Rank E-D monsters, common resources)
- **Forest Zone Intermediate** (Central, Rank D-C, uncommon resources, **PvP hotspot**)
- **Highland Zone Advanced** (West, Rank C-B, rare resources, **PvP hotspot**)
- **Ancient Ruins** (Hidden North, Rank B-A, rare drops, hidden path triggers)
- **Safe Rest Area** (emergency healer, quick portal to outpost)

#### MAP 5: ELF HUNTING GROUND

**Size:** Large (exploration-heavy)

**Theme:** Pristine wilderness, peaceful but dangerous

**Safe Zone:** NO (PvP enabled, primarily Elf territory)

**Access:** Portal from Elf City only

**Zones:**

- **Forest Sanctuary** (hub, ranger NPC)
- **Emerald Forest** (South, Rank E-D, plant materials)
- **Twilight Thicket** (Central, Rank D-C, uncommon materials, moderate PvP)
- **Ancient Grove** (North, Rank C-B, earth-element focus, **PvP hotspot**)
- **Secret Glade** (Hidden, Rank A, legendary drops, hidden path)
- **Recovery Grove** (emergency healer, quick portal)

### Maps 6-8: Dungeons (Instance/Separate)

#### MAP 6: HUMAN DUNGEON

**Entrance:** Adventurer Guild basement (Human City)

**Floors:** 1-100

**Theme:** Ancient ruins, magical chambers

#### MAP 7: DEMON DUNGEON

**Entrance:** Demon Guild Hall basement (Demon City)

**Floors:** 1-100

**Theme:** Abyssal chambers, dark energy

#### MAP 8: ELF DUNGEON

**Entrance:** Elf Guild basement (Elf City)

**Floors:** 1-100

**Theme:** Crystalline caverns, nature-infused

---

# 👹 MONSTER SYSTEM

## Monster Ranks

| Rank Examples Level Range    |                                                                      |           |
| ---------------------------- | -------------------------------------------------------------------- | --------- |
| E                            | Slime, Goblin, Kobold, Magic Wolf, Horn Rabbit                       | Lv 1-10   |
| D                            | Orc, Golem, Giant Spider, Skeleton Warrior, Rock Turtle              | Lv 10-25  |
| C                            | Wyvern, Ogre, Silver Wolf, Hobgoblin, Slime King                     | Lv 25-45  |
| B                            | King Goblin, General Ogre, Emerald Wolf, General Wyvern              | Lv 45-70  |
| A                            | King Wyvern, Hellhound/Cerberus, Wraith/King Skeleton, Mithril Golem | Lv 70-100 |
| S                            | Ancient Dragon, Behemoth, Arch Salamander, Fenrir Lord, Arch Lich    | Lv 100+   |

## Monster Spawning

- **Respawn Time:** 30-60 seconds per monster (varies by difficulty)
- **Density:** 5-15 monsters per zone (depends on zone size & tier)
- **Dynamic Respawn:** Based on kill rate (fewer kills = more spawns; farm hotspot = constant flow)
- **Level Scaling:** Monster level = zone baseline (can scale up if high-level player in zone)

## Monster Drops

### Common/Fixed Drop

- Every monster drops 1 common item (e.g., Wolf → Fang/Hide)
- Gold: `100 × Monster Level` (base, modified by player's MND for bonus)

### Rare Drop (Rank D+)

- **Base Rate:** 5% (before LUK modifier)
- **With LUK Bonus:** +0.05% per LUK stat
- **Examples:** Magic Sword, Ring, Special Material
- **Rarity Tiers:** Common, Uncommon, Rare, Epic, Legendary

### Skill Book Drop (Rank C+)

- **Base Rate:** 1% (modified by LUK)
- **Rarity:** Tied to Monster Rank 
  - C → Lv 4-6 Skill Book
  - B → Lv 7-8 Skill Book
  - A → Lv 9 Skill Book
  - S → Lv 10 Skill Book (guaranteed on S-rank)

---

# 🏰 DUNGEON SYSTEM

## 100-Floor Structure (per race)

### Progression Tiers

**Floors 1-20 (Beginner)**

- Monsters: Rank E-D
- Boss every 10 floors: Rank E boss
- Loot: Common-Uncommon Skill Books (Lv 1-3)
- Difficulty: Easy

**Floors 21-50 (Intermediate)**

- Monsters: Rank D-C
- Boss every 10 floors: Rank D/C boss
- Loot: Uncommon-Rare Skill Books (Lv 4-6)
- Difficulty: Moderate

**Floors 51-80 (Advanced)**

- Monsters: Rank C-B
- Boss every 10 floors: Rank C/B boss
- Loot: Rare-Epic Skill Books (Lv 7-8)
- Difficulty: Hard

**Floors 81-99 (Endgame)**

- Monsters: Rank B-A
- Boss every 5 floors: Rank B/A boss
- Loot: Epic-Legendary Skill Books (Lv 9)
- Difficulty: Very Hard

**Floor 100 (Final Chamber)**

- **Core Location:** Central chamber (lore: ancient energy core)
- **Final Boss:** Ancient Guardian (S-Rank equivalent)
- **Guaranteed Loot:** Legendary Skill Book (Lv 10) + special artifact
- **Core:** Static/immune, cannot be damaged; must defeat guardian to complete dungeon

## Boss Mechanics

**Loot Guarantee:** every boss (floors 10-95) drops 100% rare-tier loot + a Skill Book at the rarity tier matching its floor range (per the Skill Book System table). This is also where Crafting Blueprints drop (see the Crafting System's "Unique Recipes from Boss Drops").

### Stat Scaling (replaces the old vague "2-3x")

```text
Boss Stats = Regular_Monster_Stats_at_that_Rank × Tier_Multiplier

Floor bosses (every 10, floors 10-80):        ×2.0
Endgame floor bosses (floors 85, 90, 95):     ×2.5
Floor 100 Ancient Guardian:                   ×3.0 + unique kit (below)
```

### Special Attack Pool (shared tags, not 36 hand-written bosses)

With 12 boss floors × 3 race dungeons = 36 bosses, hand-authoring a unique kit for each isn't a good use of a 2-person team. Instead, every boss rolls **2 tags** from a shared pool at design time; the pool is what makes bosses feel distinct, not bespoke per-boss writing:

| Tag Effect            |                                                                    |
| --------------------- | ------------------------------------------------------------------ |
| Telegraphed AoE       | Large-radius attack with a 1.5s wind-up (visibly dodgeable)        |
| Enrage                | Below 30% HP: +30% attack speed, -10% defense                      |
| Summon Adds           | Spawns 2-4 regular monsters of that floor's rank                   |
| Reflect Phase         | For 5s, reflects 20% of damage taken back at attacker              |
| Knockback Slam        | Melee hit knocks back + brief stun                                 |
| Elemental Debuff Zone | Ground zone applying Burn/Slow/Root/Blind (per the boss's element) |

**Race theming (which tags lean more common per dungeon, not exclusive):** Human Dungeon bosses lean Telegraphed AoE + Summon Adds (structured, methodical); Demon Dungeon bosses lean Enrage + Reflect Phase (aggressive, punishing); Elf Dungeon bosses lean Elemental Debuff Zone + Knockback Slam (control-oriented). Same 6 tags everywhere — reskinned per dungeon theme (ancient ruins / abyssal chambers / crystalline caverns) rather than requiring separate mechanical design per race.

### Phase Mechanic (made concrete)

- **Floors 10-30:** single phase, no HP-based transition (keeps early bosses approachable).
- **Floors 40+:** mandatory Phase 2 at 50% HP — a 5-second telegraphed transition, then a 3rd special-attack tag becomes active for the rest of the fight.
- **Floor 100 Ancient Guardian only:** Phase 3 at 20% HP adds a **7-minute soft enrage timer** (+50% all boss stats if the fight runs long) — this is a deliberate anti-kiting/anti-farm-lock safeguard given 1000 concurrent players will be sharing dungeon server capacity.

### Named Boss Roster

Reuses the monster names already defined in the Monster Ranks table — bosses are buffed, named variants of existing monsters (e.g. "Goblin Chieftain" = boss Goblin), not new creatures to design from scratch. Same roster structure applies to all 3 race dungeons, reskinned per theme.

| Floor Rank Base Monster Boss Title (example)     |            |                    |                                  |
| ------------------------------------------------ | ---------- | ------------------ | -------------------------------- |
| 10                                               | E          | Goblin             | Goblin Chieftain                 |
| 20                                               | D          | Orc                | Orc Warlord                      |
| 30                                               | D          | Skeleton Warrior   | Bonelord                         |
| 40                                               | C          | Wyvern             | Wyvern Alpha                     |
| 50                                               | C          | Slime King         | Slime Sovereign                  |
| 60                                               | C          | Hobgoblin          | Hobgoblin Warchief               |
| 70                                               | B          | King Goblin        | Goblin Emperor                   |
| 80                                               | B          | General Wyvern     | Wyvern Marshal                   |
| 85                                               | B          | General Ogre       | Ogre Overlord                    |
| 90                                               | A          | King Wyvern        | Wyvern Tyrant                    |
| 95                                               | A          | Hellhound/Cerberus | Cerberus Alpha                   |
| 100                                              | S (unique) | —                  | **Ancient Guardian** (see below) |

**Ancient Guardian (Floor 100, one unique variant per race):** ties directly into the Dungeon Core lore and reuses each race's own Element Lv 10 ultimate for its signature attack, rather than inventing a new ability:

- **Human Dungeon:** Light-attuned Guardian — signature attack mirrors *Aegis of the Radiant* (massive heal-nullify pulse forcing players to burst it down before it stabilizes).
- **Demon Dungeon:** Dark-attuned Guardian — signature attack mirrors *Void Reaper*-style burst damage with self-sustain via the standard Dark element's HP-cost recovery trade-off.
- **Elf Dungeon:** Earth-attuned Guardian — signature attack mirrors *Gaia's Wrath* (party-wide AoE + damage barrier for itself, forcing a burst-through-the-shield check).

## Dungeon Floor Randomization

With 100 floors × 3 dungeons, hand-designing every floor's layout isn't realistic for a 2-dev team — so only **boss floors are fixed** (hand-built arenas, for fairness and clear telegraphing); every other floor is assembled from a room-template pool.

**Generation process (per floor, non-boss):**

```text
1. Pick 4-8 room templates from that tier's template pool (Beginner/Intermediate/Advanced/Endgame — same 4 tiers as Progression Tiers above)
2. Connect them with corridor pieces in a randomized but always-solvable order (linear chain, no dead-end-only branches)
3. Populate each room with monsters per the existing Monster Spawning density (5-15/zone, scaled to floor tier)
4. Roll for a Treasure Room (5% chance): bonus loot chest, no combat
5. Roll for a Trap Room (10% chance): hazard (e.g. Fire/Water/Earth/Wind zone matching the dungeon's flavor) but +bonus material reward if survived
```

- **Seed scope:** generated once per party when they enter that floor, shared across the whole party — everyone in the group sees the same layout (required for an MMO; per-player-unique layouts would break shared combat/loot).
- **Boss floors:** always the same hand-built arena for a given boss — randomization only applies to the 8-9 regular floors between each boss floor.

**Floor Modifiers (optional replay variety, rolled per floor per run):**

| Modifier Effect   |                                 |
| ----------------- | ------------------------------- |
| None (default)   | Baseline difficulty/reward      |
| Elite Swarm       | +50% monster density, +30% loot |
| Blessing          | -20% monster HP, -10% loot      |

This gives floors replay variety without hand-authoring 100 unique layouts, and gives players a light risk/reward choice each run (accept the roll, or leave and re-enter to reroll).

## Lore: Dungeon Core

- **Core exists** on Floor 100 (one per race)
- **Core is ancient** → pre-dates known civilization
- **Core emits System energy** → fills dungeon monsters with power
- **Skill Books are Core energy crystallized** into knowledge
- **Unknown who made Cores** → central mystery of Lost Soul

---

# ⚔️ PvP & CRIMINAL SYSTEM

## PvP Rules

- **Wilderness/Hunting Ground:** FREE PvP (can attack anyone)
- **City/Safe Zone:** NO PvP (except duels, which are consensual)
- **Duel:** Available at arena NPC in cities, both players must agree

## PvP Death Mechanics

**Item Loss:**

- Equipped items have chance to drop (5-50% per item, based on rarity)
- Locked items NEVER drop (need Lock Stone/Lock Core to lock)
- Dropped items can be looted for **5 minutes**, then disappear

**Respawn Location:**

- Respawn at own race's city (human → Human City, demon → Demon City, elf → Elf City)

## Criminal Status

Obtained by:

- Killing unaware player (PvP murder)
- Stealing (if implemented)
- PvP abuse/griefing flagging

**Criminal Indicators:**

- Red name (instead of white)
- Skull icon above head

**City Behavior:**

- Criminal CAN enter city (not banished)
- Criminal CANNOT initiate normal PvP in city (status visible)
- Criminal CAN participate in duels (with opponent consent)
- Guard will NOT auto-attack criminal (unless actively attacking)

## Criminal Rehabilitation

**Process:**

1. Get Criminal status
2. Quest Rehabilitasi appears from System
3. Complete quest → status removed immediately
4. Repeat crimes → Criminal Level increases (more difficult quest, higher debuffs)

**Debuffs (by Criminal Level):**

- Lv 1: Minor debuff (-5% all stats, 1 hour)
- Lv 2: Moderate (-10% all stats, 2 hours)
- Lv 3: Severe (-15% all stats, 4 hours)
- Lv 4+: Very Severe (-20% all stats, quest only, access restriction)

**Restrictions:**

- Cannot join certain guilds
- Cannot access certain quests
- Movement speed reduced

## Bounty System

**Who Can Create Bounty:**

- System (auto for criminals)
- NPC/Guild
- Player (post bounty on criminal, set reward)

**Bounty Mechanics:**

- Any player can become bounty hunter
- Kill target → reward: Gold + EXP
- Reward calculated: `(Target Level × 100) + (Victims Count × 500) + (Criminal Level × 1000)`
- **Bounty expires** after 7 days (Criminal Status remains)

---

# 📜 QUEST SYSTEM

## Two Quest Types

### System Quest

- **Main Quest:** Story progression, global narrative
- **Side Quest:** Optional content, story flavor, rewards

### Player-Generated Quest

- Player A needs item (e.g., Horn Rabbit Horn)
- A posts quest to Adventurer Guild
- NPC prices quest: `Item Value + 10% tax`
- Player B accepts & completes
- B gets reward, A pays from inventory or gold

---

# 💰 ECONOMY SYSTEM

## Gold Sources

> **Fixed:** this section previously stated its own gold-per-kill formula (`100 × Monster Level`), which was a *third*, different formula from the one in the Economy Balancing doc — neither of the two matched each other or the Breakdown-by-Rank table there. Rather than maintain two copies that can drift apart again, this section now points to the single corrected formula instead of restating it.

- Monster kills: see **Economy Balancing doc → Gold Sources → Monster Kills** for the formula (rank-based interpolation, now fixed to match its own breakdown table)
- Quests: varies by quest, see Economy Balancing doc → Quest Rewards
- Dungeon: varies by floor, see Economy Balancing doc → Dungeon Rewards
- Trading/selling: player-determined
- Bounties: `(Target Lv × 100) + (Victims_Count × 500) + (Criminal_Level × 1000)` — see Economy Balancing doc → Bounty Rewards for worked examples

## Trading

**Trade Window:**

- All item + gold transfers via Trade Window (no direct transfer)
- Max 20 items per trade
- Lock System: both agree → 3-second countdown → locked in

**Cancellation:**

- Can cancel before lock
- If cancelled after lock → trade fails, items returned
- Disconnect → trade cancelled

**Cross-race Trading:**

- Allowed between all races
- Item exclusivity: no; even if item not usable, can be resold

**Trade History:**

- Logged (account-only view)
- Shows: date, items, gold, both players

## Shops

### NPC Shop

- Buy/sell all items
- Buy price: `(Item Base Price) × Supply/Demand modifier`
- Sell price: **50% of buy price**

### Player Shop

- Located in: Human City, Demon City
- Player sets price (system shows recommendation)
- 10% tax on revenue
- Criminal CANNOT shop here
- All races can visit

### Guild Shop

- Guild can sell items from guild storage
- 5% commission per sale (paid by seller)
- No listing fee
- Item stays listed until sold

### Merchant Guild

- Monthly membership fee: 5000 gold
- Benefits: market info, reduced shop tax (Player Shop 10% → 7%, Guild Shop 5% → 3%), bulk purchase discount (×0.95 cost), access to market data (price trends)
- Rank: based on transaction volume & gold traded

> **Fixed:** this section said "TBD" for the fee and "7% → 5%" for the tax reduction — neither matched the Merchant Guild Benefits section already written in the Economy Balancing doc (5000 gold fee; 10%→7% and 5%→3% for the two shop types separately). Synced to match.

---

# ⛏️ GATHERING & CRAFTING

## Gathering System

**Types:**

- Mining
- Logging
- Herbalism

**Mechanics:**

- Each gathering has own level (Mining Lv 1-50, Logging Lv 1-50, etc.)
- Requires tool (pick, axe, sickle)
- Tools don't degrade
- Rarity: Common, Uncommon, Rare, Epic, Legendary
- **Legendary materials:** NOT from gathering (only from monster drops)

**Respawn:**

- Dynamic based on resource scarcity
- High-loot areas respawn slower
- Low-loot areas respawn faster

**Elf Bonus:**

- +20% gathering efficiency in forest/nature areas

## Crafting System

Crafting turns gathered materials (Mining/Logging/Herbalism) and monster-drop materials (e.g. Leather from Hide) into equipment and consumables. Full recipe examples, material costs, and the crafting-level profit curve live in the **Economy Balancing doc** ("Crafting Recipes & Costs" and "Crafting Progression" sections) — this section covers the two mechanics that live outside pricing: success/failure rate, and how top-tier gear is unlocked.

### Success / Failure Rate

```text
Success Rate = 50% + (Crafter_Level − Recipe_Required_Level) × 2%
Clamped between 10% (hard floor) and 95% (hard ceiling)
```

- Crafting **above** your level is risky but not impossible (10% floor keeps it possible to reach for Rare/Epic gear early, at a steep material-loss cost).
- Crafting **below** your level is close to guaranteed (95% ceiling) — no incentive to "grind trivial recipes" for free successes.
- **On failure:** 50% of materials are consumed (not all) and no item is produced. This keeps failure painful but not run-ending, and gives a soft reason for the Merchant Guild's bulk-purchase discount (see Economy doc) to matter for active crafters.

**Example:** Lv 15 crafter attempting the Iron Sword recipe (Recipe_Required_Level 15): 50% + 0×2% = 50% success. Same crafter at Lv 25: 50% + 10×2% = 70%.

### Equipment vs Consumable Crafting

- **Equipment** (weapons/armor): follows the Crafting Recipes & Costs table in the Economy doc — higher variance, higher profit margin, success rate applies as above.
- **Consumables** (potions): success rate is fixed at 90% regardless of crafter level (low-stakes, high-volume — see Consumable Pricing in the Economy doc for potion cost/profit) so early-game alchemists aren't blocked from reliable income.

### Unique Recipes from Boss Drops

- Dungeon bosses (per the Boss Mechanics section) drop **Blueprints** as part of their guaranteed rare-drop loot table.
- A Blueprint unlocks exactly one recipe for **Unique or Mythic** tier gear — the top rows of the Weapon/Armor pricing curves (60+ Mythic weapons, 100+ Unique/Mythic armor) that otherwise have no crafting path and can only be bought at full NPC price.
- Blueprints are Bind-on-Pickup (cannot be traded) so top-tier crafted gear stays tied to actually killing the boss, not just buying the blueprint off the market — this is a deliberate gold sink and anti-inflation lever alongside the ones in the Economy doc's Inflation Prevention section.

---

# 🏛️ GUILD SYSTEM

**Guild Types:**

- **Adventurer Guild** (main, in each city)
- **Merchant Guild** (economy-focused)
- Custom player guilds (TBD)

**Guild Features:**

- Guild reputation (separate from player reputation)
- Guild shop
- Guild quests
- Guild wars/PvP (optional)
- Guild bank (shared storage)

---

# 🧙 NPC FRAMEWORK

## NPC Categories

### Utility NPCs

- Innkeeper (rest/healing)
- Blacksmith (weapon upgrade)
- Armorer (gear)
- Merchant (buy/sell)
- Tool Merchant (gathering tools)

### Quest NPCs

- Guild Master
- Quest Board NPC
- Reward Officer
- Quest Giver NPCs (unique, per city/zone)

### Lore/Story NPCs

- City Guard Captain
- Town Crier
- Priest/Cleric (Light element)
- Dark Element Trainer
- Druid (Earth element)
- Elf Elder

### Flavor NPCs

- Various city NPCs (blacksmith apprentice, merchant guards, etc.)

## NPC Dialogue Structure

**Fully detailed in a companion document:** **`Lost_Soul_NPC_Dialogue_Quest_Text.md`**

Covers:

- Dialogue tree notation + the 5-state quest logic (Locked → Available → In Progress → Ready to Turn In → Completed)
- Personality Tag framework (8 tags) so \~36 named NPCs feel distinct without needing 36 bespoke voices
- Fully worked dialogue trees for every Utility, Quest, and Lore/Story NPC role, written for Human City with a Race Variation table (§11 of that doc) covering how Demon/Elf City reskin the same structure
- Flavor NPC bark-pool pattern for ambient city NPCs
- Full "Awakening" opening Main Quest chain text (4 quests), Side Quest examples, and the Player-Generated Quest posting/fulfillment scaffolding
- Reputation & Criminal Status dialogue gating, tied to the PvP & Criminal System above

---

# 📖 LORE & STORY

## World Name: Lost Soul

**Etymology:**

- Refers to **peradaban kuno yang telah punah** (ancient civilization that vanished)
- Mereka membuat Dungeon Core, lalu lenyap
- Jiwa/esensi mereka menyatu dengan dunia = sumber energi System
- Setiap level up, Skill Book, Dungeon mastery = memakai sisa kekuatan jiwa-jiwa yang hilang itu

## Three Races & Conflicts

### Human vs Demon

- Centuries-old conflict
- Resource competition
- Currently: Cold War (skirmishes in Central Hunting Ground)
- Player tidak wajib pilih sisi

### Elf Position

- Independent, own dimension
- Occasionally ally with either human/demon
- Neutral in conflict
- Self-sufficient through World Tree

## Central Mystery

**"Who created the System?"**

- System exists as natural part of world
- Everyone knows it, but no one knows origin
- Dungeon Core = hint of System origin, but incomplete
- Hidden paths gradually reveal lore
- True answer: reserved for endgame/expansion content

## Timeline

Three ages, building directly on the Etymology and Central Mystery above. The System's true origin is **not** resolved here on purpose — per Central Mystery, that stays reserved for endgame/expansion content. What follows gives NPCs and quest text something concrete to reference without spoiling it.

### Age of the Lost (Ancient Age)

- A civilization known to history only as **"the Lost"** existed before any recorded human, demon, or elf history — their true name, appearance, and fate are all unknown, even to modern scholars.
- The Lost either created or discovered the System (deliberately unclear — in-world scholars argue both sides, which is exactly the seed for the Central Mystery).
- They built the three **Dungeon Cores** — the same Cores sitting at Floor 100 of the Human, Demon, and Elf Dungeons today. Why each Core happens to sit beneath what later became each race's capital city is itself an open question in-world (a hook the Ancient Ruins hidden zone and the Voidwalker hidden Path can play with).
- The Lost vanished. No war, no ruins showing destruction — just absence. The dominant in-world theory (never confirmed) is that they merged their own souls/essence into the world itself, becoming the passive energy source that now powers Level-ups, Skill Books, and Dungeon mastery — per the Etymology above.
- What remains: the three Dungeon Cores, scattered ruins (the Ancient Ruins zone in Central Hunting Ground), and Skill Books — crystallized fragments of whatever the Lost left behind.

### Age of Settlement (Medieval Age)

- Human and Demon ancestors settle into the world generations after the Lost's disappearance and find the System already active and usable — where they came from before that is left open, consistent with keeping the origin mystery intact.
- **Humans** settle around ruins that become Human City, forming the structured monarchy/council already established — early System use is treated with reverence, close to religious.
- **Demons** settle their own territory and adopt the "rule by strength" culture already established — to them, the System proves that only the strong deserve power.
- **Elves** are already present, independent, tied to the World Tree in their own dimension. Some Elf oral history claims they're the closest living link to the Lost — unconfirmed, but it's why Elves get access to all four basic elements rather than one, and gives the Elf Elder NPC a natural reason to speak carefully about the subject.
- Competition over rare materials, Skill Books, and dungeon access sparks the first Human-Demon skirmishes — the start of the "centuries-old conflict" already established in Three Races & Conflicts.
- Adventurer Guilds (Human) and their Demon-side equivalent are founded in this era specifically to regulate dungeon access and prevent unchecked power grabs from Core-adjacent resources — giving the Guild system an in-world reason to exist beyond "quest hub."

### Modern Day (Cold War Era — present, where the game begins)

- Direct war has cooled into the Cold War already established: skirmishes and sabotage at Central Hunting Ground, no open war.
- The System, Levels, Dungeons, and Skill Books are now completely normalized — nobody alive remembers a world without them, which is precisely why the Central Mystery has gone from urgent to academic. Most people simply don't think to question it, which is what makes the player (a newcomer) uncovering it via Hidden Paths narratively believable rather than "how did nobody else notice this."
- Certain individuals and factions — mirrored by the Hidden Paths already defined (Voidwalker, Archsage, Twilight Reaper, Saint of Light) — actively dig into the truth, for reasons ranging from scholarly curiosity to darker ambitions. This is the natural on-ramp for late-game/expansion story content once the Central Mystery is ready to be partially unveiled.

---

# 💻 TECHNICAL NOTES

## Roblox Architecture (Summary)

### Server Structure

Multiple **Places** (not one giant place) linked via `TeleportService`, matching the "8 separate maps" performance note already in Map Structure:

- **Persistent places:** Human City, Demon City, Elf City, Central Hunting Ground, Elf Hunting Ground — always-on, shared by all players who enter them.
- **Instanced places:** Human/Demon/Elf Dungeons — each party gets a `TeleportService:ReserveServer()` private instance on entry, so dungeon floor state (monsters, loot rolls, floor-randomization seed) never leaks between parties and one party's boss pull doesn't affect another's.
- **Code organization:** `ServerScriptService` split into one ModuleScript per domain — `CombatService`, `EconomyService`, `GuildService`, `DungeonService`, `CraftingService`, `PvPService` — each with a small, explicit public API. With 2 devs working without a deadline, this boundary matters more for long-term maintainability than for launch speed: it lets either dev touch one system without reading the others.

### DataStore (Player Save Data)

- Use a session-locking wrapper (the standard pattern here is **ProfileService**-style: one profile per player, locked to the server session they're on) rather than raw `DataStore:GetAsync/SetAsync` calls — this is what prevents the classic Roblox dupe exploit where a player alt-tabs between two servers while their old session hasn't saved yet.
- **Per-player profile contents:** level/EXP, stat allocation, unlocked Paths + Path EXP, learned Skill Books, inventory, equipped gear (+ lock status), gold, gathering/crafting levels, criminal status + level, guild membership, trade history log.
- **Cross-place consistency:** because players teleport between Places (city → hunting ground → dungeon), the profile must follow them — load on `PlayerAdded` in whichever place they land in, save on `PlayerRemoving` **and** immediately before every `TeleportService:TeleportAsync` call, since a mid-teleport server crash is the single most common cause of Roblox players losing progress.
- **Guild data** is a separate DataStore keyed by guild ID (not nested in player profiles), since guild bank/reputation is shared state multiple players write to concurrently — use `UpdateAsync` with retry-on-conflict, never `SetAsync`, for anything touched by more than one player.

### Networking (Combat Sync, PvP, Trading)

**Server-authoritative for anything that touches gold, items, or damage** — the client only ever sends *intent*, never *results*:

```text
Client → RemoteEvent: "I want to cast Fireball at position X, targeting enemy Y"
Server validates: cooldown ready? in range? line of sight? enough MP?
Server computes: damage using the Physical/Magic Damage formulas (Combat & Stats section)
Server → replicates: the resulting damage/effect to nearby clients for visual feedback
```

- Character movement uses Roblox's default replication (cheap, already network-optimized) — only *skill casts, damage events, and item transfers* go through custom RemoteEvents, each server-side validated against the rules already defined elsewhere in this doc (cooldowns per skill, AGI-based attack speed, DEX-based accuracy/crit).
- **Trading** (Trade Window + 3-second lock) is a server-side state machine, not a client UI trick — the server owns "who has agreed," "what's in the offer," and "is it locked," and only the server actually moves items/gold when both sides are confirmed locked. This is what prevents the classic Roblox trade-scam pattern of swapping offered items after the other player accepts.
- **PvP death item drops** (5-50% chance per equipped item) are rolled server-side at the moment of death, before any client can react — client never sees "will this drop" ahead of time.

### Performance (1000 Concurrent Target)

- `Workspace.StreamingEnabled = true` on the large exploration maps (Hunting Grounds) — matches their "Large, exploration-heavy" sizing in Map Structure, since streaming is what makes a big open map viable on lower-end devices.
- Dungeon instancing (above) caps monster count per server to whatever one party needs, rather than 1000 players' worth of monsters existing in one place — this is what actually makes "5-15 monsters per zone" from Monster Spawning affordable at scale.
- Cities are the highest-density social spaces (all players who aren't out farming); keep NPC AI and shop-price-check scripts on a staggered update loop (e.g. every 2-3 seconds, not every frame) rather than per-frame polling.

### Security (Anti-Cheat, Exploit Prevention)

- Every RemoteEvent gets **rate limiting** (e.g. max N calls per second per player) and a **sanity check** (does this player's stated skill level even allow this action?) before the server acts on it — the single most common Roblox exploit pattern is a modified client spamming RemoteEvents directly, bypassing the intended UI cooldowns entirely.
- Gold/item quantities are validated server-side against the player's actual DataStore-backed inventory on every trade, shop transaction, and crafting attempt — never trust a client-sent quantity.
- Criminal-status and bounty state changes (Criminal System) are server-only writes, never client-triggered, since these gate PvP consequences that players have a strong incentive to fake or dodge.

## UI/UX Framework

**Fully detailed in a companion document:** **`Lost_Soul_UIUX_Design.md`**

Covers:

- Design philosophy (server-authoritative feedback, transparent numbers, mobile-first constraints)
- Main HUD, Stat & Path menu, Inventory & Equipment, Quest Log, Shop & Trade Window, Combat & Dungeon UI, Guild & Social UI, Map & Navigation
- PvP/Criminal status indicators tied to §PvP & Criminal System
- Notification/Toast system
- Settings & Accessibility (colorblind mode, text size, keybind remap)
- Roblox cross-platform implementation notes (PC/Mobile/Tablet scaling, performance, security)
- One open design question flagged for follow-up: fast travel between maps is not yet defined anywhere in this bible

---

# ✅ DEVELOPMENT CHECKLIST

## Phase 1: Foundation (Weeks 1-2)

- [ ] Map files created (8 maps in Roblox Studio)
- [ ] Basic player character model & movement
- [ ] Level system + stat allocation UI
- [ ] Combat basic (attack, skill keybind, cooldown)

## Phase 2: Core Systems (Weeks 3-4)

- [ ] Monster spawning + AI
- [ ] Skill Book drop system
- [ ] Dungeon floor structure (basic)
- [ ] Quest system (NPC interaction)

## Phase 3: Economy & PvP (Weeks 5-6)

- [ ] Trading system
- [ ] NPC shops
- [ ] PvP mechanics
- [ ] Criminal status

## Phase 4: Polish & Optimization (Weeks 7+)

- [ ] Path system UI
- [ ] Gathering mechanics
- [ ] Guild system (basic)
- [ ] Performance optimization
- [ ] Bug fixes, balancing

---

# 🎯 CURRENT STATUS

**Overall Progress:** 100%

**Locked & Ready:**

- ✅ Level system
- ✅ Stats + soft cap
- ✅ Weapon types
- ✅ Element system (6 elements, 55 skills)
- ✅ Path system (10 main + evolution + hidden)
- ✅ Map structure (8 maps, all zones)
- ✅ PvP + Criminal system
- ✅ Economy (trading, shops, guild shop)
- ✅ Monster ranks
- ✅ Dungeon concept
- ✅ Crafting (recipes, costs, success rate, boss-drop uniques)
- ✅ Boss mechanics (stat scaling, phases, named roster, race theming)
- ✅ Dungeon floor randomization (template pool, seeding, floor modifiers)
- ✅ Roblox technical architecture (server structure, DataStore, networking, performance, security)
- ✅ Balancing numbers (EXP-per-kill formula added + validated; Progression Pacing math corrected; gold-per-kill formula fixed — three conflicting versions across both docs unified into one rank-interpolation formula that now matches the Breakdown by Rank table)
- ✅ Lore timeline (Age of the Lost, Age of Settlement, Modern Day — Central Mystery kept intact)
- ✅ NPC dialogue & quest text (personality framework, dialogue trees per NPC role, Main/Side/Player-Generated quest text — see `Lost_Soul_NPC_Dialogue_Quest_Text.md`)
- ✅ UI/UX final design (HUD, all menus, combat/dungeon UI, cross-platform Roblox implementation notes — see `Lost_Soul_UIUX_Design.md`)

**Needs Detailing:**

- None — all design areas are locked. One open follow-up question noted in the UI/UX doc: fast travel between maps is not yet defined and needs a decision before World Map UI is finalized in Roblox Studio.

---

# 🚀 NEXT STEPS

Design is now 100% — remaining steps shift from *designing* to *building*:

1. **Review this master file + companion docs** with team (Economy Balancing, NPC Dialogue & Quest Text, UI/UX Design)
2. **Split into modular docs** for hand-off (08-ZONES-DETAIL, 10-MONSTER-SYSTEM, etc.) if the team finds the master file unwieldy during implementation
3. **Assign responsibilities** (Dev A = systems, Dev B = content) per the ModuleScript boundaries already defined in Technical Notes
4. **Start Roblox dev** with map files + basic systems (Phase 1 of Development Checklist)
5. **Resolve the one open design question:** fast travel between maps (flagged in `Lost_Soul_UIUX_Design.md`) — needs a decision before World Map UI implementation
6. **Iterate & balance** as you build — every formula in this bible is a first-pass tuning lever, not a guarantee (see Progression Pacing and Economy Balancing docs for how to read the tuning notes)

---

**End of Master Bible v1.0**

Last Updated: September 2026

Next Review: After Phase 1 completion