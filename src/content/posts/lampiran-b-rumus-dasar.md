---
title: "Lampiran B — Rumus Dasar TEKB"
published: 2026-09-12
description: "Ringkasan rumus-rumus dasar yang digunakan dalam penelitian TEKB: return, relative volume, ATR, MAE/MFE, R-unit, expectancy, dan perbedaan B1-B0."
tags: ["lampiran-b", "rumus", "referensi", "matematika"]
category: "Lampiran"
draft: false
lang: ""
---

Lampiran ini merangkum rumus-rumus dasar yang digunakan dalam penelitian TEKB. Rumus-rumus tersebut membantu mengubah data harga dan volume menjadi ukuran yang dapat dibandingkan, diuji, dan ditelusuri.

Rumus bukanlah kesimpulan penelitian. Rumus hanya alat untuk menghitung. Kesimpulan tetap bergantung pada definisi event, waktu ketersediaan data, aturan entry, horizon, pembanding B0, metode evaluasi, biaya, dan pengujian ketidakpastian.

Dalam seluruh rumus berikut, simbol dan periode pengukuran harus digunakan secara konsisten. Perubahan kecil pada definisi harga, waktu, atau denominator dapat mengubah hasil penelitian.

---

## B.1. Return Sederhana

Return sederhana mengukur perubahan harga relatif terhadap harga awal.

Rumusnya:

> R_t→t+k = (C_t+k − C_t) / C_t

Atau dalam bentuk persentase:

> R_% = ((C_t+k − C_t) / C_t) × 100%

Keterangan:

- C_t = harga pada waktu awal;
- C_t+k = harga pada waktu akhir;
- k = jumlah periode atau horizon.

### Contoh

Harga awal:

> C_t = 1.000

Harga setelah tiga bar:

> C_t+3 = 1.050

Maka:

> R_t→t+3 = (1.050 − 1.000) / 1.000 = 0,05

Jadi, return sederhananya adalah **5%**.

Jika harga turun dari 1.000 menjadi 950:

> R = (950 − 1.000) / 1.000 = −0,05

Artinya, return adalah **−5%**.

### Catatan TEKB

Return sederhana harus memiliki definisi entry dan exit yang jelas. Return dari close ke close tidak sama dengan return dari close ke open berikutnya.

Jika penelitian menggunakan entry aktual pada open bar berikutnya, maka harga entry harus menggunakan harga tersebut, bukan harga close sinyal.

Return sederhana juga belum memperhitungkan:

- biaya transaksi;
- slippage;
- pajak atau fee;
- spread;
- dan gap.

Jika biaya ingin dimasukkan, hasil bersih harus dihitung dengan aturan biaya yang terpisah dan terdokumentasi.

---

## B.2. Log Return

Log return mengukur perubahan harga menggunakan logaritma natural.

Rumusnya:

> r_t→t+k = ln(C_t+k / C_t)

Keterangan:

- C_t = harga awal;
- C_t+k = harga akhir;
- ln = logaritma natural.

### Contoh

Harga awal:

> C_t = 1.000

Harga akhir:

> C_t+1 = 1.050

Maka:

> r_t→t+1 = ln(1.050 / 1.000) = ln(1,05)

Hasilnya sekitar:

> r ≈ 0,04879

atau sekitar **4,879%**.

Log return sedikit lebih kecil daripada return sederhana untuk kenaikan positif sebesar 5%.

### Perbedaan return sederhana dan log return

Return sederhana:

> R = (C_t+k − C_t) / C_t

Log return:

> r = ln(C_t+k / C_t)

Keduanya mengukur perubahan harga, tetapi tidak identik.

Log return memiliki sifat aditif ketika beberapa perubahan harga berurutan dijumlahkan dalam bentuk log return:

> ln(C_2/C_1) + ln(C_3/C_2) = ln(C_3/C_1)

Dalam TEKB, log return dapat digunakan untuk mempelajari distribusi perubahan harga, terutama ketika penelitian ingin mengukur:

> P(r_t+1 | X_t)

Artinya, distribusi kemungkinan log return berikutnya berdasarkan kondisi X_t yang tersedia saat ini.

### Catatan TEKB

Return sederhana dan log return tidak boleh dicampur dalam satu analisis tanpa penjelasan. Peneliti harus mencatat:

- jenis return;
- harga yang digunakan;
- horizon;
- apakah return gross atau net;
- serta apakah harga telah disesuaikan.

