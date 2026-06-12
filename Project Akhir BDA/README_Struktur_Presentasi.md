# Struktur Presentasi Proyek BDA Kelompok 6

## Judul Proyek

**Big Data Analytics untuk Identifikasi Pola Penjualan dan Perilaku Konsumen pada Retail Transactions Dataset**

## Anggota Kelompok

- Aulia Permata Kumala
- Lidwina Eleonora Dora
- Fayza Avieninda

Program Studi Teknologi Informasi  
Universitas Brawijaya  
2026

---

## Slide 1 - Sampul

### Isi

- Proyek Akhir Big Data Analytics
- Kelompok 6
- Nama seluruh anggota
- Program Studi Teknologi Informasi
- Universitas Brawijaya
- Tahun 2026

### Narasi

> Pada proyek ini, kami melakukan analisis terhadap satu juta transaksi retail untuk mengidentifikasi produk unggulan, pola penjualan, perilaku pelanggan, asosiasi produk, dan kebutuhan stok.

---

## Slide 2 - Latar Belakang

### Judul

**Data transaksi dapat diubah menjadi dasar pengambilan keputusan bisnis**

### Isi

- Retail menghasilkan data transaksi dalam jumlah besar.
- Data mentah belum langsung memberikan informasi bisnis.
- Perusahaan perlu mengetahui:
  - Produk yang paling diminati
  - Pola penjualan berdasarkan waktu
  - Karakteristik pelanggan
  - Hubungan pembelian antarproduk
  - Produk yang perlu diprioritaskan dalam persediaan

### Visual

```text
Data Transaksi
      ↓
Big Data Analytics
      ↓
Insight dan Rekomendasi Bisnis
```

### Narasi

> Data transaksi tidak hanya berfungsi sebagai catatan penjualan. Apabila dianalisis dengan tepat, data tersebut dapat membantu perusahaan memahami produk, pelanggan, waktu penjualan, bundling, dan kebutuhan persediaan.

---

## Slide 3 - Identifikasi Masalah

### Judul

**Lima pertanyaan bisnis menjadi fokus analisis**

### Isi

1. Produk apa yang paling sering dibeli?
2. Kapan aktivitas penjualan tertinggi terjadi?
3. Bagaimana segmentasi pelanggan berdasarkan nilai transaksinya?
4. Produk apa yang sering dibeli bersamaan?
5. Produk apa yang perlu diprioritaskan dalam persediaan?

> **Catatan:** Pertanyaan nomor empat akan dijawab melalui analisis Fayza.

---

## Slide 4 - Tujuan Proyek

### Judul

**Analisis diarahkan untuk menghasilkan insight yang dapat ditindaklanjuti**

### Isi

- Mengidentifikasi produk unggulan.
- Menganalisis tren bulanan, pola musim, dan jam transaksi.
- Membentuk segmentasi pelanggan sederhana.
- Mengidentifikasi asosiasi pembelian produk.
- Membuat dashboard penjualan.
- Membuat prediksi kebutuhan stok sederhana.
- Menghasilkan rekomendasi bisnis.

---

## Slide 5 - Dataset

### Judul

**Analisis menggunakan satu juta transaksi dengan 13 atribut**

| Informasi | Nilai |
|---|---:|
| Jumlah transaksi | 1.000.000 |
| Jumlah atribut | 13 |
| Periode data | 1 Januari 2020-18 Mei 2024 |
| Sumber | Kaggle |
| Produk unik | 81 |

### Contoh Atribut

- `Transaction_ID`
- `Date`
- `Customer_Name`
- `Product`
- `Total_Items`
- `Total_Cost`
- `Customer_Category`
- `Season`
- `Promotion`

> **Catatan:** Dataset tidak menyediakan harga dan jumlah unit untuk setiap produk secara terpisah.

**Pembicara:** Aul

---

## Slide 6 - Data Preprocessing

### Judul

**Data telah dipersiapkan agar konsisten dan siap dianalisis**

### Proses

