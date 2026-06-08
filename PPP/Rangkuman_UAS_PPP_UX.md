# Rangkuman UAS Perancangan Pengalaman Pengguna

Fokus rangkuman ini adalah materi UX yang relevan untuk UAS, disusun mengikuti alur praktikum Kelompok 8 pada proyek Domma: POS. Materi non-UX dari PDF diabaikan.

## 1. Gambaran Besar UX

User Experience (UX) adalah pengalaman menyeluruh yang dirasakan pengguna ketika berinteraksi dengan produk, sistem, atau layanan. UX tidak hanya membahas tampilan antarmuka, tetapi juga apakah produk benar-benar membantu pengguna mencapai tujuannya dengan mudah, cepat, jelas, dan memuaskan.

Dalam konteks pengembangan perangkat lunak, UX penting karena desain yang buruk bisa menyebabkan:

- pengguna bingung memahami alur sistem;
- pengguna butuh waktu lama menyelesaikan tugas;
- banyak error atau salah klik;
- fitur ada, tetapi tidak sesuai kebutuhan nyata;
- sistem tidak dipakai karena terasa rumit atau tidak bernilai.

Investasi UX sebaiknya dilakukan sejak fase awal desain karena memperbaiki kesalahan saat desain masih berupa konsep, wireframe, atau prototype jauh lebih murah daripada memperbaiki produk setelah implementasi.

## 2. UX, UI, dan Usability

UX berbeda dari UI. UI berfokus pada tampilan dan komponen antarmuka, seperti warna, tombol, ikon, layout, tipografi, dan visual. UX lebih luas: mencakup riset pengguna, pemahaman masalah, alur tugas, struktur informasi, interaksi, emosi pengguna, evaluasi, dan nilai produk.

Usability adalah bagian penting dari UX. Produk yang usable harus mudah dipahami, mudah dipelajari, mudah dioperasikan, efisien, dan membantu pengguna menyelesaikan tugas secara tepat.

Aspek usability yang sering muncul:

- Understandability: pengguna memahami fungsi dan alur.
- Learnability: pengguna cepat belajar menggunakan sistem.
- Operability: pengguna mudah mengoperasikan fitur.
- Attractiveness: tampilan terasa menarik dan nyaman.
- Efficiency: pengguna bisa menyelesaikan tugas dengan cepat dan hemat usaha.
- Error tolerance: sistem mencegah error atau membantu pengguna pulih dari error.
- Satisfaction: pengguna merasa puas setelah memakai produk.

Dalam kualitas perangkat lunak, efficiency dapat dilihat dari time behaviour dan resource utilisation. Untuk UX, time behaviour penting karena berhubungan dengan seberapa cepat pengguna menyelesaikan tugas.

## 3. Pendekatan Perancangan UX

Beberapa pendekatan yang dipelajari:

- 5 Planes of UX Elements by Garrett.
- User-Centered Design (UCD).
- Human-Centered Design (HCD).
- Design Thinking.
- Design Sprint.
- Agile UX.
- Lean UX.

Semua pendekatan tersebut menempatkan kebutuhan pengguna sebagai dasar perancangan. Perbedaannya ada pada cara kerja, ritme, dan fokus proses. Dalam praktikum, alur yang paling kuat adalah Design Thinking dan HCD.

## 4. Human-Centered Design (HCD)

HCD adalah pendekatan desain yang menempatkan manusia sebagai pusat pemecahan masalah. Produk dirancang dengan memahami konteks, kebutuhan, kemampuan, hambatan, dan tujuan pengguna.

Dalam HCD versi IDEO, prosesnya dapat dipahami sebagai:

- Inspiration: belajar langsung dari pengguna dan memahami kehidupan serta kebutuhannya.
- Ideation: mengolah hasil riset menjadi insight, peluang desain, dan alternatif solusi.
- Implementation: membawa solusi menjadi prototype, produk, atau layanan nyata.

Dalam HCD versi ISO, prosesnya dapat dipahami sebagai:

- memahami dan menentukan konteks penggunaan;
- menentukan kebutuhan pengguna dan organisasi;
- menghasilkan solusi desain atau prototype;
- mengevaluasi desain bersama pengguna terhadap kebutuhan yang sudah ditentukan.

Intinya, desain tidak boleh hanya berdasarkan asumsi tim. Desain harus divalidasi melalui interaksi dengan pengguna.

## 5. Design Thinking

Design Thinking adalah pendekatan pemecahan masalah yang iteratif dan berpusat pada manusia. Tahap utamanya:

1. Empathize
2. Define
3. Ideate
4. Prototype
5. Test

Proses ini tidak selalu linear. Jika hasil test menunjukkan masalah baru, tim dapat kembali ke tahap define, ideate, atau prototype.

### Empathize

Empathize adalah tahap memahami pengguna. Pertanyaan utamanya:

- Siapa pengguna?
- Apa aktivitas mereka?
- Apa masalah yang mereka alami?
- Apa yang mereka pikirkan dan rasakan?
- Apa kebutuhan, tujuan, dan hambatan mereka?

