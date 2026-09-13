---
title: "BAB 17 — Multiple Testing dan BH-FDR: Mengendalikan Risiko Temuan Palsu"
published: 2026-09-12
description: "Semakin banyak hipotesis diuji, semakin besar peluang menemukan hasil bagus secara kebetulan. Bab ini menjelaskan multiple testing, FDR, dan prosedur BH-FDR."
tags: ["bab-17", "multiple-testing", "bh-fdr", "statistik"]
category: "Bab"
draft: false
lang: ""
---

**BAGIAN V — MESIN YANG MENENTUKAN APAKAH SEBUAH HIPOTESIS BEKERJA**

---

## 17.1. Mengapa Banyak Pengujian Menciptakan Masalah?

Bayangkan seseorang melempar sebuah koin yang seimbang. Jika koin dilempar satu kali, hasilnya hanya mungkin kepala atau ekor.

Sekarang bayangkan koin tersebut dilempar 100 kali. Hampir pasti akan muncul beberapa rangkaian hasil yang terlihat tidak biasa, misalnya:

- kepala lima kali berturut-turut;
- ekor tujuh kali dalam sepuluh lemparan;
- atau proporsi kepala yang tampak sangat tinggi dalam satu bagian percobaan.

Apakah rangkaian tersebut membuktikan bahwa koinnya tidak seimbang?

Belum tentu. Hasil ekstrem dapat muncul secara kebetulan, terutama ketika jumlah percobaan sangat banyak.

Prinsip yang sama berlaku dalam penelitian trading.

Jika peneliti menguji satu hipotesis, peluang mendapatkan hasil ekstrem secara kebetulan mungkin relatif terbatas. Namun, jika peneliti menguji ratusan atau ribuan hipotesis, peluang menemukan setidaknya satu hasil yang terlihat bagus hanya karena kebetulan akan meningkat.

### Satu eksperimen versus ratusan eksperimen

Misalnya, peneliti menguji satu aturan:

> "Apakah event SAMSON tertentu menghasilkan return yang lebih baik daripada B0?"

Jika hasilnya positif dan cukup kuat, peneliti dapat menyelidikinya lebih lanjut.

Namun, bayangkan peneliti menguji:

- 10 jenis ambang volume;
- 5 jenis periode baseline;
- 6 variasi entry;
- 9 kombinasi stop loss;
- 8 kombinasi take profit;
- 5 maximum hold;
- 10 instrumen;
- 4 jenis filter tambahan.

Jumlah kombinasi dapat menjadi sangat besar.

Dengan semakin banyak percobaan, peluang munculnya hasil yang tampak luar biasa juga meningkat. Sebagian hasil terbaik mungkin bukan mencerminkan edge yang benar, melainkan hanya hasil paling beruntung dari banyak percobaan.

### Hasil terbaik belum tentu hasil yang benar

Bayangkan 1.000 orang diminta menebak arah pergerakan harga secara acak. Walaupun tidak ada seorang pun yang memiliki kemampuan prediksi, kemungkinan besar akan ada beberapa orang yang berhasil menebak dengan sangat baik dalam sejumlah percobaan.

Jika kita hanya melihat orang dengan hasil terbaik, kita mungkin menyimpulkan:

> "Orang ini memiliki kemampuan luar biasa."

Padahal, kita mengabaikan 999 orang lainnya yang hasilnya biasa saja atau buruk.

Inilah masalah utama **multiple testing**:

> Ketika banyak hipotesis diuji, hasil terbaik harus diperlakukan dengan hati-hati karena sebagian hasil ekstrem dapat muncul hanya karena keberuntungan statistik.

Dalam TEKB, tujuan penelitian bukan mencari kandidat yang paling menarik setelah mencoba sebanyak mungkin kombinasi. Tujuannya adalah menemukan perbedaan yang memiliki bukti cukup kuat, dapat dibandingkan secara adil, dan tidak hanya muncul karena proses pencarian yang terlalu luas.

---

## 17.2. Apa Itu Multiple Testing?