---

## B.3. Relative Volume

Relative Volume atau RV mengukur volume aktual dibandingkan dengan volume baseline.

Rumus dasarnya:

> RV_t = V_t / V_baseline,t

Keterangan:

- V_t = volume aktual pada waktu t;
- V_baseline,t = volume referensi atau baseline yang relevan untuk waktu t.

### Contoh

Volume aktual:

> V_t = 750.000

Volume baseline:

> V_baseline,t = 150.000

Maka:

> RV_t = 750.000 / 150.000 = 5

Artinya, volume aktual adalah lima kali volume baseline.

### Interpretasi

- RV = 1: volume sama dengan baseline.
- RV > 1: volume lebih besar daripada baseline.
- RV < 1: volume lebih kecil daripada baseline.
- RV = 5: volume lima kali baseline.

RV tinggi menunjukkan aktivitas volume yang relatif besar. Namun, RV tidak otomatis menunjukkan arah harga. Volume besar dapat muncul ketika harga naik, turun, atau bergerak sangat tidak menentu.

### Baseline intraday

Untuk data intraday, baseline sebaiknya memperhatikan:

- sesi perdagangan;
- slot waktu;
- hari perdagangan;
- periode historis yang digunakan;
- dan aturan ex-ante.

Volume pada awal sesi biasanya memiliki karakter berbeda dari volume menjelang penutupan. Karena itu, membandingkan seluruh volume intraday dengan satu rata-rata global dapat menghasilkan ukuran yang bias.

### Catatan TEKB

Baseline harus dihitung menggunakan data yang tersedia sebelum event atau sebelum bar yang sedang dievaluasi. Data masa depan tidak boleh masuk ke dalam baseline.

Jika baseline menggunakan rata-rata historis, periode dan metode perhitungannya harus dicatat.

---

## B.4. True Range

True Range atau TR adalah ukuran rentang pergerakan harga yang mempertimbangkan kemungkinan gap dari penutupan sebelumnya.

Rumusnya:

> TR_t = max(H_t − L_t, |H_t − C_t−1|, |L_t − C_t−1|)

Keterangan:

- H_t = harga tertinggi pada periode t;
- L_t = harga terendah pada periode t;
- C_t−1 = harga penutupan periode sebelumnya;
- |x| = nilai absolut dari x.

True Range memilih nilai terbesar dari tiga komponen:

1. Rentang candle saat ini:

   > H_t − L_t

2. Jarak antara high saat ini dan close sebelumnya:

   > |H_t − C_t−1|

3. Jarak antara low saat ini dan close sebelumnya:

   > |L_t − C_t−1|

### Contoh

Misalkan:

- H_t = 110
- L_t = 98
- C_t−1 = 100

Maka:

- H_t − L_t = 110 − 98 = 12
- |H_t − C_t−1| = |110 − 100| = 10
- |L_t − C_t−1| = |98 − 100| = 2

Jadi:

> TR_t = max(12, 10, 2) = 12

### Contoh dengan gap

Misalkan:

- H_t = 115
- L_t = 108
- C_t−1 = 100

Maka:

- H_t − L_t = 7
- |H_t − C_t−1| = 15
- |L_t − C_t−1| = 8

Sehingga:

> TR_t = max(7, 15, 8) = 15

Walaupun rentang candle hanya 7 poin, True Range menjadi 15 karena terdapat jarak besar dari close sebelumnya menuju harga periode sekarang.

### Catatan TEKB

True Range bukan arah pergerakan. TR hanya mengukur besarnya rentang atau perubahan yang relevan terhadap volatilitas.

TR juga bukan ATR. TR adalah ukuran untuk satu periode, sedangkan ATR merupakan ukuran rata-rata atau pemulusan True Range selama beberapa periode.

---

## B.5. Average True Range

Average True Range atau ATR adalah ukuran volatilitas yang dibangun dari True Range.

ATR membantu memberikan "penggaris" untuk menilai apakah suatu pergerakan harga tergolong kecil atau besar dibandingkan kondisi volatilitas instrumen tersebut.

Dalam TEKB, ATR dapat digunakan untuk:

- menormalkan MAE dan MFE;
- menentukan jarak kandidat stop-loss;
- menentukan jarak kandidat take-profit;
- membandingkan gerakan antarperiode;
- dan menyatakan ukuran pergerakan dalam satuan ×ATR.

