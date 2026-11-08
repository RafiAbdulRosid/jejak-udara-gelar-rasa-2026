# JEJAK UDARA — V5 Compact Data Quality

Prototipe website dashboard lomba DA Gelar Rasa 2026 berbasis HTML, CSS, JavaScript. Ini melanjutkan V4, termasuk **peta geometri Natural Earth**, seluruh halaman, dan filter. Fokus V5 adalah tab **Data Quality**.

## Menjalankan

Ekstrak ZIP, buka `jejak_udara_v5/index.html` menggunakan Chrome atau Edge. Tidak perlu server internet atau instalasi library. Dashboard memakai file `data/data.js`, `data/quality.js`, dan `assets/map_geometry.js` lokal.

## Perubahan V5

- **Tata letak lebih padat**: lima KPI, status dan donut QC, matriks cakupan 12 bulan, ranking atau perbandingan enam polutan, interpretasi singkat, serta metodologi.
- Dua mode pada tab **Data Quality**:
  - **Overall Dataset**: audit seluruh baris dan 27 stasiun, seluruh periode sumber; filter global tidak berlaku di mode ini.
  - **Filtered Quality**: ringkasan **stasiun + tahun + polutan** yang mengikuti filter Tahun, Polutan, Stasiun di kanan atas. Klik satu baris pada panel Parameter Availability untuk mengubah polutan.
- Tambahan KPI: baris QC VALID, cakupan jam unik yang layak untuk polutan terpilih, jumlah hari layak (≥18 jam), serta jumlah seluruh pengukuran periode. Mode overall menampilkan 27 stasiun, status QC, dan cakupan jam QC.
- **Monthly Data Completeness**: pada mode Filtered, dua baris menunjukkan jam berstatus QC VALID dan jam yang memiliki nilai polutan valid; pada mode Overall, tiga baris menunjukkan 2024–2026 dengan gabungan 27 stasiun.
- Satu warna heatmap selalu merepresentasikan rentang persentase cakupan yang sama, bukan nilai konsentrasi polutan.
- Status QC tetap merupakan **status baris**; jam unik dengan pengukuran nonnegatif, terhingga, dan QC VALID dihitung secara terpisah untuk setiap polutan. Satu jam dengan banyak baris valid tetap dihitung sekali. Tahun 2026 hanya Jan–14 Okt.
- Penanda waktu berupa `timestamp_start` tanpa zona waktu eksplisit, mengikuti CSV; masih perlu verifikasi metadata untuk analisis waktu yang peka zona waktu.

## Sumber data dan metode

- Semua statistik pengukuran, QC, dan kesehatan diambil dari CSV panitia. Agregasi kualitas ditambahkan melalui `data/quality.js` yang dibangun ulang dari 27 CSV stasiun.
- File 2023-12-31 dan timestamp anomali di luar periode nominal **tidak termasuk** dalam KPI berbasis tahun atau matriks cakupan; angka **All Source Records** tetap mencakup seluruh catatan asli.
- Satu hari disebut layak untuk analisis ringkasan jika minimal **18 jam unik** memiliki pengukuran QC VALID serta nilai polutan nonnegatif dan terhingga; ini ambang analitis eksploratif, bukan standar resmi.
- Medan, Banjarbaru, dan Pesawaran masih berlabel ppm; tidak langsung dibandingkan dengan 24 stasiun lain yang berlabel µg/m³.
- Cakupan jam menunjukkan **ketersediaan pengukuran**, tidak menunjukkan udara yang lebih bersih, diagnosis sensor, atau kualitas kesehatan.
- Peta memakai geometri Natural Earth *public domain* sebagai referensi bentuk daratan, bukan data polusi. **Handbook melarang dataset di luar pemberian panitia; konfirmasikan bahwa geometri peta eksternal diizinkan sebelum submission final.**
- Jangan memublikasikan data turunan panitia ke repo publik sebelum ada kepastian izin distribusi. Logo lomba wajib dimasukkan sebelum pengumpulan. Case study resmi tetap perlu dicocokkan.

## Struktur

- `index.html`: HTML dashboard dan lima tab
- `css/style.css`: dark high-density bento layout
- `js/app.js`: navigasi, filter, kalkulasi, grafik, quality modes
- `data/data.js`: ringkasan data terolah yang digunakan dashboard
- `data/quality.js`: agregasi QC per tahun-bulan, stasiun, parameter
- `assets/map_geometry.js`: geometri referensi peta Indonesia
- `scripts/*`: skrip preprocessing awal dan peta

**Status:** V5 prototipe lokal untuk review; belum publikasi final.
