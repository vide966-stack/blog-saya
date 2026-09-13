---
title: "Lampiran A — Glosarium Istilah TEKB"
published: 2026-09-12
description: "Glosarium istilah-istilah penting dalam penelitian TEKB, dijelaskan sesederhana mungkin untuk pembaca awam."
tags: ["lampiran-a", "glosarium", "istilah", "referensi"]
category: "Lampiran"
draft: false
lang: ""
---

Lampiran ini menjelaskan istilah-istilah penting yang digunakan dalam penelitian TEKB. Penjelasan dibuat sesederhana mungkin agar pembaca dapat memahami istilah teknis tanpa harus langsung menguasai statistik atau pemrograman.

Dalam TEKB, istilah tidak hanya berfungsi sebagai nama. Setiap istilah mewakili aturan, proses, atau konsep tertentu. Karena itu, penggunaannya harus konsisten. Perubahan definisi suatu istilah dapat mengubah hasil penelitian dan harus diperlakukan sebagai perubahan metodologi.

---

## B0

**B0** adalah baseline atau pembanding utama dalam penelitian TEKB.

B0 digunakan untuk menjawab pertanyaan:

> "Apakah hasil kondisi yang sedang diuji benar-benar berbeda dari hasil kondisi pembanding yang adil?"

B0 bukan berarti strategi yang selalu menghasilkan nol. B0 adalah kelompok pembanding yang dibentuk menggunakan aturan tertentu, misalnya instrumen yang sama, slot waktu yang sama, periode yang sebanding, dan karakteristik pencocokan yang telah ditentukan.

Tanpa B0, hasil positif dari B1 dapat keliru dianggap sebagai edge, padahal hasil tersebut mungkin hanya mencerminkan kondisi pasar secara umum.

---

## B1

**B1** adalah kelompok utama atau kondisi yang sedang diuji dalam penelitian.

Misalnya, B1 dapat berisi event yang memenuhi kondisi tertentu, seperti anomali volume, breakout, atau pola OHLCV tertentu.

Hasil B1 kemudian dibandingkan dengan B0. B1 yang menghasilkan return positif belum tentu memiliki edge. Yang penting adalah apakah B1 menunjukkan keunggulan yang relevan dan dapat dipertanggungjawabkan dibandingkan B0.

---

## Baseline

**Baseline** adalah nilai dasar yang digunakan sebagai referensi pembanding.

Dalam konteks volume, baseline dapat berupa rata-rata volume historis untuk sesi atau slot waktu tertentu. Baseline membantu menentukan apakah volume saat ini tergolong normal atau tidak normal.

Contohnya, jika volume rata-rata pada slot tertentu adalah 100.000 saham dan volume saat ini 500.000 saham, maka volume saat ini dibandingkan dengan baseline tersebut untuk menghitung Relative Volume.

Baseline harus ditentukan menggunakan data yang tersedia sebelum event. Baseline tidak boleh menggunakan informasi masa depan.

---

## Bootstrap

**Bootstrap** adalah metode statistik untuk memperkirakan ketidakpastian suatu hasil dengan membentuk banyak sampel ulang dari data yang tersedia.

Dalam penelitian sederhana, bootstrap dapat dilakukan dengan mengambil kembali observasi dari sampel. Namun, dalam TEKB, metode bootstrap harus memperhatikan ketergantungan antar-event.

Jika beberapa event berasal dari tanggal yang sama atau saling berdekatan, bootstrap biasa dapat memberikan tingkat keyakinan yang terlalu tinggi. Karena itu, TEKB dapat menggunakan pendekatan seperti:

- date-cluster bootstrap;
- moving block bootstrap;
- atau metode lain yang sesuai dengan struktur data.

Bootstrap tidak membuktikan bahwa hipotesis benar. Bootstrap membantu memperkirakan seberapa stabil suatu estimasi.

---

## Candidate Grid

**Candidate grid** adalah daftar kombinasi kandidat parameter yang akan diuji.

Dalam penelitian SL/TP, candidate grid dapat berisi kombinasi:

- stop-loss dalam satuan ×ATR;
- take-profit dalam satuan ×ATR;
- maksimum holding period;
- atau konfigurasi lain yang telah ditentukan.

Contoh:

| Kandidat | Stop-Loss | Take-Profit | Maksimum Holding |
|---|---|---|---|
| C1 | 1 × ATR | 1 × ATR | 5 bar |
| C2 | 1 × ATR | 2 × ATR | 5 bar |
| C3 | 2 × ATR | 3 × ATR | 10 bar |

Candidate grid harus ditentukan dan dicatat sebelum proses seleksi. Jika grid diubah setelah melihat hasil OOS, maka proses tersebut bukan lagi OOS yang murni.

---

## Conditional Association

**Conditional association** adalah hubungan atau perbedaan hasil yang diamati dengan syarat kondisi tertentu terpenuhi.

Dalam TEKB, conditional association berarti:

> "Ketika kondisi X terjadi, distribusi hasil Y terlihat berbeda dibandingkan pembanding tertentu."

Contohnya, event dengan Relative Volume tinggi mungkin memiliki distribusi return berikutnya yang berbeda dari event dengan Relative Volume normal.

Conditional association tidak otomatis berarti hubungan sebab-akibat. TEKB dapat menemukan bahwa dua kondisi berkaitan, tetapi tidak langsung membuktikan bahwa kondisi pertama menyebabkan kondisi kedua.

---

## Counterfactual

**Counterfactual** adalah gambaran tentang apa yang mungkin terjadi pada kondisi pembanding yang sebanding, tetapi tidak mengalami perlakuan atau fitur yang sedang diuji.

Dalam TEKB, B0 berfungsi sebagai pendekatan praktis terhadap counterfactual.

Contohnya, jika B1 adalah event breakout dengan anomali volume, maka B0 berusaha mewakili kondisi sebanding tanpa fitur anomali volume tersebut.

Counterfactual dalam penelitian pasar tidak dapat diamati secara sempurna seperti eksperimen laboratorium. Karena itu, pencocokan B0 harus dilakukan menggunakan aturan yang jelas dan tidak boleh memilih pembanding berdasarkan hasil akhirnya.

---

## Declustering

**Declustering** adalah proses mengurangi atau mengendalikan event yang terlalu berdekatan agar satu episode pasar tidak dihitung berulang kali sebagai banyak bukti yang seolah-olah independen.

Misalnya, volume ekstrem muncul selama lima candle berturut-turut. Tanpa declustering, kelima candle tersebut mungkin dihitung sebagai lima event terpisah, padahal semuanya mungkin berasal dari satu episode yang sama.

Declustering dapat dilakukan dengan aturan seperti:

- hanya mengambil event pertama dalam radius waktu tertentu;
- memberi jarak minimum antar-event;
- atau memilih satu event representatif dari suatu kelompok.

Aturan declustering harus ditentukan sebelum evaluasi dan diterapkan secara konsisten pada B1 maupun B0 jika kontrak penelitian mengharuskannya.

---

## Edge

**Edge** adalah keunggulan informasi atau perbedaan hasil yang cukup kuat, konsisten, dan relevan dibandingkan pembanding yang adil.

Edge bukan sekadar:

- win rate tinggi;
- rata-rata return positif;
- satu periode profit;
- atau satu kandidat terbaik dari banyak percobaan.

Dalam TEKB, edge harus didukung oleh:

- definisi event yang jelas;
- entry yang realistis;
- pembanding B0 yang adil;
- pengukuran yang konsisten;
- pengujian ketidakpastian;
- pengendalian multiple testing;
- dan, bila diperlukan, validasi OOS.

Edge historis juga tidak menjamin bahwa keunggulan tersebut akan bertahan selamanya.

---

## Entry Gap

**Entry gap** adalah perbedaan antara harga sinyal atau harga referensi pada saat event terdeteksi dan harga entry aktual yang digunakan.

Misalnya, sinyal diketahui pada close bar T sebesar 1.000, tetapi entry dilakukan pada open bar T+1 sebesar 1.020. Maka terdapat gap entry sebesar 20 poin.

Entry gap penting karena harga entry yang lebih tinggi atau lebih rendah dapat mengubah:

- return;
- MAE;
- MFE;
- jarak stop-loss;
- jarak take-profit;
- dan kelayakan eksekusi.

Dalam TEKB, entry gap harus dicatat, bukan disembunyikan. Event dapat tetap valid untuk penelitian, tetapi belum tentu actionable secara langsung dalam kondisi live tertentu.

