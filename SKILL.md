---
name: "cartoon-short-director"
description: "Sutradara dan panduan prompt untuk short kartun 2D-di-dunia-3D kualitas tinggi: ide, naskah, rencana tiap scene, lalu prompt per scene untuk cartoon-3d-short. Pakai saat user mau bikin video baru atau minta prompt scene."
---

# Cartoon Short Director

Skill ini adalah sutradara dan penulis prompt. Ia membawa user dari ide sampai prompt per scene yang siap dijalankan. Render teknisnya memakai skill `cartoon-3d-short` (three.js + Remotion) dan dua dokumen spesifikasi: rig "Spesifikasi Teknis: Kerangka 3D, IK, dan Baju Silinder" (https://claude.ai/artifact/Y1oLh8ZW7XUzfewpGrWBvT) serta "Spesifikasi Teknis: Ekspresi, Dunia, dan Cahaya" (https://claude.ai/artifact/JdyDwYt7ZvZxdfwjL9kFKp). Patokan gaya adalah video breakdown yang kita pelajari: kalau aturan repo bertentangan dengan video, ikuti video.

## Aturan main
- Cerita, karakter, naskah, dan suara selalu orisinal. Jangan meniru naskah, shot, atau karakter channel referensi, dan jangan sebut nama channel itu di VO atau deskripsi.
- Kerjakan bertahap dengan persetujuan di tiap gerbang: Ide, Naskah, Rencana scene, Prompt scene. Setelah naskah disetujui, lanjutkan tanpa banyak bertanya.
- Simpan tiap tahap ke file proyek: `SCRIPT.md`, `SCENES.md`, `PROMPTS.md`, `sfx_sources.md`, `CREDITS.txt`.
- Jawab user dalam bahasanya. Bahasa narasi ditanyakan sekali di awal.
- Kalau user hanya minta prompt (tanpa render), berhenti di Tahap 5.

## Tahap 0 - Mulai
1. User membawa ide: lanjut ke Tahap 2. Belum ada ide: Tahap 1.
2. Tanyakan hanya yang belum diketahui: bahasa narasi, durasi target (default 60 s), platform (TikTok/Shorts/Reels, 1080x1920, 30 fps), dan apakah pipeline render (repo + rig) sudah siap.

## Tahap 1 - Cari ide
Beri 5 ide. Setiap ide harus lolos semua syarat:
- Fakta nyata yang terdengar mustahil (paradoks), dengan sumber yang bisa dicek. Cari dan buka sumbernya, jangan dari ingatan.
- Ada sebab-akibat fisik yang terlihat: benda bergerak, rusak, jatuh, tumpah, meledak.
- Bisa dijelaskan dengan satu analogi sehari-hari.
- 1-3 lokasi dan 1-3 karakter utama (maksimal 4 karakter berkerangka per shot).
- Ada aksi tubuh yang butuh kerangka 3D (duduk, berlutut, memegang alat, jatuh) dan reaksi dunia (bengkok, penyok, percikan, goresan).
- Ending bisa jadi twist ironis.

Format per ide: Judul kerja | Hook 1 kalimat | Fakta inti + sumber | Analogi | Lokasi dan waktu (siang/sunset/malam) | Aksi andalan | Twist.

## Tahap 2 - Naskah
Panjang: jumlah kata = durasi x 3,7 (60 s = sekitar 220 kata). Kalimat median 13-14 kata, bahasa lisan, singkatan boleh, tanpa jargon yang tidak dijelaskan.

Struktur beat:
1. Hook: paradoks dinyatakan sebagai fakta, 10-16 kata, tanpa pembukaan.
2. Setting: 1-2 kalimat present tense dengan waktu, tempat, tokoh biasa bernama, dan angka.
3. Eskalasi: 3-6 beat, tiap beat lebih besar. Ada yang meragukan atau mengejek. 1-2 lelucon hiperbola yang berupa fakta hasil riset.
4. Misteri: satu momen "Wait..." atau pertanyaan.
5. Pivot: "You see," lalu mekanisme sebenarnya lewat analogi sehari-hari.
6. Opsional, deadpan ganda: "Luckily... / Unluckily...".
7. Konsekuensi: aturan atau perubahan yang lahir dari kejadian itu.
8. Payoff: twist ironis 1-2 kalimat. Video berakhir tepat di kata terakhir.

Larangan: jangan mendeskripsikan apa yang sudah terlihat di layar. Tanpa intro, logo, outro, atau CTA.

Output `SCRIPT.md`: fakta dan sumber di atas, lalu naskah bernomor per baris (L01, L02, ...) dengan perkiraan detik.

## Tahap 3 - Voice-over
- Satu suara, nada stabil, deadpan, cepat: 3,5-4,1 kata/detik (sekitar 210-246 WPM, target 222).
- Hampir tanpa jeda: total jeda di atas 0,25 s kurang dari 1 s per video. Suara mulai di frame 1-4.
- Lucunya datang dari isi kalimat, bukan intonasi.
- Setelah direkam atau di-generate, buat `words.json` (waktu per kata) dan perbaiki manual. Semua timing visual mengikuti file ini.

Template prompt generator suara (mis. ElevenLabs), angka setelan hanya titik awal untuk dicoba:
```
Narator pria, kering dan deadpan, tempo cepat dan stabil, hampir tanpa jeda,
tidak dramatis, seperti menceritakan fakta aneh dengan wajah datar.
Target kecepatan sekitar 222 kata per menit. Bahasa: {bahasa}.
Naskah: {tempel naskah final}
```

## Tahap 4 - Rencana setiap scene (wajib sebelum apa pun dibuat)
AI hanya sepintar orang yang mem-prompt-nya. Rencanakan kamera, sudut, aksi setiap karakter, dan apa yang terjadi di setiap baris VO sebelum membangun apa pun.

Buat `SCENES.md`, satu blok per baris naskah:

| Kolom | Isi |
| --- | --- |
| Baris | L07 + teks VO |
| Frame | rentang dari words.json, kata kunci + frame-nya |
| Lokasi dan waktu | mis. jalan raya, siang/sunset/malam |
| Sudut kamera | pilih dari daftar sudut di bawah |
| Gerakan kamera | hold + push-in, glide ke objek, follow, fly-through, crossfade 6-8 f, shake (tanpa hard cut) |
| Pose dan aksi karakter | per karakter: jalan, duduk di mobil, berlutut, memungut, jatuh; target tangan/kaki atau grip prop |
| Ekspresi | campuran emosi berbobot, mis. kaget 0,4 + khawatir 0,6 |
| Baju dan aksesoris | arah hadap, topi, prop yang dipegang |
| Reaksi dunia | goresan, percikan, debu, pagar bengkok, mobil penyok, pintu terbuka |
| Cahaya | preset + perubahan (lampu mobil menyala, bayangan awan) |
| SFX | nama efek @ frame |
| Musik | mulai, naik, turun |

Aturan rencana:
- Setiap kalimat diilustrasikan secara harfiah. Properti yang membawa leluconnya.
- Saat VO menyebut objek atau aksi, kamera zoom in halus ke situ, lalu mundur pelan.
- Tanpa hard cut dan tanpa lompatan mendadak. Pindah tempat atau waktu memakai gerakan kontinu (ikuti objek, fly-through, crane) atau crossfade 6-8 f.
- Setiap aksi yang mengubah dunia ditulis sebagai event (lihat kolom Reaksi dunia): satu event menggerakkan efek visual, SFX, camera kick, dan baris kredit sekaligus.
- Reaksi visual jatuh 0-3 frame sebelum katanya.
- Waktu berubah mengikuti beat cerita (siang, lalu sunset, lalu malam untuk penjelasan atau klimaks).
- Jangan lebih dari 2 scene berurutan dengan sudut yang sama.

### Daftar sudut kamera
- Setinggi jalan/tanah, di samping detail (goresan, kaki, roda).
- Tinggi, memandang ke bawah sepanjang jalan (establishing).
- Lewat jendela samping mobil.
- POV pengemudi atau karakter.
- Close-up wajah, DOF aktif, fokus di mata.
- Medium; lensa sekitar 2,5 m kalau ada pagar atau rel supaya tidak memotong torso.
- Insert objek (gergaji, termos, tombol).
- Dutch tilt 4-8 derajat untuk drama atau jatuh.

## Tahap 5 - Prompt per scene
Setelah `SCENES.md` disetujui, tulis `PROMPTS.md`: satu prompt per scene, siap ditempel ke Claude Code yang memakai skill `cartoon-3d-short`.

Prompt master (sekali di awal proyek):
```
Pakai skill cartoon-3d-short. Proyek baru "{nama}". Salin templates/bridge ke
src/videos/{nama}/ dan daftarkan komposisinya. Baca SCRIPT.md, words.json, SCENES.md,
PROMPTS.md. Ikuti spesifikasi rig (kerangka 3D, IK, baju silinder) untuk karakter utama, dan spesifikasi ekspresi, dunia, dan cahaya untuk wajah, semua prop (dibangun dari kode, tanpa aset unduhan), event dunia, dan lampu.
Kerjakan satu scene per putaran sesuai PROMPTS.md. Setelah tiap scene, render still di
frame yang disebut dan tunjukkan ke saya sebelum lanjut.
```

Template prompt per scene:
```
SCENE {n} - L{xx}: "{teks VO}"
Frame: {a}-{b} (kata kunci "{kata}" @ {f})
Lokasi/waktu: {...}; preset cahaya {day|golden|night}; perubahan: {...}
Kamera: sudut {...}; gerakan {...} selama {n} f, smootherstep; DOF cInf {px}; roll {derajat};
        kick di frame {f} bila ada benturan
Karakter:
 - {nama}: pose {...}; root {posisi}; yaw {...}
   tangan L/R -> {target atau grip prop.anchor, mode reach|hold|carry}; kaki -> {...}
   ekspresi {emosi a bobot + emosi b bobot}, transisi mulai frame {f}:
   alis dulu, mulut menyusul +2 f; ganti bentuk mata di dalam kedipan + bounce kepala kecil
   baju/aksesoris: {...}
Dunia: objek baru {...} dibangun dari kode per bagian; animasi {pintu buka @ f, roda, pagar bengkok @ f};
       efek {percikan, debu}
SFX: {efek} @ {f} (sumber + lisensi). Musik: {...}
Cek: still di frame {f1}, {f2} harus memperlihatkan {...}
```

Template prompt objek dari kode:
```
Bangun {objek} dari kode di build.ts sebagai THREE.Group, bagian per bagian: {daftar bagian}.
Bagian yang bergerak punya pivot sendiri: {pintu di engsel, roda di as, mata gergaji}.
Interior: {jok, pedal, dasbor, panel pintu tebal}. Tekstur dilukis di paint.ts:
{retak, kerikil, jahitan, kotoran, baut}. Titik pegangan: {grip_L, grip_R, wheel_10, wheel_2}.
Deformasi: {pagar bengkok di titik tabrak, vertex digeser sesuai jarak dan waktu}.
Tidak ada aset unduhan.
```

Template prompt revisi:
```
Scene {n}, frame {f}: {masalah yang terlihat}. Seharusnya: {...}.
Ubah hanya {file}. Render ulang still {f} dan tunjukkan sebelum/sesudah.
```

## Checklist kualitas: 7 pilar + planning
Tiap pilar: masalah yang dipecahkan, teknik, cek.

1. Karakter dan shading. Masalah: wajah satu warna terlihat datar. Teknik: wajah putih, cel shading di satu sisi, highlight tipis di tepi, semuanya mengikuti arah matahari. Cek: saat karakter atau cahaya berputar, bayangan ikut pindah.
2. Ekspresi. Masalah: set wajah tetap (senang/sedih/marah) terasa terbatas. Teknik: wajah parametrik dari emosi saat itu, emosi bisa dicampur; transisi beberapa frame, alis dulu lalu mulut; ganti bentuk mata disembunyikan di kedipan + bounce kepala. Cek: tidak ada ekspresi yang patah dalam 1 frame kecuali kedipan.
3. Baju dan aksesoris. Masalah: baju selalu menghadap kamera atau loncat sudut. Teknik: baju dibungkus silinder tak terlihat; garis, kancing, dasi, saku bergeser dan memadat di tepi; disinari cahaya scene (sisi terang/gelap, kilau, highlight tepi, lipatan); bayangan pohon/atap jatuh ke baju; topi dan rambut digambar ulang tiap frame mengikuti kepala dengan highlight sendiri; benda yang dipegang adalah objek 3D asli dan tangan menggenggamnya. Cek: putaran 360 derajat tanpa loncatan.
4. Gerakan. Masalah: character sheet membuat karakter selalu berdiri dengan kaki lurus. Teknik: kerangka 3D (pinggul, dada, kepala, lutut, siku, tangan, kaki) + IK; kaki menapak tanpa slip, sendi menekuk benar, tangan meraih objek nyata; digambar ulang 2D tiap frame. Cek: slip kaki maksimal 1,1 px/frame; bisa duduk, berlutut, lompat, jatuh, mengayun palu.
5. Background dan objek. Masalah: background datar, warna polos, bentuk sederhana. Teknik: semua dibangun dari kode per bagian; bagian bergerak sendiri (pintu, roda, mata gergaji); bertekstur (retak, kerikil, jahitan, kotoran, baut); ladang sampai horizon; dunia bereaksi pada cerita (goresan, percikan, debu, pagar bengkok, mobil penyok, kamera bergetar). Cek: setiap aksi di naskah meninggalkan jejak di dunia.
6. Lighting. Masalah: cahaya rata tanpa bayangan. Teknik: satu matahari sebagai sumber; bayangan nyata; bayangan awan bergerak di ladang; highlight kecil hanya di benda mengilap (mobil, gergaji, helm); waktu berjalan siang-sunset-malam dengan lampu mobil yang menerangi jalan; karakter disinari matahari yang sama; wajah tetap putih bersih di malam hari; bayangan objek jatuh ke karakter. Cek: still siang, sunset, dan malam.
7. Kamera dan suara. Masalah: kamera statis atau meloncat, suara terdengar palsu. Teknik: kamera mengikuti cerita, zoom in halus ke objek yang disebut lalu keluar, semua gerakan pelan; sudut kreatif dari daftar; SFX rekaman asli di frame kejadian; musik di bawah suara. Cek: setiap objek yang disebut VO mendapat gerakan kamera; setiap kejadian punya SFX dalam 1 frame.
8. Planning. Setiap scene direncanakan lengkap (Tahap 4) sebelum dibuat.

## SFX, musik, dan lisensi
- Sumber: Freesound dan Pixabay (efek suara dan musik). Jangan ambil audio dari video orang lain.
- Freesound CC0: boleh, kredit opsional (tetap dicantumkan). CC BY 3.0/4.0: boleh, kredit WAJIB (judul, pembuat, link, lisensi). CC BY-NC dan Sampling+: JANGAN dipakai, karena video yang dimonetisasi, disponsori, atau berisi afiliasi termasuk komersial.
- Pixabay Content License: boleh komersial, kredit tidak wajib (tetap dicantumkan). Musik Pixabay kadang tetap kena klaim Content ID YouTube: unduh sertifikat lisensi lagunya dan simpan untuk sengketa.
- Catat setiap file di `sfx_sources.md`: id | file | judul | pembuat | url | sumber | lisensi | tanggal unduh | bukti | frame dipakai. Simpan screenshot halaman atau sertifikat di `audio/licences/`.
- Buat `CREDITS.txt` untuk deskripsi postingan, satu baris per file yang dipakai: `"Judul" by Pembuat (URL) - Lisensi`, dikelompokkan Sound effects / Music. Jangan render final kalau ada file tanpa lisensi tercatat.
- Kalau Claude Code tidak bisa mengunduh (perlu login), user mengunduh ke `audio/sfx_raw/` dan menempelkan URL halamannya.
- Letakkan SFX di frame kejadian visual, biasanya 0-1 frame setelah kontak.
- Mix: loudness akhir -14 LUFS; musik dan SFX 5-10 dB di bawah suara, musik ducking saat ada suara.
- Pilih musik setelah video selesai: coba 2-3 lagu di atas render final, pilih yang paling pas.
- Kalau user memilih SFX sintesis, pakai pipeline audio bawaan cartoon-3d-short.

## Angka acuan cepat
- Format 1080x1920, 30 fps; final 1440x2560.
- Kamera: gerakan sekitar 23 f ease-in-out; glide 18-40 f; push-in saat hold 0,15-0,35%/f, 0,6%/f di kata penting; roll 3,6-8 derajat; shake berbalik arah tiap frame sekitar 3 px, hilang dalam 6-8 f; tanpa hand-held.
- Karakter: tinggi 3,5 HH; wajah luma sekitar 0,93; tinta plum #241726; kedip 3-4 f tiap 0,5-2,3 s dan setiap ganti ekspresi; mulut mendahului suara 0-1 f; langkah 9-12 f; bob 3-7%; condong 1-7 derajat.
- Lighting: bayangan sunset violet-biru; kepala tetap terang (V minimal 0,86); specular kecil pada semua benda mengilap seperti di video (cat mobil, logam, mata gergaji, helm proyek, kaca), tidak pada kayu, tanah, kain, dan wajah.

## Keluaran per proyek
`SCRIPT.md`, `words.json`, `SCENES.md`, `PROMPTS.md`, `sfx_sources.md`, `CREDITS.txt` (siap tempel ke deskripsi), lalu video final dan catatan. Akhiri tiap tahap dengan ringkasan 1-2 kalimat dan pertanyaan persetujuan.