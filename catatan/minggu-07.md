# Catatan Minggu 07: Koleksi

## Yang saya kerjakan

Pada minggu ini saya melengkapi `JadwalPeminjaman` untuk memeriksa bentrok, mengurutkan jadwal berdasarkan waktu mulai, mengelompokkan peminjaman berdasarkan kode aset, dan menghapus peminjaman berdasarkan ID. Materi koleksi diterapkan menggunakan `List` sebagai penyimpanan utama, `Comparator` untuk pengurutan, dan `Map` untuk hasil pengelompokan.

Saya juga menentukan perilaku batas waktu: peminjaman 09:00–11:00 dan 11:00–13:00 pada aset yang sama dianggap tidak bentrok. Keputusan tersebut dicatat pada A-01 di `docs/asumsi.md` dan dibuktikan melalui `BatasBentrokTest`.

## Keputusan desain

- Penyimpanan internal tetap menggunakan satu `List<Peminjaman>` karena kebutuhan saat ini sederhana dan semua operasi masih cukup dilakukan dengan iterasi.
- `semuaUrutMulai()` mengurutkan salinan daftar, bukan daftar asli. Pemanggilan method ini tidak mengubah urutan penyimpanan internal.
- `perAset()` menggunakan `LinkedHashMap` agar urutan kode aset mengikuti kemunculan pertama pada daftar dan hasil mudah dibaca.
- `hapus(id)` menggunakan `removeIf` dan mengembalikan nilai boolean dari operasi tersebut.
- Batas waktu menggunakan interval setengah terbuka `[mulai, selesai)`. Waktu selesai yang sama dengan waktu mulai berikutnya tidak dihitung tumpang tindih.
- `ajukan()` tidak dikerjakan karena masih tugas minggu 9.

## Hal yang saya pahami

`List` cocok untuk menyimpan urutan data dan mengizinkan lebih dari satu peminjaman. `Map` cocok untuk mengelompokkan peminjaman berdasarkan satu kunci, yaitu kode aset. `Comparator.comparing(Peminjaman::getMulai)` membuat aturan pengurutan lebih jelas daripada membandingkan waktu secara manual.

Rumus bentrok yang digunakan adalah: aset harus sama, `mulaiBaru` harus sebelum `selesaiAda`, dan `mulaiAda` harus sebelum `selesaiBaru`. Jika salah satu peminjaman mulai tepat saat peminjaman lain selesai, salah satu perbandingan bernilai false sehingga tidak bentrok.

## Kendala

Bagian paling penting adalah membedakan rentang yang benar-benar tumpang tindih dengan rentang yang hanya bersentuhan di batas waktu. Saya memilih tidak bentrok agar aset dapat digunakan berurutan tanpa jeda buatan. 

## Penggunaan AI

- Alat yang dipakai: Claude.
- Bagian yang dibantu AI: implementasi empat method pada `JadwalPeminjaman`, penyusunan tes batas waktu, pencatatan asumsi, pengujian, dan panduan belajar.
- Prompt utama, diringkas berdasarkan topik pembahasan:
  1. "Penjelasan materi minggu 07 tentang koleksi".
- Yang saya ubah atau tolak dari saran AI, dan alasannya: saya memilih opsi batas waktu tidak bentrok. Struktur internal tetap satu `List`, tidak menambah `Map` permanen karena belum diperlukan.
