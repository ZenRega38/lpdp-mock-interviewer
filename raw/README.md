# Folder `raw/`: Knowledge Base Kandidat

Folder ini berisi **basis pengetahuan pribadi** yang dibaca AI interviewer: profil kandidat, temuan audit berkas, bank pertanyaan, dan protokol sesi.

> **Isi folder ini tidak pernah di-upload ke GitHub.** Semua file di `raw/` (kecuali README ini) diabaikan lewat `.gitignore` karena berisi data pribadi (CV, esai, dan informasi sensitif). Simpan salinannya sendiri di tempat yang aman.

## File yang diharapkan

| File | Fungsi | Wajib? |
|---|---|---|
| `LPDP_Mock_Interviewer_Knowledge_Base_Rega.md` | Basis pengetahuan: profil kandidat, konteks seleksi, temuan audit berkas, data riset, rubrik penilaian, dan bank pertanyaan. | Disarankan |
| `Sistem_Prompt_Mock_Interviewer_LPDP.md` | Protokol sesi: peran panel, aturan sesi, alur, format umpan balik, dan nada. | Opsional |

Nama file harus persis seperti di atas agar dimuat otomatis saat aplikasi dijalankan lewat `localhost`. Jika memilih file secara manual, nama bebas. File yang namanya mengandung `sistem_prompt`/`system_prompt` dianggap protokol, sisanya dianggap basis pengetahuan (bisa lebih dari satu file).

## Struktur yang dikenali aplikasi

Aplikasi mengirim isi file ke Gemini apa adanya, dengan beberapa aturan khusus berdasarkan judul bagian (heading Markdown):

| Heading / pola | Perlakuan |
|---|---|
| `- Nama: <nama lengkap>, ...` | Dipakai sebagai nama Anda di tampilan Mode Zoom. |
| `### 2.10 ...` (faktor pribadi sensitif) | **Tidak dikirim** ke AI kecuali Mode Sensitif (Kategori S) dipilih. |
| `### Kategori S ...` (pertanyaan sensitif) | **Tidak dikirim** kecuali Mode Sensitif dipilih. |
| `## 10. ...` (daftar sumber) | Selalu dibuang untuk menghemat token. |
| `## 4.` Temuan audit, `### 6.2` Rubrik, `## 9.` Bank pertanyaan, `### 5.7` Hal yang belum diketahui | Dirujuk oleh aturan panel (probe konsistensi, rubrik tujuh dimensi, ID pertanyaan seperti A1/J3, dan pertanyaan klarifikasi). |

Kategori bank pertanyaan yang dipakai Mode Sesi: **A** Pembuka, **B** Motivasi & Kampus, **C** Akademik & Riset, **D** Skema & Isu Nasional, **E** Kontribusi, **F** Nilai LPDP & Integritas, **G** Psikologi, **H** Kepemimpinan, **I** Pengalaman Kerja, **J** Serangan pada Berkas, **K** Isu Terkini, **L** Rencana Cadangan, **M** Penutup, **N** Bahasa Inggris, **S** Sensitif.

## Cara memuat

- **Lokal:** letakkan file di folder ini, jalankan `python -m http.server 8000` dari root proyek, lalu buka `http://localhost:8000`. File dimuat otomatis.
- **Online (GitHub Pages) / file://:** klik **📂 Pilih file .md…** di panel *Knowledge Base & Mode Sesi*, lalu pilih file Anda. Isinya disimpan di `localStorage` browser Anda saja (tombol **Hapus** untuk membersihkan).

Isi knowledge base dikirim ke Google Gemini sebagai bagian dari system prompt setiap giliran (sekitar 45 ribu token untuk file contoh). Jangan memuat data yang tidak ingin Anda kirim ke Google.
