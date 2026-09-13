---
title: "BAB 15 — Mengubah Hasil Menjadi Angka yang Bisa Dibandingkan"
published: 2026-09-12
description: "Win rate saja tidak cukup. Bab ini menjelaskan return, expectancy, satuan R, gross vs net expectancy, dan mengapa B1 harus dibandingkan dengan B0."
tags: ["bab-15", "expectancy", "return", "r-unit"]
category: "Bab"
draft: false
lang: ""
---

**BAGIAN V — MESIN YANG MENENTUKAN APAKAH SEBUAH HIPOTESIS BEKERJA**

---

Setelah Evaluation Engine menentukan bagaimana sebuah trade berakhir, penelitian belum selesai. Kita masih perlu mengubah hasil setiap event menjadi angka yang dapat diringkas, dibandingkan, dan dianalisis.

Misalnya, Evaluation Engine mencatat bahwa suatu event menghasilkan TP_HIT, event lain menghasilkan SL_HIT, dan event berikutnya berakhir TIMEOUT. Status-status tersebut penting, tetapi belum cukup untuk menjawab pertanyaan yang lebih luas:

- Seberapa besar keuntungan atau kerugian yang dihasilkan?
- Berapa rata-rata hasil seluruh event?
- Apakah hasil B1 lebih baik daripada B0?
- Apakah perbedaan tersebut tetap terlihat setelah biaya transaksi?
- Apakah hasil yang lebih baik juga memiliki risiko yang lebih besar?
- Apakah hasil tersebut cukup konsisten untuk dianggap memiliki informasi tambahan?

Bab ini membahas cara mengubah hasil event menjadi ukuran numerik yang dapat dibandingkan. Fokusnya bukan mencari satu angka yang terlihat bagus, melainkan membangun gambaran hasil yang lengkap dan adil.

---

## 15.1. Mengapa Win Rate Saja Tidak Cukup?

**Win rate** adalah proporsi event yang menghasilkan keuntungan atau kemenangan berdasarkan definisi tertentu.

Misalnya, dari 100 trade:

- 70 trade menghasilkan keuntungan.
- 30 trade menghasilkan kerugian.

Maka win rate-nya adalah:

> Win Rate = 70 / 100 = 70%

Angka 70% terlihat menarik. Namun, win rate tidak memberi tahu berapa besar keuntungan dan kerugian dari setiap trade.

Perhatikan dua contoh berikut.

### Strategi A

- 7 trade menang, masing-masing +1%.
- 3 trade kalah, masing-masing -5%.

Total hasil:

> (7 × 1%) − (3 × 5%) = 7% − 15% = -8%

Strategi A memiliki win rate 70%, tetapi hasil totalnya negatif.

### Strategi B

- 4 trade menang, masing-masing +5%.
- 6 trade kalah, masing-masing -1%.

Total hasil:

> (4 × 5%) − (6 × 1%) = 20% − 6% = +14%

Strategi B hanya memiliki win rate sekitar 40%, tetapi hasil totalnya positif.

Contoh ini menunjukkan bahwa:

- Win rate tinggi tidak otomatis berarti menguntungkan.
- Win rate rendah tidak otomatis berarti buruk.
- Besar keuntungan dan besar kerugian harus diperhitungkan.
- Distribusi hasil lebih informatif daripada satu angka kemenangan.

Selain itu, win rate dapat dihitung dengan definisi yang berbeda. Apakah trade dengan return nol dianggap menang, kalah, atau netral? Apakah TP_HIT selalu dianggap profit setelah biaya? Apakah trade TIMEOUT dinilai berdasarkan return positif atau hanya status exit?

Karena itu, definisi win rate harus dinyatakan secara eksplisit. TEKB tidak boleh menggunakan angka win rate tanpa menjelaskan bagaimana angka tersebut dibentuk.

### Apa yang Perlu Dilihat Selain Win Rate?

Beberapa ukuran penting antara lain:

- Return per event.
- Mean return.
- Median return.
- Expectancy.
- Penyebaran hasil.
- Return minimum dan maksimum.
- Percentile bawah dan atas.
- Proporsi kerugian ekstrem.
- Gross expectancy.
- Net expectancy.
- Perbedaan B1 dan B0.

