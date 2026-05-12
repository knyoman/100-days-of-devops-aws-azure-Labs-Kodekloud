# Day 9: Attach Network Interface Card (NIC) to Azure Virtual Machine

Dokumentasi ini menjelaskan langkah-langkah memasang NIC tambahan ke VM `nautilus-vm` di Azure.

---

## 🎯 Objective

Attach existing NIC `nautilus-nic` ke VM `nautilus-vm` dan pastikan VM kembali berjalan.

---

## Step 1: Masuk ke Menu nautilus-vm

Di Azure Portal, klik **Virtual machines**, lalu pilih `nautilus-vm`.

![images](/imgs_azure/day9.png)

---

## Step 2: Matikan VM Terlebih Dahulu

Di halaman **Overview** nautilus-vm, klik **Stop**.

Tunggu sampai status berubah menjadi **Stopped (deallocated)**.

![images](/imgs_azure/day9_1.png)

---

## Step 3: Akses Menu Pengaturan Jaringan

Di panel kiri, di bawah **Settings**, klik **Networking**.
![images](/imgs_azure/day9_2.png)

---

## Step 4: Lampirkan NIC yang Sudah Ada

Di halaman **Networking**, klik **Attach network interface**.

Pilih `nautilus-nic` dari daftar dropdown.

Klik **OK** atau **Save**.

![images](/imgs_azure/day9_3.png)

---

## Step 5: Jalankan Kembali VM

Kembali ke halaman **Overview**, lalu klik **Start**.

Tunggu sampai VM kembali menyala dan NIC `nautilus-nic` terbaca terpasang.

![images](/imgs_azure/day9_4.png)

---

## Step 6 — Verifikasi Akhir

Pastikan `nautilus-vm` sudah berjalan kembali setelah NIC terpasang.

![images](/imgs_azure/day9_5.png)
