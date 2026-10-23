# 🎓 LPDP AI Mock Interviewer

Simulasi wawancara substansi **Beasiswa LPDP** berbasis suara (*voice-to-voice*) dengan panel AI tiga peran: **Psikolog**, **Akademisi**, dan **Panelis LPDP**. Panel bersikap tajam dan kritis, serta menggali jawaban dangkal dengan *probing questions*. Konteks kandidat: MSc Artificial Intelligence, University of Edinburgh.

Semuanya berjalan **di browser**, dalam satu file `index.html`, tanpa backend.

**▶ Coba langsung:** https://zenrega38.github.io/lpdp-mock-interviewer/

## Fitur

- **Voice-to-voice.** Jawab dengan suara (Web Speech API), dan panel menjawab dengan suara (Speech Synthesis). Transkrip tampil secara real-time.
- **Mode mikrofon.** *Tahan untuk bicara* (tombol atau `Spasi`) atau *klik mulai, klik kirim* (lebih nyaman di HP).
- **Timer jawaban 90 detik.** Muncul di pojok setelah panelis selesai bertanya. Lewat batas tidak menghentikan apa pun, hanya tampil sebagai *+detik*. Durasinya dikirim ke AI sebagai catatan tersembunyi (tidak tampil di transkrip, tidak ditegur selama sesi) dan dipakai di evaluasi akhir.
- **Ruang rapat.** Tampilan ala Zoom: tiga panelis dengan kamera mati, kamera Anda menyala, penanda pembicara aktif, suara berbeda per panelis, *live caption*, dan panel chat.
- **Knowledge base pribadi.** Panel memakai profil, berkas, dan bank pertanyaan Anda (lihat [`raw/README.md`](raw/README.md)).
- **Mode sesi.** Sesi penuh (±45 menit), fokus per kategori (A sampai N, S), audit berkas, dan sesi tekanan.
- **Evaluasi akhir.** Skor per panelis (0–100), rubrik tujuh dimensi (1–5), ID pertanyaan, tanda merah, fakta yang perlu diverifikasi, dan rencana latihan 3 hari.
- **Tahan gangguan.** Coba ulang otomatis saat terkena *rate limit* (429) atau server sibuk, sesi tersimpan otomatis (bisa dilanjutkan setelah *refresh*), dan transkrip bisa diunduh.
- Bahasa **Indonesia / English**, pilihan model Gemini, suara, dan kecepatan bicara.

## Cara pakai

1. Buat **Gemini API key** gratis di [Google AI Studio](https://aistudio.google.com/apikey).
2. Buka aplikasinya (link di atas, atau jalankan lokal).
3. Tempel API key, pilih bahasa, lalu muat knowledge base (opsional tapi disarankan).
4. Klik **Mulai sesi**, jawab pertanyaan panel, lalu klik **Akhiri & nilai** untuk laporan evaluasi.

### Menjalankan lokal

```bash
git clone https://github.com/ZenRega38/lpdp-mock-interviewer.git
cd lpdp-mock-interviewer
# letakkan file knowledge base Anda di raw/ (lihat raw/README.md)
python -m http.server 8000
# buka http://localhost:8000
```

Gunakan `http://localhost`, bukan membuka file langsung (`file://`), agar izin mikrofon/kamera stabil dan folder `raw/` bisa dimuat otomatis.

## 🔐 Keamanan API key & data pribadi

- **API key tidak pernah ada di repo ini.** Key hanya diketik di browser dan dikirim langsung ke `generativelanguage.googleapis.com` lewat header `x-goog-api-key`, tidak ke server lain.
- Key **tidak disimpan** kecuali Anda mencentang *"Ingat API key di browser ini"* (disimpan di `localStorage` browser Anda saja).
- Setiap pengunjung versi online memakai **API key miliknya sendiri**.
- Untuk ekstra aman, batasi key Anda di [Google Cloud Console → Credentials](https://console.cloud.google.com/apis/credentials): *Application restrictions → Websites* → `zenrega38.github.io/*` dan `localhost:*`.
- Folder `raw/` (data pribadi) **diabaikan oleh Git**. Hanya `raw/README.md` yang di-commit.
- Riwayat sesi dan knowledge base yang dipilih manual disimpan di `localStorage` perangkat Anda dan dikirim hanya ke Gemini saat wawancara berjalan.

## Dukungan browser

| Fitur | Chrome / Edge (desktop & Android) | Safari (macOS/iOS) | Firefox |
|---|---|---|---|
| Speech-to-text | ✅ | ⚠️ terbatas | ❌ (pakai kolom ketik) |
| Text-to-speech | ✅ | ✅ | ✅ |
| Kamera (Ruang rapat) | ✅ | ✅ | ✅ |

Speech-to-text di Chrome/Edge memakai layanan cloud browser, jadi butuh koneksi internet.

## Catatan kuota

Tier gratis Gemini memiliki batas permintaan per menit dan per hari. Dengan knowledge base lengkap, tiap giliran mengirim sekitar 45 ribu token. Jika muncul error 429, aplikasi otomatis menunggu lalu mencoba lagi; jika kuota harian habis, ganti ke model Flash-Lite.

## Teknologi

HTML + Tailwind CSS (CDN) + JavaScript murni · Web Speech API · Speech Synthesis API · MediaDevices (kamera) · Google Gemini REST API.

---

*Materi latihan, bukan dokumen resmi LPDP atau University of Edinburgh, dan bukan jaminan kelulusan.*
