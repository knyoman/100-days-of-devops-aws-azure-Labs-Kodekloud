# Day 7: Create a Public IP Address for Azure VM

Dokumentasi ini menjelaskan langkah-langkah membuat Public IP Address di Azure untuk VM.

---

## 🎯 Objective

Membuat Public IP Address dengan spesifikasi:
- **Name:** `devops-pip`
- **SKU:** `Standard`
- **Tier:** `Regional`
- **IP Version:** `IPv4`
- **Assignment:** `Static`
- **Resource Group:** Pilih yang tersedia (misal: `kml_rg_main-...`)
- **Region:** Pilih wilayah yang sama dengan resource group kamu

---

## Step 1: Akses Menu Public IP Addresses

Ketik `Public IP addresses` di kolom pencarian atas dan pilih layanan tersebut.



---

## Step 2 : Inisialisasi Resource Baru

Klik tombol **+ Create** atau **+ Buat**.

---

## Step 3: Pengisian Detail Resource

Isi detail berikut:

- **Subscription:** Biarkan default.
- **Resource Group:** Pilih yang sudah tersedia.
- **Name:** `devops-pip`
- **Region:** Pilih wilayah yang sama dengan resource group.
- **SKU:** `Standard`
- **Tier:** `Regional`
- **IP Version:** `IPv4`
- **Assignment:** `Static`

---

## Step 4: Validasi dan Deployment

Klik **Review + create**.

Pastikan muncul pesan hijau **Validation passed**, lalu klik **Create**.

---

## Step 5: Verifikasi Akhir

