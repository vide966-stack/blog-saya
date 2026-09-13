---
title: "BAB 11 — Mengapa TEKB Menggunakan Satuan ×ATR?"
published: 2026-09-12
description: "Satuan ×ATR membantu mengukur pergerakan harga secara lebih adil dibandingkan rupiah atau persentase. Bab ini menjelaskan cara normalisasi MAE/MFE dan batasannya."
tags: ["bab-11", "atr", "normalisasi", "xatr"]
category: "Bab"
draft: false
lang: ""
---

**BAGIAN III — MENGUKUR HASIL TANPA MENIPU DIRI SENDIRI**

---

Pada bab sebelumnya, kita telah membahas ATR sebagai pengukur volatilitas. ATR membantu kita mengetahui seberapa besar harga biasanya bergerak dalam konteks instrumen dan periode tertentu.

Namun, muncul pertanyaan lanjutan: Mengapa hasil penelitian TEKB tidak hanya dinyatakan dalam rupiah atau persentase, tetapi juga dalam satuan ×ATR?

Jawabannya berkaitan dengan kebutuhan untuk membandingkan pergerakan harga secara lebih adil.

Dalam penelitian trading, kita mungkin membandingkan:

- beberapa saham dengan harga yang berbeda;
- beberapa instrumen dengan volatilitas yang berbeda;
- event yang terjadi pada periode pasar tenang;
- event yang terjadi pada periode pasar sangat aktif;
- atau hasil MAE dan MFE dari banyak instrumen.

Jika seluruh hasil hanya dinyatakan dalam rupiah, perbandingan dapat menyesatkan. Jika hanya menggunakan persentase, sebagian konteks pergerakan harga juga dapat hilang.

Satuan ×ATR membantu mengubah jarak harga menjadi ukuran relatif terhadap volatilitas yang tersedia sebelum entry.

Prinsip bab ini adalah:

> ×ATR bukan alat untuk menciptakan keuntungan, melainkan cara untuk mengukur besar pergerakan secara lebih sebanding.

---

## 11.1. Masalah Satuan Rupiah dan Persentase

Harga saham dan karakteristik pergerakannya tidak sama. Karena itu, angka mentah sering kali sulit digunakan untuk perbandingan lintas instrumen atau lintas kondisi pasar.

### Harga Saham Berbeda

Bayangkan dua saham:

- Saham A memiliki harga Rp1.000.
- Saham B memiliki harga Rp10.000.

Keduanya mengalami kenaikan Rp100.

Jika hanya melihat nilai rupiah, pergerakannya sama. Namun, secara persentase:

- Saham A naik 10%.
- Saham B naik 1%.

Pergerakan Rp100 memiliki arti yang sangat berbeda bagi kedua saham tersebut.

Sebaliknya, jika kita hanya menggunakan persentase, kita mungkin kehilangan informasi tentang jarak harga aktual yang penting untuk memahami entry, stop-loss, target, dan perjalanan intrabar.

### Volatilitas Saham Berbeda

Sekarang bayangkan dua saham memiliki harga yang sama, yaitu Rp5.000.

- Saham A biasanya bergerak sekitar Rp50 dalam satu periode.
- Saham B biasanya bergerak sekitar Rp300 dalam satu periode.

Keduanya sama-sama mengalami MAE sebesar Rp100.

Namun:

- Pada Saham A, MAE Rp100 mungkin merupakan gerakan yang sangat besar.
- Pada Saham B, MAE Rp100 mungkin merupakan gerakan yang relatif kecil.

Angka mentah yang sama dapat memiliki makna risiko yang berbeda karena volatilitasnya berbeda.

### Kondisi Pasar Juga Berubah

Saham yang sama pun tidak selalu memiliki karakteristik pergerakan yang sama sepanjang waktu.

Pada periode tenang:

- harga mungkin bergerak dalam rentang sempit;
- gap cenderung lebih kecil;
- dan fluktuasi intrabar relatif terbatas.

Pada periode volatil:

- rentang harga dapat melebar;
- gap dapat lebih besar;
- dan pergerakan berlawanan arah dapat terjadi lebih cepat.

