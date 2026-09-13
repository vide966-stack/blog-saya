---
title: "BAB 24 — Memahami Batasan TEKB"
published: 2026-09-12
description: "TEKB tidak menjamin profit dan tidak otomatis membuktikan kausalitas. Bab ini menjelaskan batasan TEKB, asumsi kritis, dan open items pengembangan."
tags: ["bab-24", "batasan", "asumsi", "open-items"]
category: "Bab"
draft: false
lang: ""
---

**BAGIAN VIII — BATASAN, ASUMSI, DAN ARAH PENGEMBANGAN**

---

## Tujuan Bab

TEKB dibangun untuk membantu peneliti trading mencari, mengukur, dan menguji bukti dari data. Namun, sebuah sistem penelitian yang disiplin tetap memiliki batasan.

TEKB bukan mesin yang dapat menjamin profit. TEKB juga bukan alat yang secara otomatis membuktikan bahwa suatu pola menyebabkan pergerakan harga. Hasil TEKB selalu bergantung pada kualitas data, definisi variabel, aturan penelitian, asumsi, metode evaluasi, dan kondisi pasar yang diamati.

Karena itu, semakin baik seseorang memahami TEKB, semakin hati-hati pula ia dalam menafsirkan hasilnya.

Tujuan penelitian bukan membuat ketidakpastian menghilang. Tujuan penelitian adalah membuat ketidakpastian terlihat, terukur, dan tidak disembunyikan di balik warna sinyal atau angka yang menarik.

Prinsip utama bab ini adalah:

> TEKB tidak mengubah pasar yang tidak pasti menjadi pasti. TEKB membantu kita membuat keputusan berdasarkan bukti yang lebih tertib, sambil tetap mengakui batas-batas bukti tersebut.

---

## 24.1. TEKB Tidak Menjamin Profit

### 24.1.1. Penelitian Bukan Jaminan Hasil Trading

Hasil penelitian yang positif tidak sama dengan jaminan bahwa setiap transaksi berikutnya akan menghasilkan keuntungan.

Penelitian dapat menunjukkan bahwa:

- rata-rata return B1 lebih tinggi daripada B0;
- distribusi B1 memiliki karakteristik tertentu;
- kandidat SL/TP memiliki expectancy positif;
- atau perbedaan tertentu bertahan pada data OOS.

Namun, semua itu tetap merupakan hasil pengamatan dan pengujian dalam kondisi tertentu.

Dalam praktik trading, hasil aktual dapat dipengaruhi oleh:

- harga entry yang berbeda;
- spread;
- slippage;
- antrean order;
- likuiditas;
- gap;
- keterlambatan eksekusi;
- perubahan volatilitas;
- batasan ukuran posisi;
- biaya transaksi;
- dan perilaku pasar yang berubah.

Dengan demikian, hasil penelitian tidak boleh diterjemahkan menjadi:

> "Setiap kali kondisi ini muncul, kita pasti untung."

Kesimpulan yang lebih tepat adalah:

> "Dalam data dan protokol pengujian yang digunakan, kondisi ini menunjukkan karakteristik hasil tertentu yang mungkin memiliki nilai informasi."

### 24.1.2. Distribusi Historis Dapat Berubah

TEKB mempelajari distribusi berdasarkan data historis. Namun, distribusi masa lalu tidak selalu tetap.

Pasar dapat berubah karena:

- perubahan partisipan;
- perubahan regulasi;
- perubahan struktur mikro;
- perubahan teknologi;
- perubahan biaya transaksi;
- perubahan likuiditas;
- perubahan kebijakan moneter;
- perubahan hubungan antar-aset;
- atau perubahan perilaku pelaku pasar.

Misalnya, sebuah pola volume yang dahulu sering diikuti kenaikan harga mungkin kehilangan daya informasinya ketika semakin banyak pelaku pasar menggunakan pola yang sama.

Sebaliknya, pola yang sebelumnya tidak terlihat penting dapat menjadi lebih relevan dalam kondisi pasar tertentu.

Karena itu, hasil TEKB harus dibaca sebagai:

> "Distribusi yang teramati dalam populasi dan periode penelitian."

Bukan sebagai hukum tetap yang berlaku untuk semua waktu.

### 24.1.3. Hasil Positif Tidak Menghapus Risiko

Misalnya, sebuah kandidat memiliki:

- expectancy positif;
- median return positif;
- hasil OOS positif;
- dan interval bootstrap yang mendukung.

Kandidat tersebut tetap dapat mengalami:

- rangkaian kerugian;
- drawdown;
- kerugian ekstrem;
- periode tanpa peluang;
- perubahan distribusi;
- atau kegagalan eksekusi.

Expectancy positif berarti hasil rata-rata berdasarkan definisi tertentu cenderung positif. Expectancy positif tidak berarti setiap event positif, dan tidak berarti risiko kerugian telah hilang.

Contoh sederhana:

| Event | Hasil |
|---|---|
| 1 | -1R |
| 2 | -1R |
| 3 | -1R |
| 4 | +4R |
| 5 | +4R |

Rata-rata hasilnya positif:

> (-1 − 1 − 1 + 4 + 4) / 5 = 1R

Namun, sebelum memperoleh dua hasil positif, terdapat tiga kerugian berturut-turut.

Karena itu, pembaca harus membedakan:

- profitabilitas rata-rata;
- probabilitas hasil positif;
- besarnya kerugian;
- panjang losing streak;
- drawdown;
- dan kemampuan bertahan secara finansial.

### 24.1.4. TEKB Tidak Menggantikan Manajemen Risiko

TEKB dapat membantu mengukur distribusi dan karakteristik risiko, tetapi tidak otomatis menentukan:

- ukuran posisi yang sesuai;
- batas total eksposur;
- batas kerugian harian;
- toleransi drawdown;
- kebutuhan likuiditas;
- atau kemampuan psikologis dan finansial seorang trader.

Sebuah edge statistik yang kecil dapat menjadi tidak relevan jika ukuran posisi terlalu besar. Sebaliknya, edge yang cukup baik dapat tetap tidak dapat digunakan jika biaya, likuiditas, atau kapasitas modal tidak mendukung.

Maka, hasil TEKB harus menjadi bahan pertimbangan, bukan pengganti manajemen risiko.

### 24.1.5. Bahasa Kesimpulan yang Tepat

Bahasa yang terlalu kuat:

> "TEKB membuktikan bahwa pola ini pasti menguntungkan."

Bahasa yang lebih tepat:

> "Dalam data, populasi, dan protokol pengujian yang digunakan, pola ini menunjukkan perbedaan hasil terhadap B0 yang memenuhi kriteria penelitian. Hasil tersebut tetap memiliki ketidakpastian dan tidak menjamin profit di masa depan."

Perbedaan bahasa ini penting. Bahasa pertama mengubah bukti terbatas menjadi kepastian. Bahasa kedua menjaga kesimpulan tetap sesuai dengan desain penelitian.

---

## 24.2. TEKB Tidak Membuktikan Kausalitas secara Otomatis

### 24.2.1. Conditional Association Bukan Kausalitas

TEKB terutama mempelajari **conditional association**, yaitu hubungan atau perbedaan hasil yang muncul ketika kondisi tertentu terpenuhi.

Misalnya:

> "Ketika volume relatif tinggi dan candle memiliki karakteristik tertentu, return berikutnya berbeda dari B0."

Kesimpulan tersebut dapat didukung oleh data.

Namun, kesimpulan tersebut belum otomatis berarti:

> "Volume tinggi menyebabkan return berikutnya naik."

Perbedaan ini sangat penting.

**Conditional association** menjawab:

> "Apa yang cenderung terjadi ketika kondisi X muncul?"

**Kausalitas** menjawab:

> "Apakah X menyebabkan perubahan Y, dan bagaimana mekanisme penyebabnya?"

Penelitian TEKB standar tidak selalu dirancang untuk menjawab pertanyaan kausal.

### 24.2.2. Hubungan Historis Dapat Dipengaruhi Faktor Lain

Sebuah pola dapat berkaitan dengan return karena faktor lain yang tidak sepenuhnya diukur.

Misalnya, volume tinggi dapat muncul bersamaan dengan:

- berita perusahaan;
- perubahan indeks;
- pembukaan pasar;
- aksi institusi;
- perubahan sektor;
- kondisi makroekonomi;
- atau peningkatan volatilitas umum.

Jika return setelah volume tinggi lebih besar, belum tentu volume itu sendiri menjadi penyebab langsung. Bisa saja volume tinggi merupakan penanda dari kondisi lain yang lebih luas.

Contoh:

Ketika volume meningkat, harga sering naik.

Kemungkinan penjelasan:

- Volume mencerminkan masuknya informasi baru.
- Volume muncul karena berita positif.
- Volume meningkat karena pasar sedang sangat volatil.
- Volume hanya menjadi indikator dari tren yang sudah berlangsung.
- Ada faktor lain yang tidak diukur.

TEKB dapat menemukan hubungan empiris, tetapi tidak boleh melampaui bukti yang tersedia.

### 24.2.3. Mengapa Desain Penelitian Menentukan Kesimpulan?

Kesimpulan harus disesuaikan dengan desain penelitian.

Jika desain penelitian hanya membandingkan B1 dan B0, kesimpulan yang wajar adalah:

> "B1 memiliki distribusi hasil yang berbeda dari B0 dalam populasi penelitian."

Kesimpulan yang terlalu jauh adalah:

> "B1 menyebabkan harga bergerak karena mekanisme tertentu."

Untuk mendukung klaim kausal, diperlukan desain yang lebih kuat, misalnya:

- kontrol terhadap faktor pengganggu;
- eksperimen atau quasi-experiment;
- identifikasi mekanisme;
- pengujian alternatif;
- analisis robustness;
- atau desain lain yang memang ditujukan untuk pertanyaan kausal.

TEKB dapat dikembangkan untuk penelitian yang lebih mendalam, tetapi tidak boleh mengklaim kausalitas hanya karena sebuah hubungan terlihat konsisten.

### 24.2.4. Jangan Mengubah Penanda Menjadi Penyebab

Kesalahan umum dalam membaca hasil penelitian adalah mengubah indikator atau penanda menjadi penyebab.

Contoh:

- "Volume tinggi menyebabkan harga naik."
- "Candle bearish menyebabkan reversal."
- "Breakout menyebabkan tren berlanjut."
- "Low supply menyebabkan kenaikan harga."

Kalimat-kalimat tersebut mungkin terlalu kuat jika penelitian hanya menunjukkan hubungan bersyarat.

Bahasa yang lebih hati-hati:

- "Volume tinggi berkaitan dengan perubahan distribusi return."
- "Candle bearish dalam kondisi tertentu diikuti oleh kecenderungan reversal."
- "Breakout menunjukkan karakteristik hasil yang berbeda dari B0."
- "Kondisi low supply berkaitan dengan hasil yang lebih baik dalam populasi penelitian."

Bahasa ini bukan berarti penelitian menjadi lemah. Justru, bahasa tersebut menunjukkan bahwa peneliti memahami batas inferensi.

### 24.2.5. Apa yang Dapat Disimpulkan TEKB?

Dalam desain standar, TEKB dapat membantu menjawab:

- Apakah suatu kondisi muncul secara berulang?
- Berapa banyak event yang memenuhi kondisi tersebut?
- Bagaimana distribusi return setelah kondisi muncul?
- Bagaimana MAE dan MFE-nya?
- Apakah B1 berbeda dari B0?
- Apakah perbedaan cukup besar?
- Apakah hasil cukup stabil dalam bootstrap?
- Apakah kandidat bertahan pada OOS?
- Apakah hasil masih relevan setelah friksi tertentu?

TEKB tidak otomatis dapat menjawab:

- Apakah kondisi tersebut satu-satunya penyebab pergerakan harga?
- Apakah hubungan tersebut berlaku untuk semua pasar?
- Apakah hasil akan tetap sama selamanya?
- Apakah setiap transaksi dapat dieksekusi pada harga teoritis?
- Apakah hasil tersebut bebas dari semua faktor pengganggu?

---

## 24.3. Data dan Definisi Menentukan Hasil

### 24.3.1. Data yang Salah Dapat Menghasilkan Kesimpulan yang Salah

Penelitian berbasis data sangat bergantung pada kualitas data.

Jika data salah, proses statistik yang sangat canggih tetap dapat menghasilkan kesimpulan yang salah.

Masalah data dapat berupa:

- timestamp keliru;
- bar duplikat;
- missing bar;
- volume salah;
- harga tidak disesuaikan;
- corporate action tidak ditangani;
- data survivorship-biased;
- instrumen yang sudah tidak aktif dihilangkan;
- OHLC tidak konsisten;
- atau data berasal dari sumber yang tidak sesuai kebutuhan penelitian.

Contoh sederhana:

Jika volume sebuah bar tercatat 10 kali lebih besar dari nilai sebenarnya, RV dapat terlihat sebagai anomali. Event SAMSON dapat terdeteksi secara keliru. Kesalahan tersebut kemudian dapat merambat ke:

- jumlah event;
- pemilihan B0;
- distribusi return;
- MAE/MFE;
- kandidat SL/TP;
- dan kesimpulan akhir.

Karena itu, pemeriksaan data bukan pekerjaan tambahan. Pemeriksaan data adalah bagian dari penelitian.

### 24.3.2. Data yang Tersedia Tidak Selalu Data yang Boleh Digunakan

Sebuah data mungkin tersedia secara teknis, tetapi tidak boleh digunakan untuk keputusan pada waktu tertentu.

Contohnya:

- data close belum final ketika keputusan dibuat;
- volume akhir sesi belum diketahui;
- data hasil revisi baru tersedia setelah waktu event;
- data corporate action diterapkan secara tidak tepat;
- atau indikator dihitung menggunakan bar masa depan.

TEKB harus membedakan:

- data tersedia secara teknis;
- data tersedia pada waktu keputusan;
- data valid menurut kontrak penelitian;
- dan data yang boleh digunakan tanpa look-ahead.

No-look-ahead berarti penelitian hanya boleh menggunakan informasi yang secara logis tersedia pada waktu keputusan.

### 24.3.3. Entry yang Tidak Kausal Dapat Merusak Penelitian

Definisi entry harus mengikuti urutan waktu yang dapat dilakukan.

Misalnya, jika sinyal baru diketahui setelah candle ditutup, maka entry pada harga close candle tersebut mungkin tidak dapat dilakukan secara kausal, kecuali ada mekanisme eksekusi yang memang mendukungnya.