Metode yang digunakan:

- user interview;
- observasi;
- forum group discussion;
- survey;
- pengumpulan data lapangan.

Pada proyek Kelompok 8, tahap empathize dilakukan dengan mewawancarai tiga tipe pengguna UMKM:

- Pak Afif: pemilik fotokopi dan ATK.
- Pak Yogo: pemilik UMKM sirup dengan sistem sales keliling atau canvassing.
- Pak Faizal: pemilik warung sembako.

Masalah utama yang ditemukan:

- pencatatan transaksi masih manual;
- transaksi sering lupa dicatat saat toko ramai;
- stok sulit dipantau secara real-time;
- selisih uang dan catatan saat rekap malam;
- barang kadaluarsa sulit dilacak;
- sistem POS umum tidak cocok untuk model bisnis tertentu, misalnya canvassing;
- pemilik usaha butuh aplikasi yang sederhana, cepat, dan tidak membebani.

### Define

Define adalah tahap merumuskan masalah inti berdasarkan hasil riset. Tujuannya bukan langsung membuat fitur, tetapi memastikan masalah yang diselesaikan benar-benar penting bagi pengguna.

Deliverable yang umum:

- persona;
- empathy map;
- affinity map;
- user story;
- user journey map;
- problem statement;
- design challenge;
- How Might We;
- problem-solution fit;
- value proposition canvas.

Contoh dari proyek Domma: POS:

Masalah tidak hanya "pemilik UMKM butuh aplikasi kasir", tetapi lebih spesifik: pemilik UMKM membutuhkan cara cepat dan akurat untuk mencatat transaksi, memantau stok, menghindari barang kadaluarsa, dan melihat laporan keuangan tanpa rekap manual yang melelahkan.

Contoh How Might We:

- Bagaimana kita dapat membantu pemilik UMKM mencatat transaksi saat toko ramai tanpa membuat proses pelayanan melambat?
- Bagaimana kita dapat membantu pemilik warung melihat stok dan barang kadaluarsa tanpa mengecek rak satu per satu?
- Bagaimana kita dapat membantu pemilik usaha memahami pendapatan harian tanpa menghitung manual di akhir hari?

### Ideate

Ideate adalah tahap menghasilkan banyak ide solusi. Pada tahap ini, tim tidak langsung memilih satu solusi pertama. Tim perlu membuka kemungkinan sebanyak mungkin, lalu memilih ide yang paling relevan.

Aturan brainstorming:

- tunda penilaian;
- dorong ide liar;
- bangun ide dari ide orang lain;
- tetap fokus pada masalah;
- satu percakapan pada satu waktu;
- gunakan visualisasi;
- utamakan kuantitas ide.

Dalam praktikum, Kelompok 8 menggunakan Crazy-8. Setiap anggota membuat delapan sketsa ide dalam waktu terbatas. Ide yang muncul antara lain:

- dashboard penjualan dan stok kritis;
- scan barcode;
- scan expired date;
- pembayaran tunai dan QRIS;
- nota digital via WhatsApp;
- laporan keuangan harian, mingguan, bulanan;
- daily check-in streak;
- voice search;
- katalog produk;
- quick grid untuk produk yang sering dibeli;
- notifikasi stok rendah.

Setelah ide terkumpul, dilakukan voting dan clustering untuk menentukan fitur yang paling prioritas.

### Prototype

Prototype adalah representasi solusi yang dapat diuji sebelum produk dibuat penuh. Prototype bisa low-fidelity, mid-fidelity, atau high-fidelity.

Jenis prototype:

- Sketch: gambar kasar ide antarmuka.
- Wireframe: struktur halaman dan tata letak tanpa detail visual penuh.
- Mockup: tampilan visual lebih matang, biasanya belum interaktif.
- High-fidelity prototype: tampilan dan interaksi sudah mendekati produk nyata.

Pada proyek Domma: POS, prototype dibuat di Figma. Fitur utama yang diprototipekan:

- onboarding, login, register;
- dashboard;
- produk;
- stok;
- kasir;
- scan barcode;
- transaksi tunai dan QRIS;
- struk via WhatsApp;
- laporan keuangan;
- profil dan gamifikasi streak.

Prototype berguna untuk memvalidasi apakah alur, navigasi, tombol, dan informasi dapat dipahami pengguna sebelum masuk implementasi.

### Test

Test adalah tahap menguji rancangan kepada pengguna. Tujuannya menemukan masalah usability, mengukur keberhasilan tugas, dan mendapatkan masukan untuk perbaikan desain.

Pada proyek Domma: POS, pengujian dilakukan dengan Maze menggunakan prototype Figma. Task yang diuji meliputi:

- onboarding atau masuk ke aplikasi;
- menambahkan stok barang dengan Smart Scanner;
- melakukan transaksi dengan QRIS;
- mengirim nota digital via WhatsApp;
- mencari informasi laporan atau laba bersih.

