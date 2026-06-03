Bisa, saya akan pecah rangkuman UAS ini menjadi 3 bagian seperti ini:

**Part 1 sekarang:** fondasi Big Data dan pipeline analitik  
Meliputi jenis data, sumber data, karakteristik big data, data analytics lifecycle, persiapan data, ETL modern vs tradisional, data lake vs data warehouse, dan contoh studi kasus awal.

**Part 2 nanti:** ekosistem pemrosesan Big Data  
Meliputi Hadoop, HDFS, YARN, MapReduce, command Hadoop, Hive, internal/external table, query Hive, Apache Spark, RDD transformation/action, Spark MLlib.

**Part 3 nanti:** machine learning dan studi kasus Big Data Analytics  
Meliputi supervised vs unsupervised learning, clustering, K-Means, klasifikasi, precision & recall, serta contoh kasus/permasalahan dan solusi.

Catatan penting dulu: saya bisa membaca hampir semua materi, termasuk PDF, PPTX, dan TXT. Namun [Diskusi Kelompok.pdf](<C:/Users/lidwina/Downloads/Big Ah Data/Diskusi Kelompok.pdf>) belum bisa saya baca sebagai teks karena 4 halamannya terdeteksi kosong secara ekstraksi teks. Jadi Part 1 ini memakai sumber yang terbaca seperti `01 Intro.pdf`, `02 Sumber Data.pdf`, `03 Pengambilan Data (1).pdf`, `1. Pengantar-Big-Data.pdf`, `10 Persiapan Data.pdf`, `Airbyte_vs_NiFi_BigData.pptx`, dan materi terkait lain.

**PART 1 — Fondasi Big Data dan Pipeline Analitik**

**1. Konsep Dasar Big Data**

Big Data adalah kumpulan data yang ukurannya sangat besar, bentuknya beragam, datang sangat cepat, dan biasanya tidak bisa lagi ditangani secara efektif memakai sistem tradisional biasa. Intinya bukan hanya “data besar”, tetapi data yang membutuhkan arsitektur, metode penyimpanan, pemrosesan, dan analitik yang lebih modern.

Dalam materi, Big Data dikaitkan dengan kebutuhan untuk menghasilkan insight atau nilai bisnis dari data. Jadi, data yang besar belum tentu berguna kalau tidak bisa diolah menjadi informasi yang bermakna.

Contoh sumber Big Data:
- Aktivitas media sosial seperti posting, komentar, like, share.
- Transaksi e-commerce dan perbankan.
- Sensor IoT, log mesin, data penerbangan, radar.
- Website log, clickstream, aplikasi mobile.
- Data medis, citra, teks, suara, dan video.
- Data organisasi seperti database operasional, CSV, laporan, ERP/CRM.

Contoh Big Data Analytics:
- Rekomendasi produk di e-commerce.
- Deteksi fraud transaksi keuangan.
- Analisis sentimen media sosial.
- Prediksi kerusakan mesin dari sensor.
- Segmentasi pelanggan.
- Analisis data kesehatan untuk diagnosis/prediksi risiko.

**2. Karakteristik Big Data: 5V**

Materi menekankan karakteristik Big Data dengan konsep **5V**: Volume, Velocity, Variety, Veracity, dan Value.

**Volume** berarti ukuran data sangat besar. Data bisa berupa dataset raksasa, atau data kecil-kecil yang terus terkumpul dalam waktu panjang. Contoh: log transaksi harian, data sensor tiap detik, data media sosial, data penerbangan.

Yang perlu diingat: masalah volume membuat penyimpanan dan pemrosesan tradisional tidak cukup. Maka muncul sistem terdistribusi seperti Hadoop, HDFS, Spark, dan NoSQL.

**Velocity** berarti kecepatan data masuk, tersimpan, diproses, dan dianalisis. Dalam Big Data, data sering datang terus-menerus, bahkan real-time. Contoh: data klik pengguna, stream transaksi, sensor kendaraan, monitoring server.

Implikasinya: sistem harus mampu batch processing atau real-time/stream processing. Batch cocok untuk data historis besar; real-time cocok untuk keputusan cepat seperti fraud detection.

**Variety** berarti bentuk data beragam. Data tidak hanya tabel rapi, tetapi juga JSON, XML, teks, gambar, video, log, audio, data sensor, dan sebagainya.

Variety penting karena Big Data sering menggabungkan data dari banyak sumber. Tantangannya adalah integrasi, preprocessing, transformasi, dan pemilihan format penyimpanan yang fleksibel.

**Veracity** berarti kualitas, kebenaran, dan kepercayaan terhadap data. Data besar sering mengandung noise, data hilang, duplikasi, outlier, inkonsistensi, atau data dari sumber yang tidak sepenuhnya terpercaya.

Contoh masalah veracity:
- Nama pelanggan ditulis berbeda-beda.
- Data sensor error.
- Nilai transaksi kosong.
- Komentar media sosial ambigu.
- Data duplikat dari beberapa sistem.

**Value** berarti nilai/manfaat yang dihasilkan dari Big Data. Ini yang paling penting. Data besar tidak otomatis bernilai; nilai muncul setelah data diolah menjadi insight, prediksi, rekomendasi, efisiensi, atau keputusan.

Contoh value:
- Perusahaan tahu produk mana yang harus direkomendasikan.
- Bank bisa mendeteksi transaksi mencurigakan.
- Rumah sakit bisa memprediksi risiko pasien.
- Pemerintah bisa memahami pola kemacetan.

**3. Data Terstruktur, Semi-Terstruktur, dan Tidak Terstruktur**

Dalam materi `02 Sumber Data.pdf`, data dibagi berdasarkan struktur.

**Data terstruktur** adalah data yang memiliki format tetap, panjang/kolom jelas, dan biasanya mudah dimasukkan ke tabel. Contohnya database relasional, CSV, spreadsheet, data transaksi, data pelanggan.

Ciri-ciri:
- Skema jelas.
- Kolom dan tipe data terdefinisi.
- Mudah diproses dengan SQL.
- Cocok untuk RDBMS dan data warehouse.

Contoh:
```text
id_pelanggan | nama | umur | total_transaksi
001          | Ani  | 21   | 500000
```

**Data tidak terstruktur** adalah data yang tidak punya format tabel tetap dan biasanya lebih sulit langsung dianalisis. Contohnya foto, video, audio, teks bebas, radar, dokumen, posting media sosial.

Ciri-ciri:
- Tidak punya skema tetap.
- Sulit diproses langsung dengan SQL biasa.
- Perlu preprocessing atau ekstraksi fitur.
- Sering jumlahnya dominan dalam Big Data.

Contoh:
```text
Review pelanggan: "Produknya bagus, tapi pengirimannya lama."
```

**Data semi-terstruktur** berada di tengah-tengah. Tidak serapi tabel relasional, tetapi punya metadata atau struktur penanda. Contohnya JSON, XML, YAML, data web, API response, dan data media sosial.

Contoh JSON:
```json
{
  "user": "ani",
  "produk": "sepatu",
  "rating": 5
}
```

Poin UAS yang mungkin keluar:  
Data terstruktur cocok untuk RDBMS/data warehouse. Data tidak terstruktur dan semi-terstruktur lebih cocok ditangani dengan pendekatan Big Data seperti data lake, NoSQL, Hadoop, Spark, atau pipeline ELT.

**4. Pembagian Sumber Data Big Data**

Materi membagi sumber data menjadi beberapa kelompok besar.

**Data dari organisasi**  
Contohnya database perusahaan, transaksi, data pelanggan, data inventori, laporan penjualan, sistem ERP/CRM.

**Data dari mesin**  
Contohnya sensor suhu, sensor tekanan, log server, data IoT, data kendaraan, data mesin industri.

**Data dari manusia**  
Contohnya posting media sosial, komentar, ulasan produk, pencarian web, email, dokumen, aktivitas klik.

Dalam Big Data, sering kali ketiganya digabung. Misalnya pada e-commerce:
- Data organisasi: riwayat transaksi.
- Data mesin: log klik dan waktu akses.
- Data manusia: review produk dan rating.

Hasil gabungannya bisa dipakai untuk rekomendasi produk, segmentasi pelanggan, prediksi churn, atau deteksi fraud.

**5. Data Analytics Lifecycle**

Data analytics lifecycle adalah tahapan dari masalah bisnis sampai hasil analitik digunakan. Di materi, istilah ini muncul berdekatan dengan pengambilan data, preprocessing, persiapan data, cleaning, transformation, dan knowledge discovery.

Versi ringkas yang cocok untuk UAS:

1. **Business understanding / problem definition**  
   Tentukan masalah yang ingin dijawab. Misalnya: “Bagaimana memprediksi pelanggan yang akan berhenti berlangganan?”

2. **Data acquisition / pengumpulan data**  
   Ambil data dari berbagai sumber: database, API, log, sensor, media sosial, file CSV, data warehouse, data lake.

3. **Data storage / penyimpanan data**  
   Simpan data di tempat yang sesuai. Data terstruktur bisa masuk RDBMS/data warehouse. Data mentah besar dan beragam bisa masuk data lake/HDFS/object storage.

4. **Data preparation / preprocessing**  
   Bersihkan dan siapkan data. Ini termasuk handling missing value, duplikasi, noise, outlier, transformasi format, normalisasi, encoding, dan integrasi data.

5. **Exploration / exploratory data analysis**  
   Pahami pola data: distribusi, korelasi, tren, anomali, segmentasi awal.

6. **Modeling / analytics**  
   Terapkan metode analitik atau machine learning. Contohnya klasifikasi, clustering, prediksi, rekomendasi.

