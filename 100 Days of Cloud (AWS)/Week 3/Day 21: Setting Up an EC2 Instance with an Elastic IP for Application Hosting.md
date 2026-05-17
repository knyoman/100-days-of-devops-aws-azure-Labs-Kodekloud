# Day 21: Setting Up an EC2 Instance with an Elastic IP for Application Hosting


---

## Tahap 1: Login ke AWS Console

| Field    | Value                  |
|----------|------------------------|
| Username | `kk_labs_user_844285`  |
| Password | `1m7zKdStQTIX`         |
| Region   | `us-east-1` (N. Virginia) |

---

## Tahap 2: Buat EC2 Instance

EC2 → **Instances** → **Launch instances**.

| Field       | Value                              |
|-------------|------------------------------------|
| Name        | `nautilus-ec2`                     |
| AMI         | Ubuntu (versi default LTS)         |
| Instance type | `t2.micro`                       |
| Key pair    | Proceed without a key pair         |

Klik **Launch instance** → tunggu notifikasi sukses.

![images](/imgs_aws/day21.png)
---

## Tahap 3: Buat Elastic IP

Panel kiri → **Network & Security** → **Elastic IPs** → **Allocate Elastic IP address**.

Biarkan pengaturan default → scroll ke bagian **Tags** → **Add new tag**:

| Key    | Value          |
|--------|----------------|
| `Name` | `nautilus-eip` |

Klik **Allocate**.

![images](/imgs_aws/day21_1.png)
---

## Tahap 4: Kaitkan Elastic IP ke Instance

Centang `nautilus-eip` → **Actions** → **Associate Elastic IP address**.

| Field         | Value          |
|---------------|----------------|
| Resource type | Instance       |
| Instance      | `nautilus-ec2` |

Klik **Associate**.

![images](/imgs_aws/day21_2.png)
---

## Tahap 5: Verifikasi

**Instances** → klik `nautilus-ec2` → tab **Details**.

Pastikan nilai **Public IPv4 address** dan **Elastic IP addresses** menampilkan alamat IP yang sama.

![images](/imgs_aws/day21_3.png)
> ✅ Elastic IP berhasil dikaitkan ke instance.