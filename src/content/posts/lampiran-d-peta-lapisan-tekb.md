---
title: "Lampiran D — Peta Lapisan TEKB"
published: 2026-09-13
description: "Peta 16 lapisan TEKB dari Data hingga Audit Trail, lengkap dengan hubungan antar-lapisan, tiga kelompok besar, dan prinsip urutan yang tidak boleh dibalik."
tags: ["lampiran-d", "peta-lapisan", "arsitektur", "metodologi"]
category: "Lampiran"
draft: false
lang: ""
---
D.1 Tujuan Lampiran
TEKB terdiri atas banyak komponen. Masing-masing memiliki fungsi yang berbeda, tetapi seluruhnya saling berhubungan dalam satu alur penelitian.

Tanpa peta yang jelas, seseorang dapat mencampuradukkan fungsi detektor volume dengan fungsi entry, menganggap hasil MAE/MFE sebagai keputusan trading, atau mengira hasil bootstrap sudah sama dengan bukti bahwa suatu strategi memiliki edge.

Lampiran ini memberikan peta lapisan TEKB, mulai dari data mentah hingga hasil penelitian yang telah diuji, dibekukan, dan diperiksa kembali melalui Out-of-Sample atau OOS.

Urutan dasarnya adalah:

Data → SAMSON → Event → Entry → B0 → MAE/MFE → ATR → Candidate SL/TP → Evaluation Engine → Distribution → Bootstrap → Multiple Testing → IS Selection → Freeze → OOS → Audit Trail

Urutan tersebut menggambarkan alur utama. Dalam implementasi nyata, beberapa komponen dapat digunakan secara paralel atau saling memberikan referensi. Namun, urutan logisnya tetap harus dijaga agar tidak terjadi kebocoran informasi masa depan.

D.2 Gambaran Besar Peta TEKB
Secara sederhana, TEKB dapat dipahami sebagai rangkaian lapisan berikut:

┌───────────────────────────────────────┐
│                 DATA                  │
│ OHLCV, timestamp, kualitas, sumber    │
└───────────────────┬───────────────────┘
                    ↓
┌───────────────────────────────────────┐
│               SAMSON                  │
│ Deteksi anomali volume secara kausal  │
└───────────────────┬───────────────────┘
                    ↓
┌───────────────────────────────────────┐
│                EVENT                  │
│ Identitas, waktu, status, provenance  │
└───────────────────┬───────────────────┘
                    ↓
┌───────────────────────────────────────┐
│                ENTRY                  │
│ Aturan kapan dan pada harga berapa    │
└───────────────────┬───────────────────┘
                    ↓
┌───────────────────────────────────────┐
│                  B0                   │
│ Pembanding historis yang adil         │
└───────────────────┬───────────────────┘
                    ↓
┌───────────────────────────────────────┐
│               MAE / MFE               │
│ Mengukur gerakan setelah entry        │
└───────────────────┬───────────────────┘
                    ↓
┌───────────────────────────────────────┐
│                 ATR                   │
│ Menyetarakan ukuran dengan volatilitas│
└───────────────────┬───────────────────┘
                    ↓
┌───────────────────────────────────────┐
│            CANDIDATE SL/TP             │
│ Kandidat aturan risiko dan target     │
└───────────────────┬───────────────────┘
                    ↓
┌───────────────────────────────────────┐
│           EVALUATION ENGINE           │
│ Menentukan outcome secara konsisten   │
└───────────────────┬───────────────────┘
                    ↓
┌───────────────────────────────────────┐
│              DISTRIBUTION             │
│ Bentuk dan penyebaran hasil           │
└───────────────────┬───────────────────┘
                    ↓
┌───────────────────────────────────────┐
│               BOOTSTRAP               │
│ Mengukur ketidakpastian dan stabilitas│
└───────────────────┬───────────────────┘
                    ↓
┌───────────────────────────────────────┐
│           MULTIPLE TESTING            │
│ Mengendalikan risiko temuan palsu     │
└───────────────────┬───────────────────┘
                    ↓
┌───────────────────────────────────────┐
│              IS SELECTION             │
│ Memilih kandidat berdasarkan bukti    │
└───────────────────┬───────────────────┘
                    ↓
┌───────────────────────────────────────┐
│                 FREEZE                │
│ Mengunci kandidat dan seluruh aturan  │
└───────────────────┬───────────────────┘
                    ↓
┌───────────────────────────────────────┐
│                  OOS                  │
│ Menguji generalisasi pada data baru   │
└───────────────────┬───────────────────┘
                    ↓
┌───────────────────────────────────────┐
│              AUDIT TRAIL              │
│ Menelusuri seluruh rantai bukti       │
└───────────────────────────────────────┘
Audit Trail sebenarnya melintasi seluruh lapisan, bukan hanya berada di bagian paling akhir. Setiap lapisan harus meninggalkan rekaman yang memungkinkan hasilnya ditelusuri kembali.

D.3 Lapisan 1 — Data
Fungsi
Data adalah bahan dasar seluruh penelitian TEKB. Dalam konteks OHLCV, data utama meliputi:

Open;

High;

Low;

Close;

Volume;

timestamp;

instrumen;

sesi perdagangan;

slot waktu;

sumber data;

status penyesuaian harga;

informasi kualitas data.

Data bukan sekadar kumpulan angka. Data juga memiliki konteks: kapan angka tersebut tersedia, bagaimana angka tersebut diperoleh, apakah sudah disesuaikan, dan apakah boleh digunakan untuk penelitian tertentu.

Pertanyaan utama
Apakah data berasal dari sumber yang dapat dipercaya?

Apakah timestamp benar?

Apakah urutan bar benar?

Apakah ada bar yang hilang?

Apakah ada duplikasi?

Apakah OHLC valid?

Apakah volume tersedia?

Apakah data telah disesuaikan secara konsisten?

Apakah data tersebut point-in-time?

Apakah data yang digunakan menciptakan survivorship bias?

Output
Lapisan Data menghasilkan:

dataset mentah;

dataset yang telah divalidasi;

metadata sumber;

laporan kualitas data;

batas periode penelitian;

definisi instrumen dan sesi;

status data yang boleh digunakan.

Prinsip penting
Data yang tersedia belum tentu otomatis boleh digunakan.

Data harus tersedia pada waktu yang sesuai dengan aturan penelitian. Data yang baru diketahui setelah suatu event terjadi tidak boleh digunakan untuk mendefinisikan event tersebut secara retroaktif.

D.4 Lapisan 2 — SAMSON
Fungsi
SAMSON adalah lapisan pendeteksi anomali volume. Dalam desain TEKB, SAMSON tidak bertugas menentukan apakah harga akan naik atau turun.

SAMSON menjawab pertanyaan:

“Apakah volume pada bar ini cukup tidak biasa dibandingkan baseline yang relevan?”

Contoh ukuran yang dapat digunakan adalah Relative Volume atau RV:

R
V
t
=
V
t
V
baseline
,
t
Jika volume suatu bar adalah 750.000 dan baseline-nya 150.000, maka:

R
V
t
=
750.000
150.000
=
5
Artinya, volume bar tersebut sekitar lima kali baseline.

Fungsi yang dilakukan
SAMSON dapat:

menghitung baseline volume;

menyesuaikan baseline dengan sesi dan slot waktu;

menghitung RV;

menerapkan ambang anomali;

memastikan baseline tidak menggunakan data masa depan;

melakukan declustering;

memberikan identitas awal pada event.

Fungsi yang tidak dilakukan
SAMSON tidak otomatis:

menyatakan harga akan naik;

menyatakan harga akan turun;

menetapkan entry;

menetapkan stop loss;

menetapkan take profit;

membuktikan adanya edge;

menggantikan B0;

menggantikan Evaluation Engine.

Output
event kandidat;

nilai RV;

baseline volume;

threshold;

timestamp deteksi;

versi aturan SAMSON;

status validitas deteksi.

Prinsip penting
Anomali volume adalah kondisi yang layak diteliti, bukan keputusan trading yang sudah terbukti.

D.5 Lapisan 3 — Event
Fungsi
Event adalah unit observasi penelitian. Event mengubah kondisi pasar yang terdeteksi menjadi objek yang memiliki identitas dan dapat ditelusuri.

Sebuah event minimal harus memiliki:

event_id;

instrument;

tanggal dan timestamp;

sesi;

slot waktu;

timestamp deteksi;

aturan pemicu;

nilai variabel pemicu;

versi metodologi;

status event;

informasi declustering;

hubungan dengan data sumber.

Event bukan hanya label seperti “volume besar”. Event harus menjawab:

“Kejadian apa yang dimaksud, kapan tepatnya terjadi, berdasarkan data apa, dan menurut aturan versi berapa?”

Perbedaan waktu yang harus dijaga
TEKB perlu membedakan beberapa jenis waktu:

Event time
Waktu kejadian atau bar yang memenuhi kondisi.

Confirmation time
Waktu ketika syarat konfirmasi selesai, jika strategi memerlukannya.

Availability time
Waktu ketika informasi dapat diketahui secara sah.

Evaluation time
Waktu atau horizon ketika hasil event diukur.

Perbedaan ini penting karena suatu kondisi mungkin terlihat jelas setelah candle selesai, tetapi belum tersedia ketika candle masih berjalan.

Output
event yang valid;

event yang ditolak;

event identifier;

timestamp dan metadata;

status included_in_research;

status actionable_live;

provenance event.

Prinsip penting
Event adalah objek penelitian, bukan sekadar sinyal visual pada chart.

D.6 Lapisan 4 — Entry
Fungsi
Lapisan Entry menentukan kapan dan pada harga berapa event dianggap mulai memiliki posisi hipotetis.

Dalam aturan kausal TEKB, jika sinyal baru diketahui setelah candle T selesai, entry tidak boleh menggunakan harga penutupan candle T seolah-olah harga tersebut masih dapat dipastikan diperoleh.

Contoh aturan:

Signal pada close T → entry pada open bar valid berikutnya.

Dalam bentuk sederhana:

P
entry
=
O
T
+
1
Jika terdapat jeda sesi atau bar tidak valid, aturan harus menentukan apa yang dimaksud dengan NEXT_VALID_BAR_OPEN.

Hal yang dicatat
signal timestamp;

signal close;

entry timestamp;

entry price;

bar entry;

gap antara signal close dan entry open;

aturan entry;

status kelayakan entry;

biaya atau asumsi eksekusi;

status actionable_live.

Entry gap
Jika close sinyal adalah 1.010 dan open entry berikutnya adalah 1.020, maka terdapat gap:

Gap
=
1.020
−
1.010
1.010
Gap
≈
0
,
99
%
Gap tidak boleh dihapus hanya karena membuat hasil terlihat lebih buruk atau lebih baik. Gap adalah bagian dari realitas eksekusi.

Prinsip penting
Sinyal dan entry adalah dua kejadian yang berbeda.

Kesalahan pada lapisan Entry dapat merusak seluruh penelitian karena semua MAE, MFE, SL, TP, return, dan outcome akan dihitung dari harga awal yang salah.

D.7 Lapisan 5 — B0
Fungsi
B0 adalah pembanding atau baseline kontrol. B0 digunakan untuk menjawab pertanyaan:

“Apakah hasil setelah event B1 benar-benar berbeda dari hasil yang mungkin terjadi pada kondisi pembanding yang adil?”

B0 membantu mencegah kesalahan berpikir:

“Harga naik setelah event, berarti event tersebut memiliki edge.”

Harga bisa saja naik karena kondisi pasar secara umum memang sedang mendukung. Tanpa pembanding, kenaikan tersebut dapat salah dianggap sebagai keunggulan event.

Aturan B0
B0 harus ditentukan berdasarkan aturan yang telah ditetapkan, misalnya:

instrumen yang sama;

slot atau sesi yang sama;

kondisi pemilihan yang tersedia sebelum outcome;

radius declustering yang sama;

nearest valid trading day;

tie-break yang telah ditentukan;

partisi IS/OOS yang sama;

tidak menggunakan event B0 berulang jika aturan melarang reuse;

tidak memilih berdasarkan hasil masa depan;

tidak melakukan matching berdasarkan outcome.

Output
pasangan B1–B0;

identitas event B1;

identitas event B0;

aturan matching;

jarak waktu;

status kecocokan;

alasan NO_MATCH_FOUND, jika tidak ada pasangan sah.

Prinsip penting
B0 bukan lawan yang dibuat lemah agar B1 terlihat menang.

B0 harus menjadi pembanding yang masuk akal, konsisten, dan ditentukan tanpa melihat hasil masa depan.

D.8 Lapisan 6 — MAE/MFE
Fungsi
MAE dan MFE mengukur bagaimana harga bergerak setelah entry.

MAE, atau Maximum Adverse Excursion, mengukur gerakan paling jauh yang merugikan posisi.

MFE, atau Maximum Favorable Excursion, mengukur gerakan paling jauh yang menguntungkan posisi.

Untuk posisi long:

M
A
E
raw
=
L
min
⁡
−
P
entry
M
F
E
raw
=
H
max
⁡
−
P
entry
Jika entry berada pada 1.020, harga terendah setelah entry adalah 1.005, dan harga tertinggi adalah 1.045, maka:

M
A
E
raw
=
1.005
−
1.020
=
−
15
M
F
E
raw
=
1.045
−
1.020
=
25
Horizon
MAE/MFE dapat dihitung pada beberapa horizon, misalnya:

R1;

R3;

R5;

R10.

Horizon harus ditentukan sebelum hasil diperiksa atau harus diperlakukan sebagai bagian dari candidate grid jika memang sedang diuji.

Status hasil
COMPUTED_FULL_HORIZON;

INSUFFICIENT_HORIZON;

INVALIDATED.

Fungsi MAE/MFE
MAE/MFE membantu menjawab:

Seberapa jauh harga biasanya bergerak melawan posisi?

Seberapa besar peluang harga sempat menguntungkan?

Apakah stop loss tertentu terlalu sempit?

Apakah target tertentu realistis?

Apakah B1 memiliki profil perjalanan yang berbeda dari B0?

Prinsip penting
MFE bukan berarti profit yang pasti berhasil direalisasikan.

Harga yang sempat naik 2 ATR tidak berarti trader pasti memperoleh profit 2 ATR. Untuk mengetahui hasil yang benar-benar terealisasi, diperlukan Evaluation Engine.

D.9 Lapisan 7 — ATR
Fungsi
ATR atau Average True Range digunakan sebagai satuan volatilitas. ATR membantu menyetarakan pergerakan harga antar-instrumen atau antar-periode yang memiliki skala harga berbeda.

True Range dapat dirumuskan sebagai:

T
R
t
=
max
⁡
(
H
t
−
L
t
,
 
∣
H
t
−
C
t
−
1
∣
,
 
∣
L
t
−
C
t
−
1
∣
)
ATR kemudian dihitung dari rangkaian True Range menggunakan metode yang ditentukan, misalnya Wilder.

