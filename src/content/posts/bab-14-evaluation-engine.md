---
title: "BAB 14 — Evaluation Engine: Wasit yang Menggunakan Aturan yang Sama"
published: 2026-09-12
description: "Evaluation Engine adalah wasit yang menilai setiap event dengan aturan yang sama. Bab ini menjelaskan TP_HIT, SL_HIT, TIMEOUT, gap-through, dan ambiguitas intrabar."
tags: ["bab-14", "evaluation-engine", "sl-tp", "wasit"]
category: "Bab"
draft: false
lang: ""
---

**BAGIAN V — MESIN YANG MENENTUKAN APAKAH SEBUAH HIPOTESIS BEKERJA**

---

Dalam pertandingan olahraga, hasil pertandingan tidak ditentukan hanya berdasarkan kesan penonton. Diperlukan wasit yang menggunakan aturan yang sama untuk kedua tim. Wasit menentukan apakah terjadi pelanggaran, apakah gol sah, kapan pertandingan berakhir, dan bagaimana hasil akhirnya dicatat.

Penelitian trading juga membutuhkan sesuatu yang serupa. Ketika sebuah event diuji dengan kandidat Stop Loss atau Take Profit, kita memerlukan mesin yang menentukan hasil berdasarkan aturan yang sudah ditetapkan. Mesin ini disebut **Evaluation Engine**.

Evaluation Engine bukan mesin peramal. Ia juga bukan mesin yang mencari hasil paling menguntungkan. Tugasnya lebih sederhana, tetapi sangat penting: menilai setiap event secara **konsisten**, **deterministik**, dan **dapat diaudit**.

Jika B1 dan B0 dinilai dengan aturan berbeda, perbandingan menjadi tidak adil. Jika satu event dinilai secara manual dan event lain dinilai dengan aturan berbeda, hasil penelitian dapat berubah hanya karena cara penilaian. Evaluation Engine dibutuhkan agar hasil tidak bergantung pada tafsir manusia setelah melihat chart.

---

## 14.1. Mengapa Kita Membutuhkan "Wasit"?

Chart harga dapat ditafsirkan dengan banyak cara. Dua orang yang melihat candle yang sama mungkin memberikan kesimpulan berbeda:

- Orang pertama menganggap TP sudah tersentuh.
- Orang kedua menganggap SL tersentuh lebih dahulu.
- Orang ketiga menganggap trade masih berjalan.
- Orang keempat mengabaikan gap karena menganggap harga tidak sempat menyentuh level secara tepat.

Masalah ini menjadi serius ketika jumlah event mencapai ratusan atau ribuan. Penilaian manual dapat menghasilkan ketidakkonsistenan, terutama ketika:

- Harga bergerak cepat.
- Satu candle memiliki range yang lebar.
- SL dan TP sama-sama berada dalam range candle.
- Harga membuka pasar dengan gap.
- Data memiliki jeda atau market break.
- Event B1 dan B0 memiliki karakteristik yang berbeda.

Tanpa aturan yang tetap, peneliti dapat secara sadar atau tidak sadar memberikan perlakuan berbeda kepada event yang hasilnya disukai dan tidak disukai.

Misalnya, ketika sebuah event terlihat menguntungkan, peneliti mungkin menganggap target tercapai. Namun, ketika event lain terlihat buruk, peneliti mungkin menggunakan asumsi yang lebih ketat. Ini menciptakan **bias evaluasi**.

Evaluation Engine berfungsi sebagai wasit karena:

- Menggunakan aturan yang sama untuk seluruh event.
- Menggunakan aturan yang sama untuk B1 dan B0.
- Tidak mengubah aturan berdasarkan hasil event.
- Tidak menebak informasi yang tidak tersedia.
- Mencatat status dan alasan hasil evaluasi.
- Menghasilkan hasil yang dapat diulang.

Dengan demikian, Evaluation Engine menjaga agar pertanyaan penelitian tidak berubah di tengah proses pengukuran.

---

## 14.2. Apa yang Dilakukan Evaluation Engine?

