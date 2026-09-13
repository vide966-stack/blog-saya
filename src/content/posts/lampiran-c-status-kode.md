---
title: "Lampiran C — Status dan Kode Hasil TEKB"
published: 2026-09-12
description: "Daftar status dan kode hasil yang digunakan dalam penelitian TEKB, mulai dari COMPUTED_FULL_HORIZON hingga OPEN, beserta arti dan tingkat penggunaannya."
tags: ["lampiran-c", "status", "kode-hasil", "referensi"]
category: "Lampiran"
draft: false
lang: ""
---

Dalam TEKB, tidak semua event berakhir dengan angka return atau keputusan "lolos" dan "gagal". Sebagian event tidak dapat dihitung, sebagian tidak memenuhi syarat, sebagian memiliki ketidakpastian intrabar, dan sebagian lainnya menghasilkan kesimpulan bahwa belum ditemukan edge.

Karena itu, TEKB menggunakan **status** dan **kode hasil** untuk menjelaskan apa yang terjadi pada setiap tahap penelitian.

Status bukan sekadar pesan teknis. Status merupakan bagian dari **audit trail**. Dengan adanya status, peneliti dapat membedakan:

- event yang benar-benar berhasil dihitung;
- event yang tidak memiliki data cukup;
- event yang tidak valid;
- event yang tidak memiliki pasangan B0;
- hasil yang ambigu;
- kandidat yang tidak memiliki edge;
- dan asumsi metodologis yang sudah dikunci atau masih terbuka.

Penggunaan status harus konsisten. Satu status tidak boleh digunakan untuk menggantikan status lain yang memiliki arti berbeda.

---

## C.1. COMPUTED_FULL_HORIZON

**COMPUTED_FULL_HORIZON** berarti event berhasil dihitung sampai seluruh horizon yang ditentukan.

Status ini digunakan ketika:

- event telah memenuhi syarat validitas;
- entry telah ditentukan;
- data harga tersedia untuk seluruh horizon;
- MAE/MFE atau outcome lain dapat dihitung sesuai kontrak;
- dan tidak ada masalah data yang menghalangi penyelesaian pengukuran.

### Contoh

Penelitian menetapkan horizon R5, yaitu lima bar setelah entry.

Jika event memiliki entry yang valid dan seluruh lima bar tersedia, maka hasilnya dapat diberi status:
COMPUTED_FULL_HORIZON

Status ini menunjukkan bahwa perhitungan selesai sesuai horizon. Status ini tidak otomatis berarti hasilnya positif atau bahwa event tersebut memiliki edge.

---

## C.2. INSUFFICIENT_HORIZON

**INSUFFICIENT_HORIZON** berarti data tidak cukup untuk menyelesaikan horizon pengukuran yang diwajibkan.

Contohnya:

- event terjadi terlalu dekat dengan akhir dataset;
- data setelah entry tidak tersedia hingga jumlah bar yang diperlukan;
- periode penelitian berakhir sebelum horizon selesai;
- atau data historis tidak lengkap.

### Contoh

Horizon penelitian adalah R10, tetapi event terjadi pada tiga bar terakhir dataset. Karena hanya tersedia tiga bar setelah entry, event tidak dapat dihitung sampai R10.

Statusnya:
INSUFFICIENT_HORIZON

### Perbedaan dengan TIMEOUT

**INSUFFICIENT_HORIZON** berarti data penelitian tidak cukup untuk menyelesaikan pengukuran.

**TIMEOUT** berarti data yang diperlukan tersedia sampai batas maksimum holding period, tetapi tidak ada kondisi exit yang ditentukan tercapai dalam periode tersebut.

Dengan kata lain:

- INSUFFICIENT_HORIZON = data tidak cukup.
- TIMEOUT = waktu evaluasi selesai tanpa exit yang ditentukan.

Keduanya tidak boleh disamakan.

---

## C.3. INVALIDATED

**INVALIDATED** berarti event atau observasi dinyatakan tidak valid berdasarkan aturan penelitian.

Penyebabnya dapat berupa:

