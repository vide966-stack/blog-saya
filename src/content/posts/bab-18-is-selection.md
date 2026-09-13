---
title: "BAB 18 — IS Selection: Bagaimana Memilih Kandidat Tanpa Terjebak Data?"
published: 2026-09-12
description: "IS Selection adalah proses memilih kandidat berdasarkan aturan yang telah dibekukan, bukan memilih angka tertinggi. Bab ini menjelaskan syarat kelulusan, tie-break, dan NO_EDGE_FOUND."
tags: ["bab-18", "is-selection", "provenance", "tie-break"]
category: "Bab"
draft: false
lang: ""
---

**BAGIAN V — MESIN YANG MENENTUKAN APAKAH SEBUAH HIPOTESIS BEKERJA**

---

## Tujuan Bab

Setelah memahami event, entry, B0, MAE/MFE, ATR, evaluation engine, distribusi hasil, bootstrap, dan multiple testing, pembaca sampai pada tahap penting: memilih kandidat hipotesis yang layak dibawa ke pengujian Out-of-Sample atau OOS.

Tahap ini disebut **In-Sample Selection**, atau pemilihan kandidat di dalam data In-Sample.

Di sinilah banyak penelitian trading dapat mengalami masalah. Peneliti mungkin menguji banyak kombinasi:

- Ambang volume.
- Stop-loss.
- Take-profit.
- Horizon.
- Durasi holding.
- Filter kondisi pasar.
- Variasi entry.
- Variasi indikator.

Kemudian, dari seluruh kombinasi tersebut, dipilih satu yang menghasilkan angka paling tinggi.

Sekilas, proses itu terlihat masuk akal. Namun, jika pemilihan dilakukan tanpa aturan yang jelas, kandidat terbaik bisa saja hanya merupakan hasil kebetulan dari banyak percobaan.

Karena itu, TEKB tidak mendefinisikan IS Selection sebagai:

> "Pilih hasil yang paling menguntungkan."

TEKB mendefinisikannya sebagai:

> "Pilih kandidat yang memenuhi kriteria kelayakan, memiliki perbedaan yang mendukung terhadap B0, cukup kuat secara statistik, dan lolos aturan seleksi yang telah ditentukan sebelumnya."

Jika tidak ada kandidat yang memenuhi seluruh syarat, hasil yang sah adalah:

**NO_EDGE_FOUND**

Penelitian tidak boleh dipaksa menghasilkan strategi hanya karena peneliti menginginkan sebuah strategi.

---

## 18.1. Apa Itu In-Sample?

### 18.1.1. Pengertian In-Sample

**In-Sample**, atau **IS**, adalah bagian data yang digunakan untuk membangun, mengembangkan, menguji, dan memilih hipotesis penelitian.

Dalam TEKB, data IS dapat digunakan untuk:

- Menentukan definisi event.
- Menguji apakah suatu kondisi layak diteliti.
- Mengevaluasi kandidat parameter.
- Mengukur distribusi hasil.
- Membandingkan B1 dengan B0.
- Menguji ketidakpastian.
- Melakukan multiple testing.
- Memilih kandidat yang akan dibekukan.

Contohnya, peneliti memiliki data tahun 2016–2025. Data tersebut dapat dibagi menjadi:

- IS: 2016–2021.
- OOS: 2022–2025.

Pembagian ini hanya contoh. Batas aktual harus ditentukan dalam kontrak penelitian dan tidak boleh diubah secara oportunistis setelah hasil diketahui.

### 18.1.2. IS digunakan untuk membangun dan memilih hipotesis

Misalkan peneliti ingin menguji apakah anomali volume berhubungan dengan pergerakan harga setelah tiga bar.

Peneliti dapat menguji beberapa kandidat:

| Kandidat | Ambang RV | Horizon | Aturan Exit |
|---|---|---|---|
| A | > 2,5 | 3 bar | Grid 1 |
| B | > 3,0 | 3 bar | Grid 1 |
| C | > 5,0 | 3 bar | Grid 1 |
| D | > 3,0 | 5 bar | Grid 2 |

Data IS digunakan untuk melihat bagaimana kandidat-kandidat tersebut bekerja menurut definisi dan evaluation engine yang sama.

Namun, hasil IS tidak boleh dianggap sebagai bukti final bahwa kandidat akan bekerja pada semua data masa depan.

IS adalah tempat untuk:

- Meneliti.
- Membandingkan.
- Menyaring.
- Memilih.
- Membekukan hipotesis.

IS bukan tempat untuk mengklaim bahwa generalisasi telah terbukti.

### 18.1.3. Mengapa IS bukan bukti generalisasi final?

Kandidat dipilih berdasarkan data IS. Karena itu, kandidat tersebut telah "berinteraksi" dengan data IS melalui proses penelitian.

Semakin banyak pilihan dan percobaan dilakukan, semakin besar peluang suatu kandidat terlihat bagus hanya karena menyesuaikan diri dengan karakteristik khusus data IS.

Contohnya, seorang peneliti mencoba 1.000 kombinasi aturan. Walaupun sebagian besar kombinasi sebenarnya tidak memiliki informasi yang berguna, beberapa kombinasi mungkin terlihat sangat baik hanya karena kebetulan.

Jika satu kombinasi dipilih berdasarkan hasil tersebut, angka yang terlihat dapat terlalu optimistis.

Oleh sebab itu:

> IS digunakan untuk memilih hipotesis, sedangkan OOS digunakan untuk menguji apakah hipotesis yang telah dipilih masih menunjukkan hasil yang mendukung pada data yang tidak digunakan dalam proses pemilihan.

### 18.1.4. Perbedaan IS dan OOS

| Aspek | In-Sample | Out-of-Sample |
|---|---|---|
| Fungsi utama | Membangun dan memilih hipotesis | Menguji generalisasi |
| Kandidat boleh diubah? | Ya, sesuai proses penelitian yang terdokumentasi | Tidak untuk memperbaiki hasil |
| Digunakan untuk tuning? | Ya | Tidak |
| Digunakan untuk memilih kandidat? | Ya | Tidak |
| Digunakan untuk keputusan final OOS? | Ya, melalui aturan yang telah ditetapkan | Ya, hanya sebagai pengujian |
| Risiko overfitting | Tinggi jika terlalu banyak eksplorasi | Lebih terlindungi, tetapi tidak hilang |
| Status hasil | Kandidat terpilih atau tidak | OOS_VALIDATED atau OOS_REJECTED |

