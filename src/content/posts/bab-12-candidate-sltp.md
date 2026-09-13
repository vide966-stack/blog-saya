---
title: "BAB 12 — Candidate SL/TP: Hipotesis, Bukan Hasil Ramalan"
published: 2026-09-12
description: "Candidate SL/TP adalah hipotesis yang harus diuji, bukan angka yang dipilih karena terlihat menguntungkan. Bab ini menjelaskan candidate grid, ×ATR, dan batasan grid TEKB."
tags: ["bab-12", "sl-tp", "candidate-grid", "hipotesis"]
category: "Bab"
draft: false
lang: ""
---

**BAGIAN III — MENGUKUR HASIL TANPA MENIPU DIRI SENDIRI**

---

Dalam penelitian trading, kita sering ingin mengetahui apakah suatu posisi sebaiknya diberi batas kerugian tertentu, target keuntungan tertentu, dan batas waktu tertentu.

Misalnya:

- stop-loss sebesar 1 × ATR;
- take-profit sebesar 2 × ATR;
- posisi diamati selama maksimal 10 bar.

Sekilas, angka-angka tersebut terlihat seperti keputusan trading. Namun, dalam TEKB, angka tersebut tidak langsung dianggap sebagai aturan terbaik.

Angka-angka itu terlebih dahulu diperlakukan sebagai **candidate**, yaitu kandidat yang akan diuji.

Mengapa?

Karena penelitian tidak boleh memilih aturan hanya berdasarkan hasil historis yang terlihat paling bagus. Jika peneliti melihat banyak kombinasi lalu memilih satu kombinasi yang paling menguntungkan, hasil tersebut dapat menjadi terlalu cocok dengan data masa lalu.

Karena itu, TEKB membedakan:

- **candidate SL/TP**, yaitu hipotesis yang akan diuji;
- **hasil evaluasi**, yaitu apa yang terjadi ketika hipotesis tersebut diterapkan pada event;
- **seleksi**, yaitu proses menentukan apakah kandidat memiliki bukti yang cukup;
- dan **validasi OOS**, yaitu pengujian terhadap data yang tidak digunakan untuk memilih kandidat.

Prinsip utama bab ini adalah:

> Candidate SL/TP bukan ramalan tentang apa yang pasti terjadi. Candidate SL/TP adalah kumpulan hipotesis yang harus diuji secara disiplin.

---

## 12.1. Apa Itu Stop Loss dan Take Profit?

Sebelum memahami candidate grid, kita perlu memahami tiga komponen dasar: Stop Loss, Take Profit, dan Maximum Hold.

### Stop Loss sebagai Batas Kerugian yang Dirancang

**Stop Loss** (SL) adalah batas harga yang dirancang untuk membatasi kerugian pada suatu posisi.

Untuk posisi long, stop-loss biasanya ditempatkan di bawah harga entry.

Misalnya:

- harga entry = Rp5.000;
- stop-loss = Rp4.900.

Jika harga bergerak turun dan menyentuh atau melewati level yang ditentukan sesuai aturan evaluasi, posisi dianggap mengalami kondisi stop-loss.

Namun, stop-loss yang dirancang tidak selalu sama dengan kerugian aktual. Dalam kondisi gap atau pergerakan cepat, harga eksekusi dapat berbeda dari level yang direncanakan.

Karena itu, dalam penelitian TEKB, SL adalah bagian dari aturan evaluasi, bukan jaminan bahwa kerugian akan selalu berhenti tepat pada angka tersebut.

### Take Profit sebagai Target Keuntungan yang Dirancang

**Take Profit** (TP) adalah target harga yang dirancang untuk merealisasikan keuntungan ketika harga bergerak sesuai arah posisi.

Untuk posisi long, take-profit biasanya ditempatkan di atas harga entry.

Misalnya:

- harga entry = Rp5.000;
- take-profit = Rp5.200.

Jika harga mencapai level tersebut sesuai aturan evaluasi, event dapat dikategorikan sebagai mencapai target.

Namun, TP juga bukan jaminan bahwa harga pasti akan mencapainya. TP hanyalah level yang digunakan untuk menguji pertanyaan:

> "Seberapa sering harga mampu mencapai jarak keuntungan tertentu sebelum mengalami kondisi yang berlawanan atau melewati batas waktu?"

