# 💰 Lost Soul — Economy Balancing System

**Status:** Comprehensive economy framework for 1000 concurrent players

**Focus:** Gold flow, equipment pricing, inflation prevention, progression pacing

**Baseline:** Lv 1-150 progression curve

---

## 📋 TABLE OF CONTENTS

1. [Economy Overview](#overview)
2. [Gold Sources](#gold-sources)
3. [Equipment Pricing Curve](#equipment-pricing)
4. [Material & Crafting Costs](#materials)
5. [Consumable Pricing](#consumables)
6. [Shop Systems](#shops)
7. [Inflation Prevention](#inflation)
8. [Progression Pacing](#pacing)
9. [Economy Examples](#examples)
10. [Dynamic Pricing](#dynamic)

---

# 💎 ECONOMY OVERVIEW

## Design Philosophy

**Balance:** Player should feel progression without infinite grinding

**Sustainability:** Economy stays healthy at all player levels

**Diversity:** Multiple gold earning paths (combat, quests, dungeon, etc.)

**Fairness:** No pay-to-win economy breaking

## Core Metrics

- **Target Daily Grind:** 2-4 hours for avg player to progress comfortably
- **Inflation Target:** <2% per month (monitored)
- **Gold Sink Rate:** 30-40% of total gold sources
- **Player Net Worth:** Should scale with level (no soft wall)

---

# 🪙 GOLD SOURCES

## 1. Monster Kills

**Base Formula:**

> **Fixed:** the previous formula here was `Base × (100 + Enemy_Level) × Luck_Modifier` with Base=10 — at Enemy_Level 1 that computes to 1010 gold, which is ~50× higher than the 10-20 gold the Breakdown by Rank table right below it (and the Farming Speed table, and every worked example in this doc) actually use. The table was always the real source of truth; the formula just didn't match it. Rewritten below so the formula and the table agree by construction — the table's per-rank Level/Gold ranges ARE the formula's inputs, not a separate hand-tuned set of numbers.

```text
Gold per kill = Lerp(Enemy_Level, Rank_Min_Level, Rank_Max_Level, Rank_Min_Gold, Rank_Max_Gold) × Luck_Modifier

Lerp(level, L0, L1, G0, G1) = G0 + (level − L0) / (L1 − L0) × (G1 − G0)
Luck_Modifier = 1 + (Player_LUK × 0.1%)
```

Look up the enemy's rank in the table below, then linearly interpolate its gold value between the rank's min and max level.

### Breakdown by Rank (formula inputs — this table IS the source of truth)

| Rank | Level | Gold Per Kill (base, no luck) | Notes |
|---|---:|---:|---|
| E | 1-10 | 10-20 | Beginner grinding |
| D | 10-25 | 20-50 | Early mid-game |
| C | 25-45 | 50-150 | Mid-game farming |
| B | 45-70 | 150-350 | Late mid-game |
| A | 70-100 | 350-1000 | High-level farming |
| S | 100-150 | 1000-2000 | Endgame elite farming |

**Worked example of the formula itself:** a Rank C enemy at Level 35 (C spans Level 25-45, Gold 50-150): `50 + (35−25)/(45−25) × (150−50) = 50 + 0.5×100 = 100 gold`, before Luck_Modifier. This is what the "Gold/Hour (base)" column in the Farming Speed table below and the worked examples further down already assume — they were internally consistent with each other, only the top-line formula was wrong.

### Farming Speed (Monsters/Hour)

| Rank | Difficulty | Kills/Hour | Gold/Hour (base) |
|---|---|---:|---:|
| E | Easy | 60 | 900 |
| D | Easy-Moderate | 50 | 1500 |
| C | Moderate | 40 | 3000 |
| B | Hard | 30 | 6000 |
| A | Very Hard | 20 | 9000 |
| S | Elite | 10 | 12000 |

**Player LUK Impact:**

- Lv 1 player (Lv 1 area): 900 gold/hour base
- +10 LUK: +900 gold/hour bonus (1800 total)
- +30 LUK: +2700 gold/hour bonus (3600 total) — builds over time

**Example:** Lv 50 player with 20 LUK farming Rank C monsters:

```text
Base: 3000 gold/hour
Luck: 3000 × (1 + 0.002) = 3006 gold/hour
Actual: ~3000-3200 gold/hour (variance from skill)
```

---

## 2. Quest Rewards

### System Quest Gold Rewards

**Main Quest:**

- Tier 1 (Lv 1-20): 50-200 gold per quest
- Tier 2 (Lv 20-50): 200-1000 gold per quest
- Tier 3 (Lv 50-100): 1000-5000 gold per quest
- Tier 4 (Lv 100-150): 5000-20000 gold per quest

**Side Quest:**

- Typically 50-70% of main quest value
- Example: Main quest 500g → Side quest 250-350g

**Human Racial Bonus:**

- +5% gold from all quests
- Example: 500g quest → 525g for Human player

### Player-Generated Quest Rewards

**Formula:**

```text
Quest_Reward = Item_Base_Value + (10% Item_Value_Tax)
Example: Horn Rabbit Horn worth 200g → Quest reward = 220g total
```

**Player Posting Cost:**

- System takes 10% commission
- Player A posts: 220g total payout
- System takes: 22g
- Player B receives: 198g

---

## 3. Dungeon Rewards

### Floor-Based Gold Rewards

| Floor Range | Rank | Gold Per Clear | Notes |
|---|---|---:|---|
| 1-20 | E | 500-1000 | Tutorial, low risk |
| 21-50 | D-C | 1000-5000 | Mid-level, moderate challenge |
| 51-80 | C-B | 5000-15000 | High challenge, better reward |
| 81-99 | B-A | 15000-50000 | Very hard, elite players |
| 100 | S | 100000 | Final boss, guaranteed loot + gold |

**Clear Time Estimates:**

- Floors 1-20: 30-45 min
- Floors 21-50: 1-1.5 hours
- Floors 51-80: 1.5-2.5 hours
- Floors 81-99: 2-4 hours
- Floor 100: 1-2 hours

**Gold/Hour from Dungeon:**

- Beginner (F1-20): ~1000-1500 g/hr
- Mid (F21-50): ~1500-3000 g/hr
- Advanced (F51-80): ~3000-6000 g/hr
- Endgame (F81-99): ~5000-12500 g/hr
- Elite (F100): ~50000-100000 g/hr (rare clear)

---

## 4. Bounty Rewards

**Calculation:**

```text
Bounty_Reward = (Target_Level × 100) + (Victims_Count × 500) + (Criminal_Level × 1000)
```

### Examples

**Scenario A: Low-Level Criminal**

- Target: Lv 30
- Victims: 1 person
- Criminal Lv: 1
- Reward: (30 × 100) + (1 × 500) + (1 × 1000) = **4000 gold**

**Scenario B: Serial Killer**

- Target: Lv 80
- Victims: 10 people
- Criminal Lv: 3
- Reward: (80 × 100) + (10 × 500) + (3 × 1000) = **18000 gold**

**Scenario C: Endgame Criminal**

- Target: Lv 150
- Victims: 50 people
- Criminal Lv: 5
- Reward: (150 × 100) + (50 × 500) + (5 × 1000) = **40000 gold**

**Bounty Frequency:**

- Rarely generated (1-2 active per 100 players)
- Bounties last 7 days
- Efficient for dedicated bounty hunters

---

## 5. Trading & Selling

**Player-to-Player Trade:**

- No tax (direct exchange of value)
- Both players benefit equally

**Selling to NPC:**

```text
NPC_Buy_Price = Item_Base_Price × 0.5 × (Supply/Demand_Modifier)
```

**Supply/Demand Modifiers:**

- High Supply: ×0.3-0.7 (common items flooded)
- Normal Supply: ×1.0 (baseline)
- Low Supply: ×1.5-2.0 (scarce items)
- System auto-adjusts weekly

---

## 6. Gathering (Active Gold)

**Selling gathered materials to NPC:**

| Material Rarity | Base NPC Price | Supply/Demand | Typical Net Sell Price |
|---|---:|---:|---:|
| Common | 10-50 | ×0.7 | 7-35 |
| Uncommon | 50-200 | ×1.0 | 50-200 |
| Rare | 200-1000 | ×1.3 | 260-1300 |
| Epic | 1000-5000 | ×1.5 | 1500-7500 |
| Legendary | 5000+ | ×2.0 | 10000+ |

**Gathering Rate (items/hour):**

- Mining Lv 1: 15 items/hour (mostly common)
- Mining Lv 25: 30 items/hour (mixed)
- Mining Lv 50: 50 items/hour (more uncommon)
- Logging & Herbalism: Similar rates

**Gathering Income (per hour):**

- Beginner: ~200-500 g/hr (common materials)
- Mid: ~1000-3000 g/hr (mixed)
- Advanced: ~3000-5000 g/hr (better rates)

---

# 🛡️ EQUIPMENT PRICING CURVE

## Weapon Progression

### Sword Line (STR/DEX scaling)

| Level | Quality | Base Price | Upgrade Cost | Total Cost |
|---|---|---:|---:|---:|
| 1-10 | Common | 100 | — | 100 |
| 10-20 | Uncommon | 300 | 50 | 350 |
| 20-30 | Rare | 800 | 150 | 950 |
| 30-40 | Epic | 2000 | 400 | 2400 |
| 40-50 | Legendary | 5000 | 1000 | 6000 |
| 50-60 | Unique | 10000 | 2000 | 12000 |
| 60+ | Mythic | 20000+ | 5000+ | 25000+ |

**Sword Purchase Timeline (Player with 2000 g/hr income):**

- Lv 1 Common Sword: 5 min play time
- Lv 10 Uncommon: 10-15 min play time
- Lv 20 Rare: 30-45 min play time
- Lv 30 Epic: 1-2 hours play time
- Lv 50 Legendary: 3-5 hours play time

### Other Weapon Types (similar structure)

- **Dagger:** ×0.7 cost (faster replacement)
- **Bow:** ×1.0 cost (standard)
- **Staff:** ×1.2 cost (magic scaling)
- **Great Axe:** ×1.3 cost (powerful)
- **Spear:** ×1.0 cost (standard)
- **Wand:** ×0.9 cost (supportive)

---

## Armor Progression

**Armor Set = Chest + Legs + Helm**

| Level | Quality | Set Price | Upgrade Per Piece | Total Setup |
|---|---|---:|---:|---:|
| 1-15 | Common | 150 | — | 150 |
| 15-30 | Uncommon | 600 | 100 | 700 |
| 30-50 | Rare | 2000 | 300 | 2300 |
| 50-75 | Epic | 5000 | 800 | 5800 |
| 75-100 | Legendary | 15000 | 2000 | 17000 |
| 100+ | Unique/Mythic | 30000+ | 5000+ | 35000+ |

**Armor Priority for New Players:**

1. Helm (5000 priority) — visible, stat boost
2. Chest (2000 priority) — main body
3. Legs (1500 priority) — mobility

---

## Accessory Pricing

| Slot | Common | Uncommon | Rare | Epic | Legendary |
|---|---:|---:|---:|---:|---:|
| Ring | 50 | 200 | 800 | 2000 | 5000 |
| Amulet | 75 | 300 | 1000 | 2500 | 6000 |
| Belt | 50 | 200 | 800 | 2000 | 5000 |
| Boots | — | — | — | — | — |

**Accessory Stack Impact:**

- 2 rings + amulet + belt = 10-20% of weapon/armor cost
- Endgame: Accessories crucial for optimization

---

# 📦 MATERIAL & CRAFTING COSTS

## Gathering Materials (NPC Buy Prices)

**Common:**

- Wood (Logging): 10 gold per unit
- Ore (Mining): 15 gold per unit
- Herb (Herbalism): 12 gold per unit

**Uncommon:**

- Refined Wood: 80 gold per unit
- Mithril Ore: 100 gold per unit
- Rare Herb: 90 gold per unit

**Rare:**

- Ancient Wood: 400 gold per unit
- Adamantite Ore: 500 gold per unit
- Essence Flower: 450 gold per unit

**Epic:**

- Crystallized Wood: 2000 gold per unit
- Orichalcum Ore: 2500 gold per unit
- Spirit Herb: 2200 gold per unit

**Legendary:**

- NOT from gathering (monster drops only)

---

## Crafting Recipes & Costs

### Basic Equipment Crafting

**Wooden Dagger (Lv 5 crafting)**

- Materials: 5 Wood + 2 Ore
- Cost: (5 × 10) + (2 × 15) = 80 gold
- Crafted Weapon Value: 150 gold
- Profit for Crafter: 70 gold (but time cost)
- NPC Sell Value: 75 gold (50% of weapon value)

**Iron Sword (Lv 15 crafting)**

- Materials: 8 Ore + 3 Wood + 1 Refined Ore
- Cost: (8 × 15) + (3 × 10) + (1 × 100) = 250 gold
- Crafted Weapon Value: 600 gold
- Profit: 350 gold
- NPC Sell Value: 300 gold

**Mithril Chest Plate (Lv 40 crafting)**

- Materials: 10 Mithril Ore + 5 Refined Wood + 2 Leather
- Cost: (10 × 100) + (5 × 80) + (2 × 50) = 1400 gold
- Crafted Armor Value: 3500 gold
- Profit: 2100 gold (high-level grind)
- NPC Sell Value: 1750 gold

---

## Crafting Progression

| Crafting Level | Recipe Type | Material Cost Range | Profit Margin | Crafting Time |
|---|---|---:|---:|---:|
| 1-10 | Tools, basic gear | 50-200 | 50-100% | 30-60 sec |
| 10-20 | Common armor | 200-500 | 100-150% | 1-2 min |
| 20-35 | Uncommon weapons | 500-1500 | 150-200% | 2-3 min |
| 35-50 | Rare equipment | 1500-5000 | 200-300% | 3-5 min |
| 50-75 | Epic items | 5000-15000 | 250-400% | 5-10 min |
| 75-100 | Legendary items | 15000-50000 | 300-500% | 10-20 min |

**Crafter Economy:** Crafters can earn MORE per hour than combat players if efficient

---

# 🧪 CONSUMABLE PRICING

## Potions

### HP Potions

| Tier | Potion | Quantity | Price | Stack Cost | Crafting Cost | Profit |
|---|---|---:|---:|---:|---:|---:|
| 1 | Minor HP | 1 | 10 | — | 5 | 5 |
| 2 | HP | 1 | 30 | — | 15 | 15 |
| 3 | Greater HP | 1 | 100 | — | 50 | 50 |
| 4 | Mega HP | 1 | 300 | — | 150 | 150 |
| 5 | Ultra HP | 1 | 1000 | — | 500 | 500 |

**Stack Purchase (10x discount):**

- 10x Minor HP: 85 gold (instead of 100)
- 10x Mega HP: 2700 gold (instead of 3000)

### MP Potions (same structure)

- Prices: ×1.2 multiplier (slightly more expensive)
- Usage: Support classes, mages

### Stat Buff Potions (1-hour duration)

| Buff | Cost | Effect | Used By |
|---|---:|---|---|
| +20% STR | 100 | Physical damage up | Warriors |
| +20% INT | 100 | Magic damage up | Mages |
| +20% AGI | 100 | Speed up | Assassins, Rangers |
| +15% DEF | 75 | Defense up | Tanks |
| +10% All Stats | 200 | Minor boost all | Everyone (expensive) |

**Buff Potion Economy:**

- Casual player: 0-5 potions per session
- Mid-core: 5-10 potions per PvP session
- Hardcore: 20+ potions per endgame grind

---

# 🏪 SHOP SYSTEMS

## NPC Shop Pricing

**Formula:**

```text
NPC_Buy_Price = Item_Base_Value × 0.5 × Supply_Demand_Modifier
NPC_Sell_Price = Item_Base_Value × Rarity_Multiplier
```

**Example (Iron Sword):**

- Item Base Value: 600 gold
- NPC Buy: 600 × 0.5 = 300 gold (what NPC pays you)
- NPC Sell: 600 gold (what you pay NPC to buy)

**Supply/Demand Modifier (auto-adjusts weekly):**

- Too much supply (>1000 units): ×0.3-0.7
- Normal supply (300-1000 units): ×1.0
- Low supply (<100 units): ×1.5-2.0

## Player Shop Pricing

**Commission:** 10% of selling price (paid by seller)

**Example:**

- Player lists Iron Sword at 500 gold
- Buyer purchases for 500 gold
- System takes: 50 gold (10%)
- Seller receives: 450 gold

**Player Shop Pricing Recommendations (system-provided):**

| Rarity | NPC Value | Market Recommendation | Typical Player Price |
|---|---:|---:|---:|
| Common | 200 | 300-400 | 350 |
| Uncommon | 600 | 800-1000 | 900 |
| Rare | 2000 | 2500-3500 | 3000 |
| Epic | 5000 | 7000-10000 | 8500 |
| Legendary | 15000 | 20000-30000 | 25000 |

**Player Profit = Price - Commission - NPC_Sale_Value**

- Listing at 900 gold (Uncommon): 900 - 90 (commission) - 300 (NPC value) = **510 profit vs NPC**

## Guild Shop Pricing

**Commission:** 5% per transaction (paid by seller)

**Incentive:** Lower than player shop (5% vs 10%), attracts guild usage

**Example (same Uncommon sword):**

- Seller lists at 850 gold (lower than player shop to move faster)
- Commission: 42.5 gold
- Seller receives: 807.5 gold
- Profit vs NPC: 507.5 gold

**Guild Shop Strategy:** Good for bulk selling, steady revenue

## Merchant Guild Benefits

**Monthly Fee:** 5000 gold

**Benefits:**

- Market information (price trends)
- Reduced shop tax: 10% → 7% (player shop) / 5% → 3% (guild shop)
- Access to advanced trading UI
- Bulk purchase discount (×0.95 cost)

**ROI Calculation:**

- Breakeven: 5000 gold saved in taxes
- Need to sell: ~167000 gold worth of items (at 5% vs 3% savings)
- For active traders: 1-2 weeks ROI

---

# 🛡️ INFLATION PREVENTION

## Gold Sinks (30-40% of gold sources)

### 1. NPC Shop Purchases (15-20% of total)

- Players buy gear at 100% value, sell at 50%
- Net loss: 50% of transaction
- Example: Buy 5000 gold sword, need to grind more

### 2. Taxes & Commissions (5-8%)

- Player shop: 10% tax
- Guild shop: 5% tax
- Quest posting: 10% commission
- Total: 5-8% of all trading volume

### 3. Upgrades & Maintenance (3-5%)

- Weapon upgrade costs: 50-100% of weapon value
- Armor upgrade costs: 30-50% of armor value
- Expected endgame player: 500-1000 gold/day on upgrades

### 4. Consumables (5-10%)

- Potions used during grinding
- Buff potions for PvP
- Repair costs (if implemented later)

## Inflation Monitoring

**Weekly Checkpoints:**

```text
Average_Gold_Per_Hour (all players) = Total_Gold_Earned / Total_Hours_Played
Expected_Target = 2000 gold/hour (baseline)
Inflation_Rate = (Average - Expected) / Expected
```

**Action Triggers:**

- Inflation > 5% in week: Increase NPC buy prices down (0.5 → 0.45)
- Inflation < -5% in week: Decrease NPC buy prices up (0.5 → 0.55)
- Sustained >10% inflation: Increase taxes (10% → 12%)
- Sustained <-10% deflation: Increase monster rewards +5%

---

# 🎯 PROGRESSION PACING

## Early Game (Lv 1-30)

**Gold Income:**

- Monster farming: 500-2000 g/hr
- Quests: 200-500 g per quest
- Average: 1000-1500 g/hr

**Expected Spending:**

- Weapon upgrade every 5 levels: ~300-800 gold per
- No armor (use drops)
- Total: ~200 gold/hr spending

**Net Progression:** +800-1300 g/hr (player accumulates gold)

**Milestone (Lv 30):**

- Player has: 50000-100000 gold accumulated
- Can afford: Full Rare armor set (2300 gold) + Rare weapon (950 gold)
- Time to reach: ~30-50 hours play time

## Mid Game (Lv 30-75)

**Gold Income:**

- Monster farming: 2000-6000 g/hr
- Dungeon (opt-in): 1500-3000 g/hr
- Quests: 500-2000 g per quest
- Average: 3000-4000 g/hr

**Expected Spending:**

- Equipment upgrade every 5-10 levels: 1000-3000 gold
- Armor maintenance: 300-500 gold/hr
- Potions for PvP: 100-300 gold/hr
- Total: 500-1000 gold/hr spending

**Net Progression:** +2000-3500 g/hr (still accumulating)

**Milestone (Lv 75):**

- Player has: 500000-800000 gold accumulated
- Can afford: Epic full set (5800 gold) + Epic weapon (2000 gold) + accessories
- Total gear investment: ~12000 gold (manageable)

## Late Game (Lv 75-150)

**Gold Income:**

- Monster farming: 5000-12000 g/hr
- Dungeon farming: 5000-12500 g/hr
- Bounty hunting (occasional): 5000-40000 per bounty (10-20/month)
- Crafting (optional): 500-2000 g/hr for materials
- Average: 8000-15000 g/hr

**Expected Spending:**

- Equipment upgrades: 2000-5000 gold/upgrade
- Consumables (heavy PvP): 500-1000 gold/hr
- Crafting materials: 500-1500 gold/hr
- Total: 1000-2000 gold/hr spending

**Net Progression:** +6000-13000 g/hr (still accumulating, but slower %)

**Milestone (Lv 150):**

- Player has: 5000000-10000000 gold (endgame wealthy)
- Can afford: Multiple Legendary gearsets (8000+ each)
- Multiple characters if desired
- Crafting specialists can build high-value items

---

# 📊 ECONOMY EXAMPLES

## New Player (Lv 10)

**Daily Session:** 2 hours play time

**Income:**

- 40 monster kills: 40 × 15 gold = 600 gold
- 2 quests: 2 × 100 gold = 200 gold
- Total: 800 gold (400 g/hr)

**Spending:**

- 1 weapon upgrade: 50 gold
- 1 inventory space tax: 0 (free)
- Total: 50 gold

**Net:** +750 gold

**Progress:** After 10 days (20 hours): 7500 gold → Can buy Uncommon weapon (350g) or upgrade path

## Casual Player (Lv 50)

**Weekly Session:** 8 hours (2 hrs/day × 4 days)

**Income:**

- 200 monster kills: 200 × 100 gold = 20000 gold
- 4 quests: 4 × 500 gold = 2000 gold
- 1 dungeon (optional): 5000 gold
- Total: 27000 gold (3375 g/hr)

**Spending:**

- Equipment upgrades every 2 weeks: 2000 gold
- Consumables & potions: 50 gold
- Total: 2050 gold (256 g/hr)

**Net:** +24950 gold weekly

**Monthly:** ~100000 gold accumulation → Can afford Rare equipment (2300g) + maintain gear

## Hardcore Player (Lv 100)

**Daily Session:** 5 hours play time

**Income:**

- 50 Rank A monster kills: 50 × 700 gold = 35000 gold
- Dungeon run (floors 80-90): 25000 gold
- 2 high-level quests: 2 × 3000 gold = 6000 gold
- Total: 66000 gold (13200 g/hr) – elite play

**Spending:**

- Consumables (PvP prep): 800 gold/hr = 4000 gold
- Equipment upgrades (1/week): 2000 gold
- Total: 6000 gold

**Net:** +60000 gold daily → 1.8M gold monthly

**Status:** Wealthy, can craft high-tier items, fund alts

## Economy Trader (Lv 75)

**Playstyle:** Crafting + Gathering + Trading

**Income:**

- Gather rare materials (30 items/day): 30 × 400 gold = 12000 gold
- Craft equipment (5 items): 5 × 1500 profit = 7500 gold
- Sell via player shop: 15 transactions × 500 g = 7500 gold (after tax)
- Total: 27000 gold/day

**Spending:**

- Material purchase (some buy, some craft): 5000 gold
- Player shop tax: 1500 gold
- Total: 6500 gold

**Net:** +20500 gold/day → 615000 gold/month

**Note:** Same income as combat grinder, but different playstyle -> **economy diversity**

---

# 🔄 DYNAMIC PRICING

## Weekly Price Adjustment Algorithm

**Trigger:** Every Sunday 00:00 UTC

**Process:**

```text
For each Item:
  Supply = Units_Listed_on_Shops - Units_Sold_This_Week
  If Supply > 500:
    Price_Modifier *= 0.9 (10% decrease)
  Else If Supply < 50:
    Price_Modifier *= 1.1 (10% increase)
  Else:
    Price_Modifier *= 1.0 (no change)

  Apply_Modifier_to_NPC_Prices
  Notify_Players_of_Price_Changes
```

**Example: Iron Sword**

| Week | Supply | Modifier | NPC Buy Price | NPC Sell Price | Player Market |
|---|---:|---:|---:|---:|---:|
| Week 1 | 200 | 1.0 | 300 | 600 | 550 |
| Week 2 | 450 | 0.95 | 285 | 570 | 520 |
| Week 3 | 600 | 0.9 | 270 | 540 | 490 |
| Week 4 | 50 | 1.1 | 297 | 594 | 540 |

**Impact:**

- Oversupply → Price drops → Buyers benefit, sellers less incentive to farm
- Undersupply → Price rises → Sellers benefit, attracts farmers back

---

## Seasonal Economy Events (Optional Expansion)

**Festival Events (bonus gold for participation):**

- Double monster drops (7 days)
- +25% quest rewards
- Event-exclusive vendor with rare items

**Holiday Economy:**

- New Year: +50% gold for first week
- Midwinter: Special dungeon (2x rewards)
- Anniversary: Guild shop commission -50%

---

# 🎲 BALANCING TUNING PARAMETERS

### If Economy is Too Expensive (deflation):

1. **Increase Monster Drops:** +10% gold per kill
2. **Increase Quest Rewards:** +15% across all tiers
3. **Decrease NPC Sell Prices:** 50% → 60% of item value
4. **Decrease Tax Rates:** 10% → 8% player shop
5. **Check:** Are players rushing to endgame? Adjust level XP instead

### If Economy is Too Cheap (inflation):

1. **Decrease Monster Drops:** -10% gold per kill
2. **Increase Consumable Costs:** +20% potion prices
3. **Increase Equipment Prices:** +15% weapon/armor cost
4. **Increase NPC Sell Prices:** 50% → 45%
5. **Increase Taxes:** 10% → 12%

### If Wealth Gap (Rich vs Poor) Too Large:

1. **Implement progressive taxes:** High players pay 15%, low players 5%
2. **Add endgame gold sink:** Prestige system costs 10M gold
3. **Increase common material value:** Gives low-level farmers benefit
4. **New lower-level dungeons:** Quick progression catchup

---

## 🎯 ECONOMY HEALTH CHECKPOINTS

**Monthly Review Metrics:**

```text
1. Average Gold/Hour (all players)
   Target: 2000-3000 g/hr
   Alert if: <1500 or >5000

2. Inflation Rate
   Target: <2% per month
   Alert if: >5%

3. Equipment Ownership Rate
   Target: 80% players own appropriate gear
   Alert if: <60% or >95%

4. Wealth Distribution (Gini Coefficient)
   Target: 0.5-0.6 (moderate inequality, healthy economy)
   Alert if: <0.3 (too equal) or >0.7 (too unequal)

5. Player Retention by Wealth Tier
   Target: <10% monthly churn
   Alert if: High earners drop >15%, low earners drop >20%
```

**Action Plan If Metrics Alert:**

- Week 1: Identify root cause
- Week 2: Propose tuning changes
- Week 3: Deploy hotfix
- Week 4: Monitor recovery

---

# 📋 IMPLEMENTATION CHECKLIST

- [ ] Lock monster drop gold formula
- [ ] Lock quest reward tiers
- [ ] Lock equipment price curves
- [ ] Lock consumable pricing
- [ ] Lock shop commission rates
- [ ] Implement NPC buy price algorithm
- [ ] Implement supply/demand modifiers
- [ ] Set up weekly price adjustment
- [ ] Create economy monitoring dashboard
- [ ] Train support team on price tuning
- [ ] Document all formulas for consistency
- [ ] Plan weekly economy reviews

---

**End of Economy Balancing Document**

Last Updated: September 2026

Next Review: After Week 1 of launch

Owner: PaulMaker (Lead Systems Designer)
