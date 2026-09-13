---
title: "BAB 25 — TEKB sebagai Disiplin Berpikir"
published: 2026-09-12
description: "TEKB bukan sekadar sistem penelitian trading, melainkan latihan untuk membangun kebiasaan berpikir yang lebih jujur ketika berhadapan dengan ketidakpastian."
tags: ["bab-25", "disiplin-berpikir", "filosofi", "penutup"]
category: "Bab"
draft: false
lang: ""
---

**BAGIAN VIII — BATASAN, ASUMSI, DAN ARAH PENGEMBANGAN**

---

TEKB pada akhirnya bukan hanya tentang data harga, volume, rumus, kode program, atau mesin evaluasi. Semua itu memang penting, tetapi bukan inti terdalamnya. Inti TEKB adalah **cara berpikir**.

TEKB mengajarkan kita untuk tidak terburu-buru mengubah pola menjadi keyakinan, keyakinan menjadi keputusan, dan keputusan menjadi tindakan. Sebaliknya, TEKB mengajak kita melewati proses yang lebih disiplin: mengamati, bertanya, merumuskan hipotesis, mengukur, membandingkan, menguji, mendokumentasikan, lalu mengambil keputusan sesuai kekuatan bukti.

Dengan demikian, TEKB bukan sekadar sistem penelitian trading. TEKB adalah latihan untuk membangun kebiasaan berpikir yang lebih jujur ketika berhadapan dengan ketidakpastian.

---

## 25.1. Dari Sinyal Menuju Pertanyaan

Dalam trading, kita sering memulai dari sebuah pola.

Volume tiba-tiba meningkat. Harga menembus resistance. Sebuah candle terlihat kuat. Harga mengalami pullback lalu kembali naik. Indikator menunjukkan kondisi tertentu. Dari pola tersebut, kita kemudian berkata:

- "Ini tanda harga akan naik."
- "Ini sinyal entry."
- "Pola ini biasanya menghasilkan profit."
- "Kalau kondisi ini muncul, kemungkinan besar harga melanjutkan tren."

Masalahnya, pola yang terlihat meyakinkan belum tentu memiliki informasi yang benar-benar berguna. Mata manusia sangat pandai menemukan keteraturan, termasuk keteraturan yang sebenarnya muncul secara kebetulan.

Karena itu, TEKB tidak memulai dengan pertanyaan:

> "Apakah pola ini bagus?"

TEKB mengubahnya menjadi pertanyaan yang lebih terukur:

> "Apakah kondisi ini berkaitan dengan hasil masa depan yang berbeda dari pembanding yang adil?"

Perubahan ini terlihat sederhana, tetapi sangat penting. Pertanyaan "apakah pola ini bagus?" cenderung mengundang pembenaran. Kita mungkin hanya mencari contoh yang mendukung keyakinan awal.

Sebaliknya, pertanyaan penelitian memaksa kita menentukan:

- Apa yang dimaksud dengan kondisi tersebut?
- Kapan kondisi dianggap terjadi?
- Apa hasil yang akan diukur?
- Berapa lama hasil itu diamati?
- Dibandingkan dengan apa?
- Seberapa besar perbedaannya?
- Seberapa tidak pasti hasil tersebut?

Dengan cara ini, sinyal tidak langsung diperlakukan sebagai kebenaran. Sinyal diperlakukan sebagai bahan awal untuk membangun hipotesis.

Contohnya, daripada mengatakan:

> "Volume besar setelah breakout pasti menunjukkan akumulasi."

TEKB akan merumuskannya secara lebih hati-hati:

> "Pada kondisi breakout tertentu yang disertai anomali volume, apakah distribusi return beberapa bar berikutnya berbeda dari kondisi pembanding yang memenuhi aturan serupa tetapi tidak memiliki anomali volume?"

Kalimat kedua memang lebih panjang. Namun, justru karena lebih panjang, ia lebih jelas, lebih dapat diuji, dan lebih sulit dimanipulasi setelah melihat hasil.

Inilah langkah pertama dalam disiplin berpikir TEKB:

> Jangan langsung percaya pada pola. Ubah pola menjadi pertanyaan yang dapat diuji.

---

## 25.2. Dari Hipotesis Menuju Pengukuran

Hipotesis yang baik belum cukup. Hipotesis harus diterjemahkan menjadi aturan pengukuran yang jelas.

