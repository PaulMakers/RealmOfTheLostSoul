# 🖥️ Lost Soul — UI Construction Specification

**Beda dengan UI/UX Design Document (sebelumnya):** dokumen itu menjelaskan APA yang tiap layar lakukan. Dokumen ini menjelaskan BAGAIMANA membangunnya — hierarchy, ukuran, anchor, breakpoint, state — supaya AI tidak berimprovisasi soal struktur. Warna/font/ornamen final ada di dokumen terpisah (UI Visual Style Bible, belum dibuat) — di sini semua warna ditulis sebagai **placeholder token** (mis. `$color-primary`) yang nanti diisi Visual Style Bible, bukan hex final.

**Base Reference Resolution:** 1920x1080 (Desktop), semua ukuran ditulis dalam **Scale (UDim2)** relatif terhadap ini, plus `UISizeConstraint` min/max dalam pixel absolut supaya tidak pecah di resolusi ekstrem.

---

# 📋 DAFTAR ISI

1. [Global Layout Rules](#global)
2. [Screen Hierarchy (Struktur Folder ScreenGui)](#hierarchy)
3. [Breakpoint: PC / Tablet / Mobile](#breakpoints)
4. [Interaction States (Universal)](#states)
5. [Main HUD — Spec Detail](#hud)
6. [Stat & Path Menu — Spec Detail](#statpath)
7. [Inventory & Equipment — Spec Detail](#inventory)
8. [Quest Log — Spec Detail](#questlog)
9. [Shop & Trade Window — Spec Detail](#shop)
10. [Combat & Dungeon UI — Spec Detail](#combat)
11. [Guild & Social UI — Spec Detail](#guild)
12. [Colosseum UI — Spec Detail](#colosseum)
13. [Map & Navigation — Spec Detail](#map)
14. [Notification/Toast — Spec Detail](#notification)
15. [Popup/Modal Behavior (Universal)](#popup)
16. [Naming Convention](#naming)
17. [AI Build Prompt Sequence — UI](#prompts)

---

# 🌐 GLOBAL LAYOUT RULES

<a name="global"></a>

```text
Positioning Method: UDim2 Scale untuk posisi/ukuran utama, Offset HANYA untuk padding/border tetap kecil (4-8px)
Root Container: 1 ScreenGui per grup fungsi (HUDGui, MenuGui, PopupGui, NotificationGui) — bukan 1 ScreenGui raksasa
Safe Zone: semua elemen interaktif wajib di dalam 90% area layar (margin 5% tiap sisi) — sesuai UI/UX Design doc §Layout
Corner Radius Default: $radius-panel (placeholder, isi di Visual Style Bible) — tapi WAJIB pakai UICorner, bukan gambar bulat manual
Z-Index Layer Order (DisplayOrder):
  0-9   : HUDGui (persistent)
  10-19 : MenuGui (toggle: Stat, Inventory, Quest, Map, Guild)
  20-29 : ContextGui (shop, dialog NPC, crafting station)
  30-39 : CombatGui (target frame, boss bar, party frame)
  40-49 : PopupGui (confirmation, trade lock countdown)
  50-59 : NotificationGui (toast — selalu paling atas kecuali error blocking)
```

---

# 📂 SCREEN HIERARCHY (STRUKTUR FOLDER SCREENGUI)

<a name="hierarchy"></a>

```text
StarterGui
├── HUDGui (DisplayOrder=0)
│   ├── HealthManaFrame
│   ├── LevelExpFrame
│   ├── SkillBarFrame
│   ├── MinimapFrame
│   ├── GoldCounterFrame
│   ├── StatusIconBarFrame
│   └── CriminalIndicatorFrame (world-space, BillboardGui terpisah — bukan ScreenGui)
├── MenuGui (DisplayOrder=10)
│   ├── StatPathPanel (toggle)
│   ├── InventoryPanel (toggle)
│   ├── QuestLogPanel (toggle)
│   ├── WorldMapPanel (toggle)
│   └── GuildPanel (toggle)
├── ContextGui (DisplayOrder=20)
│   ├── ShopWindow
│   ├── TradeWindow
│   ├── DialogueBox (NPC)
│   └── CraftingStation
├── CombatGui (DisplayOrder=30)
│   ├── TargetFrame
│   ├── BossHPFrame
│   ├── PartyFrame
│   └── DungeonFloorIndicator
├── ColosseumGui (DisplayOrder=32)
│   ├── BettingPanel
│   └── TournamentBracketPanel
├── PopupGui (DisplayOrder=40)
│   ├── ConfirmationModal
│   └── TradeLockCountdown
├── NotificationGui (DisplayOrder=50)
│   └── ToastQueueFrame
└── SettingsGui (DisplayOrder=15)
    └── SettingsPanel (toggle)
```

---

# 📱 BREAKPOINT: PC / TABLET / MOBILE

<a name="breakpoints"></a>

| Breakpoint | Trigger (AbsoluteSize.X) | Perubahan Layout |
|---|---:|---|
| **PC** | ≥ 1280px | Layout penuh, semua panel bisa terbuka bersamaan, keybind shortcut aktif |
| **Tablet** | 768-1279px | Skill bar & minimap sedikit diperkecil (90% scale), menu panel jadi fullscreen overlay (bukan windowed) |
| **Mobile** | < 768px | Skill bar jadi 6 slot (bukan 8), tombol minimal 44x44px wajib, menu panel selalu fullscreen, HUD elemen non-esensial (Status Icon Bar detail) disederhanakan jadi ikon tanpa label teks |

**Deteksi:** gunakan `UserInputService:GetLastInputType()` + `workspace.CurrentCamera.ViewportSize` — jangan asumsi dari device type saja (tablet landscape bisa lebih lebar dari mobile portrait).

**Constraint wajib di semua tombol interaktif:** `UISizeConstraint` dengan `MinSize = Vector2.new(44,44)` di breakpoint Tablet/Mobile.

---

# 🎛️ INTERACTION STATES (UNIVERSAL)

<a name="states"></a>

Berlaku untuk SEMUA button/interactive element di seluruh game — 1 aturan, bukan per-panel:

| State | Trigger | Perubahan Visual (placeholder token) |
|---|---|---|
| **Normal** | Default | `$color-button-normal`, Scale 1.0 |
| **Hover** (PC only) | MouseEnter | `$color-button-hover`, Scale 1.0, transisi 0.1s |
| **Pressed** | MouseButton1Down / TouchTap | `$color-button-pressed`, Scale 0.95, transisi 0.05s |
| **Disabled** | Kondisi tidak memenuhi syarat (mis. gold kurang) | `$color-button-disabled`, Transparency 0.5, tidak merespons input |

**Implementasi teknis:** 1 ModuleScript `Comp_ButtonStateHandler` dipakai ulang di semua tombol (bukan script per-tombol) — menerima reference ke 4 warna token di atas sebagai parameter.

---

# 📟 MAIN HUD — SPEC DETAIL

<a name="hud"></a>

| Elemen | AnchorPoint | Position (Scale) | Size (Scale) | Min Size (px) |
|---|---|---|---|---:|
| HealthManaFrame | (0,0) | (0.02, 0.02) | (0.18, 0.06) | 220 x 70 |
| LevelExpFrame | (0,0) | (0.02, 0.085) | (0.18, 0.03) | 220 x 30 |
| SkillBarFrame | (0.5,1) | (0.5, 0.97) | (0.32, 0.08) (8 slot) / (0.26, 0.08) (6 slot mobile) | 320 x 60 |
| MinimapFrame | (1,0) | (0.98, 0.02) | (0.15, 0.15) (persegi) | 150 x 150 |
| GoldCounterFrame | (1,0) | (0.98, 0.19) | (0.15, 0.03) | 150 x 30 |
| StatusIconBarFrame | (0,0) | (0.02, 0.13) | (0.15, 0.05) (max 6 ikon horizontal, wrap ke baris baru jika lebih) | 150 x 40 |

**Skill Slot individual:** Size `(1/8, 0, 1, 0)` dari SkillBarFrame (PC), `(1/6, 0, 1, 0)` (mobile) — persegi, `UIAspectRatioConstraint = 1`. Cooldown overlay = `Frame` radial fill child, `ZIndex +1` dari icon.

**CriminalIndicatorFrame:** BUKAN ScreenGui — pakai `BillboardGui` attached ke `Head` player, `Size = UDim2.new(2,0,2,0)` studs offset, `AlwaysOnTop = true`, hanya muncul jika `player:GetAttribute("CriminalStatus") == true`.

---

# 📊 STAT & PATH MENU — SPEC DETAIL

<a name="statpath"></a>

```text
Panel Size (PC): Scale (0.4, 0.6), AnchorPoint (0.5,0.5), Position (0.5,0.5) — centered modal
Panel Size (Mobile): Scale (0.95, 0.9) — hampir fullscreen
Tab Header: Height Scale 0.08 dari panel, 2 tab (Stats/Paths) side-by-side masing-masing 50% width tab header
```

**Tab Stats — 7 baris stat (STR/VIT/INT/MND/AGI/DEX/LUK):**

```text
Tiap baris: Height = (1/9) dari content area (7 stat + header "points remaining" + confirm button)
Layout per baris: [Label 20%] [Value 15%] [Slider/Stepper 45%] [SoftCapIndicator 20%]
SoftCapIndicator: Frame kecil 12x12px, warna berubah sesuai state (hijau/kuning/merah) — token: $color-softcap-safe / $color-softcap-warn / $color-softcap-danger
```

**Tab Paths:**

```text
ScrollingFrame dengan UIListLayout vertical, tiap Path Card:
  Height: 80px fixed
  Layout dalam card: [PathIcon 15%] [PathName+ExpBar 60%] [PrimaryBadge/SetPrimaryButton 25%]
  Locked Path Card: Transparency 0.6, teks syarat unlock ditampilkan alih-alih ExpBar
```

---

# 🎒 INVENTORY & EQUIPMENT — SPEC DETAIL

<a name="inventory"></a>

```text
Panel Size (PC): Scale (0.55, 0.7), split 35% Equipment Doll (kiri) / 65% Inventory Grid (kanan)
Panel Size (Mobile): Stack vertical — Equipment Doll atas (30% height), Grid bawah (70% height), swipe untuk switch jika perlu
```

**Equipment Doll:** 8 slot (Weapon, Helm, Chest, Legs, Ring x2, Amulet, Belt) — layout mengikuti siluet karakter kasar (Helm atas-tengah, Chest tengah, dst), tiap slot 60x60px, `UIAspectRatioConstraint = 1`.

**Inventory Grid:**

```text
Grid System: UIGridLayout, CellSize (60,60)px (PC) / (50,50)px (mobile), CellPadding (4,4)px
Default Grid: 8 kolom x N baris (scroll vertical jika melebihi viewport)
Filter Tab Bar: Height 40px di atas grid, 6 tab (All/Weapon/Armor/Material/Consumable/Quest Item)
Rarity Border: UIStroke di tiap slot terisi, Thickness 2px, Color = token rarity ($color-rarity-common s/d $color-rarity-mythic)
Quality Badge (dari City Content Addendum): Frame kecil 16x16px di pojok kanan-atas slot, hanya muncul untuk hasil craft player (Fine/Masterwork/Flawless)
```

---

# 📜 QUEST LOG — SPEC DETAIL

<a name="questlog"></a>

```text
Panel Size (PC): Scale (0.4, 0.65), 2 tab utama (System Quests / Player Requests)
Panel Size (Mobile): Scale (0.95, 0.85)
```

**List Item (per quest):**

```text
Height: 70px fixed
Layout: [StateIcon 10%] [QuestName+Objective 60%] [TrackButton 15%] [Reward preview icon 15%]
StateIcon mapping: 🔒=locked(abu) 📋=available(putih) ⏳=inprogress(kuning) ✅=readyToTurnIn(emas,glow) ✔️=completed(hijau pudar)
```

---

# 🏪 SHOP & TRADE WINDOW — SPEC DETAIL

<a name="shop"></a>

```text
Panel Size: Scale (0.5, 0.6), Tab Buy/Sell height 40px
Item Grid: sama spesifikasi grid dengan Inventory (§7) untuk konsistensi visual
NPC Fallback Badge: Frame 140x24px di header panel, teks "$token NPC Fallback +20%"
```

**Trade Window (Player-to-Player):**

```text
Split 50/50 horizontal (2 panel item + gold masing-masing pemain)
Ready Checkbox: 30x30px, posisi bawah tiap panel
Lock Countdown (saat kedua Ready): Modal terpisah (PopupGui), ukuran (0.3,0.2), angka countdown besar (font size 72px placeholder token), freeze background item grid (Transparency overlay 0.3 di atas grid)
```

---

# ⚔️ COMBAT & DUNGEON UI — SPEC DETAIL

<a name="combat"></a>

```text
TargetFrame: muncul di (0.5, 0.08) top-center saat target di-lock, Size (0.25, 0.06)
BossHPFrame: (0.5, 0.03), Size (0.5, 0.05) — lebih besar dari TargetFrame biasa, dengan phase marker (garis vertical Frame kecil 2px width di titik %HP tertentu)
PartyFrame: Anchor (0,0.3), Size per member card (0.12, 0.08), max 4 card vertical stack di sisi kiri
DungeonFloorIndicator: (0.98, 0.3) sisi kanan, Size (0.1, 0.04), persistent selama di instance dungeon
```

---

# 🏛️ GUILD & SOCIAL UI — SPEC DETAIL

<a name="guild"></a>

```text
Panel Size: Scale (0.5, 0.65), 4 tab (Members/Bank/Shop/Quests) horizontal di top
Members List: sama pola List Item dengan Quest Log (§8), height 60px, tambah online status dot 10x10px
Bank Grid: sama spesifikasi grid dengan Inventory (§7)
Chat: Frame terpisah (bukan bagian GuildPanel), Anchor (0,1), Size (0.3, 0.25), 5 channel tab kecil di atas chat log
```

---

# 🏟️ COLOSSEUM UI — SPEC DETAIL

<a name="colosseum"></a>

*(Baru, dari City Content Addendum)*

```text
BettingPanel: muncul otomatis saat masuk area Colosseum, Anchor (0.5,1), Position (0.5, 0.95), Size (0.4, 0.3)
  Layout: 2 kolom (petarung A / petarung B), tiap kolom [Foto/Model preview 40%] [Nama+WinRate 20%] [Input Stepper 25%] [ConfirmBet button 15%]
TournamentBracketPanel: toggle fullscreen-overlay style (sama seperti WorldMap), Size (0.8, 0.8), bracket tree pakai UIGridLayout bertingkat
```

---

# 🗺️ MAP & NAVIGATION — SPEC DETAIL

<a name="map"></a>

```text
WorldMapPanel: fullscreen overlay, Size (0.9, 0.9), 8 node map (3 City, 2 Hunting Ground, 3 Dungeon) sebagai ImageButton 80x80px terhubung garis (Frame tipis 2px)
MinimapFrame: sudah di §5 (HUD) — di sini tambahan: pinch-zoom (mobile) via TouchPinch event, scroll-zoom (PC) via MouseWheel, layer toggle button (Quest/Player/Resource) 30x30px masing-masing di pojok minimap
```

---

# 🔔 NOTIFICATION/TOAST — SPEC DETAIL

<a name="notification"></a>

```text
ToastQueueFrame: Anchor (0.5,0), Position (0.5, 0.05), Size (0.3, auto-height per toast)
Toast Individual: Height 50px, UIListLayout vertical dengan Padding 8px, max 3 toast bersamaan (antrian FIFO, toast baru masuk dari atas, yang lama geser turun lalu fade out)
Level Up Toast: ukuran beda — Size (0.4, 0.15), Anchor (0.5,0.4), perlu tap untuk dismiss (bukan auto-timer seperti toast biasa)
Epic+ Item Drop Card: Size (0.35, 0.12), muncul dari bawah (slide-in animation), glow effect border (UIStroke dengan efek pulsing — token $color-rarity-epic / $color-rarity-legendary)
```

---

# 🪟 POPUP/MODAL BEHAVIOR (UNIVERSAL)

<a name="popup"></a>

```text
Semua Modal (Confirmation, Trade Lock, dsb.) WAJIB:
  1. Background dim overlay (Frame fullscreen, BackgroundTransparency 0.5, warna hitam) di belakang modal, ZIndex tepat di bawah modal
  2. Tidak bisa ditutup dengan tap di luar modal untuk aksi berisiko gold (Trade Lock) — HARUS ada tombol eksplisit Confirm/Cancel
  3. Modal non-berisiko (mis. tooltip info) BOLEH ditutup tap-outside
  4. Animasi masuk: scale dari 0.8 → 1.0 dalam 0.15s (TweenService), bukan muncul instan
```

---

# 🏷️ NAMING CONVENTION

<a name="naming"></a>

```text
ScreenGui: [Fungsi]Gui — contoh "HUDGui", "MenuGui"
Panel utama: [Nama]Panel — contoh "InventoryPanel", "QuestLogPanel"
Frame dalam panel: [Nama]Frame — contoh "HealthManaFrame"
Button: [Fungsi]Button — contoh "ConfirmAllocationButton", "SetPrimaryButton"
Reusable component (dipakai berulang lintas panel): simpan di ReplicatedStorage/UIComponents, prefix "Comp_" — contoh "Comp_RarityBorder", "Comp_ButtonStateHandler"
```

---

# 🤖 AI BUILD PROMPT SEQUENCE — UI

<a name="prompts"></a>

Urutan prompt untuk Roblox Studio Assistant, pola sama seperti Map Build Package (build → validate → report → fix).

### Prompt 1 — Root Structure

```text
Buat 8 ScreenGui di StarterGui sesuai hierarchy §2 (HUDGui, MenuGui, ContextGui, CombatGui, ColosseumGui, PopupGui, NotificationGui, SettingsGui) dengan DisplayOrder persis seperti tabel Global Layout Rules §1. Jangan isi konten dulu — hanya container kosong. Laporkan 8 ScreenGui berhasil dibuat dengan DisplayOrder masing-masing.
```

### Prompt 2 — Reusable Components

```text
Buat ModuleScript "Comp_ButtonStateHandler" di ReplicatedStorage/UIComponents sesuai spesifikasi §4 (4 state: Normal/Hover/Pressed/Disabled), menerima 4 color token sebagai parameter (belum diisi warna final — pakai placeholder Color3.new(0.5,0.5,0.5) untuk semua sementara). Buat juga template "Comp_RarityBorder" (UIStroke reusable) dan "Comp_QualityBadge" (Frame 16x16 reusable dari Inventory spec §7).
```

### Prompt 3 — Main HUD

```text
Bangun HUDGui sesuai tabel §5 persis (posisi, ukuran, min-size dalam pixel). Gunakan Comp_ButtonStateHandler untuk semua slot Skill Bar yang interaktif. CriminalIndicatorFrame dibuat sebagai BillboardGui terpisah, bukan child ScreenGui. Setelah selesai, laporkan AbsoluteSize tiap elemen pada resolusi test 1920x1080 dan 375x812 (mobile).
```

### Prompt 4 — Menu Panels (ulangi per panel)

```text
Bangun [NamaPanel] sesuai spesifikasi §[nomor section terkait], termasuk breakpoint PC/Tablet/Mobile dari §3. Gunakan Comp_RarityBorder dan Comp_QualityBadge dari ReplicatedStorage untuk elemen grid/inventory. Toggle visibility panel ini terhubung ke keybind [I/P/Q/M/G sesuai fungsi]. Laporkan hierarchy Instance final panel ini (Explorer tree screenshot).
```

*(Jalankan untuk: StatPathPanel, InventoryPanel, QuestLogPanel, WorldMapPanel, GuildPanel, ShopWindow, TradeWindow)*

### Prompt 5 — Combat & Colosseum UI

```text
Bangun CombatGui (TargetFrame, BossHPFrame dengan phase marker, PartyFrame, DungeonFloorIndicator) sesuai §10, dan ColosseumGui (BettingPanel, TournamentBracketPanel) sesuai §12. Pastikan CombatGui default Visible=false, hanya muncul via script saat combat trigger (logic trigger dikerjakan terpisah — di sini cukup pastikan struktur dan default state benar).
```

### Prompt 6 — Notification & Popup

```text
Bangun NotificationGui (ToastQueueFrame dengan antrian max 3, sesuai §14) dan PopupGui (ConfirmationModal generic + TradeLockCountdown khusus, sesuai §15 — WAJIB ada background dim overlay). Buat 1 ModuleScript "ToastQueueManager" yang menangani antrian FIFO.
```

### Prompt 7 — Validation Pass

```text
Cek seluruh UI yang sudah dibuat terhadap checklist berikut, laporkan PASS/FAIL per item:
- Semua tombol interaktif punya MinSize 44x44px di breakpoint Mobile?
- Semua Modal berisiko gold (Trade Lock) tidak bisa ditutup tap-outside?
- DisplayOrder semua ScreenGui sesuai urutan §1?
- Semua Frame pakai UDim2 Scale (bukan Offset murni) untuk posisi utama?
- Tidak ada ScreenGui/Frame yang overlap tak disengaja di resolusi 1920x1080 DAN 375x812?
Jika ada FAIL, perbaiki dulu sebelum lanjut ke tahap Visual Style Bible.
```

---

**Catatan:** semua token warna (`$color-*`) di dokumen ini **sengaja belum diisi** — itu tugas UI Visual Style Bible (dokumen berikutnya). Setelah Visual Style Bible selesai, tinggal jalankan 1 prompt tambahan: "ganti semua placeholder token di UI dengan nilai final dari Visual Style Bible" — tidak perlu rebuild struktur dari nol.

**End of UI Construction Specification.**