1. Memeriksa missing value.
2. Mengisi `Promotion` yang kosong dengan `No Promotion`.
3. Memeriksa dan menghapus duplikat.
4. Mengonversi `Date` menjadi format datetime.
5. Mengonversi kolom `Product` menjadi daftar produk.
6. Memisahkan produk menggunakan `explode()`.
7. Membentuk fitur bulan, hari, jam, dan tahun-bulan.

### Hasil

- Missing value `Promotion`: 333.943 baris, sudah ditangani.
- Duplikat: 0.
- Tanggal invalid: 0.
- Transaksi setelah preprocessing: tetap 1.000.000.
- Data utama siap dianalisis.

### Visual

```text
Raw Data
   ↓
Missing Value & Duplicate Check
   ↓
Product and Date Transformation
   ↓
Analysis-Ready Dataset
```

---

## Slide 7 - Metode Analisis

### Judul

**Setiap tujuan bisnis menggunakan pendekatan analisis yang berbeda**

| Fokus | Metode |
|---|---|
| Produk unggulan | Frekuensi kemunculan produk |
| Pola waktu | Agregasi bulanan, musim, dan jam |
| Segmentasi pelanggan | Frequency, Monetary, dan Q-Cut |
| Asosiasi produk | Market Basket Analysis |
| Kebutuhan stok | Rata-rata 30 hari dan safety stock |
| Dashboard | Matplotlib dan Seaborn |

### Narasi

> Metode yang digunakan bersifat deskriptif dan sederhana sesuai dengan ketentuan proyek. Hasilnya digunakan sebagai dasar rekomendasi bisnis.

---

# Hasil Analisis

## Slide 8 - KPI Penjualan

### Judul

**Satu juta transaksi menghasilkan total penjualan $52,46 juta**

| KPI | Hasil |
|---|---:|
| Total Sales | $52.455.220,40 |
| Total Transactions | 1.000.000 |
| Total Customers | 329.738 |
| Average Transaction Value | $52,46 |

### Visual

Gunakan empat kotak KPI atau bagian atas dashboard.

**Pembicara:** Aul

---

## Slide 9 - Produk Terlaris

### Judul

**Toothpaste menjadi produk yang paling sering muncul dalam transaksi**

### Visual

Grafik **Top 10 Most Purchased Products**.

### Callout

```text
Toothpaste
73.324 kemunculan
```

### Interpretasi

- Toothpaste memiliki frekuensi tertinggi.
- Produk berikutnya adalah Ice Cream, Soap, Jam, dan Orange.
- Produk berfrekuensi tinggi perlu diprioritaskan dalam persediaan.
- Produk tersebut juga dapat digunakan sebagai pendukung promosi.

**Pembicara:** Lidwina

---

## Slide 10 - Nilai Transaksi Terkait Produk

### Judul

**Toothpaste paling sering terkait dengan transaksi bernilai tinggi**

### Visual

Grafik **Top 10 Products Associated with Highest Transaction Revenue**.

### Callout

```text
Toothpaste
$3.844.106,37 nilai transaksi terkait
```

### Interpretasi

- Toothpaste sering terdapat dalam transaksi bernilai tinggi.
- Angka tersebut bukan revenue Toothpaste secara langsung.
- Dataset tidak menyediakan harga masing-masing produk.
- `Total_Cost` merupakan nilai keseluruhan transaksi.

### Narasi Penting

> Analisis ini menunjukkan keterkaitan produk dengan transaksi bernilai tinggi, bukan pendapatan pasti setiap produk.

---

## Slide 11 - Tren Penjualan Bulanan

### Judul

**Maret 2023 menjadi bulan dengan penjualan tertinggi**

### Visual

Grafik **Monthly Sales Trend**.

### Callout

| Keterangan | Periode | Nilai |
|---|---|---:|
| Tertinggi | Maret 2023 | $1.033.556,59 |
| Terendah dari bulan lengkap | Februari 2022 | $910.431,32 |

> Data Mei 2024 hanya tersedia sampai tanggal 18 sehingga tidak digunakan untuk menentukan bulan terendah.

### Interpretasi

