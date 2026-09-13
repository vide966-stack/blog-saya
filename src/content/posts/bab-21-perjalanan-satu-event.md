---
title: "BAB 21 — Perjalanan Satu Event dari Awal sampai Akhir"
published: 2026-09-12
description: "Bab ini menyatukan seluruh komponen TEKB melalui perjalanan satu event — dari data OHLCV, deteksi SAMSON, entry, B0, MAE/MFE, hingga keputusan akhir."
tags: ["bab-21", "event", "alur", "audit-trail"]
category: "Bab"
draft: false
lang: ""
---

**BAGIAN VII — MEMBACA, MENELUSURI, DAN MENGGUNAKAN HASIL TEKB**

---

Pada bab-bab sebelumnya, kita telah membahas berbagai komponen TEKB secara terpisah. Kita mengenal data OHLCV, SAMSON sebagai detektor anomali volume, aturan entry, B0 sebagai pembanding, MAE dan MFE sebagai alat pengukuran gerakan harga, ATR sebagai satuan volatilitas, Evaluation Engine sebagai wasit, serta IS, freeze, dan OOS sebagai tahapan penelitian.

Namun, memahami setiap komponen secara terpisah belum tentu membuat seluruh proses mudah dibayangkan.

Bab ini menyatukan komponen-komponen tersebut melalui perjalanan satu event, mulai dari data awal sampai menjadi bagian dari kesimpulan penelitian. Contoh yang digunakan bersifat ilustratif. Angka-angkanya bukan hasil penelitian nyata dan tidak boleh dianggap sebagai bukti bahwa suatu sinyal menguntungkan.

Tujuan utama contoh ini bukan menunjukkan bahwa sebuah event pasti menghasilkan keuntungan. Tujuannya adalah memperlihatkan bagaimana TEKB menjaga agar setiap event diproses dengan aturan yang jelas, dapat diukur, dapat dibandingkan, dan dapat ditelusuri.

---

## 21.1. Kondisi Awal

Sebelum sebuah event dapat dideteksi, TEKB membutuhkan data dan aturan yang telah ditentukan.

### 21.1.1. Data OHLCV Tersedia

Data dasar yang digunakan adalah OHLCV:

- **Open:** harga pembukaan bar;
- **High:** harga tertinggi bar;
- **Low:** harga terendah bar;
- **Close:** harga penutupan bar;
- **Volume:** jumlah atau ukuran aktivitas transaksi sesuai sumber data.

Contoh satu bar 5 menit:

| Komponen | Nilai ilustratif |
|---|---|
| Instrumen | ABCD |
| Tanggal | 2026-03-10 |
| Session | Pagi |
| Slot | 09:30–09:34:59 |
| Open | 1.000 |
| High | 1.015 |
| Low | 995 |
| Close | 1.010 |
| Volume | 750.000 |

Angka tersebut hanya contoh untuk menjelaskan alur.

Sebelum digunakan, data harus melewati pemeriksaan kualitas. Bar yang invalid, timestamp yang bermasalah, duplikasi, data yang hilang, atau bar di luar jadwal perdagangan harus ditangani sesuai kontrak penelitian.

TEKB tidak boleh memperlakukan semua bar sebagai valid hanya karena bar tersebut tersedia dalam file.

### 21.1.2. Baseline Volume Tersedia

SAMSON tidak hanya melihat volume secara absolut. Volume harus dibandingkan dengan kondisi normal yang sesuai.

Volume 750.000 mungkin sangat besar untuk satu slot, tetapi biasa saja untuk slot lain. Karena itu, TEKB menggunakan baseline yang memperhatikan konteks waktu, misalnya:

- instrumen;
- session;
- slot waktu;
- periode historis yang diperbolehkan;
- aturan ex-ante;
- data yang tersedia sebelum bar yang sedang dinilai.

Misalnya, baseline volume untuk slot tersebut adalah 150.000.

Maka relative volume atau RV dapat dihitung sebagai:

> RV_t = V_t / BaselineVolume_t

Dengan angka ilustratif:

> RV_t = 750.000 / 150.000 = 5

Artinya, volume bar tersebut sekitar lima kali baseline yang digunakan.

Namun, angka RV=5 belum otomatis berarti harga akan naik. RV hanya menunjukkan bahwa aktivitas volume relatif tidak biasa dibandingkan kondisi pembandingnya.

### 21.1.3. Aturan SAMSON Telah Dibekukan

Sebelum event dicari, aturan SAMSON harus sudah ditentukan.

Misalnya, penelitian menetapkan:

- timeframe: 5 menit;
- baseline: session/slot-aware;
- threshold: RV > 5;
- hanya bar valid yang digunakan;
- event berdekatan ditangani dengan aturan declustering;
- volume tidak dibandingkan secara sembarangan dengan slot yang berbeda;
- event tidak boleh menggunakan informasi masa depan.

Aturan tersebut harus memiliki versi, misalnya:

samson_definition_version:
SAMSON_RV_SESSION_SLOT_V1