### Maximum Hold sebagai Batas Waktu Pengamatan atau Trade

**Maximum hold** adalah batas maksimal waktu atau jumlah bar yang digunakan untuk mengamati event.

Misalnya:

- maximum hold = 1 bar;
- maximum hold = 3 bar;
- maximum hold = 5 bar;
- maximum hold = 10 bar.

Maximum hold membatasi periode pengamatan agar semua event dievaluasi dengan aturan yang sebanding.

Jika harga belum mencapai SL atau TP sampai batas waktu tersebut, event dapat berakhir dengan status seperti TIMEOUT, sesuai definisi Evaluation Engine.

TIMEOUT bukan berarti data tidak tersedia. TIMEOUT berarti event masih dapat diamati sampai batas waktu yang ditentukan, tetapi tidak mencapai kondisi akhir SL atau TP dalam periode tersebut.

Dengan demikian:

- SL menentukan batas kerugian yang diuji;
- TP menentukan target keuntungan yang diuji;
- maximum hold menentukan berapa lama hipotesis tersebut diamati.

Ketiganya membentuk satu kandidat evaluasi.

---

## 12.2. Mengapa TEKB Tidak Langsung Memilih SL/TP dari Hasil yang Terlihat Bagus?

Dalam praktik trading, orang sering melihat grafik historis lalu berkata:

> "Kalau stop-loss-nya sedikit lebih lebar, hasilnya terlihat lebih bagus."

Atau:

> "Kalau targetnya dipersempit, win rate-nya menjadi tinggi."

Pernyataan tersebut mungkin benar untuk data tertentu. Namun, pertanyaan penelitian bukan hanya apakah sebuah angka terlihat bagus pada masa lalu. Pertanyaan yang lebih penting adalah:

> "Apakah hasil tersebut cukup kuat untuk dipercaya dan berpotensi berlaku pada data yang belum digunakan?"

### Risiko Memilih Angka Setelah Melihat Data

Bayangkan peneliti mencoba banyak kombinasi:

- SL 0,5 ATR dan TP 1 ATR;
- SL 0,5 ATR dan TP 2 ATR;
- SL 1 ATR dan TP 1 ATR;
- SL 1 ATR dan TP 2 ATR;
- SL 1,5 ATR dan TP 3 ATR;
- serta berbagai maximum hold.

Setelah semuanya diuji, peneliti memilih kombinasi dengan profit terbesar.

Masalahnya, kombinasi tersebut mungkin terlihat unggul bukan karena benar-benar memiliki information edge, melainkan karena secara kebetulan paling cocok dengan pola historis yang tersedia.

Semakin banyak pilihan yang dicoba, semakin besar peluang menemukan satu hasil yang tampak menarik hanya karena kebetulan.

### Hubungan dengan Overfitting

**Overfitting** terjadi ketika suatu aturan terlalu menyesuaikan diri dengan data yang digunakan untuk membentuk atau memilihnya, sehingga kinerjanya menurun ketika diterapkan pada data baru.

Dalam konteks SL/TP:

- peneliti mencoba banyak jarak;
- melihat hasil masing-masing;
- memilih kombinasi yang paling sesuai dengan sejarah tertentu;
- lalu menganggap kombinasi itu sebagai aturan umum.

Padahal, kombinasi tersebut mungkin hanya cocok untuk:

- periode tertentu;
- instrumen tertentu;
- rezim volatilitas tertentu;
- atau rangkaian event tertentu.

Overfitting tidak selalu terlihat sebagai kesalahan yang jelas. Justru, hasil overfit sering tampak sangat meyakinkan pada data yang digunakan untuk memilihnya.

### Bahaya Menyesuaikan Level terhadap Hasil Historis Tertentu

Misalnya, peneliti melihat bahwa banyak event mengalami penurunan kecil sebelum naik. Ia lalu memilih SL yang ditempatkan tepat di bawah titik terendah yang terlihat pada sampel historis.

Jika level tersebut dipilih setelah melihat seluruh perjalanan harga, maka peneliti telah menggunakan informasi hasil untuk menentukan aturan.

Aturan itu mungkin sangat cocok untuk data yang sudah dilihat, tetapi belum tentu memiliki dasar yang kuat untuk event berikutnya.