7. **Evaluation**  
   Ukur apakah hasilnya bagus. Untuk klasifikasi bisa pakai precision, recall, accuracy, F1-score. Untuk clustering bisa pakai cohesion/separation atau evaluasi interpretasi cluster.

8. **Communication / insight delivery**  
   Sajikan hasil dalam dashboard, laporan, visualisasi, atau rekomendasi.

9. **Operationalization**  
   Terapkan model/pipeline ke sistem nyata. Misalnya model fraud detection berjalan real-time di transaksi.

Inti lifecycle: Big Data Analytics bukan hanya menjalankan algoritma, tetapi proses end-to-end dari masalah, data, pembersihan, analisis, evaluasi, sampai pemanfaatan.

**6. Persiapan Data: Data Preparation**

Dari materi `10 Persiapan Data.pdf`, persiapan data mencakup:

- Pengumpulan data.
- Data cleaning.
- Data transformation.
- Mengenal tipe data.
- Memahami distribusi data.

**Data cleaning** bertujuan memperbaiki data yang bermasalah:
- Missing value: nilai kosong/hilang.
- Invalid value: nilai tidak valid, misalnya umur `-5`.
- Duplicate data: baris ganda.
- Noise: gangguan atau data tidak relevan.
- Outlier: nilai ekstrem yang jauh dari pola normal.

**Data transformation** mengubah data agar siap dianalisis:
- Mengubah format tanggal.
- Normalisasi skala angka.
- Encoding kategori menjadi angka.
- Agregasi data harian menjadi bulanan.
- Menggabungkan data dari beberapa sumber.

Contoh:
```text
Sebelum: "03 Juni 2026"
Sesudah: 2026-06-03
```

Kenapa preparation penting? Karena model analitik sebagus apa pun akan buruk kalau datanya kotor. Dalam konteks Big Data, masalah ini makin besar karena sumber datanya banyak, formatnya beragam, dan volumenya tinggi.

**7. ETL Tradisional vs ETL/ELT Modern**

Materi `03 Pengambilan Data (1).pdf` membahas ETL vs ELT. Ini penting karena sering muncul di Big Data.

**ETL = Extract, Transform, Load**

Alurnya:
```text
Sumber Data -> Extract -> Transform -> Load -> Data Warehouse
```

Pada ETL tradisional, data diambil dari sumber, dibersihkan/diubah dulu, baru dimasukkan ke storage tujuan. Biasanya cocok untuk data yang sudah cukup terstruktur dan kebutuhan laporan yang jelas.

Kelebihan ETL:
- Data yang masuk ke warehouse sudah rapi.
- Cocok untuk BI/reporting tradisional.
- Kualitas data lebih dikontrol sebelum masuk.

Kekurangan ETL:
- Kurang fleksibel untuk data mentah yang besar dan beragam.
- Transformasi di awal bisa lambat.
- Jika kebutuhan analitik berubah, pipeline perlu banyak penyesuaian.

**ELT = Extract, Load, Transform**

Alurnya:
```text
Sumber Data -> Extract -> Load -> Transform di storage/engine besar
```

Pada ELT modern, data dimasukkan dulu ke storage besar seperti data lake/cloud warehouse, lalu transformasi dilakukan setelahnya menggunakan engine seperti Spark, Hadoop, BigQuery, Snowflake, atau tools pipeline modern.

Kelebihan ELT:
- Cocok untuk data besar, semi-terstruktur, dan tidak terstruktur.
- Data mentah tetap disimpan sehingga bisa dianalisis ulang.
- Transformasi bisa paralel dan scalable.
- Lebih fleksibel untuk eksplorasi data.

Kekurangan ELT:
- Lebih kompleks.
- Butuh tata kelola data yang baik.
- Kalau tidak dikelola, data lake bisa menjadi “data swamp” atau tempat data berantakan.

Dari slide, ELT disebut lebih cocok untuk data tidak terstruktur dan transformasi/loading bisa paralel. Ini nyambung dengan Big Data karena pemrosesan dilakukan oleh sistem terdistribusi.

**8. ETL Modern vs ETL Tradisional**

Selain ETL vs ELT, kisi-kisi menyebut **ETL modern vs ETL tradisional**. Ini bisa dijawab seperti ini.

**ETL tradisional** biasanya:
- Fokus ke data terstruktur.
- Sumber data terbatas, misalnya RDBMS internal.
- Target utama adalah data warehouse.
- Transformasi dilakukan sebelum loading.
- Umumnya batch harian/mingguan.
- Dipakai untuk laporan BI yang stabil.

**ETL modern** biasanya:
- Mendukung data terstruktur, semi-terstruktur, dan tidak terstruktur.
- Sumber data lebih banyak: API, SaaS, event stream, log, IoT, media sosial.
- Target bisa data lake, cloud warehouse, lakehouse.
- Mendukung ELT, streaming, CDC, dan pipeline otomatis.
- Lebih scalable dan cloud-native.
- Cocok untuk analytics, machine learning, dan real-time decision.

Contoh dari PPT `Airbyte_vs_NiFi_BigData.pptx`:
- **Airbyte** digunakan untuk integrasi data modern dengan connector, cocok untuk sinkronisasi data dari banyak sumber ke warehouse/lake.
- **Apache NiFi** digunakan untuk data flow automation, ingestion, routing, transformation ringan, dan cocok untuk aliran data kompleks/real-time.

Perbedaan singkat:
```text
Tradisional: data dirapikan dulu -> masuk warehouse -> laporan
Modern: data dikumpulkan dari banyak sumber -> masuk lake/warehouse -> diproses scalable -> analytics/ML
```

**9. Data Lake vs Data Warehouse**

Ini tidak selalu panjang di slide, tapi sangat relevan dengan kisi-kisi dan nyambung dengan ETL/ELT.

**Data Warehouse** adalah penyimpanan data terstruktur yang sudah bersih, terintegrasi, dan siap untuk query/reporting. Biasanya digunakan untuk Business Intelligence, dashboard, laporan manajemen, dan analisis historis.

Ciri data warehouse:
- Schema-on-write: struktur ditentukan sebelum data masuk.
- Data sudah diproses dan rapi.
- Cocok untuk SQL dan laporan.
- Kualitas data lebih terkontrol.
- Biasanya menyimpan data terstruktur.

Contoh penggunaan:
- Laporan penjualan bulanan.
- Dashboard performa bisnis.
- Analisis revenue per wilayah.

**Data Lake** adalah penyimpanan besar untuk data mentah dalam berbagai format. Data bisa disimpan dulu apa adanya, lalu diproses ketika dibutuhkan.

Ciri data lake:
- Schema-on-read: struktur diterapkan saat data dibaca/dianalisis.
- Bisa menyimpan data mentah.
- Cocok untuk Big Data, machine learning, eksplorasi, data tidak terstruktur.
- Bisa menyimpan CSV, JSON, log, gambar, audio, video, parquet, dan lain-lain.
- Butuh metadata dan governance agar tidak berantakan.

Contoh penggunaan:
- Menyimpan log klik mentah.
- Menyimpan data sensor IoT.
- Menyimpan dokumen teks untuk NLP.
- Menyimpan data historis besar untuk training ML.

Perbandingan cepat:
```text
Data Warehouse = data sudah rapi, untuk BI/reporting.
Data Lake = data mentah/beragam, untuk eksplorasi, Big Data, ML.
```

Untuk UAS, jawaban bagusnya:  
Data warehouse cocok ketika kebutuhan analisis sudah jelas dan datanya terstruktur. Data lake cocok ketika data sangat besar, bervariasi, dan belum tentu langsung diketahui akan dianalisis seperti apa.

**10. Big Data vs Business Intelligence Tradisional**

Dari materi pengantar, ada perbedaan antara pendekatan tradisional dan Big Data/Data Science.

**BI tradisional**:
- Banyak memakai data terstruktur.
- Fokus pada laporan masa lalu dan kondisi saat ini.
- Pertanyaan umum: “Apa yang terjadi?”
- Contoh: dashboard penjualan bulan lalu.

**Big Data Analytics/Data Science**:
- Memakai data terstruktur dan tidak terstruktur.
- Dataset lebih besar dan lebih beragam.
- Fokus juga pada prediksi, optimasi, dan eksplorasi.
- Pertanyaan umum: “Apa yang akan terjadi?”, “Mengapa terjadi?”, “Apa tindakan optimal?”
- Contoh: prediksi churn pelanggan, rekomendasi produk, deteksi fraud.

Ringkasnya:
```text
BI menjelaskan masa lalu.
Big Data Analytics membantu memahami masa lalu, memprediksi masa depan, dan memberi rekomendasi tindakan.
```

**11. Komputasi Terdistribusi sebagai Dasar Big Data**

Materi `6 Komputasi Terdistribusi.pdf` menghubungkan Big Data dengan kebutuhan sistem terdistribusi karena masalah utama Big Data adalah volume dan velocity.

Komputasi terdistribusi berarti pekerjaan dibagi ke banyak komputer independen yang bekerja bersama. Tujuannya:
- Skalabilitas.
- Fault tolerance.
- Berbagi sumber daya.
- Pemrosesan paralel.
- Penyimpanan data besar.

Ada dua konsep scaling:
- **Scale up:** meningkatkan kapasitas satu mesin, misalnya RAM/CPU lebih besar.
- **Scale out:** menambah jumlah mesin/node. Ini lebih umum di Big Data.

Big Data cenderung memakai scale out karena lebih fleksibel dan murah untuk data sangat besar. Hadoop dan Spark bekerja dengan konsep ini: data dan pemrosesan dibagi ke beberapa node.

