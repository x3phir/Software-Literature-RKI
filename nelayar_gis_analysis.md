# NELAYAR (nelayar-gis)

> Laporan dibuat berdasarkan aturan anti-asumsi: setiap klaim faktual diberi status evidence **[CONFIRMED]** (ada sumber langsung di kode/repo), **[INDICATED]** (indikasi kuat/evidence tidak langsung), atau **[UNKNOWN]** (tidak dapat diverifikasi).
>
> **Catatan penting:** Berbeda dari Marisikan (produk komersial tertutup), `nelayar-gis` adalah **repository open-source publik** di GitHub (`brianabdl/nelayar-gis`). Seluruh klaim dalam laporan ini dapat dilacak ke kode sumber—ini keunggulan sekaligus perbedaan metodologi: evidence level [CONFIRMED] di sini berarti "terbaca langsung dari kode/repo", bukan sekadar klaim pemasaran.
>
> **Repo di-kloning ke direktori kerja lokal** `C:\Users\Harri Supriadi\AppData\Local\Temp\opencode\nelayar-gis` (branch `master`, clone dangkal). Nomor baris file yang dikutip mengacu pada kondisi repo saat analisis.

---

## 1. Profil Software

| Aspek | Informasi | Evidence / Sumber |
| --- | --- | --- |
| Nama | **Nelayar** ("Nelayar 🌊") | README.md [S1] |
| Judul resmi | "An Integrated Web GIS Platform with Oceanographic Forecasting Data for Precision Pelagic Fishing" | README.md [S1] |
| Developer / Institution | `brianabdl` (akun GitHub publik); afiliasi akademik tidak dicantumkan di repo; pencarian web (Sept 2026) tidak menemukan publikasi/paper resmi dari author maupun proyek → afiliasi [UNKNOWN] | Repo root [S1], web [W2] |
| Tahun pengembangan | File migrasi/seed bertanggal Mei–Juni 2026; komit terakhir yang terclone "fix(config): update default timezone to Asia/Jakarta" tertanggal 2026-08-03 (clone dangkal—riwayat lengkap tidak dapat diverifikasi); tidak ditemukan publikasi ilmiah resmi yang menyertai proyek [UNKNOWN] | Migrasi [S10], `git log` [S13], web [W2] |
| Negara | Indonesia (bahasa antarmuka & komentar kode didominasi Bahasa Indonesia; bbox perairan Indonesia; TZ Asia/Jakarta) | Kode [S2][S3][S5][S9] |
| Platform | Web GIS (mobile-first) + PWA offline; bukan aplikasi native | README [S1], package.json [S11] |
| Lisensi | Tidak ditemukan file LICENSE di repo terclone ([UNKNOWN]) | Repo [S1] |
| Target pengguna | Nelayan Indonesia ("designed to improve the efficiency and catch rates of fishermen", "accessible from their smartphones while at sea") | README.md [S1] |
| Tujuan utama | Prediksi zona penangkapan pelagis berbasis data oseanografi satelit (CMEMS) + navigasi & estimasi biaya operasional | README [S1], kode [S2][S3][S4] |
| Geographic scope | Perairan Indonesia (bbox lat −11..+6, lon 95..141) | parse_zppi.py [S2], OceanService [S3] |
| Status | **Aktif & open-source**; dapat dijalankan sendiri (Docker Compose + GitHub Actions) | docker-compose.yml [S11], workflows [S8] |

---

## 2. Fokus dan Tujuan

**Masalah yang ingin diselesaikan** (dari README [S1]): efisiensi dan hasil tangkapan nelayan melalui "precision pelagic fishing"—memvisualisasikan data oseanografi untuk merekomendasikan zona penangkapan.

**Tujuan utama** (dikonfirmasi dari kode [S2][S3][S4][S7]):
1. Mengunduh data SST & Chlorophyll-a dari **CMEMS/Copernicus Marine** setiap hari,
2. Menghitung zona potensi ikan (ZPPI = Zona Prakiraan Potensi Ikan) per spesies pelagis lewat pencocokan envelope suhu/klorofil,
3. Menyajikan zona + overlay raster SST/Chl + prakiraan 10 hari di peta web interaktif,
4. Mendukung keputusan operasional: rute pelayaran bebas daratan, cuaca per zona, estimasi biaya BBM,
5. Memonitor harga ikan pasar (KKP) untuk keputusan menjual.

**Klasifikasi fokus** (dikonfirmasi dari kode):

| Aspek | Fokus? | Evidence |
| --- | --- | --- |
| Fishing ground prediction | ✅ Inti produk—zona ZPPI per spesies | [S2][S3] |
| Fishing activity / effort | ❌ tidak ada (tidak ada data tangkapan/effort) | seluruh kode [S2–S11] |
| Vessel monitoring | ❌ tidak ada AIS/VMS (**pembeda dari Marisikan/GeeenFish**) | seluruh kode [S2–S11] |
| Fisheries management | ❌ tidak ada | seluruh kode [S2–S11] |
| Conservation / bycatch | ❌ tidak ada | seluruh kode [S2–S11] |
| Decision support | ✅ zona + rute + cuaca + biaya BBM + harga jual | [S3][S4][S5][S6][S7] |

> Karakter: Nelayar **bukan** platform pengelolaan perikanan dan **tidak** melacak kapal. Fokusnya murni pada **fishing ground intelligence sebagai decision-support nelayan kecil-menengah**.

---

## 3. Data Sources

| Data | Digunakan? | Sumber Data | Resolusi & Temporal | Fungsi | Evidence |
| --- | --- | --- | --- | --- | --- |
| Sea Surface Temperature (SST) | ✅ | **CMEMS** `GLOBAL_ANALYSISFORECAST_PHY_001_024`, dataset `cmems_mod_glo_phy-thetao_anfc_0.083deg_P1D-m` (analysis forecast harian, var `thetao`) | ~0.083° grid; harian (H+0..H+9 diunduh per tanggal) | input utama model ZPPI + overlay raster | [S2] lines 100–107; README [S1] |
| Chlorophyll-a (Chl) | ✅ | **CMEMS** `GLOBAL_ANALYSISFORECAST_BGC_001_028`, dataset `cmems_mod_glo_bgc-pft_anfc_0.25deg_P1D-m` (var `chl`) | ~0.25° grid; harian; **opsional**—jika gagal/tersedia fallback SST-only | input model (spesies 'chl_required') + overlay raster | [S2] lines 112–125 |
| Weather (suhu udara, angin, cuaca) | ✅ | **Open-Meteo** forecast API (`api.open-meteo.com/v1/forecast`, daily) | klamp [today..H+9]; TTL 60 mnt | kartu cuaca per zona | [S5] |
| Gelombang (wave height) | ✅ | **Open-Meteo Marine API** (`marine-api.open-meteo.com`, `wave_height_max`) | harian; gagal → 0 | parameter keselamatan/cuaca | [S5] |
| Harga ikan | ✅ | **mi.kkp.go.id** (dashboard internal KKP, endpoint `api_harga_dashboard.php`)—scraping tanpa lisensi resmi | 5 komoditas × ~34 provinsi; snapshot + riwayat 12 bulan | halaman/monitor harga & peta choropleth | [S7] |
| Harga BBM (Pertalite & Biosolar subs.) | ✅ | **bensin-api** (GitHub `nasgunawann/bensin-api`) | harian (TTL 6 jam) | estimasi biaya BBM per perjalanan | [S6] |
| Reverse-geocoding provinsi | ✅ | **Nominatim (OpenStreetMap)** | TTL 30 hari | deteksi provinsi asal untuk harga BBM | [S6] |
| Daratan (coastline/land boundary) | ✅ | file `storage/app/public/indonesia_land.geojson`—**provenans asli file tidak didokumentasikan** | vektor | pemotongan poligon zona agar tidak menembus darat (ST_Difference) | LandBoundarySeeder [S10] |
| Basemap peta | ✅ | **CARTO Voyager** (online) + **Protomaps PMTiles** (offline, `build.protomaps.com`, bbox 95,−11,141,6 z0–10) | vektor offline ~30–60 MB | navigasi offline | [S11] |
| Jaringan rute laut | ✅ | graf **`marnet.geojson`** (asal: pustaka searoute; disalin ke `/geo/marnet.geojson`) | global marine network | routing server (searoute-py) + Dijkstra offline di browser | [S11][S4] |
| MODIS / VIIRS / SAR / Sentinel / SSH / salinitas / arus / bathymetry | ❌ | — | — | — | seluruh kode [S2–S11] |

