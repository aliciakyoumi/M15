# RINGKASAN KRITIKAL & PANDUAN DOMAIN KNOWLEDGE
## Proyek Machine Learning: Anomaly Detection — Immersion Aluminium Holding Furnace 1120 kg/ch
**Sumber:** Manual Book PT. Tempsens Asia Jaya untuk PT. Astra Honda Motor (Project No. 4500657690 & 4500657691)

---

## A. RINGKASAN EKSEKUTIF & SPESIFIKASI TEKNIS MESIN HPDC HOLDING

### A.0. Konteks Ilmu Material: Diagram Fasa Al-Si & Titik Eutektik

Sebelum membahas spesifikasi mesin, penting untuk memahami **mengapa** parameter operasional (khususnya setpoint 650°C) dipilih sedemikian rupa. Pemilihan ini bukan angka arbitrer, melainkan turunan langsung dari perilaku termodinamika paduan **Aluminium-Silikon (Al-Si)** yang digunakan sebagai bahan baku HPDC di PT. Astra Honda Motor.

**a) Apa itu Diagram Fasa Al-Si?**
Diagram fasa Al-Si adalah peta yang menggambarkan fase (padat, cair, atau campuran padat-cair) suatu paduan Al-Si pada berbagai kombinasi **komposisi silikon (% Si)** dan **temperatur**. Diagram ini krusial dalam proses casting karena menentukan pada suhu berapa logam benar-benar 100% cair (di atas garis **liquidus**) versus mulai membeku sebagian (di bawah garis liquidus, menuju garis **solidus**).

**b) Titik Eutektik Al-Si**
Titik eutektik adalah komposisi khusus di mana campuran Al-Si membeku/mencair pada **satu temperatur tunggal** (bukan pada rentang suhu), tanpa melalui fase "pasty"/lumpur (campuran padat-cair) yang lebar. Karakteristik titik eutektik Al-Si:

| Parameter Titik Eutektik | Nilai |
|---|---|
| Komposisi Silikon (Si) | **~11 – 12,5 %** |
| Temperatur Eutektik | **~577°C** |
| Perilaku pembekuan | Membeku serentak (isotermal), bukan bertahap |
| Fase di bawah titik ini | Padat + campuran padat-cair (mulai terbentuk sludge/dross bila didinginkan tidak merata) |

**c) Representasi Sederhana Diagram Fasa (Deskripsi Poin per Rentang Suhu)**

| Rentang Suhu | Kondisi Logam (untuk paduan Al-Si tipikal casting, ~7–12% Si) | Implikasi Proses |
|---|---|---|
| **> 620°C** (jauh di atas liquidus) | 100% cair, fluiditas tinggi, homogen | Ideal untuk holding & transfer ke shot sleeve HPDC |
| **~600 – 620°C** (mendekati liquidus) | Masih cair, namun mulai mendekati ambang pembentukan fase padat awal | Zona waspada — mendekati risiko pembekuan dini di titik-titik dingin (nozzle, dinding furnace) |
| **~577°C (titik eutektik)** | Transisi cair → padat terjadi cepat/serentak | Batas kritis: di bawah titik ini logam **tidak lagi dapat dianggap cair sepenuhnya** |
| **< 577°C** | Mulai terbentuk fase padat (primary Al / Si), campuran menjadi kental ("sludging") | Berisiko menyumbat saluran, cacat casting (cold shut/misrun), kerusakan pompa/nozzle |

**d) Hubungan dengan Setpoint Operasional Mesin (650°C)**
Merujuk pada spesifikasi mesin di **A.2** (setpoint 650°C ± 10°C, rentang kerja 640–660°C), nilai ini sengaja diatur **jauh di atas titik eutektik ~577°C** dengan margin keamanan (*superheat margin*) sekitar **60–80°C**. Alasan teknisnya:

- **Mencegah pembekuan parsial (partial solidification):** Menjaga logam tetap di zona "100% cair, fluiditas tinggi" agar tidak terbentuk kristal padat prematur yang dapat menyumbat *immersion heater*, *protection tube*, atau saluran menuju mesin HPDC.
- **Mencegah sludging:** Superheat margin yang cukup mengurangi risiko terbentuknya endapan padat-cair (sludge/dross) di dasar furnace yang dapat mengganggu sirkulasi dan menurunkan kualitas logam tuang.
- **Toleransi terhadap kehilangan panas lokal:** Karena proses holding melibatkan pembukaan cover untuk charging dan pengambilan logam secara berkala, margin di atas titik eutektik memberi "ruang aman" agar fluktuasi suhu sesaat (misalnya akibat charging logam dingin) tidak langsung mendorong sebagian logam ke bawah titik eutektik.
- **Konteks langsung untuk deteksi anomali:** Inilah mengapa ambang **Metal Temperature Low (EV3, <640°C)** pada C.3 tetap berada **jauh di atas** titik eutektik 577°C — sistem dirancang untuk memicu alarm **jauh sebelum** logam benar-benar mendekati risiko pembekuan aktual, memberi waktu intervensi. Skenario **#4 Thermal Lag** dan **#6 Metal Temperature Low** pada Bagian B pada dasarnya adalah early-warning terhadap potensi drift menuju kondisi mendekati titik eutektik ini.

### A.1. Deskripsi Umum
Mesin ini adalah **Immersion Aluminium Holding Furnace** yang berfungsi untuk **holding (menjaga) molten metal (aluminium cair)** sebelum digunakan dalam proses HPDC/casting di PT. Astra Honda Motor. Mesin bekerja dengan cara mencelupkan (immersion) elemen pemanas ke dalam bak logam cair, dengan pemanas dilindungi oleh tabung pelindung (protection tube) agar tidak kontak langsung dengan logam cair.

### A.2. Spesifikasi Teknis Utama

