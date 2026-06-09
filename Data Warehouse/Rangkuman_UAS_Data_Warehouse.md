# Rangkuman UAS Data Warehouse

Fokus rangkuman ini: materi PPT/PDF yang ada di folder untuk materi awal sampai SQL OLAP dan physical design. File TXT `Chapter7_extracted.txt` dan `Chapter 8.txt` sengaja belum dimasukkan sesuai instruksi.

Sumber yang dipakai:
- `01_Introduction To Data Warehouse.pptx`
- `02_Requirement And Planning DW.pptx`
- `02 - Inmon-vs-Kimball.pdf`
- `03 - Information Package.pptx`
- `04_LOGICAL DESIGN DW.pptx.pdf`
- `04_Slowly Changing Dimension.pptx`
- `Slide Transformasi Data.pptx`
- `06_Physical Design in Data Warehouse DB2 Syntax.pptx.pdf`
- `08_SQL OLAP.pdf`
- `08_SQL OLAP DB2.pptx`

---

## 1. Konsep Dasar Data Warehouse

### Mengapa organisasi membutuhkan data warehouse?

Organisasi besar biasanya memiliki banyak sumber data yang berbeda-beda. Masalah utamanya adalah:

- Sumber informasi heterogen: berbeda DBMS, format file, struktur data, interface, dan representasi data.
- Data tersebar dalam banyak sistem operasional seperti penjualan, keuangan, manufaktur, persediaan, supplier, dan lain-lain.
- Ada duplikasi data dan inkonsistensi data antar sistem.
- Sistem operasional dibangun berdasarkan kebutuhan aplikasi tertentu, sehingga terbentuk vertical stove pipes atau silo sistem.
- Manajemen sulit mendapatkan pandangan terpadu atas bisnis karena data tidak berada dalam satu repository yang konsisten.

Tujuan data warehouse adalah menyediakan akses terpadu terhadap data organisasi. Data dari berbagai sumber dikumpulkan, dibersihkan, diintegrasikan, disimpan, lalu disediakan kepada pengguna bisnis untuk analisis.

### Dua pendekatan integrasi data

#### 1. Query-driven approach atau lazy approach

Pada pendekatan ini, data tetap berada di sumber asal. Ketika pengguna menjalankan query, sistem integrasi mengambil data dari berbagai sumber secara langsung.

Kelebihan:
- Cocok untuk data yang sangat cepat berubah.
- Cocok jika sumber data sering berubah.
- Cocok jika volume data sangat besar dan tidak realistis dipindahkan semua.
- Cocok untuk kebutuhan pengguna yang tidak dapat diprediksi.

Kekurangan:
- Query lambat karena harus mengambil data dari banyak sumber saat itu juga.
- Jika sumber data lambat atau unavailable, hasil query ikut terganggu.
- Filtering dan integrasi dilakukan saat query berjalan, sehingga kompleks.
- Dapat mengganggu sistem operasional karena query analitik membebani sumber.
- Kurang populer di industri untuk kebutuhan analitik rutin.

#### 2. Warehouse approach atau eager approach

Pada pendekatan ini, data diekstrak lebih dulu dari sumber, dibersihkan, diintegrasikan, dan disimpan di data warehouse. Pengguna melakukan query langsung ke warehouse.

Kelebihan:
- Performa query analitik lebih tinggi.
- Tidak mengganggu sistem OLTP.
- Data dapat dimodifikasi, dianotasi, diringkas, dan direstrukturisasi.
- Dapat menyimpan data historis.
- Lebih cocok untuk analisis bisnis dan decision support.

Kekurangan:
- Data tidak selalu paling baru karena ada jeda proses extract/load.
- Membutuhkan proses ETL, storage, metadata, dan maintenance.

Intinya: warehouse approach paling umum dipakai di industri karena mendukung analisis kompleks tanpa membebani sistem transaksi.

---

## 2. Definisi Data Warehouse

### Definisi praktis

Data warehouse adalah penyimpanan data yang lengkap, konsisten, dan berasal dari berbagai sumber, lalu disediakan kepada end user dalam bentuk yang dapat dipahami dan digunakan dalam konteks bisnis.

### Definisi Inmon

Menurut W. H. Inmon, data warehouse adalah kumpulan data yang:

- Subject-oriented
- Integrated
- Time-variant
- Non-volatile

Data tersebut digunakan terutama untuk pengambilan keputusan organisasi.

### Definisi umum dalam BI

Data warehouse adalah database yang dirancang untuk aktivitas business intelligence. Fokusnya bukan transaksi harian, tetapi query, analisis, pelaporan, dan pemahaman performa organisasi.

---

## 3. Karakteristik Utama Data Warehouse

### 1. Subject-oriented

Data warehouse disusun berdasarkan subject area bisnis, bukan berdasarkan aplikasi operasional.

Contoh subject area:
- Perusahaan asuransi: customer, policy, premium, claim.
- Perusahaan manufaktur: product, order, vendor, bill of material, raw goods.
- Universitas: mahasiswa, dosen, mata kuliah, pembayaran, nilai, fakultas, program studi.

Makna penting: data warehouse mengelompokkan data berdasarkan topik yang penting untuk analisis manajemen.

### 2. Integrated

Data berasal dari banyak sumber berbeda, lalu dibuat konsisten. Proses integrasi dapat mencakup:

- Konversi format data.
- Penyamaan kode dan standar.
- Pembersihan data.
- Penggabungan data duplikat.
- Perubahan struktur data.
- Penyamaan satuan, nama atribut, tipe data, dan definisi bisnis.

Contoh: di satu sistem gender ditulis `L/P`, di sistem lain `Male/Female`; warehouse harus menyamakan representasinya.

### 3. Time-variant

Data warehouse menyimpan data dengan dimensi waktu. Setiap data merepresentasikan kondisi pada periode tertentu.

Bentuk time marking:
- Timestamp.
- Tanggal transaksi.
- Effective date.
- Start date dan end date.
- Snapshot period.

Makna penting: pengguna bisa menganalisis perubahan dari waktu ke waktu, misalnya trend penjualan per bulan atau perubahan status mahasiswa per tahun.

### 4. Non-volatile

Data di warehouse tidak sering di-update seperti sistem OLTP. Setelah data masuk, data umumnya:

- Dibaca untuk analisis.
- Disimpan sebagai histori.
- Ditambahkan secara periodik.
- Tidak dihapus atau overwrite sembarangan.

Makna penting: data warehouse menjaga jejak historis untuk pelaporan dan analisis.

---

## 4. OLTP vs OLAP

### OLTP: Online Transaction Processing

OLTP adalah sistem untuk transaksi operasional harian.

Ciri-ciri OLTP:
- Banyak transaksi kecil.
- Banyak operasi insert, update, delete.
- Data biasanya current snapshot.
- Ukuran data relatif lebih kecil dibanding warehouse.
- Digunakan oleh banyak user operasional.
- Fokus pada kecepatan transaksi dan konsistensi data.
- Contoh: sistem kasir, sistem akademik aktif, sistem pemesanan.

### OLAP: Online Analytical Processing

OLAP adalah sistem untuk analisis data.

Ciri-ciri OLAP:
- Mayoritas operasi read.
- Query panjang dan kompleks.
- Data berukuran besar, bisa GB sampai TB.
- Menyimpan histori.
- Banyak scan dan aggregation.
- Data dapat berupa summarized dan reconciled data.
- Digunakan oleh analis, manajer, eksekutif, dan decision maker.

### Perbedaan penting

| Aspek | OLTP | OLAP / Data Warehouse |
|---|---|---|
| Tujuan | Transaksi harian | Analisis dan keputusan |
| Operasi dominan | Insert, update, delete | Select, scan, aggregate |
| Data | Current | Historical |
| Query | Pendek dan sederhana | Panjang dan kompleks |
| User | Operasional | Analis dan manajemen |
| Desain | Normalisasi kuat | Denormalisasi/dimensional |
| Ukuran | MB-GB | GB-TB |
| Contoh | Input order | Analisis penjualan tahunan |

Keuntungan utama warehouse: beban analitik dipisahkan dari beban transaksi, sehingga performa analisis lebih baik dan sistem transaksi tidak terganggu.

### Operational information vs analytical information

Operational information adalah informasi yang dipakai untuk menjalankan aktivitas harian organisasi.

Contoh:
- Transaksi penjualan.
- Pembayaran.
- Pendaftaran anggota.
- Input data pelanggan.
- Update inventory.

Analytical information adalah informasi yang dipakai untuk analisis, evaluasi, dan pengambilan keputusan.

Contoh:
- Tren penjualan tahunan.
- Analisis pelanggan.
- Analisis profit.
- Prediksi bisnis.
- Perbandingan performa antar periode.

Perbedaan penting:

| Aspek | Operational Information | Analytical Information |
|---|---|---|
| Horizon waktu | Hari/bulan, data saat ini | Tahunan, historis |
| Detail | Sangat detail untuk transaksi | Detail dan/atau ringkasan |
| Akses | Frekuensi tinggi | Frekuensi rendah-sedang |
| Update | Sering di-update | Umumnya read-only |
| Orientasi | Application-oriented | Subject-oriented |
| Pengguna | Banyak pegawai operasional | Analis, manajer, eksekutif |

### Application-oriented vs subject-oriented

Database operasional biasanya application-oriented, artinya dirancang untuk mendukung aplikasi atau proses tertentu.

Contoh:
- Sistem membership menyimpan member, membership level, daily visit, dan payment.
- Tujuannya adalah menjalankan proses pendaftaran, pembayaran, dan kunjungan harian.

Data warehouse bersifat subject-oriented, artinya data disusun berdasarkan subjek analisis.

