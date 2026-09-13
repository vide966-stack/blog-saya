---
title: "BAB 19 — Freeze: Mengapa Kandidat Harus Dikunci Sebelum OOS?"
published: 2026-09-12
description: "Freeze berarti mengunci kandidat dan seluruh aturan sebelum OOS. Bab ini menjelaskan apa yang harus dibekukan, mengapa OOS tidak boleh untuk tuning, dan freeze manifest."
tags: ["bab-19", "freeze", "oos", "validasi"]
category: "Bab"
draft: false
lang: ""
---

**BAGIAN VI — FREEZE, OOS, DAN GENERALISASI**

---

Setelah penelitian dilakukan pada data In-Sample atau IS, mungkin ada satu atau beberapa kandidat yang terlihat menjanjikan. Kandidat tersebut bisa berupa aturan entry tertentu, kombinasi Stop Loss dan Take Profit, batas waktu holding, atau kondisi khusus yang tampak memiliki hasil lebih baik daripada pembandingnya.

Namun, hasil yang terlihat baik pada data penelitian belum otomatis membuktikan bahwa kandidat tersebut dapat bekerja pada data baru. Kandidat masih harus diuji pada data yang tidak digunakan ketika aturan dan parameter dipilih. Data inilah yang disebut **Out-of-Sample** atau **OOS**.

Agar pengujian OOS benar-benar memiliki arti, kandidat yang akan diuji harus dikunci terlebih dahulu. Proses penguncian inilah yang disebut **freeze**.

---

## 19.1. Apa Arti Freeze?

Secara sederhana, **freeze** berarti membekukan seluruh aturan, definisi, dan kandidat penelitian sebelum hasil OOS dilihat atau digunakan untuk mengambil keputusan.

Setelah freeze dilakukan, peneliti tidak boleh lagi mengubah kandidat hanya karena ingin memperoleh hasil OOS yang lebih baik. Kandidat yang telah dibekukan harus diuji sebagaimana adanya.

Freeze bukan berarti kandidat telah terbukti benar. Freeze juga bukan jaminan bahwa kandidat akan menghasilkan keuntungan. Freeze hanya memastikan bahwa tahap validasi dilakukan terhadap sesuatu yang sudah ditentukan sebelumnya, bukan sesuatu yang terus-menerus disesuaikan berdasarkan hasil pengujian.

### 19.1.1. Mengunci Kandidat yang Dipilih

Kandidat yang dipilih melalui proses IS Selection harus ditetapkan secara jelas.

Misalnya, hasil seleksi memilih kandidat berikut:

- Entry: NEXT_VALID_BAR_OPEN.
- Stop Loss: 1 × ATR.
- Take Profit: 2 × ATR.
- Maximum Hold: 5 bar.
- Posisi: long-only.
- Evaluasi: menggunakan Evaluation Engine versi tertentu.

Setelah freeze, kombinasi tersebut tidak boleh diubah menjadi:

- Stop Loss 0,8 × ATR karena hasil OOS kurang baik;
- Take Profit 1,5 × ATR karena lebih sering terkena;
- Maximum Hold 10 bar karena harga membutuhkan waktu lebih lama;
- Entry pada harga yang berbeda karena entry awal dianggap kurang menguntungkan.

Perubahan seperti itu mungkin saja dilakukan dalam penelitian baru, tetapi tidak boleh dianggap sebagai pengujian OOS terhadap kandidat lama.

### 19.1.2. Mengunci Definisi Entry

Definisi entry menentukan kapan dan pada harga apa sebuah event dianggap mulai menjadi posisi penelitian.

Contohnya, TEKB dapat menggunakan aturan:

> Sinyal dikonfirmasi pada penutupan bar T, kemudian entry penelitian dilakukan pada Open bar valid berikutnya.

Aturan ini harus dikunci. Peneliti tidak boleh mengubahnya setelah melihat OOS menjadi:

- entry pada Close bar sinyal;
- entry pada harga yang dianggap lebih menguntungkan;
- entry setelah gap menghilang;
- entry pada harga rata-rata intrabar;
- entry setelah harga bergerak sesuai arah.

Perubahan entry dapat mengubah seluruh hasil MAE, MFE, return, durasi, dan outcome. Karena itu, entry definition merupakan bagian penting dari identitas kandidat.

### 19.1.3. Mengunci Aturan B0

B0 adalah pembanding yang digunakan untuk menilai apakah kandidat B1 benar-benar memiliki informasi tambahan.

Aturan B0 harus dibekukan, termasuk:

- instrumen pembanding;
- slot waktu;
- populasi event yang boleh digunakan;
- aturan declustering;
- pemilihan hari valid terdekat;
- aturan tie-break;
- pembagian IS dan OOS;
- larangan penggunaan ulang;
- aturan bahwa pemilihan B0 tidak boleh berdasarkan outcome.

Jika aturan B0 diubah setelah hasil OOS terlihat, perbandingan B1 dan B0 tidak lagi menggunakan dasar yang sama. Hasilnya dapat terlihat lebih baik hanya karena pembanding telah disesuaikan.

B1 yang sama dapat menghasilkan kesimpulan berbeda apabila B0 berubah. Oleh sebab itu, B0 bukan sekadar daftar event pembanding, melainkan bagian dari definisi eksperimen.

### 19.1.4. Mengunci Definisi MAE dan MFE

MAE dan MFE mengukur seberapa jauh harga bergerak melawan atau mendukung posisi setelah entry.

Definisi yang harus dikunci mencakup:

- harga entry yang digunakan;
- kapan pengukuran dimulai;
- horizon pengukuran;
- penggunaan High dan Low;
- arah posisi;
- perlakuan terhadap gap;
- aturan ketika horizon tidak mencukupi;
- status validitas hasil.

Contohnya, jika MAE untuk posisi long didefinisikan berdasarkan Low setelah entry, definisi itu tidak boleh diubah setelah OOS menjadi pengukuran berdasarkan harga penutupan hanya karena hasilnya terlihat lebih baik.

Perubahan kecil pada definisi MAE atau MFE dapat mengubah distribusi risiko dan peluang keuntungan. Karena itu, MAE/MFE harus diperlakukan sebagai bagian dari kontrak penelitian.

### 19.1.5. Mengunci Definisi ATR

ATR digunakan sebagai satuan volatilitas untuk menormalisasi jarak, misalnya:

- Stop Loss = 1 × ATR;
- Take Profit = 2 × ATR;
- MAE = -0,7 × ATR;
- MFE = +1,8 × ATR.

Definisi ATR yang perlu dibekukan meliputi:

- metode perhitungan, misalnya Wilder's ATR;
- periode ATR;
- sumber data;
- waktu pengambilan ATR;
- aturan penggunaan ATR_entry;
- apakah ATR tetap sepanjang evaluasi;
- aturan penanganan ATR yang tidak tersedia.

ATR harus dihitung menggunakan informasi yang tersedia sebelum entry. Dalam konteks event yang terdeteksi pada bar T dan entry pada bar berikutnya, ATR_entry dapat ditetapkan berdasarkan informasi sampai penutupan bar T.

Mengubah periode ATR atau waktu pengambilannya setelah melihat OOS dapat mengubah skala SL, TP, MAE, dan MFE. Kandidat baru tersebut tidak lagi identik dengan kandidat yang sebelumnya dipilih.

### 19.1.6. Mengunci Evaluation Engine

Evaluation Engine adalah wasit yang menentukan bagaimana setiap event dinilai.

Versi Evaluation Engine harus dibekukan, termasuk aturan:

- kapan evaluasi dimulai;
- bagaimana TP_HIT ditentukan;
- bagaimana SL_HIT ditentukan;
- bagaimana TIMEOUT ditentukan;
- bagaimana gap-through diperlakukan;
- bagaimana kondisi Open melewati level SL atau TP ditangani;
- bagaimana same-bar SL dan TP ditangani;
- bagaimana AMBIGUOUS_INTRABAR dilaporkan;
- bagaimana INSUFFICIENT_HORIZON dibedakan dari TIMEOUT;
- bagaimana harga keluar ditentukan;
- bagaimana biaya transaksi dicatat.

Misalnya, jika pada satu bar harga menyentuh SL dan TP sekaligus, TEKB tidak boleh mengubah aturan setelah melihat hasil OOS agar event tersebut dianggap TP_HIT. Jika urutan intrabar tidak diketahui, status AMBIGUOUS_INTRABAR harus tetap diperlakukan sesuai aturan yang telah ditetapkan.

Evaluation Engine harus menjalankan aturan yang sama untuk B1 dan B0. Tanpa pembekuan, evaluasi dapat berubah menjadi proses mencari interpretasi yang paling menguntungkan.

### 19.1.7. Mengunci Grid dan Kriteria Seleksi

Grid kandidat adalah ruang hipotesis yang telah ditentukan sebelum proses seleksi. Grid dapat berisi kombinasi:

- beberapa nilai Stop Loss;
- beberapa nilai Take Profit;
- beberapa nilai Maximum Hold.

