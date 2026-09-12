---
title: "BAB 8 — B0: Mengapa Penelitian Membutuhkan Pembanding yang Adil?"
published: 2026-09-12
description: "B0 adalah fondasi pembanding dalam TEKB. Bab ini menjelaskan mengapa hasil B1 saja tidak cukup, apa itu counterfactual, dan bagaimana aturan B0 yang adil."
tags: ["bab-8", "b0", "pembanding", "counterfactual"]
category: "Bab"
draft: false
lang: ""
---

**BAGIAN II — MEMBANGUN BAHASA DAN DATA PENELITIAN**

---

## Tujuan Bab

Dalam penelitian trading, kita sering menemukan pernyataan seperti:

> "Setelah sinyal muncul, harga naik."

Pernyataan tersebut mungkin benar secara faktual. Namun, pernyataan itu belum cukup untuk membuktikan bahwa sinyal memiliki information edge.

Pertanyaan yang lebih penting adalah:

> "Apakah harga naik lebih baik dibandingkan kondisi pembanding yang wajar?"

Jika pasar secara umum memang sedang naik, hampir semua saham mungkin ikut naik. Jika kondisi pasar sedang sangat kuat, kenaikan setelah event belum tentu berasal dari informasi yang terkandung dalam event tersebut.

Karena itu, TEKB menggunakan **B0** sebagai fondasi pembanding.

Prinsip utamanya:

> Sebuah hasil tidak cukup hanya terlihat positif. Hasil harus dibandingkan dengan sesuatu yang adil.

---

## 8.1. Masalah dengan Kalimat "Setelah Sinyal, Harga Naik"

### Naik Dibandingkan Apa?

Misalkan penelitian menemukan 100 event volume tinggi. Setelah event tersebut, return tiga hari berikutnya adalah:

- 60 event menghasilkan return positif.
- Rata-rata return = +2%.

Apakah ini berarti event volume tinggi memiliki keunggulan?

Belum tentu.

Kita perlu bertanya:

- Bagaimana return saham yang sama pada hari-hari tanpa event?
- Bagaimana kondisi pasar pada periode tersebut?
- Apakah indeks pasar juga naik sekitar 2%?
- Apakah semua saham pada periode itu memang sedang mengalami kenaikan?
- Apakah kondisi yang tidak memiliki event menghasilkan return serupa?

Jika tanpa event saham yang sama juga rata-rata naik 1,8%, maka hasil +2% setelah event mungkin hanya memberikan tambahan informasi yang sangat kecil.

Sebaliknya, jika tanpa event return rata-rata hanya 0,2%, maka perbedaan antara +2% dan +0,2% menjadi lebih menarik untuk diteliti.

### Contoh Sederhana

Misalnya terdapat dua kelompok:

| Kelompok | Rata-rata Return 3 Hari |
|---|---|
| B1 — Setelah event | +2,0% |
| B0 — Tanpa event | +0,4% |

Perbedaan:

> Δ = 2,0% − 0,4% = 1,6%

Angka 1,6 percentage points tersebut lebih informatif daripada hanya mengatakan:

> "Setelah event, harga naik 2%."

Mengapa? Karena kita mulai mengetahui apakah kondisi event memberikan hasil yang berbeda dari kondisi pembanding.

### Apakah Kondisi Pasar Memang Sedang Naik?

Bayangkan pasar mengalami tren naik kuat selama tiga bulan. Pada periode tersebut:

- Saham A naik.
- Saham B naik.
- Saham C naik.
- Saham D naik.
- Bahkan saham yang tidak memiliki sinyal juga naik.

Jika penelitian hanya mengambil event yang muncul pada periode tersebut, peneliti dapat keliru menganggap kenaikan sebagai hasil dari event.

Padahal, sebagian kenaikan mungkin disebabkan oleh:

- Tren pasar.
- Sentimen sektor.
- Kondisi makroekonomi.
- Arus dana umum.
- Pemulihan setelah penurunan.
- Faktor lain yang juga memengaruhi saham tanpa event.

B0 membantu menjawab:

> "Apakah hasil setelah event berbeda dari kondisi yang sebanding tanpa event?"

### Apakah Semua Kejadian pada Waktu Itu Menghasilkan Hasil Serupa?

Misalnya event B1 terjadi pada periode ketika sektor energi sedang naik tajam. Jika saham-saham sektor energi lain yang tidak mengalami event juga naik, maka kenaikan B1 perlu ditafsirkan dengan hati-hati.

B1 mungkin hanya mengikuti kondisi umum.

Contoh:

