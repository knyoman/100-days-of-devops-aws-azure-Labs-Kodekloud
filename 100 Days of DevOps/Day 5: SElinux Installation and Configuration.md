# Day 5: SElinux Installation and Configuration

Dokumentasi ini menjelaskan langkah-langkah instalasi dan konfigurasi SELinux pada server Linux sebagai bagian dari pengelolaan keamanan sistem.

---

## 🎯 Objective

Menginstal paket SELinux dan mengkonfigurasi statusnya menjadi disabled secara permanen melalui file konfigurasi.

- **Status SELinux:** `disabled`
- **File Konfigurasi:** `/etc/selinux/config`

---

## Step 1 — Login ke App Server 1

Login ke server target menggunakan SSH.

```bash
ssh tony@stapp01
```
![images](/imgs_DevOps/day5.png)

---

## Step 2 — Install Package SELinux

Instal paket-paket utama yang dibutuhkan untuk menjalankan SELinux menggunakan yum.

```bash
sudo yum install policycoreutils policycoreutils-python-utils selinux-policy selinux-policy-targeted libselinux-utils -y
```
![images](/imgs_DevOps/day5_1.png)

---

## Step 3 — Konfigurasi Permanen ke Status "Disabled"

Buka file konfigurasi SELinux untuk mengubah status secara permanen.

```bash
sudo vi /etc/selinux/config
```

Cari baris yang bertuliskan `SELINUX=enforcing` atau `SELINUX=permissive`, lalu ubah menjadi:

```
SELINUX=disabled
```

Simpan perubahan (dalam vi: tekan `i` untuk edit, ubah nilainya, tekan `Esc`, lalu ketik `:wq`).

![images](/imgs_DevOps/day5_2.png)

---

## Step 4 — Verifikasi Tanpa Reboot

Verifikasi isi file konfigurasi tanpa melakukan reboot.

```bash
cat /etc/selinux/config | grep "^SELINUX="
```

![images](/imgs_DevOps/day5_3.png)
