# Absensi-Patroli

Aplikasi web internal **Network Indonesia Timur (NIT)** untuk absensi dan patroli keamanan (security patrol) tim lapangan di Manado & Minahasa Utara — dibangun sebagai **single-file React app** (`index.html`) dengan backend **Firebase Firestore**, dan didistribusikan juga sebagai **APK Android** (Capacitor) untuk penggunaan di lapangan.

🔗 **Demo (GitHub Pages):** `https://djetlytakaalumang-sys.github.io/Absensi-Patroli/`
📦 **Download APK:** [`app-release.apk`](./app-release.apk)

---

## ✨ Fitur Utama

### Absensi
- Absen Masuk/Pulang dengan **verifikasi GPS** (anti fake-GPS, multi-sample validation) + **selfie**
- Deteksi status **Hadir / Terlambat** otomatis
- Deteksi **shift Piket Malam** otomatis
- Pengajuan & approval **Izin/Cuti**
- Jam server terpercaya (`getTrustedNow()`) — mencegah manipulasi jam perangkat

### Patroli & Checkpoint
- Sesi patroli **real-time** dengan pelacakan lokasi (GPS) & peta (Leaflet)
- **Checkpoint geofencing** — deteksi otomatis saat petugas masuk radius checkpoint
- Sistem **rute per tim** (Tim Manado & Tim Minut), termasuk dukungan **petugas yang merangkap di lebih dari 1 tim**
- **Bonus skor** kalau rute checkpoint kedua tim berbeda di hari yang sama
- Aturan **anti-curang**: checkpoint yang sama tidak dihitung dua kali berturut-turut (harus mampir checkpoint lain dulu)
- Laporan **Kejadian (incident report)** selama patroli

### Peta Live Patroli
- Peta live semua petugas yang sedang aktif, dengan:
  - Warna garis rute **unik per petugas** (tidak ada yang tabrakan)
  - Label melayang (nama, status, waktu update terakhir)
  - Ikon navigasi bergaya panah, berputar sesuai arah gerak
  - Ikon checkpoint otomatis menyesuaikan jenis (**STO** = menara sinyal, **CLS** = globe/kabel)
  - Legend & indikator status koneksi (Live / Terputus)

### Admin
- **Dashboard** ringkasan aktivitas & petugas aktif
- **Leaderboard / Skor** gabungan: 60% Kehadiran + 40% Patroli
- **Riwayat Login** dengan deteksi clock-skew (jam device vs server)
- **Role-based access control**: Admin / Employee / Viewer
- Manajemen **Jadwal** (import Excel) & **Checkpoint**
- **Rekap Rit/CP** — per tanggal maupun per bulan
- Export **PDF & Excel**

### Aplikasi Android (APK)
- Dibungkus dengan **Capacitor** (`com.nit.presensiteampatroli`)
- Mode **Remote** — memuat konten langsung dari GitHub Pages
- **Background GPS tracking** (`@capacitor-community/background-geolocation`) supaya lokasi tetap terkirim walau HP terkunci/di-background

---

## 🛠️ Tech Stack

| Bagian | Teknologi |
|---|---|
| Frontend | React (via CDN, single-file `index.html`) |
| Peta | Leaflet.js + tile CartoDB Positron |
| Backend / DB | Firebase Firestore (realtime listener) |
| Mobile wrapper | Capacitor (Android APK) |
| Background location | `@capacitor-community/background-geolocation` |
| Bahasa UI | Bahasa Indonesia |

---

## 📁 Struktur Repo

```
├── index.html        # seluruh aplikasi (UI + logic), single-file React app
├── app-release.apk   # APK Android siap install (mode Remote)
└── README.md
```

## 🚀 Deploy / Update

Repo ini di-hosting via **GitHub Pages**, langsung dari `index.html` di branch `main`. Setiap kali `index.html` di-update dan di-push ke `main`, GitHub Pages otomatis re-deploy — APK Android (mode Remote) ikut menampilkan versi terbaru tanpa perlu rebuild/reinstall APK.

## ⚙️ Konfigurasi

Aplikasi butuh koneksi ke **Firebase Firestore** milik NIT (collection: `users`, `records`, `patrols`, `checkpointPasses`, `checkpoints`, `settings`, dst). Konfigurasi Firebase ada langsung di dalam `index.html`.

---

## 👤 Role Pengguna

- **Admin** — akses penuh: kelola karyawan, checkpoint, jadwal, rekap, skor, peta live
- **Employee** — absensi, mulai/selesai patroli, lihat rute & progres checkpoint sendiri
- **Viewer** — akses lihat-saja (read-only) untuk monitoring

---

## 📝 Catatan

Proyek ini dikembangkan & di-maintain secara iteratif — perubahan fitur/bugfix biasanya langsung dilakukan di `index.html` per permintaan dan di-deploy ulang lewat commit ke `main`.
