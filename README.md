# Dataset Wilayah Administratif Indonesia

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![API Status](https://img.shields.io/badge/api-live-green)](https://api.ibnuhabib.web.id/api/wilayah/provinces)
[![Records](https://img.shields.io/badge/records-88.297-orange)](#data)

Data wilayah administratif Indonesia: provinsi, kabupaten/kota, kecamatan, dan desa/kelurahan. Bersumber dari data Kemendagri.

## Data

| File | Records | Size | Kolom |
|------|---------|------|-------|
| `provinces.csv` | 34 | 551 B | `id, name` |
| `regencies.csv` | 514 | 14 KB | `id, province_id, name` |
| `districts.csv` | 7.215 | 166 KB | `id, regency_id, name` |
| `villages.csv` | 80.534 | 2.3 MB | `id, district_id, name` |

**Delimiter:** koma (`,`)  
**Tanpa header** — data langsung dari baris pertama.

## Hubungan Antar Data

```
province.id ──< regencies.province_id
regency.id  ──< districts.regency_id
district.id ──< villages.district_id
```

## Contoh Data

**provinces.csv:**
```csv
11,ACEH
12,SUMATERA UTARA
```

**regencies.csv:**
```csv
1101,11,KABUPATEN SIMEULUE
1102,11,KABUPATEN ACEH SINGKIL
```

**districts.csv:**
```csv
1101010,1101,SIMEULUE TIMUR
1101020,1101,TEUPAH SELATAN
```

**villages.csv:**
```csv
1101012001,1101010,AIR DINGIN
1101012002,1101010,AMAITENG MULYA
```

## API

Gunakan [api-datasets-indonesia](https://github.com/prodhokter/api-datasets-indonesia) untuk akses REST API.

**Base URL:** `https://api.ibnuhabib.web.id`

```bash
# Semua provinsi
curl "https://api.ibnuhabib.web.id/api/wilayah/provinces"

# Kabupaten/kota di Aceh (id=11)
curl "https://api.ibnuhabib.web.id/api/wilayah/regencies/11"

# Kecamatan di Kab. Simeulue (id=1101)
curl "https://api.ibnuhabib.web.id/api/wilayah/districts/1101"

# Desa/kelurahan di kecamatan tertentu
curl "https://api.ibnuhabib.web.id/api/wilayah/villages/1101010"

# Download CSV
curl -O "https://api.ibnuhabib.web.id/download/wilayah/provinces.csv"
curl -O "https://api.ibnuhabib.web.id/download/wilayah/regencies.csv"
curl -O "https://api.ibnuhabib.web.id/download/wilayah/districts.csv"
curl -O "https://api.ibnuhabib.web.id/download/wilayah/villages.csv"
```

## Dataset Terkait

- [api-datasets-indonesia](https://github.com/prodhokter/api-datasets-indonesia) — REST API
- [dataset-sekolah-indonesia](https://github.com/prodhokter/dataset-sekolah-indonesia)
- [dataset-perguruan-tinggi-indonesia](https://github.com/prodhokter/dataset-perguruan-tinggi-indonesia)
- [dataset-program-studi-indonesia](https://github.com/prodhokter/dataset-program-studi-indonesia)
- [dataset-kbbi-indonesia](https://github.com/prodhokter/dataset-kbbi-indonesia)

## Sumber

Fork dari [emsifa/api-wilayah-indonesia](https://github.com/emsifa/api-wilayah-indonesia) — data Kemendagri.

## Lisensi

MIT — sesuai lisensi repository asli.
