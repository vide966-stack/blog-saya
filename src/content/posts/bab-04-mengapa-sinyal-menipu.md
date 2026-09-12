---
title: "BAB 4 — Mengapa Sinyal Trading Bisa Menipu?"
published: 2026-09-12
description: "Hindsight bias, look-ahead bias, survivorship bias, data snooping, dan overfitting — lima penyebab utama mengapa hasil penelitian trading bisa menipu."
tags: ["bab-4", "bias", "metodologi", "overfitting"]
category: "Bab"
draft: false
lang: ""
---

**BAGIAN I — MENGAPA KITA MEMBUTUHKAN BUKTI?**

---

## Tujuan Bab

Sinyal trading sering terlihat meyakinkan setelah kita melihat hasilnya. Sebuah pola tampak berhasil, sebuah indikator seolah-olah selalu memberi peringatan, atau sebuah strategi menghasilkan grafik keuntungan yang indah.

Namun, hasil yang terlihat bagus belum tentu berasal dari informasi yang benar-benar tersedia pada saat keputusan dibuat.

Kesalahan dalam penelitian dapat membuat sinyal tampak lebih akurat, lebih menguntungkan, dan lebih stabil daripada kenyataannya. Karena itu, sebelum membahas cara mencari dan menguji edge, kita perlu memahami terlebih dahulu mengapa hasil penelitian trading bisa menipu.

Prinsip utama bab ini adalah:

> **Hasil yang bagus tidak otomatis berarti penelitian yang benar.**

Penelitian yang benar harus menjawab bukan hanya "berapa besar keuntungan yang terlihat?", tetapi juga:

- Informasi apa yang tersedia saat keputusan dibuat?
- Apakah data masa depan ikut masuk?
- Apakah sampel penelitian mewakili populasi sebenarnya?
- Berapa banyak aturan yang telah dicoba?
- Apakah strategi benar-benar memiliki informasi yang berguna, atau hanya menghafal masa lalu?
- Apakah hasil tetap masuk akal ketika diuji pada data yang belum pernah digunakan?

---

## 4.1. Bias Melihat Hasil Setelah Kejadian

### "Saya Sudah Tahu Saham Itu Naik"

Bayangkan seseorang membuka grafik saham setelah pasar tutup. Ia melihat bahwa harga naik tajam pada hari Rabu.

Kemudian ia berkata:

> "Seharusnya saya membeli pada hari Selasa. Tanda-tandanya sudah jelas."

Pernyataan tersebut terdengar masuk akal karena ia sudah mengetahui apa yang terjadi pada hari Rabu. Namun, ketika hari Selasa berlangsung, informasi tentang kenaikan hari Rabu belum tersedia.

Inilah masalah dasar ketika kita menilai keputusan masa lalu menggunakan pengetahuan masa depan.

Dalam kehidupan sehari-hari, hal ini disebut sebagai **hindsight bias**, atau bias melihat sesuatu seolah-olah sudah jelas setelah hasilnya diketahui.

Dalam penelitian trading, bias ini dapat membuat pola yang sebenarnya tidak mudah dikenali secara real-time terlihat sangat meyakinkan.

### Informasi Saat Itu dan Informasi Sekarang

Ada dua keadaan informasi yang perlu dibedakan:

#### 1. Informasi yang tersedia saat keputusan dibuat

Misalnya pada penutupan hari Senin, peneliti hanya mengetahui:

- Harga dan volume sampai hari Senin.
- Data historis sebelum hari Senin.
- Indikator yang dihitung dari data tersebut.
- Informasi lain yang memang sudah tersedia pada saat itu.

#### 2. Informasi yang diketahui setelah kejadian

Setelah beberapa hari berlalu, peneliti mungkin mengetahui:

- Harga saham naik atau turun.
- Apakah target profit tercapai.
- Apakah stop-loss tersentuh.
- Apakah pola tersebut akhirnya berhasil.
- Apakah saham mengalami kenaikan besar setelah sinyal muncul.

Informasi kedua tidak boleh digunakan untuk membentuk keputusan yang seolah-olah dibuat hanya berdasarkan informasi pertama.

### Contoh Sederhana

Misalkan harga saham sebagai berikut:

| Hari | Harga Penutupan |
|---|---|
| Senin | 100 |
| Selasa | 102 |
| Rabu | 110 |
| Kamis | 108 |

Setelah melihat grafik, seseorang mungkin berkata:

> "Pada Selasa sudah jelas saham akan naik ke 110."

Padahal pada Selasa, terdapat banyak kemungkinan:

- Harga bisa naik.
- Harga bisa turun.
- Harga bisa bergerak mendatar.
- Harga bisa mengalami gap turun.
- Harga bisa naik sebentar lalu berbalik.

Kenaikan pada Rabu membuat pola sebelum kenaikan tampak lebih jelas daripada ketika pola itu benar-benar terjadi.

