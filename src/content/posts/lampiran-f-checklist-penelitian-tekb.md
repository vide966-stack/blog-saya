---
title: "Lampiran F — Checklist Penelitian TEKB"
published: 2026-09-14
description: "Checklist lengkap penelitian TEKB dari tahap persiapan hingga keputusan akhir, untuk memastikan penelitian dilakukan secara tertib, transparan, dan dapat ditelusuri."
tags: ["lampiran-f", "checklist", "penelitian", "integritas"]
category: "Lampiran"
draft: false
lang: ""
---

## Tujuan Checklist

Checklist ini membantu peneliti memastikan bahwa penelitian TEKB dilakukan secara tertib, transparan, dan tidak mengubah aturan setelah melihat hasil.

Checklist bukan pengganti dokumentasi teknis, kode program, atau audit trail. Fungsinya adalah sebagai pemeriksaan awal untuk menemukan celah metodologis sebelum hasil penelitian dianggap layak dipercaya.

Gunakan tanda berikut:

- ☐ Belum diperiksa
- ☑ Sudah diperiksa dan memenuhi ketentuan
- ⚠️ Perlu perbaikan atau penjelasan
- N/A Tidak berlaku untuk penelitian ini

## A. Sebelum Penelitian

Tahap ini memastikan bahwa penelitian telah memiliki aturan yang jelas sebelum data dianalisis.

| No. | Pertanyaan Pemeriksaan | Status | Catatan/Bukti |
|---|---|---|---|
| A1 | Apakah pertanyaan penelitian sudah jelas dan dapat diuji menggunakan data? | ☐ | |
| A2 | Apakah tujuan penelitian membedakan hubungan empiris dari klaim sebab-akibat? | ☐ | |
| A3 | Apakah sumber data sudah ditentukan dan terdokumentasi? | ☐ | |
| A4 | Apakah data bersifat point-in-time dan tidak menggunakan informasi yang belum tersedia pada saat event? | ☐ | |
| A5 | Apakah aturan pembersihan data telah ditentukan sebelum pengujian? | ☐ | |
| A6 | Apakah definisi event sudah tertulis secara eksplisit? | ☐ | |
| A7 | Apakah aturan validasi event sudah ditentukan? | ☐ | |
| A8 | Apakah aturan entry sudah ditentukan, termasuk waktu dan harga entry? | ☐ | |
| A9 | Apakah aturan menghadapi gap sudah ditentukan? | ☐ | |
| A10 | Apakah B0 sudah ditentukan sebelum melihat hasil penelitian? | ☐ | |
| A11 | Apakah aturan pencocokan B1 dan B0 sudah ditentukan? | ☐ | |
| A12 | Apakah aturan penggunaan ulang pasangan B0 sudah ditentukan? | ☐ | |
| A13 | Apakah horizon penelitian sudah ditentukan dan dibekukan? | ☐ | |
| A14 | Apakah definisi return, MAE, dan MFE sudah ditentukan? | ☐ | |
| A15 | Apakah definisi ATR dan cara normalisasinya sudah ditentukan? | ☐ | |
| A16 | Apakah candidate grid SL/TP atau parameter lain sudah ditentukan sebelum pengujian? | ☐ | |
| A17 | Apakah biaya transaksi, slippage, dan friction ladder sudah ditentukan? | ☐ | |
| A18 | Apakah kriteria evaluasi dan batas praktis sudah ditentukan? | ☐ | |
| A19 | Apakah periode IS dan OOS sudah ditentukan? | ☐ | |
| A20 | Apakah seluruh versi spesifikasi metodologi telah diberi identitas atau version ID? | ☐ | |

### Catatan Tahap A

Penelitian sebaiknya tidak dimulai apabila pertanyaan penelitian, definisi event, entry, B0, horizon, dan candidate grid masih berubah-ubah.

Perubahan aturan setelah hasil terlihat dapat mengubah penelitian dari pengujian hipotesis menjadi pencarian pola yang paling menguntungkan secara retrospektif.

## B. Saat Penelitian Berlangsung

Tahap ini memeriksa apakah pelaksanaan penelitian benar-benar mengikuti kontrak metodologi yang telah ditentukan.

