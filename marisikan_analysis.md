# MARISIKAN

> Laporan dibuat berdasarkan aturan anti-asumsi: setiap klaim faktual diberi status evidence **[CONFIRMED]** (ada sumber langsung), **[INDICATED]** (indikasi kuat/evidence tidak langsung), atau **[UNKNOWN]** (tidak dapat diverifikasi dari sumber publik).
>
> **Catatan penting:** Marisikan adalah produk lokal Indonesia dari perusahaan *GreenFish* (Islandia). Website resmi Marisikan sangat minimal dan hanya menyebut fitur secara umum. Sebagian besar detail teknis hanya terdokumentasi untuk platform *GreenFish* (teknologi induk). Hal ini dibedakan secara eksplisit pada setiap bagian di bawah; informasi GreenFish TIDAK otomatis sama dengan Marisikan.

---

## 1. Profil Software

| Aspek | Informasi | Evidence / Sumber |
| --- | --- | --- |
| Nama | Marisikan (ditulis "MARISIKAN by GreenFish") | Situs resmi marisikan.com [S1] |
| Developer / Institution | GreenFish (perusahaan AI Islandia; benteng produk lokal untuk Indonesia) | Situs resmi Marisikan menyebut "Didukung oleh GreenFish AI", kontak `info@greenfish.is`; © 2025 GreenFish [S1] |
| Tahun pengembangan / peluncuran | Tidak dicantumkan di situs Marisikan; GreenFish didirikan 2023 [S2][S3][S7] | [S1][S2] |
| Negara | Lokalisasi pasar: Indonesia. Developer: Islandia (kantor Reykjavík & Copenhagen) | [S1][S2] |
| Website | https://www.marisikan.com/ | [S1] |
| Platform | Aplikasi mobile (klaim "unduh dari App Store atau Google Play") + platform web GreenFish sebagai induk | [S1][S2] |
| Target pengguna | Nelayan Indonesia (per skema harga perorangan "Nelayan Pro" dan "Armada Enterprise") | [S1] |
| Tujuan utama | Membantu nelayan Indonesia "menemukan ikan lebih cepat, lebih cerdas" dgn menggabungkan oseanografi real-time, AIS, dan prediksi AI | [S1] |
| Geographic scope | Perairan Indonesia ("teknologi laut untuk nelayan Indonesia"; harga dalam Rupiah) | [S1] |
| Status | **Aktif** (site © 2025; masih dirujuk sebagai platform berjalan pada Juni 2026 oleh Noah Intelligence) | [S1][S10] |

---

## 2. Fokus dan Tujuan

**Masalah yang ingin diselesaikan** (dinyatakan oleh situs Marisikan): efisiensi penangkapan — nelayan ingin "menangkap lebih banyak ikan dengan lebih efisien", hemat bahan bakar dan waktu [S1].

**Tujuan utama:** menyatukan tiga teknologi dalam satu aplikasi — (1) kondisi oseanografi real-time, (2) AIS "kelas dunia", (3) prediksi AI oleh GreenFish [S1].

**Target pengguna:** nelayan Indonesia, dari individu (paket Free/Pro) hingga armada enterprise (multi-kapal, laporan, integrasi API) [S1].

**Konteks penggunaan:** aplikasi mobile panduan sebelum dan saat melaut ("ikuti prediksi AI"), dirancang "tanpa pelatihan teknis" [S1].

**Klasifikasi fokus** berdasarkan klaim situs [S1]:

| Aspek | Fokus? | Evidence |
| --- | --- | --- |
| Fishing ground prediction | ✅ klaim "prediksi AI lokasi terbaik menemukan ikan hari ini", "peta panas zona ikan" | [S1] |
| Fishing activity / effort | ⚠️ ada "zona penangkapan aktif" dari AIS | [S1] |
| Vessel monitoring | ✅ via AIS real-time (94% klaim "lacak ribuan kapal di sekitar Anda") | [S1] |
| Fisheries management | ❌ tidak disebutkan | [S1] |
| Conservation / bycatch | ❌ tidak disebutkan di situs Marisikan (bycatch ada di produk GreenFish) | [S1][S5] |
| Enforcement | ❌ tidak disebutkan | [S1] |
| Decision support | ✅ rekomendasi rute kapal, prediksi spesies & waktu terbaik | [S1] |

> Konteks pencetus teknologi induk: GreenFish didirikan 2023 karena penulis tesis "Innovation with AI in Fisheries" melihat industri perikanan kurang mendapat inovasi alat bantu keputusan lokasi tangkap [S5].

---

## 3. Data Sources

Situs Marisikan menyebut fitur data berikut [S1]. Mencolok: tidak ada satu pun spesifikasi sumber/resolusi/temporal yang dipublikasikan di situs Marisikan.

| Data | Digunakan? | Sumber Data | Resolusi | Temporal Coverage | Fungsi | Evidence |
| --- | --- | --- | --- | --- | --- | --- |
| SST (suhu laut) | ✅ disebut "suhu ... permukaan laut" | Tidak didokumentasikan | Tidak didokumentasikan | Tidak didokumentasikan | layer oseanografi + input prediksi AI | [S1] [CONFIRMED utk keberadaan fitur] |
| Chlorophyll-a | ✅ "peta klorofil & plankton" | Tidak didokumentasikan | Tidak didokumentasikan | Tidak didokumentasikan | layer oseanografi | [S1] |
| SSH / altimetry | ❌ tidak disebutkan di situs Marisikan | — | — | — | — | [S1] |
| Salinity | ✅ disebut "salinitas" | Tidak didokumentasikan | — | — | layer oseanografi | [S1] |
| Current (arus) | ✅ disebut "arus" | Tidak didokumentasikan | — | — | layer oseanografi | [S1] |
| Wave / gelombang | ✅ "prakiraan cuaca maritim" (gelombang tidak eksplisit; cuaca maritim disebut) | Tidak didokumentasikan | — | — | layer cuaca | [S1] |
| AIS | ✅ "AIS kelas dunia", "pelacakan kapal real-time", "identifikasi jenis & ukuran kapal" | Tidak didokumentasikan di situs Marisikan | — | — | vessel tracking + "zona penangkapan aktif" | [S1] |
| VMS | ❌ tidak disebutkan | — | — | — | — | [S1] |
| VIIRS | ❌ tidak disebutkan | — | — | — | — | [S1] |
| SAR / Sentinel | ❌ tidak disebutkan | — | — | — | — | [S1] |
| MODIS | ❌ tidak disebutkan | — | — | — | — | [S1] |
| Catch data | ❌ tidak disebutkan di situs Marisikan (di produk GreenFish: logbook hasil tangkapan klien) | — | — | — | — | [S1][S2][S5] |
| Bathymetry | ❌ tidak disebutkan di situs Marisikan (di GreenFish: kontur kedalaman/3D) | — | — | — | — | [S1][S2] |
| WPP / EEZ | ❌ tidak disebutkan | — | — | — | — | [S1] |
| Weather | ✅ "prakiraan cuaca maritim" | Tidak didokumentasikan | — | — | layer cuaca | [S1] |
| Historical / pola historis | ✅ prediksi AI disebut "menganalisis ... pola historis" | Tidak didokumentasikan | — | — | input model prediksi | [S1] |
| Lainnya | Plankton ("peta klorofil & plankton"); "posisi kapal lain di sekitar" | Tidak didokumentasikan | — | — | — | [S1] |