> Sumber SST/Chl sesungguhnya adalah **analysis/forecast (anfc) harian CMEMS**, bukan sensor satelit optik langsung (meski data CMEMS sendiri dibangun dari gabungan asimilasi satelit/in-situ). Tidak ada MODIS/VIIRS/SAR/SSH/arus/salinitas/bathymetry dalam repo.

---

## 4. Data Acquisition

| Tahap | Mekanisme | Detail | Evidence |
| --- | --- | --- | --- |
| CMEMS SST + Chl | Streaming via pustaka **`copernicusmarine.open_dataset()`** langsung ke xarray (tanpa menyimpan NetCDF) | filter bbox −11..6 / 95..141 + window tanggal; kredensial dari env `CMEMS_USERNAME/PASSWORD` | parse_zppi.py [S2] lines 95–127 |
| Weather | HTTP GET Open-Meteo (forecast) + Marine (gelombang) | timezone Asia/Jakarta; periode 1 hari; timeout 10 s; fallback `mock_data` (dummy hardcoded) | WeatherService [S5] |
| Harga KKP | Scraping JSON via **HTTP session + retry** (3x, backoff, 500/502/503/504) pada `api_harga_dashboard.php` | 5 komoditas: Tongkol, Kembung, Bandeng, Teri, Udang Basah; actions `get_prov_summary`/`get_kab_summary`/`get_region_trend`; ±340 panggilan; tanggal periode diambil dari `meta.periode` API (bukan hari ini) | scrape_kkp.py [S7] |
| Harga BBM | HTTP `bensin-api` (provinsi + nasional) | geocode Nominatim (zoom 8) utk provinsi; rata-rata nasional sebagai fallback saat titik di laut | FuelPriceService [S6] |
| Routing | Panggil proses Python `route_sea.py` via Laravel `Process::run`, timeout 60 s | arg `--start=lat,lon --end=lat,lon` (bentuk `=` agar aman untuk lintang negatif) | RouteService [S4] |
| Penjadwalan | `schedule:work` di docker (server): `ocean:sync-forecast` 02:00 harian; `nelayar:scrape-kkp` tanggal 1 bulanan 03:00 | variabel `ZPPI_SYNC_TIME`, `KKP_SCRAPE_DAY` | config/schedule.php + docker-compose scheduler [S9][S11] |
| Komputasi di CI | GitHub Actions `ocean-sync` **setiap jam** (`cron '0 * * * *'`, timeout 120 mnt) mengunduh CMEMS & menghitung ZPPI di runner luar server | upload hasil (JSON+PNG) via rsync → SSH → docker compose cp → `ocean:ingest` | [S8] |

> Pola menarik: **data berat dikumpulkan/dihitung di GitHub Actions (4 vCPU/16GB)**, server produksi hanya menerima hasil jadi (INSERT PostGIS ringan). Ini kontras dengan Marisikan yang tidak mempublikasikan arsitektur sama sekali.

---

## 5. Data Processing

Pipeline (dikonfirmasi dari parse_zppi.py [S2] + OceanService.php [S3]):

1. **Ekstraksi variabel** `thetao` (depth=0) & `chl` → array numpy; rata-rata over `time` jika ada 2+ stempel waktu; log rentang untuk cek unit (°C vs Kelvin). [S2]
2. **Resampling ke grid master** ~0.027° (~3 km; `res = 0.027`): SST dengan `RegularGridInterpolator(method='linear')`, Chl dengan `method='nearest'` (Chl asli 0.25° → dinaikkan ke 0.027°). Grid master ≈ 629×1704 sel (17°×46°). [S2] lines 167–200
3. **Overlay PNG** disimpan per tanggal di `storage/app/public/grids/{date}/`: `sst_raster.png` (cmap jet, vmin 26, vmax 32), `chl_raster.png` (cmap YlGn, vmin 0, vmax 1, smooth gaussian σ=2, latar transparan). Path PNG disimpan ke tabel `ocean_data`. [S2] lines 18–33, 180–200
4. **Pemetaan kepatuhan spesies** per piksel → bitmask `composition_grid` (`uint32`, 1 bit per spesies, hingga 32 spesies).
5. **Vektorisasi zona** via `rasterio.features.shapes(connectivity=8)` + filter luas `MIN_AREA = res²·5 ≈ 0.0036°²` + `unary_union` → `MultiPolygon`.
6. **Statistik per zona dalam satu lintasan** (`rasterize` label + `scipy.ndimage.mean`) → `sst_rata`, `chl_rata`, rata-rata confidence per spesies utk `ikan_cocok` (urut confidence menurun; `ikan_utama` = teratas).
7. **Pemotongan daratan di database**: PostGIS `ST_MakeValid(ST_Difference(geom, union land_boundaries))` saat INSERT. [S3] lines 142–157
8. **Sliding window**: data dengan `zone_date < hari ini` dihapus (DB + folder PNG); window diisi H+0..H+9. [S9]

| Data | Raw → Processed | Evidence |
| --- | --- | --- |
| SST 0.083° → grid 0.027° (linear) | raster + input confidence | [S2] |
| Chl 0.25° → 0.027° (nearest) + smooth | raster + input confidence | [S2] |
| Grid → polygon (per spesies envelope) | zona ZPPI, ikan_cocok, sst_rata/chl_rata | [S2][S3] |
| Polygon → PostGIS → dipotong daratan | zona final bounds di laut | [S3] |

---

## 6. Feature Engineering

| Raw → Derived → Intelligence | Status | Evidence |
| --- | --- | --- |
| SST & Chl aktual → **envelope matching** (envelope statis per spesies) → zona potensi | [CONFIRMED] — bukan variabel turunan; hanya banding nilai terhadap ambang literatur | [S2] |
| Posisi nilai dalam envelope → **skor confidence sintesis** (`1 − |x−mid|/half·0.5`; gabungan SST+Chl rerata) | [CONFIRMED] | [S2] lines 51–90 |
| Rata-rata zona (`sst_rata`, `chl_rata`) → tampilan parameter per zona | [CONFIRMED] | [S2][S3] |
| Bitmask per piksel (spesies mana yang cocok) → zona dengan daftar spesies (`ikan_cocok`) | [CONFIRMED] | [S2] |
| Anomali SST, gradien suhu, frontal zone, upwelling index, SAR—**tidak ada** | [CONFIRMED] tidak ada di kode | [S2] |

