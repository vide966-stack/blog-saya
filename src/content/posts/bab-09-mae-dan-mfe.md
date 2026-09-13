---
title: "BAB 9 — MAE dan MFE: Mengukur Apa yang Sebenarnya Terjadi Setelah Entry"
published: 2026-09-12
description: "MAE dan MFE mengukur perjalanan harga setelah entry — bukan hanya hasil akhir. Bab ini menjelaskan cara mengukur tekanan dan potensi gerakan yang sempat terjadi."
tags: ["bab-9", "mae", "mfe", "pengukuran"]
category: "Bab"
draft: false
lang: ""
---

**BAGIAN III — MENGUKUR HASIL TANPA MENIPU DIRI SENDIRI**

---

## Tujuan Bab

Bab ini menjelaskan bagaimana TEKB mengukur perjalanan harga setelah entry sebelum berbicara tentang strategi profit, stop-loss, take-profit, atau seleksi kandidat.

Harga tidak bergerak secara lurus dari titik entry menuju hasil akhir. Setelah entry, harga dapat naik, turun, bergerak menyamping, mengalami lonjakan, atau berbalik arah. Karena itu, return akhir saja tidak cukup untuk menggambarkan pengalaman dan risiko sebuah posisi.

TEKB menggunakan dua ukuran penting:

- **MFE — Maximum Favorable Excursion**, yaitu seberapa jauh harga sempat bergerak ke arah yang menguntungkan.
- **MAE — Maximum Adverse Excursion**, yaitu seberapa jauh harga sempat bergerak melawan posisi.

Dengan MAE dan MFE, TEKB tidak hanya bertanya:

> "Berapa return pada akhir pengamatan?"

TEKB juga bertanya:

> "Seberapa jauh harga sempat bergerak menguntungkan?"

> "Seberapa besar tekanan yang sempat dialami?"

> "Apakah hasil akhir yang positif dicapai melalui perjalanan yang tenang atau melalui penurunan yang dalam?"

MAE dan MFE merupakan alat pengukuran. Keduanya belum otomatis membuktikan bahwa suatu strategi profit atau aturan exit layak digunakan.

---

## 9.1. Mengapa Harga Penutupan Saja Tidak Cukup?

Salah satu cara paling sederhana untuk mengukur hasil adalah membandingkan harga entry dengan harga penutupan pada akhir horizon.

Misalnya:

- Harga entry: Rp1.000
- Harga penutupan tiga bar kemudian: Rp1.050

Return akhirnya:

> R = (1.050 − 1.000) ÷ 1.000 = 5%

Angka tersebut benar, tetapi belum menggambarkan seluruh perjalanan harga.

### Harga bisa naik tinggi lalu turun

Perhatikan contoh berikut:

| Tahap | Harga |
|---|---|
| Entry | Rp1.000 |
| High tertinggi selama pengamatan | Rp1.150 |
| Low terendah selama pengamatan | Rp990 |
| Close akhir | Rp1.050 |

Pada akhir horizon, return adalah +5%. Namun, harga sempat naik hingga Rp1.150 atau +15%.

Jika seseorang hanya melihat close akhir, potensi gerakan naik sebesar +15% tersebut tidak terlihat.

Informasi ini penting untuk penelitian exit. Mungkin harga sempat memberikan peluang untuk mengambil profit lebih awal, meskipun akhirnya hanya ditutup dengan return +5%.

### Harga bisa turun dahulu lalu pulih

Sekarang perhatikan contoh lain:

| Tahap | Harga |
|---|---|
| Entry | Rp1.000 |
| Low terendah selama pengamatan | Rp900 |
| High tertinggi selama pengamatan | Rp1.080 |
| Close akhir | Rp1.050 |

Return akhirnya tetap +5%. Namun, harga sempat turun hingga Rp900 atau -10%.

Bagi pemegang posisi long, perjalanan ini dapat menimbulkan tekanan besar. Trader mungkin:

