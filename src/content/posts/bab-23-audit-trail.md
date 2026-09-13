---
title: "BAB 23 — Audit Trail: Mengapa Setiap Kesimpulan Harus Dapat Ditelusuri?"
published: 2026-09-12
description: "Audit trail memastikan setiap kesimpulan TEKB dapat ditelusuri dari data mentah sampai keputusan akhir. Bab ini menjelaskan identitas, versi, dan reproduksibilitas penelitian."
tags: ["bab-23", "audit-trail", "reproduksibilitas", "versi"]
category: "Bab"
draft: false
lang: ""
---

**BAGIAN VII — MEMBACA, MENELUSURI, DAN MENGGUNAKAN HASIL TEKB**

---

## Tujuan Bab

Dalam penelitian berbasis data, sebuah kesimpulan tidak cukup hanya terlihat masuk akal. Kesimpulan tersebut harus dapat ditelusuri kembali: berasal dari data apa, menggunakan aturan yang mana, diproses melalui versi mesin yang mana, dan dihasilkan melalui tahapan apa.

Inilah fungsi **audit trail**.

Audit trail adalah rekaman keterlacakan penelitian dari data mentah sampai keputusan akhir. Dengan audit trail, peneliti tidak hanya dapat mengatakan:

> "Hasil penelitian menunjukkan bahwa kandidat ini memiliki edge."

Peneliti juga harus dapat menjawab:

- Data apa yang digunakan?
- Kapan data diambil?
- Aturan event yang digunakan versi berapa?
- Bagaimana entry ditentukan?
- Bagaimana B0 dipilih?
- Bagaimana MAE dan MFE dihitung?
- Bagaimana SL/TP dievaluasi?
- Berapa banyak event yang dikeluarkan?
- Apakah ada percobaan sebelumnya?
- Apakah hasil ini berasal dari IS atau OOS?
- Apakah aturan sudah dibekukan?
- Apakah hasil dapat diulang?

Prinsip utama bab ini adalah:

> Kesimpulan yang dapat dipercaya bukan hanya kesimpulan yang memiliki angka, tetapi kesimpulan yang memiliki jejak asal-usul yang jelas.

---

## 23.1. Apa Itu Audit Trail?

### 23.1.1. Definisi Audit Trail

**Audit trail** adalah rangkaian catatan yang memungkinkan seseorang menelusuri perjalanan sebuah hasil penelitian dari awal hingga akhir.

Dalam konteks TEKB, alurnya dapat digambarkan sebagai berikut:

Data mentah
↓
Data yang telah diperiksa
↓
Aturan penelitian
↓
Event terdeteksi
↓
Entry ditentukan
↓
B0 dipilih
↓
MAE/MFE dihitung
↓
Candidate SL/TP dievaluasi
↓
Hasil B1 dan B0 dibandingkan
↓
Bootstrap dan multiple-testing
↓
Seleksi IS
↓
Freeze
↓
Validasi OOS
↓
Kesimpulan

Setiap tahap harus memiliki hubungan yang dapat diperiksa dengan tahap sebelumnya dan sesudahnya.

Jika sebuah angka hasil tidak dapat ditelusuri kembali ke event yang membentuknya, angka tersebut sulit diaudit. Jika sebuah event tidak dapat ditelusuri kembali ke data dan aturan yang mendeteksinya, event tersebut sulit dipercaya.

### 23.1.2. Audit Trail Bukan Sekadar Log Teknis

Dalam dunia perangkat lunak, log biasanya digunakan untuk mencatat:

- kapan proses dimulai;
- kapan proses selesai;
- apakah terjadi error;
- berapa lama proses berjalan;
- atau fungsi apa yang dijalankan.

Log teknis memang berguna, tetapi audit trail penelitian memiliki cakupan yang lebih luas.

Audit trail harus menjelaskan makna ilmiah dan metodologis dari proses tersebut.

Contohnya, log teknis mungkin hanya mencatat:
process_completed = true

Namun, audit trail penelitian perlu menjelaskan:

- data yang digunakan;
- periode data;
- populasi instrumen;
- definisi event;
- aturan entry;
- aturan B0;
- versi MAE/MFE;
- versi ATR;
- versi Evaluation Engine;
- kandidat yang diuji;
- hasil yang diperoleh;
- alasan event dikeluarkan;
- serta status keputusan akhir.

Dengan demikian, audit trail bukan hanya menjawab:

> "Apakah program berjalan?"

Audit trail juga menjawab:

> "Apa yang sebenarnya dilakukan program, berdasarkan aturan apa, dan mengapa hasilnya boleh ditafsirkan seperti itu?"

### 23.1.3. Hubungan antara Data, Aturan, Event, Hasil, dan Keputusan

Audit trail harus menghubungkan lima unsur utama:

1. **Data**
   - Data OHLCV, timestamp, instrumen, volume, harga, dan sumber data.

