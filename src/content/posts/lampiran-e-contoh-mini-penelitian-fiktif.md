---
title: "Lampiran E — Contoh Mini Penelitian Fiktif"
published: 2026-09-14
description: "Contoh mini penelitian TEKB dari pertanyaan hingga kesimpulan, dengan data fiktif, untuk memperlihatkan alur penelitian yang jujur dan dapat ditelusuri."
tags: ["lampiran-e", "contoh", "mini-penelitian", "studi-kasus"]
category: "Lampiran"
draft: false
lang: ""
---

## E.1 Tujuan Lampiran

Lampiran ini memberikan contoh sederhana tentang bagaimana penelitian TEKB dapat dijalankan dari awal hingga akhir.

Seluruh angka, nama instrumen, tanggal, event, hasil statistik, dan keputusan dalam contoh ini sepenuhnya fiktif. Contoh ini bukan hasil penelitian pasar nyata dan tidak boleh digunakan sebagai dasar keputusan investasi.

Tujuan contoh ini bukan untuk menunjukkan bahwa suatu pola tertentu pasti menghasilkan keuntungan. Tujuannya adalah memperlihatkan bagaimana pertanyaan trading diubah menjadi penelitian yang memiliki:

- definisi event;
- pembanding yang adil;
- aturan entry;
- pengukuran hasil;
- evaluasi kandidat;
- pengukuran ketidakpastian;
- seleksi In-Sample;
- pengujian Out-of-Sample;
- batas kesimpulan.

Agar mudah diikuti, contoh menggunakan satu instrumen fiktif bernama ABCD dan data harian sederhana.

## E.2 Pertanyaan Penelitian

### Pertanyaan utama

Apakah event anomali volume tinggi pada saham ABCD berkaitan dengan return tiga hari berikutnya yang berbeda dari kondisi pembanding B0 yang dipilih secara adil?

Pertanyaan tersebut sengaja tidak dirumuskan sebagai:

> "Apakah volume tinggi menyebabkan harga naik?"

Alasannya, penelitian ini hanya menguji hubungan empiris antara kondisi volume dan hasil setelahnya. Desain ini belum cukup untuk membuktikan hubungan sebab-akibat.

### Hipotesis penelitian

Hipotesis kerja:

> Setelah event anomali volume tinggi, return tiga hari berikutnya pada B1 mungkin lebih tinggi daripada return tiga hari berikutnya pada B0.

Hipotesis nol secara sederhana:

> Tidak terdapat perbedaan yang berarti antara hasil B1 dan B0.

Hipotesis ini belum menyatakan bahwa B1 pasti menguntungkan. Hipotesis hanya menyatakan bahwa terdapat kemungkinan perbedaan yang dapat diuji.

### Batas penelitian

Contoh ini menggunakan asumsi berikut:

- instrumen: ABCD;
- timeframe: harian;
- event: anomali volume;
- entry: open hari perdagangan berikutnya;
- horizon utama: tiga hari perdagangan;
- posisi: long;
- pembanding: B0 pada instrumen dan kondisi waktu yang sama;
- biaya: ditampilkan secara terpisah;
- seluruh angka: fiktif.

## E.3 Definisi Event

### Definisi event

Sebuah event terjadi apabila volume pada hari $t$ memenuhi:

$$RV_t = \frac{V_t}{V_{\text{baseline},t}} \geq 3$$

Dengan:

- $V_t$ = volume pada hari $t$;
- $V_{\text{baseline},t}$ = baseline volume yang dihitung hanya dari data sebelum hari $t$;
- $RV_t$ = Relative Volume.

Dengan demikian, event terjadi ketika volume setidaknya tiga kali baseline.

### Aturan tambahan

Agar event dapat digunakan secara konsisten, ditetapkan aturan:

- Baseline dihitung dari 20 hari perdagangan sebelumnya.
- Hari $t$ harus memiliki OHLCV yang valid.
- Event hanya dinyatakan setelah candle hari $t$ selesai.
- Event tidak boleh menggunakan volume atau harga dari hari setelah $t$.
- Event yang terlalu berdekatan dapat dikenai declustering.
- Event yang berada di luar periode penelitian tidak disertakan.
- Jika data setelah event tidak cukup untuk menghitung horizon, event diberi status `INSUFFICIENT_HORIZON`.

### Contoh event

Misalnya:

| Komponen | Nilai |
|---|---|
| Instrumen | ABCD |
| Tanggal event | 10 Maret |
| Volume event | 300.000 |
| Baseline volume | 90.000 |
| RV | 3,33 |
| Status | Valid |

Perhitungan:

$$RV_t = \frac{300.000}{90.000} = 3{,}33$$

