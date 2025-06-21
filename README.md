# DOKUMENTASI PEMELIHARAAN PERANGKAT LUNAK: SISTEM INFORMASI PERPUSTAKAAN

**Nama Aplikasi:** `perpustakaan-main`  
**Versi:** 1.1.0  
**Repository/URL:** [https://github.com/ivan42118/perpustakaan.git](https://github.com/ivan42118/perpustakaan.git)  
**Nama Penyusun:** Muhammad Alwan Azmi  
**Tanggal Pembuatan:** 21/06/2025  

---

### 1. Deskripsi Umum Aplikasi

[cite_start]Aplikasi yang menjadi objek analisis adalah sebuah Sistem Informasi Perpustakaan yang dirancang sebagai solusi digital komprehensif untuk operasional perpustakaan. [cite_start]Proyek ini bersifat *open-source*, dibangun menggunakan basis teknologi PHP native yang tidak bergantung pada framework modern. [cite_start]Hal ini menjadikannya studi kasus yang relevan untuk analisis pemeliharaan perangkat lunak, khususnya untuk sistem warisan (*legacy system*). [cite_start]Target pengguna utama dari aplikasi ini adalah perpustakaan skala kecil hingga menengah yang memerlukan sistem manajemen yang efisien namun mudah diimplementasikan.

[cite_start]Sistem ini menyediakan serangkaian fungsionalitas yang terstruktur dengan baik, mencakup:
* [cite_start]**Manajemen Data Inti (Master Data):** Kemampuan untuk mengelola data fundamental perpustakaan, meliputi data anggota (dengan fitur tambah, edit, hapus, dan cetak kartu), data buku (manajemen koleksi), serta data pengguna sistem (admin dan petugas).
* [cite_start]**Manajemen Sirkulasi:** Fitur ini menangani alur peminjaman dan pengembalian buku. [cite_start]Ini termasuk pencatatan transaksi peminjaman, proses pengembalian yang terintegrasi dengan kalkulasi denda otomatis jika terjadi keterlambatan, dan opsi untuk perpanjangan masa peminjaman.
* [cite_start]**Sistem Pelaporan:** Aplikasi mampu menghasilkan laporan-laporan terperinci yang esensial untuk audit dan evaluasi kinerja perpustakaan, seperti rekapitulasi data anggota, data buku, dan seluruh riwayat transaksi sirkulasi.
* [cite_start]**Sistem Autentikasi:** Terdapat mekanisme login yang membedakan level pengguna antara Admin (hak akses penuh) dan Petugas (hak akses operasional terbatas).

### 2. Persyaratan Aplikasi

[cite_start]Untuk menjamin aplikasi dapat beroperasi dengan lancar, stabil, dan memberikan performa yang diharapkan, lingkungan instalasi harus memenuhi beberapa kriteria teknis dari sisi perangkat keras dan perangkat lunak.

* **Kebutuhan Perangkat Keras (Hardware):**
    * [cite_start]**Komputer/Server:** Diperlukan sebuah unit komputer yang akan difungsikan sebagai server dengan kapasitas memori (RAM) paling sedikit 2 GB. [cite_start]Spesifikasi ini krusial untuk menangani beban kerja dari Apache, proses PHP, dan layanan database secara simultan.
    * **Penyimpanan (Storage):** Ruang kosong pada disk minimal 500 MB. [cite_start]Alokasi ini dibutuhkan untuk menampung file-file kode sumber, direktori aset, serta pertumbuhan data di dalam database seiring waktu penggunaan.

* **Kebutuhan Perangkat Lunak (Software):**
    * [cite_start]**Web Server Stack:** Sangat direkomendasikan untuk menggunakan paket **XAMPP Control Panel v3.3.0** karena sudah mencakup seluruh dependensi yang dibutuhkan.
    * **PHP:** Versi PHP yang harus digunakan adalah **versi 8.0.30**. [cite_start]Persyaratan ini bersifat mandatori untuk menghindari masalah kompatibilitas fungsi, terutama mengingat adanya penggunaan fungsi usang di dalam kode.
    * [cite_start]**Database:** Diperlukan server database **MySQL atau MariaDB**, yang merupakan komponen standar dalam paket XAMPP.
    * [cite_start]**Browser:** Aplikasi ini dapat diakses dengan baik melalui peramban web modern seperti Google Chrome, Mozilla Firefox, atau Microsoft Edge.

### 3. Struktur Direktori dan File

[cite_start]Struktur direktori aplikasi ini dirancang secara modular untuk memisahkan antara logika bisnis, aset antarmuka, dan file-file konfigurasi. [cite_start]Pengorganisasian yang jelas seperti ini merupakan praktik yang baik karena sangat memudahkan proses pemeliharaan, pelacakan bug, dan pengembangan fitur di kemudian hari.

-   [cite_start]`admin/`: Direktori utama yang menampung semua file logika dan antarmuka untuk halaman admin.
    -   [cite_start]`agt/`: Modul spesifik untuk manajemen Anggota (tambah, edit, hapus, cetak).
    -   [cite_start]`buku/`: Modul untuk manajemen Buku.
    -   [cite_start]`laporan/`: Modul untuk menghasilkan berbagai jenis laporan.
    -   [cite_start]`log/`: Modul untuk melihat riwayat sirkulasi (peminjaman dan pengembalian).
    -   [cite_start]`pengguna/`: Modul untuk manajemen pengguna sistem.
    -   [cite_start]`sirkul/`: Modul inti yang menangani transaksi sirkulasi.
-   [cite_start]`assets/` & `assets_style/`: Berisi semua aset frontend, seperti file CSS, JavaScript, dan berbagai library pihak ketiga yang memperkaya tampilan.
-   [cite_start]`bootstrap/`: Menyimpan file-file dari framework CSS Bootstrap.
-   [cite_start]`inc/`: Berisi file-file inklusi penting, terutama `koneksi.php` yang mengatur hubungan ke database.
-   [cite_start]`home/`: Berisi file halaman dashboard atau beranda untuk pengguna yang telah login.
-   [cite_start]`plugins/`: Menyimpan berbagai plugin jQuery tambahan seperti DataTables dan Select2.
-   [cite_start]`data_perpus.sql`: File krusial berisi skema dan data awal database untuk proses instalasi.
-   [cite_start]`index.php`, `login.php`, `logout.php`: File-file utama yang mengatur alur autentikasi dan halaman awal aplikasi.

### 4. Instruksi Instalasi dan Konfigurasi

[cite_start]Berikut adalah panduan langkah demi langkah untuk melakukan instalasi dan konfigurasi aplikasi pada lingkungan pengembangan lokal menggunakan XAMPP.

1.  [cite_start]**Salin Proyek ke Direktori Server:** Salin seluruh folder proyek `perpustakaan-main` ke dalam direktori `C:\xampp\htdocs\`.
2.  [cite_start]**Buat Database:** Akses phpMyAdmin melalui browser (`http://localhost/phpmyadmin`) dan buat sebuah database baru dengan nama `data_perpus`.
3.  [cite_start]**Impor Database:** Pilih database `data_perpus` yang baru saja Anda buat. Masuk ke tab "Import", klik "Choose File" dan pilih file `data_perpus.sql` yang ada di dalam folder proyek. [cite_start]Klik tombol "Go" atau "Kirim" untuk memulai proses impor.
4.  **Verifikasi Konfigurasi:** File `inc/koneksi.php` sudah secara otomatis terkonfigurasi untuk terhubung dengan database `data_perpus`. [cite_start]Tidak ada perubahan kode yang diperlukan.
    ```php
    <?php
    $koneksi = new mysqli ("localhost","root","","data_perpus");
    ?>
    ```
5.  **Akses Aplikasi:** Buka browser dan navigasikan ke alamat `http://localhost/perpustakaan-main`. Halaman login akan muncul, dan Anda dapat masuk menggunakan kredensial default: `admin / 123`.

### 5. Dependency yang Digunakan

Aplikasi ini memanfaatkan sejumlah library dan package eksternal untuk memperkaya fungsionalitas dan pengalaman pengguna, terutama di sisi frontend.

* [cite_start]**AdminLTE v2.4.18:** Template utama untuk dasbor administrasi.
* [cite_start]**Bootstrap v3.3.7:** Framework CSS untuk desain antarmuka yang responsif.
* [cite_start]**jQuery v2.2.3:** Pustaka JavaScript yang menjadi dasar untuk manipulasi DOM dan interaktivitas.
* [cite_start]**jQuery UI:** Menyediakan komponen antarmuka tambahan seperti kalender.
* [cite_start]**DataTables:** Plugin jQuery untuk membuat tabel data yang interaktif dengan fitur pencarian, sortir, dan paginasi.
* [cite_start]**Select2:** Plugin untuk mengubah dropdown standar menjadi lebih fungsional dengan fitur pencarian.
* [cite_start]**Font Awesome:** Menyediakan set ikon vektor untuk memperindah elemen antarmuka.
* [cite_start]**Morris.js:** Digunakan untuk membuat grafik pada halaman dasbor.
* [cite_start]**PACE:** Menampilkan loading bar otomatis saat halaman dimuat.

### 6. Instruksi Build dan Deployment

* [cite_start]**Proses Build:** Aplikasi ini berbasis PHP yang merupakan bahasa *interpreted*, sehingga tidak memerlukan proses build atau kompilasi. [cite_start]File kode dapat langsung dijalankan oleh server.
* **Proses Deployment:** Untuk melakukan deployment ke server hosting online, ikuti langkah-langkah berikut:
    1.  [cite_start]Unggah semua file dan folder dari direktori proyek ke server hosting (biasanya ke dalam folder `public_html`).
    2.  [cite_start]Buat database baru di server hosting melalui panel kontrol (misalnya cPanel).
    3.  [cite_start]Impor file `data_perpus.sql` ke dalam database yang baru dibuat tersebut.
    4.  [cite_start]Sesuaikan file konfigurasi `inc/koneksi.php` dengan detail host, nama database, user, dan password yang diberikan oleh penyedia hosting.
    5.  [cite_start]Aplikasi siap untuk diakses melalui domain Anda.

### 7. Panduan Debugging dan Logging

Karena tidak adanya framework logging formal, proses debugging dan pelacakan kesalahan pada aplikasi ini dilakukan dengan pendekatan sebagai berikut:

* **Debugging Manual:** Cara paling langsung adalah dengan menyisipkan fungsi-fungsi bawaan PHP seperti `echo()`, `print_r()`, dan `var_dump()` pada baris kode yang dicurigai bermasalah untuk memeriksa nilai variabel.
* [cite_start]**Log Error Server:** Sumber informasi utama untuk kesalahan fatal adalah file log error Apache. Pada instalasi XAMPP, file ini dapat ditemukan di `C:\xampp\apache\logs\error.log`. [cite_start]Memantau file ini sangat penting saat aplikasi menunjukkan halaman putih atau error 500.
* **Error Database:** File `inc/koneksi.php` akan menghentikan eksekusi skrip jika koneksi gagal. [cite_start]Untuk men-debug query yang salah, Anda dapat menambahkan `or die(mysqli_error($koneksi))` setelah fungsi `mysqli_query()` untuk menampilkan pesan kesalahan dari MySQL.

### 8. Change Log

[cite_start]Berikut adalah rekonstruksi catatan perubahan (*change log*) berdasarkan template soal dan analisis file.

* [cite_start]**Versi 1.0.0, 2025-06-09:** Rilis awal.
* [cite_start]**Versi 1.1.0, 2025-06-15:** Tambah fitur simpan data (CRUD untuk Anggota, Buku, Sirkulasi).
* [cite_start]**Versi 1.1.0, 2025-06-21:** Pembuatan ulang dokumentasi pemeliharaan.

### 9. Bug Dikenal

[cite_start]Analisis kode sumber telah mengidentifikasi beberapa masalah dan bug yang signifikan. [cite_start]Isu-isu ini memerlukan perhatian khusus pada siklus pemeliharaan berikutnya.

* **ID Bug: 001**
    * **Deskripsi:** Penggunaan Fungsi Database Usang. [cite_start]Kode masih mengandung fungsi `mysql_*` yang telah usang (contoh: `mysql_connect`) di beberapa bagian kode. [cite_start]Fungsi-fungsi ini telah dihapus sepenuhnya di PHP 7 ke atas dan akan menyebabkan *Fatal Error* pada environment PHP 8.0.30 yang disyaratkan.
    * [cite_start]**Prioritas:** Tinggi.
    * [cite_start]**Status:** Belum Diperbaiki.
    * [cite_start]**Rekomendasi:** Refaktorisasi seluruh kode untuk menggunakan ekstensi MySQLi secara konsisten.

* **ID Bug: 002**
    * **Deskripsi:** Kerentanan SQL Injection. [cite_start]Aplikasi tidak menggunakan *prepared statements* untuk *query* database. [cite_start]Hal ini membuka celah keamanan yang sangat serius terhadap serangan SQL Injection, di mana penyerang dapat memanipulasi *input* untuk mengeksekusi perintah SQL berbahaya.
    * [cite_start]**Prioritas:** Tinggi.
    * [cite_start]**Status:** Belum Diperbaiki.
    * [cite_start]**Rekomendasi:** Implementasikan *prepared statements* pada semua *query* yang menerima *input* dari pengguna untuk menutup celah keamanan ini.

* **ID Bug: 003**
    * **Deskripsi:** Validasi Input Tidak Lengkap. [cite_start]Validasi input hanya terjadi di sisi klien (JavaScript) dan tidak ada di sisi server, sehingga rentan jika JavaScript dinonaktifkan.
    * [cite_start]**Prioritas:** Sedang.
    * [cite_start]**Status:** Belum Diperbaiki.
    * [cite_start]**Rekomendasi:** Tambahkan validasi di sisi server (PHP) untuk setiap data yang dikirim dari formulir sebelum disimpan ke database.