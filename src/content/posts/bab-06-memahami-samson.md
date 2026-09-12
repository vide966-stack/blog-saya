---
title: "BAB 6 — Memahami SAMSON: Detektor Anomali Volume"
published: 2026-09-12
description: "SAMSON adalah detektor anomali volume dalam TEKB. Bab ini menjelaskan cara kerja Relative Volume (RV), baseline per sesi dan slot, serta mengapa SAMSON bukan sinyal BUY/SELL otomatis."
tags: ["bab-6", "samson", "volume", "rv"]
category: "Bab"
draft: false
lang: ""
---


**BAGIAN II — MEMBANGUN BAHASA DAN DATA PENELITIAN**

---

## Tujuan Bab

Dalam penelitian trading, volume sering dianggap sebagai petunjuk penting. Ketika volume tiba-tiba membesar, trader dapat menganggap bahwa sedang terjadi sesuatu yang tidak biasa: perhatian pasar meningkat, banyak transaksi berlangsung, atau ada perubahan minat terhadap suatu instrumen.

Namun, volume besar tidak otomatis berarti harga akan naik. Volume besar juga tidak selalu berarti harga akan turun. Bahkan, volume yang tinggi dapat muncul ketika pembeli dan penjual sama-sama agresif, tetapi kekuatan mereka relatif seimbang sehingga harga tidak bergerak jauh.

Karena itu, TEKB tidak menggunakan volume besar sebagai perintah otomatis untuk membeli atau menjual. TEKB terlebih dahulu memperlakukannya sebagai kejadian yang perlu dideteksi, dicatat, dan diteliti.

Dalam kerangka ini, **SAMSON** berfungsi sebagai detektor anomali volume. Tugasnya bukan meramalkan arah harga, melainkan menjawab pertanyaan awal:

> Apakah volume saat ini tidak biasa dibandingkan dengan kondisi normal yang sebanding?

Setelah anomali ditemukan, barulah penelitian dapat dilanjutkan dengan pertanyaan lain:

- Apa yang terjadi pada harga setelah anomali?
- Apakah harga cenderung naik, turun, atau tidak bergerak?
- Apakah hasilnya berbeda dari kondisi normal?
- Apakah perbedaan tersebut cukup konsisten untuk dianggap memiliki informasi?

Dengan demikian, SAMSON adalah pintu masuk penelitian, bukan kesimpulan penelitian.

---

## 6.1. Apa Masalah yang Ingin Dijawab SAMSON?

### 6.1.1. Volume besar belum tentu tidak biasa

Volume adalah jumlah saham atau unit instrumen yang diperdagangkan dalam suatu periode. Akan tetapi, angka volume yang besar tidak selalu menunjukkan kondisi anomali.

Misalnya, volume 10 juta saham dapat dianggap sangat besar pada pukul 09.05, tetapi mungkin justru normal pada pukul 14.45. Hal ini terjadi karena aktivitas pasar tidak merata sepanjang hari.

Pada pembukaan pasar, banyak order yang tertunda sejak hari sebelumnya dapat dieksekusi. Menjelang penutupan, sebagian pelaku pasar juga meningkatkan aktivitas untuk menyesuaikan posisi. Akibatnya, volume pada waktu-waktu tersebut secara alami dapat lebih tinggi dibandingkan waktu lainnya.

Jadi, pertanyaan yang benar bukan sekadar:

> "Apakah volume hari ini besar?"

Melainkan:

> "Apakah volume pada waktu ini lebih besar daripada volume normal pada waktu yang sebanding?"

Perubahan cara bertanya ini sangat penting. Volume absolut hanya menyatakan berapa banyak transaksi terjadi. SAMSON berusaha menilai apakah jumlah tersebut tidak biasa dibandingkan baseline yang tepat.

### 6.1.2. Anomali harus memiliki pembanding

Sebuah angka baru dapat disebut anomali apabila dibandingkan dengan pola normal atau baseline.

Contohnya:

- Suhu 35°C mungkin dianggap panas di suatu daerah.
- Tetapi suhu 35°C mungkin normal di daerah lain.
- Volume 1 juta saham mungkin sangat tinggi untuk saham yang biasanya sepi.
- Namun, volume 1 juta saham mungkin rendah untuk saham yang sangat aktif.

Artinya, "besar" bukan sifat yang berdiri sendiri. Besar harus didefinisikan relatif terhadap konteks.

Dalam SAMSON, konteks tersebut dapat meliputi:

- Instrumen yang sama.
- Sesi perdagangan yang sama.
- Slot waktu yang sama.
- Riwayat volume yang relevan.
- Data yang tersedia sebelum kejadian.
- Aturan baseline yang telah ditentukan sebelumnya.

Tanpa baseline, istilah "volume besar" mudah berubah menjadi penilaian subjektif.

