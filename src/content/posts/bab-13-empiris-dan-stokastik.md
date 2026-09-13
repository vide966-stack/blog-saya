---
title: "BAB 13 — Dari Apa yang Terjadi Menuju Apa yang Mungkin Terjadi: Empiris dan Stokastik"
published: 2026-09-12
description: "Pendekatan empiris mencatat apa yang terjadi, pendekatan stokastik menggambarkan apa yang mungkin terjadi. Bab ini menjelaskan distribusi return, B1 vs B0, dan bootstrap."
tags: ["bab-13", "empiris", "stokastik", "distribusi"]
category: "Bab"
draft: false
lang: ""
---

**BAGIAN IV — DARI DATA HISTORIS MENUJU DISTRIBUSI KEMUNGKINAN**

---

Bayangkan seseorang berkata, "Setiap kali kondisi ini muncul, harga naik." Pernyataan seperti itu terdengar sederhana dan meyakinkan. Namun, seorang peneliti tidak akan langsung menerimanya sebagai kebenaran. Ia akan bertanya: Berapa kali kondisi itu muncul? Berapa kali harga benar-benar naik? Seberapa besar kenaikannya? Berapa kali harga justru turun? Bagaimana hasilnya dibandingkan dengan kondisi lain yang serupa tetapi tidak memiliki sinyal tersebut?

Pertanyaan-pertanyaan ini membawa kita pada dua cara penting dalam memahami data: **pendekatan empiris** dan **pendekatan stokastik**.

- **Pendekatan empiris** membantu kita melihat apa yang benar-benar terjadi dalam data historis.
- **Pendekatan stokastik** membantu kita memahami bahwa hasil berikutnya tidak selalu tunggal dan pasti, melainkan memiliki berbagai kemungkinan dengan tingkat ketidakpastian tertentu.

TEKB membutuhkan keduanya. Tanpa pendekatan empiris, penelitian akan terlepas dari kenyataan data. Tanpa pendekatan stokastik, hasil penelitian mudah disalahartikan sebagai kepastian atau ramalan.

---

## 13.1. Pendekatan Empiris: Apa yang Benar-Benar Terjadi?

Kata **empiris** berkaitan dengan sesuatu yang diperoleh melalui pengamatan atau pengalaman nyata. Dalam penelitian trading, pendekatan empiris berarti kita memulai dari kejadian yang benar-benar tercatat dalam data historis.

Misalnya, kita ingin meneliti kondisi ketika terjadi anomali volume melalui SAMSON. Kita tidak langsung mengatakan bahwa anomali volume tersebut menguntungkan. Kita terlebih dahulu mengumpulkan semua event yang memenuhi definisi SAMSON.

Setiap event kemudian dicatat, misalnya dengan informasi:

- Instrumen yang mengalami event.
- Tanggal dan waktu event.
- Harga saat sinyal terbentuk.
- Harga entry yang digunakan.
- Kondisi pasar saat event terjadi.
- Return setelah beberapa horizon.
- Nilai MAE dan MFE.
- Status outcome jika event diuji dengan aturan SL/TP tertentu.

Dari sana, kita dapat membuat pertanyaan empiris:

- Berapa jumlah event yang ditemukan?
- Berapa event yang memiliki return positif?
- Berapa event yang memiliki return negatif?
- Berapa median return?
- Berapa return terbesar dan terkecil?
- Berapa banyak event yang mencapai target?
- Berapa banyak event yang menyentuh stop loss?

Pertanyaan tersebut tidak membutuhkan ramalan. Jawabannya berasal dari data yang sudah diamati.

Contoh sederhana:

| Event | Return setelah 3 bar |
|---|---|
| 1 | +1,2% |
| 2 | -0,8% |
| 3 | +0,5% |
| 4 | +2,0% |
| 5 | -1,1% |

Dari lima event tersebut, kita dapat mengatakan bahwa tiga event menghasilkan return positif dan dua event menghasilkan return negatif. Kita juga dapat menghitung rata-rata, median, nilai minimum, dan nilai maksimum.

Inilah pendekatan empiris: mencatat dan mengukur apa yang benar-benar terjadi, bukan apa yang kita harapkan terjadi.

Namun, pendekatan empiris pada tahap awal belum menjawab seluruh pertanyaan penelitian. Ia baru memberi gambaran tentang sampel yang diamati.

---

## 13.2. Mengapa Data Historis Tidak Otomatis Menjadi Kepastian?

Data historis sangat penting, tetapi data historis bukanlah masa depan itu sendiri. Data historis adalah catatan dari sebagian kejadian yang pernah berlangsung.

Misalnya, kita menemukan 20 event dan seluruhnya menghasilkan return positif. Secara empiris, kita boleh mengatakan:

> "Dalam sampel 20 event yang diamati, seluruh event menghasilkan return positif."

