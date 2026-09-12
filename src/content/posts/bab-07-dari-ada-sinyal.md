---
title: "BAB 7 — Dari \"Ada Sinyal\" Menjadi \"Ada Kejadian yang Bisa Diukur\""
published: 2026-09-12
description: "Event adalah jembatan antara pengamatan visual dan penelitian berbasis data. Bab ini menjelaskan cara mengubah sinyal menjadi event terstruktur yang dapat diukur."
tags: ["bab-7", "event", "timestamp", "audit-trail"]
category: "Bab"
draft: false
lang: ""
---

**BAGIAN II — MEMBANGUN BAHASA DAN DATA PENELITIAN**

---

## Tujuan Bab

Dalam trading, kita sering menggunakan kalimat seperti:

- "Ada volume besar."
- "Muncul candle kuat."
- "Harga menembus resistance."
- "Terlihat tekanan beli."
- "Ada tanda-tanda pembalikan."

Kalimat-kalimat tersebut dapat berguna sebagai pengamatan awal. Namun, kalimat itu belum otomatis menjadi objek penelitian yang dapat dihitung secara konsisten.

Penelitian membutuhkan sesuatu yang lebih jelas: **event** atau kejadian yang memiliki definisi, waktu, identitas, dan aturan pengukuran.

Perubahan cara berpikirnya adalah:

> Dari "Saya melihat sinyal" menjadi "Saya dapat mendefinisikan kejadian ini sehingga orang lain dapat mengukurnya dengan aturan yang sama."

Dalam TEKB, event bukan sekadar tanda visual pada grafik. Event adalah objek penelitian yang harus dapat:

- Didefinisikan secara eksplisit.
- Dideteksi menggunakan informasi yang tersedia saat itu.
- Diberi waktu dan identitas.
- Dihubungkan dengan aturan entry.
- Diukur hasilnya.
- Ditelusuri kembali melalui audit trail.

---

## 7.1. Apa Itu Event?

### Pengertian Event

**Event** adalah satu kejadian yang memenuhi definisi tertentu dan memiliki identitas serta waktu terjadinya.

Contohnya:

> "SAMSON terdeteksi pada bar T."

Pernyataan tersebut masih perlu dijelaskan lebih lanjut. Apa yang dimaksud SAMSON? Berapa ambang volumenya? Data pembandingnya berasal dari periode mana? Kapan event dianggap benar-benar terdeteksi?

Event yang baik harus dapat dijawab dengan aturan yang tidak bergantung pada perasaan peneliti.

Misalnya, event volume dapat didefinisikan menggunakan Relative Volume:

> RV_t = V_t ÷ V_baseline,t

Dengan:

- V_t = volume pada bar atau hari ke-t.
- V_baseline,t = volume pembanding yang dihitung hanya dari data yang tersedia sebelum t.
- RV_t = volume relatif terhadap kondisi normal sebelumnya.

Contoh aturan:

> Event terjadi apabila RV_t ≥ 3.

Artinya, volume pada bar t setidaknya tiga kali lebih besar daripada baseline yang telah ditentukan.

Namun, aturan lengkap harus tetap menjelaskan:

- Baseline menggunakan berapa bar sebelumnya?
- Apakah baseline bersifat slot-aware?
- Bagaimana menangani volume nol atau data hilang?
- Apakah event yang berdekatan digabung atau dipisahkan?
- Apakah event hanya berlaku pada instrumen tertentu?
- Apakah event harus memenuhi syarat tambahan?

### Contoh Event SAMSON

Misalnya definisi penelitian menyatakan:

> SAMSON adalah event ketika volume saat ini lebih besar atau sama dengan 3 kali rata-rata volume 20 bar valid sebelumnya.

Secara formal:

> RV_t = V_t ÷ Mean(V_{t-20}, ..., V_{t-1})

Event terjadi jika:

> RV_t ≥ 3

Contoh:

- Volume bar saat ini: 300.000 saham.
- Rata-rata volume 20 bar sebelumnya: 90.000 saham.

Maka:

> RV_t = 300.000 ÷ 90.000 = 3,33

Karena 3,33 ≥ 3, event terdeteksi.

Namun, event tersebut hanya menyatakan bahwa volume relatif tinggi. Event tersebut belum menyatakan:

- Harga pasti naik.
- Harga pasti turun.
- Ada akumulasi institusi.
- Ada sinyal BUY.
- Ada peluang profit.
- Event tersebut memiliki hubungan sebab-akibat dengan return berikutnya.

Dalam TEKB, event adalah objek yang akan diuji, bukan kesimpulan yang sudah diterima.

### Sinyal Visual dan Event Terstruktur

Ada perbedaan antara sinyal visual dan event terstruktur.

#### Sinyal Visual

Sinyal visual biasanya berupa pengamatan seperti:

- "Candle ini terlihat besar."
- "Volume tampak tidak normal."
- "Harga sepertinya menembus resistance."
- "Ada tekanan jual."
- "Pola ini kelihatan bullish."