Dalam TEKB, candidate SL/TP tidak boleh dirancang dengan cara:

1. melihat hasil akhir;
2. mencari level yang paling menguntungkan;
3. menetapkan level tersebut sebagai aturan;
4. lalu menyebut hasilnya sebagai bukti independen.

Sebaliknya, ruang kandidat harus ditentukan terlebih dahulu, kemudian setiap kandidat diuji dengan Evaluation Engine yang sama.

Prinsipnya:

> Penelitian harus menguji aturan yang telah ditentukan, bukan menciptakan aturan dari hasil yang ingin dijelaskan.

---

## 12.3. Apa Itu Candidate Grid?

**Candidate grid** adalah daftar kombinasi nilai SL, TP, dan maximum hold yang telah ditentukan untuk diuji.

Grid dapat dipahami sebagai ruang pertanyaan penelitian.

Alih-alih langsung berkata:

> "SL terbaik adalah 1 ATR dan TP terbaik adalah 2 ATR,"

TEKB memulai dengan pertanyaan:

> "Bagaimana performa beberapa kombinasi SL, TP, dan maximum hold yang telah ditentukan sebelumnya?"

### Contoh Grid Sederhana

Misalnya, sebuah penelitian menggunakan:

- SL: 0,5 ATR; 1,0 ATR; 1,5 ATR;
- TP: 1,0 ATR; 2,0 ATR; 3,0 ATR;
- maximum hold: 3 bar; 5 bar; 10 bar.

Setiap kombinasi membentuk satu kandidat.

Contohnya:

- Kandidat A: SL 0,5 ATR; TP 1,0 ATR; hold 3 bar.
- Kandidat B: SL 0,5 ATR; TP 2,0 ATR; hold 5 bar.
- Kandidat C: SL 1,0 ATR; TP 2,0 ATR; hold 10 bar.
- Kandidat D: SL 1,5 ATR; TP 3,0 ATR; hold 10 bar.

Jika seluruh kombinasi diuji, jumlah kandidat dapat dihitung dari jumlah pilihan pada setiap komponen.

Dalam contoh tersebut:

- 3 pilihan SL;
- 3 pilihan TP;
- 3 pilihan maximum hold.

Maka terdapat:

> 3 × 3 × 3 = 27 kandidat.

Setiap kandidat adalah pertanyaan yang berbeda.

### Grid sebagai Ruang Hipotesis

Candidate grid bukan jawaban final. Grid adalah ruang hipotesis yang membatasi pertanyaan agar penelitian tetap terstruktur.

Contoh hipotesis:

- Apakah target 2 ATR lebih sering tercapai daripada target 1 ATR?
- Apakah SL 1 ATR menghasilkan keseimbangan yang lebih baik antara peluang mencapai TP dan risiko terkena SL?
- Apakah maximum hold 5 bar cukup untuk menangkap gerakan event?
- Apakah hasil kandidat tertentu lebih baik daripada B0 yang sebanding?

Pertanyaan-pertanyaan tersebut belum memiliki jawaban sebelum evaluasi dilakukan.

### Mengapa Grid Harus Terbatas?

Jika peneliti bebas mencoba semua kemungkinan angka:

- SL 0,01 ATR;
- SL 0,02 ATR;
- SL 0,03 ATR;
- dan seterusnya tanpa batas;

serta berbagai TP, hold, instrumen, periode, dan definisi lainnya, ruang pencarian dapat menjadi sangat besar.

Ruang pencarian yang terlalu luas meningkatkan peluang menemukan hasil yang terlihat bagus secara kebetulan.

Grid yang ditentukan sebelumnya membantu:

- membatasi jumlah percobaan;
- mendokumentasikan apa yang diuji;
- mengendalikan multiple testing;
- menjaga penelitian dapat diulang;
- dan memisahkan hipotesis dari hasil.

### Candidate Bukan Prediksi

Kandidat SL/TP tidak mengatakan:

> "Harga pasti turun 1 ATR lalu naik 2 ATR."

Kandidat hanya mengatakan:

> "Kita akan menguji apa yang terjadi jika aturan evaluasi menggunakan SL 1 ATR, TP 2 ATR, dan maximum hold tertentu."

Perbedaan ini sangat penting.

