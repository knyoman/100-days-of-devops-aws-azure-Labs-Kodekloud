# Day 4: Create a Virtual Network (VNet) in Azure

### Tahap 1: Akses Menu Virtual Network

Pada kolom pencarian di bagian paling atas, ketik **Virtual Networks**, lalu pilih layanan tersebut.

![images](/imgs_azure/day4.png)

---

### Tahap 2: Inisialisasi Pembuatan

Klik tombol "+ Create" (atau "+ Buat") di pojok kiri atas.

![images](/imgs_azure/day4_1.png)

---

### Tahap 3: Konfigurasi Dasar (Basics)

**Tindakan:**
- Resource Group: Pilih yang sudah tersedia (misal: kml_rg_main-...).
- Name: Isi dengan **nautilus-vnet**.
- Region: Pilih (US) **South Central US**.

![images](/imgs_azure/day4_2.png)

---

### Tahap 4: Pengaturan IP Addresses (Langkah Krusial)

**Tindakan:**
- Klik tab "IP Addresses" di bagian atas.
- IPv4 address space: Secara default **10.0.0.0/16**
- Subnets: Klik "+ Add subnet".
- Subnet name: default atau **nautilus-subnet**.
- Subnet address ukuran: **24**.
- Klik Add.

![images](/imgs_azure/day4_3.png)

---

### Tahap 5: Keamanan & Peninjauan (Security & Review)

**Tindakan:**
- Klik "Review + create"
- Setelah muncul tulisan hijau "Validation passed", klik "Create".

![images](/imgs_azure/day4_4.png)

---