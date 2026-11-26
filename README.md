# Portofolio Ifeb

Portofolio statis (HTML + Tailwind CDN) untuk Ifeb, siswa DKV SMKN 10 Surabaya. Sudah disiapkan agar bisa di-upload ke GitHub dan langsung dipublish ke **GitHub Pages**.

## Isi folder

| File / folder | Fungsi |
| --- | --- |
| `index.html` | Halaman utama yang akan tampil di GitHub Pages |
| `video/` | Versi video yang sudah dikompres untuk web |
| `favicon.svg` | Ikon tab browser |
| `.nojekyll` | Mencegah GitHub Pages memproses file dengan Jekyll |
| `.gitignore` | Mengabaikan `desktop.ini`, video 4K asli, serta file template lama `DESIGN.md` dan `screen.png` |
| `.gitattributes` | Menyamakan line ending menjadi LF agar tidak ada warning CRLF |

## Yang sudah diperbaiki

- Menambahkan `index.html` sebagai entry point GitHub Pages.
- Mengganti gambar placeholder/emoji dan gambar eksternal `googleusercontent` dengan file karya lokal.
- Tombol panah portofolio sekarang benar-benar berfungsi untuk berpindah karya.
- Modal portofolio: fokus otomatis ke tombol tutup, fokus kembali saat ditutup, Escape untuk keluar.
- Path video diperbaiki (`encodeURI`, bukan `encodeURIComponent`) sehingga `video/nama.mp4` tidak rusak.
- Tahun footer sekarang otomatis mengikuti tahun berjalan.
- Navbar bisa di-scroll di layar kecil tanpa scrollbar yang mengganggu.
- Menambahkan meta description, Open Graph, Twitter Card, theme color, dan favicon.
- Video 4K asli dikompres menjadi versi web yang jauh lebih ringan (total ~21 MB, sebelumnya ~290 MB).

## Yang masih perlu diganti manual

Buka `index.html`, cari komentar:

```html
<!-- TODO: ganti email dan link sosial media berikut dengan akun asli Ifeb -->
```

Lalu ganti:

- `mailto:hello@example.com`
- `https://www.instagram.com/`
- `https://www.tiktok.com/`
- `https://www.linkedin.com/`

Dengan email dan akun asli Ifeb. Saat ini sengaja memakai placeholder karena data belum diberikan.

Untuk preview sosial media yang lebih akurat, ganti nilai `og:image` dengan URL absolut setelah halaman live, misalnya:

```html
<meta content="https://USERNAME.github.io/REPO/IFEB%20FOTO.png" property="og:image"/>
```

## Upload ke GitHub

Git **sudah terpasang** dan folder ini sudah di-`git init` pada branch `main`. Semua file yang dibutuhkan juga sudah di-`git add` (video 4K asli dan `desktop.ini` otomatis terabaikan). Tinggal commit dan push.

### Opsi A — GitHub Desktop (paling mudah)

1. Download dan install [GitHub Desktop](https://desktop.github.com/) jika belum punya.
2. Buka GitHub Desktop → **File → Add Local Repository** → pilih folder ini.
3. Buat commit pertama dengan pesan misalnya `Initial portfolio for GitHub Pages`.
4. Klik **Publish repository**, beri nama misalnya `portofolio-ifeb`, lalu pilih akun GitHub Anda.
5. Setelah publish, buka repository di GitHub → **Settings → Pages**.
6. Pada **Build and deployment**, pilih **GitHub Actions** (workflow sudah disiapkan) atau **Deploy from a branch** → `main` / `/(root)`.
7. Tunggu beberapa menit, lalu buka URL:
   `https://USERNAME.github.io/portofolio-ifeb/`

### Opsi B — Git CLI

Buka terminal di folder ini, atur identitas (sekali saja), lalu commit dan push:

```powershell
git config --local user.name "Nama Anda"
git config --local user.email "email@anda.com"
git commit -m "Initial portfolio for GitHub Pages"
git remote add origin https://github.com/USERNAME/portofolio-ifeb.git
git push -u origin main
```

Ganti `USERNAME` dan nama repo sesuai akun Anda. Repository ini sudah memakai **Deploy from a branch** → `main` / `/(root)`, jadi setiap push ke `main` otomatis membuat ulang GitHub Pages. File `.nojekyll` memastikan tidak ada proses Jekyll.

## Catatan video

File asli 4K sengaja **tidak di-upload** (sudah masuk `.gitignore`) agar repository ringan. Versi yang dipakai website ada di folder `video/`:

| File asli | Versi web |
| --- | --- |
| `Flash card .mp4` | `video/flash-card.mp4` |
| `kentang goreng .mp4` | `video/kentang-goreng.mp4` |
| `squishy .mp4` | `video/squishy.mp4` |
| `i can eat .MOV` | `video/i-can-eat.mp4` (ditampilkan di bagian **Beluga Digital Studio**) |
| `hujan.mp4` | `video/hujan.mp4` |
| `nusantara coffe-.mp4` | `video/nusantara-coffe.mp4` |

Video `video/render.mp4`, foto `BAJU MERDEKA [Recovered]-01.png`, `BAJU MERDEKA TANPA DEPAN.png`, `AFTER EFFECTS NAMA IFEB.png`, dan `Screenshot 2026-07-26 095229.png` sudah dihapus dari website sesuai permintaan. Thumbnail kartu **After Effects** sekarang memakai `video/after-effects-thumb.jpg` yang diambil dari video `nusantara-coffe.mp4`.

Jika ingin mengompres ulang, contoh perintah ffmpeg:

```powershell
ffmpeg -i "kentang goreng .mp4" -vf "scale=720:-2" -c:v libx264 -preset veryfast -crf 30 -c:a aac -b:a 96k -movflags +faststart "video/kentang-goreng.mp4"
```
