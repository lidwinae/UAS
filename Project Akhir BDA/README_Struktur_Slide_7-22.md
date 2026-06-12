# Struktur Presentasi Proyek Big Data Analytics

Dokumen ini berisi rancangan isi, visual, dan narasi presentasi mulai dari Slide 7 sampai Slide 22.

## Slide 7 - Peta Metodologi

### Judul

**Empat pendekatan analitik digunakan untuk menjawab masalah bisnis**

### Isi

| Fokus | Metode | Output |
|---|---|---|
| Produk dan waktu | Analisis deskriptif | Produk unggulan dan pola penjualan |
| Pelanggan | Segmentasi berbasis monetary | Segmen pelanggan dan dashboard |
| Asosiasi produk | Apriori | Kandidat bundling |
| Persediaan | Rata-rata permintaan dan safety stock | Rekomendasi stok |

### Visual

```text
Data Bersih
    |
    v
Analisis Deskriptif -> Segmentasi -> Apriori -> Prediksi Stok
    |
    v
Rekomendasi Bisnis
```

### Narasi

Setelah preprocessing, analisis dibagi menjadi empat bagian. Analisis deskriptif digunakan untuk mengetahui produk dan waktu penjualan, segmentasi untuk memahami pelanggan, Apriori untuk mengevaluasi bundling, serta prediksi sederhana untuk memperkirakan kebutuhan stok.

---

# Bagian Analisis Produk dan Waktu

Bagian ini dapat dibawakan Aul sebagai analisis pembuka kelompok, kemudian dilanjutkan ke tugas utama Aul.

## Slide 8 - Metode Analisis Produk dan Waktu

### Judul

**Analisis deskriptif digunakan untuk menemukan produk dan waktu penjualan utama**

### Isi

- Produk dipisahkan menggunakan `explode()`.
- Frekuensi kemunculan dihitung untuk setiap produk.
- Penjualan dikelompokkan berdasarkan bulan.
- Aktivitas dibandingkan berdasarkan musim.
- Jumlah transaksi dihitung untuk setiap jam.

### Narasi

Produk dalam setiap keranjang dipisahkan agar frekuensinya dapat dihitung. Selanjutnya, nilai penjualan dikelompokkan berdasarkan bulan dan musim, sedangkan jumlah transaksi dikelompokkan berdasarkan jam.

## Slide 9 - Produk Unggulan

### Judul

**Toothpaste menjadi produk yang paling sering muncul dalam transaksi**

### Visual

Masukkan grafik **Top 10 Most Purchased Products**.

### Insight

- Toothpaste muncul sebanyak **73.324 kali**.
- Ice Cream muncul sebanyak **37.094 kali**.
- Soap muncul sebanyak **37.076 kali**.
- Toothpaste juga paling banyak terkait dengan transaksi bernilai tinggi.
- Nilai transaksi terkait Toothpaste mencapai **$3.844.106,37**.

### Catatan

Nilai tersebut bukan pendapatan produk secara langsung karena harga satuan produk tidak tersedia.

### Narasi

Toothpaste mempunyai frekuensi kemunculan yang jauh lebih tinggi dibandingkan produk lainnya. Produk ini dapat diprioritaskan dalam pengawasan persediaan dan penempatan produk, tetapi nilai transaksinya tidak boleh dianggap sebagai revenue langsung produk.

## Slide 10 - Pola Penjualan Berdasarkan Waktu

### Judul

**Aktivitas penjualan relatif merata meskipun terdapat periode tertinggi**

### Visual

- Grafik total penjualan berdasarkan musim.
- Grafik jumlah transaksi berdasarkan jam.

### Isi

- Musim tertinggi: **Fall**
- Total penjualan Fall: **$13.136.913,71**
- Jam teramai: **10.00**
- Jumlah transaksi pukul 10.00: **42.021**
- Bulan lengkap tertinggi: **Maret 2023**
- Penjualan Maret 2023: **$1.033.556,59**

### Interpretasi

Selisih antar-musim dan antarjam relatif kecil sehingga aktivitas transaksi cenderung tersebar merata.

### Narasi

Fall dan pukul 10.00 memiliki nilai tertinggi. Namun, perbedaannya dengan periode lain tidak terlalu besar. Karena itu, hasil ini lebih tepat digunakan sebagai pertimbangan awal, bukan bukti adanya lonjakan musiman yang kuat.

---

# Bagian Aul

## Slide 11 - Metode Segmentasi Pelanggan

### Judul

