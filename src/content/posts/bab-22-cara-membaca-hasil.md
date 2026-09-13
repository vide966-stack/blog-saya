---
title: "BAB 22 — Cara Membaca Hasil Penelitian TEKB"
published: 2026-09-12
description: "Membaca laporan TEKB bukan sekadar mencari angka terbesar. Bab ini menjelaskan cara membaca jumlah event, distribusi, MAE/MFE, B1 vs B0, bootstrap, dan OOS."
tags: ["bab-22", "membaca-hasil", "distribusi", "oos"]
category: "Bab"
draft: false
lang: ""
---

**BAGIAN VII — MEMBACA, MENELUSURI, DAN MENGGUNAKAN HASIL TEKB**

---

## Tujuan Bab

Hasil penelitian trading sering ditampilkan dalam bentuk angka, tabel, grafik, persentase, atau warna. Ada angka hijau yang terlihat menjanjikan, angka merah yang terlihat buruk, dan berbagai metrik yang tampak meyakinkan.

Namun, satu angka tidak pernah cukup untuk menyimpulkan bahwa suatu kondisi pasar benar-benar memiliki keunggulan informasi.

Win rate yang tinggi belum tentu menghasilkan keuntungan. Mean return yang positif belum tentu stabil. Nilai p yang kecil belum tentu berarti hasil tersebut berguna secara praktis. Bahkan hasil penelitian yang sangat baik di masa lalu dapat gagal ketika diuji pada data yang belum pernah digunakan.

Karena itu, membaca laporan TEKB bukan sekadar mencari angka terbesar atau warna paling hijau. Membaca laporan TEKB berarti memahami:

- Berapa banyak data yang benar-benar digunakan.
- Bagaimana hasil tersebar, bukan hanya berapa nilai rata-ratanya.
- Seberapa besar harga bergerak mendukung atau melawan posisi.
- Apakah hasil B1 benar-benar lebih baik daripada B0.
- Seberapa besar ketidakpastian hasil tersebut.
- Apakah hasil tetap bertahan ketika diuji pada data OOS.

Prinsip utama bab ini adalah:

> Jangan bertanya hanya, "Apakah hasilnya positif?" Tanyakan juga, "Positif dibandingkan apa, berdasarkan berapa banyak data, dengan penyebaran seperti apa, dan apakah hasilnya tetap bertahan di luar data penelitian?"

---

## 22.1. Membaca Jumlah Event

### 22.1.1. Apa Itu Event?

Dalam TEKB, **event** adalah kejadian yang memenuhi definisi penelitian tertentu.

Contohnya, sebuah event dapat didefinisikan sebagai:

- volume relatif melewati ambang tertentu;
- candle memenuhi kondisi OHLCV tertentu;
- terjadi breakout;
- muncul pola setelah kondisi strength dan pullback;
- atau kombinasi kondisi lain yang telah ditentukan sebelum pengujian.

Event bukan sekadar tanda pada grafik. Event harus memiliki identitas, waktu, instrumen, aturan deteksi, dan status yang jelas.

Misalnya, penelitian menemukan 1.000 kejadian SAMSON. Angka 1.000 tersebut baru menunjukkan jumlah kejadian yang terdeteksi, bukan jumlah kejadian yang otomatis dapat digunakan untuk menyimpulkan adanya edge.

### 22.1.2. Jumlah Event Terdeteksi

**Jumlah event terdeteksi** adalah semua kejadian yang memenuhi aturan deteksi awal.

Contoh:

| Tahap | Jumlah |
|---|---|
| Event terdeteksi | 1.000 |

Angka ini menjawab pertanyaan:

> "Berapa kali kondisi yang sedang diteliti muncul dalam data?"

Namun, event terdeteksi belum tentu semuanya valid. Sebagian mungkin memiliki masalah data, berada terlalu dekat dengan event lain, tidak memiliki horizon pengamatan yang cukup, atau tidak memenuhi syarat penelitian lanjutan.

### 22.1.3. Jumlah Event Valid

**Event valid** adalah event yang lolos pemeriksaan kualitas dan aturan penelitian.

Beberapa alasan event dapat dikeluarkan antara lain:

- data OHLCV tidak valid;
- timestamp tidak konsisten;
- event melanggar aturan no-look-ahead;
- event terlalu dekat dengan event lain sehingga terkena aturan declustering;
- entry tidak dapat ditentukan sesuai kontrak;
- instrumen atau periode tidak termasuk dalam populasi penelitian;
- event tidak memenuhi syarat minimum penelitian.

Contoh:

| Tahap | Jumlah |
|---|---|
| Event terdeteksi | 1.000 |
| Event valid | 850 |

Artinya, dari 1.000 event yang terdeteksi, hanya 850 yang memenuhi aturan validitas.

Perbedaan ini penting. Jika laporan hanya menyebut "penelitian menggunakan 1.000 event", pembaca perlu bertanya apakah 1.000 tersebut adalah event terdeteksi, event valid, atau event yang benar-benar masuk ke analisis akhir.

### 22.1.4. Jumlah Event yang Memiliki B0

Dalam penelitian TEKB, B1 biasanya adalah kelompok event yang memiliki kondisi atau sinyal yang sedang diteliti. B0 adalah pembanding yang dipilih menggunakan aturan yang telah ditentukan.

Tidak semua event valid selalu memiliki B0 yang sah.

Contoh:

| Tahap | Jumlah |
|---|---|
| Event terdeteksi | 1.000 |
| Event valid | 850 |
| Event memiliki B0 | 720 |

Dari 850 event valid, hanya 720 yang memiliki pembanding B0 sesuai aturan.

Event tanpa B0 tidak boleh diam-diam diperlakukan seolah-olah memiliki pembanding. Jika aturan penelitian mensyaratkan perbandingan berpasangan B1 versus B0, event tanpa B0 harus dicatat sebagai NO_MATCH_FOUND dan dikeluarkan dari analisis edge berpasangan.

Hal ini bukan berarti event tersebut tidak berguna sama sekali. Event masih dapat disimpan sebagai bagian dari audit atau analisis deskriptif. Namun, event tersebut tidak boleh digunakan untuk mengklaim bahwa B1 lebih baik daripada B0 jika pasangan pembandingnya tidak tersedia.

### 22.1.5. Jumlah Event yang Dievaluasi

Event yang memiliki B0 belum tentu seluruhnya dapat dievaluasi.

Contohnya:

- horizon belum lengkap;
- ATR tidak tersedia;
- data setelah entry terputus;
- event masuk status INSUFFICIENT_HORIZON;
- evaluasi SL/TP tidak dapat dilakukan;
- terdapat invalidasi berdasarkan kontrak penelitian.

Contoh lengkap:

| Tahap | Jumlah |
|---|---|
| Event terdeteksi | 1.000 |
| Event valid | 850 |
| Event memiliki B0 | 720 |
| Event dievaluasi | 680 |

Dalam contoh ini, angka utama untuk analisis tertentu mungkin bukan 1.000, bukan 850, dan bukan 720, melainkan **680**.

Namun, denominator yang benar bergantung pada metrik yang sedang dibaca. Jumlah event untuk analisis MAE horizon R3 dapat berbeda dari jumlah event untuk evaluasi TP/SL dengan max hold R10.

Karena itu, setiap angka hasil harus dibaca bersama denominator-nya.

### 22.1.6. Mengapa Denominator Harus Diperhatikan?

**Denominator** adalah jumlah pengamatan yang menjadi dasar suatu persentase atau statistik.

Misalnya:

- 90 kemenangan dari 100 event = 90%.
- 9 kemenangan dari 10 event = 90%.

Persentasenya sama, tetapi tingkat informasi keduanya tidak sama. Sampel 10 event jauh lebih rapuh terhadap kebetulan dibandingkan 100 event.

Contoh lain:

| Kelompok | Profit | Total Event | Win Rate |
|---|---|---|---|
| B1 | 90 | 100 | 90% |
| B0 | 70 | 100 | 70% |

Sekilas hasil B1 tampak kuat. Tetapi pembaca masih perlu mengetahui:

- Apakah event saling berdekatan?
- Apakah event berasal dari hanya satu tanggal?
- Apakah event didominasi satu saham?
- Apakah sebagian besar event berasal dari satu periode pasar?
- Apakah hasilnya tetap sama setelah biaya?
- Apakah B0 dipilih secara adil?
- Apakah perbedaan tersebut bertahan dalam bootstrap dan OOS?

Jumlah event saja tidak cukup. Sebaiknya laporan juga mencantumkan:

- jumlah event;
- jumlah tanggal unik;
- jumlah instrumen;
- jumlah pasangan B1-B0;
- jumlah event yang dikeluarkan;
- alasan pengeluaran;
- jumlah event dengan horizon lengkap;
- jumlah event yang berstatus ambigu atau timeout.

### 22.1.7. Event Tidak Sama dengan Observasi yang Sepenuhnya Independen

Seribu event tidak selalu berarti seribu informasi yang benar-benar terpisah.

Misalnya, 20 event muncul pada hari yang sama karena satu kondisi pasar ekstrem. Event-event tersebut dapat saling berkaitan. Jika semuanya dihitung seolah-olah independen, tingkat kepastian hasil dapat terlihat lebih tinggi daripada kenyataannya.

Karena itu, pembaca perlu memperhatikan:

- jumlah tanggal unik;
- pengelompokan berdasarkan tanggal;
- declustering;
- block bootstrap;
- moving block;
- atau metode lain untuk menangani ketergantungan antar-event.

Prinsipnya:

> Jumlah event menunjukkan banyaknya kejadian, tetapi jumlah tanggal dan struktur ketergantungannya membantu menunjukkan seberapa banyak informasi yang benar-benar berbeda.

---

## 22.2. Membaca Distribusi Hasil

Setelah mengetahui jumlah event, langkah berikutnya adalah membaca bagaimana hasil tersebar.

Jangan hanya melihat satu angka seperti mean return. Dua penelitian dapat memiliki mean yang sama, tetapi memiliki risiko dan pola hasil yang sangat berbeda.

### 22.2.1. Median

**Median** adalah nilai tengah setelah seluruh hasil diurutkan.

Jika terdapat lima hasil:

- -5%, -2%, 1%, 2%, 20%

maka median-nya adalah **1%**, karena 1% berada di tengah.

Median membantu menjawab:

> "Seperti apa hasil yang berada di tengah pengalaman event?"

Median lebih tahan terhadap pengaruh nilai ekstrem dibandingkan mean.

Misalnya, sebagian besar event menghasilkan return kecil, tetapi satu event menghasilkan keuntungan yang sangat besar. Mean dapat terdorong naik oleh satu kejadian tersebut, sedangkan median mungkin tetap rendah.