- Penjualan mengalami fluktuasi bulanan.
- Selisih antarbulan tidak menunjukkan pertumbuhan atau penurunan ekstrem.
- Analisis bulanan dapat digunakan untuk perencanaan promosi dan persediaan.

---

## Slide 12 - Pola Musiman

### Judul

**Fall mencatat penjualan tertinggi, tetapi pola musim tidak dominan**

### Visual

Grafik **Total Penjualan Berdasarkan Musim**.

| Musim | Total Penjualan |
|---|---:|
| Spring | $13.113.238,75 |
| Summer | $13.116.675,79 |
| Fall | $13.136.913,71 |
| Winter | $13.088.392,15 |

### Interpretasi

- Fall memiliki total penjualan tertinggi.
- Perbedaannya dengan musim lain sangat kecil.
- Penjualan cenderung tersebar merata sepanjang musim.
- Tidak ditemukan pola musiman yang sangat kuat.

> Hindari menyatakan bahwa penjualan meningkat drastis saat Fall karena data tidak mendukung pernyataan tersebut.

---

## Slide 13 - Jam Ramai

### Judul

**Pukul 10.00 memiliki transaksi terbanyak, tetapi aktivitas per jam relatif merata**

### Visual

Grafik **Jumlah Transaksi Berdasarkan Jam**.

### Callout

```text
Pukul 10.00
42.021 transaksi
```

### Interpretasi

- Pukul 10.00 merupakan jam dengan transaksi terbanyak.
- Selisih transaksi antarjam relatif kecil.
- Tidak terdapat satu jam yang sangat dominan.
- Temuan dapat menjadi pertimbangan awal dalam penyusunan jadwal operasional.

---

# Bagian Aul

## Slide 14 - Metode Segmentasi Pelanggan

### Judul

**Pelanggan dibagi berdasarkan kontribusi nilai pembeliannya**

### Variabel

- **Frequency:** jumlah transaksi pelanggan.
- **Monetary:** total nilai pembelian pelanggan.

### Metode

- Quantile Segmentation menggunakan `pd.qcut()`.
- Pelanggan dibagi menjadi:
  - Low Value
  - Medium Value
  - High Value

### Visual

```text
Customer Transactions
        ↓
Frequency + Monetary
        ↓
Quantile Segmentation
        ↓
Low | Medium | High Value
```

> Walaupun Frequency dihitung, pembentukan segmen terutama menggunakan Monetary.

---

## Slide 15 - Distribusi Segmentasi

### Judul

**Jumlah pelanggan pada ketiga segmen relatif seimbang**

### Visual

Grafik **Customer Segmentation Distribution**.

| Segmen | Jumlah | Persentase |
|---|---:|---:|
| Low Value | 109.922 | sekitar 33,3% |
| Medium Value | 109.905 | sekitar 33,3% |
| High Value | 109.911 | sekitar 33,3% |

### Interpretasi

- Jumlah pelanggan seimbang karena metode quantile.
- Kesamaan jumlah pelanggan tidak berarti kontribusi pendapatannya sama.
- Perbedaan utama terlihat pada nilai belanja setiap kelompok.

---

## Slide 16 - Karakteristik Segmen

### Judul

**Pelanggan High Value menjadi sumber utama penjualan**

### Visual

Grafik **Revenue Contribution by Segment**.

| Segmen | Rata-rata Belanja | Total Penjualan |
|---|---:|---:|
| Low Value | $32,97 | $3,62 juta |
| Medium Value | $83,34 | $9,16 juta |
| High Value | $360,94 | $39,67 juta |

### Callout

```text
High Value
75,6% total penjualan
```

### Interpretasi

- High Value menghasilkan sebagian besar penjualan.
- Pelanggan High Value perlu dipertahankan.
- Medium Value dapat diarahkan menjadi High Value.
- Low Value dapat ditargetkan dengan promosi untuk meningkatkan pembelian.

---

## Slide 17 - Dashboard Penjualan

### Judul

**Dashboard mengintegrasikan indikator penjualan dan perilaku pelanggan**

### Visual

Masukkan gambar dashboard penuh.