Jika MAE sebesar Rp100 terjadi pada periode tenang dan periode volatil, kita tidak dapat langsung menyimpulkan bahwa kedua kejadian memiliki tingkat tekanan yang sama.

### Angka Mentah Sulit Dibandingkan Secara Adil

Perbandingan berbasis rupiah atau persentase memiliki kegunaan masing-masing, tetapi keduanya tidak selalu cukup untuk menjawab pertanyaan penelitian.

Contohnya, peneliti ingin mengetahui:

> "Seberapa jauh harga biasanya bergerak melawan posisi sebelum akhirnya mencapai target?"

Jika hanya memakai rupiah, hasil dapat dipengaruhi oleh harga nominal saham. Jika hanya memakai persentase, hasil dapat kurang menggambarkan skala pergerakan dalam satuan harga yang digunakan oleh aturan entry dan evaluasi.

Karena itu, TEKB menggunakan ATR sebagai dasar normalisasi. Jarak harga dapat dinyatakan relatif terhadap ukuran volatilitas yang tersedia sebelum entry.

---

## 11.2. Apa Arti "1 ATR"?

Ketika kita menyebut suatu jarak sebesar 1 ATR, kita sedang menggunakan ATR sebagai satuan jarak.

Misalnya:

- harga entry = Rp5.000;
- ATR_entry = Rp100.

Maka:

- 0,5 ATR = Rp50;
- 1 ATR = Rp100;
- 1,5 ATR = Rp150;
- 2 ATR = Rp200.

Dalam contoh tersebut, ATR berfungsi seperti penggaris yang panjang satu unitnya adalah Rp100.

Namun, angka ATR berbeda untuk setiap event. Jika event lain memiliki ATR_entry sebesar Rp200, maka:

- 1 ATR = Rp200;
- 2 ATR = Rp400.

Jadi, "1 ATR" bukan angka rupiah yang selalu sama. Nilainya mengikuti ATR_entry pada event tersebut.

### Contoh Stop-Loss 1 ATR

Misalnya:

- entry = Rp5.000;
- ATR_entry = Rp100;
- candidate SL = 1 ATR.

Untuk posisi long, jarak stop-loss adalah:

> Rp5.000 − Rp100 = Rp4.900.

Stop-loss tersebut berjarak 1 ATR dari entry.

Pada event lain:

- entry = Rp8.000;
- ATR_entry = Rp250;
- candidate SL = 1 ATR.

Maka:

> Rp8.000 − Rp250 = Rp7.750.

Keduanya menggunakan aturan 1 ATR, tetapi jarak rupiahnya berbeda.

Yang sama adalah skala relatif terhadap volatilitas masing-masing event, bukan jumlah rupiahnya.

### Contoh Take-Profit 2 ATR

Misalnya:

- entry = Rp5.000;
- ATR_entry = Rp100;
- candidate TP = 2 ATR.

Untuk posisi long:

> Rp5.000 + (2 × Rp100) = Rp5.200.

Target berada 2 ATR di atas entry.

Jika ATR_entry = Rp250, maka target 2 ATR dari entry Rp5.000 menjadi:

> Rp5.000 + (2 × Rp250) = Rp5.500.

Dengan demikian, aturan yang sama dapat diterapkan pada event dengan skala volatilitas berbeda.

### Mengapa 1 ATR Tidak Berarti Risiko Pasti Sama dalam Rupiah?

Penting untuk membedakan jarak harga dengan risiko uang.

Jika dua posisi sama-sama menggunakan stop-loss 1 ATR, jaraknya mungkin berbeda:

- Posisi A: ATR = Rp100.
- Posisi B: ATR = Rp300.

Selain itu, risiko uang juga bergantung pada:

- jumlah saham atau ukuran posisi;
- harga entry;
- biaya transaksi;
- slippage;
- gap;
- dan apakah stop-loss benar-benar dapat dieksekusi pada harga yang ditentukan.

Karena itu, 1 ATR tidak berarti:

- kerugian pasti sama dalam rupiah;
- risiko portofolio pasti sama;
- kerugian maksimum pasti terbatas pada 1 ATR;
- atau eksekusi pasti terjadi tepat pada level stop-loss.

×ATR adalah satuan jarak dan skala volatilitas, bukan satuan uang dan bukan jaminan risiko aktual.

