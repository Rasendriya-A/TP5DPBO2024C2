# Tugas Praktikum 5

## Janji
Saya Rasendriya Andhika dengan NIM 2305309 mengerjakan Tugas Praktikum 5 dalam mata kuliah Desain dan Pemrograman Berorientasi Objek untuk keberkahan-Nya maka saya tidak melakukan kecurangan seperti yang telah dispesifikasikan. Aamiin.

## Desain Program
Program ini terdiri dari 3 class, yaitu Menu, Mahasiswa, dan Main.

### 1. Class Menu:
- Class ini merupakan antarmuka aplikasi yang menggunakan Java Swing GUI untuk mengelola data mahasiswa. Data yang dikelola meliputi `NIM, Nama, Jenis Kelamin, dan Status Keaktifan mahasiswa` (dengan pilihan: `Aktif, Cuti, Lulus, dan Dikeluarkan`).
- Aplikasi ini menyediakan fitur untuk `menambah, memperbarui, dan menghapus` data mahasiswa yang disajikan dalam bentuk tabel. Pengguna dapat menginput atau mengubah data melalui form yang tersedia dan melihat hasil perubahan secara real-time di tabel.
- Semua data yang dimasukkan atau dimodifikasi akan disimpan dalam `database MySQL` (db_mahasiswa) dengan tabel bernama `mahasiswa.`

- Fungsi-fungsi utama dalam Class Menu meliputi:
  - insertData(): Memasukkan data baru ke dalam tabel mahasiswa setelah mengecek apakah NIM sudah ada atau belum.
  - updateData(): Memperbarui data mahasiswa yang sudah ada berdasarkan NIM yang dimasukkan.
  - deleteData(): Menghapus data mahasiswa dari tabel mahasiswa berdasarkan NIM yang dipilih.
  - setTable(): Mengambil data dari database dan menampilkannya dalam bentuk tabel.

### 2. Class Mahasiswa:
- Class ini berfungsi sebagai `model` atau `representasi objek mahasiswa` yang menyimpan atribut-atribut seperti:
  - NIM (String)
  - Nama (String)
  - Jenis Kelamin (String)
  - Status Keaktifan (String)
- Setiap objek mahasiswa `tidak` lagi `disimpan dalam ArrayList`, melainkan langsung disimpan dalam `database MySQL`. Pengambilan atau pengubahan data dilakukan dengan menggunakan `query SQL` melalui `Class Database`.

### 3. Class Database:
- Class ini bertanggung jawab untuk `mengelola koneksi dan operasi` terhadap database MySQL.

### 4. Class Main:
- Class ini berfungsi untuk `menjalankan aplikasi` dengan membuat objek dari `Class Menu` dan menampilkan antarmuka aplikasi kepada pengguna. Class ini hanya bertugas untuk menginisialisasi antarmuka GUI dan menghubungkan antara `Class Menu` dengan `Class Database.`

## Penjelasan Alur
### 1. Inisialisasi
- Proses:
  - Saat aplikasi dijalankan, Class Menu diinisialisasi dan menampilkan antarmuka utama berupa:
    - Formulir data yang terdiri dari: NIM, Nama, Jenis Kelamin (ComboBox), dan Status (ComboBox).
    - Tombol: Add, Update, Delete, dan Clear.
    - Tabel yang menampilkan seluruh data mahasiswa yang tersimpan dalam database MySQL (db_mahasiswa).
- Data Awal:
  - Jika tabel sudah terisi sebelumnya, data tersebut akan otomatis diambil dari database dan ditampilkan di tabel aplikasi.

### 2. Add
- Proses:
  - Pengguna mengisi formulir dengan memasukkan:
    - NIM (Harus unik dan tidak boleh kosong).
    - Nama (Tidak boleh kosong).
    - Jenis Kelamin (Dipilih dari ComboBox: Laki-laki / Perempuan).
    - Status Mahasiswa (Dipilih dari ComboBox: Aktif, Cuti, Lulus, Dikeluarkan).
  - Setelah formulir terisi, pengguna menekan tombol Add.

