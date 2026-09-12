
Kelima event tersebut mungkin merupakan bagian dari satu episode pasar yang sama, bukan lima kejadian yang benar-benar terpisah.

Inilah alasan **declustering** diperlukan.

Declustering dapat digunakan untuk:

- Menggabungkan event yang terlalu berdekatan.
- Menetapkan jarak minimum antar-event.
- Memilih satu event utama dari satu episode.
- Membentuk kelompok episode.
- Menggunakan unit analisis yang sesuai dengan ketergantungan data.

Aturan declustering harus ditentukan sebelum hasil digunakan untuk mengambil kesimpulan. Aturan tersebut juga harus dicatat dalam audit trail.

Tanpa declustering atau metode yang mengakui dependensi, ketidakpastian dapat terlihat lebih kecil daripada kenyataannya.

### 6.6.4. Hanya data yang memenuhi syarat penelitian

Tidak semua bar otomatis boleh masuk ke penelitian.

Data harus memenuhi persyaratan yang telah ditentukan, misalnya:

- Timestamp valid.
- Instrumen teridentifikasi dengan benar.
- OHLCV tidak rusak.
- Sesi dan slot dapat ditentukan.
- Volume tidak hilang atau tidak valid.
- Baseline dapat dihitung.
- Tidak terjadi pelanggaran aturan look-ahead.
- Data berada dalam rentang penelitian.
- Bar memenuhi aturan kelengkapan yang ditetapkan.

Jika baseline tidak dapat dihitung secara sah, event tidak boleh dipaksakan untuk diberi nilai RV.

Demikian pula, jika data outcome belum lengkap, hasil tidak boleh dianggap sebagai hasil lengkap hanya demi menambah jumlah observasi.

Status data yang tidak memenuhi syarat perlu dicatat secara eksplisit, misalnya:

- INVALID_DATA
- BASELINE_UNAVAILABLE
- INSUFFICIENT_HISTORY
- OUT_OF_SESSION
- EXCLUDED_BY_CONTRACT

Status tersebut membantu menjaga perbedaan antara:

- Tidak terjadi anomali.
- Anomali tidak dapat dihitung.
- Data tidak memenuhi syarat.
- Anomali terdeteksi tetapi outcome belum dapat dievaluasi.

Keempat keadaan tersebut tidak boleh disamakan.

### 6.6.5. SAMSON tidak boleh langsung diterjemahkan menjadi BUY atau SELL

Batasan terpenting SAMSON v1.0 adalah:

> SAMSON bukan sinyal BUY/SELL otomatis.

Aturan seperti berikut tidak boleh dianggap telah terbukti hanya karena RV tinggi:

> RV > 2,5 → BUY

atau:

> RV > 2,5 dan candle bullish → BUY

atau:

> RV > 5 dan harga turun → SELL

Semua aturan tersebut merupakan hipotesis yang masih harus diuji.

Jika ingin meneliti hubungan antara SAMSON dan arah harga, penelitian harus mendefinisikan:

- Event SAMSON.
- Arah candle.
- Titik observasi atau entry.
- Horizon.
- Return.
- B0.
- Biaya.
- Metode pengujian.
- Kriteria keputusan.
- Aturan OOS.

Bahkan setelah penelitian selesai, hasil positif tidak otomatis berarti aturan tersebut layak digunakan secara langsung. Hasil harus diperiksa dari sisi ukuran efek, ketidakpastian, biaya, stabilitas, dan generalisasi.

### 6.6.6. SAMSON tidak menjelaskan penyebab

SAMSON mendeteksi pola volume yang tidak biasa. Ia tidak menjelaskan secara otomatis mengapa volume tersebut terjadi.

Volume tinggi dapat disebabkan oleh banyak hal, misalnya:

- Berita.
- Perubahan indeks.
- Rebalancing.
- Aksi korporasi.
- Perubahan likuiditas.
- Kepanikan.
- Perpindahan posisi.
- Aktivitas algoritmik.
- Kesalahan atau masalah data.

Karena itu, SAMSON tidak boleh diperlakukan sebagai alat untuk mengidentifikasi motif pelaku pasar secara pasti.

SAMSON hanya memberikan observasi:

> "Aktivitas volume pada konteks ini lebih tinggi atau lebih rendah daripada baseline yang ditetapkan."