**12. Contoh Studi Kasus dan Solusi Big Data Analytics**

Karena dosen menekankan contoh kasus, ini beberapa contoh yang bisa dipakai saat UAS.

**Kasus 1: E-commerce ingin meningkatkan rekomendasi produk**

Masalah:
- Data pelanggan sangat besar.
- Ada data transaksi, klik, pencarian, rating, dan review.
- Data berupa tabel, log, dan teks.

Solusi:
- Simpan data mentah di data lake.
- Gunakan ETL/ELT untuk mengintegrasikan transaksi dan clickstream.
- Bersihkan data duplikat dan missing value.
- Gunakan analytics/ML untuk rekomendasi produk.
- Hasilnya dipakai untuk personalisasi halaman utama.

Konsep yang terkait:
Volume, variety, data lake, ELT, preprocessing, machine learning.

**Kasus 2: Bank ingin mendeteksi fraud transaksi**

Masalah:
- Transaksi masuk sangat cepat.
- Fraud harus dideteksi secepat mungkin.
- Data berasal dari transaksi, lokasi, perangkat, histori nasabah.

Solusi:
- Gunakan pipeline real-time/streaming.
- Simpan histori transaksi di data warehouse/lake.
- Buat model klasifikasi untuk membedakan transaksi normal vs fraud.
- Evaluasi dengan precision dan recall.
- Recall penting agar fraud tidak banyak lolos; precision penting agar nasabah normal tidak terlalu sering diblokir.

Konsep terkait:
Velocity, veracity, classification, precision, recall, real-time analytics.

**Kasus 3: Pabrik ingin prediksi kerusakan mesin**

Masalah:
- Sensor menghasilkan data tiap detik.
- Data sangat besar dan terus bertambah.
- Kerusakan harus diprediksi sebelum mesin berhenti.

Solusi:
- Data sensor masuk ke data lake.
- Cleaning untuk sensor error/noise.
- Transformasi menjadi fitur seperti rata-rata suhu, tekanan maksimum, getaran.
- Model prediksi/anomaly detection digunakan untuk preventive maintenance.

Konsep terkait:
Machine-generated data, velocity, volume, preprocessing, distributed processing.

**Kasus 4: Analisis sentimen media sosial**

Masalah:
- Data komentar sangat banyak dan tidak terstruktur.
- Bahasa informal, typo, emoji, noise.
- Perusahaan ingin tahu opini publik.

Solusi:
- Ambil data dari API/media sosial.
- Lakukan preprocessing teks: cleaning, tokenisasi, normalisasi.
- Klasifikasi sentimen positif/negatif/netral.
- Visualisasikan tren sentimen per waktu.

Konsep terkait:
Unstructured data, variety, veracity, classification, data preprocessing.

**13. Hafalan Cepat Part 1**

Kalau besok muncul soal pendek, pakai jawaban inti ini:

- Big Data = data sangat besar, cepat, beragam, kualitasnya menantang, dan harus menghasilkan nilai.
- 5V = Volume, Velocity, Variety, Veracity, Value.
- Data terstruktur = tabel/skema jelas, contoh RDBMS/CSV.
- Data semi-terstruktur = ada metadata/format fleksibel, contoh JSON/XML/YAML.
- Data tidak terstruktur = tidak punya format tetap, contoh teks, gambar, video, audio.
- ETL = transformasi dulu baru load, cocok untuk data warehouse tradisional.
- ELT = load dulu baru transform, cocok untuk Big Data/data lake/cloud.
- Data warehouse = data rapi untuk BI/reporting.
- Data lake = data mentah beragam untuk Big Data/ML/eksplorasi.
- Data analytics lifecycle = problem definition, acquisition, storage, preparation, exploration, modeling, evaluation, communication, operationalization.
- Komputasi terdistribusi diperlukan karena satu mesin tidak cukup untuk volume dan velocity Big Data.

Nanti saat Anda minta **prompt 2**, saya lanjutkan ke bagian yang lebih teknis: Hadoop, HDFS, YARN, MapReduce, command Hadoop, Hive, Spark, RDD transformation/action, dan Spark MLlib.

**PART 2 — Hadoop, Hive, Spark, dan Ekosistem Pemrosesan Big Data**

Part 2 ini fokus ke bagian teknis dari kisi-kisi dosen: **Hadoop, HDFS, YARN, MapReduce, command Hadoop, Hive, internal/external table, query Hive, Apache Spark, RDD transformation/action, dan Spark MLlib**.

Sumber yang paling relevan: `07 Hadoop.pdf`, `08 MapReduce YARN.pdf`, `Pengantar-Hadoop.pdf`, `07-Hive.pdf`, `Pengantar HIVE.ppt.pdf`, `Hive - A Warehousing Solution Over a Map-Reduce.pdf`, `11 Spark.pdf`, dan `Airbyte_vs_NiFi_BigData.pptx`.

**1. Kenapa Hadoop Dibutuhkan**

Hadoop muncul karena data yang sangat besar tidak bisa lagi disimpan dan diproses secara efisien oleh satu komputer biasa atau sistem tradisional.

Masalah utama Big Data:
- Data terlalu besar untuk satu mesin.
- Data datang dari banyak sumber dan format.
- Analisis data besar butuh waktu lama jika diproses serial.
- Dibutuhkan sistem yang murah, scalable, dan fault-tolerant.

Hadoop menjawab dua kebutuhan utama:

```text
1. Bagaimana menyimpan data sangat besar secara andal?
2. Bagaimana memproses/menganalisis data besar tersebut?
```

Jawabannya:
- Penyimpanan: **HDFS**
- Pemrosesan: **MapReduce**
- Manajemen resource: **YARN**

Hadoop cocok digunakan ketika:
- Ukuran data besar.
- Data berasal dari berbagai sumber.
- Butuh pemrosesan batch skala besar.
- Ingin memakai cluster komputer biasa/commodity hardware.
- Butuh integrasi dengan alat Big Data lain seperti Hive, Spark, Pig, Sqoop, Flume.

Hadoop kurang cocok untuk:
- Real-time analytics dengan latency sangat rendah.
- Pengganti database transaksi harian.
- Banyak file kecil.
- Query kecil yang butuh respons sangat cepat seperti OLTP.

**2. Komponen Utama Ekosistem Hadoop**

Dari slide, komponen Hadoop meliputi:

- **HDFS**: penyimpanan data terdistribusi.
- **YARN**: manajemen sumber daya cluster.
- **MapReduce**: pemrosesan data batch.
- **Hive**: SQL di atas Hadoop.
- **Pig**: scripting untuk data flow.
- **Spark**: in-memory processing.
- **Zookeeper/Ambari**: manajemen dan koordinasi.
- **Flume/Sqoop**: pemindahan/ingestion data.

Ringkasnya:

```text
HDFS      = tempat menyimpan data besar.
YARN      = pengatur CPU/RAM/resource cluster.
MapReduce = model pemrosesan batch.
Hive      = query SQL-like untuk data Hadoop.
Spark     = pemrosesan cepat berbasis memory.
```

**3. Arsitektur Hadoop Cluster**

Hadoop cluster adalah kumpulan node/komputer yang saling terhubung. Arsitekturnya memakai pola **master-slave**.

Tabel penting dari materi:

```text
Komponen   | Master            | Slave
-----------|-------------------|----------------
HDFS       | NameNode          | DataNode
YARN       | ResourceManager   | NodeManager
MapReduce  | JobTracker*       | TaskTracker*
```

Catatan: `JobTracker` dan `TaskTracker` adalah istilah Hadoop MapReduce versi lama. Pada Hadoop modern, peran manajemen job lebih banyak ditangani YARN lewat `ResourceManager`, `NodeManager`, dan `ApplicationMaster`.

**4. HDFS: Hadoop Distributed File System**

**HDFS** adalah sistem file terdistribusi untuk menyimpan data besar di banyak node dalam cluster.

Konsep penting:
- File besar dipecah menjadi beberapa **block**.
- Block disimpan di beberapa **DataNode**.
- Metadata block disimpan oleh **NameNode**.
- Block biasanya direplikasi agar fault-tolerant.
- HDFS cocok untuk file besar, bukan banyak file kecil.

Contoh dari materi:
- File `Foo.txt` ukuran 300 MB.
- Jika block HDFS 128 MB, maka file akan dipecah menjadi beberapa block.
- Tiap block bisa direplikasi 3 kali di node berbeda.

**NameNode**:
- Master HDFS.
- Menyimpan metadata.
- Mengetahui file terdiri dari block apa saja.
- Mengetahui block disimpan di DataNode mana.
- Tidak menyimpan isi file sebenarnya.

**DataNode**:
- Slave HDFS.
- Menyimpan block data sebenarnya.
- Membaca dan menulis block.
- Mengirim laporan block secara periodik ke NameNode.

Analogi gampang:
```text
NameNode = katalog/perpustakaan pusat yang tahu lokasi buku.
DataNode = rak-rak tempat buku sebenarnya disimpan.
```

Kalau client ingin membaca file:
1. Client bertanya ke NameNode: “Block file ini ada di mana?”
2. NameNode mengembalikan lokasi block.
3. Client membaca block langsung dari DataNode.

Kalau client ingin menulis file:
1. Client meminta izin ke NameNode.
2. File dipecah menjadi block.
3. Block ditulis ke beberapa DataNode.
4. Replikasi dilakukan agar data tetap aman jika node mati.

**5. Block dan Replication di HDFS**

HDFS memecah file besar menjadi block. Ukuran block bisa 64 MB atau 128 MB tergantung konfigurasi.