- data OHLCV tidak valid;
- urutan waktu rusak;
- nilai harga atau volume tidak memenuhi syarat;
- event melanggar definisi penelitian;
- terdapat konflik timestamp;
- terjadi pelanggaran aturan no-look-ahead;
- entry tidak dapat ditentukan secara sah;
- atau event tidak memenuhi syarat struktural yang telah dikunci.

### Contoh

Sebuah bar memiliki:

> H_t < L_t

Padahal secara logika:

> H_t ≥ max(O_t, C_t, L_t)

Jika data tersebut tidak dapat diperbaiki secara sah sesuai kebijakan data, event yang bergantung pada bar tersebut dapat diberi status:
INVALIDATED

### Catatan

Event yang invalid tidak boleh diam-diam diperlakukan sebagai event normal. Alasan invalidasi harus dicatat agar peneliti dapat menelusuri penyebabnya.

---

## C.4. NO_MATCH_FOUND

**NO_MATCH_FOUND** berarti event B1 tidak menemukan pasangan B0 yang memenuhi aturan pencocokan yang telah ditentukan.

Aturan pencocokan B0 dapat mencakup:

- instrumen yang sama;
- slot waktu yang sama;
- periode yang sesuai;
- karakteristik pencocokan tertentu;
- radius waktu atau declustering;
- nearest valid trading day;
- dan aturan tie-break yang telah ditetapkan.

### Contoh

Sebuah event B1 terjadi pada slot tertentu. Namun, tidak ada event pembanding yang memenuhi semua syarat B0 dalam populasi yang tersedia.

Maka statusnya:
NO_MATCH_FOUND

### Makna metodologis

NO_MATCH_FOUND bukan berarti event tersebut rugi atau tidak memiliki edge.

Status ini hanya berarti event tersebut tidak dapat dimasukkan ke dalam analisis berpasangan B1-B0 berdasarkan aturan yang berlaku.

Event tetap dapat disimpan dalam audit trail, tetapi biasanya dikeluarkan dari analisis paired edge karena tidak memiliki pasangan pembanding yang sah.

### Larangan penting

B0 tidak boleh dipilih secara sembarangan hanya agar setiap B1 memiliki pasangan. Peneliti tidak boleh:

- melonggarkan aturan setelah melihat hasil;
- memilih pasangan berdasarkan return terbaik;
- menggunakan informasi masa depan;
- atau mengganti pasangan yang tidak menguntungkan.

---

## C.5. AMBIGUOUS_INTRABAR

**AMBIGUOUS_INTRABAR** berarti urutan kejadian dalam satu candle tidak dapat ditentukan secara pasti dari data OHLC yang tersedia.

Data OHLC hanya menunjukkan:

- Open;
- High;
- Low;
- Close.

Data tersebut tidak selalu menunjukkan **urutan** pergerakan harga di dalam candle.

### Contoh

Untuk posisi long:

- entry = 1.000;
- stop-loss = 980;
- take-profit = 1.020.

Dalam satu candle:

- High mencapai 1.025;
- Low mencapai 975.

Candle tersebut menyentuh stop-loss dan take-profit. Namun, data OHLC tidak menunjukkan apakah harga lebih dahulu mencapai 1.020 atau 980.

Karena urutannya tidak diketahui, outcome tidak boleh langsung dianggap sebagai win atau loss.

Statusnya dapat dicatat sebagai:
AMBIGUOUS_INTRABAR

### Skenario worst-case dan best-case

Untuk menangani ketidakpastian ini, TEKB dapat menghitung dua skenario:

- **Worst-case:** mengasumsikan hasil yang paling merugikan.
- **Best-case:** mengasumsikan hasil yang paling menguntungkan.

Kedua hasil tersebut harus dilaporkan secara terpisah.

AMBIGUOUS_INTRABAR tidak boleh dihapus hanya karena peneliti ingin memperoleh hasil yang lebih bersih.

---

## C.6. TIMEOUT

**TIMEOUT** berarti event telah dievaluasi sampai batas maksimum holding period, tetapi tidak mencapai stop-loss, take-profit, atau kondisi exit lain yang telah ditentukan.

### Contoh

Aturan kandidat:

- stop-loss = 1 × ATR;
- take-profit = 2 × ATR;
- maksimum holding = 5 bar.

