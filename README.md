# Warung Kitaa — Panduan Jadi APK

Folder ini berisi 2 jalur untuk mengubah aplikasi Warung Kitaa jadi APK Android.
Kamu bisa coba salah satu, atau dua-duanya.

---

## 0. Upload dulu ke GitHub

1. Buat repo baru di GitHub, misal `warung-kitaa`.
2. Upload **semua isi folder ini** (termasuk folder `.github`, `icons`, `www`) ke repo tsb.
3. Buka tab **Settings → Pages** di repo:
   - Source: `Deploy from a branch`
   - Branch: `main`, folder `/ (root)`
   - Simpan. Tunggu 1-2 menit, nanti muncul URL seperti:
     `https://username.github.io/warung-kitaa/`
4. Buka URL itu, pastikan aplikasi tampil normal.

---

## Jalur A — PWABuilder (paling gampang, tanpa coding)

1. Buka https://www.pwabuilder.com
2. Masukkan URL GitHub Pages kamu (dari langkah 0), klik **Start**.
3. PWABuilder akan mengecek manifest.json, service worker, dan ikon (semua sudah disiapkan di folder ini).
4. Klik **Package for Stores** → pilih **Android**.
5. Isi `Package ID` (bebas, misal `com.warungkitaa.app`), lalu **Generate**.
6. Download file `.apk` / `.aab` yang dihasilkan.
7. Kirim file APK ke HP Android (lewat WhatsApp/Drive/kabel), lalu install (aktifkan dulu
   "Izinkan install dari sumber tidak dikenal" di pengaturan HP).

---

## Jalur B — GitHub Actions (build otomatis tiap update)

Workflow-nya sudah ada di `.github/workflows/build-apk.yml`. Setelah repo di-push ke GitHub:

1. Buka tab **Actions** di repo GitHub kamu.
2. Kalau belum jalan otomatis, klik workflow **Build APK** → **Run workflow**.
3. Tunggu sampai selesai (durasi ±3-5 menit).
4. Setelah selesai (centang hijau), buka hasil run tersebut, scroll ke bagian
   **Artifacts**, lalu download `warung-kitaa-apk.zip`.
5. Extract zip-nya, di dalamnya ada `app-debug.apk` — itu file APK-nya.
6. Kirim & install ke HP Android seperti Jalur A.

> Setiap kali kamu update kode dan push ke branch `main`, APK baru akan otomatis
> dibuild lagi lewat Actions. Tinggal download ulang artifact-nya.

---

## Catatan penting

- APK dari Jalur A/B ini **APK debug/unsigned** — cukup untuk dipakai sendiri,
  tapi belum bisa diupload ke Play Store (perlu proses signing tambahan kalau nanti mau publish).
- Data transaksi tetap tersimpan **di HP itu sendiri** (local storage/SQLite),
  bukan di GitHub ataupun server manapun.
- Kalau nanti mau ganti nama aplikasi/ikon, edit `manifest.json` (untuk PWABuilder)
  dan `capacitor.config.json` (untuk Capacitor/GitHub Actions), lalu build ulang.