Namun, kita tidak boleh langsung mengubahnya menjadi:

> "Event ini pasti menghasilkan return positif pada kesempatan berikutnya."

Mengapa?

Karena sampel yang kita lihat hanya merupakan sebagian kecil dari seluruh kemungkinan kondisi pasar. Pasar dapat berubah karena:

- Perubahan likuiditas.
- Perubahan perilaku pelaku pasar.
- Perubahan kondisi makroekonomi.
- Perubahan karakteristik instrumen.
- Perubahan regulasi.
- Perubahan volatilitas.
- Perubahan struktur pasar.
- Kejadian luar biasa yang belum muncul dalam sampel.

Hasil historis juga dapat dipengaruhi oleh ukuran sampel. Dua puluh event yang semuanya positif belum tentu memberikan bukti yang sama kuat dengan 2.000 event yang menunjukkan pola serupa. Hasil juga dapat berubah jika periode penelitian diperluas atau komposisi instrumen diganti.

Contohnya, sebuah kondisi mungkin terlihat sangat baik ketika diuji pada saham-saham berlikuiditas tinggi, tetapi hasilnya berbeda ketika diterapkan pada saham dengan likuiditas rendah. Sebuah pola mungkin terlihat menguntungkan pada periode pasar bullish, tetapi tidak pada periode sideways atau bearish.

Karena itu, hasil empiris harus selalu dibaca bersama konteksnya:

- Sampelnya berapa besar?
- Periode pengamatannya kapan?
- Instrumen apa saja yang digunakan?
- Bagaimana event didefinisikan?
- Apakah semua event yang memenuhi aturan dimasukkan?
- Apakah ada event yang dikeluarkan?
- Apakah hasil tersebut dibandingkan dengan pembanding yang adil?

Data historis memberikan bukti tentang apa yang terjadi dalam sampel. Data historis tidak otomatis memberikan kepastian tentang setiap kejadian berikutnya.

---

## 13.3. Frekuensi Historis versus Probabilitas

Salah satu hasil paling mudah dipahami dari penelitian adalah **frekuensi**.

Frekuensi menunjukkan seberapa sering suatu kejadian muncul dalam sampel.

Misalnya, dari 100 event:

- 60 event menghasilkan return positif.
- 40 event menghasilkan return nol atau negatif.

Maka proporsi return positif dalam sampel adalah:

> Frekuensi return positif = 60 / 100 = 60%

Angka 60% tersebut adalah fakta tentang sampel yang diamati. Kita dapat menyebutnya sebagai **frekuensi historis**.

Dalam kondisi tertentu, frekuensi historis dapat digunakan sebagai estimasi awal terhadap probabilitas. Jika definisi event tetap, data cukup relevan, dan asumsi penelitian masuk akal, maka frekuensi 60% dapat menjadi perkiraan bahwa kondisi serupa mungkin diikuti return positif sekitar 60% dalam jangka panjang.

Namun, frekuensi historis bukan jaminan. Ada perbedaan penting antara:

1. "Dalam sampel, 60% event positif."
2. "Probabilitas event berikutnya positif adalah tepat 60%."

Pernyataan pertama langsung didukung oleh data sampel. Pernyataan kedua adalah kesimpulan tentang proses yang lebih luas, sehingga mengandung ketidakpastian.

Bayangkan kita mengambil lima kali lemparan koin dan mendapatkan empat kali gambar. Frekuensi gambar adalah 80%. Tetapi kita tidak akan menyimpulkan bahwa peluang gambar pada lemparan berikutnya pasti 80%. Sampelnya terlalu kecil untuk memberikan keyakinan yang kuat.

Hal yang sama berlaku dalam trading. Frekuensi 80% dari 10 event berbeda tingkat kepercayaannya dengan frekuensi 80% dari 10.000 event. Bahkan pada jumlah event yang besar, kita tetap perlu memperhatikan apakah event-event tersebut benar-benar cukup beragam atau terlalu berkumpul pada kondisi pasar tertentu.

Dengan demikian, frekuensi historis sebaiknya dipahami sebagai:

- Ringkasan dari sampel yang diamati.
- Titik awal untuk memperkirakan kemungkinan.
- Angka yang masih memiliki ketidakpastian.
- Bukan janji mengenai hasil event berikutnya.

Semakin sedikit data, biasanya semakin besar ketidakpastian estimasi. Semakin banyak data yang relevan dan berkualitas, ketidakpastian dapat berkurang, meskipun tidak pernah otomatis menjadi nol.

---

## 13.4. Pendekatan Stokastik: Mengapa Hasil Harus Dipahami sebagai Distribusi?

Pendekatan empiris mencatat kejadian yang sudah terjadi. Pendekatan stokastik membantu kita memahami variasi hasil yang mungkin muncul.

