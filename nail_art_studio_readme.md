# 💅 Nail Art Studio - Database System Management

[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Database System](https://img.shields.io/badge/Database-System-blue?style=for-the-badge)](#)

Repository ini berisi skema perancangan *Relational Database* lengkap untuk mendukung kegiatan operasional dan manajemen **Studio Nail Art**. Proyek ini merupakan pemenuhan tugas akhir/praktikum untuk mata kuliah *Database System* oleh **Kelompok 5**.

---

## 📖 Deskripsi Singkat

Sistem database ini dirancang khusus untuk mendigitalisasi alur kerja di sebuah studio kecantikan kuku (Nail Art). Struktur data telah dinormalisasi hingga tahap 3NF (*Third Normal Form*) untuk memastikan integritas data, menghindari redundansi, dan mengoptimalkan performa. Sistem mencakup pengelolaan reservasi pelanggan, manajemen harga dinamis (seperti penambahan aksesoris/charm), program loyalitas (poin & diskon ulang tahun), hingga pemantauan stok inventaris bahan baku.

## ✨ Fitur Utama (Berdasarkan *Business Rules*)

Sistem database ini merepresentasikan logika bisnis nyata dari hasil wawancara dengan pemilik usaha, yang diterjemahkan langsung ke dalam *Data Definition Language* (DDL):

* **Manajemen Reservasi & Layanan:** Mendukung pencatatan *booking* multi-layanan (Kuku Asli maupun *Soft Tip Extension*) lengkap dengan status dan metode pembayaran.
* **Kalkulator Garansi Otomatis (View):** Sistem dilengkapi dengan sebuah *View* (`view_garansi_pelanggan`) yang secara otomatis menghitung dan memantau tenggat waktu klaim garansi 7 hari setelah tanggal pengerjaan kuku.
* **Sistem Peringatan Stok (*Inventory Alert*):** Memiliki *Computed Column* pada tabel bahan baku yang otomatis mengubah status menjadi `"Perlu Restock"` saat jumlah barang menyentuh batas minimum.
* **Sistem Penetapan Harga yang Fleksibel:** Mengakomodasi *price list* berupa rentang (harga minimal-maksimal), namun tetap mencatat *deal* harga statis pada nota akhir pelanggan, ditambah kalkulasi *add-on* (seperti charm 3D).
* **Loyalty & Retention Program:** Merekam penggunaan fasilitas *member* seperti tukar poin loyalitas dan klaim diskon ulang tahun pelanggan untuk keperluan audit.

## 🗄️ Daftar Tabel Utama

Sistem ini dibangun atas **8 Tabel Utama** dan **1 View**, yaitu:

1. `pelanggan` : Menyimpan data diri, kontak, dan riwayat klinis/alergi pelanggan.
2. `layanan` : Menyimpan *master data* daftar harga dan estimasi durasi dari layanan dasar.
3. `kategori_desain` : Menyimpan variasi seni kuku (Polos, Cat Eye, Floral, dll) beserta klasifikasi tingkat kesulitannya.
4. `booking` : Entitas pusat untuk mencatat informasi transaksi, lokasi *home service*, dan status pelunasan.
5. `detail_booking_layanan` : Entitas Asosiatif (M:N) yang merinci layanan apa saja dan desain mana yang diambil pada suatu nota/booking.
6. `bahan_baku` : Menyimpan katalog bahan (kuteks, aseton, lem) beserta parameter minimum stok.
7. `transaksi_bahan` : Log harian riwayat keluar-masuk (pemakaian & *restock*) dari inventaris.
8. `ulasan` : Menyimpan data *feedback*, rating 1-5, dan otorisasi publikasi media sosial dari pelanggan.

* **View Tambahan:** `view_garansi_pelanggan`

## 🛠️ Prasyarat (Prerequisites)

Untuk dapat menjalankan atau memodifikasi *script* dari proyek ini, Anda memerlukan:
* **PostgreSQL** (versi 12.0 ke atas direkomendasikan).
* **pgAdmin 4** atau *Command Line Tool* `psql` (untuk antarmuka manajemen database).
* **Git** (opsional, jika ingin melakukan modifikasi *version control*).

## 🚀 Cara Penggunaan (Install/Setup)

Ikuti instruksi berikut untuk menjalankan skema database di sistem lokal Anda:

1. **Clone Repository**
   Buka terminal/Git Bash dan jalankan:
   ```bash
   git clone https://github.com/USERNAME/File-Project-Database-System---Nail-Art.git
   cd File-Project-Database-System---Nail-Art
   ```

2. **Siapkan Database Environment**
   Buka pgAdmin atau `psql`, lalu buat wadah database baru:
   ```sql
   CREATE DATABASE studio_nail_art;
   ```

3. **Eksekusi Skema Database**
   * Pastikan Anda sudah terhubung (berada di dalam) database `studio_nail_art`.
   * Buka file `Project_Database_NailArt.sql` dari repositori ini.
   * Jalankan (*Execute*) seluruh isi file tersebut secara berurutan. *Script* telah diatur berdasarkan hierarki referensi *Foreign Key* agar tidak terjadi *error dependency*.

## 👥 Kredit

Proyek Database ini disusun dan dikembangkan oleh **Kelompok 5**:

* **[Nama Lengkap Anda]** - [NIM/ID Mahasiswa]
* **[Nama Teman 1]** - [NIM/ID Mahasiswa]
* **[Nama Teman 2]** - [NIM/ID Mahasiswa]
* **[Nama Teman 3]** - [NIM/ID Mahasiswa]

*Dibuat dengan 💻 dan ☕ untuk evaluasi mata kuliah Database System.*