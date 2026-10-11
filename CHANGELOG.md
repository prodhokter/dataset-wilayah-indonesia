# Changelog

## 2026-10-11 (revisi), Hostname publik dan internal dipisah

- README memakai `https://api.ibnuhabib.web.id` sebagai base URL publik.
- `https://datasets.snbtku.com` adalah hostname internal untuk aplikasi SNBTKU (layanan sama), tidak dipromosikan untuk umum.

## 2026-10-11, Pindah ke Kepmendagri 2025 (38 provinsi)

- Sumber baru: `wilayah-kemendagri-2025.sql` dari [cahyadsn/wilayah](https://github.com/cahyadsn/wilayah) (Kepmendagri No. 300.2.2-2138/2025, MIT).
- Tambah `clean/` berisi CSV bersih: 38 provinsi, 514 kabupaten/kota, 7.285 kecamatan, 83.762 desa/kelurahan (kode tanpa titik, ada header, UTF-8).
- Empat provinsi baru tersedia: Papua Selatan (93), Papua Tengah (94), Papua Pegunungan (95), Papua Barat Daya (96).
- CSV lama (34 provinsi, tanpa pemekaran Papua, dan memuat 2 id desa duplikat) dipindah ke `legacy-34-provinsi/`.
- Tambah `LICENSE-WILAYAH-UPSTREAM.txt` untuk kepatuhan lisensi sumber.
- Dokumentasi API diperbarui: lihat README (API kini di `https://datasets.snbtku.com`, hostname kedua `https://api.ibnuhabib.web.id`).
