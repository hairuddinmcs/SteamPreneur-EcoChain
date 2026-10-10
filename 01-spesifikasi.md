# Spesifikasi Produk

**Nama tim:** [isi nama tim]
**Nama produk:** EcoChain
**Alur inti yang dibangun:** Admin pengiriman mencatat berat, tujuan, dan moda transportasi satu pesanan, melihat estimasi emisi karbon pesanan itu secara langsung, lalu mengunduh rekap emisi bulanan untuk mitra bisnis.

## 1. Masalah

Admin pengiriman di usaha ekspedisi skala menengah masih mencatat berat muatan, rute, dan moda transportasi secara manual. Alurnya: pesanan masuk lewat WhatsApp, dicatat di buku, lalu dipindah ke Excel pada sore hari. Penimbangan dilakukan dengan timbangan gudang dan dicatat terpisah dari dokumen pesanan. Dua staf menangani sekitar 40 sampai 60 pesanan per hari.

Akibatnya:

- Berat barang sering salah catat atau terlewat saat pesanan ramai, dan tidak ada pengecekan ulang otomatis.
- Moda transportasi belum tercatat secara konsisten.
- Emisi karbon per pengiriman tidak bisa dihitung otomatis. Perhitungan yang ada hanya estimasi kasar tahunan, sehingga tidak bisa ditelusuri ke pengiriman tertentu.
- Salah satu narasumber menyebut mitra korporat mulai meminta laporan emisi karbon (Scope 3) sebagai syarat kerja sama. Narasumber lain belum menerima permintaan langsung.

Masalah utamanya bukan kemauan beralih ke sistem digital, tetapi tidak adanya alat yang cukup sederhana untuk dipakai di tengah kesibukan harian dan tetap menghasilkan data yang bisa diaudit pihak luar.

## 2. Pengguna

Pengguna utama adalah admin di usaha ekspedisi skala menengah di Balikpapan.

**Admin pengiriman (persona 1, perkiraan usia 29 tahun).** Mencatat pesanan masuk, berat muatan, dan rute harian. Ingin menyelesaikan pencatatan secepat mungkin agar barang segera dikirim. Membutuhkan cara mencatat yang cepat dan cek ulang otomatis supaya tidak ada berat yang terlewat.

**Admin operasional dan bisnis (persona 2, perkiraan usia 25 tahun).** Menjaga efisiensi biaya sekaligus memenuhi permintaan data emisi dari mitra bisnis. Saat ini mengandalkan rekap manual bulanan dari staf dan jarang sempat memvalidasi akurasinya. Membutuhkan laporan emisi ringkas yang bisa dicek sewaktu-waktu dan dibagikan ke mitra. Terbuka terhadap sistem berlangganan bulanan asalkan harga sebanding dengan penghematan waktu admin.

## 3. Hasil wawancara calon pengguna

Narasumber:
1. Admin pengiriman, usaha ekspedisi di Balikpapan
2. Admin, ekspedisi cabang Balikpapan

Cara wawancara dan tanggal: [isi: langsung / lewat pesan], 6 Oktober 2026. Ditambah observasi langsung di gudang salah satu usaha ekspedisi di Balikpapan pada tanggal yang sama.

| Pertanyaan kami | Jawaban narasumber |
|---|---|
| Bagaimana Ibu mencatat berat, rute, dan moda transportasi saat ini? | Narasumber 1: dicatat manual di buku terlebih dahulu, lalu dipindah ke Excel pada sore hari. |
| Kapan kesalahan pencatatan paling sering terjadi? | Narasumber 1: saat volume pesanan tinggi (jam atau hari sibuk). "Kalau lagi banyak orderan, suka kelewat nulis berat barangnya." |
| Apakah pernah ada yang meminta data emisi karbon? | Narasumber 1: belum pernah ada permintaan langsung ke bagian admin. Narasumber 2: beberapa mitra korporat mulai meminta laporan emisi karbon (Scope 3) sebagai syarat kerja sama. |
| Bagaimana emisi karbon dihitung sekarang? | Narasumber 2: belum ada cara menghitung emisi per pengiriman secara otomatis. Perhitungan masih estimasi kasar tahunan, dan rekap bulanan dikerjakan manual oleh staf. |
| Apa dampaknya jika permintaan laporan emisi makin banyak? | Narasumber 2: "Kalau makin banyak klien besar yang minta laporan emisi, kami bisa keteteran." |
| Apakah terbuka dengan sistem berlangganan? | Narasumber 2: terbuka dengan sistem berlangganan bulanan asalkan harganya sebanding dengan penghematan waktu admin. |

Temuan observasi di gudang:
- Alur pencatatan: WhatsApp pelanggan, dicatat di buku, dipindah ke Excel pada sore hari.
- Penimbangan manual dengan timbangan gudang, dicatat terpisah dari dokumen pesanan.
- Tidak ada sistem digital yang menghubungkan data pesanan, berat, dan rute secara otomatis.
- Suasana kerja sibuk pada siang hari, dua staf menangani sekitar 40 sampai 60 pesanan per hari.

Hasil audit fitur terhadap bukti lapangan:

| Fitur di proposal | Status |
|---|---|
| Dasbor ringkasan dan visualisasi emisi | Terbukti dibutuhkan |
| Mesin kalkulasi emisi otomatis | Terbukti dibutuhkan (bukti terkuat) |
| Modul pencatatan pengiriman | Terbukti, perlu disesuaikan (tambah field moda transportasi) |
| Aplikasi mobile kurir | Perlu validasi lanjutan (kurir belum diwawancara) |

## 4. Fitur wajib (hanya untuk alur inti)

