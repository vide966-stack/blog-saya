---
title: "BAB 16 — Bootstrap: Mengukur Seberapa Dapat Dipercaya Hasil Penelitian"
published: 2026-09-12
description: "Bootstrap membantu mengukur ketidakpastian estimasi. Bab ini menjelaskan date-cluster bootstrap, moving block bootstrap, dan apa yang tidak bisa dilakukan bootstrap."
tags: ["bab-16", "bootstrap", "ketidakpastian", "resampling"]
category: "Bab"
draft: false
lang: ""
---

**BAGIAN V — MESIN YANG MENENTUKAN APAKAH SEBUAH HIPOTESIS BEKERJA**

---

## 16.1. Mengapa Rata-Rata Saja Tidak Cukup?

Bayangkan sebuah penelitian menguji 100 event trading. Setelah semua hasil dihitung, rata-rata return B1 ternyata +0,8%, sedangkan rata-rata return B0 hanya +0,2%. Perbedaannya adalah +0,6%.

Sekilas, hasil ini terlihat menarik. Kondisi B1 tampaknya memberikan hasil yang lebih baik daripada pembandingnya.

Namun, ada pertanyaan penting:

> Apakah perbedaan +0,6% tersebut benar-benar mencerminkan pola yang cukup stabil, atau hanya terjadi karena sampel penelitian sedang beruntung?

Pertanyaan ini penting karena hasil penelitian selalu berasal dari sampel. Kita tidak mengamati seluruh kemungkinan kejadian di pasar. Kita hanya mengamati sebagian event yang terjadi dalam periode dan instrumen tertentu.

Misalnya, dari 100 event B1, mungkin ada tiga event yang menghasilkan keuntungan sangat besar. Ketiga event tersebut dapat mengangkat rata-rata secara signifikan. Jika ketiga event itu tidak terjadi, atau jika penelitian dilakukan pada periode berbeda, hasil rata-ratanya mungkin jauh lebih kecil.

Dengan kata lain, rata-rata adalah ringkasan hasil yang diamati, bukan jaminan bahwa hasil tersebut akan selalu muncul kembali.

### Contoh sederhana

Misalkan terdapat lima hasil trading:

- -2%
- -1%
- +1%
- +2%
- +10%

Rata-ratanya adalah:

> (-2% - 1% + 1% + 2% + 10%) ÷ 5 = +2%

Rata-rata terlihat positif. Namun, sebagian besar hasil sebenarnya berada di sekitar -2% sampai +2%. Angka +10% yang ekstrem sangat memengaruhi rata-rata.

Jika event +10% tidak masuk ke dalam sampel, rata-ratanya menjadi:

> (-2% - 1% + 1% + 2%) ÷ 4 = 0%

Perubahan ini menunjukkan bahwa hasil penelitian mungkin sangat bergantung pada satu atau beberapa event ekstrem.

Karena itu, penelitian tidak cukup hanya melaporkan:

> "Rata-rata return B1 adalah +2%."

Penelitian juga perlu menjawab:

- Seberapa besar hasil dapat berubah jika sampelnya berbeda?
- Apakah hasil positif tetap muncul dalam banyak kemungkinan pengambilan sampel?
- Seberapa lebar rentang ketidakpastiannya?
- Apakah kesimpulan terutama ditentukan oleh beberapa event ekstrem?
- Apakah perbedaan B1 dan B0 cukup stabil untuk dianggap sebagai temuan yang layak diteliti lebih lanjut?

Di sinilah bootstrap digunakan.

Bootstrap membantu peneliti melihat seberapa sensitif suatu hasil terhadap variasi sampel.

---

## 16.2. Analogi Mengambil Ulang Kartu dari Kumpulan Data

Bootstrap dapat dipahami melalui analogi sederhana.

Bayangkan seluruh event penelitian ditulis pada kartu. Setiap kartu berisi informasi tentang satu event, misalnya:

- tanggal;
- instrumen;
- hasil B1;
- hasil B0;
- selisih hasil B1 dan B0;
- atau statistik lain yang sedang diteliti.

Misalkan kita memiliki 100 kartu. Dari 100 kartu tersebut, kita telah menghitung rata-rata perbedaan B1-B0.

Sekarang kita ingin mengetahui:

> Jika kita mengambil sampel 100 event lagi dari kumpulan data yang sama, seberapa besar kemungkinan rata-rata hasilnya berubah?

