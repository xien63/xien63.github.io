# Klinik Demo Sejahtera — Situs Demo Personal Agent Protocol (Poppy) Draft 0.1

Situs klinik fiktif di Bandung untuk latihan AI engineering: agen pribadi bisa menemukan klinik ini lewat Personal Agent Protocol (Poppy) draft 0.1, lalu membuat janji temu demo dan simulasi pembayaran.

**DEMO — Semua data di sini fiktif.** Tidak ada klinik sungguhan, pasien sungguhan, atau pembayaran sungguhan.

## Situs live

- Beranda demo: https://xien63.github.io/
- Dokumen discovery: https://xien63.github.io/.well-known/poppy.json
- Halaman agen: https://xien63.github.io/agen.html
- Deskripsi API demo: https://xien63.github.io/openapi.json

## Yang nyata dan yang simulasi

Nyata: `poppy.json` (draft 0.1), metadata OAuth (`oauth/.well-known/oauth-authorization-server`), deskripsi OpenAPI, dan halaman-halaman situs.

Simulasi: sign-in (tidak ada server OAuth sungguhan), sesi dan token (tidak diterbitkan), pembuatan janji (hanya di browser), pembayaran (tidak ada).

## File penting

| File | Isi |
| --- | --- |
| `index.html` | Beranda demo: layanan, dokter, formulir janji demo |
| `agen.html` | Penjelasan untuk agen AI: alur discovery sampai pembayaran demo |
| `.well-known/poppy.json` | Dokumen discovery Poppy draft 0.1 |
| `oauth/.well-known/oauth-authorization-server` | Metadata OAuth (RFC 8414) + `poppy_domains` |
| `openapi.json` | Deskripsi OpenAPI untuk API demo (belum ada server live) |
| `oauth/*/index.html`, `poppy/browser-session/index.html` | Halaman penjelas untuk endpoint demo |
| `.nojekyll` | Menonaktifkan Jekyll agar folder `.well-known` ikut terbit di GitHub Pages |

## Validasi

Dokumen discovery divalidasi dua cara:

1. SDK Python draft 0.1 (`personal-agent-protocol` dari PyPI, Datalayer) — discovery client memeriksa `protocol_version`, `organization.domain`, issuer, dan `poppy_domains`.
2. PAP Checker (papchecker.com) — pemeriksa independen dari luar, dengan cara yang sama seperti agen pribadi.

Hasil validasi tercatat di panduan pembangunan (PDF).

## Catatan versi

Demo ini mengikuti **draft 0.1** persis seperti yang diterbitkan 9 Oktober 2026. Draft 0.1 sudah beku, tetapi 0.2 juga sudah beku (24 Oktober 2026), 0.3 sudah beku (4 November 2026), dan draft 0.4 sedang berjalan. Bagian yang harus ditinjau ulang saat naik versi tercantum di panduan pembangunan.

## Lisensi

Kode demo ini bebas dipakai untuk latihan. Spesifikasi Personal Agent Protocol berlisensi Apache 2.0.