- meragukan sinyal;
- keluar sebelum harga pulih;
- terkena stop-loss;
- membutuhkan modal tambahan;
- atau tidak sanggup mempertahankan posisi.

Dua contoh tersebut sama-sama berakhir pada return +5%, tetapi profil perjalanannya berbeda.

### Close-to-close menyembunyikan perjalanan intraperiode

Harga penutupan hanya menunjukkan posisi harga pada akhir periode. Ia tidak selalu menunjukkan:

- high tertinggi yang sempat dicapai;
- low terendah yang sempat terjadi;
- tekanan sementara;
- peluang profit yang tersedia;
- kemungkinan stop-loss tersentuh;
- atau urutan pergerakan harga di dalam periode.

Karena itu, close-to-close tidak boleh menjadi satu-satunya ukuran.

Dalam TEKB, return akhir tetap berguna, tetapi perlu dilengkapi dengan pengukuran MAE dan MFE.

### Risiko intraperiode dapat hilang jika hanya melihat close

Bayangkan sebuah posisi:

- Entry pada Rp1.000;
- Harga turun ke Rp850;
- Harga kemudian pulih;
- Close pada Rp1.020.

Jika hanya melihat close, hasilnya tampak seperti profit +2%. Namun, selama perjalanan harga, posisi tersebut sempat mengalami penurunan -15%.

Penurunan sementara tersebut mungkin lebih penting bagi pengelolaan risiko daripada return akhir +2%.

Inilah alasan TEKB mengukur perjalanan harga, bukan hanya titik akhirnya.

---

## 9.2. Apa Itu MFE?

**MFE** adalah singkatan dari **Maximum Favorable Excursion**.

Dalam bahasa sederhana, MFE berarti:

> Seberapa jauh harga sempat bergerak ke arah yang menguntungkan posisi selama horizon pengukuran.

Untuk posisi long, gerakan yang menguntungkan adalah gerakan naik. Karena itu, MFE long menggunakan high tertinggi selama periode pengamatan.

### Contoh sederhana

Misalkan:

- Harga entry: Rp1.000;
- High tertinggi selama horizon: Rp1.120.

Maka:

> MFE_raw = 1.120 − 1.000 = 120

MFE mentah adalah Rp120.

Dalam bentuk persentase:

> MFE_% = (1.120 − 1.000) ÷ 1.000 × 100%

> MFE_% = 12%

Artinya, selama horizon pengamatan, harga sempat bergerak 12% ke arah yang menguntungkan.

### MFE mengukur peluang gerakan yang tersedia

MFE dapat dipahami sebagai ukuran potensi gerakan favorable yang sempat tersedia setelah entry.

Misalnya:

- Entry: Rp1.000;
- High maksimum: Rp1.150;
- Close akhir: Rp1.030.

Maka:

- MFE = +15%;
- Return akhir = +3%.

Harga sempat memberikan peluang gerakan +15%, tetapi hasil akhir hanya +3%.

Namun, MFE tidak berarti trader benar-benar mendapatkan profit +15%. Untuk merealisasikan keuntungan tersebut, trader harus memiliki aturan exit yang mampu menangkap gerakan itu.

### MFE bukan realized profit

MFE berbeda dari profit yang benar-benar direalisasikan.

MFE menjawab:

> "Seberapa jauh harga sempat bergerak menguntungkan?"

Realized profit menjawab:

> "Berapa keuntungan yang benar-benar diperoleh setelah posisi ditutup dan biaya diperhitungkan?"

Harga bisa mencapai MFE tinggi, tetapi trader mungkin:

- tidak menjual pada titik tersebut;
- menjual terlalu cepat;
- terkena pembalikan harga;
- atau tidak memiliki aturan exit untuk menangkapnya.

Karena itu, MFE tidak boleh langsung disebut sebagai profit aktual.

### Kegunaan MFE dalam TEKB

MFE dapat digunakan untuk mempelajari:

- Seberapa sering harga bergerak ke arah yang diharapkan setelah event.
- Seberapa besar gerakan favorable yang umum terjadi.
- Apakah target profit tertentu memiliki dasar empiris.
- Apakah target yang terlalu jauh jarang tercapai.
- Apakah peluang favorable muncul pada bar awal atau bar akhir.
- Apakah MFE B1 berbeda dari MFE B0.
- Apakah suatu hipotesis exit layak diuji lebih lanjut.

MFE membantu membentuk hipotesis. MFE belum menjadi bukti bahwa suatu target profit pasti menguntungkan.

---

## 9.3. Apa Itu MAE?

**MAE** adalah singkatan dari **Maximum Adverse Excursion**.

Dalam bahasa sederhana, MAE berarti:

> Seberapa jauh harga sempat bergerak melawan posisi selama horizon pengukuran.

Untuk posisi long, gerakan yang merugikan adalah gerakan turun. Karena itu, MAE long menggunakan low terendah selama periode pengamatan.

### Contoh sederhana

Misalkan:

- Harga entry: Rp1.000;
- Low terendah selama horizon: Rp920.

Maka:

> MAE_raw = 920 − 1.000 = −80

MAE mentah adalah -Rp80.

Dalam bentuk persentase:

> MAE_% = (920 − 1.000) ÷ 1.000 × 100%

> MAE_% = −8%

Artinya, harga sempat bergerak 8% melawan posisi long.

Dalam TEKB, MAE dapat disimpan sebagai angka negatif agar arah pergerakannya terlihat jelas.

### MAE mengukur tekanan yang dialami posisi

MAE bukan hanya angka kerugian akhir. MAE mengukur tekanan maksimum yang sempat dialami selama periode pengamatan.

Contoh:

- Entry: Rp1.000;
- Low minimum: Rp900;
- High maksimum: Rp1.150;
- Close akhir: Rp1.080.

Maka:

- MAE = -10%;
- MFE = +15%;
- Return akhir = +8%.

Posisi tersebut akhirnya menghasilkan profit, tetapi sebelumnya sempat turun 10%.

Ini menunjukkan bahwa:

> Posisi yang akhirnya profit tetap dapat mengalami tekanan besar.

### Mengapa MAE penting?

MAE membantu penelitian memahami:

- seberapa dalam retracement yang umum terjadi;
- seberapa besar risiko sementara setelah entry;
- apakah entry terlalu cepat;
- apakah sinyal membutuhkan ruang risiko yang lebar;
- apakah stop-loss tertentu terlalu sempit;
- apakah profit akhir dicapai dengan tekanan yang besar;
- apakah B1 memiliki tekanan yang berbeda dari B0.

MAE juga dapat membantu membedakan dua event yang memiliki return akhir sama.

| Event | Return akhir | MAE |
|---|---|---|
| A | +5% | -1% |
| B | +5% | -12% |

Kedua event sama-sama menghasilkan return akhir +5%, tetapi Event B mengalami tekanan jauh lebih besar.

Dari sudut pandang risiko, keduanya tidak sama.

### MAE bukan realized loss

MAE tidak selalu sama dengan kerugian yang benar-benar direalisasikan.

Jika harga sempat turun 10% tetapi kemudian naik dan posisi ditutup dengan profit, maka:

- MAE = -10%;
- realized result dapat tetap positif.

Sebaliknya, suatu posisi dapat mengalami MAE kecil tetapi tetap berakhir rugi karena harga kemudian turun setelah periode pengukuran atau karena aturan exit tertentu.

Karena itu, MAE adalah ukuran perjalanan harga, bukan pengganti laporan hasil transaksi.

---

## 9.4. Rumus MAE/MFE dengan Bahasa Awam

MAE dan MFE dimulai dari satu titik yang sama, yaitu harga entry.

Harga entry menjadi titik referensi untuk mengukur seberapa jauh harga bergerak naik atau turun selama horizon.

Dalam kontrak TEKB, entry standar menggunakan:

> NEXT_VALID_BAR_OPEN

Artinya, sinyal muncul pada bar T, kemudian entry dilakukan pada open bar valid berikutnya.

