# Day 1: Linux User Setup with Non-Interactive Shell

---

## Tahap 1: Akses Server (SSH)

Melakukan remote login dari jump-host ke App Server 3 menggunakan protokol SSH.

```bash
ssh banner@stapp03
```
![images](/imgs_DevOps/Day1.png)

---

## Tahap 2: Pembuatan User dengan Shell Non-Interactive

Membuat user baru bernama `javed` sekaligus mengatur shell-nya ke `/sbin/nologin` (akses terbatas).

```bash
sudo useradd -s /sbin/nologin javed
```
![images](/imgs_DevOps/Day1(1).png)

---

## Tahap 3: Verifikasi Konfigurasi User

1. Cek UID dan GID user
   Memastikan user sudah terdaftar di sistem.

```bash
id javed
```
![images](/imgs_DevOps/Day1(1).png)

---

2. Cek konfigurasi di file passwd
   Memastikan path shell sudah benar.

```bash
grep javed /etc/passwd
```
![images](/imgs_DevOps/Day1(1).png)

---