Karena RV lebih besar dari 3, event memenuhi definisi.

### Hal yang belum dapat disimpulkan

Dari event tersebut, kita baru dapat mengatakan:

> "Pada 10 Maret, ABCD mengalami anomali volume menurut aturan penelitian."

Kita belum boleh mengatakan:

- harga pasti naik;
- investor besar sedang membeli;
- event merupakan akumulasi;
- event menghasilkan profit;
- event adalah sinyal BUY yang telah terbukti.

## E.4 Definisi B1 dan B0

### B1

B1 adalah kelompok event yang memenuhi definisi anomali volume.

Untuk contoh ini:

> B1 = event ABCD dengan RV ≥ 3, berdasarkan baseline 20 hari sebelumnya.

Entry B1 dilakukan pada:

$$P_{\text{entry}} = O_{t+1}$$

Artinya, entry menggunakan open hari perdagangan berikutnya setelah candle event selesai.

### B0

B0 adalah pembanding yang tidak dipilih berdasarkan hasil masa depan.

Untuk contoh mini ini, B0 ditentukan dengan aturan:

- Instrumen sama, yaitu ABCD.
- B0 berasal dari hari perdagangan lain yang tidak termasuk event B1.
- B0 memiliki slot waktu atau konteks kalender yang sama jika relevan.
- B0 dipilih berdasarkan aturan nearest valid trading day.
- B0 tidak boleh menggunakan hasil return untuk menentukan kecocokan.
- Satu observasi B0 tidak digunakan berulang apabila aturan penelitian melarang reuse.
- B0 harus memiliki data yang cukup untuk horizon evaluasi.

### Contoh pasangan

| Pasangan | B1 Event | B0 Pembanding |
|---|---|---|
| 1 | 10 Mar | 9 Feb |
| 2 | 18 Mar | 17 Feb |
| 3 | 25 Mar | 24 Feb |
| 4 | 2 Apr | 1 Mar |
| 5 | 10 Apr | 9 Mar |

Tanggal B0 dalam tabel hanya ilustrasi. Dalam penelitian nyata, tanggal tersebut harus dihasilkan oleh aturan matching yang terdokumentasi, bukan dipilih secara manual agar hasil terlihat baik.

### Jika B0 tidak ditemukan

Jika tidak ada pembanding yang memenuhi seluruh aturan, event diberi status:

`NO_MATCH_FOUND`

Event tersebut tidak boleh dipasangkan secara paksa dengan observasi yang tidak sesuai.

## E.5 Data Contoh

### Data event B1

Tabel berikut menunjukkan contoh data fiktif. Harga entry adalah open hari setelah event.

| Event | Tanggal Event | RV | Close Event | Open Entry | Close +3 Hari | Return 3 Hari |
|---|---|---|---|---|---|---|
| B1-01 | 10 Mar | 3,33 | 100 | 102 | 106 | 3,92% |
| B1-02 | 18 Mar | 4,10 | 110 | 111 | 112 | 0,90% |
| B1-03 | 25 Mar | 3,25 | 105 | 104 | 100 | -3,85% |
| B1-04 | 2 Apr | 5,00 | 120 | 121 | 127 | 4,96% |
| B1-05 | 10 Apr | 3,60 | 115 | 114 | 116 | 1,75% |
| B1-06 | 17 Apr | 4,40 | 130 | 132 | 129 | -2,27% |
| B1-07 | 25 Apr | 3,15 | 125 | 124 | 128 | 3,23% |
| B1-08 | 2 Mei | 3,90 | 140 | 141 | 143 | 1,42% |

Return dihitung dari harga entry, bukan dari close event:

$$R_{3} = \frac{C_{t+3} - P_{\text{entry}}}{P_{\text{entry}}}$$

Contoh B1-01:

$$R_3 = \frac{106 - 102}{102}$$

$$R_3 = 3{,}92\%$$

Perbedaan antara close event dan open entry harus dipertahankan. Menggunakan close event sebagai entry hanya karena lebih mudah dapat menciptakan hasil yang tidak sesuai dengan aturan eksekusi.

### Data B0

| B0 | Tanggal Pembanding | Open Entry | Close +3 Hari | Return 3 Hari |
|---|---|---|---|---|
| B0-01 | 9 Feb | 100 | 102 | 2,00% |
| B0-02 | 17 Feb | 110 | 110 | 0,00% |
| B0-03 | 24 Feb | 103 | 100 | -2,91% |
| B0-04 | 1 Mar | 120 | 123 | 2,50% |
| B0-05 | 9 Mar | 115 | 116 | 0,87% |
| B0-06 | 16 Mar | 130 | 128 | -1,54% |
| B0-07 | 24 Mar | 124 | 126 | 1,61% |
| B0-08 | 1 Apr | 140 | 141 | 0,71% |

