# Day 11: Change Azure Virtual Machine Size Using Console
> **Task:** Resize `Standard_B1s` → `Standard_B2s` | Region: `West US`

---

## 01 · LOGIN

```
URL      → https://portal.azure.com
User     → kk_lab_user_main-a6c054fc9d274fab@azurefreekmlprod.onmicrosoft.com
Password → 8x489aSs
```

---

## 02 · BUKA VM

```
Search Bar → ketik: nautilus-vm
            → klik hasil yang muncul
```

![images](/imgs_azure/day11.png)

---

## 03 · STOP VM

```
Overview → klik [Stop]
         → konfirmasi [Yes]
         → tunggu status: Stopped (deallocated) ✓
```
![images](/imgs_azure/day11_1.png)

> ⚠️ Jangan lanjut sebelum status **deallocated**

---

## 04 · RESIZE

```
Sidebar → Settings → Size
        → search: Standard_B2s
        → pilih: Standard_B2s
        → klik [Resize]
        → tunggu proses selesai ✓
```
![images](/imgs_azure/day11_2.png)

---

## 05 · START VM

```
Overview → klik [Start]
         → tunggu status: Running ✓
```
![images](/imgs_azure/day11_3.png)

---