ATR entry
ATR yang digunakan untuk menormalisasi hasil harus tersedia secara kausal pada waktu entry atau pada waktu yang telah ditentukan oleh kontrak penelitian.

ATR tidak boleh dihitung menggunakan data setelah entry jika ATR tersebut dipakai untuk menentukan ukuran risiko pada saat entry.

Normalisasi
Jika:

MAE raw = −15;

MFE raw = +25;

ATR entry = 10;

maka:

M
A
E
×
A
T
R
=
−
15
10
=
−
1
,
5
M
F
E
×
A
T
R
=
25
10
=
2
,
5
Artinya, gerakan merugikan maksimum adalah 1,5 ATR dan gerakan menguntungkan maksimum adalah 2,5 ATR.

Output
ATR entry;

metode ATR;

periode ATR;

timestamp ATR;

nilai raw;

nilai normalized;

versi definisi ATR.

Prinsip penting
ATR adalah alat pengukur skala, bukan mesin prediksi arah.

D.10 Lapisan 8 — Candidate SL/TP
Fungsi
Lapisan Candidate SL/TP mengubah informasi pergerakan historis menjadi sekumpulan hipotesis aturan risiko dan target.

Contoh kandidat:

SL = 1 ATR;

TP = 2 ATR;

maksimum holding = 5 bar.

Jika entry adalah 1.020 dan ATR entry adalah 10, maka:

P
S
L
=
1.020
−
1
(
10
)
=
1.010
P
T
P
=
1.020
+
2
(
10
)
=
1.040
Kandidat tersebut belum tentu baik. Ia baru merupakan aturan yang akan diuji.

Candidate grid
Candidate grid adalah daftar kombinasi parameter yang akan dievaluasi, misalnya:

SL: 0,5 ATR; 1 ATR; 1,5 ATR; 2 ATR;

TP: 1 ATR; 1,5 ATR; 2 ATR; 3 ATR;

holding period: 3 bar; 5 bar; 10 bar.

Semakin besar grid, semakin banyak hipotesis yang diuji. Karena itu, candidate grid harus dicatat dan masuk ke pengendalian multiple testing.

Percentile
Percentile MAE/MFE dapat membantu membatasi rentang kandidat agar tidak sepenuhnya arbitrer. Namun, percentile bukan bukti otomatis bahwa kandidat tersebut optimal.

Output
candidate identifier;

SL;

TP;

maximum holding period;

unit risiko;

versi candidate grid;

status kandidat;

hubungan dengan hipotesis.

Prinsip penting
Candidate SL/TP adalah hipotesis yang harus diuji, bukan parameter yang boleh dipilih setelah melihat hasil terbaik.

D.11 Lapisan 9 — Evaluation Engine
Fungsi
Evaluation Engine adalah “wasit” yang menerapkan aturan evaluasi secara konsisten kepada B1 dan B0.

Engine menentukan apa yang terjadi setelah entry berdasarkan:

harga entry;

level SL;

level TP;

urutan bar;

horizon;

aturan gap;

aturan same-bar;

biaya;

maksimum holding;

status kelengkapan data.

Aturan dasar
Evaluasi dimulai dari bar setelah entry sesuai kontrak penelitian. Jika terjadi gap melewati level SL atau TP, aturan harus menentukan apakah exit dianggap terjadi pada open bar.

Jika dalam satu candle High dan Low sama-sama melewati SL dan TP, tetapi data OHLC tidak memberikan urutan intrabar, maka hasil tidak boleh ditebak secara sembarangan.

Status yang dapat digunakan:

AMBIGUOUS_INTRABAR;

worst-case;

best-case;

aturan konservatif lain yang telah ditetapkan.

TIMEOUT dan INSUFFICIENT_HORIZON
Keduanya berbeda:

TIMEOUT: horizon evaluasi selesai tanpa SL atau TP tersentuh.

INSUFFICIENT_HORIZON: data tidak cukup untuk menyelesaikan horizon yang diwajibkan.

Biaya transaksi
Biaya dapat memengaruhi:

net return;

net expectancy;

kelayakan praktis;

friction survival.

Namun, biaya tidak boleh diam-diam mengubah definisi apakah SL atau TP tersentuh. Outcome dan net P&L harus dibedakan secara jelas.

Output
outcome;

exit timestamp;

exit price;

exit reason;

gross return;

net return;

R multiple;

worst-case result;

best-case result;

status evaluasi;

versi Evaluation Engine.

Prinsip penting
Evaluation Engine tidak boleh berubah-ubah hanya agar hasil suatu kandidat terlihat lebih baik.

D.12 Lapisan 10 — Distribution
Fungsi
Distribution atau distribusi menggambarkan keseluruhan bentuk hasil, bukan hanya satu angka ringkasan.

Hasil penelitian dapat disajikan sebagai distribusi:

return;

log return;

R multiple;

MAE;

MFE;

normalized MAE;

normalized MFE;

holding period;

outcome;

net return setelah biaya.

Dalam TEKB, fokusnya bukan hanya:

“Berapa win rate?”

Tetapi juga:

Bagaimana median hasilnya?

