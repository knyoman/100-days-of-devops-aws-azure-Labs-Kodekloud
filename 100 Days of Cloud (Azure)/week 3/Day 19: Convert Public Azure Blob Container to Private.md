# Day 19: Convert Public Azure Blob Container to Private

---

## Tahap 1 — Login ke Azure Portal

| Field    | Value |
|----------|-------|
| URL      | `https://portal.azure.com` |
| Username | `kk_lab_user_main-7caf0d0601084634@azurefreekmlprod.onmicrosoft.com` |
| Password | `z&ut#ZZJ` |

---

## Tahap 2 — Navigasi ke Storage Account

Search bar → ketik **Storage accounts** → klik **`nautilusst30941`**.

![images](/imgs_azure/day19.png)
---

## Tahap 3 — Buka Containers

Panel kiri → **Data storage** → **Containers**.

| Container | Status Awal | Aksi |
|-----------|-------------|------|
| `nautilus-container-23504` | Public | ✏️ Ubah |
| `nautilus-priv-10054` | Private | 🚫 Jangan diubah |

![images](/imgs_azure/day19_1.png)
---

## Tahap 4 — Ubah Access Level

Klik `nautilus-container-23504` → **Change access level**

> Alternatif: klik **⋯** di sebelah kanan container → **Change access level**.

Pada dropdown **Public access level** pilih **Private (no anonymous access)** → klik **OK**.

![images](/imgs_azure/day19_2.png)
---

## Tahap 5 — Verifikasi

Kembali ke daftar **Containers**, pastikan:

- `nautilus-container-23504` → kolom Public access level: **Private**
- `nautilus-priv-10054` → tetap **Private** (tidak berubah)

![images](/imgs_azure/day19_3.png)
> ✅ Access level berhasil diubah.

---

## Tahapan Pakai CLI (Opsional)

```bash
az storage container set-permission \
  --name nautilus-container-23504 \
  --account-name nautilusst30941 \
  --public-access off \
  --auth-mode login
```

![images](/imgs_azure/day19_4.png)

## Verifikasi

```bash
az storage container show \
  --name nautilus-container-23504 \
  --account-name nautilusst30941 \
  --query properties.publicAccess \
  --output tsv
```

![images](/imgs_azure/day19_5.png)
> Jika level aksesnya Public, outputnya akan tertulis container atau blob
> ✅ Jika level aksesnya Private (No public access), nilainya secara teknis adalah null