### 6.1.3. Baseline bukan sekadar rata-rata sembarangan

Baseline adalah gambaran kondisi normal yang digunakan sebagai pembanding. Baseline dapat berupa rata-rata, median, atau ukuran statistik lain yang ditetapkan dalam kontrak penelitian.

Namun, baseline harus dibentuk dengan hati-hati. Baseline tidak boleh menggunakan informasi dari masa depan. Jika SAMSON mendeteksi anomali pada waktu, maka baseline harus dihitung dari data yang tersedia sebelum atau sampai batas yang diizinkan oleh kontrak pada waktu tersebut.

Prinsip dasarnya:

> Anomali harus dinilai berdasarkan apa yang dapat diketahui pada saat kejadian, bukan berdasarkan informasi yang baru diketahui setelahnya.

Jika baseline dihitung menggunakan volume masa depan, maka nilai RV dapat menjadi terlalu optimistis dan penelitian berisiko mengalami look-ahead bias.

---

## 6.2. Relative Volume atau RV

### 6.2.1. Pengertian Relative Volume

**Relative Volume** atau **RV** adalah perbandingan antara volume saat ini dan volume baseline.

Secara sederhana:

> RV_t = V_t ÷ BaselineVolume_t

Keterangan:

- V_t = volume pada waktu atau bar t.
- BaselineVolume_t = volume normal yang digunakan sebagai pembanding.
- RV_t = volume relatif terhadap baseline.

RV tidak terutama bertanya "berapa volume yang terjadi?", tetapi:

> "Berapa kali lebih besar atau lebih kecil volume saat ini dibandingkan kondisi normal?"

### 6.2.2. Contoh sederhana

Misalkan volume normal pada slot waktu tertentu adalah:

> BaselineVolume_t = 100.000

Volume aktual pada slot tersebut adalah:

> V_t = 300.000

Maka:

> RV_t = 300.000 ÷ 100.000 = 3

Artinya, volume saat ini adalah tiga kali volume baseline.

Interpretasinya:

- RV = 1: volume sama dengan baseline.
- RV = 0,5: volume sekitar setengah baseline.
- RV = 2: volume dua kali baseline.
- RV = 3: volume tiga kali baseline.
- RV = 5: volume lima kali baseline.

RV sebesar 3 tidak berarti harga akan naik tiga kali lebih besar. RV hanya menyatakan bahwa aktivitas volume relatif terhadap baseline berada pada tingkat tiga kali normal.

### 6.2.3. Volume absolut dan volume relatif

Perbedaan antara volume absolut dan volume relatif dapat dilihat pada contoh berikut.

| Instrumen | Volume Aktual | Baseline | RV |
|---|---|---|---|
| Saham A | 1.000.000 | 100.000 | 10 |
| Saham B | 10.000.000 | 20.000.000 | 0,5 |

Secara absolut, volume Saham B jauh lebih besar daripada Saham A. Namun, secara relatif:

- Saham A mengalami volume 10 kali normal.
- Saham B hanya berada pada setengah volume normal.

Jika tujuan penelitian adalah mendeteksi aktivitas yang tidak biasa, Saham A lebih menonjol meskipun volume absolutnya lebih kecil.

Inilah manfaat RV: memungkinkan peneliti membandingkan aktivitas terhadap kebiasaan instrumen dan konteksnya sendiri.

### 6.2.4. RV tidak sama dengan tekanan beli

RV mengukur besarnya aktivitas volume relatif terhadap baseline. RV tidak secara langsung mengukur:

- Berapa banyak pembeli yang lebih kuat daripada penjual.
- Berapa banyak order agresif di sisi beli.
- Apakah transaksi lebih dominan dilakukan oleh pembeli atau penjual.
- Apakah harga akan naik atau turun.

Volume dalam transaksi selalu melibatkan pihak pembeli dan penjual. Setiap transaksi yang terjadi memiliki kedua sisi tersebut.

Karena itu, RV sebaiknya dibaca sebagai:

> Ukuran intensitas aktivitas perdagangan relatif terhadap kondisi normal.

RV bukan bukti langsung tentang arah tekanan harga.

### 6.2.5. RV sebagai pemicu penelitian

Dalam TEKB, RV dapat digunakan untuk membentuk aturan deteksi, misalnya:

> SAMSON_t = 1 jika RV_t > θ

Keterangan:

- SAMSON_t = 1 berarti bar atau kejadian tersebut memenuhi syarat anomali.
- θ adalah ambang yang ditentukan dalam kontrak.

Contoh ambang dapat berupa RV > 2,5, RV > 5, atau persentil tertentu.

Namun, angka ambang tidak boleh dipilih hanya karena menghasilkan grafik atau hasil trading yang menarik. Ambang harus:

- Didefinisikan sebelum pengujian yang relevan.
- Dicatat sebagai bagian dari konfigurasi penelitian.
- Diuji dengan prosedur yang transparan.
- Tidak diubah berulang kali berdasarkan hasil OOS.
- Dibandingkan dengan baseline atau ambang alternatif bila memang termasuk dalam keluarga pengujian.

Ambang RV menghasilkan kelompok kejadian untuk diteliti. Ambang tersebut belum membuktikan adanya edge.

---

## 6.3. Mengapa Baseline Harus Memperhatikan Waktu?

### 6.3.1. Volume tidak merata sepanjang sesi

Dalam perdagangan intraday, aktivitas volume biasanya tidak konstan. Pada banyak pasar, pola volume dapat berbeda antara:

- Awal sesi.
- Tengah sesi.
- Akhir sesi.
- Periode sebelum jeda.
- Periode setelah jeda.
- Hari tertentu.
- Slot waktu tertentu.

Sebagai ilustrasi, sebuah saham dapat memiliki pola volume seperti berikut:

| Waktu | Volume Normal |
|---|---|
| 09.00–09.05 | 500.000 |
| 09.05–09.10 | 250.000 |
| 09.10–09.15 | 150.000 |
| 13.30–13.35 | 200.000 |
| 14.40–14.45 | 350.000 |

Jika volume aktual pada pukul 09.00–09.05 adalah 400.000, angka tersebut mungkin terlihat besar jika dibandingkan dengan volume tengah sesi sebesar 150.000. Namun, jika dibandingkan dengan baseline slot pembukaan sebesar 500.000, volume tersebut justru berada di bawah normal.

Kesalahan membandingkan slot yang berbeda dapat menyebabkan volume normal dianggap anomali.

### 6.3.2. Pentingnya session_id

Dalam data intraday, **session_id** digunakan untuk membedakan sesi perdagangan yang secara operasional berbeda.

Contohnya, suatu pasar dapat memiliki:

- Sesi pagi.
- Jeda perdagangan.
- Sesi siang.
- Sesi sore.
- Aturan khusus pada hari tertentu.

Sesi pagi dan sesi siang tidak selalu dapat diperlakukan sebagai satu rangkaian waktu yang identik. Kondisi likuiditas, partisipasi pelaku pasar, dan pola volume dapat berbeda.

Karena itu, baseline sebaiknya tidak mencampurkan sesi yang berbeda tanpa alasan metodologis yang jelas.

Contoh:

> session_id = MORNING

> session_id = AFTERNOON

Jika volume pada sesi pagi dibandingkan dengan baseline sesi siang, hasil RV dapat menjadi bias secara struktural. Nilai yang terlihat ekstrem mungkin sebenarnya hanya mencerminkan perbedaan karakter sesi.

### 6.3.3. Pentingnya slot_id

**slot_id** adalah identitas posisi waktu di dalam suatu sesi.

Misalnya, sesi pagi dimulai pukul 09.00 dan menggunakan bar 5 menit. Maka slot dapat diberi identitas:

| slot_id | slot_start | slot_end |
|---|---|---|
| 1 | 09.00 | 09.05 |
| 2 | 09.05 | 09.10 |
| 3 | 09.10 | 09.15 |
| 4 | 09.15 | 09.20 |

Slot pertama pada sesi pagi dibandingkan dengan slot pertama pada sesi pagi di hari-hari sebelumnya. Slot kedua dibandingkan dengan slot kedua, dan seterusnya.

Dengan cara ini, baseline lebih sebanding.

Contoh:

> session_id = MORNING

> slot_id = 3

> slot_start = 09:10:00

> slot_end = 09:15:00

Bar tersebut sebaiknya dibandingkan dengan bar yang memiliki:

- Instrumen yang sama.
- session_id yang sama.
- slot_id yang sama.
- Definisi durasi yang sama.
- Kondisi data yang memenuhi syarat.

### 6.3.4. Arti slot_start dan slot_end

**slot_start** dan **slot_end** menjelaskan batas waktu suatu bar atau slot.

Contohnya:

> slot_start = 09:10:00

> slot_end = 09:15:00

Artinya, slot tersebut mewakili interval waktu 09.10 sampai sebelum 09.15, sesuai dengan konvensi timestamp yang digunakan dalam data.

Informasi ini penting karena dua bar yang sama-sama diberi label "09.10" belum tentu memiliki definisi interval yang sama jika satu sistem menggunakan:

- Waktu pembukaan bar.
- Waktu penutupan bar.
- Interval inklusif.
- Interval eksklusif.
- Zona waktu yang berbeda.

Kesalahan dalam definisi waktu dapat menyebabkan baseline tidak benar-benar membandingkan periode yang sebanding.

### 6.3.5. Contoh kesalahan baseline