> Feature engineering **tidak ada** (hanya raw value + threshold). Tidak ada variabel turunan oseanografi (anomali, front, gradient). Confidence adalah **skor geometris sintesis**, bukan output model belajar.

---

## 7. Computational Method / Algorithm

**Ini aspek paling penting untuk benchmarking.**

`parse_zppi.py` menggunakan **model berbasis aturan (rule-based) deterministik**, yang disebut di domain perikanan Indonesia sebagai pendekatan **Habitat Suitability Index (envelope) / ambang ZPPI**. **TIDAK ada machine learning** (tanpa training, tanpa label, tanpa model statistik/fit terhadap data tangkapan) meskipun README menyebut "AI/Catch Logic". [S2] vs [S1].

| Method | Input | Output | Purpose | Evidence |
| --- | --- | --- | --- | --- |
| **Rule-based envelope matching (HSI biner)** per spesies | SST & Chl pada grid 0.027° + envelope `[sst_min,sst_max]`, `[chl_min,chl_max]` dari `fish_profiles` | mask piksel cocok per spesies | deteksi zona potensial tiap spesies | [S2] lines 51–90 |
| **Confidence sintesis (triangular membership)** | nilai SST/Chl vs midpoint/half-range envelope | `sst_conf ∈ [0.5,1.0]`; `combined=(sst_conf+chl_conf)/2` jika Chl wajib | peringkat "kesesuaian" dalam zona | [S2] lines 59–89 |
| **Komposisi bitmask + vektorisasi raster** | grid gabungan semua spesies | polygon zona (`MultiPolygon`), `ikan_cocok` per zona | representasi spasial zona | [S2] lines 202–317 |
| **Perutean lintas daratan** | graf jaringan laut (`searoute` / `marnet.geojson`) | LineString rute + jarak (km/naut/miles) | navigasi ke zona | [S4][S11] |
| **Dijkstra offline di browser** | graf laut yang sama | rute server-equivalent saat offline (+ garis lurus `approximate` sbg fallback) | navigasi tanpa internet | [S11] |
| **Merupakan ML?** | — | **Tidak.** Semua deterministik, parameter statis dari seeder literatur | — | [CONFIRMED] [S2][S10] |

Rumus exact (lines 59–89 [S2]):
```
sst_mask  = (sst_min ≤ SST ≤ sst_max)
sst_conf  = 1 − |SST − sst_mid| / sst_half × 0.5      (nilai 1.0 di tengah, 0.5 di tepi envelope)
chl_conf  = sama untuk Chl (hanya jika chl_min>0 dan dipakai)
combined  = (sst_conf + chl_conf) / 2                  (gabungan saat Chl wajib)
sst_rata / chl_rata = rata-rata zona via scipy.ndimage.mean
```

> Klaim README "AI/Catch Logic: Probability and prediction" [S1] **tidak sesuai** dengan implementasi. Ini perlu dicatat sebagai perbedaan klaim vs kenyataan—sekaligus kejujuran penting: hasilnya skor kesesuaian lingkungan, bukan probabilitas hasil tangkapan yang diukur.

---

## 8. Fishing Intelligence

### A. Fishing Ground Intelligence
- ✅ **Potential fishing ground** per spesies (zona polygon) — inti sistem. **[CONFIRMED]** [S2][S3]
- ✅ **Species-specific**: 18 spesies pelagis dikelompokkan kecil/transisi/besar: Kembung, Layang, Lemuru, Selar, Tenggiri, Kuwe, Lemadang (Mahi-Mahi), Barakuda, Sunglir, Cakalang, Tongkol, Tuna Sirip Kuning, Tuna Mata Besar, Tuna Kecil, Marlin Hitam, Layaran (Sailfish), Tuna Sirip Biru, Todak. **[CONFIRMED]** [S10]

### B. Fishing Activity Intelligence
- ❌ Tidak ada sama sekali (tanpa data tangkapan/AIS/effort) [S2–S11]

### C. Vessel Intelligence
- ❌ Tidak ada AIS/VMS/tracking kapal apa pun [S2–S11]

### D. Environmental Intelligence
- ✅ SST & Chl (CMEMS) + cuaca + gelombang per koordinat. **[CONFIRMED]**
- ❌ Tidak ada front, upwelling, arus, salinitas, SSH, bathymetry [S2–S11]

### E. Temporal Intelligence
- ✅ Prakiraan 10 hari (H+0..H+9) sliding window dengan slider waktu. **[CONFIRMED]** [S9][S11]
- ❌ Tidak ada analisis historis/musiman (data masa lalu sengaja dihapus) [S9]

---

## 9. Prediction Target

| Prediction Target | Input | Output | Unit | Accuracy | Evidence |
| --- | --- | --- | --- | --- | --- |
| Zona potensi ikan per spesies (kombinasi) | SST/Chl forecast CMEMS + envelope spesies | polygon zona + `ikan_cocok` ber-rank + `ikan_utama` | zona (poligon) | **tidak divalidasi**; confidence = skor sintesis | [S2][S3] |
| Skor confidence | nilai SST/Chl dalam envelope | 0.5–1.0 per spesies per zona | skalar | bukan probabilitas terukur | [S2] |
| `confidence` global (kolom zppi_zones) | fraksi piksel matching seluruh domain | ~persentase wilayah cocok; **disalin ke SEMUA zona pada tanggal itu** | persen | tidak divalidasi | [S2] result + [S3] insert |
| Prakiraan cuaca/gelombang per zona | Open-Meteo | deskripsi cuaca, suhu, angin, tinggi gelombang | °C / km/j / m | tidak divalidasi | [S5] |
| Jarak & biaya perjalanan | searoute + harga BBM | km + jam ETA + Rp | — | asumsi kecepatan 18 km/j, 0.4 L/km | [S4][S6][S11] |
| Harga & trend ikan | scraping KKP | avg/max/min, ticker, trend 12 bulan | Rp | data dari dashboard KKP | [S7] |

> **Tidak ada validasi terhadap tangkapan aktual** di mana pun dalam repo (tidak ada field hasil tangkapan, tidak ada ground truth). Prediksi = kesesuaian habitat *envelope*, bukan probabilitas tangkapan.

---

## 10. Spatial Intelligence

| Capability | Ada? | Evidence |
| --- | --- | --- |
| Interactive map web | ✅ Leaflet (react-leaflet) | [S11] |
| Marker zona (centroid) + poligon penuh saat klik (lazy) | ✅ `ST_PointOnSurface` centroid utk muatan ringan; poligon penuh per zona via `/api/map/zone/{id}` | [S3] lines 187–234 |
| Marker clustering (leaflet.markercluster dependency) | 🎯 indikasi kuat (`markercluster` di package.json; `ZppiLayer`) | [S11] |
| Overlay raster SST/Chl (PNG hasil Python) | ✅ layer toggle "Processed / SST / Chl" | [S2][S11] |
| Pemotongan daratan (TIDAK menembus darat) | ✅ `ST_Difference` vs `land_boundaries` di PostGIS | [S3][S10] |
| Pencarian wilayah (Nominatim, countrycodes=id) + fly-to | ✅ | [S11] |
| Pencarian ikan (indeks dari `ikan_cocok`, filter zona) | ✅ `buildFishIndex`; badge "N Zona" | [S11] |
| Locate (posisi GPS nelayan) | ✅ `LocateControl` + watchPosition saat navigasi | [S11] |
| Rute laut (menghindari darat) | ✅ searoute server + Dijkstra offline + straight-line fallback berlabel `approximate` | [S4][S11] |
| Basemap offline PMTiles z0–10 | ✅ fallback otomatis ke CARTO online | [S11] |
| WPP / EEZ / MPA / bathymetry / pelabuhan layer | ❌ tidak ada | [S2–S11] |
| Analisis spasial (jarak ke port, densitas, hotspot statistik) | ❌ tidak ada | [S2–S11] |