| No. | Pertanyaan Pemeriksaan | Status | Catatan/Bukti |
|---|---|---|---|
| B1 | Apakah prinsip no-look-ahead tetap terjaga pada seluruh proses? | ☐ | |
| B2 | Apakah setiap event dapat ditelusuri kembali ke data sumbernya? | ☐ | |
| B3 | Apakah timestamp event, konfirmasi, availability, dan evaluation dibedakan jika diperlukan? | ☐ | |
| B4 | Apakah data yang digunakan pada saat event benar-benar sudah tersedia pada saat itu? | ☐ | |
| B5 | Apakah event yang invalid dicatat, bukan diam-diam dihapus? | ☐ | |
| B6 | Apakah aturan entry diterapkan secara konsisten pada semua event? | ☐ | |
| B7 | Apakah entry tidak menggunakan harga atau informasi dari masa depan? | ☐ | |
| B8 | Apakah B1 dan B0 menggunakan evaluation engine yang sama? | ☐ | |
| B9 | Apakah B1 dan B0 menggunakan definisi return, MAE, dan MFE yang sama? | ☐ | |
| B10 | Apakah B1 dan B0 dikenakan asumsi biaya dan friction yang sama? | ☐ | |
| B11 | Apakah event yang tidak memperoleh pasangan B0 dicatat sebagai `NO_MATCH_FOUND`? | ☐ | |
| B12 | Apakah event yang memiliki horizon tidak lengkap diberi status `INSUFFICIENT_HORIZON`? | ☐ | |
| B13 | Apakah event dengan data rusak atau aturan yang dilanggar diberi status `INVALIDATED`? | ☐ | |
| B14 | Apakah kasus SL dan TP tersentuh pada candle yang sama diberi status `AMBIGUOUS_INTRABAR` jika tidak dapat dipastikan urutannya? | ☐ | |
| B15 | Apakah `TIMEOUT` dibedakan dari `INSUFFICIENT_HORIZON`? | ☐ | |
| B16 | Apakah hasil mentah disimpan sebelum agregasi atau pembulatan? | ☐ | |
| B17 | Apakah jumlah event, tanggal, instrumen, dan pasangan B0 tercatat? | ☐ | |
| B18 | Apakah proses penelitian menghasilkan audit trail yang dapat diperiksa ulang? | ☐ | |
| B19 | Apakah perubahan teknis selama proses dicatat sebagai perubahan versi? | ☐ | |
| B20 | Apakah tidak ada event atau hasil yang dihapus hanya karena hasilnya tidak sesuai harapan? | ☐ | |

### Catatan Tahap B

Data yang tidak lengkap atau event yang gagal bukan berarti harus dipaksakan menjadi hasil yang valid. Status seperti `NO_MATCH_FOUND`, `INSUFFICIENT_HORIZON`, dan `INVALIDATED` justru membantu menjaga kejujuran penelitian.

Hasil yang tidak dapat dihitung secara sah harus tetap terlihat dalam laporan, bukan disembunyikan dari pembaca.

## C. Sebelum Seleksi Kandidat

Tahap ini memastikan bahwa kandidat yang dibandingkan tidak muncul dari pencarian tanpa batas setelah hasil diketahui.

| No. | Pertanyaan Pemeriksaan | Status | Catatan/Bukti |
|---|---|---|---|
| C1 | Apakah seluruh kandidat berasal dari candidate grid yang telah ditentukan sebelumnya? | ☐ | |
| C2 | Apakah tidak ada parameter baru yang ditambahkan hanya karena hasil awal terlihat menarik? | ☐ | |
| C3 | Apakah seluruh candidate grid memiliki version ID? | ☐ | |
| C4 | Apakah jumlah seluruh kandidat yang diuji tercatat? | ☐ | |
| C5 | Apakah seluruh keluarga pengujian atau multiple-testing family tercatat? | ☐ | |
| C6 | Apakah hubungan antara kandidat, hipotesis, dan research batch dapat ditelusuri? | ☐ | |
| C7 | Apakah pengujian menggunakan B1 dan B0 secara berpasangan jika desainnya paired? | ☐ | |
| C8 | Apakah perbedaan hasil B1 terhadap B0 dihitung secara eksplisit? | ☐ | |
| C9 | Apakah evaluasi gross dan net dipisahkan? | ☐ | |
| C10 | Apakah biaya dan friction diperhitungkan sebelum kandidat dinilai layak? | ☐ | |
| C11 | Apakah hasil worst-case dan best-case dipisahkan? | ☐ | |
| C12 | Apakah kasus ambigu tidak dicampur secara sembarangan dengan hasil yang pasti? | ☐ | |
| C13 | Apakah metode bootstrap sesuai dengan struktur dependensi data? | ☐ | |
| C14 | Apakah unit bootstrap telah ditentukan, misalnya event, tanggal, instrumen, atau blok waktu? | ☐ | |
| C15 | Apakah seed, jumlah replikasi, dan metode bootstrap dicatat? | ☐ | |
| C16 | Apakah ketidakpastian hasil dilaporkan, bukan hanya nilai rata-rata? | ☐ | |
| C17 | Apakah multiple-testing adjustment, seperti BH-FDR jika digunakan, diterapkan sesuai keluarga pengujian? | ☐ | |
| C18 | Apakah kandidat tidak dipilih hanya berdasarkan win rate tertinggi? | ☐ | |
| C19 | Apakah kandidat dinilai berdasarkan keunggulan terhadap B0 dan signifikansi praktis? | ☐ | |
| C20 | Apakah kandidat yang gagal tetap dicatat dan tidak dihilangkan dari laporan seleksi? | ☐ | |