**Multiple testing** berarti melakukan banyak pengujian hipotesis atau kandidat dalam satu rangkaian penelitian.

Satu pengujian biasanya memiliki pertanyaan seperti:

> "Apakah rata-rata hasil B1 berbeda dari B0?"

Dalam multiple testing, pertanyaan tersebut diajukan berkali-kali terhadap banyak variasi.

Contohnya:

- Apakah SL 1 ATR dan TP 2 ATR menghasilkan edge?
- Apakah SL 1 ATR dan TP 3 ATR menghasilkan edge?
- Apakah SL 1,5 ATR dan TP 2 ATR menghasilkan edge?
- Apakah maximum hold 3 bar lebih baik daripada B0?
- Apakah maximum hold 5 bar lebih baik daripada B0?
- Apakah ambang RV 2,5 lebih baik daripada RV 3?
- Apakah ambang RV 3 lebih baik daripada RV 5?

Setiap kombinasi tersebut dapat dianggap sebagai kandidat atau hipotesis yang berbeda.

### Contoh kombinasi SL, TP, dan maximum hold

Misalkan TEKB menguji:

- 3 pilihan stop loss;
- 3 pilihan take profit;
- 3 pilihan maximum hold.

Jumlah kandidatnya adalah:

> 3 × 3 × 3 = 27 kandidat

Jika setiap kandidat diuji terhadap B0, berarti terdapat 27 pengujian atau **keluarga pengujian** yang perlu dipertimbangkan.

Jika peneliti kemudian menguji beberapa definisi event, instrumen, timeframe, filter, atau versi aturan tambahan, jumlah pengujian dapat meningkat jauh lebih besar.

### Mengapa setiap hasil tidak boleh dianggap berdiri sendiri?

Misalkan satu pengujian menghasilkan p-value 0,04. Jika pengujian itu dilakukan satu kali dan protokolnya telah ditetapkan sebelumnya, angka tersebut memiliki konteks tertentu.

Namun, jika peneliti melakukan 100 pengujian dan kemudian memilih hanya hasil dengan p-value di bawah 0,05, interpretasinya berbeda.

Dalam banyak pengujian, sebagian hasil dapat melewati ambang 0,05 secara kebetulan, walaupun tidak ada edge yang benar-benar nyata.

Karena itu, pertanyaan yang perlu diajukan bukan hanya:

> "Apakah kandidat ini terlihat signifikan?"

Tetapi juga:

- "Berapa banyak kandidat yang diuji sebelum kandidat ini dipilih?"
- "Apakah kandidat ini dipilih karena aturan yang telah ditentukan, atau karena hasilnya paling menarik setelah semua hasil terlihat?"
- "Bagaimana risiko temuan positif palsu dikendalikan?"

Multiple testing mengingatkan kita bahwa proses pencarian juga merupakan bagian dari bukti yang harus diperhitungkan.

---

## 17.3. Perbedaan p-value dan Bukti Edge

P-value sering muncul dalam laporan penelitian, tetapi mudah disalahartikan.

Untuk memahami perannya, kita perlu membedakan antara:

- p-value;
- besar efek;
- manfaat praktis;
- bukti edge dibandingkan B0.

### Apa itu p-value secara sederhana?

P-value adalah ukuran yang digunakan dalam kerangka pengujian hipotesis untuk menilai seberapa tidak biasa hasil yang diamati jika asumsi tertentu, biasanya hipotesis nol, dianggap berlaku.

Dalam konteks sederhana, hipotesis nol dapat berupa:

> "Tidak ada perbedaan yang relevan antara B1 dan B0."

Jika p-value kecil, hasil yang diamati dianggap relatif sulit dijelaskan oleh asumsi nol dalam kerangka pengujian tersebut.

Namun, p-value bukan ukuran langsung dari seberapa besar keuntungan.

### P-value bukan ukuran besar keuntungan

Misalnya:

- Kandidat A menghasilkan Δ = +0,10% dengan p-value 0,001.
- Kandidat B menghasilkan Δ = +2,00% dengan p-value 0,08.