**Pelanggan dikelompokkan berdasarkan total nilai transaksinya**

### Isi

- Data dikelompokkan berdasarkan `Customer_Name`.
- Frequency: jumlah transaksi pelanggan.
- Monetary: total nilai transaksi pelanggan.
- Monetary dibagi menjadi tiga kelompok menggunakan `qcut()`.
- Segmen terdiri dari Low Value, Medium Value, dan High Value.

### Narasi

Segmentasi sederhana dibentuk berdasarkan total pengeluaran atau monetary. Metode quantile membagi pelanggan ke dalam tiga kelompok dengan jumlah anggota yang hampir sama.

## Slide 12 - Hasil Segmentasi

### Judul

**High Value Customer memberikan kontribusi penjualan terbesar**

### Visual

- **Customer Segmentation Distribution**
- **Revenue Contribution by Segment**

### Hasil

| Segmen | Pelanggan | Total Penjualan |
|---|---:|---:|
| Low Value | 109.922 | $3.624.328,44 |
| Medium Value | 109.905 | $9.159.358,38 |
| High Value | 109.911 | $39.671.533,58 |

### Interpretasi

- Jumlah pelanggan hampir sama karena segmentasi menggunakan quantile.
- High Value menyumbang sekitar **75,6%** total penjualan.
- High Value menjadi prioritas program loyalitas dan retensi.

### Narasi

Jumlah pelanggan pada setiap segmen hampir sama karena dibentuk menggunakan quantile. Perbedaannya terlihat pada kontribusi penjualan, dengan High Value menghasilkan sekitar 75,6 persen dari total penjualan.

## Slide 13 - Dashboard Penjualan

### Judul

**Dashboard mengintegrasikan indikator utama penjualan dan pelanggan**

### Visual

Masukkan dashboard lengkap dari notebook.

### KPI

| Indikator | Nilai |
|---|---:|
| Total sales | $52.455.220,40 |
| Total transactions | 1.000.000 |
| Total customers | 329.738 |
| Average transaction value | $52,46 |

### Narasi

Dashboard menggabungkan KPI, produk unggulan, tren bulanan, kategori pelanggan, serta segmentasi. Tampilan ini membantu pengguna melihat kondisi penjualan secara ringkas dalam satu halaman.

---

# Bagian Fayza

## Slide 14 - Metode Apriori

### Judul

**Algoritma Apriori digunakan untuk mengevaluasi hubungan antarproduk**

### Isi

- Setiap transaksi diubah menjadi keranjang produk.
- Jumlah transaksi: **1.000.000**
- Produk unik: **81**
- Minimum support: **0,1%**
- Minimum confidence: **3%**
- Kombinasi dibatasi pada dua produk.
- Evaluasi menggunakan support, confidence, dan lift.

### Narasi

Apriori digunakan untuk mencari pasangan produk yang memenuhi batas minimum kemunculan. Kekuatan hubungan kemudian dinilai menggunakan support, confidence, dan lift.

## Slide 15 - Hasil Asosiasi Produk

### Judul

**Banana dan Butter menjadi kandidat bundling teratas**

### Visual

Masukkan grafik **Top 10 Kandidat Bundling Produk Berdasarkan Lift**.

### Hasil

| Metrik | Nilai |
|---|---:|
| Kandidat | Banana + Butter |
| Support | 0,1295% |
| Confidence | 3,61% |
| Lift | 0,9975 |
| Kemunculan bersama | Sekitar 1.295 transaksi |

### Narasi

Banana dan Butter memperoleh lift tertinggi. Namun, lift masih sedikit di bawah satu sehingga keduanya belum menunjukkan asosiasi pembelian positif yang kuat.

## Slide 16 - Interpretasi Bundling

### Judul

**Bundling direkomendasikan sebagai eksperimen, bukan keputusan permanen**

### Isi

- Tidak ditemukan aturan dengan `lift > 1`.
- Hubungan pembelian antarproduk relatif lemah.
- Banana dan Butter dapat diuji melalui promosi terbatas.
- Keberhasilan perlu diukur melalui perubahan transaksi dan penjualan.
- Bundling dihentikan apabila tidak memberikan peningkatan.

### Narasi

Hasil yang tidak menunjukkan asosiasi kuat tetap merupakan temuan penting. Bisnis sebaiknya tidak langsung menerapkan bundling secara luas. Kandidat terbaik dapat digunakan untuk A/B testing atau pilot promotion.

---

# Bagian Lidwina

## Slide 17 - Metode Prediksi Stok