### 22.2.2. Mean

**Mean** atau rata-rata aritmetika diperoleh dengan menjumlahkan seluruh hasil lalu membaginya dengan jumlah pengamatan.

Misalnya, hasil lima event adalah:

- -5%, -2%, 1%, 2%, 20%

Mean-nya:

> (-5 − 2 + 1 + 2 + 20) / 5 = 3,2%

Mean sebesar 3,2% terlihat positif. Namun, sebagian besar event sebenarnya menghasilkan hasil negatif atau kecil. Keuntungan rata-rata terutama didorong oleh satu event dengan return 20%.

Mean berguna, tetapi tidak boleh dibaca sendirian.

### 22.2.3. Percentile

**Percentile** menunjukkan posisi suatu nilai dalam distribusi.

Beberapa percentile yang umum dibaca:

- **P5:** batas bawah distribusi;
- **P25:** kuartil bawah;
- **P50:** median;
- **P75:** kuartil atas;
- **P95:** batas atas distribusi.

Contoh:

| Metrik | Nilai |
|---|---|
| P5 | -8% |
| P25 | -3% |
| P50 / Median | 0,5% |
| P75 | 4% |
| P95 | 12% |

Interpretasinya:

- sekitar 5% hasil berada di bawah -8%;
- sekitar 25% hasil berada di bawah -3%;
- separuh hasil berada di bawah 0,5%;
- sekitar 25% hasil berada di atas 4%;
- sekitar 5% hasil berada di atas 12%.

Percentile membantu pembaca melihat bentuk distribusi, bukan hanya pusatnya.

### 22.2.4. Penyebaran Hasil

**Penyebaran** menunjukkan seberapa jauh hasil berbeda satu sama lain.

Dua strategi dapat memiliki mean return 2%, tetapi:

- Strategi A menghasilkan sebagian besar event antara 1% dan 3%.
- Strategi B menghasilkan sebagian besar event antara -20% dan 20%.

Mean keduanya sama, tetapi pengalaman risikonya sangat berbeda.

Ukuran penyebaran yang dapat muncul dalam laporan antara lain:

- standard deviation;
- interquartile range;
- rentang minimum–maksimum;
- percentile;
- distribusi histogram;
- distribusi kumulatif atau CDF.

Untuk pembaca awam, pertanyaan sederhananya adalah:

> "Apakah hasilnya relatif berkumpul, atau sangat menyebar dan tidak stabil?"

### 22.2.5. Ekor Kerugian

**Ekor kerugian** adalah bagian distribusi yang berisi hasil-hasil terburuk.

Contoh:

| Metrik | B1 |
|---|---|
| P5 | -15% |
| Median | 1% |
| Mean | 2% |
| P95 | 10% |

Mean dan median positif, tetapi P5 sebesar -15% menunjukkan bahwa sebagian kecil event dapat mengalami kerugian besar.

Ekor kerugian penting karena pengalaman trading tidak hanya ditentukan oleh hasil rata-rata, tetapi juga oleh kemungkinan menghadapi kejadian buruk.

Pertanyaan yang perlu diajukan:

- Seberapa buruk 5% hasil terburuk?
- Apakah kerugian ekstrem lebih besar daripada keuntungan ekstrem?
- Apakah biaya dan slippage dapat memperburuk ekor kerugian?
- Apakah kerugian besar terjadi pada kondisi pasar tertentu?
- Apakah ekor kerugian B1 lebih buruk daripada B0?

### 22.2.6. Proporsi Return Positif

**Proporsi return positif** adalah persentase event yang menghasilkan return di atas nol.

Misalnya:

- 60 dari 100 event menghasilkan return positif;
- proporsi return positif = 60%.

Namun, proporsi return positif bukan hal yang sama dengan win rate strategi yang menggunakan SL/TP.

Return positif dapat dihitung berdasarkan perubahan harga pada horizon tertentu, sedangkan win rate SL/TP bergantung pada aturan entry, stop loss, take profit, max hold, biaya, dan penyelesaian konflik intrabar.

Karena itu, laporan harus menjelaskan definisi "positif" yang digunakan.

### 22.2.7. Mengapa Mean Saja Tidak Cukup?

Perhatikan dua distribusi berikut.

**Distribusi A:**

- 1%, 1%, 2%, 2%, 4%

Mean = 2%.

**Distribusi B:**

- -20%, -5%, 0%, 5%, 30%

Mean = 2%.

Keduanya memiliki mean yang sama, tetapi karakteristiknya berbeda:

- Distribusi A lebih rapat.
- Distribusi B lebih menyebar.
- Distribusi B memiliki ekor kerugian yang lebih berat.
- Distribusi B lebih bergantung pada hasil ekstrem.

Maka, laporan TEKB sebaiknya membaca mean bersama:

- median;
- percentile;
- proporsi positif;
- penyebaran;
- ekor kerugian;
- jumlah event;
- dan perbandingan B0.

Prinsipnya:

> Mean menjelaskan pusat rata-rata, tetapi distribusi menjelaskan pengalaman hasil secara lebih lengkap.

---

## 22.3. Membaca MAE dan MFE

MAE dan MFE membantu melihat perjalanan harga setelah entry, bukan hanya hasil akhirnya.

### 22.3.1. MAE: Seberapa Jauh Harga Melawan Posisi?

**MAE** atau Maximum Adverse Excursion mengukur pergerakan terburuk yang melawan posisi selama horizon pengamatan.