Seberapa lebar penyebarannya?

Seberapa besar ekor kerugiannya?

Apakah beberapa hasil ekstrem mendominasi mean?

Apakah B1 berbeda dari B0?

Apakah hasil positif tersebar atau hanya berasal dari beberapa event?

Apakah hasil tetap terlihat setelah biaya?

Ukuran yang dapat digunakan
jumlah event;

jumlah tanggal unik;

jumlah instrumen;

mean;

median;

standar deviasi;

percentile;

proporsi hasil positif;

kuantil kerugian;

kuantil keuntungan;

worst-case;

best-case;

expectancy;

net expectancy.

Prinsip penting
Distribusi memberikan gambaran bentuk risiko dan peluang yang tidak dapat dijelaskan oleh satu angka saja.

D.13 Lapisan 11 — Bootstrap
Fungsi
Bootstrap digunakan untuk memperkirakan ketidakpastian hasil penelitian dengan melakukan pengambilan sampel ulang dari data yang tersedia.

Pertanyaan yang ingin dijawab antara lain:

Seberapa stabil estimasi hasil?

Seberapa lebar interval ketidakpastiannya?

Apakah keunggulan tetap muncul dalam banyak pengambilan ulang?

Apakah hasil sangat bergantung pada beberapa tanggal atau event tertentu?

Ketergantungan event
Event trading sering tidak independen. Beberapa event dapat terjadi:

pada tanggal yang sama;

dalam tren yang sama;

pada instrumen yang sama;

dalam cluster waktu yang berdekatan.

Karena itu, bootstrap sederhana pada seluruh baris dapat memberikan tingkat keyakinan yang terlalu optimistis.

TEKB dapat menggunakan pendekatan seperti:

date-cluster bootstrap;

moving block bootstrap;

aturan block length yang telah ditentukan;

seed yang dicatat;

unit resampling yang sesuai dengan struktur ketergantungan.

Bootstrap bukan jaminan
Bootstrap tidak membuktikan bahwa strategi akan selalu berhasil. Bootstrap hanya membantu mengukur ketidakpastian berdasarkan data dan asumsi resampling yang digunakan.

Bootstrap juga tidak otomatis membuktikan kausalitas.

Output
estimasi statistik;

interval bootstrap;

distribusi estimasi;

metode resampling;

unit cluster atau block;

seed;

jumlah replikasi;

status keberhasilan bootstrap.

Prinsip penting
Bootstrap mengukur ketidakpastian hasil penelitian; bootstrap bukan alat untuk mengubah hasil buruk menjadi baik.

D.14 Lapisan 12 — Multiple Testing
Fungsi
Multiple Testing menangani masalah ketika banyak hipotesis atau kandidat diuji secara bersamaan.

Misalnya, peneliti menguji:

banyak instrumen;

banyak threshold RV;

banyak horizon;

banyak kombinasi SL/TP;

banyak definisi event;

banyak subkelompok;

banyak metrik.

Jika cukup banyak pengujian dilakukan, sebagian hasil dapat terlihat positif hanya karena kebetulan.

Risiko utama
Tanpa pengendalian multiple testing, peneliti dapat:

mencoba banyak kandidat;

menemukan satu kandidat dengan hasil sangat bagus;

mengabaikan kandidat lain;

menyimpulkan bahwa kandidat terpilih pasti memiliki edge.

Padahal, kandidat tersebut mungkin merupakan temuan palsu akibat banyaknya percobaan.

BH-FDR
TEKB dapat menggunakan Benjamini–Hochberg False Discovery Rate atau BH-FDR untuk mengendalikan proporsi temuan positif palsu yang diharapkan dalam suatu keluarga pengujian.

Keluarga pengujian harus didefinisikan secara jelas. Misalnya, keluarga untuk:

worst-case;

best-case;

kelompok hipotesis tertentu;

batch penelitian tertentu.

Worst-case dan best-case tidak boleh dicampur secara sembarangan jika keduanya mewakili pertanyaan statistik yang berbeda.

Provenance
Setiap pengujian perlu mencatat:

multiple_testing_family_id;

daftar hipotesis yang termasuk;

attempt number;

batch penelitian;

keluarga sebelumnya jika relevan;

aturan koreksi;

jumlah pengujian;

hasil adjusted significance.

Prinsip penting
Semakin banyak kesempatan untuk mencari hasil bagus, semakin besar kebutuhan untuk mengendalikan risiko temuan palsu.

D.15 Lapisan 13 — IS Selection
Fungsi
IS Selection adalah lapisan pemilihan kandidat berdasarkan hasil In-Sample atau IS.

Tujuannya bukan mencari kandidat yang sekadar memiliki angka tertinggi, melainkan memilih kandidat yang memenuhi kriteria penelitian yang telah ditentukan.

Dalam TEKB, perbandingan utama dilakukan antara B1 dan B0 secara berpasangan jika desain penelitian mensyaratkannya.

Untuk setiap pasangan:

D
i
=
R
B
1
,
i
−
R
B
0
,
i
Kemudian perbedaan rata-rata dapat dihitung:

D
ˉ
=
1
n
∑
i
=
1
n
D
i
Kriteria seleksi
Kandidat dapat diwajibkan memenuhi beberapa syarat, misalnya:

arah perbedaan sesuai hipotesis;

perbedaan cukup besar secara praktis;

hasil signifikan menurut prosedur yang telah ditentukan;

lolos pengendalian multiple testing;

memenuhi jumlah minimum event;

memenuhi jumlah minimum tanggal;

memenuhi jumlah minimum instrumen;

bertahan pada friction ladder;

tidak bergantung pada satu instrumen;

memenuhi leave-one-stock-out atau uji robustness lain.

Worst-case dan best-case
Jika terdapat ambiguitas intrabar, hasil dapat memiliki:

evaluasi worst-case;

evaluasi best-case.

Kandidat yang hanya terlihat bagus dalam best-case tetapi gagal dalam worst-case harus diperlakukan dengan hati-hati. Perbedaan tersebut harus ditampilkan, bukan disembunyikan.

Hasil seleksi
Kemungkinan hasil IS Selection:

kandidat lolos;

kandidat gagal;

kandidat belum cukup data;

kandidat tidak dapat dievaluasi;

NO_EDGE_FOUND.

NO_EDGE_FOUND bukan kegagalan sistem. Status tersebut berarti belum ada kandidat yang memenuhi aturan bukti yang telah ditentukan.

Prinsip penting
IS Selection memilih kandidat berdasarkan aturan yang telah ditetapkan, bukan berdasarkan kandidat yang paling menarik secara visual.

D.16 Lapisan 14 — Freeze
Fungsi
Freeze berarti mengunci kandidat dan seluruh aturan yang akan dibawa ke OOS.

Freeze mencegah peneliti mengubah aturan setelah melihat data OOS. Tanpa freeze, OOS dapat berubah fungsi menjadi tempat tuning kedua.

Komponen yang dikunci
Freeze dapat mencakup:

definisi event;

definisi SAMSON;

aturan entry;

aturan B0;

definisi MAE/MFE;

definisi ATR;

Evaluation Engine;

candidate grid;

kandidat terpilih;

kriteria seleksi;

friction ladder;

horizon;

aturan ambiguity;

aturan biaya;

aturan pelaporan;

multiple-testing family;

fingerprint metodologi.

Contoh metadata freeze
candidate_grid_version_id;

entry_definition_version_id;

b0_selection_rule_version;

mae_mfe_definition_version_id;

atr_definition_version_id;

evaluation_engine_version_id;

multiple_testing_family_id;

research_batch_id;

hypothesis_id;

kandidat terpilih;

timestamp freeze;

protocol hash;

computation fingerprint.

Status yang dapat digunakan
UNFROZEN;

FROZEN;

FREEZE_FAILED;

OOS_PENDING;

OOS_VALIDATED;

OOS_REJECTED;

OOS_SPENT;

OOS_TAINTED.

Prinsip penting
Setelah freeze, hasil OOS tidak boleh digunakan untuk memperbaiki kandidat yang sedang diuji.

Jika aturan diubah setelah freeze, maka perubahan tersebut harus dianggap sebagai versi penelitian baru dan dicatat secara terpisah.

D.17 Lapisan 15 — OOS
Fungsi
OOS atau Out-of-Sample adalah pengujian pada data yang tidak digunakan untuk membangun, menyesuaikan, atau memilih kandidat.

OOS berfungsi sebagai ujian generalisasi.

Alur sederhananya:

Data IS
   ↓
Eksplorasi dan pengujian
   ↓
IS Selection
   ↓
Freeze
   ↓
Data OOS
   ↓
Evaluasi satu kali dengan aturan yang sama
Aturan OOS
Dalam OOS:

kandidat sudah frozen;

definisi entry tetap;

B0 tetap;

MAE/MFE tetap;

ATR tetap;

Evaluation Engine tetap;

candidate grid tidak diubah untuk mencari hasil lebih baik;

kriteria evaluasi tetap;

hasil OOS tidak digunakan untuk melakukan reseleksi;

kegagalan OOS tidak dihapus.

Hasil OOS
OOS_VALIDATED: kandidat frozen memenuhi kriteria OOS yang telah ditentukan.

OOS_REJECTED: kandidat frozen tidak memenuhi kriteria OOS.

OOS positif tidak otomatis berarti strategi akan berhasil di masa depan. OOS hanya menunjukkan bahwa kandidat memiliki bukti tambahan pada periode yang belum digunakan dalam pemilihannya.

OOS yang tercemar
OOS dapat menjadi OOS_TAINTED jika peneliti:

melihat hasil OOS;

mengubah parameter;

mengulang pengujian untuk mencari versi lebih baik;

memilih kandidat baru berdasarkan hasil OOS;

menggunakan OOS sebagai bagian dari proses tuning.

OOS yang telah digunakan untuk pengambilan keputusan tidak boleh lagi diperlakukan sebagai OOS yang benar-benar belum tersentuh.

Prinsip penting
OOS bukan tempat mencari kandidat baru. OOS adalah tempat menguji kandidat yang sudah dipilih.

