# Day 20: Deploy Azure Resources Using ARM Template

---

## Tahap 1 — Ambil Nama Resource Group

```bash
az group list --query '[].name' --output table | grep 'kml'
```
![images](/imgs_azure/day20.png)
> Salin nama Resource Group yang muncul (contoh: `kml_rg_main_xxxxxx`).
---

## Tahap 2 — Edit ARM Template

```bash
nano /root/arm-templates/vnet-deployment-template.json
```

Sesuaikan nilai berikut di dalam file:

| Field            | Value                  |
|------------------|------------------------|
| `name` (VNet)    | `arm-vnet-nautilus`    |
| `addressPrefixes` | `"192.168.0.0/16"`   |
| `tags.displayName` | `arm-vnet-nautilus` |
| `tags.Environment` | `KKE-nautilus`      |

Contoh struktur JSON setelah diedit:

```json
"name": "arm-vnet-nautilus",
"properties": {
    "addressSpace": {
        "addressPrefixes": [
            "192.168.0.0/16"
        ]
    }
},
"tags": {
    "displayName": "arm-vnet-nautilus",
    "Environment": "KKE-nautilus"
}
```
![images](/imgs_azure/day20_1.png)

Simpan: **Ctrl + O** → **Enter** → keluar: **Ctrl + X**.

---

## Tahap 3 — Deploy Template

Ganti `<NAMA_RESOURCE_GROUP>` dengan hasil dari Tahap 1.

```bash
az deployment group create \
  --resource-group <NAMA_RESOURCE_GROUP> \
  --template-file /root/arm-templates/vnet-deployment-template.json
```

![images](/imgs_azure/day20_2.png)
> ✅ Jika tidak ada error, Virtual Network berhasil di-deploy ke Azure.