Sebuah penelitian dapat terlihat ilmiah karena menggunakan banyak istilah teknis, tetapi tetap lemah apabila definisinya berubah-ubah. Misalnya, "breakout" dapat berarti menembus high sebelumnya, menutup di atas resistance, atau sekadar bergerak beberapa persen dari harga tertentu. "Volume besar" juga dapat berarti dua kali rata-rata, berada di atas persentil ke-95, atau terlihat besar secara visual.

Jika definisi tidak dikunci, hasil penelitian dapat berubah hanya karena peneliti mengubah arti istilah setelah melihat data.

Karena itu, TEKB memecah hipotesis menjadi beberapa komponen yang harus ditentukan sejak awal.

### 1. Menentukan event

**Event** adalah kejadian yang menjadi unit penelitian.

Misalnya:

- munculnya anomali volume;
- breakout;
- pullback;
- candle konfirmasi;
- kondisi OHLCV tertentu;
- kombinasi aturan yang telah ditentukan.

Event harus memiliki identitas yang jelas, termasuk instrumen, tanggal, waktu, sesi, slot, dan versi aturan yang digunakan.

Satu event bukan sekadar "saya melihat pola di chart". Event harus dapat ditemukan kembali oleh mesin atau peneliti lain dengan aturan yang sama.

### 2. Menentukan entry

Kita harus membedakan antara waktu sinyal dan waktu entry.

Jika sinyal baru diketahui setelah candle T selesai, maka entry yang benar-benar dapat digunakan dalam penelitian mungkin berada pada open bar berikutnya, yaitu T+1.

Harga close candle sinyal tidak boleh diam-diam dipakai sebagai harga entry apabila pada saat close tersebut keputusan belum dapat dieksekusi sesuai aturan yang ditentukan.

Perbedaan kecil antara signal close dan entry open dapat mengubah hasil penelitian secara besar. Karena itu, TEKB memperlakukan definisi entry sebagai bagian penting dari validitas penelitian.

### 3. Menentukan hasil

Apa yang dimaksud dengan "berhasil"?

Apakah harga naik satu persen? Apakah return positif pada akhir tiga bar? Apakah target profit tercapai sebelum stop-loss? Apakah hasil dihitung sebelum atau sesudah biaya?

Semua pertanyaan ini harus dijawab secara eksplisit.

TEKB tidak cukup mengatakan bahwa suatu event "berhasil" atau "gagal". Hasil harus diterjemahkan menjadi ukuran yang dapat dihitung, misalnya:

- return;
- MAE;
- MFE;
- hasil dalam satuan ×ATR;
- outcome SL/TP;
- expectancy;
- distribusi hasil;
- hasil bersih setelah biaya.

### 4. Menentukan horizon

Hasil harus diamati pada rentang waktu yang jelas.

Misalnya:

- satu bar berikutnya;
- tiga bar;
- lima bar;
- sepuluh bar;
- atau maksimum holding period tertentu.

Tanpa horizon, kalimat "harga naik setelah sinyal" tidak memiliki makna yang cukup jelas. Harga mungkin naik setelah tiga bar, tetapi turun setelah dua puluh bar. Harga mungkin sempat naik besar, tetapi akhirnya ditutup rugi.

Horizon membuat pertanyaan penelitian menjadi spesifik.

### 5. Menentukan pembanding

Hasil suatu event tidak dapat dinilai secara adil tanpa pembanding.

Jika B1 menghasilkan return positif, pertanyaan berikutnya adalah:

> "Apakah return tersebut benar-benar lebih baik daripada kondisi yang sebanding tanpa fitur yang sedang diuji?"

Di sinilah B0 berperan. B0 bukan sekadar angka pembanding tambahan, melainkan alat untuk mencegah kita menganggap gerakan pasar umum sebagai keunggulan sinyal.

Tanpa pembanding yang adil, kita mungkin hanya menemukan bahwa pasar memang sedang naik, bukan bahwa event yang diteliti memiliki informasi tambahan.

Dengan demikian, hipotesis dalam TEKB harus berubah menjadi struktur pengukuran:

> Event → Entry → Horizon → Outcome → B0 → Perbandingan.

Jika salah satu bagian ini kabur, kesimpulan akhirnya juga menjadi kabur.

---

## 25.3. Dari Pengukuran Menuju Distribusi

Kesalahan umum dalam membaca hasil trading adalah terlalu terpaku pada satu angka.

Misalnya:

- rata-rata return sebesar 0,8%;
- win rate sebesar 65%;
- expectancy sebesar 0,2R;
- profit terbesar sebesar 5%;
- atau jumlah trade yang menghasilkan profit lebih banyak daripada trade yang rugi.

Angka-angka tersebut dapat berguna, tetapi tidak cukup untuk menggambarkan keseluruhan perilaku hasil.

Dua strategi dapat memiliki rata-rata return yang sama, tetapi karakter risikonya sangat berbeda. Strategi pertama mungkin menghasilkan keuntungan kecil secara konsisten. Strategi kedua mungkin mengalami banyak kerugian kecil lalu sesekali memperoleh keuntungan besar. Keduanya memiliki rata-rata serupa, tetapi pengalaman dan risikonya tidak sama.

Karena itu, TEKB tidak berhenti pada rata-rata. TEKB berusaha memahami **distribusi**.

Distribusi membantu menjawab pertanyaan:

- Seberapa sering hasil positif terjadi?
- Seberapa besar hasil yang umum terjadi?
- Seberapa jauh hasil menyebar?
- Seberapa besar kerugian yang buruk?
- Apakah terdapat ekor kerugian yang panjang?
- Apakah keuntungan hanya berasal dari beberapa event ekstrem?
- Apakah median jauh berbeda dari mean?
- Apakah hasil B1 lebih baik secara konsisten atau hanya karena beberapa outlier?

### Mean bukan keseluruhan cerita

Rata-rata dapat dipengaruhi oleh sejumlah kecil hasil ekstrem. Misalnya, sembilan event menghasilkan sekitar 0%, tetapi satu event menghasilkan +20%. Rata-ratanya dapat terlihat positif, padahal sebagian besar event tidak memberikan hasil berarti.

Karena itu, median, persentil, proporsi hasil positif, serta ukuran ekor distribusi perlu dibaca bersama.

### MAE dan MFE memperlihatkan perjalanan hasil

Return akhir hanya menunjukkan posisi hasil pada titik evaluasi. Ia tidak selalu memperlihatkan apa yang terjadi selama perjalanan.

MAE membantu melihat seberapa jauh harga bergerak melawan posisi. MFE membantu melihat seberapa jauh harga sempat bergerak mendukung posisi.

Dua event dapat memiliki return akhir yang sama, tetapi satu event mungkin mengalami drawdown intratrade yang sangat besar, sedangkan event lainnya bergerak relatif mulus.

Dengan mengubah MAE dan MFE ke dalam satuan ×ATR, perbandingan antarperiode dan antar-instrumen dapat menjadi lebih masuk akal karena ukuran gerakan disesuaikan dengan volatilitas.

### Ketidakpastian juga harus diukur

Distribusi hasil historis bukanlah kepastian masa depan. Distribusi itu sendiri memiliki ketidakpastian.

Jika penelitian hanya memiliki sedikit event, hasilnya mungkin sangat mudah berubah apabila beberapa event dihilangkan. Jika event saling berdekatan atau berasal dari tanggal yang sama, jumlah event yang besar belum tentu berarti jumlah informasi independen juga besar.

Karena itu, TEKB menggunakan pendekatan seperti bootstrap, termasuk date-cluster bootstrap atau moving block bootstrap sesuai kebutuhan. Tujuannya bukan membuat hasil tampak lebih ilmiah, tetapi memperkirakan seberapa stabil kesimpulan ketika data yang saling bergantung diperlakukan secara lebih realistis.

Dengan demikian, TEKB bergerak dari pertanyaan:

> "Berapa rata-rata hasilnya?"

menuju pertanyaan yang lebih lengkap:

> "Seperti apa seluruh distribusi hasilnya, seberapa besar risikonya, dan seberapa yakin kita terhadap estimasi tersebut?"

---

## 25.4. Dari Distribusi Menuju Pengujian

Melihat distribusi belum otomatis membuktikan bahwa suatu hipotesis memiliki edge.

Distribusi dapat terlihat menarik secara kebetulan. Perbedaan antara B1 dan B0 dapat muncul karena variasi sampel. Hasil positif juga dapat ditemukan karena peneliti mencoba terlalu banyak variasi aturan, horizon, instrumen, atau parameter.

Karena itu, TEKB membutuhkan lapisan pengujian yang menjaga agar kesimpulan tidak terlalu mudah dibentuk oleh kebetulan.

