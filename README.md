# Klinik Demo Sejahtera — Situs Demo Personal Agent Protocol (Poppy) 1.0

Situs klinik fiktif di Bandung untuk latihan AI engineering: agen pribadi bisa menemukan klinik ini lewat Personal Agent Protocol (Poppy) 1.0, lalu membuat janji temu demo dan simulasi pembayaran.

**DEMO — Semua data di sini fiktif.** Tidak ada klinik sungguhan, pasien sungguhan, atau pembayaran sungguhan.

## Situs live

- Beranda demo: https://xien63.github.io/
- Dokumen discovery: https://xien63.github.io/.well-known/poppy.json
- Halaman agen: https://xien63.github.io/agen.html
- Deskripsi API demo: https://xien63.github.io/openapi.json

## Yang nyata dan yang simulasi

Nyata: `poppy.json` (1.0), metadata OAuth (`oauth/.well-known/oauth-authorization-server`), metadata protected resource (`/.well-known/oauth-protected-resource`), deskripsi OpenAPI, dan halaman-halaman situs.

Simulasi: sign-in (tidak ada server OAuth sungguhan), sesi dan token (tidak diterbitkan), pembuatan janji (hanya di browser), pembayaran (tidak ada).

## File penting

| File | Isi |
| --- | --- |
| `index.html` | Beranda demo: layanan, dokter, formulir janji demo |
| `agen.html` | Penjelasan untuk agen AI: alur discovery sampai pembayaran demo |
| `.well-known/poppy.json` | Dokumen discovery Poppy 1.0 |
| `.well-known/oauth-protected-resource` | Metadata protected resource (RFC 9728): resource, authorization_servers, scopes_supported |
| `oauth/.well-known/oauth-authorization-server` | Metadata OAuth (RFC 8414) + `protected_resources` (1.0, menggantikan `poppy_domains` dari draft 0.1) |
| `openapi.json` | Deskripsi OpenAPI untuk API demo (belum ada server live) |
| `oauth/*/index.html`, `poppy/browser-session/index.html` | Halaman penjelas untuk endpoint demo |
| `.nojekyll` | Menonaktifkan Jekyll agar folder `.well-known` ikut terbit di GitHub Pages |

## Validasi

Dokumen discovery divalidasi dua cara:

1. PAP Checker (papchecker.com) — pemeriksa independen dari luar, dengan cara yang sama seperti agen pribadi. Untuk 1.0 ia memakai read-only checks dari validator resmi protokol.
2. Pemeriksaan dokumen manual terhadap aturan 1.0 bagian 3 (discovery), 3.2 (issuer dan protected resource), dan 4.7 (scope dan scope_hints).

SDK Python Datalayer terbaru (0.32.0) masih mengikuti draft 0.4, jadi tidak dipakai untuk validasi 1.0.

Hasil validasi tercatat di panduan pembangunan (PDF).

## Catatan versi

Demo ini mengikuti **Poppy 1.0**, terbit dan beku 14 November 2026 di `/docs/1.0/spec`. Riwayat: draft 0.1 (9 Oktober 2026), 0.2 beku (24 Oktober 2026), 0.3 beku (4 November 2026), 0.4 terbit 10 November 2026 sebagai release candidate.

Yang berubah dari 0.1 ke 1.0 di demo ini: `protocol_version` 1.0; `auth` memakai `scopes` dan `scope_hints` (bagian `direct`, `device`, dan `custom_scopes` dihapus); scope `poppy:read` dan `poppy:write` dihapus (sudah dihapus sejak 0.3) dan diganti scope `appointments` plus `poppy:browser-sign-in` yang wajib karena `browser_session_endpoint` tercantum; metadata issuer memakai `protected_resources` (`poppy_domains` dihapus) plus `grant_types_supported`, `scopes_supported`, dan `token_endpoint_auth_signing_alg_values_supported` ES256 dan PS384; ditambah file metadata protected resource.

Yang tetap perilaku server dan tidak bisa didemokan di static hosting: penegakan PS384 dan PAR, `prompt=consent` dan halaman consent, token dan sesi sungguhan, serta API live. Itu latihan lanjutan di panduan pembangunan.

## Lisensi

Kode demo ini bebas dipakai untuk latihan. Spesifikasi Personal Agent Protocol berlisensi Apache 2.0.