Kandidat A memiliki p-value lebih kecil, tetapi efeknya sangat kecil. Kandidat B memiliki efek lebih besar, tetapi ketidakpastiannya lebih tinggi.

P-value tidak menjawab:

> "Berapa besar keuntungan yang dihasilkan?"

Untuk menjawabnya, kita perlu melihat ukuran efek seperti:

- Δ mean;
- Δ median;
- perbedaan expectancy;
- perbedaan net expectancy;
- perbedaan win rate;
- perubahan percentile;
- perubahan risiko;
- dan biaya transaksi.

### P-value bukan probabilitas hipotesis benar

P-value 0,03 tidak berarti:

> "Peluang hipotesis benar adalah 97%."

P-value juga tidak berarti:

> "Peluang strategi akan berhasil di masa depan adalah 97%."

P-value harus dibaca sesuai definisi dan asumsi pengujian yang digunakan. Ia merupakan ukuran yang berkaitan dengan data dan model pengujian, bukan probabilitas langsung bahwa hipotesis benar.

### Signifikansi statistik tidak otomatis berarti manfaat praktis

Hasil yang sangat kecil dapat menjadi signifikan secara statistik jika jumlah observasinya besar.

Misalnya:

- B1 lebih baik daripada B0 sebesar 0,03%.

Dengan sampel yang sangat besar, perbedaan tersebut mungkin menghasilkan p-value kecil. Tetapi setelah memperhitungkan:

- biaya transaksi;
- spread;
- slippage;
- pajak;
- keterlambatan eksekusi;
- risiko;
- dan kompleksitas implementasi;

perbedaan 0,03% mungkin tidak memiliki manfaat praktis.

Sebaliknya, efek yang cukup besar tetapi memiliki sampel kecil dapat belum menghasilkan bukti statistik yang kuat.

Karena itu, TEKB harus membedakan:

- **Signifikansi statistik** — apakah data memberikan bukti yang cukup terhadap hipotesis nol dalam kerangka uji?
- **Makna praktis** — apakah besarnya perbedaan cukup berarti setelah mempertimbangkan risiko, biaya, dan cara penerapannya?

### Edge tetap harus dibandingkan dengan B0

P-value tidak menggantikan pembanding.

Misalnya, B1 menghasilkan rata-rata return +1%, tetapi B0 juga menghasilkan +0,9%. Maka perbedaan yang relevan bukan sekadar +1%, melainkan:

> Δ = B1 − B0 = +0,1%

TEKB mencari informasi tambahan dibandingkan kondisi dasar yang adil.

Dengan demikian, bukti edge harus dibaca melalui kombinasi:

- definisi B1 yang jelas;
- B0 yang adil;
- ukuran efek;
- ketidakpastian;
- koreksi multiple testing;
- biaya dan risiko;
- serta validasi OOS.

---

## 17.4. Apa Itu False Discovery Rate?

### Pengertian temuan positif palsu

Dalam penelitian, terdapat kemungkinan bahwa suatu hasil dinyatakan positif atau dianggap memiliki bukti edge, padahal sebenarnya hasil tersebut muncul karena kebetulan.

Inilah yang disebut **false discovery**, atau temuan positif palsu.

Misalnya, peneliti menyatakan:

> "Kandidat X memiliki edge."

Namun, setelah diuji pada data baru, hasil tersebut tidak bertahan dan ternyata tidak memiliki perbedaan yang nyata dibandingkan B0.

Tidak semua kegagalan OOS otomatis membuktikan bahwa hasil IS adalah positif palsu. Kegagalan dapat disebabkan oleh perubahan rezim pasar, variasi sampel, biaya, atau faktor lain. Tetapi dalam konteks multiple testing, sebagian kandidat yang lolos seleksi memang dapat merupakan temuan positif palsu.

### Apa itu False Discovery Rate?

**False Discovery Rate**, disingkat **FDR**, adalah tingkat proporsi temuan positif palsu yang diharapkan di antara seluruh temuan yang dinyatakan positif.

Misalnya, setelah suatu prosedur seleksi, peneliti menyatakan 20 kandidat sebagai temuan positif. Jika prosedur tersebut mengendalikan FDR pada tingkat 10%, interpretasi sederhananya adalah:

> Dalam jangka panjang dan di bawah asumsi prosedur yang sesuai, proporsi temuan positif palsu di antara seluruh temuan yang dinyatakan positif diharapkan terkendali sekitar tingkat 10%.

Ini bukan berarti tepat 2 dari 20 kandidat pasti palsu. FDR adalah pengendalian proporsi secara rata-rata dalam kerangka pengulangan penelitian, bukan daftar pasti kandidat mana yang salah.

### Mengapa FDR penting dalam penelitian eksploratif?

Penelitian eksploratif sering menguji banyak kemungkinan. Hal ini wajar ketika peneliti sedang mencari pola yang belum diketahui.

Namun, semakin banyak pola yang dicari, semakin besar peluang menemukan hasil yang tampak positif secara kebetulan.

FDR membantu menjaga agar proses eksplorasi tidak berubah menjadi mesin yang menghasilkan terlalu banyak klaim positif palsu.

FDR sangat relevan ketika peneliti:

- menguji banyak kandidat;
- membandingkan banyak kombinasi parameter;
- mengevaluasi banyak hipotesis;
- menyaring banyak kemungkinan edge;
- atau melakukan pencarian awal sebelum validasi lebih lanjut.

### FDR berbeda dari peluang satu kesalahan

FDR jangan disamakan dengan peluang melakukan satu kesalahan dalam seluruh rangkaian pengujian.

Ada dua konsep yang perlu dibedakan:

- **Family-Wise Error Rate (FWER)** berfokus pada peluang membuat setidaknya satu kesalahan positif palsu dalam satu keluarga pengujian.
- **False Discovery Rate (FDR)** berfokus pada proporsi temuan positif palsu di antara seluruh temuan yang dinyatakan positif.

Contoh sederhana:

Dari 100 kandidat, 20 dinyatakan positif.

Jika 2 di antaranya ternyata positif palsu, proporsi positif palsunya adalah 2/20 = 10%.

FWER akan bertanya:

> "Apakah ada setidaknya satu temuan positif palsu?"

FDR akan bertanya:

> "Di antara semua temuan yang dinyatakan positif, berapa proporsi yang diperkirakan positif palsu?"

Keduanya memiliki tujuan berbeda. Untuk penelitian eksploratif dengan banyak kandidat, pengendalian FDR sering lebih sesuai karena tidak terlalu ekstrem dalam menolak semua kandidat hanya demi menghindari satu kesalahan.

---

## 17.5. BH-FDR secara Sederhana

Salah satu prosedur populer untuk mengendalikan FDR adalah **Benjamini–Hochberg**, sering disingkat **BH-FDR**.

Prosedur ini membantu menyesuaikan penilaian terhadap banyak p-value agar peneliti tidak memperlakukan setiap p-value seolah-olah berasal dari satu pengujian tunggal.

### Gambaran dasarnya

Misalkan terdapat beberapa kandidat dengan p-value sebagai berikut:

| Kandidat | P-value |
|---|---|
| A | 0,001 |
| B | 0,008 |
| C | 0,021 |
| D | 0,040 |
| E | 0,120 |

Langkah umum BH-FDR adalah:

1. Mengumpulkan p-value dari satu keluarga pengujian.
2. Mengurutkan p-value dari yang terkecil hingga terbesar.
3. Memberi peringkat pada setiap p-value.
4. Membandingkan p-value dengan batas yang disesuaikan berdasarkan jumlah pengujian dan tingkat FDR yang ditetapkan.
5. Menentukan kandidat mana yang memenuhi kriteria setelah penyesuaian.

Jika tingkat FDR yang ditetapkan adalah q, batas sederhana BH untuk p-value pada peringkat i dari m pengujian dapat ditulis sebagai:

> p_(i) ≤ (i / m) × q

Keterangan:

- p_(i) adalah p-value yang telah diurutkan;
- i adalah peringkat p-value;
- m adalah jumlah seluruh pengujian dalam keluarga;
- q adalah tingkat FDR yang ditetapkan.

