# Day 13: Create AMI (Amazon Machine Image) from EC2 Instance

## 1️⃣ Login ke AWS Management Console

- Akses AWS Console dan login
- Username: `kk_labs_user_599963`
- Password: `5@F8p^b7e!M!`
- Pastikan region: **us-east-1 (N. Virginia)**

---

## 2️⃣ Navigasi ke Instance EC2

- Cari layanan **EC2** melalui search bar
- Klik **Instances** di panel kiri
- Cari dan centang instance **nautilus-ec2**

![images](/imgs_aws/day13.png)

---

## 3️⃣ Membuat Image (AMI)

- Klik tombol **Actions** di bagian atas
- Pilih **Image and templates** → **Create image**
- **Image name**: `nautilus-ec2-ami`
- **No reboot**: Biarkan tidak tercentang (default)
- Klik tombol **Create image** (orange)

![images](/imgs_aws/day13_1.png)

---

## 4️⃣ Verifikasi Status AMI

- Di panel kiri, klik **Images** → **AMIs**
- Cari AMI dengan nama **nautilus-ec2-ami**
- Tunggu status berubah dari **Pending** → **Available** (beberapa menit)

![images](/imgs_aws/day13_2.png)

- Cek Melalui CLI

```bash
aws ec2 describe-images --filters "Name=name,Values=nautilus-ec2-ami" --query "Images[*].State" --output text
```

![images](/imgs_aws/day13_3.png)

---