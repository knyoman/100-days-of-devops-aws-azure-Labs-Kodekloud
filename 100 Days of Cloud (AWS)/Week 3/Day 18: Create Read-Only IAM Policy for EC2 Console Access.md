# Day 18: Create Read-Only IAM Policy for EC2 Console Access

---

## Tahap 1 — Login ke AWS Console

| Field    | Value                  |
|----------|------------------------|
| Username | `kk_labs_user_166333`  |
| Password | `8Wv^z74So^sB`         |
| Layanan  | Cari **IAM** di search bar |

---

## Tahap 2 — Navigasi ke Policies

Panel kiri → **Policies** → klik **Create policy** → pilih tab **JSON**.

---

## Tahap 3 — Masukkan JSON Policy

Hapus kode default, tempel JSON berikut:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ec2:Describe*",
                "ec2:Get*"
            ],
            "Resource": "*"
        }
    ]
}
```

![images](/imgs_aws/day18.png)

> `Describe*` dan `Get*` memberi akses **read-only** ke EC2 (tanpa izin Create/Terminate).

---

## Tahap 4 — Beri Nama & Simpan

Klik **Next** → isi detail berikut → klik **Create policy**.

| Field       | Value               |
|-------------|---------------------|
| Policy name | `iampolicy_kirsty`  |
| Description | *(Opsional)* Read-only access to EC2 console |

![images](/imgs_aws/day18_1.png)

---

## Tahap 5 — Verifikasi via CLI

```bash
aws iam list-policies --scope Local \
  --query "Policies[?PolicyName=='iampolicy_kirsty'].[PolicyName, Arn]" \
  --output table
```

![images](/imgs_aws/day18_2.png)

> ✅ Policy muncul di tabel → berhasil dibuat.