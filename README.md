# Database Simulasi Pasangan Calon

Dasbor untuk data simulasi/fiktif: **Google Sheets → Apps Script (API) → GitHub Pages**,
dengan fitur edit langsung dari website yang otomatis tersimpan kembali ke Sheets.

> Data di sini bersifat simulasi/fiktif untuk pengujian database — bukan hasil survei, quick count, exit poll, atau prediksi Pemilu.

## Isi repo

- `index.html` — dasbor: peta pulau Indonesia, grafik, tabel yang bisa diedit langsung, profil paslon.
- `Code.gs` — backend Google Apps Script (API baca + tulis ke Sheets).

## Cara pasang

### 1. Google Sheets + Apps Script
1. Buka Google Sheet yang punya sheet `Database Simulasi` dan `Catatan`.
2. **(Opsional, untuk foto paslon)** Tambah sheet baru bernama `Paslon` dengan header:
   `Pasangan | FotoURL` — isi `Pasangan` persis sama dengan nama kolom di `Database Simulasi`
   (mis. `Purbaya–Sherly`), dan `FotoURL` dengan link gambar pilihanmu sendiri. Kalau
   dikosongkan, dasbor otomatis memakai avatar inisial.
3. **Ekstensi → Apps Script**, tempel isi `Code.gs`.
4. **Project Settings (ikon gerigi) → Script Properties → Add script property**:
   - Property: `EDIT_TOKEN`
   - Value: kata sandi bebas buatanmu sendiri (ini yang diminta situs sebelum bisa mengedit).
5. **Deploy → Kelola Penerapan → Penerapan Baru**:
   - Jenis: **Aplikasi Web**
   - Execute as: **Saya (Me)**
   - Siapa yang punya akses: **Siapa saja (Anyone)**
6. Salin URL yang berakhiran `/exec`.

### 2. GitHub Pages
1. Buat repo baru, unggah `index.html`.
2. Buka `index.html`, isi baris:
   ```js
   const API_URL = "https://script.google.com/macros/s/XXXXXXXX/exec";
   ```
3. **Settings → Pages → Deploy from branch → main / root**.
4. Situs tersedia di `https://<username>.github.io/<nama-repo>/`.

## Cara pakai fitur edit

1. Buka situs, klik **"Aktifkan mode edit"**.
2. Masukkan `EDIT_TOKEN` yang kamu set di langkah 4 di atas.
3. Sel angka pada tabel berubah jadi kotak input — ubah angkanya, klik di luar kotak untuk menyimpan.
4. Perubahan langsung ditulis ke Google Sheets ("Total Responden" per wilayah dan baris `TOTAL` dihitung ulang otomatis), lalu dasbor (peta, grafik, kartu total) memuat ulang data terbaru.

Kalau `API_URL` dikosongkan, situs tetap bisa dibuka (pakai data cadangan bawaan) tapi mode edit dinonaktifkan — karena tidak ada database untuk ditulisi.

## Catatan soal foto paslon

Kolom foto sengaja dibuat opsional dan kosong secara default (avatar inisial). Kalau salah satu
"pasangan" di datamu memakai nama tokoh publik sungguhan, sebaiknya isi `FotoURL` dengan
ilustrasi/gambar buatan sendiri, bukan foto asli tokoh tersebut — supaya dasbor simulasi ini
tidak berpotensi disalahartikan sebagai jajak pendapat/survei yang sungguhan.