Dalam bootstrap, kita membuat sampel-sampel tiruan dengan cara mengambil kembali observasi dari kumpulan data yang tersedia.

Hal pentingnya adalah bahwa pengambilan dilakukan dengan **pengembalian** (with replacement). Artinya, setelah satu observasi dipilih, observasi tersebut dikembalikan lagi ke kumpulan data sehingga dapat terpilih kembali.

Sebagai contoh, kumpulan data awal terdiri dari lima observasi:

> A, B, C, D, E

Satu sampel bootstrap berukuran lima dapat berupa:

> A, C, C, E, B

Sampel berikutnya mungkin:

> D, D, A, E, E

Sampel berikutnya lagi mungkin:

> B, A, B, C, D

Tidak semua sampel harus berisi setiap observasi. Sebagian observasi dapat muncul beberapa kali, sementara observasi lain mungkin tidak muncul dalam satu pengambilan.

Dari setiap sampel bootstrap, kita menghitung statistik yang sama, misalnya:

- rata-rata return B1;
- rata-rata return B0;
- perbedaan rata-rata B1-B0;
- median;
- win rate;
- expectancy;
- atau statistik lain yang telah ditentukan sebelumnya.

Proses ini diulang berkali-kali, misalnya 1.000, 5.000, atau 10.000 kali.

Hasilnya bukan lagi satu angka, melainkan **distribusi hasil bootstrap**.

Distribusi tersebut menunjukkan bagaimana statistik penelitian dapat berubah ketika komposisi sampel mengalami variasi.

### Apa arti "mengambil ulang" dalam bootstrap?

Bootstrap bukan berarti kita menciptakan harga baru atau mensimulasikan pasar masa depan secara langsung.

Bootstrap menggunakan data yang telah tersedia sebagai dasar untuk membentuk banyak kemungkinan sampel. Tujuannya adalah mengukur ketidakpastian estimasi dari sampel tersebut.

Jadi, bootstrap tidak mengatakan:

> "Inilah yang pasti terjadi di masa depan."

Bootstrap lebih tepat dibaca sebagai:

> "Berdasarkan variasi yang terdapat dalam sampel penelitian ini, seberapa besar hasil statistik dapat berubah?"

---

## 16.3. Apa yang Ingin Diketahui Bootstrap?

Dalam penelitian TEKB, bootstrap bukan sekadar prosedur matematis tambahan. Bootstrap digunakan untuk menjawab pertanyaan tentang ketahanan dan ketidakpastian hasil.

### 1. Seberapa stabil perbedaan B1-B0?

TEKB tidak hanya ingin mengetahui apakah B1 menghasilkan return positif. B0 juga dapat menghasilkan return positif karena pasar memang bergerak naik.

Karena itu, fokus pentingnya adalah perbedaan antara keduanya.

Misalnya:

- Rata-rata B1 = +1,0%
- Rata-rata B0 = +0,3%
- Δ = B1 − B0 = +0,7%

Bootstrap dapat digunakan untuk melihat bagaimana nilai Δ berubah pada banyak sampel bootstrap.

Jika sebagian besar hasil bootstrap tetap berada di sekitar nilai positif, perbedaan tersebut tampak lebih stabil.

Sebaliknya, jika sebagian hasil bootstrap positif dan sebagian besar lainnya mendekati nol atau menjadi negatif, maka temuan tersebut lebih tidak pasti.

### 2. Seberapa sering hasil tetap positif?

Misalnya, dari 10.000 pengulangan bootstrap:

- 9.700 hasil menghasilkan Δ positif;
- 300 hasil menghasilkan Δ negatif atau nol.

Maka proporsi bootstrap yang positif adalah:

> 9.700 ÷ 10.000 = 97%

Angka ini dapat menjadi informasi tambahan bahwa hasil positif cukup sering muncul dalam pengulangan bootstrap.

Namun, proporsi positif tidak boleh ditafsirkan secara berlebihan. Angka 97% bukan berarti peluang strategi pasti untung 97% pada masa depan. Angka tersebut hanya menggambarkan proporsi hasil bootstrap yang positif berdasarkan prosedur dan data penelitian yang digunakan.

### 3. Berapa rentang ketidakpastian hasil?

Satu estimasi, misalnya Δ = +0,7%, tidak memberi tahu seberapa jauh estimasi tersebut dapat berubah.