Misalkan peneliti menggunakan baseline gabungan seluruh hari dan seluruh waktu:

> BaselineVolume = rata-rata semua volume intraday

Kemudian ditemukan volume 300.000 pada pukul 09.00. Jika rata-rata seluruh waktu adalah 100.000, maka:

> RV = 300.000 ÷ 100.000 = 3

Peneliti mungkin menyimpulkan bahwa volume tiga kali normal.

Namun, jika volume normal khusus pukul 09.00 sebenarnya 400.000, maka baseline yang lebih tepat menghasilkan:

> RV = 300.000 ÷ 400.000 = 0,75

Dengan baseline yang sesuai slot, bar tersebut bukan anomali volume. Ia justru memiliki volume 25% di bawah normal.

Kesimpulannya:

> Baseline yang tidak memperhatikan waktu dapat mengubah pola musiman menjadi anomali palsu.

### 6.3.6. Prinsip perbandingan yang sebanding

Dalam TEKB, baseline intraday sebaiknya memperhatikan setidaknya:

- Instrumen.
- Sesi.
- Slot waktu.
- Durasi bar.
- Kalender perdagangan yang relevan.
- Ketersediaan data sebelum waktu pengukuran.
- Aturan pembersihan dan validasi data.

Secara konseptual:

> RV_i,t = V_i,t ÷ BaselineVolume_i,session,slot,t

Keterangan:

- i = instrumen.
- t = waktu pengamatan.
- session = sesi perdagangan.
- slot = posisi waktu dalam sesi.

Rumus tersebut menekankan bahwa volume tidak dibandingkan dengan angka umum, tetapi dengan volume normal pada konteks yang sebanding.

---


## 6.4. Apa Arti SAMSON dalam TEKB?

### 6.4.1. SAMSON sebagai detektor kejadian tidak biasa

Dalam TEKB, SAMSON adalah mekanisme untuk menandai bar atau periode ketika volume memenuhi definisi anomali yang telah ditetapkan.

Secara sederhana:
Data OHLCV
↓
Hitung baseline
↓
Hitung RV
↓
Bandingkan dengan ambang
↓
Tandai SAMSON
↓
Teliti apa yang terjadi setelahnya

SAMSON menjawab pertanyaan:

> "Apakah aktivitas volume pada bar ini cukup tidak biasa menurut aturan yang telah ditentukan?"

SAMSON belum menjawab:

> "Apa keputusan trading yang harus diambil?"

### 6.4.2. SAMSON bukan bukti harga akan naik

Volume besar dapat muncul dalam berbagai situasi:

- Pembeli dan penjual sama-sama aktif.
- Distribusi atau pelepasan posisi.
- Akumulasi atau perpindahan kepemilikan.
- Reaksi terhadap berita.
- Kepanikan pasar.
- Penyesuaian portofolio.
- Perubahan likuiditas.
- Aktivitas sementara yang tidak berlanjut.

Oleh karena itu, volume besar dapat diikuti oleh:

- Kenaikan harga.
- Penurunan harga.
- Pergerakan dua arah.
- Harga yang relatif datar.
- Volatilitas tinggi tanpa arah yang jelas.

SAMSON hanya menyatakan bahwa aktivitas volume tidak biasa. Arah harga harus diteliti secara terpisah.

### 6.4.3. SAMSON bukan keputusan entry

Kesalahan yang harus dihindari adalah menerjemahkan aturan berikut:

> Jika RV > 2,5 maka BUY

Aturan tersebut melompat terlalu jauh. Ia mengubah deteksi aktivitas menjadi keputusan arah tanpa membuktikan hubungan empirisnya.

Dalam TEKB, bentuk yang lebih tepat adalah:

> Jika RV > 2,5 maka tandai sebagai event SAMSON

Setelah itu, penelitian dapat mengukur:

- Return bar berikutnya.
- Return beberapa bar ke depan.
- Probabilitas kenaikan.
- Probabilitas penurunan.
- MAE.
- MFE.
- Distribusi hasil.
- Perbedaan terhadap B0.
- Ketahanan setelah biaya dan pengujian OOS.

Jika hasil penelitian menunjukkan tidak ada perbedaan yang berarti terhadap baseline, hasil tersebut tetap sah. Event SAMSON mungkin berguna untuk deskripsi pasar, tetapi belum tentu memiliki information edge yang dapat digunakan untuk keputusan trading.

### 6.4.4. SAMSON hanya membuka pertanyaan penelitian

SAMSON dapat membuka pertanyaan seperti:

- Apakah volume ekstrem diikuti return positif?
- Apakah volume ekstrem lebih sering muncul sebelum pembalikan?
- Apakah candle bearish dengan RV tinggi memiliki karakteristik khusus?
- Apakah arah candle saat volume ekstrem memberikan informasi tambahan?
- Apakah efeknya berbeda antara saham likuid dan kurang likuid?
- Apakah efek hanya muncul pada slot tertentu?
- Apakah hasilnya tetap terlihat setelah dibandingkan dengan B0?
- Apakah efek bertahan pada OOS?

Pertanyaan-pertanyaan tersebut harus diuji dengan definisi yang jelas. Tidak cukup hanya memilih contoh grafik yang tampak mendukung dugaan.

### 6.4.5. Hubungan SAMSON dengan penelitian TEKB

SAMSON dapat ditempatkan dalam alur penelitian sebagai berikut:

1. **Deteksi** — Menemukan volume yang tidak biasa berdasarkan baseline.
2. **Definisi event** — Mencatat kapan dan pada instrumen apa anomali terjadi.
3. **Definisi entry atau titik observasi** — Menentukan kapan pengukuran hasil dimulai, jika penelitian memang menguji entry.
4. **Pengukuran outcome** — Menghitung return, MAE, MFE, atau metrik lain.
5. **Pembanding B0** — Menguji apakah hasil event berbeda dari kondisi pembanding yang adil.
6. **Pengujian ketidakpastian** — Menggunakan metode yang sesuai, seperti bootstrap atau analisis distribusi.
7. **Validasi OOS** — Menguji apakah temuan bertahan pada data yang tidak digunakan untuk memilih aturan.
8. **Kesimpulan** — Menentukan apakah terdapat bukti informasi yang cukup atau justru NO_EDGE_FOUND.

Dengan alur ini, SAMSON tetap berada pada perannya sebagai detektor, bukan sebagai mesin keputusan otomatis.

---

## 6.5. Contoh: Tiga SAMSON, Tiga Hasil Berbeda

Untuk memahami mengapa SAMSON bukan sinyal BUY/SELL otomatis, perhatikan tiga contoh fiktif berikut.

Misalkan baseline volume pada suatu slot adalah 100.000 saham. Pada tiga kejadian, volume aktual mencapai 500.000 saham.

Maka:

> RV = 500.000 ÷ 100.000 = 5

Ketiganya memenuhi aturan:

> SAMSON aktif jika RV > 2,5

Namun, hasil setelah kejadian berbeda.

### 6.5.1. Kasus pertama: Volume besar lalu harga naik

| Komponen | Nilai |
|---|---|
| Volume aktual | 500.000 |
| Baseline | 100.000 |
| RV | 5 |
| Harga saat event | 1.000 |
| Harga setelah 3 bar | 1.030 |
| Return | +3% |

Dalam kasus ini, volume besar diikuti kenaikan harga.

Kemungkinan interpretasi awal:

- Ada peningkatan aktivitas yang bertepatan dengan permintaan kuat.
- Informasi atau perhatian pasar mungkin mendorong harga naik.
- Aktivitas volume tersebut mungkin berhubungan dengan kelanjutan pergerakan.

Namun, satu kejadian tidak cukup untuk membuktikan bahwa semua SAMSON bersifat bullish. Ia hanya menjadi satu observasi yang harus masuk ke kumpulan data penelitian.

### 6.5.2. Kasus kedua: Volume besar lalu harga turun

| Komponen | Nilai |
|---|---|
| Volume aktual | 500.000 |
| Baseline | 100.000 |
| RV | 5 |
| Harga saat event | 1.000 |
| Harga setelah 3 bar | 970 |
| Return | -3% |

Pada kasus kedua, volume sama-sama ekstrem, tetapi harga justru turun.

Hal ini dapat terjadi karena volume besar muncul saat:

- Pelaku pasar menjual dalam jumlah besar.
- Terjadi pelepasan posisi.
- Harga mengalami tekanan setelah berita.
- Pembeli menyerap transaksi, tetapi belum mampu mengangkat harga.
- Pasar mengalami kepanikan atau perubahan ekspektasi.

Kasus ini menunjukkan bahwa:

> Volume besar tidak memiliki arah tunggal.

Jika penelitian hanya mencatat contoh volume besar yang diikuti kenaikan, hasilnya akan mengalami bias seleksi.

### 6.5.3. Kasus ketiga: Volume besar tetapi harga tidak bergerak berarti

| Komponen | Nilai |
|---|---|
| Volume aktual | 500.000 |
| Baseline | 100.000 |
| RV | 5 |
| Harga saat event | 1.000 |
| Harga setelah 3 bar | 1.002 |
| Return | +0,2% |

Pada kasus ketiga, aktivitas volume sangat tinggi, tetapi harga hampir tidak berubah.

Ini juga merupakan hasil penting. Volume besar mungkin menunjukkan bahwa transaksi berlangsung ramai, tetapi belum tentu menghasilkan pergerakan arah yang besar.

