# Day 15: Create Volume Snapshot

## 1. Login ke AWS Console
- Buka AWS Management Console.
- Username: `kk_labs_user_788151`
- Password: `jval1q@6WolW`
- Pastikan region: `us-east-1 (N. Virginia)`

---

## 2. Cari Volume
- Buka layanan **EC2**.
- Pilih menu **Volumes** pada bagian **Elastic Block Store**.
- Cari volume dengan nama `nautilus-vol`.
- Catat **Volume ID**.

![images](/imgs_aws/day15.png)

---

## 3. Buat Snapshot
- Pilih volume `nautilus-vol`.
- Klik **Actions** → **Create snapshot**.
- Isi **Description**:
- Klik **Add tag** dan isi:
- Key: `Name`
- Value: `nautilus-vol-ss`
- Klik **Create snapshot**.

![images](/imgs_aws/day15_1.png)

---

## 4. Verifikasi Snapshot
- Buka menu **Snapshots**.
- Cari snapshot dengan nama `nautilus-vol-ss`.
- Tunggu hingga status berubah menjadi:

![images](/imgs_aws/day15_2.png)

