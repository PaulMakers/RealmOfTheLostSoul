# 🖥️ Lost Soul — UI/UX Design Document

**Status:** Melengkapi item terakhir yang tersisa di checklist Master Game Bible — "UI/UX Final Design (deliberately saved for last)"

**Dokumen pendamping:** `LostSoul.md` (semua sistem yang direferensikan di sini sudah lock), `Lost_Soul_Economy_Balancing.md`, `Lost_Soul_NPC_Dialogue_Quest_Text.md`

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
2. **Transparansi angka** — mengikuti pola yang sudah dipakai di dialog NPC (Reward Officer selalu menyebut angka gold/EXP persis). UI harus konsisten: setiap transaksi (beli, jual, upgrade, reward quest) menampilkan angka pasti, bukan animasi tanpa keterangan.
3. **Non-intrusive saat exploration, penuh informasi saat kombat** — HUD minim saat berjalan-jalan di kota/hunting ground, tapi elemen kombat (cooldown, HP musuh, party frame) muncul otomatis saat encounter dimulai dan hilang beberapa detik setelah combat selesai.
4. **Mobile-first constraint, desktop-enhanced** — karena Roblox mayoritas dimainkan di HP/tablet (§14), semua elemen interaktif didesain agar bisa disentuh dengan nyaman di layar kecil terlebih dahulu, baru diperkaya dengan shortcut keyboard/mouse untuk desktop.
5. **Reversibilitas terlihat jelas untuk aksi berisiko** — trading (3 detik lock), crafting (risiko gagal), PvP masuk zona (Master Bible: PvP death drop 5-50%) semua butuh konfirmasi visual yang jelas sebelum aksi final, karena ini semua melibatkan gold/item yang bisa hilang.

## Kapan UI Dibangun

Menunggu sampai sistem berikut ini lock (sudah terpenuhi per status Master Bible saat ini):

- Path system dengan multi-Path aktif
- Quest 5-state (Locked/Available/In Progress/Ready/Completed)
- Trading dengan lock 3 detik
- Crafting success/failure rate
- Soft cap stat allocation
- Criminal/Bounty status

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

---

# 📟 MAIN HUD (SELALU TAMPIL)

## Elemen (posisi default, bisa disesuaikan di Settings)

| Elemen | Posisi | Isi |
|---|---|---|
| **HP/MP Bar** | Kiri atas | Bar HP (merah) + MP (biru), angka numerik di atasnya (mis. "1240/1500") |
| **Level & EXP** | Kiri atas, di bawah HP/MP | "Lv 47" + progress bar EXP tipis, tooltip saat hover menampilkan EXP tersisa ke level berikutnya (dari formula EXP di Master Bible §Progression System) |
| **Quick Skill Bar** | Bawah tengah | 6-8 slot skill (sesuai elemen yang dipelajari), menampilkan cooldown sebagai overlay radial, dan MP cost kecil di pojok slot |
| **Minimap** | Kanan atas | Area sekitar, quest marker (kuning = available, biru = in progress, emas = ready to turn in — konsisten dengan 5-state di NPC Dialogue doc), PvP zone indicator (border merah tipis jika sedang di zona PvP) |
| **Gold Counter** | Kanan atas, di bawah minimap | Angka gold saat ini, update real-time setiap transaksi |
| **Status Icon Bar** | Kiri, di bawah Level | Ikon kecil untuk buff/debuff aktif (dari Dark element HP-cost recovery, Berserker "below 30% HP" trait, dsb.), dengan timer countdown |
| **Criminal Indicator** | Di atas nama karakter pemain (world-space, terlihat pemain lain) | Ikon tengkorak merah muncul jika status Criminal aktif — lihat §11 |

## Prinsip Layout

- HUD dirancang dalam **safe zone 90%** dari layar (menyisakan margin untuk notch/status bar HP di mode mobile).
- Semua elemen HUD punya opsi **opacity slider** (Settings) supaya tidak menghalangi visual saat screenshot/eksplorasi santai.

---

# 📊 MENU STAT & PATH

## Layout

**Dua tab dalam satu panel:** `Stats` dan `Paths`.

### Tab Stats

- 7 slider/stepper untuk STR, VIT, INT, MND, AGI, DEX, LUK (Master Bible §Seven Main Stats)
- Setiap stat menampilkan: nilai saat ini, efek formula real-time (mis. "Physical ATK: 340 → 346" saat +1 STR di-preview), dan **indikator soft cap** (warna hijau 0-50 poin, kuning 51-100, merah 101+ — sesuai tabel Soft Cap di Master Bible)
- Poin bebas tersisa ditampilkan besar di atas ("12 points remaining")
- Tombol `Confirm Allocation` — karena ini server-authoritative, alokasi tidak permanen sampai dikonfirmasi (mencegah misklik pada mobile touch)

