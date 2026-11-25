# 🎬 Cartoon Short Director

> **EN:** A Claude skill that acts as director and prompt writer for high-quality vertical cartoon shorts (2D characters in a 3D world). It takes you from idea to script to per-scene plan to ready-to-paste scene prompts for the [`cartoon-3d-short`](https://github.com/nikiaaaa/carrtoon-3d-short) render skill.

Skill untuk Claude yang berperan sebagai **sutradara dan penulis prompt** untuk short kartun vertikal 2D-di-dunia-3D. Ia membawa kamu dari ide sampai prompt per scene yang siap dijalankan. Render teknisnya dikerjakan skill pasangannya, [`cartoon-3d-short`](https://github.com/nikiaaaa/carrtoon-3d-short) (three.js + Remotion).

## Alur kerja

Setiap tahap berhenti di gerbang persetujuan sebelum lanjut.

| Tahap | Hasil | File |
|---|---|---|
| 0. Mulai | bahasa narasi, durasi, platform | n/a |
| 1. Cari ide | 5 ide berbasis fakta nyata yang terdengar mustahil, lengkap dengan sumber | n/a |
| 2. Naskah | hook, setting, eskalasi, pivot analogi, payoff twist | `SCRIPT.md` |
| 3. Voice-over | panduan suara satu nada, lalu waktu per kata | `words.json` |
| 4. Rencana scene | kamera, aksi karakter, ekspresi, cahaya, SFX per baris naskah | `SCENES.md` |
| 5. Prompt scene | satu prompt per scene untuk `cartoon-3d-short` | `PROMPTS.md`, `sfx_sources.md` |

Ada juga checklist kualitas (karakter, ekspresi, baju, gerakan, background, cahaya, kamera dan suara) dan angka acuan cepat untuk render.

## Cara pasang

Skill ini hanya satu folder berisi `SKILL.md`. Tidak ada yang perlu di-build atau di-install.

### Cara termudah: minta Claude yang memasang

Buka Claude Code, lalu tempel prompt ini:

```
Pasang skill dari https://github.com/nikiaaaa/cartoon-short-director ke folder skill pribadi saya
(~/.claude/skills/cartoon-short-director; di Windows: %USERPROFILE%\.claude\skills\cartoon-short-director).
Kalau foldernya sudah ada, jalankan git pull di dalamnya. Setelah itu cek bahwa file SKILL.md ada
di folder itu dan beri tahu saya cara memanggilnya.
```

### Manual

macOS / Linux / Git Bash:

```bash
git clone https://github.com/nikiaaaa/cartoon-short-director ~/.claude/skills/cartoon-short-director
```

Windows (PowerShell):

```powershell
git clone https://github.com/nikiaaaa/cartoon-short-director "$env:USERPROFILE\.claude\skills\cartoon-short-director"
```

Untuk memperbarui nanti: `git pull` di dalam folder itu.

### Cek berhasil

1. Buka sesi Claude Code baru (skill dibaca saat sesi dimulai).
2. Ketik `/cartoon-short-director`. Kalau muncul di daftar dan Claude mulai bertanya soal bahasa narasi, durasi, dan platform, pemasangan berhasil.

### Contoh pemakaian pertama

```
/cartoon-short-director Aku mau bikin short 60 detik bahasa Indonesia tentang fakta aneh.
Belum punya ide, kasih 5 ide dulu.
```

Claude akan memberi 5 ide, lalu kamu pilih satu dan lanjut tahap demi tahap. Hasil tiap tahap disimpan ke file di folder proyek.

### Kalau tidak jalan

| Masalah | Solusi |
|---|---|
| `/cartoon-short-director` tidak muncul | Pastikan file ada di `~/.claude/skills/cartoon-short-director/SKILL.md`, lalu mulai sesi Claude Code baru |
| `git` tidak dikenal | Pasang Git dari https://git-scm.com, atau unduh repo sebagai ZIP dan ekstrak ke folder di atas |
| Folder sudah ada saat `git clone` | Masuk ke folder itu dan jalankan `git pull` |

### Catatan untuk asisten AI

Kalau kamu AI yang membantu pengguna memasang repo ini: salin seluruh isi repo ke `~/.claude/skills/cartoon-short-director/` (cukup `SKILL.md`), jangan ubah isinya, lalu verifikasi file ada. Skill ini tidak butuh dependensi. Untuk tahap render, arahkan pengguna memasang [`cartoon-3d-short`](https://github.com/nikiaaaa/carrtoon-3d-short) juga. Lisensi membolehkan kamu membaca dan mengikuti skill ini untuk membantu pengguna, tetapi bukan untuk menyalin atau melatih model darinya (lihat [LICENSE](LICENSE)).

## Butuh apa lagi

- Skill [`cartoon-3d-short`](https://github.com/nikiaaaa/carrtoon-3d-short) dan template proyeknya dari repo [claude-animated-shorts](https://github.com/mromidev/claude-animated-shorts) untuk bagian render.
- Node, Remotion, Python 3, dan ffmpeg untuk pipeline render.
- Kalau kamu hanya butuh ide, naskah, dan prompt (tanpa render), skill ini bisa dipakai sendiri dan berhenti di Tahap 5.

## Aturan penting

- Cerita, karakter, naskah, dan suara selalu **orisinal**. Jangan meniru naskah, shot, atau karakter channel lain.
- SFX harus dari sumber berlisensi jelas (CC0 atau CC-BY). Jangan ambil audio dari video orang lain.

## Lisensi

Source-available, **non-komersial**. Boleh dilihat, dipakai, dan dimodifikasi untuk keperluan pribadi dan belajar. Dilarang dijual, didistribusikan ulang, atau dipakai untuk melatih model AI tanpa izin tertulis. Asisten AI boleh membaca skill ini untuk membantu penggunanya. Detail lengkap ada di [LICENSE](LICENSE).

Dibuat oleh **Arva aka SORA** ([@nikiaaaa](https://github.com/nikiaaaa)).