Untuk posisi long:

- harga turun setelah entry → bergerak melawan posisi;
- titik Low yang paling rendah digunakan untuk mengukur tekanan tersebut.

Contoh:

- Entry = 1.000
- Low terendah selama horizon = 960

Maka MAE raw:

> MAE = 960 − 1000 = −40

Artinya, harga sempat bergerak 40 poin melawan posisi.

Jika ATR entry = 20, maka:

> MAE_×ATR = −40 / 20 = −2 ATR

Interpretasinya:

> Harga sempat bergerak sejauh dua kali ATR melawan posisi sebelum memperhitungkan apakah posisi akhirnya untung atau rugi.

MAE membantu menjawab:

- Seberapa besar tekanan yang biasanya harus ditahan?
- Apakah stop loss tertentu terlalu sempit?
- Apakah suatu pola membutuhkan ruang gerak besar?
- Apakah hasil positif hanya terjadi setelah mengalami drawdown besar terlebih dahulu?

### 22.3.2. MFE: Seberapa Jauh Harga Mendukung Posisi?

**MFE** atau Maximum Favorable Excursion mengukur pergerakan terbaik yang mendukung posisi selama horizon pengamatan.

Untuk posisi long:

- harga naik setelah entry → bergerak mendukung posisi;
- titik High tertinggi digunakan untuk mengukur peluang gerak positif.

Contoh:

- Entry = 1.000
- High tertinggi = 1.080

Maka MFE raw:

> MFE = 1080 − 1000 = 80

Jika ATR entry = 20:

> MFE_×ATR = 80 / 20 = 4 ATR

Artinya, harga sempat bergerak sejauh empat kali ATR mendukung posisi.

### 22.3.3. MAE dan MFE Harus Dibaca Bersama

MAE dan MFE memberikan informasi yang berbeda.

| Event | Entry | MAE | MFE | Hasil Akhir |
|---|---|---|---|---|
| A | 1.000 | -10 | +40 | +5 |
| B | 1.000 | -40 | +50 | -5 |
| C | 1.000 | -5 | +10 | +8 |

Event A sempat mengalami tekanan kecil dan memiliki peluang naik cukup besar. Event B sempat memiliki peluang keuntungan besar, tetapi akhirnya berakhir rugi. Event C memiliki gerakan yang lebih kecil, tetapi hasil akhirnya positif.

Dari tabel tersebut terlihat bahwa:

- MFE bukan hasil akhir;
- MAE bukan otomatis stop loss yang benar;
- peluang gerak tidak sama dengan profit yang direalisasikan;
- hasil akhir dipengaruhi aturan exit.

### 22.3.4. Hubungan MAE/MFE dengan Hipotesis SL/TP

MAE dan MFE dapat membantu membangun kandidat SL/TP.

Misalnya, penelitian menemukan bahwa:

- sebagian besar event positif memiliki MAE di sekitar -0,8 ATR;
- banyak event mencapai MFE sekitar +1,5 ATR;
- tetapi sebagian event membutuhkan waktu sebelum bergerak naik.

Informasi tersebut dapat digunakan untuk menguji kandidat seperti:

- SL = 1 ATR;
- TP = 1,5 ATR;
- max hold = 5 bar.

Namun, MAE dan MFE tidak otomatis membuktikan bahwa kandidat tersebut optimal.

MAE/MFE hanya menggambarkan perjalanan harga. Untuk mengetahui apakah aturan SL/TP benar-benar menghasilkan outcome yang lebih baik, kandidat harus diuji melalui Evaluation Engine dengan aturan yang sama untuk B1 dan B0.

### 22.3.5. Mengapa MFE Bukan Jaminan Profit?

Misalkan suatu event memiliki:

- Entry = 1.000;
- MFE = +100;
- hasil akhir = -20.

Artinya, harga sempat naik sampai 1.100, tetapi posisi akhirnya rugi atau tidak menghasilkan profit sesuai aturan yang digunakan.

Mengapa hal ini bisa terjadi?

- trader tidak keluar ketika harga naik;
- target profit berada di atas MFE;
- harga mencapai target lalu berbalik sebelum exit tercatat;
- aturan exit menggunakan urutan bar tertentu;
- biaya, slippage, atau gap mengurangi hasil;
- strategi menggunakan max hold yang berbeda;
- MFE dihitung sebagai potensi gerak, bukan transaksi yang benar-benar direalisasikan.

Karena itu:

> MFE menunjukkan peluang gerak yang pernah tersedia, bukan keuntungan yang pasti dapat direalisasikan.

Sebaliknya, MAE juga bukan otomatis kerugian yang benar-benar dialami jika posisi memiliki stop loss yang tereksekusi lebih awal. MAE adalah ukuran perjalanan harga berdasarkan definisi pengukuran, bukan selalu catatan transaksi aktual.

---

## 22.4. Membaca B1 versus B0

### 22.4.1. Mengapa B1 Harus Dibandingkan dengan B0?

B1 adalah kelompok yang memiliki kondisi atau sinyal yang sedang diteliti. B0 adalah pembanding yang digunakan untuk mengetahui apakah hasil B1 memang berbeda dari kondisi pembanding.

Tanpa B0, pembaca hanya mengetahui:

> "Apa yang terjadi setelah event B1?"

Dengan B0, pertanyaannya menjadi:

> "Apakah yang terjadi setelah B1 berbeda dari apa yang biasanya terjadi pada kondisi pembanding yang sebanding?"

Harga dapat naik setelah hampir semua jenis kejadian karena pasar memang kadang naik. Karena itu, return positif B1 belum otomatis menunjukkan informasi tambahan.

### 22.4.2. Membaca Perbedaan Hasil

Contoh:

| Metrik | B1 | B0 | Δ B1 − B0 |
|---|---|---|---|
| Mean return | 2,4% | 1,1% | +1,3% |
| Median return | 0,8% | 0,5% | +0,3% |
| Proporsi positif | 61% | 54% | +7 poin persentase |
| MAE median | -0,7 ATR | -0,6 ATR | -0,1 ATR |
| MFE median | +1,4 ATR | +1,0 ATR | +0,4 ATR |

B1 terlihat lebih baik pada beberapa metrik. Namun, pembaca belum boleh langsung menyimpulkan bahwa B1 memiliki edge.

Masih perlu diperiksa:

- Apakah B1 dan B0 benar-benar dipasangkan secara adil?
- Apakah perbedaan cukup besar secara praktis?
- Apakah interval ketidakpastian cukup sempit?
- Apakah hasil stabil terhadap bootstrap?
- Apakah hasil tetap terlihat pada periode dan instrumen yang berbeda?
- Apakah biaya menghapus keunggulan tersebut?
- Apakah kandidat sudah diuji OOS?

### 22.4.3. Membaca Perbedaan Distribusi

Perbedaan B1 dan B0 tidak hanya berupa perbedaan mean.

Contoh:

| Percentile | B1 | B0 |
|---|---|---|
| P5 | -12% | -8% |
| P25 | -2% | -1% |
| P50 | 1% | 0,5% |
| P75 | 5% | 3% |
| P95 | 15% | 9% |

B1 memiliki median dan ekor atas yang lebih baik, tetapi P5 B1 lebih buruk daripada B0.

Artinya, B1 mungkin memberikan peluang keuntungan lebih besar, tetapi juga memiliki risiko kerugian ekstrem yang lebih berat.

Pembacaan yang jujur bukan:

> "B1 lebih baik daripada B0."

Pembacaan yang lebih tepat:

> "B1 menunjukkan distribusi dengan peluang gerak positif dan ekor atas yang lebih besar, tetapi juga memiliki ekor kerugian yang lebih buruk. Keunggulan tersebut perlu dinilai bersama ketidakpastian dan biaya."

### 22.4.4. Membaca Worst-Case dan Best-Case

Dalam evaluasi SL/TP, satu event dapat memiliki hasil berbeda tergantung bagaimana konflik intrabar ditangani.

Misalnya, dalam satu candle setelah entry:

- High menyentuh TP;
- Low menyentuh SL;
- urutan kejadian tidak diketahui dari OHLCV.

Status yang tepat adalah AMBIGUOUS_INTRABAR.

TEKB dapat melaporkan:

- **Worst-case:** menganggap hasil yang lebih buruk;
- **Best-case:** menganggap hasil yang lebih baik.

Contoh:

| Metrik | B1 Worst | B1 Best | B0 Worst | B0 Best |
|---|---|---|---|---|
| Expectancy | -0,05R | +0,18R | -0,03R | +0,10R |

Hasil ini menunjukkan bahwa keputusan dapat sensitif terhadap ketidakpastian intrabar.

Jika edge hanya muncul dalam skenario best-case tetapi hilang dalam worst-case, maka edge tersebut rapuh. Pembaca tidak boleh memperlakukannya sebagai hasil yang sudah pasti.

### 22.4.5. Mengapa B1 Positif Tidak Otomatis Berarti Edge?

B1 dapat memiliki return positif karena:

- Pasar secara umum sedang naik.
- Periode penelitian memang menguntungkan.
- B1 memiliki eksposur terhadap saham atau sektor tertentu.
- Event muncul setelah kondisi yang memang sudah bullish.
- Hasil dipengaruhi beberapa event ekstrem.
- B0 dipilih secara tidak adil.
- Biaya transaksi menghapus selisih.
- Hasil muncul karena kebetulan.
- Kandidat dipilih setelah melihat banyak percobaan.
- Hasil tidak bertahan pada OOS.

Karena itu, edge bukan sekadar:

> B1 menghasilkan profit.

Edge lebih dekat dengan:

> B1 menunjukkan informasi tambahan yang konsisten dan cukup kuat dibandingkan pembanding yang adil, setelah memperhitungkan ketidakpastian, biaya, dan pengujian di luar sampel.

---

## 22.5. Membaca Bootstrap dan Signifikansi

### 22.5.1. Estimasi Utama

**Estimasi utama** adalah angka hasil yang dihitung dari data penelitian.

Contohnya:

- Δ mean return = +0,07R;
- Δ median return = +0,03R;
- Δ expectancy = +0,07R;
- proporsi positif B1 = 58%;
- proporsi positif B0 = 52%.

Estimasi utama menjawab:

> "Seberapa besar perbedaan yang terlihat dalam sampel ini?"

Namun, estimasi tersebut masih dapat berubah jika penelitian diulang pada sampel lain.

### 22.5.2. Mengapa Estimasi Tidak Sama dengan Kepastian?

Bayangkan sebuah penelitian menemukan Δ expectancy sebesar +0,10R.

Angka ini dapat berasal dari:

- edge yang benar-benar cukup stabil;
- sampel yang kebetulan menguntungkan;
- beberapa event ekstrem;
- ketergantungan antar-event;
- pemilihan kandidat dari banyak percobaan;
- atau kombinasi faktor lain.

Karena itu, TEKB perlu mengukur ketidakpastian, bukan hanya menghitung estimasi.

### 22.5.3. Bootstrap sebagai Cara Mengukur Ketidakpastian

**Bootstrap** adalah metode untuk mempelajari seberapa besar hasil penelitian dapat berubah jika data yang tersedia dianggap sebagai representasi dari proses yang lebih luas.

Secara sederhana, bootstrap melakukan pengambilan ulang sampel dari data penelitian sesuai aturan tertentu, kemudian menghitung ulang metrik yang sama berkali-kali.

Misalnya:

1. Hitung Δ expectancy dari data asli.
2. Bentuk sampel bootstrap.
3. Hitung kembali Δ expectancy.
4. Ulangi ribuan kali.
5. Amati penyebaran hasil bootstrap.

Hasilnya dapat digunakan untuk membuat rentang ketidakpastian.

Contoh:

| Metrik | Estimasi | Interval Bootstrap |
|---|---|---|
| Δ expectancy | +0,07R | [-0,02R, +0,16R] |

Interpretasinya:

- estimasi utama positif;
- tetapi rentang ketidakpastian masih mencakup nilai negatif;
- sehingga data belum memberikan kepastian kuat bahwa perbedaan selalu positif.

Interval bootstrap bukan jaminan bahwa nilai masa depan pasti berada di dalam rentang tersebut. Interval tersebut adalah cara untuk menggambarkan ketidakpastian berdasarkan model resampling dan struktur data yang digunakan.

### 22.5.4. Mengapa Struktur Bootstrap Harus Sesuai Data?

Event trading sering tidak sepenuhnya independen.

Event pada tanggal yang sama dapat dipengaruhi oleh:

- berita yang sama;
- kondisi pasar yang sama;
- volatilitas yang sama;
- pergerakan indeks yang sama;
- atau shock yang sama.

Jika event-event tersebut di-resample satu per satu seolah-olah independen, ketidakpastian dapat diremehkan.

Karena itu, TEKB dapat menggunakan pendekatan seperti:

- date-cluster bootstrap;
- moving block bootstrap;
- atau struktur blok lain yang sesuai dengan ketergantungan data.

Tujuannya bukan membuat hasil terlihat lebih buruk atau lebih baik, melainkan membuat pengukuran ketidakpastian lebih sesuai dengan cara data terbentuk.

### 22.5.5. Membaca Stabilitas Perbedaan

Misalnya, dua hasil bootstrap berikut.

**Hasil A:**

- estimasi Δ = +0,08R;
- interval = [+0,03R, +0,13R].

**Hasil B:**

- estimasi Δ = +0,08R;
- interval = [-0,12R, +0,28R].

Kedua estimasi utamanya sama, tetapi tingkat ketidakpastiannya berbeda.

Hasil A menunjukkan bahwa perbedaan lebih stabil dalam resampling yang digunakan. Hasil B menunjukkan bahwa perbedaan jauh lebih tidak pasti.

Namun, interval yang seluruhnya positif pun tidak otomatis membuktikan edge berlaku selamanya. Interval tersebut hanya berbicara tentang ketidakpastian dalam kerangka data dan metode penelitian yang digunakan.

### 22.5.6. Signifikansi Statistik

Signifikansi statistik berusaha menjawab pertanyaan:

> "Apakah perbedaan yang terlihat cukup sulit dijelaskan hanya sebagai variasi acak berdasarkan model pengujian yang digunakan?"

Dalam laporan, signifikansi dapat ditampilkan melalui:

- p-value;
- interval bootstrap;
- proporsi hasil bootstrap yang positif;
- uji permutasi;
- atau metode lain yang sesuai.

Namun, p-value bukan ukuran besar kecilnya keuntungan.

Contoh:

- Δ = +0,001R dengan p-value kecil;
- Δ = +0,10R dengan p-value lebih besar.

Hasil pertama mungkin signifikan secara statistik tetapi tidak berguna setelah biaya. Hasil kedua mungkin lebih berarti secara praktis, tetapi belum cukup kuat secara statistik.

Karena itu, statistik dan praktik harus dibaca bersama.

### 22.5.7. Positif Tidak Sama dengan Cukup Dapat Dipercaya

Ada tiga keadaan yang harus dibedakan:

**Positif secara numerik**

Angka hasil lebih besar dari nol.

**Cukup kuat secara statistik**

Ketidakpastian dan pengujian memberikan dukungan yang memadai terhadap perbedaan.

**Bermakna secara praktis**

Perbedaan cukup besar untuk mengatasi biaya, slippage, spread, likuiditas, risiko, dan keterbatasan eksekusi.

Sebuah hasil idealnya memenuhi ketiganya. Jika hanya memenuhi salah satu, kesimpulannya harus dibatasi.

Contoh:

> "Δ expectancy positif, tetapi interval bootstrap masih mencakup nol dan selisih setelah biaya sangat kecil."

Kalimat ini lebih jujur daripada:

> "Strategi terbukti menguntungkan."

### 22.5.8. Multiple Testing dan Signifikansi

Jika peneliti menguji banyak hipotesis, banyak horizon, banyak threshold, banyak kandidat SL/TP, atau banyak variasi aturan, peluang menemukan hasil positif secara kebetulan meningkat.