Evaluation Engine menerima informasi event, definisi entry, kandidat SL/TP, data harga, dan aturan evaluasi. Kemudian mesin memeriksa apa yang terjadi setelah entry.

Secara umum, Evaluation Engine melakukan beberapa tugas berikut.

### 1. Menentukan Apakah TP Tersentuh

Untuk posisi long, TP berada di atas harga entry. Mesin memeriksa apakah harga High pada salah satu bar evaluasi mencapai atau melewati level TP.

Jika TP tersentuh sesuai aturan, mesin mencatat bahwa target tercapai.

### 2. Menentukan Apakah SL Tersentuh

Untuk posisi long, SL berada di bawah harga entry. Mesin memeriksa apakah harga Low pada salah satu bar evaluasi mencapai atau melewati level SL.

Jika SL tersentuh sesuai aturan, mesin mencatat bahwa batas kerugian tercapai.

### 3. Menentukan Apakah Trade Berakhir TIMEOUT

Jika tidak ada SL atau TP yang tersentuh sampai batas waktu yang ditetapkan, trade berakhir karena waktu evaluasi habis.

Status ini disebut **TIMEOUT**.

TIMEOUT bukan berarti trade gagal. TIMEOUT hanya berarti tidak ada SL atau TP yang tercapai sebelum batas waktu berakhir.

### 4. Mencatat Harga Keluar

Mesin mencatat harga keluar sesuai aturan:

- Harga Open jika terjadi gap-through.
- Level SL jika SL tersentuh secara normal.
- Level TP jika TP tersentuh secara normal.
- Harga penutupan atau harga yang ditentukan protokol jika trade berakhir TIMEOUT.

Harga keluar harus mengikuti aturan yang telah ditetapkan. Mesin tidak boleh memilih harga keluar yang paling menguntungkan hanya karena harga tersebut tersedia di dalam candle.

### 5. Mencatat Durasi

Mesin mencatat berapa lama trade berlangsung:

- Berapa bar sejak entry.
- Pada bar ke berapa SL atau TP tersentuh.
- Berapa lama sampai TIMEOUT.

Durasi membantu penelitian memahami apakah sebuah kondisi menghasilkan gerakan cepat atau membutuhkan waktu panjang.

### 6. Mencatat Status Evaluasi

Selain outcome, mesin harus mencatat status evaluasi. Contoh status antara lain:

- TP_HIT
- SL_HIT
- TIMEOUT
- AMBIGUOUS_INTRABAR
- INSUFFICIENT_HORIZON
- INVALIDATED
- INVALID_DATA

Status tersebut penting karena dua hasil dengan angka return yang sama belum tentu memiliki proses evaluasi yang sama.

Secara sederhana, alur Evaluation Engine dapat digambarkan sebagai:

> Event valid → Entry ditentukan → Kandidat SL/TP ditentukan → Bar evaluasi diperiksa → Kondisi exit ditentukan → Harga keluar dicatat → Durasi dan status dicatat → Hasil dikirim ke agregasi.

Evaluation Engine tidak memilih kandidat terbaik. Ia hanya menjalankan aturan evaluasi yang sama terhadap setiap kandidat.

---

## 14.3. Jendela Evaluasi

Evaluation Engine tidak boleh memeriksa seluruh data tanpa batas. Setiap trade harus memiliki jendela evaluasi yang jelas.

Jendela evaluasi menentukan:

- Kapan evaluasi dimulai.
- Bar apa saja yang boleh digunakan.
- Kapan evaluasi berakhir.
- Berapa lama trade boleh dianggap aktif.
- Bagaimana hubungan antara entry, horizon, dan maximum hold.

Dalam protokol TEKB, evaluasi dimulai pada bar T+1, yaitu bar setelah bar sinyal atau bar event yang telah ditentukan.

Jika sinyal terbentuk pada bar T dan entry menggunakan Open pada bar berikutnya, maka bar entry tersebut menjadi awal evaluasi sesuai definisi engine. Evaluasi tidak boleh dimulai dari bar sebelum entry dan tidak boleh menggunakan informasi masa depan di luar jendela yang ditetapkan.

