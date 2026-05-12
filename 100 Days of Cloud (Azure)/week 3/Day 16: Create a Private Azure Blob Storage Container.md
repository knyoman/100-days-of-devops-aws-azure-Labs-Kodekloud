# 🗄️ Azure Blob Storage — Setup

---

## Tahap 1 — Buat Storage Account

Cari **"Storage accounts"** di search bar → klik **+ Create**.

| Field                | Value                      |
|----------------------|----------------------------|
| Resource Group       | Pilih yang ada             |
| Storage account name | `xfusionst19930`           |
| Region               | Sesuaikan dengan resource lab |
| Performance          | Standard                   |
| Redundancy           | Locally-redundant storage (LRS) |

![images](/imgs_azure/day16.png)

---

## Tahap 2 — Navigasi ke Blob Container

Setelah deployment selesai → klik **Go to resource** → di panel kiri pilih **Data storage** → klik **Containers**.

![images](/imgs_azure/day16_1.png)

---

## Tahap 3 — Buat Container

Klik **+ Container** → isi detail berikut.

| Field               | Value                        |
|---------------------|------------------------------|
| Name                | `xfusion-blob-19599`         |
| Public access level | Private (no anonymous access) |

Klik **Create**.

![images](/imgs_azure/day16_2.png)

> ✅ Container berhasil dibuat dan siap digunakan.