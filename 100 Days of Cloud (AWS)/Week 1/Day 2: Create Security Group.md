# Day 2: Create Security Group

Dokumentasi ini menjelaskan langkah-langkah membuat **Security Group (SG)** di AWS sebagai firewall virtual untuk mengontrol traffic masuk ke server.

---

## 🎯 Objective

Membuat Security Group dengan spesifikasi:
- **Name:** `nautilus-sg`
- **Description:** Security group for Nautilus App Servers
- **Inbound Rules:**
  - HTTP (80) → 0.0.0.0/0
  - SSH (22) → 0.0.0.0/0
- **Region:** us-east-1

---

## Step 1 — Masuk ke Menu Security Groups

Login ke AWS Console --> Pilih **Network & Security** --> Klik **Security Groups**

![images](/imgs_aws/Day2(1).png)

---
## Step 2 — Membuat Security Group Baru

Klik tombol **Create security group**, lalu isi:

- **Security group name:** `nautilus-sg`
- **Description:** `Security group for Nautilus App Servers`
- **VPC:** Default VPC
- **Konfigurasi Inbound Rules:**

| Type | Port | Source | CIDR |
|------|------|--------|------|
| HTTP | 80   | Anywhere | 0.0.0.0/0 |
| SSH  | 22   | Anywhere | 0.0.0.0/0 |

![images](/imgs_aws/Day2(2).png)

---

## Step 5 — Simpan Security Group

- Scroll ke bawah
- Klik **Create security group**
![images](/imgs_aws/Day2(3).png)

---
## Step 6 — Verifikasi SG

```bash
aws ec2 describe-security-groups --filters Name=group-name,Values=nautilus-sg
```
![images](/imgs_aws/Day2(4).png)

---
## Step 7 — Validasi Rules Secara Spesifik

```bash
aws ec2 describe-security-groups --group-names nautilus-sg \
--query "SecurityGroups[*].IpPermissions"
```
![images](/imgs_aws/Day2(5).png)

---