1. **Form Catat Pengiriman.** Admin mengisi referensi pesanan, tujuan (jarak terisi otomatis untuk rute umum, atau diisi manual), berat muatan, dan moda transportasi. Semua kolom wajib diisi dan form memberi pesan kesalahan jika ada yang kosong atau tidak valid.
2. **Cek ulang dan estimasi emisi langsung.** Panel "Yang akan dicatat" menampilkan ringkasan isian dan estimasi emisi (kg CO2e) yang diperbarui saat form diisi, sebelum data dicatat. Setelah dicatat, entri muncul di daftar "Tercatat hari ini".
3. **Laporan Emisi bulanan.** Halaman rekap total emisi, tren harian, dan emisi per moda transportasi, dengan tombol unduh CSV yang bisa dibuka di Excel.
4. **Penanda data belum lengkap.** Pesanan yang moda transportasinya kosong ditandai "Belum dicatat" di tabel pesanan, dan Ringkasan menampilkan jumlahnya.

## 5. Di luar cakupan (tidak dikerjakan dalam challenge ini)

- Aplikasi mobile kurir dan pelacakan real-time. Kebutuhannya belum divalidasi karena kurir belum diwawancara.
- Backend dan database. Skema PostgreSQL/PostGIS dan TimescaleDB sudah dirancang, tetapi belum dihubungkan ke website.
- Penyimpanan permanen. Entri dari form hanya disimpan sementara di browser.
- Login dan pembagian peran pengguna.
- Integrasi sensor IoT dan perhitungan jarak otomatis dari peta. Jarak diambil dari daftar rute umum atau diisi manual.
- Faktor emisi dari sumber resmi. Angka yang dipakai masih ilustratif.
- Laporan dalam format PDF, dan dukungan beberapa cabang.
- Fitur langganan dan pembayaran.

## 6. Aturan bisnis dan perhitungan

- Estimasi emisi (kg CO2e) = berat (kg) ÷ 1.000 × jarak (km) × faktor emisi moda (kg CO2e per ton-km).
- Faktor emisi per moda (angka ilustratif, belum diverifikasi dengan sumber resmi):

  | Moda | Faktor emisi (kg CO2e per ton-km) |
  |---|---|
  | Truk Diesel | 0,107 |
  | Van Listrik | 0,045 |
  | Kapal Kargo | 0,008 |
  | Kargo Udara | 0,602 |
  | Kereta Barang | 0,028 |

- Contoh: 1.850 kg, 122 km, Truk Diesel → 1,85 × 122 × 0,107 = 24,15 kg CO2e.
- Semua kolom form wajib diisi: referensi pesanan, tujuan, berat, dan moda transportasi.
- Berat harus lebih dari 0 kg. Jika tujuan "Lainnya (isi manual)" dipilih, jarak wajib diisi dan harus lebih dari 0 km.
- Jarak rute umum dari Balikpapan (perkiraan, belum diverifikasi): Balikpapan Kota 12 km, Samarinda 122 km, Banjarmasin 310 km, Makassar 410 km, Surabaya 796 km.
- Pesanan tanpa moda transportasi tidak bisa dihitung emisinya dan tidak masuk total laporan.
- Total emisi ditampilkan dalam kg, dan dalam ton jika mencapai 1.000 kg atau lebih.

## 7. Data yang disimpan

| Data | Contoh isi | Disimpan di mana |
|---|---|---|
| Entri pesanan baru dari form (ID, referensi, tujuan, jarak, berat, moda, estimasi emisi, jam catat) | ORD-1001, Bpk. Andi, Samarinda, 122 km, 1850 kg, Truk Diesel, 24,15 kg, 10:42 | Memori browser (state React), hilang saat halaman di-refresh |
| Data contoh pesanan, ringkasan, dan tren emisi | ORD-1011, Samarinda, 1850 kg, Truk Diesel, 24,1 kg | `src/lib/mock-data.ts` |
| Faktor emisi per moda transportasi | Truk Diesel, 0,107 | `src/lib/mock-data.ts` |
| Daftar rute umum dan jaraknya | Samarinda, 122 km | `src/lib/common-routes.ts` |
| Laporan emisi bulanan | Tanggal, total CO2e (kg), jarak (km) | Dibuat di browser saat tombol unduh diklik, disimpan sebagai file CSV di komputer pengguna |

## 8. Kriteria "selesai"

- [ ] Form Catat Pengiriman tidak bisa dikirim jika referensi pesanan, tujuan, berat, atau moda transportasi kosong, dan pesan kesalahan muncul di bawah kolom yang bermasalah.
- [ ] Memilih tujuan "Lainnya (isi manual)" memunculkan kolom jarak yang wajib diisi.
- [ ] Mengisi tujuan Samarinda, berat 1850 kg, dan moda Truk Diesel menampilkan estimasi emisi 24,15 kg CO2e.
- [ ] Panel "Yang akan dicatat" menampilkan isian form saat diketik.
- [ ] Setelah tombol "Catat pengiriman ini" diklik dengan isian valid, entri muncul di "Tercatat hari ini" dan form kembali kosong.
- [ ] Pesanan yang moda transportasinya kosong ditandai "Belum dicatat" pada tabel pesanan.
- [ ] Tombol "Unduh laporan (CSV)" di Laporan Emisi menghasilkan file `laporan-emisi-oktober-2026.csv` berisi satu baris judul dan 15 baris data.
- [ ] Menu "Pelacakan Kurir" tampil nonaktif dengan label "Perlu validasi" dan tidak bisa dibuka.
- [ ] `npm run build` selesai tanpa error.
