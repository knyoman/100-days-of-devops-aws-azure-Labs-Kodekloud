# Day 12: Attach Volume to EC2 Instance

## 1️⃣ Login ke AWS Management Console

- Akses AWS Console dan login
- Username: `kk_labs_user_588334`
- Password: `zc%eOc12ZJ@9`
- Pastikan region: **us-east-1 (N. Virginia)**

## 2️⃣ Navigasi ke Menu Volumes

- Cari layanan **EC2** melalui search bar
- Di panel kiri, pilih **Volumes** (di bawah Elastic Block Store)
- Cari volume **nautilus-volume** dengan status **Available**

![images](/imgs_aws/day12.png)

---

## 3️⃣ Proses Attach Volume

- Centang volume **nautilus-volume**
- Klik **Actions** → **Attach volume**
- **Instance**: Pilih **nautilus-ec2**
- **Device name**: `/dev/sdb`
- Klik **Attach volume**

![images](/imgs_aws/day12_1.png)

---

## 4️⃣ Verifikasi & Validasi

- Pastikan status volume berubah menjadi **In-use**
```bash
`aws ec2 describe-volumes --volume-ids <VOLUME_ID> --query "Volumes[*].Attachments[*].State" --output text`
```
![images](/imgs_aws/day13_2.png)

---