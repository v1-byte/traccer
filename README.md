# HM Tracker (Capacitor)

Aplikasi pencatat jam kerja (hour meter) alat — **100% offline**, UI dari HTML yang sudah ada.

- Login identitas + PIN lokal (tanpa internet)
- Kamera + watermark profesional
- OCR angka meter (opsional, file di `www/tess/`)
- Galeri foto di perangkat
- Backup / restore lokal

## Syarat

- Node.js 18+
- Android Studio (SDK 24+)
- JDK 17

## Setup cepat

```bash
cd hm-tracker-capacitor
npm install
npx cap add android
npx cap sync android
npx cap open android
```

Di Android Studio: **Run** ke perangkat/emulator.

## Perintah berguna

| Perintah | Fungsi |
|----------|--------|
| `npm install` | Pasang dependency |
| `npx cap add android` | Buat project Android (sekali saja) |
| `npx cap sync android` | Salin `www/` + plugin ke Android |
| `npx cap open android` | Buka di Android Studio |
| `npm run android` | Build web + sync Android |

## Struktur

```
hm-tracker-capacitor/
├── www/                 ← UI HTML (index.html = app penuh)
│   ├── index.html
│   ├── manifest.json
│   ├── icon-*.png
│   └── tess/            ← taruh file Tesseract di sini (opsional)
├── capacitor.config.json
├── package.json
└── android/             ← muncul setelah `cap add android`
```

## Offline & OCR

- Semua data (unit, HM, PIN, foto) disimpan di perangkat.
- OCR memakai file lokal di `www/tess/`. Tanpa folder itu, app tetap jalan; angka HM diisi manual.
- Tidak ada server / API untuk alur utama.

## Plugin native yang dipakai

- `@capacitor/app`
- `@capacitor/camera` (cadangan; HTML utama pakai `getUserMedia`)
- `@capacitor/filesystem`
- `@capacitor/geolocation`
- `@capacitor/status-bar`

HTML juga mendeteksi plugin kustom `HMFiles` (opsional) untuk simpan ke galeri HP. Tanpa plugin itu, unduhan file browser dipakai.

## Izin Android

Setelah `cap add android`, pastikan di `AndroidManifest.xml` ada:

```xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" android:maxSdkVersion="28" />
```

Capacitor biasanya menambahkan otomatis saat plugin dipasang; cek sekali setelah sync.

## Versi

- App: 1.5.1  
- UI: HTML dark amber (Frostbyte / HM Tracker)