### Mengapa Bias Ini Berbahaya?

Bias melihat hasil setelah kejadian dapat menyebabkan peneliti:

- Menganggap pola yang sebenarnya samar sebagai pola yang jelas.
- Mengabaikan kejadian ketika pola yang sama gagal.
- Memilih contoh yang berhasil dan melupakan contoh yang buruk.
- Menyusun aturan berdasarkan hasil yang sudah diketahui.
- Mengira keputusan masa lalu lebih mudah daripada kenyataannya.

Masalahnya bukan hanya pada peneliti yang tidak jujur. Bias ini dapat terjadi secara tidak sadar karena otak manusia memang cenderung mencari cerita yang masuk akal setelah mengetahui hasil.

### Prinsip TEKB

Dalam TEKB, setiap keputusan harus dijelaskan berdasarkan informasi yang tersedia pada saat keputusan tersebut dibuat.

Pertanyaan yang harus diajukan adalah:

> "Apakah aturan ini benar-benar dapat dijalankan pada waktu itu, tanpa mengetahui apa yang terjadi sesudahnya?"

Jika jawabannya tidak, maka hasil penelitian tersebut tidak dapat dianggap sebagai simulasi keputusan yang valid.

---

## 4.2. Look-Ahead Bias

### Apa Itu Look-Ahead Bias?

**Look-ahead bias** adalah penggunaan informasi masa depan dalam proses yang seharusnya hanya menggunakan informasi yang tersedia pada saat keputusan dibuat.

Istilah ini dapat diterjemahkan secara sederhana sebagai:

> Melihat ke depan tanpa mengakui bahwa kita sedang melihat masa depan.

Look-ahead bias merupakan salah satu kesalahan paling serius dalam penelitian trading karena dapat membuat strategi yang sebenarnya tidak memiliki keunggulan terlihat sangat menguntungkan.

### Contoh: Menggunakan Harga Besok

Misalkan aturan penelitian ditulis seperti ini:

> "Beli saham hari ini jika harga penutupan besok lebih tinggi daripada harga penutupan hari ini."

Secara matematis, aturan tersebut mungkin menghasilkan keuntungan. Namun, aturan itu tidak dapat digunakan secara nyata karena harga penutupan besok belum diketahui ketika keputusan hari ini dibuat.

Contoh:

> Jika C(t+1) > C(t), maka beli pada hari t.

Masalahnya adalah **C(t+1)** baru diketahui setelah hari berikutnya selesai.

Aturan tersebut bukan sinyal trading yang tersedia secara real-time. Itu adalah aturan yang menggunakan jawaban dari masa depan.

### Contoh Look-Ahead pada Entry

Misalnya peneliti mengatakan:

> "Kita membeli pada harga terendah hari itu karena setelah melihat grafik, titik terendahnya terlihat jelas."

Ini juga bermasalah.

Harga terendah harian hanya diketahui setelah hari tersebut selesai. Pada awal hari, trader tidak mengetahui:

- Apakah harga akan membuat titik terendah baru.
- Apakah harga akan turun lebih dalam.
- Apakah harga terendah sudah terjadi.
- Apakah harga akan naik atau justru jatuh.

Jika penelitian menganggap trader selalu bisa membeli tepat di harga terendah, hasilnya akan terlalu optimistis.

### Look-Ahead pada Exit

Look-ahead bias juga dapat terjadi ketika menentukan waktu keluar.

Contohnya:

> "Posisi ditutup tepat sebelum harga berbalik turun."

Pernyataan ini hanya mudah dilakukan setelah kita mengetahui bahwa pembalikan akan terjadi.

Dalam penelitian yang valid, aturan exit harus ditentukan sebelumnya, misalnya:

- Stop-loss tersentuh.
- Take-profit tersentuh.
- Masa kepemilikan berakhir.
- Sinyal keluar muncul berdasarkan data yang telah tersedia.
- Posisi ditutup pada waktu yang telah ditentukan.

Bukan:

> "Keluar pada titik yang paling menguntungkan jika dilihat dari grafik."

### Look-Ahead pada Indikator

Indikator juga dapat mengandung look-ahead apabila perhitungannya menggunakan data masa depan.

Misalnya, peneliti menghitung rata-rata harga dengan memasukkan beberapa hari setelah tanggal sinyal:

> Rata-rata = harga 5 hari sebelum + harga hari ini + harga 5 hari sesudah

Jika rata-rata tersebut digunakan untuk menentukan keputusan pada hari ini, maka informasi masa depan telah masuk ke dalam sinyal.

Indikator yang terlihat sangat akurat mungkin sebenarnya hanya "mengetahui" apa yang akan terjadi karena rumusnya menggunakan data yang belum tersedia.

### Look-Ahead pada Pemilihan Sampel

Kesalahan juga dapat terjadi ketika memilih event penelitian.

Contohnya:

> "Ambil semua event volume tinggi yang ternyata diikuti kenaikan besar."