OOS bukan tempat untuk mencoba kembali kandidat sampai hasilnya bagus. Jika peneliti terus mengubah aturan berdasarkan hasil OOS, data OOS secara perlahan berubah fungsi menjadi IS tambahan.

---

## 18.2. Mengapa Kandidat Harus Dipilih dengan Aturan yang Dibekukan?

### 18.2.1. Pemilihan subjektif mudah menipu

Bayangkan peneliti menguji sepuluh kandidat. Hasilnya:

| Kandidat | Expectancy |
|---|---|
| A | 0,10 |
| B | 0,15 |
| C | 0,08 |
| D | 0,22 |
| E | 0,13 |
| F | 0,18 |
| G | 0,05 |
| H | 0,20 |
| I | 0,12 |
| J | 0,17 |

Peneliti mungkin langsung memilih kandidat D karena memiliki expectancy tertinggi.

Namun, belum diketahui:

- Apakah perbedaannya terhadap B0 positif?
- Apakah hasilnya signifikan?
- Apakah hasilnya stabil?
- Apakah kandidat D hanya ditopang beberapa event ekstrem?
- Apakah jumlah event cukup?
- Apakah data lengkap?
- Apakah kandidat D lolos pada worst-case?
- Apakah kandidat D lolos setelah koreksi multiple testing?

Jika semua pertanyaan tersebut belum dijawab, pemilihan berdasarkan angka tertinggi hanyalah pemilihan nominal.

### 18.2.2. Aturan harus ditetapkan sebelum hasil digunakan untuk memilih

Aturan pemilihan harus ditentukan sebelum hasil kandidat digunakan untuk mengambil keputusan seleksi.

Aturan tersebut perlu menjelaskan:

- Apa yang dibandingkan.
- Unit perbandingan.
- Metrik yang digunakan.
- Syarat kelayakan data.
- Syarat perbedaan terhadap B0.
- Syarat signifikansi.
- Cara menangani multiple testing.
- Cara menangani kandidat yang seri.
- Cara menangani data yang tidak lengkap.
- Kapan status NO_EDGE_FOUND digunakan.

Dengan aturan yang dibekukan, peneliti tidak dapat dengan mudah mengubah kriteria hanya karena kandidat favoritnya gagal.

Contoh aturan yang tidak sehat:

> "Jika kandidat tidak signifikan, kita turunkan ambang signifikansinya."

Contoh lain:

> "Jika worst-case gagal, kita hanya tampilkan best-case karena lebih menarik."

Perubahan seperti ini dapat membuat hasil terlihat lebih baik, tetapi mengurangi kejujuran penelitian.

### 18.2.3. Aturan yang dibekukan menjaga keterulangan

Penelitian yang baik harus dapat diulang oleh peneliti lain atau oleh versi sistem yang berbeda.

Jika dua peneliti menggunakan data dan hasil yang sama, tetapi satu memilih kandidat berdasarkan expectancy dan yang lain memilih berdasarkan grafik yang terlihat menarik, mereka dapat menghasilkan kesimpulan berbeda.

Aturan seleksi yang dibekukan mengurangi ketergantungan pada selera pribadi.

Misalnya:

1. Kandidat harus memiliki data yang memenuhi syarat.
2. B1 Worst − B0 Worst harus positif.
3. B1 Best − B0 Best harus positif.
4. Kedua perbedaan harus memenuhi syarat signifikansi.
5. Kandidat harus lolos BH-FDR dalam keluarga pengujiannya.
6. Jika beberapa kandidat lolos, gunakan tie-break yang telah ditentukan.
7. Jika tidak ada kandidat lolos, tetapkan NO_EDGE_FOUND.

Dengan aturan seperti ini, proses seleksi dapat dijalankan secara konsisten.

### 18.2.4. Frozen rule bukan berarti tidak boleh ada penelitian baru

Aturan yang dibekukan berlaku untuk satu proses seleksi atau satu kontrak penelitian tertentu. Ini tidak berarti peneliti tidak boleh melakukan eksperimen baru.

Peneliti tetap boleh:

- Membuat hipotesis baru.
- Mengubah grid untuk eksperimen berikutnya.
- Menguji timeframe lain.
- Menguji definisi event lain.
- Mengubah evaluation engine melalui versi baru.
- Menguji kelompok instrumen lain.

Namun, perubahan tersebut harus dicatat sebagai percobaan baru dengan provenance yang jelas. Hasil baru tidak boleh disamarkan seolah-olah berasal dari proses penelitian lama yang sama.

---

## 18.3. Unit Perbandingan: Pasangan B1 dan B0

### 18.3.1. Apa itu B1 dan B0?

Dalam TEKB:

- **B1** adalah observasi yang berasal dari event atau kondisi yang sedang diteliti.
- **B0** adalah observasi pembanding yang dipilih berdasarkan aturan pembanding yang telah ditetapkan.

B1 dan B0 tidak boleh dipahami sebagai dua kelompok yang boleh diringkas sembarangan sejak awal. Dalam desain TEKB, keduanya membentuk pasangan observasi.

Contoh:

| Pair ID | Timestamp B1 | Return B1 | Timestamp B0 | Return B0 |
|---|---|---|---|---|
| P001 | 2020-03-05 09.30 | 1,2% | 2020-03-04 09.30 | 0,3% |
| P002 | 2020-03-10 10.15 | -0,5% | 2020-03-09 10.15 | 0,1% |
| P003 | 2020-04-02 11.00 | 2,0% | 2020-04-01 11.00 | 0,4% |

Pasangan tersebut memungkinkan peneliti menghitung perbedaan pada unit yang sama:

> D_i = B1_i − B0_i

Jika metrik yang dibandingkan adalah return, maka:

> D_i = Return(B1_i) − Return(B0_i)

Jika metrik yang dibandingkan adalah expectancy atau hasil evaluasi tertentu, definisi perbedaannya harus mengikuti kontrak penelitian.

### 18.3.2. Mengapa pasangan harus dipertahankan?

Pasangan B1/B0 mempertahankan hubungan antara event dan pembandingnya.

Misalnya:

- B1 terjadi pada instrumen tertentu.
- B1 memiliki timestamp tertentu.
- B1 memiliki kondisi sesi atau slot tertentu.
- B0 dipilih untuk mewakili kondisi pembanding yang relevan.

Jika semua B1 dan B0 langsung digabung menjadi dua angka rata-rata tanpa mempertahankan pasangan, struktur hubungan tersebut dapat hilang.

Contoh:

| Pair | B1 | B0 | Selisih |
|---|---|---|---|
| 1 | 10 | 9 | +1 |
| 2 | 2 | 1 | +1 |
| 3 | -8 | -9 | +1 |

Rata-rata B1:

> (10 + 2 − 8) / 3 = 1,33

Rata-rata B0:

> (9 + 1 − 9) / 3 = 0,33

Perbedaan rata-rata:

> 1,33 − 0,33 = 1

Dalam contoh ini, hasilnya sama dengan rata-rata selisih karena jumlah pasangan sama. Namun, dalam proses statistik dan bootstrap, informasi tentang pasangan tetap penting karena unit resampling dan ketergantungannya ditentukan berdasarkan pasangan, bukan sekadar dua kumpulan angka terpisah.

### 18.3.3. Anchor pada timestamp B1

Dalam TEKB, pasangan biasanya **di-anchor pada timestamp B1**.

Artinya, identitas utama pasangan mengikuti event yang sedang diteliti. B0 dipilih sebagai pembanding terhadap event tersebut.

Contoh:
research_pair_id = P001
b1_timestamp = 2020-03-05 09:30
b0_timestamp = 2020-03-04 09:30
anchor_timestamp = 2020-03-05 09:30

Mengapa anchor penting?

Karena satu event B1 dapat memiliki:

- Definisi event tertentu.
- Instrumen tertentu.
- Slot tertentu.
- Entry tertentu.
- Horizon tertentu.
- Versi aturan tertentu.

B0 adalah pasangan untuk event tersebut, bukan observasi bebas yang dapat dipindahkan sesuka hati.

### 18.3.4. Agregasi tidak boleh menghilangkan struktur pasangan

Peneliti boleh menghitung statistik agregat, seperti:

- Rata-rata B1.
- Rata-rata B0.
- Rata-rata selisih.
- Median selisih.
- Persentil selisih.
- Proporsi pasangan dengan selisih positif.

Namun, data dasar pasangan harus tetap dipertahankan.

Mengapa?

Karena penelitian mungkin perlu:

- Melakukan paired bootstrap.
- Memeriksa pasangan ekstrem.
- Menelusuri event tertentu.
- Mengidentifikasi konsentrasi hasil.
- Menganalisis ketergantungan berdasarkan tanggal.
- Memeriksa apakah hasil hanya berasal dari satu instrumen.
- Mengulang evaluation engine.
- Melakukan audit terhadap pasangan tertentu.

Jika struktur pasangan dihapus sejak awal, proses audit dan pengujian menjadi lebih sulit atau bahkan tidak mungkin dilakukan.

### 18.3.5. Pasangan bukan jaminan otomatis bebas bias

Mempertahankan pasangan B1/B0 tidak otomatis membuat penelitian bebas bias.

Pasangan tetap harus dibentuk dengan aturan yang adil:

- Instrumen sesuai.
- Slot waktu sesuai.
- Sesi sesuai.
- Partisi IS/OOS sesuai.
- B0 tidak menggunakan outcome masa depan.
- Aturan pemilihan B0 telah ditentukan.
- Tidak terjadi reuse yang melanggar kontrak.
- Pasangan yang tidak sah tidak dipaksakan.

Pasangan adalah struktur desain yang membantu perbandingan. Keadilan pasangan tetap bergantung pada aturan pembentukannya.

---

## 18.4. Syarat Kelulusan TEKB

Dalam TEKB, kandidat tidak cukup hanya memiliki hasil positif. Kandidat harus memenuhi seluruh syarat kelulusan yang telah ditetapkan.

### 18.4.1. B1 Worst dibandingkan dengan B0 Worst

Jika evaluation engine menghasilkan skenario worst-case dan best-case, kedua skenario harus dianalisis secara terpisah.

Perbandingan pertama adalah:

> B1_Worst dibandingkan dengan B0_Worst

Perbedaan dapat ditulis sebagai:

> D_Worst,i = B1_Worst,i − B0_Worst,i

Kemudian penelitian menghitung statistik agregat yang sesuai, misalnya rata-rata perbedaan:

> D̄_Worst = (1/N) × Σ D_Worst,i

Syarat dasarnya:

> D̄_Worst > 0

Artinya, dalam definisi yang digunakan, hasil B1 worst harus lebih baik daripada B0 worst.

Namun, tanda positif saja belum cukup. Perbedaan tersebut juga harus memenuhi syarat ketidakpastian atau signifikansi yang ditetapkan.

### 18.4.2. B1 Best dibandingkan dengan B0 Best

Perbandingan kedua adalah:

> B1_Best dibandingkan dengan B0_Best

Perbedaannya:

> D_Best,i = B1_Best,i − B0_Best,i

Kemudian dihitung statistik agregat:

> D̄_Best = (1/N) × Σ D_Best,i

Syarat dasarnya:

> D̄_Best > 0

Dalam kontrak TEKB yang mengharuskan robustness terhadap kedua skenario, kandidat harus menunjukkan hasil yang mendukung baik pada worst-case maupun best-case.

Tujuannya bukan untuk menyatakan bahwa worst-case dan best-case adalah hasil nyata yang pasti terjadi. Keduanya adalah batas atau skenario evaluasi yang digunakan untuk menghadapi ambiguitas intrabar dan ketidakpastian urutan kejadian.

### 18.4.3. Kedua perbedaan harus memenuhi syarat signifikansi

Kandidat tidak lulus hanya karena:

> B1 Worst > B0 Worst
> B1 Best > B0 Best

Perbedaan positif dapat muncul secara kebetulan, terutama jika:

- Jumlah event kecil.
- Banyak kandidat diuji.
- Distribusi sangat tidak merata.
- Beberapa event ekstrem mendominasi.
- Event saling bergantung.
- Ada pemilihan kandidat setelah melihat hasil.

Karena itu, TEKB mensyaratkan bahwa perbedaan harus memenuhi kriteria signifikansi atau ketidakpastian yang telah ditetapkan.

Contoh sederhana:

| Skenario | Mean Difference | Q-value | Status |
|---|---|---|---|
| Worst | +0,20R | 0,03 | Lulus |
| Best | +0,35R | 0,04 | Lulus |

Jika ambang yang digunakan adalah:

> q < α

dan α = 0,05, maka kedua skenario memenuhi syarat tersebut.

Sebaliknya:

| Skenario | Mean Difference | Q-value | Status |
|---|---|---|---|
| Worst | +0,20R | 0,03 | Lulus |
| Best | +0,35R | 0,18 | Gagal |

