# Penerapan SOLID pada Aset-Pinjam

Dokumen ini menjelaskan prinsip SOLID yang sudah tampak pada kode sampai minggu 6. Tidak ada refactor Java tambahan karena struktur hasil minggu sebelumnya sudah cukup untuk menunjukkan lebih dari dua prinsip. Klaim di bawah dibatasi pada perilaku yang benar-benar tersedia; method jadwal untuk minggu 7 dan 9 tidak dianggap selesai.

## 1. Single Responsibility Principle (SRP)

Setiap class sebaiknya memiliki satu alasan utama untuk berubah. Pemisahan tanggung jawab terlihat pada beberapa bagian:

- `Aset` dan subclass-nya menangani data serta perilaku tiap jenis aset, termasuk kelayakan dipinjam dan denda dasar menurut jenis.
- `KatalogAset` menangani penyimpanan serta pencarian aset di memori. Ia tidak menghitung denda.
- `DendaFlat` dan `DendaProgresif` menangani kebijakan denda, bukan data identitas aset.
- `JadwalPeminjaman` disiapkan untuk mengelola kumpulan jadwal peminjaman, bukan pencarian katalog.

Pemisahan ini membuat perubahan pencarian nama tidak perlu mengubah class denda. Sebaliknya, perubahan rumus progresif tidak perlu mengubah `KatalogAset`. SRP bukan berarti setiap class hanya memiliki satu method, tetapi setiap class mempunyai fokus tanggung jawab yang jelas.

## 2. Open/Closed Principle (OCP)

Kode terbuka untuk penambahan perilaku, tetapi pemanggil tidak harus diubah untuk setiap variasi. Interface `AturanDenda` mendefinisikan satu operasi:

```java
long hitung(Aset aset, int hariTerlambat);
```

`DendaFlat` dan `DendaProgresif` mengimplementasikan kontrak tersebut dengan rumus berbeda. Kode pemanggil dapat menggunakan tipe `AturanDenda`, lalu mengganti object strateginya tanpa mengubah bentuk pemanggilan `hitung(...)`. Bila nanti diperlukan strategi baru, misalnya denda berdasarkan kategori pengguna, class baru dapat mengimplementasikan `AturanDenda` tanpa mengubah dua strategi yang sudah ada.

Hierarki `Aset` juga mendukung penambahan jenis aset. Subclass baru wajib menyediakan `hitungDenda(int)` karena method tersebut abstract. Namun, penambahan jenis baru tetap mungkin menuntut perubahan pada enum `JenisAset` atau bagian lain yang bergantung pada enum. Karena itu, klaim OCP yang paling jelas pada kode saat ini adalah variasi strategi melalui `AturanDenda`, bukan seluruh sistem tanpa pengecualian.

## 3. Dependency Inversion Principle (DIP)

Contoh sederhana DIP terlihat pada penggunaan kontrak `AturanDenda`. Kode tingkat tinggi yang perlu menghitung denda dapat bergantung pada interface tersebut, bukan langsung pada `DendaFlat` atau `DendaProgresif`. Implementasi konkret dapat diberikan sesuai kebutuhan:

```java
AturanDenda aturan = new DendaFlat();
long nilai = aturan.hitung(aset, hariTerlambat);
```

Ketergantungan pada abstraksi memudahkan pergantian strategi dan pengujian karena implementasi dapat diganti tanpa mengubah kontrak pemanggil. Saat ini belum ada service produksi yang menerima `AturanDenda` melalui constructor, sehingga penerapan DIP masih sederhana. Tidak perlu menambah service atau dependency injection hanya untuk memenuhi diagram; refactor seperti itu baru layak ketika ada pemanggil nyata yang membutuhkan strategi tersebut.

## Kesimpulan

Prinsip yang paling kuat ditunjukkan adalah **SRP** melalui pemisahan model, katalog, jadwal, dan aturan denda; serta **OCP** melalui interface `AturanDenda` dengan implementasi `DendaFlat` dan `DendaProgresif`. **DIP** mulai terlihat melalui pemakaian interface sebagai tipe ketergantungan. Struktur yang ada sudah cukup untuk tugas minggu 6, sehingga tidak dilakukan perubahan Java yang belum diperlukan.