2. **Aturan**
   - Definisi event, entry, B0, MAE/MFE, ATR, SL/TP, evaluasi, dan kriteria seleksi.

3. **Event**
   - Kejadian spesifik yang terdeteksi dari data.

4. **Hasil**
   - Return, MAE, MFE, outcome SL/TP, distribusi, Δ B1-B0, bootstrap, dan metrik lain.

5. **Keputusan**
   - Apakah kandidat dipilih, dibekukan, divalidasi OOS, ditolak, atau diberi status NO_EDGE_FOUND.

Contoh sederhana:
Data:
ABCD, 2026-03-10, bar 5 menit

Aturan:
SAMSON v1.0, RV ≥ 5

Event:
event_id = EVT-000123

Entry:
NEXT_VALID_BAR_OPEN

B0:
B0-000123

Pengukuran:
MAE = -1,2 ATR
MFE = +2,4 ATR

Evaluasi:
TP 2 ATR, SL 1 ATR, max hold 5 bar

Agregasi:
Δ expectancy = +0,08R

Keputusan:
Lolos IS → Freeze → OOS

Jika seseorang mempertanyakan hasil tersebut, peneliti dapat menelusuri setiap tahapnya.

### 23.1.4. Audit Trail sebagai Rantai Bukti

Audit trail dapat dipahami sebagai **rantai bukti**.

Data mentah adalah titik awal. Event merupakan hasil penerapan aturan terhadap data. Hasil event merupakan hasil pengukuran. Kesimpulan merupakan hasil agregasi dan pengujian terhadap banyak event.

Jika salah satu mata rantai tidak jelas, kesimpulan menjadi sulit diperiksa.

Misalnya:

- Data tersedia, tetapi aturan event tidak dicatat.
- Event dicatat, tetapi entry tidak jelas.
- Entry jelas, tetapi B0 tidak diketahui.
- B1 dan B0 tersedia, tetapi versi Evaluation Engine tidak dicatat.
- Hasil IS positif, tetapi tidak diketahui berapa banyak kandidat yang telah dicoba.
- OOS positif, tetapi ternyata aturan telah diubah setelah melihat OOS.

Dalam semua kasus tersebut, masalahnya bukan sekadar kurang dokumentasi. Masalahnya adalah bukti tidak lagi memiliki keterlacakan yang memadai.

---

## 23.2. Identitas dan Versi yang Harus Dicatat

Agar hasil dapat ditelusuri, TEKB perlu mencatat identitas dan versi penting pada setiap penelitian.

Tidak semua sistem harus menggunakan nama bidang yang persis sama, tetapi fungsi informasinya harus tersedia.

### 23.2.1. computation_id

**computation_id** adalah identitas unik untuk satu proses komputasi atau satu hasil eksekusi.

Contohnya:
computation_id = COMP-20260912-0007

Identitas ini membantu menjawab:

- Kapan proses dijalankan?
- Proses mana yang menghasilkan tabel tertentu?
- Apakah dua laporan berasal dari eksekusi yang sama?
- Apakah hasil telah dihitung ulang?
- Apakah ada perbedaan antara hasil lama dan hasil baru?

Satu penelitian dapat memiliki beberapa computation ID jika proses dijalankan ulang. Hal ini penting karena hasil yang terlihat sama belum tentu berasal dari eksekusi yang sama.

### 23.2.2. protocol_hash

**protocol_hash** adalah sidik jari digital dari protokol atau konfigurasi penelitian yang digunakan.

Secara sederhana, hash dapat dianggap seperti "sidik jari" dari kumpulan aturan.

Jika satu bagian penting dari protokol berubah, hash idealnya ikut berubah.

Contoh:
protocol_hash = 8f4a...c91d

Hash membantu mendeteksi apakah dua hasil benar-benar menggunakan protokol yang sama atau hanya diberi nama yang sama.

Misalnya, dua penelitian sama-sama disebut "SAMSON v1.0", tetapi salah satunya menggunakan threshold RV ≥ 5 dan yang lain menggunakan RV ≥ 4,5. Jika perubahan tersebut tidak tercermin dalam identitas atau hash, hasil dapat tercampur secara tidak sengaja.

### 23.2.3. hypothesis_id

**hypothesis_id** mengidentifikasi pertanyaan atau hipotesis yang sedang diuji.

Contoh:
hypothesis_id = HYP-SAMSON-REVERSAL-001

Hipotesis harus menjelaskan apa yang ingin diketahui.

Misalnya:

> "Apakah event volume ekstrem dengan karakteristik candle tertentu memiliki distribusi return berikutnya yang berbeda dari B0?"

Dengan hypothesis ID, peneliti dapat membedakan:

- hipotesis tentang arah;
- hipotesis tentang reversal;
- hipotesis tentang continuation;
- hipotesis tentang MAE;
- hipotesis tentang MFE;
- hipotesis tentang kandidat SL/TP.