### Catatan Tahap C

Jika peneliti menguji ratusan kombinasi event, horizon, threshold, SL, dan TP, sebagian hasil yang tampak bagus dapat muncul hanya karena kebetulan.

Karena itu, seleksi harus mempertimbangkan:

- Keunggulan terhadap B0.
- Besarnya efek secara praktis.
- Ketidakpastian atau interval hasil.
- Multiple testing.
- Biaya transaksi.
- Robustness.
- Konsistensi pada variasi yang telah ditentukan sebelumnya.

Jika tidak ada kandidat yang memenuhi kriteria, hasil yang benar adalah:

`NO_EDGE_FOUND`

## D. Sebelum OOS

Tahap ini merupakan pemeriksaan terakhir sebelum kandidat diterapkan pada data yang tidak digunakan untuk memilih atau menyetel model.

| No. | Pertanyaan Pemeriksaan | Status | Catatan/Bukti |
|---|---|---|---|
| D1 | Apakah kandidat yang akan diuji OOS sudah dipilih secara final? | ☐ | |
| D2 | Apakah kandidat sudah di-freeze sebelum data OOS dibuka untuk evaluasi? | ☐ | |
| D3 | Apakah definisi event sudah di-freeze? | ☐ | |
| D4 | Apakah aturan entry sudah di-freeze? | ☐ | |
| D5 | Apakah definisi B0 dan aturan matching sudah di-freeze? | ☐ | |
| D6 | Apakah horizon dan definisi return sudah di-freeze? | ☐ | |
| D7 | Apakah definisi MAE, MFE, dan ATR sudah di-freeze? | ☐ | |
| D8 | Apakah candidate grid dan kandidat terpilih sudah di-freeze? | ☐ | |
| D9 | Apakah evaluation engine sudah di-freeze? | ☐ | |
| D10 | Apakah asumsi biaya, slippage, dan friction sudah di-freeze? | ☐ | |
| D11 | Apakah semua versi metodologi telah dicatat dalam freeze manifest? | ☐ | |
| D12 | Apakah `hypothesis_id` telah dicatat? | ☐ | |
| D13 | Apakah `research_batch_id` telah dicatat? | ☐ | |
| D14 | Apakah `candidate_grid_version_id` telah dicatat? | ☐ | |
| D15 | Apakah `entry_definition_version_id` telah dicatat? | ☐ | |
| D16 | Apakah `b0_selection_rule_version` telah dicatat? | ☐ | |
| D17 | Apakah `mae_mfe_definition_version_id` dan `atr_definition_version_id` telah dicatat? | ☐ | |
| D18 | Apakah `evaluation_engine_version_id` telah dicatat? | ☐ | |
| D19 | Apakah `multiple_testing_family_id` telah dicatat? | ☐ | |
| D20 | Apakah data OOS belum pernah digunakan untuk tuning, memilih kandidat, atau mengubah aturan? | ☐ | |
| D21 | Apakah kriteria OOS sama dengan kriteria yang telah ditentukan sebelum OOS? | ☐ | |
| D22 | Apakah prosedur penanganan hasil OOS yang gagal sudah ditentukan? | ☐ | |
| D23 | Apakah laporan OOS akan memisahkan hasil yang benar-benar out-of-sample dari hasil yang telah terpengaruh tuning? | ☐ | |
| D24 | Apakah status akhir akan diberikan secara eksplisit, misalnya `OOS_VALIDATED` atau `OOS_REJECTED`? | ☐ | |

### Catatan Tahap D

OOS bukan tempat untuk memperbaiki kandidat. OOS adalah pemeriksaan terhadap kandidat yang telah dipilih dan dibekukan.

Jika aturan diubah setelah melihat hasil OOS, maka data tersebut tidak lagi dapat disebut sebagai OOS yang bersih untuk versi penelitian tersebut. Statusnya harus dicatat sebagai OOS yang telah digunakan atau terpengaruh tuning.

## E. Pemeriksaan Akhir dan Keputusan Status

Setelah seluruh tahap selesai, tentukan status penelitian berdasarkan bukti yang tersedia.