Untuk pembaca awam, rumus ini dapat dipahami sebagai berikut:

> Semakin banyak pengujian yang dilakukan, semakin hati-hati kita harus menilai hasil yang terlihat positif.

Prosedur BH tidak sekadar memeriksa apakah p-value lebih kecil dari 0,05. Ia mempertimbangkan posisi p-value dalam keseluruhan kumpulan pengujian.

### Mengapa p-value harus diurutkan?

P-value terkecil biasanya memberikan bukti yang lebih kuat terhadap hipotesis nol dibandingkan p-value yang lebih besar. Namun, p-value tersebut tetap harus dinilai dalam konteks jumlah pengujian.

Dengan mengurutkan p-value, BH-FDR menilai kandidat secara kolektif, bukan satu per satu secara terisolasi.

### Apa arti "mengendalikan proporsi temuan positif palsu"?

BH-FDR tidak berusaha menjamin bahwa tidak ada satu pun temuan positif palsu.

Sebaliknya, prosedur ini berusaha mengendalikan proporsi temuan positif palsu di antara hasil yang dinyatakan positif.

Ini penting karena penelitian eksploratif mungkin menguji banyak kandidat. Jika prosedur terlalu keras, semua kandidat berpotensi ditolak meskipun sebagian benar-benar memiliki informasi berguna.

BH-FDR mencari keseimbangan:

- tetap memberi ruang bagi penemuan;
- tetapi mengurangi risiko bahwa sebagian besar temuan positif sebenarnya merupakan hasil kebetulan.

### Contoh sederhana

Misalkan 100 kandidat diuji. Setelah prosedur BH-FDR, 10 kandidat dinyatakan lolos.

Jika prosedur dan asumsi yang digunakan sesuai, tingkat FDR yang ditetapkan bertujuan agar proporsi temuan positif palsu di antara 10 kandidat tersebut terkendali pada tingkat yang telah ditentukan, misalnya 5% atau 10%, dalam pengertian jangka panjang.

Namun, ini bukan berarti peneliti dapat menunjuk kandidat tertentu dan berkata:

> "Kandidat ini memiliki peluang 90% pasti benar."

BH-FDR adalah prosedur pengendalian kelompok, bukan probabilitas kebenaran individual untuk setiap kandidat.

### Keluarga pengujian harus ditetapkan dengan benar

BH-FDR hanya bermakna jika p-value yang dimasukkan berasal dari keluarga pengujian yang didefinisikan secara benar.

Peneliti tidak boleh:

- menguji 100 kandidat;
- hanya memasukkan 10 p-value yang paling menarik;
- lalu mengklaim bahwa BH-FDR telah diterapkan pada 10 pengujian.

Jumlah dan anggota keluarga harus mencerminkan proses pengujian yang relevan.

Jika sebagian pengujian disembunyikan atau dikeluarkan hanya karena hasilnya tidak bagus, koreksi dapat menjadi terlalu optimistis.

Prinsipnya:

> Koreksi multiple testing harus mencerminkan seluruh keluarga pengujian yang memang menjadi dasar klaim penelitian.

---

## 17.6. Keluarga Pengujian dalam TEKB

Dalam TEKB, proses seleksi kandidat dapat menghasilkan lebih dari satu jenis evaluasi. Karena itu, keluarga pengujian harus didefinisikan dengan jelas.

Dalam protokol TEKB, keluarga pengujian penting dibedakan antara:

- **worst-case family**;
- **best-case family**.

### Apa yang dimaksud worst-case?

Dalam Evaluation Engine, kondisi tertentu dapat menghasilkan ambiguitas intrabar.

Misalnya, pada satu bar yang sama, harga secara intrabar dapat menyentuh level stop loss dan take profit. Karena data OHLCV tidak selalu memberi tahu urutan kejadian di dalam bar, hasilnya dapat bersifat ambigu.

TEKB tidak boleh memilih urutan yang paling menguntungkan hanya berdasarkan keinginan peneliti.

Karena itu, evaluasi dapat dilakukan melalui dua batas:

- **worst-case:** skenario konservatif atau paling merugikan yang masih sesuai dengan informasi yang tersedia;
- **best-case:** skenario paling menguntungkan yang masih mungkin berdasarkan informasi yang tersedia.

Kedua skenario ini bukan dua hasil yang boleh dicampur sesuka hati. Keduanya merupakan cara berbeda untuk memahami rentang hasil yang mungkin akibat ambiguitas data.

### Mengapa worst-case dan best-case menjadi keluarga terpisah?

Worst-case dan best-case menjawab pertanyaan yang berbeda.

Keluarga worst-case bertanya:

> "Apakah kandidat masih menunjukkan keunggulan jika ambiguitas dievaluasi secara konservatif?"

Keluarga best-case bertanya:

> "Apakah kandidat menunjukkan keunggulan dalam batas skenario terbaik yang masih mungkin?"

Karena statistik, distribusi, dan p-value dari kedua keluarga tersebut dapat berbeda, koreksi multiple testing perlu diterapkan secara terpisah.

Dalam TEKB, p-value dari seluruh kandidat pada worst-case dikumpulkan ke dalam satu keluarga worst-case. P-value dari seluruh kandidat pada best-case dikumpulkan ke dalam satu keluarga best-case.

### Mengapa koreksi tidak boleh dilakukan dengan mencampur semuanya?

Jika worst-case dan best-case dicampur menjadi satu keluarga tanpa alasan metodologis yang jelas, interpretasi hasil dapat menjadi kabur.

Kedua keluarga memiliki makna evaluasi yang berbeda. Dengan memisahkannya, pembaca dapat mengetahui:

- kandidat mana yang lolos dalam kondisi konservatif;
- kandidat mana yang hanya lolos dalam kondisi terbaik;
- apakah edge tetap bertahan ketika ambiguitas diperlakukan secara ketat;
- dan apakah hasil sangat bergantung pada cara penyelesaian ambiguitas.

Pemisahan ini juga mencegah peneliti mengambil hasil terbaik dari satu skenario lalu membandingkannya dengan hasil dari skenario lain.

### Worst-case dan best-case tidak boleh dicampur silang

Misalnya:

- B1 worst-case dibandingkan dengan B0 worst-case;
- B1 best-case dibandingkan dengan B0 best-case.

Perbandingan tersebut harus konsisten.

Yang tidak boleh dilakukan:

- B1 worst-case dibandingkan dengan B0 best-case;
- B1 best-case dibandingkan dengan B0 worst-case;
- memilih hasil B1 yang paling baik dan B0 yang paling buruk;
- atau mengambil p-value dari keluarga worst-case lalu menggunakannya untuk membenarkan klaim best-case.

Cara seperti itu akan menghasilkan perbandingan yang tidak adil dan dapat menciptakan keunggulan semu.

### Contoh struktur keluarga TEKB

| Keluarga | Isi pengujian | Tujuan |
|---|---|---|
| Worst-case family | Semua kandidat dievaluasi dengan aturan worst-case | Menguji ketahanan edge secara konservatif |
| Best-case family | Semua kandidat dievaluasi dengan aturan best-case | Menggambarkan batas atas hasil yang masih mungkin |
| OOS evaluation | Kandidat yang telah dibekukan diuji pada data baru | Menguji generalisasi, bukan memperluas keluarga IS |

Keluarga pengujian harus memiliki identitas dan dokumentasi, misalnya:

- multiple_testing_family_id;
- daftar kandidat yang termasuk;
- jumlah pengujian;
- statistik yang diuji;
- metode pengujian;
- tingkat FDR;
- versi protokol;
- dan hubungan dengan batch penelitian.

Dengan begitu, koreksi tidak menjadi angka yang berdiri sendiri, melainkan bagian dari audit trail.

---

## 17.7. Batasan BH-FDR

BH-FDR berguna untuk mengendalikan risiko temuan positif palsu dalam banyak pengujian. Namun, ia bukan obat untuk seluruh masalah penelitian.

### 1. BH-FDR tidak menghapus bias desain penelitian

