# Day 6: Create a Subnet in Azure Virtual Network

Dokumentasi ini menjelaskan langkah-langkah membuat Subnet dalam Virtual Network di Azure sebagai bagian dari infrastruktur jaringan.

---

## 🎯 Objective

Membuat Virtual Network dan Subnet dengan spesifikasi:
- **Virtual Network Name:** `devops-vnet`
- **IPv4 address space:** `10.0.0.0/16`
- **Subnet name:** `devops-subnet`
- **Subnet address range:** `10.0.0.0/24`
- **Region:** `(US) South Central US`
- **Resource Group:** Pilih resource group yang sudah tersedia (misal: `kml_rg_main-...`).

---

## Step 1: Akses Menu Virtual Network

Ketik `Virtual Networks` di kolom pencarian atas dan pilih layanan tersebut.

![images](/imgs_azure/day6.png)

---

## Step 2: Konfigurasi Dasar (Basics)

Klik **+ Create**.

Isi formulir dasar:

- **Resource Group:** Pilih yang sudah tersedia (misal: `kml_rg_main-...`).
- **Name:** `devops-vnet`
- **Region:** `(US) South Central US`

![images](/imgs_azure/day6_1.png)

---

## Step 3: Pengaturan Alamat IP dan Subnet

Klik tab **IP Addresses**.

Pastikan **IPv4 address space** terisi: `10.0.0.0/16`.

Tambahkan subnet baru:

- Klik **+ Add subnet**.
- **Subnet name:** `devops-subnet`
- **Subnet address range:** `10.0.0.0/24`
- Klik **Add**.

![images](/imgs_azure/day6_2.png)

---

## Step 4: Validasi dan Finalisasi

Klik **Review + create**.

Pastikan validasi lulus, lalu klik **Create**.

![images](/imgs_azure/day6_3.png)

---

## Step 5: Verifikasi Akhir

![images](/imgs_azure/day6_4.png)

---

## Step 6: Cek Resource Group Name

```bash
az group list --output table
```

![images](/imgs_azure/day6_5.png)

---

## Step 7: Cek VNet

```bash
az network vnet show \
  --name devops-vnet \
  --resource-group <resource-group-name> \
  --query "{Name:name,Address:addressSpace.addressPrefixes,Location:location}"
```

![images](/imgs_azure/day6_6.png)

---

## Step 8: Cek Subnet

```bash
az network vnet subnet show \
  --name devops-subnet \
  --vnet-name devops-vnet \
  --resource-group <resource-group-name>
```

![images](/imgs_azure/day6_7.png)

---

## Step9: Verifikasi Public IP Azure via CLI (Opsional)

### 1. Menampilkan Detail Public IP

```bash
az network public-ip show \
  --name devops-pip \
  --resource-group <resource-group-name> \
  --query "{Name:name,IP:ipAddress,SKU:sku.name,Assignment:publicIPAllocationMethod,Region:location}" \
  --output table
```

--- 

### 2. Melihat Daftar Public IP dalam Resource Group

```bash
az network public-ip list \
  --resource-group <resource-group-name> \
  --output table
```

--- 

### 3. Mengecek Status Resource

```bash
az resource show \
  --resource-group <resource-group-name> \
  --name devops-pip \
  --resource-type "Microsoft.Network/publicIPAddresses"
```

--- 