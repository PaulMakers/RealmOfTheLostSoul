# 🎮 Lost Soul — Master Game Bible v1.0

**Status:** Design locked at \~75% completion

**Last Updated:** September 2026

**Developers:** PaulMaker + Team (2 devs, no deadline)

**Platform:** Roblox

**Target Players:** 1000 concurrent

---

## 📖 TABLE OF CONTENTS

1. [GAME OVERVIEW](https://claude.ai/chat/dfa4e839-126d-4d0f-b246-35fc60cda9ac#overview)
2. [CORE DESIGN PILLARS](https://claude.ai/chat/dfa4e839-126d-4d0f-b246-35fc60cda9ac#core-design)
3. [PROGRESSION SYSTEM](https://claude.ai/chat/dfa4e839-126d-4d0f-b246-35fc60cda9ac#progression)
4. [COMBAT & STATS](https://claude.ai/chat/dfa4e839-126d-4d0f-b246-35fc60cda9ac#combat)
5. [SKILL & ELEMENT SYSTEM](https://claude.ai/chat/dfa4e839-126d-4d0f-b246-35fc60cda9ac#skills)
6. [PATH SYSTEM](https://claude.ai/chat/dfa4e839-126d-4d0f-b246-35fc60cda9ac#paths)
7. [WORLD & GEOGRAPHY](https://claude.ai/chat/dfa4e839-126d-4d0f-b246-35fc60cda9ac#world)
8. [MAP STRUCTURE](https://claude.ai/chat/dfa4e839-126d-4d0f-b246-35fc60cda9ac#maps)
9. [ZONES & CONTENT](https://claude.ai/chat/dfa4e839-126d-4d0f-b246-35fc60cda9ac#zones)
10. [MONSTER SYSTEM](https://claude.ai/chat/dfa4e839-126d-4d0f-b246-35fc60cda9ac#monsters)
11. [DUNGEON SYSTEM](https://claude.ai/chat/dfa4e839-126d-4d0f-b246-35fc60cda9ac#dungeon)
12. [PvP & CRIMINAL SYSTEM](https://claude.ai/chat/dfa4e839-126d-4d0f-b246-35fc60cda9ac#pvp)
13. [QUEST SYSTEM](https://claude.ai/chat/dfa4e839-126d-4d0f-b246-35fc60cda9ac#quests)
14. [ECONOMY](https://claude.ai/chat/dfa4e839-126d-4d0f-b246-35fc60cda9ac#economy)
15. [GATHERING & CRAFTING](https://claude.ai/chat/dfa4e839-126d-4d0f-b246-35fc60cda9ac#gathering)
16. [GUILD SYSTEM](https://claude.ai/chat/dfa4e839-126d-4d0f-b246-35fc60cda9ac#guilds)
17. [NPC FRAMEWORK](https://claude.ai/chat/dfa4e839-126d-4d0f-b246-35fc60cda9ac#npcs)
18. [LORE & STORY](https://claude.ai/chat/dfa4e839-126d-4d0f-b246-35fc60cda9ac#lore)
19. [TECHNICAL NOTES](https://claude.ai/chat/dfa4e839-126d-4d0f-b246-35fc60cda9ac#technical)
20. [DEVELOPMENT CHECKLIST](https://claude.ai/chat/dfa4e839-126d-4d0f-b246-35fc60cda9ac#checklist)

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

## Seven Main Stats

| Stat Function Formula | | |
| --- | --- | --- |
| **STR** | Physical damage, carry weight | Physical ATK = Base + (STR × 2) |
| **VIT** | Max HP, physical defense | Max HP = Base + (VIT × 10) |
| **INT** | Magic/elemental damage, max MP | Magic ATK = Base + (INT × 2), Max MP = Base + (INT × 5) |
| **MND** | Magic defense, healing power | Magic DEF = Base + (MND × 1.5), Healing = Base + (MND × 2%) |
| **AGI** | Attack speed, move speed | ATK Speed = Base + (AGI × 0.5%), Move Speed = Base + (AGI × 0.3%) |
| **DEX** | Accuracy, critical rate | Accuracy = Base + (DEX × 1%), Crit Rate = Base + (DEX × 0.2%) |
| **LUK** | Rare drop rate, crit damage bonus | Crit Damage = Base + (LUK × 0.3%), Skill Book Drop = 1% + (LUK × 0.05%) |

## Starting Stats (Budget 70 per race)

| Stat Human Demon Elf | | | |
| --- | --- | --- | --- |
| STR | 10 | 13 | 7 |
| VIT | 10 | 11 | 9 |
| INT | 10 | 12 | 10 |
| MND | 12 | 8 | 10 |
| AGI | 9 | 9 | 12 |
| DEX | 10 | 8 | 12 |
| LUK | 9 | 9 | 10 |

## Stat Allocation on Level Up

- **Automatic Base Growth:** +1 per stat at level up (race-dependent variations possible)
- **Free Points:** `Level / 2` points per level to allocate manually
- **Hybrid System:** Player gets automatic baseline + can customize with free points

## Soft Cap (Diminishing Returns)

Berlaku berdasarkan **total poin yang dialokasikan ke satu stat**, bukan dari level:

| Points Allocated Effectiveness | |
| --- | --- |
| 0–50 | 100% |
| 51–100 | 70% |
| 101+ | 40% |

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
Physical Damage = (Base ATK + STR × 2 + Weapon Bonus) × (100 - Enemy DEF%)
Magic Damage = (Base Magic ATK + INT × 2 + Weapon Bonus) × (100 - Enemy Magic DEF%)
Healing = (Base Heal + MND × 2%) × Healing Modifiers
```

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
| --- | --- | --- | --- |
| E | N/A (no drop) | — | |
| D | Lv 1-3 | Common | |
| C | Lv 4-6 | Uncommon | |
| B | Lv 7-8 | Rare | |
| A | Lv 9 | Epic | |
| S | Lv 10 | Legendary | |

---

# 🛤️ PATH SYSTEM

## What is a Path?

Path bukan class tradisional. Path adalah **identitas + arah perkembangan** berdasarkan bagaimana pemain bermain.

## 10 Starting Paths (Level 15 Recommendation)

| Path Stat Focus Weapon Identity | | | |
| --- | --- | --- | --- |
| **Swordsman** | STR + DEX | Sword | Balanced melee, damage + precision |
| **Knight** | VIT + STR | Sword + Shield | Tank, survivability high |
| **Berserker** | STR | Great Axe | Glass cannon, massive damage |
| **Spearman** | STR + AGI | Spear/Polearm | Mid-range melee, mobile |
| **Archer** | DEX + AGI | Bow | Ranged physical, precision |
| **Assassin** | AGI + DEX | Dagger | Burst + evasion, fragile |
| **Mage** | INT | Staff | Elemental ranged, pure magic |
| **Spellblade** | STR/INT hybrid | Sword + Element | Melee + magic hybrid |
| **Priest** | MND | Wand | Recovery/support, low damage |
| **Explorer** | LUK | Any | Loot specialist, utility |

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

| Path Awal Evolve A Evolve B | | |
| --- | --- | --- |
| Swordsman | **Blademaster** (STR) | **Duelist** (DEX) |
| Knight | **Guardian** (VIT) | **Paladin** (VIT+MND) |
| Berserker | **Juggernaut** (STR+VIT) | **Warlord** (leadership) |
| Spearman | **Dragoon** (STR burst) | **Lancer** (AGI mobile) |
| Archer | **Sniper** (DEX precision) | **Ranger** (AGI mobile) |
| Assassin | **Shadow Blade** (stealth) | **Poison Blade** (DEX+INT DoT) |
| Mage | **Elementalist** (INT pure) | **Sorcerer** (INT+MND CC) |
| Spellblade | **Battlemage** (balanced) | **Runeblade** (debuff) |
| Priest | **Bishop** (pure heal) | **Exorcist** (MND+INT offensive) |
| Explorer | **Treasure Hunter** (loot) | **Trickster** (AGI evasion) |

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

| Rank Examples Level Range | | |
| --- | --- | --- |
| E | Slime, Goblin, Kobold, Magic Wolf, Horn Rabbit | Lv 1-10 |
| D | Orc, Golem, Giant Spider, Skeleton Warrior, Rock Turtle | Lv 10-25 |
| C | Wyvern, Ogre, Silver Wolf, Hobgoblin, Slime King | Lv 25-45 |
| B | King Goblin, General Ogre, Emerald Wolf, General Wyvern | Lv 45-70 |
| A | King Wyvern, Hellhound/Cerberus, Wraith/King Skeleton, Mithril Golem | Lv 70-100 |
| S | Ancient Dragon, Behemoth, Arch Salamander, Fenrir Lord, Arch Lich | Lv 100+ |

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

- **Stat Multiplier:** 2-3x vs regular monster same rank
- **Special Attack:** 1-2 unique abilities not seen in regular monsters
- **Loot Guarantee:** 100% rare drop + Skill Book
- **Phase Mechanic:** Bosses may change pattern at 50% HP (optional complexity)

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

- Monster kills: `100 × Monster Level`
- Quests: varies by quest
- Dungeon: varies by floor
- Trading/selling: player-determined
- Bounties: `(Target Lv × 100) + bonuses`

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

- Monthly membership fee: TBD
- Benefits: market info, lower shop tax (7% → 5%), access to market data (price trends)
- Rank: based on transaction volume & gold traded

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

**TBD — To be detailed in separate document**

Planned features:

- Recipe system (material → item)
- Crafting level progression
- Success/failure rate
- Equipment crafting vs consumable crafting
- Unique recipes from boss drops

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

**To Be Detailed Separately**

Planned:

- Quest acceptance/completion logic
- Dialogue trees
- Personality per NPC
- Story integration

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

**To Be Detailed Separately**

Planned:

- Ancient age (Dungeon Core creators)
- Medieval age (human/demon conflict beginning)
- Modern day (current game time, cold war)

---

# 💻 TECHNICAL NOTES

## Roblox Architecture (Summary)

**To Be Detailed in Separate Document**

Planned:

- Server structure
- DataStore integration (player save data)
- Networking (combat sync, PvP)
- Performance optimization (8 separate maps)
- Security (anti-cheat, exploit prevention)

## UI/UX Framework

**To Be Detailed in Separate Document**

Planned:

- Inventory UI
- Quest log
- Minimap
- Character sheet
- Status effects display
- Chat system

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

**Overall Progress:** \~75%

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

**Needs Detailing:**

- ⏳ Crafting recipes
- ⏳ Boss mechanics (per boss)
- ⏳ NPC dialogue & quest text
- ⏳ Dungeon floor randomization
- ⏳ Roblox technical architecture
- ⏳ UI/UX final design
- ⏳ Lore timeline
- ⏳ Balancing numbers (economy, XP curves)

---

# 🚀 NEXT STEPS

1. **Review this master file** with team
2. **Split into modular docs** (08-ZONES-DETAIL, 10-MONSTER-SYSTEM, etc.)
3. **Assign responsibilities** (Dev A = systems, Dev B = content)
4. **Start Roblox dev** with map files + basic systems
5. **Iterate & balance** as you build

---

**End of Master Bible v1.0**

Last Updated: September 2026

Next Review: After Phase 1 completion
