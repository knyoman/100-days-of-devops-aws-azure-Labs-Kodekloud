# Day 15: Create and Configure Network Security Group (NSG) in Azure

---

## Tahap 1  Buat Resource NSG

Cari **"Network security groups"** di search bar → klik **+ Create**.

| Field          | Value            |
|----------------|------------------|
| Resource Group | Pilih yang ada   |
| Name           | `devops-nsg`     |
| Region         | Sesuaikan dengan resource lab |

![images](/imgs_azure/day15.png)

---

## Tahap 2 Aturan Inbound: HTTP

Masuk ke NSG → **Inbound security rules** → **+ Add**.

| Field              | Value       |
|--------------------|-------------|
| Source             | Any         |
| Source port ranges | `*`         |
| Destination        | Any         |
| Service            | HTTP (80)   |
| Name               | `Allow-HTTP` |

![images](/imgs_azure/day15_1.png)

---

## Tahap 3 Aturan Inbound: SSH

Di halaman yang sama → **+ Add**.

| Field              | Value       |
|--------------------|-------------|
| Source             | Any         |
| Source port ranges | `*`         |
| Destination        | Any         |
| Service            | SSH (22)    |
| Name               | `Allow-SSH`  |

![images](/imgs_azure/day15_2.png)

---

## Tahap 4 Verifikasi

Pastikan kedua aturan muncul di tabel dengan status **Allow**.

![images](/imgs_azure/day15_3.png)

> ✅ NSG siap dikaitkan ke VM atau Subnet.