### 9.4.1. Entry sebagai titik awal

Misalnya:

- Sinyal terdeteksi pada bar T;
- Entry dilakukan pada open bar T+1;
- Harga entry = Rp1.000.

Maka semua pengukuran MAE dan MFE dimulai dari Rp1.000.

Harga entry harus dibedakan dari:

- close bar sinyal;
- harga entry teoritis;
- harga open bar berikutnya;
- harga eksekusi aktual;
- harga setelah biaya dan slippage.

Untuk pengukuran penelitian, harga entry harus mengikuti definisi yang telah dibekukan.

### 9.4.2. Rumus MFE untuk posisi long

Untuk posisi long:

> MFE_raw = H_max − P_entry

Keterangan:

- H_max = high tertinggi selama horizon;
- P_entry = harga entry.

Contoh:

- Harga entry = Rp1.000;
- High maksimum = Rp1.150.

> MFE_raw = 1.150 − 1.000 = 150

MFE mentah = Rp150.

Dalam bentuk persentase:

> MFE_% = (H_max − P_entry) ÷ P_entry × 100%

> MFE_% = 150 ÷ 1.000 × 100% = 15%

### 9.4.3. Rumus MAE untuk posisi long

Untuk posisi long:

> MAE_raw = L_min − P_entry

Keterangan:

- L_min = low terendah selama horizon;
- P_entry = harga entry.

Contoh:

- Harga entry = Rp1.000;
- Low minimum = Rp920.

> MAE_raw = 920 − 1.000 = −80

MAE mentah = -Rp80.

Dalam bentuk persentase:

> MAE_% = (L_min − P_entry) ÷ P_entry × 100%

> MAE_% = −80 ÷ 1.000 × 100% = −8%

### 9.4.4. Ringkasan rumus untuk posisi long

| Ukuran | Rumus | Makna |
|---|---|---|
| MFE raw | H_max − P_entry | Gerakan maksimum yang menguntungkan |
| MAE raw | L_min − P_entry | Gerakan maksimum yang melawan posisi |
| MFE % | (H_max − P_entry) / P_entry | Potensi favorable dalam persentase |
| MAE % | (L_min − P_entry) / P_entry | Tekanan adverse dalam persentase |

Untuk posisi short, arah pengukuran harus disesuaikan. Bab ini menggunakan posisi long sebagai contoh utama agar konsep dasar mudah dipahami.

### 9.4.5. Harga mentah dan hasil yang dinormalisasi

MAE dan MFE dapat dinyatakan dalam beberapa bentuk:

- Harga mentah;
- Persentase terhadap harga entry;
- Satuan ATR;
- Satuan risiko tertentu.

#### A. Harga mentah

Contoh:

- MAE = -Rp80;
- MFE = +Rp150.

Harga mentah mudah dipahami, tetapi kurang cocok untuk membandingkan instrumen dengan skala harga yang berbeda.

MAE -Rp80 pada saham seharga Rp1.000 memiliki makna berbeda dari MAE -Rp80 pada saham seharga Rp10.000.

#### B. Persentase

Contoh:

- MAE = -8%;
- MFE = +15%.

Persentase membantu membandingkan instrumen dengan harga berbeda. Namun, persentase belum tentu menggambarkan volatilitas khas setiap instrumen.

#### C. Normalisasi menggunakan ATR

ATR dapat digunakan untuk menyatakan MAE dan MFE dalam satuan volatilitas.

Misalnya:

- MAE raw = -Rp80;
- MFE raw = +Rp150;
- ATR pada entry = Rp40.

Maka:

> MAE_ATR = −80 ÷ 40 = −2,0

> MFE_ATR = 150 ÷ 40 = 3,75

Interpretasinya:

- harga sempat bergerak melawan posisi sebesar 2 ATR;
- harga sempat bergerak menguntungkan sebesar 3,75 ATR.

Normalisasi ini membantu menjawab:

> "Seberapa besar gerakan tersebut dibandingkan dengan volatilitas instrumen pada saat entry?"

Namun, ATR harus dihitung secara kausal. ATR entry tidak boleh menggunakan data setelah keputusan entry. Definisi ATR, periode ATR, dan waktu ketersediaannya harus ditetapkan sebelum penelitian.

---

## 9.5. Horizon R1, R3, R5, dan R10

MAE dan MFE selalu bergantung pada horizon pengukuran.

Horizon adalah jumlah bar setelah entry yang diamati untuk menghitung perjalanan harga.

Dalam TEKB, contoh label horizon dapat berupa:

- R1 = satu bar;
- R3 = tiga bar;
- R5 = lima bar;
- R10 = sepuluh bar.

Label tersebut harus memiliki definisi teknis yang jelas dalam kontrak penelitian.

### 9.5.1. Arti satu, tiga, lima, atau sepuluh bar

Misalnya:

- Sinyal muncul pada bar T;
- Entry dilakukan pada open bar T+1.

Jika pengukuran dimulai dari bar entry, maka:

| Horizon | Jendela pengamatan |
|---|---|
| R1 | Satu bar setelah entry |
| R3 | Tiga bar setelah entry |
| R5 | Lima bar setelah entry |
| R10 | Sepuluh bar setelah entry |

Yang paling penting bukan nama R1 atau R3, melainkan definisi yang konsisten mengenai:

- kapan pengukuran dimulai;
- bar mana yang termasuk;
- kapan pengukuran berakhir;
- bagaimana bar yang tidak lengkap diperlakukan.

### 9.5.2. Mengapa horizon pengukuran harus tetap?

Event yang diamati lebih lama akan memiliki lebih banyak kesempatan untuk:

- mencapai high yang lebih tinggi;
- mencapai low yang lebih rendah;
- menghasilkan MFE yang lebih besar;
- mengalami MAE yang lebih besar.

Karena itu, event yang diukur selama tiga bar tidak boleh dibandingkan secara langsung dengan event yang diukur selama sepuluh bar tanpa penjelasan dan penyesuaian.

Contoh kontrak yang jelas:

> Penelitian utama menggunakan horizon R3, yaitu tiga bar setelah entry. Horizon R1, R5, dan R10 digunakan sebagai analisis tambahan yang telah ditentukan sebelum evaluasi hasil.

Dengan cara ini, setiap hasil dapat ditafsirkan sesuai jendela pengukurannya.

### 9.5.3. Horizon berbeda dari durasi trade

Horizon pengukuran bukan hal yang sama dengan durasi trade aktual.

Horizon pengukuran adalah jendela standar untuk mengamati perilaku harga.

Durasi trade adalah berapa lama posisi benar-benar ditahan berdasarkan aturan exit.

Contoh:

- Horizon penelitian: R3;
- Posisi terkena stop-loss pada bar kedua;
- Atau posisi mencapai take-profit pada bar pertama;
- Atau posisi masih terbuka ketika horizon berakhir.

MAE/MFE dapat digunakan untuk mengukur perjalanan harga dalam jendela standar. Sementara itu, evaluation engine digunakan untuk menguji hasil dari aturan exit tertentu.

Pemisahan ini penting agar penelitian tidak mencampurkan:

- pengukuran perilaku harga;
- simulasi aturan exit;
- hasil transaksi setelah biaya.

### 9.5.4. Horizon harus identik antara B1 dan B0

Jika B1 diukur menggunakan R3, B0 juga harus diukur menggunakan R3.

Tidak boleh:

- B1 menggunakan tiga bar;
- B0 menggunakan lima bar;
- lalu keduanya dibandingkan sebagai pasangan.

Perbedaan horizon dapat menciptakan perbedaan hasil yang sebenarnya berasal dari cara pengukuran, bukan dari event yang sedang diuji.

Karena itu, B1 dan B0 harus menggunakan:

- definisi entry yang sama;
- horizon yang sama;
- rumus MAE/MFE yang sama;
- aturan validasi yang sama;
- evaluation engine yang sama jika dilakukan simulasi exit.