Dalam trading, hasil dari suatu kondisi hampir tidak pernah berupa satu angka yang selalu sama. Kondisi yang sama dapat diikuti oleh:

- Return positif kecil.
- Return positif besar.
- Return mendatar.
- Return negatif kecil.
- Return negatif besar.

Sebagai contoh, suatu kondisi mungkin menghasilkan return tiga bar berikut:

- +0,2%
- +1,5%
- -0,7%
- +3,1%
- -2,0%
- 0,0%
- +0,8%

Jika kita hanya bertanya, "Apakah harga naik atau turun?", sebagian informasi akan hilang. Kita tidak dapat membedakan kenaikan kecil dari kenaikan besar, atau kerugian kecil dari kerugian ekstrem.

Pendekatan stokastik memandang return sebagai hasil yang dapat memiliki banyak kemungkinan. Fokusnya bukan hanya pada satu hasil, tetapi pada pola keseluruhan hasil.

Pertanyaan stokastik antara lain:

- Di mana pusat hasil biasanya berada?
- Seberapa lebar penyebaran hasil?
- Seberapa sering hasil positif muncul?
- Seberapa sering hasil negatif besar muncul?
- Apakah ada ekor kerugian yang panjang?
- Apakah sebagian kecil event menghasilkan keuntungan yang sangat besar?
- Apakah hasil cenderung seimbang atau berat ke satu sisi?

Dengan cara ini, penelitian tidak berhenti pada kalimat "sinyal ini pernah berhasil". Penelitian bergerak menuju pemahaman yang lebih lengkap:

> "Jika kondisi ini muncul, hasil yang diamati memiliki rentang dan pola kemungkinan tertentu."

Inilah alasan TEKB tidak cukup hanya menghitung jumlah kemenangan. TEKB perlu memahami distribusi hasil.

---

## 13.5. Distribusi Return

### Apa Itu Distribusi?

**Distribusi** adalah cara menggambarkan bagaimana sekumpulan hasil tersebar.

Bayangkan kita mengumpulkan seluruh return dari 1.000 event. Return tersebut tidak akan semuanya sama. Ada yang positif, negatif, kecil, besar, dekat dengan nol, atau berada di bagian ekstrem.

Distribusi membantu kita melihat bagaimana hasil-hasil tersebut tersusun.

Misalnya, dua kelompok memiliki data berikut:

**Kelompok A:**
- +1%
- +1%
- +1%
- -1%
- -1%

**Kelompok B:**
- +5%
- +2%
- 0%
- -2%
- -5%

Kedua kelompok memiliki tiga hasil yang tidak negatif jika angka nol dihitung sebagai tidak negatif, tetapi karakter distribusinya berbeda. Kelompok B memiliki penyebaran yang jauh lebih besar dan ekor yang lebih ekstrem.

Untuk memahami distribusi, kita dapat melihat beberapa unsur penting.

### 1. Pusat Distribusi

Pusat distribusi memberikan gambaran tentang lokasi umum hasil.

Dua ukuran pusat yang sering digunakan adalah **median** dan **mean**.

### 2. Median

**Median** adalah nilai tengah setelah semua hasil diurutkan.

Misalnya, return berikut:

- -2%
- -1%
- +0,5%
- +1%
- +3%

Median-nya adalah +0,5%, karena angka tersebut berada di tengah.

Median berguna karena tidak terlalu mudah ditarik oleh satu hasil ekstrem. Jika sebagian besar event menghasilkan return kecil, tetapi satu event menghasilkan keuntungan sangat besar, median tetap menggambarkan hasil tengah dengan lebih stabil.

### 3. Mean atau Rata-Rata

**Mean** dihitung dengan menjumlahkan seluruh hasil lalu membaginya dengan jumlah event.

> Mean = Jumlah seluruh return / Jumlah event

Mean berguna untuk melihat hasil rata-rata, tetapi dapat dipengaruhi oleh nilai ekstrem. Satu atau beberapa keuntungan yang sangat besar dapat menaikkan mean, walaupun sebagian besar event menghasilkan return kecil atau negatif.

Karena itu, TEKB sebaiknya tidak hanya melihat mean. Median dan ukuran distribusi lainnya juga perlu diperiksa.

### 4. Penyebaran

**Penyebaran** menunjukkan seberapa jauh hasil-hasil tersebar dari pusatnya.

Jika sebagian besar return berada di antara -0,5% dan +0,5%, distribusinya relatif sempit. Jika return tersebar dari -10% hingga +15%, distribusinya lebih lebar.

Penyebaran penting karena dua strategi dapat memiliki mean yang sama, tetapi tingkat ketidakpastian dan risikonya sangat berbeda.

### 5. Varians dan Deviasi Standar

**Varians** dan **deviasi standar** merupakan ukuran matematis untuk menggambarkan penyebaran data.

Untuk pembaca awam, gagasan dasarnya cukup dipahami sebagai berikut:

- Deviasi standar kecil: hasil cenderung berkumpul dekat rata-rata.
- Deviasi standar besar: hasil lebih menyebar dan lebih bervariasi.

Deviasi standar bukan ukuran kerugian secara langsung. Ia mengukur variasi, baik ke arah positif maupun negatif. Karena itu, deviasi standar harus dibaca bersama median, mean, percentile, dan ekor distribusi.

### 6. Percentile

**Percentile** membantu kita memahami posisi suatu hasil dibandingkan hasil lainnya.

Contoh:

- P10 adalah nilai yang menjadi batas bawah bagi sebagian besar data; sekitar 10% hasil berada di bawahnya.
- P50 sama dengan median.
- P90 adalah nilai yang hanya dilampaui oleh sebagian kecil hasil.

Misalnya, P10 return adalah -3%. Ini memberi gambaran bahwa bagian bawah distribusi memiliki hasil yang cukup buruk. P90 sebesar +4% menunjukkan bahwa bagian atas distribusi mencapai hasil yang relatif tinggi.

Percentile berguna karena tidak hanya menunjukkan satu rata-rata, tetapi juga bagian bawah, tengah, dan atas distribusi.

### 7. Ekor Distribusi

**Ekor distribusi** adalah bagian ekstrem dari hasil, baik kerugian maupun keuntungan.

Dalam trading, ekor sangat penting karena sebagian kecil kejadian dapat memberikan dampak besar terhadap hasil keseluruhan.

Contoh:

- Sebagian besar event menghasilkan return antara -1% dan +1%.
- Namun, beberapa event menghasilkan -8%.
- Atau beberapa event menghasilkan +10%.

Jika kita hanya melihat mean, median, atau win rate, kejadian ekstrem tersebut dapat terlewatkan.

Ekor kerugian perlu diperhatikan karena risiko tidak selalu berasal dari hasil rata-rata, melainkan dapat berasal dari kejadian yang jarang tetapi sangat buruk.

### 8. Skewness secara Sederhana

**Skewness** menggambarkan ketidakseimbangan bentuk distribusi.

Secara sederhana:

- Distribusi dapat memiliki ekor lebih panjang ke sisi positif.
- Distribusi dapat memiliki ekor lebih panjang ke sisi negatif.
- Distribusi dapat relatif seimbang.

Jika distribusi memiliki beberapa keuntungan sangat besar tetapi banyak hasil kecil atau negatif, distribusinya mungkin memiliki kemencengan ke arah positif. Sebaliknya, jika terdapat beberapa kerugian ekstrem, ekornya dapat lebih berat di sisi negatif.

Skewness tidak boleh dipakai sendirian untuk menyimpulkan bahwa suatu strategi baik atau buruk. Ia hanya membantu memahami bentuk distribusi.

### Mengapa Win Rate yang Sama Tidak Berarti Hasil yang Sama?

Dua kelompok dapat sama-sama memiliki win rate 60%, tetapi distribusi hasilnya sangat berbeda.

| Ukuran | Kelompok A | Kelompok B |
|---|---|---|
| Win rate | 60% | 60% |
| Median return | +0,4% | +0,1% |
| Mean return | +0,3% | -0,2% |
| Kerugian terburuk | -1,5% | -8% |
| Keuntungan terbesar | +2% | +12% |

Kelompok B memiliki win rate yang sama, tetapi mean negatif dan kerugian ekstrem yang jauh lebih besar. Artinya, win rate saja tidak cukup untuk memahami kualitas suatu kondisi.

Inilah alasan TEKB mempelajari distribusi, bukan hanya jumlah kemenangan.

---

## 13.6. Return sebagai Variabel Penelitian

Harga adalah angka nominal. **Return** adalah perubahan harga yang dinyatakan sebagai ukuran perubahan relatif.

Misalnya, harga saham naik dari Rp1.000 menjadi Rp1.100. Kenaikannya Rp100 atau 10%.

Jika saham lain naik dari Rp10.000 menjadi Rp10.100, kenaikannya juga Rp100, tetapi return-nya hanya 1%.

Karena itu, membandingkan perubahan harga dalam rupiah saja dapat menyesatkan. Return membuat perubahan lebih mudah dibandingkan antarharga dan antarperiode.

Dalam TEKB, salah satu bentuk return yang digunakan adalah **log return**:

> r_t+1 = ln(C_t+1 / C_t)

Keterangan:

- C_t adalah harga close pada waktu t.
- C_t+1 adalah harga close pada periode berikutnya.
- r_t+1 adalah log return dari t menuju t+1.
- ln adalah logaritma natural.

Sebagai contoh, jika harga bergerak dari 100 menjadi 102:

> r = ln(102 / 100)

Hasilnya sekitar 0,0198 atau 1,98%.