Metrik yang digunakan:

- success rate;
- misclick rate;
- drop-off;
- durasi penyelesaian tugas;
- rating kepuasan pengguna;
- feedback kualitatif.

Temuan penting:

- fitur kirim nota via WhatsApp paling intuitif, dengan keberhasilan 100% dan misclick 0%;
- onboarding berhasil diselesaikan, tetapi misclick tinggi yaitu 77,9% dan durasi 189,1 detik;
- Smart Scanner masih memiliki misclick cukup tinggi yaitu 45%;
- pencarian laporan mendalam memiliki drop-off 20%;
- skor kemudahan penggunaan 4,6 dari 5;
- integrasi fitur 4,4 dari 5;
- kejelasan navigasi 3,8 dari 5, menjadi aspek yang paling perlu diperbaiki.

Rekomendasi perbaikan:

- sederhanakan onboarding;
- tambahkan tombol Skip;
- bedakan elemen informatif dan elemen yang bisa diklik;
- tambahkan coachmark atau panduan singkat;
- perbaiki posisi grafik laporan agar lebih mudah ditemukan;
- perjelas state tombol aktif;
- perbaiki masalah scroll pada katalog produk.

## 6. UX Strategy

UX Strategy adalah rencana untuk menyelaraskan pengalaman pengguna dengan tujuan bisnis. UX strategy berada di persimpangan antara UX design dan business strategy.

Komponen penting UX strategy:

- Product vision.
- Business goal.
- Team profile.
- User research plan.
- User interview.
- Competitor analysis.
- Persona.
- Empathy map.
- User stories.
- Affinity map.
- How Might We.
- Design challenge.
- Problem-solution fit.
- Validation board.
- Goal-task-action.
- Value proposition canvas.

Dalam Product Vision Board, komponen utamanya:

- Vision: tujuan utama produk dan dampak positif yang ingin dibuat.
- Target group: kelompok pengguna yang dituju.
- Needs: kebutuhan, pain point, dan alasan pengguna mau memakai produk.
- Product: fitur utama yang membuat produk bernilai.
- Business goals: tujuan bisnis dan alasan produk layak dikembangkan.

Pada Domma: POS:

- Vision: membantu pemilik UMKM mengelola stok dan transaksi secara efektif tanpa pencatatan manual.
- Target group: pemilik warung, toko kelontong, fotokopi, retail kecil, dan UMKM.
- Needs: pencatatan otomatis, stok real-time, laporan praktis, pelacakan kadaluarsa.
- Product: aplikasi Android POS dan inventaris yang sederhana.
- Business goals: freemium atau langganan, retensi pengguna, penggunaan harian, dan potensi ekosistem data transaksi.

UX strategy memastikan desain tidak hanya bagus secara tampilan, tetapi juga relevan untuk pengguna dan masuk akal secara bisnis.

## 7. User Research

User research adalah proses mengumpulkan informasi tentang pengguna untuk memahami kebutuhan, perilaku, masalah, motivasi, dan konteks penggunaan.

Sebelum melakukan riset, perlu membuat research plan:

- tujuan riset;
- metode riset;
- partisipan atau stakeholder;
- lokasi;
- daftar pertanyaan atau script;
- alat dan media;
- metode analisis data;
- konfirmasi dan persetujuan;
- timeline.

Dalam interview, pertanyaan sebaiknya menggali cerita, bukan hanya jawaban ya atau tidak. Pertanyaan yang baik mendorong pengguna bercerita tentang rutinitas, masalah, keputusan, dan pengalaman nyata.

Contoh pertanyaan:

- Bagaimana rutinitas harian Bapak/Ibu dalam mengelola toko?
- Bagian mana yang paling melelahkan saat mencatat transaksi?
- Pernahkah stok habis tanpa diketahui?
- Apa yang terjadi ketika catatan tidak sesuai dengan uang fisik?
- Sistem seperti apa yang terasa ideal bagi usaha Bapak/Ibu?

Hasil riset kemudian diterjemahkan menjadi insight, bukan sekadar daftar keluhan.

## 8. Persona

Persona adalah profil pengguna representatif yang menggambarkan karakteristik, perilaku, tujuan, kebutuhan, motivasi, dan frustrasi segmen pengguna tertentu.

Persona tidak boleh hanya berisi data demografis. Persona harus menangkap:

- kebiasaan;
- konteks kerja;
- kemampuan teknologi;
- motivasi;
- pain point;
- kebutuhan;
- tujuan;
- hambatan.

Persona pada Domma: POS:

- Pak Afif: butuh transaksi cepat, stok otomatis, dan laporan keuntungan harian karena sering lelah dengan pencatatan manual.
- Pak Yogo: butuh alokasi stok per sales, pembatasan akses data, nota PDF profesional, dan laporan performa sales.
- Pak Faizal: butuh tampilan sederhana, pemantauan stok, scan barang, dan pelacakan tanggal kadaluarsa.

