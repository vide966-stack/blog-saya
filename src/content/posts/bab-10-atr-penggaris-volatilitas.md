---
title: "BAB 10 — ATR: Penggaris Volatilitas, Bukan Bola Kristal"
published: 2026-09-12
description: "ATR adalah penggaris volatilitas, bukan alat ramalan arah. Bab ini menjelaskan True Range, Wilder's smoothing, dan mengapa ATR_entry harus dihitung sebelum entry."
tags: ["bab-10", "atr", "volatilitas", "pengukuran"]
category: "Bab"
draft: false
lang: ""
---

**BAGIAN III — MENGUKUR HASIL TANPA MENIPU DIRI SENDIRI**

---

Dalam penelitian trading, kita sering ingin membandingkan pergerakan harga setelah suatu event. Misalnya, kita ingin mengetahui apakah harga bergerak cukup jauh setelah event SAMSON, apakah stop-loss tertentu terlalu dekat, atau apakah target keuntungan tertentu realistis.

Namun, ada masalah: harga setiap saham memiliki skala dan karakteristik pergerakan yang berbeda.

Pergerakan Rp100 pada satu saham belum tentu memiliki arti yang sama dengan pergerakan Rp100 pada saham lainnya. Bahkan pada saham yang sama, pergerakan Rp100 dapat memiliki arti berbeda ketika pasar sedang tenang dibandingkan ketika pasar sedang sangat volatil.

Karena itu, TEKB membutuhkan satuan pengukuran yang lebih kontekstual. Salah satu alat yang digunakan adalah **Average True Range**, atau **ATR**.

ATR membantu menjawab pertanyaan:

> "Seberapa besar harga biasanya bergerak dalam kondisi pasar yang sedang diamati?"

ATR bukan alat untuk menebak apakah harga akan naik atau turun. ATR adalah **penggaris volatilitas** — alat untuk mengukur besar kecilnya pergerakan harga secara lebih adil.

---

## 10.1. Mengapa Harga Mentah Sulit Dibandingkan?

Bayangkan terdapat dua saham:

- Saham A bergerak dari Rp1.000 ke Rp1.100.
- Saham B bergerak dari Rp10.000 ke Rp10.100.

Keduanya sama-sama bergerak Rp100. Namun, secara relatif:

- Saham A naik 10%.
- Saham B hanya naik 1%.

Jika kita hanya melihat rupiah, kedua pergerakan tampak sama. Padahal, dampaknya terhadap harga dan risiko sangat berbeda.

Masalah yang sama muncul ketika kita membandingkan pergerakan antarperiode atau antarsaham.

### Pergerakan Rp100 Tidak Selalu Memiliki Arti yang Sama

Pergerakan Rp100 pada saham berharga Rp1.000 berarti 10%. Pergerakan Rp100 pada saham berharga Rp10.000 berarti 1%.

Dengan demikian, angka nominal tidak cukup untuk menjelaskan seberapa besar pergerakan tersebut.

Namun, persentase saja juga belum selalu memadai untuk kebutuhan penelitian. Kita juga perlu memahami karakteristik pergerakan harga dalam satuan harga aktual, terutama ketika mengukur:

- jarak stop-loss;
- jarak target;
- MAE;
- MFE;
- rentang pergerakan intraday;
- atau kemampuan harga mencapai level tertentu.

### Saham Volatil dan Saham Stabil

Misalnya, dua saham sama-sama memiliki harga Rp5.000.

- Saham A biasanya bergerak Rp50 dalam satu hari.
- Saham B biasanya bergerak Rp300 dalam satu hari.

Jika kita menetapkan stop-loss Rp100 untuk keduanya, aturan tersebut tidak memiliki makna yang sama.

Pada Saham A, jarak Rp100 mungkin sudah dua kali pergerakan harian yang umum. Pada Saham B, jarak Rp100 mungkin terlalu sempit dan mudah tersentuh oleh fluktuasi normal.

Karena itu, jarak harga sebaiknya dipahami dalam konteks volatilitas instrumen tersebut.

### Mengapa Perbandingan Mentah Bisa Tidak Adil?

Jika penelitian hanya menggunakan angka rupiah mentah, hasilnya dapat dipengaruhi oleh:

- harga nominal saham;
- karakteristik volatilitas;
- perubahan rezim pasar;
- perbedaan instrumen;
- dan kondisi pasar saat event terjadi.

Contohnya, MAE sebesar Rp100 mungkin terlihat besar pada saham yang tenang, tetapi kecil pada saham yang sangat aktif. Tanpa konteks volatilitas, peneliti dapat salah menilai risiko atau peluang.

ATR membantu menyediakan satuan yang lebih kontekstual sehingga pergerakan dapat dinyatakan, misalnya:

- MAE sebesar 0,5 × ATR;
- MFE sebesar 1,2 × ATR;
- stop-loss sebesar 1,0 × ATR;
- target keuntungan sebesar 2,0 × ATR.

Dengan satuan tersebut, pergerakan harga lebih mudah dibandingkan dalam konteks karakteristik pergerakan masing-masing instrumen.

---

## 10.2. Apa Itu Volatilitas?

Volatilitas adalah ukuran tentang seberapa besar harga biasanya bergerak dalam suatu periode.

Volatilitas **tidak menjelaskan arah** pergerakan. Volatilitas hanya menjelaskan besar kecilnya gerakan.

Harga dapat bergerak:

- naik dengan volatilitas tinggi;
- turun dengan volatilitas tinggi;
- bergerak naik-turun dengan volatilitas tinggi;
- atau bergerak sedikit dengan volatilitas rendah.

Jadi, volatilitas menjawab pertanyaan:

> "Seberapa besar harga bergerak?"

Bukan:

> "Ke mana harga akan bergerak?"

### Analogi Jalan Tenang dan Jalan Bergelombang

Bayangkan dua kendaraan berjalan di dua jalan yang berbeda.

Jalan pertama tenang dan rata. Kendaraan bergerak relatif stabil dengan sedikit guncangan.

Jalan kedua bergelombang dan penuh perubahan. Kendaraan sering bergerak naik-turun dan mengalami guncangan besar.

Kita dapat menyebut jalan kedua lebih "volatil" dalam arti pergerakannya lebih besar dan tidak tenang.

Namun, analogi ini tidak memberi tahu apakah kendaraan akan menuju utara atau selatan. Jalan yang bergelombang dapat dilalui ke arah mana pun.

Begitu pula dengan harga:

- volatilitas tinggi tidak berarti harga akan naik;
- volatilitas rendah tidak berarti harga akan turun;
- volatilitas tinggi tidak otomatis berarti peluang lebih baik;
- volatilitas rendah tidak otomatis berarti risiko lebih kecil dalam semua konteks.

Volatilitas hanya memberi konteks tentang ukuran gerakan.

### Volatilitas Bukan Arah

Misalnya, harga bergerak dari Rp5.000 ke Rp4.700. Pergerakannya cukup besar. Ini menunjukkan adanya volatilitas, tetapi arah pergerakannya adalah turun.

Pada hari lain, harga bergerak dari Rp5.000 ke Rp5.300. Pergerakannya juga besar, tetapi arahnya naik.

ATR dapat membantu mengukur bahwa kedua hari tersebut memiliki rentang pergerakan yang besar. ATR sendiri tidak menyimpulkan bahwa salah satunya lebih bullish atau bearish.

Dalam TEKB, arah dan besar gerakan dipisahkan:

- event atau kondisi penelitian dapat berkaitan dengan informasi tertentu;
- return mengukur hasil arah;
- ATR membantu menyatakan ukuran gerakan;
- MAE dan MFE mengukur perjalanan harga setelah entry.

Pemisahan ini penting agar ATR tidak diberi tugas yang bukan fungsinya.

---

## 10.3. Apa Itu True Range?

Sebelum memahami ATR, kita perlu memahami **True Range**, atau **TR**.

Secara sederhana, True Range adalah ukuran rentang pergerakan harga yang berusaha menangkap pergerakan aktual suatu bar, termasuk kemungkinan adanya gap dari harga penutupan sebelumnya.

Jika kita hanya menggunakan:

> High − Low

kita hanya melihat rentang harga di dalam bar tersebut.