Jika selama lima bar:

- stop-loss tidak tersentuh;
- take-profit tidak tersentuh;
- dan tidak ada exit lain yang ditentukan;

maka event berakhir dengan:
TIMEOUT

Hasil akhir kemudian dihitung sesuai aturan penelitian, misalnya menggunakan harga close pada akhir holding period.

### Perbedaan dengan INSUFFICIENT_HORIZON

**TIMEOUT** adalah outcome evaluasi yang sah karena seluruh periode evaluasi tersedia.

**INSUFFICIENT_HORIZON** berarti periode yang dibutuhkan tidak tersedia secara lengkap.

Contoh:

| Kondisi | Status |
|---|---|
| Lima bar tersedia, tidak ada SL/TP tersentuh | TIMEOUT |
| Hanya dua dari lima bar tersedia | INSUFFICIENT_HORIZON |

---

## C.7. NO_EDGE_FOUND

**NO_EDGE_FOUND** berarti penelitian tidak menemukan kandidat yang memenuhi seluruh kriteria edge yang telah ditentukan.

Status ini dapat terjadi ketika:

- perbedaan B1-B0 tidak cukup besar;
- hasil tidak signifikan sesuai kriteria;
- kandidat gagal pada skenario worst-case;
- kandidat tidak lolos BH-FDR;
- jumlah event tidak memenuhi batas minimum;
- cakupan instrumen atau tanggal tidak mencukupi;
- hasil tidak stabil;
- atau tidak ada kandidat yang memenuhi semua syarat seleksi.

### Contoh

Peneliti menguji beberapa kombinasi SL/TP. Sebagian kandidat menghasilkan expectancy positif, tetapi tidak ada yang:

- mengungguli B0 secara memadai;
- lolos kriteria ketidakpastian;
- dan memenuhi syarat practical significance.

Kesimpulan yang benar:
NO_EDGE_FOUND

### Makna ilmiah

NO_EDGE_FOUND bukan berarti penelitian sia-sia.

Status ini berarti:

> "Berdasarkan data, aturan, pembanding, dan pengujian yang digunakan, belum ditemukan bukti yang cukup untuk menyatakan adanya edge."

Status ini lebih jujur daripada memilih kandidat teratas hanya karena penelitian diharapkan menghasilkan strategi.

---

## C.8. OOS_VALIDATED

**OOS_VALIDATED** berarti kandidat yang telah dibekukan menunjukkan hasil yang memenuhi kriteria validasi OOS yang telah ditentukan.

Status ini diberikan apabila:

- kandidat telah melalui freeze;
- OOS dilakukan pada data yang tidak digunakan dalam pembentukan kandidat;
- Evaluation Engine dan aturan tetap sama;
- kriteria evaluasi telah ditentukan sebelumnya;
- dan hasil OOS memenuhi syarat validasi.

### Makna

Status ini menunjukkan bahwa kandidat memperoleh dukungan dari data di luar sampel pembentukan.

Namun, OOS_VALIDATED tidak berarti:

- profit dijamin;
- edge berlaku untuk semua kondisi pasar;
- risiko telah hilang;
- atau hubungan sebab-akibat telah terbukti.

OOS hanya memberikan bukti tambahan mengenai kemampuan generalisasi dalam jendela data yang diuji.

---

## C.9. OOS_REJECTED

**OOS_REJECTED** berarti kandidat yang telah dibekukan tidak memenuhi kriteria validasi OOS yang telah ditentukan.

Penyebabnya dapat berupa:

- hasil OOS tidak mengungguli B0;
- perbedaan terlalu kecil;
- hasil tidak stabil;
- risiko terlalu besar;
- kandidat gagal pada skenario konservatif;
- atau kriteria validasi yang telah ditentukan tidak terpenuhi.

### Contoh

Sebuah kandidat menunjukkan hasil baik pada IS dan kemudian dibekukan. Namun, pada OOS:

- expectancy turun;
- perbedaan terhadap B0 menghilang;
- dan hasil tidak memenuhi kriteria yang telah ditentukan.

Maka statusnya:
OOS_REJECTED

### Makna ilmiah

