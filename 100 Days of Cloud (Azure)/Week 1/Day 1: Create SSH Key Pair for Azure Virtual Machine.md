# Day 1: Create SSH Key Pair for Azure Virtual Machine

---

### Tahap 1: Akses Layanan SSH Keys

**Tindakan:**
- Pada kolom pencarian di bagian atas Azure Portal, ketik `"SSH Keys"`
- Pilih layanan tersebut dari daftar hasil

![images](/imgs_azure/Day1.png)

---

### Tahap 2: Inisialisasi Pembuatan (Create)

**Tindakan:**
- Klik tombol `"+ Create"` (atau `"+ Buat"`) di pojok kiri atas halaman SSH Keys
![images](/imgs_azure/Day1(1).png)
---

### Tahap 3: Pengisian Detail Resource & Instance

**Langkah-langkah:**

1. **Resource Group**
   - Pilih grup yang sudah ada (Contoh: `kml_rg_main-...`)

2. **Region**
   - Pilih `East US`

3. **Name**
   - Isi dengan `nautilus-kp`

4. **SSH Key Source**
   - Pilih `"Generate new key pair"`

![images](/imgs_azure/Day1(2).png)
---

### Tahap 4: Penentuan Tipe Kunci

**Tindakan:**
- Pastikan pada bagian **Key pair type**, yang terpilih adalah `RSA`
![images](/imgs_azure/Day1(3).png)
---