---

## 11. Temporal Intelligence

| Capability | Ada? | Evidence |
| --- | --- | --- |
| Forecasting | ✅ Prakiraan H+0..H+9 (10 hari) sliding window; refresh harian (CI tiap jam) | [S9][S8] |
| Time slider di map | ✅ slider 0..9 ("Sekarang ... H+9 (Maks)"), drag instan + commit server | [S11] |
| Cuaca clamp ke jendela forecast | ✅ normalizeDate → [today, H+9] | [S5] |
| Cache offline seluruh 10 hari di IndexedDB | ✅ sync.ts 10 hari + raster + basemap | [S11] |
| Historical oceanographic data | ❌ **sengaja dihapus** (sliding window `zone_date < hari ini` di-delete) | [S9] |
| Seasonal / annual / long-term trend | ❌ tidak ada | [S2–S11] |
| Trend harga ikan (bulanan) | ✅ 12 bulan, MoM change, ticker | [S7] |
| Anomaly detection | ❌ tidak ada | [S2–S11] |

> Pertanyaan "apa yang terjadi di lokasi ini 3 bulan lalu?" **tidak dapat dijawab** — data masa lalu dibuang demi keringanan penyimpanan. Ini celah temporal utama.

---

## 12. AIS / VMS / Vessel Intelligence

- **AIS:** ❌ tidak ada.
- **VMS:** ❌ tidak ada.
- **Vessel data / behavior / fusion:** ❌ tidak ada.
- Tidak ada tracking, identifikasi kapal, zona penangkapan aktif, dark vessel, dst.

> Ini perbedaan paling mencolok vs Marisikan/GreenFish yang mengandalkan AIS ("lacak ribuan kapal"). Nelayar **murni lingkungan-ke-aplikasi tanpa dimensi kapal**. Baik untuk dianggap (a) gap, atau (b) keunggulan privasi/keterbatasan kapal kecil non-AIS.

---

## 13. Decision Support

Skala 1–5 terhadap Nelayar:

| Level | Capability | Status |
| --- | --- | --- |
| 1 | Raw data visualization | ✅ [CONFIRMED]—marker zona, raster SST/Chl, weather card [S2][S5][S11] |
| 2 | Data interpretation | ✅ [CONFIRMED]—zona potensi + spesies + skor confidence (sudah interpretasi) [S2][S3] |
| 3 | Prediction | ✅ [CONFIRMED]—zona & spesies prediksi per tanggal H+0..H+9 [S2][S9] |
| 4 | Recommendation | ✅ [CONFIRMED]—rute navigasi ke zona, estimasi biaya BBM pulang-pergi, harga jual ikan [S4][S6][S7] |
| 5 | Operational decision support | ✅ [CONFIRMED]—mode navigasi aktif: GPS tracking, ETA mundur, proyeksi ke rute, re-routing >2 km menyimpang dgn cooldown 20 s, peta mengikuti perahu ("Zen Mode") [S11] |

> Dari kelima level, **Nelayar mengimplementasikan level 5 secara nyata** (lebih dalam dari Marisikan yang hanya "klaim rekomendasi rute"). Yang tidak ada: keselamatan (SOS/peringatan cuaca ekstrem aktif) dan feedback tangkapan.

---

## 14. Fisher User Experience

| Aspek | Keterangan | Evidence |
| --- | --- | --- |
| Interface utk nelayan | ✅ mobile-first, touch, single-hand, layout responsive desktop/mobile | [S11] |
| Bahasa lokal | ✅ Bahasa Indonesia (label, kompas U/TL/T/TG/S/BD/B/BL, deskripsi cuaca WMO→ID) | [S5][S11] |
| Offline mode | ✅ **PWA** (Workbox) + IndexedDB 10 hari + basemap vektor offline + rute offline | [S11] |
| Low-bandwidth friendly | ✅ payload ringan: marker centroid (bukan poligon penuh) utk muatan awal; raster PNG di-cache | [S3][S11] |
| GPS / navigasi | ✅ watchPosition, marker posisi, "Mulai Navigasi", ETA & sisa jarak | [S11] |
| Recommended fishing area | ✅ zona ZPPI + filter spesies | [S2][S11] |
| Weather card per zona | ✅ + flag out-of-window; fallback mock jika API gagal (lihat Limitation) | [S5] |
| Safety warning (SOS) | ❌ tidak ada | [S2–S11] |
| Catch recording / input nelayan | ❌ tidak ada | [S2–S11] |
| Feedback nelayan | ❌ tidak ada | [S2–S11] |
| Est. biaya & harga | ✅ rute → biaya BBM (solar/pertalite) + link "Cek Harga" | [S6][S7][S11] |

**Klasifikasi:** **Fisher Decision Support Tool (B2C)** dengan fokus operasional harian nelayan kecil-menengah + **offline-first engineering** yang sangat langka di kelasnya.

---

## 15. Historical Intelligence

| Capability | Ada? | Evidence |
| --- | --- | --- |
| Historical oceanographic | ❌ sengaja tidak (sliding window) | [S9] |
| Historical fishing ground | ❌ tidak ada (skor harian dibuang) | [S9] |
| Historical prices | ✅ 12 bulan, per komoditas & provinsi; MoM; ticker | [S7] |
| Hotspot persistence / seasonal | ❌ tidak ada | [S2–S11] |
| Historical routing / vessel | ❌ tidak ada | [S2–S11] |

---

## 16. Validation & Accuracy

| Aspect | Result | Evidence |
| --- | --- | --- |
| Ground truth (catch data) | ❌ tidak ada | [S2–S11] |
| Validation method | ❌ tidak ada (tidak ada skrip test/validasi vs tangkapan; tidak ditemukan publikasi ilmiah resmi yang menyertai proyek) | [S2–S11], web [W2] |
| Envelope sumber | `fish_profiles` (ambang SST/Chl per spesies) di-seed sebagai tipe "KELOMPOK IKAN PELAGIS"; **sumber literatur tiap ambang tidak dicantumkan** — nilai-nilai tampak mengikuti pedoman ZPPI/KKP umum, tetapi tidak ada referensi | [S10] |
| Precission/Recall/F1/RMSE | ❌ tidak ada | [S2–S11] |
| Metadata quality | ✅ log rentang SST/Chl tiap run (cek unit °C vs Kelvin) ; warn saat 0 zona | [S2][S9] |
| Unit test / CI test | ❌ tidak ditemukan test suite PHP/Python di repo | [S8][S11] |

