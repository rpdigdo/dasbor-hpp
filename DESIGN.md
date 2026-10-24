# DESIGN.md — Dasbor HPP Makanan & Minuman

Dokumen arah desain. Versi tema **Fun Cooking**, dikunci 2026-10-24 lewat grill arah Q1–Q7 (semua disetujui pemilik; Q3 dan Q4 mengikuti rekomendasi). Menggantikan versi kalem retrospektif di hari yang sama. Edit tampilan berikutnya mengacu ke dokumen ini. Fungsi, rumus, dan struktur dasbor tidak berubah oleh tema ini.

## Identity

Kalkulator modal (HPP) untuk satu pengguna nyata: istri pemilik, yang membuat makanan dan minuman untuk dijual dan menghitung modalnya dari HP. Semua bahan, harga, satuan, dan konversi diinput sendiri oleh pengguna; dasbor hanya menghitung dan memberi insight dari input itu. Temanya dapur rumahan yang ceria, bukan aplikasi finansial korporat dan bukan template SaaS.

## Personality

Fun cooking: ceria, hangat, dan mengundang untuk memasak, tapi tetap alat kerja yang jelas saat dipakai sambil masak. Bahasa Indonesia sederhana sehari-hari, tanpa istilah teknis dan tanpa jargon bisnis. Keceriaan datang dari warna, ikon masak, huruf judul yang bulat, dan sudut yang lembut, bukan dari dekorasi menumpuk.

## Palette

Basis krem hangat dipertahankan. Semua nilai di bawah sudah dihitung kontras WCAG sebelum dikunci; pasangan teks dan latar wajib AA (teks normal minimal 4,5:1) di kedua mode.

Mode terang:

- Latar krem `#FAF5EF`, permukaan putih `#FFFFFF`, permukaan kedua `#FBEFE2`
- Tinta cokelat tua `#2C211A`, teks redup `#7D6C5D`, garis `#F0DFC8`
- Aksen utama **oranye tomat** `#C2410C` (teks putih di atasnya 5,18:1; sebagai teks di atas krem 4,78:1)
- Aksen kedua **kuning telur** `#F2B705`, hanya untuk stiker dan sorotan kecil, selalu dengan teks tinta gelap di atasnya (8,62:1). Tidak pernah untuk teks kecil di atas latar terang.
- Latar lembut aksen: tomat `#FBE3D3`, kuning `#FBF0CD`
- Varian teks di atas latar lembut (disetujui pemilik 2026-10-24 setelah audit kontras): label redup di atas latar krem kedua memakai `#79654F` (4,90:1); teks chip kategori Makanan di atas oranye lembut memakai `#B03A0E` (4,93:1). Aksen utama sendiri tidak berubah.

Warna semantik (pemetaan disengaja, menjadi sistem):

- Hijau daun `#2A7347`: hasil baik, untung, status aman (4,90:1 di atas latar lembutnya)
- Amber `#85600E`: peringatan ringan
- Danger `#B3352B`: hapus, kesalahan, peringatan keras
- Teal `#177083`: kategori minuman; tomat menjadi warna kategori makanan; kuning telur menjadi warna stiker Andalan

Mode gelap mengikuti `prefers-color-scheme` perangkat: palet yang sama digelapkan, aksen utama menjadi tomat terang `#F2814F` (6,91:1 di atas latar gelap; teks tinta gelap di atasnya 6,81:1). Bukan tema terpisah yang berbeda rasa.

Dilarang: ungu, biru dingin, neon, gradien, glassmorphism, glow.

## Typography

- Judul, nama menu besar, dan angka ringkasan utama: **Fredoka** (bulat, ceria, tetap terbaca), bobot 500–600.
- Semua teks isi, label, dan input: **Plus Jakarta Sans** seperti sebelumnya (terbukti terbaca di HP), fallback system-ui.
- Angka di tabel hitungan tetap monospace agar sejajar.
- Tidak ada huruf kapital berjarak lebar, tidak ada gaya terminal, teks UI tidak memakai em dash.

## Ikon dan ilustrasi

- Satu set **ikon SVG gambar tangan sederhana bertema masak**, digambar inline (tanpa file gambar eksternal, tanpa emoji): topi koki, panci, sendok-garpu, wajan, telur, cabai, kue, gelas, timbangan, keranjang belanja, kalkulator, koin.
- Ikon hanya dipakai fungsional: penanda kategori makanan/minuman di kartu, ikon tab dan navigasi, penanda bagian di Insight dan Belanja, dan pendamping state kosong. Ikon generik non-masak (sparkle, bintang ajaib, petir, robot) dilarang.
- Ilustrasi spot kecil hanya di tiga titik: pita header (satu ilustrasi panci bertopi koki), state kosong daftar menu, dan halaman Panduan (ikon per langkah boleh, bukan ilustrasi besar baru). Tanpa foto stok.
- Motif identitas: pola kotak kain dapur (gingham) **sangat tipis** hanya di pita header. Tidak di badan halaman, tidak di kartu.

## Bentuk dan gerak

- Sudut lebih bulat: kartu 18px, tombol 14–16px, modal 20px. Chip saringan tetap pill karena fungsinya toggle.
- Label fungsional seperti Andalan tampil sebagai stiker kecil kuning telur dengan teks gelap, sedikit miring boleh pada stiker saja.
- Bayangan lembut hangat hanya untuk elevasi kartu dan tombol melayang.
- Gerak: transisi halus 150–250ms untuk buka-tutup modal, ganti tab, dan tekan tombol (efek tekan membal ringan pada tombol utama). Tidak ada animasi dekoratif berulang, tidak ada parallax.

## Dials

Dial: ENERGY 2 / RHYTHM 2 / MOTION 2

Alasannya: tema fun cooking menaikkan energi dari versi kalem (1/1/1), tapi dasbor ini tetap alat kerja harian. Ritme 2 berarti komposisi sebagian besar konsisten dengan beberapa pemecah pola yang disengaja (pita header bermotif, stiker Andalan, ilustrasi state kosong). Gerak 2 berarti transisi membantu orientasi, bukan pertunjukan.

## Struktur (terkunci, tidak berubah oleh tema)

- Daftar dan detail terpisah: daftar hanya kartu ringkas, tap kartu membuka detail layar penuh 3 tab (Hitungan | Insight & Harga | Belanja & Simulasi).
- Navigasi bawah 3 tujuan nyata: Menu | Kalkulator | Lainnya, disembunyikan saat detail terbuka.
- Cari, saringan (Semua / Makanan / Minuman / ★ Andalan), dan urutan menempel di atas daftar; tombol + Menu melayang.
- Satu tabel per menu untuk semua baris biaya (bahan, kemasan, biaya lain termasuk gas/listrik Rp per batch).
- Target tap minimum 44px. Modal bisa ditutup dengan tombol Escape. State kosong selalu ada dan bersahabat.

## Batasan yang disadari

Data tinggal di penyimpanan lokal browser pengguna (localStorage), jadi Backup (unduh file, bagikan, salin teks) dan Pulihkan (dari file, dari teks) adalah bagian dari desain. Hosting statis di GitHub Pages; halaman tidak boleh dibingkai agar unduhan file bekerja di HP. Ikon dan ilustrasi inline menjaga halaman tetap satu file mandiri.
