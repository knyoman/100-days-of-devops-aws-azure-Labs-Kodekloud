# Day 5: Create a Virtual Network (IPv4) in Azure

Dokumentasi ini menjelaskan langkah-langkah membuat Virtual Network (VNet) dengan alamat IPv4 khusus di Azure sebagai bagian dari infrastruktur jaringan DevOps.

---

## 🎯 Objective

Membuat Virtual Network dengan spesifikasi:
- **Name:** `devops-vnet`
- **Address space:** `192.168.0.0/24`
- **Subnet name:** `default` (atau nama bebas)
- **Subnet address range:** `192.168.0.0/24`
- **Region:** `(US) West US`
- **Resource Group:** Pilih resource group yang sudah tersedia (contoh: `kml_rg_main-...`).

---

## Step 1 — Navigasi ke Layanan Virtual Network

Ketik `Virtual Networks` pada kolom pencarian.

![images](/imgs_azure/day5.png)

---

## Step 2 — Inisialisasi Resource Baru

Klik tombol **+ Create** atau **+ Buat**.

![images](/imgs_azure/day5_1.png)

---

## Step 3 — Konfigurasi Dasar (Basics)

Isi formulir berikut:
- **Resource Group:** Pilih resource group yang sudah tersedia (misal: `kml_rg_main-...`).
- **Name:** `devops-vnet`
- **Region:** `(US) West US`

![images](/imgs_azure/day5_31.png)

---

## Step 4 — Pengaturan Alamat IP (Langkah Krusial)

Klik tab **IP Addresses** atau tombol **Next: IP Addresses**.

Hapus (ikon sampah) atau edit blok alamat default yang ada (biasanya `10.0.0.0/16`).

Pada kotak **IPv4 address space**, ketik:

- `192.168.0.0/24`

![images](/imgs_azure/day5_2.png)

Selanjutnya, buat subnet baru:

- Klik **+ Add subnet**.
- **Subnet name:** Masukkan nama bebas, misalnya `default`.
- **Subnet address range:** `192.168.0.0/24`
- Klik **Add**.

![images](/imgs_azure/day5_3.png)

---

## Step 5 — Validasi dan Finalisasi

Klik **Review + create**.

Pastikan muncul pesan **Validation passed**, lalu klik **Create**.

![images](/imgs_azure/day5_4.png)

---

## Step 6 — Verifikasi Akhir

![images](/imgs_azure/day5_6.png)