| Parameter | Nilai |
|---|---|
| Model Mesin | Immersion Aluminium Holding Furnace |
| Fungsi | Holding molten metal |
| **Temperatur Kerja (Setpoint Operasional)** | **650°C ± 10°C** (rentang kerja normal: **640°C – 660°C**) |
| Holding Capacity | 1120 kg/ch (maksimum) |
| Dimensi Furnace | 2415 mm x 1250 mm x 1030 mm |
| Material Bodi | Mild Steel |
| Berat Furnace (kosong) | 2.500 kg |
| Tipe Pemanas | Immersion Heater with Protection Tube |
| Kapasitas Pemanas | **2 x 8 kW = 16 kW (13.760 kcal/h)** — 2 unit heater independen (Heater #1 & Heater #2) |
| Material Protection Tube | Silicon Nitride Tube (revisi awal) / Silicon Carbide Tube (revisi update) |
| Suplai Listrik Heater | 60 VAC, 1 Phase (melalui step-down transformer TR200/TR300, 10 kVA, dari AC 400/380V ke AC 60V, dikontrol SCR/Thyristor) |
| Suplai Daya Utama Panel | AC 380 V, 3 Phase, 50 Hz (MCCB-M 3P 100A) |
| Fluktuasi Voltase yang Ditoleransi | ± 10% |
| Fluktuasi Frekuensi yang Ditoleransi | ± 5% |
| Tegangan Instrumen Panel | AC 220V/200 Volt; DC 24V untuk sirkuit kontrol |
| Arus Panel | 75 Ampere |

### A.3. Setpoint Temperature Controller (Referensi Kritikal untuk Rule-Based Labeling)

| Controller | Symbol | Setting (°C) | Makna |
|---|---|---|---|
| **Metal Temperature Controller** | COM | **660** | Temperatur normal operasi harian |
| | EV1 | **680** | Ambang **Molten Metal Temperature OVERHEAT** |
| | EV3 | **640** | Ambang **Molten Metal Temperature LOW** |
| **Safety Heater #1 Temperature Controller** | COM | 950 | Temperatur normal operasi heater |
| | EV1 | 1000 | Ambang **Safety Heater Overheat** (proteksi elemen heater, bukan molten metal) |
| | EV3 | 900 | Ambang temperatur heater terlalu rendah relatif terhadap molten metal (indikasi heater tidak bekerja optimal) |
| **Safety Heater #2 Temperature Controller** | COM/EV1/EV3 | 950 / 1000 / 900 | Sama seperti Heater #1 (redundant safety control per heater) |

> **Catatan penting untuk labeling:** Ada **dua layer sensor temperatur** — (1) `TC100` = thermocouple **molten metal** (Metal Temperature Controller, acuan `molten_temp`), dan (2) `TC101`/`TC102` = thermocouple **badan/elemen heater** (Safety Heater Temperature Controller #1 dan #2, acuan proksi untuk kondisi fisik `heater1`/`heater2`). Perbedaan drastis antar dua layer ini (heater sangat panas tapi molten metal tidak naik, atau sebaliknya) adalah sinyal anomali kuat.

### A.4. Indikator / Alarm Elektrikal & Mekanikal Bawaan Mesin

| No | Nama Alarm/Lampu Indikator | Kondisi Pemicu |
|---|---|---|
| 1 | **SCR 200 Heater#1 Abnormal** | SCR (thyristor power regulator) Heater #1 mengalami gangguan |
| 2 | **SCR 300 Heater#2 Abnormal** | SCR (thyristor power regulator) Heater #2 mengalami gangguan |
| 3 | **Melt Leak Detect** | Tube Immersion Heater pecah/retak dan molten metal masuk ke dalam Immersion Heater |
| 4 | **Emergency Stop** | Tombol Emergency Stop aktif |
| 5 | **Metal Temperature Overheat** | `molten_temp` > 680°C |
| 6 | **Metal Temperature Low** | `molten_temp` < 640°C |
| 7 | **Safety Heater Temp Overheat** | Temperatur fisik elemen heater > 1000°C (proteksi kegagalan tube/elemen, independen dari suhu molten metal) |
| 8 | **Metal Level High** | Level molten metal menyentuh sensor level (High) |
| 9 | **Metal Level Over High** | Level molten metal menyentuh sensor level (High-High) — indikasi overfill/overcapacity |
| 10 | Spare Lamp | Cadangan |
| 11 | **Heater #1/#2 Abnormal** (lampu terpisah dari SCR) | Immersion Heater #1 atau #2 tidak berfungsi (putus koneksi/overload/overload voltage) |

### A.5. Peralatan Kelistrikan Kunci (Konteks Sensor)
- **Power Meter** (Mitsubishi ME96SSR) → sumber data `voltage_avr`, `current_avr`, `power_total` (di sisi suplai utama 3 phase).
- **Ampere Meter per Heater** (Heater #1 Ampere Meter & Heater #2 Ampere Meter, via CT 200/5A) → sumber `current_avr` per-heater bila granularitas per heater tersedia.
- **SCR/Thyristor Power Regulator (W5 Series)** → mengatur daya ke tiap Immersion Heater secara phase-angle/zero-crossing control; kegagalan SCR (short/open) adalah salah satu root cause utama anomali arus & daya.
- **Temperature Controller AZBIL** (Metal: `TIC100`; Safety Heater #1: `TIA101`; Safety Heater #2: `TIA102`) → mengatur ON/OFF pemanasan berdasarkan setpoint di atas.

---

## B. PETA INDIKATOR ANOMALI & ROOT CAUSE ANALYSIS (SEBAB–AKIBAT)

### B.0. Sistem Klasifikasi Anomali Berjenjang (Severity Level)

Untuk kebutuhan pemodelan, target klasifikasi utama tetap **biner** (`Normal` vs `Anomali`) sebagaimana didefinisikan pada Bagian D. Namun, untuk keperluan **prioritisasi maintenance, interpretasi hasil oleh tim lapangan, dan metadata root-cause**, setiap baris/skenario anomali diberi **sub-label Severity Level** berjenjang sebagai berikut:

| Severity Level | Definisi | Karakteristik Umum | Tindakan yang Diharapkan |
|---|---|---|---|
| 🟢 **NORMAL** | Kondisi operasional standar, termasuk mesin mati secara wajar (open circuit by design) | Semua parameter dalam rentang normal (lihat C.3); atau kondisi off-state resistansi tinggi (Skenario B.#2) | Tidak ada tindakan — baseline |
| 🟡 **WARNING** | Indikasi awal degradasi atau masalah operasional yang **belum** membahayakan proses/keselamatan secara langsung | Thermal lag ringan tahap awal, suhu mendekati (namun belum melewati) ambang batas, level metal mendekati High | Monitoring lebih ketat, jadwalkan inspeksi/maintenance preventif |
| 🟠 **CRITICAL** | Anomali serius yang membutuhkan intervensi segera, berpotensi merusak peralatan atau menghentikan produksi bila dibiarkan | Uncontrolled heating, overheat/low temp berkelanjutan, kapasitas pemanas tidak seimbang (satu heater gagal) | Intervensi operator/teknisi segera, evaluasi root cause, pertimbangkan stop terjadwal |
| 🔴 **FATAL / EMERGENCY** | Bahaya keselamatan kerja dan/atau risiko kerusakan fisik tingkat tinggi (kebakaran, ledakan listrik, kontak logam cair-listrik) | Short circuit akibat kegagalan protection tube, Melt Leak Detect aktif, lonjakan arus ekstrem | **Emergency stop segera**, isolasi kelistrikan, evakuasi area, prosedur K3 tingkat tinggi |

> **Catatan integrasi dengan pemodelan:** Kolom **Severity Level** ditambahkan sebagai **metadata/fitur kategorikal turunan** pada setiap baris yang di-label anomali oleh Layer 1 rule-based (Bagian D.1), bukan sebagai target klasifikasi utama model. Ini konsisten dengan rekomendasi D.3 untuk menyimpan *rule yang men-trigger label* sebagai metadata — Severity Level memperkaya metadata tersebut agar tim maintenance dapat memprioritaskan penanganan (mis. FATAL/EMERGENCY selalu diprioritaskan di atas WARNING meski model ML memberi confidence score serupa).

> Tabel matriks berikut menggabungkan **5 aturan logika ahli** (dari brief proyek) dengan **alarm bawaan manual book**, lengkap dengan pola sensor, root cause mekanikal/elektrikal, dampak produksi, dan **Severity Level**.

| # | Jenis / Skenario Anomali | Severity | Pola Parameter Sensor (interaksi `molten_temp`, `heater1/2`, `current_avr`, `power_total`, R) | Akar Penyebab (Root Cause) | Dampak pada Proses Produksi |
|---|---|---|---|---|---|
| **1** | **Uncontrolled Heating** — suhu naik padahal heater OFF | 🟠 CRITICAL | `molten_temp` **naik** sementara `heater1=0` **dan** `heater2=0`. `power_total` seharusnya ≈0 tapi suhu tetap meningkat. | (a) **SCR/Thyristor gagal short-circuit** (tetap mengalirkan daya walau perintah OFF — kegagalan klasik thyristor "fail-on"); (b) Thermocouple/controller **drift atau fault** sehingga pembacaan naik palsu (bukan mesin sebenarnya memanas); (c) Sumber panas eksternal tidak terkontrol (mis. sisa panas dari charging molten metal baru dituang). | Risiko **overheat tanpa proteksi aktif** (karena sistem menganggap heater mati), potensi kerusakan refractory, dan **false confidence** operator bahwa mesin aman. |
| **2** | **Normal Off-State (High Resistance)** — kondisi mati wajar | 🟢 NORMAL | Resistance R **sangat tinggi** (mendekati Megaohm), `current_avr` ≈ 0, `power_total` = 0, `heater1`/`heater2` = OFF. | Kondisi desain normal: rangkaian terbuka saat heater tidak diaktifkan → hambatan tak-hingga secara elektris (open circuit). | **Tidak ada dampak** — ini adalah baseline normal, bukan anomali. Penting untuk *tidak* memberi label anomali pada kondisi ini (lihat Bagian C untuk aturan retensi baris partial-zero). |
| **3** | **Short Circuit / Heating Element Failure** | 🔴 FATAL/EMERGENCY | Resistance R **sangat rendah**, `power_total` **stagnan/tidak berubah** (datar), namun `current_avr` **melonjak sangat besar** (spike). | (a) **Tube heater pecah** dan molten metal masuk ke dalam elemen Immersion Heater (memicu *Melt Leak Detect*), menyebabkan hubungan pendek elemen dengan bodi/logam cair; (b) Isolasi elemen heater rusak/aus; (c) SCR mengalami *short* pada sisi output. | Berpotensi **trip breaker/fuse (high-speed fuse burn-down)**, **kebakaran/ledakan listrik**, kerusakan permanen elemen heater, dan **downtime tak terjadwal**. Wajib dikaitkan dengan alarm **SCR Abnormal** & **Melt Leak Detect**. Lihat elaborasi mekanisme lengkap di **B.5**. |
| **4** | **Thermal Lag / Heating Failure** — heater ON tapi suhu tetap turun | 🟡 WARNING (naik ke 🟠 CRITICAL jika berlanjut hingga memicu #6) | Dalam window 1 jam: `molten_temp` **turun ≥10°C**, heater **berubah status ke ON**, namun setelah ON `molten_temp` **tetap turun terus** (sistem gagal mengembalikan suhu / tidak ada respon kenaikan). | (a) Elemen heater **rusak/aus namun masih terdeteksi ON secara switch** (tidak benar-benar menghantarkan panas — early sign sebelum alarm Heater Abnormal muncul); (b) **Tube heater retak/leakage** sehingga transfer panas ke molten metal tidak efisien; (c) **Kapasitas pemanas (16 kW) tidak mencukupi** dibanding laju kehilangan panas (charging molten metal dingin dalam jumlah besar, pintu/cover terbuka lama, kerusakan lapisan **refractory**); (d) SCR kehilangan sebagian kemampuan mengatur daya (partial failure). | Produk casting berpotensi cacat (**cold shut/misrun** akibat suhu tuang tidak tercapai — lihat konteks titik eutektik di **A.0**), memicu alarm **Metal Temperature Low** (<640°C) jika berlanjut, serta indikasi dini kebutuhan **maintenance preventif** pada heater/refractory. |
| **5** | **Metal Temperature Overheat** (alarm bawaan) | 🟠 CRITICAL | `molten_temp` > 680°C (EV1 Metal Temperature Controller) secara berkelanjutan. | Thermocouple bermasalah (rank 2 pada manual troubleshooting) atau setting holding tidak sesuai kebutuhan proses (rank 1). | Degradasi kualitas logam, risiko keselamatan (overheat/ledakan), pemicu **Safety Heater Overheat** lanjutan jika dibiarkan. |
| **6** | **Metal Temperature Low** (alarm bawaan) | 🟠 CRITICAL (didahului 🟡 WARNING saat mendekati 640°C) | `molten_temp` < 640°C (EV3 Metal Temperature Controller) secara berkelanjutan. | Thermocouple bermasalah, atau kegagalan pemanasan (berkaitan erat dengan Skenario #4 Thermal Lag). | Cacat casting, proses charging/holding terhambat. Nilai 640°C masih memberi margin besar terhadap titik eutektik ~577°C (lihat **A.0**), namun tren turun terus-menerus wajib diwaspadai. |
| **7** | **Heater Abnormal (#1 atau #2)** (alarm bawaan) | 🟠 CRITICAL | Salah satu `heater1`/`heater2` menunjukkan status gagal aktif meski di-switch ON; `current_avr` per-heater terkait tidak sesuai ekspektasi. | Rank 1: koneksi heater putus. Rank 2: overload capacity (beban melebihi spesifikasi 8kW/unit). Rank 3: overload voltage (fluktuasi >±10%). | Kapasitas pemanasan total turun 50% (hanya 1 heater aktif) — **kapasitas pemanas tidak seimbang**, mempercepat risiko Skenario #4 (Thermal Lag). |
| **8** | **Melt Leak Detect** (alarm bawaan) | 🔴 FATAL/EMERGENCY | Alarm aktif bersamaan dengan pola Skenario #3 (short circuit signature) pada heater terkait. | Tube protection heater (Silicon Nitride/Silicon Carbide) pecah, molten metal merembes masuk ke Immersion Heater. | **Bahaya tinggi** — kontak logam cair dengan elemen listrik; wajib emergency stop & isolasi kelistrikan segera. Lihat elaborasi mekanisme lengkap di **B.5**. |
| **9** | **Metal Level High / Over High** (alarm bawaan) | 🟡 WARNING | Sensor level (LVS1/LVS2) aktif; tidak berkorelasi langsung dengan `molten_temp`/heater tapi relevan sebagai *confounder* — charging saat level sudah tinggi dapat memicu fluktuasi suhu palsu akibat pengadukan logam baru. | Proses charging melebihi kapasitas 1120 kg/ch atau sensor level macet/kotor. | Risiko tumpah (overflow), kerusakan lounder, dan **noise** pada sinyal `molten_temp` selama beberapa menit pasca-charging (perlu di-*flag*, bukan otomatis dianggap anomali heater). |
| **10** | **Safety Heater Temp Overheat** (alarm bawaan, `TC101`/`TC102`) | 🟡 WARNING (naik ke 🟠 CRITICAL jika terus meningkat mendekati kegagalan tube) | Temperatur badan elemen heater > 1000°C **meski** `molten_temp` normal (<680°C). | Local hotspot pada elemen akibat pengecilan luas kontak dengan molten metal (level rendah/heater sebagian terekspos udara), awal indikasi kegagalan tube. | Prekursor dini untuk Skenario #3/#4; sangat berguna sebagai **leading indicator** anomali sebelum molten_temp itu sendiri terpengaruh. |
| **11** | **Anomali Multivariat — Thermal Lag bersamaan Voltage Drop/Fluktuasi** | 🟠 CRITICAL (naik dari 🟡 WARNING jika hanya salah satu gejala muncul sendiri) | Kombinasi **simultan**: pola Thermal Lag Skenario #4 (`delta_temp_1h ≤ -10°C` meski heater ON) **bersamaan** dengan `voltage_avr` yang turun/berfluktuasi **di luar toleransi ±10%** (referensi A.2) pada window waktu yang sama. Secara univariat, masing-masing sinyal (delta_temp saja, atau voltage saja) bisa tampak "hampir normal"/borderline; namun **interaksi keduanya** memperkuat sinyal anomali yang tidak tertangkap jika fitur dievaluasi terpisah. | Voltage drop pada suplai utama (AC 380V 3 phase) menyebabkan **daya aktual yang dikirim SCR ke heater ikut turun** (daya ∝ V²), sehingga heater berstatus ON namun **tidak mampu mensuplai panas sesuai kapasitas nominal 8kW/unit** — menghasilkan gejala Thermal Lag yang **sebenarnya bukan kegagalan elemen heater**, melainkan **starvation daya akibat gangguan suplai listrik eksternal** (mis. beban pabrik yang tinggi bersamaan, gangguan grid PLN, atau ketidakseimbangan fasa). Root cause ini penting dibedakan dari Skenario #4 murni (kegagalan elemen/tube) karena **penanganannya berbeda** (perbaikan kualitas suplai daya vs penggantian komponen heater). | Jika tidak dibedakan dari Thermal Lag murni, tim maintenance berisiko **salah diagnosis** (mengganti elemen heater yang sebenarnya masih baik) sementara akar masalah sebenarnya ada pada sisi kelistrikan pabrik/panel. Berlanjutnya kondisi ini tetap berisiko mendorong `molten_temp` mendekati ambang Low (<640°C, Skenario #6) dan cacat casting (lihat konteks titik eutektik di **A.0**). |

### B.5. Elaborasi Detail: Skenario Short Circuit (FATAL/EMERGENCY) sebagai Rantai Kegagalan

Skenario #3 (Short Circuit) dan #8 (Melt Leak Detect) pada dasarnya adalah **satu rantai kegagalan fisik-elektrikal yang sama**, dilihat dari dua sudut sensor berbeda. Karena ini adalah skenario dengan severity tertinggi (🔴 FATAL/EMERGENCY), mekanismenya perlu dipahami secara berurutan:

**Tahap 1 — Kegagalan Mekanis Protection Tube**
Elemen *immersion heater* dilindungi oleh **protection tube** (Silicon Nitride pada revisi awal desain, Silicon Carbide pada revisi update — lihat A.2). Tube ini berfungsi sebagai penghalang fisik antara elemen pemanas listrik dan molten metal aluminium di sekitarnya. Seiring waktu, tube dapat **retak atau pecah** akibat: kelelahan termal (thermal fatigue) dari siklus panas berulang, korosi kimiawi oleh aluminium cair, benturan mekanis saat charging/skimming, atau cacat material bawaan.

**Tahap 2 — Molten Metal Merembes (Melt Leak)**
Begitu tube pecah, **molten metal aluminium cair merembes masuk** ke rongga tempat elemen heater berada. Karena aluminium cair bersifat konduktif secara elektrik, rembesan ini menciptakan **jalur hubung singkat (short circuit path)** antara elemen heater bertegangan dan bodi/ground mesin. Inilah yang memicu alarm bawaan **Melt Leak Detect** (indikator #3 pada tabel A.4) — sensor ini dirancang khusus untuk mendeteksi kontak logam cair dengan rongga elemen heater.

**Tahap 3 — Signature Elektrikal: Resistance Turun, Current Spike**
Secara elektrikal, jalur short circuit ini muncul sebagai:
- **Resistance (R) turun drastis** mendekati nol — karena `R = power_total / (current_avr)²` (lihat C.2), jalur short menciptakan hambatan yang jauh lebih rendah dibanding elemen heater normal.
- **`current_avr` melonjak ekstrem (spike)** — hukum Ohm menyebabkan arus naik tajam saat resistansi turun drastis pada tegangan suplai yang relatif tetap (60 VAC ke heater, referensi A.2).
- **`power_total` cenderung stagnan/datar**, karena SCR/breaker mulai membatasi atau sistem proteksi mulai merespons, berbeda dengan kondisi pemanasan normal di mana power naik seiring current.

**Tahap 4 — Eskalasi Kelistrikan Lanjutan**
Lonjakan arus ekstrem ini berisiko memicu: **SCR/Thyristor Abnormal** (indikator #1/#2 pada A.4) karena beban di luar spesifikasi desain SCR; **trip pada high-speed fuse atau breaker** (MCCB 3P 100A pada panel utama, referensi A.2) sebagai proteksi terakhir; dan dalam kasus terburuk, **kegagalan katastropik** berupa percikan api/busur listrik (arcing) yang berkontak dengan uap logam atau material mudah terbakar di sekitar furnace.

**Tahap 5 — Konsekuensi Keselamatan & Operasional**
Kombinasi *molten metal* bertemu elemen bertegangan listrik adalah salah satu bahaya K3 paling serius di lingkungan foundry/casting — berpotensi **ledakan uap logam (metal-water/metal-moisture explosion)** bila ada kontaminasi kelembapan, **kebakaran listrik**, serta cedera serius pada personel di sekitar mesin. Oleh karena itu, kombinasi alarm **Melt Leak Detect + current spike + SCR Abnormal** harus diperlakukan sebagai **interlock wajib untuk emergency stop otomatis**, bukan sekadar flag anomali yang menunggu review manual.

**Implikasi untuk Rule-Based Labeling & Model:** Kombinasi ketiga sinyal ini (R sangat rendah + current spike + alarm Melt Leak Detect aktif, jika tersedia dalam log) sebaiknya diberi **prioritas tertinggi dalam Layer 1 rule-based** (Bagian D.1) — baris data dengan pola ini harus selalu ter-label anomali dengan Severity FATAL/EMERGENCY terlepas dari output model ML manapun, karena false negative pada skenario ini memiliki konsekuensi keselamatan yang tidak dapat ditoleransi.

---

## C. PIPELINE DATA PREPROCESSING & FEATURE ENGINEERING

### C.1. Rangkuman Instruksi Pembersihan Data (Wajib, Berurutan)

| Langkah | Aturan | Alasan |
|---|---|---|
| 1. Slicing Periode | **Drop seluruh data Januari & Februari 2025.** Analisis hanya periode **Maret – Agustus 2025**. | Periode Jan–Feb 2025 mengandung banyak error/noise sensor yang tidak representatif. |
| 2. Full-Zero Row | **Drop** baris jika **seluruh fitur** (`molten_temp`, `heater1`, `heater2`, `voltage_avr`, `current_avr`, `power_total`) bernilai 0 secara berderet. | Indikasi sensor/mesin mati total (bukan data operasional valid) — sejalan dengan periode "Hentikan Operasi" pada manual (Bab 6.2) di mana seluruh sistem OFF. |
| 3. Partial-Zero Row | **JANGAN DROP** jika hanya sebagian fitur bernilai 0 (mis. `power_total`=0 tapi `molten_temp` masih terbaca). | Kondisi ini justru **kunci identifikasi anomali** — lihat Bagian B (Skenario #1 dan #2). |

### C.2. Variabel Turunan (Feature Engineering)

| Fitur Turunan | Formula/Definisi | Kegunaan |
|---|---|---|
| **Resistance (R)** | `R = power_total / (current_avr)^2` | Membedakan Normal Off-State (R besar/megaohm) vs Short Circuit (R kecil) — lihat B.#2 dan B.#3. Hindari divide-by-zero: saat `current_avr = 0`, definisikan R = `NaN`/`inf` lalu tangani terpisah sebagai kategori "Off/Zero-Current" (bukan dianggap error numerik). |
| **Delta Temp per Jam** (`delta_temp_1h`) | `molten_temp(t) - molten_temp(t-1h)` (rolling window 1 jam) | Basis deteksi **Thermal Lag** (Skenario #4): flag jika `delta_temp_1h ≤ -10°C` DAN heater status = ON pada window tersebut, DAN tren tetap turun setelah heater ON. |
| **Heater Status Composite** | `heater_active = 1` jika `heater1 > 0` **atau** `heater2 > 0`; `heater_both_off = 1` jika keduanya 0 | Basis deteksi Uncontrolled Heating (Skenario #1). |
| **Delta Temp saat Heater OFF** | `molten_temp(t) - molten_temp(t-1)` dihitung khusus pada baris `heater_both_off = 1` | Mendeteksi kenaikan suhu abnormal saat heater seharusnya tidak memanaskan. |
| **Rolling Std / Rate-of-Change `current_avr`** | Standar deviasi atau selisih `current_avr` pada window pendek (mis. 5–15 menit) | Mendeteksi lonjakan arus mendadak (spike signature Skenario #3), lebih sensitif dibanding nilai absolut. |
| **R_category (label kategori resistance)** | Binning: `Very High (>1MΩ)` / `Normal Range` / `Very Low (short-indication)` berdasarkan distribusi data historis per periode heater ON vs OFF | Mempermudah rule-based labeling & sebagai fitur kategorikal tambahan untuk model. |

### C.3. Threshold / Batas Acuan untuk Rule-Based Labeling

| Parameter | Threshold Acuan | Sumber |
|---|---|---|
| `molten_temp` normal | 640°C – 660°C (setpoint 650±10°C operasional; 660°C = COM controller) | Spesifikasi Mesin (A.2) & Metal Temp Controller (A.3) |
| `molten_temp` Overheat | **> 680°C** | Metal Temperature Controller EV1 |
| `molten_temp` Low | **< 640°C** | Metal Temperature Controller EV3 |
| Suhu elemen Safety Heater normal | ~950°C | Safety Heater Controller COM |
| Suhu elemen Safety Heater Overheat | **> 1000°C** | Safety Heater Controller EV1 |
| Suhu elemen Safety Heater Low (indikasi heater tidak efektif) | **< 900°C** | Safety Heater Controller EV3 |
| Thermal Lag window | Perubahan diamati per **1 jam**, threshold **≥10°C** penurunan | Aturan ahli (brief proyek) |
| Fluktuasi voltase wajar | ± 10% dari nominal | Spesifikasi Suplai Daya Listrik |
| Fluktuasi frekuensi wajar | ± 5% dari nominal | Spesifikasi Suplai Daya Listrik |
| Kapasitas pemanas per unit | 8 kW (total 16 kW untuk 2 unit) — basis normalisasi `power_total` wajar per heater aktif | Sistem Pemanas |

### C.4. Diagram Alur Pipeline (Ringkas)

```
Raw Data (date_time, molten_temp, heater1, heater2, voltage_avr, current_avr, power_total)
        │
        ▼
1. Filter periode: keep hanya Maret–Agustus 2025
        │
        ▼
2. Deteksi & drop baris "all-zero" (semua fitur = 0)
        │
        ▼
3. Retain baris "partial-zero" (tandai sebagai kandidat kondisi khusus)
        │
        ▼
4. Feature Engineering: Resistance R, delta_temp_1h, heater_active,
   rolling current_avr, R_category
        │
        ▼
5. Rule-Based Labeling (5 skenario anomali + alarm bawaan, Bagian B & C.3)
        │
        ▼
6. Dataset siap untuk Modeling (Bagian D)
```

---

## D. REKOMENDASI PEMODELAN MACHINE LEARNING

### D.1. Pendekatan Berlapis (Hybrid Approach — Direkomendasikan)

> **Catatan pemilihan model:** Sesuai arahan tim, proyek ini **tidak menggunakan LSTM Autoencoder, GRU-VAE, maupun Isolation Forest** (sudah digunakan oleh anggota tim lain agar tidak ada duplikasi pendekatan). Sebagai gantinya, dipilih **3 model ML yang berbeda karakteristik deteksinya** (boundary-based, density-based, dan supervised tree-based) agar hasil dapat saling melengkapi/dibandingkan (ensemble/voting) dengan Layer 1 rule-based sebagai fondasi wajib.

| Layer | Pendekatan | Alasan |
|---|---|---|
| **Layer 1 — Rule-Based Logic Interlock** (fondasi wajib, non-ML) | Implementasikan langsung ke-5 aturan domain (Bagian B, #1–#4) plus threshold alarm bawaan (Bagian C.3) sebagai **hard rules / interlock system** | Domain knowledge dari manual pabrikan bersifat *deterministik dan safety-critical* — tidak boleh sepenuhnya diserahkan ke model statistik black-box. Rule-based memberi **high precision** untuk kasus yang sudah dipahami mekanismenya (short circuit, thermal lag, dsb), sekaligus menjadi sumber **weak label** untuk melatih Model #3 di bawah. |
| **Model #1 — One-Class SVM (OCSVM)** *(boundary-based, unsupervised)* | Latih pada fitur gabungan (`molten_temp`, `current_avr`, `power_total`, `R`, `delta_temp_1h`) hanya menggunakan data **kondisi normal** (heater ON/OFF wajar) untuk membentuk *decision boundary*; titik di luar boundary = anomali | Efektif menangkap anomali yang berada **jauh di luar batas operasi normal** (mis. lonjakan arus ekstrem pada Skenario #3), robust terhadap distribusi non-Gaussian, dan berbeda prinsip kerja dari Isolation Forest (partisi pohon) maupun Autoencoder (rekonstruksi). |
| **Model #2 — Local Outlier Factor (LOF)** *(density-based, unsupervised)* | Hitung kepadatan lokal tiap titik data relatif terhadap tetangga terdekatnya pada ruang fitur yang sama; titik dengan densitas jauh lebih rendah dari tetangganya = anomali | Unggul mendeteksi **anomali kontekstual/lokal** — mis. kombinasi nilai yang secara global tampak "normal" tapi ganjil dibanding kondisi operasi sejenis (jam operasi sama, status heater sama). Melengkapi Model #1 yang berbasis batas global. |
| **Model #3 — Gradient Boosted Trees (XGBoost/LightGBM Classifier)** *(supervised, tree-based)* | Latih model klasifikasi biner (normal vs anomali) menggunakan **label hasil rule-based (Layer 1)** sebagai target, dengan fitur lengkap termasuk fitur turunan (Bagian C.2) | Memberikan **feature importance** yang interpretatif untuk tim maintenance (mengetahui fitur mana yang paling berkontribusi pada suatu anomali), performa tinggi pada data tabular/time-series-terengineer, dan dapat men-*generalisasi* pola dari rule-based ke kasus baru yang mirip tapi belum eksplisit di-rule. |

**Cara menggabungkan untuk kasus non-safety-critical (ensemble voting):** untuk skenario dengan Severity 🟢 NORMAL/🟡 WARNING/🟠 CRITICAL, sebuah baris data ditandai *flagged for review* jika **Layer 1 rule-based aktif**, **atau** minimal **2 dari 3 model ML** (OCSVM, LOF, XGBoost) sepakat menganggapnya anomali — mengurangi false positive dibanding mengandalkan satu model saja.

**Aturan Hard Interlock untuk kasus 🔴 FATAL/EMERGENCY (mutlak, non-negotiable):**

> Jika **Layer 1 rule-based** melabeli suatu baris/kejadian sebagai **FATAL/EMERGENCY** (mis. signature Short Circuit pada Skenario B.#3, atau alarm **Melt Leak Detect** pada Skenario B.#8 — lihat elaborasi mekanisme di **B.5**), maka **keputusan tersebut bersifat final dan mengesampingkan (override) seluruh output Model #1, #2, dan #3**, **terlepas dari confidence score/probability yang dihasilkan model ML tersebut** — termasuk jika ketiga model ML secara serentak memberi skor "normal" dengan confidence tinggi.

Alasan teknis di balik aturan ini:
- **Model ML bersifat probabilistik dan dapat salah**, terutama pada kondisi *rare event* seperti short circuit yang datanya sangat sedikit dalam training set (lihat penanganan imbalance di **D.3**). Model statistik tidak boleh diberi wewenang untuk "membatalkan" sinyal keselamatan yang sudah dikonfirmasi secara deterministik oleh hardware/sensor pabrikan (Melt Leak Detect, SCR Abnormal).
- **Domain safety-critical menuntut prinsip *fail-safe*, bukan *fail-open*** — sistem harus selalu condong ke sisi aman (menghentikan mesin) ketika ada konflik antara sinyal deterministik dan sinyal statistik, bukan sebaliknya.
- Secara arsitektural, ini berarti Layer 1 (rule-based/hard interlock) **berjalan sebagai gerbang independen di luar pipeline voting ML**, bukan sekadar salah satu "vote" yang setara bobotnya dengan Model #1–#3. Layer 1 mengunci output akhir ke FATAL/EMERGENCY terlebih dahulu; pipeline ensemble ML (voting 2-dari-3) hanya dijalankan untuk baris-baris yang **tidak** memenuhi kondisi hard interlock ini.
- Output model ML pada baris FATAL/EMERGENCY tetap **dicatat sebagai metadata** (bukan dibuang) — berguna untuk audit dan evaluasi apakah model ML "seharusnya" bisa menangkap sinyal ini secara mandiri, sebagai bahan perbaikan model di iterasi berikutnya.

### D.2. Strategi Windowing Waktu

- **Deteksi Thermal Lag (Skenario #4)**: wajib menggunakan **rolling window 1 jam** sesuai definisi ahli — hitung `delta_temp_1h` dan evaluasi status heater sepanjang window tersebut (bukan snapshot per-timestamp saja).
- **Agregasi per jam**: untuk model statistik/ML, pertimbangkan agregasi fitur ke **resolusi per jam** (mean, min, max, std dari `molten_temp`, `current_avr`, `power_total` dalam jam tersebut) sebagai fitur tambahan di samping data granular asli — mengurangi noise sekaligus mempertahankan sinyal aturan #4.
- **Deteksi Spike Arus (Skenario #3)**: gunakan window **lebih pendek** (5–15 menit) karena lonjakan arus akibat short circuit bersifat cepat/mendadak, berbeda karakter waktu dengan thermal lag.
- **Exclude/flag periode charging & metal level tinggi**: gunakan data alarm `Metal Level High/Over High` (jika tersedia dalam log historis) sebagai *mask* untuk mengurangi false positive akibat fluktuasi suhu normal saat charging molten metal baru.

### D.3. Catatan Implementasi Tambahan
- Karena mesin memiliki **dua heater independen**, sebaiknya evaluasi anomali dilakukan **per-heater** (bila data granular tersedia) sebelum digabung menjadi status mesin keseluruhan, agar kegagalan satu heater tidak "diencerkan" oleh heater lain yang masih normal.
- Simpan **rule yang men-trigger label** (bukan hanya label biner anomali/normal) sebagai metadata — memudahkan root cause analysis dan validasi model oleh tim maintenance PT. Tempsens/PT. AHM.
- Gunakan hasil **Layer 1 (rule-based)** sebagai *weak labels* untuk melatih **Model #3 (XGBoost/LightGBM)** secara semi-supervised, sementara **Model #1 (OCSVM)** dan **Model #2 (LOF)** dilatih murni unsupervised pada data normal — kombinasi ini penting mengingat data anomali riil kemungkinan sangat imbalance (rare event).
- Pertimbangkan penambahan fitur interaksi eksplisit (mis. `thermal_lag_flag × voltage_out_of_tolerance_flag`) agar Model #3 dapat mempelajari pola **anomali multivariat** seperti Skenario B.#11, bukan hanya mengandalkan pohon keputusan untuk menemukan interaksi tersebut secara implisit dari fitur mentah.

**Penanganan Data Imbalance pada Model #3 (Supervised — XGBoost/LightGBM):**

Karena kejadian anomali (terutama Severity CRITICAL/FATAL) bersifat *rare event* dibanding data operasional normal, pelatihan Model #3 secara naif berisiko menghasilkan model yang **bias ke kelas mayoritas** (selalu memprediksi "normal"). Rekomendasi teknis untuk menangani hal ini:

- **Resampling — SMOTE (Synthetic Minority Over-sampling Technique):** Terapkan SMOTE (atau varian seperti SMOTE-ENN/Borderline-SMOTE) pada **data training saja** (setelah train-test split, untuk menghindari data leakage) guna membangkitkan sampel sintetis kelas minoritas (anomali) berdasarkan interpolasi antar tetangga terdekat di ruang fitur. Ini membantu classifier mempelajari batas keputusan kelas anomali dengan lebih baik tanpa sekadar menduplikasi baris yang sudah ada.
- **Penyesuaian `scale_pos_weight` (khusus XGBoost/LightGBM):** Sebagai alternatif atau pelengkap SMOTE, atur parameter `scale_pos_weight` = (jumlah sampel Normal) / (jumlah sampel Anomali) agar model memberi **bobot loss lebih besar** pada kesalahan klasifikasi kelas anomali dibanding kelas normal, tanpa perlu mengubah distribusi data secara langsung. Pendekatan ini lebih ringan secara komputasi dibanding oversampling penuh dan sering dikombinasikan dengan SMOTE pada rasio imbalance yang sangat ekstrem.
- **Class weighting sebagai pendekatan tambahan:** Untuk model non-boosting atau sebagai pembanding, `class_weight='balanced'` (scikit-learn API) dapat digunakan sebagai baseline cepat sebelum tuning `scale_pos_weight` secara manual.
- **Hindari evaluasi berbasis Akurasi (Accuracy) semata:** Pada dataset dengan rasio imbalance tinggi (mis. 99% normal vs 1% anomali), model yang selalu memprediksi "normal" akan tetap mencatat akurasi ~99% meski **sepenuhnya gagal** mendeteksi anomali. Gunakan metrik yang lebih relevan:
  - **F1-Score** (harmonic mean antara Precision dan Recall) sebagai ringkasan tunggal performa kelas minoritas.
  - **Precision-Recall AUC (PR-AUC)**, bukan ROC-AUC — PR-AUC lebih informatif dibanding ROC-AUC pada kasus imbalance tinggi karena lebih sensitif terhadap performa pada kelas minoritas.
  - Lihat **D.4** untuk penjelasan lebih lanjut mengenai prioritas metrik **Recall** dalam konteks keselamatan holding furnace.
- **Stratified K-Fold Cross-Validation:** Gunakan stratifikasi pada saat cross-validation agar proporsi kelas anomali (termasuk sub-severity-nya) tetap terjaga konsisten di setiap fold, menghindari fold yang kebetulan tidak memiliki sampel anomali sama sekali.

### D.4. Metrik Evaluasi & Prioritas Keselamatan

Pemilihan metrik evaluasi untuk ketiga model ML (OCSVM, LOF, XGBoost/LightGBM) tidak boleh dilakukan secara generik, melainkan harus mencerminkan **konsekuensi asimetris** antara dua jenis kesalahan klasifikasi dalam konteks operasional holding furnace:

| Jenis Kesalahan | Definisi dalam Konteks Furnace | Konsekuensi |
|---|---|---|
| **False Negative (FN)** | Model gagal mendeteksi kondisi yang **sebenarnya anomali** (mis. short circuit atau thermal lag nyata diklasifikasikan sebagai "normal") | **Sangat berbahaya** — berpotensi membiarkan kondisi FATAL/EMERGENCY (short circuit, melt leak) berlanjut tanpa intervensi, berisiko kerusakan mesin permanen, downtime tak terjadwal, hingga bahaya keselamatan kerja (lihat **B.5**) |
| **False Positive (FP)** | Model salah menandai kondisi **normal** sebagai anomali (alarm palsu) | Merepotkan operator (perlu verifikasi manual), berpotensi menurunkan kepercayaan terhadap sistem (*alarm fatigue*) bila terlalu sering — namun **tidak menimbulkan risiko fisik/keselamatan langsung** |

**Kesimpulan:** Biaya (*cost*) dari False Negative **jauh lebih tinggi** dibanding False Positive pada domain ini — kegagalan mendeteksi anomali riil dapat berujung pada kerusakan peralatan bernilai tinggi atau insiden K3, sementara alarm palsu paling buruk hanya menambah beban verifikasi manual. Oleh karena itu:

- **Recall (Sensitivitas)** — didefinisikan sebagai `TP / (TP + FN)` — harus menjadi **metrik prioritas utama** saat mengevaluasi dan melakukan tuning hyperparameter ketiga model (OCSVM, LOF, XGBoost/LightGBM), khususnya untuk baris-baris yang berpotensi berlabel Severity CRITICAL atau FATAL/EMERGENCY.
- **Precision tetap dipantau** (agar sistem tidak membanjiri operator dengan alarm palsu berlebihan), namun ditempatkan sebagai **metrik sekunder** relatif terhadap Recall — trade-off ini idealnya divisualisasikan lewat **Precision-Recall curve** per model untuk membantu pemilihan threshold operasional yang condong ke sisi aman (*safety-biased threshold*), bukan threshold default 0.5.
- **F1-Score dan PR-AUC** (lihat **D.3**) digunakan sebagai metrik ringkasan untuk perbandingan antar model/eksperimen, namun **keputusan akhir threshold operasional** tetap merujuk pada target Recall minimum yang disepakati tim (mis. "Recall ≥ 0.95 untuk kelas anomali CRITICAL/FATAL" sebagai syarat go-live model).
- Untuk baris dengan Severity 🔴 FATAL/EMERGENCY secara khusus, target idealnya adalah **Recall mendekati 1.0 pada Layer 1 rule-based** (bukan model ML) — sejalan dengan prinsip **Hard Interlock** pada **D.1**, di mana keputusan safety-critical tidak boleh bergantung pada Recall model statistik yang secara inheren tidak pernah sempurna 100%.
- Metrik evaluasi ini sebaiknya dipecah **per Severity Level** (bukan hanya biner Normal/Anomali secara agregat) agar tim dapat memantau apakah model secara khusus lemah dalam mendeteksi skenario tertentu (mis. Recall rendah khusus untuk Skenario #11 Anomali Multivariat) dan melakukan perbaikan yang tertarget.