Dari distribusi bootstrap, peneliti dapat menghitung interval ketidakpastian. Misalnya, interval bootstrap 95% secara sederhana dapat dilaporkan sebagai:

> Δ = +0,7%
> Interval bootstrap 95%: -0,1% sampai +1,5%

Interpretasinya:

Berdasarkan prosedur bootstrap yang digunakan, terdapat ketidakpastian yang cukup besar mengenai besarnya perbedaan sebenarnya. Rentang yang diperoleh masih mencakup nilai negatif maupun positif.

Sebaliknya, jika hasilnya:

> Δ = +0,7%
> Interval bootstrap 95%: +0,3% sampai +1,1%

Maka hasil tersebut terlihat lebih konsisten positif dalam kerangka sampel dan metode bootstrap yang digunakan.

Tetap perlu diingat bahwa interval bootstrap bukan jaminan mutlak dan bukan pernyataan bahwa 95% hasil masa depan pasti berada di dalam rentang tersebut.

### 4. Apakah hasil bergantung pada beberapa event ekstrem?

Bootstrap juga membantu melihat apakah hasil terutama ditentukan oleh sejumlah kecil event.

Misalnya, rata-rata Δ terlihat positif, tetapi ketika dilakukan pengambilan ulang, hasilnya berubah drastis karena beberapa event ekstrem hanya muncul pada sebagian sampel bootstrap.

Situasi ini menunjukkan bahwa hasil mungkin belum kuat.

Dalam laporan penelitian, kondisi tersebut perlu dijelaskan secara terbuka. Hasil yang bergantung pada sedikit event ekstrem tidak otomatis salah, tetapi harus diperlakukan dengan lebih hati-hati.

---

## 16.4. Mengapa TEKB Tidak Menganggap Semua Event Independen?

Bootstrap sederhana sering memiliki asumsi tersirat bahwa setiap observasi dapat diperlakukan seolah-olah berdiri sendiri.

Dalam data trading, asumsi ini sering tidak sepenuhnya benar.

Dua event yang terjadi berdekatan dapat saling berkaitan. Event yang muncul pada tanggal yang sama dapat dipengaruhi oleh berita, kondisi pasar, atau pergerakan instrumen yang sama. Event dalam satu periode volatilitas tinggi juga mungkin memiliki karakteristik yang serupa.

### Contoh event yang saling berkaitan

Bayangkan terdapat lima event:

- Event A pada pukul 09.00;
- Event B pada pukul 09.05;
- Event C pada pukul 09.10;
- Event D pada pukul 09.15;
- Event E pada pukul 14.00.

Event A, B, C, dan D mungkin terjadi dalam satu rangkaian pergerakan harga yang sama. Keempat event tersebut tidak sepenuhnya memberikan empat informasi yang berdiri sendiri.

Jika harga melonjak karena satu berita besar, beberapa sinyal yang muncul sesudahnya dapat merupakan bagian dari episode pasar yang sama.

Apabila semua event tersebut diperlakukan sebagai observasi independen, jumlah informasi efektif dapat terlihat lebih besar daripada kenyataannya.

Akibatnya, hasil penelitian dapat tampak lebih pasti daripada yang seharusnya.

### Mengapa bootstrap biasa bisa terlalu optimistis?

Misalkan terdapat 100 event, tetapi 40 event sebenarnya berasal dari hanya beberapa episode pasar yang saling berkaitan.

Jika bootstrap mengambil event individual secara acak tanpa memperhatikan hubungan tersebut, event-event dari episode yang sama dapat muncul berulang kali dalam satu sampel bootstrap.

Hal ini dapat membuat prosedur seolah-olah memiliki banyak bukti independen, padahal sebagian bukti berasal dari sumber atau kondisi pasar yang sama.

Dampaknya dapat berupa:

- interval ketidakpastian yang terlalu sempit;
- estimasi kestabilan yang terlalu optimistis;
- keyakinan berlebihan bahwa perbedaan B1-B0 benar-benar kuat.

Karena itu, TEKB perlu mempertimbangkan struktur ketergantungan dalam data.

Dua pendekatan yang relevan adalah:

- **date-cluster bootstrap**;
- **moving block bootstrap**.

Keduanya tidak menyelesaikan semua persoalan ketergantungan, tetapi lebih sesuai daripada selalu mengacak event individual tanpa memperhatikan struktur waktu.

---

## 16.5. Date-Cluster Bootstrap

### Apa itu cluster tanggal?

