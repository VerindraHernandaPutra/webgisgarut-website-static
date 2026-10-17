# WebGIS Desa Cimaragas

Portal informasi spasial **Desa Cimaragas**: website multi-halaman yang menampilkan peta interaktif wilayah desa, pembagian RW, fasilitas umum, dan statistik wilayah. Peta dibuat dengan **QGIS** (ekspor *qgis2web*) dan **Leaflet.js**. Website ini statis, tanpa backend maupun database, dan siap di-deploy dengan **Docker + Nginx**.

## Halaman

| Halaman | File | Isi |
|---|---|---|
| Beranda | `index.html` | Pengantar portal, ringkasan informasi spasial dan statistik singkat |
| Peta Wilayah | `map-page.html` | Halaman peta interaktif (menampilkan `map.html` hasil qgis2web) |
| Statistik | `data-stats.html` | Data dan statistik wilayah |
| Fasilitas Umum | `facilities.html` | Daftar fasilitas desa beserta foto |
| Tentang | `about.html` | Profil kewilayahan dan cakupan data |

## Layer Data Peta

- **Wilayah:** Batas Desa Cimaragas, Batas RW (RW 01 sampai RW 10 dan area non-SLS)
- **Penggunaan lahan:** Sawah, Ladang, Pemukiman
- **Infrastruktur:** Jalan Desa
- **Fasilitas umum:** Kantor Desa, Masjid, Mushola, Madrasah, Sekolah Dasar, TK, Puskesmas, Pasar Mingguan, Lapangan Sepak Bola
- **Citra satelit:** raster desa (`data/CitraSatelit_5.png`)
- **Basemap:** Google Roads, Esri World Imagery, Google Terrain Hybrid

Data vektor disimpan sebagai GeoJSON berbentuk JavaScript di folder `data/`. Foto fasilitas ada di folder `images/`.

## Teknologi

- [QGIS](https://qgis.org) + plugin [qgis2web](https://github.com/tomchadwin/qgis2web)
- [Leaflet](https://leafletjs.com) beserta plugin (MarkerCluster, Measure, Locate, Layers Tree, Photon)
- HTML, CSS (`public.css`, `dashboard.css`), JavaScript
- Docker + Nginx (alpine) untuk deployment

## Struktur Folder

```
.
├── index.html, about.html, map-page.html,
│   map.html, data-stats.html, facilities.html
├── Dockerfile
├── css/              # Stylesheet situs, Leaflet, dan plugin
├── js/               # Leaflet dan plugin
├── data/             # Data spasial dan citra satelit
├── images/           # Foto fasilitas umum
├── legend/           # Gambar legenda
├── markers/          # Ikon marker (SVG)
└── webfonts/         # Font Font Awesome
```

## Cara Menjalankan

### Server lokal

Jalankan lewat server lokal, jangan membuka file langsung dengan `file://`.

```bash
# Pilih salah satu
npx serve .
python -m http.server 8000
```

Buka `http://localhost:8000`. Di VS Code bisa juga memakai ekstensi **Live Server**.

### Docker

```bash
docker build -t webgis-cimaragas .
docker run -d -p 8080:80 webgis-cimaragas
```

Buka `http://localhost:8080`.

> Basemap dimuat dari internet, jadi diperlukan koneksi.

## Catatan

- `map-page.html` memuat `map.html` hasil ekspor qgis2web. Jika peta diekspor ulang, periksa kembali file yang tertimpa.
- Basemap memakai tile Google dan Esri. Periksa ketentuan penggunaannya sebelum dipakai untuk keperluan komersial.
- Nama file foto di `images/` masih berawalan path lama (`D__Kuliah_ProjectWebgis_DataFoto_...`) bawaan hasil ekspor.

## Lisensi

Belum ditentukan. Tambahkan file `LICENSE` sesuai kebutuhan sebelum dipublikasikan.