---

## 11.3. MAE/MFE dalam Unit ATR

Dalam TEKB, MAE dan MFE digunakan untuk mengukur perjalanan harga setelah entry.

- MAE (Maximum Adverse Excursion) mengukur gerakan terburuk yang berlawanan dengan posisi.
- MFE (Maximum Favorable Excursion) mengukur gerakan terbaik yang mendukung posisi.

MAE dan MFE awalnya dapat dihitung dalam satuan harga mentah. Misalnya:

- MAE = Rp80;
- MFE = Rp180.

Namun, agar hasil lebih mudah dibandingkan dengan event lain, nilai tersebut dapat dinormalisasi menggunakan ATR_entry.

### Mengubah Gerakan Harga Menjadi Ukuran Relatif

Untuk posisi long, secara sederhana:

> MAE_×ATR = MAE_harga ÷ ATR_entry

> MFE_×ATR = MFE_harga ÷ ATR_entry

Contoh:

- ATR_entry = Rp100;
- MAE = Rp50;
- MFE = Rp200.

Maka:

- MAE = 0,5 × ATR;
- MFE = 2,0 × ATR.

Artinya, selama horizon pengukuran, harga sempat bergerak melawan posisi sejauh setengah ukuran ATR_entry dan sempat bergerak mendukung posisi sejauh dua kali ukuran ATR_entry.

Angka ini memberikan gambaran yang lebih kontekstual daripada hanya menyebut Rp50 dan Rp200.

### Contoh Perbandingan Dua Event

Misalnya terdapat dua event:

| Komponen | Event A | Event B |
|---|---|---|
| ATR_entry | Rp100 | Rp400 |
| MAE mentah | Rp50 | Rp100 |
| MFE mentah | Rp200 | Rp400 |
| MAE ×ATR | 0,5 | 0,25 |
| MFE ×ATR | 2,0 | 1,0 |

Jika hanya melihat MAE mentah, Event B tampak lebih buruk karena Rp100 lebih besar daripada Rp50.

Namun, setelah dinormalisasi:

- Event A mengalami MAE sebesar 0,5 ATR.
- Event B mengalami MAE sebesar 0,25 ATR.

Dalam konteks volatilitas masing-masing, tekanan relatif Event A justru lebih besar.

Hal yang sama berlaku untuk MFE:

- Event A mencapai 2 ATR.
- Event B mencapai 1 ATR.

Meskipun Event B menghasilkan gerakan rupiah lebih besar, gerakan tersebut lebih kecil relatif terhadap volatilitasnya.

### Kegunaan untuk Penelitian Lintas Instrumen

ATR-normalization berguna ketika peneliti ingin membandingkan:

- saham berharga rendah dan tinggi;
- saham volatil dan stabil;
- periode pasar tenang dan aktif;
- instrumen dengan skala harga berbeda;
- atau event yang terjadi pada kondisi volatilitas berbeda.

Dengan menyatakan hasil dalam ×ATR, peneliti dapat bertanya:

- Seberapa besar gerakan relatif terhadap volatilitas saat entry?
- Apakah event tertentu cenderung menghasilkan MFE yang lebih besar dari ukuran gerak normalnya?
- Apakah MAE yang dialami event tertentu relatif kecil atau besar?
- Apakah candidate SL/TP memiliki jarak yang masuk akal dibandingkan gerakan historis?

Namun, ATR-normalization tidak menghapus seluruh perbedaan antar-instrumen. Ia hanya membantu membuat satu aspek perbandingan menjadi lebih sebanding.

### Perbedaan MAE/MFE Mentah dan ATR-Normalized

MAE/MFE mentah menjawab:

> "Berapa rupiah harga bergerak?"

MAE/MFE dalam ×ATR menjawab:

> "Berapa kali ukuran volatilitas saat entry harga bergerak?"

Keduanya memiliki fungsi berbeda.

MAE/MFE mentah berguna untuk:

- melihat pergerakan harga aktual;
- memeriksa kemungkinan level harga;
- memahami dampak nominal;
- dan melakukan audit terhadap data.

MAE/MFE ×ATR berguna untuk:

- membandingkan skala gerakan;
- mengurangi pengaruh perbedaan harga nominal;
- memahami gerakan relatif terhadap volatilitas;
- dan menyusun candidate SL/TP dalam unit yang konsisten.

TEKB tidak perlu memilih salah satu dan membuang yang lain. Keduanya dapat disimpan dan digunakan untuk tujuan yang berbeda.

---

## 11.4. Batasan ATR-Normalization

ATR-normalization membantu pengukuran, tetapi tidak boleh dianggap sebagai solusi untuk semua masalah penelitian.

Normalisasi adalah transformasi satuan. Ia tidak otomatis meningkatkan kualitas sinyal atau membuktikan bahwa suatu event memiliki information edge.

### Normalisasi Tidak Menciptakan Edge

Misalnya, hasil B1 dan B0 tidak menunjukkan perbedaan yang berarti ketika diukur dalam rupiah. Peneliti kemudian mengubahnya menjadi ×ATR dan menemukan angka yang terlihat lebih menarik.

Perubahan satuan tidak otomatis menciptakan informasi baru.

Jika tidak ada perbedaan yang valid dalam data, mengubah satuan tidak boleh digunakan untuk mengklaim bahwa edge telah ditemukan.

Normalisasi dapat membuat pola lebih mudah dilihat, tetapi tidak dapat menggantikan pembanding B0, pengujian ketidakpastian, atau validasi OOS.

### ATR Tidak Membuktikan Arah

ATR hanya mengukur skala volatilitas. ATR tidak mengatakan:

- harga akan naik;
- harga akan turun;
- event tertentu bullish;
- event tertentu bearish;
- atau target akan tercapai.

Jika hasil MFE ×ATR besar, hal itu hanya berarti harga sempat bergerak mendukung posisi dalam ukuran relatif yang besar. Arah dan makna event tetap harus ditentukan melalui definisi return, kondisi penelitian, serta perbandingan B1 dan B0.

### ATR Hanya Membantu Pengukuran Menjadi Lebih Sebanding

ATR-normalization membantu menjawab pertanyaan pengukuran:

> "Seberapa besar gerakan ini dibandingkan dengan volatilitas yang tersedia sebelum entry?"

Ia tidak menjawab seluruh pertanyaan penelitian, seperti:

- apakah event memiliki information edge;
- apakah hasilnya stabil;
- apakah hasilnya signifikan secara praktis;
- apakah hasilnya bertahan pada OOS;
- atau apakah hasil tersebut dapat diperdagangkan setelah friction.

Dengan kata lain, ATR-normalization adalah salah satu lapisan pengukuran, bukan keseluruhan metode penelitian.

### Normalisasi Bukan Jaminan Distribusi Menjadi Identik

Walaupun MAE dan MFE telah dinyatakan dalam ×ATR, distribusi hasil antar-instrumen atau antarperiode belum tentu menjadi sama.

Perbedaan tetap dapat muncul karena:

- struktur pasar;
- likuiditas;
- spread;
- gap;
- batas harga;
- karakteristik sesi perdagangan;
- perubahan rezim volatilitas;
- kualitas data;
- dan mekanisme pembentukan harga.

ATR hanya menormalkan terhadap satu ukuran volatilitas. Ia tidak menghapus seluruh sumber perbedaan.

Misalnya, dua instrumen sama-sama memiliki MFE median 1 ATR. Itu tidak berarti keduanya memiliki:

- distribusi yang identik;
- tail risk yang sama;
- peluang gap yang sama;
- biaya transaksi yang sama;
- atau risiko eksekusi yang sama.

Karena itu, hasil ATR-normalized tetap perlu dibaca bersama distribusi lengkap, ukuran sampel, pembanding, dan batasan penelitian.

---

## 11.5. Kapan Event Boleh Masuk Distribusi ATR-Normalized?

Tidak semua event yang ditemukan otomatis boleh dimasukkan ke dalam distribusi MAE/MFE dalam ×ATR.

Agar suatu event dapat masuk ke distribusi ATR-normalized, komponen yang dibutuhkan harus tersedia dan valid.

### MAE/MFE Harus Lengkap

Jika penelitian menetapkan horizon tertentu, misalnya R1, R3, R5, atau R10, maka event harus memiliki data yang cukup untuk menghitung MAE/MFE sesuai horizon tersebut.