Contohnya:

| Komponen | Nilai kandidat |
|---|---|
| Stop Loss | 0,5; 1; 1,5; 2 × ATR |
| Take Profit | 1; 1,5; 2; 3 × ATR |
| Maximum Hold | 3; 5; 10 bar |

Setelah kandidat dipilih, grid dan kriteria seleksi harus tetap tercatat. Kriteria tersebut dapat mencakup:

- B1 Worst harus lebih baik daripada B0 Worst;
- B1 Best harus lebih baik daripada B0 Best;
- perbedaan harus positif;
- hasil memenuhi kriteria signifikansi;
- koreksi multiple testing telah dilakukan;
- jumlah event dan pasangan memenuhi batas minimum;
- tidak terdapat pelanggaran validitas data.

Kriteria seleksi tidak boleh diganti setelah hasil OOS dilihat. Misalnya, kandidat yang tidak lolos kriteria awal tidak boleh dinyatakan lolos hanya karena ambang signifikansi diturunkan setelah melihat hasil baru.

---

## 19.2. Mengapa OOS Tidak Boleh Digunakan untuk Memilih Ulang?

### 19.2.1. Fungsi OOS

OOS digunakan untuk menjawab pertanyaan:

> Apakah kandidat yang dipilih berdasarkan data IS masih menunjukkan perilaku yang masuk akal ketika diterapkan pada data yang tidak digunakan untuk memilihnya?

Pertanyaan ini hanya dapat dijawab jika kandidat telah ditentukan sebelum OOS diperiksa.

OOS berfungsi sebagai pemeriksaan terhadap generalisasi. Artinya, OOS menguji apakah pola yang ditemukan pada data IS memiliki kemungkinan untuk bertahan di lingkungan data lain yang belum digunakan dalam proses pemilihan.

OOS bukan tempat untuk mencari kombinasi yang paling bagus. OOS adalah tempat untuk menguji kandidat yang sudah dipilih.

### 19.2.2. Apa yang Terjadi Jika OOS Digunakan untuk Tuning?

**Tuning** berarti menyesuaikan aturan atau parameter berdasarkan hasil pengujian.

Misalnya, peneliti menguji kandidat berikut pada OOS:

> SL 1 × ATR, TP 2 × ATR, hold 5 bar.

Hasil OOS ternyata kurang baik. Kemudian peneliti mencoba:

> SL 0,5 × ATR, TP 1,5 × ATR, hold 3 bar.

Hasilnya lebih baik. Peneliti lalu memilih kandidat kedua dan menyebut hasil tersebut sebagai hasil OOS.

Masalahnya, kandidat kedua telah dipilih menggunakan informasi OOS. Dengan demikian, data OOS tidak lagi benar-benar menjadi data yang belum digunakan untuk memilih kandidat. OOS telah berubah fungsi menjadi IS tambahan.

Proses tersebut dapat diulang:

1. Kandidat diuji pada OOS.
2. Hasil dilihat.
3. Aturan diubah.
4. Kandidat baru diuji.
5. Hasil terbaik dipilih.
6. Hasil terbaik disebut sebagai validasi OOS.

Jika proses ini dilakukan berulang kali, peneliti pada akhirnya dapat menyesuaikan kandidat terhadap karakteristik OOS. Kandidat mungkin terlihat berhasil bukan karena benar-benar general, melainkan karena telah diberi kesempatan untuk menyesuaikan diri dengan data tersebut.

### 19.2.3. OOS yang Sudah Dilihat Tidak Lagi Murni

Data OOS tidak menjadi "murni" hanya karena sebelumnya diberi label OOS.

Status OOS ditentukan oleh bagaimana data tersebut digunakan.

Jika data belum digunakan untuk memilih, mengubah, atau menyetel kandidat, data tersebut dapat berfungsi sebagai OOS.

Namun, jika hasilnya telah dilihat lalu digunakan untuk:

- memilih kandidat;
- mengubah parameter;
- mengubah definisi entry;
- mengubah aturan B0;
- mengubah Evaluation Engine;
- memperluas atau mempersempit grid;
- menghapus event yang tidak disukai;
- mengganti kriteria seleksi;

maka data tersebut telah ikut masuk ke dalam proses discovery atau selection.

Dalam keadaan itu, OOS lama harus dianggap **spent**, atau telah digunakan. Jika aturan kemudian diubah, status OOS tersebut dapat menjadi **tainted**, yaitu tercemar oleh penggunaan sebelumnya.

### 19.2.4. Mengapa OOS Harus Diperlakukan sebagai Ujian Satu Kali?