Karena itu, pembaca perlu memeriksa apakah laporan mencantumkan:

- keluarga pengujian;
- jumlah hipotesis;
- prosedur multiple-testing;
- BH-FDR jika digunakan;
- candidate grid version;
- research batch;
- attempt number;
- prior family IDs.

Hasil positif yang ditemukan setelah banyak percobaan harus dibaca lebih hati-hati daripada hasil dari satu hipotesis yang telah ditentukan sebelumnya.

---

## 22.6. Membaca Hasil IS dan OOS

### 22.6.1. Apa Itu IS?

**IS** atau In-Sample adalah bagian data yang digunakan untuk:

- mengembangkan hipotesis;
- menguji definisi;
- memilih kandidat;
- menentukan parameter yang diizinkan;
- membandingkan kandidat;
- dan menetapkan aturan yang akan dibekukan.

IS adalah tempat penelitian belajar dari data.

Karena peneliti boleh melihat hasil IS dan memperbaiki hipotesis berdasarkan hasil tersebut, IS memiliki risiko overfitting yang lebih tinggi.

Hasil IS berguna untuk seleksi, tetapi belum cukup untuk mengklaim generalisasi.

### 22.6.2. Apa Itu OOS?

**OOS** atau Out-of-Sample adalah data yang tidak digunakan untuk membangun, menyesuaikan, atau memilih kandidat.

Setelah kandidat dibekukan, kandidat tersebut diuji pada OOS menggunakan:

- definisi entry yang sama;
- aturan B0 yang sama;
- definisi MAE/MFE yang sama;
- ATR yang sama;
- Evaluation Engine yang sama;
- kriteria evaluasi yang sama.

Analogi sederhananya:

- IS adalah soal latihan;
- freeze adalah saat jawaban dikunci;
- OOS adalah ujian yang belum dilihat sebelumnya.

Jika aturan diubah setelah melihat hasil OOS, OOS tersebut tidak lagi murni sebagai pengujian yang belum dilihat.

### 22.6.3. Membaca Hasil IS

Contoh:

| Metrik | IS B1 | IS B0 | Δ |
|---|---|---|---|
| Expectancy | +0,20R | +0,06R | +0,14R |
| Median | +0,08R | +0,03R | +0,05R |
| Bootstrap interval | [+0,06R, +0,22R] | — | — |

Hasil ini tampak menjanjikan. Namun, kesimpulan yang tepat masih terbatas:

> "Kandidat menunjukkan perbedaan positif pada data IS dan memenuhi kriteria seleksi yang ditentukan."

Belum tepat mengatakan:

> "Kandidat pasti memiliki edge di pasar."

IS adalah tempat kandidat dipilih. Karena kandidat dipilih berdasarkan hasil IS, performa IS dapat terlihat lebih baik daripada performa sebenarnya di data baru.

### 22.6.4. Membaca OOS_VALIDATED

Status **OOS_VALIDATED** berarti kandidat yang telah dibekukan memenuhi kriteria validasi OOS yang telah ditetapkan sebelumnya.

Misalnya, kriteria OOS mensyaratkan:

- Δ tetap positif;
- batas ketidakpastian memenuhi aturan;
- hasil tidak runtuh setelah biaya;
- jumlah event memenuhi minimum;
- hasil dapat dievaluasi;
- tidak ada pelanggaran protokol.

Jika semua syarat terpenuhi, kandidat dapat diberi status OOS_VALIDATED.

Namun, OOS_VALIDATED tidak berarti:

- strategi pasti untung selamanya;
- tidak akan mengalami drawdown;
- tidak ada risiko perubahan rezim pasar;
- hubungan tersebut pasti kausal;
- atau kandidat bebas dari semua ketidakpastian.

Status ini berarti:

> Kandidat yang dipilih melalui IS dan dibekukan menunjukkan hasil yang memenuhi kriteria pengujian pada data OOS yang ditentukan.

### 22.6.5. Membaca OOS_REJECTED

Status **OOS_REJECTED** berarti kandidat yang sebelumnya lolos seleksi IS tidak memenuhi kriteria validasi pada OOS.

Contoh:

| Metrik | IS | OOS |
|---|---|---|
| Δ expectancy | +0,15R | -0,03R |
| Median Δ | +0,07R | -0,01R |
| Status | Lolos seleksi | Ditolak |

Interpretasi yang tepat:

> Kandidat menunjukkan hasil positif pada IS, tetapi tidak mempertahankan kinerja yang diperlukan pada OOS.

Interpretasi yang tidak tepat:

> "OOS hanya sedang jelek, jadi aturan perlu sedikit diubah agar kembali bagus."

Jika aturan diubah berdasarkan hasil OOS, peneliti sedang menggunakan data pengujian untuk melakukan seleksi ulang. Hal tersebut dapat mencemari OOS.

### 22.6.6. Mengapa IS Bagus tetapi OOS Gagal?

Beberapa kemungkinan penyebabnya:

**Overfitting**

Kandidat terlalu menyesuaikan diri dengan pola khusus pada IS.

**Data snooping**

Kandidat dipilih setelah mencoba terlalu banyak variasi.

**Sinyal tidak stabil**

Hubungan yang terlihat pada IS memang berubah pada periode lain.

**Perubahan kondisi pasar**

Volatilitas, likuiditas, partisipan, regulasi, atau struktur pasar berubah.

