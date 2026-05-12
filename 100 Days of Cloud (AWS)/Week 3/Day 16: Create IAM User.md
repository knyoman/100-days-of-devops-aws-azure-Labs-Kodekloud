# Day 16: Create IAM User

---

## Tahap 1 Login ke AWS Console

Akses URL login lalu masuk dengan kredensial berikut.

| Field    | Value                          |
|----------|--------------------------------|
| URL      | `429163309141.signin.aws.amazon.com/console` |
| Username | `kk_labs_user_210069`          |
| Password | `2p%h8Kr%wJw@`                 |
| Region   | Global (IAM tidak region-spesifik) |

---

## Tahap 2 Navigasi ke IAM

Ketik **IAM** di search bar → pilih **IAM** → klik **Users** di panel kiri.

![images](/imgs_aws/day16.png)

---

## Tahap 3 Buat User Baru

Klik **Create user** → isi detail berikut.

| Field     | Value             |
|-----------|-------------------|
| User name | `iamuser_mariyam` |
| Console access | Lewati (tidak perlu dicentang) |

Klik **Next**.

---

## Tahap 4 Set Permissions

Tidak ada instruksi izin khusus → langsung klik **Next**.

---

## Tahap 5 Review & Create

Pastikan nama user sudah benar → klik **Create user**.

![images](/imgs_aws/day16_1.png)

---

## Tahap 6 Verifikasi

Pastikan `iamuser_mariyam` muncul dalam daftar **Users** IAM.

![images](/imgs_aws/day16_2.png)

> ✅ User berhasil dibuat.