### Mengapa Evaluasi Dimulai pada T+1?

Misalnya:

- Bar T adalah bar ketika kondisi sinyal terdeteksi.
- Entry dilakukan pada Open bar T+1.
- Setelah entry, mesin memeriksa pergerakan High dan Low pada bar-bar berikutnya.

Aturan ini mencegah mesin menggunakan pergerakan yang terjadi sebelum posisi benar-benar dianggap masuk.

Jika harga pada bar sinyal sudah naik sebelum entry, kenaikan tersebut tidak boleh dihitung sebagai keuntungan trade yang belum dimiliki.

### Hubungan Entry, Horizon, dan Maximum Hold

Ada beberapa istilah yang perlu dibedakan:

- **Entry:** titik harga dan waktu ketika posisi dianggap mulai.
- **Horizon:** jangka waktu pengukuran hasil, misalnya 1, 3, 5, atau 10 bar.
- **Maximum hold:** batas waktu maksimum trade untuk kandidat SL/TP.
- **Evaluation window:** seluruh rentang bar yang boleh diperiksa oleh mesin.

Contohnya, suatu kandidat memiliki:

- Entry pada Open T+1.
- SL = 1 × ATR.
- TP = 2 × ATR.
- Maximum hold = 5 bar.

Mesin akan memeriksa bar yang termasuk dalam jendela evaluasi sampai:

- SL tersentuh.
- TP tersentuh.
- Ambiguitas tidak dapat diselesaikan berdasarkan aturan.
- Lima bar evaluasi selesai dan tidak ada level yang tersentuh.

Jika tidak ada level yang tercapai sampai batas waktu tersebut, hasilnya adalah TIMEOUT.

### Konsistensi Indeks Bar

Kesalahan kecil dalam indeks bar dapat mengubah hasil penelitian. Misalnya, jika satu bagian sistem menghitung maximum hold lima bar dari bar entry, tetapi bagian lain menghitung lima bar setelah bar entry, hasilnya tidak lagi sebanding.

Karena itu, TEKB harus menetapkan secara eksplisit:

- Apakah bar entry dihitung sebagai bar evaluasi pertama.
- Bar mana yang menjadi evaluasi ke-1.
- Bar mana yang menjadi evaluasi terakhir.
- Apakah exit TIMEOUT menggunakan Close bar terakhir.
- Bagaimana market break atau sesi perdagangan diperlakukan.

Aturan tersebut harus dibekukan dan digunakan sama untuk B1, B0, seluruh kandidat, serta seluruh periode IS dan OOS.

---

## 14.4. Gap-Through

**Gap-through** terjadi ketika harga pada Open langsung berada di luar level SL atau TP. Artinya, harga tidak bergerak secara bertahap melalui level tersebut dalam data yang tersedia. Harga langsung dibuka melewati level.

Gap-through penting karena asumsi sederhana "exit selalu terjadi tepat pada harga SL atau TP" dapat menjadi tidak realistis.

### Contoh Gap-Through pada SL

Misalnya:

- Harga entry: Rp1.000.
- SL: Rp980.
- Pada bar berikutnya, pasar dibuka pada Rp950.

Harga Open Rp950 sudah berada di bawah SL Rp980. Dalam kondisi ini, posisi tidak realistis dianggap keluar tepat pada Rp980 jika harga tidak pernah tersedia di level tersebut setelah entry.

Sesuai aturan TEKB, exit gap-through dianggap terjadi pada harga Open, yaitu Rp950.

Dengan demikian:

- Harga SL teoritis: Rp980.
- Harga keluar aktual menurut aturan gap-through: Rp950.

Kerugian direalisasikan berdasarkan Rp950, bukan dipaksakan pada Rp980.

### Contoh Gap-Through pada TP

Misalnya:

- Harga entry: Rp1.000.
- TP: Rp1.050.
- Pada bar berikutnya, pasar dibuka pada Rp1.100.

Harga Open Rp1.100 sudah berada di atas TP Rp1.050. Dalam kondisi ini, exit dianggap terjadi pada Open Rp1.100, bukan otomatis pada Rp1.050.