### Tab Paths

- Daftar semua Path yang dimiliki pemain (mendukung multi-Path aktif per Master Bible §Multiple Paths), masing-masing dengan:
  - Path EXP progress bar
  - Badge "Primary" pada Path yang sedang aktif utama
  - Tombol `Set as Primary` (switch tanpa penalti)
- Path yang belum di-unlock ditampilkan **grayed-out dengan syarat unlock** (mis. "Unlocks at Lv 15") — bukan disembunyikan total, supaya pemain tahu ada progression system untuk dituju.
- Hidden Path yang belum ditemukan **tidak ditampilkan sama sekali** (sesuai sifat "hidden" di Master Bible §Hidden Paths) — baru muncul begitu syaratnya terpenuhi, dengan animasi unlock khusus.

---

# 🎒 INVENTORY & EQUIPMENT

## Layout

**Split panel:** Equipment doll (kiri) + Inventory grid (kanan).

### Equipment Doll

- Slot: Weapon, Helm, Chest, Legs, Ring ×2, Amulet, Belt (sesuai Master Bible §Equipment Pricing Curve dan §Accessory Pricing)
- Setiap slot terisi menampilkan rarity border (warna sesuai Common → Mythic, konsisten dengan warna rarity di seluruh dokumen)
- **Ikon lock** di pojok slot — item terkunci tidak bisa di-trade/ter-drop tidak sengaja (relevan untuk item Bind-on-Pickup seperti Blueprint boss drop, Master Bible §Crafting System)

### Inventory Grid

- Grid standar dengan filter tab: All / Weapon / Armor / Material / Consumable / Quest Item
- Quick-compare: tap-hold item menampilkan perbandingan stat dengan item yang sedang dipakai di slot yang sama
- Material gathering (Common → Legendary) otomatis stack, dengan angka jumlah di pojok
- Swipe-to-sell tersedia di mode mobile untuk item Common (mengurangi friksi jual cepat), dengan konfirmasi popup

---

# 📜 QUEST LOG

## Layout

**Dua tab:** `System Quests` dan `Player Requests` (sesuai dua jenis quest di Master Bible §Quest System).

### Tab System Quests

- Sub-filter: Main Quest / Side Quest
- Setiap entry menampilkan status sesuai 5-state (NPC Dialogue doc §3):
  - 🔒 Locked (tidak ditampilkan, atau abu-abu dengan syarat jika `hint_when_locked`)
  - 📋 Available (belum diterima — tampil di daftar terpisah "Nearby Quests" jika pemain dekat NPC pemberi)
  - ⏳ In Progress — dengan progress bar objective (mis. "3/5 Iron Ore collected")
  - ✅ Ready to Turn In — highlight emas + tombol "Track" untuk mengarahkan minimap ke NPC
  - ✔️ Completed (arsip, bisa dilihat tapi tidak aktif)
- Tap quest → menampilkan ringkasan + tombol `Track` (memunculkan waypoint di minimap dan world-space marker di atas objective)

### Tab Player Requests

- Sub-filter: `My Postings` / `Available to Fulfill`
- My Postings menampilkan: item diminta, reward, sisa waktu (dari 7 hari expiry, Master Bible §Player-Generated Quest), tombol `Cancel Posting` (refund parsial sesuai kebijakan tax yang sudah dibayar)
- Available to Fulfill: daftar board scrollable, sesuai tampilan Board Clerk di NPC Dialogue doc §10

---

# 🏪 SHOP & TRADE WINDOW

## NPC Shop

- Tab `Buy` / `Sell`
- Buy: grid item dengan harga, quantity stepper, total cost real-time
- Sell: drag item dari inventory ke area sell, harga otomatis terhitung dari formula `NPC_Buy_Price = Item_Base_Price × 0.5 × Supply/Demand_Modifier` (Master Bible §Shops) — modifier ditampilkan sebagai badge kecil ("High Supply ×0.7") supaya pemain paham kenapa harga naik-turun

## Player Shop

- Tampilan mirip NPC shop tapi dengan foto/nama penjual di header
- Badge "10% tax applied" muncul saat pemain sendiri sedang set harga jual, supaya transparan sebelum listing
- **Tidak dapat diakses sama sekali oleh pemain berstatus Criminal** (Master Bible §Shops) — UI menampilkan pesan block yang jelas alih-alih tombol nonaktif tanpa penjelasan: *"Player Shops are closed to Criminal-flagged adventurers."*

## Trade Window (Player-to-Player)

