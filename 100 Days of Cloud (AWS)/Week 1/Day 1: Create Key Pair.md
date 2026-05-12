# Day 1: Create Key Pair
Dokumentasi ini menjelaskan langkah-langkah membuat **Key Pair di AWS EC2** sebagai bagian dari lab KodeKloud. Key Pair digunakan untuk autentikasi aman (SSH) ke instance EC2.

---

## 🎯 Objective

Membuat Key Pair dengan spesifikasi:
- **Name:** `xfusion-kp`
- **Type:** RSA
- **Format:** `.pem`
- **Region:** us-east-1

---

## Step 1 — Ambil Kredensial AWS

```bash
showcreds
```
### untuk mendapatkan detail login AWS

![images](/imgs_aws/Day1.png)

---

## Step 2 — Pembuatan Key Pair (Melalui GUI/Web Console)

![images](/imgs_aws/Day1(1).png)

### Login ke AWS Console --> Masuk ke Layanan EC2 --> Create Key Pair

![images](/imgs_aws/Day1(2).png)

---

## Step 3 — Tahap Finalisasi & Verifikasi

```bash
aws ec2 describe-key-pairs --key-names xfusion-kp
```

![images](/imgs_aws/Day1(3).png)