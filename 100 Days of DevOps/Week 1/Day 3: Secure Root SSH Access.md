# Day 3: SSH Configuration on All App Servers

Instruksi ini harus dilakukan di ketiga App Server: App Server 1 (`stapp01`), App Server 2 (`stapp02`), dan App Server 3 (`stapp03`). Ulangi langkah-langkah berikut di setiap server.

---

## Tahap 1: Login ke App Server
Masuk ke server satu per satu menggunakan detail SSH dari tabel.

Contoh:

```bash
ssh user@stapp01
```
![images](/imgs_DevOps/day3.png)

Ulangi untuk:
- `stapp01`
- `stapp02`
- `stapp03`
---

## Tahap 2: Ubah konfigurasi SSH untuk menonaktifkan login root

```bash
sudo sed -i 's/PermitRootLogin yes/PermitRootLogin no/g' /etc/ssh/sshd_config
```
![images](/imgs_DevOps/day3_1.png)
---

## Tahap 3: Restart Layanan SSH
Agar perubahan konfigurasi berlaku, restart service SSH.

```bash
sudo systemctl restart sshd
```
![images](/imgs_DevOps/day3_2.png)
---

## Tahap 4: Verifikasi Konfigurasi
Untuk mengecek apakah konfigurasi tersebut sudah berhasil dan aktif.

1. Cek Apakah Baris Konfigurasi Sudah Benar

```bash
sudo grep "PermitRootLogin" /etc/ssh/sshd_config
```
![images](/imgs_DevOps/day3_3.png)

2. Cek Status Service SSH

```bash
sudo systemctl status sshd
```
![images](/imgs_DevOps/day3_4.png)

3. Tes Login sebagai Root

```bash
ssh root@localhost
```
![images](/imgs_DevOps/day3_5.png)

Ulangi semua tahapan ini di setiap App Server agar semua server memiliki konfigurasi yang sama.