### True Range sebagai dasar

Pertama, hitung:

> TR_t = max(H_t − L_t, |H_t − C_t−1|, |L_t − C_t−1|)

Kemudian, ATR dihitung dari rangkaian TR.

### ATR dengan rata-rata sederhana

Salah satu bentuk sederhana:

> ATR_t^SMA = (1/n) × Σ TR_t−i

Keterangan:

- n = periode ATR;
- TR_t−i = True Range pada periode yang termasuk dalam jendela perhitungan.

### ATR Wilder

Dalam banyak penggunaan teknikal, ATR dihitung menggunakan metode Wilder.

Untuk inisialisasi, ATR awal dapat dihitung sebagai rata-rata TR sebanyak n periode:

> ATR_n = (TR_1 + TR_2 + ... + TR_n) / n

Setelah itu, pembaruan ATR Wilder dapat ditulis:

> ATR_t = ((n − 1) × ATR_t−1 + TR_t) / n

Atau:

> ATR_t = ATR_t−1 + (TR_t − ATR_t−1) / n

### Contoh sederhana

Misalkan ATR periode sebelumnya adalah 10, True Range periode sekarang adalah 14, dan periode ATR adalah 14.

Maka:

> ATR_t = (13 × 10 + 14) / 14

> ATR_t = 144 / 14 ≈ 10,286

Jadi ATR baru sekitar 10,286.

### ATR entry dalam TEKB

Jika event terdeteksi pada bar T dan entry dilakukan pada bar T+1, maka ATR yang digunakan harus berasal dari informasi yang tersedia sebelum entry sesuai kontrak penelitian.

Dalam banyak desain TEKB, ATR entry diambil dari kondisi pada close T dan kemudian dianggap tetap selama evaluasi event.

Hal ini penting agar ATR tidak berubah menggunakan informasi masa depan selama trade sedang dievaluasi.

### Catatan TEKB

ATR bukan prediksi arah harga. ATR hanya mengukur skala volatilitas.

ATR juga bukan ukuran risiko total. Risiko aktual dapat dipengaruhi oleh:

- gap;
- likuiditas;
- slippage;
- biaya;
- ukuran posisi;
- dan kondisi eksekusi.

Periode ATR, misalnya n = 14, harus dicatat sebagai bagian dari konfigurasi penelitian.

---

## B.6. Maximum Adverse Excursion

Maximum Adverse Excursion atau MAE mengukur gerakan maksimum yang berlawanan dengan posisi selama horizon pengukuran.

Untuk posisi long, MAE dihitung berdasarkan harga terendah yang dicapai setelah entry.

Jika:

- P_entry = harga entry;
- L_min = harga terendah selama horizon;

maka:

> MAE_raw = L_min − P_entry

Karena harga terendah biasanya berada di bawah entry, MAE long umumnya bernilai negatif.

### Contoh

Harga entry:

> P_entry = 1.020

Harga terendah selama horizon:

> L_min = 1.005

Maka:

> MAE_raw = 1.005 − 1.020 = −15

Artinya, harga sempat bergerak 15 poin melawan posisi.

### MAE dalam satuan ×ATR

Jika ATR entry adalah 10:

> MAE_×ATR = MAE_raw / ATR_entry

> MAE_×ATR = −15 / 10 = −1,5

Artinya, gerakan maksimum yang melawan posisi adalah 1,5 ATR.

### Interpretasi

MAE dapat membantu menjawab:

- Seberapa dalam harga biasanya bergerak melawan posisi?
- Apakah stop-loss tertentu terlalu sempit?
- Berapa besar risiko intratrade?
- Apakah event yang akhirnya profit tetap mengalami penurunan besar terlebih dahulu?
- Apakah kandidat SL/TP masuk akal terhadap karakter gerakan harga?

### Catatan TEKB

MAE harus menggunakan harga entry yang benar-benar didefinisikan oleh penelitian, bukan harga sinyal jika entry aktual berada pada bar berikutnya.

Horizon MAE juga harus ditentukan, misalnya:

- R1;
- R3;
- R5;
- R10;
- atau maksimum holding period tertentu.

MAE tidak sama dengan kerugian akhir. MAE menunjukkan gerakan terburuk yang sempat terjadi selama horizon, bukan selalu hasil exit aktual.

---

## B.7. Maximum Favorable Excursion

