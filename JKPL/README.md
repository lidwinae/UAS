Bisa. Saya berhasil membaca teks dari semua file di folder ini: PDF, PPTX, dan DOCX. Catatan kecil: elemen yang berupa gambar/diagram murni di slide/PDF tidak selalu bisa diekstrak sebagai teks, tapi materi tertulisnya terbaca. Jawaban hijau di `KuisJKPL.docx` dan `Latihan UAS_JKPL.docx` juga berhasil saya deteksi.

**Inti Besar JKPL**
Jaminan Kualitas Perangkat Lunak itu bukan cuma “testing”. Tujuannya memastikan software memenuhi kebutuhan user, sesuai standar, minim defect, mudah dipelihara, aman, stabil, dan tetap layak dipakai dalam jangka panjang.

Kualitas bisa dilihat dari dua sisi:

| Perspektif | Maksud |
|---|---|
| User | software berguna, mudah dipakai, stabil, aman, sesuai harapan |
| Developer/organisasi | software sesuai requirement, standar, mudah dikembangkan, mudah dirawat |

**QA, QC, Testing**
| Istilah | Fokus | Sifat | Contoh |
|---|---|---|---|
| QA | proses pengembangan | preventif | SQA Plan, coding standard, checklist, audit proses |
| QC | produk/artefak | detektif/korektif | review requirement, design inspection, code review |
| Testing | eksekusi program | menemukan defect | unit test, integration test, system test, UAT |

Ingat rumus gampangnya: **Testing bagian dari QC, QC bagian dari QA**.  
QA memastikan prosesnya benar. QC mengecek hasilnya. Testing menjalankan program untuk mencari bug.

**QA Dalam SDLC**
Langkah QA yang sering muncul:

| Tahap | Maksud |
|---|---|
| Quality planning | menentukan standar kualitas proyek |
| Requirements review | mengecek requirement lengkap, jelas, konsisten |
| Design review | memastikan desain mendukung requirement |
| Implementation monitoring | memastikan developer mengikuti coding standard/prosedur |
| Testing | menemukan defect |
| Defect management | mencatat bug dan memastikan diperbaiki |
| Quality evaluation | mengevaluasi kualitas hasil/proses |

Di Waterfall, QA/QC/testing cenderung per fase. Risiko besar: masalah baru kelihatan di akhir.  
Di Agile, QA dilakukan terus selama sprint: Definition of Done, acceptance criteria, automated regression, review tiap increment.

**McCall’s Quality Model**
McCall membagi kualitas jadi 3 kategori besar:

| Kategori | Faktor | Arti gampang |
|---|---|---|
| Product Operation | Correctness | sistem melakukan fungsi sesuai requirement |
| Product Operation | Reliability | sistem stabil, jarang gagal |
| Product Operation | Efficiency | hemat resource dan cepat |
| Product Operation | Integrity | keamanan/akses data |
| Product Operation | Usability | mudah dipakai dan dipahami |
| Product Revision | Maintainability | mudah diperbaiki |
| Product Revision | Flexibility | mudah diubah/ditambah fitur |
| Product Revision | Testability | mudah diuji |
| Product Transition | Portability | mudah dipindah ke platform/lingkungan lain |
| Product Transition | Reusability | komponen bisa dipakai ulang |
| Product Transition | Interoperability | bisa terhubung/bertukar data dengan sistem lain |

Bedakan **quality factor** dan **quality criteria**:
Quality factor adalah atribut besar yang terasa langsung, misalnya usability, reliability, correctness.  
Quality criteria adalah kriteria pendukung yang lebih teknis/terukur, misalnya modularity, operability, response time, error handling.

**Istilah Yang Kamu Tanya**
**Correctness**: apakah output/fungsi sistem sesuai requirement dan kebutuhan user.  
Contoh: pencarian Tokopedia harus menampilkan produk relevan sesuai keyword/filter. Kalau filter bintang 5 malah muncul bintang 2, itu correctness bermasalah.

**Maintainability**: seberapa mudah sistem diperbaiki saat ada bug atau perubahan.  
Contoh: kalau downtime maintenance molor terus, sulit recovery, atau kode susah dipahami, maintainability rendah.

**Usability**: seberapa mudah, nyaman, dan masuk akal sistem dipakai user.  
Contoh: form hilang saat salah klik menu, tombol tumpang tindih, user bingung, layout kacau.

**Reliability**: kemampuan sistem tetap beroperasi stabil dalam kondisi tertentu.  
Subcontoh: availability, fault tolerance, recoverability.

**Efficiency / Performance Efficiency**: performa dibanding resource.  
Contoh: RAM 912 MB, HP panas 45°C, response time 45 detik, CPU boros.

**Interoperability**: kemampuan sistem terhubung dengan sistem lain.  
Contoh: payment gateway KAI gagal sinkron dengan core ticketing.