Tanpa identitas hipotesis, hasil positif dapat terlihat seolah-olah berasal dari pertanyaan awal, padahal mungkin berasal dari pertanyaan lain yang muncul setelah melihat data.

### 23.2.4. research_batch_id

**research_batch_id** mengidentifikasi satu kelompok penelitian yang dijalankan sebagai satu batch.

Contoh:
research_batch_id = BATCH-2026-09-SAMSON-01


Batch dapat mencakup:

- satu hipotesis;
- beberapa horizon;
- beberapa kandidat;
- satu populasi instrumen;
- satu periode IS;
- atau satu keluarga pengujian yang telah ditentukan.

Research batch membantu menjawab:

- Berapa banyak pengujian yang dilakukan dalam satu rangkaian?
- Kandidat ini ditemukan dalam batch yang mana?
- Apa saja alternatif yang ikut diuji?
- Apakah hasil ini bagian dari pencarian awal atau seleksi lanjutan?

Hal ini penting untuk membaca risiko data snooping dan multiple testing.

### 23.2.5. attempt_number

**attempt_number** mencatat percobaan ke berapa dalam proses penelitian.

Contoh:
attempt_number = 3

Mengapa ini penting?

Misalnya, peneliti menguji:

- threshold RV ≥ 3;
- threshold RV ≥ 4;
- threshold RV ≥ 5;
- threshold RV ≥ 6.

Jika hanya hasil percobaan keempat yang dilaporkan tanpa mencatat tiga percobaan sebelumnya, pembaca dapat mengira bahwa threshold RV ≥ 6 telah ditentukan sejak awal.

Padahal, threshold tersebut mungkin dipilih setelah melihat hasil percobaan sebelumnya.

Mencatat attempt number tidak berarti setiap percobaan pasti salah. Justru, pencatatan ini membuat proses pencarian lebih transparan.

### 23.2.6. candidate_grid_version_id

**candidate_grid_version_id** mengidentifikasi versi ruang kandidat yang diuji.

Candidate grid dapat mencakup:

- variasi stop loss;
- variasi take profit;
- max hold;
- threshold;
- horizon;
- atau kombinasi parameter yang diizinkan.

Contoh:
candidate_grid_version_id = GRID-SLTP-ATR-1.0

Misalnya, satu grid berisi:

- SL: 0,5 ATR; 1 ATR; 1,5 ATR;
- TP: 1 ATR; 1,5 ATR; 2 ATR; 3 ATR;
- max hold: 3; 5; 10 bar.

Jika grid berubah, hasil penelitian tidak boleh dianggap berasal dari ruang kandidat yang sama.

### 23.2.7. entry_definition_version_id

Identitas ini mencatat versi aturan entry yang digunakan.

Contoh:

Misalnya, satu grid berisi:

- SL: 0,5 ATR; 1 ATR; 1,5 ATR;
- TP: 1 ATR; 1,5 ATR; 2 ATR; 3 ATR;
- max hold: 3; 5; 10 bar.

Jika grid berubah, hasil penelitian tidak boleh dianggap berasal dari ruang kandidat yang sama.

### 23.2.7. entry_definition_version_id

Identitas ini mencatat versi aturan entry yang digunakan.

Contoh:
entry_definition_version_id = ENTRY-NEXT-VALID-OPEN-1.0

Aturan entry sangat penting karena perubahan kecil dapat mengubah seluruh hasil.

Contohnya:

- entry pada signal close;
- entry pada next bar open;
- entry pada next valid bar open;
- entry pada harga limit;
- entry setelah konfirmasi;
- atau entry setelah gap tertentu.

Jika satu laporan menggunakan close signal dan laporan lain menggunakan open bar berikutnya, hasil keduanya tidak boleh langsung dibandingkan tanpa penjelasan.

### 23.2.8. b0_selection_rule_version

Identitas ini mencatat versi aturan pemilihan B0.

Contoh:
b0_selection_rule_version = B0-PAIRED-SESSION-DECLUSTER-1.0

Aturan B0 dapat menentukan:

- instrumen yang sama;
- slot waktu yang sama;
- periode yang sama;
- nearest valid trading day;
- tie-break jika terdapat beberapa kandidat;
- radius decluster;
- larangan reuse;
- dan larangan memilih berdasarkan outcome.

Perubahan pada aturan B0 dapat mengubah pembanding dan akhirnya mengubah nilai Δ B1-B0.

Karena itu, B0 bukan sekadar label. B0 adalah bagian dari definisi penelitian yang harus diberi versi.

### 23.2.9. mae_mfe_definition_version_id

Identitas ini mencatat bagaimana MAE dan MFE dihitung.

Contohnya:
mae_mfe_definition_version_id = MAE-MFE-LONG-INTRABAR-1.0

Hal yang perlu dikunci antara lain:

- posisi long atau short;
- harga entry;
- kapan pengukuran dimulai;
- horizon R1/R3/R5/R10;
- penggunaan High dan Low;
- perlakuan gap;
- status horizon tidak lengkap;
- dan aturan invalidasi.