Dengan demikian, jika sebuah event terdeteksi, kita dapat mengetahui aturan apa yang digunakan untuk mendeteksinya.

---

## 21.2. SAMSON Mendeteksi Anomali

### 21.2.1. Volume Relatif Melewati Ambang

Pada contoh ini, volume bar T adalah 750.000, sedangkan baseline slot adalah 150.000. RV yang dihasilkan adalah 5.

Jika aturan event menyatakan bahwa SAMSON aktif ketika:

> RV_t ≥ 5

maka bar tersebut memenuhi kondisi deteksi.

Penting untuk membedakan dua hal:

- **Deteksi anomali:** volume relatif tidak biasa.
- **Prediksi arah:** harga akan naik atau turun.

SAMSON hanya melakukan hal pertama.

SAMSON belum menyatakan bahwa event tersebut merupakan sinyal BUY. Ia hanya menyatakan bahwa bar tersebut layak dicatat sebagai kejadian untuk penelitian.

### 21.2.2. Event Diberi Identitas

Setelah kondisi terpenuhi, TEKB membuat event terstruktur.

Event tidak cukup hanya berupa tanda pada chart. Event harus memiliki identitas yang memungkinkan seluruh proses setelahnya ditautkan kembali.

Contoh:
event_id:
EVT_20260310_ABCD_093000_0001

instrument:
ABCD

event_date:
2026-03-10

session_id:
MORNING

slot_id:
09:30

detection_bar:
T

detection_timestamp:
2026-03-10 09:34:59

samson_rv:
5.00

samson_threshold:
5.00

samson_definition_version:
SAMSON_RV_SESSION_SLOT_V1

Identitas event berfungsi seperti nomor registrasi. Dengan nomor tersebut, TEKB dapat menghubungkan:

- bar asal;
- baseline volume;
- RV;
- waktu deteksi;
- entry;
- B0;
- MAE/MFE;
- hasil evaluasi;
- status akhir.

### 21.2.3. Waktu Deteksi Dicatat

Waktu deteksi harus menunjukkan kapan informasi event benar-benar tersedia.

Jika SAMSON menggunakan volume dan harga penutupan bar T, event baru dapat dianggap diketahui setelah bar T selesai.

TEKB tidak boleh menggunakan informasi dari akhir bar untuk berpura-pura bahwa event telah diketahui pada awal bar.

Karena itu, setidaknya perlu dibedakan:

- **event time:** waktu bar atau kejadian;
- **confirmation time:** waktu event dikonfirmasi;
- **information availability time:** waktu informasi tersedia;
- **entry time:** waktu posisi penelitian dimulai;
- **evaluation time:** waktu hasil diukur.

Pemisahan waktu ini mencegah kebocoran informasi dari masa depan.

### 21.2.4. Declustering

Jika beberapa bar berturut-turut memenuhi threshold SAMSON, TEKB tidak boleh langsung memperlakukan semuanya sebagai event yang sepenuhnya terpisah tanpa aturan.

Event yang berdekatan dapat berasal dari episode pasar yang sama. Jika seluruhnya dihitung sebagai observasi independen, episode tersebut dapat diberi bobot terlalu besar.

Karena itu, SAMSON dapat menggunakan aturan **declustering**, misalnya:

- hanya event pertama dalam satu episode yang dipilih;
- event berikutnya dalam radius waktu tertentu dikelompokkan;
- aturan episode ditetapkan sebelum penelitian;
- event yang dikeluarkan tetap dicatat statusnya.

Declustering bukan cara untuk memilih event yang hasilnya bagus. Declustering adalah cara untuk mengendalikan pengulangan event yang terlalu berdekatan.

---

## 21.3. Penentuan Entry

Setelah event terdeteksi, TEKB harus menentukan kapan penelitian dianggap mulai mengukur posisi.

### 21.3.1. Signal Close

Misalnya, bar T ditutup pada harga 1.010.

Harga ini disebut sebagai **signal close**.

signal_close:
1.010

Namun, signal close bukan otomatis harga entry.

Jika event baru diketahui setelah bar T selesai, maka menggunakan harga penutupan T sebagai harga entry dapat menimbulkan masalah apabila harga tersebut tidak benar-benar dapat dianggap tersedia untuk eksekusi sesuai desain penelitian.

TEKB harus membedakan:

- harga penutupan yang menghasilkan sinyal;
- waktu informasi tersedia;
- harga entry yang diasumsikan;
- waktu entry.

### 21.3.2. Next Valid Bar Open

Dalam contoh ini, aturan entry telah dibekukan sebagai:

> Setelah bar T selesai dan event terkonfirmasi, entry penelitian dilakukan pada Open bar valid berikutnya.

Misalnya:

| Komponen | Nilai |
|---|---|
| Signal bar | T |
| Signal close | 1.010 |
| Bar berikutnya | T+1 |
| Open T+1 | 1.020 |
| Raw entry | 1.020 |

Maka:
entry_definition:
NEXT_VALID_BAR_OPEN

raw_entry_price:
1.020

Harga entry adalah 1.020, bukan 1.010.