Sinyal visual dapat menjadi sumber ide, tetapi sering kali memiliki kelemahan:

- Definisinya tidak pasti.
- Dua orang dapat menafsirkannya secara berbeda.
- Waktu deteksinya tidak jelas.
- Tidak mudah diulang.
- Tidak mudah diaudit.
- Sering kali baru terlihat jelas setelah hasil diketahui.

#### Event Terstruktur

Event terstruktur memiliki aturan yang lebih tegas, misalnya:

- Instrumen: ABCD.
- Bar: 2026-09-10 10:35.
- RV: 4,20.
- Threshold: RV≥3.
- Baseline: 20 bar sebelumnya.
- Status: valid.
- Event ID: EVT-ABCD-20260910-1035-001.

Event tersebut dapat diproses oleh komputer maupun diperiksa oleh manusia.

#### Perbandingan

| Sinyal Visual | Event Terstruktur |
|---|---|
| "Volume terlihat besar" | RV≥3 berdasarkan baseline 20 bar sebelumnya |
| "Candle terlihat kuat" | Definisi body, range, dan posisi close ditentukan |
| Waktu tidak selalu jelas | Timestamp ditentukan |
| Sulit diulang | Dapat direplikasi |
| Sulit diaudit | Memiliki ID dan metadata |
| Mudah dipengaruhi hindsight | Harus menggunakan informasi point-in-time |

### Event Bukan Keputusan Trading

Event dan keputusan trading adalah dua hal yang berbeda.

Contoh:

> Event terdeteksi → penelitian mengukur return berikutnya

Tidak otomatis menjadi:

> Event terdeteksi → langsung BUY

Event dapat digunakan untuk:

- Mengukur return berikutnya.
- Mengukur MAE dan MFE.
- Membandingkan dengan B0.
- Menguji distribusi.
- Menguji kondisi tertentu.
- Menjadi perhatian untuk penelitian lanjutan.

Dengan demikian, TEKB tidak menganggap setiap event sebagai perintah transaksi.

---

## 7.2. Mengapa Waktu Harus Ditulis Secara Eksplisit?

### Waktu Menentukan Apa yang Boleh Diketahui

Dalam penelitian trading, waktu bukan sekadar informasi tambahan. Waktu menentukan batas pengetahuan yang tersedia.

Sebuah event dapat terlihat sederhana, tetapi sebenarnya melibatkan beberapa waktu berbeda:

- Waktu deteksi.
- Waktu konfirmasi.
- Waktu ketersediaan informasi.
- Waktu entry.
- Waktu pengukuran hasil.
- Waktu evaluasi.

Jika semua waktu tersebut dicampur, penelitian dapat secara tidak sengaja menggunakan informasi masa depan.

### 1. Waktu Deteksi

**Detection time** adalah waktu ketika kondisi event pertama kali memenuhi definisi penelitian.

Contoh:

> Pada pukul 10:35, volume bar selesai dan RV dihitung sebesar 4,20. Karena RV≥3, event terdeteksi.

Waktu deteksi harus mengikuti struktur data yang digunakan.

Pada data candle, event biasanya baru dapat dinyatakan terdeteksi setelah candle selesai jika definisinya menggunakan:

- High.
- Low.
- Close.
- Volume total.
- Range penuh.
- Posisi penutupan.

Misalnya, jika event menggunakan volume total satu candle lima menit, maka volume tersebut belum diketahui secara lengkap sebelum candle selesai.

### 2. Waktu Konfirmasi

**Confirmation time** adalah waktu ketika syarat tambahan yang diperlukan untuk menyatakan event valid telah terpenuhi.

Contoh:

- Volume tinggi terdeteksi pada bar T.
- Konfirmasi breakout terjadi pada bar T+1.
- Event penelitian baru dianggap lengkap setelah konfirmasi T+1.

Tidak semua penelitian membutuhkan konfirmasi. Jika tidak ada konfirmasi, bagian ini dapat diberi status tidak berlaku.

Yang penting, waktu konfirmasi tidak boleh ditulis seolah-olah terjadi bersamaan dengan event jika sebenarnya baru terjadi kemudian.

### 3. Waktu Ketersediaan Informasi

**Availability time** adalah waktu ketika informasi yang digunakan benar-benar tersedia dan dapat diakses untuk keputusan.

Contohnya:

- Candle selesai pada pukul 10:35:00.
- Data baru diterima sistem pada pukul 10:35:02.
- Informasi dianggap tersedia pada waktu yang ditentukan oleh kontrak penelitian.

Perbedaan ini penting terutama untuk:

- Data intraday.
- Data yang memiliki keterlambatan.
- Data laporan keuangan.
- Data fundamental.
- Data yang direvisi.
- Data dari sumber eksternal.