Padahal, harga dapat dibuka jauh di atas atau jauh di bawah penutupan sebelumnya. Pergerakan tersebut perlu ikut dipertimbangkan karena merupakan bagian dari risiko dan dinamika harga.

### Mengapa ATR Tidak Hanya Melihat High Dikurangi Low?

Misalnya, sebuah saham memiliki data:

- Close hari sebelumnya: Rp5.000
- Open hari ini: Rp5.300
- High hari ini: Rp5.400
- Low hari ini: Rp5.250
- Close hari ini: Rp5.350

Jika kita hanya menghitung High − Low:

> Rp5.400 − Rp5.250 = Rp150

Namun, harga dibuka dengan gap naik dari Rp5.000 ke Rp5.300. Rentang Rp150 tidak sepenuhnya menggambarkan perubahan harga yang dialami dibandingkan dengan penutupan sebelumnya.

True Range mempertimbangkan tiga kemungkinan rentang:

1. High − Low
2. |High − Close sebelumnya|
3. |Low − Close sebelumnya|

True Range adalah nilai terbesar dari ketiga perhitungan tersebut:

> TR_t = max(H_t − L_t, |H_t − C_t-1|, |L_t − C_t-1|)

Keterangan:

- H_t = harga tertinggi pada bar t;
- L_t = harga terendah pada bar t;
- C_t-1 = harga penutupan bar sebelumnya.

Simbol tersebut tidak perlu dihafalkan terlebih dahulu. Intinya adalah:

> True Range memilih rentang yang paling mampu menggambarkan pergerakan harga aktual, termasuk pengaruh gap.

### Contoh Gap Naik

Misalnya:

- Close sebelumnya = Rp1.000
- High hari ini = Rp1.150
- Low hari ini = Rp1.100

Maka:

- High − Low = Rp50
- |High − Close sebelumnya| = Rp150
- |Low − Close sebelumnya| = Rp100

True Range = Rp150.

Mengapa bukan Rp50? Karena harga tidak memulai hari dari Rp1.100 atau Rp1.150. Harga sebelumnya berada di Rp1.000, lalu pasar dibuka jauh lebih tinggi. Gap tersebut merupakan bagian penting dari pergerakan.

### Contoh Gap Turun

Misalnya:

- Close sebelumnya = Rp1.000
- High hari ini = Rp920
- Low hari ini = Rp800

Maka:

- High − Low = Rp120
- |High − Close sebelumnya| = Rp80
- |Low − Close sebelumnya| = Rp200

True Range = Rp200.

Dengan demikian, True Range menangkap bahwa jarak dari penutupan sebelumnya ke titik terendah hari ini lebih besar daripada rentang internal bar.

### Mengapa Gap Penting?

Gap dapat memengaruhi:

- risiko entry;
- jarak stop-loss;
- kemungkinan harga melewati level tertentu;
- kerugian atau keuntungan aktual;
- dan besar gerakan yang dialami trader.

Jika gap diabaikan, ukuran volatilitas dapat menjadi terlalu kecil dibandingkan pergerakan yang benar-benar terjadi.

Karena itu, ATR yang menggunakan True Range lebih informatif daripada ukuran yang hanya memakai High − Low.

---

## 10.4. Apa Itu ATR?

**Average True Range** (ATR) adalah rata-rata bergerak dari True Range dalam sejumlah periode tertentu.

Secara sederhana:

> ATR mengukur rata-rata besar rentang pergerakan harga, dengan mempertimbangkan gap.

Jika ATR sebuah saham adalah Rp100, maka secara historis, dalam definisi dan periode yang digunakan, ukuran True Range rata-ratanya berada di sekitar Rp100.

Namun, pernyataan ini harus dibaca dengan hati-hati. ATR bukan janji bahwa harga akan bergerak tepat Rp100 pada bar berikutnya.

### ATR sebagai Penggaris Volatilitas

Bayangkan kita ingin mengukur panjang beberapa benda. Jika kita tidak memiliki penggaris, kita mungkin menggunakan jengkal tangan. Namun, ukuran jengkal setiap orang berbeda.

ATR berfungsi seperti penggaris yang menyesuaikan dengan karakteristik pergerakan harga.