Walaupun kedua mean positif, kandidat tidak memenuhi syarat kelulusan jika kontrak mensyaratkan keduanya signifikan.

### 18.4.4. BH-FDR diterapkan pada keluarga masing-masing

Ketika banyak kandidat diuji, sebagian hasil dapat terlihat signifikan hanya karena jumlah pengujian yang besar. Oleh sebab itu, TEKB memperhatikan masalah multiple testing.

BH-FDR atau Benjamini–Hochberg False Discovery Rate dapat digunakan untuk mengendalikan proporsi penemuan positif palsu yang diharapkan dalam suatu keluarga pengujian.

Namun, BH-FDR tidak diterapkan secara sembarangan terhadap semua angka yang pernah dihitung. Keluarga pengujian harus didefinisikan dan dicatat.

Dalam kontrak TEKB, keluarga worst-case dan best-case diperlakukan secara terpisah jika memang keduanya merupakan himpunan pengujian yang berbeda.

Contoh:
multiple_testing_family_id = FAMILY_WORST_V1
multiple_testing_family_id = FAMILY_BEST_V1

Secara konseptual:

1. Kumpulkan hasil pengujian dalam keluarga worst-case.
2. Terapkan prosedur BH-FDR pada keluarga tersebut.
3. Tentukan q-value atau status kelulusan worst-case.
4. Lakukan proses yang sesuai untuk keluarga best-case.

Kandidat harus memenuhi syarat pada kedua keluarga jika kontrak mensyaratkannya.

Penting untuk dipahami:

> BH-FDR bukan alat untuk membuat hasil yang tidak signifikan menjadi benar.

BH-FDR hanya membantu mengoreksi penilaian ketika banyak hipotesis diuji dalam suatu keluarga. Ia tidak menghapus bias desain, data leakage, look-ahead, atau eksplorasi lintas percobaan yang tidak tercatat.

### 18.4.5. Kandidat harus memenuhi syarat kelayakan data

Sebelum membahas signifikansi, kandidat harus memiliki data yang layak untuk dievaluasi.

Syarat kelayakan dapat meliputi:

- Event memenuhi definisi.
- Entry valid.
- B0 valid.
- Pasangan B1/B0 lengkap sesuai kebutuhan.
- Horizon evaluasi tersedia.
- ATR tersedia jika diperlukan.
- Evaluation engine dapat dijalankan.
- Tidak ada pelanggaran look-ahead.
- Data tidak rusak.
- Jumlah observasi memenuhi minimum yang ditetapkan.
- Status pengukuran tidak didominasi data tidak lengkap.

Data yang tidak lengkap tidak boleh diam-diam diperlakukan sebagai hasil nol atau hasil buruk tanpa dasar kontrak.

Contoh status:

- COMPUTED_FULL_HORIZON
- INSUFFICIENT_HORIZON
- INVALIDATED
- NO_MATCH_FOUND

Kandidat dengan jumlah event yang terlalu sedikit atau terlalu banyak data tidak valid dapat dinyatakan tidak layak dievaluasi, meskipun angka agregatnya terlihat menarik.

### 18.4.6. Ringkasan syarat kelulusan

Secara ringkas, kandidat TEKB dapat digambarkan sebagai berikut:

Kandidat memiliki data layak?
├─ Tidak → Gagal
└─ Ya
↓
B1 Worst − B0 Worst positif?
├─ Tidak → Gagal
└─ Ya
↓
Worst-case memenuhi signifikansi/FDR?
├─ Tidak → Gagal
└─ Ya
↓
B1 Best − B0 Best positif?
├─ Tidak → Gagal
└─ Ya
↓
Best-case memenuhi signifikansi/FDR?
├─ Tidak → Gagal
└─ Ya
↓
Kandidat memenuhi seluruh syarat
→ Eligible for IS Selection / Freeze

Kandidat yang lolos tahap ini belum otomatis terbukti berlaku di masa depan. Ia baru layak dibawa ke tahap pembekuan dan pengujian OOS.

---

## 18.5. Mengapa Tidak Cukup Memilih Expectancy Tertinggi?

### 18.5.1. Expectancy penting, tetapi tidak berdiri sendiri

Expectancy adalah salah satu metrik penting dalam evaluasi trading. Secara sederhana, expectancy menggambarkan hasil rata-rata yang diharapkan berdasarkan distribusi hasil yang diamati.

Namun, expectancy tertinggi tidak otomatis berarti kandidat tersebut paling dapat dipercaya.

Misalnya:

| Kandidat | Expectancy | Jumlah Event | Median | Hasil Terburuk |
|---|---|---|---|---|
| A | +0,40R | 20 | +0,05R | -3,0R |
| B | +0,22R | 500 | +0,18R | -1,2R |
| C | +0,30R | 80 | +0,10R | -2,0R |

Kandidat A memiliki expectancy tertinggi. Namun, hasilnya mungkin sangat dipengaruhi oleh satu atau dua event ekstrem.

Kandidat B memiliki expectancy lebih rendah, tetapi:

- Jumlah event lebih besar.
- Median lebih dekat dengan mean.
- Hasil lebih merata.
- Kerugian terburuk lebih kecil.
- Distribusi mungkin lebih stabil.

Kandidat B belum tentu otomatis lebih baik, tetapi contoh ini menunjukkan bahwa expectancy harus dibaca bersama metrik lain.

### 18.5.2. Hasil tinggi dapat berasal dari beberapa event ekstrem

Misalkan 100 event menghasilkan:

- 95 event: sekitar 0R.
- 4 event: +0,5R.
- 1 event: +20R.

Mean dapat menjadi positif tinggi karena satu event +20R.

Namun, apakah pola tersebut dapat diandalkan? Belum tentu.

Peneliti perlu memeriksa:

- Apakah event ekstrem tersebut valid?
- Apakah event berasal dari satu tanggal?
- Apakah event berasal dari satu instrumen?
- Apakah event terjadi karena kondisi yang sangat jarang?
- Apakah event tersebut masih ada dalam analisis worst-case?
- Apakah hasil tetap mendukung jika event ekstrem dikeluarkan sebagai analisis sensitivitas?
- Apakah distribusi median dan persentil juga mendukung?

Event ekstrem tidak boleh dihapus hanya karena merusak hasil. Namun, pengaruhnya harus dipahami dan dicatat.

### 18.5.3. Kandidat terbaik secara nominal belum tentu terbaik secara statistik

"Terbaik secara nominal" berarti memiliki angka hasil paling tinggi dalam sampel yang diamati.

