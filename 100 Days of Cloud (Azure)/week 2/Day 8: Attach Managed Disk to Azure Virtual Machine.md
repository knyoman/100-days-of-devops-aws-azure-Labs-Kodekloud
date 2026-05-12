# Day 8: Attach Managed Disk to Azure Virtual Machine

Dokumentasi ini menjelaskan langkah-langkah memasang managed disk ke VM Azure menggunakan portal.

---

## 🎯 Objective

Attach managed disk `nautilus-disk` ke VM `nautilus-vm` melalui Azure Portal.

---

## Step 1: Cari dan Pilih Virtual Machine

Ketik `Virtual machines` di kolom pencarian atas portal Azure.

Pilih + Klik VM `nautilus-vm`.

![images](/imgs_azure/day8.png)

---

## Step 2: Akses Menu Pengaturan Disk

Di menu sebelah kiri, di bawah **Settings**, klik **Disks**.

![images](/imgs_azure/day8_1.png)

---

## Step 3: Lampirkan Disk yang Sudah Ada

Scroll ke bagian **Data disks**.

Klik **Attach existing disks**.

Pada kolom **Disk name**, pilih `nautilus-disk` dari dropdown.

Klik tombol **Save**.

![images](/imgs_azure/day8_2.png)

---

## Step 4: Verifikasi Akhir

Pastikan disk `nautilus-disk` kini terdaftar di bagian Data disks pada VM `nautilus-vm`.