Jika penelitian sejak awal memiliki desain yang salah, koreksi p-value tidak otomatis memperbaikinya.

Contoh masalah desain:

- event dipilih setelah hasil diketahui;
- definisi entry berubah setelah melihat keuntungan;
- B0 dipilih berdasarkan outcome;
- event yang rugi dihapus tanpa aturan sebelumnya;
- data yang tidak sesuai sengaja dikeluarkan;
- periode penelitian dipilih karena hasilnya bagus.

Jika inputnya bias, BH-FDR hanya melakukan koreksi terhadap hasil dari input yang bias tersebut.

### 2. BH-FDR tidak memperbaiki look-ahead bias

Look-ahead bias terjadi ketika informasi masa depan secara tidak sengaja digunakan untuk menentukan kondisi, entry, seleksi, atau evaluasi.

Misalnya, peneliti menggunakan informasi harga setelah entry untuk menentukan apakah event layak dimasukkan sejak awal.

BH-FDR tidak dapat memperbaiki masalah ini. P-value yang telah dikoreksi tetap berasal dari data yang tercemar oleh informasi masa depan.

Prinsipnya:

> Tidak ada koreksi statistik yang dapat mengubah penelitian yang menggunakan informasi masa depan menjadi penelitian yang kausal dan valid secara waktu.

### 3. BH-FDR tidak menggantikan B0

BH-FDR mengendalikan risiko temuan positif palsu di antara banyak pengujian. Ia tidak menentukan apakah pembanding penelitian adil.

Jika B0 buruk, tidak sebanding, atau dipilih berdasarkan outcome, maka perbedaan B1-B0 dapat menyesatkan.

B0 tetap harus memiliki aturan yang jelas mengenai:

- instrumen;
- waktu;
- populasi;
- declustering;
- hari perdagangan;
- pemilihan pasangan;
- partisi IS/OOS;
- dan larangan penggunaan outcome masa depan.

### 4. BH-FDR tidak menjamin hasil akan bertahan di OOS

Kandidat dapat lolos seleksi IS setelah koreksi BH-FDR, tetapi tetap gagal pada OOS.

Hal ini dapat terjadi karena:

- perubahan rezim pasar;
- sampel IS tidak mewakili kondisi masa depan;
- efek terlalu kecil;
- biaya transaksi;
- perubahan likuiditas;
- ketergantungan data yang belum sepenuhnya ditangani;
- atau edge memang tidak stabil.

Karena itu, BH-FDR bukan pengganti OOS.

Urutan metodologis TEKB tetap:

> Data → definisi event → B0 → evaluasi → ukuran efek → ketidakpastian → multiple testing → seleksi IS → freeze → OOS.

### 5. Koreksi statistik hanya berguna jika input penelitiannya benar

BH-FDR dapat membantu mengendalikan risiko temuan positif palsu, tetapi hanya dalam kerangka asumsi dan prosedur yang sesuai.

Peneliti tetap harus memastikan:

- hipotesis didefinisikan sebelum evaluasi;
- keluarga pengujian ditetapkan dengan benar;
- seluruh pengujian relevan diperhitungkan;
- B1 dan B0 dibandingkan secara adil;
- tidak ada look-ahead;
- event tidak dipilih berdasarkan hasil;
- statistik dan p-value dihitung dengan metode yang sesuai;
- dependensi data dipertimbangkan;
- dan hasil dilaporkan secara transparan.

### 6. BH-FDR bukan izin untuk menguji tanpa batas

Kesalahpahaman yang berbahaya adalah:

> "Tidak masalah menguji ribuan kandidat, karena nanti BH-FDR akan memperbaikinya."

Pernyataan ini keliru.

BH-FDR bukan izin untuk melakukan pencarian tanpa disiplin. Semakin luas ruang pencarian, semakin kompleks masalahnya. Selain itu, proses mencoba banyak desain, mengubah aturan, mengulang batch, dan memilih hanya hasil terbaik dapat menimbulkan persoalan yang tidak sepenuhnya diselesaikan hanya dengan satu koreksi p-value.

