# 🏦 Sakumaya Digital Bank — Bank yang Stabil, Sistem yang Perlu Dirapikan

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?logo=linkedin&logoColor=white)](https://linkedin.com/in/ghifarryalnaffriza)
[![GitHub](https://img.shields.io/badge/GitHub-181717?logo=github&logoColor=white)](https://github.com/ghifarryalnaffriza)
[![Instagram](https://img.shields.io/badge/Instagram-E4405F?logo=instagram&logoColor=white)](https://instagram.com/ghifaralnaffi_)
[![Email](https://img.shields.io/badge/Email-D14836?logo=gmail&logoColor=white)](mailto:ghifaralns@gmail.com)

> Financial health analytics untuk bank digital: fondasi sehat (AUM Rp 84,5 M, success rate 98,0%), tapi **GMV jalan di tempat 38 bulan** dan **Rp 27,9 miliar dana nasabah menganggur** — tanpa perlu satu pun nasabah baru.

## 🎯 Business Problem

Sakumaya terlihat sehat di angka agregat, tapi pertumbuhan nasabah tidak berubah jadi pertumbuhan transaksi. Sepuluh pertanyaan bisnis lintas divisi (Compliance, Risk, Growth, Wealth, Engineering, Direksi) dibedah untuk menjawab: **di mana kebocoran sistem yang membuat bank ini berhenti tumbuh, dan berapa nilai uang yang bisa dibangunkan tanpa akuisisi baru?**

## 📊 Dataset

- **Sumber:** 5 tabel relasional — `customers`, `accounts`, `transactions`, `loans`, `cards`
- **Volume:** 1.000 nasabah · 1.000 akun aktif · 10.000 transaksi · 300 pinjaman
- **Periode:** Jan 2022 – Feb 2025 (38 bulan)
- **Cakupan:** 5+ kota · 4 tier rekening · 4 channel · 9 kategori merchant

## 🏗️ Arsitektur & Pendekatan

Medallion architecture, dipisah ke tiga schema (`bronze` / `silver` / `gold`):

- **Bronze** — 5 CSV dimuat apa adanya, semua kolom `TEXT` supaya proses load tidak pernah gagal + metadata `_ingested_at` dan `_source_file`.
- **Silver** — casting tipe data, parsing tanggal & waktu, standardisasi kategori, dan penurunan flag analitik (status KYC, segmen saldo, band jam transaksi). Baris bermasalah di-flag, bukan dibuang.
- **Gold** — 19 view analitik yang dipetakan langsung ke pertanyaan bisnis (`vw_q1_kyc_funnel`, `vw_q5_tier_mismatch`, `vw_q7_npl_per_loan_type`, `vw_q9_vintage`, `vw_q10_clv_top20`, dst.) — satu pertanyaan, satu view, siap dipakai dashboard.

Penamaan view yang mengikuti nomor pertanyaan bikin setiap chart di dashboard bisa dilacak balik ke satu query yang jelas.

## 🛠️ Tools & Tech

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=for-the-badge&logo=databricks&logoColor=white)
![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Medallion](https://img.shields.io/badge/Medallion_Architecture-4B8BBE?style=for-the-badge&logo=databricks&logoColor=white)

## 🔍 Key Findings

- **Funnel KYC bocor 30%:** hanya 700 dari 1.000 nasabah verified. Bali (63,3%) dan Yogyakarta (65,0%) terlemah — **250 nasabah masih bisa diselamatkan**, hanya 50 yang benar-benar ditolak.
- **Rp 27,9 miliar dana menganggur** (sepertiga AUM): Rp 10,9 M di 150 akun dormant + **Rp 17,0 M** milik 250 nasabah yang terblokir dari produk pinjaman karena KYC.
- **GMV stagnan 38 bulan:** Rp 25,2 M (2022) → 26,4 M (+4,8%) → 25,4 M (−3,9%). Berosilasi Rp 1,7–2,5 M/bulan tanpa tren — masalahnya frekuensi, bukan akuisisi.
- **Sistem tier rusak:** avg saldo platinum justru **terendah (Rp 65,4 jt)** vs silver Rp 87,6 jt. **185 nasabah affluent** (>Rp 100 jt) terjebak di tier basic/silver.
- **Kegagalan transaksi berpola, bukan acak:** mobile_app 2,29% & jam 06–12 2,52%; kombinasi terburuk merchant × 06–12 = **3,43% (1,7× rata-rata nasional)**, sementara ATM stabil di 1,19%.
- **Risiko kredit terkonsentrasi:** kredit_barang NPL **22,0% by count / 28,1% by outstanding** — terburuk di dua metrik; modal_usaha justru tersehat (9,0%) meski principal-nya terbesar.
- **Vintage 2023 anomali:** NPL 16,8% vs 11,6% (2022) dan 10,3% (2024) — bukan tren, melainkan indikasi underwriting yang dilonggarkan.
- **Referral bukan mesin engagement:** 10,86 vs 10,66 trx/nasabah (**selisih 1,9%**), cohort 90 hari identik (0,82 vs 0,82) — tapi menyumbang **67,5% akuisisi**.
- **Nilai terkonsentrasi ekstrem:** 184 nasabah top-20% menguasai **48,2% nilai bank**, 58,5% aktivitasnya via mobile_app, terpusat di Jakarta (63), Surabaya (35), Bandung (26).

## 📁 Struktur Repo
```bash
sakumaya-financial-health-analytics/
├── README.md
├── raw_data/ # 5 CSV sumber (customers, accounts, transactions, loans, cards)
├── Analyst/ # SQL Medallion: bronze → silver → gold (19 view analitik)
├── Visualisasi/ # dashboard 6 halaman (export PDF)
└── Presentation Deck/ # storyline deck 16 slide (PDF)
```

## 🛡️ License

Project ini dilisensikan di bawah [MIT License](LICENSE). Bebas dipakai, dimodifikasi, dan dibagikan dengan atribusi yang sesuai.

## 🌟 About Me

Hai! Aku **Ghifarry Alnaffriza**, mahasiswa Pembangunan Ekonomi Kewilayahan di Sekolah Vokasi UGM yang lagi ngebangun jalan sebagai **data/business analyst**. Aku suka ngulik data buat nemuin cerita di balik angka — kayak project Sakumaya ini.

Yuk connect! Boleh reach out lewat platform berikut:

[![LinkedIn](https://img.shields.io/badge/LINKEDIN-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/ghifarryalnaffriza)
[![GitHub](https://img.shields.io/badge/GITHUB-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/ghifarryalnaffriza)
[![Instagram](https://img.shields.io/badge/INSTAGRAM-E4405F?style=for-the-badge&logo=instagram&logoColor=white)](https://instagram.com/ghifaralnaffi_)
[![Email](https://img.shields.io/badge/EMAIL-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:ghifaralns@gmail.com)