OOS idealnya diperlakukan seperti ujian yang jawabannya belum boleh dilihat sebelum peserta menyelesaikan persiapan.

Jika seseorang melihat soal ujian, mencoba jawaban, mengetahui mana yang salah, lalu belajar khusus dari jawaban tersebut sebelum ujian dinilai, ujian itu tidak lagi mengukur kemampuan yang sama.

Demikian pula dengan OOS. Jika hasil OOS digunakan untuk memilih ulang kandidat, pengujian tersebut tidak lagi mengukur generalisasi dari proses IS. Ia mengukur kemampuan peneliti menyesuaikan aturan terhadap data yang telah dilihat.

Karena itu, prosedur yang lebih jujur adalah:

1. Gunakan data IS untuk membangun dan memilih kandidat.
2. Bekukan kandidat dan seluruh aturan penelitian.
3. Simpan manifest freeze dan fingerprint versi.
4. Jalankan kandidat yang telah dibekukan pada OOS.
5. Catat hasil OOS tanpa mengubah kandidat.
6. Beri status OOS_VALIDATED atau OOS_REJECTED sesuai kriteria.
7. Jika ingin mengembangkan kandidat baru, mulai penelitian baru dengan versi, batch, dan provenance baru.

### 19.2.5. Bagaimana Jika Hasil OOS Buruk?

Hasil OOS yang buruk bukan alasan untuk mengubah kandidat secara diam-diam.

Jika kandidat gagal pada OOS, beberapa kesimpulan yang mungkin adalah:

- kandidat tidak menunjukkan generalisasi;
- edge yang terlihat pada IS mungkin terlalu spesifik;
- sampel IS mungkin terlalu beruntung;
- kondisi pasar berubah;
- biaya atau friksi menghilangkan manfaat;
- definisi atau asumsi penelitian perlu ditinjau dalam studi baru.

Peneliti boleh melakukan penelitian lanjutan. Namun, penelitian lanjutan harus diperlakukan sebagai eksperimen baru, bukan sebagai "perbaikan kecil" yang tetap memakai label OOS lama.

Dengan demikian, kegagalan OOS tetap memiliki nilai. Ia memberi informasi bahwa kandidat tertentu belum memiliki bukti generalisasi yang memadai.

---

## 19.3. Apa Saja yang Harus Dicatat Sebelum Freeze?

Freeze tidak cukup hanya dengan menulis kalimat "kandidat telah dibekukan". Pembekuan harus meninggalkan catatan yang dapat diperiksa kembali.

Catatan tersebut dapat disebut sebagai **freeze manifest**.

Freeze manifest berfungsi sebagai foto keadaan penelitian pada saat kandidat dikunci. Isinya harus memungkinkan orang lain, termasuk peneliti sendiri di masa depan, mengetahui dengan tepat apa yang akan diuji pada OOS.

### 19.3.1. Candidate Grid Version

`candidate_grid_version_id` mengidentifikasi versi grid kandidat yang digunakan dalam penelitian.

Catatan ini menjelaskan:

- nilai SL yang diuji;
- nilai TP yang diuji;
- nilai Maximum Hold yang diuji;
- satuan yang digunakan, misalnya ×ATR;
- batas grid;
- aturan pembentukan kombinasi;
- apakah grid ditentukan sebelum seleksi;
- versi konfigurasi grid.

Contoh:
candidate_grid_version_id:
GRID_SLTP_HOLD_V1_2026

Nama tersebut hanya contoh. Yang penting bukan bentuk namanya, melainkan kemampuan untuk menghubungkan kandidat terpilih dengan grid asalnya.

### 19.3.2. Entry Definition Version

`entry_definition_version_id` mengidentifikasi aturan entry yang digunakan.

Catatan ini dapat memuat:

- event confirmation timestamp;
- entry timestamp;
- jenis entry;
- harga entry;
- aturan NEXT_VALID_BAR_OPEN;
- aturan bar valid berikutnya;
- perlakuan terhadap gap;
- aturan event yang included_in_research;
- perbedaan antara raw entry dan actionable live.

Contoh:
entry_definition_version_id:
ENTRY_NEXT_VALID_OPEN_V1

Dengan identitas ini, hasil OOS dapat diketahui berasal dari definisi entry yang mana.

### 19.3.3. B0 Selection Rule Version

`b0_selection_rule_version` mencatat versi aturan pemilihan pembanding.

Catatan ini mencakup:

- instrumen yang sama;
- slot waktu yang sama;
- aturan populasi;
- radius decluster;
- nearest valid trading day;
- tie-break;
- larangan penggunaan ulang;
- aturan partisi IS/OOS;
- perlakuan terhadap NO_MATCH_FOUND;
- larangan matching berdasarkan outcome.

Contoh:
b0_selection_rule_version:
B0_MATCH_SAME_INSTRUMENT_SLOT_V1

Tanpa versi B0 yang jelas, hasil perbandingan antara B1 dan B0 sulit ditafsirkan secara konsisten.

### 19.3.4. MAE/MFE Definition Version

`mae_mfe_definition_version_id` mencatat cara pengukuran gerakan harga setelah entry.

Informasi yang perlu disimpan meliputi:

- arah posisi;
- harga entry;
- horizon R1, R3, R5, R10, atau horizon lain;
- penggunaan High dan Low;
- definisi MAE;
- definisi MFE;
- aturan gap;
- status COMPUTED_FULL_HORIZON;
- status INSUFFICIENT_HORIZON;
- status INVALIDATED.

Contoh:
mae_mfe_definition_version_id:
MAE_MFE_LONG_INTRABAR_HORIZON_V1

Versi ini memastikan bahwa angka MAE dan MFE pada OOS dihitung dengan definisi yang sama seperti pada IS.

### 19.3.5. ATR Definition Version

`atr_definition_version_id` mencatat definisi ATR yang digunakan.

Informasi yang perlu dicatat antara lain:

- metode ATR;
- periode ATR;
- sumber data;
- waktu pengambilan ATR;
- definisi ATR_entry;
- aturan ATR tetap sepanjang evaluasi;
- aturan ketika ATR tidak tersedia.

Contoh:
atr_definition_version_id:
ATR_WILDER_14_ENTRY_CLOSE_T_V1

Jika ATR berubah, maka jarak berbasis ×ATR dapat berubah. Oleh karena itu, perubahan definisi ATR harus menghasilkan versi baru.

### 19.3.6. Evaluation Engine Version

`evaluation_engine_version_id` mengidentifikasi aturan yang digunakan untuk menentukan outcome.

Catatan ini mencakup:

- aturan mulai evaluasi;
- aturan TP_HIT;
- aturan SL_HIT;
- aturan TIMEOUT;
- gap-through;
- same-bar SL/TP;
- AMBIGUOUS_INTRABAR;
- worst-case dan best-case;
- INSUFFICIENT_HORIZON;
- harga exit;
- perlakuan biaya transaksi.

Contoh:
evaluation_engine_version_id:
EVAL_GAP_SAMEBAR_AMBIGUITY_V1

Jika Evaluation Engine berubah, hasil lama tidak boleh dianggap otomatis sebanding dengan hasil baru.

### 19.3.7. Multiple-Testing Family

Penelitian yang menguji banyak kandidat harus mencatat keluarga pengujian atau `multiple_testing_family_id`.

Hal ini penting karena koreksi multiple testing, seperti BH-FDR, bergantung pada kelompok pengujian yang dianggap sebagai satu keluarga.

Dalam TEKB, keluarga pengujian worst-case dan best-case diperlakukan terpisah sesuai protokol penelitian.

Catatan ini harus menjelaskan:

- keluarga pengujian;
- kandidat yang termasuk;
- statistik yang diuji;
- p-value yang digunakan;
- metode koreksi;
- tingkat q;
- hubungan dengan batch penelitian.

Contoh:
multiple_testing_family_id:
FAMILY_WORST_CASE_BATCH_2026_01
FAMILY_BEST_CASE_BATCH_2026_01

Keluarga pengujian tidak boleh diubah hanya untuk membuat kandidat tertentu terlihat lolos.

### 19.3.8. Research Batch

`research_batch_id` mengidentifikasi satu rangkaian penelitian yang dilakukan dengan protokol tertentu.

Research batch dapat mencatat:

- tanggal dan waktu penelitian;
- data yang digunakan;
- periode IS;
- universe instrumen;
- versi pipeline;
- versi data;
- versi grid;
- versi engine;
- jumlah kandidat;
- jumlah percobaan;
- status penelitian.

Contoh:
research_batch_id:
TEKB_IS_BATCH_2026_09_01

Research batch membantu membedakan penelitian pertama dari percobaan berikutnya.

### 19.3.9. Hypothesis ID

`hypothesis_id` mengidentifikasi pertanyaan atau hipotesis yang diuji.

Contohnya:
hypothesis_id:
HYP_SAMSON_HIGH_RV_NEXT_BAR_LONG_EDGE_V1