| Kelompok | Return 3 Hari |
|---|---|
| Saham dengan event | +4,0% |
| Saham sebanding tanpa event | +3,7% |

Secara absolut, B1 naik cukup besar. Namun, keunggulannya terhadap pembanding hanya:

> Δ = 4,0% − 3,7% = 0,3%

Perbedaan tersebut mungkin terlalu kecil setelah memperhitungkan biaya, slippage, dan ketidakpastian.

### Mengapa Hasil B1 Saja Belum Cukup?

B1 adalah kelompok yang memiliki kondisi yang sedang diteliti. Misalnya:

> B1 adalah event dengan RV≥3.

Jika B1 menghasilkan return positif, kita baru mengetahui:

> "Kelompok event tersebut mengalami return tertentu."

Kita belum mengetahui apakah:

- Return tersebut lebih baik daripada kondisi normal.
- Event memberikan informasi tambahan.
- Hasil tersebut hanya mengikuti pasar.
- Hasil tersebut muncul karena pemilihan sampel.
- Hasil tersebut tetap terlihat setelah biaya.
- Hasil tersebut stabil pada data lain.

Karena itu, TEKB tidak berhenti pada pengukuran B1. TEKB juga membutuhkan B0 sebagai pembanding.

---

## 8.2. Apa Itu Counterfactual?

### Penjelasan Awam

**Counterfactual** adalah pertanyaan tentang:

> "Apa yang mungkin terjadi jika kondisi yang sedang kita uji tidak terjadi?"

Misalnya kita mengamati sebuah saham yang mengalami event volume tinggi, lalu harga naik 3%.

Pertanyaan counterfactual-nya adalah:

> "Jika event volume tinggi itu tidak terjadi, apakah saham tersebut tetap akan naik, mungkin naik 2%, 3%, atau justru turun?"

Masalahnya, kita tidak dapat mengamati dua keadaan yang sama persis pada waktu yang sama:

- Keadaan ketika event terjadi.
- Keadaan yang sama persis ketika event tidak terjadi.

Inilah yang sering disebut sebagai masalah counterfactual.

### Mengapa Masa Lalu Tidak Dapat Diulang Sempurna?

Pasar hanya berjalan dalam satu jalur aktual.

Misalnya pada 10 September:

- Volume saham ABCD tinggi.
- Harga kemudian naik.
- Event tercatat.

Kita tidak dapat memutar ulang tanggal tersebut dan menciptakan dunia alternatif di mana:

- Volume tidak tinggi.
- Semua faktor lain tetap persis sama.
- Pelaku pasar bertindak dengan cara yang sama.
- Berita dan likuiditas tetap identik.
- Harga bergerak dalam kondisi alternatif tersebut.

Karena itu, kita tidak dapat mengetahui counterfactual secara sempurna.

### B0 sebagai Pendekatan Pembanding

B0 digunakan sebagai pendekatan praktis untuk mendekati pertanyaan counterfactual.

B0 bukan dunia alternatif yang sempurna. B0 adalah kelompok pembanding yang dipilih dengan aturan tertentu agar konteksnya cukup sebanding dengan B1.

Dengan kata lain:

> B0 membantu memperkirakan bagaimana hasil mungkin terlihat pada kondisi yang tidak memiliki event yang sedang diuji, berdasarkan pembanding historis yang telah ditentukan.

B0 bukan bukti bahwa kita benar-benar mengetahui apa yang akan terjadi tanpa event. B0 adalah alat untuk mengurangi kesalahan interpretasi.

### Analogi Sederhana

Bayangkan seorang guru ingin mengetahui apakah metode belajar baru membantu siswa meningkatkan nilai.

Kelompok pertama menggunakan metode baru dan mendapat nilai rata-rata 85.

Apakah metode baru pasti efektif?

Belum tentu. Jika kelompok siswa lain yang tidak menggunakan metode baru juga mendapat nilai rata-rata 84, maka keunggulan metode baru mungkin kecil.

Namun, jika kelompok pembanding hanya mendapat rata-rata 70, perbedaannya lebih menarik.

Dalam analogi tersebut:

- Kelompok metode baru = B1.
- Kelompok pembanding = B0.
- Perbedaan hasil = estimasi keunggulan relatif.

Tetapi, seperti dalam penelitian trading, pembanding harus dipilih secara adil. Jika guru memilih kelompok pembanding yang sejak awal lebih lemah, hasilnya dapat menyesatkan.

### B0 Bukan Bukti Kausalitas Otomatis

Walaupun B0 membantu memperbaiki pengukuran, B0 tidak otomatis membuktikan bahwa event menyebabkan return.