Contoh:
- Subject: revenue.
- Data yang disimpan dapat mencakup tanggal, jenis pelanggan, gender pelanggan, penggunaan fasilitas, dan nilai transaksi.
- Tujuannya bukan menjalankan transaksi, tetapi menganalisis pendapatan.

---

## 5. Data Mart

Data mart adalah subset dari data warehouse yang berfokus pada subject area, departemen, atau kebutuhan bisnis tertentu.

Contoh:
- Data mart penjualan.
- Data mart keuangan.
- Data mart akademik.
- Data mart inventory.

Karakteristik data mart:
- Lebih kecil dan lebih fokus dibanding enterprise data warehouse.
- Umumnya dibangun untuk kebutuhan user tertentu.
- Biasanya menggunakan dimensional modeling.
- Memiliki fact dan dimension table.
- Dapat bersifat dependent, independent, conformed, atau federated.

### Independent data mart

Independent data mart adalah data mart yang berdiri sendiri. Data mart ini memiliki source system dan proses ETL sendiri, tanpa bergantung pada enterprise data warehouse pusat.

Kelebihan:
- Cepat dibuat untuk kebutuhan departemen tertentu.
- Tidak perlu menunggu enterprise DW selesai.

Kekurangan:
- Berisiko menjadi silo baru.
- Definisi data bisa tidak konsisten antar data mart.
- Integrasi lintas departemen lebih sulit.

### Dependent data mart

Dependent data mart adalah data mart yang mengambil data dari data warehouse pusat.

Alur:

```text
Source Systems -> Data Warehouse -> Data Mart
```

Kelebihan:
- Lebih konsisten karena sumbernya DW pusat.
- Cocok untuk integrasi enterprise.
- Lebih mudah menjaga definisi data lintas departemen.

Kekurangan:
- Bergantung pada kesiapan dan kualitas data warehouse pusat.

Perbandingan ringkas:

| Aspek | Data Warehouse | Data Mart |
|---|---|---|
| Scope | Enterprise-wide | Departemen/subjek tertentu |
| Subject | Banyak subject | Satu atau sedikit subject |
| Sumber | Banyak sumber internal/eksternal | Lebih sedikit sumber |
| Struktur | Lebih kompleks | Lebih sederhana |
| Umur | Jangka panjang | Bisa lebih project-oriented |
| Tujuan | Integrasi organisasi | Kebutuhan analisis spesifik |

---

## 6. Arsitektur Data Warehouse

### Komponen umum

Arsitektur data warehouse umumnya mencakup:

- Source systems: sistem operasional, file, spreadsheet, sumber eksternal.
- Extractor/monitor: mengambil data dan mendeteksi perubahan.
- Staging area: tempat sementara untuk pembersihan dan transformasi.
- Integrator/ETL: membersihkan, menggabungkan, dan mengubah data.
- Warehouse storage: penyimpanan data terintegrasi.
- Metadata: informasi tentang struktur, sumber, transformasi, dan arti data.
- Query and analysis tools: reporting, dashboard, OLAP, data mining.
- Data marts/cubes: struktur analitik untuk kebutuhan khusus.

### Single-layer architecture

Data tidak banyak diduplikasi. Konsepnya mendekati virtual warehouse. Cocok ketika data tidak perlu dipindahkan atau saat kebutuhan integrasi sederhana.

### Two-layer architecture

Memisahkan operational systems dan informational systems. Data operasional diproses menjadi derived data untuk analisis. Pendekatan ini umum di industri.

### Three-layer architecture

Memiliki tiga tingkatan:

- Real-time/operational data.
- Reconciled data, yaitu data yang sudah dibersihkan dan diselaraskan.
- Derived data/view level, yaitu data untuk kebutuhan informasi tertentu.

Three-layer lebih eksplisit karena transformasi dari data operasional ke data analitik biasanya membutuhkan tahap rekonsiliasi.

---

## 7. Planning dan Requirement Data Warehouse

### Mengapa planning penting?

Proyek data warehouse berisiko tinggi karena melibatkan banyak sumber data, banyak stakeholder, kebutuhan bisnis yang tidak selalu jelas, dan biaya yang cukup besar. Planning membantu memastikan proyek realistis dan memiliki arah bisnis yang kuat.

Hal yang perlu direncanakan:

- Manfaat nyata yang diharapkan perusahaan.
- Ekspektasi user dan manajemen.
- Risiko proyek dan cara mitigasinya.
- Biaya proyek dan kemungkinan kerugian.
- Pendekatan top-down atau bottom-up.
- Keputusan build or buy.
- Pilihan single vendor atau best-of-breed.

### Build or buy

Build berarti mengembangkan solusi sendiri di dalam organisasi. Buy berarti menggunakan produk/vendor. Dalam praktik, sering terjadi kombinasi keduanya.

Pertimbangan:
- Kebutuhan spesifik organisasi.
- Biaya lisensi dan pengembangan.
- Skill tim internal.
- Integrasi dengan sistem lama.
- Waktu implementasi.
- Dukungan vendor.

### Single vendor vs best-of-breed

Single vendor:
- Semua komponen berasal dari satu vendor.
- Integrasi biasanya lebih mudah.
- Risiko vendor lock-in lebih tinggi.

Best-of-breed:
- Memilih tool terbaik untuk setiap fungsi.
- Lebih fleksibel.
- Integrasi antar tool bisa lebih kompleks.

### Tim proyek data warehouse

Tim data warehouse biasanya melibatkan:

- Sponsor bisnis.
- Project manager.
- Business analyst.
- Data architect.
- ETL developer.
- Database administrator.
- BI/report developer.
- Subject matter expert.
- End user perwakilan departemen.

Kunci suksesnya adalah keterlibatan user bisnis, karena DW dibangun untuk menjawab kebutuhan analisis bisnis.

### Skenario kegagalan umum

Proyek DW dapat gagal jika:

- Scope terlalu besar sejak awal.
- User tidak dilibatkan.
- Requirement tidak jelas.
- Data source buruk dan tidak dipahami.
- Tidak ada sponsor manajemen.
- Ekspektasi terlalu tinggi dan tidak realistis.
- Metadata dan kualitas data diabaikan.
- Tim hanya fokus teknologi, bukan kebutuhan bisnis.

---

## 8. Requirement sebagai Driving Force

Requirement adalah penggerak utama desain data warehouse. Dari requirement, kita menentukan:

- Data apa yang dibutuhkan.
- Subject area apa yang menjadi fokus.
- Measures apa yang perlu dianalisis.
- Dimensions apa yang digunakan.
- Level detail atau grain data.
- Arsitektur data warehouse.
- Kebutuhan storage.
- Strategi delivery informasi.

### Analisis bisnis secara dimensional

Manajer biasanya berpikir secara dimensional. Mereka ingin melihat ukuran bisnis berdasarkan sudut pandang tertentu.

Contoh pertanyaan dimensional:
- Berapa total penjualan per produk, per bulan, per kota?
- Berapa jumlah mahasiswa aktif per fakultas, per tahun, per jenis seleksi?
- Berapa pendapatan SPP per semester, per fakultas, per angkatan?

Dari pertanyaan seperti ini, kita dapat menemukan:
- Measures: angka yang dihitung.
- Dimensions: sudut pandang analisis.
- Hierarchy: level roll-up dan drill-down.

### Metode pengumpulan requirement

#### Individual interview

Dilakukan dengan mewawancarai user satu per satu.

Kelebihan:
- Mendalam.
- Cocok untuk menggali kebutuhan khusus.
- User lebih bebas menyampaikan masalah.

Kekurangan:
- Memakan waktu.
- Bisa menghasilkan requirement yang berbeda-beda dan perlu disatukan.

#### Group session / JAD

Joint Application Development mengumpulkan user terkait dalam diskusi terstruktur.

Kelebihan:
- Cepat menyelaraskan pemahaman.
- Konflik definisi bisnis bisa dibahas langsung.
- Cocok untuk menyepakati scope dan prioritas.

Kekurangan:
- Membutuhkan fasilitator yang kuat.
- Dominasi peserta tertentu dapat mempengaruhi hasil.

### Dokumen requirement data warehouse

Dokumen requirement sebaiknya berisi:

- Introduction: tujuan, scope, justifikasi proyek, executive summary.
- General requirements: sistem sumber yang dikaji, hasil interview, kebutuhan informasi umum.
- Specific requirements: data sumber, transformasi, storage, delivery.
- Information packages: diagram dan detail information package.
- Other requirements: frekuensi extract, metode loading, lokasi delivery.
- User expectations: masalah, peluang, dan cara user memakai DW.
- User participation and sign-off: aktivitas user selama lifecycle.
- General implementation plan: rencana implementasi level tinggi.

---

## 9. Information Package

### Pengertian

Information package adalah cara mengumpulkan requirement data warehouse berdasarkan subject tertentu. Information package membantu merumuskan kebutuhan analisis ketika user belum bisa menjelaskan seluruh kebutuhan secara lengkap.

Information package berisi:

- Subject analisis.
- Measures atau metrics.
- Dimensions.
- Hierarchy dalam dimension.
- Level granularity.
- Cara roll-up dan drill-down.

### Measures

Measures adalah data numerik yang dapat dihitung atau dianalisis.

Contoh:
- Quantity.
- Harga.
- Total penjualan.
- Nilai rata-rata.
- Jumlah pelanggan.
- Jumlah mahasiswa.
- Total pembayaran.

Dalam desain DW, measures biasanya berada di fact table.

### Dimensions

Dimension adalah kategori untuk menganalisis measures.

Contoh:
- Time.
- Product.
- Customer.
- Location.
- Hotel.
- Room type.
- Fakultas.
- Jenis seleksi.

Dalam desain DW, dimensions biasanya menjadi dimension table.

### Hierarchy

Hierarchy adalah level dalam dimension yang memungkinkan roll-up dan drill-down.

Contoh hierarchy time:
- Day -> Month -> Quarter -> Year.