Win rate dapat menjadi salah satu ringkasan, tetapi tidak boleh menjadi satu-satunya dasar kesimpulan.

---

## 15.2. Apa Itu Return?

**Return** adalah ukuran perubahan nilai dari harga entry menuju harga exit atau titik pengukuran tertentu.

Return membantu kita membandingkan hasil antar-event, meskipun harga instrumennya berbeda.

### 1. Return Absolut

Return absolut adalah perubahan harga dalam satuan harga.

> ΔP = P_exit − P_entry

Misalnya:

- Harga entry: Rp1.000.
- Harga exit: Rp1.100.

Maka:

> ΔP = 1.100 − 1.000 = Rp100

Return absolut adalah Rp100 per unit saham.

Namun, angka ini belum memperhitungkan ukuran harga awal. Kenaikan Rp100 memiliki arti berbeda pada saham dengan harga Rp1.000 dan saham dengan harga Rp10.000.

### 2. Return Persentase

Return persentase menyatakan perubahan relatif terhadap harga entry.

> R_% = (P_exit − P_entry) / P_entry

Jika harga entry Rp1.000 dan harga exit Rp1.100:

> R_% = (1.100 − 1.000) / 1.000 = 0,10 = 10%

Return persentase lebih mudah digunakan untuk membandingkan perubahan relatif antar-instrumen.

### 3. Log Return

Dalam kerangka TEKB, return dapat didefinisikan menggunakan **log return**:

> r = ln(P_exit / P_entry)

Untuk return satu periode, bentuknya dapat ditulis:

> r_t+1 = ln(C_t+1 / C_t)

Keterangan:

- P_entry adalah harga awal.
- P_exit adalah harga akhir.
- C_t adalah harga pada waktu t.
- C_t+1 adalah harga pada waktu berikutnya.
- ln adalah logaritma natural.

Untuk perubahan kecil, log return biasanya dekat dengan return persentase biasa. Log return juga memiliki sifat matematis yang berguna ketika perubahan harga dianalisis secara berurutan.

Namun, yang paling penting dalam penelitian bukan sekadar memilih rumus, melainkan menjaga konsistensi. Jika definisi utama menggunakan log return, maka B1 dan B0 harus menggunakan definisi yang sama. Periode IS dan OOS juga harus mengikuti definisi yang sama.

### 4. Return Berdasarkan Harga Entry dan Harga Exit

Return harus dihitung berdasarkan harga entry dan harga keluar yang telah ditentukan oleh protokol.

Misalnya:

- Entry menggunakan Open bar berikutnya.
- Exit TP menggunakan level TP jika tersentuh secara normal.
- Exit gap-through menggunakan Open ketika harga langsung melewati level.
- Exit TIMEOUT menggunakan harga yang ditentukan oleh aturan engine.

Harga sinyal dan harga entry tidak boleh dicampur. Jika sinyal muncul pada Close T tetapi entry terjadi pada Open T+1, return harus dihitung dari harga entry yang benar-benar digunakan dalam penelitian, bukan dari harga sinyal.

### 5. Return Mentah dan Return Bersih

**Return mentah** atau gross return menggambarkan perubahan harga sebelum biaya transaksi.

**Return bersih** atau net return memperhitungkan biaya yang ditentukan dalam model penelitian.

Contohnya:

- Harga entry: Rp1.000.
- Harga exit: Rp1.050.
- Gross return: +5%.
- Total biaya transaksi dan slippage: 1%.

Maka hasil bersih secara sederhana dapat lebih kecil daripada +5%, tergantung cara biaya dimodelkan.

TEKB harus membedakan:

- Harga dan pergerakan harga.
- Gross return.
- Biaya transaksi.
- Net realized result.

Pemisahan ini penting agar pembaca mengetahui apakah suatu hasil positif hanya terlihat pada level harga atau juga masih positif setelah biaya.

---

## 15.3. Apa Itu Expectancy?

**Expectancy** adalah rata-rata hasil yang diperoleh dari seluruh event dalam sampel penelitian berdasarkan definisi hasil yang digunakan.