"Terbaik secara statistik" berarti memiliki dukungan yang lebih baik setelah mempertimbangkan:

- Ketidakpastian.
- Variasi sampel.
- Multiple testing.
- Pembanding B0.
- Jumlah observasi.
- Dependensi event.
- Robustness.
- Kelayakan data.

Contoh:

| Kandidat | Mean Difference | Interval Ketidakpastian | Status |
|---|---|---|---|
| A | +0,50R | Sangat lebar | Tidak stabil |
| B | +0,25R | Lebih sempit | Lebih konsisten |
| C | +0,18R | Lebih sempit | Konsisten |

Kandidat A mungkin memiliki angka tertinggi, tetapi ketidakpastiannya sangat besar. Kandidat B mungkin lebih layak karena hasilnya lebih konsisten dan tetap mengungguli B0.

Sekali lagi, ini tidak berarti kandidat dengan angka lebih rendah selalu lebih baik. Maksudnya adalah bahwa angka tertinggi harus melewati pemeriksaan tambahan sebelum dianggap layak.

### 18.5.4. Pembanding B0 harus tetap menjadi pusat

Kandidat tidak dinilai hanya dari hasil absolutnya.

Misalnya, kandidat menghasilkan expectancy +0,10R. Angka tersebut tampak positif. Namun, jika B0 menghasilkan +0,15R, maka kandidat justru lebih buruk daripada pembanding.

Sebaliknya, kandidat menghasilkan +0,05R, sedangkan B0 menghasilkan -0,10R. Perbedaan relatifnya mungkin mendukung kandidat, meskipun hasil absolutnya kecil.

Karena itu, pertanyaan TEKB bukan sekadar:

> "Apakah kandidat menghasilkan keuntungan?"

Pertanyaan yang lebih tepat:

> "Apakah kandidat menghasilkan hasil yang lebih baik daripada kondisi pembanding yang adil, dengan ketidakpastian yang dapat diterima?"

### 18.5.5. Expectancy harus dibaca bersama distribusi

Selain expectancy, penelitian perlu melihat:

- Mean.
- Median.
- Persentil.
- Proporsi hasil positif.
- Tail loss.
- Tail gain.
- MAE.
- MFE.
- Jumlah event.
- Jumlah instrumen.
- Konsentrasi hasil.
- Hasil per periode.
- Hasil per instrumen.
- Hasil worst-case dan best-case.
- Hasil terhadap B0.

Distribusi membantu menjawab apakah mean mewakili sebagian besar event atau hanya dipengaruhi oleh sejumlah kecil observasi.

---

## 18.6. Tie-Break

### 18.6.1. Tie-break bukan alat untuk menyelamatkan kandidat gagal

Tie-break digunakan ketika beberapa kandidat telah memenuhi seluruh syarat kelulusan dan perlu dipilih satu atau beberapa kandidat yang paling sesuai dengan prioritas penelitian.

Tie-break tidak boleh digunakan untuk membuat kandidat yang gagal menjadi lolos.

Urutannya harus jelas:

Uji kelayakan
↓
Uji perbedaan terhadap B0
↓
Uji signifikansi dan FDR
↓
Kandidat lolos
↓
Baru gunakan tie-break

Contoh yang tidak benar:

> "Kandidat A gagal pada worst-case, tetapi expectancy-nya paling tinggi, jadi tetap dipilih."

Itu bukan tie-break. Itu adalah pengabaian terhadap syarat kelulusan.

### 18.6.2. Urutan tie-break TEKB

Dalam kontrak TEKB, tie-break dilakukan dengan urutan berikut:

1. Worst-case expectancy tertinggi.
2. Jumlah event evaluated terbesar.
3. Max hold terkecil.

Urutan ini harus diterapkan secara konsisten.

### 18.6.3. Tie-break pertama: Worst-case expectancy tertinggi

Jika beberapa kandidat sama-sama lolos, kandidat dengan expectancy worst-case yang lebih tinggi diprioritaskan.

Contoh:

| Kandidat | Worst Expectancy | Status |
|---|---|---|
| A | +0,18R | Lolos |
| B | +0,25R | Lolos |
| C | +0,20R | Lolos |

Dengan tie-break pertama, kandidat B berada di urutan teratas karena memiliki worst-case expectancy tertinggi.

Mengapa worst-case digunakan terlebih dahulu?

Karena TEKB tidak ingin memilih kandidat hanya berdasarkan skenario yang paling menguntungkan. Worst-case membantu memberikan prioritas pada kandidat yang tetap lebih baik dalam kondisi evaluasi yang lebih konservatif.

### 18.6.4. Tie-break kedua: Jumlah event evaluated terbesar

Jika dua kandidat memiliki worst-case expectancy yang sama atau sangat dekat sesuai aturan pembulatan yang ditetapkan, pertimbangan berikutnya adalah jumlah event yang benar-benar dievaluasi.

Contoh:

| Kandidat | Worst Expectancy | Event Evaluated |
|---|---|---|
| A | +0,20R | 150 |
| B | +0,20R | 420 |

Kandidat B diprioritaskan karena didukung oleh jumlah event evaluated yang lebih besar.

Jumlah event yang lebih banyak tidak otomatis menjamin kebenaran, tetapi biasanya memberikan lebih banyak informasi dibandingkan kandidat yang hanya didukung oleh sedikit observasi, selama kualitas dan dependensi data tetap diperhatikan.

Penting untuk membedakan:

- Jumlah event terdeteksi.
- Jumlah event valid.
- Jumlah event berpasangan.
- Jumlah event yang benar-benar dievaluasi.

Tie-break harus menggunakan definisi jumlah yang telah ditetapkan, bukan angka yang paling menguntungkan.

### 18.6.5. Tie-break ketiga: Max hold terkecil

Jika kandidat masih seri setelah dua kriteria pertama, kandidat dengan max_hold lebih kecil diprioritaskan.

Contoh:

| Kandidat | Worst Expectancy | Event Evaluated | Max Hold |
|---|---|---|---|
| A | +0,20R | 300 | 10 bar |
| B | +0,20R | 300 | 5 bar |

Kandidat B diprioritaskan karena memiliki durasi maksimum holding yang lebih pendek.

Alasannya dapat berkaitan dengan:

- Mengurangi waktu paparan risiko.
- Mengurangi ketergantungan terhadap pergerakan jangka panjang.
- Memperjelas horizon evaluasi.
- Mengurangi penggunaan modal yang terlalu lama.
- Memudahkan implementasi dan audit.