Contoh hierarchy customer/location:
- Customer -> City -> State -> Country -> Region.

### Roll-up dan drill-down

Roll-up berarti naik ke level ringkasan yang lebih tinggi.

Contoh:
- Dari penjualan per hari menjadi penjualan per bulan.
- Dari kota menjadi provinsi.

Drill-down berarti turun ke level detail yang lebih rendah.

Contoh:
- Dari penjualan per tahun menjadi per kuartal, lalu per bulan.
- Dari total fakultas menjadi per program studi.

### Granularity

Granularity adalah tingkat detail data dalam data warehouse.

Low granularity:
- Data sangat detail.
- Contoh: satu baris per transaksi.
- Lebih fleksibel untuk analisis.
- Ukuran data lebih besar.

High granularity:
- Data sudah diringkas.
- Contoh: total transaksi per bulan.
- Query lebih cepat.
- Detail hilang.

Keputusan granularity sangat penting karena mempengaruhi ukuran storage, fleksibilitas analisis, performa query, dan desain fact table.

### Grain terlalu kasar vs terlalu detail

Grain yang terlalu kasar membuat analisis menjadi terbatas.

Contoh:

Jika data yang disimpan hanya penjualan per bulan, maka warehouse tidak bisa menjawab pertanyaan seperti:

- Berapa penjualan hari Senin?
- Berapa penjualan minggu pertama?
- Jam berapa transaksi paling ramai?

Karena detail harian atau transaksi sudah hilang.

Grain yang terlalu detail membuat analisis sangat fleksibel, tetapi ukuran fact table bisa sangat besar.

Contoh:

- Satu row per klik user.
- Satu row per event aplikasi.
- Satu row per item transaksi.

Aturan praktis:

- Pilih grain sesuai kebutuhan analisis bisnis.
- Jika ragu, simpan grain yang cukup detail selama storage dan performa masih realistis.
- Grain harus didefinisikan sebelum memilih dimension dan measure.

### Contoh information package hotel occupancy

Subject: hotel occupancy.

Tujuan analisis:
- Menganalisis okupansi kamar pada cabang hotel.
- Melihat okupansi berdasarkan hotel, room type, dan time.

Measures:
- Jumlah kamar terisi.
- Jumlah kamar tersedia.
- Occupancy rate.
- Revenue kamar.

Dimensions:
- Hotel.
- Room type.
- Time.

Hierarchy:
- Time: day -> month -> quarter -> year.
- Hotel: hotel -> city -> region.
- Room type: room type -> room class.

### Contoh information package SIAM

Subject: akademik mahasiswa.

Contoh measures:
- Jumlah mahasiswa berdasarkan status kuliah.
- Jumlah uang SPP yang diterima.
- Jumlah mahasiswa per jenis seleksi.

Contoh dimensions:
- Waktu: semester, tahun.
- Fakultas.
- Program studi.
- Status kuliah.
- Jenis seleksi.
- Angkatan.

Contoh query analitik:
- Jumlah mahasiswa aktif/lulus/dropout/undur diri per fakultas per tahun per jenis seleksi.
- Jumlah penerimaan SPP per semester per fakultas per jenis seleksi.

---

## 10. Inmon vs Kimball

### Inmon approach

Inmon dikenal dengan pendekatan top-down dan Corporate Information Factory (CIF).

Ciri utama:
- Fokus enterprise-wide data warehouse.
- Data warehouse dibangun sebagai repository terintegrasi untuk organisasi.
- Menggunakan enterprise data model.
- Data mart dibuat setelah enterprise warehouse tersedia.
- Lebih menekankan integrasi, konsistensi, dan subject orientation.
- Modeling cenderung menggunakan ERD dan struktur yang lebih normalized.

Struktur dalam CIF:
- Operational systems.
- Atomic data warehouse.
- Departmental data.
- Individual/ad hoc access.

Kelebihan:
- Integrasi enterprise lebih kuat.
- Cocok untuk kebutuhan strategis.
- Cocok jika banyak data non-metric dan kebutuhan analisis beragam.
- Lebih baik untuk organisasi yang membutuhkan pandangan menyeluruh.

Kekurangan:
- Kompleks.
- Start-up cost lebih tinggi.
- Waktu delivery lebih lama.
- Membutuhkan tim lebih besar dan spesialis.

### Kimball approach

Kimball dikenal dengan pendekatan bottom-up dan dimensional modeling.

Ciri utama:
- Mulai dari data mart berdasarkan business process.
- Menggunakan star schema/dimensional model.
- Fokus pada kemudahan akses oleh end user.
- Enterprise data warehouse terbentuk dari gabungan data mart.
- Integrasi dicapai melalui conformed dimensions.

Empat langkah desain Kimball:

1. Select business process.
2. Declare the grain.
3. Choose dimensions.
4. Identify facts.

Kelebihan:
- Lebih cepat memberikan hasil ke user.
- Lebih mudah dipahami end user.
- Cocok untuk kebutuhan taktis.
- Cocok untuk business metrics, scorecards, dan performance measures.
- Start-up cost lebih rendah.

Kekurangan:
- Risiko integrasi enterprise jika conformed dimensions tidak dijaga.
- Setiap proyek berikutnya bisa membutuhkan biaya yang mirip.
- Jika scope berubah besar, desain perlu disiplin tinggi.

### Conformed dimensions

Conformed dimensions adalah dimensi yang memiliki definisi konsisten dan dapat digunakan lintas data mart.

Contoh: dimension `Time`, `Product`, atau `Customer` dipakai oleh data mart sales, inventory, dan finance dengan definisi yang sama.

Kunci sukses Kimball adalah conformed dimensions. Tanpa conformed dimensions, data mart akan menjadi silo baru.

### Perbandingan Inmon dan Kimball

| Aspek | Inmon | Kimball |
|---|---|---|
| Pendekatan | Top-down | Bottom-up |
| Fokus | Enterprise data warehouse | Data mart/business process |
| Modeling | ERD, enterprise data model | Dimensional model |
| Struktur | Lebih kompleks | Lebih sederhana |
| Integrasi | Enterprise data model | Conformed dimensions |
| Audience | IT/enterprise architecture | End user/business |
| Delivery | Lebih lama | Lebih cepat |
| Biaya awal | Lebih tinggi | Lebih rendah |
| Cocok untuk | Strategis, enterprise-wide | Taktis, kebutuhan cepat |

### Kapan memilih Inmon?

Pilih Inmon jika:
- Kebutuhan integrasi enterprise sangat tinggi.
- Organisasi membutuhkan pandangan strategis menyeluruh.
- Data berasal dari banyak sistem dan harus disatukan secara kuat.
- Ada waktu lebih panjang untuk start-up.
- Organisasi memiliki tim spesialis dan governance kuat.
- Data source sering berubah dan butuh persistency kuat.

### Kapan memilih Kimball?

Pilih Kimball jika:
- Aplikasi DW pertama harus cepat tersedia.
- Kebutuhan user bersifat urgent.
- Scope terbatas pada area bisnis tertentu.
- Fokus pada metrics, scorecards, dan performance analysis.
- Source systems relatif stabil.
- Tim kecil dan generalis.

---

## 11. Logical Design Data Warehouse

### Logical design vs physical design

Logical design:
- Konseptual dan abstrak.
- Fokus pada hubungan logis antar objek.
- Berorientasi pada requirement end user.
- Menentukan fact, dimension, attribute, relationship, grain.

Physical design:
- Fokus pada cara menyimpan dan mengambil data secara efektif.
- Membahas implementasi database.
- Termasuk table space, buffer pool, indexing, backup, recovery, dan storage.

### Entity Relationship Modeling

Dalam logical design, kita mengenali:

- Entity: objek data seperti mahasiswa, produk, customer, transaksi.
- Attribute: properti entity seperti nama, tanggal, harga, status.
- Relationship: hubungan antar entity.

Namun dalam data warehouse, logical design sering diarahkan ke dimensional model, bukan model transaksi murni.

### Fact dan dimension

Fact:
- Merepresentasikan event bisnis.
- Berisi measures/metrics.
- Biasanya numerik.
- Terhubung ke dimension melalui foreign key.

Contoh fact:
- Penjualan.
- Pembayaran.
- Kehadiran.
- Pengiriman.

Dimension:
- Menjelaskan konteks fact.
- Berisi atribut deskriptif.
- Digunakan untuk filtering, grouping, roll-up, drill-down.

Contoh dimension:
- Product.
- Customer.
- Time.
- Location.
- Fakultas.

---

## 12. Skema Data Warehouse

### Star schema

Star schema memiliki satu fact table di tengah dan beberapa dimension table di sekelilingnya.

Ciri:
- Fact table menyimpan measures dan foreign key ke dimensions.
- Dimension table biasanya denormalized.
- Struktur sederhana dan mudah dipahami.
- Query lebih cepat karena join lebih sedikit.
- Cocok untuk OLAP dan reporting.

Contoh:

FactSales:
- product_key
- customer_key
- date_key
- quantity_ordered
- price_each
- price_total

DimProduct:
- product_key
- product_name
- product_description
- buy_price

DimCustomer:
- customer_key
- customer_name
- city
- state
- country

DimDate:
- date_key
- date
- day
- month
- quarter
- year

### Contoh transformasi ERD operasional ke star schema

Pada sistem OLTP, data biasanya dinormalisasi menjadi banyak tabel. Contoh kasus retail seperti ZAGI dapat memiliki entitas:

- Region.
- Store.
- Product.
- Vendor.
- Category.
- Customer.
- SalesTransaction.
- SoldVia.

Model ini bagus untuk transaksi, tetapi query analisis menjadi rumit karena perlu banyak join. Misalnya untuk menganalisis penjualan produk kategori tertentu, query harus melewati store, region, transaction, product, vendor, dan category.