Beberapa kemungkinan penjelasan:

- Pembeli dan penjual relatif seimbang.
- Likuiditas cukup besar untuk menyerap transaksi.
- Aktivitas tinggi terjadi tanpa perubahan informasi yang berkelanjutan.
- Pergerakan harga terjadi intrabar, tetapi harga kembali ke sekitar titik awal.
- Volume besar hanya bersifat sementara.

Kasus ini mencegah peneliti menyamakan "ramai" dengan "menguntungkan".

### 6.5.4. Ketiga kasus harus dicatat

Ketiga kejadian tersebut memiliki nilai RV yang sama, yaitu 5, tetapi outcome berbeda:

| Event | RV | Return setelah 3 bar | Hasil |
|---|---|---|---|
| A | 5 | +3,0% | Naik |
| B | 5 | -3,0% | Turun |
| C | 5 | +0,2% | Hampir datar |

Jika hanya kasus A yang dicatat, peneliti dapat membangun cerita bahwa SAMSON bullish. Jika kasus B dan C juga dicatat, gambaran menjadi lebih lengkap.

Penelitian yang jujur harus mencatat seluruh event yang memenuhi definisi, bukan hanya event yang mendukung dugaan.

### 6.5.5. Mengapa hasil individual tidak cukup?

Satu contoh dapat digunakan untuk menjelaskan konsep, tetapi tidak cukup untuk menyimpulkan pola umum.

Misalnya, dari 100 event SAMSON diperoleh:

- 45 event diikuti kenaikan.
- 40 event diikuti penurunan.
- 15 event relatif datar.

Apakah SAMSON berguna? Belum tentu dapat dijawab hanya dari hit rate tersebut.

Peneliti masih perlu mengetahui:

- Besarnya return, bukan hanya arahnya.
- Median dan distribusi return.
- Besarnya kerugian dan keuntungan.
- MAE dan MFE.
- Kondisi B0.
- Biaya transaksi.
- Ketergantungan event pada tanggal yang sama.
- Jumlah instrumen yang terwakili.
- Apakah hasil terkonsentrasi pada satu saham atau satu periode.
- Apakah hasil bertahan pada OOS.

Dengan kata lain, deteksi event adalah awal dari pengukuran, bukan akhir dari analisis.

### 6.5.6. Jangan hanya mencari cerita yang cocok

Dalam penelitian trading, manusia mudah tertarik pada contoh yang sesuai dengan dugaan awal.

Misalnya:

> "Lihat, setiap volume besar ternyata harga naik."

Pernyataan tersebut mungkin muncul karena peneliti hanya mengingat beberapa grafik yang mendukungnya. Contoh yang berlawanan dapat terlupakan atau tidak dimasukkan.

SAMSON harus dirancang agar seluruh event yang memenuhi aturan dapat dicatat secara sistematis. Dengan demikian, penelitian tidak bergantung pada ingatan, intuisi, atau pemilihan grafik secara subjektif.

Prinsipnya:

> Semua event yang memenuhi definisi harus memiliki kesempatan yang sama untuk masuk ke analisis.

---

## 6.6. Batasan SAMSON v1.0

SAMSON v1.0 bukan sistem yang berlaku tanpa batas. Ia memiliki ruang lingkup, asumsi, dan batasan yang harus dihormati agar hasil penelitian tidak disalahartikan.

### 6.6.1. Timeframe dasar adalah 5 menit

Dalam kontrak SAMSON v1.0, timeframe dasar yang digunakan adalah **5 menit**.

Artinya, definisi:

- Volume.
- OHLC.
- RV.
- Baseline.
- Slot.
- Event.
- Horizon hasil.

semuanya dibangun berdasarkan bar 5 menit.

Timeframe 5 menit bukan berarti selalu paling baik. Ia hanya merupakan pilihan dasar yang telah ditetapkan untuk menjaga konsistensi penelitian.

Jika penelitian menggunakan timeframe 1 menit, 15 menit, 30 menit, atau harian, penelitian tersebut tidak boleh otomatis dianggap sebagai hasil SAMSON v1.0. Perubahan timeframe dapat mengubah:

- Struktur volume.
- Distribusi return.
- Frekuensi event.
- Pola noise.
- Baseline.
- Durasi reaksi harga.
- Ketergantungan antar-event.

Karena itu:

> Timeframe lain harus diperlakukan sebagai eksperimen terpisah atau versi kontrak baru.

### 6.6.2. Baseline harus sesuai sesi dan slot

Baseline SAMSON tidak boleh dibuat secara sembarangan dengan mencampurkan semua volume dari seluruh waktu.

Baseline harus mempertimbangkan konteks yang sebanding, termasuk:

- session_id.
- slot_id.
- slot_start.
- slot_end.
- Instrumen.
- Durasi bar.
- Data historis yang tersedia secara kausal.

Tujuannya adalah menghindari kesalahan ketika pola volume musiman dianggap sebagai anomali.

Contoh:

- Volume tinggi pada slot pembukaan mungkin normal.
- Volume yang sama pada tengah sesi mungkin tidak biasa.
- Volume tinggi setelah jeda mungkin memiliki baseline yang berbeda dari volume sebelum jeda.

Jika konteks waktu diabaikan, nilai RV dapat kehilangan makna.

### 6.6.3. Declustering diperlukan

Event SAMSON dapat muncul berkali-kali dalam waktu berdekatan. Misalnya, volume ekstrem terjadi selama lima bar berturut-turut.

Jika setiap bar diperlakukan sebagai observasi yang sepenuhnya independen, jumlah sampel dapat terlihat lebih besar daripada informasi yang sebenarnya tersedia.

Contoh:
09:30 — SAMSON
09:35 — SAMSON
09:40 — SAMSON
09:45 — SAMSON
09:50 — SAMSON


Kelima event tersebut mungkin merupakan bagian dari satu episode pasar yang sama, bukan lima kejadian yang benar-benar terpisah.

Inilah alasan **declustering** diperlukan.

Declustering dapat digunakan untuk:

- Menggabungkan event yang terlalu berdekatan.
- Menetapkan jarak minimum antar-event.
- Memilih satu event utama dari satu episode.
- Membentuk kelompok episode.
- Menggunakan unit analisis yang sesuai dengan ketergantungan data.

Aturan declustering harus ditentukan sebelum hasil digunakan untuk mengambil kesimpulan. Aturan tersebut juga harus dicatat dalam audit trail.

Tanpa declustering atau metode yang mengakui dependensi, ketidakpastian dapat terlihat lebih kecil daripada kenyataannya.

### 6.6.4. Hanya data yang memenuhi syarat penelitian

Tidak semua bar otomatis boleh masuk ke penelitian.

Data harus memenuhi persyaratan yang telah ditentukan, misalnya:

- Timestamp valid.
- Instrumen teridentifikasi dengan benar.
- OHLCV tidak rusak.
- Sesi dan slot dapat ditentukan.
- Volume tidak hilang atau tidak valid.
- Baseline dapat dihitung.
- Tidak terjadi pelanggaran aturan look-ahead.
- Data berada dalam rentang penelitian.
- Bar memenuhi aturan kelengkapan yang ditetapkan.

Jika baseline tidak dapat dihitung secara sah, event tidak boleh dipaksakan untuk diberi nilai RV.

Demikian pula, jika data outcome belum lengkap, hasil tidak boleh dianggap sebagai hasil lengkap hanya demi menambah jumlah observasi.

Status data yang tidak memenuhi syarat perlu dicatat secara eksplisit, misalnya:

- INVALID_DATA
- BASELINE_UNAVAILABLE
- INSUFFICIENT_HISTORY
- OUT_OF_SESSION
- EXCLUDED_BY_CONTRACT

Status tersebut membantu menjaga perbedaan antara:

- Tidak terjadi anomali.
- Anomali tidak dapat dihitung.
- Data tidak memenuhi syarat.
- Anomali terdeteksi tetapi outcome belum dapat dievaluasi.

Keempat keadaan tersebut tidak boleh disamakan.

### 6.6.5. SAMSON tidak boleh langsung diterjemahkan menjadi BUY atau SELL

Batasan terpenting SAMSON v1.0 adalah:

> SAMSON bukan sinyal BUY/SELL otomatis.

Aturan seperti berikut tidak boleh dianggap telah terbukti hanya karena RV tinggi:

> RV > 2,5 → BUY

atau:

> RV > 2,5 dan candle bullish → BUY

atau:

> RV > 5 dan harga turun → SELL

Semua aturan tersebut merupakan hipotesis yang masih harus diuji.

Jika ingin meneliti hubungan antara SAMSON dan arah harga, penelitian harus mendefinisikan:

- Event SAMSON.
- Arah candle.
- Titik observasi atau entry.
- Horizon.
- Return.
- B0.
- Biaya.
- Metode pengujian.
- Kriteria keputusan.
- Aturan OOS.

Bahkan setelah penelitian selesai, hasil positif tidak otomatis berarti aturan tersebut layak digunakan secara langsung. Hasil harus diperiksa dari sisi ukuran efek, ketidakpastian, biaya, stabilitas, dan generalisasi.

### 6.6.6. SAMSON tidak menjelaskan penyebab

SAMSON mendeteksi pola volume yang tidak biasa. Ia tidak menjelaskan secara otomatis mengapa volume tersebut terjadi.

Volume tinggi dapat disebabkan oleh banyak hal, misalnya:

- Berita.
- Perubahan indeks.
- Rebalancing.
- Aksi korporasi.
- Perubahan likuiditas.
- Kepanikan.
- Perpindahan posisi.
- Aktivitas algoritmik.
- Kesalahan atau masalah data.

Karena itu, SAMSON tidak boleh diperlakukan sebagai alat untuk mengidentifikasi motif pelaku pasar secara pasti.

SAMSON hanya memberikan observasi:

> "Aktivitas volume pada konteks ini lebih tinggi atau lebih rendah daripada baseline yang ditetapkan."

Penjelasan tentang penyebab memerlukan data dan penelitian tambahan.

### 6.6.7. SAMSON tidak menjamin adanya information edge

Detektor yang berhasil menemukan banyak kejadian anomali belum tentu menghasilkan informasi yang berguna untuk prediksi return.

Ada perbedaan antara:

- **Anomali statistik:** sesuatu berbeda dari kondisi normal.
- **Information edge:** kondisi tersebut memberikan informasi yang konsisten dan relevan terhadap outcome yang diteliti.

Contohnya, volume dapat sangat tidak biasa, tetapi arah return setelahnya tetap acak atau tidak berbeda dari B0. Dalam situasi tersebut, SAMSON berhasil mendeteksi anomali, tetapi penelitian belum menemukan edge yang dapat dibuktikan.

Hasil seperti itu bukan kegagalan sistem. Justru itulah fungsi penelitian:

> Membedakan sesuatu yang menarik secara visual dari sesuatu yang memiliki informasi terukur.

---

## Penutup Bab

SAMSON dalam TEKB adalah detektor anomali volume. Ia digunakan untuk menemukan kondisi ketika volume saat ini tidak biasa dibandingkan baseline yang relevan dan sebanding.

Konsep penting dalam SAMSON adalah:

- Volume absolut tidak sama dengan volume relatif.
- RV membandingkan volume saat ini dengan baseline.
- Baseline harus memperhatikan sesi dan slot waktu.
- `session_id`, `slot_id`, `slot_start`, dan `slot_end` membantu menjaga perbandingan tetap sebanding.
- Volume besar tidak otomatis berarti harga naik.
- Volume besar juga dapat diikuti penurunan atau pergerakan datar.
- Semua event harus dicatat, bukan hanya yang sesuai dugaan.
- Event yang berdekatan perlu diperlakukan dengan memperhatikan dependensi atau declustering.
- Timeframe lain harus dianggap sebagai eksperimen terpisah.
- SAMSON bukan keputusan entry dan bukan sinyal BUY/SELL otomatis.

Dengan demikian, SAMSON hanya membuka pintu pertanyaan:

> "Ketika aktivitas volume tidak biasa terjadi, apa yang sebenarnya terjadi pada harga setelahnya, dan apakah hasilnya berbeda dari pembanding yang adil?"

Pertanyaan tersebut baru dapat dijawab melalui pengukuran, distribusi, pembandingan, pengujian ketidakpastian, dan validasi OOS.

Prinsip TEKB tetap berlaku:

> **Bukti dulu, keputusan belakangan.**

---

## Ringkasan Bab

- SAMSON adalah detektor anomali volume dalam TEKB.
- Volume absolut tidak sama dengan volume relatif (RV).
- RV membandingkan volume saat ini dengan baseline yang sebanding.
- Baseline harus memperhatikan sesi dan slot waktu.
- Volume besar tidak otomatis berarti harga naik atau turun.
- Semua event harus dicatat, bukan hanya yang sesuai dugaan.
- Declustering diperlukan untuk event yang berdekatan.
- SAMSON bukan sinyal BUY/SELL otomatis.
- SAMSON tidak menjelaskan penyebab dan tidak menjamin adanya edge.

---

## Pertanyaan Refleksi

1. Mengapa volume besar belum tentu tidak biasa?
2. Apa perbedaan antara volume absolut dan volume relatif?
3. Mengapa baseline harus memperhatikan sesi dan slot waktu?
4. Apa fungsi `session_id`, `slot_id`, `slot_start`, dan `slot_end`?
5. Mengapa tiga event dengan RV yang sama bisa menghasilkan hasil yang berbeda?
6. Mengapa declustering diperlukan?
7. Mengapa SAMSON tidak boleh langsung diterjemahkan menjadi BUY/SELL?
8. Apa perbedaan antara anomali statistik dan information edge?
9. Mengapa SAMSON tidak menjelaskan penyebab volume?
10. Apa prinsip utama TEKB yang tetap berlaku dalam SAMSON?

---

<div align="center">

[← Bab Sebelumnya](/posts/bab-05-mengenal-data-ohlcv/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Bab Selanjutnya →](/posts/bab-07-dari-ada-sinyal/)

</div>
