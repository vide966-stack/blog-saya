
Setiap tahap memiliki fungsi berbeda:

| Tahap | Pertanyaan utama |
|---|---|
| IS Research | Hipotesis dan kandidat apa yang mungkin memiliki informasi? |
| IS Selection | Kandidat mana yang memenuhi aturan bukti? |
| Freeze | Apa tepatnya yang akan diuji? |
| OOS Evaluation | Apakah kandidat yang telah dikunci bertahan pada data baru? |
| OOS Decision | Apakah bukti generalisasi cukup atau belum? |

Tanpa freeze, OOS dapat berubah menjadi ruang tuning. Tanpa OOS, hasil IS mudah disalahartikan sebagai bukti bahwa kandidat akan bekerja di luar sampel.

Freeze tidak membuktikan kandidat benar. OOS juga tidak menjamin keuntungan masa depan. Keduanya hanya membantu menjaga agar kesimpulan penelitian tidak lebih besar daripada bukti yang tersedia.

---

## 19.6. Status Freeze dan Validitas Penelitian

Untuk menjaga keterlacakan, TEKB dapat menggunakan status seperti berikut:

| Status | Arti |
|---|---|
| UNFROZEN | Kandidat atau aturan masih dapat berubah dalam tahap IS |
| FROZEN | Kandidat dan seluruh definisi penting telah dikunci |
| FREEZE_FAILED | Pembekuan gagal karena ada informasi atau konfigurasi penting yang belum lengkap |
| OOS_PENDING | Kandidat telah dibekukan dan menunggu evaluasi OOS |
| OOS_VALIDATED | Kandidat memenuhi kriteria validasi OOS |
| OOS_REJECTED | Kandidat tidak memenuhi kriteria validasi OOS |
| OOS_SPENT | Data OOS telah digunakan untuk proses seleksi atau tuning |
| OOS_TAINTED | Hasil OOS telah tercemar oleh perubahan atau penggunaan setelah hasil dilihat |

Status tersebut membantu mencegah penggunaan data secara tidak konsisten. Misalnya, kandidat dengan status OOS_SPENT tidak boleh dipresentasikan seolah-olah baru pertama kali diuji pada data yang tidak tersentuh.

---

## 19.7. Freeze Bukan Akhir dari Sikap Kritis

Freeze sangat penting, tetapi bukan solusi untuk semua masalah penelitian.

Freeze tidak menghapus:

- overfitting yang sudah terjadi di IS;
- data snooping sebelum freeze;
- terlalu banyak percobaan;
- bias survivorship;
- kualitas data yang buruk;
- kesalahan dalam hipotesis;
- perubahan rezim pasar;
- biaya transaksi;
- keterbatasan jumlah event;
- ketergantungan antar-event;
- kelemahan definisi B0.

Freeze hanya memastikan bahwa setelah kandidat dipilih, tahap validasi tidak terus-menerus diarahkan oleh hasil OOS.

Karena itu, freeze harus dipahami sebagai mekanisme pengendalian bias, bukan sebagai bukti bahwa kandidat telah menjadi benar.

---

## Ringkasan Bab

- Freeze berarti mengunci kandidat dan seluruh aturan penting sebelum hasil OOS digunakan.
- Yang dibekukan bukan hanya SL, TP, dan Maximum Hold, tetapi juga definisi entry, B0, MAE/MFE, ATR, Evaluation Engine, grid, kriteria seleksi, dan provenance.
- OOS digunakan untuk menguji generalisasi, bukan untuk memilih ulang atau menyetel kandidat.
- Jika hasil OOS digunakan untuk mengubah aturan, OOS tersebut tidak lagi murni dan harus dianggap spent atau tainted.
- Setiap perubahan aturan harus menghasilkan versi baru dan meninggalkan jejak audit.
- Freeze manifest dan fingerprint membantu memastikan konfigurasi OOS sama dengan konfigurasi yang dipilih pada IS.
- Freeze tidak menjamin kandidat benar, tetapi menjaga agar validasi dilakukan secara lebih jujur.

---

## Pertanyaan Refleksi

1. Mengapa kandidat tidak boleh diubah setelah hasil OOS dilihat?
2. Apa perbedaan antara memperbaiki bug dan mengubah metodologi?
3. Mengapa perubahan entry dapat mengubah makna hasil penelitian?
4. Mengapa aturan B0 harus dibekukan bersama kandidat B1?
5. Apa fungsi freeze manifest?
6. Apa yang dimaksud dengan OOS spent atau tainted?
7. Mengapa freeze tidak menghapus overfitting yang sudah terjadi pada IS?
8. Jika tidak ada kandidat yang lolos OOS, mengapa hasil tersebut tetap bernilai bagi penelitian?

---

## Kalimat Kunci

> Freeze bukan berarti kandidat telah terbukti benar. Freeze berarti kandidat telah dikunci agar OOS dapat menguji generalisasi secara jujur. Jika aturan diubah setelah OOS dilihat, maka data tersebut tidak lagi berfungsi sebagai ujian yang belum digunakan, melainkan telah menjadi bagian dari proses pemilihan.

---

<div align="center">

[← Bab Sebelumnya](/posts/bab-18-is-selection/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Bab Selanjutnya →](/posts/bab-20-oos-data-baru/)

</div>