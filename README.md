# DOKUMENTASI PEMELIHARAAN PERANGKAT LUNAK: SISTEM INFORMASI PERPUSTAKAAN

**Nama Aplikasi:** `perpustakaan-main`  
**Versi:** 1.1.0  
**Repository/URL:** [https://github.com/ivan42118/perpustakaan.git](https://github.com/ivan42118/perpustakaan.git)  
**Nama Penyusun:** Muhammad Alwan Azmi  
**Tanggal Pembuatan:** 21/06/2025  

---

### 1. Deskripsi Umum Aplikasi

Aplikasi yang menjadi objek analisis adalah sebuah Sistem Informasi Perpustakaan yang dirancang sebagai solusi digital komprehensif untuk operasional perpustakaan. Proyek ini bersifat *open-source*, dibangun menggunakan basis teknologi PHP native yang tidak bergantung pada framework modern. Hal ini menjadikannya studi kasus yang relevan untuk analisis pemeliharaan perangkat lunak, khususnya untuk sistem warisan (*legacy system*). Target pengguna utama dari aplikasi ini adalah perpustakaan skala kecil hingga menengah yang memerlukan sistem manajemen yang efisien namun mudah diimplementasikan.

Sistem ini menyediakan serangkaian fungsionalitas yang terstruktur dengan baik, mencakup:
* **Manajemen Data Inti (Master Data):** Kemampuan untuk mengelola data fundamental perpustakaan, meliputi data anggota (dengan fitur tambah, edit, hapus, dan cetak kartu), data buku (manajemen koleksi), serta data pengguna sistem (admin dan petugas).
* **Manajemen Sirkulasi:** Fitur ini menangani alur peminjaman dan pengembalian buku. Ini termasuk pencatatan transaksi peminjaman, proses pengembalian yang terintegrasi dengan kalkulasi denda otomatis jika terjadi keterlambatan, dan opsi untuk perpanjangan masa peminjaman.
* **Sistem Pelaporan:** Aplikasi mampu menghasilkan laporan-laporan terperinci yang esensial untuk audit dan evaluasi kinerja perpustakaan, seperti rekapitulasi data anggota, data buku, dan seluruh riwayat transaksi sirkulasi.
* **Sistem Autentikasi:** Terdapat mekanisme login yang membedakan level pengguna antara Admin (hak akses penuh) dan Petugas (hak akses operasional terbatas).

### 2. Persyaratan Aplikasi

Untuk menjamin aplikasi dapat beroperasi dengan lancar, stabil, dan memberikan performa yang diharapkan, lingkungan instalasi harus memenuhi beberapa kriteria teknis dari sisi perangkat keras dan perangkat lunak.

* **Kebutuhan Perangkat Keras (Hardware):**
    * **Komputer/Server:** Diperlukan sebuah unit komputer yang akan difungsikan sebagai server dengan kapasitas memori (RAM) paling sedikit 2 GB. Spesifikasi ini krusial untuk menangani beban kerja dari Apache, proses PHP, dan layanan database secara simultan.
    * **Penyimpanan (Storage):** Ruang kosong pada disk minimal 500 MB. Alokasi ini dibutuhkan untuk menampung file-file kode sumber, direktori aset, serta pertumbuhan data di dalam database seiring waktu penggunaan.

* **Kebutuhan Perangkat Lunak (Software):**
    * **Web Server Stack:** Sangat direkomendasikan untuk menggunakan paket **XAMPP Control Panel v3.3.0** karena sudah mencakup seluruh dependensi yang dibutuhkan.
    * **PHP:** Versi PHP yang harus digunakan adalah **versi 8.0.30**. Persyaratan ini bersifat mandatori untuk menghindari masalah kompatibilitas fungsi, terutama mengingat adanya penggunaan fungsi usang di dalam kode.
    * **Database:** Diperlukan server database **MySQL atau MariaDB**, yang merupakan komponen standar dalam paket XAMPP.
    * **Browser:** Aplikasi ini dapat diakses dengan baik melalui peramban web modern seperti Google Chrome, Mozilla Firefox, atau Microsoft Edge.

### 3. Struktur Direktori dan File

Struktur direktori aplikasi ini dirancang secara modular untuk memisahkan antara logika bisnis, aset antarmuka, dan file-file konfigurasi. Pengorganisasian yang jelas seperti ini merupakan praktik yang baik karena sangat memudahkan proses pemeliharaan, pelacakan bug, dan pengembangan fitur di kemudian hari.

-   `admin/`: Direktori utama yang menampung semua file logika dan antarmuka untuk halaman admin.
    -   `agt/`: Modul spesifik untuk manajemen Anggota (tambah, edit, hapus, cetak).
    -   `buku/`: Modul untuk manajemen Buku.
    -   `laporan/`: Modul untuk menghasilkan berbagai jenis laporan.
    -   `log/`: Modul untuk melihat riwayat sirkulasi (peminjaman dan pengembalian).
    -   `pengguna/`: Modul untuk manajemen pengguna sistem.
    -   `sirkul/`: Modul inti yang menangani transaksi sirkulasi.
-   `assets/` & `assets_style/`: Berisi semua aset frontend, seperti file CSS, JavaScript, dan berbagai library pihak ketiga yang memperkaya tampilan.
-   `bootstrap/`: Menyimpan file-file dari framework CSS Bootstrap.
-   `inc/`: Berisi file-file inklusi penting, terutama `koneksi.php` yang mengatur hubungan ke database.
-   `home/`: Berisi file halaman dashboard atau beranda untuk pengguna yang telah login.
-   `plugins/`: Menyimpan berbagai plugin jQuery tambahan seperti DataTables dan Select2.
-   `data_perpus.sql`: File krusial berisi skema dan data awal database untuk proses instalasi.
-   `index.php`, `login.php`, `logout.php`: File-file utama yang mengatur alur autentikasi dan halaman awal aplikasi.

### 4. Instruksi Instalasi dan Konfigurasi

Berikut adalah panduan langkah demi langkah untuk melakukan instalasi dan konfigurasi aplikasi pada lingkungan pengembangan lokal menggunakan XAMPP.

1.  **Salin Proyek ke Direktori Server:** Salin seluruh folder proyek `perpustakaan-main` ke dalam direktori `C:\xampp\htdocs\`.
2.  **Buat Database:** Akses phpMyAdmin melalui browser (`http://localhost/phpmyadmin`) dan buat sebuah database baru dengan nama `data_perpus`.
3.  **Impor Database:** Pilih database `data_perpus` yang baru saja Anda buat. Masuk ke tab "Import", klik "Choose File" dan pilih file `data_perpus.sql` yang ada di dalam folder proyek. Klik tombol "Go" atau "Kirim" untuk memulai proses impor.
4.  **Verifikasi Konfigurasi:** File `inc/koneksi.php` sudah secara otomatis terkonfigurasi untuk terhubung dengan database `data_perpus`. Tidak ada perubahan kode yang diperlukan.
    ```php
    <?php
    $koneksi = new mysqli ("localhost","root","","data_perpus");
    ?>
    ```
5.  **Akses Aplikasi:** Buka browser dan navigasikan ke alamat `http://localhost/perpustakaan-main`. Halaman login akan muncul, dan Anda dapat masuk menggunakan kredensial default: `admin / 123`.

### 5. Dependency yang Digunakan

Aplikasi ini memanfaatkan sejumlah library dan package eksternal untuk memperkaya fungsionalitas dan pengalaman pengguna, terutama di sisi frontend.

* **AdminLTE v2.4.18:** Template utama untuk dasbor administrasi.
* **Bootstrap v3.3.7:** Framework CSS untuk desain antarmuka yang responsif.
* **jQuery v2.2.3:** Pustaka JavaScript yang menjadi dasar untuk manipulasi DOM dan interaktivitas.
* **jQuery UI:** Menyediakan komponen antarmuka tambahan seperti kalender.
* **DataTables:** Plugin jQuery untuk membuat tabel data yang interaktif dengan fitur pencarian, sortir, dan paginasi.
* **Select2:** Plugin untuk mengubah dropdown standar menjadi lebih fungsional dengan fitur pencarian.
* **Font Awesome:** Menyediakan set ikon vektor untuk memperindah elemen antarmuka.
* **Morris.js:** Digunakan untuk membuat grafik pada halaman dasbor.
* **PACE:** Menampilkan loading bar otomatis saat halaman dimuat.

### 6. Instruksi Build dan Deployment

* **Proses Build:** Aplikasi ini berbasis PHP yang merupakan bahasa *interpreted*, sehingga tidak memerlukan proses build atau kompilasi. File kode dapat langsung dijalankan oleh server.
* **Proses Deployment:** Untuk melakukan deployment ke server hosting online, ikuti langkah-langkah berikut:
    1.  Unggah semua file dan folder dari direktori proyek ke server hosting (biasanya ke dalam folder `public_html`).
    2.  Buat database baru di server hosting melalui panel kontrol (misalnya cPanel).
    3.  Impor file `data_perpus.sql` ke dalam database yang baru dibuat tersebut.
    4.  Sesuaikan file konfigurasi `inc/koneksi.php` dengan detail host, nama database, user, dan password yang diberikan oleh penyedia hosting.
    5.  Aplikasi siap untuk diakses melalui domain Anda.

### 7. Panduan Debugging dan Logging

Karena tidak adanya framework logging formal, proses debugging dan pelacakan kesalahan pada aplikasi ini dilakukan dengan pendekatan sebagai berikut:

* **Debugging Manual:** Cara paling langsung adalah dengan menyisipkan fungsi-fungsi bawaan PHP seperti `echo()`, `print_r()`, dan `var_dump()` pada baris kode yang dicurigai bermasalah untuk memeriksa nilai variabel.
* **Log Error Server:** Sumber informasi utama untuk kesalahan fatal adalah file log error Apache. Pada instalasi XAMPP, file ini dapat ditemukan di `C:\xampp\apache\logs\error.log`. Memantau file ini sangat penting saat aplikasi menunjukkan halaman putih atau error 500.
* **Error Database:** File `inc/koneksi.php` akan menghentikan eksekusi skrip jika koneksi gagal. Untuk men-debug query yang salah, Anda dapat menambahkan `or die(mysqli_error($koneksi))` setelah fungsi `mysqli_query()` untuk menampilkan pesan kesalahan dari MySQL.

### 8. Change Log

Berikut adalah rekonstruksi catatan perubahan (*change log*) berdasarkan template soal dan analisis file.

* **Versi 1.0.0, 2025-06-09:** Rilis awal.
* **Versi 1.1.0, 2025-06-15:** Tambah fitur simpan data (CRUD untuk Anggota, Buku, Sirkulasi).
* **Versi 1.1.0, 2025-06-21:** Pembuatan ulang dokumentasi pemeliharaan.

### 9. Bug Dikenal

Analisis kode sumber telah mengidentifikasi beberapa masalah dan bug yang signifikan. Isu-isu ini memerlukan perhatian khusus pada siklus pemeliharaan berikutnya.

* **ID Bug: 001**
    * **Deskripsi:** Penggunaan Fungsi Database Usang. Kode masih mengandung fungsi `mysql_*` yang telah usang (contoh: `mysql_connect`) di beberapa bagian kode. Fungsi-fungsi ini telah dihapus sepenuhnya di PHP 7 ke atas dan akan menyebabkan *Fatal Error* pada environment PHP 8.0.30 yang disyaratkan.
    * **Prioritas:** Tinggi.
    * **Status:** Belum Diperbaiki.
    * **Rekomendasi:** Refaktorisasi seluruh kode untuk menggunakan ekstensi MySQLi secara konsisten.

* **ID Bug: 002**
    * **Deskripsi:** Kerentanan SQL Injection. Aplikasi tidak menggunakan *prepared statements* untuk *query* database. Hal ini membuka celah keamanan yang sangat serius terhadap serangan SQL Injection, di mana penyerang dapat memanipulasi *input* untuk mengeksekusi perintah SQL berbahaya.
    * **Prioritas:** Tinggi.
    * **Status:** Belum Diperbaiki.
    * **Rekomendasi:** Implementasikan *prepared statements* pada semua *query* yang menerima *input* dari pengguna untuk menutup celah keamanan ini.

* **ID Bug: 003**
    * **Deskripsi:** Validasi Input Tidak Lengkap. Validasi input hanya terjadi di sisi klien (JavaScript) dan tidak ada di sisi server, sehingga rentan jika JavaScript dinonaktifkan.
    * **Prioritas:** Sedang.
    * **Status:** Belum Diperbaiki.
    * **Rekomendasi:** Tambahkan validasi di sisi server (PHP) untuk setiap data yang dikirim dari formulir sebelum disimpan ke database.