---

## Event

**Event** adalah kejadian yang memenuhi definisi atau aturan penelitian.

Contohnya:

- Relative Volume melewati threshold;
- breakout terjadi;
- pola tertentu muncul;
- candle konfirmasi terbentuk;
- atau kombinasi kondisi OHLCV terpenuhi.

Event harus memiliki identitas dan waktu yang jelas. Event bukan sekadar pola yang terlihat secara subjektif pada chart.

Informasi event dapat mencakup:

- instrumen;
- tanggal;
- waktu;
- sesi;
- slot;
- harga;
- volume;
- nilai indikator atau fitur;
- versi aturan;
- dan status validitas.

Event merupakan unit dasar yang kemudian dapat dipasangkan dengan B0, diukur, dan dievaluasi.

---

## Expectancy

**Expectancy** adalah nilai harapan rata-rata hasil dari serangkaian event atau trade berdasarkan distribusi hasil yang diamati.

Dalam bentuk sederhana, expectancy dapat dihitung sebagai rata-rata hasil per event:

> E(R) = (1/n) × Σ R_i

Jika hasil dinyatakan dalam satuan R, expectancy menunjukkan rata-rata berapa unit R yang dihasilkan atau hilang per event.

Contohnya, expectancy sebesar +0,15R berarti rata-rata hasil historis adalah positif 0,15R per event dalam definisi dan sampel yang digunakan.

Expectancy tidak menunjukkan:

- seberapa besar variasi hasil;
- seberapa besar kerugian terburuk;
- seberapa sering hasil positif;
- atau apakah hasil tersebut signifikan secara statistik.

Karena itu, expectancy harus dibaca bersama distribusi, MAE/MFE, biaya, ketidakpastian, dan hasil B0.

---

## FDR

**FDR** adalah singkatan dari False Discovery Rate, atau tingkat penemuan positif yang berpotensi salah.

Dalam penelitian dengan banyak pengujian, sebagian hasil yang tampak positif dapat muncul hanya karena kebetulan.

FDR berusaha mengendalikan proporsi temuan positif palsu di antara temuan yang dinyatakan positif.

FDR berbeda dari sekadar mengendalikan peluang satu kesalahan. FDR berfokus pada kumpulan hasil positif yang dipilih dari banyak pengujian.

Dalam TEKB, pengendalian FDR harus disertai pencatatan keluarga pengujian atau multiple-testing family.

---

## Freeze

**Freeze** adalah proses mengunci kandidat, aturan, definisi, parameter, dan konfigurasi penelitian sebelum pengujian OOS.

Freeze dapat mencakup:

- definisi event;
- definisi entry;
- aturan B0;
- definisi MAE/MFE;
- definisi ATR;
- Evaluation Engine;
- candidate grid;
- kriteria seleksi;
- keluarga multiple testing;
- serta identitas versi dan provenance.

Setelah freeze, hasil OOS tidak boleh digunakan untuk mengubah kandidat atau memperbaiki aturan secara diam-diam.

Jika aturan berubah setelah freeze, penelitian tersebut harus diperlakukan sebagai versi atau eksperimen baru.

---

## IS

**IS** adalah singkatan dari In-Sample, yaitu bagian data yang digunakan untuk:

- membangun hipotesis;
- mengembangkan aturan;
- menguji kandidat;
- membandingkan B1 dan B0;
- serta memilih kandidat yang akan dibekukan.

IS bukan bukti final bahwa suatu edge akan bertahan di masa depan. Hasil IS dapat terlalu optimistis karena kandidat dan aturan dibentuk menggunakan data tersebut.

Karena itu, kandidat yang dipilih melalui IS harus melalui freeze sebelum diuji pada OOS.

---

## Log Return

**Log return** adalah perubahan logaritmik harga antara dua waktu.

Rumus sederhananya:

> r_t+1 = ln(C_t+1 / C_t)

Keterangan:

- C_t adalah harga pada waktu t;
- C_t+1 adalah harga pada waktu berikutnya;
- ln adalah logaritma natural.

Log return sering digunakan dalam penelitian karena memiliki sifat matematis yang berguna, terutama ketika menggabungkan perubahan harga dalam beberapa periode.