Kenapa memakai block besar?
- Mengurangi overhead metadata.
- Cocok untuk sequential read/write file besar.
- Mendukung pemrosesan paralel.

Replication adalah penyalinan block ke beberapa node. Misalnya replication factor = 3, berarti setiap block punya 3 salinan di node berbeda.

Manfaat replication:
- Fault tolerance.
- Jika satu DataNode mati, data masih ada di node lain.
- Membantu pemrosesan dekat dengan lokasi data.

Konsep penting: **data locality**.  
Hadoop berusaha memproses data di node yang menyimpan data tersebut, agar tidak perlu memindahkan data besar lewat jaringan.

**6. YARN: Yet Another Resource Negotiator**

**YARN** adalah sistem manajemen sumber daya Hadoop. Tugasnya mengatur penggunaan CPU, memory, dan eksekusi aplikasi di cluster.

Komponen utama YARN:
- **ResourceManager**
- **NodeManager**
- **ApplicationMaster**
- **Container**

**ResourceManager**:
- Satu per cluster.
- Mengatur pembagian resource.
- Memiliki Scheduler dan Applications Manager.
- Menentukan aplikasi dapat resource berapa.

**NodeManager**:
- Berjalan di setiap node worker.
- Mengawasi resource di node tersebut.
- Menjalankan container.
- Melaporkan status ke ResourceManager.

**ApplicationMaster**:
- Dibuat untuk setiap aplikasi/job.
- Mengatur eksekusi job tertentu.
- Meminta container ke ResourceManager.
- Mengawasi task dari aplikasi tersebut.

**Container**:
- Paket resource berupa CPU dan memory.
- Tempat task dijalankan.

Alur kerja YARN:
```text
Client submit aplikasi
-> ResourceManager menerima request
-> ResourceManager membuat ApplicationMaster
-> ApplicationMaster meminta container
-> NodeManager menjalankan task dalam container
-> Status dikirim balik sampai job selesai
```

YARN penting karena memungkinkan beberapa engine berjalan dalam satu Hadoop cluster:
- MapReduce
- Spark
- Tez
- Hive
- Streaming
- Interactive SQL

**7. MapReduce**

**MapReduce** adalah model pemrosesan data besar secara paralel. Ia membagi pekerjaan menjadi dua tahap utama:

```text
Map -> Shuffle/Sort -> Reduce
```

**Map phase**:
- Membaca input.
- Memproses data menjadi pasangan key-value.
- Contoh word count: setiap kata diberi nilai 1.

**Shuffle and Sort**:
- Mengelompokkan data berdasarkan key.
- Semua value dari key yang sama dikumpulkan.

**Reduce phase**:
- Menggabungkan value untuk setiap key.
- Contoh word count: menjumlahkan semua angka 1 untuk tiap kata.

Contoh Word Count:

Input:
```text
big data
big analytics
```

Map output:
```text
(big, 1)
(data, 1)
(big, 1)
(analytics, 1)
```

Shuffle:
```text
big -> [1, 1]
data -> [1]
analytics -> [1]
```

Reduce output:
```text
big -> 2
data -> 1
analytics -> 1
```

Inti MapReduce:
- Data diproses paralel.
- Cocok untuk batch processing.
- Tahan terhadap kegagalan node.
- Kurang cocok untuk proses iteratif cepat karena banyak read/write ke disk.

**8. Cara Teknis MapReduce Bekerja**

Secara teknis:
1. File input berada di HDFS.
2. File dipecah menjadi block.
3. Map task dijalankan sedekat mungkin dengan lokasi block.
4. Mapper menghasilkan pasangan key-value.
5. Output mapper di-shuffle dan di-sort berdasarkan key.
6. Reducer menerima semua value untuk key tertentu.
7. Reducer menghasilkan output final.
8. Output disimpan kembali ke HDFS.

Poin yang sering ditanyakan:
- Mapper bekerja pada potongan data.
- Reducer menggabungkan hasil berdasarkan key.
- Shuffle/sort adalah tahap mahal karena memindahkan data antar node.
- MapReduce cocok untuk batch, bukan real-time.

**9. Command Hadoop / HDFS yang Perlu Dihafal**

HDFS tidak diakses seperti folder biasa di OS. User mengaksesnya lewat command line.

Format umum:
```bash
hdfs dfs [command] [path]
```

Command penting:

Melihat isi direktori:
```bash
hdfs dfs -ls /
hdfs dfs -ls /user/hduser
```

Membuat direktori:
```bash
hdfs dfs -mkdir /user/hduser/input
hdfs dfs -mkdir -p /user/hduser/wordcount/input
```

Upload file dari local ke HDFS:
```bash
hdfs dfs -put data.txt /user/hduser/input/
hdfs dfs -copyFromLocal data.txt /user/hduser/input/
```

Melihat isi file:
```bash
hdfs dfs -cat /user/hduser/input/data.txt
```

Download file dari HDFS ke local:
```bash
hdfs dfs -get /user/hduser/output/part-r-00000 hasil.txt
hdfs dfs -copyToLocal /user/hduser/output ./output
```

Menghapus file/direktori:
```bash
hdfs dfs -rm /user/hduser/input/data.txt
hdfs dfs -rm -r /user/hduser/output
```

Melihat ukuran file:
```bash
hdfs dfs -du -h /user/hduser
```

Menampilkan beberapa baris akhir:
```bash
hdfs dfs -tail /user/hduser/input/data.txt
```

Menjalankan contoh MapReduce WordCount:
```bash
hadoop jar hadoop-mapreduce-examples.jar wordcount /input /output
```

Poin praktis:
- Output directory MapReduce biasanya **tidak boleh sudah ada**. Kalau `/output` sudah ada, job bisa gagal.
- HDFS path berbeda dengan local path.
- `-put` untuk upload, `-get` untuk download, `-cat` untuk baca isi file.

**10. Hive**

**Hive** adalah data warehousing infrastructure di atas Hadoop. Hive memungkinkan user menjalankan query mirip SQL terhadap data besar di HDFS.

Dari materi:
- Hive dikembangkan oleh Facebook.
- Hive menggunakan bahasa **HiveQL/HQL**.
- Hive menerjemahkan query HiveQL menjadi job MapReduce atau engine lain.
- Hive cocok untuk summarization, ad-hoc query, reporting, dan analisis data besar.

Hive berguna karena MapReduce sulit diprogram langsung. Dengan Hive, user bisa menulis query seperti SQL.

Contoh:
```sql
SELECT product, COUNT(*)
FROM transaksi
GROUP BY product;
```

Query seperti itu bisa diterjemahkan menjadi pekerjaan MapReduce di cluster.

Hive bukan:
- Bukan OLTP.
- Bukan sistem real-time.
- Tidak cocok untuk transaksi kecil seperti insert/update per baris terus-menerus.
- Latency lebih tinggi dibanding RDBMS biasa.

Hive cocok untuk:
- Batch processing.
- Query data besar.
- Analisis historis.
- Data warehouse berbasis Hadoop.

**11. Arsitektur Hive**

Komponen Hive:
- **Command Line Interface / Web Interface**
- **JDBC/ODBC**
- **Thrift Server**
- **Driver**
- **Compiler**
- **Optimizer**
- **Executor**
- **Metastore**
- **HDFS**

**Metastore**:
- Menyimpan metadata.
- Metadata meliputi database, table, column, partition, lokasi data.
- Biasanya disimpan di RDBMS tradisional.
- Penting karena data fisik ada di HDFS, tetapi struktur tabelnya disimpan di metastore.

**Driver**:
- Mengelola lifecycle query HiveQL.
- Menjaga session dan statistik query.

**Compiler**:
- Mengubah HiveQL menjadi rencana eksekusi.
- Bisa menjadi DAG atau job MapReduce.

Alur query Hive:
```text
User menulis HiveQL
-> Driver menerima query
-> Compiler mengecek syntax dan metadata ke Metastore
-> Optimizer mengoptimalkan rencana
-> Executor menjalankan job di Hadoop
-> Hasil dikembalikan ke user
```

**12. Hive Data Model**

Hierarki data Hive:
```text
Database -> Table -> Partition -> Bucket
```

**Database**:
- Namespace untuk mengelompokkan tabel.

**Table**:
- Struktur data seperti tabel SQL.

**Partition**:
- Membagi data berdasarkan kolom tertentu.
- Contoh: tanggal, negara, kategori.
- Membuat query lebih cepat karena Hive tidak perlu membaca semua data.

Contoh partition:
```text
/warehouse/log/ds=2026-06-03/country=ID/
```

**Bucket**:
- Membagi data lebih lanjut berdasarkan hash kolom tertentu.
- Berguna untuk sampling dan join tertentu.

**13. Internal Table vs External Table di Hive**

Ini bagian penting dari kisi-kisi.

**Internal table / managed table**:
- Hive mengelola metadata dan data.
- Data biasanya disimpan di warehouse Hive, misalnya `/user/hive/warehouse`.
- Jika tabel di-drop, metadata dan data ikut dihapus.

Contoh:
```sql
CREATE TABLE mahasiswa (
  nim STRING,
  nama STRING,
  prodi STRING
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ',';
```

Jika dijalankan:
```sql
DROP TABLE mahasiswa;
```

Maka data tabel juga bisa ikut hilang karena dikelola Hive.

**External table**:
- Hive hanya mengelola metadata.
- Data berada di lokasi eksternal, misalnya folder HDFS tertentu.
- Jika tabel di-drop, metadata hilang, tetapi data asli tetap ada.

Contoh:
```sql
CREATE EXTERNAL TABLE log_web (
  ip STRING,
  waktu STRING,
  url STRING
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
LOCATION '/data/log_web/';
```