Dengan ATR, kita dapat menyatakan:

- pergerakan sebesar 0,5 × ATR;
- pergerakan sebesar 1,0 × ATR;
- pergerakan sebesar 2,0 × ATR.

Satuan ini membantu kita membandingkan gerakan secara lebih kontekstual.

Misalnya:

- Event A menghasilkan MFE sebesar 1,5 × ATR.
- Event B menghasilkan MFE sebesar 0,4 × ATR.

Walaupun nilai rupiahnya berbeda, kita dapat memahami bahwa event A menghasilkan gerakan yang lebih besar dibandingkan ukuran volatilitas lokalnya.

### ATR Bukan Prediksi Arah

ATR tidak mengatakan harga akan naik atau turun.

ATR sebesar Rp200 dapat terjadi ketika:

- harga naik tajam;
- harga turun tajam;
- harga naik lalu turun;
- harga turun lalu naik;
- atau harga mengalami gap besar.

ATR hanya mengukur skala pergerakan.

Jika peneliti menggunakan ATR sebagai dasar pengukuran, ia tetap membutuhkan definisi lain untuk mengukur arah, seperti return atau perubahan harga.

### ATR Bukan Jaminan Harga Akan Bergerak Sebesar Nilainya

Jika ATR = Rp100, bukan berarti:

- harga pasti bergerak Rp100;
- harga minimal bergerak Rp100;
- harga akan bergerak Rp100 ke arah yang menguntungkan;
- atau harga akan mencapai target 1 × ATR.

ATR adalah ukuran historis atau estimasi berbasis rentang sebelumnya. Harga berikutnya dapat bergerak:

- lebih kecil dari ATR;
- mendekati ATR;
- jauh lebih besar dari ATR;
- atau hampir tidak bergerak.

ATR tidak menjamin hasil pada bar berikutnya.

### ATR Bukan Sinyal BUY atau SELL

ATR tidak dirancang untuk menjawab:

- kapan harus membeli;
- kapan harus menjual;
- apakah tren sedang naik;
- apakah tren sedang turun;
- atau apakah suatu event memiliki information edge.

ATR hanya menyediakan unit pengukuran volatilitas.

Dalam arsitektur TEKB:

- SAMSON mendeteksi anomali volume;
- event dan aturan entry menentukan kapan pengukuran dimulai;
- return mengukur arah hasil;
- MAE dan MFE mengukur perjalanan harga;
- ATR menyatakan ukuran gerakan dalam konteks volatilitas;
- Evaluation Engine menentukan outcome berdasarkan aturan yang telah ditetapkan.

ATR tidak menggantikan komponen-komponen tersebut.

---

## 10.5. Mengapa TEKB Menggunakan Wilder's Smoothing?

ATR tidak hanya membutuhkan True Range. Nilai-nilai True Range tersebut perlu diringkas menjadi ukuran yang lebih stabil. Salah satu metode yang digunakan dalam definisi ATR TEKB adalah **Wilder's smoothing**, yaitu metode penghalusan yang diperkenalkan oleh J. Welles Wilder.

### Apa Arti Penghalusan?

Nilai True Range dapat berubah-ubah secara tajam dari satu bar ke bar berikutnya.

Misalnya:

- hari pertama: TR = Rp80;
- hari kedua: TR = Rp120;
- hari ketiga: TR = Rp90;
- hari keempat: TR = Rp300;
- hari kelima: TR = Rp70.

Jika kita hanya melihat nilai satu hari, ukuran volatilitas dapat berubah secara drastis. Penghalusan membantu menghasilkan ukuran yang tidak terlalu mudah berayun hanya karena satu nilai ekstrem.

Analogi sederhananya adalah mengukur suhu ruangan. Jika suhu diukur hanya dari satu detik, hasilnya dapat terlalu sensitif terhadap perubahan sesaat. Dengan melihat pola beberapa pengukuran, kita mendapatkan gambaran yang lebih stabil.

Wilder's smoothing memberi bobot pada informasi baru, tetapi tetap mempertahankan pengaruh informasi sebelumnya. Dengan demikian, ATR tidak sepenuhnya berubah hanya karena satu bar.