Persona membantu tim membuat keputusan desain berdasarkan pengguna nyata, bukan asumsi desainer.

## 9. Empathy Map

Empathy map adalah alat visual untuk memahami pengguna dari berbagai sisi:

- Think & Feel: apa yang dipikirkan dan dirasakan pengguna.
- Say & Do: apa yang dikatakan dan dilakukan pengguna.
- See: apa yang dilihat di lingkungan pengguna.
- Hear: apa yang didengar dari orang lain, keluarga, supplier, kompetitor.
- Pain: hambatan, frustrasi, risiko.
- Gain: harapan, motivasi, ukuran keberhasilan.

Pada Domma: POS, empathy map membantu menemukan bahwa masalah UMKM bukan hanya "tidak punya aplikasi", tetapi:

- takut salah hitung;
- lelah rekap manual;
- khawatir stok habis;
- sulit melacak kadaluarsa;
- ingin terlihat lebih profesional;
- butuh sistem yang sederhana karena waktu dan literasi digital terbatas.

Empathy map mengubah data interview menjadi pemahaman yang lebih manusiawi.

## 10. Mental Model

Mental model adalah cara pengguna memahami bagaimana sesuatu bekerja berdasarkan pengalaman, kebiasaan, dan pengetahuan sebelumnya.

Dalam desain UX, sistem sebaiknya mendekati mental model pengguna. Jika desain terlalu jauh dari cara berpikir pengguna, pengguna akan bingung walaupun fiturnya lengkap.

Contoh pada Domma: POS:

- Pengguna terbiasa melihat barang secara fisik di rak, sehingga dashboard stok harus sederhana dan mudah dipindai.
- Pengguna terbiasa menulis nota, sehingga nota digital harus terasa seperti bukti transaksi yang familiar.
- Pengguna terbiasa menghitung uang harian, sehingga laporan harian harus mudah ditemukan dan langsung menunjukkan pendapatan atau laba.
- Pengguna UMKM tidak ingin alur terlalu banyak langkah, sehingga transaksi harus cepat.

Mental model ditemukan melalui interview, observasi, survey, persona, empathy map, dan affinity diagram.

## 11. User Journey Map

User journey map adalah visualisasi langkah-langkah pengguna dalam mencapai tujuan tertentu. Journey map membantu melihat pengalaman pengguna secara kronologis, termasuk tindakan, pikiran, emosi, pain point, touchpoint, dan opportunity.

Elemen journey map:

- aktor;
- skenario;
- goals and expectations;
- journey phase;
- actions;
- thinking;
- feeling and emotional experience;
- touchpoint;
- opportunity atau insight.

Ada dua jenis journey map penting:

- Retrospective journey map: menggambarkan kondisi saat ini atau pengalaman sebelum solusi.
- Prospective journey map: menggambarkan pengalaman ideal setelah solusi digunakan.

Pada Domma: POS, retrospective journey menunjukkan kondisi manual:

- pagi: cek stok fisik;
- jam sibuk: melayani pelanggan sambil menghitung dan mencatat;
- operasional: memeriksa stok dan kadaluarsa manual;
- malam: rekap uang dan catatan.

Pain point utamanya:

- multitasking berat;
- human error;
- transaksi terlewat;
- stok tidak akurat;
- rekap malam melelahkan;
- emosi turun saat data tidak cocok.

Prospective journey menunjukkan kondisi setelah memakai aplikasi:

- stok dicek melalui dashboard;
- barang discan;
- transaksi diproses cepat;
- pembayaran tunai atau QRIS;
- nota dikirim digital;
- laporan langsung tersedia;
- pemilik merasa lebih tenang.

Journey map menghubungkan pain point ke peluang fitur.

## 12. Storyboard

Storyboard adalah ilustrasi naratif yang menunjukkan bagaimana pengguna mengalami masalah dan bagaimana solusi membantu mereka. Storyboard berguna untuk menjelaskan skenario penggunaan secara visual dan emosional.

Pada Domma: POS, storyboard menggunakan persona Pak Faizal:

- sebelum aplikasi: antrean ramai, nota berantakan, stok dan kadaluarsa sulit dicek;
- mulai memakai aplikasi: scan barcode dan pencatatan otomatis;
- setelah memakai aplikasi: stok berkurang otomatis, notifikasi stok rendah muncul, laporan keuntungan tersedia.

Dari sisi UX, storyboard menunjukkan perubahan dari high cognitive load menjadi interaksi yang lebih lancar. Sistem tidak hanya mencatat, tetapi membantu pengguna mengurangi beban pikiran.

## 13. User Story dan User Scenario

User story menjelaskan kebutuhan dari sudut pandang pengguna. Format umum:

Sebagai [tipe pengguna], saya ingin [tujuan], agar [manfaat].

Contoh Domma: POS:

- Sebagai pemilik toko, saya ingin mendaftar dan masuk ke sistem agar data transaksi usaha saya tersimpan aman.
- Sebagai pemilik usaha, saya ingin melihat ringkasan performa bisnis dan status stok secara instan agar dapat memantau kondisi toko dalam sekali lihat.
- Sebagai kasir, saya ingin memilih produk dan memproses pembayaran agar transaksi pelanggan selesai cepat.
- Sebagai pengelola barang, saya ingin menambah data produk agar inventaris selalu terdata.
- Sebagai pemilik toko, saya ingin melihat rekap keuangan berdasarkan periode agar dapat mengevaluasi laba rugi.

User scenario menjelaskan langkah-langkah pengguna saat menjalankan tugas tertentu. Scenario membantu menentukan urutan layar dan user flow.

## 14. Goal, Task, Action

Goal adalah tujuan akhir pengguna. Task adalah rangkaian aktivitas untuk mencapai goal. Action adalah tindakan spesifik dalam sistem.

Contoh:

Goal: menyelesaikan transaksi pelanggan.

Task:

- membuka menu kasir;
- memasukkan produk;
- memilih metode pembayaran;
- menyelesaikan pembayaran;
- mengirim nota.

Action:

- tap menu Kasir;
- scan barcode;
- input jumlah;
- pilih QRIS;
- tap Bayar;
- tap Kirim via WhatsApp.

Goal-task-action membantu tim merancang user flow yang jelas dan tidak melewatkan langkah penting.

## 15. User Flow

User flow adalah diagram alur yang menunjukkan jalur pengguna saat memakai sistem untuk mencapai tujuan.

Dalam Domma: POS, user flow dimulai dari:

- onboarding;
- login atau register;
- dashboard;
- pilihan fitur utama seperti produk, stok, kasir, laporan, profil.

Contoh flow transaksi:

- pengguna masuk dashboard;
- memilih menu kasir;
- scan barcode atau input manual;
- sistem memeriksa apakah barang terdeteksi;
- pengguna memasukkan jumlah;
- memilih metode pembayaran;
- review pembelanjaan;
- transaksi berhasil;
- nota digital dibuat;
- nota dikirim via WhatsApp;
- data masuk ke laporan.

User flow penting karena memastikan navigasi sistem sesuai tugas pengguna dan tidak menimbulkan langkah yang membingungkan.

## 16. Information Architecture

Information Architecture (IA) adalah struktur informasi agar pengguna mudah menemukan apa yang dibutuhkan. IA membantu menentukan menu, kategori, struktur halaman, dan hubungan antar konten.

Pada Domma: POS, struktur menu utama:

- Home atau Dashboard;
- Produk;
- Stok;
- Kasir;
- Laporan;
- Profil.

IA yang baik membuat pengguna tidak perlu mengingat terlalu banyak. Informasi penting seperti stok kritis, penjualan hari ini, dan laporan harus mudah ditemukan.

Masalah pada pengujian Domma menunjukkan bahwa laporan mendalam kurang mudah ditemukan. Ini berarti IA atau penempatan menu laporan perlu diperbaiki.

## 17. Design Solution

Design solution adalah tahap menerjemahkan insight menjadi model interaksi dan rancangan antarmuka.

Alurnya:

- riset menghasilkan insight;
- insight menghasilkan design challenge;
- design challenge menghasilkan ide;
- ide dipetakan menjadi conceptual model;
- conceptual model diterjemahkan ke interaction model;
- interaction model diwujudkan dalam wireframe, mockup, dan prototype.

Dalam materi, hubungan pentingnya:

- Mental Model: cara pengguna berpikir.
- Conceptual Model/System Model: bagaimana sistem disusun.
- Interaction Model: bagaimana pengguna berinteraksi dengan sistem.

Design solution harus mempertimbangkan:

- user flow;
- screen flow;
- wireframe;
- storyboard;
- visual design;
- typography;
- color palette;
- icons;
- micro-interaction;
- high-fidelity prototype.

## 18. Wireframe, Mockup, dan Prototype

Wireframe adalah kerangka halaman. Fokusnya pada struktur dan fungsi, bukan detail visual.

Mockup adalah tampilan visual yang lebih matang, biasanya sudah menggunakan warna, font, ikon, dan layout final.

Prototype adalah rancangan yang dapat diklik atau diuji, sehingga pengguna bisa mencoba alur.

Pada Domma: POS, high-fidelity wireframe mencakup:

- introduction;
- login dan register;
- dashboard dengan penjualan, grafik, dan stok kritis;
- manajemen produk dan stok;
- smart scanner;
- kasir;
- pembayaran tunai atau QRIS;
- transaksi berhasil;
- struk digital;
- laporan keuangan;
- profil dan gamifikasi.

High-fidelity prototype menambahkan interaksi dinamis untuk mensimulasikan pengalaman nyata.

## 19. Micro-interaction

Micro-interaction adalah respons kecil sistem terhadap aksi pengguna. Contoh:

- tombol berubah warna saat aktif;
- animasi sukses setelah transaksi;
- loading saat scan barcode;
- pesan error saat input salah;
- notifikasi stok rendah;
- coachmark untuk pengguna baru.

