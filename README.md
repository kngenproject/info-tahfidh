# Sistem Informasi Monitoring Tahfidz

Aplikasi web untuk memantau perkembangan hafalan Al-Qur'an siswa. Wali murid mencari nama anak dan langsung melihat surat, ayat, nilai, serta riwayat setoran. Guru dan admin mengelola data lewat dashboard.

**Demo:** https://kngenproject.github.io/info-tahfidh/
**Halaman admin:** https://kngenproject.github.io/info-tahfidh/#admin

## Fitur

### Halaman publik (wali murid)
- Pencarian nama siswa dengan hasil langsung dan nama yang disorot
- Detail siswa: surat, ayat, nilai (L / CL / KL), dan 10 riwayat setoran terakhir
- Navigasi keyboard: `/` fokus, `↑` `↓` pilih, `Enter` buka, `Esc` kembali
- Animasi pembuka dan latar bergerak bergaya gelombang

### Admin dan guru
- **Dashboard:** statistik, capaian, sebaran nilai, progres per kelas, setoran terbaru, siswa belum dinilai
- **Data Siswa:** tambah, edit, hapus, cari, filter kelas
- **Input Setoran** dan **Input Cepat** (satu kelas sekaligus)
- **Planning:** target hafalan per siswa atau kelas, dengan status Terencana / Minggu ini / Terlambat / Selesai
- **Rekap dan Laporan:** export CSV, cetak, penyimpanan dan arsip riwayat
- **Import Excel / CSV:** multi-sheet (nama sheet = kelas), mode aman tanpa menimpa data lama
- **Pengaturan:** nama sekolah, nama aplikasi, logo, warna, teks halaman publik, ganti password

### Teknis
- Satu file `index.html`, tanpa framework, tanpa proses build
- PWA: dapat dipasang dan jalan offline (`manifest.json` + `sw.js`)
- Cocok untuk GitHub Pages

## Struktur File

| File | Fungsi |
|---|---|
| `index.html` | Seluruh aplikasi |
| `data.json` | Data yang dibaca halaman publik |
| `manifest.json` | Konfigurasi PWA |
| `sw.js` | Service worker (cache offline) |
| `icon.svg` | Ikon aplikasi |

## Cara Pasang

1. Upload `index.html`, `data.json`, `manifest.json`, `sw.js`, dan `icon.svg` ke repo.
2. Buka **Settings → Pages**, pilih **Deploy from a branch**, branch `main`, folder `/ (root)`, lalu Save.
3. Buka `https://<username>.github.io/<nama-repo>/`.

Uji lokal harus lewat server, bukan `file://`:

python -m http.server 8000

Lalu buka `http://localhost:8000`.

## Alur Penggunaan

1. Buka halaman admin (`#admin`) dan login.
2. Isi data lewat **Data Siswa → Import** atau input manual.
3. Catat setoran lewat **Input Setoran** atau **Input Cepat**.
4. Buka **Laporan → Unduh data.json**.
5. Timpa `data.json` di repo, lalu commit dan push. Halaman wali murid otomatis memakai data terbaru.

Perintah update data:
git push
git commit -m “update data”
git add data.json

## Format Import

**Excel:** setiap sheet mewakili satu kelas (misalnya `4B`, `4C`). Header wajib berisi `SURAT`, `AYAT`, `NILAI`. Kolom `NAMA` boleh berada di baris judul di atas header. Baris footer seperti "Ket" dilewati otomatis.

**CSV:**
4B,Contoh Nama,Abasa,6,L
KELAS,NAMA SISWA,SURAT,AYAT,NILAI

Nilai yang dikenali: `L` (Lancar), `CL` (Cukup Lancar), `KL` (Kurang Lancar).

## Akun Awal

| Peran | Username | Password |
|---|---|---|
| Admin | `admin` | `admin123` |
| Guru | `guru` | `guru123` |

Segera ganti lewat **Pengaturan → Akses**, dan matikan kotak akun demo di halaman login.

## Keamanan dan Privasi

- Data admin tersimpan di `localStorage` browser, dan password tersimpan polos di browser tersebut. Aplikasi ini cocok untuk lingkungan kecil, bukan untuk data yang sangat sensitif.
- `data.json` di repo publik **dapat dibaca siapa saja**, termasuk nama dan nilai seluruh siswa. Gunakan data yang boleh dipublikasikan, atau jangan push data asli.
- Password hanya berlaku di browser tempat diubah dan tidak ikut ke `data.json`.

## Lisensi

Silakan gunakan dan ubah sesuai kebutuhan lembaga Anda.