Untuk penelitian berpasangan, B1-01 dibandingkan dengan B0-01, B1-02 dengan B0-02, dan seterusnya.

## E.6 Pengukuran Return B1 dan B0

### Return B1

Return tiga hari untuk setiap event dihitung dari open entry hingga close pada akhir horizon.

$$R_{B1,i} = \frac{C_{\text{akhir},i} - P_{\text{entry},i}}{P_{\text{entry},i}}$$

### Return B0

Return B0 dihitung dengan definisi yang sama:

$$R_{B0,i} = \frac{C_{\text{akhir},i} - P_{\text{entry},i}}{P_{\text{entry},i}}$$

Definisi yang sama penting agar B1 dan B0 benar-benar dapat dibandingkan.

### Perbedaan berpasangan

Untuk setiap pasangan:

$$D_i = R_{B1,i} - R_{B0,i}$$

Contoh pasangan pertama:

$$D_1 = 3{,}92\% - 2{,}00\% = 1{,}92\%$$

Tabel perbandingan:

| Pasangan | Return B1 | Return B0 | Selisih B1 − B0 |
|---|---|---|---|
| 1 | 3,92% | 2,00% | 1,92% |
| 2 | 0,90% | 0,00% | 0,90% |
| 3 | -3,85% | -2,91% | -0,94% |
| 4 | 4,96% | 2,50% | 2,46% |
| 5 | 1,75% | 0,87% | 0,88% |
| 6 | -2,27% | -1,54% | -0,73% |
| 7 | 3,23% | 1,61% | 1,62% |
| 8 | 1,42% | 0,71% | 0,71% |

Rata-rata return B1:

$$\bar{R}_{B1} = \frac{1}{8}\sum_{i=1}^{8}R_{B1,i}$$

Dari data contoh:

$$\bar{R}_{B1} \approx 1{,}26\%$$

Rata-rata return B0:

$$\bar{R}_{B0} \approx 0{,}40\%$$

Perbedaan rata-rata:

$$\Delta = \bar{R}_{B1} - \bar{R}_{B0}$$

$$\Delta \approx 0{,}86\%$$

Dalam contoh ini, B1 memiliki rata-rata return tiga hari sekitar 0,86 poin persentase lebih tinggi daripada B0.

Namun, angka ini belum cukup untuk menyatakan bahwa edge telah terbukti.

## E.7 Pengukuran MAE/MFE

### Tujuan

Return akhir hanya menunjukkan posisi harga pada akhir horizon. Return tidak menunjukkan perjalanan harga di tengah jalan.

Misalnya, dua event sama-sama menghasilkan return akhir +2%, tetapi:

- event pertama hanya turun 0,5% sebelum naik;
- event kedua sempat turun 8% sebelum naik.

Keduanya memiliki return akhir yang sama, tetapi profil risikonya sangat berbeda.

Karena itu, TEKB juga mengukur MAE dan MFE.

### Definisi

Untuk posisi long:

$$MAE_{\text{raw}} = L_{\min} - P_{\text{entry}}$$

$$MFE_{\text{raw}} = H_{\max} - P_{\text{entry}}$$

Jika ingin menggunakan bentuk persentase:

$$MAE_{\%} = \frac{L_{\min} - P_{\text{entry}}}{P_{\text{entry}}}$$

$$MFE_{\%} = \frac{H_{\max} - P_{\text{entry}}}{P_{\text{entry}}}$$

### Contoh data MAE/MFE B1

| Event | Entry | Low Terendah | High Tertinggi | MAE Raw | MFE Raw | MAE % | MFE % |
|---|---|---|---|---|---|---|---|
| B1-01 | 102 | 100 | 108 | -2 | 6 | -1,96% | 5,88% |
| B1-02 | 111 | 109 | 114 | -2 | 3 | -1,80% | 2,70% |
| B1-03 | 104 | 98 | 106 | -6 | 2 | -5,77% | 1,92% |
| B1-04 | 121 | 119 | 130 | -2 | 9 | -1,65% | 7,44% |
| B1-05 | 114 | 112 | 118 | -2 | 4 | -1,75% | 3,51% |
| B1-06 | 132 | 126 | 134 | -6 | 2 | -4,55% | 1,52% |
| B1-07 | 124 | 122 | 130 | -2 | 6 | -1,61% | 4,84% |
| B1-08 | 141 | 139 | 145 | -2 | 4 | -1,42% | 2,84% |

### Interpretasi

Dari contoh ini terlihat bahwa:

- sebagian besar event memiliki MAE sekitar −1,4% hingga −2%;
- beberapa event mengalami MAE lebih besar, sekitar −4,5% hingga −5,8%;
- MFE tidak selalu berakhir menjadi return positif;
- event B1-03 memiliki MFE positif, tetapi return akhirnya negatif;
- event B1-06 juga sempat bergerak naik, tetapi berakhir negatif.

Hal ini menunjukkan bahwa:

MFE bukan profit yang pasti direalisasikan, dan return akhir tidak menggambarkan seluruh perjalanan harga.

## E.8 ATR dan Normalisasi

Misalkan ATR pada waktu entry untuk setiap event adalah sebagai berikut:

| Event | ATR Entry | MAE Raw | MAE ×ATR | MFE Raw | MFE ×ATR |
|---|---|---|---|---|---|
| B1-01 | 2 | -2 | -1,00 | 6 | 3,00 |
| B1-02 | 2 | -2 | -1,00 | 3 | 1,50 |
| B1-03 | 3 | -6 | -2,00 | 2 | 0,67 |
| B1-04 | 2 | -2 | -1,00 | 9 | 4,50 |
| B1-05 | 2 | -2 | -1,00 | 4 | 2,00 |
| B1-06 | 3 | -6 | -2,00 | 2 | 0,67 |
| B1-07 | 2 | -2 | -1,00 | 6 | 3,00 |
| B1-08 | 2 | -2 | -1,00 | 4 | 2,00 |

Normalisasi dilakukan dengan:

$$MAE_{\times ATR} = \frac{MAE_{\text{raw}}}{ATR_{\text{entry}}}$$

$$MFE_{\times ATR} = \frac{MFE_{\text{raw}}}{ATR_{\text{entry}}}$$

Contoh B1-03:

$$MAE_{\times ATR} = \frac{-6}{3} = -2$$

Artinya, harga bergerak melawan posisi sejauh 2 ATR.

Normalisasi membantu membandingkan event dengan skala volatilitas yang berbeda. Namun, ATR tidak mengubah hasil menjadi lebih benar secara otomatis. Kualitas hasil tetap bergantung pada definisi ATR dan waktu pengambilannya.

## E.9 Evaluasi Kandidat SL/TP

### Kandidat yang diuji

Misalkan penelitian menguji tiga kandidat:

| Kandidat | Stop Loss | Take Profit | Maksimum Holding |
|---|---|---|---|
| C1 | 1 ATR | 1 ATR | 3 hari |
| C2 | 1 ATR | 2 ATR | 3 hari |
| C3 | 2 ATR | 2 ATR | 3 hari |

Ketiga kandidat ini ditentukan sebelum evaluasi OOS. Dalam contoh ini, kandidat masih dievaluasi pada data IS.

### Aturan evaluasi

Aturan Evaluation Engine:

- Evaluasi dimulai dari bar setelah entry.
- Jika harga menyentuh SL sebelum TP, posisi keluar pada SL.
- Jika harga menyentuh TP sebelum SL, posisi keluar pada TP.
- Jika SL dan TP tersentuh dalam candle yang sama dan urutannya tidak diketahui, status menjadi `AMBIGUOUS_INTRABAR`.
- Jika tidak ada SL atau TP yang tersentuh sampai akhir holding period, hasil menggunakan harga akhir sesuai aturan `TIMEOUT`.
- Biaya transaksi dihitung terpisah.
- Aturan yang sama diterapkan kepada B1 dan B0.

### Hasil evaluasi kandidat fiktif

| Kandidat | B1 Gross Expectancy | B0 Gross Expectancy | Δ B1 − B0 | B1 Net Expectancy | Status Awal |
|---|---|---|---|---|---|
| C1 | 0,08R | 0,05R | +0,03R | 0,04R | Belum cukup |
| C2 | 0,18R | 0,06R | +0,12R | 0,12R | Menjanjikan |
| C3 | 0,11R | 0,07R | +0,04R | 0,06R | Belum cukup |

Angka di atas sepenuhnya ilustratif.

Kandidat C2 terlihat paling menjanjikan karena:

- perbedaan B1–B0 lebih besar;
- expectancy net masih positif;
- hasil relatif lebih baik setelah biaya.

Namun, "paling menjanjikan" belum sama dengan "terbukti memiliki edge".

Kandidat masih harus melalui:

- pengukuran ketidakpastian;
- pengujian multiple testing;
- kriteria IS Selection;
- freeze;
- OOS.

## E.10 Distribusi Return

### Mengapa distribusi diperlukan?

Rata-rata return dapat menipu jika hanya dipengaruhi oleh beberapa hasil ekstrem.