**Portability**: kemampuan software dipindahkan ke OS/device/platform baru.  
Contoh: aplikasi dari Windows dipindah ke Linux dengan effort kecil.

**ISO/IEC 25010 Yang Sering Keluar**
| Karakteristik | Arti |
|---|---|
| Functional Suitability | fungsi sesuai kebutuhan |
| Performance Efficiency | cepat dan hemat resource |
| Compatibility | bisa hidup berdampingan/berinteraksi dengan sistem lain |
| Usability | mudah digunakan |
| Reliability | stabil, tersedia, bisa pulih |
| Security | aman dari akses tidak sah |
| Maintainability | mudah dianalisis, diubah, diuji |
| Portability | mudah dipasang/adaptasi/pindah lingkungan |

Sub-karakteristik penting:
Availability = layanan tersedia saat dibutuhkan.  
Fault tolerance = tetap berjalan walau ada fault.  
Recoverability = bisa pulih setelah gagal.  
Resource utilization = penggunaan RAM/CPU/storage/network.  
Time behaviour = response time/processing time.  
Co-existence = berbagi resource dengan software lain tanpa saling mengganggu.  
Interoperability = bertukar informasi dengan sistem lain.  
Operability = mudah dioperasikan user.  
UI aesthetics = tampilan rapi/menyenangkan.  
Adaptability = menyesuaikan diri dengan lingkungan/platform berbeda.  
Modularity = perubahan satu komponen tidak merusak komponen lain.

**Komponen SQA Menurut Galin**
| Komponen | Maksud |
|---|---|
| Pre-project components | sebelum proyek: contract review, development & quality plan |
| Project life cycle components | saat pengembangan: review, expert opinion, testing, maintenance |
| Infrastructure error prevention | prosedur, work instruction, template, checklist, training |
| Software quality management | project control, metrics, quality cost |
| Standards/certification/assessment | ISO, CMM/CMMI, SPICE |
| Human components | management, SQA unit, tester, SQA committee/forum/trustee |

Template dan checklist termasuk infrastructure error prevention karena menstandarkan kerja, mengurangi human error, dan memastikan item penting tidak terlewat.

**Quality Management**
Quality Management mencakup:
Quality planning, quality assurance, quality control, quality improvement.

Metrics:
Process metrics = menilai proses, misalnya defect rate per sprint, schedule variance.  
Product metrics = menilai produk, misalnya response time, fault density, RAM usage.  
Internal metrics = tanpa menjalankan program, misalnya static analysis, complexity.  
External metrics = saat runtime, misalnya load test, usability test, monitoring.

Software quality cost:
Prevention cost = biaya mencegah bug, misalnya training, coding standard.  
Appraisal cost = biaya menemukan bug, misalnya testing, review.  
Internal failure cost = bug ditemukan sebelum rilis.  
External failure cost = bug ditemukan setelah rilis, biasanya paling mahal.

**CMM/CMMI**
| Level | Ciri |
|---|---|
| 1 Initial | kacau, ad hoc, tergantung individu |
| 2 Repeatable | proyek mulai terkelola, bisa mengulang sukses proyek serupa |
| 3 Defined | proses standar organisasi sudah jelas |
| 4 Managed | proses diukur kuantitatif/statistik |
| 5 Optimizing | continuous improvement dan inovasi |

**Cek Jawaban Kamu**
`KuisJKPL.docx`: jawaban hijau kamu terlihat benar semua.

`Latihan UAS_JKPL.docx`: secara pilihan jawaban, saya tidak menemukan yang jelas salah. Ada beberapa yang sebaiknya kamu pahami nuansanya:
1. Soal responsive layout BIMO: jawaban kamu mengarah benar, tapi secara ISO 25010, **Adaptability** biasanya berada di **Portability**, sedangkan **UI Aesthetics** berada di **Usability**. Kalau opsi ujian mencampur “Adaptability dan UI Aesthetics di bawah Usability”, maksud dosen kemungkinan tetap ke masalah tampilan responsif.
2. “Functional Relevance” pada Tokopedia: istilah ISO 25010 yang lebih umum adalah **Functional appropriateness/correctness** dalam Functional Suitability. Tapi pilihan kamu tetap paling tepat karena intinya hasil pencarian tidak relevan = correctness/functional suitability gagal.
3. State persistence form hilang: paling kuat adalah **Usability/Operability**, dan bisa diperluas ke **Reliability/Recoverability** kalau dibahas soal pemulihan data.

Cara jawab UAS yang aman: sebutkan **masalahnya**, petakan ke **model kualitas**, lalu beri **alasan + rekomendasi testing/perbaikan**. Contoh: “Form hilang saat pindah menu menunjukkan lemahnya state persistence. Ini menurunkan Usability terutama Operability, dan dapat diperbaiki dengan local storage, autosave, unsaved changes warning, serta usability/recovery testing.”