Misalnya B1 menghasilkan return lebih tinggi daripada B0. Masih mungkin terdapat faktor lain:

- Kondisi pasar.
- Sektor.
- Likuiditas.
- Volatilitas.
- Berita.
- Posisi harga sebelum event.
- Faktor yang belum diukur.

Karena itu, bahasa yang tepat adalah:

> "B1 menunjukkan return yang lebih tinggi dibandingkan B0 dalam desain penelitian ini."

Bukan langsung:

> "Event menyebabkan harga naik."

---

## 8.3. B1 dan B0

### Apa Itu B1?

**B1** adalah kelompok event yang memiliki kondisi yang sedang diteliti.

Contohnya:

> B1 adalah event ketika RV≥3 berdasarkan baseline volume 20 bar valid sebelumnya.

B1 dapat memiliki karakteristik seperti:

- Instrumen tertentu.
- Waktu tertentu.
- Threshold tertentu.
- Definisi event tertentu.
- Aturan validasi tertentu.
- Aturan entry tertentu.

B1 harus ditentukan berdasarkan informasi yang tersedia pada saat event, bukan berdasarkan return setelah event.

### Apa Itu B0?

**B0** adalah kelompok pembanding yang dipilih menggunakan aturan yang telah ditentukan sebelumnya.

B0 harus dirancang agar konteksnya sebanding dengan B1, sejauh mungkin berdasarkan informasi yang tersedia tanpa menggunakan outcome masa depan.

Contoh:

- B1: event RV≥3 pada saham ABCD.
- B0: hari perdagangan lain pada saham ABCD yang tidak memenuhi event, dipilih berdasarkan aturan waktu dan matching yang telah ditentukan.

B0 tidak harus memiliki semua karakteristik B1 secara sempurna. Namun, B0 harus cukup masuk akal untuk menjadi pembanding.

### Contoh B1 dan B0

| Komponen | B1 | B0 |
|---|---|---|
| Instrumen | ABCD | ABCD |
| Kondisi | RV≥3 | Tidak memenuhi event |
| Waktu | Sesuai event | Waktu pembanding yang ditentukan |
| Entry | Open bar valid berikutnya | Open bar valid berikutnya |
| Horizon | 3 bar | 3 bar |
| Return | Diukur dengan rumus yang sama | Diukur dengan rumus yang sama |
| MAE/MFE | Engine yang sama | Engine yang sama |
| Biaya | Asumsi yang sama | Asumsi yang sama |

### Mengapa B1 dan B0 Harus Diukur dengan Mesin yang Sama?

Misalkan B1 dievaluasi menggunakan:

- Entry yang lebih menguntungkan.
- Biaya yang lebih rendah.
- Aturan exit yang lebih fleksibel.
- Penanganan gap yang lebih baik.

Sementara B0 dievaluasi menggunakan aturan yang lebih ketat.

Maka perbedaan hasil B1 dan B0 tidak lagi adil. B1 mungkin terlihat lebih baik bukan karena event, tetapi karena perlakuan evaluasinya berbeda.

Karena itu, B1 dan B0 harus menggunakan:

- Definisi entry yang sebanding.
- Horizon yang sama.
- Rumus return yang sama.
- Definisi MAE/MFE yang sama.
- ATR yang sama.
- Evaluation engine yang sama.
- Asumsi biaya yang sama.
- Aturan penanganan gap yang sama.
- Status data yang sama.

Perbedaan utama harus berasal dari kondisi yang sedang diuji, bukan dari perbedaan cara menghitung.

### Mengapa Pembanding Harus Berasal dari Konteks yang Sebanding?

B0 yang buruk dapat menghasilkan kesimpulan yang menyesatkan.

Misalnya B1 terdiri dari saham dengan likuiditas tinggi, sedangkan B0 terdiri dari saham yang sangat tidak likuid. Perbedaan return mungkin dipengaruhi oleh karakteristik likuiditas, bukan oleh event.

Konteks yang perlu dipertimbangkan dapat mencakup:

- Instrumen yang sama atau kelompok instrumen yang sesuai.
- Sesi atau slot waktu yang sama.
- Periode pasar yang sebanding.
- Kondisi perdagangan yang valid.
- Aturan entry yang sama.
- Horizon yang sama.
- Populasi yang sama.
- Pembatasan penggunaan ulang.
- Struktur dependensi event.

Semakin jauh konteks B0 dari B1, semakin sulit menafsirkan perbedaannya.

### B0 sebagai Kontrol, Bukan Lawan Dagang