Perubahan definisi MAE/MFE dapat membuat angka lama tidak sebanding dengan angka baru.

### 23.2.10. atr_definition_version_id

Identitas ini mencatat definisi ATR.

Contoh:
atr_definition_version_id = ATR-WILDER-N14-ENTRY-CLOSE-1.0

Informasi yang perlu diketahui:

- metode ATR;
- periode ATR;
- waktu ATR dihitung;
- apakah ATR menggunakan data sebelum entry;
- apakah ATR tetap sepanjang trade;
- dan bagaimana missing data diperlakukan.

Misalnya, ATR yang dihitung setelah entry dapat mengandung informasi yang belum tersedia saat keputusan dibuat. Karena itu, versi ATR harus mencerminkan aturan no-look-ahead.

### 23.2.11. evaluation_engine_version_id

Identitas ini mencatat versi mesin evaluasi outcome.

Contoh:
evaluation_engine_version_id = EVAL-GAP-SAMEBAR-WORSTBEST-1.0

Evaluation Engine menentukan:

- kapan evaluasi dimulai;
- bagaimana gap-through diperlakukan;
- bagaimana SL dan TP yang tersentuh pada candle yang sama diperlakukan;
- bagaimana timeout ditentukan;
- bagaimana horizon tidak lengkap dibedakan;
- bagaimana biaya diterapkan;
- dan bagaimana outcome dicatat.

Perubahan pada mesin evaluasi dapat mengubah status trade tanpa mengubah data harga.

Contohnya, jika versi lama menganggap same-bar SL/TP sebagai TP, sedangkan versi baru menetapkannya sebagai AMBIGUOUS_INTRABAR, hasil penelitian dapat berubah secara material.

### 23.2.12. multiple_testing_family_id

Identitas ini mencatat keluarga pengujian yang digunakan dalam prosedur multiple testing.

Contoh:
multiple_testing_family_id = FAMILY-SAMSON-H3-SLTP-001

Satu keluarga pengujian dapat mencakup sejumlah kandidat yang dianggap sebagai bagian dari satu proses seleksi.

Informasi ini penting karena hasil p-value atau adjusted p-value tidak dapat dibaca tanpa mengetahui:

- pengujian apa saja yang masuk dalam keluarga;
- berapa banyak kandidat yang diuji;
- apakah keluarga worst-case dan best-case dipisahkan;
- apakah ada keluarga sebelumnya;
- dan apakah hasil telah diseleksi dari banyak percobaan.

Jika keluarga pengujian tidak dicatat, pembaca dapat salah menganggap hasil yang telah melalui banyak pencarian sebagai hasil dari satu pengujian sederhana.

---

## 23.3. Mengapa Versi Metodologi Penting?

### 23.3.1. Aturan yang Berubah Dapat Mengubah Hasil

Dalam penelitian trading, perubahan kecil pada aturan dapat menghasilkan perubahan besar pada kesimpulan.

Contoh perubahan:

- threshold RV dari 5 menjadi 4;
- entry dari close menjadi next bar open;
- ATR dari periode 14 menjadi 20;
- B0 dari nearest day menjadi random day;
- same-bar SL/TP dari worst-case menjadi best-case;
- biaya transaksi dari nol menjadi biaya aktual;
- horizon dari R3 menjadi R5.

Masing-masing perubahan dapat mengubah:

- jumlah event;
- jumlah event valid;
- jumlah pasangan B1-B0;
- distribusi return;
- MAE/MFE;
- jumlah kandidat yang lolos;
- dan status OOS.

Karena itu, perubahan metodologi harus dianggap sebagai perubahan yang bermakna, bukan sekadar pembaruan kecil yang boleh diabaikan.

### 23.3.2. Hasil Versi Lama Tidak Boleh Dicampur dengan Versi Baru

Misalnya:

- hasil B1 dihitung menggunakan Entry v1.0;
- hasil B0 dihitung menggunakan Entry v1.1;
- MAE dihitung menggunakan definisi v1.0;
- Evaluation Engine menggunakan v2.0.

Jika hasil tersebut digabungkan tanpa penjelasan, perbandingan menjadi tidak sahih.

B1 dan B0 harus diproses dengan aturan yang sebanding. Demikian pula, hasil dari dua batch hanya boleh digabungkan jika definisi dan protokolnya kompatibel.

Contoh yang tidak tepat:

> "Kami menggabungkan hasil penelitian 2024 dan 2026 karena sama-sama meneliti SAMSON."

Kesamaan nama tidak menjamin kesamaan metodologi.

Pertanyaan yang harus dijawab:

- Apakah definisi SAMSON sama?
- Apakah timeframe sama?
- Apakah baseline volume sama?
- Apakah aturan declustering sama?
- Apakah entry sama?
- Apakah B0 sama?
- Apakah biaya sama?
- Apakah Evaluation Engine sama?
- Apakah populasi instrumen sama?
- Apakah periode data memiliki karakteristik yang sebanding?