Perbedaan ini penting karena seluruh pengukuran setelahnya—return, MAE, MFE, SL, TP, dan outcome—bergantung pada harga entry yang digunakan.

### 21.3.3. Entry Gap

Dalam contoh ini, signal close adalah 1.010 dan Open bar berikutnya adalah 1.020.

Maka gap entry dapat dihitung sebagai:

> Gap = (Open_T+1 − Close_T) / Close_T

> Gap = (1.020 − 1.010) / 1.010 ≈ 0,99%

Gap tersebut menunjukkan bahwa harga pembukaan berada di atas signal close.

Gap harus dicatat sebagai bagian dari event, bukan disembunyikan.

Contoh:
signal_close:
1010

raw_entry_price:
1020

entry_gap_abs:
10

entry_gap_pct:
0.00990099

Gap dapat memengaruhi:

- harga entry;
- jarak ke SL dan TP;
- MAE;
- MFE;
- return;
- biaya;
- kelayakan eksekusi;
- perbedaan antara penelitian historis dan implementasi langsung.

### 21.3.4. Included in Research dan Actionable Live

TEKB perlu membedakan dua status yang tidak selalu sama:

- **included_in_research:** event dapat dimasukkan ke penelitian sesuai aturan;
- **actionable_live:** event secara praktis dapat ditindaklanjuti dalam kondisi perdagangan nyata.

Misalnya, gap yang sangat besar mungkin tetap sah untuk dimasukkan ke penelitian karena aturan entry memang menggunakan Open bar berikutnya. Namun, dalam praktik live, gap tersebut mungkin terlalu besar untuk dianggap menarik atau layak dieksekusi.

Contoh:
included_in_research:
true

actionable_live:
false

actionability_reason:
ENTRY_GAP_TOO_LARGE

Perbedaan ini penting. TEKB tidak boleh menghapus event historis hanya karena event tersebut kurang nyaman untuk perdagangan nyata, kecuali penghapusan tersebut memang telah ditentukan dalam kontrak penelitian.

---

## 21.4. Pemilihan B0

Setelah B1 atau event utama memiliki entry, TEKB mencari pembanding B0.

Tujuannya bukan mencari event yang hasilnya mirip atau membuat B1 terlihat lebih baik. Tujuannya adalah membangun pembanding yang adil untuk mendekati pertanyaan:

> Apa yang mungkin terjadi pada kondisi yang sebanding tanpa kondisi event utama yang sedang diuji?

### 21.4.1. Instrumen yang Sama

Jika event B1 terjadi pada instrumen ABCD, maka B0 harus berasal dari instrumen yang sama, kecuali protokol penelitian secara eksplisit menetapkan desain lain.

Hal ini membantu mengurangi perbedaan yang berasal dari karakteristik instrumen.

B1 instrument:
ABCD

B0 instrument:
ABCD

Membandingkan B1 pada saham ABCD dengan B0 pada saham yang sangat berbeda dapat mencampur efek sinyal dengan perbedaan karakter instrumen.

### 21.4.2. Slot yang Sama

B0 juga harus memiliki konteks waktu yang sebanding.

Jika B1 terjadi pada slot 09:30, B0 sebaiknya dicari pada slot yang sama atau sesuai aturan slot yang telah ditetapkan.

Hal ini penting karena volume, volatilitas, spread, dan perilaku harga dapat berbeda antara:

- pembukaan pasar;
- pertengahan sesi;
- menjelang penutupan;
- sesi pagi;
- sesi siang.

B0 pada slot yang berbeda dapat menjadi pembanding yang tidak adil.

### 21.4.3. Populasi Sesuai

B0 harus dipilih dari populasi yang sesuai dengan aturan penelitian.

Jika B1 telah melalui declustering, maka populasi B0 juga harus memperhitungkan aturan yang relevan.

Jika penelitian dibagi menjadi IS dan OOS, B0 juga harus mengikuti partisi tersebut.

B0 tidak boleh dipilih dari event yang:

- menggunakan informasi masa depan;
- sudah digunakan ulang secara terlarang;
- berada di luar periode yang diizinkan;
- melanggar aturan validitas;
- dipilih karena hasilnya menguntungkan.

### 21.4.4. Tidak Ada Penggunaan Ulang

Satu event B0 tidak boleh digunakan berulang kali jika protokol melarang penggunaan ulang.

Penggunaan ulang dapat membuat satu kejadian memiliki bobot terlalu besar dan menciptakan ketergantungan yang tidak diperhitungkan.

Contoh:
B0 event:
EVT_B0_20260115_ABCD_093000

used_count:
1

reuse_allowed:
false

Jika event tersebut telah dipasangkan dengan event B1 sebelumnya, event itu tidak boleh dipakai kembali untuk pasangan lain apabila aturan penelitian melarangnya.

### 21.4.5. Jika Tidak Ada Pasangan

Ada kemungkinan bahwa event B1 tidak memiliki B0 yang memenuhi semua aturan.

Dalam keadaan ini, TEKB tidak boleh memaksakan pasangan hanya agar jumlah sampel tetap besar.