### Mengapa Metode Smoothing Harus Konsisten?

Ada berbagai cara untuk menghitung rata-rata atau menghaluskan data. Jika dua peneliti menggunakan metode yang berbeda, nilai ATR yang dihasilkan dapat berbeda meskipun memakai data harga yang sama.

Perbedaan tersebut kemudian dapat memengaruhi:

- nilai ATR_entry;
- MAE dalam satuan ×ATR;
- MFE dalam satuan ×ATR;
- jarak candidate SL/TP;
- hasil evaluasi;
- dan kesimpulan penelitian.

Karena itu, TEKB perlu menetapkan metode smoothing secara eksplisit.

Dalam penelitian, "ATR" saja belum cukup sebagai definisi lengkap. Peneliti juga perlu mengetahui:

- metode True Range yang digunakan;
- metode smoothing;
- periode ATR;
- waktu pengambilan ATR;
- serta bagaimana ATR diterapkan dalam pengukuran.

### Mengapa Definisi ATR Harus Dibekukan?

Jika definisi ATR dapat diubah setelah melihat hasil, peneliti dapat tanpa sadar menyesuaikan alat ukur agar hasil penelitian terlihat lebih baik.

Misalnya:

- pada satu percobaan menggunakan ATR periode 14;
- pada percobaan lain mengganti menjadi periode 7 karena menghasilkan distribusi yang lebih menarik;
- kemudian memilih hasil yang paling menguntungkan tanpa memperhitungkan bahwa definisinya telah berubah.

Masalahnya bukan bahwa periode 7 atau 14 selalu salah. Masalahnya adalah perubahan definisi setelah melihat hasil dapat menjadi bentuk **data snooping** atau **researcher degrees of freedom**.

Karena itu, TEKB memperlakukan definisi ATR sebagai bagian dari kontrak penelitian:

- metode True Range ditentukan;
- Wilder's smoothing ditentukan;
- periode ATR ditentukan;
- waktu pengambilan ditentukan;
- dan definisi tersebut dibekukan untuk eksperimen yang sedang dijalankan.

Jika suatu hari definisi ATR ingin diubah, perubahan tersebut harus diperlakukan sebagai versi atau eksperimen baru, bukan diam-diam mengganti definisi lama.

---

## 10.6. ATR_entry: Mengapa Dihitung Sebelum Entry?

Dalam TEKB, waktu pengambilan ATR sangat penting. ATR tidak boleh dihitung menggunakan informasi yang baru diketahui setelah entry jika penelitian ingin menjaga prinsip no-look-ahead.

TEKB menggunakan konsep **ATR_entry**, yaitu nilai ATR yang dihitung berdasarkan informasi yang tersedia sebelum entry dilakukan.

### ATR Dihitung pada Close T

Misalkan:

- bar T adalah bar tempat sinyal atau event terdeteksi;
- bar T ditutup;
- entry dilakukan pada open bar T+1.

Dalam struktur ini, ATR_entry dihitung pada **close T**.

Artinya, semua informasi yang digunakan untuk menghitung ATR_entry sudah tersedia ketika bar T selesai.

Setelah close T, peneliti mengetahui:

- Open, High, Low, dan Close bar T;
- True Range bar-bar sebelumnya;
- serta nilai ATR berdasarkan data yang tersedia sampai close T.

Namun, peneliti belum menggunakan informasi dari bar T+1 atau bar-bar setelahnya.

### Entry Dilakukan pada Open T+1

Entry dilakukan pada open bar berikutnya, sesuai dengan aturan:

> Signal close → raw entry open T+1.

Dengan demikian, ATR_entry menjadi ukuran volatilitas yang tersedia sebelum harga entry diketahui secara aktual pada bar T+1.

Contoh:

- Close T = Rp5.000.
- ATR dihitung menggunakan data sampai close T.
- Open T+1 = Rp5.050.
- Entry raw = Rp5.050.

ATR_entry tetap merupakan ATR yang diketahui sebelum entry, bukan ATR yang dihitung setelah seluruh bar T+1 selesai.

### Mengapa Tidak Menggunakan ATR Setelah Trade Berjalan?

