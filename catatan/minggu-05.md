# Catatan Minggu 05: Abstraction

## Yang saya kerjakan

Pada minggu ini, tugasnya adalah memilih penggunaan abstract class dan interface serta menerapkan interface pada kode. Materinya diterapkan dengan menjadikan Aset sebagai abstract class, melengkapi bisaDipinjam(), dan membuat dua aturan denda melalui DendaFlat dan DendaProgresif. Aset tetap menyimpan data yang sama untuk semua jenis aset, tetapi perhitungan dendanya wajib dibuat oleh masing-masing subclass. Kedua aturan denda menggunakan interface AturanDenda, sehingga mempunyai cara pemanggilan yang sama walaupun rumusnya berbeda.

## Keputusan desain

- Aset dibuat abstract karena berfungsi sebagai dasar bagi Ruang, Laptop, dan AlatLab, bukan jenis aset yang dibuat langsung.
- hitungDenda dibuat abstract sesuai tugas minggu ini. Karena itu, perhitungan pada subclass tidak lagi memanggil super.hitungDenda(), melainkan menghitung sesuai jenis asetnya sendiri.
- Aset boleh dipinjam hanya saat berstatus TERSEDIA dan kondisinya bukan RUSAK_BERAT. Kondisi RUSAK_RINGAN masih diperbolehkan selama statusnya tersedia.
- DendaFlat menggunakan hasil hitungDenda dari aset tanpa tambahan.
- Untuk denda progresif, saya memilih tujuh hari pertama memakai tarif biasa. Setiap hari setelah hari ke-7 dikenai dua kali tarif harian. Tambahan ini hanya berlaku untuk hari berikutnya, bukan untuk seluruh hari keterlambatan. Keputusan tersebut dicatat pada A-02 di docs/asumsi.md.


## Kendala

Hal yang perlu diperhatikan adalah perubahan hitungDenda menjadi abstract. Method tersebut tidak lagi mempunyai isi di Aset, sehingga pemanggilan super.hitungDenda() dari minggu sebelumnya harus disesuaikan. Ini berbeda dari super(kode, nama), yang tetap digunakan untuk memanggil constructor induk.


## Penggunaan AI

- Alat yang dipakai: Claude.
- Bagian yang dibantu AI: saya memakai Claude sebagai alat bantu untuk menerapkan abstract class dan interface pada tugas ini. Bantuan mencakup kode Aset, penyesuaian perhitungan pada turunannya, dua aturan denda, serta penjelasan hubungan antarbagian tersebut. Claude juga membantu menyiapkan tes dan panduan belajar. Hasilnya tetap perlu saya periksa dan pahami sesuai aturan tugas.
- Prompt utama, diringkas berdasarkan topik pembahasan:
  1. "Penjelasan materi minggu 05 tentang abstraction".
- Yang saya ubah atau tolak dari saran AI, dan alasannya: saat diberikan pilihan aturan progresif, saya memilih tarif tambahan untuk hari setelah tujuh hari agar batasnya mudah dijelaskan. Saya juga meminta format catatan mengikuti minggu sebelumnya dan memakai bahasa yang sederhana.
- Satu hal yang saya pahami lebih baik sekarang: Denda setelah 7 hari berubah menjadi 2x.