Maximum Favorable Excursion atau MFE mengukur gerakan maksimum yang mendukung posisi selama horizon pengukuran.

Untuk posisi long, MFE dihitung berdasarkan harga tertinggi yang dicapai setelah entry.

Jika:

- P_entry = harga entry;
- H_max = harga tertinggi selama horizon;

maka:

> MFE_raw = H_max − P_entry

### Contoh

Harga entry:

> P_entry = 1.020

Harga tertinggi selama horizon:

> H_max = 1.045

Maka:

> MFE_raw = 1.045 − 1.020 = 25

Artinya, harga sempat bergerak 25 poin mendukung posisi.

### MFE dalam satuan ×ATR

Jika ATR entry adalah 10:

> MFE_×ATR = MFE_raw / ATR_entry

> MFE_×ATR = 25 / 10 = 2,5

Artinya, harga sempat bergerak mendukung posisi sejauh 2,5 ATR.

### Interpretasi

MFE dapat membantu menjawab:

- Seberapa besar peluang gerakan positif yang tersedia?
- Apakah target profit tertentu terlalu jauh?
- Apakah harga sering sempat mencapai target tetapi kemudian berbalik?
- Apakah kandidat take-profit sesuai dengan distribusi gerakan?
- Apakah event memiliki potensi gerakan yang cukup untuk menutup biaya dan risiko?

### Catatan TEKB

MFE bukan profit yang pasti direalisasikan.

Jika harga sempat naik 2,5 ATR tetapi posisi tidak ditutup pada titik tersebut, trader belum tentu memperoleh keuntungan 2,5 ATR.

MFE adalah ukuran perjalanan harga, bukan bukti bahwa keputusan exit tertentu benar-benar terjadi.

---

## B.8. R-Unit

R-unit atau R adalah satuan hasil yang dinormalisasi berdasarkan risiko awal yang telah ditentukan.

R-unit membantu membandingkan hasil antar-trade yang memiliki harga dan ukuran volatilitas berbeda.

Secara umum:

> R = Hasil aktual / Risiko awal

Untuk posisi long dengan entry P_entry dan stop-loss P_SL, risiko per unit harga dapat ditulis:

> Risk_raw = P_entry − P_SL

Jika hasil exit adalah P_exit, maka hasil raw:

> Result_raw = P_exit − P_entry

Sehingga:

> R = (P_exit − P_entry) / (P_entry − P_SL)

### Contoh

Entry:

> P_entry = 1.000

Stop-loss:

> P_SL = 980

Risiko awal:

> Risk_raw = 1.000 − 980 = 20

Jika exit berada pada 1.040:

> Result_raw = 1.040 − 1.000 = 40

Maka:

> R = 40 / 20 = 2R

Artinya, hasilnya dua kali risiko awal.

Jika exit berada pada 970:

> Result_raw = 970 − 1.000 = −30

Maka:

> R = −30 / 20 = −1,5R

Artinya, hasilnya rugi sebesar 1,5 kali risiko awal.

### R-unit berbasis ATR

Dalam TEKB, risiko awal dapat ditentukan menggunakan jarak ×ATR.

Misalnya:

> SL = 1 × ATR

Jika ATR entry adalah 10, maka risiko awal adalah 10 poin.

Jika hasil aktual adalah +20 poin:

> R = 20 / 10 = 2R

### Catatan TEKB

Definisi R harus dikunci. Risiko awal dapat berarti:

- jarak entry ke stop-loss;
- risiko moneter;
- atau definisi lain yang telah ditentukan dalam kontrak.

R-unit tidak boleh berubah-ubah setelah hasil diketahui.

Selain itu, R sebelum biaya tidak sama dengan R bersih setelah biaya. Jika biaya dimasukkan, aturan pengurangan biaya harus dijelaskan secara terpisah.

---

## B.9. Expectancy

Expectancy adalah rata-rata hasil yang diharapkan berdasarkan distribusi hasil yang diamati dalam sampel penelitian.

Jika hasil setiap event dinyatakan sebagai R_i, maka expectancy sampel adalah:

> Ê(R) = (1/n) × Σ R_i

Keterangan:

- n = jumlah event atau trade yang dievaluasi;
- R_i = hasil event ke-i.

### Contoh

Misalkan terdapat lima hasil:

> +1R, −1R, +2R, −0,5R, +0,5R

Maka:

> Ê(R) = (1 − 1 + 2 − 0,5 + 0,5) / 5