**Sampel IS terlalu sempit**

IS tidak mencakup berbagai kondisi pasar.

**Efek kebetulan**

Perbedaan positif pada IS tidak cukup kuat untuk bertahan.

**Perbedaan implementasi**

Aturan yang digunakan pada OOS tidak benar-benar identik dengan aturan saat IS.

**Biaya dan eksekusi**

Keuntungan bruto pada IS tidak bertahan setelah friksi pada OOS.

OOS yang gagal bukan berarti penelitian tidak berguna. Justru, OOS dapat mengungkap bahwa suatu hipotesis belum memiliki bukti generalisasi yang memadai.

### 22.6.7. Cara Menulis Kesimpulan IS dan OOS secara Jujur

Contoh kesimpulan yang tepat jika IS positif dan OOS tervalidasi:

> "Kandidat menunjukkan perbedaan positif terhadap B0 pada data IS dan mempertahankan kinerja yang memenuhi kriteria validasi pada periode OOS. Hasil ini mendukung adanya informasi tambahan dalam kerangka pengujian yang digunakan, tetapi tidak menjamin kinerja masa depan atau membuktikan hubungan kausal."

Contoh kesimpulan jika IS positif tetapi OOS gagal:

> "Kandidat menunjukkan hasil positif pada IS, tetapi tidak mempertahankan kinerja yang diperlukan pada OOS. Dengan demikian, bukti generalisasi belum memadai. Kandidat tidak dapat diperlakukan sebagai edge yang telah tervalidasi."

Contoh kesimpulan jika hasil tidak meyakinkan sejak IS:

> "Perbedaan B1 terhadap B0 belum memenuhi kriteria yang ditetapkan. Berdasarkan data dan protokol ini, belum ditemukan bukti yang cukup untuk menyatakan adanya edge."

Kalimat terakhir bukan kegagalan. Dalam penelitian yang jujur, NO_EDGE_FOUND adalah hasil yang sah.

---

## Ringkasan Bab

Membaca hasil penelitian TEKB membutuhkan lebih dari sekadar melihat angka positif atau warna hijau.

Pembaca perlu mengikuti urutan berikut:

1. **Periksa jumlah event**
   - Bedakan event terdeteksi, valid, memiliki B0, dan benar-benar dievaluasi.

2. **Periksa denominator**
   - Pastikan setiap persentase dan statistik memiliki jumlah pengamatan yang jelas.

3. **Baca distribusi**
   - Perhatikan median, mean, percentile, penyebaran, proporsi positif, dan ekor kerugian.

4. **Baca MAE dan MFE**
   - Pahami tekanan terburuk dan peluang gerak terbaik, tanpa menyamakan MFE dengan profit yang pasti direalisasikan.

5. **Bandingkan B1 dengan B0**
   - Jangan menilai B1 secara terpisah. Periksa perbedaan hasil dan distribusinya.

6. **Periksa ketidakpastian**
   - Baca bootstrap, interval, struktur ketergantungan, dan signifikansi.

7. **Periksa multiple testing**
   - Pastikan hasil tidak hanya merupakan produk dari terlalu banyak percobaan tanpa pengendalian.

8. **Bedakan IS dan OOS**
   - IS digunakan untuk seleksi. OOS digunakan untuk menguji generalisasi setelah aturan dibekukan.

9. **Baca status akhir secara tepat**
   - OOS_VALIDATED bukan jaminan masa depan, sedangkan OOS_REJECTED bukan alasan untuk menyembunyikan atau memoles hasil.

Prinsip penutup bab ini:

> Laporan TEKB yang baik tidak memaksa pembaca percaya. Laporan tersebut memberi pembaca cukup informasi untuk menilai sendiri seberapa kuat, seberapa rapuh, dan seberapa terbatas bukti yang tersedia.

Dengan cara membaca seperti ini, TEKB tidak menjadi mesin pencari sinyal yang terlihat meyakinkan, melainkan alat untuk membedakan antara hasil yang sekadar menarik dan hasil yang benar-benar memiliki dukungan bukti.

---

## Pertanyaan Refleksi

1. Mengapa jumlah event terdeteksi belum tentu sama dengan jumlah event yang benar-benar dievaluasi?
2. Mengapa denominator penting ketika membaca persentase?
3. Mengapa mean saja tidak cukup untuk membaca hasil?
4. Apa perbedaan antara MAE dan MFE?
5. Mengapa MFE bukan jaminan profit?
6. Mengapa B1 harus dibandingkan dengan B0?
7. Apa arti interval bootstrap yang masih mencakup nol?
8. Mengapa signifikansi statistik tidak otomatis berarti manfaat praktis?
9. Apa perbedaan antara IS dan OOS?
10. Apa arti OOS_VALIDATED dan OOS_REJECTED?
11. Mengapa OOS_REJECTED harus tetap dicatat?
12. Mengapa NO_EDGE_FOUND adalah hasil yang sah?

---

## Kalimat Kunci

> Laporan TEKB yang baik tidak memaksa pembaca percaya. Laporan tersebut memberi pembaca cukup informasi untuk menilai sendiri seberapa kuat, seberapa rapuh, dan seberapa terbatas bukti yang tersedia.

---

<div align="center">

[← Bab Sebelumnya](/posts/bab-21-perjalanan-satu-event/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Bab Selanjutnya →](/posts/bab-23-audit-trail/)

</div>