### Bootstrap

Bootstrap membantu mengukur ketidakpastian estimasi dengan membentuk banyak sampel ulang dari data penelitian, menggunakan metode yang sesuai dengan struktur ketergantungan event.

Dalam konteks TEKB, bootstrap dapat membantu memperkirakan rentang kemungkinan nilai perbedaan B1 dan B0, seperti Δ expectancy atau perbedaan ukuran hasil lainnya.

Bootstrap tidak menjamin bahwa hipotesis benar. Bootstrap hanya membantu menjawab:

> "Jika struktur data yang kita amati menjadi dasar pengambilan sampel ulang, seberapa stabil estimasi ini?"

### Multiple testing

Semakin banyak hipotesis atau kandidat yang dicoba, semakin besar peluang menemukan hasil positif hanya karena kebetulan.

Misalnya, peneliti mencoba banyak:

- threshold volume;
- horizon;
- stop-loss;
- take-profit;
- kelompok saham;
- definisi event;
- kombinasi filter;
- atau variasi periode.

Jika hanya hasil terbaik yang ditampilkan, pembaca dapat mengira hasil itu merupakan satu-satunya pengujian yang dilakukan. Padahal, hasil tersebut mungkin merupakan pemenang dari banyak percobaan.

TEKB harus memperhitungkan kenyataan bahwa banyak pengujian telah dilakukan. Inilah fungsi pencatatan multiple-testing family, research batch, attempt number, dan riwayat keluarga pengujian sebelumnya.

### BH-FDR

Benjamini–Hochberg False Discovery Rate atau BH-FDR digunakan untuk mengendalikan proporsi temuan positif yang berpotensi merupakan false discovery dalam suatu keluarga pengujian.

Dalam TEKB, keluarga pengujian harus didefinisikan secara jelas. Misalnya, pengujian worst-case dan best-case tidak boleh dicampur secara sembarangan jika keduanya mewakili pertanyaan statistik yang berbeda.

BH-FDR bukan alat untuk membuat semua hasil menjadi benar. Ia adalah mekanisme pengendalian agar proses seleksi tidak terlalu mudah menghasilkan klaim positif palsu.

### IS Selection

IS Selection adalah tahap ketika kandidat diuji dan dipilih menggunakan data in-sample sesuai aturan yang telah ditentukan.

Pemilihan tidak boleh hanya berdasarkan kandidat dengan profit terbesar. Kandidat harus memenuhi kriteria yang relevan, misalnya:

- perbedaan terhadap B0 berada pada arah yang diharapkan;
- hasil positif secara statistik;
- memiliki ketahanan pada skenario worst-case dan/atau best-case sesuai kontrak;
- lolos pengendalian multiple testing;
- memenuhi batas minimum event dan cakupan;
- serta tidak melanggar aturan metodologi.

Jika tidak ada kandidat yang memenuhi syarat, hasil yang benar adalah:
NO_EDGE_FOUND

Bukan memilih kandidat yang "paling lumayan" hanya karena penelitian harus menghasilkan sesuatu.

### Freeze

Setelah kandidat dipilih, aturan dan kandidat harus dibekukan sebelum OOS.

Freeze berarti mengunci:

- definisi event;
- definisi entry;
- aturan B0;
- definisi MAE/MFE;
- ATR;
- Evaluation Engine;
- candidate grid;
- kriteria seleksi;
- keluarga multiple testing;
- serta identitas versi dan provenance.

Freeze mencegah peneliti mengubah aturan setelah melihat hasil OOS.

Tanpa freeze, OOS dapat berubah menjadi perpanjangan IS: hasil yang tidak disukai diperbaiki, parameter diganti, lalu diuji kembali sampai terlihat bagus.

### OOS

Out-of-sample atau OOS adalah pengujian terhadap data yang tidak digunakan untuk membangun atau memilih kandidat.

OOS bukan tempat untuk mencari kandidat baru. OOS adalah ujian terhadap keputusan yang telah dibekukan.

Jika kandidat yang lolos IS gagal pada OOS, kegagalan itu harus diterima sebagai informasi. Status seperti OOS_REJECTED, OOS_SPENT, atau OOS_TAINTED bukan aib. Status tersebut justru menunjukkan bahwa penelitian memiliki mekanisme untuk membedakan antara hasil yang dipilih dan hasil yang benar-benar bertahan di luar data pembentukan.

