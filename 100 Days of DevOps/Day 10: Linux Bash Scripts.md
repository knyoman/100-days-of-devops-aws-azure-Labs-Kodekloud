# Day 10: Linux Bash Scripts

Dokumentasi ini menjelaskan langkah-langkah membuat dan menjalankan bash script untuk backup website di App Server 3.

---

## 🎯 Objective

Membuat script `news_backup.sh` yang mengkompresi folder `/var/www/html/news` dan mengirimkannya ke Nautilus Storage Server tanpa password.

---

## Step 1 — Persiapan Awal di App Server 3

Login ke App Server 3:

```bash
ssh banner@stapp03
```

Instal package zip:

```bash
sudo yum install zip -y
```

Buat direktori dan atur hak akses:

```bash
sudo mkdir -p /backup /scripts
sudo chown -R banner:banner /backup /scripts
```

---

## Step 2 — Konfigurasi SSH Tanpa Password

Generate SSH key:

```bash
ssh-keygen -t rsa -N "" -f ~/.ssh/id_rsa
```

Kirim public key ke Storage Server (gunakan IP dari Details, misal 172.16.238.15):

```bash
ssh-copy-id natasha@172.16.238.15
```

Tes koneksi:

```bash
ssh natasha@172.16.238.15 exit
```

---

## Step 3 — Pembuatan Bash Script news_backup.sh

Buat file script:

```bash
vi /scripts/news_backup.sh
```

Isi script (sesuaikan IP Storage Server):

```bash
#!/bin/bash

# Membuat zip archive dari folder news
zip -r /backup/xfusioncorp_news.zip /var/www/html/news

# Menyalin arsip ke Nautilus Storage Server
scp /backup/xfusioncorp_news.zip natasha@172.16.238.15:/backup/
```

Simpan dan keluar.

Berikan izin eksekusi:

```bash
chmod +x /scripts/news_backup.sh
```

---

## Step 4 — Uji Coba dan Verifikasi

Jalankan script:

```bash
/scripts/news_backup.sh
```

Pastikan kompresi dan pengiriman berhasil tanpa password.