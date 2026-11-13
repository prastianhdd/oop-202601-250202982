# Catatan Minggu 06: UML dan SOLID

## Yang saya kerjakan

Pada minggu ini saya memodelkan struktur dan alur sistem Aset-Pinjam berdasarkan kode yang sudah ada. Saya membuat Class Diagram dalam `docs/uml/class.mmd`, Sequence Diagram dalam `docs/uml/sequence.mmd`, dan penjelasan SOLID dalam `docs/uml/solid.md`. File diagram memakai format Mermaid agar sumbernya mudah dibaca.
Class Diagram dibuat memuat class/interface inti, atribut dan method utama, visibility, paket, relasi, serta multiplicity. Sequence Diagram menunjukkan inti pengajuan peminjaman untuk skenario sukses dan bentrok menggunakan fragmen `alt`.

## Keputusan desain

- Saya memilih Mermaid sebagai sumber diagram karena berbentuk teks, mudah dibandingkan dengan kode, dan dapat divisualkan kemudian. Jika diperlukan, diagram dapat dibuat ulang di draw.io tanpa mengubah maknanya.
- Diagram dibuat berdasarkan kode yang benar-benar ada, bukan gambaran sistem akhir yang seolah-olah sudah selesai.
- Alur sukses dan bentrok tetap dimodelkan sebagai kebutuhan pengajuan, tetapi diagram memberi catatan bahwa `bentrok()` masih tugas minggu 7 dan `ajukan()` masih tugas minggu 9.
- Prinsip SOLID utama yang saya tunjukkan adalah SRP dan OCP. DIP juga mulai terlihat melalui penggunaan interface `AturanDenda`.
- Saya tidak melakukan refactor Java karena struktur dari minggu sebelumnya sudah cukup menunjukkan prinsip tersebut. Menambah service atau abstraction baru hanya untuk diagram belum diperlukan.

## Hal yang saya pahami

Class Diagram menjelaskan bentuk statis sistem, seperti isi class dan hubungan antartipe. Sequence Diagram menjelaskan urutan interaksi saat satu proses berlangsung. Karena itu, satu diagram tidak menggantikan diagram lainnya.

SRP tidak berarti satu class hanya boleh mempunyai satu method, melainkan satu fokus tanggung jawab. OCP terlihat ketika strategi denda baru bisa ditambahkan melalui `AturanDenda` tanpa mengubah strategi lama. Penggunaan interface juga membantu pemanggil bergantung pada kontrak, bukan implementasi tertentu.

## Kendala

Bagian yang perlu diperhatikan adalah konsistensi diagram dengan kode saat ini. Beberapa method di `JadwalPeminjaman` sudah dideklarasikan, tetapi masih berupa TODO untuk minggu berikutnya. Saya tidak boleh menggambarkannya seolah-olah implementasinya sudah selesai. 

## Penggunaan AI

- Alat yang dipakai: Claude.
- Bagian yang dibantu AI: penyusunan sumber Class Diagram dan Sequence Diagram Mermaid, pemeriksaan hubungan antarkelas, penjelasan SRP/OCP/DIP, serta pembuatan panduan belajar minggu 6.
- Prompt utama, diringkas berdasarkan topik pembahasan:
  1. "Penjelasan materi minggu 06 tentang UML dan SOLID".
- Yang saya ubah atau tolak dari saran AI, dan alasannya: saya memilih agar visual dapat dibuat melalui draw.io atau Mermaid. Diagram juga dibatasi pada kode yang relevan dan diberi catatan untuk method minggu berikutnya agar tidak mengklaim fitur yang belum selesai.
- Satu hal yang saya pahami lebih baik sekarang: setelah membuat visual diagram dengan mermaid, codebase lebih mudah dipahami dari pada sekadar kode penuh.