> Catatan penting: Situs Marisikan **tidak menyebutkan** źródła data (provider), resolusi spasial/temporal, ataupun spesifikasi satelit. Jangan menganggap Marisikan menggunakan ESA/NASA di situs Marisikan; klaim "data ESA & NASA" hanya terdokumentasi untuk platform GreenFish [S5].

---

## 4. Data Acquisition

| Data | Provider | Acquisition Method | Real-time? | Historical? | Public API? | Evidence |
| --- | --- | --- | --- | --- | --- | --- |
| Oseanografi (Marisikan) | **Tidak didokumentasikan** di situs Marisikan | Tidak didokumentasikan | ✅ klaim "data laut langsung", "real-time" | ✅ klaim paket Gratis mencakup "data historis"; Pro "data historis 30 hari" | Tidak didokumentasikan | [S1] |
| AIS (Marisikan) | **Tidak didokumentasikan** di situs Marisikan; produk induk GreenFish memakai "Satellite AIS by Kpler" [S2][S11] | Tidak didokumentasikan | ✅ "real-time" | — | Tidak didokumentasikan | [S1][S2][S11] |
| Data satelit lingkungan (GreenFish) | ESA & NASA (per artikel GSA Advocate) [S5] | Tidak didokumentasikan | — | "decades of historical catch logs" [S5][S7] | Tidak didokumentasikan | [S5][S7] |
| Data hasil tangkapan / logbook (GreenFish) | Data klien (fleet) | Tidak didokumentasikan | — | ✅ historis | — | [S2][S5] |

> Kesimpulan: mekanisme akuisisi data Marisikan **tidak didokumentasikan secara publik**. Apa pun yang tertulis di bagian ini untuk GreenFish adalah untuk produk platform B2B, bukan klaim bagi Marisikan.

---

## 5. Data Processing

**Tidak ada dokumentasi pipeline processing Marisikan.** Situs Marisikan tidak menjelaskan preprocessing, spatial processing, temporal processing, maupun vessel processing [S1]. Detail berikut hanya untuk GreenFish (produk induk):

| Processing | Digunakan? | Penjelasan | Evidence |
| --- | --- | --- | --- |
| Preprocessing (umum) | [UNKNOWN] | Tidak didokumentasikan utk Marisikan / GreenFish | — |
| Training berbasis logbook historis | [INDICATED] utk GreenFish | Model dilatih dari "millions of historical fishing logs" + data lingkungan; model dieksklusifkan per klien | [S5] |
| Update/pemrosesan berkala tetap | [CONFIRMED] utk GreenFish | "Refreshed every 6 hours", "updated every 6 hours" | [S2][S9] |
| Backtesting musiman | [CONFIRMED] utk GreenFish | Model "backtested against seasons you already know" | [S2] |
| Vessel / trajectory processing | [UNKNOWN] | Tidak didokumentasikan | — |

---

## 6. Feature Engineering

**Marisikan:** situs hanya menyebut "pola historis" sebagai input prediksi dan output "peta panas zona ikan, prediksi spesies & waktu terbaik, rekomendasi rute" [S1]. **Feature engineering spesifik tidak didokumentasikan.**

**GreenFish (produk induk):** klaim "100+ ocean environmental variables" dianalisis saat pengembangan model [S2]; layer oseanografi mencakup SST, chlorophyll, currents, thermal fronts, kedalaman, bathymetry [S11]; prediksi dihasilkan dalam bentuk occurrence probability, expected size, atau CPUE ("catch per unit effort") [S2]. Variabel turunan seperti anomali SST, gradien suhu, dan front oseanik **tidak dinyatakan secara eksplisit**.

| Raw → Derived → Intelligence | Status | Evidence |
| --- | --- | --- |
| SST/klorofil/arus → probability zone / CPUE / ukuran ikan | [INDICATED] utk GreenFish | [S2][S11] |
| CPUE → zona probabilitas tinggi | [INDICATED] (greenfish) | [S2] |
| Detail variabel turunan | [UNKNOWN] | — |

---

## 7. Computational Method / Algorithm

**Algoritma spesifik TIDAK dipublikasikan oleh Marisikan maupun GreenFish.** Istilah yang tersedia: "AI", "machine learning", "artificial intelligence" [S1][S2][S6][S7]. Jenis arsitektur (mis. Random Forest / XGBoost / DL) **tidak dapat diverifikasi** — jangan berasumsi.

