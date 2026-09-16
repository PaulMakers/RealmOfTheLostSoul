# 🖥️ Lost Soul — UI/UX Design Document

**Status:** Melengkapi item terakhir yang tersisa di checklist Master Game Bible — "UI/UX Final Design (deliberately saved for last)"

**Dokumen pendamping:** `LostSoul.md` (semua sistem yang direferensikan di sini sudah lock), `Lost Soul Economy Balancing.md`, `Lost Soul NPC Dialog & Quest Text.md`, `Lost Soul City Content Addendum.md`

**Cakupan:** Layout tiap layar, elemen UI, trigger interaksi, dan pertimbangan cross-platform (PC/Mobile/Tablet, karena Roblox)

**Catatan bahasa:** Label tombol, judul menu, dan teks UI yang muncul langsung di game ditulis dalam Bahasa Inggris (konsisten dengan dialog NPC di dokumen sebelumnya). Penjelasan, struktur, dan catatan desain dalam Bahasa Indonesia.

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

1. **Server-authoritative, UI hanya menampilkan hasil** — selaras dengan Master Bible §Technical Notes (Networking): client mengirim *intent*, server memvalidasi dan menghitung. UI tidak pernah menampilkan angka yang belum dikonfirmasi server (misalnya damage preview boleh estimasi, tapi hasil aktual selalu menunggu balasan server).
2. **Transparansi angka** — mengikuti pola yang sudah dipakai di dialog NPC (Reward Officer selalu menyebut angka gold/EXP persis). UI harus konsisten: setiap transaksi (beli, jual, upgrade, reward quest, betting) menampilkan angka pasti, bukan animasi tanpa keterangan.
3. **Non-intrusive saat exploration, penuh informasi saat kombat** — HUD minim saat berjalan-jalan di kota/hunting ground, tapi elemen kombat (cooldown, HP musuh, party frame) muncul otomatis saat encounter dimulai dan hilang beberapa detik setelah combat selesai.
4. **Mobile-first constraint, desktop-enhanced** — karena Roblox mayoritas dimainkan di HP/tablet (§14), semua elemen interaktif didesain agar bisa disentuh dengan nyaman di layar kecil terlebih dahulu, baru diperkaya dengan shortcut keyboard/mouse untuk desktop.
5. **Reversibilitas terlihat jelas untuk aksi berisiko** — trading (3 detik lock), crafting (risiko gagal), PvP masuk zona (Master Bible: PvP death drop 5-50%), dan betting (irreversible saat match mulai) semua butuh konfirmasi visual yang jelas sebelum aksi final.

## Kapan UI Dibangun

Menunggu sampai sistem berikut ini lock (sudah terpenuhi per status Master Bible saat ini):

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

Daftar semua permukaan UI yang perlu dibangun, dikelompokkan berdasarkan kapan muncul:

| Kategori | Layar | Selalu Tampil? |
|---|---|---|
| **Persistent** | Main HUD | Ya |
| **Menu Utama** | Stat & Path, Inventory & Equipment, Quest Log, Map | Toggle (keybind/tombol) |
| **Kontekstual** | Shop/Trade Window, Dialog NPC, Crafting Station | Muncul saat interaksi |
| **Kombat** | Skill bar, Boss HP bar, Party frame | Muncul otomatis saat combat |
| **Sosial** | Guild panel, Chat | Toggle |
| **Sistem** | Notification/Toast, Settings | Event-driven / toggle |
| **City Content** | Colosseum Betting/Bracket, Craft Quality surfaces | Kontekstual/event-driven |

---

# 📟 MAIN HUD (SELALU TAMPIL)

## Elemen (posisi default, bisa disesuaikan di Settings)

| Elemen | Posisi | Isi |
|---|---|---|
| **HP/MP Bar** | Kiri atas | Bar HP + MP, angka numerik di atasnya |
| **Level & EXP** | Kiri atas, di bawah HP/MP | "Lv 47" + progress bar EXP tipis |
| **Quick Skill Bar** | Bawah tengah | 6-8 slot skill, cooldown radial, MP cost |
| **Minimap** | Kanan atas | Area sekitar, quest marker, PvP zone indicator |
| **Gold Counter** | Kanan atas, di bawah minimap | Angka gold saat ini, update real-time setiap transaksi |
| **Status Icon Bar** | Kiri, di bawah Level | Ikon buff/debuff aktif + timer |
| **Criminal Indicator** | Di atas nama karakter pemain | Ikon tengkorak merah jika Criminal aktif |

## Prinsip Layout

- HUD safe zone 90% dari layar.
- Semua elemen HUD punya opsi **opacity slider**.

---

# 📊 MENU STAT & PATH

## Layout