Aturan tersebut tidak lagi memilih event hanya berdasarkan kondisi pada saat event terjadi. Peneliti telah menggunakan hasil masa depan untuk menentukan event mana yang masuk sampel.

Definisi event yang benar harus dapat dijalankan tanpa mengetahui return setelah event.

Misalnya:

> RV_t = V_t / V_baseline,t

Dengan syarat:

- V_t adalah volume pada saat event.
- V_baseline,t hanya menggunakan data sebelum event.

Event ditentukan berdasarkan informasi yang tersedia pada waktu t.

Return setelah event hanya digunakan untuk evaluasi, bukan untuk menentukan apakah event masuk sampel.

### Look-Ahead dalam TEKB

Dalam TEKB, waktu harus dipisahkan dengan jelas:

- **Event time** — kapan kondisi terdeteksi.
- **Confirmation time** — kapan syarat konfirmasi terpenuhi.
- **Availability time** — kapan informasi benar-benar tersedia.
- **Evaluation time** — kapan hasil mulai diukur.

Contohnya:

- Candle event selesai pada hari Senin.
- Aturan menyatakan entry pada open hari Selasa.
- Return tiga hari dihitung setelah entry.
- Informasi harga Rabu, Kamis, dan Jumat tidak boleh digunakan untuk mengubah keputusan entry Selasa.

### Mengapa Look-Ahead Membuat Hasil Terlalu Bagus?

Look-ahead bias menghilangkan ketidakpastian yang sebenarnya dihadapi trader.

Dalam dunia nyata, trader harus mengambil keputusan sebelum mengetahui hasil. Dalam backtest yang terkena look-ahead, sistem seolah-olah sudah mengetahui:

- Kapan harga akan naik.
- Kapan harga akan turun.
- Kapan titik terendah terjadi.
- Kapan titik tertinggi terjadi.
- Event mana yang akan berhasil.
- Kapan harus masuk dan keluar.

Akibatnya, hasil dapat menunjukkan:

- Win rate yang terlalu tinggi.
- Profit yang terlalu besar.
- Drawdown yang terlalu rendah.
- Entry dan exit yang tampak sempurna.
- Equity curve yang terlalu mulus.

Namun, keuntungan tersebut mungkin tidak dapat direalisasikan dalam kondisi nyata.

### Pertanyaan Audit

Sebelum menerima hasil penelitian, tanyakan:

> "Untuk setiap keputusan, apakah semua informasi yang digunakan benar-benar sudah tersedia pada saat keputusan itu dibuat?"

Jika tidak, penelitian tersebut harus diperbaiki atau diberi status tidak valid.

---

## 4.3. Survivorship Bias

### Apa Itu Survivorship Bias?

**Survivorship bias** adalah kesalahan penelitian yang hanya memperhatikan objek yang masih bertahan sampai sekarang, sementara objek yang gagal, delisting, bangkrut, merger, atau keluar dari populasi diabaikan.

Dalam konteks saham, peneliti mungkin hanya menggunakan daftar perusahaan yang:

- Masih tercatat di bursa.
- Masih populer.
- Masih memiliki data lengkap.
- Masih memiliki kapitalisasi besar.
- Masih dianggap sebagai saham berkualitas.

Masalahnya, daftar tersebut belum tentu mewakili saham yang benar-benar tersedia pada masa lalu.

### Contoh Sederhana

Bayangkan pada tahun 2015 terdapat 100 saham dalam suatu populasi penelitian.

Sepuluh tahun kemudian:

- 60 saham masih tercatat.
- 15 saham delisting.
- 10 saham merger.
- 5 saham bangkrut.
- 10 saham keluar dari kriteria populasi.

Jika penelitian tahun 2015–2025 hanya menggunakan 60 saham yang masih bertahan, maka penelitian tersebut mengabaikan 40 saham yang tidak bertahan.

Padahal, saham yang gagal mungkin memiliki karakteristik penting:

- Penurunan besar.
- Likuiditas yang menghilang.
- Volatilitas ekstrem.
- Event volume yang menyesatkan.
- Return buruk setelah sinyal tertentu.

Dengan menghilangkan saham-saham tersebut, hasil penelitian dapat terlihat lebih baik daripada kondisi populasi sebenarnya.

### Analogi dalam Kehidupan

Bayangkan seseorang ingin membuktikan bahwa semua pengusaha sukses karena bekerja keras. Ia hanya mewawancarai pengusaha yang berhasil dan tidak pernah mempelajari mereka yang gagal.

Kesimpulannya mungkin:

> "Cara ini pasti berhasil."

Padahal, ia tidak mengetahui berapa banyak orang yang melakukan hal serupa tetapi gagal.

Itulah gambaran sederhana survivorship bias.

### Mengapa Saham yang Hilang Penting?

Saham yang delisting atau bangkrut bukan sekadar data yang merepotkan. Mereka adalah bagian dari sejarah pasar.