D.18 Lapisan 16 — Audit Trail
Fungsi
Audit Trail adalah lapisan keterlacakan yang menghubungkan seluruh proses:

Data mentah
   ↓
Aturan
   ↓
Event
   ↓
Entry
   ↓
B0
   ↓
MAE/MFE
   ↓
ATR
   ↓
Candidate SL/TP
   ↓
Evaluation
   ↓
Distribution
   ↓
Bootstrap
   ↓
Multiple Testing
   ↓
IS Selection
   ↓
Freeze
   ↓
OOS
   ↓
Kesimpulan
Audit Trail tidak hanya mencatat apakah proses selesai. Audit Trail harus memungkinkan seseorang menjawab:

Data apa yang digunakan?

Dari sumber mana?

Aturan versi berapa?

Kapan event terdeteksi?

Kapan informasi tersedia?

Mengapa entry berada pada harga tersebut?

Bagaimana B0 dipilih?

Bagaimana MAE/MFE dihitung?

ATR versi apa yang digunakan?

Candidate grid mana yang diuji?

Evaluation Engine versi berapa?

Bagaimana hasil diringkas?

Bagaimana bootstrap dilakukan?

Keluarga multiple testing apa yang digunakan?

Mengapa kandidat dipilih atau ditolak?

Apakah kandidat sudah frozen?

Apakah OOS pernah digunakan ulang?

Apakah hasil dapat direproduksi?

Identitas penting
Audit Trail dapat menyimpan:

computation_id;

protocol_hash;

hypothesis_id;

research_batch_id;

attempt_number;

candidate_grid_version_id;

entry_definition_version_id;

b0_selection_rule_version;

mae_mfe_definition_version_id;

atr_definition_version_id;

evaluation_engine_version_id;

multiple_testing_family_id;

samson_timeframe_version;

fingerprint seluruh komponen;

timestamp proses;

seed;

konfigurasi;

status hasil;

alasan kegagalan.

Prinsip penting
Audit Trail bukan aksesori dokumentasi. Audit Trail adalah bagian dari bukti penelitian.

Tanpa Audit Trail, hasil mungkin terlihat meyakinkan, tetapi sulit diketahui apakah hasil tersebut berasal dari aturan yang benar, data yang tepat, atau perubahan metodologi yang tidak tercatat.

D.19 Hubungan Antar-Lapisan
Setiap lapisan memiliki pertanyaan utama yang berbeda.

Lapisan	Pertanyaan Utama
Data	Data apa yang tersedia dan boleh digunakan?
SAMSON	Apakah terjadi anomali volume?
Event	Kejadian apa yang sedang diteliti?
Entry	Kapan posisi dimulai dan pada harga berapa?
B0	Apa pembanding yang adil?
MAE/MFE	Bagaimana harga bergerak setelah entry?
ATR	Seberapa besar gerakan tersebut relatif terhadap volatilitas?
Candidate SL/TP	Aturan risiko dan target apa yang akan diuji?
Evaluation Engine	Apa outcome menurut aturan yang konsisten?
Distribution	Bagaimana bentuk keseluruhan hasilnya?
Bootstrap	Seberapa besar ketidakpastian estimasi?
Multiple Testing	Seberapa besar risiko temuan positif palsu?
IS Selection	Kandidat mana yang memenuhi kriteria bukti?
Freeze	Apa yang dikunci sebelum OOS?
OOS	Apakah hasil dapat digeneralisasi ke data baru?
Audit Trail	Apakah seluruh proses dapat ditelusuri dan diulang?
Kesalahan pada satu lapisan dapat merambat ke lapisan berikutnya.

Contohnya:

Entry salah
   ↓
MAE/MFE salah
   ↓
ATR-normalization salah
   ↓
SL/TP dievaluasi dari harga yang salah
   ↓
Distribution berubah
   ↓
Bootstrap mengukur hasil yang salah
   ↓
IS Selection memilih kandidat yang salah
   ↓
Freeze mengunci kesalahan
   ↓
OOS menguji definisi yang keliru
Karena itu, semakin awal suatu kesalahan terjadi, semakin luas dampaknya terhadap keseluruhan penelitian.

D.20 Tiga Kelompok Besar Lapisan TEKB
Agar lebih mudah dipahami, lapisan TEKB dapat dikelompokkan menjadi tiga bagian besar.

Kelompok A — Pembentukan Observasi
Terdiri dari:

Data;

SAMSON;

Event;

Entry;

B0.

Fokus kelompok ini adalah:

“Apa yang diamati, kapan diamati, dan dibandingkan dengan apa?”

Kesalahan pada kelompok ini dapat menyebabkan bias observasi, look-ahead bias, atau pembanding yang tidak adil.

Kelompok B — Pengukuran dan Evaluasi
Terdiri dari:

MAE/MFE;

ATR;

Candidate SL/TP;

Evaluation Engine;

Distribution.

Fokus kelompok ini adalah:

“Bagaimana hasil setelah event diukur dan diterjemahkan menjadi outcome?”