Jika dijalankan:
```sql
DROP TABLE log_web;
```

Yang hilang hanya definisi tabel di metastore, data di `/data/log_web/` tetap ada.

Ringkasnya:
```text
Internal table: DROP table -> metadata dan data dihapus.
External table: DROP table -> hanya metadata dihapus, data tetap ada.
```

Gunakan internal table jika data memang dikelola penuh oleh Hive.  
Gunakan external table jika data dipakai juga oleh sistem lain atau ingin data tetap aman.

**14. Query Hive yang Perlu Dikuasai**

Membuat database:
```sql
CREATE DATABASE uas_bigdata;
USE uas_bigdata;
```

Melihat database/tabel:
```sql
SHOW DATABASES;
SHOW TABLES;
```

Membuat tabel:
```sql
CREATE TABLE transaksi (
  id STRING,
  produk STRING,
  jumlah INT,
  harga DOUBLE
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ',';
```

Load data:
```sql
LOAD DATA INPATH '/user/hduser/transaksi.csv'
INTO TABLE transaksi;
```

Query dasar:
```sql
SELECT * FROM transaksi;
```

Filter:
```sql
SELECT *
FROM transaksi
WHERE jumlah > 10;
```

Agregasi:
```sql
SELECT produk, SUM(jumlah) AS total_jumlah
FROM transaksi
GROUP BY produk;
```

Join:
```sql
SELECT t.id, t.produk, p.kategori
FROM transaksi t
JOIN produk p
ON t.produk = p.nama_produk;
```

Membuat external table:
```sql
CREATE EXTERNAL TABLE transaksi_ext (
  id STRING,
  produk STRING,
  jumlah INT
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
LOCATION '/data/transaksi/';
```

Melihat struktur tabel:
```sql
DESCRIBE transaksi;
DESCRIBE EXTENDED transaksi;
```

Menghapus tabel:
```sql
DROP TABLE transaksi;
```

**15. Hive Schema-on-Read**

Hive memakai konsep **schema-on-read**.

Artinya:
- Data bisa disimpan dulu di HDFS.
- Struktur/schema diterapkan saat data dibaca/query.
- Ini berbeda dengan RDBMS yang biasanya schema-on-write.

Schema-on-write:
```text
Data harus cocok dengan schema sebelum masuk.
```

Schema-on-read:
```text
Data disimpan dulu, schema diterapkan saat dibaca.
```

Keuntungan schema-on-read:
- Lebih fleksibel.
- Cocok untuk data besar dan beragam.
- Data mentah bisa dianalisis dengan beberapa schema berbeda.

Kekurangannya:
- Query bisa lebih lambat.
- Jika schema salah, hasil query bisa kacau.
- Butuh disiplin metadata.

**16. Apache Spark**

**Apache Spark** adalah framework komputasi Big Data berbasis **in-memory cluster computing**. Spark dibuat untuk pemrosesan data besar yang lebih cepat dan lebih mudah dibanding MapReduce dalam banyak kasus.

Dari materi `11 Spark.pdf`:
- Spark adalah framework komputasi pada in-memory cluster.
- Spark memiliki arsitektur driver, cluster manager, worker node, executor, dan task.
- Spark memakai konsep RDD.
- Spark mendukung lazy operations.

Spark sering dianggap lebih cepat dari MapReduce karena:
- Banyak operasi dilakukan di memory.
- Cocok untuk pemrosesan iteratif.
- API lebih mudah digunakan.
- Mendukung batch, streaming, SQL, machine learning, graph processing.

Komponen Spark:
- **Spark Core**
- **Spark SQL**
- **Spark Streaming**
- **Spark MLlib**
- **GraphX**

**17. Arsitektur Spark**

Komponen utama:
- **Driver Program**
- **Cluster Manager**
- **Worker Node**
- **Executor**
- **Task**

**Driver Program**:
- Program utama.
- Membuat SparkContext/SparkSession.
- Membagi job menjadi task.
- Mengatur alur eksekusi.

**Cluster Manager**:
- Mengatur resource cluster.
- Bisa standalone, YARN, Mesos, Kubernetes.

**Worker Node**:
- Node yang menjalankan executor.

**Executor**:
- Proses yang menjalankan task.
- Menyimpan data di memory/cache.

**Task**:
- Unit kerja terkecil yang dijalankan executor.

Alur sederhana:
```text
Driver membuat job
-> Cluster Manager menyediakan resource
-> Executor berjalan di Worker Node
-> Task diproses paralel
-> Hasil dikirim kembali ke Driver
```

**18. RDD: Resilient Distributed Dataset**

RDD adalah struktur data dasar di Spark.

Dari materi:
- RDD = kumpulan elemen data yang terpartisi.
- Immutable.
- Terpartisi.
- Bisa diproses in-memory.
- Mendukung fault tolerance.

Penjelasan:

**Resilient**:
- Tahan terhadap kegagalan.
- Jika partisi hilang, Spark bisa membangun ulang dari lineage.

**Distributed**:
- Data tersebar di banyak node.

**Dataset**:
- Kumpulan data.

**Immutable**:
- RDD tidak bisa diubah langsung.
- Operasi pada RDD menghasilkan RDD baru.

Contoh:
```python
rdd = sc.textFile("hdfs:///data/log.txt")
```

**19. Lazy Evaluation di Spark**

Spark memakai **lazy evaluation**.

Artinya:
- Transformation tidak langsung dieksekusi.
- Spark hanya mencatat rencana operasi.
- Eksekusi benar-benar terjadi ketika action dipanggil.

Contoh:
```python
rdd = sc.textFile("data.txt")
words = rdd.flatMap(lambda line: line.split(" "))
pairs = words.map(lambda word: (word, 1))
```

Sampai sini belum dieksekusi.

Eksekusi terjadi saat:
```python
pairs.count()
```

Manfaat lazy evaluation:
- Spark bisa mengoptimalkan rencana eksekusi.
- Mengurangi operasi yang tidak perlu.
- Lebih efisien untuk pipeline panjang.

**20. RDD Transformation**

Transformation adalah operasi yang menghasilkan RDD baru. Karena lazy, transformation tidak langsung mengeksekusi job.

Contoh transformation penting:

`map()`  
Mengubah setiap elemen.
```python
rdd.map(lambda x: x * 2)
```

`filter()`  
Memilih elemen yang memenuhi kondisi.
```python
rdd.filter(lambda x: x > 10)
```

`flatMap()`  
Mengubah satu elemen menjadi banyak elemen.
```python
lines.flatMap(lambda line: line.split(" "))
```

`distinct()`  
Menghapus duplikasi.
```python
rdd.distinct()
```

`union()`  
Menggabungkan dua RDD.
```python
rdd1.union(rdd2)
```

`groupByKey()`  
Mengelompokkan value berdasarkan key.
```python
pairs.groupByKey()
```

`reduceByKey()`  
Menggabungkan value berdasarkan key.
```python
pairs.reduceByKey(lambda a, b: a + b)
```

`sortByKey()`  
Mengurutkan berdasarkan key.
```python
pairs.sortByKey()
```

Poin UAS:  
`reduceByKey()` biasanya lebih efisien daripada `groupByKey()` untuk agregasi karena bisa menggabungkan sebagian data sebelum shuffle.

**21. RDD Action**

Action adalah operasi yang memicu eksekusi dan menghasilkan nilai akhir atau menyimpan output.

Contoh action penting:

`collect()`  
Mengambil semua data ke driver.
```python
rdd.collect()
```

Hati-hati: jangan pakai `collect()` untuk data sangat besar.

`count()`  
Menghitung jumlah elemen.
```python
rdd.count()
```

`take(n)`  
Mengambil n elemen pertama.
```python
rdd.take(10)
```

`first()`  
Mengambil elemen pertama.
```python
rdd.first()
```

`reduce()`  
Menggabungkan semua elemen.
```python
rdd.reduce(lambda a, b: a + b)
```

`saveAsTextFile()`  
Menyimpan hasil ke file/HDFS.
```python
rdd.saveAsTextFile("hdfs:///output")
```

Ringkas:
```text
Transformation = menghasilkan RDD baru, lazy.
Action = menjalankan eksekusi dan menghasilkan output.
```

**22. Contoh Word Count di Spark**

Contoh klasik Spark:

```python
lines = sc.textFile("hdfs:///input/data.txt")

counts = (
    lines
    .flatMap(lambda line: line.split(" "))
    .map(lambda word: (word, 1))
    .reduceByKey(lambda a, b: a + b)
)

counts.saveAsTextFile("hdfs:///output/wordcount")
```

Penjelasan:
- `textFile()` membaca file dari HDFS.
- `flatMap()` memecah baris menjadi kata.
- `map()` membuat pasangan `(kata, 1)`.
- `reduceByKey()` menjumlahkan kata yang sama.
- `saveAsTextFile()` menyimpan hasil dan memicu eksekusi.

Transformation:
```text
flatMap, map, reduceByKey
```

Action:
```text
saveAsTextFile
```

**23. Spark vs Hadoop MapReduce**

Perbandingan penting:

```text
MapReduce:
- Batch processing.
- Banyak read/write ke disk.
- Lebih lambat untuk proses iteratif.
- Cocok untuk job besar yang sederhana dan stabil.

Spark:
- In-memory processing.
- Lebih cepat untuk iterative processing.
- API lebih mudah.
- Mendukung SQL, streaming, MLlib.
- Cocok untuk machine learning dan analytics modern.
```

Kenapa Spark cepat?
- Data bisa disimpan di memory.
- Tidak selalu harus menulis hasil antara ke disk.
- DAG execution engine lebih fleksibel.

