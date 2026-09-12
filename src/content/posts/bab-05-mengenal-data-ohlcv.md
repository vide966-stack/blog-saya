---
title: "BAB 5 — Mengenal Data OHLCV Tanpa Takut Rumus"
published: 2026-09-12
description: "Mengenal bahan dasar penelitian TEKB: bar harga, OHLC, volume, timeframe, dan kualitas data. Tanpa perlu takut rumus."
tags: ["bab-5", "ohlcv", "data", "timeframe"]
category: "Bab"
draft: false
lang: ""
---

**BAGIAN II — MEMBANGUN BAHASA DAN DATA PENELITIAN**

---

Sebelum meneliti apakah suatu sinyal trading memiliki informasi yang berguna, kita perlu mengenal bahan dasar yang digunakan dalam penelitian tersebut. Dalam TEKB, bahan dasar itu terutama berupa data harga dan volume yang dikenal dengan istilah OHLCV.

Bagi sebagian orang, istilah OHLCV mungkin terdengar teknis. Padahal, isinya sangat dekat dengan informasi yang biasa kita lihat pada grafik saham, forex, atau aset kripto. OHLCV pada dasarnya menjawab lima pertanyaan sederhana:

- Harga dibuka pada tingkat berapa?
- Harga tertinggi yang tercapai berapa?
- Harga terendah yang tercapai berapa?
- Harga ditutup pada tingkat berapa?
- Berapa banyak aktivitas transaksi yang tercatat?

Lima informasi tersebut menjadi dasar untuk membentuk candle, menghitung perubahan harga, membaca aktivitas volume, mengenali kejadian tertentu, dan mengukur apa yang terjadi setelah suatu event.

Namun, data OHLCV bukanlah jawaban otomatis atas pertanyaan "harga akan naik atau turun?". Data ini adalah bahan mentah penelitian. Agar dapat menghasilkan kesimpulan yang dapat dipercaya, data harus ditempatkan dalam konteks waktu, aturan penggunaan, dan pemeriksaan kualitas yang jelas.

---

## 5.1. Apa Itu Satu Bar Harga?

### Bar sebagai Ringkasan Aktivitas Harga

Satu bar harga adalah ringkasan pergerakan harga selama suatu periode waktu tertentu. Jika kita menggunakan bar harian, satu bar merangkum aktivitas perdagangan selama satu hari. Jika kita menggunakan bar 5 menit, satu bar merangkum aktivitas selama lima menit.

Dengan demikian, satu bar bukanlah satu transaksi. Satu bar merupakan kumpulan informasi dari banyak transaksi yang terjadi dalam rentang waktu tertentu.

Bayangkan kita ingin mengetahui keadaan sebuah jalan raya. Kita dapat mencatat seluruh kendaraan yang lewat satu per satu, tetapi cara itu akan menghasilkan data yang sangat besar. Sebagai ringkasan, kita bisa mencatat kondisi jalan setiap lima menit: berapa kendaraan yang terlihat, apakah lalu lintas padat, dan apakah kecepatan rata-ratanya berubah.

Bar harga bekerja dengan gagasan yang serupa. Ia merangkum aktivitas pasar selama periode tertentu agar dapat dianalisis secara sistematis.

### Bar Harian

Pada bar harian, satu bar biasanya mewakili satu hari perdagangan. Contohnya:

- Open: 1.000
- High: 1.080
- Low: 980
- Close: 1.050
- Volume: 20 juta saham

Artinya, selama hari tersebut, harga pembukaan berada di 1.000, harga tertinggi yang tercapai adalah 1.080, harga terendah adalah 980, dan harga penutupan berada di 1.050.

Bar harian berguna untuk penelitian yang ingin melihat pola dalam rentang hari, minggu, bulan, atau tahun. Misalnya, apakah suatu kondisi volume pada hari ini diikuti oleh perubahan harga selama satu sampai lima hari berikutnya?

### Bar Intraday

Bar intraday adalah bar yang memiliki periode lebih pendek daripada satu hari. Contohnya:

- Bar 5 menit
- Bar 15 menit
- Bar 30 menit
- Bar 1 jam

Misalnya, pada bar 5 menit, data OHLCV merangkum aktivitas perdagangan dari pukul 09.00 sampai 09.05. Bar berikutnya dapat merangkum pukul 09.05 sampai 09.10, dan seterusnya.

Bar intraday memungkinkan peneliti mengamati kejadian yang lebih cepat. Misalnya, peneliti ingin mengetahui apa yang biasanya terjadi pada bar berikutnya setelah muncul volume yang sangat besar. Dalam penelitian semacam ini, ketepatan waktu menjadi sangat penting.

### Hubungan Bar dan Waktu Pengamatan

Setiap bar harus memiliki identitas waktu yang jelas. Peneliti perlu mengetahui:

- Kapan periode bar dimulai.
- Kapan periode bar berakhir.
- Apakah waktu yang digunakan adalah waktu bursa, waktu lokal, atau waktu standar tertentu.
- Apakah bar tersebut sudah selesai atau masih berjalan.

Perbedaan ini penting karena sebuah bar yang belum selesai masih dapat berubah. High, Low, Close, dan Volume dapat bertambah atau berubah selama periode bar berlangsung.

Sebagai contoh, pada pukul 09.03, bar 5 menit yang dimulai pukul 09.00 belum selesai. Harga penutupan sementara pada pukul 09.03 bukanlah Close final untuk bar tersebut. Close baru diketahui setelah periode bar berakhir.

Karena itu, penelitian TEKB harus membedakan antara informasi yang tersedia ketika bar masih berjalan dan informasi yang baru sah digunakan setelah bar ditutup.

### Mengapa Bar Penting dalam Penelitian?

Bar menjadi unit dasar pengamatan. Peneliti dapat mengatakan:

> "Pada bar T terjadi volume ekstrem."

> "Setelah bar T ditutup, entry dilakukan pada pembukaan bar berikutnya."

> "Perubahan harga diukur dari entry hingga lima bar berikutnya."

Dengan adanya bar, penelitian memiliki struktur waktu yang jelas. Tanpa struktur tersebut, sulit menentukan kapan suatu informasi diketahui, kapan keputusan dianggap dibuat, dan kapan hasil mulai diukur.

---

## 5.2. Open, High, Low, dan Close

Empat komponen utama harga dalam OHLC adalah Open, High, Low, dan Close. Keempatnya sering disingkat menjadi OHLC.

### Open: Harga Pembukaan

**Open** adalah harga pembukaan pada awal periode bar.

Pada bar harian, Open biasanya merupakan harga perdagangan pertama yang digunakan untuk membentuk sesi hari tersebut, sesuai dengan definisi dan sumber data yang digunakan.

Pada bar intraday, Open adalah harga awal dari periode bar tersebut.

Contoh:

> Jika bar 5 menit dimulai pada pukul 09.00 dan transaksi pertama yang tercatat berada di harga 1.000, maka Open bar tersebut adalah 1.000.

Open berguna untuk mengetahui dari tingkat harga mana aktivitas pada periode itu dimulai.

### High: Harga Tertinggi

**High** adalah harga tertinggi yang tercapai selama periode bar.

Misalnya, dalam satu bar harga bergerak dari 1.000 ke 1.030, kemudian turun, lalu naik lagi ke 1.050. Jika 1.050 merupakan harga tertinggi yang tercatat selama periode tersebut, maka High bar itu adalah 1.050.

High membantu peneliti mengetahui seberapa jauh harga sempat bergerak ke atas selama periode pengamatan.

Namun, High tidak menjelaskan urutan perjalanan harga secara lengkap. Dua bar dapat memiliki Open, High, Low, dan Close yang sama, tetapi jalur pergerakannya di dalam bar bisa berbeda.

### Low: Harga Terendah

**Low** adalah harga terendah yang tercapai selama periode bar.

Jika harga sempat turun hingga 980, lalu kembali naik dan ditutup di 1.050, maka Low bar tersebut adalah 980.

Low membantu peneliti mengukur seberapa jauh harga sempat bergerak ke bawah. Dalam penelitian risiko, Low juga dapat digunakan untuk mengetahui apakah harga pernah mencapai tingkat tertentu setelah entry.

### Close: Harga Penutupan

**Close** adalah harga penutupan yang digunakan untuk mengakhiri periode bar.

Close sering menjadi angka yang paling banyak digunakan dalam analisis karena dapat menjadi penanda kondisi terakhir pada periode tersebut. Misalnya, peneliti dapat menghitung perubahan harga dari Close hari ini ke Close hari berikutnya.

Namun, Close hanya dapat diketahui secara final setelah bar selesai. Menggunakan Close final sebelum periode bar berakhir dapat menimbulkan look-ahead bias.

### Contoh Satu Candle

Misalkan sebuah saham memiliki data berikut pada satu bar harian:

| Komponen | Nilai |
|---|---|
| Open | 1.000 |
| High | 1.100 |
| Low | 950 |
| Close | 1.050 |
| Volume | 10.000.000 |

Dari data tersebut, kita dapat membaca beberapa hal:

- Harga dibuka pada 1.000.
- Harga sempat naik hingga 1.100.
- Harga sempat turun hingga 950.
- Harga ditutup pada 1.050.
- Aktivitas volume yang tercatat adalah 10 juta saham.

Karena Close lebih tinggi daripada Open, bar tersebut dapat disebut sebagai bar bullish atau bar naik. Akan tetapi, istilah bullish hanya menggambarkan hubungan Open dan Close pada bar itu. Istilah tersebut belum membuktikan bahwa harga akan naik pada bar berikutnya.

### Range Harga

Dari OHLC, kita juga dapat menghitung rentang harga sederhana:

> Range = High − Low

Pada contoh di atas:

> Range = 1.100 − 950 = 150

Artinya, selama periode tersebut, jarak antara harga tertinggi dan terendah adalah 150 poin harga.

Range menunjukkan luas pergerakan harga dalam satu bar, tetapi tidak secara langsung menjelaskan arah masa depan. Range besar bisa terjadi ketika pasar sedang aktif, panik, bereaksi terhadap berita, atau mengalami ketidakpastian tinggi.

### Body dan Arah Candle

Kita juga dapat melihat perbedaan antara Close dan Open:

> Body = Close − Open

Pada contoh:

> Body = 1.050 − 1.000 = 50

Nilai positif menunjukkan Close berada di atas Open. Nilai negatif menunjukkan Close berada di bawah Open.

Namun, body yang positif tidak otomatis berarti tekanan beli lebih kuat dalam arti yang lengkap. Body hanya menunjukkan posisi awal dan akhir harga, bukan seluruh proses transaksi yang terjadi di antara keduanya.

---

## 5.3. Volume

### Apa yang Diukur Volume?

**Volume** adalah jumlah aktivitas transaksi yang tercatat selama periode tertentu, sesuai dengan definisi volume dari sumber data yang digunakan.

Pada saham, volume biasanya dinyatakan dalam jumlah saham yang diperdagangkan. Pada instrumen lain, definisinya dapat berbeda. Misalnya, pada sebagian pasar forex, data yang tersedia dapat berupa tick volume, yaitu jumlah perubahan atau pembaruan harga yang tercatat, bukan selalu jumlah unit mata uang yang benar-benar berpindah.

Karena itu, sebelum menggunakan volume, peneliti harus mengetahui terlebih dahulu apa yang sebenarnya diukur oleh sumber data tersebut.

Untuk saham, contoh volume dapat berupa:

- 100.000 saham dalam satu bar.
- 5.000.000 saham dalam satu hari.
- 20.000.000 saham dalam satu sesi.

Volume memberi gambaran tentang seberapa besar aktivitas transaksi yang tercatat selama periode tersebut.

### Volume Bukan Otomatis Tekanan Beli

Kesalahan yang sering terjadi adalah menganggap volume besar selalu berarti tekanan beli besar. Padahal, setiap transaksi melibatkan pihak yang membeli dan pihak yang menjual.

Jika terjadi transaksi sebanyak 1 juta saham, angka tersebut tidak berarti 1 juta saham hanya dibeli tanpa ada pihak yang menjual. Volume mencerminkan aktivitas pertukaran, bukan arah transaksi secara otomatis.

Volume besar dapat muncul ketika:

- Banyak pelaku pasar membeli dan menjual secara aktif.
- Sebagian pelaku melakukan pembelian, sementara yang lain melakukan penjualan.
- Terjadi perpindahan kepemilikan dalam jumlah besar.
- Pasar merespons berita atau informasi tertentu.
- Terjadi kepanikan, distribusi, akumulasi, atau perubahan posisi.

Namun, istilah seperti "akumulasi" atau "distribusi" tidak boleh langsung dianggap sebagai fakta hanya karena volume besar terlihat. Istilah tersebut merupakan interpretasi yang membutuhkan definisi dan pengujian.

### Volume Besar Harus Dibaca Bersama Konteks Harga

Volume yang besar baru menjadi lebih informatif ketika dibaca bersama pergerakan harga.

Misalnya, dua bar sama-sama memiliki volume 10 juta saham:

- **Bar A:** Open 1.000, High 1.020, Low 990, Close 1.015.
- **Bar B:** Open 1.000, High 1.100, Low 900, Close 1.005.

Keduanya memiliki volume yang sama, tetapi bentuk pergerakan harganya berbeda. Bar A memiliki rentang sempit dan ditutup dekat bagian atas. Bar B memiliki rentang sangat lebar, sempat naik dan turun jauh, tetapi ditutup hampir dekat harga pembukaan.

Konteks tersebut dapat memberi pertanyaan penelitian yang berbeda:

- Apakah volume besar dengan close dekat high memiliki hasil berikutnya yang berbeda?
- Apakah volume besar dengan rentang lebar tetapi close dekat open menunjukkan ketidakpastian?
- Apakah volume besar pada bar turun memiliki karakter hasil yang berbeda dari volume besar pada bar naik?

Pertanyaan tersebut lebih tepat daripada langsung menyimpulkan "volume besar berarti harga akan naik".

### Aktivitas Transaksi dan Arah Harga adalah Dua Hal Berbeda

Volume menjawab pertanyaan:

> Seberapa besar aktivitas transaksi yang tercatat?

Sementara itu, perubahan harga menjawab pertanyaan:

> Ke mana harga berpindah selama periode tersebut?

Keduanya berhubungan, tetapi tidak identik.