Hypothesis ID sebaiknya mengarah pada pertanyaan penelitian, bukan hanya nama strategi.

Misalnya:

> Apakah event dengan relative volume yang sangat tinggi memiliki distribusi hasil long pada bar berikutnya yang berbeda dan lebih baik daripada B0 yang sebanding?

Dengan begitu, kandidat tidak terlepas dari pertanyaan ilmiah yang melahirkannya.

### 19.3.10. Freeze Fingerprint atau Hash

Selain menyimpan nama versi, sistem dapat menyimpan **fingerprint** atau **hash** dari konfigurasi penelitian.

Fingerprint merupakan jejak digital yang mewakili isi konfigurasi pada saat freeze.

Jika isi konfigurasi berubah, fingerprint seharusnya berubah pula.

Fingerprint dapat mencakup:

- entry definition;
- B0 rule;
- MAE/MFE definition;
- ATR definition;
- Evaluation Engine;
- candidate grid;
- selection criteria;
- multiple-testing family;
- research batch;
- hypothesis ID.

Tujuannya bukan membuat sistem terlihat rumit, melainkan memastikan bahwa konfigurasi yang diuji pada OOS benar-benar sama dengan konfigurasi yang dipilih pada IS.

### 19.3.11. Contoh Freeze Manifest

Contoh sederhana freeze manifest dapat terlihat seperti berikut:
freeze_status: FROZEN

hypothesis_id:
HYP_SAMSON_HIGH_RV_NEXT_BAR_LONG_EDGE_V1

research_batch_id:
TEKB_IS_BATCH_2026_09_01

candidate_grid_version_id:
GRID_SLTP_HOLD_V1_2026

entry_definition_version_id:
ENTRY_NEXT_VALID_OPEN_V1

b0_selection_rule_version:
B0_MATCH_SAME_INSTRUMENT_SLOT_V1

mae_mfe_definition_version_id:
MAE_MFE_LONG_INTRABAR_HORIZON_V1

atr_definition_version_id:
ATR_WILDER_14_ENTRY_CLOSE_T_V1

evaluation_engine_version_id:
EVAL_GAP_SAMEBAR_AMBIGUITY_V1

multiple_testing_family_id:
FAMILY_WORST_BEST_BATCH_2026_01

selected_candidate:
SL = 1.0 ATR
TP = 2.0 ATR
MAX_HOLD = 5 bars

freeze_timestamp:
2026-09-12T00:00:00Z

freeze_fingerprint:
<hash konfigurasi>

Contoh tersebut bukan format wajib tunggal. Format dapat disesuaikan dengan sistem TEKB. Prinsip utamanya adalah seluruh informasi penting harus tersedia, konsisten, dan tidak mudah diubah tanpa meninggalkan jejak.

---

## 19.4. Apa yang Terjadi Jika Aturan Berubah?

Dalam penelitian nyata, perubahan aturan kadang diperlukan. Peneliti mungkin menemukan kesalahan implementasi, definisi yang ambigu, data yang tidak valid, atau kebutuhan untuk merumuskan hipotesis baru.

Masalahnya bukan bahwa perubahan selalu dilarang. Masalahnya adalah perubahan tidak boleh disamarkan sebagai kandidat lama yang sama.

### 19.4.1. Perubahan Aturan Menghasilkan Versi Baru

Jika suatu aturan berubah secara substantif, maka aturan tersebut harus memiliki versi baru.

Misalnya:

- `ENTRY_NEXT_VALID_OPEN_V1` diubah menjadi `ENTRY_NEXT_VALID_OPEN_V2`;
- `ATR_WILDER_14_ENTRY_CLOSE_T_V1` diubah menjadi versi baru;
- `EVAL_ENGINE_V1` diubah karena aturan same-bar diperjelas;
- `B0_RULE_V1` diubah karena definisi populasi diperbaiki.

Perubahan versi membuat sejarah penelitian tetap jelas. Orang dapat mengetahui mana hasil yang berasal dari aturan lama dan mana hasil yang berasal dari aturan baru.

### 19.4.2. Perubahan Kecil Dapat Mengubah Makna Hasil

Perubahan yang tampak kecil dapat menghasilkan perubahan besar pada hasil penelitian.

Contohnya:

- Entry dari Close T menjadi Open T+1.
- ATR dihitung pada T−1, bukan pada T.
- Gap-through dianggap exit pada Open, bukan pada level SL/TP.
- Same-bar SL dan TP dipaksa menjadi TP lebih dahulu.
- B0 boleh digunakan ulang, padahal sebelumnya tidak.
- Event yang berdekatan tidak lagi dikelompokkan.
- Event tanpa horizon lengkap tetap dimasukkan ke distribusi.
- Biaya transaksi tidak lagi dihitung.
- Candidate grid diperluas setelah melihat OOS.