| Method | Input | Output | Purpose | Evidence |
| --- | --- | --- | --- | --- |
| Machine learning (jenis model tidak diungkap) | Logbook tangkapan historis + data satelit + 100+ variabel oseanografi | Zona probabilitas, CPUE/quantity/size forecast, bycatch risk | Prediksi lokasi & hasil tangkap | [CONFIRMED] utk GreenFish: [S5][S6][S7][S9] |
| Supercomputing / HPC | model training runtime | — | Skala komputasi besar | [CONFIRMED] utk GreenFish: [S5][S6][S7] |
| Model AI (utk Marisikan) | "data oseanografi dan pola historis" | "lokasi terbaik menemukan ikan hari ini" | Decision support nelayan | [CONFIRMED] klaim fitur: [S1] |

> Perbedaan angka horizon: sebagian sumber menyebut **8 hari** ke depan [S2][S5][S7][S9], sebagian **10 hari** [S6][LinkedIn][S11 listing MWM menyebut 8 hari; LinkedIn 10 hari]. Untuk Marisikan, horizon prediksi **tidak dinyatakan di situsnya** ([UNKNOWN]).
>
> Discrepancy lain yang perlu dicatat: judul EEN menyebut "10-day forecasts" dan deskripsi LinkedIn "up to ten days", sedangkan sumber resmi GreenFish dan WP lainnya konsisten "8 days". Prioritaskan sumber resmi GreenFish dan artikel berita primer (8 hari). Ini konflik sumber yang dijelaskan, bukan dipilih diam-diam.

---

## 8. Fishing Intelligence

### A. Fishing Ground Intelligence
- ✅ **Potential fishing ground / hotspot** — "peta panas zona ikan", "zona ikan terpanas" [S1]; di GreenFish: "heat map of the most promising zones" [S2]. **[CONFIRMED]**
- Prediksi spesies & waktu terbaik [S1] — **[CONFIRMED]** (klaim fitur Marisikan).

### B. Fishing Activity Intelligence
- "Zona penangkapan aktif" berbasis AIS [S1] — **[CONFIRMED] klaim fitur** (mekanisme tidak dijelaskan).

### C. Vessel Intelligence
- "Lacak ribuan kapal di sekitar Anda secara real-time; identifikasi jenis & ukuran kapal" [S1] — **[CONFIRMED] klaim fitur**. Posisinya tracking/awareness, bukan analitik perilaku (aktivitas mencari, trans-shipment, dark vessel — tidak didokumentasikan).

### D. Environmental Intelligence
- SST, arus, salinitas, klorofil/plankton, cuaca maritim [S1] — **[CONFIRMED] klaim fitur**. Front/upwelling tidak disebut.

### E. Temporal Intelligence
- "pola historis" sebagai input [S1] dan paket "data historis 30 hari" (Pro) [S1] — **[CONFIRMED] klaim**. Forecasting di Marisikan situs tidak menyebut horizon; di GreenFish 8 hari/6 jam **[CONFIRMED] utk GreenFish**.

---

## 9. Prediction Target

**Marisikan pada level landing page** mengklaim prediksi "lokasi terbaik menemukan ikan hari ini" + "prediksi spesies & waktu terbaik" [S1]. **Unit, akurasi, dan validasi TIDAK dicantumkan di situs Marisikan.**

| Prediction Target | Input | Output | Unit | Accuracy | Evidence |
| --- | --- | --- | --- | --- | --- |
| Fishing ground / potensi lokasi | data oseanografi + pola historis (Marisikan) | zona panas | — | tidak dipublikasikan utk Marisikan | [S1] |
| Species & waktu terbaik (Marisikan) | — | prediksi spesies & waktu | — | tidak dipublikasikan | [S1] |
| Location, quantity, size, bycatch (GreenFish) | logbook klien + satelit + 100+ variabel | peta probabilitas / ukuran / CPUE | — | **75–92%** (utk model GreenFish, diklaim) | [S5][S7][S9] |

> Klaim akurasi 75–92% **hanya berlaku untuk GreenFish**, dikutip oleh 3 sumber [S5][S7][S9][S10]. Akurasi utk Marisikan **[UNKNOWN]** — tidak dipublikasikan.

---

## 10. Spatial Intelligence

| Capability | Ada? | Evidence |
| --- | --- | --- |
| Interactive map / peta laut | ✅ "Buka Peta Laut", "peta panas zona ikan", "peta klorofil" | [S1] [CONFIRMED] |
| Heatmap hotspot ikan | ✅ | [S1] |
| Environmental overlay | ✅ (suhu, arus, salinitas, klorofil, cuaca) | [S1] |
| Vessel density / spatial clustering | ❌ tidak didokumentasikan | [S1] |
| WPP / EEZ / MPA layers | ❌ tidak disebutkan | [S1] |
| Zona penangkapan aktif (AIS-based) | ✅ klaim | [S1] |
| Navigation / rekomendasi rute | ✅ "rekomendasi rute kapal" (klaim) | [S1] |
| Depth/bathymetry layer | ❌ tidak di situs Marisikan (✅ di GreenFish 3D [S2]) | [S1][S2] |

> Jawaban: Marisikan menampilkan lokasi (map + heatmap + overlay lingkungan), dan klaim "rekomendasi rute". **Tingkat spatial intelligence (analisis spasial seperti clustering, jarak ke pantai/port, analisis WPP) tidak didokumentasikan.**

---

## 11. Temporal Intelligence

| Capability | Ada? | Evidence |
| --- | --- | --- |
| Historical data | ✅ (paket: "data historis" / "data historis 30 hari"; input prediksi "pola historis") | [S1] [CONFIRMED klaim] |
| Time slider | ❌ tidak didokumentasikan | [S1] |
| Monthly trend | ❌ tidak didokumentasikan | [S1] |
| Annual / seasonality | ⚠️ GreenFish klaim "season review", "year-over-year" — utk armada B2B | [S2] [INDICATED—bukan utk Marisikan] |
| Forecasting | ✅ klaim prediksi harian; horizon tidak disebut di Marisikan (GreenFish: 8 hari / 6 jam) | [S1] [CONFIRMED klaim]; [S2][S9] |
| Anomaly detection | ❌ tidak didokumentasikan | [S1] |

---

## 12. AIS / VMS / Vessel Intelligence

