# Buku Poin

Aplikasi web (PWA) untuk mencatat poin pelanggaran dan penebusan. Bisa dipasang di layar utama HP dan jalan offline. Data tersimpan di perangkat (localStorage), tidak dikirim ke mana pun.

## Struktur
- `public/` : isi aplikasi (index.html, manifest, service worker, ikon)
- `.github/workflows/pages.yml` : otomatis deploy ke GitHub Pages setiap push ke `main`

## Cara pasang di GitHub
1. Buat repo baru di github.com (misalnya `buku-poin`). Gunakan **Public**; GitHub Pages untuk repo private butuh paket berbayar.
2. Unggah semua isi folder ini. Lewat terminal:
   ```
   git init -b main
   git add .
   git commit -m "Buku Poin"
   git remote add origin https://github.com/USERNAME/buku-poin.git
   git push -u origin main
   ```
   (Lewat browser: Add file > Upload files. Pastikan folder `.github/workflows/pages.yml` ikut terunggah; kalau ragu, pakai terminal atau buat file itu manual lewat Add file > Create new file.)
3. Di repo: **Settings > Pages > Build and deployment > Source: GitHub Actions**.
4. Tunggu tab **Actions** hijau (sekitar 1 menit). Alamatnya: `https://USERNAME.github.io/buku-poin/`

## Pasang di HP
- Android (Chrome): menu ⋮ > **Install app** / **Tambahkan ke layar utama**.
- iPhone (Safari): Bagikan > **Tambahkan ke Layar Utama**.

## Catatan
- Data terikat ke browser dan alamat situs. Aplikasi yang dipasang di iPhone memakai penyimpanan terpisah dari Safari, jadi pasang dulu sebelum mulai mencatat, atau pindahkan data lewat menu **Cadangan data**.
- Repo publik berarti aturan awal (nama dan nilai poin di `index.html`) bisa dibaca orang lain. Catatan riwayatmu tidak ikut terlihat. Ubah nama aturan di kode sebelum push kalau ingin lebih privat.
- Setelah mengubah file di `public/`, naikkan nama cache di `sw.js` (`buku-poin-v1` jadi `v2`) supaya HP mengambil versi baru.

## Jadi APK Android (mandiri, tanpa browser)

APK dibuat dengan Capacitor: isi aplikasi dibungkus ke dalam paket Android, jadi berjalan sendiri tanpa internet dan tanpa membuka browser. GitHub hanya dipakai sebagai mesin pembangun APK; setelah APK terpasang, aplikasi tidak bergantung lagi pada GitHub.

1. Pastikan semua file repo ini sudah ada di GitHub, termasuk `package.json`, `capacitor.config.json`, `debug.keystore`, folder `assets/`, dan `.github/workflows/build-apk.yml`.
2. Buka tab **Actions > Build APK > Run workflow**.
3. Tunggu sekitar 5-10 menit sampai hijau.
4. Buka **Releases** (kolom kanan repo), unduh `BukuPoin.apk` dari build terbaru.
5. Di HP, buka file APK dan izinkan "Pasang aplikasi dari sumber tidak dikenal" untuk browser/Files yang kamu pakai.

Catatan:
- Data tersimpan di dalam aplikasi. Update dengan APK baru (build lebih baru) menimpa aplikasi lama dan data tetap ada, karena kunci tanda tangannya sama (`debug.keystore`). Tetap salin **Cadangan data** sebelum update atau sebelum menghapus aplikasi.
- `debug.keystore` adalah kunci debug untuk pemakaian pribadi. Jangan dipakai untuk menerbitkan ke Play Store; untuk itu buat kunci rilis sendiri.
- Android mungkin menampilkan peringatan Play Protect karena aplikasi tidak dari Play Store. Itu wajar untuk APK buatan sendiri.
- Aplikasi memakai komponen sistem Android System WebView (sudah terpasang di HP), bukan aplikasi browser.