> **Temuan penting: nilai ambang (envelope) bersifat statis, dari seeder, tanpa referensi/lisensi/validasi lokal.** `confidence` adalah skor sintesis geometris (bukan probabilitas terkalibrasi). Ini harus dicatat eksplisit karena README menyebut hasil sebagai "Probability and prediction".
>
> **Konteks metode (dari luar repo, pelengkap konteks saja—BUKAN klaim bahwa Nelayar memakai metode tersebut):** pendekatan *knowledge-based/envelope+overlay ZPPI* yang dipakai Nelayar adalah pendekatan mapan dalam literatur perikanan Indonesia jangka panjang, mis. Sadly et al. (2009) melaporkan akurasi 85% vs data in-situ untuk model knowledge-based expert system GIS SST+SSC di Sulawesi. Artinya: arsitektur aturan yang dipakai Nelayar secara metodologis *bisa* divalidasi pola ini di masa depan, tetapi **Nelayar sendiri tidak melakukan validasi apa pun** [UNKNOWN] [W1].

---

## 17. Explainability

| Capability | Ada? | Evidence |
| --- | --- | --- |
| Alasan prediksi dijelaskan | ✅ **transparan secara desain** — model aturan terbuka; UI menampilkan `sst_rata`, `chl_rata` per zona + persentase kesesuaian per spesies | [S2][S11] |
| Feature importance / SHAP | ❌ tidak relevan (bukan ML) | [S2] |
| Probability / confidence ditampilkan | ✅ lingkaran persen per spesies di kartu zona; markernya `confidence` global | [S11] |
| Penjelasan teks (mengapa) | ❌ tidak ada narasi "karena suhu…" | [S11] |

---

## 18. Feedback Loop

| Langkah | Ada? | Evidence |
| --- | --- | --- |
| Prediction → Trip → Actual Catch → Feedback → Update | ❌ Tidak ada satu pun; tidak ada input hasil tangkapan, tidak ada learning. Envelope statis sampai di-edit manual di seeder | [S2][S10] |
| Sinkronisasi offline tiap tanggal me-refetch data server | ✅ reflex non-learning (client pull) | [S11] |

---

## 19. Technical Architecture

**Di sini keunggulan repo: arsitektur lengkap dan dapat diverifikasi.**

| Lapisan | Teknologi | Evidence |
| --- | --- | --- |
| Backend | **Laravel 12** (PHP), Eloquent, Inertia (SSR), Sanctum | package.json/migrations [S11][S10] |
| Komputasi ilmiah | **Python 3.12+ microservice** (`numpy`, `scipy`, `matplotlib`, `rasterio`, `shapely`, `copernicusmarine`, `searoute`) dikelola `uv` (`pyproject.toml`) | [S2][S11] |
| Database | **PostgreSQL + PostGIS 16/3.4** (Docker) | docker-compose [S11] |
| Cache & beberapa state | **Redis 7** (appendonly) — cache rute, BBM, queue | docker-compose + RouteService [S11][S4] |
| Frontend | **React 19 + TypeScript + Vite 8 + Tailwind v4 + Leaflet**; shadcn/ui-style components; framer-motion | package.json [S11] |
| PWA/offline | Workbox (service worker `/sw.js`), **Dexie/IndexedDB**, geojson-path-finder (Dijkstra klien), PMTiles + protomaps-leaflet, cache basemap `CacheFirst` + `rangeRequests` | [S11] |
| Deployment | **Docker Compose** (db, redis, app, web/nginx, queue, scheduler, init profile) + **GitHub Actions** (deploy & ocean-sync) | [S11][S8] |
| CI (compute-heavy) | `ocean-sync` tiap jam: uv sync → SSH ambil `fish_profiles` (source of truth) → hitung H+0..H+9 → rsync → `ocean:ingest` | [S8] |
| Komunikasi PHP↔Python | `Process::forever()/run()` granular; protokol stdout=JSON, stderr=log | [S3][S4][S7] |

**Alur data end-to-end:** CMEMS → `parse_zppi.py` (CI) → `{date}.json` + PNG → rsync/SSH → `ocean:ingest` (PostGIS INSERT + clipping darat) → `getGeoJsonByDate` (centroid) → Inertia/API → React Leaflet; offline: `bulkZones` → IndexedDB → peta offline.

---

## 20. API & Interoperability

| API / Data Access | Available? | Auth | Public? | Evidence |
| --- | --- | --- | --- | --- |
| `POST /api/auth/login|register|logout|user` | ✅ Sanctum token | bearer token | tanpa docs publik | [S12] |
| `GET /api/map/route` (searoute + fuel) | ✅ | Sanctum | hanya untuk app | [S12][S4] |
| `GET /api/map/weather` | ✅ | Sanctum | hanya untuk app | [S12][S5] |
| `GET /api/map/zones/bulk` (poligon penuh 10 hari utk offline) | ✅ | Sanctum | hanya untuk app | [S12][S3] |
| `GET /api/map/zone/{id}` (poligon lazy) | ✅ | Sanctum | hanya untuk app | [S12][S3] |
| `GET /api/prices` (paginated, filter, sort whitelist) | ✅ | Sanctum | hanya untuk app | [S12][S7] |
| Halaman Inertia: `/map`, `/weather`, `/prices`, Landing, Privacy | ✅ | auth utk map/weather/prices | — | [S12] |
| Public OpenAPI/Swagger/docs | ❌ tidak ada | — | — | [S2–S12] |
| Export/unduh data mentah | ❌ tidak ada endpooint khusus | — | — | [S2–S12] |

---

## 21. Data Governance, Security & Privacy

- **Otentikasi**: semua endpoint API di belakang `auth:sanctum` [S12]. Web session (database driver). Fitur tim/undangan dari starter kit.
- **Privasi pengguna**: halaman `/privacy` ada di frontend [S12][S11]—isi tidak dianalisis (halaman statis).
- **Kredensial**: CMEMS username/password sebagai secret CI (tidak di hardcode) [S8][.env.docker.example][S11].
- **Kebijakan penggunaan data KKP**(scraping dashboard) dan lisensi dataset CMEMS/OSM/Nominatim/Protomaps **tidak didokumentasikan dalam repo** — [UNKNOWN].
- **Kepemilikan data pengguna**: tidak ada logbook/sensor — data pengguna terbatas akun & preferensi; menarik bagi privasi kapal kecil (tidak ada pelacakan, tidak ada VMS/AIS), tapi juga tanpa manfaat data.
- SQL injection: pakai parameter binding & whitelist sort [S7]; preventif dasar tersedia.

---

## 22. Limitations

### Documented Limitation (eksplisit di kode/komentar)
- Cuaca/gelombang **fallback `mock_data` hardcoded** saat API gagal → UI dapat menampilkan **data dummy** tanpa penanda jelas bagi pengguna "ini data palsu" (hanya field `source: 'mock_data'`). [S5]
- Chl **opsional**: jika `open_dataset` Chl gagal → pencocokan SST-only (spesies `chl_required` tetap BUTUH Chl, sehingga zona untuk spesies itu hilang). [S2]
- Resolusi Chl 0.25° → 0.027° memakai **nearest neighbor** (bloky), SST linear; interpolasi extrapolasi luar grid diizinkan (`fill_value=None`). [S2]
- Basemap offline membutuhkan pra-warm (file ~30–60 MB; `build-basemap.sh`; HEAD+jika belum, unduh penuh lama); di dev tanpa SW jatuh ke CARTO online. [S11]
- Routing offline tanpa graf ter-cache → **garis lurus** (`approximate=true`) di-badge di UI. [S11]
- Route server dipanggil sinkron (PHP `Process::run` timeout 60 s) — langkah berpotensi lambat saat API/graf di-cold. [S4]
- `confidence` global = fraksi piksel matching seluruh domain, **disalin ke semua zona** — visualisasi marker pakai metrik yang bisa menyesatkan. [S2][S3]