- **AIS:** digunakan. Situs Marisikan: "Lacak ribuan kapal di sekitar Anda secara real-time", "Identifikasi jenis & ukuran kapal", "Zona penangkapan aktif" [S1] — **[CONFIRMED] klaim fitur**. Provider AIS utk Marisikan tidak disebut; produk induk GreenFish memakai **"Satellite AIS by Kpler"** [S2][S11] — **[INDICATED]** utk Marisikan.
- **VMS:** **tidak disebutkan** di Marisikan maupun GreenFish publik.
- **Vessel data** (MMSI, IMO, flag, owner): tidak didokumentasikan.
- **Vessel behavior** (fishing/transit/loitering/anomaly/dark vessel): tidak didokumentasikan utk Marisikan. GreenFish menyebut "AIS activity log — who is cruising, who is fishing" [S2] — **[INDICATED]**.
- **AIS + VMS + VIIRS fusion:** tidak ditemukan evidence utk Marisikan.

> Marisikan berada pada level **vessel tracking/awareness via AIS**, bukan vessel intelligence analitik (tidak ada klaim deteksi dark vessel, trans-shipment, anomaly).

---

## 13. Decision Support

Skala 1–5 terhadap Marisikan:

| Level | Capability | Status |
| --- | --- | --- |
| 1 | Raw data visualization | ✅ [CONFIRMED] (layer oseanografi, AIS, peta) [S1] |
| 2 | Data interpretation | ⚠️ parsial — "zona penangkapan aktif", "peta panas zona ikan" (sudah merupakan interpretasi) [S1] |
| 3 | Prediction | ✅ [CONFIRMED klaim] — prediksi lokasi/spesies/waktu [S1] |
| 4 | Recommendation | ✅ [CONFIRMED klaim] — "rekomendasi rute kapal" [S1] |
| 5 | Operational decision support | ⚠️ sebagian — nasional Indonesia, tetapi tidak ada dokumentasi integrasi dengan operasional/Navigasi/GPS/keselamatan [S1] |

> Setelah user melihat informasi, tindakan yang didukung: memilih zona panas, mengikuti rute rekomendasi, hemat BBM/waktu ("hemat bahan bakar, hemat waktu, tangkap lebih banyak") [S1]. Tidak ditemukan fitur keselamatan (SOS, peringatan cuaca berbahaya) di situs Marisikan.

---

## 14. Fisher User Experience

| Aspek | Keterangan | Evidence |
| --- | --- | --- |
| Interface utk nelayan | ✅ diklaim "dirancang untuk semua nelayan", "tidak perlu pelatihan teknis" | [S1] |
| Mobile application | ✅ "Unduh dari App Store atau Google Play" | [S1] |
| Bahasa lokal | ✅ Bahasa Indonesia (seluruh situs produk Indonesia) | [S1] |
| Offline mode | ❌ tidak didokumentasikan utk Marisikan (✅ utk app GreenFish: "keeps working offline at sea" — [S11]) | [S1][S11] |
| Low-bandwidth friendly | ❌ tidak didokumentasikan | [S1] |
| GPS / navigasi | ⚠️ app GreenFish punya posisi sendiri & routing; Marisikan klaim "rekomendasi rute" — detail tidak ada | [S1][S11] |
| Recommended fishing area | ✅ "zona ikan terpanas", "ikuti prediksi AI" | [S1] |
| Weather/safety warning | ⚠️ hanya "prakiraan cuaca maritim"; tidak ada klaim peringatan keselamatan | [S1] |
| Catch recording | ❌ tidak di situs Marisikan (✅ di app GreenFish: catch logging) | [S1][S11] |
| Feedback nelayan | ❌ tidak didokumentasikan | [S1] |

**Klasifikasi:** Marisikan diposisikan sebagai **Fisher Decision Support Tool** (produk komersial langsung ke nelayan), sedangkan produk induk GreenFish bersifat **B2B Fleet Tool**. Namun kedalaman desain UX nelayan **tidak dapat diverifikasi**.

---

## 15. Historical Intelligence

| Capability | Ada? | Evidence |
| --- | --- | --- |
| Historical vessel activity | ❌ tidak didokumentasikan | [S1] |
| Historical fishing ground | ⚠️ "data historis 30 hari" utk paket Pro (red flag: tidak jelas apakah historis lingkungan atau tangkapan) | [S1] [UNKNOWN detail] |
| Historical environmental condition | ⚠️ GreenFish: "decades of historical catch logs" + variabel lingkungan [S5][S7] — utk model, bukan utk user Marisikan | [S5][S7] |
| Hotspot persistence / seasonal | ❌ tidak didokumentasikan utk Marisikan | [S1] |
| Year-to-year / long-term trend | ⚠️ GreenFish "Season Review", "year-over-year comparisons" utk fleet | [S2] [INDICATED—GreenFish] |

> Pertanyaan "apa yang terjadi di lokasi ini sebelumnya?" — **tidak dapat dijawab dari dokumentasi Marisikan yang ada.**

---

## 16. Validation & Accuracy

**Tidak ada publikasi validasi Marisikan.** Utk model GreenFish:

| Aspect | Result | Evidence |
| --- | --- | --- |
| Ground truth | Tidak didokumentasikan secara publik | — |
| Dataset | Tidak didokumentasikan secara publik | — |
| Validation method | Backtesting musiman (klaim di situs GreenFish); uji lapangan bersama klien ("validdation testing ... real-world conditions") | [S2][S9] |
| Accuracy | **75–92%** (klaim utk model GreenFish; "share of fishing activity that has historically occurred within the predicted zones") | [S5][S7][S9] |
| Precision / Recall / F1 / RMSE / MAE | Tidak dipublikasikan | — |
| Spatial / temporal validation | Tidak dipublikasikan | — |
| Studi kasus riil | Musim makarel Islandia 2024-25: user GreenFish menyelesaikan kuota lebih cepat; fuel $79/ton vs $120/ton kontrol; ROI 50x ($60k/vessel vs $1.5M estimasi penghematan) — data dilaporkan oleh GreenFish sendiri | [S2][S7] |

> Perhatian: studi kasus & angka di atas adalah **klaim vendor, bukan hasil peer-review**. Akurasi utk Marisikan di Indonesia **[UNKNOWN]**.

