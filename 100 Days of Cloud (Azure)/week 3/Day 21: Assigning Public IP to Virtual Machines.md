# Day 21: Assigning Public IP to Virtual Machines

> Panduan membuat SSH key, mengonfigurasi Static Public IP, membuat Virtual Machine Ubuntu di Azure, dan koneksi via SSH.

---

## Langkah 0 — Generate SSH Key di Azure Client

Buka terminal `azure-client`, lalu jalankan:

```bash
ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa -N ""
```

Tampilkan dan **salin** public key:

```bash
cat ~/.ssh/id_rsa.pub
```
![images](/imgs_azure/day21.png)

> Simpan output `ssh-rsa AAAA...` — akan di-paste ke portal pada Langkah 3.

---

## Langkah 1 — Login Azure Portal

Buka [https://portal.azure.com](https://portal.azure.com)

| Field | Value |
|---|---|
| Username | `kk_lab_user_main-bc231a82de554577@azurefreekmlprod.onmicrosoft.com` |
| Password | `5KNb+Ckw` |

---

## Langkah 2 — Buat Static Public IP (`xfusion-pip`)

**Public IP addresses** → **+ Create**

| Field | Value |
|---|---|
| Subscription | Pilih yang tersedia |
| Resource Group | `kml_rg_main-bc231a82de554577` |
| Region | Central US |
| Name | `xfusion-pip` |
| IP Version | IPv4 |
| SKU | Standard |
| Assignment | Static |
| Availability Zone | No Zone |

Klik **Review + Create → Create** → tunggu hingga selesai ✅

![images](/imgs_azure/day21_1.png)
---

## Langkah 3 — Buat Virtual Machine (`xfusion-vm`)

**Virtual Machines** → **+ Create → Azure virtual machine**

### 🔹 Tab Basics

| Field | Value |
|---|---|
| Resource Group | `kml_rg_main-bc231a82de554577` |
| Virtual machine name | `xfusion-vm` |
| Region | (US) Central US |
| Image | Ubuntu Server 22.04 LTS |
| Size | Standard_B1s |
| Authentication type | SSH public key |
| Username | `azureuser` |
| SSH public key source | Use existing public key |
| SSH public key | Paste output `cat ~/.ssh/id_rsa.pub` |
| Public inbound ports | Allow selected ports |
| Select inbound ports | SSH (22) |

![images](/imgs_azure/day21_2.png)
---

### 🔹 Tab Disks ⚠️ PENTING

| Field | Value |
|---|---|
| OS disk type | **Standard SSD** (locally redundant storage) |
| OS disk size | Biarkan default |

> ❌ **Jangan pilih Premium SSD** — akan ditolak oleh policy lab!

![images](/imgs_azure/day21_4.png)
---

### 🔹 Tab Networking

| Field | Value |
|---|---|
| Virtual network | Buat baru atau default |
| Subnet | default |
| Public IP | Pilih `xfusion-pip` dari dropdown |
| NIC network security group | Basic |
| Public inbound ports | Allow selected ports |
| Select inbound ports | SSH (22) |

---

### 🔹 Tab Management, Monitoring, Advanced

Semua biarkan **default**.

### 🔹 Tab Review + Create

Pastikan validasi hijau ✅ → klik **Create** → tunggu ~2-3 menit

![images](/imgs_azure/day21_3.png)
---

## Langkah 4 — Verifikasi & Test SSH

Setelah deployment selesai:

1. Klik **Go to resource**
2. Catat **Public IP address** dari `xfusion-pip`
3. Kembali ke terminal `azure-client`:

```bash
ssh -i ~/.ssh/id_rsa azureuser@<PUBLIC_IP>
```

Jika berhasil, Anda akan masuk ke VM `xfusion-vm` ✅

![images](/imgs_azure/day21_6.png)
---

### Ringkasan Resource yang Dibuat

| Resource | Nama | Keterangan |
|---|---|---|
| Public IP | `xfusion-pip` | Static IPv4, SKU Standard |
| Virtual Machine | `xfusion-vm` | Ubuntu 22.04, Standard_B1s |
| Disk | Default | Standard SSD |
| Auth | SSH Key | `~/.ssh/id_rsa` |

---

> 💡 **Tips:** Jika koneksi SSH gagal, pastikan inbound rule port **22** sudah aktif di Network Security Group VM dan IP yang digunakan sudah benar dari portal.