Status yang tepat adalah:
b0_status:
NO_MATCH_FOUND

Event B1 tetap dicatat sebagai event yang terdeteksi. Namun, event tersebut tidak dapat digunakan dalam analisis edge berpasangan yang membutuhkan B0.

Ini bukan kegagalan sistem. Justru, NO_MATCH_FOUND menunjukkan bahwa TEKB tidak mengorbankan aturan pembanding demi memperoleh hasil yang tampak lebih baik.

---

## 21.5. Pengukuran MAE dan MFE

Setelah entry ditentukan dan pasangan B0 tersedia, TEKB mengukur bagaimana harga bergerak setelah entry.

### 21.5.1. Mengapa Mengukur Lebih dari Return Akhir?

Return akhir hanya menunjukkan posisi harga pada akhir periode tertentu.

Namun, selama perjalanan menuju hasil akhir, harga mungkin:

- turun jauh terlebih dahulu;
- naik tinggi lalu kembali;
- bergerak sempit;
- menyentuh level SL;
- mencapai level TP;
- mengalami gap;
- tidak mencapai target sampai batas waktu.

MAE dan MFE membantu menggambarkan perjalanan harga tersebut.

**MAE** atau Maximum Adverse Excursion mengukur gerakan paling merugikan setelah entry.

**MFE** atau Maximum Favorable Excursion mengukur gerakan paling menguntungkan setelah entry.

Untuk posisi long:

- Low digunakan untuk mengukur gerakan melawan posisi;
- High digunakan untuk mengukur gerakan mendukung posisi.

### 21.5.2. Horizon R1, R3, R5, dan R10

TEKB dapat mengukur MAE dan MFE pada beberapa horizon.

Misalnya:

- R1: satu bar setelah entry;
- R3: tiga bar setelah entry;
- R5: lima bar setelah entry;
- R10: sepuluh bar setelah entry.

Contoh hasil ilustratif:

| Horizon | MAE harga | MFE harga |
|---|---|---|
| R1 | -8 | +12 |
| R3 | -15 | +25 |
| R5 | -18 | +32 |
| R10 | -22 | +40 |

Angka tersebut harus dibaca sebagai hasil pengukuran, bukan prediksi.

Pada horizon R5, misalnya, harga pernah bergerak 18 poin melawan entry dan 32 poin mendukung entry selama jendela pengamatan.

### 21.5.3. Menggunakan High dan Low

Jika entry long adalah 1.020, dan pada tiga bar berikutnya:

- Low terendah = 1.005;
- High tertinggi = 1.045;

maka gerakan adverse dan favorable dapat dihitung dari entry.

Secara sederhana:

> MAE_harga = Low_terendah − Entry

> MAE_harga = 1.005 − 1.020 = −15

> MFE_harga = High_tertinggi − Entry

> MFE_harga = 1.045 − 1.020 = 25

MAE negatif menunjukkan gerakan melawan posisi long. MFE positif menunjukkan gerakan mendukung posisi long.

### 21.5.4. Status Kelengkapan Pengukuran

Tidak semua event dapat memiliki horizon lengkap.

Misalnya, event terjadi mendekati akhir dataset. Jika hanya tersedia dua bar setelah entry, maka MAE/MFE R5 atau R10 tidak dapat dihitung secara lengkap.

TEKB harus membedakan:

- COMPUTED_FULL_HORIZON;
- INSUFFICIENT_HORIZON;
- INVALIDATED.

Contoh:
mae_mfe_r1_status:
COMPUTED_FULL_HORIZON

mae_mfe_r3_status:
COMPUTED_FULL_HORIZON

mae_mfe_r5_status:
INSUFFICIENT_HORIZON

mae_mfe_r10_status:
INSUFFICIENT_HORIZON

Event dengan horizon yang tidak lengkap tidak boleh diam-diam dianggap memiliki hasil nol atau dianggap selesai secara normal.

Status kelengkapan harus memengaruhi apakah event boleh masuk ke analisis pada horizon tertentu.

### 21.5.5. ATR-Normalized

Jika ATR_entry tersedia dan event memenuhi syarat kelayakan, MAE dan MFE dapat dinormalisasi menggunakan ATR.

Misalnya:

- ATR_entry = 10;
- MAE harga = -15;
- MFE harga = +25.

Maka:

> MAE_×ATR = −15 / 10 = −1,5

> MFE_×ATR = 25 / 10 = 2,5

Artinya, gerakan terburuk yang melawan posisi setara dengan -1,5 ATR, sedangkan gerakan terbaik yang mendukung posisi setara dengan +2,5 ATR.

Contoh:
atr_entry:
10

mae_r3_price:
-15

mfe_r3_price:
25

mae_r3_atr:
-1.5

mfe_r3_atr:
2.5

atr_normalization_status:
ELIGIBLE

ATR-normalization membantu membandingkan event yang memiliki skala harga dan volatilitas berbeda.

Namun, normalisasi tidak menciptakan edge. Ia hanya mengubah satuan pengukuran agar perbandingan lebih masuk akal.