Namun, max hold yang lebih kecil bukan berarti selalu lebih baik dalam semua konteks. Ia menjadi prioritas hanya karena telah ditetapkan sebagai tie-break dalam kontrak.

### 18.6.6. Contoh penerapan tie-break

Misalkan terdapat empat kandidat:

| Kandidat | Worst Exp. | Event Evaluated | Max Hold | Status |
|---|---|---|---|---|
| A | +0,25R | 200 | 10 | Lolos |
| B | +0,30R | 100 | 5 | Lolos |
| C | +0,30R | 300 | 10 | Lolos |
| D | +0,30R | 300 | 5 | Lolos |

Urutan tie-break:

1. Kandidat B, C, D memiliki worst expectancy +0,30R, lebih tinggi dari A.
2. Di antara B, C, D, kandidat C dan D memiliki event evaluated 300, lebih tinggi dari B.
3. Di antara C dan D, kandidat D memiliki max hold 5 bar, lebih kecil dari C yang 10 bar.

Maka urutan prioritas:

1. D.
2. C.
3. B.
4. A.

Proses ini bersifat mekanis dan dapat diulang.

---

## 18.7. Jika Tidak Ada Kandidat Lolos

### 18.7.1. Status NO_EDGE_FOUND

Jika tidak ada kandidat yang memenuhi seluruh syarat kelulusan, TEKB menggunakan status:

**NO_EDGE_FOUND**

Status ini berarti:

> Dalam ruang hipotesis, data, aturan, dan prosedur pengujian yang digunakan, belum ditemukan bukti yang cukup bahwa kandidat memenuhi kriteria edge yang ditetapkan.

Status tersebut tidak selalu berarti bahwa pasar tidak memiliki pola apa pun. Ia berarti bahwa penelitian belum berhasil membuktikan edge dalam batasan eksperimen yang dilakukan.

### 18.7.2. Mengapa NO_EDGE_FOUND bukan kegagalan sistem?

Tujuan sistem penelitian bukan menghasilkan strategi dalam setiap eksperimen. Tujuannya adalah menghasilkan kesimpulan yang dapat dipertanggungjawabkan.

Jika sistem selalu dipaksa menghasilkan kandidat, maka ia akan cenderung:

- Memilih kandidat yang paling tidak buruk.
- Mengabaikan kegagalan pada worst-case.
- Menurunkan standar signifikansi.
- Mengubah baseline.
- Menghapus event yang merugikan.
- Mengulang eksperimen sampai menemukan hasil yang menarik.
- Menggunakan OOS untuk tuning.
- Menyembunyikan hasil negatif.

Semua tindakan tersebut dapat menghasilkan strategi yang tampak bagus tetapi tidak dapat dipercaya.

Karena itu:

> Kemampuan menyatakan "belum ditemukan edge" adalah tanda bahwa sistem penelitian memiliki kontrol, bukan tanda bahwa sistem tidak berguna.

### 18.7.3. Contoh tidak ada kandidat yang lolos

Misalkan sepuluh kandidat diuji.

| Kandidat | Worst Diff | Best Diff | Worst q | Best q | Status |
|---|---|---|---|---|---|
| A | +0,10R | +0,15R | 0,12 | 0,04 | Gagal worst |
| B | +0,20R | +0,25R | 0,03 | 0,18 | Gagal best |
| C | -0,05R | +0,30R | 0,40 | 0,02 | Gagal worst |
| D | +0,12R | +0,14R | 0,08 | 0,09 | Gagal keduanya |
| E | +0,30R | +0,40R | 0,02 | 0,01 | Lolos secara nominal, tetapi data tidak layak |
| F–J | Beragam | Beragam | Beragam | Beragam | Gagal |

Walaupun beberapa kandidat memiliki angka positif, tidak ada yang memenuhi seluruh syarat. Maka hasil penelitian adalah:

**NO_EDGE_FOUND**

Kesimpulan tersebut lebih jujur daripada memilih kandidat E hanya karena angka hasilnya paling tinggi.

### 18.7.4. Hasil NO_EDGE_FOUND harus disimpan

Hasil negatif harus disimpan dalam arsip penelitian, termasuk:

- Pertanyaan penelitian.
- Definisi event.
- Data yang digunakan.
- Periode IS.
- Versi grid.
- Evaluation engine.
- Aturan B0.
- Jumlah kandidat.
- Hasil setiap kandidat.
- Alasan kegagalan.
- Status kelayakan data.
- Multiple testing family.
- Parameter bootstrap.
- Tanggal penelitian.
- Versi kode.
- Keputusan akhir.

Mengapa perlu disimpan?

Karena hasil negatif:

- Mencegah eksperimen yang sama diulang tanpa pengetahuan.
- Membantu memahami batas kemampuan hipotesis.
- Menunjukkan bahwa ruang kandidat telah diuji.
- Mencegah peneliti hanya mengingat hasil positif.
- Menjadi bagian dari audit trail.
- Membantu membedakan eksperimen baru dari percobaan lama.
- Menjaga integritas proses penelitian.

Penelitian yang hanya menyimpan hasil positif akan menciptakan gambaran yang tidak lengkap.

### 18.7.5. Tidak boleh memaksa strategi dari kandidat yang paling tidak buruk

Ada perbedaan besar antara:

- Kandidat terbaik di antara semua kandidat.
- Kandidat yang memenuhi syarat kelayakan dan bukti.

Misalnya, semua kandidat menghasilkan perbedaan negatif terhadap B0. Kandidat A hanya sedikit lebih buruk daripada B, C, dan D.

A tetap bukan edge.

Demikian pula, jika semua kandidat gagal signifikansi, kandidat dengan p-value paling kecil belum tentu layak dipilih. Ia hanya merupakan kandidat yang paling dekat dengan ambang, bukan kandidat yang telah memenuhi standar.

Prinsipnya:

> "Paling tidak buruk" tidak sama dengan "terbukti memiliki edge."

---

## 18.8. Research Family dan Provenance

### 18.8.1. Mengapa provenance penting?

Dalam penelitian yang melibatkan banyak eksperimen, peneliti perlu mengetahui asal-usul setiap hasil.

Sebuah angka expectancy tidak cukup jika tidak diketahui:

- Dihasilkan dari data apa.
- Menggunakan grid versi berapa.
- Menggunakan evaluation engine versi berapa.
- Menggunakan aturan B0 yang mana.
- Berasal dari percobaan ke berapa.
- Apakah pernah dipilih sebelumnya.
- Apakah keluarga pengujiannya sama dengan hasil lain.
- Apakah ada percobaan sebelumnya yang tidak berhasil.