Namun Spark bukan pengganti total HDFS/Hadoop. Spark bisa berjalan di atas HDFS dan bisa memakai YARN sebagai cluster manager.

**24. Spark MLlib**

**MLlib** adalah library machine learning di Spark. Dipakai untuk menjalankan algoritma ML pada data besar secara terdistribusi.

MLlib mendukung:
- Classification.
- Regression.
- Clustering.
- Collaborative filtering.
- Feature extraction.
- Pipeline machine learning.
- Evaluation metric.

Contoh algoritma:
- Logistic Regression.
- Decision Tree.
- Random Forest.
- K-Means.
- Naive Bayes.
- ALS recommendation.

Kenapa MLlib penting di Big Data?
- Dataset besar tidak muat di satu mesin.
- Training model bisa diparalelkan.
- Terintegrasi dengan Spark SQL/DataFrame.
- Cocok untuk pipeline analytics modern.

Contoh penggunaan konseptual:
```text
Data transaksi pelanggan
-> preprocessing dengan Spark
-> feature extraction
-> training model K-Means/Classification di MLlib
-> evaluasi
-> simpan hasil cluster/prediksi
```

**25. Airbyte dan Apache NiFi dalam Ekosistem Big Data**

Dari PPT `Airbyte_vs_NiFi_BigData.pptx`, Airbyte dan NiFi berperan pada ingestion/integrasi data.

**Airbyte**:
- Fokus pada konektor sumber dan target.
- Cocok untuk sinkronisasi data dari banyak sumber ke data warehouse/data lake.
- Mendukung batch/incremental sync.
- Bisa memakai DBT atau pipeline custom untuk transformasi.
- Berbasis Docker/Kubernetes untuk skalabilitas.

**Apache NiFi**:
- Berbasis flow-based programming.
- Memiliki UI drag-and-drop untuk desain data flow.
- Cocok untuk routing, ingestion, transformasi ringan, batch maupun real-time.
- Memakai konsep FlowFile, Processor, dan Connection.
- Bisa terintegrasi dengan Kafka, HDFS, dan sistem lain.

Dalam pipeline Big Data:
```text
Airbyte/NiFi -> Data Lake/HDFS/Warehouse -> Spark/Hive -> Analytics/ML
```

Jadi Airbyte/NiFi bukan pengganti Hadoop/Spark/Hive, tetapi membantu memindahkan dan mengatur aliran data menuju sistem analitik.

**26. Alur Big Data End-to-End Menggunakan Hadoop, Hive, Spark**

Contoh alur lengkap:

```text
1. Data dikumpulkan dari database, API, log, sensor.
2. Airbyte/NiFi mengalirkan data ke HDFS atau data lake.
3. HDFS menyimpan data besar secara terdistribusi.
4. Hive membuat tabel agar data bisa di-query dengan SQL-like syntax.
5. Spark memproses data lebih cepat untuk transformasi/ML.
6. MLlib dipakai untuk clustering/klasifikasi.
7. Hasil disimpan kembali ke HDFS/warehouse.
8. Dashboard/laporan/model digunakan untuk keputusan.
```

Contoh kasus:
- Data log web masuk ke HDFS.
- Hive dipakai untuk query jumlah akses per halaman.
- Spark dipakai untuk memproses session pengguna.
- MLlib dipakai untuk segmentasi pengguna.
- Hasil dipakai untuk rekomendasi konten.

**27. Jawaban Singkat yang Siap Dipakai Saat UAS**

Kalau ditanya **apa itu HDFS**:
> HDFS adalah sistem file terdistribusi Hadoop yang menyimpan file besar dalam bentuk block di banyak DataNode, sementara metadata lokasinya dikelola oleh NameNode. HDFS mendukung replikasi agar fault-tolerant.

Kalau ditanya **fungsi NameNode dan DataNode**:
> NameNode menyimpan metadata file dan lokasi block, sedangkan DataNode menyimpan block data sebenarnya.

Kalau ditanya **apa itu YARN**:
> YARN adalah resource manager Hadoop yang mengatur CPU, memory, container, dan eksekusi aplikasi di cluster melalui ResourceManager, NodeManager, dan ApplicationMaster.

Kalau ditanya **cara kerja MapReduce**:
> MapReduce memproses data besar dengan tahap Map untuk menghasilkan key-value, Shuffle/Sort untuk mengelompokkan key, dan Reduce untuk menggabungkan value menjadi output akhir.

Kalau ditanya **Hive itu apa**:
> Hive adalah data warehouse infrastructure di atas Hadoop yang memungkinkan query data besar di HDFS menggunakan HiveQL, lalu query tersebut dikompilasi menjadi job MapReduce atau engine eksekusi lain.

Kalau ditanya **internal vs external table Hive**:
> Internal table dikelola penuh oleh Hive, sehingga DROP TABLE dapat menghapus metadata dan data. External table hanya metadatanya dikelola Hive, sehingga DROP TABLE hanya menghapus metadata, sementara data di lokasi HDFS tetap ada.

Kalau ditanya **Spark itu apa**:
> Spark adalah framework pemrosesan Big Data berbasis in-memory cluster computing yang lebih cepat untuk proses iteratif dan mendukung SQL, streaming, machine learning, dan graph processing.

Kalau ditanya **RDD transformation vs action**:
> Transformation menghasilkan RDD baru dan lazy, contohnya map, filter, flatMap, reduceByKey. Action memicu eksekusi dan menghasilkan output, contohnya count, collect, take, reduce, saveAsTextFile.

**28. Hafalan Cepat Part 2**

```text
Hadoop = framework Big Data untuk storage dan processing terdistribusi.
HDFS = storage terdistribusi.
NameNode = metadata.
DataNode = block data.
YARN = resource manager.
ResourceManager = pengatur resource cluster.
NodeManager = pengatur resource per node.
ApplicationMaster = pengatur aplikasi/job.
Container = paket CPU + memory.
MapReduce = Map -> Shuffle/Sort -> Reduce.
Hive = SQL-like query di atas Hadoop.
Metastore = metadata Hive.
Internal table = data dikelola Hive.
External table = data tetap di lokasi eksternal.
Spark = in-memory distributed processing.
RDD = immutable, partitioned, distributed dataset.
Transformation = lazy, menghasilkan RDD baru.
Action = memicu eksekusi.
MLlib = machine learning library di Spark.
```

Nanti untuk **Part 3**, bagian yang akan saya rangkum adalah: supervised vs unsupervised learning, clustering, K-Means, MapReduce K-Means, klasifikasi Big Data, precision & recall, serta contoh studi kasus dan solusi sesuai penekanan dosen.

**PART 3 — Machine Learning, Klasifikasi, Clustering, K-Means, Precision-Recall, dan Studi Kasus Big Data Analytics**

Bagian ini melanjutkan Part 1 dan Part 2. Fokusnya adalah sisi analitik/ML dari Big Data: **supervised vs unsupervised learning, clustering, K-Means, klasifikasi, precision & recall, serta contoh studi kasus dan solusi**.

**1. Supervised vs Unsupervised Learning**

**Supervised learning** adalah pembelajaran mesin dengan data berlabel. Artinya, setiap data latih sudah punya jawaban/kelas target.

Contoh:
```text
Data transaksi -> label: fraud / bukan fraud
Data email -> label: spam / bukan spam
Data pasien -> label: sakit / sehat
```

Tujuannya adalah membuat model yang bisa memprediksi label untuk data baru.

Algoritma supervised learning:
- Decision Tree
- Random Forest
- Naive Bayes
- Support Vector Machine
- k-Nearest Neighbor
- Logistic Regression
- Neural Network

Tugas umum supervised learning:
- **Klasifikasi**: output berupa kategori, misalnya fraud/tidak fraud.
- **Regresi**: output berupa angka, misalnya prediksi harga rumah.

**Unsupervised learning** adalah pembelajaran mesin dengan data tanpa label. Model mencari pola tersembunyi dari data.

Contoh:
```text
Data pelanggan tanpa label -> dikelompokkan menjadi beberapa segmen
Data transaksi tanpa label -> dicari pola transaksi tidak biasa
```

Algoritma unsupervised learning:
- K-Means
- Hierarchical Clustering
- DBSCAN
- Fuzzy C-Means
- PCA untuk reduksi dimensi

Tugas umum unsupervised learning:
- Clustering
- Dimensionality reduction
- Anomaly detection
- Association pattern

Jawaban pendek UAS:
> Supervised learning memakai data berlabel untuk memprediksi kelas/nilai, sedangkan unsupervised learning memakai data tanpa label untuk menemukan pola atau kelompok tersembunyi.

**2. Klasifikasi dalam Big Data**

Klasifikasi adalah proses memasukkan data ke kelas tertentu berdasarkan pola dari data historis. Dalam Big Data, klasifikasi menjadi lebih menantang karena data punya volume besar, format beragam, dan sering tidak seimbang.

Contoh klasifikasi:
- Email: spam atau bukan spam.
- Transaksi: fraud atau normal.
- Pasien: risiko tinggi atau rendah.
- Komentar: positif, negatif, netral.
- Gambar medis: tumor atau tidak tumor.

Tahapan klasifikasi Big Data dari materi TXT:
1. **Data acquisition**: mengumpulkan data dari banyak sumber.
2. **Preprocessing**: membersihkan noise, missing value, duplikasi.
3. **Feature selection/extraction**: memilih fitur penting.
4. **Data classification**: menjalankan model klasifikasi.
5. **Knowledge discovery**: mengambil insight dari hasil model.

