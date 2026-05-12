# Day 9: MariaDB Troubleshooting

Dokumentasi ini menjelaskan langkah-langkah troubleshooting dan perbaikan layanan MariaDB pada server database.

---

## 🎯 Objective

Memperbaiki layanan MariaDB yang tidak berjalan dengan menganalisis log error dan memperbaiki permission folder data.

---

## Step 1: Login ke Database Server

Login ke server database menggunakan SSH:

```bash
ssh peter@stdb01
```
![images](/imgs_DevOps/day9.png)

Masukkan password user `peter` ketika diminta.

---

## Step 2: Cek Status Layanan MariaDB

Periksa status layanan MariaDB:

```bash
sudo systemctl status mariadb
```
![images](/imgs_DevOps/day9_1.png)

Status biasanya menunjukkan `failed` atau `inactive`.

---

## Step 3: Analisis Log Error

Periksa log sistem untuk penyebab spesifik:

```bash
sudo journalctl -u mariadb --no-pager
```
Atau cek file log MariaDB langsung:

```bash
sudo tail -n 50 /var/log/mariadb/mariadb.log
```
![images](/imgs_DevOps/day9_3.png)

Masalah umum: permission folder data salah, konfigurasi `/etc/my.cnf` bermasalah, atau kepemilikan folder/log bukan user `mysql`.

---

## Step 4: Perbaikan Umum

Jika masalah permission, perbaiki kepemilikan folder:

```bash
sudo chown -R mysql:mysql /var/lib/mysql
```

Kemudian, coba jalankan layanan kembali:

```bash
sudo systemctl start mariadb
```
![images](/imgs_DevOps/day9_4.png)

---

## Step 5: Verifikasi Hasilnya

Pastikan layanan MariaDB sudah berjalan normal:

```bash
sudo systemctl status mariadb
```
![images](/imgs_DevOps/day9_5.png)

Status harus berubah menjadi `active (running)` berwarna hijau.

---
### Step Opsional ⬇️
---

## Step 6: Mengatur layanan MariaDB otomatis menyala saat server booting

```bash
sudo systemctl enable mariadb
```
![images](/imgs_DevOps/day9_6.png)

---
## Step 7: Verifikasi Akhir

```bash
sudo systemctl status mariadb
```
![images](/imgs_DevOps/day9_7.png)

Pastikan teksnya berubah menjadi enabled seperti ini:
Loaded: loaded (...; enabled; preset: disabled)

---