Masing-masing perubahan dapat memengaruhi jumlah event, harga entry, MAE, MFE, outcome, distribusi, p-value, dan kandidat yang lolos.

Oleh sebab itu, "hanya mengubah sedikit" bukan alasan untuk menganggap hasilnya tetap sama.

### 19.4.3. Kandidat Lama dan Kandidat Baru Tidak Identik

Misalnya, kandidat lama adalah:
H1:
Entry = Open bar valid berikutnya
SL = 1 ATR
TP = 2 ATR
Max Hold = 5 bar

Kemudian aturan entry diubah menjadi:
H2:
Entry = Close bar sinyal
SL = 1 ATR
TP = 2 ATR
Max Hold = 5 bar

Walaupun SL, TP, dan Maximum Hold sama, H2 bukan H1. Harga entry, waktu paparan risiko, MAE, MFE, dan outcome dapat berbeda.

Demikian pula, jika hanya aturan B0 yang berubah, hasil Δ antara B1 dan B0 dapat berubah. Karena itu, kandidat harus dikenali melalui seluruh definisi eksperimen, bukan hanya tiga angka SL, TP, dan Maximum Hold.

### 19.4.4. Apa yang Harus Dilakukan Setelah Perubahan?

Jika perubahan dilakukan sebelum OOS dan kandidat belum diuji pada OOS, prosedurnya dapat berupa:

1. Tandai versi lama sebagai superseded atau digantikan.
2. Buat versi aturan baru.
3. Buat hypothesis ID atau candidate version baru bila substansinya berubah.
4. Jalankan kembali proses IS sesuai protokol.
5. Lakukan seleksi ulang jika diperlukan.
6. Buat freeze manifest baru.
7. Gunakan OOS yang belum tercemar untuk validasi.

Jika perubahan dilakukan setelah OOS telah dilihat, maka hasil OOS lama tidak boleh digunakan sebagai OOS murni untuk kandidat baru. Kandidat baru memerlukan proses validasi yang sesuai, dan OOS lama harus ditandai sebagai spent atau tainted terhadap proses tersebut.

### 19.4.5. Bug Fix dan Perubahan Metodologi

Perlu dibedakan antara:

- **Bug fix**, yaitu memperbaiki kesalahan implementasi yang membuat sistem tidak menjalankan aturan yang sebenarnya telah ditetapkan.
- **Perubahan metodologi**, yaitu mengubah definisi, asumsi, aturan, atau cara evaluasi penelitian.

Bug fix tetap harus didokumentasikan. Hasil sebelum perbaikan mungkin harus dianggap tidak valid atau perlu dihitung ulang.

Perubahan metodologi harus diperlakukan sebagai versi baru karena dapat mengubah pertanyaan atau makna hasil.

Contohnya, jika kontrak penelitian sejak awal menyatakan entry pada Open bar berikutnya, tetapi kode secara tidak sengaja menggunakan Close bar sinyal, memperbaiki kode tersebut adalah bug fix. Namun, jika peneliti memutuskan bahwa Close bar sinyal lebih sesuai setelah melihat hasil, itu adalah perubahan metodologi dan tidak boleh disebut sekadar perbaikan teknis.

---

## 19.5. Hubungan Freeze dengan OOS

Freeze dan OOS merupakan dua tahap yang saling melengkapi.

Freeze memastikan bahwa kandidat tidak berubah setelah proses seleksi. OOS kemudian menguji kandidat tersebut pada data yang belum digunakan untuk memilihnya.

Urutannya adalah:
Data historis
↓
IS Research
↓
IS Selection
↓
Freeze
↓
OOS Evaluation
↓
OOS_VALIDATED / OOS_REJECTED

Setiap tahap memiliki fungsi berbeda:

| Tahap | Pertanyaan utama |
|---|---|
| IS Research | Hipotesis dan kandidat apa yang mungkin memiliki informasi? |
| IS Selection | Kandidat mana yang memenuhi aturan bukti? |
| Freeze | Apa tepatnya yang akan diuji? |
| OOS Evaluation | Apakah kandidat yang telah dikunci bertahan pada data baru? |
| OOS Decision | Apakah bukti generalisasi cukup atau belum? |

Tanpa freeze, OOS dapat berubah menjadi ruang tuning. Tanpa OOS, hasil IS mudah disalahartikan sebagai bukti bahwa kandidat akan bekerja di luar sampel.