Kandidat adalah rancangan pengukuran. Hasil aktual berasal dari data dan aturan evaluasi, bukan dari nama atau angka kandidat itu sendiri.

---

## 12.4. Mengapa Kandidat Menggunakan ×ATR?

Dalam TEKB, kandidat SL/TP menggunakan satuan ×ATR agar jarak yang diuji lebih sebanding dengan volatilitas event.

Jika kandidat hanya dinyatakan dalam rupiah, jarak yang sama dapat memiliki arti berbeda pada instrumen atau kondisi pasar yang berbeda.

### Konsistensi Satuan

Misalnya, kandidat ditetapkan:

- SL = 1 ATR;
- TP = 2 ATR.

Untuk event dengan ATR_entry Rp100:

- SL berjarak Rp100 dari entry;
- TP berjarak Rp200 dari entry.

Untuk event dengan ATR_entry Rp300:

- SL berjarak Rp300 dari entry;
- TP berjarak Rp600 dari entry.

Aturan kandidatnya sama, tetapi jarak rupiahnya menyesuaikan ukuran volatilitas masing-masing event.

### Perbandingan Antar-Instrumen

×ATR membantu peneliti membandingkan kandidat pada instrumen dengan harga dan volatilitas berbeda.

Misalnya:

- Saham A memiliki ATR_entry Rp100.
- Saham B memiliki ATR_entry Rp400.

Kandidat SL 1 ATR berarti:

- Saham A: jarak SL Rp100.
- Saham B: jarak SL Rp400.

Kandidat TP 2 ATR berarti:

- Saham A: jarak TP Rp200.
- Saham B: jarak TP Rp800.

Dengan demikian, peneliti tidak memaksakan jarak rupiah yang sama pada instrumen yang memiliki karakteristik pergerakan berbeda.

### Contoh SL 1 ATR dan TP 2 ATR

Misalnya:

- entry = Rp5.000;
- ATR_entry = Rp100;
- SL = 1 ATR;
- TP = 2 ATR.

Maka:

- level SL = Rp4.900;
- level TP = Rp5.200.

Jika event lain memiliki:

- entry = Rp8.000;
- ATR_entry = Rp250;
- SL = 1 ATR;
- TP = 2 ATR.

Maka:

- level SL = Rp7.750;
- level TP = Rp8.500.

Kedua event menggunakan aturan kandidat yang sama secara relatif terhadap volatilitasnya.

Namun, hal ini tidak berarti risiko uang keduanya sama. Risiko aktual tetap dipengaruhi oleh ukuran posisi, biaya, gap, slippage, dan kondisi eksekusi.

### Kandidat sebagai Hipotesis yang Akan Diuji

Kandidat SL/TP dalam ×ATR harus dipahami sebagai pertanyaan:

> "Apakah jarak tertentu relatif terhadap volatilitas entry memiliki karakteristik hasil yang berbeda dari pembanding B0?"

Peneliti kemudian mengukur:

- apakah SL tersentuh;
- apakah TP tercapai;
- kapan kondisi tersebut terjadi;
- apakah terjadi ambiguitas intrabar;
- apakah event berakhir TIMEOUT;
- bagaimana hasil worst-case dan best-case;
- serta bagaimana hasil B1 dibandingkan dengan B0.

Jadi, ×ATR membantu menyusun kandidat dalam satuan yang konsisten, tetapi tidak menentukan kandidat mana yang memiliki edge.

---

## 12.5. Batasan Grid TEKB

Candidate grid TEKB memiliki batasan yang harus ditetapkan secara eksplisit. Batasan ini mencegah ruang hipotesis berubah-ubah setelah hasil terlihat.

### 1. Long-Only

Dalam konfigurasi dasar yang dibahas pada bab ini, candidate SL/TP digunakan untuk posisi **long-only**.

Artinya:

- entry dilakukan dengan asumsi membeli terlebih dahulu;
- SL berada di bawah entry;
- TP berada di atas entry;
- MAE mengukur gerakan berlawanan arah, yaitu penurunan dari entry;
- MFE mengukur gerakan yang mendukung posisi, yaitu kenaikan dari entry.