> Ê(R) = 2 / 5 = 0,4R

Expectancy sampelnya adalah **+0,4R**.

Artinya, rata-rata hasil historis dalam sampel tersebut adalah +0,4R per event.

### Bentuk berdasarkan win rate

Dalam kasus sederhana dengan rata-rata win dan rata-rata loss, expectancy dapat ditulis:

> E(R) = p_win × R̄_win + p_loss × R̄_loss

Keterangan:

- p_win = proporsi hasil menang;
- R̄_win = rata-rata hasil event menang;
- p_loss = proporsi hasil kalah;
- R̄_loss = rata-rata hasil event kalah, biasanya bernilai negatif.

### Contoh

Win rate:

> p_win = 60%

Rata-rata win:

> R̄_win = 1R

Proporsi loss:

> p_loss = 40%

Rata-rata loss:

> R̄_loss = −0,75R

Maka:

> E(R) = 0,6(1) + 0,4(−0,75)

> E(R) = 0,6 − 0,3 = 0,3R

### Expectancy bersih

Jika biaya per event dinyatakan dalam satuan R sebesar Cost_R, maka secara sederhana:

> E(R_net) = E(R_gross) − E(Cost_R)

Namun, dalam implementasi nyata, biaya dapat berbeda menurut:

- harga;
- ukuran transaksi;
- spread;
- slippage;
- likuiditas;
- dan kondisi entry/exit.

Karena itu, perhitungan net harus mengikuti model biaya yang telah ditentukan.

### Catatan TEKB

Expectancy bukan satu-satunya ukuran edge.

Expectancy harus dibaca bersama:

- distribusi hasil;
- median;
- MAE/MFE;
- ekor kerugian;
- jumlah event;
- ketidakpastian;
- hasil B0;
- dan biaya.

Expectancy positif juga belum otomatis berarti edge. Yang penting dalam TEKB adalah perbedaan hasil B1 terhadap B0:

> ΔE = E(B1) − E(B0)

---

## B.10. Perbedaan B1 dan B0

Dalam TEKB, hasil B1 tidak cukup dinilai secara terpisah. B1 harus dibandingkan dengan B0 yang dibentuk menggunakan aturan pembanding yang adil.

Jika:

- E(B1) = ukuran hasil B1;
- E(B0) = ukuran hasil B0;

maka perbedaan sederhananya adalah:

> Δ = E(B1) − E(B0)

Jika ukuran yang dibandingkan adalah expectancy:

> ΔE = E(R_B1) − E(R_B0)

### Contoh

Expectancy B1:

> E(R_B1) = 0,12R

Expectancy B0:

> E(R_B0) = 0,05R

Maka:

> ΔE = 0,12 − 0,05 = 0,07R

Artinya, B1 memiliki expectancy 0,07R lebih tinggi daripada B0 dalam sampel dan definisi penelitian tersebut.

### Perbedaan return

Jika yang dibandingkan adalah rata-rata return:

> ΔR = R̄_B1 − R̄_B0

Contoh:

- R̄_B1 = 1,2%
- R̄_B0 = 0,8%

Maka:

> ΔR = 1,2% − 0,8% = 0,4%

### Perbedaan median

Perbandingan juga dapat dilakukan pada median:

> ΔMedian = Median(B1) − Median(B0)

Median penting ketika distribusi memiliki outlier atau ekor yang panjang.

### Perbedaan proporsi hasil positif

Jika yang dibandingkan adalah proporsi event dengan return positif:

> Δp = p(B1) − p(B0)

Contoh:

- p(B1) = 55%
- p(B0) = 48%

Maka:

> Δp = 7

atau:

> +7 poin persentase

Perlu dibedakan antara "7 poin persentase" dan "7 persen relatif". Dalam laporan TEKB, istilah yang digunakan harus jelas.

### Perbedaan distribusi

Perbedaan B1 dan B0 tidak harus dibatasi pada satu angka.

Penelitian dapat membandingkan:

- mean;
- median;
- percentile;
- proporsi return positif;
- MAE;
- MFE;
- worst-case;
- best-case;
- net expectancy;
- dan bentuk ekor distribusi.

Contohnya, B1 mungkin memiliki mean lebih tinggi tetapi juga memiliki ekor kerugian yang lebih buruk. Dalam situasi seperti itu, kesimpulan tidak boleh hanya menyebut mean yang positif.

