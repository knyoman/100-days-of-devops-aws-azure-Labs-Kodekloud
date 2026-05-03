# Day 9: Enable Termination Protection for EC2 Instance

Dokumentasi ini menjelaskan langkah-langkah mengaktifkan termination protection pada instance EC2 di AWS untuk mencegah penghapusan tidak sengaja.

---

## 🎯 Objective

Mengaktifkan termination protection pada instance `devops-ec2` agar tidak dapat dihapus secara tidak sengaja.

---

## Step 1: Login ke AWS Management Console

Akses AWS Console menggunakan kredensial berikut:

- **Username:** `kk_labs_user_714408`
- **Password:** `9P3e!Pn5S9OT`
- **Region:** Pastikan di pojok kanan atas adalah `us-east-1 (N. Virginia)`.

---

## Step 2: Navigasi ke Instance EC2

Buka layanan EC2 melalui kolom pencarian.

Klik **Instances (running)** atau **Instances** di menu navigasi kiri.

Cari dan centang instance bernama `devops-ec2`.

![images](/imgs_aws/day9.png)

---

## Step 3: Mengaktifkan Termination Protection

Dengan instance `devops-ec2` terpilih:

- Klik **Actions**.
- Pilih **Instance settings**.
- Klik **Change termination protection**.
- Pilih atau centang **Enable**.
- Klik **Save**.

![images](/imgs_aws/day9_1.png)

---

## Step 4: Verifikasi

![images](/imgs_aws/day9_2.png)

---

### Menggunakan CLI ⬇️ (Opsional)

---

## 1. Cek Apakah CLI Sudah Terhubung

```bash
aws ec2 describe-instances --query "Reservations[*].Instances[*].[Tags[?Key=='Name'].Value|[0],InstanceId]" --output table
```
![images](/imgs_aws/day9_3.png)

---

## 2. Jalankan Perintah Termination Protection

```bash
aws ec2 modify-instance-attribute --instance-id i-xxxxxx --disable-api-termination
```
![images](/imgs_aws/day9_4.png) 

(Ganti i-xxxxxx dengan Instance ID)

---

## 3. Verifikasi Perubahan

```bash
aws ec2 describe-instance-attribute \
  --instance-id i-xxxxxx \
  --attribute disableApiTermination
```
![images](/imgs_aws/day9_5.png)

Jika output menampilkan "Value": true, artinya perlindungan sudah aktif.

---