**Dua tab dalam satu panel:** `Stats` dan `Paths`.

### Tab Stats

- 7 slider/stepper untuk STR, VIT, INT, MND, AGI, DEX, LUK
- Nilai saat ini, efek formula real-time, indikator soft cap
- Poin bebas tersisa ditampilkan besar di atas
- Tombol `Confirm Allocation`

### Tab Paths

- Daftar semua Path yang dimiliki pemain, masing-masing dengan Path EXP progress bar
- Badge `Primary` dan tombol `Set as Primary`
- Path belum di-unlock ditampilkan grayed-out dengan syarat unlock
- Hidden Path belum ditemukan tidak ditampilkan sampai syarat terpenuhi

---

# 🎒 INVENTORY & EQUIPMENT

## Layout

**Split panel:** Equipment doll (kiri) + Inventory grid (kanan).

### Equipment Doll

- Slot: Weapon, Helm, Chest, Legs, Ring ×2, Amulet, Belt
- Setiap slot terisi menampilkan rarity border
- Ikon lock untuk item yang dikunci dari trade/drop

### Inventory Grid

- Filter: All / Weapon / Armor / Material / Consumable / Quest Item
- Quick-compare item
- Material otomatis stack
- Swipe-to-sell di mobile untuk item Common dengan konfirmasi popup

---

# 📜 QUEST LOG

## Layout

**Dua tab:** `System Quests` dan `Player Requests`.

### Tab System Quests

- Main Quest / Side Quest
- Status: Locked / Available / In Progress / Ready to Turn In / Completed
- Tap quest → ringkasan + tombol `Track`

### Tab Player Requests

- `My Postings` / `Available to Fulfill`
- My Postings: item, reward, expiry, cancel posting
- Available to Fulfill: daftar board scrollable

---

# 🏪 SHOP & TRADE WINDOW

## NPC Shop

- Tab `Buy` / `Sell`
- Buy: grid item dengan harga dan quantity stepper
- Sell: drag item ke area sell, harga otomatis terhitung dari formula Supply/Demand
- **Badge Fallback:** NPC Shop menampilkan badge kecil `NPC Fallback +20%` pada listing yang menggunakan fallback markup, dan `Standard quality` sebagai kualitas tetap.

## Player Shop

- Header menampilkan nama/foto penjual
- Badge `10% tax applied` saat seller menetapkan harga
- Criminal tidak dapat mengakses Player Shop

### Indikator Kualitas Crafting (Player Shop)

Setiap listing hasil craft player menampilkan badge kualitas **terpisah dari rarity item**:

| Kualitas | Warna Badge | Ikon |
|---|---|---|
| Standard | Abu-abu | — (tanpa ikon) |
| Fine | Hijau muda | 1 bintang kecil |
| Masterwork | Biru | 2 bintang kecil |
| Flawless | Emas | 3 bintang + glow tipis |

Badge quality tidak menggantikan border rarity Common→Mythic. Kedua indikator harus bisa dibaca secara independen.

## Trade Window (Player-to-Player)

- Dua panel berdampingan, area gold per pemain
- Checkbox `Ready`
- Kedua pemain Ready → countdown lock 3 detik
- Setelah lock → toast `Trade Complete`
- Disconnect → trade dibatalkan otomatis

---

# ⚔️ COMBAT & DUNGEON UI

## Elemen Kombat

- Skill bar
- Target frame dengan rank badge
- Boss HP bar + phase marker

## Party Frame

- Nama, HP/MP, status icon, jarak

## Dungeon-Specific UI

- Floor indicator
- Floor modifier banner
- Loot roll popup sesuai party convenience system

---

# 🏛️ GUILD & SOCIAL UI

## Guild Panel

- Tab: `Members` / `Bank` / `Shop` / `Quests`
- Bank: shared storage + transaction log
- Shop: guild listing + commission
- Quests: guild quest progress

## Chat

- Channel: `World` / `City` / `Guild` / `Party` / `Whisper`
- NPC dialog tetap overlay terpisah

---

# 🗺️ MAP & NAVIGATION

## World Map

- Menampilkan 8 map sebagai node terhubung
- Dungeon node menampilkan progress tertinggi
- Fast travel masih menjadi catatan terbuka jika belum diputuskan
- **City Content sub-markers:** Colosseum dan Cafe ditampilkan sebagai sub-marker di node kota; Trade Post menjadi sub-marker di Central Hunting Ground/Hunter's Outpost. Tidak membuat node map baru.

## Minimap

- Zoom in/out
- Toggle layer: Quest marker / Player marker (party only) / Resource node

---

# 🏟️ COLOSSEUM UI

## Betting Panel (menjelang match)