Misalnya, dua kelompok sama-sama memiliki rata-rata return +1%:

- kelompok A memiliki hasil yang relatif merata;
- kelompok B memiliki banyak kerugian kecil dan satu keuntungan sangat besar.

Risiko keduanya tidak sama.

### Ringkasan distribusi fiktif

| Ukuran | B1 | B0 |
|---|---|---|
| Jumlah pasangan | 100 | 100 |
| Mean return 3 hari | 1,20% | 0,45% |
| Median | 0,80% | 0,40% |
| Persentase return positif | 58% | 52% |
| Persentil 10% | -4,50% | -4,00% |
| Persentil 25% | -1,20% | -1,40% |
| Persentil 75% | 3,10% | 2,10% |
| Persentil 90% | 5,80% | 4,70% |
| Worst observed | -8,00% | -7,50% |
| Best observed | 12,00% | 10,00% |

Angka ini merupakan contoh laporan yang lebih besar daripada tabel event awal. Angka tersebut tidak dimaksudkan sebagai hasil yang dihitung dari delapan baris sebelumnya.

### Interpretasi

Dalam contoh ini:

- mean B1 lebih tinggi daripada B0;
- median B1 juga lebih tinggi;
- proporsi return positif B1 sedikit lebih tinggi;
- sisi keuntungan B1 tampak lebih baik;
- sisi kerugian B1 juga tetap memiliki risiko besar.

Kesimpulan sementara yang wajar:

> "Dalam sampel contoh, B1 menunjukkan distribusi return yang secara deskriptif lebih baik daripada B0."

Kesimpulan tersebut belum berarti:

> "B1 pasti menguntungkan."

## E.11 Bootstrap

### Tujuan

Bootstrap digunakan untuk memperkirakan seberapa stabil perbedaan B1 dan B0.

Misalkan statistik utama yang digunakan adalah:

$$\Delta E = E(R_{B1}) - E(R_{B0})$$

Atau, dalam desain berpasangan:

$$\bar{D} = \frac{1}{n}\sum_{i=1}^{n} (R_{B1,i} - R_{B0,i})$$

### Prosedur bootstrap fiktif

Misalkan ditetapkan:

- unit resampling: tanggal;
- metode: date-cluster bootstrap;
- jumlah replikasi: 10.000;
- seed: 42;
- statistik utama: rata-rata selisih B1–B0;
- interval: percentile 95%.

Dalam setiap replikasi:

- tanggal penelitian dipilih ulang dengan pengembalian;
- seluruh event pada tanggal yang terpilih ikut dipertahankan;
- B1 dan B0 tetap berpasangan;
- rata-rata selisih dihitung;
- hasil disimpan;
- proses diulang 10.000 kali.

### Hasil bootstrap fiktif

| Statistik | Hasil |
|---|---|
| Estimasi Δ B1 − B0 | +0,75% |
| Interval bootstrap 95% | +0,10% hingga +1,42% |
| Proporsi replikasi Δ > 0 | 97,8% |
| Jumlah replikasi | 10.000 |
| Unit resampling | Tanggal |
| Seed | 42 |

### Interpretasi

Hasil tersebut menunjukkan bahwa, dalam simulasi bootstrap contoh:

- estimasi perbedaan berada di sekitar +0,75%;
- sebagian besar replikasi menghasilkan perbedaan positif;
- interval bootstrap tidak melewati nol dalam contoh ini.

Namun, interpretasinya harus dibatasi:

> "Berdasarkan data dan prosedur bootstrap yang digunakan, perbedaan B1–B0 tampak cukup stabil dalam sampel penelitian."

Bootstrap tidak membuktikan:

- bahwa hasil pasti berulang di masa depan;
- bahwa B1 menyebabkan return lebih tinggi;
- bahwa risiko kerugian telah hilang;
- bahwa strategi pasti menghasilkan profit setelah digunakan secara nyata.

## E.12 Multiple Testing

### Mengapa diperlukan?

Misalkan peneliti menguji:

- 5 threshold RV;
- 4 horizon;
- 6 kombinasi SL/TP;
- 3 kelompok instrumen;
- 2 jenis metrik utama.

Jumlah kandidat dapat menjadi besar. Dengan banyak pengujian, peluang menemukan hasil positif secara kebetulan juga meningkat.

### Contoh keluarga pengujian

Misalkan semua kandidat SL/TP dalam penelitian ini masuk ke satu keluarga:

`multiple_testing_family_id = FAM-2026-001`

Keluarga tersebut mencakup:

- C1;
- C2;
- C3;
- kandidat lain yang diuji dalam grid yang sama.

Untuk contoh lebih lengkap, worst-case dan best-case dapat dikelompokkan dalam keluarga berbeda karena keduanya menjawab pertanyaan evaluasi yang berbeda.

