# Laravel Penjualan Online

Aplikasi penjualan online dengan dua peran (Admin dan Pelanggan), dibuat untuk
praktikum Pengembangan Aplikasi Web.

- **Nama:** Aneira Najla Mutia
- **NIM:** 109062500062
- **Stack:** Laravel 13.x, PHP 8.3+, MySQL, Blade, Eloquent, Git

## Fitur

**Admin**
- Login dan dashboard ringkasan
- Kelola kategori dan produk (upload gambar)
- Barang masuk dan histori stok (IN/OUT)
- Kelola layanan ekspedisi
- Lihat transaksi, validasi, pembatalan (stok dikembalikan), ubah status

**Pelanggan**
- Registrasi dan login
- Katalog dengan pencarian, filter, urutan, dan pagination
- Detail produk
- Keranjang belanja (session)
- Checkout dengan pilihan ekspedisi
- Riwayat dan detail pesanan

## Aturan Bisnis

- Stok hanya berubah lewat barang masuk, checkout, dan pembatalan.
- Checkout memakai `DB::transaction()` dan `lockForUpdate()` untuk mencegah overselling.
- Harga dan total selalu dihitung ulang oleh server.
- Nama, harga produk, dan ongkir disalin ke order (snapshot).
- Alur status: `pending` → `confirmed` → `processed` → `shipped` → `completed`.
- Pembatalan hanya untuk `pending` dan `confirmed`.

## Instalasi

Prasyarat: PHP 8.3+, Composer, MySQL, Git.

```bash
git clone https://github.com/USERNAME/laravel-online-sales.git
cd laravel-online-sales
composer install
cp .env.example .env
php artisan key:generate
```

Buat database:

```sql
CREATE DATABASE laravel_online_sales CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

Atur koneksi di `.env`:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel_online_sales
DB_USERNAME=root
DB_PASSWORD=
```

Jalankan migrasi, seeder, dan storage link:

```bash
php artisan migrate
php artisan db:seed
php artisan storage:link
php artisan serve
```

Buka `http://127.0.0.1:8000`.

## Akun Latihan

| Peran | Email | Password |
|---|---|---|
| Admin | admin@example.com | Admin12345! |
| Pelanggan | daftar lewat halaman Register | - |

Akun ini hanya untuk praktikum lokal. Jangan dipakai di production.

## Pengujian Manual

| No | Skenario | Hasil yang diharapkan |
|---|---|---|
| 1 | Customer registrasi | Akun tersimpan role=customer dan langsung login |
| 2 | Customer membuka /admin | HTTP 403 |
| 3 | Admin login | Masuk dashboard admin |
| 4 | Admin tambah kategori dan produk | Produk tampil di admin dan katalog jika aktif |
| 5 | Admin upload gambar | Gambar tersimpan di public storage dan tampil di katalog |
| 6 | Admin stock-in 10 unit | Saldo stock +10, movement IN tercatat |
| 7 | Pelanggan filter produk | Hasil sesuai keyword, kategori, harga, stok, sort |
| 8 | Tambah cart melebihi stok | Validasi menolak |
| 9 | Checkout 2 unit | Order pending, stock -2, movement OUT tercatat |
| 10 | Admin confirm | Status confirmed, validator dan waktu tersimpan |
| 11 | Admin cancel pending/confirmed | Status cancelled, stok kembali, movement IN tercatat |
| 12 | Status order | Hanya urutan confirmed → processed → shipped → completed |

## Milestone Git

| Milestone | Fokus | Tag |
|---|---|---|
| M0 | Setup Laravel, database, repository | m0-setup |
| M1 | Autentikasi dan role | m1-auth-role |
| M2 | Kategori dan produk, upload gambar | m2-master-product |
| M3 | Barang masuk, stok, ekspedisi | m3-inventory-shipping |
| M4 | Katalog, detail, filter, pagination | m4-storefront |
| M5 | Session cart | m5-cart |
| M6 | Checkout, order, stok OUT | m6-checkout |
| M7 | Admin transaksi, validasi, cancel, status | m7-order-admin |
| M8 | QA dan dokumentasi | m8-final |