Dalam dimensional model, entitas tersebut dapat disederhanakan menjadi:

- `FactSales`.
- `DimCalendar`.
- `DimStore`.
- `DimProduct`.
- `DimCustomer`.

Contoh denormalisasi:

- `VendorName` dan `CategoryName` yang di OLTP berada di tabel terpisah dapat digabung ke `DimProduct`.
- `StoreRegion` dapat dimasukkan ke `DimStore`.
- Atribut tanggal seperti day, month, quarter, year dimasukkan ke `DimCalendar`.

Tujuannya adalah mengurangi join, mempercepat query analitis, dan membuat struktur lebih mudah dipahami pengguna bisnis.

### Multiple source integration dalam dimensional model

Data warehouse dapat menggabungkan data dari banyak sumber, bukan hanya dari sistem transaksi utama.

Contoh:

Source utama penjualan menyediakan:

- CustomerID.
- CustomerName.
- CustomerZip.
- StoreID.
- StoreZip.
- ProductID.
- Transaction data.

Source lain seperti customer demographic data dapat menambahkan:

- Gender.
- MaritalStatus.
- EducationLevel.
- CreditScore.

Source facilities database dapat menambahkan:

- StoreSize.
- StoreSystem, misalnya cashier, self-service, mixed.
- StoreLayout, misalnya modern atau traditional.

Akibatnya dimension menjadi lebih kaya.

Contoh `DimCustomer`:

```text
CustomerKey
CustomerID
CustomerName
CustomerZip
Gender
MaritalStatus
EducationLevel
CreditScore
```

Contoh `DimStore`:

```text
StoreKey
StoreID
StoreZip
StoreRegion
StoreSize
StoreSystem
StoreLayout
```

Makna penting: kekuatan data warehouse bukan hanya menyimpan data transaksi, tetapi mengintegrasikan berbagai sumber menjadi satu model analitis yang konsisten.

### Snowflake schema

Snowflake schema adalah variasi star schema di mana dimension table dinormalisasi menjadi beberapa tabel.

Contoh:
- DimCustomer dapat dipisah menjadi Customer, City, State, Country.
- DimProduct dapat dipisah menjadi Product, ProductLine, Category.

Kelebihan:
- Mengurangi redundansi.
- Storage bisa lebih hemat.
- Struktur normalized lebih mudah di-update dan maintain.

Kekurangan:
- Lebih kompleks untuk end user.
- Query lebih lambat karena lebih banyak join.
- Browsing data lebih sulit.
- Kurang intuitif dibanding star schema.

### Fact constellation schema

Fact constellation memiliki banyak fact table yang berbagi dimension table.

Contoh:
- FactSales dan FactInventory sama-sama memakai DimProduct dan DimDate.
- FactPembayaran dan FactAkademik sama-sama memakai DimMahasiswa dan DimWaktu.

Ciri:
- Cocok untuk data warehouse yang mencakup banyak proses bisnis.
- Lebih kompleks daripada star schema tunggal.
- Memungkinkan integrasi lintas fact.

### Multiple fact tables, shared dimensions, dan cross-fact analysis

Dalam dunia nyata, satu data warehouse tidak hanya menganalisis satu subject seperti sales. Organisasi dapat memiliki banyak fact table:

- `FactSales`.
- `FactInventory`.
- `FactDefect`.
- `FactReturns`.
- `FactShipping`.

Jika beberapa fact table memakai dimension yang sama, dimension tersebut disebut shared dimension atau reusable dimension.

Contoh:

```text
FactSales  -> DimProduct, DimStore, DimCalendar
FactDefect -> DimProduct, DimStore, DimCalendar
```

Keuntungannya:

- Tidak perlu membuat dimension duplikat seperti `DimProductSales` dan `DimProductDefect`.
- Definisi produk, toko, dan tanggal tetap konsisten.
- Maintenance lebih mudah.
- Analisis lintas fact menjadi mungkin.

Cross-fact analysis adalah analisis yang menggabungkan lebih dari satu fact table melalui shared dimension.

Contoh pertanyaan:

> Apakah produk dengan penjualan tinggi juga memiliki tingkat defect tinggi?

Untuk menjawabnya:

- Penjualan diambil dari `FactSales`.
- Jumlah defect diambil dari `FactDefect`.
- Keduanya digabung melalui `DimProduct`.

Inilah salah satu alasan utama fact constellation schema penting.

### Factless fact table

Factless fact table adalah fact table tanpa measures numerik eksplisit. Setiap baris merepresentasikan kejadian atau hubungan.

Contoh: tabel kehadiran mahasiswa.

Kolom:
- student_key
- class_key
- date_key

Tidak perlu kolom `hadir = 1`, karena keberadaan row sudah berarti mahasiswa hadir.

Kegunaan:
- Menghitung jumlah kejadian.
- Mencatat event atau coverage.
- Menjawab pertanyaan seperti "berapa mahasiswa hadir di kelas tertentu pada hari tertentu?"

### Additional fact attributes

Secara umum fact table berisi foreign key ke dimension dan measure. Namun dalam praktik, fact table kadang menyimpan atribut tambahan yang bukan measure dan bukan dimension utama.

Contoh:

- `TransactionID`.
- `InvoiceID`.
- `OrderID`.
- `ReceiptID`.
- `TransactionTime`.

#### Transaction identifier

Transaction identifier berguna untuk audit trail dan traceability.

Contoh:

Satu transaksi `T555` berisi beberapa produk. Jika auditor ingin menelusuri transaksi asli, `TransactionID` di fact table membantu menghubungkan data warehouse kembali ke sistem sumber.

Manfaat:

- Audit.
- Validasi data.
- Investigasi error.
- Menelusuri anomali transaksi.

#### Transaction time

Selain tanggal, kadang organisasi perlu menyimpan jam transaksi.

Contoh kebutuhan:

- Mengetahui jam sibuk.
- Mengetahui jam sepi.
- Melihat pola transaksi harian.

Ada dua pilihan desain:

1. Simpan langsung di fact table sebagai `TimeOfDay`.
2. Buat `DimTime` jika analisis waktu sangat penting.

Contoh `DimTime`:

- `TimeKey`.
- `Hour`.
- `Minute`.
- `Second`.
- `Shift`.
- `PartOfDay`.

Aturan praktis:

- Jika hanya butuh jam transaksi sebagai informasi tambahan, simpan di fact table.
- Jika banyak analisis berdasarkan jam, shift, atau bagian hari, buat time dimension.

### Jenis measure: additive, semi-additive, non-additive

Measure dalam fact table tidak semuanya bisa dijumlahkan dengan cara yang sama.

#### Additive measure

Additive measure dapat dijumlahkan pada semua dimension.

Contoh:

- Revenue.
- SalesAmount.
- UnitsSold.
- Profit.

Jika revenue per hari dijumlahkan menjadi revenue per bulan, hasilnya tetap bermakna.

#### Semi-additive measure

Semi-additive measure dapat dijumlahkan pada beberapa dimension, tetapi tidak semua.

Contoh:

- Inventory level.
- Account balance.
- Stock quantity.

Misalnya stok tanggal 1 = 100 unit dan stok tanggal 2 = 120 unit. Tidak benar jika disimpulkan total stok = 220 unit, karena stok adalah kondisi pada titik waktu tertentu. Namun stok mungkin masih bisa dijumlahkan berdasarkan product atau store pada tanggal yang sama.

#### Non-additive measure

Non-additive measure tidak boleh dijumlahkan langsung.

Contoh:

- Percentage.
- Ratio.
- Margin.
- Rate.

Jika margin 10%, 20%, dan 30%, tidak benar jika dijumlahkan menjadi 60%. Biasanya harus dihitung ulang dari komponen dasarnya.

Ringkasan:

| Jenis Measure | Bisa Dijumlahkan? | Contoh |
|---|---|---|
| Additive | Semua dimension | Revenue, units sold |
| Semi-additive | Sebagian dimension | Inventory level, balance |
| Non-additive | Tidak langsung dijumlahkan | Percentage, ratio, margin |

---

## 13. Key Constraint dan Surrogate Key

### Primary key dan foreign key

Dimension table memiliki primary key. Fact table menyimpan foreign key yang mengarah ke dimension.

Contoh:
- `DimProduct(product_key)` menjadi FK di `FactSales`.
- `DimCustomer(customer_key)` menjadi FK di `FactSales`.
- `DimDate(date_key)` menjadi FK di `FactSales`.

Fact table dapat memiliki composite key dari beberapa foreign key, atau menggunakan surrogate fact key jika dibutuhkan.

### Surrogate key

Surrogate key adalah key buatan, biasanya integer berurutan, yang digunakan sebagai primary key pengganti natural key dari sistem operasional.

Contoh:
- Natural key: `productCode = S10_1678`.
- Surrogate key: `product_key = 101`.

Manfaat surrogate key:
- Mengisolasi DW dari perubahan key di sistem OLTP.
- Lebih ringkas dan efisien untuk join.
- Mendukung Slowly Changing Dimension, terutama Type 2.
- Menghindari masalah natural key yang berubah, duplikat, atau berbeda antar sumber.

---

## 14. Slowly Changing Dimension (SCD)

### Pengertian

Slowly Changing Dimension adalah masalah ketika atribut pada dimension berubah seiring waktu.

Contoh:
- Customer pindah kota.
- Mahasiswa berubah status.
- Produk berubah kategori.
- Cabang berubah wilayah.

Pertanyaan desainnya: apakah warehouse harus menyimpan histori perubahan tersebut?

### SCD Type 1

Type 1 berarti data lama di-overwrite oleh data baru.

Contoh:

Sebelum:

| Customer Key | Name | State |
|---|---|---|
| 1001 | Christina | Illinois |

Sesudah pindah:

| Customer Key | Name | State |
|---|---|---|
| 1001 | Christina | California |

Kelebihan:
- Paling sederhana.
- Tidak membutuhkan storage tambahan.
- ETL lebih mudah.

Kekurangan:
- Histori hilang.
- Tidak bisa tahu bahwa Christina dulu tinggal di Illinois.

Kapan digunakan:
- Jika histori tidak penting.
- Untuk koreksi data yang memang salah.
- Untuk atribut yang tidak perlu dianalisis historinya.

### SCD Type 2

Type 2 berarti membuat row baru untuk perubahan data. Setiap versi memiliki primary key sendiri.

Contoh:

| Customer Key | Name | State |
|---|---|---|
| 1001 | Christina | Illinois |
| 1005 | Christina | California |

Sering ditambahkan atribut:
- effective_start_date
- effective_end_date
- current_flag

Kelebihan:
- Histori lengkap tersimpan.
- Analisis historis akurat.

Kekurangan:
- Ukuran dimension bertambah cepat.
- ETL lebih kompleks.
- Query perlu memperhatikan versi record.

Kapan digunakan:
- Jika perubahan historis penting untuk analisis.
- Contoh: histori wilayah customer, histori status mahasiswa, histori jabatan pegawai.

### SCD Type 3

Type 3 menyimpan sebagian histori dalam kolom tambahan.

Contoh:

| Customer Key | Name | Original State | Current State | Effective Date |
|---|---|---|---|---|
| 1001 | Christina | Illinois | California | 15-JAN-2003 |

Kelebihan:
- Tidak menambah jumlah row.
- Menyimpan sebagian histori.

Kekurangan:
- Hanya menyimpan histori terbatas.
- Jika perubahan terjadi berkali-kali, data lama akan hilang.
- Jarang digunakan dalam praktik.

Kapan digunakan:
- Jika hanya perlu membandingkan nilai lama dan nilai sekarang.
- Jika jumlah perubahan terbatas dan sudah diketahui.

### Ringkasan SCD

| Type | Cara kerja | Histori | Kelebihan | Kekurangan |
|---|---|---|---|---|
| Type 1 | Overwrite | Tidak ada | Mudah | Histori hilang |
| Type 2 | Tambah row baru | Lengkap | Analisis historis akurat | Tabel membesar, ETL kompleks |
| Type 3 | Tambah kolom lama/sekarang | Terbatas | Tidak menambah row | Tidak cocok untuk banyak perubahan |

---

## 15. Transformasi dan Load Data (ETL)

### Pengertian ETL

ETL adalah proses:

- Extract: mengambil data dari source system.
- Transform: membersihkan, mengubah, menggabungkan, dan menghitung data.
- Load: memasukkan data ke data warehouse.

Dalam materi, contoh ETL memakai database OLTP `classicmodels` dengan DBMS MySQL.

### Tujuan DW pada contoh classicmodels

Warehouse dibuat untuk menghitung:

- Jumlah pendapatan dari pembelian tiap pelanggan, tiap produk, dan tanggal pembelian.
- Kuantitas pembelian tiap produk, per pelanggan, per tanggal pembelian.
- Jumlah pelanggan per bulan, quarter, dan tahun.

Sumber measures:
- `quantityOrdered`
- `priceEach`
- `quantityOrdered * priceEach` sebagai `price_total`

### Skema DW contoh penjualan

Dimension:
- `dim_products`
- `dim_customers`
- `dim_date`

Fact:
- `fact_sales`

### Dimensi produk

Contoh atribut:
- productCode
- productName
- productDescription
- buyPrice

Catatan:
- Dalam contoh slide, `productCode` digunakan sebagai primary key.
- Dalam desain DW yang lebih umum, bisa juga dibuat surrogate key seperti `product_key`.

### Dimensi pelanggan

Contoh atribut:
- customerNumber
- customerName
- city
- state
- postalCode
- country

### Dimensi waktu

Contoh atribut:
- sk, biasanya format `yyyyMMdd`.
- date.
- year.
- quarter.
- month.
- month_name.
- day.

Dimensi waktu penting karena hampir semua analisis DW membutuhkan time-based analysis.

### Fact sales

Contoh atribut:
- productCode
- customerNumber
- sk
- quantity_ordered
- price_each
- price_total

Foreign key:
- productCode -> dim_products
- customerNumber -> dim_customers
- sk -> dim_date

Measures:
- quantity_ordered
- price_each
- price_total

Grain fact table:
- Satu row merepresentasikan penjualan untuk kombinasi produk, customer, dan tanggal.

### Transformasi dalam Talend

Komponen penting:

#### tMap

tMap digunakan untuk:
- Mapping field dari input ke output.
- Transformasi field.
- Concatenation atau penggabungan field.
- Interchange/perubahan field.
- Filtering dengan constraint.
- Reject data yang tidak valid.
- Multiplexing dan demultiplexing data.

Contoh penggunaan:
- Mapping tabel `products` dari database OLTP ke `dim_products`.
- Menghitung `price_total = quantityOrdered * priceEach`.
- Mengubah format tanggal.
- Memilih kolom tertentu untuk dimensi.

#### tRowGenerator

tRowGenerator digunakan untuk menghasilkan data secara otomatis.

Dalam materi, digunakan untuk:
- Generate data dimensi waktu.
- Membuat banyak row tanggal.
- Mengisi field seperti date, year, quarter, month, day.

Contoh task:
- Generate tanggal mulai 22-11-2017 sebanyak 100 rows.
- Tampilkan hasil ke `tLogRow`.
- Load hasil generate ke tabel `dim_date`.

### Hal penting dalam ETL

Saat ETL, perhatikan:

- Data source dan target schema.
- Mapping kolom.
- Tipe data.
- Primary key dan foreign key.
- Cleansing data null atau invalid.
- Transformasi format tanggal.
- Perhitungan measures.
- Urutan load: dimension lebih dulu, fact belakangan.
- Error handling dan rejected rows.

---

## 16. SQL OLAP

### Pengertian SQL OLAP

SQL OLAP adalah penggunaan fungsi SQL untuk membangun dan menyajikan informasi analitik. Jika OLAP secara konsep berarti analisis multidimensi, maka SQL OLAP adalah cara melakukan analisis tersebut langsung melalui query SQL.

Dalam materi DB2, SQL OLAP dipakai untuk:

- Memberi ranking data.
- Memberi nomor baris.
- Membandingkan nilai antar row dalam kelompok data.
- Mengambil nilai pertama dalam window tertentu.
- Membuat subtotal, grand total, dan agregasi multidimensi.
- Menghasilkan beberapa level grouping dalam satu query.

Fungsi yang dibahas:

- `RANK`
- `DENSE_RANK`
- `ROW_NUMBER`
- `LEAD`
- `FIRST_VALUE`
- `ROLLUP`
- `CUBE`
- `GROUPING SETS`
- `GROUPING`

### Window function dan klausa `OVER`

Fungsi seperti `RANK`, `DENSE_RANK`, `ROW_NUMBER`, `LEAD`, dan `FIRST_VALUE` menggunakan klausa `OVER`.

Bentuk umum:

```sql
fungsi_olap() OVER (
    PARTITION BY kolom_kelompok
    ORDER BY kolom_urutan
)
```

Makna:

- `OVER` mendefinisikan window atau ruang kerja fungsi OLAP.
- `PARTITION BY` membagi data menjadi kelompok-kelompok.
- `ORDER BY` menentukan urutan perhitungan dalam window.

Contoh:

```sql
SELECT empno, lastname, workdept, edlevel,
       DENSE_RANK() OVER (
           PARTITION BY workdept
           ORDER BY edlevel DESC
       ) AS rank_edlevel
FROM employee
ORDER BY workdept;
```

Artinya: beri ranking pendidikan tertinggi (`edlevel`) untuk setiap departemen (`workdept`).

### `RANK`

`RANK` memberi ranking berdasarkan urutan tertentu. Jika ada nilai yang sama, ranking juga sama, tetapi ranking berikutnya lompat.

Contoh ranking:

| Nama | Salary | RANK |
|---|---:|---:|
| A | 100 | 1 |
| B | 90 | 2 |
| C | 90 | 2 |
| D | 80 | 4 |

Perhatikan bahwa setelah ranking 2, langsung ranking 4. Ranking 3 dilewati karena ada dua row dengan nilai sama.

Contoh query:

```sql
SELECT empno,
       lastname,
       firstnme,
       salary + bonus AS total_salary,
       RANK() OVER (ORDER BY salary + bonus DESC) AS rank_salary
FROM employee
WHERE salary + bonus > 50000
ORDER BY rank_salary;
```

Makna:

- `salary + bonus` dihitung sebagai total salary.
- `RANK()` memberi peringkat dari total salary terbesar ke terkecil.
- `DESC` berarti descending, dari besar ke kecil atau Z ke A.
- `ASC` berarti ascending, dari kecil ke besar atau A ke Z.

Catatan penting:

- `ORDER BY` di dalam `OVER` menentukan ranking.
- `ORDER BY` paling luar menentukan urutan tampilan hasil akhir.
- Dua hal ini bisa berbeda.

Contoh:

```sql
SELECT empno, lastname, salary + bonus AS total_salary,
       RANK() OVER (ORDER BY salary + bonus DESC) AS salary_rank
FROM employee
WHERE salary + bonus > 30000
ORDER BY lastname;
```

Ranking dihitung berdasarkan total salary, tetapi output ditampilkan berdasarkan lastname.

### `DENSE_RANK`

`DENSE_RANK` mirip dengan `RANK`, tetapi tidak ada ranking yang lompat.

Contoh:

| Nama | Salary | RANK | DENSE_RANK |
|---|---:|---:|---:|
| A | 100 | 1 | 1 |
| B | 90 | 2 | 2 |
| C | 90 | 2 | 2 |
| D | 80 | 4 | 3 |