Dalam date-cluster bootstrap, event dikelompokkan berdasarkan tanggal.

Misalnya, data penelitian memiliki event sebagai berikut:

| Tanggal | Event |
|---|---|
| 1 Januari | A, B, C |
| 2 Januari | D |
| 3 Januari | E, F |
| 4 Januari | G, H, I, J |
| 5 Januari | K |

Maka unit pengambilan ulang bukan lagi event individual, melainkan kelompok tanggal:

- Cluster 1 Januari = A, B, C;
- Cluster 2 Januari = D;
- Cluster 3 Januari = E, F;
- Cluster 4 Januari = G, H, I, J;
- Cluster 5 Januari = K.

Jika penelitian memiliki lima tanggal, satu sampel bootstrap dapat mengambil lima cluster dengan pengembalian, misalnya:

> 1 Januari, 3 Januari, 3 Januari, 5 Januari, 4 Januari

Seluruh event dari setiap tanggal yang terpilih ikut masuk ke sampel bootstrap.

Dengan demikian, jika satu tanggal memiliki beberapa event yang saling berkaitan, hubungan tersebut tetap dipertahankan di dalam cluster.

### Mengapa mengambil cluster tanggal?

Pendekatan ini membantu menjaga ketergantungan yang mungkin terjadi di dalam satu tanggal.

Misalnya, pada tanggal tertentu terdapat berita besar yang menyebabkan:

- volume meningkat;
- volatilitas melonjak;
- beberapa event muncul;
- harga bergerak dalam arah yang sama.

Jika event diacak satu per satu, hubungan antar-event tersebut dapat rusak. Namun, jika seluruh event pada tanggal itu diambil sebagai satu cluster, episode tanggal tersebut tetap diperlakukan sebagai satu kelompok.

Dengan cara ini, bootstrap tidak sepenuhnya berpura-pura bahwa setiap event merupakan informasi independen.

### Apa yang dihitung pada setiap pengulangan?

Pada setiap pengulangan date-cluster bootstrap, peneliti:

1. memilih sejumlah cluster tanggal dengan pengembalian;
2. memasukkan seluruh event dari tanggal-tanggal terpilih;
3. menghitung statistik yang telah ditetapkan;
4. menyimpan hasil statistik tersebut.

Statistik yang dihitung dapat berupa:

- rata-rata B1;
- rata-rata B0;
- Δ B1-B0;
- median perbedaan;
- expectancy;
- win rate;
- selisih net expectancy;
- atau statistik lain yang ditentukan dalam protokol.

Proses tersebut diulang berkali-kali untuk membentuk distribusi bootstrap.

### Contoh interpretasi

Misalnya, hasil penelitian menunjukkan:

> Δ observed = +0,65%

Setelah dilakukan date-cluster bootstrap 10.000 kali, diperoleh:

- median bootstrap = +0,63%;
- interval bootstrap 95% = +0,12% sampai +1,20%;
- proporsi Δ positif = 98,1%.

Interpretasi yang hati-hati:

Dalam pengulangan yang mempertahankan pengelompokan event berdasarkan tanggal, perbedaan B1-B0 umumnya tetap positif. Namun, hasil ini tetap merupakan estimasi berbasis sampel historis dan bergantung pada kualitas data, aturan pengelompokan, serta prosedur bootstrap yang digunakan.

Jika intervalnya justru sangat lebar, misalnya:

> -0,40% sampai +1,70%

maka peneliti perlu menyimpulkan bahwa arah atau besarnya perbedaan belum cukup pasti, meskipun estimasi utamanya positif.

### Batasan date-cluster bootstrap

Date-cluster bootstrap membantu menjaga ketergantungan dalam tanggal, tetapi tidak otomatis menangkap seluruh ketergantungan waktu.

Event pada tanggal yang berdekatan dapat tetap saling berkaitan. Misalnya, tren pasar selama satu minggu, krisis selama satu bulan, atau periode volatilitas tinggi dapat membuat beberapa tanggal berurutan memiliki karakteristik serupa.

Karena itu, date-cluster bootstrap bukan solusi universal. Ia merupakan pendekatan yang sesuai untuk jenis struktur tertentu, terutama ketika ketergantungan dalam tanggal dianggap penting.

---

## 16.6. Moving Block Bootstrap

### Apa itu block bootstrap?

Moving block bootstrap mempertahankan kelompok observasi yang berdekatan dalam urutan waktu.