Informasi asal-usul tersebut disebut **provenance**.

Provenance membantu menjawab:

> "Hasil ini berasal dari proses penelitian yang mana, dengan aturan dan data yang bagaimana?"

### 18.8.2. research_batch_id

**research_batch_id** adalah identitas suatu batch atau pelaksanaan penelitian.

Contoh:
research_batch_id = RB_2026_001


Satu batch dapat mencakup:

- Dataset tertentu.
- Periode IS tertentu.
- Definisi event tertentu.
- Aturan B0 tertentu.
- Candidate grid tertentu.
- Evaluation engine tertentu.
- Prosedur bootstrap tertentu.

Dengan research_batch_id, peneliti dapat membedakan hasil dari pelaksanaan yang berbeda.

Contoh:
RB_2026_001 → penelitian SAMSON v1.0
RB_2026_002 → penelitian SAMSON v1.1

Perbedaan tersebut harus dijelaskan, bukan hanya diberi nomor.

### 18.8.3. attempt_number

**attempt_number** mencatat urutan percobaan dalam suatu proses penelitian atau rangkaian eksplorasi.

Contoh:
research_batch_id = RB_2026_001
attempt_number = 1

Jika peneliti melakukan percobaan lanjutan:
research_batch_id = RB_2026_001
attempt_number = 2

Namun, angka percobaan harus memiliki definisi yang jelas. Peneliti perlu menentukan apakah attempt_number menghitung:

- Setiap eksekusi.
- Setiap perubahan hipotesis.
- Setiap perubahan grid.
- Setiap perubahan dataset.
- Setiap perubahan evaluation engine.

Jika definisinya tidak jelas, angka tersebut tidak cukup untuk menjelaskan sejarah penelitian.

### 18.8.4. candidate_grid_version_id

**candidate_grid_version_id** mengidentifikasi versi ruang kandidat yang diuji.

Contoh:
candidate_grid_version_id = GRID_ATR_LONG_V1

Grid dapat mencakup:

- Nilai stop-loss.
- Nilai take-profit.
- Max hold.
- Horizon.
- Ambang event.
- Parameter lain yang memang termasuk dalam ruang kandidat.

Jika grid diubah, versi harus berubah.

Contoh:
GRID_ATR_LONG_V1
GRID_ATR_LONG_V2

Perubahan dari V1 ke V2 harus dijelaskan:

- Apakah rentang kandidat diperluas?
- Apakah kandidat lama dihapus?
- Apakah satuan berubah?
- Apakah max hold berubah?
- Apakah perubahan dilakukan sebelum atau sesudah hasil OOS dilihat?
- Apakah perubahan tersebut merupakan eksperimen baru?

Grid baru bukan sekadar pengaturan teknis kecil. Grid baru dapat memperluas jumlah kesempatan menemukan hasil yang terlihat baik.

### 18.8.5. multiple_testing_family_id

**multiple_testing_family_id** mengidentifikasi keluarga hipotesis yang diuji bersama untuk keperluan multiple testing.

Contoh:
multiple_testing_family_id = FAM_SAMSON_WORST_V1
multiple_testing_family_id = FAM_SAMSON_BEST_V1

Keluarga dapat dibentuk berdasarkan kontrak penelitian, misalnya:

- Semua kandidat dalam satu grid.
- Semua variasi exit dalam satu eksperimen.
- Semua kandidat worst-case.
- Semua kandidat best-case.
- Keluarga lain yang telah ditentukan.

Definisi keluarga harus dibuat sebelum hasil digunakan untuk memilih kandidat, sejauh yang dituntut oleh desain penelitian.

Jika keluarga berubah setelah melihat hasil, koreksi multiple testing dapat kehilangan makna.

### 18.8.6. prior_family_ids

**prior_family_ids** mencatat keluarga pengujian sebelumnya yang berkaitan dengan eksperimen saat ini.

Contoh:
prior_family_ids = [
FAM_SAMSON_V1,
FAM_SAMSON_GRID_EXPANSION_V1
]


Field ini penting karena eksperimen baru sering kali tidak benar-benar berdiri sendiri. Peneliti mungkin telah:

- Menguji ambang lain.
- Menguji timeframe lain.
- Menguji grid yang lebih luas.
- Menguji variasi entry.
- Menguji subset instrumen.
- Menguji filter tambahan.
- Mengulang penelitian setelah melihat hasil sebelumnya.

Riwayat tersebut dapat memengaruhi bagaimana hasil baru harus ditafsirkan.

Jika peneliti hanya melihat keluarga pengujian terakhir dan mengabaikan percobaan sebelumnya, jumlah eksplorasi yang sebenarnya dapat diremehkan.

### 18.8.7. Grid baru merupakan percobaan baru

Misalkan peneliti pertama kali menguji grid:
RV threshold = 2,5; 3,0; 3,5
Max hold = 3; 5

Tidak ada kandidat yang lolos.

Kemudian peneliti memperluas grid:
RV threshold = 2,0; 2,5; 3,0; 3,5; 4,0; 5,0
Max hold = 1; 3; 5; 10

Grid kedua memiliki lebih banyak kombinasi. Ia merupakan percobaan baru karena ruang pencarian telah berubah.

Peneliti tidak boleh menyajikan hasil terbaik dari grid kedua seolah-olah hanya berasal dari satu pengujian awal. Perlu dicatat bahwa telah terjadi perluasan ruang eksplorasi.

Alasannya sederhana:

> Semakin banyak pilihan dicoba, semakin besar kesempatan menemukan hasil yang tampak menarik secara kebetulan.

### 18.8.8. Provenance bukan pengganti koreksi formal lintas percobaan

Mencatat prior_family_ids sangat penting, tetapi pencatatan tersebut bukan pengganti koreksi statistik formal terhadap seluruh eksplorasi lintas percobaan.

Provenance menjawab:

> "Percobaan apa saja yang pernah dilakukan?"

Koreksi formal berusaha menjawab pertanyaan berbeda:

> "Bagaimana riwayat banyaknya pengujian memengaruhi tingkat kepercayaan terhadap hasil ini?"

Keduanya tidak sama.

Misalnya, peneliti mencatat bahwa telah melakukan 20 percobaan. Pencatatan itu baik. Namun, hanya menambahkan daftar 20 percobaan tidak otomatis membuat hasil percobaan ke-21 telah dikoreksi terhadap seluruh eksplorasi sebelumnya.

TEKB harus membedakan:

- Pencatatan provenance.
- Definisi keluarga pengujian.
- Koreksi multiple testing dalam keluarga.
- Penanganan eksplorasi lintas percobaan.
- Keputusan apakah suatu hasil masih layak dianggap eksploratif atau konfirmatori.

Dalam beberapa kasus, koreksi lintas percobaan mungkin belum diformalkan dalam versi metodologi tertentu. Jika demikian, status tersebut harus dicatat sebagai keterbatasan atau area yang masih terbuka, bukan disembunyikan.

### 18.8.9. Contoh provenance lengkap

Contoh metadata suatu kandidat:

research_batch_id = RB_2026_001
attempt_number = 3
candidate_grid_version_id = GRID_ATR_LONG_V2
multiple_testing_family_id = FAM_SAMSON_WORST_V2
prior_family_ids = [
FAM_SAMSON_V1,
FAM_SAMSON_GRID_V1
]
entry_definition_version_id = ENTRY_NEXT_VALID_OPEN_V1
b0_selection_rule_version = B0_SLOT_MATCH_V1
mae_mfe_definition_version_id = MAE_MFE_LONG_V1
atr_definition_version = ATR_WILDER_V1
evaluation_engine_version_id = EVAL_WORST_BEST_V1

Metadata tersebut membuat kandidat dapat ditelusuri kembali.

Jika hasil berubah, peneliti dapat memeriksa apakah penyebabnya berasal dari:

- Data.
- Event.
- Entry.
- B0.
- Grid.
- ATR.
- Evaluation engine.
- Multiple testing.
- Aturan seleksi.
- Versi kode.

Tanpa provenance, dua hasil yang berbeda dapat tampak seperti kontradiksi, padahal sebenarnya menggunakan definisi atau ruang kandidat yang berbeda.

---

## Penutup Bab

IS Selection adalah tahap ketika penelitian mulai menyaring kandidat yang layak dibawa ke proses pembekuan dan pengujian OOS.

Namun, seleksi tidak boleh dilakukan dengan prinsip sederhana:

> "Pilih angka paling tinggi."

Dalam TEKB, pemilihan kandidat harus memperhatikan:

- Data In-Sample digunakan untuk membangun dan memilih hipotesis.
- IS bukan tempat untuk membuktikan generalisasi final.
- Aturan seleksi harus dibekukan.
- B1 dan B0 harus dipertahankan sebagai pasangan.
- Pasangan di-anchor pada timestamp B1.
- Agregasi tidak boleh menghilangkan struktur pasangan.
- B1 Worst harus dibandingkan dengan B0 Worst.
- B1 Best harus dibandingkan dengan B0 Best.
- Kedua perbedaan harus positif dan memenuhi syarat signifikansi.
- BH-FDR diterapkan pada keluarga pengujian yang sesuai.
- Kandidat harus memenuhi syarat kelayakan data.
- Expectancy tertinggi tidak otomatis berarti kandidat terbaik.
- Tie-break hanya digunakan setelah seluruh syarat kelulusan terpenuhi.
- Jika tidak ada kandidat yang lolos, hasilnya adalah NO_EDGE_FOUND.
- Semua hasil, termasuk kegagalan, harus disimpan.
- Research family dan provenance harus dicatat.
- Grid baru adalah percobaan baru.
- Provenance bukan pengganti koreksi formal lintas percobaan.

Pada akhirnya, IS Selection bukan perlombaan mencari angka paling indah. Ia adalah proses untuk memastikan bahwa kandidat yang dibawa ke OOS telah dipilih melalui aturan yang jelas, pembanding yang adil, dan pengujian yang dapat diaudit.

Prinsipnya:

> Kandidat tidak dipilih karena terlihat paling bagus, tetapi karena memenuhi syarat bukti yang telah ditentukan.

---

## Ringkasan Bab

- In-Sample (IS) adalah data yang digunakan untuk membangun, mengembangkan, menguji, dan memilih hipotesis.
- IS bukan bukti generalisasi final. Generalisasi diuji melalui OOS.
- Aturan seleksi harus dibekukan sebelum hasil digunakan untuk memilih.
- B1 dan B0 harus dipertahankan sebagai pasangan, di-anchor pada timestamp B1.
- Agregasi tidak boleh menghilangkan struktur pasangan.
- Syarat kelulusan meliputi: data layak, B1 Worst − B0 Worst positif, signifikansi worst-case, B1 Best − B0 Best positif, signifikansi best-case, dan lolos BH-FDR pada keluarga masing-masing.
- Expectancy tertinggi tidak otomatis berarti kandidat terbaik.
- Tie-break digunakan hanya setelah seluruh syarat kelulusan terpenuhi, dengan urutan: worst-case expectancy, jumlah event evaluated, max hold terkecil.
- Jika tidak ada kandidat lolos, hasilnya adalah NO_EDGE_FOUND.
- Hasil NO_EDGE_FOUND harus disimpan sebagai bagian dari audit trail.
- Provenance (research_batch_id, attempt_number, candidate_grid_version_id, multiple_testing_family_id, prior_family_ids) harus dicatat.
- Grid baru merupakan percobaan baru.
- Provenance bukan pengganti koreksi formal lintas percobaan.

---

## Pertanyaan Refleksi

1. Apa perbedaan antara In-Sample dan Out-of-Sample?
2. Mengapa IS bukan bukti generalisasi final?
3. Mengapa aturan seleksi harus dibekukan sebelum hasil digunakan untuk memilih?
4. Apa itu pasangan B1/B0, dan mengapa strukturnya harus dipertahankan?
5. Apa arti anchor pada timestamp B1?
6. Apa saja syarat kelulusan kandidat dalam TEKB?
7. Mengapa expectancy tertinggi tidak otomatis berarti kandidat terbaik?
8. Kapan tie-break digunakan, dan apa urutannya?
9. Apa arti NO_EDGE_FOUND?
10. Mengapa hasil NO_EDGE_FOUND harus disimpan?
11. Apa itu provenance, dan mengapa penting?
12. Mengapa grid baru merupakan percobaan baru?

---

## Kalimat Kunci

> Kandidat tidak dipilih karena terlihat paling bagus, tetapi karena memenuhi syarat bukti yang telah ditentukan. Jika tidak ada yang memenuhi, NO_EDGE_FOUND adalah hasil yang sah.

---

<div align="center">

[← Bab Sebelumnya](/posts/bab-17-multiple-testing-bh-fdr/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Bab Selanjutnya →](/posts/bab-19-freeze-kandidat/)

</div>