- Daftar 2 petarung (atau bracket turnamen), foto/model preview, win-rate history ringkas
- Input jumlah taruhan dengan stepper, **cap 5000 gold**
- Tombol `Confirm Bet` — mengunci taruhan; setelah match mulai tidak dapat dibatalkan
- Live odds indicator opsional untuk v1

## Tournament Bracket UI

- Bracket 8/16/32 slot, update real-time setelah match selesai
- Highlight slot pemain sendiri
- Reward preview di final slot: title kosmetik + gold pool distribution

## Betting Result Toast

| Trigger | Contoh Teks | Durasi |
|---|---|---:|
| Menang taruhan | `You won! +[X] gold from the pot` | 3 detik |
| Kalah taruhan | `Bet lost. Better luck next match.` | 2 detik |

---

# 🔴 INDIKATOR STATUS PVP/CRIMINAL

Mengikat langsung ke Master Bible §PvP & Criminal System:

| Status | Indikator Visual |
|---|---|
| **Normal** | Tidak ada indikator tambahan |
| **In PvP Zone** | Border merah tipis di tepi layar |
| **Criminal** | Ikon tengkorak merah di atas nametag + badge di HUD |
| **Bounty Aktif (sebagai target)** | Ikon koin merah tambahan di atas nametag |
| **Rehabilitation In Progress** | Progress bar kecil di menu Stat & Path |

---

# 🔔 SISTEM NOTIFIKASI & TOAST

## Jenis Toast

| Trigger | Contoh Teks | Durasi |
|---|---|---:|
| Reward quest | `+[X] gold, +[Y] EXP` | 3 detik |
| Level up | `Level Up! Lv 48` | Manual dismiss |
| Item drop rarity tinggi (Epic+) | Card khusus | 5 detik |
| Trade selesai | `Trade Complete` | 2 detik |
| Crafting gagal | `Craft failed — materials partially lost` | 3 detik |
| Guild bank activity | `[PlayerName] deposited Iron Ore ×10` | 2 detik |
| Bet menang | `You won! +[X] gold from the pot` | 3 detik |
| Bet kalah | `Bet lost. Better luck next match.` | 2 detik |

## Prinsip

- Maksimum 3 toast aktif bersamaan; selebihnya diantrikan
- Toast gold/item selalu menyebut angka pasti

---

# ⚙️ SETTINGS & ACCESSIBILITY

- HUD Opacity slider
- Colorblind mode dengan palet alternatif/pattern/icon support
- Text size
- Keybind remap + touch sensitivity
- Chat filter + mute per pemain

---

# 🛠️ CATATAN IMPLEMENTASI ROBLOX

## Cross-Platform (PC / Mobile / Tablet / Console)

- Gunakan `UIListLayout`/`UIGridLayout` + `UIAspectRatioConstraint`
- Tombol interaktif minimal 44×44 px pada mobile
- Skill bar: keybind 1-8 di desktop, tap di mobile

## Performa (1000 Concurrent Target)

- `Workspace.StreamingEnabled = true` pada map besar
- HUD `ScreenGui` memakai `ResetOnSpawn = false`
- Update elemen dinamis di-throttle kecuali combat aktif
- Colosseum UI di-load saat event/area relevan, bukan setiap frame

## Keamanan

- UI tidak menghitung hasil transaksi final
- Server mengonfirmasi semua gold/item/damage/quality/bet outcomes sebelum UI menampilkan hasil final
- Client hanya mengirim intent

---

# ✅ CHECKLIST IMPLEMENTASI

- [ ] Bangun Main HUD (HP/MP, Level/EXP, Skill bar, Minimap, Gold, Status icon, Criminal indicator)
- [ ] Bangun menu Stat & Path
- [ ] Bangun Inventory & Equipment
- [ ] Bangun Quest Log
- [ ] Bangun Shop/Trade Window (NPC fallback badge, Player Craft quality badge, Criminal block, Trade 3-detik lock)
- [ ] Bangun Combat/Dungeon UI
- [ ] Bangun Guild panel + Chat
- [ ] Bangun World Map + minimap layer toggle + city sub-markers
- [ ] Bangun Colosseum UI (Betting Panel, Tournament Bracket, result toast)
- [ ] Implementasikan Toast/Notification dengan antrian
- [ ] Implementasikan Settings
- [ ] Uji cross-platform (PC/Mobile/Tablet) untuk semua panel
- [ ] **Catatan terbuka:** fast travel antar map belum didefinisikan di Master Bible — perlu keputusan desain sebelum World Map UI final

---

**End of UI/UX Design Document**

Terakhir Diperbarui: September 2026

Review Berikutnya: Setelah Phase 4 (Polish & Optimization) — saat UI mulai diimplementasikan di Roblox Studio