Log return tetap harus dibedakan dari return sederhana. Keduanya tidak boleh dicampur tanpa penjelasan.

---

## MAE

**MAE** adalah singkatan dari Maximum Adverse Excursion, yaitu gerakan maksimum yang berlawanan dengan posisi selama horizon pengukuran.

Untuk posisi long, MAE terutama diukur dari seberapa jauh harga terendah bergerak di bawah harga entry.

Contoh:

- entry = 1.000;
- harga terendah selama horizon = 970.

Maka MAE raw dapat dicatat sebagai:

> MAE = 970 − 1000 = −30

Jika ATR entry adalah 15, maka:

> MAE_×ATR = −30 / 15 = −2

Artinya, harga sempat bergerak melawan posisi sejauh 2 ATR.

MAE berguna untuk memahami risiko intratrade dan mengevaluasi apakah kandidat stop-loss terlalu sempit atau terlalu lebar.

---

## MFE

**MFE** adalah singkatan dari Maximum Favorable Excursion, yaitu gerakan maksimum yang mendukung posisi selama horizon pengukuran.

Untuk posisi long, MFE diukur dari seberapa jauh harga tertinggi bergerak di atas harga entry.

Contoh:

- entry = 1.000;
- harga tertinggi selama horizon = 1.045.

Maka:

> MFE = 1045 − 1000 = 45

Jika ATR entry adalah 15, maka:

> MFE_×ATR = 45 / 15 = 3

Artinya, harga sempat bergerak mendukung posisi sejauh 3 ATR.

MFE bukan berarti profit tersebut pasti direalisasikan. MFE hanya menunjukkan peluang gerakan maksimum yang sempat tersedia selama horizon.

---

## OOS

**OOS** adalah singkatan dari Out-of-Sample, yaitu bagian data yang tidak digunakan untuk membangun, menyesuaikan, atau memilih kandidat penelitian.

OOS digunakan untuk menguji apakah hasil yang ditemukan pada IS memiliki kemungkinan untuk bertahan pada data yang belum digunakan saat proses pembentukan model atau aturan.

OOS harus dilakukan setelah freeze. Selama OOS:

- kandidat tidak boleh diganti berdasarkan hasil;
- definisi event tidak boleh diubah;
- Evaluation Engine harus tetap sama;
- aturan B0 harus tetap sama;
- dan hasil OOS tidak boleh dipakai berulang kali sebagai sumber tuning tanpa pencatatan.

Hasil OOS dapat berstatus:

- OOS_VALIDATED;
- OOS_REJECTED;
- OOS_SPENT;
- atau OOS_TAINTED.

OOS yang positif tetap bukan jaminan profit masa depan.

---

## Percentile

**Percentile** adalah ukuran posisi suatu nilai dibandingkan dengan distribusi data.

Persentil ke-95, misalnya, menunjukkan nilai yang lebih tinggi daripada sekitar 95% observasi dalam distribusi yang digunakan.

Dalam TEKB, percentile dapat digunakan untuk:

- mendeskripsikan ekstremitas data;
- menentukan threshold awal;
- membatasi rentang candidate grid;
- atau memahami posisi suatu event terhadap populasi historis.

Percentile tidak boleh digunakan secara sembarangan untuk memilih hasil terbaik setelah melihat seluruh data. Jika percentile dipakai sebagai bagian dari aturan penelitian, definisi populasi, periode, dan cara perhitungannya harus jelas.

---

## Relative Volume

**Relative Volume** adalah perbandingan volume aktual dengan volume baseline yang relevan.

Rumus sederhananya:

> RV_t = V_t / V_baseline,t

Contoh:

- volume aktual = 500.000;
- baseline volume = 100.000.

Maka:

> RV = 5

Artinya, volume aktual lima kali baseline.

Dalam data intraday, baseline sebaiknya memperhatikan sesi dan slot waktu agar volume pagi tidak dibandingkan secara tidak adil dengan volume siang atau sesi yang berbeda.

---

## RV

**RV** adalah singkatan dari Relative Volume.

RV mengukur seberapa besar volume saat ini dibandingkan dengan volume normal atau baseline yang telah ditentukan.

RV bukan ukuran arah harga. RV tinggi hanya menunjukkan bahwa aktivitas volume relatif besar. Harga dapat naik, turun, atau bergerak tidak menentu ketika RV meningkat.