### Observed Limitation (dari observasi kode)
- **Bukan ML & tanpa validasi**: parameter statis dari seeder tanpa referensi; tidak ada ground truth; klaim README "AI probability" tidak didukung implementasi. (lihat §7,§16) [S2][S1]
- **Tanpa lapisan vessel** (AIS/VMS) — tidak ada informasi kapal/effort manapun. [S2–S11]
- **Tanpa data historis** (sliding window menghapus masa lalu) — tidak ada analisis musiman. [S9]
- **Satu titik bahasa data**: ketergantungan pada kredensial CMEMS + stabilitas scraper KKP (dashboard internal, rentan berubah) + Nominatim rate-limit. [S7][S6]
- **Tanpa WPPNRI/EEZ/MPA/bathymetry/port layers** dan tanpa integrasi data nasional KKP lainnya (WPP regional, E-Logbook, STELINA). [S2–S11]
- **Tanpa test suite terlihat di repo terclone** (lint/types saja: eslint, tsc, prettier [S11]); tidak ada unit test Python/PHP. Risiko regresi pada kode ilmiah. [S8][S11]
- UX pengaman: tidak ada peringatan cuaca berbahaya/SOS. [S2–S11]

---

## 23. Strengths

| Aspek | Evidence |
| --- | --- |
| **Offline-first benar-benar berjalan** — PWA + 10 hari ZPPI + basemap vektor + Dijkstra laut di browser: unggul untuk sinyal laut yang hilang | [S11] |
| **Pemisahan komputasi berat vs server murah** (hitung di GitHub Actions, server hanya INSERT PostGIS) — pola hemat biaya yang matang | [S8][S9] |
| **Species-specific 18 pelagis** dengan kartu detail + persentase kesesuaian — lebih granular dari produk yang hanya "hotspot" tunggal | [S10][S11] |
| **Decision loop tertutup operasional**: zona → rute laut bebas-darat → cuaca → biaya BBM → harga jual KKP dalam satu alur | [S4][S5][S6][S7] |
| **PostGIS cerdas**: centroid utk payload ringan (centroid-only map), lazy poligon, clipping daratan di DB | [S3] |
| **Responsive mobile-native UX** (slider kapal, Zen Mode navigasi, GPS watch, re-routing, kartu geser/iOS-style) | [S11] |
| **Full-stack open & reproducible** — Docker Compose + env/example + init profile + workflow CI lengkap | [S11][S8] |
| **Lokalisasi Indonesia** (bahasa, zona waktu, kompas, Rupiah, komoditas pasar) | [S5][S6][S11] |
| **Transparansi sumber primer** — status evidence dapat dilacak dari kode (berlawanan langsung dengan opacity Marisikan) | seluruh file |

---

## 24. Feature Matrix

| Feature | Available | Evidence |
| --- | --- | --- |
| SST | ✅ (CMEMS 0.083°→0.027°, harian, forecast) | [S2] |
| Chlorophyll-a | ✅ (CMEMS 0.25°→0.027°, nearest) | [S2] |
| SSH | ❌ | [S2–S11] |
| Salinity | ❌ | [S2–S11] |
| Current | ❌ | [S2–S11] |
| Wave | ✅ (Open-Meteo Marine) | [S5] |
| Weather | ✅ (Open-Meteo + mock fallback) | [S5] |
| AIS | ❌ | [S2–S11] |
| VMS | ❌ | [S2–S11] |
| VIIRS | ❌ | [S2–S11] |
| SAR | ❌ | [S2–S11] |
| MODIS (langsung) | ❌ (dalam CMEMS saja) | [S2] |
| Bathymetry | ❌ | [S2–S11] |
| WPP / EEZ / MPA | ❌ | [S2–S11] |
| Fishing ground prediction | ✅ rule-based per spesies | [S2] |
| Forecasting | ✅ H+0..H+9 (10 hari) | [S9] |
| Time slider | ✅ | [S11] |
| Historical analysis | ❌ (hanya harga 12 bln) | [S9][S7] |
| Hotspot detection | ✅ zona ZPPI | [S2] |
| Navigation (sea routing) | ✅ searoute + offline Dijkstra | [S4][S11] |
| Fuel cost estimate | ✅ bensin-api | [S6] |
| Fish price monitor | ✅ KKP | [S7] |
| Vessel monitoring | ❌ | [S2–S11] |
| Catch recording | ❌ | [S2–S11] |
| Fisher feedback | ❌ | [S2–S11] |
| Offline mode | ✅ PWA + IndexedDB | [S11] |
| API | ✅ JSON Sanctum (4–5 endpoint) | [S12] |
| ML (learning dari data) | ❌ (rule-based) | [S2] |
| Validation vs catch | ❌ | [S2–S11] |

Legenda: ✅ = confirmed ada di kode; ❌ = confirmed tidak ada (diperiksa tuntas repo terclone); ? = tidak dapat diverifikasi (jarang dipakai di sini karena akses penuh kode).

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
 [Nelayar]            ──(tidak ada)──   ──(tidak ada)──
 ⭐ terkuat:
 rule-based ZPPI     Marisikan/GreenFish   (vessel tracking AIS)
 per spesies 18       AIS → vessel intel   ── kosong di keduanya ──
 + offline PWA
 + operasional loop
 (rute, BBM, harga)
