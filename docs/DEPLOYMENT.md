# Deployment Production

## URL
- Website: https://laravel-online-sales-zeta.vercel.app
- API: https://laravel-online-sales-zeta.vercel.app/api/v1

## Arsitektur
- Kode: GitHub (branch main)
- Aplikasi: Vercel Hobby, Container Runtime (Dockerfile.vercel + FrankenPHP)
- Database: MySQL Railway melalui TCP Proxy publik

## Environment variable production
Diatur di Vercel Dashboard > Settings > Environment Variables.
Nilai rahasia (APP_KEY, DB_PASSWORD) tidak disimpan di repository.

APP_NAME, APP_ENV=production, APP_KEY, APP_DEBUG=false, APP_URL,
LOG_CHANNEL=stderr, LOG_LEVEL=warning,
DB_CONNECTION=mysql, DB_HOST, DB_PORT, DB_DATABASE, DB_USERNAME, DB_PASSWORD,
SESSION_DRIVER=database, CACHE_STORE=database, QUEUE_CONNECTION=sync,
FILESYSTEM_DISK=local

## Catatan
- Container Vercel stateless: session dan cache memakai database.
- Upload gambar produk tidak persisten di production (lihat modul 6.9).
- Migration ke Railway dijalankan dari komputer lokal dengan environment variable sementara.
- Deploy ulang otomatis setiap ada push ke branch main.