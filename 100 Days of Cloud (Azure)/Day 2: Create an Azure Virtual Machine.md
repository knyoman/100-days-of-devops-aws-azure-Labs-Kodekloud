# Day 2: Pembuatan Virtual Machine via GUI
---

### Tahap 1: Inisialisasi Resource VM

Tindakan: Klik ikon "Mesin virtual" (Virtual Machines) di dashboard utama, lalu klik "Buat" -> "Mesin virtual Azure".

![images](/imgs_azure/Day2.png)

---

### Tahap 2: Pengisian Detail Dasar (Basics)

- Resource Group: Pilih yang sudah ada (misal: `kml_rg_main-...`).
- Nama VM: Isi dengan `datacenter-vm`.
- Wilayah (Region): Pilih `(US) West US`.
- Opsi Ketersediaan: Pilih "Tidak diperlukan redundansi infrastruktur".
- Citra (Image): Pilih `Ubuntu Server 24.04 LTS - x64 Gen2`.
- Ukuran (Size): Klik "Lihat semua ukuran", cari dan pilih `Standard_B1s`.

![images](/imgs_azure/Day2(1).png)

---

### Tahap 3: Konfigurasi Autentikasi SSH

Langkah-langkah:
- Jenis Autentikasi: Pilih Kunci publik SSH.
- Nama Pengguna: Isi `azureuser`.
- Sumber Kunci: Pilih "Gunakan kunci yang ada yang disimpan di Azure".
- Kunci yang Disimpan: Pilih kunci `nautilus-kp` yang sudah dibuat di Day 1.

![images](/imgs_azure/Day2(2).png)

---

### Tahap 4: Pengaturan Penyimpanan (Disks)

Langkah-langkah:
- Klik tab "Disk" di bagian atas atau bawah.
- Tipe Disk OS: Pilih `Standard HDD (LRS)`.
- Periksa ukurannya, pastikan sudah `30 GiB`.

![images](/imgs_azure/Day2(3).png)

---

### Tahap 5: Konfigurasi Jaringan & NSG (Networking)

Langkah-langkah:
- Klik tab "Jaringan".
- Grup keamanan jaringan NIC: Pilih `Dasar`.
- Port Masuk Publik: Pilih `Izinkan port yang dipilih`.
- Pilih port masuk: Centang `SSH (22)`.

![images](/imgs_azure/Day2(4).png)

---

### Tahap 6: Validasi dan Deployment

Tindakan: Klik "Tinjau + buat", tunggu validasi lulus, lalu klik "Buat".

![images](/imgs_azure/Day2(5).png)