Rangkaian ini memperlihatkan bahwa TEKB tidak hanya bertanya apakah hasil terlihat bagus. TEKB juga bertanya apakah proses yang menghasilkan kesimpulan tersebut cukup disiplin untuk dipercaya.

---

## 25.5. Dari Hasil Menuju Keputusan yang Lebih Bertanggung Jawab

Tujuan akhir penelitian bukan mengumpulkan sebanyak mungkin sinyal positif. Tujuannya adalah membantu manusia mengambil keputusan dengan pemahaman yang lebih baik tentang bukti dan ketidakpastian.

Karena itu, hasil penelitian harus diterjemahkan secara hati-hati.

### Tidak semua sinyal layak digunakan

Sebuah pola dapat menarik secara visual, tetapi tidak cukup kuat secara empiris.

Sebuah event dapat menghasilkan beberapa trade yang menguntungkan, tetapi tidak memiliki keunggulan yang konsisten ketika dibandingkan dengan B0.

Sebuah sinyal dapat memiliki rata-rata positif, tetapi distribusinya terlalu lebar, biaya terlalu tinggi, atau risiko ekornya terlalu berat.

Maka, keberadaan sinyal tidak otomatis berarti sinyal tersebut layak digunakan dalam keputusan trading.

### Tidak semua hasil positif adalah edge

Hasil positif dapat muncul karena:

- kondisi pasar umum;
- variasi sampel;
- outlier;
- pemilihan kandidat setelah melihat hasil;
- ketidakadilan B0;
- kebocoran informasi masa depan;
- definisi entry yang tidak realistis;
- biaya yang diabaikan;
- atau terlalu banyak percobaan.

Edge bukan sekadar hasil positif. Edge adalah klaim yang didukung oleh perbedaan yang relevan terhadap pembanding, pengukuran yang konsisten, ketidakpastian yang dipahami, pengendalian pengujian, serta bukti generalisasi yang memadai.

### Tidak semua edge historis akan bertahan

Bahkan ketika suatu kandidat lolos pengujian dan OOS, tidak ada jaminan bahwa pola tersebut akan terus bekerja selamanya.

Pasar berubah. Struktur peserta berubah. Likuiditas berubah. Biaya transaksi berubah. Regulasi, teknologi, perilaku pelaku pasar, dan kondisi makroekonomi dapat berubah.

Hasil historis adalah bukti tentang kondisi dan periode tertentu. Ia bukan kontrak yang menjamin masa depan.

Karena itu, bahasa keputusan harus proporsional terhadap bukti. TEKB sebaiknya tidak mengatakan:

> "Sinyal ini pasti menghasilkan profit."

Bahasa yang lebih bertanggung jawab adalah:

> "Dalam data dan aturan yang diuji, kondisi ini menunjukkan perbedaan hasil terhadap B0 pada tingkat ketidakpastian tertentu, tetapi keberlanjutan edge di masa depan belum dapat dipastikan."

### Keputusan harus mengikuti bukti

Salah satu bahaya terbesar dalam trading adalah keputusan dibuat terlebih dahulu, kemudian bukti dicari untuk membenarkannya.

TEKB membalik urutan tersebut:

> Data → Pengukuran → Perbandingan → Pengujian → Kesimpulan → Keputusan.

Urutan ini tidak membuat keputusan menjadi bebas risiko. Namun, urutan ini membantu mengurangi keputusan yang lahir dari antusiasme, ketakutan, FOMO, atau keyakinan yang belum diuji.

TEKB juga tidak memaksa manusia untuk selalu melakukan trading. Dalam banyak situasi, hasil penelitian yang paling bertanggung jawab dapat berupa:

- menunggu;
- mengurangi ukuran posisi;
- menghindari kondisi tertentu;
- meminta data tambahan;
- melakukan penelitian lanjutan;
- atau tidak menggunakan sinyal sama sekali.

Keputusan untuk tidak bertindak dapat menjadi keputusan yang rasional apabila bukti belum cukup.

---

## 25.6. Kalimat Penutup

TEKB dibangun dari kesadaran bahwa pasar penuh dengan pola, tetapi tidak setiap pola mengandung informasi yang dapat diandalkan. Banyak kesimpulan terlihat meyakinkan hanya karena kita melihatnya setelah kejadian berlangsung. Banyak strategi terlihat hebat karena pembandingnya tidak adil, biayanya diabaikan, atau aturan dipilih setelah hasil diketahui.