Karena itu, TEKB menggunakan aturan seperti:

- signal pada close T;
- entry pada open bar berikutnya;
- atau NEXT_VALID_BAR_OPEN.

Jika entry ditetapkan pada harga yang sebenarnya belum diketahui atau tidak dapat dieksekusi pada saat sinyal muncul, hasil penelitian dapat menjadi terlalu optimistis.

Contoh masalah:

- menggunakan close final sebagai harga entry sebelum candle selesai;
- menggunakan low atau high masa depan untuk menentukan entry;
- menghapus event yang mengalami gap hanya karena harga entry aktual tidak nyaman;
- atau menggunakan harga ideal yang tidak tersedia di pasar.

Entry bukan detail kecil. Entry menentukan dasar seluruh pengukuran:

- return;
- MAE;
- MFE;
- SL/TP;
- biaya;
- dan hasil akhir.

### 24.3.4. B0 yang Tidak Adil Dapat Menciptakan Edge Palsu

B0 berfungsi sebagai pembanding. Jika B0 dipilih secara tidak adil, perbedaan B1-B0 dapat menjadi artefak metodologi.

Contoh B0 yang bermasalah:

- B0 dipilih berdasarkan hasil yang sudah diketahui;
- B0 hanya mengambil hari dengan kondisi pasar yang menguntungkan;
- B0 berasal dari periode yang berbeda secara sistematis;
- B0 memiliki distribusi volatilitas yang tidak sebanding;
- B0 menggunakan aturan entry yang berbeda;
- satu event B0 digunakan berulang kali tanpa aturan yang jelas;
- atau event B0 dipilih setelah melihat outcome.

Jika B0 terlalu buruk, B1 akan terlihat hebat meskipun sebenarnya tidak memiliki informasi tambahan.

Karena itu, B0 harus ditentukan dengan aturan yang:

- jelas;
- ditetapkan sebelum evaluasi outcome;
- konsisten;
- dapat diulang;
- dan sebanding dengan B1.

Perbedaan yang baik bukan sekadar perbedaan angka. Perbedaan harus berasal dari pembanding yang adil.

### 24.3.5. Evaluasi yang Tidak Konsisten Dapat Mengubah Hasil

Evaluation Engine menentukan bagaimana perjalanan harga diterjemahkan menjadi outcome.

Perbedaan aturan evaluasi dapat mengubah hasil secara signifikan.

Contohnya:

- evaluasi dimulai pada bar entry atau bar setelah entry;
- gap-through dianggap exit pada open atau level target;
- same-bar SL/TP dianggap TP, SL, atau ambigu;
- timeout dibedakan atau dicampur dengan horizon tidak lengkap;
- biaya diterapkan atau tidak;
- max hold berbeda;
- atau harga intrabar ditafsirkan terlalu pasti.

Jika B1 dan B0 dievaluasi dengan aturan berbeda, perbandingan menjadi tidak sahih.

B1 dan B0 harus melewati mesin evaluasi yang sama, dengan versi yang dapat diketahui dan diaudit.

### 24.3.6. Kesalahan pada Satu Tahap Dapat Merambat ke Tahap Berikutnya

Kesalahan penelitian sering bersifat berantai.

Contoh:

Data volume salah
↓
RV salah
↓
Event SAMSON salah
↓
Entry salah
↓
B0 salah atau tidak sebanding
↓
MAE/MFE salah
↓
SL/TP salah
↓
Expectancy salah
↓
Kesimpulan edge salah


Karena itu, semakin jauh sebuah kesimpulan dari data mentah, semakin penting audit trail dan pemeriksaan antar-tahap.

TEKB tidak boleh hanya memeriksa angka akhir. Sistem harus mampu memeriksa apakah setiap tahap menerapkan aturan yang benar.

---

## 24.4. Asumsi yang Masih Harus Dibaca secara Kritis

Tidak semua bagian metodologi memiliki status yang sama.

Ada aturan yang telah dikunci dan tidak boleh berubah selama penelitian. Ada asumsi yang dikonfigurasi berdasarkan kebutuhan penelitian. Ada pula hal yang masih terbuka dan membutuhkan eksperimen lebih lanjut.

Pembaca harus mengetahui perbedaan tersebut agar tidak menganggap semua angka memiliki tingkat kepastian metodologis yang sama.

### 24.4.1. ATR Period

ATR membutuhkan periode perhitungan, misalnya 14 bar.

Periode ATR memengaruhi:

- ukuran unit volatilitas;
- normalisasi MAE/MFE;
- jarak kandidat SL/TP;
- dan interpretasi besar kecilnya pergerakan.

ATR periode 14 dan ATR periode 20 dapat menghasilkan nilai yang berbeda. Akibatnya, SL 1 ATR pada kedua versi tersebut tidak selalu mewakili ruang risiko yang sama.

