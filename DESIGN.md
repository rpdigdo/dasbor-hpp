# DESIGN.md — Dasbor HPP Makanan & Minuman

Dokumen arah desain. Ditulis retrospektif pada 2026-10-24 dari keputusan yang sudah terkunci selama pembangunan (grill Q1–Q12 spek v2 dan grill daftar-detail Q1–Q13), sebagai penutup temuan R-37 audit antislop 001. Mulai sekarang dokumen ini adalah arah tertulis dasbor: edit berikutnya mengacu ke sini.

## Identity

Kalkulator modal (HPP) untuk satu pengguna nyata: istri pemilik, yang membuat makanan dan minuman untuk dijual dan menghitung modalnya dari HP. Bukan aplikasi finansial korporat dan bukan template SaaS. Semua bahan, harga, satuan, dan konversi diinput sendiri oleh pengguna; dasbor hanya menghitung dan memberi insight dari input itu.

## Personality

Hangat, praktis, dan jelas. Bahasa Indonesia sederhana yang dipakai sehari-hari di dapur dan warung, tanpa istilah teknis dan tanpa jargon bisnis. Kalimat kesalahan dan petunjuk harus bisa dipahami sekali baca.

## Palette

Palet hangat bernuansa dapur dan kertas resep:

- Latar krem `#FAF5EF`, permukaan putih `#FFFFFF`, permukaan kedua `#F4EDE3`
- Tinta cokelat tua `#2C211A`, teks redup `#7D6C5D`, garis `#E9DCCB`
- Aksen utama terracotta `#BC4B1D` (tombol aksi utama, harga, penekanan)

Warna semantik (pemetaan ini disengaja dan menjadi sistem, bukan dekorasi):

- Hijau `#2A7347`: hasil baik, untung, status aman
- Amber `#85600E`: peringatan ringan, perhatian
- Danger `#B3352B`: hapus, kesalahan, peringatan keras
- Teal `#177083` dan plum `#6D4C7D`: pembeda kategori (minuman / makanan dan penanda sekunder), bukan aksen umum

Mode gelap mengikuti `prefers-color-scheme` perangkat dengan palet hangat yang sama digelapkan, bukan tema terpisah. Semua pasangan teks dan latar wajib lolos kontras WCAG AA (teks normal minimal 4,5:1) di kedua mode.

## Typography

Plus Jakarta Sans untuk semua teks (typeface karya desainer Indonesia, karakter ramah dan terbaca jelas di layar HP), dengan fallback system-ui. Angka memakai monospace hanya di tempat angka harus sejajar dan dibandingkan (tabel hitungan dan ringkasan). Tidak ada huruf kapital berjarak lebar dan tidak ada gaya terminal.

## Mood

Seperti buku catatan resep yang rapi: tenang, kertas hangat, satu warna aksen yang muncul di momen penting saja. Tanpa gradien, tanpa glassmorphism, tanpa glow, tanpa dekorasi yang tidak melayani hitungan.

## Dials

Dial: ENERGY 1 / RHYTHM 1 / MOTION 1

Alasannya: ini alat kerja harian yang dipakai sambil memasak. Ketenangan dan keterdugaan mengalahkan ekspresi. Setiap layar punya satu titik fokus (di daftar: daftar menu; di detail: tabel hitungan menu itu). Gerakan dibatasi pada transisi seperlunya; tidak ada animasi dekoratif.

## Struktur (terkunci)

- Daftar dan detail terpisah: daftar hanya kartu ringkas (nama, jenis, modal per porsi, harga jual, untung), tap kartu membuka detail layar penuh.
- Detail satu menu punya 3 tab: Hitungan | Insight & Harga | Belanja & Simulasi.
- Navigasi bawah hanya 3 tujuan nyata: Menu | Kalkulator | Lainnya, dan disembunyikan saat detail terbuka.
- Cari, saringan (Semua / Makanan / Minuman / ★ Andalan), dan urutan menempel di atas daftar; tombol + Menu melayang.
- Satu tabel per menu untuk semua baris biaya: bahan, kemasan, dan biaya lain (gas/listrik sebagai Rp per batch) hidup di tabel yang sama.
- Target tap minimum 44px. Modal harus bisa ditutup dengan tombol Escape di perangkat berkibor.
- Teks UI tidak memakai em dash; gunakan koma, titik, titik dua, atau tanda kurung.

## Batasan yang disadari

Data tinggal di penyimpanan lokal browser pengguna (localStorage), jadi Backup (unduh file, bagikan, salin teks) dan Pulihkan (dari file, dari teks) adalah bagian dari desain, bukan fitur tambahan. Hosting statis di GitHub Pages; halaman tidak boleh dibingkai agar unduhan file bekerja di HP.
