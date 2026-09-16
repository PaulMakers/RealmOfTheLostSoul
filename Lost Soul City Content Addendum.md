# 🏙️ Lost Soul — City Content Addendum

**Status:** Perluasan konten kota (profesi player-driven, sosial, gold sink) di atas fondasi Master Bible yang sudah lock

**Dokumen pendamping:** `LostSoul.md` (§ World & Geography, § Gathering & Crafting, § Guild System, § NPC Framework), `Lost Soul Economy Balancing.md` (§ Gold Sources, § Inflation Prevention), `Lost Soul NPC Dialog & Quest Text.md` (§ Dialog NPC Utility)

**Cakupan:** 4 profesi player-driven baru (Blacksmith direvisi jadi player-driven, + Alchemist, Chef, Jeweler), Cafe, Colosseum, Trade Post netral, Guild Bank fisik, revisi Pasar — plus dampaknya ke 3 dokumen sebelumnya

**Catatan bahasa:** Nama tempat, label UI, dan contoh dialog tetap Bahasa Inggris (konsisten dengan 3 dokumen sebelumnya). Penjelasan dan catatan desain dalam Bahasa Indonesia.

---

## 📋 DAFTAR ISI

1. [Filosofi: Kenapa Player-Driven](https://claude.ai/chat/0a58adef-f145-4c99-bed2-64b8c59f154e#philosophy)
2. [Sistem Profesi (Umum)](https://claude.ai/chat/0a58adef-f145-4c99-bed2-64b8c59f154e#professions-overview)
3. [Blacksmith — Revisi Jadi Player-Driven](https://claude.ai/chat/0a58adef-f145-4c99-bed2-64b8c59f154e#blacksmith)
4. [Alchemist (Baru)](https://claude.ai/chat/0a58adef-f145-4c99-bed2-64b8c59f154e#alchemist)
5. [Chef (Baru)](https://claude.ai/chat/0a58adef-f145-4c99-bed2-64b8c59f154e#chef)
6. [Jeweler (Baru)](https://claude.ai/chat/0a58adef-f145-4c99-bed2-64b8c59f154e#jeweler)
7. [Cafe](https://claude.ai/chat/0a58adef-f145-4c99-bed2-64b8c59f154e#cafe)
8. [Colosseum](https://claude.ai/chat/0a58adef-f145-4c99-bed2-64b8c59f154e#colosseum)
9. [Trade Post Netral](https://claude.ai/chat/0a58adef-f145-4c99-bed2-64b8c59f154e#trade-post)
10. [Guild Bank — Lokasi Fisik](https://claude.ai/chat/0a58adef-f145-4c99-bed2-64b8c59f154e#guild-bank)
11. [Revisi Pasar (Market District)](https://claude.ai/chat/0a58adef-f145-4c99-bed2-64b8c59f154e#market-revision)
12. [Dampak ke Economy Balancing](https://claude.ai/chat/0a58adef-f145-4c99-bed2-64b8c59f154e#economy-impact)
13. [Dampak ke NPC Dialog Doc](https://claude.ai/chat/0a58adef-f145-4c99-bed2-64b8c59f154e#npc-impact)
14. [Dampak ke Map Structure](https://claude.ai/chat/0a58adef-f145-4c99-bed2-64b8c59f154e#map-impact)
15. [Checklist Implementasi](https://claude.ai/chat/0a58adef-f145-4c99-bed2-64b8c59f154e#checklist)

---

# 🎯 FILOSOFI: KENAPA PLAYER-DRIVEN

<a name="philosophy"></a>

Ini perluasan langsung dari Core Design Pillar **Community** dan **Freedom** yang sudah ada di Master Bible — bukan sistem baru dari nol. Prinsipnya:

1. **NPC = safety net, bukan jalur utama.** Pemain baru tetap bisa beli dari NPC (harga lebih mahal, kualitas lebih kaku), tapi pemain yang serius akan lebih untung lewat ekonomi sesama pemain.
2. **Setiap profesi butuh profesi lain.** Blacksmith butuh Miner, Chef butuh Herbalist/monster drop, Alchemist butuh keduanya — supaya nggak ada satu profesi yang self-sufficient dan ekonomi tetap saling terhubung.
3. **Gold sink baru harus proporsional**, tidak boleh mengubah target Inflation Prevention (`<2%/bulan`) yang sudah dikunci di Economy doc — semua angka baru di dokumen ini dirancang supaya total gold sink tetap di rentang 30-40% yang sudah ditetapkan.

---

# 🛠️ SISTEM PROFESI (UMUM)

<a name="professions-overview"></a>

## Struktur Umum (berlaku ke 4 profesi di bawah)

- **Profesi Level 1-50** (paralel dengan struktur Gathering yang sudah ada di Master Bible §Gathering)
- Tidak eksklusif — 1 karakter bisa punya beberapa profesi sekaligus, tapi **efisiensi menurun setelah profesi ke-2** (soft cap ala stat allocation, supaya spesialisasi tetap menarik): Profesi ke-1 & ke-2 = 100% efisiensi, profesi ke-3+ = 70%
- **Reputasi Profesi lokal** (per NPC/per pelanggan tetap) — pola yang sama seperti reputasi Blacksmith Torv yang sudah disebut di NPC Dialog doc §12, diperluas ke semua profesi
- **Blueprint/Resep** didapat dari: quest awal (dasar), NPC trainer (menengah), monster drop Rank B+ (langka), player lain yang menjual resep hasil discovery (opsional, endgame)

## Kualitas Hasil Crafting

Bukan cuma "berhasil/gagal" (Master Bible §Crafting sudah sebut success/failure rate) — ditambah **tier kualitas hasil**, supaya crafter berpengalaman punya keunggulan nyata dibanding NPC:

| Roll Kualitas Peluang Dasar Efek  |     |                                                  |
| --------------------------------- | --- | ------------------------------------------------ |
| Standard                          | 70% | Stat sesuai baseline resep                       |
| Fine                              | 20% | +5-10% stat utama                                |
| Masterwork                        | 8%  | +15-20% stat utama, border visual khusus         |
| Flawless                          | 2%  | +25% stat utama + 1 slot enchant kosong tambahan |

**Peluang Fine/Masterwork/Flawless naik seiring Profession Level** — ini insentif utama kenapa pemain mau naikin profesi alih-alih beli sekali lalu berhenti.

---

# ⚒️ BLACKSMITH — REVISI JADI PLAYER-DRIVEN

<a name="blacksmith"></a>

## Perubahan dari Master Bible Saat Ini

Sebelumnya: Torv Ironhand (NPC) adalah satu-satunya sumber upgrade senjata/armor. **Sekarang:**

- **Player Blacksmith** bisa craft & upgrade senjata/armor dari resep + material (Ore, Refined Ore, dst. — sudah ada di Economy doc §Material Costs)
- **Torv Ironhand tetap ada**, tapi perannya berubah jadi:
  1. Menjual harga Standard-quality doang, **20% lebih mahal** dari harga Equipment Pricing Curve di Economy doc (dulu itu harga acuan utama, sekarang jadi harga "malas nunggu crafter")
  2. Trainer awal — mengajarkan resep dasar (Common-Uncommon tier)
  3. NPC quality-control opsional: pemain bisa bayar kecil untuk "appraise" hasil craft player lain sebelum dibeli (mencegah scam kualitas di Player Shop)

## Ekonomi

- Player Blacksmith jual di Player Shop / Market District dengan harga bebas (mengikuti sistem Player Shop yang sudah ada, commission 10%)
- **Gap harga NPC vs Player** jadi insentif alami: NPC 20% lebih mahal + kualitas Standard fix, Player bisa lebih murah + rolling Fine/Masterwork

---

# 🧪 ALCHEMIST (BARU)

<a name="alchemist"></a>

- Craft semua Potion (HP/MP/Buff) yang formulanya sudah ada di Economy doc §Consumable Pricing — sekarang bisa dibuat pemain, bukan cuma dibeli NPC fix-price
- Bahan: Herb (Herbalism) + material Rank monster tertentu untuk tier lebih tinggi
- **Trainer:** NPC baru — **"APOTHECARY LYRA"** (Human City, Temple District — masuk akal berdampingan dengan Sister Elowen karena sama-sama elemen support), personality **Warm-Nurturing** varian sedikit lebih "sharp" soal takaran bahan
- NPC Buy Price tetap ada sebagai fallback, sama seperti Blacksmith — 20% lebih mahal, tanpa varian kualitas

---

# 🍳 CHEF (BARU)

<a name="chef"></a>

- Bahan: material monster drop (daging, dsb — belum ada di list sekarang, perlu ditambahkan sebagai drop type baru di Monster Drops) + Herbalism
- Hasil: **Food Buff** — mekanik mirip Stat Buff Potion tapi **durasi lebih lama (2 jam vs 1 jam Potion)**, efek lebih kecil per stat, dan **hanya 1 Food Buff aktif sekaligus** (tidak bisa stack dengan Food Buff lain, tapi bisa stack dengan Potion buff) — supaya Chef jadi jalur buff komplementer, bukan menggantikan Alchemist
- **Chef bekerja di Cafe** (lihat §7) — ini yang bikin Cafe punya fungsi mekanik, bukan cuma dekorasi

---

# 💍 JEWELER (BARU)

<a name="jeweler"></a>

- Craft Ring/Amulet/Belt (Accessory Pricing di Economy doc jadi harga NPC fallback, sama pola dengan profesi lain)
- Bahan: gem hasil Mining tier tinggi (perlu ditambahkan sebagai sub-kategori baru di Gathering — gem terpisah dari Ore biasa, drop rate lebih rendah)
- Fitur unik Jeweler: **Socketing** — pemain bisa titip equipment ke Jeweler untuk pasang gem tambahan (bukan cuma bikin accessory baru), jadi ada gold sink jasa (fee per socket, dibayar ke Jeweler player, bukan sistem)

---

# ☕ CAFE

<a name="cafe"></a>

## Fungsi

- **Tempat kerja Chef** (lihat §5) — dapur/counter untuk crafting Food Buff
- **Hangout/RP spot** — kursi, meja, dekorasi ambient, NPC bark-only (pola sama seperti bark pool di NPC Dialog doc §7)
- **Rumor board** ringan di dekat pintu masuk — perpanjangan Town Crier, tempat "gosip" soal Central Mystery tersebar (ide dari sesi sebelumnya) — teks flavor, tidak ada mekanik quest baru di sini, biar Cafe tetap ringan

## Lokasi

1 Cafe per kota (3 total), ditaruh di **Residential District** yang sudah ada di Map Structure (bukan zona baru) — cukup ekstensi dari zona existing.

---

# 🏟️ COLOSSEUM

<a name="colosseum"></a>

## Perubahan dari Duel Arena

Duel Arena yang sekarang cuma disebut sekilas di War Plaza (Demon City) **di-upgrade jadi Colosseum**, dan dijadikan fitur di **semua 3 kota** (bukan cuma Demon City), supaya konsisten dan tiap ras dapat identitas Colosseum sendiri (arsitektur beda per tema kota).

## Dua Mode

| Mode Mekanik Reward   |                                                                                  |                                                                         |
| --------------------- | -------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| **Duel Kasual**       | Sistem existing (consensual, no stake) — tidak berubah                           | Tidak ada (bragging rights)                                             |
| **Turnamen Mingguan** | Bracket 8/16/32 pemain, terjadwal (mis. tiap Sabtu), 1 kemenangan = maju bracket | Gold pool dari taruhan penonton (lihat bawah) + title kosmetik non-stat |

## Sistem Taruhan Penonton (Gold Sink Baru)

- Penonton bisa pasang taruhan gold ke salah satu petarung sebelum match mulai
- **System commission 15%** dari total pool taruhan (gold sink baru, masuk kategori sama dengan Taxes & Commissions di Economy doc §Inflation Prevention)
- Sisa pool dibagi ke penonton yang menang tebakan, proporsional ke taruhan mereka
- **Batas taruhan per match:** 5000 gold per orang (mencegah wallet besar mendominasi/manipulasi hasil taruhan)

## Kenapa Ini Aman untuk Ekonomi

Karena taruhan cuma memindahkan gold antar-pemain (minus commission), efeknya net **deflationary** (mengurangi total gold beredar) — cocok jadi salah satu instrumen di "Action Triggers" Economy doc kalau suatu saat butuh gold sink tambahan tanpa naikin pajak dasar.

---

# 🏪 TRADE POST NETRAL

<a name="trade-post"></a>

- Lokasi baru: **di dalam Central Hunting Ground**, dekat Hunter's Outpost yang sudah ada (bukan zona terpisah, ekstensi dari zona existing — sama pola dengan Cafe)
- Fungsi: tempat Human/Demon bisa trading tanpa masuk kota lawan (Elf tetap independen seperti biasa, bisa akses juga)
- **Tidak ada Player Shop di sini** (itu tetap eksklusif Human City/Demon City sesuai Master Bible) — Trade Post cuma untuk **Trade Window langsung antar pemain** (barter real-time, pola 3 detik lock yang sudah ada di UI/UX doc)
- **Narasi:** cocok jadi elaborasi kecil dari "Cold War tapi ekonomi tetap jalan" — bisa ditambahkan 1 baris NPC Town Crier baru soal ini kalau mau (opsional, tidak wajib untuk versi awal)

---

# 🏦 GUILD BANK — LOKASI FISIK

<a name="guild-bank"></a>

Sebelumnya cuma disebut sebagai fitur (shared storage) tanpa lokasi. Sekarang: **di dalam Guild Hall** tiap kota (Adventurer Guild Hall / Demon Guild Hall / Elf Guild Hall — zona yang sudah ada di Map Structure), sebagai ruangan terpisah dari Quest Board area.

---

# 🏬 REVISI PASAR (MARKET DISTRICT)

<a name="market-revision"></a>

Market District yang sudah ada di Map Structure sekarang dipastikan berfungsi sebagai:

- **Lokasi fisik Player Shop** (sebelumnya cuma disebut "located in Human City, Demon City" tanpa zona spesifik — sekarang eksplisit: Market District)
- **Booth Profesi** — Blacksmith/Alchemist/Jeweler player bisa "rent" booth kecil di Market District untuk jualan (bukan wajib, alternatif dari Player Shop biasa/Guild Shop), memberi rasa "pasar ramai" secara visual sesuai target 1000 concurrent

---

# 💰 DAMPAK KE ECONOMY BALANCING

<a name="economy-impact"></a>

| Perubahan Dokumen yang Perlu Diupdate                                     |                                                                                                                                                 |
| ------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| NPC Buy Price Blacksmith/Alchemist/Jeweler naik 20% dari harga acuan lama | §Equipment Pricing Curve, §Consumable Pricing, §Accessory Pricing — tandai sebagai "NPC fallback price", tambah kolom "Player Craft (variable)" |
| Colosseum betting commission 15%                                          | Tambahan baru di §Inflation Prevention → Gold Sinks, sebagai kategori ke-5                                                                      |
| Material baru: monster meat (Chef), gem (Jeweler)                         | §Gold Sources → Gathering, perlu tabel harga NPC baru untuk 2 material ini                                                                      |
| Socketing fee (Jeweler jasa)                                              | Gold sink kecil baru, masuk kategori "Upgrades & Maintenance"                                                                                   |

**Belum perlu ubah target inflasi (<2%/bulan) atau rasio 30-40% gold sink** — perubahan di atas menambah *jenis* sink/source, bukan mengubah skala totalnya. Perlu 1 pass rekalkulasi ringan setelah angka final ditentukan, tapi strukturnya tidak berubah.

---

# 🧙 DAMPAK KE NPC DIALOG DOC

<a name="npc-impact"></a>

| NPC Perubahan                                 |                                                                                                                                                                |
| --------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Torv Ironhand** (Blacksmith)                | Dialog perlu direvisi — dari "satu-satunya tukang upgrade" jadi trainer + fallback mahal. Baris baru: menawarkan appraisal jasa untuk hasil craft player lain. |
| **Apothecary Lyra** (baru, Alchemist trainer) | NPC baru, perlu dialog tree lengkap (pola sama seperti Utility NPC lain di §4 dokumen NPC)                                                                     |
| **Chef trainer** (baru, di Cafe)              | Perlu 1 NPC baru per kota atau 1 NPC keliling — belum diputuskan, tandai sebagai open question                                                                 |
| **Jeweler trainer** (baru)                    | Sama seperti Chef, perlu NPC baru                                                                                                                              |
| **Colosseum Announcer** (baru)                | NPC flavor untuk narasi match/turnamen, bark pool saja (tidak perlu dialogue tree penuh)                                                                       |

---

# 🗺️ DAMPAK KE MAP STRUCTURE

<a name="map-impact"></a>

| Zona Perubahan                                 |                                                                             |
| ---------------------------------------------- | --------------------------------------------------------------------------- |
| Residential District (semua kota)              | +Cafe (ekstensi, bukan zona baru)                                           |
| War Plaza (Demon City) / area setara kota lain | Duel Arena → **Colosseum**, butuh footprint lebih besar dari arena existing |
| Market District (semua kota)                   | +Booth Profesi, dipastikan jadi lokasi fisik Player Shop                    |
| Adventurer/Demon/Elf Guild Hall                | +ruangan Guild Bank terpisah                                                |
| Hunter's Outpost (Central Hunting Ground)      | +Trade Post (ekstensi zona existing)                                        |

**Catatan untuk Map Blockout Spec nanti:** Colosseum adalah satu-satunya item di atas yang butuh **footprint baru signifikan** (bukan cuma nambah furniture di zona existing) — perlu dipikirkan ukurannya saat bikin spec studs per kota.

---

# ✅ CHECKLIST IMPLEMENTASI

<a name="checklist"></a>

- [ ] Kunci angka NPC fallback price (20% markup) untuk Blacksmith/Alchemist/Jeweler
- [ ] Kunci tabel kualitas crafting (Standard/Fine/Masterwork/Flawless) dan kurva peluang per Profession Level
- [ ] Tambahkan material baru (monster meat, gem) ke tabel Gathering & Monster Drops
- [ ] Tulis dialog lengkap Apothecary Lyra + trainer Chef/Jeweler (pola sama dengan Utility NPC §4)
- [ ] Revisi dialog Torv Ironhand sesuai peran barunya
- [ ] Putuskan siapa Chef/Jeweler trainer (NPC baru per kota, atau 1 NPC keliling)
- [ ] Kunci angka Colosseum betting (commission 15%, cap 5000 gold/orang) — cross-check dengan target inflasi Economy doc
- [ ] Tentukan footprint Colosseum di Map Blockout Spec (item paling besar dari addendum ini)
- [ ] Update UI Player Shop untuk menampilkan badge "Player Craft" vs "NPC Standard" secara visual (rarity/kualitas Fine-Flawless perlu ikon beda dari sistem rarity item biasa)

---

**End of City Content Addendum**

Terakhir Diperbarui: September 2026

Review Berikutnya: Sebelum Map Blockout Spec dimulai (Colosseum butuh keputusan footprint duluan)
