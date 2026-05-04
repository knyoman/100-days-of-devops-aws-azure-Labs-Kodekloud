# Day 10: Attach Elastic IP to EC2 Instance

Dokumentasi ini menjelaskan langkah-langkah mengaitkan Elastic IP ke instance EC2 di AWS melalui console.

---

## 🎯 Objective

Attach Elastic IP `nautilus-ec2-eip` ke instance EC2 `nautilus-ec2` agar IP publik tetap statis.

---

## Step 1: Login ke AWS Management Console

Akses AWS Console menggunakan kredensial berikut:

- **Username:** `kk_labs_user_826667`
- **Password:** `N^uM@D%z89a2`
- **Region:** Pastikan di pojok kanan atas adalah `us-east-1 (N. Virginia)`.

---

## Step 2: Navigasi ke Layanan Elastic IP

Ketik `EC2` di kolom pencarian dan pilih EC2.

Di panel navigasi kiri, di bawah **Network & Security**, klik **Elastic IPs**.

![images](/imgs_aws/day10.png)

---

## Step 3: Mengaitkan Elastic IP ke Instance

Cari dan centang Elastic IP bernama `nautilus-ec2-eip`.

Klik menu **Actions** > **Associate Elastic IP address**.

Pada halaman konfigurasi:

- **Resource type:** Pilih **Instance**.
- **Instance:** Pilih `nautilus-ec2`.
- **Private IP address:** Pilih IP privat dari instance tersebut.

Klik **Associate**.

![images](/imgs_aws/day10_1.png)

---

## Step 4: Verifikasi

![images](/imgs_aws/day10_2.png)