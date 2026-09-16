# 🏘️ Lost Soul — Map Visual Style Bible (Human City)

**Beda dengan dokumen sebelumnya:** Map Construction Specification mengunci LAYOUT (grid, district, ukuran zona), Human City Build Package mengunci STRUKTUR (koordinat exact, dimensi modular kit, urutan build prompt). Dokumen ini mengunci **RUPA DUNIA** — bentuk, proporsi, warna, material, dan densitas dekorasi setiap komponen fisik di Human City, supaya AI tidak berimprovisasi soal "rumahnya kayak gimana" atau "warnanya apa" saat Prompt 4 & 5 dari Build Package dieksekusi.
**Hubungan dengan UI Visual Style Bible:** dokumen itu mengunci identitas visual **UI/System overlay** ("Forged Adventurer's Ledger" — parchment hangat + metal tertempa). Dokumen ini adalah **saudara kandungnya untuk dunia nyata (world art)** — palet warna di sini SENGAJA berasal dari keluarga hue yang sama (coklat hangat, krem, emas-tembaga) supaya transisi UI ↔ dunia terasa satu identitas, tapi nilai hex-nya **tidak selalu identik 1:1** karena material dunia (batu, kayu, kanvas) butuh look yang lebih fisik/natural, bukan flat digital panel. Satu-satunya token yang **benar-benar dipakai ulang persis** dari UI Visual Style Bible adalah `$border-metal` (#C9A25C) dan `$border-metal-dark` (#8A6B35) — dipakai di dunia untuk semua aksen metal tertempa (lamp, hinge, sign bracket, roof trim), supaya ada 1 warna "jangkar" yang benar-benar sama antara UI dan dunia. Warna Rarity/Element dari UI Visual Style Bible **juga dipakai ulang persis** di dunia, tapi HANYA untuk item drop glow/border di ground — TIDAK untuk mengecat bangunan atau props (supaya pemain tidak salah baca bangunan sebagai indikator rarity).
**Identitas Visual Human City (1 kalimat):** *"Kota Pandai Besi yang Rapi"* — medieval terstruktur, batu bata krem + kayu oak gelap + aksen tembaga, jalan rapi grid, tidak kumuh dan tidak liar (beda arah dari Demon City yang nanti lebih agresif/gelap, dan Elf City yang nanti lebih organik/alami) — konsisten dengan deskripsi Master Bible §World & Geography: *"Kingdom, structured monarki/council"*.

---

# 📋 DAFTAR ISI

1. [Prinsip & Aturan Konsistensi](https://claude.ai/chat/7ba1179b-66fb-4851-bd13-a6d6144b0ffb#principles)
2. [Master Material & Color Palette (Dunia)](https://claude.ai/chat/7ba1179b-66fb-4851-bd13-a6d6144b0ffb#palette)
3. [Building Silhouette & Proportion per Tier](https://claude.ai/chat/7ba1179b-66fb-4851-bd13-a6d6144b0ffb#silhouette)
4. [Roof Style Guide](https://claude.ai/chat/7ba1179b-66fb-4851-bd13-a6d6144b0ffb#roof)
5. [Window Style Guide](https://claude.ai/chat/7ba1179b-66fb-4851-bd13-a6d6144b0ffb#window)
6. [Door Style Guide](https://claude.ai/chat/7ba1179b-66fb-4851-bd13-a6d6144b0ffb#door)
7. [Wall & Stone Style Guide](https://claude.ai/chat/7ba1179b-66fb-4851-bd13-a6d6144b0ffb#wall)
8. [Fence & Railing Style](https://claude.ai/chat/7ba1179b-66fb-4851-bd13-a6d6144b0ffb#fence)
9. [Market Stall & Profession Booth Style](https://claude.ai/chat/7ba1179b-66fb-4851-bd13-a6d6144b0ffb#stall)
10. [Street Furniture](https://claude.ai/chat/7ba1179b-66fb-4851-bd13-a6d6144b0ffb#furniture)
11. [Lamp / Light Fixture Style](https://claude.ai/chat/7ba1179b-66fb-4851-bd13-a6d6144b0ffb#lamp)
12. [Signage System](https://claude.ai/chat/7ba1179b-66fb-4851-bd13-a6d6144b0ffb#signage)
13. [Vegetation](https://claude.ai/chat/7ba1179b-66fb-4851-bd13-a6d6144b0ffb#vegetation)
14. [Texture Density Rules](https://claude.ai/chat/7ba1179b-66fb-4851-bd13-a6d6144b0ffb#texture)
15. [Decoration Density Rules (per District)](https://claude.ai/chat/7ba1179b-66fb-4851-bd13-a6d6144b0ffb#decoration)
16. [Per-District Visual Summary Table](https://claude.ai/chat/7ba1179b-66fb-4851-bd13-a6d6144b0ffb#district)
17. [Token Mapping Table (Material Reference)](https://claude.ai/chat/7ba1179b-66fb-4851-bd13-a6d6144b0ffb#tokenmap)
18. [AI Apply Prompt](https://claude.ai/chat/7ba1179b-66fb-4851-bd13-a6d6144b0ffb#prompt)

---

# 🎯 PRINSIP & ATURAN KONSISTENSI

<a name="principles"></a>

```
1. Semua bentuk WAJIB tersusun dari komponen Modular Building Kit (§B Build Package) — dokumen ini TIDAK menambah komponen baru,
   hanya menentukan bagaimana komponen yang sudah ada (Wall_Straight, Roof_PitchedSegment, dst.) diberi warna/material/kombinasi
   per tier bangunan.
2. Grid 4 studs dari Build Package tetap berlaku untuk SEMUA prop dekorasi baru yang menggunakan komponen kit atau primitif sederhana yang diizinkan (lamp, fence, barrel, dst.) — supaya tidak ada
   elemen "mengambang" di luar grid yang sudah dikunci.
3. Setiap district punya "tier visual" (lihat §3) yang menentukan seberapa ornate/plain, bukan district yang menentukan
   material secara acak — supaya kalau ada bangunan baru ditambah nanti (mis. dari City Content Addendum), AI tinggal
   mencocokkan ke tier yang sesuai, bukan menebak ulang dari nol.
4. Warna world TIDAK memakai hex UI secara acak — hanya `$border-metal` dan `$border-metal-dark` yang dipakai ulang persis
   (aksen metal, lihat §2). Warna Rarity/Element UI HANYA dipakai ulang untuk glow item drop di ground, tidak untuk
   mengecat struktur bangunan atau props (mencegah pemain salah baca bangunan sebagai indikator rarity/element).
5. Setiap bangunan baru dari City Content Addendum (Cafe, Colosseum, Trade Post, Guild Bank, Profession Booth) HARUS
   dipetakan ke salah satu tier di §3 — tidak boleh jadi tier baru sendiri, supaya kota tetap terasa satu kesatuan
   visual meskipun kontennya terus bertambah.

```

---

# 🎨 MASTER MATERIAL & COLOR PALETTE (DUNIA)

<a name="palette"></a>

## Palet Inti — Struktur Bangunan

| Token Hex Roblox Material Penggunaan |         |            |                                                                                                               |
| ------------------------------------ | ------- | ---------- | ------------------------------------------------------------------------------------------------------------- |
| `$world-wall-primary`                | #D8C7A1 | Brick      | Dinding utama semua bangunan (Wall\_Straight, Wall\_Corner) — "batu bata krem hangat"                         |
| `$world-wall-secondary`              | #6B4A2E | WoodPlanks | Aksen half-timber (balok kayu diagonal/vertikal di permukaan dinding) — HANYA Tier Residensial/Utility & Cafe |
| `$world-stone-foundation`            | #8A8272 | Slate      | Foundation\_Base — semua bangunan tanpa kecuali, kesan "berdiri di atas batu"                                 |
| `$world-stone-civic`                 | #A69C89 | Concrete   | Dinding Tier Civic/Sacred (Guild Hall, Main Temple, Colosseum) — batu potong lebih halus dari Foundation      |
| `$world-roof-primary`                | #5C3A21 | WoodPlanks | Roof\_PitchedSegment — semua bangunan bertier Residensial/Utility/Civic                                       |
| `$world-roof-flat`                   | #4A3B2A | Fabric     | Roof\_FlatSegment — HANYA Market stall & Profession Booth (kesan kanvas/terpal, bukan kayu solid)             |

## Palet Aksen Metal (dipakai ulang persis dari UI Visual Style Bible)

| Token Hex Penggunaan |         |                                                                                                    |
| -------------------- | ------- | -------------------------------------------------------------------------------------------------- |
| `$border-metal`      | #C9A25C | Roof trim/ridge cap Tier Civic+, hinge pintu, bracket signage, lamp post fitting, finial Colosseum |
| `$border-metal-dark` | #8A6B35 | Shadow/rangka bawah metal, rangka lamp post, engsel pintu berat (Door\_Double)                     |

## Palet Kayu & Kain (Furniture, Stall, Signage)

| Token Hex Penggunaan    |         |                                                         |
| ----------------------- | ------- | ------------------------------------------------------- |
| `$world-wood-furniture` | #4A3524 | Bench, crate, barrel, Stall\_Counter, papan signage     |
| `$world-fabric-neutral` | #E8DCC4 | Awning/kanvas netral (Market umum, bukan booth profesi) |

## Palet Kanvas Booth Profesi (fungsional, BUKAN warna Rarity/Element — lihat Prinsip #4)

| Profesi Hex Kanvas Alasan Pemilihan |                                                         |                                                                                          |
| ----------------------------------- | ------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| Blacksmith Booth                    | #8C3B2E (merah bata tua)                                | Asosiasi "api tungku", beda jauh dari warna Fire element (#E85C3D) supaya tidak tertukar |
| Alchemist Booth                     | #4F7A4F (hijau lumut)                                   | Asosiasi "herbal/ramuan", beda dari Earth element (#7A9B4F) — lebih gelap/muted           |
| Jeweler Booth                       | #4A3B6B (ungu tua keabuan)                              | Asosiasi "barang berharga", beda dari Epic rarity (#A64CD9) — jauh lebih muted/gelap     |
| Player Shop umum (10 stall)         | `$world-fabric-neutral` #E8DCC4 + strip `$border-metal` | Netral supaya tidak bersaing visual dengan 3 booth profesi di sebelahnya                 |

## Palet Vegetasi (trimmed, bukan liar)

| Token Hex Penggunaan   |                                               |                                                                      |
| ---------------------- | --------------------------------------------- | -------------------------------------------------------------------- |
| `$world-hedge`         | #3D5C3D                                       | Pagar tanaman rapi (hedge), Central Plaza & Temple courtyard         |
| `$world-planter-wood`  | #4A3524 (sama dengan `$world-wood-furniture`) | Kotak planter bunga, konsisten dengan furniture                      |
| `$world-flower-accent` | #B85C4A / #C9A25C (bergantian)                | Bunga di planter — warna dusty, TIDAK neon, TIDAK memakai hex Rarity |

## Palet Lampu

| Token Hex Penggunaan |         |                                                                                                                             |
| -------------------- | ------- | --------------------------------------------------------------------------------------------------------------------------- |
| `$world-lamp-glow`   | #F5C97A | Warna cahaya PointLight di semua lamp post — selaras dengan Lighting.ClockTime=14 "warm soft tone" (Build Package Prompt 9) |

---

# 🏛️ BUILDING SILHOUETTE & PROPORTION PER TIER

<a name="silhouette"></a>
Semua bangunan Human City dikelompokkan ke **5 tier visual**. Tier menentukan tinggi, rasio aspek, ornament level — bukan district yang menentukan ini secara bebas.

## Tier 1 — Residential/Utility

**Anggota:** Inn (25x25), Blacksmith\_TorvIronhand (20x20), Armorer\_SirEdmund (20x20), Cafe\_Main (20x20), Apothecary\_Lyra (15x15)

```
Tinggi Dinding: 1x Wall_Straight (12 studs) — single story, TIDAK ada Tier 1 yang 2 lantai
Rasio Aspek Footprint: mendekati persegi, 1:1 sampai 1.25:1 (sesuai footprint yang sudah dikunci di Build Package A.2)
Roof: Roof_PitchedSegment, kemiringan 30° (sesuai spec kit), overhang 1 stud melebihi tepi dinding di semua sisi
Ornament: minimal — HANYA `$world-wall-secondary` half-timber accent di 2 sisi depan (bukan keempat sisi, hemat part & tetap
  terbaca "rumah warga" bukan "gedung penting")
Proporsi Tinggi Total: dinding 12 + roof 4 = 16 studs dari Foundation ke puncak atap (rasio dinding:atap = 3:1)

```

## Tier 2 — Commercial/Civic Ringan

**Anggota:** MerchantGuild\_Hall (30x30)

```
Tinggi Dinding: 1x Wall_Straight (12 studs), sama seperti Tier 1
Rasio Aspek Footprint: 1:1 (persegi, kesan "balai" bukan "rumah")
Roof: Roof_PitchedSegment 30°, TAPI dengan 1 baris Roof_FlatSegment kecil di puncak sebagai "lantern roof" sederhana
  (ventilasi visual, membedakan dari rumah tinggal Tier 1)
Ornament: `$world-stone-civic` untuk dinding (bukan `$world-wall-primary` Brick) — sinyal "bangunan bisnis resmi", trim
  `$border-metal` di sekeliling pintu masuk saja
Proporsi Tinggi Total: 12 + 4 = 16 studs (sama tinggi Tier 1, dibedakan lewat material bukan skala)

```

## Tier 3 — Guild/Civic Berat

**Anggota:** GuildHall\_Main (60x40) — termasuk Guild Bank room & Reward Officer desk di dalamnya

```
Tinggi Dinding: 1x Wall_Straight (12 studs) untuk badan utama, DITAMBAH Adventurer Guild Tower (landmark terpisah,
  Y=0 sampai Y=150 per Build Package Prompt 6) menjulang dari salah satu sudut bangunan
Rasio Aspek Footprint: 1.5:1 (60x40, memanjang) — kesan hall besar dengan interior terbuka
Roof: Roof_PitchedSegment 30° untuk badan utama, Pillar_Round (4 unit sesuai B.2) mengapit Door_Double di fasad depan
Window: Window_Arch (bukan Window_Small) — lihat §5
Ornament: trim `$border-metal` di ridge atap dan di sekeliling Door_Double — INI salah satu dari maksimal 2 bangunan
  per district yang boleh punya metal trim penuh (jangan disebar ke semua bangunan, supaya tetap terasa istimewa)
Proporsi Tinggi Total: badan 12+4=16 studs, Tower terpisah 150 studs (landmark, terlihat dari seluruh kota)

```

## Tier 4 — Sacred

**Anggota:** MainTemple (40x40)

```
Tinggi Dinding: 1x Wall_Straight (12 studs), Pillar_Round (6 unit sesuai B.2) membentuk portico di fasad depan
Rasio Aspek Footprint: 1:1 (persegi, simetris — kesan sakral/formal)
Roof: Roof_PitchedSegment 30° simetris dari 4 sisi (bukan cuma 2 sisi seperti Tier 1), bertemu di puncak tengah
Window: Window_Arch di semua sisi (6 unit sesuai B.2) — satu-satunya bangunan dengan Window_Arch di keempat dinding
Landmark: Main Temple Spire (Y=0 sampai Y=130, efek glow keemasan ringan — Build Package Prompt 6) — warna glow
  memakai `$border-metal` (#C9A25C), BUKAN warna Light element (#F5E8A8), supaya tidak tertukar dengan indikator
  elemen skill di UI
Ornament: TERTINGGI di antara semua bangunan — trim metal penuh di roof ridge + portico + spire base. Ini SATU-SATUNYA
  bangunan Tier 4 di kota, jadi tidak melanggar aturan "maksimal 2 metal trim penuh per district" di Tier 3
Proporsi Tinggi Total: badan 16 studs, Spire 130 studs (landmark kedua tertinggi setelah Guild Tower)

```

## Tier 5 — Arena (Colosseum)

**Anggota:** Colosseum\_Arena (diameter 80, arena tengah radius 25 + tribun ring 15)

```
Bentuk: SIRKULAR, satu-satunya bangunan non-persegi di Human City — pembeda visual yang disengaja karena fungsinya
  juga berbeda (spectator sport, bukan tempat tinggal/kerja)
Struktur Tribun: disusun dari Foundation_Base (Slate `$world-stone-civic`) bertingkat mengikuti kurva lingkaran,
  dengan Wall_HalfHeight sebagai railing/pembatas tribun bagian atas
Outer Wall: mengelilingi arena penuh (Build Package Prompt 6), tinggi setara 2x Wall_Straight (24 studs) — lebih
  tinggi dari bangunan Tier 1-3 supaya terasa "megah" tapi tetap di bawah Guild Tower/Temple Spire
Podium: Colosseum_Podium (Y=5, tengah arena) — struktur kecil dengan trim `$border-metal`, tempat Announcer NPC
Banner: kain vertikal tergantung di outer wall tiap ~16 studs, warna `$world-fabric-neutral` dengan garis `$border-metal`
  (BUKAN warna fraksi/tim, karena Colosseum di Human City belum ada sistem guild-vs-guild berwarna — tandai sebagai
  catatan terbuka jika nanti ditambahkan)

```

---

# 🏠 ROOF STYLE GUIDE

<a name="roof"></a>

```
Base Rule: SEMUA roof pakai Roof_PitchedSegment (8x4x8, kemiringan 30°) KECUALI Market stall & Profession Booth yang
  pakai Roof_FlatSegment (8x1x8) — aturan ini sudah dikunci di Build Package B.1, dokumen ini hanya menambah warna/trim.

Tier 1 (Residential/Utility): `$world-roof-primary` polos, TANPA trim metal, overhang 1 stud
Tier 2 (MerchantGuild): `$world-roof-primary` + 1 baris Roof_FlatSegment kecil di puncak (lantern roof), TANPA trim metal
Tier 3 (Guild Hall): `$world-roof-primary` + ridge cap trim `$border-metal` di sepanjang garis puncak atap
Tier 4 (Main Temple): `$world-roof-primary` + ridge cap trim `$border-metal` di SEMUA 4 garis puncak (simetris) + Spire
  landmark di titik pusat
Tier 5 (Colosseum): tidak pakai Roof_PitchedSegment (struktur terbuka/tribun), lihat §3 Tier 5

Larangan: JANGAN memberi ridge cap metal ke bangunan Tier 1 — ini eksklusif Tier 3+ supaya tetap jadi sinyal visual
  "bangunan penting" saat pemain berjalan di kota (wayfinding pasif tanpa perlu baca teks/minimap)

```

---

# 🪟 WINDOW STYLE GUIDE

<a name="window"></a>

```
Window_Small (3x3x1): dipakai di SEMUA Tier 1 (Inn, Blacksmith, Armorer, Cafe, Apothecary) dan Tier 2 (MerchantGuild)
  Frame: `$world-wall-secondary` (kayu gelap), Panel kaca: warna Glass bawaan Roblox transparansi 0.3, TIDAK berwarna
  (netral, supaya tidak bentrok dengan cahaya lamp warm di §11)
  Shutter (opsional, hemat part): HANYA di Inn — 1 pasang shutter kayu di jendela depan sebagai penanda "bangunan
  paling ramah/homey" di Tier 1, tidak wajib di 4 bangunan Tier 1 lainnya

Window_Arch (4x6x1): dipakai HANYA di Guild Hall (Tier 3) dan Main Temple (Tier 4) — TIDAK di Tier 1/2
  Frame: `$border-metal-dark` (bronze gelap, bukan kayu) — sinyal "bangunan formal"
  Panel kaca: Temple boleh memakai tint hangat sangat tipis (Color3 mendekati `$world-lamp-glow` tapi transparansi
  tinggi ~0.7) untuk kesan cahaya masuk dari sakral, Guild Hall tetap netral seperti Window_Small

Larangan: JANGAN campur Window_Small dan Window_Arch di bangunan yang sama — satu bangunan = satu jenis window,
  supaya bahasa visual tier tetap konsisten dan tidak ambigu.

```

---

# 🚪 DOOR STYLE GUIDE

<a name="door"></a>

```
Door_Single (4x8x1): dipakai di semua bangunan Tier 1 + Tier 2 (MerchantGuild) + Apothecary + Colosseum service entrance
  Material: `$world-wood-furniture` (coklat kayu gelap), Hardware: 2 engsel + 1 handle warna `$border-metal-dark`
  Cafe_Main mendapat SATU Door_Single tambahan (akses dapur, sesuai Build Package B.2) — pintu kedua ini identik
  gaya dengan pintu depan, hanya beda posisi (sisi belakang footprint)

Door_Double (8x10x1): dipakai HANYA di Guild Hall (Tier 3) dan Main Temple (Tier 4)
  Material: `$world-wood-furniture` dengan panel trim `$border-metal` membentuk garis vertikal di kedua daun pintu
  (kesan "pintu penting", bukan cuma pintu besar) — Hardware: engsel besar `$border-metal-dark`, handle/ring pull
  `$border-metal`

Larangan: JANGAN pakai Door_Double di bangunan Tier 1/2 sekecil apa pun alasannya (mis. "biar keliatan megah") —
  Door_Double adalah sinyal tier, bukan pilihan estetika bebas.

```

---

# 🧱 WALL & STONE STYLE GUIDE

<a name="wall"></a>

```
Foundation_Base (SEMUA bangunan tanpa kecuali): `$world-stone-foundation` (Slate #8A8272) — memberi kesan "kota
  berdiri di atas fondasi batu yang sama", elemen penyatu visual paling dasar di seluruh Human City

Wall_Straight/Wall_Corner Tier 1 & 2: `$world-wall-primary` (Brick krem #D8C7A1)
Wall_Straight/Wall_Corner Tier 3 & 4: `$world-stone-civic` (Concrete #A69C89) — lebih abu, lebih halus, sinyal
  "dipahat", beda dari bata Tier 1/2 yang lebih hangat/oranye

Half-timber Accent (`$world-wall-secondary`, balok kayu diagonal menempel di permukaan Brick):
  HANYA Tier 1 kecuali Apothecary (Apothecary polos tanpa half-timber — kesan lebih "klinis/toko obat" dibanding
  Inn/Blacksmith/Armorer/Cafe yang lebih "rumah tinggal")

Wall_HalfHeight (pagar/dinding rendah): dipakai untuk Colosseum tribun railing (§3 Tier 5), Market stall back divider
  (§9), dan pagar taman Residential (§8) — material sama dengan Fence, lihat §8

```

---

# 🚧 FENCE & RAILING STYLE

<a name="fence"></a>

```
Komponen: Wall_HalfHeight (8x6x1, sudah ada di kit — TIDAK perlu komponen baru)
Warna: `$world-wall-secondary` (#6B4A2E), TIDAK dicat warna lain — fence selalu kayu gelap polos di seluruh kota
  supaya jadi elemen "penghubung visual" netral antar zona berbeda tier

Penggunaan:
  - Residential District: pagar rendah mengelilingi halaman kecil tiap rumah Tier 1 (opsional per bangunan,
    prioritaskan Inn karena area publik paling ramai)
  - Market District: pembatas belakang tiap Player Shop stall (8x8) — MEMISAHKAN area stall dari jalur pejalan
    di belakangnya, bukan dekorasi
  - Colosseum: railing tribun (lihat §3 Tier 5), tinggi sama (Wall_HalfHeight) tapi mengikuti kurva lingkaran per
    segmen 8 studs
  - Temple courtyard: pagar rendah mengelilingi area portico, memberi jarak visual antara jalan umum dan area sakral

Larangan: JANGAN pakai fence di Gathering Hub (kesan terbuka/fungsional, bukan area privat) dan JANGAN pakai fence
  di sepanjang Road Network utama (akan mengganggu path pemain/NPC).

```

---

# 🏪 MARKET STALL & PROFESSION BOOTH STYLE

<a name="stall"></a>

```
Komponen: Stall_Counter (8x3x4) + Roof_FlatSegment (8x1x8) — TIDAK ada dinding penuh (open-air, sesuai
  Build Package B.2)

PlayerShop_Row (10 stall, Market District):
  Counter: `$world-wood-furniture`
  Awning/Roof: `$world-fabric-neutral` (#E8DCC4) dengan 1 strip `$border-metal` di tepi depan sebagai trim seragam
  Variasi: TIDAK ada variasi warna antar 10 stall ini secara default (netral, karena akan diisi barang jualan
  pemain yang sudah beragam warnanya sendiri — stall yang terlalu ramai warna akan bentrok secara visual)

ProfessionBooth_Row (4 booth, Market District):
  Counter: `$world-wood-furniture` (sama seperti PlayerShop)
  Awning/Roof: warna KANVAS PER PROFESI dari tabel §2 (Blacksmith #8C3B2E, Alchemist #4F7A4F, Jeweler #4A3B6B,
  Booth_Spare memakai warna netral `$world-fabric-neutral` sampai profesi masa depan ditentukan)
  Signage: WAJIB (lihat §12) — karena booth ini identitasnya spesifik profesi, beda dari PlayerShop yang generik

ToolVendor_OldPemberton (Gathering Hub): gaya sama dengan ProfessionBooth tapi warna kanvas netral
  `$world-fabric-neutral` (bukan profesi crafting, jadi tidak dapat warna kode khusus)

```

---

# 🪑 STREET FURNITURE

<a name="furniture"></a>

```
Bench: rangka `$world-wood-furniture` + kaki `$border-metal-dark`, ditempatkan di Central Plaza (mengelilingi
  Fountain_Central) dan Temple courtyard. TIDAK di district lain (menjaga furniture sebagai penanda "area istirahat"
  yang jelas, bukan tersebar random)

Crate & Barrel: `$world-wood-furniture`, ditempatkan berkelompok (2-4 unit) di Gathering Hub dan belakang
  Market District stall (kesan "stok barang") — hindari menaruh di Residential/Temple (area tersebut tidak
  bertema logistik)

Notice/Rumor Board: papan kayu `$world-wood-furniture` dengan frame `$border-metal-dark`, ditempatkan di 2 titik:
  dekat pintu masuk Guild Hall (Quest Board fisik, sudah disebut koordinatnya di Build Package A.2) dan dekat
  pintu masuk Cafe_Main (rumor board, sesuai City Content Addendum §Cafe)

Well/Fountain: Fountain_Central sudah ada koordinatnya (Build Package A.2, radius 15) — style: basin
  `$world-stone-civic`, finial tengah trim `$border-metal`, TIDAK memakai `$world-wall-primary` (fountain harus
  terasa lebih "civic" daripada material rumah biasa)

```

---

# 🔥 LAMP / LIGHT FIXTURE STYLE

<a name="lamp"></a>

```
Bentuk: post lamp tunggal, tinggi 10-12 studs (sejajar tinggi dinding Tier 1, tidak menjulang berlebihan)
  Rangka: `$border-metal-dark`, Kap lampu: `$border-metal`, Sumber cahaya: PointLight warna `$world-lamp-glow`

Spacing (mengikuti Road Network A.3):
  - Jalan Utama (12 studs lebar): 1 lamp post tiap ~40-48 studs di kedua sisi jalan
  - Jalan Sekunder (6 studs lebar): 1 lamp post tiap ~48-56 studs, satu sisi saja (hemat part, jalan sekunder
    lebih sepi)
  - Central Plaza & Market District: spacing lebih rapat, ~24 studs, untuk kesan "area paling hidup/ramai" di kota
  - Gathering Hub & South Gate: spacing paling jarang, ~64 studs (area transisi ke luar kota, tidak perlu terlalu terang)

Batas Performa: total lamp post + light source lain WAJIB tetap di bawah batas 20 dynamic light source per map yang
  sudah dikunci di Build Package Prompt 9 — hitung ulang jumlah titik di atas terhadap panjang total Road Network
  sebelum eksekusi, dan turunkan sebagian jadi non-lit decorative post (tanpa PointLight, kap lampu tetap ada
  secara visual) jika melebihi batas.

```

---

# 🪧 SIGNAGE SYSTEM

<a name="signage"></a>

```
Prinsip: signage di dunia BERBEDA dari UI — di UI, teks boleh pakai font PlayfairDisplay/Nunito karena itu TextLabel
  Roblox. Di dunia (papan kayu 3D), teks kecil TIDAK akan terbaca dari jarak jalan normal, jadi Human City memakai
  SIGNAGE BERBASIS IKON sebagai bahasa utama, teks hanya pelengkap kecil (bukan sebaliknya).

Bentuk Dasar: papan kayu `$world-wood-furniture` ukuran 4x3 studs (proporsional terhadap Door_Single 4x8, supaya
  tidak menutupi/mendominasi visual pintu), digantung dengan bracket `$border-metal` dari dinding, motif ikon
  dicat/diukir warna `$border-metal` di atas dasar kayu gelap

Ikon per Bangunan/Booth:
  | Bangunan/Booth | Ikon |
  |---|---|
  | Inn | Tempat tidur/bantal sederhana |
  | Blacksmith (Torv Ironhand + Booth) | Palu & landasan (anvil) |
  | Armorer | Perisai |
  | Cafe | Cangkir kopi/teh |
  | Apothecary (Lyra) / Alchemist Booth | Mortar & pestle |
  | Jeweler Booth | Permata bersegi |
  | Guild Hall | Buku terbuka |
  | Main Temple | Simbol matahari sederhana (bukan simbol religius dunia nyata) |
  | Merchant Guild | Timbangan (scale) |
  | Tool Vendor | Kapak/pickaxe bersilang |

Penempatan: WAJIB di semua bangunan Tier 1 + semua Profession Booth + Merchant Guild. TIDAK WAJIB di Guild Hall/Main
Temple (bangunan ini cukup besar untuk dikenali dari siluet saja tanpa signage — lihat §3), TIDAK ADA di
PlayerShop_Row generik (biar pemain sendiri yang beri identitas via item yang dipajang)

Ukuran Grid: semua sign 4x3 studs tanpa variasi ukuran antar bangunan — konsistensi ukuran signage adalah bagian
  dari bahasa visual "kota terstruktur/rapi" yang jadi identitas Human City.

```

---

# 🌳 VEGETATION

<a name="vegetation"></a>

```
Prinsip: Human City = "terstruktur/rapi" (Master Bible), jadi SEMUA vegetasi harus terlihat TERAWAT — hedge
  terpangkas rapi, planter box tersusun grid, TIDAK ada semak liar/pohon tumbang/rumput tinggi (itu bahasa visual
  untuk Hunting Ground, bukan kota).

Hedge (`$world-hedge`, #3D5C3D): mengelilingi Central Plaza (bentuk lingkaran/oktagon rapi mengikuti radius 75) dan
  membatasi Temple courtyard — dipangkas rata, tinggi seragam ~3 studs

Planter Box (`$world-planter-wood` + `$world-flower-accent`): ditempatkan berpasangan di depan Inn dan Cafe (kesan
  "hangat/ramah"), TIDAK di Blacksmith/Armorer/Apothecary/Guild Hall/Temple (bangunan fungsional/formal tidak
  butuh sentuhan dekoratif ini)

Pohon: jenis tunggal & seragam di seluruh Human City (untuk konsistensi, bukan variasi acak) — ditempatkan di tepi
  Road Network utama secara jarang (tidak menghalangi jalur), dan lebih rapat di sekitar Central Plaza sebagai
  peneduh. Warna daun tetap hijau natural standar (BUKAN dari palet warm kota — vegetasi sengaja jadi satu-satunya
  elemen "sejuk" untuk kontras visual terhadap dominasi coklat-krem-emas bangunan).

Larangan: JANGAN menaruh vegetasi apa pun di Market District (area sibuk berdagang, vegetasi akan terasa
  menghalangi) dan Colosseum (area sirkular sudah penuh secara struktural).

```

---

# 🧵 TEXTURE DENSITY RULES

<a name="texture"></a>

```
Prinsip Utama: variasi visual dicapai lewat KOMBINASI WARNA (Color3) di atas Material bawaan Roblox yang sudah
  ditentukan (Brick/WoodPlanks/Slate/Concrete/Fabric/Glass) — BUKAN lewat decal/texture custom tambahan. Ini
  menjaga performa (selaras dengan target 1000 concurrent, Master Bible §Technical Notes) dan menjaga waktu build
  tetap cepat (tidak perlu import asset gambar per bangunan).

Jumlah Material Berbeda per Bangunan: MAKSIMAL 3 (contoh Tier 1: Brick dinding + WoodPlanks roof + Slate
  foundation). Tier 3/4 boleh 4 (tambah Concrete untuk dinding civic). JANGAN lebih dari itu — bangunan dengan
  >4 material berbeda akan terasa "berisik" secara visual dan menambah render complexity tanpa manfaat sepadan.

Signage & Props Kecil: BOLEH pakai 1 warna solid tambahan di luar 3-4 material utama (mis. warna kanvas booth),
  karena ukurannya kecil dan fungsinya sebagai penanda, bukan permukaan besar.

Larangan Universal: JANGAN pakai Material "Neon", "ForceField", atau Material reflektif tinggi (Marble/Mirror) di
  Human City — semua permukaan harus terasa matte/natural sesuai tema "medieval terstruktur", efek berkilau
  hanya boleh dari PointLight (lamp, spire glow), bukan dari properti Material permukaan itu sendiri.

```

---

# 🎭 DECORATION DENSITY RULES (PER DISTRICT)

<a name="decoration"></a>
Build Package B.2 sudah mengunci **~250-300 part struktural** untuk seluruh Human City, dengan budget maksimal **500 part/district** dari Performance Budget. Tabel berikut mengunci **berapa banyak prop dekorasi (lamp, bench, crate, planter, signage, fence) yang boleh ditambahkan per district**, di luar part struktural, supaya total tidak mendekati/melebihi 500 part/district.

| District Estimasi Part Struktural Budget Prop Dekorasi Tambahan Tingkat Densitas |                                            |                                                             |                                                         |
| -------------------------------------------------------------------------------- | ------------------------------------------ | ----------------------------------------------------------- | ------------------------------------------------------- |
| Central Plaza                                                                    | ~15 (fountain + boundary)                 | 40-50 (bench, hedge, lamp rapat)                            | **Tinggi** — hub utama, harus terasa hidup              |
| Market District                                                                  | ~60 (Merchant Guild + 10 stall + 4 booth) | 50-60 (signage per booth, crate, lamp rapat, fence divider) | **Tinggi** — pasar ramai, sesuai target 1000 concurrent |
| Adventurer Guild                                                                 | ~50 (hall + tower)                        | 15-20 (lamp, notice board, minim vegetasi)                  | **Sedang** — formal, tidak perlu ramai dekorasi         |
| Residential District                                                             | ~60 (Inn, Blacksmith, Armorer, Cafe)      | 25-35 (planter, fence halaman, signage, lamp sedang)       | **Sedang**                                              |
| Temple District                                                                  | ~40 (Main Temple + Apothecary)            | 15-20 (hedge, bench, minim signage)                         | **Rendah-Sedang** — sakral, tenang, tidak ramai prop    |
| Colosseum                                                                        | ~35 (arena + tribun + outer wall)         | 15-20 (banner, podium trim, minim vegetasi/nol)             | **Sedang**                                              |
| Gathering Hub                                                                    | ~10 (tool vendor stall)                   | 5-10 (crate, lamp jarang, nol vegetasi)                     | **Rendah** — area fungsional/transisi                   |

**Aturan:** jika total (struktural + prop) satu district mendekati 450 part saat playtest (Build Package Prompt 10), kurangi dari kategori **prop dekorasi dulu** (bukan struktural) — mulai dari lamp non-esensial dan crate/barrel duplikat, karena elemen ini paling tidak mempengaruhi keterbacaan fungsi bangunan.

---

# 🗺️ PER-DISTRICT VISUAL SUMMARY TABLE

<a name="district"></a>

| District Tier Bangunan Dominan Material Dinding Warna Kanvas/Aksen Khas Densitas Dekorasi |                                             |                                                                    |                                                    |               |
| ----------------------------------------------------------------------------------------- | ------------------------------------------- | ------------------------------------------------------------------ | -------------------------------------------------- | ------------- |
| Central Plaza                                                                             | — (ruang terbuka)                            | `$world-stone-civic` (fountain only)                               | `$border-metal` (finial fountain)                  | Tinggi        |
| Adventurer Guild                                                                          | Tier 3                                      | `$world-stone-civic`                                               | `$border-metal` (trim penuh)                       | Sedang        |
| Market District                                                                           | Tier 1 (MerchantGuild=Tier 2) + Stall/Booth | `$world-wall-primary` / kanvas per profesi                         | Merah-tua/Hijau-lumut/Ungu-tua (booth)             | Tinggi        |
| Residential District                                                                      | Tier 1                                      | `$world-wall-primary` + half-timber                                | `$world-flower-accent` (planter)                   | Sedang        |
| Temple District                                                                           | Tier 4 (+Apothecary Tier 1)                 | `$world-stone-civic` (Temple) / `$world-wall-primary` (Apothecary) | `$border-metal` (trim Temple penuh)                | Rendah-Sedang |
| Colosseum                                                                                 | Tier 5                                      | `$world-stone-civic`                                               | `$world-fabric-neutral` + `$border-metal` (banner) | Sedang        |
| Gathering Hub                                                                             | Booth (ToolVendor)                          | kanvas netral                                                      | `$world-fabric-neutral`                            | Rendah        |

---

# 🗂️ TOKEN MAPPING TABLE (MATERIAL REFERENCE)

<a name="tokenmap"></a>
Tabel find-and-replace langsung untuk semua token `$world-*` yang dipakai dokumen ini, sekaligus referensi Roblox `Material` + `Color3` yang harus diterapkan AI saat mengeksekusi Build Package Prompt 4 (Modular Building Kit) dan Prompt 5 (Assembly):

| Token Hex Roblox Material                    |                   |                                              |
| -------------------------------------------- | ----------------- | -------------------------------------------- |
| `$world-wall-primary`                        | #D8C7A1           | Brick                                        |
| `$world-wall-secondary`                      | #6B4A2E           | WoodPlanks                                   |
| `$world-stone-foundation`                    | #8A8272           | Slate                                        |
| `$world-stone-civic`                         | #A69C89           | Concrete                                     |
| `$world-roof-primary`                        | #5C3A21           | WoodPlanks                                   |
| `$world-roof-flat`                           | #4A3B2A           | Fabric                                       |
| `$world-wood-furniture`                      | #4A3524           | WoodPlanks                                   |
| `$world-fabric-neutral`                      | #E8DCC4           | Fabric                                       |
| `$world-hedge`                               | #3D5C3D           | Grass                                        |
| `$world-planter-wood`                        | #4A3524           | WoodPlanks                                   |
| `$world-flower-accent`                       | #B85C4A / #C9A25C | Plastic (bergantian per planter)             |
| `$world-lamp-glow`                           | #F5C97A           | (PointLight Color, bukan Material permukaan) |
| `$border-metal` *(dari UI Style Bible)*      | #C9A25C           | Metal                                        |
| `$border-metal-dark` *(dari UI Style Bible)* | #8A6B35           | Metal                                        |
| Kanvas Blacksmith Booth                      | #8C3B2E           | Fabric                                       |
| Kanvas Alchemist Booth                       | #4F7A4F           | Fabric                                       |
| Kanvas Jeweler Booth                         | #4A3B6B           | Fabric                                       |

---

# 🤖 AI APPLY PROMPT

<a name="prompt"></a>
Prompt ini dijalankan **setelah** Build Package Prompt 4 (Modular Building Kit dibuat) dan **sebelum/bersamaan dengan** Prompt 5 (Assembly per bangunan) — menggantikan instruksi warna generik "Brick warna coklat krem, WoodPlanks coklat tua" di Prompt 4 dengan spesifikasi presisi dari dokumen ini:

```
Terapkan Map Visual Style Bible berikut ke Modular Building Kit dan proses assembly Human City (jangan ubah
 dimensi/koordinat dari Build Package — HANYA terapkan Material dan Color3):

1. Set Foundation_Base di SEMUA bangunan: Material=Slate, Color=$world-stone-foundation (#8A8272).
2. Set Wall_Straight/Wall_Corner: Material=Brick, Color=$world-wall-primary (#D8C7A1) untuk bangunan Tier 1 & 2
   (Inn, Blacksmith, Armorer, Cafe, Apothecary, MerchantGuild). Material=Concrete, Color=$world-stone-civic
   (#A69C89) untuk Tier 3 & 4 (Guild Hall, Main Temple, Colosseum tribun).
3. Tambahkan aksen Wall_Secondary (half-timber, Material=WoodPlanks, Color=$world-wall-secondary #6B4A2E) di 2
   sisi depan SETIAP bangunan Tier 1 KECUALI Apothecary.
4. Set Roof_PitchedSegment: Material=WoodPlanks, Color=$world-roof-primary (#5C3A21) di semua bangunan Tier 1-4.
   Tambahkan trim ridge Material=Metal, Color=$border-metal (#C9A25C) HANYA di Guild Hall dan Main Temple.
5. Set Roof_FlatSegment (Market stall & Profession Booth): Material=Fabric, Color=$world-roof-flat (#4A3B2A)
   untuk PlayerShop generik, ATAU warna kanvas profesi sesuai tabel §2/§17 untuk 4 Profession Booth.
6. Set Window_Small: Frame Material=WoodPlanks Color=$world-wall-secondary, Panel=Glass transparansi 0.3 netral —
   pasang HANYA di bangunan Tier 1 & 2. Set Window_Arch: Frame Material=Metal Color=$border-metal-dark — pasang
   HANYA di Guild Hall & Main Temple (Temple boleh tint panel kaca mendekati $world-lamp-glow transparansi 0.7).
7. Set Door_Single: Material=WoodPlanks Color=$world-wood-furniture, hardware Material=Metal Color=$border-metal-dark
   — di semua bangunan Tier 1/2/Apothecary. Set Door_Double: sama tapi tambahkan panel trim garis vertikal
   Material=Metal Color=$border-metal — HANYA Guild Hall & Main Temple.
8. Bangun lamp post (rangka Metal $border-metal-dark, kap Metal $border-metal, PointLight Color=$world-lamp-glow
   #F5C97A) di sepanjang Road Network sesuai spacing §11: 40-48 studs (jalan utama), 48-56 studs (jalan sekunder,
   satu sisi), 24 studs (Plaza & Market), 64 studs (Gathering Hub/South Gate). HITUNG total titik lamp — jika
   melebihi 20 dynamic light source total (batas dari Build Package Prompt 9), ubah sebagian jadi decorative
   post tanpa PointLight, prioritaskan menyisakan cahaya di Plaza dan Market District dulu.
9. Tambahkan signage 4x3 studs (papan WoodPlanks $world-wood-furniture, bracket Metal $border-metal, ikon dicat
   warna $border-metal) di semua bangunan Tier 1 dan semua Profession Booth + Merchant Guild, sesuai tabel ikon §12.
10. Tambahkan fence (Wall_HalfHeight, Material=WoodPlanks, Color=$world-wall-secondary) di: halaman Residential
    (opsional, prioritas Inn), pembatas belakang PlayerShop stall, railing tribun Colosseum, pagar courtyard Temple.
11. Tambahkan vegetasi: hedge (Material=Grass, Color=$world-hedge) mengelilingi Central Plaza & Temple courtyard;
    planter box (WoodPlanks $world-planter-wood + aksen $world-flower-accent) di depan Inn & Cafe; pohon seragam
    di tepi Road Network utama dan sekitar Plaza. JANGAN tambahkan vegetasi di Market District atau Colosseum.
12. Tambahkan street furniture: bench (WoodPlanks $world-wood-furniture + kaki Metal $border-metal-dark) di
    Plaza & Temple courtyard; crate/barrel (WoodPlanks $world-wood-furniture) berkelompok di Gathering Hub &
    belakang Market; notice/rumor board di pintu masuk Guild Hall & Cafe.

Setelah selesai, laporkan per district: (a) jumlah part struktural vs prop dekorasi tambahan dibanding budget di
§15, (b) apakah ada district yang mendekati/melebihi 500 part total, (c) total dynamic light source akhir
 dibanding batas 20, (d) screenshot top-down + 1 street-level view per district untuk verifikasi visual sebelum
 lanjut ke Prompt 6 (Landmark) dan Prompt 7 (NPC Placeholder) dari Build Package.

```

---

**Catatan:** dokumen ini mengunci identitas visual **dunia Human City**, bukan UI/System overlay (itu di UI Visual Style Bible). Titik temu keduanya HANYA di token `$border-metal`/`$border-metal-dark` (aksen metal dipakai ulang persis) dan warna Rarity/Element (dipakai ulang persis, tapi HANYA untuk glow item drop di ground — tidak untuk mengecat struktur). Demon City dan Elf City nanti akan punya Map Visual Style Bible sendiri dengan palet berbeda, tapi memakai struktur dokumen dan Modular Kit dimensi yang sama (sesuai catatan penutup Build Package: "swap Material Rules saja, struktur dipertahankan").
**End of Map Visual Style Bible (Human City).**
Terakhir Diperbarui: September 2026
Next: **(D) AI Validation/Guardrail Specification** — format build→validate→report→fix, mengunci bagaimana AI memverifikasi hasil eksekusi Build Package + dokumen ini terhadap spec sebelum dianggap selesai (part count, material/color compliance, spacing lamp, dsb).