---

## 21.6. Evaluasi SL/TP

Setelah MAE/MFE tersedia, TEKB dapat mengevaluasi kandidat SL/TP yang telah ditentukan dalam candidate grid.

### 21.6.1. Candidate Grid

Misalnya, grid penelitian telah ditentukan sebelum seleksi:

| Kandidat | Stop Loss | Take Profit | Maximum Hold |
|---|---|---|---|
| C1 | 0,5 ATR | 1 ATR | 3 bar |
| C2 | 1 ATR | 2 ATR | 5 bar |
| C3 | 1,5 ATR | 3 ATR | 5 bar |

Grid tersebut bukan hasil yang dipilih setelah melihat OOS. Grid merupakan ruang hipotesis yang telah ditentukan dalam tahap penelitian.

Untuk contoh ini, misalkan kandidat yang sedang dievaluasi adalah:
SL:
1 ATR

TP:
2 ATR

MAX_HOLD:
5 bars

Jika entry adalah 1.020 dan ATR_entry adalah 10, maka:

> SL = 1.020 − (1 × 10) = 1.010

> TP = 1.020 + (2 × 10) = 1.040

Level penelitian menjadi:

- SL = 1.010;
- TP = 1.040;
- Maximum Hold = 5 bar.

### 21.6.2. Gap-Through

Misalkan pada bar setelah entry, Open langsung berada di bawah SL.

Contohnya:

- entry = 1.020;
- SL = 1.010;
- Open bar berikutnya = 1.000.

Harga telah melewati level SL sebelum atau pada pembukaan bar.

Dalam aturan TEKB, gap-through harus ditangani secara eksplisit. Jika aturan menyatakan exit dilakukan pada Open ketika Open telah melewati level, maka harga keluar adalah 1.000, bukan secara otomatis 1.010.

Contoh:
gap_through:
true

exit_reason:
SL_HIT

exit_price:
1000

Hal ini membuat evaluasi lebih realistis terhadap risiko gap.

### 21.6.3. Same-Bar SL dan TP

Misalkan dalam satu bar:

- High mencapai atau melewati TP;
- Low mencapai atau melewati SL.

Dengan data OHLCV biasa, kita mengetahui bahwa kedua level tersentuh, tetapi tidak mengetahui urutan intrabar secara pasti.

Apakah harga menyentuh SL lebih dahulu atau TP lebih dahulu? Data OHLCV bar tersebut mungkin tidak dapat menjawabnya.

TEKB tidak boleh memilih urutan yang paling menguntungkan hanya karena hasilnya lebih baik.

Event tersebut harus diberi status:
outcome_status:
AMBIGUOUS_INTRABAR

Kemudian, TEKB dapat melaporkan dua skenario:

- **Worst-case:** asumsi konservatif sesuai protokol;
- **Best-case:** hasil terbaik yang masih mungkin berdasarkan informasi yang tersedia.

Contoh:

| Skenario | Outcome |
|---|---|
| Worst-case | SL_HIT |
| Best-case | TP_HIT |

Worst-case dan best-case harus diterapkan secara konsisten kepada B1 dan B0. Tidak boleh menggunakan worst-case untuk B1 tetapi best-case untuk B0, atau sebaliknya.

### 21.6.4. Worst-Case

Worst-case digunakan untuk melihat hasil dengan asumsi konservatif ketika urutan intrabar tidak diketahui atau terdapat ambiguitas tertentu.

Tujuannya bukan membuat hasil selalu buruk, melainkan menghindari klaim keuntungan berdasarkan asumsi yang tidak dapat dibuktikan.

Jika event ambigu dapat menghasilkan SL atau TP, maka worst-case memilih hasil yang lebih merugikan sesuai aturan yang telah dibekukan.

Worst-case penting karena strategi yang hanya terlihat bagus dalam skenario terbaik mungkin tidak cukup kuat untuk digunakan sebagai dasar keputusan.

### 21.6.5. Best-Case

Best-case menunjukkan hasil terbaik yang masih mungkin berdasarkan data dan aturan evaluasi.

Best-case bukan bukti bahwa trader pasti memperoleh hasil tersebut. Ia hanya menunjukkan batas atas yang mungkin dari informasi yang tersedia.

Best-case dapat berguna untuk memahami rentang ketidakpastian akibat resolusi data yang terbatas.

Namun, best-case tidak boleh dipresentasikan sebagai hasil utama tanpa menyebutkan bahwa terdapat ambiguitas intrabar.

### 21.6.6. Timeout

Jika tidak ada SL atau TP yang tercapai sampai Maximum Hold berakhir, event dapat diberi status:
outcome_status:
TIMEOUT

TIMEOUT berarti batas waktu evaluasi telah tercapai tanpa kondisi exit SL atau TP yang ditentukan.

TIMEOUT berbeda dari INSUFFICIENT_HORIZON.

- **TIMEOUT:** data cukup untuk menyelesaikan jendela evaluasi, tetapi tidak ada SL/TP yang tercapai.
- **INSUFFICIENT_HORIZON:** data tidak cukup untuk menyelesaikan jendela evaluasi.

