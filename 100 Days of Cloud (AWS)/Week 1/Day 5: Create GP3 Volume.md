# Day 5: Create GP3 Volume

Dokumentasi ini menjelaskan langkah-langkah membuat volume gp3 di AWS EC2 sebagai bagian dari pengelolaan storage untuk instance.

---

## 🎯 Objective

Membuat volume EBS dengan spesifikasi:
- **Volume type:** `General Purpose SSD (gp3)`
- **Size:** `2 GiB`
- **Availability Zone:** `us-east-1a`
- **Tag Name:** `xfusion-volume`
- **Region:** `us-east-1`

---

## Step 1 — Persiapan & Login

Login ke AWS Console menggunakan kredensial yang diberikan.

- **Username:** `kk_labs_user_990155`
- **Password:** `cQvtjGBwn8u8`
- **Region:** Pastikan di pojok kanan atas adalah `N. Virginia (us-east-1)`.

---

## Step 2 — Navigasi ke Menu Volumes

Ketik `EC2` di bilah pencarian layanan di bagian atas dan pilih **EC2** --> **Elastic Block Store**.

Klik pada menu **Volumes**.

![images](/imgs_aws/day5.png)

---

## Step 3 — Membuat Volume Baru

Klik tombol orange **Create volume** di pojok kanan atas.

Isi detail berikut:
- **Volume type:** Pilih **General Purpose SSD (gp3)**.
- **Size:** Ubah menjadi **2 GiB**.
- **Availability Zone:** Pilih salah satu, misalnya **us-east-1a**. Pastikan region tetap `us-east-1`.
- **IOPS & Throughput:** Biarkan pada nilai default (3000 IOPS dan 125 MiB/s).

Ringkasan Konfigurasi
 
```
Volume Type  : gp3 (General Purpose SSD)
Size         : 2 GiB
Availability Zone : us-east-1a
IOPS         : 3000 (default)
Throughput   : 125 MiB/s (default)
```

![images](/imgs_aws/day5_1.png)

---

## Step 4 — Menambahkan Nama Volume (Tag)

Gulir ke bawah ke bagian **Tags** --> Klik **Add tag**
```
Key     : Name
Value   : xfusion-volume
```
![images](/imgs_aws/day5_2.png)

---

## Step 5 — Simpan dan Verifikasi

Klik tombol **Create volume**.

![images](/imgs_aws/day5_3.png)

---

## Step 6 Validasi dan Cek Volume (Opsional)

```bash
aws ec2 describe-volumes \
  --filters "Name=tag:Name,Values=xfusion-volume" \
  --region us-east-1
```

![images](/imgs_aws/day5_4.png)