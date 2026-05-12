# Day 4: Script Execution Permissions

Tugas kali ini berhubungan dengan Linux Permissions. Ini krusial karena di dunia nyata (terutama saat kamu mengerjakan project Cloud Engineering), script otomatisasi sering kali gagal jalan hanya karena masalah perizinan (permission).

## 1. Login ke App Server 1
Gunakan detail SSH dari tombol "Details". Username untuk Server 1 biasanya adalah `tony`.

```bash
ssh tony@stapp01
```
![images](/imgs_DevOps/day4.png)

---

## 2. Cek Permission Saat Ini (Opsional tapi Penting)
Sebelum mengubah apa pun, sebaiknya cek status file tersebut:

```bash
ls -l /tmp/xfusioncorp.sh
```
![images](/imgs_DevOps/day4_1.png)

---

## 3. Berikan Izin Eksekusi untuk Semua User
Gunakan perintah `chmod` (change mode). Instruksi meminta agar semua user bisa mengeksekusinya, jadi kita gunakan kode `+x` atau `755`.

```bash
sudo chmod +x /tmp/xfusioncorp.sh
```
![images](/imgs_DevOps/day4_2.png)

---

## 4. Verifikasi Hasilnya
Cek kembali filenya dengan perintah `ls`:

```bash
ls -l /tmp/xfusioncorp.sh
```
![images](/imgs_DevOps/day4_3.png)

---

### Kesimpulan untuk Dokumentasi:

Langkah ini dilakukan untuk memastikan operabilitas script otomatisasi. Dalam sistem Linux, sebuah file teks (meskipun isinya kode bash) tidak akan dianggap sebagai program sampai atribut "executable" diberikan. Memberikan akses eksekusi ke semua user memastikan bahwa service account atau user lain yang menjalankan proses backup tidak akan terhalang oleh kendala Permission Denied.