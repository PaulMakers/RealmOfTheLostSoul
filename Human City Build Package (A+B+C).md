# 🏗️ Lost Soul — Human City Build Package

## (A) Exact Coordinates + (B) Modular Kit Spec + (C) AI Build Prompt Sequence

Dokumen ini adalah lapisan terakhir sebelum (D) eksekusi di Roblox Studio. Semua koordinat pakai origin (0,0,0) = pusat Central Plaza, sumbu X/Z horizontal, Y vertikal — sama seperti yang sudah ditetapkan di Map Construction Specification.

---

# 📋 DAFTAR ISI

1. [A — Koordinat Exact Seluruh Human City](https://claude.ai/chat/0a58adef-f145-4c99-bed2-64b8c59f154e#coords)
2. [B — Modular Building Kit Specification](https://claude.ai/chat/0a58adef-f145-4c99-bed2-64b8c59f154e#kit)
3. [C — AI Build Prompt Sequence](https://claude.ai/chat/0a58adef-f145-4c99-bed2-64b8c59f154e#prompts)

---

# 📍 A — KOORDINAT EXACT SELURUH HUMAN CITY

\<a name="coords">\</a>

## A.1 — District Anchor Points (pusat tiap district)

| District X Z Radius Area  |      |      |    |
| ------------------------- | ---- | ---- | -- |
| Central Plaza             | 0    | 0    | 75 |
| Adventurer Guild          | 0    | 350  | 60 |
| Market District           | 350  | 0    | 80 |
| Residential District      | -350 | 0    | 80 |
| Temple District           | 200  | -300 | 60 |
| Colosseum                 | -200 | -300 | 50 |
| Gathering Hub             | 0    | -450 | 30 |
| South Gate                | 0    | -650 | 20 |

## A.2 — Koordinat Bangunan Individual

**Adventurer Guild (anchor 0, 350):**

```
GuildHall_Main         X=0    Z=350   Rotation=180° (pintu hadap Plaza)   Footprint 60x40
  QuestBoard (interior) X=0    Z=340   (dekat pintu masuk)
  GuildBank_Room        X=10   Z=360   (ruangan terpisah, sisi kanan)
  RewardOfficer_Desk    X=-10  Z=360   (sisi kiri)
  DungeonStairs         X=0    Z=345   (turun ke basement, akses map_06_human_dungeon)

```

**Market District (anchor 350, 0):**

```
MerchantGuild_Hall     X=350  Z=0     Footprint 30x30
PlayerShop_Row (10 stall, 8 studs/stall + 2 stud gap = 100 studs total)
  Stall_01  X=310  Z=40
  Stall_02  X=320  Z=40
  Stall_03  X=330  Z=40
  Stall_04  X=340  Z=40
  Stall_05  X=350  Z=40
  Stall_06  X=360  Z=40
  Stall_07  X=370  Z=40
  Stall_08  X=380  Z=40
  Stall_09  X=390  Z=40
  Stall_10  X=400  Z=40
ProfessionBooth_Row (4 booth, 10 studs/booth + 2 stud gap)
  Booth_Blacksmith  X=320  Z=-40
  Booth_Alchemist   X=332  Z=-40
  Booth_Jeweler     X=344  Z=-40
  Booth_Spare       X=356  Z=-40   (cadangan profesi masa depan)

```

**Residential District (anchor -350, 0):**

```
Inn_MaraThistlewood    X=-390  Z=30   Footprint 25x25
Blacksmith_TorvIronhand X=-310 Z=30   Footprint 20x20
Armorer_SirEdmund      X=-390 Z=-30  Footprint 20x20
Cafe_Main              X=-310 Z=-30  Footprint 20x20

```

**Temple District (anchor 200, -300):**

```
MainTemple             X=200  Z=-300  Footprint 40x40
Apothecary_Lyra        X=240  Z=-280  Footprint 15x15

```

**Colosseum (anchor -200, -300):**

```
Colosseum_Arena        X=-200 Z=-300  Diameter 80 (circular, arena tengah radius 25 + tribun ring 15)
Colosseum_Podium       X=-200 Z=-300  Y=5 (podium announcer, tengah arena)

```

**Gathering Hub (anchor 0, -450):**

```
ToolVendor_OldPemberton X=0   Z=-450  Footprint 10x10

```

**Central Plaza (anchor 0,0):**

```
Fountain_Central       X=0    Z=0    Radius 15
SpawnPoint_Default     X=0    Z=60   (menghadap Utara ke Adventurer Guild)
FastTravel_Placeholder X=15   Z=0    (empty part, isi nanti)

```

## A.3 — Road Network (titik awal → akhir, lebar 12 studs jalan utama / 6 studs sekunder)

```
Road_Plaza_to_Guild        (0,0) → (0,320)      [Utama]
Road_Plaza_to_Market       (0,0) → (320,0)      [Utama]
Road_Plaza_to_Residential  (0,0) → (-320,0)     [Utama]
Road_Plaza_to_Temple       (0,0) → (180,-270)   [Utama]
Road_Plaza_to_Colosseum    (0,0) → (-180,-270)  [Utama]
Road_Plaza_to_Gathering    (0,0) → (0,-420)     [Utama]
Road_Gathering_to_Gate     (0,-420) → (0,-630)  [Utama]
Road_Market_to_Temple      (320,-30) → (220,-260)   [Sekunder]
Road_Residential_to_Colosseum (-320,-30) → (-220,-260) [Sekunder]

```

## A.4 — Map Boundary

```
Bounding Box: X = -700 to 700, Z = -700 to 700 (sesuai 1400x1400 di spec sebelumnya)
Invisible Wall / Terrain Cliff: di seluruh tepi KECUALI South Gate (X=-40 to 40, Z=-660 to -700 → area terbuka menuju Hunting Ground)

```

---

# 🧱 B — MODULAR BUILDING KIT SPECIFICATION

\<a name="kit">\</a>

## B.1 — Komponen Dasar (semua snap ke grid 4 studs)

| Komponen Dimensi (L x T x W, studs) Catatan  |            |                                                          |
| -------------------------------------------- | ---------- | -------------------------------------------------------- |
| Wall\_Straight                               | 8 x 12 x 1 | Unit dasar dinding, dipakai berulang sepanjang perimeter |
| Wall\_Corner                                 | 1 x 12 x 1 | Sambungan sudut 90°                                      |
| Wall\_HalfHeight                             | 8 x 6 x 1  | Untuk pagar/dinding rendah (Market stall, Gathering Hub) |
| Door\_Single                                 | 4 x 8 x 1  | Pintu standar rumah/toko                                 |
| Door\_Double                                 | 8 x 10 x 1 | Pintu Guild Hall, Main Temple                            |
| Window\_Small                                | 3 x 3 x 1  | Rumah tinggal                                            |
| Window\_Arch                                 | 4 x 6 x 1  | Temple, Guild Hall (gaya lebih formal)                   |
| Floor\_Tile                                  | 8 x 1 x 8  | Lantai interior, disusun grid                            |
| Foundation\_Base                             | 8 x 2 x 8  | Alas bangunan sebelum lantai                             |
| Roof\_PitchedSegment                         | 8 x 4 x 8  | Kemiringan 30°, dipakai berulang                         |
| Roof\_FlatSegment                            | 8 x 1 x 8  | Untuk Market stall (atap datar)                          |
| Pillar\_Round                                | 2 x 12 x 2 | Aksen Temple/Guild Hall                                  |
| Stall\_Counter                               | 8 x 3 x 4  | Khusus Player Shop/Profession Booth (open-air)           |

## B.2 — Estimasi Kebutuhan Part per Bangunan (perimeter ÷ 8, dibulatkan ke atas)

```
Inn (25x25):        perimeter 100 → 13 Wall_Straight + 4 Wall_Corner + 1 Door_Single + 6 Window_Small
Blacksmith (20x20): perimeter 80  → 10 Wall_Straight + 4 Wall_Corner + 1 Door_Single + 4 Window_Small
Armorer (20x20):     sama seperti Blacksmith
Cafe (20x20):        sama seperti Blacksmith, +1 Door_Single tambahan (akses dapur)
GuildHall (60x40):   perimeter 200 → 25 Wall_Straight + 4 Wall_Corner + 1 Door_Double + 8 Window_Arch + 4 Pillar_Round
MainTemple (40x40):  perimeter 160 → 20 Wall_Straight + 4 Wall_Corner + 1 Door_Double + 6 Window_Arch + 6 Pillar_Round
Apothecary (15x15): perimeter 60  → 8 Wall_Straight + 4 Wall_Corner + 1 Door_Single + 2 Window_Small
MerchantGuild (30x30): perimeter 120 → 15 Wall_Straight + 4 Wall_Corner + 1 Door_Single + 4 Window_Small
PlayerShop stall (8x8): Stall_Counter only, no full wall (open-air)
ProfessionBooth (10x10): Stall_Counter + Roof_FlatSegment only

```

**Total estimasi part struktural Human City (di luar prop/dekorasi):** ~250-300 part — masih di bawah budget 500 part/district dari Performance Budget.

## B.3 — Snapping & Assembly Rule

```
Semua Wall_Straight disusun dengan origin di sudut kiri-bawah, snap grid 4 studs
Roof_PitchedSegment selalu diletakkan di atas Wall_Straight terakhir tiap sisi, kemiringan menghadap keluar dari pusat bangunan
Foundation_Base wajib di-Union atau grouped sebelum Floor_Tile diletakkan di atasnya (mencegah z-fighting)
Gunakan Model (bukan Union) untuk grouping per bangunan — memudahkan reuse kit ke Demon/Elf City nanti dengan swap material saja

```

---

# 🤖 C — AI BUILD PROMPT SEQUENCE

\<a name="prompts">\</a>

Urutan prompt untuk Roblox Studio Assistant, mengikuti Build Order dari spec sebelumnya. Tiap prompt dirancang **spesifik** (sesuai rekomendasi Roblox: hindari instruksi besar/vague) dan menyertakan **self-check** sebelum lanjut ke prompt berikutnya.

### Prompt 1 — Terrain & Boundary

```
Buat terrain flat dengan sedikit variasi elevation (Y=0 sampai Y=15) di area bounding box X=-700 to 700, Z=-700 to 700. Material dasar Grass. Tambahkan invisible wall di seluruh tepi boundary KECUALI area X=-40 to 40, Z=-660 to -700 (South Gate, biarkan terbuka). Setelah selesai, laporkan jumlah part yang dipakai untuk boundary wall.

```

### Prompt 2 — Road Network

```
Buat jalan Cobblestone mengikuti 9 segmen berikut (lebar 12 studs untuk yang ditandai [Utama], 6 studs untuk [Sekunder]): [tempel tabel A.3]. Setiap jalan harus berupa Part memanjang dengan CFrame mengikuti garis lurus antar 2 titik yang diberikan. Setelah selesai, screenshot top-down view untuk verifikasi tidak ada jalan yang terputus atau tumpang tindih.

```

### Prompt 3 — District Footprint (bounding box kosong)

```
Buat 7 Part transparan (Transparency=0.8, CanCollide=false) sebagai penanda area district sesuai tabel A.1 (anchor point + radius). Beri nama sesuai format District_Name_Footprint. Ini hanya untuk verifikasi jarak sebelum bangunan asli dibuat — cek tidak ada footprint yang overlap satu sama lain.

```

### Prompt 4 — Modular Building Kit

```
Buat 13 model komponen dasar sesuai tabel B.1 (Wall_Straight, Wall_Corner, Door_Single, dst — dimensi persis seperti tabel), simpan masing-masing sebagai Model di folder ReusableKit/HumanCity. Material dinding: Brick warna coklat krem. Material atap: WoodPlanks coklat tua. Setelah selesai, tampilkan daftar semua model yang berhasil dibuat.

```

### Prompt 5 — Assembly Bangunan (ulangi per bangunan)

```
Menggunakan komponen dari folder ReusableKit/HumanCity, susun bangunan "[Nama Bangunan]" di koordinat [X, Z] dari tabel A.2, dengan footprint [ukuran], mengikuti estimasi kebutuhan part di tabel B.2. Gunakan naming convention District_BuildingType_Number (contoh: Residential_Inn_01). Group seluruh part bangunan ini menjadi satu Model. Setelah selesai, laporkan total part count bangunan ini.

```

*(Jalankan prompt ini 12 kali, satu per bangunan di tabel A.2 — Guild Hall, Merchant Guild, 10 Player Shop stall bisa digabung jadi 1 prompt loop, 4 Profession Booth, Inn, Blacksmith, Armorer, Cafe, Main Temple, Apothecary, Colosseum Arena, Tool Vendor stall)*

### Prompt 6 — Landmark

```
Tambahkan 4 landmark sesuai spesifikasi: Adventurer Guild Tower (Y=0 to Y=150, di atas GuildHall_Main), Colosseum Outer Wall (bentuk melingkar mengelilingi Colosseum_Arena), Main Temple Spire (Y=0 to Y=130, dengan efek glow ringan warna keemasan), Central Plaza Fountain (sudah dibuat di Prompt 5 sebagai bagian Central Plaza, verifikasi tingginya Y=0-20).

```

### Prompt 7 — NPC Placeholder

```
Buat 16 Part berbentuk humanoid placeholder (bisa pakai Block dengan proporsi kasar humanoid, warna berbeda per kategori: biru=Utility, hijau=Quest, ungu=Lore, abu=Flavor) di koordinat sesuai tabel NPC Locations dari Map Construction Specification §8. Beri nama format NPC_[Nama]_[Role]. Ini placeholder visual saja — logic dialog dikerjakan terpisah nanti.

```

### Prompt 8 — Spawn & Teleport

```
Buat SpawnLocation di koordinat (0, Y_terrain, 60) menghadap Utara (Rotation Y=180°), radius aman 20 studs (no collision object dalam radius ini). Tambahkan 1 Part kosong bernama "FastTravel_Placeholder" di (15, Y_terrain, 0). Tambahkan trigger part di South Gate (area X=-40 to 40, Z=-660 to -700) bernama "Exit_ToHuntingGround" untuk nanti dihubungkan ke TeleportService.

```

### Prompt 9 — Lighting Pass

```
Set Lighting.ClockTime = 14, Lighting.Ambient ke warm soft tone. Tambahkan 1 PointLight/SpotLight di interior tiap bangunan (maksimal 1 per bangunan sesuai Performance Budget). Tambahkan efek glow ringan di Main Temple Spire. Verifikasi tidak ada lebih dari 20 dynamic light source total di seluruh map.

```

### Prompt 10 — Performance & Streaming Check

```
Aktifkan Workspace.StreamingEnabled = true, StreamingTargetRadius = 512, StreamingMinRadius = 128. Hitung total part count seluruh Human City dan laporkan per district. Jika ada district melebihi 500 part, sarankan bagian mana yang bisa di-Union atau diganti MeshPart.

```

### Prompt 11 — Playtest Checklist (manual, dilakukan kamu bukan AI)

```
Jalankan Play mode. Jalan dari SpawnLocation ke tiap 7 district, lalu ke South Gate. Cek: (1) tidak ada gap terrain, (2) tidak ada collision aneh antar bangunan, (3) semua NPC placeholder terlihat di posisi benar, (4) FPS stabil (gunakan Microprofiler jika perlu).

```

---

**Catatan penting untuk eksekusi:** jalankan prompt secara berurutan (1→11), jangan skip — tiap prompt bergantung pada hasil prompt sebelumnya (mis. Prompt 5 butuh kit dari Prompt 4 sudah ada). Kalau AI Assistant gagal di satu prompt, perbaiki dulu sebelum lanjut, jangan lompat ke prompt berikutnya dengan asumsi hasil sebelumnya benar.

**End of Build Package.** Setelah Prompt 11 lolos playtest, dokumen A.2 (koordinat bangunan) dan B (kit) tinggal di-duplikasi dengan swap Material Rules untuk Demon City & Elf City — struktur road/district anchor (A.1, A.3) bisa dipertahankan sebagai template atau disesuaikan sedikit per identitas ras.