Jika tidak, hasil mungkin perlu dipisahkan atau dianalisis sebagai versi berbeda.

### 23.3.3. Setiap Hasil Harus Diketahui Berasal dari Aturan yang Mana

Bayangkan laporan menampilkan:
Δ expectancy = +0,12R

Angka tersebut belum lengkap sebagai informasi penelitian.

Setidaknya pembaca perlu mengetahui:

- hipotesis apa;
- periode IS atau OOS;
- jumlah event;
- horizon;
- entry;
- B0;
- ATR;
- Evaluation Engine;
- candidate grid;
- multiple-testing family;
- dan computation ID.

Dengan identitas tersebut, angka menjadi bagian dari objek penelitian yang jelas.

Tanpa identitas, angka mudah dipindahkan dari satu konteks ke konteks lain dan disalahgunakan untuk mendukung kesimpulan yang tidak sesuai.

### 23.3.4. Bug Fix Tidak Selalu Sama dengan Perubahan Metodologi

Tidak semua perubahan perangkat lunak memiliki makna yang sama.

Ada perbedaan antara:

**Bug fix teknis**

Program sebelumnya salah menerapkan aturan yang sebenarnya sudah ditetapkan.

**Perubahan metodologi**

Peneliti mengubah aturan yang memang digunakan dalam penelitian.

Contoh bug fix:

- perhitungan median salah;
- timestamp salah dibaca;
- bar duplikat tidak terdeteksi;
- pembulatan menyebabkan kesalahan;
- indeks array bergeser satu bar.

Contoh perubahan metodologi:

- entry diubah dari close menjadi next bar open;
- threshold event diubah;
- aturan B0 diubah;
- same-bar ambiguity diubah;
- kandidat grid diperluas setelah melihat hasil.

Bug fix dapat mengharuskan hasil lama dihitung ulang. Perubahan metodologi harus menghasilkan versi protokol baru.

Keduanya harus dicatat secara eksplisit agar pembaca mengetahui mengapa hasil berubah.

### 23.3.5. Status Versi Penelitian

TEKB dapat menggunakan status untuk menunjukkan posisi suatu hasil dalam siklus penelitian.

Contoh status:

- **UNFROZEN** — aturan atau kandidat masih dapat berubah.
- **FROZEN** — kandidat dan protokol telah dikunci.
- **FREEZE_FAILED** — proses freeze gagal atau tidak memenuhi syarat.
- **OOS_PENDING** — kandidat frozen dan menunggu pengujian OOS.
- **OOS_VALIDATED** — kandidat memenuhi kriteria OOS.
- **OOS_REJECTED** — kandidat tidak memenuhi kriteria OOS.
- **OOS_SPENT** — periode OOS telah digunakan.
- **OOS_TAINTED** — OOS telah terpengaruh oleh tuning atau penggunaan ulang yang tidak sesuai.

Status ini membantu mencegah hasil sementara diperlakukan sebagai hasil final.

---

## 23.4. Mencatat Hasil yang Gagal

Penelitian yang jujur tidak hanya mencatat hasil yang positif. Hasil yang gagal, tidak lengkap, tidak dapat dipasangkan, atau ditolak juga harus dicatat.

Jika hanya hasil yang baik yang disimpan, audit trail berubah menjadi alat untuk memilih cerita yang menyenangkan.

### 23.4.1. NO_MATCH_FOUND

**NO_MATCH_FOUND** berarti event B1 tidak memiliki pasangan B0 yang memenuhi aturan pemilihan.

Contoh penyebab:

- tidak ada hari pembanding yang valid;
- semua kandidat B0 sudah digunakan;
- tidak ada event pada slot yang sesuai;
- populasi pembanding tidak memenuhi syarat;
- atau aturan matching terlalu ketat untuk event tersebut.

Status ini harus dicatat bersama:

- event_id;
- alasan tidak ditemukan pasangan;
- aturan B0 yang digunakan;
- populasi yang diperiksa;
- dan batch penelitian.

Event dengan NO_MATCH_FOUND tidak boleh diam-diam dihapus tanpa jejak. Event tersebut dapat dikeluarkan dari analisis paired, tetapi keberadaannya tetap penting untuk memahami denominator dan potensi bias seleksi.

### 23.4.2. INSUFFICIENT_HORIZON

**INSUFFICIENT_HORIZON** berarti data setelah entry tidak cukup untuk menghitung horizon yang diwajibkan.

Contoh:

- event terjadi terlalu dekat dengan akhir dataset;
- data perdagangan terputus;
- instrumen berhenti memiliki data;
- atau horizon R10 belum tersedia.

Misalnya, penelitian membutuhkan horizon 10 bar, tetapi hanya tersedia 4 bar setelah entry. Event tersebut tidak boleh diperlakukan sebagai hasil lengkap R10.