---

## 17. Explainability

| Capability | Ada? | Evidence |
| --- | --- | --- |
| AI menjelaskan alasan prediksi | ✅ di GreenFish: "Every prediction unpacks into the ocean variables driving it — see why the model rates a zone" | [S2] [CONFIRMED—GreenFish] |
| Feature importance / SHAP | ❌ tidak didokumentasikan | — |
| Probability / confidence | ✅ GreenFish menampilkan zone probability (mis. 17.6% → 81.9%) | [S2] |
| Rule-based explanation | ❌ tidak didokumentasikan | — |

> Meskipun GreenFish memiliki penjelasan variabel, **di situs Marisikan tidak ada klaim explainability**.

---

## 18. Feedback Loop

| Langkah | Ada? | Evidence |
| --- | --- | --- |
| Prediction ↓ Fishing Trip ↓ Actual Catch ↓ Feedback ↓ Model update | ⚠️ Di GreenFish: "The model continuously learns from new fishing data and feedback"; "Every observation you make at sea sharpens the model"; "Catch logs ... feed directly into your prediction models" | [S2][S11] [CONFIRMED—GreenFish] |
| Input nelayan (lokasi/spesies/berat/gear…) via Marisikan | ❌ tidak didokumentasikan di situs Marisikan | [S1] |
| Mekanisme learning loop Marisikan konkret | [UNKNOWN] | — |

---

## 19. Technical Architecture

**Technical stack tidak dipublikasikan.** Tidak ada dokumentasi resmi Marisikan/GreenFish yang menyebut React/Vue/Python/PostGIS/etc. Hal yang dapat dikonfirmasi konseptual:

- Platform pengiriman GreenFish: "web-based platform accessible from desktop, tablet, or mobile; no hardware installation" [S2] + app mobile [S11].
- Infrastruktur komputasi: HPC/supercomputing utk training model [S5][S6][S7].
- API: Marisikan paket Enterprise menyebut "integrasi API" [S1]; GreenFish memiliki API utk buoy tracking [S2]. **Dokumentasi teknis API tidak publik.**
- Sisanya: **Technical stack tidak ditemukan dalam sumber publik.**

---

## 20. API & Interoperability

| API / Data Access | Available? | Authentication | Public? | Evidence |
| --- | --- | --- | --- | --- |
| 15API integrasi armada | ✅ diklaim utk paket Enterprise Marisikan | Tidak didokumentasikan | Tidak (enterprise) | [S1] |
| API buoy tracking (GreenFish) | ✅ | Tidak didokumentasikan | Tidak | [S2] |
| Data download / export | ❌ tidak didokumentasikan | — | — | — |
| Public developer API | ❌ tidak ditemukan dokumentasi publik | — | — | — |

---

## 21. Data Governance, Security & Privacy

- Kebijakan data GreenFish tersedia: "Data Protection Policy" & "Terms and Conditions" di greenfish.is [S2].
- Model GreenFish diklaim **exclusive per klien** dan data tetap milik klien ("The data stays yours") [S2][S9].
- **Untuk Marisikan tidak ada dokumentasi governansi AIS/VMS, anonimisasi data kapal, atau kebijakan berbagi data** [S1] — [UNKNOWN].
- Marisikan mengakses **data kapal publik via AIS** (bukan VMS); tapi detail privasi tidak didokumentasikan.

---

## 22. Limitations

### Documented Limitation (eksplisit per vendor/paper)
- Situs GreenFish menyatakan prediksi adalah **saran, bukan suruhan** — fishers mempertahankan pengetahuan & pengalaman mereka ("we are suggesting potential fishing locations rather than tell them where they should fish") [S5].
- Tidak ada klaim akurasi utk Marisikan; utk GreenFish tidak dipublikasikan angka yang bisa diverifikasi pihak ketiga (vendor sendiri menekankan tidak menjamin) — [S5][S7].

### Observed Limitation (dari observasi platform)
- Website Marisikan **sangat minimal**: tidak ada dokumentasi teknis, spesifikasi data, resolusi, metodologi, FAQ produk, ataupun evidence penggunaan di Indonesia. [S1]
- Tidak ada informasi VMS, WPPNRI, MPA, data tangkapan, maupun integrasi data pemerintah Indonesia. [S1]
- Harga konsumen berlangganan (Rp99rb/bulan) — adopsi nelayan skala kecil tanpa literasi digital tetap jadi pertanyaan (belum ada dokumentasi adopsi).

### Research Gap (dibanding kebutuhan sistem yang akan dibangun)
- Belum ada evidence sinkronisasi dengan data nasional Indonesia (KKP: WPPNRI, E-Logbook, VMS, STELINA).
- Tidak ada layer WPPNRI/EEZ/MPA/bathymetry/coastline (yang menjadi kebutuhan dataset Anda).
- Tidak ada evidence integrasi AIS+VMS+VIIRS+oSST-SAR dalam satu workflow keputusan utk nelayan.

---

## 23. Strengths

| Aspek | Evidence |
| --- | --- |
| **Data integration 3-in-1** (oseanografi + AIS + AI) dalam satu aplikasi mobile utk nelayan Indonesia | [S1][S10] |
| **Teknologi prediksi matang dari GreenFish** — model dilatih jutaan data, 100+ variabel, superkomputer, akurasi klaim 75–92% di pasar global | [S5][S6][S7][S9] |
| **Horizon prediksi operasional** (8 hari, refresh 6 jam utk GreenFish) dan update rutin | [S2][S9] |
| **Penjelasan prediksi** (unpack ocean variables) & probability zone di GreenFish | [S2] |
| **Keberhasilan terukur di Islandia** (studi kasus makarel: efisiensi bahan bakar 34%, kuota lebih cepat) — bukti konsep komersial | [S2][S7] |
| **Model bisnis skala** (Free → Pro → Enterprise + API), target pasar Indonesia langsung | [S1] |
| Pengakuan industri: Seafood Innovation Award 2025, Icelandic award 2024 | [S7] |

---

## 24. Feature Matrix