Micro-interaction penting karena memberi feedback, mengurangi kebingungan, dan membuat sistem terasa responsif.

Dalam hasil testing Domma, state tombol "Simpan" perlu diperjelas. Ini contoh masalah micro-interaction dan aksesibilitas.

## 20. Gamifikasi dalam UX

Gamifikasi adalah penggunaan elemen game untuk meningkatkan motivasi dan keterlibatan pengguna. Dalam UX, gamifikasi harus mendukung tujuan pengguna, bukan sekadar hiasan.

Ide gamifikasi Domma:

- daily check-in streak;
- streak point;
- perfect day bonus;
- merchant leveling;
- merchant elite championship;
- trust badges.

Tujuan UX dari gamifikasi:

- meningkatkan retensi;
- membangun kebiasaan penggunaan;
- membuat aktivitas administratif terasa lebih ringan;
- memberi rasa pencapaian;
- mendorong pengguna menjaga data tetap rapi.

Namun, gamifikasi harus tetap relevan. Untuk aplikasi POS UMKM, gamifikasi yang baik adalah yang mendorong disiplin mencatat transaksi, update stok, dan tutup kas.

## 21. UX Evaluation

UX evaluation adalah pengujian desain untuk memahami apakah rancangan sudah membantu pengguna. Evaluasi bisa dilakukan pada low-fidelity, mid-fidelity, high-fidelity, atau produk yang sudah rilis.

Hal yang dievaluasi:

- Utility: apakah fungsi sistem berguna?
- Usability: apakah mudah dan efisien digunakan?
- Aesthetics: apakah tampilan menarik?
- Identification: apakah pengguna merasa cocok dengan produk?
- Stimulation: apakah produk memberi inspirasi atau pengalaman menarik?
- Value: apakah produk penting dan bernilai bagi pengguna?

Tujuan evaluasi UI/UX:

- menguji efek antarmuka pada performa dan kepuasan pengguna;
- mengidentifikasi masalah usability;
- mengevaluasi akses pengguna terhadap fitur;
- membandingkan alternatif desain;
- mendapatkan dasar untuk iterasi desain.

## 22. Jenis Evaluasi

Formative evaluation dilakukan selama proses pengembangan. Tujuannya menemukan masalah dan memperbaiki desain.

Summative evaluation dilakukan untuk menilai produk secara keseluruhan, biasanya di akhir, dengan metrik kuantitatif atau perbandingan.

Inspection methods adalah evaluasi oleh evaluator atau ahli, misalnya:

- cognitive walkthrough;
- heuristic evaluation;
- guidelines review.

Usability testing adalah evaluasi dengan pengguna nyata yang menjalankan tugas tertentu.

## 23. Usability Testing

Usability testing adalah cara memahami bagaimana pengguna nyata menggunakan produk. Prinsip utamanya:

- gunakan user, bukan hanya tim sendiri;
- uji fitur atau task, bukan hanya bertanya pendapat;
- tugas penguji adalah mengamati;
- jangan terlalu cepat membantu pengguna;
- catat kebingungan, error, waktu, dan komentar pengguna.

Tahapan usability testing:

1. Planning phase
2. Execution phase
3. Data collection
4. Data analysis

Planning phase mencakup:

- siapa partisipan;
- bagaimana partisipan direkrut;
- siapa moderator dan observer;
- kapan dan di mana tes dilakukan;
- alat yang digunakan;
- task yang diuji;
- kriteria keberhasilan;
- data yang dikumpulkan;
- protokol pengujian.

Execution phase mencakup:

- menyambut partisipan;
- menjelaskan tujuan;
- meminta izin perekaman;
- menjelaskan bahwa yang diuji adalah sistem, bukan kemampuan pengguna;
- memberikan task satu per satu;
- mengamati;
- melakukan debriefing.

Etika testing:

- hasil individu dijaga;
- pengguna boleh berhenti kapan saja;
- lingkungan harus nyaman;
- jangan menertawakan kesalahan pengguna;
- jangan memberi bantuan berlebihan;
- ucapkan terima kasih.

## 24. Designing Test Tasks

Task usability test harus:

- representatif terhadap aktivitas nyata;
- mencakup bagian penting UI;
- tidak terlalu lama;
- berorientasi goal atau hasil;
- tidak membingungkan;
- task pertama sebaiknya membangun rasa percaya diri;
- task terakhir memberi rasa pencapaian.

Contoh task Domma:

- Tambahkan lima barang baru menggunakan Smart Scanner.
- Proses transaksi tiga barang dengan QRIS.
- Kirim nota digital melalui WhatsApp.
- Cari informasi laba bersih harian.
- Selesaikan onboarding dan masuk ke dashboard.

## 25. Metrik Usability

Metrik objektif:

- task completion;
- time on task;
- error rate;
- misclick rate;
- drop-off rate;
- success rate.

Metrik subjektif:

- rating kemudahan;
- rating kepuasan;
- komentar pengguna;
- kuesioner SUS;
- UEQ;
- skala Likert.

