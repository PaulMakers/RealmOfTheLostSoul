# 🧙 Lost Soul — NPC Dialogue & Quest Text

**Status:** Melengkapi item "NPC Dialogue Structure — To Be Detailed Separately" dari Master Game Bible

**Dokumen pendamping:** `LostSoul.md` (§ NPC Framework, § Quest System) dan `Lost_Soul_Economy_Balancing.md` (§ Quest Rewards)

**Cakupan:** Mekanisme sistem dialogue, kerangka kepribadian NPC, dialogue tree untuk setiap kategori NPC, dan contoh teks quest lengkap (Main, Side, Player-Generated)

**Catatan bahasa:** Teks dialog NPC yang muncul langsung di dalam game (semua kalimat dalam tanda kutip `"..."`) sengaja tetap dalam Bahasa Inggris, karena itu naskah asli yang akan dipakai di game. Bagian penjelasan, struktur, dan catatan desain diterjemahkan ke Bahasa Indonesia.

---

## 📋 DAFTAR ISI

1. [Gambaran Sistem Dialogue](https://claude.ai/chat/eb4cf320-ee6a-4be5-add9-f091b2d66587#overview)
2. [Kerangka Kepribadian NPC](https://claude.ai/chat/eb4cf320-ee6a-4be5-add9-f091b2d66587#personality)
3. [Notasi Dialogue Tree & Logika State Quest](https://claude.ai/chat/eb4cf320-ee6a-4be5-add9-f091b2d66587#notation)
4. [Dialog NPC Utility](https://claude.ai/chat/eb4cf320-ee6a-4be5-add9-f091b2d66587#utility)
5. [Dialog NPC Quest](https://claude.ai/chat/eb4cf320-ee6a-4be5-add9-f091b2d66587#quest-npc)
6. [Dialog NPC Lore/Story](https://claude.ai/chat/eb4cf320-ee6a-4be5-add9-f091b2d66587#lore-npc)
7. [Bark Flavor NPC](https://claude.ai/chat/eb4cf320-ee6a-4be5-add9-f091b2d66587#flavor)
8. [Teks Main Quest — Chain Pembuka "Awakening"](https://claude.ai/chat/eb4cf320-ee6a-4be5-add9-f091b2d66587#main-quest)
9. [Teks Side Quest — Contoh](https://claude.ai/chat/eb4cf320-ee6a-4be5-add9-f091b2d66587#side-quest)
10. [Player-Generated Quest — Teks Sistem](https://claude.ai/chat/eb4cf320-ee6a-4be5-add9-f091b2d66587#player-quest)
11. [Aturan Variasi Dialog per Ras](https://claude.ai/chat/eb4cf320-ee6a-4be5-add9-f091b2d66587#race-variation)
12. [Gating Reputasi & Status Criminal](https://claude.ai/chat/eb4cf320-ee6a-4be5-add9-f091b2d66587#gating)
13. [Checklist Implementasi](https://claude.ai/chat/eb4cf320-ee6a-4be5-add9-f091b2d66587#checklist)

---

# 🗨️ GAMBARAN SISTEM DIALOGUE

**Tujuan desain:** Dialog NPC harus terasa ditulis khusus untuk ~36 NPC bernama (12 per kota × 3 kota) tanpa harus benar-benar menulis 36 skrip yang sepenuhnya unik. Dokumen ini menyelesaikannya dengan pendekatan **satu template per role** — satu contoh dialog yang lengkap per peran NPC (Innkeeper, Blacksmith, Guild Master, dst.), ditambah lapisan **Variasi Ras** (§11) yang mengubah nuansa/kosakata per kota tanpa menulis ulang strukturnya.

**Setiap dialog NPC dibangun dari tiga lapisan:**

1. **Personality** (§2) — tag sifat singkat yang mengatur pilihan kata dan nada bicara, dijaga konsisten di setiap baris yang diucapkan NPC tersebut.
2. **Function** (§4-6) — apa yang sebenarnya dilakukan NPC ini secara mekanik (toko, hub quest, penyampai lore, bark flavor).
3. **State** (§3) — state dialog mana dari sekumpulan kecil state yang sedang aktif (locked, available, in-progress, ready to turn in, completed).

Ini meniru cara Path System (Master Bible §Path System) memisahkan *identitas* dari *mekanik* — personality dialog adalah flavor, state dialog adalah hook sistem yang sebenarnya.

---

# 🎭 KERANGKA KEPRIBADIAN NPC

Setiap NPC bernama (Utility, Quest, Lore/Story) mendapat satu **Personality Tag** dari daftar ini. Flavor NPC (§7) tidak perlu tag — mereka pakai bark singkat saja.

| Tag | Nada Bicara | Pola Bicara | Contoh Pembuka |
|---|---|---|---|
| **Gruff-Warm** | Kalimat pendek, humor kering di balik sikap kasar | Langsung ke inti, tanpa basa-basi, sesekali lelucon satu baris | "You're bleeding on my floor. Sit." |
| **Formal-Proud** | Presisi, sadar gelar/jabatan, menjunjung prosedur | Kalimat lengkap, menyapa pemain dengan pangkat/gelar setelah dikenal | "Adventurer. State your business with the Guild." |
| **Warm-Nurturing** | Menenangkan, peduli pada kondisi pemain | Balik bertanya, mengingat detail kecil | "You look tired. Sit, eat first — business can wait." |
| **Sharp-Mercantile** | Transaksional, angka-dulu, agak geli saat ditawar | Bicara dalam istilah harga & margin bahkan saat basa-basi | "Everything has a price. Yours is listening for three more seconds." |
| **Zealous-Devout** | Bicara penuh keyakinan, sering merujuk doktrin Light/Dark/nature tanpa diminta | Kalimat lebih panjang, retoris | "Do you feel it? The System answers those who ask correctly." |
| **Weary-Wise** | Tua, sudah terlalu banyak melihat, menjawab pertanyaan dengan pertanyaan lagi | Tempo lambat, kalimat menggantung, menyiratkan lebih dari yang diucapkan | "Ah. You're the one asking about the Cores now, are you." |
| **Brash-Aggressive** (condong Demon) | Konfrontatif secara default, menghormati kekuatan di atas kesopanan | Menantang, meremehkan, kasar tapi tidak sepenuhnya bermusuhan | "Still alive? Good. Boring adventurers die first." |
| **Serene-Distant** (condong Elf) | Tenang dalam situasi apa pun, bicara seolah waktu tidak mendesak | Jeda panjang tersirat dari tanda baca, metafora alam | "The grove does not rush. Neither will I." |

**Aturan:** satu NPC memakai tag yang sama di setiap state dialog (toko, quest, bark idle) — inilah yang membuat ~36 NPC terasa berbeda tanpa perlu 36 penulis yang unik.

---

# 🌳 NOTASI DIALOGUE TREE & LOGIKA STATE QUEST

Semua dialogue tree di dokumen ini memakai notasi ringan berikut (ini juga jadi spesifikasi yang bisa diserahkan ke Dev A/B untuk membangun UI dialog in-game):

```text
[NAMA NPC — Role, Personality Tag]
STATE: <state saat ini>
NPC: "<baris dialog>"
  > Option: "<respon pemain>" → <hasil>
```

## State Quest Universal

Setiap NPC pemberi quest bercabang berdasarkan tepat satu dari lima state ini — ini adalah state machine yang sudah tersirat di Master Bible §Quest System, dibuat eksplisit di sini:

| State | Pemicu | Yang Dikatakan NPC | Opsi Pemain |
|---|---|---|---|
| **LOCKED** | Prasyarat belum terpenuhi (level, quest sebelumnya, Path, ras) | Tidak menyinggung quest sama sekali, ATAU petunjuk samar jika `hint_when_locked = true` | Tidak ada (quest tidak muncul) |
| **AVAILABLE** | Prasyarat terpenuhi, quest belum diterima | Penawaran quest lengkap | Accept / Decline / Tanya lebih lanjut |
| **IN PROGRESS** | Sudah diterima, objective belum selesai | Pengingat sisa yang harus dilakukan | Cek objective / Abandon |
| **READY TO TURN IN** | Objective selesai, belum disetor | Mengonfirmasi penyelesaian | Turn in (→ reward) / (tidak ada lagi) |
| **COMPLETED** | Sudah disetor — quest sekali jalan | Hanya baris idle/flavor, ATAU penawaran ulang jika `repeatable = true` | Interaksi toko/idle saja |

**Aturan Abandon:** membatalkan quest mengembalikannya ke AVAILABLE (bukan LOCKED), kecuali quest ditandai `one_shot_only` secara eksplisit (dipakai untuk beberapa quest pemicu Hidden Path di mana mencoba ulang akan membuat penemuannya jadi terlalu mudah).

**Penyerahan reward:** saat turn-in, baris NPC selalu mengonfirmasi persis apa yang diberikan (jumlah gold, nama item, EXP) — tidak ada "kamu telah diberi hadiah" yang samar. Ini selaras dengan transparansi yang sudah ada di contoh-contoh perhitungan Economy doc.

---

# 🔨 DIALOG NPC UTILITY

NPC Utility (Innkeeper, Blacksmith, Armorer, Merchant, Tool Merchant) ada di setiap kota. Berikut satu contoh lengkap per role, ditulis untuk **Human City**; §11 membahas bagaimana versi Demon/Elf mengubah nuansa struktur yang sama.

## Innkeeper — Human City (Warm-Nurturing)

```text
[MARA THISTLEWOOD — Innkeeper, Warm-Nurturing]
STATE: Idle (menu toko)
NPC: "You look tired. Sit, eat first — business can wait."
  > Option: "Rest here." → Membuka menu Rest: full HP/MP restore, 10 gold. Respawn point diset ke Inn ini.
  > Option: "Any rumors?" → Pool baris flavor acak (lihat §7, bucket Innkeeper)
  > Option: "Just looking." → Dialog ditutup
NPC (setelah Rest dibeli): "There. Colour's back in your face. Go on, then — and mind the Forest Zone, it's been busy."
```

## Blacksmith — Human City (Gruff-Warm)

```text
[TORV IRONHAND — Blacksmith, Gruff-Warm]
STATE: Idle (menu toko)
NPC: "You're bleeding on my floor. Sit. What do you need — sharper, or stronger?"
  > Option: "Upgrade my weapon." → Membuka menu Upgrade (tier Master Bible §Equipment Pricing Curve)
  > Option: "What's this material worth?" → Membuka menu Sell, harga beli NPC sesuai Economy doc §Gold Sources
  > Option: "Nothing, just looking." → "Then stop bleeding on my floor."
NPC (upgrade berhasil): "There. Don't waste it."
NPC (roll crafting gagal): "Hah. Metal's stubborn today. Didn't take. Materials are half gone — bring more, or come back when you're stronger."
```

## Armorer — Human City (Formal-Proud)

```text
[SIR EDMUND VANCE — Armorer, Formal-Proud]
STATE: Idle (menu toko)
NPC: "Adventurer. Proper armor is not vanity — it is the difference between a story you tell and one told about you."
  > Option: "Show me armor." → Membuka toko Armor (sesuai tier harga)
  > Option: "Which piece matters most?" → "Helm first. A blow to the head forgives no one, Rare or otherwise."
  > Option: "Just browsing." → "As you wish. Return when sense finds you."
```

## Merchant — Human City (Sharp-Mercantile)

```text
[BESSY COLQUHOUN — Merchant, Sharp-Mercantile]
STATE: Idle (menu toko)
NPC: "Everything has a price. Yours is listening for three more seconds."
  > Option: "Buy." → Membuka toko barang umum
  > Option: "Sell." → Membuka menu jual (modifier Supply/Demand berlaku sesuai Economy doc)
  > Option: "Prices seem high today." → "Prices are never high. Supply is low. Go kill something, come back, we'll talk."
```

## Tool Merchant — Human City (Warm-Nurturing)

```text
[OLD PEMBERTON — Tool Merchant, Warm-Nurturing]
STATE: Idle (menu toko)
NPC: "Mining, logging, or herbs today? Or are you still deciding what suits you — no shame in that."
  > Option: "Show gathering tools." → Membuka toko Tool (Pick/Axe/Sickle, tool tidak rusak sesuai Master Bible §Gathering)
  > Option: "I'm an Elf, is there a bonus?" → "Aye, +20% in forest and nature ground for your kind. Wish I had that knack myself."
  > Option: "Not today." → "Door's open when you are."
```

---

# 📜 DIALOG NPC QUEST

## Guild Master — Human City (Formal-Proud)

Guild Master adalah NPC jangkar untuk chain Main Quest (§8) dan pintu gerbang untuk quest milestone terkait Path.

```text
[GUILD MASTER ALARIC — Guild Master, Formal-Proud]
STATE: AVAILABLE (Main Quest: "First Steps")
NPC: "Another new face. The System marked you the moment you arrived — I felt it on the Guild ledger before you walked in. Tell me: do you understand what that means?"
  > Option: "Not really." → "Then you're honest, at least. Sit. I'll explain what every adventurer needs to know before the Hunting Ground eats them alive." → Quest diterima
  > Option: "I want to get straight to fighting." → "Everyone does. Everyone who skipped this conversation is also the one I send Guards to identify later. Five minutes, adventurer." → Quest diterima (hasil sama, flavor berbeda)
  > Option: "Not now." → Dialog ditutup, quest tetap AVAILABLE

STATE: IN PROGRESS
NPC: "Still finding your feet? The Adventurer's Primer covers stats, your first skill, and how not to die in the Forest Zone Beginner. Come back once you've read it and landed a kill."

STATE: READY TO TURN IN
NPC: "You're standing straighter already. Good. That's the System settling in — most people don't notice it happening. Here." → Reward: 100 gold, +5% bonus (Human racial), 500 EXP, membuka akses Quest Board
```

## Quest Board NPC — Semua Kota (Sharp-Mercantile, disesuaikan per ras)

Quest Board secara mekanik adalah menu, tapi secara naratif diwakili oleh orang yang membacakannya — ini menjaga daftar Flavor NPC agar tidak terasa kosong.

```text
[BOARD CLERK — Quest Board NPC, Sharp-Mercantile]
STATE: Idle
NPC: "Board's current. Side jobs, bounty postings, and — " *melirik selembar kertas terlipat* " — someone's posted a player request for a Rabbit Horn again. Third one this week."
  > Option: "Show System quests." → Membuka daftar Side Quest (bertier sesuai level pemain, per Economy doc §Quest Rewards)
  > Option: "Show player quests." → Membuka Player-Generated Quest board (§10)
  > Option: "Show bounties." → Membuka bounty board (Master Bible §Bounty System) — abu-abu/tidak aktif jika pemain berstatus Criminal
```

## Reward Officer — Semua Kota (Formal-Proud)

```text
[REWARD OFFICER — Formal-Proud]
STATE: READY TO TURN IN (side quest generik)
NPC: "Confirmed complete. Let the record show: [Quest Name], closed. Payment released."
  > Baris sistem (tidak diucapkan, muncul sebagai UI toast): "+[X] gold, +[Y] EXP. [Item, jika ada] added to inventory."
NPC: "Anything else outstanding, or will that be all?"
```

## Contoh Quest Giver — "Widow Hallick" (Weary-Wise, NPC unik di Human City Residential District)

```text
[WIDOW HALLICK — Quest Giver, Weary-Wise]
STATE: LOCKED (butuh Lv 5)
NPC: (tidak ada opsi dialog yang muncul — dia hadir tapi belum punya apa-apa untuk ditawarkan)

STATE: AVAILABLE (Side Quest: "The Empty Chair")
NPC: "My husband went into the Forest Zone eleven days ago. Adventurer's Guild says eleven days means... well. They stopped saying it kindly around day nine."
  > Option: "I'll look for him." → Quest diterima
  > Option: "I'm sorry for your loss." → "Not yet, it isn't. Not until someone tells me for certain." → quest tetap AVAILABLE
  > Option: "That's not my problem." → "No. It isn't." (dialog ditutup, tanpa penalti, quest tetap AVAILABLE untuk nanti)

STATE: READY TO TURN IN (menemukan barang miliknya dekat sarang monster Rank D)
NPC: "...His pipe. That's — that's his, yes." *jeda panjang* "Thank you. For finding out, at least. Here — it isn't much." → Reward: 220 gold, 300 EXP, bundle material Common
```

---

# 📖 DIALOG NPC LORE/STORY

NPC ini tidak langsung menjalankan quest, tapi menanamkan Central Mystery (Master Bible §Lore & Story) lewat dialog opsional yang bisa diulang — jalur utama untuk petunjuk penemuan Hidden Path.

## City Guard Captain — Human City (Gruff-Warm)

```text
[CAPTAIN ROSS — City Guard Captain, Gruff-Warm]
STATE: Idle
NPC: "Central Hunting Ground's been quiet. Too quiet, if you're the suspicious type — I am."
  > Option: "Any advice?" → "Watch Demon patrols near the Highland Zone. Cold War doesn't mean cold tempers."
  > Option: "What's your stance on the Demons?" → "Wary. Not hateful — wary. There's a difference your generation seems to be forgetting."
```

## Town Crier — Human City (Formal-Proud)

```text
[TOWN CRIER — Formal-Proud]
STATE: Idle (bergilir; juga menampilkan event live server)
NPC (pool bergilir):
  - "Hear ye! The Merchant Guild reports market prices stable this week — Iron Sword holding at fair value."
  - "A Rank A dragon sighted near Ancient Ruins. The Guild advises: don't."
  - "Reminder: Player Shops close their doors to any Criminal-flagged adventurer. The law is the law."
```

## Priest/Cleric — Human City, Temple District (Zealous-Devout, elemen Light)

```text
[SISTER ELOWEN — Priest, Zealous-Devout]
STATE: Idle
NPC: "Do you feel it? The System answers those who ask correctly — Light rewards those who give before they take."
  > Option: "Teach me about Light element." → Membuka vendor/teks lore Light Skill Book
  > Option: "Who made the System?" → "A question older than this Temple. Some say the Lost gave it to us as a gift. Others say we merely found what they could not carry away when they vanished. I choose to believe the first. Belief matters more than proof, some days."
```

## Dark Element Trainer — Demon City, Shadow Temple (Brash-Aggressive)

```text
[VORAK THE HOLLOW — Dark Element Trainer, Brash-Aggressive]
STATE: Idle
NPC: "Dark doesn't heal soft. It costs you — HP for power, every cast. You want strength without a price? Go pray to the Human's Light god instead."
  > Option: "Teach me Dark element." → Membuka vendor/teks lore Dark Skill Book
  > Option: "Why does Dark cost HP?" → "Because power that's free is power that's lying to you. Ours doesn't lie."
```

## Druid — Elf City, Nature Temple (Serene-Distant, elemen Earth)

```text
[ELDER WILLOWMERE — Druid, Serene-Distant]
STATE: Idle
NPC: "The grove does not rush. Neither will I. You came for Earth's teaching, or merely its shade?"
  > Option: "Earth's teaching." → Membuka vendor/teks lore Earth Skill Book
  > Option: "Do all Elves feel this way?" → "Most. Time moves oddly under the World Tree. You will understand, in a decade or two. Or you won't need to — humans rarely stay that long."
```

## Elf Elder — Elf City, World Tree Hub (gabungan Serene-Distant / Weary-Wise — NPC lore "bicara hati-hati" yang sudah ditetapkan di Master Bible §Timeline)

```text
[ELDER SILVANESSA — Elf Elder, Weary-Wise]
STATE: Idle
NPC: "You ask about the Lost. Everyone eventually does, once they've lived here long enough to stop taking the System for granted."
  > Option: "Are Elves connected to the Lost?" → "Some of our oldest songs claim so. I won't confirm or deny — songs are not proof, only inheritance. But ask me again once you've earned a Hidden Path. You'll understand why I'm careful, by then."
  > Option: "Never mind." → "Wise, sometimes, to leave a question unopened." (ditutup)
```

---

# 💬 BARK FLAVOR NPC

Flavor NPC (asisten pandai besi, penjaga merchant, dll.) tidak mendapat dialogue tree penuh — mereka mendapat **bark pool**: 3-5 baris voice-line idle singkat per NPC, tanpa percabangan, dipicu ulang saat pemain mendekat dengan cooldown (disarankan: 45-90 detik agar tidak terasa spam). Ini membuat kota terasa hidup tanpa harus menulis 12 dialogue tree penuh tambahan per kota.

**Contoh bark pool (Human City):**

- *Blacksmith's Apprentice:* "Careful near the forge." / "Master Ironhand doesn't like idle hands." / "You need an upgrade? He's inside."
- *Merchant's Guard:* "Move along, nothing to steal here — I'm watching." / "Prices are fair. Complaints go to the Merchant Guild, not me." / *mengangguk diam*
- *Off-duty Adventurer (ambient, NPC non-toko):* "Forest Zone's been rough today." / "Anyone seen a Guild quest worth the walk?" / "I miss when Rank D felt hard."

**Patokan umum:** setiap kota butuh sekitar 6-8 NPC bark-only agar terasa ramai pada skala target (1000 concurrent, sesuai header Master Bible) tanpa membengkakkan jumlah NPC dialogue-tree penuh melebihi ~12/kota yang sudah ditetapkan di Map Structure.

---

# ⚔️ TEKS MAIN QUEST — CHAIN PEMBUKA "AWAKENING"

Teks lengkap chain Main Quest pembuka, jalur Human City (pembuka Demon/Elf mengikuti struktur 4-quest yang sama, disesuaikan nuansanya per §11 — tidak ditranskrip ulang sepenuhnya di sini agar tidak ~3x redundan, tapi struktur beatnya identik).

Reward di bawah memakai nilai Main Quest Tier 1 dari Economy doc §Quest Rewards (50-200 gold/quest).

### Quest 1: "First Steps" (Guild Master Alaric)

- **Pemberi:** Guild Master Alaric, Human City Adventurer Guild
- **Objective:** Baca Adventurer's Primer (otomatis membuka UI tutorial soal stats/skill), dapatkan 1 kill di Forest Zone Beginner
- **Dialog:** lihat contoh Guild Master di §5 di atas
- **Reward:** 100 gold (+5% bonus Human = 105g), 500 EXP, membuka akses Quest Board

### Quest 2: "A Name Worth Earning" (Guild Master Alaric)

- **Objective:** Capai Level 5, alokasikan free stat point pertama
- **NPC (Available):** "Level five. That's when the System stops being theoretical for most people. Come back once you've felt it — you'll know."
- **NPC (Ready):** "There it is. That look. Everyone gets it around Level 5 — like the world got slightly louder. Welcome to actually playing this game, adventurer."
- **Reward:** 150 gold (157g dengan bonus), 800 EXP

### Quest 3: "Pick a Path, Any Path" (Guild Master Alaric)

- **Objective:** Capai Level 15 (ambang unlock Path sesuai Master Bible §Path System), pilih Path awal
- **NPC (Available):** "Fifteen. The Guild ledger says you're eligible for a Path now — an identity, not a cage. Ten to choose from. Choose based on how you've actually been playing, not how you think you should."
- **NPC (Ready):** "[Path Name]. Suits you, from what I've heard of your fights. Wear it well — or don't, and pick a different one later. No penalty, no judgment."
- **Reward:** 200 gold (210g dengan bonus), 1200 EXP, weapon Uncommon sesuai Path yang dipilih

### Quest 4: "The Ledger's Question" (Guild Master Alaric → dilanjut ke Sister Elowen, menanamkan benih Central Mystery)

- **Objective:** Bicara dengan Sister Elowen di Temple District
- **NPC Alaric (Available):** "One more thing, before I stop hovering over you like a new recruit. The Guild ledger marks everyone who enters this world — but nobody's ever explained *how* it knows. Go ask Sister Elowen. She has... theories. So does everyone. None of them agree."
- **NPC Elowen (saat pemain tiba):** "Alaric sent you? He always does, eventually. Everyone asks the same question their first month, and everyone gets the same honest answer: I don't know. Nobody does. But I'll tell you what we *do* know — sit, this takes longer than five minutes."
- **Reward:** 200 gold (210g dengan bonus), 1500 EXP, **unlock naratif:** entri codex Central Mystery ditambahkan ke Lore Journal pemain in-game

**Catatan desain:** chain ini sengaja diakhiri dengan pertanyaan, bukan jawaban — selaras dengan Master Bible §Central Mystery ("disimpan untuk konten endgame/expansion"). Reward Quest 4 bersifat naratif, bukan mekanik, dan ini disengaja: memberi sinyal ke pemain bahwa berburu lore adalah jalur reward tersendiri, terpisah dari jalur gold/EXP.

---

# 🗺️ TEKS SIDE QUEST — CONTOH

### "The Empty Chair" (Widow Hallick) — teks lengkap ada di §5 di atas.

### "Apprentice's Request" (Blacksmith's Apprentice → dilanjut ke Torv Ironhand)

- **Rentang level:** 10-20 (batas Tier 1-2)
- **Objective:** Kumpulkan 5 Iron Ore (Mining), antarkan ke Torv
- **NPC (Available):** "Master's out of Iron Ore and too proud to say he's behind on orders. Bring five, would you? I'll make sure he credits you, not me."
- **NPC Torv (Ready to turn in, jika diantar langsung ke dia):** "Ore's good. My apprentice send you? Smart lad, hopeless at mining." → Reward: 180 gold, 400 EXP, +5 reputasi Blacksmith (membuka diskon 5% pada reputasi 50)

### "Silence in the Twilight Thicket" (Ranger NPC, hub Elf Hunting Ground)

- **Rentang level:** 30-40 (Tier 2)
- **Objective:** Bersihkan 3 sarang monster Rank C di Twilight Thicket yang mengganggu keseimbangan alam setempat
- **NPC (Available):** "The grove sends a request, not an order — the Thicket's dens have overgrown past what the balance allows. Thin them, if you're willing. Three should restore it."
- **NPC (Ready):** "Balance returns. The grove... doesn't thank in words. But I do. Take this." → Reward: 650 gold, 2200 EXP, material afinitas Earth Uncommon

---

# 📝 PLAYER-GENERATED QUEST — TEKS SISTEM

Player-Generated Quest (Master Bible §Quest System, Economy doc §Quest Rewards) diposting lewat NPC Board Clerk, tapi teks quest-nya sendiri **ditulis oleh pemain**, dengan scaffolding sistem di sekelilingnya. Bagian ini mendefinisikan scaffolding tersebut agar tetap terasa konsisten apa pun yang diketik pemain.

### Alur Posting (Player A)

```text
[BOARD CLERK — Sharp-Mercantile]
NPC: "Posting a request? Name the item, set your offer, and I'll pin it up. Standard 10% goes to the Guild — that's not negotiable, that's rent on the board."
  > UI: Pemain memasukkan [Nama Item], [Jumlah], [Nilai Tawaran]
NPC (konfirmasi): "Posted: '[Item Name] ×[Quantity], [Offer]g.' Board fee: [10% of Offer]g, deducted now. Total payout to whoever fills it: [Offer]g. Good luck — that's more than I can promise you."
```

### Listing Board (ditampilkan ke Player B yang browsing)

```text
"[Player A]'s Request — [Item Name] ×[Quantity]
Reward: [Offer]g
Posted: [X hari lalu] | Expires: [7 hari sejak posting]"
```

### Pemenuhan (Player B)

```text
[BOARD CLERK — Sharp-Mercantile]
NPC: "You've got what [Player A] is after? Hand it here, I'll verify and pay out — minus nothing on your end, the fee already came out of their pocket."
  > Memverifikasi item di inventory sesuai listing
NPC: "Confirmed. [Offer]g transferred. Pleasure doing business — for me, anyway, I didn't lift a finger."
```

**Catatan:** sesuai Economy doc §Gold Sources, *pemosting* membayar `Item_Base_Value + 10% tax` dan *pemenuh* menerima nilai dasar item (pajak sudah dipotong saat posting, bukan saat pemenuhan) — baris Board Clerk di atas sengaja ditulis untuk memperjelas timing ini, karena "ke mana perginya 10% saya" adalah pertanyaan support yang bisa diperkirakan kalau tidak dijelaskan.

---

# 🎨 ATURAN VARIASI DIALOG PER RAS

Alih-alih menulis dialog ~3x lipat, NPC Demon City dan Elf City memakai ulang **struktur role + state yang sama** seperti contoh Human City di atas, dengan pergeseran nada yang konsisten berikut:

| Elemen | Human City | Demon City | Elf City |
|---|---|---|---|
| **Sapaan default** | "Adventurer" | "Blood" / "Fighter" (tersirat rasa hormat yang harus diperoleh) | "Wanderer" / "Seedling" (penuh sayang, sedikit merendahkan) |
| **Framing pertempuran** | Tugas, perlindungan | Kekuatan, bertahan hidup bagi yang mampu | Kebutuhan, dengan enggan |
| **Bicara soal System/Level** | Penuh hormat (sesuai lore Age of Settlement) | Bukti kelayakan ("System doesn't lie about strength") | Sedikit berjarak ("alat, bagaimanapun asal-usulnya") |
| **Nada setara Guild Master** | Formal-Proud (Alaric) | Brash-Aggressive, menguji pemain secara verbal dulu sebelum menerima | Serene-Distant, tidak terburu-buru bahkan saat quest mendesak |
| **Panjang kalimat khas** | Sedang, lengkap | Pendek, terpotong | Lebih panjang, melebar |

**Contoh penerapan — pembuka Quest 1 versi setara Guild Master Demon City:**

> "New blood. The System marked you before you finished walking through that gate — I felt the ledger shift. Question is whether you're worth the ink. Let's find out." → struktur AVAILABLE/IN PROGRESS/READY sama seperti tree Alaric, hanya nada bicaranya berbeda.

---

# 🔒 GATING REPUTASI & STATUS CRIMINAL

Menghubungkan dialog langsung ke Master Bible §PvP & Criminal System, supaya penulis/dev tidak perlu menebak bagaimana seharusnya NPC bereaksi:

| Status Pemain | Perilaku NPC Utility | Perilaku NPC Quest | Perilaku NPC Lore |
|---|---|---|---|
| **Normal** | Akses toko penuh | Akses quest penuh | Dialog penuh |
| **Criminal (level rendah)** | Toko tetap buka (sesuai Master Bible: hanya *Player Shop* yang melarang Criminal) | Tab bounty di Quest Board disamarkan untuk visibilitas bounty diri sendiri; quest lain tidak terpengaruh | Tidak terpengaruh — lore tidak menghakimi |
| **Criminal (level tinggi / berulang)** | Sama seperti di atas, tapi ditambah satu bark: *"Make it quick."* (NPC Gruff-Warm/Brash) atau *"...I'd rather you didn't linger."* (NPC Warm-Nurturing) | Quest Giver yang berafiliasi Guild (Guild Master, Reward Officer) menolak quest baru sampai Criminal Rehabilitation (Master Bible) selesai: *"Guild doesn't hand work to a marked blade. Clean your name first."* | Tidak terpengaruh |
| **Reputasi Guild tinggi** (dari penyelesaian quest berulang — sistem ringan baru, lihat catatan) | Bark diskon: *"For you? Fine, I'll round down."* | Guild Master memberi satu baris pengakuan idle di milestone reputasi tertentu, tanpa perubahan mekanik | Tidak terpengaruh |

**Catatan soal Guild Reputation:** Master Bible saat ini belum mendefinisikan stat reputasi numerik di luar reputasi Guild (level guild, bukan level pemain) dan reputasi Blacksmith yang disebut di side quest "Apprentice's Request" di atas. Perlakukan reputasi per-NPC (seperti diskon 5% milik Torv di reputasi 50) sebagai **state flavor lokal yang terikat ke NPC tersebut** — sekadar counter sederhana per pemain per NPC, bukan sistem global baru — supaya tidak perlu bagian baru di Progression System Master Bible.

---

# ✅ CHECKLIST IMPLEMENTASI

- [ ] Bangun UI dialogue tree yang mendukung model 5-state (§3) dengan percabangan opsi
- [ ] Implementasikan Personality Tag sebagai metadata NPC (mengarahkan style guide voice-line untuk penulis di masa depan, bukan sistem yang kaku)
- [ ] Hubungkan Quest Board Clerk ke listing Player-Generated Quest (alur posting/pemenuhan §10)
- [ ] Implementasikan counter reputasi lokal per-NPC (ringan, lihat catatan §12) untuk hook diskon ala Blacksmith
- [ ] Lengkapi ~24 NPC Utility/Quest yang tersisa (Demon + Elf City) memakai tabel Variasi Ras §11 terhadap template Human City di §4-5
- [ ] Tulis teks lengkap chain "Awakening" untuk pembuka Demon City dan Elf City (struktur 4-beat sama seperti §8)
- [ ] Putuskan rekaman VO atau text-only (memengaruhi apakah bark pool di §7 butuh varian audio)
- [ ] Cross-check setiap angka gold/EXP yang disebut di dialog quest terhadap Economy Balancing doc §Quest Rewards sebelum dikunci final

---

**End of NPC Dialogue & Quest Text Document**

Terakhir Diperbarui: September 2026

Review Berikutnya: Setelah Phase 2 (Core Systems) — implementasi sistem quest