Jika penelitian bertujuan mengukur performa strategi pada masa lalu, maka menghilangkan saham yang gagal dapat menyebabkan:

- Risiko penurunan terlihat lebih kecil.
- Frekuensi kegagalan terlihat lebih rendah.
- Distribusi return menjadi terlalu optimistis.
- Strategi terlihat lebih tahan lama.
- Perkiraan peluang kehilangan modal menjadi tidak realistis.

### Populasi Historis Harus Ditentukan dengan Hati-hati

Peneliti harus menjelaskan populasi yang digunakan.

Ada beberapa kemungkinan desain:

#### 1. Universe saat ini

Misalnya hanya menggunakan saham yang saat ini masih tercatat.

Desain ini dapat digunakan untuk tujuan tertentu, tetapi harus dinyatakan secara terbuka. Hasilnya tidak boleh langsung disebut sebagai representasi seluruh saham yang tersedia pada masa lalu.

#### 2. Universe historis point-in-time

Populasi ditentukan berdasarkan saham yang memang termasuk dalam universe pada setiap tanggal penelitian.

Ini lebih sesuai apabila tujuan penelitian adalah mensimulasikan keputusan yang benar-benar dapat dilakukan pada masa lalu.

#### 3. Universe dengan kriteria likuiditas

Misalnya hanya saham dengan nilai transaksi minimum tertentu.

Kriteria tersebut harus dihitung menggunakan informasi yang tersedia pada saat itu, bukan berdasarkan likuiditas saat ini.

Contohnya, jangan memilih saham berdasarkan:

> "Saham yang sekarang rata-rata memiliki nilai transaksi tinggi."

Jika penelitian dimulai sepuluh tahun lalu, gunakan data likuiditas yang tersedia pada waktu tersebut.

### Survivorship Bias dan Data Point-in-Time

Data point-in-time tidak hanya berkaitan dengan harga dan volume. Ia juga berkaitan dengan status populasi.

Peneliti perlu mengetahui:

- Kapan saham masuk ke dalam universe.
- Kapan saham keluar.
- Kapan terjadi delisting.
- Kapan merger atau perubahan kode terjadi.
- Apakah data historis telah disesuaikan dengan benar.
- Apakah daftar saham yang digunakan mencerminkan kondisi pada tanggal penelitian.

Jika informasi tersebut tidak tersedia, hasil penelitian perlu diberi batasan yang jelas.

### Pertanyaan Audit

Tanyakan:

> "Apakah penelitian ini hanya melihat saham yang berhasil bertahan, atau benar-benar merepresentasikan populasi yang tersedia pada saat keputusan dibuat?"

Jika hanya menggunakan saham yang masih bertahan, jangan menyimpulkan bahwa strategi tersebut pasti berlaku untuk seluruh pasar historis.

---

## 4.4. Data Snooping dan Terlalu Banyak Mencoba

### Apa Itu Data Snooping?

**Data snooping** terjadi ketika peneliti mencoba terlalu banyak aturan, indikator, parameter, periode, atau kombinasi sampai menemukan hasil yang terlihat bagus, kemudian memperlakukan hasil tersebut seolah-olah merupakan temuan yang direncanakan sejak awal.

Contohnya, seorang peneliti mencoba:

- 20 indikator.
- 10 threshold volume.
- 8 horizon.
- 12 kombinasi stop-loss dan take-profit.
- 15 periode moving average.
- 30 saham.
- Beberapa periode penelitian.

Jumlah kombinasi dapat menjadi sangat besar.

Dari banyak percobaan tersebut, sangat mungkin ada satu atau beberapa kombinasi yang terlihat menguntungkan hanya karena kebetulan.

### Contoh Sederhana

Misalkan seorang peneliti menguji 100 aturan trading yang sebenarnya tidak memiliki keunggulan.

Jika setiap aturan memiliki peluang tertentu untuk menghasilkan hasil yang tampak bagus secara kebetulan, maka semakin banyak aturan yang dicoba, semakin besar peluang ditemukan setidaknya satu hasil yang terlihat luar biasa.

Misalnya:

- Aturan 1 gagal.
- Aturan 2 gagal.
- Aturan 3 hampir impas.
- Aturan 4 gagal.
- ...
- Aturan 87 menghasilkan profit besar.

Peneliti kemudian hanya mempublikasikan aturan 87 dan berkata:

> "Saya menemukan strategi yang menghasilkan profit besar."

Masalahnya, pembaca tidak diberi tahu bahwa ada 86 percobaan lain yang gagal.

### Data Snooping Tidak Selalu Berarti Kecurangan

Data snooping dapat terjadi secara tidak sengaja.

Peneliti mungkin berpikir:

> "Saya hanya ingin mencari konfigurasi terbaik."

Namun, ketika konfigurasi terbaik dipilih berdasarkan hasil pada data yang sama, data tersebut telah digunakan dua kali:

1. Untuk menemukan aturan.
2. Untuk menilai keberhasilan aturan.

Akibatnya, hasil evaluasi menjadi terlalu optimistis.

### Bentuk Data Snooping yang Umum

Data snooping dapat muncul dalam berbagai bentuk.

#### 1. Mencoba banyak indikator

Misalnya peneliti menguji:

- RSI.
- MACD.
- Stochastic.
- Bollinger Bands.
- Moving average.
- ATR.
- Volume.
- Berbagai kombinasi indikator.

Kemudian hanya kombinasi yang menghasilkan performa terbaik yang dipertahankan.

#### 2. Mencoba banyak threshold

Contohnya:

- RV > 1,5.
- RV > 2.
- RV > 2,5.
- RV > 3.
- RV > 4.
- RV > 5.

Jika threshold dipilih setelah melihat hasil, maka pemilihan tersebut harus dianggap sebagai bagian dari proses pencarian, bukan sebagai pengujian tunggal yang bebas dari bias.

#### 3. Memilih periode yang paling bagus

Misalnya strategi diuji pada:

- 2016–2018.
- 2017–2019.
- 2018–2020.
- 2019–2021.
- 2020–2022.
- 2021–2023.

Kemudian peneliti hanya memilih periode yang memberikan hasil terbaik.

#### 4. Memilih saham yang paling cocok

Peneliti mungkin menguji banyak saham lalu hanya menampilkan saham yang berhasil.

Jika tujuan awalnya adalah menguji strategi pada populasi tertentu, pemilihan saham berdasarkan hasil dapat merusak validitas penelitian.

#### 5. Mengubah aturan setelah melihat hasil

Contohnya:

- Entry awalnya pada open berikutnya, lalu diubah menjadi close event karena hasilnya lebih baik.
- Horizon awalnya tiga hari, lalu diubah menjadi lima hari.
- Threshold awalnya RV≥3, lalu diubah menjadi RV≥2,7.
- Kandidat yang gagal dikeluarkan dari laporan.

Perubahan seperti ini tidak selalu dilarang, tetapi harus diperlakukan sebagai penelitian baru atau tahap eksplorasi baru. Hasilnya tidak boleh dilaporkan seolah-olah aturan tersebut telah ditetapkan sejak awal.

### Mengapa Hasil Terbaik Belum Tentu Edge?

Hasil terbaik dari banyak percobaan belum tentu menunjukkan informasi yang benar-benar berguna.

Ada perbedaan antara:

> "Aturan ini terlihat bagus setelah banyak aturan dicoba."

dan:

> "Aturan ini telah diuji secara terencana, dibandingkan dengan B0, dikoreksi terhadap multiple testing, dan tetap menunjukkan hasil pada OOS."

Kalimat pertama adalah temuan eksploratif. Kalimat kedua memiliki dasar metodologis yang lebih kuat.

### Cara TEKB Menangani Data Snooping

TEKB menerapkan beberapa disiplin:

- Menentukan pertanyaan penelitian sebelum pengujian.
- Menentukan candidate grid sebelum melihat hasil.
- Mencatat seluruh kandidat yang diuji.
- Mencatat multiple-testing family.
- Tidak hanya menampilkan kandidat yang berhasil.
- Menggunakan B0 sebagai pembanding.
- Mempertimbangkan ketidakpastian.
- Menggunakan koreksi multiple testing jika sesuai.
- Melakukan freeze sebelum OOS.
- Tidak menggunakan OOS untuk tuning.

### Prinsip Penting

> Semakin banyak kesempatan untuk mencoba, semakin besar kebutuhan untuk mengoreksi optimisme hasil.

Dalam TEKB, proses pencarian harus dapat ditelusuri. Bukan hanya pemenangnya yang dicatat, tetapi juga jumlah percobaan, aturan yang gagal, dan alasan kandidat tertentu dipilih.

---

## 4.5. Overfitting: Strategi yang Hafal Masa Lalu

### Apa Itu Overfitting?

**Overfitting** terjadi ketika aturan atau model terlalu menyesuaikan diri dengan data historis sehingga tampak sangat baik pada masa lalu, tetapi gagal ketika diterapkan pada data baru.

Strategi tersebut bukan benar-benar memahami pola yang cukup umum. Ia justru terlalu banyak "menghafal" karakteristik khusus dari data yang pernah dilihat.

### Analogi Siswa yang Menghafal Soal Ujian

Bayangkan seorang siswa akan mengikuti ujian.

Siswa pertama menghafal jawaban dari 100 soal latihan. Ketika ujian berisi soal yang sama, ia mendapat nilai sempurna.

Namun, ketika guru mengubah angka, susunan kalimat, atau bentuk pertanyaan, siswa tersebut kebingungan.

Siswa kedua memahami konsep. Ia mungkin tidak menjawab semua soal latihan dengan sempurna, tetapi dapat menyelesaikan soal baru karena memahami prinsipnya.