Data kuantitatif berupa angka, seperti persentase keberhasilan dan durasi. Data kualitatif berupa alasan, komentar, ekspresi, dan insight dari perilaku pengguna.

## 26. Usability Aspect 5E

Aspek usability dapat diingat dengan 5E:

- Easy to use: mudah digunakan.
- Easy to learn: mudah dipelajari.
- Efficient: hemat waktu dan usaha.
- Engaging: menarik dan membuat pengguna mau kembali.
- Error tolerant: mencegah error dan membantu pemulihan.

Aspek lain dari Nielsen:

- learnability;
- efficiency of use;
- memorability;
- few and non-catastrophic errors;
- subjective satisfaction.

Pada Domma, masalah onboarding menunjukkan learnability belum optimal. Masalah laporan menunjukkan findability dan IA perlu diperbaiki. Fitur nota WhatsApp menunjukkan task flow sudah sangat usable.

## 27. SUS

System Usability Scale (SUS) adalah kuesioner 10 item untuk mengukur persepsi kemudahan penggunaan sistem. Jawaban menggunakan skala 1 sampai 5.

Cara scoring:

- Untuk item ganjil: skor jawaban dikurangi 1.
- Untuk item genap: 5 dikurangi skor jawaban.
- Jumlahkan semua hasil.
- Kalikan 2,5 agar menjadi skor 0 sampai 100.

Interpretasi umum:

- SUS di atas 68 dianggap di atas rata-rata.
- SUS di bawah 68 dianggap di bawah rata-rata.

SUS mengukur persepsi usability dan learnability, bukan menggantikan observasi task.

## 28. UEQ

User Experience Questionnaire (UEQ) adalah kuesioner untuk mengukur UX dengan 6 skala:

- Attractiveness: apakah produk disukai?
- Perspicuity: apakah produk mudah dipahami dan dipelajari?
- Efficiency: apakah pengguna bisa menyelesaikan tugas tanpa usaha berlebihan?
- Dependability: apakah pengguna merasa terkendali?
- Stimulation: apakah produk menarik dan memotivasi?
- Novelty: apakah produk terasa inovatif dan kreatif?

UEQ berguna untuk membandingkan desain awal dan desain perbaikan, atau membandingkan produk dengan kompetitor.

## 29. Heuristic Evaluation

Heuristic evaluation adalah evaluasi oleh evaluator menggunakan prinsip usability. Biasanya dilakukan oleh beberapa evaluator, idealnya 3 sampai 5 orang berpengalaman.

10 heuristik Nielsen:

- Visibility of system status.
- Match between system and real world.
- User control and freedom.
- Consistency and standards.
- Error prevention.
- Recognition rather than recall.
- Flexibility and efficiency of use.
- Aesthetic and minimalist design.
- Help users recognize, diagnose, and recover from errors.
- Help and documentation.

Masalah yang ditemukan diberi severity rating:

- 0: bukan masalah usability.
- 1: cosmetic problem.
- 2: minor usability problem.
- 3: major usability problem.
- 4: usability catastrophe.

Contoh pada Domma:

- Onboarding membingungkan: bisa dikaitkan dengan recognition rather than recall, visibility, dan aesthetic/minimalist design.
- Tombol simpan kurang jelas: visibility of system status dan error prevention.
- Laporan sulit ditemukan: information architecture, recognition rather than recall, dan flexibility/efficiency.

## 30. Hubungan Praktikum Kelompok 8 dengan Design Thinking

Alur praktikum Kelompok 8 sangat cocok dipahami sebagai penerapan Design Thinking:

Empathize:

- user interview;
- empathy map;
- persona;
- memahami pemilik UMKM, fotokopi, warung sembako, dan distribusi sirup.

Define:

- merumuskan pain point;
- retrospective journey map;
- design challenge;
- kebutuhan utama seperti transaksi cepat, stok real-time, expired date, dan laporan otomatis.

Ideate:

- Crazy-8;
- voting dan clustering;
- memilih fitur prioritas.

Prototype:

- sketch;
- user flow;
- wireframe;
- high-fidelity prototype Figma.

Test:

- usability test plan;
- pengujian Maze;
- analisis success rate, misclick, drop-off, durasi, dan rating;
- rekomendasi iterasi desain.

Jadi jika ditanya "apa yang dipelajari selama praktikum?", jawabannya bukan hanya membuat tampilan aplikasi. Yang dipelajari adalah proses lengkap merancang UX berbasis pengguna: memahami masalah, menerjemahkan masalah menjadi kebutuhan, membuat solusi, memvisualisasikan solusi, menguji ke pengguna, lalu memperbaiki desain.

## 31. Studi Kasus Ringkas: Domma POS

Domma: POS adalah aplikasi kasir dan manajemen stok untuk UMKM, warung, toko retail, dan usaha kecil yang masih mengandalkan pencatatan manual.

Masalah utama:

- transaksi manual lambat;
- pembukuan rawan selisih;
- stok tidak real-time;
- barang kadaluarsa sulit dipantau;
- rekap keuangan memakan waktu;
- pemilik UMKM butuh sistem sederhana.

Solusi utama:

- dashboard penjualan dan stok;
- smart scanner barcode;
- input produk dan expired date;
- kasir dengan tunai dan QRIS;
- nota digital via WhatsApp;
- laporan keuangan;
- notifikasi stok kritis;
- gamifikasi streak untuk retensi.

Nilai UX:

- mengurangi beban kognitif;
- mempercepat transaksi;
- mengurangi human error;
- meningkatkan kontrol pemilik usaha;
- membuat usaha kecil terasa lebih profesional;
- memberi ketenangan karena data lebih rapi.

Hasil testing:

- fitur nota WhatsApp sangat mudah dipahami;
- onboarding perlu disederhanakan;
- Smart Scanner perlu instruksi lebih jelas;
- laporan perlu ditempatkan lebih mudah ditemukan;
- navigasi masih perlu diperbaiki.

## 32. Poin yang Kemungkinan Keluar di UAS

Materi yang sangat mungkin ditanyakan:

- perbedaan UX, UI, dan usability;
- alasan UX perlu dilakukan sejak awal;
- tahap Design Thinking;
- HCD dan UCD;
- UX strategy dan Product Vision Board;
- research plan dan user interview;
- persona;
- empathy map;
- mental model;
- user journey map;
- retrospective vs prospective journey map;
- How Might We;
- brainstorming dan Crazy-8;
- user story, user scenario, goal-task-action;
- user flow dan information architecture;
- wireframe, mockup, prototype;
- usability testing;
- formative vs summative evaluation;
- objective vs subjective metrics;
- quantitative vs qualitative data;
- SUS;
- UEQ;
- heuristic evaluation dan 10 heuristik Nielsen;
- severity rating;
- metrik Maze seperti success rate, misclick rate, drop-off, dan time on task.

## 33. Jawaban Cepat untuk UAS

UX adalah pengalaman pengguna secara menyeluruh saat memakai produk. UX mencakup riset, pemahaman masalah, alur, interaksi, evaluasi, dan kepuasan pengguna.

UI adalah tampilan antarmuka. UI bagian dari UX, tetapi UX lebih luas.

Usability adalah ukuran seberapa mudah, cepat, efisien, dan memuaskan sebuah sistem digunakan.

Design Thinking terdiri dari empathize, define, ideate, prototype, test.

Empathize bertujuan memahami pengguna melalui interview, observasi, dan riset.

Define bertujuan merumuskan masalah inti dari hasil riset.

Ideate bertujuan menghasilkan banyak alternatif solusi.

Prototype bertujuan membuat representasi solusi yang bisa diuji.

Test bertujuan mengevaluasi desain dengan pengguna nyata dan menemukan perbaikan.

Persona adalah profil representatif pengguna yang berisi karakteristik, kebutuhan, tujuan, motivasi, dan frustrasi.

Empathy map membantu memahami apa yang pengguna pikirkan, rasakan, lihat, dengar, katakan, lakukan, serta pain dan gain mereka.

User journey map menunjukkan tahapan pengalaman pengguna dari awal sampai tujuan tercapai, termasuk emosi dan pain point.

User flow menunjukkan jalur langkah pengguna di dalam sistem.

Wireframe adalah rancangan kerangka halaman. Mockup adalah tampilan visual lebih matang. Prototype adalah rancangan yang bisa disimulasikan atau diuji.

Usability testing adalah pengujian dengan pengguna nyata yang diminta menyelesaikan task tertentu sambil diamati.

SUS adalah kuesioner 10 item untuk mengukur persepsi usability dengan skor 0 sampai 100.

UEQ mengukur UX melalui attractiveness, perspicuity, efficiency, dependability, stimulation, dan novelty.

Heuristic evaluation adalah evaluasi oleh ahli menggunakan prinsip usability Nielsen.

Severity rating menunjukkan tingkat keparahan masalah usability dari 0 sampai 4.

## 34. Kesimpulan

Inti mata kuliah Perancangan Pengalaman Pengguna adalah merancang produk berdasarkan kebutuhan manusia, bukan sekadar membuat fitur atau tampilan. Prosesnya dimulai dari memahami pengguna, merumuskan masalah, membuat ide solusi, merancang alur dan antarmuka, membuat prototype, lalu menguji desain kepada pengguna.

Dalam proyek Kelompok 8, seluruh proses ini terlihat pada Domma: POS. Tim memulai dari riset UMKM, membuat persona dan empathy map, memetakan journey manual, merancang solusi digital, membuat user flow dan prototype Figma, lalu menguji prototype melalui Maze. Hasil akhirnya bukan hanya desain aplikasi kasir, tetapi pemahaman bahwa UX adalah proses iteratif untuk mengurangi beban pengguna, meningkatkan efisiensi, dan memastikan produk benar-benar bernilai bagi kehidupan pengguna.