```

Nelayar **lebih dalam di fishing-ground intelligence operasional + offline engineering** daripada Marisikan, tetapi **kosong total pada dimensi vessel/tracking** yang jadi kekuatan Marisikan. Keduanya sama-sama lemah di fisheries management/enforcement.

---

## 26. GAP ANALYSIS

| Kategori | Temuan |
| --- | --- |
| **Data Gap** | Tidak ada AIS/VMS, VIIRS/SAR/MODIS langsung, SSH, arus, salinitas, bathymetry, WPP/EEZ/MPA, port layer; hanya SST/Chl/weather/wave/BBM/harga. Provenans `indonesia_land.geojson` tidak didokumentasikan. |
| **Intelligence Gap** | Rule-based envelope (deterministik) — bukan prediksi probabilistik terkalibrasi; tanpa validasi vs tangkapan; tanpa learning. |
| **Temporal Gap** | Hanya 10 hari ke depan; data masa lalu dihapus (~24–48 jam); tanpa seasonal/yearly insight. |
| **Spatial Gap** | Tidak ada analisis spasial lanjut (densitas, keterpautan WPP, jarak port); bounding Indonesia-only (95–141E, 11S–6N). |
| **Vessel Gap** | Sepenuhnya tanpa dimensi kapal (frontir terbesar vs Marisikan/GreenFish dan vs kebutuhan VMS/AIS nasional). |
| **Validation Gap** | Envelope tanpa referensi & tanpa ground truth; `confidence` tidak terkalibrasi; tidak ada angka presisi/recall. |
| **Integration Gap** | Tidak terhubung ke data nasional KKP selain harga (WPP, E-Logbook/STELINA, VMS, SAR, buoy). |
| **User/Feedback Gap** | Tidak ada pencatatan tangkapan & feedback → tidak ada loop perbaik-an; tidak ada fitur keselamatan (SOS/peringatan). |
| **Engineering Gap** | Mock weather di produksi (data palsu tanpa penanda UI), tidak ada test suite, ada framing README "AI" yang overclaim terhadap implementasi aturan. |

---

## 27. Potential Novelty

> **Potential research/development novelty** — bukan klaim "belum pernah ada di dunia".

| Existing Capability | Gap | Proposed Improvement | Evidence |
| --- | --- | --- | --- |
| Nelayar: zona per spesies + offline PWA | Envelope statis tanpa kalibrasi lokal & tanpa validasi | Kalibrasi ambang per WPPNRI + validator vs E-Logbook/STELINA + penalaran probabilitas Bayesian membuka "probability" sungguhan | [S2][S10] |
| Nelayar: sliding window 10 hari | Tanpa klimatologi/historis — hanya jendela 10 hari | Tambah **klimatologi musiman & anomali SST** (banding vs normal) → insight pergeseran zona antar musim | [S9] |
| Nelayar: tanpa vessel (privasi-kecil) | Tidak ada AIS/VMS — berbeda dgn produk komersial | Tambah **deteksi kapal kecil via VMS lokal/optik** opsional utk analisis effort per WPP, tetap dengan opt-in privasi | [S2–S11] vs [S1-Marisikan] |
| Nelayar: route+BBM+harga | Tidak ada input hasil tangkapan | **Closed-loop: prediksi → trip → catatan hasil → update skor kesesuaian tiap spesies per wilayah** | [S11] |
| Nelayar: mock weather fallback | Data palsu bisa tampil tanpa disadari | Tandai eksplisit + peringatan keselamatan (BMKG) | [S5] |

---

## 28. Relevance terhadap Software yang Akan Dibangun

### Bisa diadopsi (langsung)
- **Arsitektur compute-offload** (hitung berat di CI/worker → server ringan hanya ingest) — sangat ekonomis untuk VPS Indonesia.
- **PostGIS pattern**: centroid-ringan utk peta + lazy full-polygon; `ST_Difference` clipping daratan.
- **Offline-first PWA** (10 hari ZPPI + basemap vektor + Dijkstra laut klien) — desain yang memecahkan konektivitas nyata nelayan.
- **Decision chain zona → rute → cuaca → BBM → harga jual** — alur operasional yang sebenarnya dipakai nelayan.
- **Pemisahan PHP↔Python** dengan protokol stdout-JSON/stderr-log yang bersih → mudah diganti/tambah kalkulator baru.
- **18 profil spesies** berbasis konsep ZPPI/KKP — sejalan dengan literatur perikanan Indonesia.

### Bisa dikembangkan
- **Kalibrasi & validasi**: ganti envelope statis dgn parameter yang divalidasi vs data tangkapan nyata; tambah metrik (precision n-species, RMSE posisi).
- **Klimatologi**: simpan historis + hitung anomali & musiman; perpanjang jendela.
- **Data nasional**: layer WPPNRI/EEZ/MPA/bathymetry/port; integrasi E-Logbook/STELINA & VMS (tanpa pelacakan wajib—desain opt-in).
- **Feedback loop** hasil tangkapan per trip (spesies berat gear durasi) → pembaruan bobot/ambang per wilayah.
- **Keselamatan**: peringatan cuaca berbahaya + status sinyal.

### Harus dihindari
- **Overclaim**: README menyebut "AI/Catch Logic probability" padahal aturan statis — jaga klaim = implementasi (transparansi sumber, resolusi, validasi).
- **Fallback silent tanpa penanda**: `mock_data` & `approx straight line` harus tampil jelas di UI.
- **Menghapus historis demi penyimpanan** tanpa rencana fondasi data untuk analisis musim.
- **Tanpa test suite** pada pipeline ilmiah (resiko tinggi di kode geoprocessing).
- **Tanpa referensi** pada ambang ekologi (sumber literatur tiap envelope wajib dicantumkan).

### Potential Differentiator (terhadap produk lain)
- Satu-satunya kelas solusi yang **gabungkan perikanan-rule-based nasional (ZPPI) + offline PWA + loop biaya/harga** — posisinya bisa diperkuat dengan **kalibrasi WPPNRI & validasi terbuka**, dua hal yang absen di Marisikan.

---

## 29. Final Summary

| Aspek | Temuan |
| --- | --- |
| Main purpose | Web GIS prediksi zona potensi ikan pelagis berbasis CMEMS utk efisiensi & hasil tangkapan [S1] |
| Target user | Nelayan menengah-kecil Indonesia, mobile-first, pengerjaan terbuka (skripsi/proyek publik) [S1][S13] |
| Strongest capability | Zona per 18 spesies (rule-based) + **offline-first PWA** + decision loop (rute, cuaca, BBM, harga) [S2][S11][S4–S7] |
| Main data | SST & Chl CMEMS (analysis-forecast), Open-Meteo (+mock), searoute graph, KKP prices, bensin-api BBM [S2][S5][S7][S6] |
| Main intelligence | Rule-based HSI/envelope matching — **bukan ML**; skor confidence sintesis [S2] |
| Prediction | Zona + spesies + confidence per tanggal (H+0..H+9); tanpa validasi/ground truth [S2][S9] |
| Historical analysis | ❌ untuk oseanografi (data dibuat melayang); harga ikan 12 bulan ✅ [S9][S7] |
| Vessel intelligence | ❌ tanpa AIS/VMS — pembeda terbesar vs Marisikan [S2–S11] |
| Fisher decision support | ✅ level 5 (navigasi aktif GPS + re-routing) — lebih dalam dari Marisikan [S11] |
| Main limitation | Tanpa ML/validasi; tanpa historis; tanpa vessel; fallback data palsu; overclaim "AI"; tanpa referensi ambang [S2][S5][S7...][S1] |
| Biggest gap | Kalibrasi & validasi vs tangkapan nyata + analisis musiman + integrasi WPPNRI/VMS/E-Logbook + loop feedback [S26] |
| Potential novelty | Offline-first decision support per-spesies yang bisa dinaikkan menjadi **validated, climate-aware, WPP-calibrated** system utk nelayan skala kecil (non-AIS) [S27] |

### 5–10 Insight Terpenting
1. **Nelayar adalah contoh bagus engineering (open & reproducible), tetapi lemah sains**: algoritma deterministik env-based tanpa training, tanpa validasi, tanpa ground truth—berlawanan 180° dari klaim "AI" README-nya.
2. **Offline-first adalah keunggulan langka** — 10 hari + basemap vektor + Dijkstra laut di browser memecahkan masalah konektivitas yang nyata dimiliki nelayan Indonesia; tidak ada pesaing lokal terbuka yang sebagus ini.
3. **"Sliding window yang menghapus masa lalu" adalah kesalahan strategis** bagi produk riset: tanpa arsip tidak ada klimatologi, tidak ada musim, tidak ada study zona. Simpan arsip + agregat.
4. **Metrik `confidence` di marker = fraksi piksel cocok global** (disalin ke semua zona) — contoh pentingnya arsitektur metrik yang benar (harus per-zona, per-spesies terkalibrasi).
5. **Compute-offload ke CI** (`ocean-sync` tiap jam) adalah pola yang wajib ditiru untuk anggaran VPS.
6. **Ambang envelope ZPPI tanpa referensi** = risiko ilmiah & kepatuhan; setiap ambang harus punya sumber (literatur/KKP) dan uji sensitivitas.
7. **Fallback `mock_data` tanpa penanda UI** bisa menampilkan data palsu ke nelayan — "source of truth" yang menyamar.
8. **Celah vessel** (AIS/VMS) adalah perbedaan fundamental dgn Marisikan/GreenFish dan sekaligus **peluang desain privasi** bagi kapal kecil non-AIS (opsional, opt-in).
9. **Closed-loop belum ada** — tambahkan input hasil tangkapan per trip → peluang kunci untuk membedakan dari produk statis.
10. **Untuk sistem Anda**, adopsi stack & arsitektur Nelayar sebagai *reusable reference*, lalu upgrade: validasi → klimatologi → WPP/EEZ/MPA → feedback → ML yang sesungguhnya.

---

## 30. DAFTAR REFERENSI

Semua sumber adalah **kode/file dalam repository terclone** `C:\Users\Harri Supriadi\AppData\Local\Temp\opencode\nelayar-gis`, berdasarkan `https://github.com/brianabdl/nelayar-gis` (branch `master`, komit yang terclone: `11f82f3`).

