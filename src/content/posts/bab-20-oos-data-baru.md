---
title: "BAB 20 — OOS: Apakah Hasil Historis Bertahan pada Data Baru?"
published: 2026-09-12
description: "OOS adalah pengujian terhadap data baru, bukan tempat memperbaiki strategi. Bab ini menjelaskan aturan OOS, status hasil, dan konsep OOS spent atau tainted."
tags: ["bab-20", "oos", "validasi", "generalisasi"]
category: "Bab"
draft: false
lang: ""
---

**BAGIAN VI — FREEZE, OOS, DAN GENERALISASI**

---

## Tujuan Bab

Bab ini menjelaskan Out-of-Sample (OOS) sebagai pengujian terhadap kemampuan suatu hasil penelitian untuk bertahan pada data yang tidak digunakan ketika aturan atau kandidat dibangun dan dipilih.

Dalam penelitian trading, hasil historis dapat terlihat sangat baik karena peneliti telah mencoba banyak aturan, periode, indikator, parameter, atau kombinasi. Karena itu, hasil yang bagus pada data lama belum tentu menunjukkan bahwa suatu kondisi benar-benar memiliki information edge.

OOS digunakan untuk menguji pertanyaan yang lebih sulit:

> "Setelah aturan dipilih dan dibekukan, apakah aturan tersebut masih menunjukkan hasil yang sesuai ketika diterapkan pada data yang belum digunakan untuk memilihnya?"

OOS bukan tempat untuk mencari hasil terbaik. OOS adalah tempat untuk menguji apakah keputusan yang telah dibuat sebelumnya dapat bertahan tanpa penyesuaian berdasarkan hasil baru.

---

## 20.1. Apa Itu Out-of-Sample?

**Out-of-Sample**, atau **OOS**, adalah bagian data yang tidak digunakan untuk membangun, mengoptimalkan, atau memilih kandidat penelitian.

Data OOS disimpan untuk tahap pengujian setelah proses pengembangan dan seleksi selesai.

Secara sederhana, penelitian dapat dibagi menjadi:

- **In-Sample (IS):** data untuk membangun, menguji, dan memilih kandidat sesuai kontrak penelitian;
- **Out-of-Sample (OOS):** data yang disimpan untuk menguji kandidat yang sudah dibekukan.

Contoh pembagian:

| Tahap | Periode | Fungsi |
|---|---|---|
| IS | 2016–2021 | Pengembangan dan seleksi kandidat |
| OOS | 2022–2026 | Pengujian kandidat yang telah dibekukan |

Pembagian periode tersebut hanya contoh. Dalam penelitian nyata, pembagian harus ditentukan sebelum hasil OOS dilihat.

### OOS bukan sekadar data yang lebih baru

Data yang lebih baru belum tentu benar-benar OOS.

Suatu periode hanya dapat disebut OOS jika periode tersebut:

- tidak digunakan untuk memilih kandidat;
- tidak digunakan untuk menentukan parameter;
- tidak digunakan untuk mengubah aturan;
- tidak digunakan untuk memilih B0;
- tidak digunakan untuk menentukan horizon atau grid setelah melihat hasil;
- dan tidak digunakan untuk mengambil keputusan pengembangan sebelum pengujian selesai.

Jika data tahun 2025 disebut OOS, tetapi peneliti berkali-kali melihat hasil 2025 lalu mengubah strategi, maka data tersebut tidak lagi berfungsi sebagai OOS yang murni.

### Analogi ujian yang belum pernah dilihat

Bayangkan seorang siswa belajar menghadapi ujian.

Buku latihan dan soal-soal yang digunakan untuk belajar adalah IS.

Ujian dengan soal yang belum pernah dilihat adalah OOS.

Jika siswa mendapatkan nilai tinggi pada soal latihan, hal itu menunjukkan bahwa ia mampu menjawab soal yang sudah dipelajari. Namun, nilai tersebut belum cukup untuk membuktikan bahwa ia memahami materi secara umum.

