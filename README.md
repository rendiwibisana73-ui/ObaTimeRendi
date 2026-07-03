
# 💊 ObaTime — Aplikasi Pengingat Minum Obat Berbasis Android Native

**Disusun oleh:**
Rendi Nanda Wibisana
NIM: 231011400199
Kelas: 06TPLP004

---

## 🔗 LATAR BELAKANG

Kepatuhan minum obat (medication adherence) menjadi salah satu tantangan utama dalam menjaga efektivitas pengobatan, terutama bagi pengguna dengan jadwal konsumsi obat yang rutin dan berulang. Lupa waktu minum obat, dosis yang tidak konsisten, hingga tidak adanya pencatatan riwayat konsumsi seringkali berdampak pada menurunnya efektivitas terapi.

ObaTime hadir sebagai solusi digital yang membantu pengguna mengelola jadwal obat secara mandiri, dengan pengingat otomatis berbasis alarm sistem, narasi suara (Text-to-Speech), serta pencatatan riwayat konsumsi yang rapi dan mudah dipantau.

## 🔗 TENTANG APLIKASI

ObaTime adalah aplikasi mobile berbasis **Android Native (Java)** yang memungkinkan pengguna menambahkan data obat beserta jadwal konsumsinya, kemudian sistem akan membunyikan alarm tepat waktu dan membacakan pengingat secara otomatis melalui Text-to-Speech. Setiap status konsumsi (diminum, dilewati, atau terlambat) dicatat ke dalam riwayat harian menggunakan database lokal Room.

Sebagai nilai tambah, ObaTime juga terintegrasi dengan data **kualitas udara (Air Quality Index)** berdasarkan lokasi pengguna, memberikan pesan kontekstual yang mengaitkan kondisi udara di sekitar dengan pentingnya menjaga kepatuhan minum obat.

## 🔗 FITUR LENGKAP

### 📋 MANAJEMEN DATA OBAT
Pengguna dapat menambahkan, mengubah, dan menghapus data obat meliputi nama, dosis, bentuk sediaan (tablet, sirup, kapsul, dll), catatan tambahan, jumlah stok, serta warna ikon penanda. Setiap obat dapat diaktifkan atau dinonaktifkan pengingatnya sesuai kebutuhan.

### ⏰ JADWAL & ALARM OTOMATIS
Setiap obat dapat memiliki satu atau lebih jadwal konsumsi dengan jam spesifik dan pengulangan harian (mis. "setiap hari" atau hari-hari tertentu). Sistem menghitung waktu alarm terdekat secara otomatis menggunakan `AlarmManager` dengan dukungan *exact alarm*, dan tetap berjalan meski perangkat baru saja dinyalakan ulang (melalui `BootReceiver`).

### 🔊 PENGINGAT SUARA (TEXT-TO-SPEECH)
Saat alarm berbunyi, sebuah *foreground service* khusus membacakan pengingat secara otomatis (contoh: "Waktunya minum Paracetamol sebanyak 1 tablet"), sehingga pengguna tetap mendapat informasi jelas meskipun sedang tidak melihat layar. Fitur ini dapat diaktifkan/dinonaktifkan melalui halaman Pengaturan.

### 📊 RIWAYAT KONSUMSI OBAT
Setiap interaksi terhadap pengingat dicatat dengan status **Diminum**, **Dilewati**, atau **Terlambat**, lengkap dengan tanggal dan jam. Riwayat dapat difilter berdasarkan tanggal tertentu melalui `DatePicker`, dan menampilkan ringkasan jumlah obat yang diminum maupun dilewati pada hari tersebut.

### 🔔 LOG NOTIFIKASI
Seluruh riwayat notifikasi pengingat (menunggu, diminum, dilewati, terlambat) tersimpan dan dapat ditinjau kembali melalui panel notifikasi dalam aplikasi.

### 🌫️ INFORMASI KUALITAS UDARA (AQI)
Menggunakan lokasi pengguna (GPS) dan integrasi API kualitas udara, ObaTime menampilkan status kualitas udara terkini (Baik, Sedang, Tidak Sehat, Berbahaya) beserta pesan kontekstual yang mengingatkan pengguna untuk tetap menjaga kesehatan dan konsistensi minum obat sesuai kondisi lingkungan.

### ⚙️ PENGATURAN PERSONALISASI
Pengguna dapat mengatur nama tampilan, ukuran font (S/M/L/XL) untuk kenyamanan baca, mode gelap (dark mode), serta mengaktifkan/menonaktifkan narasi suara dan notifikasi sesuai preferensi masing-masing.

## 🔗 TEKNOLOGI YANG DIGUNAKAN

| Komponen | Teknologi |
|---|---|
| Bahasa Pemrograman | Java |
| Platform | Android Native (minSdk 26, targetSdk 35) |
| Database Lokal | Room Persistence Library |
| Arsitektur Navigasi | Android Navigation Component (Bottom Navigation + Fragment) |
| Penjadwalan Alarm | AlarmManager + BroadcastReceiver |
| Layanan Latar Belakang | ForegroundService (Text-to-Speech) |
| Konsumsi API | Retrofit2 + Gson Converter |
| Lokasi Pengguna | Google Play Services (FusedLocationProviderClient) |
| Build System | Gradle (Kotlin DSL) |

## 🔗 STRUKTUR MODUL UTAMA

```
id.rendinandawibisana.obatime
├── activity/        → SplashActivity, MainActivity, TambahObatActivity, JadwalObatActivity
├── fragment/         → HomeFragment, ObatFragment, RiwayatFragment, SettingFragment, NotifBottomSheet
├── model/            → Obat, JadwalObat, LogMinum, NotifLog
├── database/         → AppDatabase & DAO (Obat, JadwalObat, LogMinum, NotifLog)
├── adapter/          → RecyclerView Adapters untuk setiap modul data
├── util/             → AlarmHelper, AqiHelper, PrefHelper
├── network/          → ApiClient, AqiApiService, AqiResponse (integrasi AQI)
├── receiver/         → AlarmReceiver, BootReceiver
└── service/          → AlarmForegroundService (Text-to-Speech pengingat)
```

## 🔗 IZIN APLIKASI (PERMISSIONS)

- `POST_NOTIFICATIONS` — menampilkan notifikasi pengingat
- `SCHEDULE_EXACT_ALARM` / `USE_EXACT_ALARM` — memastikan alarm berbunyi tepat waktu
- `ACCESS_FINE_LOCATION` — mengambil data lokasi untuk informasi kualitas udara
- `RECEIVE_BOOT_COMPLETED` — menjaga jadwal alarm tetap aktif setelah restart perangkat
- `FOREGROUND_SERVICE` — menjalankan layanan Text-to-Speech saat alarm berbunyi
- `INTERNET` — mengambil data kualitas udara dari API eksternal

---

*Proyek ini dikembangkan sebagai bagian dari tugas mata kuliah Mobile Programming — Rendi Nanda Wibisana, 231011400199, Kelas 06TPLP004.*