| # | File/Path (dlm repo) | Aspek yang didukung |
| --- | --- | --- |
| [S1] | `README.md` (+ root repo) | Profil, judul, target user, fitur utama, stack badges, tautan dataset CMEMS/KKP; klaim "Searoutes API", "AI/Catch Logic" |
| [S2] | `microservice/parse_zppi.py` | CMEMS SST/Chl ingest, grid 0.027°, interpolasi, envelope+confidence, bitmask, vektorisasi, PNG overlay, output GeoJSON |
| [S3] | `app/Services/OceanService.php` (+ `app/Models/OceanData.php`, `ZppiZone.php`) | fetchAndStore, fishProfilesPayload, computeFeatures, storeFeatures, clipping PostGIS, centroid vs poligon, endpoints data |
| [S4] | `microservice/route_sea.py` + `app/Services/RouteService.php` | searoute-py, arg parsing, Redis cache route (TTL 1 hari), Process::run timeout 60 s |
| [S5] | `app/Services/WeatherService.php` + `app/Http/Controllers/WeatherController.php` | Open-Meteo forecast & marine, clamp H+0..H+9, TTL 60 mnt, kompas 8 arah, WMO→ID, `mock_data` fallback |
| [S6] | `app/Services/FuelPriceService.php` | bensin-api, Nominatim reveral, TTL provinsi 6 jam & geocode 30 hari, fallback nasional |
| [S7] | `microservice/scrape_kkp.py` + `app/Services/FishPriceService.php` + `app/Http/Controllers/PricesController.php` | scraping mi.kkp.go.id, 5 komoditas, statistik/ticker/trend, harga santuari, whitelist sort, pagination |
| [S8] | `.github/workflows/ocean-sync.yml` + `deploy.yml` | compute-offload CI tiap jam, SSH/rsync/docker cp, deploy image Docker |
| [S9] | `app/Console/Commands/SyncOceanForecast.php`, `IngestOceanForecast.php`, `ExportFishProfiles.php`, `ScrapeKkpPrices.php` + `config/schedule.php` | sliding window H+0..H+9, cleanup masa lalu, ingest hasil CI, penjadwalan 02:00/03:00 |
| [S10] | `database/migrations/*` + `database/seeders/FishProfileSeeder.php`, `LandBoundarySeeder.php` | schema (ocean_data, zppi_zones, fish_profiles, fish_prices, weather_cache, land_boundaries), 18 profil spesies+envelope, seed daratan |
| [S11] | `resources/js/**` (Map, Prices, Weather, offline/, pwa.ts, mock.ts), `package.json`, `docker-compose.yml`, `.env.docker.example`, `scripts/build-basemap.sh`, `scripts/pwa-postbuild.mjs` | frontend React/Leaflet, PWA/IndexedDB, Dijkstra offline, basemap PMTiles/CARTO, deployment Compose+init, build-basemap |
| [S12] | `routes/web.php` + `routes/api.php` | halaman Inertia (Landing, Map, Weather, Prices, Privacy), API Sanctum (auth, map/route, map/weather, zones/bulk, zone, prices) |
| [S13] | `git log` (clone dangkal `--depth 1`) | komit terclone `11f82f3` 2026-08-03, author `brianabdl`, branch `master` |

**Catatan keandalan sumber:** [S1]–[S12] adalah sumber primer (kode open-source langsung, layer evidence [CONFIRMED] tinggi). [S13] terbatas karena clone dangkal — riwayat lengkap, kontributor, dan keberadaan test suite eksternal **[UNKNOWN]**. Data cuaca `mock_data`, sumber `indonesia_land.geojson`, sumber literatur ambang `fish_profiles`, serta lisensi repo **[UNKNOWN]**. Klaim "AI/probability" & "Searoutes API" di README [S1] **tidak sesuai** dengan implementasi [S2][S4]—dicatat sebagai perbedaan dokumentasi vs kode.

### Referensi Web Pelengkap Konteks (BUKAN evidence bahwa Nelayar memakainya)

| # | Author / Organization | Tahun | Judul | Jenis | URL/DOI | Aspek yang didukung |
| --- | --- | --- | --- | --- | --- | --- |
| [W1] | Muhamad Sadly, Nani Hendiarti, et al. | 2009 | Fishing ground prediction using a knowledge-based expert system geographical information system model in the South and Central Sulawesi coastal waters (International Journal of Remote Sensing) | Paper ilmiah | https://doi.org/10.1080/01431160902865780 | Menegaskan pendekatan rule/envelope ZPPI adalah literatur mapan yang pernah divalidasi (85% vs in-situ) — konteks, bukan klaim validasi Nelayar |
| [W2] | Pencarian web (opencode, Sept 2026) | 2026 | Pencarian publikasi/artikel resmi "nelayar-gis" dan "brianabdl" | Hasil telusur (tidak ditemukan) | — | Tidak ditemukan paper/laman resmi proyek → afiliasi & validasi publik [UNKNOWN]; hasil yang relevan hanya literatur PPI umum (WPPNRI, MODIS/VIIRS, upwelling dsb.) |

---

### Aturan Final — Pemeriksaan Evidence

- **Sumber primer**: repo open-source = sumber utama; setiap pernyataan tentang fungsionalitas ditelusuri ke file & baris (bukan asumsi).
- **Tidak ada angka dibuat-buat**: tidak ada akurasi/statistik yang diinvensi; semua metrik (confidence, ETA 18 km/j, 0.4 L/km) diambil persis dari kode.
- **Overclaim dipisahkan**: klaim pemasaran README ("AI", "Searoutes API") dibedakan **secara eksplisit** dari kenyataan implementasi (rule-based; searoute-py lokal).
- **Dua metrik confidence dibedakan**: `confidence` zona (kolom DB = fraksi piksel global) vs `confidence` per spesies (`ikan_cocok` = rata-rata zona), agar tidak tercampur dalam analisis.
- **Perbedaan status evidence dipertahankan**: [CONFIRMED] (dalam kode/repo), [INDICATED] (indikasi kuat, mis. `markercluster` dependency), [UNKNOWN] (tidak dapat diverifikasi dari repo).