B0 tidak harus dianggap sebagai strategi yang ingin "dikalahkan". B0 adalah alat kontrol untuk mengetahui apakah B1 memberikan informasi tambahan.

Pertanyaan penelitian bukan:

> "Apakah B1 menghasilkan profit?"

Melainkan:

> "Apakah B1 menghasilkan hasil yang berbeda atau lebih baik daripada kondisi pembanding yang wajar?"

---

## 8.4. Aturan B0 TEKB

B0 harus ditentukan secara eksplisit. Dalam TEKB, aturan B0 tidak boleh berubah-ubah hanya karena hasil tertentu terlihat lebih menarik.

Berikut prinsip utama B0 TEKB.

### 1. Instrumen yang Sama

Jika B1 terjadi pada saham ABCD, B0 sebaiknya berasal dari saham ABCD juga, kecuali desain penelitian secara eksplisit menetapkan pembanding lintas instrumen.

Menggunakan instrumen yang sama membantu mengurangi perbedaan akibat:

- Karakteristik volatilitas.
- Likuiditas.
- Spread.
- Harga saham.
- Struktur perdagangan.
- Perilaku sektoral.
- Frekuensi event.

Contoh:
B1: ABCD pada 10 September
B0: ABCD pada hari pembanding yang memenuhi aturan

Namun, penggunaan instrumen yang sama tidak otomatis menyelesaikan seluruh masalah. Waktu, kondisi pasar, dan aturan matching tetap penting.

### 2. Slot Waktu yang Sama

Untuk data intraday, B0 sebaiknya memperhatikan slot waktu yang sama.

Contoh:

- B1 terjadi pada pukul 10:35.
- B0 dipilih dari slot pukul 10:35 pada hari lain yang valid.

Hal ini penting karena volume dan volatilitas dapat berbeda menurut waktu dalam satu sesi.

Volume pukul 09:05 tidak selalu dapat dibandingkan langsung dengan volume pukul 14:45. Demikian pula, karakteristik pembukaan pasar dapat berbeda dari kondisi menjelang penutupan.

Jika slot waktu tidak disamakan, perbedaan B1 dan B0 mungkin hanya mencerminkan pola musiman intraday.

### 3. Populasi yang Memperhitungkan Declustering

Event yang muncul berdekatan dapat saling berkaitan.

Contohnya:

- Event volume tinggi muncul pada Senin.
- Event lain muncul pada Selasa.
- Event lain muncul lagi pada Rabu.

Ketiganya mungkin merupakan bagian dari satu episode pasar yang sama.

Jika setiap event diperlakukan sebagai kejadian yang sepenuhnya independen, jumlah bukti dapat terlihat lebih besar daripada kenyataannya.

Karena itu, TEKB dapat menggunakan **declustering**, yaitu aturan untuk mengurangi penghitungan berulang dari satu episode yang sama.

Contoh aturan:

> Jika event baru muncul dalam jendela 5 hari setelah event sebelumnya pada instrumen yang sama, hanya event pertama yang dipertahankan sebagai event utama.

Aturan declustering harus ditentukan sebelum pengujian.

Declustering dapat membantu:

- Mengurangi pengulangan episode yang sama.
- Mengurangi dominasi satu periode ekstrem.
- Membuat unit analisis lebih masuk akal.
- Menyesuaikan metode bootstrap dengan dependensi data.

Namun, declustering bukan berarti semua dependensi otomatis hilang. Struktur data tetap perlu diperiksa.

### 4. Hari Perdagangan Valid Terdekat

Untuk data harian, B0 dapat dipilih dari hari perdagangan valid terdekat sesuai aturan yang telah ditentukan.

Contohnya:

- B1 terjadi pada 10 Maret.
- B0 dicari pada hari perdagangan valid yang memenuhi seluruh syarat matching.

Hari libur dan data invalid tidak dianggap sebagai hari pembanding yang sah.

"Valid" dapat berarti:

- Data OHLCV tersedia.
- Tidak ada kerusakan data yang melanggar kontrak.
- Instrumen masih termasuk dalam populasi.
- Hari tersebut tidak termasuk event yang dilarang.
- Tidak melanggar aturan reuse.
- Tidak berada di luar partisi IS/OOS.

### 5. Tie-Break ke Hari Sebelumnya

Jika terdapat lebih dari satu kandidat B0 dengan jarak yang sama, aturan tie-break harus ditentukan.

Contoh:

- Kandidat satu hari sebelum B1 tersedia.
- Kandidat satu hari sesudah B1 juga tersedia.
- Keduanya memiliki jarak waktu yang sama.

TEKB dapat menetapkan:

> Jika jarak sama, pilih hari sebelumnya.

Aturan ini disebut **tie-break**.

Contoh urutannya:

1. Cari kandidat dengan jarak terdekat.
2. Jika jaraknya sama, pilih hari sebelumnya.
3. Jika hari sebelumnya tidak valid, gunakan aturan cadangan yang telah ditentukan.
4. Jika tidak ada kandidat yang memenuhi, catat NO_MATCH_FOUND.

Tie-break tidak boleh diputuskan setelah melihat return B0.

### 6. Partisi IS/OOS yang Sama

B1 dan B0 harus berada dalam partisi penelitian yang sesuai.

Jika B1 berasal dari periode IS, B0 juga harus dipilih dari periode IS.

Jika B1 berasal dari periode OOS, B0 harus dipilih berdasarkan aturan OOS yang sama dan tidak menggunakan informasi dari masa depan.

Contoh:

- B1 IS: 2016–2021.
- B0 IS: juga dipilih dalam 2016–2021.
- B1 OOS: 2022–2025.
- B0 OOS: juga dipilih dalam 2022–2025.

B0 tidak boleh mengambil data dari periode yang tidak boleh diakses oleh B1.

Jika B0 dipilih dari seluruh sejarah termasuk masa depan, maka pembanding tersebut dapat membawa informasi yang tidak tersedia pada saat penelitian berjalan.

### 7. Tidak Boleh Digunakan Ulang

Jika kontrak penelitian melarang penggunaan ulang, satu event B0 tidak boleh dipasangkan dengan banyak B1.

Contoh:

- B1-01 menggunakan B0-01.
- B1-02 tidak boleh menggunakan B0-01 lagi jika aturan menyatakan no reuse.

Aturan **no reuse** membantu mencegah satu observasi pembanding memiliki pengaruh berlebihan terhadap hasil agregat.

Namun, apakah reuse diperbolehkan atau tidak harus ditentukan sejak awal. Tidak semua desain penelitian membutuhkan aturan yang sama. Yang penting adalah konsistensi dan transparansi.

### 8. Pemilihan Tidak Berdasarkan Outcome

B0 harus dipilih berdasarkan informasi yang tersedia sebelum atau pada waktu matching yang diizinkan.

B0 tidak boleh dipilih karena:

- Return-nya mirip dengan B1.
- Return-nya lebih rendah sehingga B1 terlihat bagus.
- Hasilnya menguntungkan.
- Tidak mengalami stop-loss.
- Menghasilkan profit terbesar.
- Memiliki MAE kecil setelah event.
- Cocok dengan cerita yang ingin dibangun.

B0 harus dipilih berdasarkan aturan, bukan berdasarkan hasil.

### Ringkasan Aturan B0 TEKB

| Aturan | Tujuan |
|---|---|
| Instrumen sama | Mengurangi perbedaan karakteristik instrumen |
| Slot waktu sama | Mengendalikan pola musiman waktu |
| Declustering | Mengurangi pengulangan episode yang sama |
| Hari perdagangan valid terdekat | Menentukan pembanding secara sistematis |
| Tie-break ke hari sebelumnya | Menghindari keputusan subjektif |
| Partisi IS/OOS sama | Menjaga pemisahan informasi |
| Tidak digunakan ulang | Menghindari dominasi satu pembanding |
| Tidak berdasarkan outcome | Mencegah bias seleksi |

---

## 8.5. Mengapa B0 Tidak Boleh Dipilih Berdasarkan Hasil?

### Pembanding Harus Dipilih Sebelum Outcome Diketahui

B0 harus dipilih berdasarkan aturan yang tidak menggunakan hasil masa depan.

Jika peneliti memilih B0 setelah melihat hasil B1, maka B0 dapat menjadi alat untuk membenarkan kesimpulan yang sudah diinginkan.

Contohnya:

> "Saya akan mencari hari tanpa event yang return-nya rendah supaya event terlihat lebih unggul."

Ini bukan pembanding yang adil. Ini adalah pemilihan pembanding berdasarkan hasil.

### Tidak Boleh Memilih karena Return-nya Mirip

Sekilas, peneliti mungkin berpikir bahwa B0 yang memiliki return awal mirip dengan B1 akan menjadi pembanding yang baik.

Namun, memilih B0 berdasarkan return yang diketahui dapat menciptakan masalah karena return tersebut adalah informasi hasil.

Misalnya:

- B1 menghasilkan +4%.
- Peneliti mencari B0 yang sebelum evaluasi juga memiliki karakteristik return tertentu agar hasil akhirnya sesuai.
- B0 dipilih setelah informasi tersebut diketahui.