### Hasil koreksi fiktif

| Kandidat | p-value Mentah | q-value BH-FDR | Lolos FDR? |
|---|---|---|---|
| C1 | 0,18 | 0,24 | Tidak |
| C2 | 0,006 | 0,018 | Ya |
| C3 | 0,11 | 0,17 | Tidak |

Angka ini ilustratif.

Kandidat C2 dapat melanjutkan ke tahap seleksi jika seluruh kriteria lain juga terpenuhi.

### Prinsip interpretasi

Lolos BH-FDR tidak berarti kandidat telah terbukti benar secara universal. Artinya, kandidat memenuhi prosedur pengendalian risiko false discovery dalam keluarga pengujian yang ditentukan.

Jika peneliti menguji keluarga tambahan setelah melihat hasil, keluarga tersebut harus dicatat. Peneliti tidak boleh menyembunyikan percobaan sebelumnya.

## E.13 Seleksi IS

### Tujuan

IS Selection memilih kandidat berdasarkan aturan yang telah ditetapkan sebelum keputusan dibuat.

Contoh kriteria IS:

- Jumlah event minimal 100.
- Jumlah tanggal minimal 30.
- Jumlah instrumen minimal 10 jika penelitian memang multi-instrumen.
- Δ B1–B0 harus positif.
- Δ harus memenuhi ambang praktis minimum.
- Hasil harus lolos bootstrap atau prosedur ketidakpastian.
- Hasil harus lolos BH-FDR.
- Hasil tetap bertahan setelah biaya.
- Kandidat tidak boleh hanya bergantung pada satu instrumen.
- Kandidat harus memenuhi aturan robustness yang telah ditentukan.

### Hasil seleksi fiktif

| Kriteria | C1 | C2 | C3 |
|---|---|---|---|
| Δ positif | Ya | Ya | Ya |
| Δ minimum | Tidak | Ya | Tidak |
| Bootstrap memadai | Tidak | Ya | Tidak |
| Lolos BH-FDR | Tidak | Ya | Tidak |
| Bertahan setelah biaya | Tidak | Ya | Ya |
| Lolos IS Selection | Tidak | Ya | Tidak |

Dalam contoh ini, C2 menjadi kandidat yang dipilih untuk dibekukan.

Status hasil:

`IS_SELECTED`

Tetapi status ini belum sama dengan:

`OOS_VALIDATED`

### Jika tidak ada kandidat yang lolos

Jika seluruh kandidat gagal memenuhi kriteria, hasil yang benar adalah:

`NO_EDGE_FOUND`

Peneliti tidak boleh memilih kandidat yang "paling bagus di antara yang gagal" lalu menyebutnya sebagai edge yang telah terbukti.

## E.14 Freeze

Sebelum OOS dijalankan, kandidat C2 harus dibekukan.

### Isi freeze

Contoh manifest freeze:

| Komponen | Nilai |
|---|---|
| Hypothesis ID | HYP-RV-3D-001 |
| Research Batch ID | BATCH-IS-001 |
| Selected Candidate | C2 |
| Event Definition | RV ≥ 3 |
| Baseline | 20 hari sebelumnya |
| Entry Definition | Open hari valid berikutnya |
| Horizon | 3 hari |
| SL | 1 ATR |
| TP | 2 ATR |
| ATR Definition | Wilder ATR, periode 14 |
| B0 Rule | Nearest valid matched day |
| Evaluation Engine | EE-V1.0 |
| Candidate Grid Version | GRID-V1.0 |
| Multiple Testing Family | FAM-2026-001 |
| Freeze Timestamp | Sebelum akses OOS |
| Status | FROZEN |

Setelah freeze:

- threshold RV tidak boleh diubah karena hasil OOS;
- SL/TP tidak boleh diganti karena hasil OOS;
- B0 tidak boleh diganti agar hasil lebih baik;
- horizon tidak boleh diubah;
- Evaluation Engine tidak boleh diubah untuk menyelamatkan kandidat;
- kandidat lain tidak boleh dipilih ulang berdasarkan hasil OOS.

## E.15 Hasil OOS

### Tujuan OOS

OOS menguji kandidat C2 pada data baru yang tidak digunakan dalam proses seleksi.

Misalkan:

- periode IS: Januari 2020–Desember 2023;
- periode OOS: Januari 2024–Desember 2025.

Periode tersebut hanya ilustrasi.

### Aturan OOS

Kandidat C2 dievaluasi menggunakan:

- definisi event yang sama;
- entry yang sama;
- B0 yang sama;
- ATR yang sama;
- SL/TP yang sama;
- Evaluation Engine yang sama;
- kriteria OOS yang telah ditetapkan;
- biaya yang sama;
- prosedur pelaporan yang sama.

### Hasil OOS fiktif

| Ukuran | B1 OOS | B0 OOS |
|---|---|---|
| Jumlah pasangan | 140 | 140 |
| Mean return 3 hari | 0,92% | 0,55% |
| Median | 0,60% | 0,48% |
| Net expectancy | +0,09R | +0,05R |
| Δ expectancy | +0,04R | — |
| Persentase positif | 55% | 53% |
| Status | — | — |

Misalkan kriteria OOS yang telah ditentukan adalah:

- Δ harus positif;
- net expectancy B1 harus positif;
- tidak ada kerusakan ekstrem pada distribusi;
- hasil tidak boleh bertentangan secara material dengan batas risiko yang ditetapkan;
- kandidat harus tetap dapat dijalankan menurut asumsi biaya.

Dalam contoh ini, C2 memenuhi kriteria tersebut.

Status:

`OOS_VALIDATED`

### Makna hasil OOS

Kesimpulan yang wajar:

> "Kandidat C2 mempertahankan perbedaan positif terhadap B0 pada periode OOS yang telah ditentukan, sehingga memperoleh dukungan tambahan untuk generalisasi pada periode tersebut."

Namun, OOS bukan jaminan bahwa hasil akan terus bertahan setelah periode OOS berakhir.

## E.16 Kesimpulan yang Boleh Dibuat

Berdasarkan contoh fiktif ini, beberapa kesimpulan berikut boleh dibuat.

### 1. Kesimpulan tentang definisi event

> "Event anomali volume dapat didefinisikan secara eksplisit menggunakan Relative Volume terhadap baseline historis yang tersedia sebelum event."

### 2. Kesimpulan deskriptif

> "Dalam sampel penelitian, return tiga hari setelah event B1 tampak lebih tinggi daripada return pada kelompok pembanding B0."

### 3. Kesimpulan tentang perbedaan

> "Estimasi perbedaan hasil B1 dan B0 bernilai positif dalam periode penelitian yang diuji."

### 4. Kesimpulan tentang ketidakpastian

> "Dengan prosedur bootstrap yang digunakan, estimasi perbedaan menunjukkan tingkat kestabilan tertentu dalam sampel penelitian."

### 5. Kesimpulan tentang seleksi IS

> "Kandidat C2 memenuhi kriteria seleksi IS yang telah ditentukan, termasuk kriteria perbedaan, ketidakpastian, multiple testing, dan biaya."

### 6. Kesimpulan tentang OOS

> "Kandidat C2 mempertahankan hasil yang memenuhi kriteria OOS pada periode pengujian yang telah ditentukan."

### 7. Kesimpulan tentang batas generalisasi

> "Hasil memberikan bukti empiris terbatas bahwa kondisi event tersebut memiliki hubungan historis dengan hasil yang berbeda dari B0 pada data dan periode yang diuji."

Kata-kata seperti "dalam sampel", "pada periode yang diuji", "menurut aturan penelitian", dan "memberikan dukungan" penting karena membatasi klaim sesuai bukti yang tersedia.

## E.17 Kesimpulan yang Tidak Boleh Dibuat

Berikut adalah contoh kesimpulan yang terlalu jauh dari bukti penelitian.

### 1. Tidak boleh mengatakan event pasti menyebabkan kenaikan

Tidak tepat:

> "Anomali volume menyebabkan harga naik."

Alasannya, penelitian ini menguji hubungan historis, bukan membuktikan kausalitas.

Pernyataan yang lebih tepat:

> "Anomali volume berkaitan dengan perbedaan return dalam data yang diuji."

### 2. Tidak boleh mengatakan profit pasti

Tidak tepat:

> "Strategi ini pasti menguntungkan."

Alasannya:

- hasil historis tidak menjamin hasil masa depan;
- distribusi memiliki risiko kerugian;
- biaya dan eksekusi nyata dapat berbeda;
- kondisi pasar dapat berubah.

### 3. Tidak boleh mengatakan semua event akan naik

Tidak tepat:

> "Setiap kali RV ≥ 3, harga akan naik."

Dalam contoh saja terdapat event dengan return negatif.

Pernyataan yang lebih tepat:

> "Event tersebut memiliki distribusi hasil, bukan kepastian arah."

### 4. Tidak boleh mengatakan win rate sebagai bukti tunggal

Tidak tepat:

> "Karena win rate 58%, strategi ini terbukti bagus."

Win rate tidak menjelaskan:

- besar keuntungan;
- besar kerugian;
- tail risk;
- biaya;
- drawdown;
- perbedaan terhadap B0;
- ketidakpastian;
- hasil OOS.

### 5. Tidak boleh mengatakan lolos IS berarti pasti lolos OOS

Tidak tepat:

> "Karena C2 lolos IS, maka C2 pasti berhasil di OOS."

IS dan OOS memiliki fungsi berbeda. OOS justru diperlukan untuk menguji apakah hasil IS dapat bertahan pada data yang belum digunakan.

### 6. Tidak boleh mengatakan OOS menjamin masa depan

Tidak tepat:

> "Karena C2 lolos OOS, maka strategi ini akan selalu berhasil."

OOS hanya memberikan bukti tambahan pada periode tertentu. OOS tidak menghapus ketidakpastian.

### 7. Tidak boleh mengklaim investor besar sedang membeli

Tidak tepat:

> "Volume tinggi membuktikan institusi sedang akumulasi."

Volume tinggi dapat memiliki banyak penjelasan. Tanpa data order flow, transaksi pelaku, atau desain penelitian khusus, klaim tersebut tidak dapat dibuat hanya dari OHLCV.

### 8. Tidak boleh menyamakan MFE dengan profit terealisasi

Tidak tepat:

> "Karena MFE mencapai +3 ATR, trader pasti memperoleh +3R."

MFE hanya menunjukkan bahwa harga pernah bergerak sejauh itu. Trader mungkin telah keluar lebih awal, terkena stop loss, atau tidak mampu mengeksekusi pada harga tersebut.

### 9. Tidak boleh menyembunyikan kandidat yang gagal

Tidak tepat:

> "Kami menemukan kandidat terbaik

E.19 Pelajaran Utama dari Contoh
Contoh ini menunjukkan beberapa hal penting.

Pertama
Event bukan keputusan trading. Event hanya kondisi yang didefinisikan untuk diteliti.

Kedua
Entry harus mengikuti waktu ketika informasi tersedia. Menggunakan harga yang tidak dapat diketahui secara sah dapat menciptakan look-ahead bias.

Ketiga
B1 harus dibandingkan dengan B0. Return positif tanpa pembanding belum cukup untuk menyatakan adanya edge.

Keempat
MAE dan MFE memperlihatkan perjalanan harga, bukan hanya hasil akhir.

Kelima
ATR membantu menyetarakan skala pergerakan, tetapi tidak membuktikan bahwa kandidat SL/TP benar.

Keenam
Candidate SL/TP adalah hipotesis yang harus diuji, bukan parameter yang boleh dipilih setelah melihat hasil terbaik.

Ketujuh
Bootstrap membantu mengukur ketidakpastian, sedangkan multiple testing membantu mengendalikan risiko temuan palsu.

Kedelapan
IS Selection memilih kandidat berdasarkan aturan yang telah ditetapkan. Freeze kemudian mengunci kandidat sebelum OOS.

Kesembilan
OOS memberikan pengujian tambahan terhadap generalisasi, tetapi tidak menjamin keberhasilan masa depan.

Kesepuluh
Kesimpulan penelitian harus lebih sempit daripada keinginan peneliti.

E.20 Penutup
Mini penelitian fiktif ini memperlihatkan bahwa penelitian trading yang jujur tidak berhenti pada kalimat:

"Setelah volume tinggi, harga sering naik."

Kalimat tersebut baru merupakan pengamatan awal.

Penelitian TEKB melangkah lebih jauh dengan bertanya:

Bagaimana volume tinggi didefinisikan?

Apakah definisinya bebas dari data masa depan?

Apa yang disebut event?

Kapan entry benar-benar terjadi?

Apa pembanding yang adil?

Bagaimana return, MAE, dan MFE dihitung?

Kandidat SL/TP apa yang diuji?

Bagaimana outcome ditentukan?

Seberapa stabil hasilnya?

Berapa banyak pengujian yang dilakukan?

Mengapa kandidat tertentu dipilih?

Apakah kandidat sudah dibekukan?

Apakah hasilnya bertahan pada OOS?

Sejauh mana kesimpulan boleh dibuat?

Dengan alur tersebut, TEKB tidak mengubah pola historis menjadi kepastian. TEKB mengubah pola menjadi hipotesis, hipotesis menjadi pengukuran, pengukuran menjadi distribusi, distribusi menjadi pengujian, dan pengujian menjadi kesimpulan yang dibatasi oleh bukti.

Tujuan penelitian bukan membuat klaim sebesar mungkin, melainkan membuat klaim yang dapat dipertanggungjawabkan oleh data dan metode.

<div align="center">
← Lampiran D | Beranda | Daftar Isi | Lampiran F →

</div> ```
