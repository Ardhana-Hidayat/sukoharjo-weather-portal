# Portal Cuaca Sukoharjo

Portal pemantauan cuaca sederhana untuk wilayah adm4 `33.11.04.1012` (Sukoharjo), menggunakan data terbuka BMKG. Satu file HTML statis, tanpa framework atau proses build.

## Isi

- `portal-cuaca-sukoharjo.html` — halaman lengkap (HTML, CSS, JS dalam satu file)

## Cara menjalankan

Fetch API tidak boleh dijalankan dari `file://` di sebagian besar browser, jadi jalankan lewat server lokal, contoh:

```bash
# Python
python3 -m http.server 8000

# Node (butuh paket serve)
npx serve .
```

Lalu buka `http://localhost:8000/portal-cuaca-sukoharjo.html`.

Atau upload begitu saja ke hosting statis mana pun (Netlify, Vercel, GitHub Pages, cPanel, dll).

## Sumber data

```
https://api.bmkg.go.id/publik/prakiraan-cuaca?adm4=33.11.04.1012
```

- Data prakiraan 3 hari ke depan, tiap 3 jam.
- Diperbarui BMKG 2x sehari.
- Batas akses: 60 permintaan/menit per IP.
- Wajib mencantumkan BMKG sebagai sumber data (sudah ada di footer halaman).

## Mengganti lokasi

Ganti nilai `ADM4` di bagian `<script>` pada file HTML dengan kode wilayah tingkat IV (kelurahan/desa) lain, mengacu ke Kepmendagri No. 100.1.1-6117 Tahun 2022.

## Catatan

- Jika request ke API BMKG diblokir CORS saat deploy, tambahkan proxy sederhana (Node/PHP) yang meneruskan request ke BMKG, lalu ubah `API_URL` di script mengarah ke proxy tersebut. Ini belum diverifikasi langsung terhadap respons live API.
- Nama field JSON (`t`, `hu`, `weather_desc`, `ws`, `tcc`, `vs_text`, dst.) diambil dari dokumentasi resmi BMKG. Jika struktur respons live sedikit berbeda, sesuaikan di fungsi `render()` dalam file HTML.