- Dua panel berdampingan (item milikku / item lawan), area gold di bawah masing-masing
- Checkbox `Ready` per pemain
- Saat kedua `Ready` tercentang → **countdown lock 3 detik** ditampilkan besar di tengah (mencegah scam swap-after-accept, Master Bible §Trading) — selama countdown, kedua panel item di-freeze visual (tidak bisa diubah)
- Setelah lock selesai → animasi konfirmasi + toast "Trade Complete"
- Disconnect salah satu pihak → trade otomatis batal, toast "Trade cancelled — player disconnected"

---

# ⚔️ COMBAT & DUNGEON UI

## Elemen Kombat (muncul otomatis saat encounter)

- **Skill bar** membesar sedikit dan pindah ke lower-center dengan cooldown radial lebih jelas
- **Target frame** (musuh yang di-lock): HP bar + nama + rank badge (E/D/C/B/A/S, warna sesuai rank)
- **Boss HP bar** (khusus dungeon boss, Master Bible §Boss Mechanics): bar besar di atas layar, dengan **phase marker** — garis pembatas di sepanjang bar menandai transisi phase (mis. 2 garis untuk boss 3-phase), dan ikon kecil muncul saat boss masuk phase Summon Adds atau state khusus lain

## Party Frame

- Muncul di kiri layar saat dalam party (dungeon run)
- Per anggota: nama, HP/MP bar mini, status icon (buff/debuff), jarak (jika terlalu jauh, nama memudar sebagai peringatan)

## Dungeon-Specific UI

- **Floor indicator** — "Floor 47/100" persisten di pojok saat dalam dungeon instance (Master Bible §Dungeon System)
- **Floor modifier banner** — muncul sekali saat masuk floor baru jika ada modifier aktif dari Dungeon Floor Randomization (mis. "⚠️ Modifier: Elite Density +50%"), hilang otomatis setelah 5 detik
- **Loot roll popup** — saat item drop dari boss/monster, muncul card kecil dari bawah layar menampilkan item + rarity, dengan opsi `Need` / `Greed` jika dalam party (sistem loot party — ditambahkan sebagai UI-level convenience, tidak mengubah sistem drop yang sudah didefinisikan di Master Bible)

---

# 🏛️ GUILD & SOCIAL UI

## Guild Panel

- Tab: `Members` / `Bank` / `Shop` / `Quests`
- **Members:** daftar dengan online status, role (Leader/Officer/Member), tombol invite (jika punya izin)
- **Bank:** grid item shared storage + log transaksi terbaru (siapa ambil/taruh apa, kapan) — penting karena ini shared state yang ditulis banyak pemain (Master Bible §Technical Notes: DataStore guild pakai `UpdateAsync` retry-on-conflict)
- **Shop:** listing item dari guild storage dengan commission 5% (Master Bible §Guild Shop) ditampilkan jelas di setiap listing
- **Quests:** guild quest aktif (jika ada), progress kontribusi per anggota

## Chat

- Tab channel: `World` / `City` (per lokasi) / `Guild` / `Party` / `Whisper`
- Chat NPC dialog **tidak** memakai channel yang sama — dialog NPC muncul sebagai overlay terpisah (dialogue box, bukan chat log) supaya tidak tercampur dengan chat pemain lain

---

# 🗺️ MAP & NAVIGATION

## World Map (toggle penuh layar)

- Menampilkan 8 map sebagai node terhubung (Master Bible §Map Structure): 3 City, 2 Hunting Ground, 3 Dungeon entrance
- Dungeon node menampilkan progress tertinggi yang pernah dicapai pemain (mis. "Best: Floor 62/100")
- Fast travel (jika ada — belum didefinisikan di Master Bible, ditandai sebagai **catatan terbuka** di §15) kemungkinan lewat `TeleportService` antar Place yang sudah dijelaskan di Technical Notes

## Minimap (persistent, lihat §3)

- Zoom in/out dengan pinch (mobile) atau scroll wheel (desktop)
- Toggle layer: Quest marker / Player marker (party only) / Resource node (gathering)

---

# 🔴 INDIKATOR STATUS PVP/CRIMINAL

Mengikat langsung ke Master Bible §PvP & Criminal System dan gating dialog di NPC Dialogue doc §12, supaya konsisten di semua permukaan UI:

| Status | Indikator Visual |
|---|---|
| **Normal** | Tidak ada indikator tambahan |
| **In PvP Zone** | Border merah tipis di tepi layar (Central Hunting Ground zone tertentu, Elf Hunting Ground zone tertentu) |
| **Criminal** | Ikon tengkorak merah di atas nametag (world-space, terlihat pemain lain), badge di HUD kiri atas |
| **Bounty Aktif (sebagai target)** | Ikon koin merah tambahan di atas nametag — memberi sinyal ke bounty hunter lain tanpa perlu membuka Quest Board |
| **Rehabilitation In Progress** | Progress bar kecil di menu Stat & Path (bukan HUD utama, supaya tidak terasa menghukum terus-menerus saat eksplorasi biasa) |

