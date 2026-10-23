# Catatan Minggu 02: Class, Object, Encapsulation

## Yang saya kerjakan

Pada minggu ini, tugasnya adalah membuat class dengan field private, konstruktor, getter/setter, dan validasi. Materi tersebut diterapkan pada class `Aset`, yang menyimpan kode, nama, status, dan kondisi aset. Field dibuat private agar datanya tidak bisa diubah langsung dari luar class. Konstruktor digunakan untuk mengisi data awal, getter untuk membaca data, dan setter untuk mengubah data dengan pemeriksaan terlebih dahulu.

## Keputusan desain

- Kode aset dibuat tetap dan tidak diberi setter supaya identitas aset tidak berubah setelah dibuat.
- Aset yang baru dibuat memiliki status `TERSEDIA` dan kondisi `BAIK`, sesuai aturan minggu ini.
- Kode dan nama tidak boleh kosong, hanya berisi spasi, atau bernilai `null`. Status dan kondisi juga tidak boleh `null`.

Keputusan di atas berkaitan dengan penerapan materi minggu 2. 

## Kendala

Kendala yang saya alami sendiri saat mempelajari materi: Meskipun simple tapi ada banyak `class` , menjadi lumayan pusing di awal.

Kendala lain adalah dari Readme.MD Line #25 bertuliskan `minggu-aktif.txt` diatur dosen dan ikut terbarui lewat `upstream`. Tes minggu yang belum aktif tidak dijalankan. akan tetapi hingga saat ini `minggu-aktif.txt` hanya 1 atau week-01, sedangkan harusnya diubah. Karena ada ketentuan `minggu-aktif.txt` dari dosen maka saya biarkan  dulu tetap di week 1 tetapi yang saya jalankan menggunakan maven dengan perintah : `mvn -B -ntp test "-Dgroups=week2"`

## Penggunaan AI

- Alat yang dipakai: Claude.
- Bagian yang dibantu AI: menjelaskan kode per baris untuk lebih membantu pemahaman saya.
- Prompt utama, diringkas dari permintaan saya:
  1. Penjelasan minggu 2 full code, arti tiap baris, perubahan, dan hal yang perlu dipahami.
- Yang saya ubah atau tolak dari saran AI, dan alasannya: Sementara tidak ada yang saya tolak, misalnya untuk nama object , alasanya sejalan dengan apa yang saya inginkan. 
- Satu hal yang saya pahami lebih baik sekarang: Cukup buat Class kemudian lakukan setter dan getter, tidak perlu menulis mengulang terus menerus.