Mesin mencatat bahwa target telah terlewati melalui gap dan harga keluar mengikuti Open.

### Mengapa Gap-Through Harus Ditangani Secara Eksplisit?

Tanpa aturan gap-through:

- Hasil dapat terlalu optimistis.
- Harga exit dapat tidak realistis.
- Perbandingan antar-event menjadi tidak konsisten.
- Perhitungan realized P&L dapat salah.
- Hasil B1 dan B0 dapat dipengaruhi oleh perlakuan gap yang berbeda.

Gap-through bukan kesalahan data dengan sendirinya. Gap adalah karakteristik pergerakan harga yang harus ditangani secara eksplisit.

Yang penting, aturan gap-through ditentukan sebelum evaluasi dan tidak diubah hanya untuk memperbaiki hasil.

---

## 14.5. Jika TP dan SL Tersentuh pada Bar yang Sama

Salah satu persoalan paling sulit dalam evaluasi berbasis OHLCV adalah ketika High dan Low pada satu bar menunjukkan bahwa TP dan SL sama-sama tersentuh.

Misalnya:

- Entry long: Rp1.000.
- TP: Rp1.050.
- SL: Rp980.
- High bar: Rp1.060.
- Low bar: Rp970.

Dari data tersebut kita tahu bahwa harga pernah mencapai atau melewati kedua level. Namun, kita tidak tahu urutannya hanya dari OHLCV.

Kemungkinan pertama:

- Harga turun lebih dahulu ke Rp980.
- SL tersentuh.
- Setelah itu harga naik ke Rp1.060.

Kemungkinan kedua:

- Harga naik lebih dahulu ke Rp1.050.
- TP tersentuh.
- Setelah itu harga turun ke Rp970.

Kedua urutan tersebut menghasilkan outcome yang berbeda, tetapi data OHLCV satu bar tidak selalu menyediakan urutan intrabar yang diperlukan untuk membedakannya.

### AMBIGUOUS_INTRABAR

Kondisi seperti ini disebut **AMBIGUOUS_INTRABAR**.

Artinya:

> Data pada resolusi yang digunakan tidak cukup untuk memastikan urutan kejadian di dalam bar.

TEKB tidak boleh menebak bahwa TP terjadi lebih dahulu hanya karena hasilnya lebih menguntungkan. TEKB juga tidak boleh selalu menganggap SL terjadi lebih dahulu tanpa menyatakan bahwa itu adalah pilihan konservatif.

Jika urutan tidak dapat diketahui, ambiguitas harus dicatat sebagai bagian dari hasil evaluasi.

### Mengapa Tidak Boleh Menebak Urutan?

Menebak urutan berdasarkan hasil yang diinginkan dapat menciptakan bias. Misalnya, jika peneliti memilih TP lebih dahulu setiap kali kedua level tersentuh, hasil strategi akan tampak lebih baik daripada kondisi yang dapat dibuktikan oleh data.

Sebaliknya, jika peneliti selalu memilih SL lebih dahulu tetapi tidak menyatakan bahwa itu merupakan skenario konservatif, pembaca dapat mengira bahwa urutan tersebut benar-benar diketahui.

Masalahnya bukan memilih skenario, melainkan menyamarkan asumsi sebagai fakta.

### Hasil sebagai Rentang

Untuk AMBIGUOUS_INTRABAR, TEKB dapat melaporkan dua skenario:

- **Worst-case:** asumsi yang paling merugikan di antara urutan yang masih mungkin.
- **Best-case:** asumsi yang paling menguntungkan di antara urutan yang masih mungkin.

Dengan demikian, penelitian tidak berpura-pura mengetahui sesuatu yang tidak tersedia dalam data.

Contoh:

| Skenario | Urutan yang diasumsikan | Outcome |
|---|---|---|
| Worst-case | SL lebih dahulu | SL_HIT |
| Best-case | TP lebih dahulu | TP_HIT |

Hasil tersebut harus tetap diberi penanda bahwa event bersifat ambigu. Worst-case dan best-case bukan dua fakta yang sama-sama benar-benar terjadi. Keduanya adalah batas skenario yang mungkin berdasarkan keterbatasan data.