---

# 🔔 SISTEM NOTIFIKASI & TOAST

## Jenis Toast

| Trigger | Contoh Teks | Durasi |
|---|---|---:|
| Reward quest | "+220 gold, +300 EXP" | 3 detik |
| Level up | "Level Up! Lv 48" (animasi lebih besar, tidak auto-dismiss, perlu tap) | Manual dismiss |
| Item drop rarity tinggi (Epic+) | Card khusus dengan efek glow, lebih besar dari toast biasa | 5 detik |
| Trade selesai | "Trade Complete" | 2 detik |
| Crafting gagal | "Craft failed — materials partially lost" | 3 detik |
| Guild bank activity | "[PlayerName] deposited Iron Ore ×10" (opsional, toggle di Settings karena bisa spam di guild aktif) | 2 detik |

## Prinsip

- Toast tidak pernah menumpuk lebih dari 3 di layar bersamaan — antrian otomatis
- Toast terkait gold/item **selalu** menyebut angka pasti (selaras dengan prinsip transparansi §1)

---

# ⚙️ SETTINGS & ACCESSIBILITY

- **HUD Opacity** slider
- **Colorblind mode** — penting karena banyak sistem bergantung warna (rarity, soft cap indicator, PvP border, rank badge) — perlu palet alternatif atau pattern/ikon tambahan, bukan warna saja
- **Text size** — untuk keterbacaan dialog NPC dan quest text di layar kecil (mobile)
- **Controls:** keybind remap (desktop), sensitivity touch (mobile)
- **Chat filter:** toggle channel mana yang tampil, mute per pemain

---

# 🛠️ CATATAN IMPLEMENTASI ROBLOX

## Cross-Platform (PC / Mobile / Tablet / Console)

- Semua panel dibangun dengan `UIListLayout`/`UIGridLayout` + `UIAspectRatioConstraint` supaya scale otomatis mengikuti ukuran layar — tidak memakai posisi absolut piksel.
- Tombol interaktif minimal **44×44 px** (standar touch target) di mode mobile, walau visualnya bisa lebih kecil di desktop.
- Skill bar: keybind 1-8 di desktop, tap langsung di mobile — tidak ada perbedaan fungsi, hanya metode input.

## Performa (selaras dengan target 1000 concurrent, Master Bible §Performance)

- HUD memakai `ScreenGui` dengan `ResetOnSpawn = false` supaya tidak re-render penuh setiap respawn
- Update elemen yang sering berubah (HP bar, minimap player dot) di-throttle ke interval pendek (bukan per-frame) kecuali saat combat aktif
- Boss HP bar dan Party frame hanya di-load saat instance combat/dungeon aktif (dungeon instancing sudah membatasi ini secara alami per Technical Notes)

## Keamanan (selaras dengan Master Bible §Security)

- UI tidak pernah menghitung hasil transaksi sendiri untuk ditampilkan sebagai final — semua angka final (gold setelah trade, damage setelah hit) menunggu event balasan dari server, walau boleh menampilkan angka *preview* estimasi sebelum konfirmasi

---

# ✅ CHECKLIST IMPLEMENTASI

- [ ] Bangun Main HUD (HP/MP, Level/EXP, Skill bar, Minimap, Gold, Status icon, Criminal indicator)
- [ ] Bangun menu Stat & Path (dua tab, soft cap indicator, multi-Path switcher)
- [ ] Bangun Inventory & Equipment (doll + grid, lock icon, quick-compare)
- [ ] Bangun Quest Log (dua tab, 5-state visual, tracking ke minimap)
- [ ] Bangun Shop/Trade Window (NPC shop, Player shop dengan Criminal block, Trade window dengan 3-detik lock)
- [ ] Bangun Combat/Dungeon UI (target frame, boss HP + phase marker, party frame, floor indicator)
- [ ] Bangun Guild panel (Members/Bank/Shop/Quests) + Chat channel
- [ ] Bangun World Map + minimap layer toggle
- [ ] Implementasikan sistem Toast/Notification dengan antrian
- [ ] Implementasikan Settings (opacity, colorblind mode, text size, keybind, chat filter)
- [ ] Uji cross-platform (PC/Mobile/Tablet) untuk semua panel di atas
- [ ] **Catatan terbuka:** fast travel antar map belum didefinisikan di Master Bible — perlu keputusan desain sebelum UI World Map final (apakah gratis, berbayar gold, atau butuh syarat tertentu)

---

**End of UI/UX Design Document**

Terakhir Diperbarui: September 2026

Review Berikutnya: Setelah Phase 4 (Polish & Optimization) — saat UI mulai diimplementasikan di Roblox Studio