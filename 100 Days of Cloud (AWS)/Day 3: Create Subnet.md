# Day 3: Create Subnet

Dokumentasi ini menjelaskan langkah-langkah membuat **Subnet** di AWS sebagai bagian dari jaringan virtual untuk mengisolasi resource.

---

## 🎯 Objective

Membuat Subnet dengan spesifikasi:
- **Name:** `nautilus-subnet`
- **VPC:** Default VPC
- **Availability Zone:** `us-east-1a`
- **IPv4 CIDR block:** `172.31.96.0/24`
- **Region:** `us-east-1`

---

## Step 1 — Persiapan & Login

Login ke AWS Console menggunakan kredensial yang diberikan.

- **Username:** `kk_labs_user_264980`
- **Password:** `898b^1lwDRT8`
- **Region:** Pastikan di pojok kanan atas adalah `N. Virginia (us-east-1)`.

---

## Step 2 — Navigasi ke Layanan VPC

Ketik `VPC` di bilah pencarian layanan di bagian atas dan pilih **VPC**.

Pada panel navigasi di sisi kiri, klik menu **Subnets**.

![images](/imgs_aws/day3.png)

---

## Step 3 — Membuat Subnet Baru

Klik tombol **Create subnet** di pojok kanan atas.

Isi detail berikut:
- **VPC ID:** Pilih VPC yang sudah ada (biasanya `Default VPC`).
- **Subnet name:** `nautilus-subnet`
- **Availability Zone:** `us-east-1a`
- **IPv4 CIDR block:** `172.31.96.0/24`

Tips: Jika CIDR block bentrok, periksa subnet yang sudah ada untuk menemukan rentang yang belum terpakai.

![images](/imgs_aws/day3_1.png)

---

## Step 4 — Simpan & Selesaikan

Gulir ke bawah dan klik tombol **Create subnet**.

Tunggu notifikasi sukses muncul.

![images](/imgs_aws/day3_2.png)

---

## Step 5 — Verifikasi Subnet via CLI

```bash
aws ec2 describe-subnets --filters Name=tag:Name,Values=nautilus-subnet
```

![images](/imgs_aws/day3_3.png)

---

## Step 6 — Validasi Detail Subnet

```bash
aws ec2 describe-subnets --subnet-ids <SUBNET-ID> \
--query "Subnets[*].{Name:Tags[?Key=='Name'].Value|[0], CIDR:CidrBlock, AZ:AvailabilityZone}"
```

![images](/imgs_aws/day3_4.png)