OOS_REJECTED bukan berarti seluruh hipotesis tentang pasar pasti salah untuk selamanya. Status ini berarti kandidat tersebut tidak memperoleh dukungan yang cukup pada OOS sesuai kontrak penelitian.

Kegagalan OOS harus dicatat, bukan disembunyikan atau diperbaiki secara diam-diam dengan mengubah aturan.

---

## C.10. LOCKED

**LOCKED** berarti suatu komponen, aturan, definisi, atau keputusan telah dikunci dan tidak boleh diubah dalam ruang lingkup penelitian yang sedang berjalan.

Contoh komponen yang dapat berstatus LOCKED:

- definisi event;
- definisi entry;
- aturan B0;
- definisi MAE/MFE;
- periode ATR;
- Evaluation Engine;
- candidate grid;
- kriteria seleksi;
- multiple-testing family;
- atau kandidat yang telah dibekukan.

### Contoh

Jika definisi entry telah ditetapkan sebagai:
NEXT_VALID_BAR_OPEN

dan tidak boleh diubah selama penelitian, maka definisi tersebut berstatus:
LOCKED

### Makna

LOCKED membantu mencegah perubahan metodologi yang tidak terlihat. Jika komponen yang sudah dikunci ingin diubah, perubahan tersebut harus dicatat sebagai versi atau eksperimen baru.

---

## C.11. CONFIGURED ASSUMPTION

**CONFIGURED ASSUMPTION** berarti suatu nilai atau aturan merupakan asumsi yang dipilih untuk konfigurasi penelitian, tetapi bukan hukum universal dan masih dapat dievaluasi dalam eksperimen berikutnya.

Contohnya:

- periode ATR = 14;
- threshold RV = 5;
- maksimum holding = 5 bar;
- radius declustering;
- friction ladder;
- horizon R3 atau R5;
- atau batas minimum event.

Asumsi tersebut harus:

- ditulis secara eksplisit;
- memiliki nilai yang jelas;
- memiliki alasan pemilihan;
- dicatat versinya;
- dan tidak diubah diam-diam setelah melihat hasil.

### Contoh

Penelitian menggunakan:
ATR_PERIOD = 14

Statusnya dapat dicatat sebagai:
CONFIGURED ASSUMPTION

Artinya, angka 14 merupakan konfigurasi metodologis yang digunakan dalam penelitian tersebut. Angka tersebut bukan berarti periode 14 selalu paling benar untuk semua instrumen dan kondisi pasar.

---

## C.12. OPEN

**OPEN** berarti suatu aspek metodologi, konfigurasi, atau pertanyaan penelitian belum dikunci dan masih terbuka untuk ditentukan, diuji, atau dikembangkan.

Contohnya:

- metode biaya transaksi yang belum final;
- pilihan baseline yang masih dibandingkan;
- horizon tambahan yang belum ditetapkan;
- definisi robustness yang masih dikembangkan;
- atau pengujian lanjutan yang belum memiliki kontrak final.

### Contoh

Jika penelitian belum menentukan apakah friction ladder akan menggunakan dua atau tiga tingkat biaya, maka bagian tersebut dapat diberi status:
OPEN

### Catatan penting

OPEN tidak berarti aturan boleh diubah sesuka hati di tengah penelitian.

Status ini berarti keputusan tersebut belum dikunci. Sebelum digunakan untuk seleksi final atau OOS, aspek yang relevan harus ditetapkan, diberi versi, dan dicatat.

---

## C.13. Perbedaan Status Pengukuran dan Status Keputusan

Status TEKB dapat dikelompokkan menjadi beberapa jenis.

### A. Status kelengkapan perhitungan

- COMPUTED_FULL_HORIZON
- INSUFFICIENT_HORIZON
- INVALIDATED

Status ini menjelaskan apakah suatu event dapat dihitung dan apakah datanya memenuhi syarat.

### B. Status pencocokan dan evaluasi

- NO_MATCH_FOUND
- AMBIGUOUS_INTRABAR
- TIMEOUT

Status ini menjelaskan masalah pencocokan atau hasil evaluasi event.

### C. Status keputusan penelitian

- NO_EDGE_FOUND
- OOS_VALIDATED
- OOS_REJECTED

