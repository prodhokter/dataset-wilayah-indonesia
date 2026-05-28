# Dataset Wilayah Administratif Indonesia

Data wilayah administratif Indonesia: provinsi, kabupaten/kota, kecamatan, dan desa/kelurahan.

## Data

| File | Records | Size | Kolom |
|------|---------|------|-------|
| `provinces.csv` | 34 | 551 B | `id, name` |
| `regencies.csv` | 514 | 14 KB | `id, province_id, name` |
| `districts.csv` | 7.215 | 166 KB | `id, regency_id, name` |
| `villages.csv` | 80.534 | 2.3 MB | `id, district_id, name` |

**Delimiter:** koma (`,`)  
**Tanpa header** — langsung data dari baris pertama.

## Hubungan Antar Data

```
province.id ──< regencies.province_id
regency.id  ──< districts.regency_id
district.id ──< villages.district_id
```

## Contoh

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

## API

Gunakan [api-datasets-indonesia](https://github.com/prodhokter/api-datasets-indonesia) untuk akses via REST API:

```
GET /api/wilayah/provinces
GET /api/wilayah/regencies/:provinceId
GET /api/wilayah/districts/:regencyId
GET /api/wilayah/villages/:districtId
```

## Sumber

Fork dari [emsifa/api-wilayah-indonesia](https://github.com/emsifa/api-wilayah-indonesia) — data Kemendagri.

## Lisensi

MIT — sesuai lisensi repository asli.