Dalam penelitian OHLCV sederhana, availability time mungkin disamakan dengan waktu penutupan bar berdasarkan asumsi sistem. Namun, asumsi tersebut harus ditulis, bukan dibiarkan tersembunyi.

### 4. Waktu Entry

**Entry time** adalah waktu ketika posisi penelitian dianggap dimulai.

Dalam TEKB, waktu entry harus ditentukan secara ex ante.

Contohnya:

> Event pada bar T selesai, lalu entry dilakukan pada open bar valid berikutnya.

Jika event terdeteksi pada Senin, entry dapat ditentukan pada open Selasa, bukan pada harga yang dipilih secara retrospektif.

### 5. Waktu Pengukuran Hasil

**Measurement time** adalah periode ketika hasil mulai dihitung.

Misalnya:

- Entry pada open T+1.
- Horizon penelitian tiga bar.
- Return diukur dari harga entry sampai close T+3.

Maka rumusnya:

> R_+3 = (C_T+3 − P_entry) ÷ P_entry

Atau dalam bentuk log return:

> r_T+3 = ln(C_T+3 ÷ P_entry)

Pengukuran hasil tidak boleh dimulai dari waktu yang tidak konsisten antara B1 dan B0.

### 6. Waktu Evaluasi

**Evaluation time** adalah waktu ketika hasil event diproses oleh evaluation engine.

Misalnya, engine mengevaluasi:

- Apakah stop-loss tersentuh.
- Apakah take-profit tersentuh.
- Apakah posisi mengalami timeout.
- Apakah horizon tidak lengkap.
- Apakah terjadi kondisi ambigu intrabar.
- Berapa hasil gross dan net.

Waktu evaluasi harus mengikuti aturan yang sama untuk B1 dan B0.

### Contoh Urutan Waktu

| Tahap | Waktu | Keterangan |
|---|---|---|
| Event candle mulai | 10:30 | Candle lima menit dimulai |
| Event candle selesai | 10:35 | Volume dan close lengkap |
| Event terdeteksi | 10:35 | RV memenuhi threshold |
| Informasi tersedia | 10:35 atau sesuai asumsi sistem | Data dapat digunakan |
| Entry | 10:35 atau open bar valid berikutnya | Sesuai kontrak penelitian |
| Pengukuran | Setelah entry | Return dan MAE/MFE dihitung |
| Evaluasi | Setelah horizon atau exit | Engine menentukan hasil akhir |

### Mengapa Pemisahan Ini Penting?

Tanpa pemisahan waktu, peneliti dapat melakukan kesalahan seperti:

- Menggunakan close candle sebelum candle selesai.
- Menganggap konfirmasi yang baru terjadi kemudian sudah diketahui sejak event awal.
- Menggunakan harga entry yang tidak tersedia.
- Menghitung return dari waktu yang berbeda.
- Menggunakan data hasil untuk mengubah status event.
- Menggabungkan event time dan evaluation time.

Prinsip TEKB:

> Setiap informasi harus memiliki waktu kapan informasi itu boleh digunakan.

---

## 7.3. Event Timestamp versus Harga Entry

### Tiga Harga yang Berbeda

Dalam penelitian trading, setidaknya terdapat tiga konsep harga yang perlu dibedakan:

- Signal close price
- Entry price raw
- Execution price assumed

Ketiganya dapat memiliki nilai yang berbeda.

### 1. Signal Close Price

**Signal close price** adalah harga penutupan bar ketika event atau sinyal terdeteksi.

Misalnya:

- Event terdeteksi pada bar T.
- Harga penutupan bar T = 100.

Maka:

> C_T = 100

Harga ini menggambarkan kondisi pasar pada saat event selesai. Namun, harga tersebut belum tentu merupakan harga entry yang dapat digunakan.

### 2. Entry Price Raw

**Entry price raw** adalah harga awal yang ditentukan oleh aturan entry sebelum penyesuaian asumsi eksekusi.

Contoh:

> Entry dilakukan pada open bar berikutnya.

Jika open bar berikutnya adalah 102, maka:

> P_entry, raw = 102

Harga entry raw dapat berbeda dari signal close:

> C_T = 100

> P_entry, raw = 102

Perbedaan tersebut dapat terjadi karena:

- Gap.
- Perubahan harga antarbar.
- Pasar dibuka pada harga berbeda.
- Bar berikutnya tidak langsung tersedia.
- Perubahan sesi perdagangan.

### 3. Execution Price Assumed

**Execution price assumed** adalah harga yang digunakan dalam simulasi setelah menerapkan aturan eksekusi penelitian.

Harga ini dapat mempertimbangkan:

- Gap.
- Slippage.
- Biaya transaksi.
- Friction.
- Batas harga.
- Ketersediaan likuiditas.
- Aturan eksekusi tertentu.

Misalnya:

- Entry raw = 102.
- Slippage asumsi = 0,2%.
- Harga eksekusi simulasi = 102,204.

Maka harga yang digunakan untuk menghitung return net dapat berbeda dari entry raw.