Untuk perubahan harga yang kecil, log return nilainya sangat dekat dengan return persentase biasa. Log return juga memiliki beberapa sifat matematis yang berguna, terutama ketika perubahan terjadi secara berurutan.

Namun, pembaca tidak perlu menganggap log return sebagai angka yang lebih "benar" untuk semua tujuan. Ia adalah pilihan definisi penelitian yang harus konsisten. Jika TEKB menetapkan log return sebagai variabel utama, maka definisi tersebut harus digunakan secara sama pada B1, B0, IS, OOS, dan seluruh evaluasi yang relevan.

Yang penting adalah membedakan:

- **Harga:** berada pada satuan rupiah atau unit harga.
- **Return:** perubahan relatif dari satu harga ke harga berikutnya.
- **Log return:** bentuk return yang dihitung menggunakan logaritma natural.

Return lebih cocok untuk mempelajari distribusi hasil karena memungkinkan perubahan dari instrumen atau periode yang berbeda dibandingkan dalam satuan yang lebih seragam.

---

## 13.7. Distribusi Kondisional

Distribusi umum menggambarkan hasil dari seluruh event atau seluruh pengamatan. Namun, TEKB tidak hanya tertarik pada distribusi umum. TEKB ingin mengetahui apakah hasil berubah ketika kondisi tertentu hadir.

Inilah yang disebut **distribusi kondisional**.

Secara sederhana, distribusi kondisional berarti:

> Distribusi hasil yang diamati ketika suatu kondisi tertentu terpenuhi.

Kita dapat menuliskannya secara konseptual sebagai:

> P(r_t+1 | X_t)

Dibaca:

> Distribusi kemungkinan return berikutnya berdasarkan kondisi yang diketahui pada waktu t.

Keterangan:

- r_t+1 adalah return pada periode berikutnya.
- X_t adalah kondisi yang tersedia pada waktu t.
- Tanda | dibaca "dengan syarat" atau "diberikan kondisi".

Contoh X_t dapat berupa:

- SAMSON terdeteksi.
- Breakout terjadi.
- Pullback memenuhi definisi tertentu.
- Relative Volume berada di atas ambang tertentu.
- Harga berada di atas struktur tertentu.
- Candle memiliki karakteristik tertentu.
- Kombinasi kondisi OHLCV yang telah didefinisikan.

Misalnya, kita ingin mengetahui:

> "Bagaimana distribusi return tiga bar berikutnya ketika terjadi SAMSON dengan RV di atas 5?"

Maka kita mengumpulkan seluruh event yang memenuhi definisi tersebut, lalu mengukur return tiga bar setelah entry atau titik evaluasi yang telah ditentukan.

Hal yang sangat penting adalah bahwa kondisi harus didefinisikan sebelum hasil dihitung atau digunakan untuk memilih hasil terbaik. Jika kondisi diubah-ubah setelah melihat return, penelitian berisiko mengalami data snooping atau overfitting.

Contohnya, peneliti tidak boleh mencoba banyak ambang volume, banyak horizon, dan banyak aturan entry, kemudian hanya memilih kombinasi yang menghasilkan distribusi paling bagus tanpa memperhitungkan seluruh percobaan yang dilakukan.

Distribusi kondisional bukan berarti kondisi tersebut pasti menyebabkan hasil. Distribusi kondisional menunjukkan bahwa hasil memiliki pola tertentu ketika kondisi tersebut hadir. Dalam kerangka TEKB, hal ini disebut sebagai informasi kondisional atau **information content**, bukan otomatis bukti hubungan sebab-akibat.

---

## 13.8. Membandingkan Distribusi B1 dan B0

Distribusi **B1** menggambarkan hasil dari event atau kondisi yang sedang diteliti. Distribusi **B0** menggambarkan hasil dari pembanding yang dirancang agar konteksnya sebanding.

- B1 menjawab: "Apa yang terjadi ketika kondisi penelitian hadir?"
- B0 membantu menjawab: "Apa yang terjadi pada kondisi pembanding yang adil ketika kondisi penelitian tersebut tidak digunakan?"

Misalnya:

- B1 adalah event breakout yang memenuhi aturan tertentu.
- B0 adalah event pembanding pada instrumen dan slot waktu yang sama, tetapi tidak memenuhi kondisi breakout yang diteliti.

Kita kemudian membandingkan distribusi return B1 dan B0.

Perbandingan tidak boleh hanya melihat apakah mean B1 positif. Kita perlu melihat apakah B1 benar-benar berbeda dari B0 dalam aspek yang relevan.

Beberapa aspek yang dapat dibandingkan:

### 1. Pusat Distribusi

- Apakah median B1 lebih tinggi daripada median B0?
- Apakah mean B1 lebih tinggi daripada mean B0?

Perbedaan pusat dapat menunjukkan bahwa kondisi penelitian berkaitan dengan perubahan kecenderungan hasil.