Sebuah bar dapat memiliki volume besar tetapi perubahan harga kecil. Ini bisa menunjukkan bahwa aktivitas transaksi tinggi tidak menghasilkan perpindahan harga yang besar selama periode tersebut.

Sebaliknya, sebuah bar dapat memiliki volume relatif lebih kecil tetapi harga bergerak cukup jauh, tergantung kondisi likuiditas dan struktur pasar.

Dalam TEKB, volume tidak langsung diperlakukan sebagai "tekanan beli" atau "tekanan jual" yang sudah terbukti. Volume diperlakukan sebagai variabel observasi yang dapat dikombinasikan dengan informasi harga untuk membentuk event penelitian.

### Contoh Sederhana

Bayangkan sebuah pasar memiliki dua situasi:

**Situasi pertama:**

- Banyak orang melakukan transaksi.
- Harga hanya bergerak sedikit.

**Situasi kedua:**

- Aktivitas transaksi lebih sedikit.
- Harga bergerak cukup jauh karena likuiditas lebih tipis.

Kedua situasi menunjukkan bahwa jumlah aktivitas dan arah pergerakan harga adalah dua dimensi yang berbeda.

Karena itu, dalam penelitian, volume sebaiknya tidak berdiri sendiri. Peneliti perlu menjelaskan volume dibandingkan dengan apa, pada periode mana, dan dalam konteks harga seperti apa.

### Volume Relatif

Volume mentah sering kali belum cukup untuk dibandingkan. Volume 5 juta saham mungkin sangat besar untuk satu saham, tetapi biasa saja untuk saham lain. Volume 5 juta pada awal sesi juga tidak selalu dapat dibandingkan langsung dengan volume 5 juta pada siang hari.

Karena itu, TEKB dapat menggunakan **volume relatif**, misalnya dengan membandingkan volume saat ini terhadap baseline volume yang sesuai.

Secara sederhana:

> RV = Volume saat ini ÷ Volume pembanding

Jika volume saat ini 10 juta dan volume pembanding 2 juta, maka:

> RV = 10 juta ÷ 2 juta = 5

Artinya, volume saat ini lima kali volume pembanding.

Angka tersebut belum berarti harga pasti naik atau turun. RV hanya membantu mengidentifikasi bahwa aktivitas volume saat ini relatif tidak biasa dibandingkan dengan acuan yang digunakan.

Dalam SAMSON v1.0, konsep volume relatif digunakan untuk membantu mendeteksi anomali volume. Namun, definisi baseline, sesi, slot waktu, dan aturan pengelompokan event harus ditetapkan secara eksplisit agar hasil penelitian tidak bias.

---

## 5.4. Timeframe

### Apa Itu Timeframe?

**Timeframe** adalah panjang periode yang digunakan untuk membentuk satu bar.

Beberapa contoh timeframe:

- **5 menit:** satu bar merangkum aktivitas selama lima menit.
- **15 menit:** satu bar merangkum aktivitas selama lima belas menit.
- **1 jam:** satu bar merangkum aktivitas selama satu jam.
- **1 hari:** satu bar merangkum aktivitas selama satu hari perdagangan.

Timeframe menentukan skala pengamatan. Peristiwa yang terlihat jelas pada timeframe 5 menit belum tentu terlihat dengan cara yang sama pada timeframe harian.

### Timeframe 5 Menit

Pada timeframe 5 menit, peneliti dapat mengamati perubahan harga dan volume secara lebih rinci. Misalnya, peneliti ingin mengetahui apa yang terjadi setelah sebuah bar mengalami volume ekstrem.

Jika bar sinyal ditutup pada pukul 10.05, penelitian dapat menetapkan bahwa entry dilakukan pada pembukaan bar valid berikutnya, misalnya pukul 10.10, sesuai aturan yang telah ditentukan.

Timeframe 5 menit cocok untuk penelitian yang membutuhkan pengamatan intraday, tetapi juga memiliki tantangan:

- Banyak bar yang saling berdekatan.
- Event dapat terjadi berulang kali dalam waktu singkat.
- Bar dapat saling tumpang tindih dalam horizon pengukuran.
- Jadwal perdagangan dan jeda sesi dapat memengaruhi volume.
- Data harus memperhatikan slot waktu agar perbandingan adil.

### Timeframe 15 Menit

Pada timeframe 15 menit, setiap bar merangkum aktivitas yang lebih panjang daripada bar 5 menit. Detail pergerakan di dalam 15 menit tidak terlihat secara lengkap.

Timeframe ini dapat mengurangi jumlah bar dan sebagian noise, tetapi juga dapat menyembunyikan kejadian yang hanya berlangsung singkat.

Misalnya, volume ekstrem yang terjadi selama tiga menit mungkin terlihat sangat jelas pada timeframe 5 menit, tetapi menjadi bagian kecil dari satu bar 15 menit.

### Timeframe 1 Jam