Perbedaan ini penting karena keduanya memiliki makna berbeda. TIMEOUT adalah hasil penelitian, sedangkan INSUFFICIENT_HORIZON adalah masalah kelengkapan data.

---

## 21.7. Perbandingan B1 dan B0

Setelah setiap event dan pasangan pembanding diproses, TEKB mulai menggabungkan hasil pada tingkat kelompok.

Satu event tidak cukup untuk menyimpulkan bahwa sebuah hipotesis memiliki edge. Edge dinilai melalui kumpulan event B1 dan B0.

### 21.7.1. Expectancy

**Expectancy** adalah rata-rata hasil berdasarkan definisi return atau outcome yang digunakan.

Misalnya, setelah semua event dinilai:

| Kelompok | Expectancy |
|---|---|
| B1 | +0,12R |
| B0 | +0,05R |

Maka perbedaannya:

> Δ = E(B1) − E(B0)

> Δ = 0,12R − 0,05R = +0,07R

Angka ini menunjukkan bahwa rata-rata hasil B1 lebih tinggi daripada B0 sebesar 0,07R dalam contoh tersebut.

Namun, angka positif ini belum otomatis membuktikan edge. Kita masih perlu melihat jumlah event, penyebaran, ketidakpastian, biaya, dan kriteria penelitian.

### 21.7.2. Net Expectancy

Gross expectancy belum tentu mencerminkan hasil yang realistis.

Biaya transaksi dapat mencakup:

- komisi;
- spread;
- slippage;
- pajak atau pungutan;
- biaya lain yang relevan.

Karena itu, TEKB dapat menghitung net expectancy:

> E_net = E_gross − Biaya

Contoh ilustratif:

| Kelompok | Gross expectancy | Biaya rata-rata | Net expectancy |
|---|---|---|---|
| B1 | +0,12R | 0,04R | +0,08R |
| B0 | +0,05R | 0,04R | +0,01R |

Perbedaan net tetap perlu dihitung secara konsisten.

Biaya tidak boleh hanya dibebankan kepada B1 atau hanya kepada B0 jika kedua kelompok dimaksudkan untuk dibandingkan dalam kondisi yang sama.

### 21.7.3. Perbedaan Distribusi

TEKB tidak hanya membandingkan rata-rata.

Dua kelompok dapat memiliki expectancy yang sama, tetapi distribusinya sangat berbeda.

Perbandingan dapat mencakup:

- mean;
- median;
- proporsi hasil positif;
- penyebaran;
- percentile bawah;
- percentile atas;
- ekor kerugian;
- ekor keuntungan;
- peluang melewati ambang tertentu;
- frekuensi TIMEOUT;
- frekuensi SL_HIT;
- frekuensi TP_HIT;
- distribusi MAE;
- distribusi MFE.

Contohnya:

| Ukuran | B1 | B0 |
|---|---|---|
| Mean return | +0,12R | +0,05R |
| Median return | +0,03R | +0,02R |
| Proporsi positif | 54% | 51% |
| Percentile bawah | -1,20R | -0,90R |
| Percentile atas | +2,10R | +1,40R |

Dari tabel tersebut, B1 tampak memiliki rata-rata dan peluang positif lebih tinggi, tetapi juga memiliki percentile bawah yang lebih buruk. Artinya, B1 mungkin memiliki potensi keuntungan lebih besar sekaligus risiko ekor yang lebih berat.

Kesimpulan tidak boleh hanya berbunyi "B1 lebih baik" tanpa menjelaskan dimensi mana yang lebih baik dan mana yang lebih buruk.

### 21.7.4. Bootstrap

Setelah perbedaan B1 dan B0 dihitung, TEKB perlu menilai seberapa tidak pasti perbedaan tersebut.

Salah satu alatnya adalah **bootstrap**.

Bootstrap dapat digunakan untuk:

- membentuk distribusi Δ;
- melihat seberapa sering Δ tetap positif;
- menghitung interval ketidakpastian;
- memeriksa pengaruh event ekstrem;
- mempertimbangkan ketergantungan antar-event melalui date-cluster atau moving block bootstrap.

Misalnya, hasil observasi menunjukkan:
observed_delta:
+0.07R

Setelah bootstrap dilakukan, hasil dapat diringkas secara ilustratif:
bootstrap_method:
DATE_CLUSTER_BOOTSTRAP

replications:
10000

proportion_delta_positive:
0.94

confidence_interval:
[-0.01R, +0.15R]

Contoh ini menunjukkan bahwa sebagian besar resampling menghasilkan Δ positif, tetapi interval masih mencakup nilai negatif. Artinya, hasil terlihat menjanjikan, tetapi ketidakpastiannya masih cukup besar.

Angka tersebut hanya ilustrasi. Keputusan nyata harus mengikuti protokol penelitian dan metode bootstrap yang telah ditentukan.

### 21.7.5. Signifikansi

Signifikansi statistik digunakan untuk menilai apakah perbedaan yang diamati cukup tidak biasa jika dibandingkan dengan model atau hipotesis nol yang digunakan.