Penjelasan tentang penyebab memerlukan data dan penelitian tambahan.

### 6.6.7. SAMSON tidak menjamin adanya information edge

Detektor yang berhasil menemukan banyak kejadian anomali belum tentu menghasilkan informasi yang berguna untuk prediksi return.

Ada perbedaan antara:

- **Anomali statistik:** sesuatu berbeda dari kondisi normal.
- **Information edge:** kondisi tersebut memberikan informasi yang konsisten dan relevan terhadap outcome yang diteliti.

Contohnya, volume dapat sangat tidak biasa, tetapi arah return setelahnya tetap acak atau tidak berbeda dari B0. Dalam situasi tersebut, SAMSON berhasil mendeteksi anomali, tetapi penelitian belum menemukan edge yang dapat dibuktikan.

Hasil seperti itu bukan kegagalan sistem. Justru itulah fungsi penelitian:

> Membedakan sesuatu yang menarik secara visual dari sesuatu yang memiliki informasi terukur.

---

## Penutup Bab

SAMSON dalam TEKB adalah detektor anomali volume. Ia digunakan untuk menemukan kondisi ketika volume saat ini tidak biasa dibandingkan baseline yang relevan dan sebanding.

Konsep penting dalam SAMSON adalah:

- Volume absolut tidak sama dengan volume relatif.
- RV membandingkan volume saat ini dengan baseline.
- Baseline harus memperhatikan sesi dan slot waktu.
- `session_id`, `slot_id`, `slot_start`, dan `slot_end` membantu menjaga perbandingan tetap sebanding.
- Volume besar tidak otomatis berarti harga naik.
- Volume besar juga dapat diikuti penurunan atau pergerakan datar.
- Semua event harus dicatat, bukan hanya yang sesuai dugaan.
- Event yang berdekatan perlu diperlakukan dengan memperhatikan dependensi atau declustering.
- Timeframe lain harus dianggap sebagai eksperimen terpisah.
- SAMSON bukan keputusan entry dan bukan sinyal BUY/SELL otomatis.

Dengan demikian, SAMSON hanya membuka pintu pertanyaan:

> "Ketika aktivitas volume tidak biasa terjadi, apa yang sebenarnya terjadi pada harga setelahnya, dan apakah hasilnya berbeda dari pembanding yang adil?"

Pertanyaan tersebut baru dapat dijawab melalui pengukuran, distribusi, pembandingan, pengujian ketidakpastian, dan validasi OOS.

Prinsip TEKB tetap berlaku:

> **Bukti dulu, keputusan belakangan.**

---

## Ringkasan Bab

- SAMSON adalah detektor anomali volume dalam TEKB.
- Volume absolut tidak sama dengan volume relatif (RV).
- RV membandingkan volume saat ini dengan baseline yang sebanding.
- Baseline harus memperhatikan sesi dan slot waktu.
- Volume besar tidak otomatis berarti harga naik atau turun.
- Semua event harus dicatat, bukan hanya yang sesuai dugaan.
- Declustering diperlukan untuk event yang berdekatan.
- SAMSON bukan sinyal BUY/SELL otomatis.
- SAMSON tidak menjelaskan penyebab dan tidak menjamin adanya edge.

---

## Pertanyaan Refleksi

1. Mengapa volume besar belum tentu tidak biasa?
2. Apa perbedaan antara volume absolut dan volume relatif?
3. Mengapa baseline harus memperhatikan sesi dan slot waktu?
4. Apa fungsi `session_id`, `slot_id`, `slot_start`, dan `slot_end`?
5. Mengapa tiga event dengan RV yang sama bisa menghasilkan hasil yang berbeda?
6. Mengapa declustering diperlukan?
7. Mengapa SAMSON tidak boleh langsung diterjemahkan menjadi BUY/SELL?
8. Apa perbedaan antara anomali statistik dan information edge?
9. Mengapa SAMSON tidak menjelaskan penyebab volume?
10. Apa prinsip utama TEKB yang tetap berlaku dalam SAMSON?

---

<div align="center">

[← Bab Sebelumnya](/posts/bab-05-mengenal-data-ohlcv/) | [Beranda](/) | [Daftar Isi](/daftar-isi/) | [Bab Selanjutnya →](/posts/bab-07-dari-ada-sinyal/)

</div>