Ujian baru membantu menguji apakah kemampuan tersebut dapat diterapkan pada soal yang belum pernah dilihat.

Dalam penelitian trading:

- IS menunjukkan bagaimana kandidat bekerja pada data yang digunakan selama pengembangan;
- OOS menguji apakah hasil tersebut bertahan pada data yang tidak digunakan untuk memilih kandidat.

### Mengapa OOS lebih dekat dengan pengujian generalisasi?

**Generalisasi** berarti kemampuan suatu metode untuk bekerja pada data baru yang masih relevan dengan masalah penelitian.

Strategi yang hanya cocok dengan data IS mungkin telah menghafal karakteristik tertentu dari masa lalu. Sebaliknya, strategi yang tetap menunjukkan hasil sesuai kriteria pada OOS memberikan bukti tambahan bahwa hasil IS tidak sepenuhnya bergantung pada kebetulan atau overfitting.

Namun, OOS bukan pembuktian mutlak. OOS hanya memberikan satu pengujian historis tambahan terhadap generalisasi.

---

## 20.2. Aturan OOS TEKB

OOS harus diperlakukan sebagai tahap pengujian yang memiliki aturan ketat. Jika aturan OOS dapat diubah setelah hasil dilihat, maka fungsi OOS sebagai pengujian independen akan melemah.

TEKB menetapkan beberapa prinsip utama.

### 20.2.1. Kandidat dibekukan sebelum OOS

Sebelum OOS dimulai, kandidat yang akan diuji harus sudah ditentukan dan dibekukan.

Yang dibekukan dapat mencakup:

- definisi event;
- aturan deteksi;
- aturan konfirmasi;
- aturan entry;
- harga entry;
- horizon;
- definisi B0;
- definisi MAE/MFE;
- ATR;
- candidate grid;
- aturan stop-loss dan take-profit;
- evaluation engine;
- biaya dan friction;
- kriteria evaluasi;
- aturan penanganan data tidak lengkap;
- aturan status hasil;
- dan versi seluruh komponen metodologi.

Artinya, setelah kandidat masuk tahap OOS, peneliti tidak boleh berkata:

> "Karena hasil OOS kurang bagus, kita ubah sedikit parameternya."

Perubahan tersebut mungkin sah sebagai penelitian baru, tetapi hasilnya tidak boleh tetap disebut sebagai hasil OOS dari kandidat lama.

### 20.2.2. Engine harus sama

Kandidat B1 dan pembanding B0 harus dievaluasi menggunakan engine yang sama.

Kesamaan engine mencakup:

- aturan entry;
- aturan horizon;
- definisi MAE/MFE;
- aturan evaluasi exit;
- aturan gap;
- aturan biaya;
- aturan slippage;
- aturan same-bar ambiguity;
- aturan data tidak lengkap;
- dan aturan status hasil.

Jika engine berubah setelah melihat OOS, hasil OOS menjadi sulit dibandingkan dengan hasil IS.

Contoh kesalahan:

- IS menggunakan entry pada open bar berikutnya;
- OOS menggunakan close bar sinyal;
- IS memakai satu aturan gap;
- OOS menghapus gap yang merugikan;
- IS memakai friction tertentu;
- OOS memakai biaya yang lebih rendah agar hasil terlihat lebih baik.

Perubahan seperti itu merusak konsistensi pengujian.

### 20.2.3. Kriteria harus sama

Kriteria yang digunakan untuk menilai hasil OOS harus ditentukan sebelum OOS dan tetap sama dengan kriteria yang telah ditetapkan dalam kontrak.

Misalnya, kriteria OOS mensyaratkan:

- jumlah event minimum;
- jumlah tanggal minimum;
- jumlah instrumen minimum;
- delta terhadap B0 tidak negatif atau memenuhi ambang tertentu;
- ketahanan terhadap friction;
- batas ketidakpastian;
- dan kriteria robustness tertentu.

Kriteria tersebut tidak boleh diganti setelah hasil OOS terlihat.

Contoh yang tidak sah:

> "Kriteria awal membutuhkan delta positif dan survival pada friction R2. Karena OOS gagal di R2, kita gunakan R0 saja."

Jika perubahan dilakukan setelah melihat hasil, maka keputusan tersebut bukan lagi pengujian OOS sesuai kriteria awal.

### 20.2.4. Tidak melakukan tuning setelah melihat OOS

**Tuning** adalah proses mengubah aturan, parameter, grid, atau keputusan agar hasil menjadi lebih baik.

Tuning dapat berupa:

- mengubah periode indikator;
- mengubah ambang event;
- mengubah horizon;
- mengubah stop-loss;
- mengubah take-profit;
- mengubah definisi konfirmasi;
- mengganti saham yang digunakan;
- menghapus event yang hasilnya buruk;
- mengganti B0;
- mengubah biaya;
- atau memilih subset OOS yang paling menguntungkan.

Tuning setelah melihat OOS membuat data OOS ikut digunakan dalam pengembangan.

Akibatnya, OOS tersebut tidak lagi benar-benar independen dari proses seleksi.

Jika peneliti ingin melakukan tuning berdasarkan hasil OOS, proses tersebut harus dicatat sebagai tahap pengembangan baru. Setelah tuning, diperlukan periode OOS baru yang belum digunakan.

### 20.2.5. Tidak melakukan FDR ulang untuk mengubah keputusan

Multiple testing dan pengendalian false discovery rate harus memiliki aturan yang jelas.

Dalam penelitian TEKB, family pengujian, metode koreksi, dan cara mengambil keputusan harus ditentukan sesuai kontrak penelitian.

Pada tahap OOS, peneliti tidak boleh melakukan koreksi atau pengelompokan ulang hanya untuk membuat kandidat terlihat lolos.

Contoh perubahan yang bermasalah:

- mengganti definisi family setelah melihat hasil OOS;
- mengeluarkan kandidat yang gagal dari family;
- memasukkan hanya hasil yang positif;
- mengubah metode koreksi agar kandidat tertentu lolos;
- mengulang pengujian sampai memperoleh keputusan yang diinginkan.

FDR atau metode multiple-testing lainnya bukan alat untuk memperbaiki hasil yang gagal. Metode tersebut merupakan bagian dari prosedur pengendalian kesalahan yang harus ditetapkan secara transparan.

Jika ada alasan metodologis untuk melakukan analisis tambahan, analisis tersebut harus diberi label sebagai analisis tambahan atau eksploratif, bukan disamakan dengan keputusan OOS utama.

### 20.2.6. Tidak mengganti B0 setelah melihat hasil

B0 merupakan pembanding yang telah ditentukan berdasarkan aturan, bukan berdasarkan hasil yang paling menguntungkan.

Pada tahap OOS, B0 tidak boleh diganti hanya karena:

- B0 menghasilkan return yang terlalu tinggi;
- B0 membuat delta B1 terlihat kecil;
- B0 menghasilkan hasil yang tidak sesuai harapan;
- B0 dianggap terlalu sulit dikalahkan;
- atau B0 yang lain menghasilkan perbandingan lebih menarik.

Jika aturan B0 berubah setelah hasil OOS dilihat, maka perbandingan B1 versus B0 tidak lagi mengikuti kontrak awal.

Perubahan B0 dapat dilakukan untuk penelitian baru, tetapi harus dicatat sebagai perubahan metodologi dan tidak boleh disamarkan sebagai hasil OOS dari penelitian sebelumnya.

### 20.2.7. Ringkasan aturan OOS

| Aturan | Prinsip TEKB |
|---|---|
| Kandidat | Dibekukan sebelum OOS |
| Engine | Sama dengan yang telah ditentukan |
| Kriteria | Tidak berubah setelah hasil dilihat |
| Tuning | Tidak dilakukan pada OOS utama |
| Multiple testing | Tidak diubah untuk memaksakan kelulusan |
| B0 | Tidak diganti berdasarkan hasil OOS |
| Audit | Semua versi dan keputusan dicatat |

Inti dari aturan tersebut adalah:

> OOS harus menguji keputusan yang sudah dibuat, bukan menjadi tempat membuat keputusan baru berdasarkan hasil yang terlihat.

---

## 20.3. Status Hasil OOS

Hasil OOS perlu memiliki status yang jelas. Status tersebut harus membedakan antara:

- hasil yang sekadar positif;
- hasil yang memenuhi kriteria;
- hasil yang tidak memenuhi kriteria;
- hasil yang tidak dapat dinilai karena masalah data atau validitas.

Dua status utama yang digunakan dalam kerangka ini adalah:

- **OOS_VALIDATED**;
- **OOS_REJECTED**.

### 20.3.1. OOS_VALIDATED

Status **OOS_VALIDATED** berarti kandidat yang telah dibekukan berhasil memenuhi kriteria OOS yang telah ditentukan sebelumnya.

Status ini tidak berarti strategi tersebut pasti menguntungkan di masa depan. Status ini berarti:

- kandidat diuji pada data yang tidak digunakan untuk memilihnya;
- aturan dan engine tetap sama;
- kriteria penilaian telah ditentukan sebelumnya;
- hasil OOS memenuhi kriteria yang ditetapkan;
- tidak ada perubahan metodologi untuk memaksakan kelulusan.

Contoh:
OOS_VALIDATED

Interpretasi yang tepat:

> Kandidat memenuhi kriteria validasi OOS yang telah ditentukan dalam kontrak penelitian.

Interpretasi yang tidak tepat:

> Kandidat pasti akan menghasilkan profit di masa depan.

OOS_VALIDATED adalah hasil validasi historis, bukan jaminan performa masa depan.

### 20.3.2. OOS_REJECTED

Status **OOS_REJECTED** berarti kandidat yang telah dibekukan tidak memenuhi satu atau lebih kriteria OOS yang telah ditentukan.

Contoh penyebab:

- delta terhadap B0 tidak memenuhi ambang;
- hasil tidak bertahan setelah biaya;
- jumlah event valid terlalu sedikit;
- ketidakpastian terlalu besar;
- robustness tidak terpenuhi;
- hasil hanya positif pada sebagian kecil instrumen;
- atau kriteria utama lainnya gagal.

Status:
OOS_REJECTED

Status ini tidak berarti penelitian tersebut tidak berguna. Hasil gagal tetap memberikan informasi penting bahwa kandidat tersebut tidak memperoleh dukungan yang cukup berdasarkan kontrak pengujian.

### 20.3.3. Hasil OOS positif tidak selalu berarti tervalidasi

Sebuah kandidat dapat menghasilkan return positif pada OOS, tetapi tetap tidak memenuhi kriteria validasi.

Contoh:

- Return OOS = +2%;
- B0 = +1,8%;
- Delta = +0,2 poin persentase;
- Namun, interval ketidakpastian terlalu lebar;
- atau hasil tidak bertahan setelah friction;
- atau jumlah event terlalu sedikit.

Dalam situasi ini, hasil OOS memang positif secara nominal, tetapi belum memenuhi kriteria validasi.

Karena itu, perlu dibedakan:

> Positif secara angka tidak sama dengan lulus secara metodologis.

Contoh tabel:

| Kandidat | Return B1 | Return B0 | Delta | Kriteria lain | Status |
|---|---|---|---|---|---|
| C1 | +4,0% | +2,0% | +2,0 pp | Semua terpenuhi | OOS_VALIDATED |
| C2 | +2,0% | +1,8% | +0,2 pp | Ketidakpastian terlalu besar | OOS_REJECTED |
| C3 | -1,0% | +0,5% | -1,5 pp | Tidak terpenuhi | OOS_REJECTED |

Angka di atas hanya ilustrasi. Dalam penelitian nyata, keputusan harus mengikuti kontrak dan hasil lengkap, bukan satu angka return.

### 20.3.4. Mengapa OOS_REJECTED harus tetap dicatat?

Kandidat yang ditolak tidak boleh dihapus hanya karena hasilnya tidak sesuai harapan.