### Judul

**Kebutuhan stok diperkirakan dari permintaan 30 hari lengkap terakhir**

### Isi

- Periode analisis: **18 April-17 Mei 2024**
- Permintaan didekati dengan frekuensi kemunculan produk.
- Prediksi dihitung dari rata-rata harian dikali tujuh hari.
- Safety stock mempertimbangkan variasi permintaan.
- Tingkat pengaman menggunakan faktor **1,65**.

### Rumus

```text
Prediksi 7 Hari = Rata-rata Harian x 7

Rekomendasi Stok = Prediksi 7 Hari + Safety Stock
```

### Narasi

Karena jumlah unit per produk tidak tersedia, frekuensi kemunculan digunakan sebagai pendekatan permintaan. Estimasi tujuh hari ditambah safety stock untuk mengantisipasi variasi harian.

## Slide 18 - Hasil Rekomendasi Stok

### Judul

**Toothpaste menjadi prioritas persediaan tertinggi**

### Visual

Masukkan grafik **Top 10 Estimasi Kebutuhan Stok Produk untuk 7 Hari**.

### Hasil Utama

| Produk | Prediksi 7 Hari | Safety Stock | Rekomendasi |
|---|---:|---:|---:|
| Toothpaste | 305,90 | 35,71 | 342 |
| Yogurt | 175,23 | 25,18 | 201 |
| Hair Gel | 170,80 | 23,51 | 195 |
| Salmon | 173,37 | 20,17 | 194 |
| Cereal Bars | 165,67 | 28,14 | 194 |

### Narasi

Toothpaste memiliki rata-rata kemunculan 43,7 kali per hari. Prediksi tujuh harinya sekitar 306 kemunculan dan setelah ditambah safety stock menghasilkan target persediaan sebesar 342.

## Slide 19 - Interpretasi Rekomendasi Stok

### Judul

**Rekomendasi stok berfungsi sebagai target persediaan awal**

### Isi

- Prioritaskan pemantauan Toothpaste.
- Siapkan stok pengaman untuk produk dengan variasi tinggi.
- Perbarui perhitungan secara berkala.
- Bandingkan estimasi dengan stok aktual.
- Hasil bukan jumlah pembelian yang mutlak.

### Narasi

Angka rekomendasi merupakan target persediaan sederhana, bukan jumlah barang yang harus langsung dipesan. Dalam penerapan nyata, perusahaan tetap harus mengurangi angka tersebut dengan stok gudang yang masih tersedia.

---

# Penutup Kelompok

## Slide 20 - Rekomendasi Bisnis

### Judul

**Hasil analisis diterjemahkan menjadi tindakan bisnis**

### Isi

- **Produk:** prioritaskan monitoring Toothpaste.
- **Operasional:** gunakan pukul 10.00 sebagai acuan awal penjadwalan.
- **Pelanggan:** fokuskan loyalitas pada High Value Customer.
- **Bundling:** uji Banana + Butter dalam promosi terbatas.
- **Stok:** gunakan prediksi tujuh hari dan safety stock sebagai target awal.

## Slide 21 - Keterbatasan

### Judul

**Hasil perlu dibaca sesuai dengan keterbatasan dataset**

### Isi

- Tidak tersedia harga dan jumlah unit setiap produk.
- Tidak tersedia data stok gudang dan lead time pemasok.
- `Customer_Name` digunakan sebagai identitas pelanggan.
- Segmentasi menggunakan pembagian quantile sederhana.
- Tidak ditemukan asosiasi produk dengan lift di atas satu.
- Data terakhir hanya sampai 18 Mei 2024 pukul 19.31.
- Hasil belum diuji menggunakan data operasional setelah rekomendasi.

## Slide 22 - Kesimpulan

### Judul

**Analisis menghasilkan insight produk, pelanggan, bundling, dan persediaan**

### Isi

- Toothpaste menjadi produk yang paling dominan.
- Aktivitas penjualan relatif merata antar-musim dan jam.
- High Value Customer memberikan kontribusi terbesar.
- Belum ditemukan asosiasi bundling yang kuat.
- Toothpaste menjadi prioritas rekomendasi stok.
- Rekomendasi dapat menjadi dasar eksperimen dan pengambilan keputusan awal.

---

# Urutan Pembicara

```text
Pembukaan Kelompok
        |
        v
Analisis Produk dan Waktu
        |
        v
Aul
        |
        v
Fayza
        |
        v
Lidwina
        |
        v
Penutup Kelompok
```
