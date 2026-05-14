# Day 19: Attach IAM Policy to IAM User

---

## Tahap 1 Login ke AWS Console

| Field    | Value                  |
|----------|------------------------|
| Username | `kk_labs_user_311229`  |
| Password | `2%ANVKiCDmA0`         |
| Layanan  | Cari **IAM** di search bar |

---

## Tahap 2 Temukan IAM User

Panel kiri → **Users** → klik **`iamuser_john`**.

![images](/imgs_aws/day19.png)
---

## Tahap 3 Attach Policy

1. Tab **Permissions** → **Add permissions** → **Add permissions**.
2. Pilih **Attach policies directly**.
3. Cari `iampolicy_john` → centang policy tersebut.
4. Klik **Next**.

![images](/imgs_aws/day19_1.png)
---

## Tahap 4 Review & Selesaikan

Pastikan policy sudah benar → klik **Add permissions**.

![images](/imgs_aws/day19_2.png)
> Verifikasi `iampolicy_john` muncul di tabel **Permissions policies** milik John.
---

## Tahap 5 Verifikasi 

![images](/imgs_aws/day19_3.png)

```bash
aws iam list-attached-user-policies --user-name iamuser_john \
  --query "AttachedPolicies[?PolicyName=='iampolicy_john'].PolicyName" \
  --output text
```
![images](/imgs_aws/day19_4.png)
> ✅ Jika output menampilkan `iampolicy_john`, konfigurasi berhasil.