---

## 14.6. Worst-Case dan Best-Case

Worst-case dan best-case digunakan untuk menghadapi ketidakpastian urutan kejadian yang tidak dapat diselesaikan dari resolusi data yang tersedia.

### Worst-Case sebagai Skenario Konservatif

Worst-case menggambarkan hasil paling buruk yang masih konsisten dengan informasi yang tersedia.

Dalam kasus TP dan SL tersentuh pada bar yang sama, worst-case untuk posisi long biasanya menganggap SL terjadi lebih dahulu jika tidak ada informasi tambahan yang dapat membuktikan sebaliknya.

Tujuannya bukan untuk menyatakan bahwa SL pasti terjadi lebih dahulu. Tujuannya adalah menguji apakah kesimpulan masih bertahan dalam skenario yang merugikan.

### Best-Case sebagai Skenario Terbaik yang Masih Mungkin

Best-case menggambarkan hasil paling baik yang masih mungkin berdasarkan data.

Dalam contoh yang sama, best-case dapat menganggap TP terjadi lebih dahulu.

Namun, best-case juga bukan bukti bahwa TP benar-benar terjadi lebih dahulu. Ia hanya menunjukkan batas atas hasil yang mungkin.

### Mengapa Keduanya Perlu Dilaporkan?

Pelaporan dua skenario membantu menjawab pertanyaan penting:

> "Apakah dugaan edge tetap terlihat jika ketidakpastian intrabar diperlakukan secara konservatif?"

Misalnya:

- Jika edge hanya muncul pada best-case tetapi hilang pada worst-case, hasilnya belum robust.
- Jika edge tetap terlihat pada worst-case dan best-case, bukti lebih tahan terhadap ambiguitas.
- Jika hasil berada di antara keduanya, pembaca dapat memahami rentang ketidakpastian.

Pendekatan ini lebih jujur daripada memilih satu skenario secara diam-diam.

### Worst-Case dan Best-Case Tidak Boleh Dicampur Silang

Dalam perbandingan B1 dan B0, skenario harus diperlakukan secara konsisten.

Tidak boleh:

- B1 dinilai dengan best-case.
- B0 dinilai dengan worst-case.
- Kemudian perbedaannya disebut sebagai information edge.

Perlakuan tersebut akan membuat B1 memperoleh keuntungan evaluasi yang tidak diberikan kepada B0.

Karena itu, perbandingan harus dilakukan dengan pasangan skenario yang sepadan:

- B1 worst-case dibandingkan B0 worst-case.
- B1 best-case dibandingkan B0 best-case.

Jika analisis menggunakan hasil worst-case untuk menguji ketahanan edge, maka aturan worst-case harus diterapkan kepada kedua kelompok.

Demikian juga, hasil best-case harus dilaporkan sebagai batas kemungkinan, bukan sebagai hasil utama yang dipilih karena paling menarik.

---

## 14.7. TIMEOUT Bukan Data Habis

Dalam evaluasi trading, istilah **TIMEOUT** dan **INSUFFICIENT_HORIZON** harus dibedakan dengan jelas. Keduanya sama-sama berkaitan dengan berakhirnya jendela pengamatan, tetapi maknanya berbeda.

### TIMEOUT

TIMEOUT berarti:

> Trade telah mencapai batas waktu evaluasi yang ditetapkan, dan tidak ada SL atau TP yang tersentuh sebelum batas tersebut.

Contoh:

- Maximum hold ditetapkan lima bar.
- Lima bar lengkap tersedia.
- Tidak ada SL atau TP yang tercapai.
- Trade ditutup berdasarkan aturan TIMEOUT.

TIMEOUT adalah outcome evaluasi yang sah. Ia bukan kegagalan data.

### INSUFFICIENT_HORIZON

INSUFFICIENT_HORIZON berarti:

> Data yang tersedia tidak cukup untuk menyelesaikan horizon atau jendela evaluasi yang diwajibkan.

Contoh:

- Event terjadi dua bar sebelum akhir dataset.
- Penelitian membutuhkan lima bar evaluasi.
- Hanya tersedia dua bar.