Gunakan `DENSE_RANK` jika ranking harus padat tanpa gap.

Contoh:

```sql
SELECT empno, lastname, workdept, edlevel,
       DENSE_RANK() OVER (
           PARTITION BY workdept
           ORDER BY edlevel DESC
       ) AS rank_edlevel
FROM employee
ORDER BY workdept, lastname;
```

Makna:

- Data dipartisi berdasarkan departemen.
- Dalam setiap departemen, employee diberi ranking berdasarkan `edlevel` tertinggi.
- Ranking dihitung ulang dari 1 untuk setiap `workdept`.

### `ROW_NUMBER`

`ROW_NUMBER` memberi nomor urut unik pada setiap row berdasarkan urutan tertentu.

Contoh:

```sql
SELECT ROW_NUMBER() OVER (ORDER BY workdept, lastname) AS number,
       lastname,
       workdept,
       salary
FROM employee
ORDER BY workdept, lastname;
```

Bedanya dengan `RANK`:

- `ROW_NUMBER` selalu unik untuk setiap row.
- Jika ada nilai sama, tetap diberi nomor berbeda.
- `RANK` bisa memberikan ranking yang sama untuk nilai yang sama.

Jika `ORDER BY` tidak ditentukan dalam `OVER`, nomor row bisa diberikan dalam urutan arbitrer, sehingga hasilnya tidak aman untuk analisis yang membutuhkan urutan pasti.

### Mengambil Top-N dengan ranking

Untuk mengambil top 5 salary, fungsi ranking biasanya perlu ditaruh dalam subquery atau common table expression, lalu difilter di query luar.

Contoh:

```sql
SELECT empno, lastname, firstnme, total_salary, rank_salary
FROM (
    SELECT empno,
           lastname,
           firstnme,
           salary + bonus AS total_salary,
           RANK() OVER (ORDER BY salary + bonus DESC) AS rank_salary
    FROM employee
) AS ranked_employee
WHERE rank_salary < 6
ORDER BY rank_salary;
```

Mengapa harus subquery?

Karena alias seperti `rank_salary` atau `total_salary` tidak selalu bisa langsung dipakai di `WHERE` pada level query yang sama. `WHERE` diproses sebelum `SELECT`, sehingga alias hasil `SELECT` belum tersedia.

Contoh yang dapat error:

```sql
SELECT empno,
       lastname,
       salary + bonus AS total_salary,
       RANK() OVER (ORDER BY salary + bonus DESC) AS rank_salary
FROM employee
WHERE total_salary > 90000;
```

Masalahnya: `total_salary` adalah alias di `SELECT`, sedangkan `WHERE` dievaluasi lebih dulu. Solusi: ulangi ekspresi `salary + bonus` di `WHERE`, atau gunakan subquery.

### `LEAD`

`LEAD` mengambil nilai dari row berikutnya dalam window.

Bentuk:

```sql
LEAD(kolom, offset) OVER (
    PARTITION BY kolom_kelompok
    ORDER BY kolom_urutan
)
```

Contoh:

```sql
SELECT empno, workdept, job, salary,
       LEAD(salary, 1) OVER (
           PARTITION BY workdept
           ORDER BY salary
       ) AS next_salary
FROM employee
ORDER BY workdept, salary;
```

Makna:

- Untuk setiap departemen, ambil salary dari row berikutnya berdasarkan urutan salary.
- `LEAD(salary, 1)` berarti ambil 1 row setelah row saat ini.
- `LEAD(salary, 2)` berarti ambil 2 row setelah row saat ini.
- `LEAD(salary, 0)` sama dengan nilai salary row saat ini.

Contoh menghitung selisih dengan row berikutnya:

```sql
SELECT empno, workdept, lastname, firstnme, job, salary,
       LEAD(salary, 1) OVER (
           PARTITION BY workdept
           ORDER BY salary
       ) - salary AS delta_salary
FROM employee
ORDER BY workdept, salary;
```

### `FIRST_VALUE`

`FIRST_VALUE` mengambil nilai pertama dalam window berdasarkan urutan tertentu.

Contoh:

```sql
SELECT empno, workdept, job, salary,
       FIRST_VALUE(salary) OVER (
           PARTITION BY workdept
           ORDER BY salary
       ) AS first_salary
FROM employee
ORDER BY workdept, salary;
```

Makna:

- Untuk setiap departemen, ambil salary pertama berdasarkan urutan salary.
- Jika `ORDER BY salary` ascending, nilai pertama adalah salary terendah.
- Jika ingin salary tertinggi, gunakan `ORDER BY salary DESC`.

Contoh membandingkan salary tiap employee dengan salary pertama berdasarkan hire date pada job yang sama:

```sql
SELECT job, hiredate, empno, lastname, firstnme, salary,
       FIRST_VALUE(salary) OVER (
           PARTITION BY job
           ORDER BY hiredate
       ) AS first_salary,
       salary - FIRST_VALUE(salary) OVER (
           PARTITION BY job
           ORDER BY hiredate
       ) AS delta_salary
FROM employee
ORDER BY job, hiredate;
```

### `ROLLUP`

`ROLLUP` adalah ekstensi `GROUP BY` untuk menghasilkan subtotal bertingkat dan grand total.

Cocok untuk hierarchy.

Contoh:

```sql
SELECT country, region, SUM(sales)
FROM trans
GROUP BY ROLLUP(country, region);
```

`ROLLUP(country, region)` menghasilkan agregasi:

- `(country, region)` detail per country dan region.
- `(country)` subtotal per country.
- `()` grand total.

Contoh hasil konseptual:

| Country | Region | SUM(sales) |
|---|---|---:|
| USA | NE | 450000 |
| USA | NW | 940000 |
| USA | SE | 550000 |
| USA | SW | 1310000 |
| USA | NULL | 3250000 |
| Canada | NW | 100000 |
| Canada | NULL | 100000 |
| NULL | NULL | 3350000 |

Urutan kolom dalam `ROLLUP` penting.

Contoh:

```sql
GROUP BY ROLLUP(region, sales_date)
```

berbeda dengan:

```sql
GROUP BY ROLLUP(sales_date, region)
```

Karena subtotal mengikuti urutan hierarchy yang ditulis.

### `CUBE`

`CUBE` menghasilkan agregasi untuk semua kombinasi dimensi.

Contoh:

```sql
SELECT country, region, SUM(sales)
FROM trans
GROUP BY CUBE(country, region);
```

`CUBE(country, region)` menghasilkan:

- `(country, region)`
- `(country)`
- `(region)`
- `()` grand total

Perbedaan penting:

- `ROLLUP` cocok untuk hierarchy bertingkat.
- `CUBE` cocok untuk analisis multidimensi dari banyak perspektif.

Jika ada dua dimensi, `CUBE` menghasilkan semua kombinasi agregasi. Jika dimensinya banyak, hasil bisa tumbuh sangat besar.

### `GROUPING SETS`

`GROUPING SETS` memungkinkan beberapa bentuk grouping ditentukan dalam satu query.

Contoh:

```sql
SELECT country, region, store, SUM(sales)
FROM trans
GROUP BY GROUPING SETS (
    (country, region),
    (country, store)
);
```

Makna:

- Query menghasilkan ringkasan berdasarkan `(country, region)`.
- Query juga menghasilkan ringkasan berdasarkan `(country, store)`.
- Hasilnya digabung dalam satu result set.

`GROUPING SETS` bisa dianggap seperti `UNION` dari beberapa hasil agregasi, tetapi ditulis dalam satu query.

Contoh sederhana:

```sql
SELECT workdept, job, SUM(salary)
FROM employee
GROUP BY GROUPING SETS (workdept, job)
ORDER BY workdept;
```

Makna:

- Hasil agregasi per `workdept`.
- Hasil agregasi per `job`.
- Tidak otomatis menghasilkan kombinasi `(workdept, job)` kecuali ditulis sebagai `(workdept, job)`.

### `GROUPING`

Masalah pada `ROLLUP`, `CUBE`, dan `GROUPING SETS`: kolom subtotal sering muncul sebagai `NULL`. Tetapi `NULL` itu bisa berarti dua hal:

- Nilai asli data memang `NULL`.
- `NULL` dibuat oleh proses aggregate sebagai tanda subtotal/grand total.

Fungsi `GROUPING` membantu membedakannya.

Contoh:

```sql
SELECT country,
       region,
       store,
       GROUPING(store) AS grouping_store,
       SUM(sales)
FROM trans
WHERE transYear = 2006
GROUP BY GROUPING SETS (
    (country, region),
    (country, store)
);
```

Makna:

- `GROUPING(store) = 1` jika `NULL` pada `store` berasal dari proses grouping/super aggregate.
- `GROUPING(store) = 0` jika nilai `store` adalah nilai asli dari data.

### Perbedaan `GROUP BY`, `ROLLUP`, `CUBE`, dan `GROUPING SETS`

Misal query dasar:

```sql
SELECT workdept, job, SUM(salary)
FROM employee
GROUP BY workdept, job;
```

Hasil:
- Hanya total salary per kombinasi `workdept` dan `job`.

Dengan `ROLLUP`:

```sql
GROUP BY ROLLUP(workdept, job)
```

Hasil:
- Total per `workdept, job`.
- Subtotal per `workdept`.
- Grand total.

Dengan `CUBE`:

```sql
GROUP BY CUBE(workdept, job)
```

Hasil:
- Total per `workdept, job`.
- Subtotal per `workdept`.
- Subtotal per `job`.
- Grand total.

Dengan `GROUPING SETS`:

```sql
GROUP BY GROUPING SETS (workdept, job)
```

Hasil:
- Total per `workdept`.
- Total per `job`.
- Tidak menghasilkan detail kombinasi `workdept, job` kecuali ditulis eksplisit.