Dalam analogi ini:

- Siswa pertama mirip strategi yang **overfit**.
- Siswa kedua mirip aturan yang memiliki **kemampuan generalisasi**.

Strategi overfit sangat pandai menjelaskan masa lalu, tetapi tidak cukup baik menghadapi kondisi baru.

### Contoh Overfitting dalam Trading

Misalnya peneliti menemukan aturan berikut:

> "Beli hanya jika RV berada di antara 3,17 dan 3,46, harga naik tepat 1,2% dalam dua hari sebelumnya, hari event terjadi pada Selasa atau Kamis, saham bukan sektor tertentu, dan entry dilakukan pada kondisi khusus tertentu."

Aturan tersebut mungkin menghasilkan performa sangat bagus pada data historis.

Namun, semakin banyak syarat yang ditambahkan, semakin besar kemungkinan aturan tersebut hanya cocok dengan kebetulan dalam sampel.

Aturan itu mungkin secara tidak sadar sedang menghafal:

- Beberapa tanggal tertentu.
- Beberapa saham tertentu.
- Kondisi pasar tertentu.
- Struktur volatilitas tertentu.
- Kejadian khusus yang tidak berulang.

### Mengapa Data Historis Bisa Dihafal?

Data pasar mengandung banyak variasi:

- Tren naik dan turun.
- Krisis.
- Periode suku bunga berbeda.
- Perubahan likuiditas.
- Perubahan perilaku pelaku pasar.
- Perubahan regulasi.
- Perubahan komposisi sektor.
- Perubahan biaya transaksi.

Aturan yang terlalu rumit dapat menyesuaikan diri dengan variasi historis tersebut tanpa memiliki dasar yang cukup kuat untuk berlaku pada masa depan.

### Gejala Overfitting

Beberapa tanda yang perlu dicurigai:

- Profit IS sangat tinggi, tetapi OOS langsung melemah.
- Strategi membutuhkan banyak parameter khusus.
- Sedikit perubahan parameter membuat hasil berubah drastis.
- Strategi hanya berhasil pada satu saham atau satu periode.
- Banyak aturan pengecualian ditambahkan.
- Hasil sangat bagus sebelum biaya, tetapi buruk setelah biaya.
- Equity curve tampak terlalu sempurna.
- Tidak ada penjelasan mengapa parameter tersebut masuk akal.
- Strategi dipilih dari banyak kandidat tanpa koreksi multiple testing.
- Peneliti tidak dapat menjelaskan hasil selain dengan berkata, "Karena backtest-nya bagus."

### Overfitting dan Kompleksitas

Semakin kompleks sebuah strategi, semakin banyak cara strategi tersebut dapat menyesuaikan diri dengan kebetulan.

Bandingkan dua aturan:

#### Aturan sederhana

> "Jika RV≥3, ukur return tiga hari berikutnya dan bandingkan dengan B0."

#### Aturan kompleks

> "Jika RV≥3, tetapi hanya pada hari tertentu, setelah pola tertentu, dengan threshold yang sangat spesifik, kecuali jika volatilitas berada dalam rentang tertentu, lalu gunakan SL dan TP khusus berdasarkan kondisi tertentu."

Aturan kompleks belum tentu salah. Namun, kompleksitas menambah risiko bahwa hasil yang terlihat bagus berasal dari penyesuaian terhadap data historis, bukan informasi yang dapat digeneralisasikan.

### Cara Mengurangi Risiko Overfitting

TEKB mengurangi risiko overfitting melalui beberapa langkah:

#### 1. Memulai dari hipotesis yang jelas

Jangan memulai dari:

> "Cari aturan apa pun yang menghasilkan profit."

Mulailah dari pertanyaan yang dapat dijelaskan:

> "Apakah event volume tinggi memiliki distribusi return berikutnya yang berbeda dari B0?"

#### 2. Menggunakan baseline yang adil

B1 harus dibandingkan dengan B0 yang sesuai. Hasil positif yang tidak dibandingkan dengan kondisi dasar dapat menyesatkan.

#### 3. Menguji distribusi, bukan hanya satu angka

Periksa:

- Mean.
- Median.
- Persentase return positif.
- Kuantil.
- Tail loss.
- MAE.
- MFE.
- Expectancy.
- Hasil setelah biaya.

#### 4. Menggunakan bootstrap dan pemeriksaan robustness

Hasil tidak cukup hanya terlihat positif. Peneliti juga perlu melihat seberapa sensitif hasil terhadap pengambilan ulang sampel atau struktur dependensi data.

#### 5. Melakukan freeze

Setelah kandidat dipilih menggunakan data IS, aturan harus dibekukan sebelum OOS.

#### 6. Menguji OOS

OOS digunakan untuk melihat apakah hasil masih bertahan pada data yang tidak digunakan untuk memilih atau menyetel kandidat.