Alih-alih mengambil event satu per satu secara acak, data dibagi atau dipandang sebagai rangkaian blok berurutan. Blok-blok tersebut kemudian diambil ulang dengan pengembalian untuk membentuk sampel bootstrap baru.

Misalnya, data event berurutan adalah:

> A, B, C, D, E, F, G, H, I, J

Jika panjang blok ditetapkan tiga, beberapa blok yang mungkin adalah:

- A, B, C;
- B, C, D;
- C, D, E;
- D, E, F;
- E, F, G;
- F, G, H;
- G, H, I;
- H, I, J.

Disebut **moving block** karena blok dapat bergerak sepanjang urutan waktu, sehingga setiap posisi berurutan dapat menjadi awal sebuah blok.

Sampel bootstrap kemudian dibentuk dengan mengambil blok-blok tersebut secara acak, misalnya:

> C, D, E | H, I, J | B, C, D | F, G, H

Dalam penerapan sebenarnya, panjang sampel akhir, aturan penyambungan blok, serta cara menangani batas data harus ditentukan secara eksplisit.

### Mengapa event berurutan perlu dipertahankan?

Event trading yang berdekatan dapat memiliki ketergantungan karena:

- tren harga belum selesai;
- volatilitas masih berada pada rezim yang sama;
- volume masih dipengaruhi berita yang sama;
- sinyal muncul dalam episode pasar yang sama;
- event sebelumnya dapat memengaruhi kemungkinan munculnya event berikutnya.

Jika urutan tersebut diacak sepenuhnya, struktur ketergantungan dapat hilang.

Moving block bootstrap berusaha mempertahankan sebagian hubungan lokal tersebut dengan mengambil kelompok event yang berdekatan, bukan event individual secara terpisah.

### Fungsi panjang blok

Panjang blok menentukan seberapa banyak struktur lokal yang dipertahankan.

- Blok terlalu pendek dapat gagal mempertahankan ketergantungan yang sebenarnya berlangsung lebih lama.
- Blok terlalu panjang dapat mengurangi jumlah blok efektif dan membuat estimasi menjadi lebih tidak stabil.

Panjang blok yang berbeda dapat menghasilkan rentang bootstrap yang berbeda.

Karena itu, panjang blok bukan detail kecil yang boleh disembunyikan. Ia merupakan bagian dari definisi metode penelitian.

Dalam TEKB, misalnya, moving block bootstrap dapat menggunakan panjang blok yang telah ditentukan dalam protokol penelitian. Jika protokol menetapkan panjang blok lima, maka angka tersebut harus dicatat dan tidak diubah hanya karena hasil tertentu terlihat lebih menarik.

### Mengapa block length harus ditetapkan dan dicatat?

Jika peneliti mencoba banyak panjang blok lalu hanya melaporkan hasil yang paling menguntungkan, prosedur bootstrap dapat berubah menjadi bentuk lain dari data snooping.

Karena itu, penelitian perlu mencatat:

- metode bootstrap;
- unit pengambilan ulang;
- panjang blok;
- jumlah pengulangan;
- statistik yang dihitung;
- seed atau pengaturan reproduksibilitas;
- aturan kelayakan event;
- aturan penanganan pasangan B1-B0;
- versi protokol yang digunakan.

Dengan pencatatan tersebut, pembaca dapat mengetahui bagaimana rentang ketidakpastian diperoleh.

### Date-cluster bootstrap dan moving block bootstrap

Kedua metode ini memiliki fokus yang berbeda.

| Aspek | Date-cluster bootstrap | Moving block bootstrap |
|---|---|---|
| Unit dasar | Kelompok tanggal | Blok event berurutan |
| Struktur yang dijaga | Ketergantungan dalam tanggal | Ketergantungan lokal sepanjang waktu |
| Cocok untuk | Event yang mengelompok pada tanggal tertentu | Event berurutan yang saling berkaitan |
| Parameter penting | Definisi cluster tanggal | Panjang blok |
| Keterbatasan | Tidak selalu menangkap ketergantungan lintas tanggal | Hasil sensitif terhadap panjang blok |

Pemilihan metode harus mengikuti struktur data dan protokol penelitian, bukan dipilih setelah melihat metode mana yang menghasilkan interval paling menarik.

---

## 16.7. Apa yang Tidak Dilakukan Bootstrap?

Bootstrap berguna, tetapi kemampuannya terbatas. Ia tidak boleh diperlakukan sebagai alat yang dapat memperbaiki seluruh kelemahan penelitian.