Status ini membantu membedakan:

- hasil buruk;
- hasil baik;
- dan hasil yang memang belum dapat dihitung.

Data yang tidak lengkap bukan otomatis hasil negatif.

### 23.4.3. INVALIDATED

**INVALIDATED** berarti event atau pengukuran tidak dapat digunakan karena melanggar aturan validitas yang telah ditetapkan.

Contoh penyebab:

- OHLC tidak konsisten;
- timestamp rusak;
- harga atau volume tidak valid;
- event melanggar aturan no-look-ahead;
- entry tidak sah;
- data terkena duplikasi;
- atau terjadi pelanggaran kontrak penelitian.

Invalidated bukan berarti event tersebut menghasilkan kerugian. Artinya, event tidak memenuhi syarat untuk digunakan dalam analisis tertentu.

### 23.4.4. OOS_REJECTED

**OOS_REJECTED** berarti kandidat yang sebelumnya lolos seleksi IS tidak memenuhi kriteria validasi OOS.

Status ini sangat penting karena menunjukkan bahwa proses penelitian tidak hanya menyimpan keberhasilan.

Kandidat dapat memiliki:

- hasil IS positif;
- statistik IS yang menjanjikan;
- status frozen;
- tetapi tetap ditolak pada OOS.

Penolakan tersebut harus disimpan, bukan disembunyikan atau diganti namanya menjadi "perlu sedikit optimasi".

OOS_REJECTED adalah informasi bahwa bukti generalisasi belum memadai.

### 23.4.5. NO_EDGE_FOUND

**NO_EDGE_FOUND** berarti penelitian tidak menemukan kandidat yang memenuhi kriteria edge yang telah ditentukan.

Penyebabnya dapat berupa:

- B1 tidak lebih baik daripada B0;
- perbedaan terlalu kecil;
- interval ketidakpastian terlalu lebar;
- hasil tidak stabil;
- kandidat gagal setelah biaya;
- multiple-testing membuat bukti tidak memadai;
- atau tidak ada kandidat yang lolos seluruh kriteria.

Status ini bukan kegagalan sistem. Status ini adalah hasil penelitian.

Contoh:

> "Dalam ruang kandidat dan protokol yang telah ditentukan, tidak ditemukan bukti yang cukup untuk menyatakan adanya edge."

Kesimpulan tersebut jauh lebih bernilai daripada memaksakan satu kandidat hanya karena penelitian harus menghasilkan sinyal.

### 23.4.6. Mengapa Kegagalan adalah Bagian dari Pengetahuan?

Bayangkan dua laboratorium melakukan penelitian.

Laboratorium pertama hanya menyimpan eksperimen yang berhasil. Laboratorium kedua menyimpan semua eksperimen, termasuk yang gagal.

Laboratorium kedua memiliki pengetahuan yang lebih baik karena dapat mengetahui:

- kondisi apa yang tidak bekerja;
- aturan mana yang tidak stabil;
- kandidat mana yang gagal di OOS;
- berapa banyak pencarian yang telah dilakukan;
- dan batas-batas hipotesis yang sedang dipelajari.

Dalam trading, informasi seperti ini sangat penting. Jika semua hasil gagal dihapus, peneliti dapat terus mengulangi percobaan yang sama tanpa menyadari bahwa ruang kandidat tersebut sudah berkali-kali tidak memberikan bukti.

Karena itu:

> Hasil negatif mengurangi ketidakpastian tentang apa yang tidak bekerja.

Kegagalan juga membantu mencegah:

- pengulangan eksperimen tanpa sadar;
- cherry-picking;
- publikasi hasil terbaik saja;
- penyamaran hasil IS yang gagal OOS;
- dan pembentukan keyakinan yang terlalu optimistis.

### 23.4.7. Contoh Rekaman Status Event

| event_id | Status | Keterangan |
|---|---|---|
| EVT-001 | VALID | Memenuhi seluruh aturan awal |
| EVT-002 | NO_MATCH_FOUND | Tidak memiliki pasangan B0 |
| EVT-003 | INSUFFICIENT_HORIZON | Data setelah entry tidak cukup |
| EVT-004 | INVALIDATED | Timestamp tidak valid |
| EVT-005 | EVALUATED | Outcome berhasil dihitung |
| EVT-006 | AMBIGUOUS_INTRABAR | Urutan SL/TP tidak diketahui |

Dengan tabel seperti ini, jumlah event tidak lagi menjadi angka yang misterius. Pembaca dapat memahami ke mana event pergi dan mengapa.

---

## 23.5. Reproduksibilitas

### 23.5.1. Apa Itu Reproduksibilitas?

**Reproduksibilitas** berarti analisis dapat dijalankan kembali menggunakan data, aturan, versi, dan konfigurasi yang sama sehingga menghasilkan keluaran yang sama atau dapat dijelaskan perbedaannya.