Jika periode ATR belum dibuktikan sebagai pilihan terbaik, periode tersebut harus diperlakukan sebagai asumsi metodologis atau konfigurasi yang perlu diuji, bukan sebagai kebenaran universal.

Pertanyaan kritis:

- Mengapa periode tersebut dipilih?
- Apakah pilihan dibuat sebelum melihat hasil?
- Apakah hasil sensitif terhadap perubahan periode?
- Apakah periode yang sama digunakan untuk B1 dan B0?
- Apakah ATR dihitung hanya dari informasi yang tersedia sebelum entry?

### 24.4.2. Grid Kandidat

Candidate grid menentukan ruang kandidat yang diuji.

Misalnya:

- SL 0,5; 1; 1,5 ATR;
- TP 1; 1,5; 2; 3 ATR;
- max hold 3; 5; 10 bar.

Grid yang terlalu sempit dapat melewatkan kandidat yang relevan. Grid yang terlalu luas dapat meningkatkan multiple testing dan peluang menemukan hasil positif secara kebetulan.

Pertanyaan kritis:

- Mengapa rentang grid tersebut dipilih?
- Apakah grid ditentukan sebelum seleksi?
- Apakah grid diperluas setelah melihat hasil?
- Berapa banyak kandidat yang diuji?
- Apakah seluruh kandidat tercatat dalam research batch?
- Apakah hasil telah disesuaikan dengan banyaknya pengujian?

Grid bukan sekadar pengaturan teknis. Grid adalah bagian dari ruang pencarian penelitian.

### 24.4.3. Friction Ladder

Friction ladder adalah rangkaian asumsi biaya dan friksi, misalnya:

- biaya nol;
- biaya dasar;
- biaya lebih realistis;
- biaya konservatif;
- atau skenario slippage tertentu.

Friction ladder membantu melihat apakah hasil hanya tampak baik ketika biaya diabaikan.

Namun, friction ladder tetap bergantung pada asumsi:

- biaya broker;
- spread;
- slippage;
- pajak;
- likuiditas;
- ukuran order;
- dan kondisi pasar.

Pertanyaan kritis:

- Apakah biaya yang digunakan realistis?
- Apakah biaya sama untuk semua instrumen?
- Apakah slippage tetap atau bergantung pada volatilitas?
- Apakah biaya diterapkan pada entry dan exit?
- Apakah kandidat hanya lolos pada skenario biaya yang terlalu optimistis?

Hasil yang hanya bertahan pada friction nol perlu ditafsirkan dengan sangat hati-hati.

### 24.4.4. Declustering

Declustering digunakan untuk mengurangi dominasi event yang terlalu berdekatan atau berasal dari episode pasar yang sama.

Declustering dapat menentukan:

- jarak minimum antar-event;
- apakah event berikutnya dalam episode yang sama dikeluarkan;
- apakah satu event menjadi representasi episode;
- dan bagaimana event yang berdekatan diperlakukan.

Declustering membantu mengurangi ketergantungan, tetapi tidak ada satu nilai declustering yang otomatis benar untuk semua hipotesis.

Declustering terlalu ketat dapat membuang informasi. Declustering terlalu longgar dapat membuat jumlah event terlihat besar padahal banyak event berasal dari episode yang sama.

Pertanyaan kritis:

- Apa alasan pemilihan radius decluster?
- Apakah radius sama untuk semua timeframe?
- Apakah declustering dilakukan sebelum evaluasi outcome?
- Apakah aturan diterapkan sama pada B1 dan B0?
- Apakah hasil sensitif terhadap perubahan radius?

### 24.4.5. Max Hold

Max hold menentukan berapa lama event atau posisi diamati sebelum dianggap selesai karena batas waktu.

Contohnya:

- 3 bar;
- 5 bar;
- 10 bar;
- atau horizon tertentu.

Max hold memengaruhi:

- peluang TP tercapai;
- peluang SL tercapai;
- jumlah timeout;
- return akhir;
- MAE/MFE;
- dan expectancy.

Max hold yang terlalu pendek mungkin tidak memberi waktu bagi pola untuk berkembang. Max hold yang terlalu panjang dapat membuat hasil dipengaruhi kondisi pasar yang sudah jauh dari konteks awal event.

Pertanyaan kritis:

- Mengapa max hold dipilih?
- Apakah pilihan tersebut ditetapkan sebelum seleksi?
- Apakah max hold sama untuk B1 dan B0?
- Apakah max hold sesuai dengan tujuan hipotesis?
- Apakah hasil berubah secara besar jika max hold diganti?

### 24.4.6. Definisi Baseline

Baseline digunakan untuk membandingkan kondisi saat ini dengan kondisi referensi.

Dalam SAMSON, misalnya, RV bergantung pada baseline volume. Baseline dapat berupa:

- rata-rata historis;
- median;
- baseline berdasarkan session;
- baseline berdasarkan slot waktu;
- atau metode lain.

Definisi baseline memengaruhi apakah suatu volume dianggap normal atau ekstrem.

