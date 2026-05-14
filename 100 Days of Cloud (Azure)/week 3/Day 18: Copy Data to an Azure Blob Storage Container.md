# Day 18: Copy Data to an Azure Blob Storage Container

---

## Tahap 1 Temukan Storage Account

Ketik **`nautilusst3144`** di search bar Azure Portal → pilih akun tersebut.

![images](/imgs_azure/day18.png)

---

## Tahap 2 Masuk ke Menu Containers

Panel kiri → kategori **Data storage** → klik **Containers**.

![images](/imgs_azure/day18_1.png)

---

## Tahap 3 Pilih Container Tujuan

Klik container **`nautilus-blob-15907`**.

---

## Tahap 4 Cek File di Server

Sebelum upload, kita buat file nautilus.txt dengan isi hasil dari output perintah berikut.

```bash
cat /tmp/nautilus.txt
```

![images](/imgs_azure/day18_2.png)

---

## Tahap 5 Unggah File

1. Klik tombol **Upload** di bagian atas.
2. Klik ikon folder → cari dan pilih file **`nautilus.txt`** dari direktori `/tmp/`.
3. Klik **Upload** di bagian bawah panel.

![images](/imgs_azure/day18_3.png)

> ✅ File berhasil diunggah ke container `nautilus-blob-15907`.


## Verifikasi via CLI

```bash
# Perintah untuk melihat daftar file (blob) di dalam container
az storage blob list \
  --account-name nautilusst3144 \
  --container-name nautilus-blob-15907 \
  --output table
```

![images](/imgs_azure/day18_4.png)
>Terminal akan menampilkan tabel yang berisi nama file nautilus.txt. Jika tabelnya kosong, berarti file belum terunggah dengan benar.