Secara sederhana:

> Expectancy = Jumlah seluruh hasil / Jumlah event

Misalnya, terdapat lima event dengan hasil:

- +2R
- -1R
- +1R
- -1R
- +3R

Jumlah hasil:

> 2R − 1R + 1R − 1R + 3R = 4R

Maka expectancy:

> Expectancy = 4R / 5 = +0,8R

Artinya, rata-rata hasil dalam sampel tersebut adalah +0,8R per event.

Namun, expectancy bukan berarti setiap trade berikutnya akan menghasilkan +0,8R. Expectancy adalah ukuran rata-rata pada kumpulan event, bukan janji untuk satu trade tertentu.

### Expectancy sebagai Rata-Rata, Bukan Jaminan

Jika expectancy sebuah kelompok adalah +0,5%, itu tidak berarti:

- Setiap trade menghasilkan +0,5%.
- Trade berikutnya pasti menghasilkan +0,5%.
- Semua event memiliki kualitas yang sama.
- Tidak ada kemungkinan kerugian besar.

Expectancy dapat berasal dari berbagai kombinasi:

- Banyak kemenangan kecil dan beberapa kerugian besar.
- Sedikit kemenangan besar dan banyak kerugian kecil.
- Hasil yang relatif merata.
- Hasil yang sangat dipengaruhi oleh beberapa event ekstrem.

Karena itu, expectancy harus dibaca bersama:

- Median.
- Win rate.
- Penyebaran.
- Percentile.
- Kerugian maksimum.
- Jumlah observasi.
- Distribusi B1 dan B0.
- Biaya transaksi.

### Expectancy dan Jumlah Observasi

Expectancy dari lima event tidak memiliki dasar pengamatan yang sama dengan expectancy dari 5.000 event.

Dengan jumlah event kecil:

- Satu hasil ekstrem dapat mengubah rata-rata secara besar.
- Komposisi event mungkin belum mewakili variasi kondisi pasar.
- Ketidakpastian estimasi biasanya lebih besar.

Dengan jumlah event yang lebih besar dan relevan, expectancy dapat menjadi lebih informatif. Namun, jumlah besar saja tidak cukup jika data bias, event saling tumpang tindih secara bermasalah, atau definisi event berubah.

Expectancy harus selalu dibaca sebagai:

> "Rata-rata hasil berdasarkan sampel dan protokol penelitian tertentu."

Bukan sebagai:

> "Keuntungan yang dijamin untuk setiap trade."

---

## 15.4. Mengapa TEKB Menggunakan Satuan R?

Dalam trading, hasil sering kali dinyatakan dalam rupiah atau persentase. Namun, TEKB juga menggunakan satuan **R** untuk menyatakan hasil relatif terhadap unit risiko yang telah didefinisikan.

R bukan angka universal yang selalu sama untuk semua penelitian. R bergantung pada definisi risiko yang digunakan.

### Definisi Dasar R

Secara sederhana:

> R = Satu unit risiko yang ditetapkan oleh protokol

Jika suatu penelitian mendefinisikan risiko sebagai jarak dari entry menuju Stop Loss, maka:

- Kerugian sampai SL dapat disebut -1R.
- Keuntungan yang besarnya dua kali jarak risiko dapat disebut +2R.
- Hasil yang sama dengan harga entry dapat disebut 0R.

Contoh:

- Entry: Rp1.000.
- SL: Rp950.
- Risiko harga: Rp50.
- TP: Rp1.100.
- Keuntungan menuju TP: Rp100.

Maka:

- Risiko 1R = Rp50.
- Kerugian pada SL = -1R.
- Keuntungan pada TP = +2R.

### Contoh Hasil dalam R

| Hasil harga | Hasil dalam R |
|---|---|
| Mencapai SL | -1R |
| Tidak untung atau rugi | 0R |
| Keuntungan sebesar satu unit risiko | +1R |
| Keuntungan sebesar dua unit risiko | +2R |
| Kerugian sebesar dua unit risiko | -2R |

Satuan R membantu membandingkan hasil ketika harga instrumen berbeda atau ketika jarak risiko nominal berbeda.

