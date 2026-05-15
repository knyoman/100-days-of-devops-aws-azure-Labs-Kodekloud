# Day 20: Create IAM Role for EC2 with Policy Attachment

---

## Tahap 1 — Login ke AWS Console

| Field    | Value                  |
|----------|------------------------|
| Username | `kk_labs_user_630888`  |
| Password | `y^1@PL%mIn@I`         |
| Layanan  | Cari **IAM** di search bar |

---

## Tahap 2 — Buat IAM Role Baru

Panel kiri → **Roles** → klik **Create role**.

![images](/imgs_aws/day20.png)
---

## Tahap 3 — Pilih Trusted Entity

| Field               | Value       |
|---------------------|-------------|
| Trusted entity type | AWS service |
| Service or use case | EC2         |

Klik **Next**.
![images](/imgs_aws/day20_1.png)
---

## Tahap 4 — Attach Policy

Cari `iampolicy_siva` → centang policy tersebut → klik **Next**.

![images](/imgs_aws/day20_2.png)
---

## Tahap 5 — Name & Create

| Field     | Value          |
|-----------|----------------|
| Role name | `iamrole_siva` |

Tinjau kembali:
- Trusted entities: `ec2.amazonaws.com`
- Policies: `iampolicy_siva`

Klik **Create role**.

![images](/imgs_aws/day20_3.png)
---

## Tahap 6 — Verifikasi via CLI

```bash
aws iam list-attached-role-policies --role-name iamrole_siva \
  --query "AttachedPolicies[*].PolicyName" \
  --output text
```

![images](/imgs_aws/day20_4.png)
> ✅ Jika output menampilkan `iampolicy_siva`, konfigurasi berhasil.