Baseline yang mencampur session berbeda dapat menghasilkan sinyal yang keliru karena volume pagi dan siang mungkin memiliki karakteristik berbeda.

Pertanyaan kritis:

- Apakah baseline session-aware?
- Apakah baseline slot-aware?
- Apakah baseline menggunakan data masa lalu saja?
- Apakah baseline terpengaruh oleh event ekstrem sebelumnya?
- Apakah baseline sama untuk seluruh instrumen?
- Apakah baseline stabil ketika kondisi pasar berubah?

### 24.4.7. Pilihan Horizon

Horizon menentukan kapan hasil diukur.

Contoh:

- return satu bar berikutnya;
- R3;
- R5;
- R10;
- atau horizon berbasis waktu.

Horizon yang berbeda dapat menghasilkan kesimpulan yang berbeda.

Sebuah kondisi dapat:

- menghasilkan reversal pada satu bar;
- tetapi continuation dalam lima bar;
- atau tidak memiliki perbedaan berarti pada sepuluh bar.

Karena itu, horizon harus dikaitkan dengan hipotesis.

Pertanyaan kritis:

- Mengapa horizon tersebut dipilih?
- Apakah horizon primer ditentukan sebelum pengujian?
- Apakah banyak horizon diuji?
- Apakah hasil terbaik dipilih setelah melihat data?
- Apakah horizon sesuai dengan tujuan penggunaan?

Horizon bukan hanya pilihan teknis. Horizon menentukan pertanyaan apa yang sebenarnya dijawab oleh penelitian.

### 24.4.8. Asumsi Execution

Hasil penelitian dapat sangat dipengaruhi oleh asumsi eksekusi.

Asumsi tersebut dapat mencakup:

- entry pada open bar berikutnya;
- kemampuan memperoleh harga open;
- perlakuan gap;
- spread;
- slippage;
- ukuran order;
- likuiditas;
- partial fill;
- latency;
- dan kemampuan keluar ketika level tercapai.

Harga teoritis dalam data tidak selalu sama dengan harga yang dapat diperoleh trader.

Misalnya, jika sebuah strategi menghasilkan edge kecil sebesar 0,05R, tetapi spread dan slippage rata-rata mencapai 0,08R, edge tersebut mungkin tidak dapat digunakan secara praktis.

Pertanyaan kritis:

- Apakah harga entry realistis?
- Apakah exit dapat dilakukan?
- Apakah gap ditangani?
- Apakah biaya diterapkan secara konsisten?
- Apakah asumsi eksekusi cocok dengan instrumen dan timeframe?
- Apakah ukuran transaksi dapat ditampung oleh likuiditas?

---

## 24.5. Open Items dan Pengembangan Versi Berikutnya

### 24.5.1. Tidak Semua Pertanyaan Harus Dikunci Sekaligus

Sebuah sistem penelitian berkembang secara bertahap. Tidak semua pertanyaan metodologis dapat diselesaikan pada versi pertama.

Contoh hal yang mungkin masih terbuka:

- pilihan baseline alternatif;
- radius declustering yang paling sesuai;
- metode penanganan gap tertentu;
- model biaya yang lebih realistis;
- validasi pada instrumen tambahan;
- pengaruh regime pasar;
- horizon alternatif;
- atau metode bootstrap yang lebih sesuai.

Hal-hal tersebut tidak boleh disembunyikan. Sebaliknya, harus dicatat sebagai **open items**.

Open item berarti:

> "Pertanyaan ini belum diselesaikan atau belum dikunci dan membutuhkan penelitian lanjutan."

Open item bukan berarti sistem gagal. Open item menunjukkan bahwa peneliti memahami batas pengetahuan saat ini.

### 24.5.2. Perbedaan LOCKED, CONFIGURED ASSUMPTION, dan OPEN

Agar status metodologi jelas, TEKB dapat membedakan tiga kategori.

#### A. LOCKED

**LOCKED** berarti aturan telah dikunci untuk versi atau penelitian tertentu.

Contoh:

- definisi entry;
- aturan no-look-ahead;
- aturan B0;
- definisi MAE/MFE;
- aturan same-bar ambiguity;
- atau Evaluation Engine yang digunakan dalam satu batch frozen.

Aturan LOCKED tidak boleh diubah di tengah proses tanpa membuat versi atau penelitian baru.

#### B. CONFIGURED ASSUMPTION

**CONFIGURED ASSUMPTION** berarti nilai atau pilihan telah ditetapkan untuk penelitian, tetapi masih merupakan asumsi yang dapat diuji dalam penelitian lain.

Contoh:

- ATR period = 14;
- max hold = 5 bar;
- radius decluster = 3 bar;
- friction ladder tertentu;
- threshold RV = 5;
- atau grid SL/TP tertentu.

Asumsi tersebut harus dicatat, bukan disamarkan sebagai fakta universal.

Contoh penulisan:

> "Penelitian ini menggunakan ATR periode 14 sebagai konfigurasi yang telah ditetapkan. Pilihan periode tersebut belum dianggap sebagai parameter universal dan dapat diuji dalam eksperimen terpisah."

#### C. OPEN

**OPEN** berarti pertanyaan atau keputusan belum ditetapkan.

Contoh:

- apakah baseline median lebih baik daripada mean;
- apakah radius decluster perlu berbeda antar-session;
- apakah biaya sebaiknya dimodelkan berdasarkan ukuran order;
- apakah horizon tertentu lebih stabil pada regime tertentu.

Status OPEN mencegah peneliti menganggap pertanyaan yang belum diselesaikan sebagai sesuatu yang sudah final.

### 24.5.3. Contoh Daftar Status Metodologi

| Komponen | Status | Keterangan |
|---|---|---|
| Entry next valid bar open | LOCKED | Berlaku untuk protokol versi tertentu |
| B0 matching rule | LOCKED | Aturan pembanding telah dikunci |
| ATR period 14 | CONFIGURED ASSUMPTION | Digunakan dalam penelitian, belum universal |
| Max hold 5 bar | CONFIGURED ASSUMPTION | Perlu diuji pada eksperimen terpisah |
| Baseline median versus mean | OPEN | Belum diputuskan |
| Model slippage berdasarkan likuiditas | OPEN | Pengembangan berikutnya |

Tabel seperti ini membantu pembaca memahami mana yang merupakan hukum internal protokol, mana yang merupakan pilihan konfigurasi, dan mana yang masih menjadi pertanyaan penelitian.

### 24.5.4. Pengembangan Harus Dilakukan sebagai Eksperimen Baru

Jika sebuah aturan telah digunakan untuk menghasilkan hasil IS atau OOS, perubahan terhadap aturan tersebut tidak boleh dilakukan diam-diam di dalam penelitian yang sama.

Misalnya, setelah melihat OOS gagal, peneliti ingin:

- mengubah threshold;
- mengganti baseline;
- memperlebar grid;
- mengganti max hold;
- mengubah B0;
- atau mengubah definisi entry.

Perubahan tersebut dapat menjadi ide penelitian baru. Namun, hasilnya harus diberi:

- hypothesis ID baru atau versi yang jelas;
- research batch baru;
- attempt number;
- protocol hash baru;
- candidate grid version baru jika relevan;
- dan provenance yang menghubungkan penelitian baru dengan penelitian sebelumnya.

Dengan cara ini, pengembangan tetap transparan.

### 24.5.5. Mengapa Perubahan Metodologi Harus Memiliki Versi?

Perubahan metodologi dapat mengubah hasil. Jika versi tidak dicatat, peneliti tidak dapat mengetahui apakah perbedaan hasil berasal dari:

- perubahan data;
- perubahan aturan;
- perubahan kode;
- perubahan asumsi;
- atau perubahan kondisi pasar.

Contoh:

**Versi 1:**
- Entry: next valid bar open
- ATR: Wilder, n=14
- B0: same slot, nearest valid day
- Max hold: 5 bar

**Versi 2:**
- Entry: next valid bar open
- ATR: Wilder, n=20
- B0: same slot, nearest valid day
- Max hold: 10 bar

Walaupun nama hipotesisnya sama, hasil versi 1 dan versi 2 tidak boleh dianggap identik. Perubahan ATR dan max hold dapat mengubah seluruh distribusi hasil.

Karena itu, setiap perubahan penting harus memiliki:

- versi;
- alasan perubahan;
- tanggal perubahan;
- pihak atau proses yang melakukan perubahan;
- hasil sebelum perubahan;
- hasil setelah perubahan;
- dan hubungan provenance antara keduanya.

### 24.5.6. Open Item Bukan Alasan untuk Mengubah Hasil Lama

Jika sebuah pertanyaan masih terbuka, peneliti tidak boleh mengubah hasil lama agar sesuai dengan jawaban baru.

Misalnya, penelitian awal menggunakan ATR 14. Kemudian muncul dugaan bahwa ATR 20 lebih baik.

Cara yang benar:

1. Pertahankan hasil ATR 14 sebagai hasil versi lama.
2. Buat eksperimen baru untuk ATR 20.
3. Catat bahwa ATR 20 merupakan konfigurasi atau hipotesis baru.
4. Bandingkan hasil secara transparan.
5. Jika diperlukan, buat protokol baru.

Jangan menghapus hasil lama hanya karena hasil baru terlihat lebih baik.

Dengan cara ini, sejarah penelitian tetap terjaga dan risiko data snooping dapat dikendalikan.

### 24.5.7. Arah Pengembangan TEKB

Pengembangan TEKB dapat diarahkan pada beberapa area:

#### A. Peningkatan Kualitas Data

- pemeriksaan data otomatis;
- deteksi bar duplikat;
- pemeriksaan timestamp;
- validasi OHLC;
- penanganan corporate action;
- dan peningkatan provenance sumber data.