### Komponen Dashboard

- KPI penjualan
- Produk terlaris
- Produk terkait transaksi bernilai tinggi
- Tren bulanan
- Revenue berdasarkan kategori pelanggan
- Segmentasi pelanggan
- Revenue per segmen

### Narasi

> Dashboard membantu pengguna melihat kondisi bisnis dalam satu tampilan tanpa membaca seluruh hasil pengolahan data.

---

# Bagian Fayza

## Slide 18 - Asosiasi Produk dan Bundling

### Judul

**Market Basket Analysis untuk rekomendasi bundling produk**

### Metode

Association Rule Mining dengan metrik:

- Support
- Confidence
- Lift

### Output yang Akan Ditambahkan

- Aturan asosiasi terbaik
- Kombinasi produk
- Interpretasi hubungan
- Rekomendasi bundling dan cross-selling

> **Catatan:** Slide ini belum boleh dipresentasikan sebagai hasil final sampai analisis Fayza selesai.

---

# Bagian Lidwina: Prediksi Stok

## Slide 19 - Masalah dan Metode Prediksi Stok

### Judul

**Permintaan 30 hari terakhir digunakan untuk memperkirakan kebutuhan tujuh hari**

### Periode Analisis

**18 April-17 Mei 2024**

### Tahapan

1. Memisahkan daftar produk.
2. Menghitung kemunculan produk setiap hari.
3. Mengambil 30 hari lengkap terakhir.
4. Menghitung rata-rata permintaan harian.
5. Memprediksi permintaan tujuh hari.
6. Menambahkan safety stock.

### Rumus

```text
Prediksi 7 Hari
= Rata-rata Permintaan Harian × 7
```

```text
Target Persediaan
= Prediksi 7 Hari + Safety Stock
```

> Jangan memasukkan kode Python yang panjang ke dalam slide.

---

## Slide 20 - Hasil Rekomendasi Stok

### Judul

**Toothpaste menjadi prioritas persediaan utama untuk tujuh hari berikutnya**

### Visual

Grafik **Top 10 Estimasi Kebutuhan Stok Produk untuk 7 Hari**.

### Callout

```text
TOOTHPASTE
Rata-rata harian : 43,70
Prediksi 7 hari  : 305,90
Safety stock     : 35,71
Target persediaan: 342
```

### Interpretasi

- Toothpaste memiliki estimasi kebutuhan tertinggi.
- Yogurt berada pada posisi berikutnya dengan target 201.
- Hair Gel memiliki target 195.
- Salmon dan Cereal Bars memiliki target 194.
- Produk tersebut dapat diprioritaskan dalam pengelolaan persediaan.

---

## Slide 21 - Prioritas Persediaan

### Judul

**Sepuluh produk menjadi prioritas awal pengelolaan stok**

| Produk | Prediksi 7 Hari | Safety Stock | Target |
|---|---:|---:|---:|
| Toothpaste | 305,90 | 35,71 | 342 |
| Yogurt | 175,23 | 25,18 | 201 |
| Hair Gel | 170,80 | 23,51 | 195 |
| Salmon | 173,37 | 20,17 | 194 |
| Cereal Bars | 165,67 | 28,14 | 194 |
| Beef | 168,93 | 22,98 | 192 |
| Coffee | 164,97 | 26,24 | 192 |
| Power Strips | 171,50 | 18,26 | 190 |
| Jam | 165,67 | 23,67 | 190 |
| Olive Oil | 170,10 | 18,84 | 189 |

> Jika tabel terlalu kecil, tampilkan lima produk teratas. Seluruh produk sudah ditampilkan pada grafik slide sebelumnya.

---

## Slide 22 - Rekomendasi Bisnis

### Judul

**Hasil analisis menghasilkan empat tindakan bisnis utama**

### Persediaan

- Memprioritaskan Toothpaste dan produk dengan estimasi kebutuhan tinggi.
- Menggunakan safety stock untuk mengantisipasi perubahan permintaan.

### Pelanggan