Jika outcome atau informasi yang berkaitan dengan outcome digunakan untuk memilih B0, maka perbandingan tidak lagi bebas dari bias.

B0 harus dipilih berdasarkan konteks, bukan berdasarkan kemiripan hasil yang baru diketahui.

### Tidak Boleh Memilih karena Outcome Menguntungkan

Contoh kesalahan:

> "Saya memilih hari pembanding yang tidak memiliki event dan ternyata return-nya rendah."

Jika pemilihan hari tersebut dilakukan setelah mengetahui return-nya, maka B0 telah dipilih secara outcome-based.

Hal ini dapat membuat:

- Delta B1−B0 terlalu besar.
- Varians terlihat lebih kecil.
- Hasil terlihat lebih stabil.
- Klaim edge menjadi terlalu optimistis.

### Tidak Boleh Menggunakan Informasi Masa Depan

Misalnya event terjadi pada 10 Maret. Peneliti memilih B0 pada 8 Maret karena setelah diketahui, hasil B0 paling cocok dengan hipotesis.

Jika pemilihan tersebut menggunakan return setelah 8 Maret, maka informasi masa depan telah digunakan.

B0 harus dipilih berdasarkan informasi yang memang diizinkan oleh kontrak penelitian, misalnya:

- Instrumen.
- Slot waktu.
- Status event.
- Jarak kalender.
- Status validitas data.
- Partisi IS/OOS.
- Aturan reuse.
- Informasi yang tersedia pada saat matching.

### Tidak Boleh Memilih Setelah Melihat Hasil Evaluasi

B0 tidak boleh dipilih setelah peneliti mengetahui:

- Apakah B1 profit.
- Apakah B1 mencapai target.
- Apakah B1 mengalami stop-loss.
- Apakah B1 memiliki MAE besar.
- Apakah B1 memiliki MFE besar.
- Apakah B1 berhasil pada horizon tertentu.

Jika B0 dipilih setelah evaluasi, maka pembanding dapat secara tidak sadar diarahkan untuk memperbesar atau memperkecil perbedaan.

### Contoh B0 yang Tidak Sah

Misalnya peneliti memiliki event B1 berikut:

| B1 | Return |
|---|---|
| B1-01 | +5% |

Kemudian peneliti memiliki tiga kandidat B0:

| Kandidat B0 | Return |
|---|---|
| B0-A | +4% |
| B0-B | +1% |
| B0-C | −3% |

Jika peneliti memilih B0-C karena membuat delta terlihat paling besar:

> Δ = 5% − (−3%) = 8%

maka delta 8% tersebut tidak dapat dianggap sebagai hasil dari aturan matching yang netral. B0 telah dipilih berdasarkan outcome.

### Contoh B0 yang Lebih Sah

Aturan telah ditentukan sebelum hasil diketahui:

- Gunakan instrumen yang sama.
- Cari hari non-event terdekat.
- Gunakan slot waktu yang sama.
- Tidak boleh memakai event lain.
- Jika jarak sama, pilih hari sebelumnya.
- Tidak boleh menggunakan ulang B0.
- Jika tidak ada kandidat valid, beri status NO_MATCH_FOUND.

Dengan aturan tersebut, B0 dipilih karena memenuhi kontrak, bukan karena menghasilkan angka yang menguntungkan.

### Prinsip Utama

> B0 harus dipilih karena aturan menyatakan bahwa ia layak menjadi pembanding, bukan karena hasilnya membuat B1 terlihat bagus.

---

## 8.6. Apa Arti NO_MATCH_FOUND?

### Tidak Semua B1 Harus Memiliki B0

Dalam penelitian nyata, tidak selalu tersedia pembanding yang memenuhi seluruh aturan.

Misalnya B1 membutuhkan:

- Instrumen yang sama.
- Slot waktu yang sama.
- Hari non-event.
- Data lengkap.
- Tidak digunakan ulang.
- Berada dalam partisi yang sama.
- Memenuhi aturan declustering.
- Tidak melanggar batas waktu.

Bisa saja tidak ada satu pun kandidat yang memenuhi semua syarat tersebut.

Dalam kondisi ini, TEKB menggunakan status:

> NO_MATCH_FOUND

Artinya:

> Tidak ditemukan pembanding B0 yang memenuhi aturan matching yang telah ditentukan.

### Mengapa Tidak Boleh Memaksa Pasangan?

Peneliti mungkin tergoda untuk berkata:

> "Kalau tidak ada B0 yang cocok, gunakan saja hari apa pun."