Dengan demikian, perbedaan hasil lebih layak diteliti sebagai kemungkinan information edge, bukan sebagai akibat dari prosedur yang tidak seimbang.

---

## 9.6. Mengapa Biaya Transaksi Tidak Masuk MAE/MFE?

MAE dan MFE dasar dirancang untuk mengukur pergerakan harga mentah setelah entry.

Karena itu, biaya transaksi tidak dimasukkan langsung ke dalam rumus dasar MAE/MFE.

Biaya transaksi dapat mencakup:

- komisi;
- pajak;
- spread;
- slippage;
- biaya bursa;
- biaya lain yang relevan dengan instrumen.

### 9.6.1. Measurement dan realized result adalah dua hal berbeda

MAE/MFE menjawab:

> "Seberapa jauh harga bergerak setelah entry?"

Sementara realized result menjawab:

> "Berapa hasil yang benar-benar diperoleh setelah aturan exit dan biaya diterapkan?"

Keduanya berhubungan, tetapi tidak identik.

Contoh:

- Entry = Rp1.000;
- High maksimum = Rp1.100;
- Low minimum = Rp960;
- Close akhir = Rp1.050;
- Biaya transaksi total = 0,5%.

Maka:

- MFE raw = +Rp100;
- MAE raw = -Rp40;
- return harga akhir = +5%;
- hasil bersih aktual bergantung pada aturan entry, aturan exit, dan biaya.

Biaya tidak mengubah fakta bahwa harga sempat mencapai Rp1.100 atau turun ke Rp960. Fakta tersebut merupakan pengukuran perjalanan harga mentah.

### 9.6.2. Mengapa biaya dilaporkan terpisah?

Pemisahan MAE/MFE dan biaya memiliki beberapa manfaat.

#### 1. Definisi pengukuran tetap jelas

MAE/MFE tetap menggambarkan gerakan harga, bukan gabungan antara harga dan asumsi biaya.

#### 2. Skenario biaya dapat diuji terpisah

Peneliti dapat menguji beberapa tingkat friction tanpa mengubah data dasar MAE/MFE.

#### 3. Risiko harga tidak tercampur dengan biaya

Gerakan harga dan biaya eksekusi merupakan dua komponen berbeda yang perlu dilaporkan secara terpisah.

#### 4. Audit menjadi lebih mudah

Orang lain dapat memeriksa apakah suatu angka berasal dari harga pasar atau dari asumsi biaya.

#### 5. Satu pengukuran dapat digunakan untuk beberapa hipotesis exit

Distribusi MAE/MFE dapat menjadi dasar untuk menguji berbagai kandidat stop-loss dan take-profit melalui evaluation engine.

### 9.6.3. MAE/MFE bukan pengganti realized P&L

MAE dan MFE tidak boleh dianggap sebagai:

- laporan profit bersih;
- hasil strategi;
- bukti bahwa target profit tercapai;
- bukti bahwa stop-loss tertentu menguntungkan;
- bukti bahwa suatu sinyal layak diperdagangkan.

MAE/MFE merupakan lapisan pengukuran perilaku harga. Setelah itu, TEKB masih memerlukan evaluation engine untuk menguji aturan exit, biaya, slippage, dan friction secara eksplisit.

---

## 9.7. Status Pengukuran

Tidak semua event dapat menghasilkan angka MAE/MFE yang lengkap dan sah.

Data dapat berhenti sebelum horizon selesai. Harga dapat rusak atau tidak valid. Timestamp dapat bermasalah. Event dapat melanggar aturan validasi. Karena itu, TEKB menggunakan status pengukuran yang eksplisit.

Status ini penting karena menjelaskan apakah suatu angka:

- lengkap;
- tidak lengkap;
- atau tidak sah.

Status bukan sekadar label teknis. Status merupakan bagian dari audit trail penelitian.

### 9.7.1. COMPUTED_FULL_HORIZON