Timeframe 1 jam digunakan untuk mengamati pergerakan dalam skala intraday yang lebih luas. Satu bar dapat mencakup beberapa perubahan kecil yang terjadi selama satu jam.

Timeframe ini dapat berguna untuk penelitian yang ingin mengamati kondisi pasar dalam rentang lebih panjang, tetapi tidak boleh dianggap otomatis lebih baik daripada timeframe lain. Kegunaannya bergantung pada pertanyaan penelitian.

### Timeframe 1 Hari

Timeframe harian merangkum aktivitas selama satu hari perdagangan. Timeframe ini umum digunakan untuk penelitian yang mengukur hasil satu sampai beberapa hari setelah event.

Misalnya:

- Event terjadi pada hari T.
- Entry dilakukan pada pembukaan hari T+1.
- Return diukur sampai penutupan hari T+3.

Penelitian harian memiliki struktur waktu yang berbeda dari penelitian intraday. Oleh sebab itu, definisi event, entry, horizon, baseline volume, dan pembanding harus disesuaikan dengan timeframe yang digunakan.

### Mengapa Hasil Antar-Timeframe Tidak Boleh Dicampur Sembarangan?

Satu event pada timeframe 5 menit tidak sama dengan satu event pada timeframe harian. Perbedaan tersebut bukan hanya soal panjang waktu, tetapi juga menyangkut:

- Jumlah observasi.
- Struktur pasar.
- Jadwal perdagangan.
- Likuiditas.
- Pola volume.
- Biaya transaksi.
- Jarak waktu antara event dan entry.
- Arti return setelah event.

Misalnya, return 0,5% dalam lima menit tidak dapat langsung dibandingkan dengan return 0,5% dalam satu hari tanpa mempertimbangkan risiko, volatilitas, biaya, dan konteks waktunya.

Jika data dari berbagai timeframe dicampur tanpa aturan, hasil penelitian dapat menjadi sulit ditafsirkan. Peneliti tidak lagi jelas sedang mengukur fenomena yang mana.

Karena itu, setiap penelitian harus menyebutkan timeframe secara eksplisit dan menjaga konsistensinya.

### Timeframe Dasar SAMSON v1.0

Dalam rancangan TEKB yang dibahas dalam buku ini, SAMSON v1.0 menggunakan timeframe dasar **5 menit** untuk penelitian intraday.

Artinya, event SAMSON, perhitungan volume relatif, penentuan slot, dan pengukuran hasil harus mengikuti kerangka waktu 5 menit yang telah ditetapkan.

Timeframe tersebut bukan klaim bahwa 5 menit selalu merupakan timeframe terbaik. Ia merupakan pilihan metodologis yang harus dikunci agar penelitian dapat direplikasi dan hasilnya dapat dibandingkan secara konsisten.

Jika suatu hari timeframe SAMSON diubah menjadi 15 menit atau 1 jam, perubahan tersebut harus diperlakukan sebagai perubahan definisi penelitian atau versi metodologi baru, bukan sekadar mengganti angka tanpa mencatat dampaknya.

---

## 5.5. Data yang Tersedia versus Data yang Boleh Digunakan

Salah satu prinsip paling penting dalam penelitian trading adalah membedakan antara data yang tercatat dalam database dan informasi yang benar-benar sudah tersedia pada saat keputusan dibuat.

Database dapat menyimpan seluruh sejarah pasar. Namun, seorang trader yang berada pada waktu tertentu tidak mengetahui masa depan. Penelitian harus meniru batas pengetahuan tersebut.

### Informasi yang Sudah Diketahui Saat Keputusan

Misalnya, sebuah bar T telah selesai. Pada saat penutupan bar T, peneliti mungkin sudah mengetahui:

- Open bar T.
- High bar T.
- Low bar T.
- Close bar T.
- Volume bar T.
- Data historis sebelum bar T.

Jika aturan penelitian menyatakan bahwa sinyal dibentuk setelah bar T ditutup, informasi tersebut dapat digunakan untuk menentukan apakah event terjadi.

Namun, peneliti tidak boleh menggunakan informasi yang baru diketahui setelah waktu tersebut.

### Informasi yang Baru Diketahui Setelah Bar Ditutup

Selama bar T masih berjalan, nilai High, Low, Close, dan Volume belum final. Nilainya dapat berubah sampai bar ditutup.

Contohnya, pada pukul 10.03 dalam bar 5 menit pukul 10.00–10.05:

- Harga tertinggi sementara belum tentu High final.
- Harga terendah sementara belum tentu Low final.
- Close sementara belum tentu Close final.
- Volume sementara belum tentu Volume final.

Jika penelitian mengklaim bahwa sinyal hanya dibuat setelah bar selesai, maka nilai final tersebut baru boleh digunakan setelah pukul 10.05.

Menggunakan nilai final sebelum waktu tersebut berarti penelitian memakai informasi yang pada kenyataannya belum tersedia.

### Contoh Look-Ahead yang Sederhana