Karena itu, TEKB perlu mencatat:

- research batch;
- attempt number;
- versi grid kandidat;
- keluarga pengujian;
- keluarga sebelumnya yang relevan;
- perubahan protokol;
- dan status apakah hasil masih eksploratif atau telah dibekukan.

Transparansi terhadap seluruh proses pencarian sama pentingnya dengan koreksi statistik itu sendiri.

---

## Ringkasan Bab

- Multiple testing muncul ketika peneliti menguji banyak hipotesis atau kandidat sekaligus. Semakin banyak pengujian dilakukan, semakin besar peluang menemukan hasil yang terlihat bagus hanya karena kebetulan.
- Dalam penelitian trading, masalah ini dapat muncul ketika peneliti mencoba banyak kombinasi: ambang volume, definisi event, stop loss, take profit, maximum hold, instrumen, timeframe, atau filter tambahan.
- Karena itu, hasil terbaik tidak boleh langsung dianggap sebagai edge.
- P-value membantu menilai hasil dalam kerangka pengujian tertentu, tetapi bukan ukuran besar keuntungan, bukan probabilitas hipotesis benar, dan bukan jaminan manfaat praktis.
- FDR atau False Discovery Rate berfokus pada pengendalian proporsi temuan positif palsu di antara seluruh temuan yang dinyatakan positif. Salah satu prosedur untuk mengendalikannya adalah Benjamini–Hochberg atau BH-FDR.
- Dalam TEKB, keluarga pengujian harus ditetapkan dengan benar. Keluarga worst-case dan best-case diperlakukan terpisah karena keduanya mewakili cara evaluasi yang berbeda. Hasil B1 dan B0 juga harus dibandingkan dalam skenario yang sama; tidak boleh dicampur silang.
- BH-FDR tetap memiliki batasan. Ia tidak memperbaiki look-ahead bias, tidak menggantikan B0, tidak menghapus bias desain, tidak menciptakan edge, dan tidak menjamin keberhasilan OOS.

Kesimpulan yang bertanggung jawab bukan:

> "Kandidat ini lolos p-value setelah koreksi, berarti pasti benar."

Kesimpulan yang lebih tepat adalah:

> "Kandidat ini memenuhi kriteria statistik dalam keluarga pengujian yang telah ditetapkan, tetapi ukuran efek, ketidakpastian, kualitas desain, dan validasi OOS tetap diperlukan untuk menilai apakah temuan tersebut layak dipercaya."

---

## Pertanyaan Refleksi

1. Mengapa peluang menemukan hasil ekstrem meningkat ketika jumlah pengujian bertambah?
2. Apa yang dimaksud dengan multiple testing?
3. Mengapa hasil terbaik dari banyak kandidat belum tentu merupakan hasil yang benar?
4. Mengapa p-value bukan ukuran besar keuntungan?
5. Mengapa p-value bukan probabilitas hipotesis benar?
6. Apa perbedaan antara FDR dan FWER?
7. Apa tujuan utama prosedur BH-FDR?
8. Mengapa keluarga pengujian harus ditetapkan dengan benar?
9. Mengapa worst-case dan best-case harus dikoreksi secara terpisah?
10. Mengapa BH-FDR tidak dapat menggantikan B0 dan OOS?
11. Mengapa koreksi statistik tidak dapat memperbaiki look-ahead bias?
12. Mengapa seluruh proses pencarian kandidat harus dicatat dalam audit trail?

---

## Kalimat Kunci

> Semakin banyak kita mencoba, semakin besar peluang menemukan hasil yang tampak bagus secara kebetulan. Multiple testing mengingatkan kita untuk menghitung seluruh proses pencarian, sedangkan BH-FDR membantu mengendalikan proporsi temuan positif palsu. Namun, koreksi statistik hanya berguna jika desain penelitian, data, pembanding, dan aturan evaluasinya sejak awal benar.

---

<div align="center">

[← Bab Sebelumnya](/posts/bab-16-bootstrap/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Bab Selanjutnya →](/posts/bab-18-is-selection/)

</div>