Namun, signifikansi bukan ukuran besarnya keuntungan dan bukan jaminan bahwa hipotesis benar.

TEKB tetap membutuhkan:

- B1 dan B0 yang adil;
- definisi statistik yang jelas;
- jumlah event yang memadai;
- metode resampling yang sesuai;
- perhatian terhadap ketergantungan data;
- interpretasi praktis.

Hasil yang signifikan tetapi sangat kecil mungkin tidak berguna setelah biaya. Sebaliknya, hasil yang besar tetapi sangat tidak stabil belum tentu dapat dipercaya.

### 21.7.6. BH-FDR

Jika banyak kandidat diuji pada tahap IS, TEKB perlu memperhitungkan multiple testing.

Misalnya, peneliti menguji berbagai kombinasi:

- SL;
- TP;
- Maximum Hold;
- threshold;
- definisi kondisi.

Semakin banyak percobaan, semakin besar peluang menemukan hasil positif secara kebetulan.

BH-FDR dapat digunakan pada tahap seleksi IS untuk mengendalikan proporsi temuan positif palsu dalam keluarga pengujian yang ditetapkan.

Dalam TEKB, keluarga pengujian worst-case dan best-case harus diperlakukan sesuai protokol, bukan dicampur sembarangan.

OOS tidak digunakan untuk memilih ulang kandidat dengan cara menguji banyak variasi baru lalu mengambil hasil terbaik.

### 21.7.7. Hasil Perbandingan B1 dan B0

Setelah semua ukuran dihitung, hasil perbandingan dapat disusun seperti berikut:

| Ukuran | B1 | B0 | Perbedaan |
|---|---|---|---|
| Jumlah event | 500 | 500 | - |
| Gross expectancy | +0,12R | +0,05R | +0,07R |
| Net expectancy | +0,08R | +0,01R | +0,07R |
| Median | +0,03R | +0,02R | +0,01R |
| Proporsi positif | 54% | 51% | +3 poin persentase |
| Worst-case Δ | +0,04R | - | +0,04R |
| Best-case Δ | +0,10R | - | +0,10R |

Tabel ini masih belum cukup untuk menyatakan edge secara final. Hasil harus dibaca bersama:

- validitas event;
- kualitas pasangan B0;
- ketidakpastian;
- bootstrap;
- signifikansi;
- multiple testing;
- biaya;
- jumlah instrumen;
- jumlah tanggal;
- stabilitas;
- kriteria seleksi yang telah ditetapkan.

---

## 21.8. Keputusan Akhir Event dan Hipotesis

Pada tahap ini, TEKB membedakan keputusan pada tingkat event dan keputusan pada tingkat hipotesis atau kandidat.

### 21.8.1. Keputusan pada Tingkat Event

Satu event dapat memiliki status seperti:

event_status:
VALID

b0_status:
MATCHED

mae_mfe_status:
COMPUTED_FULL_HORIZON

atr_normalization_status:
ELIGIBLE

evaluation_status:
COMPUTED

outcome_status:
TP_HIT

Atau:
event_status:
VALID

mae_mfe_status:
INSUFFICIENT_HORIZON

analysis_eligibility:
EXCLUDED_FROM_R10

Status event menjelaskan apa yang terjadi pada event tersebut. Status ini tidak sama dengan keputusan apakah hipotesis secara keseluruhan memiliki edge.

### 21.8.2. Keputusan pada Tingkat Kandidat

Setelah semua event dan B0 diproses, TEKB menilai kandidat berdasarkan aturan seleksi.

Misalnya, kandidat harus:

- lebih baik daripada B0 pada worst-case;
- lebih baik daripada B0 pada best-case;
- memiliki perbedaan positif;
- memenuhi kriteria statistik;
- lolos koreksi multiple testing pada keluarga yang sesuai;
- memenuhi batas minimum jumlah event;
- memiliki data yang valid;
- tidak melanggar aturan penelitian.

Jika seluruh syarat terpenuhi, kandidat dapat dinyatakan lolos IS Selection.

Namun, lolos IS Selection belum berarti kandidat siap digunakan. Kandidat masih harus dibekukan dan diuji pada OOS.

### 21.8.3. Jika Tidak Ada Kandidat yang Memenuhi Syarat

Jika tidak ada kandidat yang memenuhi seluruh kriteria, TEKB harus menghasilkan:
selection_status:
NO_EDGE_FOUND

NO_EDGE_FOUND berarti penelitian belum menemukan kandidat yang memenuhi standar bukti yang ditetapkan.

Status ini tidak berarti bahwa pasar tidak memiliki pola apa pun. Status ini berarti bahwa penelitian yang dilakukan belum berhasil menunjukkan edge yang cukup kuat, cukup stabil, atau cukup dapat dipercaya menurut protokol yang digunakan.

Peneliti tidak boleh memaksa memilih kandidat hanya karena sistem harus menghasilkan strategi.

Memilih kandidat yang tidak memenuhi syarat dapat mengubah penelitian menjadi proses pembenaran.