Misalkan peneliti ingin menguji aturan:

> Jika Close hari ini menembus High 20 hari sebelumnya, maka beli pada pembukaan hari berikutnya.

Aturan tersebut dapat diterapkan secara kausal jika Close hari ini memang sudah diketahui ketika keputusan dibuat dan entry dilakukan pada pembukaan hari berikutnya.

Namun, jika peneliti menggunakan High atau Low hari berikutnya untuk menentukan apakah sinyal hari ini valid, maka aturan tersebut telah melihat masa depan.

Contoh lain:

- Memilih hanya event yang ternyata menghasilkan profit.
- Menggunakan harga tertinggi setelah entry untuk menentukan apakah entry layak dilakukan.
- Menentukan parameter berdasarkan hasil OOS lalu mengklaim OOS tersebut sebagai pengujian murni.
- Menggunakan informasi corporate action yang baru diumumkan setelah waktu keputusan.

### Data Historis Tidak Sama dengan Information Availability

Data historis adalah catatan yang tersedia sekarang tentang kejadian masa lalu. **Information availability** adalah pertanyaan: kapan informasi tersebut benar-benar dapat diketahui oleh sistem atau pelaku pasar pada saat itu?

Perbedaan ini sangat penting.

Misalnya, sebuah database hari ini telah diperbaiki dan memasukkan harga yang sudah disesuaikan akibat stock split. Harga tersebut mungkin berguna untuk analisis return historis, tetapi peneliti harus memahami bagaimana penyesuaian itu dibuat dan apakah penggunaannya konsisten dengan definisi penelitian.

Demikian pula, data fundamental yang tercatat dalam database mungkin memiliki tanggal periode laporan, tanggal publikasi, dan tanggal tersedia untuk pasar yang berbeda. Menggunakan tanggal periode laporan seolah-olah informasi sudah diketahui pada hari itu dapat menimbulkan bias.

Walaupun penelitian TEKB dalam bab ini berfokus pada OHLCV, prinsipnya tetap sama: data yang tersimpan sekarang tidak otomatis berarti data tersebut tersedia pada waktu keputusan historis.

### Hubungan dengan No-Look-Ahead

**No-look-ahead** berarti penelitian tidak menggunakan informasi masa depan ketika menentukan event, entry, pemilihan sampel, atau aturan keputusan.

Dalam praktik TEKB, peneliti harus memisahkan beberapa waktu penting:

- Waktu event atau sinyal terbentuk.
- Waktu konfirmasi, jika ada.
- Waktu informasi tersedia.
- Waktu entry.
- Waktu evaluasi hasil.

Sebagai contoh:

- Bar T selesai.
- Sistem membaca OHLCV yang tersedia sampai bar T.
- Event dinyatakan terjadi.
- Entry dilakukan pada pembukaan bar valid berikutnya.
- Hasil mulai diukur setelah entry.

Dengan urutan ini, informasi pada masa depan tidak digunakan untuk membentuk keputusan masa lalu.

### Mengapa Aturan Waktu Harus Ditulis?

Kalimat seperti "beli ketika volume besar" masih terlalu kabur. Peneliti perlu menjelaskan:

- Volume besar dibandingkan dengan baseline apa?
- Sinyal dianggap valid ketika bar sedang berjalan atau setelah ditutup?
- Entry dilakukan pada harga apa?
- Jika pembukaan berikutnya mengalami gap, apa yang dilakukan?
- Apakah bar yang tidak valid dilewati?
- Kapan pengukuran hasil dimulai?

Semakin jelas aturan waktu, semakin kecil ruang bagi peneliti untuk secara tidak sadar menggunakan informasi masa depan.

---

## 5.6. Data Tidak Selalu Sempurna

Data pasar sering terlihat rapi dalam bentuk tabel. Namun, kerapian tabel tidak menjamin bahwa seluruh isinya benar, lengkap, atau sesuai untuk penelitian tertentu.

Data dapat mengandung masalah teknis, masalah waktu, perubahan definisi, atau perubahan kondisi perdagangan. Jika masalah tersebut diabaikan, kesimpulan penelitian dapat terlihat meyakinkan tetapi sebenarnya rapuh.

### Bar Tidak Valid

**Bar tidak valid** adalah bar yang tidak memenuhi aturan kualitas data yang telah ditetapkan.

Contoh masalah:

- High lebih rendah daripada Low.
- Open berada di luar rentang High–Low.
- Close berada di luar rentang High–Low.
- Volume bernilai negatif.
- Timestamp tidak sesuai urutan.
- Nilai harga kosong atau tidak masuk akal.

Secara umum, hubungan dasar OHLC yang wajar adalah:

> Low ≤ Open ≤ High

> Low ≤ Close ≤ High

Jika hubungan tersebut dilanggar, bar perlu diperiksa. Peneliti tidak boleh langsung menggunakannya seolah-olah valid.

