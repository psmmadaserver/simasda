# Si MasDA — Vercel Wrapper

Halaman pembungkus statis untuk menampilkan aplikasi Google Apps Script Si MasDA di dalam iframe agar bilah pemberitahuan Google Apps Script tidak tampil sebagai bilah terpisah pada halaman utama.

## Isi paket
- `index.html` — halaman utama responsif yang memuat web app GAS.
- `vercel.json` — konfigurasi statis minimal untuk Vercel.

## Deploy ke Vercel
1. Ekstrak ZIP ini ke sebuah folder.
2. Unggah folder ke repository GitHub baru, atau unggah repository tersebut ke Vercel.
3. Di Vercel pilih **Add New → Project**, impor repository.
4. Untuk proyek statis ini, biarkan Framework Preset sebagai **Other**. Build Command dan Output Directory dapat dikosongkan; root project berisi `index.html`.
5. Klik **Deploy**.
6. Buka domain Vercel yang diberikan dan uji menu, penyimpanan, serta kamera absensi.

## URL Google Apps Script
Saat paket dibuat, URL `/exec` diambil dari URL `/dev` yang terlihat pada screenshot pengguna. Jika URL `/exec` tersebut tidak aktif, buka Apps Script → **Deploy → Manage deployments**, salin URL Web app yang berakhir `/exec`, lalu ganti URL pada dua tempat di `index.html` (atribut `src` iframe dan tautan fallback).

## Pengaturan deployment GAS yang penting
- Di fungsi `doGet()` pada GAS, pastikan output HTML memakai `.setXFrameOptionsMode(HtmlService.XFrameOptionsMode.ALLOWALL)`.
- Deploy sebagai **Web app** dan pilih akses yang sesuai dengan kebijakan sekolah. Untuk akses tanpa login Google, deployment harus memang diizinkan oleh pengaturan organisasi/akun; jangan mengubah akses menjadi publik jika kebijakan sekolah melarangnya.
- Uji kamera di domain HTTPS Vercel. Iframe sudah memberi izin `camera`; browser tetap dapat meminta persetujuan pengguna.
- Jika aplikasi GAS mewajibkan autentikasi Google, pembukaan di dalam iframe bisa dibatasi oleh browser atau kebijakan login. Gunakan tombol **Buka Si MasDA di tab baru** sebagai alternatif.

Paket ini tidak mengubah kode backend GAS, spreadsheet, atau logika absensi. Ini hanya mengganti halaman masuk/tampilan luarnya.