### 21.8.4. Jika Kandidat Dipilih

Jika satu kandidat lolos IS Selection, kandidat tersebut harus masuk ke tahap **freeze**.

Freeze mencatat:

- hypothesis ID;
- candidate version;
- entry definition;
- B0 rule;
- MAE/MFE definition;
- ATR definition;
- Evaluation Engine;
- candidate grid;
- selection criteria;
- multiple-testing family;
- research batch;
- fingerprint konfigurasi.

Setelah freeze, kandidat tidak boleh diubah berdasarkan hasil OOS.

### 21.8.5. OOS sebagai Tahap Berikutnya

Setelah freeze, kandidat diuji pada data OOS.

Alurnya menjadi:
Data OHLCV
↓
Baseline Volume
↓
SAMSON Detection
↓
Event ID
↓
Entry Definition
↓
B0 Matching
↓
MAE/MFE
↓
ATR Normalization
↓
Evaluation Engine
↓
B1 vs B0
↓
Bootstrap / Statistical Assessment
↓
IS Selection
↓
Freeze
↓
OOS Evaluation
↓
OOS_VALIDATED / OOS_REJECTED


OOS bukan tempat untuk mencari kandidat baru. OOS menguji kandidat yang telah dipilih.

Jika kandidat gagal pada OOS, hasil tersebut tetap dicatat. Jika kandidat lolos, status tersebut harus dipahami sebagai bukti generalisasi dalam konteks periode dan protokol yang diuji, bukan jaminan keuntungan masa depan.

---

## Ringkasan Bab

- Perjalanan event TEKB dimulai dari data OHLCV yang valid dan baseline yang tersedia.
- SAMSON mendeteksi anomali volume, bukan langsung menentukan BUY atau SELL.
- Setiap event diberi identitas, timestamp, dan versi aturan agar dapat ditelusuri.
- Entry harus ditentukan secara kausal, misalnya melalui NEXT_VALID_BAR_OPEN.
- Signal close, raw entry, entry gap, dan actionable live harus dibedakan.
- B0 dipilih dengan aturan yang adil dan tidak boleh dipaksakan jika tidak ada pasangan yang sesuai.
- MAE dan MFE mengukur perjalanan harga setelah entry pada horizon yang ditentukan.
- ATR-normalized digunakan jika event memenuhi syarat, untuk membantu perbandingan lintas skala volatilitas.
- Evaluation Engine menentukan outcome dengan aturan yang sama untuk B1 dan B0.
- Gap-through, same-bar ambiguity, worst-case, best-case, dan TIMEOUT harus ditangani secara eksplisit.
- Edge dinilai pada tingkat kelompok melalui perbandingan B1 dan B0, bukan dari satu event.
- Expectancy, net expectancy, distribusi, bootstrap, signifikansi, dan BH-FDR memiliki fungsi yang berbeda.
- Jika tidak ada kandidat yang memenuhi syarat, NO_EDGE_FOUND adalah hasil yang sah.
- Kandidat yang lolos IS harus dibekukan sebelum diuji pada OOS.

---

## Pertanyaan Refleksi

1. Mengapa SAMSON tidak boleh langsung dianggap sebagai sinyal BUY?
2. Mengapa event harus memiliki Event ID?
3. Apa perbedaan antara signal close dan raw entry price?
4. Mengapa entry gap harus dicatat?
5. Mengapa event dapat masuk penelitian tetapi tidak actionable live?
6. Mengapa B0 tidak boleh dipilih berdasarkan hasil yang menguntungkan?
7. Apa perbedaan MAE dan MFE?
8. Mengapa event dengan horizon tidak lengkap harus diberi status khusus?
9. Mengapa same-bar SL dan TP dapat menghasilkan AMBIGUOUS_INTRABAR?
10. Mengapa expectancy B1 yang positif belum cukup untuk menyatakan edge?
11. Apa fungsi bootstrap dalam perbandingan B1 dan B0?
12. Mengapa NO_MATCH_FOUND dan NO_EDGE_FOUND memiliki arti berbeda?
13. Mengapa kandidat yang lolos IS masih harus melalui freeze dan OOS?
14. Apa yang dapat ditelusuri kembali melalui audit trail sebuah event?

---

## Kalimat Kunci

> Dalam TEKB, satu event tidak langsung menjadi sinyal trading. Event harus melewati rangkaian aturan: dideteksi dari data yang tersedia, diberi identitas, ditentukan entry-nya, dibandingkan dengan B0, diukur melalui MAE/MFE, dievaluasi dengan engine yang sama, lalu digabungkan dengan event lain untuk menilai hipotesis. Dengan alur ini, TEKB tidak hanya bertanya apakah harga bergerak setelah suatu kondisi, tetapi apakah kondisi tersebut memberikan informasi yang dapat diukur, dibandingkan, dan diuji kembali secara jujur.

---

<div align="center">

[← Bab Sebelumnya](/posts/bab-20-oos-data-baru/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Bab Selanjutnya →](/posts/bab-22-cara-membaca-hasil/)

</div>