### Mengapa R-Unit Bergantung pada Definisi Risiko?

R tidak boleh dianggap sebagai satuan yang berdiri sendiri tanpa definisi.

R dapat bergantung pada:

- Harga entry.
- Level SL yang ditetapkan.
- Jarak entry ke SL.
- ATR yang digunakan sebagai dasar jarak.
- Ukuran posisi, jika penelitian memasukkan ukuran posisi.
- Definisi gross atau net.

Karena itu, dua penelitian sama-sama menyebut hasil +2R belum tentu menggunakan definisi R yang sama.

Dalam TEKB, definisi R harus ditulis secara eksplisit dan dibekukan. Pembaca harus dapat mengetahui:

- Apa yang disebut 1R?
- Apakah R berbasis jarak harga atau risiko uang?
- Apakah biaya transaksi sudah masuk?
- Apakah R dihitung berdasarkan candidate SL?
- Bagaimana R diperlakukan untuk TIMEOUT?

Tanpa definisi ini, angka R dapat terlihat presisi tetapi sebenarnya sulit dibandingkan.

### R dan ×ATR

TEKB juga menggunakan satuan ×ATR untuk menormalkan jarak berdasarkan volatilitas. Misalnya:

- SL = 1 × ATR.
- TP = 2 × ATR.

Jika kandidat tersebut digunakan untuk mendefinisikan risiko, maka jarak SL dapat menjadi dasar 1R. Namun, hubungan antara ×ATR dan R harus dinyatakan dengan jelas dalam protokol.

×ATR menjelaskan jarak berdasarkan volatilitas. R menjelaskan hasil relatif terhadap unit risiko. Keduanya berhubungan, tetapi tidak selalu identik secara otomatis.

---

## 15.5. Net Expectancy

Expectancy dapat dihitung sebelum atau sesudah biaya transaksi. Karena itu, TEKB perlu membedakan **gross expectancy** dan **net expectancy**.

### Gross Expectancy

Gross expectancy adalah rata-rata hasil sebelum biaya transaksi.

> E_gross = (Σ R_gross,i) / N

Misalnya, hasil lima event sebelum biaya adalah:

- +2R
- -1R
- +1R
- -1R
- +3R

Gross expectancy:

> E_gross = 4R / 5 = +0,8R

### Net Expectancy

Net expectancy adalah rata-rata hasil setelah biaya transaksi yang dimodelkan.

> E_net = (Σ R_net,i) / N

Misalnya, setiap event memiliki biaya rata-rata 0,1R. Maka secara sederhana:

> E_net = +0,8R − 0,1R = +0,7R

Dalam praktik, biaya dapat berbeda antar-event karena:

- Besar spread berbeda.
- Slippage berbeda.
- Harga entry dan exit berbeda.
- Biaya dapat bergantung pada nilai transaksi.
- Kondisi likuiditas berubah.

Karena itu, net expectancy sebaiknya dihitung dari hasil net setiap event, bukan selalu dengan mengurangi satu biaya rata-rata secara sembarangan.

### Mengapa Net Expectancy Lebih Relevan?

Gross expectancy menunjukkan apakah pergerakan harga secara teoritis menghasilkan rata-rata positif. Namun, trader tidak bertransaksi tanpa biaya.

Biaya dapat mengurangi atau bahkan menghilangkan keunggulan yang terlihat pada gross result.

Contohnya:

- Gross expectancy: +0,15%.
- Biaya dan slippage rata-rata: 0,20%.
- Net expectancy: negatif.

Dalam situasi tersebut, pola mungkin terlihat menarik secara historis, tetapi belum tentu layak secara praktis.

Namun, biaya harus didefinisikan secara eksplisit:

- Komisi.
- Pajak atau pungutan.
- Spread.
- Slippage.
- Biaya lain yang relevan.
- Asumsi harga eksekusi.

Biaya tidak boleh dipilih setelah melihat hasil untuk membuat strategi terlihat baik atau buruk. Model biaya harus ditetapkan sebelum evaluasi dan diterapkan secara konsisten pada B1 dan B0.

---

## 15.6. Mengapa B1 Harus Dibandingkan dengan B0?