Jika ATR dihitung ulang setelah entry menggunakan data yang muncul selama trade, maka satuan pengukuran dapat berubah sepanjang trade.

Hal ini dapat menimbulkan masalah:

- jarak stop-loss seolah-olah berubah;
- target dapat berubah berdasarkan informasi masa depan;
- MAE/MFE dapat dinormalisasi dengan ukuran volatilitas yang belum tersedia saat entry;
- hasil antar-event menjadi sulit dibandingkan;
- dan evaluasi dapat tercampur dengan informasi setelah keputusan.

Dalam TEKB, ATR_entry digunakan sebagai ukuran tetap untuk trade tersebut.

### ATR Tetap Sepanjang Trade

Setelah ATR_entry ditetapkan, nilainya tidak berubah sepanjang horizon pengukuran trade.

Misalnya:

- ATR_entry = Rp100.
- MAE aktual = Rp70.
- MFE aktual = Rp180.

Maka:

- MAE dalam satuan ATR = 0,70 × ATR;
- MFE dalam satuan ATR = 1,80 × ATR.

Jika pada bar berikutnya ATR pasar meningkat menjadi Rp150, nilai ATR_entry untuk trade yang sedang diukur tetap Rp100.

Hal ini menjaga konsistensi:

> Satuan pengukuran ditentukan sebelum trade berjalan dan tidak disesuaikan berdasarkan perjalanan harga setelah entry.

ATR_entry bukan berarti volatilitas pasar tidak berubah. Volatilitas dapat berubah. Yang tetap adalah satuan pengukuran yang telah ditetapkan untuk event tersebut.

---

## 10.7. ATR_period_n dan Statusnya

ATR membutuhkan parameter periode, yang biasa disebut **ATR_period_n**.

Parameter ini menentukan berapa banyak informasi historis yang digunakan dalam proses pengukuran ATR.

Dalam konfigurasi awal TEKB:

> ATR_period_n = 14

Artinya, definisi awal ATR menggunakan periode 14 sesuai metode yang telah ditetapkan dalam kontrak penelitian.

### Mengapa Menggunakan Angka 14?

Angka 14 merupakan pilihan konfigurasi awal yang umum digunakan dalam banyak penerapan ATR. Angka ini menyediakan kompromi praktis antara:

- terlalu sensitif terhadap perubahan jangka pendek;
- dan terlalu lambat mengikuti perubahan volatilitas.

Namun, penggunaan angka 14 dalam TEKB bukan klaim bahwa 14 adalah angka paling optimal untuk semua saham, semua timeframe, dan semua kondisi pasar.

Angka tersebut adalah asumsi konfigurasi yang ditetapkan agar penelitian memiliki definisi yang konsisten.

### Status CONFIGURED ASSUMPTION

Dalam dokumentasi TEKB, ATR_period_n = 14 diberi status:

> CONFIGURED ASSUMPTION

Artinya, angka 14 merupakan asumsi atau konfigurasi yang dipilih untuk menjalankan penelitian, bukan hasil pembuktian bahwa angka tersebut pasti terbaik.

Perbedaan ini sangat penting.

Ada dua pernyataan yang berbeda:

1. "Kami menggunakan ATR periode 14 sebagai konfigurasi penelitian."
2. "ATR periode 14 terbukti paling optimal untuk menghasilkan keuntungan."

Pernyataan pertama adalah dokumentasi metode. Pernyataan kedua adalah klaim empiris yang membutuhkan penelitian tersendiri.

TEKB tidak boleh mengubah konfigurasi menjadi klaim keunggulan tanpa bukti.

### Mengapa ATR_period_n Tidak Dioptimasi Bersama Grid SL/TP?

Dalam TEKB, candidate SL/TP dapat diuji menggunakan grid tertentu, misalnya:

- stop-loss 0,5 × ATR;
- stop-loss 1,0 × ATR;
- target 1,0 × ATR;
- target 2,0 × ATR;
- dan seterusnya.

Namun, ATR_period_n tidak boleh diam-diam ikut dioptimasi bersama grid SL/TP jika desain penelitian menetapkannya sebagai konfigurasi tetap.