Menghapus kandidat yang gagal dapat menimbulkan gambaran yang menyesatkan, seolah-olah hanya kandidat yang berhasil pernah diuji.

Semua kandidat yang masuk proses seleksi harus memiliki catatan:

- identitas kandidat;
- aturan yang diuji;
- versi metodologi;
- hasil IS;
- hasil OOS;
- kriteria yang gagal;
- alasan penolakan;
- dan status akhir.

Contoh:

| Candidate ID | IS Status | OOS Status | Alasan |
|---|---|---|---|
| C001 | Selected | OOS_VALIDATED | Semua kriteria terpenuhi |
| C002 | Selected | OOS_REJECTED | Tidak tahan friction R2 |
| C003 | Selected | OOS_REJECTED | Delta terhadap B0 tidak cukup |
| C004 | Selected | OOS_REJECTED | Jumlah event valid terlalu sedikit |

Pencatatan ini penting untuk:

- menjaga integritas penelitian;
- mencegah cherry-picking;
- memahami kegagalan generalisasi;
- menghindari pengulangan kesalahan yang sama;
- memperlihatkan bahwa seleksi tidak hanya melaporkan pemenang;
- membedakan hasil yang benar-benar diuji dari hasil yang hanya dipilih untuk dipublikasikan.

### 20.3.5. Status OOS bukan pengganti laporan hasil

Status seperti OOS_VALIDATED atau OOS_REJECTED harus disertai laporan yang cukup, misalnya:

- jumlah event;
- jumlah event valid;
- jumlah tanggal;
- jumlah instrumen;
- return B1;
- return B0;
- delta;
- distribusi hasil;
- MAE/MFE;
- hasil setelah friction;
- interval ketidakpastian;
- hasil robustness;
- alasan keputusan;
- dan versi metodologi.

Status adalah ringkasan keputusan, bukan pengganti bukti yang mendasarinya.

---

## 20.4. Mengapa OOS Bukan Jaminan Masa Depan?

OOS merupakan alat penting untuk mengurangi risiko overfitting, tetapi OOS tidak dapat menghapus semua ketidakpastian.

Bahkan jika sebuah kandidat memperoleh status OOS_VALIDATED, masa depan tetap dapat berbeda dari masa lalu.

### 20.4.1. OOS hanya satu periode historis yang belum digunakan

OOS adalah bagian tertentu dari sejarah.

Misalnya, peneliti menggunakan:

- IS: 2016–2021;
- OOS: 2022–2026.

OOS 2022–2026 tetap hanya mewakili kondisi pasar pada periode tersebut. Ia belum tentu mencakup semua kondisi yang mungkin terjadi pada masa depan.

OOS mungkin mencakup:

- tren naik;
- tren turun;
- volatilitas tinggi;
- volatilitas rendah;
- krisis;
- pemulihan;
- perubahan likuiditas;
- perubahan kebijakan;
- atau perubahan perilaku pelaku pasar.

Namun, tidak ada jaminan bahwa seluruh jenis kondisi masa depan telah terwakili.

### 20.4.2. Kondisi pasar dapat berubah

Information edge dapat melemah atau hilang karena perubahan struktur pasar.

Contoh penyebab:

- semakin banyak pelaku menggunakan sinyal yang sama;
- likuiditas berubah;
- biaya transaksi berubah;
- regulasi berubah;
- komposisi pelaku pasar berubah;
- teknologi eksekusi berubah;
- karakteristik instrumen berubah;
- perusahaan mengalami perubahan fundamental;
- atau hubungan historis antara kondisi dan return tidak lagi sama.

Dengan demikian, hasil OOS yang baik tidak berarti hubungan tersebut bersifat permanen.

### 20.4.3. OOS mengurangi risiko overfitting, tetapi tidak menghapusnya

OOS membantu mengurangi risiko bahwa hasil IS hanya merupakan produk dari penyesuaian terhadap data lama.

Namun, OOS sendiri masih dapat menghasilkan hasil yang tampak baik secara kebetulan, terutama jika:

- OOS terlalu pendek;
- jumlah event terlalu sedikit;
- variasi kondisi pasar terbatas;
- banyak kandidat tetap diuji secara tidak terkendali;
- peneliti terus mengulang penggunaan OOS;
- atau hasil OOS dipilih dari banyak percobaan tanpa pencatatan yang lengkap.

OOS adalah lapisan perlindungan, bukan jaminan mutlak.

### 20.4.4. Generalisasi tidak sama dengan kepastian

Jika kandidat bekerja pada IS dan OOS, kesimpulan yang lebih tepat adalah:

> "Kandidat menunjukkan bukti historis yang konsisten pada data pengembangan dan data OOS sesuai kriteria yang ditentukan."

Kesimpulan yang terlalu jauh adalah:

> "Kandidat pasti akan bekerja di masa depan."

Penelitian berbasis data tidak dapat memberikan kepastian mutlak mengenai return berikutnya. Yang dapat diberikan adalah tingkat bukti, batas ketidakpastian, dan kondisi di mana hasil tersebut ditemukan.

### 20.4.5. Apa yang sebenarnya diberikan oleh OOS?

OOS dapat memberikan:

- bukti tambahan bahwa hasil tidak hanya cocok dengan IS;
- informasi tentang stabilitas hasil;
- informasi tentang kelemahan kandidat;
- gambaran apakah delta terhadap B0 bertahan;
- gambaran ketahanan terhadap biaya;
- dan dasar untuk menilai apakah penelitian layak dilanjutkan.

OOS tidak memberikan:

- kepastian profit;
- jaminan bahwa kondisi akan selalu sama;
- bukti kausalitas otomatis;
- jaminan bebas dari semua bias;
- atau jaminan bahwa kandidat akan bekerja pada semua instrumen dan semua periode.

---

## 20.5. OOS Window Spent dan Tainted

Salah satu konsep penting dalam penelitian yang disiplin adalah bahwa status "belum dilihat" dapat hilang.

OOS bukan sekadar label pada tanggal. OOS adalah status metodologis yang bergantung pada bagaimana data tersebut digunakan.

### 20.5.1. Apa itu OOS window spent?

**OOS window spent** berarti periode OOS telah digunakan dalam proses pengembangan, penyesuaian, evaluasi berulang, atau pengambilan keputusan yang memengaruhi kandidat.

Pada awalnya, sebuah periode mungkin benar-benar belum digunakan. Namun, setelah hasilnya dilihat dan digunakan untuk mengubah penelitian, periode tersebut telah "terpakai" sebagai data independen.

Contoh:

1. Peneliti menetapkan 2022–2026 sebagai OOS.
2. Kandidat diuji dan hasilnya dilihat.
3. Peneliti mengubah threshold karena hasil OOS kurang baik.
4. Kandidat baru diuji kembali pada periode 2022–2026.
5. Peneliti memilih kandidat yang hasilnya paling baik.

Dalam kondisi tersebut, periode 2022–2026 telah digunakan untuk tuning. Ia tidak lagi dapat diperlakukan sebagai OOS murni untuk kandidat baru.

### 20.5.2. Apa itu tainted OOS?

OOS disebut **tainted** atau tercemar secara metodologis ketika data OOS telah memengaruhi keputusan pengembangan atau seleksi.

Contoh penggunaan yang dapat membuat OOS tainted:

- mengubah parameter setelah melihat hasil;
- mengganti definisi event;
- mengubah entry;
- mengubah horizon;
- mengubah B0;
- memilih hanya saham atau periode yang menguntungkan;
- menghapus event buruk;
- memilih candidate grid baru;
- mengubah kriteria kelulusan;
- mengulang pengujian sampai hasil sesuai harapan;
- atau menggunakan hasil OOS untuk memutuskan kandidat final.

Masalahnya bukan karena data OOS dilihat. Dalam praktik penelitian, hasil OOS memang perlu dilihat untuk membuat laporan. Masalahnya muncul ketika hasil tersebut digunakan untuk mengubah kandidat lalu hasil yang sama masih diklaim sebagai pengujian independen.