Reproduksibilitas tidak selalu berarti setiap komputer akan menghasilkan file byte-per-byte yang identik. Perbedaan lingkungan perangkat lunak, pembulatan, atau urutan komputasi dapat menyebabkan variasi kecil.

Namun, hasil substantif harus dapat dijelaskan dan ditelusuri.

Pertanyaan utamanya:

> "Jika proses ini dijalankan kembali dengan input dan aturan yang sama, apakah kita dapat memahami mengapa hasilnya sama atau berbeda?"

### 23.5.2. Mengapa Peneliti Tidak Boleh Bergantung pada Ingatan?

Penelitian yang hanya bergantung pada ingatan peneliti rentan terhadap kesalahan.

Setelah beberapa minggu atau bulan, peneliti mungkin lupa:

- threshold yang digunakan;
- apakah entry memakai close atau open;
- apakah B0 memakai nearest day;
- apakah biaya sudah dimasukkan;
- apakah hasil berasal dari IS atau OOS;
- berapa banyak kandidat yang diuji;
- atau apakah suatu aturan telah diubah.

Ingatan manusia tidak dirancang untuk menjadi sistem version control.

Karena itu, TEKB harus menjadikan catatan terstruktur sebagai sumber kebenaran, bukan ingatan atau percakapan informal.

### 23.5.3. Apa yang Harus Disimpan?

Untuk memungkinkan reproduksibilitas, setidaknya perlu disimpan:

#### A. Identitas Penelitian

- computation_id;
- protocol_hash;
- hypothesis_id;
- research_batch_id;
- attempt_number;
- tanggal dan waktu eksekusi;
- identitas peneliti atau proses.

#### B. Definisi dan Versi

- versi event detector;
- candidate_grid_version_id;
- entry_definition_version_id;
- b0_selection_rule_version;
- mae_mfe_definition_version_id;
- atr_definition_version_id;
- evaluation_engine_version_id;
- multiple_testing_family_id.

#### C. Data

- sumber data;
- periode data;
- daftar instrumen;
- timeframe;
- status penyesuaian harga;
- versi dataset;
- checksum atau identitas file;
- aturan pembersihan data;
- dan informasi perubahan data.

#### D. Konfigurasi Penelitian

- threshold;
- horizon;
- session atau slot;
- aturan declustering;
- aturan validasi;
- biaya;
- slippage;
- aturan gap;
- aturan same-bar ambiguity;
- dan kriteria seleksi.

#### E. Hasil dan Status

- jumlah event terdeteksi;
- jumlah event valid;
- jumlah event memiliki B0;
- jumlah event dievaluasi;
- jumlah event dikeluarkan;
- alasan pengeluaran;
- metrik B1;
- metrik B0;
- Δ;
- interval bootstrap;
- hasil multiple testing;
- status IS;
- status freeze;
- status OOS.

### 23.5.4. Reproduksibilitas dari Data hingga Kesimpulan

Rantai reproduksibilitas TEKB dapat digambarkan sebagai berikut:
Dataset versi tertentu
↓
Protokol versi tertentu
↓
Event detector versi tertentu
↓
Daftar event dengan event_id
↓
Entry dan B0
↓
MAE/MFE dan evaluasi
↓
Agregasi B1 versus B0
↓
Bootstrap dan multiple testing
↓
Keputusan seleksi
↓
Freeze
↓
OOS
↓
Kesimpulan


Setiap tahap harus dapat menjawab:

- Input apa yang diterima?
- Aturan apa yang diterapkan?
- Output apa yang dihasilkan?
- Versi apa yang digunakan?
- Berapa jumlah record masuk dan keluar?
- Mengapa sebagian record dikeluarkan?
- Apakah ada perubahan dari tahap sebelumnya?

### 23.5.5. Immutable Ledger

Salah satu pendekatan yang dapat digunakan adalah **immutable ledger**, yaitu catatan hasil yang tidak diubah secara diam-diam setelah dibuat.

Jika terjadi koreksi:

- hasil lama tetap disimpan;
- alasan koreksi dicatat;
- hasil baru diberi identitas baru;
- hubungan antara hasil lama dan baru dijelaskan;
- dan tidak ada penggantian diam-diam.

Contoh:
Result A:
computation_id = COMP-001
protocol_hash = HASH-A
status = COMPLETED

Correction:
reason = ATR indexing bug fixed

Result B:
computation_id = COMP-002
protocol_hash = HASH-B
supersedes = COMP-001
status = COMPLETED

Dengan cara ini, sejarah penelitian tetap terlihat.

### 23.5.6. Reproduksibilitas Bukan Berarti Hasil Pasti Benar

Analisis yang dapat diulang belum tentu menghasilkan kesimpulan yang benar.

Sebuah metode dapat:

- sangat rapi;
- sangat konsisten;
- mudah dijalankan ulang;

tetapi tetap memiliki masalah seperti:

- data yang bias;
- hipotesis yang lemah;
- B0 yang tidak adil;
- look-ahead;
- overfitting;
- atau asumsi yang salah.

Reproduksibilitas menjawab:

> "Apakah prosesnya dapat diperiksa dan diulang?"

Reproduksibilitas tidak otomatis menjawab:

> "Apakah hipotesisnya benar?"

Karena itu, reproduksibilitas adalah syarat penting untuk audit, tetapi tetap harus disertai validitas metodologi.

### 23.5.7. Reproduksibilitas oleh Peneliti Lain atau Proses Berikutnya

Dalam sistem yang baik, peneliti lain—atau versi TEKB berikutnya—dapat mengambil:

- dataset yang sama;
- protokol yang sama;
- versi mesin yang sama;
- konfigurasi yang sama;

lalu menjalankan kembali penelitian.

Jika hasil berbeda, perbedaan tersebut dapat diselidiki:

- apakah dataset berubah?
- apakah kode berubah?
- apakah versi library berubah?
- apakah seed bootstrap berbeda?
- apakah aturan pembulatan berbeda?
- apakah ada bug?
- apakah data sumber direvisi?

Tanpa audit trail, perbedaan hasil hanya akan menjadi perdebatan. Dengan audit trail, perbedaan dapat menjadi objek pemeriksaan.

---

## Ringkasan Bab

Audit trail menjaga agar setiap kesimpulan TEKB memiliki jalur yang dapat ditelusuri dari data mentah sampai keputusan akhir.

Hal-hal utama yang harus dipahami:

- **Audit trail bukan sekadar log teknis**
  - Audit trail menjelaskan hubungan antara data, aturan, event, hasil, dan keputusan.
- **Setiap penelitian memerlukan identitas**
  - computation_id, protocol_hash, hypothesis_id, research_batch_id, dan attempt_number membantu mengidentifikasi asal suatu hasil.
- **Setiap komponen metodologi harus berversi**
  - Candidate grid, entry, B0, MAE/MFE, ATR, Evaluation Engine, dan multiple-testing family dapat mengubah hasil sehingga harus dicatat.
- **Hasil lama dan baru tidak boleh dicampur sembarangan**
  - Perubahan metodologi harus menghasilkan identitas atau versi baru.
- **Hasil gagal harus disimpan**
  - NO_MATCH_FOUND, INSUFFICIENT_HORIZON, INVALIDATED, OOS_REJECTED, dan NO_EDGE_FOUND adalah bagian dari pengetahuan.
- **Reproduksibilitas membutuhkan data, aturan, dan versi**
  - Penelitian tidak boleh bergantung pada ingatan peneliti.
- **Reproduksibilitas bukan jaminan kebenaran**
  - Proses yang dapat diulang tetap harus dinilai dari kualitas data, keadilan pembanding, validitas aturan, dan ketepatan interpretasi.

Prinsip penutup bab ini:

> Jika sebuah kesimpulan tidak dapat ditelusuri kembali ke data, aturan, event, dan proses yang menghasilkannya, maka kesimpulan tersebut belum memiliki fondasi audit yang memadai.

Dalam TEKB, audit trail bukan pekerjaan administratif tambahan. Audit trail adalah bagian dari metode penelitian itu sendiri. Ia memastikan bahwa "Bukti dulu, keputusan belakangan" tidak berhenti sebagai slogan, melainkan benar-benar terlihat dalam setiap jejak proses penelitian.

---

## Pertanyaan Refleksi

1. Apa yang dimaksud dengan audit trail dalam penelitian TEKB?
2. Mengapa audit trail bukan sekadar log teknis?
3. Apa fungsi computation_id dan protocol_hash?
4. Mengapa setiap komponen metodologi harus memiliki versi?
5. Mengapa hasil versi lama tidak boleh dicampur dengan versi baru?
6. Apa perbedaan antara bug fix dan perubahan metodologi?
7. Mengapa hasil yang gagal harus tetap dicatat?
8. Apa arti NO_MATCH_FOUND, INSUFFICIENT_HORIZON, dan INVALIDATED?
9. Mengapa OOS_REJECTED bukan alasan untuk menyembunyikan hasil?
10. Apa yang dimaksud dengan reproduksibilitas penelitian?
11. Mengapa reproduksibilitas bukan jaminan kebenaran?
12. Apa fungsi immutable ledger dalam audit trail?

---

## Kalimat Kunci

> Dalam TEKB, audit trail bukan pekerjaan administratif tambahan. Audit trail adalah bagian dari metode penelitian itu sendiri. Ia memastikan bahwa "Bukti dulu, keputusan belakangan" tidak berhenti sebagai slogan, melainkan benar-benar terlihat dalam setiap jejak proses penelitian.

---

<div align="center">

[← Bab Sebelumnya](/posts/bab-22-cara-membaca-hasil/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Bab Selanjutnya →](/posts/bab-24-batasan-tekb/)

</div>