TEKB berusaha menghadapi masalah tersebut bukan dengan menjanjikan kepastian, melainkan dengan membangun proses yang lebih sulit dimanipulasi oleh harapan peneliti sendiri.

TEKB mengajarkan kita untuk:

1. mengubah sinyal menjadi pertanyaan;
2. mengubah pertanyaan menjadi hipotesis;
3. mengubah hipotesis menjadi event yang terdefinisi;
4. mengubah event menjadi pengukuran;
5. mengubah pengukuran menjadi distribusi;
6. mengubah distribusi menjadi pengujian;
7. mengubah hasil pengujian menjadi kesimpulan yang terbatas;
8. lalu mengubah kesimpulan menjadi keputusan yang bertanggung jawab.

Pada akhirnya, keberhasilan TEKB bukan diukur dari seberapa sering ia menghasilkan kata "BUY". Keberhasilannya diukur dari seberapa baik ia membantu kita membedakan antara:

- pola dan bukti;
- kebetulan dan informasi;
- hasil positif dan edge;
- optimisme dan ketidakpastian;
- penelitian dan promosi;
- serta keyakinan pribadi dan kesimpulan yang dapat dipertanggungjawabkan.

> TEKB tidak dibangun untuk membuat kita selalu benar.
>
> TEKB dibangun agar kita lebih sulit tertipu oleh kesimpulan yang belum terbukti.

Inilah inti filosofi TEKB:

> **Bukti dulu, keputusan belakangan.**

Bukan karena bukti dapat menghapus semua risiko, melainkan karena keputusan yang tidak didahului bukti akan lebih mudah dikuasai oleh ilusi, emosi, dan kebetulan.

Dan ketika penelitian akhirnya menghasilkan:
NO_EDGE_FOUND


kita tidak sedang mengalami kegagalan.

Kita sedang memperoleh pengetahuan yang penting: bahwa berdasarkan data, aturan, pembanding, dan pengujian yang telah dilakukan, belum ada bukti yang cukup untuk menyatakan adanya keunggulan yang dapat dipercaya.

Itu adalah bentuk kedewasaan ilmiah.

Sebab dalam penelitian yang jujur, tidak menemukan edge lebih baik daripada menemukan edge palsu.

---

## Ringkasan Bab

- TEKB pada akhirnya adalah **cara berpikir**, bukan sekadar sistem penelitian.
- Sinyal harus diubah menjadi **pertanyaan yang dapat diuji**.
- Hipotesis harus diterjemahkan menjadi **struktur pengukuran**: Event → Entry → Horizon → Outcome → B0 → Perbandingan.
- Hasil harus dibaca sebagai **distribusi**, bukan satu angka.
- Distribusi harus diuji dengan **bootstrap**, **multiple testing**, **IS Selection**, **Freeze**, dan **OOS**.
- Hasil harus diterjemahkan menjadi **keputusan yang proporsional** terhadap bukti.
- **NO_EDGE_FOUND** adalah hasil yang sah, bukan kegagalan.
- **Bukti dulu, keputusan belakangan** adalah inti filosofi TEKB.

---

## Pertanyaan Refleksi

1. Apa yang dimaksud dengan TEKB sebagai disiplin berpikir?
2. Mengapa sinyal harus diubah menjadi pertanyaan yang dapat diuji?
3. Mengapa hipotesis harus diterjemahkan menjadi struktur pengukuran yang jelas?
4. Mengapa distribusi lebih penting daripada satu angka?
5. Mengapa bootstrap dan multiple testing diperlukan?
6. Mengapa freeze penting sebelum OOS?
7. Mengapa hasil positif belum tentu merupakan edge?
8. Mengapa NO_EDGE_FOUND adalah hasil yang sah?
9. Apa arti "Bukti dulu, keputusan belakangan"?
10. Mengapa keputusan untuk tidak bertindak dapat menjadi keputusan yang rasional?

---

## Kalimat Kunci

> TEKB tidak dibangun untuk membuat kita selalu benar. TEKB dibangun agar kita lebih sulit tertipu oleh kesimpulan yang belum terbukti. Dalam penelitian yang jujur, tidak menemukan edge lebih baik daripada menemukan edge palsu.

---

<div align="center">

[← Bab Sebelumnya](/posts/bab-24-batasan-tekb/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Lampiran A →](/posts/lampiran-a-glosarium/)

</div>