Status ini berarti:

- entry valid;
- seluruh bar yang diperlukan tersedia;
- high dan low selama horizon dapat dihitung;
- MAE/MFE berhasil dihitung sesuai definisi;
- tidak ada pelanggaran validasi yang membuat pengukuran tidak sah.

Contoh:

- Entry tersedia;
- Horizon R3 membutuhkan tiga bar;
- Ketiga bar tersedia;
- OHLC valid;
- MAE dan MFE berhasil dihitung.

Maka statusnya:

> COMPUTED_FULL_HORIZON

Event dengan status ini dapat digunakan dalam analisis MAE/MFE sesuai aturan penelitian.

### 9.7.2. INSUFFICIENT_HORIZON

Status ini berarti data tidak cukup untuk menyelesaikan horizon yang telah ditentukan.

Contoh:

- Event muncul menjelang akhir dataset;
- Entry tersedia;
- Penelitian membutuhkan R3;
- Namun, hanya satu bar setelah entry yang tersedia.

Maka statusnya:

> INSUFFICIENT_HORIZON

Event tersebut tetap dapat disimpan dalam audit trail, tetapi tidak boleh diperlakukan sebagai observasi R3 yang lengkap.

Peneliti tidak boleh mengisi dua bar yang hilang dengan asumsi, harga terakhir, atau angka buatan tanpa kontrak khusus yang telah ditentukan sebelumnya.

### 9.7.3. INVALIDATED

Status ini berarti event atau pengukurannya dinyatakan tidak sah berdasarkan aturan validasi penelitian.

Contoh penyebab:

- harga entry tidak valid;
- OHLC tidak memenuhi aturan integritas;
- timestamp bertentangan;
- event melanggar aturan causal availability;
- terdapat duplikasi yang tidak dapat diselesaikan;
- definisi event ternyata tidak terpenuhi;
- data mengalami kerusakan yang membuat pengukuran tidak dapat dipercaya.

Statusnya:

> INVALIDATED

Status ini berbeda dari INSUFFICIENT_HORIZON.

| Status | Makna |
|---|---|
| COMPUTED_FULL_HORIZON | Pengukuran lengkap dan valid |
| INSUFFICIENT_HORIZON | Data tidak cukup untuk menyelesaikan horizon |
| INVALIDATED | Event atau data tidak sah menurut aturan validasi |

### 9.7.4. Mengapa data tidak lengkap tidak boleh dipaksa menjadi angka lengkap?

Salah satu kesalahan penelitian adalah memperlakukan data yang diamati hanya satu bar sebagai data yang diamati tiga bar.

Misalnya, penelitian membutuhkan R3, tetapi event hanya memiliki satu bar setelah entry. Jika MAE/MFE dihitung dari satu bar tersebut lalu digabungkan dengan observasi R3 lengkap, hasilnya dapat bias.

Event dengan jendela satu bar memiliki lebih sedikit kesempatan untuk:

- mencapai MFE tinggi;
- mengalami MAE besar;
- menyentuh target;
- mengalami pembalikan.

Akibatnya, event yang tidak lengkap tidak sebanding dengan event yang memiliki horizon penuh.

Prinsip TEKB adalah:

> Data yang tidak lengkap harus diberi status yang benar, bukan dipaksa menjadi angka yang tampak lengkap.

### 9.7.5. Contoh tabel status pengukuran

| Event ID | Entry | Horizon | Status | MAE | MFE |
|---|---|---|---|---|---|
| E001 | Valid | R3 | COMPUTED_FULL_HORIZON | -1,2% | +3,5% |
| E002 | Valid | R3 | COMPUTED_FULL_HORIZON | -0,8% | +2,1% |
| E003 | Valid | R3 | INSUFFICIENT_HORIZON | — | — |
| E004 | Tidak valid | R3 | INVALIDATED | — | — |

Tanda — menunjukkan bahwa angka tidak tersedia atau tidak boleh digunakan sebagai hasil pengukuran lengkap.

