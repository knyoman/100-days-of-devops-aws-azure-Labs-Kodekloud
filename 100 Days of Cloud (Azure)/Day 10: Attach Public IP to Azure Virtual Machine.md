# Day 10: Attach Public IP to Azure Virtual Machine

Dokumentasi ini menjelaskan langkah-langkah menghubungkan Public IP ke NIC dari VM di Azure melalui portal.

---

## 🎯 Objective

Attach Public IP `nautilus-pip` ke NIC dari VM `nautilus-vm-pip` agar VM dapat diakses dari internet.

---

## Step 1: Login ke Azure Portal

Akses Azure Portal menggunakan kredensial berikut:

- **Username:** `kk_lab_user_main-b63c7d7812274442@azurefreekmlprod.onmicrosoft.com`
- **Password:** `ka6f&bf4`

---

## Step 2: Cari Virtual Machine Anda

Ketik `Virtual Machines` di bilah pencarian atas dan pilih layanannya.

Klik pada nama VM: `nautilus-vm-pip`.

![images](/imgs_azure/day10.png)

---

## Step 3: Masuk ke Pengaturan Jaringan (Networking)

Di menu navigasi kiri, di bawah **Settings**, klik **Networking**.

Klik pada nama Network Interface (NIC) yang terpasang pada VM (biasanya berakhiran `-nic`).

![images](/imgs_azure/day10_1.png)

---

## Step 4: Konfigurasi IP pada Network Interface (NIC)

Di panel navigasi kiri NIC, klik **IP configurations**.

Klik pada konfigurasi IP yang ada (biasanya `ipconfig1`).

![images](/imgs_azure/day10_2.png)

---

## Step 5: Kaitkan Public IP

Di bagian **Public IP address**, ubah menjadi **Associate**.

Pilih `nautilus-pip` dari dropdown.

Klik **Save** di bagian atas untuk menerapkan perubahan.

![images](/imgs_azure/day10_3.png)

---

## Step 6: Verifikasi & Selesaikan Lab

Tunggu sampai "Successfully updated IP configuration".

![images](/imgs_azure/day10_4.png)