Jika periode ATR, stop-loss, dan target semuanya diubah-ubah lalu dipilih berdasarkan hasil terbaik, jumlah percobaan menjadi lebih besar. Hal ini meningkatkan risiko menemukan hasil yang tampak bagus hanya karena banyak pilihan telah dicoba.

Karena itu:

- ATR_period_n ditetapkan sebagai konfigurasi;
- definisi ATR dibekukan;
- grid candidate SL/TP diuji di atas satuan ATR yang sama;
- dan perubahan periode ATR diperlakukan sebagai eksperimen atau versi penelitian tersendiri.

Jika TEKB suatu saat ingin membandingkan ATR periode 7, 14, 21, dan 28, maka perbandingan tersebut harus dirancang sebagai penelitian baru dengan dokumentasi:

- hipotesis;
- versi definisi ATR;
- ruang percobaan;
- aturan seleksi;
- pengendalian multiple testing;
- dan validasi OOS.

### Ringkasan Status ATR

| Komponen | Ketentuan TEKB |
|---|---|
| Ukuran dasar | True Range |
| Metode penghalusan | Wilder's smoothing |
| Periode awal | 14 |
| Status periode | CONFIGURED ASSUMPTION |
| Waktu pengambilan | Close T |
| Hubungan dengan entry | Entry pada Open T+1 |
| Nilai selama trade | Tetap menggunakan ATR_entry |
| Fungsi | Satuan volatilitas |
| Bukan fungsi | Prediksi arah, sinyal BUY/SELL, atau jaminan target |
| Optimasi bersama grid SL/TP | Tidak dilakukan dalam konfigurasi dasar |

---

## Ringkasan Bab

- Harga mentah sulit dibandingkan karena nilai nominal dan karakteristik volatilitas setiap instrumen berbeda.
- Volatilitas mengukur besar kecilnya pergerakan harga, bukan arah pergerakan.
- True Range mempertimbangkan High − Low serta kemungkinan gap dari Close sebelumnya.
- ATR adalah ukuran rata-rata True Range yang digunakan sebagai penggaris volatilitas.
- ATR bukan prediksi arah, bukan jaminan harga bergerak sebesar nilainya, dan bukan sinyal BUY atau SELL.
- TEKB menggunakan Wilder's smoothing agar perhitungan ATR konsisten dan tidak terlalu sensitif terhadap satu nilai ekstrem.
- Definisi ATR harus dibekukan agar alat ukur tidak diubah setelah melihat hasil.
- ATR_entry dihitung pada close T, sebelum entry pada open T+1.
- ATR_entry tetap digunakan sepanjang trade agar MAE, MFE, dan candidate SL/TP memiliki satuan yang konsisten.
- ATR_period_n = 14 merupakan CONFIGURED ASSUMPTION, bukan klaim bahwa periode 14 paling optimal.
- Periode ATR tidak dioptimasi bersama grid SL/TP dalam konfigurasi dasar TEKB.

---

## Pertanyaan Refleksi

1. Mengapa pergerakan Rp100 tidak memiliki arti yang sama pada semua saham?
2. Apa perbedaan antara volatilitas dan arah harga?
3. Mengapa True Range tidak hanya menggunakan High − Low?
4. Apa yang ditangkap True Range ketika terjadi gap?
5. Mengapa ATR tidak dapat dianggap sebagai prediksi harga?
6. Apa fungsi ATR dalam pengukuran MAE dan MFE?
7. Mengapa metode smoothing ATR harus konsisten?
8. Mengapa ATR_entry harus dihitung sebelum entry?
9. Apa risiko jika ATR dihitung ulang setelah trade berjalan?
10. Apa arti status CONFIGURED ASSUMPTION pada ATR_period_n = 14?
11. Mengapa periode ATR tidak boleh dioptimasi sembarangan bersama grid SL/TP?

---

## Kalimat Kunci

> ATR bukan bola kristal untuk meramal arah harga. ATR adalah penggaris yang membantu kita mengukur seberapa besar suatu pergerakan dalam konteks volatilitasnya.

---

<div align="center">

[← Bab Sebelumnya](/posts/bab-09-mae-dan-mfe/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Bab Selanjutnya →](/posts/bab-11-satuan-xatr/)

</div>