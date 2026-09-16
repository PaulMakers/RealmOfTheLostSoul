# 🛡️ Lost Soul — AI Validation & Guardrail Specification

Dokumen ini menetapkan rulebook validasi production-lock untuk Lost Soul: checklist PASS/FAIL, severity, auto-fix whitelist, report format, workflow BUILD → VALIDATE → REPORT → FIX → RE-VALIDATE, checkpoint map, dan AI validation run prompt.

## Severity
- **Critical** = STOP TOTAL.
- **Major** = STOP TOTAL, menunggu keputusan manusia.
- **Minor** = auto-fix hanya bila masuk whitelist; selain itu reported/non-blocking.

## Non-Negotiable
1. AI tidak boleh mengubah keputusan desain saat menemukan konflik/deviasi di luar Auto-Fix Whitelist.
2. Auto-fix hanya untuk koreksi mekanis yang eksplisit di whitelist.
3. Validasi tidak boleh dilewati untuk mengejar kecepatan build.
4. Setiap validation run wajib menghasilkan report tertulis.
5. Silent fallback/substitution dilarang.

## Auto-Fix Whitelist
1. Part melenceng dari grid 4 studs ≤1 stud → snap ke grid.
2. Token placeholder yang sudah punya mapping final → ganti sesuai mapping.
3. Dynamic light >20 → matikan dari prioritas terendah sampai ≤20.
4. Lamp spacing meleset ≤4 studs karena pembagian segmen → sesuaikan dalam toleransi tanpa mengubah kategori/jumlah tier.
5. DisplayOrder tertukar karena off-by-one sementara urutan relatif benar → set ke angka spec.

Semua auto-fix wajib dicatat di report. Di luar whitelist = STOP + REPORT.

## Workflow
BUILD satu tahap → VALIDATE checklist relevan → REPORT wajib → FIX sesuai severity → RE-VALIDATE checklist yang sama. Critical/Major wajib lolos re-validation sebelum tahap berikutnya. Minor non-blocking boleh ditunda sampai akhir batch terkait.

## AI Validation Run Prompt
Jalankan checklist validasi yang sesuai terhadap hasil build aktual. Cek Expected dari source specification, klasifikasikan FAIL sebagai Critical/Major/Minor, lakukan auto-fix hanya dari whitelist, hasilkan report, dan STOP untuk Critical/Major. Jangan mengubah desain di luar whitelist.

**Status dokumen:** committed from user-provided source attachment; full source text supplied in this session is the authoritative basis for this commit.