- Validasi & Error Handling:
  - Jika NIM atau Nama kosong, pesan kesalahan akan muncul (Input tidak boleh kosong!).
  - Sebelum menambahkan data, aplikasi akan memeriksa apakah NIM sudah terdaftar dalam database. Jika NIM sudah ada, pengguna akan diberikan pesan kesalahan (NIM sudah terdaftar!).

- Hasil:
  - Jika berhasil, data baru akan disimpan ke database (mahasiswa) dan diperbarui secara langsung di tabel.
  - Formulir akan dibersihkan (clearForm()) agar siap digunakan kembali.

### 3. Update
- Proses:
  - Pengguna memilih baris data dari tabel yang ingin diubah.
    - Formulir akan terisi otomatis dengan data yang dipilih.
    - Pengguna mengubah data yang diperlukan dan menekan tombol Update.
    - Perubahan disimpan ke dalam database berdasarkan NIM (sebagai primary key).

- Validasi & Error Handling:
  - Jika NIM atau Nama kosong, pesan kesalahan akan muncul (Input tidak boleh kosong!).
  - Jika NIM yang diinput tidak ditemukan dalam database, pesan kesalahan akan muncul (Data tidak ditemukan!).

- Hasil:
  - Jika berhasil, data dalam database dan tabel akan diperbarui.
  - Formulir akan dibersihkan (clearForm()) setelah operasi berhasil.

### 4. Delete
- Proses:
  - Pengguna memilih baris data yang ingin dihapus dari tabel.
    - Pengguna menekan tombol Delete.
    - Data akan dihapus dari database berdasarkan NIM yang dipilih.

- Validasi & Error Handling:
  - Jika pengguna tidak memilih data dari tabel, pesan kesalahan akan muncul (Pilih data yang ingin dihapus!).
  - Jika data tidak ditemukan dalam database, pesan kesalahan akan muncul (Data tidak ditemukan!).

- Hasil:
  - Jika berhasil, data akan dihapus dari database dan tabel akan diperbarui.
  - Formulir akan dibersihkan (clearForm()) agar siap digunakan kembali.

### 5. Clear
- Proses:
  - Setelah melakukan operasi Add, Update, atau Delete, semua field input pada formulir akan dikosongkan dengan memanggil metode clearForm().
    - Tidak ada validasi khusus dalam proses ini.
    - Fungsionalitas ini berguna agar pengguna dapat memasukkan data baru dengan lebih mudah.

### Error Handling (Secara Keseluruhan)
- Input Validation:
  - Semua input yang kosong akan menghasilkan pesan kesalahan.
  - Pesan kesalahan akan ditampilkan dengan JOptionPane.showMessageDialog().

- Duplicate Data Prevention:
  - Saat menambahkan data, NIM yang sudah ada di database tidak dapat dimasukkan lagi.

- Database Connection Handling:
  - Jika terjadi kegagalan koneksi dengan database, aplikasi akan melempar RuntimeException dengan pesan kesalahan yang jelas (SQLException).

- Feedback User:
  - Setelah setiap operasi berhasil (Add, Update, Delete), pesan sukses akan ditampilkan (JOptionPane.showMessageDialog()).

## Dokumentasi
- Error Handling pada saat Insert
![Error Handling Kolom Kosong Ketika Insert Data](https://github.com/user-attachments/assets/73715064-d216-424e-a2aa-1f90b02bc192)
![Error Handling Memasukkan NIM yang Sudah Terdaftar](https://github.com/user-attachments/assets/0813e688-bf2c-4732-b610-712abb94fd32)

- Error Handling pada saat Update
![Error Handling Kolom Kosong Ketika Update Data](https://github.com/user-attachments/assets/2cbfd16c-c19b-41fb-a0e3-75f77f5763cf)

- Pesan Konfirmasi ketika melakukan Delete
![Menunjukan Pesan Konfirmasi Ketika Delete Data](https://github.com/user-attachments/assets/51a6bfcc-3fc5-4bba-8cc3-4b27d12319ce)

