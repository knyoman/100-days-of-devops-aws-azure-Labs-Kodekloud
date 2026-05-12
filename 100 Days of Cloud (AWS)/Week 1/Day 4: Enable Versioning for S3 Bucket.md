# Day 4: Enable Versioning for S3 Bucket

Dokumentasi ini menjelaskan langkah-langkah mengaktifkan versioning pada S3 Bucket di AWS sebagai bagian dari pengelolaan data yang aman.

---

## 🎯 Objective

Mengaktifkan versioning pada bucket S3 dengan spesifikasi:
- **Bucket Name:** `nautilus-s3-4048`
- **Region:** `us-east-1`

---

## Step 1 — Persiapan & Login

Login ke AWS Console menggunakan kredensial yang diberikan.

- **Username:** `kk_labs_user_848525`
- **Password:** `CVUfSvbYPHN6`
- **Region:** Pastikan di pojok kanan atas adalah `N. Virginia (us-east-1)`.

---

## Step 2 — Navigasi ke Layanan S3

Ketik `S3` di bilah pencarian layanan di bagian atas dan pilih **S3**.

Kamu akan melihat daftar bucket yang ada di akun tersebut.

![images](/imgs_aws/day4.png)

---

## Step 3 — Mengaktifkan Versioning pada Bucket

Cari dan klik pada nama bucket: `nautilus-s3-4048`.

Setelah masuk ke dalam detail bucket, klik pada tab **Properties**.

Pada bagian **Bucket Versioning**, klik tombol **Edit**.

![images](/imgs_aws/day4_1.png)

Ubah status dari **Suspended/Disabled** menjadi **Activate**.

Klik tombol **Save changes** di bagian bawah.

![images](/imgs_aws/day4_2.png)
---

## Step 4 — Verifikasi Akhir

Setelah menyimpan, pastikan status di tab **Properties** sekarang menunjukkan **Bucket Versioning: Enabled**.

![images](/imgs_aws/day4_2.png)