# Day 3: Create VM using Azure CLI

---

### Tahap 1: Identifikasi Resource Group
Langkah awal untuk menentukan "kontainer" tempat VM akan dibuat.

```bash
az group list --output table
```
![images](/imgs_azure/Day3.png)

---

### Tahap 2: Pembuatan VM dengan Spesifikasi Lengkap
Langkah inti untuk membangun VM dengan parameter spesifik: Ubuntu 22.04, B2s, dan disk 30GB.

```bash
az vm create \
  --resource-group <NAMA_GRUP_DARI_TAHAP_1> \
  --name nautilus-vm \
  --image Ubuntu2204 \
  --size Standard_B2s \
  --admin-username azureuser \
  --generate-ssh-keys \
  --os-disk-size-gb 30 \
  --storage-sku Standard_LRS
```
![images](/imgs_azure/Day3(1).png)
---

### Tahap 3: Verifikasi Status "Running"
Memastikan bahwa VM tidak hanya terbuat, tapi sudah aktif dan berjalan (Running state).

```bash
az vm get-instance-view \
  --name nautilus-vm \
  --resource-group <NAMA_GRUP_DARI_TAHAP_1> \
  --query "instanceView.statuses[1].displayStatus" \
  --output table
```
![images](/imgs_azure/Day3(2).png)
---

### Tahap 4: Verifikasi Detail Disk & Size (Opsional)
Memastikan spesifikasi yang diminta sudah sesuai 100%.

```bash
az vm show \
  --name nautilus-vm \
  --resource-group <NAMA_GRUP_DARI_TAHAP_1> \
  --query "{Name:name, Size:hardwareProfile.vmSize, DiskSize:storageProfile.osDisk.diskSizeGb, State:provisioningState}" \
  --output json
```
![images](/imgs_azure/Day3(3).png)
---