### 1. Bootstrap tidak membuktikan kausalitas

Jika B1 memiliki hasil lebih baik daripada B0, bootstrap dapat membantu mengukur ketidakpastian perbedaan tersebut.

Namun, bootstrap tidak membuktikan bahwa kondisi B1 **menyebabkan** hasil tersebut.

Perbedaan dapat muncul karena:

- faktor pasar lain;
- perubahan rezim;
- karakteristik instrumen;
- kondisi makroekonomi;
- pemilihan event;
- atau variabel lain yang belum dikendalikan.

Dalam TEKB, kesimpulan utama tetap berada pada ranah **information content** atau hubungan bersyarat, bukan otomatis hubungan sebab-akibat.

### 2. Bootstrap tidak menjamin masa depan

Bootstrap menggunakan struktur informasi dari sampel yang tersedia. Jika masa depan memiliki kondisi yang benar-benar berbeda, bootstrap tidak dapat menjaminnya.

Misalnya, data historis didominasi pasar bullish. Bootstrap dari data tersebut tidak otomatis memberi gambaran akurat tentang periode bearish ekstrem.

Bootstrap membantu mengukur ketidakpastian estimasi dari sampel, bukan menjamin bahwa distribusi masa depan akan sama.

### 3. Bootstrap tidak menciptakan edge

Jika B1 tidak memiliki perbedaan yang berarti dibandingkan B0, bootstrap tidak dapat mengubahnya menjadi edge yang nyata.

Bootstrap hanya mengulang proses pengambilan sampel dari data yang ada. Ia tidak menambahkan informasi baru tentang pasar.

Jika estimasi Δ mendekati nol, distribusi bootstrap kemungkinan juga akan berpusat di sekitar nol, meskipun variasinya perlu diukur.

### 4. Bootstrap tidak menggantikan B0

Bootstrap tidak menjawab pertanyaan:

> "Apakah B1 lebih baik daripada kondisi pembanding yang adil?"

Bootstrap hanya membantu menjawab:

> "Seberapa tidak pasti estimasi perbedaan yang telah kita hitung?"

B0 tetap diperlukan untuk membangun perbandingan yang bermakna. Tanpa B0, peneliti mungkin hanya mengukur apakah B1 menghasilkan keuntungan, bukan apakah B1 memiliki informasi tambahan dibandingkan kondisi dasar.

### 5. Bootstrap tidak boleh digunakan untuk mengubah aturan setelah melihat hasil

Aturan penelitian harus ditetapkan sebelum hasil bootstrap digunakan untuk mengambil keputusan metodologis.

Misalnya, peneliti tidak boleh:

- mencoba banyak metode bootstrap lalu memilih yang paling positif;
- mengubah panjang blok setelah melihat interval yang tidak menarik;
- menghapus event yang membuat hasil bootstrap melemah;
- mengganti definisi B1 atau B0 setelah melihat distribusi;
- memilih statistik yang paling menguntungkan setelah pengujian;
- menjalankan bootstrap berulang kali sampai hasil terlihat signifikan lalu hanya melaporkan percobaan terakhir.

Bootstrap harus menjadi bagian dari protokol yang terdokumentasi, bukan alat untuk mencari pembenaran.

### 6. Bootstrap tidak menghapus bias pada data

Jika data mengandung:

- look-ahead bias;
- survivorship bias;
- data snooping;
- kesalahan corporate action;
- kesalahan timestamp;
- atau aturan entry yang tidak realistis;

maka bootstrap hanya akan mengulang data yang sudah bermasalah tersebut.

Prinsipnya sederhana:

> Bootstrap dapat membantu mengukur ketidakpastian dari penelitian, tetapi tidak dapat menyucikan penelitian yang sejak awal tidak valid.

---

## 16.8. Cara Membaca Hasil Bootstrap

Hasil bootstrap sebaiknya tidak dibaca hanya dari satu angka. Setidaknya terdapat beberapa komponen yang perlu diperhatikan.

### 1. Estimasi utama

Estimasi utama adalah hasil yang dihitung dari data asli sebelum pengulangan bootstrap.

Contoh:

> Δ observed = +0,70%

Angka ini menunjukkan perbedaan yang diamati antara B1 dan B0 pada sampel penelitian asli.

Namun, angka ini belum memberi informasi lengkap tentang ketidakpastiannya.