Klasifikasi konvensional vs klasifikasi Big Data:
```text
Konvensional:
- Data lebih kecil.
- Biasanya berjalan di satu mesin.
- Format data lebih sederhana.
- Proses relatif lebih mudah dikontrol.

Big Data:
- Data sangat besar.
- Perlu komputasi paralel/distribusi.
- Data bisa terstruktur, semi-terstruktur, tidak terstruktur.
- Perlu Spark/Hadoop/MLlib agar scalable.
```

Tantangan klasifikasi Big Data:
- Volume data besar.
- Banyak fitur/dimensi.
- Data tidak seimbang, misalnya fraud hanya 1% dari transaksi.
- Data noisy dan tidak lengkap.
- Komputasi mahal.
- Model kompleks seperti deep learning sulit diinterpretasi.

**3. Precision, Recall, Accuracy, dan Confusion Matrix**

Untuk klasifikasi, jangan hanya hafal accuracy. Dosen menulis khusus **precision & recall**, jadi ini penting.

Confusion matrix:

```text
                  Prediksi Positif   Prediksi Negatif
Aktual Positif    TP                 FN
Aktual Negatif    FP                 TN
```

Keterangan:
- **TP (True Positive)**: model memprediksi positif dan benar.
- **TN (True Negative)**: model memprediksi negatif dan benar.
- **FP (False Positive)**: model memprediksi positif padahal salah.
- **FN (False Negative)**: model memprediksi negatif padahal seharusnya positif.

**Accuracy**:
```text
Accuracy = (TP + TN) / (TP + TN + FP + FN)
```
Mengukur total prediksi yang benar. Masalahnya, accuracy bisa menipu pada data tidak seimbang.

Contoh: dari 1000 transaksi, hanya 10 fraud. Model yang selalu bilang “bukan fraud” punya accuracy 99%, tapi sebenarnya gagal mendeteksi fraud.

**Precision**:
```text
Precision = TP / (TP + FP)
```
Dari semua yang diprediksi positif, berapa yang benar-benar positif.

Precision penting jika false positive mahal.  
Contoh: sistem fraud terlalu sering menandai transaksi normal sebagai fraud, nasabah bisa terganggu.

**Recall**:
```text
Recall = TP / (TP + FN)
```
Dari semua data yang sebenarnya positif, berapa yang berhasil ditemukan model.

Recall penting jika false negative berbahaya.  
Contoh: pada diagnosis penyakit, fraud detection, atau keamanan cyber, kasus positif yang lolos bisa sangat merugikan.

**F1-score**:
```text
F1 = 2 * (Precision * Recall) / (Precision + Recall)
```
Dipakai saat ingin menyeimbangkan precision dan recall.

Contoh hitung cepat:
```text
TP = 80, FP = 20, FN = 40, TN = 860

Precision = 80 / (80 + 20) = 0.80
Recall    = 80 / (80 + 40) = 0.67
Accuracy  = (80 + 860) / 1000 = 0.94
```

Interpretasi:
- Accuracy tinggi, 94%.
- Precision bagus, 80%.
- Recall masih kurang, hanya 67%, berarti masih banyak positif yang lolos.

**4. Clustering**

Clustering adalah teknik unsupervised learning untuk mengelompokkan data berdasarkan kemiripan. Data dalam cluster yang sama harus lebih mirip satu sama lain dibanding data di cluster berbeda.

Contoh clustering:
- Segmentasi pelanggan.
- Pengelompokan dokumen.
- Pengelompokan wilayah kemacetan.
- Deteksi pola kriminal.
- Pengelompokan pasien berdasarkan gejala.
- Pengelompokan produk berdasarkan perilaku pembelian.

Tujuan clustering:
```text
Menemukan struktur/pola tersembunyi tanpa label kelas.
```

Jenis metode clustering dari materi:
- **Partitioning-based**: contoh K-Means.
- **Hierarchical-based**: agglomerative/divisive.
- **Density-based**: contoh DBSCAN.
- **Grid-based**.
- **Model-based**.
- **Fuzzy clustering**.

Dalam Big Data, clustering tradisional sulit karena:
- Data sangat besar.
- Dimensi tinggi.
- Banyak noise.
- Tidak cukup dijalankan di satu mesin.
- Perlu parallel/distributed processing seperti Spark atau MapReduce.

**5. K-Means Clustering**

K-Means adalah algoritma clustering yang membagi data menjadi **K cluster**. K ditentukan di awal oleh user.

Langkah K-Means dari materi:
1. Tentukan jumlah cluster `K`.
2. Inisialisasi centroid awal, biasanya random.
3. Untuk setiap data, hitung jaraknya ke setiap centroid.
4. Masukkan data ke cluster dengan centroid terdekat.
5. Hitung ulang centroid berdasarkan rata-rata anggota cluster.
6. Ulangi sampai centroid stabil/konvergen atau mencapai batas iterasi.

Contoh sederhana:
```text
K = 2
Data pelanggan dikelompokkan menjadi:
Cluster 1 = pelanggan murah/hemat
Cluster 2 = pelanggan premium
```

Rumus jarak yang umum dipakai adalah Euclidean distance:
```text
d(x, c) = sqrt((x1-c1)^2 + (x2-c2)^2 + ... + (xn-cn)^2)
```

Kelebihan K-Means:
- Sederhana.
- Cepat.
- Mudah dipahami.
- Cocok untuk data numerik besar jika diparalelkan.

Kekurangan K-Means:
- Harus menentukan K di awal.
- Sensitif terhadap centroid awal.
- Sensitif terhadap outlier.
- Kurang cocok untuk cluster bentuk tidak bulat.
- Kurang baik untuk data kategorikal tanpa preprocessing.

**6. Hierarchical Clustering**

Hierarchical clustering membentuk struktur seperti pohon yang disebut **dendrogram**.

Dua pendekatan:
- **Agglomerative**: bottom-up, mulai dari tiap data sebagai cluster sendiri, lalu digabung bertahap.
- **Divisive**: top-down, mulai dari satu cluster besar, lalu dipecah bertahap.

Ukuran jarak antar cluster:
- **Single linkage**: jarak terdekat antar anggota cluster.
- **Complete linkage**: jarak terjauh antar anggota cluster.
- **Average linkage**: rata-rata jarak antar anggota cluster.

Kelebihan:
- Tidak selalu perlu menentukan jumlah cluster sejak awal.
- Memberi struktur hierarki yang mudah dianalisis.

Kekurangan:
- Mahal secara komputasi.
- Kurang cocok untuk data sangat besar tanpa optimasi.

**7. MapReduce K-Means**

Materi `2022 BDA 06 Mapreduce K-Means Clustering.pdf` membahas K-Means dalam konteks MapReduce.

Masalah K-Means pada Big Data:
- Data terlalu besar untuk satu mesin.
- Setiap iterasi harus menghitung jarak semua data ke centroid.
- Perlu paralelisasi.

Ide MapReduce K-Means:

**Mapper**:
- Membaca sebagian data.
- Menghitung jarak setiap data ke centroid.
- Mengirim data ke cluster terdekat.
- Output biasanya berupa `(cluster_id, data_point)`.

**Reducer**:
- Menerima semua data untuk cluster tertentu.
- Menghitung centroid baru.
- Output berupa centroid baru.

Alurnya:
```text
Centroid awal
-> Mapper: assign data ke centroid terdekat
-> Reducer: hitung centroid baru
-> Ulangi sampai konvergen
```

Kenapa cocok dengan MapReduce?
- Perhitungan jarak data ke centroid bisa diparalelkan.
- Data besar bisa dibagi ke banyak node.
- Output tiap iterasi disimpan dan dipakai untuk iterasi berikutnya.

Kelemahannya:
- K-Means bersifat iteratif.
- MapReduce kurang efisien untuk iterasi karena banyak baca/tulis ke disk.
- Spark biasanya lebih cocok karena bisa menyimpan data di memory.

**8. Spark untuk Clustering dan MLlib**

Spark MLlib mendukung algoritma machine learning terdistribusi, termasuk clustering dan klasifikasi.

Kenapa Spark cocok untuk ML?
- In-memory processing.
- Cocok untuk algoritma iteratif seperti K-Means.
- Bisa menangani data besar.
- Mendukung pipeline preprocessing, training, dan evaluasi.

Contoh alur K-Means di Spark:
```text
Data besar di HDFS/data lake
-> dibaca Spark
-> preprocessing
-> feature vector
-> K-Means MLlib
-> hasil cluster
-> evaluasi dan interpretasi
```

Konteks UAS:
> MapReduce bisa dipakai untuk K-Means, tetapi Spark lebih efisien untuk algoritma iteratif karena Spark dapat menyimpan data di memory dan mengurangi overhead baca/tulis disk.

**9. Big Data Classification: Teknik yang Muncul di Materi**

Dari materi klasifikasi TXT dan paper:

**Machine learning-based classification**
- Random Forest
- SVM
- kNN
- Naive Bayes
- Decision Tree

Kelebihan:
- Relatif mudah dipakai.
- Banyak algoritma dapat diinterpretasi.
- Cocok untuk data tabular.

Tantangan:
- Perlu feature engineering.
- Bisa berat untuk data sangat besar.
- Rentan terhadap data tidak seimbang.

**Deep learning-based classification**
- CNN
- RNN
- Deep Belief Network

Kelebihan:
- Bagus untuk data kompleks seperti gambar, teks, suara.
- Bisa melakukan ekstraksi fitur otomatis.

Tantangan:
- Butuh data dan komputasi besar.
- Sulit diinterpretasi.
- Training bisa lama.

**Rule-based classification**
- Memakai aturan eksplisit.
- Contoh: jika transaksi > 10 juta dan lokasi berbeda negara, tandai mencurigakan.

