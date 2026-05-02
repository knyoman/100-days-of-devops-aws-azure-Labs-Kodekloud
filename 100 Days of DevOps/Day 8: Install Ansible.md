# Day 8: Install Ansible

Dokumentasi ini menjelaskan langkah-langkah menginstal Ansible 4.9.0 secara global di Jump Host menggunakan pip3.

---

## 🎯 Objective

Menginstal Ansible versi `4.9.0` secara global dan memastikan binary tersedia bagi semua user.

---

## Step 1: Install Ansible via pip3

Jalankan perintah berikut di jump host dengan `sudo`:

```bash
sudo pip3 install ansible==4.9.0
```
![images](/imgs_DevOps/day8.png)

---

## Step 2: Verifikasi Instalasi

Pastikan Ansible sudah terinstal dan versinya benar:

```bash
ansible --version
```

![images](/imgs_DevOps/day8_1.png)

Jika muncul `command not found`, artinya binary Ansible belum tersedia di path global.

---

### Step Opsional ⬇️

---

## Step 3: Buat Binary Tersedia Secara Global

Jika perlu, buat symbolic link ke direktori binary global:

```bash
sudo ln -s $(which ansible) /usr/bin/ansible
```
![images](/imgs_DevOps/day8_2.png)

---

## Step 4: Verifikasi Akhir

Jalankan ulang:

```bash
ansible --version
```

Pastikan output menampilkan `ansible 4.9.0`.