### 2. Distribusi bootstrap

Distribusi bootstrap menunjukkan kumpulan nilai statistik yang dihasilkan dari banyak pengambilan ulang.

Distribusi ini dapat diperiksa melalui:

- nilai tengah;
- penyebaran;
- kemiringan;
- ekor;
- nilai minimum dan maksimum;
- serta proporsi hasil positif atau negatif.

Jika distribusi sangat sempit dan terkonsentrasi di sekitar nilai positif, hasil terlihat lebih stabil dalam prosedur tersebut.

Jika distribusi sangat lebar atau menyebar di sekitar nol, hasil lebih tidak pasti.

### 3. Interval ketidakpastian

Interval ketidakpastian memberikan rentang nilai yang membantu pembaca memahami variasi estimasi.

Contoh:

> Δ observed = +0,70%
> Interval bootstrap 95% = +0,25% sampai +1,10%

Hasil ini menunjukkan bahwa distribusi bootstrap lebih banyak berada di wilayah positif.

Contoh lain:

> Δ observed = +0,70%
> Interval bootstrap 95% = -0,30% sampai +1,60%

Hasil ini menunjukkan bahwa estimasi utama positif, tetapi ketidakpastiannya cukup besar dan masih mencakup nilai negatif.

Interval tersebut harus selalu dibaca bersama:

- ukuran sampel;
- unit bootstrap;
- metode pengelompokan;
- panjang blok jika digunakan;
- definisi statistik;
- dan kualitas data.

### 4. Proporsi hasil bootstrap yang positif

Misalnya:

> 8.900 dari 10.000 pengulangan menghasilkan Δ > 0.

Proporsi positifnya adalah 89%.

Angka ini menunjukkan bahwa hasil positif cukup sering muncul dalam pengulangan bootstrap. Namun, angka tersebut tidak sama dengan:

- probabilitas trade berikutnya untung;
- probabilitas strategi akan menguntungkan;
- probabilitas hipotesis pasti benar;
- atau jaminan performa OOS.

Proporsi positif hanya merupakan ringkasan dari distribusi bootstrap yang dibentuk berdasarkan data dan prosedur tertentu.

### 5. Hasil positif belum tentu cukup stabil

Ini adalah salah satu pelajaran terpenting.

Sebuah estimasi dapat positif, tetapi belum tentu cukup stabil untuk dijadikan dasar keputusan.

Misalnya:

> Δ observed = +1,2%

Tetapi hasil bootstrap menunjukkan:

- interval sangat lebar;
- sebagian besar variasi berasal dari event ekstrem;
- proporsi positif hanya 55%;
- hasil berubah drastis ketika satu periode dihilangkan.

Dalam kondisi ini, kesimpulan yang tepat bukan:

> "Edge sudah terbukti."

Kesimpulan yang lebih tepat:

> "Estimasi awal positif, tetapi kestabilan hasil masih lemah dan memerlukan penelitian lanjutan."

Sebaliknya, hasil yang lebih meyakinkan dapat memiliki karakteristik:

- perbedaan B1-B0 tetap positif dalam sebagian besar pengulangan;
- interval ketidakpastian relatif lebih sempit;
- hasil tidak hanya ditentukan oleh satu atau dua event;
- pola tetap terlihat pada berbagai kelompok waktu;
- hasil tidak runtuh ketika satu instrumen atau periode dikeluarkan;
- dan hasil tersebut tetap perlu diuji melalui OOS.

### Contoh membaca dua hasil

#### Hasil A

- Δ observed = +0,80%
- Proporsi bootstrap positif = 97%
- Interval bootstrap 95% = +0,20% sampai +1,30%

**Interpretasi:**

Hasil menunjukkan perbedaan positif yang relatif konsisten dalam prosedur bootstrap yang digunakan. Namun, temuan ini belum otomatis membuktikan kausalitas atau menjamin hasil masa depan. Pengujian OOS dan pemeriksaan robustness tetap diperlukan.

#### Hasil B

- Δ observed = +0,80%
- Proporsi bootstrap positif = 58%
- Interval bootstrap 95% = -1,00% sampai +2,40%

**Interpretasi:**

Estimasi awal positif, tetapi ketidakpastiannya tinggi. Distribusi bootstrap masih sering menghasilkan nilai negatif. Temuan ini belum cukup stabil untuk dianggap sebagai bukti kuat adanya edge.