Freeze tidak membuktikan kandidat benar. OOS juga tidak menjamin keuntungan masa depan. Keduanya hanya membantu menjaga agar kesimpulan penelitian tidak lebih besar daripada bukti yang tersedia.

---

## 19.6. Status Freeze dan Validitas Penelitian

Untuk menjaga keterlacakan, TEKB dapat menggunakan status seperti berikut:

| Status | Arti |
|---|---|
| UNFROZEN | Kandidat atau aturan masih dapat berubah dalam tahap IS |
| FROZEN | Kandidat dan seluruh definisi penting telah dikunci |
| FREEZE_FAILED | Pembekuan gagal karena ada informasi atau konfigurasi penting yang belum lengkap |
| OOS_PENDING | Kandidat telah dibekukan dan menunggu evaluasi OOS |
| OOS_VALIDATED | Kandidat memenuhi kriteria validasi OOS |
| OOS_REJECTED | Kandidat tidak memenuhi kriteria validasi OOS |
| OOS_SPENT | Data OOS telah digunakan untuk proses seleksi atau tuning |
| OOS_TAINTED | Hasil OOS telah tercemar oleh perubahan atau penggunaan setelah hasil dilihat |

Status tersebut membantu mencegah penggunaan data secara tidak konsisten. Misalnya, kandidat dengan status OOS_SPENT tidak boleh dipresentasikan seolah-olah baru pertama kali diuji pada data yang tidak tersentuh.

---

## 19.7. Freeze Bukan Akhir dari Sikap Kritis

Freeze sangat penting, tetapi bukan solusi untuk semua masalah penelitian.

Freeze tidak menghapus:

- overfitting yang sudah terjadi di IS;
- data snooping sebelum freeze;
- terlalu banyak percobaan;
- bias survivorship;
- kualitas data yang buruk;
- kesalahan dalam hipotesis;
- perubahan rezim pasar;
- biaya transaksi;
- keterbatasan jumlah event;
- ketergantungan antar-event;
- kelemahan definisi B0.

Freeze hanya memastikan bahwa setelah kandidat dipilih, tahap validasi tidak terus-menerus diarahkan oleh hasil OOS.

Karena itu, freeze harus dipahami sebagai mekanisme pengendalian bias, bukan sebagai bukti bahwa kandidat telah menjadi benar.

---

## Ringkasan Bab

- Freeze berarti mengunci kandidat dan seluruh aturan penting sebelum hasil OOS digunakan.
- Yang dibekukan bukan hanya SL, TP, dan Maximum Hold, tetapi juga definisi entry, B0, MAE/MFE, ATR, Evaluation Engine, grid, kriteria seleksi, dan provenance.
- OOS digunakan untuk menguji generalisasi, bukan untuk memilih ulang atau menyetel kandidat.
- Jika hasil OOS digunakan untuk mengubah aturan, OOS tersebut tidak lagi murni dan harus dianggap spent atau tainted.
- Setiap perubahan aturan harus menghasilkan versi baru dan meninggalkan jejak audit.
- Freeze manifest dan fingerprint membantu memastikan konfigurasi OOS sama dengan konfigurasi yang dipilih pada IS.
- Freeze tidak menjamin kandidat benar, tetapi menjaga agar validasi dilakukan secara lebih jujur.

---

## Pertanyaan Refleksi

1. Mengapa kandidat tidak boleh diubah setelah hasil OOS dilihat?
2. Apa perbedaan antara memperbaiki bug dan mengubah metodologi?
3. Mengapa perubahan entry dapat mengubah makna hasil penelitian?
4. Mengapa aturan B0 harus dibekukan bersama kandidat B1?
5. Apa fungsi freeze manifest?
6. Apa yang dimaksud dengan OOS spent atau tainted?
7. Mengapa freeze tidak menghapus overfitting yang sudah terjadi pada IS?
8. Jika tidak ada kandidat yang lolos OOS, mengapa hasil tersebut tetap bernilai bagi penelitian?

---

## Kalimat Kunci

> Freeze bukan berarti kandidat telah terbukti benar. Freeze berarti kandidat telah dikunci agar OOS dapat menguji generalisasi secara jujur. Jika aturan diubah setelah OOS dilihat, maka data tersebut tidak lagi berfungsi sebagai ujian yang belum digunakan, melainkan telah menjadi bagian dari proses pemilihan.

---

<div align="center">

[← Bab Sebelumnya](/posts/bab-18-is-selection/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Bab Selanjutnya →](/posts/bab-20-oos-data-baru/)

</div>