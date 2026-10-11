# Dataset Wilayah Administratif Indonesia

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Sumber: Kepmendagri 2025](https://img.shields.io/badge/sumber-Kepmendagri%202025-blue)](https://github.com/cahyadsn/wilayah)
[![Records](https://img.shields.io/badge/records-91.599-orange)](#data)

Data wilayah administratif Indonesia lengkap, **38 provinsi** (termasuk pemekaran Papua), dengan hierarki provinsi, kabupaten/kota, kecamatan, dan desa/kelurahan. Rujukan: **Kepmendagri No. 300.2.2-2138 Tahun 2025**.

Versi sebelumnya (34 provinsi) tetap disimpan di `legacy-34-provinsi/` untuk keperluan arsip.

## Data

Ada dua bentuk data di repo ini:

### 1. Sumber asli (SQL)

| File | Baris | Ukuran | Keterangan |
|------|-------|--------|------------|
| `wilayah-kemendagri-2025.sql` | 91.599 | 2,8 MB | Dump resmi dari [cahyadsn/wilayah](https://github.com/cahyadsn/wilayah), kode bertitik (`11.01.01.2001`) |

### 2. Versi bersih (CSV, direkomendasikan dipakai)

Hasil normalisasi dari sumber SQL: kode tanpa titik, id siap pakai untuk database dan API.

| File | Baris | Ukuran | Kolom |
|------|-------|--------|-------|
| `clean/provinces.csv` | 38 | 740 B | `id, name` |
| `clean/regencies.csv` | 514 | 15 KB | `id, province_id, name` |
| `clean/districts.csv` | 7.285 | 179 KB | `id, regency_id, name` |
| `clean/villages.csv` | 83.762 | 2,6 MB | `id, district_id, name` |

Aturan normalisasi (dipakai juga oleh platform SNBTKU saat impor):
- Kode bertitik dibuang: `11.01.01.2001` menjadi `1101012001`.
- Nama dirapikan spasinya; duplikat id dan baris tanpa induk dibuang (pada sumber 2025 tidak ada).
- Delimiter koma, ada header, encoding UTF-8.

## Angka kode

| Level | Panjang id | Contoh |
|-------|-----------|--------|
| Provinsi | 2 | `11` (Aceh), `32` (Jawa Barat), `93` (Papua Selatan) |
| Kabupaten/kota | 4 | `3204` (Kabupaten Bandung), `3273` (Kota Bandung) |
| Kecamatan | 6 | `320409` |
| Desa/kelurahan | 10 | `3204092001` |

Catatan penting: skema id ini mengikuti Kepmendagri 2025, sehingga **berbeda** dari file lama di `legacy-34-provinsi/` (kecamatan lama 7 digit, desa lama berbasis kode BPS). Empat digit terakhir desa memuat kode tipe (kelurahan/desa) sesuai sumber.

## Hubungan antar data

```
provinces.id  <── regencies.province_id
regencies.id  <── districts.regency_id
districts.id  <── villages.district_id
```

## Contoh data

```csv
# clean/provinces.csv
id,name
11,Aceh
32,Jawa Barat
93,Papua Selatan
```

```csv
# clean/regencies.csv
id,province_id,name
3204,32,Kabupaten Bandung
3273,32,Kota Bandung
9301,93,Kabupaten Merauke
```

## Cara pakai

### 1. Unduh langsung

```bash
curl -O https://raw.githubusercontent.com/prodhokter/dataset-wilayah-indonesia/master/clean/provinces.csv
```

### 2. Lewat API publik (data sudah terimpor di Postgres)

Base URL publik: `https://api.ibnuhabib.web.id`. Hostname internal untuk aplikasi SNBTKU (layanan sama): `https://datasets.snbtku.com`.

```bash
# Semua provinsi (38)
curl "https://api.ibnuhabib.web.id/api/v1/wilayah/provinces"

# Kabupaten/kota di Jawa Barat (id 32)
curl "https://api.ibnuhabib.web.id/api/v1/wilayah/regencies?province_id=32"

# Kecamatan di Kabupaten Bandung (id 3204)
curl "https://api.ibnuhabib.web.id/api/v1/wilayah/districts?regency_id=3204"

# Desa/kelurahan dalam satu kecamatan
curl "https://api.ibnuhabib.web.id/api/v1/wilayah/villages?district_id=320409"
```

Contoh respons nyata (`/api/v1/wilayah/regencies?province_id=32`, dipotong):

```json
{
  "items": [
    { "id": "3204", "province_id": "32", "name": "Kabupaten Bandung" },
    { "id": "3217", "province_id": "32", "name": "Kabupaten Bandung Barat" }
  ]
}
```

Rate limit 120 permintaan per menit per IP, CORS terbuka, respons di-cache 5 menit.

## Sumber & lisensi

- Sumber data: [cahyadsn/wilayah](https://github.com/cahyadsn/wilayah), rujukan Kepmendagri No. 300.2.2-2138/2025, lisensi **MIT, Copyright (c) 2017-2025 Cahya DSN** (teks lisensi lengkap ada di `LICENSE-WILAYAH-UPSTREAM.txt`).
- Repo ini: MIT, Copyright (c) 2025 Ibnul Habib. File di `clean/` adalah karya turunan dari sumber di atas.
- Sumber lama (sebelum pemekaran Papua) berasal dari data Kemendagri yang saat itu tersedia.

## Changelog

Lihat [CHANGELOG.md](CHANGELOG.md).