**B1** adalah kelompok event yang memenuhi kondisi atau hipotesis yang sedang diteliti. **B0** adalah kelompok pembanding yang dibentuk menggunakan aturan yang adil dan sebanding.

B1 dapat memiliki hasil positif. Namun, hasil positif tersebut belum otomatis menunjukkan adanya information edge.

Mengapa? Karena kondisi pasar secara umum juga dapat menghasilkan return positif.

Misalnya:

- B1, event dengan sinyal tertentu, memiliki mean return +1%.
- B0, event pembanding tanpa kondisi tersebut, juga memiliki mean return +0,9%.

B1 memang positif. Namun, perbedaannya hanya +0,1%. Kita belum dapat langsung menyimpulkan bahwa sinyal memberikan manfaat besar. Bisa jadi sebagian besar kenaikan berasal dari kondisi pasar umum, bukan dari informasi tambahan pada sinyal.

### B1 Positif Belum Cukup

Pertanyaan penelitian yang lebih tepat bukan:

> "Apakah B1 menghasilkan keuntungan?"

Melainkan:

> "Apakah B1 menghasilkan distribusi hasil yang berbeda atau lebih baik daripada B0 yang sebanding?"

B0 membantu memisahkan dua hal:

- Hasil yang mungkin terjadi karena kondisi umum.
- Hasil tambahan yang mungkin berkaitan dengan kondisi yang sedang diteliti.

Misalnya, jika pasar secara umum sedang bullish, banyak event mungkin menghasilkan return positif, bahkan tanpa sinyal tertentu. Tanpa B0, peneliti dapat salah menganggap kenaikan umum tersebut sebagai keunggulan sinyal.

### Konsep Perbedaan B1 dan B0

Secara sederhana, perbedaan dapat ditulis sebagai:

> Δ = E(B1) − E(B0)

Jika yang dibandingkan adalah expectancy, maka:

> ΔE = E_B1 − E_B0

Misalnya:

- Expectancy B1 = +0,8R.
- Expectancy B0 = +0,3R.

Maka:

> ΔE = +0,8R − (+0,3R) = +0,5R

Artinya, rata-rata hasil B1 lebih tinggi 0,5R daripada B0 dalam sampel dan definisi yang digunakan.

Namun, perbedaan ini belum otomatis membuktikan edge yang kuat. Kita masih perlu memeriksa:

- Apakah pasangan B1-B0 dibentuk secara adil?
- Apakah jumlah event memadai?
- Apakah perbedaan dipengaruhi beberapa event ekstrem?
- Apakah median juga lebih baik?
- Apakah distribusi kerugian lebih buruk?
- Apakah perbedaan bertahan setelah biaya?
- Apakah ketidakpastian telah diuji?
- Apakah hasil bertahan pada OOS?

### Membandingkan Lebih dari Satu Ukuran

Perbandingan B1 dan B0 dapat dilakukan pada beberapa ukuran:

| Ukuran | Pertanyaan |
|---|---|
| Mean return | Apakah rata-rata hasil berbeda? |
| Median return | Apakah hasil tengah berbeda? |
| Win rate | Apakah proporsi hasil positif berbeda? |
| Net expectancy | Apakah rata-rata hasil bersih berbeda? |
| Penyebaran | Apakah salah satu kelompok lebih bervariasi? |
| Percentile bawah | Apakah bagian bawah distribusi lebih buruk? |
| Ekor kerugian | Apakah risiko ekstrem berbeda? |
| Peluang melewati ambang | Apakah peluang return tertentu berbeda? |

B1 dapat memiliki mean lebih tinggi tetapi median lebih rendah. B1 dapat memiliki win rate lebih tinggi tetapi ekor kerugian lebih berat. B1 dapat memiliki gross expectancy positif tetapi net expectancy negatif.

Karena itu, information edge tidak boleh didefinisikan hanya sebagai "B1 positif". Yang dicari adalah perbedaan distribusi yang didukung oleh desain penelitian, pembanding adil, pengujian ketidakpastian, dan validasi yang sesuai.

---

## 15.7. Perbedaan Statistik dan Makna Praktis