Kelebihan:
- Transparan.
- Mudah dijelaskan.

Kekurangan:
- Sulit menangani pola kompleks.
- Kurang fleksibel untuk data berdimensi tinggi.

**Optimization-based classification**
- Menggunakan metode optimasi untuk meningkatkan parameter/model.
- Bisa dipakai untuk memperbaiki performa model, tetapi sering lebih kompleks.

**10. Studi Kasus 1: Kemacetan Kota Malang**

Ini nyambung dengan `Diskusi Kelompok.txt`.

Masalah:
- Kemacetan di jalan sekitar kampus, pusat kota, atau area kuliner.
- Data bisa berasal dari sensor, CCTV, GPS kendaraan, Google Maps, laporan warga, media sosial.

Analisis 5V:
- **Volume**: banyak kendaraan dan titik jalan menghasilkan banyak data.
- **Velocity**: data lalu lintas berubah cepat, terutama jam sibuk.
- **Variety**: sensor, GPS, video CCTV, teks laporan, cuaca.
- **Veracity**: data bisa bias, sensor rusak, laporan warga tidak akurat.
- **Value**: prediksi macet, pengaturan lampu lalu lintas, rekomendasi rute.

Solusi Big Data:
```text
Data GPS/CCTV/sensor
-> ingestion real-time dengan NiFi/Kafka
-> simpan di data lake
-> Spark Streaming untuk analisis cepat
-> clustering titik kemacetan
-> model prediksi kepadatan
-> dashboard untuk Dishub/pengguna jalan
```

Metode:
- Clustering untuk menemukan hotspot kemacetan.
- Klasifikasi untuk menentukan status jalan: lancar, padat, macet.
- Prediksi time-series untuk jam macet.

**11. Studi Kasus 2: Data Universitas Brawijaya**

Dari diskusi kelompok, UB menghasilkan data dari:
- Formulir pendaftaran.
- Nilai akademik.
- Presensi.
- LMS.
- WiFi log.
- Perpustakaan.
- Media sosial mahasiswa.
- Data pembayaran.
- Data organisasi/kegiatan.
- Survey kepuasan.

Klasifikasi struktur:
```text
Terstruktur:
- NIM, nilai, presensi, pembayaran, data KRS.

Semi-terstruktur:
- Log LMS, JSON API, metadata dokumen, log WiFi.

Tidak terstruktur:
- Postingan media sosial, komentar, dokumen bebas, foto kegiatan.
```

Sumber:
```text
Organisasi: nilai, KRS, pembayaran.
Mesin: log WiFi, log LMS, presensi otomatis.
Manusia: komentar, survey, posting media sosial.
```

Permasalahan:
- Data tersebar di banyak sistem.
- Format berbeda.
- Privasi mahasiswa.
- Data tidak lengkap.
- Sulit integrasi antar fakultas/sistem.

Solusi:
- Data lake untuk menyimpan data beragam.
- ETL/ELT untuk integrasi.
- Hive/Spark untuk analisis.
- Dashboard akademik.
- Model klasifikasi untuk prediksi mahasiswa berisiko.
- Clustering untuk segmentasi pola belajar mahasiswa.

**12. Studi Kasus 3: Fraud Detection Bank**

Masalah:
- Transaksi sangat banyak dan cepat.
- Fraud jarang tetapi berdampak besar.
- Dataset tidak seimbang.

Solusi:
```text
Streaming transaksi
-> preprocessing dan feature extraction
-> model klasifikasi fraud
-> evaluasi precision-recall
-> alert transaksi mencurigakan
```

Kenapa precision dan recall penting?
- Recall tinggi: fraud tidak banyak lolos.
- Precision tinggi: transaksi normal tidak banyak salah blokir.

Trade-off:
```text
Jika recall dinaikkan, biasanya false positive bisa naik.
Jika precision dinaikkan, beberapa fraud mungkin lolos.
```

Dalam fraud detection, sering kali recall sangat penting, tetapi precision juga harus dijaga agar user tidak terganggu.

**13. Studi Kasus 4: Kesehatan / Data Medis**

Masalah:
- Data medis besar dan sensitif.
- Ada data terstruktur seperti usia, tekanan darah, hasil lab.
- Ada data tidak terstruktur seperti citra medis dan catatan dokter.

Solusi:
- Data lake dengan governance ketat.
- Preprocessing data medis.
- Klasifikasi penyakit.
- CNN untuk citra medis.
- Random Forest/SVM untuk data tabular.
- Evaluasi dengan precision, recall, sensitivity, specificity.

Poin penting:
- Recall/sensitivity penting agar pasien sakit tidak salah diklasifikasikan sehat.
- Precision penting agar tidak terlalu banyak false alarm.

**14. Studi Kasus 5: Rekomendasi Produk E-Commerce**

Masalah:
- Data klik, transaksi, rating, review, pencarian produk.
- Volume besar dan variety tinggi.

Solusi:
```text
Data transaksi + clickstream + review
-> data lake
-> Spark untuk preprocessing
-> clustering pelanggan
-> model rekomendasi
-> personalisasi produk
```

Metode:
- Clustering untuk segmentasi pelanggan.
- Classification untuk prediksi pelanggan akan membeli/tidak.
- NLP untuk review produk.
- Collaborative filtering untuk rekomendasi.

Value:
- Penjualan meningkat.
- Pengalaman pengguna lebih personal.
- Campaign marketing lebih tepat sasaran.

**15. Studi Kasus 6: Analisis Sentimen Media Sosial**

Masalah:
- Data teks tidak terstruktur.
- Banyak slang, typo, singkatan, emoji.
- Data datang cepat.

Solusi:
```text
Ambil data media sosial
-> cleaning teks
-> tokenisasi
-> klasifikasi sentimen positif/negatif/netral
-> dashboard tren sentimen
```

Tantangan:
- Veracity rendah.
- Sarkasme sulit dideteksi.
- Bahasa campuran.
- Data noisy.

Metode:
- Naive Bayes/SVM untuk baseline.
- Deep learning untuk data teks besar.
- Precision-recall untuk evaluasi tiap kelas sentimen.

**16. Studi Kasus 7: Prediksi Kerusakan Mesin / IoT**

Masalah:
- Sensor menghasilkan data terus-menerus.
- Data bisa sangat cepat dan besar.
- Tujuannya mencegah mesin rusak.

Solusi:
```text
Sensor IoT
-> stream ingestion
-> data lake/HDFS
-> Spark untuk feature extraction
-> klasifikasi status mesin normal/berisiko
-> alert preventive maintenance
```

Metode:
- Classification untuk status mesin.
- Clustering untuk pola operasi mesin.
- Anomaly detection untuk mendeteksi perilaku tidak normal.

Value:
- Downtime berkurang.
- Biaya maintenance lebih rendah.
- Kerusakan bisa dicegah.

**17. Cara Menjawab Soal Studi Kasus Big Data**

Kalau besok dosen memberi kasus bebas, pakai template ini:

```text
1. Jelaskan masalah.
2. Identifikasi sumber data.
3. Hubungkan ke 5V.
4. Tentukan arsitektur solusi.
5. Pilih metode analitik/ML.
6. Jelaskan evaluasi.
7. Jelaskan value/manfaat.
8. Sebutkan tantangan.
```

Contoh kerangka jawaban:
```text
Kasus: prediksi kemacetan.
Sumber data: GPS, CCTV, sensor jalan, laporan warga, cuaca.
5V: volume dari banyak kendaraan, velocity real-time, variety dari video/GPS/teks, veracity dari sensor/laporan, value untuk optimasi lalu lintas.
Solusi: ingestion dengan NiFi/Kafka, storage di data lake, Spark untuk pemrosesan, clustering hotspot macet, klasifikasi status jalan, dashboard.
Evaluasi: accuracy/precision/recall untuk klasifikasi, validasi hotspot untuk clustering.
Tantangan: privasi, kualitas sensor, integrasi data, biaya infrastruktur.
```

**18. Hafalan Cepat Part 3**

```text
Supervised learning = data berlabel, contoh klasifikasi fraud.
Unsupervised learning = data tanpa label, contoh clustering pelanggan.
Klasifikasi = memasukkan data ke kelas tertentu.
Clustering = mengelompokkan data berdasarkan kemiripan.
K-Means = tentukan K, pilih centroid, assign data, update centroid, ulangi.
Hierarchical clustering = membentuk dendrogram.
Precision = TP / (TP + FP).
Recall = TP / (TP + FN).
Accuracy bisa menipu jika data tidak seimbang.
F1-score menyeimbangkan precision dan recall.
MapReduce K-Means = mapper assign cluster, reducer hitung centroid baru.
Spark lebih cocok untuk ML iteratif karena in-memory.
MLlib = library machine learning di Spark.
```

**19. Penutup Super Ringkas untuk UAS**

Kalau harus menjelaskan hubungan semua materi dalam satu jawaban:

> Big Data Analytics dimulai dari data besar yang memiliki 5V. Data dikumpulkan dari berbagai sumber, disimpan di sistem seperti HDFS/data lake, lalu diproses memakai Hadoop, Hive, atau Spark. Setelah preprocessing, data dapat dianalisis dengan machine learning. Supervised learning dipakai untuk klasifikasi seperti fraud detection, sedangkan unsupervised learning dipakai untuk clustering seperti segmentasi pelanggan. Pada klasifikasi, performa model dievaluasi dengan precision dan recall, terutama saat data tidak seimbang. Pada clustering, K-Means mengelompokkan data berdasarkan kedekatan ke centroid dan dapat diparalelkan dengan MapReduce atau Spark untuk skala Big Data.