### IS yang Bagus Tidak Sama dengan OOS yang Bagus

Performa IS menjawab:

> "Seberapa baik aturan ini bekerja pada data yang digunakan untuk penelitian dan seleksi?"

Performa OOS menjawab:

> "Apakah aturan yang telah dibekukan masih menunjukkan bukti ketika diterapkan pada data yang belum digunakan untuk memilihnya?"

Jika strategi sangat bagus di IS tetapi gagal di OOS, beberapa kemungkinan perlu dipertimbangkan:

- Edge awal memang lemah.
- Strategi overfit.
- Kondisi pasar berubah.
- Biaya terlalu besar.
- Data atau implementasi bermasalah.
- Sampel IS terlalu kecil.
- Hasil IS merupakan kebetulan.

Karena itu, hasil OOS tidak boleh dianggap sebagai formalitas. OOS adalah salah satu pemeriksaan penting terhadap kemampuan generalisasi.

---

## 4.6. Mengapa Backtest yang Terlihat Profesional Tetap Bisa Salah?

### Tampilan yang Meyakinkan Tidak Sama dengan Bukti yang Kuat

Sebuah backtest dapat terlihat sangat profesional:

- Grafik equity curve naik terus.
- Win rate mencapai 80%.
- Profit bersih terlihat besar.
- Drawdown terlihat rendah.
- Dashboard memiliki banyak indikator.
- Ada tabel statistik lengkap.
- Warna hijau mendominasi laporan.

Namun, semua itu belum menjawab pertanyaan paling mendasar:

> "Apakah hasil tersebut diperoleh melalui proses penelitian yang benar?"

Tampilan yang bagus dapat menyembunyikan kesalahan metodologis.

### 1. Equity Curve yang Indah

**Equity curve** adalah grafik perkembangan nilai modal atau keuntungan dari waktu ke waktu.

Grafik yang terus naik tentu menarik. Namun, grafik tersebut dapat menipu jika:

- Menggunakan informasi masa depan.
- Hanya memilih transaksi yang berhasil.
- Mengabaikan biaya.
- Menggunakan saham yang masih bertahan saja.
- Memilih parameter setelah melihat hasil.
- Menghilangkan transaksi yang gagal.
- Menggunakan entry dan exit yang tidak realistis.

Equity curve yang indah hanya menunjukkan hasil dari aturan yang dijalankan dalam simulasi. Ia tidak membuktikan bahwa simulasi tersebut benar.

### 2. Win Rate Tinggi

**Win rate** adalah persentase transaksi yang menghasilkan keuntungan.

Misalnya:

- 90 transaksi menang.
- 10 transaksi kalah.
- Win rate = 90%.

Angka ini terlihat sangat bagus. Namun, win rate tidak memberi tahu besar kecilnya keuntungan dan kerugian.

Contoh:

- 9 transaksi menang masing-masing +1%.
- 1 transaksi kalah -15%.

Totalnya:

> 9 × 1% − 15% = −6%

Walaupun win rate mencapai 90%, strategi tersebut tetap merugi.

Sebaliknya, strategi dengan win rate 40% dapat menguntungkan jika transaksi yang menang jauh lebih besar daripada transaksi yang kalah.

Karena itu, TEKB tidak menilai strategi hanya dari win rate. Penilaian perlu mencakup distribusi return, tail loss, MAE, MFE, expectancy, dan biaya.

### 3. Profit Besar

Profit besar dapat muncul karena:

- Periode pasar yang sangat cocok.
- Leverage tinggi.
- Risiko besar yang tidak terlihat.
- Satu atau beberapa transaksi ekstrem.
- Penggunaan data masa depan.
- Pemilihan saham atau periode yang menguntungkan.
- Tidak memperhitungkan slippage dan biaya.

Profit besar bukan bukti otomatis bahwa strategi memiliki edge yang stabil.

Pertanyaan yang lebih penting adalah:

- Berapa banyak event yang mendasari profit tersebut?
- Apakah hasil dibandingkan dengan B0?
- Apakah profit tetap ada setelah biaya?
- Apakah hasil bergantung pada beberapa transaksi ekstrem?
- Apakah distribusinya stabil?
- Apakah hasil bertahan pada OOS?

### 4. Drawdown Rendah

**Drawdown** adalah penurunan dari puncak nilai modal menuju titik terendah berikutnya.

Drawdown rendah biasanya dianggap baik. Namun, angka tersebut dapat terlihat rendah karena:

- Periode pengujian terlalu singkat.
- Sampel hanya mencakup kondisi pasar yang tenang.
- Transaksi gagal tidak dimasukkan.
- Strategi tidak diuji pada krisis.
- Risiko tersembunyi belum muncul.
- Posisi atau leverage tidak dihitung secara benar.

Drawdown historis bukan batas maksimum kerugian yang mungkin terjadi di masa depan.

### 5. Dashboard yang Meyakinkan

