# Pasang Tekstur Senjata Custom (Java + Bedrock)

Isi paket ini:
| File | Untuk | Taruh di mana |
|---|---|---|
| `FantasyRPG-Java-Pack.zip` | Pemain **Java** | Di-upload ke link internet (lihat Langkah 1) |
| `FantasyRPG-Bedrock.mcpack` | Pemain **Bedrock** | `plugins/Geyser-Spigot/packs/` |
| `fantasyrpg_mappings.json` | Geyser | `plugins/Geyser-Spigot/custom_mappings/` |
| `sha1.txt` | Kode verifikasi pack Java | dipakai di server.properties |
| `preview.png` | Contoh tampilan 13 tekstur | - |

13 senjata punya tekstur sendiri. **Windpiercer dan Starfall (busur/crossbow) sengaja tetap tampil vanilla**
karena animasi tarik busur tidak bisa dipindah ke Bedrock lewat pemetaan item biasa.

## Prasyarat
- Plugin FantasyRPG versi terbaru (yang ada perintah `/rpg refresh`).
- Geyser yang mendukung format pemetaan item **v2** (Geyser API 2.9.3 / build 1062 ke atas; versi terbaru aman).
- Pack Java ini dibuat untuk Minecraft Java **26.1 - 26.2**.

## Langkah 1 - Pack Java (pemain Java)
1. Upload `FantasyRPG-Java-Pack.zip` (JANGAN diekstrak/diubah) ke tempat yang memberi **link langsung ke file**:
   - GitHub: buat repository **public**, upload zip-nya, lalu pakai link
     `https://raw.githubusercontent.com/USERNAME/REPO/main/FantasyRPG-Java-Pack.zip`
   - atau Dropbox (ubah akhir link jadi `?dl=1`), atau web storage dari hosting kamu.
2. Buka file `server.properties` di panel hosting, isi:
```
resource-pack=LINK_LANGSUNG_DI_ATAS
resource-pack-sha1=ff7164637f7a3560f8556861b0718ed9aa466b19
require-resource-pack=true
```
3. Restart server. Pemain Java akan diminta menerima pack saat join.

> Jika kamu mengubah isi zip, kode SHA-1 berubah. Hitung ulang (`sha1sum nama.zip` atau alat SHA-1 online).

## Langkah 2 - Pack Bedrock (pemain Bedrock, lewat Geyser)
1. Upload `FantasyRPG-Bedrock.mcpack` ke `plugins/Geyser-Spigot/packs/`.
2. Upload `fantasyrpg_mappings.json` ke `plugins/Geyser-Spigot/custom_mappings/`
   (folder dibuat otomatis saat Geyser pertama jalan).
3. Buka `plugins/Geyser-Spigot/config.yml`, cari `enable-custom-content` dan ubah jadi `true`.
4. Restart server. Pemain Bedrock harus **keluar lalu join lagi** agar pack terunduh.

## Langkah 3 - Aktifkan di plugin
1. Di `plugins/FantasyRPG/config.yml` ubah `use-custom-models: false` menjadi `true`.
2. Restart server.
3. Senjata yang sudah ada di inventory diperbarui otomatis saat pemain join, atau manual lewat `/rpg refresh`.

Urutan penting: pasang Langkah 1 dan 2 **dulu**, baru aktifkan Langkah 3.
Kalau Langkah 3 diaktifkan sebelum pack terpasang, item tampil sebagai kotak ungu-hitam.

## Kalau ada masalah
| Gejala | Kemungkinan penyebab |
|---|---|
| Java: kotak ungu-hitam | Pack belum diterima pemain / link atau SHA-1 salah / pack ditolak |
| Java: tampil seperti pedang vanilla | `use-custom-models` masih false, atau jalankan `/rpg refresh` |
| Bedrock: tampil pedang vanilla | `enable-custom-content` belum true, file mapping salah folder, atau Geyser terlalu lama |
| Bedrock: ikon kosong / tanda tanya | Pemain belum menerima pack Bedrock (join ulang), atau nama di `item_texture.json` tidak cocok |
| Resep craft tidak tampil di buku resep Bedrock | Normal: lihat resep lewat `/rpg weapons` |

Cek juga console server saat startup: Geyser mencetak error jika file pemetaan salah.
Kalau ada pesan error, kirim ke saya untuk diperbaiki.

## Ubah desain sendiri
Semua tekstur berukuran 16x16 px (PNG transparan). Ganti file di:
- Java: `assets/fantasyrpg/textures/item/NAMA.png` di dalam zip
- Bedrock: `textures/items/fantasyrpg/NAMA.png` di dalam mcpack
Nama file harus sama dengan ID senjata (mis. `emberfang.png`). Setelah ganti, hitung ulang SHA-1 pack Java.
