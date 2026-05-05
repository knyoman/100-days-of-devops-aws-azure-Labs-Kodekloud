# Day 10: Linux Bash Scripts

Dokumentasi ini menjelaskan langkah-langkah membuat dan menjalankan bash script untuk backup website di App Server 2 dan mengirimkannya ke Storage Server.

---

## 🎯 Objective

Membuat script `<name>_backup.sh` di App Server 2 untuk mengkompresi folder dan mengirimkannya ke Storage Server tanpa password.

---

## Step 1: SSH ke App Server 2

```bash
ssh steve@stapp02
```
![images](/imgs_DevOps/day10.png)

---

## Step 2: Install Package zip

```bash
sudo yum install -y zip
```
![images](/imgs_DevOps/day10_1.png)

Verifikasi:

```bash
zip --version
```
![images](/imgs_DevOps/day10_2.png)

---

## Step 3: Setup SSH Key Passwordless ke Storage Server

Generate SSH key:

```bash
ssh-keygen -t rsa -b 2048
```
![images](/imgs_DevOps/day10_3.png)

Tekan Enter terus (tanpa passphrase).

Copy public key ke Storage Server:

```bash
ssh-copy-id natasha@ststor01
```
![images](/imgs_DevOps/day10_4.png)

Test koneksi:

```bash
ssh natasha@ststor01 "echo OK"
```
![images](/imgs_DevOps/day10_5.png)

---

## Step 4: Buat Direktori /scripts

```bash
sudo mkdir -p /scripts
sudo chown steve:steve /scripts
```
![images](/imgs_DevOps/day10_6.png)

---

## Step 5: Cek Direktori Website dan /backup

Cek direktori website:

```bash
ls /var/www/html/
```
![images](/imgs_DevOps/day10_7.png)

Catat Output buat ubah: `<name>`

Cek direktori backup:

```bash
ls -ld /backup
```
---

## Step 6: Buat Script news_backup.sh

Buat file script:

```bash
vi /scripts/news_backup.sh
```
Isi script (tekan `i`, paste kode berikut):

```bash
#!/bin/bash

SOURCE_DIR="/var/www/html/<name>"
BACKUP_DIR="/backup"
ARCHIVE_NAME="xfusioncorp_<name>.zip"
STORAGE_USER="natasha"
STORAGE_HOST="ststor01"
STORAGE_PATH="/backup"

zip -r "${BACKUP_DIR}/${ARCHIVE_NAME}" "${SOURCE_DIR}"

scp "${BACKUP_DIR}/${ARCHIVE_NAME}" "${STORAGE_USER}@${STORAGE_HOST}:${STORAGE_PATH}/"
```
![images](/imgs_DevOps/day10_8.png)

Simpan dan keluar (Esc → `:wq` → Enter).

---

## Step 7: Berikan Permission Eksekusi

```bash
chmod +x /scripts/<name>_backup.sh
```
![images](/imgs_DevOps/day10_9.png)

---

## Step 8: Jalankan Script

```bash
/scripts/<name>_backup.sh
```
![images](/imgs_DevOps/day10_10.png)

---

## Step 9: Verifikasi Final

Cek archive di App Server 2:

```bash
ls -lh /backup/xfusioncorp_<name>.zip
```
![images](/imgs_DevOps/day10_11.png)

Cek archive di Storage Server:

```bash
ssh natasha@ststor01 "ls -lh /backup/xfusioncorp_<name>.zip"
```
![images](/imgs_DevOps/day10_12.png)