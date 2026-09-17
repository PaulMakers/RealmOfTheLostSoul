# 🖥️ Lost Soul — UI/UX Design Document

**Status:** Melengkapi item terakhir yang tersisa di checklist Master Game Bible — "UI/UX Final Design (deliberately saved for last)"

**Dokumen pendamping:** `LostSoul.md` (semua sistem yang direferensikan di sini sudah lock), `Lost Soul Economy Balancing.md`, `Lost Soul NPC Dialog & Quest Text.md`, `Lost Soul City Content Addendum.md`

**Cakupan:** Layout tiap layar, elemen UI, trigger interaksi, dan pertimbangan cross-platform (PC/Mobile/Tablet, karena Roblox)

**Catatan bahasa:** Label tombol, judul menu, dan teks UI yang muncul langsung di game ditulis dalam Bahasa Inggris. Penjelasan, struktur, dan catatan desain dalam Bahasa Indonesia.

---

## 📋 DAFTAR ISI

1. [Filosofi Desain UI](#philosophy)
2. [Inventaris Layar/HUD](#inventory)
3. [Main HUD (Selalu Tampil)](#hud)
4. [Menu Stat & Path](#stat-path)
5. [Inventory & Equipment](#inventory-equipment)
6. [Quest Log](#quest-log)
7. [Shop & Trade Window](#shop-trade)
8. [Combat & Dungeon UI](#combat)
9. [Guild & Social UI](#guild)
10. [Map & Navigation](#map)
11. [Indikator Status PvP/Criminal](#status)
12. [Sistem Notifikasi & Toast](#notification)
13. [Settings & Accessibility](#settings)
14. [Catatan Implementasi Roblox](#implementation)
15. [Checklist Implementasi](#checklist)

---

# 🎯 FILOSOFI DESAIN UI

## Prinsip Utama

1. **Server-authoritative, UI hanya menampilkan hasil** — client mengirim *intent*, server memvalidasi dan menghitung. UI tidak pernah menampilkan angka yang belum dikonfirmasi server.
2. **Transparansi angka** — setiap transaksi (beli, jual, upgrade, reward quest, betting) menampilkan angka pasti.
3. **Non-intrusive saat exploration, penuh informasi saat kombat** — HUD minim saat eksplorasi, elemen combat muncul otomatis saat encounter.
4. **Mobile-first constraint, desktop-enhanced** — semua elemen interaktif nyaman disentuh di layar kecil, lalu diperkaya shortcut desktop.
5. **Reversibilitas terlihat jelas untuk aksi berisiko** — trading (3 detik lock), crafting, PvP, dan betting membutuhkan konfirmasi visual sebelum aksi final.

## Kapan UI Dibangun

Menunggu sampai sistem berikut lock:

- Path system dengan multi-Path aktif
- Quest 5-state (Locked/Available/In Progress/Ready/Completed)
- Trading dengan lock 3 detik
- Crafting success/failure rate
- Crafting quality tier (Standard/Fine/Masterwork/Flawless)
- Soft cap stat allocation
- Criminal/Bounty status
- City Content Addendum UI surfaces (fallback badge, quality badges, Colosseum UI)

---

# 🗂️ INVENTARIS LAYAR/HUD

| Kategori | Layar | Selalu Tampil? |
|---|---|---|
| **Persistent** | Main HUD | Ya |
| **Menu Utama** | Stat & Path, Inventory & Equipment, Quest Log, Map | Toggle |
| **Kontekstual** | Shop/Trade Window, Dialog NPC, Crafting Station | Saat interaksi |
| **Kombat** | Skill bar, Boss HP bar, Party frame | Saat combat |
| **Sosial** | Guild panel, Chat | Toggle |
| **Sistem** | Notification/Toast, Settings | Event-driven / toggle |
| **City Content** | Colosseum Betting/Bracket, Craft Quality surfaces | Kontekstual/event-driven |

---

# 📟 MAIN HUD (SELALU TAMPIL)

| Elemen | Posisi | Isi |
|---|---|---|
| **HP/MP Bar** | Kiri atas | Bar HP + MP, angka numerik |
| **Level & EXP** | Kiri atas, di bawah HP/MP | Level + progress EXP |
| **Quick Skill Bar** | Bawah tengah | 6-8 slot skill, cooldown radial, MP cost |
| **Minimap** | Kanan atas | Area sekitar, quest marker, PvP zone indicator |
| **Gold Counter** | Kanan atas, di bawah minimap | Gold saat ini, update real-time |
| **Status Icon Bar** | Kiri, di bawah Level | Buff/debuff aktif + timer |
| **Criminal Indicator** | Di atas nama karakter | Ikon tengkorak merah jika Criminal aktif |

## Prinsip Layout

- HUD safe zone 90% dari layar.
- Semua elemen HUD punya opsi **opacity slider**.

---

# 📊 MENU STAT & PATH

**Dua tab:** `Stats` dan `Paths`.

### Tab Stats

- 7 slider/stepper: STR, VIT, INT, MND, AGI, DEX, LUK
- Nilai saat ini, efek formula real-time, indikator soft cap
- Poin bebas tersisa
- `Confirm Allocation`

### Tab Paths

- Path EXP progress bar
- Badge `Primary` dan `Set as Primary`
- Path belum di-unlock ditampilkan grayed-out dengan syarat unlock
- Hidden Path belum ditemukan tidak ditampilkan sampai syarat terpenuhi

---

# 🎒 INVENTORY & EQUIPMENT

**Split panel:** Equipment doll (kiri) + Inventory grid (kanan).

### Equipment Doll

- Weapon, Helm, Chest, Legs, Ring ×2, Amulet, Belt
- Rarity border dan ikon lock untuk item yang dikunci dari trade/drop

### Inventory Grid

- Filter: All / Weapon / Armor / Material / Consumable / Quest Item
- Quick-compare item
- Material otomatis stack
- Swipe-to-sell di mobile untuk item Common dengan konfirmasi popup

---

# 📜 QUEST LOG

**Dua tab:** `System Quests` dan `Player Requests`.

### System Quests

- Main Quest / Side Quest
- Status: Locked / Available / In Progress / Ready to Turn In / Completed
- Tap quest → ringkasan + `Track`

### Player Requests

- `My Postings` / `Available to Fulfill`
- Posting: item, reward, expiry, cancel
- Fulfillment board scrollable

---

# 🏪 SHOP & TRADE WINDOW

## NPC Shop

- `Buy` / `Sell`
- Buy: grid item + harga + quantity stepper
- Sell: harga dari formula Supply/Demand
- Fallback listing menampilkan `NPC Fallback +20%` dan `Standard quality`

## Player Shop

- Nama/foto penjual
- `10% tax applied` saat seller menetapkan harga
- Criminal tidak dapat mengakses Player Shop

### Indikator Kualitas Crafting

| Kualitas | Warna Badge | Ikon |
|---|---|---|
| Standard | Abu-abu | — |
| Fine | Hijau muda | 1 bintang |
| Masterwork | Biru | 2 bintang |
| Flawless | Emas | 3 bintang + glow |

Quality badge **terpisah dari rarity**; kedua indikator harus dapat dibaca independen.

## Trade Window

- Dua panel berdampingan + area gold
- Checkbox `Ready`
- Kedua pemain Ready → countdown lock 3 detik
- Setelah lock → `Trade Complete`
- Disconnect → trade dibatalkan otomatis

---

# ⚔️ COMBAT & DUNGEON UI

- Skill bar
- Target frame dengan rank badge
- Boss HP bar + phase marker
- Party frame: nama, HP/MP, status icon, jarak
- Dungeon floor indicator, modifier banner, loot roll popup

---

# 🏛️ GUILD & SOCIAL UI

- Guild tabs: `Members` / `Bank` / `Shop` / `Quests`
- Bank: shared storage + transaction log
- Shop: guild listing + commission
- Quests: guild quest progress
- Chat channels: `World` / `City` / `Guild` / `Party` / `Whisper`
- NPC dialog tetap overlay terpisah

---

# 🗺️ MAP & NAVIGATION

## World Map

- Menampilkan 8 map sebagai node terhubung
- Dungeon node menampilkan progress tertinggi
- Fast travel tetap **OPEN DECISION** sampai didefinisikan di Master Bible
- Colosseum dan Cafe adalah sub-marker node kota; Trade Post adalah sub-marker Central Hunting Ground/Hunter's Outpost. Tidak membuat node map baru.

## Minimap

- Zoom in/out
- Toggle: Quest marker / Party player marker / Resource node

---

# 🏟️ COLOSSEUM UI

## Betting Panel

- 2 petarung atau bracket turnamen
- Foto/model preview + ringkasan win-rate history
- Input taruhan dengan stepper, **cap 5000 gold**
- `Confirm Bet` mengunci taruhan setelah match dimulai
- Live odds indicator opsional untuk v1

## Tournament Bracket

- Bracket 8/16/32 slot, update setelah match selesai
- Highlight slot pemain sendiri
- Reward preview: title kosmetik + gold pool distribution

## Betting Result Toast

| Trigger | Contoh Teks | Durasi |
|---|---|---:|
| Menang | `You won! +[X] gold from the pot` | 3 detik |
| Kalah | `Bet lost. Better luck next match.` | 2 detik |

---

# 🔴 INDIKATOR STATUS PVP/CRIMINAL

| Status | Indikator Visual |
|---|---|
| Normal | Tidak ada indikator tambahan |
| In PvP Zone | Border merah tipis di tepi layar |
| Criminal | Tengkorak merah di nametag + badge HUD |
| Bounty Aktif (target) | Ikon koin merah tambahan di nametag |
| Rehabilitation In Progress | Progress bar kecil di Stat & Path |

---

# 🔔 SISTEM NOTIFIKASI & TOAST

| Trigger | Contoh Teks | Durasi |
|---|---|---:|
| Reward quest | `+[X] gold, +[Y] EXP` | 3 detik |
| Level up | `Level Up! Lv 48` | Manual dismiss |
| Item drop Epic+ | Card khusus | 5 detik |
| Trade selesai | `Trade Complete` | 2 detik |
| Crafting gagal | `Craft failed — materials partially lost` | 3 detik |
| Guild bank activity | `[PlayerName] deposited Iron Ore ×10` | 2 detik |
| Bet menang | `You won! +[X] gold from the pot` | 3 detik |
| Bet kalah | `Bet lost. Better luck next match.` | 2 detik |

- Maksimum 3 toast aktif; selebihnya diantrikan.
- Toast gold/item selalu menyebut angka pasti.

---

# ⚙️ SETTINGS & ACCESSIBILITY

- HUD Opacity slider
- Colorblind mode dengan palet alternatif/pattern/icon support
- Text size
- Keybind remap + touch sensitivity
- Chat filter + mute per pemain

---

# 🛠️ CATATAN IMPLEMENTASI ROBLOX

## Cross-Platform

- Gunakan `UIListLayout`/`UIGridLayout` + `UIAspectRatioConstraint`
- Tombol interaktif minimal 44×44 px pada mobile
- Skill bar: keybind 1-8 desktop, tap mobile

## Performa

- `Workspace.StreamingEnabled = true` pada map besar
- HUD `ScreenGui` memakai `ResetOnSpawn = false`
- Update elemen dinamis di-throttle kecuali combat aktif
- Colosseum UI di-load saat event/area relevan, bukan setiap frame

## Keamanan

- UI tidak menghitung hasil transaksi final
- Server mengonfirmasi gold/item/damage/quality/bet outcomes sebelum UI menampilkan hasil final
- Client hanya mengirim intent

---

# ✅ CHECKLIST IMPLEMENTASI

- [ ] Main HUD
- [ ] Stat & Path
- [ ] Inventory & Equipment
- [ ] Quest Log
- [ ] Shop/Trade Window
- [ ] Combat/Dungeon UI
- [ ] Guild panel + Chat
- [ ] World Map + minimap layer toggle + city sub-markers
- [ ] Colosseum UI
- [ ] Toast/Notification queue
- [ ] Settings
- [ ] Cross-platform test (PC/Mobile/Tablet)
- [ ] **OPEN DECISION:** fast travel antar map belum didefinisikan di Master Bible; jangan finalisasi behavior sampai diputuskan.

---

**End of UI/UX Design Document**

Terakhir Diperbarui: September 2026

Review Berikutnya: Setelah Phase 4 (Polish & Optimization) — saat UI mulai diimplementasikan di Roblox Studio