Jika horizon belum lengkap karena data berhenti terlalu cepat, event tidak boleh diperlakukan sebagai event dengan MAE/MFE lengkap.

Contohnya:

- event membutuhkan horizon 10 bar;
- data hanya tersedia sampai 4 bar setelah entry;
- MAE/MFE untuk horizon 10 bar belum dapat dihitung secara penuh.

Event tersebut harus memiliki status yang sesuai, misalnya:

> INSUFFICIENT_HORIZON

Event tidak boleh dimasukkan ke distribusi penuh seolah-olah seluruh horizon telah diamati.

### ATR Harus Tersedia

ATR_entry harus tersedia pada waktu yang benar, yaitu berdasarkan informasi sebelum entry sesuai definisi penelitian.

Jika ATR_entry tidak dapat dihitung karena:

- data historis tidak cukup;
- bar sebelumnya tidak tersedia;
- terdapat data invalid;
- atau definisi ATR tidak dapat diterapkan,

maka event tidak memiliki denominasi yang sah untuk normalisasi ×ATR.

Dalam keadaan tersebut, peneliti tidak boleh menghitung MAE/MFE ×ATR dengan nilai pengganti yang tidak ditentukan dalam kontrak penelitian.

### Event Invalid Tidak Boleh Masuk

Event dengan masalah validitas tidak boleh dimasukkan ke dalam distribusi seolah-olah hasilnya sah.

Contoh masalah validitas:

- harga entry tidak tersedia;
- ATR_entry invalid atau nol;
- data High/Low tidak valid;
- timestamp tidak konsisten;
- horizon tidak sesuai;
- bar mengalami kerusakan;
- atau terdapat pelanggaran aturan no-look-ahead.

Event tersebut harus diberi status invalid yang jelas dan dipisahkan dari event yang valid.

### Status Kelayakan Harus Terpisah dari Status MAE/MFE

Penting untuk membedakan dua hal:

1. Apakah MAE/MFE berhasil dihitung?
2. Apakah event layak dimasukkan ke distribusi ATR-normalized?

Keduanya tidak selalu sama.

Misalnya, MAE/MFE mentah mungkin berhasil dihitung, tetapi ATR_entry tidak tersedia. Dalam situasi ini:

- MAE/MFE mentah dapat memiliki status COMPUTED;
- tetapi kelayakan ATR-normalized harus berstatus NOT_ELIGIBLE atau INVALID_ATR_DENOMINATOR.

Sebaliknya, ATR_entry mungkin tersedia, tetapi horizon MAE/MFE belum lengkap. Maka:

- ATR_entry valid;
- tetapi event belum layak masuk distribusi untuk horizon tersebut.

Pemisahan status membantu mencegah kesalahan ketika data diproses secara otomatis.

### Mengapa Denominasi yang Tidak Tersedia Tidak Boleh Diganti Sembarangan?

Normalisasi membutuhkan pembagi atau denominasi. Dalam kasus ini, denominasi tersebut adalah ATR_entry.

Jika ATR_entry tidak tersedia, peneliti mungkin tergoda untuk menggantinya dengan:

- ATR setelah entry;
- ATR rata-rata dari event lain;
- ATR instrumen pada hari berikutnya;
- ATR periode berbeda;
- nilai median ATR;
- atau angka default yang dibuat agar perhitungan tetap berjalan.

Tindakan tersebut dapat merusak makna hasil.

Misalnya, MAE mentah sebesar Rp100 dibagi dengan ATR yang sebenarnya tidak tersedia. Jika peneliti menggunakan ATR hari berikutnya, ia telah memasukkan informasi yang mungkin belum tersedia saat entry. Ini dapat menciptakan look-ahead bias.

Jika peneliti menggunakan ATR median seluruh sampel, satuan tersebut tidak lagi merepresentasikan volatilitas event saat entry.

Karena itu:

> Jika denominasi yang dipersyaratkan tidak tersedia atau tidak valid, event tidak boleh dipaksakan masuk ke distribusi ATR-normalized.

Lebih baik event dikeluarkan dari distribusi tertentu dengan alasan yang terdokumentasi daripada menghasilkan angka yang tampak lengkap tetapi tidak sah.