Kesalahan pada kelompok ini dapat menyebabkan pengukuran yang tidak konsisten, bias eksekusi, atau hasil yang tidak dapat dibandingkan.

Kelompok C — Pengujian dan Generalisasi
Terdiri dari:

Bootstrap;

Multiple Testing;

IS Selection;

Freeze;

OOS;

Audit Trail.

Fokus kelompok ini adalah:

“Apakah hasil tersebut cukup dapat dipercaya, dipilih secara jujur, dan dapat diuji pada data baru?”

Kesalahan pada kelompok ini dapat menyebabkan overfitting, false discovery, kebocoran OOS, atau kesimpulan yang tidak dapat direproduksi.

D.21 Prinsip Urutan yang Tidak Boleh Dibalik
Beberapa urutan dalam TEKB tidak boleh dibalik tanpa alasan metodologis yang jelas.

1. Data harus mendahului Event
Tidak boleh mendefinisikan event berdasarkan data yang belum tersedia pada saat event.

2. Event harus mendahului Entry
Entry harus berasal dari event dan aturan waktu yang jelas. Entry tidak boleh ditentukan setelah melihat hasil terbaik.

3. Entry harus mendahului MAE/MFE
MAE dan MFE dihitung relatif terhadap entry. Jika entry berubah, hasil MAE/MFE juga berubah.

4. ATR harus tersedia secara kausal
ATR yang digunakan pada entry tidak boleh menggunakan data masa depan.

5. Candidate SL/TP harus ditentukan sebelum evaluasi kandidat
Jika level SL/TP dipilih setelah melihat hasil masing-masing event, penelitian dapat mengalami bias.

6. Distribution harus berasal dari hasil yang telah dihitung dengan aturan konsisten
Distribusi tidak boleh dibangun dari campuran hasil yang menggunakan definisi entry atau Evaluation Engine berbeda tanpa penandaan.

7. IS Selection harus mendahului Freeze
Kandidat dipilih berdasarkan IS, kemudian dikunci sebelum OOS.

8. Freeze harus mendahului OOS
Jika kandidat belum dikunci, OOS dapat berubah menjadi ruang tuning.

9. Audit Trail harus menyertai seluruh proses
Audit Trail tidak boleh dibuat hanya setelah kesimpulan selesai, karena keputusan dan perubahan penting mungkin sudah terlupakan.

D.22 Peta Ringkas dalam Satu Kalimat
Seluruh sistem TEKB dapat diringkas sebagai berikut:

Data menyediakan bahan yang tersedia secara kausal; SAMSON mendeteksi kondisi yang tidak biasa; Event memberi identitas pada kejadian; Entry menentukan awal pengukuran; B0 menyediakan pembanding; MAE/MFE mengukur perjalanan harga; ATR menyetarakan skala volatilitas; Candidate SL/TP membentuk hipotesis; Evaluation Engine menentukan outcome; Distribution menggambarkan hasil; Bootstrap mengukur ketidakpastian; Multiple Testing mengendalikan risiko temuan palsu; IS Selection memilih kandidat; Freeze mengunci aturan; OOS menguji generalisasi; dan Audit Trail memastikan seluruh rantai bukti dapat ditelusuri.

D.23 Prinsip Penutup
Peta lapisan TEKB menunjukkan bahwa tidak ada satu komponen yang sendirian dapat membuktikan adanya edge.

SAMSON hanya mendeteksi kondisi.

Event hanya mendefinisikan kejadian.

Entry hanya menentukan titik awal.

B0 hanya menyediakan pembanding.

MAE/MFE hanya mengukur perjalanan harga.

ATR hanya menyetarakan skala.

Candidate SL/TP hanya membentuk hipotesis.

Evaluation Engine hanya menerapkan aturan outcome.

Distribution hanya menggambarkan hasil.

Bootstrap hanya mengukur ketidakpastian.

Multiple Testing hanya mengendalikan risiko pencarian berlebihan.

IS Selection hanya memilih berdasarkan kriteria.

Freeze hanya mengunci aturan.

OOS hanya menguji data baru.

Audit Trail hanya memastikan proses dapat ditelusuri.

Kekuatan TEKB muncul dari hubungan seluruh lapisan yang dijalankan secara konsisten, bukan dari satu indikator atau satu angka.

TEKB bukan satu sinyal, melainkan rantai bukti.

Rantai tersebut harus dimulai dari data yang benar, berjalan melalui aturan yang kausal, menggunakan pembanding yang adil, mengukur hasil secara konsisten, memperhitungkan ketidakpastian, mengendalikan pencarian berlebihan, lalu menguji apakah hasilnya masih bertahan pada data yang belum digunakan.

Dengan demikian, TEKB tidak hanya bertanya:

“Apakah ada pola yang terlihat menguntungkan?”

TEKB bertanya lebih jauh:

“Apakah pola tersebut dapat didefinisikan, diukur, dibandingkan, diuji, dikunci, digeneralisasi, dan ditelusuri secara jujur?”
---

<div align="center">
← Lampiran C | Beranda | Daftar Isi | Lampiran E →

</div> ```