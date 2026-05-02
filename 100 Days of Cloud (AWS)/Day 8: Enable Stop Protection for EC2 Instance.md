# Day 8: Enable Stop Protection for EC2 Instance

Dokumentasi ini menjelaskan langkah-langkah mengaktifkan stop protection pada instance EC2 di AWS.

---

## 🎯 Objective

Mengaktifkan stop protection pada instance `xfusion-ec2` agar tidak dapat dihentikan secara tidak sengaja.

---

## Step 1: Login ke AWS Management Console

Akses AWS Console menggunakan kredensial berikut:

- **Username:** `kk_labs_user_610929`
- **Password:** `M3hjWf@U4JUM`
- **Region:** Pastikan di pojok kanan atas adalah `us-east-1 (N. Virginia)`.

---

## Step 2: Navigasi ke Instance EC2

Buka layanan EC2 melalui kolom pencarian.

Klik **Instances (running)** atau **Instances** di menu navigasi kiri.

Cari dan centang instance bernama `xfusion-ec2`.

![images](/imgs_aws/day8.png)

---

## Step 3: Mengaktifkan Stop Protection

Dengan instance `xfusion-ec2` terpilih:

- Klik **Actions**.
- Pilih **Instance settings**.
- Klik **Change stop protection**.
- Pilih atau centang **Enable**.
- Klik **Save**.

![images](/imgs_aws/day8_1.png)

---

## Step 4: Verifikasi

![images](/imgs_aws/day8_2.png)