| Pertanyaan Akhir | Status | Catatan |
|---|---|---|
| Apakah seluruh definisi utama terdokumentasi? | ☐ | |
| Apakah tidak ditemukan pelanggaran no-look-ahead? | ☐ | |
| Apakah B1 dan B0 dibandingkan secara adil? | ☐ | |
| Apakah event dan hasil dapat ditelusuri? | ☐ | |
| Apakah data tidak lengkap diberi status yang benar? | ☐ | |
| Apakah seluruh kandidat berasal dari grid yang telah ditentukan? | ☐ | |
| Apakah multiple testing telah diperhitungkan? | ☐ | |
| Apakah hasil telah mempertimbangkan biaya dan ketidakpastian? | ☐ | |
| Apakah kandidat telah di-freeze sebelum OOS? | ☐ | |
| Apakah OOS dijalankan tanpa tuning? | ☐ | |
| Apakah kriteria OOS diterapkan secara konsisten? | ☐ | |
| Apakah kesimpulan akhir dibatasi sesuai desain penelitian? | ☐ | |

### Status Penelitian

Pilih salah satu status berikut:

- ☐ `RESEARCH_INCOMPLETE` — penelitian belum memenuhi seluruh persyaratan.
- ☐ `RESEARCH_REQUIRES_REVIEW` — terdapat masalah yang perlu diperiksa atau diperbaiki.
- ☐ `NO_EDGE_FOUND` — tidak ditemukan keunggulan yang cukup berdasarkan kriteria yang telah ditentukan.
- ☐ `IS_SELECTED` — kandidat memenuhi kriteria seleksi in-sample.
- ☐ `LOCKED` — seluruh komponen kandidat telah dibekukan sebelum OOS.
- ☐ `OOS_VALIDATED` — kandidat memenuhi kriteria OOS yang telah ditentukan.
- ☐ `OOS_REJECTED` — kandidat tidak memenuhi kriteria OOS.
- ☐ `OOS_TAINTED` — OOS telah digunakan untuk tuning, seleksi ulang, atau perubahan aturan.

## F. Ringkasan Bukti dan Metadata Penelitian

Bagian ini diisi agar penelitian dapat diperiksa kembali tanpa bergantung pada ingatan peneliti.

| Komponen | Isi |
|---|---|
| Nama penelitian | |
| `hypothesis_id` | |
| `research_batch_id` | |
| Instrumen atau universe | |
| Sumber data | |
| Periode data | |
| Periode IS | |
| Periode OOS | |
| Definisi event | |
| Definisi entry | |
| Definisi B0 | |
| Horizon | |
| Definisi return | |
| Definisi MAE/MFE | |
| Definisi ATR | |
| Candidate grid version | |
| Evaluation engine version | |
| Multiple-testing family ID | |
| Metode bootstrap | |
| Jumlah bootstrap | |
| Seed | |
| Asumsi biaya | |
| Kriteria seleksi IS | |
| Kriteria validasi OOS | |
| Kandidat terpilih | |
| Status akhir | |
| Tanggal freeze | |
| Penanggung jawab pemeriksaan | |

## G. Pernyataan Integritas Penelitian

Sebelum penelitian dinyatakan selesai, peneliti dapat menggunakan pernyataan berikut:

> Saya menyatakan bahwa penelitian ini dijalankan berdasarkan definisi, aturan entry, pembanding B0, horizon, candidate grid, dan kriteria evaluasi yang telah ditentukan sebelumnya.
>
> Saya telah berusaha menjaga prinsip no-look-ahead, mencatat event yang tidak valid atau tidak lengkap, serta menerapkan engine evaluasi yang konsisten pada B1 dan B0.
>
> Saya tidak menghapus kandidat yang gagal hanya karena hasilnya tidak sesuai harapan. Jika tidak ditemukan keunggulan yang memenuhi kriteria, hasil tersebut akan dilaporkan sebagai `NO_EDGE_FOUND`.
>
> Saya memahami bahwa hasil IS bukan jaminan hasil OOS, hasil OOS bukan jaminan masa depan, dan hubungan empiris tidak otomatis membuktikan hubungan sebab-akibat.

**Nama peneliti:** __________________________

**Tanggal:** _______________________________

**Tanda tangan/persetujuan:** ________________

## Penutup Lampiran

Checklist ini dirancang untuk menjaga agar penelitian TEKB tidak berhenti pada pertanyaan:

> "Apakah saya menemukan sinyal yang terlihat bagus?"

Sebaliknya, peneliti diarahkan untuk bertanya:

> "Apakah sinyal ini ditemukan melalui proses yang adil, dapat ditelusuri, tahan terhadap pemeriksaan, dan masih menunjukkan bukti setelah diuji di luar sampel?"

Dalam TEKB, kualitas penelitian tidak hanya ditentukan oleh hasil yang menguntungkan. Kualitas juga ditentukan oleh kemampuan untuk menunjukkan bagaimana hasil itu diperoleh, apa yang gagal, apa yang belum diketahui, dan batas klaim yang boleh dibuat.

---

<div align="center">

[← Lampiran E](/posts/lampiran-e-contoh-mini-penelitian-fiktif/) | [Beranda](/) | [Daftar Isi](/daftar-isi/)

</div>