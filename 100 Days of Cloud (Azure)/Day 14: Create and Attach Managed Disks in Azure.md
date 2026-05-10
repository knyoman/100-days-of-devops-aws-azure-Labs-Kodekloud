# Day 14: Create and Attach Managed Disks in Azure

## Tahap 1: Akses Menu Disks

- Ketik **Disks** di kolom pencarian atas Azure Portal
- Pilih layanan **Disks**
- Masuk ke dashboard manajemen disk

![images](/imgs_azure/day14.png)

---

## Tahap 2: Inisialisasi Pembuatan

- Klik tombol **+ Create** (+ Buat) di pojok kiri atas
- Buka wizard konfigurasi disk baru

## Tahap 3: Konfigurasi Spesifikasi

- **Resource Group**: Pilih yang sudah tersedia
- **Disk Name**: `devops-disk`
- **Region**: Pilih wilayah yang sama dengan Resource Group (biasanya East US)
- **Size (Ukuran)**: 
  - Klik **Change size**
  - Pilih **Standard HDD (LRS)**
  - Ketik **2 GiB** pada kotak ukuran

![images](/imgs_azure/day14_1.png)

---

## Tahap 4: Validasi dan Deployment

- Klik **Review + create**
- Klik **Create** untuk menyelesaikan pembuatan disk

![images](/imgs_azure/day14_2.png)

---