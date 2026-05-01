# Day 7: Change EC2 Instance Type

Dokumentasi ini menjelaskan langkah-langkah mengubah tipe instance EC2 di AWS dari t2.micro ke t2.nano.

---

## 🎯 Objective

Mengubah tipe instance EC2 bernama `xfusion-ec2` dari `t2.micro` menjadi `t2.nano` dengan menghentikan instance terlebih dahulu.

---

## Step 1: Login ke AWS Management Console

Akses AWS Console menggunakan kredensial yang diberikan.

- **Username:** `kk_labs_user_760206`
- **Password:** `6IPMQPLuBBSG`
- **Region:** Pastikan di pojok kanan atas adalah `us-east-1 (N. Virginia)`.

---

## Step 2: Hentikan Instance EC2 (xfusion-ec2)

Buka layanan EC2 melalui kolom pencarian.

Klik **Instances (running)** untuk melihat daftar instance.

Pilih instance bernama `xfusion-ec2`.

Pastikan **Status check** menunjukkan `2/2 checks passed`.

Klik menu **Instance state** > **Stop instance**.

Tunggu hingga status berubah menjadi **Stopped**.

![images](/imgs_aws/day7.png)
![images](/imgs_aws/day7_1.png)

---

## Step 3: Mengubah Tipe Instance

Dengan instance `xfusion-ec2` masih terpilih.

Klik menu **Actions** > **Instance settings** > **Change instance type**.

Ubah **Instance type** dari `t2.micro` menjadi `t2.nano`.

Klik **Apply** untuk menyimpan perubahan.

![images](/imgs_aws/day7_2.png)

---

## Step 4: Menjalankan Kembali Instance

Klik menu **Instance state** > **Start instance**.

Tunggu hingga status berubah kembali menjadi **Running**.

![images](/imgs_aws/day7_3.png)

---

## Step 5: Verifikasi

![images](/imgs_aws/day7_4.png)