- Mempertahankan High Value dengan program loyalitas.
- Mendorong Medium Value menjadi High Value melalui promosi personal.

### Operasional

- Menggunakan tren waktu sebagai pertimbangan jadwal dan promosi.
- Tidak melakukan perubahan ekstrem karena pola musim dan jam relatif merata.

### Bundling

- Menyusun bundling berdasarkan aturan asosiasi dengan lift di atas satu.
- Dilengkapi setelah hasil analisis Fayza selesai.

---

## Slide 23 - Keterbatasan Penelitian

### Judul

**Hasil perlu dibaca dengan mempertimbangkan keterbatasan data**

### Isi

- Dataset tidak mencatat harga dan jumlah unit setiap produk.
- Tidak tersedia stok gudang dan lead time pemasok.
- Prediksi stok masih menggunakan metode rata-rata sederhana.
- Segmentasi belum memperhitungkan recency.
- `Customer_Name` digunakan sebagai identitas pelanggan.
- Pola musim dan jam memiliki perbedaan yang sangat kecil.
- Dataset publik belum tentu mencerminkan satu bisnis retail nyata.

### Narasi Penting

> Rekomendasi stok merupakan estimasi target persediaan, bukan jumlah pembelian yang wajib dilakukan.

---

## Slide 24 - Saran Penelitian Selanjutnya

### Judul

**Analisis dapat dikembangkan menggunakan data dan metode yang lebih lengkap**

### Isi

- Menggunakan data SKU, harga satuan, kuantitas, stok gudang, dan lead time.
- Menguji model time series:
  - Moving Average
  - Exponential Smoothing
  - ARIMA
  - Prophet
- Mengevaluasi model menggunakan MAE, RMSE, atau MAPE.
- Mengembangkan segmentasi RFM dan K-Means.
- Menguji pengaruh promosi, kota, dan jenis toko.
- Membuat dashboard interaktif menggunakan Power BI atau Tableau.
- Mengevaluasi efektivitas bundling setelah diterapkan.

---

## Slide 25 - Kesimpulan

### Judul

**Analisis transaksi menghasilkan prioritas produk, pelanggan, waktu, dan persediaan**

### Isi

1. Toothpaste merupakan produk dengan frekuensi tertinggi, yaitu 73.324 kemunculan.
2. Penjualan tertinggi dari bulan lengkap terjadi pada Maret 2023.
3. Fall dan pukul 10.00 memiliki nilai tertinggi, tetapi tidak dominan.
4. High Value menghasilkan sekitar 75,6% total penjualan.
5. Toothpaste memiliki estimasi target persediaan tertinggi, yaitu 342.
6. Dashboard berhasil mengintegrasikan hasil analisis.
7. Hasil bundling ditambahkan setelah Market Basket Analysis selesai.

### Kalimat Penutup

> Big Data Analytics membantu mengubah satu juta transaksi menjadi insight yang dapat digunakan untuk mendukung keputusan pemasaran, pelanggan, operasional, dan persediaan.

---

# Catatan Penggunaan Kode

Kode Python lengkap tidak perlu dimasukkan ke dalam PPT. Presentasi sebaiknya menampilkan:

- Alur metode
- Rumus sederhana
- Grafik output
- Angka penting
- Interpretasi
- Rekomendasi

Notebook Google Colab tetap disiapkan apabila dosen meminta demonstrasi atau bukti proses analisis.

# Pembagian Presentasi

## Bagian Bersama

- Sampul
- Latar belakang
- Identifikasi masalah
- Tujuan
- Dataset
- Preprocessing
- Kesimpulan umum
- Keterbatasan dan saran

## Aul

- KPI penjualan
- Metode segmentasi
- Distribusi segmentasi
- Karakteristik segmen
- Dashboard penjualan

## Lidwina

- Produk unggulan
- Tren penjualan bulanan
- Pola musim
- Jam ramai
- Metode prediksi stok
- Hasil dan interpretasi rekomendasi stok

## Fayza

- Market Basket Analysis
- Support, confidence, dan lift
- Aturan asosiasi terbaik
- Rekomendasi bundling dan cross-selling

