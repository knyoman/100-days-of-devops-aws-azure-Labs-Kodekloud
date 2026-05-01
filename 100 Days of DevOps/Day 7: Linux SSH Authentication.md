# Day 7: Linux SSH Authentication

Dokumentasi ini menjelaskan langkah-langkah mengonfigurasi SSH Key-Based Authentication agar user thor di jump host dapat login ke semua app servers tanpa password.

---

## 🎯 Objective

Mengatur autentikasi SSH berbasis kunci untuk koneksi tanpa password dari jump host ke:
- `tony@stapp01`
- `steve@stapp02`
- `banner@stapp03`

---

## Step 1: Generate SSH Key di Jump Host

Login ke jump host sebagai user `thor`.

Generate pasangan kunci RSA:

```bash
ssh-keygen -t rsa -b 2048 -N "" -f ~/.ssh/id_rsa
```

![images](/imgs_DevOps/day7.png)

---

## Step 2: Kirim Public Key ke Semua App Server

Salin public key ke masing-masing server aplikasi menggunakan [`ssh-copy-id`].

**Ke App Server 1:**

```bash
ssh-copy-id tony@stapp01
```

![images](/imgs_DevOps/day7_1.png)


**Ke App Server 2:**

```bash
ssh-copy-id steve@stapp02
```

![images](/imgs_DevOps/day7_2.png)

**Ke App Server 3:**

```bash
ssh-copy-id banner@stapp03
```

![images](/imgs_DevOps/day7_3.png)

---

## Step 3: Verifikasi Hasilnya

login SSH dari jump host ke setiap server. Jika berhasil, masuk tanpa diminta password.

**Test ke App Server 1:**

```bash
ssh tony@stapp01
exit
```
![images](/imgs_DevOps/day7_4.png)

**Test ke App Server 2:**

```bash
ssh steve@stapp02
exit
```
![images](/imgs_DevOps/day7_5.png)

**Test ke App Server 3:**

```bash
ssh banner@stapp03
exit
```

![images](/imgs_DevOps/day7_6.png)