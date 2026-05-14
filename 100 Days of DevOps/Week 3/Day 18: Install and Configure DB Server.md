# 🗄️ Day 18 — Install & Configure MariaDB Server

---

## Step 1 SSH ke DB Server

```bash
ssh peter@stdb01
```
![images](/imgs_DevOps/Day18_18.png)

---

## Step 2 Install MariaDB

```bash
# CentOS/RHEL
sudo yum install -y mariadb-server mariadb

# Ubuntu/Debian
sudo apt-get update && sudo apt-get install -y mariadb-server
```
![images](/imgs_DevOps/Day18_18_1.png)

---

## Step 3 Start & Enable Service

```bash
sudo systemctl start mariadb
sudo systemctl enable mariadb
sudo systemctl status mariadb
```

![images](/imgs_DevOps/Day18_18_2.png)

---

## Step 4 Login sebagai Root

```bash
sudo mysql -u root
```
![images](/imgs_DevOps/Day18_18_3.png)

> Jika diminta password dan belum diset, langsung tekan **Enter**.

---

## Step 5 Buat Database

```sql
CREATE DATABASE kodekloud_db6;
```
![images](/imgs_DevOps/Day18_18_4.png)

---

## Step 6 Buat User

```sql
CREATE USER 'kodekloud_sam'@'localhost' IDENTIFIED BY 'TmPcZjtRQx';
```
![images](/imgs_DevOps/Day18_18_5.png)

---

## Step 7 Grant Permissions

```sql
GRANT ALL PRIVILEGES ON kodekloud_db6.* TO 'kodekloud_sam'@'localhost';
```
![images](/imgs_DevOps/Day18_18_6.png)
---

## Step 8 Flush & Keluar

```sql
FLUSH PRIVILEGES;
EXIT;
```
![images](/imgs_DevOps/Day18_18_7.png)

---

## Step 9 Verifikasi

```bash
# Cek database
sudo mysql -u root -e "SHOW DATABASES;"

# Cek user & grant
sudo mysql -u root -e "SELECT user, host FROM mysql.user WHERE user='kodekloud_sam';"
sudo mysql -u root -e "SHOW GRANTS FOR 'kodekloud_sam'@'localhost';"

# Test login user baru
mysql -u kodekloud_sam -pTmPcZjtRQx kodekloud_db6
```
![images](/imgs_DevOps/Day18_18_8.png)
![images](/imgs_DevOps/Day18_18_9.png)
![images](/imgs_DevOps/Day18_18_10.png)
![images](/imgs_DevOps/Day18_18_11.png)

> ✅ Jika masuk tanpa error, konfigurasi berhasil.