### Additive vs multiplicative grouping

Materi DB2 membedakan cara kombinasi `ROLLUP`, `CUBE`, dan `GROUPING SETS` menghasilkan grouping.

Additive berarti hasil grouping ditambahkan sebagai daftar set.

Contoh:

```sql
GROUP BY GROUPING SETS (
    CUBE(A, B),
    ROLLUP(C, D),
    E
)
```

Konsepnya:

- `CUBE(A, B)` menghasilkan beberapa set.
- `ROLLUP(C, D)` menghasilkan beberapa set.
- `E` menjadi set sendiri.
- Semua set digabung secara additive.

Multiplicative berarti kombinasi grouping dikalikan satu sama lain sehingga jumlah set bisa jauh lebih banyak.

Contoh:

```sql
GROUP BY CUBE(A, B), ROLLUP(C, D), E
```

Konsepnya:

- Semua kombinasi dari `CUBE(A, B)` dikombinasikan dengan semua level `ROLLUP(C, D)` dan `E`.
- Jumlah hasil dapat meningkat cepat.

Catatan UAS: kombinasi `CUBE`, `ROLLUP`, dan `GROUPING SETS` harus hati-hati karena bisa menghasilkan pertumbuhan jumlah result set secara eksponensial.

### Index untuk SQL OLAP

Query OLAP grouping dapat berat karena menghitung banyak agregasi. Pada tabel fakta, index dapat membantu optimasi eksekusi query OLAP.

Strategi umum:

- Buat index pada kolom yang sering digunakan untuk filtering.
- Buat index pada kolom grouping.
- Perhatikan kolom yang sering muncul dalam `GROUP BY ROLLUP`, `CUBE`, atau `GROUPING SETS`.

Contoh dari materi:

```sql
SELECT region, country, COUNT(territory)
FROM cust_dim
WHERE continent = 'AMERICA'
GROUP BY GROUPING SETS ((region), (country));
```

Index yang relevan dapat mencakup:

- `continent`
- `region`
- `country`

Dalam contoh lain, index yang baik untuk query transaksi dapat mencakup:

- `transYear`
- `country`
- `region`
- `store`

Intinya: query OLAP sering melakukan grouping dan aggregation, sehingga desain index pada tabel fakta/dimensi perlu mengikuti pola query analitik.

### Kesalahan umum SQL OLAP

1. Mengira `ORDER BY` luar sama dengan `ORDER BY` di `OVER`.

`ORDER BY` dalam `OVER` mempengaruhi perhitungan ranking/window. `ORDER BY` luar hanya mengatur tampilan hasil akhir.

2. Menggunakan alias di `WHERE` pada level query yang sama.

Alias dari `SELECT` belum tersedia saat `WHERE` diproses. Gunakan subquery atau ulangi ekspresi.

3. Bingung `RANK` dan `DENSE_RANK`.

`RANK` bisa lompat ranking. `DENSE_RANK` tidak lompat.

4. Menganggap `GROUPING SETS(workdept, job)` sama dengan `GROUP BY workdept, job`.

Tidak sama. `GROUPING SETS(workdept, job)` menghasilkan agregasi terpisah per workdept dan per job. `GROUP BY workdept, job` menghasilkan agregasi per kombinasi workdept-job.

5. Menganggap `ROLLUP` dan `CUBE` sama.

`ROLLUP` mengikuti hierarchy. `CUBE` menghasilkan semua kombinasi dimensi.

### Ringkasan cepat SQL OLAP

| Fungsi | Kegunaan |
|---|---|
| `RANK` | Ranking dengan gap jika nilai sama |
| `DENSE_RANK` | Ranking tanpa gap |
| `ROW_NUMBER` | Nomor urut unik setiap row |
| `LEAD` | Mengambil nilai row berikutnya |
| `FIRST_VALUE` | Mengambil nilai pertama dalam window |
| `ROLLUP` | Subtotal bertingkat + grand total |
| `CUBE` | Semua kombinasi agregasi dimensi |
| `GROUPING SETS` | Beberapa grouping khusus dalam satu query |
| `GROUPING` | Membedakan NULL asli dan NULL hasil aggregate |

---

## 17. Physical Design Data Warehouse

### Pengertian physical design

Physical design membahas implementasi fisik database agar data dapat disimpan dan diakses secara efisien.

Fokus:
- Storage.
- Buffer pool.
- Table space.
- Table.
- Index.
- LOB storage.
- Backup dan recovery.
- Performa query.

### Urutan pembuatan object database

Dalam materi DB2, urutan pembuatan object:

1. Data warehouse/database.
2. Buffer pool.
3. Table space.
4. Table dimension.
5. Table fact.

Table space dapat dibedakan untuk:
- Regular data.
- Index data.
- Large object data.

### Buffer pool

Buffer pool adalah area memori yang digunakan DBMS untuk menyimpan halaman data yang sering diakses.

Contoh syntax DB2:

```sql
CREATE BUFFERPOOL buffer_pool_name PAGESIZE 4096;
CREATE BUFFERPOOL buffer_pool_name PAGESIZE 4 K;
```

Makna:
- Page size menentukan ukuran halaman data.
- Buffer pool yang tepat dapat meningkatkan performa akses data.

### Table space

Table space adalah area penyimpanan logis untuk table dan index.

Contoh DB2:

```sql
CREATE LARGE TABLESPACE LARGEDATA
PAGE SIZE 8 K
BUFFERPOOL IBMDEFAULT8K
INITIALSIZE 100 M
MAXSIZE 1 G;
```

Makna:
- `PAGE SIZE 8 K`: ukuran page.
- `BUFFERPOOL IBMDEFAULT8K`: buffer pool yang digunakan.
- `INITIALSIZE 100 M`: ukuran awal.
- `MAXSIZE 1 G`: ukuran maksimum.

### Penempatan table

Dalam contoh materi, diasumsikan ada tiga table space:

- `REGULAR1` untuk regular data.
- `INDEX1` untuk index data.
- `LONG1` untuk LOB data.

Contoh:

```sql
CREATE TABLE fakta_bencana (
    id_geografi INT,
    date DATE,
    id_jenis_bencana INT,
    id_jenis_korban INT,
    jumlah_korban INT,
    FOREIGN KEY (id_geografi) REFERENCES dim_geografi(id_geografi),
    FOREIGN KEY (date) REFERENCES dim_waktu(date),
    FOREIGN KEY (id_jenis_bencana) REFERENCES dim_jenis_bencana(id_jenis_bencana),
    FOREIGN KEY (id_jenis_korban) REFERENCES dim_jenis_korban(id_jenis_korban)
)
IN REGULAR1
INDEX IN INDEX1
LONG IN LONG1;
```

Makna:
- Data table disimpan di `REGULAR1`.
- Index disimpan di `INDEX1`.
- Data LOB disimpan di `LONG1`.

### Hubungan logical dan physical design

Logical design menjawab:
- Tabel apa yang dibutuhkan?
- Apa fact dan dimension?
- Atribut apa saja?
- Relasi PK/FK apa?
- Grain fact table apa?

Physical design menjawab:
- Bagaimana tabel disimpan?
- Buffer pool apa yang digunakan?
- Table space mana yang dipakai?
- Index seperti apa yang dibutuhkan?
- Bagaimana performa query dioptimalkan?

---

## 18. Alur Lengkap Pengembangan Data Warehouse

Urutan berpikir yang bagus untuk UAS:

1. Pahami kebutuhan bisnis.
2. Kumpulkan requirement melalui interview/JAD.
3. Buat information package.
4. Tentukan measures.
5. Tentukan dimensions dan hierarchy.
6. Tentukan granularity/grain.
7. Pilih pendekatan arsitektur: Inmon, Kimball, atau hybrid.
8. Buat logical design: star, snowflake, atau fact constellation.
9. Tentukan surrogate key, PK, FK, dan SCD.
10. Rancang ETL: extract, transform, load.
11. Load dimension lebih dulu.
12. Load fact table.
13. Buat query analitik/SQL OLAP untuk ranking, subtotal, cube, rollup, dan grouping.
14. Rancang physical design: buffer pool, table space, table, index.
15. Sediakan delivery: reports, dashboards, OLAP, data mining.

### Tahapan pengembangan versi lifecycle

Chapter 7 TXT menekankan tahapan pengembangan data warehouse secara lifecycle:

1. Requirements collection.
2. Requirements definition.
3. Requirements visualization.
4. Data warehouse modeling.
5. Creating data warehouse.
6. Creating ETL infrastructure.
7. Developing BI applications.
8. Deployment.
9. Use.
10. Administration and maintenance.

Makna tiap tahap:

- Requirements collection: mengumpulkan kebutuhan dari stakeholder.
- Requirements definition: merumuskan kebutuhan menjadi dokumen yang jelas.
- Requirements visualization: membuat model konseptual atau gambaran kebutuhan analisis.
- Data warehouse modeling: membuat model logical seperti star schema atau constellation schema.
- Creating data warehouse: mengimplementasikan model pada DBMS.
- Creating ETL infrastructure: membuat proses extract, transform, load.
- Developing BI applications: membuat dashboard, report, visualisasi, dan aplikasi front-end.
- Deployment: merilis sistem kepada pengguna.
- Use: data warehouse dipakai untuk analisis.
- Administration and maintenance: menjaga performa, kualitas data, security, backup, dan perubahan kebutuhan.

Catatan penting: proses ETL biasanya menjadi salah satu bagian paling memakan waktu dalam proyek data warehouse karena harus menangani kualitas data, perbedaan format, validasi, dan integrasi sumber data.

---

## 19. Pola Jawaban UAS yang Sering Keluar

### Jika ditanya "Jelaskan data warehouse"

Jawaban ideal:

Data warehouse adalah repository data terintegrasi yang berasal dari berbagai sumber, disusun berdasarkan subject area, menyimpan histori, bersifat non-volatile, dan digunakan untuk mendukung analisis serta pengambilan keputusan. Data warehouse berbeda dari OLTP karena dirancang untuk query dan analisis, bukan transaksi harian.

### Jika ditanya "Sebutkan karakteristik DW"

Jawab:

1. Subject-oriented: data disusun berdasarkan subjek bisnis.
2. Integrated: data dari berbagai sumber disatukan dan dibuat konsisten.
3. Time-variant: data memiliki aspek waktu/histori.
4. Non-volatile: data tidak sering berubah setelah masuk warehouse.

### Jika ditanya "Bedakan OLTP dan OLAP"

Jawab:

OLTP digunakan untuk transaksi operasional harian, banyak transaksi kecil, data current, banyak update, dan dipakai user operasional. OLAP digunakan untuk analisis, query kompleks, data historis, mayoritas read, dan dipakai analis/manajemen.

### Jika ditanya "Apa itu information package?"

Jawab:

Information package adalah dokumen/diagram requirement DW untuk subject tertentu yang berisi measures, dimensions, hierarchy, granularity, dan kebutuhan analisis. Information package membantu menerjemahkan kebutuhan bisnis ke desain dimensional.

### Jika ditanya "Apa itu grain?"

Jawab:

Grain adalah tingkat detail satu baris dalam fact table. Contoh: satu row fact sales merepresentasikan penjualan per produk, per pelanggan, per tanggal. Grain harus ditentukan sebelum memilih dimensions dan facts.

### Jika ditanya "Star vs snowflake"

Jawab:

Star schema memiliki fact table pusat dan dimension table denormalized. Lebih mudah dipahami dan query lebih cepat. Snowflake schema menormalisasi dimension table menjadi beberapa tabel. Lebih hemat storage dan mudah maintain, tetapi query lebih kompleks karena lebih banyak join.

### Jika ditanya "Factless fact table"

Jawab:

Factless fact table adalah fact table tanpa measures numerik. Setiap row merepresentasikan event atau hubungan. Contoh: kehadiran mahasiswa di kelas pada tanggal tertentu. Jumlah event dihitung dari jumlah row.

### Jika ditanya "Surrogate key"

Jawab:

Surrogate key adalah primary key buatan, biasanya integer, yang menggantikan natural key dari sistem sumber. Manfaatnya adalah meningkatkan performa join, mengisolasi DW dari perubahan operational key, dan mendukung histori seperti SCD Type 2.

### Jika ditanya "SCD Type 1, 2, 3"

Jawab:

Type 1 overwrite data lama sehingga histori hilang. Type 2 menambah row baru untuk setiap perubahan sehingga histori lengkap tersimpan. Type 3 menambah kolom untuk nilai lama dan nilai sekarang sehingga hanya menyimpan histori terbatas.

### Jika ditanya "Inmon vs Kimball"

Jawab:

Inmon memakai pendekatan top-down, membangun enterprise data warehouse terintegrasi lebih dulu, lalu data mart. Cocok untuk kebutuhan strategis dan integrasi enterprise. Kimball memakai pendekatan bottom-up, membangun data mart berdasarkan business process dengan dimensional model dan conformed dimensions. Cocok untuk delivery cepat dan kebutuhan analisis user.

### Jika ditanya "Langkah desain Kimball"

Jawab:

1. Select business process.
2. Declare the grain.
3. Choose dimensions.
4. Identify facts.

### Jika ditanya "Apa itu ETL?"

Jawab:

ETL adalah proses Extract, Transform, Load. Extract mengambil data dari sumber, Transform membersihkan/mengubah/menggabungkan data, dan Load memasukkan data ke data warehouse. Dalam DW, dimension biasanya di-load terlebih dahulu sebelum fact table.

### Jika ditanya "Apa itu SQL OLAP?"

Jawab:

SQL OLAP adalah penggunaan fungsi SQL untuk analisis data, seperti ranking, row numbering, pembandingan nilai antar row, subtotal, grand total, dan agregasi multidimensi. Contoh fungsinya adalah `RANK`, `DENSE_RANK`, `ROW_NUMBER`, `LEAD`, `FIRST_VALUE`, `ROLLUP`, `CUBE`, `GROUPING SETS`, dan `GROUPING`.

### Jika ditanya "Bedakan RANK dan DENSE_RANK"

Jawab:

`RANK` memberi ranking yang sama untuk nilai yang sama, tetapi ranking berikutnya bisa lompat. `DENSE_RANK` juga memberi ranking yang sama untuk nilai yang sama, tetapi ranking berikutnya tidak lompat.

### Jika ditanya "Bedakan ROLLUP dan CUBE"

Jawab:

`ROLLUP` menghasilkan subtotal bertingkat berdasarkan urutan hierarchy kolom, misalnya detail per country-region, subtotal country, lalu grand total. `CUBE` menghasilkan agregasi untuk semua kombinasi dimensi, misalnya country-region, country saja, region saja, dan grand total.

### Jika ditanya "Apa fungsi GROUPING SETS?"

Jawab:

`GROUPING SETS` digunakan untuk menentukan beberapa bentuk grouping dalam satu query. Misalnya satu query bisa sekaligus menghasilkan agregasi per `(country, region)` dan per `(country, store)`.

### Jika ditanya "Logical vs physical design"

Jawab:

Logical design fokus pada struktur konseptual seperti fact, dimension, atribut, relationship, grain, star/snowflake schema. Physical design fokus pada implementasi penyimpanan seperti buffer pool, table space, table placement, index, backup, recovery, dan performa query.

---

## 20. Mini Contoh Desain DW Penjualan

### Requirement

Manajemen ingin menganalisis:
- Total pendapatan per produk, pelanggan, dan tanggal.
- Total quantity pembelian per produk.
- Jumlah pelanggan per bulan, quarter, dan tahun.

### Measures

- quantity_ordered
- price_each
- price_total = quantity_ordered * price_each
- count customer

### Dimensions

- Product
- Customer
- Date

### Grain

Satu row fact table merepresentasikan penjualan untuk satu produk, satu pelanggan, pada satu tanggal.

### Star schema

FactSales:
- product_key/productCode
- customer_key/customerNumber
- date_key/sk
- quantity_ordered
- price_each
- price_total

DimProduct:
- product_key
- productCode
- productName
- productDescription
- buyPrice

DimCustomer:
- customer_key
- customerNumber
- customerName
- city
- state
- postalCode
- country

DimDate:
- date_key/sk
- date
- day
- month
- month_name
- quarter
- year

### ETL

1. Extract dari `classicmodels`.
2. Load `dim_products` dari tabel products.
3. Load `dim_customers` dari tabel customers.
4. Generate dan load `dim_date`.
5. Transform `orderdetails` dan order date menjadi fact.
6. Hitung `price_total`.
7. Load ke `fact_sales`.

---

## 21. Checklist Belajar Cepat Malam Sebelum UAS

Prioritas tinggi:
- Definisi DW dan empat karakteristik Inmon.
- OLTP vs OLAP.
- Data warehouse vs data mart.
- Inmon vs Kimball.
- Measures, dimensions, hierarchy, granularity.
- Information package.
- Star, snowflake, fact constellation.
- Factless fact table.
- Surrogate key.
- SCD Type 1, Type 2, Type 3.
- ETL dan urutan load dimension/fact.
- SQL OLAP: `RANK`, `DENSE_RANK`, `ROW_NUMBER`, `ROLLUP`, `CUBE`, `GROUPING SETS`.
- Logical vs physical design.

Latihan wajib:

1. Ambil satu studi kasus, misalnya penjualan toko roti.
2. Tentukan subject.
3. Buat measures.
4. Buat dimensions.
5. Tentukan hierarchy.
6. Tentukan grain.
7. Gambar star schema.
8. Ubah beberapa dimension menjadi snowflake.
9. Tentukan kemungkinan SCD.
10. Jelaskan ETL singkat.

---

## 22. Contoh Latihan Singkat

### Studi kasus: penjualan toko roti

Subject:
- Penjualan roti.

Measures:
- quantity_sold
- unit_price
- total_sales
- discount
- net_sales

Dimensions:
- Product: roti, kategori, ukuran.
- Customer: pelanggan, kota, segment.
- Store: toko, cabang, kota.
- Time: tanggal, bulan, quarter, tahun.
- Payment: metode pembayaran.

Grain:
- Satu row fact merepresentasikan satu produk yang terjual dalam satu transaksi pada satu toko dan satu tanggal.

FactSales:
- product_key
- customer_key
- store_key
- date_key
- payment_key
- quantity_sold
- unit_price
- total_sales
- discount
- net_sales

Contoh hierarchy:
- Time: day -> month -> quarter -> year.
- Product: product -> category.
- Store: store -> city -> region.

Contoh SCD:
- Jika customer pindah kota dan histori kota penting, gunakan SCD Type 2.
- Jika hanya ingin memperbaiki nama customer yang salah ketik, gunakan SCD Type 1.

---

## 23. Kesimpulan Besar

Data warehouse bukan hanya database besar. Intinya adalah sistem analitik yang mengintegrasikan data dari banyak sumber, menyimpan histori, menyajikan data berdasarkan subject bisnis, dan mendukung decision making.

Alur pikir yang harus dikuasai:

Requirement bisnis menghasilkan information package. Information package menghasilkan measures, dimensions, hierarchy, dan grain. Dari sana dibuat logical design seperti star schema atau snowflake schema. Perubahan dimensi ditangani dengan SCD. Data dimasukkan melalui ETL. Data yang sudah tersimpan dianalisis dengan OLAP/SQL OLAP seperti ranking, rollup, cube, dan grouping sets. Setelah itu physical design menentukan bagaimana struktur tersebut disimpan dan dioptimalkan di DBMS.