| Feature | Available | Evidence |
| --- | ---: | --- |
| SST | ✅ (klaim) | [S1] |
| Chlorophyll | ✅ (klaim) | [S1] |
| SSH | ❌/? tidak disebut | [S1] |
| Salinity | ✅ (klaim) | [S1] |
| Current | ✅ (klaim) | [S1] |
| Wave / cuaca maritim | ✅ (klaim cuaca) | [S1] |
| AIS | ✅ (klaim; provider tidak disebut) | [S1] |
| VMS | ? tidak disebut | [S1] |
| VIIRS | ? tidak disebut | [S1] |
| SAR / Sentinel | ? tidak disebut | [S1] |
| Weather | ✅ (klaim) | [S1] |
| Fishing Ground Prediction | ✅ (klaim AI) | [S1] |
| Vessel Monitoring | ✅ (klaim via AIS) | [S1] |
| Fishing Effort | ? (hanya "zona penangkapan aktif") | [S1] |
| Historical Analysis | ⚠️ "data historis" (30 hari di paket Pro) | [S1] |
| Seasonality | ? tidak didokumentasikan | [S1] |
| Forecasting | ✅ (klaim harian; horizon tidak disebut utk Marisikan) | [S1] |
| Hotspot Detection | ✅ (klaim "peta panas zona ikan") | [S1] |
| WPPNRI | ? tidak disebut | [S1] |
| Navigation | ✅ (klaim "rekomendasi rute kapal") | [S1] |
| Catch Recording | ? tidak di Marisikan (ada di app GreenFish) | [S1][S11] |
| Fisher Feedback | ? tidak didokumentasikan | [S1] |
| API | ✅ (klaim utk Enterprise) | [S1] |
| Offline mode | ? tidak utk Marisikan (ada di GreenFish app) | [S1][S11] |

Legenda: ✅ = confirmed tersedia (sering baru level "klaim fitur" dari situs resmi; detail di [S1]); ❌ = confirmed tidak tersedia; ? = tidak ditemukan/ tidak dapat diverifikasi. Sesuai aturan, `?` dipakai saat tidak ada bukti.

---

## 25. Positioning

```text
                FISHING INTELLIGENCE
                         │
       ┌─────────────────┼─────────────────┐
       ↓                 ↓                 ↓
 Fish Prediction    Vessel Intelligence   Fisheries
       │                 │             Management
       ↓                 ↓                 ↓
  [Marisikan]      [Marisikan]          ── (lemah)
  ⭐ terkuat:       (AIS tracking,
  prediksi lokasi    bukan analitik
  + oseanografi      perilaku)
  + AI
```

Marisikan paling kuat di **Fish Prediction / fishing ground intelligence yang diarahkan ke nelayan operasional** (mobile app). Kekuatan kedua: **vessel tracking via AIS**. Terlemah: **fisheries management & enforcement** (tidak ada VMS, WPP, logbook pemerintah, konservasi).

---

## 26. GAP ANALYSIS

| Kategori | Temuan |
| --- | --- |
| **Data Gap** | Tidak ada evidence VMS, VIIRS, SAR/Sentinel, MODIS, SSH, bathymetry, WPPNRI/EEZ/MPA, coastline, pelabuhan, data hasil tangkapan nasional. Data Indonesia (KKP) tidak terlihat terintegrasi. |
| **Intelligence Gap** | Prediksi ada (klaim), tetapi tidak ada dokumentasi metode, variabel, maupun validasi utk perairan Indonesia; tidak ada species-specific layer WPPNRI yang terverifikasi. |
| **Temporal Gap** | Horizon prediksi Marisikan tidak didokumentasikan; "data historis" terbatas (klaim 30 hari pada Pro). Tidak ada trend/seasonsal/long-term analysis utk nelayan. |
| **Spatial Gap** | Tidak ada WPP/EEZ/MPA; tidak ada analisis jarak ke pelabuhan/coast; tidak ada bathymetry di level Marisikan. |
| **Integration Gap** | AIS + oseanografi + AI sudah digabung; tetapi integrasi AIS+VMS+VIIRS+SAR (multi-source vessel + environmental) **tidak didokumentasikan**. |
| **User Gap** | Ditujukan ke nelayan (baik), tetapi tidak ada bukti desain UX khusus nelayan Indonesia skala kecil (literasi digital, offline, bahasa daerah, GPS kapal kecil), dan model bisnis langganan bulanan. |
| **Decision Support Gap** | Rekomendasi zona/rute ada (klaim), tetapi tidak ada mekanisme tertutup (prediksi → trip → tangkapan aktual → feedback → model) yang terdokumentasi utk Marisikan. |
| **Technical Gap** | Stack, arsitektur, API public, kebijakan data/privasi utk Marisikan tidak didokumentasikan. |

---

## 27. Potential Novelty

> Ini merupakan **potential research/development novelty**, bukan klaim bahwa belum pernah ada di seluruh dunia.

| Existing Capability | Gap | Proposed Improvement | Evidence |
| --- | --- | --- | --- |
| Marisikan/GreenFish: oseanografi + AIS + AI dalam satu aplikasi | Tidak ada evidence integrasi **historical oceanographic data + AIS/VMS + VIIRS/SAR catch-based feedback loop** yang disesuaikan **per WPPNRI** utk pengambilan keputusan nelayan Indonesia | Sistem yang menggabungkan penginderaan jauh multi-sensor Indonesia (MODIS/VIIRS/Sentinel) + VMS/AIS nasional + E-Logbook/STELINA hasil tangkapan + WPPNRI/EEZ/MPA dalam satu decision-support workflow dengan kalibrasi per WPPNRI | [S1][S5] — gap yang dapat diverifikasi dari kekosongan dokumentasi Marisikan |
| GreenFish: explainable prediction (unpack variables) | Marisikan tidak mendokumentasikan explainability utk nelayan (bahasa lokal, alasan rekomendasi) | Penerjemahan alasan prediksi ke nelayan (Bahasa Indonesia/lokal), confidence score, dan konteks WPPNRI | [S2] vs [S1] |
| GreenFish: feedback loop dari logbook | Marisikan tidak dokumen feedback loop utk nelayan kecil; biaya langganan Rp99rb/bulan | Desain feedback loop murah/offline + catatan tangkapan (spesies, berat, gear, durasi) → update model per wilayah | [S2][S11] vs [S1] |
| AIS tracking (Marisikan) | Tidak ada vessel behavior analytics (fishing event detection, effort) utk kapal kecil yang TIDAK punya AIS (mayoritas nelayan Indonesia) | Deteksi aktivitas dari VMS/gabungan + pengakuan polarisasi kapal kecil berbasis satelit optik/SAR docking dgn oseanografi | [S1] — gap vs kebutuhan armada kecil |
| Cuaca maritim di Marisikan | Tidak ada peringatan keselamatan operasional (SOS, cuaca ekstrem) | Integrasi early-warning cuaca/BMKG utk keselamatan trip nelayan | [S1] |