### Perbandingan berpasangan

Dalam TEKB, B1 dan B0 idealnya dipasangkan menggunakan unit pembanding yang telah ditentukan.

Pasangan dapat memiliki:

- instrumen yang sama;
- slot waktu yang sama;
- periode yang sebanding;
- aturan pencocokan yang sama;
- dan anchor timestamp yang jelas.

Perbedaan kemudian dapat dihitung per pasangan:

> D_i = R_B1,i − R_B0,i

Rata-rata perbedaan berpasangan:

> D̄ = (1/n) × Σ D_i

Bentuk berpasangan membantu mengurangi sebagian variasi yang berasal dari kondisi pasar umum, karena B1 dan B0 dibandingkan dalam konteks yang lebih sebanding.

### Catatan TEKB

Perbedaan B1-B0 hanya bermakna jika B0 dibentuk secara adil.

B0 tidak boleh:

- dipilih berdasarkan hasil akhirnya;
- menggunakan informasi masa depan;
- diganti hanya karena hasilnya tidak menguntungkan;
- atau dibentuk dengan aturan berbeda dari B1 tanpa alasan metodologis yang jelas.

Perbedaan positif juga tidak otomatis berarti edge. Perbedaan harus dinilai bersama:

- ketidakpastian;
- bootstrap;
- multiple testing;
- BH-FDR;
- practical significance;
- ketahanan terhadap skenario worst-case;
- dan validasi OOS.

---

## B.11. Ringkasan Rumus

| Ukuran | Rumus Dasar | Fungsi |
|---|---|---|
| Return sederhana | (C_t+k − C_t) / C_t | Mengukur perubahan harga relatif |
| Log return | ln(C_t+k / C_t) | Mengukur perubahan harga secara logaritmik |
| Relative Volume | V_t / V_baseline,t | Mengukur volume relatif terhadap baseline |
| True Range | max(H−L, \|H−C_t−1\|, \|L−C_t−1\|) | Mengukur rentang volatilitas satu periode |
| ATR Wilder | ((n−1)ATR_t−1 + TR_t) / n | Mengukur skala volatilitas yang diperlunak |
| MAE | L_min − P_entry | Mengukur gerakan maksimum yang melawan posisi long |
| MFE | H_max − P_entry | Mengukur gerakan maksimum yang mendukung posisi long |
| R-unit | Hasil aktual / Risiko awal | Menormalkan hasil berdasarkan risiko |
| Expectancy | (1/n) Σ R_i | Mengukur rata-rata hasil per event |
| Perbedaan B1-B0 | E(B1) − E(B0) | Mengukur keunggulan relatif terhadap pembanding |

---

## B.12. Prinsip Penggunaan Rumus dalam TEKB

Rumus-rumus dasar di atas harus digunakan dengan beberapa prinsip:

1. **Definisi harus jelas.**
   - Harga, volume, horizon, entry, exit, dan periode harus ditentukan.

2. **Waktu ketersediaan data harus dihormati.**
   - Tidak boleh menggunakan data masa depan untuk menghitung fitur, baseline, ATR, atau keputusan entry.

3. **Rumus harus konsisten.**
   - Metode yang digunakan pada B1 harus dapat dibandingkan secara adil dengan metode pada B0.

4. **Raw dan normalized harus dibedakan.**
   - Nilai dalam rupiah atau poin tidak sama dengan nilai dalam persentase, ×ATR, atau R-unit.

5. **Gross dan net harus dipisahkan.**
   - Hasil sebelum biaya tidak boleh disebut sebagai hasil bersih.

6. **Satu angka tidak cukup.**
   - Rumus harus dibaca bersama distribusi, variasi, ketidakpastian, dan pembanding.

7. **Rumus bukan bukti dengan sendirinya.**
   - Rumus hanya menghasilkan ukuran. Bukti muncul dari proses penelitian yang lengkap, transparan, dapat diaudit, dan diuji terhadap data yang belum digunakan.

Pada akhirnya, rumus dalam TEKB bukan alat untuk memperindah laporan. Rumus adalah bahasa bersama agar pengamatan dapat diubah menjadi angka yang jelas, dibandingkan secara adil, dan diuji secara jujur.

---

<div align="center">

[← Lampiran A](/posts/lampiran-a-glosarium/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Lampiran C →](/posts/lampiran-c-status-kode/)

</div>