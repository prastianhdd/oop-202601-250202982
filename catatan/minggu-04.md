# Catatan Minggu 04: Polymorphism

## Yang saya kerjakan

Pada minggu ini, tugasnya adalah menggunakan overriding dan dynamic binding serta membedakannya dari overloading. Materi tersebut diterapkan pada perhitungan denda di Aset dan tiga turunannya. Ruang, Laptop, dan AlatLab memakai nama method yang sama, yaitu hitungDenda, tetapi menghasilkan denda sesuai jenis asetnya. Selain itu, KatalogAset dilengkapi dengan dua cara pencarian: berdasarkan kata saja atau berdasarkan kata dan jenis aset.

## Keputusan desain

- Perhitungan dasar dan pemeriksaan hari negatif ditempatkan di Aset agar tidak ditulis berulang pada setiap jenis aset. Nilai nol hari menghasilkan nol denda.
- Ruang memakai denda dasar, Laptop dua kali denda dasar, dan AlatLab empat kali denda dasar. Tarif tetap dibaca dari Varian, bukan ditulis sebagai angka tetap di dalam rumus.
- Ketiga subclass mengoverride hitungDenda. Jadi, meskipun variabelnya bertipe Aset, perhitungan mengikuti object yang sebenarnya.
- Pencarian menggunakan nama aset tanpa membedakan huruf besar dan kecil. Pencarian dengan tambahan jenis memakai hasil pencarian kata, lalu menyaring jenisnya.
- Kata atau jenis pencarian yang null ditolak agar kesalahan input terlihat jelas. Ini pemeriksaan tambahan pada input, bukan perubahan aturan bisnis dari dosen.

### Perbedaan overriding dan overloading

Overriding terlihat pada hitungDenda di Ruang, Laptop, dan AlatLab. Method induk ditulis kembali di subclass dengan parameter yang sama, tetapi hasilnya mengikuti jenis aset.

Overloading terlihat pada cari(kata) dan cari(kata, jenis). Nama method sama, tetapi parameter berbeda. Pemanggil memilih apakah hanya ingin mencari nama atau sekaligus membatasi jenis aset.

## Kendala

Kendala yang saya alami sendiri saat mempelajari materi: Memahami overriding dan overloading lumayan membuat saya bingung. Tapi pada akhirnya setelah test `BUILD SUKSES` juga.

## Penggunaan AI

- Alat yang dipakai: Claude.
- Bagian yang dibantu AI: saya memakai Claude sebagai alat bantu dalam tugas polymorphism. Saya meminta bantuan kode untuk perhitungan denda dan dua bentuk pencarian aset, sekaligus penjelasan bagaimana kode tersebut menerapkan overriding, overloading, dan dynamic binding. Hasilnya tetap perlu saya periksa dan pahami, bukan langsung dianggap benar hanya karena berasal dari AI.
- Prompt utama:
  1. "Penjelasan materi minggu 04 tentang polymorphism".
- Yang saya ubah atau tolak dari saran AI, dan alasannya: saya tidak menambahkan klaim perubahan yang belum bisa dijelaskan.
- Satu hal yang saya pahami lebih baik sekarang: variabel bertipe `Aset` tetap bisa menjalankan `hitungDenda` milik `Laptop` jika object yang disimpannya adalah `Laptop`. Ini berbeda dari `cari(kata)` dan `cari(kata, jenis)`, yang dibedakan berdasarkan parameter saat dipanggil.