### 20.5.3. Melihat hasil berbeda dari menggunakan hasil untuk tuning

Perlu dibedakan dua kegiatan:

**Melihat hasil untuk pelaporan:**

- menjalankan pengujian;
- menyimpan hasil;
- membuat laporan;
- menetapkan status sesuai kriteria yang telah ditentukan.

Hal ini merupakan fungsi normal OOS.

**Menggunakan hasil untuk mengubah kandidat:**

- mengganti parameter;
- mengubah event;
- memilih hasil yang lebih baik;
- mengubah B0;
- mengubah kriteria;
- atau mengulang seleksi berdasarkan hasil OOS.

Hal ini membuat OOS ikut masuk ke proses pengembangan.

Dengan kata lain:

> Melihat OOS untuk menilai hasil adalah bagian dari pengujian. Menggunakan OOS untuk memperbaiki kandidat membuat OOS menjadi bagian dari proses pengembangan.

### 20.5.4. Mengapa penggunaan ulang harus dicatat?

Penggunaan ulang OOS tidak selalu berarti penelitian harus dihentikan. Namun, penggunaannya harus dicatat secara jujur.

Audit trail sebaiknya mencatat:

- periode OOS;
- tanggal pertama kali hasil OOS dilihat;
- siapa atau proses apa yang mengakses hasil;
- apakah hasil memengaruhi perubahan kandidat;
- versi kandidat sebelum dan sesudah perubahan;
- apakah periode tersebut masih dianggap OOS;
- dan periode baru yang digunakan jika diperlukan.

Contoh catatan:

| Periode | Penggunaan | Status |
|---|---|---|
| 2022–2026 | Pengujian pertama, kandidat telah freeze | OOS valid untuk pengujian pertama |
| 2022–2026 | Digunakan untuk mengubah threshold | Tainted untuk kandidat hasil tuning |
| 2027–2029 | Belum digunakan setelah freeze baru | Dapat menjadi OOS baru |

Pencatatan ini mencegah peneliti menyebut suatu periode sebagai "data baru" berulang kali padahal periode tersebut telah digunakan untuk mengambil keputusan.

### 20.5.5. Mengapa OOS tidak boleh dianggap sebagai cadangan tanpa batas?

Jika peneliti terus menggunakan periode OOS untuk:

- menguji kandidat;
- memperbaiki kandidat;
- menguji ulang;
- memilih hasil terbaik;
- memperbaiki lagi;
- lalu melaporkan hasil terakhir sebagai OOS;

maka OOS secara bertahap berubah menjadi bagian dari data pengembangan.

Walaupun tanggalnya tetap sama, status independennya telah berkurang atau hilang.

Karena itu, periode OOS harus diperlakukan sebagai sumber daya penelitian yang terbatas.

Prinsipnya:

> Setiap kali data OOS digunakan untuk memengaruhi keputusan pengembangan, nilai independennya berkurang.

Jika pengembangan baru dilakukan setelah melihat OOS, diperlukan salah satu tindakan berikut:

- mengakui bahwa periode tersebut telah menjadi tainted;
- memindahkan kandidat baru ke tahap pengembangan;
- melakukan freeze ulang;
- menggunakan periode OOS baru yang belum dilihat;
- atau melakukan penelitian lanjutan dengan desain validasi yang lebih tepat, misalnya walk-forward atau nested validation.

### 20.5.6. OOS yang tainted bukan berarti datanya harus dihapus

Data yang tainted tetap berguna.

Data tersebut dapat digunakan untuk:

- memahami kelemahan kandidat;
- mengevaluasi perubahan;
- membuat hipotesis baru;
- mendokumentasikan proses penelitian;
- atau mengembangkan versi metodologi berikutnya.

Yang tidak boleh dilakukan adalah menyebut hasil tersebut sebagai OOS independen dari kandidat yang telah dipengaruhi oleh data itu sendiri.

Contoh:

> Kandidat A diuji pada OOS 2022–2026 dan gagal. Peneliti mengubah threshold menjadi Kandidat B setelah melihat hasil tersebut. Pengujian Kandidat B pada 2022–2026 boleh dilakukan sebagai eksperimen pengembangan, tetapi hasilnya tidak boleh disebut validasi OOS independen untuk Kandidat B.

Untuk memvalidasi Kandidat B secara lebih jujur, diperlukan data baru yang belum digunakan untuk memilih Kandidat B.

---

## Penutup Bab 20

OOS merupakan salah satu tahap paling penting dalam penelitian TEKB karena memaksa peneliti menguji hasil pada data yang tidak digunakan untuk membangun atau memilih kandidat.

Prinsip utamanya adalah:

- OOS adalah data yang belum digunakan untuk pengembangan;
- kandidat harus dibekukan sebelum OOS;
- engine dan kriteria harus tetap sama;
- tuning tidak boleh dilakukan pada OOS utama;
- B0 tidak boleh diganti berdasarkan hasil;
- hasil positif tidak otomatis berarti tervalidasi;
- OOS_REJECTED harus tetap dicatat;
- OOS mengurangi risiko overfitting, tetapi tidak menjamin masa depan;
- dan OOS yang digunakan untuk tuning menjadi tainted.

Kesimpulan yang sehat bukan:

> "Strategi ini pasti berhasil karena OOS positif."

Melainkan:

> "Kandidat ini telah diuji pada data yang tidak digunakan untuk memilihnya. Berdasarkan kriteria yang telah ditentukan, hasilnya dinyatakan tervalidasi atau ditolak. Hasil tersebut merupakan bukti historis dengan ketidakpastian dan batas generalisasi tertentu."

Dalam TEKB, OOS bukan panggung untuk mempercantik hasil. OOS adalah ujian terhadap kejujuran proses penelitian.

---

## Ringkasan Bab

- OOS adalah data yang tidak digunakan untuk membangun, mengoptimalkan, atau memilih kandidat.
- OOS bukan sekadar data yang lebih baru — ia harus benar-benar belum digunakan untuk pengambilan keputusan.
- Kandidat harus dibekukan sebelum OOS dimulai.
- Engine, kriteria, dan B0 harus tetap sama antara IS dan OOS.
- Tuning setelah melihat OOS membuat data OOS tercemar.
- Hasil OOS dapat berstatus OOS_VALIDATED atau OOS_REJECTED.
- Hasil positif tidak otomatis berarti tervalidasi.
- OOS_REJECTED harus tetap dicatat sebagai bagian dari audit trail.
- OOS mengurangi risiko overfitting, tetapi tidak menghapusnya.
- OOS yang digunakan untuk tuning menjadi spent atau tainted.

---

## Pertanyaan Refleksi

1. Apa perbedaan antara data yang lebih baru dan data yang benar-benar OOS?
2. Mengapa kandidat harus dibekukan sebelum OOS?
3. Mengapa engine dan kriteria OOS tidak boleh diubah setelah hasil dilihat?
4. Apa arti OOS_VALIDATED?
5. Apa arti OOS_REJECTED?
6. Mengapa hasil OOS positif tidak selalu berarti tervalidasi?
7. Mengapa OOS_REJECTED harus tetap dicatat?
8. Mengapa OOS bukan jaminan masa depan?
9. Apa yang dimaksud dengan OOS spent atau tainted?
10. Mengapa OOS harus diperlakukan sebagai sumber daya yang terbatas?

---

## Kalimat Kunci

> OOS bukan panggung untuk mempercantik hasil. OOS adalah ujian terhadap kejujuran proses penelitian. Kandidat yang lulus OOS bukan berarti pasti berhasil di masa depan, tetapi setidaknya telah diuji pada data yang tidak digunakan untuk memilihnya.

---

<div align="center">

[← Bab Sebelumnya](/posts/bab-19-freeze-kandidat/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Bab Selanjutnya →](/posts/bab-21-perjalanan-satu-event/)

</div>