### 2. Penyebaran

- Apakah B1 lebih stabil atau justru lebih bervariasi daripada B0?

Kenaikan mean yang disertai penyebaran sangat besar belum tentu memberikan informasi yang lebih baik.

### 3. Proporsi Return Positif

- Apakah B1 memiliki proporsi return positif yang lebih besar daripada B0?

Perbedaan win rate dapat relevan, tetapi tetap tidak cukup jika besar keuntungan dan kerugian berbeda jauh.

### 4. Ekor Distribusi

- Apakah B1 memiliki kerugian ekstrem yang lebih berat?
- Apakah B1 memiliki keuntungan ekstrem yang lebih besar?
- Apakah perbedaan hanya berasal dari beberapa event ekstrem?

### 5. Peluang Melewati Ambang Tertentu

Misalnya:

- P(r > 1%)
- P(r < -2%)
- P(r > 0)

Perbandingan semacam ini dapat membantu memahami apakah kondisi penelitian mengubah peluang hasil tertentu dibandingkan B0.

**Information edge** dapat dipahami sebagai perbedaan distribusi B1 dan B0 yang:

- Didefinisikan dengan aturan yang jelas.
- Dihasilkan tanpa look-ahead.
- Dibandingkan dengan pembanding yang adil.
- Tidak hanya bergantung pada satu angka yang kebetulan bagus.
- Memiliki dukungan bukti dan pengujian ketidakpastian.

B1 yang positif saja belum cukup. Jika B0 juga sama positifnya atau bahkan lebih baik, maka kondisi B1 mungkin tidak memberikan informasi tambahan yang berarti.

---

## 13.9. Pertanyaan yang Dapat Dijawab oleh Distribusi

Distribusi memungkinkan penelitian menjawab pertanyaan yang lebih kaya daripada sekadar "profit atau tidak".

Beberapa pertanyaan yang dapat diajukan antara lain:

### 1. Berapa Proporsi Return Positif?

Pertanyaan ini melihat seberapa sering hasil berada di atas nol.

Contoh:

> P(r > 0) = 60%

Artinya, 60% event dalam sampel menghasilkan return positif. Angka ini tetap harus dibaca sebagai proporsi historis atau estimasi, bukan kepastian.

### 2. Berapa Peluang Return Lebih Besar dari 1%?

> P(r > 1%)

Pertanyaan ini lebih spesifik daripada sekadar return positif. Return +0,01% dan +3% sama-sama positif, tetapi dampaknya berbeda.

### 3. Berapa Peluang Return Lebih Rendah dari -2%?

> P(r < -2%)

Ini membantu melihat frekuensi hasil yang melewati ambang kerugian tertentu.

### 4. Berapa Median Return?

Median menunjukkan hasil tengah. Ia membantu menjawab:

> "Jika seluruh event diurutkan, kira-kira di mana letak hasil tengahnya?"

Median sering lebih informatif daripada mean ketika distribusi memiliki outlier atau ekor ekstrem.

### 5. Berapa Percentile Bawah dan Atas?

Percentile dapat membantu menjawab:

- Seberapa buruk bagian bawah distribusi?
- Seberapa baik bagian atas distribusi?
- Di mana 10% hasil terburuk berada?
- Di mana 10% hasil terbaik berada?

Contoh, P10 = -2,5% berarti bagian bawah distribusi memiliki hasil yang cukup buruk. Namun, interpretasinya harus mengikuti definisi percentile yang digunakan oleh sistem.

### 6. Seberapa Besar Variasi Hasil?

Pertanyaan ini berkaitan dengan penyebaran, misalnya deviasi standar, rentang interpercentile, atau ukuran lain yang ditentukan dalam protokol.

Distribusi dengan median +0,5% tetapi penyebaran sangat besar berbeda dari distribusi dengan median +0,5% yang lebih sempit.

### 7. Seberapa Berat Ekor Kerugian?

Pertanyaan ini penting untuk memahami apakah kerugian ekstrem sering atau jarang terjadi.

Sebuah kondisi mungkin memiliki median positif, tetapi tetap memiliki ekor kerugian yang berbahaya. Karena itu, distribusi perlu dibaca secara keseluruhan, bukan hanya dari pusatnya.

---

## 13.10. Distribusi Bukan Ramalan Pasti

Misalkan hasil penelitian menunjukkan bahwa 60% event dalam sampel menghasilkan return positif.

Angka tersebut tidak berarti bahwa setiap lima trade berikutnya pasti menghasilkan:

- Tiga trade positif.
- Dua trade negatif.

Urutan aktual dapat berbeda:

- Positif, positif, positif, positif, positif.
- Negatif, negatif, positif, negatif, positif.
- Positif, negatif, negatif, positif, positif.

Semua urutan tersebut mungkin terjadi meskipun proporsi jangka panjangnya mendekati 60%.