---

## 28. Relevance terhadap Software yang Akan Dibangun

### Bisa diadopsi
- Model **3-in-1** (oseanografi + AIS + prediksi AI) dalam satu app mobile — pola integrasi yang jelas dan mudah dipahami nelayan.
- **Skema harga berjenjang** (Free/Pro/Enterprise) + onboarding 3 langkah.
- Praktik **explainability** dan **probability score** dari GreenFish (user tahu "mengapa" dan "seberapa yakin").
- Monitoring update reguler (6 jam) & horizon prediksi.

### Bisa dikembangkan
- Localisasi data Indonesia: WPPNRI, bathymetry, coastline, pelabuhan, E-Logbook/STELINA, moda VMS + AIS + VIIRS/SAR — yang masih kosong di Marisikan.
- Feedback loop riil dari nelayan (hasil tangkapan aktual) utk kalibrasi per wilayah/WPPNRI.
- Mekanisme keselamatan (weather warning, SOS).

### Harus dihindari
- **Kurangnya transparansi data/metode** — Marisikan menjual tanpa spesifikasi sumber, resolusi, dan validasi utk perairan target. Jangan diulang: tetap publikasikan basis data, metode, dan angka validasi.
- Mengklaim akurasi tanpa bukti terverifikasi (risiko kredibilitas; vendor GreenFish juga enggan mempublikasikan angka yang bisa dicek ([S1][S5]).
- Bergantung pada satu vendor teknologi kompleks (superkomputer) yang mahal — pertimbangkan komputasi terjangkau.

### Potential Differentiator
- **Fokus WPPNRI + data nasional Indonesia** yang absen di Marisikan;
- **Integrasi multi-sensor** (VMS + AIS + VIIRS + SAR) + oseanografi dalam satu alur keputusan;
- **Feedback loop closed-loop** utk nelayan kecil (termasuk yang tanpa AIS);
- **Transparansi & validasi** yang bisa diverifikasi per musim.

---

## 29. Final Summary

| Aspek | Temuan |
| --- | --- |
| Main purpose | Membantu nelayan Indonesia menangkap lebih efisien dgn gabungan oseanografi real-time + AIS + prediksi AI (Marisikan by GreenFish) [S1] |
| Target user | Nelayan Indonesia (individu s/d armada enterprise) [S1] |
| Strongest capability | Prediksi fishing ground + visualisasi oseanografi dalam app mobile; teknologi prediksi GreenFish teruji di pasar global [S1][S5][S9] |
| Main data | SST, arus, salinitas, klorofil/plankton, cuaca, AIS (sumber/resolusi tidak didokumentasikan) [S1] |
| Main intelligence | Fishing ground prediction (heatmap, spesies, waktu, rute) + vessel tracking AIS [S1] |
| Prediction | Prediksi lokasi/spesies/waktu (klaim); horizon & akurasi utk Indonesia tidak dipublikasikan [S1] |
| Historical analysis | Terbatas: "data historis" (paket Pro 30 hari); tidak ada trend/seasonsal utk nelayan [S1] |
| Vessel intelligence | Level tracking saja via AIS; tidak ada analisis perilaku/dark vessel/VMS [S1] |
| Fisher decision support | Ya (rekomendasi zona/rute), namun tanpa bukti desain UX nelayan skala kecil & keselamatan [S1] |
| Main limitation | Dokumentasi sangat minim: sumber data, metode, validasi, arsitektur, privasi — semuanya tidak publik [S1] |
| Biggest gap | Integrasi data nasional Indonesia (WPPNRI, VMS, E-Logbook/STELINA, bathymetry, coastline) + feedback loop + validasi lokal [S26] |
| Potential novelty | Gap antar Marisikan & kebutuhan Anda: sistem decision-support WPPNRI yang menggabungkan oseanografi historis + AIS/VMS + VIIRS/SAR + data tangkapan dengan kalibrasi lokal & transparan [S27] |

### 5–10 Insight Terpenting
1. **Marisikan adalah permukaan dari GreenFish** — landing page pemasaran lokal; detail teknis hanya ada di produk induk B2B. Jangan menggeneralisasi fitur GreenFish sebagai Marisikan secara otomatis.
2. **Model 3-in-1 (hentikan data ganda)** sudah menjadi *market trend* yang divalidasi bahkan oleh analis pihak ketiga (Noah Intelligence, Juni 2026) [S10].
3. **Kekuatan utama = model prediksi operasional** (8 hari, refresh 6 jam, diklaim 75–92%) — tetapi klaim vendor tanpa peer-review; Anda dapat membedakan diri lewat validasi transparan.
4. **Kekosongan data nasional Indonesia** (WPPNRI, EEZ/MPA, bathymetry, coastline, VMS, E-Logbook) yang tidak diintegrasikan Marisikan adalah ruang gap terbesar Anda.
5. **Mayoritas nelayan Indonesia adalah kapal kecil tanpa AIS** — fokus AIS saja (seperti Marisikan) mengabaikan sebagian besar target pengguna; peluang integrasi VMS/SAR/optical deteksi.
6. **Feedback loop** terbukti jadi nilai di GreenFish (logbook → model lebih baik); desain end-to-end dari hasil tangkapan aktual ke model.
7. **Explainability** menjadi pembeda: GreenFish "unpacks" variabel penyebab; bawa ke konteks nelayan lokal (bahasa, sederhana).
8. **Hindari kemasan tanpa substansi** — transparansi sumber data, resolusi, dan validasi akan menjadi nilai jual berbeda dari Marisikan.
9. **Model bisnis** berjenjang (gratis/pro/enterprise + API) terbukti layak secara komersial di Indonesia via Marisikan.
10. **Keselamatan (weather/SOS) kosong di Marisikan** — fitur yang bisa menjadi pembeda positif bagi nelayan kecil.

---

## 30. DAFTAR REFERENSI

| # | Author / Organization | Tahun | Judul | Jenis | URL/DOI | Aspek yang didukung |
| --- | --- | --- | --- | --- | --- | --- |
| [S1] | GreenFish | 2025 | Marisikan – Teknologi Laut untuk Nelayan Indonesia | Website resmi Marisikan | https://www.marisikan.com/ | Profil, fitur (oseanografi/AIS/AI), harga, target, status |
| [S2] | GreenFish | 2026 | GreenFish – A New Approach To Fishing (home/FAQ/about) | Website resmi GreenFish | https://www.greenfish.is/ ; /about ; /faq | Model 8 hari/6 jam, heatmap, CPUE, satelit AIS Kpler, 100+ variabel, bukti kasus, explainability, feedback loop, kebijakan data |
| [S3] | GreenFish (LinkedIn) | 2026 | GreenFish company profile | Profil perusahaan (secondary) | https://linkedin.com/company/fishgreen | Didirikan 2023, lokasi, deskripsi platform |
| [S4] | GreenFish | 2026 | GreenFish – Navigation App | Marketing (MWM listing) | https://mwm.ai/apps/greenfish/6780506414 | App GreenFish: layer oseanografi/termal front/depth, AIS Kpler, offline, catch logging |
| [S5] | Bonnie Waycott / Global Seafood Alliance | 2025 | 'Here to stay and evolving fast': How GreenFish's AI-powered fish-forecasting tech is modernizing commercial fisheries | Artikel jurnalistik kredibel (Advocate) | https://www.globalseafood.org/advocate/here-to-stay-and-evolving-fast-how-greenfishs-ai-powered-fish-forecasting-tech-is-modernizing-commercial-fisheries/ | Data ESA & NASA, logbook historis, 8 hari, akurasi 75–92%, bycatch, pH eksplisit "suggestion bukan suruhan", pendirian 2023 |
| [S6] | Enterprise Europe Network (EC) | 2026 | Finding fish is no longer a guessing game with AI-driven location forecasting | Publikasi institusional UE | https://een.ec.europa.eu/success-stories/finding-fish-no-longer-guessing-game-ai-driven-location-forecasting | 10-day forecast/species, supercomputing, pendanaan EU €350k |
| [S7] | World Fishing | 2025 | GreenFish forecasting tool helps Icelandic fleet tackle mackerel's uncertainty | Media perdagangan perikanan | https://www.worldfishing.net/fishing-technology/greenfish-forecasting-tool-helps-icelandic-fleet-tackle-mackerels-uncertainty/1504469.article | Data "decades of satellite & fishing data", superkomputer, hasil kuota user GreenFish, penghargaan |
| [S8] | World Fishing | 2026 | GreenFish AI drives fleet efficiency | Media perdagangan | https://www.worldfishing.net/news/fishing-technology/greenfish-ai-drives-fleet-efficiency/ | Model inti: lokasi, kuantitas, ukuran, bycatch — akurasi min. 75% |
| [S9] | ATUNA | 2026 | How Predictive AI Gives Fishing Companies A Competitive Edge | Media berita industri tuna | https://www.atuna.com/news/how-predictive-ai-gives-fishing-companies-a-competitive-edge/ | Patent-pending, 6 jam update, 75–92%, model eksklusif per klien |
| [S10] | Craig Paige / Noah Intelligence | 2026 | GreenFish's AI forecasts boost global fishing efficiency | Berita pihak ketiga (analisis bisnis) | https://noah-news.com/greenfishs-ai-forecasts-boost-global-fishing-efficiency-with-exclusive-models-an/ | Satu-satunya sumber pihak ke-3 yang menyebut Marisikan (mengutip marisikan.com) |
| [S11] | Kpler (via GreenFish) | 2026 | Satellite AIS (referensi utk provider AIS) | Klaim vendor di situs GreenFish | https://www.greenfish.is/ | "Satellite AIS by Kpler" |

**Catatan keandalan sumber:** [S1][S2][S3][S4] adalah sumber vendor (resmi), [S5][S6][S7][S8][S9][S10] media/institusi pihak ketiga yang mengutip klaim vendor. Tidak ada paper ilmiah peer-review yang menjelaskan Marisikan/GreenFish yang ditemukan dalam riset ini. Klaim kuantitatif (akurasi, ROI, fuel saving) semuanya berasal dari klaim vendor dan dilaporkan media sebagai klaim → diperlakukan sebagai **[INDICATED]**, bukan bukti independen.

---

### Aturan Final — Pemeriksaan Evidence

- **Sumber primer langsung**: Marisikan hanya punya website pemasaran (marisikan.com). Tidak ditemukan dokumentasi resmi (docs), API docs, paper, repository, atau laporan pemerintah yang membahas Marisikan.
- **Tidak ada angka yang dikarang**: akurasi 75–92%, 8 hari/10 hari, fuel saving, ROI — semuanya klaim GreenFish yang dilaporkan media, diberi status [INDICATED], dan dicatat konflik horizon (8 vs 10 hari) tanpa memilih secara diam-diam.
- **Tidak ada fitur yang ditambahkan dari dugaan**: VMS, VIIRS, SAR, MODIS, SSH, WPPNRI, MPA, bathymetry diberi status ? / tidak disebut, bukan asumsi ada.
- **Perbedaan status evidence** dipertahankan: [CONFIRMED] (klaim fitur dari situs Marisikan/GreenFish), [INDICATED] (GreenFish utk Marisikan / laporan media), [UNKNOWN] (tidak terdokumentasi).