Namun, tidak semua masalah harus diselesaikan dengan cara yang sama. Sebagian bar mungkin dapat diperbaiki jika sumber data menyediakan koreksi yang dapat ditelusuri. Sebagian lainnya harus dikeluarkan dari penelitian dan dicatat sebagai data bermasalah.

### Data Hilang

**Data hilang** terjadi ketika periode yang seharusnya memiliki bar tidak memiliki catatan yang tersedia.

Contohnya:

- Tidak ada bar pada periode perdagangan tertentu.
- Sebagian data intraday hilang.
- Data hanya tersedia untuk sebagian tahun.
- Ada jeda yang tidak dijelaskan.

Data hilang dapat memengaruhi hasil penelitian. Misalnya, jika peneliti mengukur return lima bar setelah event, tetapi dua bar di antaranya hilang, maka horizon lima bar tersebut mungkin tidak lagi mewakili lima periode perdagangan yang sebenarnya.

Karena itu, TEKB perlu membedakan antara:

- Data benar-benar tidak tersedia.
- Pasar memang tidak diperdagangkan.
- Pasar sedang mengalami jeda resmi.
- Data gagal dikumpulkan.

Keempat keadaan tersebut tidak selalu memiliki arti yang sama.

### Market Break dan Jeda Perdagangan

**Market break** adalah jeda atau penghentian perdagangan yang dapat terjadi karena jadwal pasar, mekanisme bursa, gangguan teknis, atau keadaan luar biasa.

Pada pasar tertentu, perdagangan memang memiliki jeda sesi. Misalnya, sesi pagi dapat berakhir sebelum sesi siang dimulai kembali.

Dalam data intraday, jeda tersebut tidak boleh otomatis dianggap sebagai bar yang hilang atau sebagai periode dengan volume nol. Jeda resmi adalah bagian dari struktur pasar.

Peneliti perlu memahami:

- Jam perdagangan resmi.
- Sesi perdagangan.
- Waktu istirahat.
- Perubahan jadwal.
- Hari libur bursa.
- Penghentian perdagangan.

Untuk SAMSON v1.0, struktur sesi dan slot waktu menjadi penting karena volume pada awal sesi, tengah sesi, dan akhir sesi dapat memiliki karakter yang berbeda.

### Perubahan Jadwal Perdagangan

Jadwal perdagangan dapat berubah karena kebijakan bursa, hari libur, perubahan zona waktu, atau perubahan mekanisme perdagangan.

Jika peneliti menggunakan baseline volume tanpa memperhatikan perubahan jadwal, perbandingan dapat menjadi tidak adil.

Misalnya, volume pada bar pertama sesi tidak tepat dibandingkan dengan volume pada bar tengah sesi. Demikian pula, volume sebelum perubahan jadwal tidak selalu dapat langsung dibandingkan dengan volume setelah perubahan jadwal tanpa penyesuaian.

Karena itu, penelitian intraday perlu menggunakan struktur waktu yang konsisten dan mencatat perubahan jadwal yang relevan.

### Corporate Action

**Corporate action** adalah tindakan perusahaan yang dapat memengaruhi harga atau jumlah saham, misalnya:

- Stock split.
- Reverse stock split.
- Dividen.
- Right issue.
- Buyback.
- Merger.
- Perubahan jumlah saham beredar.

Corporate action dapat membuat harga historis terlihat melonjak atau turun secara mekanis, meskipun perubahan tersebut tidak selalu mencerminkan keuntungan atau kerugian ekonomi yang sebenarnya bagi pemegang saham.

Contohnya, jika satu saham dengan harga 10.000 melakukan stock split 1:2, harga teoritisnya dapat berubah menjadi sekitar 5.000 per saham. Grafik harga mentah akan terlihat seperti penurunan besar, padahal jumlah saham yang dimiliki investor juga berubah.

Karena itu, peneliti perlu mengetahui apakah data yang digunakan:

- Raw atau belum disesuaikan.
- Adjusted atau sudah disesuaikan.
- Disesuaikan untuk dividen.
- Disesuaikan untuk stock split.
- Konsisten antara harga dan volume.

Tidak ada satu jenis penyesuaian yang selalu benar untuk semua penelitian. Yang paling penting adalah kesesuaian antara jenis data, tujuan pengukuran, dan definisi penelitian.

### Penyesuaian Harga dan Konsistensi Volume

Jika harga disesuaikan akibat corporate action, volume juga mungkin perlu dipahami dalam konteks penyesuaian tersebut.

Misalnya, setelah stock split, jumlah saham yang diperdagangkan dapat berubah secara mekanis. Jika harga menggunakan data adjusted tetapi volume menggunakan definisi yang tidak konsisten, perhitungan seperti nilai transaksi, volume relatif, atau indikator berbasis harga dan volume dapat menjadi keliru.

Karena itu, peneliti tidak cukup hanya bertanya:

> Apakah harga sudah adjusted?

