# Day 17: Create a Public Azure Blob Storage Container

---

## Tahap 1 — Buat Storage Account

Cari **"Storage accounts"** di search bar → klik **+ Create**.

| Field                | Value                    |
|----------------------|--------------------------|
| Resource Group       | Pilih yang tersedia      |
| Storage account name | `nautilusst20152`        |
| Region               | Sesuaikan dengan lab     |
| Performance          | Standard                 |
| Redundancy           | Locally-redundant (LRS)  |

Klik **Review + create** → **Create** → **Go to resource**.

![images](/imgs_azure/day17.png)

---

## Tahap 2 — Aktifkan Akses Publik

> ⚠️ Wajib dilakukan sebelum membuat container.

Panel kiri → **Settings** → **Configuration**.

Cari opsi **"Allow Blob anonymous access"** → ubah ke **Enabled**.

Klik **Save**.

![images](/imgs_azure/day17_1.png)

---

## Tahap 3 — Buat Container

Panel kiri → **Data storage** → **Containers** → klik **+ Container**.

| Field               | Value                                                    |
|---------------------|----------------------------------------------------------|
| Name                | `nautilus-blob-3033`                                     |
| Public access level | Container *(anonymous read access for containers and blobs)* |

Klik **Create**.

![images](/imgs_azure/day17_2.png)

> ✅ Container publik berhasil dibuat dan siap digunakan.