Dalam penelitian, kita perlu membedakan antara **perbedaan statistik** dan **makna praktis**.

Keduanya berhubungan, tetapi tidak sama.

### Perbedaan Statistik

Perbedaan statistik berkaitan dengan apakah suatu perbedaan cukup didukung oleh data dan metode pengujian yang digunakan, dengan memperhitungkan ketidakpastian.

Misalnya, B1 memiliki expectancy sedikit lebih tinggi daripada B0. Setelah pengujian, perbedaan tersebut mungkin cukup konsisten sehingga kecil kemungkinan muncul hanya karena variasi sampel menurut kriteria yang digunakan.

Namun, hasil yang didukung secara statistik belum tentu berguna secara ekonomi.

### Makna Praktis

Makna praktis berkaitan dengan apakah perbedaan tersebut cukup besar dan cukup relevan untuk digunakan dalam konteks nyata.

Contohnya:

- B1 net expectancy: +0,02R.
- B0 net expectancy: +0,01R.
- Perbedaan: +0,01R.

Perbedaan tersebut mungkin dapat terdeteksi secara statistik jika jumlah data sangat besar dan variasinya kecil. Namun, secara praktis, tambahan +0,01R mungkin terlalu kecil untuk menutup:

- Biaya transaksi.
- Slippage.
- Kesalahan eksekusi.
- Keterlambatan.
- Kapasitas modal.
- Risiko perubahan kondisi pasar.

### Hasil Signifikan tetapi Terlalu Kecil

Sebuah perbedaan dapat terlihat meyakinkan secara statistik, tetapi terlalu kecil untuk memiliki arti praktis.

Misalnya, sinyal meningkatkan rata-rata return sebesar 0,005%. Jika biaya transaksi dan slippage lebih besar daripada tambahan tersebut, maka sinyal mungkin tidak memberikan manfaat nyata.

### Hasil Besar tetapi Tidak Cukup Pasti

Sebaliknya, sebuah hasil dapat terlihat sangat besar, tetapi berasal dari sedikit event atau beberapa outlier.

Misalnya:

- B1 memiliki mean +5R.
- Tetapi sebagian besar keuntungan berasal dari satu event ekstrem.
- Jumlah event hanya 12.
- Median mendekati nol.
- Interval ketidakpastian sangat lebar.

Hasil seperti ini menarik untuk diteliti lebih lanjut, tetapi belum tentu cukup kuat untuk dianggap sebagai edge yang dapat diandalkan.

### Hasil Positif tetapi Tidak Stabil

Hasil juga dapat positif pada satu periode tetapi hilang pada periode lain.

Contohnya:

- Positif pada pasar bullish.
- Netral pada pasar sideways.
- Negatif pada pasar bearish.

Atau:

- Positif pada beberapa saham.
- Negatif pada saham lain.
- Positif hanya pada satu tahun tertentu.

Ketidakstabilan seperti ini harus diperiksa melalui pembagian waktu, instrumen, analisis sensitivitas, dan OOS sesuai protokol.

### Statistik dan Praktis Harus Dibaca Bersama

Penelitian yang baik menggabungkan dua pertanyaan:

1. Apakah perbedaan tersebut cukup didukung oleh data?
2. Apakah perbedaan tersebut cukup besar dan relevan untuk memiliki arti praktis?

Keduanya dapat menghasilkan kombinasi yang berbeda:

| Kondisi | Makna |
|---|---|
| Signifikan dan besar | Menarik secara statistik dan praktis |
| Signifikan tetapi kecil | Terlihat secara statistik, tetapi mungkin tidak berguna secara ekonomi |
| Besar tetapi tidak pasti | Menarik, tetapi membutuhkan bukti tambahan |
| Tidak signifikan dan kecil | Belum ada bukti kuat tentang manfaat |
| Positif tetapi tidak stabil | Perlu pemeriksaan generalisasi dan ketahanan |

Dalam TEKB, sebuah kandidat tidak cukup hanya menghasilkan angka positif. Kandidat perlu melewati proses yang mempertimbangkan perbedaan B1-B0, ketidakpastian, biaya, konsistensi, dan validasi OOS.

---

## Penutup Bab