Jika suatu saat TEKB mengembangkan penelitian short, aturan tersebut harus dibuat sebagai desain atau versi penelitian tersendiri. Aturan short tidak boleh dicampurkan begitu saja ke dalam definisi long-only.

### 2. Nilai Diskrit

Grid menggunakan nilai kandidat yang telah ditentukan, bukan semua angka kontinu yang mungkin.

Contohnya:

- SL ∈ {0,5; 1,0; 1,5} ×ATR;
- TP ∈ {1,0; 2,0; 3,0} ×ATR;
- maximum hold ∈ {3; 5; 10} bar.

Nilai diskrit membantu membatasi jumlah kandidat dan membuat ruang penelitian dapat diaudit.

Jika peneliti ingin menambah nilai baru, penambahan tersebut harus didokumentasikan sebagai perubahan ruang hipotesis atau percobaan baru.

### 3. Maximum Hold Hanya pada Horizon yang Tersedia

Maximum hold tidak boleh melebihi horizon data yang tersedia dan telah ditetapkan dalam penelitian.

Misalnya, data penelitian hanya menyediakan pengukuran sampai 10 bar setelah entry. Maka maximum hold 20 bar tidak dapat dievaluasi secara penuh dalam desain tersebut.

Dalam TEKB, kandidat maximum hold harus berada dalam horizon yang tersedia, misalnya:

- R1;
- R3;
- R5;
- R10.

Jika sebuah event tidak memiliki data yang cukup untuk horizon kandidat, event tersebut tidak boleh dianggap seolah-olah telah menyelesaikan evaluasi penuh.

Status seperti INSUFFICIENT_HORIZON harus dipisahkan dari outcome yang benar-benar dapat dihitung.

### 4. Populasi Utama EQUAL_PER_EVENT

Populasi utama TEKB menggunakan prinsip **EQUAL_PER_EVENT**.

Artinya, setiap event yang memenuhi syarat memiliki bobot yang sama dalam agregasi utama, bukan setiap instrumen otomatis memiliki bobot yang sama.

Contohnya:

- satu event dari Saham A dihitung sebagai satu unit;
- satu event dari Saham B juga dihitung sebagai satu unit.

Jika Saham A memiliki lebih banyak event, kontribusinya dalam populasi utama juga dapat lebih besar karena jumlah event-nya lebih banyak.

Prinsip ini harus diketahui sejak awal karena pilihan unit agregasi dapat memengaruhi kesimpulan.

EQUAL_PER_EVENT tidak berarti bahwa setiap instrumen memiliki kontribusi yang sama. Ia berarti unit dasar analisis utama adalah event.

### 5. Populasi Diagnostik EQUAL_PER_INSTRUMENT

Selain populasi utama, TEKB dapat menggunakan **EQUAL_PER_INSTRUMENT** sebagai populasi diagnostik.

Dalam pendekatan ini, setiap instrumen diberi bobot yang sama terlebih dahulu, sehingga instrumen dengan jumlah event lebih banyak tidak otomatis mendominasi hasil agregat.

Tujuannya bukan menggantikan populasi utama, melainkan membantu memeriksa apakah kesimpulan terlalu dipengaruhi oleh instrumen tertentu.

Contoh:

- Saham A memiliki 1.000 event;
- Saham B memiliki 100 event.

Dalam EQUAL_PER_EVENT, Saham A dapat memberikan kontribusi lebih besar karena memiliki lebih banyak event.

Dalam EQUAL_PER_INSTRUMENT, hasil masing-masing instrumen diringkas terlebih dahulu, lalu kontribusinya diseimbangkan.

Jika hasil utama dan diagnostik berbeda jauh, perbedaan tersebut perlu dilaporkan dan diselidiki.

### 6. Grid Ditentukan Sebelum Seleksi

Grid harus ditentukan sebelum proses seleksi kandidat berdasarkan hasil.

Artinya, peneliti harus mengetahui:

- daftar nilai SL;
- daftar nilai TP;
- daftar maximum hold;
- aturan pembentukan kombinasi;
- dan identitas versi grid.

Peneliti tidak boleh melihat hasil terlebih dahulu lalu menambah kandidat hanya pada area yang tampak menarik, kemudian memperlakukan seluruh proses seolah-olah telah dirancang sejak awal.

Jika grid berubah, perubahan tersebut harus dicatat, misalnya melalui:

- candidate_grid_version_id;
- research_batch_id;
- attempt_number;
- atau identitas eksperimen baru.

Dokumentasi ini penting karena setiap penambahan atau perubahan grid dapat meningkatkan jumlah percobaan dan memengaruhi interpretasi hasil.

---

## 12.6. Percentile Hanya Membatasi Rentang

Dalam penelitian TEKB, **percentile** dapat digunakan untuk membantu membatasi ruang pencarian kandidat. Namun, percentile tidak boleh diperlakukan sebagai alat yang secara otomatis memilih titik SL atau TP terbaik.

### Apa Itu Percentile?

Percentile adalah cara untuk menggambarkan posisi suatu nilai dalam distribusi.

Misalnya:

- percentile 50 sering berkaitan dengan median;
- percentile 25 menunjukkan batas di mana sebagian nilai berada di bawahnya;
- percentile 75 menunjukkan batas di mana sebagian nilai berada di bawahnya.

Dalam konteks MAE/MFE, percentile dapat membantu peneliti memahami rentang gerakan historis.

Contohnya:

- MAE percentile 75 = 1,2 ATR;
- MFE percentile 75 = 2,5 ATR.

Angka tersebut dapat memberi gambaran tentang seberapa besar gerakan yang umum atau relatif ekstrem dalam sampel.

Namun, angka percentile tersebut belum membuktikan bahwa:

- SL 1,2 ATR adalah pilihan terbaik;
- TP 2,5 ATR adalah target yang memiliki edge;
- atau kombinasi tertentu akan menguntungkan.

### Percentile B1/B0 Bukan Alat untuk Memilih Titik Kandidat Secara Langsung

Percentile B1 dan B0 dapat membantu memahami distribusi kedua kelompok. Akan tetapi, percentile tidak boleh langsung diubah menjadi keputusan:

> "Karena MFE B1 percentile 75 adalah 2 ATR, maka TP terbaik pasti 2 ATR."

Kesimpulan tersebut tidak sah hanya berdasarkan percentile.

Mengapa?

Karena candidate SL/TP harus dievaluasi melalui aturan lengkap:

- urutan kejadian;
- apakah SL atau TP tersentuh lebih dahulu;
- gap-through;
- same-bar SL/TP;
- ambiguitas intrabar;
- maximum hold;
- perbandingan B1 dan B0;
- serta ketidakpastian hasil.

MFE sebesar 2 ATR tidak berarti TP 2 ATR pasti tercapai sebelum SL. Harga mungkin sempat mencapai MFE 2 ATR setelah terlebih dahulu menyentuh SL. Karena itu, MFE dan evaluasi SL/TP adalah dua hal yang berhubungan, tetapi tidak identik.

### Perbedaan Pembatasan Ruang Pencarian dan Seleksi Edge

Ada dua proses yang harus dibedakan:

1. Membatasi ruang pencarian
2. Memilih kandidat yang memiliki bukti edge

Percentile dapat digunakan untuk proses pertama. Misalnya, peneliti menetapkan bahwa kandidat SL/TP hanya boleh berada dalam rentang yang masih masuk akal berdasarkan distribusi historis.

Namun, proses kedua membutuhkan Evaluation Engine dan aturan seleksi yang telah ditentukan.

Kandidat harus diuji terhadap:

- hasil B1;
- hasil B0;
- perbedaan berpasangan;
- ketidakpastian;
- kriteria praktis;
- serta pengendalian multiple testing.

Dengan demikian:

> Percentile membantu menentukan "di mana kita mencari", tetapi tidak menjawab "kandidat mana yang terbukti memiliki edge".

### Bahaya Memilih Kandidat Hanya karena Percentile Tampak Menarik

Misalnya, peneliti melihat:

- MFE B1 percentile 90 = 3 ATR;
- MAE B1 percentile 50 = 0,4 ATR.

Peneliti lalu memilih:

- SL = 0,4 ATR;
- TP = 3 ATR.

Pilihan ini terlihat menarik, tetapi belum tentu masuk akal sebagai aturan evaluasi.

Beberapa masalah mungkin muncul:

- TP 3 ATR jarang tercapai sebelum SL;
- median MAE tidak menggambarkan ekor risiko;
- percentile MFE tidak menunjukkan urutan SL dan TP;
- B0 mungkin memiliki distribusi yang serupa;
- dan hasil tersebut mungkin tidak bertahan pada OOS.

Percentile adalah deskripsi distribusi, bukan bukti bahwa suatu kombinasi SL/TP bekerja.

### Prinsip Penggunaan Percentile dalam TEKB

Percentile boleh membantu:

- memahami skala MAE/MFE;
- memeriksa rentang kandidat yang masuk akal;
- membatasi grid agar tidak terlalu luas;
- dan menyusun hipotesis awal.

Percentile tidak boleh digunakan untuk:

- memilih kandidat terbaik secara otomatis;
- menggantikan B0;
- menggantikan Evaluation Engine;
- menghapus kandidat yang hasilnya tidak menarik setelah melihat data;
- atau membuktikan information edge.

Jika percentile digunakan untuk membatasi grid, penggunaannya harus didokumentasikan sebagai bagian dari desain penelitian, bukan disamarkan sebagai hasil seleksi yang bebas dari pengaruh data.

---

## Ringkasan Bab

- Stop-loss adalah batas kerugian yang dirancang, take-profit adalah target keuntungan yang dirancang, dan maximum hold adalah batas waktu pengamatan atau trade.
- Dalam TEKB, SL/TP tidak langsung dipilih dari hasil yang terlihat bagus.
- Pemilihan angka setelah melihat data dapat menyebabkan data snooping dan overfitting.
- Candidate grid adalah daftar kombinasi SL, TP, dan maximum hold yang ditentukan untuk diuji.
- Grid merupakan ruang hipotesis, bukan jawaban final atau ramalan.
- Penggunaan ×ATR membantu menjaga konsistensi satuan dan perbandingan antar-instrumen dengan volatilitas berbeda.
- Candidate grid dasar TEKB memiliki batasan long-only, nilai diskrit, dan maximum hold yang tidak melebihi horizon tersedia.
- Populasi utama menggunakan EQUAL_PER_EVENT, sedangkan EQUAL_PER_INSTRUMENT digunakan sebagai populasi diagnostik.
- Grid harus ditentukan sebelum seleksi dan setiap perubahan harus terdokumentasi.
- Percentile dapat membantu membatasi rentang pencarian, tetapi tidak boleh langsung digunakan untuk memilih kandidat terbaik.
- Percentile tidak menggantikan Evaluation Engine, B0, pengujian ketidakpastian, atau validasi OOS.
- Candidate SL/TP adalah hipotesis yang harus diuji, bukan hasil ramalan tentang pergerakan harga.

---

## Pertanyaan Refleksi

1. Apa perbedaan antara SL sebagai rancangan dan kerugian aktual?
2. Mengapa maximum hold diperlukan dalam evaluasi event?
3. Mengapa memilih SL/TP setelah melihat hasil historis dapat menyebabkan overfitting?
4. Apa yang dimaksud dengan candidate grid?
5. Mengapa grid harus ditentukan sebelum proses seleksi?
6. Mengapa TEKB menggunakan ×ATR untuk kandidat SL/TP?
7. Mengapa 1 ATR tidak berarti risiko uang pasti sama?
8. Apa perbedaan EQUAL_PER_EVENT dan EQUAL_PER_INSTRUMENT?
9. Mengapa maximum hold tidak boleh melebihi horizon yang tersedia?
10. Apa fungsi percentile dalam membatasi ruang pencarian?
11. Mengapa MFE 2 ATR tidak otomatis berarti TP 2 ATR akan tercapai sebelum SL?
12. Mengapa percentile tidak dapat menggantikan Evaluation Engine?
13. Apa risiko menambah kandidat baru hanya karena area tersebut terlihat menarik setelah hasil awal diperoleh?

---

## Kalimat Kunci

> Candidate SL/TP bukan angka yang dipilih karena terlihat paling menguntungkan. Candidate SL/TP adalah hipotesis yang ditentukan terlebih dahulu, lalu diuji dengan aturan yang sama terhadap B1 dan B0.

---

<div align="center">

[← Bab Sebelumnya](/posts/bab-11-satuan-xatr/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Bab Selanjutnya →](/posts/bab-13-empiris-dan-stokastik/)

</div>