Dalam TEKB, RV dapat digunakan sebagai fitur atau bagian dari definisi event, tetapi arah dan hasilnya harus diuji secara empiris.

---

## SAMSON

**SAMSON** adalah modul atau metode dalam TEKB yang digunakan untuk mendeteksi anomali volume.

SAMSON tidak dimaksudkan sebagai peramal arah harga. Fungsinya adalah menemukan kondisi ketika volume relatif tidak biasa dibandingkan baseline yang relevan.

Dalam implementasi intraday, SAMSON dapat menggunakan:

- timeframe tertentu, misalnya 5 menit;
- baseline berdasarkan sesi dan slot waktu;
- Relative Volume;
- threshold anomali;
- validasi data;
- dan declustering.

SAMSON menghasilkan event yang kemudian dapat diteliti. SAMSON sendiri bukan bukti bahwa event tersebut akan menghasilkan profit.

---

## TIMEOUT

**TIMEOUT** adalah status outcome ketika posisi atau event mencapai batas maksimum holding period tanpa terlebih dahulu mencapai kondisi exit yang ditentukan, seperti stop-loss atau take-profit.

TIMEOUT berbeda dari:

- INSUFFICIENT_HORIZON, yaitu data tidak cukup untuk menyelesaikan horizon yang diwajibkan;
- AMBIGUOUS_INTRABAR, yaitu urutan kejadian dalam candle tidak dapat dipastikan;
- atau INVALIDATED, yaitu event tidak memenuhi syarat validitas penelitian.

TIMEOUT adalah hasil evaluasi yang sah. Ia menunjukkan bahwa dalam batas waktu yang ditentukan, kondisi exit yang ditetapkan tidak tercapai.

---

## Worst-Case

**Worst-case** adalah skenario evaluasi yang menggunakan asumsi paling merugikan ketika urutan intrabar tidak dapat diketahui secara pasti.

Contohnya, dalam satu candle yang sama, harga menyentuh level stop-loss dan take-profit, tetapi data OHLC tidak menunjukkan level mana yang disentuh lebih dahulu.

Dalam kondisi tersebut, worst-case dapat mengasumsikan hasil yang paling buruk bagi posisi, misalnya stop-loss dianggap terjadi lebih dahulu.

Worst-case membantu menguji apakah kandidat tetap memiliki keunggulan ketika ketidakpastian eksekusi diperlakukan secara konservatif.

Worst-case bukan berarti semua trade pasti mengalami hasil terburuk. Ia adalah skenario evaluasi untuk menguji ketahanan klaim.

---

## Best-Case

**Best-case** adalah skenario evaluasi yang menggunakan asumsi paling menguntungkan ketika urutan intrabar tidak dapat diketahui secara pasti.

Dalam contoh candle yang menyentuh stop-loss dan take-profit pada bar yang sama, best-case dapat mengasumsikan take-profit tercapai lebih dahulu.

Best-case berguna sebagai batas atas atau skenario optimistis. Namun, hasil best-case tidak boleh diperlakukan sebagai hasil aktual yang pasti terjadi.

Dalam penelitian yang ketat, worst-case dan best-case harus dilaporkan secara terpisah dan tidak boleh dicampur menjadi satu angka tanpa penjelasan.

---

## Penutup Glosarium

Glosarium ini membantu pembaca memahami bahasa dasar TEKB. Namun, definisi singkat tidak menggantikan kontrak metodologi yang lebih lengkap.

Dalam penelitian nyata, setiap istilah harus memiliki:

- definisi formal;
- aturan implementasi;
- versi;
- waktu ketersediaan data;
- dan hubungan yang jelas dengan komponen penelitian lainnya.

Dengan demikian, istilah seperti B0, event, entry, MAE, MFE, freeze, dan OOS bukan hanya kosakata teknis. Semuanya merupakan bagian dari sistem pengendalian agar penelitian tetap dapat ditelusuri, dibandingkan, diuji, dan dipertanggungjawabkan.

---

<div align="center">

[← Bab Sebelumnya](/posts/bab-25-tekb-disiplin-berpikir/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Lampiran B →](/posts/lampiran-b-rumus-dasar/)

</div>