Mengubah hasil event menjadi angka yang dapat dibandingkan adalah tahap penting dalam penelitian TEKB. Namun, tujuan pengukuran bukan mencari angka yang paling indah. Tujuannya adalah membuat hasil dapat dibaca secara adil dan lengkap.

Win rate membantu melihat proporsi kemenangan, tetapi tidak menunjukkan besar keuntungan dan kerugian. Return membantu menyatakan perubahan harga secara relatif. Expectancy merangkum rata-rata hasil, tetapi bukan jaminan trade berikutnya. Satuan R membantu menyatakan hasil relatif terhadap risiko yang telah didefinisikan.

Gross expectancy menunjukkan hasil sebelum biaya, sedangkan net expectancy membantu melihat hasil setelah biaya transaksi. B1 harus dibandingkan dengan B0 karena hasil positif pada B1 belum tentu merupakan informasi tambahan.

Akhirnya, perbedaan statistik dan makna praktis harus dibaca bersama. Hasil yang terlihat positif belum tentu cukup pasti. Hasil yang cukup pasti belum tentu cukup besar untuk berguna.

Dengan demikian, TEKB tidak bertanya hanya:

> "Berapa besar hasilnya?"

TEKB juga bertanya:

> "Dibandingkan dengan apa, dihitung dengan definisi apa, seberapa stabil, seberapa pasti, dan apakah perbedaannya memiliki arti praktis?"

---

## Ringkasan Bab

- Win rate saja tidak cukup karena tidak menunjukkan besar keuntungan dan kerugian.
- Return dapat dinyatakan sebagai perubahan absolut, persentase, atau log return.
- Return harus dihitung dari harga entry dan harga exit yang ditetapkan protokol.
- Gross return berbeda dari net return setelah biaya transaksi.
- Expectancy adalah rata-rata hasil berdasarkan sampel, bukan jaminan trade berikutnya.
- Expectancy harus dibaca bersama median, penyebaran, jumlah observasi, dan ekor distribusi.
- R adalah satuan hasil relatif terhadap unit risiko yang didefinisikan penelitian.
- Definisi R harus eksplisit karena R tidak memiliki arti universal yang otomatis sama.
- Net expectancy lebih relevan untuk pertimbangan praktis, tetapi biaya harus dimodelkan secara jelas.
- B1 positif belum cukup; B1 harus dibandingkan dengan B0.
- Information edge berkaitan dengan perbedaan distribusi B1 dan B0 yang didukung bukti.
- Perbedaan statistik tidak selalu sama dengan makna praktis.
- Hasil besar tetapi tidak pasti, atau hasil signifikan tetapi terlalu kecil, harus ditafsirkan secara hati-hati.

---

## Pertanyaan Refleksi

1. Mengapa win rate 70% belum tentu lebih baik daripada win rate 40%?
2. Apa perbedaan return absolut, return persentase, dan log return?
3. Mengapa return harus dihitung dari harga entry, bukan hanya dari harga sinyal?
4. Apa yang dimaksud dengan expectancy?
5. Mengapa expectancy bukan jaminan hasil trade berikutnya?
6. Apa arti +2R dan -1R?
7. Mengapa definisi R harus ditetapkan secara eksplisit?
8. Apa perbedaan gross expectancy dan net expectancy?
9. Mengapa B1 yang positif belum cukup untuk menyatakan adanya information edge?
10. Apa yang dimaksud dengan perbedaan B1 dan B0?
11. Mengapa hasil yang signifikan secara statistik belum tentu bermakna secara praktis?
12. Mengapa hasil besar tetapi berasal dari sedikit event perlu dicurigai?
13. Mengapa stabilitas hasil perlu diperiksa di luar satu periode penelitian?

---

## Kalimat Kunci

> Angka yang baik bukan hanya angka yang positif, melainkan angka yang memiliki definisi jelas, dapat dibandingkan secara adil, memperhitungkan risiko dan biaya, serta didukung oleh bukti yang memadai.

---

<div align="center">

[← Bab Sebelumnya](/posts/bab-14-evaluation-engine/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Bab Selanjutnya →](/posts/bab-16-bootstrap/)

</div>