Namun, tindakan tersebut dapat merusak keadilan desain.

Jika B0 dipilih secara sembarangan, pembanding mungkin:

- Berasal dari konteks yang berbeda.
- Memiliki kondisi pasar yang tidak sebanding.
- Menggunakan slot waktu yang berbeda.
- Berasal dari periode yang tidak sesuai.
- Sudah digunakan untuk event lain.
- Mengandung informasi yang tidak tersedia saat event.
- Dipilih karena hasilnya menguntungkan.

Memaksakan pasangan hanya demi meningkatkan jumlah sampel dapat lebih buruk daripada memiliki jumlah pasangan yang lebih sedikit tetapi valid.

### Event Tetap Dicatat

Jika B1 tidak memiliki B0, event tersebut tidak boleh dihapus tanpa jejak.

Event tetap dicatat dengan informasi seperti:

- Event ID.
- Instrumen.
- Timestamp.
- Definisi event.
- Nilai event.
- Status validitas event.
- Alasan tidak memperoleh pasangan.
- Aturan matching yang gagal.
- Research batch ID.

Contoh:
event_id: EVT-ABCD-20260910-1035-001
event_status: VALID
b0_match_status: NO_MATCH_FOUND
b0_match_reason: NO_VALID_NON_EVENT_SLOT
included_in_event_log: true
included_in_edge_computation: false

Dengan cara ini, event tetap menjadi bagian dari audit trail meskipun tidak digunakan dalam perhitungan perbedaan B1−B0.

### Event Tanpa Pembanding Dikeluarkan dari Perhitungan Edge

Jika desain penelitian mensyaratkan pasangan B1 dan B0, event tanpa B0 tidak boleh dipakai untuk menghitung edge berpasangan.

Misalnya:

- Total event B1 valid = 120.
- B1 yang memperoleh B0 valid = 100.
- B1 tanpa B0 = 20.

Maka laporan harus membedakan:

| Kategori | Jumlah |
|---|---|
| Event valid terdeteksi | 120 |
| Event dengan B0 valid | 100 |
| Event NO_MATCH_FOUND | 20 |

Perhitungan delta paired dilakukan pada 100 pasangan yang valid, bukan dengan memaksakan 20 event sisanya menggunakan pembanding sembarang.

### Mengapa Ini Lebih Jujur?

Jika event tanpa pasangan dipaksa masuk, peneliti dapat memperoleh jumlah sampel yang lebih besar, tetapi kualitas pembanding menurun.

Dengan menggunakan NO_MATCH_FOUND, peneliti mengakui keterbatasan desain:

> "Event ini memang terjadi, tetapi tidak tersedia pembanding yang memenuhi kontrak penelitian."

Pernyataan tersebut lebih jujur daripada menciptakan pasangan yang sebenarnya tidak sah.

### Dampak terhadap Interpretasi

Jika jumlah NO_MATCH_FOUND besar, peneliti perlu mengevaluasi:

- Apakah aturan B0 terlalu ketat?
- Apakah event terlalu jarang?
- Apakah instrumen atau slot waktu terlalu spesifik?
- Apakah aturan no reuse mengurangi pasangan secara signifikan?
- Apakah desain matching perlu ditinjau dalam penelitian baru?
- Apakah hasil paired analysis berpotensi hanya mewakili subset tertentu?

Namun, aturan tidak boleh diubah di tengah penelitian hanya untuk meningkatkan jumlah pasangan. Jika desain B0 diubah, perubahan tersebut harus dicatat sebagai versi atau penelitian baru.

### Contoh Ringkasan Matching

| Status Matching | Jumlah | Perlakuan |
|---|---|---|
| MATCHED | 100 | Digunakan dalam analisis paired |
| NO_MATCH_FOUND | 15 | Dicatat, tidak digunakan dalam delta paired |
| INVALIDATED | 3 | Dikeluarkan sesuai aturan validitas |
| INSUFFICIENT_HORIZON | 2 | Tidak digunakan untuk metrik yang membutuhkan horizon penuh |

### Prinsip Utama

> Tidak memiliki pasangan yang sah lebih baik daripada memiliki pasangan yang dipaksakan.

---

## Contoh Mini B1 dan B0

Misalkan penelitian ingin menguji apakah event RV≥3 berkaitan dengan return tiga hari berikutnya yang berbeda dari kondisi non-event.

### Aturan Penelitian