Peneliti juga perlu bertanya:

> Apakah seluruh variabel yang digunakan konsisten dengan penyesuaian tersebut?

### Mengapa Kualitas Data Memengaruhi Kesimpulan?

Bayangkan seseorang ingin menilai kemampuan seorang pelari, tetapi sebagian hasil lombanya hilang, beberapa jarak lomba berubah, dan sebagian waktu dicatat dengan alat yang rusak. Kesimpulan tentang kemampuan pelari tersebut tentu tidak dapat dipercaya sepenuhnya.

Penelitian trading menghadapi masalah yang sama. Jika data mengandung kesalahan, maka:

- Event dapat salah terdeteksi.
- Entry dapat salah ditentukan.
- Return dapat salah dihitung.
- MAE dan MFE dapat salah diukur.
- Baseline dapat menjadi tidak adil.
- Jumlah sampel dapat keliru.
- Hasil yang terlihat signifikan dapat sebenarnya berasal dari masalah data.

Karena itu, pemeriksaan kualitas data bukan pekerjaan tambahan yang tidak penting. Ia merupakan bagian dari penelitian itu sendiri.

### Prinsip Praktis Pemeriksaan Data

Sebelum menggunakan data OHLCV, peneliti sebaiknya memiliki pemeriksaan minimum:

- Memastikan timestamp tersusun benar.
- Memeriksa hubungan logis antara Open, High, Low, dan Close.
- Memeriksa nilai volume yang kosong, negatif, atau tidak wajar.
- Memeriksa duplikasi bar.
- Memeriksa periode yang hilang.
- Memahami jadwal sesi dan market break.
- Memeriksa perubahan jadwal perdagangan.
- Mengetahui apakah data raw atau adjusted.
- Memastikan harga dan volume konsisten.
- Mencatat bar yang dikeluarkan dan alasan pengeluarannya.

Pemeriksaan tersebut tidak menjamin data sempurna. Namun, pemeriksaan itu membantu membuat keterbatasan data terlihat dan dapat diaudit.

---

## Ringkasan Bab

- OHLCV adalah bahan dasar penelitian TEKB. Satu bar merangkum aktivitas harga dan volume selama periode tertentu.
- Open menunjukkan harga pembukaan, High harga tertinggi, Low harga terendah, Close harga penutupan, dan Volume aktivitas transaksi yang tercatat.
- Volume tidak boleh langsung dianggap sebagai tekanan beli atau tekanan jual. Volume menunjukkan aktivitas transaksi, sedangkan arah harga harus dibaca melalui perubahan harga dan konteksnya.
- Timeframe menentukan skala pengamatan. Bar 5 menit, 15 menit, 1 jam, dan 1 hari tidak boleh dicampur sembarangan karena masing-masing memiliki struktur waktu, risiko, likuiditas, dan makna pengukuran yang berbeda. Dalam rancangan SAMSON v1.0, timeframe dasar penelitian intraday adalah 5 menit.
- Data yang tersimpan dalam database tidak otomatis berarti seluruhnya boleh digunakan pada saat keputusan historis. Peneliti harus memperhatikan information availability dan mematuhi prinsip no-look-ahead.
- Terakhir, data pasar tidak selalu sempurna. Bar tidak valid, data hilang, market break, perubahan jadwal perdagangan, corporate action, dan penyesuaian harga dapat memengaruhi hasil penelitian. Karena itu, kualitas data harus diperiksa dan didokumentasikan sebelum kesimpulan dibuat.

---

## Pertanyaan Refleksi

1. Mengapa satu bar bukan berarti satu transaksi?
2. Apa perbedaan antara High dan Close?
3. Mengapa volume besar tidak otomatis berarti tekanan beli?
4. Mengapa volume 5 juta saham tidak selalu memiliki arti yang sama pada setiap saham atau setiap waktu?
5. Mengapa timeframe 5 menit tidak boleh langsung dicampur dengan timeframe harian?
6. Apa perbedaan antara data yang tersimpan sekarang dan informasi yang tersedia pada saat keputusan dibuat?
7. Bagaimana penggunaan Close final sebelum bar ditutup dapat menimbulkan look-ahead bias?
8. Mengapa market break tidak boleh otomatis dianggap sebagai data hilang?
9. Mengapa corporate action dapat memengaruhi pembacaan harga historis?
10. Mengapa pemeriksaan kualitas data merupakan bagian dari penelitian, bukan sekadar pekerjaan teknis?

---

## Kalimat Kunci Bab

> Data OHLCV bukanlah ramalan. Ia adalah bahan mentah yang harus ditempatkan dalam waktu, konteks, dan aturan yang benar sebelum dapat digunakan untuk mencari bukti.

---

<div align="center">

[← Bab Sebelumnya](/posts/bab-04-mengapa-sinyal-menipu/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Bab Selanjutnya →](/posts/bab-06-memahami-samson/)

</div>