Probabilitas tidak bekerja seperti jadwal yang wajib dipenuhi dalam kelompok kecil. Probabilitas adalah cara menyatakan ketidakpastian dan kecenderungan dalam proses yang memiliki banyak kemungkinan.

Distribusi juga tidak menjamin bahwa masa depan akan identik dengan masa lalu. Distribusi historis adalah gambaran berdasarkan sampel dan definisi penelitian tertentu. Ia dapat berubah ketika:

- Kondisi pasar berubah.
- Instrumen berubah.
- Likuiditas berubah.
- Periode pengamatan berbeda.
- Mekanisme pasar mengalami perubahan.

Karena itu, distribusi tidak menghilangkan ketidakpastian. Distribusi justru membantu membuat ketidakpastian terlihat, terukur, dan dapat dibicarakan secara jujur.

> Hasil stokastik bukan janji. Hasil stokastik adalah peta kemungkinan.

---

## 13.11. Hubungan Empiris, Stokastik, dan Bootstrap

Ketiga pendekatan ini saling berhubungan, tetapi memiliki fungsi yang berbeda.

### Empiris: Mencatat Apa yang Terjadi

Pendekatan empiris mengumpulkan event dan hasil aktual:

- Berapa event terjadi?
- Berapa return masing-masing event?
- Berapa MAE dan MFE?
- Berapa outcome yang mencapai target atau stop?

Empiris adalah dasar pengamatan.

### Stokastik: Menggambarkan Variasi Hasil

Pendekatan stokastik menyusun hasil tersebut menjadi distribusi:

- Median.
- Mean.
- Penyebaran.
- Percentile.
- Ekor.
- Peluang melewati ambang tertentu.

Stokastik membantu kita memahami bahwa hasil tidak tunggal.

### Bootstrap: Mengukur Ketidakpastian Estimasi

**Bootstrap** adalah metode untuk mempelajari seberapa stabil suatu ukuran hasil jika sampel yang tersedia dianggap sebagai dasar pengambilan ulang secara terstruktur.

Misalnya, kita memperoleh median return B1 sebesar +0,4%. Pertanyaannya:

> "Seberapa yakin kita bahwa median +0,4% tersebut bukan sekadar akibat komposisi sampel yang kebetulan?"

Bootstrap dapat digunakan untuk membentuk distribusi estimasi median, mean, selisih B1-B0, atau ukuran lain sesuai protokol.

Dengan pengulangan resampling, kita dapat melihat rentang hasil estimasi yang mungkin muncul. Dari sana, kita dapat membangun interval ketidakpastian atau mengukur kestabilan suatu perbedaan.

Namun, bootstrap tidak menciptakan bukti baru. Bootstrap tidak dapat mengubah sinyal yang tidak memiliki edge menjadi edge yang nyata.

Jika data awal:

- Bias.
- Mengandung look-ahead.
- Tidak representatif.
- Terlalu sedikit.
- Mengandung event yang tidak independen tetapi diperlakukan sembarangan.

Maka bootstrap tidak otomatis memperbaiki masalah tersebut.

Dalam TEKB:

- **Empiris** menjawab: "Apa yang terjadi?"
- **Stokastik** menjawab: "Bagaimana hasil-hasil itu tersebar?"
- **Bootstrap** membantu menjawab: "Seberapa tidak pastinya ukuran distribusi atau perbedaannya?"

Ketiganya harus digunakan sesuai fungsi masing-masing.

---

## 13.12. Kesimpulan yang Boleh dan Tidak Boleh Dibuat

Penelitian yang baik tidak hanya menghasilkan angka. Penelitian yang baik juga membatasi jenis kesimpulan yang boleh ditarik dari angka tersebut.

### Kesimpulan yang Boleh Dibuat

Contoh kesimpulan yang proporsional:

> "Pada sampel yang diamati, B1 memiliki median return lebih tinggi daripada B0."

Pernyataan ini terbatas pada sampel dan ukuran yang disebutkan.

> "Distribusi B1 menunjukkan proporsi return positif yang lebih besar dibandingkan B0."

Pernyataan ini membahas perbedaan distribusi, bukan menjamin hasil berikutnya.

> "Perbedaan antara B1 dan B0 perlu diuji ketidakpastiannya."

Pernyataan ini mengakui bahwa perbedaan yang terlihat belum tentu stabil atau cukup kuat.

> "Pada periode dan instrumen penelitian ini, kondisi tersebut berkaitan dengan distribusi return yang berbeda dari pembanding."

Pernyataan ini menggunakan bahasa hubungan atau asosiasi, bukan klaim sebab-akibat.

### Kesimpulan yang Tidak Boleh Dibuat

Berikut contoh kesimpulan yang melampaui bukti:

> "Sinyal ini pasti menyebabkan harga naik."