- Instrumen: ABCD.
- Event B1: RV≥3.
- Baseline: 20 hari valid sebelumnya.
- Entry: open hari valid berikutnya.
- Horizon: 3 hari.
- B0: non-event terdekat yang valid.
- Tie-break: pilih hari sebelumnya.
- No reuse: satu B0 hanya boleh digunakan sekali.
- Evaluasi: engine yang sama.
- Return: dari entry sampai close hari ketiga.

### Hasil Contoh

| Pasangan | B1 Return | B0 Return | Delta |
|---|---|---|---|
| 1 | +3,9% | +2,0% | +1,9% |
| 2 | +0,9% | 0,0% | +0,9% |
| 3 | −3,8% | −2,9% | −0,9% |
| 4 | +5,0% | +2,5% | +2,5% |
| 5 | +1,8% | +0,9% | +0,9% |
| 6 | −2,3% | −1,5% | −0,8% |
| 7 | +3,2% | +1,6% | +1,6% |
| 8 | +1,4% | +0,7% | +0,7% |

Rata-rata return B1 sekitar:

> R̄_B1 ≈ 1,26%

Rata-rata return B0 sekitar:

> R̄_B0 ≈ 0,40%

Perbedaan rata-rata:

> Δ ≈ 1,26% − 0,40% = 0,86 percentage points

Interpretasi yang hati-hati:

> Dalam contoh fiktif ini, event B1 memiliki rata-rata return yang lebih tinggi daripada B0 sekitar 0,86 percentage points.

Interpretasi yang belum boleh dibuat:

> "RV≥3 pasti menyebabkan harga naik 0,86%."

Perbedaan tersebut masih perlu diperiksa melalui:

- Jumlah sampel yang memadai.
- Distribusi return.
- MAE dan MFE.
- Biaya transaksi.
- Bootstrap.
- Multiple testing.
- Robustness.
- Seleksi IS.
- Freeze.
- OOS.

---

## Ringkasan Bab 8

B0 merupakan fondasi penting dalam penelitian TEKB karena hasil B1 saja belum cukup untuk menunjukkan adanya information edge.

Kalimat:

> "Setelah sinyal, harga naik"

belum menjawab:

> "Apakah kenaikan tersebut lebih baik daripada kondisi pembanding yang wajar?"

B0 membantu menjawab pertanyaan tersebut, meskipun tidak dapat menciptakan counterfactual yang sempurna.

### Pelajaran Utama

- Return positif setelah event belum tentu menunjukkan edge.
- Hasil harus dibandingkan dengan kondisi pembanding yang adil.
- Counterfactual adalah pertanyaan tentang apa yang mungkin terjadi tanpa kondisi yang diuji.
- B0 merupakan pendekatan praktis untuk mendekati counterfactual, bukan bukti kausalitas otomatis.
- B1 adalah kelompok event yang diteliti; B0 adalah kelompok pembanding yang ditentukan dengan aturan.
- B1 dan B0 harus menggunakan engine, entry, horizon, rumus, biaya, dan aturan evaluasi yang sama.
- B0 harus berasal dari konteks yang sebanding.
- Pemilihan B0 tidak boleh berdasarkan return atau outcome yang telah diketahui.
- Aturan instrumen, slot waktu, declustering, nearest valid day, tie-break, partisi IS/OOS, dan no reuse harus ditentukan secara eksplisit.
- NO_MATCH_FOUND adalah hasil yang sah, bukan kegagalan yang harus disembunyikan.
- Event tanpa pasangan tetap dicatat dalam audit trail, tetapi tidak digunakan dalam perhitungan edge paired.
- Pembanding yang dipaksakan dapat lebih merusak daripada jumlah sampel yang lebih kecil tetapi valid.

> B1 memberi tahu apa yang terjadi setelah event. B0 membantu kita menilai apakah hasil tersebut benar-benar berbeda dari kondisi yang wajar.

---

## Pertanyaan Refleksi

1. Mengapa return positif setelah event belum tentu menunjukkan edge?
2. Apa yang dimaksud dengan counterfactual?
3. Apa perbedaan antara B1 dan B0?
4. Mengapa B1 dan B0 harus diukur dengan mesin yang sama?
5. Mengapa B0 tidak boleh dipilih berdasarkan return atau outcome?
6. Apa itu NO_MATCH_FOUND, dan mengapa status ini penting?
7. Mengapa event tanpa pasangan tetap harus dicatat dalam audit trail?
8. Mengapa pembanding yang dipaksakan bisa lebih buruk daripada jumlah sampel yang lebih kecil?

---

<div align="center">

[← Bab Sebelumnya](/posts/bab-07-dari-ada-sinyal/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Bab Selanjutnya →](/posts/bab-09-mae-dan-mfe/)

</div>