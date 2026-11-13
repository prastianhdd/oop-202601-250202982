# Asumsi dan Keputusan Desain

Isi bagian ini sendiri. Satu entri per keputusan. Dinilai dari kejelasan alasan dan konsistensi dengan kode dan tes Anda,
bukan dari jawaban "benar".

Format tiap entri:

```
## A-NN: judul singkat
- Pertanyaan: ...
- Keputusan: ...
- Alasan: ...
- Dampak ke kode: ... (kelas/metode)
- Tes yang membuktikan: ... (nama tes di folder mahasiswa/)
```

## Aturan ambigu dari docs/aturan-bisnis.md

Salin setiap pertanyaan ambigu (nomor 1 sampai 7) ke sini dan jawab. Contoh:

## A-01: batas waktu tidak bentrok

- Pertanyaan: Apakah peminjaman 09:00–11:00 dan 11:00–13:00 pada aset yang sama bentrok?
- Keputusan: Tidak bentrok. Rentang waktu diperlakukan sebagai interval setengah terbuka `[mulai, selesai)`, sehingga peminjaman berikutnya boleh dimulai tepat ketika peminjaman sebelumnya selesai.
- Alasan: Kedua peminjaman tidak memakai aset pada waktu yang sama. Keputusan ini juga membuat aset dapat digunakan berurutan tanpa jeda waktu buatan.
- Dampak ke kode: `JadwalPeminjaman.bentrok` menggunakan syarat `mulaiBaru < selesaiAda && mulaiAda < selesaiBaru`. Kesamaan antara waktu mulai dan selesai tidak memenuhi syarat tumpang tindih.
- Tes yang membuktikan: `BatasBentrokTest.selesaiSamaDenganMulaiTidakBentrok` di folder `core/src/test/java/id/ac/upb/asetpinjam/mahasiswa/`.

## Asumsi lain

Tambahkan di sini keputusan lain yang Anda ambil: rumus denda progresif, perubahan skema database, format error API, dan seterusnya.

## A-02: denda progresif setelah tujuh hari

- Pertanyaan: Bagaimana rumus denda progresif pada minggu 5?
- Keputusan: Hari 1–7 memakai tarif harian biasa sesuai jenis aset. Setiap hari setelah hari ke-7 memakai dua kali tarif harian. Rumusnya `aset.hitungDenda(hari) + aset.hitungDenda(Math.max(0, hari - 7))`.
- Alasan: Ambang tujuh hari dipilih mahasiswa saat menentukan aturan minggu 5. Penambahan hanya berlaku untuk hari setelah batas tersebut, sehingga tujuh hari pertama tidak ikut dihitung ulang dengan tarif ganda.
- Dampak ke kode: `DendaProgresif.hitung`. Nol hari menghasilkan nol; hari negatif ditolak oleh perhitungan aset. Denda tidak lebih murah dari flat dan terus bertambah ketika hari bertambah. Hari ke-30 dikenai 53 kali tarif harian (7 + 23 × 2), bukan 60 kali.
- Tes yang membuktikan: `Minggu05DendaTest` di folder `core/src/test/java/id/ac/upb/asetpinjam/mahasiswa/`, khususnya batas hari 7/8/30, nol, hari negatif, dan nilai hari maksimum.