Data observasional biasanya tidak cukup untuk menyatakan sebab-akibat secara otomatis.

> "Probabilitas 70% berarti trade berikutnya pasti profit."

Probabilitas 70% tidak menjamin hasil setiap trade atau kelompok kecil trade.

> "Distribusi historis adalah jaminan masa depan."

Distribusi historis merupakan estimasi berdasarkan data masa lalu, bukan kontrak terhadap masa depan.

> "Win rate tinggi berarti strategi ini pasti menguntungkan."

Profitabilitas juga dipengaruhi oleh besar keuntungan, besar kerugian, biaya, slippage, frekuensi event, dan distribusi hasil secara keseluruhan.

> "Mean positif berarti sudah ada edge."

Mean positif pada B1 belum cukup. Kita perlu mengetahui apakah B0 juga positif, apakah perbedaannya bermakna, apakah ketidakpastiannya terkendali, dan apakah hasilnya bertahan pada data OOS.

---

## Penutup Bab

Perjalanan penelitian TEKB dimulai dari kejadian nyata. Kita mencatat event, mengukur return, MAE, MFE, dan outcome. Itu adalah fondasi empiris.

Namun, hasil trading tidak muncul sebagai angka tunggal yang selalu sama. Setiap kondisi dapat diikuti oleh berbagai hasil dengan tingkat variasi dan ketidakpastian tertentu. Karena itu, kita perlu melihat distribusi, bukan hanya frekuensi kemenangan.

Distribusi membantu kita memahami pusat hasil, penyebaran, percentile, dan ekor. Perbandingan B1 dan B0 membantu kita menilai apakah kondisi yang diteliti memberikan informasi tambahan dibandingkan pembanding yang adil.

Bootstrap kemudian membantu mengukur ketidakpastian estimasi, bukan menciptakan edge baru.

Dengan demikian, TEKB bergerak melalui urutan berpikir berikut:

> Kejadian nyata → Pengukuran empiris → Distribusi hasil → Perbandingan B1 dan B0 → Pengukuran ketidakpastian → Kesimpulan yang proporsional.

Tujuan akhirnya bukan mengubah ketidakpastian menjadi kepastian palsu. Tujuannya adalah memahami ketidakpastian dengan lebih jujur.

---

## Ringkasan Bab

- Pendekatan empiris mempelajari apa yang benar-benar terjadi dalam data historis.
- Data historis adalah sampel, bukan jaminan masa depan.
- Frekuensi historis dapat menjadi estimasi probabilitas, tetapi tetap mengandung ketidakpastian.
- Pendekatan stokastik mempelajari berbagai hasil yang mungkin, bukan hanya satu angka.
- Distribusi dapat dipahami melalui median, mean, penyebaran, percentile, dan ekor.
- Win rate yang sama tidak selalu berarti distribusi atau kualitas hasil yang sama.
- Return lebih berguna daripada perubahan harga mentah untuk membandingkan hasil.
- Distribusi kondisional menggambarkan kemungkinan return berdasarkan kondisi tertentu.
- B1 harus dibandingkan dengan B0, bukan dinilai hanya karena hasilnya positif.
- Bootstrap mengukur ketidakpastian estimasi dan tidak menciptakan edge.
- Kesimpulan TEKB harus dibatasi oleh data, definisi, sampel, dan protokol penelitian.
- Distribusi bukan ramalan pasti, melainkan cara membuat ketidakpastian terlihat.

---

## Pertanyaan Refleksi

1. Apa perbedaan antara mengatakan "60% event positif" dan "probabilitas event berikutnya positif adalah 60%"?
2. Mengapa hasil 100% positif dari 10 event belum dapat dianggap sebagai kepastian?
3. Mengapa mean dan median perlu dibaca bersama?
4. Mengapa dua kelompok dengan win rate sama dapat memiliki kualitas distribusi yang berbeda?
5. Apa fungsi distribusi kondisional dalam penelitian TEKB?
6. Mengapa B1 yang positif belum cukup untuk menyatakan adanya information edge?
7. Apa perbedaan fungsi empiris, stokastik, dan bootstrap?
8. Mengapa bootstrap tidak dapat memperbaiki data yang bias?
9. Apa bahaya menganggap probabilitas sebagai urutan hasil yang pasti?
10. Mengapa TEKB harus menggunakan bahasa kesimpulan yang proporsional?

---

## Kalimat Kunci

> Empiris mencatat apa yang terjadi. Stokastik menggambarkan apa saja yang mungkin terjadi. Bootstrap membantu mengukur seberapa tidak pasti perkiraan kita. TEKB membutuhkan ketiganya agar bukti tidak berubah menjadi kepastian palsu.

---

<div align="center">

[← Bab Sebelumnya](/posts/bab-12-candidate-sltp/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Bab Selanjutnya →](/posts/bab-14-evaluation-engine/)

</div>