Status ini menjelaskan hasil pada tingkat hipotesis atau kandidat, bukan sekadar satu event.

### D. Status metodologi

- LOCKED
- CONFIGURED ASSUMPTION
- OPEN

Status ini menjelaskan tingkat kepastian atau kematangan suatu aturan dan konfigurasi penelitian.

---

## C.14. Tabel Ringkasan Status

| Status | Arti Singkat | Tingkat Penggunaan |
|---|---|---|
| COMPUTED_FULL_HORIZON | Perhitungan selesai untuk seluruh horizon | Event |
| INSUFFICIENT_HORIZON | Data tidak cukup untuk menyelesaikan horizon | Event |
| INVALIDATED | Event atau data tidak memenuhi syarat validitas | Event |
| NO_MATCH_FOUND | Tidak ditemukan pasangan B0 yang sah | Event/pasangan |
| AMBIGUOUS_INTRABAR | Urutan kejadian dalam candle tidak diketahui | Outcome event |
| TIMEOUT | Holding period selesai tanpa exit yang ditentukan | Outcome event |
| NO_EDGE_FOUND | Tidak ada kandidat yang memenuhi kriteria edge | Hipotesis/kandidat |
| OOS_VALIDATED | Kandidat memenuhi kriteria validasi OOS | Kandidat |
| OOS_REJECTED | Kandidat tidak memenuhi kriteria OOS | Kandidat |
| LOCKED | Aturan atau komponen telah dikunci | Metodologi |
| CONFIGURED ASSUMPTION | Nilai merupakan asumsi konfigurasi | Metodologi |
| OPEN | Aspek masih terbuka dan belum dikunci | Metodologi |

---

## C.15. Prinsip Penggunaan Status

Status dalam TEKB harus mengikuti prinsip berikut:

1. **Status harus memiliki definisi tunggal.**
   - Satu kode tidak boleh digunakan untuk beberapa arti yang berbeda.

2. **Status harus dapat ditelusuri.**
   - Setiap status penting sebaiknya memiliki alasan, timestamp, versi aturan, dan identitas event atau kandidat.

3. **Status event tidak boleh disamakan dengan status hipotesis.**
   - Satu event dapat COMPUTED_FULL_HORIZON, tetapi hipotesis secara keseluruhan tetap dapat berakhir NO_EDGE_FOUND.

4. **Status gagal bukan data yang harus disembunyikan.**
   - INVALIDATED, INSUFFICIENT_HORIZON, dan OOS_REJECTED merupakan bagian dari pengetahuan penelitian.

5. **Status metodologi harus membatasi perubahan.**
   - Komponen LOCKED tidak boleh diubah tanpa versi baru. Komponen OPEN harus dikunci sebelum digunakan untuk keputusan final.

6. **Status tidak menggantikan angka hasil.**
   - OOS_VALIDATED, misalnya, tetap harus disertai distribusi, ukuran sampel, perbedaan B1-B0, ketidakpastian, biaya, dan batasan.

---

## Penutup Lampiran

Kode hasil TEKB dirancang agar penelitian tidak hanya menyimpan angka, tetapi juga menyimpan konteks di balik angka tersebut.

Return tanpa status dapat menyesatkan. Angka MAE tanpa informasi horizon dapat disalahpahami. Hasil OOS tanpa status freeze dapat kehilangan makna. Kandidat tanpa catatan multiple testing dapat terlihat lebih kuat daripada kenyataannya.

Dengan status yang jelas, TEKB dapat membedakan antara:

- data yang berhasil dihitung;
- data yang tidak cukup;
- event yang tidak valid;
- outcome yang ambigu;
- kandidat yang tidak memiliki edge;
- kandidat yang lolos atau gagal OOS;
- serta aturan yang sudah dikunci dan asumsi yang masih terbuka.

Tujuan akhirnya bukan membuat sistem terlihat rumit, melainkan memastikan bahwa setiap angka dan kesimpulan memiliki arti yang jelas, batas yang jujur, dan jejak yang dapat diperiksa.

---

<div align="center">

[← Lampiran B](/posts/lampiran-b-rumus-dasar/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Lampiran D →](/posts/lampiran-d-peta-lapisan/)

</div>