### 6. Apa yang sebaiknya dilaporkan dalam penelitian TEKB?

Agar hasil dapat diaudit dan direproduksi, laporan bootstrap sebaiknya mencantumkan:

- nama statistik yang diuji;
- estimasi dari data asli;
- metode bootstrap;
- unit pengambilan ulang;
- apakah menggunakan date-cluster atau moving block bootstrap;
- panjang blok jika menggunakan block bootstrap;
- jumlah pengulangan;
- seed atau pengaturan reproduksibilitas;
- interval ketidakpastian yang digunakan;
- proporsi hasil bootstrap yang positif;
- jumlah event dan jumlah cluster atau blok;
- aturan kelayakan event;
- definisi B1 dan B0;
- versi protokol penelitian;
- serta keterbatasan interpretasi.

Contoh format ringkas:

| Komponen | Hasil |
|---|---|
| Statistik | Δ mean B1-B0 |
| Estimasi observed | +0,70% |
| Metode | Date-cluster bootstrap |
| Jumlah pengulangan | 10.000 |
| Interval | Bootstrap 95% |
| Interval hasil | +0,20% sampai +1,15% |
| Proporsi Δ positif | 96,8% |
| Unit cluster | Tanggal |
| Interpretasi | Positif dan relatif stabil dalam sampel, tetapi tetap memerlukan OOS |

---

## Ringkasan Bab

- Bootstrap adalah metode untuk mempelajari ketidakpastian estimasi dengan membentuk banyak sampel pengulangan dari data yang tersedia.
- Metode ini membantu menjawab pertanyaan:
  - Seberapa stabil rata-rata atau perbedaan B1-B0?
  - Seberapa sering hasil tetap positif?
  - Seberapa lebar rentang ketidakpastian?
  - Apakah hasil terlalu bergantung pada beberapa event ekstrem?
- Dalam TEKB, pengambilan ulang tidak boleh selalu memperlakukan semua event sebagai observasi independen. Event dapat saling berkaitan karena terjadi pada tanggal yang sama, berada dalam episode pasar yang sama, atau muncul berurutan dalam waktu yang berdekatan.
- Karena itu, TEKB dapat menggunakan pendekatan seperti:
  - **date-cluster bootstrap**, yang mengambil ulang kelompok tanggal;
  - **moving block bootstrap**, yang mengambil ulang blok event berurutan.
- Bootstrap bukan alat untuk membuktikan kausalitas, menjamin masa depan, menciptakan edge, menggantikan B0, atau memperbaiki bias data. Ia hanya membantu mengukur seberapa tidak pasti hasil penelitian berdasarkan data dan prosedur yang digunakan.

Kesimpulan yang baik tidak hanya berbunyi:

> "Hasilnya positif."

Kesimpulan yang lebih bertanggung jawab adalah:

> "Hasilnya positif, tetapi seberapa stabil hasil tersebut, seberapa besar ketidakpastiannya, dan apakah perbedaan itu tetap terlihat ketika struktur ketergantungan data diperhitungkan?"

---

## Pertanyaan Refleksi

1. Mengapa rata-rata hasil penelitian tidak selalu cukup untuk menyimpulkan bahwa sebuah sinyal memiliki edge?
2. Apa perbedaan antara satu estimasi dan distribusi bootstrap?
3. Mengapa bootstrap menggunakan pengambilan ulang dengan pengembalian?
4. Mengapa event yang berdekatan tidak selalu dapat dianggap independen?
5. Apa fungsi date-cluster bootstrap?
6. Apa fungsi panjang blok dalam moving block bootstrap?
7. Mengapa bootstrap tidak dapat menggantikan B0?
8. Mengapa bootstrap tidak membuktikan kausalitas?
9. Apa arti interval bootstrap yang masih mencakup nilai negatif?
10. Mengapa hasil positif belum tentu berarti hasil tersebut cukup stabil?

---

## Kalimat Kunci

> Bootstrap tidak membuat hasil penelitian menjadi benar. Bootstrap membantu kita melihat seberapa tidak pasti hasil tersebut. Dalam TEKB, bukti yang baik bukan hanya hasil yang positif, melainkan hasil yang tetap masuk akal ketika variasi sampel dan ketergantungan data diperhitungkan.

---

<div align="center">

[← Bab Sebelumnya](/posts/bab-15-hasil-jadi-angka/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Bab Selanjutnya →](/posts/bab-17-multiple-testing-bh-fdr/)

</div>