Kita tidak dapat mengetahui apakah SL atau TP akan tersentuh pada tiga bar berikutnya.

Dalam kondisi ini, trade tidak boleh dipaksa menjadi TIMEOUT. Jika data belum cukup, statusnya adalah INSUFFICIENT_HORIZON atau status kelengkapan data yang sesuai protokol.

### Mengapa Perbedaan Ini Penting?

Jika data yang terpotong dianggap TIMEOUT, hasil penelitian dapat menjadi bias. Event-event yang terjadi dekat akhir dataset mungkin terlihat seolah-olah tidak mencapai target atau stop, padahal periode pengamatannya belum selesai.

Perbedaan ini juga penting untuk:

- Menentukan event mana yang masuk agregasi.
- Menghitung jumlah sampel yang layak.
- Menjaga kesetaraan B1 dan B0.
- Membedakan hasil ekonomi dari masalah kelengkapan data.
- Menyusun audit trail.

Dengan demikian:

- **TIMEOUT** berarti trade selesai secara sah karena batas waktu.
- **INSUFFICIENT_HORIZON** berarti evaluasi tidak dapat diselesaikan karena data tidak mencukupi.

Keduanya tidak boleh dipertukarkan.

---

## 14.8. Biaya Transaksi

Dalam penelitian trading, biaya transaksi penting karena hasil kotor belum tentu sama dengan hasil bersih yang benar-benar diterima.

Biaya transaksi dapat mencakup:

- Komisi.
- Pajak atau pungutan.
- Spread.
- Slippage.
- Biaya lain yang relevan dengan pasar dan aturan eksekusi.

Namun, biaya transaksi harus ditempatkan pada bagian yang tepat dalam sistem evaluasi.

### Outcome dan Realized P&L Net adalah Dua Hal Berbeda

**Outcome** menunjukkan apa yang terjadi terhadap level evaluasi:

- Apakah TP tersentuh?
- Apakah SL tersentuh?
- Apakah trade TIMEOUT?
- Apakah terjadi ambiguitas?

Outcome ditentukan berdasarkan pergerakan harga dan aturan level yang telah ditetapkan.

Sementara itu, **realized P&L net** menunjukkan hasil ekonomi setelah biaya transaksi diperhitungkan.

Contohnya, sebuah trade dapat memiliki outcome TP_HIT, tetapi setelah komisi dan slippage, keuntungan bersihnya lebih kecil daripada keuntungan kotor.

Sebaliknya, trade yang secara kotor hanya menghasilkan keuntungan kecil dapat menjadi tidak menguntungkan setelah biaya.

### Mengapa Biaya Tidak Boleh Diam-Diam Mengubah Outcome?

Bayangkan sebuah kandidat memiliki:

- Entry dan TP yang secara harga memenuhi aturan.
- Namun, setelah biaya transaksi, hasil bersihnya negatif.

Dalam kondisi ini, outcome berdasarkan level tetap dapat dicatat sebagai TP_HIT, sedangkan realized P&L net dicatat sebagai hasil bersih setelah biaya.

Jika biaya diam-diam mengubah TP_HIT menjadi SL_HIT, definisi outcome menjadi tidak konsisten. Mesin tidak lagi membedakan antara:

- Apa yang terjadi pada jalur harga.
- Apa hasil ekonomi setelah biaya.

Keduanya penting, tetapi tidak sama.

### Gross Outcome dan Net Realized Result

TEKB perlu membedakan setidaknya dua lapisan:

| Lapisan | Pertanyaan yang dijawab |
|---|---|
| Gross outcome | Apakah harga mencapai SL, TP, atau TIMEOUT berdasarkan aturan level? |
| Gross P&L | Berapa hasil sebelum biaya transaksi? |
| Net realized P&L | Berapa hasil setelah biaya, spread, dan slippage yang dimodelkan? |

Pemisahan ini membuat penelitian lebih transparan.

Misalnya:

- Outcome: TP_HIT.
- Gross P&L: +2,0 × ATR.
- Total biaya: 0,3 × ATR.
- Net realized P&L: +1,7 × ATR.