Dashboard dapat menampilkan:

- Win rate.
- Profit factor.
- Sharpe ratio.
- CAGR.
- Maximum drawdown.
- Jumlah transaksi.
- Grafik modal.
- Distribusi return.
- Sinyal beli dan jual.

Semua metrik tersebut dapat berguna. Namun, dashboard hanya sebaik data dan metode yang mendasarinya.

Dashboard tidak dapat memperbaiki:

- Data yang salah.
- Look-ahead bias.
- Survivorship bias.
- B0 yang tidak adil.
- Candidate selection yang berlebihan.
- Biaya yang diabaikan.
- OOS yang telah digunakan untuk tuning.

Dengan kata lain:

> Dashboard adalah alat untuk menampilkan hasil, bukan alat untuk menjamin kebenaran hasil.

### Enam Pertanyaan untuk Membongkar Backtest yang Terlihat Bagus

Ketika melihat backtest yang meyakinkan, ajukan pertanyaan berikut:

#### Pertanyaan 1

Apakah data masa depan masuk ke dalam sinyal, entry, exit, atau pemilihan sampel?

Jika ya, hasil dapat mengalami look-ahead bias.

#### Pertanyaan 2

Apakah universe historis mencakup saham yang gagal atau hanya saham yang masih bertahan?

Jika hanya saham yang bertahan, hasil dapat mengalami survivorship bias.

#### Pertanyaan 3

Berapa banyak aturan dan parameter yang telah dicoba sebelum hasil ini dipilih?

Jika jumlah percobaan tidak jelas, hasil terbaik dapat merupakan akibat data snooping.

#### Pertanyaan 4

Apakah kandidat dipilih dan diuji pada data yang sama?

Jika ya, risiko overfitting meningkat.

#### Pertanyaan 5

Apakah hasil dibandingkan dengan B0 yang adil?

Profit positif tanpa pembanding belum menunjukkan keunggulan.

#### Pertanyaan 6

Apakah aturan telah dibekukan sebelum OOS dan diuji tanpa tuning?

Jika tidak, hasil OOS mungkin tidak lagi merupakan validasi yang bersih.

---

## Ringkasan Bab 4

Sinyal trading dapat menipu bukan hanya karena pasar sulit diprediksi, tetapi juga karena penelitian dapat dirancang atau dijalankan dengan cara yang menghasilkan optimisme palsu.

Lima sumber masalah utama yang dibahas dalam bab ini adalah:

| Masalah | Inti Kesalahan |
|---|---|
| Hindsight bias | Menilai masa lalu menggunakan pengetahuan yang baru diketahui sekarang |
| Look-ahead bias | Menggunakan informasi yang belum tersedia saat keputusan dibuat |
| Survivorship bias | Mengabaikan saham atau objek yang gagal dan tidak lagi bertahan |
| Data snooping | Mencoba terlalu banyak aturan sampai menemukan hasil yang terlihat bagus |
| Overfitting | Membuat aturan terlalu cocok dengan masa lalu sehingga gagal pada data baru |

Selain itu, backtest yang memiliki grafik indah, win rate tinggi, profit besar, drawdown rendah, atau dashboard profesional tetap belum tentu valid.

### Pelajaran Utama

- Informasi masa depan tidak boleh digunakan untuk membuat keputusan masa lalu.
- Data historis harus mewakili populasi yang benar, bukan hanya objek yang bertahan.
- Jumlah percobaan harus diperhitungkan ketika menilai hasil.
- Strategi yang sangat cocok dengan masa lalu belum tentu mampu bekerja pada data baru.
- Tampilan backtest tidak menggantikan desain penelitian yang benar.
- B0, bootstrap, multiple testing, freeze, dan OOS diperlukan untuk mengurangi klaim yang terlalu optimistis.

Kalimat penutup bab ini:

> Sinyal yang terlihat bagus belum tentu memiliki informasi yang berguna. Bisa jadi, kita hanya melihat masa lalu dengan cara yang membuatnya tampak lebih mudah daripada kenyataannya.

---

## Pertanyaan Refleksi

1. Apa perbedaan antara informasi yang tersedia saat keputusan dibuat dan informasi yang diketahui setelah kejadian?
2. Mengapa menggunakan harga besok untuk menentukan sinyal hari ini disebut look-ahead bias?
3. Apa itu survivorship bias, dan mengapa saham yang delisting penting untuk dimasukkan?
4. Apa yang dimaksud dengan data snooping?
5. Mengapa win rate tinggi belum tentu berarti strategi menguntungkan?
6. Apa gejala overfitting yang perlu dicurigai?
7. Mengapa hasil OOS lebih penting daripada hasil IS?

---

<div align="center">

[← Bab Sebelumnya](/posts/bab-03-cara-berpikir-ilmiah/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Bab Selanjutnya →](/posts/bab-05-mengenal-data-ohlcv/)

</div>