### Contoh Status Kelayakan

Berikut contoh pemisahan status:

| Kondisi Event | MAE/MFE Mentah | ATR_entry | Kelayakan ×ATR |
|---|---|---|---|
| Horizon lengkap, ATR valid | COMPUTED | VALID | ELIGIBLE |
| Horizon belum lengkap | INSUFFICIENT_HORIZON | VALID | NOT_ELIGIBLE |
| Horizon lengkap, ATR tidak tersedia | COMPUTED | INVALID/MISSING | NOT_ELIGIBLE |
| Data harga invalid | INVALIDATED | VALID atau tidak | NOT_ELIGIBLE |
| ATR nol atau tidak masuk akal | COMPUTED atau INVALIDATED | INVALID | NOT_ELIGIBLE |
| Semua komponen valid | COMPUTED_FULL_HORIZON | VALID | ELIGIBLE |

Status tersebut dapat disesuaikan dengan skema resmi TEKB, tetapi prinsip pemisahannya harus dipertahankan.

---

## Ringkasan Bab

- Harga mentah sulit dibandingkan karena harga nominal dan volatilitas setiap instrumen berbeda.
- Persentase membantu memahami perubahan relatif terhadap harga, tetapi tidak selalu cukup untuk mengukur jarak pergerakan dalam konteks volatilitas.
- 1 ATR adalah satuan jarak yang nilainya mengikuti ATR_entry pada event tertentu.
- Stop-loss 1 ATR dan target 2 ATR memiliki jarak rupiah yang berbeda ketika ATR setiap event berbeda.
- 1 ATR bukan berarti risiko uang pasti sama, karena risiko juga bergantung pada ukuran posisi, biaya, slippage, gap, dan eksekusi.
- MAE/MFE ×ATR mengubah pergerakan harga menjadi ukuran relatif terhadap volatilitas sebelum entry.
- ATR-normalization berguna untuk membandingkan skala gerakan lintas instrumen dan kondisi pasar.
- Normalisasi tidak menciptakan edge, tidak membuktikan arah, dan tidak menjamin distribusi antar-instrumen menjadi identik.
- Event hanya boleh masuk distribusi ATR-normalized jika MAE/MFE yang dibutuhkan lengkap, ATR_entry tersedia dan valid, serta event tidak invalid.
- Status kelayakan distribusi harus dipisahkan dari status keberhasilan penghitungan MAE/MFE.
- Denominasi yang tidak tersedia tidak boleh diganti sembarangan karena dapat mengubah makna hasil atau memasukkan informasi masa depan.

---

## Pertanyaan Refleksi

1. Mengapa MAE Rp100 dapat memiliki arti berbeda pada dua saham?
2. Apa perbedaan antara satuan rupiah, persentase, dan ×ATR?
3. Jika ATR_entry sebuah event adalah Rp200, berapa nilai rupiah dari 1,5 ATR?
4. Mengapa stop-loss 1 ATR tidak berarti risiko uang pasti sama?
5. Apa yang dimaksud dengan MAE-normalized dan MFE-normalized?
6. Mengapa MAE/MFE mentah tetap perlu disimpan meskipun TEKB menggunakan ×ATR?
7. Mengapa normalisasi tidak dapat menciptakan information edge?
8. Mengapa ATR-normalization tidak menjamin semua distribusi menjadi identik?
9. Apa yang terjadi jika MAE/MFE lengkap tetapi ATR_entry tidak tersedia?
10. Mengapa ATR setelah entry tidak boleh digunakan sebagai pengganti ATR_entry?
11. Mengapa status "MAE/MFE berhasil dihitung" harus dibedakan dari status "event layak masuk distribusi ×ATR"?

---

## Kalimat Kunci

> Satuan ×ATR tidak membuat sinyal menjadi lebih pintar. Satuan ini membuat pergerakan harga lebih mudah diukur dan dibandingkan dalam konteks volatilitasnya.

---

<div align="center">

[← Bab Sebelumnya](/posts/bab-10-atr-penggaris-volatilitas/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Bab Selanjutnya →](/posts/bab-12-candidate-sltp/)

</div>