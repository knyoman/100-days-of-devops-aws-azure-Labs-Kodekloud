# Day 17: Create IAM Group

---

## Tahap 1 Login ke AWS Console

| Field    | Value                  |
|----------|------------------------|
| Username | `kk_labs_user_947162`  |
| Password | `GntpTucj7Ouu`         |
| Layanan  | Cari **IAM** di search bar |

---

## Tahap 2 Navigasi ke User Groups

Panel kiri → **User groups** → klik **Create group**.

![images](/imgs_aws/day17.png)

---

## Tahap 3 Konfigurasi Group

| Field            | Value             |
|------------------|-------------------|
| User group name  | `iamgroup_kirsty` |
| Add users        | Lewati            |
| Attach policies  | Lewati            |

![images](/imgs_aws/day17_1.png)

---

## Tahap 4 Simpan & Verifikasi

Klik **Create group** → pastikan `iamgroup_kirsty` muncul di daftar **User groups**.

![images](/imgs_aws/day17_2.png)

> ✅ Group berhasil dibuat.

---

## Tahap 5 — Cek Daftar Group *(Opsional)*
 
Verifikasi via CLI, pastikan `iamgroup_kirsty` terdaftar.
 
```bash
aws iam list-groups --query "Groups[*].GroupName" --output table
```

![images](/imgs_aws/day17_3.png)
 
---
 
## Tahap 6 — Cek Detail Group *(Opsional)*
 
Lihat detail lengkap group seperti ID dan tanggal pembuatan.
 
```bash
aws iam get-group --group-name iamgroup_kirsty
```

![images](/imgs_aws/day17_4.png)