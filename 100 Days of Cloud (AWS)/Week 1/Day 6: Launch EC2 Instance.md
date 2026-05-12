# Day 6: Launch EC2 Instance

Dokumentasi ini menjelaskan langkah-langkah meluncurkan EC2 Instance di AWS sebagai bagian dari infrastruktur cloud.

---

## 🎯 Objective

Meluncurkan EC2 Instance dengan spesifikasi:
- **Instance Name:** `datacenter-ec2`
- **AMI:** `Amazon Linux 2023` atau `Amazon Linux 2`
- **Instance Type:** `t2.micro`
- **Key Pair:** `datacenter-kp` (RSA, .pem format)
- **Security Group:** `default`
- **Region:** `us-east-1 (N. Virginia)`

---

## Step 1: Login ke AWS Console

Login menggunakan kredensial yang diberikan.

- **Username:** `kk_labs_user_998111`
- **Password:** `MoGw@%Rs4^Z3`
- **Region:** Pastikan di kanan atas tertulis `us-east-1 (N. Virginia)`.

---

## Step 2: Navigasi EC2 dan Mulai Konfigurasi

Ketik `EC2` di kolom pencarian --> **Launch instance**.

![images](/imgs_aws/day6.png)

---

## Step 3: Konfigurasi Instance Details

**Name and Tags:**
- Name: `datacenter-ec2`

**Application and OS Images (AMI):**
- Pilih `Amazon Linux 2023 AMI` atau `Amazon Linux 2`.

![images](/imgs_aws/day6_1.png)

**Instance Type:**
- Pilih `t2.micro` (Free tier eligible).

![images](/imgs_aws/day6_2.png)

---

## Step 4: Konfigurasi Key Pair

Klik **Create new key pair**.

Isi detail:
- **Key pair name:** `datacenter-kp`
- **Key pair type:** `RSA`
- **Private key file format:** `.pem`

Klik **Create key pair** (file akan terunduh).

![images](/imgs_aws/day6_3.png)

---

## Step 5: Konfigurasi Network Settings

Pada bagian **Firewall (security groups)**, pilih **Select existing security group** --> Pilih **default** 

![images](/imgs_aws/day6_4.png)

---

## Step 6: Eksekusi Peluncuran

Cek **Summary** --> Klik tombol orange **Launch instance**.

![images](/imgs_aws/day6_5.png)

---

## Step 7: Verifikasi Akhir

Klik **View all instances**.

![images](/imgs_aws/day6_6.png)