Namun, jika penelitian hanya menggunakan entry raw tanpa slippage, hal itu juga diperbolehkan selama dinyatakan sebagai asumsi penelitian.

### Mengapa Ketiganya Tidak Boleh Disamakan?

Jika signal close, entry raw, dan execution price assumed disamakan secara otomatis, peneliti dapat menghasilkan simulasi yang tidak realistis.

Contoh:

- Close event = 100.
- Open bar berikutnya = 105.
- Peneliti tetap menggunakan 100 sebagai harga entry.

Jika aturan entry sebenarnya adalah open bar berikutnya, penggunaan 100 akan memberikan harga yang tidak tersedia setelah event selesai.

Hal ini dapat membuat hasil tampak lebih baik daripada yang mungkin diperoleh.

### Contoh Tabel

| Komponen | Nilai | Arti |
|---|---|---|
| Signal close price | 100 | Close bar event |
| Entry price raw | 105 | Open bar berikutnya |
| Execution price assumed | 105,21 | Setelah asumsi slippage |
| Return measurement base | 105,21 | Jika penelitian menggunakan execution price |

### Prinsip TEKB

Peneliti harus menyatakan dengan jelas:

- Harga mana yang menandai event.
- Harga mana yang menjadi dasar entry.
- Harga mana yang digunakan untuk evaluasi.
- Apakah biaya dan slippage dimasukkan.
- Apakah harga entry dapat benar-benar tersedia pada waktu yang ditentukan.

Dengan demikian, pembaca dapat membedakan antara:

> "Harga ketika sinyal muncul"

dan:

> "Harga ketika posisi dianggap masuk."

---

## 7.4. Entry pada Bar Berikutnya

### Mengapa TEKB Menggunakan NEXT_VALID_BAR_OPEN?

Dalam banyak penelitian berbasis candle, TEKB menggunakan aturan:

> Event pada bar T selesai, lalu entry dilakukan pada open bar valid berikutnya.

Aturan ini dapat ditulis sebagai:

Signal close pada bar T
↓
NEXT_VALID_BAR_OPEN
↓
Entry pada open bar valid berikutnya


Aturan tersebut membantu menjaga urutan sebab-akibat operasional dalam simulasi.

Jika event menggunakan informasi dari keseluruhan candle T, termasuk:

- High.
- Low.
- Close.
- Volume.
- Range.
- Posisi close.

Maka informasi tersebut baru lengkap setelah candle T selesai. Menggunakan harga close T sebagai entry dapat menimbulkan asumsi bahwa trader selalu dapat mengeksekusi tepat pada harga penutupan setelah mengetahui seluruh informasi candle tersebut.

### Mengapa Same-Bar-Close Tidak Digunakan?

Entry pada **same-bar-close** dapat menjadi tidak realistis apabila sinyal ditentukan menggunakan informasi yang baru diketahui saat candle selesai.

Contohnya:

> "Jika candle T memiliki volume tinggi dan close kuat, beli pada close T."

Masalahnya adalah close T baru diketahui ketika candle selesai. Untuk dapat membeli tepat pada close tersebut, penelitian harus memiliki asumsi eksekusi yang sangat spesifik dan dapat dipertanggungjawabkan.

Jika tidak ada mekanisme eksekusi yang mendukung, maka penggunaan close event sebagai harga entry dapat menghasilkan bias.

Dengan menggunakan open bar berikutnya, penelitian lebih mudah menjelaskan urutannya:

1. Candle T selesai.
2. Event dihitung.
3. Event dinyatakan valid.
4. Informasi tersedia.
5. Order diasumsikan masuk pada open bar valid berikutnya.

### Contoh

Misalkan:

| Bar | Close | Open Berikutnya |
|---|---|---|
| T | 100 | 102 |

Event terdeteksi pada close bar T.

Jika aturan entry adalah NEXT_VALID_BAR_OPEN, maka:

> P_entry = 102

Bukan:

> P_entry = 100

Perbedaan dua poin tersebut penting karena return dihitung berdasarkan harga entry yang benar-benar ditetapkan oleh aturan penelitian.

### Apa yang Dimaksud Bar Valid Berikutnya?

Bar berikutnya tidak selalu berarti bar dengan timestamp numerik paling dekat. Bar berikutnya harus memenuhi aturan validitas data dan kalender perdagangan.

Contohnya:

- Bar berikutnya tersedia.
- Bar tidak rusak.
- Bar tidak ditandai invalid.
- Bar berada dalam sesi yang diizinkan.
- Bar tidak berasal dari periode yang dikecualikan.
- Instrumen masih dapat diperdagangkan.
- Data open tersedia.

Karena itu, TEKB menggunakan istilah:

> NEXT_VALID_BAR_OPEN

bukan sekadar "open bar berikutnya" tanpa definisi.

### Market Break dan Next Valid Bar

Pasar dapat mengalami jeda atau market break, misalnya:

- Istirahat sesi siang.
- Pergantian sesi.
- Hari libur.
- Akhir pekan.
- Penghentian perdagangan.
- Suspensi.
- Gangguan data.
- Perubahan jadwal perdagangan.

Jika event terjadi sebelum jeda, bar berikutnya secara waktu kalender mungkin baru tersedia beberapa jam atau beberapa hari kemudian.

Contoh:

- Event terdeteksi Jumat sore.
- Bar valid berikutnya baru tersedia Senin pagi.
- Entry dilakukan pada open Senin, bukan pada harga fiktif selama akhir pekan.

Aturan tersebut harus ditulis secara eksplisit agar tidak terjadi asumsi bahwa perdagangan selalu berlangsung tanpa jeda.

### Kapan Entry Tidak Dapat Dilakukan?

Entry dapat dinyatakan tidak dapat dilakukan apabila:

- Tidak ada bar valid berikutnya.
- Instrumen telah disuspensi.
- Data open hilang.
- Instrumen keluar dari universe sebelum entry.
- Aturan penelitian melarang entry pada sesi berikutnya.
- Harga eksekusi tidak dapat ditentukan berdasarkan kontrak.
- Event baru diketahui setelah kesempatan entry berlalu.

Dalam kondisi tersebut, jangan memaksakan harga entry. Gunakan status yang sesuai, misalnya:

- NO_MATCH_FOUND untuk masalah pasangan B0.
- INVALIDATED untuk event yang melanggar validitas.
- Status khusus seperti ENTRY_UNAVAILABLE jika digunakan dalam skema penelitian.

### Prinsip Utama

> Entry harus mengikuti urutan informasi dan aturan eksekusi, bukan mengikuti titik harga yang terlihat paling menguntungkan pada grafik.

---

## 7.5. Entry Gap

### Apa Itu Entry Gap?

**Entry gap** adalah selisih antara harga penutupan bar sinyal dan harga pembukaan bar entry.

Rumus sederhananya:

> Gap_raw = P_entry, raw − C_T

Dalam bentuk persentase:

> Gap_% = (P_entry, raw − C_T) ÷ C_T × 100%

Contoh:

- Signal close = 100.
- Entry open = 105.

Maka:

> Gap_raw = 105 − 100 = 5

> Gap_% = (105 − 100) ÷ 100 × 100% = 5%

Artinya, harga entry berada 5% di atas harga penutupan sinyal.

### Gap Positif dan Gap Negatif

#### Gap Positif

Entry open lebih tinggi daripada signal close.

Contoh:

- Close sinyal = 100.
- Open entry = 103.

> Gap_% = +3%

Untuk posisi long, gap positif dapat membuat harga entry lebih mahal dan mengurangi ruang keuntungan potensial.

#### Gap Negatif

Entry open lebih rendah daripada signal close.

Contoh:

- Close sinyal = 100.
- Open entry = 97.

> Gap_% = −3%

Untuk posisi long, gap negatif dapat membuat entry lebih murah, tetapi juga dapat menunjukkan perubahan kondisi pasar yang penting.

### Mengapa Gap Tidak Boleh Dihapus?

Peneliti mungkin tergoda untuk menghapus event dengan gap besar karena dianggap tidak realistis atau mengganggu hasil.

Namun, gap besar adalah bagian dari perilaku pasar yang sebenarnya. Menghapusnya tanpa aturan ex ante dapat menyebabkan:

- Hasil menjadi terlalu optimistis.
- Risiko eksekusi terlihat lebih kecil.
- Event buruk tidak lagi masuk sampel.
- Distribusi return berubah.
- Strategi terlihat lebih stabil daripada kenyataannya.

Jika gap besar memang tidak dapat diperdagangkan berdasarkan mandat penelitian, aturan pengecualian boleh dibuat. Namun, aturan tersebut harus:

- Ditentukan sebelum pengujian.
- Diterapkan konsisten pada seluruh event.
- Dicatat secara transparan.
- Tidak dibuat hanya untuk menghilangkan hasil buruk.
- Memiliki alasan operasional yang jelas.

### Contoh Dampak Gap

Misalkan terdapat event dengan:

- Close sinyal = 100.
- Harga maksimum tiga hari berikutnya = 106.

#### Jika entry dihitung dari close sinyal

> R = (106 − 100) ÷ 100 = 6%

#### Jika entry sebenarnya pada open berikutnya = 104

> R = (106 − 104) ÷ 104 ≈ 1,92%

Hasilnya sangat berbeda.

Jika peneliti menggunakan 100 sebagai harga entry padahal aturan menyatakan entry pada open berikutnya, keuntungan akan terlihat jauh lebih besar.

### included_in_research dan actionable_live

TEKB membedakan dua konsep penting:

#### 1. included_in_research

Artinya event tetap dimasukkan ke dalam penelitian dan hasilnya diukur sesuai aturan yang telah ditentukan.

Misalnya:

- Gap sebesar 6%.
- Harga entry tersedia.
- Event memenuhi seluruh definisi.
- Tidak ada alasan metodologis untuk mengeluarkannya.
- Event tersebut tetap dihitung meskipun hasilnya kurang menarik.

#### 2. actionable_live

Artinya event dinilai dapat ditindaklanjuti dalam kondisi operasional nyata berdasarkan batasan yang telah ditentukan.

Contohnya, penelitian dapat memiliki aturan:

- Gap maksimum 2%.
- Likuiditas minimum tertentu.
- Slippage maksimum tertentu.
- Entry harus tersedia dalam jangka waktu tertentu.

Jika gap event sebesar 6%, event mungkin:

- Tetap included_in_research = true.
- Tetapi actionable_live = false.

Kedua status tersebut menjawab pertanyaan yang berbeda.

| Status | Pertanyaan yang Dijawab |
|---|---|
| included_in_research | Apakah event ini termasuk dalam analisis empiris? |
| actionable_live | Apakah event ini dapat ditindaklanjuti secara operasional saat ini? |

### Mengapa Pemisahan Ini Penting?

Jika semua event yang tidak nyaman langsung dihapus dari penelitian, hasil empiris akan bias.

Sebaliknya, jika seluruh event dianggap otomatis dapat diperdagangkan, hasil penelitian dapat terlalu jauh dari kenyataan operasional.

Pemisahan ini memungkinkan TEKB berkata:

> "Event ini memang bagian dari distribusi historis, tetapi berdasarkan batas eksekusi yang ditentukan, event ini tidak dianggap actionable untuk penggunaan live."

Itu lebih jujur daripada menghapus event dari data atau menyebutnya sebagai peluang trading yang siap digunakan.

### Contoh Tabel Gap

| Event | Signal Close | Entry Open | Gap | Included in Research | Actionable Live |
|---|---|---|---|---|---|
| EVT-01 | 100 | 101 | +1% | Ya | Ya |
| EVT-02 | 100 | 103 | +3% | Ya | Tergantung batas |
| EVT-03 | 100 | 108 | +8% | Ya | Tidak |
| EVT-04 | 100 | 98 | −2% | Ya | Ya |

Status tersebut harus mengikuti aturan yang telah ditentukan, bukan penilaian subjektif setelah melihat hasil.

---

## 7.6. Identitas Event dan Audit Trail

### Mengapa Event Memerlukan Identitas?

Jika penelitian hanya menyimpan kalimat:

> "Pada bulan Maret ada beberapa sinyal volume tinggi."

maka hasilnya sulit diperiksa ulang.

Peneliti perlu mengetahui:

- Sinyal yang mana?
- Terjadi kapan?
- Pada instrumen apa?
- Menggunakan aturan versi berapa?
- Berapa nilai indikatornya?
- Bagaimana harga entry ditentukan?
- Apa hasil akhirnya?
- Apakah event valid?
- Apakah event memiliki pasangan B0?
- Apakah event mengalami gap?
- Apakah horizon lengkap?

Karena itu, setiap event harus memiliki identitas unik.

### Event ID

**Event ID** adalah identitas unik untuk setiap event penelitian.

Contoh:

> EVT-ABCD-20260910-1035-001

Komponennya dapat berarti:

- EVT = event.
- ABCD = instrumen.
- 20260910 = tanggal event.
- 1035 = waktu event.
- 001 = nomor urut.

Format Event ID dapat berbeda sesuai kebutuhan sistem. Yang penting, ID tersebut:

- Unik.
- Stabil.
- Tidak berubah hanya karena hasil event berubah.
- Dapat digunakan untuk menghubungkan tabel penelitian.

### Informasi Minimum Event

Sebuah event setidaknya perlu memiliki beberapa metadata berikut:

| Komponen | Contoh |
|---|---|
| Event ID | EVT-ABCD-20260910-1035-001 |
| Instrumen | ABCD |
| Event timestamp | 2026-09-10 10:35 |
| Timezone | Asia/Jakarta |
| Event type | RV_EXTREME |
| Aturan pemicu | RV≥3 |
| Nilai RV | 4,20 |
| Baseline version | RV_BASELINE_V1.0 |
| Signal close | 100 |
| Entry rule | NEXT_VALID_BAR_OPEN |
| Entry timestamp | 2026-09-10 10:40 |
| Entry price raw | 102 |
| Execution assumption | Raw open, slippage 0 |
| Gap | +2% |
| Horizon | 3 bar |
| Status event | Valid |
| included_in_research | True |
| actionable_live | True/False |
| Definition version | EVENT_SPEC_V1.0 |
| Research batch ID | BATCH-2026-001 |

### Hubungan Event dengan Hasil

Event tidak boleh berdiri sendiri tanpa hubungan ke hasil evaluasi.

Satu event dapat dihubungkan dengan:

- Harga entry.
- Harga keluar.
- Return.
- MAE.
- MFE.
- ATR entry.
- Hasil kandidat SL/TP.
- Status evaluasi.
- Pasangan B0.
- Hasil bootstrap atau agregasi penelitian.

Contoh struktur sederhana:

Event
├── Entry
├── B0 Match
├── Return
├── MAE
├── MFE
├── ATR
├── Candidate Evaluation
└── Final Status

Dengan struktur ini, peneliti dapat menelusuri perjalanan satu event dari awal hingga akhir.

### Contoh Record Event

event_id: EVT-ABCD-20260910-1035-001
instrument: ABCD
event_type: RV_EXTREME
event_timestamp: 2026-09-10T10:35:00+07:00
availability_timestamp: 2026-09-10T10:35:00+07:00
event_definition_version: EVENT_SPEC_V1.0
rv_value: 4.20
rv_threshold: 3.00
baseline_definition: prior_20_valid_bars
signal_close_price: 100.00
entry_rule: NEXT_VALID_BAR_OPEN
entry_timestamp: 2026-09-10T10:40:00+07:00
entry_price_raw: 102.00
execution_price_assumed: 102.00
entry_gap_pct: 2.00
horizon_bars: 3
included_in_research: true
actionable_live: true
event_status: VALID
research_batch_id: BATCH-2026-001


Record tersebut belum berisi hasil return atau MAE/MFE karena hasil baru dapat dihitung setelah periode evaluasi tersedia.

### Audit Trail

**Audit trail** adalah catatan yang memungkinkan seseorang memeriksa bagaimana event dan hasil penelitian dihasilkan.

Audit trail yang baik dapat menjawab:

- Data sumber apa yang digunakan?
- Versi definisi event apa yang digunakan?
- Nilai apa yang menyebabkan event terdeteksi?
- Kapan event dianggap tersedia?
- Bagaimana entry ditentukan?
- Mengapa harga entry memiliki nilai tertentu?
- Apakah terdapat gap?
- Apakah event dinyatakan valid atau invalid?
- Bagaimana B0 dipilih?
- Bagaimana return, MAE, dan MFE dihitung?
- Evaluation engine versi berapa yang digunakan?
- Apakah event masuk dalam hasil agregat?
- Apakah event dikeluarkan, dan jika ya, apa alasannya?

### Versi Definisi Harus Dicatat

Definisi event dapat berubah selama pengembangan penelitian. Misalnya:

- EVENT_SPEC_V1.0 menggunakan RV≥3.
- EVENT_SPEC_V1.1 mengubah baseline.
- EVENT_SPEC_V2.0 menambahkan aturan declustering.

Perubahan versi tidak boleh membuat hasil lama menjadi tidak dapat dibedakan dari hasil baru.

Setiap hasil harus menyebutkan definisi yang digunakan.

Metadata yang berguna antara lain:

- hypothesis_id
- research_batch_id
- event_definition_version_id
- entry_definition_version_id
- b0_selection_rule_version
- mae_mfe_definition_version_id
- atr_definition_version_id
- evaluation_engine_version_id
- candidate_grid_version_id
- multiple_testing_family_id

### Mengapa Audit Trail Penting?

Audit trail bukan sekadar administrasi. Ia melindungi penelitian dari beberapa masalah:

- Kesalahan perhitungan.
- Perubahan aturan yang tidak tercatat.
- Penggunaan data masa depan.
- Event ganda.
- Event yang hilang.
- Entry yang tidak konsisten.
- Perbedaan perlakuan antara B1 dan B0.
- Kesulitan mengulang penelitian.
- Kesulitan menjelaskan mengapa hasil berubah.

Tanpa audit trail, hasil penelitian mungkin terlihat meyakinkan, tetapi sulit dibuktikan.

---

## Contoh Alur Lengkap Event TEKB

Berikut contoh sederhana dari sinyal hingga event yang dapat diukur.

### Langkah 1 — Kondisi Terdeteksi

Pada bar T:

- Volume = 300.000.
- Baseline volume sebelumnya = 90.000.
- RV = 3,33.

Karena RV≥3, kondisi memenuhi definisi event.

### Langkah 2 — Event Diberi Identitas

Event ID: EVT-ABCD-20260910-1035-001
Event type: RV_EXTREME
RV: 3.33
Status: VALID


### Langkah 3 — Harga Sinyal Dicatat

Signal close = 100.

Harga ini hanya menjadi catatan kondisi saat event selesai.

### Langkah 4 — Entry Ditentukan

Aturan:

> NEXT_VALID_BAR_OPEN

Open bar berikutnya = 102.

Entry raw = 102.

### Langkah 5 — Gap Dihitung

> Gap_% = (102 − 100) ÷ 100 × 100% = 2%

Event memiliki gap positif sebesar 2%.

### Langkah 6 — Event Dimasukkan ke Penelitian

Jika tidak ada aturan pengecualian yang berlaku:

> included_in_research = true