#### B. Pengujian Robustness

- perubahan horizon;
- variasi baseline;
- variasi declustering;
- variasi friction;
- variasi populasi;
- dan analisis sensitivitas.

#### C. Peningkatan Model Eksekusi

- spread;
- slippage;
- gap;
- partial fill;
- likuiditas;
- dan ukuran transaksi.

#### D. Pengujian Generalisasi

- instrumen lain;
- periode lain;
- regime pasar lain;
- pasar berbeda;
- dan OOS yang benar-benar belum digunakan.

#### E. Peningkatan Audit dan Reproduksibilitas

- immutable ledger;
- protocol hash;
- versioned datasets;
- event lineage;
- computation ID;
- dan laporan otomatis yang lengkap.

#### F. Pengembangan ke Aplikasi

Aplikasi TEKB dapat menampilkan hasil penelitian sebagai informasi pendukung, tetapi aplikasi tidak boleh menyembunyikan:

- ketidakpastian;
- jumlah event;
- perbandingan B0;
- biaya;
- status OOS;
- batasan;
- dan versi metodologi.

Pengembangan aplikasi harus mengikuti hasil penelitian yang telah diaudit, bukan menggantikan penelitian dengan tampilan sinyal yang menarik.

---

## Ringkasan Bab

TEKB adalah sistem penelitian yang membantu manusia memahami bukti dari data, tetapi TEKB memiliki batasan yang harus selalu diingat.

Pokok-pokok penting bab ini adalah:

- **TEKB tidak menjamin profit**
  - Hasil historis dapat berubah, dan hasil positif tidak menghapus risiko.
- **TEKB tidak otomatis membuktikan kausalitas**
  - Conditional association menunjukkan hubungan bersyarat, bukan otomatis hubungan sebab-akibat.
- **Data dan definisi menentukan hasil**
  - Data yang salah, entry yang tidak kausal, B0 yang tidak adil, atau evaluasi yang tidak konsisten dapat menghasilkan edge palsu.
- **Asumsi harus dibaca secara kritis**
  - ATR period, candidate grid, friction ladder, declustering, max hold, baseline, horizon, dan execution assumption dapat memengaruhi kesimpulan.
- **Status metodologi harus jelas**
  - Bedakan LOCKED, CONFIGURED ASSUMPTION, dan OPEN.
- **Hasil gagal dan pertanyaan terbuka harus dipertahankan**
  - Keduanya merupakan bagian dari pengetahuan penelitian.
- **Pengembangan harus menjadi eksperimen baru**
  - Perubahan aturan memerlukan versi, provenance, dan pencatatan yang jelas.

Prinsip penutup bab ini:

> Kekuatan TEKB bukan terletak pada kemampuannya menghapus ketidakpastian, melainkan pada kemampuannya mencegah ketidakpastian disamarkan sebagai kepastian.

TEKB yang matang tidak berkata bahwa pasar dapat diprediksi dengan sempurna. TEKB berkata bahwa setiap klaim harus dibatasi oleh data, aturan, pengukuran, pembanding, ketidakpastian, dan bukti generalisasi yang tersedia.

Dengan sikap tersebut, TEKB tidak menjadi mesin untuk membenarkan keyakinan trading. TEKB menjadi disiplin untuk menguji keyakinan tersebut.

---

## Pertanyaan Refleksi

1. Mengapa TEKB tidak dapat menjamin profit?
2. Mengapa distribusi historis dapat berubah?
3. Mengapa hasil positif tidak menghapus risiko?
4. Apa perbedaan antara conditional association dan kausalitas?
5. Mengapa TEKB tidak otomatis membuktikan kausalitas?
6. Mengapa data yang salah dapat menghasilkan kesimpulan yang salah?
7. Mengapa data yang tersedia belum tentu boleh digunakan?
8. Mengapa entry yang tidak kausal dapat merusak penelitian?
9. Mengapa B0 yang tidak adil dapat menciptakan edge palsu?
10. Apa perbedaan LOCKED, CONFIGURED ASSUMPTION, dan OPEN?
11. Mengapa pengembangan harus dilakukan sebagai eksperimen baru?
12. Mengapa open item bukan alasan untuk mengubah hasil lama?

---

## Kalimat Kunci

> Kekuatan TEKB bukan terletak pada kemampuannya menghapus ketidakpastian, melainkan pada kemampuannya mencegah ketidakpastian disamarkan sebagai kepastian. TEKB yang matang tidak berkata bahwa pasar dapat diprediksi dengan sempurna, melainkan bahwa setiap klaim harus dibatasi oleh data, aturan, pengukuran, pembanding, ketidakpastian, dan bukti generalisasi yang tersedia.

---

<div align="center">

[← Bab Sebelumnya](/posts/bab-23-audit-trail/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Bab Selanjutnya →](/posts/bab-25-tekb-disiplin-berpikir/)

</div>