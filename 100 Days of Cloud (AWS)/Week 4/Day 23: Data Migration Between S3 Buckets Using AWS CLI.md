# Day 23: Data Migration Between S3 Buckets Using AWS CLI

> Panduan lengkap memigrasikan data antar S3 bucket menggunakan AWS CLI — mulai dari pembuatan bucket, sinkronisasi data, hingga verifikasi keamanan.

---

## Langkah 1 — Verifikasi AWS CLI & Konfigurasi

```bash
aws --version                   # Cek versi AWS CLI
aws sts get-caller-identity     # Cek identitas yang sedang digunakan
aws configure get region        # Cek region default
```
![images](/imgs_aws/day23.png)
---

## Langkah 2 — Buat S3 Bucket Baru (Private)

```bash
# Buat bucket di region us-east-1
aws s3api create-bucket \
    --bucket xfusion-sync-25388 \
    --region us-east-1

# Blokir semua public access
aws s3api put-public-access-block \
    --bucket xfusion-sync-25388 \
    --public-access-block-configuration \
    "BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=true,RestrictPublicBuckets=true"

# Verifikasi bucket berhasil dibuat
aws s3api head-bucket --bucket xfusion-sync-25388 && echo "Bucket berhasil dibuat"
```
![images](/imgs_aws/day23_1.png)
> **Catatan:** Region `us-east-1` tidak memerlukan `--create-bucket-configuration`. Region lain wajib menyertakan parameter tersebut.

---

## Langkah 3 — Inspeksi Bucket Sumber

```bash
# Tampilkan semua objek beserta ukurannya
aws s3 ls s3://xfusion-s3-3435 --recursive --human-readable --summarize

# Hitung total objek (simpan angka ini untuk verifikasi nanti)
aws s3 ls s3://xfusion-s3-3435 --recursive | wc -l
```

![images](/imgs_aws/day23_2.png)
---

## Langkah 4 — Migrasi Data (Sync)

```bash
aws s3 sync s3://xfusion-s3-3435 s3://xfusion-sync-25388 \
    --region us-east-1 \
    --no-progress

echo "Sinkronisasi selesai"
```

![images](/imgs_aws/day23_3.png)
> **Mengapa `s3 sync`?** Lebih andal dari `cp` — hanya menyalin file yang belum ada atau berbeda di tujuan, sehingga aman dijalankan ulang jika terjadi gangguan.

---

## Langkah 5 — Verifikasi Konsistensi Data

### Bandingkan jumlah objek

```bash
SOURCE_COUNT=$(aws s3 ls s3://xfusion-s3-3435 --recursive | wc -l)
echo "Jumlah objek di bucket sumber : $SOURCE_COUNT"

DEST_COUNT=$(aws s3 ls s3://xfusion-sync-25388 --recursive | wc -l)
echo "Jumlah objek di bucket tujuan : $DEST_COUNT"

if [ "$SOURCE_COUNT" -eq "$DEST_COUNT" ]; then
    echo "VERIFIKASI BERHASIL: Jumlah objek sama ($SOURCE_COUNT objek)"
else
    echo "VERIFIKASI GAGAL: Sumber=$SOURCE_COUNT, Tujuan=$DEST_COUNT"
fi
```

![images](/imgs_aws/day23_4.png)

### Bandingkan ukuran total

```bash
echo "=== Ringkasan Bucket Sumber ==="
aws s3 ls s3://xfusion-s3-3435 --recursive --human-readable --summarize | tail -2

echo "=== Ringkasan Bucket Tujuan ==="
aws s3 ls s3://xfusion-sync-25388 --recursive --human-readable --summarize | tail -2
```
---

## Langkah 6 — Verifikasi Keamanan Bucket

```bash
# Pastikan konfigurasi public access tetap terblokir
aws s3api get-public-access-block --bucket xfusion-sync-25388

# Cek ACL bucket (tidak boleh ada public policy)
aws s3api get-bucket-acl --bucket xfusion-sync-25388
```

![images](/imgs_aws/day23_5.png)

---
| Perintah | Fungsi |
|---|---|
| `s3api create-bucket` | Buat bucket baru |
| `s3api put-public-access-block` | Konfigurasi blokir akses publik |
| `s3api head-bucket` | Verifikasi keberadaan bucket |
| `s3 ls --recursive --summarize` | Tampilkan daftar & ringkasan objek |
| `s3 sync` | Sinkronisasi data antar bucket |
| `s3api get-public-access-block` | Cek konfigurasi keamanan bucket |

---

> 💡 **Tips:** Selalu verifikasi jumlah **dan** ukuran objek — jumlah sama belum tentu ukuran sama jika ada file yang korup atau terpotong saat transfer.