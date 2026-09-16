# 🎨 Lost Soul — UI Visual Style Bible

**Beda dengan UI Construction Specification (sebelumnya):** dokumen itu mengunci STRUKTUR (ukuran, posisi, hierarchy). Dokumen ini mengunci **RUPA** — semua token placeholder (`$color-*`, dst) yang dipakai di Construction Spec diisi nilai final di sini. Setelah ini, AI tidak lagi punya ruang menebak "warnanya apa" atau "fontnya apa".

**Identitas Visual Lost Soul (1 kalimat):** *"Forged Adventurer's Ledger"* — perpaduan parchment/perkamen Guild yang hangat dengan aksen metal tertempa, supaya UI terasa seperti alat si petualang (bukan UI generic sci-fi atau UI kartun ceria). Ini yang menyatukan 20+ panel berbeda jadi terasa 1 game, sesuai identitas "System" yang jadi Central Mystery Lost Soul — UI-nya sendiri terasa seperti artefak dari System itu.

---

# 📋 DAFTAR ISI

1. [Color System](#color)
2. [Typography](#typography)
3. [Panel & Border Style](#panel)
4. [Button Style](#button)
5. [Icon Style Guide](#icon)
6. [Ornament System](#ornament)
7. [Shadow & Glow Rules](#shadow)
8. [Visual Hierarchy](#hierarchy)
9. [Token Mapping Table (isi semua placeholder Construction Spec)](#tokenmap)
10. [AI Apply Prompt](#prompt)

---

# 🎨 COLOR SYSTEM

<a name="color"></a>

## Base Palette

| Token | Hex | Penggunaan |
|---|---|---|
| `$bg-panel` | #2B2118 | Background utama semua panel (coklat gelap "kulit/perkamen tua") |
| `$bg-panel-light` | #3D3226 | Background sub-section dalam panel (row alternating, card) |
| `$border-metal` | #C9A25C | Border/stroke utama panel (emas tembaga tertempa) |
| `$border-metal-dark` | #8A6B35 | Border sekunder, shadow border |
| `$text-primary` | #F5EBD8 | Teks utama (krem terang, kontras di atas bg gelap) |
| `$text-secondary` | #B8A98A | Teks sekunder/deskripsi |
| `$text-disabled` | #6B6255 | Teks nonaktif |
| `$accent-primary` | #C9A25C | Aksen utama (sama dengan border-metal, dipakai icon/highlight aktif) |

## Button State Colors (mengisi §4 Construction Spec)

| Token | Hex | State |
|---|---|---|
| `$color-button-normal` | #4A3B2A | Normal |
| `$color-button-hover` | #5C4A35 | Hover (PC) |
| `$color-button-pressed` | #362A1D | Pressed |
| `$color-button-disabled` | #2E2A24 (Transparency 0.5) | Disabled |

## Rarity Colors (Item, konsisten di semua sistem — Inventory, Shop, Skill Book)

| Rarity | Hex | Catatan |
|---|---|---|
| Common | #B0B0B0 | Abu netral |
| Uncommon | #4CAF50 | Hijau |
| Rare | #4A90D9 | Biru |
| Epic | #A64CD9 | Ungu |
| Legendary | #E8A23D | Oranye-emas |
| Mythic | #E84C4C | Merah, dengan pulsing glow (lihat §7) |

## Quality Craft Colors (dari City Content Addendum — TERPISAH dari Rarity, jangan tertukar)

| Quality | Hex | Ikon |
|---|---|---|
| Standard | #8A8A8A | tidak ada ikon |
| Fine | #7FD98A | 1 bintang |
| Masterwork | #5C9DE8 | 2 bintang |
| Flawless | #E8C25C | 3 bintang + glow |

## Elemental Colors (6 elemen)

| Elemen | Hex |
|---|---|
| Fire | #E85C3D |
| Water | #3DAEE8 |
| Earth | #7A9B4F |
| Wind | #A8E8D9 |
| Light | #F5E8A8 |
| Dark | #6B4C8A |

## Status/System Colors

| Token | Hex | Penggunaan |
|---|---|---|
| `$color-softcap-safe` | #4CAF50 | Soft cap 0-50 poin |
| `$color-softcap-warn` | #E8A23D | Soft cap 51-100 poin |
| `$color-softcap-danger` | #E84C4C | Soft cap 101+ poin |
| `$color-pvp-zone` | #E84C4C | Border tipis indikator PvP zone |
| `$color-criminal` | #C41E1E | Ikon tengkorak, nametag criminal |
| `$color-quest-available` | #F5EBD8 | Marker quest available |
| `$color-quest-inprogress` | #4A90D9 | Marker in progress |
| `$color-quest-ready` | #E8A23D | Marker ready to turn in, dengan glow |

---

# ✍️ TYPOGRAPHY

<a name="typography"></a>

```text
Header/Title Font: "PlayfairDisplay" (serif elegan, kesan "ledger/manuscript") — dipakai di judul panel, nama Path, nama item Legendary+
Body/UI Font: "Nunito" (sans-serif bersih, keterbacaan tinggi di layar kecil) — dipakai di semua teks fungsional (stat angka, deskripsi, tombol)
Dialog NPC Font: sama dengan Body (Nunito) — supaya tidak melelahkan mata saat baca dialog panjang
```

### Font Availability Lock

- Sebelum menerapkan style, AI **WAJIB memverifikasi exact font name** `PlayfairDisplay` dan `Nunito` di Roblox Studio versi yang sedang digunakan.
- Jika salah satu font **tidak tersedia**, AI **HARUS STOP sebelum menerapkan typography**, lalu melaporkan font yang tidak tersedia dan meminta keputusan penggantian.
- AI **DILARANG melakukan silent fallback/substitution** ke font lain. Fallback `Merriweather` (Header) dan `SourceSans` (Body) hanya boleh dipakai setelah keputusan penggantian disetujui dan didokumentasikan.

## Type Scale

| Level | Size (px, referensi 1920x1080) | Font | Penggunaan |
|---|---:|---|---|
| Display | 48 | PlayfairDisplay Bold | Level Up toast, judul World Map |
| H1 | 32 | PlayfairDisplay | Judul panel (Inventory, Quest Log, dst) |
| H2 | 22 | PlayfairDisplay | Sub-judul (nama tab, nama Path) |
| Body Large | 18 | Nunito | Dialog NPC, deskripsi quest |
| Body | 15 | Nunito | Teks UI standar (label stat, item name) |
| Caption | 12 | Nunito | Teks kecil (timestamp, tooltip, badge) |

**Minimum size mobile:** semua Body/Caption naik +2px di breakpoint Mobile (keterbacaan layar kecil) — H1/H2 tetap sama karena sudah proporsional dengan Scale-based sizing.

---

# 🖼️ PANEL & BORDER STYLE

<a name="panel"></a>

```text
Corner Radius (`$radius-panel`): 12px — semua panel utama (Inventory, Quest Log, Shop, dst)
Corner Radius (`$radius-small`): 6px — elemen kecil (button, slot inventory, toast)
Border Treatment: UIStroke 2px, Color = $border-metal, Transparency 0 untuk panel aktif/focus, Transparency 0.4 untuk panel background/inactive
Panel Background: BackgroundColor3 = $bg-panel, BackgroundTransparency 0.05 (hampir solid, bukan transparan — kesan "material fisik", bukan overlay kaca)
Panel Header Bar: strip 8px di bagian atas tiap panel, warna $border-metal solid — identitas visual konsisten, mirip "sampul buku ledger"
```

---

# 🔘 BUTTON STYLE

<a name="button"></a>

```text
Shape: Rounded rectangle, $radius-small (6px) — TIDAK pill/full-round (kesan "tombol tertempa", bukan tombol mobile app generic)
Border: UIStroke 1.5px, Color = $border-metal-dark
Primary Button (Confirm/Accept): Background = $accent-primary, Text = $bg-panel (dark text di atas terang, kontras tinggi)
Secondary Button (Cancel/Back): Background = $bg-panel-light, Text = $text-primary, border only tanpa fill solid
Danger Button (mis. "Abandon Quest"): Background = #C41E1E (sama dengan $color-criminal), dipakai HANYA untuk aksi destruktif
Icon-only Button: visual icon/container 32x32px minimum pada desktop; interactive hitbox tetap MINIMUM 44x44px pada Tablet/Mobile sesuai universal interaction rule di UI Construction Specification. Icon centered, tanpa background kecuali Hover state.
```

---

# 🧩 ICON STYLE GUIDE

<a name="icon"></a>

```text
Style: Flat + thin outline (2px stroke), BUKAN 3D/gradient/skeuomorphic — konsisten dengan panel flat di atas
Grid: semua icon dibuat dalam grid 32x32px dasar, di-scale proporsional untuk ukuran lain (16/24/48px)
Warna Icon: mengikuti context — icon rarity/element pakai warna dari Color System di atas, icon fungsional (settings, close, back) pakai $text-primary
Icon Set yang wajib konsisten style-nya (jangan campur sumber asset berbeda gaya):
  - 6 elemen (Fire/Water/Earth/Wind/Light/Dark)
  - 6 rarity tier
  - Skill/Path icon (10 Path + evolusi)
  - System icon (gold coin, EXP star, HP heart, MP droplet)
  - UI functional icon (close X, settings gear, back arrow, search)
```

---

# 🏛️ ORNAMENT SYSTEM

<a name="ornament"></a>

Elemen dekoratif fantasy — dipakai **secukupnya**, bukan di semua tempat (supaya tidak berat visual & performa):

```text
Corner Ornament (ukiran sudut kecil, gaya metal-forged): HANYA di 4 sudut panel-panel besar (Inventory, Quest Log, Guild, World Map) — TIDAK di toast/notification/tombol kecil
Divider Line: garis tipis dengan aksen ornamen tengah (kecil, seperti gesper), dipakai untuk pisah section dalam panel (mis. antara Equipment Doll dan Inventory Grid)
Frame Accent: border ganda (outer $border-metal-dark, inner $border-metal) HANYA untuk item Legendary+ dan Path Card yang sudah Primary — sinyal visual "ini penting", bukan dekorasi rata semua elemen
Aturan Densitas: maksimal 1 jenis ornamen per panel — jangan tumpuk Corner Ornament + Divider + Frame Accent di panel yang sama kecuali memang untuk highlight khusus (Legendary item card boleh 2 sekaligus: Frame Accent + rarity glow)
```

---

# ✨ SHADOW & GLOW RULES

<a name="shadow"></a>

```text
Drop Shadow (semua panel mengambang): ImageLabel shadow asset, Offset (4,4), Transparency 0.6, Blur radius setara ~8px — dipakai di SEMUA panel modal/menu, TIDAK di HUD persistent (HUD harus terasa "menyatu" dengan game world, bukan mengambang)
Glow Effect: HANYA dipakai untuk 3 kasus — (1) item Legendary+/Flawless quality, (2) Quest Ready-to-turn-in marker, (3) Level Up toast. Efek: UIGradient animasi pulsing lambat (2s cycle), warna sesuai rarity/quality masing-masing
Larangan: JANGAN pakai glow di button biasa, JANGAN pakai glow permanen di elemen HUD persistent (mengganggu saat main lama, capek mata)
```

---

# 📐 VISUAL HIERARCHY

<a name="hierarchy"></a>

```text
Level 1 (Paling Penting — perlu aksi player SEKARANG): Quest Ready-to-turn-in, Level Up, Trade Lock Countdown → Glow + Display/H1 size + warna accent
Level 2 (Penting, tidak mendesak): Nama panel, nama Path aktif, HP/MP critical (<20%) → H2 size, warna solid tanpa glow
Level 3 (Informasi standar): Item name, stat value, quest objective text → Body size
Level 4 (Detail sekunder): Timestamp, flavor text, tooltip → Caption size, $text-secondary
```

**Aturan:** 1 layar tidak boleh punya lebih dari 2 elemen Level 1 aktif bersamaan (mencegah semua terasa "mendesak" sekaligus dan kehilangan makna).

---

# 🗂️ TOKEN MAPPING TABLE (ISI SEMUA PLACEHOLDER CONSTRUCTION SPEC)

<a name="tokenmap"></a>

Tabel ini adalah find-and-replace langsung terhadap semua token `$...` yang muncul di UI Construction Specification:

| Token di Construction Spec | Nilai Final |
|---|---|
| `$color-button-normal` | #4A3B2A |
| `$color-button-hover` | #5C4A35 |
| `$color-button-pressed` | #362A1D |
| `$color-button-disabled` | #2E2A24 @ 0.5 transparency |
| `$color-softcap-safe` | #4CAF50 |
| `$color-softcap-warn` | #E8A23D |
| `$color-softcap-danger` | #E84C4C |
| `$color-rarity-common` s/d `$color-rarity-mythic` | Lihat tabel Rarity Colors §1 |
| `$radius-panel` | 12px |
| `$color-rarity-epic` / `$color-rarity-legendary` (glow, Notification spec) | #A64CD9 / #E8A23D, dengan efek pulsing dari §7 |

---

# 🤖 AI APPLY PROMPT

<a name="prompt"></a>

Satu prompt untuk menerapkan seluruh Visual Style Bible ini ke struktur UI yang sudah dibangun dari Construction Specification:

```text
Terapkan Visual Style Bible berikut ke semua UI yang sudah dibangun sebelumnya (jangan ubah struktur/ukuran/anchor, HANYA ganti nilai visual):

0. SEBELUM PERUBAHAN: verifikasi exact font name "PlayfairDisplay" dan "Nunito" di Roblox Studio versi yang sedang digunakan. Jika salah satu tidak tersedia, STOP dan laporkan font yang tidak tersedia. Jangan lakukan silent fallback. Jangan menerapkan typography sampai keputusan penggantian font disetujui.
1. Ganti semua token warna placeholder ($color-*, $bg-*, $border-*, $text-*, $accent-*) dengan nilai hex final sesuai Token Mapping Table.
2. Set semua UICorner: 12px untuk panel utama, 6px untuk elemen kecil (button, slot, toast).
3. Set Font semua TextLabel/TextButton: "PlayfairDisplay" untuk judul panel & H1/H2, "Nunito" untuk semua teks body/button/dialog. Hanya gunakan fallback setelah keputusan penggantian font disetujui dan dicatat.
4. Terapkan Type Scale sesuai tabel §2 ke semua level teks (Display/H1/H2/Body Large/Body/Caption).
5. Tambahkan UIStroke 2px warna $border-metal ke semua panel utama, Transparency 0.4 untuk panel background/inactive.
6. Tambahkan Drop Shadow (ImageLabel shadow, offset 4x4, transparency 0.6) ke semua panel modal/menu — KECUALI elemen HUD persistent (Health/Mana, Skill Bar, Minimap).
7. Tambahkan Glow effect HANYA ke: item card Legendary+/Flawless, Quest Ready-to-turn-in marker, Level Up toast. Jangan tambahkan glow ke elemen lain.
8. Tambahkan Corner Ornament HANYA ke 4 panel besar: InventoryPanel, QuestLogPanel, GuildPanel, WorldMapPanel.
9. Untuk icon-only button, pertahankan visual icon/container 32x32px pada desktop, tetapi pastikan interactive hitbox memenuhi minimum 44x44px pada Tablet/Mobile sesuai UI Construction Specification.

Setelah selesai, laporkan: berapa banyak instance yang terpengaruh per kategori (warna/font/corner/shadow/glow/ornament), dan screenshot sebelum-sesudah minimal 2 panel (HUD + Inventory) untuk verifikasi visual.
```

---

**Catatan:** dokumen ini mengunci identitas visual **UI/System overlay**, bukan visual dunia game (rumah, jalan, dsb — itu di Map Visual Style Bible, dokumen berikutnya). Warna rarity/elemen di sini juga dipakai ulang di world (mis. warna border loot drop di dunia nyata memakai hex Rarity Colors yang sama) — jadi 2 Style Bible ini nanti saling terhubung di titik tersebut, bukan sepenuhnya terpisah.

**End of UI Visual Style Bible.**