Jika batas actionable live maksimum adalah 1%, maka:

> actionable_live = false

Keduanya tetap dapat berbeda.

### Langkah 7 — Hasil Diukur

Misalnya:

- Close pada akhir horizon = 106.
- Entry = 102.
- Horizon = 3 bar.

Maka:

> R_+3 = (106 − 102) ÷ 102 × 100%

> R_+3 ≈ 3,92%

MAE dan MFE kemudian dihitung berdasarkan low dan high selama jendela evaluasi.

### Langkah 8 — Event Dihubungkan dengan B0

Event B1 dipasangkan dengan B0 sesuai aturan matching yang telah ditentukan.

Perbandingan tidak hanya melihat apakah B1 menghasilkan return positif, tetapi apakah hasil B1 berbeda dari baseline yang adil.

---

## Kesalahan Umum dalam Mendefinisikan Event

### 1. Event Baru Didefinisikan Setelah Melihat Hasil

Contoh:

> "Event adalah volume tinggi yang ternyata diikuti kenaikan."

Ini bukan definisi event yang bebas dari hasil masa depan. Event telah dipilih berdasarkan outcome.

Definisi yang lebih benar:

> "Event adalah RV≥3 berdasarkan baseline 20 bar sebelumnya. Return setelah event diukur secara terpisah."

### 2. Menggunakan Informasi yang Belum Lengkap

Contoh:

Event ditentukan berdasarkan volume total candle, tetapi event dianggap sudah diketahui sebelum candle selesai.

Jika volume total belum lengkap, event belum dapat dinyatakan terdeteksi secara final.

### 3. Menyamakan Close Sinyal dengan Entry

Close sinyal adalah harga ketika event selesai. Entry harus mengikuti aturan eksekusi yang telah ditentukan.

### 4. Menghapus Gap Besar Setelah Melihat Hasil

Gap besar tidak boleh dikeluarkan hanya karena membuat hasil kurang bagus. Jika ada batas gap, batas tersebut harus ditentukan sebelum pengujian.

### 5. Tidak Mencatat Event yang Gagal

Event invalid, tidak memiliki bar berikutnya, atau memiliki data tidak lengkap tetap perlu dicatat dengan status yang sesuai.

### 6. Tidak Membedakan Event dan Keputusan

Event bukan otomatis BUY atau SELL. Event adalah kondisi yang akan diuji untuk mengetahui apakah memiliki informasi yang berguna.

---

## Ringkasan Bab 7

Event adalah jembatan antara pengamatan visual dan penelitian berbasis data.

Sinyal seperti "volume besar" atau "candle kuat" belum cukup untuk menjadi objek penelitian. Sinyal tersebut harus diubah menjadi event yang memiliki:

- Definisi yang jelas.
- Timestamp.
- Instrumen.
- Aturan pemicu.
- Harga sinyal.
- Aturan entry.
- Harga entry.
- Informasi gap.
- Status validitas.
- Hubungan dengan hasil.
- Versi metodologi.
- Audit trail.

### Pelajaran Utama

- Event adalah kejadian yang memiliki definisi, identitas, dan waktu.
- Sinyal visual harus diubah menjadi aturan yang dapat diulang dan diaudit.
- Waktu deteksi, konfirmasi, availability, entry, pengukuran, dan evaluasi perlu dibedakan.
- Signal close price tidak sama dengan entry price.
- Entry harus mengikuti aturan yang dapat dijalankan, seperti NEXT_VALID_BAR_OPEN.
- Gap adalah bagian dari realitas pasar dan tidak boleh dihapus secara sembarangan.
- included_in_research berbeda dari actionable_live.
- Setiap event harus memiliki ID dan dapat ditelusuri sampai hasil akhirnya.
- Event bukan keputusan BUY atau SELL; event adalah objek yang diuji.
- Penelitian yang baik tidak hanya menyimpan hasil, tetapi juga menyimpan bagaimana hasil tersebut diperoleh.

> Sinyal menjadi pengetahuan penelitian ketika ia memiliki definisi yang jelas, waktu yang benar, harga yang dapat dipertanggungjawabkan, dan jejak audit yang lengkap.

---

## Pertanyaan Refleksi

1. Apa perbedaan antara sinyal visual dan event terstruktur?
2. Mengapa waktu deteksi, konfirmasi, dan availability perlu dibedakan?
3. Apa perbedaan antara signal close price, entry price raw, dan execution price assumed?
4. Mengapa TEKB menggunakan NEXT_VALID_BAR_OPEN?
5. Mengapa gap tidak boleh dihapus sembarangan?
6. Apa perbedaan antara included_in_research dan actionable_live?
7. Mengapa setiap event memerlukan Event ID?
8. Apa yang dimaksud dengan audit trail?

---

<div align="center">

[← Bab Sebelumnya](/posts/bab-06-memahami-samson/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Bab Selanjutnya →](/posts/bab-08-b0-pembanding-adil/)

</div>