Angka tersebut menunjukkan bahwa target harga tercapai, tetapi hasil ekonomi bersih lebih kecil.

Biaya juga dapat digunakan dalam analisis kelayakan. Sebuah edge yang tampak positif secara gross tetapi hilang setelah biaya mungkin tidak layak secara praktis. Namun, biaya tidak boleh dimasukkan secara sembunyi-sembunyi ke dalam definisi outcome.

---

## Penutup Bab

Evaluation Engine adalah komponen yang memastikan bahwa penelitian TEKB tidak bergantung pada tafsir manual atau perlakuan yang berubah-ubah.

Mesin ini bertindak seperti wasit:

- Menggunakan aturan yang sama.
- Memeriksa jendela evaluasi yang sama.
- Menentukan TP, SL, dan TIMEOUT.
- Menangani gap-through.
- Mencatat ambiguitas intrabar.
- Melaporkan worst-case dan best-case.
- Membedakan TIMEOUT dari INSUFFICIENT_HORIZON.
- Memisahkan outcome harga dari realized P&L net.

Tanpa Evaluation Engine yang deterministik, hasil penelitian dapat berubah bukan karena data berubah, melainkan karena cara penilaian berubah.

Dengan Evaluation Engine, TEKB dapat memastikan bahwa B1 dan B0 dinilai secara adil, kandidat tidak diperlakukan secara istimewa, dan setiap hasil dapat ditelusuri kembali ke aturan yang digunakan.

---

## Ringkasan Bab

- Evaluation Engine adalah mesin evaluasi deterministik yang bertindak seperti wasit.
- Tugasnya bukan meramal atau memilih hasil terbaik, melainkan menjalankan aturan yang sama.
- Mesin menentukan TP_HIT, SL_HIT, TIMEOUT, harga keluar, durasi, dan status evaluasi.
- Evaluasi harus dimulai dan diakhiri berdasarkan jendela yang telah ditetapkan.
- Gap-through harus diperlakukan secara eksplisit, dengan exit pada Open ketika harga langsung melewati level.
- Jika TP dan SL tersentuh pada bar yang sama, urutan tidak boleh ditebak dari data OHLCV yang tidak memadai.
- AMBIGUOUS_INTRABAR dapat dilaporkan melalui skenario worst-case dan best-case.
- Worst-case dan best-case harus diterapkan secara konsisten kepada B1 dan B0.
- TIMEOUT berarti trade selesai karena batas waktu, sedangkan INSUFFICIENT_HORIZON berarti data tidak cukup.
- Outcome harga harus dipisahkan dari realized P&L net setelah biaya transaksi.
- Konsistensi evaluasi merupakan syarat penting agar perbandingan dan kesimpulan TEKB dapat dipercaya.

---

## Pertanyaan Refleksi

1. Mengapa evaluasi manual dapat menghasilkan bias?
2. Mengapa B1 dan B0 harus dinilai dengan Evaluation Engine yang sama?
3. Apa perbedaan antara entry, horizon, dan maximum hold?
4. Mengapa gap-through tidak boleh selalu dipaksakan keluar tepat pada level SL atau TP?
5. Apa yang dimaksud dengan AMBIGUOUS_INTRABAR?
6. Mengapa peneliti tidak boleh menebak urutan TP dan SL ketika data tidak menyediakannya?
7. Mengapa worst-case dan best-case harus diterapkan secara konsisten?
8. Apa perbedaan TIMEOUT dan INSUFFICIENT_HORIZON?
9. Mengapa outcome harga harus dipisahkan dari realized P&L net?
10. Apa risiko jika biaya transaksi diam-diam mengubah definisi outcome?

---

## Kalimat Kunci

> Evaluation Engine bukan mesin yang mencari hasil terbaik, melainkan wasit yang memastikan semua event dinilai dengan aturan yang sama.

---

<div align="center">

[← Bab Sebelumnya](/posts/bab-13-empiris-dan-stokastik/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Bab Selanjutnya →](/posts/bab-15-hasil-jadi-angka/)

</div>