### 9.7.6. Status harus dipertahankan dalam audit trail

Status pengukuran tidak boleh dihapus setelah proses analisis selesai.

Audit trail sebaiknya menyimpan:

- Event ID;
- instrumen;
- timestamp;
- entry price;
- horizon;
- status pengukuran;
- alasan status;
- MAE/MFE jika tersedia;
- versi definisi MAE/MFE;
- versi data;
- versi pipeline;
- informasi validasi yang relevan.

Dengan demikian, peneliti dapat menjawab:

> "Mengapa event ini tidak masuk distribusi?"

> "Apakah event ini tidak memiliki data yang cukup?"

> "Apakah event ini invalid?"

> "Apakah event ini dikeluarkan karena aturan yang telah ditentukan?"

Jawabannya harus dapat ditemukan dari catatan penelitian, bukan dibuat setelah melihat hasil.

---

## Penutup Bab 9

MAE dan MFE membantu TEKB melihat sesuatu yang tidak terlihat dari return akhir saja.

- MFE mengukur seberapa jauh harga sempat bergerak menguntungkan.
- MAE mengukur seberapa jauh harga sempat bergerak melawan posisi.
- Horizon menentukan jendela pengukuran yang harus konsisten.
- Biaya transaksi dipisahkan karena MAE/MFE mengukur gerakan harga mentah.
- Status pengukuran menjaga agar data yang tidak lengkap atau tidak sah tidak dipaksa menjadi angka yang menyesatkan.

Dengan MAE dan MFE, penelitian tidak berhenti pada pertanyaan:

> "Apakah harga akhirnya naik?"

Penelitian dapat bergerak ke pertanyaan yang lebih berguna:

> "Bagaimana perjalanan harga setelah entry?"

> "Seberapa besar tekanan yang biasanya terjadi?"

> "Seberapa besar potensi gerakan yang tersedia?"

> "Apakah pola tersebut berbeda dari B0?"

> "Apakah hipotesis exit tertentu masuk akal untuk diuji?"

Namun, MAE dan MFE tetap merupakan alat pengukuran, bukan bukti otomatis bahwa strategi tertentu menguntungkan. Bukti mengenai strategi exit baru dapat dinilai setelah aturan exit, biaya, horizon, dan evaluation engine diuji secara terpisah serta dibandingkan dengan pembanding yang adil.

---

## Ringkasan Bab

- Harga penutupan saja tidak cukup untuk menggambarkan perjalanan harga setelah entry.
- MFE mengukur seberapa jauh harga sempat bergerak menguntungkan.
- MAE mengukur seberapa jauh harga sempat bergerak melawan posisi.
- MAE dan MFE bergantung pada horizon pengukuran yang harus konsisten.
- Biaya transaksi dipisahkan dari MAE/MFE karena keduanya mengukur hal yang berbeda.
- Status pengukuran (COMPUTED_FULL_HORIZON, INSUFFICIENT_HORIZON, INVALIDATED) menjaga integritas data.
- Data yang tidak lengkap tidak boleh dipaksa menjadi angka yang tampak lengkap.

---

## Pertanyaan Refleksi

1. Mengapa harga penutupan saja tidak cukup untuk menggambarkan perjalanan harga?
2. Apa yang dimaksud dengan MFE?
3. Apa yang dimaksud dengan MAE?
4. Mengapa horizon pengukuran harus konsisten antara B1 dan B0?
5. Mengapa biaya transaksi tidak dimasukkan ke dalam rumus dasar MAE/MFE?
6. Apa perbedaan antara COMPUTED_FULL_HORIZON dan INSUFFICIENT_HORIZON?
7. Mengapa data yang tidak lengkap tidak boleh dipaksa menjadi angka lengkap?
8. Mengapa status pengukuran harus dipertahankan dalam audit trail?

---

<div align="center">

[← Bab Sebelumnya](/posts/bab-08-b0-pembanding-adil/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Bab Selanjutnya →](/posts/bab-10-atr-penggaris-volatilitas/)

</div>