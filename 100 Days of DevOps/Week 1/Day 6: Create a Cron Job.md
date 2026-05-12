# Day 6: Create a Cron Job

Dokumentasi ini menjelaskan langkah-langkah instalasi dan konfigurasi cron job pada server Linux sebagai bagian dari automasi tugas rutin.

---

## 🎯 Objective

Menginstal service cron dan membuat cron job untuk user `root` yang menulis pesan ke `/tmp/cron_text` setiap 5 menit.

---

## Step 1: Masuk ke App Server


```bash
ssh tony@stapp01
```
![images](/imgs_DevOps/day6.png)

---
## Step 2: Install & Aktifkan Cron

Lakukan langkah ini di setiap server target.

```bash
# Install paket cron
sudo yum install cronie -y
```
![images](/imgs_DevOps/day6_1.png)

```bash
# Aktifkan dan jalankan service crond
sudo systemctl enable crond
sudo systemctl start crond
```
![images](/imgs_DevOps/day6_2.png)

---

## Step 3: Tambahkan Cron Job untuk User Root

Untuk menambahkan cron job bagi user `root`, gunakan perintah:

```bash
sudo crontab -e
```

![images](/imgs_DevOps/day6_3.png)

Di dalam editor yang terbuka (biasanya `vi`), tambahkan baris ini di bagian paling bawah:

```
*/5 * * * * echo hello > /tmp/cron_text
```
Simpan dan keluar dengan menekan `Esc`, lalu ketik `:wq` dan tekan `Enter`.

---

## Step 4: Verifikasi

Setelah disimpan, pastikan cron job telah terdaftar dengan menjalankan:

```bash
sudo crontab -l
```
![images](/imgs_DevOps/day6_4.png)

Dan periksa bahwa file `/tmp/cron_text` akan diupdate setiap 5 menit sesuai jadwal.
